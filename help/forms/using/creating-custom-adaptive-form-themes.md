---
title: Criação de temas de formulário adaptáveis personalizados
description: Um tema de formulário adaptável é uma biblioteca do cliente Adobe Experience Manager usada para definir os estilos (aparência) de um formulário adaptável. Saiba como criar temas de formulário adaptáveis personalizados.
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 73b0057f-082d-4502-90e2-5e41b52c1185
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# Criação de temas de formulário adaptáveis personalizados {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>O Adobe Experience Manager (AEM) Forms fornece a [Editor de temas](/help/forms/using/themes.md) capacidade de criar e modificar formulários adaptáveis [temas](/help/forms/using/themes.md). Execute as etapas listadas neste artigo somente se tiver atualizado de uma versão que não tenha [Editor de temas](/help/forms/using/themes.md) e você tem um investimento existente em temas criados usando arquivos Less/CSS (método do editor de pré-tema).

## Pré-requisitos {#prerequisites}

* Conhecimento da estrutura LESS (Leaner CSS)
* Como criar uma biblioteca do cliente no Adobe Experience Manager
* [Criação de um modelo de formulário adaptável](/help/forms/using/custom-adaptive-forms-templates.md) para usar o tema que você cria

## Tema do formulário adaptável {#adaptive-form-theme}

Um **tema de formulário adaptável** é uma biblioteca de cliente AEM usada para definir os estilos (aparência e comportamento) de um formulário adaptável.

Você cria um **modelo adaptável** e aplique o tema ao modelo. Você pode usar esse modelo personalizado para criar um **formulário adaptável**.

![Formulário adaptável e biblioteca do cliente](assets/hierarchy.png)

## Para criar um tema de formulário adaptável {#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>O procedimento a seguir é descrito usando nomes de exemplo para objetos AEM, como nós, propriedades e pastas.
>
>Se você seguir essas etapas usando os nomes, o modelo resultante deverá ser semelhante ao seguinte:

![Instantâneo do Formulário adaptável com tema de floresta](assets/thumbnail.png)
**Figura:** *Amostra de tema da floresta*

1. Criar um nó do tipo `cq:ClientLibraryFolder` no `/apps`nó.

   Por exemplo, crie o seguinte nó:

   `/apps/myAfThemes/forestTheme`

1. Adicionar uma propriedade de cadeia de caracteres de vários valores `categories` ao nó e defina seu valor adequadamente.

   Por exemplo, defina a propriedade como: `af.theme.forest`.

   ![Instantâneo do repositório CRX](assets/3-2.png)

1. Adicionar duas pastas, `less` e `css`e um arquivo `css.txt` ao nó criado na etapa 1:

   * `less` pasta: Contém o `less` arquivos variáveis nos quais você define a variável `less` variáveis e `less mixins` que são usados para gerenciar os estilos .css.

     Esta pasta consiste em `less` arquivos variáveis, `less` mixin de arquivos, `less` arquivos definindo estilos usando mixins e variáveis. E todos esses menos arquivos são importados em style.less.

   * `css`pasta: contém os arquivos .css nos quais você define os estilos estáticos a serem usados no tema.

   **Menos arquivos de variáveis**: esses são os arquivos em que você define ou substitui as variáveis usadas na definição de estilos CSS.

   Os formulários adaptáveis fornecem variáveis OOTB definidas nos seguintes arquivos .less:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   Os formulários adaptáveis também fornecem variáveis de terceiros definidas no:

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   Você pode usar menos variáveis fornecidas com formulários adaptáveis, pode substituir essas variáveis ou pode criar novas menos variáveis.

   >[!NOTE]
   >
   >Ao importar os arquivos do pré-processador less, na instrução import especifique o caminho relativo dos arquivos.

   Variáveis de substituição de exemplo:

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   Para substituir o `less`variáveis:

   1. Importar variáveis de formulário adaptáveis padrão:

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. Em seguida, importe o menor arquivo que inclui variáveis substituídas.

   Exemplo de novas definições de variáveis:

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **Menos arquivos mixin:** Você pode definir as funções que aceitam variáveis como argumentos. A saída dessas funções são os estilos resultantes. Use esses mixins em diferentes estilos para evitar a repetição de estilos CSS.

   Os formulários adaptáveis fornecem mixins OOTB definidos em:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   Os formulários adaptáveis também fornecem mixins de terceiros definidos em:

   * `/apps/clientlibs/fd/af/third-party/less/mixins.less`

   Definição de mixin de exemplo:

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

   **Arquivo Styles.less:** Use esse arquivo para incluir menos arquivos (variáveis, mixins, estilos) que você deve usar na biblioteca do cliente.

   Na amostra a seguir `styles.less` a instrução import pode ser colocada em qualquer ordem.

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

   A variável `css.txt` contém os caminhos de arquivos .css a serem baixados para a biblioteca.

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
   >O arquivo style.less não é obrigatório. Isso significa que não é necessário criar esse arquivo se você não tiver definido estilos, variáveis ou mixins personalizados.
   >
   >No entanto, se você não criar um arquivo style.less, no arquivo css.txt, remova o comentário da seguinte linha:
   >
   >**`#base=less`**
   >
   >E comente a seguinte linha:
   >
   >**`styles.less`**

## Para usar um tema em um formulário adaptável {#to-use-a-theme-in-an-adaptive-form}

Depois de criar um tema de formulário adaptável, execute as seguintes etapas para usar esse tema em um formulário adaptável:

1. Para incluir o tema criado em [para criar um tema de formulário adaptável](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p) , crie uma página personalizada do tipo `cq:Component`.

   Por exemplo, `/apps/myAfCustomizations/myAfPages/forestPage`

   1. Adicionar um `sling:resourceSuperType` propriedade e defina seu valor como `fd/af/components/page/base`.

      ![Instantâneo do repositório CRX](assets/1-2.png)

   1. Para usar um tema na página, você deve adicionar um arquivo de substituição library.jsp ao nó.

      Em seguida, você pode importar o tema criado na seção Para criar um tema de formulário adaptável deste artigo.

      O trecho de código de amostra a seguir importa o `af.theme.forest` tema.

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **Opcional**: na página personalizada, substitua header.jsp, footer.jsp e body.jsp, conforme necessário.

1. Criar um modelo personalizado (por exemplo: `/apps/myAfCustomizations/myAfTemplates/forestTemplate`) cujo jcr:content aponta para a página personalizada criada na etapa anterior (por exemplo: `myAfCustomizations/myAfPages/forestPage)`.

   ![Instantâneo do repositório CRX](assets/2-1.png)

1. Crie um Formulário adaptável usando o modelo criado na etapa anterior. A aparência do formulário adaptável é definida pelo tema criado na seção Para criar um tema de formulário adaptável deste artigo.
