---
title: Modelos
seo-title: Templates
description: Os modelos são usados ao criar uma página que será usada como a base para a nova página
seo-description: Templates are used when creating a page which will be used as the base for the new page
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 1%

---

# Modelos{#templates}

Os modelos são usados em vários pontos do AEM:

* When [criação de uma página que você precisa selecionar um template](#templates-pages); isso será usado como a base para a nova página. O modelo define a estrutura da página resultante, qualquer conteúdo inicial e a variável [componentes](/help/sites-authoring/default-components.md) que podem ser usadas (propriedades de design).

* When [criar um Fragmento do conteúdo, você também precisa selecionar um modelo](#templates-content-fragments). Esse template define a estrutura, os elementos iniciais e as variações.

Os seguintes modelos são abordados detalhadamente:

* [Modelos de página - Editável](/help/sites-developing/page-templates-editable.md)
* [Modelos de página - Estático](/help/sites-developing/page-templates-static.md)
* [Modelos de fragmentos do conteúdo](/help/sites-developing/content-fragment-templates.md)
* [Renderização do modelo adaptável](/help/sites-developing/templates-adaptive-rendering.md)

## Modelos - Páginas {#templates-pages}

O AEM agora oferece dois tipos básicos de modelos para a criação de páginas:

>[!NOTE]
>
>Ao usar um modelo para [criar uma nova página](/help/sites-authoring/managing-pages.md#creating-a-new-page) não há diferença visível (para o autor da página) e nenhuma indicação do tipo de modelo que está sendo usado.

### Modelos editáveis {#editable-templates}

Os modelos editáveis agora são considerados práticas recomendadas para desenvolvimento com AEM.

As vantagens dos Modelos editáveis:

* Pode ser [criado](/help/sites-authoring/templates.md#creating-a-new-template-template-author) e [editado](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) pelos seus autores.

* Foram introduzidas para permitir definir o seguinte para qualquer página criada com o modelo:

   * a estrutura
   * o conteúdo inicial
   * políticas de conteúdo

* Após a criação da nova página, uma conexão dinâmica é mantida entre a página e o modelo; isso significa que as alterações na estrutura do modelo serão refletidas em qualquer página criada com esse modelo (as alterações no conteúdo inicial não serão refletidas).
* Usa as políticas de conteúdo (editadas no editor de modelos) para manter as propriedades de design (não usa o modo Design no editor de páginas).
* São armazenadas em `/conf`
* Consulte [Modelos editáveis](/help/sites-developing/page-templates-editable.md) para obter mais informações.

>[!NOTE]
>
>Um AEM Community Article está disponível para explicar como desenvolver um site Experience Manager com Modelos editáveis, consulte [Criação de um site do Adobe Experience Manager 6.5 usando modelos editáveis](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html).

### Modelos estáticos {#static-templates}

Modelos estáticos:

* Deve ser definido e configurado pelos desenvolvedores.
* Esse era o sistema de modelos original de AEM e estava disponível para muitas versões.
* Um modelo estático é uma hierarquia de nós que tem a mesma estrutura que a página a ser criada, mas sem nenhum conteúdo real.
* São copiados para criar a nova página, não existe nenhuma conexão dinâmica depois disso.
* Usos [Modo Design](/help/sites-authoring/default-components-designmode.md) para manter as propriedades de design.
* São armazenadas em `/apps`
* Consulte [Modelos estáticos](/help/sites-developing/page-templates-static.md) para obter mais informações.

>[!NOTE]
>
>A partir do AEM 6.5, o uso de Modelos estáticos não é considerado uma prática recomendada. Em vez disso, use Modelos editáveis.
>
>[Modernização AEM](modernization-tools.md) As ferramentas podem ajudá-lo a migrar de modelos estáticos para editáveis.

### Disponibilidade de modelo {#template-availability}

>[!CAUTION]
>
>AEM oferece várias propriedades para controlar os modelos permitidos em **Sites**. No entanto, combiná-las pode levar a regras muito complexas, que são difíceis de rastrear e gerenciar.
>
>Portanto, o Adobe recomenda que você comece de forma simples, definindo:
>
>* somente a variável `cq:allowedTemplates` propriedade
>
>* somente na raiz do site
>
>Para obter um exemplo, consulte We.Retail: `/content/we-retail/jcr:content`
>
>As propriedades `allowedPaths`, `allowedParents`e `allowedChildren` também pode ser colocado nos templates para definir regras mais sofisticadas. No entanto, quando possível, é *many* mais simples de definir `cq:allowedTemplates` propriedades nas subseções do site se houver a necessidade de restringir ainda mais os modelos permitidos.
>
>Uma vantagem adicional é que a variável `cq:allowedTemplates` As propriedades podem ser atualizadas por um autor na função **Avançado** da guia **Propriedades da página**. As outras propriedades do modelo não podem ser atualizadas usando a interface do usuário (padrão), portanto, seria necessário um desenvolvedor para manter as regras e uma implantação de código para cada alteração.

Ao criar uma nova página na interface de administração do site, a lista de modelos disponíveis depende do local da nova página e das restrições de posicionamento especificadas em cada modelo.

As seguintes propriedades determinam se um modelo `T` pode ser usada para que uma nova página seja colocada como filho de página `P`. Cada uma dessas propriedades é uma string com vários valores, contendo zero ou mais Expressões Regulares, usadas para correspondência com caminhos:

* O `cq:allowedTemplates` da `jcr:content` subnó de `P` ou um antepassado de `P`.

* O `allowedPaths` propriedade de `T`.

* O `allowedParents` propriedade de `T`.

* O `allowedChildren` propriedade do modelo de `P`.

A avaliação funciona do seguinte modo:

* O primeiro não vazio `cq:allowedTemplates` propriedade encontrada ao ascender a hierarquia de página começando com `P` corresponde ao caminho de `T`. Se nenhum dos valores corresponder, `T` é rejeitada.

* If `T` tem um não vazio `allowedPaths` , mas nenhum dos valores corresponde ao caminho de `P`, `T` é rejeitada.

* Se ambas as propriedades acima estiverem vazias ou inexistentes, `T` é rejeitada, a menos que pertença ao mesmo pedido que `P`. `T` pertence ao mesmo aplicativo que `P` se e somente se o nome do segundo nível do caminho de `T` é igual ao nome do segundo nível do caminho de `P`. Por exemplo, o modelo `/apps/geometrixx/templates/foo` pertence ao mesmo aplicativo que a página `/content/geometrixx`.

* If `T` tem um não vazio `allowedParents` , mas nenhum dos valores corresponde ao caminho de `P`, `T` é rejeitada.

* Se o modelo de `P` tem um não vazio `allowedChildren` , mas nenhum dos valores corresponde ao caminho de `T`, `T` é rejeitada.

* Em todos os outros casos, `T` é permitido.

O diagrama a seguir descreve o processo de avaliação do template:

![chlimage_1-176](assets/chlimage_1-176.png)

#### Limitação de modelos usados em páginas filhas {#limiting-templates-used-in-child-pages}

Para limitar quais modelos podem ser usados para criar páginas filhas em uma determinada página, use o `cq:allowedTemplates` propriedade de `jcr:content` nó da página para especificar a lista de modelos a serem permitidos como páginas secundárias. Cada valor na lista deve ser um caminho absoluto para um modelo para uma página secundária permitida, por exemplo `/apps/geometrixx/templates/contentpage`.

Você pode usar o `cq:allowedTemplates` na propriedade do modelo  `jcr:content` para que essa configuração seja aplicada a todas as páginas recém-criadas que usam esse modelo.

Se quiser adicionar mais restrições, por exemplo, em relação à hierarquia do modelo, use a variável `allowedParents/allowedChildren` propriedades no modelo. Você pode especificar explicitamente que as páginas criadas a partir de um modelo T devem ser pais/filhos de páginas criadas a partir de um modelo T.

## Modelos - Fragmentos de conteúdo {#templates-content-fragments}

Consulte [Modelos de fragmentos do conteúdo](/help/sites-developing/content-fragment-templates.md) para obter informações completas.
