---
title: Perfis de imagem Dynamic Media
description: Crie Perfis de imagem que contenham configurações para Tirar nitidez da máscara e Recorte inteligente ou Amostra inteligente, ou ambos, e aplique o perfil a uma pasta de ativos de imagem.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
exl-id: 67240ad0-1a7c-4e58-a518-1e36d771f1a1
solution: Experience Manager, Experience Manager Assets
source-git-commit: a4c95d604e63c4fd00f17d2fb99a9e46f823ca10
workflow-type: tm+mt
source-wordcount: '3063'
ht-degree: 4%

---

# Perfis de imagem Dynamic Media {#image-profiles}

Ao fazer upload de imagens, você pode cortar automaticamente a imagem após o upload aplicando um Perfil de imagem à pasta.

>[!IMPORTANT]
>
>* O Recorte inteligente está disponível somente no modo Dynamic Media - Scene7.
>* Os perfis de imagem não se aplicam a arquivos PDF, animado GIF ou INDD (Adobe InDesign).

## Opções de corte {#crop-options}

Ao implementar o Recorte inteligente em imagens, o Adobe recomenda a seguinte prática recomendada e impõe o seguinte limite:

| Tipo de limite | Prática recomendada | Limite imposto |
| --- | --- | --- |
| Número de cortes inteligentes por imagem | 5 | 100 |

Consulte também [limitações do Dynamic Media](/help/assets/limitations.md).

<!-- CQDOC-16069 for paragraph directly below -->

As coordenadas de corte inteligente dependem da taxa de proporção. Para as várias configurações de recorte inteligente em um Perfil de imagem, se a taxa de proporção for a mesma para as dimensões adicionadas no Perfil de imagem, a mesma taxa de proporção será enviada para o Dynamic Media. A Adobe recomenda usar a mesma área de corte. Isso garante que não haja impacto em diferentes dimensões usadas no Perfil de imagem.

Cada geração de Recorte inteligente criada requer processamento extra. Por exemplo, adicionar mais de cinco proporções de corte inteligente pode resultar em uma taxa de assimilação de ativos lenta. Também provoca um aumento de carga nos sistemas. Como você pode aplicar o Corte inteligente no nível da pasta, a Adobe recomenda usá-lo nas pastas *somente* onde for necessário.

**Diretrizes para definir o Corte inteligente em um Perfil de Imagem**
Para manter o uso do Corte inteligente sob controle e otimizar o tempo de processamento e o armazenamento das lavouras, a Adobe recomenda as seguintes diretrizes e dicas:

* Os ativos de imagem que terão um recorte inteligente aplicado a eles devem ter no mínimo 50 x 50 pixels ou mais.
* Idealmente, tenha de 10 a 15 recortes inteligentes por imagem para otimizar as taxas de tela e o tempo de processamento.
* Nomeie os cortes inteligentes com base nas dimensões do corte, não no uso final. Isso ajuda a otimizar para duplicatas em que uma única dimensão é usada em várias páginas.
* Crie perfis de imagem ao nível da página/tipo de ativo para pastas e subpastas específicas em vez de um perfil de recorte inteligente comum que é aplicado a todas as pastas ou todos os ativos.
* Um perfil de imagem aplicado a subpastas substitui um perfil de imagem aplicado à pasta.
* Um Perfil de Imagem que contém dimensões de corte inteligente duplicadas não é permitido.
* Perfis de imagem nomeados duplicados com opções de corte inteligente definidas não são permitidos.

Você tem duas opções de corte de imagem para escolher: Corte de pixels ou Corte inteligente. Também é possível optar por automatizar a criação de amostras de cores e imagens.

>[!IMPORTANT]
>
>* A Adobe recomenda que você analise todas as culturas e amostras geradas para garantir que elas sejam apropriadas e relevantes para sua marca e valores.
>* O formato de imagem CMYK não é compatível com o recorte inteligente.

| Opção | Quando usar | Descrição |
| --- | --- | --- |
| Cortar pixel | Imagens de corte em massa somente com base em dimensões. | Para usar esta opção, selecione **[!UICONTROL Recorte de pixel]** na lista suspensa Opções de Recorte.<br><br>Para recortar das laterais de uma imagem, digite o número de pixels a serem recortados de qualquer lado ou de cada lado da imagem. O quanto da imagem é cortada depende da configuração ppi (pixels por polegada) no arquivo de imagem.<br><br>Um corte de pixel do Perfil de Imagem é renderizado da seguinte maneira:<br>· Os valores são Superior, Inferior, Esquerdo e Direito.<br>· O canto superior esquerdo é considerado `0,0` e o recorte de pixels é calculado a partir desse ponto.<br>· Ponto inicial do recorte: Esquerda é X e Superior é Y<br>· Cálculo horizontal: dimensão em pixels horizontal da imagem original menos Esquerda e menos Direita.<br>· Cálculo vertical: altura vertical do pixel menos Superior e menos Inferior.<br><br>Por exemplo, suponha que você tenha uma imagem de 4000 x 3000 pixels. Você usa valores: Top=250, Bottom=500, Left=300, Right=700.<br><br>Do Canto superior esquerdo (300.250), recorte usando o espaço de preenchimento de (4000-300-700, 3000-250-500 ou 3000.2250). |
| Corte inteligente | Recorte de imagens em massa com base em seu ponto focal visual. | O Recorte inteligente usa o poder da inteligência artificial no Adobe Sensei para automatizar rapidamente o recorte de imagens em massa. O Corte inteligente detecta automaticamente e recorta até o ponto focal em qualquer imagem para capturar o ponto de interesse desejado, independentemente do tamanho da tela.</p> <p>Para usar o Recorte inteligente, selecione **[!UICONTROL Recorte inteligente]** na lista suspensa Opções de recorte, à direita de Recorte responsivo de imagem, habilite (ative) o recurso.</p> <p>Os tamanhos padrão de pontos de interrupção de Grande, Medium e Pequeno geralmente cobrem a gama completa de tamanhos que a maioria das imagens é usada em dispositivos móveis e tablets, desktops e banners. Se desejar, você pode editar os nomes padrão Grande, Medium e Pequeno.</p> <p>Para adicionar mais pontos de interrupção, selecione **[!UICONTROL Adicionar corte]** para excluir um corte, selecione o ícone Lixeira. |
| Amostra de cor e imagem | O gera uma amostra de imagem em massa para cada imagem. | **Observação**: a amostra inteligente não é suportada no Dynamic Media Classic.<br><br>Localize e gere automaticamente amostras de alta qualidade a partir de imagens de produtos que mostram cor ou textura.<br><br>Para usar a Amostra de Cor e Imagem, selecione **[!UICONTROL Recorte Inteligente]** na lista suspensa Opções de Recorte e, à direita de Amostra de Cor e Imagem, habilite (ative) o recurso. Insira um valor de pixel nas caixas de texto Largura e Altura.<br><br>Embora todos os recortes de imagem estejam disponíveis no painel Representações, as amostras são usadas somente por meio do recurso Copiar URL. Use seu próprio componente de visualização para renderizar a amostra em seu site. (A exceção a essa regra são os banners do carrossel. O Dynamic Media fornece o componente de visualização para a amostra usada nos banners do carrossel.)<br><br>**Usando amostras de imagem**<br> A URL para amostras de imagem é simples. É:<br><br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>onde `:Swatch` é anexado à solicitação de ativo.<br><br>**Usando amostras de cores**<br> Para usar amostras de cores, você faz uma solicitação `req=userdata` com o seguinte:<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>Por exemplo, este é um ativo de amostra no Dynamic Media Classic:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>e aqui está a URL `req=userdata` correspondente do ativo de amostra:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br><br>A resposta do `req=userdata` é a seguinte:<br>`SmartCropDef=Swatch SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br><br>Você também pode solicitar uma resposta do `req=userdata` no formato XML ou JSON, como nos seguintes exemplos de URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**Observação:** Crie seu próprio componente WCM para solicitar uma amostra de cores e analisar o atributo `SmartSwatchColor`, representado por um Valor hexadecimal RGB de 24 bits.<br><br>Consulte também [`userdata` no Guia de Referência de Visualizadores](https://experienceleague.adobe.com/pt-br/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata). |

## Tirar nitidez da máscara {#unsharp-mask}

Use a **[!UICONTROL Tirar nitidez da máscara]** para ajustar um efeito de filtro de nitidez na imagem final com resolução reduzida. É possível controlar a intensidade do efeito, o raio do efeito (medido em pixels) e um limite de contraste que é ignorado. Esse efeito usa as mesmas opções do filtro *Tirar nitidez da máscara* do Adobe Photoshop.

>[!NOTE]
>
>A máscara de nitidez só é aplicada a representações em menor escala no PTIFF (tiff de pirâmide) com uma resolução reduzida de mais de 50%. Isso significa que as representações de maior tamanho dentro do ptiff não são afetadas pela máscara não nítida, enquanto representações de menor tamanho, como miniaturas, são alteradas (e mostram a máscara não nítida).

Em **[!UICONTROL Tirar nitidez da máscara]**, você tem as seguintes opções de filtro:

| Opção | Descrição |
| --- | --- |
| Quantidade | Controla a quantidade de contraste aplicada aos pixels de borda. O padrão é 1,75. Para imagens de alta resolução, é possível aumentá-las para até 5. Pense na Quantidade como uma medida da intensidade do filtro. O intervalo é de 0 a 5. |
| Raio | Determina o número de pixels em torno dos pixels da borda que afetam a nitidez. Para imagens de alta resolução, insira de 1 a 2. Um valor baixo aplica nitidez apenas aos pixels da borda; um valor alto aplica nitidez a uma faixa mais ampla de pixels. O valor correto depende do tamanho da imagem. O valor padrão é 0,2. O intervalo é de 0 a 250. |
| Limite | Determina o intervalo de contraste que deve ser ignorado quando o filtro Tirar nitidez da máscara é aplicado. Em outras palavras, essa opção determina o quão diferentes os pixels com nitidez devem ser da área ao redor antes de serem considerados pixels de borda e de serem nitidez. Para evitar a introdução de ruídos, experimente valores entre 0 e 255. |

A nitidez está descrita em [Nitidez de imagens](/help/assets/assets/sharpening_images.pdf).

## Criar perfis de imagem do Dynamic Media {#creating-image-profiles}

Para definir parâmetros de processamento avançado para outros tipos de ativos, consulte [Configuração do processamento de ativos](config-dms7.md#configuring-asset-processing).

Consulte [Perfis para processamento de metadados, imagens e vídeos](processing-profiles.md).

Consulte também [Práticas recomendadas para organizar sua Assets digital para usar Perfis de processamento](/help/assets/organize-assets.md).

**Para criar Perfis de Imagem Dynamic Media:**

1. Selecione o logotipo do Adobe Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de imagem]**.
1. Selecione **[!UICONTROL Criar]** para adicionar um Perfil de Imagem.
1. Insira um nome de perfil e valores para Tirar nitidez da máscara, do recorte ou da amostra, ou ambos.

   Use um nome de perfil específico para a finalidade pretendida. Por exemplo, se você quiser criar um perfil que gere apenas amostras, ou seja, o Recorte inteligente está desativado (desativado) e a Amostra de cor e imagem está ativada (ativada), use o nome de perfil &quot;Amostras inteligentes&quot;.

   Consulte também [Opções de recorte inteligente e amostra inteligente](#crop-options) e [Tirar nitidez da máscara](#unsharp-mask).

   ![cortar](assets/crop.png)

1. Selecione **[!UICONTROL Salvar]**. O perfil recém-criado aparece na lista de perfis disponíveis.

## Editar ou excluir perfis de imagem do Dynamic Media {#editing-or-deleting-image-profiles}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de imagem]**.
1. Selecione o Perfil de imagem que deseja editar ou remover. Para editá-lo, selecione **[!UICONTROL Editar Perfil de Imagem]**. Para removê-lo, selecione **[!UICONTROL Excluir Perfil de Imagem]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Se estiver editando, salve as alterações. Se estiver excluindo, confirme se deseja remover o perfil.

## Aplicar um perfil de imagem do Dynamic Media a pastas {#applying-an-image-profile-to-folders}

Quando você atribui um Perfil de imagem a uma pasta, todas as subpastas herdam automaticamente o perfil da pasta principal. Esse fluxo de trabalho significa que você pode atribuir apenas um Perfil de imagem a uma pasta. Dessa forma, considere cuidadosamente a estrutura de pastas de onde você faz upload, armazena, usa e arquiva ativos.

Se você atribuiu um Perfil de imagem diferente a uma pasta, o novo perfil substituirá o perfil anterior. Os ativos de pasta existentes anteriormente permanecem inalterados. O novo perfil é aplicado aos ativos que são adicionados à pasta posteriormente.

As pastas que têm um perfil atribuído a elas são indicadas na interface do usuário usando o nome do perfil exibido no cartão.

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Aplique Perfis de imagem a pastas específicas ou globalmente a todos os ativos.

É possível reprocessar ativos em uma pasta que já tenha um Perfil de imagem existente que você alterou posteriormente. Consulte [Reprocessar ativos em uma pasta depois de editar seu perfil de processamento](processing-profiles.md#reprocessing-assets).

### Aplicar perfis de imagem do Dynamic Media a pastas específicas {#applying-image-profiles-to-specific-folders}

Aplique um Perfil de Imagem a uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades]**. Esta seção descreve como aplicar Perfis de imagem a pastas de ambas as maneiras.

As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você alterou posteriormente. Consulte [Reprocessar ativos em uma pasta depois de editar seu perfil de processamento](processing-profiles.md#reprocessing-assets).

#### Aplicar Perfis de imagem do Dynamic Media a pastas da interface do usuário Perfis {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de imagem]**.
1. Selecione o Perfil de imagem que deseja aplicar a uma ou várias pastas.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Selecione **[!UICONTROL Aplicar perfil de processamento às pastas]** e selecione uma ou várias pastas que deseja usar para receber os ativos carregados recentemente e selecione **[!UICONTROL Aplicar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

#### Aplicar perfis de imagem do Dynamic Media a pastas de propriedades {#applying-image-profiles-to-folders-from-properties}

1. Selecione o logotipo do Experience League e navegue até **[!UICONTROL Assets]**. Em seguida, navegue até a pasta principal da pasta à qual deseja aplicar um Perfil de imagem.
1. Na pasta, marque a marca de seleção para selecioná-la e selecione **[!UICONTROL Propriedades]**.
1. Selecione a guia **[!UICONTROL Perfis de imagem]**. Na lista suspensa **[!UICONTROL Nome do Perfil]**, selecione o perfil e **[!UICONTROL Salvar e Fechar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Aplicar um perfil de imagem do Dynamic Media globalmente {#applying-an-image-profile-globally}

Além de aplicar um perfil a uma pasta, você também pode aplicar um globalmente, de modo que qualquer conteúdo carregado nos ativos Experience Manager em qualquer pasta tenha o perfil selecionado aplicado.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você alterou posteriormente. Consulte [Reprocessando ativos em uma pasta após editar seu perfil de processamento](processing-profiles.md#reprocessing-assets).

**Para aplicar um Perfil de Imagem Dynamic Media globalmente:**

1. Siga uma das seguintes opções:

   * Navegue até `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam`, aplique o perfil apropriado e selecione **[!UICONTROL Salvar]**.

     ![chlimage_1-257](assets/chlimage_1-257.png)

   * Navegue até o CRXDE Lite para o seguinte nó: `/content/dam/jcr:content`.

     Adicione a propriedade `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` e selecione **[!UICONTROL Salvar tudo]**.

     ![configurar_perfis_de_imagem](assets/configure_image_profiles.png)

## Editar o recorte inteligente ou a amostra inteligente de uma única imagem {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
>
>* O recorte inteligente está disponível somente no modo Dynamic Media - Scene7.

Você pode realinhar ou redimensionar manualmente a janela de recorte inteligente de uma imagem para refinar ainda mais seu ponto focal.

Depois de editar um recorte inteligente e salvar, a alteração é propagada em todos os lugares em que você usa o recorte para as imagens específicas.

Execute novamente o corte inteligente para gerar os cortes adicionais novamente, se necessário.

Consulte também [Editar o recorte inteligente ou a amostra inteligente de várias imagens](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Para editar o recorte inteligente ou a amostra inteligente de uma única imagem:**

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Assets]**, em seguida, acesse a pasta que tem um Perfil de Imagem de recorte inteligente ou amostra inteligente aplicado a ela.
1. Selecione a pasta para poder abrir seu conteúdo.
1. Selecione a imagem cujo corte inteligente ou amostra inteligente você deseja ajustar.
1. Na barra de ferramentas, selecione **[!UICONTROL Recorte inteligente]**.

   >[!TIP]
   >
   >Use a tecla de atalho `s` para editar os recortes inteligentes ou as amostras inteligentes.

1. Siga um destes procedimentos:

   * Próximo ao canto superior direito da página, arraste a barra deslizante para a esquerda ou direita para aumentar ou diminuir a exibição da imagem, respectivamente.
   * Na imagem, arraste uma alça de canto para ajustar o tamanho da área visível do corte ou da amostra.
   * Na imagem, arraste a caixa/amostra para um novo local. Só é possível editar amostras de imagens; as amostras de cores são estáticas.
   * Acima da imagem, selecione **[!UICONTROL Reverter]** para desfazer todas as edições e restaurar o recorte ou a amostra original.

1. Próximo ao canto superior direito da página, selecione **[!UICONTROL Salvar]** e **[!UICONTROL Fechar]** para retornar à pasta de ativos.

## Editar o recorte inteligente ou a amostra inteligente de várias imagens {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
>
>* O recorte inteligente está disponível somente no modo Dynamic Media - Scene7.

Depois de aplicar um Perfil de imagem - contendo Recorte inteligente - a uma pasta, todas as imagens nessa pasta têm um recorte aplicado a elas. Se desejar, você pode *realinhar manualmente* ou redimensionar a janela de recorte inteligente em várias imagens para refinar ainda mais seu ponto focal.

Depois de editar um recorte inteligente e salvar, a alteração é propagada em todos os lugares em que você usa o recorte para as imagens específicas.

Execute novamente o corte inteligente para gerar os cortes adicionais novamente, se necessário.

**Para editar o recorte inteligente ou a amostra inteligente de várias imagens:**

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Assets]**, em seguida, acesse uma pasta que tenha um Perfil de Imagem de recorte inteligente ou amostra inteligente aplicado a ela.
1. Na pasta, selecione o ícone **[!UICONTROL Mais Ações]** (...) e selecione **[!UICONTROL Recorte Inteligente]**.

1. Na página **[!UICONTROL Editar cortes inteligentes]**, siga um destes procedimentos:

   * Ajuste o tamanho de exibição das imagens na página.

     À direita da lista suspensa de nomes dos pontos de interrupção, arraste a barra deslizante para a esquerda ou direita para alterar o tamanho da exibição da imagem visível.

     ![barra de controle deslizante de edit_smart_crop](assets/edit_smart_crops-sliderbar.png)

   * Filtrar a lista de imagens visualizáveis com base nos nomes dos pontos de interrupção. No exemplo abaixo, as imagens são filtradas no nome do ponto de interrupção &quot;Medium&quot;.

     Próximo ao canto superior direito da página, na lista suspensa, selecione um nome de ponto de interrupção para filtrar em quais imagens você vê. (Veja a imagem acima.)

     ![edit_smart_crop-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * Redimensionar a caixa de corte inteligente. Siga um destes procedimentos:

      * Se a imagem tiver apenas um recorte inteligente ou uma amostra inteligente, arraste a alça do canto da caixa de recorte para ajustar o tamanho da área visível do recorte.
      * Se a imagem tiver um corte inteligente e uma amostra inteligente, arraste a alça do canto da caixa de corte para ajustar o tamanho da área visível do corte. Ou selecione a amostra inteligente abaixo da imagem (as amostras de cores são estáticas) e arraste a alça do canto da caixa de recorte para ajustar o tamanho da área visível da amostra.

     ![Redimensionar o recorte inteligente de uma imagem](assets/edit_smart_crops-resize.png)

   * Mova a caixa de corte inteligente. Siga um destes procedimentos:

      * Se a imagem tiver apenas um recorte inteligente ou uma amostra inteligente, arraste a caixa de recorte para um novo local na imagem.
      * Se a imagem tiver um recorte inteligente e uma amostra inteligente, arraste a caixa de recorte inteligente para um novo local na imagem. Ou selecione a amostra inteligente abaixo da imagem (as amostras de cores são estáticas) e arraste a caixa de recorte da amostra inteligente para um novo local.

     ![editar_cortes_inteligentes-mover](assets/edit_smart_crops-move.png)

   * Desfazer todas as edições e restaurar o recorte inteligente original ou a amostra inteligente (aplica-se somente à sessão de edição atual).

     Selecione **[!UICONTROL Reverter]** acima da imagem.

     ![editar_cortes_inteligentes-reverter](assets/edit_smart_crops-revert.png)

1. Próximo ao canto superior direito da página, selecione **[!UICONTROL Salvar]** e **[!UICONTROL Fechar]** para retornar à pasta de ativos.

## Remover um perfil de imagem do Dynamic Media das pastas {#removing-an-image-profile-from-folders}

Ao remover um Perfil de imagem de uma pasta, todas as subpastas herdam automaticamente a remoção do perfil da pasta principal. No entanto, qualquer processamento de arquivos que tenha ocorrido nas pastas permanece intacto.

Remova um Perfil de Imagem de uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades]**. Esta seção descreve como remover Perfis de imagem de pastas de ambas as maneiras.

### Remover perfis de imagem do Dynamic Media de pastas por meio da interface do usuário Perfis {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de imagem]**.
1. Selecione o Perfil de imagem que deseja remover de uma ou várias pastas.
1. Selecione **[!UICONTROL Remover Perfil de Processamento das Pastas]**, selecione uma ou várias pastas que deseja usar para remover o perfil e selecione **[!UICONTROL Remover]**.

   É possível confirmar que o Perfil de imagem não é mais aplicado a uma pasta porque o nome não aparece mais abaixo do nome da pasta.

### Remova Perfis de imagem do Dynamic Media das pastas por meio de Propriedades {#removing-image-profiles-from-folders-via-properties}

1. Selecione o logotipo do Experience Manager, navegue até **[!UICONTROL Assets]** e, em seguida, acesse a pasta da qual deseja remover um Perfil de Imagem.
1. Na pasta, marque a marca de seleção para selecioná-la e selecione **[!UICONTROL Propriedades]**.
1. Selecione a guia **[!UICONTROL Perfis de imagem]**.
1. Na lista suspensa **[!UICONTROL Nome do Perfil]**, selecione **[!UICONTROL Nenhum]** e **[!UICONTROL Salvar e Fechar]**.

   As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.
