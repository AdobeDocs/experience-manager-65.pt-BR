---
title: Integração dos visualizadores do Dynamic Media ao Adobe Analytics e ao Adobe Launch
description: A extensão do Dynamic Media Viewers para Adobe Launch, juntamente com o lançamento do Dynamic Media Viewers 5.13, permite que os clientes do Dynamic Media, do Adobe Analytics e do Adobe Launch usem eventos e dados específicos dos Dynamic Media Viewers na configuração do Adobe Launch.
uuid: d218ee1c-cd2c-40c3-a3d4-b95719ae8e98
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: f4051767-182e-4cfd-9dfc-8f516378e0b6
docset: aem65
translation-type: tm+mt
source-git-commit: 8bdb019855edd08ef3d8ef58e627c91a092bc29f
workflow-type: tm+mt
source-wordcount: '6623'
ht-degree: 17%

---


# Integração dos visualizadores do Dynamic Media ao Adobe Analytics e ao Adobe Launch {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## O que é a integração dos visualizadores de mídia dinâmica com o Adobe Analytics e o Adobe Launch? {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

The new *Dynamic Media Viewers* extension for Adobe Launch, along with the recent release of Dynamic Media Viewers 5.13, lets customers of Dynamic Media, Adobe Analytics, and Adobe Launch to use events and data specific for the Dynamic Media Viewers in their Adobe Launch configuration.

Essa integração significa que você pode rastrear o uso de visualizadores de mídia dinâmica em seu site com a Adobe Analytics. Ao mesmo tempo, você pode usar os eventos e os dados expostos pelos visualizadores com qualquer outra extensão do Launch que venha do Adobe ou de terceiros.

Consulte Extensão [do](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/overview.html) Adobe no Guia do usuário do Experience Platform Launch para saber mais sobre extensões.

**Quem deve ler esta documentação:** administradores de site, desenvolvedores na plataforma AEM e aqueles em Operações.

### Limitações da integração {#limitations-of-the-integration}

* A integração Adobe Launch para visualizadores do Dynamic Media não funciona no nó do autor AEM. Não é possível ver nenhum rastreamento de uma página WCM até que ela seja publicada.
* A integração do Adobe Launch para visualizadores do Dynamic Media não é compatível com o modo de operação &quot;pop-up&quot;, onde o URL do visualizador é obtido usando o botão &quot;URL&quot; na página Detalhes do ativo.
* A integração do Adobe Launch não pode ser usada simultaneamente com a integração do Analytics de visualizadores herdados (por meio do `config2=` parâmetro).
* O suporte para rastreamento de vídeo está limitado somente ao rastreamento de reprodução principal, conforme descrito em Visão geral [do](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html)rastreamento. Especificamente, o rastreamento de QoS, Anúncios, Capítulo/Segmentos ou Erros não é suportado.
* A configuração de Duração do armazenamento para Elementos de dados não é compatível com Elementos de dados que usam a extensão Visualizadores *de mídia* dinâmica. A Duração do armazenamento deve ser definida como **[!UICONTROL Nenhum]**.

### Casos de uso para a integração {#use-cases-for-the-integration}

O principal caso de uso para a integração com o Adobe Launch são os clientes que usam o AEM Assets e o AEM Sites. Nesses cenários, você pode configurar uma integração padrão entre o nó do autor AEM e o Adobe Launch e associar a instância Sites à propriedade Adobe Launch. Depois disso, qualquer componente WCM do Dynamic Media adicionado a uma página Sites rastreará os dados e eventos dos visualizadores.

Consulte [Sobre o rastreamento de visualizadores de Mídia dinâmica no AEM Sites](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersinAEMSites).

Um caso de uso secundário suportado pela integração são os clientes que usam somente o AEM Assets ou o Dynamic Media Classic. Nesses casos, você obtém o código incorporado para seu visualizador e o adiciona à página do site. Em seguida, obtenha o URL de produção da biblioteca de inicialização de Adobe do Adobe Launch e adicione-o manualmente ao código da página da Web.

Consulte [Sobre o rastreamento de visualizadores de Mídia dinâmica usando o código](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersusingEmbedcode)incorporado.

## Como o rastreamento de dados e eventos funciona na integração {#how-data-and-event-tracking-works-in-the-integration}

A integração aproveita dois tipos separados e independentes de rastreamento de visualizadores de mídia dinâmica: *Adobe Analytics* e *Adobe Analytics para áudio e vídeo*.

### Sobre o rastreamento usando o Adobe Analytics  {#about-tracking-using-adobe-analytics}

A Adobe Analytics permite que você rastreie ações executadas pelo usuário final quando interagem com Visualizadores de Mídia Dinâmica em seu site. A Adobe Analytics também permite rastrear dados específicos do visualizador. Por exemplo, você pode rastrear e gravar eventos de carregamento de visualização junto com o nome do ativo, quaisquer ações de zoom que ocorreram, ações de reprodução de vídeo e assim por diante.

No Adobe Launch, os conceitos de Elementos *de* dados e *Regras* trabalham juntos para permitir o rastreamento do Adobe Analytics.

#### Sobre elementos de dados na inicialização do Adobe {#about-data-elements-in-adobe-launch}

Um elemento de dados no Adobe Launch é uma propriedade nomeada cujo valor é definido estaticamente ou calculado dinamicamente com base no estado de uma página da Web ou nos dados do Dynamic Media Viewers.

As opções disponíveis para uma definição de Elemento de dados dependem da lista de Extensões instaladas na Propriedade Adobe Launch. A extensão &quot;Core&quot; é pré-instalada e está disponível imediatamente em qualquer configuração. Essa extensão &quot;Core&quot; permite definir um Elemento de dados que o valor vem do cookie, código JavaScript, sequência de query e muitas outras fontes.

Para o Adobe Analytics tracking, é necessário instalar várias extensões adicionais, conforme descrito em [Instalação e configuração de extensões](#installing-and-setup-of-extensions). A extensão Visualizadores de mídia dinâmica adiciona uma capacidade de definir um Elemento de dados cujo valor é um argumento do evento Visualizador dinâmico. Por exemplo, é possível fazer referência ao tipo de visualizador, ou ao nome do ativo reportado pelo visualizador durante a carga, o nível de zoom reportado quando o usuário final aumenta o zoom e muito mais.

A extensão do Visualizador de mídia dinâmica mantém automaticamente os valores de seus Elementos de dados atualizados.

Depois de defini-lo, um Elemento de dados pode ser usado em outros locais da interface do usuário do Adobe Launch, usando o widget do seletor de elementos de dados. Especificamente, os Elementos de dados definidos para fins de rastreamento de Visualizadores de Mídia Dinâmica serão referenciados pela Ação Definir Variáveis da extensão do Adobe Analytics na Regra (consulte abaixo).

Consulte Elementos [de](https://docs.adobe.com/content/help/pt-BR/launch/using/reference/manage-resources/data-elements.html) dados no Guia do usuário do Experience Platform Launch para saber mais.

#### Sobre regras no Adobe Launch {#about-rules-in-adobe-launch}

Uma regra no Adobe Launch é uma configuração agnóstica que define três áreas que compõem uma regra: *Eventos*, *condições* e *ações*:

* *Os eventos* (se) informam Adobe Launch quando disparar uma regra.
* *As condições* (se) indicam ao Adobe Launch quais restrições adicionais serão permitidas ou não quando uma Regra for acionada.
* *As ações* (em seguida) informam ao Adobe Launch o que fazer quando uma Regra é acionada.

As opções disponíveis na seção Eventos, condições e ações dependem das extensões instaladas na Propriedade de inicialização do Adobe. A extensão *Core* é pré-instalada e está disponível prontamente em qualquer configuração. A extensão fornece várias opções para Eventos, como ações básicas em nível de navegador que incluem mudança de foco, pressionamentos de tecla, envios de formulário e assim por diante. Também inclui opções para Condições, como valor de cookie, tipo de navegador e muito mais. Para Ações, somente a opção Código personalizado está disponível.

Para o rastreamento do Adobe Analytics, várias extensões adicionais devem ser instaladas, conforme descrito em [Instalação e configuração de extensões](#installing-and-setup-of-extensions). Especificamente:

* A extensão do visualizador de mídia dinâmica estende a lista de Eventos suportados para eventos específicos do visualizador de mídia dinâmica, como carregamento do visualizador, troca de ativos, aumento de zoom e reprodução de vídeo.
* A extensão do Adobe Analytics estende a lista de Ações suportadas com duas ações necessárias para enviar dados para servidores de rastreamento: *Defina Variáveis* e *Enviar beacon*.

Para rastrear visualizadores de Dynamic Media, é possível usar qualquer tipo de:

* Eventos da extensão, extensão Core ou qualquer outra extensão do Visualizador de Mídia Dinâmica.
* Condições na definição da regra. Ou você pode deixar a área de condições vazia.

Na seção Ações, é necessário que você tenha uma ação *Definir variáveis* . Esta ação informa a Adobe Analytics como preencher variáveis de rastreamento com dados. Ao mesmo tempo, a ação *Definir variáveis* não envia nada para o servidor de rastreamento.

A ação *Definir variáveis* deve ser seguida por uma ação *Enviar beacon* . A ação *Enviar beacon* na verdade envia dados para o servidor de rastreamento do Analytics. Ambas as ações, *Definir variáveis* e *Enviar beacon*, vêm da extensão do Adobe Analytics.

Consulte [Regras](https://docs.adobe.com/content/help/pt-BR/launch/using/reference/manage-resources/rules.html) no Guia do usuário do Experience Platform Launch para saber mais.

#### Exemplo de configuração {#sample-configuration}

A seguinte configuração de exemplo na inicialização de Adobe demonstra como rastrear um nome de ativo na carga do visualizador.

1. Na guia Elementos **[!UICONTROL de]** dados, defina um elemento de dados `AssetName` que faça referência ao `asset` parâmetro do `LOAD` evento da extensão Visualizadores de mídia dinâmica.

   ![image2019-11](assets/image2019-11.png)

1. Na guia **[!UICONTROL Regras]** , defina uma regra *TrackAssetOnLoad*.

   Nessa regra, o campo **[!UICONTROL Evento]** usa o evento **[!UICONTROL LOAD]** da extensão Visualizadores de mídia dinâmica.

   ![image2019-22](assets/image2019-22.png)

1. A configuração Ação tem dois tipos de Ação da extensão Adobe Analytics:

   *Defina Variáveis*, que mapeiam uma variável de análise de sua escolha para o valor do Elemento de `AssetName` dados.

   *Envie o Beacon*, que envia informações de rastreamento para a Adobe Analytics.

   ![image2019-3](assets/image2019-3.png)

1. A configuração de regra resultante é semelhante ao seguinte:

   ![image2019-4](assets/image2019-4.png)

### Sobre o Adobe Analytics para áudio e vídeo {#about-adobe-analytics-for-audio-and-video}

Quando uma conta de Experience Cloud é assinada para usar o Adobe Analytics para áudio e vídeo, é suficiente para ativar o rastreamento de vídeo nas configurações de extensão do *Dynamic Media Viewers* . As métricas de vídeo tornam-se disponíveis no Adobe Analytics. O rastreamento de vídeo depende da presença da extensão Adobe Media Analytics para áudio e vídeo.

Consulte [Instalação e configuração de extensões](#installing-and-setup-of-extensions).

Atualmente, o suporte para rastreamento de vídeo está limitado somente ao rastreamento de &quot;reprodução principal&quot;, conforme descrito em Visão geral [do](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html)rastreamento. Especificamente, o rastreamento de QoS, Anúncios, Capítulo/Segmentos ou Erros não é suportado.

## Uso da extensão Visualizadores de Mídia Dinâmica {#using-the-dynamic-media-viewers-extension}

Conforme mencionado em Casos de [uso para integração](#use%20cases%20for%20the%20integration), é possível rastrear visualizadores de Dynamic Media com a nova integração de inicialização de Adobe no AEM Sites e usando o código incorporado.

### Rastreamento de visualizadores de Dynamic Media no AEM Sites {#tracking-dynamic-media-viewers-in-aem-sites}

Para rastrear visualizadores do Dynamic Media no AEM Sites, todas as etapas listadas na seção [Configuração de todas as partes](#configuring-all-the-integration-pieces) da integração devem ser executadas. Especificamente, você deve criar a configuração IMS e a configuração da Adobe Launch Cloud.

Após a configuração correta, qualquer visualizador de Dynamic Media que você adiciona a uma página Sites, usando um componente WCM suportado pelo Dynamic Media, rastreia automaticamente os dados para Adobe Analytics, Adobe Analytics para Vídeo, ou ambos.

<!-- To be reviewed and updated:
See [Adding Dynamic Media Assets to Pages using Adobe Sites](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html).
-->

### Rastreamento de visualizadores de Dynamic Media usando código incorporado {#tracking-dynamic-media-viewers-using-embed-code}

Os clientes que não usam o AEM Sites ou incorporam visualizadores do Dynamic Media em páginas da Web fora do AEM Sites, ou ambos, ainda podem usar a integração Adobe Launch.

Conclua as etapas de configuração nas seções [Configuração do Adobe Analytics](#configuringadobeanalytics) e [Configuração do Adobe Launch](#configuringadobelaunch). No entanto, as etapas de configuração relacionadas ao AEM não são necessárias.

Após a configuração correta, você pode adicionar o suporte ao Adobe Launch a uma página da Web com um visualizador de Dynamic Media.

Consulte [Adicionar o código](https://docs.adobe.com/content/help/en/launch/using/implement/configure/implement-the-launch-install-code.html) Incorporado para saber mais sobre como usar o código incorporado da biblioteca de inicialização de Adobe.

<!-- To be reviewed and updated:
See [Embedding the Video or Image Viewer on a Web Page](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html) to learn more about how to use the embed code feature of AEM Dynamic Media.
-->

**Para rastrear visualizadores de Dynamic Media usando o código** incorporado:

1. Tenha uma página da Web pronta para incorporar um visualizador de Dynamic Media.
1. Obtenha o código incorporado para a biblioteca Adobe Launch fazendo logon primeiro no Adobe Launch (consulte [Configuração do Adobe Launch](#configuringadobelaunch)).
1. Clique em **[!UICONTROL Propriedade]** e, em seguida, clique na guia **[!UICONTROL Ambientes]** .
1. Escolha o nível de Ambiente relevante para o ambiente da página da Web. Em seguida, na coluna **[!UICONTROL Instalar]** , clique no ícone da caixa.
1. **[!UICONTROL Na caixa de diálogo Instruções]** de instalação na Web, copie o código incorporado da biblioteca de inicialização de Adobe, juntamente com as `<script/>` tags adjacentes.

## Guia de referência para a extensão do visualizador de mídia dinâmica {#reference-guide-for-the-dynamic-media-viewers-extension}

### Sobre a configuração do Visualizador de mídia dinâmica {#about-the-dynamic-media-viewers-configuration}

A extensão do Visualizador de mídia dinâmica é integrada automaticamente à biblioteca de inicialização do Adobe se todas as condições abaixo forem verdadeiras:

* O objeto global da biblioteca de inicialização de Adobe ( `_satellite`) está presente na página.
* A função de extensão Visualizadores de Mídia Dinâmica `_dmviewers_v001()` é definida em `_satellite`.

* `config2=` o parâmetro do visualizador não foi especificado, o que significa que o visualizador não usa a integração herdada do Analytics.

Além disso, há uma opção para desativar explicitamente a integração do Adobe Launch no visualizador especificando o `launch=0` parâmetro na configuração do visualizador. O valor padrão desse parâmetro é `1`.

### Configuração da extensão do visualizador de mídia dinâmica {#configuring-the-dynamic-media-viewers-extension}

A única opção de configuração para a extensão Visualizadores de Mídia Dinâmica é **[!UICONTROL Ativar o Adobe Media Analytics para áudio e vídeo]**.

Ao marcar (ativar ou &quot;ativar&quot;) essa opção e se a extensão do Adobe Media Analytics para áudio e vídeo estiver instalada e configurada corretamente, as métricas de reprodução de vídeo serão enviadas para a solução de Áudio e Vídeo da Adobe Analytics. Desativar esta opção desativa o rastreamento de vídeo.

Observe que se você ativar essa opção *sem* ter a extensão Adobe Media Analytics para áudio e vídeo instalada, a opção não terá efeito.

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### Sobre elementos de dados na extensão Visualizadores de mídia dinâmica {#about-data-elements-in-the-dynamic-media-viewers-extension}

O único tipo de Elemento de dados fornecido pela extensão Visualizadores do Dynamic Media é o **[!UICONTROL Evento do visualizador]** na lista suspensa **[!UICONTROL Tipo de elemento de dados]**.

Quando selecionado, o editor de Elementos de dados renderiza um formulário com dois campos:

* **[!UICONTROL Tipo de dados do evento de visualizadores do DM]** - uma lista suspensa que identifica todos os eventos do visualizador compatíveis com a extensão do Visualizador do Dynamic Media que têm argumentos, além de um item **[!UICONTROL COMMON]** especial. Um item **[!UICONTROL COMUM]** representa uma lista de parâmetros de evento comuns a todos os tipos de eventos enviados pelos visualizadores.
* **[!UICONTROL Parâmetro]** de rastreamento - um argumento do evento visualizador do Dynamic Media selecionado.

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

Consulte o guia [de referência Visualizadores de mídia](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html) dinâmica para obter a lista de eventos suportados por cada tipo de visualizador; vá para a seção específica do visualizador e clique em Suporte para a subseção de rastreamento do Adobe Analytics. Atualmente, o guia de referência Visualizadores de mídia dinâmica não documento argumentos de evento.

Vamos agora considerar o ciclo de vida do elemento de *dados* do visualizador de mídia dinâmica. O valor desse Elemento de dados é preenchido depois que o evento do visualizador do Dynamic Media correspondente ocorre na página. Por exemplo, se o Elemento de dados apontar para o evento **[!UICONTROL LOAD]** e seu argumento &quot;asset&quot;, o valor desse Elemento de dados receberá dados válidos depois que o visualizador executar o evento LOAD pela primeira vez. Se o Elemento de dados apontar para o evento **[!UICONTROL ZOOM]** e seu argumento de &quot;escala&quot;, o valor desse Elemento de dados permanecerá vazio até que o visualizador envie um evento **[!UICONTROL ZOOM]** pela primeira vez.

Da mesma forma, os valores dos Elementos de dados são atualizados automaticamente quando o visualizador envia um evento correspondente na página. A atualização de valor acontece mesmo se o evento específico não for definido na configuração Regra. Por exemplo, se **[!UICONTROL ZoomScale]** do elemento de dados for definido como o parâmetro &quot;scale&quot; do evento ZOOM, mas a única regra presente na configuração Regra for acionada pelo evento **[!UICONTROL LOAD]**, o valor de **[!UICONTROL ZoomScale]** ainda será atualizado sempre que um usuário executar o Zoom dentro do visualizador.

Qualquer visualizador do Dynamic Media tem um identificador exclusivo na página da Web. O Elemento de dados rastreia o próprio valor e o visualizador o preencheu. Isso significa que, se houver vários visualizadores na mesma página e houver um Elemento de dados **[!UICONTROL AssetName]** que aponte para o evento **[!UICONTROL LOAD]** e seu argumento &quot;asset&quot;, o Elemento de dados **[!UICONTROL AssetName]** manterá uma coleção de nomes de ativos associados a cada visualizador carregado na página.

O valor exato retornado pelo Elemento de dados depende do contexto. Se o Elemento de dados for solicitado em uma Regra que foi acionada por um evento do visualizador de Mídia dinâmica, o valor do Elemento de dados será retornado para o visualizador que iniciou a Regra. E, se o Elemento de dados for solicitado em uma Regra que foi acionada por um Evento de outra extensão de inicialização de Adobe, o valor do Elemento de dados será o valor do visualizador que foi o último a atualizar esse Elemento de dados.

**Considere a seguinte configuração** de amostra:

* Uma página da Web com dois visualizadores de zoom do Dynamic Media; nós os referenciaremos como *viewer1* e *viewer2*.

* **[!UICONTROL O elemento de dados ZoomScale]** aponta para o evento **[!UICONTROL ZOOM]** e seu argumento &quot;scale&quot;.
* **[!UICONTROL Regra TrackPan]** com o seguinte:

   * Usa o evento **[!UICONTROL PAN]** do visualizador de mídia dinâmica como disparador.
   * Envia o valor do Elemento de dados **[!UICONTROL ZoomScale]** para a Adobe Analytics.

* 
   * **[!UICONTROL Regra TrackKey]** com o seguinte:

   * Usa o evento key press da extensão Core Adobe Launch como disparador.
   * Envia o valor do Elemento de dados **[!UICONTROL ZoomScale]** para a Adobe Analytics.

Agora, suponha que o usuário final carregue a página da Web com os dois visualizadores. No *visualizador1*, eles aumentam o zoom para 50% de escala; em seguida, no *visualizador2*, eles aumentam o zoom para 25%. No *visualizador1*, eles deslocam a imagem e, por fim, pressionam uma tecla no teclado.

A atividade do usuário final resulta nas duas chamadas de rastreamento a seguir feitas para a Adobe Analytics:

* A primeira chamada ocorre porque a Regra **[!UICONTROL TrackPan]** é acionada quando o usuário entra em *exibição1*. Essa chamada envia 50% como um valor do Elemento de Dados **[!UICONTROL ZoomScale]** , pois o Elemento de Dados saberá que a Regra é acionada pelo *visualizador1* e busca o valor de escala correspondente;
* A segunda chamada ocorre porque a Regra **[!UICONTROL TrackKey]** é acionada quando o usuário pressiona uma tecla no teclado. Essa chamada envia 25% como um valor do Elemento de dados **[!UICONTROL ZoomScale]** porque a Regra não foi acionada pelo visualizador. Dessa forma, o Elemento de dados retorna o valor mais atualizado.

A amostra configurada acima também afeta a duração do valor do Elemento de dados. O valor do Elemento de dados gerenciado pelo Visualizador de mídia dinâmica é armazenado no código da biblioteca de inicialização de Adobe, mesmo depois que o próprio visualizador é descartado na página da Web. Isso significa que, se houver uma Regra acionada por uma extensão que não seja o Visualizador de mídia dinâmica e fizer referência a esse Elemento de dados, o Elemento de dados retornará o último valor conhecido, mesmo que o visualizador não esteja mais presente na página da Web.

Em qualquer caso, os valores dos elementos de dados controlados pelos visualizadores de mídia dinâmica não são armazenados no armazenamento local ou no servidor; em vez disso, eles são mantidos somente na biblioteca de inicialização de Adobe do cliente. Os valores desse Elemento de dados desaparecem quando a página da Web é recarregada.

Geralmente, o editor de Elementos de dados oferece suporte à seleção [da duração do](https://docs.adobe.com/content/help/pt-BR/launch/using/reference/manage-resources/data-elements.html#create-a-data-element)armazenamento. No entanto, os Elementos de dados que usam a extensão Visualizadores de mídia dinâmica só suportam a opção de duração do armazenamento de **[!UICONTROL Nenhum]**. A definição de qualquer outro valor é possível na interface do usuário, mas o comportamento do Elemento de dados não é definido nesse caso. A extensão gerencia o valor do Elemento de dados sozinho: o elemento de dados que mantém o valor do argumento do evento do visualizador durante todo o ciclo de vida do visualizador.

### Sobre regras na extensão Visualizadores de Mídia Dinâmica {#about-rules-in-the-dynamic-media-viewers-extension}

No Editor de regras, a extensão adiciona novas opções de configuração para o editor de Eventos. Além disso, o oferece uma opção para fazer referência manual aos parâmetros do evento no editor de Ação como uma opção de mão curta, em vez de usar elementos de dados pré-configurados.

#### Sobre o editor de Eventos {#about-the-events-editor}

No Editor de eventos, a extensão Visualizadores do Dynamic Media adiciona um novo **[!UICONTROL Tipo de evento]** chamado **[!UICONTROL Evento do visualizador]**.

Quando selecionado, o editor de Eventos renderiza os eventos **[!UICONTROL suspensos do]** Dynamic Media Viewer, listando todos os eventos disponíveis que são suportados pelos visualizadores do Dynamic Media.

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### Sobre o editor de Ações {#about-the-actions-editor}

A extensão Visualizadores de Mídia Dinâmica permite usar parâmetros de evento dos visualizadores de Mídia Dinâmica para mapear para variáveis de análise no editor Definir variáveis da extensão Adobe Analytics.

O método mais simples para fazer isso é concluir o seguinte processo de duas etapas:

* Primeiro, defina um ou mais Elementos de dados, onde cada Elemento de dados representa um parâmetro de um evento do Visualizador de mídia dinâmica.
* Finalmente, no editor Definir variáveis da extensão do Adobe Analytics, clique no ícone do seletor de elementos de dados (três discos empilhados) para abrir a caixa de diálogo Selecionar elemento de dados e selecione um elemento de dados a partir dele.

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

No entanto, é possível usar uma abordagem alternativa e ignorar a criação do Elemento de dados. Faça referência direta a um argumento de um evento do Visualizador do Dynamic Media ao digitar o nome totalmente qualificado do argumento de evento no campo de entrada **[!UICONTROL valor]** da atribuição de variável do Analytics, com sinais de porcentagem (%) de ambos os lados. Por exemplo,

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

Observe que há uma diferença importante entre o uso de Elementos de dados e a referência do argumento de evento direto. Para Elemento de dados, não importa qual evento aciona a ação Definir variáveis, o evento que aciona a regra pode não estar relacionado ao Visualizador dinâmico (como um clique do mouse na página da Web da extensão Principal). Mas, ao usar uma referência de argumento direto, é importante garantir que o evento que aciona a regra corresponda ao argumento do evento que ela menciona.

Por exemplo, a referência `%event.detail.dm.LOAD.asset%` retornará o nome correto do ativo se Regra for acionado pelo evento **[!UICONTROL LOAD]** da extensão do Visualizador do Dynamic Media. No entanto, retorna um valor vazio para qualquer outro evento.

A tabela a seguir lista eventos do Visualizador de Mídia Dinâmica do e seus argumentos suportados:

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

## Configuração de todas as peças de integração {#configuring-all-the-integration-pieces}

**ANTES DE COMEÇAR**

Caso ainda não o tenha feito, o Adobe recomenda que você analise toda a documentação antes desta seção para entender a integração completa.

Esta seção explica as etapas de configuração necessárias para integrar os visualizadores de Dynamic Media ao Adobe Analytics e ao Adobe Analytics para áudio e vídeo. Embora o uso da extensão Visualizadores de Mídia Dinâmica para outros fins no Adobe Launch seja possível, esses cenários não são abordados nesta documentação.

Você configurará a integração nos seguintes produtos de Adobe:

* Adobe Analytics - você configurará as variáveis de rastreamento e os relatórios.
* Adobe Launch - você definirá uma Propriedade, uma ou mais Regras e um ou mais Elementos de dados para ativar o rastreamento do visualizador.

Além disso, se essa solução de integração for usada com a AEM Sites, a seguinte configuração também precisará ser feita:

* Console de E/S do Adobe - a integração é criada para o Adobe Launch.
* AEM nó do autor - configuração IMS e configuração da nuvem Adobe Launch.

Como parte da configuração, verifique se você tem acesso a uma empresa no Adobe Experience Cloud que já tenha o Adobe Analytics e o Adobe Launch habilitados.

## Configuração da Adobe Analytics para integração {#configuring-adobe-analytics-for-the-integration}

Depois de configurar o Adobe Analytics, o seguinte será configurado para a integração:

* Um Conjunto de relatórios está no lugar e selecionado.
* As Variáveis do Analytics estão disponíveis para receber dados de rastreamento.
* Os relatórios estão disponíveis para visualização de dados coletados dentro do Adobe Analytics.

Consulte também Guia [de implementação do](https://docs.adobe.com/content/help/en/analytics/implementation/home.html)Analytics.

**Para configurar o Adobe Analytics para integração**:

1. Start acessando o Adobe Analytics a partir do [home page](https://exc-home.experiencecloud.adobe.com/exc-home/home.html#/)Experience Cloud. Na barra de menus, clique no ícone Soluções (uma tabela de três por três pontos) próximo ao canto superior direito da página e, em seguida, clique em **[!UICONTROL Analytics]**.

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   Agora você selecionará um conjunto de relatórios.

### Selecionar um conjunto de relatórios {#selecting-a-report-suite}

1. Próximo ao canto superior direito da página do Adobe Analytics, à direita do campo **[!UICONTROL Pesquisar relatórios]**, selecione o conjunto de relatórios correto na lista suspensa. Se houver vários conjuntos de relatórios disponíveis e você não tiver certeza de qual usar, entre em contato com o administrador do Adobe Analytics, que pode ajudá-lo a selecionar qual usar.

   Na ilustração abaixo, um usuário criou um conjunto de relatórios chamado *DynamicMediaViewersExtensionDoc* e o selecionou na lista suspensa. O nome do conjunto de relatórios é apenas para fins ilustrativos; o nome do conjunto de relatórios selecionado será diferente.

   Se nenhum conjunto de relatórios estiver disponível, você ou o administrador da Adobe Analytics devem criar um antes de prosseguir com a configuração.

   Consulte [Relatórios e conjuntos](https://docs.adobe.com/content/help/en/analytics/admin/manage-report-suites/report-suites-admin.html) de relatórios e [Criar um conjunto](https://docs.adobe.com/content/help/en/analytics/admin/admin-console/create-report-suite.html)de relatórios.

   No Adobe Analytics, os conjuntos de relatórios são gerenciados em **[!UICONTROL Admin > Conjuntos]** de relatórios.

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   Agora, você configurará as variáveis do Adobe Analytics.

### Configuração de variáveis do Adobe Analytics {#setting-up-adobe-analytics-variables}

1. Agora, você designará uma ou mais variáveis do Adobe Analytics que deseja usar para rastrear o comportamento dos Visualizadores de mídia dinâmica na página da Web.

   É possível usar qualquer tipo de variável suportada pela Adobe Analytics. A decisão sobre o tipo de variável (como [props]de Tráfego personalizado, [eVar]de conversão) deve ser orientada por necessidades específicas da implementação do Analytics.

   Consulte [Visão geral de props e eVars](https://docs.adobe.com/content/help/en/analytics/implementation/vars/page-vars/evar.html).

   Para os fins desta documentação, somente uma variável de Tráfego personalizado (props) será usada porque eles se tornam disponíveis em um Relatório do Analytics em poucos minutos após uma ação ocorrer em uma página da Web.

   Para ativar uma nova variável de Tráfego personalizado, no Adobe Analytics, na barra de ferramentas, clique em **[!UICONTROL Admin > Report Suites]**.

1. Na página **[!UICONTROL Gerenciador do conjunto de relatórios]**, selecione o relatório correto e, na barra de ferramentas, clique em **[!UICONTROL Editar configurações > Tráfego > Variáveis de tráfego]**.
1. Ali, selecione a variável não utilizada, dê a ela um nome descritivo ( ativo **[!UICONTROL do visualizador (prop 30)]**) e altere a caixa de combinação para &quot;Ativado&quot; na coluna Ativado.

   A captura de tela a seguir é um exemplo de uma variável de Tráfego personalizado ( **[!UICONTROL prop30]**) para rastrear um nome de ativo usado pelo visualizador:

   ![image2019-6-26_23-6-59](assets/image2019-6-26_23-6-59.png)

1. Na parte inferior da lista de variáveis, clique em **[!UICONTROL Salvar]**.

### Configuração de um relatório {#setting-up-a-report}

1. Geralmente, a configuração de um Relatório no Adobe Analytics é orientada por necessidades específicas do projeto. Dessa forma, a configuração detalhada do relatório está além do escopo dessa integração.

   No entanto, basta saber que os relatórios de Tráfego personalizado ficam automaticamente disponíveis no Adobe Analytics depois que você configura as variáveis de Tráfego personalizado na **[configuração das variáveis](#setting-up-adobe-analytics-variables)**do Adobe Analytics.

   Por exemplo, o relatório da variável **[!UICONTROL Ativo do visualizador (prop 30)]** está disponível no menu Relatórios, em **[!UICONTROL Tráfego personalizado > Tráfego personalizado 21-30 > Ativo do visualizador (prop 30)]**.

   Visitar este relatório logo após a criação do **[!UICONTROL Ativo do visualizador (prop 30)]**, não mostra dados; o que é esperado neste momento da integração.

   ![image2019-6-26_23-12-49](assets/image2019-6-26_23-12-49.png)

## Configuração do Adobe Launch para integração {#configuring-adobe-launch-for-the-integration}

Depois de configurar o Adobe Launch, o seguinte será configurado para a integração:

* A criação de uma nova propriedade para manter todas as configurações juntas.
* A instalação e configuração de extensões. O código do cliente de todas as extensões instaladas na Propriedade é compilado em conjunto em uma biblioteca. Esta biblioteca é usada pela página da Web mais tarde.
* Configuração de elementos de dados e regras. Essa configuração define quais dados devem ser capturados nos visualizadores de Dynamic Media, quando disparar a lógica de rastreamento e onde enviar os dados do visualizador no Adobe Analytics.
* Publicação da biblioteca.

**Para configurar o Adobe Launch para integração**:

1. Start acessando Adobe Launch a partir do [home page](https://exc-home.experiencecloud.adobe.com/exc-home/home.html#/). Na barra de menus, clique no ícone Soluções (três por três tabelas de pontos) próximo ao canto superior direito da página e clique em **[!UICONTROL Iniciar]**.

   Você também pode [abrir o Adobe Launch diretamente](https://launch.adobe.com/).

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### Criação de uma propriedade no Adobe Launch {#creating-a-property-in-adobe-launch}

Uma propriedade no Adobe Launch é uma configuração nomeada que mantém todas as configurações juntas. Uma biblioteca das configurações é gerada e publicada em diferentes níveis de ambiente (desenvolvimento, armazenamento temporário e produção).

Consulte também [Criar uma propriedade](https://docs.adobe.com/content/help/en/launch/using/implement/configure/create-a-property.html).

1. Em Adobe Launch (Inicialização), clique em **[!UICONTROL New Property (Nova propriedade]**).
1. Na caixa de diálogo **[!UICONTROL Criar propriedade]**, no campo **[!UICONTROL Nome]**, digite um nome descritivo, como o título do site. Por exemplo, `DynamicMediaViewersProp.`
1. No campo **[!UICONTROL Domínios]** , insira o domínio do site.
1. In the **[!UICONTROL Advanced Options]** drop-down, enable **[!UICONTROL Configure for extension development (cannot be modified later)]** in case the extension you want to use--in this case, *Dynamic Media Viewers*--is not yet released.

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. Clique em **[!UICONTROL Salvar]**.

   Clique na propriedade recém-criada e prossiga para *Instalação e configuração de extensões*.

### Instalação e configuração de extensões {#installing-and-setup-of-extensions}

Todas as extensões disponíveis no Adobe Launch são listadas em **[!UICONTROL Extensões > Catálogo]**.

Para instalar uma extensão, clique em **[!UICONTROL Instalar]**. Se necessário, execute uma configuração de extensão única e clique em **[!UICONTROL Salvar]**.

Quando necessário, as seguintes extensões devem ser instaladas e configuradas:

* (Obrigatório) *Extensão *Serviço de ID de Experience Cloud

Nenhuma configuração adicional é necessária, aceitar para quaisquer valores propostos. Quando terminar, certifique-se de clicar em **[!UICONTROL Salvar]**.

Consulte Extensão [do serviço de ID de](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)Experience Cloud.

* (Obrigatório) Extensão *Adobe Analytics*

Para configurar essa extensão, primeiro será necessário a ID do conjunto de relatórios encontrada no Adobe Analytics, em **[!UICONTROL Admin > Conjunto de relatórios]**, no cabeçalho da coluna **[!UICONTROL ID do conjunto de relatórios]**.

(Para fins de demonstração, a ID de Conjunto de relatórios do Conjunto de relatórios **[!UICONTROL DynamicMediaViewersExtensionDoc]** será usada nas seguintes capturas de tela. Esta ID foi criada e usada em [Selecionar um conjunto de relatórios](#selecting-a-report-suite) anteriormente.)

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

Na página Instalar extensão, digite a ID do conjunto de relatórios no campo **[!UICONTROL Conjuntos de relatórios]**, no campo **[!UICONTROL Conjuntos de relatórios de preparo]** e no campo **[!UICONTROL Conjuntos de relatórios de produção]**.

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*Configure o seguinte item somente se você planeja usar o rastreamento de vídeo:*

Na página **[!UICONTROL Instalar extensão]** , expanda **[!UICONTROL Geral]** e especifique o Servidor de rastreamento. O Servidor de rastreamento segue o modelo `<trackingNamespace>.sc.omtrdc.net`, onde `<trackingNamespace>` estão as informações obtidas no email de provisionamento.

Clique em **[!UICONTROL Salvar]**.

Consulte [Adobe Analytics Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html).

* (Opcional; necessário somente se o rastreamento de vídeo for necessário) *Adobe Media Analytics para extensão de áudio e vídeo*

Preencha o campo do servidor de rastreamento. O servidor de rastreamento do *Adobe Media Analytics para extensão de Áudio e Vídeo* é diferente do servidor de rastreamento usado para Adobe Analytics. Ele segue o modelo `<trackingNamespace>.hb.omtrdc.net`, onde `<trackingNamespace>` estão as informações do email de provisionamento.

Todos os outros campos são opcionais.

Consulte Análise de mídia do [Adobe para obter informações sobre a extensão](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)de áudio e vídeo.

* (Obrigatório) Extensão de visualizadores ** de mídia dinâmica

Selecione **[!UICONTROL ativar o Adobe Analytics para Vídeo]** para habilitar (ativar) o rastreamento do Video Heartbeat.

Observe que, no momento desta gravação, a extensão do *Dynamic Media Viewers* só estará disponível se a propriedade Adobe Launch for criada para desenvolvimento.

Consulte [Criação de uma propriedade em Adobe Launch](#creating-a-property-in-adobe-launch).

Depois que as extensões forem instaladas e configuradas, no mínimo, as cinco extensões a seguir (quatro se você não estiver acompanhando o vídeo) serão listadas na área Extensões > Instaladas.

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### Configuração de elementos de dados e regras {#setting-up-data-elements-and-rules}

No Adobe Launch, crie Elementos de dados e regras que sejam necessários para rastrear visualizadores de Mídia dinâmica.

Consulte [Como o rastreamento de dados e eventos funciona na integração](#how-data-and-event-tracking-works-in-the-integration) para obter uma visão geral do rastreamento com o Adobe Launch.

Consulte Configuração [de](#sample-configuration) amostra para obter uma configuração de amostra no Adobe Launch que demonstra como rastrear um nome de ativo na carga do visualizador.

Consulte [Configuração da extensão](#configuring-the-dynamic-media-viewers-extension) do visualizador de mídia dinâmica para obter informações detalhadas sobre os recursos da extensão.

### Publicar uma biblioteca {#publishing-a-library}

Para fazer alterações na configuração de Adobe Launch (incluindo Propriedade, Extensões, Regras e Elementos de dados configurados), é necessário *publicar* essas alterações*.* A publicação no Adobe Launch é realizada a partir da guia Publicação na configuração Propriedade.

O Adobe Launch pode ter vários ambientes de desenvolvimento, um ambiente de preparo e um ambiente de produção. Por padrão, a Configuração da Adobe Launch Cloud no AEM aponta o nó do autor AEM para o ambiente Stage do Adobe Launch e o nó de publicação AEM para o ambiente Production do Adobe Launch. Essa disposição significa que, com as configurações de AEM padrão, é necessário publicar a biblioteca de inicialização de Adobe para o ambiente de preparo, a fim de usá-la AEM autor e publicá-la no ambiente Produção, para que possa ser usada em AEM publicação.

Consulte [Ambientes](https://docs.adobe.com/content/help/en/launch/using/reference/publish/environments.html) para obter mais informações sobre ambientes de inicialização de Adobe.

A publicação de uma biblioteca envolve as duas etapas a seguir:

* Adicionar e criar uma nova biblioteca incluindo todas as alterações necessárias (novas e atualizações) na biblioteca.
* Movimentação da biblioteca pelos diferentes níveis de ambiente (de Desenvolvimento a Preparação e Produção)

#### Adicionar e criar uma nova biblioteca {#adding-and-building-a-new-library}

1. Na primeira vez que você abrir a guia Publicação no Adobe Launch, a lista da biblioteca estará vazia.

   Na coluna esquerda, clique em **[!UICONTROL Adicionar nova biblioteca]**.

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. Na página Criar nova biblioteca, no campo **[!UICONTROL Nome]** , digite o nome descritivo da nova biblioteca. Por exemplo,

   *DynamicMediaViewersLib*

   Na lista suspensa Ambiente, escolha o nível do Ambiente. Inicialmente, apenas o Nível de desenvolvimento está disponível para seleção. Ao lado esquerdo inferior da página, clique em **[!UICONTROL Adicionar todos os recursos]** alterados.

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. Near the upper-right corner of the page, click **[!UICONTROL Save &amp; Build for Development]**.

   Em poucos minutos a biblioteca é criada e pronta para ser usada.

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >Na próxima vez que fizer alterações na configuração do Adobe Launch, acesse a guia **[!UICONTROL Publicação]** na configuração **[!UICONTROL Propriedade]** e clique na biblioteca criada anteriormente.
   >
   >
   >Na tela de publicação da biblioteca, clique em **[!UICONTROL Adicionar todos os recursos]** alterados e, em seguida, clique em **[!UICONTROL Salvar e construir para desenvolvimento]**.

#### Mover uma biblioteca para cima em níveis de ambiente {#moving-a-library-up-through-environment-levels}

1. Depois que uma nova biblioteca é adicionada, ela está localizada inicialmente no ambiente de desenvolvimento. Para movê-lo para o nível do ambiente de preparo (que corresponde à coluna Enviado), no menu suspenso da biblioteca, clique em **[!UICONTROL Enviar para aprovação]**.

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. Na caixa de diálogo de confirmação, clique em **[!UICONTROL Enviar]**.

   Depois que a biblioteca for movida para a coluna Enviado, no menu suspenso da biblioteca, clique em **[!UICONTROL Criar para armazenamento temporário]**.

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. Siga um processo semelhante para mover a biblioteca do ambiente de armazenamento temporário para o ambiente de produção (que é a coluna Publicado).

   Primeiro, no menu suspenso, clique em **[!UICONTROL Aprovar para publicação]**.

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. No menu suspenso, clique em **[!UICONTROL Criar e publicar na produção]**.

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   Consulte [Publicação](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html) para obter mais informações sobre o processo de publicação no Adobe Launch.

## Configuração da Adobe Experience Manager para integração {#configuring-adobe-experience-manager-for-the-integration}

Pré-requisitos:

* AEM executa as instâncias Autor e Publicar.
* AEM nó do autor está configurado no Dynamic Media - modo de execução Scene7 (dynamicmedia_s7)
* Os componentes do Dynamic Media WCM estão habilitados no AEM Sites.

A configuração AEM consiste nas duas etapas principais a seguir:

* Configuração do AEM IMS.
* Configuração da Adobe Launch Cloud.

### Configuração AEM IMS {#configuring-aem-ims}

1. AEM autor, clique no ícone Ferramentas (martelo) e, em seguida, clique em **[!UICONTROL Segurança > Configurações]** do Adobe IMS.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. Na página Configuração IMC Adobe, perto do canto superior esquerdo, clique em **[!UICONTROL Criar]**.
1. Na página **[!UICONTROL Configuração de conta técnica do Adobe IMS]**, na lista suspensa **[!UICONTROL Solução da nuvem]**, clique em **[!UICONTROL Adobe Launch]**.
1. Ative **[!UICONTROL Criar novo certificado]** e, no campo de texto, digite qualquer valor significativo para o seu certificado. Por exemplo, *AdobeLaunchIMSCert*. Clique em **[!UICONTROL Criar certificado]**.

   A seguinte mensagem de informações é exibida:

   *Para recuperar um token de acesso válido, a chave pública do novo certificado deve ser adicionada à conta técnica no Adobe I/O!*.

   Click **[!UICONTROL OK]** to dismiss the Info dialog box.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. Clique em **[!UICONTROL Baixar chave]** pública para baixar um arquivo de chave pública (*.crt) no seu sistema local.

   >[!NOTE]
   >
   >Nesse momento, ***deixe aberta*** a página **[!UICONTROL Configuração da conta técnica do Adobe IMS]**; ***não*** feche a página e ***não*** clique em Avançar. Você retornará posteriormente a esta página nas etapas.

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. Em uma nova guia do navegador, navegue até o Console [de E/S do](https://console.adobe.io/integrations)Adobe.

1. Na página Integrações **[!UICONTROL do console de E/S do]** Adobe, perto do canto superior direito, clique em **[!UICONTROL Nova integração]**.
1. Na caixa de diálogo **[!UICONTROL Criar uma nova integração]**, verifique se o botão de opção **[!UICONTROL Acessar uma API]** está selecionado e clique em **[!UICONTROL Continuar]**.

   ![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. Na segunda página **[!UICONTROL Criar uma nova integração]**, habilite (ative) o botão de opção **[!UICONTROL API do Experience Platform Launch]**. No canto inferior direito da página, clique em **[!UICONTROL Continuar]**.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. Na terceira página **[!UICONTROL Criar uma nova integração]** , faça o seguinte:

   * No campo **[!UICONTROL Nome]** , insira o nome descritivo. Por exemplo, *DynamicMediaViewersIO*.

   * No campo **[!UICONTROL Descrição]** , insira a descrição para a integração.

   * Na área Certificados **[!UICONTROL de chave]** pública, carregue o arquivo de chave pública (*.crt) que você baixou anteriormente nessas etapas.

   * Under the **[!UICONTROL Select a role for Experience Platform Launch API]** heading, select **[!UICONTROL Admin]**.

   * Em **[!UICONTROL Selecionar um ou mais perfis de produto para a API]** Experience Platform Launch, selecione o perfil de produto chamado **[!UICONTROL Iniciar - &lt;nome_empresa_do_produto>]**.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. Click **[!UICONTROL Create integration]**.
1. Na página **[!UICONTROL Integração criada]** , clique em **[!UICONTROL Continuar para obter os detalhes]** da integração.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. Uma página de detalhes de Integrações é exibida, de **** modo semelhante ao seguinte:

   >[!NOTE]
   >
   >***Deixe aberta esta página de Detalhes da integração***. Você logo precisará de várias informações nas guias **[!UICONTROL Visão geral]** e **[!UICONTROL JWT]**.

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)

   Página de detalhes da integração.

1. Retorne à página **[!UICONTROL Configuração de conta técnica do Adobe IMS]** que você deixou aberta anteriormente. No canto superior direito da página, clique em **[!UICONTROL Avançar]** para abrir a página **[!UICONTROL Conta]** na janela **[!UICONTROL Configuração de conta técnica do Adobe IMS]**.

   (Se você tiver fechado a página anterior acidentalmente, volte para o autor do AEM e clique em **[!UICONTROL Ferramentas > Segurança > Configurações do Adobe IMS]**. Clique em **[!UICONTROL Criar]**. Na lista suspensa **[!UICONTROL Solução da nuvem]**, selecione **[!UICONTROL Adobe Launch]**. Na lista suspensa **[!UICONTROL Certificado]**, selecione o nome do certificado criado anteriormente.)

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)

   Configuração técnica de conta Adobe IMS - página Certificado.

1. A página **[!UICONTROL Conta]** tem cinco campos que exigirão que você preencha usando as informações da página Detalhes da integração da etapa anterior.

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)

   Configuração técnica de conta Adobe IMS - página Conta.

1. Na página **[!UICONTROL Conta]** , preencha os seguintes campos:

   * **[!UICONTROL Título]** - Informe um título descritivo da conta.
   * **[!UICONTROL Servidor]** de autorização - Retorne à página de detalhes da integração aberta anteriormente. Click the **[!UICONTROL JWT]** tab. Copie o nome do servidor, sem o caminho, conforme destacado abaixo.

(o nome do servidor de exemplo é apenas para fins ilustrativos)   Retorne à página **[!UICONTROL Conta]** e cole o nome no respectivo campo.
Por exemplo, `https://ims-na1.adobelogin.com/`(o nome do servidor de exemplo é apenas para fins ilustrativos)

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)

   Página de detalhes da integração - guia JWT

1. **[!UICONTROL Chave da API]** - Retorne à página de detalhes da integração. Clique na guia **[!UICONTROL Visão geral]** e, à direita do campo **[!UICONTROL Chave da API (ID do cliente)]**, clique em **[!UICONTROL Copiar]**.

   Return to the **[!UICONTROL Account]** page, then paste the key into the respective ****field.

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)

   Página de detalhes da integração.

1. **[!UICONTROL Segredo do cliente]** - Retorne à página Detalhes da integração. Na guia **[!UICONTROL Visão geral]**, clique em **[!UICONTROL Recuperar segredo do cliente]**. À direita do campo **[!UICONTROL Segredo do cliente]**, clique em **[!UICONTROL Copiar]**.

   Retorne à página **[!UICONTROL Conta]** e cole a chave no respectivo campo.

1. **[!UICONTROL Carga]** - Retorne à página de detalhes da Integração. Na guia **[!UICONTROL JWT]** , no campo Carga JWT, copie todo o código do objeto JSON.

   Retorne à página **[!UICONTROL Conta]** e cole o código no respectivo campo.

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)

   Página de detalhes da integração - guia JWT

   A página Conta, com todos os campos preenchidos, será semelhante ao seguinte:

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. Near the upper-right corner of the **[!UICONTROL Account]** page, click **[!UICONTROL Create]**.

   Com AEM IMS configurado, agora você tem uma nova IMSAccount listada em Configurações **[!UICONTROL IMS do]** Adobe.

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## Configuração da Adobe Launch Cloud para integração {#configuring-adobe-launch-cloud-for-the-integration}

1. AEM autor, próximo ao canto superior esquerdo, clique no ícone Ferramentas (martelo) e clique em **[!UICONTROL Cloud Services > Configurações]** de inicialização de Adobe.

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. Na página Configurações **[!UICONTROL de inicialização de]** Adobe, no painel esquerdo, selecione um Site AEM para o qual você deseja aplicar a Configuração de inicialização de Adobe.

   Somente para fins de ilustração, o Site **[!UICONTROL We.Retail]** é selecionado na captura de tela abaixo.

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. Ao lado do canto superior esquerdo da página, clique em **[!UICONTROL Criar]**.
1. Na página **[!UICONTROL Geral]** (1/3 páginas) da janela **[!UICONTROL Criar configuração do Adobe Launch]**, preencha os seguintes campos:

   * **[!UICONTROL Título]** - Insira um título de configuração descritiva. Por exemplo, `We.Retail Launch cloud configuration`.

   * **[!UICONTROL Configuração]** Adobe IMS associada - selecione a configuração IMS criada anteriormente em [Configuração AEM IMS](#configuring-aem-ims).

   * **[!UICONTROL Empresa]** - Na lista suspensa **[!UICONTROL Empresa]** , selecione a empresa da Experience Cloud. A lista é preenchida automaticamente.

   * **[!UICONTROL Propriedade]** - Na lista suspensa Propriedade, selecione a propriedade Adobe Launch criada anteriormente. A lista é preenchida automaticamente.
   Depois de preencher todos os campos, sua página **[!UICONTROL Geral]** será semelhante ao seguinte:

   ![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. Próximo ao canto superior esquerdo, clique em **[!UICONTROL Avançar]**.
1. Na página **[!UICONTROL Preparo]** (2/3 páginas) da janela **[!UICONTROL Criar configuração do Adobe Launch]**, preencha o seguinte campo:

   No campo **[!UICONTROL URI da biblioteca]**, verifique o local da versão de preparo da biblioteca do Adobe Launch. O AEM preenche esse campo automaticamente.

   Apenas para fins ilustrativos, esta etapa usará bibliotecas de Adobe Launch implantadas no Adobe CDN.

   >[!NOTE]
   >
   >Verifique se o URI da biblioteca preenchido automaticamente (Uniform Resource Identifier) não está malformado. Se necessário, corrija-o para que o URI represente um URI relativo ao protocolo. Ou seja, ele start de uma duplo para a frente.
   >
   >
   >Por exemplo: `//assets.adobetm.com/launch-xxxx`.

   Sua página **[!UICONTROL Preparação]** deve ser semelhante a seguinte. Observe que as opções **[!UICONTROL Arquivar]** e **[!UICONTROL Carregar biblioteca de forma assíncrona]** ***não*** estão definidas:

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. Perto do canto superior direito, clique em **[!UICONTROL Avançar]**.
1. Na página **[!UICONTROL Produção]** (3/3 páginas) da janela **[!UICONTROL Criar configuração do Adobe Launch]**, se necessário, corrija o URI de produção preenchido automaticamente de modo semelhante ao que foi feito na página **[!UICONTROL Preparação]** anterior.
1. Perto do canto superior direito, clique em **[!UICONTROL Criar]**.

   Sua nova Configuração da Adobe Launch Cloud agora é criada e listada ao lado do seu site da Web, como no exemplo a seguir:

1. Selecione sua nova Adobe para Iniciar a configuração da nuvem (uma marca de seleção é exibida à esquerda do título da configuração quando ela é selecionada). Na barra de ferramentas, clique em **[!UICONTROL Publicar]**.

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

Atualmente, AEM autor não suporta a integração dos Visualizadores de Mídia Dinâmica com o Adobe Launch.

No entanto, ele é suportado no nó de publicação AEM. Usando as configurações padrão da Configuração da Adobe Launch Cloud, AEM publish usa o ambiente de produção da Adobe Launch. Dessa forma, é necessário enviar atualizações da biblioteca de inicialização de Adobe do Desenvolvimento para o ambiente de produção sempre durante o teste.

É possível contornar essa limitação especificando o URL de desenvolvimento ou armazenamento temporário da biblioteca de inicialização do Adobe na configuração da Adobe Launch Cloud para AEM publicação acima. Isso faz com que o nó de publicação AEM use a versão de Desenvolvimento ou Preparação da biblioteca de Adobe Launch.

Consulte [Integrar AEM com o Adobe Launch via E/S](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html) Adobe para obter mais informações sobre como configurar a Configuração da Adobe Launch Cloud.
