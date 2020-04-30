---
title: Modelos de grupo
seo-title: Modelos de grupo
description: Como acessar o console Modelos de grupo
seo-description: Como acessar o console Modelos de grupo
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# Modelos de grupo {#group-templates}

O console Modelos de grupo é semelhante ao console Modelos [de](/help/communities/sites.md) site. Ambos são blueprints para um conjunto de páginas e recursos pré-conectados que formam um site da comunidade. A diferença é que um modelo de site é para a comunidade principal e um modelo de grupo é para um grupo da comunidade, uma subcomunidade aninhada na comunidade principal.

Um grupo da comunidade é incorporado a um modelo de site, incluindo a função [](/help/communities/functions.md#groups-function) Grupos (que pode não ser a primeira nem apenas a função no modelo).

No pacote de [recursos de Comunidades 1](/help/communities/deploy-communities.md#latestfeaturepack), é possível aninhar grupos incluindo a função Grupos em um modelo de grupo.

No momento em que uma ação é executada para criar um novo grupo da comunidade, o modelo do grupo (estrutura) é selecionado. A seleção depende de como a função Grupos foi configurada quando adicionada ao modelo do site ou grupo.

>[!NOTE]
>
>Os consoles para a criação de sites [da](/help/communities/sites-console.md)comunidade, modelos [de site da](/help/communities/sites.md)comunidade, modelos [de grupos da](/help/communities/tools-groups.md) comunidade e funções [da](/help/communities/functions.md) comunidade são para uso somente no ambiente do autor.


## Console de modelos de grupo {#group-templates-console}

Para acessar o console de modelos de grupos no ambiente de autor de AEM:

* Selecionar **ferramentas| Comunidades| Modelos de grupo,** da navegação global.

Este console exibe os modelos a partir dos quais um site [da](/help/communities/sites-console.md) comunidade pode ser criado e permite a criação de novos modelos de grupo.

![Modelo de grupos da comunidade](assets/groups-template.png)

## Criar modelo de grupo {#create-group-template}

Para começar a criar um novo modelo de grupo, selecione `Create`.

Isso exibirá o painel do Editor de sites, que contém três subpainéis:

### Informações básicas {#basic-info}

![chlimage_1-137](assets/chlimage_1-137.png)

No painel Informações básicas, um nome, uma descrição e se o modelo está ativado ou desativado são configurados:

* **Novo nome do modelo de grupo**

   A ID do nome do modelo.

* **Descrição**

   A descrição do modelo.

* **Desativado/Ativado**

   Um switch de alternância que controla se o modelo é referenciável.

#### Miniatura     {#thumbnail}

![chlimage_1-138](assets/chlimage_1-138.png)

(Opcional) Selecione o ícone Carregar imagem para exibir uma miniatura junto com o Nome e a Descrição para os criadores dos sites da comunidade.

#### Estrutura {#structure}

>[!CAUTION]
>
>Se estiver trabalhando com o AEM 6.1 Communities FP4 ou anterior, não adicione uma função de grupo a um modelo de grupo.
>
>O recurso de grupos aninhados está disponível a partir do [FP1](/help/communities/communities.md#latestfeaturepack)das Comunidades.
>
>Ainda não é permitido adicionar uma função de Grupos como a primeira função ou somente função em um modelo.


![Editor de modelos de grupo](assets/template-editor.png)

Para adicionar funções de comunidade, arraste do lado direito para a esquerda na ordem em que os links de menu do site devem aparecer. Os estilos serão aplicados ao modelo durante a criação do site.

Por exemplo, se você quiser um fórum, arraste a função do fórum da biblioteca e solte sob o construtor de modelos. Isso resultará na abertura da caixa de diálogo de configuração do fórum. Consulte o console [de](/help/communities/functions.md) funções para obter informações sobre as caixas de diálogo de configuração.

Continue arrastando e soltando quaisquer outras funções da comunidade desejadas para um site da subcomunidade (grupo) com base nesse modelo.

![funções arrastar](assets/dragfunctions.png)

Depois que todas as funções desejadas forem soltas na área do construtor de modelos e configuradas, selecione **Salvar** no canto superior direito.

## Editar modelo do grupo {#edit-group-template}

Ao exibir grupos de comunidade no console [principal Modelos de](#group-templates-console)grupo, é possível selecionar um modelo de grupo existente para edição.

Editar um modelo de grupo não afetará os sites da comunidade já criados a partir do modelo. É possível [editar diretamente a estrutura de um site](/help/communities/sites-console.md#modify-structure)da comunidade.

Esse processo fornece os mesmos painéis que [criar um modelo](#create-group-template)de grupo.
