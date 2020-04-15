---
title: Ativar a detecção de ativos de duplicado
description: Saiba como ativar a detecção de ativos de duplicado no AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# Ativar a detecção de ativos de duplicado {#enable-detection-of-duplicate-assets}

Se você tentar carregar um ativo que existe nos ativos Adobe Experience Manager (AEM), o recurso de detecção de duplicados o identificará como duplicado. A detecção de Duplicados está desativada por padrão. Para ativar o recurso, execute as seguintes etapas:

1. Abra a página Configuração do console da Web do AEM acessando `https://[aem_server]:[port]/system/console/configMgr`.
1. Edite a configuração para o **[!UICONTROL Dia do servlet CQ DAM Criar ativo]**.
1. Selecione a opção **[!UICONTROL detectar duplicado]** e clique em **[!UICONTROL Salvar]**.

   ![Selecione a opção detectar duplicado no servlet](assets/chlimage_1-377.png)

   *Figura: Selecione a opção detectar duplicado no servlet*

O recurso de detecção de duplicado agora está ativado nos ativos AEM. Quando um usuário tenta carregar um ativo que existe no AEM, o sistema verifica se há conflito e indica-o. Os ativos são identificados usando o hash SHA-1 armazenado em `jcr:content/metadata/dam:sha1`, o que significa que os ativos do duplicado são detectados independentemente dos nomes dos arquivos.

>[!MORELIKETHIS]
>
>* [Ativos do Duplicado no repositório existente (um tutorial de um membro da comunidade)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

