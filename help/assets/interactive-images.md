---
title: Imagens interativas
description: Saiba como trabalhar com imagens interativas no Dynamic Media
uuid: 0bdb73f7-6ce9-4cdf-b6b5-a4d3d4e19a23
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: a6f58f6a-015a-4ced-941c-ef1b6d3e1d6f
docset: aem65
feature: Interactive Images
role: User, Admin
exl-id: 8a609024-e9e6-4805-8306-48d095110eb6
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '4275'
ht-degree: 1%

---

# Imagens interativas{#interactive-images}

Você pode facilmente fazer imagens estáticas avançadas e envolventes para os clientes, arrastando e soltando pontos de acesso &quot;que podem ser comprados&quot; em uma imagem. Os hotspots que podem ser comprados combinam informações adicionais sobre um produto ou serviço com um recurso direto de &quot;Adicionar ao carrinho&quot; ou &quot;Comprar&quot; no ponto de venda. Os clientes podem selecionar esses pontos de acesso e ser vinculados diretamente ao produto ou serviço, adicioná-lo a um carrinho de compras ou ser vinculados a uma página da Web. Experiências diretas como essas aumentam os envolvimentos do cliente e as conversões no seu site.

Veja a seguir um banner que pode ser comprado com um pop-up do Quickview. Um usuário ativa o Quickview selecionando o círculo ou o &quot;ponto de acesso&quot; no modelo.

![chlimage_1-152](assets/chlimage_1-368.png)

Veja as imagens interativas em ação na página da Web acima acessando o seguinte:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html)

## Veja como os banners de imagem interativos são criados {#watch-how-interactive-image-banners-are-created}

Reproduzir uma apresentação em [como os banners de imagem interativos são criados](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner) (10 minutos e 33 segundos). Você também aprenderá a visualizar, editar e fornecer banners de imagem interativos.

## Início rápido: Imagens interativas {#quick-start-interactive-images}

A seguinte descrição passo a passo do fluxo de trabalho foi criada para ajudar você a ativar e executar rapidamente com imagens interativas no Adobe Experience Manager Assets.

Procure o **Exemplo** em algumas das tarefas do Início rápido. Ele contém um breve tutorial baseado no seguinte exemplo de página da Web que ainda não tem Imagens interativas adicionadas a ele:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

O tutorial ajuda a ilustrar as etapas da integração de imagens interativas em seu próprio site.

Etapas de imagens interativas:

1. **(Opcional) Identificar variáveis de ponto de acesso** - Se você usa o Experience Manager Assets e o Dynamic Media de forma independente, comece identificando as variáveis dinâmicas usadas na implementação existente do Quickview. Em seguida, você pode inserir dados de ponto de acesso ao criar a imagem interativa. Consulte [(Opcional) Identificar variáveis de ponto de acesso](#optional-identifying-hotspot-variables).
No entanto, se você usar o Adobe Experience Manager Sites, o Adobe Experience Manager eCommerce ou ambos, essa etapa não será necessária.
Consulte [Conceitos de comércio eletrônico no Experience Manager Assets](/help/commerce/cif-classic/administering/concepts.md).

1. **(Opcional) Criar uma predefinição do visualizador de Imagem interativa** - Personalize a imagem gráfica usada para representar pontos de acesso. Não é necessário criar sua própria predefinição do visualizador de Imagem interativa se você pretende usar a predefinição do visualizador de Imagem interativa pronta para uso chamada `Shoppable_Banner` em vez disso.
Consulte [(Opcional) Criar uma predefinição do visualizador de Imagem interativa](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset).

1. **Fazer upload de um banner de imagem** - Carregue banners de imagem que você deseja tornar interativos.
Consulte [Fazer upload de um banner de imagem](#uploading-an-image-banner).

1. **Adicionar pontos de acesso a um banner de imagem** - Adicione um ou mais pontos de acesso a um banner de imagem e associe-os a uma ação, como um hiperlink, uma visualização rápida ou um fragmento de experiência. Depois de adicionar pontos de acesso, você concluirá essa tarefa publicando a imagem interativa.

   * Consulte [Adicionar pontos de acesso a um banner de imagem](#adding-hotspots-to-an-image-banner).
   * Consulte [Visualizar imagens interativas](#optional-previewing-interactive-images) - Opcional. Se desejar, você pode visualizar uma representação do banner que pode ser comprado e testar sua interatividade.
   * Consulte [Publicar ativos](/help/assets/publishing-dynamicmedia-assets.md) para obter detalhes sobre como publicar ativos de imagem interativos.

1. **Adicionar uma imagem interativa ao seu site** - Se você usar o Experience Manager Sites, o eCommerce ou ambos, poderá adicionar a imagem interativa a uma página da Web no Experience Manager. Arraste o componente Mídia interativa para a página. Consulte [Adicionar ativos Dynamic Media às páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

   Se você usar o Experience Manager Assets e o Dynamic Media de forma independente, deverá copiar o código incorporado no seu site e integrá-lo ao seu Quickview existente. Consulte [Integrar uma imagem interativa ao seu site](#integrating-an-interactive-image-with-your-website).

   Se estiver usando um WCM de terceiros (Web Content Manager), é necessário integrar o novo vídeo interativo com a implementação existente do Quickview, usada em seu site. Consulte [Integrar uma imagem interativa a uma Quickview existente](#integrating-an-interactive-image-with-an-existing-quickview).

## (Opcional) Identificar variáveis de ponto de acesso {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>Essa tarefa só será necessária se o seguinte for verdadeiro:
>
>* Você deseja adicionar interatividade à imagem, acionando para o Quickview.
>* Sua implementação do Experience Manager faz *not* use uma estrutura de integração de eCommerce para inserir dados de produtos no Experience Manager a partir de qualquer solução de eCommerce, como IBM® WebSphere® Commerce, Elastic Path, hybris ou Intershop. Consulte [Conceitos de comércio eletrônico no Experience Manager Assets](/help/commerce/cif-classic/administering/concepts.md).
>
>Se sua implementação do Experience Manager usar o eCommerce, você poderá ignorar esta tarefa e prosseguir para a próxima tarefa.

Comece identificando as variáveis dinâmicas usadas pela implementação existente do Quickview, para que você possa inserir dados de pontos de acesso para criar a imagem interativa.

Ao adicionar pontos de acesso a uma imagem de banner no Experience Manager Assets, você deve atribuir uma SKU (Stock Keeping Unit) e variáveis adicionais opcionais a cada ponto de acesso. Essas variáveis de ponto de acesso são usadas posteriormente para corresponder pontos de acesso com conteúdo do Quickview.

É importante identificar corretamente o número e o tipo de variáveis a serem associadas aos dados do ponto de acesso. Cada ponto de acesso adicionado a uma imagem de banner deve ter informações suficientes para identificar inequivocamente o produto no sistema de back-end existente.

Há diferentes maneiras de identificar um conjunto de variáveis a serem usadas para dados de pontos de acesso.

Às vezes, basta consultar especialistas de TI responsáveis pela implementação atual do Quickview. Os especialistas em TI provavelmente saberão qual é o conjunto mínimo de dados necessário para a identificação do Quickview no sistema. No entanto, também é possível simplesmente analisar o comportamento existente do código front-end.

A maioria das implementações do Quickview usa o seguinte paradigma:

* O usuário ativa um elemento da interface do usuário no site. Por exemplo, selecionar um botão &quot;Quickview&quot;.
* O site envia uma solicitação do Ajax para o backend para carregar os dados ou o conteúdo do Quickview, se necessário.
* Os dados do Quickview são traduzidos para o conteúdo em preparação para renderização na página da Web.
* Por fim, o código front-end renderiza visualmente esse conteúdo na tela.

A abordagem é então visitar diferentes áreas do site existente, onde o recurso Quickview é implementado. Em seguida, você aciona o Quickview e captura o URL Ajax enviado pela página da Web para carregar os dados ou o conteúdo do Quickview.

Normalmente, não há necessidade de usar ferramentas de depuração especializadas. Os navegadores modernos da Web apresentam inspetores da Web que fazem um trabalho adequado. A seguir estão alguns exemplos de navegadores da Web que incluem inspetores da Web:

* Para ver todas as solicitações HTTP de saída no Google Chrome, pressione F12 para abrir o painel Ferramentas do desenvolvedor e selecione a guia Rede.
Em um Mac, pressione Command+Option+I para abrir o painel Ferramentas do desenvolvedor e selecione a guia Rede.

* No Firefox, é possível ativar o plug-in do Firebug pressionando F12 e usar a guia Rede ou usar a ferramenta Inspetor integrada e a guia Rede.
Em um Mac, pressione Command+Option+I para abrir o painel Ferramentas do desenvolvedor e selecione a guia Inspetor .

Quando o monitoramento de rede estiver ativado no navegador, acione o Quickview na página.

Agora, encontre o URL do Ajax do Quickview no log de rede e copie o URL registrado para análise futura. Geralmente, quando você aciona o Quickview, há várias solicitações que são enviadas ao servidor. Normalmente, o URL de Ajax do Quickview é um dos primeiros na lista. Ela tem uma parte ou um caminho complexo da sequência de consulta e seu tipo MIME de resposta é `text/html`, `text/xml`ou `text/javascript`.

Durante esse processo, é importante visitar diferentes áreas de seu site, com diferentes categorias e tipos de produtos. O motivo é que os URLs do Quickview podem ter partes comuns para uma determinada categoria de site, mas podem ser alteradas somente se você visitar uma área diferente do site.

No caso mais simples, a única parte variável no URL do Quickview é o SKU do produto. Nesse caso, o valor de SKU é o único dado necessário para adicionar pontos de acesso à imagem do banner.

No entanto, em casos complexos, o URL do Quickview tem elementos variáveis diferentes além do SKU, como ID da categoria, código de cor e código de tamanho. Nesses casos, cada elemento é uma variável separada na definição de dados do ponto de acesso no recurso de imagem interativa que pode ser comprada no Experience Manager Assets.

Considere os exemplos a seguir de URLs do Quickview e suas variáveis de ponto de acesso resultantes:

<table>
  <tbody>
  <tr>
    <td><p>SKU único, encontrado na string de consulta.</p> </td>
    <td><p>Os URLs do Quickview registrados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>A única parte variável no URL é o valor do parâmetro da string de consulta productId= e é claramente um valor SKU. Portanto, seus pontos de acesso precisam apenas de campos SKU preenchidos com valores como <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU único, encontrado no caminho do URL.</p> </td>
    <td><p>Os URLs do Quickview registrados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>A parte variável está na última parte do caminho e se torna o valor SKU dos pontos de acesso: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID de categoria na sequência de consulta.</p> </td>
    <td><p>Os URLs do Quickview registrados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>Nesse caso, há duas partes variáveis no URL. O SKU é armazenado no <code>prodId</code> e a ID da categoria<code></code> é armazenado no <code>category=</code> parâmetro.</p> <p>Dessa forma, as definições de ponto de acesso são pares. Ou seja, um valor SKU e uma variável extra chamada <code>categoryId</code>. Os pares resultantes são os seguintes:</p>
    <ul>
      <li><p>SKU é <strong><code>305466</code></strong> e <code>categoryId</code> é <code>1100004</code>.</p> </li>
      <li><p>SKU é <strong><code>310181</code></strong> e <code>categoryId</code> é <strong><code>1100004</code></strong>.</p> </li>
      <li><p>SKU é <strong><code>308706</code></strong> e <code>categoryId</code> é <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Exemplo**

Você pode aplicar a mesma abordagem usada nos três exemplos acima na página da Web de demonstração:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

A página da Web de demonstração tem várias miniaturas de produto, cada uma com um botão Quickview chamado &quot;Veja mais&quot;. Com a ferramenta de depuração do navegador da Web ainda ativada, selecione cada botão e observe os URLs do Quickview gravados. Depois de ativar todos os quatro produtos do Quickview disponíveis na página, você tem a seguinte lista de solicitações do Quickview feitas ao back-end:

* `/datafeed/Male-Windbreaker.json`
* `/datafeed/Male-SimpleHenley.json`
* `/datafeed/Male-CamoPullover.json`
* `/datafeed/Female-QuiltedDownJacket.json`

Ao examinar as chamadas do servidor, você verá que informações específicas do produto estão presentes somente no caminho da solicitação. Você também notará que a sequência de consulta não é usada e que há dois tipos distintos de partes de dados envolvidos:

* O primeiro tipo é masculino ou feminino. Você pode chamar esta &quot;categoria de produto&quot;.
* O segundo tipo é o nome do produto, como CamoPulover. Você pode assumir que essas informações são o SKU do produto.

Considerando essas informações, todo o URL do Quickview tem o seguinte padrão:

`/datafeed/$categoryId$-$SKU$.json`

Com base nessa análise, você usaria `categoryId` e `SKU` para pontos de conexão.

Agora você está pronto para fazer upload de um banner de imagem e adicionar pontos de acesso a ele usando o recurso de imagem interativa que pode ser comprado no Experience Manager Assets.

## (Opcional) Criar uma predefinição do visualizador de Imagem interativa {#optional-creating-an-interactive-image-viewer-preset}

Você pode optar por usar a predefinição padrão do visualizador de Imagem interativa pronta para uso chamada `Shoppable_Banner` que vem com o Experience Manager Assets. Ou você pode criar sua própria predefinição personalizada do visualizador para uso com imagens interativas.

Ao criar uma predefinição personalizada do visualizador de Imagem interativa, você pode determinar a aparência dos pontos de acesso no banner de imagem. Como parte da criação da predefinição do visualizador, você pode optar por usar um gráfico de ponto de acesso de uma galeria de imagens predefinidas.

Depois de salvar a predefinição do visualizador, ela é ativada automaticamente (ativada) na página de lista Predefinição do visualizador no Experience Manager Assets. Essa funcionalidade significa que está visível no componente Mídia interativa e sempre que você exibe um ativo. No entanto, para *delivery* um banner interativo com essa predefinição do visualizador, você deve *publicar* sua predefinição do visualizador também. Essa regra é verdadeira para predefinições do visualizador personalizadas ou predefinidas.

**Para criar uma predefinição do visualizador de Imagem interativa :**

1. No painel à esquerda, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Predefinições do visualizador]**.
1. Ao lado do canto superior direito da página, selecione **[!UICONTROL Criar]**.
1. Na caixa de diálogo Nova predefinição do visualizador, digite um nome para descrever a predefinição interativa do visualizador de banner.

   O título aparece na página de lista Predefinição do visualizador depois de salvar.

1. No menu suspenso Rich Media Type (Tipo de mídia avançada), selecione **[!UICONTROL Imagem interativa]**.
1. Selecione **[!UICONTROL Criar]**.
1. Na página Editar predefinição do visualizador , selecione o **[!UICONTROL Aparência]** guia .
1. Siga uma das seguintes opções:

   * Para carregar sua própria imagem de ponto de acesso que deseja usar nas imagens, selecione o ícone Seletor de ativos. Na página Selecionar conteúdo , navegue até a imagem do ponto de acesso que deseja usar, selecione-a e selecione o ícone Marca de seleção no canto superior direito.
   * Para selecionar uma imagem de ponto de acesso predefinida, selecione o ícone Galeria de pontos de acesso . Na paleta galeria de pontos de acesso, selecione a imagem do ponto de acesso que deseja usar.

1. Ao lado do canto superior direito da página, selecione **[!UICONTROL Salvar]**.

   Certifique-se de publicar a nova predefinição do visualizador.

   Consulte [Predefinições Do Visualizador De Publicação Que Você Adicionou](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

   Agora você está pronto para fazer upload de um banner de imagem.

## Fazer upload de um banner de imagem {#uploading-an-image-banner}

Se você já tiver carregado as imagens que deseja usar, vá para a próxima etapa, [Adicionar pontos de acesso a um banner de imagem](#adding-hotspots-to-an-image-banner).

**Para fazer upload de um banner de imagem:**

1. Carregue banners de imagem que você deseja tornar interativos.

   Consulte [Upload de ativos](/help/assets/manage-assets.md#uploading-assets).

   Agora você está pronto para adicionar pontos de acesso ao banner de imagem; consulte a próxima tarefa abaixo.

## Adicionar pontos de acesso a um banner de imagem {#adding-hotspots-to-an-image-banner}

Você pode adicionar pontos de acesso a um banner de imagem usando o editor na página Gerenciamento de pontos de acesso .

Ao adicionar pontos de acesso, você pode defini-los como uma exibição pop-up do Quickview, como um hiperlink ou um Fragmento de experiência.

Consulte [Fragmentos de experiência](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
>
>As ferramentas de compartilhamento de mídia social na Imagem interativa não são compatíveis quando você incorpora o visualizador em um Fragmento de experiência. Para contornar esse problema, você pode usar ou criar predefinições do visualizador que não tenham ferramentas de compartilhamento de redes sociais. Essas predefinições do visualizador permitem que você as incorpore com êxito aos Fragmentos de experiência.

As opções Desfazer e Refazer, próximo ao canto superior direito da página, são compatíveis durante a sessão de criação/edição atual.

Ao terminar de criar a imagem interativa, você pode usar a Visualização para ver uma representação de como a imagem interativa aparece para os clientes.

Consulte [(Opcional) Visualizar imagens interativas](#optional-previewing-interactive-images).

>[!NOTE]
>
>Quando você adiciona pontos de acesso a uma imagem em uma Imagem interativa ou em um Banner de carrossel, as informações do ponto de acesso são armazenadas no mesmo local de metadados. Esse local é relativo ao local da imagem, independentemente de ser uma Imagem interativa ou um Banner de carrossel. Essa funcionalidade significa que você pode reutilizar facilmente a mesma imagem - juntamente com seus dados de ponto de acesso definidos - em qualquer um dos visualizadores.
Os banners de carrossel são compatíveis com mapas de imagens em imagens que também podem conter pontos de acesso; Imagens interativas não. Lembre-se dessa regra se você pretende criar uma Imagem interativa ou um Banner de carrossel que use a mesma imagem. Você pode criar Imagens interativas e Banners de carrossel usando cópias separadas da mesma imagem.
Consulte também [Banners em carrossel](/help/assets/carousel-banners.md).

>[!NOTE]
Se você estiver editando imagens interativas com pontos de acesso e recortar a imagem, seus pontos de acesso serão removidos.

**Para adicionar pontos de acesso a um banner de imagem:**

1. Na exibição Ativos, navegue até o banner de imagem que deseja tornar interativo.
1. Siga uma das seguintes opções:

   * Passe o mouse sobre a imagem, em seguida selecione **[!UICONTROL Selecionar]** (ícone de marca de seleção). Na barra de ferramentas, selecione **[!UICONTROL Editar]**.

   * Passe o mouse sobre a imagem, em seguida selecione **[!UICONTROL Mais ações]** (ícone de três pontos) **[!UICONTROL Editar]**.

   * Selecione a imagem para abri-la na página Exibição detalhada . Na barra de ferramentas, selecione **[!UICONTROL Editar]**.

1. Ao lado do canto superior esquerdo da página, selecione **[!UICONTROL Adicionar ponto de acesso]** (ícone de toque com o dedo) para abrir a página Gerenciamento de pontos de acesso .
1. Ao lado do canto superior esquerdo da página, selecione **[!UICONTROL Ponto de conexão]**.

   1. Próximo ao canto superior esquerdo da página Gerenciamento de pontos de acesso, selecione **[!UICONTROL Ponto de conexão]**.
   1. Na imagem, selecione um local onde deseja que o ponto de acesso apareça. Se necessário, arraste o ponto de conexão para ajustar sua localização.
   1. Adicione outros pontos de acesso, conforme necessário, repetindo as etapas a e b.
   1. (Opcional) Para excluir um ponto de acesso, selecione-o na imagem e, em seguida, selecione **[!UICONTROL Excluir]** (ícone da lixeira) sob a **[!UICONTROL Pontos de conexão]** cabeçalho.

1. No campo de texto Nome , digite o nome do ponto de acesso. Esse nome também aparece na lista suspensa Ponto de acesso selecionado .
1. Siga uma das seguintes opções:

   * Selecionar **[!UICONTROL QuickView]**.

      * Se você for um cliente do Experience Manager Sites ou eCommerce, selecione o ícone Seletor de produto (lupa) para abrir a página Selecionar produto . Selecione o produto que deseja usar e selecione **[!UICONTROL Selecionar]** no canto superior direito da página, para que você possa retornar à página Gerenciamento de pontos de acesso .
      * Se você *not* um cliente Experience Manager Sites ou eCommerce

         * Consulte [Identificar variáveis de ponto de acesso](#optional-identifying-hotspot-variables); você deve definir essas variáveis.
         * Em seguida, insira manualmente o valor de SKU. No campo de texto Valor SKU , digite o SKU (Stock Keeping Unit) do produto, que é um identificador exclusivo para cada produto ou serviço distinto que você oferece. O valor de SKU inserido preenche automaticamente a parte variável do modelo do Quickview, de modo que o sistema saiba associar o ponto de acesso selecionado a um Quickview específico do SKU.
         * (Opcional) Se houver outras variáveis no Quickview que você deve usar para identificar ainda mais um produto, selecione **[!UICONTROL Adicionar variável genérica]**. No campo de texto, especifique uma variável extra. Por exemplo, `category=Males` é uma variável adicionada.
   * Selecionar **[!UICONTROL Hiperlink]**.

      * Se você for um cliente do Experience Manager Sites, selecione o ícone do Seletor de site (pasta) para navegar até um URL. O método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, especialmente links para páginas do Experience Manager Sites.
      * Se você for um cliente independente, no campo de texto HREF, especifique o caminho do URL completo para uma página da Web vinculada.

   Certifique-se de especificar se deseja abrir o link em uma nova guia do navegador (padrão recomendado) ou na mesma guia.

   Consulte [Trabalhar com seletores](/help/assets/working-with-selectors.md) para obter mais informações.

   * Selecionar **[!UICONTROL Fragmento de experiência]**.

      * Se você for um cliente do Experience Manager Sites, selecione o ícone de Pesquisa (lupa) para abrir a página Fragmento de experiência . Selecione o Fragmento de experiência que deseja usar e selecione **[!UICONTROL Selecionar]** no canto superior direito da página, para que você possa retornar à página Gerenciamento de pontos de acesso .
Consulte [Fragmentos de experiência](/help/sites-authoring/experience-fragments.md).

      * Especifique a largura e a altura do Fragmento de experiência da maneira que deseja que apareça no banner.

         >[!NOTE]
         As ferramentas de compartilhamento de mídia social na Imagem interativa não são compatíveis quando você incorpora o visualizador em um Fragmento de experiência. Para contornar esse problema, você pode usar ou criar predefinições do visualizador que não tenham ferramentas de compartilhamento de redes sociais. Essas predefinições do visualizador permitem que você as incorpore com êxito aos Fragmentos de experiência.



1. Selecionar **[!UICONTROL Salvar]** para salvar seu trabalho e retornar à página Procurar.
1. Publique a imagem interativa. A publicação permite que o banner seja entregue por meio da nuvem e também gera código incorporado se você precisar se integrar a um site de terceiros.

   Consulte [Publicar ativos](/help/assets/manage-assets.md#publishing-assets).

   Após adicionar pontos de acesso e publicar a imagem interativa, você estará pronto para adicioná-la ao seu site existente.

   Consulte [Integrar uma imagem interativa ao seu site](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   Se você estiver editando imagens interativas com pontos de acesso e recortar a imagem, seus pontos de acesso serão excluídos.

### (Opcional) Visualizar imagens interativas {#optional-previewing-interactive-images}

Você pode usar a Visualização para ver uma representação de como sua imagem interativa aparece para os clientes e testar os pontos de acesso da imagem para garantir que eles estejam se comportando conforme esperado.

Quando estiver satisfeito com a imagem interativa, você poderá publicá-la.
Consulte [Incorporar o visualizador de vídeo ou imagem a uma página da Web](/help/assets/embed-code.md).
Consulte [Vincular URLs ao aplicativo da Web](/help/assets/linking-urls-to-yourwebapplication.md). O método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, especialmente links para páginas do Experience Manager Sites.
Consulte [Adicionar ativos Dynamic Media às páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

**Para visualizar imagens interativas:**

1. Na exibição Ativos, navegue até uma imagem interativa existente que você criou e selecione para abri-la em Visualização.
1. Próximo ao canto superior esquerdo da página Visualização, na lista suspensa Conteúdo , selecione **[!UICONTROL Visualizadores]**.
1. Na lista Visualizadores, selecione **[!UICONTROL Shoppable_Banner]** ou o nome da predefinição interativa do visualizador de imagens que você criou.
1. Selecione pontos de acesso na imagem se desejar testar as ações associadas.

## Publicar ativos de imagem interativos {#publishing-interactive-image-assets}

Consulte [Publicar ativos](/help/assets/publishing-dynamicmedia-assets.md) para obter detalhes sobre como publicar ativos de imagem interativos.

## Integrar uma imagem interativa ao seu site {#integrating-an-interactive-image-with-your-website}

Após carregar uma imagem de banner, adicionar pontos de acesso à imagem e publicar a imagem interativa, você estará pronto para adicioná-la à página do site.

Se você for um cliente do Experience Manager Sites, é possível adicionar a imagem interativa, arrastando o componente Mídia interativa para a página. Consulte [Adicionar ativos Dynamic Media às páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

Se você for um cliente independente do Experience Manager Assets, poderá adicionar manualmente a imagem interativa ao seu site, conforme descrito nesta seção.

1. Copie o código incorporado da imagem interativa publicada.
Consulte [Incorporar o visualizador de vídeo ou imagem a uma página da Web](/help/assets/embed-code.md).

1. Adicione o código incorporado copiado no local desejado na página da Web.
O código incorporado copiado é definido para um ambiente responsivo para que ele se ajuste automaticamente à área atribuída.

**Exemplo**

Usando o site de demonstração como exemplo:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

Observe que a imagem dos três machos é estática `IMG` tag:

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

A integração é tão simples quanto remover a `IMG` e substituí-la pelo código incorporado copiado do Experience Manager Assets. Você pode ver o resultado no seguinte URL que mostra a imagem interativa que pode ser comprada na página com três pontos de acesso de círculo:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html)

>[!NOTE]
Como este ponto, os pontos de acesso na imagem interativa que pode ser comprada do site de demonstração são somente para fins de exibição; eles ainda não estão integrados ao Quickview existente.

Para aplicar um &quot;recorte&quot; a uma imagem interativa que pode ser comprada em um ambiente responsivo, você pode incluir o atributo de configuração Imagem interativa `ZoomView.iscommand` para o caminho. O componente `ZoomView` é chamado de e `iscommand` é o comando de veiculação de imagens &quot;cortar&quot; aplicado.

Consulte [ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html) atributo de configuração.

Consulte [cultura](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html) comando de veiculação de imagens.

Agora você está pronto para integrar a imagem interativa com uma exibição rápida existente no seu site.

## Integrar uma imagem interativa a uma Quickview existente {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
Essa tarefa só se aplica se você for um cliente independente do Experience Manager Assets.

A última etapa desse processo é integrar a imagem interativa a uma implementação existente do Quickview em seu site. Não há solução para a integração que funcione para todos os casos. Cada implementação do Quickview é exclusiva e uma abordagem específica é necessária. Isso provavelmente envolve a assistência de uma pessoa de TI front-end.

A implementação existente do Quickview normalmente representa uma cadeia de ações inter-relacionadas que ocorrem na página da Web na seguinte ordem:

1. Um usuário aciona um elemento na interface do usuário do site.
1. O código front-end obtém um URL do Quickview com base no elemento da interface do usuário acionado na etapa 1.
1. O código de front-end envia uma solicitação Ajax usando o URL obtido na etapa 2.
1. A lógica de back-end retorna os dados ou o conteúdo correspondentes do Quickview de volta ao código de front-end.
1. O código front-end carrega os dados ou o conteúdo do Quickview.
1. Opcionalmente, o código front-end converte os dados do Quickview carregados em uma representação de HTML.
1. O código front-end exibe uma caixa de diálogo ou painel modal e renderiza o conteúdo do HTML na tela do usuário final.

Essas chamadas não representam chamadas de API públicas independentes que podem ser chamadas pela lógica da página da Web de uma etapa arbitrária. Em vez disso, é uma chamada encadeada em que cada próxima etapa está oculta na última fase (retorno de chamada) da etapa anterior.

Ao mesmo tempo em que a imagem interativa que pode ser comprada está substituindo a etapa 1 e parcialmente a etapa 2, em que um usuário seleciona um ponto de acesso dentro da imagem que pode ser comprada, essa interação do usuário é tratada pelo visualizador. O visualizador retorna um evento para a página da Web que contém todos os dados de ponto de acesso adicionados anteriormente ao Experience Manager Assets.

Nesse manipulador de evento, o código front-end faz o seguinte:

* Escuta um evento emitido pela imagem interativa que pode ser comprada.
* Constrói um URL do Quickview com base nos dados do ponto de acesso.
* Aciona o processo de carregamento do Quickview a partir do back-end e renderização na tela para exibição.

O código incorporado retornado pelo Experience Manager Assets já tem um manipulador de eventos pronto para uso no local, que é comentado, como visto no seguinte trecho de código destacado:

```xml
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : {
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/",
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you will need to add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //Please refer to your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

Portanto, é necessário remover o comentário do código e substituir o corpo do manipulador de teste pelo código específico da página da Web em particular.

O processo de construção do URL do Quickview é oposto do processo usado para identificar variáveis de ponto de acesso abordadas anteriormente.

Consulte [Identificar variáveis de ponto de acesso](#optional-identifying-hotspot-variables).

Usando os exemplos de URL do Quickview anteriores, você pode ver nos exemplos a seguir como o URL do Quickview é construído em cada caso:

<table>
 <tbody>
  <tr>
   <td><p>SKU único, encontrado na sequência de consulta</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU único, encontrado no caminho do URL</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU e ID de categoria na sequência de consulta</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

A última etapa para acionar o URL do Quickview e ativar o painel do Quickview provavelmente requer a assistência de uma pessoa de TI front-end do seu departamento de TI. Eles têm o conhecimento de saber mais sobre como acionar com precisão a implementação do Quickview a partir da etapa adequada, tendo um URL Quickview pronto para uso.

Você pode ver como essas etapas são aplicadas ao site de demonstração para integrar totalmente uma imagem interativa que pode ser comprada com o código do Quickview. Anteriormente, a estrutura do URL do Quickview era identificada como a seguinte:

```xml
/datafeed/$categoryId$-$SKU$.json
```

Para reconstruir esse URL dentro do `quickViewActivate` manipulador, você pode usar o `categoryId` e `SKU` campos disponíveis na `inData` objeto passado ao manipulador pelo código do visualizador:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

O site de demonstração está acionando a caixa de diálogo do Quickview com um `loadQuickView()` chamada de função. Essa função utiliza apenas um argumento, que é o URL dos dados do Quickview. Dessa forma, a última etapa para integrar a imagem interativa que pode ser comprada é adicionar a seguinte linha de código ao `quickViewActivate` manipulador:

```xml
loadQuickView(quickViewUrl);
```

Este é o código-fonte completo:

```xml
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : {
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   });
 s7interactiveimageviewer.init();
```

O site de demonstração final com a imagem interativa totalmente integrada tem a seguinte aparência:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html)

## Usar o Quickview para criar pop-ups personalizados {#using-quickviews-to-create-custom-pop-ups}

Consulte [Criar pop-ups personalizados usando o Quickview](/help/assets/custom-pop-ups.md).
