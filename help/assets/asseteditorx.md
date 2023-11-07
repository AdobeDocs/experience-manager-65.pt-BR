---
title: Estender editor de ativos
description: Saiba como estender os recursos do Editor de ativos usando componentes personalizados.
contentOwner: AG
role: User, Admin
feature: Developer Tools
exl-id: de1c63c1-a0e5-470b-8d83-b594513a5dbd
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 13%

---

# Estender editor de ativos {#extending-asset-editor}

O Editor de ativos é a página que abre quando um ativo encontrado por meio do Compartilhamento de ativos é clicado, permitindo que o usuário edite esses aspectos do ativo como metadados, miniatura, título e tags.

A configuração do editor usando os componentes de edição predefinidos é abordada em [Criação e configuração de uma página do Editor de ativos](assets-finder-editor.md#creating-and-configuring-an-asset-editor-page).

Além de usar componentes de editor pré-existentes, [!DNL Adobe Experience Manager] os desenvolvedores também podem criar seus próprios componentes.

## Criar um modelo do Editor de ativos {#creating-an-asset-editor-template}

As seguintes páginas de exemplo estão incluídas no Geometrixx:

* Página de exemplo do Geometrixx: `/content/geometrixx/en/press/asseteditor.html`
* Modelo de amostra: `/apps/geometrixx/templates/asseteditor`
* Componente de página de exemplo: `/apps/geometrixx/components/asseteditor`

### Configurar Clientlib {#configuring-clientlib}

[!DNL Assets] Os componentes do usam uma extensão da biblioteca WCM edit clientlib. Normalmente, as clientlibs são carregadas no `init.jsp`.

Comparado ao carregamento padrão do clientlib (nas `init.jsp`), um [!DNL Assets] O modelo deve ter o seguinte:

* O template deve incluir o `cq.dam.edit` clientlib (em vez de `cq.wcm.edit`).

* A clientlib também deve ser incluído no modo WCM desativado (por exemplo, carregado na **publicação**) para poder renderizar os predicados, as ações e as lentes.

Na maioria dos casos, copiar a amostra existente `init.jsp` (`/apps/geometrixx/components/asseteditor/init.jsp`) devem atender a essas necessidades.

### Configurar ações JS {#configuring-js-actions}

Alguns dos [!DNL Assets] componentes exigem funções JS definidas em `component.js`. Copie este arquivo para o diretório do componente e vincule-o.

```javascript
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

A amostra carrega essa origem de JavaScript no `head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`).

### Folhas de estilos adicionais {#additional-style-sheets}

Alguns dos [!DNL Assets] componentes usam a biblioteca de widgets. Para ser renderizada corretamente no contexto de conteúdo, uma folha de estilos adicional deve ser carregada. O componente de ação de tag requer mais um.

```css
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Folha de Estilos do Geometrixx {#geometrixx-style-sheet}

Os componentes de página de exemplo exigem que todos os seletores comecem com `.asseteditor` de `static.css` (`/etc/designs/geometrixx/static.css`). Prática recomendada: Copiar tudo `.asseteditor` seletores para sua folha de estilos e ajuste as regras conforme desejado.

### FormChooser: ajustes para recursos eventualmente carregados {#formchooser-adjustments-for-eventually-loaded-resources}

O Editor de ativos usa o Seletor de formulários, que permite editar recursos — neste caso, ativos — na mesma página de formulário simplesmente adicionando um seletor de formulários e o caminho do formulário para o URL do ativo.

Por exemplo:

* Página de forma simples: [http://localhost:4502/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/geometrixx/en/press/asseteditor.html)
* Ativo carregado na página do formulário: [http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html)

A amostra lida com `head.jsp` (`/apps/geometrixx/components/asseteditor/head.jsp`) faça o seguinte:

* Eles detectam se um ativo é carregado ou se o formulário simples deve ser exibido.
* Se um ativo for carregado, ele desativará o modo WCM, pois parsys só pode ser editado em uma página de formulário simples.
* Se um ativo for carregado, eles usarão seu título em vez do título na página do formulário.

```javascript
 List<Resource> resources = FormsHelper.getFormEditResources(slingRequest);
    if (resources != null) {
        if (resources.size() == 1) {
            // single resource
            FormsHelper.setFormLoadResource(slingRequest, resources.get(0));
        } else if (resources.size() > 1) {
            // multiple resources
            // not supported by CQ 5.3
        }
    }
    Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
    String title;
    if (loadResource != null) {
        // an asset is loaded: disable WCM
        WCMMode.DISABLED.toRequest(request);

        String path = loadResource.getPath();
        Asset asset = loadResource.adaptTo(Asset.class);
        try {
            // it might happen that the adobe xmp lib creates an array
            Object titleObj = asset.getMetadata("dc:title");
            if (titleObj instanceof Object[]) {
                Object[] titleArray = (Object[]) titleObj;
                title = (titleArray.length > 0) ? titleArray[0].toString() : "";
            } else {
                title = titleObj.toString();
            }
        }
        catch (NullPointerException e) {
            title = path.substring(path.lastIndexOf("/") + 1);
        }
    }
    else {
        title = currentPage.getTitle() == null ? currentPage.getName() : currentPage.getTitle();
    }
```

Na parte HTML, use o conjunto de títulos anterior (título de ativo ou página):

```html
<title><%= title %></title>
```

## Criar um componente de campo de formulário simples {#creating-a-simple-form-field-component}

Este exemplo descreve como criar um componente que mostra e exibe os metadados de um ativo carregado.

1. Crie uma pasta de componentes no diretório de projetos, por exemplo, `/apps/geometrixx/components/samplemeta`.
1. Adicionar `content.xml` com o seguinte trecho:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. Adicionar `samplemeta.jsp` com o seguinte trecho:

   ```javascript
   <%--
   
     Sample metadata field component
   
   --%><%@ page import="com.day.cq.dam.api.Asset,
                    java.security.AccessControlException" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       String value = "";
       String name = "dam:sampleMetadata";
       boolean readOnly = false;
   
       // If the form page is requested for an asset loadResource is the asset.
       Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
   
       if (loadResource != null) {
   
           // Determine if the loaded asset is read only.
           Session session = slingRequest.getResourceResolver().adaptTo(Session.class);
           try {
               session.checkPermission(loadResource.getPath(), "set_property");
               readOnly = false;
           }
           catch (AccessControlException ace) {
               // checkPermission throws exception if asset is read only
               readOnly = true;
           }
           catch (RepositoryException re) {}
   
           // Get the value of the metadata.
           Asset asset = loadResource.adaptTo(Asset.class);
           try {
               value = asset.getMetadata(name).toString();
           }
           catch (NullPointerException npe) {
               // no metadata dc:description available
           }
       }
   %>
   <div class="form_row">
       <div class="form_leftcol">
           <div class="form_leftcollabel">Sample Metadata</div>
       </div>
       <div class="form_rightcol">
           <%
           if (readOnly) {
               %><c:out value="<%= value %>"/><%
           }
           else {
               %><input class="text" type="text" name="./jcr:content/metadata/<%= name %>" value="<c:out value="<%= value %>" />"><%
           }%>
       </div>
   </div>
   ```

1. Para disponibilizar o componente, é necessário editá-lo. Para tornar um componente editável, no CRXDE Lite, adicione um nó `cq:editConfig` do tipo primário `cq:EditConfig`. Para que possa remover parágrafos, adicione uma propriedade de vários valores `cq:actions` com um único valor `DELETE`.

1. Navegue até o navegador e, na página de exemplo (por exemplo, `asseteditor.html`) alternar para o modo de design e ativar o novo componente para o sistema de parágrafos.

1. No modo **Editar**, o novo componente (por exemplo, **Metadados de amostra**) agora está disponível no sidekick (encontrado no grupo **Editor de ativos**). Insira o componente. Para poder armazenar os metadados, eles devem ser adicionados ao formulário de metadados.

## Modificar opções de metadados {#modifying-metadata-options}

Você pode modificar os namespaces disponíveis na [formulário de metadados](assets-finder-editor.md#metadata-form-and-text-field-configuring-the-view-metadata-component).

Os metadados disponíveis no momento estão definidos em `/libs/dam/options/metadata`:

* O primeiro nível dentro desse diretório contém os namespaces.
* Os itens dentro de cada namespace representam metadados, como resultados em um item de parte local.
* O conteúdo dos metadados contém as informações para o tipo e as opções de vários valores.

As opções podem ser substituídas em `/apps/dam/options/metadata`:

1. Copiar o diretório de `/libs` para `/apps`.

1. Remover, modificar ou adicionar itens.

>[!NOTE]
>
>Se você adicionar novos namespaces, eles deverão ser registrados no repositório/CRX. Caso contrário, o envio do formulário de metadados resultará em um erro.
