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

Com a versão mais recente do AEM, o botão Selecionar tudo foi estendido para todas as exibições: Lista, Coluna e Exibição de cartão. O botão Selecionar tudo agora seleciona todo o conteúdo em uma determinada pasta ou coleção e não apenas os Ativos e páginas carregados e visíveis no navegador do cliente.

As ações principais foram habilitadas para a operação em massa: **Mover**, **Excluir** e **Copiar**. Uma nova caixa de diálogo informará aos clientes quais ações o processamento em massa não está disponível.

## Como Usar {#how-to-use}

Um novo botão chamado **Selecionar tudo** foi adicionado às exibições de Cartão, Lista ou Coluna. Esse botão pode ser usado em qualquer uma das exibições para selecionar todos os elementos no conjunto de dados.

Em versões anteriores do AEM, a seleção limitava o que era carregado no navegador do cliente. Essas novas alterações foram introduzidas para evitar confusão com relação ao número de elementos em que uma operação em massa está sendo executada.

Por enquanto, três operações foram adicionadas ao processamento em massa:

* Mover
* Copiar
* Excluir

O suporte para mais operações será adicionado no futuro.
Para usar esse recurso, é necessário navegar até a pasta ou coleção em que deseja executar a operação em massa em Páginas ou Ativos.

Em seguida, escolha uma das exibições, conforme mostrado abaixo:

### Exibição de cartão {#card-view}

![](assets/unu.png)

### Seleção em massa na exibição de cartão {#bulk-selection-in-card-view}

Os ativos ou as Páginas podem ser selecionados em massa usando o **Selecionar tudo** botão superior direito:

![](assets/doi.png) ![](assets/trei.png)

### Exibição de lista {#list-view}

O mesmo se aplica à Exibição em lista:

![](assets/patru_modified.png)

### Seleção em massa na exibição de lista {#bulk-selection-in-list-view}

Na Exibição em Lista, use o **Selecionar tudo** ou use a caixa de seleção à esquerda para seleção em massa.

![](assets/cinci.png) ![](assets/sase.png)

### Exibição de coluna {#column-view}

![](assets/sapte.png)

### Seleção em Massa na Exibição de Coluna {#bulk-selection-in-column-view}

![](assets/opt.png)

## Operações ativadas em massa {#bulk-enabled-operations}

Após a seleção, uma das três ações ativadas em massa pode ser executada: **Mover**, **Copiar** ou **Excluir**.

Aqui, **Mover** a operação é executada nos Ativos selecionados acima. Em qualquer uma das exibições, isso resultará na movimentação de todos os ativos para o local escolhido e não apenas aqueles que são carregados na tela.

![](assets/noua.png)

Para outras operações que não são ativadas em massa, como **Download,** será mostrado um aviso de que somente os elementos carregados no navegador serão incluídos na operação.

![](assets/zece.png)
