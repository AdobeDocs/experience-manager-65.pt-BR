---
title: Usar Imagem inteligente com proporção de pixels do dispositivo no lado do cliente
description: Saiba como usar a proporção de pixels do dispositivo no lado do cliente com a Imagem inteligente no Adobe Experience Manager as a Cloud Service com Dynamic Media.
role: Admin,User
exl-id: e38f522a-242a-4ea9-a866-d8d129950831
solution: Experience Manager, Experience Manager Assets
feature: Smart Imaging
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
subfeature_v2:
  - id: b39a6d56-d787-413f-8024-351803c28d44
    internal-label: Smart Imaging
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%
---
# Sobre a imagem inteligente com a proporção de pixels do dispositivo (DPR) do lado do cliente {#client-side-dpr}

A solução Smart Imaging atual usa strings de agente do usuário para determinar o tipo de dispositivo (desktop, tablet, celular e assim por diante) que está sendo usado.

Os recursos de detecção de dispositivos - DPR com base em sequências de agente do usuário - geralmente são imprecisos, especialmente para dispositivos Apple. Além disso, sempre que um novo dispositivo for iniciado, ele deverá ser validado.

A DPR do lado do cliente fornece valores 100% precisos e funciona para qualquer dispositivo, seja o Apple ou qualquer outro novo dispositivo iniciado.

## Usar o código DPR do lado do cliente

**Aplicativos renderizados do lado do servidor**

1. Carregue a inicialização do service worker (`srvinit.js`) incluindo o seguinte script na seção de cabeçalho da página do HTML:

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   ```

   A Adobe recomenda que você carregue este script _antes_ de qualquer outro script para que o service worker comece a inicialização imediatamente.

1. Inclua o seguinte código de tag de imagem DPR na parte superior da seção body da página HTML:

   ```html
   <img src="aem_dm_dpr_1x.jpg" style="width:1px;height:1px;display:none"
       srcset="aem_dm_dpr_1x.jpg 1x, aem_dm_dpr_1.1x.jpg 1.1x, aem_dm_dpr_1.2x.jpg 1.2x, aem_dm_dpr_1.3x.jpg 1.3x, aem_dm_dpr_1.4x.jpg 1.4x, aem_dm_dpr_1.5x.jpg 1.5x, aem_dm_dpr_1.6x.jpg 1.6x,          aem_dm_dpr_1.7x.jpg 1.7x, aem_dm_dpr_1.8x.jpg 1.8x, aem_dm_dpr_1.9x.jpg 1.9x,
       aem_dm_dpr_2x.jpg 2x, aem_dm_dpr_2.1x.jpg 2.1x, aem_dm_dpr_2.2x.jpg 2.2x, aem_dm_dpr_2.3x.jpg 2.3x, aem_dm_dpr_2.4x.jpg 2.4x, aem_dm_dpr_2.5x.jpg 2.5x, aem_dm_dpr_2.6x.jpg 2.6x, aem_dm_dpr_2.7x.jpg 2.7x, aem_dm_dpr_2.8x.jpg 2.8x, aem_dm_dpr_2.9x.jpg 2.9x,
       aem_dm_dpr_3x.jpg 3x, aem_dm_dpr_3.1x.jpg 3.1x, aem_dm_dpr_3.2x.jpg 3.2x, aem_dm_dpr_3.3x.jpg 3.3x, aem_dm_dpr_3.4x.jpg 3.4x, aem_dm_dpr_3.5x.jpg 3.5x, aem_dm_dpr_3.6x.jpg 3.6x, aem_dm_dpr_3.7x.jpg 3.7x, aem_dm_dpr_3.8x.jpg 3.8x, aem_dm_dpr_3.9x.jpg 3.9x,
       aem_dm_dpr_4x.jpg 4x, aem_dm_dpr_4.1x.jpg 4.1x, aem_dm_dpr_4.2x.jpg 4.2x, aem_dm_dpr_4.3x.jpg 4.3x, aem_dm_dpr_4.4x.jpg 4.4x, aem_dm_dpr_4.5x.jpg 4.5x, aem_dm_dpr_4.6x.jpg 4.6x, aem_dm_dpr_4.7x.jpg 4.7x, aem_dm_dpr_4.8x.jpg 4.8x, aem_dm_dpr_4.9x.jpg 4.9x,
       aem_dm_dpr_5x.jpg 5x">
   ```

   É obrigatório incluir este código de marca de imagem DPR _antes_ em todas as imagens estáticas da sua página do HTML.

**Aplicativos renderizados do lado do cliente**

1. Inclua os seguintes scripts DPR na seção de cabeçalho da página do HTML:

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   <script type="text/javascript" src="dprImageInjection.js"></script>
   ```

   Você pode combinar ambos os scripts DPR em um para evitar várias solicitações de rede.

   A Adobe recomenda que você carregue esses scripts _antes_ de qualquer outro script na página do HTML.
   A Adobe também recomenda que você Bootstrap seu aplicativo em tag HTML de comparação em vez de um elemento body. O motivo é que o `dprImageInjection.js` injeta dinamicamente a marca de imagem na parte superior da seção do corpo na página do HTML.

## Download de arquivos do JavaScript {#client-side-dpr-script}

Os seguintes arquivos JavaScript no download são fornecidos a você somente como referência de exemplo. Se você pretende usar esses arquivos nas páginas do HTML, edite o código de cada arquivo para atender aos seus próprios requisitos.

* `dprImageInjection.js`
* `srvinit.js`
* `srvwrk.js`

[Download de arquivos do JavaScript](/help/assets/assets-dm/aem-dynamicmedia-smartimaging-dpr.zip)

>[!MORELIKETHIS]
>
>* [Imagem inteligente](/help/assets/imaging-faq.md)
