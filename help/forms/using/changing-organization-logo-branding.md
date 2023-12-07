---
title: Alteração do logotipo da organização para identidade visual
description: Para marcar a AEM Forms, forneça o logotipo da sua organização personalizando o logotipo padrão.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Alteração do logotipo da organização para identidade visual {#changing-the-organization-logo-for-branding}

O logotipo da organização é exibido no canto superior esquerdo do espaço de trabalho do AEM Forms. Para atualizar o logotipo, siga as instruções [Etapas genéricas de personalização do espaço de trabalho do AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) e depois as etapas a seguir.

1. Crie um logotipo e nomeie o arquivo como `NewWorkspace.png`. Coloque o arquivo de imagem na pasta /apps/ws/images usando um cliente WebDAV.

   >[!NOTE]
   >
   >O tamanho recomendado da imagem do logotipo é 218 px × 20 px.

   >[!NOTE]
   >
   >Para obter mais informações sobre o acesso WebDAV, consulte [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=pt-BR).

1. Referencie a nova imagem de logotipo na folha de estilos em /apps/ws/css/newStyle.css, adicionando o estilo a seguir.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
