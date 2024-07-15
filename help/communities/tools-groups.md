---
title: Modelos de grupo
description: Saiba como acessar o console Modelos de grupo para um conjunto de páginas e recursos pré-conectados que formam um site da comunidade.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: aed2c3f2-1b5e-4065-8cec-433abb738ef5
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---

# Modelos de grupo {#group-templates}

O console Modelos de Grupo é semelhante ao console [Modelos de Site](/help/communities/sites.md). Ambos são blueprints para um conjunto de páginas e recursos pré-conectados que formam um site da comunidade. A diferença é que um modelo de site é para a comunidade principal e um modelo de grupo é para um grupo da comunidade, uma subcomunidade aninhada na comunidade principal.

Um grupo da comunidade é incorporado a um modelo de site através da inclusão da [função de Grupos](/help/communities/functions.md#groups-function) (que pode não ser a primeira nem a única função no modelo).

A partir do Communities [feature pack 1](/help/communities/deploy-communities.md#latestfeaturepack), é possível aninhar grupos incluindo a função Grupos em um modelo de grupo.

No momento em que uma ação é executada para criar um grupo da comunidade, o modelo (estrutura) do grupo é selecionado. A seleção depende de como a função Grupos foi configurada quando adicionada ao site ou modelo de grupo.

>[!NOTE]
>
>Os consoles para a criação de [sites de comunidade](/help/communities/sites-console.md), [modelos de site de comunidade](/help/communities/sites.md), [modelos de grupo de comunidade](/help/communities/tools-groups.md) e [funções de comunidade](/help/communities/functions.md) são para uso somente no ambiente de autor.

## Console de modelos de grupo {#group-templates-console}

Para acessar o console de modelos de grupo no ambiente de autor do AEM:

* Selecionar **Ferramentas | Communities | Modelos de grupo,** da navegação global.

Este console exibe os modelos a partir dos quais um [site da comunidade](/help/communities/sites-console.md) pode ser criado e permite que novos modelos de grupo sejam criados.

![Modelo de grupos da comunidade](assets/groups-template.png)

## Criar modelo de grupo {#create-group-template}

Para começar a criar um modelo de grupo, selecione `Create`.

Isso exibe o painel Editor de sites, que contém três subpainéis:

### Informações básicas {#basic-info}

![informações-básicas-site](assets/site-basic-info.png)

No painel Informações básicas, um nome, uma descrição e se o modelo está ativado ou desativado são configurados:

* **Nome do Novo Modelo do Grupo**

  A ID do nome do modelo.

* **Descrição**

  A descrição do modelo.

* **Desabilitado/Habilitado**

  Um switch que controla se o modelo é referenciável.

#### Miniatura  {#thumbnail}

![miniatura-site](assets/site-thumbnail.png)

(Opcional) Selecione o ícone Fazer upload da imagem para exibir uma miniatura junto com o Nome e a Descrição para os criadores de sites da comunidade.

#### Estrutura {#structure}

>[!CAUTION]
>
>Se estiver trabalhando com o AEM 6.1 Communities FP4 ou anterior, não adicione uma função de grupos a um modelo de grupo.
>
>O recurso de grupos aninhados está disponível a partir das Comunidades [FP1](/help/communities/communities.md#latestfeaturepack).
>
>Ainda não é permitido adicionar uma função Groups como a primeira ou única função em um template.

![Editor de modelo de grupo](assets/template-editor.png)

Para adicionar funções da comunidade, arraste do lado direito para o lado esquerdo na ordem em que os links do menu do site devem aparecer. Os estilos são aplicados ao modelo durante a criação do site.

Por exemplo, se você quiser um fórum, arraste a função forum da biblioteca e solte-a no construtor de modelos. Isso resulta na abertura da caixa de diálogo de configuração do fórum. Consulte o [console de funções](/help/communities/functions.md) para obter informações sobre as caixas de diálogo de configuração.

Continue a arrastar e soltar quaisquer outras funções da comunidade desejadas para um site da subcomunidade (grupo) com base nesse modelo.

![arrastar funções](assets/dragfunctions.png)

Depois que todas as funções desejadas forem soltas na área do construtor de modelos e configuradas, selecione **Salvar** no canto superior direito.

## Editar modelo do grupo {#edit-group-template}

Ao visualizar grupos da comunidade no [console Modelos de grupo](#group-templates-console) principal, é possível selecionar um modelo de grupo existente para edição.

A edição de um modelo de grupo não afeta os sites da comunidade já criados a partir do modelo. É possível [editar diretamente a estrutura de um site da comunidade](/help/communities/sites-console.md#modify-structure).

Este processo fornece os mesmos painéis que [criando um modelo de grupo](#create-group-template).
