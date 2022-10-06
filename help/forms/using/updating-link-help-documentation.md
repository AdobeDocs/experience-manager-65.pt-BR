---
title: Atualização do link para a documentação
seo-title: Updating the link to the documentation
description: Como atualizar o destino do link Ajuda do Workspace no espaço de trabalho do AEM Forms para apontar para o link de documentação personalizado.
seo-description: How-to update the destination of Workspace Help link in AEM Forms workspace to point to your custom documentation link.
uuid: 64056d10-1451-44ed-8f25-81a21037dc75
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 788c427f-190f-4580-9efd-6a4c4a008837
exl-id: ca637bea-05c1-4920-9283-e782f07607de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 3%

---

# Atualização do link para a documentação {#updating-the-link-to-the-documentation}

Você pode acessar o conteúdo de ajuda padrão do espaço de trabalho do AEM Forms selecionando **Ajuda > Ajuda do Workspace**. Ele aponta para a documentação online no site do Adobe. No entanto, você pode atualizá-lo para apontar para qualquer outro URL.

Considere os seguintes casos de uso em que você pode querer alterar o URL de ajuda padrão:

* Para fornecer ajuda localizada em um idioma de sua escolha.
* Para fornecer conteúdo de ajuda personalizado para seu espaço de trabalho personalizado.

Para atualizar o URL da documentação online, siga as [Etapas genéricas da personalização](/help/forms/using/generic-steps-html-workspace-customization.md) e, em seguida, execute as etapas a seguir.

1. Copie o `userinfo.html` arquivo de `/libs/ws/js/runtime/templates` para `/apps/ws/js/runtime/templates`.
1. Alterar:

   ```html
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   para

   ```html
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. Faça o seguinte:

   1. Abra /apps/ws/js/registry.js para edição.
   1. Pesquisar e substituir `text!/lc/libs/ws/js/runtime/templates/userinfo.html` com `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.
