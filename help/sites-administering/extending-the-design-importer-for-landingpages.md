---
title: Extensão e configuração do Importador de design para páginas de aterrissagem
seo-title: Extending and Configuring the Design Importer for Landing Pages
description: Saiba como configurar o Importador de design para páginas de aterrissagem.
seo-description: Learn how to configure the Design Importer for landing pages.
uuid: a2dd0c30-03e4-4e52-ba01-6b0b306c90fc
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e02f5484-fbc2-40dc-8d06-ddb53fd9afc2
docset: aem65
exl-id: 1b8c6075-13c6-4277-b726-8dea7991efec
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '3503'
ht-degree: 5%

---

# Extensão e configuração do Importador de design para páginas de aterrissagem{#extending-and-configuring-the-design-importer-for-landing-pages}

Esta seção descreve como configurar e, se desejado, estender o importador de design para páginas de aterrissagem. O trabalho com páginas de aterrissagem após a importação é abordado em [Páginas de aterrissagem.](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**Fazer com que o importador de design extraia seu componente personalizado**

Estas são as etapas lógicas para fazer com que o importador de design reconheça seu componente personalizado

1. Criar um TagHandler

   * Um manipulador de tags é um POJO que manipula tags HTML de um tipo específico. O &quot;tipo&quot; de tags de HTML que seu TagHandler pode manipular é definido por meio da propriedade OSGi de TagHandlerFactory &quot;tagpattern.name&quot;. Essa propriedade OSGi é essencialmente um regex que deve corresponder à tag html de entrada que você deseja manipular. Todas as tags aninhadas seriam jogadas no manipulador de tags para manipulação. Por exemplo, se você se registrar em um div que contém um &lt;p> , a variável &lt;p> A tag também seria lançada ao TagHandler e depende de você como deseja cuidar dela.
   * A interface do manipulador de tags é semelhante a uma interface do manipulador de conteúdo SAX. Ele recebe eventos SAX para cada tag html. Como provedor do manipulador de tags, é necessário implementar determinados métodos do ciclo de vida que são automaticamente chamados pela estrutura do importador de design.

1. Crie o TagHandlerFactory correspondente.

   * A fábrica do manipulador de tags é um componente OSGi (singleton) responsável pela geração de instâncias do manipulador de tags.
   * a fábrica do manipulador de tags deve expor uma propriedade OSGi chamada &quot;tagpattern.name&quot; cujo valor é comparado à tag html de entrada.
   * Se houver vários manipuladores de tags correspondentes à tag html de entrada, aquele com uma classificação mais alta será escolhido. A própria classificação é exposta como uma propriedade OSGi **service.ranking**.
   * O TagHandlerFactory é um componente OSGi. Todas as referências que você deseja fornecer ao TagHandler devem ser feitas por meio desta fábrica.

1. Certifique-se de que seu TagHandlerFactory tenha uma classificação melhor se desejar substituir o padrão.

>[!CAUTION]
>
>O Importador de Design, usado para importar páginas de aterrissagem, [ foi descontinuado com o AEM 6.5](/help/release-notes/deprecated-removed-features.md#deprecated-features).

## Preparação do HTML para importação {#preparing-the-html-for-import}

Após criar uma página de importador, você pode importar sua página de aterrissagem de HTML completo. Para importar a página de aterrissagem do HTML, primeiro compacte o conteúdo em um pacote de design. O pacote de design contém a página de aterrissagem do HTML junto com os ativos referenciados (imagens, css, ícones, scripts e assim por diante).

O gabarito a seguir fornece uma amostra de como preparar o HTML para importação:

Folha de características da página de aterrissagem

[Obter arquivo](assets/cheatsheet.zip)

### Layout e requisitos do arquivo zip {#zip-file-layout-and-requirements}

>[!NOTE]
>
>Nesse ponto, os arquivos ZIP podem conter apenas uma HTML page ou uma parte de uma página.

Um exemplo de layout do zip é o seguinte:

* /index.html -> arquivo de HTML de página de aterrissagem
* /css -> para adicionar à clientlib CSS
* /img -> todas as imagens e ativos
* /js -> para adicionar à clientlib JS

O layout é baseado no layout de práticas recomendadas do HTML5 Boilerplate. Leia mais em [https://html5boilerplate.com/](https://html5boilerplate.com/)

>[!NOTE]
>
>No mínimo, o pacote de design **must** contém um **index.html** no nível da raiz. Caso a landing page a ser importada também tenha uma versão móvel, o zip deverá conter uma **mobile.index.html** juntamente com **index.html** no nível da raiz.

### Preparação do HTML de página de aterrissagem {#preparing-the-landing-page-html}

Para importar o HTML, é necessário adicionar um div de tela ao HTML de página de aterrissagem.

O div da tela é um html **div** com `id="cqcanvas"` que deve ser inserido no HTML `<body>` e devem envolver o conteúdo destinado à conversão.

Um trecho de amostra do HTML da página de aterrissagem após a adição do div da tela é o seguinte:

```xml
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title></title>
  <meta name="description" content="">
</head>
<body>
 <div id="cqcanvas">
  <!-- HTML content intended for conversion -->
 </div>
</body>
</html>
```

### Preparação do HTML para incluir componentes AEM editáveis {#preparing-the-html-to-include-editable-aem-components}

Ao importar uma landing page, você tem a opção de importar a página como está, o que significa que depois que a landing page é importada, não é possível editar nenhum dos itens importados no AEM (ainda é possível adicionar mais componentes AEM na página).

Antes de importar a landing page, convém converter algumas partes da landing page para que elas possam ser editadas AEM componentes. Isso permite que você edite rapidamente partes da página de aterrissagem, mesmo depois que o design da página de aterrissagem tenha sido importado.

Para fazer isso, adicione a variável `data-cq-component` para o componente adequado no arquivo HTML que você importa.

A seção a seguir descreve como editar seu arquivo HTML para que você converta determinadas partes de suas páginas de aterrissagem em diferentes componentes AEM editáveis. Os componentes são descritos detalhadamente em [Componentes de páginas de aterrissagem](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md).

>[!NOTE]
>
>A marcação de HTML para converter partes da landing page em componentes AEM tem uma declaração de tag longa e curta. Ambos estão descritos para cada componente.

### Limitações {#limitations}

Antes de importar, observe as seguintes limitações:

### Qualquer atributo como classe ou id aplicado na tag &amp;lt;body> não é preservado {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

Se qualquer atributo como id ou classe for aplicado na tag do corpo, por exemplo `<body id="container">` então, não é preservado após a importação. Portanto, o design que está sendo importado não deve ter dependências nos atributos aplicados na variável `<body>` .

### Arrastar e soltar zip {#drag-and-drop-zip}

O carregamento de zip de arrastar/soltar não é compatível com o Internet Explorer e o Firefox versões 3.6 e anteriores. Para fazer upload de um design ao usar esses navegadores, clique na área de arquivo para abrir uma caixa de diálogo de upload de arquivo e fazer upload do design usando essa caixa de diálogo.

Os navegadores que suportam &quot;arrastar e soltar&quot; do zip de design são Chrome, Safari5.x, Firefox 4 e superior.

### Não há suporte para o Modernizador {#modernizr-is-not-supported}

`Modernizr.js` é uma ferramenta baseada em javascript que detecta recursos nativos de navegadores e detecta se são adequados para elementos html5 ou não. Os designs que usam o Modernizer para aprimorar o suporte em versões mais antigas de navegadores diferentes podem causar problemas de importação na solução de página de aterrissagem. `Modernizr.js` os scripts não são compatíveis com o Importador de design.

### As propriedades da página não são preservadas no momento da importação do pacote de design {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

Qualquer propriedade de página (por exemplo, Domínio personalizado, imposição de HTTPS etc.) definido para uma página (que usa o modelo de Página de aterrissagem em branco) antes de importar o pacote de design são perdidos depois que o design é importado. Portanto, a prática recomendada é definir as propriedades da página após a importação do pacote de design.

### Marcação somente HTML assumida {#html-only-markup-assumed}

Ao importar, a marcação analisada por motivos de segurança e para evitar a importação e publicação de uma marcação inválida. Isso pressupõe que a marcação somente de HTML e outras formas de elementos, como componentes incorporados SVG ou da Web serão filtrados.

### Texto {#text}

Marcação de HTML para inserir um componente de texto ( `foundation/components/text`) na HTML dentro do pacote de design:

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

A inclusão da marcação acima no HTML faz o seguinte:

* Cria um componente de texto AEM editável ( `sling:resourceType=foundation/components/text`) na landing page criada após a importação do pacote de design.
* Define a variável `text` propriedade do componente de texto criado para a HTML incluída no `div`.

**Declaração de tag do componente abreviado**:

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**Texto com uma lista**

Para adicionar um texto com uma lista:

* 1st
* 2nd

que pode ser editado no editor de RTE:

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**Texto com cor**

Para adicionar um texto com cor (rosa) que pode ser editada no editor de RTE:

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### Título {#title}

Marcação de HTML para inserir um componente de título ( `wcm/landingpage/components/title`) na HTML dentro do pacote de design:

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

A inclusão da marcação acima no HTML faz o seguinte:

* Cria um componente de título de AEM editável ( `sling:resourceType=wcm/landingpage/components/title`) na landing page criada após a importação do pacote de design.
* Define a variável `jcr:title` propriedade do componente de título criado no texto dentro da tag de cabeçalho encapsulada em div.
* Define a variável `type` propriedade da tag de cabeçalho, neste caso `h1`.

O componente de título suporta 7 tipos - `h1, h2, h3, h4, h5, h6` e `default`.

**Declaração de tag do componente abreviado**:

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### Imagem {#image}

Marcação de HTML para inserir um componente de imagem (foundation/components/image) na HTML dentro do pacote de design:

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

A inclusão da marcação acima no HTML faz o seguinte:

* Cria um componente de imagem AEM editável ( `sling:resourceType=foundation/components/image`) na landing page criada após a importação do pacote de design.
* Define a variável `fileReference` propriedade do componente de imagem criado para o caminho para o qual a imagem especificada no atributo src é importada.
* Define a variável `alt` propriedade para o valor do atributo alt na tag img.
* Define a variável `title` propriedade para o valor do atributo title na tag img.
* Define a variável `width` propriedade para o valor do atributo width na tag img.
* Define a variável `height` propriedade para o valor do atributo height na tag img .

**Declaração de tag do componente de abreviação:**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### URL absoluto img src não compatível com o componente de imagem Div {#absolute-url-img-src-not-supported-within-image-component-div}

Se uma `<img>` uma tag com um url absoluto src é tentada para a conversão do componente, uma **UnsupportedTagContentException** é levantada. Por exemplo, o seguinte não é compatível:

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

Caso contrário, imagens de URL absolutas são compatíveis com tags img que não fazem parte de div do Componente de imagem.

### Componentes de chamada para ação {#call-to-action-components}

Você pode marcar parte da landing page para importação como um &quot;componente de ação Chamada editável&quot; - esses componentes de chamada para ação importados podem ser editados após a importação da landing page. AEM inclui os seguintes componentes de CTA:

* Link de clickthrough - permite adicionar um link de texto que, quando clicado, direciona o visitante a um URL.
* Link gráfico - permite adicionar uma imagem que, quando clicada, leva o visitante para um URL de destino.

#### Link de clickthrough {#click-through-link}

Este componente de CTA pode ser usado para adicionar um link de texto na página de aterrissagem.

Propriedades compatíveis

* Rótulo, com negrito, itálico e opções de sublinhado
* URL do Target, suporta url de terceiros e AEM
* Opções de renderização de página (mesma janela, nova janela etc.)

Tag HTML para incluir o componente click through no zip importado. Aqui, o href mapeia para o url do target, &quot;Exibir detalhes do produto&quot; mapeia para o rótulo e assim por diante.

```xml
<div id="cqcanvas">
.
.
                <div data-cq-component="clickThroughLink">
        <a href="/content/we-retail/us/en/products/equipment/snow-sports/flying-snowboard.html">View Product Details  ></a>
  </div>
.
.
</div>
```

Esse componente pode ser usado em qualquer aplicativo independente ou pode ser importado do zip.

**Declaração de tag do componente abreviado**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### Link gráfico {#graphical-link}

Esse componente de CTA pode ser usado para adicionar qualquer imagem gráfica com um link à página de aterrissagem. A imagem pode ser um simples botão ou qualquer imagem gráfica como fundo. Quando a imagem é clicada, o usuário é direcionado ao URL de destino especificado nas propriedades do componente. Ele faz parte do grupo “Frases de chamariz”.

Propriedades compatíveis

* Corte de imagem, rotação
* Texto ao passar o mouse, descrição, tamanho em px
* URL do Target, suporta url de terceiros e AEM
* Opções de renderização de página (mesma janela, nova janela etc.)

tag HTML para incluir o componente de link gráfico no zip importado. Aqui, a href será mapeada para o url de destino, a img src será a imagem de renderização, o &quot;título&quot; será tomado como texto de focalização e assim por diante.

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**Declaração de tag do componente abreviado**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>Para criar um link gráfico de click-throughs, é necessário vincular uma tag de âncora e a tag de imagem dentro de uma div com `data-cq-component="clickthroughgraphicallink"` atributo.
>
>Por exemplo: `<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>Outras maneiras de associar uma imagem a uma tag de âncora usando CSS não são compatíveis, por exemplo, a marcação a seguir não funcionará:
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>com um `css .hasbackground { background-image: pathtoimage }`

### Formulário de lead {#lead-form}

Um formulário de lead é um formulário usado para coletar informações de perfil de um visitante/lead. Essas informações podem ser armazenadas e usadas posteriormente como base para realizar um marketing eficiente. Essas informações geralmente incluem título, nome, email, data de nascimento, endereço, interesse e assim por diante. Faz parte do grupo &quot;Formulário de lead para CTA&quot;.

**Recursos compatíveis**

* Campos de lead predefinidos - nome, sobrenome, endereço, dob, gênero, sobre, userId, emailId, botão Enviar estão disponíveis no sidekick. Basta arrastar/soltar o componente necessário no formulário de lead.
* Com a ajuda desses componentes, o autor pode criar um formulário de lead independente, esses campos correspondem aos campos de formulário de lead. No aplicativo zip independente ou importado, o usuário pode adicionar campos extras usando campos de formulário cq:form ou cta lead, nomeá-los e projetá-los de acordo com os requisitos.
* Mapeie campos de formulário de lead usando nomes específicos predefinidos do formulário de lead para CTA, por exemplo - firstName para nome no formulário de lead, e assim por diante.
* Os campos que não estão mapeados para o formulário de lead serão mapeados para cq:componentes do formulário - texto, rádio, caixa de seleção, lista suspensa, oculta, senha.
* O usuário pode fornecer o título usando a tag &quot;label&quot; e pode fornecer estilo usando o atributo de estilo &quot;class&quot; (disponível somente para componentes de formulário de lead para CTA).
* A página de agradecimento e a lista de subscrição podem ser fornecidas como um parâmetro oculto do formulário (presente no index.htm) ou podem ser adicionadas/editadas na barra de edição de &quot;Início do formulário de lead&quot;

   &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot;/>

   &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* Restrições como - obrigatórias podem ser fornecidas a partir da configuração de edição de cada componente.

tag HTML para incluir o componente de link gráfico no zip importado. Aqui, &quot;firstName&quot; é mapeado para o formulário de lead firstName e assim por diante, exceto por caixas de seleção - essas duas caixas de seleção mapeiam para o componente suspenso cq:form.

```xml
<div id="cqcanvas">
   <div id="form_wrapper">
    <h2>NEWSLETTER SIGN UP</h2>
       <div data-cq-component="leadFormGeneration">
       <form method="post" action="#" onsubmit="return popupBox()">
       <label for="firstName" class="checkText">
        FIRST NAME
       </label><br />
       <input name="firstName" class="text pink" type="text" /><br />
       <label for="lastName" class="checkText">
        LAST NAME
       </label><br />
       <input name="lastName" class="text pink" type="text" /><br />
       <label for="emailId" class="checkText">
        EMAIL ADDRESS
       </label><br />
       <input name="emailId" class="text pink" type="text" /><br />

       <div class="checkboxes">
       <input type="checkbox" class="check" name="send_news" /> <label for="send_news" class="checkText">Send me the latest We.Retail news and announcements.</label><br />
       <input type="checkbox" class="check" name="send_offers" /> <label for="send_offers" class="checkText">Send me We.Retail deals and special offers.</label><br />
       </div>
       <input type="submit" name="submit" class="submit pink" value="Sign Up >" />
       </form>
     </div>
   </div>
```

### Parsys {#parsys}

O componente parsys AEM é um componente de contêiner que pode conter outros componentes AEM. É possível adicionar um componente parsys no HTML importado. Isso permite que o usuário adicione/exclua componentes editáveis AEM à página de aterrissagem, mesmo após sua importação.

O sistema de parágrafo fornece aos usuários a capacidade de adicionar componentes usando o sidekick.

Marcação de HTML para inserir um componente parsys ( `foundation/components/parsys`) na HTML dentro do pacote de design:

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

A inclusão da marcação acima no HTML faz o seguinte:

* Insere um componente parsys AEM (foundation/components/parsys) na página de aterrissagem criada após a importação do pacote de design.
* Inicializa o sidekick com componentes padrão. Novos componentes podem ser adicionados à página de aterrissagem arrastando os componentes do sidekick para o componente parsys.
* Dois componentes de título também fazem parte do parsys.

### Destino {#target}

O componente de destino mostra o conteúdo de uma experiência na página. É possível ter muitas experiências criadas em uma campanha e o componente de destino pode mostrar dinamicamente o conteúdo de diferentes experiências para vários usuários que visitam a página.

A marcação html para inserir um componente de direcionamento e também criar experiências diferentes em uma campanha:

```xml
<div data-cq-component="target">
 <section data-cq-component="experience" data-cq-experience="default">
  <p data-cq-component="text">Default content. Select this campaign in client context to view other experiences</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="over-30">
  <p data-cq-component="text">Content for Over 30</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="under-30">
  <p data-cq-component="text">Content for Under 30</p>
 </section>
</div>
```

## Opções adicionais de importação {#additional-importing-options}

Além de especificar se os componentes importados são editáveis AEM componentes, você também pode configurar o seguinte antes de importar o pacote de design:

* Definir as propriedades da página ao extrair os metadados definidos no HTML importado.
* Especificação da codificação charset no HTML.
* Sobreposição do modelo de página do importador.

### Definição das propriedades da página ao extrair metadados definidos no HTML importado {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

Os seguintes metadados declarados no cabeçalho do HTML importado devem ser extraídos e conservados pelo importador de desenhos ou modelos como propriedade &quot;jcr:description&quot;:

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

O atributo Lang definido na tag HTML deve ser extraído e preservado pelo importador de design como propriedade &quot;jcr:language&quot;

* &lt;html lang=&quot;en&quot;>

### Especificação da codificação de charset no html {#specifying-the-charset-encoding-in-the-html}

O importador de design lê a codificação especificada no HTML importado. A codificação pode ser especificada da seguinte maneira:

`<meta charset="UTF-8">`

*OU*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

Se nenhuma codificação for especificada no HTML importado, a codificação padrão definida pelo importador de design será UTF-8.

### Sobreposição de modelo {#overlaying-template}

O modelo de Página de aterrissagem em branco pode ser substituído pela criação de um novo em: `/apps/<appName>/designimporter/templates/<templateName>`

As etapas para criar um novo modelo no AEM são explicadas [here](/help/sites-developing/templates.md).

### Referência a um componente da Landing page {#referring-a-component-from-landing-page}

Suponha que você tenha um componente que deseja referenciar em seu HTML usando o atributo data-cq-component, de modo que o importador de design renderize um componente para incluir neste local. Por exemplo, você deseja fazer referência ao componente de tabela ( `resourceType = /libs/foundation/components/table`). É necessário adicionar o seguinte no HTML:

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

O caminho no componente data-cq-deve ser o resourceType do componente.

### Práticas recomendadas     {#best-practices}

O uso de seletores de CSS semelhantes aos seguintes não é recomendado para uso com elementos que estão marcados para conversão de componentes na importação.

| E > F | um elemento F filho de um elemento E | [Combinador infantil](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | Um elemento F imediatamente precedido de um elemento E | [Combinador irmão adjacente](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | um elemento F precedido de um elemento E | [Combinador de irmãos](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:root | um elemento E, raiz do documento | [Pseudo-classes estruturais](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-child(n) | um elemento E, o n-ésimo filho do pai | [Pseudo-classes estruturais](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | um elemento E, o n-ésimo filho do pai, contando a partir do último | [Pseudo-classes estruturais](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-of-type(n) | um elemento E, o n-º irmão do seu tipo | [Pseudo-classes estruturais](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-of-type(n) | um elemento E, o n-º irmão de seu tipo, contando a partir do último | [Pseudo-classes estruturais](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

Isso se deve ao fato de elementos html adicionais como &lt;div> são adicionadas ao Html gerado após a importação.

* Scripts baseados na estrutura semelhante também não são recomendados para uso com elementos marcados para conversão em componentes AEM.
* Uso de estilos nas tags de marcação para conversão de componentes como &lt;div data-cq-component=&quot;&amp;ast;&quot;> não é recomendada.
* O layout de design deve seguir as práticas recomendadas do HTML5 Boilerplate. Leia mais sobre: [https://html5boilerplate.com/](https://html5boilerplate.com/).

## Configuração de módulos OSGI {#configuring-osgi-modules}

Os componentes que expõem propriedades configuráveis por meio do console OSGI são os seguintes:

* Importador de design de página de aterrissagem
* Criador de página de aterrissagem
* Criador de página de aterrissagem para dispositivos móveis
* Pré-processador de entrada de página de aterrissagem

A tabela abaixo descreve as propriedades:

<table>
 <tbody>
  <tr>
   <td><strong>Componente</strong></td>
   <td><strong>Nome da Propriedade</strong></td>
   <td><strong>Descrição da propriedade </strong></td>
  </tr>
  <tr>
   <td>Importador de design de página de aterrissagem</td>
   <td>Extrair filtro</td>
   <td>A lista de expressões regulares a serem usadas para filtrar arquivos da extração. <br /> As entradas de CEP que correspondem a qualquer um dos padrões especificados são excluídas da extração</td>
  </tr>
  <tr>
   <td>Criador de página de aterrissagem</td>
   <td>Padrão de arquivo</td>
   <td>O Construtor de página de aterrissagem pode ser configurado para lidar com arquivos HTML que correspondem a uma expressão regular conforme definido pelo padrão de arquivo.</td>
  </tr>
  <tr>
   <td>Criador de página de aterrissagem para dispositivos móveis</td>
   <td>Padrão de arquivo</td>
   <td>O Construtor de página de aterrissagem pode ser configurado para lidar com arquivos HTML que correspondem a uma expressão regular conforme definido pelo padrão de arquivo.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Grupos de dispositivos</td>
   <td>A lista de grupos de dispositivos a serem suportados.</td>
  </tr>
  <tr>
   <td>Pré-processador de entrada de página de aterrissagem</td>
   <td>Padrão de pesquisa </td>
   <td>O padrão a ser procurado, no conteúdo da entrada de arquivo. Essa expressão regular corresponde à linha de conteúdo de entrada por linha. Após a correspondência, o texto correspondente é substituído pelo padrão de substituição especificado.<br /> <br /> Consulte a observação abaixo sobre as limitações atuais do pré-processador de entrada de página inicial.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Substituir padrão</td>
   <td>O padrão que substitui as correspondências encontradas. Você pode usar referências de grupo regex como $1, $2. Além disso, esse padrão suporta palavras-chave como {designPath} que são resolvidas com o valor real durante a importação.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**Limitação atual do pré-processador de entrada de página de aterrissagem:**
>Se você precisar fazer alterações no padrão de pesquisa, ao abrir o editor de propriedades felix, será necessário adicionar manualmente caracteres de barra invertida para escapar dos metacaracteres regex. Se você não adicionar caracteres de barra invertida manualmente, o regex será considerado inválido e não substituirá o mais antigo.
>
>Por exemplo, se a configuração padrão for
>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>E você precisa substituir >`CQ_DESIGN_PATH` com `VIPURL` no padrão de pesquisa, o padrão de pesquisa deve ser semelhante a:
`/\* *VIPURL *\*/ *(['"])`

## Resolução de problemas {#troubleshooting}

Ao importar o pacote de design, você pode encontrar vários erros, descritos nesta seção.

### Inicialização do sidekick com componentes relevantes da página de aterrissagem {#initialization-of-sidekick-with-landing-page-relevant-components}

Se o pacote de design contiver uma marcação de componente parsys, depois da importação, o sidekick começará a mostrar componentes relevantes da página de aterrissagem. Você pode arrastar e soltar novos componentes no componente parsys na página de aterrissagem. Você também pode ir para o modo de design e adicionar novos componentes ao sidekick.

### Mensagens de erro exibidas durante a importação {#error-messages-displayed-during-import}

Em caso de erros (por exemplo, o pacote importado não é um zip válido), a importação de design não importará o pacote e, em vez disso, exibirá uma mensagem de erro na parte superior da página logo acima da caixa de arrastar e soltar. Exemplos de cenários de erro são apresentados aqui. Depois de corrigir o erro, você pode reimportar o zip atualizado para a mesma página de aterrissagem em branco. Diferentes cenários em que erros são lançados são os seguintes:

* O pacote de design importado não é um arquivo zip válido.
* O pacote de design importado não contém um index.html no nível superior.

### Avisos exibidos após a importação {#warnings-displayed-after-import}

No caso de avisos (por exemplo, HTML refere-se a imagens que não existem no pacote), o importador de design importará o zip, mas ao mesmo tempo exibirá uma lista de problemas/avisos no Painel de resultados, Clicando no link de problemas, exibirá uma lista de avisos que apontam quaisquer problemas no pacote de design. Diferentes cenários em que os avisos são capturados e exibidos pelo importador de design são os seguintes:

* HTML refere-se às imagens que não existem no pacote.
* HTML refere-se aos scripts que não existem no pacote.
* HTML refere-se aos estilos que não existem no pacote.

### Onde os arquivos do arquivo ZIP estão sendo armazenados no AEM? {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

Após a importação da landing page, os arquivos (imagens, css, js, etc.) no pacote de design são armazenadas no seguinte local em AEM:

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

Suponha que a landing page seja criada sob a campanha We.Retail e o nome da landing page seja **myBlankLandingPage** em seguida, o local onde os arquivos Zip são armazenados é o seguinte:

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### Formatação não preservada {#formatting-not-preserved}

Ao criar seu CSS, esteja ciente das seguintes limitações:

Se um texto e uma imagem (editável) forem semelhantes a:

```xml
<div class="box">
<p><div data-cq-component="image"><img src="assets/image.jpg" width="115"
height="116" /></div>Some Text </p>
</div>
```

com um CSS aplicado na classe `box` como se segue:

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

Então `box img` é usada no importador de design, a landing page resultante parece não ter preservado a formatação. Para contornar isso, esteja ciente de que o AEM adiciona tags div no CSS e reescreve o código de acordo. Caso contrário, algumas regras de CSS serão inválidas.

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
Além disso, os designers devem estar cientes de que somente o código dentro da variável **id=cqcanvas** é reconhecida pelo importador, caso contrário, o design não é preservado.
