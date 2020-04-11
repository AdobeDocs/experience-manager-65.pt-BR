---
title: Atualização do link para a documentação
seo-title: Atualização do link para a documentação
description: Como atualizar o destino do link Ajuda do Workspace na área de trabalho do AEM Forms para apontar para o link personalizado da documentação.
seo-description: Como atualizar o destino do link Ajuda do Workspace na área de trabalho do AEM Forms para apontar para o link personalizado da documentação.
uuid: 64056d10-1451-44ed-8f25-81a21037dc75
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 788c427f-190f-4580-9efd-6a4c4a008837
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Atualização do link para a documentação {#updating-the-link-to-the-documentation}

Você pode acessar o conteúdo de ajuda padrão da área de trabalho do AEM Forms selecionando **Ajuda > Ajuda** da Workspace. Ele aponta para a documentação on-line no site da Adobe. No entanto, você pode atualizá-lo para apontar para qualquer outro URL.

Considere os seguintes casos de uso nos quais você pode querer alterar o URL de ajuda padrão:

* Para fornecer ajuda localizada em um idioma de sua escolha.
* Para fornecer conteúdo de ajuda personalizado para sua área de trabalho personalizada.

Para atualizar o URL da documentação on-line, siga as etapas [genéricas de personalização](/help/forms/using/generic-steps-html-workspace-customization.md) e, em seguida, siga as etapas a seguir.

1. Copie o `userinfo.html` arquivo de `/libs/ws/js/runtime/templates` para `/apps/ws/js/runtime/templates`.
1. Alterar:

   ```
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   para

   ```
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. Faça o seguinte:

   1. Abra /apps/ws/js/registry.js para edição.
   1. Pesquise e substitua `text!/lc/libs/ws/js/runtime/templates/userinfo.html` por `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.
