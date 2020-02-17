---
title: Configurar restrições de upload de ativos
description: 'Restringir o tipo de ativos (arquivos) que os usuários podem carregar '
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Configurar restrições de upload de ativos {#configuring-asset-upload-restrictions}

Você pode configurar os ativos Adobe Experience Manager (AEM) para restringir o tipo de ativos (arquivos) que os usuários podem carregar. Este recurso ajuda a eliminar a possibilidade de os usuários carregarem ativos em um formato indesejado ou carregarem arquivos mal-intencionados. O `Day CQ DAM Asset Upload Restriction` serviço permite controlar o tipo de arquivos que os usuários podem carregar. Por padrão, o AEM Assets permite que os usuários carreguem ativos de todos os tipos MIME. No entanto, você pode configurar o serviço para restringir usuários a carregarem somente arquivos de tipos MIME específicos.

1. Abra o console da Web do Configuration Manager. Acesso `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra o serviço **[!UICONTROL Dia CQ DAM Asset Upload Restriction (Restrição]** de upload de ativo do CQ DAM) no modo de edição. Por padrão, a opção **Permitir todos os MIME** está selecionada, permitindo que os usuários carreguem arquivos de todos os tipos MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Para restringir usuários a carregarem arquivos de determinados tipos MIME apenas, desmarque a opção **[!UICONTROL Permitir todos os MIME]** e especifique os tipos MIME permitidos nos campos MIMEs de ativos **[!UICONTROL permitidos (regex)]** usando expressões regulares.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Clique/toque em **[!UICONTROL Salvar]** para salvar as alterações. Se você especificar sequências de caracteres MIME para tipos MIME permitidos, a operação de upload falhará para qualquer ativo com tipo MIME que não corresponda às sequências de caracteres MIME configuradas nesses campos.
