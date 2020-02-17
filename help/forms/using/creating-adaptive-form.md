---
title: Criação de um formulário adaptável
seo-title: Criação de um formulário adaptável
description: Como criar um formulário adaptável usando o AEM Forms. Formulários adaptáveis são formulários HTML5 responsivos que simplificam o processamento e a coleta de informações.
seo-description: Como criar um formulário adaptável usando o AEM Forms. Formulários adaptáveis são formulários HTML5 responsivos que simplificam o processamento e a coleta de informações.
uuid: 444f461a-9e88-4385-b5ee-e985067ab7bc
content-type: reference
topic-tags: author
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: f06b8cb2-6f98-465f-beec-1e91e3f45707
translation-type: tm+mt
source-git-commit: 24728d320d46edc5e18385868ba92cb4292c8c5f

---


# Criação de um formulário adaptável {#creating-an-adaptive-form}

## <strong>Criar um formulário</strong> adaptável {#strong-create-an-adaptive-form-strong}

Siga estas etapas para criar um formulário adaptável.

1. Acessar a instância do autor de formulários AEM em `https://[server]:[port]/<custom-context-if-any>.`

1. Digite suas credenciais na página de logon do AEM.

   Depois de fazer logon, no canto superior esquerdo, toque em **[!UICONTROL Adobe Experience Manager > Formulários > Formulários e documentos]**.

   >[!NOTE]
   >
   >Para uma instalação padrão, o login é feito `admin` e a senha é `admin`.

1. Toque em **[!UICONTROL Criar]** e selecione Formulário **** adaptável.
1. Uma opção para selecionar um modelo é exibida. Para obter mais informações sobre modelos, consulte Modelos [de formulário](/help/forms/using/creating-adaptive-form.md#p-adaptive-form-templates-p)adaptáveis. Toque em um modelo para selecioná-lo e toque em Próximo.
1. Uma opção para &quot;Adicionar propriedades&quot; é exibida. Especifique os valores para os seguintes campos de propriedade. Os campos Título e Nome são obrigatórios:

   * **** Título: Especifica o nome de exibição do formulário. O título ajuda a identificar o formulário na interface do usuário do AEM Forms.
   * **** Nome: Especifica o nome do formulário.  Um nó com o nome especificado é criado no repositório. À medida que você digita um título, o valor do campo de nome é gerado automaticamente. Você pode alterar o valor sugerido. O campo de nome pode incluir somente caracteres alfanuméricos, hífens e sublinhados. Todas as entradas inválidas são substituídas por um hífen.
   * **** Descrição: Especifica as informações detalhadas sobre o formulário.
   * **** Tags: Especifica tags para identificar exclusivamente o formulário adaptável. As tags ajudam na pesquisa do formulário. Para criar tags, digite novos nomes de tags na caixa **Tags** .

1. É possível criar um formulário adaptável com base em um dos seguintes modelos de formulário:

   * [Modelo de dados de formulário](#fdm)
   * [Modelo de formulário XFA](/help/forms/using/creating-adaptive-form.md#p-create-an-adaptive-form-based-on-an-xfa-form-template-p)
   * [Esquema XML ou JSON](/help/forms/using/creating-adaptive-form.md#p-create-an-adaptive-form-based-on-xml-or-json-schema-p)
   * Nenhum ou sem qualquer modelo de formulário
   É possível configurá-los na guia Modelo **[!UICONTROL de]** formulário na página **[!UICONTROL Adicionar propriedades]** . Por padrão, o modelo de formulário selecionado é **[!UICONTROL Nenhum]**.

1. Toque em **Criar**. Um formulário adaptável é criado e uma caixa de diálogo para abrir o formulário para edição é exibida.

   Depois de terminar de especificar todas as propriedades, clique em **[!UICONTROL Criar]**. Um formulário adaptável é criado e uma caixa de diálogo para abrir o formulário para edição é exibida.

   Depois de terminar de especificar todas as propriedades, clique em **[!UICONTROL Criar]**. Um formulário adaptável é criado e uma caixa de diálogo para abrir o formulário para edição é exibida.

1. Toque em **[!UICONTROL Abrir]** para abrir o formulário recém-criado em uma nova guia. O formulário é aberto para edição e exibe o conteúdo disponível no modelo. Ela também exibe a barra lateral para personalizar o formulário recém-criado de acordo com as necessidades.

   Com base no tipo de formulário adaptável, os elementos de formulário presentes no modelo de formulário XFA, esquema XML ou esquema JSON associados são exibidos na guia Objetos **[!UICONTROL do Modelo de]** dados do Navegador **[!UICONTROL de]** conteúdo na barra lateral. Você também pode arrastar e soltar esses elementos para criar seu formulário adaptável.

   Para obter informações sobre a interface adaptativa de criação de formulários e os componentes disponíveis, consulte [Introdução à criação de formulários](/help/forms/using/introduction-forms-authoring.md)adaptáveis.

   >[!NOTE] {grayBox=&quot;true&quot;}
   >
   >Permita que as janelas pop-up do seu navegador abram o formulário recém-criado em uma nova guia.

## Criar um formulário adaptável com base em um modelo de dados de formulário {#fdm}

[A integração](/help/forms/using/data-integration.md) de dados do AEM Forms permite integrar várias fontes de dados e unir suas entidades e serviços para criar um modelo de dados de formulário. É uma extensão do esquema JSON. É possível usar um modelo de dados de formulário para criar um formulário adaptável. As entidades ou objetos de modelo de dados configurados em um modelo de dados de formulário estão disponíveis como objetos de modelo de dados para a criação de formulário. Estão vinculados às respectivas fontes de dados e são usados para pré-preencher um formulário e gravar os dados enviados de volta nas respectivas fontes de dados. Também é possível invocar serviços configurados em um modelo de dados de formulário usando regras de formulário adaptáveis.

Para usar um modelo de dados de formulário para criar um formulário adaptável:

1. Na guia Modelo de formulário na tela Adicionar propriedades, selecione Modelo **[!UICONTROL de dados de]** formulário na lista suspensa **[!UICONTROL Selecionar]** .

   ![create-af-1-1](assets/create-af-1-1.png)

1. Toque em para expandir **[!UICONTROL Selecionar modelo]** de dados do formulário. Todos os modelos de dados de formulário disponíveis são listados.

   Selecione um a partir do modelo de dados.

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>Também é possível alterar o modelo de dados de formulário para um formulário adaptável. Para obter etapas detalhadas, consulte [Editar propriedades do modelo de formulário de um formulário](#edit-form-model)adaptável.

## Criar um formulário adaptável com base em um modelo de formulário XFA {#create-an-adaptive-form-based-on-an-xfa-form-template}

Você pode reaproveitar os modelos de formulário XFA para criar formulários adaptáveis. Para redefinir a finalidade, carregue e associe um modelo de formulário XFA a um formulário adaptável. Os elementos do Modelo de formulário (formulário XFA) são disponibilizados para uso no localizador de conteúdo no momento da criação de formulário adaptável. No Localizador de conteúdo, é possível arrastar e soltar os elementos do modelo de formulário no formulário.

>[!NOTE]
>
>[Faça upload do modelo](/help/forms/using/get-xdp-pdf-documents-aem.md) de formulário XFA para formulários AEM antes de começar a criar um formulário adaptável com base no modelo de formulário.

Faça o seguinte para usar um modelo de formulário XFA como modelo de formulário para o formulário adaptável:

1. Na página **[!UICONTROL Adicionar propriedades]** , abra a guia Modelo **[!UICONTROL de]** formulário.
1. Na guia Modelo de formulário, na lista suspensa, selecione Modelos **[!UICONTROL de]** formulário. Todos os modelos de formulário carregados no repositório por meio da interface do usuário do AEM Forms são listados para seleção. Selecione um modelo na lista.

   ![Associar modelo de formulário XFA a um formulário adaptável](assets/form_model_xfa_associate.png)
   **** Figura: *Seleção de um modelo de formulário*

   >[!NOTE]
   >
   >Também é possível alterar o modelo de formulário para um formulário adaptável. Para obter etapas detalhadas, consulte [Editar propriedades do modelo de formulário de um formulário](#edit-form-model)adaptável.

## Criar um formulário adaptável com base no esquema XML ou JSON {#create-an-adaptive-form-based-on-xml-or-json-schema}

 Os esquemas XML e JSON representam a estrutura na qual os dados são produzidos ou consumidos pelo sistema back-end em sua organização. É possível associar um esquema a um formulário adaptável e usar seus elementos para adicionar conteúdo dinâmico ao formulário adaptável. Os elementos do esquema estão disponíveis na guia Objeto de modelo de dados do navegador de conteúdo para a criação de formulários adaptáveis. Você pode arrastar e soltar os elementos do esquema para criar o formulário.

Consulte os seguintes documentos para entender como projetar um esquema XML ou JSON para criar formulários adaptáveis.

* [Criação de formulários adaptáveis usando o esquema XML](/help/forms/using/adaptive-form-xml-schema-form-model.md)
* [Criação de formulários adaptáveis usando o esquema JSON](/help/forms/using/adaptive-form-json-schema-form-model.md)

Faça o seguinte para usar o esquema XML ou JSON como modelo de formulário para um formulário adaptável:

1. Na etapa **[!UICONTROL Adicionar propriedades]** da página de criação de formulário adaptável, toque na guia Modelo **[!UICONTROL de]** formulário.
1. Na guia Modelo de formulário, selecione **[!UICONTROL Esquema]** no campo **[!UICONTROL suspenso Selecionar]** .

1. Toque em **[!UICONTROL Selecionar esquema]** e execute um dos procedimentos a seguir:

   * **[!UICONTROL Carregar do disco]** - Selecione essa opção e toque em Carregar definição de esquema para navegar e carregar um esquema XML ou JSON do sistema de arquivos. O arquivo de esquema carregado reside no formulário e não pode ser acessado por outros formulários adaptáveis.
   * **[!UICONTROL Pesquisar no repositório]** - Selecione essa opção para selecionar na lista de arquivos de definição de esquema disponíveis no repositório. Selecione o arquivo de esquema XML ou JSON como modelo de formulário. O esquema selecionado será associado ao formulário por referência e estará acessível para uso em outros formulários adaptáveis.
   >[!CAUTION] {grayBox=&quot;true&quot;}
   >
   >Certifique-se de que o nome de arquivo do esquema JSON termine com **.schema.json**. Por exemplo: mySchema.schema.json

   ![Seleção do esquema XML ou JSON](assets/upload-schema.png)
   **** Figura: *Seleção do esquema XML ou JSON*

1. (Somente para esquema XML) Depois de selecionar ou carregar um Esquema XML, especifique um elemento raiz do arquivo XSD selecionado para mapear com o formulário adaptável.

   ![Seleção do elemento raiz XSD](assets/xsd-root-element.png)
   **** Figura: *Seleção do elemento raiz XSD*

>[!NOTE]
>
>Também é possível alterar o esquema de um formulário adaptável. Para obter etapas detalhadas, consulte [Editar propriedades do modelo de formulário de um formulário](#edit-form-model)adaptável.

## Modelos de formulário adaptável {#adaptive-form-templates}

Um modelo fornece uma estrutura básica e define a aparência (layouts e estilos) de um formulário adaptável. Ele possui componentes pré-formatados contendo determinadas propriedades e estrutura de conteúdo. O AEM Forms fornece alguns modelos de formulário adaptáveis. Para obter o pacote de modelo completo, incluindo modelos avançados, é necessário instalar o pacote complementar AEM Forms. Para obter mais informações, consulte [Instalação do pacote](/help/forms/using/installing-configuring-aem-forms-osgi.md)complementar AEM Forms.

Além disso, você pode usar o editor de modelos para criar seus próprios modelos. Para obter mais informações sobre como trabalhar com modelos, consulte Modelos [de formulário](/help/forms/using/template-editor.md)adaptáveis.

>[!NOTE]
>
>Quando você abre um formulário adaptável criado usando o modelo avançado para edição, uma mensagem de erro é exibida. O modelo avançado tem um componente Etapa de assinatura e o Adobe Sign está habilitado para ele por padrão. Crie e selecione uma configuração [em nuvem do](/help/forms/using/adobe-sign-integration-adaptive-forms.md) Adobe Sign e [configure um assinante](/help/forms/using/working-with-adobe-sign.md#main-pars-header-1374317451) para resolver o erro.

## Editar propriedades do Modelo de formulário de um formulário adaptável {#edit-form-model}

Os formulários adaptáveis são criados sem um modelo de formulário (usando a opção Nenhum para o modelo de formulário) ou usando um modelo de formulário, como modelo de formulário, esquema XML ou esquema JSON, ou modelo de dados de formulário. É possível alterar o modelo de formulário para um formulário adaptável de Nenhum para outro modelo de formulário. Para formulários adaptáveis baseados em um modelo de formulário, você pode escolher outro modelo de formulário, esquema XML, esquema JSON ou modelo de dados de formulário para o mesmo modelo de formulário. No entanto, não é possível alterar de um modelo de formulário para outro.

1. Selecione o formulário adaptável e toque no ícone **Propriedades** .
1. Abra a guia Modelo **[!UICONTROL de]** formulário e execute um dos procedimentos a seguir.

   * Se o formulário adaptável estiver sem um modelo de formulário, é possível escolher outro modelo de formulário e, consequentemente, selecionar um modelo de formulário, um esquema XML ou JSON ou um modelo de dados de formulário.
   * Se o formulário adaptável for baseado em um modelo de formulário, você poderá escolher outro modelo de formulário, esquema XML ou JSON ou modelo de dados de formulário para o mesmo modelo de formulário.

1. Toque em **[!UICONTROL Salvar]** para salvar as propriedades.

## Salvar automaticamente um formulário adaptável {#auto-save-an-adaptive-form}

Por padrão, o conteúdo de um formulário adaptável é salvo em uma ação do usuário, como ao pressionar o botão Salvar. Você também pode configurar um formulário adaptável para começar a salvar automaticamente o conteúdo com base em um evento ou intervalo de tempo. A opção de salvar automaticamente é útil em:

* Salvar automaticamente o conteúdo para usuários anônimos e conectados
* Salvar o conteúdo de um formulário sem a intervenção ou o mínimo possível do usuário
* Comece a salvar conteúdo de um formulário com base em um evento de usuário
* Salvar o conteúdo de um formulário repetidamente após um intervalo de tempo especificado

### Ativar a opção Salvar automaticamente para um formulário adaptável {#enable-auto-save-for-an-adaptive-form}

Por padrão, a opção de salvar automaticamente não está ativada. É possível ativar a opção de salvar automaticamente na guia Salvar automaticamente de um formulário adaptável. A guia Salvar automaticamente também fornece várias outras opções de configuração. Execute as seguintes etapas para ativar e configurar a opção de salvar automaticamente para um formulário adaptável:

1. Para acessar a seção de salvamento automático nas propriedades, selecione um componente, em seguida, toque em nível ![de](assets/field-level.png) campo > Contêiner **[!UICONTROL de formulário]** adaptável e, em seguida, toque em ![cmppr](assets/cmppr.png).
1. Na seção Salvar **** automaticamente, **[!UICONTROL ative]** a opção de salvar automaticamente.
1. Na caixa Evento **[!UICONTROL de formulário]** adaptável, especifique 1 ou TRUE para começar a salvar automaticamente o formulário quando ele for carregado no navegador. Também é possível especificar uma expressão condicional para um evento, que, quando acionada e retorna true, começa a salvar o conteúdo do formulário.
1. Especifique o Acionador. O salvamento automático é acionado com base na sua configuração. Suas opções são:

   * **** Baseado em tempo: Selecione a opção para começar a salvar o conteúdo com base em um intervalo de tempo específico.
   * **** Baseado em eventos: Selecione a opção para começar a salvar o conteúdo com base quando um evento é acionado.
   Quando você seleciona um acionador, a caixa Configuração de estratégia é ativada. A caixa Configuração de estratégia permite:

   * Especifique um intervalo de tempo se você selecionar acionador baseado **[!UICONTROL em]** tempo.
   * Especifique um nome de evento se você selecionar o acionador baseado **[!UICONTROL em]** evento.
   Você também pode criar e adicionar sua própria estratégia personalizada à lista. Para obter detalhes, consulte [Implementar uma estratégia personalizada para salvar automaticamente os formulários](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. (Somente salvamento automático com base em tempo) Execute as seguintes etapas para configurar opções para o salvamento automático com base em tempo.

   1. Na caixa Salvar **[!UICONTROL automaticamente nesse intervalo]** , especifique o intervalo de tempo em segundos. O formulário é salvo repetidamente depois que o número de segundos especificado na caixa de intervalo decorre.

1. (Somente salvamento automático com base em eventos) Execute as seguintes etapas para configurar opções para o salvamento automático com base em eventos.

   1. Na caixa Salvar **automaticamente após esse evento** , especifique um evento [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) . O formulário é salvo sempre que a expressão é avaliada como VERDADEIRO.

1. (Opcional) Para salvar automaticamente o conteúdo para usuários anônimos, selecione a opção **Ativar salvamento automático para usuários** anônimos e clique em **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Para que a opção de salvar automaticamente funcione para usuários anônimos, certifique-se de configurar o Serviço de configuração comum do Forms para permitir que todos os usuários visualizem, verifiquem e assinem formulários.
   >
   >Para configurar o serviço, vá até Configuração do console da Web do AEM em `https://[server]:[host]/system/console/configMgr` e edite o serviço **[!UICONTROL de configuração comum do]** Forms para escolher a opção **[!UICONTROL Todos os usuários]** no campo **[!UICONTROL Permitir]** e salve a configuração.