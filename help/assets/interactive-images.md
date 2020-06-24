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
translation-type: tm+mt
source-git-commit: 5015a55b79d363a8b7364f154921e956a818ce19
workflow-type: tm+mt
source-wordcount: '4345'
ht-degree: 2%

---


# Imagens interativas{#interactive-images}

Você pode facilmente tornar as imagens estáticas excelentes e envolventes experiências para os clientes, arrastando e soltando pontos de conexão &quot;compráveis&quot; em uma imagem. Os hotspots que podem ser comprados combinam informações adicionais sobre um produto ou serviço com um recurso direto de &quot;Adicionar ao carrinho&quot; ou &quot;Comprar&quot; no ponto de venda. Os clientes podem tocar ou clicar nesses pontos de acesso e ser vinculados diretamente ao produto ou serviço, adicioná-lo a um carrinho de compras ou ser vinculados a uma página da Web. Experiências diretas, como essas, aumentam o envolvimento e a conversão do cliente em seu site.

A seguir está um banner que pode ser comprado com um pop-up do Quickview. Um usuário ativa o Quickview tocando no círculo ou no &quot;ponto de acesso&quot; no modelo.

![chlimage_1-152](assets/chlimage_1-368.png)

Consulte as imagens interativas em ação na página da Web acima, acessando o seguinte:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html)

## Veja como os banners de imagem interativos são criados {#watch-how-interactive-image-banners-are-created}

Watch a 10 minute and 33 second walkthrough on [how interactive image banners are created](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner). Você também aprenderá a pré-visualização, edição e fornecimento de banners de imagem interativos.

## Start rápido: Imagens interativas {#quick-start-interactive-images}

A seguinte descrição passo a passo do fluxo de trabalho foi projetada para ajudá-lo a iniciar e executar rapidamente com imagens interativas em AEM Assets.

Procure o cabeçalho **Exemplo** em algumas tarefas do Start rápido. Ele contém um breve tutorial baseado no seguinte exemplo de página da Web que ainda não tem Imagens interativas adicionadas a ele:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

O tutorial ajuda a ilustrar as etapas da integração de imagens interativas em seu próprio site.

Etapas de imagens interativas:

1. **(Opcional) Identificação de variáveis** de hotspots - se você usar AEM Assets e Dynamic Media separadamente, start identificando as variáveis dinâmicas usadas na implementação do Quickview existente para que você possa digitar dados de hotspots ao criar a imagem interativa. Consulte [(Opcional) Identificação de variáveis](#optional-identifying-hotspot-variables)de pontos de conexão.
No entanto, se você usar o AEM Sites, o eCommerce do AEM ou ambos, essa etapa não será necessária.
Consulte Conceitos de [eCommerce em AEM Assets](/help/sites-administering/concepts.md).

1. **(Opcional) Criação de uma predefinição** do visualizador de Imagem interativa - Personalize a imagem gráfica usada para representar pontos de acesso. A criação de sua própria predefinição do visualizador de Imagem interativa não é necessária se você pretende usar a predefinição do visualizador de Imagem interativa predefinida chamada `Shoppable_Banner` .
Consulte [(Opcional) Criação de uma predefinição](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset)do visualizador de Imagem interativa.

1. **Carregar um banner** de imagem - Carregue banners de imagem que você deseja tornar interativos.
Consulte [Carregar um banner](#uploading-an-image-banner)de imagem.

1. **Adicionar pontos de acesso a um banner** de imagem - Adicione um ou mais pontos de acesso a um banner de imagem e associe cada um a uma ação, como um hiperlink, uma visualização rápida ou um fragmento de experiência. Depois de adicionar pontos de acesso, você concluirá essa tarefa publicando a imagem interativa.

   * Consulte [Adicionar pontos de acesso a um banner](#adding-hotspots-to-an-image-banner)de imagem.
   * Consulte [Visualizar imagens](#optional-previewing-interactive-images) interativas - Opcional. Se desejar, você pode visualização uma representação do banner que pode ser comprado e testar sua interatividade.
   * Consulte [Publicação de ativos](/help/assets/publishing-dynamicmedia-assets.md) para obter detalhes sobre como publicar ativos de imagem interativos.

1. **Adicionando uma imagem interativa ao seu site ou ao seu site no AEM** Se você usar o AEM Sites, o eCommerce do AEM ou ambos, poderá adicionar a imagem interativa diretamente a uma página da Web no AEM arrastando o componente de Mídia interativa para a página. See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)
Se você usar o AEM Assets e o Dynamic Media de forma independente, é necessário copiar o código incorporado em seu site e, em seguida, integrá-lo ao seu Quickview existente. Consulte [Integrar uma imagem interativa ao seu site](#integrating-an-interactive-image-with-your-website).
Se você estiver usando um WCM de terceiros (Web Content Manager), é necessário integrar o novo vídeo interativo com a implementação existente do Quickview usada em seu site. Consulte [Integração de uma imagem interativa com uma exibição rápida](#integrating-an-interactive-image-with-an-existing-quickview)existente.

## (Opcional) Identificação de variáveis de hotspots {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>Essa tarefa só é necessária se as seguintes condições forem verdadeiras:
>
>* Você deseja adicionar interatividade à sua imagem, acionando para o Quickviews.
>* Sua implementação do AEM *não* usa uma estrutura de integração de comércio eletrônico para extrair dados de produtos para o AEM de qualquer solução de comércio eletrônico como IBM Webphere Commerce, Elastic Path, hybris ou Intershop. Consulte Conceitos de [eCommerce em AEM Assets](/help/sites-administering/concepts.md).
>
>
Se sua implementação do AEM usar o eCommerce, você poderá ignorar essa tarefa e ir para a próxima tarefa.

Start identificando variáveis dinâmicas usadas pela implementação do Quickview existente para que você possa digitar dados de ponto de acesso para criar a imagem interativa.

Quando você adiciona pontos de acesso a uma imagem de banner no AEM Assets, é necessário atribuir um SKU (Stock Keeping Unit; Unidade de manutenção de estoque); um identificador exclusivo para cada produto ou serviço distinto que você oferta) e variáveis adicionais opcionais para cada ponto de conexão. Essas variáveis de ponto de conexão são usadas posteriormente para corresponder a pontos de conexão com conteúdo do Quickview.

É importante identificar corretamente o número e o tipo de variáveis a serem associadas aos dados dos pontos de conexão. Cada ponto de conexão adicionado a uma imagem de banner deve ter informações suficientes para identificar inequivocamente o produto no sistema de backend existente.

Há diferentes maneiras de identificar um conjunto de variáveis a serem usadas para dados de pontos de conexão.

Às vezes, pode ser suficiente consultar especialistas de TI responsáveis pela implementação atual do Quickview, já que eles provavelmente saberão qual é o conjunto mínimo de dados necessário para identificar o Quickview no sistema. No entanto, na maioria dos casos, é possível simplesmente analisar o comportamento existente do código front-end.

A maioria das implementações do Quickview usa o seguinte paradigma:

* O usuário ativa um elemento da interface do usuário no site. Por exemplo, clicar em um botão &quot;Quickview&quot;.
* O site envia uma solicitação do Ajax para o backend para carregar os dados ou o conteúdo do Quickview, se necessário.
* Os dados do Quickview são traduzidos para o conteúdo em preparação para renderização na página da Web.
* Por fim, o código front-end exibe visualmente esse conteúdo na tela.

A abordagem então é visitar diferentes áreas do site existente onde o recurso Quickview é implementado, acionar o Quickview e capturar o URL Ajax enviado por página da Web para carregar os dados ou o conteúdo do Quickview.

Normalmente, não é necessário usar nenhuma ferramenta de depuração especializada. Os navegadores da Web modernos dispõem de inspetores da Web que fazem um trabalho adequado. A seguir estão alguns exemplos de navegadores da Web que incluem inspetores da Web:

* Para ver todas as solicitações HTTP de saída no Google Chrome, pressione F12 para abrir o painel Ferramentas do desenvolvedor e clique na guia Rede.
No Mac, pressione Command+Option+I para abrir o painel Ferramentas do desenvolvedor e clique na guia Rede.

* No Firefox, você pode ativar o plug-in Firebug pressionando a tecla F12 e usando a guia Rede, ou usar a ferramenta Inspetor integrada e a guia Rede.
No Mac, pressione Command+Option+I para abrir o painel Ferramentas do desenvolvedor e clique na guia Inspetor.

Quando o monitoramento de rede estiver ativado no navegador, dispare o Quickview na página.

Agora, encontre o URL Ajax do Quickview no registro de rede e copie o URL gravado para análise futura. Na maioria dos casos, quando você aciona o Quickview, há várias solicitações que são enviadas para o servidor. Normalmente, o URL do Ajax do Quickview é um dos primeiros na lista. Ele tem uma parte ou um caminho de sequência de query complexo, e seu tipo MIME de resposta é `text/html`, `text/xml`ou `text/javascript`.

Durante esse processo, é importante visitar diferentes áreas do seu site, com diferentes categorias e tipos de produtos. O motivo é que os URLs do Quickview podem ter partes comuns para uma determinada categoria do site, mas são alterados somente se você visitar uma área diferente do site.

No caso mais simples, a única parte variável no URL do Quickview é o SKU do produto. Nesse caso, o valor SKU é o único dado necessário para adicionar pontos de acesso à imagem do banner.

No entanto, em casos complexos, o URL do Quickview tem diferentes elementos variáveis além do SKU, como ID da categoria, código de cor, código de tamanho e assim por diante. Nesses casos, cada elemento é uma variável separada na definição de dados do ponto de acesso no recurso de imagem interativa que pode ser comprado no AEM Assets.

Considere os seguintes exemplos de URLs do Quickview e suas variáveis de ponto de acesso resultantes:

<table>
  <tbody>
  <tr>
    <td><p>SKU único, encontrado na string do query.</p> </td>
    <td><p>Os URLs de exibição rápida gravados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>A única parte variável no URL é o valor do parâmetro da string de query productId= e é claramente um valor SKU. Portanto, nossos pontos de conexão precisam apenas de campos SKU preenchidos com valores como <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU único, encontrado no caminho do URL.</p> </td>
    <td><p>Os URLs de exibição rápida gravados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>A parte variável está na última parte do caminho e se torna o valor SKU dos pontos de acesso: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID da categoria na sequência do query.</p> </td>
    <td><p>Os URLs de exibição rápida gravados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>Nesse caso, há duas partes diferentes no URL. O SKU é armazenado no <code>prodId</code> parâmetro e a ID<code></code> da categoria é armazenada no <code>category=</code> parâmetro.</p> <p>Dessa forma, as definições dos pontos de conexão são pares. Ou seja, um valor de SKU e uma variável adicional chamada <code>categoryId</code>. Os pares resultantes são os seguintes:</p>
    <ul>
      <li><p>SKU é <strong><code>305466</code></strong> e <code>categoryId</code> é <code>1100004</code>.</p> </li>
      <li><p>SKU é <strong><code>310181</code></strong> e <code>categoryId</code> é <strong><code>1100004</code></strong>.</p> </li>
      <li><p>SKU é <strong><code>308706</code></strong> e <code>categoryId</code> é <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Exemplo**

Você pode aplicar a mesma abordagem usada nos três exemplos acima à página de demonstração da Web:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

A página da Web de demonstração tem várias miniaturas de produtos, cada uma com um botão do Quickview chamado &quot;Ver mais&quot;. Com a ferramenta de depuração do navegador da Web ainda ativada, clique em cada botão e observe os URLs de exibição rápida gravados. Após ativar as quatro exibições rápidas de produtos disponíveis na página, você terá a seguinte lista de solicitações do Quickview feitas ao backend:

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

Olhando para essas chamadas de servidor, você verá que informações específicas do produto estão presentes apenas no caminho da solicitação. Você também observa que a sequência de caracteres do query não é usada e que há dois tipos distintos de partes de dados envolvidas:

* O primeiro tipo é Homens ou Mulheres. Você pode chamar isso de &quot;categoria do produto&quot;.
* O segundo tipo é o nome do produto, como CamoPullover. Você pode supor que este é o SKU do produto.

Considerando essas informações, todo o URL do Quickview tem o seguinte padrão:

`/datafeed/$categoryId$-$SKU$.json`

Com base nessa análise, você usaria `categoryId` e `SKU` para pontos de conexão.

Agora você está pronto para carregar um banner de imagem e adicionar pontos de acesso a ele usando o recurso de imagem interativa que pode ser comprado no AEM Assets.

## (Opcional) Criação de uma predefinição do visualizador de imagens interativas {#optional-creating-an-interactive-image-viewer-preset}

Você pode optar por usar a predefinição padrão do visualizador de Imagem interativa, pronta para uso, chamada `Shoppable_Banner` que acompanha os AEM Assets. Ou você pode criar sua própria predefinição do visualizador personalizado para usar com imagens interativas.

Ao criar uma predefinição personalizada do visualizador de Imagem interativa, você pode determinar a aparência dos pontos de acesso no banner de imagem. Como parte da criação da predefinição do visualizador, você pode optar por usar um gráfico de ponto de acesso de uma galeria de imagens predefinidas.

Depois de salvar a predefinição do visualizador, ela é ativada automaticamente (ativada) na página lista predefinida do visualizador em AEM Assets. Essa funcionalidade significa que é visível no componente de Mídia interativa e sempre que você visualização um ativo. No entanto, para *fornecer *um banner interativo com essa predefinição do visualizador, você também deve *publicar *sua predefinição do visualizador (isso vale para predefinições personalizadas ou não).

**Para criar uma predefinição do visualizador de Imagem interativa**

1. No painel esquerdo, toque em **[!UICONTROL Ferramentas > Ativos > Predefinições do visualizador.]**
1. Near the upper-right corner of the page, tap **[!UICONTROL Create.]**
1. Na caixa de diálogo Nova predefinição do visualizador, digite um nome para descrever a predefinição do visualizador de banner interativo.

   Esse é o título que aparecerá na página lista do Viewer Preset depois que você salvar.

1. No menu suspenso Rich Media Type (Tipo de mídia avançada), selecione **[!UICONTROL Imagem interativa.]**
1. Toque em **[!UICONTROL Criar.]**
1. On the Edit Viewer Preset page, tap the **[!UICONTROL Appearance]** tab.
1. Faça uma das seguintes opções:

   * Para carregar sua própria imagem de ponto de acesso que você deseja usar nas imagens, toque no ícone Seletor de ativos. Na página Selecionar conteúdo, navegue até a imagem do ponto de acesso que deseja usar, selecione-a e toque no ícone Marcar no canto superior direito.
   * Para selecionar uma imagem de ponto de acesso predefinida, toque no ícone Galeria de pontos de acesso. Na paleta da galeria do ponto de acesso, toque na imagem do ponto de acesso que deseja usar.

1. Near the upper-right corner of the page, tap **[!UICONTROL Save.]**

   Certifique-se de publicar a nova predefinição do visualizador.

   Consulte Predefinições [Do Visualizador De Publicação Adicionadas](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

   Agora você está pronto para carregar um banner de imagem.

## Fazer upload de um banner de imagem {#uploading-an-image-banner}

Se você já tiver carregado as imagens que deseja usar, vá para a próxima etapa, [Adicionando pontos de acesso a um banner](#adding-hotspots-to-an-image-banner)de imagem.

**Para carregar um banner de imagem**

1. Faça upload de banners de imagem que deseja tornar interativos.

   See [Uploading assets](/help/assets/managing-assets-touch-ui.md#uploading-assets).

   Agora você está pronto para adicionar pontos de acesso ao banner de imagem; veja a próxima tarefa abaixo.

## Adicionar pontos de acesso a um banner de imagem {#adding-hotspots-to-an-image-banner}

Você pode adicionar pontos de acesso a um banner de imagem usando o editor na página Gerenciamento de pontos de conexão.

Ao adicionar pontos de acesso, você pode defini-los como uma exibição pop-up do Quickview, como um hiperlink ou um Fragmento de experiência.

Consulte Fragmentos [de experiência](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
>
>Observe que as ferramentas de compartilhamento de mídia social na Imagem interativa não são suportadas quando você incorpora o visualizador em um Fragmento de experiência. Para contornar isso, você pode usar ou criar predefinições do visualizador que não tenham ferramentas de compartilhamento de mídia social. Essas predefinições do visualizador permitem que você as incorpore com êxito aos Fragmentos de experiência.

As opções Desfazer e Refazer, perto do canto superior direito da página, são suportadas durante a sessão atual de criação/edição.

Ao terminar de criar sua imagem interativa, você pode usar a Pré-visualização para ver uma representação de como sua imagem interativa aparecerá para os clientes.

Consulte [(Opcional) Visualização de imagens](#optional-previewing-interactive-images)interativas.

>[!NOTE]
>
>Quando você adiciona pontos de acesso a uma imagem em uma imagem interativa ou em um banner de carrossel, as informações do ponto de acesso são armazenadas no mesmo local de metadados (relativo ao local da imagem), independentemente de se tratar de uma imagem interativa ou de um banner de carrossel. Essa funcionalidade significa que você pode reutilizar facilmente a mesma imagem, juntamente com seus dados de ponto de conexão definidos, em qualquer um dos visualizadores.

>Esteja ciente, no entanto, de que os Carousel Banners oferecem suporte para mapas de imagem em imagens que também podem conter pontos de conexão; uma imagem interativa não. Lembre-se disso se você pretende criar uma imagem interativa ou um banner de carrossel que use a mesma imagem. Você pode criar Imagens interativas e Banners de carrossel usando cópias separadas da mesma imagem.
>
>Consulte também [Carrossel Banners](/help/assets/carousel-banners.md).

>[!NOTE]
>
>Se você estiver editando imagens interativas com pontos de acesso e recortar a imagem, seus pontos de acesso serão removidos.

**Para adicionar pontos de acesso a um banner de imagem**

1. Na visualização Ativos, navegue até o banner de imagem que deseja tornar interativo.
1. Faça uma das seguintes opções:

   * Hover on the image, then tap **[!UICONTROL Select]** (checkmark icon). Na barra de ferramentas, toque em **[!UICONTROL Editar.]**

   * Passe o mouse sobre a imagem e toque em **[!UICONTROL Mais ações]** (ícone de três pontos) **[!UICONTROL > Editar.]**

   * Toque na imagem para abri-la na página Visualização Detalhe. Na barra de ferramentas, toque em **[!UICONTROL Editar.]**

1. Próximo ao canto superior esquerdo da página, toque em **[!UICONTROL Adicionar ponto de acesso]** (ícone de toque com o dedo) para abrir a página Gerenciamento de ponto de acesso.
1. Near the upper-left corner of the page, tap **[!UICONTROL Hotspot.]**

1. Perto do canto superior esquerdo da página Gerenciamento de hotspots, toque em **[!UICONTROL Hotspot.]**
1.  Na imagem, toque em um local onde deseja que o ponto de acesso apareça. Se necessário, arraste o ponto de conexão para ajustar sua localização.
1. Adicione outros pontos de conexão, conforme necessário, repetindo as etapas a e b.
1. (Opcional) Para excluir um ponto de acesso, selecione-o na imagem e toque em **[!UICONTROL Excluir]** (ícone de lixeira) no cabeçalho **[!UICONTROL Pontos de acesso]** .

1. No campo de texto Nome, digite o nome do ponto de acesso. Esse nome também aparece na lista suspensa Ponto de acesso selecionado.
1. Faça uma das seguintes opções:

   * Toque em **[!UICONTROL Quickview.]**

      * Se você for um cliente do AEM Sites ou eCommerce, toque ou clique no ícone do Seletor de produto (lupa) para abrir a página Selecionar produto. Toque ou clique no produto que deseja usar e, em seguida, toque em **Select **no canto superior direito da página para retornar à página de gerenciamento de Hotspot.
      * Se você *não* for um cliente de AEM Sites ou eCommerce

         * Consulte [Identificação de variáveis](#optional-identifying-hotspot-variables)de pontos de conexão; será necessário definir essas variáveis.
         * Em seguida, insira manualmente o valor SKU. No campo de texto Valor SKU, digite o SKU do produto (Stock Keeping Unit), que é um identificador exclusivo para cada produto ou serviço distinto que você oferta. O valor SKU inserido preenche automaticamente a parte variável do modelo do Quickview, de modo que o sistema saiba associar o ponto de acesso tocado a uma exibição rápida do SKU.
         * (Opcional) Se houver outras variáveis na exibição Rápida que você precisa usar para identificar ainda mais um produto, toque em **[!UICONTROL Adicionar variável genérica.]** No campo de texto, especifique uma variável adicional. Por exemplo, `category=Mens` é uma variável adicionada.
   * Toque em **[!UICONTROL Hiperlink.]**

      * Se você for um cliente do AEM Sites, toque ou clique no ícone Seletor de site (pasta) para navegar até um URL. Observe que o método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas de AEM Sites.
      * Se você for um cliente independente, no campo de texto HREF, especifique o caminho do URL completo para uma página da Web vinculada.
   Certifique-se de especificar se deseja abrir o link em uma nova guia do navegador (padrão recomendado) ou na mesma guia.

   Consulte [Trabalhar com seletores](/help/assets/working-with-selectors.md) para obter mais informações.

   * Tap **[!UICONTROL Experience Fragment.]**

      * Se você for um cliente do AEM Sites, toque ou clique no ícone Pesquisar (lupa) para abrir a página Fragmento de experiência. Toque ou clique no Fragmento de experiência que você deseja usar e, em seguida, toque em Selecionar no canto superior direito da página para retornar à página de gerenciamento do Hotspot.
Consulte Fragmentos [de experiência](/help/sites-authoring/experience-fragments.md).

      * Especifique a largura e a altura do Fragmento de experiência como ele aparecerá no banner.

         >[!NOTE]
         >
         >Observe que as ferramentas de compartilhamento de mídia social na Imagem interativa não são suportadas quando você incorpora o visualizador em um Fragmento de experiência. Para contornar isso, você pode usar ou criar predefinições do visualizador que não tenham ferramentas de compartilhamento de mídia social. Essas predefinições do visualizador permitem que você as incorpore com êxito aos Fragmentos de experiência.



1. Toque em **[!UICONTROL Salvar]** para salvar seu trabalho e retornar à página Procurar.
1. Publique a imagem interativa. A publicação permite que o banner seja entregue pela nuvem e também gera código incorporado se você precisar se integrar a um site de terceiros.

   Consulte [Publicar ativos](/help/assets/managing-assets-touch-ui.md#publishing-assets).

   Depois de adicionar pontos de acesso e publicar a imagem interativa, você está pronto para adicioná-la ao seu site existente.

   Consulte [Integrar uma imagem interativa ao seu site](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   >
   >Se você estiver editando imagens interativas com pontos de acesso e recortar a imagem, seus pontos de acesso serão excluídos.

### (Opcional) Visualização de imagens interativas {#optional-previewing-interactive-images}

Você pode usar a Pré-visualização para ver uma representação da aparência da imagem interativa para os clientes e testar os pontos de conexão da imagem para garantir que eles estejam se comportando como esperado.

Quando estiver satisfeito com a imagem interativa, você poderá publicá-la.
See [Embedding the Video or Image Viewer on a Web Page](/help/assets/embed-code.md).
See [Linking URLs to your web application](/help/assets/linking-urls-to-yourwebapplication.md). Observe que o método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas de AEM Sites.
See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)

**Para pré-visualização de imagens interativas**

1. Na visualização Ativos, navegue até uma imagem interativa existente que você criou e toque para abri-la na Pré-visualização.
1. Próximo ao canto superior esquerdo da página de Pré-visualização, na lista suspensa Conteúdo, toque em **[!UICONTROL Visualizadores.]**
1. Na lista Visualizadores, toque em **[!UICONTROL Shoppable_Banner]** ou no nome da predefinição do visualizador de imagens interativo que você criou.
1. Toque em pontos de acesso na imagem para testar suas ações associadas.

## Publicar ativos de imagem interativos {#publishing-interactive-image-assets}

Consulte [Publicação de ativos](/help/assets/publishing-dynamicmedia-assets.md) para obter detalhes sobre como publicar ativos de imagem interativos.

## Integração de uma imagem interativa com seu site {#integrating-an-interactive-image-with-your-website}

Depois de carregar uma imagem de banner, adicionar pontos de acesso à imagem e publicar a imagem interativa, você estará pronto para adicioná-la à página do site.

Se você for um cliente do AEM Sites, poderá adicionar a imagem interativa arrastando o componente de Mídia interativa para a página. See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)

Se você for um cliente do AEM Assets independente, poderá adicionar manualmente a imagem interativa ao seu site, conforme descrito nesta seção.

1. Copie o código incorporado da imagem interativa publicada.
See [Embedding the Video or Image Viewer on a Web Page](/help/assets/embed-code.md).

1. Adicione o código incorporado copiado no local desejado na página da Web.
O código incorporado copiado é definido para um ambiente responsivo, de modo que ele deve se ajustar automaticamente à área atribuída.

**Exemplo**

Como usar o site de demonstração como exemplo:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

Observe que a imagem dos três homens é uma `IMG` tag estática:

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

A integração é tão simples quanto remover a `IMG` tag e substituí-la pelo código incorporado copiado dos AEM Assets. Você pode ver o resultado no seguinte URL que mostra a imagem interativa que pode ser comprada na página com três pontos de acesso circulares:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html)

>[!NOTE]
>
>Neste ponto, os pontos de conexão na imagem interativa que pode ser comprada do site da demonstração são apenas para fins de exibição; eles ainda não estão integrados às exibições rápidas existentes.

Para aplicar um &quot;recorte&quot; a uma imagem interativa que pode ser comprada para um ambiente responsivo, você pode incluir o atributo de configuração Imagem interativa `ZoomView.iscommand` ao caminho — onde `ZoomView` é o componente a ser chamado e `iscommand` é o comando de serviço de imagem &quot;recortar&quot; aplicado.

Consulte Atributo de configuração [ZoomView.iscommand](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_interactive_image_config_attrib_zoomview_iscommand.html) .

Consulte comando [Recortar](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/http_ref/r_crop.html) serviço de imagem.

Agora você está pronto para integrar a imagem interativa com uma exibição rápida existente em seu site.

## Integração de uma imagem interativa com uma exibição rápida existente {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
>
>Esta tarefa só se aplica se você for um cliente AEM Assets independente.

A última etapa neste processo é integrar a imagem interativa com uma implementação do Quickview existente em seu site. Não há solução para a integração que funcione para todos os casos. Toda implementação do QuickView é única e é necessária uma abordagem específica que provavelmente envolva a assistência de uma pessoa de TI de front-end.

A implementação atual do Quickview normalmente representa uma cadeia de ações inter-relacionadas que ocorrem na página da Web na seguinte ordem:

1. Um usuário aciona um elemento na interface do usuário do seu site.
1. O código front-end obtém um URL de exibição rápida com base no elemento da interface do usuário que foi acionado na etapa 1.
1. O código de front-end envia uma solicitação do Ajax usando o URL obtido na etapa 2.
1. A lógica de backend retorna os dados ou o conteúdo correspondentes do Quickview de volta ao código de front-end.
1. O código front-end carrega os dados ou o conteúdo do Quickview.
1. Como opção, o código front-end converte os dados carregados do Quickview em uma representação HTML.
1. O código front-end exibe uma caixa de diálogo modal ou um painel e renderiza o conteúdo HTML na tela do usuário final.

Essas chamadas podem não representar chamadas de API públicas independentes que podem ser chamadas pela lógica da página da Web de uma etapa arbitrária. Em vez disso, é uma chamada encadeada na qual cada próxima etapa está oculta na última fase (retorno de chamada) da etapa anterior.

Ao mesmo tempo que a imagem interativa que pode ser comprada está substituindo a etapa 1 e parcialmente a etapa 2, quando um usuário clica em um ponto de acesso dentro da imagem que pode ser comprada, essa interação do usuário é manipulada pelo visualizador. O visualizador retorna um evento para a página da Web que contém todos os dados de ponto de acesso adicionados anteriormente aos AEM Assets.

Nesse manipulador de eventos, o código front-end faz o seguinte:

* Escuta um evento emitido pela imagem interativa que pode ser comprada.
* Constrói um URL de exibição rápida com base nos dados do ponto de acesso.
* Aciona o processo de carregamento do Quickview do backend e renderização na tela para exibição.

O código incorporado retornado pelos AEM Assets já tem um manipulador de eventos pronto para uso no lugar que é comentado, como visto no trecho de código destacado a seguir:

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

Portanto, é necessário remover as barras de comentário do código e substituir o corpo do manipulador de simulação pelo código específico da página da Web em particular.

O processo de construção do URL do Quickview é basicamente o oposto do processo usado para identificar variáveis de hotspots abordadas anteriormente.

Consulte [Identificação de variáveis](#optional-identifying-hotspot-variables)de pontos de conexão.

Usando nossos exemplos anteriores de URL do Quickview, você pode ver, nos seguintes exemplos, como o URL do Quickview é construído em cada caso:

<table>
 <tbody>
  <tr>
   <td><p>SKU único, encontrado na string do query</p> </td>
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
   <td><p>SKU e ID de categoria na sequência de query</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

A última etapa para acionar o URL do Quickview e ativar o painel do Quickview provavelmente requer a assistência de uma pessoa de TI front-end do seu departamento de TI. Eles têm conhecimento para saber melhor como acionar com precisão a implementação do Quickview a partir da etapa correta, tendo um URL do Quickview pronto para uso.

Você pode ver como essas etapas são aplicadas ao site de demonstração para integrar totalmente uma imagem interativa que pode ser comprada com o código do Quickview. Anteriormente, a estrutura do URL do Quickview era identificada como a seguinte:

```xml
/datafeed/$categoryId$-$SKU$.json
```

Para reconstruir esse URL dentro do manipulador `quickViewActivate` , você pode usar os campos `categoryId` e `SKU` disponíveis no `inData` objeto passado ao manipulador pelo código do visualizador:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

O site de demonstração está acionando a caixa de diálogo do Quickview usando uma chamada de `loadQuickView()` função simples. Essa função utiliza apenas um argumento, que é o URL de dados do Quickview. Dessa forma, a última etapa necessária para integrar a imagem interativa que pode ser comprada é adicionar a seguinte linha de código ao `quickViewActivate` manipulador:

```xml
loadQuickView(quickViewUrl);
```

Este é o código fonte completo:

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

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html)

## Uso do Quickviews para criar pop-ups personalizados {#using-quickviews-to-create-custom-pop-ups}

See [Using Quickviews to create custom pop-ups](/help/assets/custom-pop-ups.md).
