---
title: Usar Imagem inteligente com proporção de pixels do dispositivo no lado do cliente
description: Saiba como usar a proporção de pixels do dispositivo no lado do cliente com a Imagem inteligente no Adobe Experience Manager as a Cloud Service com o Dynamic Media.
role: Admin,User
exl-id: e38f522a-242a-4ea9-a866-d8d129950831
source-git-commit: c8682118f15132063073df5cdc2b576b6e62a0c8
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Sobre a imagem inteligente com a proporção de pixels do dispositivo (DPR) do lado do cliente {#client-side-dpr}

A solução Smart Imaging atual usa strings de agente do usuário para determinar o tipo de dispositivo (desktop, tablet, celular e assim por diante) que está sendo usado.

Os recursos de detecção de dispositivos - DPR com base em sequências de agente do usuário - geralmente são imprecisos, especialmente para dispositivos Apple. Além disso, sempre que um novo dispositivo for iniciado, ele deverá ser validado.

A DPR do lado do cliente fornece valores 100% precisos e funciona para qualquer dispositivo, seja o Apple ou qualquer outro novo dispositivo iniciado.

## Usar o código DPR do lado do cliente

**Aplicativos renderizados do lado do servidor**

1. Carregar inicialização do trabalhador do serviço (`srvinit.js`) incluindo o seguinte script na seção de cabeçalho da página HTML:

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   ```

   O Adobe recomenda que você carregue esse script _antes_ qualquer outro script para que o service worker comece a inicialização imediatamente.

1. Inclua o seguinte código de tag de imagem DPR na parte superior da seção body da página HTML:

   ```html
   <img src="aem_dm_dpr_1x.jpg" style="width:1px;height:1px;display:none"
       srcset="aem_dm_dpr_1x.jpg 1x, aem_dm_dpr_1.1x.jpg 1.1x, aem_dm_dpr_1.2x.jpg 1.2x, aem_dm_dpr_1.3x.jpg 1.3x, aem_dm_dpr_1.4x.jpg 1.4x, aem_dm_dpr_1.5x.jpg 1.5x, aem_dm_dpr_1.6x.jpg 1.6x,          aem_dm_dpr_1.7x.jpg 1.7x, aem_dm_dpr_1.8x.jpg 1.8x, aem_dm_dpr_1.9x.jpg 1.9x,
       aem_dm_dpr_2x.jpg 2x, aem_dm_dpr_2.1x.jpg 2.1x, aem_dm_dpr_2.2x.jpg 2.2x, aem_dm_dpr_2.3x.jpg 2.3x, aem_dm_dpr_2.4x.jpg 2.4x, aem_dm_dpr_2.5x.jpg 2.5x, aem_dm_dpr_2.6x.jpg 2.6x, aem_dm_dpr_2.7x.jpg 2.7x, aem_dm_dpr_2.8x.jpg 2.8x, aem_dm_dpr_2.9x.jpg 2.9x,
       aem_dm_dpr_3x.jpg 3x, aem_dm_dpr_3.1x.jpg 3.1x, aem_dm_dpr_3.2x.jpg 3.2x, aem_dm_dpr_3.3x.jpg 3.3x, aem_dm_dpr_3.4x.jpg 3.4x, aem_dm_dpr_3.5x.jpg 3.5x, aem_dm_dpr_3.6x.jpg 3.6x, aem_dm_dpr_3.7x.jpg 3.7x, aem_dm_dpr_3.8x.jpg 3.8x, aem_dm_dpr_3.9x.jpg 3.9x,
       aem_dm_dpr_4x.jpg 4x, aem_dm_dpr_4.1x.jpg 4.1x, aem_dm_dpr_4.2x.jpg 4.2x, aem_dm_dpr_4.3x.jpg 4.3x, aem_dm_dpr_4.4x.jpg 4.4x, aem_dm_dpr_4.5x.jpg 4.5x, aem_dm_dpr_4.6x.jpg 4.6x, aem_dm_dpr_4.7x.jpg 4.7x, aem_dm_dpr_4.8x.jpg 4.8x, aem_dm_dpr_4.9x.jpg 4.9x,
       aem_dm_dpr_5x.jpg 5x">
   ```

   É obrigatório incluir esse código de tag de imagem DPR _antes_ todas as imagens estáticas na página do HTML.

**Aplicativos renderizados do lado do cliente**

1. Inclua os seguintes scripts DPR na seção de cabeçalho da página HTML:

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   <script type="text/javascript" src="dprImageInjection.js"></script>
   ```

   Você pode combinar ambos os scripts DPR em um para evitar várias solicitações de rede.

   O Adobe recomenda carregar esses scripts _antes_ qualquer outro script na página HTML.
O Adobe também recomenda que você Bootstrap seu aplicativo com a tag HTML diff em vez de um elemento body. O motivo é porque `dprImageInjection.js` injeta dinamicamente a tag de imagem na parte superior da seção body na página HTML.

## Download de arquivos JavaScript {#client-side-dpr-script}

Os seguintes arquivos JavaScript no download são fornecidos a você somente como referência de exemplo. Se você pretende usar esses arquivos em páginas de HTML, edite o código de cada arquivo para atender aos seus próprios requisitos.

* `dprImageInjection.js`
* `srvinit.js`
* `srvwrk.js`

[Download de arquivos JavaScript](/help/assets/assets-dm/aem-dynamicmedia-smartimaging-dpr.zip)

>[!MORELIKETHIS]
>
>* [Imagem inteligente](/help/assets/imaging-faq.md)

