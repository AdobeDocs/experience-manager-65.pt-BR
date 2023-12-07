---
title: Atualização do link para a documentação
description: Como atualizar o destino do link de Ajuda do Espaço de trabalho no espaço de trabalho do AEM Forms para apontar para o link de documentação personalizado.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: ca637bea-05c1-4920-9283-e782f07607de
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 2%

---

# Atualização do link para a documentação {#updating-the-link-to-the-documentation}

Você pode acessar o conteúdo de ajuda padrão do espaço de trabalho do AEM Forms selecionando **Ajuda > Ajuda do Workspace**. Ele aponta para a documentação online no site do Adobe. No entanto, você pode atualizá-lo para apontar para qualquer outro URL.

Considere os seguintes casos de uso em que talvez você queira alterar o URL de ajuda padrão:

* Por fornecer ajuda localizada em um idioma de sua escolha.
* Para fornecer conteúdo de ajuda personalizado para o seu espaço de trabalho personalizado.

Para atualizar o URL da documentação online, siga o [Etapas genéricas de personalização](/help/forms/using/generic-steps-html-workspace-customization.md) e depois as etapas a seguir.

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
