---
title: Hospedagem de duas instâncias de espaço de trabalho de AEM Forms em um servidor
seo-title: Hospedagem de duas instâncias de espaço de trabalho de AEM Forms em um servidor
description: Como os administradores LC podem personalizar o HTML WS para hospedar duas instâncias em um único servidor acessível por meio de URLs diferentes.
seo-description: Como os administradores LC podem personalizar o HTML WS para hospedar duas instâncias em um único servidor acessível por meio de URLs diferentes.
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---


# Hospedagem de duas instâncias de espaço de trabalho de AEM Forms em um servidor {#hosting-two-aem-forms-workspace-instances-on-one-server}

A instalação e as configurações padrão do AEM Forms permitem que apenas um espaço de trabalho de AEM Forms esteja disponível no servidor. No entanto, pode ser necessário hospedar duas instâncias diferentes de espaço de trabalho do AEM Forms em um único servidor de AEM Forms. As duas instâncias são acessíveis por URLs diferentes.

Os administradores do AEM Forms personalizam o espaço de trabalho para criar dois URLs diferentes e disponibilizar dois espaços de trabalho no mesmo servidor. Neste artigo de personalização, supomos que os dois espaços de trabalho estejam acessíveis em `https://'[server]:[port]'/lc/ws` e `https://'[server]:[port]':/lc/ws2`.

Siga estas etapas para configurar a área de trabalho do AEM Forms.

1. Instale o pacote dev do espaço de trabalho do AEM Forms no seu servidor. Consulte o pacote [](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)dev para obter instruções sobre como criá-lo.
1. Faça logon no CRXDE Lite como administrador, acessando `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Copie o nó em /content e cole em /content. Renomeie o nó como ws2. Clique em **[!UICONTROL Salvar tudo]**. Nas propriedades desse nó, altere o valor de `sling:resourceType` para ws2. Clique em **[!UICONTROL Salvar tudo]**.

1. Copie a pasta de /libs e cole em /apps. Renomeie a pasta para ws2. Clique em **[!UICONTROL Salvar tudo]**.
1. Em `GET.jsp` at, `/apps/ws2`faça as seguintes alterações de código. Substitua o seguinte

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

1. Em `registry.js` at, altere o caminho dos modelos para fazer referência aos modelos em `/apps/ws2/js``/apps/ws2/js/runtime/templates`. Substitua o seguinte código

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

1. Em `userinfo.js` at `/apps/ws2/js/runtime/models` and `/apps/ws2/js/runtime/views`, altere string `/lc/content/ws` para `lc/content/ws2`.

1. Em `/apps/ws2/js/runtime/services/service.js`, altere o caminho na `getLocalizationData` função para apontar para `/lc/apps/ws2/Locale.html`.

1. Para fazer referência ao novo Espaço `pdf.html` de trabalho, altere o caminho de `pdf.html` entrada `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. Para fazer referência ao `pdf.html` novo Espaço de trabalho, altere os caminhos de `pdf.html` e `WsNextAdapter.swf` dentro `startprocess.html`, `taskdetails.html`e `processinstancehistory.html` em `/apps/ws2/js/runtime/templates`.

1. Copie a `/etc/map/ws` pasta e cole em `/etc/map`. Renomeie a nova pasta para ws2. Clique em Salvar tudo.

1. Nas propriedades de `ws2`, altere o valor de `sling:redirect` para `content/ws2`.

1. Altere o valor de `sling:match` para `^[^/\||]/[^/\||]/ws2$`.
