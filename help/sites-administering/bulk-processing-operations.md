---
title: Operações de processamento em massa
seo-title: Operações de processamento em massa
description: 'null'
seo-description: 'null'
page-status-flag: never-activated
uuid: 62a6c379-a460-4f8f-a909-03d04fa8944b
contentOwner: sarchiz
discoiquuid: 47c2a80f-78ac-4372-86b4-06351a1dd58f
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538

---


# Operações de processamento em massa {#bulk-processing-operations}

## Introdução {#introduction}

Com a versão mais recente do AEM, o botão selecionar todos foi estendido para todas as exibições: Exibição de lista, coluna e cartão. O botão selecionar tudo agora seleciona todo o conteúdo em uma determinada pasta ou coleção e não apenas os Ativos e Páginas que são carregados e visíveis no navegador do cliente.

As ações principais foram ativadas para a operação em massa: **Mover**, **Excluir** e **Copiar**. Uma nova caixa de diálogo informará os clientes sobre as ações para as quais o processamento em massa não está disponível.

## How To Use {#how-to-use}

Um novo botão chamado **Selecionar tudo** foi adicionado às exibições Cartão, Lista ou Coluna. Esse botão pode ser usado em qualquer uma das exibições para selecionar todos os elementos no conjunto de dados.

Em versões anteriores do AEM, a seleção era limitada ao que era carregado no navegador do cliente. Estas novas alterações foram introduzidas para evitar confusões quanto ao número de elementos em que uma operação em massa está a ser efetuada.

Por enquanto, foram adicionadas três operações à transformação em massa:

* Mover
* Copiar
* Excluir

O suporte para mais operações será adicionado no futuro.
Para usar esse recurso, você precisa navegar até a pasta ou coleção na qual deseja executar a operação em massa em Páginas ou Ativos.

Em seguida, escolha uma das exibições, como mostrado abaixo:

### Exibição de cartão {#card-view}

![](assets/unu.png)

### Seleção em massa na exibição de cartão {#bulk-selection-in-card-view}

Os ativos ou as páginas podem ser selecionados em massa usando o botão **Selecionar tudo** na parte superior direita:

![](assets/doi.png) ![](assets/trei.png)

### Exibição de lista {#list-view}

O mesmo se aplica à Exibição de lista:

![](assets/patru_modified.png)

### Bulk Selection in List View {#bulk-selection-in-list-view}

Na Exibição de lista, use o botão **Selecionar tudo** ou a caixa de seleção à esquerda para seleção em massa.

![](assets/cinci.png) ![](assets/sase.png)

### Exibição de coluna {#column-view}

![](assets/sapte.png)

### Seleção em massa na exibição de coluna {#bulk-selection-in-column-view}

![](assets/opt.png)

## Operações ativadas em massa {#bulk-enabled-operations}

Após a seleção, uma das três ações habilitadas em massa pode ser executada: **Mover**, **Copiar** ou **Excluir**.

Aqui, a operação **Mover** é executada nos Ativos selecionados acima. Em qualquer uma das exibições, isso resultará na movimentação de todos os Ativos para o local escolhido e não apenas para os que são carregados na tela.

![](assets/noua.png)

Para outras operações que não são ativadas em massa, como **Download,** será mostrado um aviso informando que somente os elementos carregados no navegador serão incluídos na operação.

![](assets/zece.png)
