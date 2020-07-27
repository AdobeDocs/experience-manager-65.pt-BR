---
title: Criação de temas de formulário adaptáveis personalizados
seo-title: Criação de temas de formulário adaptáveis personalizados
description: Um tema de formulário adaptável é uma biblioteca de cliente do AEM que você usa para definir os estilos (aparência) de um formulário adaptável. Saiba como criar temas de formulário adaptáveis personalizados.
seo-description: Um tema de formulário adaptável é uma biblioteca de cliente do AEM que você usa para definir os estilos (aparência) de um formulário adaptável. Saiba como criar temas de formulário adaptáveis personalizados.
uuid: b25df10e-b07c-4e9d-a799-30f1c6fb3c44
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 437e6581-4eb1-4fbd-a6da-86b9c90cec89
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---


# Criação de temas de formulário adaptáveis personalizados {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>Os AEM Forms fornecem o recurso do Editor [de](/help/forms/using/themes.md) Temas para criar e modificar [temas](/help/forms/using/themes.md)de formulários adaptáveis. Execute as etapas listadas neste artigo somente se você tiver atualizado de uma versão que não tem o Editor [de](/help/forms/using/themes.md) Temas e tiver um investimento existente em temas criados usando arquivos Menos/CSS (método editor pré-temático).

## Pré-requisitos {#prerequisites}

* Conhecimento da estrutura LESS (Leaner CSS)
* Como criar uma biblioteca de clientes no Adobe Experience Manager
* [Criar um modelo](/help/forms/using/custom-adaptive-forms-templates.md) de formulário adaptável para usar o tema criado

## Adaptive form theme {#adaptive-form-theme}

Um tema **de formulário** adaptável é uma biblioteca do cliente AEM que você usa para definir os estilos (aparência e comportamento) de um formulário adaptável.

Você cria um modelo **** adaptável e aplica o tema ao modelo. Use esse modelo personalizado para criar um formulário **** adaptável.

![Formulário adaptável e biblioteca do cliente](assets/hierarchy.png)

## Para criar um tema de formulário adaptável {#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>O procedimento a seguir é descrito usando nomes de amostra para objetos AEM, como nó, propriedades e pastas.
>
>Se você seguir essas etapas usando os nomes, o modelo resultante deverá aparecer de forma semelhante ao seguinte instantâneo:

![Instantâneo](assets/thumbnail.png)do formulário adaptável com tema de floresta **Figura:** *Exemplo de tema da floresta*

1. Crie um nó do tipo `cq:ClientLibraryFolder` abaixo do `/apps`nó.

   Por exemplo, crie o seguinte nó:

   `/apps/myAfThemes/forestTheme`

1. Adicione uma propriedade de string com vários valores `categories` ao nó e defina seu valor adequadamente.

   Por exemplo, defina a propriedade como: `af.theme.forest`.

   ![Instantâneo do repositório CRX](assets/3-2.png)

1. Adicione duas pastas `less` e `css`um arquivo `css.txt` ao nó criado na etapa 1:

   * `less` pasta: Contém os arquivos de `less` variável nos quais você define as `less` variáveis e `less mixins` que são usados para gerenciar os estilos .css.

      Essa pasta consiste em arquivos `less` variáveis, arquivos `less` de mixagem, `less` arquivos que definem estilos usando misturas e variáveis. E todos esses arquivos a menos são importados em styles.less.

   * `css`pasta: Contém os arquivos .css nos quais você define os estilos estáticos a serem usados no tema.

   **Menos arquivos** de variáveis: Esses são os arquivos, nos quais você define ou substitui as variáveis usadas na definição de estilos CSS.

   Os formulários adaptáveis fornecem variáveis OOTB definidas nos seguintes arquivos .less:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   Os formulários adaptáveis também fornecem variáveis de terceiros definidas em:

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   Você pode usar menos variáveis fornecidas com formulários adaptáveis, pode substituir essas variáveis ou criar novas variáveis menos.

   >[!NOTE]
   >
   >Ao importar os arquivos do pré-processador menor, na instrução import especifique o caminho relativo dos arquivos.

   Exemplo de variáveis de substituição:

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   Para substituir as `less`variáveis:

   1. Importar variáveis de formulário adaptável padrão:

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. Em seguida, importe o arquivo less que inclui variáveis substituídas.

   Amostra de novas definições de variáveis:

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **Menos arquivos de mixagem:** É possível definir as funções que aceitam variáveis como argumentos. A saída dessas funções são os estilos resultantes. Use essas combinações em estilos diferentes para evitar a repetição de estilos CSS.

   Os formulários adaptáveis fornecem misturas OOTB definidas em:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   Formulários adaptáveis também fornecem combinações de terceiros definidas em:

   * `/apps/clientlibs/fd/af/third-party/less/mixins.less`

   Definição da mistura de amostra:

   ```css
   .rounded-corners (@radius) {
     -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
     -ms-border-radius: @radius;
     -o-border-radius: @radius;
     border-radius: @radius;
   }
   
   .border(@color, @type, @size) {
      border: @color @size @type;
   }
   ```

   **Arquivo Styles.less:** Use esse arquivo para incluir todos os arquivos menores (variáveis, mixins, estilos) que você precisa usar na biblioteca do cliente.

   No arquivo de amostra a seguir, a declaração de importação pode ser colocada em qualquer ordem. `styles.less`

   As instruções para importar os seguintes arquivos .less são obrigatórias:

   * `globalvariables.less`
   * `layoutvariables.less`
   * `components.less`
   * `layouts.less`

   ```css
   @import "../../../clientlibs/fd/af/guidetheme/common/less/globalvariables.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layoutvariables.less";
   @import "forestTheme-variables";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/components.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layouts.less";
   
   /* custom styles */
   
   .guidetoolbar {
     input[type="button"], button, .button {
       .rounded-corners (@button-radius);
       &:hover {
         background-color: @button-hover-bg-color;
       }
       &:focus {
         background-color: @button-focus-bg-color;
       }
     }
   }
   
   form {
       background-image: url(../images/forest.png);
    background-repeat: no-repeat;
    background-size: 100%;
   }
   ```

   O `css.txt` contém os caminhos de arquivos .css a serem baixados para a biblioteca.

   Por exemplo:

   ```javascript
   #base=/apps/clientlibs/fd/af/third-party/css
   bootstrap.css
   
   #base=less
   styles.less
   
   #base=/apps/clientlibs/fd/xfaforms/xfalib/css
   datepicker.css
   listboxwidget.css
   scribble.css
   dialog.css
   ```

   >[!NOTE]
   >
   >O arquivo styles.less não é obrigatório. Isso significa que não é necessário criar esse arquivo, se você não tiver definido estilos, variáveis ou combinações personalizados.
   >
   >No entanto, se você não criar um arquivo style.less, no arquivo css.txt, será necessário excluir as barras de comentário da seguinte linha:
   >
   >**`#base=less`**
   >
   >E comente a seguinte linha:
   >
   >**`styles.less`**

## Para usar um tema em um formulário adaptável {#to-use-a-theme-in-an-adaptive-form}

Depois de criar um tema de formulário adaptável, execute as seguintes etapas para usar esse tema em um formulário adaptável:

1. Para incluir o tema criado em [para criar uma seção de tema](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p) de formulário adaptável, crie uma página personalizada do tipo `cq:Component`.

   Por exemplo, `/apps/myAfCustomizations/myAfPages/forestPage`

   1. Adicione uma `sling:resourceSuperType` propriedade e defina seu valor como `fd/af/components/page/base`.

      ![Instantâneo do repositório CRX](assets/1-2.png)

   1. Para usar um tema na página, é necessário adicionar um arquivo de substituição library.jsp ao nó.

      Em seguida, importe o tema criado em Para criar uma seção adaptativa do tema de formulário deste artigo.

      O trecho de código de amostra a seguir importa o `af.theme.forest` tema.

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **Opcional**: Na página personalizada, substitua o header.jsp, o footer.jsp e o body.jsp, conforme necessário.

1. Crie um modelo personalizado (por exemplo: `/apps/myAfCustomizations/myAfTemplates/forestTemplate`) cujo jcr:content aponta para a página personalizada criada na etapa anterior (por exemplo: `myAfCustomizations/myAfPages/forestPage)`.

   ![Instantâneo do repositório CRX](assets/2-1.png)

1. Crie um formulário adaptável usando o modelo criado na etapa anterior. A aparência do formulário adaptável é definida pelo tema criado em Para criar uma seção adaptativa do tema de formulário deste artigo.

