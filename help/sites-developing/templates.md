---
title: Modelos
description: Os modelos são usados ao criar uma página que é usada como base para a nova página.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# Modelos{#templates}

Modelos são usados em vários pontos no AEM:

* [Ao criar uma página, selecione um modelo](#templates-pages). Esse modelo é usado como base para a nova página. O modelo define a estrutura da página, qualquer conteúdo inicial e o [componentes](/help/sites-authoring/default-components.md) que podem ser usadas (propriedades de design).

* [Ao criar um fragmento de conteúdo, você também seleciona um modelo](#templates-content-fragments). Esse template define a estrutura, os elementos iniciais e as variações.

Os seguintes templates são abordados em detalhes:

* [Modelos de página - Editável](/help/sites-developing/page-templates-editable.md)
* [Modelos de página - Estáticos](/help/sites-developing/page-templates-static.md)
* [Modelos de fragmentos do conteúdo](/help/sites-developing/content-fragment-templates.md)
* [Renderização adaptável do modelo](/help/sites-developing/templates-adaptive-rendering.md)

## Modelos - Páginas {#templates-pages}

O AEM agora oferece dois tipos básicos de modelos para a criação de páginas:

>[!NOTE]
>
>Ao usar um modelo para [criar uma página](/help/sites-authoring/managing-pages.md#creating-a-new-page), não há diferença visível (para o autor da página) e nenhuma indicação do tipo de modelo que está sendo usado.

### Modelos editáveis {#editable-templates}

Os modelos editáveis agora são considerados práticas recomendadas para desenvolvimento com AEM.

As vantagens dos Modelos editáveis:

* Pode ser [criado](/help/sites-authoring/templates.md#creating-a-new-template-template-author) e [editado](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) pelos seus autores.

* Foram introduzidos para permitir que você defina o seguinte para qualquer página criada com o modelo:

   * a estrutura
   * o conteúdo inicial
   * políticas de conteúdo

* Após a criação da nova página, uma conexão dinâmica é mantida entre a página e o modelo. Essa conexão significa que as alterações na estrutura do modelo são refletidas em qualquer página criada com esse modelo; as alterações no conteúdo inicial não são refletidas.
* Usa políticas de conteúdo (editadas pelo editor de modelo) para manter as propriedades de design (não usa o modo Design no editor de páginas).
* São armazenados em `/conf`
* Consulte [Modelos editáveis](/help/sites-developing/page-templates-editable.md) para obter mais informações.

>[!NOTE]
>
>Consulte [Utilização de modelos de página editáveis para desenvolver um site de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html?lang=pt-BR).

### Modelos estáticos {#static-templates}

Modelos estáticos:

* Deve ser definido e configurado pelos desenvolvedores.
* O sistema de modelo original do AEM que está disponível para muitas versões.
* Um modelo estático é uma hierarquia de nós que tem a mesma estrutura que a página a ser criada, mas sem nenhum conteúdo real.
* São copiados para criar a página; não existe conexão dinâmica depois.
* Usos [Modo Design](/help/sites-authoring/default-components-designmode.md) para manter as propriedades de design.
* São armazenados em `/apps`
* Consulte [Modelos estáticos](/help/sites-developing/page-templates-static.md) para obter mais informações.

>[!NOTE]
>
>A partir do AEM 6.5, o uso de Modelos estáticos não é considerado uma prática recomendada. Em vez disso, use Modelos editáveis.
>
>[Modernização do AEM](modernization-tools.md) As ferramentas do podem ajudar a migrar de modelos estáticos para editáveis.

### Disponibilidade de modelo {#template-availability}

>[!CAUTION]
>
>O AEM oferece várias propriedades para controlar os modelos permitidos em **Sites**. No entanto, combiná-los pode levar a regras complexas que são difíceis de rastrear e gerenciar.
>
>Portanto, o Adobe recomenda que você comece de forma simples, definindo:
>
>* somente o `cq:allowedTemplates` propriedade
>
>* somente na raiz do site
>
>Para obter um exemplo, consulte We.Retail: `/content/we-retail/jcr:content`
>
>As propriedades `allowedPaths`, `allowedParents`, e `allowedChildren` O também pode ser colocado nos modelos para definir regras mais sofisticadas. No entanto, sempre que possível, *muito* mais simples de definir `cq:allowedTemplates` propriedades nas subseções do site se houver necessidade de restringir ainda mais os modelos permitidos.
>
>Uma vantagem extra é que o `cq:allowedTemplates` as propriedades podem ser atualizadas por um autor na **Avançado** guia do **Propriedades da página**. As outras propriedades do template não podem ser atualizadas usando a interface do usuário (padrão), portanto, seria necessário um desenvolvedor para manter as regras e uma implantação de código para cada alteração.

Ao criar uma página na interface do administrador do site, a lista de modelos disponíveis depende do local da nova página e das restrições de posicionamento especificadas em cada modelo.

As propriedades a seguir determinam se um modelo `T` é usado para que uma nova página seja colocada como secundária da página `P`. Cada uma dessas propriedades é uma string de vários valores que contém zero ou mais expressões regulares usadas para correspondência com caminhos:

* A variável `cq:allowedTemplates` propriedade do `jcr:content` subnó de `P` ou um ancestral de `P`.

* A variável `allowedPaths` propriedade de `T`.

* A variável `allowedParents` propriedade de `T`.

* A variável `allowedChildren` propriedade do modelo de `P`.

A avaliação funciona da seguinte forma:

* O primeiro não vazio `cq:allowedTemplates` propriedade encontrada ao aumentar a hierarquia de páginas que começa com `P` corresponde ao caminho de `T`. Se nenhum dos valores for correspondente, `T` foi rejeitada.

* Se `T` tem um não vazio `allowedPaths` propriedade, mas nenhum dos valores corresponde ao caminho de `P`, `T` foi rejeitada.

* Se ambas as propriedades acima estiverem vazias ou não existirem, `T` é rejeitada, a menos que pertença ao mesmo aplicativo que `P`. `T` pertence ao mesmo aplicativo que `P` se e somente se o nome do segundo nível do caminho de `T` é o mesmo que o nome do segundo nível do caminho de `P`. Por exemplo, o template `/apps/geometrixx/templates/foo` pertence ao mesmo aplicativo que a página `/content/geometrixx`.

* Se `T` tem um não vazio `allowedParents` propriedade, mas nenhum dos valores corresponde ao caminho de `P`, `T` foi rejeitada.

* Se o modelo de `P` tem um não vazio `allowedChildren` propriedade, mas nenhum dos valores corresponde ao caminho de `T`, `T` foi rejeitada.

* Em todos os outros casos, `T` é permitido.

O diagrama a seguir descreve o processo de avaliação do modelo:

![chlimage_1-176](assets/chlimage_1-176.png)

#### Limite de modelos usados em páginas secundárias {#limiting-templates-used-in-child-pages}

Para limitar quais modelos podem ser usados para criar páginas secundárias em uma determinada página, use o `cq:allowedTemplates` propriedade de `jcr:content` nó da página para especificar a lista de modelos que podem ser páginas secundárias. Cada valor na lista deve ser um caminho absoluto para um modelo de uma página secundária permitida, por exemplo, `/apps/geometrixx/templates/contentpage`.

Você pode usar o `cq:allowedTemplates` propriedade no modelo  `jcr:content` para que esta configuração seja aplicada a todas as páginas recém-criadas que usam este modelo.

Se quiser adicionar mais restrições, por exemplo, em relação à hierarquia do template, você poderá usar o `allowedParents/allowedChildren` propriedades no modelo. Em seguida, é possível especificar explicitamente que as páginas criadas a partir de um modelo T devem ser páginas principais/secundárias das páginas criadas a partir de um modelo T.

## Modelos - Fragmentos de conteúdo {#templates-content-fragments}

Consulte [Modelos de fragmentos do conteúdo](/help/sites-developing/content-fragment-templates.md).
