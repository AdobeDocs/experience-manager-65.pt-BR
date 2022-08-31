---
title: Personalizar os Componentes principais da CIF
description: Saiba como personalizar AEM Componentes principais da CIF. O tutorial aborda como estender com segurança um Componente principal da CIF para atender às necessidades específicas dos negócios. Saiba como estender uma consulta GraphQL para retornar um atributo personalizado e exibir o novo atributo em um Componente principal da CIF.
sub-product: Commerce
topics: Development
version: Cloud Service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
exl-id: 8933942e-be49-49d3-bf0a-7225257e2803
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '2604'
ht-degree: 25%

---

# Personalizar os Componentes principais da CIF do AEM {#customize-cif-components}

O [Projeto CIF Venia](https://github.com/adobe/aem-cif-guides-venia) é uma base de código de referência para usar [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components). Neste tutorial, você estenderá ainda mais o [Teaser do produto](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) componente para exibir um atributo personalizado do Adobe Commerce. Você também aprenderá mais sobre a integração GraphQL entre o AEM e a Adobe Commerce e os ganchos de extensão fornecidos pelos Componentes principais da CIF.

>[!TIP]
>
> Use o [Arquétipo de projeto AEM](https://github.com/adobe/aem-project-archetype) ao iniciar sua própria implementação de comércio.

## O que você vai criar

A marca Venia começou recentemente a fabricar alguns produtos usando materiais sustentáveis e a empresa gostaria de exibir um **Econômica** emblema como parte do Teaser do produto. Um novo atributo personalizado será criado no Adobe Commerce para indicar se um produto usa a variável **Ecológico** material. Esse atributo personalizado será adicionado como parte da consulta GraphQL e exibido no Teaser do produto para produtos especificados.

![Implementação Final do Símbolo Ecológico](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Pré-requisitos {#prerequisites}

Um ambiente de desenvolvimento local é necessário para concluir este tutorial. Isso inclui uma instância em execução de AEM que é configurada e conectada a uma instância do Adobe Commerce. Revise os requisitos e as etapas para [configuração de um desenvolvimento local com AEM](../develop.md). Para seguir o tutorial completamente, você precisará de permissões para adicionar [Atributos a um produto](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) no Adobe Commerce.

Você também precisará do GraphQL IDE como [GraphiQL](https://github.com/graphql/graphiql) ou uma extensão do navegador para executar amostras de código e tutoriais. Se você instalar uma extensão do navegador, verifique se ela tem a capacidade de definir cabeçalhos de solicitação. No Google Chrome, [Cliente GraphQL Altair](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) é uma extensão que pode fazer o trabalho.

## Clonar o projeto Venia {#clone-venia-project}

Nós vamos clonar o [Projeto Venia](https://github.com/adobe/aem-cif-guides-venia) e, em seguida, substituir os estilos padrão.

>[!NOTE]
>
> **Você pode usar um projeto existente** (com base no AEM Project Archetype com a CIF incluída) e ignore esta seção.

1. Execute o seguinte comando git para clonar o projeto:

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. Crie e implante o projeto em uma instância local do AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Adicione as configurações OSGi necessárias para conectar a instância do AEM a uma instância do Adobe Commerce ou adicionar as configurações ao projeto recém-criado.

1. Neste ponto, você deve ter uma versão funcional de uma loja conectada a uma instância do Adobe Commerce. Navegue até o `US` > `Home` página em: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Você verá que a loja está usando o tema Venia. Ao expandir o Menu principal da loja, você verá várias categorias, indicando que a conexão com o Adobe Commerce está funcionando.

   ![Loja configurada com o tema Venia](../assets/customize-cif-components/venia-store-configured.png)

## Criação do Teaser do produto {#author-product-teaser}

O Teaser do produto será estendido por todo este tutorial. Como primeira etapa, adicione uma nova instância do Teaser do produto à página inicial para entender a funcionalidade da linha de base.

1. Acesse a **página inicial** do site: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. Insira um novo **Teaser do produto** no container do layout principal da página.

   ![Inserir Teaser do produto](../assets/customize-cif-components/product-teaser-add-component.png)

3. Expanda o painel lateral (se ainda não estiver sendo exibido) e na lista suspensa do localizador de ativos selecione **Produtos**. Isso deve exibir uma lista de produtos disponíveis de uma instância conectada do Adobe Commerce. Selecione, **arraste e solte** um produto no **Teaser do produto** exibido na página.

   ![Arrastar e soltar Teaser do produto](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > Observação: você também pode configurar o produto exibido definindo o componente na caixa de diálogo (clicando na _chave inglesa_).

4. Agora você já deve estar vendo um produto no teaser. O nome e o preço do produto são atributos exibidos por padrão.

   ![Teaser do produto — estilo padrão](../assets/customize-cif-components/product-teaser-default-style.png)

## Adicionar um atributo personalizado no Adobe Commerce {#add-custom-attribute}

Os produtos e os dados do produto exibidos no AEM são armazenados no Adobe Commerce. Em seguida, adicione um novo atributo para **Econômica** como parte do conjunto de atributos do produto usando a interface do usuário do Adobe Commerce.

>[!TIP]
>
> Já tem um **Sim/Não** como parte do conjunto de atributos do produto? Sinta-se à vontade para usá-lo e ignore esta seção.

1. Faça logon na instância do Adobe Commerce.
1. Navegar para **Catálogo** > **Produtos**.
1. Atualize o filtro de pesquisa para encontrar o **Produto configurável** usado quando adicionado ao componente Teaser do exercício anterior. Abra o produto no modo de edição.

   ![Procurar o produto Valeria](../assets/customize-cif-components/search-valeria-product.png)

1. Na exibição do produto, clique em **Adicionar atributo** > **Criar novo atributo**.
1. Preencha o **Novo atributo** com os seguintes valores (deixe as configurações padrão para outros valores)

   | Conjunto de campos | Rótulo do campo | Valor |
   | ----------------------------- | ------------------ | ---------------- |
   | Propriedades do atributo | Rótulo do atributo | **Econômica** |
   | Propriedades do atributo | Tipo de entrada do catálogo | **Sim/Não** |
   | Propriedades avançadas de atributos | Código do atributo | **eco_friendly** |

   ![Novo formulário de Atributo](../assets/customize-cif-components/attribute-new-form.png)

   Clique em **Salvar atributo** quando terminar.

1. Role até a parte inferior do produto e expanda a **Atributos** cabeçalho. Você deve ver o novo **Econômica** campo. Alterne o botão para **Sim**.

   ![Mudar para sim](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **Salvar** as alterações no produto.

   >[!TIP]
   >
   > Mais detalhes sobre o gerenciamento [Atributos do produto podem ser encontrados no guia do usuário do Adobe Commerce](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html).

1. Navegar para **Sistema** > **Ferramentas** > **Gerenciamento de cache**. Como uma atualização foi feita no schema de dados, precisamos invalidar alguns dos Tipos de cache no Adobe Commerce.
1. Marque a caixa ao lado de **Configuração** e envie o tipo de cache para **Atualizar**

   ![Atualizar Tipo de Cache de Configuração](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > Mais detalhes sobre [O Gerenciamento de cache pode ser encontrado no guia do usuário do Adobe Commerce](https://docs.magento.com/user-guide/system/cache-management.html).

## Usar um GraphQL IDE para verificar o atributo {#use-graphql-ide}

Antes de entrar em AEM código, é útil explorar a variável [Adobe Commerce GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) usando um GraphQL IDE. A integração do Adobe Commerce com o AEM é feita principalmente por meio de uma série de consultas GraphQL. Entender e modificar as consultas GraphQL é uma das principais maneiras de estender os Componentes principais da CIF.

Em seguida, use um GraphQL IDE para verificar se a variável `eco_friendly` foi adicionado ao conjunto de atributos do produto. As capturas de tela deste tutorial estão usando o [Cliente GraphQL Altair](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja).

1. Abra o GraphQL IDE e insira o URL `http://<server>/graphql` na barra de URL do IDE ou da extensão.
2. Adicione o seguinte [consulta de produtos](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) em que `YOUR_SKU` é **SKU** do produto utilizado no exercício anterior:

   ```json
     {
       products(
       filter: { sku: { eq: "YOUR_SKU" } }
       ) {
           items {
           name
           sku
           eco_friendly
           }
       }
   }
   ```

3. Execute a query e você deverá obter uma resposta como a seguinte:

   ```json
   {
     "data": {
       "products": {
         "items": [
           {
             "name": "Valeria Two-Layer Tank",
             "sku": "VT11",
             "eco_friendly": 1
           }
         ]
       }
     }
   }
   ```

   ![Resposta GraphQL de exemplo](../assets/customize-cif-components/sample-graphql-query.png)

   Observe que o valor de **Sim** é um número inteiro de **1**. Isso será útil quando gravarmos a consulta GraphQL no Java.

   >[!TIP]
   >
   > Documentação mais detalhada sobre [Adobe Commerce GraphQL pode ser encontrado aqui](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## Atualizar o Modelo do Sling para o Teaser do produto {#updating-sling-model-product-teaser}

A seguir, estenderemos a lógica de negócios do Teaser do produto implementando um Modelo do Sling. Os [Modelos do Sling](https://sling.apache.org/documentation/bundles/models.html) são objetos POJO (Plain Old Java Objects) orientados por anotações que implementam qualquer lógica de negócios exigida pelo componente. Modelos do Sling são usados junto com os scripts HTL como parte do componente. Seguiremos o [padrão de delegação para Modelos do Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) para que possamos estender partes do modelo existente do Teaser do produto.

Os Modelos do Sling são implementados como Java e podem ser encontrados no módulo **principal** do projeto gerado.

Use [o IDE de sua escolha](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) para importar o projeto Venia. As capturas de tela usadas são da [Visual Studio Code IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code).

1. No IDE, navegue sob o **núcleo** para: `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![IDE de localização principal](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` é uma interface Java que estende a CIF [ProductTeaser](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) interface.

   Já foi adicionado um novo método chamado `isShowBadge()` para exibir um selo se o produto for considerado &quot;Novo&quot;.

1. Adicione um novo método `isEcoFriendly()` à interface:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   Esse é um novo método que introduziremos para encapsular a lógica de indicar se o produto tem o `eco_friendly` conjunto de atributos para **Sim** ou **Não**.

1. Em seguida, inspecione o `MyProductTeaserImpl.java` at `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`.

   O [padrão de delegação para Modelos do Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) allow `MyProductTeaserImpl` referência `ProductTeaser` modelo por meio do `sling:resourceSuperType` propriedade:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   Para todos os métodos que não queremos substituir ou alterar, podemos simplesmente retornar o valor que o `ProductTeaser` retorna. Por exemplo:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   Isso minimiza a quantidade de código Java que uma implementação precisa gravar.

1. Um dos pontos de extensão adicionais fornecidos pelos Componentes principais AEM CIF é o `AbstractProductRetriever` que fornece acesso a atributos específicos do produto. A Inspect `initModel()` método :

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to intialize the proudctRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   O `@PostConstruct` A anotação garante que esse método seja chamado assim que o Modelo do Sling for inicializado.

   Observe que a consulta GraphQL do produto já foi estendida com o uso da variável `extendProductQueryWith` para recuperar o método adicional `created_at` atributo. Esse atributo é usado posteriormente como parte do `isShowBadge()` método .

1. Atualize a consulta GraphQL para incluir a variável `eco_friendly` na consulta parcial:

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p -> p
               .createdAt()
               .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
           );
       }
   }
   ```

   Atualizar o método `extendProductQueryWith` é uma maneira eficiente de garantir que atributos de produto adicionais estejam disponíveis para o restante do modelo. Essa ação também minimiza o número de consultas executadas.

   No código acima, a variável`addCustomSimpleField` é usada para recuperar o `eco_friendly` atributo. Isso ilustra como você pode consultar qualquer atributo personalizado que faça parte do esquema do Adobe Commerce.

   >[!NOTE]
   >
   > O `createdAt()` foi efetivamente implementado como parte da [Interface do produto](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java). A maioria dos atributos de esquema encontrados com frequência foram implementados, portanto, use `addCustomSimpleField` somente para atributos verdadeiramente personalizados.

1. Adicione um logger para ajudar a depurar o código Java:

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. Em seguida, implemente o `isEcoFriendly()` método :

   ```java
   @Override
   public Boolean isEcoFriendly() {
   
       Integer ecoFriendlyValue;
       try {
           ecoFriendlyValue = productRetriever.fetchProduct().getAsInteger(ECO_FRIENDLY_ATTRIBUTE);
           if(ecoFriendlyValue != null && ecoFriendlyValue.equals(Integer.valueOf(1))) {
               LOGGER.info("*** Product is Eco Friendly**");
               return true;
           }
       } catch (SchemaViolationError e) {
           LOGGER.error("Error retrieving eco friendly attribute");
       }
       LOGGER.info("*** Product is not Eco Friendly**");
       return false;
   }
   ```

   No método acima, a variável `productRetriever` é usada para buscar o produto e a variável `getAsInteger()` é usado para obter o valor da variável `eco_friendly` atributo. Com base nas consultas GraphQL executadas anteriormente, sabemos que o valor esperado quando a variável `eco_friendly` está definido como &quot;**Sim**&quot; é, na verdade, um número inteiro de **1**.

   Agora que o Modelo do Sling foi atualizado, a marcação de componente precisa ser atualizada para realmente exibir um indicador de **Econômica** baseado no Modelo do Sling.

## Personalização da marcação do Teaser do produto {#customize-markup-product-teaser}

Uma extensão comum de componentes do AEM é modificar a marcação gerada pelo componente. Essa modificação é feita substituindo o [script HTL](https://docs.adobe.com/content/help/pt-BR/experience-manager-htl/using/overview.html) que o componente usa para renderizar sua marcação. A Linguagem de modelo HTML (HTL) é uma linguagem de modelo leve que os componentes do AEM usam para renderizar dinamicamente a marcação com base no conteúdo criado, permitindo que os componentes sejam reutilizados. O Teaser do produto, por exemplo, pode ser reutilizado várias vezes para exibir produtos diferentes.

Em nosso caso, queremos renderizar um banner sobre o teaser para indicar que o produto é &quot;ecológico&quot; com base em um atributo personalizado. O padrão de design para [personalizar a marcação](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) de um componente é, na verdade, padrão para todos os componentes do AEM, não apenas para os Componentes principais da CIF do AEM.

>[!NOTE]
>
> Se você personalizar um componente usando o seletor de produto e categoria da CIF, como este Teaser do produto ou o componente da página da CIF, certifique-se de incluir o `cif.shell.picker` clientlib para as caixas de diálogo do componente. Consulte [Uso do seletor de produto e categoria da CIF](use-cif-pickers.md) para obter detalhes.

1. No IDE, navegue e expanda o `ui.apps` e expanda a hierarquia de pastas para: `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` e inspecionar o `.content.xml` arquivo.

   ![User.apps do Teaser do produto](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   Veja acima a definição de componente para o Teaser do produto em nosso projeto. Observe a propriedade `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Este é um exemplo de criação de um [componente Proxy](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/get-started/using.html#create-proxy-components). Em vez de copiar e colar todos os scripts HTL do Teaser do produto dos Componentes principais da CIF do AEM, podemos usar o `sling:resourceSuperType` para herdar toda a funcionalidade. 

1. Abra o arquivo `productteaser.html`. Esta é uma cópia do `productteaser.html` do [Teaser do produto CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)

   ```html
   <!--/* productteaser.html */-->
   <sly
     data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
     data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
     data-sly-use.actionsTpl="actions.html"
     data-sly-test.isConfigured="${properties.selection}"
     data-sly-test.hasProduct="${product.url}"
   ></sly>
   ```

   Observe que o Modelo do Sling para `MyProductTeaser` é usada e atribuída ao `product` variável.

1. Modificar `productteaser.html` para fazer uma chamada para a `isEcoFriendly` método implementado no exercício anterior:

   ```html
   ...
   <div
     data-sly-test="${isConfigured && hasProduct}"
     class="item__root"
     data-cmp-is="productteaser"
     data-virtual="${product.virtualProduct}"
   >
     <div data-sly-test="${product.showBadge}" class="item__badge">
       <span>${properties.text || 'New'}</span>
     </div>
     <!--/* Insert call to Eco Friendly here */-->
     <div data-sly-test="${product.ecoFriendly}" class="item__eco">
       <span>Eco Friendly</span>
     </div>
     ...
   </div>
   ```

   Ao chamar um método do Modelo do Sling no HTL, a variável `get` e `is` parte do método é solta e a primeira letra é minúscula. So `isShowBadge()` become `.showBadge` e `isEcoFriendly` become `.ecoFriendly`. Com base no valor booleano retornado de `.isEcoFriendly()` determina se a variável `<span>Eco Friendly</span>` é exibida.

   Mais informações sobre `data-sly-test` e outros [Declarações de bloco HTL podem ser encontradas aqui](https://docs.adobe.com/content/help/en/experience-manager-htl/using/htl/block-statements.html#test).

1. Salve as alterações e implante as atualizações no AEM usando suas habilidades Maven em um terminal de linha de comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Abra uma nova janela do navegador e navegue até AEM e o **Console do OSGi** > **Status** > **Modelos Sling**: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. Procurar por `MyProductTeaserImpl` e você deve ver uma linha como a seguinte:

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   Isso indica que o Modelo do Sling foi devidamente implantado e mapeado para o componente correto.

1. Atualize para o **Página inicial Venia** at [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) onde o Teaser do produto foi adicionado.

   ![Mensagem compatível com o ambiente exibida](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   Se o produto tiver a variável `eco_friendly` conjunto de atributos para **Sim**, você deve ver o texto &quot;Ecológico&quot; na página. Tente alternar para produtos diferentes para ver a mudança de comportamento.

1. Em seguida, abra o AEM `error.log` para ver as declarações de log que adicionamos. O `error.log` está localizado em `<AEM SDK Install Location>/crx-quickstart/logs/error.log`.

   Pesquise nos logs de AEM para ver as declarações de log adicionadas no Modelo do Sling:

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > Você também pode ver alguns rastreamentos de pilha se o produto usado no teaser não tiver o `eco_friendly` como parte do conjunto de atributos.

## Adicionar estilos para o emblema compatível com o ambiente {#add-styles}

Nesse momento, a lógica de quando exibir o **Econômica** O selo está funcionando, no entanto, o texto simples pode usar alguns estilos. Em seguida, adicione um ícone e estilos à `ui.frontend` para concluir a implementação.

1. Baixe o [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) arquivo. Isso será usado como a variável **Econômica** selo.
1. Retorne ao IDE e navegue até o `ui.frontend` pasta.
1. Adicione o `eco_friendly.svg` para `ui.frontend/src/main/resources/images` pasta:

   ![SVG compatível com o ambiente adicionado](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. Abra o arquivo `productteaser.scss` at `ui.frontend/src/main/styles/commerce/_productteaser.scss`.
1. Adicione as seguintes regras de Sass dentro do `.productteaser` classe:

   ```scss
   .productteaser {
       ...
       .item__eco {
           width: 60px;
           height: 60px;
           left: 0px;
           overflow: hidden;
           position: absolute;
           padding: 5px;
   
       span {
           display: block;
           position: absolute;
           width: 45px;
           height: 45px;
           text-indent: -9999px;
           background: no-repeat center center url('../resources/images/eco_friendly.svg');
           }
       }
   ...
   }
   ```

   >[!NOTE]
   >
   > Veja [Alterar estilo dos Componentes principais da CIF](./style-cif-component.md) para obter mais detalhes sobre fluxos de trabalho front-end.

1. Salve as alterações e implante as atualizações no AEM usando suas habilidades Maven em um terminal de linha de comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Atualize para o **Página inicial Venia** at [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) onde o Teaser do produto foi adicionado.

   ![Implementação Final do Símbolo Ecológico](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Parabéns {#congratulations}

Você acabou de personalizar seu primeiro componente CIF do AEM. Baixe o [finalização de arquivos de solução aqui](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip).

## Desafio extra {#bonus-challenge}

Revise a funcionalidade do **Novo** selo que já foi implementado no Teaser do produto. Tente adicionar uma caixa de seleção adicional para os autores controlarem quando a função **Econômica** símbolo deve ser exibido. Será necessário atualizar a caixa de diálogo do componente em `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`.

![Novo desafio de implementação do emblema](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## Recursos adicionais {#additional-resources}

- [Arquétipo do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt_BR)
- [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components)
- [Personalizar os Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
- [Personalizar os Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=pt-BR)
- [Introdução ao AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR)
- [Uso do seletor de produto e categoria da CIF](use-cif-pickers.md)
