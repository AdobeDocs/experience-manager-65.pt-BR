---
title: Configuração do rastreamento de vídeo para o Adobe Analytics
description: Saiba mais sobre como configurar o rastreamento de vídeo para o SiteCatalyst.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 5d51f898-b6d1-40ac-bdbf-127cda1dc777
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1754'
ht-degree: 0%

---

# Configuração do rastreamento de vídeo para o Adobe Analytics{#configuring-video-tracking-for-adobe-analytics}

Há vários métodos disponíveis para rastrear eventos de vídeo, dois dos quais são opções herdadas para versões mais antigas do Adobe Analytics. Essas opções herdadas são: Marcos herdados e Segundos herdados.

>[!NOTE]
>
>Antes de continuar, verifique se você tem uma **vídeo reproduzível** enviado por AEM.
>
>Para garantir que seus vídeos sejam reproduzidos na página, consulte **[este tutorial](/help/sites-authoring/default-components-foundation.md#video)** para obter informações sobre como transcodificar arquivos de vídeo no AEM.

Use o procedimento a seguir para configurar uma estrutura para o rastreamento de vídeo usando cada método.

>[!NOTE]
>
>Para novas implementações, é recomendável que você **não usar** as opções herdadas para o rastreamento de vídeo. Use o **Etapas** em vez disso.

## Etapas comuns {#common-steps}

1. Configurar uma página da Web arrastando um **componente de vídeo** no sidekick e adicionar um reproduzível **vídeo como um ativo** para o componente

1. [Criar uma configuração e estrutura do Adobe Analytics](/help/sites-administering/adobeanalytics.md).

   * Os exemplos nas seções seguintes usam o nome **my-sc-configuration** para a configuração e **videofw** para o quadro.

1. Na página da estrutura, selecione uma RSID e defina o uso para todos. ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. Na categoria geral de componentes no Sidekick, arraste o componente de Vídeo para a estrutura.
1. Selecione um método de rastreamento:

   * [Etapas](/help/sites-administering/adobeanalytics.md)
   * [Etapas não herdadas](/help/sites-administering/adobeanalytics.md)
   * [Etapas herdadas](/help/sites-administering/adobeanalytics.md)
   * [Segundos herdados](/help/sites-administering/adobeanalytics.md)

1. Quando você seleciona um método de rastreamento, a lista de variáveis CQ é alterada de acordo. Use as seções a seguir para obter informações sobre como configurar o componente e mapear as variáveis CQ com propriedades do Adobe Analytics.

## Etapas {#milestones}

O método de etapas rastreia a maioria das informações sobre o vídeo, é altamente personalizável e fácil de configurar.

Para usar o método Marcos, especifique deslocamentos de rastreamento com base no tempo para definir os marcos. Quando uma reprodução de vídeo passa um marco, a página chama o Adobe Analytics para rastrear o evento. Para cada marco definido, o componente cria uma variável do CQ que você pode mapear para uma propriedade do Adobe Analytics. O nome dessas variáveis CQ usa o seguinte formato:

```shell
eventdata.events.milestoneXX
```

O sufixo XX é o deslocamento da faixa que define o marco. Por exemplo, especificar deslocamentos de rastreamento de 4, 8, 16, 20 e 28 segundos gera as seguintes variáveis CQ:

* `eventdata.events.milestone4`
* `eventdata.events.milestone8`
* `eventdata.events.milestone16`
* `eventdata.events.milestone20`
* `eventdata.events.milestone28`

A tabela a seguir descreve as variáveis de CQ padrão fornecidas para o método de Marcos:

<table>
 <tbody>
  <tr>
   <th>Variáveis CQ</th>
   <th>Propriedades do Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>As variáveis mapeadas para esse conterão a variável <strong>fácil de usar</strong> nome (<strong>Título</strong>) do vídeo, se definido no DAM; se não estiver definido, o do vídeo <strong>nome do arquivo</strong> será enviado. Enviado somente uma vez, no início da reprodução de um vídeo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>As variáveis mapeadas para esse local conterão o nome do arquivo. Enviado somente junto com eventdata.events.a.media.view </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>As variáveis mapeadas para esse local conterão o caminho do arquivo no servidor. Enviado somente junto com eventdata.events.a.media.view </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>Enviado sempre que uma etapa do segmento é aprovada </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>Enviado sempre que um marco é acionado, o número de segundos que o usuário gastou assistindo ao segmento específico também é enviado junto com esse evento. por exemplo, eventX=21<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>Enviado ao inicializar visualização de vídeo</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>Enviado quando o vídeo terminar de ser reproduzido<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestoneX </td>
   <td>Enviado quando o marco fornecido é passado, X representa o segundo em que o marco é acionado<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>Enviado em cada marco; exibido como pev3 na chamada do Adobe Analytics, geralmente enviado como "vídeo"<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>Corresponde exatamente a eventdata.videoName </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>Contém informações sobre o segmento que foi visualizado, por exemplo, <code>2:O:4-8</code> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>É possível definir as configurações de **fácil de usar** abrindo o vídeo para edição no DAM e definindo o parâmetro **Título** para o nome desejado.

1. Depois de selecionar Etapas como método de rastreamento, na caixa Rastrear deslocamento, insira uma lista separada por vírgulas de deslocamentos de rastreamento em segundos. Por exemplo, o valor a seguir define marcos em 4, 8, 16, 20 e 28 segundos após o início do vídeo:

   ```xml
   4,8,16,20,24
   ```

   Os valores de deslocamento devem ser números inteiros maiores que 0. O valor padrão é `10,25,50,75`.

1. Para mapear as variáveis CQ para as propriedades do Adobe Analytics, arraste as propriedades do Adobe Analytics do ContentFinder ao lado da variável CQ no componente.

   Para obter informações sobre como otimizar os mapeamentos, consulte [Medição de vídeo no Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html) guia.

1. [Adicionar a estrutura](/help/sites-administering/adobeanalytics.md) para a página.
1. Para testar a configuração no **Modo de visualização**, reproduza o vídeo para obter as chamadas do Adobe Analytics para acionar o.

Os exemplos de dados de rastreamento do Adobe Analytics a seguir se aplicam ao rastreamento de Marco usando deslocamentos de rastreamento de 4, 8, 16, 20 e 24, e os seguintes mapeamentos para as variáveis CQ:

<table>
 <tbody>
  <tr>
   <th>Variável CQ</th>
   <th>propriedade do Adobe Analytics</th>
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
   <td>EVAR 3</td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>eVar 1, prop1 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>EVAR 2</td>
  </tr>
 </tbody>
</table>

Neste exemplo, o componente de Vídeo aparece da seguinte maneira na página da estrutura:

![video1](assets/video1.png)

>[!NOTE]
>
>Para ver as chamadas feitas ao Adobe Analytics, use uma ferramenta apropriada, como DigitalPulse Debugger ou Fiddler.

As chamadas para o Adobe Analytics usando o exemplo fornecido devem ter esta aparência quando visualizadas com o DigitalPulse Debugger:

![chlimage_1-128](assets/chlimage_1-128.png)

*Este é o **primeira chamada**feito no Adobe Analytics contendo os seguintes valores:*

* *prop1 e eVar 1 para eventdata.a.media.name,*
* *props2-4, juntamente com eVar 2 e eVar 3 contendo contentType (vídeo) e segmento (1:O:1-4)*
* *event3 que foi mapeado para eventdata.events.a.media.view.*

![chlimage_1-129](assets/chlimage_1-129.png)

*Este é o **terceira chamada**feito no Adobe Analytics:*

* *prop1 e eVar 1 contêm a.media.name;*
* *event1 porque um segmento foi visualizado*
* *event2 enviado com o tempo reproduzido = 4*
* *event11 enviado porque eventdata.events.milestone8 foi atingido*
* *prop2 para 4 não são enviados (já que eventdata.events.a.media.view não foi acionado)*

## Etapas não herdadas {#non-legacy-milestones}

O método de Etapas não herdadas é semelhante ao método de Etapas, exceto que as etapas são definidas usando porcentagens da duração da trilha. As semelhanças são as seguintes:

* Quando uma reprodução de vídeo passa um marco, a página chama o Adobe Analytics para rastrear o evento.
* A variável [conjunto estático de variáveis CQ](#cqvars) que são definidos para mapeamento com propriedades do Adobe Analytics.
* Para cada marco definido, o componente cria uma variável do CQ que você pode mapear para uma propriedade do Adobe Analytics.

O nome dessas variáveis CQ usa o seguinte formato:

O sufixo XX é a porcentagem de duração da trilha que define o marco. Por exemplo, especificar porcentagens de 10, 25, 50 e 75 gera as seguintes variáveis CQ:

* `eventdata.events.milestone10`
* `eventdata.events.milestone25`
* `eventdata.events.milestone50`
* `eventdata.events.milestone75`

```shell
eventdata.events.milestoneXX
```

1. Depois de selecionar Etapas não herdadas como método de rastreamento, na caixa Rastrear deslocamento, insira uma lista separada por vírgulas de porcentagens de duração da faixa. Por exemplo, o valor padrão a seguir define marcos em 10, 25, 50 e 75% da duração da trilha:

   ```xml
   10,25,50,75
   ```

   Os valores de deslocamento devem ser números inteiros maiores que 0.

1. Para mapear as variáveis CQ para as propriedades do Adobe Analytics, arraste as propriedades do Adobe Analytics do ContentFinder ao lado da variável CQ no componente.

   Para obter informações sobre como otimizar os mapeamentos, consulte [Medição de vídeo no Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html) guia.

1. [Adicionar a estrutura](/help/sites-administering/adobeanalytics.md) para a página.
1. Para testar a configuração no **Modo de visualização**, reproduza o vídeo para obter as chamadas do Adobe Analytics para acionar o.

## Etapas herdadas {#legacy-milestones}

Este método é semelhante ao método de Marcos com a diferença de que os marcos especificados na variável *Deslocamento de rastreamento* são porcentagens em vez de pontos definidos no vídeo.

>[!NOTE]
>
>O campo Tracking offset aceita apenas uma lista separada por vírgulas contendo números inteiros entre 1 e 100.

1. Defina a opção Rastrear deslocamento.

   * por exemplo,10,50,75,100

   Além disso, as informações enviadas para o Adobe Analytics são menos personalizáveis. Há apenas três variáveis disponíveis para mapeamento:

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>As variáveis mapeadas para esse conterão a variável <strong>fácil de usar</strong> nome (<strong>Título</strong>) do vídeo se definido no DAM; se o Título não estiver definido, o nome do vídeo <strong>nome do arquivo</strong> será enviado. Enviado somente uma vez, no início da reprodução de um vídeo.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>As variáveis mapeadas para esse local conterão o nome do arquivo. Enviado somente uma vez, no início da reprodução de um vídeo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>A variável mapeada para este conterá o caminho do arquivo no servidor. Enviado somente uma vez, no início da reprodução de um vídeo.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>É possível definir as configurações de **fácil de usar** abrindo o vídeo para edição no DAM e definindo o parâmetro **Título** para o nome desejado. Também é necessário Salvar as alterações feitas ao concluir.

1. Mapear essas variáveis para props 1 a 3

   A variável **resto das informações relevantes** na chamada será enviada concatenada em **um** variável nomeada **pev3**.

   **Exemplos de chamadas** Para o Adobe Analytics usar o exemplo fornecido, deve ter esta aparência quando visualizado com o DigitalPulse Debugger:

   ![marcos1](assets/lmilestones1.png)

   *A variável **pev3**enviada na chamada contém as seguintes informações:*

   * *Nome* - O nome do arquivo de vídeo (*film.avi*)

   * *Length* - A duração do arquivo de vídeo, em segundos (*100*)

   * *Nome do player* - O reprodutor de vídeo usado para reproduzir o arquivo de vídeo (*vídeo HTML5*)

   * *Total de segundos reproduzidos* - O número total de segundos em que o vídeo foi reproduzido (*25*)

   * *Carimbo de data e hora inicial* - Carimbo de data e hora que identifica quando a reprodução do vídeo começou (*1331035567*)

   * *Reproduzir sessão* - Os detalhes da sessão de reprodução. Esse campo indica como o usuário interagiu com o vídeo. Isso pode incluir dados como onde começaram a reproduzir o vídeo, se usaram o controle deslizante do vídeo para avançar o vídeo e onde pararam de reproduzir o vídeo (*L10E24S58L58 - video was stopped at sec (O vídeo foi interrompido em segundos). 25 da seção L10, então ignorado para s. 48*)

## Segundos herdados {#legacy-seconds}

Ao usar o método** legacy seconds**, as chamadas do Adobe Analytics são acionadas a cada N-ésimo segundo, em que N é especificado no campo Track offset.

1. Defina o deslocamento da faixa para qualquer número de segundos,

   * por exemplo, 6

   >[!NOTE]
   >
   >O campo de deslocamento de Rastreamento aceita apenas números inteiros maiores que 0

   As informações enviadas para o Adobe Analytics são menos personalizáveis. Há apenas 3 variáveis disponíveis para mapeamento:

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>As variáveis mapeadas para esse conterão a variável <strong>fácil de usar</strong> nome (<strong>Título</strong>) do vídeo se definido no DAM; se o Título não estiver definido, o nome do vídeo <strong>nome do arquivo</strong> será enviado. Enviado somente uma vez, no início da reprodução de um vídeo.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>A variável mapeada para este conterá o nome do arquivo. Enviado somente uma vez, no início da reprodução de um vídeo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>A variável mapeada para este conterá o caminho do arquivo no servidor. Enviado somente uma vez, no início da reprodução de um vídeo.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>É possível definir as configurações de **fácil de usar** abrindo o vídeo para edição no DAM e definindo o parâmetro **Título** para o nome desejado. Também é necessário Salvar as alterações feitas ao concluir.

1. Mapear essas variáveis para prop1, prop2 e prop3

   A variável **resto das informações relevantes** na chamada será enviado concatinado em **um** variável nomeada **pev3**.

   As chamadas para o Adobe Analytics usando o exemplo fornecido devem ter esta aparência quando visualizadas com o DigitalPulse Debugger:

   ![lseconds](assets/lseconds.png)

   *A chamada é semelhante à chamada de Marcos herdados acima. Consulte as informações em pev3 **[fornecido lá](/help/sites-administering/adobeanalytics.md)**.*

**Referências usadas neste tutorial:**

[0] [https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html)
