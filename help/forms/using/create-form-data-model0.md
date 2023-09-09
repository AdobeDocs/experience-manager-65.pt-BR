---
title: "Tutorial: Criar modelo de dados de formulário no AEM Forms"
description: Criar modelo de dados de formulário para Comunicação Interativa
uuid: b56d3dac-be54-4812-b958-38a085686218
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5413fb3-9d50-4f4f-9db8-7e53cd5145d5
docset: aem65
feature: Interactive Communication
exl-id: c8a6037c-46bd-4058-8314-61cb925ba5a8
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2737'
ht-degree: 0%

---

# Tutorial: criar modelo de dados do formulário no AEM Forms{#tutorial-create-form-data-model}

![04-criar-formulário-modelo-dados-principal](assets/04-create-form-data-model-main.png)

Este tutorial é uma etapa da [Criar a primeira comunicação interativa](/help/forms/using/create-your-first-interactive-communication.md) série. É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso completo do tutorial.

## Sobre o tutorial {#about-the-tutorial}

O módulo de integração de dados do AEM Forms permite criar um modelo de dados de formulário a partir de diferentes fontes de dados de back-end, como o perfil de usuário AEM, os serviços Web RESTful, os serviços Web baseados em SOAP, os serviços OData e os bancos de dados relacionais. Você pode configurar serviços e objetos de modelo de dados em um modelo de dados de formulário e associá-lo a um formulário adaptável. Os campos de formulário adaptável são vinculados às propriedades do objeto de modelo de dados. Os serviços permitem preencher previamente o formulário adaptável e gravar dados do formulário enviado de volta no objeto de modelo de dados.

Para obter mais informações sobre a integração de dados de formulário e o modelo de dados de formulário, consulte [Integração de dados do AEM Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html).

Este tutorial percorre as etapas para preparar, criar, configurar e associar um modelo de dados de formulário a uma comunicação interativa. Ao final deste tutorial, você será capaz de:

* [Configurar o banco de dados](../../forms/using/create-form-data-model0.md#step-set-up-the-database)
* [Configurar o banco de dados MySQL como fonte de dados](../../forms/using/create-form-data-model0.md#step-configure-mysql-database-as-data-source)
* [Criar modelo de dados de formulário](../../forms/using/create-form-data-model0.md#step-create-form-data-model)
* [Configurar modelo de dados do formulário](../../forms/using/create-form-data-model0.md#step-configure-form-data-model)
* [Testar modelo de dados do formulário](../../forms/using/create-form-data-model0.md#step-test-form-data-model-and-services)

O modelo de dados de formulário é semelhante ao seguinte:

![Modelo de dados do formulário](assets/form_data_model_callouts_new.png)

**A.** Fontes de dados configuradas **B.** Esquemas de fonte de dados **C** Serviços disponíveis **D.** Objetos do modelo de dados **E** Serviços configurados

## Pré-requisitos {#prerequisites}

Antes de começar, verifique se você tem o seguinte:

* Banco de dados MySQL com dados de amostra conforme declarado na [Configurar o banco de dados](../../forms/using/create-form-data-model0.md#step-set-up-the-database) seção.
* Pacote OSGi para o driver JDBC MySQL, conforme explicado em [Agrupando o driver do banco de dados JDBC](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/jdbc.html#bundling-the-jdbc-database-driver)

## Etapa 1: configurar o banco de dados {#step-set-up-the-database}

Um banco de dados é essencial para criar uma comunicação interativa. Este tutorial usa um banco de dados para exibir o Modelo de dados de formulário e os recursos de persistência das Comunicações interativas. Configurar um banco de dados contendo tabelas de clientes, faturamentos e chamadas.
A imagem a seguir ilustra dados de exemplo para a tabela do cliente:

![sample_data_cust](assets/sample_data_cust.png)

Use a seguinte instrução DDL para criar a **cliente** tabela no banco de dados.

```sql
CREATE TABLE `customer` (
   `mobilenum` int(11) NOT NULL,
   `name` varchar(45) NOT NULL,
   `address` varchar(45) NOT NULL,
   `alternatemobilenumber` int(11) DEFAULT NULL,
   `relationshipnumber` int(11) DEFAULT NULL,
   `customerplan` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`mobilenum`),
   UNIQUE KEY `mobilenum_UNIQUE` (`mobilenum`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

Use a seguinte instrução DDL para criar a **faturas** tabela no banco de dados.

```sql
CREATE TABLE `bills` (
   `billplan` varchar(45) NOT NULL,
   `latepayment` decimal(4,2) NOT NULL,
   `monthlycharges` decimal(4,2) NOT NULL,
   `billdate` date NOT NULL,
   `billperiod` varchar(45) NOT NULL,
   `prevbal` decimal(4,2) NOT NULL,
   `callcharges` decimal(4,2) NOT NULL,
   `confcallcharges` decimal(4,2) NOT NULL,
   `smscharges` decimal(4,2) NOT NULL,
   `internetcharges` decimal(4,2) NOT NULL,
   `roamingnational` decimal(4,2) NOT NULL,
   `roamingintnl` decimal(4,2) NOT NULL,
   `vas` decimal(4,2) NOT NULL,
   `discounts` decimal(4,2) NOT NULL,
   `tax` decimal(4,2) NOT NULL,
   PRIMARY KEY (`billplan`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

Use a seguinte instrução DDL para criar a **chamadas** tabela no banco de dados.

```sql
CREATE TABLE `calls` (
   `mobilenum` int(11) DEFAULT NULL,
   `calldate` date DEFAULT NULL,
   `calltime` varchar(45) DEFAULT NULL,
   `callnumber` int(11) DEFAULT NULL,
   `callduration` varchar(45) DEFAULT NULL,
   `callcharges` decimal(4,2) DEFAULT NULL,
   `calltype` varchar(45) DEFAULT NULL
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

A variável **chamadas** A tabela inclui os detalhes da chamada, como data da chamada, hora da chamada, número da chamada, duração da chamada e encargos da chamada. A variável **cliente** A tabela é vinculada à tabela de chamadas usando o campo Mobile Number (mobilenum). Para cada número de celular listado no **cliente** tabela, há vários registros na **chamadas** tabela. Por exemplo, você pode recuperar os detalhes da chamada para a variável **1457892541** número do celular por meio da referência ao **chamadas** tabela.

A variável **faturas** A tabela inclui os detalhes de faturamento, como data de faturamento, período de faturamento, encargos mensais e encargos de chamada. A variável **cliente** A tabela está vinculada à variável **faturas** tabela usando o campo Plano de Faturamento. Há um plano associado a cada cliente na **cliente** tabela. A variável **faturas** A tabela inclui os detalhes de precificação de todos os planos existentes. Por exemplo, você pode recuperar os detalhes do plano para **Sarah** do **cliente** tabela e use esses detalhes para recuperar detalhes de preços da **faturas** tabela.

## Etapa 2: configurar o banco de dados MySQL como fonte de dados {#step-configure-mysql-database-as-data-source}

É possível configurar diferentes tipos de fontes de dados para criar um modelo de dados de formulário. Para este tutorial, você configurará o banco de dados MySQL que está configurado e preenchido com dados de amostra. Para obter informações sobre outras fontes de dados compatíveis e como configurá-las, consulte [Integração de dados do AEM Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html).

Faça o seguinte para configurar o banco de dados MySQL:

1. Instale o driver JDBC para o banco de dados MySQL como um pacote OSGi:

   1. Faça logon na instância do autor do AEM Forms como administrador e acesse os pacotes de console da Web AEM. O URL padrão é [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).
   1. Toque **Instalar/Atualizar**. Um **Carregar/instalar pacotes** será exibida.

   1. Toque **Escolher arquivo** para procurar e selecionar o pacote OSGi do driver JDBC MySQL. Selecionar **Iniciar pacote** e **Atualizar pacotes** e toque em **Instalar** ou **Atualizar**. Verifique se o driver JDBC da Oracle Corporation para MySQL está ativo. O driver está instalado.

1. Configure o banco de dados MySQL como uma fonte de dados:

   1. Ir para o console da Web do AEM em [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Localizar **Fonte de dados agrupada da conexão Apache Sling** configuração. Toque para abrir a configuração no modo de edição.
   1. Na caixa de diálogo de configuração, especifique os seguintes detalhes:

      * **Nome da fonte de dados:** Você pode especificar qualquer nome. Por exemplo, especifique **MySQL**.

      * **Nome da propriedade do serviço DataSource**: especifique o nome da propriedade de serviço que contém o nome da DataSource. É especificado ao registrar a instância da fonte de dados como serviço OSGi. Por exemplo, **datasource.name**.

      * **Classe de driver JDBC**: Especifique o nome da classe Java do driver JDBC. Para o banco de dados MySQL, especifique **com.mysql.jdbc.Driver**.

      * **URI da conexão JDBC**: especifique o URL de conexão do banco de dados. Para o banco de dados MySQL executado na porta 3306 e schema teleca, o URL é: `jdbc:mysql://'server':3306/teleca?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **Nome de usuário:** Nome de usuário do banco de dados. É necessário habilitar o driver JDBC para estabelecer uma conexão com o banco de dados.
      * **Senha:** Senha do banco de dados. É necessário habilitar o driver JDBC para estabelecer uma conexão com o banco de dados.
      * **Teste ao tomar emprestado:** Ativar o **Teste ao tomar emprestado** opção.

      * **Testar ao retornar:** Ativar o **Testar na devolução** opção.

      * **Consulta de validação:** Especifique uma consulta SQL SELECT para validar as conexões do pool. A consulta deve retornar pelo menos uma linha. Por exemplo, **selecionar &#42; do cliente**.

      * **Isolamento de transação**: Defina o valor como **READ_COMMITTED**.

   Deixar outras propriedades com o padrão [valores](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) e toque em **Salvar**.

   Uma configuração semelhante à seguinte é criada.

   ![Configuração do Apache](assets/apache_configuration_new.png)

## Etapa 3: Criar modelo de dados de formulário {#step-create-form-data-model}

O AEM Forms fornece uma interface intuitiva para [criar um modo de dados de formulário](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html#main-pars_header_1524967585)l de fontes de dados configuradas. É possível usar várias fontes de dados em um modelo de dados de formulário. Para o caso de uso deste tutorial, você usará o MySQL como fonte de dados.

Faça o seguinte para criar o modelo de dados de formulário:

1. Na instância do autor AEM, navegue até **Forms** > **Integrações de dados**.
1. Toque **Criar** > **Modelo de dados do formulário**.
1. No assistente Criar modelo de dados de formulário, especifique uma **name** para o modelo de dados do formulário. Por exemplo, **FDM_Create_First_IC**. Toque **Próxima**.
1. A tela selecionar fonte de dados lista todas as fontes de dados configuradas. Selecionar **MySQL** fonte de dados e toque em **Criar**.

   ![Fonte de dados MYSQL](assets/fdm_mysql_data_source_new.png)

1. Clique em **Concluído**. A variável **FDM_Create_First_IC** modelo de dados de formulário é criado.

## Etapa 4: configurar o modelo de dados de formulário {#step-configure-form-data-model}

A configuração do modelo de dados de formulário inclui:

* [adição de objetos e serviços de modelo de dados](#add-data-model-objects-and-services)
* [criação de propriedades filho computadas para o objeto de modelo de dados](#create-computed-child-properties-for-data-model-object)
* [adição de associações entre objetos de modelo de dados](#add-associations-between-data-model-objects)
* [edição de propriedades do objeto de modelo de dados](#edit-data-model-object-properties)
* [configuração de serviços para objetos de modelo de dados](#configure-services)

### Adicionar objetos e serviços de modelo de dados {#add-data-model-objects-and-services}

1. Na instância do autor AEM, navegue até **Forms** > **Integrações de dados**. O URL padrão é [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. A variável **FDM_Create_First_IC** o modelo de dados de formulário criado anteriormente está listado aqui. Selecione e toque em **Editar**.

   A fonte de dados selecionada **MySQL** é exibido na **Fontes de dados** painel.

   ![Fonte de dados MYSQL para FDM](assets/mysql_fdm_new.png)

1. Expanda a **MySQL** árvore da fonte de dados. Selecione os seguintes serviços e objetos de modelo de dados em **teleca** esquema:

   * **Objetos do modelo de dados**:

      * faturas
      * chamadas
      * cliente

   * **Serviços:**

      * obter
      * atualizar

   Toque **Adicionar selecionado** para adicionar objetos de modelo de dados e serviços selecionados ao modelo de dados de formulário.

   ![Selecionar serviços de objeto de modelo de dados](assets/select_data_model_object_services_new.png)

   Os objetos de modelo de dados de listas, chamadas e clientes são exibidos no painel direito na **Modelo** guia. Os serviços de obtenção e atualização são exibidos no **Serviços** guia.

   ![Objetos do modelo de dados](assets/data_model_objects_new.png)

### Criar propriedades filho computadas para o objeto de modelo de dados {#create-computed-child-properties-for-data-model-object}

Uma propriedade calculada é aquela cujo valor é calculado com base em uma regra ou expressão. Usando uma regra, você pode definir o valor de uma propriedade calculada como uma cadeia de caracteres literal, um número, o resultado de uma expressão matemática ou o valor de outra propriedade no modelo de dados de formulário.

Com base no caso de uso, crie o **encargos de uso** propriedade secundária calculada na variável **faturas** objeto de modelo de dados usando a seguinte expressão matemática:

* encargos de utilização = encargos das chamadas + encargos das chamadas em conferência + encargos SMS + encargos da internet móvel + itinerância nacional + itinerância internacional + SAV (todas estas propriedades existem no objeto de modelo de dados faturas) Para mais informações sobre a **encargos de uso** propriedade secundária calculada, consulte [Planejar a comunicação interativa](/help/forms/using/planning-interactive-communications.md).

Execute as seguintes etapas para criar propriedades-filho calculadas para o objeto de modelo de dados de listas:

1. Marque a caixa de seleção na parte superior da **faturas** objeto de modelo de dados para selecioná-lo e tocar **Criar propriedade secundária**.
1. No **Criar propriedade secundária** painel:

   1. Enter **encargos de uso** como o nome da propriedade secundária.
   1. Ativar **Calculado**.
   1. Selecionar **Flutuante** como o tipo e toque em **Concluído** para adicionar a propriedade secundária à **faturas** objeto de modelo de dados.

   ![Criar propriedade secundária](assets/create_child_property_new.png)

1. Toque **Editar regra** para abrir o Editor de regras.
1. Toque em **Criar**. A variável **Definir valor** a janela regra é aberta.
1. No menu suspenso Selecionar opção, selecione **Expressão matemática**.

   ![Editor de regras de encargos de uso](assets/usage_charges_rule_editor_new.png)

1. Na expressão matemática, selecione **encargos de chamada** e **confcallcharge** como primeiro e segundo objetos, respectivamente. Selecionar **mais** como operador. Toque na expressão matemática e toque em **Estender expressão** para adicionar **smscharge**, **taxas de internet**, **roamingnational**, **roamingintnl**, e **vas** objetos à expressão.

   A imagem a seguir descreve a expressão matemática no editor de regras:

   ![Regra de encargos de uso](assets/usage_charges_rule_all_new.png)

1. Toque **Concluído**. A regra é criada no Editor de regras.
1. Toque **Fechar** para fechar a janela Editor de regras.

### Adicionar associações entre objetos de modelo de dados {#add-associations-between-data-model-objects}

Depois que os objetos do modelo de dados tiverem sido definidos, você poderá criar associações entre eles. A associação pode ser um para um ou um para muitos. Por exemplo, pode haver vários dependentes associados a um funcionário. É chamada de associação um para muitos e é representada por 1:n na linha que conecta os objetos do modelo de dados associados. No entanto, se uma associação retornar um nome de funcionário exclusivo para uma determinada ID de funcionário, ela será chamada de associação um para um.

Ao adicionar objetos de modelo de dados associados em uma fonte de dados a um modelo de dados de formulário, suas associações são mantidas e exibidas como conectadas por linhas de seta.

Com base no caso de uso, crie as seguintes associações entre os objetos do modelo de dados:

| Associação | Objetos do modelo de dados |
|---|---|
| 1:n | cliente: chamadas (várias chamadas podem ser associadas a um cliente em uma fatura mensal) |
| 1:1 | cliente:listas (Um faturamento é associado a um cliente para um determinado mês) |

Execute as seguintes etapas para criar associações entre objetos de modelo de dados:

1. Marque a caixa de seleção na parte superior da **cliente** objeto de modelo de dados para selecioná-lo e tocar **Adicionar associação**. A variável **Adicionar associação** painel de propriedades é aberto.
1. No **Adicionar associação** painel:

   * Especifique um título para a associação. É um campo opcional.
   * Selecionar **Um para muitos** do **Tipo** lista suspensa.

   * Selecionar **chamadas** do **Objeto de modelo** lista suspensa.

   * Selecionar **obter** do **Serviço** lista suspensa.

   * Toque **Adicionar** para vincular a variável **cliente** objeto de modelo de dados para **chamadas** objeto de modelo de dados usando uma propriedade. Com base no caso de uso, o objeto de modelo de dados de chamadas deve ser vinculado à propriedade de número de celular no objeto de modelo de dados do cliente. A variável **Adicionar argumento** é aberta.

   ![Adicionar associação](assets/add_association_new.png)

1. No **Adicionar argumento** caixa de diálogo:

   * Selecionar **mobilenum** do **Nome** lista suspensa. A propriedade de número de celular é uma propriedade comum disponível no cliente e chama objetos de modelo de dados. Como resultado, é usado para criar uma associação entre o cliente e chamar objetos de modelo de dados.
Para cada número de celular disponível no objeto de modelo de dados do cliente, há vários registros de chamada disponíveis na tabela de chamadas.

   * Especifique um título opcional e uma descrição para o argumento.
   * Selecionar **cliente** do **Vinculando a** lista suspensa.

   * Selecionar **mobilenum** do **Valor do vínculo** lista suspensa.

   * Toque **Adicionar**.

   ![Adicionar associação para um argumento](assets/add_association_argument_new.png)

   A propriedade mobilenum é exibida no campo **Argumentos** seção.

   ![Adicionar associação de argumento](assets/add_argument_association_new.png)

1. Toque **Concluído** para criar uma associação 1:n entre objetos de modelo de dados cliente e chamadas.

   Depois de criar uma associação entre o cliente e chamar objetos de modelo de dados, crie uma associação 1:1 entre o cliente e os objetos de modelo de dados de faturamento.

1. Marque a caixa de seleção na parte superior da **cliente** objeto de modelo de dados para selecioná-lo e tocar **Adicionar associação**. A variável **Adicionar associação** painel de propriedades é aberto.
1. No **Adicionar associação** painel:

   * Especifique um título para a associação. É um campo opcional.
   * Selecionar **Um para um** do **Tipo** lista suspensa.

   * Selecionar **faturas** do **Objeto de modelo** lista suspensa.

   * Selecionar **obter** do **Serviço** lista suspensa. A variável **plano de cobrança** propriedade, que é a chave primária para a tabela de faturas, já está disponível na **Argumentos** seção.
Os objetos de modelo de dados de listas e clientes são vinculados usando as propriedades billplan (listas) e customerplan (cliente), respectivamente. Crie um vínculo entre essas propriedades para recuperar os detalhes do plano para qualquer cliente disponível no banco de dados MySQL.

   * Selecionar **cliente** do **Vinculando a** lista suspensa.

   * Selecionar **customerplan** do **Valor do vínculo** lista suspensa.

   * Toque **Concluído** para criar uma vinculação entre as propriedades billplan e customerplan.

   ![Adicionar associação para fatura de cliente](assets/add_association_customer_bills_new.png)

   A imagem a seguir descreve as associações entre os objetos do modelo de dados e as propriedades usadas para criar associações entre eles:

   ![fdm_associations](assets/fdm_associations.gif)

### Editar propriedades do objeto de modelo de dados {#edit-data-model-object-properties}

Depois de criar associações entre o cliente e outros objetos de modelo de dados, edite as propriedades do cliente para definir a propriedade com base na qual os dados são recuperados do objeto de modelo de dados. Com base no caso de uso, o número de celular é usado como a propriedade para recuperar dados do objeto de modelo de dados do cliente.

1. Marque a caixa de seleção na parte superior da **cliente** objeto de modelo de dados para selecioná-lo e tocar **Editar propriedades**. A variável **Editar propriedades** será aberto.
1. Especificar **cliente** como o **Objeto de modelo de nível superior**.
1. Selecionar **obter** do **Serviço de leitura** lista suspensa.
1. No **Argumentos** seção:

   * Selecionar **Solicitar atributo** do **Vinculando a** lista suspensa.

   * Especificar **mobilenum** como o Valor de vinculação.

1. Selecionar **atualizar** do **Gravar** Lista suspensa Serviço.
1. No **Argumentos** seção:

   * Para **mobilenum** , selecione **cliente** do **Vinculando a** lista suspensa.

   * Selecionar **mobilenum** do **Valor do vínculo** lista suspensa.

1. Toque **Concluído** para salvar as propriedades.

   ![Configurar serviços](assets/configure_services_customer_new.png)

1. Marque a caixa de seleção na parte superior da **chamadas** objeto de modelo de dados para selecioná-lo e tocar **Editar propriedades**. A variável **Editar propriedades** será aberto.
1. Desative o **Objeto de modelo de nível superior** para **chamadas** objeto de modelo de dados.
1. Toque **Concluído**.

   Repita as etapas 8 - 10 para configurar as propriedades para **faturas** objeto de modelo de dados.

### Configurar serviços {#configure-services}

1. Vá para a **Serviços** guia.
1. Selecione o **obter** serviço e toque em **Editar propriedades**. A variável **Editar propriedades** será aberto.
1. No **Editar propriedades** painel:

   * Insira um título opcional e uma descrição.
   * Selecionar **cliente** do **Objeto de modelo de saída** lista suspensa.

   * Toque **Concluído** para salvar as propriedades.

   ![Editar propriedades](assets/edit_properties_get_details_new.png)

1. Selecione o **atualizar** serviço e toque em **Editar propriedades**. A variável **Editar propriedades** será aberto.
1. No **Editar propriedades** painel:

   * Insira um título opcional e uma descrição.
   * Selecionar **cliente** do **Objeto de modelo de entrada** lista suspensa.

   * Toque **Concluído**.
   * Toque **Salvar** para salvar o modelo de dados do formulário.

   ![Atualizar propriedades do serviço](assets/update_service_properties_new.png)

## Etapa 5: testar o modelo de dados e os serviços do formulário {#step-test-form-data-model-and-services}

Você pode testar o objeto de modelo de dados e os serviços para verificar se o modelo de dados de formulário está configurado corretamente.

Faça o seguinte para executar o teste:

1. Vá para a **Modelo** , selecione a **cliente** modelo de dados e toque em **Testar objeto de modelo**.
1. No **Testar modelo de dados do formulário** selecione **Ler objeto de modelo** do **Selecionar modelo/serviço** lista suspensa.
1. No **Entrada** especifique um valor para a variável **mobilenum** que existe no banco de dados MySQL configurado e toque em **Teste**.

   Os detalhes do cliente associados à propriedade mobilenum especificada são obtidos e exibidos na seção Saída, como mostrado abaixo. Feche a caixa de diálogo.

   ![Testar modelo de dados](assets/test_data_model_new.png)

1. Vá para a **Serviços** guia.
1. Selecione o **obter** serviço e toque em **Testar serviço.**
1. No **Entrada** especifique um valor para a variável **mobilenum** que existe no banco de dados MySQL configurado e toque em **Teste**.

   Os detalhes do cliente associados à propriedade mobilenum especificada são obtidos e exibidos na seção Saída, como mostrado abaixo. Feche a caixa de diálogo.

   ![Testar serviço](assets/test_service_new.png)

### Editar e salvar dados de amostra {#edit-and-save-sample-data}

O editor do modelo de dados de formulário permite gerar dados de amostra para todas as propriedades do objeto de modelo de dados, incluindo propriedades computadas, em um modelo de dados de formulário. É um conjunto de valores aleatórios que estão em conformidade com o tipo de dados configurado para cada propriedade. Também é possível editar e salvar os dados, que são retidos mesmo que você gere novamente os dados de amostra.

Faça o seguinte para gerar, editar e salvar dados de amostra:

1. Na página do modelo de dados do formulário, toque em **Editar dados de amostra**. Ele gera e exibe os dados de amostra na janela Editar dados de amostra.

   ![Editar dados de amostra](assets/edit_sample_data_new.png)

1. Entrada **Editar dados de amostra** editar dados, conforme necessário, e toque em **Salvar**. Feche a janela.
