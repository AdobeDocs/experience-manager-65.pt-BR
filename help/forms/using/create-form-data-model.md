---
title: "Tutorial: Criar modelo de dados de formulário"
seo-title: Create Form Data Model Tutorial
description: Criar modelo de dados de formulário
seo-description: Create form data model
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1511'
ht-degree: 1%

---

# Tutorial: Criar modelo de dados do formulário {#tutorial-create-form-data-model}

![04-criar-formulário-modelo-dados-principal](assets/04-create-form-data-model-main.png)

Este tutorial é uma etapa da [Criar O Primeiro Formulário Adaptável](../../forms/using/create-your-first-adaptive-form.md) série. É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso completo do tutorial.

## Sobre o tutorial {#about-the-tutorial}

AEM [!DNL Forms] o módulo de integração de dados permite criar um modelo de dados de formulário a partir de diferentes fontes de dados de back-end, como perfil de usuário AEM, serviços Web RESTful, serviços Web baseados em SOAP, serviços OData e bancos de dados relacionais. Você pode configurar serviços e objetos de modelo de dados em um modelo de dados de formulário e associá-lo a um formulário adaptável. Os campos de formulário adaptável são vinculados às propriedades do objeto de modelo de dados. Os serviços permitem preencher previamente o formulário adaptável e gravar dados do formulário enviado de volta no objeto de modelo de dados.

Para obter mais informações sobre a integração de dados de formulário e o modelo de dados de formulário, consulte [Integração de dados do AEM Forms](../../forms/using/data-integration.md).

Este tutorial percorre as etapas para preparar, criar, configurar e associar um modelo de dados de formulário a um formulário adaptável. Ao final deste tutorial, você será capaz de:

* [Configurar o banco de dados MySQL como fonte de dados](#config-database)
* [Criar modelo de dados de formulário usando o banco de dados MySQL](#create-fdm)
* [Configurar modelo de dados do formulário](#config-fdm)
* [Testar modelo de dados do formulário](#test-fdm)

O modelo de dados de formulário será semelhante ao seguinte:

![form-data-model_l](assets/form-data-model_l.png)

**A.** Fontes de dados configuradas **B.** Esquemas de fonte de dados **C** Serviços disponíveis **D.** Objetos do modelo de dados **E** Serviços configurados

## Pré-requisitos {#prerequisites}

Antes de começar, verifique se você tem o seguinte:

* [!DNL MySQL] banco de dados com dados de amostra, conforme declarado na seção Pré-requisitos de [Criar o primeiro formulário adaptável](../../forms/using/create-your-first-adaptive-form.md)
* Pacote OSGi para [!DNL MySQL] Driver JDBC conforme explicado em [Agrupando o driver do banco de dados JDBC](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* Formulário adaptável conforme explicado no primeiro tutorial [Criar um formulário adaptável](/help/forms/using/create-adaptive-form.md)

## Etapa 1: configurar o banco de dados MySQL como fonte de dados {#config-database}

É possível configurar diferentes tipos de fontes de dados para criar um modelo de dados de formulário. Para este tutorial, configuraremos o banco de dados MySQL que você configurou e preencheu com dados de amostra. Para obter informações sobre outras fontes de dados compatíveis e como configurá-las, consulte [Integração de dados do AEM Forms](../../forms/using/data-integration.md).

Faça o seguinte para configurar suas [!DNL MySQL] banco de dados:

1. Instale o driver JDBC para [!DNL MySQL] o banco de dados como uma pacote OSGi:

   1. Baixe [!DNL MySQL] o pacote JDBC Driver OSGi de `http://www.java2s.com/ref/jar/download-orgosgiservicejdbc100jar-file.html` . <!-- This URL is an insecure link but using https is not possible -->
   1. Fazer logon no AEM [!DNL Forms] Instância do autor como administrador e acesse pacotes de console da Web AEM. O URL padrão é [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Toque **[!UICONTROL Instalar/Atualizar]**. Um [!UICONTROL Carregar/instalar pacotes] será exibida.

   1. Toque **[!UICONTROL Escolher arquivo]** para procurar e selecionar a variável [!DNL MySQL] Pacote OSGi do driver JDBC. Selecionar **[!UICONTROL Iniciar pacote]** e **[!UICONTROL Atualizar pacotes]** e toque em **[!UICONTROL Instalar ou atualizar]**. Certifique-se de que o [!DNL Oracle Corporation's] Driver JDBC para [!DNL MySQL] está ativo. O driver está instalado.

1. Configure [!DNL MySQL] o banco de dados como um fonte de dados:

   1. Vá para AEM console da Web em [ https://localhost:4502/System/console/configMgr ](https://localhost:4502/system/console/configMgr) .
   1. Localize **a configuração da fonte** de dados Pooled do Apache sling Connection. Toque para abrir a configuração no modo de edição.
   1. Na caixa de diálogo de configuração, especifique os seguintes detalhes:

      * **Nome da fonte de dados:** Você pode especificar qualquer nome. Por exemplo, especifique **WeRetailMySQL**.
      * **Nome da propriedade do serviço DataSource**: especifique o nome da propriedade de serviço que contém o nome da DataSource. É especificado ao registrar a instância da fonte de dados como serviço OSGi. Por exemplo, **datasource.name**.
      * **Classe de driver JDBC**: Especifique o nome da classe Java do driver JDBC. Para [!DNL MySQL] banco de dados, especificar **com.mysql.jdbc.Driver**.
      * **URI** de conexão JDBC: especifique URL de conexão do banco de dados. Para o banco de [!DNL MySQL] dados em execução no porta 3306 e Schema weretail, o URL é: `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`

      >[!NOTE]
      >
      > Quando o banco de dados está atrás de um firewall, o nome do host do banco de [!DNL MySQL] dados não é um DNS público. O endereço IP do banco de dados precisa ser adicionado no *arquivo/etc/hosts* da máquina host do AEM.

      * **Nome de usuário:** Nome de usuário do banco de dados. É necessário habilitar o driver JDBC para estabelecer uma conexão com o banco de dados.
      * **Senha:** Senha do banco de dados. É necessário habilitar o driver JDBC para estabelecer uma conexão com o banco de dados.

      >[!NOTE]
      >
      >O AEM Forms não oferece suporte à autenticação NT para [!DNL MySQL]. Vá para AEM console da Web em [ https://localhost:4502/System/console/configMgr ](https://localhost:4502/system/console/configMgr) e pesquisa &quot;fonte de dados em pool de conexões do Apache sling&quot;. Para &quot;URI de conexão JDBC&quot; propriedade valor definido como &quot;integratedSecurity&quot; como false e use o nome de usuário e o senha para se conectar ao [!DNL MySQL] banco de dados.

      * **Teste no empréstimo:** ative a **[!UICONTROL opção testar no empréstimo]** .
      * **Teste no Return:** ative a **[!UICONTROL opção testar ao retornar]** .
      * **Consulta de validação:** especifique um SQL SELECT Query para validar as conexões do pool. A consulta deve retornar pelo menos uma linha. Por exemplo, **selecionar &#42; dos detalhes do cliente**.
      * **Isolamento de transação**: Defina o valor como **READ_COMMITTED**.

        Deixar outras propriedades com o padrão [valores](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) e toque em **[!UICONTROL Salvar]**.

        Uma configuração semelhante à seguinte é criada.

        ![relacional-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## Etapa 2: Criar modelo de dados de formulário {#create-fdm}

AEM [!DNL Forms] O oferece uma interface intuitiva para [criar um modelo de dados de formulário](data-integration.md) de fontes de dados configuradas. É possível usar várias fontes de dados em um modelo de dados de formulário. No nosso caso de uso, usaremos o configurado [!DNL MySQL] fonte de dados.

Faça o seguinte para criar o modelo de dados de formulário:

1. Na instância do autor AEM, navegue até **[!UICONTROL Forms]** > **[!UICONTROL Integrações de dados]**.
1. Toque **[!UICONTROL Criar]** > **[!UICONTROL Modelo de dados do formulário]**.
1. Na caixa de diálogo Criar modelo de dados de formulário, especifique uma **name** para o modelo de dados do formulário. Por exemplo, **customer-shipping-billing-details**. Toque **[!UICONTROL Próxima]**.
1. A tela selecionar fonte de dados lista todas as fontes de dados configuradas. Selecionar **WeRetailMySQL** fonte de dados e toque em **[!UICONTROL Criar]**.

   ![data-source-selection](assets/data-source-selection.png)

A variável **customer-shipping-billing-details** modelo de dados de formulário é criado.

## Etapa 3: configurar o modelo de dados de formulário {#config-fdm}

A configuração do modelo de dados de formulário envolve:

* adição de objetos e serviços de modelo de dados
* configuração de serviços de leitura e gravação para objetos de modelo de dados

Faça o seguinte para configurar o modelo de dados de formulário:

1. Na instância do autor AEM, navegue até **[!UICONTROL Forms]** > **[!UICONTROL Integrações de dados]**. O URL padrão é [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. A variável **customer-shipping-billing-details** o modelo de dados de formulário criado anteriormente está listado aqui. Abra-o no modo de edição.

   A fonte de dados selecionada **WeRetailMySQL** está configurado no modelo de dados de formulário.

   ![default-fdm](assets/default-fdm.png)

1. Expanda a árvore da fonte de dados WeRailMySQL. Selecione os seguintes serviços e objetos de modelo de dados em **weretail** > **customerdetails** esquema para formar o modelo de dados:

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

   Toque **Adicionar selecionado** para adicionar objetos de modelo de dados e serviços selecionados ao modelo de dados de formulário.

   ![Esquema do WeRetail](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >Os serviços padrão de obtenção, atualização e inserção para fontes de dados JDBC são fornecidos com o modelo de dados de formulário pronto para uso.

1. Configure serviços de leitura e gravação para o objeto de modelo de dados.

   1. Selecione o **customerdetails** objeto de modelo de dados e toque em **[!UICONTROL Editar propriedades]**.
   1. Selecionar **[!UICONTROL obter]** no menu suspenso Serviço de leitura. A variável **id** O argumento, que é a chave primária no objeto de modelo de dados customerdetails, é adicionado automaticamente. Toque ![aem_6_3_edit](assets/aem_6_3_edit.png) e configure o argumento da seguinte maneira.

      ![read-default](assets/read-default.png)

   1. Da mesma forma, selecione **[!UICONTROL atualizar]** como o Serviço de gravação. A variável **customerdetails** objeto é adicionado automaticamente como argumento. O argumento é configurado da seguinte maneira.

      ![write-default](assets/write-default.png)

      Adicione e configure o argumento ID **da** seguinte maneira.

      ![ID-ARG](assets/id-arg.png)

   1. Toque em **[!UICONTROL concluído]** para salvar as propriedades do objeto de modelo de dados. Em seguida, toque **[!UICONTROL em salvar]** para salvar o modelo de dados de formulário.

      Os **[!UICONTROL serviços get]** e **[!UICONTROL Update]** são adicionados como serviços padrão para o objeto de modelo de dados.

      ![modelo de dados-objeto](assets/data-model-object.png)

1. Vá para a **[!UICONTROL Serviços]** guia e configurar **[!UICONTROL obter]** e **[!UICONTROL atualizar]** serviços.

   1. Selecione o **[!UICONTROL serviço get]** e toque **[!UICONTROL Editar propriedades]** . A caixa de diálogo de propriedades é aberta.
   1. Especifique o seguinte na caixa de diálogo Editar Propriedades:

      * **Título** : especificar o título do serviço. Por exemplo: recuperar endereço de envio.
      * **Descrição** : Especifique a descrição que contém o funcionamento detalhado do serviço. Por exemplo:

        Este serviço recupera o endereço de entrega e outros detalhes do cliente de [!DNL MySQL] banco de dados

      * **Objeto de modelo de saída**: Selecione o schema que contém dados do cliente. Por exemplo:

        esquema customerdetail

      * **Retornar matriz**: Desative a variável **Retornar matriz** opção.
      * **Argumentos**: selecione o argumento chamado **ID**.

      Toque **[!UICONTROL Concluído]**. O serviço para recuperar os detalhes do cliente do banco de dados MySQL está configurado.

      ![delivery-address-retrieval](assets/shiiping-address-retrieval.png)

   1. Selecione o **[!UICONTROL atualizar]** serviço e toque em **[!UICONTROL Editar propriedades]**. A caixa de diálogo de propriedades é aberta.

   1. Especifique o seguinte no [!UICONTROL Editar propriedades] diálogo:

      * **Título**: especifique o título do serviço. Por exemplo, Atualizar endereço de entrega.
      * **Descrição**: especifique a descrição que contém o funcionamento detalhado do serviço. Por exemplo:

        Este serviço atualiza o endereço de entrega e campos relacionados no banco de dados MySQL

      * **Objeto de modelo de entrada**: Selecione o schema que contém dados do cliente. Por exemplo:

        esquema customerdetail

      * **Tipo de saída**: Selecionar **BOOLEANO**.

      * **Argumentos**: selecione o argumento chamado **ID** e **customerdetails**.

      Toque **[!UICONTROL Concluído]**. A variável **[!UICONTROL atualizar]** serviço para atualizar os detalhes do cliente na [!DNL MySQL] banco de dados está configurado.

      ![shiping-address-update](assets/shiiping-address-update.png)

O objeto de modelo de dados e os serviços no modelo de dados de formulário são configurados. Agora você pode testar o modelo de dados do formulário.

## Etapa 4: testar o modelo de dados do formulário {#test-fdm}

Você pode testar o objeto de modelo de dados e os serviços para verificar se o modelo de dados de formulário está configurado corretamente.

Faça o seguinte para executar o teste:

1. Vá para a **[!UICONTROL Modelo]** , selecione a **customerdetails** modelo de dados e toque em **[!UICONTROL Testar objeto de modelo]**.
1. No [!UICONTROL Modelo de teste/serviço] selecione **[!UICONTROL Ler objeto de modelo]** do **[!UICONTROL Selecionar modelo/serviço]** menu suspenso.
1. No **customerdetails** especifique um valor para a variável **id** argumento que existe na variável [!DNL MySQL] banco de dados e toque **[!UICONTROL Teste]**.

   Os detalhes do cliente associados à ID especificada são obtidos e exibidos no **[!UICONTROL Output]** conforme mostrado abaixo.

   ![test-read-model](assets/test-read-model.png)

1. Da mesma forma, você pode testar o objeto e os serviços do modelo Gravar.

   No exemplo a seguir, o serviço de atualização atualiza com êxito os detalhes de endereço da id 7102715 no banco de dados.

   ![test-write-model](assets/test-write-model.png)

   Agora, se você testar o serviço do modelo de leitura novamente para a id 7107215, ele buscará e exibirá os detalhes do cliente atualizados, como mostrado abaixo.

   ![atualizado para leitura](assets/read-updated.png)
