---
title: Usuários do serviço no AEM
seo-title: Usuários do serviço no AEM
description: Saiba mais sobre os usuários do serviço no AEM.
seo-description: Saiba mais sobre os usuários do serviço no AEM.
uuid: 4efab5fb-ba11-4922-bd68-43ccde4eb355
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 9cfe5f11-8a0e-4a27-9681-a8d50835c864
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '1788'
ht-degree: 0%

---


# Usuários do serviço em AEM{#service-users-in-aem}

## Visão geral {#overview}

A principal maneira de obter uma sessão administrativa ou um resolvedor de recursos no AEM era usar os métodos `SlingRepository.loginAdministrative()` e `ResourceResolverFactory.getAdministrativeResourceResolver()` fornecidos pelo Sling.

No entanto, nenhum desses métodos foi projetado em torno do princípio [de menor privilégio](https://en.wikipedia.org/wiki/Principle_of_least_privilege) e facilita demais para um desenvolvedor não planejar uma estrutura adequada e os Níveis de Controle de acesso (ACLs) correspondentes para seu conteúdo no início. Se uma vulnerabilidade estiver presente em um serviço desse tipo, isso geralmente resultará em escalonamentos de privilégio para o usuário `admin`, mesmo que o código em si não precise de privilégios administrativos para funcionar.

## Como eliminar as sessões administrativas {#how-to-phase-out-admin-sessions}

### Prioridade 0: O recurso está ativo/necessário/removido? {#priority-is-the-feature-active-needed-derelict}

Pode haver casos em que a sessão de administrador não é usada ou o recurso é desativado totalmente. Se esse for o caso com sua implementação, remova o recurso completamente ou ajuste-o com [código NOP](https://en.wikipedia.org/wiki/NOP).

### Prioridade 1: Usar A Sessão De Solicitação {#priority-use-the-request-session}

Sempre que possível, reative seu recurso para que a sessão de solicitação autenticada fornecida possa ser usada para ler ou gravar conteúdo. Se tal não for possível, poderá ser conseguido, muitas vezes, aplicando as prioridades que se seguem às que se seguem.

### Prioridade 2: Reestruturar conteúdo {#priority-restructure-content}

Muitas questões podem ser resolvidas através da reestruturação do conteúdo. Lembre-se dessas regras simples ao fazer a reestruturação:

* **Alterar controle de acesso**

   * Certifique-se de que os usuários ou grupos que realmente precisam de acesso tenham realmente acesso;

* **Refinar estrutura de conteúdo**

   * Mova-o para outros locais, por exemplo, onde o controle de acesso corresponde às sessões de solicitação disponíveis;
   * Alterar a granularidade do conteúdo;

* **Refaça seu código para ser um serviço adequado**

   * Mova a lógica comercial do código JSP para o serviço. Isso permite modelagem de conteúdo diferente.

Além disso, certifique-se de que todos os novos recursos desenvolvidos seguem estes princípios:

* **Os requisitos de segurança devem orientar a estrutura do conteúdo**

   * Gerenciar controles de acesso deve se sentir natural
   * O controle de acesso deve ser imposto pelo repositório, não pelo aplicativo

* **Usar tipos de nó**

   * Restringir o conjunto de propriedades que pode ser definido

* **Respeitar configurações de privacidade**

   * No caso de perfis particulares, um exemplo seria não expor a imagem do perfil, o email ou o nome completo encontrados no nó privado `/profile`.

## Controle de acesso restrito {#strict-access-control}

Se você aplicar controles de acesso durante a reestruturação de conteúdo ou quando fizer isso para um novo usuário de serviço, deverá aplicar as ACLs mais rigorosas possíveis. Usar todos os recursos possíveis do controle de acesso:

* Por exemplo, em vez de aplicar `jcr:read` em `/apps`, aplique-o somente a `/apps/*/components/*/analytics`

* Usar [restrições](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* Aplicar ACLs para tipos de nó
* Limitar permissões

   * por exemplo, quando for necessário apenas gravar propriedades, não conceda a permissão `jcr:write`; use `jcr:modifyProperties` em vez disso

## Usuários do serviço e mapeamentos {#service-users-and-mappings}

Se o acima falhar, o Sling 7 oferta um serviço de Mapeamento de usuário de serviço, que permite configurar um mapeamento de grupo para usuário e dois métodos de API correspondentes: ` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)` e ` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)` que retornam um resolvedor de sessão/recurso com os privilégios somente de um usuário configurado. Esses métodos têm as seguintes características:

* Eles permitem serviços de mapeamento para usuários
* Permitem definir usuários subserviços
* O ponto central de configuração é: `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` =  `service-name` [ &quot;:&quot; subservice-name  ] 

* `service-id` está mapeada para um resolvedor de recursos e/ou ID de usuário do repositório JCR para autenticação
* `service-name` é o nome simbólico do pacote que fornece o serviço

## Outros Recommendations {#other-recommendations}

### Substituição da sessão de administrador por um usuário de serviço {#replacing-the-admin-session-with-a-service-user}

Um usuário de serviço é um usuário JCR sem definição de senha e com um conjunto mínimo de privilégios necessários para executar uma tarefa específica. Não ter uma senha definida significa que não será possível fazer logon com um usuário do serviço.

Uma maneira de desaprovar uma sessão administrativa é substituí-la por sessões de usuário de serviço. Ele também pode ser substituído por vários usuários de sub-serviço, se necessário.

Para substituir a sessão de administrador por um usuário de serviço, execute as seguintes etapas:

1. Identifique as permissões necessárias para o seu serviço, tendo em mente o princípio da menor permissão.
1. Verifique se já existe um usuário disponível com a configuração de permissão necessária. Crie um novo usuário de serviço do sistema se nenhum usuário existente corresponder às suas necessidades. O RTC é necessário para criar um novo usuário de serviço. Às vezes, faz sentido criar vários usuários de sub-serviço (por exemplo, um para escrita e outro para leitura) para compartimentalizar ainda mais o acesso.
1. Configure e teste ACEs para seu usuário.
1. Adicione um mapeamento `service-user` para seu serviço e para `user/sub-users`

1. Disponibilize o recurso de sling do usuário do serviço ao seu pacote: atualize para a versão mais recente de `org.apache.sling.api`.

1. Substitua `admin-session` no código pelas APIs `loginService` ou `getServiceResourceResolver`.

## Criando um novo usuário de serviço {#creating-a-new-service-user}

Depois de verificar que nenhum usuário na lista de AEM usuários do serviço é aplicável ao caso de uso e que os problemas de RTC correspondentes foram aprovados, você pode continuar e adicionar o novo usuário ao conteúdo padrão.

A abordagem recomendada é criar um usuário de serviço para usar o explorador de repositório em *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*

O objetivo é obter uma propriedade válida `jcr:uuid` que é obrigatória para criar o usuário por meio de uma instalação de pacote de conteúdo.

Você pode criar usuários do serviço ao:

1. Ir para o explorador de repositório em *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*
1. Efetuar logon como administrador pressionando o link **Login** no canto superior esquerdo da tela.
1. Em seguida, crie e nomeie o usuário do sistema. Para criar o usuário como um sistema, defina o caminho intermediário como `system` e adicione subpastas opcionais, dependendo de suas necessidades:

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. Verifique se o nó do usuário do sistema tem a seguinte aparência:

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >Observe que não há tipos de combinação associados aos usuários do serviço. Isso significa que não haverá políticas de controle de acesso para usuários do sistema.

Ao adicionar o .content.xml correspondente ao conteúdo do seu pacote, certifique-se de ter definido `rep:authorizableId` e de que o tipo primário é `rep:SystemUser`. Deve ser parecido com isto:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## Adicionando uma emenda de configuração à configuração ServiceUserMapper {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

Para adicionar um mapeamento do seu serviço aos Usuários do sistema correspondentes, é necessário criar uma configuração de fábrica para o serviço ` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)`. Para manter este modular, essas configurações podem ser fornecidas usando o [mecanismo de correção Sling](https://issues.apache.org/jira/browse/SLING-3578). A maneira recomendada para instalar essas configurações com seu pacote é usar [Carregamento inicial de conteúdo](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. Crie uma subpasta SLING-INF/content abaixo da pasta src/main/resources do seu pacote
1. Nesta pasta, crie um arquivo chamado org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.changed-&lt;algum nome exclusivo para sua configuração de fábrica>.xml com o conteúdo de sua configuração de fábrica (incluindo todos os mapeamentos de usuário de sub-serviço). Exemplo:

1. Crie uma pasta `SLING-INF/content` abaixo da pasta `src/main/resources` do seu pacote;
1. Nesta pasta, crie um arquivo `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` com o conteúdo de sua configuração de fábrica, incluindo todos os mapeamentos de subserviços do usuário.

   Para fins de ilustração, siga um arquivo chamado `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

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

1. Consulte o conteúdo inicial do Sling na configuração de `maven-bundle-plugin` em `pom.xml` do seu pacote. Exemplo:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. Instale o pacote e verifique se a configuração de fábrica foi instalada. Você pode fazer isso:

   * Ir para o Web Console em *https://serverhost:serveraddress/system/console/configMgr*
   * Procure **Apache Sling Service User Mapper Service Emenda do Serviço Mapeador do Usuário do Apache Sling**
   * Clique no link para ver se a configuração correta está ativada.

## Lidar com sessões compartilhadas em serviços {#dealing-with-shared-sessions-in-services}

As chamadas para `loginAdministrative()` geralmente aparecem junto com as sessões compartilhadas. Essas sessões são adquiridas na ativação de serviço e são desconectadas somente depois que o serviço é interrompido. Embora esta prática seja comum, leva a dois problemas:

* **Segurança:** tais sessões administrativas são usadas para armazenar em cache e retornar recursos ou outros objetos vinculados à sessão compartilhada. Mais tarde na pilha de chamadas, esses objetos podem ser adaptados a sessões ou resolvedores de recursos com privilégios elevados e, frequentemente, não fica claro para o chamador que é uma sessão de administrador com a qual eles estão operando.
* **Desempenho:** em sessões compartilhadas no Oak podem causar problemas de desempenho e não é recomendado usá-los no momento.

A solução mais óbvia para o risco de segurança é simplesmente substituir a chamada `loginAdministrative()` por uma `loginService()` para um usuário com privilégios restritos. No entanto, isso não terá nenhum impacto em qualquer potencial degradação do desempenho. Uma possibilidade de mitigar isso é envolver todas as informações solicitadas em um objeto que não tenha associação com a sessão. Em seguida, crie (ou destrua) a sessão sob demanda.

A abordagem recomendada é refatorar a API do serviço para dar ao chamador controle sobre a criação/destruição da sessão.

## Sessões administrativas em JSPs {#administrative-sessions-in-jsps}

Os JSPs não podem usar `loginService()`, porque não há serviço associado. No entanto, as sessões administrativas em JSPs são geralmente um sinal de violação do paradigma MVC.

Isso pode ser corrigido de duas formas:

1. Reestruturar o conteúdo de forma a permitir manipulá-lo com a sessão do usuário;
1. Extrair a lógica para um serviço que fornece uma API que pode ser usada pelo JSP.

O primeiro método é o preferido.

## Processando Eventos, Pré-processadores de Replicação e Trabalhos {#processing-events-replication-preprocessors-and-jobs}

Ao processar eventos ou trabalhos e, em alguns casos, workflows, a sessão correspondente que disparou o evento geralmente é perdida. Isso leva os manipuladores de eventos e os processadores de trabalho, que geralmente usam sessões administrativas para fazer seu trabalho. Existem diferentes abordagens concebíveis para resolver este problema, cada uma com as suas vantagens e desvantagens:

1. Passe `user-id` na carga do evento e use representação.

   **Vantagens:** fácil de usar.

   **Desvantagens:** Ainda usa  `loginAdministrative()`. Ela autentica novamente uma solicitação que já foi autenticada.

1. Crie ou reutilize um usuário de serviço que tenha acesso aos dados.

   **Vantagens:** consistente com o design atual. Precisa de uma mudança mínima.

   **Desvantagens:** precisa de usuários de serviços muito poderosos para serem flexíveis, o que pode facilmente levar a escalonamentos de privilégio. Evita o modelo de segurança.

1. Passe uma serialização de `Subject` na carga do evento e crie um `ResourceResolver` com base nesse assunto. Um exemplo seria usar o JAAS `doAsPrivileged` no `ResourceResolverFactory`.

   **Vantagens:implementação** limpa do ponto de vista de segurança. Evita a reautenticação e opera com os privilégios originais. O código relevante em matéria de segurança é transparente para o consumidor do evento.

   **Desvantagens:** Precisa de refatoração. O fato de o código relevante para a segurança ser transparente para o consumidor do evento também pode causar problemas.

A terceira abordagem é atualmente a técnica de processamento preferencial.

## Processos de Fluxo de Trabalho {#workflow-processes}

Nas implementações do processo de fluxo de trabalho, a sessão de usuário correspondente que acionou o fluxo de trabalho normalmente é perdida. Isso leva a processos de fluxo de trabalho que geralmente usam sessões administrativas para realizar seu trabalho.

Para corrigir esses problemas, recomenda-se que as mesmas abordagens mencionadas em [Eventos de processamento, pré-processadores de replicação e tarefas](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs) sejam usadas.

## Processadores Sling POST e páginas excluídas {#sling-post-processors-and-deleted-pages}

Há algumas sessões administrativas usadas em implementações de POST sling. Geralmente, as sessões administrativas são usadas para acessar nós que estão com exclusão pendente no POST sendo processado. Consequentemente, eles não estão mais disponíveis por meio da sessão de solicitação. Um nó com exclusão pendente pode ser acessado para revelar uma metáada que, de outra forma, não deveria estar acessível.
