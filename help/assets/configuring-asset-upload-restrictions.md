---
title: Configurar restrições de upload de ativos
description: Restringir os tipos de ativos (arquivos) que os usuários podem fazer upload
contentOwner: AG
role: Developer, Admin, Architect
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 18%

---

# Configurar restrições de upload de ativos {#configuring-asset-upload-restrictions}

Você pode configurar [!DNL Adobe Experience Manager Assets] para restringir os tipos de ativos que os usuários podem fazer upload. Ele ajuda a impedir uploads acidentais de formato indesejado e arquivos mal-intencionados. A variável `Day CQ DAM Asset Upload Restriction` serviço permite controlar os tipos de arquivos que os usuários podem fazer upload. Por padrão, [!DNL Assets] permite que os usuários façam upload de ativos de todos os tipos MIME. No entanto, você pode configurar o serviço para impedir que os usuários façam upload de arquivos apenas de tipos MIME específicos.

1. Abra o console da Web do Configuration Manager. Access `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra o **[!UICONTROL Restrição de carregamento de ativos DAM do Day CQ]** serviço no modo de Edição. Por padrão, a variável **Permitir todos os MIME** for selecionada, permitindo que os usuários façam upload de arquivos de todos os tipos MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Para impedir que usuários façam upload de arquivos apenas de determinados tipos MIME, desmarque a opção **[!UICONTROL Permitir todos os MIME]** e especifique os tipos MIME permitidos na variável **[!UICONTROL MIMEs de ativos permitidos (regex)]** campos que usam expressões regulares.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações. Se você especificar cadeias de caracteres MIME para os tipos MIME permitidos, a operação de upload falhará todos os ativos de tipo MIME que não correspondam às cadeias de caracteres MIME configuradas nesses campos.
