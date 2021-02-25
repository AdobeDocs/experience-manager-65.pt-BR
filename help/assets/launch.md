---
title: Integração de visualizadores Dynamic Media com Adobe Analytics e Experience Platform Launch
description: A extensão Dynamic Media Viewers para Experience Platform Launch, juntamente com Dynamic Media Viewers 5.13, permite que os clientes da Adobe Analytics e do Platform launch usem eventos e dados específicos para os Dynamic Media Viewers em suas configurações de Platform launch.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 1f40c099518bc9d296026d8cfac5b6291e41a846
workflow-type: tm+mt
source-wordcount: '6634'
ht-degree: 9%

---


# Integração de visualizadores Dynamic Media com Adobe Analytics e Experience Platform Launch {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## O que é a integração dos visualizadores Dynamic Media com o Adobe Analytics e o Experience Platform Launch? {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

A nova extensão *Dynamic Media Viewers* para Platform launch e Dynamic Media Viewers 5.13 permite que os clientes da Adobe Analytics e do Platform launch usem eventos e dados específicos para os visualizadores em suas configurações de Platforms launch.

Essa integração significa que você pode rastrear o uso de visualizadores do Dynamic Media no seu site com a Adobe Analytics. Ao mesmo tempo, você pode usar os eventos e dados expostos pelos visualizadores com qualquer outra extensão de Experience Platform Launch que venha do Adobe ou de terceiros.

Para saber mais sobre extensões, consulte [Extensão do Adobe](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/overview.html#adobe-extension) no Guia do Usuário do Experience Platform Launch.

**Para quem esta documentação se destina:administradores de** site, desenvolvedores na plataforma Experience Manager e pessoas em operações.

### Limitações da integração {#limitations-of-the-integration}

* A integração do Experience Platform Launch para visualizadores Dynamic Media não funciona no nó do autor do Experience Manager. Não é possível ver nenhum rastreamento de uma página WCM até que ela seja publicada.
* A integração do Experience Platform Launch para visualizadores Dynamic Media não é compatível com o modo de operação &quot;pop-up&quot;, onde o URL do visualizador é obtido usando o botão &quot;URL&quot; na página Detalhes do ativo.
* A integração do Experience Platform Launch não pode ser usada simultaneamente com a integração do Analytics de visualizadores herdados (por meio do parâmetro `config2=`).
* O suporte para rastreamento de vídeo está limitado somente ao rastreamento de &quot;reprodução principal&quot;, conforme descrito em [Visão geral do rastreamento](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html#player-events). Especificamente, o rastreamento de QoS, Anúncios, Capítulo/Segmentos ou Erros não é suportado.
* A configuração da Duração do armazenamento para Elementos de dados não é compatível com Elementos de dados que usam a extensão *Dynamic Media Viewers*. A Duração do armazenamento deve ser definida como **[!UICONTROL Nenhum]**.

### Casos de uso para a integração {#use-cases-for-the-integration}

O principal caso de uso para a integração com o Experience Platform Launch são os clientes que usam o AEM Assets e o AEM Sites. Nesses cenários, você pode configurar uma integração padrão entre o nó do autor AEM e o Experience Platform Launch, em seguida, associar a instância Sites à propriedade Experience Platform Launch. Depois disso, qualquer componente Dynamic Media WCM adicionado a uma página Sites rastreará os dados e eventos dos visualizadores.

Consulte [Sobre o rastreamento de visualizadores Dynamic Media no AEM Sites](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersinAEMSites).

Um caso de uso secundário suportado pela integração são os clientes que usam somente o AEM Assets ou o Dynamic Media Classic. Nesses casos, você obtém o código incorporado para seu visualizador e o adiciona à página do site. Em seguida, obtenha o URL de produção da biblioteca de Experience Platform Launch do Experience Platform Launch e adicione-o manualmente ao código da página da Web.

Consulte [Sobre o rastreamento de visualizadores Dynamic Media usando o código incorporado](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersusingEmbedcode).

## Como o rastreamento de dados e eventos funciona na integração {#how-data-and-event-tracking-works-in-the-integration}

A integração aproveita dois tipos separados e independentes de rastreamento de visualizadores do Dynamic Media: *Adobe Analytics* e *Adobe Analytics para Áudio e Vídeo*.

### Sobre o rastreamento usando o Adobe Analytics {#about-tracking-using-adobe-analytics}

A Adobe Analytics permite que você rastreie ações executadas pelo usuário final quando interagem com os visualizadores do Dynamic Media em seu site. A Adobe Analytics também permite rastrear dados específicos do visualizador. Por exemplo, você pode rastrear e gravar eventos de carregamento de visualização junto com o nome do ativo, quaisquer ações de zoom que ocorreram e ações de reprodução de vídeo.

No Experience Platform Launch, os conceitos de *Elementos de dados* e *Regras* trabalham juntos para ativar o rastreamento do Adobe Analytics.

#### Sobre elementos de dados no Experience Platform Launch {#about-data-elements-in-adobe-launch}

Um elemento de dados no Experience Platform Launch é uma propriedade nomeada cujo valor é definido estaticamente ou calculado dinamicamente com base no estado de uma página da Web ou nos dados do Dynamic Media Viewers.

As opções disponíveis para uma definição de Elemento de dados dependem da lista de Extensões instaladas na Propriedade Experience Platform Launch. A extensão &quot;Core&quot; é pré-instalada e está disponível imediatamente em qualquer configuração. Essa extensão &quot;Core&quot; permite definir um Elemento de dados que o valor vem do cookie, código JavaScript, sequência de query e muitas outras fontes.

Para o Adobe Analytics tracking, é necessário instalar várias outras extensões, conforme descrito em [Instalação e configuração de extensões](#installing-and-setup-of-extensions). A extensão Visualizadores do Dynamic Media adiciona uma capacidade de definir um Elemento de dados cujo valor é um argumento do evento Visualizador dinâmico. Por exemplo, é possível fazer referência ao tipo de visualizador, ou ao nome do ativo reportado pelo visualizador durante a carga, o nível de zoom reportado quando o usuário final aumenta o zoom e muito mais.

A extensão do Dynamic Media Viewer mantém automaticamente os valores de seus Elementos de dados atualizados.

Depois de defini-lo, um Elemento de dados pode ser usado em outros locais da interface do usuário do Experience Platform Launch, usando o widget do seletor de elementos de dados. Especificamente, os Elementos de dados definidos para fins de rastreamento de visualizadores do Dynamic Media são referenciados pela Ação Definir variáveis da extensão do Adobe Analytics na Regra (consulte abaixo).

Consulte [Elementos de dados](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/data-elements.html#reference).

#### Sobre regras no Experience Platform Launch {#about-rules-in-adobe-launch}

Uma Regra no Experience Platform Launch é uma configuração agnóstica que define três áreas que compõem uma regra: *Eventos*, *Condições* e *Ações*:

* *Eventos*  (se) informam ao Experience Platform Launch quando acionar uma regra.
* *As condições*  (se) indicam ao Experience Platform Launch que outras restrições serão permitidas ou não quando uma regra for acionada.
* *As ações*  (em seguida) informam ao Experience Platform Launch o que fazer quando uma Regra é acionada.

As opções disponíveis na seção Evento, Condições e Ações dependem das extensões instaladas na Propriedade do Experience Platform Launch. A extensão *Core* é pré-instalada e está disponível prontamente em qualquer configuração. A extensão fornece várias opções para Eventos, como ações básicas em nível de navegador. Essas ações incluem mudança de foco, pressionamentos de tecla e envios de formulário. Também inclui opções para Condições, como valor de cookie, tipo de navegador e muito mais. Para Ações, somente a opção Código personalizado está disponível.

Para o rastreamento do Adobe Analytics, várias outras extensões devem ser instaladas, conforme descrito em [Instalação e configuração de extensões](#installing-and-setup-of-extensions). Especificamente:

* A extensão dos visualizadores do Dynamic Media estende a lista dos Eventos suportados para eventos específicos dos visualizadores Dynamic Media, como carregamento do visualizador, troca de ativos, aumento de zoom e reprodução de vídeo.
* A extensão do Adobe Analytics estende a lista de Ações suportadas com duas ações necessárias para enviar dados para servidores de rastreamento: *Defina variáveis* e *Enviar beacon*.

Para rastrear visualizadores Dynamic Media, é possível usar qualquer tipo de:

* Eventos da extensão do Dynamic Media Viewers, da extensão Core ou de qualquer outra extensão.
* Condições na definição da regra. Ou você pode deixar a área de condições vazia.

Na seção Ações, é necessário que você tenha uma ação *Definir variáveis*. Esta ação informa a Adobe Analytics como preencher variáveis de rastreamento com dados. Ao mesmo tempo, a ação *Definir variáveis* não envia nada para o servidor de rastreamento.

A ação *Definir variáveis* deve ser seguida por uma ação *Enviar beacon*. A ação *Enviar beacon* envia dados para o servidor de rastreamento do Analytics. Ambas as ações, *Definir variáveis* e *Enviar beacon*, vêm da extensão do Adobe Analytics.

Consulte [Regras](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html#reference).

#### Exemplo de configuração {#sample-configuration}

A seguinte configuração de amostra no Experience Platform Launch demonstra como rastrear um nome de ativo durante a carga do visualizador.

1. Na guia **[!UICONTROL Elementos de dados]**, defina um elemento de dados `AssetName` que faça referência ao parâmetro `asset` do evento `LOAD` da extensão Dynamic Media Viewers.

   ![image2019-11](assets/image2019-11.png)

1. Na guia **[!UICONTROL Regras]**, defina uma regra *TrackAssetOnLoad*.

   Nesta regra, o campo **[!UICONTROL Evento]** usa o evento **[!UICONTROL LOAD]** da extensão de Visualizadores Dynamic Media.

   ![image2019-22](assets/image2019-22.png)

1. A configuração Ação tem dois tipos de Ação da extensão Adobe Analytics:

   *Defina Variáveis*, que mapeiam uma variável de análise de sua escolha para o valor do Elemento de  `AssetName` dados.

   *Envie o Beacon*, que envia informações de rastreamento para a Adobe Analytics.

   ![image2019-3](assets/image2019-3.png)

1. A configuração de regra resultante é semelhante ao seguinte:

   ![image2019-4](assets/image2019-4.png)

### Sobre o Adobe Analytics para áudio e vídeo {#about-adobe-analytics-for-audio-and-video}

Quando uma conta de Experience Cloud é assinada para usar o Adobe Analytics para Áudio e Vídeo, é suficiente ativar o rastreamento de vídeo nas configurações de extensão *Dynamic Media Viewers*. As métricas de vídeo tornam-se disponíveis no Adobe Analytics. O rastreamento de vídeo depende da presença das extensões Adobe Medium Analytics para áudio e vídeo.

Consulte [Instalação e configuração de extensões](#installing-and-setup-of-extensions).

Atualmente, o suporte para rastreamento de vídeo está limitado somente ao rastreamento de &quot;reprodução principal&quot;, conforme descrito em [Visão geral do rastreamento](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html#player-events). Especificamente, o rastreamento de QoS, Anúncios, Capítulo/Segmentos ou Erros não é suportado.

## Uso da extensão do Dynamic Media Viewers {#using-the-dynamic-media-viewers-extension}

Conforme mencionado em [Casos de uso para a integração](#use-cases-for-the-integration), é possível rastrear visualizadores Dynamic Media com a nova integração do Experience Platform Launch no AEM Sites e usando o código incorporado.

### Rastrear visualizadores do Dynamic Media no AEM Sites {#tracking-dynamic-media-viewers-in-aem-sites}

Para rastrear visualizadores Dynamic Media no AEM Sites, todas as etapas listadas na seção [Configurar todas as partes de integração](#configuring-all-the-integration-pieces) devem ser executadas. Especificamente, você deve criar a configuração IMS e a configuração da Experience Platform Launch Cloud.

Após a configuração correta, qualquer visualizador do Dynamic Media que você adicionar a uma página Sites, usando um componente WCM suportado pela Dynamic Media, rastreia automaticamente os dados para o Adobe Analytics ou Adobe Analytics para Vídeo, ou ambos.

<!-- To be reviewed and updated although this is found live in the AEMaaCS version:
See [Adding Dynamic Media Assets to Pages using Adobe Sites](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html).
-->

### Rastreamento de visualizadores Dynamic Media usando o código incorporado {#tracking-dynamic-media-viewers-using-embed-code}

Os clientes que não usam o AEM Sites ou incorporam visualizadores do Dynamic Media em páginas da Web fora do AEM Sites, ou ambos, ainda podem usar a integração com o Experience Platform Launch.

Complete as etapas de configuração das seções [Configuração do Adobe Analytics](#configuring-adobe-analytics-for-the-integration) e [Configuração do Experience Platform Launch](#configuring-adobe-launch-for-the-integration). No entanto, as etapas de configuração relacionadas ao Experience Manager não são necessárias.

Após a configuração correta, você pode adicionar suporte a Experience Platform Launch a uma página da Web com um visualizador Dynamic Media.

Consulte [Adicionar o código incorporado do Platform launch](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html#configure-launch) para saber mais sobre como usar o código incorporado da biblioteca do Experience Platform Launch.

<!-- To be reviewed and updated although this is found live in the AEMaaCS version:
See [Embedding the Video or Image Viewer on a Web Page](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html) to learn more about how to use the embed code feature of AEM Dynamic Media.
-->

**Para rastrear visualizadores Dynamic Media usando código** incorporado:

1. Tenha uma página da Web pronta para incorporar um visualizador do Dynamic Media.
1. Obtenha o código incorporado para a biblioteca de Experience Platform Launch fazendo login primeiro em Experience Platform Launch (consulte [Configurando Experience Platform Launch](#configuring-adobe-launch-for-the-integration)).
1. Clique em **[!UICONTROL Propriedade]** e clique na guia **[!UICONTROL Ambientes]**.
1. Escolha o nível de Ambiente relevante para o ambiente da página da Web. Em seguida, na coluna **[!UICONTROL Instalar]**, clique no ícone da caixa.
1. **[!UICONTROL Na caixa de diálogo]** Instruções de instalação na Web, copie o código incorporado da biblioteca de Experience Platform Launch, juntamente com as  `<script/>` tags ao redor.

## Guia de referência para a extensão do Dynamic Media Viewers {#reference-guide-for-the-dynamic-media-viewers-extension}

### Sobre a configuração dos visualizadores do Dynamic Media {#about-the-dynamic-media-viewers-configuration}

A extensão do Dynamic Media Viewer se integra automaticamente à biblioteca de Experience Platform Launch se as seguintes condições forem verdadeiras:

* O objeto global da biblioteca de Experience Platform Launch ( `_satellite`) está presente na página.
* A função de extensão do Dynamic Media Viewers `_dmviewers_v001()` está definida em `_satellite`.

* `config2=` o parâmetro do visualizador não foi especificado, o que significa que o visualizador não usa a integração herdada do Analytics.

Além disso, há uma opção para desativar explicitamente a integração do Experience Platform Launch no visualizador especificando o parâmetro `launch=0` na configuração do visualizador. O valor padrão desse parâmetro é `1`.

### Configuração da extensão do Dynamic Media Viewers {#configuring-the-dynamic-media-viewers-extension}

A única opção de configuração para a extensão de visualizadores Dynamic Media é **[!UICONTROL Ativar a Análise de Adobe Medium para Áudio e Vídeo]**.

Quando você marcar (ativar) essa opção e a extensão do Adobe Medium Analytics para áudio e vídeo estiver instalada e configurada, as métricas de reprodução de vídeo serão enviadas para a solução de Áudio e vídeo da Adobe Analytics. Desativar esta opção desativa o rastreamento de vídeo.

Se você habilitar essa opção *sem* ter a extensão Adobe Medium Analytics para áudio e vídeo instalada, a opção não terá efeito.

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### Sobre elementos de dados na extensão {#about-data-elements-in-the-dynamic-media-viewers-extension} do Dynamic Media Viewers

O único tipo de Elemento de dados fornecido pela extensão Visualizadores do Dynamic Media é o **[!UICONTROL Evento do visualizador]** na lista suspensa **[!UICONTROL Tipo de elemento de dados]**.

Quando selecionado, o editor de Elementos de dados renderiza um formulário com dois campos:

* **[!UICONTROL Tipo de dados do evento de visualizadores do DM]** - uma lista suspensa que identifica todos os eventos do visualizador compatíveis com a extensão do Visualizador do Dynamic Media que têm argumentos, além de um item **[!UICONTROL COMMON]** especial. Um item **[!UICONTROL COMUM]** representa uma lista de parâmetros de evento comuns a todos os tipos de eventos enviados pelos visualizadores.
* **[!UICONTROL Parâmetro]**  de rastreamento - um argumento do evento visualizador do Dynamic Media selecionado.

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

Consulte o [Guia de referência do Visualizador do Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) para obter a lista de eventos suportados por cada tipo de visualizador; vá para a seção do visualizador específico e clique em Suporte para a subseção de rastreamento do Adobe Analytics. Atualmente, o guia de referência Visualizadores do Dynamic Media não apresenta argumentos de evento de documento.

Agora considere o ciclo de vida dos Visualizadores do Dynamic Media *Elemento de dados*. O valor desse Elemento de dados é preenchido depois que o evento do visualizador do Dynamic Media correspondente acontece na página. Por exemplo, suponha que o Elemento de dados aponte para o evento **[!UICONTROL LOAD]** e seu argumento &quot;asset&quot;. Nesse caso, o valor desse Elemento de dados recebe dados válidos depois que o visualizador executa o evento **[!UICONTROL LOAD]** pela primeira vez. Se o Elemento de dados apontar para o evento **[!UICONTROL ZOOM]** e seu argumento &quot;scale&quot;, o valor desse Elemento de dados permanecerá vazio até que o visualizador envie um evento **[!UICONTROL ZOOM]** pela primeira vez.

Da mesma forma, os valores dos Elementos de dados são atualizados automaticamente quando o visualizador envia um evento correspondente na página. A atualização de valor acontece mesmo se o evento específico não for definido na configuração Regra. Por exemplo, suponha que o Elemento de dados **[!UICONTROL ZoomScale]** esteja definido para o parâmetro &quot;scale&quot; do evento ZOOM. No entanto, a única regra presente na configuração Regra é acionada pelo evento **[!UICONTROL LOAD]**. O valor de **[!UICONTROL ZoomScale]** ainda é atualizado sempre que um usuário executa o zoom dentro do visualizador.

Qualquer visualizador do Dynamic Media tem um identificador exclusivo na página da Web. O elemento de dados rastreia o próprio valor e o visualizador que preencheu o valor. Por exemplo, suponha que haja vários visualizadores na mesma página e um **[!UICONTROL AssetName]** Elemento de dados que aponte para o evento **[!UICONTROL LOAD]** e seu argumento &quot;asset&quot;. O elemento de dados **[!UICONTROL AssetName]** mantém uma coleção de nomes de ativos associados a cada visualizador carregado na página.

O valor exato retornado pelo Elemento de dados depende do contexto. Se o Elemento de dados for solicitado em uma Regra que foi acionada por um evento do visualizador do Dynamic Media, o valor do Elemento de dados será retornado para o visualizador que iniciou a Regra. Além disso, o Elemento de dados é solicitado em uma Regra que foi acionada por um Evento de outra extensão de Platform launch. Nesse ponto, o valor do Elemento de dados provém do visualizador que foi o último a atualizar esse Elemento de dados.

**Considere a seguinte configuração** de exemplo:

* Uma página da Web que tem dois visualizadores de zoom do Dynamic Media: *viewer1* e *viewer2*.

* **[!UICONTROL O elemento]** ZoomScaleData aponta para o evento  **** ZOOM e seu argumento &quot;scale&quot;.
* **** TrackPanRule com o seguinte:

   * Usa o evento do Dynamic Media Viewer **[!UICONTROL PAN]** como disparador.
   * Envia o valor de **[!UICONTROL ZoomScale]** Elemento de dados para a Adobe Analytics.

* **** TrackKeyRule com o seguinte:

   * Usa o evento key press da extensão do Experience Platform Launch Core como disparador.
   * Envia o valor de **[!UICONTROL ZoomScale]** Elemento de dados para a Adobe Analytics.

Agora, suponha que o usuário final carregue a página da Web com os dois visualizadores. Em *viewer1*, eles aumentam o zoom para 50% de escala; em seguida, em *viewer2*, aumentam o zoom para 25% da escala. Em *viewer1*, eles deslocam a imagem e finalmente selecionam uma tecla no teclado.

A atividade do usuário final resulta nas duas chamadas de rastreamento a seguir feitas para a Adobe Analytics:

* A primeira chamada ocorre porque a regra **[!UICONTROL TrackPan]** é acionada quando o usuário entra em *viewer1*. Essa chamada envia 50% como um valor de **[!UICONTROL ZoomScale]** Elemento de dados porque o Elemento de dados sabe que a Regra é acionada por *viewer1* e obtém o valor de escala correspondente;
* A segunda chamada ocorre porque a regra **[!UICONTROL TrackKey]** é acionada quando o usuário pressiona uma tecla no teclado. Essa chamada envia 25% como um valor de **[!UICONTROL ZoomScale]** Elemento de dados porque a Regra não foi acionada pelo visualizador. Dessa forma, o Elemento de dados retorna o valor mais atualizado.

A amostra configurada acima também afeta a duração do valor do Elemento de dados. O valor do Elemento de dados gerenciado pelo Dynamic Media Viewer é armazenado no código da biblioteca de Platforms launch mesmo depois que o próprio visualizador é descartado na página da Web. Essa funcionalidade significa que, se houver uma Regra acionada por uma extensão que não seja o Dynamic Media Viewer e fizer referência a esse Elemento de dados, o Elemento de dados retornará o último valor conhecido. Mesmo se o visualizador não estiver mais presente na página da Web.

Em qualquer caso, os valores dos Elementos de dados acionados pelos Visualizadores do Dynamic Media não são armazenados no armazenamento local ou no servidor; em vez disso, eles são mantidos apenas na biblioteca de Experience Platform Launch do lado do cliente. Os valores desse Elemento de dados desaparecem quando a página da Web é recarregada.

Geralmente, o editor de Elementos de dados oferece suporte a [seleção da duração do armazenamento](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/data-elements.html?lang=en#create-a-data-element). Entretanto, os Elementos de dados que usam a extensão de Visualizadores do Dynamic Media suportam apenas a opção de duração do armazenamento de **[!UICONTROL Nenhum]**. A definição de qualquer outro valor é possível na interface do usuário, mas o comportamento do Elemento de dados não é definido nesse caso. A extensão gerencia o valor do Elemento de dados sozinho: o elemento de dados que mantém o valor do argumento do evento do visualizador durante todo o ciclo de vida do visualizador.

### Sobre as regras na extensão do Dynamic Media Viewers {#about-rules-in-the-dynamic-media-viewers-extension}

No Editor de regras, a extensão adiciona novas opções de configuração para o editor de Eventos. Além disso, o editor fornece uma opção para fazer referência manual aos parâmetros do evento no editor de Ação como uma opção de mão curta, em vez de usar elementos de dados pré-configurados.

#### Sobre o editor de Eventos {#about-the-events-editor}

No editor de Eventos, a extensão do Dynamic Media Viewers adiciona um **[!UICONTROL Tipo de evento]** chamado **[!UICONTROL Evento do visualizador]**.

Quando selecionado, o editor de Eventos renderiza o menu suspenso **[!UICONTROL eventos do Dynamic Media Viewer]**, listando todos os eventos disponíveis que são suportados pelos visualizadores Dynamic Media.

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### Sobre o editor de Ações {#about-the-actions-editor}

A extensão Visualizadores do Dynamic Media permite que você use parâmetros de evento de visualizadores do Dynamic Media para mapear as variáveis de análise no editor Definir variáveis da extensão do Adobe Analytics.

O método mais simples para fazer isso é concluir o seguinte processo de duas etapas:

* Primeiro, defina um ou mais Elementos de dados, onde cada Elemento de dados representa um parâmetro de um evento do Dynamic Media Viewer.
* Finalmente, no editor Definir variáveis da extensão do Adobe Analytics, clique no ícone do seletor de elementos de dados (três discos empilhados) para abrir a caixa de diálogo Selecionar elemento de dados e selecione um elemento de dados a partir dele.

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

No entanto, é possível usar uma abordagem alternativa e ignorar a criação do Elemento de dados. Você pode fazer referência direta a um argumento de um evento do Dynamic Media Viewer. Digite o nome totalmente qualificado do argumento evento no campo de entrada **[!UICONTROL value]** da atribuição de variável do Analytics. Certifique-se de circundá-lo com sinais de percentagem (%). Por exemplo,

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

Há uma diferença importante entre o uso de Elementos de dados e a referência do argumento de evento direto. Para Elemento de dados, não importa qual evento aciona a ação Definir variáveis. O evento que aciona a Regra pode não estar relacionado ao Visualizador dinâmico. Por exemplo, ao clicar na página da Web na extensão Principal. Mas, ao usar uma referência de argumento direto, é importante garantir que o evento que aciona a regra corresponda ao argumento do evento que ela menciona.

Por exemplo, a referência `%event.detail.dm.LOAD.asset%` retornará o nome correto do ativo se Regra for acionado pelo evento **[!UICONTROL LOAD]** da extensão do Visualizador do Dynamic Media. No entanto, retorna um valor vazio para qualquer outro evento.

A tabela a seguir lista eventos do Dynamic Media Viewer e seus argumentos suportados:

<table>
 <tbody>
  <tr>
   <td>Nome do evento do visualizador</td>
   <td>Referência do argumento</td>
  </tr>
  <tr>
   <td><code>COMMON</code></td>
   <td><code>%event.detail.dm.objID%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.compClass%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.instName%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.timeStamp%</code></td>
  </tr>
  <tr>
   <td><code>BANNER</code> </td>
   <td><code>%event.detail.dm.BANNER.asset%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.label%</code></td>
  </tr>
  <tr>
   <td><code>HREF</code></td>
   <td><code>%event.detail.dm.HREF.rollover%</code></td>
  </tr>
  <tr>
   <td><code>ITEM</code></td>
   <td><code>%event.detail.dm.ITEM.rollover%</code></td>
  </tr>
  <tr>
   <td><code>LOAD</code></td>
   <td><code>%event.detail.dm.LOAD.applicationname%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.asset%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.company%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.sdkversion%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewertype%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewerversion%</code></td>
  </tr>
  <tr>
   <td><code>METADATA</code></td>
   <td><code>%event.detail.dm.METADATA.length%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.METADATA.type%</code></td>
  </tr>
  <tr>
   <td><code>MILESTONE</code></td>
   <td><code>%event.detail.dm.MILESTONE.milestone%</code></td>
  </tr>
  <tr>
   <td><code>PAGE</code></td>
   <td><code>%event.detail.dm.PAGE.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.PAGE.label%</code></td>
  </tr>
  <tr>
   <td><code>PAUSE</code></td>
   <td><code>%event.detail.dm.PAUSE.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>PLAY</code></td>
   <td><code>%event.detail.dm.PLAY.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SPIN</code></td>
   <td><code>%event.detail.dm.SPIN.framenumber%</code></td>
  </tr>
  <tr>
   <td><code>STOP</code></td>
   <td><code>%event.detail.dm.STOP.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SWAP</code></td>
   <td><code>%event.detail.dm.SWAP.asset%</code></td>
  </tr>
  <tr>
   <td><code>SWATCH</code></td>
   <td><code>%event.detail.dm.SWATCH.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.SWATCH.label%</code></td>
  </tr>
  <tr>
   <td><code>TARG</code></td>
   <td><code>%event.detail.dm.TARG.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.TARG.label%</code></td>
  </tr>
  <tr>
   <td><code>ZOOM</code></td>
   <td><code>%event.detail.dm.ZOOM.scale%</code></td>
  </tr>
 </tbody>
</table>

## Configurar todas as partes de integração {#configuring-all-the-integration-pieces}

**ANTES DE COMEÇAR**

Caso ainda não o tenha feito, a Adobe recomenda que você analise toda a documentação antes desta seção para entender a integração completa.

Esta seção explica as etapas de configuração necessárias para integrar os visualizadores Dynamic Media ao Adobe Analytics e Adobe Analytics para áudio e vídeo. Embora seja possível usar a extensão Dynamic Media Viewers para outros fins no Experience Platform Launch, tais cenários não são abordados nesta documentação.

Você usará os seguintes produtos de Adobe para configurar sua integração:

* Adobe Analytics - usado para configurar variáveis e relatórios de rastreamento.
* Experience Platform Launch - usado para definir uma Propriedade, uma ou mais Regras e um ou mais Elementos de dados para ativar o rastreamento do visualizador.

Além disso, se essa solução de integração for usada com o Experience Manager Sites, a seguinte configuração também deverá ser feita:

* [!DNL Adobe I/O] Console - a integração é criada para o Experience Platform Launch.
* nó do autor do Experience Manager - configuração IMS e configuração da nuvem do Experience Platform Launch.

Como parte da configuração, verifique se você tem acesso a uma empresa no Adobe Experience Cloud que já tenha o Adobe Analytics e o Experience Platform Launch.

## Configuração da Adobe Analytics para a integração {#configuring-adobe-analytics-for-the-integration}

Depois de configurar o Adobe Analytics, o seguinte será configurado para a integração:

* Um Conjunto de relatórios está no lugar e selecionado.
* As Variáveis do Analytics estão disponíveis para receber dados de rastreamento.
* Os relatórios estão disponíveis para visualização de dados coletados dentro do Adobe Analytics.

Consulte também [Guia de implementação do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html).

**Para configurar o Adobe Analytics para integração**:

1. Start acessando o Adobe Analytics a partir do Experience Cloud [home page](https://exc-home.experiencecloud.adobe.com/exc-home/home.html#/). Na barra de menus, clique no ícone Soluções (uma tabela de três por três pontos) próximo ao canto superior direito da página e, em seguida, clique em **[!UICONTROL Analytics]**.

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   Agora selecione um conjunto de relatórios.

### Selecionar um conjunto de relatórios {#selecting-a-report-suite}

1. Próximo ao canto superior direito da página do Adobe Analytics, à direita do campo **[!UICONTROL Pesquisar relatórios]**, selecione o conjunto de relatórios correto na lista suspensa. Se houver vários conjuntos de relatórios disponíveis e você não tiver certeza de qual usar, entre em contato com o administrador do Adobe Analytics, que pode ajudá-lo a selecionar qual usar.

   Na ilustração abaixo, um usuário criou um conjunto de relatórios chamado *DynamicMediaViewersExtensionDoc* e o selecionou na lista suspensa. O nome do conjunto de relatórios é apenas para fins ilustrativos. O nome do conjunto de relatórios que você selecionar depende de você.

   Se nenhum conjunto de relatórios estiver disponível, você ou o administrador da Adobe Analytics devem criar um antes de prosseguir com a configuração.

   Consulte [Relatórios e conjuntos de relatórios](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html#manage-report-suites) e [Criar um conjunto de relatórios](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/create-report-suite.html#admin-console).

   No Adobe Analytics, os conjuntos de relatórios são gerenciados em **[!UICONTROL Admin > Conjuntos de relatórios]**.

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   Agora, configure as variáveis do Adobe Analytics.

### Configuração de variáveis do Adobe Analytics {#setting-up-adobe-analytics-variables}

1. Designe uma ou mais variáveis do Adobe Analytics que você deseja usar para rastrear o comportamento dos Visualizadores do Dynamic Media na página da Web.

   É possível usar qualquer tipo de variável suportada pela Adobe Analytics. A decisão sobre o tipo de variável (como Tráfego personalizado [props], Conversão [eVar]) é orientada pelas necessidades específicas da implementação do Analytics.

   Consulte [Visão geral de props e eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html#vars).

   Para os fins desta documentação, somente uma variável de Tráfego personalizado (props) será usada porque eles ficam disponíveis em um Relatório do Analytics alguns minutos depois que uma ação ocorre em uma página da Web.

   Para ativar uma nova variável de Tráfego personalizado, no Adobe Analytics, na barra de ferramentas, clique em **[!UICONTROL Administrador > Report Suites]**.

1. Na página **[!UICONTROL Gerenciador de conjunto de relatórios]**, selecione o relatório correto e, na barra de ferramentas, clique em **[!UICONTROL Editar configurações > Tráfego > Variáveis de tráfego]**.
1. Ali, selecione uma variável não utilizada, atribua a ela um nome descritivo ( **[!UICONTROL ativo do visualizador (prop 30)]**) e altere a caixa de combinação para &quot;Ativado&quot; na coluna Ativado.

   A captura de tela a seguir é um exemplo de uma variável de Tráfego personalizado ( **[!UICONTROL prop30]**) para rastrear um nome de ativo usado pelo visualizador:

   ![image2019-6-26_23-6-59](assets/image2019-6-26_23-6-59.png)

1. Na parte inferior da lista de variáveis, clique em **[!UICONTROL Salvar]**.

### Configuração de um relatório {#setting-up-a-report}

1. Geralmente, a configuração de um Relatório no Adobe Analytics é orientada por necessidades específicas do projeto. Dessa forma, a configuração detalhada do relatório está além do escopo dessa integração.

   No entanto, basta saber que os relatórios de Tráfego personalizado ficam automaticamente disponíveis no Adobe Analytics depois que você configura as variáveis de Tráfego personalizado em [Configuração de variáveis do Adobe Analytics](#setting-up-adobe-analytics-variables).

   Por exemplo, o relatório da variável **[!UICONTROL Ativo do visualizador (prop 30)]** está disponível no menu Relatórios, em **[!UICONTROL Tráfego personalizado > Tráfego personalizado 21-30 > Ativo do visualizador (prop 30)]**.

   Visitar este relatório logo após a criação do **[!UICONTROL Ativo do visualizador (prop 30)]**, não mostra dados; o que é esperado neste momento da integração.

   ![image2019-6-26_23-12-49](assets/image2019-6-26_23-12-49.png)

## Configurando o Experience Platform Launch para a integração {#configuring-adobe-launch-for-the-integration}

Depois de configurar o Experience Platform Launch, o seguinte será configurado para a integração:

* A criação de uma nova propriedade para manter todas as configurações juntas.
* A instalação e configuração de extensões. O código do cliente de todas as extensões instaladas na Propriedade é compilado em conjunto em uma biblioteca. Esta biblioteca é usada pela página da Web mais tarde.
* Configuração de elementos de dados e regras. Essa configuração define quais dados devem ser capturados dos visualizadores do Dynamic Media, quando disparar a lógica de rastreamento e onde enviar os dados do visualizador no Adobe Analytics.
* Publicação da biblioteca.

**Para configurar o Experience Platform Launch para a integração**:

1. Start acessando Experience Platform Launch do Experience Cloud [home page](https://exc-home.experiencecloud.adobe.com/exc-home/home.html#/). Na barra de menus, clique no ícone Soluções (três por três tabelas de pontos) próximo ao canto superior direito da página e, em seguida, clique em **[!UICONTROL Iniciar]**.

   Você também pode [abrir Experience Platform Launch diretamente](https://launch.adobe.com/).

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### Criação de uma propriedade em Experience Platform Launch {#creating-a-property-in-adobe-launch}

Uma propriedade no Experience Platform Launch é uma configuração nomeada que mantém todas as suas configurações unidas. Uma biblioteca das configurações é gerada e publicada em diferentes níveis de ambiente (desenvolvimento, armazenamento temporário e produção).

Consulte também [Criar uma propriedade de inicialização](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-mobile-android-apps-with-launch/configure-launch/launch-create-a-property.html#configure-launch).

1. No Experience Platform Launch, clique em **[!UICONTROL Nova propriedade]**.
1. Na caixa de diálogo **[!UICONTROL Criar propriedade]**, no campo **[!UICONTROL Nome]**, digite um nome descritivo, como o título do site. Por exemplo, `DynamicMediaViewersProp.`
1. No campo **[!UICONTROL Domínios]**, insira o domínio do site.
1. Na lista suspensa **[!UICONTROL Opções avançadas]**, ative **[!UICONTROL Configurar para desenvolvimento de extensão (não pode ser modificado posteriormente)]** no caso de a extensão que você deseja usar - neste caso, *Visualizadores Dynamic Media* - ainda não ser lançada.

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. Clique em **[!UICONTROL Salvar]**.

   Clique na propriedade recém-criada e prossiga para *Instalação e configuração de extensões*.

### Instalação e configuração de extensões {#installing-and-setup-of-extensions}

Todas as extensões disponíveis no Experience Platform Launch estão listadas em **[!UICONTROL Extensões > Catálogo]**.

Para instalar uma extensão, clique em **[!UICONTROL Instalar]**. Se necessário, execute uma configuração de extensão única e clique em **[!UICONTROL Salvar]**.

Quando necessário, as seguintes extensões devem ser instaladas e configuradas:

* (Obrigatório) *Extensão *Serviço de ID de Experience Cloud

Nenhuma configuração adicional é necessária, aceitar para quaisquer valores propostos. Quando terminar, clique em **[!UICONTROL Salvar]**.

Consulte [Extensão do serviço de ID de Experience Cloud](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html#extensions-ref).

* (Obrigatório) extensão *Adobe Analytics*

Para configurar essa extensão, você precisa da ID do conjunto de relatórios encontrada no Adobe Analytics, em **[!UICONTROL Admin > Conjunto de relatórios]**, no cabeçalho da coluna **[!UICONTROL ID do conjunto de relatórios]**.

(Somente para fins de demonstração, a ID do Conjunto de relatórios do **[!UICONTROL DynamicMediaViewersExtensionDoc]** Conjunto de relatórios é usada nas seguintes capturas de tela. Esta ID foi criada e usada em [Selecionar um conjunto de relatórios](#selecting-a-report-suite) anteriormente.)

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

Na página Instalar extensão, digite a ID do conjunto de relatórios no campo **[!UICONTROL Conjuntos de relatórios]**, no campo **[!UICONTROL Conjuntos de relatórios de preparo]** e no campo **[!UICONTROL Conjuntos de relatórios de produção]**.

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*Configure o seguinte item somente se você planeja usar o rastreamento de vídeo:*

Na página **[!UICONTROL Instalar extensão]**, expanda **[!UICONTROL Geral]** e especifique o Servidor de rastreamento. O Servidor de rastreamento segue o modelo `<trackingNamespace>.sc.omtrdc.net`, onde `<trackingNamespace>` são as informações obtidas no email de provisionamento.

Clique em **[!UICONTROL Salvar]**.

Consulte [Adobe Analytics Extension](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html#extensions-ref).

* (Opcional; obrigatório somente se o rastreamento de vídeo for necessário) *Adobe Medium Analytics para extensão de Áudio e Vídeo*

Preencha o campo do servidor de rastreamento. O servidor de rastreamento para a extensão *Adobe Medium Analytics para áudio e vídeo* é diferente do servidor de rastreamento usado para Adobe Analytics. Ele segue o modelo `<trackingNamespace>.hb.omtrdc.net`, onde `<trackingNamespace>` são as informações do email de provisionamento.

Todos os outros campos são opcionais.

Consulte [Adobe Medium Analytics para obter mais informações sobre a extensão de áudio e vídeo](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#extensions-ref).

* (Obrigatório) *Visualizadores Dynamic Media* extensão

Selecione **[!UICONTROL ativar o Adobe Analytics para Vídeo]** para habilitar (ativar) o rastreamento do Video Heartbeat.

A partir dessa gravação, a extensão *Visualizadores do Dynamic Media* só estará disponível se a Propriedade Experience Platform Launch for criada para desenvolvimento.

Consulte [Criação de uma propriedade em Experience Platform Launch](#creating-a-property-in-adobe-launch).

Depois que as extensões forem instaladas e configuradas, no mínimo, as cinco extensões a seguir (quatro se você não estiver acompanhando o vídeo) serão listadas na área Extensões > Instaladas.

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### Configuração de elementos de dados e regras {#setting-up-data-elements-and-rules}

No Experience Platform Launch, crie Elementos de dados e Regras necessários para rastrear visualizadores Dynamic Media.

Consulte [Como o rastreamento de dados e eventos funciona na integração](#how-data-and-event-tracking-works-in-the-integration) para obter uma visão geral do rastreamento com o Experience Platform Launch.

Consulte [Exemplo de configuração](#sample-configuration) para obter uma amostra de configuração no Experience Platform Launch que demonstra como rastrear um nome de ativo no carregamento do visualizador.

Consulte [Configuração da extensão do Dynamic Media Viewers](#configuring-the-dynamic-media-viewers-extension) para obter informações detalhadas sobre os recursos da extensão.

### Publicar uma biblioteca {#publishing-a-library}

Para alterar a configuração do Experience Platform Launch (incluindo Propriedade, Extensões, Regras e Elementos de Dados configurados), você deve *publicar* essas alterações. A publicação no Experience Platform Launch é realizada na guia Publicação na configuração Propriedade.

O platform launch pode potencialmente ter vários ambientes de desenvolvimento, um ambiente de armazenamento temporário e um ambiente de produção. Por padrão, a Configuração da nuvem do Platform launch no Experience Manager aponta o nó do autor do Experience Manager para o ambiente Stage do Platform launch. O nó Experience Manager publish aponta para o ambiente Production of Platform launch. Essa disposição significa que, com as configurações padrão de Experience Manager, é necessário publicar a biblioteca de Platforms launch no ambiente de preparo. Isso permite que você o use no Experience Manager. Em seguida, você pode publicá-lo no ambiente Produção para que possa ser usado na publicação do Experience Manager.

Consulte [Ambiente](https://experienceleague.adobe.com/docs/launch/using/reference/publish/environments/environments.html#environment-types) para obter mais informações sobre ambientes Experience Platform Launch.

A publicação de uma biblioteca envolve as duas etapas a seguir:

* Adicionar e criar uma nova biblioteca incluindo todas as alterações necessárias (novas e atualizações) na biblioteca.
* Mover a biblioteca pelos diferentes níveis de ambiente (de Desenvolvimento para Armazenamento temporário e produção)

#### Adicionar e criar uma nova biblioteca {#adding-and-building-a-new-library}

1. Na primeira vez que você abrir a guia Publicação no Experience Platform Launch, a lista da biblioteca estará vazia.

   Na coluna esquerda, clique em **[!UICONTROL Adicionar nova biblioteca]**.

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. Na página Criar nova biblioteca, no campo **[!UICONTROL Nome]**, digite o nome descritivo da nova biblioteca. Por exemplo,

   *DynamicMediaViewersLib*

   Na lista suspensa Ambiente, escolha o nível do Ambiente. Inicialmente, apenas o Nível de desenvolvimento está disponível para seleção. Próximo ao lado inferior esquerdo da página, clique em **[!UICONTROL Adicionar todos os recursos alterados]**.

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. Perto do canto superior direito da página, clique em **[!UICONTROL Salvar e construir para o Desenvolvimento]**.

   Em poucos minutos, a biblioteca é criada e pronta para ser usada.

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >Na próxima vez que você alterar a configuração do Experience Platform Launch, vá para a guia **[!UICONTROL Publishing]** na configuração **[!UICONTROL Propriedade]** e clique na biblioteca criada anteriormente.
   >
   >
   >Na tela de publicação da biblioteca, clique em **[!UICONTROL Adicionar todos os recursos alterados]** e, em seguida, clique em **[!UICONTROL Salvar e construir para desenvolvimento]**.

#### Mover uma biblioteca pelos níveis de ambiente {#moving-a-library-up-through-environment-levels}

1. Depois que uma nova biblioteca é adicionada, ela é encontrada no ambiente de desenvolvimento. Para movê-lo para o nível do ambiente de preparo (que corresponde à coluna Enviado), no menu suspenso da biblioteca, clique em **[!UICONTROL Enviar para aprovação]**.

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. Na caixa de diálogo de confirmação, clique em **[!UICONTROL Enviar]**.

   Depois que a biblioteca for movida para a coluna Enviado, no menu suspenso da biblioteca, clique em **[!UICONTROL Criar para armazenamento temporário]**.

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. Para mover a biblioteca do ambiente de preparo para o ambiente de produção (que é a coluna Publicado), siga um processo semelhante.

   Primeiro, no menu suspenso, clique em **[!UICONTROL Aprovar para publicação]**.

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. No menu suspenso, clique em **[!UICONTROL Criar e publicar na produção]**.

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   Consulte [Publicação](https://experienceleague.adobe.com/docs/launch/using/reference/publish/overview.html#reference) para obter mais informações sobre o processo de publicação no Experience Platform Launch.

## Configuração da Adobe Experience Manager para a integração {#configuring-adobe-experience-manager-for-the-integration}

Pré-requisitos:

* AEM executa as instâncias Autor e Publicar.
* AEM nó do autor está configurado no Dynamic Media - modo de execução Scene7 (dynamicmedia_s7)
* Os componentes Dynamic Media WCM estão habilitados no AEM Sites.

A configuração AEM consiste nas duas etapas principais a seguir:

* Configuração do AEM IMS.
* Configuração da Experience Platform Launch Cloud.

### Configurando AEM IMS {#configuring-aem-ims}

1. Em AEM autor, clique no ícone Ferramentas (martelo) e, em seguida, clique em **[!UICONTROL Segurança > Configurações de IMS de Adobe]**.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. Na página Configuração IMC de Adobe, próximo ao canto superior esquerdo, clique em **[!UICONTROL Criar]**.
1. Na página **[!UICONTROL Configuração técnica de conta Adobe IMS]**, na lista suspensa **[!UICONTROL Solução em nuvem]**, clique em **[!UICONTROL Experience Platform Launch]**.
1. Ative **[!UICONTROL Crie um novo certificado]** e, no campo de texto, digite qualquer valor significativo para o seu certificado. Por exemplo, *AdobeLaunchIMSCert*. Clique em **[!UICONTROL Criar certificado]**.

   A seguinte mensagem de informações é exibida:

   *Para recuperar um token de acesso válido, a chave pública do novo certificado é adicionada à conta técnica no Adobe I/O!*.

   Para descartar a caixa de diálogo Informações, clique em **[!UICONTROL OK]**.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. Para baixar um arquivo de chave pública (*.crt) no sistema local, clique em **[!UICONTROL Baixar chave pública]**.

   >[!NOTE]
   >
   >Nesse momento, ***deixe aberta*** a página **[!UICONTROL Configuração da conta técnica do Adobe IMS]**; ***não*** feche a página e ***não*** clique em Avançar. Você retornará a esta página mais tarde nas etapas.

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. Em uma nova guia do navegador, navegue até [[!DNL Adobe I/O] Console](https://console.adobe.io/integrations).

1. Na página **[!UICONTROL Integrações do console do Adobe I/O]**, próximo ao canto superior direito, clique em **[!UICONTROL Nova integração]**.
1. Na caixa de diálogo **[!UICONTROL Criar uma nova integração]**, verifique se o botão de opção **[!UICONTROL Acessar uma API]** está selecionado e clique em **[!UICONTROL Continuar]**.

   ![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. Na segunda página **[!UICONTROL Criar uma nova integração]**, habilite (ative) o botão de opção **[!UICONTROL API do Experience Platform Launch]**. No canto inferior direito da página, clique em **[!UICONTROL Continuar]**.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. Na terceira página **[!UICONTROL Criar uma nova integração]**, faça o seguinte:

   * No campo **[!UICONTROL Name]**, insira o nome descritivo. Por exemplo, *DynamicMediaViewersIO*.

   * No campo **[!UICONTROL Descrição]**, insira a descrição da integração.

   * Na área **[!UICONTROL Certificados de chave pública]**, carregue o arquivo de chave pública (*.crt) que você baixou anteriormente nessas etapas.

   * No cabeçalho **[!UICONTROL Selecione uma função para API de Experience Platform Launch]**, selecione **[!UICONTROL Admin]**.

   * No cabeçalho **[!UICONTROL Selecione um ou mais perfis de produto para a API Experience Platform Launch]**, selecione o perfil de produto chamado **[!UICONTROL Iniciar - &lt;nome_da_empresa>]**.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. Clique em **[!UICONTROL Criar integração]**.
1. Na página **[!UICONTROL Integração criada]**, clique em **[!UICONTROL Continuar para os detalhes da integração]**.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. Uma página de detalhes de Integrações é exibida, **** semelhante ao seguinte:

   >[!NOTE]
   >
   >***Deixe aberta esta página de Detalhes da integração***. Você precisará de várias informações das guias **[!UICONTROL Visão geral]** e **[!UICONTROL JWT]** em apenas um momento.

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)

   Página de detalhes da integração.

1. Retorne à página **[!UICONTROL Configuração de conta técnica do Adobe IMS]** que você deixou aberta anteriormente. No canto superior direito da página, clique em **[!UICONTROL Avançar]** para abrir a página **[!UICONTROL Conta]** na janela **[!UICONTROL Configuração de conta técnica do Adobe IMS]**.

   (Se você fechou a página acidentalmente antes, volte ao autor do Experience Manager e clique em **[!UICONTROL Ferramentas > Segurança > Configurações do Adobe IMS]**. Clique em **[!UICONTROL Criar]**. Na lista suspensa **[!UICONTROL Solução em nuvem]**, selecione **[!UICONTROL Experience Platform Launch]**. Na lista suspensa **[!UICONTROL Certificado]**, selecione o nome do certificado criado anteriormente.)

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)

   Configuração técnica de conta Adobe IMS - página Certificado.

1. A página **[!UICONTROL Account]** tem cinco campos que você deve preencher usando as informações da página de detalhes da integração da etapa anterior.

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)

   Configuração técnica de conta Adobe IMS - página Conta.

1. Na página **[!UICONTROL Conta]**, preencha os seguintes campos:

   * **[!UICONTROL Título]**  - Informe um título descritivo da conta.
   * **[!UICONTROL Servidor]**  de autorização - Retorne à página de detalhes da integração aberta anteriormente. Clique na guia **[!UICONTROL JWT]**. Copie o nome do servidor, sem o caminho, conforme destacado abaixo.

(o nome do servidor de exemplo é apenas para fins ilustrativos)   Retorne à página **[!UICONTROL Conta]** e cole o nome no respectivo campo.
Por exemplo, `https://ims-na1.adobelogin.com/`
(o nome do servidor de exemplo é apenas para fins ilustrativos)

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)

   Página de detalhes da integração - guia JWT

1. **[!UICONTROL Chave da API]** - Retorne à página de detalhes da integração. Clique na guia **[!UICONTROL Visão geral]** e, à direita do campo **[!UICONTROL Chave da API (ID do cliente)]**, clique em **[!UICONTROL Copiar]**.

   Retorne à página **[!UICONTROL Conta]** e cole a tecla no respectivo campo ****de.

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)

   Página de detalhes da integração.

1. **[!UICONTROL Segredo do cliente]** - Retorne à página Detalhes da integração. Na guia **[!UICONTROL Visão geral]**, clique em **[!UICONTROL Recuperar segredo do cliente]**. À direita do campo **[!UICONTROL Segredo do cliente]**, clique em **[!UICONTROL Copiar]**.

   Retorne à página **[!UICONTROL Conta]** e cole a chave no respectivo campo.

1. **[!UICONTROL Carga]**  - Retorne à página de detalhes da Integração. Na guia **[!UICONTROL JWT]**, no campo Carga JWT, copie todo o código do objeto JSON.

   Retorne à página **[!UICONTROL Conta]** e cole o código no respectivo campo.

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)

   Página de detalhes da integração - guia JWT

   A página Conta, com todos os campos preenchidos, é semelhante ao seguinte:

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. Perto do canto superior direito da página **[!UICONTROL Conta]**, clique em **[!UICONTROL Criar]**.

   Com AEM IMS configurado, agora você tem uma nova IMSAccount listada em **[!UICONTROL Configurações IMS Adobe]**.

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## Configuração da Experience Platform Launch Cloud para integração {#configuring-adobe-launch-cloud-for-the-integration}

1. Em AEM autor, próximo ao canto superior esquerdo, clique no ícone Ferramentas (martelo) e, em seguida, clique em **[!UICONTROL Cloud Services > Configurações de Experience Platform Launch]**.

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. Na página **[!UICONTROL Configurações de Experience Platform Launch]**, no painel esquerdo, selecione um Site AEM para o qual deseja aplicar a Configuração de Experience Platform Launch.

   Somente para fins de ilustração, o Site **[!UICONTROL We.Retail]** é selecionado na captura de tela abaixo.

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. Ao lado do canto superior esquerdo da página, clique em **[!UICONTROL Criar]**.
1. Na página **[!UICONTROL Geral]** (páginas de 1/3) da janela **[!UICONTROL Criar Configuração de Experience Platform Launch]**, preencha os seguintes campos:

   * **[!UICONTROL Título]**  - insira um título de configuração descritiva. Por exemplo, `We.Retail Launch cloud configuration`.

   * **[!UICONTROL Configuração]**  Adobe IMS associada: selecione a configuração IMS criada anteriormente em  [Configuração AEM IMS](#configuring-aem-ims).

   * **[!UICONTROL Empresa]**  - Na lista  **** suspensa Empresa, selecione a empresa da Experience Cloud. A lista é preenchida automaticamente.

   * **[!UICONTROL Propriedade]**  - Na lista suspensa Propriedade, selecione a propriedade Experience Platform Launch que você criou anteriormente. A lista é preenchida automaticamente.
   Depois de preencher todos os campos, sua página **[!UICONTROL Geral]** será semelhante ao seguinte:

   ![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. Próximo ao canto superior esquerdo, clique em **[!UICONTROL Próximo]**.
1. Na página **[!UICONTROL Armazenamento temporário]** (2/3 páginas) da janela **[!UICONTROL Criar configuração de Experience Platform Launch]**, preencha o seguinte campo:

   No campo **[!UICONTROL URI da biblioteca]**, verifique o local da versão de preparo da biblioteca de Experience Platform Launch. O AEM preenche esse campo automaticamente.

   Apenas para fins de ilustração, esta etapa usa bibliotecas de Experience Platform Launch que são implantadas no Adobe CDN.

   >[!NOTE]
   >
   >Verifique se o URI da biblioteca preenchido automaticamente (Uniform Resource Identifier) não está malformado. Se necessário, corrija-o para que o URI represente um URI relativo ao protocolo. Ou seja, ele start de uma duplo para a frente.
   >
   >
   >Por exemplo: `//assets.adobetm.com/launch-xxxx`.

   Sua página **[!UICONTROL Preparando]** provavelmente aparecerá semelhante ao seguinte. As opções **[!UICONTROL Arquivar]** e **[!UICONTROL Carregar biblioteca assíncronas]** estão ***e não*** definidas:

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. Próximo ao canto superior direito, clique em **[!UICONTROL Próximo]**.
1. Na página **[!UICONTROL Production]** (3/3 páginas) da janela **[!UICONTROL Create Experience Platform Launch Configuration]**, se necessário, corrija o URI de produção preenchido automaticamente de modo semelhante ao que foi feito na página anterior **[!UICONTROL Staging]**.
1. Próximo ao canto superior direito, clique em **[!UICONTROL Criar]**.

   Sua nova configuração da Experience Platform Launch Cloud agora é criada e listada ao lado do site, como no exemplo a seguir:

1. Selecione sua nova configuração da Experience Platform Launch Cloud (uma marca de seleção é exibida à esquerda do título da configuração quando ela é selecionada). Na barra de ferramentas, clique em **[!UICONTROL Publicar]**.

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

Atualmente, AEM autor não suporta a integração de Visualizadores Dynamic Media com o Experience Platform Launch.

No entanto, ele é suportado no nó de publicação Experience Manager. Usando as configurações padrão de Configuração da nuvem de Platform launch, o nó de publicação de Experience Manager usa o ambiente de produção do Experience Platform Launch. Dessa forma, é necessário enviar atualizações da biblioteca de Experience Platform Launch do Desenvolvimento para o ambiente de produção todas as vezes durante o teste.

É possível contornar essa limitação. Especifique o URL de desenvolvimento ou armazenamento temporário da biblioteca de Platforms launch na configuração da Platform launch Cloud para o nó de publicação do Experience Manager acima. Isso faz com que o nó de publicação de Experience Manager use a versão de Desenvolvimento ou armazenamento temporário da biblioteca de Platforms launch.

Consulte [Integrar AEM com o Experience Platform Launch Via [!DNL Adobe I/O]](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html) para obter mais informações sobre como configurar a Configuração da Experience Platform Launch Cloud.
