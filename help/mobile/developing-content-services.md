---
title: Content Services
seo-title: Serviços de conteúdo
description: 'null'
seo-description: nulo
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 3%

---


# Content Services{#content-services}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>O recurso Serviços de conteúdo é documentado apenas para fins de pré-visualização.
>
>Ele está sujeito a alterações com a versão 6.3 GA Service Pack 1.

O AEM Mobile Content Services é um recurso leve e leve para solicitar conteúdo gerenciado pela AEM. Isso fornece a todos os desenvolvedores de aplicativos uma maneira de obter conteúdo de alto desempenho sem precisar ter um conhecimento profundo AEM repositório de conteúdo (JCR) e estrutura da Web (Sling). Isso permite que os aplicativos solicitantes sejam dissociados do repositório de conteúdo.

O Content Services apresenta várias construções novas de AEM que permitem que um desenvolvedor acesse AEM conteúdo gerenciado sem conhecer a estrutura do repositório desse conteúdo.

Essas construções são necessárias para manter a flexibilidade e permitir a futura expansão, fornecendo uma camada de abstração entre o conteúdo gerenciado AEM e os aplicativos móveis que consomem o conteúdo. Isso permite que AEM Content Services funcione como uma camada de abstração entre os requisitos de conteúdo do aplicativo nativo e o repositório de conteúdo AEM.

Os Serviços de conteúdo podem fornecer o conteúdo como ativos, HTML empacotado (HTML/CSS/JS) ou como conteúdo independente do canal.

>[!CAUTION]
>
>**Pré-requisitos:**
>
>Antes de começar a usar o Content Services, ative o sinalizador Content Services. Para ativar a criação e o gerenciamento de modelos no aplicativo, é necessário ativar os modelos de dados no Navegador de configuração.
>
>Consulte **[Administração de serviços de conteúdo](/help/mobile/developing-content-services.md)** e a documentação [Navegador de configuração](/help/sites-administering/configurations.md) para obter mais informações.

![chlimage_1-143](assets/chlimage_1-143.png)

Depois de definir o sinalizador de Serviços de conteúdo e os modelos de dados ativados no Navegador de configuração, consulte os recursos abaixo para começar a usar os Serviços de conteúdo da AEM Mobile, familiarize-se com Conceitos de serviços de conteúdo, como gerenciamento de modelo, gerenciamento de entidade seguido de delivery/renderização de conteúdo para os Serviços de conteúdo da AEM Mobile.

* Modelos no repositório
* Renderização e Delivery
