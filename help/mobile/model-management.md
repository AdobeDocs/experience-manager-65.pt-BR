---
title: Visão geral dos modelos
seo-title: Visão geral dos modelos
description: 'null'
seo-description: nulo
uuid: e09dac52-9515-43f7-9d3b-6637e2283d59
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: c8281f98-9811-42f7-9a31-f82dd0f09319
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---


# Visão geral dos modelos{#models-overview}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

O gerenciamento de modelos envolve a criação e o gerenciamento de modelos com o objetivo de associar a eventuais objetos de dados. Cada modelo incluirá todas as propriedades e definições de campo necessárias para facilitar a criação e renderização de objetos.

O Gerenciamento de modelos envolve a criação de **modelos**, **entidades** e **espaços**. O diagrama a seguir ilustra a relação entre o Conteúdo do AEM e os modelos.

![chlimage_1-81](assets/chlimage_1-81.png)

## O Modelo de conteúdo {#the-content-model}

Um modelo descreve o tipo de conteúdo e indica quais informações estarão disponíveis para o aplicativo nativo. É uma descrição do que constitui um conteúdo. Um modelo de conteúdo são as regras para criar um conteúdo. O modelo de conteúdo inclui quais dados estão disponíveis, quais ativos podem ser usados, a relação entre ativos e dados, a relação com outros modelos de conteúdo e os metadados disponíveis.

Os modelos também servem como uma forma de transformar conteúdo AEM existente em objetos que podem ser facilmente usados por aplicativos móveis nativos.

Os Serviços de conteúdo fornecerão alguns modelos prontos para uso para objetos comuns, como ativos, coleções de ativos, páginas HTML, configurações de aplicativos e páginas independentes de canais. Elas serão configuráveis para atender às necessidades específicas do cliente sem exigir um esforço de desenvolvimento AEM.

O usuário pode criar seus próprios modelos. Isso permite a criação de novos tipos de conteúdo que ainda não são gerenciados pela AEM. A criação do modelo é feita por meio de uma interface do usuário usando tipos primitivos existentes.

O diagrama a seguir ilustra o modelo de conteúdo para aplicativos AEM Mobile e como entidades, pastas e espaços são atribuídos a um aplicativo.

![chlimage_1-82](assets/chlimage_1-82.png)

### Os modelos {#the-models}

Os modelos são usados para determinar como as entidades são criadas. Eles definem o que está disponível em uma entidade e como esses dados são gerados AEM conteúdo. Antes de se start de trabalhar com Espaços, Pastas e Entidades, você deve se familiarizar com a criação e o gerenciamento de modelos.

>[!NOTE]
>
>Existe um modelo fora de um aplicativo, pois mais de um aplicativo pode usá-lo.


Consulte **[Modelos](/help/mobile/administer-mobile-apps.md)** para criar e gerenciar modelos no painel e no repositório.

### Entidades no Modelo de conteúdo {#entities-in-content-model}

Uma entidade é uma instância de um modelo de conteúdo. Uma entidade é exposta por meio da Content Services API à biblioteca do lado do cliente e fornece uma maneira de um aplicativo nativo acessar o conteúdo de forma independente do canal.

No caso de conteúdo AEM existente, uma entidade é gerada usando um modelo e a fonte de conteúdo AEM. Por exemplo, uma entidade de página é um objeto independente de canal e layout que é gerado de uma página AEM e do modelo de página.

As alterações no conteúdo referenciado de uma entidade resultarão em uma alteração na entidade. Por exemplo, se um *cq:page* for atualizado, todas as entidades baseadas nessa página também serão atualizadas.

Consulte **[Trabalhando com Entidades](/help/mobile/spaces-and-entities.md)** para criar entidades personalizadas a partir de modelos.

>[!NOTE]
>
>Se o modelo não corresponder a um conteúdo AEM existente, como o cliente criou um novo modelo, haverá uma interface do usuário para que o cliente possa criar uma nova entidade.


### Espaços no Modelo de conteúdo {#spaces-in-content-model}

Um espaço é usado para organizar entidades para fácil acesso. Um espaço pode conter um ou mais tipos de entidade e pode conter subpastas.

Do lado AEM, um espaço é uma maneira conveniente de gerenciar entidades relacionadas. Também pode ser usado para atribuir permissões de autorização. A autorização pode ser feita num espaço, que protegerá então as entidades que estão nesse espaço.

*Por exemplo*,

Um usuário tem três classificações gerais de entidades. Um é apenas para uso interno, outro é aprovado para uso público e ainda um terceiro é para entidades comuns que são usadas por muitos aplicativos. Para facilitar o gerenciamento, o usuário cria três espaços: *internal*, *public* (com conteúdo em inglês e francês) e *common* para gerenciar as entidades apropriadas, conforme mencionado abaixo:

* /content/entity/internal
* /content/entity/public/en
* /content/entity/public/fr
* /content/entity/common

Um ponto final de serviço será fornecido ao espaço para que a biblioteca cliente nativa possa solicitar uma lista do conteúdo de um espaço. Essa &quot;listagem&quot; será retornada como um objeto JSON.

Consulte **[Espaços e Entidades](/help/mobile/spaces-and-entities.md)** para criar e publicar espaços.

>[!NOTE]
>
>Um espaço pode ser usado por muitos aplicativos e um aplicativo pode usar muitos espaços.

### Pastas no Modelo de conteúdo {#folders-in-content-model}

As pastas permitem que os usuários organizem as entidades conforme necessário e facilitam um controle ACL mais refinado. Os espaços podem incluir pastas para ajudar a organizar ainda mais o conteúdo e os ativos do espaço. Um usuário pode criar sua própria hierarquia em um espaço.

Consulte **[Trabalhar com pastas em um espaço](/help/mobile/spaces-and-entities.md)** para criar e gerenciar pastas em um espaço.
