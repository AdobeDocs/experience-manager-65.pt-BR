---
title: Habilitar detecção de ativos duplicados
description: Saiba como habilitar a detecção de ativos duplicados no Experience Manager.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
hide: true
source-git-commit: 477c62b857ab98d8617c7bd8ba226019d42d330d
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Habilitar detecção de ativos duplicados {#enable-detection-of-duplicate-assets}

Se você tentar fazer upload de um ativo que existe no [!DNL Adobe Experience Manager Assets], o recurso de detecção de duplicidades o identifica como duplicado. A detecção de duplicados está desativada por padrão. Para ativar o recurso, siga estas etapas:

1. Abra o [!DNL Experience Manager] Página de configuração do Console da Web acessando `https://[aem_server]:[port]/system/console/configMgr`.
1. Edite a configuração do servlet **[!UICONTROL Criar ativo DAM CQ do dia]**.
1. Selecione o **[!UICONTROL detectar duplicata]** e clique em **[!UICONTROL Salvar]**.

   ![Selecione a opção detectar duplicatas no servlet](assets/chlimage_1-377.png)

   *Figura: selecione a opção detectar duplicação no servlet.*

O recurso de detecção de duplicidade agora está habilitado em [!DNL Assets]. Quando um usuário tenta fazer upload de um ativo que existe no [!DNL Experience Manager], o sistema verifica se há conflito e o indica. Os ativos são identificados usando o hash SHA-1 armazenado em `jcr:content/metadata/dam:sha1`, o que significa que ativos duplicados são detectados independentemente dos nomes de arquivo.

>[!MORELIKETHIS]
>
>* [Ativos duplicados no repositório existente (um tutorial de um membro da comunidade)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)
>* [Detectar ativos duplicados no AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/detect-duplicate-assets.html)
