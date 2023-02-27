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
role: User, Admin
mini-toc-levels: 3
exl-id: b290fac2-7259-45d7-b733-70419d632b07
source-git-commit: 78aa7aac838dabc1c4f0329520092e4755541322
workflow-type: tm+mt
source-wordcount: '3736'
ht-degree: 9%

---

# Perfis de vídeo {#video-profiles}

O Dynamic Media já vem com um perfil de codificação de vídeo adaptável predefinido. As configurações nesse perfil pronto para uso são otimizadas para proporcionar aos clientes a melhor experiência de visualização possível. Quando você codifica os vídeos de origem primária usando o perfil de Codificação de Vídeo Adaptável, durante a reprodução o reprodutor de vídeo ajusta automaticamente a qualidade do fluxo de vídeo com base na velocidade de conexão da Internet de seus clientes. Essa funcionalidade é conhecida como transmissão adaptável da taxa de bits.

A seguir estão outros fatores que determinam a qualidade de seus vídeos:

* **Resolução do vídeo de fonte primária carregado**

   Se o vídeo MP4 foi gravado em uma resolução mais baixa, como 240p ou 360p, ele não pode ser transmitido em alta definição.

* **Tamanho do reprodutor de vídeo**

   Por padrão, a &quot;Largura&quot; no perfil de Codificação de vídeo adaptativo é definida como &quot;Auto&quot;. Novamente, durante a reprodução, a melhor qualidade é usada com base no tamanho do reprodutor.

Consulte [Práticas recomendadas para codificação de vídeo](/help/assets/video.md#best-practices-for-encoding-videos).

Consulte também [Práticas recomendadas para organizar ativos digitais para usar perfis de processamento](/help/assets/organize-assets.md).

>[!NOTE]
>
>Para gerar os metadados de um vídeo e as miniaturas de imagem de vídeo associadas, o próprio vídeo deve passar pelo processo de codificação no Dynamic Media. No Adobe Experience Manager, a variável **[!UICONTROL Codificar vídeo no Dynamic Media]** O fluxo de trabalho codifica o vídeo se você tiver ativado o Dynamic Media e configurado os serviços da nuvem de vídeo. Esse fluxo de trabalho captura o histórico do processo de fluxo de trabalho e as informações de falha. Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](/help/assets/video.md#monitoring-video-encoding-and-youtube-publishing-progress). Se você ativou o Dynamic Media e configurou os serviços da nuvem de vídeo, a variável **[!UICONTROL Codificar vídeo no Dynamic Media]** O fluxo de trabalho entra em vigor automaticamente ao carregar um vídeo. (Se você não estiver usando o Dynamic Media, a variável **[!UICONTROL Ativo de atualização DAM]** O fluxo de trabalho entra em vigor.)
>
>Os metadados são úteis quando você está procurando ativos. As miniaturas são imagens de vídeo estáticas geradas durante a codificação. Eles são exigidos pelo sistema Experience Manager e usados na interface do usuário para ajudar você a identificar visualmente os vídeos na exibição Cartões, na exibição Resultados da pesquisa e na exibição Lista de ativos. É possível ver as miniaturas geradas ao selecionar o ícone Representações (paleta Tinta) de um vídeo codificado.

Quando terminar de criar o perfil de vídeo, aplique-o a uma ou várias pastas. Consulte [Aplicar um perfil de vídeo a pastas](#applying-a-video-profile-to-folders).

Para definir parâmetros de processamento avançados para outros tipos de ativos, consulte [Configurar o processamento de ativos](/help/assets/config-dms7.md#configuring-asset-processing).

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
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>720<br /> </td>
   <td>Sim</td>
   <td>3000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
 </tbody>
</table>

## Sobre o uso do recorte inteligente em perfis de vídeo {#about-smart-crop-video}

Recorte inteligente para vídeo - um recurso opcional disponível em Perfis de vídeo - é uma ferramenta que usa o poder da inteligência artificial no Adobe Sensei. Ele detecta e recorta automaticamente o ponto focal em qualquer vídeo adaptável ou vídeo progressivo que você tenha carregado, independentemente do tamanho.

Os formatos de vídeo suportados para recorte inteligente incluem MP4, MKV, MOV, AVI, FLV e WMV.

O tamanho máximo suportado do arquivo de vídeo para o recorte inteligente é o seguinte critério:

* Duração de cinco minutos.
* 30 quadros por segundo (FPS).
* 300 MB de tamanho de arquivo.

O Adobe Sensei é limitado a 9000 quadros. Ou seja, cinco minutos a 30 QPS. Se o vídeo tiver um FPS maior, a duração máxima do vídeo compatível diminuirá. Por exemplo, um vídeo de 60 FPS deve ter dois minutos e meio de duração para ser compatível com o Adobe Sensei e o recorte inteligente.

![Recorte inteligente para vídeo](assets/smart-crop-video.png)

>[!IMPORTANT]
>
>Para que o recorte inteligente de vídeo funcione, você deve incluir uma ou mais predefinições de codificação de vídeo com seu perfil de vídeo.

Para usar o recorte inteligente para vídeo, você cria um perfil de codificação de vídeo adaptável ou progressivo. Como parte do seu perfil, use o **[!UICONTROL Proporção de corte inteligente]** para selecionar taxas de proporção predefinidas. Como exemplo, depois de definir suas predefinições de codificação de vídeo, você pode adicionar uma definição de &quot;Paisagem móvel&quot; com uma proporção de aspecto de 16x9 e uma definição de &quot;Retrato móvel&quot; com uma proporção de aspecto de 9x16. Outros aspectos ou proporções de corte a partir dos quais você pode escolher incluem 1x1, 4x3 e 4x5.

![Editar um perfil de codificação de vídeo com recorte inteligente](assets/edit-smart-crop-video2.png)

Você pode alternar entre ativado e desativado o recorte inteligente de vídeo no perfil de vídeo usando o controle deslizante à direita de **[!UICONTROL Proporção de corte inteligente]** na interface do usuário.

Depois de criar e salvar seu perfil de vídeo, você pode aplicá-lo às pastas desejadas.

Consulte [Aplicar perfis de vídeo a pastas específicas](#applying-video-profiles-to-specific-folders) ou [Aplicar um perfil de vídeo globalmente](#applying-a-video-profile-globally).

Consulte também [Recorte inteligente de imagens](image-profiles.md).

## Criar um perfil de vídeo para transmissão adaptável da taxa de bits {#creating-a-video-encoding-profile-for-adaptive-streaming}

O Dynamic Media já vem com um perfil de codificação de vídeo adaptável predefinido, um grupo de configurações de upload de vídeo para MP4 H.264, que é otimizado para a melhor experiência de visualização. Você pode usar esse perfil ao carregar seus vídeos.

No entanto, se esse perfil predefinido não atender às suas necessidades, você poderá criar seu próprio perfil de codificação de vídeo adaptável. Ao usar a configuração **[!UICONTROL Codificar para transmissão adaptável]** - como prática recomendada - todas as predefinições de codificação adicionadas ao perfil são validadas para garantir que todos os vídeos tenham a mesma proporção. Além disso, os vídeos codificados são tratados como uma taxa de bits múltipla definida para transmissão contínua.

Ao criar o perfil de codificação de vídeo, observe que a maioria das opções de codificação é pré-preenchida com as configurações padrão recomendadas para ajudá-lo. No entanto, se você selecionar um valor diferente do padrão recomendado, isso pode resultar em má qualidade do vídeo durante a reprodução e outros problemas de desempenho.

Portanto, para todas as predefinições de codificação de vídeo MP4 H.264 no perfil, os seguintes valores são validados para garantir que sejam os mesmos em predefinições de codificação individuais no perfil, possibilitando o streaming adaptável da taxa de bits:

* Codec de formato de vídeo - MP4 H.264 (.mp4)
* Codec de áudio
* Taxa de áudio
* Manter taxa de proporção
* Codificação em dois passos
* Taxa de bits constante
* Perfil H264
* Taxa de amostra do áudio

Se os valores não forem os mesmos, você poderá continuar criando o perfil como está. No entanto, o streaming adaptável da taxa de bits não é possível. Em vez disso, os usuários experimentam o streaming de taxa de bits única. É recomendável editar as configurações de codificação para usar os mesmos valores em predefinições de codificação individuais no perfil. (O editor de perfil/predefinição de vídeo aplica a paridade das configurações de codificação de vídeo adaptável se **[!UICONTROL Codificar para transmissão adaptável]** está ativado.)

Consulte também [Criar um perfil de codificação de vídeo para streaming progressivo](#creating-a-video-encoding-profile-for-progressive-streaming).

Consulte também [Práticas recomendadas para codificação de vídeo](/help/assets/video.md#best-practices-for-encoding-videos).

Para definir parâmetros de processamento avançados para outros tipos de ativos, consulte [Configurar o processamento de ativos](/help/assets/config-dms7.md#configuring-asset-processing).

**Para criar um perfil de vídeo para transmissão adaptável da taxa de bits**,

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de vídeo]**.
1. Selecionar **[!UICONTROL Criar]** para adicionar um perfil de vídeo.

1. Insira um nome e uma descrição para o perfil.
1. Na página Criar/editar predefinições de codificação de vídeo , selecione **[!UICONTROL Adicionar predefinição de codificação de vídeo]**.
1. No **[!UICONTROL Básico]** , defina as opções de vídeo e áudio.
Selecione o ícone de informações ao lado de cada opção para obter descrições adicionais ou configurações recomendadas com base no codec de formato de vídeo selecionado.
1. No cabeçalho Tamanho do vídeo , verifique se **[!UICONTROL Manter proporção]** está marcada.
1. Defina a resolução do tamanho do quadro de vídeo em pixels. Use o **[!UICONTROL Automático]** para dimensionar automaticamente para corresponder à proporção de aspecto de origem (relação largura/altura). Por exemplo, Auto x 480 ou 640 x Auto.

1. Siga uma das seguintes opções:

   * No **[!UICONTROL Largura]** , insira **[!UICONTROL auto]**. No **[!UICONTROL Altura]** , insira um valor em pixels.

   * Para ajudá-lo a visualizar o tamanho do vídeo, selecione o ícone Informações (i) à direita de **[!UICONTROL Altura]** para abrir a página Calculadora de tamanho. Use **[!UICONTROL Calculadora de tamanho]** para definir as dimensões do vídeo (representadas pela caixa azul) desejada. Selecionar **[!UICONTROL X]** no canto superior direito quando terminar.

1. (Opcional) Selecione o **[!UICONTROL Avançado]** e garanta que a função **[!UICONTROL Usar valores padrão]** estiver selecionada (recomendada). Como alternativa, modifique configurações avançadas de vídeo e áudio.
1. No canto superior direito da página, selecione **[!UICONTROL Salvar]** para salvar a predefinição.
1. Siga uma das seguintes opções:
   * Repita as etapas 4 a 10 para criar predefinições de codificação adicionais. (O streaming de vídeo adaptável requer mais de uma predefinição de vídeo.)
   * Prossiga para a próxima etapa.

1. (Opcional) Para adicionar o recorte inteligente de vídeo aos vídeos aos quais esse perfil é aplicado, faça o seguinte:
   * Na página Editar perfil de vídeo, à direita do cabeçalho Proporção de recorte inteligente , selecione **[!UICONTROL Adicionar novo]**.
   * No campo Nome , digite um nome para a proporção de corte que o ajude a identificá-lo facilmente.
   * No **[!UICONTROL Proporção de corte]** selecione a proporção que deseja usar.

1. Siga uma das seguintes opções:

   * Continue adicionando novas proporções de corte, conforme necessário.
   * Prossiga para a próxima etapa.

1. No canto superior direito da página, selecione **[!UICONTROL Salvar]** novamente para salvar o perfil.

Agora é possível aplicar o perfil às pastas que contêm vídeos. Consulte [Aplicar um perfil de vídeo a pastas](#applying-a-video-profile-to-folders) ou [Aplicar um perfil de vídeo globalmente](#applying-a-video-profile-globally).

## Criar um perfil de vídeo para transmissão progressiva {#creating-a-video-encoding-profile-for-progressive-streaming}

Se você optar por não usar a opção **[!UICONTROL Codificar para transmissão adaptável]**, todas as predefinições de codificação adicionadas ao perfil são tratadas como representações de vídeo individuais para transmissão de streaming com taxa de bits única ou entrega de vídeo progressiva. Além disso, não há validação para garantir que todas as representações de vídeo tenham a mesma proporção.

Dependendo do modo em que você está executando, os codecs de formato de vídeo aceitos são os seguintes:

* Modo Dynamic Media-Scene7: H.264 (.mp4)
* Dynamic Media-Modo híbrido: H.264 (.mp4), WebM

Consulte também [Criar um perfil de codificação de vídeo para transmissão adaptável da taxa de bits](#creating-a-video-encoding-profile-for-adaptive-streaming).

Consulte também [Práticas recomendadas para codificação de vídeo](/help/assets/video.md#best-practices-for-encoding-videos).

Para definir parâmetros de processamento avançados para outros tipos de ativos, consulte [Configurar o processamento de ativos](/help/assets/config-dms7.md#configuring-asset-processing).

**Para criar um perfil de vídeo para transmissão progressiva:**

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de vídeo]**.
1. Selecionar **[!UICONTROL Criar]** para adicionar um perfil de vídeo.
1. Insira um nome e uma descrição para o perfil.
1. Na página Criar/editar predefinições de codificação de vídeo , selecione **[!UICONTROL Adicionar predefinição de codificação de vídeo]**.
1. No **[!UICONTROL Básico]** , defina as opções de vídeo e áudio.
Selecione o ícone de informações ao lado de cada opção para obter descrições adicionais ou configurações recomendadas com base no codec de formato de vídeo selecionado.
1. (Opcional) No cabeçalho Tamanho do vídeo , desmarque **[!UICONTROL Manter proporção]**.
1. Faça o seguinte:
   * No **[!UICONTROL Largura]** , insira **[!UICONTROL auto]**.
   * No **[!UICONTROL Altura]** , insira um valor em pixels.
Para ajudar você a visualizar o tamanho do vídeo, selecione o ícone Height&#39;s information para abrir o **[!UICONTROL Calculadora de tamanho]** página. Use o **[!UICONTROL Calculadora de tamanho]** para definir ainda mais a dimensão do vídeo (caixa azul) como desejar. Quando terminar, no canto superior direito da caixa de diálogo, selecione **[!UICONTROL X]**.
1. (Opcional) Siga um destes procedimentos:

   * Selecione o **[!UICONTROL Avançado]** e verifique se a variável **[!UICONTROL Usar valores padrão]** estiver selecionada (recomendada).

   * Limpe o **[!UICONTROL Usar valores padrão]** e especifique as configurações de vídeo e áudio desejadas.
Selecione o ícone de informações ao lado de cada opção para obter descrições adicionais ou configurações recomendadas com base no codec de formato de vídeo selecionado.

1. No canto superior direito da página, selecione **[!UICONTROL Salvar]** para salvar a predefinição.
1. Siga uma das seguintes opções:

   * Repita as etapas de 4 a 9 para criar predefinições de codificação adicionais.
   * Prossiga para a próxima etapa.

1. (Opcional) Para adicionar o recorte inteligente de vídeo aos vídeos aos quais esse perfil é aplicado, faça o seguinte:

   * Na página Editar perfil de vídeo, à direita do cabeçalho Proporção de recorte inteligente , selecione **[!UICONTROL Adicionar novo]**.
   * No campo Nome , digite um nome para a proporção de corte que o ajude a identificá-lo facilmente.
   * No **[!UICONTROL Proporção de corte]** selecione a proporção que deseja usar.

1. Siga uma das seguintes opções:

   * Continue adicionando novas proporções de corte, conforme necessário.
   * Prossiga para a próxima etapa.

1. No canto superior direito da página, selecione **[!UICONTROL Salvar]** para salvar o perfil.

Agora é possível aplicar o perfil às pastas que contêm vídeos. Consulte [Aplicar um perfil de vídeo a pastas](#applying-a-video-profile-to-folders) ou [Aplicar um perfil de vídeo globalmente](#applying-a-video-profile-globally).

## Usar parâmetros de codificação de vídeo personalizados {#using-custom-added-video-encoding-parameters}

É possível editar um perfil de codificação de vídeo existente para aproveitar os parâmetros de codificação avançada de vídeo não encontrados na interface do usuário ao criar ou editar um Perfil de vídeo no Experience Manager. Adicione um ou mais parâmetros avançados - como minBitrate e maxBitrate - ao perfil existente.

**Para usar parâmetros de codificação de vídeo personalizados:**

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
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
   <td>Nível H.264 a ser usado na codificação. Normalmente, esse parâmetro é determinado automaticamente com base nas configurações de codificação que você está usando.</td>
   <td><code>String</code></td>
   <td><p>10 * h264 nível</p> <p>Por exemplo, 3,0 = 30, 1,3 = 13)</p> <p>Nenhum valor padrão.</p> </td>
  </tr>
  <tr>
   <td><code>keyframe</code></td>
   <td>O número alvo de quadros entre quadros-chave. Calcule esse valor para que ele possa gerar um quadro-chave a cada 2-10 segundos. Por exemplo, a 30 quadros por segundo, o intervalo do quadro-chave deve ser de 60 a 300.<br /> <br /> Intervalos de quadro-chave menores melhoram o comportamento de busca de fluxo e troca de fluxo para codificações de vídeo adaptáveis e também podem melhorar a qualidade de vídeos que têm muito movimento. No entanto, como os quadros-chave aumentam o tamanho de um arquivo, um intervalo de quadros-chave mais baixo normalmente resulta em uma menor qualidade geral do vídeo em uma determinada taxa de bits.</td>
   <td><code>String</code></td>
   <td><p>Número positivo.</p> <p>O padrão é 300.</p> <p>O valor recomendado para DASH ou HLS é de 60-90. (Para usar o DASH em seus vídeos, ele deve primeiro ser ativado em sua conta. Consulte <a href="/help/assets/video.md#enable-dash">Habilitar o DASH em sua conta</a>.)</p> </td>
  </tr>
  <tr>
   <td><code>minBitrate</code></td>
   <td><p>Taxa mínima de bits para permitir codificações variáveis de taxa de bits, em Kbps (kilobits por segundo).</p> <p>Esse parâmetro só se aplica quando<strong> Usar taxa de bits constante</strong> é desmarcada na guia Advanced ao criar ou editar um perfil de codificação de vídeo.</p> <p>Consulte também <a href="/help/assets/video.md#bitrate">Taxa de bits</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>Número positivo, em Kbps.</p> <p>Nenhum valor padrão.</p> </td>
  </tr>
  <tr>
   <td><code>maxBitrate</code></td>
   <td><p>Taxa de bits máxima para permitir codificações de taxa de bits variável, em Kbps.</p> <p>Esse parâmetro só se aplica quando<strong> Usar taxa de bits constante</strong> é desmarcada na guia Advanced ao criar ou editar um perfil de codificação de vídeo.</p> <p>Consulte também <a href="/help/assets/video.md#bitrate">Taxa de bits</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>Número positivo, em Kbps.</p> <p>Nenhum valor padrão. No entanto, o valor recomendado é até duas vezes a taxa de bits de codificação.</p> </td>
  </tr>
  <tr>
   <td><code>audioBitrateCustom</code></td>
   <td>Defina o valor como <code>true</code> para forçar uma taxa de bits constante para o fluxo de áudio, se suportado pelo codec de áudio.</td>
   <td><code>String</code></td>
   <td><p><code>true</code>/<code>false</code></p> <p>O padrão é <code>false</code>.</p> <p>O valor recomendado para DASH ou HLS é <code>false</code>. (Para usar o DASH em seus vídeos, ele deve primeiro ser ativado em sua conta. Consulte <a href="/help/assets/video.md#enable-dash">Habilitar o DASH em sua conta</a>.)</p> <p> </p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-516](assets/chlimage_1-516.png)

1. Ao lado do canto inferior direito da página, selecione **[!UICONTROL Adicionar]**.
1. Siga uma das seguintes opções:

   * Repita as etapas 3 e 4 para adicionar outro parâmetro ao perfil de codificação de vídeo.
   * Ao lado do canto superior esquerdo da página, selecione **[!UICONTROL Salvar tudo]**.

1. No canto superior esquerdo da página do CRXDE Lite, selecione o **[!UICONTROL Página inicial]** ícone para retornar ao Experience Manager.

### Editar um perfil de vídeo {#editing-a-video-encoding-profile}

É possível editar qualquer perfil de vídeo criado para adicionar, editar ou excluir predefinições de vídeo nesse perfil.

Por padrão, não é possível editar o predefinido e pronto para uso **[!UICONTROL Codificação de vídeo adaptável]** perfil que veio com o Dynamic Media. Em vez disso, você pode copiar facilmente o perfil e salvá-lo com um novo nome. Em seguida, você pode editar as predefinições desejadas no perfil copiado.

Consulte também [Práticas recomendadas para codificação de vídeo](/help/assets/video.md#best-practices-for-encoding-videos).

Para definir parâmetros de processamento avançados para outros tipos de ativos, consulte [Configurar o processamento de ativos](/help/assets/config-dms7.md#configuring-asset-processing).

**Para editar um perfil de vídeo:**

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de vídeo]**.
1. Na página Perfis de vídeo , verifique o nome de um perfil de vídeo.
1. Na barra de ferramentas, selecione **[!UICONTROL Editar]**.
1. Na página Perfil de codificação de vídeo , edite o nome e a descrição, conforme desejado.
1. Como prática recomendada, verifique se a variável **[!UICONTROL Codificar para transmissão adaptável da taxa de bits]** está selecionada.
Selecione o ícone de informações para obter uma descrição do fluxo de taxa de bits adaptável. (Se você estiver editando um perfil de vídeo progressivo, não marque essa caixa de seleção.)
1. No cabeçalho Predefinições de codificação de vídeo , adicione, edite ou exclua predefinições de codificação de vídeo que compõem o perfil.

   Selecione o ícone de informações ao lado de cada opção na **[!UICONTROL Básico]** e **[!UICONTROL Avançado]** para obter descrições adicionais ou configurações recomendadas com base no codec de formato de vídeo selecionado.

1. No canto superior direito da página, selecione **[!UICONTROL Salvar]**.

### Copiar um perfil de vídeo {#copying-a-video-encoding-profile}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de vídeo]**.
1. Na página Perfis de vídeo , verifique o nome de um perfil de vídeo.
1. Na barra de ferramentas, selecione **[!UICONTROL Copiar]**.
1. Na página Perfil de codificação de vídeo , digite um novo nome para o perfil.
1. Como prática recomendada, verifique se a caixa de seleção **[!UICONTROL Codificar para transmissão adaptável]** está selecionada. Selecione o ícone de informações para obter uma descrição do fluxo de taxa de bits adaptável. (Se você estiver copiando um perfil de vídeo progressivo, não marque a caixa de seleção.)

   No Dynamic Media - Modo híbrido, se uma predefinição de vídeo do WebM fizer parte do perfil de vídeo, **[!UICONTROL Codificar para transmissão adaptável]** não é possível porque todas as predefinições devem ser MP4.
1. No cabeçalho Predefinições de codificação de vídeo , adicione, edite ou exclua predefinições de codificação de vídeo que compõem o perfil.

   Selecione o ícone de informações ao lado de cada opção nas guias Básico e Avançado para obter as configurações e descrições recomendadas.

1. No canto superior direito da página, selecione **[!UICONTROL Salvar]**.

### Excluir um perfil de vídeo {#deleting-a-video-encoding-profile}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de vídeo]**.
1. Na página Perfis de vídeo , verifique um ou mais nomes de perfil de vídeo.
1. Na barra de ferramentas, selecione **[!UICONTROL Excluir]**.
1. Selecionar **[!UICONTROL OK]**.

## Aplicar um perfil de vídeo a pastas {#applying-a-video-profile-to-folders}

Ao atribuir um perfil de vídeo a uma pasta, qualquer subpasta herda automaticamente o perfil da pasta pai. Essa regra significa que você pode atribuir somente um perfil de vídeo a uma pasta. Dessa forma, considere cuidadosamente a estrutura de pastas de onde você faz upload, armazena, usa e arquiva ativos.

Se você atribuiu um perfil de vídeo diferente a uma pasta, o novo perfil substituirá o perfil anterior. Os ativos de pasta existentes anteriormente permanecem inalterados. O novo perfil é aplicado aos ativos que são adicionados à pasta posteriormente.

As pastas que têm um perfil atribuído a elas são indicadas na interface do usuário pela aparência do nome do perfil no nome do cartão.

![chlimage_1-517](assets/chlimage_1-517.png)

Você pode aplicar perfis de vídeo a pastas específicas ou globalmente a todos os ativos.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você alterou posteriormente. Consulte [Reprocessar ativos em uma pasta depois de ter editado seu perfil de processamento](processing-profiles.md#reprocessing-assets).

### Aplicar um perfil de vídeo a pastas específicas {#applying-video-profiles-to-specific-folders}

Aplique um perfil de vídeo a uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades]**. Esta seção descreve como aplicar perfis de vídeo a pastas de ambas as maneiras.

As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

Consulte também [Reprocessar ativos em uma pasta depois de ter editado seu perfil de processamento](processing-profiles.md#reprocessing-assets).

#### Aplicar um perfil de vídeo a pastas por meio da interface do usuário Perfis {#applying-video-profiles-to-folders-by-way-of-the-profiles-user-interface}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de vídeo]**.
1. Selecione o perfil de vídeo que deseja aplicar a uma ou várias pastas.
1. Selecionar **[!UICONTROL Aplicar perfil a pastas]** e selecione a pasta ou várias pastas que deseja usar para receber os ativos carregados recentemente e selecione **[!UICONTROL Aplicar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta enquanto estão na **[!UICONTROL Exibição de cartão]**.
Você pode [monitorar o progresso de um trabalho de processamento de perfil de vídeo](#monitoring-the-progress-of-an-encoding-job).

#### Aplicar um perfil de vídeo a pastas em Propriedades {#applying-video-profiles-to-folders-from-properties}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ativos]** e, em seguida, na pasta à qual deseja aplicar um perfil de vídeo.
1. Na pasta , selecione a marca de seleção para selecioná-la e, em seguida, selecione **[!UICONTROL Propriedades]**.
1. Selecione o **[!UICONTROL Perfis de vídeo]** e selecione o perfil no menu suspenso e selecione **[!UICONTROL Salvar e fechar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

   ![chlimage_1-518](assets/chlimage_1-518.png)
Você pode [monitorar o progresso de um trabalho de processamento de perfil de vídeo](#monitoring-the-progress-of-an-encoding-job).

### Aplicar um perfil de vídeo globalmente {#applying-a-video-profile-globally}

Além de aplicar um perfil a uma pasta, também é possível aplicar um globalmente para que qualquer conteúdo carregado no Experience Manager Assets em qualquer pasta tenha o perfil selecionado aplicado.

Consulte também [Reprocessar ativos em uma pasta depois de ter editado seu perfil de processamento](processing-profiles.md#reprocessing-assets).

**Para aplicar um perfil de vídeo globalmente:**

* Navegue até CRXDE Lite para o seguinte nó: `/content/dam/jcr:content`. Adicionar a propriedade `videoProfile:/libs/settings/dam/video/dynamicmedia/<name of video encoding profile>` e selecione **[!UICONTROL Salvar tudo]**.

   ![chlimage_1-519](assets/chlimage_1-519.png)
* Você pode [monitorar o progresso de um trabalho de processamento de perfil de vídeo](#monitoring-the-progress-of-an-encoding-job).

## Monitorar o progresso de um trabalho de processamento de perfil de vídeo {#monitoring-the-progress-of-an-encoding-job}

Um indicador de processamento (ou barra de progresso) é exibido para que você possa monitorar visualmente o progresso de um trabalho de processamento de perfil de vídeo.

Você também pode visualizar o `error.log` para monitorar o progresso de um trabalho de codificação, para ver se a codificação foi concluída ou para ver quaisquer erros de trabalho. O `error.log` é encontrado no `logs` pasta onde sua instância do Experience Manager está instalada.

## Remover um perfil de vídeo das pastas {#removing-a-video-profile-from-folders}

Ao remover um perfil de vídeo de uma pasta, qualquer subpasta herda automaticamente a remoção do perfil da pasta pai. No entanto, o processamento de arquivos que ocorreu dentro das pastas permanece intacto.

Remova um perfil de vídeo de uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, nas **[!UICONTROL Configurações da pasta]**. Esta seção descreve como remover perfis de vídeo de pastas de ambas as maneiras.

### Remover um perfil de vídeo das pastas por meio da interface do usuário Perfis {#removing-video-profiles-from-folders-by-way-of-the-profiles-user-interface}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de vídeo]**.
1. Selecione o perfil de vídeo que deseja remover de uma pasta ou de várias pastas.
1. Selecionar **[!UICONTROL Remover perfil das pastas]** e selecione a pasta ou várias pastas que deseja usar para remover o perfil e selecione **[!UICONTROL Remover]**.

   Você pode confirmar que o perfil de vídeo não é mais aplicado a uma pasta porque o nome não aparece mais abaixo do nome da pasta.

### Remover um perfil de vídeo das pastas por meio de Propriedades {#removing-video-profiles-from-folders-by-way-of-properties}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ativos]** e, em seguida, para a pasta da qual deseja remover um perfil de vídeo.
1. Na pasta , selecione a marca de seleção e selecione **[!UICONTROL Propriedades]**.
1. Selecione o **[!UICONTROL Perfis de vídeo]** e selecione **[!UICONTROL Nenhum]** no menu suspenso e selecione **[!UICONTROL Salvar e fechar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.
