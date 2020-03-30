---
title: Gerenciamento Programático de Pontos de Extremidade
seo-title: Gerenciamento Programático de Pontos de Extremidade
description: 'null'
seo-description: 'null'
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Gerenciamento Programático de Pontos de Extremidade {#programmatically-managing-endpoints}

**Sobre o Endpoint Registry Service**

O serviço Endpoint Registry fornece a capacidade de gerenciar programaticamente os pontos de extremidade. Por exemplo, é possível adicionar os seguintes tipos de pontos de extremidade a um serviço:

* EJB
* SOAP
* Pasta assistida
* E-mail
* (Obsoleto para formulários do AEM) Solução remota
* Gerenciador de Tarefas

   ***Observação **: SOAP, EJB e (obsoleto para formulários AEM no JEE) Os pontos finais remotos são criados automaticamente para cada serviço ativado. Os pontos de extremidade SOAP e EJB habilitam SOAP e EJB para todas as operações de serviço.*

   Um terminal Remoting permite que clientes Flex chamem operações no serviço AEM Forms ao qual o terminal é adicionado. Um destino Flex com o mesmo nome do ponto de extremidade é criado e os clientes Flex podem criar RemoteObjects que apontam para esse destino para chamar operações no serviço relevante.

   Os pontos de extremidade Email, Gerenciador de Tarefas e Pasta assistida expõem apenas uma operação específica do serviço. A adição desses pontos finais requer uma segunda etapa de configuração para selecionar um método para chamar, definir parâmetros de configuração e especificar mapeamentos de parâmetros de entrada e saída.

   Você pode organizar pontos de extremidade do TaskManager em grupos chamados *categoria*. Essas categorias são então expostas ao Workspace por meio do TaskManager, com os usuários finais visualizando os pontos finais do TaskManager à medida que são categorizados. No Workspace, os usuários finais visualizam essas categorias no painel de navegação. Os pontos de extremidade dentro de cada categoria são exibidos como cartões de processo na página Processos do Start no Workspace.

   É possível realizar essas tarefas usando o serviço Endpoint Registry:

* Adicione pontos de extremidade EJB. (Consulte [Adicionando pontos finais](programmatically-endpoints.md#adding-ejb-endpoints)EJB.)
* Adicionar pontos de extremidade SOAP. (Consulte [Adicionando Pontos de Extremidade](programmatically-endpoints.md#adding-soap-endpoints)SOAP.)
* Adicionar pontos de extremidade de pasta monitorada (Consulte [Adicionar pontos de extremidade](programmatically-endpoints.md#adding-watched-folder-endpoints)de pasta monitorados.)
* Adicionar pontos de extremidade de email. (Consulte [Adicionando Pontos de Extremidade](programmatically-endpoints.md#adding-email-endpoints)de Email.)
* Adicionar pontos finais remotos. (Consulte [Adicionando Pontos Finais](programmatically-endpoints.md#adding-remoting-endpoints)Remotos.)
* Adicionar pontos de extremidade do TaskManager (Consulte [Adicionar pontos de extremidade](programmatically-endpoints.md#adding-taskmanager-endpoints)do TaskManager.)
* Modifique pontos de extremidade (Consulte [Modificando Pontos de Extremidade](programmatically-endpoints.md#modifying-endpoints).)
* Remova os pontos de extremidade (Consulte [Remoção dos pontos de extremidade](programmatically-endpoints.md#removing-endpoints).)
* Recuperar informações do conector do ponto de extremidade (Consulte [Recuperando informações](programmatically-endpoints.md#retrieving-endpoint-connector-information)do conector do ponto de extremidade.)

## Adicionando pontos finais EJB {#adding-ejb-endpoints}

Você pode adicionar programaticamente um terminal EJB a um serviço usando a API Java de formulários AEM. Ao adicionar um terminal EJB a um serviço, você está permitindo que um aplicativo cliente chame o serviço usando o modo EJB. Ou seja, ao definir as propriedades de conexão necessárias para chamar os formulários AEM, você pode selecionar o modo EJB. (Consulte [Configuração das propriedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexão.)

>[!NOTE]
>
>Não é possível adicionar um terminal EJB usando serviços da Web.

>[!NOTE]
>
>Normalmente, um ponto de extremidade EJB é adicionado a um serviço por padrão. Entretanto, um ponto de extremidade EJB pode ser adicionado a um processo que é implantado programaticamente ou quando um ponto de extremidade EJB foi removido e deve ser adicionado novamente.

### Resumo das etapas {#summary-of-steps}

Para adicionar um terminal EJB a um serviço, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um `EndpointRegistry Client` objeto.
1. Defina atributos de ponto de extremidade EJB.
1. Crie um terminal EJB.
1. Ative o terminal.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

**Criar um objeto de Cliente EndpointRegistry**

Antes de poder adicionar programaticamente um terminal EJB, é necessário criar um `EndpointRegistryClient` objeto.

**Definir atributos de ponto de extremidade EJB**

Para criar um terminal EJB para um serviço, especifique os seguintes valores:

* **Identificador** do conector: Especifica o tipo de terminal a ser criado. Para criar um terminal EJB, especifique `EJB`.
* **Descrição**: Especifica a descrição do ponto de extremidade.
* **Nome**: Especifica o nome do ponto final.
* **Identificador** do serviço: Especifica o serviço ao qual o ponto de extremidade pertence.
* **Nome** da operação: Especifica o nome da operação que é invocada usando o ponto final. Ao criar um terminal EJB, especifique um caractere curinga ( `*`). No entanto, se você quiser especificar uma operação específica em vez de chamar todas as operações de serviço, especifique o nome da operação em vez de usar o caractere curinga ( `*`).

**Criar um ponto de extremidade EJB**

Depois de definir atributos de ponto de extremidade EJB, você pode criar um ponto de extremidade EJB para um serviço.

**Ativar o ponto final**

Depois de criar um novo terminal, é necessário ativá-lo. Depois de ativar o terminal, ele pode ser usado para chamar o serviço. Depois de ativar o terminal, você pode visualização-lo no console de administração.

**Consulte também:**

[Adicionar um terminal EJB usando a API Java](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicionar um terminal EJB usando a API Java {#adding-an-ejb-endpoint-using-the-java-api}

Adicione um terminal EJB usando a API Java:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java. (

1. Crie um objeto EndpointRegistry Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `EndpointRegistryClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Defina atributos de ponto de extremidade EJB.

   * Crie um `CreateEndpointInfo` objeto usando seu construtor.
   * Especifique o valor do identificador do conector, chamando o método do `CreateEndpointInfo` objeto `setConnectorId` e transmitindo o valor da string `EJB`.
   * Especifique a descrição do ponto de extremidade chamando o método do `CreateEndpointInfo` objeto `setDescription` e transmitindo um valor de string que descreve o ponto de extremidade.
   * Especifique o nome do ponto de extremidade chamando o método do `CreateEndpointInfo` `setName` objeto e transmitindo um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o método do `CreateEndpointInfo` objeto `setServiceId` e transmitindo um valor de string que especifica o nome do serviço.
   * Especifique a operação que é invocada invocando o método do `CreateEndpointInfo` `setOperationName` objeto e transmita um valor de string que especifica o nome da operação. Para pontos de extremidade SOAP e EJB, especifique um caractere curinga ( `*`), o que implica todas as operações.

1. Crie um terminal EJB.

   Crie o ponto de extremidade chamando o `EndpointRegistryClient` método do `createEndpoint` objeto e transmitindo o `CreateEndpointInfo` objeto. Este método retorna um `Endpoint` objeto que representa o novo ponto final EJB.

1. Ative o terminal.

   Ative o terminal chamando o método enable do `EndpointRegistryClient` objeto e transmitindo o `Endpoint` objeto que foi retornado pelo `createEndpoint` método.

**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Adicionar um terminal EJB usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Adicionando pontos de extremidade SOAP {#adding-soap-endpoints}

Você pode adicionar programaticamente um terminal SOAP a um serviço usando a API Java de formulários AEM. Ao adicionar um terminal SOAP, você permite que um aplicativo cliente chame o serviço usando o modo SOAP. Ou seja, ao definir as propriedades de conexão necessárias para chamar os formulários AEM, você pode selecionar o modo SOAP.

>[!NOTE]
>
>Não é possível adicionar um terminal SOAP usando serviços da Web.

>[!NOTE]
>
>Normalmente, um terminal SOAP é adicionado a um serviço por padrão. Entretanto, um terminal SOAP pode ser adicionado a um processo que é implantado de forma programática ou quando um terminal SOAP foi removido e precisa ser adicionado novamente.

### Resumo das etapas {#summary_of_steps-1}

Para adicionar um terminal SOAP a um serviço, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um `EndpointRegistryClient` objeto.
1. Defina os atributos de ponto de extremidade SOAP.
1. Crie um terminal SOAP.
1. Ative o terminal.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Esses arquivos JAR são necessários para criar um terminal SOAP. No entanto, é necessário adicionar arquivos JAR se você usar o terminal SOAP para chamar o serviço. Para obter informações sobre arquivos JAR do AEM Forms, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

**Criar um objeto de Cliente EndpointRegistry**

Para adicionar programaticamente um terminal SOAP a um serviço, é necessário criar um `EndpointRegistryClient` objeto.

**Definir atributos de ponto de extremidade SOAP**

Para adicionar um terminal SOAP a um serviço, especifique os seguintes valores:

* **Valor** do identificador do conector: Especifica o tipo de terminal a ser criado. Para criar um terminal SOAP, especifique `SOAP`.
* **Descrição**: Especifica a descrição do ponto de extremidade.
* **Nome**: Especifica o nome do ponto final.
* **Valor** do identificador de serviço: Especifica o serviço ao qual o ponto de extremidade pertence.
* **Nome** da operação: Especifica o nome da operação que é invocada usando o ponto final. Ao criar um terminal SOAP, especifique um caractere curinga ( `*`). No entanto, se você quiser especificar uma operação específica em vez de chamar todas as operações de serviço, especifique o nome da operação em vez de usar o caractere curinga ( `*`).

**Criar um terminal SOAP**

Depois de definir atributos de ponto de extremidade SOAP, você pode criar um ponto de extremidade SOAP.

**Ativar o ponto final**

Depois de criar um novo terminal, é necessário ativá-lo. Quando o terminal está ativado, ele pode ser usado para chamar o serviço. Depois de ativar o terminal, é possível vê-lo em visualização no console de administração.

**Consulte também:**

[Adicionar um terminal SOAP usando a API Java](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicionar um terminal SOAP usando a API Java {#add-a-soap-endpoint-using-the-java-api}

Adicione um terminal SOAP a um serviço usando a API Java:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto EndpointRegistry Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `EndpointRegistryClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Defina os atributos de ponto de extremidade SOAP.

   * Crie um `CreateEndpointInfo` objeto usando seu construtor.
   * Especifique o valor do identificador do conector, chamando o método do `CreateEndpointInfo` objeto `setConnectorId` e transmitindo o valor da string `SOAP`.
   * Especifique a descrição do ponto de extremidade chamando o método do `CreateEndpointInfo` objeto `setDescription` e transmitindo um valor de string que descreve o ponto de extremidade.
   * Especifique o nome do ponto de extremidade chamando o método do `CreateEndpointInfo` `setName` objeto e transmitindo um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o método do `CreateEndpointInfo` objeto `setServiceId` e transmitindo um valor de string que especifica o nome do serviço.
   * Especifique a operação que é invocada chamando o método do `CreateEndpointInfo` `setOperationName` objeto e transmitindo um valor de string que especifica o nome da operação. Para pontos de extremidade SOAP e EJB, especifique um caractere curinga ( `*`), o que implica todas as operações.

1. Crie um terminal SOAP.

   Crie o ponto de extremidade chamando o `EndpointRegistryClient` método do `createEndpoint` objeto e transmitindo o `CreateEndpointInfo` objeto. Esse método retorna um `Endpoint` objeto que representa o novo terminal SOAP.

1. Ative o terminal.

   Ative o terminal chamando o método enable do `EndpointRegistryClient` objeto e transmitindo o `Endpoint` objeto que foi retornado pelo `createEndpoint` método.

**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Adicionar um terminal SOAP usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Adicionando pontos de extremidade de pasta monitorada {#adding-watched-folder-endpoints}

Você pode adicionar programaticamente um terminal de Pasta assistida a um serviço usando a API Java de formulários AEM. Ao adicionar um terminal de Pasta assistida, você permite que os usuários coloquem um arquivo (como um arquivo PDF) em uma pasta. Quando o arquivo é colocado na pasta, o serviço configurado é então chamado e manipula o arquivo. Depois que o serviço executa a operação especificada, ele salva o arquivo modificado em uma pasta de saída especificada. Uma pasta assistida é configurada para ser digitalizada em um intervalo de taxa fixa ou com um cronograma de verificação, como todas as segundas, quartas e sextas-feiras ao meio-dia.

Para fins de adicionar programaticamente um ponto de extremidade de Pasta assistida a um serviço, considere o seguinte processo de vida curta chamado *EncryptDocument*. (Consulte [Como entender os processos](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)do AEM Forms.)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

Esse processo aceita um documento PDF não protegido como um valor de entrada e passa o documento PDF não protegido para a `EncryptPDFUsingPassword` operação do serviço de criptografia. O documento PDF é criptografado com uma senha e o documento PDF criptografado por senha é o valor de saída desse processo. O nome do valor de entrada (o documento PDF não protegido) é `InDoc` e o tipo de dados é `com.adobe.idp.Document`. O nome do valor de saída (o documento PDF criptografado por senha) é `SecuredDoc` e o tipo de dados é `com.adobe.idp.Document`.

>[!NOTE]
>
>Não é possível adicionar um ponto de extremidade de Pasta assistida usando serviços da Web.

### Resumo das etapas {#summary_of_steps-2}

Para adicionar um terminal de Pasta assistida a um serviço, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um `EndpointRegistryClient` objeto.
1. Defina os atributos do ponto de extremidade da Pasta assistida.
1. Especifique os valores de configuração.
1. Defina os valores dos parâmetros de entrada.
1. Defina um valor de parâmetro de saída.
1. Criar um terminal de Pasta assistida.
1. Ative o terminal.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

**Criar um objeto de Cliente EndpointRegistry**

Para adicionar programaticamente um ponto de extremidade de Pasta assistida, é necessário criar um `EndpointRegistryClient` objeto.

**Definir atributos de ponto de extremidade de Pasta assistida**

Para criar um ponto de extremidade de Pasta assistida para um serviço, especifique os seguintes valores:

* **Identificador** do conector: Especifica o tipo de endpoint criado. Para criar um ponto de extremidade de Pasta assistida, especifique `WatchedFolder`.
* **Descrição**: Especifica a descrição do ponto final.
* **Nome**: Especifica o nome do ponto final.
* **Identificador** do serviço: Especifica o serviço ao qual o ponto de extremidade pertence. Por exemplo, para adicionar um endpoint de Pasta assistida ao processo que é introduzido nesta seção (um processo se torna um serviço quando ativado usando o Workbench), especifique `EncryptDocument`.
* **Nome** da operação: Especifica o nome da operação que é invocada usando o ponto final. Geralmente, ao criar um terminal de Pasta assistida para um serviço que se originou de um processo criado no Workbench, o nome da operação é `invoke`.

**Especificar valores de configuração**

Você deve especificar valores de configuração para um endpoint de Pasta assistida ao adicionar programaticamente um endpoint de Pasta assistida a um serviço. Esses valores de configuração são especificados por um administrador se um endpoint de Pasta assistida for adicionado usando o console de administração.

A lista a seguir especifica os valores de configuração que são definidos ao adicionar programaticamente um ponto de extremidade de Pasta assistida a um serviço:

* **url**: Especifica o local da pasta monitorada. Em um ambiente clusterizado, esse valor deve apontar para uma pasta de rede compartilhada acessível de todos os computadores do cluster.
* **assíncrono**: Identifica o tipo de invocação como assíncrono ou síncrono. Processos transitórios e síncronos só podem ser chamados de forma síncrona. O valor padrão é true. Recomenda-se assíncrono.
* **cronExpression**: Usado por quartzo para agendar a pesquisa do diretório de entrada. Para obter detalhes sobre como configurar a expressão cron, consulte [https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html](https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html).
* **purgeDuration**: Este atributo é obrigatório. Os arquivos e pastas na pasta de resultados são removidos quando são mais antigos que esse valor. Esse valor é medido em dias. Esse atributo é útil para garantir que a pasta de resultados não fique cheia. Um valor de -1 dias indica que a pasta de resultados nunca será excluída. O valor padrão é -1.
* **duplicateInterval**: O intervalo, em segundos, para verificar a entrada da Pasta assistida. A menos que a limitação esteja ativada, esse valor deve ser maior que o tempo para processar um trabalho médio; caso contrário, o sistema poderá ficar sobrecarregado. O valor padrão é 5.
* **againCount**: O número de vezes que uma Pasta assistida verifica a pasta ou o diretório. Um valor de -1 indica uma varredura indefinida. O valor padrão é -1.
* **aceleração**: Limita o número de trabalhos da Pasta assistida que podem ser processados em um determinado momento. O número máximo de trabalhos é determinado pelo valor batchSize.
* **userName**: O nome de usuário usado ao invocar um serviço de público alvo da Pasta assistida. Este valor é obrigatório. O valor padrão é SuperAdmin.
* **domainName**: O domínio do usuário. Este valor é obrigatório. O valor padrão é DefaultDom.
* **batchSize**: O número de arquivos ou pastas a serem coletados por varredura. Use esse valor para evitar uma sobrecarga no sistema; a verificação de muitos arquivos ao mesmo tempo pode resultar em uma falha. O valor padrão é 2.
* **waitTime**: O tempo, em milissegundos, para aguardar antes de digitalizar uma pasta ou arquivo após a criação. Por exemplo, se o tempo de espera for de 36.000.000 milissegundos (uma hora) e o arquivo tiver sido criado há um minuto, esse arquivo será coletado depois de 59 minutos ou mais. Esse atributo é útil para garantir que um arquivo ou pasta seja completamente copiado para a pasta de entrada. Por exemplo, se você tiver um arquivo grande para processar e o arquivo levar dez minutos para ser baixado, defina o tempo de espera como 10&amp;ast;60 &amp;ast;1000 milissegundos. Essa configuração impede que a pasta assistida verifique o arquivo se ele não estiver aguardando por dez minutos. O valor padrão é 0.
* **excludeFilePattern**: O padrão que uma pasta assistida usa para determinar quais arquivos e pastas serão examinados e coletados. Qualquer arquivo ou pasta que tenha esse padrão não será verificado para processamento. Essa configuração é útil quando a entrada é uma pasta que contém vários arquivos. O conteúdo da pasta pode ser copiado em uma pasta que tenha um nome que será selecionado pela pasta assistida. Esta etapa impede que a pasta assistida pegue uma pasta para processamento antes que ela seja completamente copiada para a pasta de entrada. Por exemplo, se o valor excludeFilePattern for `data*`, todos os arquivos e pastas correspondentes não `data*` serão selecionados. Isso inclui arquivos e pastas nomeados `data1`, `data2`etc. Além disso, o padrão pode ser complementado com padrões curingas para especificar padrões de arquivos. A pasta assistida modifica a expressão normal para suportar padrões curingas, como `*.*` e `*.pdf`. Esses padrões curingas não são suportados por expressões regulares.
* **includeFilePattern**: O padrão que a pasta assistida usa para determinar quais pastas e arquivos serão examinados e coletados. Por exemplo, se esse valor for `*`, todos os arquivos e pastas correspondentes `input*` serão selecionados. Isso inclui arquivos e pastas nomeados `input1`, `input2`etc. O valor padrão é `*`. Esse valor indica todos os arquivos e pastas. Além disso, o padrão pode ser complementado com padrões curingas para especificar padrões de arquivos. A pasta assistida modifica a expressão normal para suportar padrões curingas, como `*.*` e `*.pdf`. Esses padrões curingas não são suportados por expressões regulares. Este valor é obrigatório.
* **resultFolderName**: A pasta onde os resultados salvos são armazenados. Esse local pode ser um caminho absoluto ou relativo do diretório. Se os resultados não forem exibidos nessa pasta, verifique a pasta de falha. Os arquivos somente leitura não são processados e serão salvos na pasta de falha. O valor padrão é `result/%Y/%M/%D/`. Esta é a pasta de resultados dentro da pasta assistida.
* **preserveFolderName**: O local onde os arquivos são armazenados após a verificação e coleta bem-sucedidas. Esse local pode ser um caminho de diretório absoluto, relativo ou nulo. O valor padrão é `preserve/%Y/%M/%D/`.
* **failureFolderName**: A pasta onde os arquivos de falha são salvos. Esse local é sempre relativo à pasta assistida. Os arquivos somente leitura não são processados e serão salvos na pasta de falha. O valor padrão é `failure/%Y/%M/%D/`.
* **preserveOnFailure**: Preservar arquivos de entrada em caso de falha ao executar a operação em um serviço. O valor padrão é true.
* **overwriteDuplicateFilename**: Quando definido como true, os arquivos na pasta de resultados e a pasta preserve são substituídos. Quando definido como falso, os arquivos e pastas que têm um sufixo de índice numérico são usados para o nome. O valor padrão é false.

**Definir valores de parâmetros de entrada**

Ao criar um ponto final de Pasta assistida, você deve definir valores de parâmetro de entrada. Ou seja, você deve descrever os valores de entrada passados para a operação chamada pela pasta assistida. Por exemplo, considere o processo apresentado neste tópico. Tem um valor de entrada nomeado `InDoc` e seu tipo de dados é `com.adobe.idp.Document`. Ao criar um terminal de Pasta assistida para esse processo (depois que um processo é ativado, ele se torna um serviço), você deve definir o valor do parâmetro de entrada.

Para definir valores de parâmetro de entrada necessários para um ponto de extremidade de Pasta assistida, especifique os seguintes valores:

**Nome** do parâmetro de entrada: O nome do parâmetro de entrada. O nome de um valor de entrada é especificado no Workbench para um processo. Se o valor de entrada pertencer a uma operação de serviço (um serviço que não é um processo criado no Workbench), o nome de entrada será especificado no arquivo component.xml. Por exemplo, o nome do parâmetro de entrada para o processo introduzido nesta seção é `InDoc`.

**Tipo** de mapeamento: Usado para configurar os valores de entrada necessários para chamar a operação de serviço. Há dois tipos de mapeamento:

* `Literal`: O endpoint de Pasta assistida usa o valor inserido no campo conforme ele é exibido. Todos os tipos básicos de Java são suportados. Por exemplo, se uma API usar uma entrada como String, long, int e Boolean, a string será convertida no tipo correto e o serviço será chamado.
* `Variable`: O valor inserido é um padrão de arquivo que a pasta assistida usa para escolher a entrada. Por exemplo, se você selecionar Variável para o tipo de mapeamento e o documento de entrada precisar ser um arquivo PDF, poderá especificar `*.pdf`como valor de mapeamento.

**Valor** de mapeamento: Especifica o valor do tipo de mapeamento. Por exemplo, se você selecionar um tipo de `Variable` mapeamento, poderá especificar `*.pdf` como padrão de arquivo.

**Tipo** de dados: Especifica o tipo de dados dos valores de entrada. Por exemplo, o tipo de dados do valor de entrada do processo introduzido nesta seção é `com.adobe.idp.Document`.

**Definir um valor de parâmetro de saída**

Ao criar um ponto final de Pasta assistida, você deve definir um valor de parâmetro de saída. Ou seja, você deve descrever o valor de saída que é retornado pelo serviço chamado pelo endpoint de Pasta assistida. Por exemplo, considere o processo apresentado neste tópico. Tem um valor de saída nomeado `SecuredDoc` e seu tipo de dados é `com.adobe.idp.Document`. Ao criar um terminal de Pasta assistida para esse processo (depois que um processo é ativado, ele se torna um serviço), você deve definir o valor do parâmetro de saída.

Para definir um valor de parâmetro de saída necessário para um endpoint de Pasta assistida, especifique os seguintes valores:

**Nome** do parâmetro de saída: O nome do parâmetro de saída. O nome de um valor de saída de processo é especificado no Workbench. Se o valor de saída pertencer a uma operação de serviço (um serviço que não é um processo criado no Workbench), o nome de saída será especificado no arquivo component.xml. Por exemplo, o nome do parâmetro de saída para o processo introduzido nesta seção é `SecuredDoc`.

**Tipo** de mapeamento: Usado para configurar a saída do serviço e da operação. As opções disponíveis são as seguintes:

* Se o serviço retornar um único objeto (um único documento), o padrão será `%F.pdf` e o destino de origem será sourcefilename.pdf. Por exemplo, o processo introduzido nesta seção retorna um único documento. Como resultado, o tipo de mapeamento pode ser definido como `%F.pdf` ( `%F` significa usar o nome de arquivo fornecido). O padrão `%E` especifica a extensão do documento de entrada.
* Se o serviço retornar uma lista, o padrão será `Result\%F\`e o destino de origem será Result\sourcefilename\source1 (output 1) e Result\sourcefilename\source2 (output 2).
* Se o serviço retornar um mapa, o padrão será `Result\%F\`e o destino de origem será Result\sourcefilename\file1 and Result\sourcefilename\file2. Se o mapa tiver mais de um objeto, o padrão será `Result\%F.pdf` e o destino de origem será Result\sourcefilename1.pdf (saída 1), Result\sourcefilenam2.pdf (saída 2) e assim por diante.

**Tipo** de dados: Especifica o tipo de dados do valor de retorno. Por exemplo, o tipo de dados do valor de retorno do processo introduzido nesta seção é `com.adobe.idp.Document`.

**Criar um ponto de extremidade de Pasta assistida**

Depois de definir os atributos do ponto final, os valores de configuração e os valores dos parâmetros de entrada e saída, você deve criar o ponto final da Pasta assistida.

**Ativar o ponto final**

Depois de criar um terminal de Pasta assistida, é necessário ativá-lo. Quando o terminal está ativado, ele pode ser usado para chamar o serviço. Depois de ativar o terminal, você pode visualização-lo no console de administração.

**Consulte também:**

[Adicionar um terminal de Pasta assistida usando a API Java](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicionar um terminal de Pasta assistida usando a API Java {#add-a-watched-folder-endpoint-using-the-java-api}

Adicione um terminal de Pasta assistida usando a API Java de formulários AEM:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto EndpointRegistry Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `EndpointRegistryClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Defina os atributos do ponto de extremidade da Pasta assistida.

   * Crie um `CreateEndpointInfo` objeto usando seu construtor.
   * Especifique o valor do identificador do conector, chamando o método do `CreateEndpointInfo` objeto `setConnectorId` e transmitindo o valor da string `WatchedFolder`.
   * Especifique a descrição do ponto de extremidade chamando o método do `CreateEndpointInfo` objeto `setDescription` e transmitindo um valor de string que descreve o ponto de extremidade.
   * Especifique o nome do ponto de extremidade chamando o método do `CreateEndpointInfo` `setName` objeto e transmitindo um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o método do `CreateEndpointInfo` objeto `setServiceId` e transmitindo um valor de string que especifica o nome do serviço.
   * Especifique a operação que é invocada chamando o método do `CreateEndpointInfo` `setOperationName` objeto e transmitindo um valor de string que especifica o nome da operação. Geralmente, ao criar um ponto de extremidade de Pasta assistida para um serviço originado de um processo criado no Workbench, o nome da operação é chamado.

1. Especifique os valores de configuração.

   Para cada valor de configuração a ser definido para o endpoint de Pasta assistida, é necessário chamar o `CreateEndpointInfo` método do `setConfigParameterAsText` objeto. Por exemplo, para definir o valor de `url` configuração, chame o método `CreateEndpointInfo` do objeto `setConfigParameterAsText` e transmita os seguintes valores de string:

   * Um valor de string que especifica o nome do valor de configuração. Ao definir o valor de `url` configuração, especifique `url`.
   * Um valor de string que especifica o valor da configuração. Ao definir o valor de `url` configuração, especifique o local da pasta monitorada.
   >[!NOTE]
   >
   >Para ver todos os valores de configuração definidos para o serviço EncryptDocument, consulte o exemplo de código Java localizado em [QuickStart: Adicionando um terminal de Pasta assistida usando a API](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)Java.

1. Defina os valores dos parâmetros de entrada.

   Defina um valor de parâmetro de entrada chamando o método do `CreateEndpointInfo` objeto `setInputParameterMapping` e transmitindo os seguintes valores:

   * Um valor de string que especifica o nome do parâmetro de entrada. Por exemplo, o nome do parâmetro de entrada para o serviço EncryptDocument é `InDoc`.
   * Um valor de string que especifica o tipo de dados do parâmetro de entrada. Por exemplo, o tipo de dados do parâmetro de `InDoc` entrada é `com.adobe.idp.Document`.
   * Um valor de string que especifica o tipo de mapeamento. For example, you can specify `variable`.
   * Um valor de string que especifica o valor do tipo de mapeamento. Por exemplo, você pode especificar &amp;ast;.pdf como padrão de arquivo.
   >[!NOTE]
   >
   >Chame o `setInputParameterMapping` método para cada valor de parâmetro de entrada a ser definido. Como o processo EncryptDocument tem apenas um parâmetro de entrada, é necessário chamar esse método uma vez.

1. Defina um valor de parâmetro de saída.

   Defina um valor de parâmetro de saída chamando o método do `CreateEndpointInfo` objeto `setOutputParameterMapping` e transmitindo os seguintes valores:

   * Um valor de string que especifica o nome do parâmetro de saída. Por exemplo, o nome do parâmetro de saída para o serviço EncryptDocument é `SecuredDoc`.
   * Um valor de string que especifica o tipo de dados do parâmetro de saída. Por exemplo, o tipo de dados do parâmetro de `SecuredDoc` saída é `com.adobe.idp.Document`.
   * Um valor de string que especifica o tipo de mapeamento. For example, you can specify `%F.pdf`.

1. Criar um terminal de Pasta assistida.

   Crie o ponto de extremidade chamando o `EndpointRegistryClient` método do `createEndpoint` objeto e transmitindo o `CreateEndpointInfo` objeto. Esse método retorna um `Endpoint` objeto que representa o endpoint de Pasta assistida.

1. Ative o terminal.

   Ative o terminal chamando o `EndpointRegistryClient` método do `enable` objeto e transmitindo o `Endpoint` objeto que foi retornado pelo `createEndpoint` método.

**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Adicionar um ponto de extremidade de Pasta assistida usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Arquivo constante de valores de configuração de pasta monitorada {#watched-folder-configuration-values-constant-file}

O [QuickStart: A adição de um terminal de Pasta assistida usando a API](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) Java usa um arquivo constante que deve fazer parte do seu projeto Java para compilar o start rápido. Esse arquivo constante representa valores de configuração que devem ser definidos ao adicionar um ponto final de Pasta assistida. O código Java a seguir representa o arquivo constante.

```as3
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

## Adicionando Pontos de Extremidade de Email {#adding-email-endpoints}

Você pode adicionar programaticamente um terminal de email a um serviço usando a API Java de formulários AEM. Ao adicionar um terminal de email, você permite que os usuários enviem uma mensagem de email com um ou mais anexos de arquivo para uma conta de email especificada. Em seguida, a operação de configuração de serviço é chamada e manipula os arquivos. Depois que o serviço executa a operação especificada, ele envia uma mensagem de email para o remetente com os arquivos modificados como anexos de arquivo.

Para fins de adicionar programaticamente um ponto de extremidade de email a um serviço, considere o seguinte processo de vida curta chamado *MyApplication\EncryptDocument*. Para obter informações sobre processos de duração curta, consulte [Entendendo os processos](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)do AEM Forms.

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

Esse processo aceita um documento PDF não protegido como um valor de entrada e passa o documento PDF não protegido para a `EncryptPDFUsingPassword` operação do serviço de criptografia. Esse processo criptografa o documento PDF com uma senha e retorna o documento PDF criptografado por senha como valor de saída. O nome do valor de entrada (o documento PDF não protegido) é `InDoc` e o tipo de dados é `com.adobe.idp.Document`. O nome do valor de saída (o documento PDF criptografado por senha) é `SecuredDoc` e o tipo de dados é `com.adobe.idp.Document`.

>[!NOTE]
>
>Não é possível adicionar um terminal de email usando serviços da Web.

### Resumo das etapas {#summary_of_steps-3}

Para adicionar um terminal de email a um serviço, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um `EndpointRegistryClient` objeto.
1. Defina atributos de ponto de extremidade de email.
1. Especifique os valores de configuração.
1. Defina os valores dos parâmetros de entrada.
1. Defina um valor de parâmetro de saída.
1. Crie o terminal Email.
1. Ative o terminal.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

**Criar um objeto de Cliente EndpointRegistry**

Antes de poder adicionar programaticamente um terminal de E-mail, é necessário criar um `EndpointRegistryClient` objeto.

**Definir atributos de ponto de extremidade de email**

Para criar um terminal de email para um serviço, especifique os seguintes valores:

* **Valor** do identificador do conector: Especifica o tipo de endpoint criado. Para criar um terminal de email, especifique `Email`.
* **Descrição**: Especifica uma descrição para o ponto final.
* **Nome**: Especifica o nome do ponto final.
* **Valor** do identificador de serviço: Especifica o serviço ao qual o ponto de extremidade pertence. Por exemplo, para adicionar um terminal de Email ao processo que é introduzido nesta seção (um processo se torna um serviço quando ativado usando o Workbench), especifique `EncryptDocument`.
* **Nome** da operação: Especifica o nome da operação que é invocada usando o ponto final. Geralmente, ao criar um terminal de email para um serviço originado de um processo criado no Workbench, o nome da operação é `invoke`.

**Especificar valores de configuração**

Você deve especificar valores de configuração para um terminal de email ao adicionar programaticamente um terminal de email a um serviço. Esses valores de configuração são especificados por um administrador se um terminal de email for adicionado usando o console de administração.

>[!NOTE]
>
>A conta de email que é monitorada é uma conta especial usada apenas para o terminal Email. Esta conta não é uma conta de email normal do usuário. A conta de email de um usuário regular não deve ser configurada como a conta que o Provedor de email usa, pois o Provedor de email exclui mensagens da caixa de entrada depois que elas são terminadas.

Os seguintes valores de configuração são definidos ao adicionar programaticamente um ponto de extremidade de Email a um serviço:

* **cronExpression**: Uma expressão cron se o email precisar ser agendado usando uma expressão cron.
* **againCount**: Número de vezes que o ponto de extremidade de email verifica a pasta ou o diretório. Um valor de -1 indica uma varredura indefinida. O valor padrão é -1.
* **duplicateInterval**: A taxa de varredura, em segundos, que o receptor usa para verificar a entrada de emails. O valor padrão é 10.
* **startDelay**: O tempo de espera para digitalizar após os start do scheduler. A hora padrão é 0.
* **batchSize**: O número de mensagens de e-mail que o receptor processa por verificação para obter um desempenho ótimo. O valor -1 indica todos os emails. O valor padrão é 2.
* **userName**: O nome de usuário usado ao chamar um serviço de público alvo do email. O valor padrão é `SuperAdmin`.
* **domainName**: Um valor de configuração obrigatório. O valor padrão é `DefaultDom`.
* **domainPattern**: Especifica os padrões de domínio do email recebido que o provedor aceita. Por exemplo, se `adobe.com` for usado, somente o email do adobe.com será processado, o email de outros domínios será ignorado.
* **filePattern**: Especifica os padrões de anexo de arquivo de entrada aceitos pelo provedor. Isso inclui arquivos com extensões de nome de arquivo específicas (&amp;ast;.dat, &amp;ast;.xml), arquivos com nomes específicos (dados) e arquivos com expressões compostas no nome e na extensão (&amp;ast;.[dD][aA]&#39;port&#39;). O valor padrão é `*`.
* **receiptSuccessfulJob**: Um endereço de email para o qual as mensagens são enviadas para indicar trabalhos bem-sucedidos. Por padrão, uma mensagem de trabalho bem-sucedida é sempre enviada ao remetente. Se você digitar `sender`, os resultados do email serão enviados ao remetente. Há suporte para até 100 recipient. Especifique recipient adicionais com endereços de email, cada um separado por vírgula. Para desativar essa opção, deixe esse valor em branco. Em alguns casos, talvez você queira acionar um processo e não desejar uma notificação por email do resultado. O valor padrão é `sender`.
* **receiptFailedJob**: Um endereço de email para o qual são enviadas mensagens para indicar trabalhos com falha. Por padrão, uma mensagem de falha de trabalho é sempre enviada ao remetente. Se você digitar `sender`, os resultados do email serão enviados ao remetente. Há suporte para até 100 recipient. Especifique recipient adicionais com endereços de email, cada um separado por vírgula. Para desativar essa opção, deixe esse valor em branco. O valor padrão é `sender`.
* **inboxHost**: O nome do host da caixa de entrada ou o endereço IP do provedor de email a ser verificado.
* **inboxPort**: A porta que o servidor de email usa. O valor padrão para POP3 é 110 e o valor padrão para IMAP é 143. Se SSL estiver ativado, o valor padrão para POP3 é 995 e o valor padrão para IMAP é 993.
* **inboxProtocol**: O protocolo de email do terminal de email a ser usado para digitalizar a caixa de entrada. As opções são `IMAP` ou `POP3`. O servidor de correio do host da caixa de entrada deve suportar esses protocolos.
* **inboxTimeOut**: Tempo limite em segundos para que o provedor de email aguarde respostas da caixa de entrada. O valor padrão é 60.
* **inboxUser**: O nome de usuário necessário para fazer logon na conta de email. Dependendo do servidor de e-mail e da configuração, essa pode ser apenas a parte do nome do usuário do e-mail ou pode ser o endereço de e-mail completo.
* **inboxPassword**: A senha do usuário da caixa de entrada.
* **inboxSSLEnabled**: Defina esse valor para forçar o provedor de email a usar SSL ao enviar mensagens de notificação de resultados ou erros. Verifique se o host IMAP ou POP3 suporta SSL.
* **smtpHost**: O nome de host do servidor de email para o qual o provedor de email envia resultados e mensagens de erro.
* **smtpPort**: O valor padrão para a porta SMTP é 25.
* **smtpUser**: A conta de usuário que o provedor de email deve usar ao enviar notificações por email de resultados e erros.
* **smtpPassword**: A senha da conta SMTP. Alguns servidores de email não exigem uma senha SMTP.
* **charSet**: O conjunto de caracteres usado pelo provedor de email. O valor padrão é `UTF-8`.
* **smtpSSLEnabled**: Defina esse valor para forçar o provedor de email a usar SSL ao enviar mensagens de notificação de resultados ou erros. Verifique se o Host SMTP suporta SSL.
* **failedJobFolder**: Especifica um diretório no qual armazenar resultados quando o servidor de correio SMTP não estiver operacional.
* **assíncrono**: Quando definido como síncrono, todos os documentos de entrada são processados e uma única resposta é retornada. Quando definido como assíncrono, uma resposta é enviada para cada documento de entrada processado. Por exemplo, um ponto de extremidade de email é criado para o processo introduzido neste tópico e uma mensagem de email é enviada para a caixa de entrada do ponto de extremidade que contém vários documentos PDF não protegidos. Quando todos os documentos PDF são criptografados com uma senha e, se o ponto final estiver configurado como síncrono, uma única mensagem de email de resposta é enviada com todos os documentos PDF protegidos anexados. Se o terminal estiver configurado como assíncrono, uma mensagem de email de resposta separada será enviada para cada documento PDF protegido. Cada mensagem de email contém um único documento PDF como anexo. O valor padrão é assíncrono.

**Definir valores de parâmetros de entrada**

Ao criar um terminal de email, você deve definir valores de parâmetro de entrada. Ou seja, você deve descrever os valores de entrada passados para a operação chamada pelo terminal Email. Por exemplo, considere o processo apresentado neste tópico. Tem um valor de entrada nomeado `InDoc` e seu tipo de dados é `com.adobe.idp.Document`. Ao criar um terminal de email para esse processo (depois que um processo é ativado, ele se torna um serviço), você deve definir o valor do parâmetro de entrada.

Para definir os valores de parâmetro de entrada necessários para um ponto de extremidade Email, especifique os seguintes valores:

**Nome** do parâmetro de entrada: O nome do parâmetro de entrada. O nome de um valor de entrada é especificado no Workbench para um processo. Se o valor de entrada pertencer a uma operação de serviço (um serviço do Forms que não é um processo criado no Workbench), o nome de entrada será especificado no arquivo component.xml. Por exemplo, o nome do parâmetro de entrada para o processo introduzido nesta seção é `InDoc`.

**Tipo** de mapeamento: Usado para configurar os valores de entrada necessários para chamar a operação de serviço. Dois tipos de mapeamento são os seguintes:

* `Literal`: O terminal Email usa o valor inserido no campo conforme é exibido. Todos os tipos básicos de Java são suportados. Por exemplo, se uma API usar uma entrada como String, long, int e Boolean, a string será convertida no tipo correto e o serviço será chamado.
* `Variable`: O valor inserido é um padrão de arquivo que o terminal Email usa para escolher a entrada. Por exemplo, se você selecionar Variável para o tipo de mapeamento e o documento de entrada precisar ser um arquivo PDF, poderá especificar `*.pdf` como valor de mapeamento.

**Valor** de mapeamento: Especifica o valor do tipo de mapeamento. Por exemplo, se você selecionar um tipo de mapeamento de variável, poderá especificar `*.pdf` como padrão de arquivo.

**Tipo** de dados: Especifica o tipo de dados dos valores de entrada. Por exemplo, o tipo de dados do valor de entrada do processo introduzido nesta seção é com.adobe.idp.Documento.

**Definir um valor de parâmetro de saída**

Ao criar um terminal de email, você deve definir um valor de parâmetro de saída. Ou seja, você deve descrever o valor de saída que é retornado pelo serviço chamado pelo terminal Email. Por exemplo, considere o processo apresentado neste tópico. Tem um valor de saída nomeado `SecuredDoc` e seu tipo de dados é `com.adobe.idp.Document`. Ao criar um terminal de email para esse processo (depois que um processo é ativado, ele se torna um serviço), você deve definir o valor do parâmetro de saída.

Para definir um valor de parâmetro de saída necessário para um ponto de extremidade Email, especifique os seguintes valores:

**Nome** do parâmetro de saída: O nome do parâmetro de saída. O nome de um valor de saída de processo é especificado no Workbench. Se o valor de saída pertencer a uma operação de serviço (um serviço que não é um processo criado no Workbench), o nome de saída será especificado no arquivo component.xml. Por exemplo, o nome do parâmetro de saída para o processo introduzido nesta seção é `SecuredDoc`.

**Tipo** de mapeamento: Usado para configurar a saída do serviço e da operação. As opções disponíveis são as seguintes:

* Se o serviço retornar um único objeto (um único documento), o padrão será `%F.pdf` e o destino de origem será sourcefilename.pdf. Por exemplo, o processo introduzido nesta seção retorna um único documento. Como resultado, o tipo de mapeamento pode ser definido como `%F.pdf` ( `%F` significa usar o nome de arquivo fornecido). O padrão `%E` especifica a extensão do documento de entrada.
* Se o serviço retornar uma lista, o padrão será `Result\%F\`e o destino de origem será Result\sourcefilename\source1 (output 1) e Result\sourcefilename\source2 (output 2).
* Se o serviço retornar um mapa, o padrão será `Result\%F\`e o destino de origem será Result\sourcefilename\file1 and Result\sourcefilename\file2. Se o mapa tiver mais de um objeto, o padrão será `Result\%F.pdf` e o destino de origem será Result\sourcefilename1.pdf (saída 1), Result\sourcefilenam2.pdf (saída 2) e assim por diante.

**Tipo** de dados: Especifica o tipo de dados do valor de retorno. Por exemplo, o tipo de dados do valor de retorno do processo introduzido nesta seção é `com.adobe.idp.Document`.

**Criar o terminal Email**

Depois de definir os atributos e os valores de configuração do ponto de extremidade de E-mail e definir os valores dos parâmetros de entrada e saída, você deve criar o ponto de extremidade de E-mail.

**Ativar o ponto final**

Depois de criar um terminal de email, é necessário ativá-lo. Quando o terminal está ativado, ele pode ser usado para chamar o serviço. Depois de ativar o terminal, você pode visualização-lo no console de administração.

**Consulte também:**

[Adicionar um terminal de email usando a API Java](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicionar um terminal de email usando a API Java {#add-an-email-endpoint-using-the-java-api}

Adicione um terminal de email usando a API Java:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto EndpointRegistry Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `EndpointRegistryClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Defina atributos de ponto de extremidade de email.

   * Crie um `CreateEndpointInfo` objeto usando seu construtor.
   * Especifique o valor do identificador do conector, chamando o método do `CreateEndpointInfo` objeto `setConnectorId` e transmitindo o valor da string `Email`.
   * Especifique a descrição do ponto de extremidade chamando o método do `CreateEndpointInfo` objeto `setDescription` e transmitindo um valor de string que descreve o ponto de extremidade.
   * Especifique o nome do ponto de extremidade chamando o método do `CreateEndpointInfo` `setName` objeto e transmitindo um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o método do `CreateEndpointInfo` objeto `setServiceId` e transmitindo um valor de string que especifica o nome do serviço.
   * Especifique a operação que é invocada chamando o método do `CreateEndpointInfo` `setOperationName` objeto e transmitindo um valor de string que especifica o nome da operação. Geralmente, ao criar um terminal de email para um serviço originado de um processo criado no Workbench, o nome da operação é chamado.

1. Especifique os valores de configuração.

   Para que cada valor de configuração seja definido para o terminal Email, é necessário chamar o método do `CreateEndpointInfo` objeto `setConfigParameterAsText` . Por exemplo, para definir o valor de `smtpHost` configuração, chame o método `CreateEndpointInfo` do objeto `setConfigParameterAsText` e passe os seguintes valores:

   * Um valor de string que especifica o nome do valor de configuração. Ao definir o valor de `smtpHost` configuração, especifique `smtpHost`.
   * Um valor de string que especifica o valor da configuração. Ao definir o valor de `smtpHost` configuração, especifique um valor de string que especifique o nome do servidor SMTP.
   >[!NOTE]
   >
   >Para ver todos os valores de configuração definidos para o serviço EncryptDocument introduzido nesta seção, consulte o exemplo de código Java localizado em [QuickStart: Adicionando um terminal de email usando a API](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api)Java.

1. Defina os valores dos parâmetros de entrada.

   Defina um valor de parâmetro de entrada chamando o método do `CreateEndpointInfo` objeto `setInputParameterMapping` e transmitindo os seguintes valores:

   * Um valor de string que especifica o nome do parâmetro de entrada. Por exemplo, o nome do parâmetro de entrada para o serviço EncryptDocument é `InDoc`.
   * Um valor de string que especifica o tipo de dados do parâmetro de entrada. Por exemplo, o tipo de dados do parâmetro de `InDoc` entrada é `com.adobe.idp.Document`.
   * Um valor de string que especifica o tipo de mapeamento. For example, you can specify `variable`.
   * Um valor de string que especifica o valor do tipo de mapeamento. Por exemplo, você pode especificar &amp;ast;.pdf como padrão de arquivo.
   >[!NOTE]
   >
   >Chame o `setInputParameterMapping` método para cada valor de parâmetro de entrada a ser definido. Como o processo EncryptDocument tem apenas um parâmetro de entrada, é necessário chamar esse método uma vez.

1. Defina um valor de parâmetro de saída.

   Defina um valor de parâmetro de saída chamando o método do `CreateEndpointInfo` objeto `setOutputParameterMapping` e transmitindo os seguintes valores:

   * Um valor de string que especifica o nome do parâmetro de saída. Por exemplo, o nome do parâmetro de saída para o serviço EncryptDocument é `SecuredDoc`.
   * Um valor de string que especifica o tipo de dados do parâmetro de saída. Por exemplo, o tipo de dados do parâmetro de `SecuredDoc` saída é `com.adobe.idp.Document`.
   * Um valor de string que especifica o tipo de mapeamento. For example, you can specify `%F.pdf`.

1. Crie o terminal Email.

   Crie o ponto de extremidade chamando o `EndpointRegistryClient` método do `createEndpoint` objeto e transmitindo o `CreateEndpointInfo` objeto. Esse método retorna um `Endpoint` objeto que representa o ponto de extremidade Email.

1. Ative o terminal.

   Ative o terminal chamando o `EndpointRegistryClient` método do `enable` objeto e transmitindo o `Endpoint` objeto que foi retornado pelo `createEndpoint` método.

**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Adicionar um ponto de extremidade de Pasta assistida usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Arquivo constante de valores de configuração de email {#email-configuration-values-constant-file}

O [QuickStart: Adicionar um terminal de email usando a API](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) Java usa um arquivo constante que deve fazer parte do seu projeto Java para compilar o start rápido. Esse arquivo constante representa valores de configuração que devem ser definidos ao adicionar um ponto de extremidade de email. O código Java a seguir representa o arquivo constante.

```as3
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

## Adicionando Pontos Finais Remotos {#adding-remoting-endpoints}

>[!NOTE]
>
>As APIs do LiveCycle Remoting foram substituídas para formulários AEM no JEE.

Você pode adicionar programaticamente um terminal Remoting a um serviço usando a API Java de formulários AEM. Ao adicionar um terminal Remoting, você está permitindo que um aplicativo Flex chame o serviço usando a remoção. (Consulte [Invocar formulários AEM usando (obsoleto para formulários AEM) Formulários AEM Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

Para fins de adicionar programaticamente um terminal Remoto a um serviço, considere o seguinte processo de vida curta chamado *EncryptDocument*.

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

Esse processo aceita um documento PDF não protegido como um valor de entrada e passa o documento PDF não protegido para a `EncryptPDFUsingPassword` operação do serviço de criptografia. O documento PDF é criptografado com uma senha e o documento PDF criptografado por senha é o valor de saída desse processo. O nome do valor de entrada (o documento PDF não protegido) é `InDoc` e o tipo de dados é `com.adobe.idp.Document`. O nome do valor de saída (o documento PDF criptografado por senha) é `SecuredDoc` e o tipo de dados é `com.adobe.idp.Document`.

Para demonstrar como adicionar um terminal Remoto a um serviço, esta seção adiciona um terminal Remoto a um serviço chamado EncryptDocument.

>[!NOTE]
>
>Não é possível adicionar um terminal Remoto usando serviços da Web.

### Resumo das etapas {#summary_of_steps-4}

Para remover um terminal de um serviço, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um `EndpointRegistryClient` objeto.
1. Definir atributos de ponto final remoto.
1. Criar um terminal Remoto.
1. Ative o terminal.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

**Criar um objeto de Cliente EndpointRegistry**

Para adicionar programaticamente um terminal Remoting, é necessário criar um `EndpointRegistryClient` objeto.

**Definir atributos de ponto final remoto**

Para criar um terminal Remoto para um serviço, especifique os seguintes valores:

* **Valor** do identificador do conector: Especifica o tipo de endpoint criado. Para criar um terminal Remoto, especifique `Remoting`.
* **Descrição**: Especifica a descrição do ponto final.
* **Nome**: Especifica o nome do ponto final.
* **Valor** do identificador de serviço: Especifica o serviço ao qual o ponto de extremidade pertence. Por exemplo, para adicionar um terminal Remoto ao processo que é introduzido nesta seção (um processo se torna um serviço quando é ativado no Workbench), especifique `EncryptDocument`.
* **Nome** da operação: Especifica o nome da operação que é invocada usando o ponto final. Ao criar um terminal Remoto, especifique um caractere curinga (&amp;ast;).

**Criar um terminal Remoto**

Depois de definir os atributos de ponto de extremidade Remoto, você pode criar um ponto de extremidade Remota para um serviço.

**Ativar o ponto final**

Depois de criar um novo terminal, é necessário ativá-lo. Quando um terminal Remoting está ativado, ele permite que um cliente Flex chame o serviço.

**Consulte também:**

[Adicionar um terminal Remoto usando a API Java](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicionar um terminal Remoto usando a API Java {#add-a-remoting-endpoint-using-the-java-api}

Adicione um terminal Remoting usando a API Java:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto EndpointRegistry Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `EndpointRegistryClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Definir atributos de ponto final remoto.

   * Crie um `CreateEndpointInfo` objeto usando seu construtor.
   * Especifique o valor do identificador do conector, chamando o método do `CreateEndpointInfo` objeto `setConnectorId` e transmitindo o valor da string `Remoting`.
   * Especifique a descrição do ponto de extremidade chamando o método do `CreateEndpointInfo` objeto `setDescription` e transmitindo um valor de string que descreve o ponto de extremidade.
   * Especifique o nome do ponto de extremidade chamando o método do `CreateEndpointInfo` `setName` objeto e transmitindo um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o método do `CreateEndpointInfo` objeto `setServiceId` e transmitindo um valor de string que especifica o nome do serviço.
   * Especifique a operação que é invocada pelo método do `CreateEndpointInfo` `setOperationName` objeto e transmitindo um valor de string que especifica o nome da operação. Para um terminal Remoto, especifique um caractere curinga (&amp;ast;).

1. Criar um terminal Remoto.

   Crie o ponto de extremidade chamando o `EndpointRegistryClient` método do `createEndpoint` objeto e transmitindo o `CreateEndpointInfo` objeto. Esse método retorna um `Endpoint` objeto que representa o novo terminal Remoto.

1. Ative o terminal.

   Ative o terminal chamando o `EndpointRegistryClient` método do `enable` objeto e transmitindo o `Endpoint` objeto que foi retornado pelo `createEndpoint` método.

**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Adicionar um terminal Remoting usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Adicionando pontos finais do TaskManager {#adding-taskmanager-endpoints}

Você pode adicionar programaticamente um terminal do TaskManager a um serviço usando a API Java do AEM Forms. Ao adicionar um terminal do TaskManager a um serviço, você permite que um usuário do Workspace chame o serviço. Ou seja, um usuário que trabalha no Workspace pode chamar um processo que tem um terminal do TaskManager correspondente.

>[!NOTE]
>
>Não é possível adicionar um terminal do TaskManager usando serviços da Web.

### Resumo das etapas {#summary_of_steps-5}

Para adicionar um terminal do TaskManager a um serviço, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um `EndpointRegistryClient` objeto.
1. Crie uma categoria para o terminal.
1. Defina os atributos do ponto de extremidade do TaskManager.
1. Criar um terminal do TaskManager.
1. Ative o terminal.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

**Criar um objeto de Cliente EndpointRegistry**

Antes de poder adicionar programaticamente um terminal do TaskManager, é necessário criar um `EndpointRegistryClient` objeto.

**Criar uma categoria para o terminal**

As Categorias são usadas para organizar serviços no Workspace. Ou seja, um usuário do Workspace pode chamar um serviço que tenha um terminal do TaskManager selecionando uma categoria no Workspace. Ao criar um terminal do TaskManager, você pode fazer referência a uma categoria existente ou criar programaticamente uma nova categoria.

>[!NOTE]
>
>Esta seção cria uma nova categoria como parte da adição de um terminal do TaskManager a um serviço.

**Definir atributos de ponto de extremidade do TaskManager**

Para criar um terminal do TaskManager para um serviço, especifique os seguintes valores:

* **Identificador** do conector: Especifica o tipo de endpoint criado. Para criar um terminal do TaskManager, especifique `TaskManagerConnector`.
* **Descrição**: Especifica a descrição do ponto final.
* **Nome**: Especifica o nome do ponto final.
* **Identificador** do serviço: Especifica o serviço ao qual o ponto de extremidade pertence.
* **Categoria**: Especifica um valor de identificador de categoria associado ao terminal do TaskManager.
* **Nome** da operação: Geralmente, ao criar um terminal do TaskManager para um serviço originado de um processo criado no Workbench, o nome da operação é `invoke`.

**Criar um terminal do TaskManager**

Depois de definir atributos de ponto de extremidade do TaskManager, você pode criar um ponto de extremidade do TaskManager para um serviço.

**Ativar o ponto final**

Depois de criar um novo terminal, é necessário ativá-lo. Quando o terminal está ativado, ele pode ser usado para chamar o serviço a partir do Workspace. Depois de ativar o terminal, você pode visualização-lo no console de administração.

**Consulte também:**

[Adicionar um terminal do TaskManager usando a API Java](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicionar um terminal do TaskManager usando a API Java {#add-a-taskmanager-endpoint-using-the-java-api}

Adicione um terminal do TaskManager usando a API Java:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto EndpointRegistry Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `EndpointRegistryClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Crie uma categoria para o terminal.

   * Crie um `CreateEndpointCategoryInfo` objeto usando seu construtor e transmitindo os seguintes valores:

      * Um valor de string que especifica o valor identificador da categoria
      * Um valor de string que especifica a descrição da categoria
   * Crie a categoria chamando o `EndpointRegistryClient` método do `createEndpointCategory` objeto e transmitindo o `CreateEndpointCategoryInfo` objeto. Esse método retorna um `EndpointCategory` objeto que representa a nova categoria.


1. Defina os atributos do ponto de extremidade do TaskManager.

   * Crie um `CreateEndpointInfo` objeto usando seu construtor.
   * Especifique o valor do identificador do conector, chamando o método do `CreateEndpointInfo` objeto `setConnectorId` e transmitindo o valor da string `TaskManagerConnector`.
   * Especifique a descrição do ponto de extremidade chamando o método do `CreateEndpointInfo` objeto `setDescription` e transmitindo um valor de string que descreve o ponto de extremidade.
   * Especifique o nome do ponto de extremidade chamando o método do `CreateEndpointInfo` `setName` objeto e transmitindo um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o método do `CreateEndpointInfo` objeto `setServiceId` e transmitindo um valor de string que especifica o nome do serviço.
   * Especifique a categoria à qual o ponto de extremidade pertence, chamando o método do `CreateEndpointInfo` objeto `setCategoryId` e transmitindo um valor de string que especifica o valor do identificador de categoria. Você pode invocar o método do `EndpointCategory` objeto para obter o valor identificador dessa categoria `getId` .
   * Especifique a operação que é invocada chamando o método do `CreateEndpointInfo` `setOperationName` objeto e transmitindo um valor de string que especifica o nome da operação. Normalmente, ao criar um `TaskManager` terminal para um serviço que tenha origem em um processo criado no Workbench, o nome da operação é `invoke`.

1. Criar um terminal do TaskManager.

   Crie o ponto de extremidade chamando o `EndpointRegistryClient` método do `createEndpoint` objeto e transmitindo o `CreateEndpointInfo` objeto. Este método retorna um `Endpoint` objeto que representa o novo endpoint do TaskManager.

1. Ative o terminal.

   Ative o terminal chamando o `EndpointRegistryClient` método do `enable` objeto e transmitindo o `Endpoint` objeto que foi retornado pelo `createEndpoint` método.

**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Adicionar um terminal do TaskManager usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Modificação de Pontos de Extremidade {#modifying-endpoints}

Você pode modificar programaticamente um terminal existente usando a API Java de formulários AEM. Ao modificar um endpoint, você pode alterar o comportamento do endpoint. Considere, por exemplo, um endpoint de Pasta assistida que especifica uma pasta que é usada como a pasta assistida. Você pode modificar programaticamente os valores de configuração que pertencem ao ponto final da Pasta assistida, resultando em outra pasta funcionando como a pasta assistida. Para obter informações sobre os valores de configuração que pertencem a um endpoint de Pasta assistida, consulte [Adicionar pontos finais](programmatically-endpoints.md#adding-watched-folder-endpoints)de pasta monitorada.

Para demonstrar como modificar um terminal, esta seção modifica um terminal de Pasta assistida alterando a pasta que se comporta como a pasta assistida.

>[!NOTE]
>
>Não é possível modificar um terminal usando serviços da Web.

### Resumo das etapas {#summary_of_steps-6}

Para modificar um terminal, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um `EndpointRegistryClient` objeto.
1. Recupere o terminal.
1. Especifique novos valores de configuração.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

**Criar um objeto de Cliente EndpointRegistry**

Para modificar programaticamente um terminal, é necessário criar um `EndpointRegistryClient` objeto.

**Recuperar o ponto de extremidade para modificar**

Antes de modificar um terminal, é necessário recuperá-lo. Para recuperar um terminal, é necessário conectar-se como um usuário que pode acessar um terminal. É recomendável conectar-se como administrador. (Consulte [Configuração das propriedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexão).

Você pode recuperar um terminal recuperando uma lista de pontos finais. Em seguida, você pode iterar pela lista, pesquisando o endpoint específico a ser removido. Por exemplo, você pode localizar um terminal determinando o serviço que corresponde ao terminal e o tipo de terminal. Ao localizar o terminal, é possível modificá-lo.

**Especificar novos valores de configuração**

Ao modificar um terminal, especifique novos valores de configuração. Por exemplo, para modificar um endpoint de Pasta assistida, redefina todos os valores de configuração de endpoint de Pasta assistida, não apenas aqueles que você deseja modificar. Para obter informações sobre os valores de configuração que pertencem a um endpoint de Pasta assistida, consulte [Adicionar pontos finais](programmatically-endpoints.md#adding-watched-folder-endpoints)de pasta monitorada.

>[!NOTE]
>
>Para obter informações sobre valores de configuração que pertencem a um ponto de extremidade de email, consulte [Adicionar pontos de extremidade](programmatically-endpoints.md#adding-email-endpoints)de email.

>[!NOTE]
>
>Não é possível modificar o serviço chamado pelo ponto final. Se você tentar modificar o serviço, uma exceção será lançada. Para modificar o serviço associado a um determinado terminal, remova o terminal e crie um novo. (Consulte [Remoção de pontos de extremidade](programmatically-endpoints.md#removing-endpoints).)

**Consulte também:**

[Modificação de um terminal usando a API Java](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Modificação de um terminal usando a API Java {#modifying-an-endpoint-using-the-java-api}

Modifique um terminal usando a API Java:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto EndpointRegistry Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `EndpointRegistryClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere o terminal para modificá-lo.

   * Recupere uma lista de todos os pontos de extremidade aos quais o usuário atual (especificado nas propriedades de conexão) pode acessar chamando o `EndpointRegistryClient` método do `getEndpoints` objeto e transmitindo um `PagingFilter` objeto que atue como filtro. Você pode passar um `(PagingFilter)null` valor para retornar todos os pontos de extremidade. Esse método retorna um `java.util.List` objeto no qual cada elemento é um `Endpoint` objeto. Para obter informações sobre um `PagingFilter` objeto, consulte Referência [da API do](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.
   * Iterar pelo `java.util.List` objeto para determinar se ele tem pontos de extremidade. Se houver pontos de extremidade, cada elemento será uma `EndPoint` instância.
   * Determine o serviço que corresponde a um ponto final chamando o método do `EndPoint` objeto `getServiceId` . Esse método retorna um valor de string que especifica o nome do serviço.
   * Determine o tipo de endpoint chamando o `EndPoint` método do `getConnectorId` objeto. Esse método retorna um valor de string que especifica o tipo de endpoint. Por exemplo, se o endpoint for um endpoint de Pasta assistida, esse método retornará `WatchedFolder`.

1. Especifique novos valores de configuração.

   * Crie um `ModifyEndpointInfo` objeto chamando seu construtor.
   * Para cada valor de configuração a ser definido, chame o `ModifyEndpointInfo` método do `setConfigParameterAsText` objeto. Por exemplo, para definir o valor de configuração de url, chame o método do `ModifyEndpointInfo` objeto `setConfigParameterAsText` e transmita os seguintes valores:

      * Um valor de string que especifica o nome do valor de configuração. Por exemplo, para definir o valor de `url` configuração, especifique `url`.
      * Um valor de string que especifica o valor da configuração. Para definir um valor para o valor de `url` configuração, especifique o local da pasta monitorada.
   * Chame o `EndpointRegistryClient` método do `modifyEndpoint` objeto e passe o `ModifyEndpointInfo` objeto.


**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Modificação de um terminal usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Remoção de pontos de extremidade {#removing-endpoints}

Você pode remover programaticamente um terminal de um serviço usando a API Java de formulários AEM. Depois de remover um terminal, o serviço não pode ser chamado usando o método de invocação que o terminal ativou. Por exemplo, se você remover um terminal SOAP de um serviço, não será possível chamar o serviço usando o modo SOAP.

Para demonstrar como remover um ponto de extremidade de um serviço, esta seção remove um ponto de extremidade EJB de um serviço chamado *EncryptDocument*.

>[!NOTE]
>
>Não é possível remover um terminal usando serviços da Web.

### Resumo das etapas {#summary_of_steps-7}

Para remover um terminal de um serviço, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um `EndpointRegistryClient` objeto.
1. Recupere o terminal.
1. Remova o terminal.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

**Criar um objeto Cliente EndpointRegistry**

Para remover programaticamente um terminal, é necessário criar um `EndpointRegistryClient` objeto.

**Recuperar o ponto de extremidade a ser removido**

Antes de remover um terminal, é necessário recuperá-lo. Para recuperar um terminal, é necessário conectar-se como um usuário que pode acessar um terminal. É recomendável conectar-se como administrador. (Consulte [Configuração das propriedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexão).

Você pode recuperar um terminal recuperando uma lista de pontos finais. Em seguida, você pode iterar pela lista, pesquisando o endpoint específico a ser removido. Por exemplo, você pode localizar um terminal determinando o serviço que corresponde ao terminal e o tipo de terminal. Ao localizar o terminal, você pode removê-lo.

**Remover o ponto final**

Depois de criar um novo terminal, é necessário ativá-lo. Quando o terminal está ativado, ele pode ser usado para chamar o serviço. Depois de ativar o terminal, você pode visualização-lo no console de administração.

**Consulte também:**

[Remoção de um terminal usando a API Java](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Remoção de um terminal usando a API Java {#removing-an-endpoint-using-the-java-api}

Remova um terminal usando a API Java:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto EndpointRegistry Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `EndpointRegistryClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere o terminal a ser removido.

   * Recupere uma lista de todos os pontos de extremidade aos quais o usuário atual (especificado nas propriedades de conexão) tem acesso, invocando o `EndpointRegistryClient` método do `getEndpoints` objeto e transmitindo um `PagingFilter` objeto que atua como filtro. Você pode passar `(PagingFilter)null` para retornar todos os pontos de extremidade. Esse método retorna um `java.util.List` objeto no qual cada elemento é um `Endpoint` objeto.
   * Iterar pelo `java.util.List` objeto para determinar se ele tem pontos de extremidade. Se houver pontos de extremidade, cada elemento será uma `EndPoint` instância.
   * Determine o serviço que corresponde a um ponto final chamando o método do `EndPoint` objeto `getServiceId` . Esse método retorna um valor de string que especifica o nome do serviço.
   * Determine o tipo de terminal chamando o `EndPoint` método do `getConnectorId` objeto. Esse método retorna um valor de string que especifica o tipo de endpoint. Por exemplo, se o endpoint for um endpoint EJB, esse método retornará `EJB`.

1. Remova o terminal.

   Remova o ponto de extremidade chamando o `EndpointRegistryClient` método do `remove` objeto e transmitindo o `EndPoint` objeto que representa o ponto de extremidade a ser removido.

**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Remoção de um terminal usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Recuperando informações do conector do ponto de extremidade {#retrieving-endpoint-connector-information}

Você pode recuperar programaticamente informações sobre conectores de ponto de extremidade usando a API de formulários do AEM. Um conector permite que um terminal chame um serviço usando vários métodos de invocação. Por exemplo, um conector de Pasta assistida permite que um terminal chame um serviço usando pastas monitoradas. Ao recuperar informações programaticamente sobre conectores de ponto de extremidade, você pode recuperar valores de configuração associados a um conector, como quais valores de configuração são obrigatórios e quais são opcionais.

Para demonstrar como recuperar informações sobre conectores de ponto de extremidade, esta seção recupera informações sobre um conector de Pasta assistida. (Consulte [Adicionando Pontos de Extremidade](programmatically-endpoints.md#adding-watched-folder-endpoints)da Pasta Observada.)

>[!NOTE]
>
>Não é possível recuperar informações sobre pontos finais usando serviços da Web.

>[!NOTE]
>
>Este tópico usa a `ConnectorRegistryClient` API para recuperar informações sobre conectores de ponto de extremidade. (Consulte Referência [da API do](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.)

### Resumo das etapas {#summary_of_steps-8}

Para recuperar as informações do conector do ponto de extremidade, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um `ConnectorRegistryClient` objeto.
1. Especifique o tipo de conector.
1. Recuperar valores de configuração.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, substitua adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms é implantado. Para obter informações sobre a localização de todos os arquivos JAR do AEM Forms, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

**Criar um objeto ConnectorRegistry Client**

Para recuperar programaticamente as informações do conector do ponto de extremidade, crie um `ConnectorRegistryClient` objeto.

**Especificar o tipo de conector**

Especifique o tipo de conector a partir do qual recuperar informações. Os seguintes tipos de conectores existem:

* **EJB**: Permite que um aplicativo cliente chame um serviço usando o modo EJB.
* **SOAP**: Permite que um aplicativo cliente chame um serviço usando o modo SOAP.
* **Pasta** assistida: Permite que as pastas monitoradas chamem um serviço.
* **Email**: Permite que mensagens de email cheguem a um serviço.
* **Remoto**: Permite que um aplicativo cliente Flex chame um serviço.
* **TaskManagerConnector**: Permite que um usuário do Workspace chame um serviço de dentro do Workspace.

**Recuperar valores de configuração**

Depois de especificar o tipo de conector, você pode recuperar informações sobre o conector, como o valor de configuração suportado. Por exemplo, para qualquer conector, você pode determinar quais valores de configuração são obrigatórios e quais são opcionais.

**Consulte também:**

[Recuperar informações do conector do ponto de extremidade usando a API Java](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar informações do conector do ponto de extremidade usando a API Java {#retrieve-endpoint-connector-information-using-the-java-api}

Recupere informações do conector do ponto de extremidade usando a API Java:

1. Incluir arquivos de projeto. .

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto ConnectorRegistry Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `ConnectorRegistryClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Especifique o tipo de conector.

   Especifique o tipo de conector, chamando o método do `ConnectorRegistryClient` objeto `getEndpointDefinition` e transmitindo um valor de string que especifica o tipo de conector. Por exemplo, para especificar o tipo de conector de Pasta assistida, passe o valor da string `WatchedFolder`. Esse método retorna um `Endpoint` objeto que corresponde ao tipo de conector.

1. Recuperar valores de configuração.

   * Recupere os valores de configuração associados a esse ponto de extremidade, chamando o `Endpoint` método do `getConfigParameters` objeto. Esse método retorna uma matriz de `ConfigParameter` objetos.
   * Recupere informações sobre cada valor de configuração recuperando cada elemento dentro da matriz. Cada elemento é um `ConfigParameter` objeto. Você pode, por exemplo, determinar se o valor de configuração é obrigatório ou opcional chamando o método do `ConfigParameter` objeto `isRequired` . Se o valor de configuração for necessário, esse método retornará `true`.

**Consulte também:**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[Início rápido: Recuperando informações do conector do ponto de extremidade usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
