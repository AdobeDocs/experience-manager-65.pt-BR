---
title: Content Services
seo-title: Content Services
description: Content Services
seo-description: null
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 3%

---

# Content Services{#content-services}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>O recurso Serviços de conteúdo é documentado apenas para fins de visualização.
>
>Está sujeito a alterações com o lançamento do 6.3 GA Service Pack 1.

O AEM Mobile Content Services é um recurso leve e eficiente para solicitar conteúdo gerenciado pelo AEM. Isso fornece a todos os desenvolvedores de aplicativos uma maneira de alto desempenho para recuperar conteúdo sem precisar ter profundo conhecimento do repositório de conteúdo AEM (JCR) e da estrutura da Web (Sling). Ele permite que os aplicativos solicitantes sejam dissociados do repositório de conteúdo.

Os Content Services apresentam várias novas construções de AEM que permitem que um desenvolvedor acesse conteúdo gerenciado por AEM sem conhecer a estrutura do repositório desse conteúdo.

Essas construções são necessárias para manter a flexibilidade e permitir a expansão futura, fornecendo uma camada de abstração entre o conteúdo gerenciado pelo AEM e os aplicativos móveis que consomem o conteúdo. Isso permite que os Serviços de conteúdo AEM funcionem como uma camada de abstração entre os requisitos de conteúdo do aplicativo nativo e o repositório de conteúdo AEM.

Os Serviços de conteúdo podem fornecer o conteúdo como ativos, HTML empacotado (HTML/CSS/JS) ou como conteúdo independente de canal.

>[!CAUTION]
>
>**Pré-requisitos:**
>
>Antes de começar a usar os Serviços de conteúdo, ative o sinalizador dos Serviços de conteúdo. Para habilitar a criação e o gerenciamento de modelos no seu aplicativo, você precisa habilitar os modelos de dados no Navegador de configuração.
>
>Consulte **[Administração dos serviços de conteúdo](/help/mobile/developing-content-services.md)** e a variável [Navegador de configuração](/help/sites-administering/configurations.md) para obter mais informações.

![chlimage_1-143](assets/chlimage_1-143.png)

Depois de definir o sinalizador do Content Services e ativar os modelos de dados no Navegador de configuração, consulte os recursos abaixo para começar a usar o AEM Mobile Content Services, familiarizar-se com os Conceitos do Content Services, como gerenciamento de modelos, gerenciamento de entidades seguido de entrega/renderização de conteúdo para o AEM Mobile Content Services.

* Modelos no repositório
* Renderização e entrega
