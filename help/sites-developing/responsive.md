---
title: Design responsivo para páginas da Web
description: Com um design responsivo, as mesmas páginas podem ser exibidas efetivamente em vários dispositivos em várias orientações.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
legacypath: /content/docs/en/aem/6-0/develop/mobile/responsive
exl-id: c705710b-a94a-4f4f-affa-ddd4fc6cb0ec
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '5272'
ht-degree: 0%

---

# Design responsivo para páginas da Web{#responsive-design-for-web-pages}

{{ue-over-mobile}}

>[!NOTE]
>
>Vários exemplos são baseados no conteúdo de amostra do Geometrixx, que não é mais enviado com AEM (Adobe Experience Manager), tendo sido substituído pelo We.Retail. Consulte o documento [Implementação de referência do We.Retail](/help/sites-developing/we-retail.md#we-retail-geometrixx) para saber como baixar e instalar o Geometrixx.

Projete suas páginas da Web para que elas se adaptem à janela de visualização do cliente em que são exibidas. Com um design responsivo, as mesmas páginas podem ser exibidas efetivamente em vários dispositivos em ambas as orientações. A imagem a seguir demonstra algumas maneiras pelas quais uma página pode responder às alterações no tamanho da janela de visualização:

* Layout: use layouts de coluna única para visores menores e layouts de várias colunas para visores maiores.
* Tamanho do texto: use um tamanho de texto maior (quando apropriado, como cabeçalhos) em visores maiores.
* Conteúdo: inclua apenas o conteúdo mais importante ao exibir em dispositivos menores.
* Navegação: ferramentas específicas de dispositivos são fornecidas para acessar outras páginas.
* Imagens: exibe representações de imagens apropriadas para a janela de visualização do cliente. de acordo com as dimensões da janela.

![chlimage_1-4](assets/chlimage_1-4a.png)

Desenvolva aplicativos Adobe Experience Manager (AEM) que geram páginas HTML5 que se adaptam a vários tamanhos e orientações de janela. Por exemplo, os seguintes intervalos de larguras de visor correspondem a vários tipos e orientações de dispositivo

* Largura máxima de 480 pixels (telefone, retrato)
* Largura máxima de 767 pixels (telefone, paisagem)
* Largura entre 768 pixels e 979 pixels (tablet, retrato)
* Largura entre 980 pixels e 1199 pixels (tablet, paisagem)
* Largura de 1200 pixels ou superior (desktop)

Consulte os seguintes tópicos para obter informações sobre como implementar um comportamento de design responsivo:

* [Consultas de mídia](/help/sites-developing/responsive.md#using-media-queries)
* [Grades fluídas](/help/sites-developing/responsive.md#developing-a-fluid-grid)
* [Imagens adaptáveis](/help/sites-developing/responsive.md#using-adaptive-images)

Conforme você cria, use o **[!UICONTROL Sidekick]** para visualizar suas páginas para vários tamanhos de tela.

## Antes de desenvolver {#before-you-develop}

Antes de desenvolver o aplicativo AEM compatível com suas páginas da Web, várias decisões de design devem ser tomadas. Por exemplo, você deve ter as seguintes informações:

* Os dispositivos que você está direcionando.
* Os tamanhos das janelas de visualização de destino.
* Os layouts de página para cada tamanho de visor direcionado.

### Estrutura do aplicativo {#application-structure}

A estrutura típica do aplicativo AEM é compatível com todas as implementações de design responsivas:

* Os componentes da página residem abaixo de /apps/*application_name*/components
* Os modelos residem abaixo de /apps/*application_name*/templates
* Os designs ficam abaixo de /etc/designs

## Uso de consultas de mídia {#using-media-queries}

As consultas de mídia permitem o uso seletivo de estilos CSS para renderização da página. As ferramentas e os recursos de desenvolvimento do AEM permitem que você implemente de forma eficaz e eficiente as consultas de mídia em seus aplicativos.

O grupo W3C fornece a recomendação [Consultas de Mídia](https://www.w3.org/TR/mediaqueries-3/) que descreve esse recurso CSS3 e a sintaxe.

### Criação do arquivo CSS {#creating-the-css-file}

No arquivo CSS, defina consultas de mídia com base nas propriedades dos dispositivos que você está direcionando. A seguinte estratégia de implementação é eficaz para gerenciar estilos para cada consulta de mídia:

* Use um ClientLibraryFolder para definir o CSS que é montado quando a página é renderizada.
* Defina cada consulta de mídia e os estilos associados em arquivos CSS separados. É útil usar nomes de arquivo que representem os recursos do dispositivo da query de mídia.
* Defina estilos comuns a todos os dispositivos em um arquivo CSS separado.
* No arquivo css.txt de ClientLibraryFolder, ordene os arquivos CSS da lista conforme necessário no arquivo CSS montado.

A amostra de mídia `We.Retail` usa essa estratégia para definir estilos no design do site. O arquivo CSS usado por `We.Retail` está em `*/apps/weretail/clientlibs/clientlib-site/less/grid.less`.

A tabela a seguir lista os arquivos na pasta secundária css.

<table>
 <tbody>
  <tr>
   <th>Nome do arquivo</th>
   <th>Descrição</th>
   <th>Consulta de mídia</th>
  </tr>
  <tr>
   <td>style.css</td>
   <td>Estilos comuns.</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td>bootstrap.css</td>
   <td>Estilos comuns, definidos pelo Twitter Bootstrap.</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td>responsive-1200px.css</td>
   <td>Estilos para todas as mídias com 1200 pixels de largura ou largura.</td>
   <td><p>@media (min-width: 1200 px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-980px-1199px.css</td>
   <td>Estilos de mídia entre 980 e 1199 pixels de largura.</td>
   <td><p>@media (largura mínima: 980 px) e (largura máxima: 1199 px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-768px-979px.css</td>
   <td>Estilos de mídia entre 768 e 979 pixels de largura. </td>
   <td><p>@media (largura mínima: 768 px) e (largura máxima: 979 px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-767px-max.css</td>
   <td>Estilos para todas as mídias com menos de 768 pixels de largura.</td>
   <td><p>@media (max-width: 767 px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-480px.css</td>
   <td>Estilos para todas as mídias com menos de 481 pixels de largura.</td>
   <td>@media (max-width: 480 px) {<br /> ...<br /> }</td>
  </tr>
 </tbody>
</table>

O arquivo css.txt na pasta `/etc/designs/weretail/clientlibs` lista os arquivos CSS incluídos na pasta da biblioteca do cliente. A ordem dos arquivos implementa a precedência de estilo. Os estilos são mais específicos à medida que o tamanho do dispositivo diminui.

`#base=css`

```
style.css
 bootstrap.css
```

```
responsive-1200px.css
 responsive-980px-1199px.css
 responsive-768px-979px.css
 responsive-767px-max.css
 responsive-480px.css
```

**Dica**: nomes de arquivos descritivos permitem identificar facilmente o tamanho do visor direcionado.

### Uso de consultas de mídia com páginas AEM {#using-media-queries-with-aem-pages}

Inclua a pasta da biblioteca do cliente no script JSP do componente de página. Isso ajuda a gerar o arquivo CSS que inclui as consultas de mídia e faz referência ao arquivo.

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

>[!NOTE]
>
>A pasta da biblioteca do cliente `apps.weretail.all` incorpora a biblioteca clientlibs.

O script JSP gera o seguinte código de HTML que faz referência às folhas de estilos:

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## Visualização de dispositivos específicos {#previewing-for-specific-devices}

Veja visualizações de suas páginas em diferentes tamanhos de visor para testar o comportamento do design responsivo. No modo **[!UICONTROL Visualização]**, o **[!UICONTROL Sidekick]** inclui um menu suspenso de **[!UICONTROL Dispositivos]** que você usa para selecionar um dispositivo. Ao selecionar um dispositivo, a página muda para se adaptar ao tamanho do visor.

![chlimage_1-5](assets/chlimage_1-5a.png)

Para habilitar a visualização de dispositivo em **[!UICONTROL Sidekick]**, configure a página e o serviço **[!UICONTROL MobileEmulatorProvider]**. Outra configuração de página controla a lista de dispositivos que aparece na lista **[!UICONTROL Dispositivos]**.

### Adicionando a lista de dispositivos {#adding-the-devices-list}

A lista **[!UICONTROL Dispositivos]** aparece em **[!UICONTROL Sidekick]** quando a página inclui o script JSP que renderiza a lista **[!UICONTROL Dispositivos]**. Para adicionar a lista **[!UICONTROL Dispositivos]** a **[!UICONTROL Sidekick]**, inclua o script `/libs/wcm/mobile/components/simulator/simulator.jsp` na seção `head` da sua página.

Inclua o seguinte código no JSP que define a seção `head`:

`<cq:include script="/libs/wcm/mobile/components/simulator/simulator.jsp"/>`

Para ver um exemplo, abra o arquivo `/apps/weretail/components/page/head.jsp` no CRXDE Lite.

### Registrando componentes de Página para simulação {#registering-page-components-for-simulation}

Para habilitar o simulador de dispositivo para oferecer suporte às suas páginas, registre os componentes da página no serviço de fábrica MobileEmulatorProvider e defina a propriedade `mobile.resourceTypes`.

Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos.

Por exemplo, para criar um nó ` [sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)` no aplicativo:

* Pasta pai: `/apps/application_name/config`
* Nome: `com.day.cq.wcm.mobile.core.impl.MobileEmulatorProvider-*alias*`

  O sufixo - `*alias*` é necessário porque o serviço MobileEmulatorProvider é um serviço de fábrica. Use qualquer alias que seja exclusivo para esta fábrica.

* `jcr:primaryType`: `sling:OsgiConfig`

Adicione a seguinte propriedade do nó:

* Nome: `mobile.resourceTypes`
* Tipo: `String[]`
* Valor: os caminhos para os componentes da página que renderizam suas páginas da Web. Por exemplo, o aplicativo geometrixx-media usa os seguintes valores:

  ```
  geometrixx-media/components/page
   geometrixx-unlimited/components/pages/page
   geometrixx-unlimited/components/pages/coverpage
   geometrixx-unlimited/components/pages/issue
  ```

### Especificando os grupos de dispositivos {#specifying-the-device-groups}

Para especificar os grupos de dispositivos que aparecem na lista Dispositivos, adicione uma propriedade `cq:deviceGroups` ao nó `jcr:content` da página raiz do site. O valor da propriedade é uma matriz de caminhos para os nós do grupo de dispositivos.

Os nós do grupo de dispositivos estão na pasta `/etc/mobile/groups`.

Por exemplo, a página raiz do site Geometrixx Media é `/content/geometrixx-media`. O nó `/content/geometrixx-media/jcr:content` inclui a seguinte propriedade:

* Nome: `cq:deviceGroups`
* Tipo: `String[]`
* Valor: `/etc/mobile/groups/responsive`

Use o console Ferramentas para [criar e editar grupos de dispositivos](/help/sites-developing/groupfilters.md).

>[!NOTE]
>
>Para grupos de dispositivos que você usa para design responsivo, edite o grupo de dispositivos e, na guia Geral, selecione Desativar emulador. Essa opção impede que o carrossel do emulador apareça, o que não é relevante para o design responsivo.
>

## Uso de imagens adaptáveis {#using-adaptive-images}

Você pode usar consultas de mídia para selecionar um recurso de imagem a ser exibido na página. No entanto, cada recurso que usa um query de mídia para condicionalizar seu uso é baixado para o cliente. A consulta de mídia simplesmente determina se o recurso baixado é exibido.

Para recursos grandes, como imagens, baixar todos os recursos não é um uso eficiente do pipeline de dados do cliente. Para baixar recursos seletivamente, use o JavaScript para iniciar a solicitação de recurso depois que as consultas de mídia executarem a seleção.

A estratégia a seguir carrega um único recurso que é escolhido usando consultas de mídia:

1. Adicione um elemento DIV para cada versão do recurso. Inclua o URI do recurso como o valor de um valor de atributo. O navegador não interpreta o atributo como um recurso.
1. Adicione uma consulta de mídia a cada elemento DIV apropriado para o recurso.
1. Quando o documento é carregado ou a janela é redimensionada, o código JavaScript testa a consulta de mídia de cada elemento DIV.
1. Com base nos resultados dos queries, determine qual recurso incluir.
1. Insira um elemento HTML no DOM que faça referência ao recurso.

### Avaliação de consultas de mídia usando o JavaScript {#evaluating-media-queries-using-javascript}

As implementações da [interface MediaQueryList](https://drafts.csswg.org/cssom-view/#the-mediaquerylist-interface) que o W3C define permitem avaliar consultas de mídia usando o JavaScript. Você pode aplicar lógica aos resultados da consulta de mídia e executar scripts direcionados para a janela atual:

* Os navegadores que implementam a interface MediaQueryList dão suporte à função `window.matchMedia()`. Esta função testa as consultas de mídia em relação a uma determinada sequência de caracteres. A função retorna um objeto `MediaQueryList` que fornece acesso aos resultados da consulta.

* Para navegadores que não implementam a interface, você pode usar um `matchMedia()` polyfill, como [matchMedia.js](https://github.com/paulirish/matchMedia.js), uma biblioteca de JavaScript disponível gratuitamente.

#### Seleção de recursos específicos de mídia {#selecting-media-specific-resources}

O [elemento de imagem](https://html.spec.whatwg.org/multipage/embedded-content.html#the-picture-element) do W3C usa consultas de mídia para determinar a origem a ser usada para elementos de imagem. O elemento de imagem usa atributos de elemento para associar consultas de mídia a caminhos de imagem.

A [biblioteca picturefill.js](https://github.com/scottjehl/picturefill) disponível gratuitamente fornece funcionalidade semelhante ao elemento `picture` proposto e usa uma estratégia semelhante. A biblioteca picturefill.js chama `window.matchMedia` para avaliar as consultas de mídia definidas para um conjunto de elementos `div`. Cada elemento `div` também especifica uma fonte de imagem. A origem é usada quando a consulta de mídia do elemento `div` retorna `true`.

A biblioteca `picturefill.js` requer um código de HTML semelhante ao seguinte exemplo:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
</div>
```

Quando a página é renderizada, picturefull.js insere um elemento `img` como o último filho do elemento `<div data-picture>`:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
    <img src="path to medium image">
</div>
```

Em uma página AEM, o valor do atributo `data-src` é o caminho para um recurso no repositório.

### Implementação de imagens adaptáveis no AEM {#implementing-adaptive-images-in-aem}

Para implementar imagens adaptáveis em seu aplicativo AEM, você deve adicionar as bibliotecas JavaScript necessárias e incluir a marcação HTML necessária em suas páginas.

**Bibliotecas**

Obtenha as seguintes bibliotecas JavaScript e inclua-as em uma pasta da biblioteca do cliente:

* [matchMedia.js](https://github.com/paulirish/matchMedia.js) (para navegadores que não implementam a interface MediaQueryList)
* [picturefill.js](https://github.com/scottjehl/picturefill)
* jquery.js (disponível por meio da pasta da biblioteca do cliente `/etc/clientlibs/granite/jquery` (category = jquery)
* [jquery.debouncedresize.js](https://github.com/louisremi/jquery-smartresize) (um evento jquery que ocorre uma vez depois que a janela é redimensionada)

**Dica:** você pode concatenar automaticamente várias pastas da biblioteca do cliente ao [incorporar](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries).

**HTML**

Crie um componente que gera os elementos div necessários que o código picturefill.js espera. Em uma página AEM, o valor do atributo data-src é o caminho para um recurso no repositório. Por exemplo, um componente de Página pode codificar as consultas de mídia e os caminhos associados para representações de imagem no DAM. Ou crie um componente de Imagem personalizado que permita aos autores selecionar representações de imagem ou especificar opções de renderização em tempo de execução.

O HTML de exemplo a seguir seleciona entre duas representações DAM da mesma imagem.

```xml
<div data-picture>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png'></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.319.319.png'    data-media="(min-width: 769px)"></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.140.100.png'   data-media="(min-width: 481px)"></div>
</div>
```

>[!NOTE]
>
>O componente de base da Imagem adaptável implementa imagens adaptáveis:
>
>* Pasta da biblioteca do cliente: `/libs/foundation/components/adaptiveimage/clientlibs`
>* Script que gera o HTML: `/libs/foundation/components/adaptiveimage/adaptiveimage.jsp`
>
>A seção subsequente fornece detalhes sobre esse componente.
>

### Como entender a renderização de imagem no AEM {#understanding-image-rendering-in-aem}

Para personalizar a renderização de imagens, você deve entender a implementação padrão da renderização de imagem estática do AEM. O AEM fornece o componente de Imagem e um servlet de renderização de imagem que trabalham juntos para renderizar imagens para a página da Web. As seguintes sequências de eventos ocorrem quando o componente de Imagem é incluído no sistema de parágrafos da página:

1. Criação: os autores editam o componente de Imagem para especificar o arquivo de imagem a ser incluído em uma página de HTML. O caminho do arquivo é armazenado como um valor de propriedade do nó do componente de Imagem.
1. Solicitação de página: o JSP do componente de página gera o código HTML. O JSP do componente de Imagem gera e adiciona um elemento img à página.
1. Solicitação de imagem: o navegador carrega a página e solicita a imagem de acordo com o atributo src do elemento img.
1. Renderização de imagem: o servlet de renderização de imagem retorna a imagem para o navegador da Web.

![chlimage_1-6](assets/chlimage_1-6a.png)

Por exemplo, o JSP do componente de Imagem gera o seguinte elemento de HTML:

`<img title="My Image" alt="My Image" class="cq-dd-image" src="/content/mywebsite/en/_jcr_content/par/image_0.img.jpg/1358372073597.jpg">`

Quando o navegador carrega a página, ele solicita a imagem usando o valor do atributo src como o URL. O Sling decompõe o URL:

* Recurso: `/content/mywebsite/en/_jcr_content/par/image_0`
* Extensão de nome de arquivo: `.jpg`
* Seletor: `img`
* Sufixo: `1358372073597.jpg`

O nó `image_0` tem um valor `jcr:resourceType` de `foundation/components/image`, que tem um valor `sling:resourceSuperType` de `foundation/components/parbase`. O componente parbase inclui o script img.GET.java que corresponde ao seletor e a extensão de nome de arquivo do URL da solicitação. O CQ usa esse script (servlet) para renderizar a imagem.

Para ver o código-fonte do script, use CRXDE Lite para abrir o `/libs/foundation/components/parbase/img.GET.java`
arquivo.

## Dimensionar imagens para o tamanho atual do visor {#scaling-images-for-the-current-viewport-size}

Dimensione imagens no tempo de execução de acordo com as características do visor do cliente para fornecer imagens que estejam em conformidade com os princípios de design responsivo. Use o mesmo padrão de design como renderização de imagem estática, usando um servlet e um componente de criação.

O componente deve executar as seguintes tarefas:

* Armazene o caminho e as dimensões desejadas do recurso de imagem como valores de propriedade.
* Gerar `div` elementos que contêm seletores de mídia e chamadas de serviço para renderizar a imagem.

>[!NOTE]
>
>O cliente da Web usa as bibliotecas JavaScript matchMedia e Picturefill (ou bibliotecas semelhantes) para avaliar os seletores de mídia.
>

O servlet que processa a solicitação de imagem deve executar as seguintes tarefas:

* Recupere o caminho e as dimensões da imagem das propriedades do componente.
* Dimensione a imagem de acordo com as propriedades e retorne a imagem.

**Soluções disponíveis**

O AEM instala as seguintes implementações que você pode usar ou estender.

* O componente de base da Imagem adaptável que gera consultas de mídia e solicitações HTTP para o Servlet do componente de Imagem adaptável que dimensiona as imagens.
* O pacote Geometrixx Commons instala os servlets de amostra do Image Reference Modification Servlet que alteram a resolução da imagem.

### Noções básicas sobre o componente de Imagem adaptável {#understanding-the-adaptive-image-component}

O componente de Imagem adaptável gera chamadas para o Servlet do componente de Imagem adaptável para renderizar uma imagem que é dimensionada de acordo com a tela do dispositivo. O componente inclui os seguintes recursos:

* JSP: adiciona elementos div que associam consultas de mídia a chamadas para o Servlet do componente de imagem adaptável.
* Bibliotecas do cliente: a pasta clientlibs é um `cq:ClientLibraryFolder` que monta a biblioteca JavaScript matchMedia polyfill e uma biblioteca JavaScript Picturefill modificada.
* Caixa de diálogo de edição: o nó `cq:editConfig` substitui o componente de imagem de base CQ para que o destino de soltar crie um componente de imagem adaptável em vez de um componente de imagem de base.

#### Adição de elementos DIV {#adding-the-div-elements}

O script adaptive-image.jsp inclui o seguinte código que gera elementos div e consultas de mídia:

```
<div data-picture data-alt='<%= alt %>'>
    <div data-src='<%= path + ".img.320.low." + extension + suffix %>'       data-media="(min-width: 1px)"></div>                                        <%-- Small mobile --%>
    <div data-src='<%= path + ".img.320.medium." + extension + suffix %>'    data-media="(min-width: 320px)"></div>  <%-- Portrait mobile --%>
    <div data-src='<%= path + ".img.480.medium." + extension + suffix %>'    data-media="(min-width: 321px)"></div>  <%-- Landscape mobile --%>
    <div data-src='<%= path + ".img.476.high." + extension + suffix %>'      data-media="(min-width: 481px)"></div>   <%-- Portrait iPad --%>
    <div data-src='<%= path + ".img.620.high." + extension + suffix %>'      data-media="(min-width: 769px)"></div>  <%-- Landscape iPad --%>
    <div data-src='<%= path + ".img.full.high." + extension + suffix %>'     data-media="(min-width: 1025px)"></div> <%-- Desktop --%>

    <%-- Fallback content for non-JS browsers. Same img src as the initial, unqualified source element. --%>
    <noscript>
        <img src='<%= path + ".img.320.low." + extension + suffix %>' alt='<%= alt %>'>
    </noscript>
</div>
```

A variável `path` contém o caminho do recurso atual (o nó do componente de imagem adaptável). O código gera uma série de elementos `div` com a seguinte estrutura:

`<div data-scr = "*path-to-parent-node*.adaptive-image.adapt.*width*.*quality*.jpg" data-media="*media query*"></div>`

O valor do atributo `data-scr` é uma URL que o Sling resolve para o Servlet do componente de Imagem adaptável que renderiza a imagem. O atributo data-media contém a consulta de mídia que é avaliada em relação às propriedades do cliente.

O código de HTML a seguir é um exemplo dos elementos `div` gerados pelo JSP:

```xml
<div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.low.jpg'></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.medium.jpg'    data-media="(min-width: 320px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.480.medium.jpg'    data-media="(min-width: 321px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.476.high.jpg'     data-media="(min-width: 481px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.620.high.jpg'     data-media="(min-width: 769px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.full.high.jpg'     data-media="(min-width: 1025px)"></div>
```

#### Alteração dos seletores de tamanho da imagem {#changing-the-image-size-selectors}

Se você personalizar o componente de Imagem adaptável e alterar os seletores de largura, também deverá configurar o Servlet do componente de Imagem adaptável para oferecer suporte às larguras.

### Compreender o servlet do componente de imagem adaptável {#understanding-the-adaptive-image-component-servlet}

O Servlet do componente de Imagem adaptável redimensiona uma imagem de JPEG de acordo com uma largura especificada e define a qualidade do JPEG.

#### A interface do Servlet do componente de Imagem adaptável {#the-interface-of-the-adaptive-image-component-servlet}

O Servlet do componente de Imagem adaptável está vinculado ao servlet Sling padrão e é compatível com as extensões de arquivo .jpg, .jpeg, .gif e .png. O seletor de servlet é img.

>[!CAUTION]
>
>Arquivos .gif animados não são suportados no AEM para representações adaptáveis.

Portanto, o Sling resolve URLs de solicitação HTTP do seguinte formato para esse servlet:

`*path-to-node*.img.*extension*`

Por exemplo, o Sling encaminha solicitações HTTP com a URL `http://localhost:4502/content/geometrixx/adaptiveImage.img.jpg` para o Servlet do componente de imagem adaptável.

JPEG Dois seletores adicionais especificam a largura e a qualidade da imagem solicitada. O exemplo a seguir solicita uma imagem de largura de 480 pixels e qualidade média:

`http://localhost:4502/content/geometrixx/adaptiveImage.adapt.480.MEDIUM.jpg`

**Propriedades de imagem com suporte**

O servlet aceita um número finito de larguras e qualidades de imagem. As seguintes larguras são suportadas por padrão (em pixels):

* completo
* 320
* 480
* 476
* 620

O valor inteiro indica sem dimensionamento.

Os seguintes valores de qualidade do JPEG são suportados:

* BAIXA
* MÉDIA
* ALTA

Os valores numéricos são 0,4, 0,82 e 1,0, respectivamente.

**Alterando as larguras padrão com suporte**

Use o Console da Web ([http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)) ou um nó sling:OsgiConfig para configurar as larguras com suporte do Servlet do Componente de Imagem Adaptável do Adobe CQ.

Para obter informações sobre como configurar serviços AEM, consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md).

<table>
 <tbody>
  <tr>
   <th> </th>
   <th>Console da Web</th>
   <th>sling:OsgiConfig</th>
  </tr>
  <tr>
   <th>Nome do serviço ou nó</th>
   <td>O nome do serviço na guia Configuração é Servlet do componente de imagem adaptável do Adobe CQ</td>
   <td>com.day.cq.wcm.foundation.impl ServletComponenteDeImagemAdaptável</td>
  </tr>
  <tr>
   <th>Propriedade</th>
   <td><p>Larguras suportadas</p>
    <ul>
     <li>Para adicionar uma largura compatível, clique em um botão + e insira um número inteiro positivo.</li>
     <li>Para remover uma largura suportada, clique no botão - associado.</li>
     <li>Para modificar uma largura compatível, edite o valor do campo.</li>
    </ul> </td>
   <td><p>adapt.supported.widths</p>
    <ul>
     <li>A propriedade é um valor de string com vários valores.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### Detalhes da implementação {#implementation-details}

A classe `com.day.cq.wcm.foundation.impl.AdaptiveImageComponentServlet` estende a classe [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html). O código-fonte AdaptiveImageComponentServlet está na pasta `/libs/foundation/src/impl/src/com/day/cq/wcm/foundation/impl`.

A classe usa anotações Felix SCR para configurar o tipo de recurso e a extensão de arquivo à qual o servlet está associado, além do nome do primeiro seletor.

```java
@Component(metatype = true, label = "Adobe CQ Adaptive Image Component Servlet",
        description = "Render adaptive images in a variety of qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = "foundation/components/adaptiveimage", propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "img", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value ={
            "jpg",
            "jpeg",
            "png",
            "gif"
    }, propertyPrivate = true)
})
```

O servlet usa a anotação SCR de propriedade para definir a qualidade e as dimensões de imagem padrão suportadas.

```java
@Property(value = {
            "320", // iPhone portrait
            "480", // iPhone landscape
            "476", // iPad portrait
            "620" // iPad landscape
    },
            label = "Supported Widths",
            description = "List of widths this component is permitted to generate.")
```

A classe `AbstractImageServlet` fornece o método `doGet` que processa a solicitação HTTP. Este método determina o recurso associado à solicitação, recupera propriedades de recurso do repositório e as retorna em um objeto [ImageContext](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html).

>[!NOTE]
>
>A classe [com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html) fornece o `getFileReference method`, que recupera o valor da propriedade `fileReference` do recurso.

A classe `AdaptiveImageComponentServlet` substitui o método `createLayer`. O método obtém o caminho do recurso de imagem e a largura de imagem solicitada do objeto `ImageContext`. Em seguida, ele chama os métodos da classe `info.geometrixx.commons.impl.AdaptiveImageHelper`, que executa o dimensionamento real da imagem.

A classe AdaptiveImageComponentServlet também substitui o método writeLayer. Este método aplica a qualidade do JPEG à imagem.

### Servlet de modificação de referência de imagem (Geometrixx Common) {#image-reference-modification-servlet-geometrixx-common}

O servlet de modificação de referência de imagem de amostra gera atributos de tamanho para o elemento img dimensionar uma imagem na página da Web.

#### Chamar o servlet {#calling-the-servlet}

O servlet está vinculado a `cq:page` recursos e oferece suporte à extensão de arquivo .jpg. O seletor de servlet é `image`. Portanto, o Sling resolve URLs de solicitação HTTP do seguinte formato para esse servlet:

`path-to-page-node.image.jpg`

Por exemplo, o Sling encaminha solicitações HTTP com a URL `http://localhost:4502/content/geometrixx/en.image.jpg` para o Servlet de modificação de referência de imagem.

Três seletores adicionais especificam a largura, a altura e a qualidade da imagem solicitada. O exemplo a seguir solicita uma imagem de largura 770 pixels, altura 360 pixels e qualidade média.

`http://localhost:4502/content/geometrixx/en.image.770.360.MEDIUM.jpg`

**Propriedades de imagem com suporte**

O servlet aceita um número finito de dimensões de imagem e valores de qualidade.

Os seguintes valores são suportados por padrão (widthxheight):

* 256x192
* 370x150
* 480x200
* 127x127
* 770x360
* 620x290
* 480x225
* 320x150
* 375x175
* 303x142
* 1170x400
* 940x340
* 770x300
* 480x190

Os seguintes valores de qualidade de imagem são compatíveis:

* baixa
* médio
* alta

Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos.

#### Especificação do recurso de imagem {#specifying-the-image-resource}

O caminho da imagem, as dimensões e os valores de qualidade devem ser armazenados como propriedades de um nó no repositório:

* O nome do nó é `image`.
* O nó pai é o nó `jcr:content` de um recurso `cq:page`.

* O caminho da imagem é armazenado como o valor de uma propriedade chamada `fileReference`.

Ao criar uma página, use **Sidekick** para especificar a imagem e adicionar o nó `image` às propriedades da página:

1. Em **Sidekick**, clique na guia **Página** e em **Propriedades da Página**.
1. Clique na guia **Imagem** e especifique a imagem.
1. Clique em **OK**.

#### Detalhes da implementação {#implementation-details-1}

A classe info.geometrixx.commons.impl.servlets.ImageReferenceModificationServlet estende a classe [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html). Se você tiver o pacote cq-geometrixx-commons-pkg instalado, o código-fonte ImageReferenceModificationServlet estará na pasta `/apps/geometrixx-commons/src/core/src/main/java/info/geometrixx/commons/impl/servlets`.

A classe usa anotações Felix SCR para configurar o tipo de recurso e a extensão de arquivo à qual o servlet está associado, além do nome do primeiro seletor.

```java
@Component(metatype = true, label = "Adobe CQ Image Reference Modification Servlet",
        description = "Render the image associated with a page in a variety of dimensions and qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = NameConstants.NT_PAGE, propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "image", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value = "jpg", propertyPrivate = true)
})
```

O servlet usa a anotação SCR de propriedade para definir a qualidade e as dimensões de imagem padrão suportadas.

```java
@Property(label = "Image Quality",
            description = "Quality must be a double between 0.0 and 1.0", value = "0.82")
@Property(value = {
                "256x192", // Category page article list images
                "370x150", // "Most popular" desktop & iPad & carousel min-width: 1px
                "480x200", // "Most popular" phone
                "127x127", // article summary phone square images
                "770x360", // article summary, desktop
                "620x290", // article summary, tablet
                "480x225", // article summary, phone (landscape)
                "320x150", // article summary, phone (portrait) and fallback
                "375x175", // 2-column article summary, desktop
                "303x142", // 2-column article summary, tablet
                "1170x400", // carousel, full
                "940x340",  // carousel min-width: 980px
                "770x300",  // carousel min-width: 768px
                "480x190"   // carousel min-width: 480px
            },
            label = "Supported Resolutions",
            description = "List of resolutions this component is permitted to generate.")
```

A classe `AbstractImageServlet` fornece o método `doGet` que processa a solicitação HTTP. Este método determina o recurso associado à chamada, recupera propriedades de recurso do repositório e as salva em um objeto [ImageContext](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html).

A classe `ImageReferenceModificationServlet` substitui o método `createLayer` e implementa a lógica que determina o recurso de imagem a ser renderizado. O método recupera um nó filho do nó `jcr:content` da página chamado `image`. Um objeto [Image](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/Image.html) é criado a partir deste nó `image`, e o método `getFileReference` retorna o caminho para o arquivo de imagem da propriedade `fileReference` do nó de imagem.

>[!NOTE]
>A classe [com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html) fornece o getFileReferencemethod.
>

## Desenvolvimento de uma grade de fluidos {#developing-a-fluid-grid}

O AEM permite que você implemente de forma eficiente e eficaz grades de fluidos. Esta página explica como você pode integrar sua grade fluida ou uma implementação de grade existente (como o [Bootstrap](https://github.com/topics/twitter-bootstrap?l=css)) ao aplicativo AEM.

Se você não estiver familiarizado com grades fluidas, consulte a seção [Introdução a Grades Fluidas](/help/sites-developing/responsive.md#developing-a-fluid-grid) na parte inferior desta página. Esta introdução fornece uma visão geral das grades de fluidos e orientação para projetá-las.

### Definição da grade usando um componente de Página {#defining-the-grid-using-a-page-component}

Use componentes de página para gerar os elementos HTML que definem os blocos de conteúdo da página. A ClientLibraryFolder à qual a página faz referência fornece o CSS que controla o layout dos blocos de conteúdo:

* Componente da página: adiciona elementos div que representam linhas de blocos de conteúdo. Os elementos div que representam blocos de conteúdo incluem um componente parsys no qual os autores adicionam conteúdo.
* Pasta da biblioteca do cliente: fornece o arquivo CSS que inclui consultas de mídia e estilos para os elementos div.

Por exemplo, o aplicativo de amostra geometrixx-media contém o componente media-home. Este componente de página insere dois scripts, que geram dois elementos `div` da classe `row-fluid`:

* A primeira linha contém um elemento `div` da classe `span12` (o conteúdo abrange 12 colunas). O elemento `div` contém o componente parsys.

* A segunda linha contém dois elementos `div`, um da classe `span8` e outro da classe `span4`. Cada elemento `div` inclui o componente parsys.

```xml
<div class="page-content">
    <div class="row-fluid">
        <div class="span12">
            <cq:include path="grid-12-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
    <div class="row-fluid">
        <div class="span8">
            <cq:include path="grid-8-par" resourceType="foundation/components/parsys" />
        </div>
        <div class="span4">
            <cq:include path="grid-4-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
</div>
```

>[!NOTE]
>
>Quando um componente inclui vários elementos `cq:include` que fazem referência ao componente parsys, cada atributo `path` deve ter um valor diferente.
>

#### Dimensionamento da grade de componentes Página {#scaling-the-page-component-grid}

O design associado ao componente de página de mídia geometrixx (`/etc/designs/geometrixx-media`) contém ClientLibraryFolder `clientlibs`. Esta ClientLibraryFolder define estilos CSS para classes `row-fluid`, classes `span*` e classes `span*` que são filhos de classes `row-fluid`. Os queries de mídia permitem que os estilos sejam redefinidos para tamanhos de visor diferentes.

O exemplo de CSS a seguir é um subconjunto desses estilos. Esse subconjunto focaliza as classes `span12`, `span8` e `span4`, e as consultas de mídia para dois tamanhos de visor. Observe as seguintes características do CSS:

* Os estilos `.span` definem larguras de elemento usando números absolutos.
* Os estilos `.row-fluid .span*` definem larguras de elemento como porcentagens do pai. As porcentagens são calculadas a partir das larguras absolutas.
* As consultas de mídia para janelas de visualização maiores atribuem larguras absolutas maiores.

>[!NOTE]
>
>A amostra de Geometrixx Media integra a estrutura do JavaScript [Bootstrap](https://getbootstrap.com/2.0.2/) em sua implementação de grade fluida. A estrutura do Bootstrap fornece o arquivo bootstrap.css.

```xml
/* default styles (no media queries) */
 .span12 { width: 940px }
 .span8 { width: 620px }
 .span4 { width: 300px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.95744680851064% }
 .row-fluid .span4 { width: 31.914893617021278% }

@media (min-width: 768px) and (max-width: 979px) {
 .span12 { width: 724px; }
 .span8 {     width: 476px; }
 .span4 {     width: 228px; }
 .row-fluid .span12 {     width: 100%;}
 .row-fluid .span8 {     width: 65.74585635359117%; }
 .row-fluid .span4 {     width: 31.491712707182323%; }
}

@media (min-width: 1200px) {
 .span12 { width: 1170px }
 .span8 { width: 770px }
 .span4 { width: 370px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.81196581196582% }
 .row-fluid .span4 { width: 31.623931623931625% }
}
```

#### Reposicionamento de conteúdo na grade do componente Página {#repositioning-content-in-the-page-component-grid}

As páginas do aplicativo de amostra Geometrixx Media distribuem linhas de blocos de conteúdo horizontalmente em janelas de visualização amplas. Em janelas de visualização menores, os mesmos blocos são distribuídos verticalmente. O exemplo de CSS a seguir mostra os estilos que implementam esse comportamento para o código de HTML gerado pelo componente de página inicial de mídia:

* O CSS padrão da página de boas-vindas de mídia atribui o estilo `float:left` para as classes `span*` que estão dentro das classes `row-fluid`.

* As consultas de mídia para janelas de visualização menores atribuem o estilo `float:none` para as mesmas classes.

```xml
/* default styles (no media queries) */
    .row-fluid [class*="span"] {
        width: 100%;
        float: left;
}

@media (max-width: 767px) {
    [class*="span"], .row-fluid [class*="span"] {
        float: none;
        width: 100%;
    }
}
```

#### Modular os componentes da página {#tip-modularize-your-page-components}

Module seus componentes para que você possa usar o código com eficiência. Seu site provavelmente usa vários tipos diferentes de páginas, como uma página de boas-vindas, uma página de artigo ou uma página de produto. Cada tipo de página contém diferentes tipos de conteúdo e provavelmente usam diferentes layouts. No entanto, quando determinados elementos de cada layout são comuns em várias páginas, você pode reutilizar o código que implementa essa parte do layout.

**Usar sobreposições de componentes da página**

Crie um componente de página principal que forneça scripts para gerar as várias partes de uma página, como as seções `head` e `body` e as seções `header`, `content` e `footer` do corpo.

Crie outros componentes de página que usam o componente de página principal como o `cq:resourceSuperType`. Esses componentes incluem scripts que substituem os scripts da página principal, conforme necessário.

Por exemplo, o aplicativo goemetrixx-media inclui o componente de página (o `sling:resourceSuperType` é o componente de página de base). Vários componentes filhos (como artigo, categoria e media-home) usam esse componente de página como `sling:resourceSuperType`. Cada componente secundário inclui um arquivo content.jsp que substitui o arquivo content.jsp do componente Página.

**Reutilizar scripts**

Crie vários scripts JSP que geram combinações de linha e coluna comuns para vários componentes da página. Por exemplo, o script `content.jsp` do artigo e os componentes media-home fazem referência ao script `8x4col.jsp`.

**Organizar estilos CSS por tamanho de visor direcionado**

Inclua estilos CSS e consultas de mídia para diferentes tamanhos de visor em arquivos separados. Use as pastas da biblioteca do cliente para concatená-las.

### Inserir componentes na grade da página {#inserting-components-into-the-page-grid}

Quando os componentes geram um único bloco de conteúdo, geralmente a grade que o componente de página estabelece controla o posicionamento do conteúdo.

Como autor, o bloco de conteúdo pode ser renderizado em vários tamanhos e posições relativas. O texto do conteúdo não deve usar direções relativas para se referir a outros blocos de conteúdo.

Se necessário, o componente deve fornecer bibliotecas CSS ou JavaScript necessárias para o código HTML gerado. Use uma pasta da biblioteca do cliente dentro do componente para que os arquivos CSS e JS sejam gerados. Para expor os arquivos, [crie uma dependência ou incorpore a biblioteca](/help/sites-developing/clientlibs.md#creating-client-library-folders) em outra pasta da biblioteca do cliente abaixo da pasta /etc.

**Subgrades**

Se o componente contiver vários blocos de conteúdo, adicione os blocos de conteúdo dentro de uma linha para estabelecer uma subgrade na página:

* Use os mesmos nomes de classe do componente página de contenção para expressar elementos div como linhas e blocos de conteúdo.
* Para substituir o comportamento que o CSS do design da página implementa, use um nome de segunda classe para o elemento div da linha e forneça o CSS associado em uma pasta da biblioteca do cliente.

Por exemplo, o componente `/apps/geometrixx-media/components/2-col-article-summary` gera duas colunas de conteúdo. O HTML gerado tem a seguinte estrutura:

```xml
<div class="row-fluid mutli-col-article-summary">
    <div class="span6">
        <article>
            <div class="article-summary-image">...</div>
            <div class="social-header">...</div>
            <div class="article-summary-description">...</div>
            <div class="social">...</div>
        </article>
    </div>
</div>
```

Os seletores `.row-fluid .span6` do CSS da página se aplicam aos elementos `div` da mesma classe e estrutura neste HTML. No entanto, o componente também inclui a pasta /apps/geometrixx-media/components/2-col-article-summary/clientlibs da biblioteca do cliente:

* O CSS usa as mesmas consultas de mídia que o componente da página para estabelecer alterações no layout nas mesmas larguras de página distintas.
* Os seletores usam a classe `multi-col-article-summary` do elemento `div` da linha para substituir o comportamento da classe `row-fluid` da página.

Por exemplo, os seguintes estilos estão incluídos no arquivo `/apps/geometrixx-media/components/2-col-article-summary/clientlibs/css/responsive-480px.css`:

```xml
@media (max-width: 480px) {
    .mutli-col-article-summary .article-summary-image {
        float: left;
        width: 127px;
    }
    .mutli-col-article-summary .article-summary-description {
        width: auto;
        margin-left: 127px;
    }
    .mutli-col-article-summary .article-summary-description h4 {
        padding-left: 10px;
    }
    .mutli-col-article-summary .article-summary-text {
        margin-left: 127px;
        min-height: 122px;
        top: 0;
    }
}
```

## Introdução a grades de fluidos {#introduction-to-fluid-grids}

As grades fluídas permitem que os layouts de página se adaptem às dimensões da janela de visualização do cliente. As grades consistem em colunas e linhas lógicas que posicionam os blocos de conteúdo na página.

* As colunas determinam as posições horizontais e larguras dos blocos de conteúdo.
* As linhas determinam as posições verticais relativas dos blocos de conteúdo.

Com a tecnologia HTML5, é possível implementar a grade e manipulá-la para adaptar os layouts de página a diferentes tamanhos de visor:

* Os elementos HTML `div` contêm blocos de conteúdo que abrangem algumas colunas.
* Um ou mais desses elementos div compõem uma linha quando compartilham um elemento div pai comum.

### Uso de larguras discretas {#using-discrete-widths}

Para cada intervalo de larguras de visor que você está direcionando, use uma largura de página estática e blocos de conteúdo de largura constante. Ao redimensionar manualmente uma janela do navegador, as alterações no tamanho do conteúdo ocorrem em larguras de janela distintas (também conhecidas como pontos de interrupção). Portanto, os designs de página são mais estritamente seguidos, maximizando a experiência do usuário.

#### Dimensionamento da grade {#scaling-the-grid}

Use grades para dimensionar blocos de conteúdo e adaptá-los a diferentes tamanhos de visor. Os blocos de conteúdo se estendem por um número específico de colunas. À medida que as larguras das colunas aumentam ou diminuem para se ajustarem a diferentes tamanhos de visor, as larguras dos blocos de conteúdo aumentam ou diminuem de acordo. O dimensionamento pode suportar visores de grande e médio porte com largura suficiente para acomodar o posicionamento lado a lado dos blocos de conteúdo.

![Imagem de duas grades, uma que seja dimensionada menor que a outra.](do-not-localize/chlimage_1-1a.png)

#### Reposicionamento de conteúdo na grade {#repositioning-content-in-the-grid}

O tamanho dos blocos de conteúdo pode ser restringido por uma largura mínima, além da qual o dimensionamento não é mais eficaz. Para janelas de visualização menores, a grade pode ser usada para distribuir verticalmente blocos de conteúdo, em vez de horizontalmente.

![Imagem de duas grades, uma que seja reposicionada menor que a outra.](do-not-localize/chlimage_1-2a.png)

### Design da grade {#designing-the-grid}

Determine as colunas e linhas nas quais você deve posicionar os blocos de conteúdo nas suas páginas. Os layouts de página determinam o número de colunas e linhas que abrangem a grade.

**Número de colunas**

Inclua colunas suficientes para posicionar horizontalmente os blocos de conteúdo em todos os layouts, para todos os tamanhos de visor. Use mais colunas do que o necessário para acomodar designs de página futuros.

**Conteúdo da linha**

Use linhas para controlar o posicionamento vertical dos blocos de conteúdo. Determine os blocos de conteúdo que compartilham a mesma linha:

* Os blocos de conteúdo localizados horizontalmente um ao lado do outro em qualquer um dos layouts estão na mesma linha.
* Blocos de conteúdo localizados horizontalmente (visores mais largos) e verticalmente (visores menores) próximos um do outro estão na mesma linha.

### Implementações em grade {#grid-implementations}

Crie classes e estilos CSS para controlar o layout dos blocos de conteúdo em uma página. Os designs de página geralmente são baseados no tamanho relativo e na posição dos blocos de conteúdo no visor. O visor determina o tamanho real dos blocos de conteúdo. Seu CSS deve considerar os tamanhos relativo e absoluto. Você pode implementar uma grade fluida usando três tipos de classes CSS:

* Uma classe para um elemento `div` que é um contêiner para todas as linhas. Essa classe define a largura absoluta da grade.
* Uma classe para `div` elementos que representam uma linha. Essa classe controla o posicionamento horizontal ou vertical dos blocos de conteúdo que ela contém.
* Classes para elementos `div` que representam blocos de conteúdo de diferentes larguras. As larguras são expressas como uma porcentagem do pai (a linha).

As larguras do visor direcionado (e seus queries de mídia associados) demarcam larguras distintas usadas para um layout de página.

#### Larguras dos blocos de conteúdo {#widths-of-content-blocks}

Geralmente, os estilos `width` de classes de blocos de conteúdo são baseados nas seguintes características da página e da grade:

* A largura absoluta da página que você está usando para cada tamanho de visor direcionado. Valores conhecidos.
* A largura absoluta das colunas de grade para cada largura de página. Você determina esses valores.
* A largura relativa de cada coluna como uma porcentagem da largura total da página. Você calcula esses valores.

O CSS inclui uma série de consultas de mídia que usam a seguinte estrutura:

```xml
@media(query_for_targeted_viewport){

  .class_for_container{ width:absolute_page_width }
  .class_for_row { width:100%}

  /* several selectors for content blocks   */
  .class_for_content_block1 { width:absolute_block_width1 }
  .class_for_content_block2 { width:absolute_block_width2 }
  ...

  /* several selectors for content blocks inside rows */
  .class_for_row .class_for_content_block1 { width:relative_block_width1 }
  .class_for_row .class_for_content_block2 { width:relative_block_width2 }
  ...
}
```

Use o algoritmo a seguir como ponto de partida para desenvolver as classes de elemento e os estilos CSS para as suas páginas.

1. Defina um nome de classe para o elemento div que contém todas as linhas, por exemplo, `content.`
1. Defina uma classe CSS para elementos div que representam linhas, como `row-fluid`.
1. Defina nomes de classe para elementos de bloco de conteúdo. Uma classe é necessária para todas as larguras possíveis, em termos de extensões de coluna. Por exemplo, use a classe `span3` para elementos `div` que abrangem três colunas, use classes `span4` para extensões de quatro colunas. Defina quantas classes houver colunas na grade.

1. Para cada tamanho de visor que você está direcionando, adicione a consulta de mídia correspondente ao arquivo CSS. Adicione os seguintes itens em cada consulta de mídia:

   * Um seletor para a classe `content`, por exemplo, `.content{}`.
   * Seletores para cada classe de span, por exemplo, `.span3{ }`.
   * Um seletor para a classe `row-fluid`, por exemplo, `.row-fluid{ }`
   * Seletores para classes span que estão dentro de classes row-flow, por exemplo, `.row-fluid span3 { }`.

1. Adicionar estilos de largura para cada seletor:

   1. Defina a largura de `content` seletores para o tamanho absoluto da página, por exemplo, `width:480px`.
   1. Defina a largura de todos os seletores de fluido de linha para 100%.
   1. Defina a largura de todos os seletores de extensão com a largura absoluta do bloco de conteúdo. Uma grade trivial usa colunas distribuídas uniformemente com a mesma largura: `(absolute width of page)/(number of columns)`.
   1. Defina a largura dos seletores `.row-fluid .span` como uma porcentagem da largura total. Calcule esta largura usando a fórmula `(absolute span width)/(absolute page width)*100`.

#### Posicionamento de blocos de conteúdo em linhas {#positioning-content-blocks-in-rows}

Use o estilo de flutuação da classe `.row-fluid` para controlar se os blocos de conteúdo em uma linha são organizados horizontal ou verticalmente.

* O estilo `float:left` ou `float:right` causa a distribuição horizontal de elementos filho (blocos de conteúdo).

* O estilo `float:none` causa a distribuição vertical de elementos filho.

Adicione o estilo ao seletor `.row-fluid` dentro de cada consulta de mídia. Defina o valor de acordo com o layout de página que você está usando para essa consulta de mídia. Por exemplo, o diagrama a seguir ilustra uma linha que distribui conteúdo horizontalmente para janelas de visualização amplas e verticalmente para janelas de visualização estreitas.

![Duas imagens de blocos de conteúdo em uma linha; a segunda imagem mostrando a linha reposicionada.](do-not-localize/chlimage_1-3a.png)

O CSS a seguir pode implementar esse comportamento:

```xml
@media (min-width: 768px) and (max-width: 979px) {
   .row-fluid {
       width:100%;
       float:left
   }
}

@media (max-width:480px){
    .row-fluid {
       width:100%;
       float:none
   }
}
```

#### Atribuição de classes a blocos de conteúdo {#assigning-classes-to-content-blocks}

Para o layout de página de cada tamanho de visor que você está direcionando, determine o número de colunas que cada bloco de conteúdo abrange. Em seguida, determine qual classe usar para os elementos div desses blocos de conteúdo.

Ao estabelecer as classes div, é possível implementar a grade usando o aplicativo AEM.
