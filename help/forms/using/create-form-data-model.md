---
title: '"Tutorial: Criar modelo de dados de formulário "'
seo-title: Tutorial Criar modelo de dados de formulário
description: Criar modelo de dados de formulário
seo-description: Criar modelo de dados de formulário
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# Tutorial: Create form data model {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

This tutorial is a step in the [Create Your First Adaptive Form](../../forms/using/create-your-first-adaptive-form.md) series. É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso do tutorial completo.

## About the tutorial {#about-the-tutorial}

AEM Forms data integration module allows you to create a form data model from disparate backend data sources such as AEM user profile, RESTful web services, SOAP-based web services, OData services, and relational databases. É possível configurar objetos e serviços de modelo de dados em um modelo de dados de formulário e associá-lo a um formulário adaptável. Adaptive form fields are bound to data model object properties. The services enable you to prefill the adaptive form and write submitted form data back to the data model object.

For more information about form data integration and form data model, see [AEM Forms Data Integration](../../forms/using/data-integration.md).

This tutorial walks you through the steps to prepare, create, configure, and associate a form data model with an adaptive form. At the end of this tutorial, you will be able to:

* [Configurar o banco de dados MySQL como fonte de dados](#config-database)
* [Create form data model using MySQL database](#create-fdm)
* [Configurar modelo de dados de formulário](#config-fdm)
* [Modelo de dados do formulário de ensaio](#test-fdm)

O modelo de dados de formulário será semelhante ao seguinte:

![form-data-model_l](assets/form-data-model_l.png)

**A.** Configured data sources **B.** Data source schemas **C.** Available services **D.** Data model objects **E.** Configured services

## Pré-requisitos {#prerequisites}

Before you begin, ensure that you have the following:

* Banco de dados MySQL com dados de amostra conforme declarado na seção Pré-requisitos de [Criar seu primeiro formulário adaptável](../../forms/using/create-your-first-adaptive-form.md)
* OSGi bundle for MySQL JDBC driver as explained in [Bundling the JDBC Database Driver](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* Formulário adaptável, conforme explicado no primeiro tutorial [Criar um formulário adaptável](/help/forms/using/create-adaptive-form.md)

## Etapa 1: Configurar o banco de dados MySQL como fonte de dados {#config-database}

Você pode configurar diferentes tipos de fontes de dados para criar um modelo de dados de formulário. Para este tutorial, configuraremos o banco de dados MySQL que você configurou e preencheu com dados de amostra. Para obter informações sobre outras fontes de dados compatíveis e como configurá-las, consulte Integração [de dados do](../../forms/using/data-integration.md)AEM Forms.

Faça o seguinte para configurar seu banco de dados MySQL:

1. Instale o driver JDBC para o banco de dados MySQL como um pacote OSGi:

   1. Faça logon na instância de autor do AEM Forms como administrador e vá para pacotes de console da Web do AEM. O URL padrão é [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Toque em **Instalar/atualizar**. Uma caixa de diálogo **Carregar / Instalar pacotes** é exibida.

   1. Toque em **Escolher arquivo** para navegar e selecionar o pacote OSGi do driver JDBC do MySQL. Selecione Pacote **de** Start e **Atualize pacotes** e toque em **Instalar ou atualizar**. Certifique-se de que o Driver JDBC da Oracle Corporation para MySQL esteja ativo. O driver está instalado.

1. Configure o banco de dados MySQL como uma fonte de dados:

   1. Vá para o console da Web do AEM em [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Localize a configuração **Apache Sling Connection Pooling DataSource** . Toque em para abrir a configuração no modo de edição.
   1. Na caixa de diálogo de configuração, especifique os seguintes detalhes:

      * **Nome da fonte de dados:** Você pode especificar qualquer nome. Por exemplo, especifique **WeRetailMySQL**.
      * **DataSource service property name**: Specify name of the service property containing the DataSource name. It is specified while registering the data source instance as OSGi service. For example, **datasource.name**.
      * **JDBC driver class**: Specify Java class name of the JDBC driver. For MySQL database, specify **com.mysql.jdbc.Driver**.
      * **JDBC connection URI**: Specify connection URL of the database. For MySQL database running on port 3306 and schema weretail, the URL is: `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **Username:** Username of the database. It is required to enable JDBC driver to establish a connection with the database.
      * **Password:** Password of the database. It is required to enable JDBC driver to establish a connection with the database.
      * **Test on Borrow:** Enable the **Test on Borrow** option.
      * **Teste na devolução:** Ative a opção **Testar ao Retornar** .
      * **Validation Query:** Specify a SQL SELECT query to validate connections from the pool. The query must return at least one row. Por exemplo, **selecione * em detalhes** do cliente.
      * **Transaction Isolation**: Set the value to **READ_COMMITTED**.
      Leave other properties with default [values](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) and tap **Save**.
   A configuration similar to the following is created.

   ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## Step 2: Create form data model {#create-fdm}

AEM Forms provides an intuitive user interface to [create a form data model](data-integration.md) from configured data sources. You can use multiple data sources in a form data model. For our use case, we will use the configured MySQL data source.

Do the following to create form data model:

1. In AEM author instance, navigate to **Forms** > **Data Integrations**.
1. Tap **Create** > **Form Data Model**.
1. In the Create Form Data Model dialog, specify a **name** for the form data model. For example, **customer-shipping-billing-details**. Toque em **Avançar**.
1. The select datasource screen lists all configured data sources. Select **WeRetailMySQL** data source and tap **Create**.

   ![data-source-selection](assets/data-source-selection.png)

The **customer-shipping-billing-details** form data model is created.

## Step 3: Configure form data model {#config-fdm}

Configuring form data model involves:

* adding data model object and services
* configuring read and write services for data model objects

Do the following to configure the form data model:

1. On AEM author instance, navigate to **Forms** > **Data Integrations**. The default URL is [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. The **customer-shipping-billing-details** form data model you created earlier is listed here. Open it in edit mode.

   The selected data source **WeRetailMySQL** is configured in the form data model.

   ![default-fdm](assets/default-fdm.png)

1. Expand the WeRailMySQL data source tree. Select the following data model objects and services from **weretail** > **customerdetails** schema to form data model:

   * **Objetos** do modelo de dados:

      * id
      * name
      * ShippingAddress
      * cidade
      * estado
      * código postal
   * **Serviços:**

      * get
      * atualizar
   Tap **Add Selected** to add selected data model objects and services to the form data model.

   ![WeRetail Schema](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >The default get, update, and insert services for JDBC datasources are provided out-of-the-box with form data model .

1. Configure read and write services for the data model object.

   1. Select the **customerdetails** data model object and tap **Edit Properties**.
   1. Select **get** from the Read Service drop-down. The **id** argument, which is the primary key in the customerdetails data model object is added automatically. Tap ![aem_6_3_edit](assets/aem_6_3_edit.png) and configure the argument as follows.

      ![read-default](assets/read-default.png)

   1. Similarly, select **update** as the Write Service. The **customerdetails** object is added as an argument automatically. The argument is configured as follows.

      ![write-default](assets/write-default.png)

      Add and configure the **id** argument as follows.

      ![id-arg](assets/id-arg.png)

   1. Toque em **Concluído** para salvar as propriedades do objeto de modelo de dados. Em seguida, toque em **Salvar** para salvar o modelo de dados do formulário.

      Os serviços **get** e **update** são adicionados como serviços padrão para o objeto de modelo de dados.

      ![data-model-object](assets/data-model-object.png)

1. Vá para a guia **Serviços** e configure os serviços **get** e **update** .

   1. Selecione o serviço **get** e toque em **Editar propriedades**. A caixa de diálogo de propriedades é aberta.
   1. Specify the following in the Edit Properties dialog:

      * **Título**: Especifique o título do serviço. For example: Retrieve Shipping Address.
      * **Description**: Specify description containing detailed functioning of the service. Por exemplo:

         This service retrieves shipping address and other customer details from MySQL database

      * **Objeto** do Modelo de Saída: Selecione o schema que contém os dados do cliente. Por exemplo:

         customerdetail schema

      * **Return array**: Disable the **Return array** option.
      * **Arguments**: Select argument named **ID**.
      Toque em **Concluído**. Service to retrieve customer details from the MySQL database is configured.

      ![shiiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. Select the **update** service and tap **Edit Properties**. The properties dialog opens.

   1. Specify the following in the Edit Properties dialog:

      * **Title**: Specify title of the service. For example, Update Shipping Address.
      * **Description**: Specify description containing detailed functioning of the service. Por exemplo:

         This service updates shipping address and related fields in MySQL database

      * **Input Model Object**: Select schema containing customer data. Por exemplo:

         customerdetail schema

      * **Output type**: Select **BOOLEAN**.

      * **Arguments**: Select argument named **ID** and **customerdetails**.
      Toque em **Concluído**. The **update** service to update customer details in the MySQL database is configured.

      ![shiiping-address-update](assets/shiiping-address-update.png)



The data model object and services in the form data model are configured. You can now test the form data model.

## Step 4: Test form data model {#test-fdm}

You can test the data model object and services to verify that the form data model is configured properly.

Do the following to run the test:

1. Go to the **Model** tab, select the **customerdetails** data model object, and tap **Test Model Object**.
1. In the **Test Model/Service** window, select **Read model object** from the **Select Model/Service** drop-down.
1. In the **customerdetails** section, specify a value for the **id** argument that exists in the configured MySQL database and tap **Test**.

   The customer details associated with the specified id are fetched and displayed in the **Output** section as shown below.

   ![test-read-model](assets/test-read-model.png)

1. Da mesma forma, é possível testar o objeto e os serviços do modelo Gravar.

   No exemplo a seguir, o serviço de atualização atualiza com êxito os detalhes do endereço do id 7102715 no banco de dados.

   ![test-write-model](assets/test-write-model.png)

   Now, if you test the read model service again for the id 7107215, it will fetch and display the updated customer details as shown below.

   ![read-updated](assets/read-updated.png)
