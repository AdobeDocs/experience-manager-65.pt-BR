---
title: Content Services
seo-title: Content Services
description: 'null'
seo-description: 'null'
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Content Services{#content-services}

>[!NOTE]
>
>A Adobe recomenda usar o Editor SPA para projetos que exigem renderização do lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>O recurso Serviços de conteúdo é documentado apenas para fins de visualização.
>
>Ele está sujeito a alterações com a versão 6.3 GA Service Pack 1.

O AEM Mobile Content Services é um recurso leve e leve para solicitar conteúdo gerenciado pelo AEM. Isso fornece a todos os desenvolvedores de aplicativos uma maneira de obter conteúdo de alto desempenho sem precisar ter um conhecimento profundo do repositório de conteúdo (JCR) e da estrutura da Web (Sling) do AEM. Isso permite que os aplicativos solicitantes sejam dissociados do repositório de conteúdo.

Os Serviços de conteúdo apresentam várias novas construções do AEM que permitem que um desenvolvedor acesse conteúdo gerenciado pelo AEM sem conhecer a estrutura do repositório desse conteúdo.

Essas construções são necessárias para manter a flexibilidade e permitir a futura expansão, fornecendo uma camada de abstração entre o conteúdo gerenciado pelo AEM e os aplicativos móveis que usam o conteúdo. Isso permite que o AEM Content Services funcione como uma camada de abstração entre os requisitos de conteúdo do aplicativo nativo e o repositório de conteúdo do AEM.

Os Serviços de conteúdo podem fornecer o conteúdo como ativos, HTML empacotado (HTML/CSS/JS) ou como conteúdo independente de canal.

>[!CAUTION]
>
>**Pré-requisitos:**
>
>Antes de começar a usar o Content Services, ative o sinalizador Content Services. Para ativar a criação e o gerenciamento de modelos no aplicativo, é necessário ativar modelos de dados no Navegador de configuração.
>
>Consulte **[Administração de serviços](/help/mobile/developing-content-services.md)**de conteúdo para obter detalhes.

![chlimage_1-143](assets/chlimage_1-143.png)

Depois de definir o sinalizador Content Services e os modelos de dados ativados no Navegador de configuração, consulte os recursos abaixo para começar a usar o AEM Mobile Content Services, familiarize-se com Conceitos do Content Services, como gerenciamento de modelo, gerenciamento de entidades seguido de entrega/renderização de conteúdo para o AEM Mobile Content Services.

* Modelos no repositório
* Renderização e entrega

