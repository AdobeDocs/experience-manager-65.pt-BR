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

---


# Usuários do serviço no AEM{#service-users-in-aem}

## Visão geral {#overview}

A principal maneira de obter uma sessão administrativa ou um resolvedor de recursos no AEM era usar os métodos `SlingRepository.loginAdministrative()` e `ResourceResolverFactory.getAdministrativeResourceResolver()` fornecidos pelo Sling.

No entanto, nenhum desses métodos foi projetado em torno do [princípio do menor privilégio](https://en.wikipedia.org/wiki/Principle_of_least_privilege) e facilita demais para um desenvolvedor não planejar uma estrutura adequada e os Níveis de controle de acesso (ACLs) correspondentes para seu conteúdo desde o início. Se uma vulnerabilidade estiver presente em um serviço desse tipo, isso geralmente leva a escalonamentos de privilégio para o `admin` usuário, mesmo que o código em si não precise de privilégios administrativos para funcionar.

## Como eliminar gradualmente as sessões administrativas {#how-to-phase-out-admin-sessions}

### Prioridade 0: O recurso está ativo/necessário/removido? {#priority-is-the-feature-active-needed-derelict}

Pode haver casos em que a sessão de administrador não é usada ou o recurso é desativado totalmente. Se esse for o caso com sua implementação, remova o recurso completamente ou ajuste-o ao código [](https://en.wikipedia.org/wiki/NOP)NOP.

### Prioridade 1: Usar A Sessão De Solicitação {#priority-use-the-request-session}

Sempre que possível, reative seu recurso para que a sessão de solicitação autenticada fornecida possa ser usada para ler ou gravar conteúdo. Se tal não for possível, poderá ser conseguido aplicando frequentemente as prioridades que se seguem às que se seguem.

### Prioridade 2: Reestruturar conteúdo {#priority-restructure-content}

Muitas questões podem ser resolvidas através da reestruturação do conteúdo. Lembre-se dessas regras simples ao fazer a reestruturação:

* **Alterar controle de acesso**

   * Certifique-se de que os usuários ou grupos que realmente precisam de acesso tenham realmente acesso;

* **Refinar estrutura de conteúdo**

   * Mova-o para outros locais, por exemplo, onde o controle de acesso corresponda às sessões de solicitação disponíveis;
   * Alterar a granularidade do conteúdo;

* **Refaça seu código para ser um serviço adequado**

   * Mova a lógica comercial do código JSP para o serviço. Isso permite modelagem de conteúdo diferente.

Além disso, certifique-se de que todos os novos recursos desenvolvidos seguem estes princípios:

* **Os requisitos de segurança devem orientar a estrutura do conteúdo**

   * O gerenciamento do controle de acesso deve ser natural
   * O controle de acesso deve ser imposto pelo repositório, não pelo aplicativo

* **Usar tipos de nó**

   * Restringir o conjunto de propriedades que pode ser definido

* **Respeitar configurações de privacidade**

   * No caso de perfis privados, um exemplo seria não expor a imagem do perfil, o email ou o nome completo encontrados no `/profile` nó privado.

## Controle de acesso restrito {#strict-access-control}

Independentemente de você aplicar controle de acesso ao reestruturar conteúdo ou quando fizer isso para um novo usuário de serviço, deverá aplicar as ACLs mais rigorosas possíveis. Usar todos os recursos possíveis de controle de acesso:

* Por exemplo, em vez de aplicar `jcr:read` em `/apps`, aplique-o somente a `/apps/*/components/*/analytics`

* Use [restrictions](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* Aplicar ACLs para tipos de nó
* Limitar permissões

   * por exemplo, quando for necessário apenas gravar propriedades, não dê a `jcr:write` permissão; use `jcr:modifyProperties` em vez

## Usuários e mapeamentos do serviço {#service-users-and-mappings}

Se o acima falhar, o Sling 7 oferece um serviço de Mapeamento de usuário de serviço, que permite configurar um mapeamento de conjunto para usuário e dois métodos de API correspondentes: ` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)` e ` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)` que retornam um resolvedor de sessão/recurso com os privilégios somente de um usuário configurado. Esses métodos têm as seguintes características:

* Eles permitem serviços de mapeamento para usuários
* Permitem definir usuários subserviços
* O ponto central de configuração é: `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name` [ &quot;:&quot; subservice-name ] 

* `service-id` está mapeada para um resolvedor de recursos e/ou ID de usuário do repositório JCR para autenticação
* `service-name` é o nome simbólico do pacote que fornece o serviço

## Outras recomendações {#other-recommendations}

### Substituição da sessão de administrador por um usuário-serviço {#replacing-the-admin-session-with-a-service-user}

Um usuário de serviço é um usuário JCR sem definição de senha e com um conjunto mínimo de privilégios necessários para executar uma tarefa específica. Sem definição de senha significa que não será possível fazer logon com um usuário do serviço.

Uma maneira de desaprovar uma sessão administrativa é substituí-la por sessões de usuário de serviço. Ele também pode ser substituído por vários usuários de sub-serviço, se necessário.

Para substituir a sessão de administrador por um usuário de serviço, execute as seguintes etapas:

1. Identifique as permissões necessárias para o seu serviço, tendo em mente o princípio da menor permissão.
1. Verifique se já existe um usuário disponível com a configuração de permissão necessária. Crie um novo usuário de serviço do sistema se nenhum usuário existente corresponder às suas necessidades. O RTC é necessário para criar um novo usuário de serviço. Às vezes, faz sentido criar vários usuários de subserviço (por exemplo, um para escrita e outro para leitura) para compartimentalizar ainda mais o acesso.
1. Configure e teste ACEs para seu usuário.
1. Adicione um `service-user` mapeamento para seu serviço e para `user/sub-users`

1. Disponibilize o recurso de sling do usuário do serviço ao seu pacote: atualizar para a versão mais recente do `org.apache.sling.api`.

1. Substitua o código `admin-session` por APIs `loginService` ou `getServiceResourceResolver` APIs.

## Criar um novo usuário de serviço {#creating-a-new-service-user}

Depois de verificar que nenhum usuário na lista de usuários do serviço AEM é aplicável ao caso de uso e que os problemas de RTC correspondentes foram aprovados, você pode continuar e adicionar o novo usuário ao conteúdo padrão.

A abordagem recomendada é criar um usuário de serviço para usar o explorador de repositório em *https://&lt;servidor>:&lt;porta>/crx/explorer/index.jsp*

O objetivo é obter uma `jcr:uuid` propriedade válida que é obrigatória para criar o usuário por meio de uma instalação de pacote de conteúdo.

Você pode criar usuários do serviço ao:

1. Ir para o explorador de repositório em *https://&lt;servidor>:&lt;porta>/crx/explorer/index.jsp*
1. Efetuar logon como administrador pressionando o link **Fazer logon** no canto superior esquerdo da tela.
1. Em seguida, crie e nomeie o usuário do sistema. Para criar o usuário como um sistema, defina o caminho intermediário como `system` e adicione subpastas opcionais, dependendo de suas necessidades:

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. Verifique se o nó do usuário do sistema tem a seguinte aparência:

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >Observe que não há tipos de combinação associados aos usuários do serviço. Isso significa que não haverá políticas de controle de acesso para usuários do sistema.

Ao adicionar o .content.xml correspondente ao conteúdo do seu pacote, verifique se você definiu o tipo `rep:authorizableId` e o tipo principal `rep:SystemUser`. Deve ser semelhante a:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## Adicionando uma emenda de configuração à configuração ServiceUserMapper {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

Para adicionar um mapeamento do seu serviço aos Usuários do sistema correspondentes, é necessário criar uma configuração de fábrica para o ` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)` serviço. Para manter este modular, essas configurações podem ser fornecidas usando o mecanismo [de correção](https://issues.apache.org/jira/browse/SLING-3578)Sling. A maneira recomendada para instalar essas configurações com seu pacote é usando o [Sling Initial Content Loading](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. Crie uma subpasta SLING-INF/content abaixo da pasta src/main/resources do seu pacote
1. Nesta pasta, crie um arquivo chamado org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.changed-&lt;algum nome exclusivo para sua configuração de fábrica>.xml com o conteúdo de sua configuração de fábrica (incluindo todos os mapeamentos de usuário de sub-serviço). Exemplo:

1. Crie uma `SLING-INF/content` pasta abaixo da `src/main/resources` pasta do seu pacote;
1. Nesta pasta, crie um arquivo `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` com o conteúdo de sua configuração de fábrica, incluindo todos os mapeamentos de usuário de subserviço.

   Para fins ilustrativos, pegue um arquivo chamado `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

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

1. Faça referência ao conteúdo inicial do Sling na configuração do `maven-bundle-plugin` no `pom.xml` pacote. Exemplo:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. Instale o pacote e verifique se a configuração de fábrica foi instalada. Você pode fazer isso:

   * Ir para o Web Console em *https://serverhost:serveraddress/system/console/configMgr*
   * Procurar Alteração do Serviço Mapeador de Usuário do Serviço **Apache Sling**
   * Clique no link para ver se a configuração correta está ativada.

## Lidar com sessões compartilhadas em serviços {#dealing-with-shared-sessions-in-services}

Chamadas para aparecerem `loginAdministrative()` frequentemente em conjunto com sessões compartilhadas. Essas sessões são adquiridas na ativação do serviço e são desconectadas somente depois que o serviço é interrompido. Embora esta prática seja comum, leva a dois problemas:

* **** Segurança: Essas sessões administrativas são usadas para armazenar em cache e retornar recursos ou outros objetos vinculados à sessão compartilhada. Mais tarde na pilha de chamadas, esses objetos podem ser adaptados a sessões ou resolvedores de recursos com privilégios elevados e, frequentemente, não fica claro para o chamador que é uma sessão de administrador com a qual eles estão operando.
* **** Desempenho: Em sessões compartilhadas do Oak podem causar problemas de desempenho e não é recomendado usá-los no momento.

A solução mais óbvia para o risco de segurança é simplesmente substituir a `loginAdministrative()` chamada por uma `loginService()` para um usuário com privilégios restritos. No entanto, isso não terá nenhum impacto em qualquer potencial degradação do desempenho. Uma possibilidade de mitigar isso é envolver todas as informações solicitadas em um objeto que não tenha associação com a sessão. Em seguida, crie (ou destrua) a sessão sob demanda.

A abordagem recomendada é refatorar a API do serviço para dar ao chamador controle sobre a criação/destruição da sessão.

## Sessões administrativas em JSPs {#administrative-sessions-in-jsps}

Os JSPs não podem usar `loginService()`, pois não há serviço associado. No entanto, as sessões administrativas em JSPs são geralmente um sinal de violação do paradigma MVC.

Isso pode ser corrigido de duas formas:

1. Reestruturar o conteúdo de forma a permitir manipulá-lo com a sessão do usuário;
1. Extrair a lógica para um serviço que fornece uma API que pode ser usada pelo JSP.

O primeiro método é o preferido.

## Eventos de processamento, pré-processadores de replicação e tarefas {#processing-events-replication-preprocessors-and-jobs}

Ao processar eventos ou trabalhos e, em alguns casos, fluxos de trabalho, a sessão correspondente que acionou o evento normalmente é perdida. Isso leva os manipuladores de eventos e os processadores de trabalho, que geralmente usam sessões administrativas para fazer seu trabalho. Existem diferentes abordagens concebíveis para resolver este problema, cada uma com as suas vantagens e desvantagens:

1. Passe a carga do evento `user-id` e use representação.

   **** Vantagens: Fácil de usar.

   **** Desvantagens: Ainda usa `loginAdministrative()`. Ela autentica novamente uma solicitação que já foi autenticada.

1. Crie ou reutilize um usuário de serviço que tenha acesso aos dados.

   **** Vantagens: Consistente com o design atual. Precisa de uma mudança mínima.

   **** Desvantagens: Precisa de usuários de serviço muito poderosos para serem flexíveis, o que pode facilmente levar a escalonamentos de privilégio. Evita o modelo de segurança.

1. Passe uma serialização do evento `Subject` na carga do evento e crie um `ResourceResolver` baseado nesse assunto. Um exemplo seria usar o JAAS `doAsPrivileged` no `ResourceResolverFactory`.

   **** Vantagens: Limpar a implementação do ponto de vista de segurança. Evita a reautenticação e opera com os privilégios originais. O código de segurança relevante é transparente para o consumidor do evento.

   **** Desvantagens: Precisa de refatoração. O fato de o código relevante para a segurança ser transparente para o consumidor do evento também pode causar problemas.

A terceira abordagem é atualmente a técnica de processamento preferencial.

## Processos de fluxo de trabalho {#workflow-processes}

Nas implementações do processo de fluxo de trabalho, a sessão de usuário correspondente que acionou o fluxo de trabalho normalmente é perdida. Isso leva a processos de fluxo de trabalho que geralmente usam sessões administrativas para realizar seu trabalho.

Para corrigir esses problemas, recomenda-se que as mesmas abordagens mencionadas em Eventos [de processamento, Pré-processadores de replicação e Tarefas](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs) sejam usadas.

## Processadores Sling POST e páginas excluídas {#sling-post-processors-and-deleted-pages}

Há algumas sessões administrativas usadas em implementações do processador POST. Normalmente, as sessões administrativas são usadas para acessar nós que estão com exclusão pendente no POST que está sendo processado. Consequentemente, eles não estão mais disponíveis por meio da sessão de solicitação. Um nó com exclusão pendente pode ser acessado para revelar uma metáada que, de outra forma, não deveria estar acessível.
