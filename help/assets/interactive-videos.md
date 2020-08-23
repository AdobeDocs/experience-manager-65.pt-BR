---
title: Vídeos interativos
description: Saiba como trabalhar com vídeo interativo e vídeos que podem ser comprados no Dynamic Media
uuid: c3ff6839-fff5-4709-8163-5c4245b80e6d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 04be55f2-c7d8-45ef-89e5-58856b971de5
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '6050'
ht-degree: 4%

---


# Vídeos interativos{#interactive-videos}

Você pode criar vídeos interativos facilmente - também conhecidos como vídeos que podem ser comprados - que impulsionam a conversão diretamente do vídeo. O envolvimento do cliente com o vídeo ocorre em um painel ao lado do player de vídeo, onde o serviço, as informações ou as miniaturas do produto relacionados são rolados para a visualização com base no que aparece no vídeo. Os clientes podem tocar na miniatura e ser vinculados diretamente ao serviço, adicionar o item a um carrinho de compras para compra imediata ou ser vinculados a uma página da Web para obter mais informações.

Quando o vídeo terminar, um resumo visual de todas as ofertas será exibido para direcionar uma chamada à ação. Os clientes têm outra oportunidade de tocar no item que desejam. Experiências acionáveis e específicas, como essas, aumentam o envolvimento e a conversão do cliente.

Consulte também Imagens [](/help/assets/interactive-images.md)interativas.

## Vídeo interativo em ação {#interactive-video-in-action}

To see an interactive, shoppable video in action, click [Live Demos](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html), scroll to the **[!UICONTROL Shoppable Media]** heading on the page, then click the shoppable video.

* Durante a reprodução, à medida que os produtos são usados no vídeo, o produto idêntico aparece à direita como uma imagem em miniatura.

* Clique na miniatura para pausar o vídeo e abrir a visualização rápida do produto. Por exemplo, clique na imagem em miniatura de KitchenAid no vídeo para exibir uma visualização de rotação de 360 graus do mixer ou amplie para ver os detalhes do mixer.

<!-- There was a link here that showed the video frame of an interactive video and when the reader clicked the frame the video would play https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/AXIS/index.html. This now needs to call a new interactive video-->

![Um quadro de um vídeo](assets/chlimage_1-126.png) interativo e que pode ser comprado *Uma captura de quadro de vídeo de um vídeo interativo e que pode ser comprado.*

>[!NOTE]
>
>Se você criar um vídeo interativo para iniciar uma página da Web quando um usuário clicar em uma imagem em miniatura, alguns dispositivos impedirão a abertura da página da Web pop-up. Nesses casos, é necessário alterar a configuração do bloqueador de pop-ups no dispositivo. Por exemplo, em um Apple iPhone 6, toque em **[!UICONTROL Configurações]** > **Safari** > Pop-ups **de** bloqueio e deslize o controle para **[!UICONTROL Desativado]**. Agora, ao reproduzir um vídeo interativo e clicar em uma miniatura, você será solicitado a abrir o pop-up. Se você aceitar, a página da Web será aberta.

### Veja como os vídeos interativos são criados {#watch-how-interactive-videos-are-created}

Assista a uma apresentação de 7 minutos e 30 segundos sobre [como os vídeos interativos são criados](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveVideo) [](https://outv.omniture.com?v=s4NHQ2dzqd7hIqWjeG2sIdyNWsTWyupA).
(Embora a apresentação em vídeo tenha a marca Assets on Demand, os princípios e etapas ainda se aplicam a Vídeo interativo no AEM Assets.)

### Webinar de sucesso do cliente Adobe {#adobe-customer-success-webinar}

O webinário &quot;Usando vídeo interativo, compartilhamento de links e compartilhamento do YouTube no AEM Assets&quot; ensina como usar vídeos interativos e outros recursos para associar eventos direcionados à conversão ao conteúdo de marketing de vídeo.

>[!NOTE]
[Usar vídeo interativo, compartilhamento de links e compartilhamento do YouTube no AEM Assets](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/).

## Start rápido: Vídeos interativos {#quick-start-interactive-videos}

A seguinte descrição passo a passo do fluxo de trabalho foi projetada para ajudá-lo a iniciar e executar rapidamente com vídeos interativos no Dynamic Media.

Procure o cabeçalho **Exemplo** em algumas tarefas do Start rápido. Ele contém um breve tutorial baseado nesta página de demonstração inicial da Web que ainda não ** tem interatividade adicionada a ela:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

Os **Exemplos** ajudam a ilustrar as etapas da integração de vídeos interativos em seu próprio site.

Quando você terminar o tutorial na última seção Exemplo, a página da Web de demonstração final com o vídeo interativo totalmente integrado terá a seguinte aparência:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html)

Etapas interativas do vídeo:

1. **(Opcional) Identificação de variáveis** do Quickview - Start identificando variáveis dinâmicas usadas pela implementação do Quickview existente. Use as variáveis para mapear miniaturas de produtos para o Quickview de produto correspondente ao criar seu vídeo interativo. Consulte [(Opcional) Como identificar variáveis](#optional-identifying-quickview-variables)do Quickview.
   *Observe que esta etapa só é necessária se todas as seguintes etapas forem verdadeiras*:
・ Você deseja adicionar interatividade ao seu vídeo, disparando para visualizações rápidas.
・ Sua implementação do AEM *não* usa uma estrutura de integração de eCommerce para inserir dados de produtos em AEM de qualquer solução de eCommerce como IBM Webphere Commerce, Elastic Path, hybris ou Intershop. Consulte Conceitos de [eCommerce na AEM Assets](/help/sites-administering/concepts.md).

1. **(Opcional) Criação de uma predefinição** do visualizador de vídeo interativo - Personalize a aparência e o comportamento de vários componentes que compõem o player, como o depurador de vídeo e as miniaturas interativas.
A criação de sua própria predefinição do visualizador de vídeo interativo não é necessária se você pretende usar as predefinições do visualizador de vídeo interativo prontas `Shoppable_Video_Light` ou `Shoppable_Video_Dark` .
Consulte [Criação de uma nova predefinição](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) do visualizador (opcional) e considerações [especiais para criar uma predefinição](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset)do visualizador interativo.

1. **Carregar um vídeo e seus ativos** de imagem associados - Carregue um vídeo e imagens associadas que você deseja tornar interativas.
Consulte [Carregar um vídeo e seus ativos](#uploading-a-video-and-its-associated-thumbnail-assets)em miniatura associados.

1. **Adicionar interatividade ao vídeo** - Adicione um ou mais segmentos de tempo ao vídeo. Em seguida, associe miniaturas de imagem nesses segmentos de tempo. Atribua cada miniatura de imagem a uma ação, como um hiperlink, uma visualização rápida ou um fragmento de experiência.
(Observe que o método baseado em URL de vinculação não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas do AEM Sites.)
Conclua publicando os ativos de vídeo interativos. A publicação cria o código incorporado ou o URL que você eventualmente copiará e aplicará à landing page do site.Consulte [Adicionar interatividade ao vídeo](#adding-interactivity-to-your-video).
Consulte [Publicação de ativos](/help/assets/publishing-dynamicmedia-assets.md).

1. **Adicionando um vídeo interativo ao seu site ou ao seu site em AEM** Se você usar o AEM Sites ou AEM eCommerce, ou ambos, você pode adicionar o vídeo interativo diretamente a uma página da Web em AEM arrastando o componente de Mídia interativa para a página. See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)
Use o código incorporado ou URL para integrar seu vídeo interativo com as experiências do site. Consulte [Integrar um vídeo interativo ao seu site](#integrating-an-interactive-video-with-your-website).
Se você estiver usando um WCM de terceiros (Web Content Manager), é necessário integrar o novo vídeo interativo com a implementação existente do Quickview usada em seu site. Consulte [Integrar um vídeo interativo a um Quickview](#integrating-an-interactive-video-with-an-existing-quickview)existente.
   [](/help/assets/adding-dynamic-media-assets-to-pages.md)

## (Opcional) Como identificar variáveis do Quickview {#optional-identifying-quickview-variables}

>[!NOTE]
Essa tarefa só é necessária se as seguintes condições forem verdadeiras:
* Você deseja adicionar interatividade ao vídeo, disparando para o Quickviews.
* Sua implementação do AEM *não* usa uma estrutura de integração de eCommerce para inserir dados de produtos em AEM de qualquer solução de eCommerce como IBM Webphere Commerce, Elastic Path, hybris ou Intershop. Consulte Conceitos de [eCommerce na AEM Assets](/help/sites-administering/concepts.md).

Se sua implementação do AEM usar o eCommerce, você poderá pular essa tarefa e seguir para a próxima tarefa.

Start identificando variáveis dinâmicas usadas pela implementação do Quickview existente para que você possa mapear miniaturas de produtos para o produto correspondente do Quickview durante o processo de criação de vídeo interativo.

Quando você adiciona segmentos de tempo a um vídeo, atribui um SKU e quaisquer variáveis adicionais a cada miniatura que você adiciona a um segmento. Essas variáveis são usadas posteriormente para exibir o produto Quickview correto.

É importante identificar corretamente quais variáveis são necessárias para acionar exclusivamente um Quickview de produto.

Às vezes, pode ser suficiente consultar especialistas de TI responsáveis pela implementação atual do Quickview. Eles provavelmente conhecem o conjunto mínimo de dados necessário para identificar o Quickview no sistema. No entanto, na maioria dos casos, é possível simplesmente analisar o comportamento existente do código front-end.

A maioria das implementações do Quickview usa o seguinte paradigma:

* O usuário ativa um elemento da interface do usuário no site. Por exemplo, clicar em um botão &quot;Quickview&quot;.
* O site envia uma solicitação do Ajax para o backend para carregar os dados ou o conteúdo do Quickview, se necessário.
* Os dados do Quickview são traduzidos para o conteúdo em preparação para renderização na página da Web.
* Por fim, o código front-end exibe visualmente esse conteúdo na tela.

A abordagem, portanto, é visitar diferentes áreas de seu site existente onde o Quickview é implementado, acionar o Quickview e capturar o URL Ajax enviado pela página da Web para carregar os dados ou o conteúdo do Quickview.

Normalmente, não é necessário usar nenhuma ferramenta de depuração especializada. Os navegadores da Web modernos dispõem de inspetores da Web que fazem um trabalho adequado. A seguir estão alguns exemplos de navegadores da Web que incluem inspetores da Web:

* Para ver todas as solicitações HTTP de saída no Google Chrome, pressione **F12** (Windows) ou **Command+Options+I** (Mac) para abrir o painel Ferramentas do desenvolvedor e clique na guia **Rede** .

* In Firefox, you can either activate the Firebug plug-in by pressing **F12** (Windows) or **Command+Option+I** (Mac) and use its **`[Net]`** tab, or you can use the built-in Inspector tool and its Network tab.

* No Internet Explorer, ative a ferramenta de depuração pressionando **F12**.

Quando o monitoramento de rede estiver ativado no navegador, dispare o Quickview na página.

Agora, encontre o URL Ajax do Quickview no registro de rede e copie o URL gravado para análise futura. Na maioria dos casos, quando você aciona o Quickview, há várias solicitações que são enviadas para o servidor. Normalmente, o URL do Ajax do Quickview é um dos primeiros na lista. Ele tem uma parte ou um caminho de sequência de query complexo, e seu tipo MIME de resposta é `text/html`, `text/xml`ou `text/javascript`.

Durante esse processo, é importante visitar diferentes áreas do seu site, com diferentes categorias e tipos de produtos. O motivo é que os URLs do Quickview podem ter partes comuns para uma determinada categoria do site, mas são alterados somente se você visitar uma área diferente do site.

No caso mais simples, a única parte variável no URL do Quickview é o SKU do produto. Nesse caso, o valor SKU do produto é o único dado necessário para adicionar miniaturas a um segmento de tempo no vídeo interativo no AEM.

No entanto, em casos complexos, o URL do Quickview tem diferentes elementos variados além do SKU do produto, como ID da categoria, código de cor e assim por diante. Nesses casos, cada elemento se torna uma variável separada na definição de dados em miniatura no AEM.

Considere os seguintes exemplos de URLs do Quickview e suas variáveis de miniatura resultantes:

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
    </ul> <p>A única parte variável no URL é o valor do parâmetro da string de <code>productId=</code> query e é claramente um valor SKU. Portanto, nossas miniaturas precisam apenas de campos SKU preenchidos com valores como <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU único, encontrado no caminho do URL.</p> </td>
    <td><p>Os URLs de exibição rápida gravados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>A parte variável está na última parte do caminho e se torna o valor SKU de miniaturas AEM: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID da categoria na sequência do query.</p> </td>
    <td><p>Os URLs de exibição rápida gravados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>Nesse caso, há duas partes diferentes no URL. O SKU é armazenado no <code>prodId</code> parâmetro e a ID da categoria é armazenada no <code>category=</code> parâmetro.</p> <p>Dessa forma, as definições de miniaturas são pares. Ou seja, um valor de SKU e uma variável adicional chamada <code>categoryId</code>. Os pares resultantes são os seguintes:</p>
    <ul>
      <li>O SKU é <code>305466</code> e <code>categoryId</code> é <code>1100004</code></li>
      <li>O SKU é <code>310181</code> e <code>categoryId</code> é <code>1100004</code></li>
      <li>O SKU é <code>308706</code> e <code>categoryId</code> é <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Exemplo**

Quando a abordagem acima é aplicada ao nosso site de exemplo, temos uma página da Web com várias miniaturas de produtos, cada uma com um botão &quot;VER MAIS&quot;:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

Depois de ativar todas as exibições rápidas de produtos disponíveis na página, você obtém a seguinte lista de solicitações do Quickview feitas ao backend:

* datafeed/candles-233396346.json
* datafeed/candles-233978050.json
* datafeed/candles-234024346.json
* datafeed/candles-234024356.json
* datafeed/candles-234024359.json
* datafeed/cushions-233939848.json
* datafeed/cushions-234019477.json
* datafeed/cushions-234019483.json
* datafeed/furniture-231747479.json
* datafeed/furniture-232625621.json
* datafeed/furniture-232625626.json
* datafeed/furniture-233939810.json
* datafeed/furniture-233939825.json
* datafeed/furniture-233939828.json
* datafeed/furniture-233939853.json
* datafeed/furniture-233940334.json
* datafeed/glassware-000064007.json
* datafeed/glassware-230722193.json
* datafeed/glassware-233916550.json
* datafeed/glassware-233916597.json

Olhando para essas chamadas de servidor, você verá que informações específicas do produto estão presentes apenas no caminho da solicitação. Você também observa que a sequência de caracteres do query não é usada de todo, e há dois tipos distintos de partes de dados envolvidas:

* O primeiro tipo é velas, almofadas, móveis e artigos de vidro. Você pode chamar isso de &quot;categoria do produto&quot;.
* O segundo tipo é o código do produto, como 233916597. Você pode assumir que é &quot;SKU de produto&quot;.

Considerando essas informações, todo o URL do Quickview tem o seguinte padrão:

`/datafeed/$categoryId$-$SKU$.json`

Com base nessa análise, você conclui que pode usar as duas variáveis a seguir para as miniaturas: `categoryId` e `SKU`.

Agora você está pronto para carregar um vídeo e seus ativos em miniatura associados.

## (Opcional) Criação de uma predefinição do visualizador de vídeo interativo {#optional-creating-an-interactive-video-viewer-preset}

Você pode ignorar essa tarefa e continuar para a próxima se pretender usar um dos tipos predefinidos padrão e predefinidos do visualizador de vídeo interativo `Shoppable_Video_dark` ou `Shoppable_Video_light`.

Quando uma miniatura é clicada no ambiente de criação, uma pré-visualização da caixa de diálogo do Quickview é exibida.

![chlimage_1-21](assets/chlimage_1-127.png)

Como opção, você pode criar sua própria predefinição personalizada do visualizador de vídeo interativo. Você pode determinar, entre outras coisas, o estilo do player de vídeo, as miniaturas interativas e a visualização da grade de miniaturas que aparece no final do vídeo.

Uma predefinição de Visualizador de vídeo interativo renderiza corretamente o vídeo e todos os segmentos de linha do tempo adicionados. Ele também usa um exemplo de exibição rápida padrão quando você clica em uma miniatura de produto no modo de Pré-visualização para que você possa testar sua interatividade antes de publicar.

Após salvar a predefinição do visualizador, seu estado é automaticamente definido como **Ativado **in na página Predefinições do visualizador. Esse estado significa que está visível no componente do Dynamic Media e sempre que você visualiza um vídeo com ele. Certifique-se de publicar manualmente a nova predefinição do visualizador.

Consulte [Criar uma nova predefinição](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) do visualizador para criar sua própria predefinição do visualizador de vídeo interativo.

## Fazer upload de um vídeo e de seus ativos em miniatura associados {#uploading-a-video-and-its-associated-thumbnail-assets}

Se você já carregou seus ativos de vídeo e miniatura, prossiga para [Adicionar interatividade ao vídeo](#adding-interactivity-to-your-video).

Se você carregou os vídeos ou imagens errados, ou quiser excluir vídeos ou imagens carregados de que não precisa mais, consulte [Excluindo ativos](/help/assets/managing-assets-touch-ui.md#deleting-assets).

Para carregar um vídeo e seus ativos em miniatura associados:

1. Faça upload do vídeo e dos ativos em miniatura associados para a pasta ou pastas desejadas.

   See [Uploading assets](/help/assets/managing-assets-touch-ui.md).
Consulte [Fazer upload de ativos usando o agendamento](/help/assets/managing-assets-touch-ui.md)de tarefas FTP.

   Agora, adicione interatividade ao seu vídeo.

## Adicionar interatividade ao vídeo {#adding-interactivity-to-your-video}

Você adiciona segmentos de linha do tempo a um vídeo usando o editor visual local na página Criar vídeo interativo.

Depois de adicionar segmentos de linha do tempo, adicione imagens em miniatura em cada segmento. Para cada miniatura adicionada, você aplica uma ação a ela. Por exemplo, você pode aplicar uma visualização rápida à miniatura, ou pode atribuir um hiperlink a ela ou um Fragmento de experiência.

Consulte Fragmentos [de experiência](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
Observe que as ferramentas de compartilhamento de mídia social em Vídeo interativo não são suportadas quando você incorpora o visualizador em um Fragmento de experiência. Para contornar isso, você pode usar ou criar predefinições do visualizador que não tenham ferramentas de compartilhamento de mídia social. Essas predefinições do visualizador permitem que você as incorpore com êxito aos Fragmentos de experiência.

>[!NOTE]
O método baseado em URL de vinculação não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas do AEM Sites.

As opções Desfazer e Refazer, perto do canto superior direito da página, são suportadas durante a sessão atual de criação/edição.

Após salvar o vídeo interativo, ele será aberto imediatamente na Pré-visualização. A partir daí, você pode selecionar uma predefinição do visualizador de vídeo interativo e reproduzir o vídeo para ver uma representação aproximada de como ele aparecerá para os clientes.

Para adicionar interatividade ao vídeo:

1. Na visualização Ativos, navegue até o vídeo que você carregou e deseje tornar interativo.
1. Faça uma das seguintes opções:

   * Hover on the image, then tap **[!UICONTROL Select]** (checkmark icon). Na barra de ferramentas, toque em **[!UICONTROL Editar.]**

   * Passe o mouse sobre a imagem e toque em **[!UICONTROL Mais ações]** (ícone de três pontos) **[!UICONTROL > Editar.]**

   * Toque na imagem para abri-la na página Visualização Detalhe. Na barra de ferramentas, toque em **[!UICONTROL Editar.]**

1. Na página Criar vídeo interativo, execute um dos procedimentos a seguir:

   * Toque no botão **[!UICONTROL Reproduzir]** para começar a reproduzir o vídeo. Quando um produto, serviço ou detalhe específico que você deseja destacar entrar na visualização, toque em **[!UICONTROL Adicionar segmento]** na barra de ferramentas. Repita até chegar ao fim do vídeo.

      Para cada segmento de tempo adicionado, é possível atribuir uma ou mais imagens em miniatura a ele e, em seguida, vincular essas miniaturas às páginas de produto do Quickview para que os clientes comprem ou às páginas da Web para obter mais informações.

   * Toque no botão **[!UICONTROL Reproduzir]** para começar a reproduzir o vídeo. Quando um produto, serviço ou detalhe específico que você deseja destacar entrar na visualização, toque em **[!UICONTROL Pausar.]** Toque em **[!UICONTROL Adicionar segmento.]**

      Continue reproduzindo e pausando o vídeo em pontos na linha do tempo em que deseja adicionar um segmento até atingir o fim do vídeo.

1. (Opcional) Arraste a barra no **[!UICONTROL controle deslizante Escala da linha do tempo]** para a esquerda para aumentar ou diminuir o zoom e para direita para diminuir o zoom, controlando assim quantos detalhes você vê dos segmentos adicionados.

   ![chlimage_1-22](assets/chlimage_1-128.png)

   Dependendo da duração do vídeo, a Duração do segmento assumirá os seguintes valores como padrão:

   <table>
      <tbody>
        <tr>
        <td><strong>Se a duração do vídeo for...</strong></td>
        <td><strong>O padrão da configuração Duração do segmento é...</strong></td>
        </tr>
        <tr>
        <td>3 minutos ou mais</td>
        <td>60 segundos</td>
        </tr>
        <tr>
        <td>2 a 3 minutos</td>
        <td>30 segundos</td>
        </tr>
        <tr>
        <td>1-2 minutos</td>
        <td>20 seconds<br /> </td>
        </tr>
        <tr>
        <td>30 a 60 segundos</td>
        <td>10 segundos</td>
        </tr>
        <tr>
        <td>30 segundos ou menos</td>
        <td>5 segundos</td>
        </tr>
      </tbody>
    </table>

   A linha do tempo do vídeo usa tantas propriedades de tela quanto o que está disponível para ele. Dessa forma, ao redimensionar o navegador, os segmentos adicionados mantêm sua largura correta.

   Para ilustrar, as três capturas de tela a seguir estão usando o mesmo vídeo. Observe que a largura de cada segmento muda dependendo da configuração Escala da linha do tempo.

   ![chlimage_1-23](assets/chlimage_1-129.png)

   Captura de tela A

   Captura de tela A acima mostra a visualização padrão de um vídeo de 29 segundos do produto. A Escala da Linha do Tempo é definida como padrão de 5 segundos.

   ![chlimage_1-130](assets/chlimage_1-130.png)

   Captura de tela B

   Na Captura de tela B acima, o controle deslizante Escala da linha do tempo foi arrastado do padrão de 5 segundos para 3 segundos. Observe que os carimbos de data e hora individuais da Escala de linha do tempo agora estão todos definidos em intervalos de 3 segundos.

   ![chlimage_1-25](assets/chlimage_1-131.png)

   Captura de tela C

   Na captura de tela C acima, a configuração Escala da linha do tempo foi movida para 8 segundos. Observe como os segmentos que contêm miniaturas de produtos foram reduzidos. Reduzir dessa forma é útil se você tiver um vídeo longo e quiser ver uma visão geral de mais segmentos que normalmente se ajustariam à largura da página.

1. (Opcional) Execute um dos procedimentos a seguir:

   * Para ajustar a hora e a hora de término do start de um segmento.

      Selecione um segmento e arraste a oval azul à esquerda ou à direita para ajustar a hora de start ou de término, respectivamente. O quadro de vídeo exibido é movido para a hora apropriada no vídeo, com base em seus ajustes. O movimento do segmento da linha do tempo é restrito com base em qualquer segmento adjacente na linha do tempo. O tempo mínimo de segmento permitido é de um segundo.

      Use os seguintes atalhos de navegação para verificar e ajustar rapidamente seus segmentos de vídeo:

      * Toque na oval azul à esquerda para buscar o vídeo diretamente para o início desse segmento.
      * Toque na oval azul à direita para buscar o vídeo diretamente ao final desse segmento.
      * Toque no segmento inteiro para retornar a reprodução do vídeo ao start desse segmento

   ![chlimage_1-26](assets/chlimage_1-132.png)

   Reposicionamento do final de um segmento de linha do tempo

   * Para excluir um segmento

      Selecione o último segmento que está na linha do tempo e, na barra de ferramentas, toque em **[!UICONTROL Excluir segmento.]** Se dois ou mais segmentos forem selecionados, o recurso Excluir segmento será desativado.

      Você só pode excluir o último segmento. Por exemplo, se você deseja excluir todos os segmentos na linha do tempo, sempre selecione o último e, em seguida, toque em **[!UICONTROL Excluir segmento.]**


1. Selecione um segmento de tempo ao qual você deseja associar uma ou mais imagens em miniatura.
1. À direita do vídeo, toque na guia **[!UICONTROL Conteúdo]** .
1. Na guia Conteúdo, toque em **[!UICONTROL Selecionar ativos]** e, em seguida, navegue e selecione todos os ativos de imagem que deseja usar com o vídeo. Os ativos selecionados são adicionados ao painel Seletor de ativos na guia Conteúdo.

1. No seletor de ativos abaixo da guia Conteúdo, execute um dos procedimentos a seguir:

   <table>
      <tbody>
        <tr>
        <td>Para associar uma miniatura ao segmento de linha do tempo selecionado</td>
        <td><p>Toque na imagem no painel seletor de ativos à direita.</p> <p>Você pode adicionar quantas miniaturas desejar a um segmento de linha do tempo. Para cada imagem selecionada, uma marca de seleção aparece sobre a imagem no seletor de ativos.</p> </td>
        </tr>
        <tr>
        <td>Para remover uma miniatura do segmento de linha do tempo selecionado</td>
        <td><p>Siga um destes procedimentos:</p>
          <ul>
          <li>No painel seletor de ativos, toque em uma imagem com uma marca de seleção para desmarcá-la. O ativo de imagem é removido do segmento de linha do tempo.<br /> </li>
          <li>No segmento de linha do tempo selecionado, toque em uma imagem e, em seguida, na barra de ferramentas, toque em <strong>Excluir produto</strong>.</li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![Seletor de ativos](assets/chlimage_1-133.png)

   Tocar em uma imagem no painel seletor de ativos a adiciona ao segmento de linha do tempo selecionado.

1. Selecione uma única imagem em miniatura em um dos segmentos da linha do tempo e toque na guia **[!UICONTROL Ações]** .
1. Siga um destes procedimentos:
   <table> 
    <tbody> 
      <tr> 
      <td>Para associar a imagem em miniatura selecionada a uma exibição Rápida</td> 
      <td><p>Em Tipo de ação, toque em <strong>Quickview</strong>.</p> <p>Se você for um cliente AEM Sites e Ecommerce:</p> 
       <ul> 
       <li>Observe que o campo de texto Valor SKU é pré-preenchido com o SKU do produto selecionado (Stock Keeping Unit), que é um identificador exclusivo para cada produto ou serviço distinto que você está oferecendo. Isso é preenchido automaticamente quando a imagem é associada a um produto no AEM Commerce.</li> 
       <li>Se o SKU pré-preenchido estiver incorreto, toque ou clique no ícone Seletor de produto (lupa) para abrir a página Selecionar produto. Toque ou clique no produto que deseja usar e, em seguida, toque na marca de seleção no canto superior direito da página para retornar ao Editor de vídeo interativo.</li> 
       </ul> <p> Se você <em>não</em> for um cliente AEM Sites ou Ecommerce</p> 
       <ul> 
       <li>Consulte <a href="/help/assets/carousel-banners.md#identifying-hotspot-and-image-map-variables">Identificação de variáveis</a>de pontos de conexão. Será necessário definir essas variáveis. </li> 
       <li>Por padrão, esse campo SKU usa o nome de arquivo do ativo de imagem sem a extensão. Se você seguir uma convenção de nomenclatura padrão para seus arquivos com base no SKU, isso geralmente não requer edições adicionais. </li> 
       <li>Caso contrário, edite o valor padrão e insira o valor SKU correto. No campo de texto Valor SKU, digite o SKU do produto (Stock Keeping Unit), que é um identificador exclusivo para cada produto ou serviço distinto que você oferta. O valor SKU inserido preenche automaticamente a parte variável do modelo do Quickview, de modo que o sistema saiba associar a imagem tocada a uma exibição rápida do SKU.</li> 
       </ul> <p>(Opcional) Se houver outras variáveis na exibição Rápida que você precisa usar para identificar ainda mais um produto, toque em <strong>Adicionar variável</strong>genérica. No campo de texto, especifique uma variável adicional. Por exemplo, <code>category=Womens</code> é uma variável adicionada.</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>Para associar a imagem em miniatura selecionada a um hiperlink</td> 
      <td><p>Em Tipo de ação, toque em <strong>Hiperlink</strong>e execute um dos procedimentos a seguir:</p> 
       <ul> 
       <li>Se você for um cliente da AEM Sites, toque no ícone Seletor de site (pasta) para navegar até uma página da Web. Observe que o método baseado em URL de vinculação não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas do AEM Sites.</li> 
       <li>Se você for um cliente independente do Dynamic Media, no campo de texto HREF, especifique o caminho do URL completo para uma página da Web vinculada.</li> 
       </ul> <p>Certifique-se de especificar se deseja abrir o link em uma nova guia do navegador ou na guia atual.</p> </td> 
      </tr> 
      <tr> 
      <td>Para associar a imagem em miniatura selecionada a um fragmento de experiência</td> 
      <td><p>Em Tipo de ação, toque em Fragmento <strong>de</strong>experiência e faça o seguinte:<p> 
       <ul> 
       <li>Se você for um cliente da AEM Sites, toque ou clique no ícone Pesquisar (lupa) para abrir a página Fragmento de experiência. Toque ou clique no Fragmento de experiência que deseja usar e, em seguida, toque em <strong>Selecionar </strong>no canto superior direito da página para retornar ao painel Ações na página anterior.<br /> Consulte Fragmentos <a href="/help/sites-authoring/experience-fragments.md">de experiência</a>.</li> 
      </ul> 
       <ul> 
       <li>Especifique a largura e a altura do Fragmento de experiência como ele será exibido no vídeo.</li>
       </ul><strong>Observação</strong>: Observe que as ferramentas de compartilhamento de mídia social em Vídeo interativo não são suportadas quando você incorpora o visualizador em um Fragmento de experiência. Para contornar isso, você pode usar ou criar predefinições do visualizador que não tenham ferramentas de compartilhamento de mídia social. Essas predefinições do visualizador permitem que você as incorpore com êxito aos Fragmentos de experiência.</p></tr>&lt; 
      <tr> 
      <td>Para editar uma ação já atribuída a uma imagem em miniatura</td> 
      <td>Em um segmento de linha do tempo, toque em uma imagem em miniatura que tenha um link de cadeia à direita de seu rótulo de texto. O link de cadeia indica que uma ação foi atribuída a ela. Toque na guia <strong>Ações</strong> para fazer as alterações.</td> 
      </tr> 
      <tr> 
      <td>Alteração do rótulo de texto de uma imagem em miniatura</td> 
      <td><p>Por padrão, o rótulo do texto usa o campo de <code>Title</code> metadados da imagem em miniatura. Se não <code>Title</code> estiver presente, o nome de arquivo da imagem em miniatura será usado, mas sem a extensão.</p> <p>Para alterar o rótulo de texto de uma imagem em miniatura, na <strong>guia </strong>Ações, logo abaixo do ativo de imagem exibido, insira o texto desejado. Veja a ilustração abaixo.</p> <p>Observe que o novo rótulo de texto é usado somente pelo próprio player de vídeo e o texto em miniatura exibido no segmento de linha do tempo. A alteração de rótulo não afeta o campo de metadados de Título da imagem em miniatura nem seu nome de arquivo.</p> </td> 
      </tr> 
      <tr> 
      <td>Para reverter uma alteração que você fez</td> 
      <td>Próximo ao canto superior direito da página, toque em <strong>Desfazer</strong> ou <strong>Refazer</strong>.</td> 
      </tr> 
    </tbody> 
   </table>

   ![experiencefragment_interativevideos](assets/experiencefragment_interactivevideos.png)

   Um novo rótulo de texto é adicionado à imagem em miniatura.

1. Faça uma das seguintes opções:

   * Repita as etapas de 6 a 11 para adicionar mais imagens em miniatura a segmentos de linha do tempo em seu vídeo.
   * Continue com a etapa opcional 13.

1. (Opcional) Execute um dos procedimentos a seguir:

   * **[!UICONTROL Mesclar segmento]** - é possível combinar dois segmentos adjacentes (com ou sem miniaturas de produtos atribuídas a eles) em um segmento.

      Na linha do tempo, toque em dois ou mais segmentos contíguos que deseja mesclar em um. Observe que não há alças de arrastar ovais azuis nos dois segmentos selecionados na figura abaixo.

      Toque em **[!UICONTROL Unir segmento]** na barra de ferramentas.
   ![chlimage_1-134](assets/chlimage_1-134.png)

   Mesclando dois segmentos selecionados de cinco segundos em um segmento de dez segundos.

   * **[!UICONTROL Dividir segmento]** - é possível dividir um único segmento em dois segmentos igualmente cronometrados. Se houver miniaturas de produtos já atribuídas ao segmento, as miniaturas serão combinadas ao segmento esquerdo.

      Na linha do tempo, toque em um segmento que deseja dividir ao meio e, em seguida, toque em **[!UICONTROL Dividir segmento]** na barra de ferramentas.

      Selecionar dois ou mais segmentos desativa o recurso **[!UICONTROL Dividir segmento]** .
   ![chlimage_1-135](assets/chlimage_1-135.png)

   Dividindo um segmento selecionado de dez segundos em dois segmentos de cinco segundos cada.

1. Perto do canto superior direito da página **[!UICONTROL Criar vídeo]** interativo, o nome da predefinição do visualizador atualmente selecionado usada com o vídeo é exibido. Toque no nome para selecionar uma predefinição de visualizador diferente.

   Por exemplo, a predefinição do `Shoppable_Video_light` visualizador permite reproduzir o vídeo com uma área de exibição branca adjacente ao vídeo. A área de exibição é onde as imagens em miniatura clicáveis são exibidas durante a reprodução. A predefinição do `Shoppable_Video_dark` visualizador permite reproduzir o vídeo com uma área de exibição preta adjacente ao vídeo.

   Se você tiver criado sua própria predefinição do visualizador de vídeo interativo, também a visualizará na lista de predefinições que podem ser escolhidas.

   Quando terminar, toque em **[!UICONTROL Salvar.]**

   >[!NOTE]
   Ao salvar o vídeo interativo, um arquivo associado é automaticamente salvo com ele. `.vtt` O arquivo `.vtt` é salvo na pasta `_VTT` localizada na raiz do **[!UICONTROL Assets.]** O arquivo e a pasta são necessários para que o vídeo interativo seja reproduzido corretamente no site. Sendo assim, não mova, edite ou exclua a pasta `_VTT` ou seu conteúdo.

1. Publique o vídeo interativo. A publicação cria o código incorporado ou o URL que você eventualmente copiará e colará nas experiências do site.

   Se você adicionou interatividade com o Quickviews, use apenas o código incorporado; se você adicionou interatividade com páginas da Web hipervinculadas, também é possível usar o URL publicado. Entretanto, observe que o método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas do AEM Sites.

   Consulte [Publicar ativos](publishing-dynamicmedia-assets.md).

   >[!NOTE]
   Para publicar um vídeo que pode ser comprado com o Quickviews, certifique-se de publicar cada um dos ativos de imagem relacionados do vídeo da sua área de comércio, separadamente.

   Depois de adicionar segmentos de linha do tempo e publicar o vídeo interativo, você estará pronto para adicioná-lo à landing page do site existente. Consulte [Integrar um vídeo interativo ao seu site.](#integrating-an-interactive-video-with-your-website)

## Publicar ativos de vídeo interativo {#publishing-interactive-video-assets}

Consulte [Publicação de ativos](/help/assets/publishing-dynamicmedia-assets.md) para obter detalhes sobre como publicar ativos de vídeo interativos.

## Integração de um vídeo interativo com seu site {#integrating-an-interactive-video-with-your-website}

Depois de fazer upload de um vídeo, adicionar segmentos de linha do tempo a ele e publicar o vídeo interativo, você estará pronto para adicioná-lo ao site existente.

Se você for um cliente da AEM Sites, poderá adicionar o vídeo interativo arrastando o componente de Mídia interativa para sua página. See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)

Se você for um cliente independente da AEM Assets, poderá adicionar manualmente o vídeo interativo ao seu site, conforme descrito nesta seção.

1. Copie o código incorporado ou URL do vídeo interativo publicado.
See [Embedding the Video or Image Viewer on a Web Page](/help/assets/embed-code.md).
Se você adicionou interatividade com o Quickviews, use apenas o código incorporado; se você adicionou interatividade com páginas da Web hipervinculadas, também é possível usar o URL publicado. Entretanto, observe que o método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas do AEM Sites.

1. No código da página da Web do público alvo, identifique onde o vídeo estático está localizado.
1. Remova o vídeo estático e substitua o código pelo código incorporado ou URL que você copiou do AEM Assets, como está.
O código incorporado copiado é definido para um ambiente responsivo, de modo que ele se ajuste automaticamente à área ocupada anteriormente pelo vídeo estático.

>[!NOTE]
Como esse ponto, se você adicionou interatividade somente com páginas da Web hipervinculadas, você está pronto.
No entanto, se você adicionou qualquer interatividade para acionar uma exibição Rápida, as miniaturas adjacentes ao vídeo interativo são apenas para fins de exibição; eles ainda não estão integrados às suas exibições rápidas existentes. Nesse caso, agora é necessário integrar o vídeo interativo com as exibições rápidas existentes em seu site.

**Exemplo**

Como usar o site de demonstração como exemplo:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

Observe que é o código de incorporação de vídeo padrão:

```xml
<style type="text/css">
 #s7video_div.s7videoviewer{
   width:100%;
   height:auto;
 }
</style>

<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/VideoViewer.js"></script>
<div id="s7video_div"></div>
<script type="text/javascript">
 var s7videoviewer = new s7viewers.VideoViewer({
  "containerId" : "s7video_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Video",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "posterimage": "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 }).init();
</script>
```

A integração é tão simples quanto remover o código incorporado de vídeo e substituí-lo pelo código incorporado de vídeo interativo do AEM. Você pode ver o resultado no seguinte URL. Embora ele mostre um vídeo interativo presente na página, ele ainda não está integrado às exibições rápidas existentes:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-1.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-1.html)

## Integração de um vídeo interativo com um Quickview existente {#integrating-an-interactive-video-with-an-existing-quickview}

>[!NOTE]
Esta tarefa só se aplica se você for um cliente independente da AEM Assets.

A última etapa desse processo é integrar seu vídeo interativo com uma implementação do Quickview existente que é usada em seu site. Não há solução para a integração que funcione para todos os casos. Toda implementação do QuickView é exclusiva. Como tal, é necessária uma abordagem específica que envolva muito provavelmente a assistência de uma pessoa de TI de front-end.

A implementação atual do Quickview normalmente representa uma cadeia de ações inter-relacionadas que ocorrem na página da Web na seguinte ordem:

1. Um usuário aciona um elemento na interface do usuário do seu site.
1. O código front-end obtém um URL de exibição rápida com base no elemento da interface do usuário que foi acionado na etapa 1.
1. O código de front-end envia uma solicitação AJAX usando o URL obtido na etapa 2.
1. A lógica de backend retorna os dados ou o conteúdo correspondentes do Quickview de volta ao código de front-end.
1. O código front-end carrega os dados ou o conteúdo do Quickview.
1. Como opção, o código front-end converte os dados carregados do Quickview em uma representação HTML.
1. O código front-end exibe uma caixa de diálogo modal ou um painel e renderiza o conteúdo HTML na tela do usuário final.

Essas chamadas podem não representar chamadas de API públicas independentes que podem ser chamadas pela lógica da página da Web de uma etapa arbitrária. Em vez disso, é uma chamada encadeada na qual cada próxima etapa está oculta na última fase (retorno de chamada) da etapa anterior.

Ao mesmo tempo que o vídeo interativo está substituindo a etapa 1 e parcialmente a etapa 2, quando um usuário clica em uma miniatura dentro do vídeo interativo, essa interação do usuário é feita pelo visualizador. O visualizador retorna um evento para a página da Web que contém todos os dados em miniatura adicionados anteriormente ao AEM.

Nesse manipulador de eventos, o código front-end faz o seguinte:

* Escuta um evento emitido pelo vídeo interativo.
* Constrói um URL de exibição rápida com base nos dados em miniatura.
* Aciona o processo de carregamento do Quickview do backend e renderização na tela para exibição.

Além disso, o visualizador de vídeo interativo oferece suporte ao modo de operação de tela cheia. O usuário final aciona as exibições rápidas clicando em uma miniatura sem sair da tela cheia. Para obter essa funcionalidade, altere o código de front-end para que a caixa de diálogo modal do Quickview seja anexada ao container do visualizador. Não adicione o BODY do documento ou algum outro elemento da página da Web que não esteja disponível quando o visualizador estiver no modo de tela cheia. O código que executa este trabalho precisa ouvir mais um retorno de chamada do visualizador enviado depois que o visualizador carrega na página.

O código incorporado retornado pelo AEM já possui um manipulador de eventos pronto para uso. Ele é comentado como visto no trecho de código destacado a seguir:

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 /* // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
    //To pass other parameter from the hotspot, you need to add custom parameter during the hotspot setup as parameterName=value
    loadQuickView(sku); //Replace this call with your quickview plugin
    //Please refer to your quickviewer plugin for the quickview call
    },
"initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var popup = document.getElementById('quickview_div'); // get custom quickview container
    popup.parentNode.removeChild(popup); // remove it from current DOM
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(popup); //Attach custom quickview container to viewer
    }
   });
 */
 s7interactivevideoviewer.init();
</script>
```

Portanto, é necessário remover as barras de comentário do trecho de código destacado acima e substituir o corpo dos manipuladores de simulação por um código específico para a página da Web em particular.

Há dois manipuladores de retorno de chamada padrão presentes no código incorporado padrão: `quickViewActivate` e `initComplete`. O `quickViewActivate` manipulador dispara quando uma miniatura é clicada no visualizador. Use-o para integrar o visualizador à lógica de ativação do Quickview. O `initComplete` manipulador dispara apenas uma vez quando o visualizador é carregado na página. Esse manipulador é usado para ajustar o local da caixa de diálogo do Quickview no DOM da página da Web.

O processo de construção do URL do Quickview é oposto ao processo de identificação das variáveis de miniatura abordadas anteriormente neste tópico. Usando nossos exemplos de URL do Quickview identificados anteriormente, você pode ver como o URL do Quickview é construído em cada caso:

<table>
  <tbody>
  <tr>
    <td><p>SKU único, encontrado na string do query</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
    <td>SKU único, encontrado no caminho do URL</td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
    <td><p>SKU e ID de categoria na sequência de query</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
  </tbody>
</table>

A última etapa para acionar o URL do Quickview e ativar o painel do Quickview provavelmente requer a assistência de uma pessoa de TI front-end do seu departamento de TI. Eles têm conhecimento para saber melhor como acionar com precisão a implementação do Quickview a partir da etapa correta, tendo um URL do Quickview pronto para uso.

Você pode ver como essas etapas são aplicadas ao site de demonstração para integrar totalmente um vídeo interativo ao código do Quickview. Anteriormente neste tópico, a estrutura do URL do Quickview era identificada como a seguinte:

```xml
/datafeed/$CategoryId$-$SKU$.json
```

É fácil reconstruir esse URL dentro do manipulador `quickViewActivate` usando `categoryId` e `sku` os campos disponíveis no `inData` objeto passado ao manipulador por meio do código do visualizador, como a seguir:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

O site de demonstração está acionando a caixa de diálogo do Quickview usando uma chamada de `loadQuickView()` função simples. Essa função utiliza apenas um argumento, que é o URL de dados do Quickview. Assim, a última etapa necessária para integrar o vídeo interativo é adicionar a seguinte linha de código ao `quickViewActivate` manipulador:

```xml
loadQuickView(quickViewUrl);
```

Por fim, verifique se a caixa de diálogo do Quickview está anexada ao elemento de container do visualizador. O código incorporado padrão fornece etapas de amostra para obter essa funcionalidade. Para obter uma referência ao elemento de container do visualizador, você pode usar as seguintes linhas de código:

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

Onde `inner_container` é uma referência a um `DIV` elemento gerenciado pelo visualizador. Você quer que a caixa de diálogo seja filha disso `DIV`.

As etapas para localizar o elemento da caixa de diálogo modal e anexá-lo ao container acima são específicas para maiúsculas e minúsculas. Novamente, você pode buscar a ajuda de seu desenvolvedor de front-end familiarizado com a implementação do Quickview necessária.

No caso do site de amostra, a caixa de diálogo modal do Quickview é implementada como uma `DIV` com a ID modal quickview anexada diretamente ao documento `BODY`. Portanto, o código para mover essa caixa de diálogo para o container do visualizador é tão simples quanto o seguinte:

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
inner_container.appendChild(document.getElementById("quickview-modal"));
```

O código fonte completo é o seguinte:

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
     var categoryId=inData.categoryId; //categoryId
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   "initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(document.getElementById("quickview-modal"));
    }
   });
 s7interactivevideoviewer.init();
</script>
```

O site de demonstração final com o vídeo interativo totalmente integrado tem a seguinte aparência:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html)

## Uso do Quickviews para criar pop-ups personalizados {#using-quickviews-to-create-custom-pop-ups}

See [Using Quickviews to create custom pop-ups](/help/assets/custom-pop-ups.md).
