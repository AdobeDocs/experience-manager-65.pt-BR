---
title: Desenvolvimento de componentes AEM (IU clássica)
seo-title: Desenvolvimento de componentes AEM (IU clássica)
description: A interface clássica usa o ExtJS para criar widgets que fornecem a aparência dos componentes. HTL não é a linguagem de script recomendada para AEM.
seo-description: A interface clássica usa o ExtJS para criar widgets que fornecem a aparência dos componentes. HTL não é a linguagem de script recomendada para AEM.
uuid: ed53d7c6-5996-4892-81a4-4ac30df85f04
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: c68f724f-f9b3-4018-8d3a-1680c53d73f8
legacypath: /content/docs/en/aem/6-2/develop/components/components-classic
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '2423'
ht-degree: 1%

---


# Desenvolvimento de componentes AEM (Interface clássica){#developing-aem-components-classic-ui}

A interface clássica usa o ExtJS para criar widgets que fornecem a aparência dos componentes. Devido à natureza desses widgets, há algumas diferenças entre a forma como os componentes interagem com a interface clássica e a [interface habilitada para toque](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Muitos aspectos do desenvolvimento de componentes são comuns à interface clássica e à interface habilitada para toque, portanto **você deve ler [AEM Componentes - Informações básicas](/help/sites-developing/components-basics.md) antes de** usar esta página, que lê as especificações da interface clássica.

>[!NOTE]
>
>Embora a Linguagem de modelo HTML (HTL) e o JSP possam ser usados para desenvolver componentes para a interface clássica, esta página ilustra o desenvolvimento com o JSP. Isso se deve exclusivamente ao histórico de uso do JSP na interface clássica.
>
>HTL agora é a linguagem de script recomendada para AEM. Consulte [HTL](https://docs.adobe.com/content/help/pt-BR/experience-manager-htl/using/overview.html) e [Desenvolvimento de componentes AEM](/help/sites-developing/developing-components.md) para comparar métodos.

## Estrutura {#structure}

A estrutura básica de um componente é abordada na página [AEM Componentes - Informações básicas](/help/sites-developing/components-basics.md#structure), que aplica as interfaces de toque e clássica. Mesmo se você não precisar usar as configurações para a interface habilitada para toque em seu novo componente, pode ajudar a conhecê-las ao herdar dos componentes existentes.

## Scripts JSP {#jsp-scripts}

Scripts ou Servlets JSP podem ser usados para renderizar componentes. De acordo com as regras de processamento de solicitação de Sling, o nome do script padrão é:

`<*componentname*>.jsp`

## global.jsp {#global-jsp}

O arquivo de script JSP `global.jsp` é usado para fornecer acesso rápido a objetos específicos (isto é, para acessar conteúdo) a qualquer arquivo de script JSP usado para renderizar um componente.

Portanto, `global.jsp` deve ser incluído em cada script JSP de renderização de componente onde um ou mais dos objetos fornecidos em `global.jsp` são usados.

O local padrão `global.jsp` é:

`/libs/foundation/global.jsp`

>[!NOTE]
>
>O caminho `/libs/wcm/global.jsp`, que foi usado pelas versões CQ 5.3 e anterior, agora está obsoleto.

### Função de global.jsp, APIs usadas e Taglibs {#function-of-global-jsp-used-apis-and-taglibs}

A seguir, são listas os objetos mais importantes fornecidos pelo padrão `global.jsp`:

Resumo:

* `<cq:defineObjects />`

   * `slingRequest` - O objeto de solicitação encapsulado (  `SlingHttpServletRequest`).
   * `slingResponse` - O objeto de resposta encapsulado (  `SlingHttpServletResponse`).
   * `resource` - O Objeto De Recurso Sling (  `slingRequest.getResource();`).
   * `resourceResolver` - O Objeto Sling Resource Resolver (  `slingRequest.getResoucreResolver();`).
   * `currentNode` - O nó JCR resolvido para a solicitação.
   * `log` - O registrador padrão ().
   * `sling` - O auxiliar de script Sling.
   * `properties` - As propriedades do recurso endereçado (  `resource.adaptTo(ValueMap.class);`).
   * `pageProperties` - As propriedades da página do recurso endereçado.
   * `pageManager` - O gerenciador de páginas para acessar AEM páginas de conteúdo (  `resourceResolver.adaptTo(PageManager.class);`).
   * `component` - O objeto componente do componente AEM atual.
   * `designer` - O objeto designer para recuperar informações de design (  `resourceResolver.adaptTo(Designer.class);`).
   * `currentDesign` - A concepção do recurso endereçado.
   * `currentStyle` - O estilo do recurso endereçado.

### Acessar conteúdo {#accessing-content}

Existem três métodos para acessar o conteúdo AEM WCM:

* Pelo objeto properties introduzido em `global.jsp`:

   O objeto properties é uma instância de um ValueMap (consulte [Sling API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ValueMap.html)) e contém todas as propriedades do recurso atual.

   Exemplo: `String pageTitle = properties.get("jcr:title", "no title");` usado no script de renderização de um componente de página.

   Exemplo: `String paragraphTitle = properties.get("jcr:title", "no title");` usado no script de renderização de um componente de parágrafo padrão.

* Pelo objeto `currentPage` introduzido em `global.jsp`:

   O objeto `currentPage` é uma instância de uma página (consulte [AEM API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.mhtml)). A classe page fornece alguns métodos para acessar o conteúdo.

   Exemplo: `String pageTitle = currentPage.getTitle();`

* Via `currentNode` objeto introduzido em `global.jsp`:

   O objeto `currentNode` é uma instância de um nó (consulte [API JCR](https://jackrabbit.apache.org/api/2.16/org/apache/jackrabbit/standalone/cli/core/CurrentNode.html)). As propriedades de um nó podem ser acessadas pelo método `getProperty()`.

   Exemplo: `String pageTitle = currentNode.getProperty("jcr:title");`

## Bibliotecas de tags JSP {#jsp-tag-libraries}

As bibliotecas de tags CQ e Sling fornecem acesso a funções específicas para uso no script JSP dos seus modelos e componentes.

Para obter mais informações, consulte o documento [Bibliotecas de tags](/help/sites-developing/taglib.md).

## Usando bibliotecas HTML do lado do cliente {#using-client-side-html-libraries}

Sites modernos dependem muito do processamento no cliente, conduzido por códigos complexos de JavaScript e CSS. Organizar e otimizar a entrega desse código pode ser um problema complicado.

Para ajudar a lidar com esse problema, AEM fornece **Pastas de biblioteca do lado do cliente**, que permitem armazenar o código do lado do cliente no repositório, organizá-lo no categoria e definir quando e como cada categoria de código deve ser fornecida ao cliente. O sistema de biblioteca do lado do cliente cuida de produzir os links corretos em sua página da Web final para carregar o código correto.

Consulte o documento [Usando bibliotecas HTML do lado do cliente](/help/sites-developing/clientlibs.md) para obter mais informações.

## Caixa de diálogo {#dialog}

Seu componente precisará de uma caixa de diálogo para que os autores adicionem e configurem o conteúdo.

Consulte [AEM Componentes - Informações básicas](/help/sites-developing/components-basics.md#dialogs) para obter mais detalhes.

## Configuração do comportamento de edição {#configuring-the-edit-behavior}

Você pode configurar o comportamento de edição de um componente. Isso inclui atributos como ações disponíveis para o componente, características do editor local e ouvintes relacionados a eventos no componente. A configuração é comum às interfaces de usuário habilitadas para toque e clássica, embora com certas diferenças específicas.

O comportamento [editar de um componente é configurado](/help/sites-developing/components-basics.md#edit-behavior) adicionando um nó `cq:editConfig` do tipo `cq:EditConfig` abaixo do nó do componente (do tipo `cq:Component`) e adicionando propriedades e nós secundários específicos.

## Uso e extensão de widgets ExtJS {#using-and-extending-extjs-widgets}

Consulte [Usar e estender widgets ExtJS](/help/sites-developing/widgets.md) para obter mais detalhes.

## Uso de xtypes para widgets ExtJS {#using-xtypes-for-extjs-widgets}

Consulte [Usando xtypes](/help/sites-developing/xtypes.md) para obter mais detalhes.

## Desenvolvimento de novos componentes {#developing-new-components}

Esta seção descreve como criar seus próprios componentes e adicioná-los ao sistema de parágrafo.

Uma maneira rápida de começar é copiar um componente existente e fazer as alterações desejadas.

Um exemplo de como desenvolver um componente é descrito detalhadamente em [Extensão do Componente de Texto e Imagem - Um Exemplo.](#extending-the-text-and-image-component-an-example)

### Desenvolver um novo componente (Adaptar componente existente) {#develop-a-new-component-adapt-existing-component}

Para desenvolver novos componentes para AEM com base no componente existente, você pode copiar o componente, criar um arquivo javascript para o novo componente e armazená-lo em um local acessível para AEM (consulte também [Personalizando componentes e outros elementos](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)):

1. Usando o CRXDE Lite, crie uma nova pasta de componentes em:

   / `apps/<myProject>/components/<myComponent>`

   Recrie a estrutura do nó como em libs e copie a definição de um componente existente, como o componente de Texto. Por exemplo, para personalizar a cópia do componente de Texto:

   * de `/libs/foundation/components/text`
   * para `/apps/myProject/components/text`

1. Modifique `jcr:title` para refletir seu novo nome.
1. Abra a nova pasta de componentes e faça as alterações necessárias. Além disso, exclua quaisquer informações estranhas na pasta.

   É possível fazer alterações como:

   * adição de um novo campo na caixa de diálogo

      * `cq:dialog` - caixa de diálogo para a interface habilitada para toque
      * `dialog` - caixa de diálogo para a interface clássica
   * substituição do arquivo `.jsp` (nomeie-o após seu novo componente)
   * ou retrabalhar completamente o componente inteiro se desejar

   Por exemplo, se você pegar uma cópia do componente Texto padrão, poderá adicionar um campo adicional à caixa de diálogo e, em seguida, atualizar o `.jsp` para processar a entrada feita lá.

   >[!NOTE]
   >
   >Um componente para:
   >
   >* A interface habilitada para toque usa componentes [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
   >* A interface clássica usa [widgets ExtJS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)


   >[!NOTE]
   >
   >Uma caixa de diálogo definida para a interface clássica funcionará dentro da interface habilitada para toque.
   >
   >Uma caixa de diálogo definida para a interface habilitada para toque não funcionará na interface clássica.
   >
   >Dependendo da instância e do ambiente do autor, talvez você queira definir ambos os tipos de diálogo para o seu componente.

1. Um dos nós a seguir deve estar presente e ser inicializado corretamente para que o novo componente seja exibido:

   * `cq:dialog` - caixa de diálogo para a interface habilitada para toque
   * `dialog` - caixa de diálogo para a interface clássica
   * `cq:editConfig` - como os componentes se comportam no ambiente de edição (por exemplo, arrastar e soltar)
   * `design_dialog` - caixa de diálogo para o modo de design (somente interface clássica)

1. Ative o novo componente no sistema de parágrafo:

   * usando a CRXDE Lite para adicionar o valor `<path-to-component>` (por exemplo, `/apps/geometrixx/components/myComponent`) aos componentes de propriedade do nó `/etc/designs/geometrixx/jcr:content/contentpage/par`
   * seguindo as instruções em [Adicionar novos componentes aos sistemas de parágrafo](#adding-a-new-component-to-the-paragraph-system-design-mode)

1. Em AEM WCM, abra uma página no site e insira um novo parágrafo do tipo que você acabou de criar para garantir que o componente esteja funcionando corretamente.

>[!NOTE]
>
>Para ver as estatísticas de tempo para o carregamento da página, você pode usar Ctrl-Shift-U - com `?debugClientLibs=true` definido no URL.

### Adicionar um novo componente ao Sistema de parágrafo (Modo de design) {#adding-a-new-component-to-the-paragraph-system-design-mode}

Depois que o componente for desenvolvido, você o adicionará ao sistema de parágrafo, que permite que os autores selecionem e usem o componente ao editar uma página.

1. Acesse uma página no ambiente de criação que usa o sistema de parágrafo, por exemplo `<contentPath>/Test.html`.
1. Alterne para o modo Design:

   * adicionar `?wcmmode=design` ao final do URL e acessar novamente, por exemplo:

      `<contextPath>/ Test.html?wcmmode=design`

   * clicando em Design no Sidekick

   Agora você está no modo de design e pode editar o sistema de parágrafo.

1. Clique em Editar.

   Uma lista de componentes pertencentes ao sistema de parágrafo é mostrada. Seu novo componente também está listado.

   Os componentes podem ser ativados (ou desativados) para determinar quais são oferecidos ao autor ao editar uma página.

1. Ative seu componente e retorne ao modo de edição normal para confirmar que ele está disponível para uso.

### Extensão do componente de texto e imagem - um exemplo {#extending-the-text-and-image-component-an-example}

Esta seção fornece um exemplo de como estender o texto amplamente usado e o componente padrão de imagem com um recurso de posicionamento de imagem configurável.

A extensão para o componente de texto e imagem permite que os editores usem toda a funcionalidade existente do componente, além de ter uma opção extra para especificar o posicionamento da imagem:

* No lado esquerdo do texto (comportamento atual e o novo padrão)
* Assim como no lado direito

Após estender esse componente, é possível configurar o posicionamento da imagem por meio da caixa de diálogo do componente.

As seguintes técnicas são descritas neste exercício:

* Copiar o nó do componente existente e modificar seus metadados
* Modificação da caixa de diálogo do componente, incluindo herança de widgets de caixas de diálogo pai
* Modificação do script do componente para implementar a nova funcionalidade

>[!NOTE]
>
>Este exemplo é direcionado para a interface clássica.

>[!NOTE]
>
>Este exemplo é baseado no conteúdo de amostra do Geometrixx, que não é mais fornecido com AEM, tendo sido substituído por We.Retail. Consulte o documento [Implementação de referência We.Retail](/help/sites-developing/we-retail.md#we-retail-geometrixx) para obter mais informações sobre como baixar e instalar o Geometrixx.

#### Extensão do componente de tempo de textura existente {#extending-the-existing-textimage-component}

Para criar o novo componente, usamos o componente de textura padrão como base e o modificamos. Armazenamos o novo componente no aplicativo de exemplo AEM WCM do Geometrixx.

1. Copie o componente de mensagem de texto padrão de `/libs/foundation/components/textimage` para a pasta do componente do Geometrixx, `/apps/geometrixx/components`, usando a mensagem de tempo como o nome do nó do público alvo. (Copie o componente navegando até o componente, clicando com o botão direito do mouse e selecionando Copiar e navegando até o diretório do público alvo.)

   ![chlimage_1-59](assets/chlimage_1-59a.png)

1. Para manter esse exemplo simples, navegue até o componente que você copiou e exclua todos os subnós do novo nó de tempo de textura, exceto os seguintes:

   * definição da caixa de diálogo: `textimage/dialog`
   * script de componente: `textimage/textimage.jsp`
   * editar nó de configuração (permitindo arrastar e soltar ativos): `textimage/cq:editConfig`

   >[!NOTE]
   >
   >A definição da caixa de diálogo depende da interface do usuário:
   >
   >* Interface habilitada para toque: `textimage/cq:dialog`
   >* Interface clássica: `textimage/dialog`


1. Edite os metadados do componente:

   * Nome do componente

      * Defina `jcr:description` como `Text Image Component (Extended)`
      * Defina `jcr:title` como `Text Image (Extended)`
   * Grupo, onde o componente está listado no sidekick (deixe como está)

      * Deixe `componentGroup` definido como `General`
   * Componente pai do novo componente (o componente de tempo de textura padrão)

      * Defina `sling:resourceSuperType` como `foundation/components/textimage`

   Após esta etapa, o nó do componente terá a seguinte aparência:

   ![chlimage_1-60](assets/chlimage_1-60a.png)

1. Altere a propriedade `sling:resourceType` do nó de configuração de edição da imagem (propriedade: `textimage/cq:editConfig/cq:dropTargets/image/parameters/sling:resourceType`) para `geometrixx/components/textimage.`

   Dessa forma, quando uma imagem é solta no componente na página, a propriedade `sling:resourceType` do componente de tempo de textura estendida é definida como: `geometrixx/components/textimage.`

1. Modifique a caixa de diálogo do componente para incluir a nova opção. O novo componente herda as partes da caixa de diálogo que são as mesmas do original. A única adição que fazemos é estender a guia **Avançado**, adicionando uma lista suspensa **Posição da imagem**, com as opções **Esquerda** e **Direita**:

   * Deixe as propriedades `textimage/dialog`inalteradas.

   Observe como `textimage/dialog/items` tem quatro subnós, tab1 a tab4, representando as quatro guias da caixa de diálogo de tempo de texto.

   * Para as duas primeiras guias (guia1 e guia2):

      * Altere xtype para cqinclude (para herdar do componente padrão).
      * Adicione uma propriedade path com valores `/libs/foundation/components/textimage/dialog/items/tab1.infinity.json`e `/libs/foundation/components/textimage/dialog/items/tab2.infinity.json`, respectivamente.
      * Remova todas as outras propriedades ou subnós.
   * Para a guia3:

      * Deixe as propriedades e os subnós sem alterações
      * Adicionar uma nova definição de campo a `tab3/items`, posição do nó do tipo `cq:Widget`
      * Defina as seguintes propriedades (do tipo String) para o novo nó `tab3/items/position`:

         * `name`: `./imagePosition`
         * `xtype`:  `selection`
         * `fieldLabel`:  `Image Position`
         * `type`:  `select`
      * Adicione o subnó `position/options` do tipo `cq:WidgetCollection` para representar as duas opções de posicionamento de imagem e, sob ele, crie dois nós, o1 e o2 do tipo `nt:unstructured`.
      * Para o nó `position/options/o1` defina as propriedades: `text` para `Left` e `value` para `left.`
      * Para o nó `position/options/o2` defina as propriedades: `text` para `Right` e `value` para `right`.
   * Excluir guia4.

   A posição da imagem é persistente no conteúdo como a propriedade `imagePosition`do nó que representa o parágrafo `textimage`. Após essas etapas, a caixa de diálogo do componente terá a seguinte aparência:

   ![chlimage_1-61](assets/chlimage_1-61a.png)

1. Amplie o script de componente, `textimage.jsp`, com a manipulação extra do novo parâmetro:

   ```xml
   Image image = new Image(resource, "image");
   
   if (image.hasContent() || WCMMode.fromRequest(request) == WCMMode.EDIT) {
        image.loadStyleData(currentStyle);
   ```

   Vamos substituir o fragmento de código enfatizado *%>&lt;div class=&quot;image&quot;>&lt;%* por um novo código que gera um estilo personalizado para essa tag.

   ```xml
   // todo: add new CSS class for the 'right image' instead of using
   // the style attribute
   String style="";
        if (properties.get("imagePosition", "left").equals("right")) {
             style = "style=\"float:right\"";
        }
        %><div <%= style %> class="image"><%
   ```

1. Salve o componente no repositório. O componente está pronto para teste.

#### Verificando o novo componente {#checking-the-new-component}

Depois que o componente for desenvolvido, você poderá adicioná-lo ao sistema de parágrafo, que permite que os autores selecionem e usem o componente ao editar uma página. Essas etapas permitem testar o componente.

1. Abra uma página em Geometrixx, como inglês / Empresa.
1. Alterne para o modo de design clicando em Design no Sidekick.
1. Edite o design do sistema de parágrafo clicando em Editar no sistema de parágrafo no meio da página. Uma lista de componentes, que pode ser colocada no sistema de parágrafo, é mostrada e deve incluir seu componente recém-desenvolvido, Imagem de texto (estendida). Ative-o para o sistema de parágrafo selecionando-o e clicando em OK.
1. Volte para o modo de edição.
1. Adicione o parágrafo Imagem de texto (estendida) ao sistema de parágrafo, inicialize o texto e a imagem com conteúdo de amostra. Salve as alterações.
1. Abra a caixa de diálogo do texto e do parágrafo da imagem, altere a Posição da imagem na guia Avançado para Direita e clique em OK para salvar as alterações.
1. O parágrafo é renderizado com a imagem à direita.
1. O componente agora está pronto para uso.

O componente armazena seu conteúdo em um parágrafo na página Empresa.

### Desativar a capacidade de carregamento do componente de imagem {#disable-upload-capability-of-the-image-component}

Para desativar esse recurso, usamos o componente de imagem padrão como base e o modificamos. Armazenamos o novo componente no aplicativo de exemplo de Geometrixx.

1. Copie o componente de imagem padrão de `/libs/foundation/components/image` para a pasta do componente do Geometrixx, `/apps/geometrixx/components`, usando a imagem como o nome do nó do público alvo.

   ![chlimage_1-62](assets/chlimage_1-62a.png)

1. Edite os metadados do componente:

   * Defina **jcr:title** como `Image (Extended)`

1. Vá até `/apps/geometrixx/components/image/dialog/items/image`.
1. Adicionar uma nova propriedade:

   * **Nome**: `allowUpload`
   * **Tipo**: `String`
   * **Valor**:  `false`

   ![chlimage_1-63](assets/chlimage_1-63a.png)

1. Clique em **Salvar tudo**. O componente está pronto para teste.
1. Abra uma página em Geometrixx, como inglês / Empresa.
1. Alterne para o modo de design e ative Imagem (estendida).
1. Volte para o modo de edição e adicione-o ao sistema de parágrafo. Nas próximas imagens, você pode ver as diferenças entre o componente de imagem original e aquele que você acabou de criar.

   Componente de imagem original:

   ![chlimage_1-64](assets/chlimage_1-64a.png)

   Seu novo componente de imagem:

   ![chlimage_1-65](assets/chlimage_1-65a.png)

1. O componente agora está pronto para uso.

