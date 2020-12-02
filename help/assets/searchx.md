---
title: Amplie a funcionalidade de pesquisa.
description: Estenda os recursos de pesquisa de [!DNL Adobe Experience Manager Assets] além dos padrões.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 19%

---


# Estender pesquisa de ativos {#extending-assets-search}

Você pode estender [!DNL Adobe Experience Manager Assets] os recursos de pesquisa. A partir da caixa, [!DNL Experience Manager Assets] procura ativos por strings.

A pesquisa é feita pela interface do QueryBuilder para que a pesquisa possa ser personalizada com vários predicados. Você pode sobrepor o conjunto padrão de predicados no seguinte diretório: `/apps/dam/content/search/searchpanel/facets`.

Você também pode adicionar outras guias ao painel administrativo [!DNL Assets].

>[!CAUTION]
>
>A partir de [!DNL Experience Manager] 6.4, a interface clássica está obsoleta. Para o anúncio, consulte [recursos obsoletos e removidos](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html). O Adobe recomenda o uso da interface habilitada para toque. Para personalização, consulte [aspectos de pesquisa](/help/assets/search-facets.md).

## Sobreposição {#overlaying}

Para sobrepor os predicados pré-configurados, copie o nó `facets` de `/libs/dam/content/search/searchpanel` para `/apps/dam/content/search/searchpanel/` ou especifique outra propriedade `facetURL` na configuração `searchpanel` (o padrão é `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`).

![screen_shot_2012-06-05at113619am](assets/screen_shot_2012-06-05at113619am.png)

>[!NOTE]
>
>Por padrão, a estrutura de diretório em `/apps` não existe, portanto, crie-a. Certifique-se de que os tipos de nó correspondem aos de `/libs`.

## Adicionar guias {#adding-tabs}

Você pode adicionar outras guias de pesquisa configurando-as na interface administrativa [!DNL Assets]. Para criar guias adicionais:

1. Crie a estrutura de pastas `/apps/wcm/core/content/damadmin/tabs,`se ela ainda não existir, e copie o nó `tabs` de `/libs/wcm/core/content/damadmin` e cole-o.
1. Crie e configure a segunda guia, conforme desejado.

   >[!NOTE]
   >
   >Ao criar um segundo `siteadminsearchpanel`, certifique-se de definir uma propriedade `id` para evitar conflitos de formulário.

## Criar predicados personalizados {#creating-custom-predicates}

[!DNL Assets] vem com um conjunto de predicados predefinidos que podem ser usados para personalizar uma página de compartilhamento de ativos. Personalizar um compartilhamento de ativos dessa forma é abordado em [criar e configurar uma página de compartilhamento de ativos](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

Além de usar predicados preexistentes, os desenvolvedores [!DNL Experience Manager] também podem criar seus próprios predicados usando a [API do Construtor de Query](/help/sites-developing/querybuilder-api.md).

A criação de predicados personalizados requer conhecimento básico sobre a [estrutura de widgets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

A prática recomendada é copiar um predicado existente e ajustá-lo. Os predicados de amostra estão localizados em **/libs/cq/search/components/predicados**.

### Exemplo: Criar um predicado de propriedade simples {#example-build-a-simple-property-predicate}

Para criar um predicado de propriedade:

1. Crie uma pasta de componentes no diretório de projetos, por exemplo **/apps/geometrixx/components/titlepredicate**.
1. Adicionar **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Adicionar `titlepredicate.jsp`.

   ```java
   <%--
   
     Sample title predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Title</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:title";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // createId adds a counter to the predicate name - useful in case this predicate
           // is inserted multiple times on the same page.
           var id = qb.createId(predicateName);
   
           // Hidden field that defines the property to search for; in our case this
           // is the "dc:title" metadata. The name "property" (or "1_property", "2_property" etc.)
           // indicates the server to use the property predicate
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id,
               "value": propertyName
           });
   
           // The visible text field. The name has to be like the one of the hidden field above
           // plus the ".value" suffix.
           qb.addField({
               "xtype": "textfield",
               "renderTo": elemId,
               "name": id + ".value"
           });
   
           // Depending on the predicate additional parameters allow to configure the
           // predicate. Here we add an operation parameter to create a "like" query.
           // Again note the name set to the id and a suffix.
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id + ".operation",
               "value": "like"
           });
       });
   </script>
   ```

1. Para disponibilizar o componente, é necessário editá-lo. Para tornar um componente editável, no CRXDE, adicione um nó **cq:editConfig** do tipo primário **cq:EditConfig**. Para que possa remover parágrafos, adicione uma propriedade de vários valores **cq:actions** com um único valor **DELETE**.
1. Navegue até o navegador e, na página de amostra (por exemplo, **press.html**), alterne para o modo de design e ative o novo componente para o sistema de parágrafo do predicado (por exemplo, **left**).

1. No modo **Editar**, o novo componente agora está disponível no sidekick (encontrado no grupo **Pesquisar**). Insira o componente na coluna **Predicados** e digite uma palavra de pesquisa, por exemplo, **Diamond** e clique na lupa para start da pesquisa.

   >[!NOTE]
   >
   >Ao pesquisar, digite exatamente o termo, incluindo as letras maiúsculas e minúsculas corretas.

### Exemplo: Criar um predicado de grupo simples {#example-build-a-simple-group-predicate}

Para criar um predicado de grupo:

1. Crie uma pasta de componentes no diretório de projetos, por exemplo **/apps/geometrixx/components/picspredicate.**
1. Adicionar **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Adicione **titlepredicate.jsp**:

   ```java
   <%--
   
     Sample group predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page.
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Image Formats</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:format";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // Create a unique group ID; will return e.g. "1_group".
           var groupId = qb.createGroupId();
   
           // Hidden field that defines the property to search for  - in our case "dc:format" -
           // and declares the group of predicates. "property" in the name ("1_group.property")
           // indicates to the server to use the "property predicate"
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": "<%= elemId %>",
               "name": groupId + "." + predicateName, // 1_group.property
               "value": propertyName
           });
   
           // Declare to combine the multiple values using OR.
           qb.add(new CQ.Ext.form.Hidden({
               "name": groupId + ".p.or",  // 1_group.p.or
               "value": "true"
           }));
   
           // The options
           var options = [
               { "label":"JPEG", "value":"image/jpeg"},
               { "label":"PNG",  "value":"image/png" },
               { "label":"GIF",  "value":"image/gif" }
           ];
   
           // Build a checkbox for each option.
           for (var i = 0; i < options.length; i++) {
               qb.addField({
                   "xtype": "checkbox",
                   "renderTo": "<%= elemId %>",
                   // 1_group.property.0_value, 1_group.property.1_value etc.
                   "name": groupId + "." +  predicateName + "." + i + "_value",
                   "inputValue": options[i].value,
                   "boxLabel": options[i].label,
                   "listeners": {
                       "check": function() {
                           // Submit the search form when checking/unchecking a checkbox.
                           qb.submit();
                       }
                   }
               });
           }
       });
   ```

1. Para disponibilizar o componente, é necessário editá-lo. Para tornar um componente editável, no CRXDE, adicione um nó **cq:editConfig** do tipo primário **cq:EditConfig**. Para que possa remover parágrafos, adicione uma propriedade de vários valores **cq:actions** com um único valor **DELETE**.
1. Navegue até o navegador e, na página de amostra (por exemplo, **press.html**), alterne para o modo de design e ative o novo componente para o sistema de parágrafo do predicado (por exemplo, **left**).
1. No modo **Editar**, o novo componente agora está disponível no sidekick (encontrado no grupo **Pesquisar**). Insira o componente na coluna **Predicados**.

## Widgets previstos instalados {#installed-predicate-widgets}

Os seguintes predicados estão disponíveis como widgets ExtJS pré-configurados.

### Predicado de texto completo {#fulltextpredicate}

| Propriedade | Tipo | Descrição |
|---|---|---|
| predicateName | Sequência de caracteres | Nome do predicado. O padrão é `fulltext` |
| searchCallback | Função | Retorno de chamada para acionar a pesquisa no evento `keyup`. O padrão é `CQ.wcm.SiteAdmin.doSearch` |

### PropertyPredicate {#propertypredicate}

| Propriedade | Tipo | Descrição |
|---|---|---|
| predicateName | Sequência de caracteres | Nome do predicado. O padrão é `property` |
| propertyName | Sequência de caracteres | Nome da propriedade JCR. O padrão é `jcr:title` |
| defaultValue | Sequência de caracteres | Valor padrão pré-preenchido. |

### PathPredicate {#pathpredicate}

| Propriedade | Tipo | Descrição |
|---|---|---|
| predicateName | Sequência de caracteres | Nome do predicado. O padrão é `path` |
| rootPath | Sequência de caracteres | Caminho raiz do predicado. O padrão é `/content/dam` |
| pathFieldPredicateName | Sequência de caracteres | O padrão é `folder` |
| showFlatOption | Booleano | Sinalizador para mostrar a caixa de seleção `search in subfolders`. O padrão é true. |

### DatePredicate {#datepredicate}

| Propriedade | Tipo | Descrição |
|---|---|---|
| predicateName | Sequência de caracteres | Nome do predicado. O padrão é `daterange` |
| propertyname | Sequência de caracteres | Nome da propriedade JCR. O padrão é `jcr:content/jcr:lastModified` |
| defaultValue | Sequência de caracteres | Valor padrão pré-preenchido |

### OpçõesPredicar {#optionspredicate}

| Propriedade | Tipo | Descrição |
|---|---|---|
| título | Sequência de caracteres | Adiciona um título superior adicional |
| predicateName | Sequência de caracteres | Nome do predicado. O padrão é `daterange` |
| propertyname | Sequência de caracteres | Nome da propriedade JCR. O padrão é `jcr:content/metadata/cq:tags` |
| colapso | Sequência de caracteres | Reduzir nível. O padrão é `level1` |
| triggerSearch | Booleano | Sinalizador para acionar a pesquisa na verificação. O padrão é false |
| searchCallback | Função | Retorno de chamada para acionar a pesquisa. O padrão é `CQ.wcm.SiteAdmin.doSearch` |
| searchTimeoutTime | Número | Tempo limite antes de o searchCallback ser disparado. O padrão é 800 ms |

## Personalizar os resultados da pesquisa {#customizing-search-results}

A apresentação dos resultados da pesquisa em uma página Compartilhamento de ativos é regida pela lente selecionada. [!DNL Experience Manager Assets] vem com um conjunto de lentes predefinidas que podem ser usadas para personalizar uma página de compartilhamento de ativos. Personalizar um compartilhamento de ativos desta forma é abordado em [Criar e configurar uma página de compartilhamento de ativos](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

Além de usar lentes pré-existentes, os desenvolvedores [!DNL Experience Manager] também podem criar suas próprias lentes.
