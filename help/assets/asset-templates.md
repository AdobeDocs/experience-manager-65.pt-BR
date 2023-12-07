---
title: Modelos de ativos
description: Saiba mais sobre modelos de ativos no [!DNL Adobe Experience Manager Assets] e como usar modelos de ativos para criar material de apoio de marketing.
contentOwner: AG
role: User
feature: Asset Management,Developer Tools
exl-id: 12c92aad-3a1d-486e-a830-31de2fc6d07b
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 0%

---

# Modelos de ativos {#asset-templates}

Os modelos de ativos são uma classe especial de ativos que facilitam a redefinição rápida da finalidade de conteúdo visualmente avançado para mídia digital e impressa. Um modelo de ativo inclui duas partes, a seção de mensagens fixas e a seção editável. A seção de mensagem fixa pode conter conteúdo proprietário, como logotipo da marca e informações de copyright que estão desativadas para edição. A seção editável pode conter conteúdo visual e textual em campos que podem ser editados para personalizar as mensagens.

A flexibilidade de fazer edições limitadas e, ao mesmo tempo, proteger a sinalização global torna os modelos de ativos os componentes ideais para a rápida adaptação e distribuição de conteúdo como artefatos de conteúdo para várias funções. A redefinição dos objetivos do conteúdo ajuda a reduzir o custo de gerenciamento de canais impressos e digitais e a fornecer experiências holísticas e consistentes nesses canais.

Como profissional de marketing, você pode armazenar e gerenciar modelos no [!DNL Experience Manager Assets] e use um modelo de base única para criar várias experiências de impressão personalizadas com facilidade. Você pode criar vários tipos de material de apoio de marketing, incluindo folhetos, panfletos, cartões postais, cartões de visita e assim por diante, para transmitir de forma lúcida sua mensagem de marketing aos clientes. Você também pode reunir saídas de impressão de várias páginas a partir de saídas de impressão existentes ou novas. Acima de tudo, você pode oferecer simultaneamente experiências digitais e de impressão com facilidade para fornecer uma experiência consistente e integrada para os usuários.

Embora os modelos de ativos sejam [!DNL Adobe InDesign] arquivos, proficiência em [!DNL Adobe InDesign] não é uma barreira à criação de artefatos estelares. Você não precisa mapear os campos de seu [!DNL Adobe InDesign] modelo com os campos de produto que seriam necessários ao criar catálogos. É possível editar os modelos no modo WYSIWYG diretamente na interface da Web. No entanto, para [!DNL Adobe InDesign] para processar as alterações de edição, é necessário configurar [!DNL Experience Manager Assets] para integrar com a [!DNL Adobe InDesign Server].

A capacidade de editar [!DNL Adobe InDesign] Os templates da interface da web ajudam a promover uma maior colaboração entre a equipe de criação e marketing. O aumento da velocidade do conteúdo reduz o tempo de entrada no mercado de materiais de apoio de marketing.

É possível obter os seguintes resultados com modelos de ativos:

* Modifique campos de modelo editáveis na interface da Web.
* Controle o estilo básico do texto, por exemplo, tamanho da fonte, estilo e tipo no nível da tag.
* Altere imagens no modelo usando o Seletor de conteúdo.
* Visualizar edições de modelo.
* Mescle vários arquivos de modelo para criar um artefato de várias páginas.

Quando você escolhe um modelo para seu material de apoio, [!DNL Experience Manager Assets] O cria uma cópia do modelo que pode ser editada. O modelo original é preservado, o que garante que sua sinalização global permaneça intacta e possa ser reutilizada para impor a consistência da marca.

Você pode exportar o arquivo atualizado para a pasta pai nos formatos INDD, PDF ou JPG. Você também pode baixar a saída nesses formatos para o sistema de arquivos local.

## Criar uma garantia {#creating-a-collateral}

Considere um cenário em que você deseja criar materiais de apoio digitais imprimíveis, como folhetos, folhetos e anúncios para uma campanha futura e compartilhe com lojas de pontos de venda em todo o mundo. A criação de material de apoio com base em um modelo ajuda a fornecer uma experiência unificada ao cliente em todos os canais. Os designers podem criar os templates de campanha (página única ou várias páginas) usando uma solução criativa, como [!DNL InDesign] e faça upload dos modelos para [!DNL Experience Manager Assets] para você. Antes de criar um material de apoio, faça upload de um ou mais modelos INDD para o e disponibilize-os no [!DNL Experience Manager] antecipadamente.

1. Entrada [!DNL Experience Manager] clique na interface [!UICONTROL Assets].

1. Nas opções, escolha **[!UICONTROL Modelos]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. Clique em **[!UICONTROL Criar]** e, em seguida, escolha o material de apoio que deseja criar no menu. Por exemplo, escolha **[!UICONTROL Folheto]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. Faça upload de um ou mais modelos INDD para o e disponibilize-os no [!DNL Experience Manager] antecipadamente. Escolha um modelo para o folheto e clique em **[!UICONTROL Próxima]**.
1. Especifique um nome e uma descrição opcional para o folheto.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (Opcional) Clique em **[!UICONTROL Tags]** e selecione uma ou mais tags para o folheto. Clique em **[!UICONTROL Confirmar o]** para confirmar a seleção.
1. Clique em **[!UICONTROL Criar]**. Uma caixa de diálogo confirma que um novo folheto é criado. Clique em **[!UICONTROL Abertura]** para abrir o folheto no modo de edição.

   <!--![chlimage_1-106](assets/.png) -->

   Como alternativa, feche a caixa de diálogo e navegue até a pasta na página Modelos que você começou com para exibir o folheto criado. O tipo do material adicional aparece em sua miniatura na exibição de cartão. Por exemplo, neste caso, a palavra [!UICONTROL Folheto] é exibido na miniatura.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## Editar uma garantia {#editing-a-collateral}

Você pode editar um material de apoio imediatamente após criá-lo. Como alternativa, você pode abri-lo a partir do [!UICONTROL Modelos] ou a página do ativo.

1. Para abrir o material de apoio para edição, siga um destes procedimentos:

   * Abra o material de apoio (folheto neste caso) que você criou na etapa 7 de [Criar uma garantia](/help/assets/asset-templates.md#creating-a-collateral).
   * Na página Modelos, navegue até a pasta onde você criou o material de apoio e clique no [!UICONTROL Editar] ação rápida na miniatura de uma garantia.
   * Na página do ativo para o material de apoio, clique em **[!UICONTROL Editar]** na barra de ferramentas.
   * Selecione o material e clique em **[!UICONTROL Editar]** na barra de ferramentas.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   O localizador de ativos e o editor de texto são exibidos à esquerda da página. O editor de texto é aberto por padrão.

   Você pode usar o editor de texto para modificar o texto que deseja exibir no campo de texto. É possível modificar o tamanho, o estilo, a cor e o tipo da fonte no nível da tag.

   Usando o localizador de ativos, você pode navegar ou pesquisar imagens no [!DNL Experience Manager Assets] e substitua as imagens editáveis no modelo pelas imagens de sua escolha.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   Os editáveis são exibidos à direita. Para que um campo seja editável no [!DNL Experience Manager Assets], o campo correspondente no modelo deve ser marcado em [!DNL InDesign]. Em outras palavras, eles devem ser marcados como editáveis em [!DNL InDesign].

   >[!NOTE]
   >
   >Verifique se [!DNL Experience Manager] A implantação é integrada com um [!DNL InDesign Server] para habilitar [!DNL Experience Manager Assets] para extrair dados do [!DNL InDesign] e disponibilizá-lo para edição. Para obter detalhes, consulte [integrar o Experience Manager Assets ao InDesign Server](/help/assets/indesign.md).

1. Para modificar o texto em um campo editável, clique no campo de texto da lista de campos editáveis e edite o texto no campo.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   É possível editar as propriedades do texto, por exemplo, estilo da fonte, cor e tamanho, usando as opções fornecidas.

1. Clique em **[!UICONTROL Visualizar]** para visualizar as alterações de texto.

1. Para trocar uma imagem, clique no link **[!UICONTROL Localizador de ativos]** ![chlimage_1-113](assets/chlimage_1-318.png).

1. Selecione o campo de imagem na lista de campos editáveis e arraste uma imagem desejada do seletor de ativos para o campo editável.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   Também é possível pesquisar imagens usando palavras-chave, tags e com base no status de publicação. Você pode navegar pelo [!DNL Experience Manager Assets] e navegue até o local da imagem desejada.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. Clique em **[!UICONTROL Visualizar]** para visualizar a imagem.
1. Para editar uma página específica em um material de apoio de várias páginas, use o navegador de página na parte inferior.

1. Clique em **[!UICONTROL Visualizar]** na barra de ferramentas para visualizar todas as alterações. Clique em **[!UICONTROL Concluído]** para salvar as alterações de edição no material de apoio.

   >[!NOTE]
   >
   >As opções Visualizar e Concluído são ativadas somente quando os campos de imagem editáveis no material de apoio não têm ícones ausentes. Se faltam ícones em seu material de apoio, é porque [!DNL Experience Manager] não consegue resolver as imagens no [!DNL InDesign] modelo. Normalmente, [!DNL Experience Manager] O não pode resolver imagens nos seguintes casos:
   >
   >* As imagens não estão incorporadas à base [!DNL InDesign] modelo.
   >* As imagens são vinculadas a partir do sistema de arquivos local.
   >
   >Para habilitar [!DNL Experience Manager] para resolver imagens, faça o seguinte:
   >
   >* Incorporar imagens ao criar [!DNL InDesign] modelos (Consulte [Sobre links e gráficos incorporados](https://helpx.adobe.com/indesign/using/graphics-links.html)).
   >* Montagem [!DNL Experience Manager] para o sistema de arquivos local e, em seguida, mapear os ícones ausentes com os ativos existentes no [!DNL Experience Manager].
   >
   >Para obter mais informações sobre como trabalhar com [!DNL InDesign] documentos, consulte [práticas recomendadas para trabalhar com documentos do InDesign no Experience Manager](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. Para gerar uma representação de PDF para o folheto, selecione a opção Acrobat na caixa de diálogo e clique em **[!UICONTROL Continuar]**.
1. O material de apoio é criado na pasta em que você começou. Para exibir as representações, abra o material de apoio e escolha **[!UICONTROL Representações]** na lista GlobalNav.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. Clique na representação de PDF da lista de representações para baixar o arquivo de PDF. Abra o arquivo PDF para revisar o material de apoio.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Mesclar material de apoio {#merge-collateral}

1. No [!DNL Experience Manager] clique na interface [!UICONTROL Assets] na página Navegação.

1. Nas opções, escolha **[!UICONTROL Modelos]**.

1. Clique em **[!UICONTROL Criar]** e escolha **[!UICONTROL Mesclar]** no menu.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. No [!UICONTROL Mesclagem de modelos] clique em **[!UICONTROL Mesclar]** ![adicionar ativos](assets/do-not-localize/assets_add_icon.png).

1. Navegue até o local do material de apoio que deseja intercalar, clique nas miniaturas do material de apoio que deseja intercalar para selecioná-los.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   Você também pode pesquisar modelos na caixa Omnisearch.

   Você pode navegar pelo [!DNL Experience Manager Assets] repositório ou coleções, navegue até o local dos modelos desejados e selecione-os para mesclar.

   É possível aplicar vários filtros para pesquisar os modelos desejados. Por exemplo, você pode pesquisar modelos com base no tipo de arquivo ou nas tags.

1. Clique em **[!UICONTROL Próxima]** na barra de ferramentas.
1. No **[!UICONTROL Visualizar e reordenar]** , reorganize os modelos se necessário e visualize a seleção de modelos a serem mesclados. Em seguida, clique em **[!UICONTROL Próxima]** na barra de ferramentas.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. No [!UICONTROL Configurar modelo] especifique um nome para o material de apoio. Como opção, especifique as tags que você considerar apropriadas. Se desejar exportar a saída no formato PDF, selecione **[!UICONTROL Acrobat (.PDF)]**. Por padrão, a garantia é exportada em JPG e [!DNL InDesign] formato. Para alterar a miniatura de exibição do material de apoio de várias páginas, clique em **[!UICONTROL Alterar miniatura]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. Clique em **[!UICONTROL Salvar]** e clique em **[!UICONTROL OK]** na caixa de diálogo para fechar a caixa. O material de apoio de várias páginas é criado na pasta em que você começou.

   >[!NOTE]
   >
   >Não é possível editar um material de apoio intercalado posteriormente ou usá-lo para criar outro material de apoio.

## Práticas recomendadas e limitações {#best-practices-limitations-tips}

* A variável [!DNL InDesign] editor em [!DNL Experience Manager] O funciona em nível de tag e todo o texto em uma única tag é considerado uma única entidade. Para preservar a formatação e os estilos de texto ao editar, marque separadamente cada parágrafo (ou texto com um estilo diferente).
