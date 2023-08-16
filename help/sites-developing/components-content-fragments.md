---
title: Componentes para fragmentos de conteúdo
seo-title: Components for Content Fragments
description: Fragmentos de conteúdo do AEM são criados e gerenciados como ativos independentes da página
seo-description: AEM content fragments are created and managed as page-independent assets
uuid: 81a9e0fe-ed45-4880-b36c-4f49e2598389
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: b7777dc5-a867-4799-9e2c-a1f4bb5dd96a
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 3%

---

# Componentes para fragmentos de conteúdo{#components-for-content-fragments}

## Componentes para criação de fragmentos {#components-for-fragment-authoring}

>[!CAUTION]
>
>Não é recomendável estender ou alterar os componentes reais usados no Editor de fragmentos, pois eles ainda estão sujeitos a alterações.

Consulte a [API de gerenciamento de fragmento de conteúdo — lado do cliente](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## Componentes para criação de página {#components-for-page-authoring}

>[!CAUTION]
>
>A variável [Componente principal do fragmento de conteúdo](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) O agora é recomendado. Consulte [Desenvolvimento dos Componentes principais](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) para obter mais detalhes.
>
>Esta seção detalha o componente original entregue para uso com fragmentos de conteúdo (**Fragmento do conteúdo** no **Geral** grupo).

>[!NOTE]
>
>Consulte também [Fragmentos de conteúdo configuram componentes para renderização](/help/sites-developing/content-fragments-config-components-rendering.md) para obter mais informações.

Os fragmentos de conteúdo do Adobe Experience Manager (AEM) são [criados e gerenciados como ativos independentes da página](/help/assets/content-fragments/content-fragments.md). Eles permitem criar conteúdo não vinculado a canais, juntamente com variações (podem ser específicas de cada canal). [Em seguida, é possível usar estes fragmentos e suas variações ao criar suas páginas de conteúdo](/help/sites-authoring/content-fragments.md). Também é possível usar um ativo de fragmento de conteúdo existente ao [arrastar do navegador de ativos para a página](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) (assim como para outros componentes baseados em ativos, como o componente de base Imagem). O componente Fragmento de conteúdo pronto para uso exibe apenas um [element](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) do fragmento de conteúdo referenciado. Usando a caixa de diálogo de componentes, é possível definir o [elemento, variação e intervalo de parágrafos do fragmento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) que deseja exibir na página.

>[!NOTE]
>
>Esse componente Fragmento de conteúdo foi introduzido no AEM 6.2 como uma versão aprimorada do componente Artigo, que foi descontinuada.

>[!NOTE]
>
>Fragmentos de conteúdo não são compatíveis com a interface clássica.

### Definição {#definition}

A variável **Fragmento do conteúdo** O componente é usado para manter uma referência a um ativo de fragmento de conteúdo (ativos de texto aprimorados efetivamente). O tipo de recurso do fragmento de conteúdo é:

`dam/cfm/components/contentfragment/contentfragment`

A referência é definida na propriedade:

`fileReference`

Somente o editor da interface habilitada para toque oferece suporte total aos componentes do fragmento de conteúdo, que inclui a biblioteca do cliente:

`cq.authoring.editor.plugin.cfm`

Essa biblioteca adiciona recursos, específicos dos fragmentos de conteúdo, ao editor. Por exemplo, o suporte para a capacidade de adicionar e configurar fragmentos de conteúdo na página, a capacidade de pesquisar ativos de fragmento de conteúdo no navegador de ativos e para conteúdo associado no painel lateral estão disponíveis.

### Conteúdo intermediário {#in-between-content}

A variável **Fragmento do conteúdo** O componente t permite soltar componentes adicionais entre os diferentes parágrafos do exibido [element](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment). Basicamente, o elemento exibido é composto de parágrafos diferentes (cada parágrafo é marcado por um retorno de carro). Entre cada um desses parágrafos, é possível inserir conteúdo usando outros componentes.

De um ponto de vista técnico, cada parágrafo do elemento exibido * * * vive em seu próprio parsys, e cada componente adicionado entre os parágrafos será (abaixo do capô) inserido no parsys.

Em outras palavras, se a instância do componente Fragmento de conteúdo for composta de três parágrafos, o componente terá três parsys diferentes no repositório. Todo o conteúdo intermediário adicionado ao fragmento de conteúdo estará realmente localizado dentro desses parsys.

No repositório, o conteúdo intermediário é armazenado em relação à sua posição dentro da estrutura geral do parágrafo, ou seja, não é anexado ao conteúdo real do parágrafo.

Para ilustrar isso, considere que temos:

* Uma instância de um fragmento de conteúdo composto por três parágrafos
* E que parte do conteúdo já foi inserido após o segundo parágrafo

   * Isso significa que o conteúdo será armazenado no segundo parsys.

Basicamente, se a estrutura de parágrafo dessa ocorrência for alterada (alterando a variação, o elemento ou o intervalo de parágrafos exibidos), isso poderá afetar o conteúdo intermediário exibido quando o conteúdo do fragmento de conteúdo:

* É editado e outro parágrafo é adicionado antes do segundo parágrafo:

   * O conteúdo intermediário será exibido após o parágrafo recém-criado (o segundo parsys agora contém o parágrafo recém-criado).

* É editado e o segundo parágrafo é removido:

   * O conteúdo intermediário será exibido após o parágrafo que era o terceiro (o segundo parsys agora contém o terceiro parágrafo anterior).

* Está configurado para que somente o primeiro parágrafo seja exibido:

   * O conteúdo intermediário não será exibido (o segundo parsys não é mais renderizado devido à nova configuração).

### Personalização do componente Fragmento de Conteúdo {#customizing-the-content-fragment-component}

Para usar o componente Fragmento de conteúdo pronto para uso como um blueprint para a extensão, você deve respeitar o seguinte contrato:

* Reutilize o script de renderização HTL e o POJO associado para ver como o recurso de conteúdo intermediário é implementado.
* Reutilizar o nó do fragmento de conteúdo: `cq:editConfig`

   * A variável `afterinsert`/ `afteredit`/ `afterdelete` Os ouvintes são usados para acionar eventos JS. Esses eventos serão tratados no `cq.authoring.editor.plugin.cfm` para exibir o conteúdo associado no painel lateral.
   * A variável `cq:dropTargets` estão configurados para serem compatíveis com a ação de arrastar ativos do fragmento de conteúdo.
   * `cq:inplaceEditing` O está configurado para oferecer suporte à criação de um fragmento de conteúdo no editor de páginas. O editor do fragmento no local é definido na variável `cq.authoring.editor.plugin.cfm` biblioteca cliente e permite que um link rápido abra a biblioteca [elemento/variação](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) no [editor de fragmento](/help/assets/content-fragments/content-fragments-variations.md).

### Regravação de ativos antes da renderização {#asset-rewriting-before-rendering}

O gerenciamento de fragmento de conteúdo usa um processo de renderização interno para gerar a saída de HTML final para uma página. Isso é usado internamente pelo componente Fragmento de conteúdo, mas também pelo processo em segundo plano que atualiza os fragmentos referenciados nas páginas de referência.

Internamente, o Sling Rewriter é usado para essa renderização. A respectiva configuração é encontrada em `/libs/dam/config/rewriter/cfm` e podem ser ajustadas, se necessário. Consulte a [Reescrita do Apache Sling](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) para obter mais informações.

>[!CAUTION]
>
>Se você ajustar/sobrepor a configuração do reescritor:
>
>* `/libs/dam/config/rewriter/cfm`
>
>em seguida, o `serializerType` **deve** ser atualizado para:
>
>* `serializerType="html5-serializer"`

A configuração pronta para uso usa os seguintes transformadores:

* `transformer-cfm-payloadfilter` - para recuperar o `body` parte ( `<body>...</body>`) somente do HTML do fragmento

* `transformer-cfm-parfilter` - filtra parágrafos indesejados se um intervalo de parágrafo for especificado (como pode ser feito com o componente Fragmento de conteúdo)
* `transformer-cfm-assetprocessor` - é usado internamente para recuperar uma lista dos ativos incorporados ao fragmento

O processo de renderização é exposto por meio de [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) e podem ser aproveitadas (por exemplo) por componentes personalizados, se necessário.
