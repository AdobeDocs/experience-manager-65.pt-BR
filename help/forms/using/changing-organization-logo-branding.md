---
title: Alteração do logotipo da organização para marcas
seo-title: Alteração do logotipo da organização para marcas
description: Para criar uma marca no espaço de trabalho do AEM Forms, forneça o logotipo de sua organização, personalizando o logotipo padrão.
seo-description: Para criar uma marca no espaço de trabalho do AEM Forms, forneça o logotipo de sua organização, personalizando o logotipo padrão.
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Alteração do logotipo da organização para marcas {#changing-the-organization-logo-for-branding}

O logotipo da organização é exibido no canto superior esquerdo da área de trabalho do AEM Forms. Para atualizar o logotipo, siga as etapas [Genéricas da personalização](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) da área de trabalho do AEM Forms e siga as seguintes etapas.

1. Crie um logotipo e nomeie o arquivo como `NewWorkspace.png`. Coloque o arquivo de imagem na pasta /apps/ws/images usando um cliente WebDAV.

   >[!NOTE]
   >
   >O tamanho recomendado para a imagem do logotipo é de 218 px × 20 px.

   >[!NOTE]
   >
   >Para obter mais informações sobre o acesso ao WebDAV, consulte [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

1. Consulte a nova imagem de logotipo na folha de estilos em /apps/ws/css/newStyle.css, adicionando o seguinte estilo.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```

[Contate o suporte](https://www.adobe.com/account/sign-in.supportportal.html)
