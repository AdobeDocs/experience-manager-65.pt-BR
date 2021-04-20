---
title: '"Tutorial: Criar fragmentos de documento"'
seo-title: Criar fragmentos de documento para comunicação interativa
description: Criar fragmentos de documento para comunicação interativa
seo-description: Criar fragmentos de documento para comunicação interativa
uuid: 677d717e-e92e-434e-8266-6fbbf94f3867
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8ae97a21-83af-4615-9be3-61e2f8065081
docset: aem65
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 2%

---


# Tutorial: Criar fragmentos de documento{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Este tutorial é uma etapa da série [Create your first Interative Communication](/help/forms/using/create-your-first-interactive-communication.md). É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso tutorial completo.

Fragmentos de documento são componentes reutilizáveis de uma correspondência usados para compor uma Comunicação interativa. Os fragmentos de documento são dos seguintes tipos:

* Texto - Um ativo de texto é um conteúdo que consiste em um ou mais parágrafos de texto. Um parágrafo pode ser estático ou dinâmico.
* Lista - Lista é um grupo de fragmentos de documento, incluindo texto, listas, condições e imagens.
* Condição - As condições permitem definir qual conteúdo é incluído na Comunicação interativa com base nos dados recebidos do Modelo de dados de formulário.

Este tutorial o orienta pelas etapas para criar vários fragmentos de documento de texto com base na anatomia fornecida na seção [Planejar a comunicação interativa](/help/forms/using/planning-interactive-communications.md). Ao final deste tutorial, você poderá:

* Criar fragmentos de documento
* Criar variáveis
* Criar e aplicar regras

![text_document_fragments](assets/text_document_fragments.gif)

Esta é a lista de fragmentos de documento criados neste tutorial:

* [Detalhes da fatura](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [Detalhes do cliente](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [Resumo da fatura](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [Resumo dos encargos](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

Cada fragmento de documento inclui campos com texto estático, dados recebidos do modelo de dados de formulário e dados inseridos usando a interface do agente. Todos esses campos foram descritos na seção [Planejar a comunicação interativa](/help/forms/using/planning-interactive-communications.md).

Ao criar fragmentos de documento neste tutorial, as variáveis são criadas para campos que recebem dados usando a interface do agente.

Use **FDM_Create_First_IC**, conforme descrito na seção [Criar modelo de dados de formulário](../../forms/using/create-form-data-model0.md), como o modelo de dados de formulário para criar fragmentos de documento neste tutorial.

## Etapa 1: Criar fragmento de documento de Detalhes da Lista {#step-create-bill-details-text-document-fragment}

O fragmento de documento Detalhes da Lista inclui os seguintes campos:

| Texto | Fonte de Dados |
|---|---|
| Números da fatura | IU do agente |
| Período de Faturamento | IU do agente |
| Data da Cobrança | IU do agente |
| Seu plano | Modelo de dados do formulário |

Execute as etapas a seguir para criar variáveis para campos com a interface do usuário do agente como a fonte de dados, criar texto estático e usar elementos do modelo de dados de formulário no fragmento do documento:

1. Selecione **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos de Documento]**.

1. Selecione **Criar** > **Texto**.
1. Especifique as seguintes informações:

   1. Insira **bill_details_first_ic** como o nome no campo **Title**. O título é preenchido automaticamente no campo **Nome**.

   1. Selecione **Modelo de dados de formulário** na seção **Modelo de dados**.

   1. Selecione **FDM_Create_First_IC** como o modelo de dados de formulário e toque em **Selecionar**.

   1. Toque em **Próximo**.

1. Selecione a guia **Variables** no painel esquerdo e toque em **Create**.
1. Na seção **Criar variável**:

   1. Insira **Invoicenumber** como o nome da variável.
   1. Selecione **String** como tipo.
   1. Toque em **Criar**.

   ![Criar variável do tipo String](assets/variable_create_string_new.png)

   Repita as etapas 4 e 5 para criar as seguintes variáveis:

   * Período: Tipo de string
   * Data da Lista: Tipo de data

   ![Detalhes da Lista](assets/variable_bill_details_new.png)

1. Crie texto estático para os seguintes campos usando o painel direito:

   * Números da fatura
   * Período de Faturamento
   * Data da Cobrança
   * Seu plano

   ![Texto estático](assets/variable_bill_details_static_text_new.png)

1. Coloque o cursor ao lado do campo **Invoice No** e clique duas vezes na variável **InvoiceNumber** da guia **Variables** no painel esquerdo.
1. Posicione o cursor ao lado do campo **Período de cobrança** e clique duas vezes na variável **Período de cobrança**.
1. Posicione o cursor ao lado do campo **Data da cobrança** e clique duas vezes na variável **Data da cobrança**.
1. Selecione a guia **Objetos de Modelo de Dados** no painel esquerdo.
1. Coloque o cursor ao lado do campo **Seu Plano** e clique duas vezes na propriedade **customer** > **customerplan**.

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. Clique em **Salvar** para criar o fragmento de documento Detalhes da Lista .

## Etapa 2: Criar fragmento do documento de texto Detalhes do cliente {#step-create-customer-details-text-document-fragment}

O fragmento de documento Detalhes do cliente inclui os seguintes campos:

| Texto | Fonte de Dados |
|---|---|
| Nome do cliente | Modelo de dados do formulário |
| Endereço | Modelo de dados do formulário |
| Local de fornecimento | IU do agente |
| Código do Estado | IU do agente |
| Número do celular | Modelo de dados do formulário |
| Número de Contato Alternativo | Modelo de dados do formulário |
| Número do relacionamento | Modelo de dados do formulário |
| Número de Conexões | IU do agente |

Execute as etapas a seguir para criar variáveis para campos com a interface do usuário do agente como a fonte de dados, criar texto estático e usar elementos do modelo de dados de formulário no fragmento do documento:

1. Selecione **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos de Documento]**.
1. Selecione **Criar** > **Texto**.
1. Especifique as seguintes informações:

   1. Insira **customer_details_first_ic** como o nome no campo **Title**. O título é preenchido automaticamente no campo **Nome**.

   1. Selecione **Modelo de dados de formulário** na seção **Modelo de dados**.

   1. Selecione **FDM_Create_First_IC** como o modelo de dados de formulário e toque em **Selecionar**.

   1. Toque em **Próximo**.

1. Selecione a guia **Variables** no painel esquerdo e toque em **Create**.
1. Na seção **Criar variável**:

   1. Insira **Places** como o nome da variável.
   1. Selecione **String** como tipo.
   1. Toque em **Criar**.

   Repita as etapas 4 e 5 para criar as seguintes variáveis:

   * Código de estado: Tipo de número
   * Numerconexões: Tipo de número


1. Selecione a guia **Objetos do Modelo de Dados**, coloque o cursor no painel direito e clique duas vezes na propriedade **customer** > **name**.
1. Pressione Enter para mover o cursor para a próxima linha e clique duas vezes na propriedade **customer** > **address**.
1. Crie texto estático para os seguintes campos usando o painel direito:

   * Número do celular
   * Número de Contato Alternativo
   * Local de fornecimento
   * Número do relacionamento
   * Código do Estado
   * Número de conexões

   ![Texto estático dos detalhes do cliente](assets/customer_details_static_text_new.png)

1. Coloque o cursor ao lado do campo **Mobile Number** e clique duas vezes na propriedade **customer** > **mobilenum**.
1. Coloque o cursor ao lado do campo **Alternate Contact Number** e clique duas vezes na propriedade** customer** > **alternatemobilenumber**.
1. Coloque o cursor ao lado do campo **Número do relacionamento** e clique duas vezes na propriedade **customer** > **relation number**.
1. Selecione a guia **Variables**, coloque o cursor próximo ao campo **Local de Suprimento** e clique duas vezes na variável **Places**.
1. Coloque o cursor ao lado do campo **State Code** e clique duas vezes na variável **Statecode**.
1. Coloque o cursor ao lado do campo **Number of Connections** e clique duas vezes na variável **Numberconnections**.

   ![Detalhes do cliente](assets/customer_details_df2_new.png)

1. Clique em **Save** para criar o fragmento de documento Detalhes do cliente.

## Etapa 3: Criar fragmento de documento de resumo de lista {#step-create-bill-summary-text-document-fragment}

O fragmento de documento Resumo da Lista inclui os seguintes campos:

| Texto | Fonte de Dados |
|---|---|
| Saldo anterior | IU do agente |
| Pagamentos | IU do agente |
| Ajustamentos | IU do agente |
| Encargos do período de faturamento atual | Modelo de dados do formulário |
| Valor devido | IU do agente |
| Data de vencimento | IU do agente |

Execute as etapas a seguir para criar variáveis para campos com a interface do usuário do agente como a fonte de dados, criar texto estático e usar elementos do modelo de dados de formulário no fragmento do documento:

1. Selecione **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos de Documento]**.
1. Selecione **Criar** > **Texto**.
1. Especifique as seguintes informações:

   1. Insira **bill_summary_first_ic** como o nome no campo **Title**. O título é preenchido automaticamente no campo **Nome**.

   1. Selecione **Modelo de dados de formulário** na seção **Modelo de dados**.

   1. Selecione **FDM_Create_First_IC** como o modelo de dados de formulário e toque em **Selecionar**.

   1. Toque em **Próximo**.

1. Selecione a guia **Variables** no painel esquerdo e toque em **Create**.
1. Na seção **Criar variável**:

   1. Insira **Previousbalance** como o nome da variável.
   1. Selecione **Number** como tipo.
   1. Toque em **Criar**.

   Repita as etapas 4 e 5 para criar as seguintes variáveis:

   * Pagamentos: Tipo de número
   * Ajustamentos: Tipo de número
   * Montante devido: Tipo de número
   * Duedata: Tipo de data


1. Crie texto estático para os seguintes campos usando o painel direito:

   * Saldo anterior
   * Pagamentos
   * Ajustamentos
   * Encargos do período de faturamento atual
   * Valor devido
   * Data de vencimento
   * Encargos por pagamento atrasado após Data de Vencimento é $ 20

   ![Texto estático do Resumo da Lista](assets/bill_summary_static_new.png)

1. Posicione o cursor ao lado do campo **Previous Balance** e clique duas vezes na variável **Previousbalance**.
1. Coloque o cursor ao lado do campo **Payments** e clique duas vezes na variável **Payments**.
1. Coloque o cursor ao lado do campo **Ajustes** e clique duas vezes na variável **Ajustes**.
1. Coloque o cursor ao lado do campo **Valor devido** e clique duas vezes na variável **Valor devido**.
1. Posicione o cursor ao lado do campo **Data de vencimento** e clique duas vezes na variável **Duedate**.
1. Selecione a guia **Objetos do Modelo de Dados**, coloque o cursor próximo ao campo **Encargos do período de faturamento atual** no painel direito e clique duas vezes na propriedade **bill** > **usagecharges**.

   ![Resumo da fatura](assets/bill_summary_static_variables_new.png)

1. Clique em **Save** para criar o fragmento de documento Detalhes do cliente.

## Etapa 4: Criar Resumo do fragmento do documento de texto de encargos {#step-create-summary-of-charges-text-document-fragment}

O fragmento do documento Resumo de encargos inclui os seguintes campos:

| Texto | Fonte de Dados |
|---|---|
| Encargos de Chamada | Modelo de dados do formulário |
| Encargos de Chamada em Conferência | Modelo de dados do formulário |
| Encargos SMS | Modelo de dados do formulário |
| Tarifas de Internet Móvel | Modelo de dados do formulário |
| Encargos de roaming nacional | Modelo de dados do formulário |
| Encargos de roaming internacional | Modelo de dados do formulário |
| Encargos de Serviços de Valor Acrescentado | Modelo de dados do formulário |
| Encargos Totais | Modelo de dados do formulário |
| TOTAL A PAGAR | Modelo de dados do formulário |

Execute as seguintes etapas para criar texto estático e usar elementos do modelo de dados de formulário no fragmento do documento:

1. Selecione **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos de Documento]**.
1. Selecione **Criar** > **Texto**.
1. Especifique as seguintes informações:

   1. Insira **summary_charge_first_ic** como o nome no campo **Title**. O título é preenchido automaticamente no campo Nome .

   1. Selecione **Modelo de dados de formulário** na seção **Modelo de dados**.

   1. Selecione **FDM_Create_First_IC** como o modelo de dados de formulário e toque em **Selecionar**.

   1. Toque em **Próximo**.

1. Crie texto estático para os seguintes campos usando o painel direito:

   * Encargos de Chamada
   * Encargos de Chamada em Conferência
   * Encargos SMS
   * Tarifas de Internet Móvel
   * Encargos de roaming nacional
   * Encargos de roaming internacional
   * Encargos de Serviços de Valor Acrescentado
   * Encargos Totais
   * TOTAL A PAGAR

   ![Encargos Sumários](assets/summary_charges_static_new.png)

1. Selecione a guia **Objetos do Modelo de Dados**.
1. Coloque o cursor ao lado do campo **Call Charges** e clique duas vezes na propriedade **bill** > **callcharge**.
1. Coloque o cursor ao lado do campo **Encargos de chamada de conferência** e clique duas vezes na propriedade **bill** > **confcallcharge**.
1. Coloque o cursor ao lado do campo **SMS Charges** e clique duas vezes na propriedade **bill** > **smscharges**.
1. Coloque o cursor ao lado do campo **Mobile Internet Charges** e clique duas vezes na propriedade **bill** > **internetcharge**.
1. Coloque o cursor ao lado do campo **Encargos de roaming nacional** e clique duas vezes na propriedade **bill** > **roamingnational**.
1. Coloque o cursor ao lado do campo **Encargos de roaming internacional** e clique duas vezes na propriedade **bill** > **roamingintnl**.
1. Coloque o cursor ao lado do campo **Encargos de serviços de valor agregado** e clique duas vezes na propriedade **bill** > **vas**.
1. Coloque o cursor ao lado do campo **Total de encargos** e clique duas vezes na propriedade **bill** > **usagecharges**.
1. Coloque o cursor ao lado do campo **TOTAL PAYABLE** e clique duas vezes na propriedade **bill** > **usagecharges**.

   ![Resumo dos Encargos](assets/summary_charges_static_fdm_new.png)

1. Selecione o texto na linha **Encargos de Serviços de Valor Agregado** e toque em **Criar Regra** para criar uma condição baseada na qual a linha é exibida na Comunicação Interativa:
1. Na janela pop-up **Criar regra**:

   1. Selecione **Modelos de Dados e Variáveis** e **listas** > **encargos de chamada**.

   1. Selecione **é menor que** como operador.
   1. Selecione **Number** e insira o valor como **60**.

   Com base nessa condição, a linha Encargos de Serviços de Valor Agregado é exibida somente se o valor do campo Encargos de Chamada for menor que 60.

   ![create_rules_caption](assets/create_rules_caption.gif)

1. Clique em **Save** para criar o fragmento de documento Resumo de encargos.
