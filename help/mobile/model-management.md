---
title: Visão geral de modelos
seo-title: Models Overview
description: Visão geral de modelos
seo-description: null
uuid: e09dac52-9515-43f7-9d3b-6637e2283d59
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: c8281f98-9811-42f7-9a31-f82dd0f09319
exl-id: 50785534-5784-4354-b123-5e640b7c0242
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 0%

---

# Visão geral de modelos{#models-overview}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

O gerenciamento de modelos envolve a criação e o gerenciamento de modelos com a finalidade de associar a objetos de dados eventuais. Cada modelo incluirá todas as propriedades e definições de campo necessárias para facilitar a criação e a renderização de objetos.

O gerenciamento de modelos envolve a criação de **modelos**, **entidades**, e **espaços**. O diagrama a seguir ilustra a relação entre o Conteúdo AEM e os modelos.

![chlimage_1-81](assets/chlimage_1-81.png)

## O modelo de conteúdo {#the-content-model}

Um modelo descreve o tipo de conteúdo e indica quais informações estarão disponíveis para o aplicativo nativo. É uma descrição do que constitui um conteúdo. Um modelo de conteúdo são as regras para criar um conteúdo. O modelo de conteúdo inclui quais dados estão disponíveis, quais ativos podem ser usados, o relacionamento entre ativos e dados, o relacionamento com outros modelos de conteúdo e os metadados disponíveis.

Os modelos também servem como uma maneira de transformar conteúdo AEM existente em objetos que podem ser facilmente usados por aplicativos móveis nativos.

Os Content Services fornecerão alguns modelos prontos para uso para objetos comuns, como ativos, coleções de ativos, páginas de HTML, configurações de aplicativos e páginas independentes de canal. Eles serão configuráveis para atender às necessidades específicas do cliente sem exigir um esforço de desenvolvimento de AEM.

O usuário pode criar seus próprios modelos. Isso permite a criação de novos tipos de conteúdo que ainda não são gerenciados pelo AEM. A criação do modelo é feita por meio de uma interface do usuário usando tipos primitivos existentes.

O diagrama a seguir ilustra o modelo de conteúdo para aplicativos AEM Mobile e como entidades, pastas e espaços são atribuídos a um aplicativo.

![chlimage_1-82](assets/chlimage_1-82.png)

### Os Modelos {#the-models}

Os modelos são usados para determinar como as entidades são criadas. Eles definem o que está disponível em uma entidade e como esses dados são gerados a partir do conteúdo AEM. Antes de começar a trabalhar com Espaços, Pastas e Entidades, você deve estar familiarizado com a criação e o gerenciamento de modelos.

>[!NOTE]
>
>Existe um modelo fora de um aplicativo, pois mais de um aplicativo pode usá-lo.
>

Consulte **[Modelos](/help/mobile/administer-mobile-apps.md)** para criar e gerenciar modelos no painel e no repositório.

### Entidades no modelo de conteúdo {#entities-in-content-model}

Uma entidade é uma instância de um modelo de conteúdo. Uma entidade é exposta por meio da API de serviços de conteúdo à biblioteca do lado do cliente e fornece uma maneira de um aplicativo nativo acessar conteúdo de uma maneira independente de canal.

No caso de conteúdo AEM existente, uma entidade é gerada usando um modelo e a fonte de conteúdo AEM. Por exemplo, uma entidade de página é um objeto independente de canal e layout gerado a partir de uma página AEM e do modelo de página.

As alterações no conteúdo referenciado de uma entidade resultarão em uma alteração na entidade. Por exemplo, se um *cq:page* for atualizada, as entidades baseadas nessa página também serão atualizadas.

Consulte **[Trabalhar com entidades](/help/mobile/spaces-and-entities.md)** para criar entidades personalizadas a partir de modelos.

>[!NOTE]
>
>Se o modelo não corresponder a um conteúdo AEM existente, como o cliente que criou um novo modelo, haverá uma interface do usuário para que um cliente possa criar uma nova entidade.
>

### Espaços no modelo de conteúdo {#spaces-in-content-model}

Um espaço é usado para organizar entidades para fácil acesso. Um espaço pode conter um ou mais tipos de entidade e subpastas.

No lado do AEM, um espaço é uma maneira conveniente de gerenciar entidades relacionadas. Ele também pode ser usado para atribuir permissões de autorização. A autorização pode ser feita para um espaço, que protegerá as entidades que estão nesse espaço.

*Por exemplo*,

Um usuário tem três classificações gerais de entidades. Uma é apenas para uso interno, outra é aprovada para uso público e ainda uma terceira é para entidades comuns usadas por muitos aplicativos. Para facilitar o gerenciamento, o usuário cria três espaços, a saber: *interno*, *público* (com conteúdo em inglês e francês) e *comum* para gerenciar as entidades apropriadas, conforme mencionado abaixo:

* /content/entities/internal
* /content/entities/public/br
* /content/entities/public/fr
* /content/entities/common

Um ponto final de serviço será fornecido ao espaço para que a biblioteca nativa do cliente possa solicitar uma lista do conteúdo de um espaço. Essa &quot;listagem&quot; será retornada como um objeto JSON.

Consulte **[Espaços e entidades](/help/mobile/spaces-and-entities.md)** para criar e publicar espaços.

>[!NOTE]
>
>Um espaço pode ser usado por muitos aplicativos e um aplicativo pode usar muitos espaços.

### Pastas no modelo de conteúdo {#folders-in-content-model}

As pastas permitem que os usuários organizem entidades conforme necessário e facilitam um controle mais fino da ACL. Os espaços podem incluir pastas para ajudar a organizar ainda mais o conteúdo e os ativos do espaço. Um usuário pode criar sua própria hierarquia em um espaço.

Consulte **[Trabalhar com pastas em um espaço](/help/mobile/spaces-and-entities.md)** para criar e gerenciar pastas em um espaço.
