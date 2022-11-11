---
title: Perfis de imagem do Dynamic Media
description: Crie perfis de imagem que contenham configurações para Tirar nitidez da máscara e recorte inteligente ou amostra inteligente, ou ambos, e aplique o perfil a uma pasta de ativos de imagem.
uuid: 9049fab9-d2be-4118-8684-ce58f3c8c16a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 4f9301db-edf8-480b-886c-b5e8fca5bf5c
feature: Image Profiles
role: User, Admin
exl-id: 67240ad0-1a7c-4e58-a518-1e36d771f1a1
source-git-commit: 3b869153e0fdee08df2a4aaf73fe3ce9fbebaad7
workflow-type: tm+mt
source-wordcount: '2831'
ht-degree: 10%

---

# Perfis de imagem do Dynamic Media {#image-profiles}

Ao carregar imagens, você pode cortar automaticamente a imagem ao carregá-la aplicando um perfil de imagem à pasta.

>[!IMPORTANT]
>
>・ O recorte inteligente está disponível somente no modo Dynamic Media - Scene7.
・ Os perfis de imagem não se aplicam a arquivos PDF, GIF animado ou INDD (Adobe InDesign).

## Opções de corte {#crop-options}

Quando você implementa o Recorte inteligente em imagens, o Adobe recomenda a seguinte prática recomendada e aplica o seguinte limite:

| Tipo de limite | Prática recomendada | Limite imposto | Alteração do limite em 31 de dezembro de 2022 |
| --- | --- | --- | --- |
| Número de Recortes Inteligentes por imagem | 5 | 100 | 20 |

Consulte também [Limitações do Dynamic Media](/help/assets/limitations.md).

<!-- CQDOC-16069 for paragraph directly below -->

As coordenadas de recorte inteligente dependem da taxa de proporção. Para as várias configurações de recorte inteligente em um perfil de imagem, se a proporção for a mesma para as dimensões adicionadas no perfil de imagem, a mesma proporção de aspecto será enviada para a Dynamic Media. O Adobe recomenda usar a mesma área de corte. Isso garante que não haja impacto para diferentes dimensões usadas no perfil de imagem.

Cada geração de Corte inteligente que você cria requer processamento extra. Por exemplo, adicionar mais de cinco taxas de proporção de Corte inteligente pode resultar em uma taxa lenta de ingestão de ativos. Também causa um aumento da carga nos sistemas. Como você pode aplicar o Recorte inteligente no nível da pasta, o Adobe recomenda usá-lo nas pastas *only* quando necessário.

Você tem duas opções de recorte de imagem que podem ser escolhidas. Você também tem uma opção para automatizar a criação de amostras de cores e imagens.

| Opção | Quando usar | Descrição |
| --- | --- | --- |
| Cortar pixel | Imagens de corte em massa com base somente em dimensões. | Para usar essa opção, selecione **[!UICONTROL Corte de pixels]** na lista suspensa Opções de corte .<br><br>Para cortar das laterais de uma imagem, você insere o número de pixels para cortar de qualquer lado ou de cada lado da imagem. A quantidade de imagens cortadas depende da configuração ppi (pixels por polegada) no arquivo de imagem.<br><br>Um corte de pixels do Perfil de imagem é renderizado da seguinte maneira:<br>・ Os valores são Superior, Inferior, Esquerda e Direita.<br>・ O canto superior esquerdo é considerado `0,0` e o corte de pixels é calculado a partir daí.<br>・ Ponto de partida do corte: A esquerda é X e a parte superior é Y<br>・ Cálculo horizontal: dimensão de pixel horizontal da imagem original menos Esquerda e depois menos Direita.<br>・ Cálculo vertical: altura vertical do pixel menos Superior e depois menos Inferior.<br><br>Por exemplo, suponha que você tenha uma imagem de 4000 x 3000 pixels. Você usa valores: Superior=250, Inferior=500, Esquerda=300, Direita=700.<br><br>Do canto superior esquerdo (300.250), corte usando o espaço de preenchimento de (4000-300-700, 3000-250-500 ou 3000.2250). |
| Corte inteligente | Imagens de corte em massa com base em seu ponto focal visual. | O Smart Crop usa o poder da inteligência artificial no Adobe Sensei para automatizar rapidamente o corte de imagens em massa. O Recorte inteligente detecta e recorta automaticamente o ponto focal em qualquer imagem para capturar o ponto de interesse pretendido, independentemente do tamanho da tela.</p> <p>Para usar o Recorte inteligente, selecione **[!UICONTROL Corte inteligente]** na lista suspensa Opções de recorte , à direita de Recorte responsivo de imagem, ative (ative) o recurso.</p> <p>Os tamanhos padrão de ponto de interrupção Grande, Médio e Pequeno geralmente abrangem a gama completa de tamanhos que a maioria das imagens é usada em dispositivos móveis e tablets, desktops e banners. Se desejar, você pode editar os nomes padrão de Grande, Médio e Pequeno.</p> <p>Para adicionar mais pontos de interrupção, selecione **[!UICONTROL Adicionar corte]** para excluir um corte, selecione o ícone Garbage Can . |
| Amostra de cor e imagem | Em massa gera uma amostra de imagem para cada imagem. | **Observação**: O Smart Swatch não é compatível com o Dynamic Media Classic.<br><br>Localize e gere automaticamente amostras de alta qualidade a partir de imagens de produto que mostram cor ou textura.<br><br>Para usar a Amostra de cores e imagens, selecione **[!UICONTROL Corte inteligente]** na lista suspensa Opções de recorte , à direita de Amostra de cor e imagem, ative (ative) o recurso. Insira um valor de pixel nas caixas de texto Largura e Altura .<br><br>Embora todas as recortes de imagem estejam disponíveis no painel Representações , as amostras são usadas somente por meio do recurso Copiar URL . Use seu próprio componente de visualização para renderizar a amostra em seu site. (A exceção a essa regra são os banners de carrossel. O Dynamic Media fornece o componente de visualização para a amostra usada em banners de carrossel.)<br><br>**Uso de amostras de imagem**<br> O URL para amostras de imagem é direto. É:<br><br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>em que `:Swatch` é anexada à solicitação de ativo.<br><br>**Uso de amostras de cores**<br> Para usar amostras de cores, você cria uma `req=userdata` com o seguinte:<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>Por exemplo, o seguinte é um ativo de amostra no Dynamic Media Classic:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>e aqui está o ativo de amostra correspondente `req=userdata` URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br><br>O `req=userdata` A resposta é a seguinte:<br>`SmartCropDef=Swatch SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br><br>Você também pode solicitar um `req=userdata` resposta no formato XML ou JSON, como nos seguintes exemplos de URL respectivos:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**Observação:** Crie seu próprio componente WCM para solicitar uma amostra de cores e analisar a `SmartSwatchColor` , representado por um valor RGB hexadecimal de 24 bits.<br><br>Consulte também [`userdata` no Guia de referência de visualizadores](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html). |

## Tirar nitidez da máscara {#unsharp-mask}

Use a **[!UICONTROL Tirar nitidez da máscara]** para ajustar um efeito de filtro de nitidez na imagem final com resolução reduzida. Você pode controlar a intensidade do efeito, o raio do efeito (medido em pixels) e um limite de contraste que é ignorado. Esse efeito usa as mesmas opções da Adobe Photoshop *Tirar nitidez da máscara* filtro.

>[!NOTE]
A Tirar nitidez da máscara é aplicada apenas a representações baixadas dentro do PTIFF (tiff de pirâmide) que têm uma resolução reduzida de mais de 50%. Isso significa que as representações de maior tamanho dentro do ptiff não são afetadas pela máscara de nitidez, enquanto representações de menor tamanho, como miniaturas, são alteradas (e mostram a máscara de nitidez).

Em **[!UICONTROL Tirar nitidez da máscara]**, você tem as seguintes opções de filtragem:

| Opção | Descrição |
| --- | --- |
| Quantidade | Controla a quantidade de contraste aplicado aos pixels da borda. O padrão é 1,75. Para imagens de alta resolução, é possível aumentá-lo para 5. Pense em Quantia como uma medida de intensidade de filtro. O intervalo é de 0 a 5. |
| Raio | Determina o número de pixels em torno dos pixels de borda que afetam a nitidez. Para imagens de alta resolução, insira de 1 a 2. Um valor baixo aplica nitidez apenas aos pixels de borda; um valor alto aplica nitidez a uma faixa mais ampla de pixels. O valor correto depende da imagem. O valor padrão é 0,2. O intervalo é de 0 a 250. |
| Limite | Determina o intervalo de contraste a ser ignorado quando o filtro de máscara de nitidez for aplicado. Em outras palavras, essa opção determina o quão diferentes os pixels com nitidez devem ser da área ao redor antes de serem considerados pixels de borda e terem nitidez. Para evitar a introdução de ruído, experimente valores entre 0 e 255. |

A nitidez é descrita em [Nitidez de imagens](/help/assets/assets/sharpening_images.pdf).

## Criar perfis de imagem do Dynamic Media {#creating-image-profiles}

Para definir parâmetros de processamento avançados para outros tipos de ativos, consulte [Configuração do processamento de ativos](config-dms7.md#configuring-asset-processing).

Consulte [Perfis para processar metadados, imagens e vídeos](processing-profiles.md).

Consulte também [Práticas recomendadas para organizar ativos digitais para usar perfis de processamento](/help/assets/organize-assets.md).

**Para criar perfis de imagem do Dynamic Media:**

1. Selecione o logotipo do Adobe Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de imagem]**.
1. Selecionar **[!UICONTROL Criar]** para que você possa adicionar um perfil de imagem.
1. Insira um nome de perfil e valores para Tirar nitidez da máscara, recortar ou amostra, ou ambos.

   Use um nome de perfil específico para a finalidade pretendida. Por exemplo, se você quiser criar um perfil que gera amostras somente, ou seja, o Recorte inteligente está desativado (desativado) e a Amostra de cor e imagem está ativada (ativada), use o nome de perfil &quot;Amostras inteligentes&quot;.

   Consulte também [Opções de recorte inteligente e amostra inteligente](#crop-options) e [Tirar nitidez da máscara](#unsharp-mask).

   ![cortar](assets/crop.png)

1. Selecione **[!UICONTROL Salvar]**. O perfil recém-criado aparece na lista de perfis disponíveis.

## Editar ou excluir perfis de imagem do Dynamic Media {#editing-or-deleting-image-profiles}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de imagem]**.
1. Selecione o perfil de imagem que deseja editar ou remover. Para editá-lo, selecione **[!UICONTROL Editar perfil de imagem]**. Para removê-lo, selecione **[!UICONTROL Excluir perfil de imagem]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Se estiver editando, salve as alterações. Se estiver excluindo, confirme se deseja remover o perfil.

## Aplicar um perfil de imagem do Dynamic Media a pastas {#applying-an-image-profile-to-folders}

Ao atribuir um perfil de imagem a uma pasta, qualquer subpasta herda automaticamente o perfil da pasta pai. Esse fluxo de trabalho significa que você pode atribuir somente um perfil de imagem a uma pasta. Dessa forma, considere cuidadosamente a estrutura de pastas de onde você faz upload, armazena, usa e arquiva ativos.

Se você atribuiu um perfil de imagem diferente a uma pasta, o novo perfil substituirá o perfil anterior. Os ativos de pasta existentes anteriormente permanecem inalterados. O novo perfil é aplicado aos ativos que são adicionados à pasta posteriormente.

As pastas que têm um perfil atribuído a elas são indicadas na interface do usuário usando o nome do perfil que aparece no cartão.

<!-- When you add smart crop to an existing image profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Você pode aplicar perfis de imagem a pastas específicas ou globalmente a todos os ativos.

Você pode reprocessar ativos em uma pasta que já tem um perfil de imagem existente que você alterou posteriormente. Consulte [Reprocessar ativos em uma pasta depois de ter editado seu perfil de processamento](processing-profiles.md#reprocessing-assets).

### Aplicar perfis de imagem do Dynamic Media a pastas específicas {#applying-image-profiles-to-specific-folders}

Aplique um perfil de imagem a uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades]**. Esta seção descreve como aplicar perfis de imagem a pastas de ambas as maneiras.

As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você alterou posteriormente. Consulte [Reprocessar ativos em uma pasta depois de ter editado seu perfil de processamento](processing-profiles.md#reprocessing-assets).

#### Aplicar perfis de imagem do Dynamic Media a pastas da interface do usuário Perfis {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de imagem]**.
1. Selecione o perfil de imagem que deseja aplicar a uma ou várias pastas.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Selecionar **[!UICONTROL Aplicar perfil de processamento a pastas]** e selecione a pasta ou várias pastas que deseja usar para receber os ativos carregados recentemente e selecione **[!UICONTROL Aplicar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

#### Aplicar perfis de imagem do Dynamic Media a pastas de Propriedades {#applying-image-profiles-to-folders-from-properties}

1. Selecione o logotipo do Experience League e navegue até **[!UICONTROL Ativos]**. Em seguida, navegue até a pasta pai da pasta à qual deseja aplicar um perfil de imagem.
1. Na pasta , selecione a marca de seleção para selecioná-la e, em seguida, selecione **[!UICONTROL Propriedades]**.
1. Selecione o **[!UICONTROL Perfis de imagem]** guia . No **[!UICONTROL Nome do perfil]** lista suspensa, selecione o perfil e selecione **[!UICONTROL Salvar e fechar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Aplicar um perfil de imagem do Dynamic Media globalmente {#applying-an-image-profile-globally}

Além de aplicar um perfil a uma pasta, também é possível aplicar um globalmente para que qualquer conteúdo carregado nos ativos do Experience Manager em qualquer pasta tenha o perfil selecionado aplicado.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você alterou posteriormente. Consulte o [reprocessando de ativos em uma pasta após a edição do perfil de processamento](processing-profiles.md#reprocessing-assets).

**Para aplicar um perfil de imagem do Dynamic Media globalmente:**

1. Siga uma das seguintes opções:

   * Navegar para `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` e aplique o perfil apropriado e selecione **[!UICONTROL Salvar]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * Navegue até CRXDE Lite para o seguinte nó: `/content/dam/jcr:content`.

      Adicionar a propriedade `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` e selecione **[!UICONTROL Salvar tudo]**.

      ![configure_image_profiles](assets/configure_image_profiles.png)

## Editar o recorte inteligente ou a amostra inteligente de uma única imagem {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
O recorte inteligente está disponível somente no modo Dynamic Media - Scene7.

Você pode realinhar ou redimensionar manualmente a janela de recorte inteligente de uma imagem para refinar ainda mais seu ponto focal.

Depois de editar um recorte inteligente e salvar, a alteração é propagada em todos os locais em que você usa o recorte para as imagens específicas.

Você pode executar o recorte inteligente novamente para gerar as culturas adicionais, se necessário.

Consulte também [Editar o recorte inteligente ou a amostra inteligente de várias imagens](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Para editar o recorte inteligente ou a amostra inteligente de uma única imagem:**

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ativos]**, em seguida, na pasta que tem um recorte inteligente ou um perfil de imagem de amostra inteligente aplicado a ele.

1. Selecione a pasta para abrir seu conteúdo.
1. Selecione a imagem cujo recorte inteligente ou amostra inteligente você deseja ajustar.
1. Na barra de ferramentas, selecione **[!UICONTROL Corte inteligente]**.

1. Siga um destes procedimentos:

   * Próximo ao canto superior direito da página, arraste a barra de controle deslizante para a esquerda ou para a direita para aumentar ou diminuir a exibição da imagem, respectivamente.
   * Na imagem, arraste uma alça de canto para ajustar o tamanho da área visível do corte ou amostra.
   * Na imagem, arraste a caixa/amostra para um novo local. Você só pode editar amostras de imagens; amostras de cores são estáticas.
   * Acima da imagem, selecione  **[!UICONTROL Reverter]** para desfazer todas as edições e restaurar o corte ou a amostra original.

1. Ao lado do canto superior direito da página, selecione **[!UICONTROL Salvar]**, em seguida selecione **[!UICONTROL Fechar]** para retornar à pasta de ativos.

## Editar o recorte inteligente ou a amostra inteligente de várias imagens {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

Depois de aplicar um perfil de imagem - contendo o Recorte inteligente - a uma pasta, todas as imagens nessa pasta terão um recorte aplicado a elas. Se desejar, é possível *manualmente* realinhar ou redimensionar a janela de recorte inteligente em várias imagens para refinar ainda mais seu ponto focal.

Depois de editar um recorte inteligente e salvar, a alteração é propagada em todos os locais em que você usa o recorte para as imagens específicas.

Você pode executar o recorte inteligente novamente para gerar as culturas adicionais, se necessário.

**Para editar o recorte inteligente ou a amostra inteligente de várias imagens:**

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ativos]**, em seguida, em uma pasta que tenha um recorte inteligente ou um perfil de imagem de amostra inteligente aplicado a ele.
1. Na pasta , selecione o **[!UICONTROL Mais ações]** ícone (...) e selecione **[!UICONTROL Corte inteligente]**.

1. No **[!UICONTROL Editar recortes inteligentes]** , siga um destes procedimentos:

   * Ajuste o tamanho de visualização das imagens na página.

      À direita da lista suspensa nome do ponto de interrupção, arraste a barra de controle deslizante para a esquerda ou para a direita para alterar o tamanho da exibição da imagem visível.

      ![edit_smart_measures-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * Filtre a lista de imagens visíveis com base nos nomes dos pontos de interrupção. No exemplo abaixo, as imagens são filtradas no nome do ponto de interrupção &quot;Médio&quot;.

      Próximo ao canto superior direito da página, na lista suspensa, selecione um nome de ponto de interrupção para filtrar quais imagens você vê. (Veja a imagem acima.)

      ![edit_smart_measures-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * Redimensione a caixa de recorte inteligente. Siga um destes procedimentos:

      * Se a imagem tiver um recorte inteligente ou apenas uma amostra inteligente, arraste a alça do canto da caixa de recorte para ajustar o tamanho da área visível do recorte.
      * Se a imagem tiver um recorte inteligente e uma amostra inteligente, arraste a alça do canto da caixa de recorte para ajustar o tamanho da área visível do recorte. Ou selecione a amostra inteligente abaixo da imagem (as amostras de cores são estáticas), em seguida, arraste a alça do canto da caixa de corte para ajustar o tamanho da área visível da amostra.

      ![Redimensionar o recorte inteligente de uma imagem](assets/edit_smart_crops-resize.png)

   * Mova a caixa de recorte inteligente. Siga um destes procedimentos:

      * Se a imagem tiver um recorte inteligente ou apenas uma amostra inteligente, arraste a caixa de recorte para um novo local.
      * Se a imagem tiver um recorte inteligente e uma amostra inteligente, arraste a caixa de recorte inteligente para um novo local. Ou selecione a amostra inteligente abaixo da imagem (as amostras de cores são estáticas), em seguida, arraste a caixa de recorte da amostra inteligente para um novo local.

      ![edit_smart_measures-move](assets/edit_smart_crops-move.png)

   * Desfaça todas as suas edições e restaure o recorte inteligente original ou a amostra inteligente (aplica-se somente à sessão de edição atual).

      Selecionar **[!UICONTROL Reverter]** acima da imagem.

      ![edit_smart_measures-revert](assets/edit_smart_crops-revert.png)



1. Ao lado do canto superior direito da página, selecione **[!UICONTROL Salvar]**, em seguida selecione **[!UICONTROL Fechar]** para retornar à pasta de ativos.

## Remover um perfil de imagem do Dynamic Media das pastas {#removing-an-image-profile-from-folders}

Ao remover um perfil de imagem de uma pasta, qualquer subpasta herda automaticamente a remoção do perfil da pasta pai. No entanto, o processamento de arquivos que ocorreu dentro das pastas permanece intacto.

Remova um perfil de imagem de uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades]**. Esta seção descreve como remover perfis de imagem de pastas de ambas as maneiras.

### Remover perfis de imagem do Dynamic Media de pastas por meio da interface do usuário de Perfis {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de imagem]**.
1. Selecione o perfil de imagem que deseja remover de uma pasta ou de várias pastas.
1. Selecionar **[!UICONTROL Remover perfil de processamento das pastas]** e selecione a pasta ou várias pastas que deseja usar para remover o perfil e selecione **[!UICONTROL Remover]**.

   Você pode confirmar que o perfil de imagem não é mais aplicado a uma pasta porque o nome não aparece mais abaixo do nome da pasta.

### Remover perfis de imagem do Dynamic Media de pastas por meio de Propriedades {#removing-image-profiles-from-folders-via-properties}

1. Selecione o logotipo do Experience Manager e navegue **[!UICONTROL Ativos]** e, em seguida, para a pasta da qual deseja remover um perfil de imagem.
1. Na pasta , selecione a marca de seleção para selecioná-la e, em seguida, selecione **[!UICONTROL Propriedades]**.
1. Selecione o **[!UICONTROL Perfis de imagem]** guia .
1. No **[!UICONTROL Nome do perfil]** , selecione **[!UICONTROL Nenhum]**, em seguida selecione **[!UICONTROL Salvar e fechar]**.

   As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.
