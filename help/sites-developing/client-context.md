---
title: Contexto do cliente em detalhes
seo-title: Contexto do cliente em detalhes
description: O Contexto do Cliente representa uma coleção dinâmica de dados do usuário
seo-description: O Contexto do Cliente representa uma coleção dinâmica de dados do usuário
uuid: 95b08fbd-4f50-44a1-80fb-46335fe04a40
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c881ad66-bcc3-4f99-b77f-0944c23e2d29
docset: aem65
feature: Context Hub
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3025'
ht-degree: 0%

---


# Contexto do Cliente em Detalhe{#client-context-in-detail}

>[!NOTE]
>
>O Contexto do Cliente foi substituído pelo ContextHub. Consulte a [documentação relacionada](/help/sites-developing/contexthub.md) para obter detalhes.

O Contexto do Cliente representa uma coleção dinâmica de dados do usuário. Você pode usar os dados para determinar o conteúdo a ser exibido em uma página da Web em uma determinada situação (direcionamento de conteúdo). Os dados também estão disponíveis para análises de sites e para qualquer javascript na página.

O Contexto do Cliente consiste principalmente nos seguintes aspectos:

* O armazenamento de sessão, que contém os dados do usuário.
* A interface do usuário que exibe os dados do usuário e fornece ferramentas para simular a experiência do usuário.
* Uma [API javascript](/help/sites-developing/ccjsapi.md) para interagir com armazenamentos de sessão.

Para criar um armazenamento de sessão independente e adicioná-lo ao Contexto do Cliente ou criar um armazenamento de sessão vinculado a um componente do Armazenamento de Contexto. AEM instala vários componentes da Loja de contexto que você pode usar imediatamente. Você pode usar esses componentes como base para seus componentes.

Para obter informações sobre como abrir o Contexto do Cliente, configurar as informações exibidas e simular a experiência do usuário, consulte [Contexto do Cliente](/help/sites-administering/client-context.md).

## Lojas de sessão {#session-stores}

O Contexto do Cliente inclui vários armazenamentos de sessão que contêm dados do usuário. Os dados de armazenamento vêm das seguintes fontes:

* O navegador da Web do cliente.
* O servidor (consulte [JSONP Store](/help/sites-administering/client-context.md#main-pars-variable-8) para armazenar informações de fontes de terceiros)

A estrutura de Contexto do Cliente fornece uma [API javascript](/help/sites-developing/ccjsapi.md) que você pode usar para interagir com armazenamentos de sessão para ler e gravar dados do usuário e ouvir e reagir a eventos de armazenamento. Você também pode criar armazenamentos de sessão para dados do usuário que você usa para direcionamento de conteúdo ou outros fins.

Os dados do armazenamento da sessão permanecem no cliente. O Contexto do Cliente não grava dados de volta no servidor. Para enviar dados ao servidor, use um formulário ou desenvolva um javascript personalizado.

Cada armazenamento de sessão é uma coleção de pares de valores de propriedade. O armazenamento de sessão representa uma coleção de dados (de qualquer tipo), cujo significado conceitual pode ser decidido pelo designer e/ou desenvolvedor. O exemplo de código javascript a seguir define um objeto que representa os dados de perfil que o armazenamento de sessão pode conter:

```
{
  age: 20,
  authorizableId: "aparker@geometrixx.info",
  birthday: "27 Feb 1992",
  email: "aparker@geometrixx.info",
  formattedName: "Alison Parker",
  gender: "female",
  path: "/home/users/geometrixx/aparker@geometrixx.info/profile"
}
```

Um armazenamento de sessão pode ser mantido nas sessões do navegador ou pode durar apenas para a sessão do navegador em que foi criado.

>[!NOTE]
>
>A persistência de armazenamento usa o armazenamento do navegador ou os cookies (o cookie `SessionPersistence`). O armazenamento do navegador é mais comum.
>
>Quando o navegador é fechado e reaberto, um armazenamento de sessão pode ser carregado com os valores de um armazenamento persistente. A limpeza do cache do navegador é necessária para remover os valores antigos.

### Componentes do armazenamento de contexto {#context-store-components}

Um componente de armazenamento de contexto é um componente CQ que pode ser adicionado ao Contexto do Cliente. Normalmente, os componentes do armazenamento de contexto exibem dados de um armazenamento de sessão com o qual estão associados. No entanto, as informações exibidas pelos componentes do armazenamento de contexto não se limitam aos dados do armazenamento de sessão.

Os componentes do armazenamento de contexto podem incluir os seguintes itens:

* Scripts JSP que definem a aparência no Contexto do Cliente.
* Propriedades para listar o componente no Sidekick.
* Edite caixas de diálogo para configurar instâncias de componente.
* Javascript que inicializa o armazenamento de sessão.

Para obter uma descrição dos Componentes do Armazenamento de Contexto instalados que você pode adicionar ao Armazenamento de Contexto, consulte [Componentes de Contexto do Cliente Disponíveis](/help/sites-administering/client-context.md#available-client-context-components).

>[!NOTE]
>
>Os dados da página não estão mais no contexto do cliente como um componente padrão. Se necessário, é possível adicionar isso editando o contexto do cliente, adicionando o componente **Propriedades de armazenamento genérico** e configurando-o para definir a **Loja** como `pagedata`.

### Entrega de conteúdo direcionada {#targeted-content-delivery}

As informações de perfil também são usadas para fornecer [conteúdo direcionado](/help/sites-authoring/content-targeting-touch.md).

![clientcontext_](assets/clientcontext_targetedcontentdelivery.png) ![targetedcontentdeliveryclientcontext_targetedcontentdeliverydetail](assets/clientcontext_targetedcontentdeliverydetail.png)

## Adicionar contexto do cliente a uma página {#adding-client-context-to-a-page}

Inclua o componente Contexto do Cliente na seção de corpo de suas páginas da Web para ativar o Contexto do Cliente. O caminho do nó do componente Contexto do Cliente é `/libs/cq/personalization/components/clientcontext`. Para incluir o componente, adicione o seguinte código ao arquivo JSP do componente de página, localizado logo abaixo do elemento `body` da página:

```java
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

O componente clientcontext faz com que a página carregue as bibliotecas de clientes que implementam o ClientContext.

* A API javascript do Contexto do Cliente.
* A estrutura Contexto do Cliente que suporta armazenamentos de sessão, gerenciamento de eventos, etc.
* Segmentos definidos.
* Os scripts init.js gerados para cada componente de armazenamento de contexto que foi adicionado ao Contexto do Cliente.
* (Somente instância do autor) A interface do usuário de contexto do cliente.

A interface do usuário de contexto do cliente está disponível somente na instância do autor.

## Extensão do contexto do cliente {#extending-client-context}

Para estender o Contexto do Cliente, crie um armazenamento de sessão e, como opção, exiba os dados do armazenamento:

* Crie um armazenamento de sessão para os dados do usuário necessários para direcionamento de conteúdo e análise da Web.
* Crie um componente de armazenamento de contexto para permitir que os administradores configurem o armazenamento de sessão associado e exibam dados de armazenamento no Contexto do Cliente para fins de teste.

>[!NOTE]
>
>Se você tiver (ou criar) um serviço `JSONP` que possa fornecer os dados, poderá simplesmente usar o componente de armazenamento de contexto `JSONP` e mapeá-lo para o serviço JSONP. Isso lidará com o armazenamento de sessão.

### Criação de um armazenamento de sessão {#creating-a-session-store}

Crie um armazenamento de sessão para os dados que você precisa adicionar e recuperar do Contexto do Cliente. Geralmente, você usa o seguinte procedimento para criar um armazenamento de sessão:

1. Crie uma pasta da biblioteca do cliente que tenha um valor de propriedade `categories` de `personalization.stores.kernel`. O Contexto do Cliente carrega automaticamente as bibliotecas do cliente desta categoria.

1. Configure a pasta da biblioteca do cliente para que ela tenha uma dependência na pasta da biblioteca do cliente `personalization.core.kernel`. A biblioteca do cliente `personalization.core.kernel` fornece a API javascript do Contexto do Cliente.

1. Adicione o javascript que cria e inicializa o armazenamento de sessão.

A inclusão do javascript na biblioteca de clientes personalization.stores.kernel faz com que a loja seja criada quando a estrutura Contexto do Cliente for carregada.

>[!NOTE]
>
>Se estiver criando um armazenamento de sessão como parte de um componente de armazenamento de contexto, você pode, como alternativa, colocar o javascript no arquivo init.js.jsp do componente. Nesse caso, o armazenamento de sessão é criado somente se o componente for adicionado ao Contexto do Cliente.

#### Tipos de armazenamentos de sessão {#types-of-session-stores}

Os armazenamentos de sessão são criados e disponibilizados durante uma sessão do navegador ou persistem no armazenamento do navegador ou nos cookies. A API javascript de Contexto do Cliente define várias classes que representam ambos os tipos de armazenamentos de dados:

* ` [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore)`: Esses objetos residem somente no DOM da página. Os dados são criados e mantidos durante a vida útil da página.
* ` [CQ_Analytics.PerstistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore)`: Esses objetos residem no DOM da página e são mantidos no armazenamento do navegador ou em cookies. Os dados estão disponíveis em páginas e em sessões de usuário.

A API também fornece extensões dessas classes especializadas para armazenar dados JSON ou dados JSONP:

* Objetos somente sessão: [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonstore) e [CQ_Analytics.JSONPStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonpstore).

* Objetos persistentes: [CQ_Analytics.PersistedJSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedjsonstore) e [CQ_Analytics.PersistedJSONPStore](/help/sites-developing/ccjsapi.md#cq-analyics-persistedjsonpstore).

#### Criando o objeto do armazenamento de sessão {#creating-the-session-store-object}

O javascript da pasta da biblioteca de clientes cria e inicializa o armazenamento de sessão. O armazenamento de sessão deve ser registrado usando o Gerenciador de armazenamento de contexto. O exemplo a seguir cria e registra um objeto [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore).

```
//Create the session store
if (!CQ_Analytics.MyStore) {
    CQ_Analytics.MyStore = new CQ_Analytics.SessionStore();
    CQ_Analytics.MyStore.STOREKEY = "MYSTORE";
    CQ_Analytics.MyStore.STORENAME = "mystore";
    CQ_Analytics.MyStore.data={};
}
//register the session store
if (CQ_Analytics.ClientContextMgr){
    CQ_Analytics.ClientContextMgr.register(CQ_Analytics.MyStore)
}
```

Para armazenar dados JSON, o exemplo a seguir cria e registra um objeto [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore).

```
if (!CQ_Analytics.myJSONStore) {
    CQ_Analytics.myJSONStore = CQ_Analytics.JSONStore.registerNewInstance("myjsonstore",{});
}
```

### Criação de um componente de armazenamento de contexto {#creating-a-context-store-component}

Crie um componente de armazenamento de contexto para renderizar dados de armazenamento de sessão no Contexto do Cliente. Depois de criado, você pode arrastar seu componente de armazenamento de contexto para o Contexto do Cliente para renderizar dados de um armazenamento de sessão. Os componentes do armazenamento de contexto consistem nos seguintes itens:

* Script JSP para renderizar os dados.
* Uma caixa de diálogo de edição.
* Um script JSP para inicializar o armazenamento de sessão.
* (Opcional) Uma pasta da biblioteca do cliente que cria o armazenamento da sessão. Não há necessidade de incluir a pasta da biblioteca do cliente se o componente usar um armazenamento de sessão existente.

#### Extensão dos componentes fornecidos do armazenamento de contexto {#extending-the-provided-context-store-components}

AEM fornece o armazenamento genérico e os componentes do armazenamento de contexto genericstoreproperties que você pode estender. A estrutura dos dados da loja determina o componente que você estende:

* Pares de valor de propriedade: Estenda o componente `GenericStoreProperties`. Esse componente renderiza automaticamente lojas de pares de valores de propriedade. Vários pontos de interação são fornecidos:

   * `prolog.jsp` e  `epilog.jsp`: interação de componente que permite adicionar lógica do lado do servidor antes ou depois da renderização do componente.

* Dados complexos: Estenda o componente `GenericStore`. O armazenamento de sessão precisará de um método de &quot;renderizador&quot; que será chamado sempre que o componente precisar ser renderizado. A função renderizadora é chamada com dois parâmetros:

   * `@param {String} store`
A loja a renderizar

   * `@param {String} divId`
Id do div no qual o armazenamento deve ser renderizado.

>[!NOTE]
>
>Todos os componentes de Contexto do Cliente são extensões dos componentes Loja Genérica ou Propriedades de Loja Genérica. Vários exemplos são instalados na pasta `/libs/cq/personalization/components/contextstores`.

#### Configurar a aparência no Sidekick {#configuring-the-appearance-in-sidekick}

Ao editar o Contexto do Cliente, os componentes do armazenamento de contexto são exibidos no Sidekick. Como em todos os componentes, as propriedades `componentGroup` e `jcr:title` do componente de contexto do cliente determinam o grupo e o nome do componente.

Todos os componentes que têm um valor de propriedade `componentGroup` de `Client Context` aparecem no Sidekick por padrão. Se você usar um valor diferente para a propriedade `componentGroup`, deverá adicionar manualmente o componente ao Sidekick usando o modo Design.

#### Instâncias do componente de armazenamento de contexto {#context-store-component-instances}

Ao adicionar um componente de armazenamento de contexto ao Contexto do Cliente, um nó que representa a instância do componente é criado abaixo de `/etc/clientcontext/default/content/jcr:content/stores`. Esse nó contém os valores da propriedade que são configurados usando a caixa de diálogo Editar do componente.

Quando o Contexto do Cliente é inicializado, esses nós são processados.

#### Inicializando o Repositório de Sessões Associado {#initializing-the-associated-session-store}

Adicione um arquivo init.js.jsp ao seu componente para gerar um código javascript que inicializa o armazenamento de sessão que seu componente de armazenamento de contexto usa. Por exemplo, use o script de inicialização para recuperar as propriedades de configuração do componente e usá-las para preencher o armazenamento de sessão.

O javascript gerado é adicionado à página quando o Contexto do Cliente é inicializado no carregamento da página nas instâncias de autor e de publicação. Esse JSP é executado antes que a instância do componente de armazenamento de contexto seja carregada e renderizada.

O código deve definir o tipo mime do arquivo para `text/javascript` ou não é executado.

>[!CAUTION]
>
>O script init.js.jsp é executado na instância de criação e publicação, mas somente se o componente de armazenamento de contexto for adicionado ao Contexto do Cliente.

O procedimento a seguir cria o arquivo de script init.js.jsp e adiciona o código que define o tipo mime correto. O código que executa a inicialização de armazenamento seria seguido.

1. Clique com o botão direito do mouse no nó do componente de armazenamento de contexto e clique em Criar > Criar arquivo.
1. No campo Nome , digite `init.js.jsp` e clique em OK.
1. Na parte superior da página, adicione o seguinte código e clique em Salvar tudo.

   ```java
   <%@page contentType="text/javascript" %>
   ```

### Renderização de dados do armazenamento de sessão para componentes de propriedades de armazenamento genérico {#rendering-session-store-data-for-genericstoreproperties-components}

Exibir dados do armazenamento da sessão no Contexto do Cliente usando um formato consistente.

#### Exibição dos dados de propriedade {#displaying-property-data}

O taglib de personalização fornece a tag `personalization:storePropertyTag` que exibe o valor de uma propriedade de um armazenamento de sessão. Para usar a tag , inclua a seguinte linha de código no arquivo JSP:

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

A tag tem o seguinte formato:

```xml
<personalization:storePropertyTag propertyName="property_name" store="session_store_name"/>
```

O atributo `propertyName` é o nome da propriedade de armazenamento a ser exibida. O atributo `store` é o nome do armazenamento registrado. A tag de exemplo a seguir exibe o valor da propriedade `authorizableId` do armazenamento `profile`:

```xml
<personalization:storePropertyTag propertyName="authorizableId" store="profile"/>
```

#### Estrutura HTML {#html-structure}

A pasta da biblioteca do cliente personalization.ui (/etc/clientlibs/foundation/personalization/ui/themes/default) fornece os estilos CSS que o Client Context usa para formatar o código HTML. O código a seguir ilustra a estrutura sugerida a ser usada para exibir dados da loja:

```xml
<div class="cq-cc-store">
   <div class="cq-cc-thumbnail">
      <div class="cq-cc-store-property">
           <!-- personalization:storePropertyTag for the store thumbnail image goes here -->
      </div>
   </div>
   <div class="cq-cc-content">
       <div class="cq-cc-store-property cq-cc-store-property-level0">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level1">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level2">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level3">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
   </div>
   <div class="cq-cc-clear"></div>
</div>
```

O componente de armazenamento de contexto `/libs/cq/personalization/components/contextstores/profiledata` usa essa estrutura para exibir dados do armazenamento de sessão do perfil. A classe `cq-cc-thumbnail` coloca a imagem em miniatura. As classes `cq-cc-store-property-level*x*` formatam os dados alfanuméricos:

* level0, level1 e level2 são distribuídos verticalmente e usam uma fonte branca.
* o nível3 e quaisquer níveis adicionais são distribuídos horizontalmente e usam uma fonte branca com um plano de fundo mais escuro.

![chlimage_1-4](assets/chlimage_1-4.png)

### Renderizar dados do armazenamento da sessão para componentes do armazenamento genérico {#rendering-session-store-data-for-genericstore-components}

Para renderizar dados de armazenamento usando um componente de armazenamento de genéricos, é necessário:

* Adicione a tag personalization:storeRendererTag ao script JSP do componente para identificar o nome do armazenamento de sessão.
* Implemente um método de renderização na classe de armazenamento da sessão.

#### Identificação do armazenamento genérico Armazenamento de sessão {#identifying-the-genericstore-session-store}

O taglib de personalização fornece a tag `personalization:storePropertyTag` que exibe o valor de uma propriedade de um armazenamento de sessão. Para usar a tag , inclua a seguinte linha de código no arquivo JSP:

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

A tag tem o seguinte formato:

```java
<personalization:storeRendererTag store="store_name"/>
```

#### Implementando o método de renderização do Repositório de Sessões {#implementing-the-session-store-renderer-method}

O armazenamento de sessão precisará de um método de &quot;renderizador&quot; que será chamado sempre que o componente precisar ser renderizado. A função renderizadora é chamada com dois parâmetros:

* repositório @param {String}
A loja a renderizar
* @param {String} divId
Id do div no qual o armazenamento deve ser renderizado.

## Interagir com armazenamentos de sessão {#interacting-with-session-stores}

Use o javascript para interagir com armazenamentos de sessão.

### Acessar armazenamentos de sessão {#accessing-session-stores}

Obtenha um objeto de armazenamento de sessão para ler ou gravar dados no armazenamento. [CQ_Analytics.](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextmgr) ClientContextMgrfornece acesso às lojas com base no nome da loja. Depois de obtido, use os métodos do [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) ou [CQ_Analytics.PersistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore) para interagir com os dados de armazenamento.

O exemplo a seguir obtém o armazenamento `profile` e recupera a propriedade `formattedName` do armazenamento.

```
function getName(){
   var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
   if(profilestore){
      return profilestore.getProperty("formattedName", false);
   } else {
      return null;
   }
}
```

### Criação de um ouvinte para reagir a uma atualização do armazenamento de sessão {#creating-a-listener-to-react-to-a-session-store-update}

A sessão armazena eventos de acionamento, portanto, é possível adicionar ouvintes e acionar eventos com base nesses eventos.

Os armazenamentos de sessão são criados no padrão `Observable`. Eles estendem [ `CQ_Analytics.Observable`](/help/sites-developing/ccjsapi.md#cq-analytics-observable) que fornece o método ` [addListener](/help/sites-developing/ccjsapi.md#addlistener-event-fct-scope)`.

O exemplo a seguir adiciona um ouvinte ao evento `update` do armazenamento de sessão `profile`.

```
var profileStore = ClientContextMgr.getRegisteredStore("profile");
if( profileStore ) {
  //callback execution context
  var executionContext = this;

  //add "update" event listener to store
  profileStore.addListener("update",function(store, property) {
    //do something on store update

  },executionContext);
}
```

### Verificando se um Repositório de Sessões está definido e inicializado {#checking-that-a-session-store-is-defined-and-initialized}

Os armazenamentos de sessão não estão disponíveis até serem carregados e inicializados com dados. Os seguintes fatores podem afetar o tempo de disponibilidade do armazenamento da sessão:

* Carregamento de página
* Carregamento de JavaScript
* Tempo de execução do JavaScript
* Tempos de resposta para solicitações XHR
* Alterações dinâmicas no armazenamento de sessão

Use os métodos [CQ_Analytics.ClientContextUtils](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextutils) do objeto [onStoreRegistered](/help/sites-developing/ccjsapi.md#onstoreregistered-storename-callback) e [onStoreInitialized](/help/sites-developing/ccjsapi.md#onstoreinitialized-storename-callback-delay) para acessar os armazenamentos de sessão somente quando estiverem disponíveis. Esses métodos permitem registrar ouvintes de eventos que reagem aos eventos de registro e inicialização da sessão.

>[!CAUTION]
>
>Se você depender de outra loja, precisará atender o caso de a loja nunca ser registrada.

O exemplo a seguir usa o evento `onStoreRegistered` do armazenamento de sessão `profile`. Quando a loja é registrada, um ouvinte é adicionado ao evento `update` do armazenamento de sessão. Quando a loja é atualizada, o conteúdo do elemento `<div class="welcome">` na página é atualizado com o nome da loja `profile`.

```
//listen for the store registration
CQ_Analytics.ClientContextUtils.onStoreRegistered("profile", listen);

//listen for the store's update event
function listen(){
 var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
    profilestore.addListener("update",insertName);
}

//insert the welcome message
function insertName(){
 $("div.welcome").text("Welcome "+getName());
}

//obtain the name from the profile store
function getName(){
 var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
 if(profilestore){
  return profilestore.getProperty("formattedName", false);
    } else {
        return null;
    }
}
```

### Excluir uma propriedade do cookie de persistência de sessão {#excluding-a-property-from-the-sessionpersistence-cookie}

Para evitar que uma propriedade de `PersistedSessionStore` seja persistente (ou seja, exclua-a do cookie `sessionpersistence`), adicione a propriedade à lista de propriedades não persistentes do armazenamento de sessão persistente.

Consulte ` [CQ_Analytics.PersistedSessionStore.setNonPersisted(propertyName)](/help/sites-developing/ccjsapi.md#setnonpersisted-name)`

```
CQ_Analytics.ClientContextUtils.onStoreRegistered("surferinfo", function(store) {
  //this will exclude the browser, OS and resolution properties of the surferinfo session store from the
  store.setNonPersisted("browser");
  store.setNonPersisted("OS");
  store.setNonPersisted("resolution");
});
```

## Configurar o controle deslizante do dispositivo {#configuring-the-device-slider}

### Condições {#conditions}

A página atual deve ter uma página móvel correspondente; isso é determinado somente se a página tiver uma LiveCopy configurada com uma configuração de implantação móvel ( `rolloutconfig.path.toLowerCase` contém `mobile`).

#### Configuração {#configuration}

Ao alternar da página de desktop para seu equivalente móvel:

* O DOM da página móvel é carregado.
* O principal `div` (obrigatório) que contém o conteúdo, é extraído e inserido na página de desktop atual.

* As classes CSS e body que precisam ser carregadas precisam ser configuradas manualmente.

Por exemplo:

```
window.CQMobileSlider["geometrixx-outdoors"] = {
  //CSS used by desktop that need to be removed when mobile
  DESKTOP_CSS: [
    "/etc/designs/${app}/clientlibs_desktop_v1.css"
  ],

  //CSS used by mobile that need to be removed when desktop
  MOBILE_CSS: [
    "/etc/designs/${app}/clientlibs_mobile_v1.css"
  ],

  //id of the content that needs to be removed when mobile
  DESKTOP_MAIN_ID: "main",

  //id of the content that needs to be removed when desktop
  MOBILE_MAIN_ID: "main",

  //body classes used by desktop that need to be removed when mobile
  DESKTOP_BODY_CLASS: [
    "page"
  ],

  //body classes used by mobile that need to be removed when desktop
  MOBILE_BODY_CLASS: [
    "page-mobile"
  ]
};
```

## Exemplo: Criação de um componente personalizado do armazenamento de contexto {#example-creating-a-custom-context-store-component}

Neste exemplo, você cria um componente de armazenamento de contexto que recupera dados de um serviço externo e o armazena no armazenamento de sessão:

* Estende o componente genericstoreproperties.
* Inicializa uma loja usando um objeto javascript CQ_Analytics.JSONPStore.
* Chama um serviço JSONP para recuperar dados e adicioná-los ao armazenamento.
* Renderiza os dados no Contexto do Cliente.

### Adicionar o componente geoloc {#add-the-geoloc-component}

Crie um aplicativo CQ e adicione o componente geoloc.

1. Abra o CRXDE Lite no navegador da Web ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Clique com o botão direito do mouse na pasta `/apps` e clique em Criar > Criar pasta. Especifique um nome de `myapp` e clique em OK.
1. Da mesma forma, abaixo de `myapp`, crie uma pasta chamada `contextstores`. &quot;
1. Clique com o botão direito do mouse na pasta `/apps/myapp/contextstores` e clique em Criar > Criar componente. Especifique os seguintes valores de propriedade e clique em Avançar:

   * Rótulo: geoloc
   * Título: Loja de localização
   * Supertipo: cq/personalization/components/contextstores/genericstoreproperties
   * Grupo: Contexto do cliente

1. Na caixa de diálogo Criar componente, clique em Avançar em cada página até que o botão OK esteja ativado e clique em OK.
1. Clique em Salvar tudo.

### Criar a caixa de diálogo de edição {#create-the-geoloc-edit-dialog}

O componente de armazenamento de contexto requer uma caixa de diálogo de edição. A caixa de diálogo de edição geográfica conterá uma mensagem estática indicando que não há propriedades a serem configuradas.

1. Clique com o botão direito do mouse no nó `/libs/cq/personalization/components/contextstores/genericstoreproperties/dialog` e clique em Copiar.
1. Clique com o botão direito do mouse no nó `/apps/myapp/contextstores/geoloc` e clique em colar.
1. Exclua todos os nós filhos abaixo do nó /apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items:

   * loja
   * propriedades
   * miniatura

1. Clique com o botão direito do mouse no nó `/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items` e clique em Criar > Criar nó. Especifique os seguintes valores de propriedade e clique em OK:

   * Nome: estático
   * Tipo: cq:Widget

1. Adicione as seguintes propriedades ao nó :

   | Nome | Tipo | Valor |
   |---|---|---|
   | cls | Sequência de caracteres | x-form-fieldset-description |
   | texto | Sequência de caracteres | O componente geoloc não requer configuração. |
   | xtype | Sequência de caracteres | estáticas |

1. Clique em Salvar tudo.

   ![chlimage_1-5](assets/chlimage_1-5.png)

### Criar o script de inicialização {#create-the-initialization-script}

Adicione um arquivo init.js.jsp ao componente geoloc e use-o para criar o armazenamento de sessão, recuperar os dados de localização e adicioná-los ao armazenamento.

O arquivo init.js.jsp é executado quando o Contexto do Cliente é carregado pela página. Por esse tempo, a API javascript do Contexto do Cliente será carregada e estará disponível no seu script.

1. Clique com o botão direito do mouse no nó /apps/myapp/contextstores/geoloc e clique em Criar > Criar arquivo. Especifique um Nome de init.js.jsp e clique em OK.
1. Adicione o seguinte código à parte superior da página e clique em Salvar tudo.

   ```java
   <%@page contentType="text/javascript;charset=utf-8" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   log.info("***** initializing geolocstore ****");
   String store = "locstore";
   String jsonpurl = "https://api.wipmania.com/jsonp?callback=${callback}";
   
   %>
   var locstore = CQ_Analytics.StoreRegistry.getStore("<%= store %>");
   if(!locstore){
    locstore = CQ_Analytics.JSONPStore.registerNewInstance("<%= store %>", "<%= jsonpurl %>",{});
   }
   <% log.info(" ***** done initializing geoloc ************"); %>
   ```

### Renderizar os dados do armazenamento de sessão geoloc {#render-the-geoloc-session-store-data}

Adicione o código ao arquivo JSP do componente geoloc para renderizar os dados de armazenamento no Contexto do Cliente.

![chlimage_1-6](assets/chlimage_1-6.png)

1. No CRXDE Lite, abra o arquivo `/apps/myapp/contextstores/geoloc/geoloc.jsp`.
1. Adicione o seguinte código HTML abaixo do código stub:

   ```xml
   <%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
   <div class="cq-cc-store">
      <div class="cq-cc-content">
          <div class="cq-cc-store-property cq-cc-store-property-level0">
              Continent: <personalization:storePropertyTag propertyName="address/continent" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level1">
              Country: <personalization:storePropertyTag propertyName="address/country" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level2">
              City: <personalization:storePropertyTag propertyName="address/city" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level3">
              Latitude: <personalization:storePropertyTag propertyName="latitude" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level4">
              Longitude: <personalization:storePropertyTag propertyName="longitude" store="locstore"/>
          </div>
      </div>
       <div class="cq-cc-clear"></div>
   </div>
   ```

1. Clique em Salvar tudo.

### Adicionar o componente ao contexto do cliente {#add-the-component-to-client-context}

Adicione o componente Armazenamento de localização ao Contexto do cliente para que ele seja inicializado quando a página for carregada.

1. Abra a página inicial do Geometrixx Outdoors na instância do autor ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html)).
1. Clique em Ctrl-Alt-c (windows) ou control-option-c (Mac) para abrir o Contexto do Cliente.
1. Clique no ícone de edição na parte superior do Contexto do Cliente para abrir o Designer de Contexto do Cliente.

   ![](do-not-localize/chlimage_1.png)

1. Arraste o componente Armazenamento de local para o Contexto do cliente.

### Consulte as Informações de localização no Contexto do Cliente {#see-the-location-information-in-client-context}

Abra a página inicial do Geometrixx Outdoors no modo de edição e, em seguida, abra o Contexto do Cliente para ver os dados do componente Armazenamento de Local.

1. Abra a página em inglês do site Geometrixx Outdoors. ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))
1. Para abrir o Contexto do Cliente, pressione Ctrl-Alt-c (windows) ou control-option-c (Mac).

## Criando um Contexto de Cliente Personalizado {#creating-a-customized-client-context}

Para criar um segundo contexto de cliente, você precisa duplicar a ramificação:

`/etc/clientcontext/default`

* A subpasta:
   `/content`
conterá o conteúdo do contexto de cliente personalizado.

* A pasta:
   `/contextstores`
permite definir configurações diferentes para os armazenamentos de contexto.

Para usar o contexto personalizado do cliente, edite a propriedade
`path`
no estilo de design do componente de contexto do cliente, conforme incluído no modelo da página. Por exemplo, como o local padrão de:
`/libs/cq/personalization/components/clientcontext/design_dialog/items/path`
