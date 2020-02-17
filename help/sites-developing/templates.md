---
title: Modelos
seo-title: Modelos
description: Os modelos são usados ao criar uma página que será usada como base para a nova página
seo-description: Os modelos são usados ao criar uma página que será usada como base para a nova página
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# Modelos{#templates}

Os modelos são usados em vários pontos no AEM:

* When [creating a page you need to select a template](#templates-pages); this will be used as the base for the new page. The template defines the structure of the resultant page, any initial content and the [components](/help/sites-authoring/default-components.md) that can be used (design properties).

* Ao [criar um fragmento de conteúdo, também é necessário selecionar um modelo](#templates-content-fragments). Este modelo define a estrutura, os elementos iniciais e as variações.

Os seguintes modelos são abordados detalhadamente:

* [Modelos de página - Editável](/help/sites-developing/page-templates-editable.md)
* [Modelos de página - Estáticos](/help/sites-developing/page-templates-static.md)
* [Modelos de fragmento de conteúdo](/help/sites-developing/content-fragment-templates.md)
* [Renderização de modelo adaptável](/help/sites-developing/templates-adaptive-rendering.md)

## Modelos - Páginas {#templates-pages}

O AEM agora oferece dois tipos básicos de modelos para a criação de páginas:

>[!NOTE]
>
>Ao usar um modelo para [criar uma nova página](/help/sites-authoring/managing-pages.md#creating-a-new-page) , não há diferença visível (para o autor da página) e nenhuma indicação do tipo de modelo que está sendo usado.

### Modelos editáveis {#editable-templates}

Modelos editáveis agora são considerados práticas recomendadas para desenvolvimento com o AEM.

As vantagens dos modelos editáveis:

* Podem ser [criados](/help/sites-authoring/templates.md#creating-a-new-template-template-author) e [editados](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) por seus autores.

* Foram introduzidas para permitir que você defina o seguinte para qualquer página criada com o modelo:

   * a estrutura
   * o conteúdo inicial
   * políticas de conteúdo

* Após a criação da nova página, uma conexão dinâmica é mantida entre a página e o modelo; isso significa que as alterações na estrutura do modelo serão refletidas em qualquer página criada com esse modelo (as alterações no conteúdo inicial não serão refletidas).
* Usa políticas de conteúdo (editadas no editor de modelo) para persistir nas propriedades de design (não usa o modo Design no editor de página).
* São armazenados em `/conf`
* Consulte Modelos [editáveis](/help/sites-developing/page-templates-editable.md) para obter mais informações.

>[!NOTE]
>
>Um artigo da comunidade AEM está disponível para explicar como desenvolver um site do Experience Manager com modelos editáveis. Consulte [Criar um site do Adobe Experience Manager 6.5 usando modelos](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html)editáveis.

### Modelos estáticos {#static-templates}

Modelos estáticos:

* Deve ser definido e configurado pelos desenvolvedores.
* Esse era o sistema de modelo original do AEM e estava disponível para muitas versões.
* Um modelo estático é uma hierarquia de nós que tem a mesma estrutura da página a ser criada, mas sem nenhum conteúdo real.
* São copiados para criar a nova página; não há conexão dinâmica após isso.
* Uses [Design Mode](/help/sites-authoring/default-components-designmode.md) to persist design properties.
* São armazenados em `/apps`
* Consulte Modelos [estáticos](/help/sites-developing/page-templates-static.md) para obter mais informações.

>[!NOTE]
>
>A partir do AEM 6.5, o uso de Modelos estáticos não é considerado uma prática recomendada. Em vez disso, use Modelos editáveis.
>
>[As ferramentas de modernização](modernization-tools.md) do AEM podem ajudá-lo a migrar de modelos estáticos para editáveis.

### Disponibilidade do modelo {#template-availability}

>[!CAUTION]
>
>O AEM oferece várias propriedades para controlar os modelos permitidos em **Sites**. No entanto, combiná-las pode levar a regras muito complexas que são difíceis de rastrear e gerenciar.
>
>Portanto, a Adobe recomenda que você comece de forma simples, definindo:
>
>* somente a `cq:allowedTemplates` propriedade
   >
   >
* somente na raiz do site
>
>
Para ver um exemplo, consulte We.Retail: `/content/we-retail/jcr:content`
>
>As propriedades `allowedPaths`, `allowedParents`e `allowedChildren` também podem ser colocadas nos modelos para definir regras mais sofisticadas. No entanto, quando possível, é *muito* mais simples definir outras `cq:allowedTemplates` propriedades em subseções do site se houver necessidade de restringir ainda mais os modelos permitidos.
>
>Uma vantagem adicional é que as `cq:allowedTemplates` propriedades podem ser atualizadas por um autor na guia **Avançado** das Propriedades **da** página. As outras propriedades do modelo não podem ser atualizadas usando a interface do usuário (padrão), portanto, seria necessário um desenvolvedor para manter as regras e uma implantação de código para cada alteração.

Ao criar uma nova página na interface do administrador do site, a lista de modelos disponíveis depende do local da nova página e das restrições de posicionamento especificadas em cada modelo.

As propriedades a seguir determinam se um modelo `T` pode ser usado para uma nova página ser colocada como um filho da página `P`. Cada uma dessas propriedades é uma string de vários valores contendo zero ou mais expressões regulares usadas para correspondência com caminhos:

* A `cq:allowedTemplates` propriedade do `jcr:content` subnó de `P` ou um ancestral de `P`.

* A `allowedPaths` propriedade de `T`.

* A `allowedParents` propriedade de `T`.

* A `allowedChildren` propriedade do modelo de `P`.

A avaliação funciona do seguinte modo:

* A primeira propriedade não vazia encontrada ao aumentar a hierarquia da página que começa com `cq:allowedTemplates` corresponde ao caminho de `P` `T`. Se nenhum dos valores corresponder, `T` será rejeitado.

* Se `T` tiver uma `allowedPaths` propriedade não vazia, mas nenhum dos valores corresponder ao caminho de `P`, `T` será rejeitado.

* Se ambas as propriedades acima estiverem vazias ou inexistentes, `T` será rejeitado, a menos que pertença ao mesmo aplicativo `P`. `T` pertence ao mesmo aplicativo como `P` se e somente se o nome do segundo nível do caminho `T` for o mesmo do nome do segundo nível do caminho `P`. Por exemplo, o modelo `/apps/geometrixx/templates/foo` pertence ao mesmo aplicativo que a página `/content/geometrixx`.

* Se `T` tiver uma `allowedParents` propriedade não vazia, mas nenhum dos valores corresponder ao caminho de `P`, `T` será rejeitado.

* Se o modelo de `P` tiver uma `allowedChildren` propriedade não vazia, mas nenhum dos valores corresponder ao caminho de `T`, `T` será rejeitado.

* Em todos os outros casos, `T` é permitido.

O diagrama a seguir descreve o processo de avaliação do modelo:

![chlimage_1-176](assets/chlimage_1-176.png)

#### Limitação de modelos usados em páginas secundárias {#limiting-templates-used-in-child-pages}

Para limitar quais modelos podem ser usados para criar páginas secundárias em uma determinada página, use a `cq:allowedTemplates` propriedade do nó `jcr:content` da página para especificar a lista de modelos a serem permitidos como páginas secundárias. Cada valor na lista deve ser um caminho absoluto para um modelo para uma página secundária permitida, por exemplo `/apps/geometrixx/templates/contentpage`.

Você pode usar a `cq:allowedTemplates` propriedade no `jcr:content` nó do modelo para aplicar essa configuração a todas as páginas recém-criadas que usam esse modelo.

Se desejar adicionar mais restrições, por exemplo, em relação à hierarquia do modelo, você pode usar as `allowedParents/allowedChildren` propriedades no modelo. Você pode especificar explicitamente que as páginas criadas a partir de um modelo T devem ser pais/filhos de páginas criadas a partir de um modelo T.

## Modelos - Fragmentos de conteúdo {#templates-content-fragments}

Consulte Modelos [de fragmento de](/help/sites-developing/content-fragment-templates.md) conteúdo para obter informações completas.
