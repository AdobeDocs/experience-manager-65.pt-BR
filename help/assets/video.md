---
title: Vídeo no Dynamic Media
description: Saiba como trabalhar com vídeo no Dynamic Media, como práticas recomendadas para codificação de vídeos, publicação de vídeos no YouTube e exibição de relatórios de vídeo. Saiba também como adicionar legendas ocultas, legendas ou marcadores de capítulo aos vídeos.
mini-toc-levels: 3
uuid: 97f311a3-a227-479a-91bf-fb54ecd1a55d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 1103b849-0042-4e11-b170-38ee81dd0157
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 28cf9e39-cab4-4278-b6c9-e84cc31964db
source-git-commit: 3430897fc98aecbcf6cc7bf6bdc9b3df24e92366
workflow-type: tm+mt
source-wordcount: '8098'
ht-degree: 3%

---

# Vídeo no Dynamic Media {#video}

Esta seção descreve como trabalhar com vídeo no Dynamic Media.

## Início rápido: Vídeos {#quick-start-videos}

A seguinte descrição passo a passo do fluxo de trabalho foi criada para ajudá-lo a ativar e executar rapidamente com conjuntos de vídeos adaptáveis no Dynamic Media. Após cada etapa, há referências cruzadas para os cabeçalhos de tópicos, onde você pode encontrar mais informações.

>[!IMPORTANT]
>
>Antes de trabalhar com vídeo no Dynamic Media, verifique se o administrador do Adobe Experience Manager já ativou e configurou o Dynamic Media Cloud Services no modo Dynamic Media - Scene7 ou Dynamic Media - Modo híbrido.
>
>* Consulte [Configurar Dynamic Media Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) em Configuração do Dynamic Media - Modo Scene7 e [Solução de problemas do Dynamic Media - Modo Scene7](/help/assets/troubleshoot-dms7.md).
>
>* Consulte [Configurar Dynamic Media Cloud Services](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services) em Configuração do Dynamic Media - Modo híbrido.
>
>Problema de reprodução de vídeo conhecido no Dynamic Media *somente no Experience Manager 6.5.9.0*:
>
>* Se um vídeo publicado for atualizado, ele deverá ser publicado novamente para refletir as alterações no delivery.
>


1. **Fazer upload de seus vídeos do Dynamic Media** fazendo o seguinte:

   * Crie seu próprio perfil de codificação de vídeo. Ou você pode simplesmente usar o predefinido _Codificação de vídeo adaptável_ perfil que vem com o Dynamic Media.

      * [Criar um perfil de codificação de vídeo](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * Saiba mais sobre [Práticas recomendadas para codificação de vídeo](#best-practices-for-encoding-videos).
   * Associe o perfil de processamento de vídeo a uma ou mais pastas, onde você fará upload dos vídeos de origem primária.

      * [Aplicar um perfil de vídeo a pastas](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).
      * Saiba mais sobre [Práticas recomendadas para organizar ativos digitais para usar perfis de processamento](/help/assets/organize-assets.md).
      * Saiba mais sobre [Organizar ativos digitais](/help/assets/organize-assets.md).
   * Faça upload dos vídeos de origem primária para as pastas. Ao adicionar vídeos à pasta, eles são codificados de acordo com o perfil de processamento de vídeo atribuído à pasta.

      * O Dynamic Media oferece suporte principalmente a vídeos de forma curta, com duração máxima de 30 minutos e resolução mínima superior a 25 x 25.
      * Você pode fazer upload de arquivos de vídeo com até 15 GB cada.
      * [Fazer upload de seus vídeos](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).
      * Saiba mais sobre [Formatos de arquivo de entrada suportados](/help/assets/assets-formats.md#supported-multimedia-formats).
   * Monitorar como [a codificação de vídeo está progredindo](#monitoring-video-encoding-and-youtube-publishing-progress) na visualização de ativo ou fluxo de trabalho.




1. **Gerenciar os vídeos do Dynamic Media** executando um dos seguintes procedimentos:

   * Organizar, navegar e pesquisar ativos de vídeo

      * [Organizar ativos digitais](/help/assets/organize-assets.md)
Saiba mais sobre [Práticas recomendadas para organizar ativos digitais para usar perfis de processamento](organize-assets.md)

      * [Pesquisar ativos de vídeo](search-assets.md#custompredicates) ou [Pesquisar ativos](/help/assets/search-assets.md)
   * Visualizar e publicar ativos de vídeo

      * Visualize o vídeo de origem e as representações codificadas do vídeo, juntamente com as miniaturas associadas:
         [Visualizar vídeos](managing-video-assets.md#upload-and-preview-video-assets) ou [Visualizar ativos](previewing-assets.md)
         [Exibir representações de vídeo](video-renditions.md)
         [Gerenciar representações de vídeo](manage-assets.md#managing-renditions)

      * [Gerenciar predefinições do visualizador](managing-viewer-presets.md)
      * [Publicar ativos](publishing-dynamicmedia-assets.md)
   * Trabalhar com metadados de vídeo

      * Visualize as propriedades de uma representação de vídeo codificado, como taxa de quadros, taxa de bits de áudio e vídeo e codec:
         [Exibir propriedades de representação de vídeo](video-renditions.md)

      * Edite as propriedades do vídeo, como título, descrição e tags, e os campos de metadados personalizados:
         [Editar propriedades de vídeo](manage-assets.md#editing-properties)

      * [Gerenciar metadados para ativos digitais](metadata.md)
      * [Esquemas de metadados](metadata-schemas.md)
   * Revisar, aprovar e anotar vídeos e manter o controle total da versão

      * [Anotar vídeos](managing-video-assets.md#annotate-video-assets) ou [Anotar ativos](manage-assets.md#annotating)

      * [Criar uma versão](manage-assets.md#asset-versioning)
      * [Aplicar fluxos de trabalho a ativos](assets-workflow.md) ou veja [Iniciar um fluxo de trabalho em um ativo](manage-assets.md#starting-a-workflow-on-an-asset)

      * [Revisar ativos da pasta](bulk-approval.md)
      * [Projetos](../sites-authoring/projects.md)




1. **Publicar seus vídeos do Dynamic Media** executando um dos seguintes procedimentos:

   * Se você usa o Adobe Experience Manager como seu sistema de gerenciamento de conteúdo da Web, é possível adicionar vídeos diretamente às suas páginas da Web.

      * [Adicionar vídeos às suas páginas da Web](adding-dynamic-media-assets-to-pages.md).
   * Se você estiver usando um sistema de gerenciamento de conteúdo da Web de terceiros, poderá vincular ou incorporar vídeos às suas páginas da Web.

      * Integrar vídeo usando URL:
         [Vincular URLs ao aplicativo da Web](linking-urls-to-yourwebapplication.md).

      * Integre o vídeo usando o código incorporado na página da Web:
         [Incorporar o visualizador de vídeo em uma página da Web](embed-code.md).
   * [Publicar vídeos no YouTube](#publishing-videos-to-youtube).
   * [Gerar relatórios de vídeo](#viewing-video-reports).

   * [Adicionar legendas ao vídeo](#adding-captions-to-video).



## Trabalhar com vídeo no Dynamic Media {#working-with-video-in-dynamic-media}

O vídeo no Dynamic Media é uma solução completa que facilita a publicação de vídeos adaptáveis de alta qualidade para transmissão em várias telas, incluindo dispositivos móveis de desktop, iOS, Android™, BlackBerry® e Windows. Um Conjunto de vídeos adaptáveis agrupa versões do mesmo vídeo codificadas em diferentes formatos e taxas de bits, como 400 kbps, 800 kbps e 1000 kbps. O computador desktop ou dispositivo móvel detecta a largura de banda disponível.

Por exemplo, em um dispositivo móvel iOS, ele detecta uma largura de banda como 3G, 4G ou Wi-Fi. Em seguida, ele seleciona automaticamente o vídeo codificado direito dentre as várias taxas de bits de vídeo no Conjunto de vídeos adaptáveis. O vídeo é transmitido em desktops, dispositivos móveis ou tablets.

Além disso, a qualidade do vídeo é alternada dinamicamente automaticamente se as condições da rede mudarem no desktop ou no dispositivo móvel. Além disso, se um cliente entrar no modo de tela cheia em um desktop, o Adaptive Video Set responde usando uma resolução melhor, melhorando a experiência de visualização do cliente. O uso de conjuntos de vídeos adaptáveis fornece a melhor reprodução possível para os clientes que reproduzem o vídeo do Dynamic Media em várias telas e dispositivos.

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

* Legenda de vídeo em todos os visualizadores de vídeo do HTML5.
* Organize, navegue e pesquise vídeos com suporte completo a metadados para o gerenciamento eficiente dos ativos de vídeo.
* Forneça Conjuntos de Vídeos Adaptativos para a Web e para desktops e dispositivos móveis, incluindo iPhone, iPad, Android™, BlackBerry® e telefone Windows.

O streaming de vídeo adaptável é compatível com várias plataformas iOS. Consulte [Guia de referência de visualizadores do Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html#video).

O Dynamic Media oferece suporte para reprodução de vídeo móvel para vídeo MP4 H.264. Você pode encontrar dispositivos BlackBerry® que suportam este formato de vídeo no seguinte endereço: [Formatos de vídeo compatíveis com o BlackBerry®](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

Você pode encontrar dispositivos Windows compatíveis com este formato de vídeo no seguinte endereço: [Codecs de mídia compatíveis com o Windows Phone 8](https://learn.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs)



* Reproduzir o vídeo usando as Predefinições do visualizador de vídeo do Dynamic Media, incluindo o seguinte:

   * Visualizadores de vídeo individuais.
   * Visualizadores de mídia mista que combinam conteúdo de vídeo e imagem.

* Configure players de vídeo para atender às suas necessidades de marca.
* Integre vídeo ao seu site, site móvel ou aplicativo móvel com um URL simples ou código incorporado.

<!-- See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample. -->

Consulte também [Visualizadores do Experience Manager Assets e Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) e [Visualizadores somente de ativos do Experience Manager](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

## Prática recomendada: Uso do visualizador de vídeo do HTML5 {#best-practice-using-the-html-video-viewer}

As predefinições do visualizador de vídeo do Dynamic Media HTML5 são players de vídeo robustos. Você pode usá-los para evitar muitos problemas comuns associados à reprodução do vídeo no HTML5. E problemas associados a dispositivos móveis, como falta de entrega adaptável de streaming de taxa de bits e alcance limitado do navegador de desktop.

No lado de design do reprodutor, é possível projetar a funcionalidade do reprodutor de vídeo usando ferramentas de desenvolvimento da Web padrão. Por exemplo, você pode projetar botões, controles e imagens de fundo de pôster personalizadas usando HTML5 e CSS para ajudá-lo a alcançar seus clientes com uma aparência personalizada.

No lado da reprodução do visualizador, ele detecta automaticamente o recurso de vídeo do navegador. Em seguida, ele serve o vídeo usando HLS (HTTP Live Streaming) ou DASH (Dynamic Adaptive Streaming over HTTP) , também conhecido como transmissão adaptável da taxa de bits. Ou, se esses métodos de entrega não estiverem presentes, então HTML5 progressivo será usado.

Ao combinar em um único reprodutor o seguinte:

* A capacidade de projetar os componentes de reprodução usando HTML5 e CSS
* Ter reprodução incorporada
* Use streaming adaptável e progressivo dependendo da capacidade do navegador

Você estende o alcance do seu conteúdo de mídia avançada para usuários de desktop e de dispositivos móveis e garante uma experiência de vídeo simplificada.

Consulte também [Sobre visualizadores do HTML5](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

### Reprodução de vídeo em computadores desktop e dispositivos móveis usando o visualizador de vídeo HTML5 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

Para streaming de vídeo adaptável para desktop e dispositivos móveis, os vídeos usados para alternância de taxa de bits são baseados em todos os vídeos MP4 no Adaptive Video Set.

A reprodução de vídeo ocorre usando DASH ou HLS, ou o download de vídeo progressivo. Em versões anteriores do Experience Manager, como 6.0, 6.1 e 6.2, os vídeos eram transmitidos via HTTP.

No Experience Manager 6.3 e mais, os vídeos agora são transmitidos por HTTPS (ou seja, DASH ou HLS) porque o URL do serviço de gateway do DM sempre usa HTTPS também. Não há impacto do cliente nesse comportamento padrão. Ou seja, o streaming de vídeo sempre ocorre por HTTPS, a menos que não seja suportado pelo navegador. (ver quadro seguinte). Por conseguinte,

* Se você tiver um site HTTPS com streaming de vídeo HTTPS, o streaming estará bom.
* Se você tiver um site HTTP com streaming de vídeo HTTPS, o streaming estará correto e não haverá problemas de conteúdo misto no navegador da Web.

O DASH é o padrão internacional e o HLS é um padrão da Apple. Ambos são usados para streaming de vídeo adaptável. Além disso, ambas as tecnologias ajustam automaticamente a reprodução com base na capacidade da largura de banda da rede. Ele também permite que o cliente &quot;procure&quot; em qualquer ponto do vídeo, sem precisar aguardar o download do restante do vídeo.

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
   <td>Desktop</td>
   <td>Internet Explorer 9 e 10</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Internet Explorer 11+</td>
   <td>No Windows 8 e no Windows 10 - Forçar o uso de HTTPS sempre que DASH* ou HLS for solicitado. Limitação conhecida: HTTP no DASH* ou HLS não funciona nesta combinação de navegador/sistema operacional<br /> <br /> No Windows 7 - Download progressivo. Usa a lógica padrão para selecionar o protocolo HTTP versus HTTPS.</td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Firefox 23-44</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Firefox 45 ou superior</td>
   <td>Fluxo de taxa de bits adaptável DASH* ou HLS.</td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Chrome</td>
   <td>Fluxo de taxa de bits adaptável DASH* ou HLS.</td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Safari (Mac)</td>
   <td>Fluxo de taxa de bits adaptável HLS.</td>
  </tr>
  <tr>
   <td>Móvel</td>
   <td>Chrome (Android™ 6 ou anterior)</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Móvel</td>
   <td>Chrome (Android™ 7 ou posterior)</td>
   <td>Fluxo de taxa de bits adaptável DASH* ou HLS.</td>
  </tr>
  <tr>
   <td>Móvel</td>
   <td>Android™ (navegador padrão)</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Móvel</td>
   <td>Safari (iOS)</td>
   <td>Fluxo de taxa de bits adaptável HLS.</td>
  </tr>
  <tr>
   <td>Móvel</td>
   <td>Chrome (iOS)</td>
   <td>Fluxo de taxa de bits adaptável HLS.</td>
  </tr>
  <tr>
   <td>Móvel</td>
   <td>BlackBerry®</td>
   <td>Fluxo de taxa de bits adaptável DASH* ou HLS./td&gt;
  </tr>
 </tbody>
</table>

>[!IMPORTANT]
>
>*Para usar o DASH em seus vídeos, primeiro ele deve ser ativado pelo Suporte técnico do Adobe em sua conta. Consulte [Habilitar o DASH em sua conta](#enable-dash).

## Arquitetura da solução de vídeo Dynamic Media {#architecture-of-dynamic-media-video-solution}

O gráfico a seguir mostra o fluxo de trabalho de criação geral de vídeos que são carregados e codificados por meio do DMGgateway (no modo Dynamic Media Hybrid) e disponibilizados para consumo público.

![chlimage_1-427](assets/chlimage_1-427.png)

## Arquitetura de publicação híbrida para vídeos {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## Práticas recomendadas para codificação de vídeos {#best-practices-for-encoding-videos}

O **Codificar vídeo no Dynamic Media** O fluxo de trabalho codifica o vídeo se você tiver ativado o Dynamic Media e configurado os serviços da nuvem de vídeo. Esse fluxo de trabalho captura o histórico do processo de fluxo de trabalho e as informações de falha. Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress). Se você ativou o Dynamic Media e configurou os serviços da nuvem de vídeo, a variável **[!UICONTROL Codificar vídeo no Dynamic Media]** O fluxo de trabalho entra em vigor automaticamente ao carregar um vídeo. (Se você não estiver usando o Dynamic Media, a variável **[!UICONTROL Ativo de atualização DAM]** O fluxo de trabalho entra em vigor.)

<!-- DEAD The following are best-practice tips for encoding source video files.

For advice about video encoding, see [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en).

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en). -->

### Arquivos de vídeo de origem {#source-video-files}

Ao codificar um arquivo de vídeo, use um arquivo de vídeo de origem com a maior qualidade possível. Evite usar arquivos de vídeo previamente codificados, pois esses arquivos já estão compactados, e uma codificação adicional criará um vídeo de qualidade inferior.

* O Dynamic Media oferece suporte principalmente a vídeos de forma curta, com duração máxima de 30 minutos e resolução mínima superior a 25 x 25.
* Você pode fazer upload de arquivos de vídeo de origem primária com até 15 GB cada.

A tabela a seguir descreve o tamanho recomendado, a proporção e a taxa mínima de bits que seus arquivos de vídeo de origem devem ter antes de codificá-los:

| Tamanho | Taxa de proporção | Taxa mínima de bits |
|--- |--- |--- |
| 1024 X 768 | 4:3 | 4500 kbps para a maioria dos vídeos. |
| 1280 X 720 | 16:9 | 3000 - 6000 kbps, dependendo da quantidade de movimento no vídeo. |
| 1920 X 1080 | 16:9 | 6000 - 8000 kbps, dependendo da quantidade de movimento no vídeo. |

### Obter os metadados de um arquivo {#obtaining-a-file-s-metadata}

Você pode obter os metadados de um arquivo ao visualizar seus metadados usando uma ferramenta de edição de vídeo ou um aplicativo projetado para obter metadados. A seguir estão as instruções para usar MediaInfo, um aplicativo de terceiros, para obter os metadados de um arquivo de vídeo:

1. Ir para [Download do MediaInfo](https://mediaarea.net/en/MediaInfo/Download).
1. Selecione e baixe o instalador da versão da GUI e siga as instruções de instalação.
1. Após a instalação, clique com o botão direito do mouse no arquivo de vídeo (somente Windows) e selecione MediaInfo ou abra MediaInfo e arraste o arquivo de vídeo para o aplicativo. Você verá todos os metadados associados ao arquivo de vídeo, incluindo largura, altura e fps.

### Taxa de proporção {#aspect-ratio}

Ao escolher ou criar uma predefinição de codificação de vídeo para o arquivo de vídeo de origem primária, certifique-se de que a predefinição tenha a mesma proporção de aspecto do arquivo de vídeo de origem primária. A proporção é a relação entre a largura e a altura do vídeo.

Para determinar a proporção de um arquivo de vídeo, obtenha os metadados do arquivo e anote a largura e a altura do arquivo (consulte Obter os metadados de um arquivo acima). Em seguida, use essa fórmula para determinar a proporção:

largura/altura = proporção

A tabela a seguir descreve como os resultados da fórmula são traduzidos para opções comuns de proporção:

| Resultado da fórmula | Taxa de proporção |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

Por exemplo, um vídeo com 1440 largura x 1080 altura tem uma proporção largura/altura de 1440/1080 ou 1,33. Nesse caso, você escolhe uma predefinição de codificação de vídeo com uma proporção de aspecto 4:3 para codificar o arquivo de vídeo.

### Taxa de bits {#bitrate}

A taxa de bits é a quantidade de dados codificada para formar um único segundo de reprodução de vídeo. A taxa de bits é medida em kilobits por segundo (Kbps).

>[!NOTE]
>
>Como todos os codecs usam compactação com perdas, a taxa de bits é o fator mais importante na qualidade do vídeo. Com a compactação com perdas, quanto mais você compacta um arquivo de vídeo, mais a qualidade é degradada. Por isso, todas as outras características são iguais (resolução, taxa de quadros e codec), quanto menor a taxa de bits, menor a qualidade do arquivo compactado.

Ao selecionar uma codificação de taxa de bits, você pode escolher dois tipos:

* **[!UICONTROL Codificação constante da taxa de bits]** (CBR) - Durante a codificação de CBR, a taxa de bits ou o número de bits por segundo é mantido o mesmo durante todo o processo de codificação. A codificação CBR mantém a taxa de dados definida para sua configuração durante todo o vídeo. Além disso, a codificação CBR não otimiza arquivos de mídia para qualidade, mas salva no espaço de armazenamento.
Use o CBR se o vídeo contiver um nível de movimento semelhante em todo o vídeo. O CBR é mais usado para transmissão de conteúdo de vídeo. Consulte também [Usar parâmetros de codificação de vídeo personalizados](/help/assets/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL Codificação da taxa de bits variável]** (VBR) - A codificação VBR ajusta a taxa de dados para baixo e para o limite superior que você definiu, com base nos dados exigidos pelo compressor. Essa funcionalidade significa que, durante um processo de codificação VBR, a taxa de bits do arquivo de mídia aumenta ou diminui dinamicamente, dependendo das necessidades de taxa de bits dos arquivos de mídia.
O VBR demora mais para codificar, mas produz os resultados mais favoráveis; a qualidade do arquivo de mídia é superior. O VBR é usado mais frequentemente para entrega progressiva de conteúdo de vídeo em http.

Quando você usa VBR versus CRB?
Ao selecionar VBR versus CBR, quase sempre é recomendado usar VBR para seus arquivos de mídia. O VBR fornece arquivos de maior qualidade a taxas de bits competitivas. Ao usar o VBR, certifique-se de usar com a codificação de duas etapas e definir a taxa de bits máxima para ser 1,5x a taxa de bits do vídeo de destino.

Ao escolher uma predefinição de codificação de vídeo, lembre-se da velocidade de conexão do usuário final de destino. Escolha uma predefinição com uma taxa de dados de 80% dessa velocidade. Por exemplo, se a velocidade de conexão do usuário final de destino for 1000 Kbps, a melhor predefinição é aquela com uma taxa de dados de vídeo de 800 Kbps.

Esta tabela descreve a taxa de dados de velocidades de conexão típicas.

| Velocidade (Kbps) | Tipo de conexão |
|--- |--- |
| 256 | Conexão discada. |
| 800 | Conexão móvel típica. Para essa conexão, direcione uma taxa de dados no intervalo de 400 a um máximo de 800 para experiências 3G. |
| 2000 | Conexão típica de desktop de banda larga. Para esta conexão, direcione uma taxa de dados no intervalo de 800-2000 Kbps, com a maioria dos destinos com média de 1200-1500 Kbps. |
| 5000 | Conexão típica de alta banda larga. A codificação nesse intervalo superior não é recomendada porque a entrega de vídeo nessa velocidade não está disponível para a maioria dos consumidores. |

### Resolução {#resolution}

**Resolução** descreve a altura e a largura de um arquivo de vídeo em pixels. A maioria dos vídeos de origem é armazenada em alta resolução (por exemplo, 1920 x 1080). Para fins de transmissão, o vídeo de origem é compactado em uma resolução menor (640 x 480 ou menor).

A resolução e a taxa de dados são dois fatores totalmente vinculados que determinam a qualidade do vídeo. Para manter a mesma qualidade de vídeo, quanto maior o número de pixels em um arquivo de vídeo (quanto maior a resolução), maior deverá ser a taxa de dados. Por exemplo, considere o número de pixels por quadro em uma resolução de 320 x 240 e um arquivo de vídeo de resolução de 640 x 480:

| Resolução | Pixels por quadro |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

O arquivo de 640 x 480 tem quatro vezes mais pixels por quadro. Para atingir a mesma taxa de dados para essas duas resoluções de exemplo, aplique quatro vezes a compactação no arquivo 640 x 480, o que pode reduzir a qualidade do vídeo. Portanto, uma taxa de dados de vídeo de 250 Kbps produz uma exibição de alta qualidade com uma resolução de 320 x 240, mas não com resolução de 640 x 480.

Em geral, quanto maior a taxa de dados, melhor a aparência do vídeo e maior a resolução usada, maior a taxa de dados que você deve manter a qualidade de visualização (em comparação com resoluções mais baixas).

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
| Codificado | 640 x 360 | 3 | 3 |
| Codificado | 480 x 270 | 4 | 4 |

### Formato de arquivo de vídeo codificado {#encoded-video-file-format}

A Dynamic Media recomenda usar predefinições de codificação de vídeo MP4 H.264. Como os arquivos MP4 usam o codec de vídeo H.264, ele fornece vídeo de alta qualidade, mas em um tamanho de arquivo compactado.

### Habilitar o DASH em sua conta {#enable-dash}

O DASH (Digital Adaptive Streaming over HTTP, transmissão adaptativa digital por HTTP) é o padrão internacional para transmissão de vídeo e é amplamente adotado em diferentes visualizadores de vídeo. Quando o DASH é ativado em sua conta, você obtém a opção de escolher DASH ou HLS para transmissão de vídeo adaptável. Ou você pode optar por ambos com a alternância automática entre reprodutores quando **[!UICONTROL auto]** é selecionado como o tipo de reprodução na predefinição do Visualizador.

Alguns dos principais benefícios de habilitar o DASH em sua conta incluem o seguinte:

* Compacte o vídeo de fluxo DASH para transmissão adaptável da taxa de bits. Esse método leva a uma maior eficiência do delivery. O streaming adaptativo garante a melhor experiência de visualização para seus clientes.
* Streaming otimizado pelo navegador com switches Dynamic Media players entre streaming HLS e DASH para garantir a melhor qualidade de serviço. O reprodutor de vídeo alterna automaticamente para HLS quando um navegador Safari é usado.
* Você pode configurar seu método de transmissão preferido (HLS ou DASH) editando a predefinição do visualizador de vídeo.
* A codificação otimizada de vídeo garante que nenhum armazenamento adicional seja usado durante a ativação do recurso DASH. Um único conjunto de codificações de vídeo é criado para HLS e DASH para otimizar os custos de armazenamento de vídeo.
* Ajuda a tornar a entrega de vídeo mais acessível para seus clientes.
* Obtenha o URL de transmissão por meio de APIs também.

   >[!IMPORTANT]
   >
   >Habilitar o DASH em sua conta está disponível atualmente apenas na Ásia-Pacífico e na América do Norte; em breve na Europa-Oriente Médio-África.

Habilitar o DASH em sua conta requer duas etapas:

* Configurar o Dynamic Media para usar o DASH, o que você pode fazer facilmente.
* Configuração do Experience Manager 6.5 para usar o DASH, que é feito por meio de um caso de Suporte ao cliente do Adobe criado e enviado.

**Para ativar o DASH em sua conta:**

1. **Configurar o Dynamic Media** - No Dynamic Media no Experience Manager 6.5, navegue até [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Procurar por **Fluxo avançado de vídeo AEM Assets Dynamic Media** sinalizador de recurso.
1. Marque a caixa de seleção para ativar (ativar) o DASH.
1. Selecione **[!UICONTROL Salvar]**.
1. **Configurar o Experience Manager 6.5** - [Use o Admin Console para iniciar a criação de um novo caso de suporte](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).
1. Siga as instruções para criar um caso de suporte, garantindo que você forneça as seguintes informações:

   * Nome do contato principal, email, telefone.
   * Nome da sua conta do Dynamic Media.
   * Especifique que deseja habilitar o DASH no Experience Manager 6.5.

1. O Suporte ao cliente do Adobe adiciona você à Lista de espera do cliente DASH com base na ordem em que as solicitações são enviadas.
1. Quando o Adobe estiver pronto para lidar com sua solicitação, o Suporte ao cliente entrará em contato com você para coordenar e definir uma data de destino para a ativação do DASH.
1. Você será notificado após a conclusão pelo Suporte ao cliente.
1. Crie seu [predefinição do visualizador de vídeo](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) como de costume.

## Exibir relatórios de vídeo {#viewing-video-reports}

>[!NOTE]
>
>Os relatórios de vídeo só estão disponíveis quando você executa o Dynamic Media - Modo híbrido.

Os Relatórios de vídeo exibem diversas métricas agregadas em um período especificado para ajudá-lo a monitorar *publicado* vídeos individuais e agregados estão funcionando como esperado. Os seguintes dados de métricas principais são agregados para todos os vídeos publicados em todo o seu site:

* Vídeos iniciados
* Taxa de Conclusão
* Tempo médio no vídeo
* Tempo total no vídeo
* Vídeos por visita

Uma tabela de todos *publicado* os vídeos também são listados para que você possa acompanhar os vídeos mais vistos em seu site com base no total de inícios de vídeo.

Ao tocar no nome de um vídeo na lista, ele mostra o relatório de retenção de público-alvo (lista suspensa) do vídeo no formato de um gráfico de linha. O gráfico exibe o número de visualizações em qualquer momento durante a reprodução do vídeo. Quando você reproduz o vídeo, a barra vertical é rastreada em sincronização com o indicador de hora no reprodutor. Quedas nos dados do gráfico de linha indicam onde o público-alvo sai do desinteresse.

Se o vídeo foi codificado fora do Adobe Experience Manager Dynamic Media, o gráfico de retenção de público-alvo (lista suspensa) e os dados de Porcentagem de reprodução na tabela não estarão disponíveis.

Consulte também [Configurar Dynamic Media Cloud Services](/help/assets/config-dynamic.md).

>[!NOTE]
>
>Os dados de rastreamento e relatórios se baseiam exclusivamente no uso do próprio reprodutor de vídeo do Dynamic Media e da predefinição associada do reprodutor de vídeo. Dessa forma, não é possível rastrear e gerar relatórios sobre os vídeos reproduzidos por meio de outros players de vídeo.

Por padrão, na primeira vez que você insere Relatórios de vídeo, o relatório exibe dados de vídeo que começam no primeiro dia do mês atual e terminam com a data do mês atual. No entanto, você pode substituir o intervalo de datas padrão especificando seu próprio intervalo de datas. Na próxima vez que você inserir os Relatórios de vídeo, será usado o intervalo de datas especificado.

Para que os relatórios de vídeo funcionem corretamente, uma ID de conjunto de relatórios é criada automaticamente quando o Dynamic Media Cloud Services é configurado. Ao mesmo tempo, a ID do conjunto de relatórios é enviada para o servidor de publicação, para que fique disponível para o recurso Copiar URL ao visualizar ativos. No entanto, essa funcionalidade exige que o servidor de publicação já esteja configurado. Se o servidor de Publicação não estiver configurado, você ainda poderá publicar para ver o relatório de vídeo. No entanto, você deve retornar à Configuração da Dynamic Media Cloud e tocar em **[!UICONTROL OK]**.

**Para exibir relatórios de vídeo:**

1. No canto superior esquerdo do Experience Manager, toque no logotipo do Experience Manager e, em seguida, no painel à esquerda, toque em **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Ativos]** > **[!UICONTROL Relatórios de vídeo]**.
1. Na página Relatórios de vídeo , execute um dos seguintes procedimentos:

   * Próximo ao canto superior direito, toque no **Atualizar relatório de vídeo** ícone .
Use Atualizar somente se a data final do relatório for o dia atual. Isso garante que você visualize o rastreamento de vídeo que ocorreu desde a última vez em que você executou o relatório.

   * Próximo ao canto superior direito, toque no **Seletor de data** ícone .
Especifique o intervalo de datas de início e término para o qual deseja obter os dados de vídeo e toque em **[!UICONTROL Executar relatório]**.

   A caixa de grupo Principais métricas identifica várias medidas agregadas para todas *publicado* vídeos em seu site.

1. Na tabela que lista os vídeos publicados principais, toque no nome de um vídeo para reproduzir o vídeo e também veja o relatório de retenção de público-alvo (drop-off) do vídeo.

### Exibir relatórios de vídeo com base em um visualizador de vídeo criado por meio do SDK do visualizador do Dynamic Media HTML5 {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

Se você usar um visualizador de vídeo pronto para uso fornecido pelo Dynamic Media ou se tiver criado uma predefinição de visualizador personalizada com base em um visualizador de vídeo pronto para uso, nenhuma etapa adicional será necessária para exibir relatórios de vídeo. No entanto, se você criou seu próprio visualizador de vídeo com base na API do SDK do visualizador do HTML5, use as seguintes etapas para garantir que seu visualizador de vídeo esteja enviando eventos de rastreamento para os Relatórios de vídeo do Dynamic Media.

Use o [Guia de referência de visualizadores do Adobe Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html) e [API do SDK do visualizador do HTML5](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) para criar seus próprios visualizadores de vídeo.

**Para exibir relatórios de vídeo com base em um visualizador de vídeo criado usando o Dynamic Media HTML5 Viewer SDK:**

1. Navegue até qualquer ativo de vídeo publicado.
1. Próximo ao canto superior esquerdo da página do ativo, na lista suspensa, selecione **[!UICONTROL Visualizadores]**.
1. Selecione qualquer predefinição do visualizador de vídeo e copie o código incorporado.
1. No código incorporado, encontre a linha com o seguinte:

   `videoViewer.setParam("config2", "<value>");`

   O `config2` ativa o rastreamento em visualizadores do HTML5. Também é uma predefinição específica da empresa que contém as informações de configuração dos Relatórios de vídeo e das configurações específicas do Adobe Analytics para o cliente.

   O valor correto do parâmetro config2 é encontrado tanto no **[!UICONTROL Código incorporado]** quanto na função de cópia **[!UICONTROL URL]**. No URL do comando de cópia **[!UICONTROL URL]**, procure pelo parâmetro `&config2=<value>`. O valor é quase sempre `companypreset`, mas em algumas instâncias também pode ser `companypreset-1`, `companypreset-2` e assim por diante.

1. No código personalizado do visualizador de vídeo, adicione AppMeasurementBridge.jsp à página do visualizador fazendo o seguinte:

   * Primeiro, determine se você precisa da variável `&preset` parâmetro.

      Se a variável `config2` parâmetro é `companypreset`, você *not* need `&preset=parameter`.

      If `config2` for qualquer outra coisa, defina o parâmetro predefinido como `config2` parâmetro. Por exemplo, se `config2=companypreset-2`, adicionar `&param2=companypreset-2` para o URL AppMeasurementBridge.jsp.

   * Em seguida, adicione o script AppMeasurementBridge.jsp:

      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. Crie o componente TrackingManager fazendo o seguinte:

   * Depois de chamar `s7sdk.Util.init();`, crie uma instância TrackingManager para rastrear eventos, adicionando o seguinte:

      `var trackingManager = new s7sdk.TrackingManager();`

   * Conecte componentes ao TrackingManager fazendo o seguinte:

      No `s7sdk.Event.SDK_READY` manipulador de eventos, anexe o componente que deseja rastrear ao TrackingManager.

      Por exemplo, se o componente for `videoPlayer`, adicionar

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

## Adicionar legendas ou legendas ocultas ao vídeo {#adding-captions-to-video}

Você pode estender o alcance de seus vídeos para os mercados globais adicionando legendas ocultas a vídeos individuais ou aos Conjuntos de vídeos adaptáveis. Ao adicionar legendas ocultas, evite a necessidade de dublar o áudio ou a necessidade de usar alto-falantes nativos para regravar o áudio para cada idioma diferente. O vídeo é reproduzido no idioma em que foi gravado. As legendas em idioma estrangeiro são exibidas para que pessoas de idiomas diferentes ainda possam entender a parte de áudio.

As legendas ocultas também permitem maior acessibilidade para pessoas surdas ou com deficiência auditiva.

>[!NOTE]
>
>O reprodutor de vídeo usado deve ser compatível com a exibição de legendas.

Consulte também [Acessibilidade no Dynamic Media](/help/assets/accessibility-dm.md).

O Dynamic Media converte arquivos de legenda para o formato JSON (Notação de objeto JavaScript). Essa conversão significa que você pode incorporar o texto JSON em uma página da Web como uma transcrição oculta, mas completa, do vídeo. Os mecanismos de pesquisa podem, então, rastrear e indexar o conteúdo para tornar os vídeos mais fáceis de serem descobertos e fornecer aos clientes detalhes adicionais sobre o conteúdo do vídeo.

Consulte [Fornecer conteúdo estático (não imagem)](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api) no *Ajuda da API de disponibilização e renderização de imagens do Dynamic Media* para obter mais informações sobre como usar a função JSON em um URL.

**Para adicionar legendas ou legendas ao vídeo:**

1. Use um aplicativo ou serviço de terceiros para criar sua legenda/arquivo de subtítulo de vídeo.

   Certifique-se de que o arquivo criado siga o padrão WebVTT (Web Video Text Tracks). A extensão de nome de arquivo de legendagem é .vtt. Você pode obter mais informações sobre o padrão de legendagem WebVTT.

   Consulte [WebVTT: O formato de Rastreamento de texto da Web](https://w3c.github.io/webvtt/).

   Há ferramentas e serviços gratuitos e premium que podem ser usados para criar arquivos de legenda/subtítulo fora do Dynamic Media. Por exemplo, para criar um arquivo de legenda de vídeo simples sem estilização, você pode usar a seguinte ferramenta de edição e criação de legendas online gratuitas:

   [Criador de legendas WebVTT](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   Para obter melhores resultados, use a ferramenta no Internet Explorer 9 ou superior, Google Chrome ou Safari.

   Na ferramenta, no **[!UICONTROL Inserir o URL do arquivo de vídeo]** cole o URL copiado do arquivo de vídeo e clique em **[!UICONTROL Carregar]**. Consulte [Obter um URL para um ativo](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) para obter o URL para o próprio arquivo de vídeo, o qual você pode colar no **[!UICONTROL Inserir o URL do campo de arquivo de vídeo]**. O Internet Explorer, o Chrome ou o Safari podem reproduzir nativamente o vídeo.

   Agora siga as instruções na tela do site para criar e salvar seu arquivo WebVTT. Quando terminar, copie o conteúdo do arquivo de legenda e o cole em um editor de texto simples e salve com um `.vtt` extensão do nome do arquivo.

   >[!NOTE]
   >
   >Para oferecer suporte global a legendas de vídeo em vários idiomas, o padrão WebVTT requer a criação de arquivos .vtt e chamadas separadas para cada idioma que você deseja suportar.

   Geralmente, você deseja nomear o arquivo VTT da legenda com o mesmo nome do arquivo de vídeo e anexá-lo à localidade do idioma, como -EN, -FR ou -DE. Ao fazer isso, ele pode ajudá-lo a automatizar a geração dos URLs de vídeo usando seu sistema de gerenciamento de conteúdo da Web existente.

1. No Experience Manager, faça upload do arquivo de legenda WebVTT no DAM.
1. Navegue até o *publicado* ativo de vídeo que você deseja associar ao arquivo de legenda carregado.

   Lembre-se de que os URLs só estão disponíveis para cópia *depois* que você *publicou* os ativos pela primeira vez.

   Consulte [Publicar ativos](/help/assets/publishing-dynamicmedia-assets.md).

1. Siga uma das seguintes opções:

   * Para obter uma experiência do visualizador de vídeo pop-up, toque em **[!UICONTROL URL]**. Na caixa de diálogo URL, selecione e copie o URL para a Área de transferência e, em seguida, passe o URL para um editor de texto simples. Anexe o URL copiado do vídeo com a seguinte sintaxe:

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      Observe que `,1` no final do caminho da legenda. Imediatamente após a `.vtt` extensão do nome do arquivo no caminho, você pode ativar (ativar) ou desativar (desativar) o botão de legenda na barra do reprodutor de vídeo, definindo como `,1` ou `,0`, respectivamente.

   * Para obter uma experiência de visualizador de vídeo incorporado, toque em **[!UICONTROL Código incorporado]**. Na caixa de diálogo Incorporar código, selecione e copie o código incorporado na Área de transferência e cole o código em um editor de texto simples. Anexe o código incorporado copiado com a seguinte sintaxe:

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      Observe que `,1` no final do caminho da legenda. Imediatamente após a `.vtt` extensão do nome do arquivo no caminho, você pode ativar (ativar) ou desativar (desativar) o botão de legenda na barra do reprodutor de vídeo, definindo como `,1` ou `,0`, respectivamente.

## Adicionar marcadores de capítulo ao vídeo {#adding-chapter-markers-to-video}

Você pode tornar seus vídeos de formulário longos mais fáceis de assistir e navegar adicionando marcadores de capítulo a vídeos individuais ou aos Conjuntos de vídeos adaptáveis. Quando um usuário reproduz o vídeo, ele pode clicar nos marcadores de capítulo na linha do tempo do vídeo (também conhecidos como depurador de vídeo) para navegar facilmente até o ponto de interesse. Ou podem ir imediatamente para novos conteúdos, demonstrações e tutoriais.

>[!NOTE]
>
>O reprodutor de vídeo usado deve suportar o uso de marcadores de capítulo. Os players de vídeo do Dynamic Media são compatíveis com marcadores de capítulo, mas o uso de players de vídeo de terceiros não é compatível.

Se desejar, você pode criar e marcar seu próprio visualizador de vídeo personalizado com capítulos em vez de usar uma predefinição do visualizador de vídeo. Para obter instruções sobre como criar seu próprio visualizador do HTML5 com navegação de capítulo, na API do SDK do visualizador do Adobe HTML5, consulte o cabeçalho &quot;Personalização do comportamento usando modificadores&quot; nas classes `s7sdk.video.VideoPlayer` e `s7sdk.video.VideoScrubber`. Consulte a [API do SDK do visualizador do HTML5](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) documentação.

<!-- If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

Você cria uma lista de capítulo para o vídeo da mesma forma que cria legendas. Ou seja, você cria um arquivo WebVTT. Observe, no entanto, que esse arquivo deve ser separado de qualquer arquivo de legenda da WebVTT que você também esteja usando; não é possível combinar legendas e capítulos em um arquivo WebVTT.

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

No exemplo acima, `Chapter 1` é o identificador de sinalização e é opcional. A hora de sinalização de `00:00:000 --> 01:04:364` especifica a hora de início e a hora de término do capítulo, em `00:00:000` formato. Os últimos três dígitos são milissegundos e podem ser deixados como `000`, se preferir. O título do capítulo de `The bicycle store behind it all` é a descrição real do conteúdo do capítulo. O identificador de sinalização, a hora de início e o título do capítulo são exibidos em uma pop-up de reprodutor de vídeo quando um usuário passa o ponteiro do mouse sobre um ponto de sinalização visual na linha do tempo do vídeo.

Como você está usando um visualizador de vídeo HTML5, certifique-se de que o arquivo de capítulo criado siga o padrão WebVTT (Web Video Text Tracks). A extensão do nome de arquivo do capítulo é `.vtt`. Você pode obter mais informações sobre o padrão de legendagem WebVTT.

Consulte [WebVTT: O formato de Rastreamento de texto da Web](https://w3c.github.io/webvtt/)

**Para adicionar navegação de capítulo de vídeo:**

1. Salve as `.vtt` na codificação UTF8, para evitar problemas com a representação de caracteres no texto do título do capítulo.

   Geralmente, você deseja nomear o arquivo VTT do capítulo com o mesmo nome do arquivo de vídeo e anexá-lo a capítulos. Ao fazer isso, ele pode ajudá-lo a automatizar a geração dos URLs de vídeo usando seu sistema de gerenciamento de conteúdo da Web existente.
1. No Experience Manager, faça upload do arquivo de capítulo WebVTT.

   Consulte [Fazer upload de ativos](/help/assets/manage-assets.md#uploading-assets).

1. Siga uma das seguintes opções:

   <table>
     <tbody>
      <tr>
       <td>Para obter uma experiência de visualizador de vídeo pop-up</td>
       <td>
       <ol>
       <li>Navegue até o <i>publicado </i>ativo de vídeo que você deseja associar ao arquivo de capítulo carregado. Lembre-se de que os URLs só estão disponíveis para cópia <i>depois</i> que você <i>publicou</i> os ativos pela primeira vez. Consulte <a href="/help/assets/publishing-dynamicmedia-assets.md">Publicar ativos.</a></li>
       <li>No menu suspenso, clique ou toque em <strong>Visualizadores</strong>.</li>
       <li>No painel à esquerda, toque ou clique no nome predefinido do visualizador de vídeo. Uma visualização do vídeo é aberta em uma página separada.</li>
       <li>No painel à esquerda, na parte inferior, clique em <strong>URL</strong>.</li>
       <li>Na caixa de diálogo URL, selecione e copie o URL para a Área de transferência e, em seguida, passe o URL para um editor de texto simples.</li>
       <li>Anexe o URL copiado do vídeo com a seguinte sintaxe para associá-lo ao URL copiado ao arquivo de capítulo:<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>Para uma experiência de visualizador de vídeo incorporado<br /> </td>
       <td>
       <ol>
       <li>Navegue até o <i>publicado </i>ativo de vídeo que você deseja associar ao arquivo de capítulo carregado. Lembre-se de que os URLs só estão disponíveis para cópia <i>depois</i> que você <i>publicou</i> os ativos pela primeira vez. Consulte <a href="/help/assets/publishing-dynamicmedia-assets.md">Publicar ativos.</a></li>
       <li>No menu suspenso, clique ou toque em <strong>Visualizadores</strong>.</li>
       <li>No painel à esquerda, toque ou clique no nome predefinido do visualizador de vídeo. Uma visualização do vídeo é aberta em uma página separada.</li>
       <li>No painel à esquerda, na parte inferior, clique em <strong>Incorporar</strong>.</li>
       <li>Na caixa de diálogo Incorporar código, selecione e copie o código inteiro para a Área de transferência e, em seguida, cole-o em um editor de texto simples.</li>
       <li>Anexe o código incorporado do vídeo à seguinte sintaxe para associá-lo ao URL copiado ao arquivo de capítulo:<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt&gt;"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

## Sobre miniaturas de vídeo no Dynamic Media - Modo Scene7 {#about-video-thumbnails-in-dynamic-media-scene-mode}

Uma miniatura de vídeo é uma versão reduzida de um quadro de vídeo ou um ativo de imagem que representa o vídeo para o cliente. A miniatura serve para incentivar um cliente a clicar no vídeo.

Todos os vídeos no Experience Manager devem ter uma miniatura associada; não é possível excluir uma miniatura sem substituí-la. Por padrão, ao carregar um vídeo no Experience Manager, o primeiro quadro é usado como miniatura. Entretanto, é possível personalizar a miniatura para fins de identidade visual ou de criação de marcas, por exemplo. Ao personalizar uma miniatura de vídeo, você pode reproduzir o vídeo e pausar no quadro que deseja usar. Ou, você pode selecionar um ativo de imagem que já foi carregado e *publicado* no gerenciador de ativos digitais.

Uma imagem em miniatura de vídeo personalizada selecionada em um vídeo não é extraída e salva no DAM como um ativo separado e distinto. No entanto, uma miniatura de vídeo personalizada selecionada de um ativo de imagem existente é salva no JCR. O caminho do ativo selecionado é armazenado no nó do ativo de vídeo, como no seguinte caminho de exemplo:

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

A capacidade de personalizar uma miniatura de vídeo só estará disponível depois de aplicar um perfil de vídeo à pasta onde o vídeo está localizado.

Consulte também [Sobre miniaturas de vídeo no Dynamic Media - Modo híbrido](#about-video-thumbnails-in-dynamic-media-hybrid-mode).

### Adicionar uma miniatura de vídeo personalizada {#adding-a-custom-video-thumbnail}

Essas etapas se aplicam somente ao Dynamic Media em execução no modo &quot;Dynamicmedia_Scene7&quot;.

**Para adicionar uma miniatura de vídeo personalizada:**

1. Certifique-se de que você já fez o seguinte:

   * Uma pasta foi criada para os ativos de vídeo.
   * [Aplicar um perfil de vídeo à pasta](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   * [Carregou seus vídeos na pasta](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

1. Navegue até um ativo de vídeo carregado cuja imagem em miniatura você deseja alterar.
1. No modo de seleção de ativos, em **[!UICONTROL Exibição de lista]** ou **[!UICONTROL Exibição de cartão]**, toque no ativo de vídeo.
1. Na barra de ferramentas, toque no botão **[!UICONTROL Propriedades]** ícone (um círculo com um &quot;i&quot; nele).
1. Na página Propriedades do vídeo, toque em **[!UICONTROL Alterar miniatura]**.
1. Na página Alterar miniatura , siga um destes procedimentos:

   * Para usar um quadro do vídeo como a nova miniatura:

      * Na barra de ferramentas, toque em **[!UICONTROL Selecionar quadro do vídeo]**.
      * Toque no botão Reproduzir e toque no botão Pausar no quadro que deseja capturar como a nova miniatura do vídeo.
   * Para usar um ativo de imagem como a nova miniatura:

      * Na barra de ferramentas, toque em **[!UICONTROL Selecionar miniatura dos ativos]**.
      * Toque **[!UICONTROL Selecionar miniatura]**.
      * Navegue até um ativo de imagem carregado e publicado anteriormente que você deseja usar. O ativo é redimensionado automaticamente para servir como uma imagem em miniatura do vídeo.
      * Selecione o ativo de imagem e toque em **[!UICONTROL Selecionar]**.


1. Na página Alterar miniatura , toque em **[!UICONTROL Salvar alteração]**.
1. Na página Propriedades do vídeo, no canto superior direito, toque em **[!UICONTROL Salvar e fechar]**.

## Sobre miniaturas de vídeo no Dynamic Media - Modo híbrido {#about-video-thumbnails-in-dynamic-media-hybrid-mode}

Você pode escolher entre uma das dez imagens em miniatura geradas automaticamente pelo Dynamic Media para adicionar ao vídeo. O reprodutor de vídeo exibe a miniatura selecionada quando um ativo de vídeo é usado com o componente Dynamic Media no ambiente de criação do Experience Manager Sites, Experience Manager Mobile ou Experience Manager Screens. A miniatura serve como uma imagem estática que melhor representa o conteúdo de todo o vídeo e estimula ainda mais os usuários a clicar no botão Reproduzir .

Com base no tempo total do vídeo, o Dynamic Media captura dez (padrão) imagens em miniatura. As imagens são capturadas em 1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81% e 91% no vídeo. As dez miniaturas persistem, o que significa que, se você decidir escolher uma miniatura diferente posteriormente, não precisará gerar novamente a série. Você visualiza as dez imagens em miniatura e, em seguida, seleciona aquela que deseja usar com o vídeo. Se quiser alterar para o padrão, use o CRXDE Lite para configurar o intervalo de tempo em que as imagens em miniatura são geradas. Por exemplo, se você quiser gerar apenas uma série de quatro imagens em miniatura espaçadas uniformemente a partir do seu vídeo, é possível configurar o tempo do intervalo em 24%, 49%, 74% e 99%.

Idealmente, você pode adicionar uma miniatura de vídeo a qualquer momento depois de fazer upload do vídeo, mas antes de publicar o vídeo no seu site.

Se preferir, você pode optar por fazer upload de uma miniatura personalizada para representar seu vídeo em vez de usar uma miniatura gerada pelo Dynamic Media. Por exemplo, você pode criar uma imagem em miniatura personalizada com o título do vídeo, uma imagem de abertura atraente ou uma imagem específica capturada do vídeo. A imagem de miniatura de vídeo personalizada que você faz upload deve ter uma resolução máxima de 1280 x 720 pixels (largura mínima de 640 pixels) e não ser maior que 2 MB.

Consulte também [Sobre miniaturas de vídeo no Dynamic Media - Modo Scene7](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### Adicionar uma miniatura de vídeo {#adding-a-video-thumbnail}

Essas etapas se aplicam somente à Dynamic Media em execução no modo Híbrido.

**Para adicionar uma miniatura de vídeo:**

1. Navegue até um ativo de vídeo carregado que você deseja adicionar uma miniatura de vídeo.
1. No modo de seleção de ativo, na Exibição de lista ou na Exibição de cartão, toque no ativo de vídeo.
1. Na barra de ferramentas, toque no botão **[!UICONTROL Propriedades da exibição]** ícone (um círculo com um &quot;i&quot; nele).
1. Na página Propriedades do vídeo, toque em **[!UICONTROL Alterar miniatura]**.
1. Na página Alterar miniatura , na barra de ferramentas, toque em **[!UICONTROL Selecionar quadro]**.

   O Dynamic Media gera uma série de imagens em miniatura do vídeo, com base no intervalo padrão ou no intervalo de tempo personalizado.

1. Visualize as imagens em miniatura geradas e selecione aquela que deseja adicionar ao vídeo.
1. Toque **[!UICONTROL Salvar alteração]**.

   A imagem em miniatura do vídeo é atualizada para usar a miniatura selecionada. Se decidir alterar a imagem em miniatura posteriormente, você poderá retornar ao **[!UICONTROL Alterar miniatura]** e selecione uma nova.

   Se você configurou novos intervalos de tempo padrão, ou carregou um novo vídeo para substituir o vídeo existente, peça para o Dynamic Media gerar novamente as miniaturas.

   Consulte [Configure o intervalo de tempo padrão em que as miniaturas de vídeo são geradas](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

#### Configure o intervalo de tempo padrão em que as miniaturas de vídeo são geradas {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

Ao configurar e salvar o novo intervalo padrão, a alteração se aplica automaticamente somente aos vídeos que você fizer upload no futuro. Ele não aplica automaticamente o novo padrão aos vídeos que você carregou anteriormente. Para vídeos existentes, você deve gerar novamente as miniaturas.

Consulte [Adicionar uma miniatura de vídeo](#adding-a-video-thumbnail).

**Para configurar o intervalo de tempo padrão em que as miniaturas de vídeo são geradas:**

1. No Experience Manager, toque em **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.

1. Na página CRXDE Lite, no painel de diretórios à esquerda, navegue até `o etc/dam/imageserver/configuration/jcr:content/settings.`

   se o painel do diretório não estiver visível, toque no ícone >> à esquerda da guia Início .

1. No painel inferior direito, na guia Propriedades, toque duas vezes em `thumbnailtime`.
1. No **[!UICONTROL Editar hora da miniatura]** use os campos de texto para inserir valores de intervalo como porcentagens.

   * Toque no ícone de sinal de adição (+) se desejar adicionar um ou mais campos de valor de intervalo. Se necessário, role até a parte inferior da caixa de diálogo para ver o ícone .
   * Toque no ícone do sinal de menos (-) à direita de um campo de valor de intervalo se desejar excluí-lo da lista.
   * Toque no ícone de seta para cima e no ícone de seta para baixo se desejar reordenar os valores do intervalo.

1. Toque **[!UICONTROL OK]** e retorne à guia Properties .
1. Próximo ao canto superior esquerdo da página do CRXDE Lite, toque em **[!UICONTROL Salvar tudo]** e toque no ícone Voltar ao início no canto superior esquerdo para retornar ao Experience Manager.

   Consulte [Adicionar uma miniatura de vídeo](#adding-a-video-thumbnail).

### Adicionar uma miniatura de vídeo personalizada {#adding-a-custom-video-thumbnail-1}

Essas etapas se aplicam somente à Dynamic Media em execução no modo Híbrido.

**Para adicionar uma miniatura de vídeo personalizada:**

1. Navegue até um ativo de vídeo carregado que você deseja adicionar uma miniatura de vídeo personalizada.
1. No modo de seleção de ativo, na Exibição de lista ou na Exibição de cartão, toque no ativo de vídeo.
1. Na barra de ferramentas, toque no botão **[!UICONTROL Propriedades da exibição]** ícone (um círculo com um &quot;i&quot; nele).
1. Na página Propriedades do vídeo, toque em **[!UICONTROL Alterar miniatura]**.
1. Na página Alterar miniatura , na barra de ferramentas, toque em **[!UICONTROL Fazer upload da nova miniatura]**.
1. Navegue até uma imagem em miniatura que deseja usar, selecione-a e toque em **[!UICONTROL Abrir]** para começar a carregar a imagem no Experience Manager. Após o upload, certifique-se de publicar a imagem.
1. Depois de fazer upload e publicar a imagem com êxito, na página Alterar miniatura , toque em **[!UICONTROL Salvar alterações]**.

   A miniatura personalizada é adicionada ao vídeo.

## Alterar o URL do Dynamic Media para ativos do Dynamic Media {#manifest-urls}

Os vídeos processados no Dynamic Media podem ser usados por meio de visualizadores prontos para uso e também acessando diretamente os URLs de manifesto e reproduzindo-os por meio de seus próprios visualizadores personalizados. Veja a seguir a API para buscar URLs de manifesto de um vídeo.

### Sobre a API getVideoManifestURI

O `getVideoManifestURI`A API é exposta por meio de c`q-scene7-api:com.day.cq.dam.scene7.api` e podem ser usados para gerar os seguintes URLs de manifesto:

```java
/**   
* Returns the manifest url for videos 
* @param resource video resource 
* @param manifestType type of video streaming manifest being requested 
* @param onlyIfPublished return a manifest only if the video is published 
* @return the manifest url for videos 
* 
* @throws Exception 
*/
@Nullable 
String getVideoManifestURI(Resource resource, ManifestType manifestType, boolean onlyIfPublished) throws Exception;
```

#### Parâmetros da API getVideoManifestURI

Essa API utiliza os três parâmetros a seguir:

| Parâmetro | Descrição |
| --- | --- |
| `resource` | O recurso correspondente ao vídeo que a Dynamic Media assimilou. |
| `manifestType` | Pode ser `ManifestType.DASH` ou `ManifestType.HLS` |
| `onlyIfPublished` | Defina como true no caso do uri de manifesto ser gerado somente se ele for publicado e disponível no nível de delivery. |

Para buscar os URLs de manifesto de vídeos usando o método acima, adicione um [perfil de codificação de vídeo](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) para uma pasta &quot;fazer upload de vídeos&quot;. O Dynamic Media processa esses vídeos com base nas codificações encontradas no arquivo de codificação de vídeo que foi atribuído à pasta. Agora você pode chamar a API acima para buscar URLs de manifesto dos vídeos carregados.

### Cenários de erro

A API retornará um valor nulo se houver erros. As exceções são registradas em logs de erro de Experience Manager. Todos esses erros registrados começam com `Could not generate Video Manifest URI`. Os seguintes cenários podem fazer com que esses erros ocorram:

* Um `IllegalArgumentException` é registrado para qualquer um dos seguintes:

   * O `resource` parâmetro transmitido é nulo.
   * O `resource` transmitido não é um vídeo.
   * O `manifestType` parâmetro transmitido é nulo.
   * O `onlyIfPublished` é passado como verdadeiro, mas o vídeo não é publicado.
   * O vídeo não foi assimilado usando um conjunto de vídeos adaptáveis do Dynamic Media.

* `IOException` é registrado quando há um problema ao se conectar ao Dynamic Media.
* `UnsupportedOperationException` é registrado quando um `manifestType` parâmetro passado é `ManifestType.DASH`, enquanto o vídeo não foi processado usando o formato DASH.

Este é um exemplo da API acima usando servlets escritos em *HTTPWhiteBoard* especificação. Selecione cada guia para a sintaxe do código.

>[!BEGINTABS]

>[!TAB Adicionar dependência em pom.xml]

+++**Adicionar dependência em pom.xml**

```java
dependency> 
     <groupId>com.day.cq.dam</groupId> 
     <artifactId>cq-scene7-api</artifactId> 
     <version>5.12.64</version> 
     <scope>provided</scope> 
</dependency> 
```

+++

>[!TAB Servlet de exemplo]

+++**Servlet de exemplo**

```java
@Component
        service = Servlet.class 
) 
@HttpWhiteboardServletPattern(value = ManifestServlet.SERVLET_PATTERN) 
@HttpWhiteboardContextSelect(value = Constants.SERVLET_CONTEXT_SELECTOR) 
public class ManifestServlet extends HttpServlet { 

   private static final Logger LOGGER = LoggerFactory.getLogger(ManifestServlet.class); 

   private final ObjectMapper objectMapper; 

    @Reference 
    private Scene7Service scene7Service; 

   public static final String SERVLET_PATTERN = Constants.VIDEO_API_PREFIX + "/manifestUrl"; 

   public ManifestServlet() {
         this.objectMapper = new ObjectMapper(); 
         objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL); 
   }

   @Override 

   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        final ResourceResolver resolver = getResourceResolver(request); 
        String assetPath = request.getParameter("assetPath"); 
        String manifest = request.getParameter("manifestType"); 
        String onlyIfPublished = request.getParameter("onlyIfPublished"); 
        Resource resource = resolver.getResource(assetPath); 
        response.setCharacterEncoding(StandardCharsets.UTF_8.toString()); 
        response.setContentType("application/json"); 
        if(resource == null) { 
            LOGGER.info("could not retrieve the resource from JCR"); 
            error("could not retrieve the resource from JCR", response); 
            return; 
        }

        String manifestUri = null; 

        try{ 
            ManifestType manifestType =  ManifestType.DASH; 
            if(manifest != null) { 
                manifestType = ManifestType.valueOf(manifest); 
            } 
            manifestUri = scene7Service.getVideoManifestURI(resource, manifestType, onlyIfPublished != null); 
            objectMapper.writeValue(response.getWriter(), new ManifestUrl(manifestUri)); 
            response.setContentType("application/json"); 
        } catch (Exception e) { 
            LOGGER.error(e.getMessage(), e); 
            error(String.format("Unable to get the manifest url for %s. %s", assetPath, e.getMessage()), response); 
        } 
    } 

    private ResourceResolver getResourceResolver(HttpServletRequest request) { 
        Object rr = request.getAttribute(AuthenticationSupport.REQUEST_ATTRIBUTE_RESOLVER); 
        if (!(rr instanceof ResourceResolver)) { 
            throw new IllegalStateException( 
                    "The request does not seem to have been created via Apache Sling's authentication mechanism."); 
        } else { 
            return (ResourceResolver) rr; 
        } 
    } 

    private void error(String errorMessage, HttpServletResponse response) throws IOException { 
        ManifestUrl errorManifest = new ManifestUrl(null); 
        errorManifest.setErrorMessage(errorMessage); 
        response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR); 
        objectMapper.writeValue(response.getWriter(), errorManifest); 
    } 
} 
```

+++

>[!TAB Classe de Resposta para servlet]

+++**Classe de Resposta para servlet**

```java
public class ManifestUrl extends VideoResponse { 
     String manifestUrl; 
     public ManifestUrl(String manifestUrl) { 
         this.manifestUrl = manifestUrl; 
     } 
     public String getManifestUrl() { 
         return manifestUrl; 
     } 
} 

public abstract class VideoResponse { 
     String errorString; 

     public String getErrorString() { 
         return errorString; 
     } 

     public void setErrorMessage(String errorString) { 
         this.errorString = errorString; 
     } 
} 
```

+++

>[!TAB Arquivo de constantes referenciado no servlet]

+++**Arquivo de constantes referenciado no servlet**

```java
public final class Constants { 

     private Constants() { 
     } 

     public static final String VIDEO_API_PREFIX = "/dynamicmedia/video"; 
     public static final String SERVLET_CONTEXT_SELECTOR = "(" + HttpWhiteboardConstants.HTTP_WHITEBOARD_CONTEXT_NAME + "=" + 
             DMSampleApiHttpContext.CONTEXT_NAME + ")"; 

 } 
```

+++

>[!TAB ServletContext]

+++**ServletContext**

Monte o servlet acima usando um `servletContext`. Este é um exemplo de `servletContext`.

```java
public class DMSampleApiHttpContext extends ServletContextHelper { 

 public static final String CONTEXT_NAME = "com.adobe.dmSample"; 
 public static final String CONTEXT_PATH = "/dmSample"; 

 private final MimeTypeService mimeTypeService; 

 private final AuthenticationSupport authenticationSupport; 

 /** 
  * Constructs a new context that will use the given dependencies. 
  * 
  * @param mimeTypeService Used when providing mime type of requests. 
  * @param authenticationSupport Used to authenticate requests with sling. 
  */ 
 @Activate 
 public DMSampleApiHttpContext(@Reference final MimeTypeService mimeTypeService, 
                               @Reference final AuthenticationSupport authenticationSupport) { 
     this.mimeTypeService = mimeTypeService; 
     this.authenticationSupport = authenticationSupport; 
 } 

 // ---------- HttpContext interface ---------------------------------------- 
 /** 
  * Returns the MIME type as resolved by the <code>MimeTypeService</code> or 
  * <code>null</code> if the service is not available. 
  */ 
 @Override 
 public String getMimeType(String name) { 
     MimeTypeService mtservice = mimeTypeService; 
     if (mtservice != null) { 
         return mtservice.getMimeType(name); 
     } 
     return null; 
 } 

 /** 
  * Returns the real context path that is used to mount this context. 
  * @param req servlet request 
  * @return the context path 
  */ 
 public static String getRealContextPath(HttpServletRequest req) { 
     final String path = req.getContextPath(); 
     if (path.equals(CONTEXT_PATH)) { 
         return ""; 
     } 
     return path.substring(CONTEXT_PATH.length()); 
 } 

 /** 
  * Returns a request wrapper that transforms the context path back to the original one 
  * @param req request 
  * @return the request wrapper 
  */ 
 public static HttpServletRequest createContextPathAdapterRequest(HttpServletRequest req) { 
     return new HttpServletRequestWrapper(req) { 

         @Override 
         public String getContextPath() { 
             return getRealContextPath((HttpServletRequest) getRequest()); 
         } 

     }; 

 } 

 /** 
  * Always returns <code>null</code> because resources are all provided 
  * through individual endpoint implementations. 
  */ 
 @Override 
 public URL getResource(String name) { 
     return null; 
 } 

 /** 
  * Tries to authenticate the request using the 
  * <code>SlingAuthenticator</code>. If the authenticator or the Repository 
  * is missing this method returns <code>false</code> and sends a 503/SERVICE 
  * UNAVAILABLE status back to the client. 
  */ 
 @Override 
 public boolean handleSecurity(HttpServletRequest request, 
                               HttpServletResponse response) throws IOException { 

     final AuthenticationSupport authenticator = this.authenticationSupport; 
     if (authenticator != null) { 
         return authenticator.handleSecurity(createContextPathAdapterRequest(request), response); 
     } 

     // send 503/SERVICE UNAVAILABLE, flush to ensure delivery 
     response.sendError(HttpServletResponse.SC_SERVICE_UNAVAILABLE, 
             "AuthenticationSupport service missing. Cannot authenticate request."); 
     response.flushBuffer(); 

     // terminate this request now 
     return false; 
 } 
}
```

+++

>[!ENDTABS]

### Usar o servlet de amostra

Você chama o servlet executando um `GET` operação em `/dmSample/dynamicmedia/video/manifestUrl`. Os seguintes parâmetros de consulta são passados:

| Parâmetro de consulta | Descrição |
| --- | --- |
| `assetPath` | Obrigatório. O caminho para o vídeo para o qual `manifestUrl` é gerado. |
| `manifestType` | Opcional. O parâmetro pode ser DASH ou HLS. Se não for transmitido, o padrão será DASH. |
| `onlyIfPublished` | Opcional. Se for aprovado, a variável `manifestUrl` é retornado somente se o vídeo for publicado. |

Neste exemplo, vamos supor a seguinte configuração:

* A empresa é `samplecompany`.
* A instância de criação é `http://sample-aem-author.com`.
* A pasta `/content/dam/video-example` tem um perfil de codificação de vídeo aplicado a ele.
* O vídeo `scenery.mp4` é carregado na pasta `/content/dam/video-example`.

Você pode chamar o servlet das seguintes maneiras:

| Tipo | Descrição |
| :--- | --- |
| HLS | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=HLS&assetPath=/content/dam/video-example/scenery.mp4`<br><br>Caso a entrega de DASH esteja ativada:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8?packagedStreaming=true"}`<br><br>Caso a entrega de DASH esteja desativada:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8"}` |
| PASH | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scenery.mp4`<br><br>Caso a entrega de DASH esteja ativada:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.mpd"}`<br><br>Caso a entrega de DASH esteja desativada:<br>`{}` |
| Erro: caminho de ativo incorreto | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scennnnnnery.mp4`<br><br>`{"errorString":"could not retrieve the resource from JCR"}` |


