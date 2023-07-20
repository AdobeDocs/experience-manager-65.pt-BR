---
title: Modelos e componentes do aplicativo
description: Siga esta página para saber mais sobre Modelos e componentes de aplicativo. Ele fornece informações detalhadas sobre a estrutura dos templates.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 1%

---

# Modelos e componentes do aplicativo{#app-templates-and-components}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Um Modelo é usado para criar uma Página e define quais componentes podem ser usados dentro do escopo selecionado. Um modelo é uma hierarquia de nós que tem a mesma estrutura da página a ser criada, mas sem nenhum conteúdo real.

Cada modelo apresenta uma seleção de componentes disponíveis para uso.

* Os modelos são criados de [Componentes](/help/sites-developing/components.md);
* Os componentes usam e permitem acesso a Widgets e eles são usados para renderizar o Conteúdo.

>[!NOTE]
>
>Para saber como desenvolver o aplicativo Adobe Experience Manager (AEM) usando o CRXDE Lite, consulte [Desenvolvimento com o CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

Um modelo é a base de uma página.

Para criar uma página, o modelo deve ser copiado (árvore de nó **/apps/&lt;myapp>/templates/&lt;mytemplate>**) para a posição correspondente na árvore do site: isso é o que acontece se uma página é criada usando o **Sites** guia.

Essa ação de cópia também fornece à página seu conteúdo inicial (geralmente, Conteúdo de nível superior somente) e a propriedade sling:resourceType, o caminho para o componente de página usado para renderizar a página (tudo no nó filho jcr:content).

## Estrutura de um modelo {#structure-of-a-template}

Há dois aspectos a considerar:

* a estrutura do próprio modelo
* a estrutura do conteúdo produzido quando um template é usado

Um modelo é criado em um nó do tipo **cq:Template**.

Várias propriedades podem ser definidas, em particular:

* **jcr:title** - título do modelo; aparece na caixa de diálogo ao criar uma página.
* **jcr:description** - descrição do modelo; aparece na caixa de diálogo ao criar uma página.

Este nó contém *um jcr:content (cq:PageContent)* que é usado como base para o nó de conteúdo das páginas resultantes. Isso faz referência, usando *sling:resourceType*, o componente a ser usado para renderizar o conteúdo real de uma nova página.

>[!NOTE]
>
>Para saber mais sobre as noções básicas para modelos e componentes no AEM, consulte os recursos abaixo:
>
>* [Modelos](/help/sites-developing/templates.md)
>* [Componentes](/help/sites-developing/components.md)
>

Depois de ter a compreensão básica de Modelos e Componentes, consulte os seguintes recursos:

* [Criação e adição de modelos e componentes](/help/mobile/mobile-ondemand-app-templates.md)
* [Uso das propriedades de conteúdo para exportar conteúdo](/help/mobile/on-demand-content-properties-exporting.md)
* [Práticas recomendadas](/help/mobile/best-practices-aem-mobile.md)
* [Desenvolvimento dos serviços de conteúdo do AEM Mobile](/help/mobile/developing-content-services.md)

### Recursos adicionais {#additional-resources}

Para saber mais sobre tópicos adicionais sobre aplicativos móveis, consulte os links abaixo:

* [Dispositivo móvel com sincronização de conteúdo](/help/mobile/mobile-ondemand-contentsync.md)
* [Teste de aplicativos móveis](/help/mobile/develop-mobile-apps-testing.md)
