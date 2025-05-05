---
title: Administração de tags
description: Saiba como gerenciar e administrar tags na Adobe Experience Manager.
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
exl-id: ff041ef0-e566-4373-818e-76680ff668d8
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1769'
ht-degree: 2%

---

# Administração de tags {#administering-tags}

As tags são um método rápido e fácil de classificar conteúdo em um site. Elas podem ser consideradas palavras-chave ou rótulos (metadados) que permitem que o conteúdo seja encontrado mais rapidamente como resultado de uma pesquisa.

No Adobe Experience Manager (AEM), uma tag pode ser uma propriedade de

* um nó de conteúdo para uma página (consulte [Usando Tags](/help/sites-authoring/tags.md))

* um nó de metadados para um ativo (consulte [Gerenciamento de metadados para Assets Digital](/help/assets/metadata.md))

Além de páginas e ativos, as tags são usadas para recursos do AEM Communities

* conteúdo gerado pelo usuário (consulte [Marcação UGC)](/help/communities/tag-ugc.md)

* Recursos de ativação (consulte [Marcação de recursos de ativação](/help/communities/functions.md#catalog-function))

## Recursos de tag {#tag-features}

Alguns dos recursos das tags no AEM incluem:

* As tags podem ser agrupadas em vários namespaces. Essas hierarquias permitem que taxonomias sejam criadas. Essas taxonomias são globais por todo o AEM.
* A restrição principal para tags recém-criadas é que elas devem ser exclusivas em um namespace específico.
* O título de uma tag não deve incluir caracteres de separação de caminho de tag (nem eles serão exibidos, se presentes)

   * dois pontos `:` - delimita a marca de namespace
   * barra `/` - delimita submarcas

* As tags podem ser aplicadas por autores e visitantes do site. Independentemente do criador, todas as formas de tags são disponibilizadas para seleção, tanto ao atribuir a uma página quanto ao pesquisar.
* As marcas podem ser criadas e sua taxonomia modificada por membros do grupo &quot;administradores de marcas&quot; e membros que tenham direitos de modificação para `/content/cq:tags`.

   * Uma tag que contém tags secundárias é chamada de tag de container
   * Uma tag que não é uma tag container é chamada de tag folha
   * Um namespace de tag é uma tag folha ou container

* As marcas são usadas pelo [componente de Pesquisa](https://helpx.adobe.com/experience-manager/core-components/using/quick-search.html) para facilitar a localização do conteúdo.
* As marcas são usadas pelo [componente de Teaser](https://helpx.adobe.com/experience-manager/core-components/using/teaser.html), que monitora a nuvem de marcas de um usuário para fornecer conteúdo direcionado.
* Se a marcação for um aspecto importante do seu conteúdo

   * empacotar tags com as páginas que as usam
   * verifique se as [permissões de tag](#setting-tag-permissions) habilitam o acesso de leitura

## Console de marcação {#tagging-console}

O console Marcação é usado para criar e gerenciar tags e suas taxonomias. Um objetivo é evitar ter muitas tags semelhantes relacionadas basicamente à mesma coisa: por exemplo, páginas e páginas ou calçados e sapatos.

As tags são gerenciadas por meio do agrupamento em namespaces, da revisão do uso de tags existentes antes da criação de novas e da reorganização sem desconectar a tag do conteúdo referenciado no momento.

Para acessar o console de Marcação:

* no autor
* entrar com privilégios administrativos
* da navegação global

   * selecionar **`Tools`**
   * selecionar **`General`**
   * selecionar **`Tagging`**

![managing_tags_usingthetagasministrationconsole](assets/managing_tags_usingthetagasministrationconsolea.png)

### Criar um namespace {#creating-a-namespace}

Para criar um namespace, selecione o ícone **`Create Namespace`**.

O namespace é em si uma tag e não contém nenhuma subtag. No entanto, para continuar criando uma taxonomia, [crie submarcas](#creating-tags), que por sua vez podem ser marcas de folha ou marcas de contêiner.

![chlimage_1-183](assets/chlimage_1-183a.png) ![creating_tags_andnamespaces](assets/creating_tags_andnamespacesa.png)

* **Título**
  *(obrigatório)* Um título de exibição para o namespace.

* **Nome**
  *(opcional)* Um nome para o namespace. Se não for especificado, um nome de nó válido será criado a partir do Título. Consulte [TagID](/help/sites-developing/framework.md#tagid).

* **Descrição**
  *(opcional)* Uma descrição do namespace.

Quando as informações necessárias forem inseridas

* selecione **Criar**

### Operações em tags {#operations-on-tags}

Selecionar um namespace ou outra tag disponibiliza as seguintes operações:

* [Propriedades da exibição](#viewing-tag-properties)
* [Referências](#showing-tag-references)
* [Criar tag](#creating-tags)
* [Editar](#editing-tags)
* [Mover](#moving-tags)
* [Mesclar](#merging-tags)
* [Publicação](#publishing-tags)
* [Desfazer publicação](#unpublishing-tags)
* [Excluir](#deleting-tags)

![chlimage_1-184](assets/chlimage_1-184.png)

Quando a janela do navegador não é larga o suficiente para exibir todos os ícones, os ícones mais à direita são agrupados sob um ícone **`... More`**, que exibirá uma lista suspensa dos ícones de operação ocultos quando selecionados.

![chlimage_1-185](assets/chlimage_1-185.png)

### Selecionar uma tag de namespace {#selecting-a-namespace-tag}

Quando selecionado pela primeira vez, se o namespace não contiver tags, as propriedades serão exibidas à direita; caso contrário, as tags secundárias serão exibidas. Cada tag selecionada exibirá as tags que contém ou suas propriedades se não tiver tags secundárias.

Para selecionar a tag para operações e para várias seleções, selecione somente o ícone ao lado do título. Selecionar o título exibirá somente as propriedades ou abrirá a tag para exibir seu conteúdo.

![chlimage_1-186](assets/chlimage_1-186.png) ![chlimage_1-187](assets/chlimage_1-187.png)

### Exibição das propriedades da tag {#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

Quando um namespace ou outra marca é selecionada, selecionar o ícone **`View Properties`** resulta na exibição de informações sobre `name`, hora da última edição e número de referências. Se publicado, são mostradas a hora em que foi publicado pela última vez e a ID do editor. Essas informações serão exibidas em uma coluna à esquerda das colunas de tag.

![chlimage_1-189](assets/chlimage_1-189.png)

### Mostrando referências de tag {#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

Quando um namespace ou outra marca é selecionada, selecionar o ícone **Referências** identificará o conteúdo ao qual a marca foi aplicada.

A exibição inicial é uma contagem de tags aplicadas.

![chlimage_1-191](assets/chlimage_1-191.png)

Ao selecionar a seta à direita da contagem, os nomes de referência são listados.

O caminho para a referência é exibido como uma dica de ferramenta ao passar o mouse sobre uma referência.

![chlimage_1-192](assets/chlimage_1-192.png)

### Criação de tags {#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

Quando um namespace ou outra marca é selecionada (selecionando o ícone ao lado do título), uma marca secundária pode ser criada para a marca atual selecionando o ícone **`Create Tag`**.

![chlimage_1-194](assets/chlimage_1-194.png)

* **Título**
* (obrigatório) *Um título de exibição para a tag.

* **Nome**
* (opcional) *Um nome para a tag. Se não for especificado, um nome de nó válido será criado a partir do Título. Consulte [TagID](/help/sites-developing/framework.md#tagid).

* **Descrição**
* (opcional) *Uma descrição da tag.

Quando as informações necessárias forem inseridas

* selecione **Criar**

### Edição de tags {#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

Quando um namespace ou outra marca é selecionada, é possível alterar o Título, a Descrição e fornecer localizações do Título selecionando o ícone **`Edit`**.

Depois de fazer as edições, selecione **Salvar**.

Para obter detalhes sobre como adicionar traduções de idioma, consulte a seção em [Gerenciando Tags em Diferentes Idiomas](#managing-tags-in-different-languages).

![chlimage_1-196](assets/chlimage_1-196.png)

### Mover tags {#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

Quando um namespace ou outra marca é selecionada, selecionar o ícone **`Move`** permitirá que Administradores e Desenvolvedores de marcas limpem a taxonomia movendo a marca para um novo local ou renomeando-a. Quando a tag selecionada for uma tag container, movê-la também moverá todas as tags secundárias.

>[!NOTE]
>
>Recomenda-se que os Autores só tenham permissão para [editar](#editing-tags) o `title` da marca, e não para mover ou renomear marcas.

![chlimage_1-198](assets/chlimage_1-198.png)

* **Caminho**
  *(somente leitura)* O caminho atual para a marca selecionada.

* **Mover para**
Navegue até o novo caminho no qual mover a tag.

* **Renomear para**
Exibe inicialmente a `name` atual da marca. Um novo `name`pode ser inserido.

* selecione **Salvar**

### Mesclar tags {#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

A mesclagem de tags pode ser usada quando uma taxonomia tem duplicatas. Quando a tag A é mesclada à tag B, todas as páginas marcadas com a tag A são marcadas com a tag B e a tag A não está mais disponível para os autores.

Quando um namespace ou outra marca é selecionada, selecionar o ícone **Mesclar** abre um painel onde o caminho para mesclagem pode ser selecionado.

![chlimage_1-200](assets/chlimage_1-200.png)

* **Caminho**
  *(somente leitura)* O caminho da marca selecionada para ser mesclada em outra marca.

* **Mesclar para**
Procure para selecionar o caminho da tag na qual mesclar.

>[!NOTE]
>
>Após a mesclagem, o **Caminho** selecionado originalmente (virtualmente) não existirá mais.
>
>Quando uma tag referenciada é movida ou mesclada, a tag não é fisicamente excluída, de modo que é possível manter referências.

### Publicação de tags {#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

Quando um namespace ou outra marca é selecionada, selecionando o ícone **Publish** para ativar a marca no ambiente de publicação. Similar ao conteúdo da página, somente a tag selecionada é publicada, independentemente de ser uma tag container ou não.

Para publicar uma taxonomia (um namespace e subtags), a prática recomendada é criar um [pacote](/help/sites-administering/package-manager.md) do namespace (consulte [Nó Raiz da Taxonomia](/help/sites-developing/framework.md#taxonomy-root-node)). Certifique-se de [aplicar permissões](#setting-tag-permissions) ao namespace antes de criar o pacote.

### Desfazer publicação de tags {#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

Quando um namespace ou outra marca é selecionada, selecionar o ícone **Cancelar publicação** desativará a marca no ambiente de criação e a removerá do ambiente de publicação. Semelhante à operação `Delete`, se a marca selecionada for uma marca de contêiner, todas as suas marcas secundárias serão desativadas no ambiente de criação e removidas do ambiente de publicação.

### Exclusão de tags {#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

Quando um namespace ou outra marca é selecionada, selecionar o ícone **Excluir** removerá permanentemente a marca do ambiente de criação. Se a tag tiver sido publicada, ela também será removida do ambiente de publicação. Se a tag selecionada for uma tag container, todas as tags secundárias também serão removidas.

## Definição de permissões de tag {#setting-tag-permissions}

As permissões de tag são [&#39;seguras (por padrão)&#39;](/help/sites-administering/production-ready.md); uma prática recomendada para o ambiente de publicação que requer que a permissão de leitura seja explicitamente permitida para tags. Basicamente, isso é feito criando um pacote do namespace de tag depois que as permissões forem definidas no autor e instalando o pacote em todas as instâncias de publicação.

* na instância do autor

   * entrar com privilégios administrativos
   * acessar o [Console de Segurança](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console),

      * por exemplo, navegue até http://localhost:4502/useradmin

   * no painel esquerdo, selecione o grupo (ou usuário) para o qual a [permissão de leitura](/help/sites-administering/security.md#permissions) será concedida
   * no painel direito, localize o **Caminho &#x200B;** para o namespace da tag

      * por exemplo, `/content/cq:tags/mycommunity`

   * selecione o `checkbox`na coluna **Read**
   * selecione **Salvar**

![chlimage_1-204](assets/chlimage_1-204.png)

* verifique se todas as instâncias de publicação têm as mesmas permissões

   * uma abordagem é [criar um pacote](/help/sites-administering/package-manager.md#package-manager) do namespace no autor

      * na guia `Advanced`, para `AC Handling`, selecione `Overwrite`

   * replicar o pacote

      * escolha `Replicate` no gerenciador de pacotes

## Gerenciamento de tags em diferentes idiomas {#managing-tags-in-different-languages}

A propriedade `title`de uma marca pode ser traduzida em vários idiomas. Depois de traduzida, a tag apropriada `title` pode ser exibida de acordo com o idioma do usuário ou do idioma da página.

### Definição de títulos de tag em vários idiomas {#defining-tag-titles-in-multiple-languages}

A tabela a seguir descreve como traduzir os `title`da marca **Animais** do inglês para o alemão e o francês.

Comece selecionando a marca no namespace **Stock Photography** e selecionando o ícone **`Edit`* (consulte a seção [Edição de Marcas](#editing-tags)).

O painel Editar tag apresenta a capacidade de escolher idiomas nos quais o título da tag deve ser localizado.

À medida que cada idioma é selecionado, uma caixa de entrada de texto é exibida, na qual o título traduzido pode ser inserido.

Depois que todas as traduções forem inseridas, selecione **Salvar** para sair do modo de edição.

![chlimage_1-205](assets/chlimage_1-205.png)

Em geral, o idioma escolhido para a tag é retirado do idioma da página, quando disponível. Quando o widget [`tag` ](/help/sites-developing/building.md#tagging-on-the-client-side) é usado em outros casos (por exemplo, em formulários ou caixas de diálogo), o idioma da marca depende do contexto.

Em vez de usar a configuração de idioma da página, o console Marcação usa a configuração de idioma do usuário. No console de marcação, para a tag &quot;Animais&quot;, &quot;Animaux&quot; seria exibido para um usuário que define o idioma para francês em suas propriedades de usuário.

Para adicionar um novo idioma à caixa de diálogo, consulte [Adicionando um Novo Idioma à Caixa de Diálogo Editar Marca](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog).

>[!NOTE]
>
>A nuvem de tags e as metapalavras-chave no componente de página padrão usam a tag localizada `titles` com base no idioma da página, se disponível.

## Recursos {#resources}

* [Marcação para desenvolvedores](/help/sites-developing/tags.md)

  Informações sobre a estrutura de marcação e a extensão e inclusão de tags em aplicativos personalizados.

* [Console de marcação da interface clássica](/help/sites-administering/classic-console.md)
