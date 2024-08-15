---
title: Console de marcação da interface clássica
description: Saiba mais sobre o Console de marcação da interface do usuário do Adobe Experience Manager Classic.
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
docset: aem65
exl-id: 8c6ba22f-5555-4e3c-998a-9353bd44715b
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 1%

---


# Console de marcação da interface clássica{#classic-ui-tagging-console}

Esta seção é para o Console de marcação da interface do usuário clássica.

>[!NOTE]
>
>Consulte [Administração de Tags](/help/sites-administering/tags.md#tagging-console) para obter detalhes do Console de Marcação da Interface do Usuário Otimizada para Toque.

Para acessar o console de Marcação da Interface Clássica:

* no autor
* entrar com privilégios administrativos
* navegar até o console
por exemplo, [https://localhost:4502/tagging](https://localhost:4502/tagging)

![Janela do console clássico](assets/managing_tags_usingthetagasministrationconsole.png)

## Criação de tags e namespaces {#creating-tags-and-namespaces}

1. Dependendo do nível a partir do qual você está começando, é possível criar uma marca ou um namespace usando **Novo**:

   Se você selecionar **Marcas**, será possível criar um namespace:

   ![Criando uma caixa de diálogo de namespace](assets/creating_tags_andnamespaces.png)

   Se você selecionar um namespace (por exemplo, **Demonstração**), será possível criar uma marca dentro desse namespace:

   ![Criando uma caixa de diálogo de marca](assets/creating_tags_andnamespacesinnewnamespace.png)

1. Em ambos os casos, insira

   * **Título**
(*Obrigatório*) O título de exibição da marca. Embora qualquer caractere possa ser inserido,
é recomendável não usar estes caracteres especiais:

      * `colon (:)` - delimitador de namespace
      * `forward slash (/)` - delimitador de submarca

     Esses caracteres não serão exibidos se inseridos.

   * **Nome**
(*Obrigatório*) O nome do nó da marca.

   * **Descrição**
(*Opcional*) Uma descrição para a marca.

   * selecione **Criar**

## Edição de tags {#editing-tags}

1. No painel direito, selecione a tag que deseja editar.
1. Clique em **Editar**.
1. Você pode modificar o **Título** e a **Descrição**.
1. Clique em **Salvar** para fechar a caixa de diálogo.

## Exclusão de tags {#deleting-tags}

1. No painel direito, selecione a tag que deseja excluir.
1. Clique em **Excluir**.
1. Clique em **Sim** para fechar a caixa de diálogo.

   A tag não deve mais ser listada.

## Ativação e desativação de tags {#activating-and-deactivating-tags}

1. No painel direito, selecione o namespace ou a tag que deseja ativar (publicar) ou desativar (cancelar a publicação).
1. Clique em **Ativar** ou **Desativar** conforme necessário.

## Lista - mostrando onde as tags são referenciadas {#list-showing-where-tags-are-referenced}

**Lista** abre uma nova janela mostrando os caminhos de todas as páginas usando a marca realçada:

![Localizando onde as marcas são referenciadas](assets/list_showing_wheretagsarereferenced.png)

## Mover tags {#moving-tags}

Para ajudar os administradores e desenvolvedores de tags a limpar a taxonomia ou renomear uma ID de tag, é possível mover uma tag para um novo local:

1. Abra o console **Marcação**.
1. Selecione a marca e clique em **Mover...** na barra de ferramentas superior (ou no menu de contexto).
1. Na caixa de diálogo **Mover Marca**, defina:

   * **a**, o nó de destino.
   * **Renomear para**, o novo nome de nó.

1. Clique em **Mover**.

A caixa de diálogo **Mover Marca** tem esta aparência:

![Movendo uma marca](assets/move_tag.png)

>[!NOTE]
>
>Os autores não devem mover tags ou renomear uma ID de tag. Quando necessário, os Autores devem [alterar apenas os títulos das marcas](#editing-tags).

## Mesclar tags {#merging-tags}

A mesclagem de tags pode ser usada quando uma taxonomia tem duplicatas. Quando a tag A é mesclada à tag B, todas as páginas marcadas com a tag A são marcadas com a tag B e a tag A não está mais disponível para os autores.

Para mesclar uma tag a outra:

1. Abra o console **Marcação**.
1. Selecione a marca e clique em **Mesclar...** na barra de ferramentas superior (ou no menu de contexto).
1. Na caixa de diálogo **Mesclar Marca**, defina:

   * **em**, o nó de destino.

1. Clique em **Mesclar**.

A caixa de diálogo **Mesclar Marca** tem esta aparência:

![Mesclando uma marca](assets/mergetag.png)

## Contagem do uso de tags {#counting-usage-of-tags}

Para ver quantas vezes uma tag está sendo usada:

1. Abra o console **Marcação**.
1. Clique em **Uso da contagem** na barra de ferramentas superior: a coluna Contagem exibe o resultado.

## Gerenciamento de tags em diferentes idiomas {#managing-tags-in-different-languages}

A propriedade `title` opcional de uma tag pode ser traduzida em vários idiomas. A tag `titles` pode ser exibida de acordo com o idioma do usuário ou da página.

### Definição de títulos de tag em vários idiomas {#defining-tag-titles-in-multiple-languages}

O procedimento a seguir mostra como traduzir os `title`da marca **Animais** para inglês, alemão e francês:

1. Vá para o console **Marcação**.
1. Edite a marca **Animais** abaixo de **Marcas** > **Banco de Fotografia**.
1. Adicione as traduções nos seguintes idiomas:

   * **Inglês**: Animais
   * **Alemão**: Tiere
   * **Francês**: Animaux

1. Salve as alterações.

A caixa de diálogo tem a seguinte aparência:

![Editando uma marca](assets/edit_tag.png)

O console Marcação usa a configuração de idioma do usuário, portanto, para a tag Animal, &quot;Animaux&quot; é exibido para um usuário que define o idioma para francês nas propriedades do usuário.

Para adicionar um novo idioma à caixa de diálogo, consulte a seção [Adicionando um Novo Idioma à Caixa de Diálogo Editar Marca](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) na seção **Marcação para Desenvolvedores**.

### Exibição de títulos de tag em propriedades de página em um idioma especificado {#displaying-tag-titles-in-page-properties-in-a-specified-language}

Por padrão, a tag `titles` nas propriedades da página é exibida no idioma da página. A caixa de diálogo de marcas nas propriedades da página tem um campo de idioma que permite a exibição da marca `titles` em um idioma diferente. O procedimento a seguir descreve como exibir a tag `titles` em francês:

1. Consulte a seção anterior para adicionar a tradução em francês aos **Animais** abaixo de **Marcas** > **Estoque de Fotografia**.
1. Abra as propriedades da página **Produtos** na ramificação em inglês do site **Geometrixx**.
1. Abra a caixa de diálogo **Marcas/Palavras-chave** (selecionando o menu suspenso à direita da área de exibição Marcas/Palavras-chave) e selecione o idioma **Francês** no menu suspenso no canto inferior direito.
1. Role usando as setas para a esquerda e para a direita até poder selecionar a guia **Stock Photography**

   Selecione a marca **Animais** (**Animaux**) e selecione fora da caixa de diálogo para fechá-la e adicionar a marca às propriedades da página.

   ![Editando outra marca](assets/french_tag.png)

Por padrão, a caixa de diálogo Propriedades da página exibe a tag `titles` de acordo com o idioma da página.

Em geral, o idioma da tag é retirado do idioma da página se o idioma da página estiver disponível. Quando o widget [`tag` ](/help/sites-developing/building.md#tagging-on-the-client-side) é usado em outros casos (por exemplo, em formulários ou caixas de diálogo), o idioma da marca depende do contexto.

>[!NOTE]
>
>A nuvem de tags e as metapalavras-chave no componente de página padrão usam a tag localizada `titles` com base no idioma da página, se disponível.
