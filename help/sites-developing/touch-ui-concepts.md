---
title: Conceitos da interface de usuário habilitada para toque AEM
seo-title: Conceitos da interface de usuário habilitada para toque AEM
description: Com o AEM 5.6 Adobe introduziu uma nova interface otimizada ao toque com design responsivo para o ambiente do autor
seo-description: Com o AEM 5.6 Adobe introduziu uma nova interface otimizada ao toque com design responsivo para o ambiente do autor
uuid: 401c5a65-6ddc-4942-ab8e-395016f9c629
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: df3aaed1-97b5-4a4a-af74-cb887462475b
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '2197'
ht-degree: 0%

---


# Conceitos da interface de usuário habilitada para toque AEM{#concepts-of-the-aem-touch-enabled-ui}

AEM apresenta uma interface habilitada para toque com [design responsivo](/help/sites-authoring/responsive-layout.md) para o ambiente do autor, projetado para operar em dispositivos de toque e desktop.

>[!NOTE]
>
>A interface do usuário habilitada para toque é a interface padrão para AEM. A interface clássica foi substituída pela AEM 6.4.

A interface habilitada para toque inclui:

* O cabeçalho do conjunto que:
   * Mostra o logotipo
   * Fornece um link para a Navegação global
   * Fornece um link para outras ações genéricas; como Pesquisa, Ajuda, Soluções de Marketing Cloud, Notificações e Configurações do usuário.
* O painel esquerdo (exibido quando necessário e oculto), que pode mostrar:
   * Linha do tempo
   * Referências
   * Filtros
* O cabeçalho de navegação, que é novamente sensível ao contexto e pode mostrar:
   * Indica qual console você está usando no momento e/ou seu local dentro desse console
   * Seleção do painel esquerdo
   * Navegações estruturais
   * Acesso às ações **Create** apropriadas
   * Seleções de visualização
* A área de conteúdo que:
   * Lista os itens de conteúdo (sejam páginas, ativos, postagens do fórum etc.)
   * Pode ser formatado como solicitado, por exemplo, coluna, cartão ou lista
   * Usa um design responsivo (a tela é redimensionada automaticamente de acordo com o dispositivo e/ou o tamanho da janela)
   * Usa rolagem infinita (não há mais paginação, todos os itens são listados em uma janela)

![chlimage_1-79](assets/chlimage_1-79.png)

>[!NOTE]
>
>Quase toda a funcionalidade AEM foi portada para a interface habilitada para toque. No entanto, em alguns casos limitados, a funcionalidade reverterá para a interface clássica. Consulte [Touch UI Feature Status](/help/release-notes/touch-ui-features-status.md) para obter mais informações.

A interface do usuário habilitada para toque foi projetada pela Adobe para fornecer consistência na experiência do usuário em vários produtos. Baseia-se em:

* **A interface do usuário**  do Coral (CUI) é uma implementação do estilo visual do Adobe para a interface do usuário habilitada para toque. A interface do usuário do Coral fornece tudo o que seu produto / projeto / aplicativo da Web precisa para adotar o estilo visual da interface do usuário.
* **Os** componentes da interface do usuário Granite são criados com a interface do usuário Coral.

Os princípios básicos da interface habilitada para toque são:

* Primeiro móvel (com desktop em mente)
* Design responsivo
* Exibição relevante ao contexto
* Reutilizável
* Incluir documentação de referência incorporada
* Incluir testes incorporados
* Design inferior para garantir que esses princípios sejam aplicados a todos os elementos e componentes

Para obter mais uma visão geral da estrutura da interface habilitada para toque, consulte o artigo [Estrutura da interface habilitada para toque AEM](/help/sites-developing/touch-ui-structure.md).

## Pilha de tecnologia AEM {#aem-technology-stack}

AEM usa a plataforma Granite como base e a plataforma Granite inclui, entre outras coisas, o repositório de conteúdo Java.

![chlimage_1-80](assets/chlimage_1-80.png)

## Granite {#granite}

Granite é uma pilha de componentes Open Web que oferece:

* Um iniciador de aplicativo
* Uma estrutura OSGi na qual tudo é implantado
* Vários serviços de compêndio OSGi para apoiar a criação de aplicativos
* Uma estrutura de registro abrangente que fornece várias APIs de registro
* Implementação do repositório CRX da especificação da API JCR
* Apache Sling Web Framework
* Partes adicionais do produto CRX atual

>[!NOTE]
>
>Granite é executado como um projeto de desenvolvimento aberto dentro do Adobe: as contribuições para o código, discussões e questões são feitas em toda a empresa.
>
>No entanto, Granite é **e não** um projeto de código aberto. Ele é fortemente baseado em vários projetos de código aberto (Apache Sling, Felix, Jackrabbit e Lucene em particular), mas o Adobe traça uma linha clara entre o que é público e o que é interno.

## Interface do usuário Granite {#granite-ui}

A plataforma de engenharia Granite também fornece uma estrutura de interface de usuário básica. Os principais objetivos são:

* Fornecer widgets de interface granular
* Implemente os conceitos da interface do usuário e ilustre as práticas recomendadas (renderização de listas longas, filtragem de listas, CRUD de objetos, assistentes CUD...)
* Fornecer uma interface de usuário de administração extensível e baseada em plug-in

Eles atendem aos requisitos:

* Respeite &quot;celular primeiro&quot;
* Seja extensível
* Seja fácil de substituir

![chlimage_1-81](assets/chlimage_1-81.png)
GraniteUI.pdf

[Obter ](assets/graniteui.pdf)
arquivoA interface do usuário Granite:

* Usa a arquitetura RESTful da Sling
* Implementa bibliotecas de componentes destinadas à criação de aplicativos da Web centrados em conteúdo
* Fornece widgets de interface granular
* Fornece uma interface padrão e padronizada
* É extensível
* Foi projetado para dispositivos móveis e de desktop (primeiro para dispositivos móveis)
* Pode ser usado em qualquer plataforma/produto/projeto baseado em Granite; eg AEM

![chlimage_1-82](assets/chlimage_1-82.png)

* [Componentes ](#granite-ui-foundation-components)
da fundação da interface do usuário Granite Esta biblioteca de componentes da fundação pode ser usada ou estendida por outras bibliotecas.
* [Componentes de administração da interface do usuário Granite](#granite-ui-administration-components)

### Lado do cliente vs Lado do servidor {#client-side-vs-server-side}

A comunicação cliente-servidor na interface de usuário Granite consiste em hipertexto, não objetos, portanto não há necessidade de o cliente entender a lógica comercial

* O servidor enriquece o HTML com dados semânticos
* O cliente enriquece o hipertexto com a hipermídia (interação)

![chlimage_1-83](assets/chlimage_1-83.png)

#### Cliente {#client-side}

Isso usa uma extensão do vocabulário HTML, desde que o autor possa expressar sua intenção de criar um aplicativo Web interativo. Esta é uma abordagem semelhante para [WAI-ARIA](https://www.w3.org/TR/wai-aria/) e [microformatos](https://microformats.org/).

Consiste principalmente em uma coleção de padrões de interação (por exemplo, enviar um formulário de forma assíncrona) interpretados por códigos JS e CSS, executados no cliente. O papel do cliente é aprimorar a marcação (dada como o preço da hipermídia pelo servidor) para a interatividade.

O cliente é independente de qualquer tecnologia de servidor. Desde que o servidor forneça a marcação apropriada, o lado do cliente pode cumprir sua função.

Atualmente, os códigos JS e CSS são fornecidos como Granite [clientlibs](/help/sites-developing/clientlibs.md) na categoria:

`granite.ui.foundation and granite.ui.foundation.admin`

Eles são entregues como parte do pacote de conteúdo:

`granite.ui.content`

#### Lado do servidor {#server-side}

Isso é formado por uma coleção de componentes de sling que permitem ao autor *compor* um aplicativo da Web rapidamente. O desenvolvedor desenvolve componentes, o autor monta os componentes para serem um aplicativo da Web. A função do servidor é fornecer o preço da hipermídia (marcação) ao cliente.

Atualmente, os componentes estão localizados no repositório Granite em:

`/libs/granite/ui/components/foundation`

Isso é fornecido como parte do pacote de conteúdo:

`granite.ui.content`

### Diferenças com a interface clássica {#differences-with-the-classic-ui}

As diferenças entre a interface do usuário do Granite e o ExtJS (usado para a interface clássica) também são de interesse:

<table>
 <tbody>
  <tr>
   <td><strong>ExtJS</strong></td>
   <td><strong>Interface do usuário Granite</strong></td>
  </tr>
  <tr>
   <td>Chamada de procedimento remoto<br /> </td>
   <td>Transmissões estaduais</td>
  </tr>
  <tr>
   <td>Objetos de transferência de dados</td>
   <td>Hipermídia</td>
  </tr>
  <tr>
   <td>O cliente conhece os componentes internos do servidor</td>
   <td>O cliente não sabe internamente</td>
  </tr>
  <tr>
   <td>"Cliente Gordo"</td>
   <td>"Cliente fino"</td>
  </tr>
  <tr>
   <td>Bibliotecas especializadas de clientes</td>
   <td>Bibliotecas de clientes universais</td>
  </tr>
 </tbody>
</table>

### Componentes básicos da interface do usuário Granite {#granite-ui-foundation-components}

Os [componentes básicos da interface do usuário Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) fornecem os blocos básicos necessários para a construção de qualquer interface do usuário. Incluem, entre outros:

* Botão
* Hiperlink
* Avatar do usuário

Os componentes básicos podem ser encontrados em:

`/libs/granite/ui/components/foundation`

Esta biblioteca contém um componente de interface do usuário Granite para cada elemento Coral. Um componente é controlado por conteúdo, com sua configuração residindo no repositório. Isso possibilita a composição de um aplicativo de interface de usuário Granite sem gravar marcação HTML à mão.

Propósito:

* Modelo de componente para elementos HTML
* Composição do componente
* Teste automático de unidade e funcionalidade

Implementação:

* Composição e configuração baseadas em repositório
* Aproveitamento das instalações de teste fornecidas pela plataforma Granite
* Modelos JSP

Essa biblioteca de componentes da base pode ser usada ou estendida por outras bibliotecas.

### Componentes do ExtJS e da IU Granite Correspondente {#extjs-and-corresponding-granite-ui-components}

Ao atualizar o código ExtJS para usar a interface do usuário Granite, a lista a seguir fornece uma visão geral conveniente dos tipos xtypes e nós ExtJS com seus tipos de recursos equivalentes da interface do usuário Granite.

| **ExtJS xtype** | **Tipo de recurso da interface de usuário do Granite** |
|---|---|
| `button` | `granite/ui/components/foundation/form/button` |
| `checkbox` | `granite/ui/components/foundation/form/checkbox` |
| `componentstyles` | `cq/gui/components/authoring/dialog/componentstyles` |
| `cqinclude` | `granite/ui/components/foundation/include` |
| `datetime` | `granite/ui/components/foundation/form/datepicker` |
| `dialogfieldset` | `granite/ui/components/foundation/form/fieldset` |
| `hidden` | `granite/ui/components/foundation/form/hidden` |
| `html5smartfile, html5smartimage` | `granite/ui/components/foundation/form/fileupload` |
| `multifield` | `granite/ui/components/foundation/form/multifield` |
| `numberfield` | `granite/ui/components/foundation/form/numberfield` |
| `pathfield, paragraphreference` | `granite/ui/components/foundation/form/pathbrowser` |
| `selection` | `granite/ui/components/foundation/form/select` |
| `sizefield` | `cq/gui/components/authoring/dialog/sizefield` |
| `tags` | `granite/ui/components/foundation/form/autocomplete``cq/gui/components/common/datasources/tags` |
| `textarea` | `granite/ui/components/foundation/form/textarea` |
| `textfield` | `granite/ui/components/foundation/form/textfield` |

| **Tipo de nó** | **Tipo de recurso da interface de usuário do Granite** |
|---|---|
| `cq:WidgetCollection` | `granite/ui/components/foundation/container` |
| `cq:TabPanel` | `granite/ui/components/foundation/container``granite/ui/components/foundation/layouts/tabs` |
| `cq:panel` | `granite/ui/components/foundation/container` |

### Componentes de Administração da Interface do Usuário Granite {#granite-ui-administration-components}

Os [componentes de administração da interface de usuário Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) baseiam-se nos componentes básicos para fornecer blocos componentes genéricos que qualquer aplicativo de administração pode implementar. Estes incluem, entre outros:

* Barra de navegação global
* Painel (esqueleto)
* Painel de pesquisa

Propósito:

* Aparência unificada para aplicativos de administração
* RAD para aplicativos administrativos

Implementação:

* Componentes predefinidos usando os componentes básicos
* Os componentes podem ser personalizados

## Interface do usuário Coral {#coral-ui}

CoralUI.pdf

[A interface do usuário Get ](assets/coralui.pdf)
File Coral (CUI) é uma implementação do estilo visual Adobe para a interface do usuário habilitada para toque, que foi projetada para fornecer consistência na experiência do usuário em vários produtos. A interface do usuário do Coral fornece tudo o que você precisa para adotar o estilo visual usado no ambiente de criação.

>[!CAUTION]
>
>A interface do usuário Coral é uma biblioteca da interface do usuário disponibilizada para clientes AEM para criar aplicativos e interfaces da Web dentro dos limites do uso licenciado do produto.
>
>O uso da interface do coral é permitido apenas:
>
>
>* Quando tiver sido despachado e acompanhado de AEM.
>* Para uso ao estender a interface existente do ambiente de criação.
>* materiais de apoio corporativos, anúncios e apresentações do Adobe.
>* A interface do usuário de aplicativos da marca Adobe (a fonte não deve estar prontamente disponível para outros usos).
>* Com pequenas personalizações.

>
>
A utilização da interface do coral deve ser evitada em:
>
>* Documentos e outros itens não relacionados ao Adobe.
>* Ambientes de criação de conteúdo (onde os itens anteriores podem ser gerados por outros).
>* Aplicativos/componentes/páginas da Web que não estão claramente conectados ao Adobe.

>



A interface do usuário do Coral é uma coleção de elementos básicos para o desenvolvimento de aplicativos da Web.

![chlimage_1-84](assets/chlimage_1-84.png)

Projetado para ser modular a partir do start, cada módulo forma uma camada distinta com base em sua função primária. Embora as camadas tenham sido projetadas para oferecer suporte umas às outras, elas também podem ser usadas independentemente, se necessário. Isso permite implementar a experiência do usuário do Coral em qualquer ambiente compatível com HTML.

Com a interface do usuário Coral, não é obrigatório usar um modelo e/ou plataforma de desenvolvimento específico. O objetivo principal do Coral é fornecer marcação HTML5 unificada e limpa, independentemente do método real usado para emitir essa marcação. Isso pode ser usado para renderização do cliente ou do servidor, modelos, JSP, PHP ou até mesmo aplicativos RIA do Flash do Adobe - para nomear apenas alguns.

### Elementos HTML - A camada de marcação {#html-elements-the-markup-layer}

Os elementos HTML fornecem uma aparência comum para todos os elementos básicos da interface do usuário (incluindo barra de navegação, botão, menu, painel, entre outros).

No nível mais básico, um elemento HTML é uma tag HTML com um nome de classe dedicado. Elementos mais complexos podem ser compostos de várias tags, aninhadas entre si (de uma maneira específica).

O CSS é usado para fornecer a aparência real. Para facilitar a personalização da aparência (por exemplo, no caso da marca), os valores de estilo reais são declarados como variáveis que são expandidas pelo pré-processador [LESS](https://lesscss.org/) durante o tempo de execução.

Propósito:

* Fornecer elementos básicos da interface com aparência e comportamento comuns
* Fornecer o sistema de grade padrão

Implementação:

* Tags HTML com estilos inspirados por [bootstrap](https://twitter.github.com/bootstrap/)
* As classes são definidas em arquivos MENOS
* Os ícones são definidos como sprites de fonte

Por exemplo, a marcação:

```xml
<button class="btn btn-large btn-primary" type="button">Large button</button>
<button class="btn btn-large" type="button">Large button</button>
```

É exibido como:

![chlimage_1-85](assets/chlimage_1-85.png)

A aparência é definida em LESS, vinculada a um elemento por nome de classe dedicado (o seguinte extrato foi encurtado por uma questão de brevidade):

```xml
.btn {
    font-size: @baseFontSize;
    line-height: @baseLineHeight;
    .buttonBackground(@btnBackground,
                                @btnBackgroundHighlight,
                                @grayDark, 0 1px 1px rgba(255,255,255,.75));
```

Os valores reais são definidos em um arquivo de variável MENOS (o seguinte extrato foi encurtado por questões de brevidade):

```xml
@btnBackgroundHighlight: darken(@white, 10%);
@btnPrimaryBackgroundHighlight: spin(@btnPrimaryBackground, 20%);
@baseFontSize: 17px;
@baseFontFamily: @sansFontFamily;
```

### Plug-ins de elemento {#element-plugins}

Muitos dos elementos HTML precisarão exibir algum tipo de comportamento dinâmico, como abrir e fechar menus pop-up. Essa é a função dos plug-ins do elemento, que fazem essas tarefas manipulando o DOM usando o JavaScript.

Um plug-in é:

* Projetado para operar em um elemento DOM específico. Por exemplo, um plug-in de diálogo espera localizar `DIV class=dialog`
* Genérico na natureza. Por exemplo, um gerenciador de layout fornece layout para qualquer lista de elementos `DIV` ou `LI`

O comportamento do plug-in pode ser personalizado com parâmetros, por meio de:

* Passar os parâmetros por meio de uma chamada javascript
* Uso de atributos dedicados `data-*` ligados à marcação HTML

Embora o desenvolvedor possa selecionar a melhor abordagem para qualquer plug-in, a regra é usar:

* `data-*` para opções relacionadas ao layout HTML. Por exemplo, para especificar o número de colunas
* Opções/classes da API para funcionalidade relacionada aos dados. Por exemplo, construir a lista de itens a serem exibidos

O mesmo conceito é usado para implementar a validação do formulário. Para um elemento que você deseja validar, especifique o formulário de entrada necessário como um atributo `data-*` personalizado. Esse atributo é usado como uma opção para um plug-in de validação.

>[!NOTE]
>
>A validação de formulário nativo HTML5 deve ser usada sempre que possível e/ou ampliada.

Propósito:

* Fornecer comportamento dinâmico para elementos HTML
* Fornecer layouts personalizados não possíveis com CSS puro
* Executar validação de formulário
* Executar manipulação avançada de DOM

Implementação:

* Plug-in jQuery, vinculado a elementos DOM específicos
* Usar atributos `data-*` para personalizar o comportamento

Uma extração de marcação de exemplo (observe as opções especificadas como atributos data-*):

```xml
<ul data-column-width="220" data-layout="card" class="cards">
  <li class="item">
    <div class="thumbnail">
      <img href="/a.html" src="/a.thumb.319.319..png">
      <div class="caption">
        <h4>Toolbar</h4>
          <p><small>toolbar</small><br></p>
      </div>
    </div>
  </li>
  <li class="item">
    <div class="thumbnail">
      <img href="/a.html" src="/a.thumb.319.319..png">
      <div class="caption">
        <h4>Toolbar</h4>
        <p><small>toolbar</small><br></p>
      </div>
    </div>
  </li>
```

A chamada para o plug-in jQuery:

```
$(‘.cards’).cardlayout ();
```

Isso mostrará como:

![chlimage_1-86](assets/chlimage_1-86.png)

O plug-in `cardLayout` apresenta os elementos `UL` delimitados com base em suas respectivas alturas e também leva em consideração a largura do pai.

### Widgets de elementos HTML {#html-elements-widgets}

Um widget combina um ou mais elementos básicos com um plug-in javascript para formar elementos de UI de &quot;nível superior&quot;. Eles podem implementar um comportamento mais complexo e também uma aparência mais complexa do que um único elemento poderia oferecer. Exemplos bons são o seletor de tags ou os widgets de trilho.

Um widget pode acionar e ouvir eventos personalizados para cooperar com outros widgets na página. Alguns widgets são na verdade widgets nativos do jQuery que usam os elementos HTML Coral.

Propósito:

* Implemente elementos de interface de usuário de nível superior que exibem comportamento complexo
* Acionamento e manipulação de eventos

Implementação:

* Plug-in jQuery + marcação HTML
* Pode utilizar modelos do cliente/servidor

Exemplo de marcação é:

```
<input type="text" name="tags" placeholder="Tags" class="tagManager"/>
```

A chamada para o plug-in jQuery (com opções):

```
$(".tagManager").tagsManager({
        prefilled: ["Pisa", "Rome"] })
```

O plug-in emite marcação HTML (esta marcação usa elementos básicos, que podem usar outros plug-ins internamente):

```
<span>Pisa</code>
<a title="Removing tag" tagidtoremove="0"
   id="myRemover_0" class="myTagRemover" href="#">x</a></code>

<span id="myTag_1" class="myTag"><span>Rome</code>
<a title="Removing tag" tagidtoremove="1"
   id="myRemover_1" class="myTagRemover" href="#">x</a></code>

<input type="text" data-original-title="" class="input-medium tagManager"
       placeholder="Tags" name="tags" data-provide="typeahead" data-items="6"
       autocomplete="off">
```

Isso mostrará como:

![chlimage_1-87](assets/chlimage_1-87.png)

### Biblioteca de utilitários {#utility-library}

Esta biblioteca é uma coleção de plug-ins auxiliares javascript e/ou funções que são:

* Independente da interface
* No entanto, é fundamental para a criação de aplicativos da Web completos

Eles incluem o manuseio XSS e o barramento do evento.

Embora os plug-ins e os widgets do elemento HTML possam depender da funcionalidade fornecida pela biblioteca de utilitários, a biblioteca de utilitários não pode ter nenhuma dependência dos elementos nem dos próprios widgets.

Propósito:

* Fornecer funcionalidade comum
* Implementação do barramento do evento
* Modelos do cliente
* XSS

Implementação:

* Plug-ins jQuery ou módulos JavaScript compatíveis com AMD
