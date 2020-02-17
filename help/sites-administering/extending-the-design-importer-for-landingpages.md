---
title: Extensão e configuração do Importador de design para páginas iniciais
seo-title: Extensão e configuração do Importador de design para páginas iniciais
description: Saiba como configurar o Importador de design para páginas iniciais.
seo-description: Saiba como configurar o Importador de design para páginas iniciais.
uuid: a2dd0c30-03e4-4e52-ba01-6b0b306c90fc
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e02f5484-fbc2-40dc-8d06-ddb53fd9afc2
docset: aem65
translation-type: tm+mt
source-git-commit: 0a94bf49a7136c5831c42eb274d07517c12014ec

---


# Extensão e configuração do Importador de design para páginas iniciais{#extending-and-configuring-the-design-importer-for-landing-pages}

Esta seção descreve como configurar e, se desejado, estender o importador de design para páginas iniciais. Trabalhar com páginas de aterrissagem após a importação é abordado em Páginas de [aterrissagem.](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**Como fazer com que o importador de design extraia seu componente personalizado**

Estas são as etapas lógicas para fazer com que o importador de design reconheça seu componente personalizado

1. Criar um TagHandler

   * Um manipulador de tags é um POJO que manipula tags HTML de um tipo específico. O &quot;tipo&quot; de tags HTML que seu TagHandler pode manipular é definido pela propriedade &quot;tagpattern.name&quot; do OSGi de TagHandlerFactory. Essa propriedade OSGi é essencialmente um regex que deve corresponder à tag html de entrada que você deseja manipular. Todas as tags aninhadas seriam jogadas ao seu manipulador de tags para manipulação. Por exemplo, se você se registrar em uma div que contém uma tag &lt;p> aninhada, a tag &lt;p> também será jogada em seu TagHandler e depende de você como deseja cuidar dela.
   * A interface do manipulador de tags é semelhante a uma interface do manipulador de conteúdo SAX. Ele recebe eventos SAX para cada tag html. Como um provedor manipulador de tags, é necessário implementar certos métodos de ciclo de vida que são automaticamente chamados pela estrutura do importador de design.

1. Crie seu TagHandlerFactory correspondente.

   * A fábrica do manipulador de tags é um componente OSGi (singleton) responsável pelas instâncias de geração do manipulador de tags.
   * sua fábrica do manipulador de tags deve expor uma propriedade OSGi chamada &quot;tagpattern.name&quot; cujo valor é comparado com a tag html de entrada.
   * Se houver vários manipuladores de tags que correspondem à tag html de entrada, o que tem uma classificação mais alta será escolhido. A própria classificação é exposta como um **service.ranking** de propriedade OSGi.
   * O TagHandlerFactory é um componente OSGi. Todas as referências que você deseja fornecer ao TagHandler devem ser feitas via esta fábrica.

1. Certifique-se de que sua TagHandlerFactory tenha uma classificação melhor se desejar substituir o padrão.

>[!CAUTION]
>
>O Importador de Design, usado para importar páginas de aterrissagem, [ foi descontinuado com o AEM 6.5](/help/release-notes/deprecated-removed-features.md#deprecated-features).

## Preparação do HTML para importação {#preparing-the-html-for-import}

Depois de criar uma página de importador, você pode importar sua página inicial HTML completa. Para importar sua página inicial HTML, primeiro compacte seu conteúdo em um pacote de design. O pacote de design contém sua página inicial HTML junto com os ativos referenciados (imagens, css, ícones, scripts e assim por diante).

A seguinte folha de prova fornece uma amostra de como preparar seu HTML para importação:

Folha de capítulo da página inicial

[Obter arquivo](assets/cheatsheet.zip)

### Layout e requisitos do arquivo zip {#zip-file-layout-and-requirements}

>[!NOTE]
>
>Nesse ponto, os arquivos ZIP podem conter apenas uma página HTML ou uma parte de uma página.

Um exemplo de layout do zip é o seguinte:

* /index.html -> arquivo HTML da página de aterrissagem
* /css -> para adicionar à clientlib do CSS
* /img -> todas as imagens e ativos
* /js -> para adicionar à clientlib JS

O layout se baseia no layout de práticas recomendadas do HTML5 Boilerplate. Leia mais em [https://html5boilerplate.com/](https://html5boilerplate.com/)

>[!NOTE]
>
>No mínimo, o pacote de design **deve** conter um arquivo **index.html** no nível raiz. Caso a página inicial a ser importada também tenha uma versão móvel, o zip deve conter um **mobile.index.html** junto com o **index.html** no nível raiz.

### Preparação do HTML da página inicial {#preparing-the-landing-page-html}

Para poder importar o HTML, é necessário adicionar uma div de tela ao HTML da página de aterrissagem.

A tela div é um html **div** com `id="cqcanvas"` o qual deve ser inserido dentro da `<body>` tag HTML e deve envolver o conteúdo destinado à conversão.

Um trecho de amostra do HTML da página inicial após a adição da tela div é o seguinte:

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

Ao importar uma página de aterrissagem, você tem a opção de importar a página como está, o que significa que após a página de aterrissagem ser importada, você não poderá editar nenhum dos itens importados no AEM (você ainda poderá adicionar outros componentes do AEM na página).

Antes de importar a página de aterrissagem, talvez você queira converter algumas partes da página de aterrissagem para que sejam componentes editáveis do AEM. Isso permite que você edite rapidamente partes da página inicial mesmo depois que o design da página inicial for importado.

Para fazer isso, adicione o componente apropriado `data-cq-component` ao arquivo HTML que você importa.

A seção a seguir descreve como editar seu arquivo HTML para que você converta certas partes de suas páginas iniciais em diferentes componentes editáveis do AEM. Os componentes são descritos detalhadamente em Componentes [de páginas](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)iniciais.

>[!NOTE]
>
>A marcação HTML para converter partes da página de aterrissagem em componentes AEM tem uma declaração de formulário longa e de tag curta. Ambos estão descritos para cada componente.

### Limitações {#limitations}

Antes de importar, observe as seguintes limitações:

### Qualquer atributo como classe ou id aplicado na tag &amp;lt;body> não é preservado {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

Se algum atributo como id ou class for aplicado na tag body, por exemplo, `<body id="container">` , ele não será preservado após a importação. Portanto, o design que está sendo importado não deve ter nenhuma dependência dos atributos aplicados na `<body>` tag .

### Arrastar e soltar zip {#drag-and-drop-zip}

O carregamento de zip de arrastar/soltar não é compatível com o Internet Explorer e o Firefox versões 3.6 e anteriores. Para fazer upload de um design ao usar esses navegadores, clique na área de arquivo para abrir uma caixa de diálogo de upload de arquivo e faça upload do design usando essa caixa de diálogo.

Os navegadores compatíveis com &quot;arrastar e soltar&quot; do zip de design são Chrome, Safari5.x, Firefox 4 e superior.

### Modernizador não é suportado {#modernizr-is-not-supported}

`Modernizr.js` é uma ferramenta baseada em javascript que detecta recursos nativos de navegadores e detecta se são adequados para elementos html5 ou não. Os designs que usam o Modernizer para aprimorar o suporte em versões mais antigas de navegadores diferentes podem causar problemas de importação na solução da página de aterrissagem. `Modernizr.js` scripts não são suportados pelo importador de design.

### As propriedades da página não são preservadas no momento da importação do pacote de design {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

Qualquer propriedade de página (por exemplo, Domínio personalizado, Imposição de HTTPS etc.) definido para uma página (que usa o modelo de Página inicial em branco) antes de importar o pacote de design são perdidos depois que o design é importado. Portanto, a prática recomendada é definir as propriedades da página depois de importar o pacote de design.

### Marcação somente HTML assumida {#html-only-markup-assumed}

Ao importar, a marcação analisada por motivos de segurança e para evitar a importação e publicação de uma marcação inválida. Isso pressupõe que a marcação somente de HTML e outras formas de elementos, como componentes incorporados SVG ou da Web serão filtrados.

### Texto {#text}

Marcação HTML para inserir um componente de texto ( `foundation/components/text`) no HTML dentro do pacote de design:

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

A inclusão da marcação acima no HTML faz o seguinte:

* Cria um componente de texto AEM editável ( `sling:resourceType=foundation/components/text`) na página inicial criada após a importação do pacote de design.
* Define a `text` propriedade do componente de texto criado para o HTML delimitado no `div`.

**Declaração** abreviada de tag do componente:

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**Texto com uma lista**

Para adicionar um texto com uma lista:

* 1st
* 2nd

que podem ser editados no editor RTE:

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**Texto com cor**

Para adicionar um texto com cor (rosa) que pode ser editado no editor RTE:

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### Título {#title}

Marcação HTML para inserir um componente de título ( `wcm/landingpage/components/title`) no HTML dentro do pacote de design:

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

A inclusão da marcação acima no HTML faz o seguinte:

* Cria um componente de título do AEM editável ( `sling:resourceType=wcm/landingpage/components/title`) na página inicial criada após a importação do pacote de design.
* Define a `jcr:title` propriedade do componente de título criado para o texto dentro da tag de cabeçalho encapsulada em div.
* Define a `type` propriedade para a marca de cabeçalho, neste caso `h1`.

O componente de título suporta 7 tipos - `h1, h2, h3, h4, h5, h6` e `default`.

**Declaração** abreviada de tag do componente:

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### Imagem {#image}

Marcação HTML para inserir um componente de imagem (base/componentes/imagem) no HTML dentro do pacote de design:

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

A inclusão da marcação acima no HTML faz o seguinte:

* Cria um componente de imagem do AEM editável ( `sling:resourceType=foundation/components/image`) na página inicial criada após a importação do pacote de design.
* Define a `fileReference` propriedade do componente de imagem criado para o caminho para o qual a imagem especificada no atributo src é importada.
* Define a `alt` propriedade para o valor do atributo alt na tag img.
* Define a `title` propriedade para o valor do atributo title na tag img.
* Define a `width` propriedade para o valor do atributo width na tag img.
* Define a `height` propriedade para o valor do atributo height na tag img.

**Declaração abreviada de tag do componente:**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### URL absoluto img src não suportado no componente de imagem Div {#absolute-url-img-src-not-supported-within-image-component-div}

Se uma `<img>` tag com um url src absoluto for tentada para conversão de componente, um **UnsupportedTagContentException** apropriado será gerado. Por exemplo, o seguinte não é suportado:

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

Caso contrário, imagens de URL absolutas são compatíveis com tags img que não fazem parte da div do Componente de imagem.

### Componentes de chamada para ação {#call-to-action-components}

Você pode marcar parte da página de aterrissagem para importação como um &quot;componente de Chamada para ação editável&quot; - tais componentes de chamada para ação importados podem ser editados após a importação da página de aterrissagem. O AEM inclui os seguintes componentes do CTA:

* Link de clickthrough - permite adicionar um link de texto que, quando clicado, direciona o visitante a um URL.
* Link gráfico - permite adicionar uma imagem que, quando clicada, leva o visitante para um URL de destino.

#### Link de clickthrough {#click-through-link}

Este componente de CTA pode ser usado para adicionar um link de texto na página de aterrissagem.

Propriedades suportadas

* Rótulo, com negrito, itálico e opções de sublinhado
* URL de destino, compatível com o url de terceiros e AEM
* Opções de renderização de página (mesma janela, nova janela etc.)

Marca HTML para incluir o componente click through no zip importado. Aqui href mapeia para o url de destino, &quot;Exibir detalhes do produto&quot; mapeia para o rótulo e assim por diante.

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

**Declaração** abreviada de tag do componente:

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### Link gráfico {#graphical-link}

Esse componente de CTA pode ser usado para adicionar qualquer imagem gráfica com um link à página de aterrissagem. A imagem pode ser um simples botão ou qualquer imagem gráfica como fundo. Quando a imagem é clicada, o usuário será direcionado para o URL de destino especificado nas propriedades do componente. Ele faz parte do grupo “Frases de chamariz”.

Propriedades suportadas

* Recorte de imagem, rotação
* Texto de focalização, descrição, tamanho em px
* URL de destino, compatível com o url de terceiros e AEM
* Opções de renderização de página (mesma janela, nova janela etc.)

Marca HTML para incluir o componente de link gráfico no zip importado. Aqui, href mapeará para o URL de destino, img src será a imagem de renderização, &quot;título&quot; será tomado como texto flutuante e assim por diante.

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**Declaração** abreviada de tag do componente:

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>Para criar um link gráfico de cliques, é necessário vincular uma tag de âncora e a tag de imagem dentro de uma div com `data-cq-component="clickthroughgraphicallink"` atributo.
>
>ex. `<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>Outras maneiras de associar uma imagem a uma tag de âncora usando CSS não são suportadas, por exemplo, a seguinte marcação não funcionará:
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>com um `css .hasbackground { background-image: pathtoimage }`


### Formulário de lead {#lead-form}

Um formulário de lead é um formulário usado para coletar informações de perfil de um visitante/lead. Essas informações podem ser armazenadas e usadas posteriormente como base para realizar um marketing eficiente. Essas informações geralmente incluem título, nome, email, data de nascimento, endereço, interesse e assim por diante. Faz parte do grupo &quot;Formulário de cliente potencial&quot;.

**Recursos suportados**

* Campos de lead predefinidos - nome, sobrenome, endereço, dob, gênero, sobre, userId, emailId, botão Enviar estão disponíveis no sidekick. Basta arrastar/soltar o componente necessário no formulário de cliente potencial.
* Com a ajuda desses componentes, o autor pode criar um formulário de formulário de cliente potencial independente, esses campos correspondem aos campos de formulário de cliente potencial. No aplicativo zip independente ou importado, o usuário pode adicionar campos extras usando campos de formulário cq:form ou cta lead, nomear e projetar de acordo com os requisitos.
* Mapeie campos de formulário de cliente potencial usando nomes predefinidos específicos do formulário de cliente potencial CTA, por exemplo - firstName para nome próprio no formulário de cliente potencial, e assim por diante.
* Os campos que não estão mapeados para o formulário principal mapearão para cq:componentes de formulário - texto, rádio, caixa de seleção, lista suspensa, oculta, senha.
* O usuário pode fornecer o título usando a tag &quot;label&quot; e pode fornecer estilo usando o atributo de estilo &quot;class&quot; (disponível apenas para componentes de formulário de cliente potencial CTA).
* A página de agradecimento e a lista de assinaturas podem ser fornecidas como um parâmetro oculto do formulário (presente no index.htm) ou podem ser adicionadas/editadas na barra de edição de &quot;Início do formulário de cliente potencial&quot;

   &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-varejo/en/user/register/welcome_you&quot;/>

   &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* As restrições como - obrigatórias podem ser fornecidas a partir da configuração de edição de cada componente.

Marca HTML para incluir o componente de link gráfico no zip importado. Aqui, &quot;firstName&quot; é mapeado para o formulário lead firstName e assim por diante, exceto para caixas de seleção - essas duas caixas de seleção mapeiam para o componente suspenso cq:form.

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

O componente parsys do AEM é um componente de contêiner que pode conter outros componentes do AEM. É possível adicionar um componente parsys no HTML importado. Isso permite que o usuário adicione/exclua componentes editáveis do AEM à página de aterrissagem mesmo depois de ela ter sido importada.

O sistema de parágrafo oferece aos usuários a capacidade de adicionar componentes usando o sidekick.

Marcação HTML para inserir um componente parsys ( `foundation/components/parsys`) no HTML dentro do pacote de design:

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

A inclusão da marcação acima no HTML faz o seguinte:

* Insere um componente parsys do AEM (fundação/componentes/parsys) na página inicial criada após a importação do pacote de design.
* Inicializa o sidekick com componentes padrão. Novos componentes podem ser adicionados à página de aterrissagem arrastando os componentes do sidekick para o componente parsys.
* Dois componentes de título também fazem parte do parsys.

### Target {#target}

O componente de destino mostra o conteúdo de uma experiência na página. É possível ter muitas experiências criadas em uma campanha e o componente de destino pode mostrar dinamicamente o conteúdo de diferentes experiências para vários usuários que visitam a página.

A marcação html para inserir um componente de destino e também criar experiências diferentes em uma campanha:

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

Além de especificar se os componentes importados são componentes editáveis do AEM, você também pode configurar o seguinte antes de importar o pacote de design:

* Definir propriedades da página extraindo os metadados definidos no HTML importado.
* Especificação da codificação charset no HTML.
* Sobreposição do modelo de página do importador.

### Definição das propriedades da página extraindo metadados definidos no HTML importado {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

Os seguintes metadados declarados no cabeçalho do HTML importado serão extraídos e conservados pelo importador de desenhos como propriedade &quot;jcr:description&quot;:

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

O atributo lang definido na marca HTML deve ser extraído e preservado pelo importador de design como propriedade &quot;jcr:language&quot;

* &lt;html lang=&quot;en&quot;>

### Especificação da codificação charset no html {#specifying-the-charset-encoding-in-the-html}

O importador de design lê a codificação especificada no HTML importado. A codificação pode ser especificada da seguinte maneira:

`<meta charset="UTF-8">`

*OU*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

Se nenhuma codificação for especificada no HTML importado, a codificação padrão definida pelo importador de design será UTF-8.

### Sobreposição de modelo {#overlaying-template}

O modelo de Página inicial em branco pode ser sobreposto criando um novo em: `/apps/<appName>/designimporter/templates/<templateName>`

As etapas para criar um novo modelo no AEM são explicadas [aqui](/help/sites-developing/templates.md).

### Referência a um componente da página de aterrissagem {#referring-a-component-from-landing-page}

Suponha que você tenha um componente que deseja referenciar em seu HTML usando o atributo data-cq-component, de modo que o importador de design renderize um componente para incluir neste local. Por exemplo, você deseja fazer referência ao componente de tabela ( `resourceType = /libs/foundation/components/table`). O seguinte precisa ser adicionado ao HTML:

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

O caminho no componente data-cq-deve ser o resourceType do componente.

### Práticas recomendadas {#best-practices}

O uso de seletores de CSS semelhantes aos seguintes não é recomendado para uso com elementos marcados para conversão de componentes na importação.

| E > F | um elemento F filho de um elemento E | [Combinador filho](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | um elemento F imediatamente precedido de um elemento E | [Combinador irmão adjacente](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | um elemento F precedido de um elemento E | [Combinador irmão geral](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:root | um elemento E, raiz do documento | [Pseudo-classes estruturais](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:enth-child(n) | um elemento E, o n-ésimo filho do pai | [Pseudo-classes estruturais](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:enésimo último filho(n) | um elemento E, o n-ésimo filho do pai, contando do último | [Pseudo-classes estruturais](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:enth-of-type(n) | um elemento E, o n-ésimo irmão do seu tipo | [Pseudo-classes estruturais](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:enésimo último tipo(n) | um elemento E, o n-ésimo irmão do seu tipo, contando do último | [Pseudo-classes estruturais](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

Isso ocorre porque elementos html adicionais, como a tag &lt;div>, são adicionados ao Html gerado após a importação.

* Os scripts que dependem da estrutura semelhante a acima também não são recomendados para uso com elementos marcados para conversão em componentes do AEM.
* O uso de estilos nas tags de marcação para conversão de componentes, como &lt;div data-cq-component=&quot;&amp;ast;&quot;> não é recomendado.
* O layout de design deve seguir as práticas recomendadas do HTML5 Boilerplate. Leia mais sobre: [https://html5boilerplate.com/](https://html5boilerplate.com/).

## Configuração de módulos OSGI {#configuring-osgi-modules}

Os componentes que expõem propriedades configuráveis pelo console OSGI são os seguintes:

* Importador de design de página inicial
* Construtor de página de aterrissagem
* Construtor de página de aterrissagem móvel
* Pré-processador de entrada da página inicial

A tabela abaixo descreve as propriedades de forma breve:

<table>
 <tbody>
  <tr>
   <td><strong>Componente</strong></td>
   <td><strong>Nome da Propriedade</strong></td>
   <td><strong>Descrição da propriedade </strong></td>
  </tr>
  <tr>
   <td>Importador de design de página inicial</td>
   <td>Extrair filtro</td>
   <td>A lista de expressões regulares a serem usadas para filtrar arquivos da extração. <br /> As entradas de CEP que correspondem a qualquer um dos padrões especificados são excluídas da extração</td>
  </tr>
  <tr>
   <td>Construtor de página de aterrissagem</td>
   <td>Padrão de arquivo</td>
   <td>O Construtor de página inicial pode ser configurado para manipular arquivos HTML que correspondem a uma expressão regular conforme definido pelo padrão de arquivo.</td>
  </tr>
  <tr>
   <td>Construtor de página de aterrissagem móvel</td>
   <td>Padrão de arquivo</td>
   <td>O Construtor de página inicial pode ser configurado para manipular arquivos HTML que correspondem a uma expressão regular conforme definido pelo padrão de arquivo.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Grupos de dispositivos</td>
   <td>A lista de grupos de dispositivos a serem suportados.</td>
  </tr>
  <tr>
   <td>Pré-processador de entrada da página inicial</td>
   <td>Padrão de pesquisa </td>
   <td>O padrão a ser pesquisado no conteúdo da entrada do arquivo. Essa expressão regular corresponde à linha de conteúdo de entrada por linha. Após a correspondência, o texto correspondente é substituído pelo padrão de substituição especificado.<br /> <br /> Consulte a observação abaixo sobre as limitações atuais do pré-processador de entrada da página inicial.</td>
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
>**Limitação atual do pré-processador de entrada da página inicial:**
>Se precisar fazer alterações no padrão de pesquisa, ao abrir o editor de propriedades felix, é necessário adicionar manualmente caracteres de barra invertida para escapar dos metacaracteres regex. Se você não adicionar manualmente caracteres de barra invertida, o regex será considerado inválido e não substituirá o anterior.
>
>Por exemplo, se a configuração padrão for
>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>E você precisa substituir >`CQ_DESIGN_PATH` com `VIPURL` o padrão de pesquisa, seu padrão de pesquisa deve ser semelhante a:
`/\* *VIPURL *\*/ *(['"])`

## Resolução de Problemas{#troubleshooting}

Ao importar o pacote de design, você pode encontrar vários erros, descritos nesta seção.

### Inicialização do sidekick com componentes relevantes da página de aterrissagem {#initialization-of-sidekick-with-landing-page-relevant-components}

Se o pacote de design contiver uma marcação de componente parsys, depois da importação, o sidekick começará a mostrar componentes relevantes para a página de aterrissagem. Você pode arrastar e soltar novos componentes no componente parsys dentro da sua página inicial. Você também pode ir para o modo de design e adicionar novos componentes ao sidekick.

### Mensagens de erro exibidas durante a importação {#error-messages-displayed-during-import}

Em caso de erros (por exemplo, o pacote importado não é um zip válido), a importação de design não importará o pacote e exibirá uma mensagem de erro na parte superior da página logo acima da caixa de arrastar e soltar. Aqui são apresentados exemplos de cenários de erro. Depois de corrigir o erro, você pode importar novamente o zip atualizado para a mesma página inicial em branco. Os cenários diferentes em que são lançados erros são os seguintes:

* O pacote de design importado não é um arquivo zip válido.
* O pacote de design importado não contém index.html no nível superior.

### Avisos exibidos após a importação {#warnings-displayed-after-import}

No caso de avisos (por exemplo, HTML se refere a imagens que não existem no pacote), o importador de design importará o zip, mas ao mesmo tempo exibirá uma lista de problemas/avisos no Painel de resultados, ao clicar no link de problemas, exibirá uma lista de avisos que apontam quaisquer problemas no pacote de design. Os cenários diferentes em que os avisos são capturados e exibidos pelo importador de design são os seguintes:

* HTML refere-se a imagens que não existem no pacote.
* O HTML se refere a scripts que não existem no pacote.
* O HTML se refere a estilos que não existem no pacote.

### Onde os arquivos do arquivo ZIP estão sendo armazenados no AEM? {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

Depois que a página inicial for importada, os arquivos (imagens, css, js etc.) dentro do pacote de design são armazenados no seguinte local no AEM:

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

Suponha que a página de aterrissagem seja criada sob a campanha We.Retail e que o nome da página de aterrissagem seja **myBlankLandingPage** ; em seguida, o local onde os arquivos Zip são armazenados é o seguinte:

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

com um CSS aplicado na classe `box` como segue:

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

Em seguida, `box img` é usada no importador de design, a página inicial resultante parece não ter preservado a formatação. Para contornar isso, lembre-se de que o AEM adiciona tags div no CSS e regrava o código de acordo. Caso contrário, algumas regras CSS serão inválidas.

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
Além disso, os designers devem estar cientes de que somente o código dentro da tag **id=cqcanvas** é reconhecido pelo importador, caso contrário o design não é preservado.

