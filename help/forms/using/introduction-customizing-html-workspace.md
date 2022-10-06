---
title: Introdução à Personalização AEM espaço de trabalho de formulário
seo-title: Introduction to Customizing AEM form workspace
description: Uma introdução rápida, com informações conceituais e técnicas, para personalizar a área de trabalho do LiveCycle AEM Forms para o gerenciamento de processos.
seo-description: A quick introduction, with conceptual and technical information, to customize LiveCycle AEM Forms workspace for process management.
uuid: 38759071-e6b8-4976-8b06-909ad7a786cd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 021c6606-8cd3-472c-a80b-b1bcace7e87f
docset: aem65
exl-id: b183d42f-343c-4acb-bc73-f80ad72e54df
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 0%

---

# Introdução à Personalização AEM espaço de trabalho de formulário{#introduction-to-customizing-aem-form-workspace}

AEM espaço de trabalho de formulário fornece recursos para modificar a semântica de apresentação e a funcionalidade de sua interface. Os tipos de personalizações para alterar o estilo, layout, formatação, marca e funcionalidade principal estão descritos abaixo.

![cu_customized_workspace_example](assets/cu_customized_workspace_example.png)

Um exemplo de um espaço de trabalho personalizado

## Tipos de personalizações {#types-of-customizations}

A área de trabalho do AEM Forms é compatível com uma grande variedade de personalizações para atualizar o layout da interface do usuário, sua aparência, funcionalidade e muito mais. As personalizações envolvem a atualização de um ou mais dos seguintes itens:

* Aspectos da interface do usuário
* Funcionalidade usando personalizações semânticas
* Reutilização de componentes HTML em outros aplicativos

### Alterações na interface do usuário {#user-interface-changes}

Você pode alterar a aparência, o layout e outras semânticas de apresentação do espaço de trabalho do AEM Forms. Altere o espaço de trabalho personalizando os arquivos CSS, HTML e JavaScript™. Todos os arquivos padrão são fornecidos na instalação padrão.

As etapas mais comumente aplicáveis são abordadas no [Etapas genéricas para personalização do espaço de trabalho do AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Para obter exemplos específicos dessas personalizações, incluindo as etapas detalhadas, consulte os artigos relacionados no final deste artigo.

#### Como entender a folha de estilos {#understanding-the-style-sheet}

Antes de personalizar o espaço de trabalho, familiarize-se com a folha de estilos padrão fornecida com o AEM Forms em /libs/ws/css/style.css.

Para personalizar o espaço de trabalho, é recomendável que você se familiarize com a folha de estilos existente, style.css, localizada na pasta /libs/ws/css. Alguns componentes de destaque estão descritos abaixo.

<table>
 <tbody>
  <tr>
   <th><p>Elemento CSS</p> </th>
   <th><p>Componente da interface do usuário modificado</p> </th>
  </tr>
  <tr>
   <td><p>#cabeçalho</p> </td>
   <td><p>Cabeçalho do espaço de trabalho do AEM Forms</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList</p> </td>
   <td><p>Lista de categorias</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList .header</p> </td>
   <td><p>Cabeçalho da lista de categorias</p> </td>
  </tr>
  <tr>
   <td><p>.categories, .filters</p> </td>
   <td><p>Espaço abaixo da lista de categorias</p> </td>
  </tr>
  <tr>
   <td><p>.category, .filter</p> </td>
   <td><p>Categoria</p> </td>
  </tr>
  <tr>
   <td><p>.category:hover, .category.seleted, .filter:hover, .filter.seleted</p> </td>
   <td><p>Categoria selecionada e passar o mouse sobre o estilo da categoria</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar .tool, categoryListBar .content</p> </td>
   <td><p>Página Iniciar processo (lista de Categoria fechada)</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar .tool, filterListBar .content</p> </td>
   <td><p>Página de Tarefas Pendentes (lista de Filtros fechada)</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar .tool, processNameListBar .content</p> </td>
   <td><p>Página de rastreamento (lista fechada de nomes de Processo)</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList, .tasklist</p> </td>
   <td><p>A lista de pontos de partida ou a lista de tarefas</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList .header, .tasklist .header</p> </td>
   <td><p>O cabeçalho de uma lista de pontos de partida ou de uma lista de tarefas</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.seleted, .task.seleted</p> </td>
   <td><p>O ponto de partida ou a tarefa selecionada</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.seleted .description, .task.seleted .description</p> </td>
   <td><p>Descrição do ponto de partida ou da tarefa selecionada</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>A área Tarefa</p> </td>
  </tr>
  <tr>
   <td><p>#header.drop-down</p> </td>
   <td><p>Menu suspenso do usuário no cabeçalho</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>Lista suspensa Classificar tarefa</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

A aparência do espaço de trabalho do AEM Forms recebe sua aparência de um CSS. Ao personalizar o CSS, é possível alterar a semântica de apresentação do espaço de trabalho, como fontes, cores, marcas e layout.

As etapas de nível superior para personalização de CSS são:

* Crie um arquivo CSS.
* Adicione itens de estilo a este CSS. Consulte Entendendo os estilos de CSS para obter mais informações.
* Atualize suas referências em `html.jsp`.

Para obter as etapas exatas para fazer essas personalizações, consulte [Etapas genéricas para personalização do espaço de trabalho do AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). O arquivo CSS enviado com o espaço de trabalho do AEM Forms está em /libs/ws/css/. Para personalizações relacionadas a CSS, use o [Envio](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p). Para obter exemplos específicos de personalizações relacionadas ao CSS, consulte os tópicos de Ajuda relacionados no final deste artigo.

#### Imagem {#image}

Você pode personalizar a área de trabalho do AEM Forms para adicionar avatares de usuários ou adicionar o logotipo de sua organização. Para essas personalizações, use [Envio](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p).

As etapas de nível superior para personalizações das imagens são:

* Instale e configure o WebDAV.
* Adicione novas imagens.
* Adicione novos estilos correspondentes às imagens adicionadas.
* Link para o novo arquivo CSS em `html.jsp` arquivo.

Para começar a personalizar as imagens na área de trabalho do AEM Forms, siga as [Etapas genéricas para personalização do espaço de trabalho do AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Para obter exemplos específicos de personalizações relacionadas à imagem, consulte os tópicos de Ajuda relacionados no final deste artigo.

#### modelo HTML {#html-template}

Os templates de HTML ajudam a definir a aparência e o layout da interface do usuário do espaço de trabalho. Ao atualizar os templates HTML padrão, é possível personalizar a interface de usuário padrão do layout.

As etapas de nível superior para personalizações no modelo de HTML são:

* Em uma pasta criada pelo usuário, faça cópias dos arquivos padrão necessários.
* Adicione novos templates na pasta definida pelo usuário.
* Faça atualizações relevantes nos arquivos copiados, como o caminho do novo modelo.

Para obter exemplos específicos dessas personalizações, consulte os tópicos de Ajuda fornecidos no final deste artigo. Escolha entre as [Envio](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) ou [Pacote de desenvolvimento](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p), dependendo do modelo a ser personalizado.

### Alterações semânticas {#semantic-changes}

Para modificar a funcionalidade do espaço de trabalho do AEM Forms, altere o código-fonte do JavaScript. As modificações na funcionalidade principal são rotuladas como Alterações semânticas. Você modifica modelos, visualizações e modelos fornecidos como parte do código-fonte do espaço de trabalho do AEM Forms.

As etapas de nível superior para fazer alterações semânticas para modificar a funcionalidade do espaço de trabalho do AEM Forms são:

* Em uma pasta criada pelo usuário, faça cópias dos arquivos padrão apropriados.
* Adicione novos modelos e visualizações na pasta definida pelo usuário.
* Faça atualizações relevantes, como atualizar caminhos de modelos e visualizações recém-adicionados nos arquivos JavaScript padrão.
* Reduza o pacote para otimizar o desempenho.

Para obter mais informações conceituais sobre os componentes que fazem parte do código-fonte, consulte o [Descrição dos componentes reutilizáveis](/help/forms/using/description-reusable-components.md). Para essas personalizações, use o Pacote de desenvolvimento.

### Componentes reutilizáveis {#reusable-components}

Como o AEM Forms workspace é um software baseado em componentes, ele pode ser facilmente personalizado e reutilizado. É possível integrar facilmente os componentes do espaço de trabalho com seus aplicativos Web.

Para obter mais informações conceituais, consulte a [Descrição dos componentes reutilizáveis](/help/forms/using/description-reusable-components.md) e para obter instruções sobre como usar os componentes, consulte [Integração de componentes do espaço de trabalho do AEM Forms em aplicativos da Web](/help/forms/using/description-reusable-components.md).

## Criação do código do espaço de trabalho do AEM Forms {#building-html-workspace-code}

### Pacote SDK {#sdk-package}

O pacote contém o código-fonte do espaço de trabalho do AEM Forms. O pacote está disponível em `[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`.

Destina-se principalmente a personalizações, pois fornece a capacidade de gerar:

* Pacotes CRX para perfis de Entrega, Depuração e Desenvolvimento (mencionados abaixo em [Pacotes CRX](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)).
* Versão reduzida do código personalizado (para alterações semânticas).

#### Conteúdo WS {#ws-content}

* client-pkg:

   * src - Contém artefatos necessários para criar nós CRX.
   * pom.xml - script para criar pacotes de implantação para vários perfis WS-Depload Package

* client-html:

   * assembly - Contém zip.xml usado pelo script para criar o SDK do espaço de trabalho do AEM Forms.
   * src/main/webapp -

      * css - Contém folhas de estilos para o espaço de trabalho do AEM Forms.
      * imagens - Contém imagens usadas na área de trabalho do AEM Forms.
      * js:

         * libs - Contém todas as bibliotecas de terceiros usadas no AEM Forms workspace.
         * licenças - contém licenças para arquivos HTML e JS, bem como código para prefixar essas licenças para os respectivos arquivos de origem.
         * minificador - Usado para combinação, minificação e certificação do código JavaScript personalizado.
         * resourcejs_otimizer - Usado para combinação, minificação e correção da origem do JavaScript.
         * resource_generator - Usado para gerar register.js e modelcontrollerpath.js.
         * tempo de execução:

            * initializer - Contém initializer.js usado para inicializar exibições de backbone e modelos usados no AEM Forms workspace.
            * Modelos - contém modelos de backbone de todos os componentes presentes no espaço de trabalho do AEM Forms.
            * rotas - Contém arquivos JavaScript e HTML que carregam processos de início, tarefas, rastreamento e preferências no espaço de trabalho AEM Forms.
            * services - Contém service.js usado no espaço de trabalho do AEM Forms. Todas as chamadas do servidor são feitas por meio de service.js.
            * modelos - Contém todos os modelos, ou seja, arquivos HTML de todas as exibições no espaço de trabalho do AEM Forms.
            * util - Contém todos os arquivos de utilitário (javascript) que são usados no AEM Forms workspace.
            * exibições - contém exibições de backbone de todos os componentes no espaço de trabalho do AEM Forms.
         * main.js
         * router.js
      * libs/ws: pdf.html e pluginPing.pdf são usados para carregar PDF forms no espaço de trabalho do AEM Forms e WSNextAdapter.swf é usado para carregar formulários e guias SWF no espaço de trabalho do AEM Forms.
      * localidades:

         * de-DE - Contém translation.json para alemão.
         * en-US - Contém translation.json para inglês.
         * fr-FR - Contém translation.json para francês.
         * ja-JP - Contém translation.json para japonês.
         * html.jsp - Contém código para descobrir a localidade atual do navegador.
      * html.jsp
      * GET.jsp




### Pacote CRX {#crx-package}

O pacote CRX pode ser implantado no repositório CRX™. Está disponível em `[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`.

Este pacote pode ser criado usando os três perfis descritos abaixo.

| **Perfil** | **Descrição** | **Uso** |
|---|---|---|
| Perfil de envio | Esse perfil cria um pacote CRX do menor tamanho possível usando minificação. Este pacote é o mais eficiente. Todos os arquivos JavaScript™ são combinados e minificados em um único arquivo JS. | Use esse perfil quando não forem necessárias mais alterações semânticas nos arquivos JS. |
| Depurar perfil | Esse perfil cria um pacote CRX moderadamente eficiente. O tamanho do pacote é ligeiramente maior do que o pacote criado usando o perfil de Entrega. Esse pacote tem a maioria dos arquivos JavaScript combinados em um único arquivo JS. | Use esse perfil para depuração. |
| Perfil de desenvolvimento | Esse perfil cria um pacote CRX do maior tamanho possível. Todos os arquivos JavaScript estão disponíveis separadamente, pois estão no pacote SDK. | Use esse perfil ao incorporar alterações semânticas. |

#### Perfil de Entrega {#ship-profile}

#### Comando {#command}

* mvn clean -P Enviar instalação na pasta client-pkg do pacote de origem enviado ao cliente.
* A execução do comando de perfil de remessa funciona somente em uma JVM de 64 bits.

#### Conteúdo WS {#ws-content-1}

* css - Contém style.css, ie.css e jquery-ui.css.
* imagens - Contém todas as imagens.
* js:

   * libs:

      * require - Contém require.js.
      * jqueryui - Contém jquery.ui.datepicker.ja.js.
   * tempo de execução:

      * modelos - Contém todos os modelos, ou seja, arquivos HTML de todos os componentes no espaço de trabalho do AEM Forms.
   * main.js (combinado, minificado e certificado).
   * registry.js



* libs:

   * ws - Contém pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Locale - Contém .content.xml.
* localidades:

   * de-DE - Contém translation.json para alemão.
   * en-US - Contém translation.json para inglês.
   * fr-FR - Contém translation.json para francês.
   * ja-JP - Contém translation.json para japonês.
   * html.jsp - Contém código para descobrir a localidade atual do navegador.

* Índice - Contém .content.xml
* profile - Contém offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Perfil de depuração {#debug-profile}

#### Comando {#command-1}

* mvn clean -P Debug install em client-pkg
* A execução do comando do perfil de depuração funciona somente na JVM de 64 bits.

#### Conteúdo WS {#ws-content-2}

* css - Contém style.css, ie.css e jqueri-ui.css.
* imagens - Contém todas as imagens.
* js:

   * libs:

      * require - Contém require.js.
      * jqueryui - Contém jquery.ui.datepicker.ja.js.
   * tempo de execução:

      * modelos - Contém todos os modelos, ou seja, arquivos HTML de todos os componentes no espaço de trabalho do AEM Forms.
   * main.js (combinado).
   * registry.js



* libs:

   * ws - Contém pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Locale - Contém .content.xml.
* localidades:

   * de-DE - Contém translation.json para alemão.
   * en-US - Contém translation.json para inglês.
   * fr-FR - Contém translation.json para francês.
   * ja-JP - Contém translation.json para japonês.
   * html.jsp - Contém código para descobrir a localidade atual do navegador.

* Índice - Contém .content.xml
* profile - Contém offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Perfil de desenvolvimento {#dev-profile}

#### Comando {#command-2}

mvn clean -P Dev install no client-pkg

#### Conteúdo WS {#ws-content-3}

* css - Contém style.css, ie.css e jqueri-ui.css.
* imagens - Contém todas as imagens.
* js:

   * libs - Contém todas as bibliotecas usadas na área de trabalho do AEM Forms.
   * obrigatório - Contém require.js
   * jqueryui - Contém jquery.ui.datepicker.ja.js
   * tempo de execução:

      * initializer - Contém initializer.js e modelcontrollerpath.js.
      * modelos - Contém modelos de todos os componentes no espaço de trabalho do AEM Forms.
      * rotas - Contém arquivos JavaScript e HTML que carregam processos de início, tarefas, rastreamento e preferências no espaço de trabalho AEM Forms.
      * services - Contém service.js usado no espaço de trabalho do AEM Forms.
      * modelos - Contém todos os modelos, ou seja, arquivos HTML de todos os componentes no espaço de trabalho do AEM Forms.
      * util - Contém todos os arquivos de utilitário (JavaScript) que são usados no AEM Forms workspace.
      * exibições - contém exibições de todos os componentes no espaço de trabalho do AEM Forms.
   * main.js
   * registry.js
   * router.js


* libs:

   * ws - Contém pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Locale - Contém .content.xml.
* localidades:

   * de-DE - Contém translation.json para alemão.
   * en-US - Contém translation.json para inglês.
   * fr-FR - Contém translation.json para francês.
   * ja-JP - Contém translation.json para japonês.
   * html.jsp - Contém código para descobrir a localidade atual do navegador.

* Índice - Contém .content.xml
* profile - Contém offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml
