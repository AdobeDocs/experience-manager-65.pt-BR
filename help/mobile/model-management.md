---
title: Visão geral de modelos
description: Saiba como usar o gerenciamento de modelos que envolve a criação e o gerenciamento de modelos para associação com eventuais objetos de dados.
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 50785534-5784-4354-b123-5e640b7c0242
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# Visão geral de modelos{#models-overview}

{{ue-over-mobile}}

O gerenciamento de modelos envolve a criação e o gerenciamento de modelos para associação com eventuais objetos de dados. Cada modelo inclui todas as propriedades e definições de campo necessárias para facilitar a criação e a renderização de objetos.

O Gerenciamento de Modelos envolve a criação de **modelos**, **entidades** e **espaços**. O diagrama a seguir ilustra a relação entre o Conteúdo AEM e os modelos.

![chlimage_1-81](assets/chlimage_1-81.png)

## O modelo de conteúdo {#the-content-model}

Um modelo descreve o tipo de conteúdo e indica quais informações estão disponíveis para o aplicativo nativo. É uma descrição do que constitui um conteúdo. Um modelo de conteúdo são as regras para criar um conteúdo. O modelo de conteúdo inclui quais dados estão disponíveis, quais ativos podem ser usados, o relacionamento entre ativos e dados, o relacionamento com outros modelos de conteúdo e os metadados disponíveis.

Os modelos também servem como uma maneira de transformar conteúdo AEM existente em objetos que podem ser facilmente usados por aplicativos móveis nativos.

Os Content Services fornecem alguns modelos prontos para uso para objetos comuns, como ativos, coleções de ativos, páginas de HTML, configurações de aplicativos e páginas independentes de canal. Eles são configuráveis para atender às necessidades específicas do cliente sem exigir um esforço de desenvolvimento de AEM.

Os usuários podem criar seus próprios modelos. Isso permite a criação de novos tipos de conteúdo que ainda não são gerenciados pelo AEM. A criação do modelo é feita por meio de uma interface do usuário usando tipos primitivos existentes.

O diagrama a seguir ilustra o modelo de conteúdo para aplicativos AEM Mobile e como entidades, pastas e espaços são atribuídos a um aplicativo.

![chlimage_1-82](assets/chlimage_1-82.png)

### Os Modelos {#the-models}

Os modelos são usados para determinar como as entidades são criadas. Eles definem o que está disponível em uma entidade e como esses dados são gerados a partir do conteúdo AEM. Antes de começar a trabalhar com Espaços, Pastas e Entidades, você deve estar familiarizado com a criação e o gerenciamento de modelos.

>[!NOTE]
>
>Existe um modelo fora de um aplicativo, pois mais de um aplicativo pode usá-lo.
>

Para criar e gerenciar modelos no painel e no repositório, consulte **[Modelos](/help/mobile/administer-mobile-apps.md)**.

### Entidades no modelo de conteúdo {#entities-in-content-model}

Uma entidade é uma instância de um modelo de conteúdo. Uma entidade é exposta por meio da API de serviços de conteúdo à biblioteca do lado do cliente e fornece uma maneira de um aplicativo nativo acessar conteúdo de forma independente de canal.

Se houver conteúdo de AEM existente, uma entidade é gerada usando um modelo e a fonte de conteúdo de AEM. Por exemplo, uma entidade de página é um objeto independente de canal e layout gerado a partir de uma página AEM e do modelo de página.

As alterações no conteúdo referenciado de uma entidade resultam em uma alteração na entidade. Por exemplo, se uma *cq:page* for atualizada, quaisquer entidades baseadas nessa página também serão atualizadas.

Para criar entidades personalizadas a partir de modelos, consulte **[Trabalhando com Entidades](/help/mobile/spaces-and-entities.md)**.

>[!NOTE]
>
>Se o modelo não corresponder a um conteúdo AEM existente, como o cliente criou um modelo, então há uma interface do usuário para que um cliente possa criar uma entidade.
>

### Espaços no modelo de conteúdo {#spaces-in-content-model}

Um espaço é usado para organizar entidades para fácil acesso. Um espaço pode conter um ou mais tipos de entidade e subpastas.

No lado do AEM, um espaço é uma maneira conveniente de gerenciar entidades relacionadas. Ele também pode ser usado para atribuir permissões de autorização. A autorização pode ser feita para um espaço, que protege as entidades que estão nesse espaço.

*Por exemplo*,

Um usuário tem três classificações gerais de entidades. Uma é apenas para uso interno, outra é aprovada para uso público e ainda uma terceira é para entidades comuns usadas por muitos aplicativos. Para facilitar o gerenciamento, o usuário cria três espaços: *interno*, *público* (com conteúdo em inglês e francês) e *comum* para gerenciar as entidades apropriadas, conforme mencionado abaixo:

* /content/entities/internal
* /content/entities/public/br
* /content/entities/public/fr
* /content/entities/common

Um ponto final de serviço é fornecido ao espaço para que a biblioteca nativa do cliente possa solicitar uma lista do conteúdo de um espaço. Essa &quot;listagem&quot; é retornada como um objeto JSON.

Consulte **[Espaços e Entidades](/help/mobile/spaces-and-entities.md)** para criar e publicar espaços.

>[!NOTE]
>
>Um espaço pode ser usado por muitos aplicativos e um aplicativo pode usar muitos espaços.

### Pastas no modelo de conteúdo {#folders-in-content-model}

As pastas permitem que os usuários organizem entidades conforme necessário e facilitam um controle mais fino da ACL. Os espaços podem incluir pastas para ajudar a organizar ainda mais o conteúdo e os ativos do espaço. Um usuário pode criar sua própria hierarquia em um espaço.

Para criar e gerenciar pastas em um espaço, consulte **[Trabalhando com Pastas em um Espaço](/help/mobile/spaces-and-entities.md)**.
