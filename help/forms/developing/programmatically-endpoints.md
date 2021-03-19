---
title: Gerenciar endpoints de forma programática
seo-title: Gerenciar endpoints de forma programática
description: Use o serviço Endpoint Registry para adicionar pontos de extremidade EJB, adicionar pontos de extremidade SOAP, adicionar pontos de extremidade de Pasta assistida, adicionar pontos de extremidade de email, adicionar pontos de extremidade Remoting, adicionar pontos de extremidade do Gerenciador de tarefas, modificar pontos de extremidade, remover pontos de extremidade e recuperar informações do conector do ponto de extremidade.
seo-description: Use o serviço Endpoint Registry para adicionar pontos de extremidade EJB, adicionar pontos de extremidade SOAP, adicionar pontos de extremidade de Pasta assistida, adicionar pontos de extremidade de email, adicionar pontos de extremidade Remoting, adicionar pontos de extremidade do Gerenciador de tarefas, modificar pontos de extremidade, remover pontos de extremidade e recuperar informações do conector do ponto de extremidade.
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
role: Desenvolvedor
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '10864'
ht-degree: 1%

---


# Gerenciando Programaticamente Endpoints {#programmatically-managing-endpoints}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

**Sobre o serviço de registro do Endpoint**

O serviço Endpoint Registry fornece a capacidade de gerenciar programaticamente os endpoints. Você pode, por exemplo, adicionar os seguintes tipos de endpoints a um serviço:

* EJB
* SOAP
* Pasta assistida
* E-mail
* (Obsoleto para formulários AEM) Remoção
* Gerenciador de tarefas

>[!NOTE]
>
>SOAP, EJB e (obsoleto para formulários AEM no JEE) Os pontos finais remotos são criados automaticamente para cada serviço ativado. Os endpoints SOAP e EJB habilitam SOAP e EJB para todas as operações de serviço.

Um terminal Remoting permite que os clientes Flex chamem operações no serviço AEM Forms ao qual o terminal foi adicionado. Um destino Flex com o mesmo nome do ponto de extremidade é criado e os clientes Flex podem criar RemoteObjects que apontam para esse destino para chamar operações no serviço relevante.

Os endpoints Email, Gerenciador de tarefas e Pasta assistida expõem apenas uma operação específica do serviço. A adição desses endpoints requer uma segunda etapa de configuração para selecionar um método para chamar, definir parâmetros de configuração e especificar mapeamentos de parâmetros de entrada e saída.

Você pode organizar endpoints do TaskManager em grupos chamados *categories*. Essas categorias são então expostas ao Workspace por meio do TaskManager, com os usuários finais vendo os pontos de extremidade do TaskManager à medida que são categorizados. No Workspace, os usuários finais visualizam essas categorias no painel de navegação. Os endpoints em cada categoria são exibidos como cartões de processo na página Iniciar processos no Workspace.

Você pode realizar essas tarefas usando o serviço Endpoint Registry:

* Adicione pontos de extremidade EJB. (Consulte [Adicionar Endpoints EJB](programmatically-endpoints.md#adding-ejb-endpoints).)
* Adicione pontos de extremidade SOAP. (Consulte [Adicionar Endpoints SOAP](programmatically-endpoints.md#adding-soap-endpoints).)
* Adicionar endpoints de pastas assistidos (consulte [Adicionar endpoints de pasta assistidos](programmatically-endpoints.md#adding-watched-folder-endpoints).)
* Adicionar endpoints de email. (Consulte [Adicionar Endpoints de Email](programmatically-endpoints.md#adding-email-endpoints).)
* Adicione pontos de extremidade remotos. (Consulte [Adicionar Pontos de Extremidade Remotos](programmatically-endpoints.md#adding-remoting-endpoints).)
* Adicionar endpoints do TaskManager (Consulte [Adicionar Endpoints do TaskManager](programmatically-endpoints.md#adding-taskmanager-endpoints).)
* Modifique endpoints (Consulte [Modificando Endpoints](programmatically-endpoints.md#modifying-endpoints).)
* Remova pontos de extremidade (consulte [Removendo pontos de extremidade](programmatically-endpoints.md#removing-endpoints).)
* Recuperar informações do conector do ponto de extremidade (Consulte [Recuperando Informações do Conector do Ponto de Extremidade](programmatically-endpoints.md#retrieving-endpoint-connector-information).)

## Adicionar Endpoints EJB {#adding-ejb-endpoints}

Você pode adicionar um ponto de extremidade EJB a um serviço por programação usando a API Java do AEM Forms. Ao adicionar um ponto de extremidade EJB a um serviço, você está permitindo que um aplicativo cliente chame o serviço usando o modo EJB. Ou seja, ao definir propriedades de conexão necessárias para chamar o AEM Forms, você pode selecionar o modo EJB. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>Não é possível adicionar um ponto de extremidade EJB usando serviços da Web.

>[!NOTE]
>
>Normalmente, um ponto de extremidade EJB é adicionado a um serviço por padrão. No entanto, um ponto de extremidade EJB pode ser adicionado a um processo que é programaticamente implantado ou quando um ponto de extremidade EJB foi removido e deve ser adicionado novamente.

### Resumo das etapas {#summary-of-steps}

Para adicionar um ponto de extremidade EJB a um serviço, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto `EndpointRegistry Client`.
1. Defina os atributos do ponto de extremidade EJB.
1. Crie um ponto de extremidade EJB.
1. Habilite o endpoint .

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de cliente EndpointRegistry**

Antes de poder adicionar programaticamente um ponto de extremidade EJB, você deve criar um objeto `EndpointRegistryClient`.

**Definir atributos de ponto de extremidade EJB**

Para criar um ponto de extremidade EJB para um serviço, especifique os seguintes valores:

* **Identificador** do conector: Especifica o tipo de ponto de extremidade a ser criado. Para criar um ponto de extremidade EJB, especifique `EJB`.
* **Descrição**: Especifica a descrição do ponto de extremidade.
* **Nome**: Especifica o nome do ponto de extremidade.
* **Identificador** de serviço: Especifica o serviço ao qual o ponto de extremidade pertence.
* **Nome** da operação: Especifica o nome da operação que é invocada usando o ponto de extremidade. Ao criar um ponto de extremidade EJB, especifique um caractere curinga ( `*`). No entanto, se quiser especificar uma operação específica em vez de chamar todas as operações de serviço, especifique o nome da operação, em vez de usar o caractere curinga ( `*`).

**Criar um ponto de extremidade EJB**

Depois de definir atributos de ponto de extremidade EJB, você pode criar um ponto de extremidade EJB para um serviço.

**Ativar o ponto de extremidade**

Depois de criar um novo terminal, você deve habilitá-lo. Após habilitar o endpoint, ele poderá ser usado para chamar o serviço. Depois de ativar o endpoint, você pode visualizá-lo no console de administração.

**Consulte também:**

[Adicionar um ponto de extremidade EJB usando a API Java](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicionar um ponto de extremidade EJB usando a API Java {#adding-an-ejb-endpoint-using-the-java-api}

Adicione um ponto de extremidade EJB usando a API do Java:

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java. (

1. Crie um objeto Cliente EndpointRegistry.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `EndpointRegistryClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Defina os atributos do ponto de extremidade EJB.

   * Crie um objeto `CreateEndpointInfo` usando seu construtor.
   * Especifique o valor do identificador do conector, chamando o método `CreateEndpointInfo` do objeto e passando o valor da string `EJB`.`setConnectorId`
   * Especifique a descrição do ponto de extremidade chamando o método `CreateEndpointInfo` do objeto `setDescription` e passando um valor de string que descreve o ponto de extremidade.
   * Especifique o nome do ponto final chamando o método `CreateEndpointInfo` do objeto `setName` e passando um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o método `CreateEndpointInfo` do objeto `setServiceId` e passando um valor de string que especifica o nome do serviço.
   * Especifique a operação que é invocada chamando o método `CreateEndpointInfo` do objeto `setOperationName` e transmita um valor de string que especifica o nome da operação. Para pontos de extremidade SOAP e EJB, especifique um caractere curinga ( `*`), o que implica todas as operações.

1. Crie um ponto de extremidade EJB.

   Crie o ponto de extremidade chamando o método `EndpointRegistryClient` do objeto `createEndpoint` e transmitindo o objeto `CreateEndpointInfo`. Este método retorna um objeto `Endpoint` que representa o novo ponto de extremidade EJB.

1. Habilite o endpoint .

   Ative o endpoint chamando o método enable do objeto `EndpointRegistryClient` e transmitindo o objeto `Endpoint` retornado pelo método `createEndpoint`.

**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Adicionar um ponto de extremidade EJB usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Adicionar pontos de extremidade SOAP {#adding-soap-endpoints}

Você pode adicionar um terminal SOAP a um serviço por programação usando a API do AEM Forms Java. Ao adicionar um ponto de extremidade SOAP, você permite que um aplicativo cliente chame o serviço usando o modo SOAP. Ou seja, ao definir as propriedades de conexão necessárias para chamar o AEM Forms, você pode selecionar o modo SOAP.

>[!NOTE]
>
>Não é possível adicionar um terminal SOAP usando serviços da Web.

>[!NOTE]
>
>Normalmente, um ponto de extremidade SOAP é adicionado a um serviço por padrão. No entanto, um ponto de extremidade SOAP pode ser adicionado a um processo que é implantado programaticamente ou quando um ponto de extremidade SOAP é removido e deve ser adicionado novamente.

### Resumo das etapas {#summary_of_steps-1}

Para adicionar um terminal SOAP a um serviço, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto `EndpointRegistryClient`.
1. Defina atributos de ponto de extremidade SOAP.
1. Crie um terminal SOAP.
1. Habilite o endpoint .

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

Esses arquivos JAR são necessários para criar um terminal SOAP. No entanto, é necessário adicionar arquivos JAR se você usar o terminal SOAP para chamar o serviço. Para obter informações sobre arquivos AEM Forms JAR, consulte [Incluindo arquivos da biblioteca AEM Forms Java](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de cliente EndpointRegistry**

Para adicionar programaticamente um terminal SOAP a um serviço, é necessário criar um objeto `EndpointRegistryClient`.

**Definir atributos de ponto de extremidade SOAP**

Para adicionar um terminal SOAP a um serviço, especifique os seguintes valores:

* **Valor** do identificador do conector: Especifica o tipo de ponto de extremidade a ser criado. Para criar um ponto de extremidade SOAP, especifique `SOAP`.
* **Descrição**: Especifica a descrição do ponto de extremidade.
* **Nome**: Especifica o nome do ponto de extremidade.
* **Valor** do identificador de serviço: Especifica o serviço ao qual o ponto de extremidade pertence.
* **Nome** da operação: Especifica o nome da operação que é invocada usando o ponto de extremidade. Ao criar um ponto de extremidade SOAP, especifique um caractere curinga ( `*`). No entanto, se quiser especificar uma operação específica em vez de chamar todas as operações de serviço, especifique o nome da operação, em vez de usar o caractere curinga ( `*`).

**Criar um terminal SOAP**

Depois de definir atributos de ponto de extremidade SOAP, você pode criar um ponto de extremidade SOAP.

**Ativar o ponto de extremidade**

Depois de criar um novo terminal, você deve habilitá-lo. Quando o endpoint está ativado, ele pode ser usado para chamar o serviço. Depois de ativar o endpoint, você pode visualizá-lo no console de administração.

**Consulte também:**

[Adicionar um terminal SOAP usando a API Java](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicione um terminal SOAP usando a API Java {#add-a-soap-endpoint-using-the-java-api}

Adicione um terminal SOAP a um serviço usando a API do Java:

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto Cliente EndpointRegistry.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `EndpointRegistryClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Defina atributos de ponto de extremidade SOAP.

   * Crie um objeto `CreateEndpointInfo` usando seu construtor.
   * Especifique o valor do identificador do conector, chamando o método `CreateEndpointInfo` do objeto e passando o valor da string `SOAP`.`setConnectorId`
   * Especifique a descrição do ponto de extremidade chamando o método `CreateEndpointInfo` do objeto `setDescription` e passando um valor de string que descreve o ponto de extremidade.
   * Especifique o nome do ponto final chamando o método `CreateEndpointInfo` do objeto `setName` e passando um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o método `CreateEndpointInfo` do objeto `setServiceId` e passando um valor de string que especifica o nome do serviço.
   * Especifique a operação que é invocada chamando o método `CreateEndpointInfo` do objeto `setOperationName` e passando um valor de string que especifica o nome da operação. Para pontos de extremidade SOAP e EJB, especifique um caractere curinga ( `*`), o que implica todas as operações.

1. Crie um terminal SOAP.

   Crie o ponto de extremidade chamando o método `EndpointRegistryClient` do objeto `createEndpoint` e transmitindo o objeto `CreateEndpointInfo`. Esse método retorna um objeto `Endpoint` que representa o novo ponto de extremidade SOAP.

1. Habilite o endpoint .

   Ative o endpoint chamando o método enable do objeto `EndpointRegistryClient` e transmita o objeto `Endpoint` retornado pelo método `createEndpoint`.

**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Adicionar um terminal SOAP usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Adicionar pontos de extremidade de pasta assistida {#adding-watched-folder-endpoints}

Você pode adicionar programaticamente um endpoint de Pasta assistida a um serviço usando a API Java do AEM Forms. Ao adicionar um endpoint de Pasta assistida, os usuários podem colocar um arquivo (como um arquivo PDF) em uma pasta. Quando o arquivo é colocado na pasta, o serviço configurado é chamado e manipula o arquivo. Depois que o serviço executa a operação especificada, ele salva o arquivo modificado em uma pasta de saída especificada. Uma pasta assistida é configurada para ser digitalizada em um intervalo de taxa fixa ou com um cronograma de medição, como todas as segundas, quartas e sextas-feiras ao meio-dia.

Para adicionar programaticamente um ponto de extremidade de Pasta assistida a um serviço, considere o seguinte processo de curta duração chamado *EncryptDocument*. (Consulte [Entendendo os processos do AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

Esse processo aceita um documento PDF não seguro como um valor de entrada e, em seguida, passa o documento PDF não seguro para a operação `EncryptPDFUsingPassword` do serviço de criptografia. O documento PDF é criptografado com uma senha e o documento PDF criptografado por senha é o valor de saída desse processo. O nome do valor de entrada (o documento PDF não seguro) é `InDoc` e o tipo de dados é `com.adobe.idp.Document`. O nome do valor de saída (o documento PDF criptografado por senha) é `SecuredDoc` e o tipo de dados é `com.adobe.idp.Document`.

>[!NOTE]
>
>Não é possível adicionar um endpoint de Pasta assistida usando serviços da Web.

### Resumo das etapas {#summary_of_steps-2}

Para adicionar um endpoint de Pasta assistida a um serviço, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto `EndpointRegistryClient`.
1. Defina os atributos do ponto de extremidade da pasta assistida.
1. Especifique os valores de configuração.
1. Defina os valores dos parâmetros de entrada.
1. Defina um valor de parâmetro de saída.
1. Crie um ponto de extremidade de Pasta assistida.
1. Habilite o endpoint .

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de cliente EndpointRegistry**

Para adicionar programaticamente um ponto de extremidade de Pasta assistida, é necessário criar um objeto `EndpointRegistryClient` .

**Definir atributos de ponto de extremidade de pasta assistida**

Para criar um endpoint de Pasta assistida para um serviço, especifique os seguintes valores:

* **Identificador** do conector: Especifica o tipo de ponto de extremidade criado. Para criar um ponto de extremidade de Pasta assistida, especifique `WatchedFolder`.
* **Descrição**: Especifica a descrição do ponto de extremidade.
* **Nome**: Especifica o nome do ponto de extremidade.
* **Identificador** de serviço: Especifica o serviço ao qual o ponto de extremidade pertence. Por exemplo, para adicionar um endpoint de Pasta assistida ao processo que é introduzido nesta seção (um processo se torna um serviço quando ativado usando o Workbench), especifique `EncryptDocument`.
* **Nome** da operação: Especifica o nome da operação que é invocada usando o ponto de extremidade. Normalmente, ao criar um endpoint de Pasta assistida para um serviço originado de um processo criado no Workbench, o nome da operação é `invoke`.

**Especificar valores de configuração**

Você deve especificar valores de configuração para um endpoint de Pasta assistida ao adicionar programaticamente um endpoint de Pasta assistida a um serviço. Esses valores de configuração são especificados por um administrador se um endpoint Pasta assistida for adicionado usando o console de administração.

A lista a seguir especifica os valores de configuração que são definidos ao adicionar programaticamente um ponto de extremidade de Pasta assistida a um serviço:

* **url**: Especifica o local da pasta monitorada. Em um ambiente em cluster, esse valor deve apontar para uma pasta de rede compartilhada acessível de cada computador no cluster.
* **assíncrono**: Identifica o tipo de invocação como assíncrona ou síncrona. Processos transitórios e síncronos só podem ser invocados de forma síncrona. O valor padrão é true. Recomenda-se assíncrono.
* **cronExpression**: Usado por quartzo para agendar a pesquisa do diretório de entrada. Para obter detalhes sobre como configurar a expressão cron, consulte [https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html](https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html).
* **purgeDuration**: Este é um atributo obrigatório. Os arquivos e pastas na pasta de resultados são removidos quando são mais antigos que esse valor. Esse valor é medido em dias. Esse atributo é útil para garantir que a pasta de resultados não fique cheia. Um valor de -1 dias indica que nunca excluir a pasta de resultados. O valor padrão é -1.
* **repeatInterval**: O intervalo, em segundos, para verificar a entrada da Pasta assistida. A menos que a limitação esteja ativada, esse valor deve ser maior que o tempo para processar um trabalho médio; caso contrário, o sistema poderá ficar sobrecarregado. O valor padrão é 5.
* **repeatCount**: O número de vezes que uma Pasta assistida verifica a pasta ou o diretório. Um valor de -1 indica varredura indefinida. O valor padrão é -1.
* **throttleOn**: Limita o número de trabalhos de Pasta assistida que podem ser processados em um determinado momento. O número máximo de trabalhos é determinado pelo valor batchSize.
* **userName**: O nome de usuário usado ao invocar um serviço de destino a partir da Pasta assistida. Esse valor é obrigatório. O valor padrão é SuperAdmin.
* **domainName**: O domínio do usuário. Esse valor é obrigatório. O valor padrão é DefaultDom.
* **batchSize**: O número de arquivos ou pastas a serem coletados por varredura. Use esse valor para evitar sobrecarga no sistema; a verificação de muitos arquivos de uma vez pode resultar em falha. O valor padrão é 2.
* **waitTime**: O tempo, em milissegundos, para aguardar antes de digitalizar uma pasta ou arquivo após a criação. Por exemplo, se o tempo de espera for de 36.000.000 milissegundos (uma hora) e o arquivo tiver sido criado um minuto atrás, esse arquivo será selecionado após 59 ou mais minutos terem passado. Esse atributo é útil para garantir que um arquivo ou pasta seja copiado completamente para a pasta de entrada. Por exemplo, se você tiver um arquivo grande para processar e o arquivo levar dez minutos para ser baixado, defina o tempo de espera como 10&amp;ast;60 &amp;ast;1000 milissegundos. Essa configuração impede que a pasta assistida verifique o arquivo se ele não estiver aguardando por dez minutos. O valor padrão é 0.
* **excludeFilePattern**: O padrão que uma pasta assistida usa para determinar quais arquivos e pastas serão examinados e coletados. Qualquer arquivo ou pasta que tenha esse padrão não será verificado para processamento. Essa configuração é útil quando a entrada é uma pasta que contém vários arquivos. O conteúdo da pasta pode ser copiado em uma pasta que tenha um nome que será selecionado pela pasta assistida. Essa etapa impede que a pasta assistida escolha uma pasta para processamento antes que ela seja completamente copiada para a pasta de entrada. Por exemplo, se o valor excludeFilePattern for `data*`, todos os arquivos e pastas que correspondem a `data*` não serão coletados. Isso inclui arquivos e pastas chamados `data1`, `data2`, e assim por diante. Além disso, o padrão pode ser complementado com padrões curingas para especificar padrões de arquivo. A pasta assistida modifica a expressão regular para suportar padrões curingas, como `*.*` e `*.pdf`. Esses padrões curingas não são compatíveis com expressões regulares.
* **includeFilePattern**: O padrão que a pasta assistida usa para determinar quais pastas e arquivos digitalizar e coletar. Por exemplo, se esse valor for `*`, todos os arquivos e pastas que correspondem a `input*` serão coletados. Isso inclui arquivos e pastas chamados `input1`, `input2`, e assim por diante. O valor padrão é `*`. Esse valor indica todos os arquivos e pastas. Além disso, o padrão pode ser complementado com padrões curingas para especificar padrões de arquivo. A pasta assistida modifica a expressão regular para suportar padrões curingas, como `*.*` e `*.pdf`. Esses padrões curingas não são compatíveis com expressões regulares. Esse valor é obrigatório.
* **resultFolderName**: A pasta onde os resultados salvos são armazenados. Esse local pode ser um caminho absoluto ou relativo do diretório. Se os resultados não forem exibidos nessa pasta, verifique a pasta de falha. Os arquivos somente leitura não são processados e serão salvos na pasta de falha. O valor padrão é `result/%Y/%M/%D/`. Esta é a pasta de resultados dentro da pasta observada.
* **preserveFolderName**: O local onde os arquivos são armazenados após a varredura e coleta bem-sucedidas. Esse local pode ser absoluto, relativo ou nulo. O valor padrão é `preserve/%Y/%M/%D/`.
* **failureFolderName**: A pasta onde os arquivos de falha são salvos. Esse local é sempre relativo à pasta assistida. Os arquivos somente leitura não são processados e serão salvos na pasta de falha. O valor padrão é `failure/%Y/%M/%D/`.
* **preserveOnFailure**: Preservar arquivos de entrada em caso de falha na execução da operação em um serviço. O valor padrão é true.
* **overwriteDuplicateFilename**: Quando definido como true, os arquivos na pasta de resultados e na pasta preserve são substituídos. Quando definido como falso, os arquivos e pastas que têm um sufixo de índice numérico são usados para o nome. O valor padrão é false.

**Definir valores de parâmetros de entrada**

Ao criar um ponto de extremidade de Pasta assistida, é necessário definir valores de parâmetro de entrada. Ou seja, você deve descrever os valores de entrada passados para a operação que é invocada pela pasta assistida. Por exemplo, considere o processo introduzido neste tópico. Ele tem um valor de entrada chamado `InDoc` e seu tipo de dados é `com.adobe.idp.Document`. Ao criar um endpoint de Pasta assistida para esse processo (depois que um processo é ativado, ele se torna um serviço), é necessário definir o valor do parâmetro de entrada.

Para definir os valores de parâmetro de entrada necessários para um endpoint de Pasta assistida, especifique os seguintes valores:

**Nome** do parâmetro de entrada: O nome do parâmetro de entrada. O nome de um valor de entrada é especificado no Workbench para um processo. Se o valor de entrada pertencer a uma operação de serviço (um serviço que não é um processo criado no Workbench), o nome de entrada será especificado no arquivo component.xml. Por exemplo, o nome do parâmetro de entrada para o processo introduzido nesta seção é `InDoc`.

**Tipo** de mapeamento: Usado para configurar os valores de entrada necessários para chamar a operação de serviço. Existem dois tipos de mapeamento:

* `Literal`: O endpoint Pasta assistida usa o valor inserido no campo como ele é exibido. Todos os tipos básicos de Java são suportados. Por exemplo, se uma API usar entrada, como String, long, int e Boolean, a cadeia de caracteres será convertida no tipo adequado e o serviço será chamado.
* `Variable`: O valor inserido é um padrão de arquivo que a pasta assistida usa para escolher a entrada. Por exemplo, se você selecionar Variável para o tipo de mapeamento e o documento de entrada precisar ser um arquivo PDF, poderá especificar `*.pdf`como o valor de mapeamento.

**Valor** do mapeamento: Especifica o valor do tipo de mapeamento. Por exemplo, se você selecionar um tipo de mapeamento `Variable` , poderá especificar `*.pdf` como o padrão de arquivo.

**Tipo** de dados: Especifica o tipo de dados dos valores de entrada. Por exemplo, o tipo de dados do valor de entrada do processo introduzido nesta seção é `com.adobe.idp.Document`.

**Definir um valor de parâmetro de saída**

Ao criar um endpoint de Pasta assistida, é necessário definir um valor de parâmetro de saída. Ou seja, você deve descrever o valor de saída que é retornado pelo serviço chamado pelo endpoint Pasta assistida . Por exemplo, considere o processo introduzido neste tópico. Ele tem um valor de saída chamado `SecuredDoc` e seu tipo de dados é `com.adobe.idp.Document`. Ao criar um endpoint de Pasta assistida para esse processo (depois que um processo é ativado, ele se torna um serviço), é necessário definir o valor do parâmetro de saída.

Para definir um valor de parâmetro de saída necessário para um endpoint de Pasta assistida, especifique os seguintes valores:

**Nome** do parâmetro de saída: O nome do parâmetro de saída. O nome de um valor de saída do processo é especificado no Workbench. Se o valor de saída pertencer a uma operação de serviço (um serviço que não é um processo criado no Workbench), o nome de saída será especificado no arquivo component.xml. Por exemplo, o nome do parâmetro de saída para o processo introduzido nesta seção é `SecuredDoc`.

**Tipo** de mapeamento: Usado para configurar a saída do serviço e da operação. As opções disponíveis são as seguintes:

* Se o serviço retornar um único objeto (um único documento), o padrão será `%F.pdf` e o destino de origem será sourcefilename.pdf. Por exemplo, o processo introduzido nesta seção retorna um único documento. Como resultado, o tipo de mapeamento pode ser definido como `%F.pdf` ( `%F` significa usar o nome de arquivo especificado). O padrão `%E` especifica a extensão do documento de entrada.
* Se o serviço retornar uma lista, o padrão será `Result\%F\`, e o destino de origem será Result\sourcefilename\source1 (output 1) e Result\sourcefilename\source2 (output 2).
* Se o serviço retornar um mapa, o padrão será `Result\%F\` e o destino de origem será Result\sourcefilename\file1 and Result\sourcefilename\file2. Se o mapa tiver mais de um objeto, o padrão será `Result\%F.pdf` e o destino de origem será Result\sourcefilename1.pdf (saída 1), Result\sourcefilenam2.pdf (saída 2) e assim por diante.

**Tipo** de dados: Especifica o tipo de dados do valor de retorno. Por exemplo, o tipo de dados do valor de retorno do processo introduzido nesta seção é `com.adobe.idp.Document`.

**Criar um endpoint de pasta monitorada**

Depois de definir os atributos do ponto de extremidade, os valores de configuração e os valores de parâmetro de entrada e saída, é necessário criar o ponto de extremidade Pasta assistida.

**Ativar o ponto de extremidade**

Depois de criar um endpoint de Pasta assistida, você deve ativá-lo. Quando o endpoint está ativado, ele pode ser usado para chamar o serviço. Depois de ativar o endpoint, você pode visualizá-lo no console de administração.

**Consulte também:**

[Adicionar um endpoint de pasta assistida usando a API Java](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicione um endpoint de pasta assistida usando a API Java {#add-a-watched-folder-endpoint-using-the-java-api}

Adicione um endpoint de Pasta assistida usando a API do Java do AEM Forms:

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto Cliente EndpointRegistry.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `EndpointRegistryClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Defina os atributos do ponto de extremidade da pasta assistida.

   * Crie um objeto `CreateEndpointInfo` usando seu construtor.
   * Especifique o valor do identificador do conector, chamando o método `CreateEndpointInfo` do objeto e passando o valor da string `WatchedFolder`.`setConnectorId`
   * Especifique a descrição do ponto de extremidade chamando o método `CreateEndpointInfo` do objeto `setDescription` e passando um valor de string que descreve o ponto de extremidade.
   * Especifique o nome do ponto final chamando o método `CreateEndpointInfo` do objeto `setName` e passando um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o método `CreateEndpointInfo` do objeto `setServiceId` e passando um valor de string que especifica o nome do serviço.
   * Especifique a operação que é invocada chamando o método `CreateEndpointInfo` do objeto `setOperationName` e passando um valor de string que especifica o nome da operação. Normalmente, ao criar um endpoint de Pasta assistida para um serviço originado de um processo criado no Workbench, o nome da operação é chamado.

1. Especifique os valores de configuração.

   Para cada valor de configuração a ser definido para o endpoint Pasta assistida, você deve chamar o método `CreateEndpointInfo` do objeto `setConfigParameterAsText`. Por exemplo, para definir o valor de configuração `url`, chame o método `CreateEndpointInfo` do objeto `setConfigParameterAsText` e passe os seguintes valores da string:

   * Um valor de string que especifica o nome do valor de configuração. Ao definir o valor de configuração `url`, especifique `url`.
   * Um valor de string que especifica o valor do valor de configuração. Ao definir o valor de configuração `url`, especifique o local da pasta monitorada.

   >[!NOTE]
   >
   >Para ver todos os valores de configuração definidos para o serviço EncryptDocument, consulte o exemplo de código Java localizado em [QuickStart: Adicionar um endpoint de pasta assistida usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api).

1. Defina os valores dos parâmetros de entrada.

   Defina um valor de parâmetro de entrada chamando o método `CreateEndpointInfo` do objeto e transmita os seguintes valores:`setInputParameterMapping`

   * Um valor de string que especifica o nome do parâmetro de entrada. Por exemplo, o nome do parâmetro de entrada para o serviço EncryptDocument é `InDoc`.
   * Um valor de string que especifica o tipo de dados do parâmetro de entrada. Por exemplo, o tipo de dados do parâmetro de entrada `InDoc` é `com.adobe.idp.Document`.
   * Um valor de string que especifica o tipo de mapeamento. Por exemplo, você pode especificar `variable`.
   * Um valor de string que especifica o valor do tipo mapping. Por exemplo, você pode especificar &amp;ast;.pdf como padrão de arquivo.

   >[!NOTE]
   >
   >Chame o método `setInputParameterMapping` para cada valor de parâmetro de entrada a ser definido. Como o processo EncryptDocument tem apenas um parâmetro de entrada, é necessário chamar esse método uma vez.

1. Defina um valor de parâmetro de saída.

   Defina um valor de parâmetro de saída chamando o método `CreateEndpointInfo` do objeto e transmita os seguintes valores:`setOutputParameterMapping`

   * Um valor de string que especifica o nome do parâmetro de saída. Por exemplo, o nome do parâmetro de saída para o serviço EncryptDocument é `SecuredDoc`.
   * Um valor de string que especifica o tipo de dados do parâmetro de saída. Por exemplo, o tipo de dados do parâmetro de saída `SecuredDoc` é `com.adobe.idp.Document`.
   * Um valor de string que especifica o tipo de mapeamento. Por exemplo, você pode especificar `%F.pdf`.

1. Crie um ponto de extremidade de Pasta assistida.

   Crie o ponto de extremidade chamando o método `EndpointRegistryClient` do objeto `createEndpoint` e transmitindo o objeto `CreateEndpointInfo`. Esse método retorna um objeto `Endpoint` que representa o ponto de extremidade da Pasta assistida.

1. Habilite o endpoint .

   Ative o endpoint chamando o método `EndpointRegistryClient` do objeto `enable` e transmitindo o objeto `Endpoint` retornado pelo método `createEndpoint`.

**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Adicionar um endpoint de pasta assistida usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Arquivos constantes de valores de configuração de pasta monitorados {#watched-folder-configuration-values-constant-file}

O [Início Rápido: A adição de um endpoint de Pasta assistida usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) usa um arquivo constante que deve fazer parte do seu projeto Java para compilar o início rápido. Esse arquivo constante representa valores de configuração que devem ser definidos ao adicionar um ponto de extremidade de Pasta assistida. O código Java a seguir representa o arquivo constante.

```java
 /**
     * This class contains constants that can be used when setting Watched Folder
     * configuration values
     */

 public final class WatchedFolderEndpointConfigConstants {

         public static final String PROPERTY_FILEPROVIDER_URL = "url";
         public static final String PROPERTY_PROPERTY_ASYNCHRONOUS = "asynchronous";
         public static final String PROPERTY_CRON_EXPRESSION = "cronExpression";
         public static final String PROPERTY_PURGE_DURATION = "purgeDuration";
         public static final String PROPERTY_REPEAT_INTERVAL = "repeatInterval";
         public static final String PROPERTY_REPEAT_COUNT = "repeatCount";
         public static final String PROPERTY_THROTTLE = "throttleOn";
         public static final String PROPERTY_USERNAMER = "userName";
         public static final String PROPERTY_DOMAINNAME = "domainName";
         public static final String PROPERTY_FILEPROVIDER_BATCH_SIZE = "batchSize";
         public static final String PROPERTY_FILEPROVIDER_WAIT_TIME = "waitTime";
         public static final String PROPERTY_EXCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_INCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_FILEPROVIDER_RESULT_FOLDER_NAME =  "resultFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_FOLDER_NAME = "preserveFolderName";
         public static final String PROPERTY_FILEPROVIDER_FAILURE_FOLDER_NAME = "failureFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_ON_FAILURE = "preserveOnFailure";
         public static final String PROPERTY_FILEPROVIDER_OVERWRITE_DUPLICATE_FILENAME = "overwriteDuplicateFilename";
        }
```

## Adicionar pontos de extremidade de email {#adding-email-endpoints}

Você pode adicionar um endpoint de email a um serviço de maneira programática usando a API do AEM Forms Java. Ao adicionar um ponto de extremidade de email, os usuários podem enviar uma mensagem de email com um ou mais anexos de arquivo para uma conta de email especificada. Em seguida, a operação de configuração de serviço é invocada e manipula os arquivos. Depois que o serviço executa a operação especificada, ele envia uma mensagem de email para o remetente com os arquivos modificados como anexos de arquivo.

Para fins de adicionar programaticamente um ponto de extremidade de email a um serviço, considere o seguinte processo de curta duração chamado *MyApplication\EncryptDocument*. Para obter informações sobre processos de duração curta, consulte [Entendendo os processos do AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).

![ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

Esse processo aceita um documento PDF não seguro como um valor de entrada e, em seguida, passa o documento PDF não seguro para a operação `EncryptPDFUsingPassword` do serviço de criptografia. Esse processo criptografa o documento PDF com uma senha e retorna o documento PDF criptografado por senha como o valor de saída. O nome do valor de entrada (o documento PDF não seguro) é `InDoc` e o tipo de dados é `com.adobe.idp.Document`. O nome do valor de saída (o documento PDF criptografado por senha) é `SecuredDoc` e o tipo de dados é `com.adobe.idp.Document`.

>[!NOTE]
>
>Não é possível adicionar um ponto de extremidade de email usando serviços da Web.

### Resumo das etapas {#summary_of_steps-3}

Para adicionar um terminal Email a um serviço, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto `EndpointRegistryClient`.
1. Defina os atributos do ponto de extremidade de email.
1. Especifique os valores de configuração.
1. Defina os valores dos parâmetros de entrada.
1. Defina um valor de parâmetro de saída.
1. Crie o endpoint de email .
1. Habilite o endpoint .

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de cliente EndpointRegistry**

Antes de poder adicionar um ponto de extremidade de email programaticamente, você deve criar um objeto `EndpointRegistryClient`.

**Definir atributos de ponto de extremidade de email**

Para criar um ponto de extremidade de email para um serviço, especifique os seguintes valores:

* **Valor** do identificador do conector: Especifica o tipo de ponto de extremidade criado. Para criar um ponto de extremidade de email, especifique `Email`.
* **Descrição**: Especifica uma descrição para o ponto de extremidade.
* **Nome**: Especifica o nome do ponto de extremidade.
* **Valor** do identificador de serviço: Especifica o serviço ao qual o ponto de extremidade pertence. Por exemplo, para adicionar um endpoint de email ao processo que é introduzido nesta seção (um processo se torna um serviço quando ativado usando o Workbench), especifique `EncryptDocument`.
* **Nome** da operação: Especifica o nome da operação que é invocada usando o ponto de extremidade. Normalmente, ao criar um endpoint de email para um serviço que se originou de um processo criado no Workbench, o nome da operação é `invoke`.

**Especificar valores de configuração**

Você deve especificar valores de configuração para um endpoint de email ao adicionar programaticamente um endpoint de email a um serviço. Esses valores de configuração são especificados por um administrador se um endpoint de email for adicionado usando o console de administração.

>[!NOTE]
>
>A conta de email monitorada é uma conta especial usada somente para o endpoint de email . Esta conta não é uma conta de email normal do usuário. A conta de email de um usuário comum não deve ser configurada como a conta que o Provedor de email usa, pois o Provedor de email exclui mensagens de email da caixa de entrada após sua conclusão com as mensagens.

Os seguintes valores de configuração são definidos ao adicionar programaticamente um ponto de extremidade de email a um serviço:

* **cronExpression**: Uma expressão cron se o email tiver de ser agendado usando uma expressão cron.
* **repeatCount**: Número de vezes que o ponto de extremidade do email verifica a pasta ou o diretório. Um valor de -1 indica varredura indefinida. O valor padrão é -1.
* **repeatInterval**: A taxa de varredura em segundos que o receptor usa para verificar emails recebidos. O valor padrão é 10.
* **startDelay**: O tempo de espera para a verificação após o agendador ser iniciado. O tempo padrão é 0.
* **batchSize**: O número de mensagens de email que o receptor processa por verificação para obter desempenho ideal. Um valor de -1 indica todos os emails. O valor padrão é 2.
* **userName**: O nome de usuário usado ao invocar um serviço de destino a partir de email. O valor padrão é `SuperAdmin`.
* **domainName**: Um valor de configuração obrigatório. O valor padrão é `DefaultDom`.
* **domainPattern**: Especifica os padrões de domínio do email de entrada que o provedor aceita. Por exemplo, se `adobe.com` for usado, somente o email do adobe.com será processado, o email de outros domínios será ignorado.
* **filePattern**: Especifica os padrões de anexo de arquivo de entrada aceitos pelo provedor. Isso inclui arquivos com extensões de nome de arquivo específicas (&amp;ast;.dat, &amp;ast;.xml), arquivos com nomes específicos (dados) e arquivos com expressões compostas no nome e na extensão (&amp;ast;.[dD][aA]&#39;port&#39;). O valor padrão é `*`.
* **recipientSuccessfulJob**: Um endereço de email para o qual as mensagens são enviadas para indicar trabalhos bem-sucedidos. Por padrão, uma mensagem de trabalho bem-sucedida é sempre enviada ao remetente. Se você digitar `sender`, os resultados do email serão enviados ao remetente. Há suporte para até 100 recipients. Especifique recipients adicionais com endereços de email, cada um separado por vírgula. Para desativar essa opção, deixe esse valor em branco. Em alguns casos, talvez você queira acionar um processo e não desejar uma notificação por email do resultado. O valor padrão é `sender`.
* **recipientFailedJob**: Um endereço de email para o qual são enviadas mensagens para indicar tarefas com falha. Por padrão, uma mensagem de trabalho com falha é sempre enviada ao remetente. Se você digitar `sender`, os resultados do email serão enviados ao remetente. Há suporte para até 100 recipients. Especifique recipients adicionais com endereços de email, cada um separado por vírgula. Para desativar essa opção, deixe esse valor em branco. O valor padrão é `sender`.
* **inboxHost**: O nome do host da caixa de entrada ou o endereço IP do provedor de email a ser verificado.
* **inboxPort**: A porta que o servidor de email usa. O valor padrão para POP3 é 110 e o valor padrão para IMAP é 143. Se SSL estiver ativado, o valor padrão para POP3 é 995 e o valor padrão para IMAP é 993.
* **inboxProtocol**: O protocolo de email do endpoint de email a ser usado para verificar a caixa de entrada. As opções são `IMAP` ou `POP3`. O servidor de correio do host da caixa de entrada deve oferecer suporte a esses protocolos.
* **inboxTimeOut**: Tempo limite em segundos para que o provedor de email aguarde as respostas da caixa de entrada. O valor padrão é 60.
* **inboxUser**: O nome de usuário necessário para fazer logon na conta de email. Dependendo do servidor de email e da configuração, essa pode ser apenas a parte do nome do usuário do email ou pode ser o endereço de email completo.
* **inboxPassword**: A senha do usuário da caixa de entrada.
* **inboxSSLEnabled**: Defina esse valor para forçar o provedor de email a usar SSL ao enviar mensagens de notificação de resultados ou erros. Verifique se o host IMAP ou POP3 suporta SSL.
* **smtpHost**: O nome do host do servidor de email para o qual o provedor de email envia resultados e mensagens de erro.
* **smtpPort**: O valor padrão da porta SMTP é 25.
* **smtpUser**: A conta de usuário que o provedor de email deve usar ao enviar notificações por email de resultados e erros.
* **smtpPassword**: A senha da conta SMTP. Alguns servidores de email não exigem uma senha SMTP.
* **charSet**: O conjunto de caracteres usado pelo provedor de email. O valor padrão é `UTF-8`.
* **smtpSSLEnabled**: Defina esse valor para forçar o provedor de email a usar SSL ao enviar mensagens de notificação de resultados ou erros. Certifique-se de que o Host SMTP seja compatível com SSL.
* **failedJobFolder**: Especifica um diretório no qual armazenar resultados quando o servidor de email SMTP não estiver operacional.
* **assíncrono**: Quando definido como síncrono, todos os documentos de entrada são processados e uma única resposta é retornada. Quando definido como assíncrono, uma resposta será enviada para cada documento de entrada processado. Por exemplo, um endpoint de email é criado para o processo introduzido neste tópico e uma mensagem de email é enviada para a caixa de entrada do endpoint que contém vários documentos PDF não seguros. Quando todos os documentos PDF são criptografados com uma senha e se o ponto de extremidade for configurado como síncrono, uma única mensagem de email de resposta é enviada com todos os documentos PDF protegidos anexados. Se o endpoint estiver configurado como assíncrono, uma mensagem de email de resposta separada será enviada para cada documento PDF seguro. Cada mensagem de email contém um único documento PDF como anexo. O valor padrão é assíncrono.

**Definir valores de parâmetros de entrada**

Ao criar um ponto de extremidade de email, você deve definir os valores do parâmetro de entrada. Ou seja, você deve descrever os valores de entrada passados para a operação que é invocada pelo endpoint de email . Por exemplo, considere o processo introduzido neste tópico. Ele tem um valor de entrada chamado `InDoc` e seu tipo de dados é `com.adobe.idp.Document`. Ao criar um endpoint de email para esse processo (depois que um processo é ativado, ele se torna um serviço), é necessário definir o valor do parâmetro de entrada.

Para definir valores de parâmetros de entrada necessários para um ponto de extremidade de email, especifique os seguintes valores:

**Nome** do parâmetro de entrada: O nome do parâmetro de entrada. O nome de um valor de entrada é especificado no Workbench para um processo. Se o valor de entrada pertencer a uma operação de serviço (um serviço Forms que não é um processo criado no Workbench), o nome de entrada será especificado no arquivo component.xml. Por exemplo, o nome do parâmetro de entrada para o processo introduzido nesta seção é `InDoc`.

**Tipo** de mapeamento: Usado para configurar os valores de entrada necessários para chamar a operação de serviço. Dois tipos de mapeamento são os seguintes:

* `Literal`: O endpoint de email usa o valor inserido no campo, conforme ele é exibido. Todos os tipos básicos de Java são suportados. Por exemplo, se uma API usar entrada, como String, long, int e Boolean, a cadeia de caracteres será convertida para o tipo adequado e o serviço será chamado.
* `Variable`: O valor inserido é um padrão de arquivo que o ponto de extremidade de email usa para escolher a entrada. Por exemplo, se você selecionar Variável para o tipo de mapeamento e o documento de entrada precisar ser um arquivo PDF, poderá especificar `*.pdf` como o valor de mapeamento.

**Valor** do mapeamento: Especifica o valor do tipo de mapeamento. Por exemplo, se você selecionar um tipo de mapeamento Variável , poderá especificar `*.pdf` como padrão de arquivo.

**Tipo** de dados: Especifica o tipo de dados dos valores de entrada. Por exemplo, o tipo de dados do valor de entrada do processo introduzido nesta seção é com.adobe.idp.Document.

**Definir um valor de parâmetro de saída**

Ao criar um ponto de extremidade de email, você deve definir um valor de parâmetro de saída. Ou seja, você deve descrever o valor de saída retornado pelo serviço chamado pelo endpoint de email. Por exemplo, considere o processo introduzido neste tópico. Ele tem um valor de saída chamado `SecuredDoc` e seu tipo de dados é `com.adobe.idp.Document`. Ao criar um endpoint de email para esse processo (depois que um processo é ativado, ele se torna um serviço), é necessário definir o valor do parâmetro de saída.

Para definir um valor de parâmetro de saída necessário para um ponto de extremidade de email, especifique os seguintes valores:

**Nome** do parâmetro de saída: O nome do parâmetro de saída. O nome de um valor de saída do processo é especificado no Workbench. Se o valor de saída pertencer a uma operação de serviço (um serviço que não é um processo criado no Workbench), o nome de saída será especificado no arquivo component.xml. Por exemplo, o nome do parâmetro de saída para o processo introduzido nesta seção é `SecuredDoc`.

**Tipo** de mapeamento: Usado para configurar a saída do serviço e da operação. As opções disponíveis são as seguintes:

* Se o serviço retornar um único objeto (um único documento), o padrão será `%F.pdf` e o destino de origem será sourcefilename.pdf. Por exemplo, o processo introduzido nesta seção retorna um único documento. Como resultado, o tipo de mapeamento pode ser definido como `%F.pdf` ( `%F` significa usar o nome de arquivo especificado). O padrão `%E` especifica a extensão do documento de entrada.
* Se o serviço retornar uma lista, o padrão será `Result\%F\`, e o destino de origem será Result\sourcefilename\source1 (output 1) e Result\sourcefilename\source2 (output 2).
* Se o serviço retornar um mapa, o padrão será `Result\%F\` e o destino de origem será Result\sourcefilename\file1 and Result\sourcefilename\file2. Se o mapa tiver mais de um objeto, o padrão será `Result\%F.pdf` e o destino de origem será Result\sourcefilename1.pdf (saída 1), Result\sourcefilenam2.pdf (saída 2) e assim por diante.

**Tipo** de dados: Especifica o tipo de dados do valor de retorno. Por exemplo, o tipo de dados do valor de retorno do processo introduzido nesta seção é `com.adobe.idp.Document`.

**Criar o endpoint de email**

Depois de definir os atributos e os valores de configuração do ponto de extremidade de email e os valores de parâmetro de entrada e saída, é necessário criar o ponto de extremidade de email.

**Ativar o ponto de extremidade**

Depois de criar um ponto de extremidade de email, você deve habilitá-lo. Quando o endpoint está ativado, ele pode ser usado para chamar o serviço. Depois de ativar o endpoint, você pode visualizá-lo no console de administração.

**Consulte também:**

[Adicionar um endpoint de email usando a API do Java](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicione um endpoint de email usando a API do Java {#add-an-email-endpoint-using-the-java-api}

Adicione um endpoint de email usando a API do Java:

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto Cliente EndpointRegistry.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `EndpointRegistryClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Defina os atributos do ponto de extremidade de email.

   * Crie um objeto `CreateEndpointInfo` usando seu construtor.
   * Especifique o valor do identificador do conector, chamando o método `CreateEndpointInfo` do objeto e passando o valor da string `Email`.`setConnectorId`
   * Especifique a descrição do ponto de extremidade chamando o método `CreateEndpointInfo` do objeto `setDescription` e passando um valor de string que descreve o ponto de extremidade.
   * Especifique o nome do ponto final chamando o método `CreateEndpointInfo` do objeto `setName` e passando um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o método `CreateEndpointInfo` do objeto `setServiceId` e passando um valor de string que especifica o nome do serviço.
   * Especifique a operação que é invocada chamando o método `CreateEndpointInfo` do objeto `setOperationName` e passando um valor de string que especifica o nome da operação. Normalmente, ao criar um endpoint de email para um serviço originado de um processo criado no Workbench, o nome da operação é chamado.

1. Especifique os valores de configuração.

   Para cada valor de configuração a ser definido para o ponto de extremidade de email, você deve chamar o método `CreateEndpointInfo` do objeto `setConfigParameterAsText`. Por exemplo, para definir o valor de configuração `smtpHost`, chame o método `CreateEndpointInfo` do objeto `setConfigParameterAsText` e passe os seguintes valores:

   * Um valor de string que especifica o nome do valor de configuração. Ao definir o valor de configuração `smtpHost`, especifique `smtpHost`.
   * Um valor de string que especifica o valor do valor de configuração. Ao definir o valor de configuração `smtpHost`, especifique um valor de string que especifique o nome do servidor SMTP.

   >[!NOTE]
   >
   >Para ver todos os valores de configuração definidos para o serviço EncryptDocument introduzido nesta seção, consulte o exemplo de código Java localizado em [QuickStart: Adicionar um endpoint de email usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api).

1. Defina os valores dos parâmetros de entrada.

   Defina um valor de parâmetro de entrada chamando o método `CreateEndpointInfo` do objeto e transmita os seguintes valores:`setInputParameterMapping`

   * Um valor de string que especifica o nome do parâmetro de entrada. Por exemplo, o nome do parâmetro de entrada para o serviço EncryptDocument é `InDoc`.
   * Um valor de string que especifica o tipo de dados do parâmetro de entrada. Por exemplo, o tipo de dados do parâmetro de entrada `InDoc` é `com.adobe.idp.Document`.
   * Um valor de string que especifica o tipo de mapeamento. Por exemplo, você pode especificar `variable`.
   * Um valor de string que especifica o valor do tipo mapping. Por exemplo, você pode especificar &amp;ast;.pdf como padrão de arquivo.

   >[!NOTE]
   >
   >Chame o método `setInputParameterMapping` para cada valor de parâmetro de entrada a ser definido. Como o processo EncryptDocument tem apenas um parâmetro de entrada, é necessário chamar esse método uma vez.

1. Defina um valor de parâmetro de saída.

   Defina um valor de parâmetro de saída chamando o método `CreateEndpointInfo` do objeto `setOutputParameterMapping` e passando os seguintes valores:

   * Um valor de string que especifica o nome do parâmetro de saída. Por exemplo, o nome do parâmetro de saída para o serviço EncryptDocument é `SecuredDoc`.
   * Um valor de string que especifica o tipo de dados do parâmetro de saída. Por exemplo, o tipo de dados do parâmetro de saída `SecuredDoc` é `com.adobe.idp.Document`.
   * Um valor de string que especifica o tipo de mapeamento. Por exemplo, você pode especificar `%F.pdf`.

1. Crie o endpoint de email .

   Crie o ponto de extremidade chamando o método `EndpointRegistryClient` do objeto `createEndpoint` e transmitindo o objeto `CreateEndpointInfo`. Esse método retorna um objeto `Endpoint` que representa o ponto de extremidade de email.

1. Habilite o endpoint .

   Ative o endpoint chamando o método `EndpointRegistryClient` do objeto `enable` e transmitindo o objeto `Endpoint` retornado pelo método `createEndpoint`.

**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Adicionar um endpoint de pasta assistida usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Arquivo constante de valores de configuração de email {#email-configuration-values-constant-file}

O [Início Rápido: Adicionar um terminal de email usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) usa um arquivo constante que deve fazer parte do seu projeto Java para compilar o início rápido. Esse arquivo constante representa valores de configuração que devem ser definidos ao adicionar um ponto de extremidade de email. O código Java a seguir representa o arquivo constante.

```java
 /**
     * This class contains constants that can be used when setting email endpoint
     * configuration values
     */
 public class EmailEndpointConfigConstants {

     public static final String PROPERTY_EMAILPROVIDER_CRON_EXPRESSION = "cronExpression";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_COUNT = "repeatCount";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_INTERVAL = "repeatInterval";
     public static final String PROPERTY_EMAILPROVIDER_START_DELAY = "startDelay";
     public static final String PROPERTY_EMAILPROVIDER_BATCH_SIZE = "batchSize";
     public static final String PROPERTY_EMAILPROVIDER_USERNAME = "userName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINNAME = "domainName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINPATTERN = "domainPattern";
     public static final String PROPERTY_EMAILPROVIDER_FILEPATTERN = "filePattern";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_SUCCESSFUL_JOB = "recipientSuccessfulJob";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_FAILED_JOB = "recipientFailedJob";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_HOST = "inboxHost";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PORT = "inboxPort";
     public static final String PROPERTY_EMAILPROVIDER_PROTOCOL = "inboxProtocol";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_TIMEOUT = "inboxTimeOut";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_USER = "inboxUser";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PASSWORD = "inboxPassword";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_SSL = "inboxSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_HOST = "smtpHost";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PORT = "smtpPort";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_USER = "smtpUser";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PASSWORD = "smtpPassword";
     public static final String PROPERTY_EMAILPROVIDER_CHARSET = "charSet";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_SSL = "smtpSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_FAILED_FOLDER = "failedJobFolder";
     public static final String PROPERTY_EMAILPROVIDER_ASYNCHRONOUS = "asynchronous";
 }
```

## Adicionar pontos finais remotos {#adding-remoting-endpoints}

>[!NOTE]
>
>APIs do LiveCycle Remoting obsoletas para formulários AEM no JEE.

Você pode adicionar um terminal Remoting programaticamente a um serviço usando a API Java do AEM Forms. Ao adicionar um terminal Remoting, você está permitindo que um aplicativo Flex chame o serviço usando o remoting. (Consulte [Invocar o AEM Forms usando (obsoleto para formulários AEM) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

Para fins de adicionar programaticamente um terminal Remoting a um serviço, considere o seguinte processo de curta duração chamado *EncryptDocument*.

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

Esse processo aceita um documento PDF não seguro como um valor de entrada e, em seguida, passa o documento PDF não seguro para a operação `EncryptPDFUsingPassword` do serviço de criptografia. O documento PDF é criptografado com uma senha e o documento PDF criptografado por senha é o valor de saída desse processo. O nome do valor de entrada (o documento PDF não seguro) é `InDoc` e o tipo de dados é `com.adobe.idp.Document`. O nome do valor de saída (o documento PDF criptografado por senha) é `SecuredDoc` e o tipo de dados é `com.adobe.idp.Document`.

Para demonstrar como adicionar um terminal Remoting a um serviço, esta seção adiciona um terminal Remoting a um serviço chamado EncryptDocument.

>[!NOTE]
>
>Não é possível adicionar um terminal Remoting usando os serviços da Web.

### Resumo das etapas {#summary_of_steps-4}

Para remover um terminal de um serviço, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto `EndpointRegistryClient`.
1. Defina os atributos do ponto de extremidade remoto.
1. Crie um terminal Remoting .
1. Habilite o endpoint .

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de cliente EndpointRegistry**

Para adicionar um terminal Remoting programaticamente, você deve criar um objeto `EndpointRegistryClient`.

**Definir atributos de ponto de extremidade remoto**

Para criar um terminal Remoting para um serviço, especifique os seguintes valores:

* **Valor** do identificador do conector: Especifica o tipo de ponto de extremidade criado. Para criar um terminal Remoting , especifique `Remoting`.
* **Descrição**: Especifica a descrição do ponto de extremidade.
* **Nome**: Especifica o nome do ponto de extremidade.
* **Valor** do identificador de serviço: Especifica o serviço ao qual o ponto de extremidade pertence. Por exemplo, para adicionar um ponto de extremidade Remoto ao processo que é introduzido nesta seção (um processo se torna um serviço quando é ativado no Workbench), especifique `EncryptDocument`.
* **Nome** da operação: Especifica o nome da operação que é invocada usando o ponto de extremidade. Ao criar um terminal Remoting, especifique um caractere curinga (&amp;ast;).

**Criar um terminal Remoting**

Depois de definir os atributos de ponto de extremidade Remota, você pode criar um ponto de extremidade Remota para um serviço.

**Ativar o ponto de extremidade**

Depois de criar um novo terminal, você deve habilitá-lo. Quando um terminal Remoting é ativado, ele permite que um cliente Flex chame o serviço.

**Consulte também:**

[Adicionar um terminal Remoting usando a API Java](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicione um terminal Remoting usando a API Java {#add-a-remoting-endpoint-using-the-java-api}

Adicione um terminal Remoting usando a API Java:

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto Cliente EndpointRegistry.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `EndpointRegistryClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Defina os atributos do ponto de extremidade remoto.

   * Crie um objeto `CreateEndpointInfo` usando seu construtor.
   * Especifique o valor do identificador do conector, chamando o método `CreateEndpointInfo` do objeto e passando o valor da string `Remoting`.`setConnectorId`
   * Especifique a descrição do ponto de extremidade chamando o método `CreateEndpointInfo` do objeto `setDescription` e passando um valor de string que descreve o ponto de extremidade.
   * Especifique o nome do ponto final chamando o método `CreateEndpointInfo` do objeto `setName` e passando um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o método `CreateEndpointInfo` do objeto `setServiceId` e passando um valor de string que especifica o nome do serviço.
   * Especifique a operação que é invocada pelo método `CreateEndpointInfo` do objeto e transmita um valor de string que especifica o nome da operação. `setOperationName` Para um terminal Remoting, especifique um caractere curinga (&amp;ast;).

1. Crie um terminal Remoting .

   Crie o ponto de extremidade chamando o método `EndpointRegistryClient` do objeto `createEndpoint` e transmitindo o objeto `CreateEndpointInfo`. Esse método retorna um objeto `Endpoint` que representa o novo ponto de extremidade Remota.

1. Habilite o endpoint .

   Ative o endpoint chamando o método `EndpointRegistryClient` do objeto `enable` e transmitindo o objeto `Endpoint` retornado pelo método `createEndpoint`.

**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Adicionar um terminal Remoting usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Adicionar pontos de extremidade do TaskManager {#adding-taskmanager-endpoints}

Você pode adicionar programaticamente um terminal TaskManager a um serviço usando a API Java do AEM Forms. Ao adicionar um ponto de extremidade do TaskManager a um serviço, você permite que um usuário do Workspace chame o serviço. Ou seja, um usuário que trabalha no Workspace pode chamar um processo que tem um ponto de extremidade do TaskManager correspondente.

>[!NOTE]
>
>Não é possível adicionar um ponto de extremidade do TaskManager usando serviços da Web.

### Resumo das etapas {#summary_of_steps-5}

Para adicionar um ponto de extremidade do TaskManager a um serviço, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto `EndpointRegistryClient`.
1. Crie uma categoria para o endpoint .
1. Defina os atributos do ponto de extremidade do TaskManager.
1. Crie um ponto de extremidade do TaskManager.
1. Habilite o endpoint .

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de cliente EndpointRegistry**

Antes de poder adicionar programaticamente um ponto de extremidade do TaskManager, você deve criar um objeto `EndpointRegistryClient`.

**Criar uma categoria para o endpoint**

As categorias são usadas para organizar serviços no Workspace. Ou seja, um usuário do Workspace pode chamar um serviço que tem um terminal TaskManager selecionando uma categoria no Workspace. Ao criar um ponto de extremidade do TaskManager, você pode fazer referência a uma categoria existente ou criar programaticamente uma nova categoria.

>[!NOTE]
>
>Esta seção cria uma nova categoria como parte da adição de um ponto de extremidade do TaskManager a um serviço.

**Definir atributos de ponto de extremidade do TaskManager**

Para criar um ponto de extremidade do TaskManager para um serviço, especifique os seguintes valores:

* **Identificador** do conector: Especifica o tipo de ponto de extremidade criado. Para criar um ponto de extremidade do TaskManager, especifique `TaskManagerConnector`.
* **Descrição**: Especifica a descrição do ponto de extremidade.
* **Nome**: Especifica o nome do ponto de extremidade.
* **Identificador** de serviço: Especifica o serviço ao qual o ponto de extremidade pertence.
* **Categoria**: Especifica um valor de identificador de categoria associado ao ponto de extremidade do TaskManager.
* **Nome** da operação: Geralmente, ao criar um terminal do TaskManager para um serviço originado de um processo criado no Workbench, o nome da operação é  `invoke`.

**Criar um ponto de extremidade do Gerenciador de Tarefas**

Depois de definir atributos de ponto de extremidade do TaskManager, você pode criar um ponto de extremidade do TaskManager para um serviço.

**Ativar o ponto de extremidade**

Depois de criar um novo terminal, você deve habilitá-lo. Quando o endpoint está ativado, ele pode ser usado para chamar o serviço de dentro do Workspace. Depois de ativar o endpoint, você pode visualizá-lo no console de administração.

**Consulte também:**

[Adicionar um ponto de extremidade do TaskManager usando a API do Java](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicionar um ponto de extremidade do TaskManager usando a API Java {#add-a-taskmanager-endpoint-using-the-java-api}

Adicione um ponto de extremidade do TaskManager usando a API do Java:

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto Cliente EndpointRegistry.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `EndpointRegistryClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Crie uma categoria para o endpoint .

   * Crie um objeto `CreateEndpointCategoryInfo` usando seu construtor e transmitindo os seguintes valores:

      * Um valor de string que especifica o valor identificador da categoria
      * Um valor da string que especifica a descrição da categoria
   * Crie a categoria chamando o método `EndpointRegistryClient` do objeto `createEndpointCategory` e transmitindo o objeto `CreateEndpointCategoryInfo`. Este método retorna um objeto `EndpointCategory` que representa a nova categoria.


1. Defina os atributos do ponto de extremidade do TaskManager.

   * Crie um objeto `CreateEndpointInfo` usando seu construtor.
   * Especifique o valor do identificador do conector, chamando o método `CreateEndpointInfo` do objeto e passando o valor da string `TaskManagerConnector`.`setConnectorId`
   * Especifique a descrição do ponto de extremidade chamando o método `CreateEndpointInfo` do objeto `setDescription` e passando um valor de string que descreve o ponto de extremidade.
   * Especifique o nome do ponto final chamando o método `CreateEndpointInfo` do objeto `setName` e passando um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o método `CreateEndpointInfo` do objeto `setServiceId` e passando um valor de string que especifica o nome do serviço.
   * Especifique a categoria à qual o ponto de extremidade pertence, chamando o método `CreateEndpointInfo` do objeto `setCategoryId` e passando um valor de string que especifica o valor do identificador de categoria. Você pode chamar o método `EndpointCategory` do objeto `getId` para obter o valor identificador desta categoria.
   * Especifique a operação que é invocada chamando o método `CreateEndpointInfo` do objeto `setOperationName` e passando um valor de string que especifica o nome da operação. Normalmente, ao criar um terminal `TaskManager` para um serviço originado de um processo criado no Workbench, o nome da operação é `invoke`.

1. Crie um ponto de extremidade do TaskManager.

   Crie o ponto de extremidade chamando o método `EndpointRegistryClient` do objeto `createEndpoint` e transmitindo o objeto `CreateEndpointInfo`. Este método retorna um objeto `Endpoint` que representa o novo ponto de extremidade do TaskManager.

1. Habilite o endpoint .

   Ative o endpoint chamando o método `EndpointRegistryClient` do objeto `enable` e transmitindo o objeto `Endpoint` retornado pelo método `createEndpoint`.

**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Adicionar um ponto de extremidade do TaskManager usando a API do Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Modificando Endpoints {#modifying-endpoints}

Você pode modificar programaticamente um terminal existente usando a API do AEM Forms Java. Ao modificar um endpoint, é possível alterar o comportamento do endpoint. Considere, por exemplo, um endpoint de Pasta assistida que especifica uma pasta que é usada como a pasta assistida. Você pode modificar programaticamente os valores de configuração que pertencem ao endpoint Pasta assistida, resultando em outra pasta funcionando como a pasta assistida. Para obter informações sobre os valores de configuração que pertencem a um endpoint de Pasta assistida, consulte [Adicionar endpoints de pasta monitorada](programmatically-endpoints.md#adding-watched-folder-endpoints).

Para demonstrar como modificar um endpoint, esta seção modifica um endpoint de Pasta assistida alterando a pasta que se comporta como a pasta assistida.

>[!NOTE]
>
>Não é possível modificar um terminal usando serviços da Web.

### Resumo das etapas {#summary_of_steps-6}

Para modificar um endpoint, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto `EndpointRegistryClient`.
1. Recupere o terminal.
1. Especifique novos valores de configuração.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de cliente EndpointRegistry**

Para modificar programaticamente um ponto de extremidade, você deve criar um objeto `EndpointRegistryClient`.

**Recuperar o ponto de extremidade para modificar**

Antes de poder modificar um endpoint, você deve recuperá-lo. Para recuperar um terminal, você deve se conectar como um usuário que pode acessar um terminal. É recomendável conectar-se como um administrador. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

Você pode recuperar um ponto de extremidade recuperando uma lista de pontos de extremidade. Em seguida, você pode iterar pela lista, procurando pelo endpoint específico a ser removido. Por exemplo, você pode localizar um ponto de extremidade determinando o serviço que corresponde ao ponto de extremidade e o tipo de ponto de extremidade. Ao localizar o ponto de extremidade, você pode modificá-lo.

**Especificar novos valores de configuração**

Ao modificar um ponto de extremidade, especifique novos valores de configuração. Por exemplo, para modificar um endpoint de Pasta assistida, redefina todos os valores de configuração do endpoint de Pasta assistida, não apenas os que você deseja modificar. Para obter informações sobre os valores de configuração que pertencem a um endpoint de Pasta assistida, consulte [Adicionar endpoints de pasta monitorada](programmatically-endpoints.md#adding-watched-folder-endpoints).

>[!NOTE]
>
>Para obter informações sobre valores de configuração que pertencem a um ponto de extremidade de email, consulte [Adicionar pontos de extremidade de email](programmatically-endpoints.md#adding-email-endpoints).

>[!NOTE]
>
>Não é possível modificar o serviço chamado pelo endpoint. Se você tentar modificar o serviço, uma exceção será lançada. Para modificar o serviço associado a um determinado terminal, remova o terminal e crie um novo. (Consulte [Removendo Endpoints](programmatically-endpoints.md#removing-endpoints).)

**Consulte também:**

[Modificação de um terminal usando a API do Java](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Modificação de um terminal usando a API Java {#modifying-an-endpoint-using-the-java-api}

Modifique um terminal usando a API do Java:

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto Cliente EndpointRegistry.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `EndpointRegistryClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recupere o terminal para modificar.

   * Recupere uma lista de todos os endpoints aos quais o usuário atual (especificado nas propriedades de conexão) pode acessar chamando o método `EndpointRegistryClient` do objeto `getEndpoints` e transmitindo um objeto `PagingFilter` que atue como filtro. Você pode passar um valor `(PagingFilter)null` para retornar todos os pontos finais. Este método retorna um objeto `java.util.List` em que cada elemento é um objeto `Endpoint`. Para obter informações sobre um objeto `PagingFilter`, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Itere pelo objeto `java.util.List` para determinar se ele tem endpoints. Se houver pontos de extremidade, cada elemento é uma instância `EndPoint`.
   * Determine o serviço que corresponde a um ponto de extremidade chamando o método `EndPoint` `getServiceId` do objeto. Esse método retorna um valor de string que especifica o nome do serviço.
   * Determine o tipo de ponto de extremidade chamando o método `EndPoint` do objeto `getConnectorId`. Esse método retorna um valor de string que especifica o tipo de endpoint. Por exemplo, se o ponto de extremidade for um ponto de extremidade de Pasta assistida, esse método retornará `WatchedFolder`.

1. Especifique novos valores de configuração.

   * Crie um objeto `ModifyEndpointInfo` chamando seu construtor.
   * Para cada valor de configuração a ser definido, chame o método `ModifyEndpointInfo` do objeto `setConfigParameterAsText`. Por exemplo, para definir o valor de configuração de url, chame o método `ModifyEndpointInfo` do objeto e passe os seguintes valores:`setConfigParameterAsText`

      * Um valor de string que especifica o nome do valor de configuração. Por exemplo, para definir o valor de configuração `url`, especifique `url`.
      * Um valor de string que especifica o valor do valor de configuração. Para definir um valor para o valor de configuração `url`, especifique o local da pasta monitorada.
   * Chame o método `EndpointRegistryClient` do objeto `modifyEndpoint` e passe o objeto `ModifyEndpointInfo`.


**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Modificação de um terminal usando a API do Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Removendo pontos de extremidade {#removing-endpoints}

Você pode remover programaticamente um terminal de um serviço usando a API Java do AEM Forms. Após remover um ponto de extremidade, o serviço não poderá ser chamado usando o método de invocação que o ponto de extremidade ativou. Por exemplo, se você remover um terminal SOAP de um serviço, não poderá chamar o serviço usando o modo SOAP.

Para demonstrar como remover um ponto de extremidade de um serviço, esta seção remove um ponto de extremidade EJB de um serviço chamado *EncryptDocument*.

>[!NOTE]
>
>Não é possível remover um terminal usando serviços da Web.

### Resumo das etapas {#summary_of_steps-7}

Para remover um terminal de um serviço, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto `EndpointRegistryClient`.
1. Recupere o terminal.
1. Remova o ponto de extremidade.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de cliente EndpointRegistry**

Para remover um endpoint programaticamente, você deve criar um objeto `EndpointRegistryClient` .

**Recuperar o ponto de extremidade para remover**

Antes de remover um terminal, é necessário recuperá-lo. Para recuperar um terminal, você deve se conectar como um usuário que pode acessar um terminal. É recomendável conectar-se como um administrador. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

Você pode recuperar um ponto de extremidade recuperando uma lista de pontos de extremidade. Em seguida, você pode iterar pela lista, procurando pelo endpoint específico a ser removido. Por exemplo, você pode localizar um ponto de extremidade determinando o serviço que corresponde ao ponto de extremidade e o tipo de ponto de extremidade. Ao localizar o ponto de extremidade, você pode removê-lo.

**Remover o ponto de extremidade**

Depois de criar um novo terminal, você deve habilitá-lo. Quando o endpoint está ativado, ele pode ser usado para chamar o serviço. Depois de ativar o endpoint, você pode visualizá-lo no console de administração.

**Consulte também:**

[Remoção de um terminal usando a API do Java](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Remoção de um endpoint usando a API Java {#removing-an-endpoint-using-the-java-api}

Remova um terminal usando a API do Java:

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto Cliente EndpointRegistry.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `EndpointRegistryClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recupere o ponto de extremidade a ser removido.

   * Recupere uma lista de todos os endpoints aos quais o usuário atual (especificado nas propriedades de conexão) tem acesso, chamando o método `EndpointRegistryClient` do objeto `getEndpoints` e transmitindo um objeto `PagingFilter` que atue como filtro. Você pode passar `(PagingFilter)null` para retornar todos os pontos de extremidade. Este método retorna um objeto `java.util.List` em que cada elemento é um objeto `Endpoint`.
   * Itere pelo objeto `java.util.List` para determinar se ele tem endpoints. Se houver pontos de extremidade, cada elemento é uma instância `EndPoint`.
   * Determine o serviço que corresponde a um ponto de extremidade chamando o método `EndPoint` `getServiceId` do objeto. Esse método retorna um valor de string que especifica o nome do serviço.
   * Determine o tipo de ponto de extremidade chamando o método `EndPoint` do objeto `getConnectorId`. Esse método retorna um valor de string que especifica o tipo de endpoint. Por exemplo, se o ponto de extremidade for um ponto de extremidade EJB, esse método retornará `EJB`.

1. Remova o ponto de extremidade.

   Remova o ponto de extremidade chamando o método `EndpointRegistryClient` do objeto `remove` e passando o objeto `EndPoint` que representa o ponto de extremidade a ser removido.

**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Remoção de um terminal usando a API do Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Recuperando informações do conector de terminal {#retrieving-endpoint-connector-information}

Você pode recuperar programaticamente informações sobre conectores de ponto de extremidade usando a API do AEM Forms. Um conector permite que um endpoint chame um serviço usando vários métodos de invocação. Por exemplo, um conector de Pasta assistida permite que um terminal chame um serviço usando pastas assistidas. Ao recuperar programaticamente informações sobre conectores de ponto de extremidade, é possível recuperar valores de configuração associados a um conector, como quais valores de configuração são necessários e quais são opcionais.

Para demonstrar como recuperar informações sobre conectores de endpoint, esta seção recupera informações sobre um conector de Pasta assistida. (Consulte [Adicionar pontos de extremidade de pasta assistida](programmatically-endpoints.md#adding-watched-folder-endpoints).)

>[!NOTE]
>
>Não é possível recuperar informações sobre endpoints usando serviços da Web.

>[!NOTE]
>
>Este tópico usa a API `ConnectorRegistryClient` para recuperar informações sobre conectores de ponto de extremidade. (Consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

### Resumo das etapas {#summary_of_steps-8}

Para recuperar informações do conector do ponto de extremidade, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto `ConnectorRegistryClient`.
1. Especifique o tipo de conector.
1. Recupere os valores de configuração.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

Se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, substitua adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado. Para obter informações sobre a localização de todos os arquivos AEM Forms JAR, consulte [Incluindo arquivos da biblioteca AEM Forms Java](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de cliente ConnectorRegistry**

Para recuperar programaticamente as informações do conector do ponto de extremidade, crie um objeto `ConnectorRegistryClient`.

**Especificar o tipo de conector**

Especifique o tipo de conector do qual recuperar informações. Os seguintes tipos de conectores existem:

* **EJB**: Permite que um aplicativo cliente chame um serviço usando o modo EJB.
* **SOAP**: Permite que um aplicativo cliente chame um serviço usando o modo SOAP.
* **Pasta** assistida: Permite que as pastas assistidas chamem um serviço.
* **Email**: Permite que mensagens de email chamem um serviço.
* **Remoção**: Permite que um aplicativo cliente Flex chame um serviço.
* **Conector** do GerenciadorTarefa: Permite que um usuário do Workspace chame um serviço do Workspace.

**Recuperar valores de configuração**

Depois de especificar o tipo de conector, é possível recuperar informações sobre o conector, como o valor de configuração suportado. Por exemplo, para qualquer conector, você pode determinar quais valores de configuração são necessários e quais são opcionais.

**Consulte também:**

[Recuperar informações do conector do ponto de extremidade usando a API Java](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recupere informações do conector do ponto de extremidade usando a API Java {#retrieve-endpoint-connector-information-using-the-java-api}

Recupere informações do conector do ponto de extremidade usando a API Java:

1. Inclua arquivos de projeto. .

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto Cliente ConnectorRegistry.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `ConnectorRegistryClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Especifique o tipo de conector.

   Especifique o tipo de conector chamando o método `ConnectorRegistryClient` do objeto e passando um valor de string que especifica o tipo de conector. `getEndpointDefinition` Por exemplo, para especificar o tipo de conector de Pasta assistida, passe o valor da string `WatchedFolder`. Esse método retorna um objeto `Endpoint` que corresponde ao tipo de conector.

1. Recupere os valores de configuração.

   * Recupere os valores de configuração associados a esse ponto de extremidade, chamando o método `Endpoint` `getConfigParameters` do objeto. Esse método retorna uma matriz de objetos `ConfigParameter`.
   * Recupere informações sobre cada valor de configuração recuperando cada elemento dentro da matriz. Cada elemento é um objeto `ConfigParameter` . Você pode, por exemplo, determinar se o valor de configuração é obrigatório ou opcional, chamando o método `ConfigParameter` do objeto `isRequired`. Se o valor de configuração for necessário, esse método retornará `true`.

**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Recuperação de informações do conector do ponto de extremidade usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
