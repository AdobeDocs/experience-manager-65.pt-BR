---
title: Extensão e configuração do importador de design para páginas iniciais
description: Saiba como configurar o Importador de design para páginas iniciais.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 1b8c6075-13c6-4277-b726-8dea7991efec
source-git-commit: 80e85ed78a26d784f4aa8e36c7de413cf9c03fa2
workflow-type: tm+mt
source-wordcount: '3442'
ht-degree: 0%

---

# Extensão e configuração do importador de design para páginas iniciais{#extending-and-configuring-the-design-importer-for-landing-pages}

Esta seção descreve como configurar e, se desejado, estender o importador de design para páginas de aterrissagem. O trabalho com landing pages após a importação é coberto na [Landing Pages.](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**Fazer o importador de design extrair seu componente personalizado**

Estas são as etapas lógicas para fazer o importador de design reconhecer seu componente personalizado

1. Criar um TagHandler

   * Um manipulador de tags é um POJO que lida com tags HTML de um tipo específico. O &quot;tipo&quot; de tags HTML que seu TagHandler pode manipular é definido por meio da propriedade OSGi &quot;tagpattern.name&quot; de TagHandlerFactory. Essa propriedade OSGi é essencialmente um regex que deve corresponder à tag html de entrada que você deseja manipular. Todas as tags aninhadas seriam lançadas ao manipulador de tags para manipulação. Por exemplo, se você se registrar para uma div que contém uma variável &lt;p> tag, a variável &lt;p> Tag também seria lançado para o seu TagHandler e depende de você como você deseja cuidar dele.
   * A interface do manipulador de tags é semelhante a uma interface do manipulador de conteúdo SAX. Ele recebe eventos SAX para cada tag html. Como provedor de manipulador de tags, é necessário implementar determinados métodos de ciclo de vida que são chamados automaticamente pela estrutura do importador de design.

1. Crie o TagHandlerFactory correspondente.

   * A fábrica do manipulador de tags é um componente OSGi (singleton) responsável por gerar instâncias do seu manipulador de tags.
   * a fábrica do manipulador de tags deve expor uma propriedade OSGi chamada &quot;tagpattern.name&quot;, cujo valor corresponde à tag html de entrada.
   * Se houver vários manipuladores de tag que correspondam à tag html de entrada, aquele com uma classificação mais alta será escolhido. A própria classificação é exposta como uma propriedade OSGi **classificação.serviço**.
   * TagHandlerFactory é um componente OSGi. Todas as referências que você deseja fornecer ao seu TagHandler devem ser fornecidas por meio dessa fábrica.

1. Certifique-se de que o TagHandlerFactory tenha uma classificação melhor se desejar substituir o padrão.

>[!CAUTION]
>
>O Importador de design, usado para importar páginas de aterrissagem, [foi descontinuado com o AEM 6.5](/help/release-notes/deprecated-removed-features.md#deprecated-features).

## Preparação do HTML para importação {#preparing-the-html-for-import}

Depois de criar uma página de importação, você pode importar a página de aterrissagem de HTML completo. Para importar a página de aterrissagem do HTML, primeiro você precisa compactar o conteúdo em um pacote de design. O pacote de design contém a página de aterrissagem do HTML junto com os ativos referenciados (imagens, css, ícones, scripts e assim por diante).

A seguinte folha de características fornece uma amostra de como preparar seu HTML para importação:

Folha de características da página de destino

[Obter arquivo](assets/cheatsheet.zip)

### Layout e requisitos do arquivo Zip {#zip-file-layout-and-requirements}

>[!NOTE]
>
>Nesse ponto, os arquivos ZIP só podem conter uma página de HTML ou uma parte de uma página.

Este é um exemplo de layout do zip:

* /index.html > arquivo HTML da página de aterrissagem
* /css > para adicionar ao clientlib CSS
* /img > todas as imagens e ativos
* /js > para adicionar ao clientlib JS

O layout é baseado no layout de práticas recomendadas do HTML5 Boilerplate. Leia mais em [https://html5boilerplate.com/](https://html5boilerplate.com/)

>[!NOTE]
>
>No mínimo, o pacote de design **deve** contém um **index.html** arquivo no nível raiz. Se a landing page a ser importada também tiver uma versão móvel, o zip deverá conter uma **mobile.index.html** junto com **index.html** no nível raiz.

### Preparação do HTML da landing page {#preparing-the-landing-page-html}

Para importar o HTML, é necessário adicionar uma div da tela de desenho ao HTML da página de aterrissagem.

A div da tela é um html **div** com `id="cqcanvas"` que deve ser inserido no HTML `<body>` e devem vincular o conteúdo destinado à conversão.

Um trecho de amostra do HTML da landing page após a adição da div da tela é o seguinte:

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

### Preparação do HTML para incluir componentes editáveis do AEM {#preparing-the-html-to-include-editable-aem-components}

Ao importar uma landing page, você tem a opção de importar a página como está, o que significa que, após a importação, não é possível editar nenhum dos itens importados no AEM (ainda é possível adicionar outros componentes do AEM na página).

Antes de importar a landing page, convém converter algumas partes da landing page para que elas sejam componentes de AEM editáveis. Isso permite editar rapidamente partes da página de aterrissagem, mesmo depois que o design da página de aterrissagem for importado.

Para fazer isso, adicione o `data-cq-component` para o componente apropriado no arquivo de HTML que você importa.

A seção a seguir descreve como editar o arquivo HTML para converter determinadas partes das páginas de aterrissagem em diferentes componentes editáveis do AEM. Os componentes são descritos em detalhes em [Componentes de páginas de aterrissagem](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md).

>[!NOTE]
>
>A marcação HTML para converter partes da landing page em componentes AEM tem um formulário longo e uma declaração de tag abreviada. Ambos são descritos para cada componente.

### Limitações {#limitations}

Antes de importar, observe as seguintes limitações:

### Qualquer atributo como classe ou id aplicado na tag &amp;lt;body> não é preservado {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

Se qualquer atributo, como id ou classe, for aplicado na tag body, por exemplo, `<body id="container">` então, não será preservado após a importação. Portanto, o design que está sendo importado não deve ter dependências nos atributos aplicados na `<body>` tag.

### Arrastar e soltar zip {#drag-and-drop-zip}

O upload do zip de arrastar/soltar não é compatível com o Internet Explorer e com as versões 3.6 e anteriores do Firefox. Para fazer upload de um design ao usar esses navegadores, clique na zona soltar arquivo para abrir uma caixa de diálogo de upload de arquivo e fazer upload do design usando essa caixa de diálogo.

Os navegadores compatíveis com &quot;arrastar e soltar&quot; do zip de design são Chrome, Safari5.x, Firefox 4 e superior.

### Modernizador não é suportado {#modernizr-is-not-supported}

`Modernizr.js` é uma ferramenta baseada em JavaScript que detecta recursos nativos de navegadores e detecta se eles são adequados para elementos html5 ou não. Designs que usam o Modernizador para aprimorar o suporte em versões mais antigas de navegadores diferentes podem causar problemas de importação na solução de página de aterrissagem. `Modernizr.js` scripts não são suportados com o importador Design.

### As propriedades da página não são preservadas no momento da importação do pacote de design {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

Qualquer propriedade de página (por exemplo, Domínio personalizado, Imposição de HTTPS e assim por diante) definida para uma página (que usa o modelo de Página de aterrissagem em branco) antes de importar o pacote de design é perdida após a importação do design. Portanto, a prática recomendada é definir as propriedades da página após importar o pacote de design.

### Marcação somente HTML assumida {#html-only-markup-assumed}

Durante a importação, a marcação é limpa por motivos de segurança e para evitar a importação e a publicação de marcação inválida. Isso pressupõe uma marcação somente HTML e todas as outras formas de elementos, como SVG em linha ou Componentes da Web, serão filtradas.

### Texto {#text}

Marcação HTML para inserir um componente de texto ( `foundation/components/text`) no HTML dentro do pacote de design:

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

Incluindo a marcação acima no HTML, o faz o seguinte:

* Cria um componente de texto AEM editável ( `sling:resourceType=foundation/components/text`) na landing page criada após a importação do pacote de design.
* Define o `text` propriedade do componente de texto criado para o HTML contido na variável `div`.

**Declaração de tag de componente abreviada**:

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**Texto com uma lista**

Para adicionar um texto com uma lista:

* 1º
* 2nd

que podem ser editadas no editor de RTE:

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**Texto com cor**

Para adicionar um texto com cor (rosa) que possa ser editado no editor RTE:

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### Título {#title}

Marcação HTML para inserir um componente de título ( `wcm/landingpage/components/title`) no HTML dentro do pacote de design:

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

Incluindo a marcação acima no HTML, o faz o seguinte:

* Cria um componente de título AEM editável ( `sling:resourceType=wcm/landingpage/components/title`) na landing page criada após a importação do pacote de design.
* Define o `jcr:title` propriedade do componente de título criado para o texto dentro da tag de cabeçalho encapsulada em div.
* Define o `type` à tag de cabeçalho, nesse caso `h1`.

O componente de título é compatível com sete tipos - `h1, h2, h3, h4, h5, h6` e `default`.

**Declaração de tag de componente abreviada**:

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### Imagem {#image}

marcação HTML para inserir um componente de imagem (foundation/components/image) no HTML dentro do pacote de design:

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

Incluindo a marcação acima no HTML, o faz o seguinte:

* Cria um componente de imagem AEM editável ( `sling:resourceType=foundation/components/image`) na landing page criada após a importação do pacote de design.
* Define o `fileReference` propriedade do componente de imagem criado para o caminho para o qual a imagem especificada no atributo src é importada.
* Define o `alt` ao valor do atributo alt na tag img.
* Define o `title` ao valor do atributo title na tag img.
* Define o `width` ao valor do atributo width na tag img.
* Define o `height` ao valor do atributo height na tag img.

**Declaração de tag de componente abreviada:**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### URL absoluto img src não suportado no componente de Imagem Div {#absolute-url-img-src-not-supported-within-image-component-div}

Se um `<img>` com um url absoluto src for tentado para a conversão de componentes, um método **UnsupportedTagContentException** é elevada. Por exemplo, o seguinte não é suportado:

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

Caso contrário, as imagens de URL absolutas são suportadas para tags img que não fazem parte do componente de Imagem div.

### Componentes de frase de chamariz {#call-to-action-components}

Você pode marcar parte da página de aterrissagem para importação como um &quot;componente de chamada para ação editável&quot;; esses componentes de chamada para ação importados podem ser editados após a importação da página de aterrissagem. O AEM inclui os seguintes componentes do CTA:

* Clicar através do link - Permite adicionar um link de texto que, quando clicado, leva o visitante a um URL de destino.
* Link gráfico - Permite adicionar uma imagem que, quando clicada, leva o visitante a um URL de destino.

#### Link de Click Through {#click-through-link}

Esse componente CTA pode ser usado para adicionar um link de texto na landing page.

Propriedades suportadas

* Rótulo, com as opções negrito, itálico e sublinhado
* URL do Target, compatível com URL de terceiros e AEM
* Opções de renderização de página (mesma janela, nova janela e assim por diante)

tag HTML para incluir o componente de click-through no zip importado. Aqui, o href mapeia para o url de destino, a opção &quot;Exibir detalhes do produto&quot; mapeia para o rótulo e assim por diante.

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

**Declaração de tag de componente abreviada**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### Vincular ao gráfico {#graphical-link}

Esse componente CTA pode ser usado para adicionar qualquer imagem gráfica com link na página de destino. A imagem pode ser um botão simples ou qualquer imagem gráfica como plano de fundo. Quando a imagem é clicada, o usuário é levado para o URL de destino especificado nas propriedades do componente. Ele faz parte do grupo &quot;Plano de ação&quot;.

Propriedades suportadas

* Recorte de imagem, rotação
* Focalizar texto, descrição, tamanho em px
* URL do Target, compatível com URL de terceiros e AEM
* Opções de renderização de página (mesma janela, nova janela e assim por diante)

tag HTML para incluir o componente de link gráfico no zip importado. Aqui, href mapeia para o url de destino, img src é a imagem de renderização, &quot;title&quot; é tomado como texto ao passar o mouse e assim por diante.

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**Declaração de tag de componente abreviada**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>Para criar um link gráfico clickthrough, é necessário envolver uma tag de âncora e a tag de imagem dentro de uma div com `data-cq-component="clickthroughgraphicallink"` atributo.
>
>Por exemplo, `<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>Outras maneiras de associar uma imagem a uma tag de âncora usando CSS não são compatíveis. Por exemplo, a marcação a seguir não funciona:
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>com um associado `css .hasbackground { background-image: pathtoimage }`
>

### Formulário de cliente em potencial {#lead-form}

Um formulário de cliente potencial é um formulário usado para coletar informações de perfil de um visitante/cliente potencial. Essas informações podem ser armazenadas e usadas posteriormente para fazer um marketing eficaz com base nas informações. Essas informações geralmente incluem título, nome, email, data de nascimento, endereço, interesse e assim por diante. Faz parte do grupo &quot;Formulário de cliente potencial CTA&quot;.

**Recursos compatíveis**

* Campos de leads predefinidos - nome, sobrenome, endereço, data, gênero, sobre, userId, emailId, botão enviar estão disponíveis no sidekick. Basta arrastar/soltar o componente desejado em seu formulário de lead.
* Com a ajuda desses componentes, o autor pode criar um formulário de cliente potencial independente, esses campos correspondem a campos de formulário de cliente potencial. Em aplicativos zip independentes ou importados, o usuário pode adicionar campos extras usando campos de formulário de cliente em potencial cq:form ou cta, nomeá-los e projetá-los de acordo com os requisitos.
* Mapeie campos de formulário de cliente potencial usando nomes predefinidos específicos do formulário de cliente potencial CTA, por exemplo, - firstName para o nome no formulário de cliente potencial e assim por diante.
* Os campos que não estão mapeados para formulários de cliente potencial são mapeados para cq:componentes de formulário - texto, rádio, caixa de seleção, lista suspensa, oculto, senha.
* O usuário pode fornecer o título usando a tag &quot;label&quot; e o estilo usando o atributo de estilo &quot;class&quot; (disponível somente para componentes de formulário de lead CTA).
* A página de agradecimento e a lista de assinaturas podem ser fornecidas como um parâmetro oculto do formulário (presente no index.htm) ou podem ser adicionadas/editadas na barra de edição do &quot;Início do formulário de cliente potencial&quot;

  &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot;/>

  &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* Restrições como - necessárias podem ser fornecidas a partir da configuração de edição de cada um dos componentes.

tag HTML para incluir o componente de link gráfico no zip importado. Aqui, &quot;firstName&quot; é mapeado para o formulário de cliente potencial firstName, e assim por diante, exceto para caixas de seleção - essas duas caixas de seleção mapeiam para o componente cq:form dropdown.

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

O componente parsys do AEM é um componente de contêiner que pode conter outros componentes do AEM. É possível adicionar um componente parsys no HTML importado. Isso permite que o usuário adicione/exclua componentes editáveis do AEM na página de aterrissagem mesmo após sua importação.

O sistema de parágrafo oferece aos usuários a capacidade de adicionar componentes usando o sidekick.

Marcação HTML para inserir um componente parsys ( `foundation/components/parsys`) no HTML dentro do pacote de design:

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

A inclusão da marcação acima no HTML faz o seguinte:

* Insere um componente parsys do AEM (foundation/components/parsys) na landing page criada após a importação do pacote de design.
* Inicializa o sidekick com componentes padrão. Novos componentes podem ser adicionados à página de aterrissagem arrastando componentes do sidekick para o componente parsys.
* Dois componentes de título também fazem parte do parsys.

### Planejado {#target}

O componente de Direcionamento mostra o conteúdo de uma experiência na página. É possível ter muitas experiências criadas em uma campanha e o componente de Direcionamento pode mostrar dinamicamente o conteúdo de diferentes experiências para vários usuários que visitam a página.

A marcação html para inserir um componente de direcionamento e também criar diferentes experiências em uma campanha:

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

## Opções de importação adicionais {#additional-importing-options}

Além de especificar se os componentes importados são componentes AEM editáveis, você também pode configurar o seguinte antes de importar o pacote de design:

* Definir propriedades de página extraindo os metadados definidos no HTML importado.
* Especificando a codificação de conjunto de caracteres no HTML.
* Sobrepondo o modelo de página do importador.

### Definir propriedades de página extraindo metadados definidos no HTML importado {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

Os seguintes metadados declarados no cabeçalho do HTML importado devem ser extraídos e preservados pelo importador de concepção como propriedade &quot;jcr:description&quot;:

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

O atributo Lang definido na tag HTML deve ser extraído e preservado pelo importador de design como a propriedade &quot;jcr:language&quot;

* &lt;html lang=&quot;en&quot;>

### Especificar a codificação de conjunto de caracteres no html {#specifying-the-charset-encoding-in-the-html}

O importador de design lê a codificação especificada no HTML importado. A codificação pode ser especificada da seguinte maneira:

`<meta charset="UTF-8">`

*OU*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

Se nenhuma codificação for especificada no HTML importado, a codificação padrão definida pelo importador de design será UTF-8.

### Sobrepondo modelo {#overlaying-template}

O modelo de página de aterrissagem em branco pode ser sobreposto ao criar um em: `/apps/<appName>/designimporter/templates/<templateName>`

As etapas para criar um modelo no AEM são explicadas [aqui](/help/sites-developing/templates.md).

### Referência a um componente da landing page {#referring-a-component-from-landing-page}

Suponha que você tenha um componente que deseja referenciar em seu HTML usando o atributo data-cq-component de modo que o importador de design renderize um componente para incluir neste local. Por exemplo, você deseja fazer referência ao componente de tabela ( `resourceType = /libs/foundation/components/table`). O seguinte precisa ser adicionado no HTML:

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

O caminho no data-cq-component deve ser o resourceType do componente.

### Práticas recomendadas {#best-practices}

O uso de seletores CSS semelhantes aos seguintes não é recomendado para uso com elementos marcados para conversão de componentes na importação.

| E > F | um elemento F filho de um elemento E | [Combinador filho](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | um elemento F imediatamente precedido por um elemento E | [Combinador irmão adjacente](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | um elemento F precedido por um elemento E | [Combinador irmão geral](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:raiz | um elemento E, raiz do documento | [Pseudo-classes estruturais](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:enésimo filho(n) | um elemento E, o enésimo filho de seu pai | [Pseudo-classes estruturais](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:enésimo-último-filho(n) | um elemento E, o enésimo filho de seu pai, contando do último | [Pseudo-classes estruturais](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:n-ésimo de tipo(n) | um elemento E, o n-ésimo irmão de seu tipo | [Pseudo-classes estruturais](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:enésimo-último-de-tipo(n) | um elemento E, o n-ésimo irmão de seu tipo, contando do último | [Pseudo-classes estruturais](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

Isso ocorre porque elementos html adicionais, como &lt;div> são adicionadas ao HTML gerado após a importação.

* Scripts que dependem da estrutura semelhante à mostrada acima também não são recomendados para uso com elementos marcados para conversão em componentes AEM.
* O uso de estilos nas tags de marcação para conversão de componentes como &lt;div data-cq-component=&quot;&amp;ast;&quot;> não é recomendado.
* O layout de design deve seguir as práticas recomendadas da placa de expansão HTML5. Leia mais sobre: [https://html5boilerplate.com/](https://html5boilerplate.com/).

## Configuração de módulos OSGI {#configuring-osgi-modules}

Os componentes que expõem propriedades configuráveis por meio do console OSGI são os seguintes:

* Importador de design de landing page
* Construtor de landing page
* Construtor de página de aterrissagem móvel
* Pré-processador de entrada de página inicial

A tabela abaixo descreve brevemente as propriedades:

<table>
 <tbody>
  <tr>
   <td><strong>Componente</strong></td>
   <td><strong>Nome de propriedade</strong></td>
   <td><strong>Descrição da propriedade </strong></td>
  </tr>
  <tr>
   <td>Importador de design de landing page</td>
   <td>Extrair filtro</td>
   <td>A lista de expressões regulares a serem usadas para filtrar arquivos da extração. <br /> As entradas de CEP correspondentes a qualquer um dos padrões especificados são excluídas da extração</td>
  </tr>
  <tr>
   <td>Construtor de landing page</td>
   <td>Padrão do arquivo</td>
   <td>O Construtor de landing pages pode ser configurado para lidar com arquivos HTML que correspondem a uma expressão regular, conforme definido pelo padrão do arquivo.</td>
  </tr>
  <tr>
   <td>Construtor de página de aterrissagem móvel</td>
   <td>Padrão do arquivo</td>
   <td>O Construtor de landing pages pode ser configurado para lidar com arquivos HTML que correspondem a uma expressão regular, conforme definido pelo padrão do arquivo.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Grupos de dispositivos</td>
   <td>A lista de grupos de dispositivos a serem suportados.</td>
  </tr>
  <tr>
   <td>Pré-processador de entrada de página inicial</td>
   <td>Padrão de pesquisa </td>
   <td>O padrão a ser pesquisado, no conteúdo da entrada do arquivo. Essa expressão regular corresponde ao conteúdo da entrada linha por linha. Após a correspondência, o texto correspondente é substituído pelo padrão de substituição especificado.<br /> <br /> Consulte a observação abaixo sobre as limitações atuais de pré-processador de entrada de página de aterrissagem.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Substituir padrão</td>
   <td>O padrão que substitui as correspondências encontradas. Você pode usar referências de grupos regex como $1, $2. Além disso, esse padrão suporta palavras-chave como {designPath} que são resolvidos com o valor real durante a importação.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**Limitação atual do pré-processador de entrada de página inicial:**
>Se você precisar fazer alterações no padrão de pesquisa, ao abrir o editor de propriedades felix, será necessário adicionar manualmente caracteres de barra invertida para escapar dos metacaracteres regex. Se você não adicionar caracteres de barra invertida manualmente, o regex será considerado inválido e não substituirá o mais antigo.
>
>Por exemplo, se a configuração padrão for
>
>>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>E você precisa substituir `CQ_DESIGN_PATH` com `VIPURL` no padrão de pesquisa, o padrão de pesquisa deve ter esta aparência:
>
>`/\* *VIPURL *\*/ *(['"])`

## Resolução de problemas {#troubleshooting}

Ao importar o pacote de design, você pode encontrar vários erros, descritos nesta seção.

### Inicialização do sidekick com componentes relevantes para a página de aterrissagem {#initialization-of-sidekick-with-landing-page-relevant-components}

Se o pacote de design contiver uma marcação de componente parsys, após a importação, o sidekick começará a mostrar componentes relevantes da página inicial. Você pode arrastar e soltar novos componentes no componente parsys na página de aterrissagem. Você também pode ir para o modo de design e adicionar novos componentes ao sidekick.

### Mensagens de erro exibidas durante a importação {#error-messages-displayed-during-import}

Se houver erros (por exemplo, o pacote importado não é um zip válido), a importação do design não importará o pacote. Em vez disso, uma mensagem de erro é exibida na parte superior da página logo acima da caixa de arrastar e soltar. Exemplos de cenários de erro são apresentados aqui. Após corrigir o erro, é possível reimportar o zip atualizado para a mesma landing page em branco. Os diferentes cenários em que os erros são lançados são os seguintes:

* O pacote de design importado não é um arquivo zip válido.
* O pacote de design importado não contém um index.html no nível superior.

### Avisos exibidos após a importação {#warnings-displayed-after-import}

Se houver avisos (por exemplo, HTML se refere a imagens que não existem no pacote), o importador de design importa o zip, mas ao mesmo tempo exibe uma lista de problemas/avisos no Painel de resultados. Ao clicar no link de problemas, será exibida uma lista de avisos que apontam quaisquer problemas no pacote de design. Os diferentes cenários em que os avisos são capturados e exibidos pelo importador de design são os seguintes:

* HTML refere-se a imagens que não existem no pacote.
* HTML refere-se a scripts que não existem no pacote.
* HTML refere-se a estilos que não existem no pacote.

### Onde os arquivos do arquivo ZIP estão sendo armazenados no AEM? {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

Depois que a landing page é importada, os arquivos (imagens, css, js e assim por diante) no pacote de design são armazenados no seguinte local no AEM:

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

Suponha que a landing page seja criada na campanha `We.Retail` e o nome da landing page for **myBlankLandingPage** em seguida, o local onde os arquivos Zip são armazenados é o seguinte:

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### Formatação não preservada {#formatting-not-preserved}

Ao criar seu CSS, esteja ciente das seguintes limitações:

Se um texto e uma imagem (editável) forem como os seguintes:

```xml
<div class="box">
<p><div data-cq-component="image"><img src="assets/image.jpg" width="115"
height="116" /></div>Some Text </p>
</div>
```

com um CSS aplicado na classe `box` do seguinte modo:

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

Depois `box img` for usada no importador de design, a landing page resultante parecerá não ter preservado a formatação. Para contornar isso, o AEM adiciona tags div no CSS e reescreve o código de acordo. Caso contrário, algumas regras CSS serão inválidas.

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
>
>Os designers devem codificar somente dentro do **id=cqcanvas** for reconhecida pelo importador, caso contrário, o design não será preservado.
