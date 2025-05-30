---
title: Usuários de serviço no Adobe Experience Manager
description: Saiba mais sobre Usuários de serviço no Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 0%

---


# Usuários de serviço no Adobe Experience Manager (AEM) {#service-users-in-aem}

## Visão geral {#overview}

A forma principal de obter uma sessão administrativa ou um resolvedor de recursos no AEM era usando os métodos `SlingRepository.loginAdministrative()` e `ResourceResolverFactory.getAdministrativeResourceResolver()` fornecidos pelo Sling.

No entanto, nenhum desses métodos foi desenvolvido com base no [princípio do menor privilégio](https://en.wikipedia.org/wiki/Principle_of_least_privilege). Isso facilita muito para um desenvolvedor não planejar uma estrutura adequada e os respectivos Níveis de controle de acesso (ACLs) para o conteúdo antecipadamente. Se uma vulnerabilidade estiver presente em tal serviço, ela frequentemente leva a escalonamentos de privilégios para o usuário `admin`, mesmo que o próprio código não precise de privilégios administrativos para funcionar.

## Como eliminar as sessões de administrador {#how-to-phase-out-admin-sessions}

### Prioridade 0: o recurso está ativo/necessário/abandonado? {#priority-is-the-feature-active-needed-derelict}

Pode haver casos em que a sessão de administrador não seja usada ou o recurso seja totalmente desativado. Em caso afirmativo, remova o recurso completamente ou ajuste-o com o [código NOP](https://en.wikipedia.org/wiki/NOP).

### Prioridade 1: Usar A Sessão De Solicitação {#priority-use-the-request-session}

Sempre que possível, refatore seu recurso para que a sessão de solicitação fornecida e autenticada possa ser usada para ler ou gravar conteúdo. Caso tal não seja possível, pode muitas vezes conseguir-se aplicando as prioridades que se seguem.

### Prioridade 2: Reestruturar Conteúdo {#priority-restructure-content}

Muitos problemas podem ser resolvidos reestruturando o conteúdo. Lembre-se dessas regras simples ao fazer a reestruturação:

* **Alterar controle de acesso**

   * Certifique-se de que os usuários ou grupos que realmente precisam de acesso tenham acesso;

* **Refinar estrutura de conteúdo**

   * Movê-lo para outros locais, por exemplo, onde o controle de acesso corresponde às sessões de solicitação disponíveis;
   * Alterar a granularidade do conteúdo;

* **Refatorar seu código para que seja um serviço adequado**

   * Mova a lógica de negócios do código JSP para o serviço. Isso permite modelagem de conteúdo diferente.

Além disso, verifique se os novos recursos desenvolvidos seguem estes princípios:

* **Os requisitos de segurança devem orientar a estrutura do conteúdo**

   * O gerenciamento do controle de acesso deve parecer natural
   * O controle de acesso deve ser aplicado pelo repositório, não pelo aplicativo

* **Usar tipos de nós**

   * Restringir o conjunto de propriedades que podem ser definidas

* **Respeitar configurações de privacidade**

   * Se houver perfis privados, um exemplo seria não expor a imagem do perfil, o email ou o nome completo encontrado no nó `/profile` privado.

## Controle de acesso estrito {#strict-access-control}

Se você aplicar o controle de acesso ao reestruturar o conteúdo ou quando o fizer para um novo usuário de serviço, deverá aplicar as ACLs mais rigorosas possíveis. Usar todos os recursos possíveis de controle de acesso:

* Por exemplo, em vez de aplicar `jcr:read` em `/apps`, aplique somente a `/apps/*/components/*/analytics`

* Usar [restrições](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* Aplicar ACLs para tipos de nó
* Limitar permissões

   * por exemplo, quando precisar apenas gravar propriedades, não dê a permissão `jcr:write`; use `jcr:modifyProperties`

## Usuários e Mapeamentos do Serviço {#service-users-and-mappings}

Se falhar, o Sling 7 oferecerá um serviço de Mapeamento de usuários do serviço, que permite configurar um mapeamento de pacote para usuário e dois métodos de API correspondentes:

* [`SlingRepository.loginService()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)
* [`ResourceResolverFactory.getServiceResourceResolver()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)

Os métodos retornam um resolvedor de sessão/recurso com os privilégios somente de um usuário configurado. Esses métodos têm as seguintes características:

* Eles permitem serviços de mapeamento para usuários
* Eles permitem definir usuários de subserviço
* O ponto de configuração central é: `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name` [&quot;:&quot; nome-subserviço]

* `service-id` está mapeado para um resolvedor de recursos e/ou ID de usuário do repositório JCR para autenticação
* `service-name` é o nome simbólico do pacote que fornece o serviço

## Outro Recommendations {#other-recommendations}

### Substituição da sessão de administrador por um usuário de serviço {#replacing-the-admin-session-with-a-service-user}

Um usuário de serviço é um usuário JCR sem senha definida e com um conjunto mínimo de privilégios necessários para executar uma tarefa específica. Não ter senha definida significa que não é possível fazer logon com um usuário de serviço.

Uma maneira de descontinuar uma sessão administrativa é substituí-la por sessões de usuário de serviço. Ele também pode ser substituído por vários usuários de subserviço, se necessário.

Para substituir a sessão de administrador por um usuário de serviço, execute as seguintes etapas:

1. Identifique as permissões necessárias para seu serviço, tendo em mente o princípio de menos permissão.
1. Verifique se já existe um usuário disponível com exatamente a configuração de permissão necessária. Crie um usuário de serviço do sistema se nenhum usuário existente atender às suas necessidades. O RTC é necessário para criar um usuário de serviço. Às vezes, faz sentido criar vários usuários de subserviço (por exemplo, um para escrita e outro para leitura) para compartimentalizar ainda mais o acesso.
1. Configurar e testar ACEs para o usuário.
1. Adicione um mapeamento de `service-user` para seu serviço e para `user/sub-users`

1. Disponibilize o recurso sling do usuário do serviço para o seu pacote: atualize para a versão mais recente do `org.apache.sling.api`.

1. Substitua o `admin-session` em seu código pelas APIs `loginService` ou `getServiceResourceResolver`.

## Criação de um usuário de serviço {#creating-a-new-service-user}

Depois de verificar que nenhum usuário na lista de usuários do serviço AEM se aplica ao seu caso de uso e que os problemas de RTC correspondentes foram aprovados, adicione o novo usuário ao conteúdo padrão.

A abordagem recomendada é criar um usuário de serviço para usar o explorador de repositório em *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*

O objetivo é obter uma propriedade `jcr:uuid` válida, que é obrigatória para criar o usuário por meio de uma instalação de pacote de conteúdo.

Você pode criar usuários de serviço ao:

1. Acessando o explorador de repositório em *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*
1. Para fazer logon como administrador, pressione o link **Fazer logon**, no canto superior esquerdo da tela.
1. Em seguida, crie e nomeie o usuário do sistema. Para criar o usuário como um sistema, defina o caminho intermediário como `system` e adicione subpastas opcionais de acordo com suas necessidades:

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. Verifique se o nó do usuário do sistema tem a seguinte aparência:

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >Não há tipos de mixin associados a usuários de serviço. Isso significa que não há políticas de controle de acesso para usuários do sistema.

Ao adicionar o .content.xml correspondente ao conteúdo do seu pacote, verifique se você definiu o `rep:authorizableId` e se o tipo primário é `rep:SystemUser`. Deve ter esta aparência:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## Adicionando uma alteração de configuração à configuração ServiceUserMapper {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

Para adicionar um mapeamento de seu serviço aos Usuários do Sistema correspondentes, crie uma configuração de fábrica para o serviço [`ServiceUserMapper`](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html). Para manter essa configuração modular, ela pode ser fornecida usando o [mecanismo de correção do Sling](https://issues.apache.org/jira/browse/SLING-3578). A maneira recomendada de instalar essas configurações com seu pacote é usando o [Carregamento de Conteúdo Inicial do Sling](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. Crie uma subpasta SLING-INF/content abaixo da pasta src/main/resources do seu pacote
1. Nesta pasta, crie um arquivo chamado org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.ended-&lt;algum nome exclusivo para a configuração de fábrica>.xml com o conteúdo da configuração de fábrica (incluindo todos os mapeamentos de usuário de subserviço). Exemplo:

1. Crie uma pasta `SLING-INF/content` abaixo da pasta `src/main/resources` do seu pacote;
1. Nesta pasta, crie um arquivo `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` com o conteúdo da configuração de fábrica, incluindo todos os mapeamentos de subserviço de usuário.

   Para fins de ilustração, use o arquivo chamado `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

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

1. Referencie o conteúdo inicial do Sling na configuração do `maven-bundle-plugin` no `pom.xml` de seu pacote. Exemplo:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. Instale seu pacote e verifique se a configuração de fábrica está instalada. Você pode fazer isso ao:

   * Acessando o Console da Web em *https://serverhost:serveraddress/system/console/configMgr*
   * Procurar por **Aditamento do Serviço Mapeador de Usuários do Apache Sling Service**
   * Clique no link para ver se a configuração apropriada está em vigor.

## Lidar com sessões compartilhadas em serviços {#dealing-with-shared-sessions-in-services}

As chamadas para `loginAdministrative()` geralmente aparecem junto com sessões compartilhadas. Essas sessões são adquiridas na ativação do serviço e só são desconectadas após a interrupção do serviço. Embora essa seja uma prática comum, ela gera dois problemas:

* **Segurança:** essas sessões de administrador são usadas para armazenar em cache e retornar recursos ou outros objetos associados à sessão compartilhada. Mais tarde na pilha de chamadas, esses objetos poderiam ser adaptados a sessões ou resolvedores de recursos com privilégios elevados. Geralmente, não está claro para o chamador que essa é uma sessão de administrador com a qual ele está operando.
* **Desempenho:** no Oak, as sessões compartilhadas podem causar problemas de desempenho, e não é recomendável usá-las.

A solução mais óbvia para o risco de segurança é simplesmente substituir a chamada do `loginAdministrative()` por uma chamada do `loginService()` para um usuário com privilégios restritos. No entanto, isso não tem impacto em nenhuma possível degradação do desempenho. Uma possibilidade de mitigar isso é envolver todas as informações solicitadas em um objeto que não esteja associado à sessão. Em seguida, crie (ou destrua) a sessão sob demanda.

A abordagem recomendada é refatorar a API do serviço para dar ao chamador controle sobre a criação/destruição da sessão.

## Sessões administrativas em JSPs {#administrative-sessions-in-jsps}

JSPs não podem usar `loginService()`, porque não há serviço associado. No entanto, as sessões administrativas em JSPs geralmente são um sinal de violação do paradigma MVC.

Isso pode ser corrigido de duas maneiras:

1. Reestruturar o conteúdo de forma que permita manipulá-lo com a sessão do usuário;
1. Extraindo a lógica para um serviço que fornece uma API que pode ser usada pelo JSP.

O primeiro método é o preferido.

## Eventos de processamento, pré-processadores e trabalhos de replicação {#processing-events-replication-preprocessors-and-jobs}

Ao processar eventos ou trabalhos e, às vezes, workflows, a sessão correspondente que acionou o evento é perdida. Isso faz com que manipuladores de eventos e processadores de trabalho geralmente usem sessões administrativas para fazer seu trabalho. Existem diferentes abordagens concebíveis para resolver este problema, cada uma com suas vantagens e desvantagens:

1. Passe o `user-id` na carga do evento e use representação.

   **Vantagens:** fácil de usar.

   **Desvantagens:** ainda usa `loginAdministrative()`. Ele reautentica uma solicitação que já foi autenticada.

1. Criar ou reutilizar um usuário de serviço que tenha acesso aos dados.

   **Vantagens:** consistente com o design atual. Precisa de mudanças mínimas.

   **Desvantagens:** precisa de usuários avançados de serviços para ser flexível, o que pode facilmente levar a escalonamentos de privilégios. Contorna o modelo de segurança.

1. Passe uma serialização de `Subject` na carga do evento e crie um `ResourceResolver` com base nesse assunto. Um exemplo seria o uso do JAAS `doAsPrivileged` em `ResourceResolverFactory`.

   **Vantagens:** implementação limpa de um ponto de vista de segurança. Ela evita a reautenticação e opera com os privilégios originais. O código relevante para a segurança é transparente para o consumidor do evento.

   **Desvantagens:** Requer refatoração. O fato de o código relevante para a segurança ser transparente para o consumidor do evento também pode causar problemas.

A terceira abordagem é a técnica de processamento preferida.

## Processos de fluxo de trabalho {#workflow-processes}

Nas implementações do processo de fluxo de trabalho, a sessão do usuário correspondente que acionou o fluxo de trabalho é perdida. Isso leva a processos de fluxo de trabalho que geralmente usam sessões administrativas para executar seu trabalho.

Para corrigir esses problemas, é recomendável usar as mesmas abordagens mencionadas em [Processando Eventos, Pré-processadores de Replicação e Trabalhos](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs).

## Processadores Sling POST e páginas excluídas {#sling-post-processors-and-deleted-pages}

Há algumas sessões administrativas usadas em implementações do processador sling POST. Normalmente, as sessões administrativas são usadas para acessar nós com exclusão pendente no POST que está sendo processado. Em consequência, eles não estarão mais disponíveis por meio da sessão de solicitação. Uma exclusão pendente de um nó pode ser acessada para divulgar metadados que, de outra forma, não deveriam estar acessíveis.
