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
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 1%

---


# Console de marcação da interface clássica{#classic-ui-tagging-console}

Esta seção é para o Console de marcação da interface do usuário clássica.

O console de marcação da interface otimizada para toque é [aqui](/help/sites-administering/tags.md#tagging-console).

Para acessar o console de Marcação da Interface Clássica:

* no autor
* entrar com privilégios administrativos
* navegue até o console, por exemplo, [https://localhost:4502/tagging](https://localhost:4502/tagging)

![Janela do console clássico](assets/managing_tags_usingthetagasministrationconsole.png)

## Criação de tags e namespaces {#creating-tags-and-namespaces}

1. Dependendo do nível a partir do qual você está começando, é possível criar uma tag ou um namespace usando **Novo**:

   Se você selecionar **Tags** você pode criar um namespace:

   ![Caixa de diálogo Criando um namespace](assets/creating_tags_andnamespaces.png)

   Se você selecionar um namespace (por exemplo, **Demonstração**), você pode criar uma tag nesse namespace:

   ![Caixa de diálogo Criação de uma tag](assets/creating_tags_andnamespacesinnewnamespace.png)

1. Em ambos os casos, insira

   * **Título**
(*Obrigatório*) O título de exibição da tag. Embora qualquer caractere possa ser inserido, é recomendável não usar estes caracteres especiais:

      * `colon (:)` - delimitador de namespace
      * `forward slash (/)` - delimitador de submarca

     Esses caracteres não serão exibidos se inseridos.

   * **Nome**
(*Obrigatório*) O nome do nó da tag.

   * **Descrição**
(*Opcional*) Uma descrição para a tag.

   * selecionar **Criar**

## Edição de tags {#editing-tags}

1. No painel direito, selecione a tag que deseja editar.
1. Clique em **Editar**.
1. Você pode modificar a variável **Título** e a variável **Descrição**.
1. Clique em **Salvar** para fechar o diálogo.

## Exclusão de tags {#deleting-tags}

1. No painel direito, selecione a tag que deseja excluir.
1. Clique em **Excluir**.
1. Clique em **Sim** para fechar o diálogo.

   A tag não deve mais ser listada.

## Ativação e desativação de tags {#activating-and-deactivating-tags}

1. No painel direito, selecione o namespace ou a tag que deseja ativar (publicar) ou desativar (cancelar a publicação).
1. Clique em **Ativar** ou **Desativar** conforme necessário.

## Lista - mostrando onde as tags são referenciadas {#list-showing-where-tags-are-referenced}

**Lista** abre uma nova janela mostrando os caminhos de todas as páginas usando a tag destacada:

![Localização de onde as tags são referenciadas](assets/list_showing_wheretagsarereferenced.png)

## Mover tags {#moving-tags}

Para ajudar os administradores e desenvolvedores de tags a limpar a taxonomia ou renomear uma ID de tag, é possível mover uma tag para um novo local:

1. Abra o **Marcação** console.
1. Selecione a tag e clique em **Mover...** na barra de ferramentas superior (ou no menu de contexto).
1. No **Mover tag** defina:

   * **para**, o nó de destino.
   * **Renomear para**, o novo nome do nó.

1. Clique em **Mover**.

A variável **Mover tag** tem a seguinte aparência:

![Mover uma tag](assets/move_tag.png)

>[!NOTE]
>
>Os autores não devem mover tags ou renomear uma ID de tag. Quando necessário, os autores devem apenas [alterar os títulos das tags](#editing-tags).

## Mesclar tags {#merging-tags}

A mesclagem de tags pode ser usada quando uma taxonomia tem duplicatas. Quando a tag A é mesclada à tag B, todas as páginas marcadas com a tag A são marcadas com a tag B e a tag A não está mais disponível para os autores.

Para mesclar uma tag a outra:

1. Abra o **Marcação** console.
1. Selecione a tag e clique em **Mesclar...** na barra de ferramentas superior (ou no menu de contexto).
1. No **Mesclar tag** defina:

   * **em**, o nó de destino.

1. Clique em **Mesclar**.

A variável **Mesclar tag** tem a seguinte aparência:

![Mesclar uma tag](assets/mergetag.png)

## Contagem do uso de tags {#counting-usage-of-tags}

Para ver quantas vezes uma tag está sendo usada:

1. Abra o **Marcação** console.
1. Clique em **Uso da contagem** na barra de ferramentas superior: a coluna Count exibe o resultado.

## Gerenciamento de tags em diferentes idiomas {#managing-tags-in-different-languages}

O modelo opcional `title`A propriedade de uma tag pode ser traduzida em vários idiomas. Tag `titles` podem ser exibidos de acordo com o idioma do usuário ou da página.

### Definição de títulos de tag em vários idiomas {#defining-tag-titles-in-multiple-languages}

O procedimento a seguir mostra como traduzir o `title`da tag **Animais** para inglês, alemão e francês:

1. Vá para a **Marcação** console.
1. Editar a tag **Animais** abaixo **Tags** > **Banco de imagens**.
1. Adicione as traduções nos seguintes idiomas:

   * **Inglês**: Animais
   * **Alemão**: Camada
   * **Francês**: Animaux

1. Salve as alterações.

A caixa de diálogo tem a seguinte aparência:

![Edição de uma tag](assets/edit_tag.png)

O console Marcação usa a configuração de idioma do usuário, portanto, para a tag Animal, &quot;Animaux&quot; é exibido para um usuário que define o idioma para francês nas propriedades do usuário.

Para adicionar um novo idioma ao diálogo, consulte a seção [Adicionar um novo idioma à caixa de diálogo Editar tag](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) no **Marcação para desenvolvedores** seção.

### Exibição de títulos de tag em propriedades de página em um idioma especificado {#displaying-tag-titles-in-page-properties-in-a-specified-language}

Por padrão, a tag `titles`nas propriedades da página são exibidas no idioma da página. A caixa de diálogo da tag nas propriedades da página tem um campo de idioma que permite a exibição da tag `titles`em um idioma diferente. O procedimento a seguir descreve como exibir a tag `titles`em francês:

1. Consulte a seção anterior para adicionar a tradução em francês à **Animais** abaixo **Tags** > **Banco de imagens**.
1. Abra as propriedades de página do **Produtos** página na ramificação em inglês da **Geometrixx** local.
1. Abra o **Tags/Palavras-chave** (selecionando o menu suspenso à direita da área de exibição Tags/Palavras-chave) e selecione a caixa **Francês** idioma no menu suspenso no canto inferior direito.
1. Role usando as setas para a esquerda e para a direita até poder selecionar a variável **Banco de imagens** guia

   Selecione o **Animais** (**Animaux**) e selecione fora da caixa de diálogo para fechá-la e adicionar a tag às propriedades da página.

   ![Edição de outra tag](assets/french_tag.png)

Por padrão, a caixa de diálogo Propriedades da página exibe a tag `titles`de acordo com o idioma da página.

Em geral, o idioma da tag é retirado do idioma da página se o idioma da página estiver disponível. Quando a variável [`tag` widget](/help/sites-developing/building.md#tagging-on-the-client-side) for usada em outros casos (por exemplo, em formulários ou caixas de diálogo), o idioma da tag dependerá do contexto.

>[!NOTE]
>
>A nuvem de tags e as metapalavras-chave no componente de página padrão usam a tag localizada `titles`com base no idioma da página, se disponível.
