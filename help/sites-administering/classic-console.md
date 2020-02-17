---
title: Console de marcação da interface clássica
seo-title: Console de marcação da interface clássica
description: Saiba mais sobre o console de marcação da interface clássica.
seo-description: Saiba mais sobre o console de marcação da interface clássica.
uuid: 51e29422-f967-424b-a7fd-4ca2ddc6b8a3
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: b279c033-bc93-4e62-81ad-123c40b9fdd2
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# Console de marcação da interface clássica{#classic-ui-tagging-console}

Esta seção é para o console de marcação da interface clássica.

O console de marcação da interface otimizada para toque está [aqui](/help/sites-administering/tags.md#tagging-console).

Para acessar o console Marcação de interface clássica:

* sobre o autor
* fazer logon com privilégios administrativos
* navegue até o console, por exemplo, [https://localhost:4502/tagging](https://localhost:4502/tagging)

![](assets/managing_tags_usingthetagasministrationconsole.png)

## Criação de tags e namespaces {#creating-tags-and-namespaces}

1. Dependendo do nível a partir do qual você está começando, é possível criar uma tag ou um namespace usando **Novo**:

   Se você selecionar **Tags** , poderá criar um namespace:

   ![](assets/creating_tags_andnamespaces.png)

   Se você selecionar um namespace (por exemplo, **Demonstração**), poderá criar uma tag nesse namespace:

   ![](assets/creating_tags_andnamespacesinnewnamespace.png)

1. Em ambos os casos, informe

   * **Título**(*obrigatório*) O título de exibição da tag . Embora qualquer caractere possa ser inserido, recomenda-se não usar esses caracteres especiais:

      * `colon (:)` - delimitador de namespace
      * `forward slash (/)` - delimitador de subtags
      Esses caracteres não serão exibidos se forem inseridos.

   * **Nome**(*obrigatório*) O nome do nó da tag.

   * **Descrição**(*Opcional*) Uma descrição da tag.

   * select **Create**


## Edição de tags {#editing-tags}

1. No painel direito, selecione a tag que deseja editar.
1. Clique em **Editar**.
1. É possível modificar o **Título** e a **Descrição**.
1. Clique em **Salvar** para fechar a caixa de diálogo.

## Excluindo tags {#deleting-tags}

1. No painel direito, selecione a tag que deseja excluir.
1. Clique em **Excluir**.
1. Clique em **Sim** para fechar a caixa de diálogo.

   A tag não deve mais ser listada.

## Ativação e desativação de tags {#activating-and-deactivating-tags}

1. No painel direito, selecione o namespace ou a tag que deseja ativar (publicar) ou desativar (cancelar a publicação).
1. Clique em **Ativar** ou em **Desativar** , conforme necessário.

## Lista - mostrar onde as tags são referenciadas {#list-showing-where-tags-are-referenced}

**A lista** abre uma nova janela mostrando os caminhos de todas as páginas usando a tag realçada:

![](assets/list_showing_wheretagsarereferenced.png)

## Mover tags {#moving-tags}

Para ajudar os administradores e desenvolvedores de tags a limpar a taxonomia ou renomear uma ID de tag, é possível mover uma tag para um novo local:

1. Open the **Tagging** console.
1. **Selecione a tag e clique em** Mover... na barra de ferramentas superior (ou no menu de contexto).
1. Na caixa de diálogo **Mover tag** , defina:

   * **para**, o nó de destino.
   * **Renomeie para**, o novo nome do nó.

1. Clique em **Mover**.

A caixa de diálogo **Mover tag** é a seguinte:

![](assets/move_tag.png)

>[!NOTE]
>
>Os autores não devem mover tags nem renomear uma ID de tag. Quando necessário, os Autores devem apenas [alterar os títulos](#editing-tags)das tags.

## Mesclar tags {#merging-tags}

A mesclagem de tags pode ser usada quando uma taxonomia tem duplicatas. Quando a tag A é unida à tag B, todas as páginas marcadas com a tag A serão marcadas com a tag B e a tag A não estará mais disponível para os autores.

Para unir uma tag a outra:

1. Open the **Tagging** console.
1. **Selecione a tag e clique em** Mesclar... na barra de ferramentas superior (ou no menu de contexto).
1. Na caixa de diálogo **Mesclar tag** , defina:

   * **no** nó de destino.

1. Clique em **Mesclar**.

A caixa de diálogo **Mesclar tag** é exibida da seguinte maneira:

![](assets/mergetag.png)

## Contagem de uso de tags {#counting-usage-of-tags}

Para ver quantas vezes uma tag está sendo usada:

1. Open the **Tagging** console.
1. Clique em **Contar uso** na barra de ferramentas superior: a contagem de colunas exibe o resultado.

## Gerenciamento de tags em diferentes idiomas {#managing-tags-in-different-languages}

A `title`propriedade opcional de uma tag pode ser traduzida para vários idiomas. A tag `titles` pode ser exibida de acordo com o idioma do usuário ou com o idioma da página.

### Definição de títulos de tag em vários idiomas {#defining-tag-titles-in-multiple-languages}

O procedimento a seguir mostra como traduzir o `title`da tag **Animais** para inglês, alemão e francês:

1. Go to the **Tagging** console.
1. Edite a tag **Animais** abaixo de **Tags** > Fotografia **** de estoque.
1. Adicione as traduções nos seguintes idiomas:

   * **Inglês**: Animais
   * **Alemão**: Tiere
   * **Francês**: Animaux

1. Salve as alterações.

A caixa de diálogo tem a seguinte aparência:

![](assets/edit_tag.png)

O console Marcação usa a configuração de idioma do usuário, portanto, para a tag Animal, &quot;Animaux&quot; é exibido para um usuário que define o idioma como francês nas propriedades do usuário.

Para adicionar um novo idioma à caixa de diálogo, consulte a seção [Adicionar um novo idioma à caixa de diálogo](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) Editar tag na seção **Marcação para desenvolvedores** .

### Exibição de títulos de tag nas propriedades da página em um idioma especificado {#displaying-tag-titles-in-page-properties-in-a-specified-language}

Por padrão, a tag `titles`nas propriedades da página é exibida no idioma da página. A caixa de diálogo da tag nas propriedades da página tem um campo de idioma que permite a exibição da tag `titles`em um idioma diferente. O procedimento a seguir descreve como exibir a tag `titles`em francês:

1. Consulte a seção anterior para adicionar a tradução em francês aos **Animais** abaixo de **Tags** > Fotografia **de** estoque.
1. Abra as propriedades da página **Produtos** na ramificação em inglês do site **Geometrixx** .
1. Abra a caixa de diálogo **Tags/Palavras-chave** (selecionando o menu suspenso à direita da área de exibição Tags/Palavras-chave) e selecione o idioma **francês** no menu suspenso no canto inferior direito.
1. Role usando as setas para a esquerda e para a direita até selecionar a guia Fotografia **do** Stock

   Selecione a tag **Animais** (**Animaux**) e selecione fora da caixa de diálogo para fechá-la e adicionar a tag às propriedades da página.

   ![](assets/french_tag.png)

Por padrão, a caixa de diálogo Propriedades da página exibe a tag de `titles`acordo com o idioma da página.

Em geral, o idioma da tag será retirado do idioma da página se o idioma da página estiver disponível. Quando o [`tag` widget](/help/sites-developing/building.md#tagging-on-the-client-side) é usado em outros casos (por exemplo, em formulários ou em caixas de diálogo), a linguagem da tag depende do contexto.

>[!NOTE]
>
>A nuvem de tags e as palavras-chave meta no componente de página padrão usam a tag localizada `titles`com base no idioma da página, se disponível.