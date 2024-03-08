---
title: Gerenciamento de predefinições da imagem do Dynamic Media
description: Entenda as predefinições de imagem do Dynamic Media e saiba como criar, modificar e gerenciar predefinições de imagem.
mini-toc-levels: 3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/image-presets
feature: Image Presets
role: User, Admin
exl-id: 556b99fe-91c3-441f-ba81-22cb8c10ef7f
source-git-commit: db0e9d6105484b37e2e21e49bf0f95cef9da2a62
workflow-type: tm+mt
source-wordcount: '3792'
ht-degree: 7%

---

# Gerenciamento de predefinições da imagem do Dynamic Media{#managing-image-presets}

As Predefinições de imagem permitem que o Adobe Experience Manager Assets forneça imagens dinamicamente em diferentes tamanhos, formatos ou com outras propriedades de imagem geradas dinamicamente. Cada predefinição de imagem representa uma coleção predefinida de comandos de dimensionamento e formatação para a exibição de imagens. Ao criar uma Predefinição de imagem, você escolhe um tamanho para a entrega da imagem. Você também escolhe comandos de formatação para que a aparência da imagem seja otimizada quando ela for entregue para visualização.

Os administradores podem criar predefinições para exportar ativos. Os usuários podem escolher uma predefinição ao exportar imagens, o que também reformata imagens para as especificações especificadas pelo administrador.

Também é possível criar predefinições de imagens responsivas. Se você aplicar uma predefinição de imagem responsiva aos seus ativos, eles mudam dependendo do dispositivo ou tamanho da tela em que são exibidos. É possível configurar predefinições de imagens para usar CMYK no espaço de cores, além de RGB ou Cinza.

Esta seção descreve como criar, modificar e gerenciar predefinições de imagens. É possível aplicar uma predefinição de imagem a uma imagem sempre que ela for visualizada. Consulte [Aplicação de predefinições da imagem](/help/assets/image-presets.md).

>[!NOTE]
>
>A geração de imagens inteligentes funciona com suas predefinições de imagens existentes e usa inteligência nos últimos milissegundos do delivery para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador ou da conexão de rede. Consulte [Imagem inteligente](/help/assets/imaging-faq.md) para obter mais informações.

## Noções básicas sobre predefinições de imagem do Dynamic Media {#understanding-image-presets}

Como uma macro, uma Predefinição de imagem é uma coleção predefinida de comandos de dimensionamento e formatação salvos com um nome. Para entender como as Predefinições de imagem funcionam, suponha que seu site exija que cada imagem do produto seja exibida em tamanhos, formatos e taxas de compactação diferentes para entrega de desktops e dispositivos móveis.

>[!NOTE]
>
>No modo Dynamic Media - Scene7, as predefinições de imagens são compatíveis somente com ativos de imagem.

Você pode criar duas predefinições de imagem: uma com 500 x 500 pixels para a versão para desktop e 150 x 150 pixels para a versão móvel. Você cria duas Predefinições de imagem, uma chamada `Enlarge` para exibir imagens a 500x500 pixels e uma chamada `Thumbnail` para exibir imagens a 150 x 150 pixels. Para fornecer imagens no `Enlarge` e `Thumbnail` tamanho, o Experience Manager procurará a definição das predefinições Ampliar imagem e Imagem em miniatura. Em seguida, o Experience Manager gera dinamicamente uma imagem com as especificações de tamanho e formatação de cada Predefinição de imagem.

Imagens com tamanho reduzido quando entregues dinamicamente podem perder nitidez e detalhes. Por esse motivo, cada Predefinição de imagem contém controles de formatação para otimizar uma imagem quando ela é entregue em um tamanho específico. Esses controles garantem que suas imagens sejam nítidas e claras quando forem entregues ao seu site ou aplicativo.

Os administradores podem criar Predefinições de imagem. Para criar uma predefinição de imagem, inicie do zero ou inicie a partir de uma predefinição existente e salve-a com um novo nome.

## Gerenciamento de predefinições da imagem do Dynamic Media {#managing-image-presets-1}

Para gerenciar as predefinições de imagem no Experience Manager, toque ou clique no logotipo do Experience Manager para acessar o console de navegação global e, em seguida, toque ou clique no ícone Ferramentas e navegue até **[!UICONTROL Ativos > Predefinições de imagem]**.

![6_5_tools-assets-imagepresets](assets/6_5_tools-assets-imagepresets.png)

>[!NOTE]
>
>Todas as predefinições de imagens criadas também estão disponíveis como representações dinâmicas ao pré-visualizar ou fornecer ativos.
>
>Entrada *Dynamic Media - Modo Scene7*, você precisa *não* publicar predefinições de imagem, pois as predefinições de imagem são publicadas automaticamente.
>
>Entrada *Dynamic Media - Modo híbrido*, você deve publicar predefinições de imagem manualmente.
>
>Consulte [Publicar predefinições de imagem](#publishing-image-presets).

>[!NOTE]
>
>O sistema mostra várias representações ao selecionar **[!UICONTROL Representações]** na Exibição detalhada de um ativo. É possível aumentar ou diminuir o número de predefinições de imagens exibidas. Consulte [Aumentar o número de predefinições de imagens exibidas](#increasing-or-decreasing-the-number-of-image-presets-that-display).

### Recortes inteligentes, Adobe Illustrator (AI), Postscript (EPS) e formatos de arquivo PDF {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

>[!NOTE]
>
>Este tópico é aplicável somente ao Dynamic Media - Modo híbrido.

Se sua intenção for oferecer suporte à assimilação de arquivos AI, EPS e PDF para que você possa gerar representações dinâmicas desses formatos de arquivo, revise as informações a seguir antes de criar predefinições de imagem.

O formato de arquivo do Adobe Illustrator é uma variante do PDF. As principais diferenças, no contexto do Experience Manager Assets, são as seguintes:

* Os documentos do Adobe Illustrator consistem em uma única página com várias camadas. Cada camada é extraída como um subativo PNG no ativo principal do Illustrator.
* Os documentos PDF consistem em uma ou mais páginas. Cada página é extraída como um único subativo de PDF de página no documento principal de PDF de várias páginas.

Os subativos são criados pela variável `Create Sub Asset process` componente no âmbito do `DAM Update Asset` fluxo de trabalho. Para ver esse componente do processo no fluxo de trabalho, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]** > **[!UICONTROL Ativo de atualização DAM]** > **[!UICONTROL Editar]**.

Consulte também [Visualização de páginas de um arquivo de várias páginas](/help/assets/managing-linked-subassets.md#view-pages-of-a-multi-page-file).

É possível exibir os subativos ou as páginas ao abrir o ativo, selecionar o menu Conteúdo e selecionar **[!UICONTROL Subativos]** ou **[!UICONTROL Páginas]**. Os subativos são ativos reais. Ou seja, as páginas de PDF são extraídas pelo `Create Sub Asset` componente do fluxo de trabalho. Eles são armazenados como `page1.pdf`, `page2.pdf`e assim por diante, abaixo do ativo principal. Após serem armazenados, o `DAM Update Asset` fluxo de trabalho os processa.

Para usar o Dynamic Media para visualizar e gerar representações dinâmicas para arquivos AI, EPS ou PDF, as seguintes etapas de processamento são necessárias:

1. No `DAM Update Asset` workflow, a variável `Rasterize PDF/AI Image Preview Rendition` componente de processo rasteriza a primeira página do ativo original, usando a resolução configurada, em um `cqdam.preview.png` representação.

1. A variável `cqdam.preview.png` A representação é otimizada em um PTIFF pelo `Dynamic Media Process Image Assets` componente do processo no fluxo de trabalho.

>[!NOTE]
>
>No [!UICONTROL Ativo de atualização DAM] workflow, a variável **[!UICONTROL Miniaturas do EPS]** A etapa gera miniaturas para arquivos do EPS.

#### Propriedades de metadados de ativos do PDF/AI/EPS {#pdf-ai-eps-asset-metadata-properties}

| **Propriedade de metadados** | **Descrição** |
|---|---|
| `dam:Physicalwidthininches` | Largura do documento em polegadas. |
| `dam:Physicalheightininches` | Altura do documento em polegadas. |

Você acessa `Rasterize PDF/AI Image Preview Rendition` processar opções de componente por meio da `DAM Update Asset` fluxo de trabalho.

No canto superior esquerdo, selecione Adobe Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**. Na página Modelos de fluxo de trabalho, selecione **[!UICONTROL Ativo de atualização DAM]**, em seguida, selecione na barra de ferramentas **[!UICONTROL Editar]**. No [!UICONTROL Ativo de atualização DAM] fluxo de trabalho, selecione duas vezes a variável `Rasterize PDF/AI Image Preview Rendition` processar componente para abrir sua caixa de diálogo Propriedades da etapa.

#### Opções de Rasterizar representação da exibição de imagens do PDF/AI {#rasterize-pdf-ai-image-preview-rendition-options}

![Argumentos para rasterizar o fluxo de trabalho do PDF ou da IA](assets/rasterize_pdf_ai_image_preview.png)

Argumentos para rasterizar o fluxo de trabalho do PDF ou da IA

<table>
 <tbody>
  <tr>
   <td><strong>Argumento do processo</strong></td>
   <td><strong>Configuração padrão</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Tipos de mime</td>
   <td><p>application/pdf</p> <p>application/postscript</p> <p>application/illustrator<br /> </p> </td>
   <td>Lista de tipos MIME de documentos que são considerados documentos PDF ou Illustrator.<br /> </td>
  </tr>
  <tr>
   <td>Largura máxima</td>
   <td>2048</td>
   <td>Largura máxima da representação de visualização gerada, em pixels.<br /> </td>
  </tr>
  <tr>
   <td>Altura máxima</td>
   <td>2048</td>
   <td>Altura máxima da representação de visualização gerada, em pixels.<br /> </td>
  </tr>
  <tr>
   <td>Resolução</td>
   <td>72</td>
   <td>Resolução para rasterizar a primeira página, em ppi (pixels por polegada).</td>
  </tr>
 </tbody>
</table>

Usando os argumentos de processo padrão, a primeira página de um documento PDF/AI é rasterizada em 72 ppi e a imagem de visualização gerada é dimensionada em 2048 x 2048 pixels. Para uma implantação típica, convém aumentar a resolução para um mínimo de 150 ppi ou mais. Por exemplo, um documento tamanho carta EUA a 300 ppi requer no máximo 2550 x 3300 pixels de largura e altura, respectivamente.

Largura máxima e Altura máxima limitam a resolução na qual rasterizar. Por exemplo, se os máximos não forem alterados e a Resolução for definida como 300 ppi, um documento Carta dos EUA será rasterizado em 186 ppi. Ou seja, o documento tem 1581 x 2046 pixels.

A variável `Rasterize PDF/AI Image Preview Rendition` o componente do processo tem um máximo definido para garantir que não crie imagens muito grandes na memória. Essas imagens grandes podem estourar a memória fornecida para a JVM (Java™ Virtual Machine). É necessário tomar cuidado para fornecer à JVM memória suficiente para gerenciar o número configurado de workflows paralelos, com cada um tendo o potencial de criar uma imagem no tamanho máximo configurado.

### formato de arquivo InDesign (INDD) {#indesign-indd-file-format}

Se você pretende suportar a assimilação de arquivos INDD para gerar uma representação dinâmica desse formato de arquivo, convém revisar as informações a seguir antes de criar predefinições de imagem.

Para arquivos de InDesign, os sub-ativos são extraídos somente se o Adobe InDesign Server estiver integrado ao Experience Manager. Os ativos referenciados são vinculados com base em seus metadados. O InDesign Server não é necessário para vinculação. No entanto, os ativos referenciados devem estar presentes no Experience Manager antes que os arquivos de InDesign sejam processados para que os links sejam criados entre os arquivos de InDesign e os ativos referenciados.

Consulte [Integração do Experience Manager Assets com o InDesign Server](/help/assets/indesign.md).

O componente do processo de extração de mídia no `DAM Update Asset` O fluxo de trabalho do executa vários Scripts de extensão pré-configurados para processar arquivos InDesign.

![Os caminhos do ExtendScript nos argumentos do processo de extração de mídia](assets/6_5_mediaextractionprocess.png)

Os caminhos do ExtendScript nos argumentos do componente do processo de Extração de mídia na [!UICONTROL Ativo de atualização DAM] fluxo de trabalho.

Os seguintes scripts são usados pela integração do Dynamic Media:

<table>
 <tbody>
  <tr>
   <td><strong>Nome do ExtendScript</strong></td>
   <td><strong>Padrão</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>ThumbnailExport.jsx</td>
   <td>Sim</td>
   <td>Gera uma taxa de 300 ppi <code>thumbnail.jpg</code> que é otimizada e transformada em uma representação PTIFF pelo <code>Dynamic Media Process Image Assets</code> componente do processo.<br /> </td>
  </tr>
  <tr>
   <td>JPEGPagesExport.jsx</td>
   <td>Sim</td>
   <td>Gera um subativo de JPEG de 300 PPI para cada página. O subativo JPEG é um ativo real armazenado no ativo InDesign. Ele também é otimizado e transformado em um PTIFF pelo <code>DAM Update Asset</code> fluxo de trabalho.<br /> </td>
  </tr>
  <tr>
   <td>PDFPagesExport.jsx</td>
   <td>Não</td>
   <td>Gera um subativo PDF para cada página. O subativo PDF é processado conforme descrito anteriormente. Como o PDF contém apenas uma página, nenhum subativo é gerado.<br /> </td>
  </tr>
 </tbody>
</table>

## Configuração do tamanho da miniatura da imagem {#configuring-image-thumbnail-size}

Você pode definir o tamanho das miniaturas definindo essas configurações na **[!UICONTROL Ativo de atualização DAM]** fluxo de trabalho. Há duas etapas no fluxo de trabalho nas quais você pode configurar o tamanho da miniatura de ativos de imagem. Embora (**[!UICONTROL Ativos de imagem do processo Dynamic Media]**) é usada para ativos de imagem dinâmicos e (**[!UICONTROL Miniaturas do processo]**) é para geração de miniaturas estáticas ou quando todos os outros processos não conseguem gerar miniaturas, *ambos* deve ter as mesmas configurações.

Com a etapa **[!UICONTROL Ativos de imagem de processo do Dynamic Media]**, as miniaturas são geradas pelo servidor de imagem e essa configuração é independente da configuração aplicada à etapa **[!UICONTROL Processar miniaturas]**. Gerar miniaturas por meio da etapa **[!UICONTROL Processar miniaturas]** é a maneira mais lenta e intensiva de memória para criar miniaturas.

O dimensionamento de miniatura é definido no seguinte formato: **`width:height:center`**, por exemplo, `80:80:false`. A largura e a altura determinam o tamanho da miniatura em pixels. O valor central é falso ou true e, se definido como true, indica que a imagem em miniatura tem exatamente o tamanho fornecido na configuração. Se a imagem redimensionada for menor, ela será centralizada na miniatura.

>[!NOTE]
>
>* Os tamanhos de miniatura de arquivos do EPS são configurados no **[!UICONTROL Miniaturas do EPS]** etapa, na guia **[!UICONTROL Argumentos]** em Miniaturas.
>
>* Os tamanhos de miniatura de vídeos são configurados no **[!UICONTROL Miniaturas de FFmpeg]** etapa, na guia **[!UICONTROL Processo]** em **[!UICONTROL Argumentos]**.
>

**Para configurar o tamanho da miniatura da imagem:**

1. Selecionar **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]** > **[!UICONTROL Ativo de atualização DAM]** > **[!UICONTROL Editar]**.
1. Selecione o **[!UICONTROL Ativos de imagem do processo Dynamic Media]** e clique no botão **[!UICONTROL Miniaturas]** guia. Altere o tamanho da miniatura, conforme necessário, e selecione **[!UICONTROL OK]**.

   ![6_5_dynamicmediaprocessimageassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. Selecione o **[!UICONTROL Miniaturas do processo]** e, em seguida, selecione a **[!UICONTROL Miniaturas]** guia. Altere o tamanho da miniatura, conforme necessário, e selecione **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Os valores no argumento de miniaturas da etapa **[!UICONTROL Processar miniaturas]** devem corresponder ao argumento de miniaturas na etapa **[!UICONTROL Ativos de imagem do processo do Dynamic Media]**.

1. Selecionar **[!UICONTROL Salvar]** para salvar as alterações no workflow.

### Como aumentar ou diminuir o número de predefinições de imagens do Dynamic Media exibidas {#increasing-or-decreasing-the-number-of-image-presets-that-display}

As predefinições de imagem criadas estão disponíveis como representações dinâmicas ao visualizar ativos. O Experience Manager mostra várias representações dinâmicas ao visualizar um ativo do **[!UICONTROL Exibição detalhada > Representações]**. É possível aumentar ou diminuir o limite de representações exibidas.

**Aumente ou diminua o número de predefinições de imagens do Dynamic Media exibidas:**

1. Navegue até CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Navegue até o nó da listagem de predefinições de imagens em `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`

   ![aumentar_diminuir_enumerarnofimapredefiniçõesque exibem](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. Na propriedade **[!UICONTROL limit]**, altere o **[!UICONTROL Value]**, que é definido como 15 por padrão, para o número desejado.
1. Navegue até a fonte de dados da predefinição de imagem em `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. Na propriedade limit, altere o número para o número desejado, por exemplo, `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. Selecionar **[!UICONTROL Salvar tudo]**.

## Criação de uma predefinição de imagem do Dynamic Media {#creating-image-presets}

A criação de uma predefinição de imagem do Dynamic Media permite aplicar essas configurações a qualquer imagem ao pré-visualizar ou publicar.

>[!NOTE]
>
>Se estiver usando o Internet Explorer 9, a criação de uma predefinição não aparecerá na lista de predefinições imediatamente após salvar. Para contornar esse problema, desabilite o cache do IE9.

Se sua intenção for oferecer suporte à assimilação de arquivos AI, PDF e EPS para que você possa gerar a representação dinâmica desses formatos de arquivo, revise as informações a seguir antes de criar predefinições de imagem.
Consulte [Formatos de arquivo Adobe Illustrator (AI), Postscript (EPS) e PDF](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats).

Se você pretende suportar a assimilação de arquivos INDD para gerar uma representação dinâmica desse formato de arquivo, convém revisar as informações a seguir antes de criar predefinições de imagem.
Consulte [formato de arquivo InDesign (INDD)](#indesign-indd-file-format).

>[!NOTE]
>
>Para criar predefinições de imagens do Dynamic Media, é necessário ter privilégios de administrador como administrador de Experience Manager ou administrador de Admin Console.

**Para criar uma predefinição de imagem do Dynamic Media:**

1. Em Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global e, em seguida, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefinições da imagem]**.
1. Clique em **[!UICONTROL Criar]**. A variável **[!UICONTROL Editar predefinição de imagem]** é aberta.

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >Para tornar essa predefinição de imagem responsiva, apague os valores nos campos **[!UICONTROL largura]** e **[!UICONTROL altura]** e deixe-os em branco.

1. Insira valores nas guias **[!UICONTROL Básico]** e **[!UICONTROL Avançado]**, conforme apropriado, incluindo um nome. As opções são descritas em [Opções de predefinição de imagem](#image-preset-options). As predefinições aparecem no painel à esquerda e podem ser usadas junto com outros ativos.

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. Clique em **[!UICONTROL Salvar]**.

## Criação de uma predefinição de imagem responsiva {#creating-a-responsive-image-preset}

Para criar uma predefinição de imagem responsiva, execute as etapas em [Criação de predefinições de imagem](#creating-image-presets). Ao inserir a altura e a largura no **[!UICONTROL Editar predefinição de imagem]** apagar os valores e deixá-los em branco.

Deixá-los em branco informa ao Experience Manager que essa predefinição de imagem é responsiva. Você pode ajustar os outros valores conforme apropriado.



>[!NOTE]
>
>O ativo deve ser publicado para ver os botões **[!UICONTROL URL]** e **[!UICONTROL RESS]** ao aplicar uma predefinição de imagem a um ativo.
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>No modo Dynamic Media - Scene7, as predefinições de imagem e os ativos de imagem são publicados automaticamente.
>
>No modo Dynamic Media - Híbrido, você deve publicar manualmente as predefinições de imagem e os ativos de imagem.

### Opções de predefinição de imagem {#image-preset-options}

Ao criar ou editar predefinições de imagens, você tem as opções descritas nesta seção. Além disso, a Adobe recomenda que estas opções de &quot;práticas recomendadas&quot; comecem:

* **[!UICONTROL Formato]** (**[!UICONTROL Básico]** ) - Selecionar **[!UICONTROL JPEG]** ou outro formato que atenda aos seus requisitos. Todos os navegadores da Web são compatíveis com o formato de imagem JPEG; ele oferece um bom equilíbrio entre arquivos pequenos e qualidade de imagem. No entanto, as imagens no formato JPEG usam um esquema de compactação com perdas que pode apresentar artefatos de imagem indesejados se a configuração de compactação for muito baixa. Por esse motivo, a Adobe recomenda definir a qualidade de compactação como 75. Essa configuração oferece um bom equilíbrio entre a qualidade da imagem e o tamanho pequeno de arquivo.

* **[!UICONTROL Ativar nitidez simples]** - Não selecione **[!UICONTROL Ativar nitidez simples]** (este filtro de nitidez oferece menos controle do que as configurações Tirar nitidez da máscara).

* **[!UICONTROL Nitidez: Modo de Reamostragem]** - Selecionar **[!UICONTROL Sharp2]**.

#### Opções da guia Básico {#basic-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>Texto</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td><strong>Nome</strong></td>
   <td>Insira um nome descritivo sem espaços em branco. Inclua a especificação de tamanho da imagem no nome para que os usuários possam identificar essa Predefinição de imagem.</td>
  </tr>
  <tr>
   <td><strong>Largura e altura</strong></td>
   <td>Insira, em pixels, o tamanho da imagem. A largura e a altura devem ser maiores que 0 pixels. Se um dos valores for 0, nenhuma predefinição será criada. Se ambos os valores estiverem em branco, uma predefinição de imagem responsiva será criada.</td>
  </tr>
  <tr>
   <td><strong>Formato</strong></td>
   <td><p>Escolha um formato no menu.</p> <p>Escolhendo <strong>JPEG</strong> O oferece as seguintes opções adicionais:</p>
    <ul>
     <li><strong>Qualidade</strong> - Controla o nível de compressão JPEG. Essa configuração afeta o tamanho do arquivo e a qualidade da imagem. A escala de qualidade do JPEG é de 1 a 100. A escala fica visível quando você arrasta o controle deslizante.</li>
     <li><strong>Ativar redução de resolução de crominância de JPG</strong> - Como o olho é menos sensível a informações de cores de alta frequência do que a luminosidade de alta frequência, as imagens de JPEG dividem as informações da imagem em componentes de luminosidade e cor. Quando uma imagem de JPEG é compactada, o componente de luminosidade fica com a resolução total, enquanto os componentes de cor ficam com uma resolução mais baixa para calcular a média de grupos de pixels. A redução da resolução reduz o volume de dados pela metade ou em um terço com quase nenhum impacto na qualidade aparente. A redução da resolução não é aplicável a imagens em tons de cinza. Essa técnica reduz a quantidade de compactação útil para imagens com alto contraste (por exemplo, imagens com texto sobreposto).</li>
    </ul>
    <div>
      Escolhendo
     <strong>GIF</strong> ou
     <strong>GIF com alfa</strong> fornece esses recursos adicionais
     <strong>Quantização de cor do GIF</strong> opções:
    </div>
    <ul>
     <li><strong>Tipo </strong>- Selecionar <strong>Adaptável</strong> (o padrão), <strong>Web</strong>ou <strong>Macintosh</strong>. Se você selecionar <strong>GIF com Alpha</strong>, a opção Macintosh não está disponível.</li>
     <li><strong>Pontilhamento</strong> - Selecionar <strong>Difuso</strong> ou <strong>Desligado</strong>.</li>
     <li><strong>Número de cores </strong>- Insira um número de 2 a 256.</li>
     <li><strong>Lista de cores</strong> - Insira uma lista separada por vírgulas. Por exemplo, para branco, cinza e preto, insira <code>000000,888888,ffffff</code>.</li>
    </ul>
    <div>
      Escolhendo
     <strong>PDF</strong>,
     <strong>TIFF</strong>ou
     <strong>TIFF com alfa</strong> O fornece esta opção adicional:
    </div>
    <ul>
     <li><strong>Compactação</strong> - Selecione um algoritmo de compactação. As opções de algoritmo para PDF são <strong>Nenhum</strong>, <strong>Zip</strong>, e <strong>Jpeg</strong>; para o TIFF, as opções são <strong>Nenhum</strong>, <strong>LZW</strong>, <strong>Jpeg</strong>, e <strong>Zip</strong>; e para TIFF com Alpha são <strong>Nenhum</strong>, <strong>LZW</strong>, e <strong>Zip</strong>.</li>
    </ul> <p>Escolhendo <strong>PNG</strong>, <strong>PNG com Alpha,</strong> ou <strong>EPS</strong> O não fornece opções adicionais.</p> </td>
  </tr>
  <tr>
   <td><strong>Nitidez</strong></td>
   <td>Selecione o <strong>Ativar nitidez simples</strong> opção para aplicar um filtro de nitidez básico à imagem depois que todo o dimensionamento ocorrer. A nitidez pode ajudar a compensar o desfoque que pode ocorrer ao exibir uma imagem de tamanho diferente. </td>
  </tr>
 </tbody>
</table>

#### Opções da guia Avançadas {#advanced-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>Texto</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td><strong>Espaço de cor</strong></td>
   <td>Selecionar <strong>RGB, CMYK,</strong> ou <strong>Tons de cinza</strong> para o espaço de cores.</td>
  </tr>
  <tr>
   <td><strong>Perfil de cor</strong></td>
   <td>Selecione o perfil do espaço de cores de saída no qual o ativo deve ser convertido se for diferente do perfil de trabalho.</td>
  </tr>
  <tr>
   <td><strong>Renderizar recuo</strong></td>
   <td>Você pode substituir a tentativa de renderização padrão. As tentativas de renderização determinam o que acontece com as cores que não podem ser reproduzidas no perfil de cores de destino (fora do gamut). A intenção de renderização é ignorada se não for compatível com o perfil ICC.
    <ul>
     <li>Selecionar <strong>Perceptivo</strong> para compactar o gamut total de um espaço de cores em outro espaço de cores quando uma ou mais cores da imagem original estiverem fora do gamut do espaço de cores de destino.</li>
     <li>Selecionar <strong>Colorimétrico relativo</strong> quando uma cor no espaço de cores atual estiver fora do gamut no espaço de cores de destino. E, você deseja mapeá-lo para a cor mais próxima possível dentro do gamut do espaço de cores de destino, sem afetar outras cores. </li>
     <li>Selecionar <strong>Saturação</strong> se desejar reproduzir a saturação de cores da imagem original ao converter no espaço de cores de destino. </li>
     <li>Selecionar <strong>Colorimétrico absoluto</strong> para corresponder exatamente as cores sem nenhum ajuste para o ponto branco ou o ponto preto, o que alteraria o brilho da imagem.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Compensação de pontos pretos</strong></td>
   <td>Selecione essa opção se o perfil de saída suportar esse recurso. A compensação de Blackpoint é ignorada se não for compatível com o perfil ICC especificado.</td>
  </tr>
  <tr>
   <td><strong>Pontilhamento</strong></td>
   <td>Selecione essa opção para possivelmente evitar ou reduzir artefatos de banda de cores. </td>
  </tr>
  <tr>
   <td><strong>Tipo de nitidez</strong></td>
   <td><p>Selecionar <strong>Nenhum</strong>, <strong>Nitidez</strong>ou <strong>Tirar nitidez da máscara</strong>. </p>
    <ul>
     <li>Selecionar <strong>Nenhum</strong> se quiser desativar a nitidez.</li>
     <li>Selecionar <strong>Nitidez</strong> se quiser aplicar um filtro de nitidez básico à imagem depois que todo o dimensionamento ocorrer. A nitidez pode ajudar a compensar o desfoque que pode ocorrer ao exibir uma imagem de tamanho diferente. </li>
     <li>Selecionar<strong> Tirar nitidez da máscara</strong> se quiser ajustar um efeito de filtro de nitidez na imagem final com resolução reduzida. É possível controlar a intensidade do efeito, o raio do efeito (medido em pixels) e um limite de contraste que é ignorado. Esse efeito usa as mesmas opções do filtro "Tirar nitidez da máscara" do Photoshop.</li>
    </ul> <p>Entrada <strong>Tirar nitidez da máscara</strong>, você tem as seguintes opções:</p>
    <ul>
     <li><strong>Quantidade</strong> - Controla a quantidade de contraste aplicada aos pixels de borda. O valor padrão do número real é 1,0. Para imagens de alta resolução, é possível aumentá-las para até 5,0. Pense na Quantidade como uma medida da intensidade do filtro.</li>
     <li><strong>Raio</strong> - Determina o número de pixels em torno dos pixels da borda que afetam a nitidez. Para imagens de alta resolução, digite um número real de 1 a 2. Um valor baixo aplica nitidez apenas aos pixels da borda; um valor alto aplica nitidez a uma faixa mais ampla de pixels. O valor correto depende do tamanho da imagem.</li>
     <li><strong>Limite</strong> - Determina o intervalo de contraste que deve ser ignorado quando o filtro Tirar nitidez da máscara é aplicado. Em outras palavras, essa opção determina o quão diferentes os pixels com nitidez devem ser da área ao redor antes de serem considerados pixels de borda e de serem nitidez. Para evitar a introdução de ruídos, experimente valores inteiros de 2 a 20. </li>
     <li><strong>Aplicar a</strong> - Determina se a desnitidez se aplica a cada cor ou brilho.</li>
    </ul>
    <div>
      A nitidez é descrita em
     <a href="https://experienceleague.adobe.com/docs/experience-manager-65/assets/sharpening_images.pdf">Nitidez de imagens</a>.
    </div> </td>
  </tr>
  <tr>
   <td><strong>Modo de nova amostra</strong></td>
   <td>Selecione um <strong>Modo de reamostragem</strong> opção. Essas opções deixam a imagem mais nítida quando a resolução é reduzida:
    <ul>
     <li><strong>Bilinear</strong> - O método de reamostragem mais rápido. Alguns artefatos de suavização são visíveis.</li>
     <li><strong>Bi-Cúbico</strong> - Aumenta o uso da CPU, mas produz imagens mais nítidas com menos artefatos de suavização visíveis.</li>
     <li><strong>Sharp2</strong> - Pode produzir resultados ligeiramente mais nítidos do que o Bi-Cubic, mas com um custo de CPU ainda maior.</li>
     <li><strong>Bi-Sharp</strong> - Seleciona o reamostragem padrão do Photoshop para reduzir o tamanho da imagem, que é chamado de <strong>bicúbico mais nítido</strong> no Adobe Photoshop.</li>
     <li><strong>Cada cor</strong> e <strong>Brilho</strong> - cada método pode ser baseado na cor ou no brilho. Por padrão <strong>Cada cor</strong> está selecionada.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Resolução de impressão</strong></td>
   <td>Selecione uma resolução para imprimir esta imagem; o padrão é 72 pixels.</td>
  </tr>
  <tr>
   <td><strong>Modificador de imagem</strong></td>
   <td><p>Além das configurações comuns de imagem disponíveis na interface, o Dynamic Media oferece suporte a várias modificações avançadas de imagem que você pode especificar na <strong>Modificadores de imagem</strong> campo. Esses parâmetros são definidos na <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html#image-serving-api">Referência de comando do Protocolo do Servidor de Imagens</a>.</p> <p>Importante: a seguinte funcionalidade listada na API não é compatível:</p>
    <ul>
     <li>Modelos básicos e comandos de renderização de texto: <code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code> e <code>textPs=</code></li>
     <li>Comandos de localização: <code>locale=</code> e <code>req=xlate</code></li>
     <li><code>req=set</code> não está disponível para uso geral.</li>
     <li><code>req=mbrset</code></li>
     <li><code>req=saveToFile</code></li>
     <li><code>req=targets</code></li>
     <li><code>template=</code></li>
     <li>Serviços Dynamic Media não essenciais: SVG, renderização de imagem e Web-to-Print</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Definição de opções de predefinição de imagem com Modificadores de imagem {#defining-image-preset-options-with-image-modifiers}

Além das opções disponíveis nas guias Básico e Avançado, é possível definir modificadores de imagem para oferecer mais opções ao definir predefinições de imagens. A Renderização de imagem depende da API de renderização de imagem definida em detalhes na seção [Referência de protocolo HTTP](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html#image-serving-api).

A seguir estão alguns exemplos básicos do que você pode fazer com modificadores de imagem.

>[!NOTE]
>
>Alguns modificadores de imagem [não pode ser usado no Experience Manager](#advanced-tab-options).

* [op_invert](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-invert.html#image-serving-api) - Inverte cada componente de cor para obter um efeito de imagem negativo.

  ```xml
  &op_invert=1
  ```

  ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-blur.html#image-serving-api) - Aplica um filtro de desfoque à imagem.

  ```xml
  &op_blur=7
  ```

  ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* Comandos combinados - op_blur e op-invert

  ```xml
  &op_invert=1&op_blur=7
  ```

  ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_brightness](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-brightness.html#image-serving-api) - Diminui ou aumenta o brilho.

  ```xml
  &op_brightness=58
  ```

  ![6_5_imagepreset-edit-brightness](assets/6_5_imagepreset-edit-brightness.png)

* [opac](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-opac.html#image-serving-api) - Ajusta a opacidade da imagem. Permite diminuir a opacidade do primeiro plano.

  ```xml
  opac=29
  ```

  ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

## Edição de predefinições da imagem {#modifying-image-presets}

1. Em Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global e, em seguida, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefinições da imagem]**.

   ![6_5_imagepreset-editpreset](assets/6_5_imagepreset-editpreset.png)

1. Selecione uma predefinição e clique em **[!UICONTROL Editar]**. A variável **[!UICONTROL Editar predefinição de imagem]** é aberta.
1. Faça alterações e clique em **[!UICONTROL Salvar]** para salvar as alterações ou **[!UICONTROL Cancelar]** para cancelar as alterações.

## Publicação de predefinições de imagem do Dynamic Media {#publishing-image-presets}

Se você estiver executando o Dynamic Media - Modo híbrido, publique manualmente as predefinições da imagem.

(Se você estiver executando o modo Dynamic Media - Scene7, as predefinições de imagem são publicadas automaticamente para você; não é necessário concluir essas etapas.)

**Para publicar predefinições de imagem no Dynamic Media - modo híbrido:**

1. No Experience Manager, clique no logotipo do Experience Manager para acessar o console de navegação global, clique no ícone Ferramentas e navegue até **[!UICONTROL Assets]** > **[!UICONTROL Predefinições da imagem]**.
1. Selecione a predefinição de imagem ou várias predefinições de imagem na lista de predefinições de imagem e clique em **[!UICONTROL Publish]**.
1. Depois que a predefinição de imagem é publicada, o status muda de não publicado para publicado.

   ![chlimage_1-81](assets/chlimage_1-505.png)

## Exclusão de predefinições de imagem do Dynamic Media {#deleting-image-presets}

1. No Experience Manager, clique no logotipo Experience Manager para acessar o console de navegação global.
1. Selecione o **[!UICONTROL Ferramentas]** e navegue até **[!UICONTROL Assets]** > **[!UICONTROL Predefinições da imagem]**.
1. Selecione uma predefinição e clique em **[!UICONTROL Excluir]**. O Dynamic Media confirma que você deseja excluí-lo. Selecionar **[!UICONTROL Excluir]** para excluir ou selecionar **[!UICONTROL Cancelar]** para suspender.
