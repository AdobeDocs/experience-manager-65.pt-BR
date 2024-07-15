---
title: Criação e adição de modelos e componentes
description: Siga esta página para saber mais sobre como criar e adicionar modelos e componentes ao seu aplicativo. A página usa o aplicativo Geometrixx Unlimited como o aplicativo que contém um modelo de aplicativo de amostra e modelos de página.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 5f050baa-fe10-4acc-ad32-de20793edc13
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 0%

---

# Criação e adição de modelos e componentes {#creating-and-adding-templates-and-components}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

O AEM Mobile On-Demand fornece um modelo de aplicativo totalmente configurado, um modelo de artigo e componentes de artigo.

O aplicativo We.Unlimited é um modelo de amostra que representa o shell de um aplicativo AEM Mobile On-Demand totalmente configurável e gerenciável.

Selecionar esse modelo de amostra ao criar um aplicativo fornece um painel avançado de recursos do AEM Mobile.

![chlimage_1-70](assets/chlimage_1-70.png)

>[!NOTE]
>
>Para gerenciar o conteúdo do aplicativo móvel e do aplicativo no Centro de Controle de Aplicativos AEM Mobile, consulte o [Painel de Aplicativos AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

## Criação de modelos de aplicativo {#creating-app-templates}

Um modelo de aplicativo é usado para criar um aplicativo e atua como uma coleção de modelos de página e componentes que representam uma linha de base ou base de um aplicativo. O modelo elimina algumas propriedades fundamentais para liderar o aplicativo da maneira apropriada. Em geral, um cliente não criaria muitos aplicativos no total.

Os modelos de aplicativo oferecem uma maneira fácil de usar os designs existentes criados pelos desenvolvedores, usados para a criação de novos aplicativos no AEM.

Ao criar um aplicativo com base no modelo de outro aplicativo, você obterá um aplicativo que tem um ponto de partida representativo do aplicativo no qual ele foi criado.

Etapas para criar um aplicativo com base em um modelo de aplicativo:

1. Navegue até o catálogo de aplicativos do AEM Mobile: *&lt;server-url>/aem/apps.html/content/mobileapps*
1. Selecione **Criar** > **Aplicativo** como mostrado abaixo

Depois de criar um aplicativo usando esse modelo, você pode adicionar artigos, banners e coleções ao aplicativo. Para visitar novamente, criar artigos, banners e coleções, consulte [Ações de gerenciamento de conteúdo](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

>[!NOTE]
>
>Como alternativa, você também pode selecionar um modelo de aplicativo de exemplo, por exemplo, o aplicativo **We.Unlimited**, disponibilizado a você por um desenvolvedor de AEM. Se você usar esse modelo de amostra para o seu aplicativo, obterá alguns artigos e coleções de exemplo para trabalhar. Você terá a opção de usar modelos e componentes de amostra, personalizar os existentes ou criar novos para seu aplicativo.

>[!CAUTION]
>
>Definindo propriedade ***redirectTarget***
>
>Ao usar um dos modelos do aplicativo, o desenvolvedor define o conteúdo do aplicativo. No entanto, o desenvolvedor deve estar ciente de onde o aplicativo é criado no jcr e do valor da propriedade ***redirectTarget***.
>
>O ***redirectTarget*** é calculado como parte da operação de criação de aplicativo e tenta resolver um caminho, se houver uma propriedade redirectTarget disponível como parte do modelo de aplicativo e o valor do redirectTarget for definido como relativo. Quando o processo de criação do aplicativo encontra um valor relativo para o redirectTarget no modelo do aplicativo, o valor é anexado ao local resolvido de onde o aplicativo foi criado.
>
>Por exemplo, se um modelo de aplicativo definir um ***redirectTarget*** com um valor de &quot;*language-masters/en*&quot; e o aplicativo tiver sido criado em &quot;*/content/mobileapps/fooApp*&quot;, o valor final para redirectTarget após a criação do aplicativo será &quot;*/content/mobileapps/fooApp/language-masters/en*&quot;.
>

## Criação de modelos de conteúdo {#creating-content-templates}

Cada tipo de entidade tem dois templates prontos para uso. São eles:

* **Modelos padrão:** usados para a criação de conteúdo com propriedades/estrutura padrão aplicáveis
* **Modelos importados:** usado para importar conteúdo do AEM Mobile com propriedades/estrutura padrão aplicáveis

### Modelos de artigo {#article-templates}

O Unlimited Article é um modelo de amostra representando um layout de artigo típico do AEM Mobile On-Demand.

1. Em **Gerenciar Artigos**, selecione **+** para criar um artigo. Você pode escolher um **Artigo Ilimitado** ou um **Artigo de Rich Text**. A imagem abaixo mostra a opção que permite escolher qualquer um desses dois modelos de artigo.

1. Clique em **Avançar** para definir os metadados do artigo, como Nome/Título do artigo, Descrição, Autor, Resumo, Departamento, Imagem em miniatura, Acesso ao artigo etc.
1. Clique em **Avançar** para preencher as Propriedades do Anúncio.
1. Clique em **Avançar** para inserir a imagem do artigo ou a imagem da rede social
1. Clique em **Avançar** para escolher uma coleção para a qual vincular este novo Artigo.
1. Clique em **Avançar** para inserir os detalhes de compartilhamento em redes sociais.
1. Clique em **Criar** para concluir o processo de criação de um artigo usando a amostra. Você pode clicar em **Concluído** ou **Editar artigo** para editar as propriedades deste artigo.

![chlimage_1-71](assets/chlimage_1-71.png)

### Adição de componentes ao artigo {#adding-components-to-article}

Depois de criado, um autor pode editar o conteúdo de um artigo adicionando componentes como texto e imagens. Os artigos são uma extensão dos modelos de página do AEM.

Selecione um artigo que deseja editar e clique em **Editar** para adicionar componentes ao artigo.

![chlimage_1-72](assets/chlimage_1-72.png) ![chlimage_1-73](assets/chlimage_1-73.png)

Escolha o &#39;**+**&#39; no painel esquerdo para adicionar componentes ao seu artigo.

![chlimage_1-74](assets/chlimage_1-74.png)

### Criação de modelos prontos para uso {#creating-out-of-the-box-templates}

Não há Modelos de artigo prontos para uso. No entanto, há um modelo padrão que os modelos personalizados devem estender. Consulte a [amostra de modelo de artigo](http://localhost:4502/crx/de/index.jsp#/apps/geometrixx-unlimited-app/templates/article) do Geometrixx Unlimited App.

As propriedades principais além das propriedades obrigatórias do modelo AEM normal incluem;

***dps-resourceType=&quot;dps:Article&quot;***

Essa propriedade garante que a página do AEM seja reconhecida como uma página de artigo direcionada da AEM Mobile.

De acordo com os modelos AEM, você pode adicionar propriedades padrão ou nós filhos ao ***jcr:content*** do modelo.

### Modelos de banner e coleção {#banner-and-collection-templates}

>[!CAUTION]
>
>Os banners e coleções não têm conteúdo, portanto, sua criação não é compatível com modelos personalizados.

## Criação e adição de componentes {#creating-and-adding-components}

Os componentes usam e permitem acesso a Widgets e são usados para renderizar o Conteúdo.

Um componente simples é incluído no repositório de código, cuja origem pode ser encontrada no AEM. Posteriormente, também pode ser aberto localmente no CRXDE Lite.

>[!NOTE]
>
>No momento, não há componentes prontos para uso fornecidos para o AEM Mobile.
>

Você pode adicionar componentes à sua página. Qualquer componente pode ser usado em um aplicativo AEM Mobile, mas quando aplicado, pode não ser renderizado corretamente.

No entanto, os componentes personalizados podem não ser exportados e carregados corretamente no AEM Mobile On-demand Services sem um manipulador de sincronização de conteúdo de exportação personalizado que seja renderizado no AEM.

Depois que o componente já tiver sido incluído em uma página AEM, juntamente com alguns outros componentes do bloco de construção, você poderá adicionar outro componente à página ou editar um existente.

**Para adicionar outro componente à página:**

1. Escolha essa página e verifique se você está no modo de Edição, por meio da lista suspensa na parte superior direita do cabeçalho do Editor
1. Alterne o painel lateral usando o ícone mais à esquerda no cabeçalho do editor
1. Selecione a guia **Componentes**
1. Arraste e solte um dos componentes disponíveis na página

![chlimage_1-75](assets/chlimage_1-75.png)

**Para editar um componente existente:**

1. Escolha essa página, verifique se você está no modo **Editar** e selecione o componente
1. Selecione a chave inglesa para configurar o componente

>[!NOTE]
>
>Você pode criar um componente no AEM e personalizar o mesmo usando [Desenvolvimento com CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Depois de personalizar o componente existente como seus requisitos, você pode adicioná-lo em sua página usando a opção **Editar** em **Gerenciar artigos**, conforme mostrado na figura acima.

>[!NOTE]
>
>Consulte [Práticas recomendadas para o desenvolvimento de modelos e componentes](/help/mobile/best-practices-aem-mobile.md) no AEM Mobile.

### Próximas etapas {#the-next-steps}

* [Uso das propriedades de conteúdo para exportar conteúdo](/help/mobile/on-demand-content-properties-exporting.md)
* [Dispositivo móvel com sincronização de conteúdo](/help/mobile/mobile-ondemand-contentsync.md)
