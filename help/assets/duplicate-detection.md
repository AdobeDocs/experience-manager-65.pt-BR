---
title: Ativar a detecção de ativos de duplicado
description: Saiba como ativar a detecção de ativos de duplicado no Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---


# Ativar a detecção de ativos de duplicado {#enable-detection-of-duplicate-assets}

Se você tentar carregar um ativo que existe em [!DNL Adobe Experience Manager Assets], o recurso de detecção de duplicados o identificará como duplicado. A detecção de duplicados está desativada por padrão. Para ativar o recurso, execute as seguintes etapas:

1. Abra a página [!DNL Experience Manager] de configuração do Web Console acessando `https://[aem_server]:[port]/system/console/configMgr`.
1. Edite a configuração do servlet **[!UICONTROL Dia CQ DAM Criar Ativo]**.
1. Selecione a opção **[!UICONTROL detectar duplicado]** e clique em **[!UICONTROL Salvar]**.

   ![Selecione a opção detectar duplicado no servlet](assets/chlimage_1-377.png)

   *Figura: Selecione a opção detectar duplicado no servlet.*

O recurso de detecção de duplicado agora está ativado em [!DNL Assets]. Quando um usuário tenta carregar um ativo que existe em [!DNL Experience Manager], o sistema verifica se há conflito e indica-o. Os ativos são identificados usando o hash SHA-1 armazenado em `jcr:content/metadata/dam:sha1`, o que significa que os ativos do duplicado são detectados independentemente dos nomes dos arquivos.

>[!MORELIKETHIS]
>
>* [Ativos do duplicado no repositório existente (um tutorial de um membro da comunidade)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

