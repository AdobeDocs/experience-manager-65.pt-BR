---
title: Modelos de grupo
seo-title: Group Templates
description: Como acessar o console Modelos de grupo
seo-description: How to access the Group Templates console
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
role: Admin
exl-id: aed2c3f2-1b5e-4065-8cec-433abb738ef5
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 3%

---

# Modelos de grupo {#group-templates}

O console Modelos de grupo é semelhante ao [Modelos de site](/help/communities/sites.md) console. Ambos são blueprints para um conjunto de páginas e recursos pré-conectados que formam um site da comunidade. A diferença é que um modelo de site é para a comunidade principal e um modelo de grupo é para um grupo da comunidade, uma subcomunidade aninhada dentro da comunidade principal.

Um grupo da comunidade é incorporado em um modelo de site ao incluir a variável [Função Grupos](/help/communities/functions.md#groups-function) (que pode não ser a primeira nem a única função no template).

Comunidades [pacote de recursos 1](/help/communities/deploy-communities.md#latestfeaturepack), é possível aninhar grupos incluindo a função Grupos em um modelo de grupo.

No momento em que uma ação é realizada para criar um novo grupo de comunidade, o modelo (estrutura) do grupo é selecionado. A seleção depende de como a função Grupos foi configurada quando adicionada ao modelo de site ou grupo.

>[!NOTE]
>
>Os consoles para a criação de [sites da comunidade](/help/communities/sites-console.md), [modelos de site da comunidade](/help/communities/sites.md), [modelos de grupo da comunidade](/help/communities/tools-groups.md) e [funções da comunidade](/help/communities/functions.md) são para uso somente no ambiente do autor.

## Console Modelos de Grupo {#group-templates-console}

Para acessar o console modelos de grupos no ambiente de Autor do AEM:

* Selecionar **Ferramentas | Comunidades | Modelos de grupo,** da navegação global.

Esse console exibe os modelos a partir dos quais uma [site da comunidade](/help/communities/sites-console.md) podem ser criados e permitem a criação de novos modelos de grupo.

![Modelo de grupos da comunidade](assets/groups-template.png)

## Criar modelo de grupo {#create-group-template}

Para começar a criar um novo modelo de grupo, selecione `Create`.

Isso exibirá o painel Editor de sites , que contém três subpainéis:

### Informações básicas {#basic-info}

![informações básicas do site](assets/site-basic-info.png)

No painel Informações básicas , um nome, uma descrição e se o modelo está ativado ou desativado são configurados:

* **Novo nome do modelo de grupo**

   A ID do nome do modelo.

* **Descrição**

   A descrição do modelo.

* **Desativado/Ativado**

   Um switch de alternância que controla se o modelo é referenciável.

#### Miniatura  {#thumbnail}

![miniatura do site](assets/site-thumbnail.png)

(Opcional) Selecione o ícone Fazer upload da imagem para exibir uma miniatura junto com o Nome e a Descrição para os criadores de sites da comunidade.

#### Estrutura {#structure}

>[!CAUTION]
>
>Se estiver trabalhando com AEM 6.1 Communities FP4 ou anterior, não adicione uma função de grupos a um modelo de grupo.
>
>O recurso de grupos aninhados está disponível a partir de Comunidades [FP1](/help/communities/communities.md#latestfeaturepack).
>
>Ainda não é permitido adicionar uma função Grupos como a primeira ou única função em um modelo.

![Editor de modelo de grupo](assets/template-editor.png)

Para adicionar funções de comunidade, arraste do lado direito para a esquerda na ordem em que os links de menu do site devem aparecer. Os estilos serão aplicados ao modelo durante a criação do site.

Por exemplo, se você quiser um fórum, arraste a função de fórum da biblioteca e solte no construtor de modelo. Isso resultará na abertura da caixa de diálogo de configuração do fórum. Consulte a [console funções](/help/communities/functions.md) para obter informações sobre as caixas de diálogo de configuração.

Continue arrastando e soltando quaisquer outras funções da comunidade desejadas para um site da subcomunidade (grupo) com base nesse modelo.

![arrastar funções](assets/dragfunctions.png)

Depois que todas as funções desejadas forem soltas na área do construtor de modelos e configuradas, selecione **Salvar** no canto superior direito.

## Editar modelo do grupo {#edit-group-template}

Ao visualizar grupos da comunidade no [Console Modelos de grupo](#group-templates-console), é possível selecionar um modelo de grupo existente para edição.

Editar um modelo de grupo não afetará os sites da comunidade já criados a partir do modelo. É possível diretamente [editar um site da comunidade](/help/communities/sites-console.md#modify-structure)Em vez disso, a estrutura do .

Esse processo fornece os mesmos painéis que [criação de um modelo de grupo](#create-group-template).
