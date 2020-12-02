---
title: Criação de um Cloud Service personalizado
seo-title: Criação de um Cloud Service personalizado
description: O conjunto padrão de Cloud Services pode ser estendido com tipos de Cloud Service personalizados
seo-description: O conjunto padrão de Cloud Services pode ser estendido com tipos de Cloud Service personalizados
uuid: b105a0c1-b68c-4f57-8e3b-561c8051a08e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e48e87c6-43ca-45ba-bd6b-d74c969757cd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 11%

---


# Criação de um Cloud Service personalizado{#creating-a-custom-cloud-service}

O conjunto padrão de Cloud Services pode ser estendido com tipos de Cloud Service personalizados. Isso permite que você insira a marcação personalizada na página de forma estruturada. Isso será usado principalmente para provedores de análises de terceiros, por exemplo, Google Analytics, Chartbeat etc. Cloud Services são herdados de páginas pai para páginas secundárias com a capacidade de quebrar a herança em qualquer nível.

>[!NOTE]
>
>Este guia passo a passo para a criação de um novo Cloud Service é um exemplo usando Google Analytics. Tudo pode não se aplicar ao seu caso de uso.

1. No CRXDE Lite, crie um novo nó em `/apps`:

   * **Nome**: `acs`
   * **Tipo**: `nt:folder`

1. Crie um novo nó em `/apps/acs`:

   * **Nome**: `analytics`
   * **Tipo**: `sling:Folder`

1. Crie 2 novos nós em `/apps/acs/analytics`:

   * **Nome**: componentes
   * **Tipo**: `sling:Folder`

   e

   * **Nome**: modelos
   * **Tipo**: `sling:Folder`


1. Clique com o botão direito do mouse em `/apps/acs/analytics/components`. Selecione **Criar...** seguido por **Criar componente...** A caixa de diálogo que é aberta permite especificar:

   * **Rótulo**:  `googleanalyticspage`
   * **Título**: `Google Analytics Page`
   * **Super Type**: `cq/cloudserviceconfigs/components/configpage`
   * **Grupo**: `.hidden`

1. Clique duas vezes em **Próximo** e especifique:

   * **Primários permitidos:** `acs/analytics/templates/googleanalytics`

   Clique duas vezes em **Avançar** e clique em **OK**.

1. Adicione uma propriedade a `googleanalyticspage`:

   * **Nome:** `cq:defaultView`
   * **Valor:** `html`

1. Crie um novo arquivo chamado `content.jsp` em `/apps/acs/analytics/components/googleanalyticspage`, com o seguinte conteúdo:

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

1. Crie um novo nó em `/apps/acs/analytics/components/googleanalyticspage/`:

   * **Nome**: `dialog`
   * **Tipo**: `cq:Dialog`
   * **Propriedades**:

      * **Nome**: `title`
      * **Tipo**: `String`
      * **Valor**:  `Google Analytics Config`
      * **Nome**: `xtype`
      * **Tipo**: `String`
      * **Valor**:  `dialog`

1. Crie um novo nó em `/apps/acs/analytics/components/googleanalyticspage/dialog`:

   * **Nome**: `items`
   * **Tipo**: `cq:Widget`
   * **Propriedades**:

      * **Nome**: `xtype`
      * **Tipo**: `String`
      * **Valor**:  `tabpanel`

1. Crie um novo nó em `/apps/acs/analytics/components/googleanalyticspage/dialog/items`:

   * **Nome**: `items`
   * **Tipo**: `cq:WidgetCollection`

1. Crie um novo nó em `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items`:

   * **Nome**: tab1
   * **Tipo**: `cq:Panel`
   * **Propriedades**:

      * **Nome**: `title`
      * **Tipo**: `String`
      * **Valor**:  `Config`

1. Crie um novo nó em `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1`:

   * **Nome**: items
   * **Tipo**: `nt:unstructured`
   * **Propriedades**:

      * **Nome**: `fieldLabel`
      * **Tipo**: String
      * **Valor**: ID da conta

      * **Nome**: `fieldDescription`
      * **Tipo**: `String`
      * **Valor**:  `The account ID assigned by Google. Usually in the form UA-NNNNNN-N`

      * **Nome**: `name`
      * **Tipo**: `String`
      * **Valor**:  `./accountID`
      * **Nome**: `validateOnBlur`
      * **Tipo**: `String`
      * **Valor**:  `true`
      * **Nome**: `xtype`
      * **Tipo**: `String`
      * **Valor**:  `textfield`

1. Copie `/libs/cq/cloudserviceconfigs/components/configpage/body.jsp` para `/apps/acs/analytics/components/googleanalyticspage/body.jsp` e altere `libs` para `apps` na linha 34 e faça da referência de script na linha 79 um caminho totalmente qualificado.
1. Crie um novo modelo em `/apps/acs/analytics/templates/`:

   * com **Tipo de Recurso** = `acs/analytics/components/googleanalyticspage`
   * com **Etiqueta** = `googleanalytics`
   * com **Título**= `Google Analytics Configuration`
   * com **allowPath** = `/etc/cloudservices/googleanalytics(/.*)?`
   * com **authorizedChildren** = `/apps/acs/analytics/templates/googleanalytics`
   * com **sling:resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage` (no nó do modelo, não no nó jcr:content)
   * com **cq:designPath** = `/etc/designs/cloudservices/googleanalytics` (em jcr:content)

1. Criar novo componente: `/apps/acs/analytics/components/googleanalytics`.

   Adicione o seguinte conteúdo a `googleanalytics.jsp`:

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

   Isso deve produzir a marcação personalizada com base nas propriedades de configuração.

1. Navegue até `http://localhost:4502/miscadmin#/etc/cloudservices` e crie uma nova página:

   * **Título**: `Google Analytics`
   * **Nome**: `googleanalytics`

   Volte ao CRXDE Lite e, em `/etc/cloudservices/googleanalytics`, adicione a seguinte propriedade a `jcr:content`:

   * **Nome**: `componentReference`
   * **Tipo**: `String`
   * **Valor**:  `acs/analytics/components/googleanalytics`


1. Navegue até a página Serviço recém-criada ( `http://localhost:4502/etc/cloudservices/googleanalytics.html`) e clique em **+** para criar uma nova configuração:

   * **Configuração primária**: `/etc/cloudservices/googleanalytics`
   * **Título:**  `My First GA Config`

   Escolha **Configuração de Google Analytics** e clique em **Criar**.

1. Insira uma **ID da conta**, por exemplo `AA-11111111-1`. Clique em **OK**.
1. Navegue até uma página e adicione a configuração recém-criada nas propriedades da página, na guia **Cloud Services**.
1. A página terá a marcação personalizada adicionada.

