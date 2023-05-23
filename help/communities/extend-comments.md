---
title: Estender componente de comentários
seo-title: Extend Comments Component
description: Estender o componente Comentários para alterar sua aparência ou comportamento para usos específicos
seo-description: Extend the Comments component to alter its appearance or behavior for specific uses
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Estender componente de comentários  {#extend-comments-component}

A intenção da [extensão](client-customize.md#extensions) um componente padrão é alterar a aparência ou o comportamento de um componente para usos específicos.

O caminho para o componente é exclusivo e faz referência ao componente padrão como um tipo de super recurso. Há menos risco, pois o escopo é limitado em comparação ao escopo global de uma sobreposição de componente.

>[!NOTE]
>
>Extensão de um [sobreposto](client-customize.md#overlays) não há suporte para o componente.

## Exemplo {#example}

Suponha que o cabeçalho do componente de comentário deve ser exibido com uma aparência alternativa em um site da instância do AEM, enquanto aparece com a exibição padrão em outro site. Em vez de sobrepor o comentário padrão, que altera o componente de comentário para todas as instâncias, uma solução melhor é garantir que haja vários componentes de comentário disponíveis para uso em vários sites.

Para implementar esta solução, crie um novo componente que estenda (substitua) o existente e modifique o script Handlebars. A área do site que usa os novos comentários pode usar o estendido, enquanto os sites que usam a aparência padrão permanecem inalterados.

O componente de comentários é, na verdade, um dos dois componentes que compõem o sistema de comentários. Portanto, há dois componentes a serem estendidos: *comentários* e *comentário*. O script a ser editado está na *comentário* do componente `header.hbs` arquivo, enquanto o pai *comentários* O componente (o sistema de comentários) é o que um autor realmente adiciona à página.

Para estender comentários, é necessário:

1. [Criar os componentes](extend-create-components.md)
1. [Adicionar comentário à página de exemplo](extend-sample-page.md)
1. [Alterar a aparência](extend-alter-appearance.md)
