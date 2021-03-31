---
title: Ativar a detecção de ativos duplicados
description: Saiba como habilitar a detecção de ativos duplicados no Experience Manager.
contentOwner: AG
role: Profissional de negócios, Administrador
feature: Gerenciamento de ativos,Relatórios de ativos
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Ativar a detecção de ativos duplicados {#enable-detection-of-duplicate-assets}

Se você tentar fazer upload de um ativo que existe em [!DNL Adobe Experience Manager Assets], o recurso de detecção de duplicatas o identificará como duplicado. A detecção de duplicados está desabilitada por padrão. Para ativar o recurso, execute as seguintes etapas:

1. Abra a página [!DNL Experience Manager] de configuração do Console da Web acessando `https://[aem_server]:[port]/system/console/configMgr`.
1. Edite a configuração do servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Selecione a opção **[!UICONTROL detect duplicate]** e clique em **[!UICONTROL Save]**.

   ![Selecione a opção detectar duplicata no servlet](assets/chlimage_1-377.png)

   *Figura: Selecione a opção detect duplicate no servlet.*

O recurso detectar duplicata agora está ativado em [!DNL Assets]. Quando um usuário tenta fazer upload de um ativo que existe em [!DNL Experience Manager], o sistema verifica se há conflito e o indica. Os ativos são identificados usando o hash SHA-1 armazenado em `jcr:content/metadata/dam:sha1`, o que significa que os ativos duplicados são detectados independentemente dos nomes de arquivo.

>[!MORELIKETHIS]
>
>* [Duplicar ativos no repositório existente (um tutorial de um membro da comunidade)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

