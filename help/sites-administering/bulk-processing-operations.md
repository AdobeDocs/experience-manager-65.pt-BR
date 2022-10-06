---
title: Operações de processamento em massa
seo-title: Bulk Processing Operations
description: null
seo-description: null
page-status-flag: never-activated
uuid: 62a6c379-a460-4f8f-a909-03d04fa8944b
contentOwner: sarchiz
discoiquuid: 47c2a80f-78ac-4372-86b4-06351a1dd58f
docset: aem65
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 2%

---


# Operações de processamento em massa {#bulk-processing-operations}

## Introdução {#introduction}

Com a versão mais recente do AEM, o botão selecionar tudo foi estendido para todas as exibições: Exibição de lista, coluna e cartão. O botão selecionar tudo agora seleciona todo o conteúdo em uma determinada pasta ou coleção e não apenas os Ativos e páginas que são carregados e visíveis no navegador do cliente.

As ações principais foram habilitadas para a operação em massa: **Mover**, **Excluir** e **Copiar**. Uma nova caixa de diálogo permitirá que os clientes saibam quais são as ações para as quais o processamento em massa não está disponível.

## Como usar {#how-to-use}

Um novo botão chamado **Selecionar tudo** foi adicionado às exibições Cartão, Lista ou Coluna. Esse botão pode ser usado em qualquer uma das exibições para selecionar todos os elementos no conjunto de dados.

Em versões anteriores do AEM, a seleção limitava o que era carregado no navegador do cliente. Essas novas alterações foram introduzidas para evitar confusão em relação ao número de elementos em que uma operação em massa está sendo executada.

Por enquanto, três operações foram adicionadas ao processamento em massa:

* Mover
* Copiar
* Excluir

O suporte para mais operações será adicionado no futuro.
Para usar esse recurso, você precisa navegar até a pasta ou coleção em que deseja executar a operação em massa nas Páginas ou nos Ativos.

Em seguida, escolha uma das exibições, conforme mostrado abaixo:

### Exibição de cartão {#card-view}

![](assets/unu.png)

### Seleção em massa na exibição de cartão {#bulk-selection-in-card-view}

Os ativos ou as páginas podem ser selecionados em massa usando o **Selecionar tudo** no canto superior direito:

![](assets/doi.png) ![](assets/trei.png)

### Exibição de lista {#list-view}

O mesmo se aplica à Exibição de lista:

![](assets/patru_modified.png)

### Seleção em massa na exibição de lista {#bulk-selection-in-list-view}

Na Exibição de lista, use **Selecionar tudo** ou use a caixa de seleção à esquerda para seleção em massa.

![](assets/cinci.png) ![](assets/sase.png)

### Exibição de coluna {#column-view}

![](assets/sapte.png)

### Seleção em massa na exibição de Coluna {#bulk-selection-in-column-view}

![](assets/opt.png)

## Operações habilitadas em massa {#bulk-enabled-operations}

Após a seleção, uma das três ações ativadas em massa pode ser executada: **Mover**, **Copiar** ou **Excluir**.

Aqui, **Mover** é executada no Assets selecionado acima. Em qualquer uma das exibições, isso resultará na movimentação de todos os Ativos para o local escolhido e não apenas para os que são carregados na tela.

![](assets/noua.png)

Para outras operações que não são ativadas em massa, como **Download,** um aviso será mostrado informando que somente os elementos carregados no navegador serão incluídos na operação.

![](assets/zece.png)
