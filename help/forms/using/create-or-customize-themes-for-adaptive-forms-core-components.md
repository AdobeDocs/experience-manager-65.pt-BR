---
title: Como criar ou personalizar temas do Formulário adaptável?
description: Saiba como criar ou personalizar temas para os Componentes principais do Forms adaptável usando especificações do BEM
keywords: criar tema dos componentes principais dos formulários adaptáveis, criar novo tema, personalizar tema, carregar novo tema, usar tema em formulários, excluir um tema, criar um tema em formulários AEM 6.5
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms,Core Components
exl-id: 9f9b35a3-0479-4179-9fad-994a482c96b6
solution: Experience Manager, Experience Manager Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1939'
ht-degree: 5%

---

# Criar ou personalizar um tema de formulário adaptável {#introduction-to-theme}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |


<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

No AEM Forms 6.5, um tema é uma biblioteca cliente AEM usada para definir os estilos (aparência e comportamento) de um Formulário adaptável. Um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de fundo, cores de estado, transparência, alinhamento e tamanho. Ao aplicar um tema, o estilo especificado é refletido nos componentes correspondentes. Um tema é gerenciado de forma independente sem uma referência a um Formulário adaptável e pode ser reutilizado em vários Forms adaptáveis.

## Temas disponíveis {#available-theme}

O ambiente AEM 6.5 fornece os temas listados abaixo para o Forms adaptável baseado em Componentes principais:

* [Tema Tela de desenho](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema do CAVALETE](https://github.com/adobe/aem-forms-theme-easel)
* [Tema FSI](https://github.com/adobe/aem-forms-theme-fsi)
* [Tema de saúde](https://github.com/adobe/aem-forms-theme-healthcare)
* [Tema público](https://github.com/adobe/aem-forms-theme-public)
* [Tema de fabricação](https://github.com/adobe/aem-forms-theme-manufacturing)

## Compreender a estrutura dos temas {#understanding-structure-of-theme}

Um tema é um pacote que abrange o arquivo CSS, os arquivos JavaScript e os recursos (como ícones) que definem o estilo do Forms adaptável. Um tema do Formulário adaptável segue uma organização específica, consistindo nos seguintes componentes:

* `src/theme.scss`: esta pasta inclui o arquivo CSS que tem um amplo impacto sobre todo o tema. Ele serve como um local centralizado para definir e gerenciar o estilo e o comportamento do tema. Ao fazer edições nesse arquivo, você pode fazer alterações aplicadas universalmente no tema, influenciando a aparência e a funcionalidade das Páginas adaptáveis do Forms e do AEM Sites.

* `src/site`: esta pasta contém arquivos CSS que são aplicados à página inteira de um Site AEM. Esses arquivos consistem em códigos e estilos que afetam a funcionalidade geral e o layout da página do seu site AEM. Quaisquer modificações feitas aqui serão refletidas em todas as páginas do site.

* `src/components`: os arquivos CSS nesta pasta são projetados para componentes principais individuais do AEM. Cada pasta dedicada de um componente inclui um arquivo `.scss` que estimula esse componente específico em um Formulário adaptável. Por exemplo, o arquivo `/src/components/button/_button.scss` contém informações de estilo para o componente Adaptive Forms Button.

  ![Estrutura de Tema da Tela](/help/forms/using/assets/component-based-theme-folder-structure.png)

* `src/resources`: esta pasta contém arquivos estáticos, como ícones, logotipos e fontes. Esses recursos são usados para aprimorar os elementos visuais e o design geral do tema.

## Criar um tema

O AEM Forms 6.5 fornece os temas listados abaixo para o Adaptive Forms baseado em Componentes principais.

* [Tema Tela de desenho](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema do CAVALETE](https://github.com/adobe/aem-forms-theme-easel)
* [Tema público](https://github.com/adobe/aem-forms-theme-public)
* [Tema de fabricação](https://github.com/adobe/aem-forms-theme-manufacturing)

Você pode [personalizar qualquer um desses temas para criar um tema](#customize-a-theme-core-components).

## Personalizar um tema {#customize-a-theme-core-components-based-adaptive-forms}

A personalização de um tema refere-se ao processo de modificação e personalização da aparência de um tema. Ao personalizar um tema, você altera seus elementos de design, layout, cores, tipografia e, às vezes, o código subjacente. Isso permite criar uma aparência exclusiva e personalizada para seu site ou aplicativo, mantendo a estrutura básica e a funcionalidade fornecidas pelo tema.

>[!NOTE]
>
> * Use o Gerenciador de pacotes para implantar um tema em todas as instâncias do Autor e do Publish.
> * Uma biblioteca de temas de cliente é importada ou exportada pelo Gerenciador de pacotes como qualquer outro pacote.

### Pré-requisitos para personalizar um tema {#prerequisites}

* [Habilite os Componentes principais adaptáveis do Forms](/help/forms/using/enable-adaptive-forms-core-components.md) para o seu ambiente.

* Instale a última versão do [Apache Maven.](https://maven.apache.org/download.cgi) O Apache Maven é uma ferramenta de automação de compilação comumente usada para projetos Java™. A instalação da versão mais recente garante que você tenha as dependências necessárias para a personalização de temas.

* Saiba como criar uma [biblioteca do cliente no Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html?lang=pt-BR). O AEM fornece bibliotecas de clientes, que permitem armazenar o código do lado do cliente no repositório, organizá-lo em categorias e definir quando e como cada categoria de código deve ser entregue ao cliente.

* Instale um editor de texto simples. Por exemplo, Microsoft® Visual Studio Code. O uso de um editor de texto simples, como o Microsoft® Visual Studio Code, fornece um ambiente amigável para a edição e modificação de arquivos de tema.

* Certifique-se de que o ambiente do AEM Forms esteja em funcionamento.

### Considerações para personalizar um tema {#consideration}

* Use o [projeto do Arquétipo usado para habilitar os Componentes principais do Adaptive Forms](/help/forms/using/enable-adaptive-forms-core-components.md) no seu ambiente para personalizar seus temas.

* Ao publicar um Formulário adaptável, as bibliotecas de clientes não são publicadas automaticamente na instância do Publish. Certifique-se de publicar manualmente a biblioteca do cliente referenciada em um Formulário adaptável em seus ambientes do Publish.

* O Adobe recomenda não alterar os nomes de classe das bibliotecas de clientes.

### Personalizar um tema {#customize-a-theme-core-components}

A criação ou personalização de um tema é um processo de várias etapas. Execute as etapas na ordem listada para criar/personalizar o tema:

1. [Clonar um tema](#clone-git-repo-of-theme)
1. [Personalizar a aparência do tema](#customize-the-theme)
1. [Pronto o tema para implantação local](#generate-the-clientlib)
1. [Implantar o tema em um ambiente local](#deploy-the-theme-on-a-local-environment)
1. [Implantar o tema no ambiente de produção](#5-deploy-a-theme-on-your-production-environment)

<!--
 ![Theme Customization workflow](/help/forms/using/assets/custom-theme-steps.png)
-->

Os exemplos fornecidos no documento são baseados no tema **Tela**, mas você pode clonar qualquer tema e personalizá-lo usando as mesmas instruções. Essas instruções se aplicam a qualquer tema, permitindo modificar temas de acordo com suas necessidades específicas.

#### 1. Clonar o repositório Git do tema {#clone-git-repo-of-theme}

Para clonar um tema para os Componentes principais com base no Adaptive Forms, escolha um dos seguintes temas:

* [Tema Tela de desenho](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema do CAVALETE](https://github.com/adobe/aem-forms-theme-easel)

Execute as seguintes instruções para clonar um tema:

1. Abra o prompt de comando ou a janela do terminal no ambiente de desenvolvimento local.

1. Execute o comando `git clone` para clonar um tema.

   ```
      git clone [Path of Git Repository of the theme]
   ```

   Substituir o [Caminho do Repositório Git do tema] pela URL real do Repositório Git correspondente do tema

   Por exemplo, para clonar o tema da Tela de Pintura, execute o seguinte comando:

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

1. Selecione **Confiar nos autores de todos os arquivos da pasta pai** e clique em **Sim, eu confio nos autores**.

Depois de executar o comando com êxito, você terá uma cópia local do tema disponível em sua máquina na pasta `aem-forms-theme-canvas`.

#### 2. Personalizar o tema {#customize-the-theme}

Você tem a flexibilidade de personalizar componentes individuais ou fazer alterações no nível do tema usando as variáveis globais de um tema. A modificação de variáveis globais tem um efeito em cascata em todos os componentes individuais. Por exemplo, você pode utilizar variáveis globais para alterar a cor da borda de todos os componentes em um Formulário adaptável ou aplicar uma cor de preenchimento vibrante aos botões de Chamada para ação (CTA). É possível:

* [Definir estilos de nível de tema](#theme-customization-global-level)

* [Definir estilos de nível de componente](#component-based-customization)

##### Definir estilos de nível de tema {#theme-customization-global-level}

O arquivo `variable.scss` contém as variáveis globais do tema. Ao atualizar essas variáveis, é possível fazer alterações relacionadas ao estilo no nível do tema. Para aplicar estilos de nível de tema, siga estas etapas:

1. Abra o arquivo `<your-theme-sources>/src/site/_variables.scss` para edição.
1. Altere o valor de qualquer propriedade. Por exemplo, a cor de erro padrão é vermelha. Para alterar a cor do erro de vermelho para azul, altere o código hexadecimal de cor da variável `$error`. Por exemplo, `$error: #196ee5`.

   ![Exemplo: Cor do erro definida para azul](/help/forms/using/assets/theme-level-changes.png)

1. Salvar e fechar o arquivo.


Da mesma forma, você pode usar o arquivo `variable.scss` para definir a família e o tipo de fonte, as cores do tema e da fonte, o tamanho da fonte, o espaçamento do tema, o ícone de erro, os estilos de borda do tema e mais variáveis que afetam vários componentes do Formulário adaptável.

##### Definir estilos de nível de componente {#component-based-customization}

Você também tem a opção de personalizar a fonte, a cor, o tamanho e outras propriedades CSS de componentes principais específicos do Formulário adaptável, como botões, caixas de seleção, contêineres, rodapés e muito mais. Ao editar o arquivo CSS associado ao componente específico, é possível alinhar o estilo com a marca da organização. Para personalizar o estilo de um componente, siga estas etapas:

1. Abra o arquivo `<your-theme-sources>/src/components/<component>/<component.scss>` para edição. Por exemplo, para alterar a cor da fonte do componente de botão, abra o arquivo `<your-theme-sources>/src/components/button/button.scss`.
1. Altere o valor de qualquer de acordo com suas necessidades. Por exemplo, para alterar a cor do componente de botão ao passar o mouse para Verde, altere o valor da propriedade `color: $white` na classe `cmp-adaptiveform-button__widget:hover` para o código hexadecimal #12b453 ou qualquer outro tom de verde. O código final é semelhante ao seguinte:

   ```
    .cmp-adaptiveform-button__widget:hover {
    background: $dark-gray;
    color: #12b453;
    }
   ```


1. Salvar e fechar o arquivo.

<!--

   ![Example: Hover color set to green](/help/forms/using/assets/button-customization.png)

-->

>[!NOTE]
>
> Quando um estilo é definido no nível do tema e do componente, o estilo definido no nível do componente tem prioridade.

#### 3. Prepare o tema para implantação {#generate-the-clientlib}

Para implantar um tema em uma instância do AEM, ele precisa ser convertido em uma Biblioteca do cliente. Siga estas etapas para converter o tema em uma biblioteca do cliente:

1. Abra o prompt de comando ou a janela do terminal.
1. Navegue até a pasta `<your-theme-sources>`. Por exemplo, `C:\aem-forms-theme-canvas`
1. Execute o seguinte comando:

   ```
      npm run create-clientlib --category=adaptiveform.theme.[yourtheme]
   ```

   Substitua `[yourtheme]` pelo nome do seu tema personalizado. Por exemplo, se o nome do tema personalizado for `customcanvastheme`, execute o seguinte comando

   ```
       npm run create-clientlib --category=adaptiveform.theme.customcanvastheme
   ```

   Na execução bem-sucedida do comando, uma pasta da biblioteca do cliente é criada em `themerepo\theme-clientlibs\[yourtheme]`.

   ![Geração de Biblioteca de Cliente](/help/forms/using/assets/clientlib_created.png)


   ![Local da Biblioteca do Cliente](/help/forms/using/assets/adaptiveform.theme.easel.png)

#### 4. Implantar o tema em um ambiente local {#deploy-the-theme-on-a-local-environment}

Para implantar o tema no ambiente de desenvolvimento ou teste local, siga estas etapas:

1. Copie a Biblioteca do cliente, criada na seção anterior, para o projeto do Arquétipo, no seguinte caminho:

   `/ui.apps/src/main/content/jcr_root/apps/[AEM Archetype Project Folder]/clientlibs/<yourtheme>`

1. Abra o prompt de comando ou o terminal.
1. Navegue até o diretório raiz do seu projeto do Arquétipo AEM, o projeto usado para ativar os Componentes principais do formulário adaptável.
1. Execute o seguinte comando para implantar o tema personalizado no ambiente:

   `mvn clean install`

   ![Compilação da Biblioteca de Clientes](/help/forms/using/assets/mvndeploy.png)

<!--

#### 5. Test the theme with a local Adaptive Form {#test-the-theme-with-a-local-adaptive-form}

To apply and test the customized theme with an Adaptive Form:

**Apply theme while creating an Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Select **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Click **Create** > **Adaptive Forms**. The wizard for creating Adaptive Form opens.

1. Select the core component template in the **Source** tab.
1. Select the theme in the **Style** tab.
1. Click **Create**.

An Adaptive Form with the selected theme is created. 

**Apply theme to an existing Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Select **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Select an Adaptive Form and click Properties. 

1. For the **Theme Client Library** option, select the theme. 

1. Click **Save & Close**.

The selected theme is applied to the Adaptive Form. 
-->

#### 5. Implantar um tema no ambiente de produção {#deploy-theme}

Depois de testar com êxito o tema no ambiente de desenvolvimento local, você pode prosseguir para implantar o tema nos ambientes de produção, incluindo as instâncias do Autor e do Publish. Siga estas etapas para implantar o tema em seus ambientes de produção:

1. Faça logon no ambiente AEM.
1. Abra o Gerenciador de pacotes. A URL padrão é `https://localhost:4502/crx/packmgr/index.jsp`.
1. Clique em **Carregar Pacote** e em **Procurar**.
1. Navegue até `[AEM Archetype Project Folder]\all\target[appid].all-[version].zip` e selecione-o. Clique em **Abrir**.
1. Clique em Instalar. Repita a etapa em todos os ambientes de produção.


Após a instalação do pacote, o tema fica disponível para seleção.

![Biblioteca de Temas do Cliente](/help/forms/using/assets/themeclientlibrary.png)

>[!NOTE]
>
>
> Caso encontre dificuldades ao acessar a caixa de diálogo de logon em uma instância de publicação para instalar o pacote por meio do Gerenciador de Pacotes, tente fazer logon pela seguinte URL: `http://[Publish Server URL]:[PORT]/system/console`. Isso permite o acesso para fazer logon na instância do Publish, permitindo continuar com o processo de instalação.

## Aplicar um tema a um formulário adaptável {#using-theme-in-adaptive-form}

As etapas para aplicar um tema a um Formulário adaptável são:

1. Faça logon na instância de autor local do AEM.
1. Insira suas credenciais na página de logon do Experience Manager. Selecione **Adobe Experience Manager** > **Forms** > **Forms e Documentos**.
1. Clique em **Criar** > **Forms Adaptável**.
1. Selecione um modelo dos Componentes principais adaptáveis do Forms e clique em **Avançar**. A **Adicionar propriedades** aparece
1. Especifique o **Nome** do formulário adaptável.


   >[!NOTE]
   >
   > * Por padrão, o tema `adaptiveform.theme.canvas3` é selecionado.
   > * Você pode escolher um tema diferente do menu suspenso **Biblioteca de Temas do Cliente**.

1. Clique em **Criar**.

Os temas do formulário adaptável são usados como parte de um modelo de formulário adaptável para definir o estilo ao criar um formulário adaptável.

## Excluir um tema {#delete-a-theme}

Para remover temas não utilizados ou indesejados:

1. Faça logon na instância do Author.
1. Abrir `http://[Publish Server URL]:[PORT]/crx/de/index.jsp`
1. Vá até `apps/[AEM Archetype Project Folder]/clientlibs/[yourtheme]`.
1. Exclua a pasta de tema e salve as alterações.


## Perguntas frequentes {#faq}

**P:** Qual personalização tem prioridade ao fazer personalizações em uma pasta de tema no nível global e no nível do componente?

**Ans:** Quando um estilo é definido nos níveis de tema e componente, o estilo definido no nível do componente tem prioridade.

**P:** Que etapas devem ser executadas se o tema personalizado não estiver visível na **[!UICONTROL Biblioteca de Temas do Cliente]**?

**Ans:** Se o tema personalizado não aparecer no menu suspenso **[!UICONTROL Biblioteca de Temas do Cliente]**, siga estas etapas:

1. Navegue até o local onde você adicionou a biblioteca de temas personalizados do cliente. O caminho recomendado é `/ui.apps/src/main/content/jcr_root/apps[AEM Archetype Project Folder]/clientlibs/<yourtheme>`.

1. Abra o arquivo `.content.xml` e inclua os seguintes metadados:

   ```
       formstheme:true
       allowproxy:true
   ```

1. Salve o arquivo e implante novamente o tema.

## Consulte também:

* [Criar um formulário adaptável baseado nos Componentes principais](create-an-adaptive-form-core-components.md)
* [Usar o editor de regras para adicionar comportamento dinâmico ao formulário](rule-editor.md)
* [Criar ou personalizar temas para Componentes principais com base no Forms adaptável](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [Criar um modelo para os Componentes principais com base no Forms adaptável](template-editor.md)
* [Criar ou adicionar um formulário adaptável a uma página do AEM Sites ou a um fragmento de experiência](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Modelos de temas de exemplo e modelos de dados de formulário](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=pt-BR)
