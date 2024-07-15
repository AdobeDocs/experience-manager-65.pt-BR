---
title: Editor de rich text
description: O Editor de Rich Text é um elemento básico fundamental para inserir conteúdo textual no AEM.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
docset: aem65
exl-id: 5623dcf4-bda9-4dee-ace3-5a1f6057e96c
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1764'
ht-degree: 2%

---

# Editor de rich text {#rich-text-editor}

O Editor de Rich Text é um elemento básico fundamental para inserir conteúdo textual no AEM. É a base de vários componentes, incluindo:

* Texto
* Imagem de texto
* Tabela

## Editor de rich text {#rich-text-editor-1}

A caixa de diálogo de edição WYSIWYG fornece uma ampla variedade de funcionalidades:

![cq55_rte_basicchars](assets/cq55_rte_basicchars.png)

>[!NOTE]
>
>Os recursos disponíveis podem ser configurados para projetos individuais, portanto, podem variar para sua instalação.

## Edição no local {#in-place-editing}

Além do modo de Edição de Rich Text baseado em caixas de diálogo, o AEM também fornece o modo de edição no local, que permite a edição direta do texto conforme é exibido no layout da página.

Clique duas vezes em um parágrafo (um clique duplo lento) para entrar no modo de edição local (a borda do componente agora será laranja).

Você poderá editar o texto diretamente na página, em vez de dentro de uma janela de diálogo. Basta fazer as alterações, que serão salvas automaticamente.

![cq55_rte_inlineediting](assets/cq55_rte_inlineediting.png)

>[!NOTE]
>
>Se o localizador de conteúdo estiver aberto, uma barra de ferramentas com as opções de formatação do RTE será exibida na parte superior da guia (como acima).
>
>Se o localizador de conteúdo não estiver aberto, a barra de ferramentas não será exibida.

Atualmente, o modo Edição de Entrada está habilitado para elementos de página gerados pelos componentes **Texto** e **Título**.

>[!NOTE]
>
>O componente [!UICONTROL Título] foi projetado para conter um texto curto sem quebras de linha. Ao editar um título no Modo de Edição no Local, inserir uma quebra de linha abre um novo componente **Texto** abaixo do título.

## Recursos do Editor de Rich Text {#features-of-the-rich-text-editor}

O Editor de Rich Text fornece um intervalo de recursos, eles [dependem da configuração](/help/sites-administering/rich-text-editor.md) do componente individual. Os recursos estão disponíveis para a interface otimizada para toque e a clássica.

### Formatos de caractere básico {#basic-character-formats}

![Barra de ferramentas de Formato de Caractere](do-not-localize/cq55_rte_basicchars.png)

Aqui você pode aplicar formatação aos caracteres que selecionou (realçados); algumas opções também possuem teclas de atalho:

* Negrito (Ctrl-B)
* Itálico (Ctrl-I)
* Sublinhado (Ctrl-U)
* Subscrito
* Sobrescrito

![cq55_rte_basicchars_use](assets/cq55_rte_basicchars_use.png)

Todos operam como um botão de alternância, portanto, a reseleção removerá o formato.

### Estilos e formatos predefinidos {#predefined-styles-and-formats}

![cq55_rte_stylesParagraph](assets/cq55_rte_stylesparagraph.png)

Sua instalação pode incluir estilos e formatos predefinidos. Eles estão disponíveis com as listas suspensas **[!UICONTROL Estilo]** e **[!UICONTROL Formato]** e podem ser aplicados ao texto selecionado.

Um estilo pode ser aplicado a uma cadeia de caracteres específica (um estilo correlaciona-se ao CSS):

![cq55_rte_style_use](assets/cq55_rte_styles_use.png)

Enquanto um formato é aplicado a todo o parágrafo de texto (um formato é baseado em HTML):

![cq55_rte_Paragraph_use](assets/cq55_rte_paragraph_use.png)

Um formato específico só pode ser alterado (o padrão é **[!UICONTROL Parágrafo]**).

Um estilo pode ser removido; coloque o cursor dentro do texto ao qual o estilo foi aplicado e clique no ícone remover:

>[!CAUTION]
>
>Na verdade, não selecione novamente nenhum texto no qual o estilo foi aplicado ou o ícone será desativado.

### Recortar, copiar, colar {#cut-copy-paste}

![Barra de ferramentas Recortar, Copiar, Colar](do-not-localize/cq55_rte_cutcopypaste.png)

As funções padrão de **[!UICONTROL Recortar]** e **[!UICONTROL Copiar]** estão disponíveis. Várias opções de **[!UICONTROL Colar]** são fornecidas para atender a diferentes formatos.

* Recortar (Ctrl-X)
* Copiar (Ctrl-C)
* Colar
Este é o mecanismo de colagem padrão (Ctrl-V) do componente; quando instalado pronto para uso, está configurado para ser [!UICONTROL Colar do Word].

* Colar como texto: elimina todos os estilos e formatações para colar apenas o texto sem formatação.

* Colar do Word: cola o conteúdo como HTML (com alguma reformatação necessária).

### Desfazer, Refazer {#undo-redo}

![Desfazer, Refazer barra de ferramentas](do-not-localize/cq55_rte_undoredo.png)

O AEM mantém um registro das suas últimas 50 ações no componente atual, mantido em ordem cronológica. Essas ações podem ser desfeitas (e então refeitas) em ordem estrita, se necessário.

>[!CAUTION]
>
>O histórico é mantido somente para a sessão de edição atual. Ele é reiniciado sempre que o componente é aberto para edição.

>[!NOTE]
>
>Cinquenta é o número padrão de tarefas. Isso pode ser diferente para a sua instalação.

### Alinhamento {#alignment}

![Barra de ferramentas de alinhamento](do-not-localize/cq55_rte_alignment.png)

O texto pode ser alinhado à esquerda, ao centro ou à direita.

![cq55_rte_alignment_use](assets/cq55_rte_alignment_use.png)

### Recuo {#indentation}

![Barra de ferramentas de recuo](do-not-localize/cq55_rte_indent.png)

O recuo de um parágrafo pode ser aumentado ou diminuído. O parágrafo selecionado será recuado, qualquer novo texto inserido manterá o nível atual de recuo.

![cq55_rte_Indent_use](assets/cq55_rte_indent_use.png)

### Listas {#lists}

![Barra de ferramentas de listas](do-not-localize/cq55_rte_lists.png)

Listas com marcadores e numeradas podem ser criadas dentro do texto. Selecione o tipo de lista e comece a digitar ou destaque o texto a ser convertido. Em ambos os casos, um feed de linha iniciará um novo item de lista.

É possível obter listas aninhadas recuando um ou mais itens de lista.

O estilo de uma lista pode ser alterado simplesmente posicionando o cursor dentro da lista e selecionando o outro estilo. Uma sublista também pode ter um estilo diferente da lista que a contém. Isso pode ser aplicado depois que a sublista é criada (por recuo).

![cq55_rte_lists_use](assets/cq55_rte_lists_use.png)

### Links {#links}

![Barra de ferramentas de links](do-not-localize/cq55_rte_links.png)

Um link para um URL (no site ou em um local externo) é gerado destacando o texto necessário e clicando no ícone de hiperlink:

![Ícone de Hiperlink](do-not-localize/chlimage_1-9.png)

Uma caixa de diálogo permitirá que você especifique o URL de destino; também se ele deve ser aberto em uma nova janela.

![cq55_rte_link_use](assets/cq55_rte_link_use.png)

É possível:

* Digite um URI diretamente
* Use o mapa do site para selecionar uma página em seu site
* Insira o URI e anexe a âncora de destino; por exemplo, `www.TargetUri.org#AnchorName`
* Insira uma âncora apenas (para fazer referência à &quot;página atual&quot;); Por exemplo, `#anchor`
* Procure uma página no localizador de conteúdo e, em seguida, arraste e solte o ícone de página na caixa de diálogo Hiperlink

>[!NOTE]
>
>O URI pode ser anexado a qualquer um dos protocolos configurados para sua instalação. Em uma instalação padrão, eles são `https://`, `ftp://` e `mailto:`. Os protocolos não configurados para a sua instalação serão rejeitados e marcados como inválidos.

Para quebrar a posição do link, coloque o cursor em qualquer lugar dentro do texto do link e clique no ícone [!UICONTROL Desvincular]:

![Ícone Desvincular](do-not-localize/chlimage_1-10.png)

### Âncoras {#anchors}

![Barra de ferramentas Âncoras](do-not-localize/cq55_rte_anchor.png)

Uma âncora pode ser criada em qualquer lugar dentro do texto posicionando o cursor ou selecionando algum texto. Em seguida, clique no ícone **Âncora** para abrir a caixa de diálogo.

Insira o nome da âncora e clique em **OK** para salvar.

![cq55_rte_anchor_use](assets/cq55_rte_anchor_use.png)

A âncora é exibida quando o componente está sendo editado e agora pode ser usada em um destino para links.

![chlimage_1-104](assets/chlimage_1-104.png)

### Localizar e substituir {#find-and-replace}

![Localizar e substituir a barra de ferramentas](do-not-localize/cq55_rte_findreplace.png)

O AEM fornece as funções **Localizar** e **Substituir** (localizar e substituir).

Ambos têm um botão **Localizar próximo** para procurar o texto especificado no componente aberto. Você também pode especificar se precisa que letras maiúsculas e minúsculas sejam correspondidas.

A pesquisa sempre iniciará a partir da posição atual do cursor dentro do texto. Quando o fim do componente for atingido, uma mensagem informará que a próxima operação de pesquisa começará do início.

![cq55_rte_find_use](assets/cq55_rte_find_use.png)

A opção **Substituir** permite **Localizar** e **Substituir** uma instância individual com o texto especificado ou **Substituir todas** instâncias no componente atual.

![cq55_rte_findreplace_use](assets/cq55_rte_findreplace_use.png)

### Imagens {#images}

As imagens podem ser arrastadas do localizador de conteúdo para adicioná-las ao texto.

![cq55_rte_image_use](assets/cq55_rte_image_use.png)

>[!NOTE]
>
>O AEM também oferece componentes especializados para configurações de imagem mais detalhadas. Por exemplo, os componentes **Imagem** e **Imagem de Texto** estão disponíveis.

### Verificador ortográfico {#spelling-checker}

![Verificador ortográfico](do-not-localize/cq55_rte_spellchecker.png)

O verificador ortográfico verificará todo o texto no componente atual.

Qualquer grafia incorreta será destacada:

![cq55_rte_spellchecker_use](assets/cq55_rte_spellchecker_use.png)

>[!NOTE]
>
>O verificador ortográfico operará no idioma do site ao obter a propriedade de idioma da subárvore ou extrair o idioma do URL. Por exemplo, a ramificação `en` será verificada em inglês e a ramificação `de` em alemão.

### Tabelas {#tables}

As tabelas estão disponíveis:

* Como o componente **Tabela**

  ![Componente de tabela](assets/chlimage_1-105.png)

* No componente **Texto**

  ![Barra de ferramentas de texto](do-not-localize/chlimage_1-11.png)

  >[!NOTE]
  >
  >Embora as tabelas estejam disponíveis no RTE, é recomendável usar o componente **Tabela** ao criar tabelas.

A funcionalidade de tabela dos componentes **Texto** e **Tabela** está disponível por meio do menu de contexto (geralmente o botão direito do mouse) clicado na tabela; por exemplo:

![cq55_rte_tablemenu](assets/cq55_rte_tablemenu.png)

>[!NOTE]
>
>No componente **Tabela**, uma barra de ferramentas especializada também está disponível, incluindo várias funções padrão de editor de rich text, juntamente com um subconjunto das funções específicas de tabela.

As funções específicas da tabela são:

* [Propriedades da tabela](#table-properties)
* [Propriedades da célula](#cell-properties)
* [Adicionar ou Excluir Linhas](#add-or-delete-rows)
* [Adicionar ou excluir colunas](#add-or-delete-columns)
* [Seleção de Linhas ou Colunas Inteiras](#selecting-entire-rows-or-columns)
* [Mesclar Células](#merge-cells)
* [Dividir células](#split-cells)
* [Tabelas aninhadas](#creating-nested-tables)
* [Remover tabela](#remove-table)

#### Propriedades da tabela {#table-properties}

![cq55_rte_tableproperties_icon](assets/cq55_rte_tableproperties_icon.png)

As propriedades básicas da tabela podem ser configuradas antes de clicar em **OK** para salvar:

![cq55_rte_tableproperties_dialog](assets/cq55_rte_tableproperties_dialog.png)

* **Largura**: a largura total da tabela.

* **Altura**: a altura total da tabela.

* **Borda**: o tamanho da borda da tabela.

* **Preenchimento da célula**: isso define o espaço em branco entre o conteúdo da célula e suas bordas.

* **Espaçamento entre células**: isso define a distância entre as células.

>[!NOTE]
>
>Algumas propriedades de célula, como Largura e Altura, podem ser definidas como pixels ou como porcentagens.

>[!CAUTION]
>
>A Adobe recomenda que você defina uma largura para a tabela.

#### Propriedades da célula {#cell-properties}

![cq55_rte_cellproperties_icon](assets/cq55_rte_cellproperties_icon.png)

As propriedades de uma célula específica, ou série de células, podem ser configuradas:

![cq55_rte_cellproperties_dialog](assets/cq55_rte_cellproperties_dialog.png)

* **Largura**
* **Altura**
* **Alinhamento Horizontal** - Esquerda, Centro ou Direita
* **Alinhamento Vertical** - Superior, Meio, Inferior ou Linha de Base
* **Tipo de célula**- Dados ou Cabeçalho
* **Aplicar a:** Célula única, Linha inteira, Coluna inteira

#### Adicionar ou Excluir Linhas {#add-or-delete-rows}

![cq55_rte_rows](assets/cq55_rte_rows.png)

As linhas podem ser adicionadas acima ou abaixo da linha atual.

A linha atual também pode ser excluída.

#### Adicionar ou excluir colunas {#add-or-delete-columns}

![cq55_rte_columns](assets/cq55_rte_columns.png)

As colunas podem ser adicionadas à esquerda ou à direita da coluna atual.

A coluna atual também pode ser excluída.

#### Seleção de Linhas ou Colunas Inteiras {#selecting-entire-rows-or-columns}

![chlimage_1-106](assets/chlimage_1-106.png)

Seleciona toda a linha ou coluna atual. Ações específicas (por exemplo, mesclar) ficam disponíveis.

#### Mesclar Células {#merge-cells}

![cq55_rte_cellmerge](assets/cq55_rte_cellmerge.png) ![cq55_rte_cellmerge-1](assets/cq55_rte_cellmerge-1.png)

* Se você selecionou um grupo de células, é possível mesclá-las em um.
* Se você tiver apenas uma célula selecionada, poderá mesclá-la com a célula à direita ou abaixo.

#### Dividir células {#split-cells}

![cq55_rte_cellsplit](assets/cq55_rte_cellsplit.png)

Selecione uma única célula para dividi-la:

* Dividir uma célula horizontalmente gerará uma nova célula à direita da célula atual, dentro da coluna atual.
* Dividir uma célula verticalmente gerará uma nova célula abaixo da célula atual, mas dentro da linha atual.

#### Criação de Tabelas Aninhadas {#creating-nested-tables}

![chlimage_1-107](assets/chlimage_1-107.png)

A criação de uma tabela aninhada cria uma tabela independente dentro da célula atual.

>[!NOTE]
>
>Alguns comportamentos adicionais dependem do navegador:
>
>* Windows IE: Use Ctrl+primary-mouse-button-click (geralmente à esquerda) para selecionar várias células.
>* Firefox: arraste o ponteiro para selecionar um intervalo de células.

#### Remover tabela {#remove-table}

![cq55_rte_removetable](assets/cq55_rte_removetable.png)

Use a opção para remover a tabela do componente **[!UICONTROL Texto]**.

### Caracteres especiais {#special-characters}

![Barra de ferramentas de caracteres especiais](do-not-localize/cq55_rte_specialchars.png)

Caracteres especiais podem ser disponibilizados para o editor de rich text; eles podem variar de acordo com a sua instalação.

![cq55_rte_specialchars_use](assets/cq55_rte_specialchars_use.png)

Use o mouse sobre ele para ver uma versão ampliada do caractere, em seguida, clique para que ele seja incluído no local atual em seu texto.

### Modo de edição do Source {#source-editing-mode}

![barra de ferramentas do modo de edição do Source](do-not-localize/cq55_rte_sourceedit.png)

O modo de edição de origem permite visualizar e editar o HTML subjacente do componente.

Assim, o texto:

![cq55_rte_sourcemode_1](assets/cq55_rte_sourcemode_1.png)

Será a seguinte aparência no modo de origem (geralmente, a origem é muito mais longa, portanto, você terá que rolar a tela):

![cq55_rte_sourcemode_2](assets/cq55_rte_sourcemode_2.png)

>[!CAUTION]
>
>Ao sair do modo de origem, o AEM faz determinadas verificações de validação (por exemplo, garantir que o texto esteja corretamente contido/aninhado em blocos). Isso pode resultar em alterações nas edições.
