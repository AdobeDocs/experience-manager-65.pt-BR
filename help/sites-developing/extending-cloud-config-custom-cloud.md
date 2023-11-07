---
title: Criação de um Cloud Service personalizado
description: O conjunto padrão de Cloud Services pode ser estendido com tipos de Cloud Service personalizados
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 9414c77a-b180-4440-8386-e6eb4426e475
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 15%

---

# Criação de um Cloud Service personalizado{#creating-a-custom-cloud-service}

O conjunto padrão de Cloud Services pode ser estendido com tipos de Cloud Service personalizados. Isso permite inserir marcação personalizada na página de forma estruturada. Isso é usado principalmente para provedores de análises de terceiros, por exemplo, Google Analytics, Chartbeat e assim por diante. Os Cloud Service são herdados das páginas principais para as páginas secundárias com a capacidade de interromper a herança em qualquer nível.

>[!NOTE]
>
>Este guia passo a passo para criar um Cloud Service é um exemplo usando Google Analytics. Tudo pode não se aplicar ao seu caso de uso.

1. No CRXDE Lite, crie um nó em `/apps`:

   * **Nome**: `acs`
   * **Tipo**: `nt:folder`

1. Criar um nó em `/apps/acs`:

   * **Nome**: `analytics`
   * **Tipo**: `sling:Folder`

1. Criar dois nós em `/apps/acs/analytics`:

   * **Nome**: componentes
   * **Tipo**: `sling:Folder`

   e

   * **Nome**: templates
   * **Tipo**: `sling:Folder`

1. Clique com o botão direito do mouse em `/apps/acs/analytics/components`. Selecionar **Criar...** seguido por **Criar componente...** A caixa de diálogo que é aberta permite especificar:

   * **Rótulo**: `googleanalyticspage`
   * **Título**: `Google Analytics Page`
   * **Super Type**: `cq/cloudserviceconfigs/components/configpage`
   * **Grupo**: `.hidden`

1. Clique em **Próxima** duas vezes e especificar:

   * **Primários permitidos:** `acs/analytics/templates/googleanalytics`

   Clique em **Próxima** duas vezes e clique **OK**.

1. Adicionar uma propriedade ao `googleanalyticspage`:

   * **Nome:** `cq:defaultView`
   * **Valor:** `html`

1. Crie um arquivo chamado `content.jsp` em `/apps/acs/analytics/components/googleanalyticspage`, com o seguinte conteúdo:

   ```xml
   <%@page contentType="text/html"
               pageEncoding="utf-8"%><%
   %><%@include file="/libs/foundation/global.jsp"%><div>
   
   <div>
       <h3>Google Analytics Settings</h3>
       <ul>
           <li><div class="li-bullet"><strong>accountID: </strong><br><%= xssAPI.encodeForHTML(properties.get("accountID", "")) %></div></li>
       </ul>
   </div>
   ```

1. Criar um nó em `/apps/acs/analytics/components/googleanalyticspage/`:

   * **Nome**: `dialog`
   * **Tipo**: `cq:Dialog`
   * **Propriedades**:

      * **Nome**: `title`
      * **Tipo**: `String`
      * **Valor**: `Google Analytics Config`
      * **Nome**: `xtype`
      * **Tipo**: `String`
      * **Valor**: `dialog`

1. Criar um nó em `/apps/acs/analytics/components/googleanalyticspage/dialog`:

   * **Nome**: `items`
   * **Tipo**: `cq:Widget`
   * **Propriedades**:

      * **Nome**: `xtype`
      * **Tipo**: `String`
      * **Valor**: `tabpanel`

1. Criar um nó em `/apps/acs/analytics/components/googleanalyticspage/dialog/items`:

   * **Nome**: `items`
   * **Tipo**: `cq:WidgetCollection`

1. Criar um nó em `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items`:

   * **Nome**: tab1
   * **Tipo**: `cq:Panel`
   * **Propriedades**:

      * **Nome**: `title`
      * **Tipo**: `String`
      * **Valor**: `Config`

1. Criar um nó em `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1`:

   * **Nome**: itens
   * **Tipo**: `nt:unstructured`
   * **Propriedades**:

      * **Nome**: `fieldLabel`
      * **Tipo**: String
      * **Valor**: ID da conta

      * **Nome**: `fieldDescription`
      * **Tipo**: `String`
      * **Valor**: `The account ID assigned by Google. Usually in the form UA-NNNNNN-N`

      * **Nome**: `name`
      * **Tipo**: `String`
      * **Valor**: `./accountID`
      * **Nome**: `validateOnBlur`
      * **Tipo**: `String`
      * **Valor**: `true`
      * **Nome**: `xtype`
      * **Tipo**: `String`
      * **Valor**: `textfield`

1. Copiar `/libs/cq/cloudserviceconfigs/components/configpage/body.jsp` para `/apps/acs/analytics/components/googleanalyticspage/body.jsp` e alterar `libs` para `apps` na linha 34 e faça da referência do script na linha 79 um caminho totalmente qualificado.
1. Criar um modelo em `/apps/acs/analytics/templates/`:

   * com **Tipo de recurso** = `acs/analytics/components/googleanalyticspage`
   * com **Rótulo** = `googleanalytics`
   * com **Título**= `Google Analytics Configuration`
   * com **allowedPath** = `/etc/cloudservices/googleanalytics(/.*)?`
   * com **allowedChildren** = `/apps/acs/analytics/templates/googleanalytics`
   * com **sling:resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage` (no nó do modelo, não no nó jcr:content)
   * com **cq:designPath** = `/etc/designs/cloudservices/googleanalytics` (em jcr:content)

1. Criar um componente: `/apps/acs/analytics/components/googleanalytics`.

   Adicionar o seguinte conteúdo a `googleanalytics.jsp`:

   ```xml
   <%@page import="org.apache.sling.api.resource.Resource,
                   org.apache.sling.api.resource.ValueMap,
                   org.apache.sling.api.resource.ResourceUtil,
                   com.day.cq.wcm.webservicesupport.Configuration,
                   com.day.cq.wcm.webservicesupport.ConfigurationManager" %>
   <%@include file="/libs/foundation/global.jsp" %><%
   
   String[] services = pageProperties.getInherited("cq:cloudserviceconfigs", new String[]{});
   ConfigurationManager cfgMgr = resource.getResourceResolver().adaptTo(ConfigurationManager.class);
   if(cfgMgr != null) {
       String accountID = null;
       Configuration cfg = cfgMgr.getConfiguration("googleanalytics", services);
       if(cfg != null) {
           accountID = cfg.get("accountID", null);
       }
   
       if(accountID != null) {
       %>
   <script type="text/javascript">
   
     var _gaq = _gaq || [];
     _gaq.push(['_setAccount', '<%= accountID %>']);
     _gaq.push(['_trackPageview']);
   
     (function() {
       var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
       ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
       var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
     })();
   
   </script><%
       }
   }
   %>
   ```

   Isso deve gerar a marcação personalizada com base nas propriedades de configuração.

1. Navegue até `http://localhost:4502/miscadmin#/etc/cloudservices` e crie uma página:

   * **Título**: `Google Analytics`
   * **Nome**: `googleanalytics`

   Voltar ao CRXDE Lite e abaixo de `/etc/cloudservices/googleanalytics`, adicione a seguinte propriedade a `jcr:content`:

   * **Nome**: `componentReference`
   * **Tipo**: `String`
   * **Valor**: `acs/analytics/components/googleanalytics`

1. Navegue até a página Serviço recém-criada ( `http://localhost:4502/etc/cloudservices/googleanalytics.html`) e clique no link **+** para criar uma configuração:

   * **Configuração primária**: `/etc/cloudservices/googleanalytics`
   * **Título:**  `My First GA Config`

   Escolher **Configuração do Google Analytics** e clique em **Criar**.

1. Insira um **ID da conta**, por exemplo, `AA-11111111-1`. Clique em **OK**.
1. Navegue até uma página e adicione a configuração recém-criada nas propriedades da página, na seção **Cloud Service** guia.
1. A página terá a marcação personalizada adicionada a ela.
