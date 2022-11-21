---
title: "Tutorial: Criar modelo de dados de formulário "
seo-title: Create Form Data Model Tutorial
description: Criar modelo de dados de formulário
seo-description: Create form data model
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
source-git-commit: c3178eefb5aca3afea2f3df8381b52461247d6f3
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 1%

---

# Tutorial: Criar modelo de dados de formulário {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Este tutorial é uma etapa do [Criar seu primeiro formulário adaptável](../../forms/using/create-your-first-adaptive-form.md) série. É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso tutorial completo.

## Sobre o tutorial {#about-the-tutorial}

AEM [!DNL Forms] o módulo de integração de dados permite criar um modelo de dados de formulário a partir de diferentes fontes de dados de backend, como AEM perfil de usuário, serviços Web RESTful, serviços Web baseados em SOAP, serviços OData e bancos de dados relacionais. É possível configurar objetos e serviços do modelo de dados em um modelo de dados de formulário e associá-lo a um formulário adaptável. Os campos de formulário adaptável são vinculados às propriedades de objetos do modelo de dados. Os serviços permitem preencher previamente o formulário adaptável e gravar os dados de formulário enviados de volta no objeto de modelo de dados.

Para obter mais informações sobre a integração de dados de formulário e o modelo de dados de formulário, consulte [Integração de dados do AEM Forms](../../forms/using/data-integration.md).

Este tutorial o orienta pelas etapas para preparar, criar, configurar e associar um modelo de dados de formulário a um formulário adaptável. Ao final deste tutorial, você poderá:

* [Configurar o banco de dados MySQL como fonte de dados](#config-database)
* [Criar modelo de dados de formulário usando o banco de dados MySQL](#create-fdm)
* [Configurar o modelo de dados de formulário](#config-fdm)
* [Modelo de dados do formulário de teste](#test-fdm)

O modelo de dados de formulário será semelhante ao seguinte:

![form-data-model_l](assets/form-data-model_l.png)

**A.** Fontes de dados configuradas **B.** Esquemas da fonte de dados **C.** Serviços disponíveis **D.** Objetos do modelo de dados **E.** Serviços configurados

## Pré-requisitos {#prerequisites}

Antes de começar, verifique se você tem o seguinte:

* [!DNL MySQL] banco de dados com dados de amostra conforme declarado na seção Pré-requisitos de [Criar o primeiro formulário adaptável](../../forms/using/create-your-first-adaptive-form.md)
* Pacote OSGi para [!DNL MySQL] Driver JDBC, conforme explicado em [Pacote do driver de banco de dados JDBC](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* Formulário adaptável, conforme explicado no primeiro tutorial [Criar um formulário adaptável](/help/forms/using/create-adaptive-form.md)

## Etapa 1: Configurar o banco de dados MySQL como fonte de dados {#config-database}

Você pode configurar diferentes tipos de fontes de dados para criar um modelo de dados de formulário. Para este tutorial, configuraremos o banco de dados MySQL que você configurou e preencheu com dados de amostra. Para obter informações sobre outras fontes de dados compatíveis e como configurá-las, consulte [Integração de dados do AEM Forms](../../forms/using/data-integration.md).

Faça o seguinte para configurar [!DNL MySQL] banco de dados:

1. Instale o driver JDBC para [!DNL MySQL] banco de dados como um pacote OSGi:

   1. Baixar [[!DNL MySQL] Pacote OSGi do driver JDBC](http://www.java2s.com/ref/jar/download-orgosgiservicejdbc100jar-file.html).
   1. Faça logon no AEM [!DNL Forms] Instância do autor como administrador e vá para AEM pacotes do console da Web. O URL padrão é [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Toque **[!UICONTROL Instalar/atualizar]**. Um [!UICONTROL Fazer upload / instalar pacotes] será exibida.

   1. Toque **[!UICONTROL Escolher arquivo]** para navegar e selecionar o [!DNL MySQL] Pacote OSGi do driver JDBC. Selecionar **[!UICONTROL Iniciar Pacote]** e **[!UICONTROL Atualizar pacotes]** e toque em **[!UICONTROL Instalar ou atualizar]**. Certifique-se de que [!DNL Oracle Corporation's] Driver JDBC para [!DNL MySQL] está ativo. O driver está instalado.

1. Configurar [!DNL MySQL] banco de dados como fonte de dados:

   1. Vá para AEM console da Web em [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Localizar **Fonte de dados agrupada da conexão Apache Sling** configuração. Toque em para abrir a configuração no modo de edição.
   1. Na caixa de diálogo de configuração, especifique os seguintes detalhes:

      * **Nome da fonte de dados:** Você pode especificar qualquer nome. Por exemplo, especifique **WeRetailMySQL**.
      * **Nome da propriedade do serviço DataSource**: Especifique o nome da propriedade de serviço que contém o nome DataSource. Ele é especificado ao registrar a instância da fonte de dados como serviço OSGi. Por exemplo, **datasource.name**.
      * **Classe de driver JDBC**: Especifique o nome da classe Java do driver JDBC. Para [!DNL MySQL] banco de dados, especifique **com.mysql.jdbc.Driver**.
      * **URI de conexão JDBC**: Especifique o URL de conexão do banco de dados. Para [!DNL MySQL] banco de dados em execução na porta 3306 e schema weretail, o URL é: `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`

      >[!NOTE]
      >
      > Quando a variável [!DNL MySQL] O banco de dados está por trás de um firewall, então o nome do host do banco de dados não é um DNS público. O endereço IP do banco de dados precisa ser adicionado no */etc/hosts* arquivo da máquina host AEM.

      * **Nome de usuário:** Nome de usuário do banco de dados. É necessário habilitar o driver JDBC para estabelecer uma conexão com o banco de dados.
      * **Senha:** Senha do banco de dados. É necessário habilitar o driver JDBC para estabelecer uma conexão com o banco de dados.

      >[!NOTE]
      >
      >A AEM Forms não suporta Autenticação NT para [!DNL MySQL]. Vá para AEM console da Web em [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) e pesquise &quot;Apache Sling Connection Pool Datasource&quot;. Para a propriedade &quot;JDBC connection URI&quot;, defina o valor de &quot;IntegratedSecurity&quot; como False e use o nome de usuário e a senha criados para conexão com [!DNL MySQL] banco de dados.

      * **Teste em linha de crédito:** Ative o **[!UICONTROL Teste em linha de crédito]** opção.
      * **Teste no retorno:** Ative o **[!UICONTROL Testar no retorno]** opção.
      * **Consulta de validação:** Especifique uma consulta SQL SELECT para validar conexões do pool. A consulta deve retornar pelo menos uma linha. Por exemplo, **select &#42; de detalhes do cliente**.
      * **Isolamento de transação**: Defina o valor como **READ_BUTED**.

         Deixe outras propriedades com o padrão [values](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) e tocar **[!UICONTROL Salvar]**.

         Uma configuração semelhante ao seguinte é criada.

         ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)



## Etapa 2: Criar modelo de dados de formulário {#create-fdm}

AEM [!DNL Forms] O oferece uma interface de usuário intuitiva para [criar um modelo de dados de formulário](data-integration.md) em fontes de dados configuradas. É possível usar várias fontes de dados em um modelo de dados de formulário. No nosso caso de uso, usaremos o [!DNL MySQL] fonte de dados.

Faça o seguinte para criar um modelo de dados de formulário:

1. Em AEM instância do autor, navegue até **[!UICONTROL Forms]** > **[!UICONTROL Integrações de dados]**.
1. Toque **[!UICONTROL Criar]** > **[!UICONTROL Modelo de dados do formulário]**.
1. Na caixa de diálogo Criar modelo de dados de formulário , especifique um **name** para o modelo de dados de formulário. Por exemplo, **detalhes de faturamento de entrega do cliente**. Toque **[!UICONTROL Próximo]**.
1. A tela selecionar fonte de dados lista todas as fontes de dados configuradas. Selecionar **WeRetailMySQL** fonte de dados e toque **[!UICONTROL Criar]**.

   ![seleção de fonte de dados](assets/data-source-selection.png)

O **detalhes de faturamento de entrega do cliente** o modelo de dados de formulário é criado.

## Etapa 3: Configurar o modelo de dados de formulário {#config-fdm}

A configuração do modelo de dados de formulário envolve:

* adição de objetos e serviços do modelo de dados
* configuração de serviços de leitura e gravação para objetos de modelo de dados

Faça o seguinte para configurar o modelo de dados de formulário:

1. Em AEM instância do autor, navegue até **[!UICONTROL Forms]** > **[!UICONTROL Integrações de dados]**. O URL padrão é [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. O **detalhes de faturamento de entrega do cliente** o modelo de dados de formulário criado anteriormente está listado aqui. Abra-o no modo de edição.

   A fonte de dados selecionada **WeRetailMySQL** é configurado no modelo de dados de formulário.

   ![default-fdm](assets/default-fdm.png)

1. Expanda a árvore da fonte de dados WeRailMySQL . Selecione os seguintes objetos e serviços do modelo de dados de **rede** > **detalhes do cliente** esquema para formulário de modelo de dados:

   * **Objetos do modelo de dados**:

      * id
      * name
      * ShippingAddress
      * cidade
      * estado
      * código postal
   * **Serviços:**

      * get
      * atualizar

   Toque **Adicionar Selecionado** para adicionar objetos e serviços de modelo de dados selecionados ao modelo de dados de formulário.

   ![Esquema WeRetail](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >Os serviços padrão de obter, atualizar e inserir para fontes de dados JDBC são fornecidos prontos para uso com o modelo de dados de formulário .

1. Configure os serviços de leitura e gravação para o objeto de modelo de dados.

   1. Selecione o **detalhes do cliente** objeto e toque do modelo de dados **[!UICONTROL Editar propriedades]**.
   1. Selecionar **[!UICONTROL get]** na lista suspensa Serviço de leitura . O **id** O argumento , que é a chave primária no objeto de modelo de dados de detalhes do cliente, é adicionado automaticamente. Toque ![aem_6_3_edit](assets/aem_6_3_edit.png) e configure o argumento da seguinte maneira.

      ![read-default](assets/read-default.png)

   1. Da mesma forma, selecione **[!UICONTROL atualizar]** como o Serviço de gravação. O **detalhes do cliente** é adicionado automaticamente como argumento. O argumento é configurado da seguinte maneira.

      ![write-default](assets/write-default.png)

      Adicione e configure o **id** como se segue.

      ![id-arg](assets/id-arg.png)

   1. Toque **[!UICONTROL Concluído]** para salvar as propriedades do objeto de modelo de dados. Em seguida, toque em **[!UICONTROL Salvar]** para salvar o modelo de dados de formulário.

      O **[!UICONTROL get]** e **[!UICONTROL atualizar]** são adicionados como serviços padrão para o objeto de modelo de dados.

      ![objeto de modelo de dados](assets/data-model-object.png)

1. Vá para o **[!UICONTROL Serviços]** guia e configure **[!UICONTROL get]** e **[!UICONTROL atualizar]** serviços.

   1. Selecione o **[!UICONTROL get]** serviço e toque **[!UICONTROL Editar propriedades]**. A caixa de diálogo de propriedades é aberta.
   1. Especifique o seguinte na caixa de diálogo Editar propriedades:

      * **Título**: Especifique o título do serviço. Por exemplo: Recuperar Endereço de Entrega.
      * **Descrição**: Especifique a descrição que contém o funcionamento detalhado do serviço. Por exemplo:

         Esse serviço recupera o endereço de entrega e outros detalhes do cliente de [!DNL MySQL] banco de dados

      * **Objeto do Modelo de Saída**: Selecione o schema que contém os dados do cliente. Por exemplo:

         esquema customerdetail

      * **Matriz de retorno**: Desative o **Matriz de retorno** opção.
      * **Argumentos**: Selecione o argumento com o nome **ID**.

      Toque **[!UICONTROL Concluído]**. O serviço para recuperar detalhes do cliente do banco de dados do MySQL está configurado.

      ![shiiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. Selecione o **[!UICONTROL atualizar]** serviço e toque **[!UICONTROL Editar propriedades]**. A caixa de diálogo de propriedades é aberta.

   1. Especifique o seguinte no [!UICONTROL Editar propriedades] caixa de diálogo:

      * **Título**: Especifique o título do serviço. Por exemplo, Atualizar Endereço de Entrega.
      * **Descrição**: Especifique a descrição que contém o funcionamento detalhado do serviço. Por exemplo:

         Este serviço atualiza o endereço de entrega e campos relacionados no banco de dados MySQL

      * **Objeto do Modelo de Entrada**: Selecione o schema que contém os dados do cliente. Por exemplo:

         esquema customerdetail

      * **Tipo de saída**: Selecionar **BOOLEANO**.

      * **Argumentos**: Selecione o argumento com o nome **ID** e **detalhes do cliente**.
      Toque **[!UICONTROL Concluído]**. O **[!UICONTROL atualizar]** para atualizar os detalhes do cliente na [!DNL MySQL] o banco de dados está configurado.

      ![shiiping-address-update](assets/shiiping-address-update.png)



O objeto e os serviços do modelo de dados no modelo de dados de formulário são configurados. Agora é possível testar o modelo de dados de formulário.

## Etapa 4: Modelo de dados do formulário de teste {#test-fdm}

É possível testar o objeto e os serviços do modelo de dados para verificar se o modelo de dados do formulário está configurado corretamente.

Faça o seguinte para executar o teste:

1. Vá para o **[!UICONTROL Modelo]** selecione a guia **detalhes do cliente** objeto de modelo de dados e toque em **[!UICONTROL Objeto de Modelo de Teste]**.
1. No [!UICONTROL Modelo/serviço de ensaio] janela , selecione **[!UICONTROL Ler objeto de modelo]** do **[!UICONTROL Selecionar Modelo/Serviço]** lista suspensa.
1. No **detalhes do cliente** especifique um valor para a seção **id** que existe no argumento configurado [!DNL MySQL] banco de dados e toque em **[!UICONTROL Teste]**.

   Os detalhes do cliente associados à id especificada são buscados e exibidos na variável **[!UICONTROL Saída]** conforme mostrado abaixo.

   ![modelo de leitura-teste](assets/test-read-model.png)

1. Da mesma forma, é possível testar o objeto e os serviços do modelo Gravar.

   No exemplo a seguir, o serviço de atualização atualiza com êxito os detalhes do endereço da id 7102715 no banco de dados.

   ![modelo de gravação de teste](assets/test-write-model.png)

   Agora, se você testar o serviço do modelo de leitura novamente para a id 7107215, ele buscará e exibirá os detalhes atualizados do cliente, conforme mostrado abaixo.

   ![atualizado em leitura](assets/read-updated.png)
