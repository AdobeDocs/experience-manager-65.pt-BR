---
title: Configuração do rastreamento de vídeo para Adobe Analytics
seo-title: Configuração do rastreamento de vídeo para Adobe Analytics
description: Saiba mais sobre como configurar o rastreamento de vídeo para o SiteCatalyst.
seo-description: Saiba mais sobre como configurar o rastreamento de vídeo para o SiteCatalyst.
uuid: 5a862f05-abfa-42a2-ad40-4c1c32f1bd75
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: a18ddac1-9e4c-4857-9cb3-4d5eeb8dd9ec
docset: aem65
translation-type: tm+mt
source-git-commit: 90c99e527a40bb663d4f32d8746b46cf34a2319f
workflow-type: tm+mt
source-wordcount: '1766'
ht-degree: 1%

---


# Configuração do rastreamento de vídeo para Adobe Analytics{#configuring-video-tracking-for-adobe-analytics}

Há vários métodos disponíveis para rastrear eventos de vídeo, sendo 2 opções herdadas para versões mais antigas do Adobe Analytics. Essas opções herdadas são: Marcos herdados e segundos herdados.

>[!NOTE]
>
>Antes de continuar, verifique se o vídeo **** reproduzível foi carregado no AEM.
>
>Para garantir que seus vídeos sejam reproduzidos na página, consulte **[este tutorial](/help/sites-authoring/default-components-foundation.md#video)** para obter informações sobre como transcodificar arquivos de vídeo no AEM.

Use o procedimento a seguir para configurar uma estrutura para rastreamento de vídeo usando cada método.

>[!NOTE]
>
>Para novas implementações, é recomendável que você **não use** as opções herdadas para rastreamento de vídeo. Em vez disso, use o método **Milestones** .

## Etapas comuns {#common-steps}

1. Configure uma página da Web arrastando um componente **de** vídeo do sidekick e adicionando um **vídeo reproduzível como um ativo** para o componente

1. [Crie uma configuração e uma estrutura](/help/sites-administering/adobeanalytics.md)Adobe Analytics.

   * Os exemplos nas seções a seguir usam o nome **my-sc-configuration** para a configuração e o **videofw** da estrutura.

1. Na página da estrutura, selecione um RSID e defina o uso como todos. ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. A partir da categoria de componente Geral no Sidekick, arraste o componente Vídeo até a estrutura.
1. Selecione um método de rastreamento:

   * [Marcos](/help/sites-administering/adobeanalytics.md)
   * [Marcos não herdados](/help/sites-administering/adobeanalytics.md)
   * [Marcos herdados](/help/sites-administering/adobeanalytics.md)
   * [Segundos herdados](/help/sites-administering/adobeanalytics.md)

1. Quando você seleciona um método de rastreamento, a lista das variáveis do CQ muda de acordo. Use as seções a seguir para obter informações sobre como configurar ainda mais o componente e mapear as variáveis do CQ com as propriedades do Adobe Analytics.

## Milestones {#milestones}

O método Marcos rastreia a maioria das informações sobre o vídeo, é altamente personalizável e fácil de configurar.

Para usar o método Marcos, especifique os deslocamentos de rastreamento baseados em tempo para definir os marcos. Quando uma reprodução de vídeo ultrapassar um marco, a página chamará a Adobe Analytics para rastrear o evento. Para cada marco definido, o componente cria uma variável CQ que pode ser mapeada para uma propriedade do Adobe Analytics. O nome dessas variáveis CQ usa o seguinte formato:

```shell
eventdata.events.milestoneXX
```

O sufixo XX é o deslocamento de rastreamento que define o marco. Por exemplo, a especificação de deslocamentos de rastreamento de 4, 8, 16, 20 e 28 segundos gera as seguintes variáveis de CQ:

* `eventdata.events.milestone4`
* `eventdata.events.milestone8`
* `eventdata.events.milestone16`
* `eventdata.events.milestone20`
* `eventdata.events.milestone28`

A tabela a seguir descreve as variáveis CQ padrão fornecidas para o método Marcos:

<table>
 <tbody>
  <tr>
   <th>Variáveis CQ</th>
   <th>Propriedades do Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>As variáveis mapeadas para esta opção conterão o nome amigável <strong>para o</strong> usuário (<strong>Título</strong>) do vídeo, se definido no DAM; se isso não for definido, o nome <strong>do</strong> arquivo do vídeo será enviado. Enviado apenas uma vez, no início da reprodução de um vídeo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>As variáveis mapeadas para isso conterão o nome do arquivo. Enviados somente com eventdata.eventos.a.media.visualização </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>As variáveis mapeadas para isso conterão o caminho do arquivo no servidor. Enviados somente com eventdata.eventos.a.media.visualização </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>Enviado sempre que um marco de segmento é aprovado </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>Sempre que um marco é acionado, o número de segundos que o usuário gastou assistindo ao segmento especificado também é enviado juntamente com esse evento. por exemplo, eventX=21<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>Enviado ao inicializar a visualização de vídeo</td>
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
   <td>Enviados em cada marco; aparece como pev3 na chamada do Adobe Analytics, normalmente enviada como "vídeo"<br /> </td>
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
>É possível definir o nome amigável **para o** usuário de um vídeo abrindo o vídeo para edição no DAM e definindo o campo de metadados **Título** como o nome desejado.

1. Depois de selecionar Marcos como o método de rastreamento, na caixa Deslocamento da faixa, digite uma lista separada por vírgulas de deslocamentos de rastreamento em segundos. Por exemplo, o valor a seguir define marcos em 4, 8, 16, 20 e 28 segundos após o start do vídeo:

   ```xml
   4,8,16,20,24
   ```

   Os valores de deslocamento devem ser inteiros com mais de 0. O valor padrão é `10,25,50,75`.

1. Para mapear as variáveis do CQ para as propriedades do Adobe Analytics, arraste as propriedades do Adobe Analytics do ContentFinder ao lado da variável do CQ no componente.

   Para obter informações sobre como otimizar os mapeamentos, consulte o guia [Medição de vídeo no Adobe Analytics](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html) .

1. [Adicione a estrutura](/help/sites-administering/adobeanalytics.md) à página.
1. Para testar a configuração no modo **de** Pré-visualização, reproduza o vídeo para acionar as chamadas do Adobe Analytics.

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

Neste exemplo, o componente Vídeo é exibido da seguinte forma na página de estrutura:

![video1](assets/video1.png)

>[!NOTE]
>
>Para ver as chamadas feitas para a Adobe Analytics, use uma ferramenta apropriada, como o Depurador DigitalPulse ou o Fiddler.

As chamadas para a Adobe Analytics usando o exemplo fornecido devem ser semelhantes quando visualizadas com o DigitalPulse Debugger:

![chlimage_1-128](assets/chlimage_1-128.png)

*Esta é a **primeira chamada**feita para a Adobe Analytics que contém os seguintes valores:*

* *prop1 e eVar1 para eventdata.a.media.name,*
* *props2-4, juntamente com o eVar 2 e o eVar 3 contendo contentType (vídeo) e segmento (1:O:1-4)*
* *evento3 que foi mapeado para eventdata.eventos.a.media.visualização.*

![chlimage_1-129](assets/chlimage_1-129.png)

*Esta é a **terceira chamada**feita à Adobe Analytics:*

* *prop1 e eVar1 contêm a.media.name;*
* *evento 1 porque um segmento foi visualizado*
* *evento2 enviado com tempo reproduzido = 4*
* *evento11 enviado porque eventdata.eventos.milestone8 foi atingido*
* *prop2 para 4 não são enviados (já que eventdata.eventos.a.media.visualização não foi acionado)*

## Marcos não herdados {#non-legacy-milestones}

O método Marcos não herdados é semelhante ao método Marcos, exceto que os marcos são definidos usando porcentagens da duração da faixa. Os pontos comuns são os seguintes:

* Quando uma reprodução de vídeo ultrapassar um marco, a página chamará a Adobe Analytics para rastrear o evento.
* O conjunto [estático de variáveis](#cqvars) CQ definidas para mapeamento com propriedades do Adobe Analytics.
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

1. Depois de selecionar Etapas não herdadas como método de rastreamento, na caixa Deslocamento da faixa, digite uma lista separada por vírgulas com porcentagens da duração da faixa. Por exemplo, o seguinte valor padrão define marcos em 10, 25, 50 e 75 por cento do comprimento da faixa:

   ```xml
   10,25,50,75
   ```

   Os valores de deslocamento devem ser inteiros com mais de 0.

1. Para mapear as variáveis do CQ para as propriedades do Adobe Analytics, arraste as propriedades do Adobe Analytics do ContentFinder ao lado da variável do CQ no componente.

   Para obter informações sobre como otimizar os mapeamentos, consulte o guia [Medição de vídeo no Adobe Analytics](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html) .

1. [Adicione a estrutura](/help/sites-administering/adobeanalytics.md) à página.
1. Para testar a configuração no modo **de** Pré-visualização, reproduza o vídeo para acionar as chamadas do Adobe Analytics.

## Marcos herdados {#legacy-milestones}

Esse método é semelhante ao método Marcos com a diferença de que os marcos especificados no campo de deslocamento *de* rastreamento são percentuais em vez de pontos definidos no vídeo.

>[!NOTE]
>
>O campo de deslocamento de rastreamento aceita apenas uma lista separada por vírgulas contendo números inteiros entre 1 e 100.

1. Defina o deslocamento da faixa.

   * e.g.10,50,75,100

   Além disso, as informações enviadas à Adobe Analytics são menos personalizáveis; há apenas 3 variáveis disponíveis para mapeamento:

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>As variáveis mapeadas para esta opção conterão o nome amigável <strong>para o</strong> usuário (<strong>Título</strong>) do vídeo, se definido no DAM; se o Título não estiver definido, o nome <strong>do</strong> arquivo do vídeo será enviado. Enviado apenas uma vez, no início da reprodução de um vídeo.<br /> </td>
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
>É possível definir o nome amigável **para o** usuário de um vídeo abrindo o vídeo para edição no DAM e definindo o campo de metadados **Título** como o nome desejado. Também é necessário Salvar as alterações feitas ao terminar.

1. Mapear essas variáveis para props 1 a 3

   O **restante das informações** relevantes na chamada serão enviadas concatenadas para **uma** variável chamada **pev3**.

   **As chamadas** de amostra para a Adobe Analytics usando o exemplo fornecido devem ser semelhantes quando visualizadas com o Depurador DigitalPulse:

   ![lmilestones1](assets/lmilestones1.png)

   *A variável **pev3**enviada na chamada contém as seguintes informações:*

   * *Nome* - O nome do arquivo de vídeo (*movie.avi*)

   * *Duração* - A duração do arquivo de vídeo, em segundos (*100*)

   * *Nome* do player - o player de vídeo usado para reproduzir o arquivo de vídeo (vídeo ** HTML5)

   * *Total de segundos reproduzidos* - o número total de segundos em que o vídeo foi reproduzido (*25*)

   * *Carimbo de data e hora* do start - Carimbo de data e hora que identifica quando a reprodução do vídeo começou (*1331035567*)

   * *Sessão* Play - Os detalhes da sessão Play. Este campo indica como o usuário interagiu com o vídeo. Isso pode incluir dados como o local em que começaram a reproduzir o vídeo, se eles usaram o controle deslizante para avançar o vídeo e onde pararam de reproduzir o vídeo (*L10E24S58L58 - o vídeo foi interrompido em segundos. 25 da seção L10, depois pulado para s. 48*)

## Segundos herdados {#legacy-seconds}

Ao usar o método** de segundos herdados**, as chamadas da Adobe Analytics são acionadas a cada N-ésimo segundo, onde N é especificado no campo de deslocamento Track.

1. Defina o deslocamento da faixa para qualquer número de segundos,

   * por exemplo, 6
   >[!NOTE]
   >
   >O campo de deslocamento de rastreamento aceita apenas números inteiros que sejam superiores a 0

   As informações enviadas à Adobe Analytics são menos personalizáveis. Há apenas 3 variáveis disponíveis para mapeamento:

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>As variáveis mapeadas para esta opção conterão o nome amigável <strong>para o</strong> usuário (<strong>Título</strong>) do vídeo, se definido no DAM; se o Título não estiver definido, o nome <strong>do</strong> arquivo do vídeo será enviado. Enviado apenas uma vez, no início da reprodução de um vídeo.<br /> </td>
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
>É possível definir o nome amigável **para o** usuário de um vídeo abrindo o vídeo para edição no DAM e definindo o campo de metadados **Título** como o nome desejado. Também é necessário Salvar as alterações feitas ao terminar.

1. Mapeie essas variáveis para prop1, prop2 e prop3

   O **restante das informações** relevantes na chamada serão enviadas concatenadas para **uma** variável chamada **pev3**.

   As chamadas para a Adobe Analytics usando o exemplo fornecido devem ser semelhantes quando visualizadas com o DigitalPulse Debugger:

   ![segundos](assets/lseconds.png)

   *A chamada é semelhante à chamada Legacy Milestones acima. Consulte as informações sobre o pev3 **[fornecidas lá](/help/sites-administering/adobeanalytics.md)**.*

**Referências usadas neste tutorial:**

[0] [https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)
