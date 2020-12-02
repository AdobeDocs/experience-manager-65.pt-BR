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
source-git-commit: 78768e6eab65f452421d8809384500c6eab6b97f
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 1%

---


# Tutorial: Criar modelo de dados de formulário {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Este tutorial é uma etapa da série [Criar seu primeiro formulário adaptável](../../forms/using/create-your-first-adaptive-form.md). É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso do tutorial completo.

## Sobre o tutorial {#about-the-tutorial}

AEM módulo de integração de dados [!DNL Forms] permite criar um modelo de dados de formulário a partir de diferentes fontes de dados de backend, como AEM perfil do usuário, serviços Web RESTful, serviços Web baseados em SOAP, serviços OData e bancos de dados relacionais. É possível configurar objetos e serviços de modelo de dados em um modelo de dados de formulário e associá-lo a um formulário adaptável. Campos de formulário adaptáveis são vinculados às propriedades de objetos de modelo de dados. Os serviços permitem que você preencha previamente o formulário adaptável e grave os dados de formulário enviados de volta para o objeto de modelo de dados.

Para obter mais informações sobre a integração de dados de formulário e o modelo de dados de formulário, consulte [Integração de dados da AEM Forms](../../forms/using/data-integration.md).

Este tutorial o orienta pelas etapas para preparar, criar, configurar e associar um modelo de dados de formulário a um formulário adaptável. No final deste tutorial, você poderá:

* [Configurar o banco de dados MySQL como fonte de dados](#config-database)
* [Criar modelo de dados de formulário usando o banco de dados MySQL](#create-fdm)
* [Configurar modelo de dados de formulário](#config-fdm)
* [Modelo de dados do formulário de ensaio](#test-fdm)

O modelo de dados de formulário será semelhante ao seguinte:

![form-data-model_l](assets/form-data-model_l.png)

**A.** Fontes de dados configuradas  **B.schemas** de fonte de dados  **C.** Serviços disponíveis  **D.** Objetos de modelo de dados  **E.** Serviços configurados

## Pré-requisitos {#prerequisites}

Antes de começar, verifique se você tem o seguinte:

* [!DNL MySQL] banco de dados com dados de amostra conforme declarado na seção Pré-requisitos de  [Criar seu primeiro formulário adaptável](../../forms/using/create-your-first-adaptive-form.md)
* Pacote OSGi para [!DNL MySQL] driver JDBC, conforme explicado em [Fazendo o Bundling do Driver de Banco de Dados JDBC](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* Formulário adaptável, conforme explicado no primeiro tutorial [Criar um formulário adaptável](/help/forms/using/create-adaptive-form.md)

## Etapa 1: Configurar o banco de dados MySQL como fonte de dados {#config-database}

Você pode configurar diferentes tipos de fontes de dados para criar um modelo de dados de formulário. Para este tutorial, configuraremos o banco de dados MySQL que você configurou e preencheu com dados de amostra. Para obter informações sobre outras fontes de dados compatíveis e como configurá-las, consulte [Integração de dados da AEM Forms](../../forms/using/data-integration.md).

Faça o seguinte para configurar seu banco de dados [!DNL MySQL]:

1. Instale o driver JDBC para o banco de dados [!DNL MySQL] como um pacote OSGi:

   1. Faça logon em AEM [!DNL Forms] Instância do autor como administrador e vá para AEM pacotes do console da Web. O URL padrão é [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Toque em **[!UICONTROL Instalar/Atualizar]**. Uma caixa de diálogo [!UICONTROL Carregar / Instalar Pacotes] é exibida.

   1. Toque em **[!UICONTROL Escolha Arquivo]** para navegar e selecionar o pacote OSGi do driver JDBC [!DNL MySQL]. Selecione **[!UICONTROL Pacote de Start]** e **[!UICONTROL Atualizar Pacotes]** e toque em **[!UICONTROL Instalar ou Atualizar]**. Verifique se o [!DNL Oracle Corporation's] Driver JDBC para [!DNL MySQL] está ativo. O driver está instalado.

1. Configure o banco de dados [!DNL MySQL] como uma fonte de dados:

   1. Vá para AEM console da Web em [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Localize a configuração **Apache Sling Connection Pooling DataSource**. Toque em para abrir a configuração no modo de edição.
   1. Na caixa de diálogo de configuração, especifique os seguintes detalhes:

      * **Nome da fonte de dados:** você pode especificar qualquer nome. Por exemplo, especifique **WeRetailMySQL**.
      * **Nome** da propriedade do serviço DataSource: Especifique o nome da propriedade de serviço que contém o nome DataSource. É especificado ao registrar a instância da fonte de dados como serviço OSGi. Por exemplo, **datasource.name**.
      * **Classe** de driver JDBC: Especifique o nome da classe Java do driver JDBC. Para o banco de dados [!DNL MySQL], especifique **com.mysql.jdbc.Driver**.
      * **URI** de conexão JDBC: Especifique o URL de conexão do banco de dados. Para banco de dados [!DNL MySQL] em execução na porta 3306 e schema, o URL é: `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **Nome de usuário:** Nome de usuário do banco de dados. É necessário ativar o driver JDBC para estabelecer uma conexão com o banco de dados.
      * **Senha:** Senha do banco de dados. É necessário ativar o driver JDBC para estabelecer uma conexão com o banco de dados.
      * **Teste em linha de crédito:** ative o  **[!UICONTROL teste em]** linha de crédito.
      * **Teste na devolução:** ative o  **[!UICONTROL teste na]** devolução.
      * **Query de validação:** especifique um query SQL SELECT para validar conexões do pool. O query deve retornar pelo menos uma linha. Por exemplo, **selecione * de customerdetails**.
      * **Isolamento** da transação: Defina o valor como  **READ_COMPROMISTED**.

         Deixe outras propriedades com os [valores](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) padrão e toque em **[!UICONTROL Salvar]**.

         É criada uma configuração semelhante à seguinte.

         ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## Etapa 2: Criar modelo de dados de formulário {#create-fdm}

AEM [!DNL Forms] fornece uma interface de usuário intuitiva para [criar um modelo de dados de formulário](data-integration.md) a partir de fontes de dados configuradas. É possível usar várias fontes de dados em um modelo de dados de formulário. Em nosso caso de uso, usaremos a fonte de dados [!DNL MySQL] configurada.

Faça o seguinte para criar um modelo de dados de formulário:

1. Em AEM instância do autor, navegue até **[!UICONTROL Forms]** > **[!UICONTROL Integrações de dados]**.
1. Toque em **[!UICONTROL Criar]** > **[!UICONTROL Modelo de Dados de Formulário]**.
1. Na caixa de diálogo Criar modelo de dados de formulário, especifique um **nome** para o modelo de dados de formulário. Por exemplo, **detalhes de faturamento de entrega do cliente**. Toque em **[!UICONTROL Next]**.
1. A tela da fonte de dados selecionada lista todas as fontes de dados configuradas. Selecione **Origem de dados WeRetailMySQL** e toque em **[!UICONTROL Criar]**.

   ![seleção da fonte de dados](assets/data-source-selection.png)

O modelo de dados do formulário **customer-Shipping-billing-details** é criado.

## Etapa 3: Configurar o modelo de dados de formulário {#config-fdm}

A configuração do modelo de dados de formulário envolve:

* adição de objetos e serviços de modelo de dados
* configuração de serviços de leitura e gravação para objetos de modelo de dados

Faça o seguinte para configurar o modelo de dados de formulário:

1. Em AEM instância do autor, navegue até **[!UICONTROL Forms]** > **[!UICONTROL Integrações de dados]**. O URL padrão é [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. O modelo de dados do formulário **customer-Shipping-billing-details** criado anteriormente está listado aqui. Abra-o no modo de edição.

   A fonte de dados selecionada **WeRetailMySQL** está configurada no modelo de dados de formulário.

   ![default-fdm](assets/default-fdm.png)

1. Expanda a árvore da fonte de dados WeRailMySQL. Selecione os seguintes objetos e serviços de modelo de dados do schema **weretail** > **customerdetails** para formar o modelo de dados:

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

   Toque em **Adicionar selecionados** para adicionar objetos e serviços de modelo de dados selecionados ao modelo de dados de formulário.

   ![Schema WeRetail](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >Os serviços padrão get, update e insert para fontes de dados JDBC são fornecidos prontamente com o modelo de dados de formulário.

1. Configure os serviços de leitura e gravação para o objeto de modelo de dados.

   1. Selecione o objeto de modelo de dados **customerdetails** e toque em **[!UICONTROL Editar propriedades]**.
   1. Selecione **[!UICONTROL get]** no menu suspenso Serviço de leitura. O argumento **id**, que é a chave primária no objeto de modelo de dados de detalhes do cliente, é adicionado automaticamente. Toque em ![aem_6_3_edit](assets/aem_6_3_edit.png) e configure o argumento da seguinte maneira.

      ![read-default](assets/read-default.png)

   1. Da mesma forma, selecione **[!UICONTROL update]** como Serviço de Gravação. O objeto **customerdetails** é adicionado automaticamente como argumento. O argumento é configurado da seguinte maneira.

      ![write-default](assets/write-default.png)

      Adicione e configure o argumento **id** como segue.

      ![id-arg](assets/id-arg.png)

   1. Toque em **[!UICONTROL Done]** para salvar as propriedades do objeto de modelo de dados. Em seguida, toque em **[!UICONTROL Salvar]** para salvar o modelo de dados do formulário.

      Os serviços **[!UICONTROL get]** e **[!UICONTROL update]** são adicionados como serviços padrão para o objeto de modelo de dados.

      ![data-model-object](assets/data-model-object.png)

1. Vá para a guia **[!UICONTROL Serviços]** e configure os serviços **[!UICONTROL get]** e **[!UICONTROL update]**.

   1. Selecione o serviço **[!UICONTROL get]** e toque em **[!UICONTROL Editar propriedades]**. A caixa de diálogo de propriedades é aberta.
   1. Especifique o seguinte na caixa de diálogo Editar propriedades:

      * **Título**: Especifique o título do serviço. Por exemplo: Recuperar Endereço de Entrega.
      * **Descrição**: Especifique a descrição que contém o funcionamento detalhado do serviço. Por exemplo:

         Este serviço recupera o endereço de entrega e outros detalhes do cliente do banco de dados [!DNL MySQL]

      * **Objeto** do Modelo de Saída: Selecione o schema que contém os dados do cliente. Por exemplo:

         schema customerdetail

      * **Matriz** de retorno: Desative a opção  **Retornar** matriz.
      * **Argumentos**: Selecione o argumento com o nome  **ID**.

      Toque em **[!UICONTROL Concluído]**. O serviço para recuperar detalhes do cliente do banco de dados MySQL está configurado.

      ![shiiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. Selecione o serviço **[!UICONTROL update]** e toque em **[!UICONTROL Editar propriedades]**. A caixa de diálogo de propriedades é aberta.

   1. Especifique o seguinte na caixa de diálogo [!UICONTROL Editar propriedades]:

      * **Título**: Especifique o título do serviço. Por exemplo, Atualizar Endereço de Entrega.
      * **Descrição**: Especifique a descrição que contém o funcionamento detalhado do serviço. Por exemplo:

         Este serviço atualiza o endereço de envio e os campos relacionados no banco de dados MySQL

      * **Objeto** do Modelo de Entrada: Selecione o schema que contém os dados do cliente. Por exemplo:

         schema customerdetail

      * **Tipo** de saída: Selecione  **BOOLEAN**.

      * **Argumentos**: Selecione o argumento chamado  **** IDs e detalhes  **do cliente**.
      Toque em **[!UICONTROL Concluído]**. O serviço **[!UICONTROL update]** para atualizar os detalhes do cliente no banco de dados [!DNL MySQL] está configurado.

      ![shiiping-address-update](assets/shiiping-address-update.png)



O objeto e os serviços do modelo de dados no modelo de dados de formulário são configurados. Agora é possível testar o modelo de dados de formulário.

## Etapa 4: Testar modelo de dados de formulário {#test-fdm}

Você pode testar o objeto e os serviços do modelo de dados para verificar se o modelo de dados do formulário está configurado corretamente.

Execute o teste a seguir:

1. Vá para a guia **[!UICONTROL Modelo]**, selecione o objeto de modelo de dados **customerdetails** e toque em **[!UICONTROL Testar objeto de modelo]**.
1. Na janela [!UICONTROL Modelo de Teste/Serviço], selecione **[!UICONTROL Ler objeto de modelo]** no menu suspenso **[!UICONTROL Selecionar Modelo/Serviço]**.
1. Na seção **customerdetails**, especifique um valor para o argumento **id** que existe no banco de dados [!DNL MySQL] configurado e toque em **[!UICONTROL Test]**.

   Os detalhes do cliente associados à ID especificada são buscados e exibidos na seção **[!UICONTROL Output]**, como mostrado abaixo.

   ![test-read-model](assets/test-read-model.png)

1. Da mesma forma, é possível testar o objeto e os serviços do modelo Gravar.

   No exemplo a seguir, o serviço de atualização atualiza com êxito os detalhes do endereço do id 7102715 no banco de dados.

   ![test-write-model](assets/test-write-model.png)

   Agora, se você testar o serviço de modelo de leitura novamente para o id 7107215, ele buscará e exibirá os detalhes atualizados do cliente, conforme mostrado abaixo.

   ![atualizado por leitura](assets/read-updated.png)
