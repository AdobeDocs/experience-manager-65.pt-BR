---
title: Aplicar regras a campos de formulário adaptáveis
description: Crie regras para adicionar interatividade, lógica de negócios e validações inteligentes a um formulário adaptável.
page-status-flag: de-activated
products: SG_EXPERIENCEMANAGER/6.3/FORMS
exl-id: 0202ca65-21ef-4477-b704-7b52314a7d7b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 0%

---

# Tutorial: aplicar regras a campos de formulário adaptáveis {#tutorial-apply-rules-to-adaptive-form-fields}

![06-aplicar-regras-ao-formulário-adaptável_principal](assets/06-apply-rules-to-adaptive-form_main.png)

Este tutorial é uma etapa da série [Criar o primeiro formulário adaptável](/help/forms/using/create-your-first-adaptive-form.md). A Adobe recomenda seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso completo do tutorial.

## Sobre o tutorial {#about-the-tutorial}

Você pode usar regras para adicionar interatividade, lógica de negócios e validações inteligentes a um formulário adaptável. Os formulários adaptáveis têm um editor de regras incorporado. O editor de regras fornece uma funcionalidade de arrastar e soltar, semelhante às visitas guiadas. O método arrastar e soltar é o método mais rápido e fácil de criar regras. O editor de regras também fornece uma janela de código para usuários interessados em testar suas habilidades de codificação ou levar as regras para o próximo nível.

Você pode saber mais sobre o editor de regras em [Editor de regras do Adaptive Forms](/help/forms/using/rule-editor.md).

Ao final do tutorial, você aprenderá a criar regras para:

* Chamar um serviço de modelo de dados de formulário para recuperar dados do banco de dados
* Chamar um serviço de modelo de dados de formulário para adicionar dados ao banco de dados
* Executar uma verificação de validações e exibir mensagens de erro

As imagens de GIF interativas no final de cada seção do tutorial ajudam a aprender e validar a funcionalidade do formulário que está sendo criado, dinamicamente.

## Etapa 1: Recuperar um registro de cliente do banco de dados {#retrieve-customer-record}

Você criou um modelo de dados de formulário seguindo o artigo [criar modelo de dados de formulário](/help/forms/using/create-form-data-model.md). Agora, você pode usar o editor de regras para chamar os serviços do Modelo de dados da Forms para recuperar e adicionar informações ao banco de dados.

A cada cliente é atribuído um número exclusivo de ID do cliente, que ajuda a identificar dados relevantes do cliente em um banco de dados. O procedimento abaixo usa a ID do cliente para recuperar informações do banco de dados:

1. Abra o formulário adaptável para edição.

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. Selecione o campo **[!UICONTROL ID do cliente]** e selecione o ícone **[!UICONTROL Editar regras]**. A janela Editor de regras é aberta.
1. Selecione o ícone **[!UICONTROL + Criar]** para adicionar uma regra. Ele abre o Editor visual.

   No Editor visual, a instrução **[!UICONTROL WHEN]** é selecionada por padrão. Além disso, o objeto de formulário (neste caso, **[!UICONTROL ID do Cliente]**) de onde você iniciou o editor de regras é especificado na instrução **[!UICONTROL WHEN]**.

1. Selecione o menu suspenso **[!UICONTROL Selecionar estado]** e selecione **[!UICONTROL foi alterado]**.

   ![quando customeridischanged](assets/whencustomeridischanged.png)

1. Na instrução **[!UICONTROL THEN]**, selecione **[!UICONTROL Invocar Serviço]** no menu suspenso **[!UICONTROL Selecionar Ação]**.
1. Selecione o serviço **[!UICONTROL Recuperar Endereço de Remessa]** na lista suspensa **[!UICONTROL Selecionar]**.
1. Arraste e solte o campo **[!UICONTROL ID do Cliente]** da guia Objetos de Formulário para o campo **[!UICONTROL Soltar objeto ou selecionar aqui]** na caixa **[!UICONTROL ENTRADA]**.

   ![dropobjectstoinputfield-retrievedata](assets/dropobjectstoinputfield-retrievedata.png)

1. Arraste e solte o campo **[!UICONTROL ID do Cliente, Nome, Endereço de Remessa, Estado e CEP]** da guia Objetos de Formulário para o campo **[!UICONTROL Soltar objeto ou selecionar aqui]** na caixa **[!UICONTROL SAÍDA]**.

   ![dropobjectstooutputfield-retrievedata](assets/dropobjectstooutputfield-retrievedata.png)

   Selecione **[!UICONTROL Concluído]** para salvar a regra. Na janela do editor de regras, selecione **[!UICONTROL Fechar]**.

1. Visualize o formulário adaptável. Digite uma ID no campo **[!UICONTROL ID do cliente]**. O formulário agora pode recuperar detalhes do cliente do banco de dados.

   ![recuperar-informações](assets/retrieve-information.gif)

## Etapa 2: adicionar o endereço atualizado do cliente ao banco de dados {#updated-customer-address}

Depois que os detalhes do cliente forem recuperados do banco de dados, você poderá atualizar o endereço de entrega, o estado e o CEP. O procedimento abaixo chama um serviço de Modelo de dados de formulário para atualizar as informações do cliente para o banco de dados:

1. Selecione o campo **[!UICONTROL Enviar]** e selecione o ícone **[!UICONTROL Editar Regras]**. A janela Editor de regras é aberta.
1. Selecione a regra **[!UICONTROL Enviar - Clique]** e selecione o ícone **[!UICONTROL Editar]**. As opções para editar a regra Enviar são exibidas.

   ![regra de envio](assets/submit-rule.png)

   Na opção QUANDO, as opções **[!UICONTROL Enviar]** e **[!UICONTROL é clicado]** já estão selecionadas.

   ![enviar-é-clicado](assets/submit-is-clicked.png)

1. Na opção **[!UICONTROL THEN]**, selecione a opção **[!UICONTROL + Adicionar instrução]**. Selecione **[!UICONTROL Invocar Serviço]** no menu suspenso **[!UICONTROL Selecionar Ação]**.
1. Selecione o serviço **[!UICONTROL Atualizar Endereço de Remessa]** no menu suspenso **[!UICONTROL Selecionar]**.

   ![update-shipping-address](assets/update-shipping-address.png)

   ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. Arraste e solte o campo **[!UICONTROL Endereço de Remessa, Estado e CEP]** da guia [!UICONTROL Objetos de Formulário] para a propriedade de nome de tabela .correspondente (por exemplo, customerdetails .shippingAddress) do objeto **[!UICONTROL Soltar ou selecione aqui o campo]** na caixa **[!UICONTROL ENTRADA]**. Todos os campos com o prefixo tablename (por exemplo, customerdetails neste caso de uso) servem como dados de entrada para o serviço de atualização. Todo o conteúdo fornecido nesses campos é atualizado na fonte de dados.

   >[!NOTE]
   >
   >Não arraste e solte os campos **[!UICONTROL Nome]** e **[!UICONTROL ID do Cliente]** na tablename.property correspondente (por exemplo, customerdetails.name). Ajuda a evitar a atualização do nome e da ID do cliente por engano.

1. Arraste e solte o campo **[!UICONTROL ID do cliente]** da guia [!UICONTROL Objetos de formulário] para o campo de ID na caixa **[!UICONTROL ENTRADA]**. Os campos sem um nome de tabela prefixado (por exemplo, customerdetails neste caso de uso) servem como parâmetro de pesquisa para o serviço de atualização. O campo **[!UICONTROL id]** neste caso de uso identifica exclusivamente um registro na tabela **customerdetails**.
1. Selecione **[!UICONTROL Concluído]** para salvar a regra. Na janela do editor de regras, selecione **[!UICONTROL Fechar]**.
1. Visualize o formulário adaptável. Recupere os detalhes de um cliente, atualize o endereço de entrega e envie o formulário. Ao recuperar os detalhes do mesmo cliente novamente, o endereço de entrega atualizado é exibido.

## Etapa 3: (seção de bônus) usar o editor de código do para executar validações e exibir mensagens de erro {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

Você deve executar a validação no formulário para garantir que os dados inseridos nele estejam corretos e uma mensagem de erro seja exibida se houver dados incorretos. Por exemplo, se uma ID de cliente não existente for inserida no formulário, uma mensagem de erro será exibida.

Os formulários adaptáveis fornecem vários componentes com validações integradas, por exemplo, email e campos numéricos que você pode usar para casos de uso comuns. Use o editor de regras para casos de uso avançados, por exemplo, para exibir uma mensagem de erro quando o banco de dados retornar zero (0) registros (sem registros).

O procedimento a seguir mostra como criar uma regra para exibir uma mensagem de erro se a ID do cliente inserida no formulário não existir no banco de dados. A regra também traz o foco para e redefine o campo **[!UICONTROL ID do cliente]**. A regra usa [a API dataIntegrationUtils do serviço de modelo de dados de formulário](/help/forms/using/invoke-form-data-model-services.md) para verificar se a ID do cliente existe no banco de dados.

1. Selecione o campo **[!UICONTROL ID do cliente]** e selecione o ícone `Edit Rules`. A janela [!UICONTROL Editor de regras] é aberta.
1. Selecione o ícone **[!UICONTROL + Criar]** para adicionar uma regra. Ele abre o Editor visual.

   No Editor visual, a instrução **[!UICONTROL WHEN]** é selecionada por padrão. Além disso, o objeto de formulário (neste caso, **[!UICONTROL ID do Cliente]**) de onde você iniciou o editor de regras é especificado na instrução **[!UICONTROL WHEN]**.

1. Selecione o menu suspenso **[!UICONTROL Selecionar estado]** e selecione **[!UICONTROL foi alterado]**.

   ![quando customeridischanged](assets/whencustomeridischanged.png)

   Na instrução **[!UICONTROL THEN]**, selecione **[!UICONTROL Invocar Serviço]** no menu suspenso **[!UICONTROL Selecionar Ação]**.

1. Mudar do **[!UICONTROL Editor Visual]** para o **[!UICONTROL Editor de Código]**. O controle do switch está no lado direito da janela. O Editor de códigos é aberto, exibindo o código semelhante ao seguinte:

   ![editor de código](assets/code-editor.png)

1. Substitua a seção da variável de entrada pelo seguinte código:

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. Substitua a seção `guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)` pelo seguinte código:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, function (result) {
     if (result) {
         result = JSON.parse(result);
       customer_Name.value = result.name;
       customer_Shipping_Address = result.shippingAddress;
     } else {
       if(window.confirm("Invalid Customer ID. Provide a valid customer ID")) {
             customer_Name.value = " ";
            guideBridge.setFocus(customer_ID);
       }
     }
   });
   ```

1. Visualize o formulário adaptável. Insira uma ID de cliente incorreta. Uma mensagem de erro é exibida.

   ![erro-validação-exibição](assets/display-validation-error.gif)
