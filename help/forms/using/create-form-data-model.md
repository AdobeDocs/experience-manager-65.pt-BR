---
title: 'Tutorial: Criar modelo de dados do formulário '
description: Saiba como configurar o MySQL como fonte de dados, criar o modelo de dados de formulário (FDM), configurá-lo e testar o AEM Forms.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
docset: aem65
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
solution: Experience Manager, Experience Manager Forms
feature: Form Data Model
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 1%

---

# Tutorial: Criar modelo de dados do formulário {#tutorial-create-form-data-model}

![04-criar-formulário-modelo-dados-principal](assets/04-create-form-data-model-main.png)

Este tutorial é uma etapa da série [Criar o primeiro formulário adaptável](../../forms/using/create-your-first-adaptive-form.md). A Adobe recomenda que você siga a série em sequência cronológica para entender, executar e demonstrar o caso de uso tutorial completo.

## Sobre o tutorial {#about-the-tutorial}

O módulo de integração de dados AEM [!DNL Forms] permite criar um modelo de dados de formulário a partir de diferentes fontes de dados de back-end, como o perfil de usuário AEM, os serviços Web RESTful, os serviços Web baseados em SOAP, os serviços OData e os bancos de dados relacionais. Você pode configurar serviços e objetos de modelo de dados em um modelo de dados de formulário e associá-lo a um formulário adaptável. Os campos de formulário adaptável são vinculados às propriedades do objeto de modelo de dados. Os serviços permitem preencher previamente o formulário adaptável e gravar dados do formulário enviado de volta no objeto de modelo de dados.

Para obter mais informações sobre a integração de dados de formulário e o modelo de dados de formulário, consulte [Integração de dados do AEM Forms](../../forms/using/data-integration.md).

Este tutorial percorre as etapas para preparar, criar, configurar e associar um modelo de dados de formulário a um formulário adaptável. Ao final deste tutorial, você será capaz de:

* [Configurar o banco de dados MySQL como fonte de dados](#config-database)
* [Criar modelo de dados de formulário usando o banco de dados MySQL](#create-fdm)
* [Configurar modelo de dados do formulário](#config-fdm)
* [Testar modelo de dados do formulário](#test-fdm)

O modelo de dados de formulário será semelhante ao seguinte:

![formulário-modelo-dados_l](assets/form-data-model_l.png)

**A.** Fontes de dados **B.** Esquemas de fonte de dados **C.** Serviços disponíveis **D.** Objetos de modelo de dados **E.** Serviços configurados

## Pré-requisitos {#prerequisites}

Antes de começar, verifique se você tem o seguinte:

* Banco de dados do [!DNL MySQL] com dados de exemplo conforme declarado na seção Pré-requisitos do [Criar o primeiro formulário adaptável](../../forms/using/create-your-first-adaptive-form.md)
* Pacote OSGi para o driver JDBC [!DNL MySQL], conforme explicado em [Agrupando o driver do banco de dados JDBC](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* Formulário adaptável conforme explicado no primeiro tutorial [Criar um formulário adaptável](/help/forms/using/create-adaptive-form.md)

## Etapa 1: configurar o banco de dados MySQL como fonte de dados {#config-database}

É possível configurar diferentes tipos de fontes de dados para criar um modelo de dados de formulário. Para este tutorial, você configura o banco de dados MySQL que configurou e preencheu com dados de amostra. Para obter informações sobre outras fontes de dados com suporte e como configurá-las, consulte [Integração de Dados do AEM Forms](../../forms/using/data-integration.md).

Faça o seguinte para configurar o banco de dados do [!DNL MySQL]:

1. Instale o driver JDBC para [!DNL MySQL] o banco de dados como um osGi pacote:

   1. Baixe [!DNL MySQL] o pacote JDBC Driver OSGi em `http://www.java2s.com/ref/jar/download-orgosgiservicejdbc100jar-file.html`. <!-- This URL is an insecure link but using https is not possible -->
   1. Faça logon na instância do autor [!DNL Forms] do AEM como administrador e acesse os pacotes de console da Web do AEM. A URL padrão é [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Selecione **[!UICONTROL Instalar/Atualizar]**. Uma caixa de diálogo [!UICONTROL Carregar/Instalar Pacotes] é exibida.

   1. Selecione **[!UICONTROL Escolher Arquivo]** para procurar e selecionar o pacote OSGi do driver JDBC [!DNL MySQL]. Selecione **[!UICONTROL Iniciar Pacote]** e **[!UICONTROL Atualizar Pacotes]** e selecione **[!UICONTROL Instalar ou Atualizar]**. Certifique-se de que o [!DNL Oracle Corporation's] Driver [!DNL MySQL] JDBC esteja ativo. O motorista está instalado.

1. Configure [!DNL MySQL] o banco de dados como um fonte de dados:

   1. Acesse AEM console da Web no [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Localize **a configuração do DataSource** com conexão Apache Sling. Selecione para abrir a configuração no modo de edição.
   1. Na caixa de diálogo de configuração, especifique os seguintes detalhes:

      * **Nome da fonte de dados:** Você pode especificar qualquer nome. Por exemplo, especifique **WeRetailMySQL**.
      * **Nome da propriedade de serviço DataSource**: especifique o nome da propriedade de serviço que contém o nome DataSource. É especificado ao registrar a instância da fonte de dados como serviço OSGi. Por exemplo, **datasource.name**.
      * **Classe do driver JDBC**: especifique o nome da classe Java™ do driver JDBC. Para o banco de dados [!DNL MySQL], especifique **com.mysql.jdbc.Driver**.
      * **URI** de conexão JDBC: especifique o URL de conexão do banco de dados. Para [!DNL MySQL] o banco de dados em execução em porta 3306 e schema `weretail`, a URL é: `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`

      >[!NOTE]
      >
      > Quando o banco de dados está atrás de um firewall, o [!DNL MySQL] nome do host do banco de dados não é um DNS público. O endereço IP do banco de dados deve ser adicionado no *arquivo /etc/hosts* do AEM máquina host.

      * **Nome de usuário:** Nome de usuário do banco de dados. É necessário habilitar o driver JDBC para estabelecer uma conexão com o banco de dados.
      * **Senha:** Senha do banco de dados. É necessário habilitar o driver JDBC para estabelecer uma conexão com o banco de dados.

      >[!NOTE]
      >
      >O AEM Forms não oferece suporte à Autenticação NT para [!DNL MySQL]. Vá para AEM console da Web no [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) e pesquisa &quot;Apache Sling Connection Pooled Datasource&quot;. Para &quot;URI de conexão JDBC&quot; propriedade, defina o valor de &quot;Segurança integrada&quot; como Falso e use o nome de usuário e o senha criados para conexão com [!DNL MySQL] o banco de dados.

      * **Testar em Emprestar:** ative a opção **[!UICONTROL Testar em Emprestar]** .
      * **Teste no retorno:** ative a opção **[!UICONTROL Testar no retorno]** .
      * **Consulta de Validação:** especifique uma consulta SQL SELECT para validar as conexões do pool. A consulta deve retornar pelo menos uma linha. Por exemplo, **selecione &#42; em customerdetails**.
      * **Isolamento de Transação**: Defina o valor como **READ_COMMITTED**.

        Deixe as outras propriedades com os [valores](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) padrão e selecione **[!UICONTROL Salvar]**.

        Uma configuração semelhante à seguinte é criada.

        ![configuração-fonte-de-dados-banco-de-dados-relacional](assets/relational-database-data-source-configuration.png)

## Etapa 2: Criar modelo de dados de formulário {#create-fdm}

O AEM [!DNL Forms] fornece uma interface de usuário intuitiva para [criar um modelo de dados de formulário](data-integration.md) a partir de fontes de dados configuradas. É possível usar várias fontes de dados em um modelo de dados de formulário. Neste caso de uso, você pode usar a fonte de dados [!DNL MySQL] configurada.

Faça o seguinte para criar o modelo de dados de formulário:

1. Na instância do autor AEM, navegue até **[!UICONTROL Forms]** > **[!UICONTROL Integrações de Dados]**.
1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Modelo de Dados de Formulário]**.
1. Na caixa de diálogo Criar modelo de dados de formulário, especifique um **nome** para o modelo de dados de formulário. Por exemplo, **customer-shipping-billing-details**. Selecione **[!UICONTROL Próximo]**.
1. A tela selecionar fonte de dados lista todas as fontes de dados configuradas. Selecione a fonte de dados **WeRetailMySQL** e selecione **[!UICONTROL Criar]**.

   ![seleção-fonte-dados](assets/data-source-selection.png)

O modelo de dados de formulário **customer-shipping-billing-details** foi criado.

## Etapa 3: configurar o modelo de dados de formulário {#config-fdm}

A configuração do modelo de dados de formulário envolve:

* adição de objetos e serviços de modelo de dados
* configuração de serviços de leitura e gravação para objetos de modelo de dados

Faça o seguinte para configurar o modelo de dados de formulário:

1. Na instância do autor do AEM, navegue até **[!UICONTROL Forms]** > **[!UICONTROL Integrações de Dados]**. A URL padrão é [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. O **customer-shipping-billing-details** do modelo de dados de formulário criado anteriormente está listado aqui. Abra-o no modo de edição.

   A fonte de dados selecionada **WeRetailMySQL** está configurada no modelo de dados de formulário.

   ![fdm-padrão](assets/default-fdm.png)

1. Expanda a árvore da fonte de dados WeRailMySQL. Selecione os seguintes objetos e serviços de modelo de dados do esquema **weretail** > **customerdetails** para poder formar o modelo de dados:

   * **Objetos do modelo de dados**:

      * id
      * name
      * shippingAddress
      * cidade
      * estado
      * código postal

   * **Serviços:**

      * obter
      * atualizar

   Selecione **Adicionar Selecionados** para adicionar objetos e serviços de modelo de dados selecionados ao modelo de dados de formulário.

   ![Esquema do WeRetail](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >Os serviços padrão de obtenção, atualização e inserção para fontes de dados JDBC são fornecidos com o modelo de dados de formulário pronto para uso.

1. Configure serviços de leitura e gravação para o objeto de modelo de dados.

   1. Selecione o objeto de modelo de dados **customerdetails** e selecione **[!UICONTROL Editar Propriedades]**.
   1. Selecione **[!UICONTROL get]** no menu suspenso Serviço de Leitura. O argumento **id**, que é a chave primária no objeto de modelo de dados customerdetails, é adicionado automaticamente. Selecione ![aem_6_3_edit](assets/aem_6_3_edit.png) e configure o argumento da seguinte maneira.

      ![leitura-padrão](assets/read-default.png)

   1. Da mesma forma, selecione **[!UICONTROL atualizar]** como o Serviço de gravação. O objeto **customerdetails** é adicionado automaticamente como argumento. O argumento é configurado da seguinte maneira.

      ![gravação-padrão](assets/write-default.png)

      Adicione e configure o argumento da **ID** da seguinte maneira.

      ![id-arg](assets/id-arg.png)

   1. Selecione **[!UICONTROL Concluído]** para salvar as propriedades de objetos de modelo de dados. Em seguida, selecione **[!UICONTROL Salvar]** para salvar o modelo de dados do formulário.

      Os serviços **[!UICONTROL get]** e **[!UICONTROL update]** são adicionados como serviços padrão para o objeto de modelo de dados.

      ![objeto-modelo-dados](assets/data-model-object.png)

1. Vá para a guia **[!UICONTROL Serviços]** e configure os serviços **[!UICONTROL obter]** e **[!UICONTROL atualizar]**.

   1. Selecione o serviço **[!UICONTROL get]** e selecione **[!UICONTROL Editar Propriedades]**. A caixa de diálogo de propriedades é aberta.
   1. Especifique o seguinte na caixa de diálogo Propriedades de Editar:

      * **** Título: especifique o título do serviço. Por exemplo: Recuperar endereço de envio.
      * **Descrição**: especifique a descrição que contém o funcionamento detalhado do serviço. Por exemplo:

        Este serviço recupera o endereço de entrega e outros detalhes do cliente do banco de dados [!DNL MySQL]

      * **Objeto de Modelo de Saída**: Selecione um esquema contendo dados do cliente. Por exemplo:

        esquema customerdetail

      * **Retornar matriz**: desabilitar a opção **Retornar matriz**.
      * **Argumentos**: selecione o argumento denominado **ID**.

      Selecione **[!UICONTROL Concluído]**. O serviço para recuperar os detalhes do cliente do banco de dados MySQL está configurado.

      ![recuperação-endereço-entrega](assets/shiiping-address-retrieval.png)

   1. Selecione o serviço **[!UICONTROL atualizar]** e selecione **[!UICONTROL Editar Propriedades]**. A caixa de diálogo de propriedades é aberta.

   1. Especifique o seguinte na caixa de diálogo [!UICONTROL Editar Propriedades]:

      * **Título**: especifique o título do serviço. Por exemplo, Atualizar endereço de entrega.
      * **Descrição**: especifique a descrição que contém o funcionamento detalhado do serviço. Por exemplo:

        Este serviço atualiza o endereço de entrega e campos relacionados no banco de dados MySQL

      * **Objeto de Modelo de Entrada**: Selecione um esquema contendo dados do cliente. Por exemplo:

        esquema customerdetail

      * **Tipo de saída**: selecione **BOOLEANO**.

      * **Argumentos**: selecione o nome do argumento **ID** e **customerdetails**.

      Selecione **[!UICONTROL Concluído]**. O serviço **[!UICONTROL update]** para atualizar os detalhes do cliente no banco de dados [!DNL MySQL] está configurado.

      ![atualização de endereço de envio](assets/shiiping-address-update.png)

O objeto de modelo de dados e os serviços no modelo de dados de formulário são configurados. Agora você pode testar o modelo de dados do formulário.

## Etapa 4: testar o modelo de dados do formulário {#test-fdm}

Você pode testar o objeto de modelo de dados e os serviços para verificar se o modelo de dados de formulário está configurado corretamente.

Faça o seguinte para executar o teste:

1. Vá para a guia **[!UICONTROL Modelo]**, selecione o objeto de modelo de dados **customerdetails** e selecione **[!UICONTROL Testar Objeto de Modelo]**.
1. Na janela [!UICONTROL Modelo/Serviço de Teste], selecione **[!UICONTROL Ler objeto de modelo]** no menu suspenso **[!UICONTROL Selecionar Modelo/Serviço]**.
1. Na seção **customerdetails**, especifique um valor para o argumento **id** que existe no banco de dados [!DNL MySQL] configurado e selecione **[!UICONTROL Test]**.

   Os detalhes do cliente associados à ID especificada são obtidos e exibidos na seção **[!UICONTROL Saída]**, conforme mostrado abaixo.

   ![teste-leitura-modelo](assets/test-read-model.png)

1. Da mesma forma, você pode testar o objeto e os serviços do modelo Gravar.

   No exemplo a seguir, o serviço de atualização atualiza com êxito os detalhes de endereço da id 7102715 no banco de dados.

   ![modelo-de-gravação-de-teste](assets/test-write-model.png)

   Agora, se você testar o serviço do modelo de leitura novamente para a id 7107215, ele buscará e exibirá os detalhes do cliente atualizados, como mostrado abaixo.

   ![lido-atualizado](assets/read-updated.png)


>[!NOTE]
>
> Você pode criar e usar a configuração da Lista do SharePoint usando o Modelo de dados de formulário em um Formulário adaptável para salvar dados ou o Documento de registro gerado em uma Lista do SharePoint. Consulte [Conectar um formulário adaptável à Lista do Microsoft® SharePoint](/help/forms/using/configuring-submit-actions.md#create-a-sharepoint-list-configuration) para ver as etapas detalhadas.