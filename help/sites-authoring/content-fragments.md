---
title: Criação da página de conteúdo com fragmentos de conteúdo
description: AEM Fragmentos do conteúdo permite projetar, criar, preparar e usar conteúdo independente da página.
uuid: 987de428-8354-4b23-a552-3ea415122184
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 4049a7a5-4b33-4462-a25f-3c0daeb6a8a9
docset: aem65
exl-id: d5dad844-80ca-4ace-a082-38d892d9ffe2
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 60%

---

# Criação de página com fragmentos de conteúdo{#page-authoring-with-content-fragments}

Os fragmentos de conteúdo do Adobe Experience Manager (AEM) são [criados e gerenciados como ativos independentes da página](/help/assets/content-fragments/content-fragments.md).

Eles permitem criar conteúdo não vinculado a canais, juntamente com variações (podem ser específicas de cada canal). Em seguida, é possível usar estes fragmentos e suas variações ao criar suas páginas de conteúdo.

Juntamente com o exportador JSON atualizado, os fragmentos de conteúdo estruturados também podem ser usados para fornecer o conteúdo do AEM através do Content Services a canais diferentes das páginas do AEM.

>[!NOTE]
>
>**Fragmentos de conteúdo** e **[Fragmentos de experiência](/help/sites-authoring/experience-fragments.md)** são recursos diferentes no AEM:
>
>* **Fragmentos de conteúdo** são conteúdo editorial, principalmente texto e imagens relacionadas. São conteúdo puro, sem design e layout.
>* **Fragmentos de experiência** são conteúdo totalmente apresentado; um fragmento de uma página da Web.
>
>Fragmentos de experiência podem incluir conteúdo na forma de Fragmentos de conteúdo, mas não o contrário.

>[!CAUTION]
>
>Esta página deve ser lida junto com a seção [Trabalhar com fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) (e páginas relacionadas), pois apresenta a terminologia e os conceitos básicos, além dos processos de criação e de gerenciamento de fragmentos.

Os fragmentos de conteúdo permitem:

* **Estratégia de marketing e campanha**

   * Revise o conteúdo por meio de fragmentos de conteúdo gerenciados centralmente.

* **Creative Pro**

   * Rastreamento de ativos criativos por meio de coleções associadas aos fragmentos de conteúdo.

* **Escritores de Cópia**

   * Escreva no editor de fragmento de conteúdo do AEM.
   * Pode criar variações de conteúdo.
   * Pode associar o conteúdo relevante ao fragmento de conteúdo.
   * Pode usar controle de versão/fluxo de trabalho.
   * É possível compartilhar o fragmento de conteúdo.
   * Pode gerenciar traduções centralmente.

* **Produtores e Gerentes de Jornadas**

   * Selecione de fragmentos e variações predefinidos com a criação no AEM.
   * Pode confiar que o fragmento e o conteúdo associado estejam sempre atualizados, já que os redatores e criadores fazem suas atualizações em fragmentos e ativos gerenciados centralmente.
   * Pode confiar no conteúdo de mídia associado que está sendo preparado para relevância.
   * Pode criar variações de conteúdo ad hoc dinamicamente, garantindo que essas variações permaneçam gerenciadas centralmente no fragmento.

## Adicionar um fragmento de conteúdo à sua página     {#adding-a-content-fragment-to-your-page}

1. Abra a página para edição. 

1. Adicione o componente **Fragmento de conteúdo**; do navegador **Componentes** ou **Inserir novo componente**. 

1. Você pode:

   * Abra o navegador de **ativos** e filtre por **Fragmentos de conteúdo** (o filtro padrão é por Imagens). Em seguida, arraste o fragmento necessário para a instância do componente.

   * Selecione o componente do fragmento de conteúdo e **Configurar** na barra de ferramentas. Na caixa de diálogo, é possível abrir a caixa de diálogo de seleção para procurar e selecionar o **Fragmento de conteúdo** necessário.
   >[!NOTE]
   >
   >Um método alternativo é arrastar um fragmento de conteúdo específico diretamente para a página. Essa ação cria o componente associado (Fragmento de conteúdo) de maneira automática.

1. Inicialmente, o conteúdo do elemento **Principal** e do **Mestre** (variação) serão mostrados. Você pode [selecionar outros elementos e/ou variações](#selecting-the-element-or-variation) conforme necessário.

   ![cfm-6420-01](assets/cfm-6420-01.png)

   >[!NOTE]
   >
   >Para obter mais informações sobre outras funcionalidades de edição, consulte também:
   >
   >
   >
   >    * [Layout responsivo](/help/sites-authoring/responsive-layout.md)
   >    * [Editar conteúdo da página](/help/sites-authoring/editing-content.md)


### Selecionar o elemento ou a variação {#selecting-the-element-or-variation}

Abra a caixa de diálogo **Configuração** do fragmento para configurar o fragmento para o uso na página atual. A caixa de diálogo pode depender do componente usado.

Na caixa de diálogo de configuração apropriada, é possível selecionar os parâmetros disponíveis, incluindo:

* **Fragmento de conteúdo**

   Especifique o fragmento a ser usado.

* **Modo de exibição**:

   * **Elemento de texto simples**

   * **Vários elementos**

* **Elemento**

   * O padrão **Principal** estará sempre disponível.
   * Uma seleção estará disponível se o fragmento tiver sido criado com um modelo apropriado.

   >[!NOTE]
   >
   >Os elementos disponíveis dependem do template usado.

* **Variação**

   * O padrão **Mestre** sempre estará disponível.
   * Uma seleção estará disponível se as variações forem criadas para o fragmento.

* **Parágrafos**: especifique o intervalo dos parágrafos a serem incluídos:

   * **Todos**
   * **Intervalo**: por exemplo, `1`, `3-5`, `9-*`

      * **Tratar cabeçalhos como seus próprios parágrafos**

* **Tratar cabeçalhos como seus próprios parágrafos**

### Conexão rápida no editor de fragmentos    {#quick-connection-to-fragment-editor}

É possível abrir a origem do fragmento para edição (o ativo) usando o ícone **Editar** na barra de ferramentas do componente. Assim, você pode [editar e gerenciar o fragmento de conteúdo](/help/assets/content-fragments/content-fragments.md).

>[!CAUTION]
>
>Como sempre, editar a origem do fragmento afetará todas as páginas que fazem referência a esse fragmento de conteúdo.

### Adicionar conteúdo intermediário     {#adding-in-between-content}

Quando um fragmento de conteúdo específico for adicionado à página, há um espaço reservado para **Arrastar os componentes aqui** entre cada parágrafo HTML (e na parte superior/inferior) do fragmento.

Isso permite adicionar conteúdo extra [intermediário (ou seja, conteúdo intermediário)](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) o conteúdo do fragmento (em qualquer um dos pontos disponíveis), sem precisar alterar o fragmento raiz.

Para conteúdo intermediário, você pode:

* Adicionar componentes da [Navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser).
* Adicionar ativos no [Navegador de ativos](/help/sites-authoring/author-environment-tools.md#assets-browser).
* Usar [Conteúdo associado](#using-associated-content) como uma origem de conteúdo intermediário.

>[!CAUTION]
>
>O conteúdo intermediário é o conteúdo da página. Ele não é armazenado no fragmento de conteúdo.

![cfm-6420-02](assets/cfm-6420-02.png)

>[!NOTE]
>
>Você também pode [inserir ativos visuais (imagens) ao próprio fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Os ativos visuais inseridos no fragmento propriamente dito são anexados ao parágrafo anterior no fragmento. Isso significa que não é possível posicionar conteúdo intermediário entre um ativo visual e o parágrafo anterior.

>[!CAUTION]
>
>Depois de adicionar o conteúdo intermediário a um fragmento de conteúdo na página, a alteração da estrutura do fragmento de conteúdo subjacente (ou seja, no editor de fragmentos de conteúdo) pode causar resultados errôneos/inesperados.
>
>Quando isso ocorre, o conteúdo intermediário é mantido como está:
>
>* Os componentes intermediários têm uma posição absoluta na sequência de componentes no fluxo do fragmento. Essa posição não muda, mesmo quando o conteúdo dos parágrafos no fragmento muda.
>
>  Isso causa a impressão de que o posicionamento relativo mudou, pois os parágrafos intermediários não têm relacionamento contextual com os parágrafos (fragmento) ao lado dos quais estão posicionados.
>* A menos que as duas estruturas de parágrafo entrem em conflito; nesse caso, o conteúdo intermediário não é exibido (embora ainda esteja presente internamente).
>


### Usar conteúdo associado     {#using-associated-content}

Se você tiver [conteúdo associado](/help/assets/content-fragments/content-fragments-assoc-content.md) ao [fragmento de conteúdo](/help/assets/content-fragments/content-fragments.md), esses ativos estarão disponíveis no painel lateral (depois de colocar o fragmento na página de conteúdo). O conteúdo associado é uma fonte especial de conteúdo do [conteúdo intermediário](#adding-in-between-content).

>[!NOTE]
>
>Existem vários métodos de adicionar [ativos visuais (por exemplo, imagens)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) ao fragmento e/ou página.

>[!NOTE]
>
>Se você tiver vários fragmentos de conteúdo em uma página, a variável **Conteúdo associado** mostrará os ativos adequados para todos os fragmentos.

Depois de adicionar um fragmento com conteúdo associado à página, uma nova guia (**Conteúdo associado**) é aberta no painel lateral.

Aqui, é possível arrastar os ativos para o local desejado (para um componente existente ou para a posição desejada onde o componente adequado será criado): 

![cfm-6420-03](assets/cfm-6420-03.png)

### Ativos inseridos no fragmento {#assets-inserted-into-the-fragment}

Se os ativos (por exemplo, imagens) tiverem sido inseridos no próprio fragmento, as opções para editar esses ativos no editor de páginas serão limitadas. <!-- Removed link as it was a 404 on helpx -->

Por exemplo, para uma imagem, é possível

* Recorte, gire ou vire a imagem.
* Adicione um título ou texto alternativo.
* Especifique um tamanho.
* Você também pode configurar o layout.

Outras alterações, como mover, copiar ou excluir, devem ser feitas no editor de fragmentos.

### Publicação {#publishing}

Os fragmentos precisam ser publicados para que possam ser usados em suas páginas da Web publicadas:

* Um fragmento pode ser publicado depois de [criar o fragmento no console de Ativos](/help/assets/content-fragments/content-fragments.md#publishingandreferencingafragment).
* Se um *fragmento não publicado* for usado em uma página que está sendo publicada, ele também poderá ser publicado neste momento.
