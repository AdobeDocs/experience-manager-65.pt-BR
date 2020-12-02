---
title: Introdução à Personalização AEM espaço de trabalho do formulário
seo-title: Introdução à Personalização AEM espaço de trabalho do formulário
description: Uma introdução rápida, com informações conceituais e técnicas, para personalizar a área de trabalho do LiveCycle AEM Forms para gerenciamento de processos.
seo-description: Uma introdução rápida, com informações conceituais e técnicas, para personalizar a área de trabalho do LiveCycle AEM Forms para gerenciamento de processos.
uuid: 38759071-e6b8-4976-8b06-909ad7a786cd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 021c6606-8cd3-472c-a80b-b1bcace7e87f
docset: aem65
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '1786'
ht-degree: 0%

---


# Introdução à Personalização AEM espaço de trabalho do formulário{#introduction-to-customizing-aem-form-workspace}

AEM espaço de trabalho do formulário fornece recursos para modificar a semântica e a funcionalidade da apresentação de sua interface. Os tipos de personalizações para alterar o estilo, o layout, a formatação, a marca e a funcionalidade principal estão descritos abaixo.

![cu_customized_workspace_example](assets/cu_customized_workspace_example.png)

Um exemplo de um espaço de trabalho personalizado

## Tipos de personalizações {#types-of-customizations}

A área de trabalho do AEM Forms oferece suporte a uma grande variedade de personalizações para atualizar o layout da interface do usuário, sua aparência, funcionalidade e muito mais. As personalizações envolvem a atualização de um ou mais dos seguintes:

* Aparências da interface do usuário
* Funcionalidade usando personalizações semânticas
* Reutilização de componentes HTML em outros aplicativos

### Alterações na interface do usuário {#user-interface-changes}

Você pode alterar a aparência, o layout e outras semânticas de apresentação da área de trabalho do AEM Forms. Altere o espaço de trabalho personalizando os arquivos CSS, HTML e JavaScript™. Todos os arquivos padrão são fornecidos na instalação padrão.

As etapas mais comumente aplicáveis são abordadas em [Etapas genéricas para personalização do espaço de trabalho AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Para obter exemplos específicos dessas personalizações, incluindo as etapas detalhadas, consulte os artigos relacionados no final deste artigo.

#### Como entender a folha de estilos {#understanding-the-style-sheet}

Antes de personalizar o espaço de trabalho, familiarize-se com a folha de estilos padrão fornecida com a AEM Forms em /libs/ws/css/style.css.

Para personalizar o espaço de trabalho, é recomendável que você se familiarize com a folha de estilos existente, style.css, localizada na pasta /libs/ws/css. Descreve - se a seguir alguns componentes de relevo.

<table>
 <tbody>
  <tr>
   <th><p>Elemento CSS</p> </th>
   <th><p>Componente da interface do usuário modificado</p> </th>
  </tr>
  <tr>
   <td><p>#cabeçalho</p> </td>
   <td><p>Cabeçalho da área de trabalho do AEM Forms</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList</p> </td>
   <td><p>Lista categoria</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList .header</p> </td>
   <td><p>Cabeçalho da lista da categoria</p> </td>
  </tr>
  <tr>
   <td><p>.categoria, .filtros</p> </td>
   <td><p>Espaço abaixo da lista da categoria</p> </td>
  </tr>
  <tr>
   <td><p>.categoria, .filter</p> </td>
   <td><p>Categoria</p> </td>
  </tr>
  <tr>
   <td><p>.categoria:pairar, .categoria.seleted, .filter:pairar, .filter.seleted</p> </td>
   <td><p>Categoria e mouse sobre o estilo de categoria selecionados</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar .tool, categoryListBar .content</p> </td>
   <td><p>Página de processo de start (lista fechada)</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar .tool, filterListBar .content</p> </td>
   <td><p>Página de Tarefas Pendentes (lista de Filtro Fechado)</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar .tool, processNameListBar .content</p> </td>
   <td><p>Página de rastreamento (lista de nome de processo fechada)</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList, .tasklist</p> </td>
   <td><p>A lista do ponto de partida ou a lista da tarefa</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList .header, .tasklist .header</p> </td>
   <td><p>O cabeçalho de uma lista de ponto de partida ou de uma lista de tarefa</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.seleted, .tarefa.seleted</p> </td>
   <td><p>O ponto de partida ou a tarefa selecionada</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.seleted .description, .tarefa.seleted .description</p> </td>
   <td><p>Descrição do ponto de partida ou tarefa selecionado</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>Área da Tarefa</p> </td>
  </tr>
  <tr>
   <td><p>#header.dropdown</p> </td>
   <td><p>Menu suspenso do usuário no cabeçalho</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>Lista suspensa Classificar tarefa</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

A aparência da área de trabalho do AEM Forms recebe sua aparência de um CSS. Ao personalizar o CSS, é possível alterar a semântica de apresentação do espaço de trabalho, como fontes, cores, marcas e layout.

As etapas de nível superior para personalização de CSS são:

* Crie um arquivo CSS.
* Adicione itens de estilo a este CSS. Consulte Entendendo estilos CSS para obter mais informações.
* Atualize suas referências em `html.jsp`.

Para obter as etapas exatas para fazer essas personalizações, consulte [Etapas genéricas para personalização do espaço de trabalho AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). O arquivo CSS fornecido com a área de trabalho da AEM Forms está em /libs/ws/css/. Para personalizações relacionadas a CSS, use o [Pacote de remessa](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p). Para obter exemplos específicos de personalizações relacionadas ao CSS, consulte os tópicos de Ajuda relacionados no final deste artigo.

#### Imagem {#image}

Você pode personalizar a área de trabalho do AEM Forms para adicionar avatares de usuários ou para adicionar o logotipo de sua organização. Para essas personalizações, use [Envio de pacote](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p).

As etapas de nível superior para personalizações das imagens são:

* Instale e configure o WebDAV.
* Adicione novas imagens.
* Adicione novos estilos correspondentes às imagens adicionadas.
* Link para o novo arquivo CSS no arquivo `html.jsp`.

Para começar a personalizar as imagens na área de trabalho do AEM Forms, siga as [etapas genéricas para personalização da área de trabalho do AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Para obter exemplos específicos de personalizações relacionadas à imagem, consulte os tópicos de Ajuda relacionados no final deste artigo.

#### Modelo HTML {#html-template}

Os modelos HTML ajudam a definir a aparência e o layout da interface do usuário do espaço de trabalho. Ao atualizar os modelos HTML padrão, você pode personalizar a interface de usuário padrão do layout.

As etapas de nível superior para personalizações no modelo HTML são:

* Em uma pasta criada pelo usuário, faça cópias dos arquivos padrão necessários.
* Adicione novos modelos na pasta definida pelo usuário.
* Faça atualizações relevantes para os arquivos copiados, como o caminho do novo modelo.

Para obter exemplos específicos dessas personalizações, consulte os tópicos de Ajuda fornecidos no final deste artigo. Escolha entre o [Pacote de Entrega](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) ou [Pacote de Desenvolvimento](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p), dependendo do modelo a ser personalizado.

### Alterações semânticas {#semantic-changes}

Para modificar a funcionalidade do espaço de trabalho do AEM Forms, altere o código-fonte do JavaScript. As modificações na funcionalidade principal são rotuladas como alterações semânticas. Você modifica modelos, visualizações e modelos fornecidos como parte do código-fonte da área de trabalho do AEM Forms.

As etapas de nível superior para fazer alterações semânticas para modificar a funcionalidade da área de trabalho do AEM Forms são:

* Em uma pasta criada pelo usuário, faça cópias dos arquivos padrão apropriados.
* Adicione novos modelos e visualizações na pasta definida pelo usuário.
* Faça atualizações relevantes, como atualizar caminhos de modelos e visualizações recém-adicionados nos arquivos JavaScript padrão.
* Reduza o pacote para otimizar o desempenho.

Para obter mais informações conceituais sobre os componentes que fazem parte do código-fonte, consulte [Descrição de componentes reutilizáveis](/help/forms/using/description-reusable-components.md). Para essas personalizações, use o Pacote de desenvolvedores.

### Componentes reutilizáveis {#reusable-components}

Como o espaço de trabalho AEM Forms é um software baseado em componentes, ele pode ser facilmente personalizado e reutilizado. Você pode integrar facilmente os componentes da área de trabalho com seus aplicativos da Web.

Para obter mais informações conceituais, consulte [Descrição de componentes reutilizáveis](/help/forms/using/description-reusable-components.md) e para obter instruções sobre como usar os componentes, consulte [Integração de componentes do espaço de trabalho AEM Forms em aplicativos da Web](/help/forms/using/description-reusable-components.md).

## Criando código de espaço de trabalho AEM Forms {#building-html-workspace-code}

### Pacote SDK {#sdk-package}

O pacote contém o código-fonte da área de trabalho do AEM Forms. O pacote está disponível em `[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`.

Ele se destina principalmente a personalizações, pois fornece a capacidade de gerar:

* Pacotes CRX para perfis de Entrega, Depuração e Desenvolvimento (mencionados abaixo em [pacotes CRX](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)).
* Versão reduzida do código personalizado (para alterações semânticas).

#### Conteúdo WS {#ws-content}

* client-pkg:

   * src - contém artefatos necessários para criar nós CRX.
   * pom.xml - Script para criar pacotes de implantação para vários perfis WS-Deploy Package

* client-html:

   * assembly - contém zip.xml usado pelo script para criar o SDK do espaço de trabalho do AEM Forms.
   * src/main/webapp -

      * css - contém folhas de estilos para a área de trabalho do AEM Forms.
      * imagens - contém imagens usadas na área de trabalho do AEM Forms.
      * js:

         * libs - contém todas as bibliotecas de terceiros usadas na área de trabalho do AEM Forms.
         * licenciamentos - contém licenças para arquivos HTML e JS, bem como código para prefixar essas licenças para os respectivos arquivos de origem.
         * minifier - usado para combinação, miniificação e especificação do código personalizado JavaScript.
         * resourcejs_otimizer - Usado para combinação, miniificação e especificação da origem do JavaScript.
         * resource_generator - usado para gerar register.js e modelcontrollerpath.js.
         * tempo de execução:

            * initializer - contém initializer.js usado para inicializar visualizações de backbone e modelos usados na área de trabalho do AEM Forms.
            * modelos - contém modelos de backbone de todos os componentes presentes na área de trabalho do AEM Forms.
            * rotas - contém arquivos JavaScript e arquivos HTML que carregam processos de start, Tarefas, rastreamento e preferências na área de trabalho do AEM Forms.
            * services - contém service.js usado na área de trabalho do AEM Forms. Todas as chamadas do servidor são feitas por meio de service.js.
            * modelos - contém todos os modelos, ou seja, arquivos HTML de todas as visualizações na área de trabalho do AEM Forms.
            * util - contém todos os arquivos de utilitário (javascript) que são usados na área de trabalho do AEM Forms.
            * visualização - contém visualizações de backbone de todos os componentes na área de trabalho do AEM Forms.
         * main.js
         * router.js
      * libs/ws: pdf.html e pluginPing.pdf são usados para carregar PDF forms na área de trabalho do AEM Forms e WSNextAdapter.swf é usado para carregar formulários SWF e Guias na área de trabalho do AEM Forms.
      * localidades:

         * de-DE - Contém Translation.json para alemão.
         * en-US - Contém Translation.json para inglês.
         * fr-FR - Contém Translation.json para francês.
         * ja-JP - Contém Translation.json para japonês.
         * html.jsp - contém código para descobrir a localidade atual do navegador.
      * html.jsp
      * GET.jsp




### Pacote CRX {#crx-package}

O pacote CRX pode ser implantado no repositório CRX™. Está disponível em `[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`.

Este pacote pode ser criado usando os três perfis descritos abaixo.

| **Perfil** | **Descrição** | **Uso** |
|---|---|---|
| Perfil de remessa | Este perfil cria um pacote CRX do menor tamanho possível usando a miniificação. Este pacote é o mais eficiente. Todos os arquivos JavaScript™ são combinados e reduzidos em um único arquivo JS. | Use esse perfil quando não forem necessárias mais alterações semânticas nos arquivos JS. |
| Depurar perfil | Este perfil cria um pacote CRX moderadamente eficiente. O tamanho do pacote é ligeiramente maior do que o pacote criado usando o perfil de remessa. Este pacote tem a maioria dos arquivos JavaScript combinados em um único arquivo JS. | Use este perfil para depuração. |
| Perfil Dev | Este perfil cria um pacote CRX do maior tamanho possível. Todos os arquivos JavaScript estão disponíveis separadamente, como estão no pacote SDK. | Use esse perfil ao incorporar alterações semânticas. |

#### Perfil de Entrega {#ship-profile}

#### Comando {#command}

* mvn clean -P Envio da instalação na pasta client-pkg do pacote de origem enviado ao cliente.
* A execução do comando Entregar perfil funciona somente em uma JVM de 64 bits.

#### Conteúdo WS {#ws-content-1}

* css - contém style.css, ie.css e jquery-ui.css.
* imagens - Contém todas as imagens.
* js:

   * libs:

      * request - contém requirements.js.
      * jqueryui - Contém jquery.ui.datepicker.ja.js.
   * tempo de execução:

      * modelos - contém todos os modelos, ou seja, arquivos HTML de todos os componentes na área de trabalho do AEM Forms.
   * main.js (combinado, minimizado e certificado).
   * registry.js



* libs:

   * ws - contém pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Localidade - contém .content.xml.
* localidades:

   * de-DE - Contém Translation.json para alemão.
   * en-US - Contém Translation.json para inglês.
   * fr-FR - Contém Translation.json para francês.
   * ja-JP - Contém Translation.json para japonês.
   * html.jsp - contém código para descobrir a localidade atual do navegador.

* Índice - contém .content.xml
* perfil - contém offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Depurar Perfil {#debug-profile}

#### Comando {#command-1}

* instalação de Depuração de mvn clean -P no client-pkg
* A execução do comando Depurar perfil funciona somente em JVM de 64 bits.

#### Conteúdo WS {#ws-content-2}

* css - contém style.css, ie.css e jqueri-ui.css.
* imagens - Contém todas as imagens.
* js:

   * libs:

      * request - contém requirements.js.
      * jqueryui - Contém jquery.ui.datepicker.ja.js.
   * tempo de execução:

      * modelos - contém todos os modelos, ou seja, arquivos HTML de todos os componentes na área de trabalho do AEM Forms.
   * main.js (combinado).
   * registry.js



* libs:

   * ws - contém pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Localidade - contém .content.xml.
* localidades:

   * de-DE - Contém Translation.json para alemão.
   * en-US - Contém Translation.json para inglês.
   * fr-FR - Contém Translation.json para francês.
   * ja-JP - Contém Translation.json para japonês.
   * html.jsp - contém código para descobrir a localidade atual do navegador.

* Índice - contém .content.xml
* perfil - contém offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Perfil Dev {#dev-profile}

#### Comando {#command-2}

instalação mvn clean -P Dev em client-pkg

#### Conteúdo WS {#ws-content-3}

* css - contém style.css, ie.css e jqueri-ui.css.
* imagens - Contém todas as imagens.
* js:

   * libs - contém todas as bibliotecas usadas na área de trabalho do AEM Forms.
   * required - Contém requirements.js
   * jqueryui - Contém jquery.ui.datepicker.ja.js
   * tempo de execução:

      * initializer - contém initializer.js e modelcontrollerpath.js.
      * modelos - contém modelos de todos os componentes na área de trabalho do AEM Forms.
      * rotas - contém arquivos JavaScript e arquivos HTML que carregam processos de start, Tarefas, rastreamento e preferências na área de trabalho do AEM Forms.
      * services - contém service.js usado na área de trabalho do AEM Forms.
      * modelos - contém todos os modelos, ou seja, arquivos HTML de todos os componentes na área de trabalho do AEM Forms.
      * util - Contém todos os arquivos utilitários (JavaScript) que são usados na área de trabalho do AEM Forms.
      * visualização - contém visualizações de todos os componentes na área de trabalho do AEM Forms.
   * main.js
   * registry.js
   * router.js


* libs:

   * ws - contém pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Localidade - contém .content.xml.
* localidades:

   * de-DE - Contém Translation.json para alemão.
   * en-US - Contém Translation.json para inglês.
   * fr-FR - Contém Translation.json para francês.
   * ja-JP - Contém Translation.json para japonês.
   * html.jsp - contém código para descobrir a localidade atual do navegador.

* Índice - contém .content.xml
* perfil - contém offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml
