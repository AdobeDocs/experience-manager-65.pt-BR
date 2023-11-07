---
title: Introdução à personalização do espaço de trabalho do formulário AEM
seo-title: Introduction to Customizing AEM form workspace
description: Uma introdução rápida, com informações conceituais e técnicas, para personalizar o espaço de trabalho do LiveCycle AEM Forms para gerenciamento de processos.
seo-description: A quick introduction, with conceptual and technical information, to customize LiveCycle AEM Forms workspace for process management.
uuid: 38759071-e6b8-4976-8b06-909ad7a786cd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 021c6606-8cd3-472c-a80b-b1bcace7e87f
docset: aem65
exl-id: b183d42f-343c-4acb-bc73-f80ad72e54df
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1760'
ht-degree: 0%

---

# Introdução à personalização do espaço de trabalho do formulário AEM{#introduction-to-customizing-aem-form-workspace}

O espaço de trabalho do formulário AEM fornece recursos para modificar a semântica de apresentação e a funcionalidade de sua interface. Os tipos de personalizações para alterar o estilo, o layout, a formatação, a identidade visual e as funcionalidades principais são descritos abaixo.

![cu_custom_workspace_example](assets/cu_customized_workspace_example.png)

Um exemplo de um espaço de trabalho personalizado

## Tipos de personalizações {#types-of-customizations}

O espaço de trabalho do AEM Forms oferece suporte a uma grande variedade de personalizações para atualizar o layout da interface do usuário, sua aparência, funcionalidade e muito mais. As personalizações envolvem a atualização de um ou mais dos itens a seguir:

* Aparências da interface do usuário
* Funcionalidade usando personalizações semânticas
* Reutilizar componentes de HTML em outros aplicativos

### Alterações na interface do usuário {#user-interface-changes}

É possível alterar a aparência, o layout e outras semânticas de apresentação do espaço de trabalho do AEM Forms. Altere o espaço de trabalho personalizando os arquivos CSS, modelos de HTML e JavaScript™. Todos os arquivos padrão são fornecidos na instalação padrão.

As etapas mais comumente aplicáveis são abordadas em [Etapas genéricas para personalização do espaço de trabalho do AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Para obter exemplos específicos dessas personalizações, incluindo as etapas detalhadas, consulte os artigos relacionados no final deste artigo.

#### Como entender a folha de estilos {#understanding-the-style-sheet}

Antes de personalizar o espaço de trabalho, familiarize-se com a folha de estilos padrão fornecida com o AEM Forms em /libs/ws/css/style.css.

Para personalizar o espaço de trabalho, é recomendável que você se familiarize com a folha de estilos existente, style.css, na pasta /libs/ws/css. Alguns componentes proeminentes são descritos abaixo.

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
   <td><p>.categorias, .filtros</p> </td>
   <td><p>Espaço abaixo da lista de categorias</p> </td>
  </tr>
  <tr>
   <td><p>categoria, filtro</p> </td>
   <td><p>Categoria</p> </td>
  </tr>
  <tr>
   <td><p>.categoria:passar o mouse, .categoria.selecionada, .filtro:passar o mouse, .filtro.selecionado</p> </td>
   <td><p>Categoria selecionada e estilo de passar o mouse sobre a categoria</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar .tool, categoryListBar .content</p> </td>
   <td><p>Página Iniciar processo (lista de Categorias fechada)</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar .tool, filterListBar .content</p> </td>
   <td><p>Página Tarefas Pendentes (lista de Filtros fechada)</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar .tool, processNameListBar .content</p> </td>
   <td><p>Página de rastreamento (lista de nomes de processos fechada)</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList, .tasklist</p> </td>
   <td><p>A lista de pontos iniciais ou a lista de tarefas</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList .header, .tasklist .header</p> </td>
   <td><p>O cabeçalho de uma lista de pontos iniciais ou de uma lista de tarefas</p> </td>
  </tr>
  <tr>
   <td><p>.ponto inicial.selecionado, .tarefa.selecionado</p> </td>
   <td><p>O ponto inicial ou a tarefa selecionada</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.descrição selecionada, .task.descrição selecionada</p> </td>
   <td><p>Descrição do ponto de partida ou da tarefa selecionada</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>A área Tarefa</p> </td>
  </tr>
  <tr>
   <td><p>#header .dropdown</p> </td>
   <td><p>Lista suspensa de usuários no cabeçalho</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>Lista suspensa Classificar tarefa</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

A aparência do espaço de trabalho do AEM Forms empresta sua aparência de um CSS. Personalizando o CSS, você pode alterar a semântica de apresentação do espaço de trabalho, como fontes, cores, identidade visual e layout.

As etapas de nível superior para personalização de CSS são:

* Crie um arquivo CSS.
* Adicione itens de estilo a este CSS. Consulte Noções básicas sobre estilos CSS para obter mais informações.
* Atualizar as referências no `html.jsp`.

Para obter as etapas exatas para fazer essas personalizações, consulte [Etapas genéricas para personalização do espaço de trabalho do AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). O arquivo CSS fornecido com o espaço de trabalho do AEM Forms está em /libs/ws/css/. Para personalizações relacionadas ao CSS, use o [Pacote de envio](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p). Para obter exemplos específicos de personalizações relacionadas a CSS, consulte os tópicos de Ajuda relacionados no final deste artigo.

#### Imagem {#image}

É possível personalizar o espaço de trabalho do AEM Forms para adicionar avatares de usuários ou adicionar o logotipo da organização. Para essas personalizações, use [Pacote de envio](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p).

As etapas de nível superior para personalizações das imagens são:

* Instale e configure o WebDAV.
* Adicione novas imagens.
* Adicione novos estilos correspondentes às imagens adicionadas.
* Link para o novo arquivo CSS no `html.jsp` arquivo.

Para começar a personalizar as imagens no espaço de trabalho do AEM Forms, siga o [Etapas genéricas para personalização do espaço de trabalho do AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Para obter exemplos específicos de personalizações relacionadas a imagens, consulte os tópicos da Ajuda relacionados no final deste artigo.

#### modelo HTML {#html-template}

Os modelos de HTML ajudam a definir a aparência e o layout da interface do usuário do espaço de trabalho. Ao atualizar os modelos de HTML padrão, é possível personalizar a interface do usuário padrão de layout.

As etapas de nível superior para personalizações no modelo de HTML são:

* Em uma pasta criada pelo usuário, faça cópias dos arquivos padrão necessários.
* Adicionar novos modelos na pasta definida pelo usuário.
* Faça atualizações relevantes nos arquivos copiados, como o caminho do novo modelo.

Para obter exemplos específicos dessas personalizações, consulte os tópicos da Ajuda fornecidos no final deste artigo. Escolha entre as opções [Pacote de envio](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) ou o [Pacote de Desenvolvimento](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p), dependendo do template a ser personalizado.

### Alterações semânticas {#semantic-changes}

Para modificar a funcionalidade do espaço de trabalho do AEM Forms, altere o código-fonte do JavaScript. As modificações na funcionalidade principal são rotuladas como Alterações semânticas. Modifique modelos, visualizações e modelos fornecidos como parte do código-fonte do espaço de trabalho do AEM Forms.

As etapas de nível superior para fazer alterações semânticas para modificar a funcionalidade do espaço de trabalho do AEM Forms são:

* Em uma pasta criada pelo usuário, faça cópias dos arquivos padrão apropriados.
* Adicionar novos modelos e visualizações na pasta definida pelo usuário.
* Faça atualizações relevantes, como a atualização de caminhos de modelos e exibições recém-adicionados nos arquivos JavaScript padrão.
* Reduza o pacote para otimizar o desempenho.

Para obter informações mais conceituais sobre os componentes que fazem parte do código-fonte, consulte [Descrição de componentes reutilizáveis](/help/forms/using/description-reusable-components.md). Para essas personalizações, use o Pacote de Desenvolvimento.

### Componentes reutilizáveis {#reusable-components}

Como o AEM Forms Workspace é um software baseado em componentes, ele pode ser facilmente personalizado e reutilizado. É possível integrar facilmente os componentes do espaço de trabalho às suas aplicações Web.

Para obter mais informações conceituais, consulte [Descrição de componentes reutilizáveis](/help/forms/using/description-reusable-components.md) e para obter instruções sobre como usar os componentes, consulte [Integração de componentes do espaço de trabalho do AEM Forms em aplicativos web](/help/forms/using/description-reusable-components.md).

## Criação do código do espaço de trabalho do AEM Forms {#building-html-workspace-code}

### Pacote do SDK {#sdk-package}

O pacote contém o código-fonte do espaço de trabalho do AEM Forms. O pacote está disponível em `[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`.

Destina-se principalmente a personalizações, pois fornece a capacidade de gerar:

* Pacotes CRX para perfis de envio, depuração e desenvolvimento (mencionados abaixo em [Pacotes CRX](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)).
* Versão minificada do código personalizado (para alterações semânticas).

#### Conteúdo WS {#ws-content}

* client-pkg:

   * src - Contém artefatos necessários para criar nós do CRX.
   * pom.xml - Script para criar pacotes de implantação para vários perfis Pacote WS-Deploy

* client-html:

   * assembly - Contém zip.xml usado pelo script para criar o SDK do espaço de trabalho do AEM Forms.
   * src/main/webapp -

      * css - Contém folhas de estilos do espaço de trabalho do AEM Forms.
      * imagens - Contém imagens usadas no espaço de trabalho do AEM Forms.
      * js:

         * libs - contém todas as bibliotecas de terceiros usadas no AEM Forms workspace.
         * licenças - Contém licenças para arquivos HTML e JS e código para prefixar essas licenças aos respectivos arquivos de origem.
         * minificador - Usado para combinação, minificação e unificação do código JavaScript personalizado.
         * resourcejs_otimizer - usado para combinação, minificação e unificação da origem do JavaScript.
         * resource_generator - Usado para gerar register.js e modelcontrollerpath.js.
         * tempo de execução:

            * inicializador - Contém initializer.js usado para inicializar exibições e modelos de backbone usados no espaço de trabalho do AEM Forms.
            * templates - Contém modelos de backbone de todos os componentes presentes no AEM Forms workspace.
            * rotas - Contém arquivos JavaScript e arquivos HTML que carregam o processo de início, tarefas, rastreamento e preferências no espaço de trabalho do AEM Forms.
            * serviços - Contém service.js usado no espaço de trabalho do AEM Forms. Todas as chamadas de servidor são feitas por service.js.
            * modelos - Contém todos os modelos, ou seja, arquivos HTML de todas as exibições no AEM Forms workspace.
            * util - Contém todos os arquivos de utilitários (javascript) usados no espaço de trabalho do AEM Forms.
            * exibições - Contém exibições de backbone de todos os componentes no espaço de trabalho do AEM Forms.

         * main.js
         * router.js

      * libs/ws: pdf.html e pluginPing.pdf são usados para carregar PDF forms no espaço de trabalho do AEM Forms e WSNextAdapter.swf é usado para carregar formulários e guias de SWF no espaço de trabalho do AEM Forms.
      * códigos de idiomas:

         * de-DE - Contém translation.json para alemão.
         * en-US - Contém translation.json para inglês.
         * fr-FR - Contém translation.json para francês.
         * ja-JP - Contém translation.json para japonês.
         * html.jsp - Contém o código para descobrir a localidade atual do navegador.

      * html.jsp
      * GET.jsp

### Pacote CRX {#crx-package}

O pacote CRX pode ser implantado no repositório CRX™. Está disponível em `[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`.

Esse pacote pode ser criado usando os três perfis descritos abaixo.

| **Perfil** | **Descrição** | **Uso** |
|---|---|---|
| Perfil de remessa | Esse perfil cria um pacote CRX do menor tamanho possível usando minificação. Este pacote é o mais eficiente. Todos os arquivos JavaScript™ são combinados e minificados em um único arquivo JS. | Use este perfil quando nenhuma alteração semântica adicional for necessária nos arquivos JS. |
| Depurar perfil | Este perfil cria um pacote CRX moderadamente eficiente. O tamanho do pacote é ligeiramente maior do que o pacote criado usando o Perfil de envio. Este pacote tem a maioria dos arquivos JavaScript combinados em um único arquivo JS. | Use esse perfil para depuração. |
| Perfil de desenvolvimento | Este perfil cria um pacote CRX do maior tamanho possível. Todos os arquivos JavaScript estão disponíveis separadamente, pois estão no pacote SDK. | Use este perfil ao incorporar alterações semânticas. |

#### Perfil de envio {#ship-profile}

#### Comando {#command}

* mvn clean -P Entrega a instalação na pasta client-pkg do pacote de Origem entregue ao cliente.
* A execução do comando Ship profile funciona somente em uma JVM de 64 bits.

#### Conteúdo WS {#ws-content-1}

* css - Contém style.css, ie.css e jquery-ui.css.
* imagens - Contém todas as imagens.
* js:

   * bibliotecas:

      * require - Contém require.js.
      * jqueryui - Contém jquery.ui.datepicker.ja.js.

   * tempo de execução:

      * modelos - contém todos os modelos, ou seja, arquivos HTML de todos os componentes no espaço de trabalho do AEM Forms.

   * main.js (combinado, minificado e unificado).
   * registry.js

* bibliotecas:

   * ws - Contém pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Localidade - Contém .content.xml.
* códigos de idiomas:

   * de-DE - Contém translation.json para alemão.
   * en-US - Contém translation.json para inglês.
   * fr-FR - Contém translation.json para francês.
   * ja-JP - Contém translation.json para japonês.
   * html.jsp - Contém o código para descobrir a localidade atual do navegador.

* Índice - Contém .content.xml
* perfil - Contém offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Depurar perfil {#debug-profile}

#### Comando {#command-1}

* mvn clean -P Instalação de depuração no client-pkg
* A execução do comando Debug profile funciona somente em JVM de 64 bits.

#### Conteúdo WS {#ws-content-2}

* css - Contém style.css, ie.css e jqueri-ui.css.
* imagens - Contém todas as imagens.
* js:

   * bibliotecas:

      * require - Contém require.js.
      * jqueryui - Contém jquery.ui.datepicker.ja.js.

   * tempo de execução:

      * modelos - contém todos os modelos, ou seja, arquivos HTML de todos os componentes no espaço de trabalho do AEM Forms.

   * main.js (combinado).
   * registry.js

* bibliotecas:

   * ws - Contém pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Localidade - Contém .content.xml.
* códigos de idiomas:

   * de-DE - Contém translation.json para alemão.
   * en-US - Contém translation.json para inglês.
   * fr-FR - Contém translation.json para francês.
   * ja-JP - Contém translation.json para japonês.
   * html.jsp - Contém o código para descobrir a localidade atual do navegador.

* Índice - Contém .content.xml
* perfil - Contém offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Perfil de Desenvolvimento {#dev-profile}

#### Comando {#command-2}

mvn clean -P Dev install no client-pkg

#### Conteúdo WS {#ws-content-3}

* css - Contém style.css, ie.css e jqueri-ui.css.
* imagens - Contém todas as imagens.
* js:

   * libs - contém todas as bibliotecas usadas no AEM Forms workspace.
   * require - Contém require.js
   * jqueryui - Contém jquery.ui.datepicker.ja.js
   * tempo de execução:

      * inicializador - Contém initializer.js e modelcontrollerpath.js.
      * templates - Contém modelos de todos os componentes no AEM Forms workspace.
      * rotas - Contém arquivos JavaScript e arquivos HTML que carregam o processo de início, tarefas, rastreamento e preferências no espaço de trabalho do AEM Forms.
      * serviços - Contém service.js usado no espaço de trabalho do AEM Forms.
      * modelos - contém todos os modelos, ou seja, arquivos HTML de todos os componentes no espaço de trabalho do AEM Forms.
      * util - Contém todos os arquivos de utilitários (JavaScript) usados no espaço de trabalho do AEM Forms.
      * exibições - Contém exibições de todos os componentes no espaço de trabalho do AEM Forms.

   * main.js
   * registry.js
   * router.js

* bibliotecas:

   * ws - Contém pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Localidade - Contém .content.xml.
* códigos de idiomas:

   * de-DE - Contém translation.json para alemão.
   * en-US - Contém translation.json para inglês.
   * fr-FR - Contém translation.json para francês.
   * ja-JP - Contém translation.json para japonês.
   * html.jsp - Contém o código para descobrir a localidade atual do navegador.

* Índice - Contém .content.xml
* perfil - Contém offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml
