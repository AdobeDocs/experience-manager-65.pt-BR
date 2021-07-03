---
title: Modelos de ativos
description: Saiba mais sobre os modelos de Ativos no [!DNL Adobe Experience Manager Assets] e como usar os modelos de ativos para criar materiais de apoio de marketing.
contentOwner: AG
role: User
feature: Gerenciamento de ativos,Ferramentas do desenvolvedor
exl-id: 12c92aad-3a1d-486e-a830-31de2fc6d07b
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 0%

---

# Modelos de ativos {#asset-templates}

Os modelos de ativos são uma classe especial de ativos que facilitam o redirecionamento rápido de conteúdo visualmente rico para mídia digital e impressa. Um modelo de ativo inclui duas partes, a seção de mensagens fixas e a seção editável. A seção de mensagens fixas pode conter conteúdo proprietário, como logotipo da marca e informações de direitos autorais que estão desativados para edição. A seção editável pode conter conteúdo visual e textual em campos que podem ser editados para personalizar mensagens.

A flexibilidade para fazer edições limitadas e, ao mesmo tempo, proteger a sinalização global torna os modelos de ativos os blocos de construção ideais para adaptação e distribuição rápidas de conteúdo como artefatos de conteúdo para várias funções. O redirecionamento de conteúdo ajuda a reduzir o custo do gerenciamento de canais digitais e de impressão, além de fornecer experiências holísticas e consistentes nesses canais.

Como comerciante, você pode armazenar e gerenciar modelos em [!DNL Experience Manager Assets] e usar um único modelo básico para criar várias experiências de impressão personalizadas com facilidade. Você pode criar vários tipos de materiais de apoio de marketing, incluindo folhetos, cartões postais, cartões comerciais e assim por diante, para transmitir de forma lúdica sua mensagem de marketing aos clientes. Também é possível reunir saídas de impressão de várias páginas de saídas de impressão existentes ou novas. Acima de tudo, você pode oferecer simultaneamente experiências digitais e de impressão com facilidade para fornecer uma experiência consistente e integrada para os usuários.

Embora os modelos de ativos sejam principalmente arquivos [!DNL Adobe InDesign], a proficiência em [!DNL Adobe InDesign] não é uma barreira para criar artefatos estelares. Não é necessário mapear os campos do modelo [!DNL Adobe InDesign] com os campos de produto que você precisa para criar catálogos. Você pode editar os modelos no modo WYSIWYG diretamente na interface da Web. No entanto, para [!DNL Adobe InDesign] processar suas alterações de edição, primeiro você deve configurar [!DNL Experience Manager Assets] para integrar com [!DNL Adobe InDesign Server].

A capacidade de editar [!DNL Adobe InDesign] modelos da interface da Web ajuda a promover maior colaboração entre a equipe de criação e marketing. O aumento da velocidade do conteúdo reduz o tempo de comercialização dos colaterais de marketing.

Você pode obter o seguinte com modelos de ativos:

* Modifique campos de modelo editáveis da interface da Web.
* Controle o estilo básico do texto, por exemplo, tamanho da fonte, estilo e tipo no nível da tag.
* Altere imagens no modelo usando o Seletor de conteúdo.
* Visualizar edições do modelo.
* Mesclar vários arquivos de modelo para criar um artefato de várias páginas.

Quando você escolhe um modelo para sua garantia, [!DNL Experience Manager Assets] cria uma cópia do modelo que você pode editar. O modelo original é preservado, o que garante que sua assinatura global permaneça intacta e possa ser reutilizada para reforçar a consistência da marca.

É possível exportar o arquivo atualizado dentro da pasta principal nos formatos INDD, PDF ou JPG. Também é possível baixar a saída nesses formatos para o sistema de arquivos local.

## Criar uma garantia {#creating-a-collateral}

Considere um cenário em que você deseja criar materiais de apoio para impressão digitais, como folhetos, panfletos e anúncios para uma campanha futura e compartilhar com lojas de varejo globalmente. Criar ativos de garantia com base em um modelo ajuda a fornecer uma experiência unificada do cliente em todos os canais. Os designers podem criar os modelos de campanha (página única ou várias páginas) usando uma solução criativa, como [!DNL InDesign] e fazer upload dos modelos para [!DNL Experience Manager Assets] para você. Antes de criar um material adicional, faça com que um ou mais modelos INDD sejam carregados e disponibilizados com [!DNL Experience Manager] antecedência.

1. Na interface [!DNL Experience Manager] clique em [!UICONTROL Ativos].

1. Nas opções, escolha **[!UICONTROL Templates]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. Clique em **[!UICONTROL Criar]** e escolha os materiais de apoio que deseja criar no menu. Por exemplo, escolha **[!UICONTROL Brochura]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. Tenha um ou mais modelos INDD carregados e disponíveis [!DNL Experience Manager] com antecedência. Escolha um modelo para o folheto e clique em **[!UICONTROL Next]**.
1. Especifique um nome e uma descrição opcional para a brochura.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (Opcional) Clique em **[!UICONTROL Tags]** e selecione uma ou mais tags para o folheto. Clique em **[!UICONTROL Confirm]** para confirmar a seleção.
1. Clique em **[!UICONTROL Criar]**. Uma caixa de diálogo confirma que uma nova brochura foi criada. Clique em **[!UICONTROL Abrir]** para abrir o folheto no modo de edição.

   <!--![chlimage_1-106](assets/.png) -->

   Como alternativa, feche a caixa de diálogo e navegue até a pasta na página Modelos que você começou a usar para exibir o folheto que você criou. O tipo de material de apoio aparece na miniatura na exibição de cartão. Por exemplo, neste caso, a palavra [!UICONTROL Brochure] é exibida na miniatura.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## Editar uma garantia {#editing-a-collateral}

Você pode editar um material adicional imediatamente depois de criá-lo. Como alternativa, você a abre na página [!UICONTROL Modelos] ou na página de ativos.

1. Para abrir o material para edição, execute um dos seguintes procedimentos:

   * Abra o material adicional (brochura neste caso) criado na etapa 7 de [Create a collateral](/help/assets/asset-templates.md#creating-a-collateral).
   * Na página Modelos , navegue até uma pasta onde você criou o material de apoio e clique na ação rápida [!UICONTROL Editar] na miniatura de um material de apoio.
   * Na página de ativos do material de apoio, clique em **[!UICONTROL Editar]** na barra de ferramentas.
   * Selecione o material de apoio e clique em **[!UICONTROL Editar]** na barra de ferramentas.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   O localizador de ativos e o editor de texto são exibidos à esquerda da página. O editor de texto é aberto por padrão.

   Você pode usar o editor de texto para modificar o texto que deseja exibir no campo de texto. Você pode modificar o tamanho, estilo, cor e tipo da fonte no nível da tag.

   Usando o localizador de ativos, você pode procurar ou procurar imagens em [!DNL Experience Manager Assets] e substituir as imagens editáveis no modelo por imagens de sua escolha.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   Os editáveis são exibidos à direita. Para que um campo possa ser editado em [!DNL Experience Manager Assets], o campo correspondente no modelo deve ser marcado em [!DNL InDesign]. Em outras palavras, eles devem ser marcados como editáveis em [!DNL InDesign].

   >[!NOTE]
   >
   >Certifique-se de que a implantação [!DNL Experience Manager] esteja integrada a um [!DNL InDesign Server] para habilitar [!DNL Experience Manager Assets] para extrair dados do template [!DNL InDesign] e disponibilizá-la para edição. Para obter detalhes, consulte [integrar ativos do Experience Manager com o InDesign Server](/help/assets/indesign.md).

1. Para modificar o texto em um campo editável, clique no campo de texto da lista de campos editáveis e edite o texto no campo.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   É possível editar as propriedades do texto, por exemplo, estilo de fonte, cor e tamanho usando as opções fornecidas.

1. Clique em **[!UICONTROL Preview]** para visualizar as alterações de texto.

1. Para trocar uma imagem, clique no **[!UICONTROL Localizador de ativos]** ![chlimage_1-113](assets/chlimage_1-318.png).

1. Selecione o campo de imagem da lista de campos editáveis e arraste uma imagem desejada do seletor de ativos para o campo editável.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   Também é possível pesquisar por imagens usando palavras-chave, tags e com base em seu status de publicação. Você pode navegar pelo repositório [!DNL Experience Manager Assets] e navegar até o local da imagem desejada.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. Clique em **[!UICONTROL Preview]** para visualizar a imagem.
1. Para editar uma página específica em um material de apoio de várias páginas, use o navegador da página na parte inferior.

1. Clique em **[!UICONTROL Preview]** na barra de ferramentas para visualizar todas as alterações. Clique em **[!UICONTROL Concluído]** para salvar as alterações de edição nas garantias.

   >[!NOTE]
   >
   >As opções Visualização e Concluído são ativadas somente quando os campos de imagem editáveis no material de apoio não têm ícones ausentes. Se houver ícones ausentes em seu material de apoio, isso ocorre porque [!DNL Experience Manager] não consegue resolver as imagens no modelo [!DNL InDesign]. Geralmente, [!DNL Experience Manager] não consegue resolver imagens nos seguintes casos:
   >
   >* As imagens não são incorporadas no modelo [!DNL InDesign] subjacente.
   >* As imagens são vinculadas do sistema de arquivos local.

   >
   >Para habilitar [!DNL Experience Manager] para resolver imagens, faça o seguinte:
   >
   >* Incorpore imagens ao criar modelos [!DNL InDesign] (Consulte [Sobre links e gráficos incorporados](https://helpx.adobe.com/indesign/using/graphics-links.html)).
   >* Monte [!DNL Experience Manager] em seu sistema de arquivos local e mapeie ícones ausentes com ativos existentes em [!DNL Experience Manager].

   >
   >Para obter mais informações sobre como trabalhar com documentos [!DNL InDesign], consulte [práticas recomendadas para trabalhar com documentos do InDesign no Experience Manager](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. Para gerar uma representação PDF para o folheto, selecione a opção Acrobat na caixa de diálogo e clique em **[!UICONTROL Continuar]**.
1. O material adicional é criado na pasta com a qual você começou. Para visualizar as representações, abra o material de apoio e escolha **[!UICONTROL Representações]** na lista GlobalNavigation.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. Clique na representação do PDF na lista de representações para baixar o arquivo PDF. Abra o arquivo PDF para revisar o material adicional.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Colateral de fusão {#merge-collateral}

1. Na interface [!DNL Experience Manager], clique em [!UICONTROL Ativos] na página Navegação.

1. Nas opções, escolha **[!UICONTROL Templates]**.

1. Clique em **[!UICONTROL Criar]** e escolha **[!UICONTROL Mesclar]** no menu.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. Na página [!UICONTROL Mesclar modelos], clique em **[!UICONTROL Mesclar]** ![adicionar ativos](assets/do-not-localize/assets_add_icon.png).

1. Navegue até o local do material de apoio que deseja mesclar, clique nas miniaturas do material de apoio que deseja mesclar para selecioná-las.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   Também é possível procurar modelos na caixa Omnisearch.

   Você pode navegar pelo repositório ou coleções [!DNL Experience Manager Assets], navegar até o local dos modelos desejados e, em seguida, selecioná-los para mesclar.

   Você pode aplicar vários filtros para pesquisar os modelos desejados. Por exemplo, você pode pesquisar modelos com base no tipo de arquivo ou tags.

1. Clique em **[!UICONTROL Avançar]** na barra de ferramentas.
1. Na tela **[!UICONTROL Preview &amp; Reorder]**, reorganize os modelos, se necessário, e visualize a seleção de modelos para mesclar. Em seguida, clique em **[!UICONTROL Next]** na barra de ferramentas.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. Na tela [!UICONTROL Configurar modelo], especifique um nome para o material adicional. Opcionalmente, especifique quaisquer tags que você considere apropriadas. Se quiser exportar a saída no formato PDF, selecione **[!UICONTROL Acrobat (.PDF)]**. Por padrão, o material de apoio é exportado no formato JPG e [!DNL InDesign] . Para alterar a miniatura de exibição do material de apoio de várias páginas, clique em **[!UICONTROL Alterar miniatura]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. Clique em **[!UICONTROL Save]** e em **[!UICONTROL OK]** na caixa de diálogo para fechar a caixa de diálogo. O material de apoio multipáginas é criado na pasta com a qual você começou.

   >[!NOTE]
   >
   >Não é possível editar posteriormente uma garantia resultante da fusão ou usá-la para criar outra garantia.

## Práticas recomendadas e limitações {#best-practices-limitations-tips}

* O editor [!DNL InDesign] em [!DNL Experience Manager] funciona em um nível de tag e todo o texto em uma única tag é considerado uma única entidade. Para preservar a formatação e os estilos do texto durante a edição, adicione uma tag a cada parágrafo (ou um texto com estilos diferentes) separadamente.
