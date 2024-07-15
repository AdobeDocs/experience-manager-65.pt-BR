---
title: Perfis de vídeo
description: O Dynamic Media já vem com um perfil de Codificação de vídeo adaptável predefinido. As configurações desse perfil pronto para uso são otimizadas para fornecer aos clientes a melhor experiência de visualização possível. Você também pode adicionar recorte inteligente aos seus vídeos.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
docset: aem65
feature: Video Profiles
role: User, Admin
mini-toc-levels: 3
exl-id: b290fac2-7259-45d7-b733-70419d632b07
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3770'
ht-degree: 8%

---

# Perfis de vídeo {#video-profiles}

O Dynamic Media já vem com um perfil de Codificação de vídeo adaptável predefinido. As configurações desse perfil pronto para uso são otimizadas para fornecer aos clientes a melhor experiência de visualização possível. Ao codificar os vídeos de origem primária usando o perfil Codificação de vídeo adaptável, durante a reprodução o reprodutor de vídeo ajusta automaticamente a qualidade do fluxo de vídeo com base na velocidade de conexão com a Internet dos clientes. Essa funcionalidade é conhecida como transmissão adaptável de taxa de bits.

Estes são outros fatores que determinam a qualidade dos seus vídeos:

* **Resolução do vídeo de origem primária carregado**

  Se o vídeo MP4 foi gravado em uma resolução mais baixa, como 240p ou 360p, ele não poderá ser transmitido em alta definição.

* **Tamanho do player de vídeo**

  Por padrão, a &quot;Largura&quot; no perfil de Codificação de vídeo adaptável está definida como &quot;Automática&quot;. Novamente, durante a reprodução, a melhor qualidade é usada com base no tamanho do reprodutor.

Consulte [Práticas recomendadas de codificação de vídeo](/help/assets/video.md#best-practices-for-encoding-videos).

Consulte também [Práticas recomendadas para organizar sua Assets digital para usar Perfis de processamento](/help/assets/organize-assets.md).

>[!NOTE]
>
>Para gerar os metadados de um vídeo e as miniaturas de imagem de vídeo associadas, o próprio vídeo deve passar pelo processo de codificação no Dynamic Media. No Adobe Experience Manager, o fluxo de trabalho **[!UICONTROL Codificação de vídeo do Dynamic Media]** codifica o vídeo se você tiver habilitado o Dynamic Media e configurado os serviços da nuvem de vídeo. Esse fluxo de trabalho captura o histórico do processo de fluxo de trabalho e as informações de falha. Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](/help/assets/video.md#monitoring-video-encoding-and-youtube-publishing-progress). Se você habilitou o Dynamic Media e configurou os serviços da nuvem de vídeo, o fluxo de trabalho **[!UICONTROL Codificação de vídeo do Dynamic Media]** será aplicado automaticamente quando você carregar um vídeo. (Se você não estiver usando o Dynamic Media, o fluxo de trabalho **[!UICONTROL Ativo de atualização do DAM]** entrará em vigor.)
>
>Os metadados são úteis ao pesquisar ativos. As miniaturas são imagens de vídeo estáticas geradas durante a codificação. Eles são exigidos pelo sistema Experience Manager e usados na interface do usuário para ajudar a identificar visualmente os vídeos na exibição Cartões, na exibição Resultados da pesquisa e na exibição da Lista de ativos. É possível ver as miniaturas geradas ao selecionar o ícone Representações (paleta de pintura) de um vídeo codificado.

Quando terminar de criar o perfil de vídeo, aplique-o a uma ou várias pastas. Consulte [Aplicar um perfil de vídeo a pastas](#applying-a-video-profile-to-folders).

Para definir parâmetros de processamento avançado para outros tipos de ativos, consulte [Configurar processamento de ativos](/help/assets/config-dms7.md#configuring-asset-processing).

Consulte também [Perfis para processamento de Metadados, Imagens e Vídeos](processing-profiles.md).

## Predefinições de codificação de vídeo adaptável {#adaptive-video-encoding-presets}

A tabela a seguir identifica os perfis de codificação de práticas recomendadas para streaming de vídeo adaptável em dispositivos móveis, tablets e computadores desktop. É possível usar essas predefinições para qualquer proporção de vídeo.

<table>
 <tbody>
  <tr>
   <td><strong>Codec de formatação do vídeo</strong></td>
   <td><strong>Tamanho do vídeo - Largura (px)</strong></td>
   <td><strong>Tamanho do vídeo - Altura (px)</strong></td>
   <td><strong>Manter taxa de proporção?</strong></td>
   <td><strong>Taxa De Bits Do Vídeo (Kbps)</strong></td>
   <td><strong>Taxa De Quadros Do Vídeo (Fps)</strong></td>
   <td><strong>Codec de áudio</strong></td>
   <td><strong>Taxa De Áudio (Kbps)</strong></td>
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

## Sobre o uso de recorte inteligente em perfis de vídeo {#about-smart-crop-video}

Recorte inteligente para vídeo - um recurso opcional disponível em Perfis de vídeo - é uma ferramenta que usa o poder da inteligência artificial do Adobe Sensei. Ele detecta e recorta automaticamente o ponto focal em qualquer vídeo adaptável ou progressivo que você tenha carregado, independentemente do tamanho.

Os formatos de vídeo compatíveis com o corte inteligente incluem MP4, MKV, MOV, AVI, FLV e WMV.

O tamanho máximo suportado do arquivo de vídeo para corte inteligente é o seguinte:

* Duração de cinco minutos.
* 30 quadros por segundo (FPS).
* Tamanho de arquivo de 300 MB.

O Adobe Sensei é limitado a 9000 quadros. Isto é, cinco minutos a 30 FPS. Se o vídeo tiver um FPS mais alto, a duração máxima de vídeo compatível diminui. Por exemplo, um vídeo de 60 FPS deve ter dois minutos e meio de duração para ser compatível com o Adobe Sensei e o recorte inteligente.

![Recorte inteligente para vídeo](assets/smart-crop-video.png)

>[!IMPORTANT]
>
>Para que o recorte inteligente de vídeo funcione, é necessário incluir uma ou mais predefinições de codificação de vídeo no perfil de vídeo.

Para usar o recorte inteligente para vídeo, você cria um perfil de codificação de vídeo adaptável ou progressivo. Como parte do seu perfil, use a ferramenta **[!UICONTROL Taxa de Corte Inteligente]** para selecionar taxas de aspecto predefinidas. Por exemplo, depois de definir as predefinições de codificação de vídeo, é possível adicionar uma definição de &quot;Paisagem móvel&quot; com uma proporção largura/altura de 16×9 e uma definição de &quot;Retrato móvel&quot; com uma proporção largura/altura de 9×16. Outros aspectos ou proporções de corte dentre os quais você pode escolher incluem 1×1, 4×3 e 4×5.

![Editar um perfil de codificação de vídeo com recorte inteligente](assets/edit-smart-crop-video2.png)

Você pode alternar entre ativado e desativado o recorte inteligente de vídeo no perfil de vídeo usando o controle deslizante à direita da **[!UICONTROL Proporção de recorte inteligente]** na interface.

Depois de criar e salvar seu perfil de vídeo, você pode aplicá-lo às pastas desejadas.

Consulte [Aplicar perfis de vídeo a pastas específicas](#applying-video-profiles-to-specific-folders) ou [Aplicar um perfil de vídeo globalmente](#applying-a-video-profile-globally).

Consulte também [Recorte inteligente para imagens](image-profiles.md).

## Criar um perfil de vídeo para transmissão adaptável da taxa de bits {#creating-a-video-encoding-profile-for-adaptive-streaming}

O Dynamic Media já vem com um perfil de codificação de vídeo adaptável predefinido - um grupo de configurações de upload de vídeo para MP4 H.264 - que é otimizado para obter a melhor experiência de visualização. Você pode usar este perfil quando carregar seus vídeos.

No entanto, se esse perfil predefinido não atender às suas necessidades, você pode optar por criar seu próprio perfil de codificação de vídeo adaptável. Ao usar a configuração **[!UICONTROL Codificar para transmissão adaptável]** - como prática recomendada - todas as predefinições de codificação adicionadas ao perfil são validadas para garantir que todos os vídeos tenham a mesma proporção. Além disso, os vídeos codificados são tratados como uma taxa de multi bits definidos para transmissão.

Ao criar o perfil de codificação de vídeo, observe que a maioria das opções de codificação é pré-preenchida com configurações padrão recomendadas para ajudar. No entanto, se você selecionar um valor diferente do padrão recomendado, poderá resultar em baixa qualidade de vídeo durante a reprodução e outros problemas de desempenho.

Assim, para todas as predefinições de codificação de vídeo MP4 H.264 no perfil, os seguintes valores são validados para garantir que sejam os mesmos em todas as predefinições individuais de codificação no perfil, possibilitando o streaming da taxa de bits adaptável:

* Codec de formato de vídeo - MP4 H.264 (.mp4)
* Codec de áudio
* Taxa de áudio
* Manter taxa de proporção
* Codificação em dois passos
* Taxa de bits constante
* Perfil H264
* Taxa de amostra do áudio

Se os valores não forem os mesmos, você pode continuar criando o perfil como está. No entanto, a transmissão adaptável da taxa de bits não é possível. Em vez disso, os usuários experimentam transmissão com taxa de bits única. É recomendável editar as configurações de codificação para usar os mesmos valores em predefinições individuais de codificação no perfil. (O editor de perfil de vídeo/predefinição impõe a paridade das configurações de codificação de vídeo adaptável se **[!UICONTROL Codificar para transmissão adaptável]** estiver habilitado.)

Consulte também [Criar um perfil de codificação de vídeo para streaming progressivo](#creating-a-video-encoding-profile-for-progressive-streaming).

Consulte também [Práticas recomendadas de codificação de vídeo](/help/assets/video.md#best-practices-for-encoding-videos).

Para definir parâmetros de processamento avançado para outros tipos de ativos, consulte [Configurar processamento de ativos](/help/assets/config-dms7.md#configuring-asset-processing).

**Para criar um perfil de vídeo para transmissão adaptável da taxa de bits**,

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de Vídeo]**.
1. Selecione **[!UICONTROL Criar]** para adicionar um perfil de vídeo.

1. Insira um nome e uma descrição para o perfil.
1. Na página Criar/Editar Predefinições de Codificação de Vídeo, selecione **[!UICONTROL Adicionar Predefinição de Codificação de Vídeo]**.
1. Na guia **[!UICONTROL Básico]**, defina as opções de vídeo e áudio.
Selecione o ícone de informações ao lado de cada opção para obter descrições adicionais ou configurações recomendadas com base no codec de formato de vídeo selecionado.
1. No cabeçalho Tamanho do vídeo, verifique se **[!UICONTROL Manter taxa de proporção]** está marcada.
1. Defina a resolução do tamanho do quadro do vídeo em pixels. Use o valor **[!UICONTROL Automático]** para dimensionar automaticamente para corresponder à taxa de proporção de origem (largura e altura). Por exemplo, Automático x 480 ou 640 x Automático.

1. Siga uma das seguintes opções:

   * No campo **[!UICONTROL Largura]**, digite **[!UICONTROL auto]**. No campo **[!UICONTROL Altura]**, digite um valor em pixels.

   * Para ajudá-lo a visualizar o tamanho do vídeo, selecione o ícone Informações (i) à direita de **[!UICONTROL Altura]** para abrir a página Calculadora de tamanho. Use a **[!UICONTROL Calculadora de Tamanho]** para definir as dimensões do vídeo (representadas pela caixa azul) desejadas. Selecione **[!UICONTROL X]** no canto superior direito quando terminar.

1. (Opcional) Selecione a guia **[!UICONTROL Avançado]** e certifique-se de que a caixa de seleção **[!UICONTROL Usar valores padrão]** esteja marcada (recomendado). Como alternativa, modifique as configurações avançadas de vídeo e áudio.
1. No canto superior direito da página, selecione **[!UICONTROL Salvar]** para salvar a predefinição.
1. Siga uma das seguintes opções:
   * Repita as etapas 4 a 10 para criar predefinições de codificação adicionais. (O streaming de vídeo adaptável requer mais de uma predefinição de vídeo.)
   * Continue com a próxima etapa.

1. (Opcional) Para adicionar o recorte inteligente de vídeo aos vídeos aos quais esse perfil é aplicado, faça o seguinte:
   * Na página Editar perfil de vídeo, à direita do cabeçalho Proporção de corte inteligente, selecione **[!UICONTROL Adicionar novo]**.
   * No campo Nome, digite um nome para a taxa de corte que ajude a identificá-la facilmente.
   * Na lista suspensa **[!UICONTROL Taxa de Corte]**, selecione a taxa que deseja usar.

1. Siga uma das seguintes opções:

   * Continue adicionando novas taxas de corte, conforme necessário.
   * Continue com a próxima etapa.

1. No canto superior direito da página, selecione **[!UICONTROL Salvar]** novamente para salvar o perfil.

Agora é possível aplicar o perfil às pastas que contêm vídeos. Consulte [Aplicar um perfil de vídeo a pastas](#applying-a-video-profile-to-folders) ou [Aplicar um perfil de vídeo globalmente](#applying-a-video-profile-globally).

## Criar um perfil de vídeo para transmissão progressiva {#creating-a-video-encoding-profile-for-progressive-streaming}

Se você optar por não usar a opção **[!UICONTROL Codificar para transmissão adaptável]**, todas as predefinições de codificação adicionadas ao perfil serão tratadas como representações de vídeo individuais para transmissão de streaming com taxa de bits única ou entrega de vídeo progressiva. Além disso, não há validação para garantir que todas as representações de vídeo tenham a mesma proporção.

Dependendo do modo em que você estiver executando, os codecs de formato de vídeo compatíveis são os seguintes:

* Modo Dynamic Media-Scene7: H.264 (.mp4)
* Modo Dynamic Media-Hybrid: H.264 (.mp4), WebM

Consulte também [Criar um perfil de codificação de vídeo para transmissão adaptável da taxa de bits](#creating-a-video-encoding-profile-for-adaptive-streaming).

Consulte também [Práticas recomendadas de codificação de vídeo](/help/assets/video.md#best-practices-for-encoding-videos).

Para definir parâmetros de processamento avançado para outros tipos de ativos, consulte [Configurar processamento de ativos](/help/assets/config-dms7.md#configuring-asset-processing).

**Para criar um perfil de vídeo para transmissão progressiva:**

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de Vídeo]**.
1. Selecione **[!UICONTROL Criar]** para adicionar um perfil de vídeo.
1. Insira um nome e uma descrição para o perfil.
1. Na página Criar/Editar Predefinições de Codificação de Vídeo, selecione **[!UICONTROL Adicionar Predefinição de Codificação de Vídeo]**.
1. Na guia **[!UICONTROL Básico]**, defina as opções de vídeo e áudio.
Selecione o ícone de informações ao lado de cada opção para obter descrições adicionais ou configurações recomendadas com base no codec de formato de vídeo selecionado.
1. (Opcional) No cabeçalho Tamanho do vídeo, desmarque **[!UICONTROL Manter taxa de proporção]**.
1. Faça o seguinte:
   * No campo **[!UICONTROL Largura]**, digite **[!UICONTROL auto]**.
   * No campo **[!UICONTROL Altura]**, digite um valor em pixels.
Para ajudá-lo a visualizar o tamanho do vídeo, selecione o ícone Informações de altura para abrir a página **[!UICONTROL Calculadora de tamanho]**. Use a página **[!UICONTROL Calculadora de tamanho]** para definir ainda mais a dimensão do vídeo (caixa azul) como desejar. Quando terminar, no canto superior direito da caixa de diálogo, selecione **[!UICONTROL X]**.
1. (Opcional) Siga um destes procedimentos:

   * Selecione a guia **[!UICONTROL Avançado]** e verifique se a caixa de seleção **[!UICONTROL Usar Valores Padrão]** está marcada (recomendado).

   * Desmarque a caixa de seleção **[!UICONTROL Usar Valores Padrão]** e especifique as configurações de vídeo e áudio desejadas.
Selecione o ícone de informações ao lado de cada opção para obter descrições adicionais ou configurações recomendadas com base no codec de formato de vídeo selecionado.

1. No canto superior direito da página, selecione **[!UICONTROL Salvar]** para salvar a predefinição.
1. Siga uma das seguintes opções:

   * Repita as etapas 4 a 9 para criar predefinições de codificação adicionais.
   * Continue com a próxima etapa.

1. (Opcional) Para adicionar o recorte inteligente de vídeo aos vídeos aos quais esse perfil é aplicado, faça o seguinte:

   * Na página Editar perfil de vídeo, à direita do cabeçalho Proporção de corte inteligente, selecione **[!UICONTROL Adicionar novo]**.
   * No campo Nome, digite um nome para a taxa de corte que ajude a identificá-la facilmente.
   * Na lista suspensa **[!UICONTROL Taxa de Corte]**, selecione a taxa que deseja usar.

1. Siga uma das seguintes opções:

   * Continue adicionando novas taxas de corte, conforme necessário.
   * Continue com a próxima etapa.

1. No canto superior direito da página, selecione **[!UICONTROL Salvar]** para salvar o perfil.

Agora é possível aplicar o perfil às pastas que contêm vídeos. Consulte [Aplicar um perfil de vídeo a pastas](#applying-a-video-profile-to-folders) ou [Aplicar um perfil de vídeo globalmente](#applying-a-video-profile-globally).

## Usar parâmetros de codificação de vídeo adicionados personalizados {#using-custom-added-video-encoding-parameters}

É possível editar um perfil de codificação de vídeo existente para aproveitar os parâmetros avançados de codificação de vídeo que não são encontrados na interface do usuário ao criar ou editar um Perfil de vídeo no Experience Manager. Adicione um ou mais parâmetros avançados, como minBitrate e maxBitrate, ao perfil existente.

**Para usar parâmetros de codificação de vídeo adicionados personalizados:**

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
   <td>Nível H.264 a ser usado para codificação. Normalmente, esse parâmetro é determinado automaticamente com base nas configurações de codificação que você está usando.</td>
   <td><code>String</code></td>
   <td><p>10 * nível h264</p> <p>Por exemplo, 3,0 = 30, 1,3 = 13)</p> <p>Nenhum valor padrão.</p> </td>
  </tr>
  <tr>
   <td><code>keyframe</code></td>
   <td>O número alvo de quadros entre quadros-chave. Calcule esse valor para que ele possa gerar um quadro-chave a cada 2-10 segundos. Por exemplo, a 30 quadros por segundo, o intervalo do quadro principal deve ser de 60 a 300.<br /> <br /> Os intervalos de quadro-chave mais baixos melhoram a busca por transmissão e o comportamento de comutação de fluxo para codificações de vídeo adaptáveis e também podem melhorar a qualidade de vídeos com muito movimento. No entanto, como os quadros-chave aumentam o tamanho de um arquivo, um intervalo de quadro-chave menor geralmente resulta em uma qualidade geral de vídeo mais baixa em uma determinada taxa de bits.</td>
   <td><code>String</code></td>
   <td><p>Número positivo.</p> <p>O padrão é 300.</p> <p>O valor recomendado para DASH ou HLS é 60-90. (Para usar o DASH em seus vídeos, primeiro ele deve estar ativado em sua conta. Consulte <a href="/help/assets/video.md#enable-dash">Habilitar DASH na sua conta</a>.)</p> </td>
  </tr>
  <tr>
   <td><code>minBitrate</code></td>
   <td><p>Taxa de bits mínima para permitir codificações variáveis de taxa de bits, em Kbps (kilobits por segundo).</p> <p>Esse parâmetro só se aplica quando <strong> Usar taxa de bits constante</strong> é desmarcado na guia Avançado ao criar ou editar um perfil de codificação de vídeo.</p> <p>Consulte também <a href="/help/assets/video.md#bitrate">Taxa de bits</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>Número positivo, em Kbps.</p> <p>Nenhum valor padrão.</p> </td>
  </tr>
  <tr>
   <td><code>maxBitrate</code></td>
   <td><p>Taxa de bits máxima para permitir codificações variáveis de taxa de bits, em Kbps.</p> <p>Esse parâmetro só se aplica quando <strong> Usar taxa de bits constante</strong> é desmarcado na guia Avançado ao criar ou editar um perfil de codificação de vídeo.</p> <p>Consulte também <a href="/help/assets/video.md#bitrate">Taxa de bits</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>Número positivo, em Kbps.</p> <p>Nenhum valor padrão. No entanto, o valor recomendado é até duas vezes a taxa de bits da codificação.</p> </td>
  </tr>
  <tr>
   <td><code>audioBitrateCustom</code></td>
   <td>Defina o valor como <code>true</code> para forçar uma taxa de bits constante para o fluxo de áudio, se suportado pelo codec de áudio.</td>
   <td><code>String</code></td>
   <td><p><code>true</code>/<code>false</code></p> <p>O padrão é <code>false</code>.</p> <p>O valor recomendado para DASH ou HLS é <code>false</code>. (Para usar o DASH em seus vídeos, primeiro ele deve estar ativado em sua conta. Consulte <a href="/help/assets/video.md#enable-dash">Habilitar DASH na sua conta</a>.)</p> <p> </p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-516](assets/chlimage_1-516.png)

1. Próximo ao canto inferior direito da página, selecione **[!UICONTROL Adicionar]**.
1. Siga uma das seguintes opções:

   * Repita as etapas 3 e 4 para adicionar outro parâmetro ao perfil de codificação de vídeo.
   * Próximo ao canto superior esquerdo da página, selecione **[!UICONTROL Salvar tudo]**.

1. No canto superior esquerdo da página de CRXDE Lite, selecione o ícone **[!UICONTROL Voltar à página inicial]** para retornar ao Experience Manager.

### Editar um perfil de vídeo {#editing-a-video-encoding-profile}

É possível editar qualquer perfil de vídeo criado para adicionar, editar ou excluir predefinições de vídeo nesse perfil.

Por padrão, você não pode editar o perfil predefinido **[!UICONTROL Codificação de vídeo adaptável]** que veio com o Dynamic Media. Em vez disso, você pode copiar o perfil facilmente e salvá-lo com um novo nome. É possível editar as predefinições desejadas no perfil copiado.

Consulte também [Práticas recomendadas de codificação de vídeo](/help/assets/video.md#best-practices-for-encoding-videos).

Para definir parâmetros de processamento avançado para outros tipos de ativos, consulte [Configurar processamento de ativos](/help/assets/config-dms7.md#configuring-asset-processing).

**Para editar um perfil de vídeo:**

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de Vídeo]**.
1. Na página Perfis de vídeo, marque um nome de perfil de vídeo.
1. Na barra de ferramentas, selecione **[!UICONTROL Editar]**.
1. Na página Perfil de codificação de vídeo, edite o nome e a descrição, conforme desejado.
1. Como prática recomendada, verifique se a caixa de seleção **[!UICONTROL Codificar para transmissão adaptável da taxa de bits]** está marcada.
Selecione o ícone de informações para obter uma descrição da transmissão adaptável da taxa de bits. (Se você estiver editando um perfil de vídeo progressivo, não marque essa caixa de seleção.)
1. No cabeçalho Predefinições de codificação de vídeo, adicione, edite ou exclua predefinições de codificação de vídeo que compõem o perfil.

   Selecione o ícone de informações ao lado de cada opção nas guias **[!UICONTROL Básico]** e **[!UICONTROL Avançado]** para obter descrições adicionais ou configurações recomendadas com base no codec de formato de vídeo selecionado.

1. No canto superior direito da página, selecione **[!UICONTROL Salvar]**.

### Copiar um perfil de vídeo {#copying-a-video-encoding-profile}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de Vídeo]**.
1. Na página Perfis de vídeo, marque um nome de perfil de vídeo.
1. Na barra de ferramentas, selecione **[!UICONTROL Copiar]**.
1. Na página Perfil de codificação de vídeo, digite um novo nome para o perfil.
1. Como prática recomendada, verifique se a caixa de seleção **[!UICONTROL Codificar para transmissão adaptável]** está selecionada. Selecione o ícone de informações para obter uma descrição da transmissão adaptável da taxa de bits. (Se você estiver copiando um perfil de vídeo progressivo, não marque a caixa de seleção.)

   No modo Dynamic Media - Híbrido, se uma predefinição de vídeo WebM fizer parte do perfil de vídeo, **[!UICONTROL a codificação para o fluxo adaptável]** não será possível, pois todas as predefinições devem ser MP4.
1. No cabeçalho Predefinições de codificação de vídeo, adicione, edite ou exclua predefinições de codificação de vídeo que compõem o perfil.

   Selecione o ícone de informações ao lado de cada opção nas guias Básico e Avançado para obter as configurações e descrições recomendadas.

1. No canto superior direito da página, selecione **[!UICONTROL Salvar]**.

### Excluir um perfil de vídeo {#deleting-a-video-encoding-profile}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de Vídeo]**.
1. Na página Perfis de vídeo, verifique um ou mais nomes de perfis de vídeo.
1. Na barra de ferramentas, selecione **[!UICONTROL Excluir]**.
1. Selecione **[!UICONTROL OK]**.

## Aplicar um perfil de vídeo a pastas {#applying-a-video-profile-to-folders}

Ao atribuir um perfil de vídeo a uma pasta, todas as subpastas herdam automaticamente o perfil da pasta principal. Essa regra significa que você pode atribuir somente um perfil de vídeo a uma pasta. Dessa forma, considere cuidadosamente a estrutura de pastas de onde você faz upload, armazena, usa e arquiva ativos.

Se você atribuiu um perfil de vídeo diferente a uma pasta, o novo perfil substituirá o perfil anterior. Os ativos de pasta existentes anteriormente permanecem inalterados. O novo perfil é aplicado aos ativos que são adicionados à pasta posteriormente.

As pastas que têm um perfil atribuído a elas são indicadas na interface pelo aspecto do nome do perfil no nome do cartão.

![chlimage_1-517](assets/chlimage_1-517.png)

Aplique perfis de vídeo a pastas específicas ou globalmente a todos os ativos.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você alterou posteriormente. Consulte [Reprocessar ativos em uma pasta depois de editar seu perfil de processamento](processing-profiles.md#reprocessing-assets).

### Aplicar um perfil de vídeo a pastas específicas {#applying-video-profiles-to-specific-folders}

Aplique um perfil de vídeo a uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades]**. Esta seção descreve como aplicar perfis de vídeo a pastas de ambas as maneiras.

As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

Consulte também [Reprocessar ativos em uma pasta depois de editar seu perfil de processamento](processing-profiles.md#reprocessing-assets).

#### Aplicar um perfil de vídeo a pastas por meio da interface do usuário Perfis {#applying-video-profiles-to-folders-by-way-of-the-profiles-user-interface}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de Vídeo]**.
1. Selecione o perfil de vídeo que deseja aplicar a uma ou várias pastas.
1. Selecione **[!UICONTROL Aplicar perfil às pastas]** e selecione uma ou várias pastas que deseja usar para receber os ativos carregados recentemente e selecione **[!UICONTROL Aplicar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta enquanto estão na **[!UICONTROL Exibição de Cartão]**.
Você pode [monitorar o progresso de um trabalho de processamento de perfil de vídeo](#monitoring-the-progress-of-an-encoding-job).

#### Aplicar um perfil de vídeo a pastas em Propriedades {#applying-video-profiles-to-folders-from-properties}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Assets]** e, em seguida, até a pasta à qual você deseja aplicar um perfil de vídeo.
1. Na pasta, marque a marca de seleção para selecioná-la e selecione **[!UICONTROL Propriedades]**.
1. Selecione a guia **[!UICONTROL Perfis de Vídeo]**, selecione o perfil no menu suspenso e selecione **[!UICONTROL Salvar e Fechar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

   ![chlimage_1-518](assets/chlimage_1-518.png)
Você pode [monitorar o progresso de um trabalho de processamento de perfil de vídeo](#monitoring-the-progress-of-an-encoding-job).

### Aplicar um perfil de vídeo globalmente {#applying-a-video-profile-globally}

Além de aplicar um perfil a uma pasta, também é possível aplicá-lo globalmente para que qualquer conteúdo carregado no Experience Manager Assets em qualquer pasta tenha o perfil selecionado aplicado.

Consulte também [Reprocessar ativos em uma pasta depois de editar seu perfil de processamento](processing-profiles.md#reprocessing-assets).

**Para aplicar um perfil de vídeo globalmente:**

* Navegue até o CRXDE Lite para o seguinte nó: `/content/dam/jcr:content`. Adicione a propriedade `videoProfile:/libs/settings/dam/video/dynamicmedia/<name of video encoding profile>` e selecione **[!UICONTROL Salvar tudo]**.

  ![chlimage_1-519](assets/chlimage_1-519.png)
* Você pode [monitorar o progresso de um trabalho de processamento de perfil de vídeo](#monitoring-the-progress-of-an-encoding-job).

## Monitorar o progresso de um trabalho de processamento de perfil de vídeo {#monitoring-the-progress-of-an-encoding-job}

Um indicador de processamento (ou barra de progresso) é exibido para que você possa monitorar visualmente o progresso de um trabalho de processamento de perfil de vídeo.

Você também pode exibir o arquivo `error.log` para monitorar o progresso de um trabalho de codificação, para ver se a codificação foi concluída ou para ver quaisquer erros de trabalho. O `error.log` é encontrado na pasta `logs` onde sua instância do Experience Manager está instalada.

## Remover um perfil de vídeo das pastas {#removing-a-video-profile-from-folders}

Ao remover um perfil de vídeo de uma pasta, todas as subpastas herdam automaticamente a remoção do perfil da pasta principal. No entanto, qualquer processamento de arquivos que tenha ocorrido nas pastas permanece intacto.

Remova um perfil de vídeo de uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, nas **[!UICONTROL Configurações da pasta]**. Esta seção descreve como remover perfis de vídeo de pastas de ambas as maneiras.

### Remover um perfil de vídeo das pastas por meio da interface do usuário Perfis {#removing-video-profiles-from-folders-by-way-of-the-profiles-user-interface}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de Vídeo]**.
1. Selecione o perfil de vídeo que deseja remover de uma ou várias pastas.
1. Selecione **[!UICONTROL Remover Perfil das Pastas]**, selecione uma ou várias pastas que deseja usar para remover o perfil e selecione **[!UICONTROL Remover]**.

   Você pode confirmar que o perfil de vídeo não é mais aplicado a uma pasta porque o nome não aparece mais abaixo do nome da pasta.

### Remova um perfil de vídeo das pastas por meio de Propriedades {#removing-video-profiles-from-folders-by-way-of-properties}

1. Selecione o logotipo do Experience Manager e navegue até o **[!UICONTROL Assets]** e, em seguida, acesse a pasta da qual deseja remover um perfil de vídeo.
1. Na pasta, marque a marca de seleção e selecione **[!UICONTROL Propriedades]**.
1. Selecione a guia **[!UICONTROL Perfis de Vídeo]**, selecione **[!UICONTROL Nenhum]** no menu suspenso e selecione **[!UICONTROL Salvar e Fechar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.
