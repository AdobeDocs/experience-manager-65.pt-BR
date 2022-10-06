---
title: Administração de tags
seo-title: Administering Tags
description: Saiba como administrar Tags no AEM.
seo-description: Learn how to administer Tags in AEM.
uuid: 77e1280a-feea-4edd-94b6-4fb825566c42
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 69253ee9-8c28-436b-9331-6fb875f64cba
exl-id: ff041ef0-e566-4373-818e-76680ff668d8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1760'
ht-degree: 1%

---

# Administração de tags {#administering-tags}

Tags são um método rápido e fácil de classificar o conteúdo em um site. Eles podem ser considerados palavras-chave ou rótulos (metadados) que permitem que o conteúdo seja encontrado mais rapidamente como resultado de uma pesquisa.

No Adobe Experience Manager (AEM), uma tag pode ser uma propriedade de

* um nó de conteúdo para uma página (consulte [Uso de tags](/help/sites-authoring/tags.md))

* um nó de metadados para um ativo (consulte [Gerenciamento de metadados para ativos digitais](/help/assets/metadata.md))

Além de páginas e ativos, tags são usadas para recursos do AEM Communities

* conteúdo gerado pelo usuário (consulte [Marcando UGC)](/help/communities/tag-ugc.md)

* Recursos de ativação (consulte [Marcar recursos de ativação](/help/communities/functions.md#catalog-function))

## Recursos de tag {#tag-features}

Alguns dos recursos das tags no AEM incluem:

* As tags podem ser agrupadas em vários namespaces. Essas hierarquias permitem a construção de taxonomias. Essas taxonomias são globais em todo o AEM.
* A restrição principal para tags recém-criadas é que elas devem ser exclusivas em um namespace específico.
* O título de uma tag não deve incluir caracteres de separação de caminho de tag (nem serão exibidos se estiverem presentes)

   * dois pontos `:` - delimita a tag namespace
   * barra `/` - subtags delimits

* As tags podem ser aplicadas por autores e visitantes do site. Independentemente do criador, todas as formas de tags são disponibilizadas para seleção, tanto ao atribuir a uma página quanto ao pesquisar.
* As tags podem ser criadas e sua taxonomia modificada por membros do grupo &quot;tag-administrators&quot; e membros que têm direitos de modificação para `/content/cq:tags`.

   * Uma tag que contém tags secundárias é chamada de tag container
   * Uma tag que não é uma tag de container é chamada de tag de folha
   * Um namespace de tag é uma tag de folha ou uma tag de container

* As tags são usadas pelo [Componente de pesquisa](https://helpx.adobe.com/experience-manager/core-components/using/quick-search.html) para facilitar a descoberta de conteúdo.
* As tags são usadas pelo [Componente Teaser](https://helpx.adobe.com/experience-manager/core-components/using/teaser.html), que monitora a nuvem de tags de um usuário para fornecer conteúdo direcionado.
* Se a marcação for um aspecto importante do seu conteúdo

   * certifique-se de empacotar tags com as páginas que as usam
   * certifique-se [permissões de tag](#setting-tag-permissions) habilitar acesso de leitura

## Console de marcação {#tagging-console}

O console Marcação é usado para criar e gerenciar tags e suas taxonomias. Um objetivo é evitar ter muitas tags similares relacionadas basicamente à mesma coisa : por exemplo, página e páginas ou calçados e sapatos.

As tags são gerenciadas agrupando-se em namespaces, revisando o uso de tags existentes antes de criar novas e reorganizando-as sem desconectar a tag do conteúdo referenciado no momento.

Para acessar o console Marcação :

* sobre o autor
* fazer logon com privilégios administrativos
* da navegação global

   * select **`Tools`**
   * select **`General`**
   * select **`Tagging`**

![managing_tags_usingthetagasministationconsole](assets/managing_tags_usingthetagasministrationconsolea.png)

### Criação de um namespace {#creating-a-namespace}

Para criar um novo namespace, selecione a variável **`Create Namespace`** ícone .

O namespace é, em si, uma tag e não precisa conter nenhuma subtag. No entanto, para continuar criando uma taxonomia, [criar subtags](#creating-tags), que, por sua vez, pode ser tags de folha ou tags de container.

![chlimage_1-183](assets/chlimage_1-183a.png) ![create_tags_andnamespaces](assets/creating_tags_andnamespacesa.png)

* **Título**

   *(obrigatório)* Um título de exibição para o namespace.

* **Nome**
   *(opcional)* Um nome para o namespace. Se não especificado, um nome de nó válido é criado a partir do Título. Consulte [TagID](/help/sites-developing/framework.md#tagid).

* **Descrição**

   *(opcional)* Uma descrição do namespace.

Uma vez inseridas as informações necessárias

* select **Criar**

### Operações em tags {#operations-on-tags}

Selecionar um namespace ou outra tag torna disponíveis as seguintes operações:

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

Quando a janela do navegador não for larga o suficiente para exibir todos os ícones, os ícones mais à direita serão agrupados em um **`... More`** , que exibirá uma lista suspensa dos ícones de operação oculta quando selecionados.

![chlimage_1-185](assets/chlimage_1-185.png)

### Selecionar uma tag de namespace {#selecting-a-namespace-tag}

Quando selecionadas pela primeira vez, se o namespace não contiver nenhuma tag, as propriedades serão exibidas à direita, caso contrário, as tags filho serão exibidas. Cada tag selecionada exibirá as tags que contém ou suas propriedades se não tiver tags filho.

Para selecionar a tag para operações e fazer várias seleções, selecione somente o ícone ao lado do título. Selecionar o título exibirá somente as propriedades ou abrirá a tag para exibir seu conteúdo.

![chlimage_1-186](assets/chlimage_1-186.png) ![chlimage_1-187](assets/chlimage_1-187.png)

### Exibição das propriedades da tag {#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

Quando um namespace ou outra tag for selecionada, selecione a variável **`View Properties`** O ícone resulta na exibição de informações sobre o `name`, hora da última edição e número de referências. Se publicado, é exibida a hora em que foi publicado pela última vez e a ID do editor. Essas informações aparecerão em uma coluna à esquerda das colunas de tag.

![chlimage_1-189](assets/chlimage_1-189.png)

### Referências de tag exibidas {#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

Quando um namespace ou outra tag for selecionada, selecione a variável **Referências** ícone identificará o conteúdo ao qual a tag foi aplicada.

A exibição inicial é uma contagem de tags aplicadas.

![chlimage_1-191](assets/chlimage_1-191.png)

Ao selecionar a seta à direita da contagem, os nomes de referência são listados.

O caminho para a referência é exibido como uma dica de ferramenta ao passar o mouse sobre uma referência.

![chlimage_1-192](assets/chlimage_1-192.png)

### Criação de tags {#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

Quando um namespace ou outra tag é selecionada (selecionando o ícone ao lado do título), uma tag filho pode ser criada para a tag atual selecionando o **`Create Tag`** ícone .

![chlimage_1-194](assets/chlimage_1-194.png)

* **Título**
*(obrigatório) *Um título de exibição para a tag.

* **Nome**
*(opcional) *Um nome para a tag. Se não especificado, um nome de nó válido é criado a partir do Título. Consulte [TagID](/help/sites-developing/framework.md#tagid).

* **Descrição**
*(opcional) *Uma descrição da tag.

Uma vez inseridas as informações necessárias

* select **Criar**

### Edição de tags {#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

Quando um namespace ou outra tag é selecionada, é possível alterar o Título, a Descrição e fornecer as localizações do Título selecionando o **`Edit`**ícone.

Depois que as edições forem feitas, selecione **Salvar**.

Para obter detalhes sobre como adicionar traduções de idioma, consulte a seção em [Gerenciamento de tags em diferentes idiomas](#managing-tags-in-different-languages).

![chlimage_1-196](assets/chlimage_1-196.png)

### Mover tags {#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

Quando um namespace ou outra tag for selecionada, selecione a variável **`Move`** Esse ícone permitirá que os administradores e desenvolvedores de tags limpem a taxonomia movendo a tag para um novo local ou renomeando-a. Quando a tag selecionada é uma tag container, mover a tag também moverá todas as tags filho.

>[!NOTE]
>
>Recomenda-se que os Autores só tenham permissão para [editar](#editing-tags) da tag `title`, não para mover ou renomear tags.

![chlimage_1-198](assets/chlimage_1-198.png)

* **Caminho**

   *(somente leitura)* O caminho atual para a tag selecionada.

* **Mover para**
Navegue até o novo caminho sob o qual deseja mover a tag.

* **Renomear para**
Exibe inicialmente o 
`name`da tag . Um novo `name`podem ser inseridas.

* select **Salvar**

### Mesclar tags {#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

A mesclagem de tags pode ser usada quando uma taxonomia tem duplicatas. Quando a tag A é unida à tag B, todas as páginas marcadas com a tag A serão marcadas com a tag B e a tag A não estará mais disponível para os autores.

Quando um namespace ou outra tag for selecionada, selecione a variável **Mesclar** abrirá um painel onde o caminho para mesclar pode ser selecionado.

![chlimage_1-200](assets/chlimage_1-200.png)

* **Caminho**

   *(somente leitura)* O caminho da tag selecionada a ser mesclada com outra tag.

* **Mesclar em**
Navegue para selecionar o caminho da tag para mesclar.

>[!NOTE]
>
>Após a mesclagem, o **Caminho** originalmente selecionado não existirá (virtualmente) mais.
>
>Quando uma tag referenciada é movida ou mesclada, ela não é fisicamente excluída de modo que seja possível manter referências.

### Publicação de tags {#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

Quando um namespace ou outra tag for selecionada, selecione a variável **Publicar** ícone para ativar a tag no ambiente de publicação. Semelhante ao conteúdo da página, somente a tag selecionada é publicada, independentemente de ser ou não uma tag container.

Para publicar uma taxonomia (um namespace e subtags), a prática recomendada é criar um [pacote](/help/sites-administering/package-manager.md) do namespace (consulte [Nó raiz da taxonomia](/help/sites-developing/framework.md#taxonomy-root-node)). Certifique-se de [aplicar permissões](#setting-tag-permissions) para o namespace antes de criar o pacote.

### Desfazer a publicação de tags {#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

Quando um namespace ou outra tag for selecionada, selecione a variável **Cancelar publicação** ícone desativará a tag no ambiente de criação e a removerá do ambiente de publicação. Semelhante ao `Delete`, se a tag selecionada for uma tag container , todas as tags filho serão desativadas no ambiente de criação e removidas do ambiente de publicação.

### Exclusão de tags {#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

Quando um namespace ou outra tag for selecionada, selecione a variável **Excluir** ícone removerá permanentemente a tag do ambiente de criação. Se a tag foi publicada, ela também é removida do ambiente de publicação. Se a tag selecionada for uma tag container, todas as tags filho também serão removidas.

## Definir permissões de tag {#setting-tag-permissions}

As permissões de tag são [&#39;secure (por padrão)&#39;](/help/sites-administering/production-ready.md); uma prática recomendada para o ambiente de publicação que requer permissão de leitura para ser explicitamente permitida para tags. Basicamente, isso é feito criando um pacote do Namespace de tag depois que as permissões são definidas no autor e instalando o pacote em todas as instâncias de publicação.

* na instância do autor

   * fazer logon com privilégios administrativos
   * acesse o [Console de segurança](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console),

      * por exemplo, navegue até http://localhost:4502/useradmin
   * no painel esquerdo, selecione o grupo (ou usuário) para o qual [permissão de leitura](/help/sites-administering/security.md#permissions) é concedida
   * no painel direito, localize o **Caminho **para o namespace da tag

      * por exemplo, `/content/cq:tags/mycommunity`
   * selecione o `checkbox`no **Ler** column
   * select **Salvar**



![chlimage_1-204](assets/chlimage_1-204.png)

* verifique se todas as instâncias de publicação têm as mesmas permissões

   * uma abordagem é [criar um pacote](/help/sites-administering/package-manager.md#package-manager) do namespace no autor

      * on `Advanced` guia , para `AC Handling` select `Overwrite`
   * replicar o pacote

      * Choose `Replicate` do gerenciador de pacotes


## Gerenciamento de tags em diferentes idiomas {#managing-tags-in-different-languages}

O `title`a propriedade de uma tag pode ser traduzida para vários idiomas. Depois de traduzido, a tag apropriada `title`pode ser exibido de acordo com o idioma do usuário ou com o idioma da página.

### Definição de títulos de tag em vários idiomas {#defining-tag-titles-in-multiple-languages}

A seguir, você descreve como traduzir a variável `title`da tag **Animais** do inglês para o alemão e o francês.

Comece selecionando a tag no **Fotografia de bancos de dados** namespace e seleção de **`Edit`**ícone (consulte [Edição de tags](#editing-tags) seção).

O painel Editar tag apresenta a capacidade de escolher idiomas nos quais o título da tag deve ser localizado.

Como cada idioma é selecionado, uma caixa de entrada de texto é exibida na qual o título traduzido pode ser inserido.

Depois que todas as traduções forem inseridas, selecione **Salvar** para sair do modo de edição.

![chlimage_1-205](assets/chlimage_1-205.png)

Em geral, o idioma escolhido para a tag é retirado do idioma da página, quando disponível. Quando a variável [ `tag` widget](/help/sites-developing/building.md#tagging-on-the-client-side) é usada em outros casos (por exemplo, em formulários ou em caixas de diálogo), o idioma da tag depende do contexto.

Em vez de usar a configuração de idioma da página, o console Marcação usa a configuração de idioma do usuário. No console Marcação , para a tag &quot;Animais&quot;, &quot;Animaux&quot; seria exibido para um usuário que define o idioma para francês em suas propriedades do usuário.

Para adicionar um novo idioma à caixa de diálogo, consulte [Adicionar um novo idioma à caixa de diálogo Editar tag](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog).

>[!NOTE]
>
>A nuvem de tags e as meta palavras-chave no componente de página padrão usam a tag localizada `titles`com base no idioma da página, se disponível.

## Recursos {#resources}

* [Marcação para desenvolvedores](/help/sites-developing/tags.md)

   Informações sobre a estrutura de marcação, bem como a extensão e inclusão de tags em aplicativos personalizados.

* [Console de marcação da interface clássica](/help/sites-administering/classic-console.md)
