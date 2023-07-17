---
title: Operações de processamento em massa
description: null
page-status-flag: never-activated
contentOwner: sarchiz
docset: aem65
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 1%

---


# Operações de processamento em massa {#bulk-processing-operations}

## Introdução {#introduction}

Com a versão mais recente do Adobe Experience Manager (AEM), o botão Selecionar tudo foi estendido para todas as exibições: Lista, Coluna e Exibição de cartão. O botão Selecionar tudo agora seleciona todo o conteúdo em uma determinada pasta ou coleção e não apenas os Ativos e páginas carregados e visíveis no navegador do cliente.

As ações principais foram habilitadas para a operação em massa: **Mover**, **Excluir**, e **Copiar**. Uma nova caixa de diálogo permite que os clientes saibam para quais ações o processamento em massa não está disponível.

## Como Usar {#how-to-use}

Um novo botão chamado **Selecionar tudo** foi adicionado às exibições Cartão, Lista ou Coluna. Esse botão pode ser usado em qualquer uma das exibições para selecionar todos os elementos no conjunto de dados.

Em versões anteriores do AEM, a seleção limitava o que era carregado no navegador do cliente. Essa nova alteração foi introduzida para evitar confusão com relação ao número de elementos em que uma operação em massa está sendo executada.

Por enquanto, três operações foram adicionadas ao processamento em massa:

* Mover
* Copiar
* Excluir

O suporte para mais operações será adicionado no futuro.
Para usar esse recurso, navegue até a pasta ou coleção em que deseja executar a operação em massa nas Páginas ou nos Ativos.

Em seguida, escolha uma das exibições, conforme mostrado abaixo:

### Exibição de cartão {#card-view}

![Exibição de cartão que mostra imagens em miniatura de uma variedade de ativos de imagem.](assets/unu.png)

### Seleção em massa na exibição de cartão {#bulk-selection-in-card-view}

Os ativos ou as Páginas podem ser selecionados em massa usando o **Selecionar tudo** botão superior direito:

![Selecione o botão Tudo exibido no canto superior direito na Exibição de cartão.](assets/doi.png) ![Todas as imagens em miniatura de ativos de imagem na Exibição de cartão são mostradas como selecionadas com marcas de seleção.](assets/trei.png)

### Exibição de lista {#list-view}

O mesmo se aplica à Exibição de lista:

![A opção Selecionar tudo no canto superior direito da Exibição de lista está realçada.](assets/patru_modified.png)

### Seleção em massa na exibição de lista {#bulk-selection-in-list-view}

Na Exibição em Lista, use o **Selecionar tudo** ou use a caixa de seleção à esquerda para seleção em massa.

![Visualização dinâmica mostrando miniaturas, imagens de ativos de imagem exibidas em linhas horizontais.](assets/cinci.png) ![Caixa de listagem que mostra miniaturas, imagens de ativos de imagem e uma caixa de seleção à esquerda de Nome.](assets/sase.png)

### Exibição de coluna {#column-view}

![Exibição de coluna que mostra imagens em miniatura de imagens e ativos exibidos em colunas verticais.](assets/sapte.png)

### Seleção em Massa na Exibição de Coluna {#bulk-selection-in-column-view}

![Todas as imagens em miniatura de ativos de imagem na Exibição de coluna são mostradas como selecionadas com marcas de seleção.](assets/opt.png)

## Operações ativadas em massa {#bulk-enabled-operations}

Após a seleção, uma das três ações habilitadas em massa pode ser executada: **Mover**, **Copiar** ou **Excluir**.

Aqui, **Mover** a operação é executada nos Ativos selecionados acima. Em qualquer uma das exibições, isso resulta na movimentação de todos os ativos para o local escolhido e não apenas daqueles que são carregados na tela.

![Mova ativos que mostram uma pasta selecionada na Exibição de coluna.](assets/noua.png)

Para outras operações que não são ativadas em massa, como **Download,** um aviso é exibido informando que somente os elementos carregados no navegador são incluídos na operação.

![Exibição de ativos mostrando os ativos de imagem selecionados e a caixa de diálogo pop-up &quot;Ação em massa não suportada&quot;.](assets/zece.png)
