---
title: Hospedagem de duas instâncias do espaço de trabalho do AEM Forms em um servidor
seo-title: Hosting two AEM Forms workspace instances on one server
description: Como os administradores de LC podem personalizar o HTML WS para hospedar duas instâncias em um único servidor acessível por URLs diferentes.
seo-description: How LC administrators can customize HTML WS to host two instances on a single server accessible via different URLs.
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Hospedagem de duas instâncias do espaço de trabalho do AEM Forms em um servidor {#hosting-two-aem-forms-workspace-instances-on-one-server}

A instalação e as configurações padrão do AEM Forms permitem que apenas um espaço de trabalho do AEM Forms esteja disponível no servidor. No entanto, talvez seja necessário hospedar duas instâncias diferentes do espaço de trabalho do AEM Forms em um único servidor do AEM Forms. As duas instâncias podem ser acessadas por URLs diferentes.

Os administradores do AEM Forms personalizam o espaço de trabalho para criar dois URLs diferentes e disponibilizar dois espaços de trabalho no mesmo servidor. Neste artigo de personalização, pressupomos que os dois espaços de trabalho estejam acessíveis em `https://'[server]:[port]'/lc/ws` e `https://'[server]:[port]':/lc/ws2`.

Siga estas etapas para configurar o espaço de trabalho do AEM Forms.

1. Instale o pacote dev do espaço de trabalho do AEM Forms em seu servidor. Consulte [pacote dev](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p), para obter instruções sobre como criá-lo.
1. Faça login no CRXDE Lite como administrador, acessando `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Copie o nó ws em /content e cole em /content. Renomeie o nó para ws2. Clique em **[!UICONTROL Salvar tudo]**. Nas propriedades deste nó, altere o valor de `sling:resourceType` para ws2. Clique em **[!UICONTROL Salvar tudo]**.

1. Copie a pasta ws de /libs e cole em /apps. Renomeie a pasta para ws2. Clique em **[!UICONTROL Salvar tudo]**.
1. Entrada `GET.jsp` em `/apps/ws2`, faça as seguintes alterações de código. Substitua o seguinte

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" /><html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" />
   ```

   com o seguinte código

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. Entrada `registry.js` em `/apps/ws2/js`, alterar o caminho dos modelos para consultar os modelos em `/apps/ws2/js/runtime/templates`. Substitua o código a seguir

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/libs/ws/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

   com o seguinte código

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/apps/ws2/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

1. Entrada `userinfo.js` em `/apps/ws2/js/runtime/models` e `/apps/ws2/js/runtime/views`, alterar sequência de caracteres `/lc/content/ws` para `lc/content/ws2`.

1. Entrada `/apps/ws2/js/runtime/services/service.js`, alterar o caminho em `getLocalizationData` função para apontar para `/lc/apps/ws2/Locale.html`.

1. Para consultar `pdf.html` do novo Espaço de trabalho, altere o caminho de `pdf.html` in `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. Para consultar `pdf.html` do novo Espaço de trabalho, alterar caminhos de `pdf.html` e `WsNextAdapter.swf` in `startprocess.html`, `taskdetails.html`, e `processinstancehistory.html` em `/apps/ws2/js/runtime/templates`.

1. Copiar `/etc/map/ws` pasta e colar em `/etc/map`. Renomeie a nova pasta para ws2. Clique em Salvar tudo.

1. Nas propriedades de `ws2`, alterar valor de `sling:redirect` para `content/ws2`.

1. Alterar valor de `sling:match` para `^[^/\||]/[^/\||]/ws2$`.
