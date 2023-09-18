---
title: "Tutorial: Criar fragmentos de documento"
description: Criar fragmentos de documento para comunicação interativa
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: 81429735-cd52-4621-8dc2-10dd89df3052
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '1674'
ht-degree: 2%

---

# Tutorial: Criar fragmentos de documento{#tutorial-create-document-fragments}

![05-criar-formulário-modelo-dados-principal_pequeno](assets/05-create-form-data-model-main_small.png)

Este tutorial é uma etapa da [Criar a primeira comunicação interativa](/help/forms/using/create-your-first-interactive-communication.md) série. A Adobe recomenda que você siga a série em sequência cronológica para entender, executar e demonstrar o caso de uso tutorial completo.

Os fragmentos de documento são componentes reutilizáveis de uma correspondência usados para compor uma comunicação interativa. Os fragmentos de documento são dos seguintes tipos:

* Texto - Um ativo de texto é um conteúdo que consiste em um ou mais parágrafos de texto. Um parágrafo pode ser estático ou dinâmico.
* Lista - Lista é um grupo de fragmentos de documento, incluindo texto, listas, condições e imagens.
* Condição - As condições permitem definir qual conteúdo é incluído na Comunicação interativa com base nos dados recebidos do Modelo de dados de formulário.

Este tutorial percorre as etapas para criar vários fragmentos de documento de texto com base na anatomia fornecida em [Planejar a comunicação interativa](/help/forms/using/planning-interactive-communications.md) seção. No final deste tutorial, você poderá fazer o seguinte:

* Criar fragmentos de documento
* Criar variáveis
* Criar e aplicar regras

![text_document_fragments](assets/text_document_fragments.gif)

Esta é a lista de fragmentos de documento criados neste tutorial:

* [Detalhes da fatura](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [Detalhes do cliente](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [Resumo da fatura](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [Resumo dos encargos](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

Cada fragmento de documento inclui campos com texto estático, dados recebidos do modelo de dados de formulário e dados inseridos usando a interface do usuário do agente. Todos esses campos foram descritos no [Planejar a comunicação interativa](/help/forms/using/planning-interactive-communications.md) seção.

Ao criar fragmentos de documento neste tutorial, as variáveis são criadas para campos que recebem dados usando a interface do usuário do agente.

Uso **FDM_Create_First_IC**, conforme descrito na seção [Criar modelo de dados de formulário](../../forms/using/create-form-data-model0.md) como o modelo de dados de formulário para criar fragmentos de documento neste tutorial.

## Etapa 1: Criar fragmento de documento de texto de Detalhes da Lista {#step-create-bill-details-text-document-fragment}

O Fragmento do Documento Detalhes da Lista inclui os seguintes campos:

| Texto | Fonte de Dados |
|---|---|
| Número da Fatura | IU do agente |
| Período de Cobrança | IU do agente |
| Data de Cobrança | IU do agente |
| Seu plano | Modelo de dados do formulário |

Para criar variáveis para campos com a interface do usuário do agente como fonte de dados, criar texto estático e usar elementos do modelo de dados de formulário no fragmento do documento, faça o seguinte:

1. Selecionar **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos do documento]**.

1. Selecionar **Criar** > **Texto**.
1. Especifique as seguintes informações:

   1. Enter **bill_details_first_ic** como o nome na variável **Título** campo. O título é preenchido automaticamente na variável **Nome** campo.

   1. Selecionar **Modelo de dados do formulário** do **Modelo de dados** seção.

   1. Selecionar **FDM_Create_First_IC** como o modelo de dados do formulário e toque em **Selecionar**.

   1. Toque **Próxima**.

1. Selecione o **Variáveis** no painel esquerdo e toque em **Criar**.
1. No **Criar variável** seção:

   1. Enter **Invoicenumber** como o nome da variável.
   1. Selecionar **String** como o tipo.
   1. Toque em **Criar**.

   ![Criar variável do tipo String](assets/variable_create_string_new.png)

   Repita as etapas 4 e 5 para criar as seguintes variáveis:

   * Billperiod: tipo de cadeia de caracteres
   * BillDate: Tipo de data

   ![Detalhes da Lista](assets/variable_bill_details_new.png)

1. Crie texto estático para os seguintes campos usando o painel direito:

   * Número da Fatura
   * Período de Cobrança
   * Data de Cobrança
   * Seu plano

   ![Texto estático](assets/variable_bill_details_static_text_new.png)

1. Coloque o cursor próximo ao **Número da Fatura** e clique duas vezes no botão **NúmeroDaFatura** variável do **Variáveis** no painel esquerdo.
1. Coloque o cursor próximo ao **Período de Cobrança** e clique duas vezes no botão **Billperiod** variável.
1. Coloque o cursor próximo ao **Data de Cobrança** e clique duas vezes no botão **Data de Cobrança** variável.
1. Selecione o **Objetos do modelo de dados** no painel esquerdo.
1. Coloque o cursor próximo ao **Seu plano** e clique duas vezes no botão **cliente** > **customerplan** propriedade.

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. Clique em **Salvar** para criar o fragmento de documento de texto Detalhes da lista.

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

1. Selecionar **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos do documento]**.
1. Selecionar **Criar** > **Texto**.
1. Especifique as seguintes informações:

   1. Enter **customer_details_first_ic** como o nome na variável **Título** campo. O título é preenchido automaticamente na variável **Nome** campo.

   1. Selecionar **Modelo de dados do formulário** do **Modelo de dados** seção.

   1. Selecionar **FDM_Create_First_IC** como o modelo de dados do formulário e toque em **Selecionar**.

   1. Toque **Próxima**.

1. Selecione o **Variáveis** no painel esquerdo e toque em **Criar**.
1. No **Criar variável** seção:

   1. Enter **Placesupply** como o nome da variável.
   1. Selecionar **String** como o tipo.
   1. Toque em **Criar**.

   Repita as etapas 4 e 5 para criar as seguintes variáveis:

   * Statecode: Tipo numérico
   * Numberconnections: Tipo de número

1. Selecione o **Objetos do modelo de dados** coloque o cursor no painel direito e clique duas vezes na guia **cliente** > **name** propriedade.
1. Pressione Enter para mover o cursor para a próxima linha e clique duas vezes no **cliente** > **endereço** propriedade.
1. Crie texto estático para os seguintes campos usando o painel direito:

   * Número de celular
   * Número de Contato Alternativo
   * Local de fornecimento
   * Número do relacionamento
   * Código de Estado
   * Número de conexões

   ![Texto estático de detalhes do cliente](assets/customer_details_static_text_new.png)

1. Coloque o cursor próximo ao **Número de celular** e clique duas vezes no botão **cliente** > **mobilenum** propriedade.
1. Coloque o cursor próximo ao **Número de Contato Alternativo** e clique duas vezes em ** customer** > **alternatemobilenumber** propriedade.
1. Coloque o cursor próximo ao **Número do relacionamento** e clique duas vezes no botão **cliente** > **número do relacionamento** propriedade.
1. Selecione o **Variáveis** coloque o cursor próximo à guia **Local de fornecimento** e clique duas vezes no botão **Placesupply** variável.
1. Coloque o cursor próximo ao **Código de Estado** e clique duas vezes no botão **Statecode** variável.
1. Coloque o cursor próximo ao **Número de conexões** e clique duas vezes no botão **Numberconnections** variável.

   ![Detalhes do cliente](assets/customer_details_df2_new.png)

1. Clique em **Salvar** para criar o Fragmento de documento de texto de Detalhes do cliente.

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

1. Selecionar **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos do documento]**.
1. Selecionar **Criar** > **Texto**.
1. Especifique as seguintes informações:

   1. Enter **bill_summary_first_ic** como o nome na variável **Título** campo. O título é preenchido automaticamente na variável **Nome** campo.

   1. Selecionar **Modelo de dados do formulário** do **Modelo de dados** seção.

   1. Selecionar **FDM_Create_First_IC** como o modelo de dados do formulário e toque em **Selecionar**.

   1. Toque **Próxima**.

1. Selecione o **Variáveis** no painel esquerdo e toque em **Criar**.
1. No **Criar variável** seção:

   1. Enter **Saldo anterior** como o nome da variável.
   1. Selecionar **Número** como tipo.
   1. Toque em **Criar**.

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

1. Coloque o cursor próximo ao **Saldo Anterior** e clique duas vezes no botão **Saldo anterior** variável.
1. Coloque o cursor próximo ao **Pagamentos** e clique duas vezes no botão **Pagamentos** variável.
1. Coloque o cursor próximo ao **Ajustes** e clique duas vezes no botão **Ajustes** variável.
1. Coloque o cursor próximo ao **Valor Devido** e clique duas vezes no botão **Valor devido** variável.
1. Coloque o cursor próximo ao **Prazo** e clique duas vezes no botão **Data final** variável.
1. Selecione o **Objetos do modelo de dados** coloque o cursor próximo à guia **Cobra o período de faturamento atual** no painel direito e clique duas vezes na guia **faturas** > **encargos de uso** propriedade.

   ![Resumo da fatura](assets/bill_summary_static_variables_new.png)

1. Clique em **Salvar** para criar o Fragmento de documento de texto de Detalhes do cliente.

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

1. Selecionar **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos do documento]**.
1. Selecionar **Criar** > **Texto**.
1. Especifique as seguintes informações:

   1. Enter **summary_charge_first_ic** como o nome na variável **Título** campo. O título é preenchido automaticamente no campo Nome.

   1. Selecionar **Modelo de dados do formulário** do **Modelo de dados** seção.

   1. Selecionar **FDM_Create_First_IC** como o modelo de dados do formulário e toque em **Selecionar**.

   1. Toque **Próxima**.

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

   ![Encargos Resumidos](assets/summary_charges_static_new.png)

1. Selecione o **Objetos do modelo de dados** guia.
1. Coloque o cursor próximo ao **Encargos de chamada** e clique duas vezes no botão **faturas** > **encargos de chamada** propriedade.
1. Coloque o cursor próximo ao **Encargos de Chamada em Conferência** e clique duas vezes no botão **faturas** > **confcallcharge** propriedade.
1. Coloque o cursor próximo ao **Encargos de SMS** e clique duas vezes no botão **faturas** > **smscharge** propriedade.
1. Coloque o cursor próximo ao **Encargos de Internet Móvel** e clique duas vezes no botão **faturas** > **taxas de internet** propriedade.
1. Coloque o cursor próximo ao **Tarifas de roaming nacional** e clique duas vezes no botão **faturas** > **roamingnational** propriedade.
1. Coloque o cursor próximo ao **Tarifas de roaming internacional** e clique duas vezes no botão **faturas** > **roamingintnl** propriedade.
1. Coloque o cursor próximo ao **Encargos de Serviços de Valor Agregado** e clique duas vezes no botão **faturas** > **vas** propriedade.
1. Coloque o cursor próximo ao **Total de Encargos** e clique duas vezes no botão **faturas** > **encargos de uso** propriedade.
1. Coloque o cursor próximo ao **TOTAL A PAGAR** e clique duas vezes no botão **faturas** > **encargos de uso** propriedade.

   ![Resumo de Encargos](assets/summary_charges_static_fdm_new.png)

1. Selecione o texto no campo **Encargos de Serviços de Valor Agregado** linha e toque **Criar regra** para criar uma condição com base na qual a linha é exibida na Comunicação Interativa:
1. No **Criar regra** janela pop-up:

   1. Selecionar **Variáveis e modelos de dados** e depois **faturas** > **encargos de chamada**.

   1. Selecionar **é menor que** como operador.
   1. Selecionar **Número** e insira o valor como **60**.

   Com base nessa condição, a linha Encargos de Serviços de Valor Agregado será exibida somente se o valor do campo Encargos de Chamada for menor que 60.

   ![create_rules_caption](assets/create_rules_caption.gif)

1. Clique em **Salvar** para criar o texto Fragmento do documento do Resumo de encargos.
