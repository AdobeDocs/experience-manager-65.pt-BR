---
title: Modelos de ativos
description: Saiba mais sobre os modelos de ativos no [!DNL Adobe Experience Manager Assets]  e como usá-los para criar materiais de suporte de marketing.
contentOwner: AG
role: User
feature: Asset Management,Developer Tools
exl-id: 12c92aad-3a1d-486e-a830-31de2fc6d07b
solution: Experience Manager, Experience Manager Assets
source-git-commit: 0b90fdd13efc5408ef94ee1966f04a80810b515e
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 0%

---

# Modelos de ativos {#asset-templates}

Os modelos de ativos são uma classe especial de ativos que facilitam a redefinição rápida de objetivos de conteúdo visualmente avançado para mídia digital e impressa. Um modelo de ativo inclui duas partes, a seção de mensagens fixas e a seção editável. A seção de mensagem fixa pode conter conteúdo proprietário, como logotipo da marca e informações de copyright que estão desativadas para edição. A seção editável pode conter conteúdo visual e textual em campos que podem ser editados para personalizar as mensagens.

Os modelos de ativos oferecem a flexibilidade de fazer edições limitadas, mantendo a sinalização global segura. Essa capacidade os torna os blocos fundamentais ideais para adaptar e distribuir rapidamente o conteúdo em várias funções. A redefinição de objetivos do conteúdo ajuda a reduzir o custo de gerenciamento de canais impressos e digitais e a fornecer experiências holísticas e consistentes nesses canais.

Como profissional de marketing, você pode armazenar e gerenciar modelos no [!DNL Experience Manager Assets] e usar um único modelo base para criar várias experiências de impressão personalizadas com facilidade. Você pode criar vários tipos de material de apoio de marketing, incluindo folhetos, panfletos, cartões postais, cartões de visita e assim por diante, para transmitir sua mensagem de marketing com lucidez aos clientes. Você também pode reunir saídas de impressão de várias páginas a partir de saídas de impressão existentes ou novas. Acima de tudo, você pode oferecer simultaneamente experiências digitais e de impressão com facilidade para fornecer uma experiência consistente e integrada para os usuários.

Embora os modelos de ativos sejam, em sua maioria, arquivos [!DNL Adobe InDesign], a proficiência em [!DNL Adobe InDesign] não é uma barreira à criação de artefatos estelares. Você não precisa mapear os campos do seu modelo do [!DNL Adobe InDesign] com os campos de produto que seriam necessários ao criar catálogos. É possível editar os modelos no modo WYSIWYG diretamente na interface da Web. No entanto, para que o [!DNL Adobe InDesign] processe suas alterações de edição, primeiro você deve configurar o [!DNL Experience Manager Assets] para integrar-se com o [!DNL Adobe InDesign Server].

A capacidade de editar modelos do [!DNL Adobe InDesign] na interface da Web ajuda a promover maior colaboração entre a equipe criativa e de marketing. O aumento da velocidade do conteúdo reduz o tempo de entrada no mercado de materiais de apoio de marketing.

É possível obter os seguintes resultados com modelos de ativos:

* Modifique campos de modelo editáveis na interface da Web.
* Controle o estilo básico do texto, por exemplo, tamanho da fonte, estilo e tipo no nível da tag.
* Altere imagens no modelo usando o Seletor de conteúdo.
* Visualizar edições de modelo.
* Mesclar vários arquivos de modelo para criar um artefato de várias páginas.

Quando você escolhe um modelo para o material de apoio, o [!DNL Experience Manager Assets] cria uma cópia do modelo que você pode editar. O modelo original é preservado, o que garante que sua sinalização global permaneça intacta e possa ser reutilizada para impor a consistência da marca.

É possível exportar o arquivo atualizado na pasta pai nos formatos INDD, PDF ou JPG. Você também pode baixar a saída nesses formatos para o sistema de arquivos local.

## Criar uma peça colateral {#creating-a-collateral}

Considere um cenário em que você deseja criar materiais de apoio digitais imprimíveis, como folhetos, folhetos e anúncios para uma campanha futura e compartilhe com lojas de pontos de venda em todo o mundo. A criação de material de apoio com base em um modelo ajuda a fornecer uma experiência unificada ao cliente em todos os canais. Os designers podem criar os modelos de campanha (página única ou várias páginas) usando uma solução criativa, como o [!DNL InDesign], e carregá-los no [!DNL Experience Manager Assets] para você. Antes de criar uma peça colateral, faça upload de um ou mais modelos INDD para o e disponibilize-os antecipadamente em [!DNL Experience Manager].

1. Na interface [!DNL Experience Manager], selecione [!UICONTROL Assets].

1. Nas opções, escolha **[!UICONTROL Modelos]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. Selecione **[!UICONTROL Criar]** e escolha o material de apoio que deseja criar no menu. Por exemplo, escolha **[!UICONTROL Folheto]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. Tenha um ou mais modelos INDD carregados e disponíveis em [!DNL Experience Manager] antecipadamente. Escolha um modelo para o folheto e clique em **[!UICONTROL Avançar]**.
1. Especifique um nome e uma descrição opcional para o folheto.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (Opcional) Clique em **[!UICONTROL Marcas]** e selecione uma ou mais marcas para o folheto. Clique em **[!UICONTROL Confirmar]** para confirmar a seleção.
1. Clique em **[!UICONTROL Criar]**. Uma caixa de diálogo confirma que um novo folheto é criado. Clique em **[!UICONTROL Abrir]** para abrir o folheto no modo de edição.

   <!--![chlimage_1-106](assets/.png) -->

   Como alternativa, feche a caixa de diálogo e navegue até a pasta na página Modelos que você começou com para exibir o folheto criado. O tipo do material adicional aparece em sua miniatura na exibição de cartão. Por exemplo, neste caso, a palavra [!UICONTROL Folheto] é exibida na miniatura.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## Editar uma peça de material de apoio {#editing-a-collateral}

Você pode editar um material de apoio imediatamente após criá-lo. Como alternativa, você pode abri-lo a partir da página [!UICONTROL Modelos] ou da página Ativo.

1. Para abrir o material de apoio para edição, siga um destes procedimentos:

   * Abra o material de apoio (folheto neste caso) que você criou na etapa 7 de [Criar um material de apoio](/help/assets/asset-templates.md#creating-a-collateral).
   * Na página Modelos, navegue até a pasta onde você criou o material de apoio e clique na ação rápida [!UICONTROL Editar] na miniatura de um material de apoio.
   * Na página de ativos do material de apoio, clique em **[!UICONTROL Editar]** na barra de ferramentas.
   * Selecione o material de apoio e clique em **[!UICONTROL Editar]** na barra de ferramentas.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   O localizador de ativos e o editor de texto são exibidos à esquerda da página. O editor de texto é aberto por padrão.

   Use o editor de texto para modificar o texto que deseja exibir no campo de texto. É possível modificar o tamanho, o estilo, a cor e o tipo da fonte no nível da tag.

   Para usar o localizador de ativos, você pode procurar ou pesquisar imagens no [!DNL Experience Manager Assets] e substituir as imagens editáveis no modelo por imagens de sua escolha.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   As imagens editáveis são exibidas à direita. Para que um campo seja editável em [!DNL Experience Manager Assets], o campo correspondente no modelo deve ser marcado em [!DNL InDesign]. Em outras palavras, eles devem ser marcados como editáveis em [!DNL InDesign].

   >[!NOTE]
   >
   >Integre sua implantação do [!DNL Experience Manager] com um [!DNL InDesign Server] para que o [!DNL Experience Manager Assets] possa extrair dados do modelo [!DNL InDesign] e disponibilizá-los para edição. Para obter detalhes, consulte [Integrar o Experience Manager Assets com o InDesign Server](/help/assets/indesign.md).

1. Para modificar o texto em um campo editável, clique no campo de texto da lista de campos editáveis e edite o texto no campo.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   É possível editar as propriedades do texto, por exemplo, estilo da fonte, cor e tamanho, usando as opções fornecidas.

1. Selecione **[!UICONTROL Visualizar]** para poder visualizar as alterações de texto.

1. Para trocar uma imagem, selecione o **[!UICONTROL Localizador de Ativos]** ![chlimage_1-113](assets/chlimage_1-318.png).

1. Selecione o campo de imagem na lista de campos editáveis e arraste uma imagem desejada do seletor de ativos para o campo editável.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   Também é possível pesquisar imagens usando palavras-chave, tags e com base no status de publicação. Você pode navegar pelo repositório [!DNL Experience Manager Assets] e navegar até o local da imagem desejada.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. Selecione **[!UICONTROL Visualizar]** para poder visualizar a imagem.
1. Para editar uma página específica em um material de apoio de várias páginas, use o navegador de página na parte inferior.

1. Selecione **[!UICONTROL Visualizar]** na barra de ferramentas para que você possa visualizar todas as alterações. Selecione **[!UICONTROL Concluído]** para salvar as alterações de edição no material de apoio.

   >[!NOTE]
   >
   >As opções Visualizar e Concluído são ativadas somente quando os campos de imagem editáveis no material de apoio não têm ícones ausentes. Se houver ícones ausentes em seu material de apoio, é porque [!DNL Experience Manager] não pode resolver as imagens no modelo [!DNL InDesign]. Normalmente, [!DNL Experience Manager] não consegue resolver imagens nos seguintes casos:
   >
   >* As imagens não estão inseridas no modelo [!DNL InDesign] subjacente.
   >* As imagens são vinculadas a partir do sistema de arquivos local.
   >
   >Para habilitar [!DNL Experience Manager] para resolver imagens, faça o seguinte:
   >
   >* Inserir imagens ao criar modelos [!DNL InDesign] (Consulte [Sobre links e elementos gráficos inseridos](https://helpx.adobe.com/br/indesign/using/graphics-links.html)).
   >* Monte o [!DNL Experience Manager] no seu sistema de arquivos local e mapeie os ícones ausentes com os ativos existentes no [!DNL Experience Manager].
   >

1. Para gerar uma representação PDF para o folheto, selecione a opção Acrobat na caixa de diálogo e clique em **[!UICONTROL Continuar]**.
1. O material de apoio é criado na pasta em que você começou. Para exibir as representações, abra o material de apoio e escolha **[!UICONTROL Representações]** na lista GlobalNav.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. Selecione a representação do PDF na lista de representações para baixar o arquivo do PDF. Abra o arquivo PDF para revisar o material de apoio.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Mesclar material de apoio {#merge-collateral}

1. Na interface [!DNL Experience Manager], selecione [!UICONTROL Assets] na página Navegação.

1. Nas opções, selecione **[!UICONTROL Modelos]**.

1. Selecione **[!UICONTROL Criar]** e, no menu, selecione **[!UICONTROL Mesclar]**.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. Na página [!UICONTROL Mesclagem de modelos], selecione **[!UICONTROL Mesclar]** ![adicionar ativos](assets/do-not-localize/assets_add_icon.png).

1. Navegue até o local do material de apoio que deseja intercalar, selecione as miniaturas do material de apoio que deseja intercalar para selecioná-los.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   Você também pode pesquisar modelos na caixa Omnisearch.

   Você pode navegar pelo repositório ou pelas coleções [!DNL Experience Manager Assets], navegar até o local dos modelos desejados e selecioná-los para mesclagem.

   É possível aplicar vários filtros para pesquisar os modelos desejados. Por exemplo, você pode pesquisar modelos com base no tipo de arquivo ou nas tags.

1. Selecione **[!UICONTROL Avançar]** na barra de ferramentas.
1. Na tela **[!UICONTROL Visualizar e reordenar]**, reorganize os modelos, se necessário, e visualize a seleção de modelos a serem mesclados. Na barra de ferramentas, selecione **[!UICONTROL Próximo]**.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. Na tela [!UICONTROL Configurar Modelo], especifique um nome para o material de apoio. Como opção, especifique as tags que você considerar apropriadas. Para exportar a saída no formato PDF, selecione **[!UICONTROL Acrobat (.PDF)]**. Por padrão, a garantia é exportada no formato JPG e [!DNL InDesign]. Para alterar a miniatura de exibição do material de apoio de várias páginas, clique em **[!UICONTROL Alterar Miniatura]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. Selecione **[!UICONTROL Salvar]** e feche a caixa de diálogo selecionando **[!UICONTROL OK]**. O material de apoio de várias páginas é criado na pasta em que você começou.

   >[!NOTE]
   >
   >Não é possível editar um material de apoio mesclado posteriormente ou usá-lo para criar outro material de apoio.

## Práticas recomendadas e limitações {#best-practices-limitations-tips}

* O editor [!DNL InDesign] no [!DNL Experience Manager] funciona em nível de marca e todo o texto sob uma única marca é considerado uma única entidade. Para preservar a formatação e os estilos de texto ao editar, marque separadamente cada parágrafo (ou texto com um estilo diferente).
