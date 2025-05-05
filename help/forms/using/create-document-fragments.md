---
title: 'Tutorial: Criar fragmentos de documento'
description: Criar fragmentos de documento para comunicação interativa
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: 81429735-cd52-4621-8dc2-10dd89df3052
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1653'
ht-degree: 3%

---

# Tutorial: Criar fragmentos de documento{#tutorial-create-document-fragments}

![05-criar-formulário-modelo-dados-principal_pequeno](assets/05-create-form-data-model-main_small.png)

Este tutorial é uma etapa da série [Criar sua primeira Comunicação Interativa](/help/forms/using/create-your-first-interactive-communication.md). A Adobe recomenda que você siga a série em sequência cronológica para entender, executar e demonstrar o caso de uso tutorial completo.

Os fragmentos de documento são componentes reutilizáveis de uma correspondência usados para compor uma comunicação interativa. Os fragmentos de documento são dos seguintes tipos:

* Texto - Um ativo de texto é um conteúdo que consiste em um ou mais parágrafos de texto. Um parágrafo pode ser estático ou dinâmico.
* Lista - Lista é um grupo de fragmentos de documento, incluindo texto, listas, condições e imagens.
* Condição - As condições permitem definir qual conteúdo é incluído na Comunicação interativa com base nos dados recebidos do Modelo de dados de formulário.

Este tutorial percorre as etapas para criar vários fragmentos de documento de texto com base na anatomia fornecida na seção [Planejar a comunicação interativa](/help/forms/using/planning-interactive-communications.md). No final deste tutorial, você poderá fazer o seguinte:

* Criar fragmentos de documento
* Criar variáveis
* Criar e aplicar regras

![fragmentos_de_documento_de_texto](assets/text_document_fragments.gif)

Esta é a lista de fragmentos de documento criados neste tutorial:

* [Detalhes da fatura](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [Detalhes do cliente](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [Resumo da fatura](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [Resumo dos encargos](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

Cada fragmento de documento inclui campos com texto estático, dados recebidos do modelo de dados de formulário e dados inseridos usando a interface do usuário do agente. Todos esses campos foram descritos na seção [Planejar a Comunicação Interativa](/help/forms/using/planning-interactive-communications.md).

Ao criar fragmentos de documento neste tutorial, as variáveis são criadas para campos que recebem dados usando a interface do usuário do agente.

Use o **FDM_Create_First_IC**, conforme descrito na seção [Criar modelo de dados de formulário](../../forms/using/create-form-data-model0.md), como o modelo de dados de formulário para criar fragmentos de documento neste tutorial.

## Etapa 1: Criar fragmento de documento de texto de Detalhes da Lista {#step-create-bill-details-text-document-fragment}

O Fragmento do Documento Detalhes da Lista inclui os seguintes campos:

| Texto | Fonte de Dados |
|---|---|
| Número da Fatura | IU do agente |
| Período de Cobrança | IU do agente |
| Data de Cobrança | IU do agente |
| Seu plano | Modelo de dados do formulário |

Para criar variáveis para campos com a interface do usuário do agente como fonte de dados, criar texto estático e usar elementos do modelo de dados de formulário no fragmento do documento, faça o seguinte:

1. Selecione **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos de documento]**.

1. Selecione **Criar** > **Texto**.
1. Especifique as seguintes informações:

   1. Insira **bill_details_first_ic** como o nome no campo **Título**. O título é preenchido automaticamente no campo **Nome**.

   1. Selecione **Modelo de Dados de Formulário** na seção **Modelo de Dados**.

   1. Selecione **FDM_Create_First_IC** como o modelo de dados de formulário e selecione **Selecionar**.

   1. Selecione **Próximo**.

1. Selecione a guia **Variáveis** no painel esquerdo e selecione **Criar**.
1. Na seção **Criar Variável**:

   1. Insira **Invoicenumber** como o nome da variável.
   1. Selecione **String** como o tipo.
   1. Selecione **Criar**.

   ![Criar variável do tipo String](assets/variable_create_string_new.png)

   Repita as etapas 4 e 5 para criar as seguintes variáveis:

   * Billperiod: tipo de cadeia de caracteres
   * BillDate: Tipo de data

   ![Detalhes da Conta](assets/variable_bill_details_new.png)

1. Crie texto estático para os seguintes campos usando o painel direito:

   * Número da Fatura
   * Período de Cobrança
   * Data de Cobrança
   * Seu plano

   ![Texto estático](assets/variable_bill_details_static_text_new.png)

1. Posicione o cursor ao lado do campo **Fatura nº** e clique duas vezes na variável **InvoiceNumber** na guia **Variables** no painel esquerdo.
1. Coloque o cursor próximo ao campo **Período de cobrança** e clique duas vezes na variável **Billperiod**.
1. Coloque o cursor próximo ao campo **Data de cobrança** e clique duas vezes na variável **Data de cobrança**.
1. Selecione a guia **Objetos do Modelo de Dados** no painel esquerdo.
1. Coloque o cursor ao lado do campo **Seu Plano** e clique duas vezes na propriedade **customer** > **customerplan**.

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. Clique em **Salvar** para criar o fragmento de documento de texto Detalhes da Lista.

## Etapa 2: Criar texto de Detalhes do cliente Fragmento do documento {#step-create-customer-details-text-document-fragment}

O Fragmento do documento Detalhes do cliente inclui os seguintes campos:

| Texto | Fonte de Dados |
|---|---|
| Nome do cliente | Modelo de dados do formulário |
| Endereço | Modelo de dados do formulário |
| Local de fornecimento | IU do agente |
| Código de Estado | IU do agente |
| Número de celular | Modelo de dados do formulário |
| Número de Contato Alternativo | Modelo de dados do formulário |
| Número do relacionamento | Modelo de dados do formulário |
| Número de conexões | IU do agente |

Para criar variáveis para campos com a interface do usuário do agente como fonte de dados, criar texto estático e usar elementos do modelo de dados de formulário no fragmento do documento, faça o seguinte:

1. Selecione **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos de documento]**.
1. Selecione **Criar** > **Texto**.
1. Especifique as seguintes informações:

   1. Digite **customer_details_first_ic** como o nome no campo **Título**. O título é preenchido automaticamente no campo **Nome**.

   1. Selecione **Modelo de Dados de Formulário** na seção **Modelo de Dados**.

   1. Selecione **FDM_Create_First_IC** como o modelo de dados de formulário e selecione **Selecionar**.

   1. Selecione **Próximo**.

1. Selecione a guia **Variáveis** no painel esquerdo e selecione **Criar**.
1. Na seção **Criar Variável**:

   1. Digite **Placesupply** como o nome da variável.
   1. Selecione **String** como o tipo.
   1. Selecione **Criar**.

   Repita as etapas 4 e 5 para criar as seguintes variáveis:

   * Statecode: Tipo numérico
   * Numberconnections: Tipo de número

1. Selecione a guia **Objetos do Modelo de Dados**, coloque o cursor no painel direito e clique duas vezes na propriedade **customer** > **name**.
1. Pressione Enter para mover o cursor para a próxima linha e clique duas vezes na propriedade **customer** > **address**.
1. Crie texto estático para os seguintes campos usando o painel direito:

   * Número de celular
   * Número de Contato Alternativo
   * Local de fornecimento
   * Número do relacionamento
   * Código de Estado
   * Número de conexões

   ![Texto estático de detalhes do cliente](assets/customer_details_static_text_new.png)

1. Coloque o cursor próximo ao campo **Número de celular** e clique duas vezes na propriedade **customer** > **mobilenum**.
1. Coloque o cursor ao lado do campo **Número de Contato Alternativo** e clique duas vezes na propriedade **&#x200B; customer** > **alternatemobilenumber**.
1. Coloque o cursor ao lado do campo **Número do Relacionamento** e clique duas vezes na propriedade **customer** > **relationship number**.
1. Selecione a guia **Variáveis**, coloque o cursor ao lado do campo **Local de Fornecimento** e clique duas vezes na variável **Placesupply**.
1. Coloque o cursor próximo ao campo **Código do estado** e clique duas vezes na variável **Código do estado**.
1. Coloque o cursor próximo ao campo **Número de Conexões** e clique duas vezes na variável **Numberconnections**.

   ![Detalhes do cliente](assets/customer_details_df2_new.png)

1. Clique em **Salvar** para criar o fragmento de texto de Detalhes do cliente.

## Etapa 3: Criar Fragmento de Documento de Texto de Resumo de Lista {#step-create-bill-summary-text-document-fragment}

O Fragmento do Documento Sumariado de Lista inclui os seguintes campos:

| Texto | Fonte de Dados |
|---|---|
| Saldo Anterior | IU do agente |
| Pagamentos | IU do agente |
| Ajustes | IU do agente |
| Cobra o período de faturamento atual | Modelo de dados do formulário |
| Valor Devido | IU do agente |
| Data de vencimento | IU do agente |

Para criar variáveis para campos com a interface do usuário do agente como fonte de dados, criar texto estático e usar elementos do modelo de dados de formulário no fragmento do documento, faça o seguinte:

1. Selecione **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos de documento]**.
1. Selecione **Criar** > **Texto**.
1. Especifique as seguintes informações:

   1. Insira **bill_summary_first_ic** como o nome no campo **Title**. O título é preenchido automaticamente no campo **Nome**.

   1. Selecione **Modelo de Dados de Formulário** na seção **Modelo de Dados**.

   1. Selecione **FDM_Create_First_IC** como o modelo de dados de formulário e selecione **Selecionar**.

   1. Selecione **Próximo**.

1. Selecione a guia **Variáveis** no painel esquerdo e selecione **Criar**.
1. Na seção **Criar Variável**:

   1. Digite **Previousbalance** como o nome da variável.
   1. Selecione **Número** como tipo.
   1. Selecione **Criar**.

   Repita as etapas 4 e 5 para criar as seguintes variáveis:

   * Pagamentos: Tipo de número
   * Ajustes: Tipo de número
   * Valor devido: Tipo de número
   * Duedate: Tipo de data

1. Crie texto estático para os seguintes campos usando o painel direito:

   * Saldo Anterior
   * Pagamentos
   * Ajustes
   * Cobra o período de faturamento atual
   * Valor Devido
   * Data de vencimento
   * Encargos de pagamento em atraso após a Data de Vencimento é $ 20

   ![Texto estático do Resumo da Lista](assets/bill_summary_static_new.png)

1. Coloque o cursor próximo ao campo **Saldo anterior** e clique duas vezes na variável **Saldo anterior**.
1. Coloque o cursor ao lado do campo **Pagamentos** e clique duas vezes na variável **Pagamentos**.
1. Coloque o cursor próximo ao campo **Ajustes** e clique duas vezes na variável **Ajustes**.
1. Coloque o cursor próximo ao campo **Valor devido** e clique duas vezes na variável **Valor devido**.
1. Coloque o cursor próximo ao campo **Data de vencimento** e clique duas vezes na variável **Data de vencimento**.
1. Selecione a guia **Objetos do Modelo de Dados**, coloque o cursor ao lado do campo **Período de cobrança atual de encargos** no painel direito e clique duas vezes na propriedade **faturas** > **encargos de uso**.

   ![Resumo da fatura](assets/bill_summary_static_variables_new.png)

1. Clique em **Salvar** para criar o fragmento de texto de Detalhes do cliente.

## Etapa 4: Criar Sumário de encargos texto Fragmento do Documento {#step-create-summary-of-charges-text-document-fragment}

O Fragmento do documento do Resumo de encargos inclui os seguintes campos:

| Texto | Fonte de Dados |
|---|---|
| Encargos de chamada | Modelo de dados do formulário |
| Encargos de Chamada em Conferência | Modelo de dados do formulário |
| Encargos de SMS | Modelo de dados do formulário |
| Encargos de Internet Móvel | Modelo de dados do formulário |
| Tarifas de roaming nacional | Modelo de dados do formulário |
| Tarifas de roaming internacional | Modelo de dados do formulário |
| Encargos de Serviços de Valor Agregado | Modelo de dados do formulário |
| Total de Encargos | Modelo de dados do formulário |
| TOTAL A PAGAR | Modelo de dados do formulário |

Para criar texto estático e usar elementos de modelo de dados de formulário no fragmento do documento, faça o seguinte:

1. Selecione **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos de documento]**.
1. Selecione **Criar** > **Texto**.
1. Especifique as seguintes informações:

   1. Insira **summary_charge_first_ic** como o nome no campo **Título**. O título é preenchido automaticamente no campo Nome.

   1. Selecione **Modelo de Dados de Formulário** na seção **Modelo de Dados**.

   1. Selecione **FDM_Create_First_IC** como o modelo de dados de formulário e selecione **Selecionar**.

   1. Selecione **Próximo**.

1. Crie texto estático para os seguintes campos usando o painel direito:

   * Encargos de chamada
   * Encargos de Chamada em Conferência
   * Encargos de SMS
   * Encargos de Internet Móvel
   * Tarifas de roaming nacional
   * Tarifas de roaming internacional
   * Encargos de Serviços de Valor Agregado
   * Total de Encargos
   * TOTAL A PAGAR

   ![Encargos de resumo](assets/summary_charges_static_new.png)

1. Selecione a guia **Objetos do Modelo de Dados**.
1. Coloque o cursor ao lado do campo **Encargos da Chamada** e clique duas vezes na propriedade **contas** > **encargos da chamada**.
1. Coloque o cursor próximo ao campo **Encargos de Chamada em Conferência** e clique duas vezes na propriedade **bill** > **confcallcharge**.
1. Coloque o cursor ao lado do campo **Encargos de SMS** e clique duas vezes na propriedade **contas** > **smscharge**.
1. Coloque o cursor próximo ao campo **Encargos da Internet Móvel** e clique duas vezes na propriedade **contas** > **encargos da Internet**.
1. Coloque o cursor ao lado do campo **Encargos de Roaming Nacional** e clique duas vezes na propriedade **contas** > **roamingnational**.
1. Coloque o cursor próximo ao campo **Encargos de Roaming Internacional** e clique duas vezes na propriedade **bills** > **roamingintnl**.
1. Coloque o cursor próximo ao campo **Encargos de Serviços com Valor Agregado** e clique duas vezes na propriedade **bills** > **vas**.
1. Coloque o cursor próximo ao campo **Total de encargos** e clique duas vezes na propriedade **contas** > **encargos de uso**.
1. Coloque o cursor próximo ao campo **TOTAL A PAGAR** e clique duas vezes na propriedade **contas** > **encargos de uso**.

   ![Resumo dos Encargos](assets/summary_charges_static_fdm_new.png)

1. Selecione o texto na linha **Encargos de Serviços com Valor Agregado** e selecione **Criar Regra** para criar uma condição com base na qual a linha é exibida na Comunicação Interativa:
1. Na janela pop-up **Criar regra**:

   1. Selecione **Modelos de Dados e Variáveis** e depois **contas** > **encargos de chamada**.

   1. Selecione **é menor que** como operador.
   1. Selecione **Número** e insira o valor como **60**.

   Com base nessa condição, a linha Encargos de Serviços de Valor Agregado será exibida somente se o valor do campo Encargos de Chamada for menor que 60.

   ![create_rules_caption](assets/create_rules_caption.gif)

1. Clique em **Salvar** para criar o Resumo do Fragmento de Documento do texto de encargos.
