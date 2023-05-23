---
title: Usuários de serviço no AEM
seo-title: Service Users in AEM
description: Saiba mais sobre Usuários de serviço no AEM.
seo-description: Learn about Service Users in AEM.
uuid: 4efab5fb-ba11-4922-bd68-43ccde4eb355
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 9cfe5f11-8a0e-4a27-9681-a8d50835c864
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Security
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 0%

---

# Usuários de serviço no AEM{#service-users-in-aem}

## Visão geral {#overview}

A principal maneira de obter uma sessão administrativa ou um resolvedor de recursos no AEM era usando o `SlingRepository.loginAdministrative()` e `ResourceResolverFactory.getAdministrativeResourceResolver()` métodos fornecidos pelo Sling.

No entanto, nenhum desses métodos foi projetado em torno do [princípio do privilégio mínimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege) e tornar muito fácil para um desenvolvedor não planejar uma estrutura adequada e os respectivos Níveis de controle de acesso (ACLs) para o conteúdo antecipadamente. Se uma vulnerabilidade estiver presente em um serviço desse tipo, ela geralmente leva a escaladas de privilégio para o `admin` mesmo se o código em si não precisasse de privilégios administrativos para funcionar.

## Como eliminar as sessões de administrador {#how-to-phase-out-admin-sessions}

### Prioridade 0: o recurso está ativo/necessário/abandonado? {#priority-is-the-feature-active-needed-derelict}

Pode haver casos em que a sessão de administrador não seja usada ou o recurso seja totalmente desativado. Se esse for o caso com sua implementação, remova o recurso completamente ou ajuste-o com [Código NOP](https://en.wikipedia.org/wiki/NOP).

### Prioridade 1: Usar A Sessão De Solicitação {#priority-use-the-request-session}

Sempre que possível, refatore seu recurso para que a sessão de solicitação fornecida e autenticada possa ser usada para ler ou gravar conteúdo. Caso tal não seja possível, pode muitas vezes conseguir-se aplicando as prioridades que se seguem.

### Prioridade 2: Reestruturar Conteúdo {#priority-restructure-content}

Muitos problemas podem ser resolvidos reestruturando o conteúdo. Lembre-se dessas regras simples ao fazer a reestruturação:

* **Alterar controle de acesso**

   * Certifique-se de que os usuários ou grupos que realmente precisam de acesso tenham acesso;

* **Refinar estrutura de conteúdo**

   * Movê-lo para outros locais, por exemplo, onde o controle de acesso corresponde às sessões de solicitação disponíveis;
   * Alterar a granularidade do conteúdo;

* **Refatorar seu código para ser um serviço adequado**

   * Mova a lógica de negócios do código JSP para o serviço. Isso permite modelagem de conteúdo diferente.

Além disso, verifique se os novos recursos desenvolvidos seguem estes princípios:

* **Os requisitos de segurança devem orientar a estrutura do conteúdo**

   * O gerenciamento do controle de acesso deve parecer natural
   * O controle de acesso deve ser aplicado pelo repositório, não pelo aplicativo

* **Usar tipos de nós**

   * Restringir o conjunto de propriedades que podem ser definidas

* **Respeitar as configurações de privacidade**

   * No caso de perfis privados, um exemplo seria não expor a imagem do perfil, o email ou o nome completo encontrado no `/profile` nó.

## Controle de acesso estrito {#strict-access-control}

Se você aplicar o controle de acesso ao reestruturar o conteúdo ou quando o fizer para um novo usuário de serviço, deverá aplicar as ACLs mais rigorosas possíveis. Usar todos os recursos possíveis de controle de acesso:

* Por exemplo, em vez de aplicar `jcr:read` em `/apps`, aplique-o somente a `/apps/*/components/*/analytics`

* Uso [restrições](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* Aplicar ACLs para tipos de nó
* Limitar permissões

   * por exemplo, quando precisar apenas gravar propriedades, não forneça a `jcr:write` permissão; usar `jcr:modifyProperties` em vez disso

## Usuários e Mapeamentos do Serviço {#service-users-and-mappings}

Se o procedimento acima falhar, o Sling 7 oferecerá um serviço de Mapeamento de usuários do serviço, que permite configurar um mapeamento de pacote para usuário e dois métodos de API correspondentes: ` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)` e ` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)` que retornam um resolvedor de sessão/recurso com os privilégios somente de um usuário configurado. Esses métodos têm as seguintes características:

* Eles permitem serviços de mapeamento para usuários
* Eles permitem definir usuários de subserviço
* O ponto de configuração central é: `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name` [ &quot;:&quot; subservice-name ] 

* `service-id` é mapeado para um resolvedor de recursos e/ou ID de usuário do repositório JCR para autenticação
* `service-name` é o nome simbólico do pacote que fornece o serviço

## Outro Recommendations {#other-recommendations}

### Substituição da sessão de administrador por um usuário de serviço {#replacing-the-admin-session-with-a-service-user}

Um usuário de serviço é um usuário JCR sem senha definida e com um conjunto mínimo de privilégios necessários para executar uma tarefa específica. Não ter senha definida significa que não será possível fazer logon com um usuário de serviço.

Uma maneira de descontinuar uma sessão administrativa é substituí-la por sessões de usuário de serviço. Ele também pode ser substituído por vários usuários de subserviço, se necessário.

Para substituir a sessão de administrador por um usuário de serviço, execute as seguintes etapas:

1. Identifique as permissões necessárias para seu serviço, tendo em mente o princípio de menos permissão.
1. Verifique se já existe um usuário disponível com exatamente a configuração de permissão necessária. Crie um novo usuário de serviço do sistema se nenhum usuário existente atender às suas necessidades. O RTC é necessário para criar um novo usuário de serviço. Às vezes, faz sentido criar vários usuários de subserviço (por exemplo, um para gravação e outro para leitura) para compartimentalizar ainda mais o acesso.
1. Configurar e testar ACEs para o usuário.
1. Adicionar um `service-user` mapeamento para seu serviço e para `user/sub-users`

1. Disponibilize o recurso sling do usuário de serviço para o seu pacote: atualização para a versão mais recente do `org.apache.sling.api`.

1. Substitua o `admin-session` em seu código com o `loginService` ou `getServiceResourceResolver` APIs.

## Criando um novo usuário de serviço {#creating-a-new-service-user}

Depois de verificar que nenhum usuário na lista de usuários do serviço AEM se aplica ao seu caso de uso e que os problemas de RTC correspondentes foram aprovados, você pode adicionar o novo usuário ao conteúdo padrão.

A abordagem recomendada é criar um usuário de serviço para usar o explorador do repositório em *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*

O objetivo é obter um certificado válido `jcr:uuid` propriedade obrigatória para criar o usuário por meio de uma instalação de pacote de conteúdo.

Você pode criar usuários de serviço ao:

1. Acessar o explorador de repositório em *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*
1. Para fazer logon como administrador, pressione a tecla **Fazer logon** no canto superior esquerdo da tela.
1. Em seguida, crie e nomeie o usuário do sistema. Para criar o usuário como um sistema, defina o caminho intermediário como `system` e adicione subpastas opcionais de acordo com suas necessidades:

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. Verifique se o nó do usuário do sistema tem a seguinte aparência:

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >Observe que não há tipos de mixin associados a usuários de serviço. Isso significa que não haverá políticas de controle de acesso para usuários do sistema.

Ao adicionar o .content.xml correspondente ao conteúdo do pacote, verifique se você definiu o `rep:authorizableId` e que o tipo primário é `rep:SystemUser`. Deve ter esta aparência:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## Adicionando uma alteração de configuração à configuração ServiceUserMapper {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

Para adicionar um mapeamento de seu serviço para os Usuários do sistema correspondentes, é necessário criar uma configuração de fábrica para o ` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)` serviço. Para manter essa configuração modular, essas configurações podem ser fornecidas usando o [Mecanismo de alteração do Sling](https://issues.apache.org/jira/browse/SLING-3578). A maneira recomendada de instalar essas configurações com seu pacote é usando [Carregamento do conteúdo inicial do Sling](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. Crie uma subpasta SLING-INF/content abaixo da pasta src/main/resources do seu pacote
1. Nesta pasta, crie um arquivo chamado org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.ended-&lt;some unique=&quot;&quot; name=&quot;&quot; for=&quot;&quot; your=&quot;&quot; factory=&quot;&quot; configuration=&quot;&quot;>.xml com o conteúdo da configuração de fábrica (incluindo todos os mapeamentos de usuário de subserviço). Exemplo:

1. Criar um `SLING-INF/content` pasta abaixo do `src/main/resources` pasta do seu pacote;
1. Nesta pasta, crie um arquivo `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` com o conteúdo da configuração de fábrica, incluindo todos os mapeamentos de subserviço de usuário.

   Para fins ilustrativos, use o arquivo chamado `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <node>
       <primaryNodeType>sling:OsgiConfig</primaryNodeType>
       <property>
           <name>user.default</name>
           <value></value>
       </property>
       <property>
           <name>user.mapping</name>
           <values>
               <value>com.adobe.granite.auth.saml=authentication-service</value>
           </values>
       </property>
   </node>
   ```

1. Faça referência ao conteúdo inicial do Sling na configuração do `maven-bundle-plugin` no `pom.xml` do seu pacote. Exemplo:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. Instale seu pacote e verifique se a configuração de fábrica foi instalada. Você pode fazer isso ao:

   * Acessando o console da Web em *https://serverhost:serveraddress/system/console/configMgr*
   * Pesquisar por **Aditamento do serviço Mapeador de usuários do Apache Sling Service**
   * Clique no link para ver se a configuração apropriada está em vigor.

## Lidar com sessões compartilhadas em serviços {#dealing-with-shared-sessions-in-services}

Chamadas para `loginAdministrative()` aparecem frequentemente junto com sessões compartilhadas. Essas sessões são adquiridas na ativação do serviço e só são desconectadas após a interrupção do serviço. Embora essa seja uma prática comum, ela gera dois problemas:

* **Segurança:** Essas sessões administrativas são usadas para armazenar em cache e retornar recursos ou outros objetos vinculados à sessão compartilhada. Mais tarde na pilha de chamadas, esses objetos podem ser adaptados a sessões ou resolvedores de recursos com privilégios elevados e, muitas vezes, não está claro para o chamador que é uma sessão de administrador com a qual estão operando.
* **Desempenho:** As sessões compartilhadas do Oak podem causar problemas de desempenho e, no momento, não é recomendável usá-las.

A solução mais óbvia para o risco de segurança é simplesmente substituir o `loginAdministrative()` chamar com um `loginService()` um para um usuário com privilégios restritos. No entanto, isso não terá impacto em nenhuma possível degradação do desempenho. Uma possibilidade de mitigar isso é envolver todas as informações solicitadas em um objeto que não esteja associado à sessão. Em seguida, crie (ou destrua) a sessão sob demanda.

A abordagem recomendada é refatorar a API do serviço para dar ao chamador controle sobre a criação/destruição da sessão.

## Sessões administrativas em JSPs {#administrative-sessions-in-jsps}

JSPs não podem usar `loginService()`, pois não há serviço associado. No entanto, as sessões administrativas em JSPs geralmente são um sinal de violação do paradigma MVC.

Isso pode ser corrigido de duas maneiras:

1. Reestruturar o conteúdo de forma que permita manipulá-lo com a sessão do usuário;
1. Extraindo a lógica para um serviço que fornece uma API que pode ser usada pelo JSP.

O primeiro método é o preferido.

## Eventos de processamento, pré-processadores e trabalhos de replicação {#processing-events-replication-preprocessors-and-jobs}

Ao processar eventos ou trabalhos e, em alguns casos, workflows, a sessão correspondente que acionou o evento geralmente é perdida. Isso faz com que manipuladores de eventos e processadores de trabalho geralmente usem sessões administrativas para fazer seu trabalho. Existem diferentes abordagens concebíveis para resolver este problema, cada uma com suas vantagens e desvantagens:

1. Passe o `user-id` no payload do evento e usar representação.

   **Vantagens** Fácil de usar.

   **Desvantagens:** Ainda usa `loginAdministrative()`. Ele reautentica uma solicitação que já foi autenticada.

1. Criar ou reutilizar um usuário de serviço que tenha acesso aos dados.

   **Vantagens** Consistente com o design atual. Precisa de mudanças mínimas.

   **Desvantagens:** Precisa de usuários de serviço muito poderosos para ser flexível, o que pode facilmente levar a escalonamentos de privilégios. Contorna o modelo de segurança.

1. Transmita uma serialização do `Subject` na carga do evento, e crie uma `ResourceResolver` com base nesse assunto. Um exemplo seria o uso do JAAS `doAsPrivileged` no `ResourceResolverFactory`.

   **Vantagens** Implementação limpa do ponto de vista da segurança. Ele evita a reautenticação e opera com os privilégios originais. O código relevante para a segurança é transparente para o consumidor do evento.

   **Desvantagens:** Precisa de refatoração. O fato de o código relevante para a segurança ser transparente para o consumidor do evento também pode causar problemas.

A terceira abordagem é atualmente a técnica de processamento preferida.

## Processos de fluxo de trabalho {#workflow-processes}

Nas implementações de processos de fluxo de trabalho, a sessão de usuário correspondente que acionou o fluxo de trabalho geralmente é perdida. Isso faz com que processos de fluxo de trabalho geralmente usem sessões administrativas para executar seu trabalho.

Para corrigir esses problemas, recomenda-se que as mesmas abordagens mencionadas no [Eventos de processamento, pré-processadores e trabalhos de replicação](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs) ser utilizado.

## Processadores Sling POST e páginas excluídas {#sling-post-processors-and-deleted-pages}

Há algumas sessões administrativas usadas em implementações do processador sling POST. Normalmente, as sessões administrativas são usadas para acessar nós com exclusão pendente no POST que está sendo processado. Em consequência, eles não estarão mais disponíveis por meio da sessão de solicitação. Uma exclusão pendente de um nó pode ser acessada para divulgar metadados que, de outra forma, não deveriam estar acessíveis.
