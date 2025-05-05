---
title: Adição de ativos do Dynamic Media a páginas
description: Para adicionar a funcionalidade Dynamic Media aos ativos que você usa nos sites, é possível adicionar o componente Dynamic Media ou Mídia interativa diretamente na página.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: d2ebfca5-19f9-4fa5-b142-b978f46a912f
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 2%

---

# Adição de ativos do Dynamic Media a páginas{#adding-dynamic-media-assets-to-pages}

Para adicionar a funcionalidade Dynamic Media aos ativos que você usa nos sites, é possível adicionar o componente **[!UICONTROL Dynamic Media]** ou **[!UICONTROL Mídia interativa]** diretamente na página. Entre no modo **[!UICONTROL Design]** e habilite os componentes do Dynamic Media. Em seguida, adicione esses componentes à página e adicionar ativos ao componente. Os componentes de mídia interativa e do Dynamic Media são inteligentes - eles sabem se você está adicionando uma imagem ou um vídeo e as opções disponíveis mudam de acordo.

Você adiciona ativos do Dynamic Media diretamente à página se estiver usando o Adobe Experience Manager como o WCM.

>[!NOTE]
>
>Os mapas de imagem estão disponíveis prontamente para os banners do carrossel.

## Adicionar um componente Dynamic Media a uma página {#adding-a-dynamic-media-component-to-a-page}

Adicionar o componente [!UICONTROL Dynamic Media] ou [!UICONTROL Mídia interativa] a uma página é o mesmo que adicionar um componente a qualquer página. Os componentes [!UICONTROL Dynamic Media] e [!UICONTROL Mídia interativa] são descritos detalhadamente nas seções a seguir.

Para adicionar um componente/visualizador do Dynamic Media a uma página:

1. No Experience Manager, abra a página em que deseja adicionar o componente Dynamic Media.
1. Se nenhum componente do Dynamic Media estiver disponível, selecione a régua no [!UICONTROL Sidekick] para entrar no modo **[!UICONTROL Design]**.
1. Selecione **[!UICONTROL Editar]** parsys.
1. Selecione **[!UICONTROL Dynamic Media]** para disponibilizar os componentes do Dynamic Media.

   >[!NOTE]
   >
   >Consulte [Configurando Componentes no Modo de Design](/help/sites-authoring/default-components-designmode.md) para obter mais informações.

1. Retorne ao modo **[!UICONTROL Editar]** clicando no ícone de lápis no [!UICONTROL Sidekick].
1. Arraste o componente **[!UICONTROL Dynamic Media]** ou **[!UICONTROL Mídia interativa]** do grupo **[!UICONTROL Outros]** no sidekick para a página no local desejado.
1. Selecione **[!UICONTROL Editar]** para que o componente seja aberto.
1. [Edite o componente](#dynamic-media-component) conforme necessário.
1. Selecione **[!UICONTROL OK]** para salvar suas alterações.

## Componentes do Dynamic Media {#dynamic-media-components}

A [!UICONTROL Dynamic Media] e a [!UICONTROL Mídia interativa] estão disponíveis no [!UICONTROL Sidekick] em **[!UICONTROL Dynamic Media]**. Use o componente **[!UICONTROL Mídia interativa]** para qualquer ativo interativo, como vídeo interativo, imagens interativas ou conjuntos de carrossel. Para todos os outros componentes do Dynamic Media, use o componente **[!UICONTROL Dynamic Media]**.

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>Esses componentes não estão disponíveis por padrão e devem ser selecionados no modo Design antes de usar. [Depois que eles forem disponibilizados no modo de Design](/help/sites-authoring/default-components-designmode.md), você poderá adicionar os componentes à sua página como faria com qualquer outro componente Experience Manager.

### Componente do Dynamic Media {#dynamic-media-component}

O componente Dynamic Media é inteligente — dependendo se você adiciona uma imagem ou um vídeo, existem várias opções. O componente oferece suporte a predefinições de imagens, visualizadores baseados em imagem, como conjuntos de imagens, conjuntos de rotação, conjuntos de mídia mista e vídeo. Além disso, o visualizador é responsivo. Ou seja, o tamanho da tela muda automaticamente com base no tamanho da tela. Todos os visualizadores são baseados em HTML5.

>[!NOTE]
>
>Quando você adicionar o componente [!UICONTROL Dynamic Media] e as **[!UICONTROL Configurações do Dynamic Media]** estiver em branco ou não puder adicionar um ativo corretamente, verifique o seguinte:
>
>* Você habilitou o [Dynamic Media](/help/assets/config-dynamic.md). O Dynamic Media está desativado por padrão.
>* A imagem tem um arquivo TIFF de pirâmide. As imagens importadas antes da ativação do Dynamic Media não têm um arquivo TIFF em pirâmide.
>

#### Ao trabalhar com imagens {#when-working-with-images}

O componente [!UICONTROL Dynamic Media] permite adicionar imagens dinâmicas, incluindo conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista. Você pode ampliar, reduzir e, se aplicável, girar uma imagem em um conjunto de rotação ou selecionar uma imagem de outro tipo de conjunto.

Também é possível configurar a predefinição do visualizador, a predefinição da imagem ou o formato da imagem diretamente no componente. Para tornar uma imagem responsiva, você pode definir os pontos de interrupção ou aplicar uma predefinição de imagem responsiva.

![chlimage_1-72](assets/chlimage_1-72a.png)

Você pode editar as seguintes configurações do Dynamic Media clicando em **[!UICONTROL Editar]** no componente e depois na guia **[!UICONTROL Configurações do Dynamic Media]**.

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>Por padrão, o componente de imagem do Dynamic Media é adaptável. Se quiser torná-lo de um tamanho fixo, defina-o no componente na guia **[!UICONTROL Avançado]** com as propriedades **[!UICONTROL Largura]** e **[!UICONTROL Altura]**.

**[!UICONTROL Predefinição do visualizador]** - Selecione uma predefinição do visualizador existente no menu suspenso. Se a predefinição do visualizador que você está procurando não estiver visível, é necessário torná-la visível. Consulte [Gerenciamento de Predefinições do Visualizador](/help/assets/managing-viewer-presets.md). Não é possível selecionar uma predefinição do visualizador se você estiver usando uma predefinição de imagem e vice-versa.

Essa opção só estará disponível se você exibir conjuntos de imagens, conjuntos de rotação ou conjuntos de mídia mista. As predefinições do visualizador exibidas são inteligentes. Ou seja, somente as predefinições relevantes do visualizador são exibidas.

**[!UICONTROL Predefinição de imagem]** - Selecione uma predefinição de imagem existente no menu suspenso. Se a predefinição de imagem que você está procurando não estiver visível, será necessário torná-la visível. Consulte [Gerenciamento de Predefinições de Imagem](/help/assets/managing-image-presets.md). Não é possível selecionar uma predefinição do visualizador se você estiver usando uma predefinição de imagem e vice-versa.

Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mídia mista.

**[!UICONTROL Modificadores de Imagem]** - Você pode alterar efeitos de imagem fornecendo comandos de imagem adicionais. Estes comandos estão descritos em [Gerenciando Predefinições de Imagem](/help/assets/managing-viewer-presets.md) e na [Referência de Comando](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=pt-BR).

Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mídia mista.

**[!UICONTROL Pontos de interrupção]** - Se estiver usando este ativo em um site responsivo, você deve adicionar os pontos de interrupção da página. Os pontos de interrupção da imagem são separados por vírgulas (,). Essa opção funciona quando não há altura ou largura definidas em uma predefinição de imagem.

Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mídia mista.

Você pode editar as [!UICONTROL Configurações avançadas] a seguir clicando em **[!UICONTROL Editar]** no componente.

**[!UICONTROL Título]** - Alterar o título da imagem.

**[!UICONTROL Texto Alternativo]** - Adicione um título à imagem para os usuários que têm gráficos desativados.

Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mídia mista.

**[!UICONTROL URL, Abrir em]** - Você pode definir um ativo de para abrir um link. Defina o **[!UICONTROL URL]** e o **[!UICONTROL Abrir em]** para indicar se você deseja que ele seja aberto na mesma janela ou em uma nova janela.

Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mídia mista.

**[!UICONTROL Largura e Altura]** - Insira o valor em pixels se desejar que a imagem seja de tamanho fixo. Deixar esses valores em branco torna o ativo adaptável.

#### Ao trabalhar com vídeo {#when-working-with-video}

Use o componente **[!UICONTROL Dynamic Media]** para adicionar vídeo dinâmico às suas páginas da Web. Ao editar o componente, você pode optar por usar uma predefinição predefinida do visualizador de vídeo para reproduzir o vídeo na página.

![chlimage_1-74](assets/chlimage_1-74a.png)

Você pode editar as [!UICONTROL Configurações do Dynamic Media] a seguir clicando em **[!UICONTROL Editar]** no componente.

>[!NOTE]
>
>Por padrão, o componente de vídeo do Dynamic Media é adaptável. Se quiser torná-lo de um tamanho fixo, defina-o no componente com a **[!UICONTROL Largura]** e a **[!UICONTROL Altura]** na guia **[!UICONTROL Avançado]**.

**[!UICONTROL Predefinição do visualizador]** - Selecione uma predefinição do visualizador de vídeo existente no menu suspenso. Se a predefinição do visualizador que você está procurando não estiver visível, é necessário torná-la visível. Consulte [Gerenciamento de Predefinições do Visualizador](/help/assets/managing-viewer-presets.md).

Você pode editar as seguintes configurações [!UICONTROL Avançadas] clicando em **[!UICONTROL Editar]** no componente.

**[!UICONTROL Título]** - Alterar o título do vídeo.

**[!UICONTROL Largura e Altura]** - Insira o valor em pixels se desejar que o vídeo seja de tamanho fixo. Deixar esses valores em branco o torna adaptável.

#### Fornecer vídeo seguro {#how-to-delivery-secure-video}

No Experience Manager 6.2, ao instalar o [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480), você pode controlar se um vídeo é entregue por uma conexão SSL segura (HTTPS) ou por uma conexão insegura (HTTP). Por padrão, o protocolo de entrega de vídeo é herdado automaticamente do protocolo da página da Web de incorporação. Se a página da Web for carregada por HTTPS, o vídeo também será entregue por HTTPS. E, por outro lado, se a página da Web estiver em HTTP, o vídeo será entregue via HTTP. Normalmente, esse comportamento padrão é adequado e não há necessidade de fazer alterações na configuração. No entanto, é possível substituir esse comportamento padrão. Anexe `VideoPlayer.ssl=on` ao final de um caminho de URL ou à lista de outros parâmetros de configuração do visualizador em um trecho de código incorporado. Qualquer ação força a entrega segura do vídeo.

Para obter mais informações sobre a entrega segura de vídeo e o uso do atributo de configuração `VideoPlayer.ssl` no caminho da URL, consulte [Entrega segura de vídeo](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html?lang=pt-BR) no Guia de Referência de Visualizadores. Além do visualizador de vídeo, a entrega segura de vídeo está disponível para o visualizador de Mídia mista e o visualizador de Vídeo interativo.

### Componente de mídia interativa {#interactive-media-component}

O componente de Mídia interativa é para os ativos que têm interatividade, como pontos de acesso ou mapas de imagem. Se você tiver uma imagem interativa, vídeo interativo ou banner de carrossel, use o componente **[!UICONTROL Mídia interativa]**.

O componente de [!UICONTROL Mídia interativa] é inteligente - você tem várias opções, dependendo de adicionar uma imagem ou um vídeo. Além disso, o visualizador é responsivo. Ou seja, o tamanho da tela muda automaticamente com base no tamanho da tela. Todos os visualizadores são baseados em HTML5.

![chlimage_1-75](assets/chlimage_1-75a.png)

Você pode editar as seguintes configurações de **[!UICONTROL Geral]** clicando em **[!UICONTROL Editar]** no componente.

**[!UICONTROL Predefinição do visualizador]** - Selecione uma predefinição do visualizador existente no menu suspenso. Se a predefinição do visualizador que você está procurando não estiver visível, é necessário torná-la visível. As predefinições do visualizador devem ser publicadas antes de serem usadas. Consulte [Gerenciar predefinições do visualizador](/help/assets/managing-viewer-presets.md).

**[!UICONTROL Título]** - Alterar o título do vídeo.

**[!UICONTROL Largura e Altura]** - Insira o valor em pixels se desejar que o vídeo seja de tamanho fixo. Deixar esses valores em branco o torna adaptável.

Você pode editar as seguintes configurações de **[!UICONTROL Adicionar ao carrinho]** clicando em **[!UICONTROL Editar]** no componente.

**[!UICONTROL Mostrar ativo de produto]** - Por padrão, este valor está selecionado. O ativo do produto mostra uma imagem do produto conforme definido no módulo Commerce. Desmarque a marca de seleção para não mostrar o ativo do produto.

**[!UICONTROL Mostrar Preço do Produto]** - Por padrão, este valor é selecionado. Preço do produto mostra o preço do item conforme definido no módulo Commerce. Desmarque a marca de seleção para não mostrar o preço do produto.

**[!UICONTROL Mostrar Formulário de Produto]** - Por padrão, esse valor não está selecionado. O Formulário de produto inclui qualquer variante de produto, como tamanho e cor. Desmarque a marca de seleção para não mostrar as grades de produtos.
