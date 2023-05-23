---
title: Desenvolvimento de componentes do AEM (interface clássica)
seo-title: Developing AEM Components (Classic UI)
description: A interface clássica usa ExtJS para criar dispositivos que fornecem a aparência dos componentes. HTL não é a linguagem de script recomendada para AEM.
seo-description: The classic UI uses ExtJS to create widgets that provide the look-and-feel of the components. HTL is not the recommended scripting language for AEM.
uuid: ed53d7c6-5996-4892-81a4-4ac30df85f04
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: c68f724f-f9b3-4018-8d3a-1680c53d73f8
legacypath: /content/docs/en/aem/6-2/develop/components/components-classic
exl-id: 3f078139-73fd-4913-9d67-264fb2515f8a
source-git-commit: 43a30b5ba76ea470cc50a962d4f04b4a1508964d
workflow-type: tm+mt
source-wordcount: '2392'
ht-degree: 1%

---

# Desenvolvimento de componentes do AEM (interface clássica){#developing-aem-components-classic-ui}

A interface clássica usa ExtJS para criar dispositivos que fornecem a aparência dos componentes. Devido à natureza desses widgets, há algumas diferenças entre como os componentes interagem com a interface clássica e o [interface habilitada para toque](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Vários aspectos do desenvolvimento de componentes são comuns à interface clássica e à interface habilitada para toque, portanto **você deve ler [Componentes do AEM - Noções básicas](/help/sites-developing/components-basics.md) antes** usando esta página, que lida com as especificidades da interface clássica.

>[!NOTE]
>
>Embora a Linguagem de modelo de HTML (HTL) e o JSP possam ser usados para desenvolver componentes para a interface clássica, esta página ilustra o desenvolvimento com o JSP. Isso se deve exclusivamente ao histórico de uso do JSP na interface clássica.
>
>HTL agora é a linguagem de script recomendada para AEM. Consulte [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=pt-BR) e [Desenvolvimento de componentes do AEM](/help/sites-developing/developing-components.md) para comparar métodos.

## Estrutura {#structure}

A estrutura básica de um componente é abordada na página [Componentes do AEM - Noções básicas](/help/sites-developing/components-basics.md#structure), que se aplica às interfaces do usuário sensíveis ao toque e às clássicas. Mesmo que você não precise usar as configurações para a interface habilitada para toque no novo componente, pode ser útil estar ciente delas ao herdar de componentes existentes.

## Scripts JSP {#jsp-scripts}

Scripts JSP ou Servlets podem ser usados para renderizar componentes. De acordo com as regras de processamento de solicitações do Sling, o nome do script padrão é:

`<*componentname*>.jsp`

## global.jsp {#global-jsp}

O arquivo de script JSP `global.jsp` O é usado para fornecer acesso rápido a objetos específicos (ou seja, para acessar conteúdo) para qualquer arquivo de script JSP usado para renderizar um componente.

Portanto `global.jsp` deve ser incluído em cada script JSP de renderização de componente em que um ou mais objetos fornecidos em `global.jsp` são usados.

A localização do padrão `global.jsp` é:

`/libs/foundation/global.jsp`

>[!NOTE]
>
>O caminho `/libs/wcm/global.jsp`, que foi usado pelas versões CQ 5.3 e anteriores, agora está obsoleto.

### Função de global.jsp, APIs usadas e Taglibs {#function-of-global-jsp-used-apis-and-taglibs}

A seguir estão os objetos mais importantes fornecidos por padrão `global.jsp`:

Resumo:

* `<cq:defineObjects />`

   * `slingRequest` - O Objeto De Solicitação Encapsulado ( `SlingHttpServletRequest`).
   * `slingResponse` - O Objeto De Resposta Disposto ( `SlingHttpServletResponse`).
   * `resource` - O objeto de recurso Sling ( `slingRequest.getResource();`).
   * `resourceResolver` - O objeto Sling Resource Resolver ( `slingRequest.getResoucreResolver();`).
   * `currentNode` - O nó JCR resolvido para a solicitação.
   * `log` - O logger Padrão ().
   * `sling` - O auxiliar de script do Sling.
   * `properties` - As propriedades do recurso endereçado ( `resource.adaptTo(ValueMap.class);`).
   * `pageProperties` - As propriedades da página do recurso endereçado.
   * `pageManager` - O gerenciador de páginas para acessar páginas de conteúdo AEM ( `resourceResolver.adaptTo(PageManager.class);`).
   * `component` - O objeto do componente AEM atual.
   * `designer` - O objeto de designer para recuperar informações de design ( `resourceResolver.adaptTo(Designer.class);`).
   * `currentDesign` - O design do recurso endereçado.
   * `currentStyle` - O estilo do recurso endereçado.

### Acesso ao conteúdo {#accessing-content}

Há três métodos para acessar conteúdo no WCM do AEM:

* Por meio do objeto de propriedades introduzido no `global.jsp`:

   O objeto de propriedades é uma instância de um ValueMap (consulte [API Sling](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ValueMap.html)) e contém todas as propriedades do recurso atual.

   Exemplo: `String pageTitle = properties.get("jcr:title", "no title");` usado no script de renderização de um componente página.

   Exemplo: `String paragraphTitle = properties.get("jcr:title", "no title");` usado no script de renderização de um componente de parágrafo padrão.

* Através do `currentPage` objeto introduzido no `global.jsp`:

   A variável `currentPage` é uma instância de uma página (consulte [API AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.mhtml)). A classe de página fornece alguns métodos para acessar conteúdo.

   Exemplo: `String pageTitle = currentPage.getTitle();`

* Via `currentNode` objeto introduzido no `global.jsp`:

   A variável `currentNode` é uma instância de um nó (consulte [API JCR](https://jackrabbit.apache.org/api/2.16/org/apache/jackrabbit/standalone/cli/core/CurrentNode.html)). As propriedades de um nó podem ser acessadas pelo `getProperty()` método.

   Exemplo: `String pageTitle = currentNode.getProperty("jcr:title");`

## Bibliotecas de tags JSP {#jsp-tag-libraries}

As bibliotecas de tags CQ e Sling fornecem acesso a funções específicas para uso no script JSP de seus modelos e componentes.

Para obter mais informações, consulte o documento [Bibliotecas de tags](/help/sites-developing/taglib.md).

## Uso de bibliotecas de HTML do lado do cliente {#using-client-side-html-libraries}

Sites modernos dependem muito do processamento do lado do cliente orientado por códigos JavaScript e CSS complexos. Organizar e otimizar a veiculação desse código pode ser um problema complicado.

Para ajudar a lidar com esse problema, o AEM fornece **Pastas de biblioteca do lado cliente**, que permitem armazenar o código do lado do cliente no repositório, organizá-lo em categorias e definir quando e como cada categoria de código deve ser entregue ao cliente. O sistema de biblioteca do lado do cliente cuida de produzir os links corretos na página final da Web para carregar o código correto.

Consulte o documento [Uso de bibliotecas de HTML do lado do cliente](/help/sites-developing/clientlibs.md) para obter mais informações.

## Caixa de diálogo {#dialog}

Seu componente precisará de uma caixa de diálogo para que os autores adicionem e configurem o conteúdo.

Consulte [Componentes do AEM - Noções básicas](/help/sites-developing/components-basics.md#dialogs) para obter mais detalhes.

## Configuração do comportamento de edição {#configuring-the-edit-behavior}

É possível configurar o comportamento de edição de um componente. Isso inclui atributos como ações disponíveis para o componente, características do editor de local e os ouvintes relacionados aos eventos no componente. A configuração é comum às interfaces habilitadas para toque e às clássicas, embora com determinadas diferenças específicas.

A variável [editar comportamento de um componente está configurado](/help/sites-developing/components-basics.md#edit-behavior) adicionando um `cq:editConfig` nó do tipo `cq:EditConfig` abaixo do nó do componente (do tipo `cq:Component`) e adicionando propriedades específicas e nós filhos.

## Uso e extensão de dispositivos ExtJS {#using-and-extending-extjs-widgets}

Consulte [Uso e extensão de dispositivos ExtJS](/help/sites-developing/widgets.md) para obter mais detalhes.

## Utilização de xtypes para widgets ExtJS {#using-xtypes-for-extjs-widgets}

Consulte [Uso de xtypes](/help/sites-developing/xtypes.md) para obter mais detalhes.

## Desenvolvimento de novos componentes {#developing-new-components}

Esta seção descreve como criar seus próprios componentes e adicioná-los ao sistema de parágrafos.

Uma maneira rápida de começar é copiar um componente existente e fazer as alterações desejadas.

Um exemplo de como desenvolver um componente é descrito detalhadamente em [Extensão do componente de Texto e imagem - um exemplo.](#extending-the-text-and-image-component-an-example)

### Desenvolver um novo componente (Adaptar componente existente) {#develop-a-new-component-adapt-existing-component}

Para desenvolver novos componentes para AEM com base em um componente existente, você pode copiar o componente, criar um arquivo javascript para o novo componente e armazená-lo em um local acessível ao AEM (consulte também [Personalização de Componentes e Outros Elementos](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)):

1. Usando o CRXDE Lite, crie uma nova pasta de componentes no:

   / `apps/<myProject>/components/<myComponent>`

   Recrie a estrutura do nó como em bibliotecas e copie a definição de um componente existente, como o componente de Texto. Por exemplo, para personalizar a cópia do componente de Texto:

   * de `/libs/foundation/components/text`
   * para `/apps/myProject/components/text`

1. Modifique o `jcr:title` para refletir seu novo nome.
1. Abra a pasta de novos componentes e faça as alterações necessárias. Além disso, exclua todas as informações irrelevantes na pasta.

   É possível fazer alterações como:

   * adição de um novo campo na caixa de diálogo

      * `cq:dialog` - caixa de diálogo para a interface habilitada para toque
      * `dialog` - caixa de diálogo para a interface clássica
   * substituindo o `.jsp` arquivo (nomeie-o com o nome do novo componente)
   * ou retrabalhando completamente o componente inteiro, se desejar

   Por exemplo, se você fizer uma cópia do componente Texto padrão, poderá adicionar outro campo à caixa de diálogo e, em seguida, atualizar o `.jsp` para processar a entrada feita lá.

   >[!NOTE]
   >
   >Um componente para o:
   >
   >* UI habilitada para toque usa [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) componentes
   >* UI Clássica usa [Widgets ExtJS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)


   >[!NOTE]
   >
   >Uma caixa de diálogo definida para a interface clássica operará na interface habilitada para toque.
   >
   >Uma caixa de diálogo definida para a interface habilitada para toque não funcionará na interface clássica.
   >
   >Dependendo da instância e do ambiente de autor, talvez você queira definir ambos os tipos de caixa de diálogo para o componente.

1. Um dos nós a seguir deve estar presente e inicializado corretamente para que o novo componente seja exibido:

   * `cq:dialog` - caixa de diálogo para a interface habilitada para toque
   * `dialog` - caixa de diálogo para a interface clássica
   * `cq:editConfig` - como os componentes se comportam no ambiente de edição (por exemplo, arrastar e soltar)
   * `design_dialog` - caixa de diálogo para o modo de design (somente interface clássica)

1. Ative o novo componente no seu sistema de parágrafos:

   * utilização do CRXDE Lite para adicionar o valor `<path-to-component>` (por exemplo, `/apps/geometrixx/components/myComponent`) para os componentes de propriedade do nó `/etc/designs/geometrixx/jcr:content/contentpage/par`
   * seguindo as instruções em [Adicionar novos componentes a sistemas de parágrafos](#adding-a-new-component-to-the-paragraph-system-design-mode)

1. No WCM do AEM, abra uma página no seu site e insira um novo parágrafo do tipo que você acabou de criar para garantir que o componente esteja funcionando corretamente.

>[!NOTE]
>
>Para ver as estatísticas de tempo do carregamento de página, é possível usar Ctrl-Shift-U - com `?debugClientLibs=true` definido no URL.

### Adicionar um novo componente ao Sistema de parágrafos (Modo Design) {#adding-a-new-component-to-the-paragraph-system-design-mode}

Depois que o componente tiver sido desenvolvido, você o adiciona ao sistema de parágrafo, o que permite aos autores selecionar e usar o componente ao editar uma página.

1. Acesse uma página em seu ambiente de criação que use o sistema de parágrafos, por exemplo `<contentPath>/Test.html`.
1. Alterne para o modo Design por meio de:

   * adicionando `?wcmmode=design` ao final do URL e acessando novamente, por exemplo:

      `<contextPath>/ Test.html?wcmmode=design`

   * clicar em Design no Sidekick

   Agora você está no modo de design e pode editar o sistema de parágrafos.

1. Clique em Editar.

   Uma lista de componentes pertencentes ao sistema de parágrafos é mostrada. O novo componente também está listado.

   Os componentes podem ser ativados (ou desativados) para determinar quais são oferecidos ao autor ao editar uma página.

1. Ative o componente e volte ao modo de edição normal para confirmar que ele está disponível para uso.

### Extensão do componente de Texto e imagem - um exemplo {#extending-the-text-and-image-component-an-example}

Esta seção fornece um exemplo de como estender o componente padrão de texto e imagem amplamente usado com um recurso de posicionamento de imagem configurável.

A extensão para o componente de texto e imagem permite que os editores usem toda a funcionalidade existente do componente, além de ter uma opção extra para especificar a disposição da imagem:

* No lado esquerdo do texto (comportamento atual e o novo padrão)
* Assim como no lado direito

Depois de estender esse componente, você pode configurar a disposição da imagem por meio da caixa de diálogo do componente.

As seguintes técnicas estão descritas neste exercício:

* Copiar o nó do componente existente e modificar seus metadados
* Modificar a caixa de diálogo do componente, incluindo a herança de widgets das caixas de diálogo principais
* Modificação do script do componente para implementar a nova funcionalidade

>[!NOTE]
>
>Este exemplo é direcionado para a interface clássica.

>[!NOTE]
>
>Este exemplo é baseado no conteúdo de amostra do Geometrixx, que não é mais enviado com AEM, tendo sido substituído por We.Retail. Consulte o documento [Implementação de referência do We.Retail](/help/sites-developing/we-retail.md#we-retail-geometrixx) para saber como baixar e instalar o Geometrixx.

#### Extensão do componente textimage existente {#extending-the-existing-textimage-component}

Para criar o novo componente, usamos o componente textimage padrão como uma base e o modificamos. Armazenamos o novo componente no aplicativo de exemplo WCM do Geometrixx AEM.

1. Copie o componente de imagem de texto padrão de `/libs/foundation/components/textimage` na pasta do componente Geometrixx, `/apps/geometrixx/components`, utilizando teximage como o nome do nó de destino. (Copie o componente navegando até o componente, clicando com o botão direito do mouse e selecionando Copiar e navegando até o diretório de destino.)

   ![chlimage_1-59](assets/chlimage_1-59a.png)

1. Para manter esse exemplo simples, navegue até o componente copiado e exclua todos os subnós do novo nó de imagem de texto, exceto os seguintes:

   * definição de diálogo: `textimage/dialog`
   * script do componente: `textimage/textimage.jsp`
   * editar nó de configuração (permitindo arrastar e soltar ativos): `textimage/cq:editConfig`

   >[!NOTE]
   >
   >A definição da caixa de diálogo depende da interface do usuário:
   >
   >* Interface habilitada para toque: `textimage/cq:dialog`
   >* IU Clássica: `textimage/dialog`


1. Edite os metadados do componente:

   * Nome do componente

      * Definir `jcr:description` para `Text Image Component (Extended)`
      * Definir `jcr:title` para `Text Image (Extended)`
   * Grupo, onde o componente está listado no sidekick (deixe como está)

      * Sair `componentGroup` definir como `General`
   * O componente principal do novo componente (o componente textimage padrão)

      * Definir `sling:resourceSuperType` para `foundation/components/textimage`

   Após esta etapa, o nó do componente terá esta aparência:

   ![chlimage_1-60](assets/chlimage_1-60a.png)

1. Altere o `sling:resourceType` propriedade do nó de configuração de edição da imagem (propriedade: `textimage/cq:editConfig/cq:dropTargets/image/parameters/sling:resourceType`) para `geometrixx/components/textimage.`

   Dessa forma, quando uma imagem é solta no componente na página, a variável `sling:resourceType` a propriedade do componente textimage estendido está definida como: `geometrixx/components/textimage.`

1. Modifique a caixa de diálogo do componente para incluir a nova opção. O novo componente herda as partes da caixa de diálogo que são as mesmas da original. A única adição que fazemos é estender a **Avançado** , adicionando um **Posição da imagem** lista suspensa, com opções **Esquerda** e **Direita**:

   * Deixe a `textimage/dialog`propriedades inalteradas.

   Observe como `textimage/dialog/items` O tem quatro subnós, tab1 a tab4, que representam as quatro guias da caixa de diálogo textimage.

   * Para as duas primeiras guias (tab1 e tab2):

      * Altere xtype para cqinclude (para herdar do componente padrão).
      * Adicionar uma propriedade de caminho com valores `/libs/foundation/components/textimage/dialog/items/tab1.infinity.json`e `/libs/foundation/components/textimage/dialog/items/tab2.infinity.json`, respectivamente.
      * Remova todas as outras propriedades ou nós secundários.
   * Para tab3:

      * Deixar as propriedades e os subnós sem alterações
      * Adicionar uma nova definição de campo a `tab3/items`, posição do nó do tipo `cq:Widget`
      * Defina as seguintes propriedades (do tipo String) para o novo `tab3/items/position`nó:

         * `name`: `./imagePosition`
         * `xtype`: `selection`
         * `fieldLabel`: `Image Position`
         * `type`: `select`
      * Adicionar subnó `position/options` do tipo `cq:WidgetCollection` para representar as duas opções de posicionamento de imagem e, abaixo dela, criar dois nós, o1 e o2 do tipo `nt:unstructured`.
      * Para o nó `position/options/o1` defina as propriedades: `text` para `Left` e `value` para `left.`
      * Para o nó `position/options/o2` defina as propriedades: `text` para `Right` e `value` para `right`.
   * Excluir guia 4.

   A posição da imagem é mantida no conteúdo como a `imagePosition`propriedade do nó que representa `textimage` parágrafo. Após essas etapas, a caixa de diálogo do componente fica assim:

   ![chlimage_1-61](assets/chlimage_1-61a.png)

1. Estender o script do componente, `textimage.jsp`, com manipulação extra do novo parâmetro:

   ```xml
   Image image = new Image(resource, "image");
   
   if (image.hasContent() || WCMMode.fromRequest(request) == WCMMode.EDIT) {
        image.loadStyleData(currentStyle);
   ```

   Vamos substituir o fragmento de código enfatizado *%>&lt;div class=&quot;image&quot;>&lt;%* com o novo código gerando um estilo personalizado para essa tag.

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

#### Verificação do novo componente {#checking-the-new-component}

Depois que o componente tiver sido desenvolvido, é possível adicioná-lo ao sistema de parágrafo, o que permite aos autores selecionar e usar o componente ao editar uma página. Essas etapas permitem testar o componente.

1. Abra uma página no Geometrixx, como Inglês/Empresa.
1. Alterne para o modo de design clicando em Design no Sidekick.
1. Edite o design do sistema de parágrafo clicando em Editar no sistema de parágrafo no meio da página. Uma lista de componentes, que podem ser colocados no sistema de parágrafo, é mostrada e deve incluir seu componente recém-desenvolvido, Imagem de texto (estendida) . Ative-o para o sistema de parágrafo selecionando-o e clicando em OK.
1. Volte para o modo de edição.
1. Adicione o parágrafo Imagem de texto (Estendido) ao sistema de parágrafo, inicialize o texto e a imagem com conteúdo de amostra. Salve as alterações.
1. Abra a caixa de diálogo do texto e do parágrafo de imagem, altere a Posição da imagem na guia Avançado para Direita e clique em OK para salvar as alterações.
1. O parágrafo é renderizado com a imagem à direita.
1. O componente está pronto para uso.

O componente armazena seu conteúdo em um parágrafo na página Empresa.

### Desativar a capacidade de carregamento do componente de Imagem {#disable-upload-capability-of-the-image-component}

Para desativar esse recurso, usamos o componente de imagem padrão como uma base e o modificamos. Armazenamos o novo componente no aplicativo de exemplo do Geometrixx.

1. Copie o componente de imagem padrão de `/libs/foundation/components/image` na pasta do componente Geometrixx, `/apps/geometrixx/components`, usando imagem como o nome do nó de destino.

   ![chlimage_1-62](assets/chlimage_1-62a.png)

1. Edite os metadados do componente:

   * Definir **jcr:title** para `Image (Extended)`

1. Vá até `/apps/geometrixx/components/image/dialog/items/image`.
1. Adicionar uma nova propriedade:

   * **Nome**: `allowUpload`
   * **Tipo**: `String`
   * **Valor**: `false`

   ![chlimage_1-63](assets/chlimage_1-63a.png)

1. Clique em **Salvar tudo**. O componente está pronto para teste.
1. Abra uma página no Geometrixx, como Inglês/Empresa.
1. Alterne para o modo de design e ative a Imagem (Estendida).
1. Volte para o modo de edição e adicione-o ao sistema de parágrafos. Nas próximas imagens, é possível ver as diferenças entre o componente de imagem original e o que você acabou de criar.

   Componente da imagem original:

   ![chlimage_1-64](assets/chlimage_1-64a.png)

   Seu novo componente de imagem:

   ![chlimage_1-65](assets/chlimage_1-65a.png)

1. O componente está pronto para uso.
