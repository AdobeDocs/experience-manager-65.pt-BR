---
title: Habilitar detecção de ativos duplicados
description: Saiba como habilitar a detecção de ativos duplicados no Experience Manager.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
hide: true
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: c29e3a96-cd2b-4e21-b382-a8279aa04553
    internal-label: Asset reports
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%
---
# Habilitar detecção de ativos duplicados {#enable-detection-of-duplicate-assets}

Se você tentar carregar um ativo que existe em [!DNL Adobe Experience Manager Assets], o recurso de detecção de duplicidades o identifica como duplicado. A detecção de duplicados está desativada por padrão. Para ativar o recurso, siga estas etapas:

1. Abra a página de configuração do Console da Web [!DNL Experience Manager] acessando `https://[aem_server]:[port]/system/console/configMgr`.
1. Edite a configuração do servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Selecione a opção **[!UICONTROL detectar duplicata]** e clique em **[!UICONTROL Salvar]**.

   ![Selecione a opção de detecção de duplicidade no servlet](assets/chlimage_1-377.png)

   *Figura: selecione a opção de detecção de duplicidade no servlet.*

O recurso de detecção de duplicidade agora está habilitado em [!DNL Assets]. Quando um usuário tenta fazer upload de um ativo que existe em [!DNL Experience Manager], o sistema verifica se há conflito e o indica. Os ativos são identificados usando o hash SHA-1 armazenado em `jcr:content/metadata/dam:sha1`, o que significa que os ativos duplicados são detectados independentemente dos nomes de arquivo.

>[!MORELIKETHIS]
>
>* [Duplicar ativos no repositório existente (um tutorial de um membro da comunidade)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)
>* [Detectar ativos duplicados no AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/detect-duplicate-assets.html?lang=pt-BR)
