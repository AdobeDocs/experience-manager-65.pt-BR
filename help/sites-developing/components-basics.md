---
title: Componentes do AEM - Noções básicas
seo-title: Componentes do AEM - Noções básicas
description: Ao start para desenvolver novos componentes, você precisa entender as noções básicas de sua estrutura e configuração
seo-description: Ao start para desenvolver novos componentes, você precisa entender as noções básicas de sua estrutura e configuração
uuid: 0225b34d-5ac4-40c3-b226-0c9b24bdf782
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 1f9867f1-5089-46d0-8e21-30d62dbf4f45
legacypath: /content/docs/en/aem/6-0/develop/components/components-develop
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '4719'
ht-degree: 1%

---


# Componentes do AEM - Noções básicas{#aem-components-the-basics}

Ao start para desenvolver novos componentes, é necessário compreender as noções básicas de sua estrutura e configuração.

Esse processo envolve a leitura da teoria e a análise da ampla variedade de implementações de componentes em uma instância padrão do AEM. Essa última abordagem é um pouco complicada pelo fato de que, embora o AEM tenha mudado para uma nova interface padrão, moderna e habilitada para toque, ele continua a suportar a interface clássica.

## Visão geral {#overview}

Esta seção aborda os principais conceitos e problemas como uma introdução aos detalhes necessários ao desenvolver seus próprios componentes.

### Planejamento {#planning}

Antes de começar a configurar ou codificar seu componente, você deve perguntar:

* O que exatamente você precisa do novo componente para fazer?
   * Uma especificação clara ajuda em todas as etapas de desenvolvimento, teste e entrega. Os detalhes podem mudar com o tempo, mas a especificação pode ser atualizada (embora as alterações também devam ser documentadas).
* Você precisa criar seu componente do zero ou pode herdar as noções básicas de um componente existente?
   * Não há necessidade de reinventar a roda.
   * Existem vários mecanismos fornecidos pelo AEM para permitir que você herde e estenda detalhes de outra definição de componente, incluindo substituição, sobreposição e Fusão [de recursos do](/help/sites-developing/sling-resource-merger.md)Sling.
* Seu componente exigirá lógica para selecionar/manipular o conteúdo?
   * A lógica deve ser mantida separada da camada da interface do usuário. HTL foi projetado para ajudar a garantir que isso aconteça.
* Seu componente precisará de formatação CSS?
   * A formatação de CSS deve ser mantida separada das definições de componentes. Defina as convenções para nomear seus elementos HTML para que você possa modificá-los por meio de arquivos CSS externos.
* Que aspectos de segurança devo ter em consideração?
   * Consulte Lista de verificação de [segurança - Práticas](/help/sites-administering/security-checklist.md#development-best-practices) recomendadas de desenvolvimento para obter mais detalhes.

### Interface habilitada para toque vs clássica {#touch-enabled-vs-classic-ui}

Antes de qualquer start sério de discussão sobre o desenvolvimento de componentes, você precisa saber qual interface seus autores usarão:

* **Interface do usuário habilitada para toque**
   [A interface](/help/sites-developing/touch-ui-concepts.md) de usuário padrão é baseada na experiência de usuário unificada para o Adobe Marketing Cloud, usando as tecnologias subjacentes da interface de usuário [do](/help/sites-developing/touch-ui-concepts.md#coral-ui) Coral e da interface de usuário do [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui).
* **Interface clássica do** usuário com base na tecnologia ExtJS que foi substituída pelo AEM 6.4.

Consulte Recomendações da interface de [usuário para clientes](/help/sites-deploying/ui-recommendations.md) para obter mais detalhes.

Os componentes podem ser implementados para suportar a interface habilitada para toque, a interface clássica ou ambos. Ao observar uma instância padrão, você também verá componentes prontos para uso originalmente projetados para a interface clássica, para a interface habilitada para toque ou para ambos.

Por isso cobriremos as noções básicas de ambos, e como reconhecê-los, nesta página.

>[!NOTE]
>
>A Adobe recomenda aproveitar a interface habilitada para toque para se beneficiar da tecnologia mais recente. [Ferramentas e ferramentas de moderação do AEM (moderniatzion-tools.md) podem facilitar a migração.

### Lógica de conteúdo e marcação de renderização  {#content-logic-and-rendering-markup}

É recomendável manter o código responsável pela marcação e renderização separado do código que controla a lógica usada para selecionar o conteúdo do componente.

Essa filosofia é apoiada pelo [HTL](https://docs.adobe.com/content/help/br/experience-manager-htl/using/overview.html), uma linguagem de modelo que é propositadamente limitada para garantir que uma linguagem de programação real seja usada para definir a lógica comercial subjacente. Essa lógica (opcional) é chamada de HTL com um comando específico. Esse mecanismo realça o código chamado para uma determinada visualização e, se necessário, permite uma lógica específica para visualizações diferentes do mesmo componente.

### HTL vs JSP {#htl-vs-jsp}

HTL é uma linguagem de modelo HTML introduzida com o AEM 6.0.

A discussão sobre usar [HTL](https://docs.adobe.com/content/help/br/experience-manager-htl/using/overview.html) ou JSP (Java Server Pages) ao desenvolver seus próprios componentes deve ser simples, já que o HTL agora é a linguagem de script recomendada para o AEM.

HTL e JSP podem ser usados para desenvolver componentes para a interface clássica e habilitada para toque. Embora possa haver uma tendência de supor que o HTL seja apenas para a interface habilitada para toque e o JSP para a interface clássica, isso é um equívoco e mais devido à temporização. A interface do usuário habilitada para toque e o HTL foram incorporados ao AEM durante aproximadamente o mesmo período. Como o HTL agora é o idioma recomendado, ele está sendo usado para novos componentes, que tendem a ser para a interface habilitada para toque.

>[!NOTE]
>
>As exceções são Campos de formulário da Fundação da interface do usuário Granite (conforme usado em caixas de diálogo). Eles ainda exigem o uso do JSP.

### Desenvolver seus próprios componentes {#developing-your-own-components}

Para criar seus próprios componentes para a interface de usuário apropriada, consulte (após ler esta página):

* [Componentes do AEM para a interface habilitada para toque](/help/sites-developing/developing-components.md)
* [Componentes do AEM para a interface clássica](/help/sites-developing/developing-components-classic.md)

Uma maneira rápida de começar é copiar um componente existente e fazer as alterações desejadas. Para saber como criar seus próprios componentes e adicioná-los ao sistema de parágrafo, consulte:

* [Desenvolvimento de componentes](/help/sites-developing/developing-components-samples.md) (focados na interface habilitada para toque)

### Mover componentes para a instância de publicação {#moving-components-to-the-publish-instance}

Os componentes que renderizam o conteúdo devem ser implantados na mesma instância do AEM que o conteúdo. Portanto, todos os componentes usados para criar e renderizar páginas na instância do autor devem ser implantados na instância de publicação. Quando implantados, os componentes ficam disponíveis para renderizar páginas ativadas.

Use as seguintes ferramentas para mover seus componentes para a instância de publicação:

* [Use o Gerenciador](/help/sites-administering/package-manager.md) de pacotes para adicionar seus componentes a um pacote e movê-los para outra instância do AEM.
* [Use a ferramenta](/help/sites-authoring/publishing-pages.md#manage-publication) de replicação Ativar árvore para replicar os componentes.

>[!NOTE]
>
>Esses mecanismos também podem ser usados para transferir seu componente entre outras instâncias, por exemplo, do seu desenvolvimento para a sua instância de teste.

### Componentes a serem conhecidos do Start {#components-to-be-aware-of-from-the-start}

* Página:

   * O AEM tem o componente de *página* ( `cq:Page`).
   * Este é um tipo específico de recurso que é importante para a gestão de conteúdo.
      * Uma página corresponde a uma página da Web com conteúdo para seu site.

* Sistemas de parágrafo:

   * O sistema de parágrafo é uma parte essencial de um site, pois gerencia uma lista de parágrafos. É usado para manter e estruturar os componentes individuais que contêm o conteúdo real.
   * É possível criar, mover, copiar e excluir parágrafos no sistema de parágrafo.
   * Você também pode selecionar os componentes que estarão disponíveis para uso em um sistema de parágrafo específico.
   * Há vários sistemas de parágrafo disponíveis em uma instância padrão (por exemplo `parsys`, ` [responsivegrid](/help/sites-authoring/responsive-layout.md)`).

## Estrutura {#structure}

A estrutura de um componente AEM é poderosa e flexível, as principais considerações são:

* Tipo de recurso
* Definição do componente
* Propriedades e nós secundários de um componente
* Caixas de diálogo
* Caixas de diálogo de design
* Disponibilidade do componente
* Componentes e o conteúdo que eles criam

### Tipo de recurso {#resource-type}

Um elemento-chave da estrutura é o tipo de recurso.

* A estrutura de conteúdo declara intenções.
* O tipo de recurso os implementa.

Essa é uma abstração que ajuda a garantir que, mesmo quando a aparência muda com o tempo, a intenção fica no tempo.

### Definição do componente {#component-definition}

#### Noções básicas sobre componentes {#component-basics}

A definição de um componente pode ser dividida da seguinte forma:

* Os componentes do AEM são baseados no [Sling](https://sling.apache.org/documentation.html).
* Os componentes do AEM estão (normalmente) localizados em:

   * HTL: `/libs/wcm/foundation/components`
   * JSP: `/libs/foundation/components`

* Os componentes específicos do projeto/site estão (normalmente) localizados em:

   * `/apps/<myApp>/components`

* Os componentes padrão do AEM são definidos como `cq:Component` e têm os principais elementos:

   * propriedades do jcr:

      lista de propriedades jcr; são variáveis e algumas podem ser opcionais por meio da estrutura básica de um nó de componente, suas propriedades e subnós são definidos pela `cq:Component` definição

   * Recursos:

      Eles definem elementos estáticos usados pelo componente.

   * Scripts:

   São usados para implementar o comportamento da instância resultante do componente.

* **Nó raiz**:

   * `<mycomponent> (cq:Component)` - Nó de hierarquia do componente.

* **Propriedades** vitais:

   * `jcr:title` - Título do componente; por exemplo, usado como um rótulo quando o componente está listado no navegador de componentes ou sidekick.
   * `jcr:description` - Descrição do componente; pode ser usado como dica de mouse sobre o navegador de componentes ou sidekick.
   * Interface clássica:

      * `icon.png` - Ícone para este componente.
      * `thumbnail.png` - Imagem exibida se esse componente estiver listado no sistema de parágrafo.
   * Interface do usuário de toque

      * Consulte a seção Ícone [de componente na interface do usuário](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) de toque para obter detalhes.


* **Nós** de Crianças Vitais:

   * `cq:editConfig (cq:EditConfig)` - Define as propriedades de edição do componente e permite que o componente apareça no navegador Componentes ou no Sidekick.

      Observação: se o componente tiver uma caixa de diálogo, ele aparecerá automaticamente no navegador Componentes ou no Sidekick, mesmo se o cq:editConfig não existir.

   * `cq:childEditConfig (cq:EditConfig)` - Controla os aspectos da interface do usuário do autor para componentes filhos que não definem seus próprios `cq:editConfig`.
   * Interface do usuário habilitada para toque:

      * `cq:dialog` ( `nt:unstructured`) - Caixa de diálogo para este componente. Define a interface que permite ao usuário configurar o componente e/ou editar o conteúdo.
      * `cq:design_dialog` ( `nt:unstructured`) - Edição de design para este componente
   * Interface clássica:

      * `dialog` ( `cq:Dialog`) - Caixa de diálogo para este componente. Define a interface que permite ao usuário configurar o componente e/ou editar o conteúdo.
      * `design_dialog` ( `cq:Dialog`) - Edição de design para este componente.


#### Ícone de componente na interface de usuário de toque {#component-icon-in-touch-ui}

O ícone ou abreviação do componente é definido pelas propriedades do JCR do componente quando o componente é criado pelo desenvolvedor. Essas propriedades são avaliadas na seguinte ordem e a primeira propriedade válida encontrada é usada.

1. `cq:icon` - Propriedade String que aponta para um ícone padrão na biblioteca [de interface do usuário](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) Coral para exibir no navegador de componente
   * Use o valor do atributo HTML do ícone Coral.
1. `abbreviation` - Propriedade String para personalizar a abreviação do nome do componente no navegador do componente
   * A abreviação deve ser limitada a dois caracteres.
   * Fornecer uma string vazia criará a abreviação dos dois primeiros caracteres da `jcr:title` propriedade.
      * Por exemplo &quot;Im&quot; para &quot;Image&quot;
      * O título localizado será usado para criar a abreviação.
   * A abreviação só é traduzida se o componente tiver uma `abbreviation_commentI18n` propriedade, que é então usada como dica de tradução.
1. `cq:icon.png` ou `cq:icon.svg` - Ícone para este componente, que é mostrado no navegador do componente
   * 20 x 20 pixels é o tamanho dos ícones dos componentes padrão.
      * Os ícones maiores serão rebaixados (do lado do cliente).
   * A cor recomendada é rgb(112, 112, 112) > #707070
   * O plano de fundo dos ícones de componentes padrão é transparente.
   * Only `.png` and `.svg` files are supported.
   * Se importar do sistema de arquivos por meio do plug-in do Eclipse, os nomes de arquivo precisam ser salvos como `_cq_icon.png` ou `_cq_icon.svg` , por exemplo.
   * `.png` tem precedência sobre `.svg` se ambos estiverem presentes

Se nenhuma das propriedades acima ( `cq:icon`, `abbreviation`, `cq:icon.png` ou `cq:icon.svg`) for encontrada no componente:

* O sistema pesquisará as mesmas propriedades nos supercomponentes que seguem a `sling:resourceSuperType` propriedade.
* Se nada ou uma abreviação vazia for encontrada no nível do supercomponente, o sistema criará a abreviação das primeiras letras da `jcr:title` propriedade do componente atual.

Para cancelar a herança de ícones dos supercomponentes, definir uma `abbreviation` propriedade vazia no componente reverterá para o comportamento padrão.

O Console [de](/help/sites-authoring/default-components-console.md#component-details) componentes exibe como o ícone de um componente específico é definido.

#### Exemplo de ícone SVG {#svg-icon-example}

```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "https://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg version="1.1" id="Layer_1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" x="0px" y="0px"
     width="20px" height="20px" viewBox="0 0 20 20" enable-background="new 0 0 20 20" xml:space="preserve">
    <ellipse cx="5" cy="5" rx="3" ry="3" fill="#707070"/>
    <ellipse cx="15" cy="5" rx="4" ry="4" fill="#707070"/>
    <ellipse cx="5" cy="15" rx="5" ry="5" fill="#707070"/>
    <ellipse cx="15" cy="15" rx="4" ry="4" fill="#707070"/>
</svg>
```

### Propriedades e nós secundários de um componente {#properties-and-child-nodes-of-a-component}

Muitos dos nós/propriedades necessários para definir um componente são comuns a ambas as interfaces do usuário, com diferenças independentes que permanecem, para que seu componente possa funcionar em ambos os ambientes.

Um componente é um nó do tipo `cq:Component` e tem as seguintes propriedades e nós secundários:

<table>
 <tbody>
  <tr>
   <td><strong>Nome <br /> </strong></td>
   <td><strong>Tipo <br /> </strong></td>
   <td><strong>Descrição <br /> </strong></td>
  </tr>
  <tr>
   <td>.<br /> </td>
   <td><code>cq:Component</code></td>
   <td>Componente atual. Um componente é do tipo de nó <code>cq:Component</code>.<br /> </td>
  </tr>
  <tr>
   <td><code>componentGroup</code></td>
   <td><code>String</code></td>
   <td>Grupo no qual o componente pode ser selecionado no navegador Componentes (interface habilitada para toque) ou Sidekick (interface clássica).<br /> Um valor de <code>.hidden</code> é usado para componentes que não estão disponíveis para seleção na interface do usuário, como os sistemas de parágrafo reais.</td>
  </tr>
  <tr>
   <td><code>cq:isContainer</code></td>
   <td><code>Boolean</code></td>
   <td>Indica se o componente é um componente de container e, portanto, pode conter outros componentes, como um sistema de parágrafo.</td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:dialog</code></td>
   <td><code>nt:unstructured</code> </td>
   <td>Definição da caixa de diálogo de edição para a interface habilitada para toque.</td>
  </tr>
  <tr>
   <td><code>dialog</code></td>
   <td><code>cq:Dialog</code></td>
   <td>Definição da caixa de diálogo de edição para a interface clássica.</td>
  </tr>
  <tr>
   <td><code>cq:design_dialog</code></td>
   <td><code>nt:unstructured</code></td>
   <td>Definição da caixa de diálogo de design para a interface habilitada para toque.</td>
  </tr>
  <tr>
   <td><code>design_dialog</code></td>
   <td><code>cq:Dialog </code></td>
   <td>Definição da caixa de diálogo de design para a interface clássica.<br /> </td>
  </tr>
  <tr>
   <td><code>dialogPath</code></td>
   <td><code>String</code></td>
   <td>Caminho para uma caixa de diálogo para abranger o caso quando o componente não tem um nó de diálogo.<br /> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:cellName</code></td>
   <td><code>String</code></td>
   <td>Se definida, essa propriedade é assumida como ID de célula. Para obter mais informações, consulte o artigo da Base de conhecimento <a href="https://helpx.adobe.com/experience-manager/kb/DesigneCellId.html">Como as IDs de célula de design são criadas</a>.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:childEditConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td>Quando o componente é um container, como por exemplo um sistema de parágrafo, isso direciona a configuração de edição dos nós filhos.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:editConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td><a href="#edit-behavior">Edite a configuração do componente</a>.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:htmlTag</code></td>
   <td><code>nt:unstructured </code></td>
   <td>Retorna atributos de tag adicionais que são adicionados à tag html adjacente. Permite a adição de atributos aos divs gerados automaticamente.</td>
  </tr>
  <tr>
   <td><code>cq:noDecoration</code></td>
   <td><code>Boolean</code></td>
   <td>Se verdadeiro, o componente não é renderizado com classes div e css geradas automaticamente.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:template</code></td>
   <td><code>nt:unstructured</code></td>
   <td>Se encontrado, esse nó será usado como modelo de conteúdo quando o componente for adicionado do Navegador de componentes ou do Sidekick.</td>
  </tr>
  <tr>
   <td><code>cq:templatePath</code></td>
   <td><code>String</code></td>
   <td>Caminho para um nó para usar como modelo de conteúdo quando o componente for adicionado do navegador Componentes ou do Sidekick. Esse deve ser um caminho absoluto, não relativo ao nó do componente.<br /> A menos que você queira reutilizar conteúdo já disponível em outro lugar, isso não é obrigatório e <code>cq:template</code> é suficiente (veja abaixo).</td>
  </tr>
  <tr>
   <td><code>jcr:created</code></td>
   <td><code>Date</code></td>
   <td>Data de criação do componente.<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:description</code></td>
   <td><code>String</code></td>
   <td>Descrição do componente.<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:title</code></td>
   <td><code>String</code></td>
   <td>Título do componente.<br /> </td>
  </tr>
  <tr>
   <td><code>sling:resourceSuperType</code></td>
   <td><code>String</code></td>
   <td>Quando definido, o componente é herdado deste componente.<br /> </td>
  </tr>
  <tr>
   <td><code>virtual</code></td>
   <td><code>sling:Folder</code></td>
   <td>Permite a criação de componentes virtuais. Para ver um exemplo, consulte o componente de contato em:<br /> <code>/libs/foundation/components/profile/form/contact</code></td>
  </tr>
  <tr>
   <td><code>&lt;breadcrumb.jsp&gt;</code></td>
   <td><code>nt:file</code> </td>
   <td>Arquivo de script.<br /> </td>
  </tr>
  <tr>
   <td><code>icon.png</code></td>
   <td><code>nt:file</code></td>
   <td>O ícone do componente é exibido ao lado do Título no Sidekick.<br /> </td>
  </tr>
  <tr>
   <td><code>thumbnail.png</code></td>
   <td><code>nt:file</code></td>
   <td>Miniatura opcional que é mostrada enquanto o componente é arrastado do Sidekick para o local.<br /> </td>
  </tr>
 </tbody>
</table>

Se olharmos para o componente **Texto** (qualquer uma das versões), podemos ver estes elementos:

* HTL ( `/libs/wcm/foundation/components/text`)

   ![chlimage_1-241](assets/chlimage_1-241.png)

* JSP ( `/libs/foundation/components/text`)

   ![screen_shot_2012-02-13at60457pm](assets/screen_shot_2012-02-13at60457pm.png)

As propriedades de um interesse particular incluem:

* `jcr:title` - título do componente; isso pode ser usado para identificar o componente, por exemplo, ele aparece na lista do componente no navegador de componentes ou sidekick
* `jcr:description` - descrição do componente; pode ser usado como dica de mouse sobre a lista do componente dentro do sidekick
* `sling:resourceSuperType`: isso indica o caminho da herança ao estender um componente (substituindo uma definição)

Os nós secundários de interesse especial incluem:

* `cq:editConfig` ( `cq:EditConfig`) - controlo dos aspectos visuais; por exemplo, ele pode definir a aparência de uma barra ou de um widget ou pode adicionar controles personalizados
* `cq:childEditConfig` ( `cq:EditConfig`) - controla os aspectos visuais dos componentes filhos que não têm suas próprias definições
* Interface do usuário habilitada para toque:
   * `cq:dialog` ( `nt:unstructured`) - define a caixa de diálogo para editar o conteúdo deste componente
   * `cq:design_dialog` ( `nt:unstructured`) - especifica as opções de edição de design para este componente
* Interface clássica:
   * `dialog` ( `cq:Dialog`) - define a caixa de diálogo para editar o conteúdo deste componente (específico da interface clássica)
   * `design_dialog` ( `cq:Dialog`) - especifica as opções de edição de design para este componente
   * `icon.png` - arquivo gráfico a ser usado como ícone do componente no Sidekick
   * `thumbnail.png` - arquivo gráfico a ser usado como miniatura do componente enquanto o arrasta do Sidekick

### Caixas de diálogo {#dialogs}

As caixas de diálogo são um elemento chave do seu componente, pois fornecem uma interface para os autores configurarem e fornecerem informações para esse componente.

Dependendo da complexidade do componente, sua caixa de diálogo pode precisar de uma ou mais guias - para manter a caixa de diálogo curta e para classificar os campos de entrada.

As definições de caixa de diálogo são específicas para a interface do usuário:

>[!NOTE]
>
>* Para fins de compatibilidade, a interface do usuário habilitada para toque pode usar a definição de uma caixa de diálogo clássica, quando nenhuma caixa de diálogo tiver sido definida para a interface habilitada para toque.
>* A Ferramenta [de conversão de](/help/sites-developing/dialog-conversion.md) caixa de diálogo também é fornecida para ajudar a estender/converter componentes que tenham apenas diálogos definidos para a interface clássica.

>



* Interface do usuário habilitada para toque
   * `cq:dialog` ( `nt:unstructured`) nodes:
      * definir a caixa de diálogo para editar o conteúdo deste componente
      * específico da interface habilitada para toque
      * são definidos usando componentes da interface do usuário do Granite
      * tem uma propriedade `sling:resourceType`, como estrutura de conteúdo Sling padrão
      * pode ter uma propriedade `helpPath` para definir o recurso de ajuda sensível ao contexto (caminho absoluto ou relativo) que é acessado quando o ícone Ajuda (o ? ícone) está selecionado.
         * Para componentes prontos para uso, isso geralmente faz referência a uma página na documentação.
         * Se nenhum `helpPath` for especificado, o URL padrão (página de visão geral da documentação) será exibido.

   ![chlimage_1-242](assets/chlimage_1-242.png)

   Na caixa de diálogo, os campos individuais são definidos:

   ![screen_shot_2012-02-13at60937pm](assets/screen_shot_2012-02-13at60937pm.png)

* Interface do usuário clássica
   * `dialog` ( `cq:Dialog`) nodes
      * definir a caixa de diálogo para editar o conteúdo deste componente
      * específico da interface clássica
      * são definidos usando widgets ExtJS
      * têm uma propriedade `xtype`, que se refere a ExtJS
      * pode ter uma propriedade `helpPath` para definir o recurso de ajuda sensível ao contexto (caminho absoluto ou relativo) que é acessado quando o botão **Ajuda** é selecionado.
         * Para componentes prontos para uso, isso geralmente faz referência a uma página na documentação.
         * Se nenhum `helpPath` for especificado, o URL padrão (página de visão geral da documentação) será exibido.

   ![chlimage_1-243](assets/chlimage_1-243.png)

   Na caixa de diálogo, os campos individuais são definidos:

   ![chlimage_1-244](assets/chlimage_1-244.png)

   Em uma caixa de diálogo clássica:

   * é possível criar a caixa de diálogo como `cq:Dialog`, que fornecerá uma única guia - como no componente de texto, ou se você precisar de várias guias, como no componente de tempo de texto, a caixa de diálogo pode ser definida como `cq:TabPanel`.
   * uma `cq:WidgetCollection` ( `items`) é usada para fornecer uma base para os campos de entrada ( `cq:Widget`) ou para outras guias ( `cq:Widget`). Essa hierarquia pode ser estendida.


### Caixas de diálogo de design {#design-dialogs}

As caixas de diálogo de design são muito semelhantes às caixas de diálogo usadas para editar e configurar conteúdo, mas fornecem a interface para os autores configurarem e fornecerem detalhes de design para esse componente.

[As caixas de diálogo de design estão disponíveis no Modo](/help/sites-authoring/default-components-designmode.md)de design, embora não sejam necessárias para todos os componentes, por exemplo, **Título** e **Imagem** , ambos têm caixas de diálogo de design, enquanto **Texto** não.

A caixa de diálogo de design para o sistema de parágrafo (por exemplo, parsys) é um caso especial, pois permite que o usuário forneça outros componentes específicos para seleção (do navegador de componentes ou sidekick) na página.

### Adicionar seu componente ao sistema de parágrafo {#adding-your-component-to-the-paragraph-system}

Uma vez definido, um componente deve ser disponibilizado para uso. Para disponibilizar um componente para uso em um sistema de parágrafo, é possível:

1. Abra o Modo [de](/help/sites-authoring/default-components-designmode.md) design para uma página e ative o componente necessário.
1. Adicione os componentes necessários à propriedade `components` da definição do modelo em:

   `/etc/designs/<*yourProject*>/jcr:content/<*yourTemplate*>/par`

   Por exemplo, consulte:

   `/etc/designs/geometrixx/jcr:content/contentpage/par`

   ![chlimage_1-245](assets/chlimage_1-245.png)

### Componentes e o conteúdo que eles criam {#components-and-the-content-they-create}

Se criarmos e configurarmos uma instância do componente **Título** na página: `<content-path>/Prototype.html`

* Interface do usuário habilitada para toque

   ![chlimage_1-246](assets/chlimage_1-246.png)

* Interface do usuário clássica

   ![screen_shot_2012-02-01at34257pm](assets/screen_shot_2012-02-01at34257pm.png)

Em seguida, podemos ver a estrutura do conteúdo criado no repositório:

![screen_shot_2012-02-13at61405pm](assets/screen_shot_2012-02-13at61405pm.png)

Em particular, se você observar o texto real de um **Título**:

* a definição (para ambas as interfaces) tem a propriedade `name`= `./jcr:title`

   * `/libs/foundation/components/title/cq:dialog/content/items/column/items/title`
   * `/libs/foundation/components/title/dialog/items/title`

* dentro do conteúdo, isso gera a propriedade que `jcr:title` contém o conteúdo do autor.

As propriedades definidas dependem das definições individuais. Embora possam ser mais complexos do que acima, continuam a seguir os mesmos princípios básicos.

## Hierarquia e herança do componente {#component-hierarchy-and-inheritance}

Os componentes no AEM estão sujeitos a 3 hierarquias diferentes:

* **Hierarquia de Tipo de Recurso**

   Isso é usado para estender componentes usando a propriedade `sling:resourceSuperType`. Isso permite que o componente herde. Por exemplo, um componente de texto herdará vários atributos do componente padrão.

   * scripts (resolvidos pelo Sling)
   * diálogos
   * descrições (incluindo imagens em miniatura, ícones etc.)

* **Hierarquia do Container**

   Isso é usado para preencher as configurações para o componente filho e é usado com mais frequência em um cenário parsys.

   Por exemplo, as configurações dos botões da barra de edição, o layout do conjunto de controle (barras de edição, sobreposição), o layout da caixa de diálogo (em linha, flutuante) podem ser definidos no componente pai e propagados para os componentes filhos.

   As configurações (relacionadas à funcionalidade de edição) em `cq:editConfig` e `cq:childEditConfig` são propagadas.

* **Incluir hierarquia**

   Isso é imposto no tempo de execução pela sequência de inclusões.

   Essa hierarquia é usada pelo Designer, que, por sua vez, atua como a base para vários aspectos de design da renderização; incluindo informações de layout, informações de css, os componentes disponíveis em um parsys, entre outros.

## Editar comportamento {#edit-behavior}

Esta seção explica como configurar o comportamento de edição de um componente. Isso inclui atributos como ações disponíveis para o componente, características do editor local e ouvintes relacionados a eventos no componente.

A configuração é comum à interface habilitada para toque e clássica, embora com certas diferenças específicas.

O comportamento de edição de um componente é configurado adicionando um `cq:editConfig` nó do tipo `cq:EditConfig` abaixo do nó do componente (do tipo `cq:Component`) e adicionando propriedades e nós filhos específicos. As seguintes propriedades e nós secundários estão disponíveis:

* [ `cq:editConfig` propriedades](#configuring-with-cq-editconfig-properties)do nó:

   * `cq:actions` ( `String array`): define as ações que podem ser executadas no componente.
   * `cq:layout` ( `String`): : define como o componente é editado na interface clássica.
   * `cq:dialogMode` ( `String`): define como a caixa de diálogo do componente é aberta na interface clássica

      * Na interface habilitada para toque, as caixas de diálogo sempre flutuam no modo de desktop e são abertas automaticamente como tela cheia em dispositivos móveis.
   * `cq:emptyText` ( `String`): define o texto que é exibido quando nenhum conteúdo visual está presente.
   * `cq:inherit` ( `Boolean`): define se os valores ausentes são herdados do componente do qual são herdados.
   * `dialogLayout` (String): define como a caixa de diálogo deve ser aberta.


* [ `cq:editConfig` nós](#configuring-with-cq-editconfig-child-nodes)secundários:

   * `cq:dropTargets` (tipo de nó `nt:unstructured`): define uma lista de públicos alvos que podem aceitar uma queda de um ativo do localizador de conteúdo

      * Vários públicos alvos de soltar estão disponíveis somente na interface clássica.
      * Na interface habilitada para toque, um único público alvo é permitido.
   * `cq:actionConfigs` (tipo de nó `nt:unstructured`): define uma lista de novas ações que são anexadas à lista cq:actions.
   * `cq:formParameters` (tipo de nó `nt:unstructured`): define parâmetros adicionais que são adicionados ao formulário de diálogo.
   * `cq:inplaceEditing` (tipo de nó `cq:InplaceEditingConfig`): define uma configuração de edição local para o componente.
   * `cq:listeners` (tipo de nó `cq:EditListenersConfig`): define o que acontece antes ou depois de uma ação ocorrer no componente.


>[!NOTE]
>
>Nesta página, um nó (propriedades e nós filhos) é representado como XML, como mostrado no exemplo a seguir.

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:dialogMode="floating"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afteredit="REFRESH_PAGE"/>
</jcr:root>
```

Há muitas configurações existentes no repositório. Você pode pesquisar facilmente por propriedades específicas ou nós secundários:

* Procurar uma propriedade do `cq:editConfig` nó, por exemplo, `cq:actions`, você pode usar a ferramenta Query no **CRXDE Lite** e pesquisar com a seguinte string de query XPath:

   `//element(cq:editConfig, cq:EditConfig)[@cq:actions]`

* Para procurar por um nó filho de `cq:editConfig`, por exemplo, você pode pesquisar por `cq:dropTargets`, que é do tipo `cq:DropTargetConfig`; você pode usar a ferramenta Query em** CRXDE Lite** e pesquisar com a seguinte string de query XPath:

   `//element(cq:dropTargets, cq:DropTargetConfig)`

### Configuração com cq:EditConfig Properties {#configuring-with-cq-editconfig-properties}

### cq:actions {#cq-actions}

A `cq:actions` propriedade ( `String array`) define uma ou várias ações que podem ser executadas no componente. Os seguintes valores estão disponíveis para configuração:

<table>
 <tbody>
  <tr>
   <td><strong>Valor da propriedade</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td><code>text:&lt;some text&gt;</code></td>
   <td>Exibe o valor do texto estático &lt;some text&gt;<br /> visível somente na interface clássica. A interface de usuário habilitada para toque não exibe ações em um menu contextual, portanto isso não é aplicável.</td>
  </tr>
  <tr>
   <td>-</td>
   <td>Adiciona um espaçador.<br /> Visível somente na interface clássica. A interface de usuário habilitada para toque não exibe ações em um menu contextual, portanto isso não é aplicável.</td>
  </tr>
  <tr>
   <td><code>edit</code></td>
   <td>Adiciona um botão para editar o componente.</td>
  </tr>
      <tr>
    <td><code>editannotate</code></td>
    <td>Adiciona um botão para editar o componente e permitir <a href="/help/sites-authoring/annotations.md">anotações</a>.</td>
   </tr>
  <tr>
   <td><code>delete</code></td>
   <td>Adiciona um botão para excluir o componente</td>
  </tr>
  <tr>
   <td><code>insert</code></td>
   <td>Adiciona um botão para inserir um novo componente antes do componente atual</td>
  </tr>
  <tr>
   <td><code>copymove</code></td>
   <td>Adiciona um botão para copiar e recortar o componente.</td>
  </tr>
 </tbody>
</table>

A configuração a seguir adiciona um botão de edição, um espaçador, um botão de exclusão e um botão de inserção à barra de edição do componente:

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit,-,delete,insert]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig"/>
```

A configuração a seguir adiciona o texto &quot;Configurações herdadas da estrutura básica&quot; à barra de edição de componentes:

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[text:Inherited Configurations from Base Framework]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig"/>
```

### cq:layout (somente interface clássica) {#cq-layout-classic-ui-only}

A `cq:layout` propriedade ( `String`) define como o componente pode ser editado na interface clássica. Os seguintes valores estão disponíveis:

<table>
 <tbody>
  <tr>
   <td><strong>Valor da propriedade</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td><code>rollover</code></td>
   <td>Valor padrão. A edição do componente pode ser acessada "com o mouse sobre" por meio de cliques e/ou do menu de contexto.<br /> Para uso avançado, observe que o objeto correspondente do lado do cliente é: <code>CQ.wcm.EditRollover</code>.</td>
  </tr>
  <tr>
   <td><code>editbar</code></td>
   <td>A edição do componente é acessível por meio de uma barra de ferramentas.<br /> Para uso avançado, observe que o objeto correspondente do lado do cliente é: <code>CQ.wcm.EditBar</code>.</td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>A escolha é deixada ao código do lado do cliente.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Os conceitos de sobreposição e barra de edição não são aplicáveis na interface habilitada para toque.

A configuração a seguir adiciona um botão de edição à barra de edição do componente:

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
</jcr:root>
```

### cq:dialogMode (somente interface clássica) {#cq-dialogmode-classic-ui-only}

O componente pode ser vinculado a uma caixa de diálogo de edição. A `cq:dialogMode` propriedade ( `String`) define como a caixa de diálogo do componente será aberta na interface clássica. Os seguintes valores estão disponíveis:

<table>
 <tbody>
  <tr>
   <td><strong>Valor da propriedade</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td><code>floating</code></td>
   <td>A caixa de diálogo está flutuando.<br /> </td>
  </tr>
  <tr>
   <td><code>inline</code></td>
   <td>(Valor padrão). A caixa de diálogo está ancorada sobre o componente.<br /> </td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>Se a largura do componente for menor que o <code>CQ.themes.wcm.EditBase.INLINE_MINIMUM_WIDTH</code> valor do lado do cliente, a caixa de diálogo estará flutuando, caso contrário, estará em linha.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Na interface habilitada para toque, as caixas de diálogo sempre flutuam no modo de desktop e são abertas automaticamente como tela cheia em dispositivos móveis.

A configuração a seguir define uma barra de edição com um botão de edição e uma caixa de diálogo flutuante:

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:dialogMode="floating"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
</jcr:root>
```

### cq:emptyText {#cq-emptytext}

A `cq:emptyText` propriedade ( `String`) define o texto que é exibido quando nenhum conteúdo visual está presente. O padrão é: `Drag components or assets here`.

### cq:herdar {#cq-inherit}

A `cq:inherit` propriedade ( `boolean`) define se os valores ausentes são herdados do componente do qual são herdados. O padrão é `false`.

### dialogLayout {#dialoglayout}

A `dialogLayout` propriedade define como uma caixa de diálogo deve ser aberta por padrão.

* Um valor de `fullscreen` abre a caixa de diálogo em tela cheia.
* Um valor vazio ou a ausência da propriedade padroniza a abertura da caixa de diálogo normalmente.
* Observe que o usuário sempre pode alternar o modo de tela cheia na caixa de diálogo.
* Não se aplica à interface clássica.

### Configuração com cq:EditConfig Child Nodes {#configuring-with-cq-editconfig-child-nodes}

### cq:dropTargets {#cq-droptargets}

O `cq:dropTargets` nó (tipo de nó `nt:unstructured`) define uma lista de públicos alvos de soltar que podem aceitar uma queda de um ativo arrastado do localizador de conteúdo. Ela serve como uma coleção de nós do tipo `cq:DropTargetConfig`.

>[!NOTE]
>
>Vários públicos alvos de soltar estão disponíveis somente na interface clássica.
>
>Na interface habilitada para toque, somente o primeiro público alvo será usado.

Cada nó filho do tipo `cq:DropTargetConfig` define um público alvo de soltar no componente. O nome do nó é importante porque ele deve ser usado no JSP, da seguinte forma, para gerar o nome da classe CSS atribuído ao elemento DOM que é o público alvo de soltar efetivo:

```
<drop target css class> = <drag and drop prefix> +
 <node name of the drop target in the edit configuration>
```

A propriedade `<drag and drop prefix>` é definida pela propriedade Java:

`com.day.cq.wcm.api.components.DropTarget.CSS_CLASS_PREFIX`.

Por exemplo, o nome da classe é definido da seguinte forma no JSP do componente de Download( `/libs/foundation/components/download/download.jsp`), onde `file` é o nome do nó do público alvo solto na configuração de edição do componente de Download:

`String ddClassName = DropTarget.CSS_CLASS_PREFIX + "file";`

O nó do tipo `cq:DropTargetConfig` precisa ter as seguintes propriedades:

<table>
 <tbody>
  <tr>
   <td><strong>Nome da Propriedade</strong></td>
   <td><strong>Valor da propriedade<br /> </strong></td>
  </tr>
  <tr>
   <td><code>accept</code></td>
   <td>Regex aplicado ao tipo MIME do ativo para validar se o descarte é permitido.</td>
  </tr>
  <tr>
   <td><code>groups</code></td>
   <td>Matriz de grupos alvos. Cada grupo deve corresponder ao tipo de grupo definido na extensão do localizador de conteúdo e que está anexado aos ativos.</td>
  </tr>
  <tr>
   <td><code>propertyName</code></td>
   <td>Nome da propriedade que será atualizada após uma entrega válida.</td>
  </tr>
 </tbody>
</table>

A configuração a seguir é obtida do componente Download. Ela permite que qualquer ativo (o mime-type pode ser qualquer string) do `media` grupo seja descartado do localizador de conteúdo para o componente. Após a queda, a propriedade do componente `fileReference` é atualizada:

```
    <cq:dropTargets jcr:primaryType="nt:unstructured">
        <file
            jcr:primaryType="cq:DropTargetConfig"
            accept="[.*]"
            groups="[media]"
            propertyName="./fileReference"/>
    </cq:dropTargets>
```

### cq:actionConfigs (somente interface clássica) {#cq-actionconfigs-classic-ui-only}

O `cq:actionConfigs` nó (tipo de nó `nt:unstructured`) define uma lista de novas ações que são anexadas à lista definida pela `cq:actions` propriedade. Cada nó filho de `cq:actionConfigs` define uma nova ação definindo um widget.

A seguinte configuração de amostra define um novo botão (com um separador para a interface clássica):

* Um separador, definido pelo xtype `tbseparator`;

   * Isso é usado apenas pela interface clássica.
   * Essa definição é ignorada pela interface habilitada para toque, pois os xtypes são ignorados (e os separadores são desnecessários, pois a barra de ferramentas de ação é construída de forma diferente na interface habilitada para toque).

* um botão chamado **Gerenciar comentários** que executa a função de manipulador `CQ_collab_forum_openCollabAdmin()`.

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    cq:actions="[EDIT,COPYMOVE,DELETE,INSERT]"
    jcr:primaryType="cq:EditConfig">
    <cq:actionConfigs jcr:primaryType="nt:unstructured">
        <separator0
            jcr:primaryType="nt:unstructured"
            xtype="tbseparator"/>
        <manage
            jcr:primaryType="nt:unstructured"
            handler="function(){CQ_collab_forum_openCollabAdmin();}"
            text="Manage comments"/>
    </cq:actionConfigs>
</jcr:root>
```

>[!NOTE]
>
>Consulte [Adicionar nova ação a uma barra de ferramentas](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) de componente como um exemplo para a interface habilitada para toque.

### cq:formParameters {#cq-formparameters}

O `cq:formParameters` nó (tipo de nó `nt:unstructured`) define parâmetros adicionais que são adicionados ao formulário de diálogo. Cada propriedade é mapeada para um parâmetro de formulário.

A configuração a seguir adiciona um parâmetro chamado `name`, definido com o valor `photos/primary` para o formulário de diálogo:

```
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        name="photos/primary"/>
```

### cq:inplaceEditing {#cq-inplaceediting}

O `cq:inplaceEditing` nó (tipo de nó `cq:InplaceEditingConfig`) define uma configuração de edição local para o componente. Pode ter as seguintes propriedades:

<table>
 <tbody>
  <tr>
   <td><strong>Nome da Propriedade</strong></td>
   <td><strong>Valor da propriedade<br /> </strong></td>
  </tr>
  <tr>
   <td><code>active</code></td>
   <td>(<code>boolean</code>) Verdadeiro para permitir a edição local do componente.</td>
  </tr>
  <tr>
   <td><code>configPath</code></td>
   <td>(<code>String</code>) Caminho da configuração do editor. A configuração pode ser especificada por um nó de configuração.</td>
  </tr>
  <tr>
   <td><code>editorType</code></td>
   <td><p>(<code>String</code>) Tipo de editor. Os tipos disponíveis são:</p>
    <ul>
     <li>plaintext: a ser usado para conteúdo não HTML.<br /> </li>
     <li>título: é um editor de texto simples aprimorado que converte títulos gráficos em um texto simples antes do início da edição. Usado pelo componente de título do Geometrixx.<br /> </li>
     <li>texto: a ser usado para conteúdo HTML (usa o Editor de Rich Text).<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

A seguinte configuração permite a edição local do componente e define `plaintext` como o tipo de editor:

```
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### cq:ouvintes {#cq-listeners}

O `cq:listeners` nó (tipo de nó `cq:EditListenersConfig`) define o que acontece antes ou depois de uma ação no componente. A tabela a seguir define suas possíveis propriedades.

<table>
 <tbody>
  <tr>
   <td><strong>Nome da Propriedade</strong></td>
   <td><strong>Valor da propriedade<br /> </strong></td>
   <td><p><strong>Valor padrão</strong></p> <p>(Somente interface clássica)</p> </td>
  </tr>
  <tr>
   <td><code>beforedelete</code></td>
   <td>O manipulador é acionado antes da remoção do componente.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforeedit</code></td>
   <td>O manipulador é acionado antes da edição do componente.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforecopy</code></td>
   <td>O manipulador é acionado antes que o componente seja copiado.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforemove</code></td>
   <td>O manipulador é acionado antes de o componente ser movido.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforeinsert</code></td>
   <td>O manipulador é acionado antes de o componente ser inserido.<br /> Somente operacional para a interface habilitada para toque.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforechildinsert</code></td>
   <td>O manipulador é acionado antes que o componente seja inserido dentro de outro componente (somente container).</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>afterdelete</code></td>
   <td>O manipulador é acionado depois que o componente é removido.</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>afteredit</code></td>
   <td>O manipulador é acionado depois que o componente é editado.</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>aftercopy</code></td>
   <td>O manipulador é acionado depois que o componente é copiado.</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>afterinsert</code></td>
   <td>O manipulador é acionado depois que o componente é inserido.</td>
   <td><code>REFRESH_INSERTED</code></td>
  </tr>
  <tr>
   <td><code>aftermove</code></td>
   <td>O manipulador é acionado depois que o componente é movido.</td>
   <td><code>REFRESH_SELFMOVED</code></td>
  </tr>
  <tr>
   <td><code>afterchildinsert</code></td>
   <td>O manipulador é acionado depois que o componente é inserido dentro de outro componente (somente container).</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Os manipuladores `REFRESH_INSERTED` e `REFRESH_SELFMOVED` estão disponíveis somente na interface clássica.

>[!NOTE]
>
>Os valores padrão para os ouvintes são definidos somente na interface clássica.

>[!NOTE]
>
>No caso de componentes aninhados, há certas restrições em ações definidas como propriedades no `cq:listeners` nó:
>
>* Para componentes aninhados, os valores das seguintes propriedades *devem* ser `REFRESH_PAGE`: >
>  * `aftermove`
>  * `aftercopy`


O manipulador de eventos pode ser implementado com uma implementação personalizada. Por exemplo (onde `project.customerAction` é um método estático):

`afteredit = "project.customerAction"`

O exemplo a seguir equivale à `REFRESH_INSERTED` configuração:

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

>[!NOTE]
>
>Para a interface clássica, para ver quais parâmetros podem ser usados nos manipuladores, consulte a seção `before<action>` e `after<action>` eventos da documentação do [ widget `CQ.wcm.EditBar`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar) e do [ `CQ.wcm.EditRollover`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover) widget.

Com a seguinte configuração, a página é atualizada depois que o componente é excluído, editado, inserido ou movido:

```
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```
