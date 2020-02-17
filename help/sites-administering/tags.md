---
title: Administração de tags
seo-title: Administração de tags
description: Saiba como administrar tags no AEM.
seo-description: Saiba como administrar tags no AEM.
uuid: 77e1280a-feea-4edd-94b6-4fb825566c42
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 69253ee9-8c28-436b-9331-6fb875f64cba
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Administração de tags {#administering-tags}

Tags são um método rápido e fácil de classificar o conteúdo em um site. Eles podem ser considerados palavras-chave ou rótulos (metadados) que permitem que o conteúdo seja encontrado mais rapidamente como resultado de uma pesquisa.

No Adobe Experience Manager (AEM), uma tag pode ser uma propriedade de

* um nó de conteúdo para uma página (consulte [Uso de tags](/help/sites-authoring/tags.md))

* um nó de metadados para um ativo (consulte [Gerenciamento de metadados para ativos](/help/assets/metadata.md)digitais)

Além de páginas e ativos, as tags são usadas para os recursos do AEM Communities

* conteúdo gerado pelo usuário (consulte [Marcação de UGC)](/help/communities/tag-ugc.md)

* Recursos de ativação (consulte [Marcação de recursos](/help/communities/functions.md#catalog-function)de ativação)

## Recursos da tag {#tag-features}

Alguns dos recursos das tags no AEM incluem:

* As tags podem ser agrupadas em vários namespaces. Essas hierarquias permitem construir taxonomias. Essas taxonomias são globais em todo o AEM.
* A principal restrição para tags recém-criadas é que elas devem ser exclusivas em um namespace específico.
* O título de uma tag não deve incluir caracteres de separação de caminho de tag (nem serão exibidos se presentes)

   * dois pontos `:` - delimita a marca de namespace
   * barra `/` - delimita as subtags

* As tags podem ser aplicadas por autores e visitantes do site. Independentemente do criador, todas as formas de tags são disponibilizadas para seleção, tanto ao atribuir a uma página quanto ao pesquisar.
* As tags podem ser criadas e sua taxonomia modificada por membros do grupo &quot;administradores de tags&quot; e membros que têm direitos de modificação para `/content/cq:tags`.

   * Uma tag que contém tags-filho é chamada de tag container
   * Uma tag que não é uma tag de contêiner é chamada de tag de folha
   * Um namespace de tag é uma tag de folha ou uma tag de contêiner

* As tags são usadas pelo componente [](https://helpx.adobe.com/experience-manager/core-components/using/quick-search.html) Pesquisar para facilitar a localização de conteúdo.
* As tags são usadas pelo componente [](https://helpx.adobe.com/experience-manager/core-components/using/teaser.html)Teaser, que monitora a nuvem de tags de um usuário para fornecer conteúdo direcionado.
* Se a marcação for um aspecto importante do seu conteúdo

   * certifique-se de disponibilizar tags com as páginas que as usam
   * verifique se as permissões [de](#setting-tag-permissions) tag permitem acesso de leitura

## Console de marcação {#tagging-console}

O console Marcação é usado para criar e gerenciar tags e suas taxonomias. Um objetivo é evitar ter muitas tags similares relacionadas basicamente à mesma coisa: por exemplo, página e páginas ou calçados e sapatos.

As tags são gerenciadas agrupando-se em namespaces, revisando o uso de tags existentes antes de criar novas e reorganizando-se sem desconectar a tag do conteúdo referenciado no momento.

Para acessar o console Marcação :

* sobre o autor
* fazer logon com privilégios administrativos
* da navegação global

   * select **`Tools`**
   * select **`General`**
   * select **`Tagging`**

![managing_tags_usingthetagasministationconsole](assets/managing_tags_usingthetagasministrationconsolea.png)

### Criação de um namespace {#creating-a-namespace}

Para criar um novo namespace, selecione o **`Create Namespace`** ícone.

O namespace é uma tag e não precisa conter subtags. Entretanto, para continuar a criar uma taxonomia, [crie subtags](#creating-tags)que, por sua vez, podem ser tags de folha ou de contêiner.

![chlimage_1-183](assets/chlimage_1-183a.png) ![creating_tags_andnamespaces](assets/creating_tags_andnamespacesa.png)

* **Título**
   *(obrigatório)* Um título de exibição para o namespace.

* **Nome**
   *(opcional)* Um nome para o namespace. Se não for especificado, um nome de nó válido será criado a partir do Título. Consulte [TagID](/help/sites-developing/framework.md#tagid).

* **Descrição**
   *(opcional)* Uma descrição do namespace.

Após a inserção das informações necessárias

* select **Create**

### Operações em tags {#operations-on-tags}

Selecionar um namespace ou outra tag disponibiliza as seguintes operações:

* [Propriedades da exibição](#viewing-tag-properties)
* [Referências](#showing-tag-references)
* [Criar tag](#creating-tags)
* [Editar](#editing-tags)
* [Mover](#moving-tags)
* [Mesclar](#merging-tags)
* [Publicação](#publishing-tags)
* [Cancelar publicação](#unpublishing-tags)
* [Excluir](#deleting-tags)

![chlimage_1-184](assets/chlimage_1-184.png)

Quando a janela do navegador não for larga o suficiente para exibir todos os ícones, os ícones mais à direita serão agrupados em um **`... More`** ícone, que exibirá uma lista suspensa dos ícones de operação ocultos quando selecionados.

![chlimage_1-185](assets/chlimage_1-185.png)

### Seleção de uma tag de namespace {#selecting-a-namespace-tag}

Quando selecionadas pela primeira vez, se o namespace não contiver nenhuma tag, as propriedades serão exibidas à direita, caso contrário, as tags-filho serão exibidas. Cada tag selecionada exibirá as tags que contém ou suas propriedades se não tiver tags-filho.

Para selecionar a tag para operações e para fazer várias seleções, selecione apenas o ícone ao lado do título. Selecionar o título exibirá somente as propriedades ou abrirá a tag para exibir seu conteúdo.

![chlimage_1-186](assets/chlimage_1-186.png) ![chlimage_1-187](assets/chlimage_1-187.png)

### Exibição das propriedades da tag {#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

Quando um namespace ou outra tag é selecionada, a seleção do **`View Properties`** ícone resulta na exibição de informações sobre o `name`, a hora da última edição e o número de referências. Se publicada, a hora em que foi publicada pela última vez e a ID do editor são mostradas. Essas informações aparecerão em uma coluna à esquerda das colunas da tag.

![chlimage_1-189](assets/chlimage_1-189.png)

### Mostrando referências de tag {#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

Quando um namespace ou outra tag é selecionada, selecionar o ícone **Referências** identificará o conteúdo ao qual a tag foi aplicada.

A exibição inicial é uma contagem de tags aplicadas.

![chlimage_1-191](assets/chlimage_1-191.png)

Ao selecionar a seta à direita da contagem, os nomes de referência são listados.

O caminho para a referência é exibido como uma dica de ferramenta ao passar o mouse sobre uma referência.

![chlimage_1-192](assets/chlimage_1-192.png)

### Criação de tags {#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

Quando um namespace ou outra tag é selecionada (selecionando o ícone ao lado do título), uma tag filho pode ser criada para a tag atual selecionando o **`Create Tag`** ícone.

![chlimage_1-194](assets/chlimage_1-194.png)

* **Título*** (obrigatório) *Um título de exibição para a tag .

* **Nome*** (opcional) *Um nome para a tag . Se não for especificado, um nome de nó válido será criado a partir do Título. Consulte [TagID](/help/sites-developing/framework.md#tagid).

* **Descrição*** (opcional) *Uma descrição da tag.

Após a inserção das informações necessárias

* select **Create**

### Edição de tags {#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

Quando um namespace ou outra tag é selecionada, é possível alterar o Título, a Descrição e fornecer as localizações do Título selecionando o ícone **`Edit`**.

Depois que as edições forem feitas, selecione **Salvar**.

Para obter detalhes sobre como adicionar traduções de idiomas, consulte a seção sobre [Gerenciamento de tags em diferentes idiomas](#managing-tags-in-different-languages).

![chlimage_1-196](assets/chlimage_1-196.png)

### Mover tags {#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

Quando um namespace ou outra tag for selecionada, a seleção do **`Move`** ícone permitirá que os administradores e desenvolvedores de tags limpem a taxonomia movendo a tag para um novo local ou renomeando-a. Quando a tag selecionada é uma tag container, mover a tag também moverá todas as tags filho.

>[!NOTE]
>
>É recomendável que os Autores só tenham permissão para [editar](#editing-tags) as tags `title`, e não para mover ou renomeá-las.

![chlimage_1-198](assets/chlimage_1-198.png)

* **Caminho**
   *(somente leitura)* O caminho atual para a tag selecionada.

* **Mova para** Procurar até o novo caminho sob o qual mover a tag.

* **Renomear para** Exibe a versão atual `name`da tag. É `name`possível inserir uma nova.

* select **Save**

### Mesclar tags {#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

A mesclagem de tags pode ser usada quando uma taxonomia tem duplicatas. Quando a tag A é unida à tag B, todas as páginas marcadas com a tag A serão marcadas com a tag B e a tag A não estará mais disponível para os autores.

Quando um namespace ou outra tag for selecionada, a seleção do ícone **Mesclar** abrirá um painel no qual o caminho a ser mesclado poderá ser selecionado.

![chlimage_1-200](assets/chlimage_1-200.png)

* **Caminho**
   *(somente leitura)* O caminho da tag selecionada a ser unida em outra tag.

* **Mesclar para** Procurar para selecionar o caminho da tag a ser unida.

>[!NOTE]
>
>Após a mesclagem, o **Caminho** selecionado originalmente não existirá (virtualmente).
>
>Quando uma tag referenciada é movida ou unida, ela não é fisicamente excluída, de modo que seja possível manter referências.

### Publicação de tags {#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

Quando um namespace ou outra tag for selecionada, selecione o ícone **Publicar** para ativar a tag no ambiente de publicação. Semelhante ao conteúdo da página, somente a tag selecionada é publicada, independentemente de ser ou não uma tag de contêiner.

Para publicar uma taxonomia (um namespace e subtags), a prática recomendada é criar um [pacote](/help/sites-administering/package-manager.md) do namespace (consulte Nó [raiz de](/help/sites-developing/framework.md#taxonomy-root-node)taxonomia). Certifique-se de [aplicar permissões](#setting-tag-permissions) ao namespace antes de criar o pacote.

### Desfazer publicação de tags {#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

Quando um namespace ou outra tag é selecionada, selecionar o ícone **Cancelar publicação** desativará a tag no ambiente do autor e a removerá do ambiente de publicação. Semelhante à `Delete`operação, se a tag selecionada for uma tag container, todas as tags-filho serão desativadas no ambiente do autor e removidas do ambiente de publicação.

### Excluindo tags {#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

Quando um namespace ou outra tag for selecionada, a seleção do ícone **Excluir** removerá permanentemente a tag do ambiente do autor. Se a tag tiver sido publicada, ela também será removida do ambiente de publicação. Se a tag selecionada for uma tag container, todas as tags filho também serão removidas.

## Definindo permissões de tag {#setting-tag-permissions}

As permissões de tag são [&#39;seguras (por padrão)&#39;](/help/sites-administering/production-ready.md); uma prática recomendada para o ambiente de publicação que requer permissão de leitura para ser explicitamente permitida para tags. Basicamente, isso é feito criando um pacote do Namespace da tag depois que as permissões são definidas no autor e instalando o pacote em todas as instâncias de publicação.

* na instância do autor

   * fazer logon com privilégios administrativos
   * acessar o console [de](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console)segurança,

      * por exemplo, navegue até http://localhost:4502/useradmin
   * no painel esquerdo, selecione o grupo (ou usuário) para o qual a permissão [de](/help/sites-administering/security.md#permissions) leitura deve ser concedida
   * no painel direito, localize o **Caminho **para o espaço para nome da tag

      * for example, `/content/cq:tags/mycommunity`
   * selecione o `checkbox`na coluna **Ler**
   * select **Save**



![chlimage_1-204](assets/chlimage_1-204.png)

* garantir que todas as instâncias de publicação tenham as mesmas permissões

   * uma abordagem é [criar um pacote](/help/sites-administering/package-manager.md#package-manager) do namespace no autor

      * na `Advanced` guia, para `AC Handling` selecionar `Overwrite`
   * replicar o pacote

      * escolher `Replicate` do gerenciador de pacotes


## Gerenciamento de tags em diferentes idiomas {#managing-tags-in-different-languages}

A `title`propriedade de uma tag pode ser traduzida para vários idiomas. Depois de traduzida, a tag apropriada `title`pode ser exibida de acordo com o idioma do usuário ou com o idioma da página.

### Definição de títulos de tag em vários idiomas {#defining-tag-titles-in-multiple-languages}

A seguir, é descrito como traduzir o texto `title`da etiqueta **Animais** do inglês para o alemão e o francês.

Comece selecionando a tag no namespace **Stock Photography** e selecionando o **`Edit`**ícone (consulte a seção [Edição de tags](#editing-tags) ).

O painel Editar tag apresenta a capacidade de escolher idiomas nos quais o título da tag deve ser localizado.

Conforme cada idioma é selecionado, uma caixa de entrada de texto é exibida na qual o título traduzido pode ser inserido.

Depois que todas as traduções forem inseridas, selecione **Salvar** para sair do modo de edição.

![chlimage_1-205](assets/chlimage_1-205.png)

Em geral, o idioma escolhido para a tag é retirado do idioma da página, quando disponível. Quando o [`tag` widget](/help/sites-developing/building.md#tagging-on-the-client-side) é usado em outros casos (por exemplo, em formulários ou em caixas de diálogo), a linguagem da tag depende do contexto.

Em vez de usar a configuração de idioma da página, o console Marcação usa a configuração de idioma do usuário. No console Marcação, para a tag &#39;Animais&#39;, &#39;Animaux&#39; seria exibido para um usuário que define o idioma como francês em suas propriedades de usuário.

Para adicionar um novo idioma à caixa de diálogo, consulte [Adicionar um novo idioma à caixa de diálogo](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog)Editar tag.

>[!NOTE]
>
>A nuvem de tags e as palavras-chave meta no componente de página padrão usam a tag localizada `titles`com base no idioma da página, se disponível.

## Recursos {#resources}

* [Marcação para desenvolvedores](/help/sites-developing/tags.md)

   Informações sobre a estrutura de marcação, além de estender e incluir tags em aplicativos personalizados.

* [Console de marcação da interface clássica](/help/sites-administering/classic-console.md)

