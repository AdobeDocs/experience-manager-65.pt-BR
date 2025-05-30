---
title: Como criar um formulário adaptável
description: Saiba como criar um formulário adaptável usando o  [!DNL Experience Manager Forms]. Os formulários adaptáveis são formulários HTML5 responsivos que simplificam a coleta e o processamento de informações. Saiba mais sobre como criar um formulário adaptável com base em um modelo de dados de formulário, modelo de formulário XFA e esquema XML ou JSON.
role: User, Developer
level: Beginner
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
exl-id: 2c25a8b7-73f7-40fb-a303-9446a708c8eb
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1984'
ht-degree: 6%

---

# Criação de um formulário adaptável {#creating-an-adaptive-form}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=pt-br) |
| AEM 6.5 | Este artigo |

## Criar um formulário adaptável {#strong-create-an-adaptive-form-strong}

Siga estas etapas para criar um formulário adaptável.

1. Acessar instância de autor [!DNL Experience Manager Forms] em `https://'[server]:[port]'/<custom-context-if-any>.`

1. Insira suas credenciais na página de logon do Experience Manager.

   Depois de fazer logon, no canto superior esquerdo, selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.

   >[!NOTE]
   >
   >Para uma instalação padrão, o logon é `admin` e a senha é `admin`.

1. Selecione **[!UICONTROL Criar]** e selecione **[!UICONTROL Formulário adaptável]**.
1. Uma opção para selecionar um modelo é exibida. Para obter mais informações sobre modelos, consulte [Modelos de formulário adaptável](creating-adaptive-form.md#p-adaptive-form-templates-p). Selecione um template para selecioná-lo e clique em Next.
1. Uma opção para &quot;Adicionar propriedades&quot; é exibida. Especifique os valores para os seguintes campos de propriedade. Os campos Título e Nome são obrigatórios:

   * **[!UICONTROL Título:]** Especifica o nome de exibição do formulário. O título ajuda a identificar o formulário na interface do usuário do [!DNL Experience Manager Forms].
   * **[!UICONTROL Nome:]** especifica o nome do formulário. Um nó com o nome especificado será criado no repositório. Ao começar a digitar um título, o valor do campo de nome é gerado automaticamente. É possível alterar o valor sugerido. O campo de nome pode incluir apenas caracteres alfanuméricos, hifens e sublinhados. Todas as entradas inválidas são substituídas por um hífen.
   * **[!UICONTROL Descrição:]** Especifica as informações detalhadas sobre o formulário.
   * **[!UICONTROL Marcas:]** especifica marcas para identificar exclusivamente o formulário adaptável. A ajuda das tags na pesquisa do formulário. Para criar marcas, digite novos nomes de marcas na caixa **[!UICONTROL Marcas]**.

1. Você pode criar um formulário adaptável com base em um dos seguintes modelos de formulário:

   * [Modelo de dados do formulário](#fdm)
   * [Modelo de formulário XFA](#create-an-adaptive-form-based-on-an-xfa-form-template)
   * [Esquema XML ou JSON](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * Nenhum ou sem nenhum modelo de formulário

   Você pode configurá-los na guia **[!UICONTROL Modelo de formulário]** da página **[!UICONTROL Adicionar propriedades]**. Por padrão, o modelo de formulário selecionado é **[!UICONTROL Nenhum]**.

1. Selecione **[!UICONTROL Criar]**. Um formulário adaptável é criado e uma caixa de diálogo para abrir o formulário para edição é exibida.

   Depois que você terminar de especificar todas as propriedades, clique em **[!UICONTROL Criar]**. Um formulário adaptável é criado e uma caixa de diálogo para abrir o formulário para edição é exibida.

   Depois que você terminar de especificar todas as propriedades, clique em **[!UICONTROL Criar]**. Um formulário adaptável é criado e uma caixa de diálogo para abrir o formulário para edição é exibida.

1. Selecione **[!UICONTROL Abrir]** para abrir o formulário recém-criado em uma nova guia. O formulário é aberto para edição e exibe o conteúdo disponível no template. Também exibirá a barra lateral para personalizar o formulário recém-criado de acordo com as necessidades.

   Com base no tipo de formulário adaptável, os elementos de formulário presentes no modelo de formulário XFA associado, no esquema XML ou no esquema JSON são exibidos na guia **[!UICONTROL Objetos do Modelo de Dados]** do **[!UICONTROL Navegador de Conteúdo]** na barra lateral. Você também pode arrastar e soltar esses elementos para criar seu formulário adaptável.

   Para obter informações sobre a interface de criação de formulários adaptáveis e os componentes disponíveis, consulte [Introdução à criação de formulários adaptáveis](introduction-forms-authoring.md).

   >[!NOTE]
   >
   >Permite que janelas pop-up em seu navegador abram o formulário recém-criado em uma nova guia.

## Criar um formulário adaptável com base em um modelo de dados de formulário {#fdm}

A [[!DNL Experience Manager Forms] integração de dados](data-integration.md) permite que você integre várias fontes de dados e reúna suas entidades e serviços para criar um modelo de dados de formulário. É uma extensão do esquema JSON. Você pode usar um modelo de dados de formulário para criar um formulário adaptável. As entidades ou os objetos de modelo de dados configurados em um modelo de dados de formulário estão disponíveis como objetos de modelo de dados para criação de formulário. Eles são vinculados às respectivas fontes de dados e usados para preencher previamente um formulário e gravar dados enviados nas respectivas fontes de dados. Você também pode chamar serviços configurados em um modelo de dados de formulário usando regras de formulário adaptáveis.

Para usar um modelo de dados de formulário para criar um formulário adaptável:

1. Na guia Modelo de formulário na tela Adicionar propriedades, selecione **[!UICONTROL Modelo de dados de formulário]** na lista suspensa **[!UICONTROL Selecionar de]**.

   ![criar-af-1-1](assets/create-af-1-1.png)

1. Selecione para expandir **[!UICONTROL Selecionar modelo de dados de formulário]**. Todos os modelos de dados de formulário disponíveis estão listados.

   Selecione um do modelo de dados.

   ![criar-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>Também é possível alterar o modelo de dados de formulário para um formulário adaptável. Para obter etapas detalhadas, consulte [Editar propriedades do Modelo de Formulário de um formulário adaptável](#edit-form-model).

## Criar um formulário adaptável com base em um modelo de formulário XFA {#create-an-adaptive-form-based-on-an-xfa-form-template}

Você pode redefinir os modelos de formulário XFA para criar formulários adaptáveis. Para redefinir objetivos, carregue e associe um modelo de formulário XFA a um formulário adaptável. Os elementos do Modelo de formulário (formulário XFA) são disponibilizados para uso no localizador de conteúdo no momento da criação do formulário adaptável. No Localizador de conteúdo, você pode arrastar e soltar os elementos do modelo de formulário no formulário.

<!-- >>[!NOTE]
>
>[Upload the XFA Form Template](get-xdp-pdf-documents-aem.md) to AEM Forms before you start creating an adaptive form based on the form template.

Do the following to use an XFA form template as form model for your adaptive form:

1. On the **[!UICONTROL Add Properties]** page, open the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, from the drop-down list, select **[!UICONTROL Form Templates]**. All the form templates that are uploaded to the repository via AEM Forms UI are listed for selection. Select a template from the list.

   ![Associate XFA Form Template with an Adaptive Form](assets/form_model_xfa_associate.png)
**Figure:** *Selecting a form template*

   >[!NOTE]
   >
   >You can also change the form template for an adaptive form. For detailed steps, see [Edit Form Model properties of an adaptive form](#edit-form-model). -->

## Criar um formulário adaptável com base em um esquema XML ou JSON {#create-an-adaptive-form-based-on-xml-or-json-schema}

Os esquemas XML e JSON representam a estrutura em que os dados são produzidos ou consumidos pelo sistema de back-end em sua organização. Você pode associar um esquema a um formulário adaptável e usar seus elementos para adicionar conteúdo dinâmico ao formulário adaptável. Os elementos do esquema estão disponíveis na guia Objeto de modelo de dados do navegador de conteúdo para a criação de formulários adaptáveis. Você pode arrastar e soltar os elementos do esquema para criar o formulário.

Consulte os documentos a seguir para entender como projetar esquemas XML ou JSON para a criação de formulários adaptáveis.

* [Criação de formulários adaptáveis usando o esquema XML](adaptive-form-xml-schema-form-model.md)
* [Criação de formulários adaptáveis usando o esquema JSON](adaptive-form-json-schema-form-model.md)

Faça o seguinte para usar o esquema XML ou JSON como modelo de formulário para um formulário adaptável:

1. Na etapa **[!UICONTROL Adicionar propriedades]** da página de criação do formulário adaptável, selecione na guia **[!UICONTROL Modelo de formulário]**.
1. Na guia Modelo de formulário, selecione **[!UICONTROL Esquema]** no campo suspenso **[!UICONTROL Selecionar de]**.

1. Selecione **[!UICONTROL Selecionar esquema]** e siga um destes procedimentos:

   * **[!UICONTROL Carregar do disco]** - Selecione esta opção e selecione Carregar Definição de Esquema para procurar e carregar um esquema XML ou esquema JSON do sistema de arquivos. O arquivo de esquema carregado reside no formulário e não pode ser acessado por outros formulários adaptáveis.
   * **[!UICONTROL Pesquisar no repositório]** - Selecione esta opção para selecionar na lista de arquivos de definição de esquema disponíveis no repositório. Selecione o arquivo de esquema XML ou JSON como modelo de formulário. O esquema selecionado é associado ao formulário por referência e pode ser acessado para uso em outros formulários adaptáveis.

   >[!CAUTION]
   >
   >Verifique se o nome do arquivo do esquema JSON termina com **.schema.json**. Por exemplo: mySchema.schema.json

   ![Selecionando esquema XML ou JSON](assets/upload-schema.png)
   **Figura:** *Selecionando esquema XML ou JSON*

1. (Somente para esquema XML) Depois de selecionar ou fazer upload de um esquema XML, especifique um elemento raiz do arquivo XSD selecionado para mapear com o formulário adaptável.

   ![Selecionando elemento raiz XSD](assets/xsd-root-element.png)
   **Figura:** *Selecionando elemento raiz XSD*

>[!NOTE]
>
>Também é possível alterar o esquema para um formulário adaptável. Para obter etapas detalhadas, consulte [Editar propriedades do Modelo de Formulário de um formulário adaptável](#edit-form-model).

## Modelos de formulário adaptável {#adaptive-form-templates}

Um modelo fornece uma estrutura básica e define a aparência (layouts e estilos) de um formulário adaptável. Ele tem componentes pré-formatados que contêm determinadas propriedades e estrutura de conteúdo. <!-- Out of the box, AEM Forms provides some adaptive form templates. To get the complete template package including advanced templates, you need to install the AEM Forms add-on package. For more information, see [Installing AEM Forms add-on package](installing-configuring-aem-forms-osgi.md).-->

Além disso, você pode usar o editor de modelos para criar seus próprios modelos. Para obter mais informações sobre como trabalhar com modelos, consulte [Modelos de formulário adaptável](template-editor.md).

>[!NOTE]
>
>Ao abrir um formulário adaptável criado usando o modelo avançado para edição, uma mensagem de erro é exibida. O modelo avançado tem um componente de Etapa de assinatura e o Adobe Sign é ativado para ele por padrão. Crie e selecione uma [configuração de nuvem do Adobe Sign](adobe-sign-integration-adaptive-forms.md) e [configure um signatário](working-with-adobe-sign.md#addsignerstoanadaptiveform) para resolver o erro.

## Editar propriedades do Modelo de formulário de um formulário adaptável {#edit-form-model}

Os formulários adaptáveis são criados sem um modelo de formulário (usando a opção Nenhum para o modelo de formulário) ou usando um modelo de formulário, como um modelo de formulário, esquema XML ou esquema JSON, ou modelo de dados de formulário. É possível alterar o modelo de formulário para um formulário adaptável de Nenhum para outro modelo de formulário. Para formulários adaptáveis baseados em um modelo de formulário, você pode escolher outro modelo de formulário, esquema XML, esquema JSON ou modelo de dados de formulário para o mesmo modelo de formulário. No entanto, não é possível alterar de um modelo de formulário para outro.

1. Selecione o formulário adaptável e o ícone **Propriedades**.
1. Abra a guia **[!UICONTROL Modelo de Formulário]** e siga um destes procedimentos.

   * Se o formulário adaptável não tiver um modelo de formulário, você poderá escolher outro modelo de formulário e selecionar um modelo de formulário, esquema XML ou JSON ou modelo de dados de formulário.
   * Se o formulário adaptável for baseado em um modelo de formulário, você poderá escolher outro modelo de formulário, esquema XML ou JSON, ou modelo de dados de formulário para o mesmo modelo de formulário.

1. Selecione **[!UICONTROL Salvar]** para salvar as propriedades.

## Salvar automaticamente um formulário adaptável {#auto-save-an-adaptive-form}

Por padrão, o conteúdo de um formulário adaptável é salvo em uma ação do usuário, como ao pressionar o botão Salvar. Você também pode configurar um formulário adaptável para começar a salvar automaticamente o conteúdo com base em um evento ou intervalo de tempo. A opção de salvamento automático é útil em:

* Salvando automaticamente o conteúdo para usuários anônimos e conectados
* Salvamento do conteúdo de um formulário sem a mínima intervenção do usuário
* Começar a salvar o conteúdo de um formulário com base em um evento do usuário
* Salvamento repetido do conteúdo de um formulário após um intervalo de tempo especificado

### Habilitar Salvamento automático para um formulário adaptável {#enable-auto-save-for-an-adaptive-form}

Por padrão, a opção de salvamento automático não está habilitada. Você pode ativar a opção de salvamento automático na guia Salvamento automático de um formulário adaptável. A guia Salvamento automático também fornece várias outras opções de configuração. Execute as seguintes etapas para ativar e configurar a opção de salvamento automático para um formulário adaptável:

1. Para acessar a seção de salvamento automático nas propriedades, selecione um componente e, em seguida, ![nível do campo](assets/field-level.png) > **[!UICONTROL Contêiner de formulário adaptável]** e selecione ![cmppr](assets/cmppr.png).
1. Na seção **[!UICONTROL Salvamento Automático]**, **[!UICONTROL Habilite]** a opção de salvamento automático.
1. Na caixa **[!UICONTROL Evento de formulário adaptável]**, especifique 1 ou TRUE para iniciar automaticamente o salvamento do formulário quando ele for carregado no navegador. Você também pode especificar uma expressão condicional para um evento, que, quando acionado e retornar true, inicia o salvamento do conteúdo do formulário.
1. Especifique o Acionador. O salvamento automático é acionado com base na sua configuração. As opções são:

   * **[!UICONTROL Baseado em tempo:]** Selecione a opção para começar a salvar o conteúdo com base em um intervalo de tempo específico.
   * **[!UICONTROL Baseado em evento:]** selecione a opção para começar a salvar o conteúdo com base em quando um evento for acionado.

   Ao selecionar um acionador, a caixa Configuração de estratégia é ativada. A caixa de configuração de estratégia permite:

   * Especifique um intervalo se você selecionar o acionador **[!UICONTROL Baseado em tempo]**.
   * Especifique um nome de evento se você selecionar o acionador **[!UICONTROL Baseado em evento]**.

   <!-- You can also create and add your own custom strategy to the list. For details, see [Implement a custom strategy to autosave the forms](auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p). -->

1. (Somente salvamento automático baseado em tempo) Execute as seguintes etapas para configurar opções para o salvamento automático baseado em tempo.

   1. Na caixa **[!UICONTROL Salvar automaticamente neste intervalo]**, especifique o intervalo de tempo em segundos. O formulário é salvo repetidamente depois que o número de segundos especificado na caixa intervalo decorrer.

1. (Somente salvamento automático baseado em evento) Execute as seguintes etapas para configurar opções para o salvamento automático baseado em evento.

   1. Na caixa **[!UICONTROL Salvar automaticamente após este evento]**, especifique um evento [GuideBridge](https://helpx.adobe.com/br/aem-forms/6/javascript-api/GuideBridge.html). O formulário é salvo sempre que a expressão é avaliada como TRUE.

1. (Opcional) Para salvar automaticamente o conteúdo para usuários anônimos, selecione a opção **[!UICONTROL Habilitar salvamento automático para usuários anônimos]** e clique em **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Para que a opção de salvamento automático funcione para usuários anônimos, certifique-se de configurar o Serviço de configuração comum da Forms para permitir que todos os usuários visualizem, verifiquem e assinem formulários.
   >
   >Para configurar o serviço, vá para Configuração do Console da Web do Adobe Experience Manager em `https://'[server]:[port]'system/console/configMgr` e edite o **[!UICONTROL Serviço de Configuração Comum do Forms]** para escolher a opção **[!UICONTROL Todos os Usuários]** no campo **[!UICONTROL Permitir]** e salve a configuração.


## Como renomear um formulário adaptável para AEM? {#rename-an-AEM-Adaptive-Form}

Para renomear um formulário adaptável, execute as seguintes etapas:

1. Selecione um formulário adaptável na interface do usuário do AEM Forms.
1. Clique nas **Propriedades** localizadas no painel superior.

   ![Propriedades](/help/forms/using/assets/rename-form-properties.png)

1. Altere o nome do formulário na guia **Título**, conforme mostrado na imagem abaixo.
1. Clique em **Salvar e fechar**.

   ![Renomear um Formulário adaptável de AEM](/help/forms/using/assets/rename-form-title.png)
