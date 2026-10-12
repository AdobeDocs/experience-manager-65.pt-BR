---
title: Configurar restrições de upload de ativos
description: Restringir os tipos de ativos (arquivos) que os usuários podem fazer upload
contentOwner: AG
role: Developer, Admin
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: cda65036-5305-4f01-89da-9b3506ae8c50
    internal-label: Administration
subfeature_v2:
  - id: f1dc0c96-022d-4003-afbe-47bd40173c4a
    internal-label: Upload assets
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 7%
---
# Configurar restrições de upload de ativos {#configuring-asset-upload-restrictions}

Você pode configurar o [!DNL Adobe Experience Manager Assets] para restringir os tipos de ativos que os usuários podem carregar. Ele ajuda a impedir uploads acidentais de formato indesejado e arquivos mal-intencionados. O serviço `Day CQ DAM Asset Upload Restriction` permite que você controle o tipo de arquivo que os usuários podem carregar. Por padrão, o [!DNL Assets] permite que usuários carreguem ativos de todos os tipos MIME. No entanto, você pode configurar o serviço para impedir que os usuários façam upload de arquivos apenas de tipos MIME específicos.

1. Abra o console da Web do Configuration Manager. Acessar `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra o serviço **[!UICONTROL Restrição de carregamento de ativos DAM CQ do]** no modo de Edição. Por padrão, a opção **Permitir todos os MIME** está selecionada, o que permite que os usuários carreguem arquivos de todos os tipos MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Para impedir que usuários façam upload de arquivos apenas de determinados tipos MIME, desmarque a opção **[!UICONTROL Permitir todos os tipos MIME]** e especifique os tipos MIME permitidos nos campos **[!UICONTROL MIMEs de ativos permitidos (regex)]** usando expressões regulares.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações. Se você especificar cadeias de caracteres MIME para os tipos MIME permitidos, a operação de upload falhará todos os ativos de tipo MIME que não correspondam às cadeias de caracteres MIME configuradas nesses campos.
