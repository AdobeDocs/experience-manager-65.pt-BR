---
title: Integrar visualizadores do Dynamic Media com tags do Analytics e da Adobe Experience Platform
description: Saiba mais sobre a extensão Visualizadores do Dynamic Media para Tags do Experience Platform e Visualizadores do Dynamic Media 5.13. Ela permite que clientes de Adobe Analytics e Tags do Experience Platform usem eventos e dados específicos para Visualizadores do Dynamic Media em suas configurações de Tags do Experience Platform.
mini-toc-levels: 3
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Viewers
role: User, Admin,Developer,Data Engineer,Data Architect
exl-id: 161dfe22-bc1c-4b60-8ab6-a19407a39e2e
source-git-commit: b5cf18d8e83786a23005aadf8aafe43d006a2e67
workflow-type: tm+mt
source-wordcount: '6633'
ht-degree: 7%

---

# Integrar visualizadores do Dynamic Media com tags do Analytics e da Adobe Experience Platform {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## O que é a integração dos visualizadores do Dynamic Media com as tags Adobe Analytics e Experience Platform? {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

<!-- Leave this hidden path here; it points to the topic source from Sasha https://wiki.corp.adobe.com/pages/viewpage.action?spaceKey=~oufimtse&title=Dynamic+Media+Viewers+integration+with+Adobe+Launch -->

*Visualizadores do Dynamic Media* A extensão para Tags do Experience Platform e Visualizadores do Dynamic Media 5.13 permite que os clientes das Tags do Adobe Analytics e Experience Platform usem eventos e dados específicos para visualizadores do Dynamic Media em sua configuração de Tags do Experience Platform.

Essa integração significa que você pode rastrear o uso de visualizadores do Dynamic Media no seu site com o Adobe Analytics. Ao mesmo tempo, você pode usar os eventos e dados expostos pelos visualizadores com qualquer outra extensão de Tags do Experience Platform que vem do Adobe ou de terceiros.

Para saber mais sobre extensões do Adobe ou de terceiros, consulte [Extensões do Adobe](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html) no Guia do usuário de Tags do Experience Platform.

**Este tópico destina-se ao seguinte:** Administradores de site, desenvolvedores no Experience Platform e pessoas em operações.

### Limitações da integração {#limitations-of-the-integration}

* A integração de Tags Experience Platform para visualizadores Dynamic Media não funciona no nó de autor do Experience Manager. Não é possível ver nenhum rastreamento de uma página do WCM até que ela seja publicada.
* A integração de Tags de Experience Platform para visualizadores do Dynamic Media não é compatível com o modo de operação &quot;pop-up&quot;, onde o URL do visualizador é obtido usando o botão &quot;URL&quot; na página Detalhes do ativo.
* A integração de Tags do Experience Platform não pode ser usada simultaneamente com a integração do Analytics de visualizadores herdados (por meio do `config2=` parâmetro).
* O suporte para rastreamento de vídeo está limitado ao rastreamento de &quot;reprodução principal&quot;, conforme descrito em [Visão geral do rastreamento](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html#player-events). Especificamente, o rastreamento de QoS, Anúncios, Capítulo/Segmentos ou Erros não é suportado.
* A configuração da Duração do armazenamento para Elementos de dados não é compatível com Elementos de dados que usam o *Visualizadores do Dynamic Media* extensão. Duração do armazenamento deve ser definida como **[!UICONTROL Nenhum]**.

### Casos de uso da integração {#use-cases-for-the-integration}

O principal caso de uso da integração com Tags do Experience Platform são os clientes que usam os ativos Adobe Experience Manager e o Adobe Experience Manager Sites. Nesses cenários, você pode configurar uma integração padrão entre o nó Experience Manager author e as Tags do Experience Platform e, em seguida, associar a instância do Sites à propriedade Tags do Experience Platform. Depois disso, qualquer componente WCM do Dynamic Media adicionado a uma página do Sites rastreará os dados e eventos dos visualizadores.

Consulte [Rastrear visualizadores do Dynamic Media no Experience Manager Sites](#tracking-dynamic-media-viewers-in-aem-sites).

Um caso de uso secundário suportado pela integração são os clientes que usam somente o Experience Manager Assets ou o Dynamic Media Classic. Nesses casos, você obtém o código de inserção do visualizador e o adiciona à página do site. Em seguida, obtenha o URL de produção da biblioteca de Tags de Experience Platform e adicione-o manualmente ao código da página da Web.

Consulte [Rastrear visualizadores do Dynamic Media usando o código incorporado](#tracking-dynamic-media-viewers-using-embed-code).

<!-- Path on internal wiki [About tracking Dynamic Media viewers using embed code](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersusingEmbedcode). -->

## Como o rastreamento de dados e eventos funciona na integração {#how-data-and-event-tracking-works-in-the-integration}

A integração aproveita dois tipos separados e independentes de rastreamento de visualizadores do Dynamic Media: *Adobe Analytics* e *Adobe Analytics para áudio e vídeo*.

### Sobre o rastreamento usando o Adobe Analytics  {#about-tracking-using-adobe-analytics}

O Adobe Analytics permite que você rastreie ações executadas pelo usuário final quando elas interagem com os Visualizadores do Dynamic Media em seu site. O Adobe Analytics também permite rastrear dados específicos do visualizador. Por exemplo, você pode rastrear e registrar eventos de carregamento de exibição junto com o nome do ativo, quaisquer ações de zoom que ocorreram e as ações de reprodução de vídeo.

Em Tags de Experience Platform, os conceitos de *Elementos de dados* e *Regras* trabalhe em conjunto para ativar o rastreamento do Adobe Analytics.

#### Sobre elementos de dados em tags Experience Platform {#about-data-elements-in-adobe-launch}

Um Elemento de dados em Tags Experience Platform é uma propriedade nomeada cujo valor é definido estaticamente ou calculado dinamicamente com base no estado de uma página da Web ou nos dados de Visualizadores do Dynamic Media.

As opções disponíveis para uma definição de Elemento de dados dependem da lista de Extensões instaladas na Propriedade de Tags do Experience Platform. A extensão &quot;Core&quot; é pré-instalada e está disponível para uso imediato em qualquer configuração. Essa extensão &quot;Core&quot; permite definir um Elemento de dados cujo valor provém de cookie, código JavaScript, sequência de consulta e muitas outras fontes.

Para o rastreamento do Adobe Analytics, várias outras extensões devem ser instaladas, conforme descrito em [Instalação e configuração de extensões](#installing-and-setup-of-extensions). A extensão Visualizadores do Dynamic Media adiciona uma capacidade de definir um Elemento de dados que é um argumento do evento Visualizador dinâmico. Por exemplo, é possível fazer referência ao tipo de visualizador ou ao nome do ativo relatado pelo visualizador quando carregado, o nível de zoom relatado quando o usuário final faz zoom e muito mais.

A extensão Visualizador do Dynamic Media mantém os valores de seus Elementos de dados atualizados automaticamente.

Depois de defini-lo, um Elemento de dados pode ser usado em outros locais da interface do usuário de Tags do Experience Platform, usando o widget seletor de elementos de dados. Especificamente, os Elementos de dados definidos para as finalidades do rastreamento de Visualizadores do Dynamic Media são referenciados pela Ação Definir variáveis da extensão Adobe Analytics na Regra (veja abaixo).

Consulte [Elementos de dados](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html).

#### Sobre regras em tags Experience Platform {#about-rules-in-adobe-launch}

Uma Regra em Tags de Experience Platform é uma configuração agnóstica que define três áreas que compõem uma regra: *Eventos*, *Condições* e *Ações*:

* *Eventos* (if) informa às Tags de Experience Platform quando acionar uma regra.
* *Condições* (if) informa às Tags de Experience Platform que outras restrições serão permitidas ou não durante o acionamento de uma Regra.
* *Ações* (em seguida) informa às Tags de Experience Platform o que fazer quando uma Regra é acionada.

As opções disponíveis na seção Eventos, Condições e Ações dependem das extensões instaladas na Propriedade de Tags do Experience Platform. O *Núcleo* A extensão do é pré-instalada e está disponível para uso imediato em qualquer configuração. A extensão fornece várias opções para Eventos, como ações básicas no nível do navegador. Essas ações incluem mudança de foco, pressionamentos de tecla e envios de formulário. Também inclui opções para Condições, como valor do cookie, tipo de navegador e muito mais. Para Ações, somente a opção Código personalizado está disponível.

Para o rastreamento do Adobe Analytics, várias outras extensões devem ser instaladas, conforme descrito em [Instalação e configuração de extensões](#installing-and-setup-of-extensions). Especificamente:

* A extensão Visualizadores do Dynamic Media estende a lista de Eventos suportados para eventos específicos dos visualizadores do Dynamic Media, como carregamento do visualizador, troca de ativos, zoom e reprodução de vídeo.
* A extensão Adobe Analytics estende a lista de ações compatíveis com duas ações necessárias para enviar dados para servidores de rastreamento: *Definir variáveis* e *Enviar beacon*.

Para rastrear visualizadores do Dynamic Media, é possível usar qualquer tipo de um dos seguintes itens:

* Eventos da extensão do Dynamic Media Viewers, da extensão principal ou de qualquer outra extensão.
* Condições na definição da regra. Ou você pode deixar a área de condições vazia.

Na seção Ações , é necessário que você tenha uma *Definir variáveis* ação. Essa ação informa ao Adobe Analytics como preencher variáveis de rastreamento com dados. Ao mesmo tempo, a variável *Definir variáveis* não envia nada para o servidor de rastreamento.

O *Definir variáveis* deve ser seguida de uma *Enviar beacon* ação. O *Enviar beacon* na verdade envia dados para o servidor de rastreamento do analytics. Ambas as ações, *Definir variáveis* e *Enviar beacon*, vêm da extensão do Adobe Analytics.

Consulte [Regras](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html).

#### Exemplo de configuração {#sample-configuration}

A configuração de exemplo a seguir em Tags de Experience Platform demonstra como rastrear um nome de ativo no carregamento do visualizador.

1. No **[!UICONTROL Elementos de dados]** , defina um elemento de dados `AssetName` que referenciam `asset` do `LOAD` da extensão Visualizadores do Dynamic Media.

   ![image2019-11](assets/image2019-11.png)

1. No **[!UICONTROL Regras]** , definir uma regra *TrackAssetOnLoad*.

   Nessa regra, a variável **[!UICONTROL Evento]** O campo usa a variável **[!UICONTROL CARREGAR]** da extensão Visualizadores do Dynamic Media.

   ![image2019-22](assets/image2019-22.png)

1. A configuração Ação tem dois tipos de Ação da extensão Adobe Analytics:

   *Definir variáveis*, que mapeia uma variável do analytics de sua escolha para o valor de `AssetName` Elemento de dados.

   *Enviar beacon*, que envia informações de rastreamento para o Adobe Analytics.

   ![image2019-3](assets/image2019-3.png)

1. A configuração de regra resultante é semelhante ao seguinte:

   ![image2019-4](assets/image2019-4.png)

### Sobre o Adobe Analytics para áudio e vídeo {#about-adobe-analytics-for-audio-and-video}

Quando uma conta do Experience Cloud é inscrita para usar o Adobe Analytics para áudio e vídeo, é suficiente ativar o rastreamento de vídeo na *Visualizadores do Dynamic Media* configurações de extensão. As métricas de vídeo se tornam disponíveis no Adobe Analytics. O rastreamento de vídeo depende da presença da extensão Adobe Medium Analytics for Audio and Video.

Consulte [Instalação e configuração de extensões](#installing-and-setup-of-extensions).

Atualmente, o suporte para rastreamento de vídeo está limitado somente ao rastreamento de &quot;reprodução principal&quot;, conforme descrito em [Visão geral do rastreamento](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html#player-events). Especificamente, o rastreamento de QoS, Anúncios, Capítulo/Segmentos ou Erros não é suportado.

## Usar a extensão Visualizadores do Dynamic Media {#using-the-dynamic-media-viewers-extension}

Conforme mencionado no [Casos de uso da integração](#use-cases-for-the-integration), é possível rastrear os visualizadores do Dynamic Media com a nova integração de Tags do Experience Platform no Experience Manager Sites e usando o código incorporado.

### Rastrear visualizadores do Dynamic Media no Experience Manager Sites {#tracking-dynamic-media-viewers-in-aem-sites}

Para rastrear visualizadores do Dynamic Media no Experience Manager Sites, todas as etapas listadas na [Configurar todas as partes da integração](#configuring-all-the-integration-pieces) deve ser executada. Especificamente, você deve criar a configuração IMS e a configuração da nuvem de tags do Experience Platform.

Após a configuração correta, qualquer visualizador do Dynamic Media adicionado a uma página Sites, usando um componente WCM suportado pelo Dynamic Media, rastreia automaticamente os dados para o Adobe Analytics ou Adobe Analytics para Vídeo, ou ambos.

<!-- To be reviewed and updated although this is found live in the Experience ManageraaCS version:
See [Adding Dynamic Media Assets to Pages using Adobe Sites](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html).
-->

### Rastrear visualizadores do Dynamic Media usando o código incorporado {#tracking-dynamic-media-viewers-using-embed-code}

Os clientes que não usam o Experience Manager Sites ou incorporam visualizadores do Dynamic Media em páginas da Web fora do Experience Manager Sites, ou ambos, ainda podem usar a integração de Tags do Experience Platform.

Complete as etapas de configuração no [Configurar o Adobe Analytics](#configuring-adobe-analytics-for-the-integration) e [Configurar tags de Experience Platform](#configuring-adobe-launch-for-the-integration) seções. No entanto, as etapas de configuração relacionadas ao Experience Manager não são necessárias.

Após a configuração correta, você pode adicionar suporte a Tags de Experience Platform a uma página da Web com um visualizador do Dynamic Media.

Consulte [Adicionar o código de inserção de tags de Experience Platform](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html#configure-launch) para saber mais sobre como usar o código incorporado da biblioteca de Tags do Experience Platform.

<!-- To be reviewed and updated although this is found live in the Experience ManageraaCS version:
See [Embedding the Video or Image Viewer on a Web Page](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html) to learn more about how to use the embed code feature of Experience Manager Dynamic Media.
-->

**Rastrear visualizadores do Dynamic Media usando o código incorporado:**

1. Ter uma página da Web pronta para incorporar um visualizador do Dynamic Media.
1. Obtenha o código incorporado da biblioteca de Tags do Experience Platform fazendo logon primeiro em Tags do Experience Platform (consulte [Configuração de tags de Experience Platform](#configuring-adobe-launch-for-the-integration)).
1. Selecionar **[!UICONTROL Propriedade]**, em seguida, selecione o **[!UICONTROL Ambientes]** guia .
1. Escolha o nível de Ambiente que seja relevante para o ambiente da página da Web. Em seguida, no **[!UICONTROL Instalar]** selecione o ícone de caixa .
1. **[!UICONTROL Nas Instruções de Instalação na Web]** caixa de diálogo, copie o código incorporado completo da biblioteca de Tags de Experience Platform, juntamente com o `<script/>` tags.

## Guia de referência para a extensão Visualizadores do Dynamic Media {#reference-guide-for-the-dynamic-media-viewers-extension}

### Sobre a configuração dos visualizadores do Dynamic Media {#about-the-dynamic-media-viewers-configuration}

A extensão do Visualizador do Dynamic Media integra-se automaticamente à biblioteca de Tags do Experience Platform se as seguintes condições forem verdadeiras:

* Objeto global da biblioteca de Tags de Experience Platform ( `_satellite`) está presente na página.
* A função de extensão Visualizadores do Dynamic Media `_dmviewers_v001()` é definido em `_satellite`.

* `config2=` O parâmetro do visualizador não é especificado, o que significa que o visualizador não usa a integração herdada do Analytics.

Além disso, há uma opção para desativar explicitamente a integração de Tags de Experience Platform no visualizador especificando `launch=0` na configuração do visualizador. O valor padrão desse parâmetro é `1`.

### Configurar a extensão Visualizadores do Dynamic Media {#configuring-the-dynamic-media-viewers-extension}

A única opção de configuração para a extensão Visualizadores do Dynamic Media é **[!UICONTROL Ativar o Adobe Medium Analytics para áudio e vídeo]**.

Ao marcar (habilitar) essa opção e a extensão Adobe Medium Analytics for Audio and Video estiver instalada e configurada, as métricas de reprodução de vídeo serão enviadas à solução Adobe Analytics para áudio e vídeo. Desativar esta opção desativa o rastreamento de vídeo.

Se você ativar esta opção *without* com a extensão Adobe Medium Analytics for Audio and Video instalada, a opção não terá efeito.

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### Sobre elementos de dados na extensão Visualizadores do Dynamic Media {#about-data-elements-in-the-dynamic-media-viewers-extension}

O único tipo de Elemento de dados fornecido pela extensão Visualizadores do Dynamic Media é o **[!UICONTROL Evento do visualizador]** na lista suspensa **[!UICONTROL Tipo de elemento de dados]**.

Quando selecionado, o editor de Elemento de dados renderiza um formulário com dois campos:

* **[!UICONTROL Tipo de dados do evento de visualizadores do DM]** - uma lista suspensa que identifica todos os eventos do visualizador compatíveis com a extensão do Visualizador do Dynamic Media que têm argumentos, além de um item **[!UICONTROL COMMON]** especial. Um item **[!UICONTROL COMUM]** representa uma lista de parâmetros de evento comuns a todos os tipos de eventos enviados pelos visualizadores.
* **[!UICONTROL Parâmetro de rastreamento]** - um argumento do evento do visualizador do Dynamic Media selecionado.

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

Consulte a [Guia de referência de visualizadores do Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) para obter a lista de eventos suportados por cada tipo de visualizador; vá para a seção visualizador específico e selecione Suporte para a subseção de rastreamento do Adobe Analytics . No momento, o guia de referência Visualizadores do Dynamic Media não documenta argumentos de evento.

Agora considere o ciclo de vida dos visualizadores do Dynamic Media *Elemento de dados*. O valor desse Elemento de dados é preenchido depois que o evento do visualizador do Dynamic Media correspondente ocorre na página. Por exemplo, suponha que o Elemento de dados aponte para a variável **[!UICONTROL CARREGAR]** e seu argumento &quot;asset&quot;. Nesse caso, o valor desse Elemento de dados recebe dados válidos depois que o visualizador executa a variável **[!UICONTROL CARREGAR]** pela primeira vez. Se o elemento de dados apontar para a variável **[!UICONTROL ZOOM]** e seu argumento &quot;scale&quot;, o valor de tal Elemento de dados permanece vazio até que o visualizador envie uma **[!UICONTROL ZOOM]** pela primeira vez.

Da mesma forma, os valores dos Elementos de dados são atualizados automaticamente quando o visualizador envia um evento correspondente na página. A atualização de valor acontece mesmo se o evento específico não for definido na configuração Regra. Por exemplo, suponha que o elemento de dados **[!UICONTROL ZoomScale]** é definido para o parâmetro &quot;scale&quot; do evento ZOOM. No entanto, a única regra presente na configuração Regra é acionada pela variável **[!UICONTROL CARREGAR]** evento. O valor de **[!UICONTROL ZoomScale]** O ainda é atualizado sempre que um usuário executa o zoom dentro do visualizador.

Qualquer visualizador do Dynamic Media tem um identificador exclusivo na página da Web. O Elemento de dados rastreia o próprio valor e o visualizador o preencheu. Por exemplo, suponha que haja vários visualizadores na mesma página e um **[!UICONTROL AssetName]** Elemento de dados que aponta para o **[!UICONTROL CARREGAR]** e seu argumento &quot;asset&quot;. O **[!UICONTROL AssetName]** O Elemento de dados mantém uma coleção de nomes de ativos associados a cada visualizador carregado na página.

O valor exato retornado pelo Elemento de dados depende do contexto. Se o Elemento de dados for solicitado em uma Regra que foi acionada por um evento do visualizador do Dynamic Media, o valor do Elemento de dados será retornado para o visualizador que iniciou a Regra. E o Elemento de dados é solicitado em uma Regra que foi acionado por um Evento de alguma outra extensão de Tags de Experience Platform. Nesse momento, o valor do Elemento de dados vem do visualizador que foi o último a atualizar esse Elemento de dados.

**Considere a seguinte configuração de exemplo:**

* Uma página da Web que tem dois visualizadores de zoom do Dynamic Media: *viewer1* e *visualizador2*.

* **[!UICONTROL ZoomScale]** O elemento de dados aponta para a variável **[!UICONTROL ZOOM]** e seu argumento &quot;scale&quot;.
* **[!UICONTROL TrackPan]** Regra com o seguinte:

   * Usa o Visualizador do Dynamic Media **[!UICONTROL PAN]** como um acionador.
   * Envia o valor de **[!UICONTROL ZoomScale]** Elemento de dados para o Adobe Analytics.

* **[!UICONTROL TrackKey]** Regra com o seguinte:

   * Usa o evento de pressionamento de tecla da extensão Tags do Experience Platform principal como acionador.
   * Envia o valor de **[!UICONTROL ZoomScale]** Elemento de dados para o Adobe Analytics.

Agora, suponha que o usuário final carregue a página da Web com os dois visualizadores. Em *viewer1*, ampliam para 50% de escala; em seguida, em *visualizador2*, ampliam para 25% de escala. Em *viewer1*, eles deslocam a imagem e finalmente selecionam uma tecla no teclado.

A atividade do usuário final resulta nas duas chamadas de rastreamento a seguir feitas para o Adobe Analytics:

* A primeira chamada ocorre porque **[!UICONTROL TrackPan]** A regra é acionada quando o usuário entra *viewer1*. Essa chamada envia 50% como um valor de **[!UICONTROL ZoomScale]** Elemento de dados porque o Elemento de dados sabe que a Regra é acionada por *viewer1* e obtém o valor de escala correspondente;
* A segunda chamada ocorre porque **[!UICONTROL TrackKey]** A regra é acionada quando o usuário pressiona uma tecla no teclado. Essa chamada envia 25% como um valor de **[!UICONTROL ZoomScale]** Elemento de dados porque a regra não foi acionada pelo visualizador. Dessa forma, o Elemento de dados retorna o valor mais atualizado.

A amostra configurada acima também afeta a duração do valor do Elemento de dados. O valor do Elemento de dados gerenciado pelo Visualizador do Dynamic Media é armazenado no código da biblioteca de Tags do Experience Platform mesmo depois que o próprio visualizador é descartado na página da Web. Essa funcionalidade significa que, se houver uma Regra que é acionada por uma extensão de Visualizador que não é da Dynamic Media e faz referência a esse Elemento de dados, o Elemento de dados retornará o último valor conhecido. Mesmo se o visualizador não estiver mais presente na página da Web.

Em qualquer caso, os valores dos Elementos de dados orientados pelos Visualizadores do Dynamic Media não são armazenados no armazenamento local ou no servidor; em vez disso, elas são mantidas somente na biblioteca de Tags do Experience Platform do lado do cliente. Os valores desse Elemento de dados desaparecem quando a página da Web é recarregada.

Geralmente, o editor de Elemento de dados suporta [seleção da duração do armazenamento](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html#create-a-data-element). No entanto, os Elementos de dados que usam a extensão Visualizadores do Dynamic Media suportam apenas a opção de duração de armazenamento de **[!UICONTROL Nenhum]**. A configuração de qualquer outro valor é possível na interface do usuário, mas o comportamento do Elemento de dados não é definido nesse caso. A extensão gerencia o valor do Elemento de dados sozinho: o Elemento de dados que mantém o valor do argumento de evento do visualizador durante todo o ciclo de vida do visualizador.

### Sobre regras na extensão Visualizadores do Dynamic Media {#about-rules-in-the-dynamic-media-viewers-extension}

No editor de Regras, a extensão adiciona novas opções de configuração para o editor de Eventos. Além disso, o editor fornece uma opção para fazer referência manual aos parâmetros de evento no editor de Ação como uma opção de mão curta, em vez de usar elementos de dados pré-configurados.

#### Sobre o Editor de eventos {#about-the-events-editor}

No Editor de eventos, a extensão Visualizadores do Dynamic Media adiciona um **[!UICONTROL Tipo de evento]** chamado **[!UICONTROL Evento do visualizador]**.

Quando selecionado, o Editor de eventos renderiza o menu suspenso **[!UICONTROL Eventos do visualizador do Dynamic Media]**, listando todos os eventos disponíveis compatíveis com os visualizadores do Dynamic Media.

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### Sobre o editor de Ações {#about-the-actions-editor}

A extensão Visualizadores do Dynamic Media permite usar parâmetros de evento de visualizadores do Dynamic Media para mapear variáveis de análise no editor Definir variáveis da extensão Adobe Analytics.

O método mais simples de fazer isso é concluir o seguinte processo de duas etapas:

* Primeiro, defina um ou mais Elementos de dados, onde cada Elemento de dados representa um parâmetro de um evento do Visualizador do Dynamic Media.
* Finalmente, no editor Definir variáveis da extensão Adobe Analytics, selecione o **[!UICONTROL Elemento de dados]** ícone do seletor (três discos empilhados) para abrir a caixa de diálogo Selecionar elemento de dados e, em seguida, selecionar um elemento de dados a partir dele.

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

No entanto, é possível usar uma abordagem alternativa e ignorar a criação do Elemento de dados. Você pode fazer referência diretamente a um argumento de um evento do Visualizador do Dynamic Media. Insira o nome totalmente qualificado do argumento de evento na **[!UICONTROL value]** campo de entrada da atribuição de variável do Analytics. Certifique-se de rodar com sinais de porcentagem (%). Por exemplo,

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

Há uma diferença importante entre o uso de Elementos de dados e a referência do argumento de evento direto. Para o Elemento de dados, não importa qual evento aciona a ação Definir variáveis . O evento que aciona a Regra pode não estar relacionado ao Visualizador dinâmico. Por exemplo, selecionar a página da Web na extensão principal. Mas, ao usar uma referência de argumento direto, é importante garantir que o evento que aciona a regra corresponda ao argumento de evento que ela faz referência.

Por exemplo, a referência `%event.detail.dm.LOAD.asset%` retornará o nome correto do ativo se Regra for acionado pelo evento **[!UICONTROL LOAD]** da extensão do Visualizador do Dynamic Media. No entanto, retorna um valor vazio para qualquer outro evento.

A tabela a seguir lista os eventos do Visualizador do Dynamic Media e seus argumentos compatíveis:

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

## Configurar todas as partes da integração {#configuring-all-the-integration-pieces}

**ANTES DE COMEÇAR**

O Adobe recomenda que você analise toda a documentação antes desta seção para entender a integração completa.

Esta seção explica as etapas de configuração necessárias para integrar os visualizadores do Dynamic Media com o Adobe Analytics e o Adobe Analytics para áudio e vídeo. Embora o uso da extensão Visualizadores do Dynamic Media para outros propósitos em Tags de Experience Platform, esses cenários não são abordados nesta documentação.

Você usará os seguintes produtos do Adobe para configurar a integração:

* Adobe Analytics - usado para configurar variáveis e relatórios de rastreamento.
* Tags de Experience Platform - usadas para definir uma Propriedade, uma ou mais Regras e um ou mais Elementos de dados para ativar o rastreamento do visualizador.

Além disso, se essa solução de integração for usada com o Experience Manager Sites, a seguinte configuração também deverá ser feita:

* [!DNL Adobe I/O] Console - a integração é criada para Tags do Experience Platform.
* Nó Experience Manager author - Configuração IMS e configuração da nuvem de Experience Platform Tags.

Como parte da configuração, certifique-se de ter acesso a uma empresa no Adobe Experience Cloud que já tenha Adobe Analytics e Experience Platform Tags ativadas.

## Configurar o Adobe Analytics para integração {#configuring-adobe-analytics-for-the-integration}

Após configurar o Adobe Analytics, as seguintes etapas serão configuradas para a integração:

* Um Conjunto de relatórios está no lugar e está selecionado.
* As Variáveis do Analytics estão disponíveis para receber dados de rastreamento.
* Os relatórios estão disponíveis para exibir dados coletados dentro do Adobe Analytics.

Consulte também [Guia de implementação do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html).

**Para configurar o Adobe Analytics para a integração:**

1. Comece acessando o Adobe Analytics a partir do Experience Cloud [página inicial](https://experience.adobe.com/#/home). Na barra de menus, selecione o **[!UICONTROL Soluções]** ícone (uma tabela de pontos três por três) próximo ao canto superior direito da página, em seguida, selecione **[!UICONTROL Analytics]**.

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   Em seguida, selecione um conjunto de relatórios.

### Selecionar um conjunto de relatórios {#selecting-a-report-suite}

1. Próximo ao canto superior direito da página do Adobe Analytics, à direita do campo **[!UICONTROL Pesquisar relatórios]**, selecione o conjunto de relatórios correto na lista suspensa. Se houver vários conjuntos de relatórios disponíveis e você não tiver certeza de qual usar, entre em contato com o administrador do Adobe Analytics, que pode ajudá-lo a selecionar qual usar.

   Na captura de tela abaixo, um usuário criou um conjunto de relatórios chamado *DynamicMediaViewersExtensionDoc* e selecionou na lista suspensa. O nome do conjunto de relatórios é somente um exemplo. O nome do conjunto de relatórios que você selecionar dependerá de você.

   Se nenhum conjunto de relatórios estiver disponível, você ou o administrador da Adobe Analytics devem criar um antes de continuar com a configuração.

   Consulte [Relatórios e conjuntos de relatórios](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html#manage-report-suites) e [Criar um conjunto de relatórios](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).

   No Adobe Analytics, os conjuntos de relatórios são gerenciados em **[!UICONTROL Administrador]** > **[!UICONTROL Conjuntos de relatórios]**.

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   Agora, configure as variáveis do Adobe Analytics.

### Configurar variáveis do Adobe Analytics {#setting-up-adobe-analytics-variables}

1. Atribua uma ou mais variáveis do Adobe Analytics que você deseja usar para rastrear o comportamento dos Visualizadores do Dynamic Media na página da Web.

   É possível usar qualquer tipo de variável compatível com o Adobe Analytics. A decisão sobre o tipo de variável (como Tráfego personalizado) [props], Conversão [eVar]) é orientado pelas necessidades específicas de sua implementação do Analytics.

   Consulte [Visão geral de props e eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html#vars).

   Para os fins desta documentação, somente uma variável de Tráfego personalizado (props) será usada porque se tornam disponíveis em um Relatório do Analytics alguns minutos depois que uma ação ocorre em uma página da Web.

   Para ativar uma nova variável Tráfego personalizado, no Adobe Analytics, na barra de ferramentas, acesse **[!UICONTROL Administrador]** > **[!UICONTROL Conjuntos de relatórios]**.

1. No **[!UICONTROL Gerenciador do Conjunto de relatórios]** selecione o relatório correto e, na barra de ferramentas, navegue até **[!UICONTROL Editar configurações]** > **[!UICONTROL Tráfego]** > **[!UICONTROL Variáveis de tráfego]**.
1. Selecione uma variável que não esteja sendo usada, atribua a ela um nome descritivo (**[!UICONTROL Ativo do visualizador (prop 30)]**) e altere a caixa de combinação para &quot;Ativado&quot; na coluna Ativado .

   A captura de tela a seguir é um exemplo de uma variável de Tráfego personalizado ( **[!UICONTROL prop30]**) para rastrear um nome de ativo usado pelo visualizador:

   ![image2019-6-26_23-6-59](assets/image2019-6-26_23-6-59.png)

1. Na parte inferior da lista de variáveis, selecione **[!UICONTROL Salvar]**.

### Configurar um relatório {#setting-up-a-report}

1. Geralmente, a configuração de um Relatório no Adobe Analytics é orientada por necessidades específicas do projeto. Dessa forma, a configuração detalhada do relatório está além do escopo dessa integração.

   No entanto, é suficiente saber que os relatórios de Tráfego personalizado ficam automaticamente disponíveis no Adobe Analytics depois que você configura as variáveis de Tráfego personalizado em [Configurar variáveis do Adobe Analytics](#setting-up-adobe-analytics-variables).

   Por exemplo, o relatório de **[!UICONTROL Ativo do visualizador (prop 30)]** está disponível no menu Relatórios em **[!UICONTROL Tráfego personalizado]** > **[!UICONTROL Tráfego personalizado 21-30]** > **[!UICONTROL Ativo do visualizador (prop 30)]**.

   Visitar este relatório logo após a criação do **[!UICONTROL Ativo do visualizador (prop 30)]**, não mostra dados; o que é esperado neste momento da integração.

   ![image2019-6-26_23-12-49](assets/image2019-6-26_23-12-49.png)

## Configurar tags de Experience Platform para a integração {#configuring-adobe-launch-for-the-integration}

Após configurar as Tags de Experience Platform, as seguintes etapas serão configuradas para a integração:

* A criação de uma nova propriedade para manter todas as configurações juntas.
* A instalação e configuração das extensões. O código do lado do cliente de todas as extensões instaladas na Propriedade é compilado em conjunto em uma biblioteca. Essa biblioteca é usada posteriormente pela página da Web.
* Configuração de elementos de dados e regras. Essa configuração define quais dados capturar dos visualizadores do Dynamic Media, quando acionar a lógica de rastreamento e onde enviar os dados do visualizador no Adobe Analytics.
* Publicação da biblioteca.

**Para configurar Tags de Experience Platform para a integração:**

1. Comece acessando Tags de Experience Platform do Experience Cloud [página inicial](https://experience.adobe.com/#/home). Na barra de menus, selecione o **[!UICONTROL Soluções]** ícone (três por três tabelas de pontos) próximo ao canto superior direito da página, em seguida, selecione **[!UICONTROL Tags]**.

   Você também pode [abrir Tags do Experience Platform diretamente](https://launch.adobe.com/).

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### Criar uma propriedade em Tags do Experience Platform {#creating-a-property-in-adobe-launch}

Uma propriedade nas Tags do Experience Platform é uma configuração nomeada que mantém todas as configurações juntas. Uma biblioteca das configurações é gerada e publicada em diferentes níveis de ambiente (desenvolvimento, armazenamento temporário e produção).

Consulte também [Criar uma propriedade de Tags](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-mobile-android-apps-with-launch/configure-launch/launch-create-a-property.html#configure-launch).

1. Em Tags de Experience Platform, selecione **[!UICONTROL Nova propriedade]**.
1. Na caixa de diálogo **[!UICONTROL Criar propriedade]**, no campo **[!UICONTROL Nome]**, digite um nome descritivo, como o título do site. Por exemplo, `DynamicMediaViewersProp.`
1. No **[!UICONTROL Domínios]** , insira o domínio do site.
1. No **[!UICONTROL Opções avançadas]** menu suspenso, ativar **[!UICONTROL Configurar para desenvolvimento de extensão (não pode ser modificado mais tarde)]** caso a extensão que você deseja usar, nesse caso, *Visualizadores do Dynamic Media*—ainda não foi lançado.

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. Selecione **[!UICONTROL Salvar]**.

   Selecione a propriedade recém-criada e prossiga para *Instalação e configuração de extensões*.

### Instalação e configuração de extensões {#installing-and-setup-of-extensions}

Todas as extensões disponíveis nas Tags do Experience Platform estão listadas em **[!UICONTROL Extensões]** > **[!UICONTROL Catálogo]**.

Para instalar uma extensão, selecione **[!UICONTROL Instalar]**. Se necessário, execute uma configuração de extensão única e selecione **[!UICONTROL Salvar]**.

Quando necessário, as seguintes extensões devem ser instaladas e configuradas:

* (Obrigatório) *Serviço de ID de Experience Cloud* extensão.

Nenhuma configuração adicional é necessária, aceite para qualquer valor proposto. Quando terminar, selecione **[!UICONTROL Salvar]**.

Consulte [Extensão do Adobe Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html).

* (Obrigatório) *Adobe Analytics* extensão

Para configurar essa extensão, você precisa da ID do conjunto de relatórios encontrada no Adobe Analytics, em **[!UICONTROL Administrador]** > **[!UICONTROL Conjunto de relatórios]** nos termos do **[!UICONTROL ID do conjunto de relatórios]** cabeçalho da coluna.

(Somente para fins de demonstração, a ID do conjunto de relatórios do **[!UICONTROL DynamicMediaViewersExtensionDoc]** O Conjunto de relatórios é usado nas seguintes capturas de tela. Essa ID foi criada e usada em [Selecionar um conjunto de relatórios](#selecting-a-report-suite) mais cedo.)

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

Na página Instalar extensão, digite a ID do conjunto de relatórios no campo **[!UICONTROL Conjuntos de relatórios]**, no campo **[!UICONTROL Conjuntos de relatórios de preparo]** e no campo **[!UICONTROL Conjuntos de relatórios de produção]**.

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*Configure o seguinte item somente se planeja usar o rastreamento de vídeo:*

No **[!UICONTROL Instalar extensão]** página, expandir **[!UICONTROL Geral]**, em seguida, especifique o Servidor de rastreamento. O servidor de rastreamento segue o modelo `<trackingNamespace>.sc.omtrdc.net`, onde `<trackingNamespace>` é a informação obtida no email de provisionamento.

Selecione **[!UICONTROL Salvar]**.

Consulte [Extensão do Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html).

* (Opcional; obrigatório somente se o rastreamento de vídeo for necessário) *Adobe Medium Analytics para áudio e vídeo* extensão

Preencha o campo do servidor de rastreamento. O servidor de rastreamento para *Adobe Medium Analytics para áudio e vídeo* é diferente do servidor de rastreamento usado para o Adobe Analytics. Ele segue o modelo `<trackingNamespace>.hb.omtrdc.net`, onde `<trackingNamespace>` é a informação do email de provisionamento.

Todos os outros campos são opcionais.

Consulte [Extensão Adobe Medium Analytics for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html).

* (Obrigatório) *Visualizadores do Dynamic Media* extensão

Selecione **[!UICONTROL ativar o Adobe Analytics para Vídeo]** para habilitar (ativar) o rastreamento do Video Heartbeat.

A partir dessa escrita, a *Visualizadores do Dynamic Media* A extensão só estará disponível se a propriedade Tags do Experience Platform for criada para desenvolvimento.

Consulte [Criar uma propriedade em Tags do Experience Platform](#creating-a-property-in-adobe-launch).

Depois que as extensões forem instaladas e configuradas, no mínimo, as cinco extensões a seguir (quatro se você não estiver rastreando vídeo) serão listadas na área Extensões > Instalado.

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### Configurar elementos de dados e regras {#setting-up-data-elements-and-rules}

Em Tags de Experience Platform, crie os Elementos de dados e as Regras necessários para rastrear os visualizadores do Dynamic Media.

Consulte [Como o rastreamento de dados e eventos funciona na integração](#how-data-and-event-tracking-works-in-the-integration) para obter uma visão geral do rastreamento com Tags de Experience Platform.

Consulte [Exemplo de configuração](#sample-configuration) para obter uma configuração de exemplo em Tags do Experience Platform que demonstra como rastrear um nome de ativo no carregamento do visualizador.

Consulte [Configurar a extensão Visualizadores do Dynamic Media](#configuring-the-dynamic-media-viewers-extension) para obter informações detalhadas sobre os recursos da extensão.

### Publicar uma biblioteca {#publishing-a-library}

Para alterar a configuração das Tags do Experience Platform (incluindo a configuração de Propriedade, Extensões, Regras e Elementos de Dados), você deve *publicar* tais alterações. A publicação em Tags do Experience Platform é executada a partir da guia Publicação na configuração Propriedade.

As Tags do Experience Platform podem ter vários ambientes de desenvolvimento, um ambiente de preparo e um ambiente de produção. Por padrão, a Configuração da nuvem de Experience Platform Tags no Experience Manager aponta o nó Experience Manager author para o ambiente Stage das Experience Platform Tags. O nó Experience Manager Publish aponta para o ambiente de produção das Tags do Experience Platform. Esse arranjo significa que, com as configurações padrão do Experience Manager, é necessário publicar a biblioteca de Tags do Experience Platform no ambiente de preparo. Isso permite usá-lo no Experience Manager author. Em seguida, você pode publicá-lo no ambiente de Produção para que ele possa ser usado na publicação do Experience Manager.

Consulte [Ambientes](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html) para obter mais informações sobre ambientes de Tags do Experience Platform.

A publicação de uma biblioteca envolve as duas etapas a seguir:

* Adicionar e criar uma nova biblioteca incluindo todas as alterações necessárias (novas e atualizações) na biblioteca.
* Migração da biblioteca para níveis de ambiente diferentes (de desenvolvimento para armazenamento temporário e produção).

#### Adicionar e criar uma nova biblioteca {#adding-and-building-a-new-library}

1. Na primeira vez que você abre a guia Publicação em Tags do Experience Platform, a lista da biblioteca fica vazia.

   Na coluna da esquerda, selecione **[!UICONTROL Adicionar nova biblioteca]**.

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. Na página Criar nova biblioteca , no **[!UICONTROL Nome]** , insira o nome descritivo da nova biblioteca. Por exemplo,

   *DynamicMediaViewersLib*

   Na lista suspensa Ambiente , escolha o nível Ambiente . Inicialmente, somente o nível de Desenvolvimento está disponível para seleção. Próximo ao lado inferior esquerdo da página, selecione **[!UICONTROL Adicionar todos os recursos alterados]**.

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. Ao lado do canto superior direito da página, selecione **[!UICONTROL Salvar e criar para desenvolvimento]**.

   Em alguns minutos, a biblioteca é criada e pronta para ser usada.

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >Na próxima vez que você alterar a configuração de Tags do Experience Platform, acesse **[!UICONTROL Publicação]** na guia **[!UICONTROL Propriedade]** , em seguida, selecione a biblioteca criada anteriormente.
   >
   >
   >Na tela de publicação da biblioteca, selecione **[!UICONTROL Adicionar todos os recursos alterados]**, em seguida selecione **[!UICONTROL Salvar e criar para desenvolvimento]**.

#### Mover uma biblioteca para cima por meio de níveis de ambiente {#moving-a-library-up-through-environment-levels}

1. Após a adição de uma nova biblioteca, ela é encontrada no ambiente de desenvolvimento. Para movê-lo para o nível de ambiente de preparo (que corresponde à coluna Enviado ), no menu suspenso da biblioteca, selecione **[!UICONTROL Enviar para aprovação]**.

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. Na caixa de diálogo de confirmação, selecione **[!UICONTROL Enviar]**.

   Depois que a biblioteca for movida para a coluna Enviado, no menu suspenso da biblioteca, selecione **[!UICONTROL Criar para armazenamento temporário]**.

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. Para mover a biblioteca do ambiente de preparo para o ambiente de produção (que é a coluna Publicado ), siga um processo semelhante.

   Primeiro, no menu suspenso, selecione **[!UICONTROL Aprovar para publicação]**.

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. No menu suspenso , selecione **[!UICONTROL Criar e publicar na produção]**.

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   Consulte [Publicação](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html) para obter mais informações sobre o processo de publicação em Tags do Experience Platform.

## Configurar o Adobe Experience Manager para integração {#configuring-adobe-experience-manager-for-the-integration}

Pré-requisitos:

* O Experience Manager executa as instâncias Autor e Publicação.
* O nó Experience Manager author é configurado no Dynamic Media - Modo de execução Scene7 (dynamicmedia_s7)
* Os componentes WCM do Dynamic Media são ativados no Experience Manager Sites.

A configuração de Experience Manager consiste nas duas etapas principais a seguir:

* Configuração do Experience Manager IMS.
* Configuração da nuvem de tags do Experience Platform.

### Configurar Experience Manager IMS {#configuring-aem-ims}

1. No autor do Experience Manager, selecione a variável **[!UICONTROL Ferramentas]** ícone (martelo), em seguida, vá para **[!UICONTROL Segurança]** > **[!UICONTROL Configurações do Adobe IMS]**.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. Na página Configuração IMC do Adobe, próximo ao canto superior esquerdo, selecione **[!UICONTROL Criar]**.
1. No **[!UICONTROL Configuração de conta técnica do Adobe IMS]** na página **[!UICONTROL Solução da nuvem]** , selecione **[!UICONTROL Tags de Experience Platform]**.
1. Habilitar **[!UICONTROL Criar novo certificado]**, em seguida, no campo de texto, insira qualquer valor significativo para o certificado. Por exemplo, *AdobeLaunchIMSCert*. Selecionar **[!UICONTROL Criar certificado]**.

   A seguinte mensagem de Informações é exibida:

   *Para recuperar um token de acesso válido, a chave pública do novo certificado é adicionada à conta técnica no Adobe I/O!*

   Para fechar a caixa de diálogo Informações, selecione **[!UICONTROL OK]**.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. Para baixar um arquivo de chave pública (&#42;.crt) no sistema local, selecione **[!UICONTROL Baixar chave pública]**.

   >[!NOTE]
   >
   >Neste ponto, ***deixar aberto*** o **[!UICONTROL Configuração de conta técnica do Adobe IMS]** página; ***não*** feche a página e ***não*** selecione Next. Você retornará a esta página mais tarde nas etapas.

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. Em uma nova guia do navegador, navegue até o [[!DNL Adobe I/O] Console](https://console.adobe.io/integrations).

1. No **[!UICONTROL Integrações do console do Adobe I/O]** , próximo ao canto superior direito, selecione **[!UICONTROL Nova integração]**.
1. No **[!UICONTROL Criar uma nova integração]** , verifique se **[!UICONTROL Acessar uma API]** o botão de opção está selecionado e, em seguida, selecione **[!UICONTROL Continuar]**.

   ![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. No segundo **[!UICONTROL Criar uma nova integração]** , ativar (ativar) a **[!UICONTROL API de Tags do Experience Platform]** botão de opção. No canto inferior direito da página, selecione **[!UICONTROL Continuar]**.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. No terceiro **[!UICONTROL Criar uma nova integração]** faça o seguinte:

   * No **[!UICONTROL Nome]** digite o nome descritivo. Por exemplo, *DynamicMediaViewersIO*.

   * No **[!UICONTROL Descrição]** , insira a descrição da integração.

   * No **[!UICONTROL Certificados de chave pública]** , faça upload do arquivo de chave pública (&#42;.crt) que você baixou anteriormente nessas etapas.

   * Em **[!UICONTROL Selecione uma função para a API de Tags de Experience Platform]** título, selecione **[!UICONTROL Administrador]**.

   * Em **[!UICONTROL Selecione um ou mais perfis de produto para a API de Tags do Experience Platform]** , selecione o perfil de produto chamado **[!UICONTROL Tags - &lt;your_company_name>]**.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. Selecionar **[!UICONTROL Criar integração]**.
1. No **[!UICONTROL Integração criada]** página, selecione **[!UICONTROL Continuar para detalhes de integração]**.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. Uma página de detalhes de Integrações é exibida, **** semelhante ao seguinte:

   >[!NOTE]
   >
   >***Deixe aberta esta página de Detalhes da integração***. Você precisará de várias informações da **[!UICONTROL Visão geral]** e **[!UICONTROL JWT]** em um momento.

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)

   Página de detalhes da integração.

1. Retorne à página **[!UICONTROL Configuração de conta técnica do Adobe IMS]** que você deixou aberta anteriormente. No canto superior direito da página, selecione **[!UICONTROL Próximo]** para abrir o **[!UICONTROL Conta]** na página **[!UICONTROL Configuração de conta técnica do Adobe IMS]** janela.

   (Se você tiver fechado a página anterior, volte para o autor do Experience Manager e navegue para **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Configurações do Adobe IMS]**. Selecione **[!UICONTROL Criar]**. No **[!UICONTROL Solução da nuvem]** , selecione **[!UICONTROL Tags de Experience Platform]**. Na lista suspensa **[!UICONTROL Certificado]**, selecione o nome do certificado criado anteriormente.)

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)

   Configuração de conta técnica do Adobe IMS - página Certificado .

1. O **[!UICONTROL Conta]** tem cinco campos que devem ser preenchidos usando informações da página Detalhes da integração da etapa anterior.

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)

   Configuração de conta técnica do Adobe IMS - página Conta.

1. No **[!UICONTROL Conta]** preencha os seguintes campos:

   * **[!UICONTROL Título]** - Insira um título de conta descritiva.
   * **[!UICONTROL Servidor de autorização]** - Retorne à página Detalhes da integração que você abriu anteriormente. Selecione o **[!UICONTROL JWT]** guia . Copie o nome do servidor, sem o caminho, conforme destacado abaixo.

(o nome do servidor é apenas um exemplo)   Retorne à página **[!UICONTROL Conta]** e cole o nome no respectivo campo.
Por exemplo, `https://ims-na1.adobelogin.com/`
(o nome do servidor é apenas um exemplo)

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)

   Página de detalhes da integração - guia JWT

1. **[!UICONTROL Chave da API]** - Retorne à página de detalhes da integração. Selecione o **[!UICONTROL Visão geral]** , em seguida à direita do **[!UICONTROL Chave da API (ID do cliente)]** , selecione **[!UICONTROL Copiar]**.

   Retorne à página **[!UICONTROL Conta]** e cole a chave no respectivo campo.

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)

   Página de detalhes da integração.

1. **[!UICONTROL Segredo do cliente]** - Retorne à página Detalhes da integração. No **[!UICONTROL Visão geral]** guia , selecione **[!UICONTROL Recuperar Segredo do Cliente]**. À direita do **[!UICONTROL Segredo do cliente]** , selecione **[!UICONTROL Copiar]**.

   Retorne à página **[!UICONTROL Conta]** e cole a chave no respectivo campo.

1. **[!UICONTROL Carga]** - Retorne à página Detalhes da integração . No **[!UICONTROL JWT]** , no campo Carga JWT , copie todo o código do objeto JSON.

   Retorne à página **[!UICONTROL Conta]** e cole o código no respectivo campo.

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)

   Página de detalhes da integração - Guia JWT

   A página Conta, com todos os campos preenchidos, é semelhante ao seguinte:

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. Próximo ao canto superior direito do **[!UICONTROL Conta]** página, selecione **[!UICONTROL Criar]**.

   Com o Experience Manager IMS configurado, agora há um novo IMSAccount listado em **[!UICONTROL Configurações do Adobe IMS]**.

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## Configurar a Experience Platform Tags Cloud para integração {#configuring-adobe-launch-cloud-for-the-integration}

1. No autor do Experience Manager, próximo ao canto superior esquerdo, selecione o **[!UICONTROL Ferramentas]** ícone (martelo), em seguida, vá para **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurações de Tags de Experience Platform]**.

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. No **[!UICONTROL Configurações de Tags de Experience Platform]** no painel esquerdo, selecione um Experience Manager Site para o qual deseja aplicar sua Configuração de tags do Experience Platform.

   Somente para fins de amostra, a variável **`We.Retail`** site é selecionado na captura de tela abaixo.

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. Ao lado do canto superior esquerdo da página, selecione **[!UICONTROL Criar]**.
1. No **[!UICONTROL Geral]** página (1/3 páginas) do **[!UICONTROL Criar configuração de Experience Platform Tags]** , preencha os seguintes campos:

   * **[!UICONTROL Título]** - Insira um título de configuração descritivo. Por exemplo, `We.Retail Tags cloud configuration`.

   * **[!UICONTROL Configuração associada do Adobe IMS]** - Selecione a configuração IMS criada anteriormente em [Configurar Experience Manager IMS](#configuring-aem-ims).

   * **[!UICONTROL Empresa]** - Do **[!UICONTROL Empresa]** selecione sua empresa do Experience Cloud. A lista é preenchida automaticamente.

   * **[!UICONTROL Propriedade]** - Na lista suspensa Propriedade, selecione a propriedade Tags de Experience Platform criada anteriormente. A lista é preenchida automaticamente.
   Depois de completar todos os campos, **[!UICONTROL Geral]** será semelhante ao seguinte:

   ![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. Ao lado do canto superior esquerdo, selecione **[!UICONTROL Próximo]**.
1. No **[!UICONTROL Estágios]** página (2/3 páginas) do **[!UICONTROL Criar configuração de Experience Platform Tags]** , preencha o seguinte campo:

   No **[!UICONTROL URI da biblioteca]** (Identificador de recurso uniforme), verifique o local da versão de preparo da biblioteca de Tags do Experience Platform. Experience Manager preenche este campo automaticamente.

   Por exemplo, apenas para fins de teste, essa etapa usa bibliotecas de Tags de Experience Platform que são implantadas no Adobe CDN.

   >[!NOTE]
   >
   >Verifique se o URI da biblioteca preenchido automaticamente (Uniform Resource Identifier) não está malformado. Se necessário, corrija-o para que o URI represente um URI relativo ao protocolo. Ou seja, começa com uma barra dupla.
   >
   >
   >Por exemplo: `//assets.adobetm.com/launch-xxxx`.

   Seu **[!UICONTROL Estágios]** A página provavelmente aparecerá de forma semelhante ao seguinte. O **[!UICONTROL Arquivar]** e **[!UICONTROL Carregar biblioteca de forma assíncrona]** as opções são ***not*** definido:

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. Próximo ao canto superior direito, selecione **[!UICONTROL Próximo]**.
1. No **[!UICONTROL Produção]** página (3/3 páginas) do **[!UICONTROL Criar configuração de Experience Platform Tags]** , se necessário, corrija o URI de produção preenchido automaticamente de modo semelhante ao que foi feito no **[!UICONTROL Estágios]** página.
1. Próximo ao canto superior direito, selecione **[!UICONTROL Criar]**.

   A nova configuração da nuvem de tags de Experience Platform é criada e listada ao lado do site, como no exemplo a seguir:

1. Selecione a nova Configuração da nuvem de tags de Experience Platform (uma marca de seleção é exibida à esquerda do título da configuração quando selecionada). Na barra de ferramentas, selecione **[!UICONTROL Publicar]**.

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

No momento, o autor do Experience Manager não oferece suporte à integração de visualizadores Dynamic Media com tags Experience Platform.

No entanto, ele é compatível com o nó de publicação do Experience Manager. Usando as configurações padrão da Configuração da nuvem de Experience Platform Tags, o nó de publicação do Experience Manager usa o ambiente de produção de Tags do Experience Platform. Dessa forma, é necessário enviar atualizações da biblioteca de Tags do Experience Platform do Desenvolvimento para o ambiente de Produção sempre durante o teste.

É possível contornar essa limitação. Especifique o URL de desenvolvimento ou armazenamento temporário da biblioteca de Tags de plataforma na configuração da nuvem de Tags do Experience Platform para o nó de publicação do Experience Manager acima. Isso faz com que o nó de publicação do Experience Manager use a versão de Desenvolvimento ou Armazenamento temporário da biblioteca de Tags do Experience Platform.

Consulte [Integre o Experience Manager com Tags de Experience Platform por meio de [!DNL Adobe I/O]](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html?lang=pt-BR) para obter mais informações sobre como configurar a Configuração da nuvem de tags do Experience Platform.
