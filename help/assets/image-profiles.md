---
title: Perfis de imagem do Dynamic Media
description: Crie perfis de imagem que contenham configurações para máscara de nitidez e recorte inteligente ou amostra inteligente, ou ambos, e depois aplique o perfil a uma pasta de ativos de imagem.
uuid: 9049fab9-d2be-4118-8684-ce58f3c8c16a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 4f9301db-edf8-480b-886c-b5e8fca5bf5c
translation-type: tm+mt
source-git-commit: d40488ce830eb15b4209145df03dff027f9a2470
workflow-type: tm+mt
source-wordcount: '2682'
ht-degree: 14%

---


# Perfis de imagem do Dynamic Media {#image-profiles}

Ao fazer upload de imagens, você pode cortar automaticamente a imagem ao fazer upload aplicando um perfil de imagem à pasta.

>[!NOTE]
>
>O Smart Crop está disponível somente no modo Mídia dinâmica - Scene7.

>[!IMPORTANT]
>
>perfis de imagem não se aplicam a arquivos PDF.

## Crop options {#crop-options}

<!-- CQDOC-16069 -->Smart Crop coordinates are aspect ratio dependent. That is, for the various smart crop settings in an image profile, if the aspect ratio is the same for the added dimensions that are in the image profile, then the same aspect ratio is sent to Dynamic media. Because of this, Adobe recommends that you use the same crop area. Doing so will ensure that there is no impact to different dimensions used in the image profile.

Esteja ciente de que cada geração de Recorte inteligente criada requer processamento extra. Por exemplo, adicionar mais de cinco proporções de Recorte inteligente pode resultar em uma taxa lenta de ingestão de ativos. Ele também pode causar um aumento da carga nos sistemas. Como você pode aplicar o Smart Crop no nível da pasta, a Adobe recomenda usá-lo em pastas *somente* onde for necessário.

Você tem duas opções de recorte de imagem nas quais pode escolher. Você também tem uma opção para automatizar a criação de amostras de cores e imagens.

<table>
 <tbody>
  <tr>
   <td><strong>Opção</strong></td>
   <td><strong>Quando usar</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Cortar pixel</td>
   <td>Imagens de corte em massa com base apenas em dimensões.</td>
   <td><p>Para usar essa opção, selecione Cortar <strong></strong> pixels na lista suspensa Opções de corte.</p> <p>Para cortar das laterais de uma imagem, insira o número de pixels a serem cortados de qualquer lado ou de cada lado da imagem. A quantidade de imagens cortadas depende da configuração ppi (pixels por polegada) no arquivo de imagem.</p> <p>Um recorte de pixel de Perfil de imagem é renderizado da seguinte maneira:<br /> </p>
    <ul>
     <li>Os valores são Superior, Inferior, Esquerda e Direita.</li>
     <li>A parte superior esquerda é considerada 0,0 e o corte de pixels é calculado a partir daí.</li>
     <li>Ponto de partida do corte: A esquerda é X e a parte superior é Y</li>
     <li>Cálculo horizontal: dimensão em pixels horizontais da imagem original menos Esquerda e depois menos Direita.</li>
     <li>Cálculo vertical: altura vertical do pixel menos Superior e depois menos Inferior.</li>
    </ul> <p>Por exemplo, suponha que você tenha uma imagem de 4000 x 3000 pixels. Você usa valores: Superior=250, Inferior=500, Esquerda=300, Direita=700.</p> <p>Do canto superior esquerdo (300.250) recorte usando o espaço de preenchimento de (4000-300-700, 3000-250-500 ou 3000.2250).</p> </td>
  </tr>
  <tr>
   <td>Corte inteligente</td>
   <td>Imagens de corte em massa com base em seu ponto focal visual.</td>
   <td><p>O Smart Crop usa o poder da inteligência artificial no Adobe Sensei para automatizar rapidamente o recorte de imagens em massa. O Smart Crop detecta e recorta automaticamente o ponto focal em qualquer imagem para capturar o ponto de interesse pretendido, independentemente do tamanho da tela.</p> <p>Para usar o Recorte inteligente, selecione Recorte <strong></strong> inteligente na lista suspensa Opções de recorte e, à direita de Recorte de imagem responsiva, ative (ative) o recurso.</p> <p>Os tamanhos padrão de pontos de interrupção Grandes, Médios e Pequenos geralmente abrangem a gama completa de tamanhos que a maioria das imagens são usadas em dispositivos móveis e tablets, desktops e banners. Se desejar, edite os nomes padrão de Grande, Médio e Pequeno.</p> <p>Para adicionar mais pontos de interrupção, clique em <strong>Adicionar corte</strong>; para excluir um corte, clique no ícone Garbage Can.</p> </td>
  </tr>
  <tr>
   <td>Amostra de cor e imagem</td>
   <td>Gerar uma amostra de imagem em massa para cada imagem.</td>
   <td><p><strong>Observação</strong>: A Smart Swatch não é compatível com o Dynamic Media Classic.</p> <p>Localize e gere automaticamente amostras de alta qualidade a partir de imagens de produtos que mostram cor ou textura.</p> <p>Para usar a Amostra de cores e imagens, selecione Recorte <strong></strong> inteligente na lista suspensa Opções de recorte e, à direita de Amostra de cores e imagens, ative (ative) o recurso. Insira um valor de pixel nas caixas de texto Largura e Altura.</p> <p>Enquanto todos os recortes de imagem estão disponíveis no painel Representações, as amostras são usadas somente por meio do recurso Copiar URL. Observe que você deve usar seu próprio componente de visualização para renderizar a amostra em seu site. (A exceção a isso são banners de carrossel. O Dynamic Media fornece o componente de visualização da amostra usada em banners de carrossel.)</p> <p><strong>Uso de amostras de imagem</strong></p> <p>O URL para amostras de imagem é direto. Ou seja:</p> <p><code>/is/image/company/&lt;asset_name&gt;:Swatch</code></p> <p>em que <code>:Swatch</code> é anexado à solicitação de ativo.</p> <p><strong>Uso de amostras de cores</strong></p> <p>Para usar amostras de cores, faça uma <code>req=userdata</code> solicitação com o seguinte:</p> <p><code>/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata</code></p> <p>Por exemplo, este é um ativo de amostra no Dynamic Media Classic (Scene7):</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch</code></p> <p>e este é o <code>req=userdata</code> URL correspondente do ativo de amostra:</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata</code></p> <p>A <code>req=userdata</code> resposta é a seguinte:</p> <p><code class="code">SmartCropDef=Swatch
       SmartCropHeight=200.0
       SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200
       SmartCropType=Swatch
       SmartCropWidth=200.0
       SmartSwatchColor=0xA56DB2</code></p> <p>Você também pode solicitar uma <code>req=userdata</code> resposta no formato XML ou JSON, como nos seguintes exemplos de URL:</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml</code></p><p><code>SmartSwatchColor</code></p><p></p></td></tr></tbody></table>

## Tirar nitidez da máscara {#unsharp-mask}

Use a **[!UICONTROL Tirar nitidez da máscara]** para ajustar um efeito de filtro de nitidez na imagem final com resolução reduzida. Controle a intensidade do efeito, o raio do efeito (medido em pixels) e um limite de contraste que será ignorado. Esse efeito usa as mesmas opções do filtro &quot;Tirar nitidez da máscara&quot; do Adobe Photoshop.

>[!NOTE]
>
>A máscara de nitidez só é aplicada a representações em baixa dentro do PTIFF (tiff de pirâmide) com resolução reduzida superior a 50%. Isso significa que as renderizações de maior tamanho dentro do ptiff não são afetadas por máscara de nitidez, enquanto representações de menor tamanho, como miniaturas, são alteradas (e mostrarão a máscara de nitidez).

Em Máscara de **[!UICONTROL nitidez]**, você tem as seguintes opções de filtragem:

<table>
 <tbody>
  <tr>
   <td><strong>Opção</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Quantidade</td>
   <td>Controla a quantidade de contraste aplicada aos pixels da borda. O padrão é 1,75. Para imagens de alta resolução, é possível aumentar para até 5. Pense em Amount como uma medida da intensidade do filtro. O intervalo é de 0 a 5.</td>
  </tr>
  <tr>
   <td>Raio</td>
   <td>Determina o número de pixels em torno dos pixels de borda que afetam a nitidez. Para imagens de alta resolução, insira de 1 a 2. Um valor baixo aplica nitidez apenas aos pixels de borda; um valor alto aplica nitidez a uma faixa mais ampla de pixels. O valor correto depende da imagem. O valor padrão é 0,2. O intervalo é de 0 a 250.</td>
  </tr>
  <tr>
   <td>Limite</td>
   <td><p>Determina o intervalo de contraste a ser ignorado quando o filtro de máscara de nitidez é aplicado. Em outras palavras, essa opção determina o quão diferentes os pixels com nitidez devem ser da área ao redor antes que sejam considerados pixels de borda e sejam apontados. Para evitar a introdução de ruído, experimente valores entre 0 e 255.</p> </td>
  </tr>
 </tbody>
</table>

O ajuste de nitidez é descrito em Imagens [de]ajuste de nitidez (/help/assets/assets/s7_sharpening_images.pdf).

## Creating Dynamic Media Image Profiles {#creating-image-profiles}

Para definir parâmetros de processamento avançados para outros tipos de ativos, consulte [Configuração do processamento](config-dms7.md#configuring-asset-processing)de ativos.

Consulte [Perfis para processar metadados, imagens e vídeos](processing-profiles.md).

Consulte também Práticas [recomendadas para organizar seus ativos digitais para usar Perfis](/help/assets/organize-assets.md)de processamento.

**Para criar Perfis de Imagem de Mídia Dinâmica**

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Image Profiles]**.
1. Toque em **[!UICONTROL Criar]** para adicionar um novo perfil de imagem.
1. Insira um nome de perfil e valores para máscara de nitidez, recorte ou amostra, ou ambos.

   Você pode achar útil usar um nome de perfil que seja específico para a finalidade pretendida. Por exemplo, se você deseja criar um perfil que gera apenas amostras, ou seja, o Smart Crop está desativado (desativado) e o Color e Image Swatch está ativado (ativado), você pode usar o nome do perfil &quot;Smart Swatches&quot;.

   Consulte também [Opções de recorte inteligente e amostra inteligente](#crop-options) e [Tirar nitidez da máscara](#unsharp-mask).

   ![cortar](assets/crop.png)

1. Toque em **[!UICONTROL Salvar]**. O perfil recém-criado é exibido na lista dos perfis disponíveis.

## Edição ou exclusão de Perfis de imagem de mídia dinâmica {#editing-or-deleting-image-profiles}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Image Profiles]**.
1. Selecione o perfil de imagem que deseja editar ou remover. Para editá-la, selecione **[!UICONTROL Editar Perfil]** de processamento de imagem. Para removê-lo, selecione **[!UICONTROL Excluir Perfil]** de processamento de imagem.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Se estiver editando, salve as alterações. Se estiver excluindo, confirme que deseja remover o perfil.

## Aplicar um perfil de imagem do Dynamic Media a pastas {#applying-an-image-profile-to-folders}

Quando você atribui um perfil de imagem a uma pasta, qualquer subpasta herda automaticamente o perfil da pasta pai. Isso significa que você pode atribuir apenas um perfil de imagem a uma pasta. Dessa forma, considere cuidadosamente a estrutura de pastas de onde você carrega, armazena, usa e arquiva ativos.

Se você atribuiu um perfil de imagem diferente a uma pasta, o novo perfil substituirá o perfil anterior. Os ativos de pasta existentes anteriormente permanecem inalterados. O novo perfil é aplicado aos ativos adicionados posteriormente à pasta.

As pastas que têm um perfil atribuído a ele são indicadas na interface do usuário pelo nome do perfil que aparece no cartão.

<!-- When you add smart crop to an existing image profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Você pode aplicar perfis de imagem a pastas específicas ou globalmente a todos os ativos.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de imagem existente que você tenha alterado posteriormente. Consulte o [reprocessando de ativos em uma pasta após a edição do perfil de processamento](processing-profiles.md#reprocessing-assets).

### Aplicar perfis de imagem do Dynamic Media a pastas específicas {#applying-image-profiles-to-specific-folders}

Aplique um perfil de imagem a uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades]**. Esta seção descreve como aplicar perfis de imagem a pastas de ambas as maneiras.

As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você tenha alterado posteriormente. Consulte o [reprocessando de ativos em uma pasta após a edição do perfil de processamento](processing-profiles.md#reprocessing-assets).

#### Aplicação de perfis de imagem do Dynamic Media a pastas da interface do usuário do Perfil {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Image Profiles]**.
1. Selecione o perfil de imagem que deseja aplicar a uma pasta ou várias pastas.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Tap **[!UICONTROL Apply Processing Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and tap/click **[!UICONTROL Apply]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

#### Aplicação de perfis de imagem do Dynamic Media a pastas a partir de Propriedades {#applying-image-profiles-to-folders-from-properties}

1. Toque no logotipo do AEM e navegue até **[!UICONTROL Assets]** e, em seguida, para a pasta à qual deseja aplicar um perfil de imagem.
1. Na pasta, toque na marca de seleção para selecioná-la e, em seguida, toque em **[!UICONTROL Propriedades]**.
1. Toque na guia **[!UICONTROL Perfis de imagem]**. Na lista suspensa **[!UICONTROL Nome do perfil]**, selecione o perfil e toque em **[!UICONTROL Salvar e fechar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Aplicar um perfil de imagem do Dynamic Media globalmente {#applying-an-image-profile-globally}

Além de aplicar um perfil a uma pasta, também é possível aplicar um globalmente para que qualquer conteúdo carregado em ativos AEM em qualquer pasta tenha o perfil selecionado aplicado.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você tenha alterado posteriormente. Consulte o [reprocessando de ativos em uma pasta após a edição do perfil de processamento](processing-profiles.md#reprocessing-assets).

**Para aplicar um perfil de imagem do Dynamic Media globalmente**:

1. Faça uma das seguintes opções:

   * Navegue até `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` e aplique o perfil apropriado e toque em **[!UICONTROL Salvar]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * Navegue até CRXDE Lite até o seguinte nó: `/content/dam/jcr:content`.

      Adicione a propriedade `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` e toque em **[!UICONTROL Salvar tudo]**.

      ![configure_image_perfis](assets/configure_image_profiles.png)

## Editar o recorte inteligente ou a amostra inteligente de uma única imagem {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!NOTE]
>
>O Smart Crop está disponível somente no modo Mídia dinâmica - Scene7.

Você pode realinhar ou redimensionar manualmente a janela de recorte inteligente de uma imagem para refinar ainda mais seu ponto focal.

Depois de editar um recorte inteligente e salvar, a alteração é propagada em qualquer lugar em que você usa o recorte para as imagens específicas.

Você pode executar novamente o recorte inteligente para gerar as colheitas adicionais novamente, se necessário.

Consulte também [Edição do recorte inteligente ou da amostra inteligente de várias imagens](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Para editar o recorte inteligente ou a amostra inteligente de uma única imagem**:

1. Toque no logotipo do AEM e navegue até **[!UICONTROL Assets]**, em seguida, para a pasta que tem um recorte inteligente ou um perfil de imagem de amostra aplicado a ele.

1. Toque na pasta para abrir seu conteúdo.
1. Toque na imagem cujo recorte inteligente ou amostra inteligente você deseja ajustar.
1. Na barra de ferramentas, toque em **[!UICONTROL Recortar]** inteligente.

1. Siga um destes procedimentos:

   * Próximo ao canto superior direito da página, arraste a barra deslizante para a esquerda ou direita para aumentar ou diminuir a exibição da imagem, respectivamente.
   * Na imagem, arraste uma alça de canto para ajustar o tamanho da área visível do corte ou da amostra.
   * Na imagem, arraste a caixa/amostra até um novo local. Você só pode editar amostras de imagem; as amostras de cores são estáticas.
   * Acima da imagem, toque em **[!UICONTROL Reverter]** para desfazer todas as edições e restaurar o recorte ou a amostra original.

1. Próximo ao canto superior direito da página, toque em **[!UICONTROL Salvar]** e, em seguida, em **[!UICONTROL Fechar]** para retornar à pasta de ativos.

## Editar o recorte inteligente ou a amostra inteligente de várias imagens {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

Depois de aplicar um perfil de imagem - que contém o Smart Crop - a uma pasta, todas as imagens dessa pasta terão um recorte aplicado a elas. Se desejar, você pode realinhar *manualmente* ou redimensionar a janela de recorte inteligente em várias imagens para refinar ainda mais o ponto focal.

Depois de editar um recorte inteligente e salvar, a alteração é propagada em qualquer lugar em que você usa o recorte para as imagens específicas.

Você pode executar novamente o recorte inteligente para gerar as colheitas adicionais novamente, se necessário.

**Para editar o recorte inteligente ou a amostra inteligente de várias imagens**:

1. Toque no logotipo do AEM e navegue até **[!UICONTROL Assets]**, em seguida, para uma pasta que tenha um recorte inteligente ou um perfil de imagem de amostra aplicado a ele.
1. Na pasta, toque no ícone **[!UICONTROL Mais ações]** (...) e, em seguida, em **[!UICONTROL Recortar]** inteligente.

1. Na página **[!UICONTROL Editar recortes]** inteligentes, execute um dos procedimentos a seguir:

   * Ajuste o tamanho de exibição das imagens na página.

      À direita da lista suspensa do nome do ponto de interrupção, arraste a barra deslizante para a esquerda ou direita para alterar o tamanho da exibição da imagem visível.

      ![edit_smart_ches-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * Filtre a lista de imagens visualizáveis com base em nomes de pontos de interrupção. No exemplo abaixo, as imagens são filtradas no nome do ponto de interrupção &quot;Médio&quot;.

      Próximo ao canto superior direito da página, na lista suspensa, selecione um nome de ponto de interrupção para filtrar as imagens que você vê. (Consulte a imagem acima.)

      ![edit_smart_lines-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * Redimensione a caixa de corte inteligente. Execute um dos procedimentos a seguir:

      * Se a imagem tiver apenas um recorte inteligente ou uma amostra inteligente, arraste na imagem a alça do canto da caixa de recorte para ajustar o tamanho da área visível do recorte.
      * Se a imagem tiver um recorte inteligente e uma amostra inteligente, arraste a alça do canto da caixa de recorte para ajustar o tamanho da área visível do recorte. Ou, toque ou clique na amostra inteligente abaixo da imagem (as amostras de cores são estáticas), em seguida, arraste a alça do canto da caixa de corte para ajustar o tamanho da área visível da amostra.
      ![Redimensionamento do recorte inteligente de uma imagem.](assets/edit_smart_crops-resize.png)

   * Mova a caixa de recorte inteligente. Execute um dos procedimentos a seguir:

      * Se a imagem tiver apenas um recorte inteligente ou uma amostra inteligente, arraste a caixa de recorte para um novo local.
      * Se a imagem tiver um recorte inteligente e uma amostra inteligente, arraste a caixa de recorte inteligente para um novo local. Ou, toque ou clique na amostra inteligente abaixo da imagem (as amostras de cores são estáticas) e arraste a caixa de recorte de amostra inteligente para um novo local.
      ![edit_smart_ches-move](assets/edit_smart_crops-move.png)

   * Desfaça todas as edições e restaure o recorte inteligente ou a amostra inteligente original (aplica-se somente à sessão de edição atual).

      Toque em **[!UICONTROL Reverter]** acima da imagem.

      ![edit_smart_lines-revert](assets/edit_smart_crops-revert.png)



1. Near the upper-right corner of the page, tap **[!UICONTROL Save]**. em seguida, toque em **[!UICONTROL Fechar]** para retornar à pasta de ativos.

## Remoção de um perfil de imagem de pastas {#removing-an-image-profile-from-folders}

Quando você remove um perfil de imagem de uma pasta, qualquer subpasta herda automaticamente a remoção do perfil da pasta pai. No entanto, qualquer processamento de arquivos que tenha ocorrido dentro das pastas permanece intacto.

Remova um perfil de imagem de uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades]**. Esta seção descreve como remover perfis de imagem de pastas de ambas as maneiras.

### Remoção de perfis de imagem do Dynamic Media de pastas por meio da interface do usuário do Perfil {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Image Profiles]**.
1. Selecione o perfil de imagem que deseja remover de uma pasta ou de várias pastas.
1. Toque em **[!UICONTROL Remover perfil de processamento das pastas]** e selecione uma ou várias pastas que deseja usar para remover o perfil e toque em **[!UICONTROL Remover]**.

   Você pode confirmar que o perfil de imagem não é mais aplicado a uma pasta porque o nome não aparece mais abaixo do nome da pasta.

### Remoção de perfis de imagem do Dynamic Media de pastas por meio de Propriedades {#removing-image-profiles-from-folders-via-properties}

1. Toque no logotipo do AEM e navegue **[!UICONTROL pelos Ativos]** e, em seguida, até a pasta da qual você deseja remover um perfil de imagem.
1. Na pasta, toque na marca de seleção para selecioná-la e, em seguida, toque em **[!UICONTROL Propriedades]**.
1. Select the **[!UICONTROL Image Profiles]** tab.
1. From the **[!UICONTROL Profile Name]** drop-down list, select **[!UICONTROL None]**, then tap **[!UICONTROL Save &amp; Close]**.

   As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.
