---
title: Modelos de ativos
description: Saiba mais sobre os modelos de ativos em [!DNL Adobe Experience Manager Assets] e como usar modelos de ativos para criar materiais de apoio de marketing.
contentOwner: AG
role: User
feature: Asset Management,Developer Tools
exl-id: 12c92aad-3a1d-486e-a830-31de2fc6d07b
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---

# Modelos de ativos {#asset-templates}

Os modelos de ativos são uma classe especial de ativos que facilitam o redirecionamento rápido de conteúdo visualmente rico para mídia digital e impressa. Um modelo de ativo inclui duas partes, a seção de mensagens fixas e a seção editável. A seção de mensagens fixas pode conter conteúdo proprietário, como logotipo da marca e informações de direitos autorais que estão desativados para edição. A seção editável pode conter conteúdo visual e textual em campos que podem ser editados para personalizar mensagens.

A flexibilidade para fazer edições limitadas e, ao mesmo tempo, proteger a sinalização global torna os modelos de ativos os blocos de construção ideais para adaptação e distribuição rápidas de conteúdo como artefatos de conteúdo para várias funções. O redirecionamento de conteúdo ajuda a reduzir o custo do gerenciamento de canais digitais e de impressão, além de fornecer experiências holísticas e consistentes nesses canais.

Como comerciante, você pode armazenar e gerenciar modelos em [!DNL Experience Manager Assets] e use um único modelo básico para criar várias experiências de impressão personalizadas com facilidade. Você pode criar vários tipos de materiais de apoio de marketing, incluindo folhetos, cartões postais, cartões comerciais e assim por diante, para transmitir de forma lúdica sua mensagem de marketing aos clientes. Também é possível reunir saídas de impressão de várias páginas de saídas de impressão existentes ou novas. Acima de tudo, você pode oferecer simultaneamente experiências digitais e de impressão com facilidade para fornecer uma experiência consistente e integrada para os usuários.

Embora os modelos de ativos sejam [!DNL Adobe InDesign] arquivos, proficiência em [!DNL Adobe InDesign] não constitui um obstáculo à criação de artefatos estelares. Não é necessário mapear os campos de [!DNL Adobe InDesign] com os campos do produto que você precisaria para criar catálogos. Você pode editar os modelos no modo WYSIWYG diretamente na interface da Web. No entanto, para [!DNL Adobe InDesign] para processar suas alterações de edição, primeiro você deve configurar [!DNL Experience Manager Assets] para integrar com [!DNL Adobe InDesign Server].

A capacidade de editar [!DNL Adobe InDesign] modelos da interface da Web ajudam a promover maior colaboração entre a equipe de criação e marketing. O aumento da velocidade do conteúdo reduz o tempo de comercialização dos colaterais de marketing.

Você pode obter o seguinte com modelos de ativos:

* Modifique campos de modelo editáveis da interface da Web.
* Controle o estilo básico do texto, por exemplo, tamanho da fonte, estilo e tipo no nível da tag.
* Altere imagens no modelo usando o Seletor de conteúdo.
* Visualizar edições do modelo.
* Mesclar vários arquivos de modelo para criar um artefato de várias páginas.

Ao escolher um modelo para sua garantia, [!DNL Experience Manager Assets] cria uma cópia do modelo que pode ser editada. O modelo original é preservado, o que garante que sua assinatura global permaneça intacta e possa ser reutilizada para reforçar a consistência da marca.

Você pode exportar o arquivo atualizado dentro da pasta pai nos formatos INDD, PDF ou JPG. Também é possível baixar a saída nesses formatos para o sistema de arquivos local.

## Criar uma garantia {#creating-a-collateral}

Considere um cenário em que você deseja criar materiais de apoio para impressão digitais, como folhetos, panfletos e anúncios para uma campanha futura e compartilhar com lojas de varejo globalmente. Criar ativos de garantia com base em um modelo ajuda a fornecer uma experiência unificada do cliente em todos os canais. Os designers podem criar os modelos de campanha (página única ou várias páginas) usando uma solução criativa, como [!DNL InDesign] e fazer upload dos modelos para [!DNL Experience Manager Assets] para você. Antes de criar um material de apoio, tenha um ou mais modelos INDD enviados para e disponibilizados em [!DNL Experience Manager] antecipadamente.

1. Em [!DNL Experience Manager] clique na interface [!UICONTROL Ativos].

1. Nas opções, escolha **[!UICONTROL Modelos]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. Clique em **[!UICONTROL Criar]** e, em seguida, escolha o material que deseja criar no menu . Por exemplo, escolha **[!UICONTROL Brochura]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. Faça upload de um ou mais modelos INDD para e estejam disponíveis em [!DNL Experience Manager] antecipadamente. Escolha um modelo para a brochura e clique em **[!UICONTROL Próximo]**.
1. Especifique um nome e uma descrição opcional para a brochura.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (Opcional) Clique em **[!UICONTROL Tags]** e selecione uma ou mais tags para o folheto. Clique em **[!UICONTROL Confirmar]** para confirmar a seleção.
1. Clique em **[!UICONTROL Criar]**. Uma caixa de diálogo confirma que uma nova brochura foi criada. Clique em **[!UICONTROL Abrir]** para abrir a brochura no modo de edição.

   <!--![chlimage_1-106](assets/.png) -->

   Como alternativa, feche a caixa de diálogo e navegue até a pasta na página Modelos que você começou a usar para exibir o folheto que você criou. O tipo de material de apoio aparece na miniatura na exibição de cartão. Por exemplo, neste caso, a palavra [!UICONTROL Brochura] é exibida na miniatura.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## Editar uma garantia {#editing-a-collateral}

Você pode editar um material adicional imediatamente depois de criá-lo. Como alternativa, abra-a no [!UICONTROL Modelos] ou a página do ativo.

1. Para abrir o material para edição, execute um dos seguintes procedimentos:

   * Abra o material de apoio (neste caso, brochura) criado na etapa 7 de [Criar uma garantia](/help/assets/asset-templates.md#creating-a-collateral).
   * Na página Modelos , navegue até uma pasta onde você criou o material de apoio e clique no link [!UICONTROL Editar] ação rápida na miniatura de um material de apoio.
   * Na página do ativo do material de apoio, clique em **[!UICONTROL Editar]** na barra de ferramentas.
   * Selecione o material de apoio e clique em **[!UICONTROL Editar]** na barra de ferramentas.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   O localizador de ativos e o editor de texto são exibidos à esquerda da página. O editor de texto é aberto por padrão.

   Você pode usar o editor de texto para modificar o texto que deseja exibir no campo de texto. Você pode modificar o tamanho, estilo, cor e tipo da fonte no nível da tag.

   Usando o localizador de ativos, você pode procurar ou procurar imagens no [!DNL Experience Manager Assets] e substitua as imagens editáveis no modelo por imagens de sua escolha.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   Os editáveis são exibidos à direita. Para que um campo seja editável em [!DNL Experience Manager Assets], o campo correspondente no template deve ser marcado em [!DNL InDesign]. Em outras palavras, eles devem ser marcados como editáveis no [!DNL InDesign].

   >[!NOTE]
   >
   >Certifique-se de que [!DNL Experience Manager] a implantação é integrada a um [!DNL InDesign Server] para ativar [!DNL Experience Manager Assets] para extrair dados do [!DNL InDesign] e disponibilizá-lo para edição. Para obter detalhes, consulte [integrar o Experience Manager Assets ao InDesign Server](/help/assets/indesign.md).

1. Para modificar o texto em um campo editável, clique no campo de texto da lista de campos editáveis e edite o texto no campo.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   É possível editar as propriedades do texto, por exemplo, estilo de fonte, cor e tamanho usando as opções fornecidas.

1. Clique em **[!UICONTROL Visualizar]** para visualizar as alterações de texto.

1. Para trocar uma imagem, clique no botão **[!UICONTROL Localizador de ativos]** ![chlimage_1-113](assets/chlimage_1-318.png).

1. Selecione o campo de imagem da lista de campos editáveis e arraste uma imagem desejada do seletor de ativos para o campo editável.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   Também é possível pesquisar por imagens usando palavras-chave, tags e com base em seu status de publicação. Você pode navegar pelo [!DNL Experience Manager Assets] e navegue até o local da imagem desejada.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. Clique em **[!UICONTROL Visualizar]** para visualizar a imagem.
1. Para editar uma página específica em um material de apoio de várias páginas, use o navegador da página na parte inferior.

1. Clique em **[!UICONTROL Visualizar]** na barra de ferramentas para visualizar todas as alterações. Clique em **[!UICONTROL Concluído]** para salvar as alterações de edição no material de apoio.

   >[!NOTE]
   >
   >As opções Visualização e Concluído são ativadas somente quando os campos de imagem editáveis no material de apoio não têm ícones ausentes. Se houver ícones ausentes em sua garantia, é porque [!DNL Experience Manager] não consegue resolver as imagens no [!DNL InDesign] modelo . Geralmente, [!DNL Experience Manager] O não pode resolver imagens nos seguintes casos:
   >
   >* As imagens não são incorporadas no subjacente [!DNL InDesign] modelo .
   >* As imagens são vinculadas do sistema de arquivos local.

   >
   >Para ativar [!DNL Experience Manager] para resolver imagens, faça o seguinte:
   >
   >* Incorporar imagens ao criar [!DNL InDesign] modelos (consulte [Sobre links e gráficos incorporados](https://helpx.adobe.com/indesign/using/graphics-links.html)).
   >* Montagem [!DNL Experience Manager] para seu sistema de arquivos local e, em seguida, mapeie ícones ausentes com os ativos existentes no [!DNL Experience Manager].

   >
   >Para obter mais informações sobre como trabalhar com a [!DNL InDesign] documentos, consulte [práticas recomendadas para trabalhar com documentos do InDesign no Experience Manager](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. Para gerar uma representação de PDF para o folheto, selecione a opção Acrobat na caixa de diálogo e clique em **[!UICONTROL Continuar]**.
1. O material adicional é criado na pasta com a qual você começou. Para visualizar as representações, abra o material adicional e escolha **[!UICONTROL Representações]** na lista GlobalNavigation.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. Clique na representação de PDF da lista de representações para baixar o arquivo de PDF. Abra o arquivo PDF para revisar a garantia.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Colateral de fusão {#merge-collateral}

1. No [!DNL Experience Manager] clique na interface [!UICONTROL Ativos] na página Navegação.

1. Nas opções, escolha **[!UICONTROL Modelos]**.

1. Clique em **[!UICONTROL Criar]** e escolha **[!UICONTROL Mesclar]** no menu .

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. No [!UICONTROL Mesclagem de modelos] página, clique em **[!UICONTROL Mesclar]** ![adicionar ativos](assets/do-not-localize/assets_add_icon.png).

1. Navegue até o local do material de apoio que deseja mesclar, clique nas miniaturas do material de apoio que deseja mesclar para selecioná-las.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   Também é possível procurar modelos na caixa Omnisearch.

   Você pode navegar pelo [!DNL Experience Manager Assets] repositório ou coleções, navegue até o local dos modelos desejados e selecione-os para mesclar.

   Você pode aplicar vários filtros para pesquisar os modelos desejados. Por exemplo, você pode pesquisar modelos com base no tipo de arquivo ou tags.

1. Clique em **[!UICONTROL Próximo]** na barra de ferramentas.
1. No **[!UICONTROL Visualizar e reordenar]** , reorganize os modelos, se necessário, e visualize a seleção de modelos para mesclar. Em seguida, clique em **[!UICONTROL Próximo]** na barra de ferramentas.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. No [!UICONTROL Configurar modelo] , especifique um nome para o material de apoio. Opcionalmente, especifique quaisquer tags que você considere apropriadas. Se quiser exportar a saída no formato PDF, selecione **[!UICONTROL Acrobat (.PDF)]**. Por padrão, as garantias são exportadas em JPG e [!DNL InDesign] formato. Para alterar a miniatura de exibição do material de apoio de várias páginas, clique em **[!UICONTROL Alterar miniatura]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. Clique em **[!UICONTROL Salvar]** e, em seguida, clique em **[!UICONTROL OK]** na caixa de diálogo para fechar a caixa de diálogo. O material de apoio multipáginas é criado na pasta com a qual você começou.

   >[!NOTE]
   >
   >Não é possível editar posteriormente uma garantia resultante da fusão ou usá-la para criar outra garantia.

## Práticas recomendadas e limitações {#best-practices-limitations-tips}

* O [!DNL InDesign] editor em [!DNL Experience Manager] funciona em um nível de tag e todo o texto em uma única tag é considerado uma única entidade. Para preservar a formatação e os estilos do texto durante a edição, adicione uma tag a cada parágrafo (ou um texto com estilos diferentes) separadamente.
