---
title: Conceitos da interface habilitada para toque por AEM
seo-title: Concepts of the AEM Touch-Enabled UI
description: Com o AEM 5.6, o Adobe apresentou uma nova interface otimizada para toque com design responsivo para o ambiente de criação
seo-description: With AEM 5.6 Adobe introduced a new touch-optimized UI with responsive design for the author environment
uuid: 401c5a65-6ddc-4942-ab8e-395016f9c629
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: df3aaed1-97b5-4a4a-af74-cb887462475b
docset: aem65
exl-id: f13ac6c2-16ab-422d-9005-ab0b49172271
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2176'
ht-degree: 0%

---

# Conceitos da interface habilitada para toque por AEM{#concepts-of-the-aem-touch-enabled-ui}

O AEM apresenta uma interface habilitada para toque com [design responsivo](/help/sites-authoring/responsive-layout.md) para o ambiente de criação projetado para operar em dispositivos de toque e desktop.

>[!NOTE]
>
>A interface habilitada para toque é a interface padrão para AEM. A interface clássica foi descontinuada com o AEM 6.4.

A interface habilitada para toque inclui:

* O cabeçalho do conjunto que:
   * Mostra o logotipo
   * Fornece um link para a Navegação global
   * Fornece link para outras ações genéricas, como Pesquisa, Ajuda, Soluções do Marketing Cloud, Notificações e Configurações do usuário.
* O painel esquerdo (exibido quando necessário e oculto), que pode mostrar:
   * Linha do tempo
   * Referências
   * Filtros
* O cabeçalho de navegação, que novamente é sensível ao contexto e pode mostrar:
   * Indica qual console você está usando no momento e/ou seu local nesse console
   * Seleção para o painel esquerdo
   * Navegações estruturais
   * O acesso a **Criar** ações
   * Exibir seleções
* A área de conteúdo que:
   * Lista os itens de conteúdo (sejam páginas, ativos, publicações de fóruns etc.)
   * Pode ser formatado conforme solicitado, por exemplo, coluna, cartão ou lista
   * Usa um design responsivo (a tela é redimensionada automaticamente de acordo com o tamanho do dispositivo e/ou da janela)
   * Usa rolagem infinita (sem mais paginação, todos os itens são listados em uma janela)

![chlimage_1-79](assets/chlimage_1-79.png)

>[!NOTE]
>
>Quase toda a funcionalidade do AEM foi transferida para a interface habilitada para toque. No entanto, em alguns casos limitados, a funcionalidade reverterá para a interface clássica. Consulte [Status do recurso da interface de toque](/help/release-notes/touch-ui-features-status.md) para obter mais informações.

A interface habilitada para toque foi projetada pelo Adobe para fornecer consistência na experiência do usuário em vários produtos. Tem por base:

* **Coral UI** (CUI) uma implementação do estilo visual do Adobe para a interface habilitada para toque. A interface Coral fornece tudo o que seu produto/projeto/aplicativo Web precisa para adotar o estilo visual da interface.
* **Interface do Granite** Os componentes do são criados com a interface do Coral.

Os princípios básicos da interface habilitada para toque são:

* Mobilidade em primeiro lugar (com o desktop em mente)
* Design responsivo
* Exibição relevante ao contexto
* Reutilizável
* Incluir documentação de referência incorporada
* Incluir testes incorporados
* Design ascendente para garantir que esses princípios sejam aplicados a todos os elementos e componentes

Para obter mais uma visão geral da estrutura da interface habilitada para toque, consulte o artigo [Estrutura da interface habilitada para toque por AEM](/help/sites-developing/touch-ui-structure.md).

## Pilha de tecnologia AEM {#aem-technology-stack}

O AEM usa a plataforma Granite como base e a plataforma Granite inclui, entre outras coisas, o Repositório de conteúdo Java.

![chlimage_1-80](assets/chlimage_1-80.png)

## Granite {#granite}

O Granite é uma pilha da Web aberta do Adobe, que fornece vários componentes, incluindo:

* Um inicializador de aplicativos
* Uma estrutura OSGi na qual tudo é implantado
* Vários serviços de compêndio OSGi para dar suporte à criação de aplicativos
* Uma estrutura de log abrangente que fornece várias APIs de log
* A implementação do repositório CRX da especificação da API JCR
* A estrutura da Web do Apache Sling
* Partes adicionais do produto CRX atual

>[!NOTE]
>
>O Granite é executado como um projeto de desenvolvimento aberto no Adobe: contribuições para o código, discussões e problemas são feitas em toda a empresa.
>
>No entanto, o Granite é **não** um projeto de código aberto. É fortemente baseado em vários projetos de código aberto (Apache Sling, Felix, Jackrabbit e Lucene em particular), mas Adobe traça uma linha clara entre o que é público e o que é interno.

## Interface do Granite {#granite-ui}

A plataforma de engenharia do Granite também fornece uma estrutura básica de interface do usuário. Os principais objetivos são:

* Fornecer widgets granulares da interface do usuário
* Implementar os conceitos da interface do usuário e ilustrar as práticas recomendadas (renderização de listas longas, filtragem de listas, CRUD de objetos, assistentes de CUD...)
* Fornecer uma interface de administração extensível e baseada em plug-in

Eles atendem aos requisitos:

* Respeite &quot;móvel primeiro&quot;
* Ser extensível
* Ser fácil de substituir

![chlimage_1-81](assets/chlimage_1-81.png)
GraniteUI.pdf

[Obter arquivo](assets/graniteui.pdf)
A interface do Granite:

* Usa a arquitetura RESTful do Sling
* Implementa bibliotecas de componentes destinadas à criação de aplicativos da Web centrados em conteúdo
* Fornece widgets granulares da interface do usuário
* Fornece uma interface padrão e padronizada
* É extensível
* É projetado para dispositivos móveis e desktop (respeita dispositivos móveis primeiro)
* Pode ser usado em qualquer plataforma/produto/projeto baseado no Granite; por exemplo, AEM

![chlimage_1-82](assets/chlimage_1-82.png)

* [Componentes de base da interface de usuário do Granite](#granite-ui-foundation-components)
Essa biblioteca de componentes de base pode ser usada ou estendida por outras bibliotecas.
* [Componentes de administração da interface de usuário do Granite](#granite-ui-administration-components)

### Lado do cliente vs Lado do servidor {#client-side-vs-server-side}

A comunicação cliente-servidor na interface do Granite consiste em hipertexto, não em objetos, portanto, não há necessidade de o cliente entender a lógica de negócios

* O servidor enriquece o HTML com dados semânticos
* O cliente enriquece o hipertexto com a função hypermedia (interação)

![chlimage_1-83](assets/chlimage_1-83.png)

#### Lado do cliente {#client-side}

Isso usa uma extensão do vocabulário HTML, fornecida para que o autor possa expressar sua intenção de criar um aplicativo web interativo. Esta abordagem é semelhante à [WAI-ARIA](https://www.w3.org/TR/wai-aria/) e [microformatos](https://microformats.org/).

Consiste principalmente em uma coleção de padrões de interação (por exemplo, envio assíncrono de um formulário) que são interpretados por códigos JS e CSS, executados no lado do cliente. A função do lado do cliente é aprimorar a marcação (fornecida como o custo de hipermídia pelo servidor) para interatividade.

O lado do cliente é independente de qualquer tecnologia de servidor. Desde que o servidor forneça a marcação apropriada, o lado do cliente pode cumprir sua função.

Atualmente, os códigos JS e CSS são entregues como Granite [clientlibs](/help/sites-developing/clientlibs.md) na categoria:

`granite.ui.foundation and granite.ui.foundation.admin`

Eles são entregues como parte do pacote de conteúdo:

`granite.ui.content`

#### Lado do servidor {#server-side}

Isso é formado por uma coleção de componentes do sling que permitem que o autor *compor* um aplicativo da web rápido. O desenvolvedor desenvolve componentes, o autor monta os componentes para ser um aplicativo da Web. A função do lado do servidor é oferecer o preço acessível da hipermídia (marcação) ao cliente.

Atualmente, os componentes estão localizados no repositório do Granite em:

`/libs/granite/ui/components/foundation`

Isso é fornecido como parte do pacote de conteúdo:

`granite.ui.content`

### Diferenças com a interface clássica {#differences-with-the-classic-ui}

As diferenças entre a interface do Granite e a ExtJS (usada para a interface clássica) também são de interesse:

<table>
 <tbody>
  <tr>
   <td><strong>ExtJS</strong></td>
   <td><strong>Interface do Granite</strong></td>
  </tr>
  <tr>
   <td>Chamada de procedimento remoto<br /> </td>
   <td>Transições de Estado</td>
  </tr>
  <tr>
   <td>Objetos de transferência de dados</td>
   <td>Hipermídia</td>
  </tr>
  <tr>
   <td>O cliente conhece os recursos internos do servidor</td>
   <td>O cliente não conhece internos</td>
  </tr>
  <tr>
   <td>"Fat client"</td>
   <td>"Thin client"</td>
  </tr>
  <tr>
   <td>Bibliotecas de clientes especializadas</td>
   <td>Bibliotecas de clientes universais</td>
  </tr>
 </tbody>
</table>

### Componentes de base da interface de usuário do Granite {#granite-ui-foundation-components}

A variável [Componentes de base da interface do Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) O fornece os blocos de construção básicos necessários para criar qualquer interface do usuário. Incluem, entre outros:

* Botão
* Hiperlink
* Avatar do usuário

Os componentes de base podem ser encontrados em:

`/libs/granite/ui/components/foundation`

Esta biblioteca contém um componente de interface do usuário do Granite para cada elemento Coral. Um componente é orientado por conteúdo e sua configuração fica no repositório. Isso permite compor um aplicativo de interface do usuário do Granite sem gravar a marcação HTML manualmente.

Propósito:

* Modelo de componente para elementos de HTML
* Composição do componente
* Teste automático de unidade e funcionalidade

Implementação:

* Composição e configuração baseadas no repositório
* Aproveitamento das instalações de teste fornecidas pela plataforma Granite
* Modelos JSP

Essa biblioteca de componentes de base pode ser usada ou estendida por outras bibliotecas.

### ExtJS e componentes correspondentes da interface do Granite {#extjs-and-corresponding-granite-ui-components}

Ao atualizar o código ExtJS para usar a interface do Granite, a lista a seguir fornece uma visão geral conveniente dos tipos de nó e xtypes ExtJS com seus tipos de recursos equivalentes da interface do Granite.

| **ExtJS xtype** | **Tipo de recurso da interface do Granite** |
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

| **Tipo de nó** | **Tipo de recurso da interface do Granite** |
|---|---|
| `cq:WidgetCollection` | `granite/ui/components/foundation/container` |
| `cq:TabPanel` | `granite/ui/components/foundation/container``granite/ui/components/foundation/layouts/tabs` |
| `cq:panel` | `granite/ui/components/foundation/container` |

### Componentes de administração da interface de usuário do Granite {#granite-ui-administration-components}

A variável [Componentes de administração da interface do Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) aproveite os componentes básicos para fornecer blocos de construção genéricos que qualquer aplicativo de administração possa implementar. Estas incluem, entre outras:

* Barra de navegação global
* Trilho (esqueleto)
* Painel de pesquisa

Propósito:

* Aparência unificada para aplicativos de administração
* RAD para aplicativos de administração

Implementação:

* Componentes predefinidos usando os componentes de base
* Os componentes podem ser personalizados

## Coral UI {#coral-ui}

CoralUI.pdf

[Obter arquivo](assets/coralui.pdf)
A CUI (Coral UI) é uma implementação do estilo visual Adobe para a interface habilitada para toque, projetada para fornecer consistência na experiência do usuário em vários produtos. A interface do usuário do Coral fornece tudo o que você precisa para adotar o estilo visual usado no ambiente de criação.

>[!CAUTION]
>
>A Coral UI é uma biblioteca de interface do usuário disponibilizada para clientes AEM para a criação de aplicativos e interfaces da Web dentro dos limites do uso licenciado do produto.
>
>O uso da interface do Coral só é permitido:
>
>
>* Quando tiver sido enviado e empacotado com AEM.
>* Para uso ao estender a interface do usuário existente do ambiente de criação.
>* material de apoio, anúncios e apresentações da Adobe Corporate.
>* A interface do usuário dos aplicativos da marca Adobe (a fonte não deve estar prontamente disponível para outros usos).
>* Com pequenas personalizações.
>
>O uso da interface do Coral deve ser evitado em:
>
>* Documentos e outros itens não relacionados ao Adobe.
>* Ambientes de criação de conteúdo (em que os itens anteriores possam ser gerados por outros).
>* Aplicativos/componentes/páginas da Web que não estão claramente conectados ao Adobe.
>


A interface do Coral é uma coleção de blocos fundamentais para o desenvolvimento de aplicativos web.

![chlimage_1-84](assets/chlimage_1-84.png)

Projetado para ser modular desde o início, cada módulo forma uma camada distinta com base em sua função principal. Embora as camadas tenham sido projetadas para suportar umas às outras, elas também podem ser usadas independentemente, se necessário. Isso permite implementar a experiência do usuário do Coral em qualquer ambiente com capacidade para HTML.

Com a interface do Coral, não é obrigatório usar um modelo e/ou plataforma de desenvolvimento específico. O objetivo principal do Coral é fornecer marcação de HTML5 unificada e limpa, independentemente do método real usado para emitir essa marcação. Isso pode ser usado para renderização do lado do cliente ou do servidor, templates, JSP, PHP ou até mesmo aplicativos RIA de Flash de Adobe - para citar apenas alguns.

### Elementos de HTML - A Camada de Marcação {#html-elements-the-markup-layer}

Os elementos HTML fornecem uma aparência comum para todos os elementos básicos da interface do usuário (incluindo barra de navegação, botão, menu, painel, entre outros).

No nível mais básico, um elemento HTML é uma tag HTML com um nome de classe dedicado. Elementos mais complexos podem ser compostos de várias tags, aninhadas entre si (de uma maneira específica).

O CSS é usado para fornecer a aparência real. Para facilitar a personalização da aparência e comportamento (por exemplo, no caso de marca), os valores de estilo reais são declarados como variáveis, que são expandidas pela variável [MENOS](https://lesscss.org/) pré-processador durante o tempo de execução.

Propósito:

* Fornecer elementos básicos da interface do usuário com aparência comum
* Fornecer o sistema de grade padrão

Implementação:

* tags HTML com estilos inspirados em [bootstrap](https://twitter.github.com/bootstrap/)
* As classes são definidas em arquivos LESS
* Os ícones são definidos como sprites de fonte

Por exemplo, a marcação:

```xml
<button class="btn btn-large btn-primary" type="button">Large button</button>
<button class="btn btn-large" type="button">Large button</button>
```

É exibido como:

![chlimage_1-85](assets/chlimage_1-85.png)

A aparência é definida em MENOS, vinculado a um elemento por nome de classe dedicado (o seguinte extrato foi encurtado por motivos de brevidade):

```xml
.btn {
    font-size: @baseFontSize;
    line-height: @baseLineHeight;
    .buttonBackground(@btnBackground,
                                @btnBackgroundHighlight,
                                @grayDark, 0 1px 1px rgba(255,255,255,.75));
```

Os valores reais são definidos em um arquivo de variável LESS (a seguinte extração foi encurtada por motivos de brevidade):

```xml
@btnBackgroundHighlight: darken(@white, 10%);
@btnPrimaryBackgroundHighlight: spin(@btnPrimaryBackground, 20%);
@baseFontSize: 17px;
@baseFontFamily: @sansFontFamily;
```

### Plug-ins de elementos {#element-plugins}

Muitos dos elementos de HTML precisarão exibir algum tipo de comportamento dinâmico, como menus pop-up de abertura e fechamento. Essa é a função dos plug-ins de elementos, que realizam essas tarefas manipulando o DOM usando JavaScript.

Um plug-in pode ser:

* Projetado para operar em um elemento DOM específico. Por exemplo, um plug-in de diálogo espera encontrar `DIV class=dialog`
* Natureza genérica. Por exemplo, um gerenciador de layout fornece layout para qualquer lista de `DIV` ou `LI` elementos

O comportamento do plug-in pode ser personalizado com parâmetros, através:

* Passagem dos parâmetros por meio de uma chamada de javascript
* Uso de dedicado `data-*` atributos vinculados à marcação HTML

Embora o desenvolvedor possa selecionar a melhor abordagem para qualquer plug-in, a regra geral é usar:

* `data-*` atributos para opções relacionadas ao layout HTML. Por exemplo, para especificar o número de colunas
* Opções/classes de API para funcionalidade relacionada aos dados. Por exemplo, criar a lista de itens para exibir

O mesmo conceito é usado para implementar a validação de formulários. Para um elemento que você deseja validar, você deve especificar o formulário de entrada necessário como um personalizado `data-*` atributo. Esse atributo é usado como uma opção para um plug-in de validação.

>[!NOTE]
>
>A validação do formulário nativo HTML5 deve ser usada sempre que possível e/ou expandida.

Propósito:

* Fornecer comportamento dinâmico para elementos de HTML
* Não é possível fornecer layouts personalizados com CSS puro
* Executar validação
* Executar manipulação de DOM avançada

Implementação:

* Plug-in jQuery, vinculado a elementos DOM específicos
* Usar `data-*` atributos para personalizar o comportamento

Uma extração de marcação de exemplo (observe as opções especificadas como data-&#42; atributos):

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

Isso será exibido como:

![chlimage_1-86](assets/chlimage_1-86.png)

A variável `cardLayout` O plug-in apresenta o `UL` elementos com base nas respectivas alturas e tendo também em conta a largura do pai.

### Widgets de elementos do HTML {#html-elements-widgets}

Um widget combina um ou mais elementos básicos com um plug-in javascript para formar elementos de interface do usuário de &quot;nível superior&quot;. Eles podem implementar comportamentos mais complexos e também uma aparência mais complexa do que um único elemento pode oferecer. Bons exemplos são o seletor de tags ou os widgets do painel.

Um widget pode acionar e ouvir eventos personalizados para cooperar com outros widgets na página. Alguns widgets são widgets nativos do jQuery que usam os elementos HTML Coral.

Propósito:

* Implementar elementos de interface do usuário de nível superior que exibam comportamento complexo
* Acionamento e manuseio de eventos

Implementação:

* Plug-in jQuery + marcação HTML
* Pode utilizar modelos do lado do cliente/servidor

Exemplo de marcação:

```
<input type="text" name="tags" placeholder="Tags" class="tagManager"/>
```

A chamada para o plug-in jQuery (com opções):

```
$(".tagManager").tagsManager({
        prefilled: ["Pisa", "Rome"] })
```

O plug-in emite a marcação HTML (essa marcação usa elementos básicos, que podem usar outros plug-ins internamente):

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

Isso será exibido como:

![chlimage_1-87](assets/chlimage_1-87.png)

### Biblioteca do utilitário {#utility-library}

Esta biblioteca é uma coleção de plug-ins e/ou funções de ajuda do javascript que são:

* Independente da interface
* No entanto, é fundamental para a criação de aplicativos web completos

Isso inclui a manipulação de XSS e o barramento de evento.

Embora os plug-ins e widgets do elemento HTML possam depender da funcionalidade fornecida pela biblioteca de utilitários, esta não pode ter nenhuma dependência rígida em relação aos elementos nem aos próprios widgets.

Propósito:

* Fornecer funcionalidade comum
* Implementação do barramento de evento
* Modelos do lado do cliente
* XSS

Implementação:

* Plug-ins do jQuery ou módulos JavaScript compatíveis com AMD
