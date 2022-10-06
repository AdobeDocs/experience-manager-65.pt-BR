---
title: Integração de páginas de aterrissagem com o Adobe Analytics
seo-title: Integrating Landing Pages with Adobe Analytics
description: Saiba como integrar landing pages ao Adobe Analytics.
seo-description: Learn how to integrate landing pages with Adobe Analytics.
uuid: 8f6672d1-497f-4ccb-b3cc-f6120fc467ba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 8ae7ccec-489b-4d20-ac56-6101402fb18a
exl-id: da3f7b7e-87e5-446a-9a77-4b12b850a381
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Integração de páginas de aterrissagem com o Adobe Analytics{#integrating-landing-pages-with-adobe-analytics}

A AEM integrou a solução de landing pages com o [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) usando os seguintes componentes de chamada-para-ação (CTA):

1. Componente de Click-Through
1. Componente de link gráfico

Esses componentes expõem determinados atributos que podem ser mapeados por meio das variáveis do Adobe Analytics (Tráfego, variáveis de conversão) e eventos de sucesso para enviar informações para o Adobe Analytics.

## Pré-requisitos {#prerequisites}

O Adobe recomenda que você passe pelo [integração AEM-Adobe Analytics existente](/help/sites-administering/adobeanalytics.md) para entender como essa integração funciona.

## Componentes disponíveis para mapeamento {#components-available-for-mapping}

Em AEM, a variável **Chamada à ação** componentes - **ClickThroughLink** e **GraphicalLink** - exibido aqui no sidekick, pode ser mapeado para variáveis do Adobe Analytics.

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### Mapeamento de componentes da página de aterrissagem para o Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

Para mapear componentes de página de aterrissagem para o Adobe Analytics:

1. Depois de criar a configuração do Adobe Analytics e criar uma nova estrutura, selecione o conjunto de relatórios apropriado no menu suspenso. Isso resulta na busca das variáveis do Adobe Analytics e na exibição delas no localizador de conteúdo.
1. Arraste e solte os componentes de Chamada para ação (CTA) do sidekick até a área de mapeamento no meio da página, conforme apropriado.

<table>
 <tbody>
  <tr>
   <td><strong>Nome do componente</strong></td>
   <td><strong>Atributos expostos</strong></td>
   <td><strong>Significado do atributo</strong></td>
  </tr>
  <tr>
   <td><strong>Link de Click Through CTA</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i> <br /> </td>
   <td>O rótulo no link ou o texto do link </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i> <br /> </td>
   <td>O destino para onde você é levado ao clicar no link </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i> <br /> </td>
   <td>O evento click </td>
  </tr>
  <tr>
   <td><strong>Link gráfico CTA</strong></td>
   <td><i>eventdata.clicktroughImageLabel</i> <br /> </td>
   <td>O título da imagem do CTA </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageTarget</i> <br /> </td>
   <td>O destino onde você é levado ao clicar na imagem que contém um link</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageAsset</i> <br /> </td>
   <td>O caminho para o ativo de imagem no repositório </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clicktroughImageClick</i> <br /> </td>
   <td>O evento click</td>
  </tr>
 </tbody>
</table>

1. Mapeie esses atributos expostos com qualquer variável do Adobe Analytics a partir do localizador de conteúdo. A estrutura agora está pronta para ser usada.
1. Agora é possível criar uma nova landing page ou abrir uma landing page existente com componentes CTA existentes e clicar em **Cloud Services** em **Propriedades da página** no sidekick (na interface otimizada para toque, selecione **Abrir propriedades** e clique em **Cloud Services**) e configure a estrutura a ser usada com a landing page. Selecione a estrutura na lista suspensa.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. Depois de configurar a estrutura com a landing page, você pode usar os componentes instrumentados e todos os cliques no CTA são registrados no Adobe Analytics.
