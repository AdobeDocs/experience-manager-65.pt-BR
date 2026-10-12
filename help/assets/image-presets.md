---
title: Aplicar predefinições de imagem do Dynamic Media
description: Saiba como você pode permitir que os ativos forneçam imagens dinamicamente em diferentes tamanhos, formatos ou com outras propriedades de imagem geradas dinamicamente.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Image Presets
role: User,Admin
exl-id: 98d88b59-eb8f-42db-abb8-04506a5b8c30
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: d4b6216b-4a89-4ff0-8ac0-5a699ba23100
    internal-label: Images and videos
subfeature_v2:
  - id: a16e03b7-8456-4383-8860-31ab5ab00e9e
    internal-label: Image presets
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 3%
---
# Aplicar predefinições de imagem do Dynamic Media {#applying-image-presets}

As predefinições de imagem permitem que os ativos forneçam imagens dinamicamente em diferentes tamanhos, formatos ou com outras propriedades de imagem geradas dinamicamente. É possível escolher uma predefinição ao exportar imagens. A predefinição reformata imagens de acordo com as especificações especificadas pelo administrador.

Além disso, você pode escolher uma predefinição de imagem que seja responsiva (designada pelo botão **[!UICONTROL RESS]** depois de selecioná-la).

Esta seção descreve como usar predefinições de imagens. [Os administradores podem criar e configurar predefinições de imagens](managing-image-presets.md).

>[!NOTE]
>
>A geração de imagens inteligentes funciona com suas predefinições de imagens existentes e usa inteligência nos últimos milissegundos do delivery para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador ou da conexão de rede. Consulte [Smart Imaging](imaging-faq.md) para obter mais informações.

É possível aplicar uma predefinição de imagem a uma imagem sempre que ela for visualizada.

>[!NOTE]
>
>No modo Dynamic Media - Scene7, as predefinições de imagem são compatíveis somente com ativos de imagem.

**Para aplicar predefinições de imagem do Dynamic Media:**

1. Abra o ativo e, no painel à esquerda, selecione o menu suspenso e **[!UICONTROL Representações]**.

   >[!NOTE]
   >
   >* As representações estáticas aparecem na metade superior do painel. As representações dinâmicas aparecem na metade inferior. Somente com representações dinâmicas, é possível usar o URL para exibir a imagem. O botão **[!UICONTROL URL]** só será exibido se você selecionar uma representação dinâmica. O botão **[!UICONTROL RESS]** só será exibido se você selecionar uma predefinição de imagem responsiva.
   >
   >* O sistema mostra várias execuções ao selecionar **[!UICONTROL Representações]** na exibição de Detalhes de um ativo. Você pode aumentar o número de predefinições vistas. Consulte [Aumentar o número de predefinições de imagens exibidas](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display).

   ![chlimage_1-208](assets/chlimage_1-208.png)

1. Siga um destes procedimentos:

   * Selecione uma representação dinâmica para poder visualizar a predefinição de imagem.
   * Para exibir o pop-up, selecione **[!UICONTROL URL]**, **[!UICONTROL Incorporar]** ou **[!UICONTROL RESS]**.

   >[!NOTE]
   >
   >Se o ativo *e* a predefinição de imagem ainda não foi publicada, o botão **[!UICONTROL URL]** (ou os botões **[!UICONTROL URL]** e **[!UICONTROL RESS]**, se aplicável) não estará disponível.
   >
   >Observe também que as predefinições de imagem são publicadas automaticamente em um servidor do Dynamic Media.
