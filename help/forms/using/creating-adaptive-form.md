---
title: Como criar um formulário adaptável
description: 'Saiba como criar um formulário adaptável usando [!DNL Experience Manager Forms]. Formulários adaptáveis são formulários HTML5 responsivos que simplificam o processamento e a coleta de informações. Saiba mais sobre como criar um formulário adaptável com base em um modelo de dados de formulário, modelo de formulário XFA e schema XML ou JSON. '
feature: Adaptive Forms
role: Business Practitioner, Developers
level: Beginner
translation-type: tm+mt
source-git-commit: 52fedc234b3edf581393bb42325902d2da3ab46e
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 0%

---


# Criação de um formulário adaptável {#creating-an-adaptive-form}

## <strong>Criar um formulário adaptável</strong> {#strong-create-an-adaptive-form-strong}

Siga estas etapas para criar um formulário adaptável.

1. Acessar [!DNL Experience Manager Forms] instância do autor em `https://'[server]:[port]'/<custom-context-if-any>.`

1. Digite suas credenciais na página de login do Experience Manager.

   Depois de fazer logon, no canto superior esquerdo, toque em **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documentos]**.

   >[!NOTE]
   >
   >Para uma instalação padrão, o logon é `admin` e a senha é `admin`.

1. Toque em **[!UICONTROL Criar]** e selecione **[!UICONTROL Formulário adaptável]**.
1. Uma opção para selecionar um modelo é exibida. Para obter mais informações sobre modelos, consulte [Modelos de formulário adaptáveis](creating-adaptive-form.md#p-adaptive-form-templates-p). Toque em um modelo para selecioná-lo e toque em Próximo.
1. Uma opção para &quot;Adicionar propriedades&quot; é exibida. Especifique os valores para os seguintes campos de propriedade. Os campos Título e Nome são obrigatórios:

   * **[!UICONTROL Título:]** Especifica o nome de exibição do formulário. O título ajuda a identificar o formulário na interface do usuário [!DNL Experience Manager Forms].
   * **[!UICONTROL Nome:]** Especifica o nome do formulário. Um nó com o nome especificado é criado no repositório. À medida que você digita um título, o valor do campo de nome é gerado automaticamente. Você pode alterar o valor sugerido. O campo de nome pode incluir somente caracteres alfanuméricos, hífens e sublinhados. Todas as entradas inválidas são substituídas por um hífen.
   * **[!UICONTROL Descrição:]** Especifica as informações detalhadas sobre o formulário.
   * **[!UICONTROL Tags:]** Especifica tags para identificar exclusivamente o formulário adaptável. As tags ajudam na pesquisa do formulário. Para criar tags, digite novos nomes de tags na caixa **[!UICONTROL Tags]**.

1. É possível criar um formulário adaptável com base em um dos seguintes modelos de formulário:

   * [Modelo de dados de formulário](#fdm)
   * [Modelo de formulário XFA](#create-an-adaptive-form-based-on-an-xfa-form-template)
   * [SCHEMA XML ou JSON](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * Nenhum ou sem qualquer modelo de formulário

   Você pode configurá-los na guia **[!UICONTROL Modelo de formulário]** na página **[!UICONTROL Adicionar propriedades]**. Por padrão, o modelo de formulário selecionado é **[!UICONTROL Nenhum]**.

1. Toque em **[!UICONTROL Criar]**. Um formulário adaptável é criado e uma caixa de diálogo para abrir o formulário para edição é exibida.

   Depois de terminar de especificar todas as propriedades, clique em **[!UICONTROL Criar]**. Um formulário adaptável é criado e uma caixa de diálogo para abrir o formulário para edição é exibida.

   Depois de terminar de especificar todas as propriedades, clique em **[!UICONTROL Criar]**. Um formulário adaptável é criado e uma caixa de diálogo para abrir o formulário para edição é exibida.

1. Toque em **[!UICONTROL Abrir]** para abrir o formulário recém-criado em uma nova guia. O formulário é aberto para edição e exibe o conteúdo disponível no modelo. Ela também exibe a barra lateral para personalizar o formulário recém-criado de acordo com as necessidades.

   Com base no tipo de formulário adaptável, os elementos de formulário presentes no modelo de formulário XFA, no schema XML ou no schema JSON associados são exibidos na guia **[!UICONTROL Objetos do Modelo de Dados]** do **[!UICONTROL Navegador de Conteúdo]** na barra lateral. Você também pode arrastar e soltar esses elementos para criar seu formulário adaptável.

   Para obter informações sobre a interface adaptativa de criação de formulários e os componentes disponíveis, consulte [Introdução à criação de formulários adaptáveis](introduction-forms-authoring.md).

   >[!NOTE]
   >
   >Permita que as janelas pop-up do seu navegador abram o formulário recém-criado em uma nova guia.

## Criar um formulário adaptável com base em um modelo de dados de formulário {#fdm}

[[!DNL Experience Manager Forms] a ](data-integration.md) integração de dados permite integrar várias fontes de dados e unir suas entidades e serviços para criar um modelo de dados de formulário. É uma extensão do schema JSON. É possível usar um modelo de dados de formulário para criar um formulário adaptável. As entidades ou objetos de modelo de dados configurados em um modelo de dados de formulário estão disponíveis como objetos de modelo de dados para a criação de formulário. Estão vinculados às respectivas fontes de dados e são usados para pré-preencher um formulário e gravar os dados enviados de volta nas respectivas fontes de dados. Também é possível chamar serviços configurados em um modelo de dados de formulário usando regras de formulário adaptáveis.

Para usar um modelo de dados de formulário para criar um formulário adaptável:

1. Na guia Modelo de formulário na tela Adicionar propriedades, selecione **[!UICONTROL Modelo de dados de formulário]** na lista suspensa **[!UICONTROL Selecionar de]**.

   ![create-af-1-1](assets/create-af-1-1.png)

1. Toque em para expandir **[!UICONTROL Selecionar Modelo de Dados de Formulário]**. Todos os modelos de dados de formulário disponíveis são listados.

   Selecione um a partir do modelo de dados.

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>Também é possível alterar o modelo de dados de formulário para um formulário adaptável. Para obter etapas detalhadas, consulte [Editar propriedades do Modelo de formulário de um formulário adaptável](#edit-form-model).

## Criar um formulário adaptável com base em um modelo de formulário XFA {#create-an-adaptive-form-based-on-an-xfa-form-template}

Você pode reaproveitar os modelos de formulário XFA para criar formulários adaptáveis. Para redefinir a finalidade, carregue e associe um modelo de formulário XFA a um formulário adaptável. Os elementos do Modelo de formulário (formulário XFA) são disponibilizados para uso no localizador de conteúdo no momento da criação de formulário adaptável. No Localizador de conteúdo, é possível arrastar e soltar os elementos do modelo de formulário no formulário.

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

## Criar um formulário adaptável com base no schema XML ou JSON {#create-an-adaptive-form-based-on-xml-or-json-schema}

Os schemas XML e JSON representam a estrutura na qual os dados são produzidos ou consumidos pelo sistema back-end em sua organização. É possível associar um schema a um formulário adaptável e usar seus elementos para adicionar conteúdo dinâmico ao formulário adaptável. Os elementos do schema estão disponíveis na guia Objeto de modelo de dados do navegador de conteúdo para a criação de formulários adaptáveis. É possível arrastar e soltar os elementos do schema para criar o formulário.

Consulte os documentos a seguir para entender como projetar o schema XML ou JSON para criar formulários adaptáveis.

* [Criação de formulários adaptáveis usando o schema XML](adaptive-form-xml-schema-form-model.md)
* [Criação de formulários adaptáveis usando o schema JSON](adaptive-form-json-schema-form-model.md)

Faça o seguinte para usar o schema XML ou JSON como modelo de formulário para um formulário adaptável:

1. Na etapa **[!UICONTROL Adicionar propriedades]** da página de criação de formulário adaptável, toque na guia **[!UICONTROL Modelo de formulário]**.
1. Na guia Modelo de formulário, selecione **[!UICONTROL Schema]** no campo suspenso **[!UICONTROL Selecionar de]**.

1. Toque em **[!UICONTROL Selecionar Schema]** e execute um dos procedimentos a seguir:

   * **[!UICONTROL Carregar do disco]**  - Selecione esta opção e toque em Carregar definição de Schema para navegar e carregar um schema XML ou schema JSON do seu sistema de arquivos. O arquivo de schema carregado reside no formulário e não pode ser acessado por outros formulários adaptáveis.
   * **[!UICONTROL Pesquisar no repositório]**  - Selecione essa opção para selecionar a partir da lista de arquivos de definição de schemas disponíveis no repositório. Selecione o arquivo de schema XML ou JSON como modelo de formulário. O schema selecionado é associado ao formulário por referência e pode ser usado em outros formulários adaptáveis.

   >[!CAUTION]
   >
   >Certifique-se de que o nome de arquivo do schema JSON termine com **.schema.json**. Por exemplo: mySchema.schema.json

   ![Selecionar schema XML ou JSON](assets/upload-schema.png)
   **Figura:** *Seleção do schema XML ou JSON*

1. (Somente para schema XML) Depois de selecionar ou carregar um Schema XML, especifique um elemento raiz do arquivo XSD selecionado para mapear com o formulário adaptável.

   ![Seleção do elemento raiz XSD](assets/xsd-root-element.png)
   **Figura:** *Seleção do elemento raiz XSD*

>[!NOTE]
>
>Você também pode alterar o schema de um formulário adaptável. Para obter etapas detalhadas, consulte [Editar propriedades do Modelo de formulário de um formulário adaptável](#edit-form-model).

## Modelos de formulário adaptável {#adaptive-form-templates}

Um modelo fornece uma estrutura básica e define a aparência (layouts e estilos) de um formulário adaptável. Ele possui componentes pré-formatados contendo determinadas propriedades e estrutura de conteúdo. <!-- Out of the box, AEM Forms provides some adaptive form templates. To get the complete template package including advanced templates, you need to install the AEM Forms add-on package. For more information, see [Installing AEM Forms add-on package](installing-configuring-aem-forms-osgi.md).-->

Além disso, você pode usar o editor de modelos para criar seus próprios modelos. Para obter mais informações sobre como trabalhar com modelos, consulte [Modelos de formulário adaptáveis](template-editor.md).

>[!NOTE]
>
>Quando você abre um formulário adaptável criado usando o modelo avançado para edição, uma mensagem de erro é exibida. O modelo avançado tem um componente Etapa de assinatura e a Adobe Sign está habilitada para ele por padrão. Crie e selecione uma [configuração de nuvem do Adobe Sign](adobe-sign-integration-adaptive-forms.md) e [configure um assinante](working-with-adobe-sign.md#addsignerstoanadaptiveform) para resolver o erro.

## Editar propriedades do Modelo de formulário de um formulário adaptável {#edit-form-model}

Os formulários adaptáveis são criados sem um modelo de formulário (usando a opção Nenhum para o modelo de formulário) ou usando um modelo de formulário, como modelo de formulário, schema XML ou schema JSON ou modelo de dados de formulário. É possível alterar o modelo de formulário para um formulário adaptável de Nenhum para outro modelo de formulário. Para formulários adaptáveis baseados em um modelo de formulário, é possível escolher outro modelo de formulário, schema XML, schema JSON ou modelo de dados de formulário para o mesmo modelo de formulário. No entanto, não é possível alterar de um modelo de formulário para outro.

1. Selecione o formulário adaptável e toque no ícone **Propriedades**.
1. Abra a guia **[!UICONTROL Modelo de formulário]** e execute um dos procedimentos a seguir.

   * Se o formulário adaptável estiver sem um modelo de formulário, é possível escolher outro modelo de formulário e, consequentemente, selecionar um modelo de formulário, schema XML ou JSON ou modelo de dados de formulário.
   * Se o formulário adaptável for baseado em um modelo de formulário, você poderá escolher outro modelo de formulário, schema XML ou JSON ou modelo de dados de formulário para o mesmo modelo de formulário.

1. Toque em **[!UICONTROL Salvar]** para salvar as propriedades.

## Salvar automaticamente um formulário adaptável {#auto-save-an-adaptive-form}

Por padrão, o conteúdo de um formulário adaptável é salvo em uma ação do usuário, como ao pressionar o botão Salvar. Você também pode configurar um formulário adaptável para que o start automaticamente salve o conteúdo com base em um evento ou intervalo de tempo. A opção de salvar automaticamente é útil em:

* Salvar automaticamente o conteúdo para usuários anônimos e conectados
* Salvar o conteúdo de um formulário sem a intervenção ou o mínimo possível do usuário
* Start que salva o conteúdo de um formulário com base em um evento do usuário
* Salvar o conteúdo de um formulário repetidamente após um intervalo de tempo especificado

### Habilitar gravação automática para um formulário adaptável {#enable-auto-save-for-an-adaptive-form}

Por padrão, a opção de salvar automaticamente não está ativada. É possível ativar a opção de salvar automaticamente na guia Salvar automaticamente de um formulário adaptável. A guia Salvar automaticamente também fornece várias outras opções de configuração. Execute as seguintes etapas para ativar e configurar a opção de salvar automaticamente para um formulário adaptável:

1. Para acessar a seção de salvamento automático nas propriedades, selecione um componente, em seguida, toque em ![field-level](assets/field-level.png) > **[!UICONTROL Container de formulário adaptável]** e, em seguida, toque em ![cmppr](assets/cmppr.png).
1. Na seção **[!UICONTROL Salvar automaticamente]**, **[!UICONTROL Ative]** a opção de salvar automaticamente.
1. Na caixa **[!UICONTROL Evento de formulário adaptável]**, especifique 1 ou VERDADEIRO para salvar automaticamente o formulário quando o formulário for carregado no navegador. Também é possível especificar uma expressão condicional para um evento, que, quando acionado e retorna true, salva start no conteúdo do formulário.
1. Especifique o Acionador. O salvamento automático é acionado com base na sua configuração. Suas opções são:

   * **[!UICONTROL Baseado em tempo:]** selecione a opção para salvar o conteúdo em start com base em um intervalo de tempo específico.
   * **[!UICONTROL Baseado em eventos:]** selecione a opção para salvar o conteúdo com base em start quando um evento é acionado.

   Quando você seleciona um acionador, a caixa Configuração de estratégia é ativada. A caixa Configuração de estratégia permite:

   * Especifique um intervalo de tempo se selecionar o acionador **[!UICONTROL Baseado em hora]**.
   * Especifique um nome de evento se você selecionar **[!UICONTROL acionador baseado em Evento]**.

   <!-- You can also create and add your own custom strategy to the list. For details, see [Implement a custom strategy to autosave the forms](auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p). -->

1. (Somente salvamento automático com base em tempo) Execute as seguintes etapas para configurar opções para o salvamento automático com base em tempo.

   1. Na caixa **[!UICONTROL Salvar automaticamente neste intervalo]**, especifique o intervalo de tempo em segundos. O formulário é salvo repetidamente depois que o número de segundos especificado na caixa de intervalo decorre.

1. (Somente para salvar automaticamente com base em Eventos) Execute as seguintes etapas para configurar opções para o salvamento automático com base em Eventos.

   1. Na caixa **[!UICONTROL Guardar automaticamente depois deste evento]**, especifique um evento [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html). O formulário é salvo sempre que a expressão é avaliada como VERDADEIRO.

1. (Opcional) Para salvar automaticamente o conteúdo para usuários anônimos, selecione a opção **[!UICONTROL Ativar o salvamento automático para usuários anônimos]** e clique em **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Para que a opção de salvamento automático funcione para usuários anônimos, certifique-se de configurar o Forms Common Configuration Service para permitir que todos os usuários possam pré-visualização, verificar e assinar formulários.
   >
   >Para configurar o serviço, vá para a configuração do Adobe Experience Manager Web Console em `https://'[server]:[port]'system/console/configMgr` e edite o **[!UICONTROL Forms Common Configuration Service]** para escolher a opção **[!UICONTROL Todos os usuários]** no campo **[!UICONTROL Permitir]** e salve a configuração.