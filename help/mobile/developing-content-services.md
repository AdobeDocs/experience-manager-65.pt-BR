---
title: Serviços de conteúdo
description: Saiba como usar o AEM Mobile Content Services para solicitar conteúdo gerenciado pelo AEM.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
solution: Experience Manager
feature: Mobile
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 1%
---
# Serviços de conteúdo{#content-services}

{{ue-over-mobile}}

>[!CAUTION]
>
>O recurso Serviços de conteúdo é documentado apenas para fins de visualização.
>
>Ela está sujeita a alterações com o lançamento do 6.3 Service Pack 1.

O AEM Mobile Content Services é um recurso leve para solicitar conteúdo gerenciado pelo AEM. Isso fornece a todos os desenvolvedores de aplicativos uma maneira de alto desempenho para recuperar conteúdo sem precisar ter um conhecimento profundo do repositório de conteúdo (JCR) e da estrutura da Web (Sling) da AEM. Ele permite que os aplicativos solicitantes sejam dissociados do repositório de conteúdo.

Os Content Services apresentam várias novas construções do AEM que permitem que um desenvolvedor acesse conteúdo gerenciado pela AEM sem conhecer a estrutura do repositório desse conteúdo.

Essas construções são necessárias para manter a flexibilidade e permitir a expansão futura, fornecendo uma camada de abstração entre o conteúdo gerenciado pela AEM e os aplicativos móveis que consomem o conteúdo. Isso permite que o AEM Content Services funcione como uma camada de abstração entre os requisitos de conteúdo do aplicativo nativo e o repositório de conteúdo do AEM.

Os Serviços de conteúdo podem fornecer o conteúdo como ativos, pacotes de HTML (HTML/CSS/JS) ou como conteúdo independente de canal.

>[!CAUTION]
>
>**Pré-requisitos:**
>
>Antes de começar a usar os Serviços de conteúdo, ative o sinalizador dos Serviços de conteúdo. Para habilitar a criação e o gerenciamento de modelos no seu aplicativo, habilite os modelos de dados no Navegador de configuração.
>
>Consulte **[Administrando o Content Services](/help/mobile/developing-content-services.md)** e a documentação do [Navegador de Configuração](/help/sites-administering/configurations.md) para obter mais informações.

![chlimage_1-143](assets/chlimage_1-143.png)

Depois de definir o sinalizador do Content Services e ativar os modelos de dados no Navegador de configuração, consulte os recursos abaixo para começar a usar o AEM Mobile Content Services. Familiarize-se com os conceitos do Content Services, como gerenciamento de modelos e de entidades, seguidos pela entrega/renderização de conteúdo para o AEM Mobile Content Services.

* Modelos no repositório
* Renderização e entrega
