---
title: Design responsivo para páginas da Web
seo-title: Responsive design for web pages
description: Com o design responsivo, as mesmas páginas podem ser exibidas efetivamente em vários dispositivos em várias orientações
seo-description: With responsive design, the same pages can be effectively displayed on multiple devices in multiple orientations
uuid: 3d324557-e7ff-4c82-920f-9b5a906925e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 532544b0-1932-419a-b6bd-ecf57a926fef
legacypath: /content/docs/en/aem/6-0/develop/mobile/responsive
exl-id: c705710b-a94a-4f4f-affa-ddd4fc6cb0ec
source-git-commit: 4472da2e9aa0b45e0d5f03bfdc53a2748d82cdb3
workflow-type: tm+mt
source-wordcount: '5351'
ht-degree: 1%

---

# Design responsivo para páginas da Web{#responsive-design-for-web-pages}

>[!NOTE]
>
>O Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (como _Reagir_). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Vários exemplos são baseados no conteúdo de amostra do Geometrixx, que não é mais enviado com o AEM, tendo sido substituído por We.Retail. Consulte o documento [Implementação de referência We.Retail](/help/sites-developing/we-retail.md#we-retail-geometrixx) para saber como baixar e instalar o Geometrixx.

Projete suas páginas da Web para que elas se adaptem à janela de visualização do cliente em que são exibidas. Com o design responsivo, as mesmas páginas podem ser exibidas efetivamente em vários dispositivos em ambas as orientações. A imagem a seguir demonstra algumas maneiras pelas quais uma página pode responder às alterações no tamanho da janela de visualização:

* Layout: Use layouts de coluna única para visores menores e layouts de várias colunas para visores maiores.
* Tamanho do texto: Use um tamanho de texto maior (quando apropriado, como cabeçalhos) em visores maiores.
* Conteúdo: Inclua apenas o conteúdo mais importante ao exibir em dispositivos menores.
* Navegação: Ferramentas específicas de dispositivo são fornecidas para acessar outras páginas.
* Imagens: Exibição de representações de imagem adequadas ao visor do cliente. de acordo com as dimensões da janela.

![chlimage_1-4](assets/chlimage_1-4a.png)

Desenvolva aplicativos Adobe Experience Manager (AEM) que geram páginas HTML5 que se adaptam a vários tamanhos e orientações de janela. Por exemplo, os seguintes intervalos de larguras do visor correspondem a vários tipos de dispositivo e orientações

* Largura máxima de 480 pixels (telefone, retrato)
* Largura máxima de 767 pixels (telefone, paisagem)
* Largura entre 768 pixels e 979 pixels (tablet, retrato)
* Largura entre 980 pixels e 1199 pixels (tablet, paisagem)
* Largura de 1200px ou superior (desktop)

Consulte os tópicos a seguir para obter informações sobre como implementar o comportamento de design responsivo:

* [Consultas de mídia](/help/sites-developing/responsive.md#using-media-queries)
* [Grades de fluidos](/help/sites-developing/responsive.md#developing-a-fluid-grid)
* [Imagens adaptativas](/help/sites-developing/responsive.md#using-adaptive-images)

Conforme você projeta, use **[!UICONTROL Sidekick]** para visualizar suas páginas para vários tamanhos de tela.

## Antes de desenvolver {#before-you-develop}

Antes de desenvolver o aplicativo AEM que suporta suas páginas da Web, várias decisões de design devem ser tomadas. Por exemplo, você precisa ter as seguintes informações:

* Os dispositivos que você está direcionando.
* Os tamanhos do visor de destino.
* Os layouts de página para cada tamanho de visor direcionado.

### Estrutura do aplicativo {#application-structure}

A estrutura típica do aplicativo de AEM suporta todas as implementações de design responsivas:

* Os componentes da página ficam abaixo de /apps/*application_name*/componentes
* Os modelos ficam abaixo de /apps/*application_name*/templates
* Designs reside abaixo de /etc/designs

## Uso de consultas de mídia {#using-media-queries}

As consultas de mídia permitem o uso seletivo de estilos CSS para renderização de página. AEM ferramentas e recursos de desenvolvimento permitem que você implemente consultas de mídia de maneira eficaz e eficiente em seus aplicativos.

O grupo W3C fornece a variável [Consultas de mídia](https://www.w3.org/TR/css3-mediaqueries/) recomendação que descreve esse recurso CSS3 e a sintaxe.

### Criação do arquivo CSS {#creating-the-css-file}

No arquivo CSS, defina consultas de mídia com base nas propriedades dos dispositivos que você está direcionando. A seguinte estratégia de implementação é eficaz para gerenciar estilos para cada query de mídia:

* Use ClientLibraryFolder para definir o CSS montado quando a página é renderizada.
* Defina cada consulta de mídia e os estilos associados em arquivos CSS separados. É útil usar nomes de arquivo que representem os recursos do dispositivo da consulta de mídia.
* Defina estilos comuns a todos os dispositivos em um arquivo CSS separado.
* No arquivo css.txt de ClientLibraryFolder, ordene os arquivos CSS da lista, conforme necessário no arquivo CSS montado.

A amostra de mídia We.Retail usa essa estratégia para definir estilos no design do site. O arquivo CSS usado pelo We.Retail está localizado em `*/apps/weretail/clientlibs/clientlib-site/less/grid.less`.

A tabela a seguir lista os arquivos na pasta filho css.

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
   <td>N/D</td>
  </tr>
  <tr>
   <td>responsive-1200px.css</td>
   <td>Estilos para todas as mídias com 1200 pixels de largura ou mais larga.</td>
   <td><p>@media (largura mínima: 1200px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-980px-1199px.css</td>
   <td>Estilos para mídia com 980 pixels e 1199 pixels de largura.</td>
   <td><p>@media (largura mínima: 980px) e (largura máxima: 1199px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-768px-979px.css</td>
   <td>Estilos para mídia com largura entre 768 pixels e 979 pixels. </td>
   <td><p>@media (largura mínima: 768px) e (largura máxima: 979px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-767px-max.css</td>
   <td>Estilos para todas as mídias com menos de 768 pixels de largura.</td>
   <td><p>@media (largura máxima: 767px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-480px.css</td>
   <td>Estilos para todas as mídias com menos de 481 pixels de largura.</td>
   <td>@media (largura máxima: 480) {<br /> ...<br /> }</td>
  </tr>
 </tbody>
</table>

O arquivo css.txt na variável `/etc/designs/weretail/clientlibs` lista os arquivos CSS incluídos na pasta da biblioteca do cliente. A ordem dos arquivos implementa a precedência do estilo. Os estilos são mais específicos à medida que o tamanho do dispositivo diminui.

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

**Ponta**: Os nomes de arquivo descritivos permitem identificar facilmente o tamanho do visor direcionado.

### Uso de consultas de mídia com páginas de AEM {#using-media-queries-with-aem-pages}

Inclua a pasta da biblioteca do cliente no script JSP do seu componente de página para gerar o arquivo CSS que inclui as consultas de mídia e para fazer referência ao arquivo.

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

>[!NOTE]
>
>O `apps.weretail.all` a pasta da biblioteca do cliente incorpora a biblioteca clientlibs.

O script JSP gera o seguinte código de HTML que faz referência às folhas de estilos:

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## Visualização de dispositivos específicos {#previewing-for-specific-devices}

Consulte visualizações de suas páginas em diferentes tamanhos de visor para testar o comportamento do design responsivo. Em **[!UICONTROL Visualizar]** modo, **[!UICONTROL Sidekick]** inclui um **[!UICONTROL Dispositivos]** menu suspenso usado para selecionar um dispositivo. Quando você seleciona um dispositivo, a página muda para se adaptar ao tamanho da janela de visualização.

![chlimage_1-5](assets/chlimage_1-5a.png)

Para ativar a visualização do dispositivo em **[!UICONTROL Sidekick]**, você deve configurar a página e a variável **[!UICONTROL MobileEmulatorProvider]** serviço. Outra configuração de página controla a lista de dispositivos que aparecem no **[!UICONTROL Dispositivos]** lista.

### Adicionar a lista de dispositivos {#adding-the-devices-list}

O **[!UICONTROL Dispositivos]** aparece em **[!UICONTROL Sidekick]** quando a página inclui o script JSP que renderiza a variável **[!UICONTROL Dispositivos]** lista. Para adicionar o **[!UICONTROL Dispositivos]** listar para **[!UICONTROL Sidekick]**, inclua o `/libs/wcm/mobile/components/simulator/simulator.jsp` no `head` da sua página.

Inclua o seguinte código no JSP que define a variável `head` seção:

`<cq:include script="/libs/wcm/mobile/components/simulator/simulator.jsp"/>`

Para ver um exemplo, abra o `/apps/weretail/components/page/head.jsp` no CRXDE Lite.

### Registrar componentes da página para simulação {#registering-page-components-for-simulation}

Para permitir que o simulador de dispositivos suporte suas páginas, registre os componentes da página no serviço de fábrica MobileEmulatorProvider e defina o `mobile.resourceTypes` propriedade.

Ao trabalhar com AEM, existem vários métodos de gestão das definições de configuração para esses serviços; see [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos.

Por exemplo, para criar um ` [sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)` no seu aplicativo:

* Pasta pai: `/apps/application_name/config`
* Nome: `com.day.cq.wcm.mobile.core.impl.MobileEmulatorProvider-*alias*`

   O - `*alias*` O sufixo é necessário porque o serviço MobileEmulatorProvider é um serviço de fábrica. Use qualquer alias exclusivo para esta fábrica.

* jcr:primaryType: `sling:OsgiConfig`

Adicione a seguinte propriedade de nó:

* Nome: `mobile.resourceTypes`
* Tipo: `String[]`
* Valor: Os caminhos para os componentes da página que renderizam as páginas da Web. Por exemplo, o aplicativo geometrixx-media usa os seguintes valores:

   ```
   geometrixx-media/components/page
    geometrixx-unlimited/components/pages/page
    geometrixx-unlimited/components/pages/coverpage
    geometrixx-unlimited/components/pages/issue
   ```

### Especificação dos grupos de dispositivos {#specifying-the-device-groups}

Para especificar os grupos de dispositivos que aparecem na lista Dispositivos, adicione um `cq:deviceGroups` para a `jcr:content` nó da página raiz do site. O valor da propriedade é uma matriz de caminhos para os nós do grupo de dispositivos.

Os nós do grupo de dispositivos estão localizados na `/etc/mobile/groups` pasta.

Por exemplo, a página raiz do site Geometrixx Media é `/content/geometrixx-media`. O `/content/geometrixx-media/jcr:content` O nó inclui a seguinte propriedade:

* Nome: `cq:deviceGroups`
* Tipo: `String[]`
* Valor: `/etc/mobile/groups/responsive`

Use o console Ferramentas para [criar e editar grupos de dispositivos](/help/sites-developing/groupfilters.md).

>[!NOTE]
>
>Para grupos de dispositivos que você usa para design responsivo, edite o grupo de dispositivos e, na guia Geral , selecione Desativar emulador. Essa opção impede que o carrossel do emulador apareça, o que não é relevante para o design responsivo.

## Uso de imagens adaptáveis {#using-adaptive-images}

Você pode usar consultas de mídia para selecionar um recurso de imagem a ser exibido na página. No entanto, todos os recursos que usam um query de mídia para condicionar seu uso são baixados para o cliente. O query de mídia determina apenas se o recurso baixado é exibido.

Para recursos grandes, como imagens, baixar todos os recursos não é um uso eficiente do pipeline de dados do cliente. Para baixar seletivamente os recursos, use o javascript para iniciar a solicitação de recursos depois que as consultas de mídia executarem a seleção.

A estratégia a seguir carrega um único recurso escolhido por meio de consultas de mídia:

1. Adicione um elemento DIV para cada versão do recurso. Inclua o URI do recurso como o valor de um valor de atributo. O navegador não interpreta o atributo como um recurso.
1. Adicione uma consulta de mídia a cada elemento DIV apropriado para o recurso.
1. Quando o documento é carregado ou a janela é redimensionada, o código javascript testa a consulta de mídia de cada elemento DIV.
1. Com base nos resultados das consultas, determine qual recurso incluir.
1. Insira um elemento HTML no DOM que faça referência ao recurso.

### Avaliação de consultas de mídia usando Javascript {#evaluating-media-queries-using-javascript}

Implementação do [Interface MediaQueryList](https://dev.w3.org/csswg/cssom-view/#the-mediaquerylist-interface) que o W3C define permite avaliar consultas de mídia usando javascript. Você pode aplicar lógica aos resultados da consulta de mídia e executar scripts direcionados para a janela atual:

* Os navegadores que implementam a interface MediaQueryList são compatíveis com o `window.matchMedia()` . Essa função testa consultas de mídia em relação a uma determinada string. A função retorna um `MediaQueryList` que fornece acesso aos resultados da consulta.

* Em navegadores que não implementam a interface, você pode usar um `matchMedia()` polienchimento, como [matchMedia.js](https://github.com/paulirish/matchMedia.js), uma biblioteca javascript disponível gratuitamente.

#### Seleção de recursos específicos de mídia {#selecting-media-specific-resources}

O W3C proposto [elemento de imagem](https://picture.responsiveimages.org/) O usa consultas de mídia para determinar a fonte a ser usada para elementos de imagem. O elemento picture usa atributos de elemento para associar consultas de mídia a caminhos de imagem.

Disponível livremente [biblioteca picturefill.js](https://github.com/scottjehl/picturefill) O oferece funcionalidade semelhante à `picture` e usa uma estratégia semelhante. As chamadas da biblioteca picturefill.js `window.matchMedia` para avaliar as consultas de mídia definidas para um conjunto de `div` elementos. Cada `div` O elemento também especifica uma fonte de imagem. A fonte é usada quando a consulta de mídia do `div` retorno do elemento `true`.

O `picturefill.js` A biblioteca requer código HTML semelhante ao seguinte exemplo:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
</div>
```

Quando a página é renderizada, o picturefull.js insere um `img` elemento como o último filho do `<div data-picture>` elemento:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
    <img src="path to medium image">
</div>
```

Em uma página AEM, o valor da variável `data-src` é o caminho para um recurso no repositório.

### Implementação de imagens adaptáveis no AEM {#implementing-adaptive-images-in-aem}

Para implementar imagens adaptáveis no aplicativo AEM, é necessário adicionar as bibliotecas javascript necessárias e incluir a marcação de HTML necessária nas páginas.

**Bibliotecas**

Obtenha as seguintes bibliotecas javascript e inclua-as em uma pasta da biblioteca de clientes:

* [matchMedia.js](https://github.com/paulirish/matchMedia.js) (para navegadores que não implementam a interface MediaQueryList)
* [picturefill.js](https://github.com/scottjehl/picturefill)
* jquery.js (disponível por meio do `/etc/clientlibs/granite/jquery` pasta da biblioteca do cliente (categoria = jquery)
* [jquery.debouncedresize.js](https://github.com/louisremi/jquery-smartresize) (um evento jquery que ocorre uma vez depois que a janela é redimensionada)

**Dica:** Você pode concatenar automaticamente várias pastas da biblioteca do cliente ao [incorporação](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries).

**HTML**

Crie um componente que gera os elementos div necessários que o código picturefill.js espera. Em uma página AEM, o valor do atributo data-src é o caminho para um recurso no repositório. Por exemplo, um componente de página pode codificar as consultas de mídia e os caminhos associados para as representações de imagem no DAM. Ou crie um componente de Imagem personalizado que permite aos autores selecionar representações de imagem ou especificar opções de renderização de tempo de execução.

O exemplo a seguir HTML seleciona a partir de duas representações DAM da mesma imagem.

```xml
<div data-picture>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png'></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.319.319.png'    data-media="(min-width: 769px)"></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.140.100.png'   data-media="(min-width: 481px)"></div>
</div>
```

>[!NOTE]
>
>O componente fundamental da Imagem adaptativa implementa imagens adaptáveis:
>
>* Pasta da biblioteca do cliente: `/libs/foundation/components/adaptiveimage/clientlibs`
>* Script que gera o HTML: `/libs/foundation/components/adaptiveimage/adaptiveimage.jsp`
>
>A seção subsequente fornece detalhes sobre este componente.

### Como entender a renderização de imagem no AEM {#understanding-image-rendering-in-aem}

Para personalizar a renderização da imagem, você deve entender a implementação padrão AEM da renderização da imagem estática. AEM fornece o componente de Imagem e um servlet de renderização de imagem que trabalham juntos para renderizar imagens para a página da Web. A seguinte sequência de eventos ocorre quando o componente Imagem é incluído no sistema de parágrafo da página:

1. Criação: Os autores editam o componente Imagem para especificar o arquivo de imagem a ser incluído em uma página HTML. O caminho do arquivo é armazenado como um valor de propriedade do nó do componente Imagem .
1. Solicitação de página: O JSP do componente de página gera o código HTML. O JSP do componente de Imagem gera e adiciona um elemento img à página.
1. Solicitação de imagem: O navegador da Web carrega a página e solicita a imagem de acordo com o atributo src do elemento img.
1. Renderização da imagem: O servlet de renderização de imagem retorna a imagem para o navegador da Web.

![chlimage_1-6](assets/chlimage_1-6a.png)

Por exemplo, o JSP do componente de Imagem gera o seguinte elemento HTML:

`<img title="My Image" alt="My Image" class="cq-dd-image" src="/content/mywebsite/en/_jcr_content/par/image_0.img.jpg/1358372073597.jpg">`

Quando o navegador carrega a página, ele solicita a imagem usando o valor do atributo src como URL. O Sling decompõe o URL:

* Recurso: `/content/mywebsite/en/_jcr_content/par/image_0`
* Extensão do nome do arquivo: `.jpg`
* Seletor: `img`
* Sufixo: `1358372073597.jpg`

O `image_0` o nó tem um `jcr:resourceType` valor de `foundation/components/image`, que tem um `sling:resourceSuperType` valor de `foundation/components/parbase`. O componente parbase inclui o script img.GET.java que corresponde ao seletor e a extensão do nome do arquivo do URL da solicitação. O CQ usa esse script (servlet) para renderizar a imagem.

Para ver o código-fonte do script, use CRXDE Lite para abrir o `/libs/foundation/components/parbase/img.GET.java`
arquivo.

## Dimensionar imagens para o tamanho atual da janela de visualização {#scaling-images-for-the-current-viewport-size}

Dimensione imagens em tempo de execução de acordo com as características da janela de visualização do cliente para fornecer imagens que estejam em conformidade com os princípios do design responsivo. Use o mesmo padrão de design que a renderização de imagem estática, usando um servlet e um componente de criação.

O componente precisa executar as seguintes tarefas:

* Armazene o caminho e as dimensões desejadas do recurso de imagem como valores de propriedade.
* Gerar `div` elementos que contêm seletores de mídia e chamadas de serviço para renderizar a imagem.

>[!NOTE]
>
>O cliente da Web usa as bibliotecas javascript matchMedia e Picturefill (ou bibliotecas semelhantes) para avaliar os seletores de mídia.

O servlet que processa a solicitação de imagem precisa executar as seguintes tarefas:

* Recupere o caminho e as dimensões da imagem das propriedades do componente.
* Dimensione a imagem de acordo com as propriedades e retorne a imagem.

**Soluções disponíveis**

AEM instala as seguintes implementações que você pode usar ou estender.

* O componente básico da Imagem adaptativa que gera consultas de mídia e solicitações HTTP para o Servlet do componente de imagem adaptativa que dimensiona as imagens.
* O pacote Geometrixx Commons instala os servlets de amostra do Servlet de modificação de referência de imagem que alteram a resolução da imagem.

### Noções básicas sobre o componente da Imagem adaptativa {#understanding-the-adaptive-image-component}

O componente de Imagem adaptativa gera chamadas para o Servlet do componente de imagem adaptativa para renderizar uma imagem que é dimensionada de acordo com a tela do dispositivo. O componente inclui os seguintes recursos:

* JSP: Adiciona elementos div que associam consultas de mídia às chamadas para o Servlet do componente de imagem adaptativa.
* Bibliotecas do cliente: A pasta clientlibs é uma `cq:ClientLibraryFolder` que monta a biblioteca de javascript matchMedia polyfill e uma biblioteca de javascript modificada Picturefill.
* Caixa de diálogo Editar: O `cq:editConfig` O nó substitui o componente de imagem de base do CQ para que o destino de soltar crie um componente de imagem adaptável em vez de um componente de imagem de base.

#### Adicionar os elementos DIV {#adding-the-div-elements}

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

O `path` contém o caminho do recurso atual (o nó do componente de imagem adaptável). O código gera uma série de `div` elementos com a seguinte estrutura:

`<div data-scr = "*path-to-parent-node*.adaptive-image.adapt.*width*.*quality*.jpg" data-media="*media query*"></div>`

O valor da variável `data-scr` é um URL que o Sling resolve para o Servlet do Componente de Imagem Adaptativa que renderiza a imagem. O atributo data-media contém a consulta de mídia que é avaliada em relação às propriedades do cliente.

O código de HTML a seguir é um exemplo de `div` elementos gerados pelo JSP:

```xml
<div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.low.jpg'></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.medium.jpg'    data-media="(min-width: 320px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.480.medium.jpg'    data-media="(min-width: 321px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.476.high.jpg'     data-media="(min-width: 481px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.620.high.jpg'     data-media="(min-width: 769px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.full.high.jpg'     data-media="(min-width: 1025px)"></div>
```

#### Alteração dos seletores de tamanho de imagem {#changing-the-image-size-selectors}

Se você personalizar o componente Imagem adaptativa e alterar os seletores de largura, também deverá configurar o Servlet do componente de imagem adaptativa para suportar as larguras.

### Noções básicas sobre o servlet do componente de imagem adaptativa {#understanding-the-adaptive-image-component-servlet}

O Servlet do componente de imagem adaptativa redimensiona uma imagem JPEG de acordo com uma largura especificada e define a qualidade do JPEG.

#### A interface do Servlet do componente de imagem adaptativa {#the-interface-of-the-adaptive-image-component-servlet}

O Servlet do Componente de Imagem Adaptativa é vinculado ao servlet Sling padrão e oferece suporte às extensões de arquivo .jpg, .jpeg, .gif e .png . O seletor de servlet é img.

>[!CAUTION]
>
>Arquivos .gif animados não são suportados no AEM para renderizações adaptativas.

Portanto, o Sling resolve URLs de solicitação HTTP do seguinte formato para este servlet:

`*path-to-node*.img.*extension*`

Por exemplo, o Sling encaminha solicitações HTTP com o URL `http://localhost:4502/content/geometrixx/adaptiveImage.img.jpg` para Servlet do componente de imagem adaptativa.

Dois seletores adicionais especificam a largura da imagem solicitada e a qualidade da JPEG. O exemplo a seguir solicita uma imagem de largura de 480 pixels e qualidade média:

`http://localhost:4502/content/geometrixx/adaptiveImage.adapt.480.MEDIUM.jpg`

**Propriedades de imagens suportadas**

O servlet aceita um número finito de larguras e qualidades de imagem. As seguintes larguras são suportadas por padrão (em pixels):

* completo
* 320
* 480
* 476
* 620

O valor completo indica que não há escala.

Os seguintes valores para qualidade de JPEG são suportados:

* BAIXO
* MÉDIO
* ALTO

Os valores numéricos são 0,4, 0,82 e 1,0, respectivamente.

**Alteração das larguras padrão suportadas**

Use o Console da Web ([http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)) ou um nó sling:OsgiConfig para configurar as larguras suportadas do Servlet do Componente de Imagem Adaptativa do Adobe CQ.

Para obter informações sobre como configurar AEM serviços, consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md).

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
   <td>com.day.cq.wcm.foundation.impl. AdaptiveImageComponentServlet</td>
  </tr>
  <tr>
   <th>Propriedade</th>
   <td><p>Larguras suportadas</p>
    <ul>
     <li>Para adicionar uma largura compatível, clique em um botão + e insira um número inteiro positivo.</li>
     <li>Para remover uma largura compatível, clique no botão - associado.</li>
     <li>Para modificar uma largura compatível, edite o valor do campo.</li>
    </ul> </td>
   <td><p>adapt.supported.widths</p>
    <ul>
     <li>A propriedade é um valor de String com vários valores.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### Detalhes da implementação {#implementation-details}

O `com.day.cq.wcm.foundation.impl.AdaptiveImageComponentServlet` estende a [AbstractImageServlet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) classe . O código-fonte AdaptiveImageComponentServlet está localizado no `/libs/foundation/src/impl/src/com/day/cq/wcm/foundation/impl` pasta.

A classe usa anotações Felix SCR para configurar o tipo de recurso e a extensão de arquivo à qual o servlet está associado e o nome do primeiro seletor.

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

O servlet usa a anotação SCR de propriedade para definir a qualidade e as dimensões padrão da imagem suportada.

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

O `AbstractImageServlet` A classe fornece `doGet` que processa a solicitação HTTP. Esse método determina o recurso associado à solicitação, recupera as propriedades do recurso do repositório e as retorna em um [ImageContext](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) objeto.

>[!NOTE]
>
>O [com.day.cq.commons.DownloadResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/DownloadResource.html) A classe fornece `getFileReference method`, que recupera o valor do recurso `fileReference` propriedade.

O `AdaptiveImageComponentServlet` substitui a `createLayer` método . O método obtém o caminho do recurso de imagem e a largura da imagem solicitada do `ImageContext` objeto. Em seguida, chama os métodos do `info.geometrixx.commons.impl.AdaptiveImageHelper` classe , que executa a escala de imagem real.

A classe AdaptiveImageComponentServlet também substitui o método writeLayer. Esse método aplica a qualidade do JPEG à imagem.

### Servlet de modificação de referência de imagem (Geometrixx Comum) {#image-reference-modification-servlet-geometrixx-common}

O exemplo de Servlet de modificação de referência de imagem gera atributos de tamanho para o elemento img dimensionar uma imagem na página da Web.

#### Chamar o servlet {#calling-the-servlet}

O servlet está vinculado a `cq:page` e suporta a extensão de arquivo .jpg . O seletor de servlet é `image`. Portanto, o Sling resolve URLs de solicitação HTTP do seguinte formato para este servlet:

`path-to-page-node.image.jpg`

Por exemplo, o Sling encaminha solicitações HTTP com o URL `http://localhost:4502/content/geometrixx/en.image.jpg` ao Servlet de modificação de referência de imagem.

Três seletores adicionais especificam a largura, a altura e a qualidade (opcionalmente) da imagem solicitada. O exemplo a seguir solicita uma imagem de 770 pixels de largura, altura 360 pixels e de qualidade média.

`http://localhost:4502/content/geometrixx/en.image.770.360.MEDIUM.jpg`

**Propriedades de imagens suportadas**

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

Os seguintes valores para qualidade de imagem são suportados:

* low
* médio
* alto

Ao trabalhar com AEM, existem vários métodos de gestão das definições de configuração para esses serviços; see [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos.

#### Especificação do recurso de imagem {#specifying-the-image-resource}

O caminho da imagem, as dimensões e os valores de qualidade devem ser armazenados como propriedades de um nó no repositório:

* O nome do nó é `image`.
* O nó pai é o `jcr:content` nó de um `cq:page` recurso.

* O caminho da imagem é armazenado como o valor de uma propriedade chamada `fileReference`.

Ao criar uma página, use **Sidekick** para especificar a imagem e adicionar o `image` às propriedades da página:

1. Em **Sidekick**, clique no botão **Página** e clique em **Propriedades da página**.
1. Clique no botão **Imagem** e especifique a imagem.
1. Clique em **OK**.

#### Detalhes da implementação {#implementation-details-1}

A classe info.geometrixx.commons.impl.servlets.ImageReferenceModificationServlet estende o [AbstractImageServlet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) classe . Se o pacote cq-geometrixx-commons-pkg estiver instalado, o código-fonte ImageReferenceModificationServlet estará localizado na seção `/apps/geometrixx-commons/src/core/src/main/java/info/geometrixx/commons/impl/servlets` pasta.

A classe usa anotações Felix SCR para configurar o tipo de recurso e a extensão de arquivo à qual o servlet está associado e o nome do primeiro seletor.

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

O servlet usa a anotação SCR de propriedade para definir a qualidade e as dimensões padrão da imagem suportada.

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

O `AbstractImageServlet` A classe fornece `doGet` que processa a solicitação HTTP. Esse método determina o recurso associado à chamada, recupera as propriedades do recurso do repositório e as salva em um [ImageContext](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) objeto.

O `ImageReferenceModificationServlet` substitui a `createLayer` e implementa a lógica que determina o recurso de imagem a ser renderizado. O método recupera um nó filho do `jcr:content` nome do nó `image`. Um [Imagem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/Image.html) é criado a partir desta `image` e o `getFileReference` retorna o caminho para o arquivo de imagem do `fileReference` propriedade do nó da imagem.

>[!NOTE]
>O [com.day.cq.commons.DownloadResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/DownloadResource.html) A classe fornece o método getFileReferencemod.

## Desenvolvimento de uma grade de fluidos {#developing-a-fluid-grid}

AEM permite implementar grades fluidas de maneira eficiente e eficaz. Esta página explica como você pode integrar sua grade fluida ou uma implementação de grade existente (como [Bootstrap](https://twitter.github.com/bootstrap/)) no aplicativo AEM.

Se você não estiver familiarizado com grades de fluidos, consulte o [Introdução às grades fluídas](/help/sites-developing/responsive.md#developing-a-fluid-grid) na parte inferior desta página. Essa introdução fornece uma visão geral das grades de fluidos e orientação para projetá-las.

### Definição da grade usando um componente Página {#defining-the-grid-using-a-page-component}

Use componentes de página para gerar os elementos de HTML que definem os blocos de conteúdo da página. A ClientLibraryFolder à qual a página faz referência fornece o CSS que controla o layout dos blocos de conteúdo:

* Componente de página: Adiciona elementos div que representam linhas de blocos de conteúdo. Os elementos div que representam os blocos de conteúdo incluem um componente parsys, onde os autores adicionam conteúdo.
* Pasta da biblioteca do cliente: Fornece o arquivo CSS que inclui consultas de mídia e estilos para os elementos div.

Por exemplo, o aplicativo geometrixx-media de amostra contém o componente media-home . Esse componente de página insere dois scripts, que geram dois `div` elementos da classe `row-fluid`:

* A primeira linha contém um `div` elemento da classe `span12` (o conteúdo abrange 12 colunas). O `div` contém o componente parsys.

* A segunda linha contém dois `div` elementos, um da classe `span8` e o outro da classe `span4`. Cada `div` inclui o componente parsys.

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
>Quando um componente inclui vários `cq:include` elementos que fazem referência ao componente parsys, cada `path` deve ter um valor diferente.

#### Dimensionar a grade do componente Página {#scaling-the-page-component-grid}

O design associado ao componente página geometrixx-media (`/etc/designs/geometrixx-media`) contém a variável `clientlibs` ClientLibraryFolder. Esta ClientLibraryFolder define estilos CSS para `row-fluid` classes, `span*` classes e `span*` classes que são filhos de `row-fluid` classes. Consultas de mídia permitem a redefinição de estilos para diferentes tamanhos de visor.

O exemplo de CSS a seguir é um subconjunto desses estilos. Esse subconjunto se concentra em `span12`, `span8`e `span4` classes e consultas de mídia para dois tamanhos de visor. Observe as seguintes características do CSS:

* O `.span` os estilos definem as larguras do elemento usando números absolutos.
* O `.row-fluid .span*` os estilos definem a largura do elemento como porcentagens do pai. As porcentagens são calculadas a partir das larguras absolutas.
* Consultas de mídia para visores maiores atribuem larguras absolutas maiores.

>[!NOTE]
>
>A amostra Geometrixx Media integra o [Bootstrap](https://twitter.github.com/bootstrap/javascript.html) estrutura javascript em sua implementação de grade fluida. A estrutura do Bootstrap fornece o arquivo bootstrap.css.

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

As páginas do aplicativo Geometrixx Media de amostra distribuem linhas de blocos de conteúdo horizontalmente em visores amplos. Em janelas de visualização menores, os mesmos blocos são distribuídos verticalmente. O exemplo de CSS a seguir mostra os estilos que implementam esse comportamento no código de HTML gerado pelo componente de página de mídia-página inicial:

* O CSS padrão para a página de boas-vindas da mídia atribui a variável `float:left` estilo para `span*` classes que estão dentro `row-fluid` classes.

* Consultas de mídia para visualizações menores atribuem a variável `float:none` estilo para as mesmas classes.

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

#### Modularizar os componentes da página {#tip-modularize-your-page-components}

Modularize seus componentes para fazer uso eficiente do código. Seu site provavelmente usa vários tipos diferentes de páginas, como uma página de boas-vindas, uma página de artigo ou uma página de produto. Cada tipo de página contém tipos diferentes de conteúdo e provavelmente usa layouts diferentes. No entanto, quando certos elementos de cada layout são comuns em várias páginas, é possível reutilizar o código que implementa essa parte do layout.

**Usar as sobreposições de componentes da página**

Crie um componente de página principal que forneça scripts para gerar as várias partes de uma página, como `head` e `body` seções e `header`, `content`e `footer` seções dentro do corpo.

Crie outros componentes de página que usam o componente de página principal como `cq:resourceSuperType`. Esses componentes incluem scripts que substituem os scripts da página principal, conforme necessário.

Por exemplo, o aplicativo goemetrixx-media inclui o componente página (a variável `sling:resourceSuperType` é o componente de página de base). Vários componentes filho (como artigo, categoria e media-home) usam esse componente de página como `sling:resourceSuperType`. Cada componente filho inclui um arquivo content.jsp que substitui o arquivo content.jsp do componente página.

**Reutilizar scripts**

Crie vários scripts JSP que geram combinações de linha e coluna comuns para vários componentes de página. Por exemplo, a variável `content.jsp` o script dos componentes do artigo e do media-home fazem referência à variável `8x4col.jsp` script.

**Organizar estilos de CSS por tamanho de visor direcionado**

Inclua estilos CSS e consultas de mídia para diferentes tamanhos de visor em arquivos separados. Use as pastas da biblioteca do cliente para concatená-las.

### Inserção de componentes na grade da página {#inserting-components-into-the-page-grid}

Quando os componentes geram um único bloco de conteúdo, geralmente a grade que o componente da página estabelece controla a posição do conteúdo.

Os autores devem estar cientes de que o bloco de conteúdo pode ser renderizado em vários tamanhos e posições relativas. O texto do conteúdo não deve usar direções relativas para se referir a outros blocos de conteúdo.

Se necessário, o componente deve fornecer qualquer biblioteca de CSS ou javascript necessária para o código HTML gerado. Use uma pasta da biblioteca do cliente dentro do componente para gerar os arquivos CSS e JS. Para expor os arquivos, [criar uma dependência ou incorporar a biblioteca](/help/sites-developing/clientlibs.md#creating-client-library-folders) em outra pasta da biblioteca do cliente abaixo da pasta /etc.

**Sub-grades**

Se o componente contiver vários blocos de conteúdo, adicione os blocos de conteúdo dentro de uma linha para estabelecer uma subgrade na página:

* Use os mesmos nomes de classe do componente de página contêiner para expressar elementos div como linhas e blocos de conteúdo.
* Para substituir o comportamento que o CSS do design da página implementa, use um nome de segunda classe para o elemento div da linha e forneça o CSS associado em uma pasta da biblioteca do cliente.

Por exemplo, a variável `/apps/geometrixx-media/components/2-col-article-summary` O componente gera duas colunas de conteúdo. O HTML gerado tem a seguinte estrutura:

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

O `.row-fluid .span6` os seletores do CSS da página se aplicam à variável `div` elementos da mesma classe e estrutura neste HTML. No entanto, o componente também inclui a pasta da biblioteca do cliente /apps/geometrixx-media/components/2-col-article-summary/clientlibs:

* O CSS usa as mesmas consultas de mídia que o componente página para estabelecer alterações no layout nas mesmas larguras de página discretas.
* Os seletores usam o `multi-col-article-summary` classe da linha `div` para substituir o comportamento do `row-fluid` classe .

Por exemplo, os seguintes estilos estão incluídos na variável `/apps/geometrixx-media/components/2-col-article-summary/clientlibs/css/responsive-480px.css` arquivo:

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

## Introdução às grades de fluidos {#introduction-to-fluid-grids}

As grades de fluxo permitem que os layouts de página se adaptem às dimensões do visor do cliente. As grades consistem em colunas lógicas e linhas que posicionam os blocos de conteúdo na página.

* As colunas determinam as posições e larguras horizontais dos blocos de conteúdo.
* As linhas determinam as posições verticais relativas dos blocos de conteúdo.

Com a tecnologia HTML5, você pode implementar a grade e manipulá-la para adaptar layouts de página a diferentes tamanhos de visor:

* HTML `div` Os elementos contêm blocos de conteúdo que abrangem um determinado número de colunas.
* Um ou mais desses elementos div compõem uma linha quando compartilham um elemento pai comum.

### Uso de larguras discretas {#using-discrete-widths}

Para cada faixa de larguras de visor que você está direcionando, use uma largura de página estática e blocos de conteúdo de largura constante. Ao redimensionar manualmente uma janela do navegador, as alterações no tamanho do conteúdo ocorrem em larguras de janela discretas (também conhecidas como pontos de interrupção). Consequentemente, os designs de página são mais seguidos, maximizando a experiência do usuário.

#### Dimensionamento da grade {#scaling-the-grid}

Use grades para dimensionar blocos de conteúdo para adaptar-se a diferentes tamanhos de visor. Os blocos de conteúdo abrangem um número específico de colunas. À medida que as larguras de coluna aumentam ou diminuem para se ajustarem a diferentes tamanhos de visor, a largura dos blocos de conteúdo aumenta ou diminui de acordo. O dimensionamento pode suportar visores de grande e médio porte que são amplos o suficiente para acomodar o posicionamento lado a lado dos blocos de conteúdo.

![](do-not-localize/chlimage_1-1a.png)

#### Reposicionamento de conteúdo na grade {#repositioning-content-in-the-grid}

O tamanho dos blocos de conteúdo pode ser restrito por uma largura mínima, além da qual a escala não é mais eficaz. Para visores menores, a grade pode ser usada para distribuir verticalmente blocos de conteúdo em vez de horizontalmente.

![](do-not-localize/chlimage_1-2a.png)

### Criação da grade {#designing-the-grid}

Determine as colunas e linhas necessárias para posicionar os blocos de conteúdo nas páginas. Os layouts de página determinam o número de colunas e linhas que abrangem a grade.

**Número de colunas**

Inclua colunas suficientes para posicionar horizontalmente os blocos de conteúdo em todos os layouts, para todos os tamanhos das janelas de visualização. Você deve usar mais colunas do que o necessário para acomodar designs de página futuros.

**Conteúdo da linha**

Use linhas para controlar o posicionamento vertical dos blocos de conteúdo. Determine os blocos de conteúdo que compartilham a mesma linha:

* Os blocos de conteúdo que estão localizados próximos um do outro horizontalmente em qualquer um dos layouts estão na mesma linha.
* Os blocos de conteúdo que estão localizados próximos um do outro horizontalmente (visores mais largos) e verticalmente (visores menores) estão na mesma linha.

### Implementações de grade {#grid-implementations}

Crie classes e estilos de CSS para controlar o layout dos blocos de conteúdo em uma página. Os designs de página geralmente se baseiam no tamanho e na posição relativa dos blocos de conteúdo no visor. A janela de visualização determina o tamanho real dos blocos de conteúdo. Seu CSS precisa levar em conta os tamanhos relativo e absoluto. Você pode implementar uma grade fluida usando três tipos de classes CSS:

* Uma classe para um `div` elemento que é um contêiner para todas as linhas. Essa classe define a largura absoluta da grade.
* Uma classe para `div` elementos que representam uma linha. Essa classe controla o posicionamento horizontal ou vertical dos blocos de conteúdo que ela contém.
* Classes para `div` elementos que representam blocos de conteúdo de diferentes larguras. As larguras são expressas como uma porcentagem do pai (a linha).

As larguras do visor direcionadas (e as consultas de mídia associadas) demarcam as larguras discretas usadas para um layout de página.

#### Larguras dos blocos de conteúdo {#widths-of-content-blocks}

Geralmente, a variável `width` o estilo das classes de bloco de conteúdo é baseado nas seguintes características da página e da grade:

* A largura absoluta da página que você está usando para cada tamanho de visor direcionado. Esses são valores conhecidos.
* A largura absoluta das colunas de grade para cada largura de página. Esses valores são determinados.
* A largura relativa de cada coluna como uma porcentagem da largura total da página. Esses valores são calculados.

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

Use o seguinte algoritmo como ponto de partida para desenvolver as classes de elementos e os estilos de CSS para suas páginas.

1. Defina um nome de classe para o elemento div que contenha todas as linhas, por exemplo `content.`
1. Defina uma classe CSS para elementos div que representem linhas, como `row-fluid`.
1. Defina nomes de classe para elementos de bloco de conteúdo. Uma classe é necessária para todas as larguras possíveis, em termos de extensões de coluna. Por exemplo, use a variável `span3` classe para `div` elementos que abrangem 3 colunas, use `span4` classes para extensões de 4 colunas. Defina quantas classes houver colunas em sua grade.

1. Para cada tamanho do visor que você está direcionando, adicione a consulta de mídia correspondente ao arquivo CSS. Adicione os seguintes itens em cada query de mídia:

   * Um seletor para a `content` classe , por exemplo `.content{}`.
   * Seletores para cada classe de span, por exemplo `.span3{ }`.
   * Um seletor para a `row-fluid` classe , por exemplo `.row-fluid{ }`
   * Seletores para classes de span que estão dentro de classes de fluido de linha, por exemplo `.row-fluid span3 { }`.

1. Adicionar estilos de largura para cada seletor:

   1. Defina a largura de `content` seletores para o tamanho absoluto da página, por exemplo `width:480px`.
   1. Defina a largura de todos os seletores de fluido de linha como 100%.
   1. Defina a largura de todos os seletores de span para a largura absoluta do bloco de conteúdo. Uma grade trivial usa colunas uniformemente distribuídas da mesma largura: `(absolute width of page)/(number of columns)`.
   1. Defina a largura da variável `.row-fluid .span` seletores como uma porcentagem da largura total. Calcule essa largura usando o `(absolute span width)/(absolute page width)*100` fórmula.

#### Posicionamento de blocos de conteúdo em linhas {#positioning-content-blocks-in-rows}

Use o estilo flutuante do `.row-fluid` classe para controlar se os blocos de conteúdo em uma linha são organizados horizontal ou verticalmente.

* O `float:left` ou `float:right` style causa a distribuição horizontal de elementos secundários (blocos de conteúdo).

* O `float:none` O estilo causa a distribuição vertical de elementos filho.

Adicione o estilo ao `.row-fluid` em cada consulta de mídia. Defina o valor de acordo com o layout da página que você está usando para esse query de mídia. Por exemplo, o diagrama a seguir ilustra uma linha que distribui o conteúdo horizontalmente para janelas largas e verticalmente para janelas de visualização estreitas.

![](do-not-localize/chlimage_1-3a.png)

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

Para o layout de página de cada tamanho de visor que está direcionando, determine o número de colunas que cada bloco de conteúdo expande. Em seguida, determine qual classe usar para os elementos div desses blocos de conteúdo.

Ao estabelecer as classes div, você pode implementar a grade usando seu aplicativo AEM.
