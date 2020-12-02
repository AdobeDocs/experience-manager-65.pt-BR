---
title: Modelos e componentes do aplicativo
seo-title: Modelos e componentes do aplicativo
description: Siga esta página para saber mais sobre Modelos e componentes do aplicativo. Ele fornece informações detalhadas sobre a estrutura dos modelos.
seo-description: Siga esta página para saber mais sobre Modelos e componentes do aplicativo. Ele fornece informações detalhadas sobre a estrutura dos modelos.
uuid: ba2fd91b-de5a-4f39-a976-5455f9983669
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 7f31c6a7-92d5-4a87-a9f0-68a82b834d5a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 1%

---


# Modelos e componentes do aplicativo{#app-templates-and-components}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Um Modelo é usado para criar uma Página e define quais componentes podem ser usados dentro do escopo selecionado. Um modelo é uma hierarquia de nós que tem a mesma estrutura que a página a ser criada, mas sem nenhum conteúdo real.

Cada modelo apresentará uma seleção de componentes disponíveis para uso.

* Os modelos são construídos de [Components](/help/sites-developing/components.md);
* Os componentes usam e permitem acesso a Widgets, e esses são usados para renderizar o Conteúdo.

>[!NOTE]
>
>Para saber como desenvolver seu aplicativo AEM usando o CRXDE Lite, consulte [Desenvolvimento com CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

Um modelo é a base de uma página.

Para criar uma página, o modelo deve ser copiado (node-tree **/apps/&lt;myapp>/models/&lt;mytemplate>**) para a posição correspondente na árvore do site: isso é o que acontece se uma página for criada usando a guia **Sites**.

Essa ação de cópia também fornece à página seu conteúdo inicial (normalmente, somente conteúdo de nível superior) e a propriedade sling:resourceType, o caminho para o componente de página que é usado para renderizar a página (tudo no nó filho jcr:content).

## Estrutura de um Modelo {#structure-of-a-template}

Há dois aspectos a considerar:

* a estrutura do próprio modelo
* a estrutura do conteúdo produzido quando um modelo é usado

Um Modelo é criado em um nó do tipo **cq:Template**.

Podem ser definidas várias propriedades, em especial:

* **jcr:title** - title para o modelo; aparece na caixa de diálogo ao criar uma página.
* **jcr:description** - descrição do modelo; aparece na caixa de diálogo ao criar uma página.

Este nó contém *um nó jcr:content (cq:PageContent)* que pode ser usado como a base para o nó de conteúdo das páginas resultantes; isso faz referência, usando *sling:resourceType*, ao componente a ser usado para renderizar o conteúdo real de uma nova página.

>[!NOTE]
>
>Para saber mais sobre as noções básicas de modelos e componentes no AEM, consulte os recursos abaixo:
>
>* [Modelos](/help/sites-developing/templates.md)
>* [Componentes](/help/sites-developing/components.md)

>



Depois de ter a compreensão básica de Modelos e componentes, consulte os seguintes recursos:

* [Criação e adição de modelos e componentes](/help/mobile/mobile-ondemand-app-templates.md)
* [Uso das propriedades do conteúdo para exportar conteúdo](/help/mobile/on-demand-content-properties-exporting.md)
* [Práticas recomendadas    ](/help/mobile/best-practices-aem-mobile.md)
* [Desenvolvimento dos serviços de conteúdo da AEM Mobile](//help/mobile/developing-content-services.md)

### Recursos adicionais {#additional-resources}

Para saber mais sobre tópicos adicionais em aplicativos móveis, consulte os links abaixo:

* [Mobile com sincronização de conteúdo](/help/mobile/mobile-ondemand-contentsync.md)
* [Testar aplicativos móveis](/help/mobile/develop-mobile-apps-testing.md)

