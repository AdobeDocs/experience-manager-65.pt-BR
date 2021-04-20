---
title: Usar modelo de dados de formulário
seo-title: Usar modelo de dados de formulário
description: Saiba como usar o modelo de dados de formulário para criar e trabalhar com formulários adaptáveis e comunicações interativas.
seo-description: Saiba como usar o modelo de dados de formulário para criar e trabalhar com formulários adaptáveis e comunicações interativas.
uuid: 9d8d8f43-9a50-4905-a6ef-a5ea3b9c11f7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 87f5f9f5-2d03-4565-830e-eacc3757e542
docset: aem65
feature: Form Data Model
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 1%

---


# Usar modelo de dados de formulário{#use-form-data-model}

![](do-not-localize/data-integeration.png)

A integração de dados do AEM Forms permite usar diferentes fontes de dados de backend para criar um modelo de dados de formulário que pode ser usado como schema em vários formulários adaptáveis e fluxos de trabalho de comunicações interativas. Ela requer a configuração de fontes de dados e a criação de um modelo de dados de formulário com base em objetos e serviços de modelo de dados disponíveis em fontes de dados. Para obter mais informações, consulte:

* [Integração de dados do AEM Forms](../../forms/using/data-integration.md)
* [Configurar fontes de dados](../../forms/using/configure-data-sources.md)
* [Criar modelo de dados de formulário](../../forms/using/create-form-data-models.md)
* [Trabalhar com o modelo de dados de formulário](../../forms/using/work-with-form-data-model.md)

Um modelo de dados de formulário é uma extensão do esquema JSON que pode ser usada para:

* [Criar formulários e fragmentos adaptáveis](#create-af)
* [Criar comunicações interativas e blocos de construção como fragmentos de texto, lista e condição](#create-ic)
* [Visualizar comunicações interativas com dados de amostra](#preview-ic)
* [Preencher previamente formulários adaptáveis e comunicações interativas](#prefill)
* [Gravar dados de formulário adaptável enviados de volta em fontes de dados](#write-af)
* [Invocar serviços usando regras de formulário adaptáveis](#invoke-services)

## Criar formulários e fragmentos adaptáveis {#create-af}

Você pode criar [formulários adaptáveis](../../forms/using/creating-adaptive-form.md) e [fragmentos de formulário adaptáveis](../../forms/using/adaptive-form-fragments.md) com base em um modelo de dados de formulário. Faça o seguinte para usar um modelo de dados de formulário ao criar um formulário adaptável ou fragmento de formulário adaptável:

1. Na guia Modelo de formulário na tela Adicionar propriedades, selecione **[!UICONTROL Modelo de dados de formulário]** na lista suspensa **[!UICONTROL Selecionar de]**.

   ![create-af-1-1](assets/create-af-1-1.png)

1. Toque para expandir **[!UICONTROL Selecionar Modelo de Dados de Formulário]**. Todos os modelos de dados de formulário disponíveis são listados.

   Selecione um do modelo de dados.

   ![create-af-2-1](assets/create-af-2-1.png)

1. (**Somente fragmentos de formulário adaptáveis**) É possível criar um fragmento de formulário adaptável com base em apenas um objeto de modelo de dados em um modelo de dados de formulário. Expanda a lista suspensa **[!UICONTROL Definições do Modelo de dados de formulário]** . Ele lista todos os objetos de modelo de dados no modelo de dados de formulário especificado. Selecione um objeto de modelo de dados na lista.

   ![create-af-3](assets/create-af-3.png)

Depois que o formulário adaptável ou o fragmento de formulário adaptável com base em um modelo de dados de formulário for criado, os objetos de modelo de dados de formulário aparecerão na guia **[!UICONTROL Objetos de Modelo de Dados]** do navegador Conteúdo no editor de formulário adaptável.

>[!NOTE]
>
>Para um fragmento de formulário adaptável, somente o objeto de modelo de dados selecionado no momento da criação e seus objetos de modelo de dados associados aparecem na guia Objetos do modelo de dados .

![data-model-objects-tab](assets/data-model-objects-tab.png)

É possível arrastar e soltar objetos de modelo de dados no formulário ou fragmento adaptável para adicionar campos de formulário. Os campos de formulário adicionados mantêm as propriedades de metadados e o vínculo com as propriedades de objetos do modelo de dados. O vínculo garante que os valores do campo sejam atualizados nas fontes de dados correspondentes no envio do formulário e pré-preenchidos no momento em que o formulário for renderizado.

## Criar comunicações interativas {#create-ic}

É possível criar uma comunicação interativa com base em um modelo de dados de formulário que pode ser usado para preencher previamente a comunicação interativa com dados de fontes de dados configuradas. Além disso, os blocos de construção de uma comunicação interativa, como fragmentos de documento de texto, lista e condição, podem ser baseados em um modelo de dados de formulário.

É possível escolher um modelo de dados de formulário ao criar uma comunicação interativa ou um fragmento de documento. A imagem a seguir mostra a guia Geral da caixa de diálogo Criar comunicação interativa .

![create-ic](assets/create-ic.png)

Guia Geral da caixa de diálogo Criar comunicação interativa

Para obter mais informações, consulte:

[Criar uma comunicação interativa](../../forms/using/create-interactive-communication.md)

[Texto em Comunicações interativas](/help/forms/using/texts-interactive-communications.md)

[Condições em comunicações interativas](/help/forms/using/conditions-interactive-communications.md)

[Fragmentos de lista](/help/forms/using/lists.md)

## Visualizar com dados de amostra {#preview-ic}

O editor de modelo de dados de formulário permite gerar e editar dados de amostra para objetos de modelo de dados no modelo de dados de formulário. Você pode usar esses dados para visualizar e testar comunicações interativas e formulários adaptáveis. Você deve gerar os dados de amostra antes de visualizar conforme descrito em [Trabalhar com o modelo de dados de formulário](../../forms/using/work-with-form-data-model.md#sample).

Para visualizar uma comunicação interativa com dados de modelo de dados de formulário de amostra:

1. Em AEM instância do autor, navegue até **[!UICONTROL Forms > Forms &amp; Documents]**.
1. Selecione uma comunicação interativa e toque em **[!UICONTROL Visualizar]** na barra de ferramentas para selecionar **[!UICONTROL Canal da Web]**, **[!UICONTROL Canal de impressão]** ou **[!UICONTROL Ambos os Canais]** para visualizar a comunicação interativa.
1. Na caixa de diálogo Visualizar [*canal*], verifique se **[!UICONTROL Testar dados do modelo de dados de formulário]** está selecionado e toque em **[!UICONTROL Visualizar]**.

A comunicação interativa é aberta com dados de amostra pré-preenchidos.

![visualização da Web](assets/web-preview.png)

Da mesma forma, para visualizar um formulário adaptável com dados de amostra, abra o formulário adaptável no modo de criação e toque em **[!UICONTROL Visualizar]**.

## Preencher previamente usando o serviço de modelo de dados de formulário {#prefill}

O AEM Forms fornece o serviço de preenchimento prévio do modelo de dados de formulário pronto para uso que você pode ativar para formulários adaptáveis e comunicações interativas com base no modelo de dados de formulário. O serviço de preenchimento prévio consulta fontes de dados para objetos de modelo de dados no formulário adaptável e na comunicação interativa e, portanto, preenche os dados previamente ao renderizar o formulário ou a comunicação.

Para ativar o Serviço de preenchimento prévio do modelo de dados de formulário para um formulário adaptável, abra as propriedades do contêiner de formulário adaptável e selecione **[!UICONTROL Serviço de preenchimento prévio do modelo de dados de formulário]** no menu suspenso **[!UICONTROL Preencher serviço]** na opção Básico . Em seguida, salve as propriedades.

![serviço de preenchimento prévio](assets/prefill-service.png)

Para configurar o serviço de preenchimento prévio do modelo de dados de formulário em uma comunicação interativa, você pode selecionar Serviço de preenchimento prévio do modelo de dados de formulário na lista suspensa Serviço de preenchimento prévio ao criá-lo ou posteriormente, modificando as propriedades.

![edit-ic-props](assets/edit-ic-props.png)

Caixa de diálogo Editar propriedades para uma comunicação interativa

## Gravar dados de formulário adaptável enviados em fontes de dados {#write-af}

Quando um usuário envia um formulário com base em um modelo de dados de formulário, é possível configurar o formulário para gravar dados enviados de um objeto de modelo de dados em suas fontes de dados. Para obter esse caso de uso, o AEM Forms fornece [Form Data Model envia a ação](../../forms/using/configuring-submit-actions.md), disponível imediatamente apenas para formulários adaptáveis com base em um modelo de dados de formulário. Ele grava dados enviados para um objeto de modelo de dados em sua fonte de dados.

Para configurar a ação de envio do Modelo de dados de formulário, abra as propriedades do Contêiner de formulário adaptável e selecione **[!UICONTROL Enviar usando o Modelo de dados de formulário]** no menu suspenso Enviar ação da opção Enviar. Em seguida, navegue e selecione um objeto de modelo de dados no menu suspenso **[!UICONTROL Name of the data model object to submit]**. Salve as propriedades.

No envio do formulário, os dados do objeto de modelo de dados configurado são gravados na respectiva fonte de dados.

![envio de dados](assets/data-submission.png)

Também é possível enviar anexos de formulário para uma fonte de dados usando a propriedade de objeto de modelo de dados binário. Faça o seguinte para enviar anexos a uma fonte de dados JDBC:

1. Adicione um objeto de modelo de dados que inclua uma propriedade binária ao modelo de dados de formulário.
1. No formulário adaptável, arraste e solte o componente **[!UICONTROL File Attachment]** do navegador Componentes no formulário adaptável.
1. Toque para selecionar o componente adicionado e toque em ![settings_icon](assets/settings_icon.png) para abrir o navegador Propriedades do componente.
1. No campo Bind Reference (Referência de associação), toque em ![foldersearch_18](assets/foldersearch_18.png) e navegue para selecionar a propriedade binária adicionada no modelo de dados de formulário. Configure outras propriedades, conforme apropriado.

   Toque em ![check-button](assets/check-button.png) para salvar as propriedades. O campo de anexo agora está vinculado à propriedade binária do modelo de dados de formulário.

1. Na seção Enviar das propriedades do Contêiner de formulário adaptável, ative **[!UICONTROL Enviar anexos de formulário]**. Ele envia o anexo no campo de propriedade binária para a fonte de dados no envio do formulário.

## Invocar serviços em formulários adaptáveis usando regras {#invoke-services}

Em um formulário adaptável com base em um modelo de dados de formulário, você pode [criar regras](../../forms/using/rule-editor.md) para invocar serviços configurados no modelo de dados de formulário. A operação **[!UICONTROL Invoke Services]** em uma regra lista todos os serviços disponíveis no modelo de dados de formulário e permite selecionar campos de entrada e saída para o serviço. Também é possível usar o tipo de regra **Definir valor** para chamar um serviço de modelo de dados de formulário e definir o valor de um campo para a saída retornada pelo serviço.

Por exemplo, a regra a seguir chama um serviço get que utiliza a ID do Funcionário como entrada e os valores retornados são preenchidos nos campos ID Dependente, Sobrenome, Nome e Gênero correspondentes no formulário.

![invoke-service](assets/invoke-service.png)

Além disso, você pode usar a API `guidelib.dataIntegrationUtils.executeOperation` para gravar um JavaScript no editor de códigos do editor de regras. Para obter detalhes da API, consulte [API para invocar o serviço de modelo de dados de formulário](/help/forms/using/invoke-form-data-model-services.md).
