---
title: Estender componente de comentários
description: Estender o componente Comentários para alterar sua aparência ou comportamento para usos específicos
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Estender componente de comentários  {#extend-comments-component}

A intenção de [estender](client-customize.md#extensions) um componente padrão é alterar a aparência ou o comportamento de um componente para usos específicos.

O caminho para o componente é exclusivo e faz referência ao componente padrão como um tipo de super recurso. Há menos risco, pois o escopo é limitado em comparação ao escopo global de uma sobreposição de componente.

>[!NOTE]
>
>Não há suporte para a extensão de um componente [sobreposto](client-customize.md#overlays).

## Exemplo {#example}

Suponha que o cabeçalho do componente de comentário deve ser exibido com uma aparência alternativa em um site da instância do AEM, enquanto aparece com a exibição padrão em outro site. Em vez de sobrepor o comentário padrão, que altera o componente de comentário para todas as instâncias, uma solução melhor é garantir que haja vários componentes de comentário disponíveis para uso em vários sites.

Para implementar esta solução, crie um componente que estenda (substitua) o existente e modifique o script Handlebars. A área do site que usa os novos comentários pode usar o estendido, enquanto os sites que usam a aparência padrão permanecem inalterados.

O componente de comentários é, na verdade, um dos dois componentes que compõem o sistema de comentários. Há dois componentes a serem estendidos: *comentários* e *comentários*. O script a ser editado está no arquivo `header.hbs` do componente *comentário*, enquanto o componente *comentários* principal (o sistema de comentários) é o que um autor realmente adiciona à página.

Para estender comentários, você deve:

1. [Criar os componentes](extend-create-components.md)
1. [Adicionar comentário à página de exemplo](extend-sample-page.md)
1. [Alterar a aparência](extend-alter-appearance.md)
