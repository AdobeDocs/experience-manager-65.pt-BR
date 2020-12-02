---
title: Editor de Rich Text
description: O Editor de Rich Text é um elemento básico fundamental para introduzir o conteúdo textual no AEM.
uuid: 4bcce45a-e14f-41b7-8c6f-89d1e1bb595c
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: ccc0e434-8847-4e12-8a18-84b55fb2964b
docset: aem65
translation-type: tm+mt
source-git-commit: 7bf6657a8fd7677ab15e0f91324a065b684e2f92
workflow-type: tm+mt
source-wordcount: '1801'
ht-degree: 77%

---


# Rich Text Editor {#rich-text-editor}

O Editor de Rich Text é um elemento básico fundamental para introduzir o conteúdo textual no AEM. É a base de vários componentes, incluindo:

* Texto
* Imagem de texto
* Tabela

## Editor de Rich Text {#rich-text-editor-1}

A caixa de diálogo de edição WYSIWYG fornece uma grande variedade de funcionalidades:

![cq55_rte_basicchars](assets/cq55_rte_basicchars.png)

>[!NOTE]
>
>Os recursos disponíveis podem ser configurados para projetos individuais, por isso podem variar de acordo com a sua instalação.

## Edição no local {#in-place-editing}

Além do diálogo com base no modo de Edição de Rich Text, o AEM também fornece o modo de edição local, o qual permite a edição direta do texto enquanto é exibido no layout da página.

Clique duas vezes em um parágrafo (um clique duplo lento) para entrar no modo de edição local (a borda do componente fica laranja).

Você poderá editar o texto diretamente na página, em vez de dentro de uma janela de diálogo. Basta fazer as alterações e elas serão salvas automaticamente.

![cq55_rte_inlineediting](assets/cq55_rte_inlineediting.png)

>[!NOTE]
>
>Se o localizador de conteúdo estiver aberto, uma barra de ferramentas com as opções de formatação do ERT será exibida na parte superior da guia (como mostrado acima).
>
>A barra de ferramentas não será exibida se o localizador de conteúdo não estiver aberto.

No momento, o modo de Edição local está habilitado para elementos de página gerados pelos componentes de **Texto** e **Título**.

>[!NOTE]
>
>O componente [!UICONTROL Título] foi projetado para conter um texto curto se quebras de linha. Ao editar um título no Modo de edição no local, inserir uma quebra de linha abrirá um novo componente de **Texto** abaixo do título.

## Recursos do Editor de Rich Text {#features-of-the-rich-text-editor}

O Editor de Rich Text fornece vários recursos, esses [dependem da configuração](/help/sites-administering/rich-text-editor.md) do componente individual. Os recursos estão disponíveis para a interface otimizada ao toque e clássica.

### Formatos básicos de caracteres {#basic-character-formats}

![](do-not-localize/cq55_rte_basicchars.png)

Aqui, é possível aplicar a formatação aos caracteres selecionados (destacados); algumas opções também têm teclas de atalho:

* Negrito (Ctrl+B)
* Itálico (Ctrl+I)
* Sublinhado (Ctrl+U)
* Subscrito
* Sobrescrito

![cq55_rte_basicchars_use](assets/cq55_rte_basicchars_use.png)

Todos funcionam como uma alternância, assim, selecionar novamente removerá o formato.

### Estilos e formatos pré-definidos {#predefined-styles-and-formats}

![cq55_rte_stylesparágrafo](assets/cq55_rte_stylesparagraph.png)

Sua instalação pode incluir estilos e formatos predefinidos. Estão disponíveis com as listas suspensas de **[!UICONTROL estilo]** e **[!UICONTROL formato]** e podem ser aplicados ao texto selecionado.

Um estilo pode ser aplicado a uma sequência específica (um estilo correlaciona-se com CSS):

![cq55_rte_styles_use](assets/cq55_rte_styles_use.png)

Considerando que um formato é aplicado a todo o parágrafo do texto (um formato é baseado em HTML):

![cq55_rte_parameter_use](assets/cq55_rte_paragraph_use.png)

Um formato específico pode ser apenas alterado (o padrão é **[!UICONTROL Parágrafo]**).

Um estilo pode ser removido; coloque o cursor dentro do texto ao qual o estilo foi aplicado e clique no ícone para remover:

>[!CAUTION]
>
>Não selecione novamente nenhuma parte do texto ao qual o estilo foi aplicado ou, o ícone será desativado.

### Cortar, copiar, colar {#cut-copy-paste}

![](do-not-localize/cq55_rte_cutcopypaste.png)

As funções padrão de **[!UICONTROL recortar]** e **[!UICONTROL copiar]** estão disponíveis. Vários tipos da função **[!UICONTROL colar]** são fornecidos para atender a diferentes formatos.

* Cortar (Ctrl-X)
* Copiar (Ctrl-C)
* Colar
Este é o mecanismo de colagem padrão (Ctrl-V) para o componente; quando instalado e pronto, isso é configurado para ser [!UICONTROL Colar do Word].

* Colar como texto: Remove todos os estilos e formatação para colar apenas o texto sem formatação.

* Colar do Word: Isso cola o conteúdo como HTML (com alguma reformatação necessária).

### Desfazer, refazer {#undo-redo}

![](do-not-localize/cq55_rte_undoredo.png)

O AEM mantém um registro de suas últimas 50 ações no componente atual, mantidas em ordem cronológica. Essas ações podem ser desfeitas (e, em seguida, refeitas), em ordem rigorosa, se necessário.

>[!CAUTION]
>
>O histórico é mantido somente para a sessão de edição atual. Ele é reiniciado sempre que você abrir o componente para edição.

>[!NOTE]
>
>Cinquenta é o número padrão de tarefas. Isso pode ser diferente para a sua instalação.

### Alinhamento {#alignment}

![](do-not-localize/cq55_rte_alignment.png)

O texto pode ser alinhado na esquerda, centralizado ou na direita.

![cq55_rte_alignment_use](assets/cq55_rte_alignment_use.png)

### Recuo {#indentation}

![](do-not-localize/cq55_rte_indent.png)

O recuo de margem de um parágrafo pode ser aumentado ou diminuído. O parágrafo selecionado será recuado, qualquer novo texto inserido manterá o nível atual de recuo de margem.

![cq55_rte_native_use](assets/cq55_rte_indent_use.png)

### Listas {#lists}

![](do-not-localize/cq55_rte_lists.png)

As listas com marcadores e numeradas podem ser criadas dentro do texto. Selecione o tipo de lista e comece a digitar ou destaque o texto a ser convertido. Em ambos os casos, um avanço de linha iniciará um novo item da lista.

Para listas aninhadas, recue um ou mais itens da lista.

Para alterar o estilo de uma lista, basta posicionar o cursor dentro da lista e, em seguida, selecionando o outro estilo. Uma sublista também pode ter um estilo diferente da lista que a contém. Isso pode ser aplicado quando a sublista tiver sido criada (por recuo).

![cq55_rte_lista_use](assets/cq55_rte_lists_use.png)

### Links {#links}

![](do-not-localize/cq55_rte_links.png)

Um link para um URL (dentro do seu site ou de um local externo) é gerado destacando o texto necessário e clicando no ícone de hiperlink:

![](do-not-localize/chlimage_1-9.png)

Uma caixa de diálogo permitirá que você especifique a URL de destino; e se deve também ser aberta em uma nova janela.

![cq55_rte_link_use](assets/cq55_rte_link_use.png)

É possível:

* Digite um URI diretamente
* Usar o mapa do site para selecionar uma página dentro do site
* Digite o URI e anexe a âncora do público alvo; por exemplo, `www.TargetUri.org#AnchorName`
* Insira somente uma âncora (para fazer referência à &quot;página atual&quot;); Por exemplo, `#anchor`
* Procure uma página no localizador de conteúdo e arraste e solte o ícone da página na caixa de diálogo Hiperlink

>[!NOTE]
>
>A URL pode ser anexada a quaisquer protocolos configurados para sua instalação. Em uma instalação padrão, eles são `https://`, `ftp://` e `mailto:`. Os protocolos não configurados para sua instalação são rejeitados e marcados como inválidos.

Para quebrar o link, coloque o cursor em qualquer lugar no texto do link e clique no ícone [!UICONTROL Desvincular]:

![](do-not-localize/chlimage_1-10.png)

### Âncoras {#anchors}

![](do-not-localize/cq55_rte_anchor.png)

Uma âncora pode ser criada em qualquer lugar dentro do texto ao posicionar o cursor ou selecionar algum texto. Em seguida, clique no ícone **âncora** para abrir a caixa de diálogo.

Digite o nome da âncora, em seguida, clique em **OK** para salvar.

![cq55_rte_anchor_use](assets/cq55_rte_anchor_use.png)

A âncora é exibida quando o componente está sendo editado e agora pode ser usada dentro de um destino para os links.

![chlimage_1-104](assets/chlimage_1-104.png)

### Localizar e substituir {#find-and-replace}

![](do-not-localize/cq55_rte_findreplace.png)

O AEM fornece as funções **Localizar** e **Substituir**.

As funções tem um botão **Localizar próximo** para pesquisar o componente aberto para o texto especificado. Também é possível especificar caso precise que a letra (maiúscula/minúscula) coincida.

A pesquisa sempre iniciará da posição atual do cursor dentro do texto. Quando o final do componente for atingido uma mensagem vai informá-lo que a próxima operação de busca começará do início.

![cq55_rte_find_use](assets/cq55_rte_find_use.png)

A opção **Substituir** permite **Localizar** e **Substituir** uma instância individual por um texto especificado, ou **Substituir todas** as instâncias no componente atual.

![cq55_rte_findreplace_use](assets/cq55_rte_findreplace_use.png)

### Imagens {#images}

As imagens podem ser arrastadas do localizador de conteúdo para adicioná-las ao texto.

![cq55_rte_image_use](assets/cq55_rte_image_use.png)

>[!NOTE]
>
>O AEM também oferece componentes especializados para uma configuração mais detalhada da imagem. Os componentes **Imagem** e **Imagem de texto**, por exemplo, estão disponíveis.

### Verificador ortográfico {#spelling-checker}

![](do-not-localize/cq55_rte_spellchecker.png)

O verificador ortográfico vai conferir todo o texto no componente atual.

Quaisquer erros de ortografia serão destacados:

![cq55_rte_spellchecker_use](assets/cq55_rte_spellchecker_use.png)

>[!NOTE]
>
>O verificador ortográfico operará no idioma do site utilizando a propriedade de idioma da subárvore ou extraindo o idioma do URL. Por exemplo, a ramificação `en` será verificada para inglês e a ramificação `de` para alemão.

### Tabelas {#tables}

As tabelas estão disponíveis:

* Como o componente de **Tabela**

   ![chlimage_1-105](assets/chlimage_1-105.png)

* No componente **Texto**

   ![](do-not-localize/chlimage_1-11.png)

   >[!NOTE]
   >
   >Embora as tabelas estejam disponíveis no RTE, recomenda-se usar o componente **Table** ao criar tabelas.

Nos componentes **Texto** e **Tabela** a funcionalidade de tabela está disponível por meio do menu de contexto (normalmente, o botão direito do mouse) clicado na tabela; por exemplo:

![cq55_rte_tablemenu](assets/cq55_rte_tablemenu.png)

>[!NOTE]
>
>No componente **Tabela,** uma barra de ferramentas especializada também está disponível, incluindo várias funções do editor de rich text padrão juntamente com um subconjunto de funções específicas de tabela.

As funções específicas da tabela são:

* [Table Properties](#table-properties)
* [Cell Properties](#cell-properties)
* [Add or Delete Rows](#add-or-delete-rows)
* [Add or Delete Columns](#add-or-delete-columns)
* [Selecting Entire Rows or Columns](#selecting-entire-rows-or-columns)
* [Merge Cells](#merge-cells)
* [Split Cells](#split-cells)
* [Tabelas aninhadas](#creating-nested-tables)
* [Remover tabela](#remove-table)

#### Propriedades da tabela  {#table-properties}

![cq55_rte_tableproperties_icon](assets/cq55_rte_tableproperties_icon.png)

As propriedades básicas da tabela podem ser configuradas antes de clicar em **OK** para salvar:

![cq55_rte_tableproperties_dialog](assets/cq55_rte_tableproperties_dialog.png)

* **Largura**: A largura total da tabela.

* **Altura**: A altura total da tabela.

* **Borda**: O tamanho da borda da tabela.

* **Preenchimento** da célula: Isso define o espaço em branco entre o conteúdo da célula e suas bordas.

* **Espaçamento** da célula: Isso define a distância entre as células.

>[!NOTE]
>
>Algumas propriedades de células, como Largura e Altura, podem ser definidas como pixels ou porcentagens.

>[!CAUTION]
>
>O Adobe recomenda que você defina uma largura para a tabela.

#### Propriedades da célula {#cell-properties}

![cq55_rte_cellproperties_icon](assets/cq55_rte_cellproperties_icon.png)

As propriedades de uma célula específica ou a série de células, podem ser configuradas:

![cq55_rte_cellproperties_dialog](assets/cq55_rte_cellproperties_dialog.png)

* **Largura**
* **Altura**
* **Alinhamento**  horizontal - Esquerda, Centro ou Direita
* **Alinhamento**  vertical - Parte superior, Meio, Parte inferior ou Linha de base
* **Tipo** de célula - Dados ou cabeçalho
* **Aplicar a:célula** única, linha inteira, coluna inteira

#### Adicionar ou excluir linhas {#add-or-delete-rows}

![cq55_rte_lines](assets/cq55_rte_rows.png)

As linhas podem ser adicionadas acima ou abaixo da linha atual.

A linha atual também pode ser excluída.

#### Adicionar ou remover colunas {#add-or-delete-columns}

![cq55_rte_columns](assets/cq55_rte_columns.png)

As colunas podem ser adicionadas à esquerda ou à direita da coluna atual.

A coluna atual também pode ser excluída.

#### Selecionar linhas ou colunas inteiras {#selecting-entire-rows-or-columns}

![chlimage_1-105](assets/chlimage_1-106.png)

Seleciona toda a linha ou coluna atual. As ações específicas (por exemplo, mesclar) estarão, em seguida, disponíveis.

#### Mesclar células {#merge-cells}

![cq55_rte_](assets/cq55_rte_cellmerge.png) ![cellmergecq55_rte_cellmerge-1](assets/cq55_rte_cellmerge-1.png)

* Caso tenha selecionado um grupo de células, você pode mesclá-las em uma.
* Caso tenha apenas uma célula selecionada, então você pode mesclá-la com a célula à direita ou abaixo.

#### Dividir células {#split-cells}

![cq55_rte_cellsplit](assets/cq55_rte_cellsplit.png)

Selecione uma única célula para dividi-la:

* Dividir uma célula horizontalmente vai gerar uma nova célula à direita da célula atual, dentro da coluna atual.
* Dividir uma célula verticalmente vai gerar uma nova célula abaixo da célula atual, mas dentro da linha atual.

#### Creating Nested Tables {#creating-nested-tables}

![chlimage_1-107](assets/chlimage_1-107.png)

Criar uma tabela aninhada criará uma nova tabela autossuficiente, dentro da célula atual.

>[!NOTE]
>
>Certos comportamentos adicionais são dependentes de um navegador:
>
>* IE do Windows: usar o clique do botão do mouse principal + Ctrl (geralmente à esquerda) para selecionar várias células.
>* Firefox: Arraste o ponteiro para selecionar um intervalo de células.


#### Remove Table {#remove-table}

![cq55_rte_removetable](assets/cq55_rte_removetable.png)

Use a opção para remover a tabela do componente **[!UICONTROL Texto]**.

### Caracteres especiais {#special-characters}

![](do-not-localize/cq55_rte_specialchars.png)

Os caracteres especiais podem ser disponibilizados para o seu editor de rich text; podem variar de acordo com a sua instalação.

![cq55_rte_specialchars_use](assets/cq55_rte_specialchars_use.png)

Usar o mouse sobre o caractere para visualizar uma versão ampliada do mesmo, em seguida, clicar para que seja incluído na posição atual em seu texto.

### Modo de edição de fonte {#source-editing-mode}

![](do-not-localize/cq55_rte_sourceedit.png)

O modo de edição da origem permite que você visualize e edite o HTML subjacente do componente.

Assim, o texto:

![cq55_rte_sourcemode_1](assets/cq55_rte_sourcemode_1.png)

Será como o modo de origem (muitas vezes a origem é muito longa, então será necessário usar a barra de rolagem):

![cq55_rte_sourcemode_2](assets/cq55_rte_sourcemode_2.png)

>[!CAUTION]
>
>Ao sair do modo de origem, o AEM fará certas verificações de validação (por exemplo, garantindo que o texto está corretamente contido/aninhado em blocos). Isso pode resultar em mudanças para as suas edições.
