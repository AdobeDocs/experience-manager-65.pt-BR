---
title: Componente Estender comentários
seo-title: Componente Estender comentários
description: Estender o componente Comentários para alterar sua aparência ou comportamento para usos específicos
seo-description: Estender o componente Comentários para alterar sua aparência ou comportamento para usos específicos
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Componente Estender comentários  {#extend-comments-component}

A intenção de [estender](client-customize.md#extensions) um componente padrão é alterar a aparência ou o comportamento de um componente para usos específicos.

O caminho para o componente é exclusivo e faz referência ao componente padrão como um tipo de superrecurso. Há menos risco, pois o escopo é limitado em comparação ao escopo global de uma sobreposição de componente.

>[!NOTE]
>
>Não há suporte para a extensão de um componente [sobreposto](client-customize.md#overlays) .

## Exemplo {#example}

Suponha que o cabeçalho do componente de comentário deve ser exibido com uma aparência alternativa em um site da instância de AEM, enquanto aparece com a exibição padrão em outro site. Em vez de sobrepor o comentário padrão, que altera o componente de comentário para todas as instâncias, uma solução melhor é garantir que haja vários componentes de comentário disponíveis para uso em vários sites.

Para implementar essa solução, crie um novo componente que estenda (substitui) o existente e modifique o script Handlebars. A área do site que usa os novos comentários pode usar o extendido, enquanto os sites que usam a aparência padrão permanecem não afetados.

O componente de comentário é, na verdade, um dos dois componentes que compõem o sistema de comentários. Assim, há dois componentes a serem estendidos: *comentários* e *comentários*. O script a ser editado está no arquivo do componente de *comentário* , enquanto o componente de `header.hbs` comentários ** pai (o sistema de comentários) é o que um autor realmente adiciona à página.

Para estender comentários, é necessário:

1. [Criar os componentes](extend-create-components.md)
1. [Adicionar comentário à página de amostra](extend-sample-page.md)
1. [Alterar a aparência](extend-alter-appearance.md)

