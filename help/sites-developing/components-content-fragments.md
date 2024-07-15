---
title: Componentes para fragmentos de conteúdo
description: Os fragmentos de conteúdo do Adobe Experience Manager (AEM) são criados e gerenciados como ativos independentes da página
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
solution: Experience Manager, Experience Manager Sites
feature: Developing,Content Fragments
role: Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Componentes para fragmentos de conteúdo{#components-for-content-fragments}

## Componentes para criação de fragmentos {#components-for-fragment-authoring}

>[!CAUTION]
>
>Não é recomendável estender ou alterar os componentes reais usados no Editor de fragmentos, pois eles ainda estão sujeitos a alterações.

Consulte a [API de gerenciamento de fragmento de conteúdo - lado do cliente](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## Componentes para criação de página {#components-for-page-authoring}

>[!CAUTION]
>
>O [Componente principal do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=pt-BR) agora é recomendado. Consulte [Desenvolvendo componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html) para obter mais detalhes.
>
>Esta seção detalha o componente original entregue para uso com fragmentos de conteúdo (**Fragmento de Conteúdo** no grupo **Geral**).

>[!NOTE]
>
>Consulte também [Fragmentos de conteúdo configurando componentes para renderização](/help/sites-developing/content-fragments-config-components-rendering.md) para obter mais informações.

Os fragmentos de conteúdo do Adobe Experience Manager (AEM) são [criados e gerenciados como ativos independentes da página](/help/assets/content-fragments/content-fragments.md). Eles permitem criar conteúdo não vinculado a canais, juntamente com variações (podem ser específicas de cada canal). [É possível usar esses fragmentos e suas variações ao criar suas páginas de conteúdo](/help/sites-authoring/content-fragments.md). Você também pode usar um ativo de fragmento de conteúdo existente [arrastando-o do navegador de ativos para a página](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) (assim como para outros componentes baseados em ativos, como o componente de base Imagem). O componente de fragmento de conteúdo pronto para uso exibe apenas um [elemento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) do fragmento de conteúdo referenciado. Usando a caixa de diálogo de componentes, você pode definir o [elemento, a variação e o intervalo de parágrafos de fragmento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) que deseja exibir na página.

>[!NOTE]
>
>Esse componente Fragmento de conteúdo foi introduzido no AEM 6.2 como uma versão aprimorada do componente Artigo, que foi descontinuada.

>[!NOTE]
>
>Fragmentos de conteúdo não são compatíveis com a interface clássica.

### Definição {#definition}

O componente **Fragmento de Conteúdo** é usado para conter uma referência a um ativo de fragmento de conteúdo (ativos de texto efetivamente aprimorados). O tipo de recurso do fragmento de conteúdo é:

`dam/cfm/components/contentfragment/contentfragment`

A referência é definida na propriedade:

`fileReference`

Somente o editor da interface habilitada para toque oferece suporte total aos componentes do fragmento de conteúdo, que incluem a biblioteca do cliente:

`cq.authoring.editor.plugin.cfm`

Essa biblioteca adiciona recursos, específicos dos fragmentos de conteúdo, ao editor. Por exemplo, o suporte para a capacidade de adicionar e configurar fragmentos de conteúdo na página, a capacidade de pesquisar ativos de fragmento de conteúdo no navegador de ativos e conteúdo associado no painel lateral está disponível.

### Conteúdo intermediário {#in-between-content}

O componente **Fragmento do Conteúdo** t permite que você solte componentes adicionais entre os diferentes parágrafos do [elemento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) exibido. Basicamente, o elemento exibido é composto de parágrafos diferentes (cada parágrafo é marcado por um retorno de carro). Entre cada um desses parágrafos, é possível inserir conteúdo usando outros componentes.

De um ponto de vista técnico, cada parágrafo do elemento exibido reside em seu próprio parsys, e cada componente adicionado entre os parágrafos é inserido (abaixo do capô) no parsys.

Em outras palavras, se a instância do componente Fragmento de conteúdo for composta de três parágrafos, o componente terá três parsys diferentes no repositório. Todo o conteúdo intermediário adicionado ao fragmento de conteúdo está realmente localizado dentro desses parsys.

No repositório, o conteúdo intermediário é armazenado em relação à sua posição dentro da estrutura geral do parágrafo, ou seja, não é anexado ao conteúdo real do parágrafo.

Para ilustrar isso, considere que você tem o seguinte:

* Uma instância de um fragmento de conteúdo composto por três parágrafos
* E que parte do conteúdo já foi inserido após o segundo parágrafo

   * Isso significa que o conteúdo é armazenado no segundo parsys.

Basicamente, se a estrutura de parágrafo dessa ocorrência for alterada (alterando a variação, o elemento ou o intervalo de parágrafos exibidos), isso poderá afetar o conteúdo intermediário exibido quando o conteúdo do fragmento de conteúdo:

* É editado e outro parágrafo é adicionado antes do segundo parágrafo:

   * O conteúdo intermediário é exibido após o parágrafo recém-criado (o segundo parsys agora contém o parágrafo recém-criado).

* É editado e o segundo parágrafo é removido:

   * O conteúdo intermediário é exibido após o parágrafo que era o terceiro (o segundo parsys agora contém o terceiro parágrafo anterior).

* Está configurado para que somente o primeiro parágrafo seja exibido:

   * O conteúdo intermediário não é exibido (o segundo parsys não é mais renderizado devido à nova configuração).

### Personalização do componente Fragmento de Conteúdo {#customizing-the-content-fragment-component}

Para usar o componente Fragmento de conteúdo pronto para uso como um blueprint para a extensão, você deve respeitar o seguinte contrato:

* Reutilize o script de renderização HTL e seu POJO associado para que você possa ver como o recurso de conteúdo intermediário é implementado.
* Reutilizar o nó do fragmento de conteúdo: `cq:editConfig`

   * Os ouvintes `afterinsert`/ `afteredit`/ `afterdelete` são usados para acionar eventos JS. Esses eventos são manipulados na biblioteca do cliente `cq.authoring.editor.plugin.cfm` para exibir o conteúdo associado no painel lateral.
   * Os `cq:dropTargets` estão configurados para serem compatíveis com a ação de arrastar ativos do fragmento de conteúdo.
   * O `cq:inplaceEditing` está configurado para oferecer suporte à criação de um fragmento de conteúdo no editor de páginas. O editor local de fragmentos está definido na biblioteca cliente `cq.authoring.editor.plugin.cfm` e permite que um link rápido abra o [elemento/variação](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) atual no [editor de fragmentos](/help/assets/content-fragments/content-fragments-variations.md).

### Regravação de ativos antes da renderização {#asset-rewriting-before-rendering}

O gerenciamento de fragmento de conteúdo usa um processo de renderização interno para gerar a saída de HTML final para uma página. Isso é usado internamente pelo componente Fragmento de conteúdo, mas também pelo processo em segundo plano que atualiza os fragmentos referenciados nas páginas de referência.

Internamente, o Sling Rewriter é usado para essa renderização. A respectiva configuração é encontrada em `/libs/dam/config/rewriter/cfm` e pode ser ajustada, se necessário. Consulte o [Apache Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) para obter mais informações.

>[!CAUTION]
>
>Se você ajustar/sobrepor a configuração do reescritor:
>
>* `/libs/dam/config/rewriter/cfm`
>
>Em seguida, o `serializerType` **deve** ser atualizado para:
>
>* `serializerType="html5-serializer"`

A configuração pronta para uso usa os seguintes transformadores:

* `transformer-cfm-payloadfilter` - para recuperar somente a parte `body` ( `<body>...</body>`) do HTML do fragmento

* `transformer-cfm-parfilter` - filtra parágrafos indesejados se um intervalo de parágrafos for especificado (como pode ser feito com o componente Fragmento de Conteúdo)
* `transformer-cfm-assetprocessor` - é usado internamente para recuperar uma lista dos ativos incorporados ao fragmento

O processo de renderização é exposto por meio de [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) e pode ser usado (por exemplo) por componentes personalizados, se necessário.
