---
title: Criação de temas de formulário adaptáveis personalizados
seo-title: Creating custom adaptive form themes
description: Um tema de formulário adaptável é uma biblioteca cliente AEM que você usa para definir os estilos (aparência e comportamento) de um formulário adaptável. Saiba como criar temas de formulário adaptáveis personalizados.
seo-description: An adaptive form theme is an AEM client library that you use to define the styles (look and feel) for an adaptive form. Learn how you can create custom adaptive form themes.
uuid: b25df10e-b07c-4e9d-a799-30f1c6fb3c44
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 437e6581-4eb1-4fbd-a6da-86b9c90cec89
exl-id: 73b0057f-082d-4502-90e2-5e41b52c1185
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Criação de temas de formulário adaptáveis personalizados {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>A AEM Forms fornece a [Editor de Temas](/help/forms/using/themes.md) capacidade de criar e modificar formulários adaptáveis [temas](/help/forms/using/themes.md). Execute as etapas listadas neste artigo somente se tiver atualizado de uma versão que não tem [Editor de Temas](/help/forms/using/themes.md) e você tem um investimento existente em temas criados usando arquivos Less/CSS (método de editor pré-tema).

## Pré-requisitos {#prerequisites}

* Conhecimento da estrutura MENOS (CSS mais importante)
* Como criar uma biblioteca do cliente no Adobe Experience Manager
* [Criação de um modelo de formulário adaptável](/help/forms/using/custom-adaptive-forms-templates.md) para usar o tema que você criar

## Tema de formulário adaptável {#adaptive-form-theme}

Um **tema de formulário adaptável** é uma biblioteca cliente AEM que você usa para definir os estilos (aparência e comportamento) de um formulário adaptável.

Você cria um **modelo adaptável** e aplicar o tema ao modelo. Em seguida, use este modelo personalizado para criar um **formulário adaptável**.

![Formulário adaptável e biblioteca do cliente](assets/hierarchy.png)

## Para criar um tema de formulário adaptável {#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>O procedimento a seguir é descrito usando nomes de exemplo para objetos AEM como nó, propriedades e pastas.
>
>Se você seguir essas etapas usando os nomes, o modelo resultante deverá aparecer de forma semelhante ao seguinte instantâneo:

![Instantâneo do formulário adaptável com tema de floresta](assets/thumbnail.png)
**Figura:** *Amostra de Tema da Floresta*

1. Criar um nó do tipo `cq:ClientLibraryFolder` nos termos do `/apps`nó .

   Por exemplo, crie o seguinte nó:

   `/apps/myAfThemes/forestTheme`

1. Adicionar uma propriedade de string com vários valores `categories` no nó e defina seu valor adequadamente.

   Por exemplo, defina a propriedade como: `af.theme.forest`.

   ![Instantâneo do repositório CRX](assets/3-2.png)

1. Adicionar duas pastas, `less` e `css`e um arquivo `css.txt` para o nó criado na etapa 1:

   * `less` pasta: Contém o `less` os arquivos variáveis nos quais você define a variável `less` variáveis e `less mixins` usados para gerenciar os estilos .css.

      Esta pasta consiste em `less` arquivos variáveis, `less` arquivos mixin, `less` arquivos que definem estilos usando mixins e variáveis. E todos esses arquivos menores são importados em styles.less.

   * `css`pasta: Contém os arquivos .css nos quais você define os estilos estáticos a serem usados no tema.

   **Menos arquivos de variáveis**: Esses são os arquivos, onde você define ou substitui as variáveis usadas na definição de estilos de CSS.

   Os formulários adaptáveis fornecem variáveis OOTB definidas nos seguintes arquivos .less:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   Os formulários adaptáveis também fornecem variáveis de terceiros definidas em:

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   Você pode usar menos variáveis fornecidas com formulários adaptáveis, pode substituir essas variáveis ou criar novas variáveis menos.

   >[!NOTE]
   >
   >Ao importar os arquivos do menos pré-processador, na instrução import, especifique o caminho relativo dos arquivos.

   Exemplo de variáveis de substituição:

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   Para substituir o `less`variáveis:

   1. Importar variáveis de formulário adaptável padrão:

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. Em seguida, importe o arquivo less que inclui variáveis substituídas.

   Amostra de novas definições de variável:

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **Menos arquivos mixin:** É possível definir as funções que aceitam variáveis como argumentos. A saída dessas funções são os estilos resultantes. Use essas combinações em estilos diferentes para evitar a repetição de estilos de CSS.

   Os formulários adaptáveis fornecem combinações de OOTB definidas em:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   Os formulários adaptáveis também fornecem mixins de terceiros definidos em:

   * `/apps/clientlibs/fd/af/third-party/less/mixins.less`

   Definição de mistura de amostra:

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

   Na amostra a seguir `styles.less` , a declaração de importação pode ser colocada em qualquer ordem.

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

   O `css.txt` contém os caminhos dos arquivos .css a serem baixados para a biblioteca.

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
   >O arquivo styles.less não é obrigatório. Isso significa que não é necessário criar esse arquivo, caso não tenha definido estilos, variáveis ou mixins personalizados.
   >
   >No entanto, se você não criar um arquivo style.less, no arquivo css.txt, será necessário remover o comentário da seguinte linha:
   >
   >**`#base=less`**
   >
   >E comente a seguinte linha:
   >
   >**`styles.less`**

## Para usar um tema em um formulário adaptável {#to-use-a-theme-in-an-adaptive-form}

Depois de criar um tema de formulário adaptável, execute as seguintes etapas para usar esse tema em um formulário adaptável:

1. Para incluir o tema criado em [para criar um tema de formulário adaptável](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p) seção , crie uma página personalizada do tipo `cq:Component`.

   Por exemplo, `/apps/myAfCustomizations/myAfPages/forestPage`

   1. Adicione um `sling:resourceSuperType` e defina seu valor como `fd/af/components/page/base`.

      ![Instantâneo do repositório CRX](assets/1-2.png)

   1. Para usar um tema na página, você precisa adicionar um arquivo de substituição library.jsp ao nó .

      Em seguida, importe o tema criado na seção Para criar um tema de formulário adaptável deste artigo.

      O trecho de código de amostra a seguir importa a variável `af.theme.forest` tema.

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **Opcional**: Na página personalizada, substitua o header.jsp, o footer.jsp e o body.jsp, conforme necessário.

1. Crie um modelo personalizado (por exemplo: `/apps/myAfCustomizations/myAfTemplates/forestTemplate`) cujo jcr:content aponta para uma página personalizada criada na etapa anterior (por exemplo: `myAfCustomizations/myAfPages/forestPage)`.

   ![Instantâneo do repositório CRX](assets/2-1.png)

1. Crie um formulário adaptável usando o modelo criado na etapa anterior. A aparência do formulário adaptável é definida pelo tema criado na seção Para criar um tema de formulário adaptável deste artigo.
