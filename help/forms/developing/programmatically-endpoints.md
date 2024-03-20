---
title: Gerenciando Endpoints Programaticamente
description: Use o serviço de Registro de Ponto de Extremidade para adicionar pontos de extremidade EJB, adicionar ponto de extremidade SOAP, adicionar pontos de extremidade de Pasta monitorada, adicionar pontos de extremidade de Email, adicionar pontos de extremidade de Comunicação Remota, adicionar pontos de extremidade do Gerenciador de Tarefas, modificar pontos de extremidade, remover pontos de extremidade e recuperar informações do conector do ponto de extremidade.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: b94dcca2-136b-4b7d-b5ce-544804575876
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '10800'
ht-degree: 1%

---

# Gerenciando Endpoints Programaticamente {#programmatically-managing-endpoints}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

**Sobre o Serviço de Registro de Ponto de Extremidade**

O serviço Registro de Ponto de Extremidade fornece a capacidade de gerenciar pontos de extremidade de forma programática. Você pode, por exemplo, adicionar os seguintes tipos de endpoints a um serviço:

* EJB
* SOAP
* Pasta monitorada
* Email
* (Obsoleto para formulários AEM) Comunicação remota
* Gerenciador de tarefas

>[!NOTE]
>
>SOAP, EJB e (obsoleto para formulários AEM no JEE) Os endpoints de comunicação remota são criados automaticamente para cada serviço ativado. Os endpoints SOAP e EJB ativam SOAP e EJB para todas as operações de serviço.

Um endpoint de Comunicação Remota permite que os clientes Flex chamem operações no serviço AEM Forms ao qual o endpoint é adicionado. Um destino do Flex com o mesmo nome do ponto de extremidade é criado, e os clientes do Flex podem criar RemoteObjects que apontem para esse destino para chamar operações no serviço relevante.

Os pontos de acesso de Email, Gerenciador de tarefas e Pasta monitorada expõem apenas uma operação específica do serviço. A adição desses endpoints requer uma segunda etapa de configuração para selecionar um método a ser chamado, definir parâmetros de configuração e especificar mapeamentos de parâmetros de entrada e saída.

Você pode organizar os pontos de extremidade do TaskManager em grupos chamados *categorias*. Essas categorias são expostas ao Espaço de trabalho por meio do TaskManager, com os usuários finais vendo os pontos de extremidade do TaskManager à medida que são categorizados. No Workspace, os usuários finais veem essas categorias no painel de navegação. Os endpoints dentro de cada categoria são exibidos como cartões de processo na página Iniciar processos no Workspace.

Você pode realizar essas tarefas usando o serviço Registro de Ponto de Extremidade:

* Adicionar pontos finais EJB. (Consulte [Adicionando pontos finais EJB](programmatically-endpoints.md#adding-ejb-endpoints).)
* Adicionar pontos de extremidade SOAP. (Consulte [Adicionando pontos de extremidade SOAP](programmatically-endpoints.md#adding-soap-endpoints).)
* Adicionar endpoints de pasta monitorados (consulte [Adicionar pontos de extremidade da pasta monitorada](programmatically-endpoints.md#adding-watched-folder-endpoints).)
* Adicionar pontos de extremidade de email. (Consulte [Adicionar pontos de extremidade de email](programmatically-endpoints.md#adding-email-endpoints).)
* Adicionar pontos de extremidade de Comunicação Remota. (Consulte [Adicionando Pontos de Extremidade de Comunicação Remota](programmatically-endpoints.md#adding-remoting-endpoints).)
* Adicionar pontos de extremidade do Gerenciador de Tarefas (Consulte [Adicionando pontos finais do Gerenciador de Tarefas](programmatically-endpoints.md#adding-taskmanager-endpoints).)
* Modifique endpoints (Consulte [Modificação de Pontos de Extremidade](programmatically-endpoints.md#modifying-endpoints).)
* Remover pontos de extremidade (Consulte [Removendo Pontos de Extremidade](programmatically-endpoints.md#removing-endpoints).)
* Recuperar informações do conector do ponto de extremidade (Consulte [Recuperando Informações do Conector do Ponto de Extremidade](programmatically-endpoints.md#retrieving-endpoint-connector-information).)

## Adicionando pontos finais EJB {#adding-ejb-endpoints}

Você pode adicionar programaticamente um endpoint EJB a um serviço usando a API Java do AEM Forms. Adicionando um ponto final EJB a um serviço, você está permitindo que uma aplicação cliente chame o serviço usando o modo EJB. Ou seja, ao definir as propriedades de conexão necessárias para chamar o AEM Forms, você pode selecionar o modo EJB. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>Não é possível adicionar um ponto final EJB usando serviços Web.

>[!NOTE]
>
>Normalmente, um ponto final EJB é adicionado a um serviço por padrão. No entanto, um ponto final EJB pode ser adicionado a um processo que é implantado programaticamente ou quando um ponto final EJB foi removido e deve ser adicionado novamente.

### Resumo das etapas {#summary-of-steps}

Para adicionar um ponto final EJB a um serviço, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um `EndpointRegistry Client` objeto.
1. Definir atributos de ponto final EJB.
1. Criar um ponto final EJB.
1. Ative o endpoint.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto Cliente EndpointRegistry**

Antes de adicionar programaticamente um endpoint EJB, você deve criar um `EndpointRegistryClient` objeto.

**Definir atributos de ponto final EJB**

Para criar um endpoint EJB para um serviço, especifique os seguintes valores:

* **Identificador do conector**: especifica o tipo de ponto de extremidade a ser criado. Para criar um endpoint EJB, especifique `EJB`.
* **Descrição**: especifica a descrição do ponto de extremidade.
* **Nome**: especifica o nome do ponto de extremidade.
* **Identificador de serviço**: especifica o serviço ao qual o ponto de extremidade pertence.
* **Nome da operação**: especifica o nome da operação que é invocada usando o ponto de extremidade. Ao criar um endpoint EJB, especifique um caractere curinga ( `*`). No entanto, se você quiser especificar uma operação específica em vez de chamar todas as operações de serviço, especifique o nome da operação em vez de usar o caractere curinga ( `*`).

**Criar um ponto final EJB**

Após definir atributos de endpoint EJB, você pode criar um endpoint EJB para um serviço.

**Habilitar o endpoint**

Depois de criar um endpoint, você deve habilitá-lo. Depois de habilitar o endpoint, ele poderá ser usado para chamar o serviço. Após habilitar o endpoint, é possível visualizá-lo no console de administração.

**Consulte também**

[Adicionando um ponto final EJB usando a API Java](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicionando um ponto final EJB usando a API Java {#adding-an-ejb-endpoint-using-the-java-api}

Adicionar um ponto final EJB usando a API Java:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho de classe do projeto Java. (

1. Crie um objeto Cliente EndpointRegistry.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `EndpointRegistryClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Definir atributos de ponto final EJB.

   * Criar um `CreateEndpointInfo` usando seu construtor.
   * Especifique o valor do identificador do conector chamando o `CreateEndpointInfo` do objeto `setConnectorId` e transmitindo o valor da string `EJB`.
   * Especifique a descrição do ponto de extremidade chamando o `CreateEndpointInfo` do objeto `setDescription` e transmitindo um valor de string que descreve o endpoint.
   * Especifique o nome do endpoint chamando o `CreateEndpointInfo` do objeto `setName` e transmitindo um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o `CreateEndpointInfo` do objeto `setServiceId` e transmitindo um valor de string que especifica o nome do serviço.
   * Especifique a operação que é invocada chamando o `CreateEndpointInfo` do objeto `setOperationName` e passe um valor de string que especifique o nome da operação. Para pontos de extremidade SOAP e EJB, especifique um caractere curinga ( `*`), o que implica todas as operações.

1. Criar um ponto final EJB.

   Crie o endpoint chamando o `EndpointRegistryClient` do objeto `createEndpoint` e transmitindo o `CreateEndpointInfo` objeto. Este método retorna um valor de `Endpoint` objeto que representa o novo ponto final EJB.

1. Ative o endpoint.

   Ative o endpoint chamando o botão `EndpointRegistryClient` método enable do objeto e transmitindo o `Endpoint` objeto que foi retornado pelo `createEndpoint` método.

**Consulte também**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[QuickStart: adicionando um endpoint EJB usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Adicionando pontos de extremidade SOAP {#adding-soap-endpoints}

Você pode adicionar programaticamente um endpoint SOAP a um serviço usando a API Java do AEM Forms. Adicionando um ponto de extremidade SOAP, você habilita um aplicativo cliente a chamar o serviço usando o modo SOAP. Ou seja, ao definir as propriedades de conexão necessárias para chamar o AEM Forms, você pode selecionar o modo SOAP.

>[!NOTE]
>
>Não é possível adicionar um ponto de extremidade SOAP usando serviços da Web.

>[!NOTE]
>
>Normalmente, um ponto de extremidade SOAP é adicionado a um serviço por padrão. No entanto, um ponto de extremidade SOAP pode ser adicionado a um processo que é implantado programaticamente ou quando um ponto de extremidade SOAP foi removido e precisa ser adicionado novamente.

### Resumo das etapas {#summary_of_steps-1}

Para adicionar um ponto de extremidade SOAP a um serviço, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um `EndpointRegistryClient` objeto.
1. Definir atributos de ponto de extremidade SOAP.
1. Crie um ponto de extremidade SOAP.
1. Ative o endpoint.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Esses arquivos JAR são necessários para criar um endpoint SOAP. No entanto, você precisará adicionar arquivos JAR se usar o endpoint SOAP para chamar o serviço. Para obter informações sobre arquivos JAR do AEM Forms, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto Cliente EndpointRegistry**

Para adicionar programaticamente um ponto de extremidade SOAP a um serviço, você deve criar um `EndpointRegistryClient` objeto.

**Definir atributos de ponto de extremidade SOAP**

Para adicionar um ponto de extremidade SOAP a um serviço, especifique os seguintes valores:

* **Valor do identificador do conector**: especifica o tipo de ponto de extremidade a ser criado. Para criar um ponto de extremidade SOAP, especifique `SOAP`.
* **Descrição**: especifica a descrição do ponto de extremidade.
* **Nome**: especifica o nome do ponto de extremidade.
* **Valor do identificador de serviço**: especifica o serviço ao qual o ponto de extremidade pertence.
* **Nome da operação**: especifica o nome da operação que é invocada usando o ponto de extremidade. Ao criar um ponto de extremidade SOAP, especifique um caractere curinga ( `*`). No entanto, se você quiser especificar uma operação específica em vez de chamar todas as operações de serviço, especifique o nome da operação em vez de usar o caractere curinga ( `*`).

**Criar um ponto de extremidade SOAP**

Após definir os atributos do ponto de extremidade SOAP, você pode criar um ponto de extremidade SOAP.

**Habilitar o endpoint**

Depois de criar um endpoint, você deve habilitá-lo. Quando o endpoint está habilitado, ele pode ser usado para chamar o serviço. Depois de habilitar o endpoint, você pode visualizá-lo no console de administração.

**Consulte também**

[Adicionar um endpoint SOAP usando a API Java](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicionar um endpoint SOAP usando a API Java {#add-a-soap-endpoint-using-the-java-api}

Adicionar um ponto de extremidade SOAP a um serviço usando a API Java:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto Cliente EndpointRegistry.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `EndpointRegistryClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Definir atributos de ponto de extremidade SOAP.

   * Criar um `CreateEndpointInfo` usando seu construtor.
   * Especifique o valor do identificador do conector chamando o `CreateEndpointInfo` do objeto `setConnectorId` e transmitindo o valor da string `SOAP`.
   * Especifique a descrição do ponto de extremidade chamando o `CreateEndpointInfo` do objeto `setDescription` e transmitindo um valor de string que descreve o endpoint.
   * Especifique o nome do endpoint chamando o `CreateEndpointInfo` do objeto `setName` e transmitindo um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o `CreateEndpointInfo` do objeto `setServiceId` e transmitindo um valor de string que especifica o nome do serviço.
   * Especifique a operação que é invocada chamando o `CreateEndpointInfo` do objeto `setOperationName` e transmitindo um valor de string que especifica o nome da operação. Para pontos de extremidade SOAP e EJB, especifique um caractere curinga ( `*`), o que implica todas as operações.

1. Crie um ponto de extremidade SOAP.

   Crie o endpoint chamando o `EndpointRegistryClient` do objeto `createEndpoint` e transmitindo o `CreateEndpointInfo` objeto. Este método retorna um valor de `Endpoint` objeto que representa o novo ponto de extremidade SOAP.

1. Ative o endpoint.

   Ative o endpoint chamando o botão `EndpointRegistryClient` método enable do objeto e transmita o `Endpoint` objeto que foi retornado pelo `createEndpoint` método.

**Consulte também**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[QuickStart: adicionando um endpoint SOAP usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Adicionar pontos de extremidade da pasta monitorada {#adding-watched-folder-endpoints}

Você pode adicionar programaticamente um endpoint de Pasta monitorada a um serviço usando a API Java do AEM Forms. Ao adicionar um endpoint de Pasta monitorada, você permite que os usuários coloquem um arquivo (como um arquivo de PDF) em uma pasta. Quando o arquivo é colocado na pasta, o serviço configurado é chamado e manipula o arquivo. Depois que o serviço executa a operação especificada, ele salva o arquivo modificado em uma pasta de saída especificada. Uma pasta monitorada é configurada para ser digitalizada em um intervalo de taxa fixa ou com uma programação cron, como toda segunda, quarta e sexta ao meio-dia.

Para fins de adicionar programaticamente um endpoint de Pasta monitorada a um serviço, considere o seguinte processo de vida curta chamado *EncryptDocument*. (Consulte [Noções básicas sobre processos do AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

Esse processo aceita um documento de PDF não seguro como valor de entrada e, em seguida, passa o documento de PDF não seguro para o do serviço de criptografia `EncryptPDFUsingPassword` operação. O documento PDF é criptografado com uma senha e o documento PDF criptografado com senha é o valor de saída desse processo. O nome do valor de entrada (o documento PDF não seguro) é `InDoc` e o tipo de dados for `com.adobe.idp.Document`. O nome do valor de saída (o documento PDF criptografado por senha) é `SecuredDoc` e o tipo de dados for `com.adobe.idp.Document`.

>[!NOTE]
>
>Não é possível adicionar um ponto de extremidade de Pasta monitorada usando serviços da Web.

### Resumo das etapas {#summary_of_steps-2}

Para adicionar um ponto de extremidade de Pasta monitorada a um serviço, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um `EndpointRegistryClient` objeto.
1. Defina atributos de ponto de extremidade da Pasta monitorada.
1. Especifique os valores de configuração.
1. Defina os valores do parâmetro de entrada.
1. Defina um valor de parâmetro de saída.
1. Crie um ponto de extremidade de Pasta monitorada.
1. Ative o endpoint.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto Cliente EndpointRegistry**

Para adicionar programaticamente um endpoint de Pasta monitorada, você deve criar um `EndpointRegistryClient` objeto.

**Definir atributos de ponto de extremidade da pasta monitorada**

Para criar um ponto final de Pasta monitorada para um serviço, especifique os seguintes valores:

* **Identificador do conector**: especifica o tipo de ponto de extremidade criado. Para criar um ponto de extremidade de Pasta monitorada, especifique `WatchedFolder`.
* **Descrição**: especifica a descrição do ponto de extremidade.
* **Nome**: especifica o nome do ponto de extremidade.
* **Identificador de serviço**: especifica o serviço ao qual o ponto de extremidade pertence. Por exemplo, para adicionar um endpoint de Pasta monitorada ao processo introduzido nesta seção (um processo se torna um serviço quando ativado usando o Workbench), especifique `EncryptDocument`.
* **Nome da operação**: especifica o nome da operação que é invocada usando o ponto de extremidade. Normalmente, ao criar um endpoint de Pasta monitorada para um serviço que se originou de um processo criado no Workbench, o nome da operação é `invoke`.

**Especificar valores de configuração**

Especifique os valores de configuração para um ponto de extremidade de Pasta monitorada ao adicionar programaticamente um ponto de extremidade de Pasta monitorada a um serviço. Esses valores de configuração são especificados por um administrador se um endpoint de Pasta monitorada for adicionado usando o console de administração.

A lista a seguir especifica os valores de configuração que são definidos quando você adiciona programaticamente um ponto de extremidade de Pasta monitorada a um serviço:

* **url**: especifica o local da pasta monitorada. Em um ambiente clusterizado, esse valor deve apontar para uma pasta de rede compartilhada que possa ser acessada de todos os computadores no cluster.
* **assíncrono**: identifica o tipo de invocação como assíncrono ou síncrono. Processos transitórios e síncronos só podem ser chamados de forma síncrona. O valor padrão é true. É recomendável o modo assíncrono.
* **cronExpression**: usado pelo quartzo para agendar a pesquisa do diretório de entrada.
* **purgeDuration**: este é um atributo obrigatório. Os arquivos e pastas na pasta de resultados são removidos quando são mais antigos que esse valor. Esse valor é medido em dias. Esse atributo é útil para garantir que a pasta de resultados não fique cheia. Um valor de -1 dias indica que a pasta de resultados nunca deve ser excluída. O valor padrão é -1.
* **repeatInterval**: o intervalo, em segundos, para verificar a pasta monitorada para entrada. A menos que a limitação esteja habilitada, esse valor deve ser maior do que o tempo médio para processar um trabalho; caso contrário, o sistema pode ficar sobrecarregado. O valor padrão é 5.
* **repeatCount**: o número de vezes que uma pasta monitorada verifica a pasta ou o diretório. Um valor de -1 indica varredura indefinida. O valor padrão é -1.
* **throttleOn**: limita o número de trabalhos de Pastas monitoradas que podem ser processados a qualquer momento. O número máximo de trabalhos é determinado pelo valor batchSize.
* **userName**: o nome de usuário usado ao chamar um serviço de destino da Pasta monitorada. Esse valor é obrigatório. O valor padrão é SuperAdmin.
* **domainName**: o domínio do usuário. Esse valor é obrigatório. O valor padrão é DefaultDom.
* **batchSize**: O número de arquivos ou pastas a serem selecionados por verificação. Use esse valor para evitar uma sobrecarga no sistema; a varredura de muitos arquivos de uma vez pode resultar em falha. O valor padrão é 2.
* **waitTime**: o tempo, em milissegundos, que deve ser aguardado antes de verificar uma pasta ou um arquivo após a criação. Por exemplo, se o tempo de espera for de 36.000.000 milissegundos (uma hora) e o arquivo tiver sido criado há um minuto, esse arquivo será selecionado após 59 minutos ou mais. Esse atributo é útil para garantir que um arquivo ou pasta seja copiado completamente para a pasta de entrada. Por exemplo, se você tiver um arquivo grande para processar e ele levar dez minutos para ser baixado, defina o tempo de espera como 10&amp;ast;60 &amp;ast;1000 milissegundos. Essa configuração impede que a pasta monitorada verifique o arquivo se ele não estiver aguardando dez minutos. O valor padrão é 0.
* **excludeFilePattern**: o padrão usado por uma pasta monitorada para determinar quais arquivos e pastas serão verificados e selecionados. Qualquer arquivo ou pasta que tenha esse padrão não será examinado para processamento. Essa configuração é útil quando a entrada é uma pasta que contém vários arquivos. O conteúdo da pasta pode ser copiado para uma pasta que tenha um nome que será selecionado pela pasta monitorada. Esta etapa impede que a pasta monitorada selecione uma pasta para processamento antes que ela seja completamente copiada para a pasta de entrada. Por exemplo, se o valor excludeFilePattern for `data*`, todos os arquivos e pastas que corresponderem `data*` não são coletadas. Isso inclui arquivos e pastas chamados `data1`, `data2`e assim por diante. Além disso, o padrão pode ser complementado com padrões curingas para especificar padrões de arquivo. A pasta monitorada modifica a expressão regular para suportar padrões curingas, como `*.*` e `*.pdf`. Esses padrões curingas não são suportados por expressões regulares.
* **includeFilePattern**: o padrão que a pasta monitorada usa para determinar quais pastas e arquivos serão verificados e coletados. Por exemplo, se esse valor for `*`, todos os arquivos e pastas que corresponderem `input*` são coletadas. Isso inclui arquivos e pastas chamados `input1`, `input2`e assim por diante. O valor padrão é `*`. Esse valor indica todos os arquivos e pastas. Além disso, o padrão pode ser complementado com padrões curingas para especificar padrões de arquivo. A pasta monitorada modifica a expressão regular para suportar padrões curingas, como `*.*` e `*.pdf`. Esses padrões curingas não são suportados por expressões regulares. Esse valor é obrigatório.
* **resultFolderName**: a pasta onde os resultados salvos são armazenados. Esse local pode ser um caminho de diretório absoluto ou relativo. Se os resultados não aparecerem nessa pasta, verifique a pasta de falha. Arquivos somente leitura não são processados e serão salvos na pasta de falha. O valor padrão é `result/%Y/%M/%D/`. Esta é a pasta de resultados dentro da pasta monitorada.
* **preserveFolderName**: o local onde os arquivos são armazenados após a verificação e a coleta bem-sucedidas. Esse local pode ser um caminho de diretório absoluto, relativo ou nulo. O valor padrão é `preserve/%Y/%M/%D/`.
* **failureFolderName**: a pasta onde os arquivos de falha são salvos. Este local é sempre relativo à pasta monitorada. Arquivos somente leitura não são processados e serão salvos na pasta de falha. O valor padrão é `failure/%Y/%M/%D/`.
* **preserveOnFailure**: preserva os arquivos de entrada se houver uma falha ao executar a operação em um serviço. O valor padrão é true.
* **overwriteDuplicateFilename**: quando definido como verdadeiro, os arquivos na pasta de resultados e na pasta de preservação são substituídos. Quando definido como false, os arquivos e as pastas que têm um sufixo de índice numérico são usados para o nome. O valor padrão é false.

**Definir valores de parâmetro de entrada**

Ao criar um endpoint de Pasta monitorada, você deve definir valores de parâmetro de entrada. Ou seja, você deve descrever os valores de entrada transmitidos para a operação chamada pela pasta monitorada. Por exemplo, considere o processo introduzido neste tópico. Ele tem um valor de entrada chamado `InDoc` e seu tipo de dados é `com.adobe.idp.Document`. Ao criar um endpoint de Pasta monitorada para esse processo (depois que um processo é ativado, ele se torna um serviço), você deve definir o valor do parâmetro de entrada.

Para definir valores de parâmetro de entrada necessários para um endpoint de Pasta monitorada, especifique os seguintes valores:

**Nome do parâmetro de entrada**: o nome do parâmetro de entrada. O nome de um valor de entrada é especificado na Bancada para um processo. Se o valor de entrada pertencer a uma operação de serviço (um serviço que não é um processo criado no Workbench), o nome de entrada será especificado no arquivo component.xml. Por exemplo, o nome do parâmetro de entrada para o processo introduzido nesta seção é `InDoc`.

**Tipo de mapeamento**: usado para configurar os valores de entrada necessários para chamar a operação de serviço. Há dois tipos de mapeamento:

* `Literal`: o endpoint da Pasta monitorada usa o valor inserido no campo como ele é exibido. Todos os tipos básicos de Java são compatíveis. Por exemplo, se uma API usar entradas como String, long, int e Boolean, a cadeia de caracteres será convertida no tipo adequado e o serviço será chamado.
* `Variable`: o valor inserido é um padrão de arquivo que a pasta monitorada usa para escolher a entrada. Por exemplo, se você selecionar Variável para o tipo de mapeamento e o documento de entrada precisar ser um arquivo PDF, será possível especificar `*.pdf`como o valor de mapeamento.

**Mapeamento de valor**: especifica o valor do tipo de mapeamento. Por exemplo, se você selecionar um `Variable` tipo de mapeamento, é possível especificar `*.pdf` como o padrão do arquivo.

**Tipo de dados**: especifica o tipo de dados do(s) valor(es) de entrada. Por exemplo, o tipo de dados do valor de entrada do processo introduzido nesta seção é `com.adobe.idp.Document`.

**Definir um valor de parâmetro de saída**

Ao criar um endpoint de Pasta monitorada, você deve definir um valor de parâmetro de saída. Ou seja, você deve descrever o valor de saída retornado pelo serviço chamado pelo endpoint da Pasta monitorada. Por exemplo, considere o processo introduzido neste tópico. Ele tem um valor de saída chamado `SecuredDoc` e seu tipo de dados é `com.adobe.idp.Document`. Ao criar um endpoint de Pasta monitorada para esse processo (depois que um processo é ativado, ele se torna um serviço), você deve definir o valor do parâmetro de saída.

Para definir um valor de parâmetro de saída necessário para um endpoint de Pasta monitorada, especifique os seguintes valores:

**Nome do parâmetro de saída**: o nome do parâmetro de saída. O nome de um valor de saída de processo é especificado no Workbench. Se o valor de saída pertencer a uma operação de serviço (um serviço que não é um processo criado no Workbench), o nome da saída será especificado no arquivo component.xml. Por exemplo, o nome do parâmetro de saída para o processo introduzido nesta seção é `SecuredDoc`.

**Tipo de mapeamento**: usado para configurar a saída do serviço e da operação. As opções disponíveis são as seguintes:

* Se o serviço retornar um único objeto (um único documento), o padrão será `%F.pdf` e o destino de origem é sourcefilename.pdf. Por exemplo, o processo introduzido nesta seção retorna um único documento. Como resultado, o tipo de mapeamento pode ser definido como `%F.pdf` ( `%F` significa usar o nome de arquivo fornecido). O padrão `%E` especifica a extensão do documento de entrada.
* Se o serviço retornar uma lista, o padrão será `Result\%F\`, e o destino de origem é Result\sourcefilename\source1 (saída 1) e Result\sourcefilename\source2 (saída 2).
* Se o serviço retornar um mapa, o padrão será `Result\%F\`e o destino de origem é Result\sourcefilename\file1 e Result\sourcefilename\file2. Se o mapa tiver mais de um objeto, o padrão será `Result\%F.pdf` e o destino de origem é Result\sourcefilename1.pdf (saída 1), Result\sourcefilenam2.pdf (saída 2) e assim por diante.

**Tipo de dados**: especifica o tipo de dados do valor de retorno. Por exemplo, o tipo de dados do valor de retorno do processo introduzido nesta seção é `com.adobe.idp.Document`.

**Criar um ponto de extremidade de Pasta monitorada**

Depois de definir os atributos do endpoint, os valores de configuração e os valores de parâmetro de entrada e saída, você deve criar o endpoint Pasta monitorada.

**Habilitar o endpoint**

Depois de criar um endpoint de Pasta monitorada, você deve ativá-lo. Quando o endpoint está habilitado, ele pode ser usado para chamar o serviço. Após habilitar o endpoint, é possível visualizá-lo no console de administração.

**Consulte também**

[Adicionar um endpoint de pasta monitorada usando a API Java](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicionar um endpoint de pasta monitorada usando a API Java {#add-a-watched-folder-endpoint-using-the-java-api}

Adicione um endpoint de Pasta monitorada usando a API Java do AEM Forms:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto Cliente EndpointRegistry.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `EndpointRegistryClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Defina atributos de ponto de extremidade da Pasta monitorada.

   * Criar um `CreateEndpointInfo` usando seu construtor.
   * Especifique o valor do identificador do conector chamando o `CreateEndpointInfo` do objeto `setConnectorId` e transmitindo o valor da string `WatchedFolder`.
   * Especifique a descrição do ponto de extremidade chamando o `CreateEndpointInfo` do objeto `setDescription` e transmitindo um valor de string que descreve o endpoint.
   * Especifique o nome do endpoint chamando o `CreateEndpointInfo` do objeto `setName` e transmitindo um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o `CreateEndpointInfo` do objeto `setServiceId` e transmitindo um valor de string que especifica o nome do serviço.
   * Especifique a operação que é invocada chamando o `CreateEndpointInfo` do objeto `setOperationName` e transmitindo um valor de string que especifica o nome da operação. Normalmente, ao criar um endpoint de Pasta monitorada para um serviço que se originou de um processo criado no Workbench, o nome da operação é chamado.

1. Especifique os valores de configuração.

   Para cada valor de configuração a ser definido para o endpoint da Pasta monitorada, você deve chamar o `CreateEndpointInfo` do objeto `setConfigParameterAsText` método. Por exemplo, para definir a variável `url` valor de configuração, chame o `CreateEndpointInfo` do objeto `setConfigParameterAsText` e passe os seguintes valores de string:

   * Um valor de string que especifica o nome do valor de configuração. Ao definir a variável `url` valor de configuração, especifique `url`.
   * Um valor de string que especifica o valor do valor de configuração. Ao definir a variável `url` valor de configuração, especifique o local da pasta monitorada.

   >[!NOTE]
   >
   >Para ver todos os valores de configuração definidos para o serviço EncryptDocument, consulte o exemplo de código Java localizado em [QuickStart: adicionando um endpoint de pasta monitorada usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api).

1. Defina os valores do parâmetro de entrada.

   Defina um valor de parâmetro de entrada chamando o `CreateEndpointInfo` do objeto `setInputParameterMapping` e passe os seguintes valores:

   * Um valor de string que especifica o nome do parâmetro de entrada. Por exemplo, o nome do parâmetro de entrada para o serviço EncryptDocument é `InDoc`.
   * Um valor de string que especifica o tipo de dados do parâmetro de entrada. Por exemplo, o tipo de dados do `InDoc` o parâmetro de entrada é `com.adobe.idp.Document`.
   * Um valor de string que especifica o tipo de mapeamento. Por exemplo, você pode especificar `variable`.
   * Um valor de string que especifica o valor do tipo de mapeamento. Por exemplo, você pode especificar &amp;ast;.pdf como o padrão do arquivo.

   >[!NOTE]
   >
   >Chame o `setInputParameterMapping` para cada valor de parâmetro de entrada a ser definido. Como o processo EncryptDocument tem apenas um parâmetro de entrada, é necessário chamar esse método uma vez.

1. Defina um valor de parâmetro de saída.

   Defina um valor de parâmetro de saída chamando o `CreateEndpointInfo` do objeto `setOutputParameterMapping` e passe os seguintes valores:

   * Um valor de string que especifica o nome do parâmetro de saída. Por exemplo, o nome do parâmetro de saída para o serviço EncryptDocument é `SecuredDoc`.
   * Um valor de string que especifica o tipo de dados do parâmetro de saída. Por exemplo, o tipo de dados do `SecuredDoc` o parâmetro de saída é `com.adobe.idp.Document`.
   * Um valor de string que especifica o tipo de mapeamento. Por exemplo, você pode especificar `%F.pdf`.

1. Crie um ponto de extremidade de Pasta monitorada.

   Crie o endpoint chamando o `EndpointRegistryClient` do objeto `createEndpoint` e transmitindo o `CreateEndpointInfo` objeto. Este método retorna um valor de `Endpoint` objeto que representa o ponto de extremidade da Pasta monitorada.

1. Ative o endpoint.

   Ative o endpoint chamando o botão `EndpointRegistryClient` do objeto `enable` e transmitindo o `Endpoint` objeto que foi retornado pelo `createEndpoint` método.

**Consulte também**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[QuickStart: adicionando um endpoint de pasta monitorada usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Arquivo constante de valores de configuração da pasta monitorada {#watched-folder-configuration-values-constant-file}

A variável [QuickStart: adicionando um endpoint de pasta monitorada usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) O usa um arquivo constante que deve fazer parte do projeto Java para compilar o início rápido. Esse arquivo constante representa valores de configuração que devem ser definidos ao adicionar um ponto de extremidade de Pasta monitorada. O código Java a seguir representa o arquivo de constante.

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

Você pode adicionar programaticamente um endpoint de email a um serviço usando a API Java do AEM Forms. Ao adicionar um endpoint de email, você permite que os usuários enviem uma mensagem de email com um ou mais anexos de arquivo para uma conta de email especificada. Em seguida, a operação de configuração do serviço é chamada e manipula os arquivos. Depois que o serviço executa a operação especificada, ele envia uma mensagem de email para o remetente com os arquivos modificados como anexos de arquivo.

Para fins de adição programática de um endpoint de email a um serviço, considere o seguinte processo de vida curta chamado *MyApplication\EncryptDocument*. Para obter informações sobre processos de vida curta, consulte [Noções básicas sobre processos do AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

Esse processo aceita um documento de PDF não seguro como valor de entrada e, em seguida, passa o documento de PDF não seguro para o do serviço de criptografia `EncryptPDFUsingPassword` operação. Esse processo criptografa o documento PDF com uma senha e retorna o documento PDF criptografado por senha como o valor de saída. O nome do valor de entrada (o documento PDF não seguro) é `InDoc` e o tipo de dados for `com.adobe.idp.Document`. O nome do valor de saída (o documento PDF criptografado por senha) é `SecuredDoc` e o tipo de dados for `com.adobe.idp.Document`.

>[!NOTE]
>
>Não é possível adicionar um terminal de email usando serviços da Web.

### Resumo das etapas {#summary_of_steps-3}

Para adicionar um terminal de email a um serviço, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um `EndpointRegistryClient` objeto.
1. Defina atributos de endpoint de email.
1. Especifique os valores de configuração.
1. Defina os valores do parâmetro de entrada.
1. Defina um valor de parâmetro de saída.
1. Crie o endpoint de email.
1. Ative o endpoint.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto Cliente EndpointRegistry**

Antes de adicionar programaticamente um endpoint de email, você deve criar um `EndpointRegistryClient` objeto.

**Definir atributos de ponto de extremidade de email**

Para criar um terminal de email para um serviço, especifique os seguintes valores:

* **Valor do identificador do conector**: especifica o tipo de ponto de extremidade criado. Para criar um endpoint de email, especifique `Email`.
* **Descrição**: especifica uma descrição para o ponto de extremidade.
* **Nome**: especifica o nome do ponto de extremidade.
* **Valor do identificador de serviço**: especifica o serviço ao qual o ponto de extremidade pertence. Por exemplo, para adicionar um terminal de email ao processo introduzido nesta seção (um processo se torna um serviço quando ativado usando o Workbench), especifique `EncryptDocument`.
* **Nome da operação**: especifica o nome da operação que é invocada usando o ponto de extremidade. Normalmente, ao criar um endpoint de email para um serviço que se originou de um processo criado no Workbench, o nome da operação é `invoke`.

**Especificar valores de configuração**

Especifique os valores de configuração para um endpoint de email ao adicionar programaticamente um endpoint de email a um serviço. Esses valores de configuração são especificados por um administrador se um endpoint de email for adicionado usando o console de administração.

>[!NOTE]
>
>A conta de email monitorada é uma conta especial usada somente para o endpoint de email. Esta conta não é uma conta de email de usuário comum. A conta de email de um usuário comum não deve ser configurada como a conta que o provedor de email usa, pois o provedor exclui mensagens de email da caixa de entrada após concluir a configuração das mensagens.

Os seguintes valores de configuração são definidos ao adicionar programaticamente um endpoint de email a um serviço:

* **cronExpression**: uma expressão cron se o email precisar ser agendado usando uma expressão cron.
* **repeatCount**: Número de vezes que o endpoint de email verifica a pasta ou o diretório. Um valor de -1 indica varredura indefinida. O valor padrão é -1.
* **repeatInterval**: a taxa de varredura, em segundos, que o destinatário usa para verificar se há e-mails de entrada. O valor padrão é 10.
* **startDelay**: O tempo de espera para verificação depois que o scheduler é iniciado. A hora padrão é 0.
* **batchSize**: o número de mensagens de email que o receptor processa por verificação para obter o desempenho ideal. Um valor -1 indica todos os emails. O valor padrão é 2.
* **userName**: O nome de usuário usado ao chamar um serviço do Target a partir de um email. O valor padrão é `SuperAdmin`.
* **domainName**: um valor de configuração obrigatório. O valor padrão é `DefaultDom`.
* **domainPattern**: especifica os padrões de domínio de emails de entrada que o provedor aceita. Por exemplo, se `adobe.com` for usado, somente o email do adobe.com for processado, o email de outros domínios será ignorado.
* **filePattern**: especifica os padrões de anexo de arquivo de entrada que o provedor aceita. Isso inclui arquivos que têm extensões de nome de arquivo específicas (&amp;ast;.dat, &amp;ast;.xml), arquivos que têm nomes específicos (dados) e arquivos que têm expressões compostas no nome e na extensão (&amp;ast;.[dD][aA]&#39;porta&#39;). O valor padrão é `*`.
* **recipientSuccessfulJob**: um endereço de email para o qual as mensagens são enviadas para indicar tarefas bem-sucedidas. Por padrão, uma mensagem de tarefa bem-sucedida é sempre enviada ao remetente. Se você digitar `sender`, os resultados de email são enviados ao remetente. Até 100 recipients são suportados. Especifique recipients adicionais com endereços de email, cada um separado por vírgula. Para desativar essa opção, deixe esse valor em branco. Em alguns casos, você pode acionar um processo e não quiser uma notificação por email sobre o resultado. O valor padrão é `sender`.
* **recipientFailedJob**: um endereço de email para o qual as mensagens são enviadas para indicar tarefas com falha. Por padrão, uma mensagem de tarefa com falha é sempre enviada ao remetente. Se você digitar `sender`, os resultados de email são enviados ao remetente. Até 100 recipients são suportados. Especifique recipients adicionais com endereços de email, cada um separado por vírgula. Para desativar essa opção, deixe esse valor em branco. O valor padrão é `sender`.
* **inboxHost**: O nome do host ou endereço IP da caixa de entrada que o provedor de email deve verificar.
* **inboxPort**: a porta usada pelo servidor de email. O valor padrão para POP3 é 110 e o valor padrão para IMAP é 143. Se o SSL estiver ativado, o valor default para POP3 será 995 e o valor default para IMAP será 993.
* **inboxProtocol**: O protocolo de email para o endpoint de email a ser usado para verificar a caixa de entrada. As opções são `IMAP` ou `POP3`. O servidor de e-mail do host da caixa de entrada deve suportar esses protocolos.
* **inboxTimeOut**: Tempo limite em segundos para o provedor de email aguardar as respostas da caixa de entrada. O valor padrão é 60.
* **inboxUser**: o nome de usuário necessário para fazer logon na conta de email. Dependendo do servidor de email e da configuração, essa pode ser apenas a parte do nome de usuário do email ou o endereço de email completo.
* **inboxPassword**: a senha do usuário da caixa de entrada.
* **inboxSSLEnabled**: Defina esse valor para forçar o provedor de email a usar SSL ao enviar mensagens de notificação de resultados ou erros. Verifique se o host IMAP ou POP3 é compatível com SSL.
* **smtpHost**: o nome do host do servidor de email para o qual o provedor de email envia resultados e mensagens de erro.
* **smtpPort**: o valor padrão para a porta SMTP é 25.
* **smtpUser**: a conta de usuário do provedor de email a ser usada quando ele enviar notificações por email de resultados e erros.
* **smtpPassword**: a senha da conta SMTP. Alguns servidores de email não exigem uma senha SMTP.
* **charSet**: o conjunto de caracteres usado pelo provedor de email. O valor padrão é `UTF-8`.
* **smtpSSLEnabled**: Defina esse valor para forçar o provedor de email a usar SSL ao enviar mensagens de notificação de resultados ou erros. Verifique se o host SMTP oferece suporte a SSL.
* **failedJobFolder**: especifica um diretório no qual armazenar resultados quando o servidor de email SMTP não estiver operacional.
* **assíncrono**: quando definido como síncrono, todos os documentos de entrada são processados e uma única resposta é retornada. Quando definido como assíncrono, uma resposta é enviada para cada documento de entrada processado. Por exemplo, um endpoint de email é criado para o processo introduzido neste tópico e uma mensagem de email é enviada para a caixa de entrada do endpoint que contém vários documentos PDF não seguros. Quando todos os documentos de PDF são criptografados com uma senha e se o endpoint é configurado como síncrono, uma única mensagem de e-mail de resposta é enviada com todos os documentos de PDF seguros anexados. Se o endpoint for configurado como assíncrono, uma mensagem de email de resposta separada será enviada para cada documento de PDF protegido. Cada mensagem de email contém um único documento PDF como anexo. O valor padrão é assíncrono.

**Definir valores de parâmetro de entrada**

Ao criar um endpoint de email, você deve definir valores de parâmetro de entrada. Ou seja, você deve descrever os valores de entrada transmitidos para a operação chamada pelo endpoint de email. Por exemplo, considere o processo introduzido neste tópico. Ele tem um valor de entrada chamado `InDoc` e seu tipo de dados é `com.adobe.idp.Document`. Ao criar um endpoint de email para esse processo (depois que um processo é ativado, ele se torna um serviço), você deve definir o valor do parâmetro de entrada.

Para definir valores de parâmetro de entrada necessários para um endpoint de Email, especifique os seguintes valores:

**Nome do parâmetro de entrada**: o nome do parâmetro de entrada. O nome de um valor de entrada é especificado na Bancada para um processo. Se o valor de entrada pertencer a uma operação de serviço (um serviço Forms que não é um processo criado no Workbench), o nome de entrada será especificado no arquivo component.xml. Por exemplo, o nome do parâmetro de entrada para o processo introduzido nesta seção é `InDoc`.

**Tipo de mapeamento**: usado para configurar os valores de entrada necessários para chamar a operação de serviço. Dois tipos de mapeamento são os seguintes:

* `Literal`: O endpoint de Email usa o valor inserido no campo como ele é exibido. Todos os tipos básicos de Java são compatíveis. Por exemplo, se uma API usar entradas como String, long, int e Boolean, a cadeia de caracteres será convertida no tipo adequado e o serviço será chamado.
* `Variable`: o valor inserido é um padrão de arquivo que o endpoint de email usa para escolher a entrada. Por exemplo, se você selecionar Variável para o tipo de mapeamento e o documento de entrada precisar ser um arquivo PDF, será possível especificar `*.pdf` como o valor de mapeamento.

**Mapeamento de valor**: especifica o valor do tipo de mapeamento. Por exemplo, se você selecionar um tipo de mapeamento Variável, será possível especificar `*.pdf` como o padrão do arquivo.

**Tipo de dados**: especifica o tipo de dados dos valores de entrada. Por exemplo, o tipo de dados do valor de entrada do processo introduzido nesta seção é com.adobe.idp.Document.

**Definir um valor de parâmetro de saída**

Ao criar um endpoint de email, você deve definir um valor de parâmetro de saída. Ou seja, você deve descrever o valor de saída retornado pelo serviço chamado pelo endpoint de email. Por exemplo, considere o processo introduzido neste tópico. Ele tem um valor de saída chamado `SecuredDoc` e seu tipo de dados é `com.adobe.idp.Document`. Ao criar um endpoint de email para esse processo (depois que um processo é ativado, ele se torna um serviço), você deve definir o valor do parâmetro de saída.

Para definir um valor de parâmetro de saída necessário para um endpoint de email, especifique os seguintes valores:

**Nome do parâmetro de saída**: o nome do parâmetro de saída. O nome de um valor de saída de processo é especificado no Workbench. Se o valor de saída pertencer a uma operação de serviço (um serviço que não é um processo criado no Workbench), o nome da saída será especificado no arquivo component.xml. Por exemplo, o nome do parâmetro de saída para o processo introduzido nesta seção é `SecuredDoc`.

**Tipo de mapeamento**: usado para configurar a saída do serviço e da operação. As opções disponíveis são as seguintes:

* Se o serviço retornar um único objeto (um único documento), o padrão será `%F.pdf` e o destino de origem é sourcefilename.pdf. Por exemplo, o processo introduzido nesta seção retorna um único documento. Como resultado, o tipo de mapeamento pode ser definido como `%F.pdf` ( `%F` significa usar o nome de arquivo fornecido). O padrão `%E` especifica a extensão do documento de entrada.
* Se o serviço retornar uma lista, o padrão será `Result\%F\`, e o destino de origem é Result\sourcefilename\source1 (saída 1) e Result\sourcefilename\source2 (saída 2).
* Se o serviço retornar um mapa, o padrão será `Result\%F\`e o destino de origem é Result\sourcefilename\file1 e Result\sourcefilename\file2. Se o mapa tiver mais de um objeto, o padrão será `Result\%F.pdf` e o destino de origem é Result\sourcefilename1.pdf (saída 1), Result\sourcefilenam2.pdf (saída 2) e assim por diante.

**Tipo de dados**: especifica o tipo de dados do valor de retorno. Por exemplo, o tipo de dados do valor de retorno do processo introduzido nesta seção é `com.adobe.idp.Document`.

**Criar o endpoint de email**

Depois de definir os atributos do endpoint de email e os valores de configuração, e definir valores de parâmetro de entrada e saída, você deve criar o endpoint de email.

**Habilitar o endpoint**

Depois de criar um endpoint de email, você deve habilitá-lo. Quando o endpoint está habilitado, ele pode ser usado para chamar o serviço. Após habilitar o endpoint, é possível visualizá-lo no console de administração.

**Consulte também**

[Adicionar um terminal de email usando a API Java](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicionar um terminal de email usando a API Java {#add-an-email-endpoint-using-the-java-api}

Adicionar um endpoint de email usando a API Java:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto Cliente EndpointRegistry.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `EndpointRegistryClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Defina atributos de endpoint de email.

   * Criar um `CreateEndpointInfo` usando seu construtor.
   * Especifique o valor do identificador do conector chamando o `CreateEndpointInfo` do objeto `setConnectorId` e transmitindo o valor da string `Email`.
   * Especifique a descrição do ponto de extremidade chamando o `CreateEndpointInfo` do objeto `setDescription` e transmitindo um valor de string que descreve o endpoint.
   * Especifique o nome do endpoint chamando o `CreateEndpointInfo` do objeto `setName` e transmitindo um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o `CreateEndpointInfo` do objeto `setServiceId` e transmitindo um valor de string que especifica o nome do serviço.
   * Especifique a operação que é invocada chamando o `CreateEndpointInfo` do objeto `setOperationName` e transmitindo um valor de string que especifica o nome da operação. Normalmente, ao criar um endpoint de email para um serviço que se originou de um processo criado no Workbench, o nome da operação é chamado.

1. Especifique os valores de configuração.

   Para cada valor de configuração a ser definido para o endpoint de email, chame o `CreateEndpointInfo` do objeto `setConfigParameterAsText` método. Por exemplo, para definir a variável `smtpHost` valor de configuração, chame o `CreateEndpointInfo` do objeto `setConfigParameterAsText` e passe os seguintes valores:

   * Um valor de string que especifica o nome do valor de configuração. Ao definir a variável `smtpHost` valor de configuração, especifique `smtpHost`.
   * Um valor de string que especifica o valor do valor de configuração. Ao definir a variável `smtpHost` valor de configuração, especifique um valor de string que especifique o nome do servidor SMTP.

   >[!NOTE]
   >
   >Para ver todos os valores de configuração definidos para o serviço EncryptDocument introduzidos nesta seção, consulte o exemplo de código Java localizado em [QuickStart: adicionando um endpoint de email usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api).

1. Defina os valores do parâmetro de entrada.

   Defina um valor de parâmetro de entrada chamando o `CreateEndpointInfo` do objeto `setInputParameterMapping` e passe os seguintes valores:

   * Um valor de string que especifica o nome do parâmetro de entrada. Por exemplo, o nome do parâmetro de entrada para o serviço EncryptDocument é `InDoc`.
   * Um valor de string que especifica o tipo de dados do parâmetro de entrada. Por exemplo, o tipo de dados do `InDoc` o parâmetro de entrada é `com.adobe.idp.Document`.
   * Um valor de string que especifica o tipo de mapeamento. Por exemplo, você pode especificar `variable`.
   * Um valor de string que especifica o valor do tipo de mapeamento. Por exemplo, você pode especificar &amp;ast;.pdf como o padrão do arquivo.

   >[!NOTE]
   >
   >Chame o `setInputParameterMapping` para cada valor de parâmetro de entrada a ser definido. Como o processo EncryptDocument tem apenas um parâmetro de entrada, é necessário chamar esse método uma vez.

1. Defina um valor de parâmetro de saída.

   Defina um valor de parâmetro de saída chamando o `CreateEndpointInfo` do objeto `setOutputParameterMapping` e transmitindo os seguintes valores:

   * Um valor de string que especifica o nome do parâmetro de saída. Por exemplo, o nome do parâmetro de saída para o serviço EncryptDocument é `SecuredDoc`.
   * Um valor de string que especifica o tipo de dados do parâmetro de saída. Por exemplo, o tipo de dados do `SecuredDoc` o parâmetro de saída é `com.adobe.idp.Document`.
   * Um valor de string que especifica o tipo de mapeamento. Por exemplo, você pode especificar `%F.pdf`.

1. Crie o endpoint de email.

   Crie o endpoint chamando o `EndpointRegistryClient` do objeto `createEndpoint` e transmitindo o `CreateEndpointInfo` objeto. Este método retorna um valor de `Endpoint` objeto que representa o endpoint de email.

1. Ative o endpoint.

   Ative o endpoint chamando o botão `EndpointRegistryClient` do objeto `enable` e transmitindo o `Endpoint` objeto que foi retornado pelo `createEndpoint` método.

**Consulte também**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[QuickStart: adicionando um endpoint de pasta monitorada usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Arquivo de constante de valores de configuração de email {#email-configuration-values-constant-file}

A variável [QuickStart: adicionando um endpoint de email usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) O usa um arquivo constante que deve fazer parte do projeto Java para compilar o início rápido. Esse arquivo de constante representa valores de configuração que devem ser definidos ao adicionar um terminal de email. O código Java a seguir representa o arquivo de constante.

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

## Adicionando Pontos de Extremidade de Comunicação Remota {#adding-remoting-endpoints}

>[!NOTE]
>
>APIs do LiveCycle Remoting descontinuadas para formulários AEM no JEE.

Você pode adicionar programaticamente um endpoint de comunicação remota a um serviço usando a API Java do AEM Forms. Ao adicionar um endpoint de Comunicação Remota, você está habilitando um aplicativo do Flex a chamar o serviço usando comunicação remota. (Consulte [Chamada do AEM Forms usando (obsoleto para o AEM formulários) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

Para adicionar programaticamente um terminal de Comunicação Remota a um serviço, considere o seguinte processo de vida curta chamado *EncryptDocument*.

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

Esse processo aceita um documento de PDF não seguro como valor de entrada e, em seguida, passa o documento de PDF não seguro para o do serviço de criptografia `EncryptPDFUsingPassword` operação. O documento PDF é criptografado com uma senha e o documento PDF criptografado com senha é o valor de saída desse processo. O nome do valor de entrada (o documento PDF não seguro) é `InDoc` e o tipo de dados for `com.adobe.idp.Document`. O nome do valor de saída (o documento PDF criptografado por senha) é `SecuredDoc` e o tipo de dados for `com.adobe.idp.Document`.

Para demonstrar como adicionar um ponto de extremidade de Comunicação Remota a um serviço, esta seção adiciona um ponto de extremidade de Comunicação Remota a um serviço chamado EncryptDocument.

>[!NOTE]
>
>Não é possível adicionar um ponto de extremidade de Comunicação Remota usando serviços da Web.

### Resumo das etapas {#summary_of_steps-4}

Para remover um ponto de extremidade de um serviço, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um `EndpointRegistryClient` objeto.
1. Defina atributos de ponto de extremidade de Comunicação Remota.
1. Criar um ponto de extremidade de Comunicação Remota.
1. Ative o endpoint.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto Cliente EndpointRegistry**

Para adicionar programaticamente um ponto de extremidade de Comunicação Remota, você deve criar um `EndpointRegistryClient` objeto.

**Definir atributos de ponto de extremidade de Comunicação Remota**

Para criar um ponto de extremidade de Comunicação Remota para um serviço, especifique os seguintes valores:

* **Valor do identificador do conector**: especifica o tipo de ponto de extremidade criado. Para criar um ponto de extremidade de Comunicação Remota, especifique `Remoting`.
* **Descrição**: especifica a descrição do ponto de extremidade.
* **Nome**: especifica o nome do ponto de extremidade.
* **Valor do identificador de serviço**: especifica o serviço ao qual o ponto de extremidade pertence. Por exemplo, para adicionar um terminal de Comunicação remota ao processo introduzido nesta seção (um processo se torna um serviço quando é ativado no Workbench), especifique `EncryptDocument`.
* **Nome da operação**: especifica o nome da operação que é invocada usando o ponto de extremidade. Ao criar um ponto de extremidade Remoto, especifique um caractere curinga (&amp;ast;).

**Criar um ponto de extremidade de Comunicação Remota**

Após definir os atributos do ponto de extremidade Remoting, você pode criar um ponto de extremidade Remoting para um serviço.

**Habilitar o endpoint**

Depois de criar um endpoint, você deve habilitá-lo. Quando um endpoint de Comunicação Remota está habilitado, ele permite que um cliente Flex chame o serviço.

**Consulte também**

[Adicionar um terminal de comunicação remota usando a API Java](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicionar um terminal de comunicação remota usando a API Java {#add-a-remoting-endpoint-using-the-java-api}

Adicionar um endpoint de Comunicação Remota usando a API Java:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto Cliente EndpointRegistry.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `EndpointRegistryClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Defina atributos de ponto de extremidade de Comunicação Remota.

   * Criar um `CreateEndpointInfo` usando seu construtor.
   * Especifique o valor do identificador do conector chamando o `CreateEndpointInfo` do objeto `setConnectorId` e transmitindo o valor da string `Remoting`.
   * Especifique a descrição do ponto de extremidade chamando o `CreateEndpointInfo` do objeto `setDescription` e transmitindo um valor de string que descreve o endpoint.
   * Especifique o nome do endpoint chamando o `CreateEndpointInfo` do objeto `setName` e transmitindo um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o `CreateEndpointInfo` do objeto `setServiceId` e transmitindo um valor de string que especifica o nome do serviço.
   * Especifique a operação que é chamada pelo `CreateEndpointInfo` do objeto `setOperationName` e transmitindo um valor de string que especifica o nome da operação. Para um ponto de extremidade de Comunicação Remota, especifique um caractere curinga (&amp;ast;).

1. Criar um ponto de extremidade de Comunicação Remota.

   Crie o endpoint chamando o `EndpointRegistryClient` do objeto `createEndpoint` e transmitindo o `CreateEndpointInfo` objeto. Este método retorna um valor de `Endpoint` objeto que representa o novo ponto de extremidade Remoting.

1. Ative o endpoint.

   Ative o endpoint chamando o botão `EndpointRegistryClient` do objeto `enable` e transmitindo o `Endpoint` objeto que foi retornado pelo `createEndpoint` método.

**Consulte também**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[QuickStart: adicionando um endpoint de comunicação remota usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Adicionando pontos finais do Gerenciador de Tarefas {#adding-taskmanager-endpoints}

Você pode adicionar programaticamente um endpoint TaskManager a um serviço usando a API Java do AEM Forms. Ao adicionar um terminal TaskManager a um serviço, você permite que um usuário do Workspace chame o serviço. Ou seja, um usuário que trabalha no Espaço de trabalho pode chamar um processo que tenha um endpoint do TaskManager correspondente.

>[!NOTE]
>
>Não é possível adicionar um ponto de extremidade TaskManager usando serviços da Web.

### Resumo das etapas {#summary_of_steps-5}

Para adicionar um ponto de extremidade TaskManager a um serviço, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um `EndpointRegistryClient` objeto.
1. Crie uma categoria para o endpoint.
1. Defina os atributos do ponto de extremidade do TaskManager.
1. Crie um ponto de extremidade TaskManager.
1. Ative o endpoint.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto Cliente EndpointRegistry**

Antes de adicionar programaticamente um ponto de extremidade TaskManager, você deve criar um `EndpointRegistryClient` objeto.

**Criar uma categoria para o ponto de extremidade**

As categorias são usadas para organizar serviços no Espaço de trabalho. Ou seja, um usuário do Workspace pode chamar um serviço que tenha um terminal TaskManager selecionando uma categoria no Workspace. Ao criar um endpoint do TaskManager, você pode fazer referência a uma categoria existente ou criar uma categoria de forma programática.

>[!NOTE]
>
>Esta seção cria uma nova categoria como parte da adição de um ponto de extremidade TaskManager a um serviço.

**Definir atributos de ponto de extremidade do TaskManager**

Para criar um ponto de extremidade TaskManager para um serviço, especifique os seguintes valores:

* **Identificador do conector**: especifica o tipo de ponto de extremidade criado. Para criar um ponto de extremidade TaskManager, especifique `TaskManagerConnector`.
* **Descrição**: especifica a descrição do ponto de extremidade.
* **Nome**: especifica o nome do ponto de extremidade.
* **Identificador de serviço**: especifica o serviço ao qual o ponto de extremidade pertence.
* **Categoria**: especifica um valor de identificador de categoria associado ao ponto de extremidade do TaskManager.
* **Nome da operação**: normalmente, ao criar um endpoint TaskManager para um serviço que se originou de um processo criado no Workbench, o nome da operação é `invoke`.

**Criar um ponto de extremidade TaskManager**

Após definir os atributos de um ponto de extremidade do TaskManager, você pode criar um ponto de extremidade do TaskManager para um serviço.

**Habilitar o endpoint**

Depois de criar um endpoint, você deve habilitá-lo. Quando o endpoint está habilitado, ele pode ser usado para chamar o serviço no Espaço de trabalho. Após habilitar o endpoint, é possível visualizá-lo no console de administração.

**Consulte também**

[Adicionar um terminal TaskManager usando a API Java](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicionar um terminal TaskManager usando a API Java {#add-a-taskmanager-endpoint-using-the-java-api}

Adicione um endpoint TaskManager usando a API Java:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto Cliente EndpointRegistry.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `EndpointRegistryClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Crie uma categoria para o endpoint.

   * Criar um `CreateEndpointCategoryInfo` usando seu construtor e transmitindo os seguintes valores:

      * Um valor de string que especifica o valor do identificador da categoria
      * Um valor de string que especifica a descrição da categoria

   * Crie a categoria chamando o `EndpointRegistryClient` do objeto `createEndpointCategory` e transmitindo o `CreateEndpointCategoryInfo` objeto. Este método retorna um valor de `EndpointCategory` objeto que representa a nova categoria.

1. Defina os atributos do ponto de extremidade do TaskManager.

   * Criar um `CreateEndpointInfo` usando seu construtor.
   * Especifique o valor do identificador do conector chamando o `CreateEndpointInfo` do objeto `setConnectorId` e transmitindo o valor da string `TaskManagerConnector`.
   * Especifique a descrição do ponto de extremidade chamando o `CreateEndpointInfo` do objeto `setDescription` e transmitindo um valor de string que descreve o endpoint.
   * Especifique o nome do endpoint chamando o `CreateEndpointInfo` do objeto `setName` e transmitindo um valor de string que especifica o nome.
   * Especifique o serviço ao qual o ponto de extremidade pertence, chamando o `CreateEndpointInfo` do objeto `setServiceId` e transmitindo um valor de string que especifica o nome do serviço.
   * Especifique a categoria à qual o ponto de extremidade pertence, chamando o `CreateEndpointInfo` do objeto `setCategoryId` e transmitindo um valor de string que especifica o valor do identificador de categoria. Você pode chamar a variável `EndpointCategory` do objeto `getId` para obter o valor identificador desta categoria.
   * Especifique a operação que é invocada chamando o `CreateEndpointInfo` do objeto `setOperationName` e transmitindo um valor de string que especifica o nome da operação. Normalmente, ao criar uma `TaskManager` endpoint para um serviço originado de um processo criado no Workbench, o nome da operação é `invoke`.

1. Crie um ponto de extremidade TaskManager.

   Crie o endpoint chamando o `EndpointRegistryClient` do objeto `createEndpoint` e transmitindo o `CreateEndpointInfo` objeto. Este método retorna um valor de `Endpoint` objeto que representa o novo ponto de extremidade do TaskManager.

1. Ative o endpoint.

   Ative o endpoint chamando o botão `EndpointRegistryClient` do objeto `enable` e transmitindo o `Endpoint` objeto que foi retornado pelo `createEndpoint` método.

**Consulte também**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[QuickStart: adicionando um endpoint TaskManager usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Modificação de Pontos de Extremidade {#modifying-endpoints}

Você pode modificar programaticamente um endpoint existente usando a API Java do AEM Forms. Ao modificar um endpoint, é possível alterar o comportamento dele. Considere, por exemplo, um endpoint de Pasta monitorada que especifica uma pasta usada como a pasta monitorada. Você pode modificar programaticamente os valores de configuração que pertencem ao endpoint da Pasta monitorada, resultando em outra pasta funcionando como a pasta monitorada. Para obter informações sobre valores de configuração que pertencem a um endpoint de Pasta monitorada, consulte [Adicionar pontos de extremidade da pasta monitorada](programmatically-endpoints.md#adding-watched-folder-endpoints).

Para demonstrar como modificar um endpoint, esta seção modifica um endpoint de Pasta monitorada alterando a pasta que se comporta como a pasta monitorada.

>[!NOTE]
>
>Não é possível modificar um ponto de extremidade usando serviços da Web.

### Resumo das etapas {#summary_of_steps-6}

Para modificar um endpoint, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um `EndpointRegistryClient` objeto.
1. Recuperar o ponto de extremidade.
1. Especifique novos valores de configuração.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto Cliente EndpointRegistry**

Para modificar programaticamente um endpoint, você deve criar um `EndpointRegistryClient` objeto.

**Recuperar o ponto de extremidade a ser modificado**

Antes de modificar um endpoint, você deve recuperá-lo. Para recuperar um endpoint, você deve se conectar como um usuário que pode acessar um endpoint. É recomendável conectar-se como administrador. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

Você pode recuperar um ponto de extremidade recuperando uma lista de pontos de extremidade. É possível percorrer a lista, procurando o endpoint específico a ser removido. Por exemplo, você pode localizar um endpoint determinando o serviço que corresponde ao endpoint e o tipo de endpoint. Ao localizar o endpoint, você pode modificá-lo.

**Especificar novos valores de configuração**

Ao modificar um endpoint, especifique novos valores de configuração. Por exemplo, para modificar um endpoint de Pasta monitorada, redefina todos os valores de configuração de endpoint de Pasta monitorada, não apenas aqueles que você deseja modificar. Para obter informações sobre valores de configuração que pertencem a um endpoint de Pasta monitorada, consulte [Adicionar pontos de extremidade da pasta monitorada](programmatically-endpoints.md#adding-watched-folder-endpoints).

>[!NOTE]
>
>Para obter informações sobre valores de configuração que pertencem a um endpoint de email, consulte [Adicionar pontos de extremidade de email](programmatically-endpoints.md#adding-email-endpoints).

>[!NOTE]
>
>Não é possível modificar o serviço chamado pelo ponto de extremidade. Se você tentar modificar o serviço, uma exceção será lançada. Para modificar o serviço associado a um determinado ponto de extremidade, remova o ponto de extremidade e crie um. (Consulte [Removendo Pontos de Extremidade](programmatically-endpoints.md#removing-endpoints).)

**Consulte também**

[Modificação de um endpoint usando a API Java](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Modificação de um endpoint usando a API Java {#modifying-an-endpoint-using-the-java-api}

Modifique um endpoint usando a API Java:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto Cliente EndpointRegistry.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `EndpointRegistryClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere o ponto de extremidade a ser modificado.

   * Recupera uma lista de todos os pontos de extremidade aos quais o usuário atual (especificado nas propriedades de conexão) pode acessar chamando o `EndpointRegistryClient` do objeto `getEndpoints` e passar um `PagingFilter` objeto que atua como filtro. Você pode passar um `(PagingFilter)null` para retornar todos os pontos de extremidade. Este método retorna um valor de `java.util.List` objeto no qual cada elemento é um `Endpoint` objeto. Para obter informações sobre uma `PagingFilter` objeto, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Repita através do `java.util.List` para determinar se tem pontos de extremidade. Se existirem endpoints, cada elemento será um `EndPoint` instância.
   * Determine o serviço que corresponde a um endpoint chamando o `EndPoint` do objeto `getServiceId` método. Este método retorna um valor de string que especifica o nome do serviço.
   * Determine o tipo de endpoint chamando o `EndPoint` do objeto `getConnectorId` método. Esse método retorna um valor de string que especifica o tipo de endpoint. Por exemplo, se o endpoint for um endpoint de Pasta monitorada, esse método retornará `WatchedFolder`.

1. Especifique novos valores de configuração.

   * Criar um `ModifyEndpointInfo` invocando seu construtor.
   * Para cada valor de configuração a ser definido, chame o `ModifyEndpointInfo` do objeto `setConfigParameterAsText` método. Por exemplo, para definir o valor de configuração do url, chame o `ModifyEndpointInfo` do objeto `setConfigParameterAsText` e passe os seguintes valores:

      * Um valor de string que especifica o nome do valor de configuração. Por exemplo, para definir a variável `url` valor de configuração, especifique `url`.
      * Um valor de string que especifica o valor do valor de configuração. Para definir um valor para a variável `url` valor de configuração, especifique o local da pasta monitorada.

   * Chame o `EndpointRegistryClient` do objeto `modifyEndpoint` e transmita o `ModifyEndpointInfo` objeto.

**Consulte também**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[QuickStart: modificando um endpoint usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Removendo Pontos de Extremidade {#removing-endpoints}

Você pode remover programaticamente um endpoint de um serviço usando a API Java do AEM Forms. Depois que você remove um ponto de extremidade, o serviço não pode ser chamado usando o método de invocação que o ponto de extremidade habilitou. Por exemplo, se você remover um ponto de extremidade SOAP de um serviço, não poderá chamar o serviço usando o modo SOAP.

Para demonstrar como remover um endpoint de um serviço, esta seção remove um endpoint EJB de um serviço chamado *EncryptDocument*.

>[!NOTE]
>
>Não é possível remover um ponto de extremidade usando serviços da Web.

### Resumo das etapas {#summary_of_steps-7}

Para remover um ponto de extremidade de um serviço, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um `EndpointRegistryClient` objeto.
1. Recuperar o ponto de extremidade.
1. Remova o endpoint.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto Cliente EndpointRegistry**

Para remover programaticamente um endpoint, você deve criar um `EndpointRegistryClient` objeto.

**Recuperar o ponto de extremidade a ser removido**

Antes de remover um endpoint, é necessário recuperá-lo. Para recuperar um endpoint, você deve se conectar como um usuário que pode acessar um endpoint. É recomendável conectar-se como administrador. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

Você pode recuperar um ponto de extremidade recuperando uma lista de pontos de extremidade. É possível percorrer a lista, procurando o endpoint específico a ser removido. Por exemplo, você pode localizar um endpoint determinando o serviço que corresponde ao endpoint e o tipo de endpoint. Ao localizar o endpoint, você pode removê-lo.

**Remover o ponto de extremidade**

Depois de criar um endpoint, você deve habilitá-lo. Quando o endpoint está habilitado, ele pode ser usado para chamar o serviço. Após habilitar o endpoint, é possível visualizá-lo no console de administração.

**Consulte também**

[Remoção de um endpoint usando a API Java](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Remoção de um endpoint usando a API Java {#removing-an-endpoint-using-the-java-api}

Remova um endpoint usando a API Java:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto Cliente EndpointRegistry.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `EndpointRegistryClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere o ponto de extremidade a ser removido.

   * Recupera uma lista de todos os pontos de extremidade aos quais o usuário atual (especificado nas propriedades de conexão) tem acesso chamando o `EndpointRegistryClient` do objeto `getEndpoints` e passar um `PagingFilter` objeto que atua como filtro. Você pode passar `(PagingFilter)null` para retornar todos os pontos de extremidade. Este método retorna um valor de `java.util.List` objeto no qual cada elemento é um `Endpoint` objeto.
   * Repita através do `java.util.List` para determinar se tem pontos de extremidade. Se existirem endpoints, cada elemento será um `EndPoint` instância.
   * Determine o serviço que corresponde a um endpoint chamando o `EndPoint` do objeto `getServiceId` método. Este método retorna um valor de string que especifica o nome do serviço.
   * Determine o tipo de endpoint chamando o `EndPoint` do objeto `getConnectorId` método. Esse método retorna um valor de string que especifica o tipo de endpoint. Por exemplo, se o ponto final for um ponto final EJB, este método retornará `EJB`.

1. Remova o endpoint.

   Remova o endpoint chamando o `EndpointRegistryClient` do objeto `remove` e transmitindo o `EndPoint` objeto que representa o ponto de extremidade a ser removido.

**Consulte também**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[QuickStart: removendo um endpoint usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Recuperando Informações do Conector do Ponto de Extremidade {#retrieving-endpoint-connector-information}

Você pode recuperar programaticamente informações sobre conectores de endpoint usando a API do AEM Forms. Um conector permite que um endpoint chame um serviço usando vários métodos de invocação. Por exemplo, um conector de Pasta monitorada permite que um terminal chame um serviço usando pastas monitoradas. Ao recuperar programaticamente informações sobre conectores de endpoint, é possível recuperar valores de configuração associados a um conector, como quais valores de configuração são necessários e quais são opcionais.

Para demonstrar como recuperar informações sobre conectores de endpoint, esta seção recupera informações sobre um conector de Pasta monitorada. (Consulte [Adicionar pontos de extremidade da pasta monitorada](programmatically-endpoints.md#adding-watched-folder-endpoints).)

>[!NOTE]
>
>Não é possível recuperar informações sobre pontos de extremidade usando serviços da Web.

>[!NOTE]
>
>Este tópico usa a variável `ConnectorRegistryClient` API para recuperar informações sobre conectores de endpoint. (Consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

### Resumo das etapas {#summary_of_steps-8}

Para recuperar informações do conector do ponto de extremidade, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um `ConnectorRegistryClient` objeto.
1. Especifique o tipo de conector.
1. Recupere valores de configuração.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, substitua adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms é implantado. Para obter informações sobre a localização de todos os arquivos JAR do AEM Forms, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto Cliente ConnectorRegistry**

Para recuperar programaticamente as informações do conector do ponto de extremidade, crie um `ConnectorRegistryClient` objeto.

**Especificar o tipo de conector**

Especifique o tipo de conector do qual recuperar informações. Existem os seguintes tipos de conectores:

* **EJB**: permite que uma aplicação cliente chame um serviço usando o modo EJB.
* **SOAP**: permite que um aplicativo cliente chame um serviço usando o modo SOAP.
* **Pasta monitorada**: permite que as pastas monitoradas chamem um serviço.
* **E-mail**: permite que mensagens de email chamem um serviço.
* **Comunicação remota**: permite que um aplicativo cliente do Flex chame um serviço.
* **ConectorDoGerenciadorDeTarefas**: permite que um usuário do Workspace chame um serviço de dentro do Workspace.

**Recuperar valores de configuração**

Após especificar o tipo de conector, você pode recuperar informações sobre o conector, como o valor de configuração suportado. Por exemplo, para qualquer conector, é possível determinar quais valores de configuração são necessários e quais são opcionais.

**Consulte também**

[Recuperar informações do conector de ponto de extremidade usando a API Java](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar informações do conector de ponto de extremidade usando a API Java {#retrieve-endpoint-connector-information-using-the-java-api}

Recupere informações do conector de ponto de extremidade usando a API Java:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto Cliente ConnectorRegistry.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `ConnectorRegistryClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Especifique o tipo de conector.

   Especifique o tipo de conector chamando o `ConnectorRegistryClient` do objeto `getEndpointDefinition` e transmitindo um valor de string que especifica o tipo de conector. Por exemplo, para especificar o tipo de conector Pasta monitorada, passe o valor da string `WatchedFolder`. Este método retorna um valor de `Endpoint` objeto que corresponde ao tipo de conector.

1. Recupere valores de configuração.

   * Recupere os valores de configuração associados a este ponto de extremidade chamando o `Endpoint` do objeto `getConfigParameters` método. Este método retorna uma matriz de `ConfigParameter` objetos.
   * Recupere informações sobre cada valor de configuração recuperando cada elemento na matriz. Cada elemento é um `ConfigParameter` objeto. Você pode, por exemplo, determinar se o valor de configuração é obrigatório ou opcional, chamando o `ConfigParameter` do objeto `isRequired` método. Se o valor de configuração for necessário, esse método retornará `true`.

**Consulte também**

[Resumo das etapas](programmatically-endpoints.md#summary-of-steps)

[QuickStart: recuperando informações do conector de ponto de extremidade usando a API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
