---
title: Criar carta
seo-title: Criar carta
description: 'Este tópico fornece as etapas para criar uma carta, adicionar módulos de dados e anexos a ela e pré-visualização no Gerenciamento de correspondência. '
seo-description: 'Este tópico fornece as etapas para criar uma carta, adicionar módulos de dados e anexos a ela e pré-visualização no Gerenciamento de correspondência. '
uuid: b5cdbf01-db85-4ff8-9fda-1489542bffef
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: correspondence-management
discoiquuid: 6cef0bcf-e2f0-4a5a-85a1-6d8a5dd9bd01
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# Criar carta {#create-letter}

## Fluxo de trabalho do Gerenciamento de correspondência {#correspondence-management-workflow}

O fluxo de trabalho do Gerenciamento de correspondência consiste em quatro fases:

1. Template creation
1. Document Fragment creation
1. Criação de cartas
1. Pós-processamento

### Criação de modelo {#template-creation}

O gráfico a seguir mostra um fluxo de trabalho típico para criar um modelo de correspondência.

![Fluxo de trabalho para criar um modelo de correspondência](assets/01.png)

Neste fluxo de trabalho:

1. Os designers de formulário criam layouts e layouts de fragmento usando o Adobe Forms Designer e os carregam em um repositório CRX. Os layouts contêm campos de formulário típicos, recursos de layout, como um cabeçalho e rodapé, e &quot;áreas de público alvo&quot; vazias para o posicionamento do conteúdo. Posteriormente, os Application Specialists mapeiam o conteúdo necessário para essas áreas de público alvo. Mais informações sobre [criação de layout](/help/forms/using/layout-design-details.md).
1. Especialistas em assuntos de assunto dos departamentos Jurídico, Financeiro ou de Marketing, criam e carregam conteúdo, como cláusulas de texto, isenções de responsabilidade, termos e condições e imagens, como logotipos, que são reutilizados em vários modelos de correspondência.
1. Os especialistas em aplicativos criam modelos de correspondência. O especialista do aplicativo

   * Maps text clauses and images to target areas in the layout templates
   * Defines conditions/rules for the inclusion of content
   * Binds layout fields and variables to underlying data models

1. Author previews the letter and submits it for post processing. More information about [post processing](/help/forms/using/submit-letter-topostprocess.md).

#### Uso de modelos de carta fornecidos com o Gerenciamento de correspondência {#using-letter-templates-provided-with-correspondence-management}

Em vez de criar um modelo de layout do zero, você pode optar por modificar e reutilizar os modelos fornecidos pelo Gerenciamento de correspondência. You can use designer to quickly modify the branding and the data and content fields of the templates to suit your organization&#39;s needs. Para obter mais informações sobre os modelos de Gerenciamento de correspondência, consulte Modelos [de carta de](/help/forms/using/reference-cm-layout-templates.md)referência.

### Criação de fragmentos de Documento {#document-fragment-creation}

Document fragments are reusable parts\components of a correspondence using which you can compose letters\correspondence.

Os fragmentos de documento são dos seguintes tipos:

#### Texto {#text}

Um ativo de texto é um conteúdo que consiste em um ou mais parágrafos de texto. Um parágrafo pode ser estático ou dinâmico. Um parágrafo dinâmico contém referências a elementos de dados, cujos valores são fornecidos em tempo de execução.

#### Lista {#list}

Lista é uma série de fragmentos de documento, incluindo texto, listas (a mesma lista não pode ser &quot;adicionada em si mesma&quot;), condições e imagens. A ordem dos elementos de lista pode ser fixa ou editável. Ao criar uma carta, você pode usar alguns ou todos os elementos da lista para replicar um padrão reutilizável de elementos.

#### Condição {#condition}

As condições permitem que você defina qual conteúdo será incluído no momento da criação da correspondência, com base nos dados fornecidos. A condição é descrita em termos de variáveis de controle. As variáveis podem ser um elemento de dicionário de dados ou um espaço reservado. Ao adicionar uma condição, você pode optar por incluir um ativo com base no valor que a variável de controle tem. As condições têm uma única saída com base em uma expressão. A primeira expressão é considerada verdadeira, com base na variável de condição atual. Seu valor se torna a saída da condição.

#### Layout fragment {#layout-fragment}

A layout fragment is a layout that can be used within one or more letters. A layout fragment is used to create repeatable patterns, especially dynamic tables. The layout can contain typical form fields such as “Address” and &quot;Reference Number.&quot; Ele também contém subformulários vazios que indicam áreas de público alvo. The layouts (XDPs) are created in Designer and then are [uploaded to Forms and Documents](/help/forms/using/get-xdp-pdf-documents-aem.md).

### Letter creation {#letter-creation}

There are two ways to generate the correspondence that is sent to your customers: user-driven and system-driven.

#### User driven {#user-driven}

Os funcionários voltados para o cliente, como os ajustadores de solicitações ou os trabalhadores de gabinete, podem criar correspondência personalizada. Using a simple and intuitive letter-filling interface, business users can add optional text to the correspondence, personalize editable content while previewing the correspondence in real time. They can then submit the customized correspondence to a back-end process.

![User-driven, customized correspondence](assets/02.png)

#### System driven {#system-driven}

The correspondence generation is automated, driven by event triggers. For example, a reminder notice sent to a citizen prompting her for advance tax filing, is generated by merging the predefined template with citizen data. The final letter can be emailed, printed, faxed, or archived.

![System-driven correspondence](assets/us_cm_generate.png)

### Post processing {#post-processing}

The final correspondence can be sent to a back-end process for postprocessing. The correspondence can be:

1. Processed for email, fax, or batch printing, or placed in a folder for printing or e-mailing.
1. Submitted for review and approval.
1. Secured by applying digital signatures, certification, encryption, or rights management.
1. Converted to a searchable PDF document that contains all the necessary metadata for archiving and auditing purposes.
1. Included in a PDF Portfolio that includes more documents, such as marketing material. The PDF Portfolio can then be sent as the final correspondence.

### Correspondence Management solution architecture {#correspondence-management-solution-architecture}

The following graphic provides an overview of an example architecture of the Letters Solution.

![Letter solution architecture](assets/us_cm_architecture_es3.png)

## Deconstructing a letter {#deconstructing-a-letter}

This Notice of Cancelation document is an example of a typical correspondence:

![A sample letter of cancelation](assets/5_deconstructingaletter.png)

<table> 
 <tbody> 
  <tr> 
   <td><strong>Letter elements</strong></td> 
   <td><strong>Descrição</strong></td> 
   <td><strong>Formed with</strong></td> 
  </tr> 
  <tr> 
   <td>Data from back-end Enterprise systems</td> 
   <td>Data that is sourced from backend enterprise systems. The data is merged dynamically with the correspondence template.</td> 
   <td>The<br /> Data file created based on a Data Dictionary</td> 
  </tr> 
  <tr> 
   <td>Data<br /> Entered by front-line Employee</td> 
   <td>Data that can be supplied by a front-line employee who is customizing the letter before sending it out.<br /> </td> 
   <td><p>Unprotected DD elements<br /> Editable text paragraphs<br /> Variables/placeholders<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Pre-Approved<br /> Text Paragraphs</td> 
   <td>Pre-approved text content. Experts in Legal, Finance, or a line of business who understand the business context of the letter, typically author the text content. Content such as header, footer, disclaimers, and salutation would be common to most of the letters. However, content such as "reason for termination" would be specific to the particular letter.</td> 
   <td><p>Text\Lists\<br /> Conditions\Layout</p> <p> </p> </td> 
  </tr> 
  <tr> 
   <td>Data<br /> Based on Custom Logic ?</td> 
   <td>For some letters, such as a letter to request more information regarding a claim, users such as the Claims Adjustor can add custom text content.</td> 
   <td>Document<br /> Fragment of type Condition </td> 
  </tr> 
  <tr> 
   <td>Stored<br /> Images from Central Repository</td> 
   <td>Images such as logos and signature images. Images such as corporate logos would appear in most or all of the correspondence. Signature images are specific to the letter and to the person on whose behalf the letter is sent.</td> 
   <td><p>Images stored in AEM assets (DAM)<br /> </p> <p> </p> </td> 
  </tr> 
 </tbody> 
</table>

## Analyze a letter before you construct it {#analyze-a-letter-before-you-construct-it}

Analyze every letter to uncover the various pieces that make up the letter. The Application Specialist analyzes the correspondences that are generated.

* Which parts of the correspondence are static and which are dynamic. The variables that are filled from backend data sources or by end users.
* The order in which the various text paragraphs appear in the correspondence such as whether a business user can change paragraphs during correspondence creation.
* Is the correspondence system-generated or does it require an end user to edit the correspondence? How many correspondences are system-generated and how many require user intervention?
* How frequently does the correspondence template change? Will it be updated yearly, quarterly, or only when a particular legislation changes? What type of changes is expected? Is it a change to fix typographical errors, a layout change, adding more fields, adding more paragraphs, and so on.
* When planning your correspondence requirements, assemble the list of new correspondence templates. For each correspondence template, you require:

   * Text clauses, images, and tables
   * Data values from backend systems
   * O layout e os layouts de fragmento da correspondência
   * The order in which content appears in the letter and rules for inclusion and exclusion of content

* The conditions under which business users such as claims adjustors or case workers modify content or portions in the letter.
* Os cenários são narrativas que descrevem a experiência do usuário, os requisitos e os benefícios do uso da Solução Letters.
* Scenarios also provide:The required skill sets and tools you require for your project.
* Best practices for planning your implementation. ``High-level implementation overview.

## Benefits of performing the analysis {#benefits-of-performing-the-analysis}

**Content reuse** You have a consolidated list of new content required for generating correspondence. Much of the content such as headers, footers, disclaimers, and introductions are common to many letters and can be reused across various letters. All such common content can be created and approved by experts once and then reused in many pieces of correspondence.

**Building the data dictionary** There will be data values such as &quot;Customer Id&quot; and &quot;Customer Name&quot; that are common to many letters. You can prepare a consolidated list of all such data values. Typically someone from the enterprise middleware team is consulted when planning the structure. This forms the basis for building the Data Dictionary.

**Sourcing data from backend enterprise systems** You will also know all of the data values that are needed and from where the enterprise system data is obtained. You can then architect the implementation to extract the data from the enterprise system and feed to the Letters solution.

**Estimating the complexity of letters** It is important to determine how complex it will be to create a particular correspondence. This analysis helps in determining the amount of time and skill sets that will be required to create the letter templates. This in turn will help in estimating the resources and cost of implementing the Letters solution.

## Correspondence complexity {#correspondence-complexity}

A complexidade da correspondência pode ser determinada pela análise dos seguintes parâmetros:

**Layout complexity** How complex is the layout? Letters such as Notice of Cancelation have simple layouts. Whereas letters such as Claims Coverage Confirmation has a complex layout with several tables and more than 60 form fields. Creating complex layouts takes more time and requires advanced layout design skill sets.

**Number of text paragraphs and conditions** A loan contract can be 10 pages long and contain more than 40 text clauses. Many of these clauses would depend `` loan parameters. Based on the exact terms and conditions, the clauses would be included or excluded from the contract. Creating such letters requires thorough planning and careful definition of the complex conditions.

This table provides some guidelines that you can use to classify your letters:

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Complexity level</strong></p> </td> 
   <td><p><strong>Layout complexity (subjective)</strong></p> </td> 
   <td><p><strong>Número de parágrafos de texto</strong></p> </td> 
   <td><p><strong>Number of conditional texts or images</strong></p> </td> 
   <td><p><strong>Required skill set</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Low complexity</p> </td> 
   <td><p>Baixa. Layout has few form fields (&lt;15).</p> <p>Typically one page<span class="acrolinxCursorMarker"></span>.</p> </td> 
   <td><p>8</p> </td> 
   <td><p>1</p> </td> 
   <td><p>Medium Designer skills.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Complexidade média</p> </td> 
   <td><p>Medium complexity layout. Inclui estruturas como tabelas. Typically more than one page long.</p> </td> 
   <td><p>16</p> </td> 
   <td><p>2</p> </td> 
   <td><p>Medium Designer skills.</p> <p> </p> <p>Capability to create complex expressions using user interfaces.</p> </td> 
  </tr> 
  <tr> 
   <td><p>High complexity</p> </td> 
   <td><p>Complex layout. Can be greater than three pages. Contains tables and more than 60 form fields.</p> </td> 
   <td><p>40</p> </td> 
   <td><p>8</p> </td> 
   <td><p>Expert Designer skills.</p> <p> </p> <p>Capability to create complex expressions using user interfaces.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Overview of Creating a Letter {#overview-of-creating-a-letter}

1. Select the appropriate layout that serves as the base of the letter and create a letter.
1. Add data modules or layout fragments to the letter and configure them.
1. Choose to preview the correspondence.
1. Edit and set up the fields, variables, content, and attachments.

### Pré-requisitos {#prerequisites}

You need the following in place first to create a correspondence:

* [Compatibility Package](compatibility-package.md). Install the Compatibility Package to view the **Letters** option on the **Forms** page.
* The letter XDP ([layout](/help/forms/using/document-fragments.md)).
* Other XDPs ([layout fragments](document-fragments.md#document-fragments)) that form parts of the letter. The XDPs\Layouts are created in [Designer](https://help.adobe.com/en-US/AEMForms/6.1/DesignerHelp/).
* The relevant [data dictionary](/help/forms/using/data-dictionary.md) (Optional).
* The [data modules](/help/forms/using/document-fragments.md) you want to use in the correspondence.
* [Test Data](/help/forms/using/data-dictionary.md#p-working-with-test-data-p) is the XML file with the test data ported in it. Test data is required if you are using a data dictionary.

## Create a letter template {#create-a-letter-template}

### Select a layout and enter the letter properties {#select-a-layout-and-enter-the-letter-properties}

1. Select **Forms** > **Letters**.

1. Selecione **Criar > Carta**. Correspondence Management displays the available layouts (XDPs). These layouts come from Designer. The layouts also include the letter templates that Correspondence Management provides out of the box. For more information on Correspondence Management templates, see [Reference letter templates](/help/forms/using/reference-cm-layout-templates.md). To add your own layouts, create XDP (layout) files in Designer and then [upload them to AEM Forms](/help/forms/using/get-xdp-pdf-documents-aem.md).

   ![create-letter](assets/create-letter.png)

1. Select a layout by tapping it and tap **Next**.

   ![Select layout to create a letter](assets/selectlayout.png)

1. Enter the properties for the Correspondence and tap **Save:**

   * **Title (Optional):** Enter the title for the letter. Title need not be unique and can have special characters and non-english characters.
   * **Name:** The unique name for the letter. No two letters in any state can exist with the same name. No campo Nome, é possível digitar somente caracteres, números e hífens do idioma inglês. The Name field is automatically populated based on the Title field. The special characters, spaces, numbers, and non-English characters entered in the Title field are replaced with hyphens in the Name field. Embora o valor no campo Título seja copiado automaticamente para o Nome, é possível editar o valor.
   * **Description (Optional):** Describe the letter for your reference.
   * **Dicionário de dados (opcional)**: O Dicionário de dados pode ser associado à correspondência. The assets that you later insert in this correspondence should either have the same data dictionary as the one you choose for the correspondence here or no data dictionary.
   * **Tags (Optional):** Select the tags to apply to the correspondence. Você também pode digitar um nome de tag novo/personalizado e pressionar Enter para criá-lo.
   * **Post Process (Optional):** Select the post process to be applied to the letter template. Há processos de postagem fora da caixa e aqueles que você criou usando o AEM, como email e impressão.
   ![Propriedades da correspondência](assets/createcorrespondenceproperties.png)

1. O sistema exibe uma mensagem: &quot;Carta criada com êxito.&quot; (na mensagem de alerta) Toque em **Abrir** para configurar os módulos de dados e os fragmentos de layout nele contidos. Or tap **Done** to go back to the previous page.

   ![Alert message: letter created successfully](assets/createcorrespondencecreated.png)

   **Próximo**: Quando você toca em **Abrir**, o Gerenciamento de correspondência exibe uma representação do layout com todos os componentes do layout (XDP) listados. Continue inserindo os Módulos de [dados e Fragmentos de layout e Configurando-os](/help/forms/using/create-letter.md#p-insert-data-modules-and-layout-fragments-in-a-letter-and-configure-them-p).

### Inserir módulos de dados e fragmentos de layout em uma letra e configurá-los {#insert-data-modules-and-layout-fragments-in-a-letter-and-configure-them}

Depois de criar uma correspondência, toque em Abrir, o Gerenciamento de correspondência exibe uma representação do layout com todas as áreas de subformulários/públicos alvos no layout (XDP) listado. Em cada uma das áreas de público alvo, você pode optar por inserir um Módulo de dados ou um Fragmento de layout (e, em seguida, módulos de dados no fragmento de layout).

>[!NOTE]
>
>Você também pode escolher tocar no ícone Editar para uma letra na página Letras para Inserir módulos de dados e fragmentos de layout em uma letra e configurá-los.

1. Toque em **Inserir** para cada um dos subformulários e selecione Módulos de dados ou um Fragmento de layout para inserir em cada um dos subformulários.

   ![Inserir módulos de dados e fragmentos de layout](assets/insertdmandlf.png)

1. Selecione Módulo de dados ou Fragmento de layout para essas opções para cada um dos subformulários e escolha os Módulos de dados ou os Fragmentos de layout a serem inseridos. A layout fragment allows you to further insert data modules or layout fragments in it according to its design (up to four levels).

   ![nestedlf](assets/nestedlf.png)

1. Se um fragmento de layout for inserido, o nome desse fragmento aparecerá no subformulário. E, de acordo com o fragmento selecionado, subformulários aninhados aparecem no subformulário.
1. Depois que os Módulos de dados selecionados forem inseridos no layout, você poderá tocar no modo de configuração e definir o seguinte após tocar no ícone Editar para cada um dos módulos:

   1. **Editável**: Quando essa opção é selecionada, o conteúdo pode ser editado na interface do usuário Criar correspondência. Marque o conteúdo como editável somente se ele exigir que o usuário comercial (como um Ajustador de solicitações) o modifique.
   1. **Obrigatório**: Quando essa opção é selecionada, o conteúdo é necessário na interface do usuário Criar correspondência.
   1. **Selecionado**: Quando essa opção é selecionada, o conteúdo é selecionado por padrão na interface do usuário Criar correspondência.
   1. **Recuo**: Aumente ou diminua o recuo do módulo/conteúdo na letra. O recuo é especificado em termos de níveis, começando em 0. Cada nível recua 36 pontos. Para obter mais informações sobre como personalizar formulários, consulte Configurações **[!UICONTROL de gerenciamento de]** correspondência no fluxo de trabalho [do](submit-letter-topostprocess.md#formsworkflow)Forms.
   1. **Quebra de página antes**: Se você definir a opção Quebra de página antes como ativada, o conteúdo DESTE módulo sempre será exibido em uma nova página.
   1. **Page break after**: If you set the Page Break After to on for a specific module, the contents of the NEXT module always display on a new page.
   ![Inserted data modules and layout fragments](assets/insertdmandlf2.png)

1. To edit a module, tap the Edit icon next to it. Depois de editar os módulos, toque em **Salvar**.

   In this page, you can also do the following for the subforms:

   1. **Permitir texto** gratuito: Se Permitir texto livre estiver ativado, o usuário poderá adicionar texto em linha na visualização CCR. Na visualização CCR, uma ação &#39;T&#39; é ativada para as áreas de público alvo com Permitir texto livre ativado e quando o usuário toca nela, ela solicita o nome e a descrição do texto e, ao tocar em OK, abre o texto no modo de edição, onde o usuário pode adicionar texto. Portanto, isto funciona como outros módulos de texto
   1. **Lock Order**: Locks the order of the subforms in the letter. O autor não tem permissão para reordenar os subformulários/componentes ao criar a carta.
   Nesta página, você também pode fazer o seguinte para cada um dos ativos nos subformulários:

   1. **Altere a ordem dos ativos**: arraste e solte um ativo que contém o ícone de reordem de um ativo ( ![arrastar e soltar](assets/dragndrop.png)).
   1. **Excluir ativos**: Toque no ícone Excluir ao lado de um ativo para excluí-lo.
   1. **Ativos** de Pré-visualização: Toque no ícone de mostrar pré-visualização ( ![mostrar visualização](assets/showpreview.png)) ao lado de um ativo.


1. Toque em **Avançar**.
1. A página Dados detalha como os campos de dados e as variáveis são usados no modelo. Os dados podem ser vinculados a fontes de dados, como um dicionário de dados ou uma entrada do usuário. Cada campo define as propriedades a partir das quais o dicionário de dados mapeia dados ou qual legenda é exibida para os campos de entrada do usuário.

   Ligação:

   * Os elementos de **campo** podem ser vinculados a um literal, a um elemento de dicionário de dados, a um ativo ou a um valor especificado pelo usuário. You can also ignore a field element by binding it to the Ignore option.
   * The **variable** elements can be linked to a literal, data dictionary element, a field, a variable, an asset, or a user specified value.
   A seguir estão alguns campos principais no vínculo:

   * **Várias linhas**: Você pode especificar se a entrada de dados de um campo ou variável é de várias linhas. Se você selecionar essa opção, a caixa de entrada do campo ou da variável será exibida como uma caixa de entrada de várias linhas na Visualização de edição de dados. O campo ou variável também é exibido como várias linhas nas visualizações de dados e conteúdo na interface do usuário Criar correspondência. O campo de entrada de várias linhas é semelhante ao campo para inserir um comentário em um TextModule. A opção de várias linhas está disponível somente para campos e variáveis com o tipo de vínculo Usuário ou Elementos de dicionário de dados desprotegidos.
   * **Opcional**: Você pode especificar se o valor para campo ou variável é opcional ou não. A opção de campo opcional está disponível para campos e variáveis com o tipo de vínculo Usuário ou Elementos de dicionário de dados desprotegidos.

   * **Validação** de campo/variável: Para fornecer a validação aprimorada do valor de um campo ou variável, é possível atribuir um validador ao campo ou à variável. Essa opção está disponível somente para campos e variáveis com o tipo de vínculo Usuário ou Elementos de dicionário de dados desprotegidos.
   * **Legenda** e **dica** de ferramenta: Legenda é o rótulo do campo que aparece antes do campo na interface do usuário do CCR. Essa opção está disponível para campos e variáveis com o tipo de vínculo Usuário ou Elementos de dicionário de dados desprotegidos.
   Following are the types of validation you can use for the fields:

   * **String Validator**: Use the String Validator to specify a minimum and maximum length of the string entered in field or variable. When you create a String Validator, ensure that you specify valid validation parameters. Enter a valid length for both the minimum and maximum values. For String validator, you can specify the min and max length of the value that can be entered. If the value entered is not according to the min and max specified, the relevant field in the CCR user interface is marked in red color.

   * **Number Validator**: Use the Number Validator to specify the minimum and maximum numeric value entered in a field or variable. When you create a Number Validator, ensure that you specify valid validation parameters. Insira valores numéricos para os valores mínimo e máximo.

   * **Regular Expression Validator**: Use the Regular Expression Validator to define a regular expression that is used to validate the value of a field or variable. In addition, you can customize the error message. Ao criar um Validador de Expressão regular, especifique uma expressão regular válida.
   >[!NOTE]
   >
   >Os validadores de campos e variáveis estão disponíveis somente em campos ou variáveis com o tipo de vínculo Usuário ou Elementos de dicionário de dados desprotegidos.

   ![ligações](assets/linkages.png)

1. Depois de especificar o vínculo, toque em **Próximo**. Correspondence Management displays the Attachments screen.

### Configurar os anexos {#set-up-the-attachments}

1. Select **Add Asset**.
1. Na tela Selecionar ativo, toque nos ativos a serem anexados com a letra e toque em **Concluído**. É necessário primeiro fazer upload dos ativos para os Ativos. É recomendável anexar somente documentos PDF e do Microsoft Office, mas também pode anexar imagens. Para obter mais informações sobre como fazer upload de ativos no DAM, consulte [Fazer upload de ativos](/help/assets/managing-assets-touch-ui.md).
1. Para bloquear a ordem dos ativos na lista de modo que o Ajustador de solicitações não possa alterar a ordem, toque em **Bloquear pedido**. Se você não selecionar essa opção, o Ajustador de solicitações poderá alterar a ordem dos itens de lista.
1. Para alterar a ordem dos ativos, arraste e solte um ativo que contém o ícone de reordem de um ativo ( ![arrastar e soltar](assets/dragndrop.png)).
1. Toque em **Editar** na frente de um anexo e especifique um anexo como Obrigatório se não quiser que o autor o exclua. Specify an attachment as Selected if you want it to be preselected in the CCR interface.
1. Select **Library Access** to give the access to the library. If Library Access is enabled, the Claims Adjustor can access content library while creating a letter and insert attachments.
1. Select **Attachments Configuration** and specify the maximum number of attachments.

1. Toque em **Salvar**. Your correspondence is created and listed on the Letters page.

After a letter template is created in Correspondence Management, the end user/agent/claim adjustor can open the letter in the CCR user interface and create a correspondence by entering data, setting up content, and managing attachments. For more information, see [Create Correspondence](/help/forms/using/create-correspondence.md).

## Types of linkage available for each of the fields {#types-of-linkage-available-for-each-of-the-fields}

The following table describes which types of linkage are available for various types of fields.

Os seguintes valores na tabela

* **Yes**: Field type in the leftmost column supports that type of mapping
* **No**: Field type in the leftmost column does not support that type of mapping
* **N/A**: Field type in the leftmost column is not applicable

<table> 
 <tbody> 
  <tr> 
   <td> </td> 
   <td><strong>Literal</strong></td> 
   <td><strong>Ativo</strong></td> 
   <td><strong>Dicionários de dados</strong></td> 
   <td><strong>Ignorar</strong></td> 
   <td><strong>Usuário</strong></td> 
   <td><strong>Texto</strong></td> 
   <td><strong>Variável</strong></td> 
  </tr> 
  <tr> 
   <td><strong>date</strong></td> 
   <td>Sim</td> 
   <td>Não</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>N/A</td> 
   <td>N/A</td> 
  </tr> 
  <tr> 
   <td><strong>time</strong></td> 
   <td>Sim</td> 
   <td>Não</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>N/A</td> 
   <td>N/A</td> 
  </tr> 
  <tr> 
   <td><strong>datetime</strong></td> 
   <td>Sim</td> 
   <td>Não</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>N/A</td> 
   <td>N/A</td> 
  </tr> 
  <tr> 
   <td><strong>integer</strong></td> 
   <td>Sim</td> 
   <td>Não</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>Sim<br /> </td> 
   <td>N/A</td> 
   <td>N/A</td> 
  </tr> 
  <tr> 
   <td><strong>float</strong></td> 
   <td>Sim</td> 
   <td>Não</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>Sim<br /> </td> 
   <td>N/A</td> 
   <td>N/A<br /> </td> 
  </tr> 
  <tr> 
   <td><strong>richtext</strong></td> 
   <td>Sim</td> 
   <td>text only</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>N/A</td> 
   <td>N/A</td> 
  </tr> 
  <tr> 
   <td><strong>simples</strong> <strong>texto</strong></td> 
   <td>Sim</td> 
   <td>somente texto</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>N/A</td> 
   <td>N/A</td> 
  </tr> 
  <tr> 
   <td><strong>imagem</strong></td> 
   <td>Não</td> 
   <td>image only</td> 
   <td>Não</td> 
   <td>Sim</td> 
   <td>Não</td> 
   <td>N/A</td> 
   <td>N/A</td> 
  </tr> 
  <tr> 
   <td><strong>signature</strong></td> 
   <td>Não</td> 
   <td>Não</td> 
   <td>Não<br /> </td> 
   <td>Sim</td> 
   <td>Não</td> 
   <td>N/A</td> 
   <td>N/A<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Create copy of a letter template {#createcopylettertemplate}

Você pode usar um modelo de carta existente para criar rapidamente um modelo de carta com propriedades, conteúdo e ativos herdados semelhantes, como fragmentos de documento e dicionário de dados. To do this, copy and paste a letter.

1. In the Letters page, select one or more letters. A interface do usuário exibe o ícone Copiar.
1. Toque em Copiar. A interface do usuário exibe o ícone Colar. Você também pode escolher entrar em uma pasta antes de colar. Different folders can contain assets with same names. For more information on folders, see [Folders and organizing assets](/help/forms/using/import-export-forms-templates.md#folders-and-organizing-assets).
1. Toque em Colar. The Paste dialog appears. If you are copying and pasting the letters at the same place, the system automatically assigns names and titles to the new copies of letters but you can edit the titles and names of the letters.
1. If required, edit the Title and Name with which you want to save the copy of the letter.
1. Toque em Colar. The copy of the letter is created. Now you can make the required changes in your newly created letter.

