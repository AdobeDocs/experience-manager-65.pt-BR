---
title: Vídeos interativos
description: Saiba como trabalhar com vídeo interativo e vídeo para compra no Dynamic Media
uuid: c3ff6839-fff5-4709-8163-5c4245b80e6d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 04be55f2-c7d8-45ef-89e5-58856b971de5
docset: aem65
feature: Interactive Videos
role: User, Admin
exl-id: d118879d-c17b-43f3-9cc8-0405531b4d9f
source-git-commit: 9052ed3e89fdc67d94fc60bbff64d42255565767
workflow-type: tm+mt
source-wordcount: '6036'
ht-degree: 3%

---

# Vídeos interativos{#interactive-videos}

Você pode criar vídeos interativos com facilidade (também conhecidos como vídeos que podem ser comprados), que impulsionam a conversão diretamente do vídeo. O envolvimento do cliente com o vídeo ocorre em um painel ao lado do reprodutor de vídeo, onde as miniaturas de serviços, informações ou produtos relacionados são roladas para a exibição com base no que é apresentado no vídeo. Os clientes podem selecionar a miniatura e ser vinculados diretamente ao serviço, adicionar o item a um carrinho de compras para compra imediata ou ser vinculados a uma página da Web para obter mais informações.

Quando o vídeo termina, um resumo visual de todas as ofertas é exibido para orientar um plano de ação. Os clientes têm outra oportunidade de selecionar o item que desejam. Experiências acionáveis e específicas como essas aumentam os envolvimentos e as conversões do cliente.

Consulte também [Imagens interativas](/help/assets/interactive-images.md).

## Vídeo interativo em ação {#interactive-video-in-action}

Para ver um vídeo interativo e que pode ser comprado, selecione [Demonstrações ao vivo](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html), role até o **[!UICONTROL Mídia comprável]** na página e selecione o vídeo que pode ser comprado.

* Durante a reprodução, à medida que os produtos são usados no vídeo, o produto idêntico é exibido à direita como uma imagem em miniatura.

* Selecione a miniatura se desejar pausar o vídeo e abrir a exibição rápida do produto. Por exemplo, selecione a imagem em miniatura KitchenAid no vídeo para ver uma exibição de rotação de 360 graus do mixer ou amplie para ver os detalhes do mixer.

<!-- There was a link here that showed the video frame of an interactive video and when the reader selected the frame the video would play https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/AXIS/index.html. This now needs to call a new interactive video-->

![Um quadro de um vídeo interativo e que pode ser comprado](assets/chlimage_1-126.png) *Uma captura de quadro de vídeo de um vídeo interativo e que pode ser comprado.*

>[!NOTE]
>
>Se você criar um vídeo interativo para iniciar uma página da Web quando um usuário selecionar uma imagem em miniatura, alguns dispositivos impedirão que a página da Web pop-up seja aberta. Nesses casos, você deve alterar a configuração do bloqueador de pop-ups no dispositivo. Por exemplo, em um Apple iPhone 6, navegue até **[!UICONTROL Configurações]** > **Safari** > **Bloquear pop-ups** e deslize o controle para **[!UICONTROL Desligado]**. Agora, ao reproduzir um vídeo interativo e selecionar uma miniatura, você será avisado se quiser abrir o pop-up. Se você aceitar, a página da Web será aberta.

### Veja como os vídeos interativos são criados {#watch-how-interactive-videos-are-created}

Reproduzir uma apresentação sobre [como os vídeos interativos são criados](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveVideo) (7 minutos e 30 segundos).
Embora a apresentação em vídeo tenha a marca Assets on Demand, os princípios e etapas ainda se aplicam a Vídeo interativo no Adobe Experience Manager Assets.

### Webinário de soluções para o cliente do Adobe {#adobe-customer-success-webinar}

O webinário &quot;Uso de vídeo interativo, compartilhamento de links e compartilhamento do YouTube no Experience Manager Assets&quot; ensina como usar vídeo interativo e outros recursos para vincular eventos orientados por conversão ao conteúdo de marketing em vídeo.

>[!NOTE]
>
>[Uso de vídeo interativo, compartilhamento de links e compartilhamento do YouTube no Experience Manager Assets](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/).

## Início rápido: vídeos interativos {#quick-start-interactive-videos}

A descrição do fluxo de trabalho passo a passo a seguir foi projetada para ajudar você a começar a usar os vídeos interativos no Dynamic Media com rapidez.

Procure o **Exemplo** em algumas das tarefas de Início rápido. Ele contém um breve tutorial baseado nesta página da Web de demonstração inicial que *não* têm interatividade adicionada a ela ainda:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

Os **Exemplos** ajudam a ilustrar as etapas da integração de vídeos interativos em seu próprio site.

Ao concluir o tutorial na última seção de Exemplo, a página da Web de demonstração final com o vídeo interativo totalmente integrado será semelhante ao seguinte:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html)

Etapas de vídeo interativo:

1. **(Opcional) Identificar variáveis do Quickview** - Comece identificando variáveis dinâmicas usadas pela implementação do Quickview existente. As variáveis são usadas para mapear miniaturas de produtos ao Quickview do produto correspondente quando você cria o vídeo interativo. Consulte [(Opcional) Identificar variáveis do Quickview](#optional-identifying-quickview-variables).
   *Esta etapa só será necessária se todos os itens a seguir forem verdadeiros*:
   * Você deseja adicionar interatividade ao vídeo acionando o Quickview.
   * Sua implementação do Experience Manager faz *não* use uma estrutura de integração de comércio eletrônico para obter dados de produtos para o Experience Manager de qualquer solução de comércio eletrônico, como o IBM® WebSphere® Commerce, Elastic Path, Hybris ou Intershop. Consulte [Conceitos de comércio eletrônico no Experience Manager Assets](/help/commerce/cif-classic/administering/concepts.md).

1. **(Opcional) Criar uma predefinição do visualizador de vídeo interativo** - Personalize a aparência e o comportamento de vários componentes que compõem o reprodutor, como o depurador de vídeo e as miniaturas interativas.
Criar sua própria predefinição do visualizador de Vídeo interativo não é necessário se você pretende usar as predefinições do visualizador de Vídeo interativo prontas para uso `Shoppable_Video_Light` ou `Shoppable_Video_Dark` em vez disso.
Consulte [Criar uma predefinição do visualizador](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) (opcional) e [Considerações especiais para a criação de uma predefinição do Visualizador interativo](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset).

1. **Carregar um vídeo e seus ativos de imagem associados** - Carregue um vídeo e imagens associadas que você deseja tornar interativos.
Consulte [Carregar um vídeo e seus ativos em miniatura associados](#uploading-a-video-and-its-associated-thumbnail-assets).

   >[!NOTE]
   >
   >O formato de vídeo MXF ainda não é compatível com vídeos interativos no Dynamic Media.

1. **Adicionar interatividade ao vídeo** - Adicionar um ou mais segmentos de tempo ao vídeo. Em seguida, associe as miniaturas de imagem nesses segmentos de tempo. Atribua cada miniatura de imagem a uma ação, como um hiperlink, um Quickview ou um Fragmento de experiência.
(O método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, especialmente links para páginas do Experience Manager Sites.)
Conclua o publicando os ativos de vídeo interativos. A publicação cria o código incorporado ou o URL que você eventualmente copia e aplica à página de aterrissagem do site. Consulte [Adicionar interatividade ao vídeo](#adding-interactivity-to-your-video).
Consulte [Publicar ativos](/help/assets/publishing-dynamicmedia-assets.md).

1. **Adicione um vídeo interativo ao seu site ou ao seu site no Experience Manager** - Se você usa o Experience Manager Sites ou eCommerce, ou ambos, é possível adicionar o vídeo interativo a uma página da Web. Arraste o componente Mídia interativa para a página no Experience Manager. Consulte [Adicionar ativos do Dynamic Media às páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).
Use o código incorporado ou o URL para integrar o vídeo interativo às experiências do site. Consulte [Integre um vídeo interativo ao seu site](#integrating-an-interactive-video-with-your-website).
Se você estiver usando um WCM (Web Content Manager, gerenciador de conteúdo da Web) de terceiros, é necessário integrar o novo vídeo interativo à implementação existente do Quickview usada em seu site. Consulte [Integrar um vídeo interativo a uma visualização rápida existente](#integrating-an-interactive-video-with-an-existing-quickview).
   [Adicionar ativos do Dynamic Media às páginas](/help/assets/adding-dynamic-media-assets-to-pages.md)

## (Opcional) Identificar variáveis do Quickview {#optional-identifying-quickview-variables}

>[!NOTE]
>
>Essa tarefa só será necessária se o seguinte for verdadeiro:
>
>* Você deseja adicionar interatividade ao vídeo acionando o Quickview.
>* Sua implementação do Experience Manager faz *não* use uma estrutura de integração de comércio eletrônico para obter dados de produtos para o Experience Manager de qualquer solução de comércio eletrônico, como o IBM® WebSphere® Commerce, Elastic Path, Hybris ou Intershop. Consulte [Conceitos de comércio eletrônico no Experience Manager Assets](/help/commerce/cif-classic/administering/concepts.md).
>
Se sua implementação do Experience Manager usar eCommerce, você poderá ignorar essa tarefa e prosseguir para a próxima tarefa.

Comece identificando as variáveis dinâmicas usadas pela sua implementação do Quickview existente, para que você possa mapear as miniaturas de produtos para o Quickview do produto correspondente durante o processo de criação interativo de vídeos.

Ao adicionar segmentos de tempo a um vídeo, você atribui uma SKU (Stock Keeping Unit, Unidade de manutenção de estoque) e quaisquer variáveis adicionais a cada miniatura adicionada a um segmento. Essas variáveis são usadas posteriormente para exibir o produto Quickview correto.

É importante identificar corretamente quais variáveis são necessárias para acionar exclusivamente uma Quickview do produto.

Às vezes, basta consultar especialistas de TI responsáveis pela implementação existente do Quickview. Eles provavelmente conhecerão o conjunto mínimo de dados para identificar o Quickview no sistema. No entanto, também é possível simplesmente analisar o comportamento existente do código front-end.

A maioria das implementações do Quickview usa o seguinte paradigma:

* O usuário ativa um elemento da interface do usuário no site. Por exemplo, selecionar um botão &quot;Quickview&quot;.
* O site envia uma solicitação de Ajax para o backend a fim de carregar os dados ou o conteúdo da Visualização rápida, se necessário.
* Os dados do Quickview são traduzidos no conteúdo como preparação para renderização na página da Web.
* Por fim, o código de front-end renderiza visualmente esse conteúdo na tela.

A abordagem, portanto, é visitar diferentes áreas do seu site existente, onde o Quickview é implementado, acionar o Quickview e capturar o URL do Ajax enviado pela página da Web para carregar os dados ou conteúdo do Quickview.

Normalmente, não há necessidade de usar ferramentas de depuração especializadas. Navegadores da Web modernos possuem inspetores da Web que fazem um trabalho adequado. A seguir estão alguns exemplos de navegadores da Web que incluem inspetores da Web:

* Para ver todas as solicitações HTTP de saída no Google Chrome, pressione **F12** (Windows) ou **Command+Opções+I** (Mac) para abrir o painel Ferramentas do desenvolvedor e selecione a **Rede** guia.

* No Firefox, você pode ativar o plug-in do Firebug pressionando **F12** (Windows) ou **Command+Option+I** (Mac) e utilizar sua **`[Net]`** ou você pode usar a ferramenta Inspetor integrada e sua guia Rede.

* No Internet Explorer, ative a ferramenta de depuração pressionando **F12**.

Quando o monitoramento de rede estiver ativado no navegador, acione o Quickview na página.

Agora, localize o URL do Ajax Quickview no log de rede e copie o URL gravado para análise futura. Normalmente, quando você aciona a Visualização rápida, várias solicitações são enviadas para o servidor. Normalmente, o URL do Ajax Quickview é um dos primeiros na lista. Ele tem uma parte ou um caminho de sequência de consulta complexo e seu tipo de resposta MIME é `text/html`, `text/xml`ou `text/javascript`.

Durante esse processo, é importante visitar diferentes áreas do site, com diferentes categorias e tipos de produtos. O motivo é que os URLs do Quickview podem ter partes comuns para uma determinada categoria de site, mas só podem ser alteradas se você visitar uma área diferente do site.

No caso mais simples, a única parte variável no URL do Quickview é o SKU do produto. Nesse caso, o valor do SKU do produto é o único dado necessário para adicionar miniaturas a um segmento de tempo no vídeo interativo no Experience Manager.

No entanto, em casos complexos, o URL do Quickview tem diferentes elementos variáveis, além do SKU do produto, como ID de categoria, código de cor e código de tamanho. Nesses casos, cada elemento se torna uma variável separada na definição de dados em miniatura no Experience Manager.

Considere os seguintes exemplos de URLs do Quickview e as variáveis de miniatura resultantes:

<table>
  <tbody>
  <tr>
    <td><p>SKU única, encontrada na cadeia de caracteres de consulta.</p> </td>
    <td><p>Os URLs de Quickview gravados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>A única parte variável no URL é o valor da variável <code>productId=</code> parâmetro da sequência de consulta e é claramente um valor de SKU. Portanto, suas miniaturas só precisam de campos de SKU preenchidos com valores como <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU única, encontrada no caminho do URL.</p> </td>
    <td><p>Os URLs de Quickview gravados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>A parte variável está na última parte do caminho e se torna o valor SKU das miniaturas de Experience Manager: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID de categoria na cadeia de caracteres de consulta.</p> </td>
    <td><p>Os URLs de Quickview gravados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>Nesse caso, há duas partes variáveis no URL. O SKU é armazenado no <code>prodId</code> e a ID da categoria for armazenada na variável <code>category=</code> parâmetro.</p> <p>Dessa forma, as definições de miniatura são pares. Ou seja, um valor de SKU e uma variável extra chamada <code>categoryId</code>. Os pares resultantes são os seguintes:</p>
    <ul>
      <li>O SKU é <code>305466</code> e <code>categoryId</code> é <code>1100004</code></li>
      <li>O SKU é <code>310181</code> e <code>categoryId</code> é <code>1100004</code></li>
      <li>O SKU é <code>308706</code> e <code>categoryId</code> é <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Exemplo**

Quando a abordagem acima é aplicada ao site Exemplo, você tem uma página da Web com várias miniaturas de produtos, cada uma com um botão &quot;VEJA MAIS&quot;:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

Depois de ativar todas as exibições rápidas de produtos disponíveis na página, você obtém a seguinte lista de solicitações do QuickView feitas no back-end:

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

Observando as chamadas do servidor, você pode ver que as informações específicas do produto estão presentes somente no caminho da solicitação. Você também percebe que a sequência de consulta não é usada e que há dois tipos distintos de dados envolvidos:

* O primeiro tipo são velas, almofadas, móveis e utensílios de vidro. Você pode chamar isso de &quot;categoria de produto&quot;.
* O segundo tipo é o código do produto, como 233916597. Você pode supor que seja &quot;SKU do produto&quot;.

Dadas essas informações, todo o URL do Quickview tem o seguinte padrão:

`/datafeed/$categoryId$-$SKU$.json`

Com base nessa análise, você conclui que pode usar as duas variáveis a seguir para as miniaturas: `categoryId` e `SKU`.

Agora você está pronto para fazer upload de um vídeo e de seus ativos em miniatura associados.

## (Opcional) Criar uma predefinição do visualizador de vídeo interativo {#optional-creating-an-interactive-video-viewer-preset}

Ignore essa tarefa e vá para a próxima se pretender usar qualquer um dos tipos de predefinição padrão do visualizador de Vídeo interativo, pronto para uso `Shoppable_Video_dark` ou `Shoppable_Video_light`.

Quando uma miniatura é selecionada no ambiente de criação, uma pré-visualização da caixa de diálogo Visualização rápida é exibida.

![chlimage_1-21](assets/chlimage_1-127.png)

Opcionalmente, é possível criar sua própria predefinição personalizada do visualizador de Vídeo interativo. É possível determinar, entre outras coisas, o estilo do reprodutor de vídeo, as miniaturas interativas e a exibição da grade de miniaturas que aparece no final do vídeo.

Uma predefinição do visualizador de Vídeo interativo renderiza corretamente o vídeo e todos os segmentos de linha do tempo adicionados. Ela também usa um exemplo de Quickview padrão ao selecionar uma miniatura de produto no modo de Visualização, para que você possa testar a interatividade antes de publicar.

Após salvar a predefinição do visualizador, seu estado é automaticamente definido como **Ligado** na página Predefinições do visualizador. Esse estado significa que está visível no componente do Dynamic Media e sempre que você visualiza um vídeo com ele. Certifique-se de publicar manualmente a nova predefinição do visualizador.

Consulte [Criar uma nova predefinição do visualizador](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) para criar sua própria predefinição do visualizador de Vídeo interativo.

## Carregar um vídeo e seus ativos em miniatura associados {#uploading-a-video-and-its-associated-thumbnail-assets}

Se você já tiver carregado os ativos de vídeo e miniatura, prossiga para [Adicionar interatividade ao vídeo](#adding-interactivity-to-your-video).

>[!NOTE]
O formato de vídeo MXF ainda não é compatível com o uso de Vídeos interativos no Dynamic Media.

Se você carregou os vídeos ou imagens incorretos, ou se deseja excluir os vídeos ou imagens carregados que não são mais necessários, consulte [Excluir ativos](/help/assets/manage-assets.md#deleting-assets).

Para fazer upload de um vídeo e de seus ativos em miniatura associados:

1. Carregue o vídeo e os ativos em miniatura associados na pasta ou pastas desejadas.

   Consulte [Fazer upload de ativos](/help/assets/manage-assets.md).
Consulte [Fazer upload de ativos usando o agendamento de trabalhos FTP](/help/assets/manage-assets.md).

   Agora, adicione interatividade ao vídeo.

## Adicionar interatividade ao vídeo {#adding-interactivity-to-your-video}

Adicione segmentos de linha do tempo a um vídeo usando o editor visual no local na página Criar vídeo interativo.

Depois de adicionar segmentos de linha do tempo, você adiciona imagens em miniatura em cada segmento. Para cada miniatura adicionada, aplique uma ação a ela. Por exemplo, você pode aplicar uma Visualização rápida à miniatura, atribuir um hiperlink a ela ou um Fragmento de experiência.

Consulte [Fragmentos de experiência](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
As ferramentas de compartilhamento de redes sociais no Vídeo interativo não são compatíveis quando você incorpora o visualizador em um Fragmento de experiência. Para contornar esse problema, é possível usar ou criar predefinições do visualizador que não tenham ferramentas de compartilhamento de redes sociais. Essas predefinições do visualizador permitem incorporá-lo com sucesso aos Fragmentos de experiência.

>[!NOTE]
O método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas do Experience Manager Sites.

As opções Desfazer e Refazer, próximas ao canto superior direito da página, são compatíveis durante a sessão de criação/edição atual.

Depois de salvar o vídeo interativo, ele é aberto imediatamente na Pré-visualização. Ali, é possível selecionar uma predefinição do visualizador de Vídeo interativo e reproduzir o vídeo para ver uma representação aproximada de como ele aparece para os clientes.

**Para adicionar interatividade ao vídeo:**

1. Na visualização de Ativos, navegue até o vídeo que você carregou e deseja tornar interativo.
1. Siga uma das seguintes opções:

   * Passe o mouse sobre a imagem e selecione **[!UICONTROL Selecionar]** (ícone de marca de seleção). Na barra de ferramentas, selecione **[!UICONTROL Editar]**.

   * Passe o mouse sobre a imagem e selecione **[!UICONTROL Mais ações]** (ícone de três pontos) **[!UICONTROL > Editar]**.

   * Selecione a imagem para abri-la na página Exibição de detalhes. Na barra de ferramentas, selecione **[!UICONTROL Editar]**.

1. Na página Criar vídeo interativo, siga um destes procedimentos:

   * Para começar a reproduzir o vídeo, selecione a **[!UICONTROL Reproduzir]** botão. Quando um produto, serviço ou detalhe específico que você deseja destacar aparecer, selecione **[!UICONTROL Adicionar segmento]** na barra de ferramentas. Repita até chegar ao fim do vídeo.

      Para cada segmento de tempo que você adicionar, atribua uma ou mais imagens em miniatura a ele e, em seguida, vincule essas miniaturas às páginas de produto do Quickview para que os clientes as comprem ou às páginas da Web para obter mais informações.

   * Para começar a reproduzir o vídeo, selecione a **[!UICONTROL Reproduzir]** botão. Quando um produto, serviço ou detalhe específico que você deseja destacar aparecer, selecione **[!UICONTROL Pausar]**. Selecionar **[!UICONTROL Adicionar segmento]**.

      Continue a reproduzir e pausar o vídeo em pontos ao longo da linha do tempo em que deseja adicionar um segmento até chegar ao fim do vídeo.

1. (Opcional) Arraste a barra no **[!UICONTROL Controle Deslizante de Escala da Linha do Tempo]** da esquerda para aumentar ou da direita para diminuir o zoom, para controlar quantos detalhes são vistos dos segmentos adicionados.

   ![chlimage_1-22](assets/chlimage_1-128.png)

   Dependendo da duração do vídeo, a Duração do segmento assume os seguintes valores como padrão:

   <table>
      <tbody>
        <tr>
        <td><strong>Se a duração do vídeo for...</strong></td>
        <td><strong>A configuração padrão de Duração do segmento é...</strong></td>
        </tr>
        <tr>
        <td>3 minutos ou mais</td>
        <td>60 segundos</td>
        </tr>
        <tr>
        <td>2-3 minutos</td>
        <td>30 segundos</td>
        </tr>
        <tr>
        <td>1-2 minutos</td>
        <td>20 segundos<br /> </td>
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

   A linha do tempo do vídeo usa tanto espaço na tela quanto o que é disponibilizado para ele. Dessa forma, ao redimensionar o navegador, os segmentos adicionados mantêm a largura correta.

   Para ilustrar, as três capturas de tela a seguir estão usando o mesmo vídeo. Observe que a largura de cada segmento muda dependendo da configuração de Escala da linha do tempo.

   ![chlimage_1-23](assets/chlimage_1-129.png)

   Captura de tela A

   A captura de tela A acima mostra a exibição padrão de um vídeo de produto de 29 segundos. A Escala da linha do tempo é definida como o padrão de 5 segundos.

   ![chlimage_1-130](assets/chlimage_1-130.png)

   Captura de tela B

   Na Captura de tela B acima, o controle deslizante Escala da linha do tempo foi arrastado do padrão de 5 segundos para 3 segundos. Observe que os carimbos de data e hora individuais da Escala da linha do tempo agora estão todos definidos em intervalos de 3 segundos.

   ![chlimage_1-25](assets/chlimage_1-131.png)

   Captura C

   Na Captura de tela C acima, a configuração Escala da linha do tempo foi movida para 8 segundos. Observe como os segmentos que contêm miniaturas de produtos encolheram. Reduzir dessa maneira é útil se você tiver um vídeo longo e quiser ter uma visão geral de mais segmentos que normalmente se encaixariam na largura da página.

1. (Opcional) Siga qualquer um destes procedimentos:

   * Para ajustar a hora inicial e a hora final de um segmento.

      Selecione um segmento e arraste o oval azul à esquerda ou à direita para ajustar a hora inicial ou final, respectivamente. O quadro do vídeo exibido se move para o momento apropriado no vídeo, com base nos ajustes. O movimento do segmento da linha do tempo é restrito com base em quaisquer segmentos adjacentes na linha do tempo. O tempo mínimo de segmento permitido é de um segundo.

      Use os seguintes atalhos de navegação para verificar e ajustar rapidamente os segmentos de vídeo:

      * Para buscar o vídeo diretamente no início desse segmento, selecione a oval azul à esquerda.
      * Para buscar o vídeo diretamente no final desse segmento, selecione o oval azul à direita.
      * Para retornar a reprodução de vídeo para o início desse segmento, selecione o segmento inteiro.

   ![chlimage_1-26](assets/chlimage_1-132.png)

   Reposicionamento do final de um segmento da linha do tempo

   * Para excluir um segmento

      Selecione o último segmento na linha do tempo e, na barra de ferramentas, selecione **[!UICONTROL Excluir segmento]**. Se dois ou mais segmentos forem selecionados, o recurso Excluir segmento ficará desativado.

      Você só pode excluir o último segmento. Por exemplo, se você deseja excluir todos os segmentos na linha do tempo, sempre é necessário selecionar o último e selecionar **[!UICONTROL Excluir segmento]**.


1. Selecione um segmento de tempo ao qual você deseja associar uma ou mais imagens em miniatura.
1. À direita do vídeo, selecione a **[!UICONTROL Conteúdo]** guia.
1. Na guia Conteúdo, selecione **[!UICONTROL Selecionar ativos]**, navegue e selecione todos os ativos de imagem que deseja usar com o vídeo. Os ativos selecionados são adicionados ao painel Seletor de ativos na guia Conteúdo.

1. No seletor de ativos abaixo da guia Conteúdo, siga um destes procedimentos:

   <table>
      <tbody>
        <tr>
        <td>Para associar uma miniatura ao segmento de linha do tempo selecionado</td>
        <td><p>Selecione a imagem no painel seletor de ativos à direita.</p> <p>Você pode adicionar quantas miniaturas desejar a um segmento da linha do tempo. Para cada imagem selecionada, uma marca de seleção aparece sobre a imagem no seletor de ativos.</p> </td>
        </tr>
        <tr>
        <td>Para remover uma miniatura do segmento de linha do tempo selecionado</td>
        <td><p>Siga um destes procedimentos:</p>
          <ul>
          <li>No painel do seletor de ativos, selecione uma imagem com uma marca de seleção para desmarcá-la. O ativo de imagem é removido do segmento da linha do tempo.<br /> </li>
          <li>No segmento da linha do tempo selecionado, selecione uma imagem e, na barra de ferramentas, selecione <strong>Excluir produto</strong>.</li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![Seletor de ativos](assets/chlimage_1-133.png)

   Selecionar uma imagem no painel seletor de ativos a adiciona ao segmento da linha do tempo selecionado.

1. Selecione uma única imagem em miniatura dentro de um dos segmentos da linha do tempo e selecione a **[!UICONTROL Ações]** guia.
1. Siga um destes procedimentos:
   <table> 
    <tbody> 
      <tr> 
      <td>Para associar a imagem em miniatura selecionada a uma visualização rápida</td> 
      <td><p>Em Tipo de ação, selecione <strong>Quickview</strong>.</p> <p>Se você for um cliente do Experience Manager Sites e do Ecommerce:</p> 
       <ul> 
       <li>Observe que o campo de texto Valor do SKU é pré-preenchido com o SKU (Unidade de manutenção de estoque) do produto selecionado, que é um identificador exclusivo para cada produto ou serviço distinto que você está oferecendo. Esse valor é preenchido automaticamente quando a imagem é associada a um produto no Experience Manager Commerce.</li> 
       <li>Se o SKU pré-preenchido estiver incorreto, selecione o ícone Seletor de produto (lupa) para abrir a página Selecionar produto. Selecione o produto que deseja usar e marque a marca de seleção no canto superior direito da página para que você possa retornar ao Editor de vídeo interativo.</li> 
       </ul> <p> Se você estiver <em>não</em> um cliente do Experience Manager Sites ou do Ecommerce</p> 
       <ul> 
       <li>Consulte <a href="/help/assets/carousel-banners.md#identifying-hotspot-and-image-map-variables">Identificação de variáveis de ponto de acesso</a>. As variáveis devem ser definidas.  </li> 
       <li>Por padrão, esse campo SKU usa o nome de arquivo do ativo de imagem sem a extensão. Se você seguir uma convenção de nomenclatura padrão para seus arquivos com base no SKU, esse nome de arquivo normalmente não exigirá edições adicionais. </li> 
       <li>Caso contrário, edite o valor padrão e insira o valor SKU correto. No campo de texto Valor do SKU, digite o SKU (Unidade de manutenção de estoque) do produto, que é um identificador exclusivo para cada produto ou serviço distinto que você oferece. O valor SKU inserido preenche automaticamente a parte variável do modelo Quickview para que o sistema saiba como associar a imagem selecionada a uma Quickview de SKU específica.</li> 
       </ul> <p>(Opcional) Se houver outras variáveis na Visualização rápida que você deve usar para identificar melhor um produto, selecione <strong>Adicionar variável genérica</strong>. No campo de texto, especifique uma variável extra. Por exemplo, <code>category=Womens</code> é uma variável adicionada.</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>Para associar a imagem em miniatura selecionada a um hiperlink</td> 
      <td><p>Em Tipo de ação, selecione <strong>Hiperlink</strong>, siga um destes procedimentos:</p> 
       <ul> 
       <li>Se você for um cliente do Experience Manager Sites, selecione o ícone Seletor de sites (pasta) para navegar até uma página da Web. O método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas do Experience Manager Sites.</li> 
       <li>Se você for um cliente independente do Dynamic Media, no campo de texto HREF, especifique o caminho completo do URL para uma página da Web vinculada.</li> 
       </ul> <p>Certifique-se de especificar se o link deve ser aberto em uma nova guia do navegador ou na guia atual.</p> </td> 
      </tr> 
      <tr> 
      <td>Para associar a imagem em miniatura selecionada a um Fragmento de experiência</td> 
      <td><p>Em Tipo de ação, selecione <strong>Fragmento de experiência</strong>, faça o seguinte:<p> 
       <ul> 
       <li>Se você for um cliente do Experience Manager Sites, selecione o ícone Pesquisar (lupa) para abrir a página Fragmento de experiência. Selecione o Fragmento de experiência que deseja usar e selecione <strong>Selecionar </strong>no canto superior direito da página para que você possa retornar ao painel Ações na página anterior.<br /> Consulte <a href="/help/sites-authoring/experience-fragments.md">Fragmentos de experiência</a>.</li> 
      </ul> 
       <ul> 
       <li>Especifique a largura e a altura do Fragmento de experiência como deseja que ele seja exibido no vídeo.</li>
       </ul><strong>Nota</strong>: as ferramentas de compartilhamento de redes sociais no Vídeo interativo não são compatíveis quando você incorpora o visualizador em um Fragmento de experiência. Para contornar esse problema, é possível usar ou criar predefinições do visualizador que não tenham ferramentas de compartilhamento de redes sociais. Essas predefinições do visualizador permitem incorporá-lo com sucesso aos Fragmentos de experiência.</p></tr>&lt; 
      <tr> 
      <td>Para editar uma ação já atribuída a uma imagem em miniatura</td> 
      <td>Em um segmento de linha do tempo, selecione uma imagem em miniatura que tenha um vínculo em cadeia à direita de seu rótulo de texto. O vínculo de cadeia indica que uma ação está atribuída a ela. Selecione o <strong>Ações</strong> para que você possa fazer as alterações.</td> 
      </tr> 
      <tr> 
      <td>Para alterar o rótulo do texto de uma imagem em miniatura</td> 
      <td><p>Por padrão, o rótulo de texto usa a tag da imagem em miniatura <code>Title</code> campo de metadados. Se <code>Title</code> não estiver presente, o nome de arquivo da imagem em miniatura será usado, mas sem a extensão.</p> <p>Para alterar o rótulo do texto de uma imagem em miniatura, sob o <strong>Ações </strong>, logo abaixo do ativo de imagem que é exibido, insira o texto desejado. Consulte a captura de tela abaixo.</p> <p>O novo rótulo de texto é usado somente pelo próprio reprodutor de vídeo e pelo texto em miniatura exibido no segmento da linha do tempo. A alteração do rótulo não afeta o campo de metadados Título da imagem em miniatura nem seu nome de arquivo.</p> </td> 
      </tr> 
      <tr> 
      <td>Para reverter uma alteração:</td> 
      <td>Próximo ao canto superior direito da página, selecione <strong>Desfazer</strong> ou <strong>Refazer</strong>.</td> 
      </tr> 
    </tbody> 
   </table>

   ![experiencefragment_interactivevideos](assets/experiencefragment_interactivevideos.png)

   Um novo rótulo de texto é adicionado à imagem em miniatura.

1. Siga uma das seguintes opções:

   * Repita as etapas 6 a 11 para adicionar mais imagens em miniatura a segmentos da linha do tempo em seu vídeo.
   * Prossiga para a etapa opcional 13.

1. (Opcional) Siga um destes procedimentos:

   * **[!UICONTROL Mesclar segmento]** - É possível combinar dois segmentos adjacentes (com ou sem miniaturas de produto atribuídas a eles) em um segmento.

      Na linha do tempo, selecione dois ou mais segmentos contíguos que você deseja mesclar em um. Não há alças de arrastar ovais azuis nos dois segmentos selecionados na captura de tela abaixo.

      Selecionar **[!UICONTROL Mesclar segmento]** na barra de ferramentas.
   ![chlimage_1-134](assets/chlimage_1-134.png)

   Mesclar dois segmentos de cinco segundos selecionados em um segmento de dez segundos.

   * **[!UICONTROL Dividir segmento]** - É possível dividir um único segmento em dois segmentos com tempo igual. Se houver miniaturas de produtos já atribuídas ao segmento, as miniaturas serão combinadas no segmento esquerdo.

      Na linha do tempo, selecione um segmento que deseja dividir pela metade e selecione **[!UICONTROL Dividir segmento]** na barra de ferramentas.

      Selecionar dois ou mais segmentos desativa o **[!UICONTROL Dividir segmento]** recurso.
   ![chlimage_1-135](assets/chlimage_1-135.png)

   Dividir um segmento de dez segundos selecionado em dois segmentos de cinco segundos cada.

1. Próximo ao canto superior direito do **[!UICONTROL Criar vídeo interativo]** é exibido o nome da predefinição do visualizador selecionada no momento usada com o vídeo. Selecione o nome se quiser selecionar outra predefinição do visualizador.

   Por exemplo, a variável `Shoppable_Video_light` a predefinição do visualizador permite reproduzir o vídeo com uma área de exibição branca ao lado do vídeo. A área de exibição é onde as imagens em miniatura selecionáveis são exibidas durante a reprodução. A variável `Shoppable_Video_dark` a predefinição do visualizador permite reproduzir o vídeo com uma área de exibição preta ao lado do vídeo.

   Se você criou sua própria predefinição do visualizador de Vídeo interativo, a verá na lista de predefinições que podem ser escolhidas.

   Quando terminar, selecione **[!UICONTROL Salvar]**.

   >[!NOTE]
   Ao salvar o vídeo interativo, um arquivo associado é automaticamente salvo com ele. `.vtt` A variável `.vtt` o arquivo é salvo na `_VTT` pasta na raiz de **[!UICONTROL Assets]**. O arquivo e a pasta são necessários para que o vídeo interativo seja reproduzido corretamente no site. Sendo assim, não mova, edite ou exclua a pasta `_VTT` ou seu conteúdo.

1. Publique o vídeo interativo. A publicação cria o código incorporado ou o URL que você eventualmente copia e cola nas experiências do site.

   Se você adicionou interatividade com o Quickview, use apenas o código incorporado; se adicionou interatividade com páginas da Web com hiperlink, você também pode usar o URL publicado. Observe, no entanto, que o método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas do Experience Manager Sites.

   Consulte [Publicar ativos](publishing-dynamicmedia-assets.md).

   >[!NOTE]
   Para publicar um vídeo que pode ser comprado com o Quickview, publique também cada um dos ativos de imagem relacionados do vídeo na sua área de comércio, separadamente.

   Depois de adicionar segmentos de linha do tempo e publicar o vídeo interativo, você está pronto para adicioná-lo à página de aterrissagem existente do site. Consulte [Integre um vídeo interativo ao seu site](#integrating-an-interactive-video-with-your-website).

## Publicar ativos de vídeo interativos {#publishing-interactive-video-assets}

Consulte [Publicar ativos](/help/assets/publishing-dynamicmedia-assets.md) para obter detalhes sobre como publicar ativos de vídeo interativos.

## Integre um vídeo interativo ao seu site {#integrating-an-interactive-video-with-your-website}

Após carregar um vídeo, adicionar segmentos de linha do tempo a ele e publicar o vídeo interativo, você está pronto para adicioná-lo ao seu site existente.

Se você for um cliente do Experience Manager Sites, poderá adicionar o vídeo interativo arrastando o componente de Mídia interativa para sua página. Consulte [Adicionar ativos do Dynamic Media a páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

Se você for um cliente independente do Experience Manager Assets, poderá adicionar manualmente o vídeo interativo ao seu site, conforme descrito nesta seção.

1. Copie o código ou URL incorporado do vídeo interativo publicado.
Consulte [Incorporar o visualizador de vídeo ou imagem em uma página da Web](/help/assets/embed-code.md).
Se você adicionou interatividade com o Quickview, use apenas o código incorporado; se adicionou interatividade com páginas da Web com hiperlink, você também pode usar o URL publicado. Observe, no entanto, que o método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas do Experience Manager Sites.

1. No código da página da Web do público-alvo, identifique onde o vídeo estático está localizado.
1. Remova o vídeo estático e substitua o código pelo código incorporado ou URL que você copiou do Experience Manager Assets, como está.
O código incorporado copiado é definido para um ambiente responsivo, de modo que se ajuste automaticamente à área ocupada anteriormente pelo vídeo estático.

>[!NOTE]
Nesse momento, se você tiver adicionado interatividade somente com páginas da Web com hiperlink, está concluído.
No entanto, se você adicionou qualquer interatividade para acionar uma Visualização rápida, as miniaturas ao lado do vídeo interativo serão somente para fins de exibição; elas ainda não estão integradas à Visualização rápida existente. Nesse caso, agora você deve integrar o vídeo interativo ao Quickview existente em seu site.

**Exemplo**

Usando o site de demonstração como exemplo:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

Observe que o código incorporado é padrão:

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

A integração é tão simples quanto remover o código de inserção do vídeo e substituí-lo pelo código de inserção interativo do vídeo do Experience Manager. Você pode ver o resultado no URL a seguir. Embora ele mostre um Vídeo interativo presente na página, ainda não está integrado à exibição rápida existente:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html)

## Integrar um vídeo interativo a uma visualização rápida existente {#integrating-an-interactive-video-with-an-existing-quickview}

>[!NOTE]
Essa tarefa só se aplica se você for um cliente independente do Experience Manager Assets.

A última etapa desse processo é integrar seu vídeo interativo a uma implementação do Quickview existente usada em seu site. Não há solução para a integração que funcione para todos os casos. Cada implementação do Quickview é exclusiva. Dessa forma, é necessária uma abordagem específica que envolva a assistência de um profissional de TI de front-end.

A implementação existente do Quickview normalmente representa uma cadeia de ações inter-relacionadas que ocorrem na página da Web na seguinte ordem:

1. Um usuário aciona um elemento na interface do usuário do seu site.
1. O código de front-end obtém um URL do Quickview com base no elemento de interface do usuário que foi acionado na etapa 1.
1. O código de front-end envia uma solicitação de AJAX usando o URL obtido na etapa 2.
1. A lógica de back-end retorna os dados ou o conteúdo correspondentes do Quickview ao código de front-end.
1. O código de front-end carrega os dados ou o conteúdo da visualização rápida.
1. Como opção, o código de front-end converte os dados do Quickview carregados em uma representação HTML.
1. O código de front-end exibe uma caixa de diálogo ou painel modal e renderiza o conteúdo de HTML na tela para o usuário final.

Essas chamadas não representam chamadas de API públicas independentes que podem ser chamadas pela lógica da página da Web de uma etapa arbitrária. Em vez disso, é uma chamada encadeada em que cada próxima etapa é ocultada na última fase (retorno de chamada) da etapa anterior.

Ao mesmo tempo em que o vídeo interativo substitui a etapa 1 e parcialmente a etapa 2, quando um usuário seleciona em uma miniatura dentro do vídeo interativo, essa interação do usuário é tratada pelo visualizador. O visualizador retorna um evento à página da Web que contém todos os dados de miniatura adicionados anteriormente ao Experience Manager.

Nesse manipulador de eventos, o código de front-end faz o seguinte:

* Escuta um evento emitido pelo vídeo interativo.
* Constrói um URL do Quickview com base nos dados de miniatura.
* Aciona o processo de carregar o Quickview do back-end e renderizá-lo na tela para exibição.

Além disso, o visualizador de Vídeo interativo suporta o modo de operação de tela cheia. O usuário final aciona a Visualização rápida selecionando uma miniatura sem sair da tela cheia. Para obter essa funcionalidade, altere o código de front-end para que a caixa de diálogo modal do Quickview seja anexada ao contêiner do visualizador. Não adicione o CORPO do documento ou algum outro elemento de página da Web que não esteja disponível quando o visualizador estiver no modo de tela cheia. O código que executa esse trabalho deve ouvir um ou mais retornos de chamada do visualizador que são enviados após o visualizador ser carregado na página.

O código incorporado retornado pelo Experience Manager já tem um manipulador de eventos pronto para uso em vigor. Ele é comentado como visto no seguinte trecho de código destacado:

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

Portanto, é necessário apenas remover o comentário do trecho de código destacado acima e substituir o corpo dos manipuladores fictícios pelo código específico da página da Web.

Há dois manipuladores de retorno de chamada padrão presentes no código incorporado padrão: `quickViewActivate` e `initComplete`. A variável `quickViewActivate` O manipulador é acionado quando uma miniatura é selecionada no visualizador. Use-o para integrar o visualizador à lógica de ativação do Quickview. A variável `initComplete` O manipulador do é acionado apenas uma vez quando o visualizador é carregado na página. Esse manipulador é usado para ajustar a localização da caixa de diálogo de Visualização rápida no DOM da página da Web.

O processo de construção do URL do Quickview é oposto ao processo de identificação das variáveis de miniatura abordadas anteriormente neste tópico. Usando os exemplos de URL do Quickview identificados anteriormente, você pode ver como o URL do Quickview é construído em cada caso:

<table>
  <tbody>
  <tr>
    <td><p>SKU única, encontrada na sequência de consulta</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
    <td>SKU única, encontrada no caminho do URL</td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
    <td><p>SKU e ID de categoria na cadeia de caracteres de consulta</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
  </tbody>
</table>

A última etapa para acionar o URL do Quickview e ativar o painel do Quickview provavelmente requer a assistência de um profissional de TI de front-end do seu departamento de TI. Eles têm o conhecimento para saber melhor como acionar com precisão a implementação do Quickview a partir da etapa adequada, tendo um URL do Quickview pronto para uso.

Você pode ver como essas etapas são aplicadas ao site de demonstração para integrar completamente um vídeo interativo ao código do Quickview. Anteriormente neste tópico, a estrutura do URL do Quickview foi identificada como a seguinte:

```xml
/datafeed/$CategoryId$-$SKU$.json
```

É fácil reconstruir esse URL dentro da variável `quickViewActivate` manipulador usando `categoryId` e `sku` campos disponíveis no `inData` objeto passado para o manipulador por meio do código do visualizador, como no seguinte:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

O site de demonstração está acionando a caixa de diálogo Quickview usando uma `loadQuickView()` função. Essa função aceita apenas um argumento, que é o URL de dados do Quickview. Assim, o último passo para integrar o vídeo interativo é adicionar a seguinte linha de código à `quickViewActivate` manipulador:

```xml
loadQuickView(quickViewUrl);
```

Por fim, verifique se a caixa de diálogo Quickview está anexada ao elemento de contêiner do visualizador. O código incorporado padrão fornece exemplos de etapas para obter essa funcionalidade. Para obter uma referência para o elemento de contêiner do visualizador, você pode usar as seguintes linhas de código:

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

Onde `inner_container` é uma referência a um `DIV` elemento gerenciado pelo visualizador. Você deseja que a caixa de diálogo seja filha disso `DIV`.

As etapas para localizar realmente o elemento de caixa de diálogo modal e anexá-lo ao contêiner acima fazem distinção entre maiúsculas e minúsculas. Novamente, você pode buscar a ajuda de seu desenvolvedor de front-end familiarizado com a implementação do Quickview necessária.

Se você usa o site de exemplo, a caixa de diálogo modal do Quickview é implementada como uma `DIV` com a ID modal de visualização rápida anexada diretamente ao documento `BODY`. Portanto, o código para mover essa caixa de diálogo para o contêiner do visualizador é tão simples quanto o seguinte:

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
inner_container.appendChild(document.getElementById("quickview-modal"));
```

O código-fonte completo é o seguinte:

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

O site final de demonstração com vídeo interativo totalmente integrado é semelhante ao seguinte:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html)

## Criar pop-ups personalizados usando o Quickview {#using-quickviews-to-create-custom-pop-ups}

Consulte [Criar pop-ups personalizados usando o Quickview](/help/assets/custom-pop-ups.md).
