---
title: Usar imagem inteligente com relação de pixels de dispositivo do lado do cliente
description: Saiba como usar a Proporção de pixels de dispositivo do lado do cliente com imagens inteligentes no Adobe Experience Manager as a Cloud Service com Dynamic Media.
role: Admin,User
exl-id: e38f522a-242a-4ea9-a866-d8d129950831
source-git-commit: c8682118f15132063073df5cdc2b576b6e62a0c8
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Sobre a Smart Imaging com DPR (Device Pixel Ratio, rácio de pixels de dispositivo) do lado do cliente {#client-side-dpr}

A solução atual de Smart Imaging usa strings do agente do usuário para determinar o tipo de dispositivo (desktop, tablet, móvel e assim por diante) que está sendo usado.

Os recursos de detecção de dispositivo - DPR baseado em sequências de agente do usuário - são imprecisos com frequência, especialmente para dispositivos Apple. Além disso, sempre que um novo dispositivo for iniciado, ele deverá ser validado.

O DPR do lado do cliente fornece valores 100% precisos e funciona para qualquer dispositivo, seja o Apple ou qualquer outro novo dispositivo que foi inicializado.

## Usar o código DPR do lado do cliente

**Aplicativos renderizados do lado do servidor**

1. Inicialização do trabalhador do serviço de carregamento (`srvinit.js`) ao incluir o seguinte script na seção de cabeçalho da página HTML:

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   ```

   O Adobe recomenda carregar esse script _before_ quaisquer outros scripts para que o trabalhador de serviço inicie a inicialização imediatamente.

1. Inclua o seguinte código de tag de imagem do DPR na parte superior da seção do corpo da sua página do HTML:

   ```html
   <img src="aem_dm_dpr_1x.jpg" style="width:1px;height:1px;display:none"
       srcset="aem_dm_dpr_1x.jpg 1x, aem_dm_dpr_1.1x.jpg 1.1x, aem_dm_dpr_1.2x.jpg 1.2x, aem_dm_dpr_1.3x.jpg 1.3x, aem_dm_dpr_1.4x.jpg 1.4x, aem_dm_dpr_1.5x.jpg 1.5x, aem_dm_dpr_1.6x.jpg 1.6x,          aem_dm_dpr_1.7x.jpg 1.7x, aem_dm_dpr_1.8x.jpg 1.8x, aem_dm_dpr_1.9x.jpg 1.9x,
       aem_dm_dpr_2x.jpg 2x, aem_dm_dpr_2.1x.jpg 2.1x, aem_dm_dpr_2.2x.jpg 2.2x, aem_dm_dpr_2.3x.jpg 2.3x, aem_dm_dpr_2.4x.jpg 2.4x, aem_dm_dpr_2.5x.jpg 2.5x, aem_dm_dpr_2.6x.jpg 2.6x, aem_dm_dpr_2.7x.jpg 2.7x, aem_dm_dpr_2.8x.jpg 2.8x, aem_dm_dpr_2.9x.jpg 2.9x,
       aem_dm_dpr_3x.jpg 3x, aem_dm_dpr_3.1x.jpg 3.1x, aem_dm_dpr_3.2x.jpg 3.2x, aem_dm_dpr_3.3x.jpg 3.3x, aem_dm_dpr_3.4x.jpg 3.4x, aem_dm_dpr_3.5x.jpg 3.5x, aem_dm_dpr_3.6x.jpg 3.6x, aem_dm_dpr_3.7x.jpg 3.7x, aem_dm_dpr_3.8x.jpg 3.8x, aem_dm_dpr_3.9x.jpg 3.9x,
       aem_dm_dpr_4x.jpg 4x, aem_dm_dpr_4.1x.jpg 4.1x, aem_dm_dpr_4.2x.jpg 4.2x, aem_dm_dpr_4.3x.jpg 4.3x, aem_dm_dpr_4.4x.jpg 4.4x, aem_dm_dpr_4.5x.jpg 4.5x, aem_dm_dpr_4.6x.jpg 4.6x, aem_dm_dpr_4.7x.jpg 4.7x, aem_dm_dpr_4.8x.jpg 4.8x, aem_dm_dpr_4.9x.jpg 4.9x,
       aem_dm_dpr_5x.jpg 5x">
   ```

   É obrigatório incluir esse código de tag de imagem do DPR _before_ todas as imagens estáticas na sua página do HTML.

**Aplicativos renderizados do lado do cliente**

1. Inclua os seguintes scripts DPR na seção de cabeçalho da página HTML:

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   <script type="text/javascript" src="dprImageInjection.js"></script>
   ```

   É possível combinar ambos os scripts do DPR em um para evitar várias solicitações de rede.

   O Adobe recomenda carregar esses scripts _before_ qualquer outro script na página HTML.
O Adobe também recomenda que você Bootstrap seu aplicativo em diff HTML tag em vez de um elemento de corpo. A razão é porque `dprImageInjection.js` injeta dinamicamente a tag de imagem na parte superior da seção de corpo na página HTML.

## Download de arquivos JavaScript {#client-side-dpr-script}

Os arquivos JavaScript a seguir no download são fornecidos somente como referência de exemplo. Se você pretende usar esses arquivos em HTML pages, edite o código de cada arquivo para atender aos seus próprios requisitos.

* `dprImageInjection.js`
* `srvinit.js`
* `srvwrk.js`

[Download de arquivos JavaScript](/help/assets/assets-dm/aem-dynamicmedia-smartimaging-dpr.zip)

>[!MORELIKETHIS]
>
>* [Imagem inteligente](/help/assets/imaging-faq.md)

