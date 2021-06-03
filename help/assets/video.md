---
title: Vídeo no Dynamic Media
description: Saiba como trabalhar com vídeo no Dynamic Media
uuid: 97f311a3-a227-479a-91bf-fb54ecd1a55d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 1103b849-0042-4e11-b170-38ee81dd0157
docset: aem65
feature: Gerenciamento de ativos
role: Business Practitioner, Administrator
exl-id: 28cf9e39-cab4-4278-b6c9-e84cc31964db
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '11748'
ht-degree: 7%

---

# Vídeo no Dynamic Media {#video}

Esta seção descreve como trabalhar com vídeo no Dynamic Media.

## Início rápido: Vídeos {#quick-start-videos}

A seguinte descrição passo a passo do fluxo de trabalho foi criada para ajudá-lo a ativar e executar rapidamente com conjuntos de vídeos adaptáveis no Dynamic Media. Após cada etapa, são referências cruzadas a títulos de tópico, onde você pode encontrar mais informações.

>[!NOTE]
>
>Antes de trabalhar com vídeo no Dynamic Media, verifique se o administrador do AEM já ativou e configurou o Dynamic Media Cloud Services no modo Dynamic Media - Scene7 ou Dynamic Media - Modo híbrido.
>
>* Consulte [Configuração do Dynamic Media Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) em Configuração do Dynamic Media - Modo Scene7 e [Solução de problemas do Dynamic Media - Modo Scene7.](/help/assets/troubleshoot-dms7.md)
   >
   >
* Consulte [Configuração do Dynamic Media Cloud Services](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services) em Configuração do Dynamic Media - Modo híbrido.

>



1. **Faça o upload de seus** vídeos do Dynamic Media fazendo o seguinte:

   * Crie seu próprio perfil de codificação de vídeo. Ou você pode simplesmente usar o perfil predefinido _Adaptive Video Encoding_ que vem com o Dynamic Media.

      * [Criação de um perfil de codificação de vídeo](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * Saiba mais sobre [Práticas recomendadas para codificação de vídeo](#best-practices-for-encoding-videos).
   * Associe o perfil de processamento de vídeo a uma ou mais pastas, onde você fará upload dos vídeos de origem primária.

      * [Aplicar um perfil de vídeo a pastas](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).
      * Saiba mais sobre as [Práticas recomendadas para organizar ativos digitais para usar perfis de processamento](/help/assets/organize-assets.md).
      * Saiba mais sobre [Organização de ativos digitais](/help/assets/organize-assets.md).
   * Faça upload dos vídeos de origem primária para as pastas. Você pode fazer upload de arquivos de vídeo com até 15 GB cada. Ao adicionar vídeos à pasta, eles são codificados de acordo com o perfil de processamento de vídeo atribuído à pasta.

      * [Carregue seus vídeos](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).
      * Saiba mais sobre [Formatos de arquivo de entrada compatíveis](/help/assets/assets-formats.md#supported-multimedia-formats).
   * Monitore como a [codificação de vídeo está progredindo](#monitoring-video-encoding-and-youtube-publishing-progress) a partir do ativo ou da visualização de fluxo de trabalho.




1. **Gerencie seus** vídeos do Dynamic Media seguindo um destes procedimentos:

   * Organizar, navegar e pesquisar ativos de vídeo

      * [Organizar ](/help/assets/organize-assets.md)
ativos digitaisSaiba mais sobre as práticas  [recomendadas para organizar ativos digitais para usar perfis de processamento](organize-assets.md)

      * [Pesquisar ](search-assets.md#custompredicates) ativos de vídeo ou  [pesquisar ativos](/help/assets/search-assets.md)
   * Visualizar e publicar ativos de vídeo

      * Visualize o vídeo de origem e as representações codificadas do vídeo, juntamente com as miniaturas associadas:
         [Visualização ](managing-video-assets.md#upload-and-preview-video-assets) de vídeos ou  [visualização de ativos](previewing-assets.md)
         [Exibição de representações de vídeo](video-renditions.md)
         [Gerenciamento de representações de vídeo](manage-assets.md#managing-renditions)

      * [Gerenciar predefinições do visualizador](managing-viewer-presets.md)
      * [Publicação de ativos](publishing-dynamicmedia-assets.md)
   * Trabalhar com metadados de vídeo

      * Visualize as propriedades de uma representação de vídeo codificado, como taxa de quadros, taxa de bits de áudio e vídeo e codec:
         [Exibir propriedades de representação de vídeo](video-renditions.md)

      * Edite as propriedades do vídeo, como título, descrição e tags, e os campos de metadados personalizados:
         [Edição de propriedades do vídeo](manage-assets.md#editing-properties)

      * [Gerenciamento de metadados para ativos digitais](metadata.md)
      * [Esquemas de metadados](metadata-schemas.md)
   * Revisar, aprovar e anotar vídeos e manter o controle total da versão

      * [Anotação de ](managing-video-assets.md#annotate-video-assets) vídeos ou  [Anotação de ativos](manage-assets.md#annotating)

      * [Criar uma versão](manage-assets.md#asset-versioning)
      * [Aplicar fluxos de trabalho a ](assets-workflow.md) ativos ou consultar  [Iniciar um fluxo de trabalho em um ativo](manage-assets.md#starting-a-workflow-on-an-asset)

      * [Revisar ativos da pasta](bulk-approval.md)
      * [Projetos](../sites-authoring/projects.md)




1. **Publique seus** vídeos do Dynamic Media seguindo um destes procedimentos:

   * Se você estiver usando o Adobe Experience Manager como seu sistema de gerenciamento de conteúdo da Web, poderá adicionar vídeos diretamente às suas páginas da Web.

      * [Adicionar vídeos às suas páginas da Web](adding-dynamic-media-assets-to-pages.md).
   * Se você estiver usando um sistema de gerenciamento de conteúdo da Web de terceiros, poderá vincular ou incorporar vídeos às suas páginas da Web.

      * Integrar vídeo usando URL:
         [Vincular URLs do ao aplicativo da Web](linking-urls-to-yourwebapplication.md).

      * Integre o vídeo usando o código incorporado na página da Web:
         [Incorporação do visualizador de vídeo em uma página da Web](embed-code.md).
   * [Publicação de vídeos no YouTube](#publishing-videos-to-youtube).
   * [Geração de relatórios de vídeo](#viewing-video-reports).

   * [Adição de legendas ao vídeo](#adding-captions-to-video).



## Trabalhar com vídeo no Dynamic Media {#working-with-video-in-dynamic-media}

O vídeo no Dynamic Media é uma solução completa que facilita a publicação de vídeo adaptável de alta qualidade para transmissão em várias telas, incluindo dispositivos móveis para desktop, iOS, Android, Blackberry e Windows. Um Conjunto de vídeos adaptáveis agrupa versões do mesmo vídeo codificadas em diferentes formatos e taxas de bits, como 400 kbps, 800 kbps e 1000 kbps. O computador desktop ou dispositivo móvel detecta a largura de banda disponível.

Por exemplo, em um dispositivo móvel iOS, ele detecta uma largura de banda como 3G, 4G ou Wi-Fi. Em seguida, ele seleciona automaticamente o vídeo codificado direito dentre as várias taxas de bits de vídeo no Conjunto de vídeos adaptáveis. O vídeo é transmitido em desktops, dispositivos móveis ou tablets.

Além disso, a qualidade do vídeo é alternada dinamicamente automaticamente se as condições da rede mudarem no desktop ou no dispositivo móvel. Além disso, se um cliente entrar no modo de tela cheia em um desktop, o Adaptive Video Set responde usando uma resolução melhor, melhorando assim a experiência de visualização do cliente. O uso de conjuntos de vídeos adaptáveis fornece a melhor reprodução possível para os clientes que reproduzem o vídeo do Dynamic Media em várias telas e dispositivos.

A lógica usada por um reprodutor de vídeo para determinar qual vídeo codificado reproduzir ou selecionar durante a reprodução é baseada no seguinte algoritmo:

1. O reprodutor de vídeo carrega o fragmento de vídeo inicial com base na taxa de bits mais próxima do valor definido para &quot;taxa de bits inicial&quot; no próprio reprodutor.
1. O reprodutor de vídeo é alternado com base em alterações na velocidade da largura de banda usando os seguintes critérios:

   1. O reprodutor escolhe o fluxo de largura de banda mais alto abaixo ou igual à largura de banda estimada.
   1. O Player considera apenas 80% da largura de banda disponível. No entanto, se estiver mudando, é mais conservador em apenas 70% para evitar sobrestimações e imediatamente voltar.

Para obter informações técnicas detalhadas sobre o algoritmo, consulte [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

Para gerenciar vídeos únicos e conjuntos de vídeos adaptáveis, o seguinte é suportado:

* Upload de vídeo de vários formatos de vídeo e formatos de áudio suportados e codificação de vídeo para o formato MP4 H.264 para reprodução em várias telas. Você pode usar predefinições de vídeo adaptável predefinidas, predefinições de codificação de vídeo único ou personalizar sua própria codificação para controlar a qualidade e o tamanho do vídeo.

   * Quando um conjunto de vídeo adaptável é gerado, ele inclui vídeos MP4.
   * **Observação**: Vídeos principais/de origem não são adicionados a um Conjunto de vídeos adaptáveis.

* Legenda de vídeo em todos os visualizadores de vídeo HTML5.
* Organize, navegue e pesquise vídeos com suporte completo a metadados para o gerenciamento eficiente dos ativos de vídeo.
* Forneça Conjuntos de Vídeos Adaptativos para a Web, bem como para desktops e dispositivos móveis, incluindo iPhone, iPad, Android, Blackberry e Windows phone.

O streaming de vídeo adaptável é compatível com diversas plataformas iOS. Consulte [Guia de Referência de Visualizadores do Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html#video).

O Dynamic Media oferece suporte para reprodução de vídeo móvel para vídeo MP4 H.264. Você pode encontrar dispositivos Blackberry que suportam esse formato de vídeo no seguinte endereço: [Formatos de vídeo suportados no Blackberry](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

Você pode encontrar dispositivos Windows compatíveis com este formato de vídeo no seguinte endereço: [Formatos de vídeo suportados no Windows Phone](https://msdn.microsoft.com/library/windows/apps/ff462087%28v=vs.105%29.aspx)

* Reproduzir o vídeo usando as Predefinições do visualizador de vídeo do Dynamic Media, incluindo o seguinte:

   * Visualizadores de vídeo individuais.
   * Visualizadores de mídia mista que combinam conteúdo de vídeo e imagem.

* Configure players de vídeo para atender às suas necessidades de marca.
* Integre vídeo ao seu site, site móvel ou aplicativo móvel com um URL simples ou código incorporado.

<!-- See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample. -->

Consulte também [Visualizadores do AEM Assets e Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) e [Visualizadores de ativos AEM somente](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

## Prática recomendada: Uso do visualizador de vídeo HTML5 {#best-practice-using-the-html-video-viewer}

As predefinições do visualizador de vídeo HTML5 do Dynamic Media são players de vídeo robustos. Você pode usá-los para evitar muitos problemas comuns associados à reprodução de vídeo HTML5 e problemas associados a dispositivos móveis, como falta de entrega de transmissão adaptável e alcance limitado do navegador do desktop.

No lado do design do reprodutor, é possível projetar toda a funcionalidade do reprodutor de vídeo usando ferramentas de desenvolvimento da Web padrão. Por exemplo, você pode projetar os botões, controles e o plano de fundo personalizado da imagem de pôster usando HTML5 e CSS para ajudar você a alcançar seus clientes com uma aparência personalizada.

No lado da reprodução do visualizador, ele detecta automaticamente o recurso de vídeo do navegador. Em seguida, ele serve o vídeo usando HLS (HTTP Live Streaming), também conhecido como streaming de vídeo adaptável. Ou, se esses métodos de delivery não estiverem presentes, o HTML5 progressivo será usado.

Ao combinar em um único reprodutor a capacidade de projetar os componentes de reprodução usando HTML5 e CSS, ter reprodução incorporada e usar streaming adaptável e progressivo, dependendo da capacidade do navegador, você estende o alcance do conteúdo de mídia avançada para usuários de desktop e móveis e garante uma experiência de vídeo simplificada.

Consulte também [Sobre visualizadores HTML5](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

### Reprodução de vídeo em computadores desktop e dispositivos móveis usando o visualizador de vídeo HTML5 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

Para streaming de vídeo adaptável para desktop e dispositivos móveis, os vídeos usados para alternância de taxa de bits são baseados em todos os vídeos MP4 no Adaptive Video Set.

A reprodução de vídeo ocorre usando HLS ou o download de vídeo progressivo. Em versões anteriores do AEM, como 6.0, 6.1 e 6.2, os vídeos eram transmitidos via HTTP.

No entanto, no AEM 6.3 e mais, os vídeos agora são transmitidos por HTTPS (ou seja, HLS), pois o URL do serviço de gateway do DM sempre usa HTTPS também. Observe que não há impacto do cliente nesse comportamento padrão. Ou seja, o streaming de vídeo sempre ocorrerá por HTTPS, a menos que não seja suportado pelo navegador. (ver quadro seguinte). Portanto,

* Se você tiver um site HTTPS com streaming de vídeo HTTPS, o streaming estará bom.
* Se você tiver um site HTTP com streaming de vídeo HTTPS, o streaming estará correto e não haverá problemas de conteúdo misto no navegador da Web.

O HLS é um padrão da Apple para streaming de vídeo adaptável que ajusta automaticamente a reprodução com base na capacidade da largura de banda da rede. Ele também permite que o cliente &quot;procure&quot; em qualquer ponto do vídeo, sem precisar aguardar o download do restante do vídeo.

O vídeo progressivo é fornecido pelo download e armazenamento local do vídeo no sistema de desktop de um usuário ou dispositivo móvel.

A tabela a seguir descreve o dispositivo, o navegador e o método de reprodução de vídeos em computadores desktop e dispositivos móveis usando o Dynamic Media Video Viewer.

<table>
 <tbody>
  <tr>
   <td><strong>Device</strong></td>
   <td><strong>Navegador</strong></td>
   <td><strong>Modo de reprodução de vídeo</strong></td>
  </tr>
  <tr>
   <td>Área de trabalho</td>
   <td>Internet Explorer 9 e 10</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Área de trabalho</td>
   <td>Internet Explorer 11+</td>
   <td>No Windows 8 e no Windows 10 - Forçar o uso de HTTPS sempre que HLS for solicitado. Limitação conhecida: HTTP no HLS não funciona nesta combinação de navegador/sistema operacional<br /> <br /> No Windows 7 - Download progressivo. Usa a lógica padrão para selecionar o protocolo HTTP versus HTTPS.</td>
  </tr>
  <tr>
   <td>Área de trabalho</td>
   <td>Firefox 23-44</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Área de trabalho</td>
   <td>Firefox 45 ou superior</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Área de trabalho</td>
   <td>Cromo</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Área de trabalho</td>
   <td>Safari (Mac)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Móvel</td>
   <td>Chrome (Android 6 ou anterior)</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Móvel</td>
   <td>Chrome (Android 7 ou posterior)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Móvel</td>
   <td>Android (navegador padrão)</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Móvel</td>
   <td>Safari (iOS)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Móvel</td>
   <td>Chrome (iOS)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Móvel</td>
   <td>Blackberry</td>
   <td>HLS</td>
  </tr>
 </tbody>
</table>

## Arquitetura da solução de vídeo Dynamic Media {#architecture-of-dynamic-media-video-solution}

O gráfico a seguir mostra o fluxo de trabalho de criação geral de vídeos que são carregados e codificados por meio do DMGgateway (no modo Dynamic Media Hybrid) e disponibilizados para consumo público.

![chlimage_1-427](assets/chlimage_1-427.png)

## Arquitetura de publicação híbrida para vídeos {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## Práticas recomendadas para codificação de vídeos {#best-practices-for-encoding-videos}

O fluxo de trabalho **Codificação de vídeo do Dynamic Media** codifica o vídeo se você tiver ativado o Dynamic Media e configurado os serviços da nuvem de vídeo. Esse fluxo de trabalho captura o histórico do processo de fluxo de trabalho e as informações de falha. Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress). Se você ativou o Dynamic Media e configurou serviços de nuvem de vídeo, o fluxo de trabalho **[!UICONTROL Codificação de vídeo do Dynamic Media]** entrará em vigor automaticamente ao carregar um vídeo. (Se você não estiver usando o Dynamic Media, o fluxo de trabalho **[!UICONTROL Ativo de atualização do DAM]** entrará em vigor.)

A seguir estão dicas de práticas recomendadas para a codificação de arquivos de vídeo de origem.

Para obter conselhos sobre a codificação de vídeo, consulte o seguinte:

* [Streaming 101: Noções básicas — Codecs, Largura de banda, Taxa de dados e Resolução](https://www.adobe.com/go/learn_s7_streaming101_en).
* [Noções básicas sobre codificação de vídeo](https://www.adobe.com/go/learn_s7_encoding_en).

### Arquivos de vídeo de origem {#source-video-files}

Ao codificar um arquivo de vídeo, use um arquivo de vídeo de origem com a maior qualidade possível. Evite usar arquivos de vídeo previamente codificados, pois esses arquivos já estão compactados, e uma codificação adicional criará um vídeo de qualidade inferior.

A tabela a seguir descreve o tamanho recomendado, a proporção e a taxa mínima de bits que seus arquivos de vídeo de origem devem ter antes de codificá-los:

| Tamanho | Taxa de proporção | Taxa mínima de bits |
|--- |--- |--- |
| 1024 X 768 | 4:3 | 4500 kbps para a maioria dos vídeos. |
| 1280 X 720 | 16:9 | 3000 - 6000 kbps, dependendo da quantidade de movimento no vídeo. |
| 1920 X 1080 | 16:99 | 6000 - 8000 kbps, dependendo da quantidade de movimento no vídeo. |

### Obter os metadados de um arquivo {#obtaining-a-file-s-metadata}

Você pode obter os metadados de um arquivo ao visualizar seus metadados usando uma ferramenta de edição de vídeo ou um aplicativo projetado para obter metadados. A seguir estão as instruções para usar MediaInfo, um aplicativo de terceiros, para obter os metadados de um arquivo de vídeo:

1. Vá para esta página da Web: [https://mediainfo.sourceforge.net/en/Download](https://mediainfo.sourceforge.net/en/Download).
1. Selecione e baixe o instalador da versão da GUI e siga as instruções de instalação.
1. Após a instalação, clique com o botão direito do mouse no arquivo de vídeo (somente Windows) e selecione MediaInfo ou abra MediaInfo e arraste o arquivo de vídeo para o aplicativo. Você verá todos os metadados associados ao arquivo de vídeo, incluindo largura, altura e fps.

### Taxa de proporção {#aspect-ratio}

Ao escolher ou criar uma predefinição de codificação de vídeo para o arquivo de vídeo de origem primária, certifique-se de que a predefinição tenha a mesma proporção de aspecto do arquivo de vídeo de origem primária. A proporção é a relação entre a largura e a altura do vídeo.

Para determinar a proporção de um arquivo de vídeo, obtenha os metadados do arquivo e anote a largura e a altura do arquivo (consulte Obter os metadados de um arquivo acima). Em seguida, use essa fórmula para determinar a proporção:

largura/altura = proporção

A tabela a seguir descreve como os resultados da fórmula são traduzidos para opções comuns de proporção:

| Resultado da fórmula | Taxa de proporção |
|--- |--- |
| 1,33 | 4:3 |
| 0,75 | 3:4 |
| 1,78 | 16:99 |
| 0,56 | 9:16 |

Por exemplo, um vídeo com 1440 largura x 1080 altura tem uma proporção largura/altura de 1440/1080 ou 1,33. Nesse caso, você escolhe uma predefinição de codificação de vídeo com uma proporção de aspecto 4:3 para codificar o arquivo de vídeo.

### Taxa de bits {#bitrate}

A taxa de bits é a quantidade de dados codificada para formar um único segundo de reprodução de vídeo. A taxa de bits é medida em kilobits por segundo (Kbps).

>[!NOTE]
>
>Como todos os codecs usam compactação com perdas, a taxa de bits é o fator mais importante na qualidade do vídeo. Com a compactação com perdas, quanto mais você compacta um arquivo de vídeo, mais a qualidade é degradada. Por isso, todas as outras características são iguais (resolução, taxa de quadros e codec), quanto menor a taxa de bits, menor a qualidade do arquivo compactado.

Ao selecionar uma codificação de taxa de bits, você pode escolher dois tipos:

* **[!UICONTROL Codificação]**  constante da taxa de bits (CBR) - Durante a codificação de CBR, a taxa de bits ou o número de bits por segundo é mantido o mesmo durante todo o processo de codificação. A codificação CBR mantém a taxa de dados definida para sua configuração durante todo o vídeo. Além disso, a codificação CBR não otimiza arquivos de mídia para qualidade, mas salva no espaço de armazenamento.
Use o CBR se o vídeo contiver um nível de movimento semelhante em todo o vídeo. O CBR é mais usado para transmissão de conteúdo de vídeo. Consulte também [Usar parâmetros de codificação de vídeo personalizados](/help/assets/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL Codificação]**  da taxa de bits variável (VBR) - A codificação VBR ajusta a taxa de dados para baixo e para o limite superior definido, com base nos dados exigidos pelo compressor. Isso significa que, durante um processo de codificação VBR, a taxa de bits do arquivo de mídia aumenta ou diminui dinamicamente, dependendo das necessidades de taxa de bits dos arquivos de mídia.
O VBR demora mais para codificar, mas produz os resultados mais favoráveis; a qualidade do arquivo de mídia é superior. O VBR é usado mais frequentemente para entrega progressiva de conteúdo de vídeo em http.

Quando você deve usar o VBR versus o CRB?
Quando se trata de selecionar VBR versus CBR, quase sempre é recomendável usar VBR para seus arquivos de mídia. O VBR fornece arquivos de maior qualidade a taxas de bits competitivas. Ao usar o VBR, certifique-se de usar com a codificação de duas etapas e definir a taxa de bits máxima para ser 1,5x a taxa de bits do vídeo de destino.

Ao escolher uma predefinição de codificação de vídeo, considere a velocidade de conexão do usuário final de destino. Escolha uma predefinição com uma taxa de dados de 80% dessa velocidade. Por exemplo, se a velocidade de conexão do usuário final de destino for 1000 Kbps, a melhor predefinição é aquela com uma taxa de dados de vídeo de 800 Kbps.

Esta tabela descreve a taxa de dados de velocidades de conexão típicas.

| Velocidade (Kbps) | Tipo de conexão |
|--- |--- |
| 256 | Conexão discada. |
| 800 | Conexão móvel típica. Para essa conexão, direcione uma taxa de dados no intervalo de 400 a um máximo de 800 para experiências 3G. |
| 2000 | Conexão típica de desktop de banda larga. Para esta conexão, direcione uma taxa de dados no intervalo de 800-2000 Kbps, com a maioria dos destinos com média de 1200-1500 Kbps. |
| 5000 | Conexão típica de alta banda larga. A codificação nesse intervalo superior não é recomendada porque a entrega de vídeo nessa velocidade não está disponível para a maioria dos consumidores. |

### Resolução {#resolution}

**Resolução **descreve a altura e a largura de um arquivo de vídeo em pixels. A maioria dos vídeos de origem é armazenada em alta resolução (por exemplo, 1920 x 1080). Para fins de transmissão, o vídeo de origem é compactado em uma resolução menor (640 x 480 ou menor).

A resolução e a taxa de dados são dois fatores totalmente vinculados que determinam a qualidade do vídeo. Para manter a mesma qualidade de vídeo, quanto maior o número de pixels em um arquivo de vídeo (quanto maior a resolução), maior deverá ser a taxa de dados. Por exemplo, considere o número de pixels por quadro em uma resolução de 320 x 240 e um arquivo de vídeo de resolução de 640 x 480:

| Resolução | Pixels por quadro |
|--- |--- |
| 320 x 240 | 76 800 |
| 640 x 480 | 307 200 |

O arquivo de 640 x 480 tem quatro vezes mais pixels por quadro. Para atingir a mesma taxa de dados para essas duas resoluções de exemplo, aplique quatro vezes a compactação no arquivo 640 x 480, o que pode reduzir a qualidade do vídeo. Portanto, uma taxa de dados de vídeo de 250 Kbps produz uma exibição de alta qualidade com uma resolução de 320 x 240, mas não com resolução de 640 x 480.

Em geral, quanto maior for a taxa de dados, melhor será a aparência do vídeo e maior será a resolução usada, maior será a taxa de dados necessária para manter a qualidade de exibição (em comparação com resoluções mais baixas).

Como a resolução e a taxa de dados estão vinculadas, você tem duas opções ao codificar o vídeo:

* Escolha uma taxa de dados e, em seguida, codifique na resolução mais alta que fique boa na taxa de dados escolhida.
* Escolha uma resolução e, em seguida, codifique na taxa de dados necessária para obter vídeo de alta qualidade na resolução escolhida.

Ao escolher (ou criar) uma predefinição de codificação de vídeo para o arquivo de vídeo de origem primária, use esta tabela para direcionar a resolução correta:

| Resolução | Altura (pixels) | Tamanho da tela |
|--- |--- |--- |
| 240p | 240 | Tela pequena |
| 300p | 300 | Tela pequena normalmente para dispositivos móveis |
| 360p | 360 | Tela pequena |
| 480p | 480 | Tela média |
| 720p | 720 | Tela grande |
| 1080p | 1080 | Tela grande de alta definição |

### Fps (Quadros por segundo) {#fps-frames-per-second}

Nos Estados Unidos e Japão, a maioria dos vídeos é capturada a 29,97 quadros por segundo (fps); na Europa, a maioria dos vídeos é filmada a 25 fps. O filme é filmado a 24 fps.

Escolha uma predefinição de codificação de vídeo que corresponda à taxa fps do arquivo de vídeo de origem primária. Por exemplo, se o vídeo de origem primária for 25 fps, escolha uma predefinição de codificação com 25 fps. Por padrão, toda codificação personalizada usa o fps do arquivo de vídeo de origem primária. Por isso, não é necessário especificar explicitamente a configuração fps ao criar uma predefinição de codificação de vídeo.

### Dimensões de codificação de vídeo {#video-encoding-dimensions}

Para obter resultados ideais, selecione dimensões de codificação de modo que o vídeo de origem seja um múltiplo completo de todos os vídeos codificados.

Para calcular essa proporção, você divide a largura da origem por largura codificada para obter a relação de largura. Em seguida, divida a altura da origem por altura codificada para obter a proporção de altura.

Se a proporção resultante for um inteiro, significa que o vídeo é dimensionado de maneira ideal. Se a proporção resultante não for um inteiro, ela afetará a qualidade do vídeo, deixando artefatos de pixel à esquerda na exibição. Esse efeito é mais notável quando o vídeo tem texto.

Por exemplo, suponha que o vídeo de origem seja 1920 x 1080. Na tabela a seguir, os três vídeos codificados fornecem as configurações de codificação ideais para usar.

| Tipo de vídeo | Largura x altura | Proporção de largura | Taxa de altura |
|--- |--- |--- |--- |
| Origem | 1920x1080 | 1 | 1 |
| Codificado | 960 x 540 | 2 | 2 |
| Codificado | 640 x 360 | 3 | 1 |
| Codificado | 480 x 270 | 4 | 4 |

### Formato de arquivo de vídeo codificado {#encoded-video-file-format}

A Dynamic Media recomenda usar predefinições de codificação de vídeo MP4 H.264. Como os arquivos MP4 usam o codec de vídeo H.264, ele fornece vídeo de alta qualidade, mas em um tamanho de arquivo compactado.

## Publicar vídeos no YouTube {#publishing-videos-to-youtube}

Você pode publicar ativos de vídeo no local AEM diretamente em um canal do YouTube criado anteriormente.

Para publicar ativos de vídeo no YouTube, configure o AEM Assets com tags. Você associa essas tags a um canal YouTube. Se a tag de um ativo de vídeo corresponder à tag de um canal de YouTube, o vídeo será publicado no YouTube. Publicar no YouTube ocorre junto com uma publicação normal do vídeo, desde que uma tag associada seja usada.

O YouTube faz sua própria codificação. Dessa forma, o arquivo de vídeo original que foi carregado no AEM é publicado no YouTube em vez de qualquer representação de vídeo criada pela codificação do Dynamic Media. Embora não seja necessário processar vídeos usando o Dynamic Media, espera-se que eles o façam caso uma predefinição do visualizador seja necessária para reprodução.

Ao ignorar o perfil de processamento de vídeo e publicar diretamente no YouTube, isso significa apenas que o ativo de vídeo no AEM Asset pode não obter uma miniatura visualizável. Isso também significa que, se você executar nos modos de execução dynamicmedia ou dynamicmedia_scene7, os vídeos que não estiverem codificados não funcionarão com nenhum dos tipos de ativos Dynamic Media.

A publicação de ativos de vídeo em servidores da YouTube envolve a conclusão das seguintes tarefas para garantir a autenticação segura de servidor para servidor com o YouTube:

1. [Definição das configurações do Google Cloud](#configuring-google-cloud-settings)
1. [Criação de um canal YouTube](#creating-a-youtube-channel)
1. [Adição de tags para publicação](#adding-tags-for-publishing)
1. [Ativação do agente de Replicação de Publicação do YouTube](#enabling-the-youtube-publish-replication-agent)
1. [Configuração do YouTube no AEM](#setting-up-youtube-in-aem)
1. [(Opcional) Automatização da configuração das propriedades padrão do YouTube para os vídeos enviados por upload](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [Publicar vídeos no seu canal do YouTube](#publishing-videos-to-your-youtube-channel)
1. [(Opcional) Verificação do vídeo publicado no YouTube](/help/assets/video.md#optional-verifying-the-published-video-on-youtube)
1. [Vincular URLs do YouTube ao seu aplicativo web](#linking-youtube-urls-to-your-web-application)

Você também pode [cancelar a publicação de vídeos para removê-los do YouTube](#unpublishing-videos-to-remove-them-from-youtube).

### Definição das configurações do Google Cloud {#configuring-google-cloud-settings}

Para publicar no YouTube, você precisa de uma conta do Google. Se tiver uma conta GMAIL, você já tem uma conta do Google; se você não tiver uma conta do Google, poderá criar uma facilmente. Você precisa da conta, pois precisa de credenciais para publicar ativos de vídeo no YouTube. Se você tiver uma conta já criada, ignore esta tarefa e prossiga diretamente para [Criação de um canal YouTube](#creating-a-youtube-channel).

A conta usada com o Google Cloud e a conta do Google usada para o YouTube não precisam ser a mesma.

Esteja ciente de que o Google altera periodicamente a interface do usuário. Dessa forma, as etapas para publicar vídeos no YouTube podem variar um pouco do que está documentado abaixo. Esse aviso também se aplica ao YouTube quando você tenta verificar se os vídeos foram carregados nele.

>[!NOTE]
>
>As etapas a seguir foram precisas no momento da escrita. No entanto, o Google atualiza periodicamente seus sites sem aviso prévio. Como tal, essas etapas podem ser um pouco diferentes.

Para definir as configurações da Google Cloud:

1. Crie uma nova conta do Google.
   [https://accounts.google.com/SignUp?service=mail](https://accounts.google.com/SignUp?service=mail)

   Se você já tiver uma conta do Google, pule para a próxima etapa.

1. Vá para [https://cloud.google.com/](https://cloud.google.com/).
1. Na página do Google Cloud, próximo ao canto superior direito, clique em **[!UICONTROL Console]**.

   Se necessário, talvez seja necessário **[!UICONTROL Fazer logon]** usando suas credenciais de conta do Google para ver a opção **[!UICONTROL Console]**.

1. Na página Painel , à direita de **[!UICONTROL Google Cloud Platform]**, clique na lista suspensa Projeto para abrir a caixa de diálogo Selecionar um projeto .
1. Na caixa de diálogo Selecionar um projeto , toque em **[!UICONTROL Novo projeto]**.

   ![6_5_googleaccount-newproject](assets/6_5_googleaccount-newproject.png)

1. Na caixa de diálogo Novo projeto , no campo Nome do projeto , digite o nome do novo projeto.

   Observe que a ID do projeto se baseia no nome do projeto. Como tal, escolha cuidadosamente o nome do projeto; ele não pode ser alterado após ser criado. Além disso, será necessário inserir a mesma ID de projeto novamente ao configurar o YouTube AEM posteriormente; talvez você queira anotá-lo.

1. Clique em **[!UICONTROL Criar]**.

1. Siga um destes procedimentos:

   * No Painel do projeto, no cartão Introdução , toque em **[!UICONTROL Explorar e habilite as APIs]**.
   * No Painel do projeto, no cartão APIs , toque em **[!UICONTROL Ir para a visão geral das APIs]**.

   ![6_5_googleaccount-apis-enable2](assets/6_5_googleaccount-apis-enable2.png)

1. Próximo à parte superior da página APIs e serviços, toque em **[!UICONTROL Ativar APIs e serviços]**.
1. Na página Biblioteca de API, no lado esquerdo, em **[!UICONTROL Categoria]**, toque em **[!UICONTROL YouTube]**. No lado direito da página, toque em **[!UICONTROL YouTube Data API]**.
1. Na página API de dados do YouTube v3 , toque em **[!UICONTROL Ativar]**.

   ![6_5_googleaccount-apis-enable3](assets/6_5_googleaccount-apis-enable3.png)

1. Para usar a API, talvez você precise de credenciais. Se necessário, clique em **[!UICONTROL Criar Credenciais]**.

   ![6_5_googleaccount-apis-createcredentials](assets/6_5_googleaccount-apis-createcredentials.png)

1. Na página **[!UICONTROL Adicionar credenciais ao projeto]**, etapa 1, faça o seguinte:

   * No **[!UICONTROL Qual API você está usando?]** na lista suspensa, selecione  **[!UICONTROL YouTube Data API v3]**.

   * Em **[!UICONTROL De onde você chamará a API?]** na lista suspensa, selecione  **[!UICONTROL Web Server (por exemplo, node.js, Tomcat)]**

   * No **[!UICONTROL Que dados você acessará?]** na lista suspensa, toque em Dados  **[!UICONTROL do usuário]**.

   ![6_5_googleaccount-apis-createcredentials2](assets/6_5_googleaccount-apis-createcredentials2.png)

1. Toque em **[!UICONTROL Quais credenciais são necessárias?]**
1. Na página **[!UICONTROL Adicionar credenciais ao projeto]**, etapa 2, no cabeçalho **[!UICONTROL Criar uma ID de cliente do OAuth 2.0]**, no campo Nome, digite um nome exclusivo, se desejar. Ou você pode usar o nome padrão especificado pelo Google.
1. No cabeçalho **[!UICONTROL Authorized Javascript origins]** , no campo de texto, digite o seguinte caminho, substituindo seu próprio domínio e número de porta no caminho, e pressione **[!UICONTROL Enter]** para adicionar o caminho à lista:

   `https://<servername.domain>:<port_number>`

   Por exemplo, `https://1a2b3c.mycompany.com:4321`

   **Observação**: O exemplo de caminho acima destina-se apenas a fins ilustrativos.

   ![6_5_googleaccount-apis-createcredentials-oauth](assets/6_5_googleaccount-apis-createcredentials-oauth.png)

1. No cabeçalho **[!UICONTROL Authorized redirect URIs]**, no campo de texto, digite o seguinte caminho, substituindo seu próprio domínio e número da porta no caminho, e pressione **[!UICONTROL Enter]** para adicionar o caminho à lista:

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   Por exemplo, `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   **Observação**: O exemplo de caminho acima destina-se apenas a fins ilustrativos.

1. Clique em **[!UICONTROL Criar ID de cliente OAuth]**.
1. Na página **[!UICONTROL Adicionar credenciais ao projeto]**, etapa 3, no cabeçalho **[!UICONTROL Configurar a tela de consentimento do OAuth 2.0]**, selecione o endereço de email do Gmail que você está usando no momento.

   ![6_5_googleaccount-apis-createcredentials-consent-tela de consentimento](assets/6_5_googleaccount-apis-createcredentials-consentscreen.png)

1. No cabeçalho **[!UICONTROL Product name displayed to users]** , no campo de texto, insira o que deseja mostrar na tela de consentimento.

   A tela de consentimento é exibida para o administrador do AEM quando eles são autenticados para o YouTube; AEM entrará em contato com a YouTube para obter permissão.

1. Clique em **[!UICONTROL Continuar]**.
1. Na página Adicionar credenciais ao projeto, etapa 4, no cabeçalho **[!UICONTROL Baixar credenciais]**, toque em **[!UICONTROL Download]**.

   ![6_5_googleaccount-apis-createcredentials-downloadcredentials](assets/6_5_googleaccount-apis-createcredentials-downloadcredentials.png)

1. Salve o arquivo `client_id.json`.

   Você precisará desse arquivo json baixado ao configurar o YouTube no Adobe Experience Manager posteriormente.

1. Clique em **[!UICONTROL Concluído]**.

   Faça logoff de sua conta do Google. Agora você criará um canal YouTube.

### Criação de um canal YouTube {#creating-a-youtube-channel}

A publicação de vídeos no YouTube requer um ou mais canais. Se você já criou um canal YouTube, pode ignorar esta tarefa e acessar [Adição de tags para publicação](/help/assets/video.md#adding-tags-for-publishing).

>[!CAUTION]
>
>Certifique-se de que você já configurou um ou mais canais no YouTube *antes de* adicionar canais em Configurações do YouTube em AEM (consulte [Configuração do YouTube no AEM](#setting-up-youtube-in-aem) abaixo). Se você não conseguir fazer isso, não receberá nenhum aviso de nenhum canal existente. No entanto, a autenticação do Google ainda ocorre ao adicionar um canal, mas não há uma opção para escolher qual canal o vídeo será enviado.

Para criar um canal YouTube:

1. Vá para [https://www.youtube.com](https://www.youtube.com/) e faça logon usando suas credenciais de conta do Google.
1. No canto superior direito da página do YouTube, clique na imagem do perfil (também pode aparecer como uma letra dentro de um círculo colorido sólido) e clique em **[!UICONTROL YouTube settings]** (ícone de engrenagem redonda).
1. Na página Visão geral , no cabeçalho Recursos adicionais, clique em **[!UICONTROL Ver todos os meus canais ou criar um novo canal]**.
1. Na página Canais , clique em **[!UICONTROL Criar um novo canal]**.
1. Na página Conta de marca, no campo Nome da conta de marca , digite um nome de negócios ou qualquer outro nome de canal que você escolher onde deseja publicar seus ativos de vídeo e, em seguida, clique em **[!UICONTROL Criar]**.

   Lembre-se do nome inserido aqui, pois será necessário inseri-lo novamente ao configurar o YouTube no AEM.

1. (Opcional) Se necessário, adicione mais canais.

   Agora, você adicionará tags para publicação.

### Adicionar tags para publicação {#adding-tags-for-publishing}

Para publicar seus vídeos no YouTube, AEM associa as tags a um ou mais canais do YouTube. Para adicionar tags para publicação, consulte [Administração de tags](/help/sites-administering/tags.md).

Ou, se você pretende usar as tags padrão no AEM, ignore esta tarefa e vá para [Ativando o agente de replicação YouTube Publish](#enabling-the-youtube-publish-replication-agent).

### Ativando o agente de replicação de publicação do YouTube {#enabling-the-youtube-publish-replication-agent}

Depois de habilitar o agente de replicação YouTube Publish , se quiser testar a conexão com a conta do Google Cloud, toque em **[!UICONTROL Testar conexão]**. Uma guia do navegador exibe os resultados da conexão. Se você tiver adicionado os Canais do YouTube, uma lista desses é exibida como parte do teste.

1. No canto superior esquerdo do AEM, clique no logotipo do AEM e, no painel à esquerda, clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]** > **[!UICONTROL Agentes no autor]**.
1. Na página Agentes do autor , clique em **[!UICONTROL Publicação do YouTube (youtube)]**.
1. Na barra de ferramentas, à direita de Configurações, clique em **[!UICONTROL Editar]**.
1. Marque a caixa de seleção **[!UICONTROL Enabled]** para ativar o agente de replicação.
1. Clique em **[!UICONTROL OK]**.

   Agora, você configurará o YouTube no AEM.

### Configuração do YouTube no AEM {#setting-up-youtube-in-aem}

A partir do AEM 6.4, um novo método de interface do usuário de toque foi introduzido para configurar a publicação do YouTube no AEM. Com base na instância do AEM instalada que você está usando, execute um dos procedimentos a seguir:

* Para configurar o YouTube no AEM antes da versão 6.4, consulte [Configuração do YouTube no AEM anterior a 6.4](/help/assets/video.md#setting-up-youtube-in-aem-before).
* Para configurar o YouTube no AEM 6.4 ou posterior, consulte [Configuração do YouTube no AEM 6.4 e posterior](#setting-up-youtube-in-aem-and-later).

#### Configuração do YouTube no AEM 6.4 e posterior {#setting-up-youtube-in-aem-and-later}

1. Certifique-se de fazer logon na sua instância do Dynamic Media como um administrador.
1. No canto superior esquerdo, toque no logotipo Experience Manager e, em seguida, no painel à esquerda, toque em **[!UICONTROL Ferramentas]**(ícone de martelo) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuração de publicação do YouTube]**.
1. Toque em **[!UICONTROL global]** (não selecione).

1. Próximo ao canto superior direito da página global, toque em **[!UICONTROL Criar]**.
1. Na página Criar configuração do YouTube, em Configurações da Google Cloud Platform, no campo **[!UICONTROL Nome do aplicativo]**, digite a ID do projeto do Google.

   Você especificou a ID do projeto quando definiu as configurações da Google Cloud anteriormente.
Deixe a página Criar configuração do YouTube aberta; você retornará a ele em um momento.

   ![6_5_youtubepublish-createyoutubeconfiguration](assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. Usando um editor de texto simples, abra o arquivo JSON que você baixou e salvou anteriormente na tarefa [Definição das configurações do Google Cloud](/help/assets/video.md#configuring-google-cloud-settings).
1. Selecione e copie o texto JSON inteiro.
1. Retorne à caixa de diálogo Configurações da conta do YouTube. No campo **[!UICONTROL Configuração JSON]**, cole o texto JSON.
1. Próximo ao canto superior direito da página, toque em **[!UICONTROL Salvar]**.

   Agora, você configurará os canais YouTube no AEM.

1. Toque em **[!UICONTROL Adicionar Canal]**.
1. No campo Nome do canal , insira o nome do canal criado na tarefa **[!UICONTROL Adicionar um ou mais canais ao YouTube]** anteriormente.

   Opcionalmente, é possível adicionar uma descrição, se desejar.

1. Toque em **[!UICONTROL Adicionar]**.
1. Autenticação YouTube/Google é exibida. Se você ainda não estiver conectado à conta do Google Cloud, ignore esta etapa.

   * Digite o nome de usuário e a senha do Google associados à ID do projeto do Google e o texto JSON acima.
   * Dependendo de quantos canais sua conta tem para ver dois ou mais itens. Selecione um canal. Não selecionar o endereço de correio eletrônico; não é um canal.
   * Na próxima página, toque em **[!UICONTROL Accept]** para permitir o acesso a este canal.

1. Toque em **[!UICONTROL Permitir]**.

   Agora você irá configurar tags para publicação.

1. **[!UICONTROL Configuração de tags para publicação]**  - Na página Cloud Services > YouTube , toque no ícone de lápis para editar a lista de tags que deseja usar.
1. Toque no ícone da lista suspensa (sinal de interpolação) para exibir a lista de tags disponíveis no AEM.
1. Toque em uma ou mais tags para adicioná-las.

   Para excluir uma tag adicionada, selecione a tag e toque em **[!UICONTROL X]**.

1. Quando terminar de adicionar as tags desejadas, toque em **[!UICONTROL Salvar]**.

   Agora você publica vídeos no seu canal do YouTube.

#### Configuração do YouTube no AEM antes de 6.4 {#setting-up-youtube-in-aem-before}

1. Certifique-se de fazer logon na sua instância do Dynamic Media como um administrador.

1. No canto superior esquerdo, toque no logotipo Experience Manager e, em seguida, no painel à esquerda, toque em **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Implantação]** > **[!UICONTROL Cloud Services]**.
1. No cabeçalho Serviços de terceiros , em YouTube, toque em **[!UICONTROL Configurar agora]**.
1. Na caixa de diálogo Criar configuração , digite um título (obrigatório) e um nome (opcional) nos respectivos campos.
1. Toque em **[!UICONTROL Criar]**.
1. Na caixa de diálogo Configurações da conta do YouTube, no campo **[!UICONTROL Nome do aplicativo]**, digite a ID do projeto do Google.

   Você especificou a ID do projeto quando inicialmente [configurou as configurações do Google Cloud](/help/assets/video.md#configuring-google-cloud-settings) anteriormente.
Deixe a caixa de diálogo Configuração da conta do YouTube aberta; você retornará a ele em um momento.

1. Usando um editor de texto simples, abra o arquivo JSON que você baixou e salvou anteriormente na tarefa Definir configurações do Google Cloud.
1. Selecione e copie o texto JSON inteiro.
1. Retorne à caixa de diálogo Configurações da conta do YouTube. No campo **[!UICONTROL Configuração JSON]**, cole o texto JSON.
1. Toque em **[!UICONTROL OK]**.

   Agora você configurará os canais YouTube no Experience Manager.

1. À direita de **[!UICONTROL Canais disponíveis]**, toque em **+** (ícone de adição).
1. Na caixa de diálogo Configurações do canal do YouTube, no campo Título, digite o nome do canal criado na tarefa **[!UICONTROL Adicionar um ou mais canais ao YouTube]** anteriormente.

   Opcionalmente, é possível adicionar uma descrição, se desejar.

1. Toque em **[!UICONTROL OK]**.
1. Autenticação YouTube/Google é exibida. Se você ainda não estiver conectado à conta do Google Cloud, ignore esta etapa.

   * Digite o nome de usuário e a senha do Google associados à ID do projeto do Google e o texto JSON acima.
   * Dependendo de quantos canais sua conta tem para ver dois ou mais itens. Selecione um canal. Não selecionar o endereço de correio eletrônico; não é um canal.
   * Na próxima página, toque em **[!UICONTROL Accept]** para permitir o acesso a este canal.

1. Toque em **[!UICONTROL Permitir]**.

   Agora você irá configurar tags para publicação.

1. **[!UICONTROL Configuração de tags para publicação]**  - Na página Cloud Services > YouTube , toque no ícone de lápis para editar a lista de tags que deseja usar.
1. Toque no ícone da lista suspensa (sinal de interpolação) para exibir a lista de tags disponíveis no AEM.
1. Toque em uma ou mais tags para adicioná-las.

   Para excluir uma tag adicionada, selecione a tag e toque em **X**.

1. Quando terminar de adicionar as tags desejadas, toque em **[!UICONTROL OK]**.

   Agora você publica vídeos no seu canal do YouTube.

### (Opcional) Automatizando a configuração das propriedades padrão do YouTube para seus vídeos carregados {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

Opcionalmente, é possível automatizar a configuração das propriedades do YouTube ao fazer upload dos vídeos. Para isso, crie um perfil de processamento de metadados no AEM.

Para criar o perfil de processamento de metadados, você primeiro copiará valores dos campos **[!UICONTROL Rótulo do campo]**, **[!UICONTROL Mapear para a propriedade]** e **[!UICONTROL Opções]**, todos encontrados nos Esquemas de metadados do vídeo. Em seguida, você criará seu perfil de processamento de metadados de vídeo do YouTube, adicionando esses valores a ele.

Para automatizar a configuração das propriedades padrão do YouTube para os vídeos carregados:

1. No canto superior esquerdo, toque no logotipo do Experience Manager e, em seguida, no painel à esquerda, clique em **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados]**.
1. Clique em **[!UICONTROL default]**. (Não adicione uma marca de seleção à caixa de seleção à esquerda de &quot;padrão&quot;.)
1. Na página **[!UICONTROL padrão]**, marque a caixa à esquerda de **[!UICONTROL vídeo]** e toque em **[!UICONTROL Editar]**.
1. Na página Editor de esquema de metadados , toque na guia **[!UICONTROL Avançado]**.
1. No cabeçalho Publicação no YouTube, clique em **[!UICONTROL Categoria do YouTube]**.
1. No lado direito da página, na guia **[!UICONTROL Settings]**, faça o seguinte:

   * No campo de texto **[!UICONTROL Mapear para propriedade]**, selecione e copie o valor.
Cole o valor copiado no editor de texto aberto. Você precisará desse valor posteriormente ao criar seu perfil de processamento de metadados. Deixe o editor de texto aberto.

   * Em **[!UICONTROL Choices]**, selecione e copie o valor padrão que deseja usar (como People &amp; Blogs ou Science &amp; Technology).
Cole o valor copiado no editor de texto aberto. Você precisará desse valor posteriormente ao criar seu perfil de processamento de metadados. Deixe o editor de texto aberto.

1. No cabeçalho Publicação do YouTube, toque em **[!UICONTROL Privacidade do YouTube]**.
1. No lado direito da página, na guia **[!UICONTROL Settings]**, faça o seguinte:

   * No campo de texto **[!UICONTROL Mapear para propriedade]**, selecione e copie o valor.
Cole o valor copiado no editor de texto aberto. Você precisará desse valor posteriormente ao criar seu perfil de processamento de metadados. Deixe o editor de texto aberto.

   * Em **[!UICONTROL Choices]**, selecione e copie o valor padrão que deseja usar. Observe que as Opções são agrupadas em pares de dois. O campo inferior do par é o valor padrão que você deseja copiar, como público, não listado ou privado.
Cole o valor copiado no editor de texto aberto. Você precisará desse valor posteriormente ao criar seu perfil de processamento de metadados. Deixe o editor de texto aberto.

1. Próximo ao canto superior direito da página Editor de esquema de metadados, clique em **[!UICONTROL Cancelar]**.
1. No canto superior esquerdo do AEM, toque no logotipo do AEM e, no painel à esquerda, clique em **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de metadados]**.

1. Na página Perfis de metadados , próximo ao canto superior direito da página, clique em **[!UICONTROL Criar]**.
1. Na caixa de diálogo Adicionar perfil de metadados, no campo de texto **[!UICONTROL Título do perfil]**, digite o nome `YouTube Video` e clique em **[!UICONTROL Criar]**.
1. Na página Editor de perfil de metadados , clique na guia **[!UICONTROL Avanço]** .
1. Adicione os valores copiados de Publicação no YouTube ao perfil, fazendo o seguinte:

   * No lado direito da página, clique na guia **[!UICONTROL Criar formulário]**.
   * (Opcional) Arraste o componente rotulado **[!UICONTROL Cabeçalho da seção]** para a esquerda e solte-o na área do formulário.
   * (Opcional) Clique em **[!UICONTROL Rótulo do campo]** para selecionar o componente.
   * (Opcional) No lado direito da página, na guia Configurações , no campo de texto Rótulo do campo , digite `YouTube Publishing`.
   * Clique na guia **[!UICONTROL Criar formulário]** e arraste o componente rotulado **[!UICONTROL Texto de vários valores]** e solte-o abaixo do cabeçalho **[!UICONTROL Publicação do YouTube]** que você acabou de criar.

   * Clique em **[!UICONTROL Rótulo do campo]** para selecionar o componente.
   * No lado direito da página, na guia Configurações , cole os valores de Publicação do YouTube (valor do Rótulo do campo e Mapear para o valor da propriedade) que você copiou anteriormente, em seus respectivos campos no formulário. Cole o valor Choices no campo Default Value .

1. Adicione os valores copiados da Privacidade do YouTube ao perfil, fazendo o seguinte:

   * No lado direito da página, clique na guia **[!UICONTROL Criar formulário]**.
   * (Opcional) Arraste o componente rotulado **[!UICONTROL Cabeçalho da seção]** para a esquerda e solte-o na área do formulário.
   * (Opcional) Clique em **[!UICONTROL Rótulo do campo]** para selecionar o componente.
   * (Opcional) No lado direito da página, na guia Configurações , no campo de texto Rótulo do campo , digite `YouTube Privacy`.
   * Clique na guia **[!UICONTROL Criar formulário]** e arraste o componente rotulado **[!UICONTROL Texto de vários valores]** e solte-o abaixo do cabeçalho **[!UICONTROL Privacidade do YouTube]** que você acabou de criar.

   * Clique em **[!UICONTROL Rótulo do campo]** para selecionar o componente.
   * No lado direito da página, na guia Configurações , cole os valores de Publicação do YouTube (valor do Rótulo do campo e Mapear para o valor da propriedade) que você copiou anteriormente, em seus respectivos campos no formulário. Cole o valor Choices no campo Default Value .

1. Ao lado do canto superior direito da página, clique em **[!UICONTROL Salvar]**.
1. Aplique o perfil de metadados de Publicação do YouTube às pastas onde você fará upload de vídeos. Você precisará ter o Perfil de metadados e o Perfil de vídeo definidos.

   Consulte [Perfis de metadados](/help/assets/metadata-config.md#metadata-profiles) e [Perfis de vídeo](/help/assets/video-profiles.md).

### Publicar vídeos no seu canal do YouTube {#publishing-videos-to-your-youtube-channel}

Agora, associe as tags adicionadas anteriormente aos ativos de vídeo. Esse processo permite AEM saber quais ativos serão publicados no canal do YouTube.

>[!NOTE]
>
>Ao executar o no modo Dynamic Media - Scene7, observe que a publicação imediatamente não é publicada automaticamente no YouTube. Quando o modo Dynamic Media - Scene7 estiver configurado, há duas opções de publicação para escolher: **[!UICONTROL Imediatamente]** ou **[!UICONTROL Após ativação]**.
>
>**[!UICONTROL Publicar]** imediatamente significa que o ativo carregado, depois de sincronizado com o IPS, é publicado automaticamente no sistema de entrega. Embora isso seja verdade para o Dynamic Media, não é verdadeiro para o YouTube. Para publicar no YouTube, você deve publicar por meio do AEM Author.

>[!NOTE]
>
>Para publicar conteúdo do YouTube, o AEM usa o fluxo de trabalho **[!UICONTROL Publicar no YouTube]**, que permite monitorar o progresso e exibir quaisquer informações de falha.
>
>Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).
>
>Para obter informações de progresso mais detalhadas, você pode monitorar o log do YouTube em replicação. Esteja ciente, no entanto, de que esse monitoramento requer acesso de administrador.

Para publicar vídeos no seu canal do YouTube:

1. Em AEM, navegue até um ativo de vídeo que deseja publicar no canal do YouTube.
1. Selecione o ativo de vídeo (o conjunto de vídeos adaptáveis).
1. Na barra de ferramentas, clique em **[!UICONTROL Propriedades]**.
1. Na guia Básico , no cabeçalho Metadados , clique em **[!UICONTROL Abrir caixa de diálogo de seleção]** à direita do campo Tags .
1. Na página Selecionar tags , navegue até as tags que deseja usar e selecione uma ou mais tags.

   Lembre-se de que as tags devem ser associadas ao canal do YouTube.

1. No canto superior direito da página, clique em **[!UICONTROL Selecionar]**.
1. No canto superior direito da página de propriedades do vídeo, clique em **[!UICONTROL Salvar e fechar]**.
1. Na barra de ferramentas, clique em **[!UICONTROL Publicação rápida]**.

   Consulte também [Uso do gerenciamento de publicação com AEM Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html).

   Opcionalmente, é possível verificar o vídeo publicado no canal do YouTube.

### (Opcional) Verificação do vídeo publicado no YouTube {#optional-verifying-the-published-video-on-youtube}

Opcionalmente, é possível monitorar o progresso da publicação (ou desfazer a publicação) do YouTube.

Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

Os tempos de publicação podem variar bastante, dependendo de vários fatores que incluem o formato do vídeo de origem primária, o tamanho do arquivo e o tráfego de upload. O processo de publicação pode levar de alguns minutos a várias horas. Além disso, esteja ciente de que os formatos de resolução mais alta são renderizados muito mais lentamente. Por exemplo, 720p e 1080p levam significativamente mais tempo para aparecer do que 480p.

Após oito horas, se você ainda vir uma mensagem de status que diz **[!UICONTROL Uploaded (processing, por favor aguarde)]**, tente remover o vídeo de nosso site e carregá-lo novamente.

### Vincular URLs do YouTube à sua aplicação web {#linking-youtube-urls-to-your-web-application}

Você pode obter uma string de URL do YouTube gerada pelo Dynamic Media após publicar o vídeo. Ao copiar o URL do YouTube, ele chega à Área de transferência para que você possa colá-lo conforme necessário nas páginas do seu site ou aplicativo.

>[!NOTE]
>
>O URL do YouTube não está disponível para cópia até que você tenha publicado o ativo de vídeo no YouTube.

Para vincular URLs do YouTube ao seu aplicativo da Web:

1. Navegue até o ativo de vídeo *YouTube publicado* cujo URL você deseja copiar e selecione-o.

   Lembre-se de que os URLs do YouTube só estão disponíveis para copiar *depois de* você tem primeiro *publicado* os ativos de vídeo para o YouTube.

1. Na barra de ferramentas, clique em **[!UICONTROL Propriedades]**.
1. Clique na guia **[!UICONTROL Avançado]**.
1. No cabeçalho Publicação do YouTube, na Lista de URLs do YouTube, selecione e copie o texto do URL para o navegador da Web para visualizar o ativo ou adicionar à página de conteúdo da Web.

### Desfazer a publicação de vídeos para removê-los do YouTube {#unpublishing-videos-to-remove-them-from-youtube}

Ao cancelar a publicação de um ativo de vídeo no AEM, o vídeo é removido do YouTube.

>[!CAUTION]
>
>Se você remover um vídeo diretamente do YouTube, o AEM não estará ciente e continuará a se comportar como se o vídeo ainda estivesse publicado no YouTube. Sempre cancele a publicação de um ativo de vídeo do YouTube por meio de AEM.

>[!NOTE]
>
>Para remover o conteúdo do YouTube, o AEM usa o workflow **[!UICONTROL Cancelar publicação do YouTube]**, que permite monitorar o progresso e exibir quaisquer informações de falha.
>
>Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

Para cancelar a publicação de vídeos para removê-los do YouTube:

1. Navegue até os ativos de vídeo que você deseja cancelar a publicação por meio do canal do YouTube.
1. Em um modo de seleção de ativo, selecione um ou mais ativos de vídeo publicados.
1. Na barra de ferramentas, clique em **[!UICONTROL Gerenciar publicação]**. Talvez seja necessário tocar no ícone de três pontos (. . .) na barra de ferramentas para ver **[!UICONTROL Gerenciar publicação]**.
1. Na página Gerenciar publicação , toque em **[!UICONTROL Cancelar publicação]**.
1. No canto superior direito da página, toque em **[!UICONTROL Next]**.
1. No canto superior direito da página, toque em **[!UICONTROL Cancelar publicação]**.

## Monitorar o progresso da codificação de vídeo e da publicação no YouTube {#monitoring-video-encoding-and-youtube-publishing-progress}

Ao carregar um novo vídeo para uma pasta com codificação de vídeo aplicada ou ao publicar seu vídeo no Youtube, você pode monitorar como sua codificação de vídeo/publicação do Youtube está progredindo (ou falhando) de várias maneiras. O progresso da publicação do YouTube real só está disponível por meio dos logs, mas se ele falhar ou for bem-sucedido é listado de formas adicionais descritas no procedimento a seguir. Além disso, você pode receber notificações por email quando um fluxo de trabalho de publicação ou codificação de vídeo do YouTube for concluído ou interrompido.

### Monitorar o progresso {#monitoring-progress}

Para monitorar o progresso (incluindo codificação com falha/publicação do YouTube):

1. Exibir o progresso da codificação de vídeo na pasta de ativos:

   * Na exibição de cartão, o progresso da codificação de vídeo é exibido no ativo por porcentagem. Se houver um erro, essas informações também serão exibidas no ativo.

   ![chlimage_1-429](assets/chlimage_1-429.png)

   * Na exibição em lista, o progresso da codificação do vídeo é exibido na coluna **[!UICONTROL Status de processamento]**. Se houver um erro, essa mensagem será exibida nessa mesma coluna.

   ![chlimage_1-430](assets/chlimage_1-430.png)

   Essa coluna não é exibida por padrão. Para ativar a coluna, selecione **[!UICONTROL Configurações de exibição]** no menu suspenso de exibições e adicione a coluna **[!UICONTROL Status de processamento]** e toque ou clique em **[!UICONTROL Atualizar]**.

   ![chlimage_1-431](assets/chlimage_1-431.png)

1. Exibir o progresso nos detalhes do ativo. Ao tocar ou clicar em um ativo, abra o menu suspenso e selecione **[!UICONTROL Linha do tempo]**. Para restringi-lo a atividades de fluxo de trabalho como codificação ou publicação do YouTube, selecione **[!UICONTROL Fluxos de trabalho]**.

   ![chlimage_1-432](assets/chlimage_1-432.png)

   Qualquer informação do fluxo de trabalho, como codificação, é exibida na linha do tempo. Para publicação do YouTube, a linha do tempo do Fluxo de trabalho também inclui o nome do canal do YouTube e o URL do vídeo do YouTube. Além disso, você vê notificações de falha na linha do tempo do fluxo de trabalho depois que a publicação é concluída.

   >[!NOTE]
   >
   >Pode levar muito tempo para que as mensagens de erro/falha sejam gravadas, devido a várias configurações de fluxo de trabalho em **[!UICONTROL tentativas]**, **[!UICONTROL atraso de repetição]** e **[!UICONTROL tempo limite]** em [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), por exemplo:
   >
   >    * Configuração da fila de trabalhos do Apache Sling
   >    * Manipulador de Trabalho do Processo Externo do Fluxo de Trabalho do Adobe Granite
   >    * Fila de tempo limite do fluxo de trabalho do Granite

   >
   >Você pode ajustar as **[!UICONTROL tentativas]**, o **[!UICONTROL atraso de repetição]** e as propriedades de **[!UICONTROL tempo limite]** nessas configurações.

1. Nos fluxos de trabalho em andamento, consulte Instâncias de fluxo de trabalho disponíveis em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Instâncias]**.

   >[!NOTE]
   >
   >Talvez seja necessário direitos administrativos para acessar o menu **[!UICONTROL Tools]**.

   ![chlimage_1-433](assets/chlimage_1-433.png)

   Selecione a instância e toque em **[!UICONTROL Abrir histórico]**.

   ![chlimage_1-434](assets/chlimage_1-434.png)

   Na área Instâncias do fluxo de trabalho , também é possível suspender, encerrar ou renomear fluxos de trabalho. Consulte [Administração de fluxos de trabalho](/help/sites-administering/workflows-administering.md) para obter mais informações.

1. Em tarefas com falha, consulte Falhas de fluxo de trabalho, disponível em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Falhas]**. A **[!UICONTROL Falha do fluxo de trabalho]** lista todas as atividades do fluxo de trabalho com falha.

   >[!NOTE]
   >
   >Talvez seja necessário direitos administrativos para acessar o menu **[!UICONTROL Tools]**.

   ![chlimage_1-435](assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >Pode levar muito tempo para que a mensagem de erro seja gravada devido a várias configurações de fluxo de trabalho em **[!UICONTROL tentativas]**, **[!UICONTROL atraso de repetição]** e **[!UICONTROL tempo limite]** em [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), por exemplo:
   >
   >
   >
   >    * Configuração da fila de trabalhos do Apache Sling
   >    * Manipulador de Trabalho do Processo Externo do Fluxo de Trabalho do Adobe Granite
   >    * Fila de tempo limite do fluxo de trabalho do Granite

   >
   >
   >Você pode ajustar as **[!UICONTROL tentativas]**, o **[!UICONTROL atraso de repetição]** e as propriedades de **[!UICONTROL tempo limite]** nessas configurações.

1. Em fluxos de trabalho concluídos, consulte Arquivo de fluxo de trabalho disponível em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Arquivar]**. O **[!UICONTROL Arquivo de fluxo de trabalho]** lista todas as atividades de fluxo de trabalho concluídas.

   >[!NOTE]
   >
   >Talvez seja necessário direitos administrativos para acessar o menu **[!UICONTROL Tools]**.

   ![chlimage_1-436](assets/chlimage_1-436.png)

1. Você pode receber notificações por email sobre trabalhos de fluxo de trabalho abortados ou com falha. Essas notificações por email podem ser configuradas por um administrador. Consulte [Configuração de notificações por email](#configuring-e-mail-notifications).

#### Configurar notificações por email {#configuring-e-mail-notifications}

>[!NOTE]
>
>Talvez seja necessário direitos administrativos para acessar o menu **[!UICONTROL Tools]**.

A forma como você configura a notificação depende se você deseja notificações para codificar trabalhos ou trabalhos de publicação do YouTube:

* Para tarefas de codificação, você pode acessar a página de configuração de todas as notificações por email de fluxo de trabalho AEM em **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]** e procurando por **[!UICONTROL Day CQ Workflow Notification Service]**. Consulte [Configuração da notificação por email no AEM](/help/sites-administering/notification.md). Você pode marcar ou desmarcar as caixas de seleção de **[!UICONTROL Notificar em Abortar]** ou **[!UICONTROL Notificar em Concluir]** de acordo.

* Para trabalhos de publicação do YouTube, faça o seguinte:

1. Em AEM, toque em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos de fluxo de trabalho , selecione **[!UICONTROL Publicar no YouTube]** e toque em **[!UICONTROL Editar]** na barra de ferramentas.
1. Próximo ao canto superior direito da página do fluxo de trabalho Publicar no YouTube , toque em **[!UICONTROL Editar]**.
1. Passe o mouse sobre o componente Upload do YouTube e toque uma vez para exibir a barra de ferramentas em linha.

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. Na barra de ferramentas em linha, toque no ícone Configuração (chave). Clique na guia **[!UICONTROL Argumentos]**.

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. Na caixa de diálogo Processo de upload do YouTube - Propriedades da etapa , toque na guia **[!UICONTROL Argumentos]**.

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. Você pode marcar ou desmarcar as seguintes caixas de seleção:

   * Início da publicação
   * Falha na publicação
   * Conclusão de publicação - inclui informações sobre canais e URLs

   Limpar uma caixa de seleção significa que você não receberá a notificação por email especificada do fluxo de trabalho de Publicação do YouTube .

   >[!NOTE]
   >
   >Esses emails são específicos do YouTube e, além das notificações por email de workflow genéricas. Como resultado, você pode receber dois conjuntos de notificações por email - a notificação genérica disponível no **[!UICONTROL Day CQ Workflow Email Notification Service]** e uma específica para o YouTube, dependendo das configurações.

1. Quando terminar, próximo ao canto superior direito da caixa de diálogo, toque no ícone **[!UICONTROL Concluído]** (marca de seleção).
1. Na página Publicar no YouTube workflow , próximo ao canto superior direito, toque em **[!UICONTROL Sincronizar]**.

## Exibição de relatórios de vídeo {#viewing-video-reports}

>[!NOTE]
>
>Os relatórios de vídeo só estão disponíveis quando você executa o Dynamic Media - Modo híbrido.

Os Relatórios de vídeo exibem várias métricas agregadas em um período especificado para ajudar você a monitorar o desempenho *publicado *individual e de vídeos agregados conforme o esperado. Os seguintes dados de métricas principais são agregados para todos os vídeos publicados em todo o seu site:

* Vídeos iniciados
* Taxa de Conclusão
* Tempo médio no vídeo
* Tempo total no vídeo
* Vídeos por visita

Uma tabela de todos os vídeos *publicados* também é listada para que você possa rastrear os vídeos mais vistos em seu site com base no total de inícios de vídeo.

Ao tocar no nome de um vídeo na lista, ele mostra o relatório de retenção de público-alvo (lista suspensa) do vídeo, na forma de um gráfico de linha. O gráfico exibe o número de visualizações em qualquer momento durante a reprodução do vídeo. Quando você reproduz o vídeo, a barra vertical é rastreada em sincronização com o indicador de hora no reprodutor. Quedas nos dados do gráfico de linha indicam onde o público-alvo sai do desinteresse.

Se o vídeo foi codificado fora do Adobe Experience Manager Dynamic Media, o gráfico de retenção de público-alvo (lista suspensa) e os dados de Porcentagem de reprodução na tabela não estarão disponíveis.

Consulte também [Configuração do Dynamic Media Cloud Services](/help/assets/config-dynamic.md).

>[!NOTE]
>
>Os dados de rastreamento e relatórios se baseiam exclusivamente no uso do próprio reprodutor de vídeo do Dynamic Media e da predefinição associada do reprodutor de vídeo. Dessa forma, não é possível rastrear e gerar relatórios sobre os vídeos reproduzidos por meio de outros players de vídeo.

Por padrão, na primeira vez que você insere Relatórios de vídeo, o relatório exibe dados de vídeo que começam no primeiro dia do mês atual e terminam com a data do mês atual. No entanto, você pode substituir o intervalo de datas padrão especificando seu próprio intervalo de datas. Na próxima vez que você inserir os Relatórios de vídeo, será usado o intervalo de datas especificado.

Para que os relatórios de vídeo funcionem corretamente, uma ID de conjunto de relatórios é criada automaticamente quando o Dynamic Media Cloud Services é configurado. Ao mesmo tempo, a ID do conjunto de relatórios é enviada para o servidor de publicação, para que fique disponível para o recurso Copiar URL ao visualizar ativos. No entanto, isso requer que o servidor de publicação já esteja configurado. Se o servidor de Publicação não estiver configurado, você ainda poderá publicar para ver o relatório de vídeo. No entanto, será necessário retornar à Configuração da Dynamic Media Cloud e tocar em **[!UICONTROL OK]**.

Para exibir relatórios de vídeo:

1. No canto superior esquerdo do AEM, toque no logotipo do AEM e, no painel à esquerda, toque em **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Ativos]** > **[!UICONTROL Relatórios de vídeo]**.
1. Na página Relatórios de vídeo , execute um dos seguintes procedimentos:

   * Próximo ao canto superior direito, toque no ícone **Atualizar relatório de vídeo**.
Você só precisará usar Atualizar se a data final do relatório for o dia atual. Isso garante que você visualize o rastreamento de vídeo que ocorreu desde a última vez em que você executou o relatório.

   * Próximo ao canto superior direito, toque no ícone **Seletor de data**.
Especifique o intervalo de datas de início e término para o qual deseja obter os dados de vídeo e toque em **[!UICONTROL Executar relatório]**.

   A caixa de grupo Principais métricas identifica várias medidas agregadas para todos os vídeos *publicados* no seu site.

1. Na tabela que lista os vídeos publicados principais, toque no nome de um vídeo para reproduzir o vídeo e também veja o relatório de retenção de público-alvo (drop-off) do vídeo.

### Exibição de relatórios de vídeo com base em um visualizador de vídeo criado usando o SDK do visualizador HTML5 do Dynamic Media {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

Se você estiver usando um visualizador de vídeo pronto para uso fornecido pelo Dynamic Media ou se tiver criado uma predefinição de visualizador personalizada com base em um visualizador de vídeo pronto para uso, nenhuma etapa adicional será necessária para exibir relatórios de vídeo. No entanto, se você criou seu próprio visualizador de vídeo com base na API do SDK do visualizador de HTML5, use as seguintes etapas para garantir que o visualizador de vídeo esteja enviando eventos de rastreamento para os Relatórios de vídeo do Dynamic Media.

Use o [Adobe Dynamic Media Viewers Reference Guide](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html) e a [API HTML5 Viewer SDK](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) para criar seus próprios visualizadores de vídeo.

Para exibir os Relatórios de vídeo com base em um visualizador de vídeo criado usando a API do SDK do Visualizador de HTML5:

1. Navegue até qualquer ativo de vídeo publicado.
1. Próximo ao canto superior esquerdo da página do ativo, na lista suspensa, selecione **[!UICONTROL Visualizadores]**.
1. Selecione qualquer predefinição do visualizador de vídeo e copie o código incorporado.
1. No código incorporado, encontre a linha com o seguinte:

   `videoViewer.setParam("config2", "<value>");`

   O parâmetro `config2` permite o rastreamento em Visualizadores HTML5. Também é uma predefinição específica da empresa que contém as informações de configuração dos Relatórios de vídeo e das configurações específicas do Adobe Analytics para o cliente.

   O valor correto do parâmetro config2 é encontrado tanto no **[!UICONTROL Código incorporado]** quanto na função de cópia **[!UICONTROL URL]**. No URL do comando de cópia **[!UICONTROL URL]**, procure pelo parâmetro `&config2=<value>`. O valor é quase sempre `companypreset`, mas em algumas instâncias também pode ser `companypreset-1`, `companypreset-2` e assim por diante.

1. No código personalizado do visualizador de vídeo, adicione AppMeasurementBridge.jsp à página do visualizador fazendo o seguinte:

   * Primeiro, determine se você precisa do parâmetro `&preset`.

      Se o parâmetro `config2` for `companypreset`, você *não* precisará de `&preset=parameter`.

      Se `config2` for algo diferente, defina o parâmetro predefinido como o parâmetro `config2`. Por exemplo, se `config2=companypreset-2`, adicione `&param2=companypreset-2` ao URL AppMeasurementBridge.jsp.

   * Em seguida, adicione o script AppMeasurementBridge.jsp:

      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. Crie o componente TrackingManager fazendo o seguinte:

   * Depois de chamar `s7sdk.Util.init();` crie uma instância do TrackingManager para rastrear eventos, adicionando o seguinte:

      `var trackingManager = new s7sdk.TrackingManager();`

   * Conecte componentes ao TrackingManager fazendo o seguinte:

      No manipulador de eventos `s7sdk.Event.SDK_READY`, anexe o componente que deseja rastrear ao TrackingManager.

      Por exemplo, se o componente for `videoPlayer`, adicione

      `trackingManager.attach(videoPlayer);`

      para anexar o componente ao trackingManager. Para rastrear vários visualizadores em uma página, use vários componentes do gerenciador de rastreamento.

   * Crie o objeto AppMeasurementBridge adicionando o seguinte:

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

   * Adicione a função de rastreamento ao adicionar o seguinte:

      ```
      trackingManager.setCallback(appMeasurementBridge.track, 
       appMeasurementBridge);
      ```
   O objeto appMeasurementBridge tem uma função de rastreamento integrada. No entanto, você pode fornecer o seu próprio para suportar vários sistemas de rastreamento ou outras funcionalidades.

<!--    For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

## Adicionar legendas ao vídeo {#adding-captions-to-video}

Você pode estender o alcance de seus vídeos para os mercados globais adicionando legendas a vídeos individuais ou aos Conjuntos de vídeos adaptáveis. Ao adicionar legendas, você evita a necessidade de dublar o áudio ou a necessidade de usar alto-falantes nativos para regravar o áudio para cada idioma diferente. O vídeo é reproduzido no idioma em que foi gravado. As legendas em idioma estrangeiro são exibidas para que pessoas de idiomas diferentes ainda possam entender a parte de áudio.

As legendas também permitem maior acessibilidade, usando legendas ocultas para pessoas surdas ou com deficiência auditiva.

>[!NOTE]
>
>O reprodutor de vídeo usado deve ser compatível com a exibição de legendas.

O Dynamic Media tem a capacidade de converter arquivos de legenda para o formato JSON (JavaScript Object Notation). Essa conversão significa que você pode incorporar o texto JSON em uma página da Web como uma transcrição oculta, mas completa, do vídeo. Os mecanismos de pesquisa podem, então, rastrear e indexar o conteúdo para tornar os vídeos mais fáceis de serem descobertos e fornecer aos clientes detalhes adicionais sobre o conteúdo do vídeo.

Consulte [Serving static (non-image) content](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api) na *Ajuda da API de disponibilização e renderização de imagens do Dynamic Media* para obter mais informações sobre o uso da função JSON em um URL.

**Para adicionar legendas ou legendas ao vídeo**:

1. Use um aplicativo ou serviço de terceiros para criar sua legenda/arquivo de subtítulo de vídeo.

   Certifique-se de que o arquivo criado siga o padrão WebVTT (Web Video Text Tracks). A extensão de nome de arquivo de legendagem é .vtt. Você pode obter mais informações sobre o padrão de legendagem WebVTT.

   Consulte [WebVTT: O texto da Web rastreia o formato](https://dev.w3.org/html5/webvtt/).

   Há ferramentas e serviços gratuitos e premium que podem ser usados para criar arquivos de legenda/subtítulo fora do Dynamic Media. Por exemplo, para criar um arquivo de legenda de vídeo simples sem estilização, você pode usar a seguinte ferramenta de edição e criação de legendas online gratuitas:

   [Criador de legendas WebVTT](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   Para obter melhores resultados, use a ferramenta no Internet Explorer 9 ou superior, Google Chrome ou Safari.

   Na ferramenta, no campo **[!UICONTROL Inserir URL do arquivo de vídeo]**, cole o URL copiado do arquivo de vídeo e clique em **[!UICONTROL Carregar]**. Consulte [Obter um URL de um ativo](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) para obter o URL para o próprio arquivo de vídeo, o qual você pode colar no campo **[!UICONTROL Inserir URL]** do arquivo de vídeo. O Internet Explorer, o Chrome ou o Safari podem reproduzir nativamente o vídeo.

   Agora siga as instruções na tela do site para criar e salvar seu arquivo WebVTT. Quando terminar, copie o conteúdo do arquivo de legenda e o cole em um editor de texto simples e salve com uma extensão de nome de arquivo .vtt.

   >[!NOTE]
   >
   >Para obter suporte global a legendas de vídeo em vários idiomas, esteja ciente de que o padrão WebVTT requer a criação de arquivos .vtt e chamadas separadas para cada idioma que você deseja suportar.

   Geralmente, você deseja nomear o arquivo VTT da legenda com o mesmo nome do arquivo de vídeo e anexá-lo à localidade do idioma, como -EN, ou -FR, ou -DE e assim por diante. Ao fazer isso, ele pode ajudá-lo a automatizar a geração dos URLs de vídeo usando seu sistema de gerenciamento de conteúdo da Web existente.

1. No AEM, carregue o arquivo de legenda da WebVTT no DAM.
1. Navegue até o ativo de vídeo *publicado* que deseja associar ao arquivo de legenda que você carregou.

   Lembre-se de que os URLs só estão disponíveis para cópia *depois* que você *publicou* os ativos pela primeira vez.

   Consulte [Publicar ativos.](/help/assets/publishing-dynamicmedia-assets.md)

1. Faça uma das seguintes opções:

   * Para obter uma experiência do visualizador de vídeo pop-up, toque em **[!UICONTROL URL]**. Na caixa de diálogo URL, selecione e copie o URL para a Área de transferência e, em seguida, passe o URL para um editor de texto simples. Anexe o URL copiado do vídeo com a seguinte sintaxe:

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      Observe o `,1` no final do caminho da legenda. Imediatamente após a extensão do nome de arquivo .vtt no caminho, você tem a opção de ativar (ativar) ou desativar (desativar) o botão de legenda fechada na barra do reprodutor de vídeo, definindo para `,1` ou `,0`, respectivamente.

   * Para obter uma experiência de visualizador de vídeo incorporado, toque em **[!UICONTROL Incorporar código]**. Na caixa de diálogo Incorporar código, selecione e copie o código incorporado na Área de transferência e cole o código em um editor de texto simples. Anexe o código incorporado copiado com a seguinte sintaxe:

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      Observe o `,1` no final do caminho da legenda. Imediatamente após a extensão do nome de arquivo .vtt no caminho, você tem a opção de ativar (ativar) ou desativar (desativar) o botão de legenda fechada na barra do reprodutor de vídeo, definindo para `,1` ou `,0`, respectivamente.

## Adicionar marcadores de capítulo ao vídeo {#adding-chapter-markers-to-video}

Você pode tornar seus vídeos de formulário longos mais fáceis de assistir e navegar adicionando marcadores de capítulo a vídeos individuais ou aos Conjuntos de vídeos adaptáveis. Quando um usuário reproduz o vídeo, pode clicar nos marcadores de capítulo na linha do tempo do vídeo (também conhecidos como depurador de vídeo) para navegar facilmente até o ponto de interesse, ou imediatamente para novos conteúdos, demonstrações, tutoriais e assim por diante.

>[!NOTE]
>
>O reprodutor de vídeo usado deve suportar o uso de marcadores de capítulo. Os players de vídeo do Dynamic Media são compatíveis com marcadores de capítulo, mas o uso de players de vídeo de terceiros não é compatível.

Se desejar, você pode criar e marcar seu próprio visualizador de vídeo personalizado com capítulos em vez de usar uma predefinição do visualizador de vídeo. Para obter instruções sobre como criar seu próprio visualizador HTML5 com navegação de capítulo, na API do SDK do visualizador HTML5 do Adobe, consulte o cabeçalho &quot;Personalizando o comportamento usando modificadores&quot; nas classes `s7sdk.video.VideoPlayer` e `s7sdk.video.VideoScrubber`. Consulte a documentação do [HTML5 Viewer SDK API](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html).

<!-- If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading “Customizing Behavior Using Modifiers” under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

Você cria uma lista de capítulo para o vídeo da mesma forma que cria legendas. Ou seja, você cria um arquivo WebVTT. Observe, no entanto, que esse arquivo deve ser separado de qualquer arquivo de legenda WebVTT que você também possa estar usando; não é possível combinar legendas e capítulos em um arquivo WebVTT.

Você pode usar a seguinte amostra como exemplo do formato usado para criar um arquivo WebVTT com navegação de capítulo:

### Arquivo WebVTT com navegação de capítulo de vídeo {#webvtt-file-with-video-chapter-navigation}

```xml
WEBVTT
Chapter 1
00:00.000 --> 01:04.364
The bicycle store behind it all.
Chapter 2
01:04.364 --> 02:00.944
Creative Cloud.
Chapter 3
02:00.944 --> 03:02.937
Ease of management for a working solution.
Chapter 4
03:02.937 --> 03:35.000
Cost-efficient access to rapidly evolving technology.
```

No exemplo acima, `Chapter 1` é o identificador de sinalização e é opcional. A hora de sinalização de `00:00:000 --> 01:04:364` especifica a hora de início e a hora de término do capítulo, no formato `00:00:000`. Os três últimos dígitos são milissegundos e podem ser deixados como `000`, se preferir. O título do capítulo de `The bicycle store behind it all` é a descrição real do conteúdo do capítulo. O identificador de sinalização, a hora de início e o título do capítulo são exibidos em uma pop-up no reprodutor de vídeo quando um usuário passa o ponteiro do mouse sobre um ponto de sinalização visual na linha do tempo do vídeo.

Como você está usando um visualizador de vídeo HTML5, certifique-se de que o arquivo de capítulo criado siga o padrão WebVTT (Web Video Text Tracks). A extensão do nome de arquivo do capítulo é .vtt. Você pode obter mais informações sobre o padrão de legendagem WebVTT.

Consulte [WebVTT: O formato de Rastreamento de texto do vídeo da Web](https://dev.w3.org/html5/webvtt/)

**Para adicionar marcadores de capítulo ao vídeo:**

1. Salve o arquivo .vtt na codificação UTF8 para evitar problemas com a representação de caracteres no texto do título do capítulo.

   Geralmente, você deseja nomear o arquivo VTT do capítulo com o mesmo nome do arquivo de vídeo e anexá-lo a capítulos. Ao fazer isso, ele pode ajudá-lo a automatizar a geração dos URLs de vídeo usando seu sistema de gerenciamento de conteúdo da Web existente.
1. No AEM, faça upload do arquivo de capítulo WebVTT.

   Consulte [Upload de ativos](/help/assets/manage-assets.md#uploading-assets).

1. Faça uma das seguintes opções:

   <table>
     <tbody>
      <tr>
       <td>Para obter uma experiência de visualizador de vídeo pop-up</td>
       <td>
       <ol>
       <li>Navegue até o <i>ativo de vídeo publicado </i>que você deseja associar ao arquivo de capítulo que você enviou. Lembre-se de que os URLs só estão disponíveis para cópia <i>depois</i> que você <i>publicou</i> os ativos pela primeira vez. Consulte <a href="/help/assets/publishing-dynamicmedia-assets.md">Publicar ativos.</a></li>
       <li>No menu suspenso, clique ou toque em <strong>Visualizadores</strong>.</li>
       <li>No painel à esquerda, toque ou clique no nome predefinido do visualizador de vídeo. Uma visualização do vídeo é aberta em uma página separada.</li>
       <li>No painel à esquerda, na parte inferior, clique em <strong>URL</strong>.</li>
       <li>Na caixa de diálogo URL, selecione e copie o URL para a Área de transferência e, em seguida, passe o URL para um editor de texto simples.</li>
       <li>Anexe o URL copiado do vídeo com a seguinte sintaxe para associá-lo ao URL copiado para o arquivo de capítulo:<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>Para uma experiência de visualizador de vídeo incorporado<br /> </td>
       <td>
       <ol>
       <li>Navegue até o <i>ativo de vídeo publicado </i>que você deseja associar ao arquivo de capítulo que você enviou. Lembre-se de que os URLs só estão disponíveis para cópia <i>depois</i> que você <i>publicou</i> os ativos pela primeira vez. Consulte <a href="/help/assets/publishing-dynamicmedia-assets.md">Publicar ativos.</a></li>
       <li>No menu suspenso, clique ou toque em <strong>Visualizadores</strong>.</li>
       <li>No painel à esquerda, toque ou clique no nome predefinido do visualizador de vídeo. Uma visualização do vídeo é aberta em uma página separada.</li>
       <li>No painel à esquerda, na parte inferior, clique em <strong>Incorporado</strong>.</li>
       <li>Na caixa de diálogo Incorporar código, selecione e copie o código inteiro para a Área de transferência e, em seguida, cole-o em um editor de texto simples.</li>
       <li>Anexe o código incorporado do vídeo à seguinte sintaxe para associá-lo ao URL copiado ao arquivo de capítulo:<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt&gt;"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

## Sobre miniaturas de vídeo no Dynamic Media - Modo Scene7 {#about-video-thumbnails-in-dynamic-media-scene-mode}

Uma miniatura de vídeo é uma versão reduzida de um quadro de vídeo ou um ativo de imagem que representa o vídeo para o cliente. A miniatura deve servir para incentivar um cliente a clicar no vídeo.

Todos os vídeos no AEM devem ter uma miniatura associada; não é possível excluir uma miniatura sem substituí-la. Por padrão, ao fazer upload de um vídeo para o AEM, o primeiro quadro é usado como miniatura. Entretanto, é possível personalizar a miniatura para fins de identidade visual ou de criação de marcas, por exemplo. Ao personalizar uma miniatura de vídeo, você pode reproduzir o vídeo e pausar no quadro que deseja usar ou selecionar um ativo de imagem que já foi carregado e *publicado* no gerenciador de ativos digitais.

Observe que uma imagem em miniatura de vídeo personalizada selecionada a partir de um vídeo não é extraída e salva no DAM como um ativo separado e distinto. No entanto, uma miniatura de vídeo personalizada selecionada de um ativo de imagem existente é salva no JCR. O caminho do ativo selecionado é armazenado no nó do ativo de vídeo, como no seguinte caminho de exemplo:

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

A capacidade de personalizar uma miniatura de vídeo só estará disponível depois de aplicar um perfil de vídeo à pasta onde o vídeo está localizado.

Consulte também [Sobre miniaturas de vídeo no Dynamic Media - Modo híbrido](#about-video-thumbnails-in-dynamic-media-hybrid-mode).

### Adicionar uma miniatura de vídeo personalizada {#adding-a-custom-video-thumbnail}

Essas etapas se aplicam somente ao Dynamic Media em execução no modo &quot;Dynamicmedia_Scene7&quot;.

**Para adicionar uma miniatura de vídeo personalizada:**

1. Certifique-se de que você já fez o seguinte:

   * Uma pasta foi criada para os ativos de vídeo.
   * [Aplicado um perfil de vídeo à pasta](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   * [Carregou seus vídeos na pasta](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

1. Navegue até um ativo de vídeo carregado cuja imagem em miniatura você deseja alterar.
1. No modo de seleção de ativos, em **[!UICONTROL Exibição de lista]** ou **[!UICONTROL Exibição de cartão]**, toque no ativo de vídeo.
1. Na barra de ferramentas, toque no ícone **[!UICONTROL Properties]** (um círculo com um &quot;i&quot; nela).
1. Na página Propriedades do vídeo, toque em **[!UICONTROL Alterar miniatura]**.
1. Na página Alterar miniatura , siga um destes procedimentos:

   * Para usar um quadro do vídeo como a nova miniatura:

      * Na barra de ferramentas, toque em **[!UICONTROL Selecionar quadro do vídeo]**.
      * Toque no botão Reproduzir e toque no botão Pausar no quadro que deseja capturar como a nova miniatura do vídeo.
   * Para usar um ativo de imagem como a nova miniatura:

      * Na barra de ferramentas, toque em **[!UICONTROL Selecionar miniatura do Assets]**.
      * Toque em **[!UICONTROL Selecionar Miniatura]**.
      * Navegue até um ativo de imagem carregado e publicado anteriormente que deseja usar. Observe que o ativo será redimensionado automaticamente para servir como uma imagem em miniatura do vídeo.
      * Selecione o ativo de imagem e toque em **[!UICONTROL Selecionar]**.


1. Na página Alterar miniatura , toque em **[!UICONTROL Salvar alteração]**.
1. Na página Propriedades do vídeo, no canto superior direito, toque em **[!UICONTROL Salvar e fechar]**.

## Sobre miniaturas de vídeo no Dynamic Media - Modo híbrido {#about-video-thumbnails-in-dynamic-media-hybrid-mode}

Você pode escolher entre uma das dez imagens em miniatura geradas automaticamente pelo Dynamic Media para adicionar ao vídeo. O reprodutor de vídeo exibe a miniatura selecionada quando um ativo de vídeo é usado com o componente Dynamic Media no ambiente de criação do AEM Sites, AEM Mobile ou AEM Screens. A miniatura serve como uma imagem estática que melhor representa o conteúdo de todo o vídeo e estimula ainda mais os usuários a clicar no botão Reproduzir .

Com base no tempo total do vídeo, o Dynamic Media captura dez imagens em miniatura (padrão) em 1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81% e 91% no vídeo. As dez miniaturas persistem, o que significa que, se você decidir escolher uma miniatura diferente posteriormente, não precisará gerar novamente a série. Você visualiza as dez imagens em miniatura e, em seguida, seleciona aquela que deseja usar com o vídeo. Se quiser mudar para o padrão, use o CRXDE Lite para configurar o intervalo de tempo em que as imagens em miniatura são geradas. Por exemplo, se você quiser gerar apenas uma série de quatro imagens em miniatura espaçadas uniformemente a partir do seu vídeo, é possível configurar o tempo do intervalo em 24%, 49%, 74% e 99%.

Idealmente, você pode adicionar uma miniatura de vídeo a qualquer momento depois de fazer upload do vídeo, mas antes de publicar o vídeo no seu site.

Se preferir, você pode optar por fazer upload de uma miniatura personalizada para representar seu vídeo em vez de usar uma miniatura gerada pelo Dynamic Media. Por exemplo, você pode criar uma imagem em miniatura personalizada que tenha o título do seu vídeo, uma imagem de abertura atraente ou uma imagem muito específica capturada do seu vídeo. A imagem de miniatura de vídeo personalizada carregada deve ter uma resolução máxima de 1280 x 720 pixels (largura mínima de 640 pixels) e não deve ser maior que 2 MB.

Consulte também [Sobre miniaturas de vídeo no Dynamic Media - Modo Scene7](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### Adicionar uma miniatura de vídeo {#adding-a-video-thumbnail}

Essas etapas se aplicam somente à Dynamic Media em execução no modo Híbrido.

**Para adicionar uma miniatura de vídeo:**

1. Navegue até um ativo de vídeo carregado que você deseja adicionar uma miniatura de vídeo.
1. No modo de seleção de ativo, na Exibição de lista ou na Exibição de cartão, toque no ativo de vídeo.
1. Na barra de ferramentas, toque no ícone **[!UICONTROL Exibir propriedades]** (um círculo com um &quot;i&quot; nela).
1. Na página Propriedades do vídeo, toque em **[!UICONTROL Alterar miniatura]**.
1. Na página Alterar miniatura , na barra de ferramentas, toque em **[!UICONTROL Selecionar quadro]**.

   O Dynamic Media gera uma série de imagens em miniatura do vídeo, com base no intervalo padrão ou no intervalo de tempo personalizado.

1. Visualize as imagens em miniatura geradas e selecione aquela que deseja adicionar ao vídeo.
1. Toque em **[!UICONTROL Salvar alteração]**.

   A imagem em miniatura do vídeo é atualizada para usar a miniatura selecionada. Posteriormente, se decidir alterar a imagem em miniatura, você poderá retornar à página **[!UICONTROL Alterar miniatura]** e selecionar uma nova.

   Se você configurou novos intervalos de tempo padrão, ou carregou um novo vídeo para substituir o vídeo existente, será necessário ter o Dynamic Media regenerando as miniaturas.

   Consulte [Configurar o intervalo de tempo padrão em que as miniaturas de vídeo são geradas](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

#### Configurar o intervalo de tempo padrão em que as miniaturas de vídeo são geradas {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

Ao configurar e salvar o novo intervalo padrão, a alteração se aplica automaticamente somente aos vídeos que você fizer upload no futuro. Ele não aplica automaticamente o novo padrão aos vídeos que você carregou anteriormente. Para vídeos existentes, você deve gerar novamente as miniaturas.

Consulte [Adicionar uma miniatura de vídeo](#adding-a-video-thumbnail).

**Para configurar o intervalo de tempo padrão em que as miniaturas de vídeo são geradas:**

1. No Experience Manager, toque em **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.

1. Na página CRXDE Lite, no painel de diretório à esquerda, navegue até `o etc/dam/imageserver/configuration/jcr:content/settings.`

   se o painel do diretório não estiver visível, talvez seja necessário tocar no ícone >> à esquerda da guia Home .

1. No painel inferior direito, na guia Propriedades, toque duas vezes em `thumbnailtime`.
1. Na caixa de diálogo Editar hora da miniatura, use os campos de texto para inserir valores de intervalo como porcentagens.

   * Toque no ícone de sinal de adição (+) para adicionar um ou mais campos de valor de intervalo. Talvez seja necessário rolar até a parte inferior da caixa de diálogo para ver o ícone .
   * Toque no ícone do sinal de menos (-) à direita de um campo de valor de intervalo para excluí-lo da lista.
   * Toque no ícone de seta para cima e no ícone de seta para baixo para reordenar os valores do intervalo.

1. Toque em **[!UICONTROL OK]** para retornar à guia Propriedades.
1. Próximo ao canto superior esquerdo da página do CRXDE Lite, toque em **[!UICONTROL Salvar tudo]** e toque no ícone Voltar início no canto superior esquerdo para retornar ao AEM.

   Consulte [Adicionar uma miniatura de vídeo.](#adding-a-video-thumbnail)

### Adicionar uma miniatura de vídeo personalizada {#adding-a-custom-video-thumbnail-1}

Essas etapas se aplicam somente à Dynamic Media em execução no modo Híbrido.

**Para adicionar uma miniatura de vídeo personalizada:**

1. Navegue até um ativo de vídeo carregado que você deseja adicionar uma miniatura de vídeo personalizada.
1. No modo de seleção de ativo, na Exibição de lista ou na Exibição de cartão, toque no ativo de vídeo.
1. Na barra de ferramentas, toque no ícone **[!UICONTROL Exibir propriedades]** (um círculo com um &quot;i&quot; nela).
1. Na página Propriedades do vídeo, toque em **[!UICONTROL Alterar miniatura]**.
1. Na página Alterar miniatura , na barra de ferramentas, toque em **[!UICONTROL Fazer upload de nova miniatura]**.
1. Navegue até uma imagem em miniatura que deseja usar, selecione-a e toque em **[!UICONTROL Abrir]** para começar a carregar a imagem no AEM. Após o upload, certifique-se de publicar a imagem.
1. Depois de fazer upload e publicar a imagem com êxito, na página Alterar miniatura , toque em **[!UICONTROL Salvar alterações]**.

   A miniatura personalizada é adicionada ao vídeo.
