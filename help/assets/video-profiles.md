---
title: Perfis de vídeo
description: O Dynamic Media já vem com um perfil de codificação de vídeo adaptável predefinido. As configurações nesse perfil pronto para uso são otimizadas para proporcionar aos clientes a melhor experiência de visualização possível. Você também pode adicionar recorte inteligente aos seus vídeos.
uuid: 26a20984-db63-41e9-b16c-6e164b7596a0
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 3b8791c8-2c97-42b7-b4a9-e1157ac9ea02
docset: aem65
feature: Video Profiles
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '3712'
ht-degree: 18%

---


# Perfis de vídeo {#video-profiles}

O Dynamic Media já vem com um perfil de codificação de vídeo adaptável predefinido. As configurações nesse perfil pronto para uso são otimizadas para proporcionar aos clientes a melhor experiência de visualização possível. Quando você codifica os vídeos de origem primária usando o perfil de Codificação de Vídeo Adaptável, durante a reprodução o reprodutor de vídeo ajusta automaticamente a qualidade do fluxo de vídeo com base na velocidade de conexão da Internet de seus clientes. Isso é conhecido como streaming adaptável.

A seguir estão outros fatores que determinam a qualidade de seus vídeos:

* **Resolução do vídeo de fonte primária carregado**

   Se o vídeo MP4 foi gravado em uma resolução mais baixa, como 240p ou 360p, ele não pode ser transmitido em alta definição.

* **Tamanho do reprodutor de vídeo**

   Por padrão, a &quot;Largura&quot; no perfil de Codificação de vídeo adaptativo é definida como &quot;Auto&quot;. Novamente, durante a reprodução, a melhor qualidade é usada com base no tamanho do reprodutor.

Consulte [Práticas recomendadas para codificação de vídeo](/help/assets/video.md#best-practices-for-encoding-videos).

Consulte também [Práticas recomendadas para organizar ativos digitais para usar perfis de processamento](/help/assets/organize-assets.md).

>[!NOTE]
>
>Para gerar os metadados de um vídeo e as miniaturas de imagem de vídeo associadas, o próprio vídeo precisa passar pelo processo de codificação no Dynamic Media. Em AEM, o fluxo de trabalho **[!UICONTROL Dynamic Media Encode Video]** codifica o vídeo se você tiver ativado o Dynamic Media e configurado os serviços da nuvem de vídeo. Esse fluxo de trabalho captura o histórico do processo de fluxo de trabalho e as informações de falha. Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](/help/assets/video.md#monitoring-video-encoding-and-youtube-publishing-progress). Se você ativou o Dynamic Media e configurou serviços de nuvem de vídeo, o fluxo de trabalho **[!UICONTROL Codificação de vídeo do Dynamic Media]** entrará em vigor automaticamente ao carregar um vídeo. (Se você não estiver usando o Dynamic Media, o fluxo de trabalho **[!UICONTROL Ativo de atualização do DAM]** entrará em vigor.)
>
>Os metadados são úteis quando você está procurando ativos. As miniaturas são imagens de vídeo estáticas geradas durante a codificação. Eles são exigidos pelo sistema de AEM e usados na interface do usuário para ajudar você a identificar visualmente os vídeos na exibição Cartões, na exibição Resultados da pesquisa e na exibição Lista de ativos. É possível ver as miniaturas geradas ao tocar no ícone Representações (uma paleta de pintor) de um vídeo codificado.

Quando terminar de criar o perfil de vídeo, aplique-o a uma pasta ou várias pastas. Consulte [Aplicar um perfil de vídeo a pastas.](#applying-a-video-profile-to-folders)

Para definir parâmetros de processamento avançados para outros tipos de ativos, consulte [Configuração do processamento de ativos](/help/assets/config-dms7.md#configuring-asset-processing).

Consulte também [Perfis para processar metadados, imagens e vídeos](processing-profiles.md).

## Predefinições de codificação de vídeo adaptável {#adaptive-video-encoding-presets}

A tabela a seguir identifica perfis de codificação de práticas recomendadas para streaming de vídeo adaptável para dispositivos móveis e tablets, além de computadores desktop. Você pode usar essas predefinições para qualquer vídeo com taxa de proporção.

<table>
 <tbody>
  <tr>
   <td><strong>Codec de formatação do vídeo</strong></td>
   <td><strong>Tamanho do vídeo - Largura (px)</strong></td>
   <td><strong>Tamanho do vídeo - Altura (px)</strong></td>
   <td><strong>Manter taxa de proporção?</strong></td>
   <td><strong>Taxa de bits do vídeo (Kbps)</strong></td>
   <td><strong>Taxa De Quadros De Vídeo (Fps)</strong></td>
   <td><strong>Codec de áudio</strong></td>
   <td><strong>Taxa de bits de áudio (Kbps)</strong></td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>360</td>
   <td>Sim</td>
   <td>730</td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>540</td>
   <td>Sim</td>
   <td>2000<br /> </td>
   <td>30º</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>720<br /> </td>
   <td>Sim</td>
   <td>3000<br /> </td>
   <td>30º</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
 </tbody>
</table>

## Sobre o uso do recorte inteligente em perfis de vídeo {#about-smart-crop-video}

Recorte inteligente para vídeo - um recurso opcional disponível em Perfis de vídeo - é uma ferramenta que usa o poder da inteligência artificial no Adobe Sensei para detectar e recortar automaticamente o ponto focal em qualquer vídeo adaptável ou vídeo progressivo que você tenha carregado, independentemente do tamanho.

Os formatos de vídeo suportados para recorte inteligente incluem MP4, MKV, MOV, AVI, FLV e WMV.

O tamanho máximo suportado do arquivo de vídeo para o recorte inteligente é o seguinte critério:

* Duração de cinco minutos.
* 30 quadros por segundo (FPS).
* 300 MB de tamanho de arquivo.

Observe que o Adobe Sensei está atualmente limitado a 9000 quadros. Ou seja, cinco minutos a 30 QPS. Se o vídeo tiver um FPS maior, a duração máxima do vídeo compatível diminuirá. Por exemplo, um vídeo de 60 FPS deve ter dois minutos e meio de duração para ser compatível com o Adobe Sensai e o recorte inteligente.

![Recorte inteligente para vídeo](assets/smart-crop-video.png)

>[!IMPORTANT]
>
>Para que o recorte inteligente de vídeo funcione, você deve incluir uma ou mais predefinições de codificação de vídeo com seu perfil de vídeo.

Para usar o recorte inteligente para vídeo, você cria um perfil de codificação de vídeo adaptável ou progressivo. Como parte do seu perfil, use a ferramenta **[!UICONTROL Proporção de recorte inteligente]** para selecionar proporções predefinidas. Como exemplo, depois de definir suas predefinições de codificação de vídeo, você pode adicionar uma definição de &quot;Paisagem móvel&quot; com uma proporção de aspecto de 16x9 e uma definição de &quot;Retrato móvel&quot; com uma proporção de aspecto de 9x16. Outros aspectos ou proporções de corte a partir dos quais você pode escolher incluem 1x1, 4x3 e 4x5.

![Edição de um perfil de codificação de vídeo com recorte inteligente](assets/edit-smart-crop-video2.png)

Observe que você pode alternar entre ativado e desativado o recorte inteligente de vídeo no perfil de vídeo usando o controle deslizante à direita da **[!UICONTROL Proporção de recorte inteligente]** na interface do usuário.

Depois de criar e salvar seu perfil de vídeo, você pode aplicá-lo às pastas desejadas.

Consulte [Aplicar perfis de vídeo a pastas específicas](#applying-video-profiles-to-specific-folders) ou [Aplicar um perfil de vídeo globalmente](#applying-a-video-profile-globally).

Consulte também [Recorte inteligente para imagens](image-profiles.md).

## Criação de um perfil de vídeo para transmissão adaptável {#creating-a-video-encoding-profile-for-adaptive-streaming}

O Dynamic Media já vem com um perfil de codificação de vídeo adaptável predefinido, um grupo de configurações de upload de vídeo para MP4 H.264, que é otimizado para a melhor experiência de visualização. Você pode usar esse perfil ao carregar seus vídeos.

No entanto, se esse perfil predefinido não atender às suas necessidades, você poderá criar seu próprio perfil de codificação de vídeo adaptável. Ao usar a configuração **[!UICONTROL Codificar para transmissão adaptável]**-como uma prática recomendada, todas as predefinições de codificação adicionadas ao perfil são validadas para garantir que todos os vídeos tenham a mesma proporção. Além disso, os vídeos codificados são tratados como uma taxa de bits múltipla definida para transmissão contínua.

Ao criar o perfil de codificação de vídeo, você observará que a maioria das opções de codificação é pré-preenchida com as configurações padrão recomendadas para ajudá-lo. No entanto, se você selecionar um valor diferente do padrão recomendado, lembre-se de que isso pode resultar em má qualidade do vídeo durante a reprodução e outros problemas de desempenho.

Portanto, para todas as predefinições de codificação de vídeo MP4 H.264 no perfil, os seguintes valores são validados para garantir que sejam os mesmos em predefinições de codificação individuais no perfil, tornando assim possível o streaming adaptável:

* Codec de formato de vídeo - MP4 H.264 (.mp4)
* Codec de áudio
* Taxa de áudio
* Manter taxa de proporção
* Codificação em dois passos
* Taxa de bits constante
* Perfil H264
* Taxa de amostra do áudio

Se os valores não forem os mesmos, você poderá continuar criando o perfil como está. No entanto, esteja ciente de que o streaming adaptável não será possível. Em vez disso, os usuários experimentarão o streaming de taxa de bits única. É recomendável editar as configurações de codificação para usar os mesmos valores em predefinições de codificação individuais no perfil. (Observe que o perfil de vídeo/editor predefinido deve impor a paridade das configurações de codificação adaptáveis do vídeo se &quot;Codificar para transmissão adaptável&quot; estiver ativado.)

Consulte também [Criar um perfil de codificação de vídeo para streaming progressivo](#creating-a-video-encoding-profile-for-progressive-streaming).

Consulte também [Práticas recomendadas para codificação de vídeo](/help/assets/video.md#best-practices-for-encoding-videos).

Para definir parâmetros de processamento avançados para outros tipos de ativos, consulte [Configuração do processamento de ativos](/help/assets/config-dms7.md#configuring-asset-processing).

**Para criar um perfil de vídeo para transmissão** adaptável,

1. Toque no logotipo do AEM e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de vídeo.]**
1. Clique ou toque em **[!UICONTROL Criar]** para adicionar um novo perfil de vídeo.

1. Insira um nome e uma descrição para o perfil.
1. Na página Criar/editar predefinições de codificação de vídeo, toque em **[!UICONTROL Adicionar predefinição de codificação de vídeo.]**
1. Na guia **[!UICONTROL Basic]**, defina as opções de vídeo e áudio.
Toque no ícone de informações ao lado de cada opção para obter descrições adicionais ou configurações recomendadas com base no codec de formato de vídeo selecionado.
1. No cabeçalho Tamanho do vídeo, verifique se **[!UICONTROL Manter proporção&lt;/a1/> está marcado.]**
1. Defina a resolução do tamanho do quadro de vídeo em pixels. Use o valor **[!UICONTROL Auto]** para dimensionar automaticamente para corresponder à proporção do aspecto de origem (relação largura/altura). Por exemplo, Auto x 480 ou 640 x Auto.

1. Faça uma das seguintes opções:

   * No campo **[!UICONTROL Width]**, digite **[!UICONTROL auto.]** No campo  **** Heightfield , insira um valor em pixels.

   * Para ajudá-lo a visualizar o tamanho do vídeo, toque no ícone Informações (i) à direita de **[!UICONTROL Altura]** para abrir a página Calculadora de tamanho. Use **[!UICONTROL Calculadora de tamanho]** para definir as dimensões do vídeo (representadas pela caixa azul) desejada. Toque em **[!UICONTROL X]** no canto superior direito quando terminar.

1. (Opcional) Toque na guia **[!UICONTROL Avançado]** e verifique se a caixa de seleção **[!UICONTROL Usar valores padrão]** está marcada (recomendada). Como alternativa, modifique configurações avançadas de vídeo e áudio.
1. No canto superior direito da página, toque em **[!UICONTROL Save]** para salvar a predefinição.
1. Faça uma das seguintes opções:
   * Repita as etapas 4 a 10 para criar predefinições de codificação adicionais. (O streaming de vídeo adaptável requer mais de uma predefinição de vídeo.)
   * Prossiga para a próxima etapa.

1. (Opcional) Para adicionar o recorte inteligente de vídeo aos vídeos aos quais esse perfil será aplicado, faça o seguinte:
   * Na página Editar perfil de vídeo, à direita do cabeçalho Proporção de recorte inteligente, toque em **[!UICONTROL Adicionar novo.]**
   * No campo Nome , digite um nome para a proporção de corte que o ajudará a identificá-lo facilmente.
   * Na lista suspensa **[!UICONTROL Proporção de corte]** , selecione a proporção que deseja usar.

1. Faça uma das seguintes opções:

   * Continue adicionando novas proporções de corte, conforme necessário.
   * Prossiga para a próxima etapa.

1. No canto superior direito da página, toque em **[!UICONTROL Save]** novamente para salvar o perfil.

Agora é possível aplicar o perfil às pastas que contêm vídeos. Consulte [Aplicar um perfil de vídeo a pastas](#applying-a-video-profile-to-folders) ou [Aplicar um perfil de vídeo globalmente](#applying-a-video-profile-globally).

## Criar um perfil de vídeo para transmissão progressiva {#creating-a-video-encoding-profile-for-progressive-streaming}

Se você optar por não usar a opção **[!UICONTROL Codificar para transmissão adaptável]**, lembre-se de que todas as predefinições de codificação adicionadas ao perfil são tratadas como representações de vídeo individuais para transmissão de streaming com taxa de bits única ou entrega de vídeo progressiva. Além disso, não há validação para garantir que todas as representações de vídeo tenham a mesma proporção.

Dependendo do modo em que você está executando, os codecs de formato de vídeo aceitos são os seguintes:

* Modo Dynamic Media-Scene7: H.264 (.mp4)
* Dynamic Media-Modo híbrido: H.264 (.mp4), WebM

Consulte também [Criar um perfil de codificação de vídeo para transmissão adaptável](#creating-a-video-encoding-profile-for-adaptive-streaming).

Consulte também [Práticas recomendadas para codificação de vídeo](/help/assets/video.md#best-practices-for-encoding-videos).

Para definir parâmetros de processamento avançados para outros tipos de ativos, consulte [Configuração do processamento de ativos](/help/assets/config-dms7.md#configuring-asset-processing).

**Para criar um perfil de vídeo para transmissão progressiva:**

1. Toque no logotipo do AEM e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de vídeo.]**
1. Toque em **[!UICONTROL Criar]** para adicionar um novo perfil de vídeo.
1. Insira um nome e uma descrição para o perfil.
1. Na página Criar/editar predefinições de codificação de vídeo, toque em **[!UICONTROL Adicionar predefinição de codificação de vídeo.]**
1. Na guia **[!UICONTROL Basic]**, defina as opções de vídeo e áudio.
Toque no ícone de informações ao lado de cada opção para obter descrições adicionais ou configurações recomendadas com base no codec de formato de vídeo selecionado.
1. (Opcional) No cabeçalho Tamanho do vídeo, desmarque **[!UICONTROL Manter proporção.]**
1. Faça o seguinte:
   * No campo **[!UICONTROL Width]**, digite **[!UICONTROL auto.]**
   * No campo **[!UICONTROL Height]**, insira um valor em pixels.
Para ajudá-lo a visualizar o tamanho do vídeo, toque no ícone Informações de altura para abrir a página **[!UICONTROL Calculadora de tamanho]**. Use a página **[!UICONTROL Calculadora de tamanho]** para definir ainda mais a dimensão do vídeo (caixa azul) como desejar. Quando terminar, no canto superior direito da caixa de diálogo, toque em **[!UICONTROL X.]**
1. (Opcional) Siga um destes procedimentos:

   * Toque na guia **[!UICONTROL Avançado]** e verifique se a caixa de seleção **[!UICONTROL Usar valores padrão]** está marcada (recomendada).

   * Desmarque a caixa de seleção **[!UICONTROL Usar valores padrão]** e especifique as configurações de vídeo e áudio desejadas.
Toque no ícone de informações ao lado de cada opção para obter descrições adicionais ou configurações recomendadas com base no codec de formato de vídeo selecionado.

1. No canto superior direito da página, toque em **[!UICONTROL Save]** para salvar a predefinição.
1. Faça uma das seguintes opções:

   * Repita as etapas de 4 a 9 para criar predefinições de codificação adicionais.
   * Prossiga para a próxima etapa.

1. (Opcional) Para adicionar o recorte inteligente de vídeo aos vídeos aos quais esse perfil será aplicado, faça o seguinte:

   * Na página Editar perfil de vídeo, à direita do cabeçalho Proporção de recorte inteligente, toque em **[!UICONTROL Adicionar novo.]**
   * No campo Nome , digite um nome para a proporção de corte que o ajudará a identificá-lo facilmente.
   * Na lista suspensa **[!UICONTROL Proporção de corte]** , selecione a proporção que deseja usar.

1. Faça uma das seguintes opções:

   * Continue adicionando novas proporções de corte, conforme necessário.
   * Prossiga para a próxima etapa.

1. No canto superior direito da página, toque em **[!UICONTROL Salvar]** para salvar o perfil.

Agora é possível aplicar o perfil às pastas que contêm vídeos. Consulte [Aplicar um perfil de vídeo a pastas](#applying-a-video-profile-to-folders) ou [Aplicar um perfil de vídeo globalmente](#applying-a-video-profile-globally).

## Uso de parâmetros de codificação de vídeo adicionados personalizados {#using-custom-added-video-encoding-parameters}

É possível editar um perfil de codificação de vídeo existente para aproveitar os parâmetros de codificação avançada de vídeo não encontrados na interface do usuário ao criar ou editar um Perfil de vídeo no AEM. Você personaliza a adição de um ou mais parâmetros avançados (como minBitrate e maxBitrate) ao seu perfil existente.

**Para usar parâmetros** de codificação de vídeo personalizados:

1. Toque no logotipo do AEM e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite.]**
1. Na página CRXDE Lite, no painel Explorer à esquerda, navegue até o seguinte:

   `/conf/global/settings/dam/dm/presets/video/*name_of_video_encoding_profile_to_edit`

1. No painel no lado inferior direito da página, na guia Propriedades, especifique o **[!UICONTROL Nome]**, o **[!UICONTROL Tipo]** e o **[!UICONTROL Valor]** do parâmetro que deseja usar.

   Os seguintes parâmetros avançados estão disponíveis para uso:

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td>
   <td><strong>Descrição</strong><br /> </td>
   <td><strong>Tipo</strong><br /> </td>
   <td><strong>Valor</strong></td>
  </tr>
  <tr>
   <td><code>h264Level</code></td>
   <td>Nível H.264 a ser usado na codificação. Normalmente, isso é determinado automaticamente com base nas configurações de codificação que você está usando.</td>
   <td><code>String</code></td>
   <td><p>10 * h264 nível</p> <p>Por exemplo, 3,0 = 30, 1,3 = 13)</p> <p>Nenhum valor padrão.</p> </td>
  </tr>
  <tr>
   <td><code>keyframe</code></td>
   <td>O número alvo de quadros entre quadros-chave. Calcule esse valor para gerar um quadro-chave a cada 2-10 segundos. Por exemplo, a 30 quadros por segundo, o intervalo do quadro-chave deve ser de 60 a 300.<br /> <br /> Intervalos de quadro-chave menores melhoram o comportamento de busca de fluxo e troca de fluxo para codificações de vídeo adaptáveis e também podem melhorar a qualidade de vídeos que têm muito movimento. No entanto, como os quadros-chave aumentam o tamanho de um arquivo, um intervalo de quadros-chave mais baixo normalmente resulta em uma menor qualidade geral do vídeo em uma determinada taxa de bits.</td>
   <td><code>String</code></td>
   <td><p>Número positivo.</p> <p>O padrão é 300.</p> <p>O valor recomendado para HLS (HTTP Live Streaming) é 60-90.</p> </td>
  </tr>
  <tr>
   <td><code>minBitrate</code></td>
   <td><p>Taxa mínima de bits para permitir codificações variáveis de taxa de bits, em Kbps (kilobits por segundo).</p> <p>Esse parâmetro só se aplica quando<strong> Usar a taxa de bits constante</strong> é desmarcado na guia Avançado quando você cria ou edita um perfil de codificação de vídeo.</p> <p>Consulte também <a href="/help/assets/video.md#bitrate">Bitrate</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>Número positivo, em Kbps.</p> <p>Nenhum valor padrão.</p> </td>
  </tr>
  <tr>
   <td><code>maxBitrate</code></td>
   <td><p>Taxa de bits máxima para permitir codificações de taxa de bits variável, em Kbps.</p> <p>Esse parâmetro só se aplica quando<strong> Usar a taxa de bits constante</strong> é desmarcado na guia Avançado quando você cria ou edita um perfil de codificação de vídeo.</p> <p>Consulte também <a href="/help/assets/video.md#bitrate">Bitrate</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>Número positivo, em Kbps.</p> <p>Nenhum valor padrão. No entanto, o valor recomendado é até duas vezes a taxa de bits de codificação.</p> </td>
  </tr>
  <tr>
   <td><code>audioBitrateCustom</code></td>
   <td>Defina o valor como <code>true</code> para forçar uma taxa de bits constante para o fluxo de áudio, se suportado pelo codec de áudio.</td>
   <td><code>String</code></td>
   <td><p><code>true</code>/<code>false</code></p> <p>O padrão é <code>false</code>.</p> <p>O valor recomendado para HLS (HTTP Live Streaming) é <code>false</code>.</p> <p> </p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-516](assets/chlimage_1-516.png)

1. Próximo ao canto inferior direito da página, toque em **[!UICONTROL Adicionar.]**
1. Faça uma das seguintes opções:

   * Repita as etapas 3 e 4 para adicionar outro parâmetro ao perfil de codificação de vídeo.
   * Próximo ao canto superior esquerdo da página, toque em **[!UICONTROL Salvar tudo.]**

1. No canto superior esquerdo da página CRXDE Lite, toque no ícone **[!UICONTROL Voltar ao início]** para retornar ao AEM.

### Editar um perfil de vídeo {#editing-a-video-encoding-profile}

É possível editar qualquer perfil de vídeo criado para adicionar, editar ou excluir predefinições de vídeo nesse perfil.

Por padrão, não é possível editar o perfil predefinido e pronto para uso **[!UICONTROL Adaptive Video Encoding]** que veio com o Dynamic Media. Em vez disso, você pode copiar facilmente o perfil e salvá-lo com um novo nome. Em seguida, você pode editar as predefinições desejadas no perfil copiado.

Consulte também [Práticas recomendadas para codificação de vídeo](/help/assets/video.md#best-practices-for-encoding-videos).

Para definir parâmetros de processamento avançados para outros tipos de ativos, consulte [Configuração do processamento de ativos](/help/assets/config-dms7.md#configuring-asset-processing).

**Para editar um perfil** de vídeo:

1. Toque no logotipo do AEM e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de vídeo.]**
1. Na página Perfis de vídeo , verifique o nome de um perfil de vídeo.
1. Na barra de ferramentas, toque em **[!UICONTROL Editar.]**
1. Na página Perfil de codificação de vídeo , edite o nome e a descrição, conforme desejado.
1. Como prática recomendada, verifique se a caixa de seleção **[!UICONTROL Codificar para transmissão adaptável]** está selecionada.
Toque no ícone de informações para obter uma descrição da transmissão adaptável. (Se você estiver editando um perfil de vídeo progressivo, não marque essa caixa de seleção.)
1. No cabeçalho Predefinições de codificação de vídeo , adicione, edite ou exclua predefinições de codificação de vídeo que compõem o perfil.

   Toque no ícone de informações ao lado de cada opção nas guias **[!UICONTROL Básico]** e **[!UICONTROL Avançado]** para obter descrições adicionais ou configurações recomendadas com base no codec de formato de vídeo selecionado.

1. No canto superior direito da página, toque em **[!UICONTROL Salvar.]**

### Copiando um perfil de vídeo {#copying-a-video-encoding-profile}

1. Toque no logotipo do AEM e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de vídeo.]**
1. Na página Perfis de vídeo , verifique o nome de um perfil de vídeo.
1. Na barra de ferramentas, toque em **[!UICONTROL Copiar.]**
1. Na página Perfil de codificação de vídeo , digite um novo nome para o perfil.
1. Como prática recomendada, verifique se a caixa de seleção **[!UICONTROL Codificar para transmissão adaptável]** está selecionada. Toque no ícone de informações para obter uma descrição da transmissão adaptável. (Se você estiver copiando um perfil de vídeo progressivo, não marque a caixa de seleção.)

   No Dynamic Media - Modo híbrido, se uma predefinição de vídeo do WebM fizer parte do perfil de vídeo, **[!UICONTROL Codificar para transmissão adaptável]** não será possível porque todas as predefinições devem ser MP4.
1. No cabeçalho Predefinições de codificação de vídeo , adicione, edite ou exclua predefinições de codificação de vídeo que compõem o perfil.

   Toque no ícone de informações ao lado de cada opção nas guias Básico e Avançado para obter as configurações e descrições recomendadas.

1. No canto superior direito da página, toque em **[!UICONTROL Salvar.]**

### Excluir um perfil de vídeo {#deleting-a-video-encoding-profile}

1. Toque no logotipo do AEM e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de vídeo.]**
1. Na página Perfis de vídeo , verifique um ou mais nomes de perfil de vídeo.
1. Na barra de ferramentas, toque em **[!UICONTROL Delete.]**
1. Toque em **[!UICONTROL OK.]**

## Aplicar um perfil de vídeo a pastas {#applying-a-video-profile-to-folders}

Ao atribuir um perfil de vídeo a uma pasta, qualquer subpasta herda automaticamente o perfil da pasta pai. Isso significa que você pode atribuir somente um perfil de vídeo a uma pasta. Dessa forma, considere cuidadosamente a estrutura de pastas de onde você faz upload, armazena, usa e arquiva ativos.

Se você atribuiu um perfil de vídeo diferente a uma pasta, o novo perfil substituirá o perfil anterior. Os ativos de pasta existentes anteriormente permanecem inalterados. O novo perfil é aplicado aos ativos que são adicionados à pasta posteriormente.

As pastas que têm um perfil atribuído a elas são indicadas na interface do usuário pelo nome do perfil que aparece no nome do cartão.

![chlimage_1-517](assets/chlimage_1-517.png)

Você pode aplicar perfis de vídeo a pastas específicas ou globalmente a todos os ativos.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você alterou posteriormente. Consulte o [reprocessando de ativos em uma pasta após a edição do perfil de processamento](processing-profiles.md#reprocessing-assets).

### Aplicar um perfil de vídeo a pastas específicas {#applying-video-profiles-to-specific-folders}

Aplique um perfil de vídeo a uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades.]** Esta seção descreve como aplicar perfis de vídeo a pastas de ambas as maneiras.

As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

Consulte também [Reprocessando ativos em uma pasta depois de ter editado seu perfil de processamento](processing-profiles.md#reprocessing-assets).

#### Aplicar um perfil de vídeo a pastas por meio da interface do usuário de Perfis {#applying-video-profiles-to-folders-by-way-of-the-profiles-user-interface}

1. Toque no logotipo do AEM e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de vídeo.]**
1. Selecione o perfil de vídeo que deseja aplicar a uma ou várias pastas.
1. Toque em **[!UICONTROL Aplicar perfil às pastas]** e selecione uma ou várias pastas que deseja usar para receber os ativos carregados recentemente e toque em **[!UICONTROL Aplicar.]** As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta enquanto estão na **[!UICONTROL Exibição de cartão.]**
Você pode  [monitorar o progresso de um trabalho](#monitoring-the-progress-of-an-encoding-job) de processamento de perfil de vídeo.

#### Aplicar um perfil de vídeo a pastas a partir de Propriedades {#applying-video-profiles-to-folders-from-properties}

1. Toque ou clique no logotipo do AEM e navegue até **[!UICONTROL Assets]** e, em seguida, até a pasta à qual deseja aplicar um perfil de vídeo.
1. Na pasta, toque na marca de seleção para selecioná-la e toque em **[!UICONTROL Propriedades.]**
1. Selecione a guia **[!UICONTROL Perfis de vídeo]**, selecione o perfil no menu suspenso e clique em **[!UICONTROL Salvar e fechar.]** As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

   ![chlimage_1-518](assets/chlimage_1-518.png)
Você pode  [monitorar o progresso de um trabalho de processamento de perfil de vídeo](#monitoring-the-progress-of-an-encoding-job).

### Aplicar um perfil de vídeo globalmente {#applying-a-video-profile-globally}

Além de aplicar um perfil a uma pasta, também é possível aplicar um globalmente para que qualquer conteúdo carregado AEM ativos em qualquer pasta tenha o perfil selecionado aplicado.

Consulte também [Reprocessando ativos em uma pasta depois de ter editado seu perfil de processamento](processing-profiles.md#reprocessing-assets).

**Para aplicar um perfil de vídeo globalmente**,

* Navegue até CRXDE Lite para o seguinte nó: `/content/dam/jcr:content`. Adicione a propriedade `videoProfile:/libs/settings/dam/video/dynamicmedia/<name of video encoding profile>` e toque em **[!UICONTROL Salvar tudo.]**

   ![chlimage_1-519](assets/chlimage_1-519.png)
* Você pode [monitorar o progresso de um trabalho de processamento de perfil de vídeo](#monitoring-the-progress-of-an-encoding-job).

## Monitorar o progresso de um trabalho de processamento de perfil de vídeo {#monitoring-the-progress-of-an-encoding-job}

Um indicador de processamento (ou barra de progresso) é exibido para que você possa monitorar visualmente o progresso de um trabalho de processamento de perfil de vídeo.

Você também pode visualizar o arquivo `error.log` para monitorar o progresso de um trabalho de codificação, ver se a codificação foi concluída ou ver quaisquer erros de trabalho. O `error.log` é encontrado na pasta `logs` onde sua instância do AEM está instalada.

## Remover um perfil de vídeo das pastas {#removing-a-video-profile-from-folders}

Ao remover um perfil de vídeo de uma pasta, qualquer subpasta herda automaticamente a remoção do perfil da pasta pai. No entanto, o processamento de arquivos que ocorreu dentro das pastas permanece intacto.

Remova um perfil de vídeo de uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, nas **[!UICONTROL Configurações da pasta.]** Esta seção descreve como remover perfis de vídeo de pastas de ambas as maneiras.

### Remover um perfil de vídeo das pastas por meio da interface do usuário de Perfis {#removing-video-profiles-from-folders-by-way-of-the-profiles-user-interface}

1. Toque no logotipo do AEM e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de vídeo.]**
1. Selecione o perfil de vídeo que deseja remover de uma pasta ou de várias pastas.
1. Toque em **[!UICONTROL Remover perfil das pastas]** e selecione uma ou várias pastas que deseja usar para remover o perfil e toque em **[!UICONTROL Remover.]**

   Você pode confirmar que o perfil de vídeo não é mais aplicado a uma pasta porque o nome não aparece mais abaixo do nome da pasta.

### Remover um perfil de vídeo das pastas por meio das Propriedades {#removing-video-profiles-from-folders-by-way-of-properties}

1. Toque ou clique no logotipo do AEM e navegue até **[!UICONTROL Assets]** e, em seguida, até a pasta da qual deseja remover um perfil de vídeo.
1. Na pasta, toque ou clique na marca de seleção para selecioná-la e toque ou clique em **[!UICONTROL Propriedades.]**
1. Selecione a guia **[!UICONTROL Perfis de vídeo]**, selecione **[!UICONTROL Nenhum]** no menu suspenso e clique em **[!UICONTROL Salvar e fechar.]** As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

