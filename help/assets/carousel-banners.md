---
title: Banners em carrossel
description: Saiba como trabalhar com banners de carrossel no Dynamic Media
uuid: 73684a08-d84d-4665-ab89-3a1bf88ac5dd
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e26c7f7f-bdd7-421a-8614-ba48abf381d2
docset: aem65
translation-type: tm+mt
source-git-commit: 90c99e527a40bb663d4f32d8746b46cf34a2319f
workflow-type: tm+mt
source-wordcount: '4802'
ht-degree: 4%

---


# Banners em carrossel{#carousel-banners}

Os banners de carrossel permitem que os profissionais de marketing conduzam a conversão, criando facilmente conteúdo promocional giratório interativo e o entregando a qualquer tela.

Criar e modificar o conteúdo em destaque em banners promocionais pode ser demorado, limitando sua capacidade de publicar rapidamente novo conteúdo ou torná-lo mais direcionado. Os banners de carrossel permitem que você crie ou modifique rapidamente banners rotativos, adicione interatividade, como links de hotspots para detalhes de produtos ou recursos relacionados, e os entregue a qualquer tela, permitindo que você coloque o novo conteúdo promocional no mercado mais rapidamente.

Os banners de carrossel são designados por um banner com a palavra **[!UICONTROL CAROUSELSET]**:

![chlimage_1-438](assets/chlimage_1-438.png)

Em seu site, um banner de carrossel pode ser exibido da seguinte maneira:

![chlimage_1-439](assets/chlimage_1-439.png)

Aqui você pode navegar pelas imagens (clicando nos números). Além disso, os slides são girados automaticamente com base em um intervalo de tempo que você pode personalizar. As imagens adicionadas no banner do carrossel são compatíveis com hotspots e mapas de imagem, onde os usuários podem tocar ou acessar um hiperlink ou uma janela de visualização rápida.

Neste exemplo, um usuário tocou ou clicou em um mapa de imagem e acessou a janela de visualização rápida para obter luvas:

![chlimage_1-440](assets/chlimage_1-440.png)

## Veja como os banners de carrossel são criados {#watch-how-carousel-banners-are-created}

Assista a uma caminhada de 10 minutos e 33 segundos sobre [como os banners de carrossel são criados](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner). Você também aprenderá a pré-visualização, edição e entrega de banners de carrossel.

>[!NOTE]
>
>Usuários não administrativos devem ser adicionados ao grupo de usuários **[!UICONTROL do]** DAM para que possam criar ou editar banners do carrossel. Se tiver problemas para criar ou editar, consulte o administrador do sistema que pode adicioná-lo ao grupo de usuários **[!UICONTROL do]** DAM.

## Start rápido: Banners de carrossel {#quick-start-carousel-banners}

Para começar a trabalhar rapidamente:

1. [Identificar as variáveis](#identifying-hotspot-and-image-map-variables) de hotspot e mapa de imagem (somente para clientes que usam AEM Assets + Dynamic Media)

   Start identificando variáveis dinâmicas usadas pela implementação de visualização rápida existente para que você possa inserir os pontos de conexão e os dados do mapa de imagem corretamente durante o processo de criação do banner do carrossel no AEM Assets.

   >[!NOTE]
   >
   >Se você for um cliente da AEM Sites ou do Ecommerce, poderá usar o recurso integrado para navegar até páginas de produtos e pesquisar os skus existentes no catálogo de produtos. Não é necessário inserir manualmente as variáveis de hotspot ou mapa de imagem. Consulte as informações sobre como [configurar o eCommerce](/help/sites-administering/generic.md).
   >
   >
   >Se você for um cliente da AEM Assets e do Dynamic Media, inserirá manualmente os dados para pontos de conexão e mapas de imagem e, em seguida, integrará o URL publicado ou o código Incorporado ao seu sistema de gestão de conteúdo de terceiros.

1. Opcional: [crie uma predefinição do visualizador Conjunto de carrossel](/help/assets/managing-viewer-presets.md), conforme necessário.

   Se você for um administrador, poderá personalizar o comportamento e a aparência do carrossel criando sua própria predefinição do visualizador do carrossel. O principal benefício é que você pode reutilizar essa predefinição de visualizador personalizado para vários carrosséis. No entanto, os usuários também têm a opção de personalizar o comportamento e a aparência do carrossel diretamente durante a criação do carrossel. Essa é a abordagem preferida quando você deseja um design muito específico para um determinado carrossel.

1. [Carregue um banner](#uploading-image-banners)de imagem.

   Faça upload de banners de imagem que deseja tornar interativos.

1. [Criar um conjunto](#creating-carousel-sets)de carrossel.

   Em Conjuntos de carrosséis, os usuários navegam por imagens de banner e tocam em pontos de acesso ou mapas de imagem para acessar conteúdo relevante.

   Para criar um Conjunto de carrossel no Assets, toque em **[!UICONTROL Criar]** e selecione **[!UICONTROL Conjuntos de carrossel.]** Adicione ativos a slides e toque em **[!UICONTROL Salvar.]** Além disso, edite a aparência e o comportamento do carrossel diretamente no editor.

1. [Adicione pontos de acesso ou mapas de imagem a um banner de imagem.](#adding-hotspots-or-image-maps-to-an-image-banner)

   Adicione um ou mais pontos de acesso ou mapas de imagem a um banner de imagem e associe cada um a uma ação, como um link, uma visualização rápida ou um fragmento de experiência. Depois de adicionar pontos de acesso ou mapas de imagem, termine essa tarefa publicando o conjunto de carrossel. A publicação cria o código incorporado que você pode usar para copiar e aplicar à landing page do site.

   Consulte [(Opcional) Visualização de banners](#optional-previewing-carousel-banners) de carrossel - Opcional. Se desejar, você pode visualização uma representação do conjunto de carrossel e testar sua interatividade.

1. [Publique banners de carrossel.](#publishing-carousel-banners)

   Você publica um Conjunto de carrossel como faria com qualquer ativo. Em Ativos, navegue até o Conjunto de carrossel e selecione-o e toque em **[!UICONTROL Publicar.]** A publicação de um conjunto de carrossel ativa o URL e a string Incorporada.

1. Faça uma das seguintes opções:

   * [Adicione um banner de carrossel à página](#adding-a-carousel-banner-to-your-website-page) do site Você pode adicionar o URL do banner de carrossel ou incorporar o código que você copiou na página do site.

      * [Integre o banner do carrossel a um Quickview](#integrating-the-carousel-banner-with-an-existing-quickview)existente. Se você estiver usando um sistema de gestão de conteúdo da Web de terceiros, precisará integrar o novo banner do carrossel com a implementação do Quickview existente em seu site.
   * [Adicione um banner de carrossel ao seu site em AEM](/help/assets/adding-dynamic-media-assets-to-pages.md) Se você for um cliente da AEM Sites, poderá adicionar o conjunto de carrossel diretamente à página em AEM, usando o componente de Mídia interativa.


Se precisar editar Conjuntos de carrossel, consulte [edição de Conjuntos de carrossel.](#editing-carousel-sets) Além disso, você pode visualização e editar as propriedades [do Conjunto de](manage-assets.md#editing-properties)carrossel.

## Como identificar as variáveis de hotspot e mapa de imagem {#identifying-hotspot-and-image-map-variables}

Start identificando variáveis dinâmicas usadas pela implementação de visualização rápida existente para que você possa digitar os pontos de acesso ou os dados do mapa de imagem corretamente durante o processo de criação do conjunto de carrossel no AEM Assets.

Quando você adiciona pontos de acesso ou mapas de imagem a uma imagem de banner no AEM Assets, é necessário atribuir um SKU e variáveis adicionais opcionais a cada ponto de acesso ou mapa de imagem. Essas variáveis são usadas posteriormente para corresponder a pontos de acesso ou mapas de imagem com conteúdo de visualização rápida.

>[!NOTE]
>
>Se você for um cliente AEM Sites e/ou AEM Ecommerce, pule esta etapa. Não é necessário identificar manualmente as variáveis de hotspot ou mapa de imagem; você pode usar a integração com o Ecommerce para integração de produtos. Consulte as informações sobre como [configurar o eCommerce](/help/sites-administering/generic.md). Além disso, você pode usar o componente Interativo e adicioná-lo à sua página da Web.
>
>Se você for um cliente da AEM Assets ou da Mídia, publique o URL ou o código Incorporado e, em seguida, integre-se ao seu sistema de gestões de conteúdo de terceiros e identifique pontos de conexão e mapas de imagem manualmente.

É importante identificar corretamente o número e o tipo de variáveis a serem associadas aos dados do ponto de acesso ou do mapa de imagens. Cada ponto de conexão ou mapa de imagem adicionado a uma imagem de banner deve ter informações suficientes para identificar inequivocamente o produto no sistema de backend existente. Ao mesmo tempo, cada ponto de conexão ou mapa de imagem não deve incluir mais dados do que o necessário. O motivo é que isso tornaria o processo de entrada de dados excessivamente complexo e o gerenciamento de hotspots ou mapas de imagem mais propenso a erros.

Há diferentes maneiras de identificar um conjunto de variáveis a serem usadas para os dados de ponto de acesso ou mapa de imagem.

Às vezes, pode ser suficiente consultar especialistas de TI responsáveis pela implementação rápida da visualização, já que eles provavelmente saberão qual é o conjunto mínimo de dados necessário para identificar a visualização rápida no sistema. No entanto, na maioria dos casos, é possível simplesmente analisar o comportamento existente do código front-end.

A maioria das implementações de visualização rápida usa o seguinte paradigma:

* O usuário ativa um elemento da interface do usuário no site. Por exemplo, tocar em um botão **[!UICONTROL Exibição rápida]**.
* O site envia uma solicitação do Ajax para o backend para carregar os dados ou o conteúdo da visualização rápida, se necessário.
* Os dados de visualização rápida são traduzidos para o conteúdo em preparação para renderização na página da Web.
* Por fim, o código front-end exibe visualmente esse conteúdo na tela.

A abordagem então é visitar diferentes áreas do site existente onde o recurso de visualização rápida é implementado, acionar a visualização rápida e capturar o URL Ajax enviado pela página da Web para carregar os dados ou o conteúdo da visualização rápida.

Normalmente, não é necessário usar nenhuma ferramenta de depuração especializada. Os navegadores da Web modernos dispõem de inspetores da Web que fazem um trabalho adequado. A seguir estão alguns exemplos de navegadores da Web que incluem inspetores da Web:

* Para ver todas as solicitações HTTP de saída no Google Chrome, pressione F12 (Windows) ou Command-Option-I (Mac) para abrir o painel Ferramentas do desenvolvedor e toque na guia Rede.
* No Firefox, você pode ativar o plug-in Firebug pressionando F12 (Windows) ou Command-Option-I (Mac) e usar a guia Rede, ou usar a ferramenta Inspetor integrada e a guia Rede.

Quando o monitoramento de rede estiver ativado no navegador, dispare a visualização rápida na página.

Agora, encontre o URL Ajax de visualização rápida no registro de rede e copie o URL gravado para análises futuras. Na maioria dos casos, quando você aciona a visualização rápida, há várias solicitações que são enviadas para o servidor. Normalmente, o URL Ajax de visualização rápida é um dos primeiros na lista. Ele tem uma parte ou um caminho de sequência de query complexo, e seu tipo MIME de resposta é `text/html`, `text/xml`ou `text/javascript`.

Durante esse processo, é importante visitar diferentes áreas do seu site, com diferentes categorias e tipos de produtos. O motivo é que URLs de visualização rápida podem ter partes comuns para uma determinada categoria do site, mas são alteradas somente se você visitar uma área diferente do site.

No caso mais simples, a única parte variável no URL de visualização rápida é o SKU do produto. Nesse caso, o valor SKU é o único dado necessário para adicionar pontos de acesso ou mapas de imagem à imagem do banner.

No entanto, em casos complexos, o URL de visualização rápida tem elementos variáveis diferentes além do SKU, como ID de categoria, código de cor, código de tamanho e assim por diante. Nesses casos, cada elemento é uma variável separada no ponto de conexão ou na definição de dados do mapa de imagem no recurso de banner do carrossel.

Considere os seguintes exemplos de URLs de visualização rápida e suas variáveis de hotspot ou mapa de imagem resultantes:

<table>
 <tbody>
  <tr>
   <td>SKU único, encontrado na string do query.</td>
   <td><p>Os URLs de visualização rápida gravados incluem o seguinte:</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>A única parte variável no URL é o valor do parâmetro da string de <code>productId=</code> query e é claramente um valor SKU. Portanto, nossos pontos de acesso ou mapas de imagem só precisam de campos SKU preenchidos com valores como <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>SKU único, encontrado no caminho do URL.</td>
   <td><p>Os URLs de visualização rápida gravados incluem o seguinte:</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>A parte variável está na última parte do caminho e se torna o valor SKU dos pontos de acesso/mapas de imagem:<strong><code>6422350843</code>, <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU e ID da categoria na sequência do query.</td>
   <td><p>Os URLs de visualização rápida gravados incluem o seguinte:</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>Nesse caso, há duas partes diferentes no URL. O SKU é armazenado no <code>prodId</code> parâmetro e a ID da categoria é armazenada no <code>category=</code>parâmetro.</p> <p>Dessa forma, as definições de hotspot/mapa de imagem são pares. Ou seja, um valor de SKU e uma variável adicional chamada <code>categoryId</code>. Os pares resultantes são os seguintes:</p>
    <ul>
     <li><p>SKU é <strong><code>305466</code></strong> e <code>categoryId</code> é <code>1100004</code>.</p> </li>
     <li><p>SKU é <strong><code>310181</code></strong> e <code>categoryId</code> é <strong><code>1100004</code></strong>.</p> </li>
     <li><p>SKU é <strong><code>308706</code></strong> e <code>categoryId</code> é <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Carregando banners de imagem {#uploading-image-banners}

Se você já tiver carregado as imagens que deseja usar, vá para a próxima etapa, [Criando conjuntos](#creating-carousel-sets)de carrossel. Observe que as imagens usadas no carrossel devem ser carregadas após o Dynamic Media ter sido ativado.

Para fazer upload de banners de imagem, consulte [Fazer upload de ativos](/help/assets/manage-assets.md).

## Criação de conjuntos de carrossel {#creating-carousel-sets}

>[!NOTE]
>
>Usuários não administrativos devem ser adicionados ao grupo de usuários **[!UICONTROL do]** DAM para que possam criar ou editar banners do carrossel. Se tiver problemas para criar ou editar, consulte o administrador do sistema que pode adicioná-lo ao grupo de usuários **[!UICONTROL do]** DAM.

**Para criar um conjunto de carrossel**

1. Em Ativos, navegue até a pasta na qual deseja criar o Conjunto de carrossel e toque em **[!UICONTROL Criar > Conjunto de carrossel.]**
1. Na página Editor de banner do carrossel, toque em **[!UICONTROL Tocar para abrir o Seletor]** de ativos para selecionar a imagem para o primeiro slide.

   Na página do Editor de banner do carrossel, execute um dos procedimentos a seguir:

   * Perto do canto superior esquerdo da página, toque no ícone **[!UICONTROL Adicionar slide]** .

   * Próximo ao meio da página, toque em **[!UICONTROL Tocar para abrir o Seletor de ativos.]**
   Toque para selecionar os ativos que deseja incluir ao Conjunto de carrossel. Os ativos selecionados têm um ícone de marca de seleção sobre eles. When you are finished, near the upper-right corner of the page, tap **[!UICONTROL Select]**.

   Com o Seletor de ativos, procure por ativos ao digitar uma palavra-chave e tocar ou clicar em **[!UICONTROL Retornar.]** Aplique filtros para refinar os resultados da pesquisa. Filtre por caminho, coleção, tipo de arquivo e tag. Selecione o filtro e toque no ícone **[!UICONTROL Filtro]**, na barra de ferramentas. Altere a exibição ao tocar no ícone Exibir e selecionar **[!UICONTROL Exibição em coluna]**, **[!UICONTROL Exibição de cartão]** ou **[!UICONTROL Exibição em lista.]**

   Consulte [Trabalhar com seletores](/help/assets/working-with-selectors.md) para obter mais informações.

1. Continue a adicionar slides até que você tenha adicionado todas as imagens pelas quais deseja girar no Conjunto de carrossel.
1. (Opcional) Execute um dos procedimentos a seguir:

   * Se necessário, arraste o slide para reordenar as imagens na lista do conjunto.
   * Para excluir uma imagem, selecione-a e toque em **[!UICONTROL Excluir slide]** na barra de ferramentas.

   * Para aplicar uma predefinição, perto do canto superior direito da página, toque na lista suspensa predefinida e selecione uma predefinição para aplicar ao conjunto de uma vez.
   Para excluir um slide, toque ou clique no slide e toque ou clique em **[!UICONTROL Excluir slide]** na barra de ferramentas. Para mover um slide, toque no ícone de borda e segure e mova-se para o local desejado.

1. Depois de adicionar as imagens nos slides, adicione um ponto de acesso, um mapa de imagens ou ambos à imagem. Consulte [adicionar pontos de acesso ou mapas](#adding-hotspots-or-image-maps-to-an-image-banner)de imagem.
1. Você pode alterar o design visual e o comportamento dos conjuntos de carrossel tocando ou clicando nas guias Comportamento e Aparência e fazendo ajustes na aparência do banner do carrossel ou no comportamento dos componentes específicos. Consulte [Gerenciamento de predefinições](/help/assets/viewer-presets.md) do visualizador para obter mais informações sobre como usar o editor do visualizador.

   >[!NOTE]
   >
   >Para banners de carrossel, as seguintes opções podem ser ajustadas:
   >    * Duração que uma imagem exibe. Por padrão, cada imagem é exibida por 9 segundos.
   >    * Animação. Por padrão, cada transição de slide está esmaecida. Você pode mudar isso para uma transição de slide.
   >    * Estilo dos botões. Os usuários podem girar pelos banners tocando em cada ponto ou número. Você pode alterar o local em que os botões de indicador definidos aparecem (e se eles são numéricos ou de estilo pontilhado) e o tamanho deles.
   >    * Altere o estilo de realce de um mapa de imagem ou o ícone usado para pontos de acesso.
   >    * Antes de editar uma predefinição do visualizador, escolha o estilo do qual deseja basear a predefinição. Se você não fizer isso, ao start de editar a predefinição do visualizador, perderá todas as alterações se decidir mudar para uma predefinição diferente.

   >
   >Consulte Considerações [especiais para banners](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-a-carousel-banner-viewer-preset) de carrossel para obter instruções detalhadas e mais informações sobre o editor do visualizador.

   Você também pode pré-visualização como será o banner do carrossel. Consulte [(Opcional) Visualização de banners](#optional-previewing-carousel-banners)de carrossel.

1. Toque em **[!UICONTROL Salvar]** ao terminar.

## Adicionar pontos de conexão ou mapas de imagem a um banner de imagem {#adding-hotspots-or-image-maps-to-an-image-banner}

Você pode adicionar pontos de acesso ou mapas de imagem a um banner usando o editor Conjunto de carrossel.

Quando você adiciona pontos de acesso ou mapas de imagem, pode defini-los como uma exibição pop-up do Quickview, como um hiperlink ou um Fragmento de experiência.

Consulte Fragmento [de experiência](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
>
>Observe que as ferramentas de compartilhamento de mídia social no Carousel Banner não são suportadas quando você incorpora o visualizador em um Fragmento de experiência.
>
>Para contornar isso, você pode usar ou criar predefinições do visualizador que não tenham ferramentas de compartilhamento de mídia social. Essas predefinições do visualizador permitem que você as incorpore com êxito aos Fragmentos de experiência.

À medida que você adiciona pontos de acesso ou mapas de imagem a uma imagem, lembre-se de salvar seu trabalho. As opções Desfazer e Refazer, perto do canto superior direito da página, são suportadas durante a sessão atual de criação/edição.

Quando terminar de criar o banner do carrossel, você pode usar a Pré-visualização como opção para ver uma representação de como o banner do carrossel será exibido aos clientes.

Consulte [(Opcional) Visualização de banners de carrossel.](#optional-previewing-carousel-banners)

>[!NOTE]
>
>Quando você adiciona pontos de acesso a uma imagem em uma Imagem [](/help/assets/interactive-images.md) interativa ou em um banner de carrossel, as informações do ponto de acesso são armazenadas no mesmo local de metadados, em relação ao local da imagem e ao mdashtag, independentemente de ser uma Imagem interativa ou um banner de carrossel. Essa funcionalidade significa que você pode reutilizar facilmente a mesma imagem, juntamente com seus dados de ponto de conexão definidos, em qualquer um dos visualizadores.
Esteja ciente, no entanto, de que os Carousel Banners oferecem suporte para mapas de imagem em imagens que também podem conter pontos de conexão; uma imagem interativa não. Lembre-se disso se você pretende criar uma imagem interativa ou um banner de carrossel que use a mesma imagem. Você pode criar Imagens interativas e Banners de carrossel usando cópias separadas da mesma imagem.

>[!NOTE]
Se você estiver editando imagens interativas com pontos de acesso e recortar a imagem, seus pontos de acesso serão removidos.

Consulte também [Adição de mapas de imagem](/help/assets/image-maps.md).

**Para adicionar pontos de acesso ou mapas de imagem a um banner de imagem**

1. Em Ativos, navegue até o conjunto de carrossel que deseja tornar interativo.
1. Selecione o conjunto de carrossel e toque em **[!UICONTROL Editar.]** O Editor do visualizador do carrossel é aberto.
1. Selecione o slide que deseja tornar interativo.
1. Próximo ao canto superior esquerdo da página, toque em **[!UICONTROL Ponto de acesso]** ou **[!UICONTROL Mapa de imagem.]**
1. Execute um dos procedimentos a seguir:

   * Para pontos de conexão: Na imagem, toque em um local onde deseja que o ponto de acesso apareça.
   * Para mapas de imagem: Na imagem, clique em e arraste da parte superior esquerda para a parte inferior direita para criar a área do mapa de imagem. É possível ajustar o tamanho do mapa de imagem arrastando os cantos.

   Se necessário, arraste o ponto de acesso ou o mapa de imagem para um novo local. Adicione outros pontos de acesso ou mapas de imagem, conforme necessário.

   Para excluir um ponto de acesso ou mapa de imagem, toque na guia **[!UICONTROL Ações]**. No cabeçalho **[!UICONTROL Mapas e pontos de acesso]**, no menu suspenso **[!UICONTROL Tipo selecionado]**, selecione o nome do ponto de acesso ou mapa de imagem que deseja remover. Toque no ícone **[!UICONTROL Lixeira]**, ao lado do menu, e toque em **[!UICONTROL Excluir.]**

1. No campo de texto Nome, digite o nome do ponto de acesso ou do mapa de imagem. Esse nome também aparece na lista suspensa **[!UICONTROL Mapas e pontos de conexão]** . Fornecer um nome facilita a identificação do ponto de conexão ou do mapa de imagem se você decidir fazer alterações no mapa no futuro.
1. Execute um dos procedimentos a seguir na guia **[!UICONTROL Ações]** :

   * Toque em **[!UICONTROL Quickview.]**

      * Se você for um cliente do AEM Sites e do Ecommerce, toque no ícone Seletor de produto (lupa) para abrir a página Selecionar produto. Toque no produto que deseja usar e, em seguida, toque na marca de seleção no canto superior direito da página para retornar ao Editor de banner do carrossel.
      * Se você não for um cliente da AEM Sites ou do Ecommerce

         * Consulte [Identificação de variáveis](#identifying-hotspot-and-image-map-variables) de pontos de acesso, conforme desejado, para definir essas variáveis.
         * Em seguida, insira manualmente o valor SKU. No campo de texto Valor SKU, digite o SKU do produto (Stock Keeping Unit), que é um identificador exclusivo para cada produto ou serviço distinto que você oferta. O valor SKU inserido preenche automaticamente a parte variável do modelo de visualização rápida para que o sistema saiba associar o ponto de acesso tocado a uma visualização rápida do SKU específica.
         * (Opcional) Se houver outras variáveis na visualização rápida que você precisa usar para identificar um produto, toque em **[!UICONTROL Adicionar variável genérica.]** No campo de texto, especifique uma variável adicional. Por exemplo, categoria=Masculino é uma variável adicionada.

         * Consulte [Trabalhar com seletores](/help/assets/working-with-selectors.md) para obter mais informações.
   * Toque em **[!UICONTROL Hiperlink.]**

      * Se você for um cliente AEM Sites, toque no ícone Seletor de site (pasta) para navegar até um URL.
         >[!NOTE]
         O método baseado em URL de vinculação não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas do AEM Sites.

      * Se você for um cliente independente, no campo de texto HREF, especifique o caminho do URL completo para uma página da Web vinculada.

   Certifique-se de especificar se deseja abrir o link em uma nova guia do navegador (padrão recomendado) ou na mesma guia.

   Consulte [Trabalhar com seletores](/help/assets/working-with-selectors.md) para obter mais informações.

   * Tap **[!UICONTROL Experience Fragment.]**

      * Se você for um cliente AEM Sites, toque no ícone Pesquisar (lupa) para abrir a página Fragmento de experiência. Toque ou clique no Fragmento de experiência que você deseja usar e, em seguida, toque em Selecionar no canto superior direito da página para retornar à página de gerenciamento do Hotspot.
Consulte Fragmentos [de experiência](/help/sites-authoring/experience-fragments.md).

      * Especifique a largura e a altura do Fragmento de experiência como ele aparecerá no banner.

         >[!NOTE]
         Observe que as ferramentas de compartilhamento de mídia social no Carousel Banner não são suportadas quando você incorpora o visualizador em um Fragmento de experiência.
         Para contornar isso, você pode usar ou criar predefinições do visualizador que não tenham ferramentas de compartilhamento de mídia social. Essas predefinições do visualizador permitem que você as incorpore com êxito aos Fragmentos de experiência.
   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   Você também pode pré-visualização como será o banner do carrossel. Consulte [(Opcional) Visualização de banners](#optional-previewing-carousel-banners)de carrossel.

1. Toque em **[!UICONTROL Salvar.]**
1. Publique o conjunto de carrossel. A publicação cria o código incorporado ou o URL que você pode usar na página do site. Se você for um cliente da AEM Sites, poderá adicionar o conjunto de carrossel diretamente à sua página da Web.

   Consulte [Publicar ativos](/help/assets/publishing-dynamicmedia-assets.md).

   Consulte [Adicionar um conjunto de carrossel à landing page do site](#adding-a-carousel-banner-to-your-website-page)

## Edição de conjuntos de carrossel {#editing-carousel-sets}

>[!NOTE]
Usuários não administrativos devem ser adicionados ao grupo de usuários **[!UICONTROL do]** DAM para que possam criar ou editar banners do carrossel. Se tiver problemas para criar ou editar, consulte o administrador do sistema que pode adicioná-lo ao grupo de usuários **[!UICONTROL do]** DAM.

É possível executar várias tarefas de edição em Conjuntos de carrossel, como:

* Adicione slides a um conjunto de carrossel. Consulte também [Trabalhar com seletores](/help/assets/working-with-selectors.md).
* Reorganize os slides no Conjunto de carrossel.
* Exclua ativos no Conjunto de carrossel.
* Aplicar uma predefinição do visualizador.
* Exclua o conjunto de carrossel.
* Adicione ou edite pontos de acesso e mapas de imagem. Consulte também [Trabalhar com seletores](/help/assets/working-with-selectors.md).

**Para editar um conjunto de carrossel**

1. Execute um dos procedimentos a seguir:

   * Passe o mouse sobre um ativo do Conjunto de carrossel e toque em **[!UICONTROL Editar]** (ícone de lápis).
   * Passe o mouse sobre um ativo do Conjunto de carrossel, toque em **[!UICONTROL Selecionar]** (ícone de marca de seleção) e, em seguida, toque em **[!UICONTROL Editar]** na barra de ferramentas.

   * Tap on a Carousel Set asset, then in the upper-left corner of the page tap **[!UICONTROL Edit]** (pencil icon).

1. Para editar o Conjunto de carrossel, execute um dos procedimentos a seguir:

   * To add a slide, tap the **[!UICONTROL Add Slide]** icon then navigate to the asset you want to add to that slide and tap or click the checkmark.
   * Para reordenar os slides, arraste um slide para um novo local (selecione o ícone de reordenação para mover os itens).
   * Para adicionar um ponto de acesso ou mapa de imagem, clique nos ícones de ponto de acesso ou mapa de imagem e consulte [adicionar pontos de acesso e mapas](#adding-hotspots-or-image-maps-to-an-image-banner)de imagem.
   * To edit the appearance or behavior of the carousel set, tap the **[!UICONTROL Appearance]** tab or **[!UICONTROL Behavior]** tab, then set the options you want.
   * Para editar pontos de acesso ou mapas de imagem, no slide apropriado, selecione um ponto de acesso ou mapa de imagem e faça as alterações necessárias na guia **[!UICONTROL Ações]** .
   * Para excluir um slide, selecione-o e toque em **[!UICONTROL Excluir slide]** na barra de ferramentas.
   * To apply a preset, near the upper-right corner of the page, tap the **[!UICONTROL Preset]** drop-down list, then select a viewer preset.
   * Para excluir um conjunto de carrossel inteiro, navegue até o conjunto de carrossel, selecione-o e toque em **[!UICONTROL Excluir.]**

   >[!NOTE]
   Se você estiver editando imagens interativas com pontos de acesso e recortar a imagem, seus pontos de acesso serão removidos.

## (Opcional) Visualização de banners de carrossel {#optional-previewing-carousel-banners}

Você pode usar a Pré-visualização para ver a aparência do seu banner de carrossel para os clientes e testar os pontos de conexão e mapas de imagem dos banners de carrossel para garantir que eles estejam se comportando como esperado.

Quando estiver satisfeito com o banner do carrossel, você poderá publicá-lo.
See [Embedding the Video or Image Viewer on a Web Page](/help/assets/embed-code.md).
See [Linking URLs to your web application](/help/assets/linking-urls-to-yourwebapplication.md). Observe que o método baseado em URL de vinculação não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas do AEM Sites.
See [Adding Dynamic Media Assets to pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)

Você pode pré-visualização banners de carrossel no Editor de carrossel (método preferencial) ou na lista **[!UICONTROL Visualizadores]** .

**Para pré-visualização de banners de carrossel**

1. Em **[!UICONTROL Ativos]**, navegue até um banner de carrossel existente que você criou e toque para abri-lo.
1. Toque em **[!UICONTROL Editar.]**
1. No visualizador predefine a lista no canto direito da barra de ferramentas, selecione um visualizador para pré-visualização no banner do carrossel.

   ![experience_fragment-carouselbanner-viewerlista suspensa](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. Toque em **[Pré-visualização.]**
1. Toque nos pontos de acesso ou mapas de imagem na imagem para testar suas ações associadas.

**Para pré-visualização de banners de carrossel da lista Visualizadores**

1. Em **[!UICONTROL Ativos]**, navegue até um banner de carrossel existente que você criou e toque para abri-lo.
1. Ao lado do canto superior esquerdo da página de Pré-visualização, clique no ícone Conteúdo.
1. Na lista **[!UICONTROL Visualizadores]** no painel no lado esquerdo da página, toque no nome da predefinição do visualizador do banner do carrossel que deseja usar.
1. Toque nos pontos de acesso ou mapas de imagem na imagem para testar suas ações associadas.

## Publicação de banners de carrossel {#publishing-carousel-banners}

Você precisa publicar o carrossel para usá-lo. A publicação de um conjunto de carrossel ativa o URL e o código incorporado. Ele também publica o carrossel para a nuvem Dynamic Media, que é integrada a uma CDN para delivery escaláveis e de desempenho.

>[!NOTE]
Se você usar uma imagem interativa existente com pontos de acesso para seu banner de carrossel, deverá publicar a imagem interativa separadamente depois de publicar o banner do carrossel.
Além disso, se você modificar uma imagem interativa publicada pré-existente que esteja usando em um banner de carrossel, deverá publicar a imagem interativa antes que essas alterações sejam refletidas no banner de carrossel.

Consulte [Publicação de ativos](/help/assets/publishing-dynamicmedia-assets.md) de mídia dinâmica para obter informações sobre como publicar banners de carrossel.

## Adicionando um banner do carrossel à sua página do site {#adding-a-carousel-banner-to-your-website-page}

Depois de fazer upload de imagens de banner para criar um carrossel, adicionar pontos de acesso e/ou mapas de imagem ao banner e publicar o conjunto de carrossel, você estará pronto para adicioná-lo à página existente do site.

>[!NOTE]
Se você for um cliente da AEM Sites, poderá adicionar o banner do carrossel diretamente à sua página arrastando o componente de Mídia interativa para a página. See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)

No entanto, se você for um cliente AEM ativos independentes, poderá adicionar manualmente o banner do carrossel à landing page do site, conforme descrito nesta seção.

1. Copie o código incorporado do conjunto de carrossel publicado.
See [Embedding the Video or Image Viewer on a Web Page](/help/assets/embed-code.md).

1. Adicione o código incorporado que você copiou do AEM Assets à sua página da Web.
O código incorporado copiado é responsivo, portanto, deve ajustar-se automaticamente à área de incorporação da página.

## Integração do banner do carrossel com uma exibição rápida existente {#integrating-the-carousel-banner-with-an-existing-quickview}

Observação: esta etapa se aplica somente se você for um cliente independente da AEM Assets.

A última etapa desse processo é integrar o banner do carrossel a uma implementação de visualização rápida existente em seu site. Toda implementação de visualização rápida é única e é necessária uma abordagem específica que provavelmente envolva a assistência de uma pessoa de TI de front-end.

A implementação de visualização rápida existente normalmente representa uma cadeia de ações inter-relacionadas que ocorrem na página da Web na seguinte ordem:

1. Um usuário aciona um elemento na interface do usuário do seu site.
1. O código front-end obtém um URL de visualização rápido com base no elemento da interface do usuário que foi acionado na etapa 1.
1. O código de front-end envia uma solicitação do Ajax usando o URL obtido na etapa 2.
1. A lógica de backend retorna os dados de visualização rápida correspondentes ou o conteúdo de volta ao código de front-end.
1. O código front-end carrega os dados ou o conteúdo da visualização rápida.
1. Como opção, o código front-end converte os dados de visualização rápida carregados em uma representação HTML.
1. O código front-end exibe uma caixa de diálogo modal ou um painel e renderiza o conteúdo HTML na tela do usuário final.

Essas chamadas podem não representar chamadas de API públicas independentes que podem ser chamadas pela lógica da página da Web de uma etapa arbitrária. Em vez disso, é uma chamada encadeada na qual cada próxima etapa está oculta na última fase (retorno de chamada) da etapa anterior.

Ao mesmo tempo que o banner do carrossel substitui a etapa 1 e parcialmente a etapa 2, quando um usuário clica em um ponto de conexão ou mapa de imagem dentro do banner do carrossel, essa interação do usuário é feita pelo visualizador. O visualizador retorna um evento para a página da Web que contém todos os dados de hotspot ou mapa de imagem adicionados anteriormente.

Nesse manipulador de eventos, o código front-end faz o seguinte:

* Escuta um evento emitido pelo banner do carrossel.
* Constrói um URL de visualização rápido com base no ponto de acesso ou nos dados do mapa de imagem.
* Aciona o processo de carregamento da visualização rápida do backend e renderização na tela para exibição.

O código incorporado retornado pela AEM Assets já tem um manipulador de eventos pronto para uso no lugar que é comentado.

Portanto, é necessário remover as barras de comentário do código e substituir o corpo do manipulador de simulação pelo código específico da página da Web em particular.

O processo de construção do URL de visualização rápida é basicamente o oposto do processo usado para identificar as variáveis de hotspot e mapa de imagem abordadas anteriormente.

Consulte [Identificação de variáveis](#identifying-hotspot-and-image-map-variables)de hotspot e mapa de imagem.

A última etapa para acionar o URL de visualização rápida e ativar o painel de visualização rápida provavelmente requer a assistência de uma pessoa de TI front-end do seu departamento de TI. Eles têm conhecimento para saber melhor como acionar com precisão a implementação rápida da visualização a partir da etapa correta, tendo um URL de visualização rápido pronto para uso.

## Uso do Quickviews para criar pop-ups personalizados {#using-quickviews-to-create-custom-pop-ups}

See [Using Quickviews to create custom pop-ups](/help/assets/custom-pop-ups.md).
