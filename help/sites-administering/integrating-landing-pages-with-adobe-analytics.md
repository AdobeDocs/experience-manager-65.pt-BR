---
title: Integração de páginas iniciais com o Adobe Analytics
seo-title: Integração de páginas iniciais com o Adobe Analytics
description: Saiba como integrar páginas iniciais ao Adobe Analytics.
seo-description: Saiba como integrar páginas iniciais ao Adobe Analytics.
uuid: 8f6672d1-497f-4ccb-b3cc-f6120fc467ba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 8ae7ccec-489b-4d20-ac56-6101402fb18a
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Integração de páginas iniciais com o Adobe Analytics{#integrating-landing-pages-with-adobe-analytics}

O AEM integrou a solução de páginas de aterrissagem com o [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) usando os seguintes componentes de chamada para ação (CTA):

1. Componente Click Through
1. Componente de link gráfico

Esses componentes expõem determinados atributos que podem ser mapeados por meio das variáveis do Adobe Analytics (Tráfego, variáveis de conversão) e eventos bem-sucedidos para enviar informações ao Adobe Analytics.

## Pré-requisitos {#prerequisites}

A Adobe recomenda que você passe pela integração [](/help/sites-administering/adobeanalytics.md) do AEM-Adobe Analytics para entender como essa integração funciona.

## Componentes disponíveis para mapeamento {#components-available-for-mapping}

No AEM, os componentes **Chamada para ação** - **ClickThroughLink** e **GraphicalLink** - exibidos aqui no sidekick, podem ser mapeados para variáveis do Adobe Analytics.

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### Mapeamento de componentes da página de aterrissagem para o Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

Para mapear os componentes da página inicial para o Adobe Analytics:

1. Depois de criar a configuração do Adobe Analytics e criar uma nova estrutura, selecione o conjunto de relatórios apropriado no menu suspenso. Isso resulta na busca das variáveis do Adobe Analytics e na sua exibição no localizador de conteúdo.
1. Arraste e solte os componentes Chamada para ação (CTA) do sidekick para a área de mapeamento no meio da página, conforme apropriado.

<table>
 <tbody>
  <tr>
   <td><strong>Nome do componente</strong></td>
   <td><strong>Atributos Expostos</strong></td>
   <td><strong>Significado do atributo</strong></td>
  </tr>
  <tr>
   <td><strong>Link de Click-Through CTA</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i><br /> </td>
   <td>O rótulo do link ou o texto do link </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i><br /> </td>
   <td>O destino para o qual você é direcionado ao clicar no link </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i><br /> </td>
   <td>O evento click </td>
  </tr>
  <tr>
   <td><strong>Link gráfico CTA</strong></td>
   <td><i>eventdata.clicktroughImageLabel</i><br /> </td>
   <td>O título da imagem CTA </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageTarget</i><br /> </td>
   <td>O destino para o qual você é levado ao clicar na imagem que contém um link</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageAsset</i><br /> </td>
   <td>O caminho para o ativo de imagem no repositório </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clicktroughImageClick</i><br /> </td>
   <td>O evento click</td>
  </tr>
 </tbody>
</table>

1. Mapeie esses atributos expostos com qualquer variável do Adobe Analytics a partir do localizador de conteúdo. A estrutura agora está pronta para ser usada.
1. Agora você pode criar uma nova página de aterrissagem ou abrir uma página de aterrissagem existente com componentes CTA existentes e clicar na guia Serviços **da** Cloud em Propriedades **da** página no sidekick (na interface otimizada ao toque, selecione **Abrir propriedades** e clique em Serviços **da** Cloud) e configurar a estrutura para usar com a página de aterrissagem. Selecione a estrutura na lista suspensa.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. Depois de configurar a estrutura com a página de aterrissagem, agora você pode usar os componentes instrumentados e todos os cliques no CTA são registrados no Adobe Analytics.

