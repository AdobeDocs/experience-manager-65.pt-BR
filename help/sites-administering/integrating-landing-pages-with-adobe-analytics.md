---
title: Integração de landing pages ao Adobe Analytics
description: Saiba como integrar páginas de aterrissagem ao Adobe Analytics.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: da3f7b7e-87e5-446a-9a77-4b12b850a381
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%
---
# Integração de landing pages ao Adobe Analytics{#integrating-landing-pages-with-adobe-analytics}

A AEM integrou a solução de páginas de aterrissagem com o [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) usando os seguintes componentes do call-to-action (CTA):

1. Componente de Click Through
1. Componente Link gráfico

Esses componentes expõem determinados atributos que podem ser mapeados por meio de variáveis do Adobe Analytics (tráfego, variáveis de conversão) e eventos bem-sucedidos para enviar informações ao Adobe Analytics.

## Pré-requisitos {#prerequisites}

A Adobe recomenda que você passe pela [integração AEM-Adobe Analytics existente](/help/sites-administering/adobeanalytics.md) para entender como essa integração funciona.

## Componentes disponíveis para mapeamento {#components-available-for-mapping}

No AEM, os componentes do **Call to action** - **ClickThroughLink** e **GraphicalLink** - exibidos aqui no sidekick, podem ser mapeados para variáveis do Adobe Analytics.

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### Mapeamento de componentes da página de aterrissagem para o Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

Para mapear componentes da página de aterrissagem para o Adobe Analytics:

1. Depois de criar a configuração do Adobe Analytics e uma estrutura, selecione o conjunto de relatórios apropriado no menu suspenso. Isso resulta na busca das variáveis do Adobe Analytics e sua exibição no localizador de conteúdo.
1. Arraste e solte os componentes do Call to action (CTA) do sidekick na área de mapeamento no meio da página, conforme apropriado.

<table>
 <tbody>
  <tr>
   <td><strong>Nome do componente</strong></td>
   <td><strong>Atributos expostos</strong></td>
   <td><strong>Significado do atributo</strong></td>
  </tr>
  <tr>
   <td><strong>Link de Click Through do CTA</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i> <br /> </td>
   <td>O rótulo no link ou o texto do link </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i> <br /> </td>
   <td>O destino para onde você foi levado ao clicar no link </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i> <br /> </td>
   <td>O evento click </td>
  </tr>
  <tr>
   <td><strong>Link gráfico do CTA</strong></td>
   <td><i>eventdata.clickthroughImageLabel</i> <br /> </td>
   <td>O título da imagem do CTA </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughImageTarget</i> <br /> </td>
   <td>O destino para onde você foi levado ao clicar na imagem que contém um link</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughImageAsset</i> <br /> </td>
   <td>O caminho para o ativo de imagem no repositório </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughImageClick</i> <br /> </td>
   <td>O evento click</td>
  </tr>
 </tbody>
</table>

1. Mapeie esses atributos expostos com qualquer variável do Adobe Analytics no localizador de conteúdo. A estrutura agora está pronta para uso.
1. Agora você pode criar uma página de aterrissagem ou abrir uma página de aterrissagem existente com componentes existentes do CTA e clicar na guia **Serviços da Nuvem** em **Propriedades da Página** no sidekick (na interface otimizada para toque, selecione **Abrir Propriedades** e clique em **Serviços da Nuvem**) e configurar a estrutura para usar com a página de aterrissagem. Selecione a estrutura na lista suspensa.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. Após configurar a estrutura com a página de aterrissagem, agora é possível usar os componentes instrumentados e os cliques no CTA são registrados no Adobe Analytics.
