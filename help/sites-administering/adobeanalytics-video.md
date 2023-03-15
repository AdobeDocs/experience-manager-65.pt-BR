---
title: Configuração do rastreamento de vídeo para o Adobe Analytics
seo-title: Configuring Video Tracking for Adobe Analytics
description: Saiba mais sobre como configurar o rastreamento de vídeo para SiteCatalyst.
seo-description: Learn about configuring video tracking for SiteCatalyst.
uuid: 5a862f05-abfa-42a2-ad40-4c1c32f1bd75
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: a18ddac1-9e4c-4857-9cb3-4d5eeb8dd9ec
docset: aem65
exl-id: 5d51f898-b6d1-40ac-bdbf-127cda1dc777
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 2%

---

# Configuração do rastreamento de vídeo para o Adobe Analytics{#configuring-video-tracking-for-adobe-analytics}

Há vários métodos disponíveis para rastrear eventos de vídeo, 2 dos quais são opções herdadas para versões mais antigas do Adobe Analytics. Essas opções herdadas são: Marcos herdados e segundos herdados.

>[!NOTE]
>
>Antes de continuar, verifique se você tem uma **vídeo reproduzível** carregado no AEM.
>
>Para garantir que seus vídeos sejam reproduzidos na página, consulte **[este tutorial](/help/sites-authoring/default-components-foundation.md#video)** para obter informações sobre como transcodificar arquivos de vídeo no AEM.

Use o procedimento a seguir para configurar uma estrutura para o rastreamento de vídeo usando cada método.

>[!NOTE]
>
>Para novas implementações, é recomendável que você **não use** as opções herdadas para rastreamento de vídeo. Use o **Marcos** em vez disso.

## Etapas comuns {#common-steps}

1. Configure uma página da Web arrastando um **componente de vídeo** do sidekick e adição de um player **vídeo como um ativo** para o componente

1. [Criar uma configuração e uma estrutura do Adobe Analytics](/help/sites-administering/adobeanalytics.md).

   * Os exemplos nas seções seguintes usam o nome **my-sc-configuration** para a configuração e **videofw** para o quadro.

1. Na página da estrutura, selecione um RSID e defina o uso para todos. ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. Na categoria de componente Geral do Sidekick, arraste o componente Vídeo até a estrutura.
1. Selecione um método de rastreamento:

   * [Marcos](/help/sites-administering/adobeanalytics.md)
   * [Marcos não herdados](/help/sites-administering/adobeanalytics.md)
   * [Marcos herdados](/help/sites-administering/adobeanalytics.md)
   * [Segundos herdados](/help/sites-administering/adobeanalytics.md)

1. Quando você seleciona um método de rastreamento, a lista de variáveis CQ é alterada de acordo. Use as seções a seguir para obter informações sobre como configurar ainda mais o componente e mapear as variáveis do CQ com propriedades do Adobe Analytics.

## Marcos {#milestones}

O método de marcos rastreia a maioria das informações sobre o vídeo, é altamente personalizável e fácil de configurar.

Para usar o método Marcos, especifique deslocamentos de rastreamento com base no tempo para definir os marcos. Quando a reprodução de um vídeo ultrapassa um marco, a página chama o Adobe Analytics para rastrear o evento. Para cada marco definido, o componente cria uma variável CQ que pode ser mapeada para uma propriedade do Adobe Analytics. O nome dessas variáveis CQ usa o seguinte formato:

```shell
eventdata.events.milestoneXX
```

O sufixo XX é o deslocamento de rastreamento que define o marco. Por exemplo, especificar deslocamentos de rastreamento de 4, 8, 16, 20 e 28 segundos gera as seguintes variáveis de CQ:

* `eventdata.events.milestone4`
* `eventdata.events.milestone8`
* `eventdata.events.milestone16`
* `eventdata.events.milestone20`
* `eventdata.events.milestone28`

A tabela a seguir descreve as variáveis CQ padrão fornecidas para o método de Marcos:

<table>
 <tbody>
  <tr>
   <th>Variáveis CQ</th>
   <th>Propriedades do Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>As variáveis mapeadas para isso conterão a variável <strong>fácil de usar</strong> name (<strong>Título</strong>) do vídeo, se definido no DAM; se isso não for definido, a variável <strong>nome do arquivo</strong> será enviada em vez disso. Enviado apenas uma vez, no início da reprodução de um vídeo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>As variáveis mapeadas para isso conterão o nome do arquivo. Enviado somente com eventdata.events.a.media.view </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>As variáveis mapeadas para isso conterão o caminho do arquivo no servidor. Enviado somente com eventdata.events.a.media.view </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>Enviado sempre que um marco de segmento é passado </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>Enviado sempre que um marco é acionado, o número de segundos que o usuário gastou assistindo a determinado segmento também é enviado junto com esse evento. por exemplo, eventX=21<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>Enviado ao inicializar visualização de vídeo</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>Enviado quando a reprodução do vídeo é concluída<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestoneX </td>
   <td>Enviado quando o marco especificado é passado, X representa o segundo em que o marco é acionado em<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>Enviado em cada marco; é exibido como pev3 na chamada do Adobe Analytics, normalmente enviado como "vídeo"<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>Corresponde exatamente a eventdata.videoName </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>Contém informações sobre o segmento que foi visualizado, por exemplo, 2:O:4-8 </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>É possível definir um **fácil de usar** abra o vídeo para edição no DAM e defina a variável **Título** campo de metadados para o nome desejado.

1. Depois de selecionar Marcos como método de rastreamento, na caixa Rastrear deslocamento , insira uma lista separada por vírgulas de deslocamentos de rastreamento em segundos. Por exemplo, o valor a seguir define os marcos em 4, 8, 16, 20 e 28 segundos após o início do vídeo:

   ```xml
   4,8,16,20,24
   ```

   Os valores de deslocamento devem ser inteiros com mais de 0. O valor padrão é `10,25,50,75`.

1. Para mapear as variáveis CQ para as propriedades do Adobe Analytics, arraste as propriedades do Adobe Analytics do ContentFinder ao lado da variável CQ no componente.

   Para obter informações sobre otimização de mapeamentos, consulte o [Avaliação de vídeo no Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html) guia.

1. [Adicionar a estrutura](/help/sites-administering/adobeanalytics.md) à página.
1. Para testar a configuração em **Modo de visualização**, reproduza o vídeo para acionar chamadas do Adobe Analytics.

Os exemplos de dados de rastreamento do Adobe Analytics a seguir se aplicam ao rastreamento de marcos usando deslocamentos de rastreamento de 4,8,16,20 e 24, e os seguintes mapeamentos para as variáveis do CQ:

<table>
 <tbody>
  <tr>
   <th>Variável CQ</th>
   <th>Propriedade Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>prop2</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>prop3 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>prop4</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>event1</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>event2<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>event3</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>event4<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestone4</td>
   <td>event10</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone8</td>
   <td>event11</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone16</td>
   <td>event12</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone20</td>
   <td>event13</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone24</td>
   <td>event14</td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>eVar 1, prop1 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>eVar2</td>
  </tr>
 </tbody>
</table>

Para este exemplo, o componente Vídeo é exibido da seguinte maneira na página de estrutura:

![video1](assets/video1.png)

>[!NOTE]
>
>Para ver as chamadas feitas para o Adobe Analytics, use uma ferramenta adequada, como o DigitalPulse Debugger ou Fiddler.

As chamadas para o Adobe Analytics usando o exemplo fornecido devem ser semelhantes quando exibidas com o DigitalPulse Debugger:

![chlimage_1-128](assets/chlimage_1-128.png)

*Este é o **primeira chamada**feito no Adobe Analytics contendo os seguintes valores:*

* *prop1 e eVar1 para eventdata.a.media.name,*
* *props2-4, juntamente com eVar2 e eVar3 contendo contentType (vídeo) e segmento (1:O:1-4)*
* *event3 que foi mapeado para eventdata.events.a.media.view.*

![chlimage_1-129](assets/chlimage_1-129.png)

*Este é o **terceira chamada**feito no Adobe Analytics:*

* *prop1 e eVar1 contêm a.media.name;*
* *event1 porque um segmento foi visualizado*
* *event2 enviado com tempo reproduzido = 4*
* *event11 enviado porque eventdata.events.milestone8 foi atingido*
* *prop2 a 4 não são enviadas (já que eventdata.events.a.media.view não foi acionado)*

## Marcos não herdados {#non-legacy-milestones}

O método de marcos não herdados é semelhante ao método de marcos, exceto que os marcos são definidos usando porcentagens da duração da faixa. Os pontos comuns são os seguintes:

* Quando a reprodução de um vídeo ultrapassa um marco, a página chama o Adobe Analytics para rastrear o evento.
* O [conjunto estático de variáveis CQ](#cqvars) que são definidas para mapeamento com propriedades do Adobe Analytics.
* Para cada marco definido, o componente cria uma variável CQ que pode ser mapeada para uma propriedade do Adobe Analytics.

O nome dessas variáveis CQ usa o seguinte formato:

O sufixo XX é a porcentagem da duração da faixa que define o marco. Por exemplo, especificar porcentagens de 10, 25, 50 e 75 gera as seguintes variáveis de CQ:

* `eventdata.events.milestone10`
* `eventdata.events.milestone25`
* `eventdata.events.milestone50`
* `eventdata.events.milestone75`

```shell
eventdata.events.milestoneXX
```

1. Depois de selecionar marcos não herdados como método de rastreamento, na caixa Rastrear deslocamento , insira uma lista separada por vírgulas de porcentagens da duração da faixa. Por exemplo, o valor padrão a seguir define os marcos em 10, 25, 50 e 75% da duração da faixa:

   ```xml
   10,25,50,75
   ```

   Os valores de deslocamento devem ser inteiros com mais de 0.

1. Para mapear as variáveis CQ para as propriedades do Adobe Analytics, arraste as propriedades do Adobe Analytics do ContentFinder ao lado da variável CQ no componente.

   Para obter informações sobre otimização de mapeamentos, consulte o [Avaliação de vídeo no Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html) guia.

1. [Adicionar a estrutura](/help/sites-administering/adobeanalytics.md) à página.
1. Para testar a configuração em **Modo de visualização**, reproduza o vídeo para acionar chamadas do Adobe Analytics.

## Marcos herdados {#legacy-milestones}

Esse método é semelhante ao método Marcos com a diferença de que os marcos especificados na variável *Deslocamento de rastreamento* são porcentagens em vez de pontos definidos no vídeo.

>[!NOTE]
>
>O campo Tracking offset aceita apenas uma lista separada por vírgulas contendo números inteiros entre 1 e 100.

1. Defina o deslocamento da Faixa.

   * e.g.10,50,75,100

   Além disso, as informações enviadas para a Adobe Analytics são menos personalizáveis; há apenas 3 variáveis disponíveis para mapeamento:

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>As variáveis mapeadas para isso conterão a variável <strong>fácil de usar</strong> name (<strong>Título</strong>) do vídeo, se definido no DAM; se o Título não estiver definido, o <strong>nome do arquivo</strong> será enviada em vez disso. Enviado apenas uma vez, no início da reprodução de um vídeo.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>As variáveis mapeadas para isso conterão o nome do arquivo. Enviado apenas uma vez, no início da reprodução de um vídeo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>A variável mapeada para isso conterá o caminho do arquivo no servidor. Enviado apenas uma vez, no início da reprodução de um vídeo.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>É possível definir um **fácil de usar** abra o vídeo para edição no DAM e defina a variável **Título** campo de metadados para o nome desejado. Também é necessário Salvar as alterações feitas ao concluir.

1. Mapear essas variáveis para props 1 a 3

   O **resto das informações pertinentes** na chamada será enviada concatenada para **one** variável nomeada **pev3**.

   **Exemplos de chamadas** para o Adobe Analytics usando o exemplo fornecido deve ser semelhante a este quando exibido com o DigitalPulse Debugger:

   ![lmilestones1](assets/lmilestones1.png)

   *O **pev3**enviada na chamada contém as seguintes informações:*

   * *Nome* - O nome do arquivo de vídeo (*filme.avi*)

   * *Length* - A duração do arquivo de vídeo, em segundos (*100*)

   * *Nome do reprodutor* - O reprodutor de vídeo utilizado para reproduzir o ficheiro de vídeo (*Vídeo HTML5*)

   * *Total de segundos reproduzidos* - O número total de segundos de reprodução do vídeo (*25.*)

   * *Iniciar carimbo de data e hora* - Carimbo de data e hora que identifica quando a reprodução do vídeo foi iniciada (*1331035567*)

   * *Reproduzir sessão* - Os detalhes da sessão de reprodução. Este campo indica como o usuário interagiu com o vídeo. Isso pode incluir dados como onde eles começaram a reproduzir o vídeo, se eles usaram o controle deslizante do vídeo para avançar o vídeo e onde pararam de reproduzir o vídeo (*L10E24S58L58 - vídeo parado em s. 25 da seção L10, em seguida, ignoradas. 48*)

## Segundos herdados {#legacy-seconds}

Ao usar o método** herdado seconds**, as chamadas do Adobe Analytics são acionadas a cada N-ésimo segundo, onde N é especificado no campo Track offset.

1. Defina o deslocamento da Faixa para qualquer número de segundos,

   * Por exemplo, 6
   >[!NOTE]
   >
   >O campo Rastreamento de deslocamento aceita apenas números inteiros que sejam maiores que 0

   As informações enviadas para a Adobe Analytics são menos personalizáveis. Há apenas 3 variáveis disponíveis para mapeamento:

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>As variáveis mapeadas para isso conterão a variável <strong>fácil de usar</strong> name (<strong>Título</strong>) do vídeo, se definido no DAM; se o Título não estiver definido, o <strong>nome do arquivo</strong> será enviada em vez disso. Enviado apenas uma vez, no início da reprodução de um vídeo.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>A variável mapeada para isso conterá o nome do arquivo. Enviado apenas uma vez, no início da reprodução de um vídeo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>A variável mapeada para isso conterá o caminho do arquivo no servidor. Enviado apenas uma vez, no início da reprodução de um vídeo.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>É possível definir um **fácil de usar** abra o vídeo para edição no DAM e defina a variável **Título** campo de metadados para o nome desejado. Também é necessário Salvar as alterações feitas ao concluir.

1. Mapear essas variáveis para prop1, prop2 e prop3

   O **resto das informações pertinentes** na chamada será enviada concatinada para **one** variável nomeada **pev3**.

   As chamadas para o Adobe Analytics usando o exemplo fornecido devem ser semelhantes quando exibidas com o DigitalPulse Debugger:

   ![lseconds](assets/lseconds.png)

   *A chamada é semelhante à chamada de marcos herdados acima. Consulte as informações sobre pev3 **[desde que](/help/sites-administering/adobeanalytics.md)**.*

**Referências usadas neste tutorial:**

[0] [https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html)
