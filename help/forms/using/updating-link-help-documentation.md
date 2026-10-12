---
title: Atualização do link para a documentação
description: Como atualizar o destino do link de Ajuda do Workspace no espaço de trabalho do AEM Forms para apontar para o link de documentação personalizado.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: ca637bea-05c1-4920-9283-e782f07607de
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 2%
---
# Atualização do link para a documentação {#updating-the-link-to-the-documentation}

Você pode acessar o conteúdo de ajuda padrão do espaço de trabalho do AEM Forms selecionando **Ajuda > Ajuda do Workspace**. Ele aponta para a documentação online no site da Adobe. No entanto, você pode atualizá-lo para apontar para qualquer outro URL.

Considere os seguintes casos de uso em que talvez você queira alterar o URL de ajuda padrão:

* Por fornecer ajuda localizada em um idioma de sua escolha.
* Para fornecer conteúdo de ajuda personalizado para o seu espaço de trabalho personalizado.

Para atualizar a URL da documentação online, siga as [Etapas genéricas de personalização](/help/forms/using/generic-steps-html-workspace-customization.md) e as seguintes etapas.

1. Copie o arquivo `userinfo.html` de `/libs/ws/js/runtime/templates` para `/apps/ws/js/runtime/templates`.
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
   1. Pesquisar e substituir `text!/lc/libs/ws/js/runtime/templates/userinfo.html` por `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.
