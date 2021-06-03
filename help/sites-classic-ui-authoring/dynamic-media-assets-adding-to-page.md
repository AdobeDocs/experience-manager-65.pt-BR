---
title: Adição de ativos do Dynamic Media a páginas
description: Para adicionar a funcionalidade Dynamic Media aos ativos que você usa nos sites, é possível adicionar o componente Dynamic Media ou Mídia interativa diretamente na página.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: d2ebfca5-19f9-4fa5-b142-b978f46a912f
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 52%

---

# Adição de ativos do Dynamic Media a páginas{#adding-dynamic-media-assets-to-pages}

Para adicionar a funcionalidade Dynamic Media aos ativos que você usa nos sites, é possível adicionar o componente **[!UICONTROL Dynamic Media]** ou **[!UICONTROL Mídia interativa]** diretamente na página. Para isso, entre no modo [!UICONTROL Design] e ative os componentes do Dynamic Media. Em seguida, adicione esses componentes à página e adicionar ativos ao componente. A Dynamic Media e os componentes de mídia interativa são inteligentes - eles sabem se você está adicionando uma imagem ou um vídeo e as opções disponíveis mudam de acordo.

Você adiciona ativos do Dynamic Media diretamente à página se estiver usando o AEM como o WCM.

>[!NOTE]
>
>Os mapas de imagem estão disponíveis imediatamente para banners de carrossel.

## Adicionar um componente Dynamic Media a uma página {#adding-a-dynamic-media-component-to-a-page}

Adicionar o componente [!UICONTROL Dynamic Media] ou [!UICONTROL Mídia interativa] a uma página é o mesmo que adicionar um componente a qualquer página. Os componentes [!UICONTROL Dynamic Media] e [!UICONTROL Mídia interativa] são descritos detalhadamente nas seções a seguir.

Para adicionar um componente/visualizador de mídia dinâmica a uma página:

1. No AEM, abra a página à qual você deseja adicionar o componente Mídia dinâmica.
1. Se nenhum componente Dynamic Media estiver disponível, clique na régua no [!UICONTROL Sidekick] para entrar no modo **[!UICONTROL Design]**, clique em **[!UICONTROL Editar]** parsys e selecione **[!UICONTROL Dynamic Media]** para disponibilizar os componentes do Dynamic Media.

   >[!NOTE]
   >
   >Para obter mais informações, Consulte [Configuração dos componentes no modo de Design](/help/sites-authoring/default-components-designmode.md).

1. Retorne ao modo **[!UICONTROL Editar]** clicando no ícone de lápis no [!UICONTROL Sidekick].
1. Arraste o componente **[!UICONTROL Dynamic Media]** ou **[!UICONTROL Mídia interativa]** do grupo **[!UICONTROL Outro]** no sidekick para a página no local desejado.
1. Clique em **[!UICONTROL Editar]** para abrir o componente.
1. [](#dynamic-media-component)Edite o componente conforme necessário e clique em **[!UICONTROL OK]** para salvar as alterações.

## Componentes de mídia dinâmica {#dynamic-media-components}

[!UICONTROL Dynamic ] Media e  [!UICONTROL Mídia ] interativa estão disponíveis no   Sidekickem  **[!UICONTROL Dynamic Media]**. Você usa o componente **[!UICONTROL Mídia interativa]** para quaisquer ativos interativos, como vídeo interativo, imagens interativas ou conjuntos de carrossel. Para todos os outros componentes do Dynamic Media, use o componente **[!UICONTROL Dynamic Media]**.

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>Esses componentes não estão disponíveis por padrão e precisam ser selecionados no modo de Design antes de serem usados. [Depois que eles forem disponibilizados no modo de Design](/help/sites-authoring/default-components-designmode.md), você poderá adicionar os componentes à sua página como faria com qualquer outro componente do AEM.

### Componente Mídia dinâmica {#dynamic-media-component}

O componente Dynamic Media é inteligente — dependendo de você adicionar uma imagem ou um vídeo, você terá várias opções. O componente oferece suporte a predefinições de imagem, visualizadores baseados em imagem, como conjuntos de imagens, conjuntos de rotação, conjuntos de mídia mista e vídeo. Além disso, o visualizador é responsivo. Ou seja, o tamanho da tela muda automaticamente com base no tamanho da tela. Todos os visualizadores são visualizadores baseados em HTML5.

>[!NOTE]
>
>Ao adicionar o componente [!UICONTROL Dynamic Media] e **[!UICONTROL Configurações do Dynamic Media]** estiver em branco ou não for possível adicionar um ativo corretamente, verifique o seguinte:
>
>* Você [ativou a Mídia dinâmica](/help/assets/config-dynamic.md). As mídias dinâmicas são desativadas por padrão.
>* A imagem tem um arquivo tiff de pirâmide. As imagens importadas antes da ativação do Dynamic Media não têm um arquivo tiff de pirâmide.

>



#### Ao trabalhar com imagens {#when-working-with-images}

O componente [!UICONTROL Dynamic Media] permite adicionar imagens dinâmicas, incluindo conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista. Você pode ampliar, reduzir e, se aplicável, transformar uma imagem em um conjunto de giro ou selecionar uma imagem de outro tipo de conjunto.

Você também pode configurar a predefinição do visualizador, a predefinição da imagem ou o formato da imagem diretamente no componente. Para tornar uma imagem responsiva, você pode definir os pontos de interrupção ou aplicar uma predefinição de imagem responsiva.

![chlimage_1-72](assets/chlimage_1-72a.png)

Você pode editar as seguintes configurações do Dynamic Media clicando em **[!UICONTROL Editar]** no componente e clicando na guia **[!UICONTROL Configurações do Dynamic Media]**.

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>Por padrão, o componente de imagem do Dynamic Media é adaptável. Se quiser torná-lo de um tamanho fixo, defina-o no componente na guia **[!UICONTROL Avançado]** com as propriedades **[!UICONTROL Largura]** e **[!UICONTROL Altura]**.

**[!UICONTROL Predefinição do visualizador]**  - Selecione uma predefinição do visualizador existente no menu suspenso. Se a predefinição de visualizador que você está procurando não estiver visível, pode ser necessário torná-la visível. Consulte [Gerenciar predefinições do visualizador](/help/assets/managing-viewer-presets.md). Não é possível selecionar uma predefinição de visualizador se você estiver usando uma predefinição de imagem e vice-versa.

Essa será a única opção disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia. As predefinições do visualizador exibidas também são inteligentes - somente as predefinições do visualizador relevantes são exibidas.

**[!UICONTROL Predefinição de imagem]**  - Selecione uma predefinição de imagem existente no menu suspenso. Se a predefinição de imagem que você está procurando não estiver visível, pode ser necessário torná-la visível. Consulte [Gerenciar predefinições de imagens](/help/assets/managing-image-presets.md). Não é possível selecionar uma predefinição de visualizador se você estiver usando uma predefinição de imagem e vice-versa.

Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

**[!UICONTROL Modificadores de imagem]**  - Você pode alterar os efeitos de imagem fornecendo comandos de imagem adicionais. Eles são descritos em [Gerenciar predefinições de imagem](/help/assets/managing-viewer-presets.md) e na [Referência de comando](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

**[!UICONTROL Pontos de interrupção]**  - se estiver usando esse ativo em um site responsivo, é necessário adicionar os pontos de interrupção da página. Os pontos de interrupção da imagem precisam ser separados por vírgulas (,). Essa opção funciona quando não há altura ou largura definida em uma predefinição de imagem.

Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

Você pode editar as seguintes [!UICONTROL Configurações avançadas] clicando em **[!UICONTROL Editar]** no componente.

**[!UICONTROL Título]**  - Altere o título da imagem.

**[!UICONTROL Texto alternativo]**  - Adicione um título à imagem para os usuários que têm os gráficos desativados.

Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

**[!UICONTROL URL, Abrir em]**  - É possível definir um ativo de para abrir um link. Defina o **[!UICONTROL URL]** e **[!UICONTROL Abrir em]** para indicar se deseja que ele seja aberto na mesma janela ou em uma nova janela.

Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

**[!UICONTROL Largura e altura]**  - Insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esses valores em branco torna o recurso adaptável.

#### Ao trabalhar com vídeo {#when-working-with-video}

Use o componente [!UICONTROL Dynamic Media] para adicionar vídeo dinâmico às suas páginas da Web. Ao editar o componente, você pode optar por usar uma predefinição de visualizador de vídeo predefinida para reproduzir o vídeo na página.

![chlimage_1-74](assets/chlimage_1-74a.png)

Você pode editar as seguintes [!UICONTROL Configurações do Dynamic Media] clicando em **[!UICONTROL Editar]** no componente.

>[!NOTE]
>
>Por padrão, o componente de vídeo Mídia dinâmica é adaptável. Se quiser torná-lo de um tamanho fixo, defina-o no componente com a **[!UICONTROL Largura]** e **[!UICONTROL Altura]** na guia **[!UICONTROL Avançado]**.

**[!UICONTROL Predefinição do visualizador]**  - Selecione uma predefinição do visualizador de vídeo existente no menu suspenso. Se a predefinição de visualizador que você está procurando não estiver visível, pode ser necessário torná-la visível. Consulte [Gerenciar predefinições do visualizador](/help/assets/managing-viewer-presets.md).

Você pode editar as seguintes configurações [!UICONTROL Avançado] clicando em **[!UICONTROL Editar]** no componente.

**[!UICONTROL Título]**  - Altere o título do vídeo.

**[!UICONTROL Largura e altura]**  - Insira o valor em pixels se desejar que o vídeo tenha um tamanho fixo. Deixar esses valores em branco faz com ele que seja adaptável.

#### Como fornecer vídeos seguros {#how-to-delivery-secure-video}

No AEM 6.2, ao instalar [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480), você pode controlar se um vídeo é entregue por meio de uma conexão SSL segura (HTTPS) ou por uma conexão não segura (HTTP). Por padrão, o protocolo de entrega de vídeo é herdado automaticamente do protocolo da página da web de incorporação. Se a página da web for carregada via HTTPS, o vídeo também será entregue via HTTPS. E vice-versa, se a página da web estiver em HTTP, o vídeo será entregue via HTTP. Na maioria dos casos, esse comportamento padrão é satisfatório, e não há necessidade de fazer alterações na configuração. No entanto, você pode substituir esse comportamento padrão anexando `VideoPlayer.ssl=on` ao final de um caminho de URL ou à lista de outros parâmetros de configuração do visualizador em um trecho de código de incorporação, para forçar a entrega segura de vídeos.

Para obter mais informações sobre a entrega segura de vídeos e o uso do atributo de configuração `VideoPlayer.ssl` no caminho do URL, consulte [Entrega de vídeo seguro](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html) no Guia de referência de visualizadores. Além do visualizador de Vídeo, a entrega segura de vídeo está disponível para o visualizador de Mídia mista e o visualizador de Vídeo interativo.

### Componente Mídia interativa {#interactive-media-component}

O componente Mídia interativa é para ativos que possuem interatividade em pontos de acesso ou mapas de imagem. Se você tiver uma imagem interativa, um vídeo interativo ou um banner de carrossel, use o componente **[!UICONTROL Mídia interativa]**.

O componente [!UICONTROL Mídia interativa] é inteligente - dependendo de você adicionar uma imagem ou um vídeo, você terá várias opções. Além disso, o visualizador é responsivo. Ou seja, o tamanho da tela muda automaticamente com base no tamanho da tela. Todos os visualizadores são visualizadores baseados em HTML5.

![chlimage_1-75](assets/chlimage_1-75a.png)

É possível editar as seguintes configurações **[!UICONTROL Gerais]** clicando em **[!UICONTROL Editar]** no componente.

**[!UICONTROL Predefinição do visualizador]**  - Selecione uma predefinição do visualizador existente no menu suspenso. Se a predefinição de visualizador que você está procurando não estiver visível, pode ser necessário torná-la visível. As Predefinições do visualizador devem ser publicadas para poderem ser usadas. Consulte Gerenciar predefinições do visualizador.

**[!UICONTROL Título]**  - Altere o título do vídeo.

**[!UICONTROL Largura e altura]**  - Insira o valor em pixels se desejar que o vídeo tenha um tamanho fixo. Deixar esses valores em branco faz com ele que seja adaptável.

É possível editar as seguintes configurações de **[!UICONTROL Adicionar ao carrinho]** clicando em **[!UICONTROL Editar]** no componente.

**[!UICONTROL Mostrar ativo do produto]**  - por padrão, esse valor é selecionado. O ativo do produto mostra uma imagem do produto, conforme definido no módulo Comércio. Limpe a marca de seleção para não mostrar o ativo do produto.

**[!UICONTROL Mostrar preço do produto]**  - por padrão, esse valor é selecionado. O preço do produto mostra o preço do item, conforme definido no módulo Comércio. Limpe a marca de seleção para não mostrar o preço do produto.

**[!UICONTROL Mostrar formulário do produto]**  - por padrão, esse valor não está selecionado. O Formulário de produto inclui quaisquer variantes de produto, como tamanho e cor. Limpe a marca de seleção para não mostrar as variantes do produto.
