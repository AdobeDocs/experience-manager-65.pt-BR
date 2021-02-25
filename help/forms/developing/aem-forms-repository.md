---
title: Trabalhar com o AEM Forms Repository
seo-title: Trabalhar com o AEM Forms Repository
description: Gerencie o repositório da AEM Forms para criar pastas, gravar, lista, ler, atualizar e pesquisar recursos usando a API Java e a API de serviço da Web. Além disso, saiba como criar relacionamentos de recursos, bloquear e excluir recursos.
seo-description: Gerencie o repositório da AEM Forms para criar pastas, gravar, lista, ler, atualizar recursos e pesquisar recursos usando a API Java e a API de serviço da Web. Além disso, saiba como criar relacionamentos de recursos, bloquear e excluir recursos.
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '9157'
ht-degree: 0%

---


# Trabalhar com o AEM Forms Repository {#working-with-aem-forms-repository}

**Exemplos e exemplos neste documento são apenas para AEM Forms no ambiente JEE.**

**Sobre o Serviço de Repositório**

O serviço Repositório fornece serviços de gerenciamento e armazenamento de recursos à AEM Forms. Quando os desenvolvedores criam um aplicativo *AEM Forms*, eles podem implantar os ativos no repositório em vez do sistema de arquivos. Os ativos podem incluir qualquer tipo de material de apoio, incluindo formulários XML, PDF forms (incluindo formulários Acrobat), fragmentos de formulário, imagens, perfis, políticas, arquivos SWF, arquivos DX, schemas XML, arquivos WSDL e dados de teste.

Por exemplo, considere o seguinte aplicativo Forms chamado *Applications/FormsApplication*:

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

Observe que há um arquivo chamado Loan.xdp localizado em FormsFolder. Para acessar esse design de formulário, especifique o caminho completo (incluindo a versão): `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Para obter informações sobre como criar um aplicativo Forms usando o Workbench, consulte [Ajuda do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

O caminho para um recurso localizado no repositório AEM Forms é:

`Applications/Application-name/Application-version/Folder.../Filename`

Os valores a seguir mostram alguns exemplos de valores de URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>Você pode navegar pelo AEM Forms Repository usando um navegador da Web. Para navegar pelo repositório, insira o seguinte URL em um navegador da Web `https://[server name]:[server port]/repository`. Você pode verificar os resultados do start rápido associados à seção Trabalhar com o repositório do AEM Forms usando um navegador da Web. Por exemplo, se você adicionar conteúdo ao AEM Forms Repository, poderá ver o conteúdo em um navegador da Web. (Consulte [Start rápido (modo SOAP): Gravando um recurso usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

A API do repositório fornece várias operações que podem ser usadas para armazenar e recuperar informações do repositório. Por exemplo, você pode obter uma lista de recursos ou recuperar recursos específicos que são armazenados no repositório quando um recurso é necessário como parte do processamento de um aplicativo.

>[!NOTE]
>
>A API do repositório não pode ser usada para interagir com o Content Services (obsoleto). Para interagir com o Content Services (obsoleto), use a API de gerenciamento de Documentos.

Usando a API de serviço do Repositório, você pode realizar as seguintes tarefas:

* Criar pastas. Consulte [Criando Pastas](aem-forms-repository.md#creating-folders).
* Escreva recursos e suas propriedades. Consulte [Gravando recursos](aem-forms-repository.md#writing-resources).
* Recursos de lista em uma determinada coleção ou relacionados a outros recursos. Consulte [Listando recursos](aem-forms-repository.md#listing-resources).
* Leia os recursos e suas propriedades. Consulte [Lendo recursos](aem-forms-repository.md#reading-resources).
* Atualize os recursos e suas propriedades. Consulte [Atualizando Recursos](aem-forms-repository.md#updating-resources).
* Procure recursos, incluindo seu histórico, recursos relacionados e propriedades. Consulte [Procurando por Recursos](aem-forms-repository.md#searching-for-resources).
* Especifique relações entre recursos. Consulte [Criando Relacionamentos de Recursos](aem-forms-repository.md#creating-resource-relationships).
* Gerencie o controle de acesso de recursos, incluindo o bloqueio e desbloqueio de recursos, e a leitura e gravação de listas de controles de acesso (ACLs). Consulte [Bloqueando recursos](aem-forms-repository.md#locking-resources).
* Exclua recursos e suas propriedades. Consulte [Excluindo Recursos](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>Usando a API de repositório, não é possível gerenciar o controle de acesso de recursos, procurar recursos ou especificar relacionamentos de recursos usando um repositório ECM.

>[!NOTE]
>
>Quando um PDF criptografado é gravado no repositório, o recurso de extração de relacionamento automatizado não pode ser usado. Caso contrário, um PDF criptografado pode ser armazenado no repositório e recuperado posteriormente. O recuperador pode optar por descriptografar o PDF após ele ser recuperado do repositório.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Repositório, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Criando Pastas {#creating-folders}

As pastas (coleções de recursos) são usadas para armazenar objetos (arquivos ou recursos) em agrupamentos organizados. As pastas podem conter recursos e outras pastas, também conhecidas como subpastas. Os recursos só podem ser armazenados em uma pasta por vez.

Os arquivos herdam listas de controles de acesso (ACLs) de pastas e as subpastas herdam ACLs de suas pastas pai. Portanto, as pastas pai devem existir para que você possa criar pastas secundárias. O IDE permite que você interaja somente com base em pasta por pasta, e não com base em arquivo por arquivo. Não é possível fazer a versão de pastas e não há necessidade de fazê-lo; uma pasta não contém os dados propriamente ditos. Em vez disso, é apenas um container para recursos que contêm dados. A ACL padrão é uma permissão no nível do sistema, o que significa que os usuários devem ter permissões no nível do sistema (ler, gravar, navegar, gerenciar ACLs) até que alguém lhes conceda permissões para uma pasta específica. As ACLs funcionam somente no IDE.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Repositório, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para criar uma pasta, siga estas etapas:

1. Incluir arquivos de projeto.
1. Crie o cliente de serviço.
1. Crie a pasta.
1. Grave a pasta no repositório.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de criar programaticamente uma coleção de recursos, você deve estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Criar a pasta**

Chame o método do serviço Repositório para criar a coleção de recursos e preencher a coleção de recursos com informações de identificação, incluindo UUID, nome da pasta e descrição.

**Gravar a pasta no repositório**

Chame o método do serviço Repositório para gravar a coleção de recursos, especificando o URI da pasta do público alvo.

**Consulte também:**

[Criar pastas usando a API Java](aem-forms-repository.md#create-folders-using-the-java-api)

[Criar pastas usando a API de serviço da Web](aem-forms-repository.md#create-folders-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Criar pastas usando a API Java {#create-folders-using-the-java-api}

Crie uma pasta usando a API de serviço do Repositório (Java):

1. Incluir arquivos de projeto

   Inclua arquivos de projeto no caminho de classe do seu projeto Java.

1. Criar o cliente de serviço

   Crie um objeto `ResourceRepositoryClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Criar a pasta

   Para criar uma coleção de recursos, primeiro crie um objeto `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`.

   Chame o método `repositoryInfomodelFactoryBean` do objeto `newResourceCollection` e passe os seguintes parâmetros:

   * Um identificador UUID `com.adobe.repository.infomodel.Id` a ser atribuído ao recurso.
   * Um identificador UUID `com.adobe.repository.infomodel.Lid` a ser atribuído ao recurso.
   * Um `java.lang.String` contendo o nome da coleção de recursos. Por exemplo, `FormsFolder`.

   O método retorna um objeto `com.adobe.repository.infomodel.bean.ResourceCollection` que representa a nova pasta.

   Defina a descrição da pasta usando o método `setDescription` e passe o seguinte parâmetro:

   * Um `String` que descreve a coleção de recursos. Neste exemplo, `"test Folder"` é usado `.`


1. Gravar a pasta no repositório

   Chame o método `ResourceRepositoryClient` do objeto `writeResource` e transmita o URI da pasta e o objeto `ResourceCollection`. Por exemplo, o URI para a pasta pode ser o seguinte valor `/Applications/FormsApplication/1.0/`.

   O método retorna uma instância do objeto `com.adobe.repository.infomodel.bean.Resource` recém-criado. Você pode, por exemplo, recuperar o valor identificador do novo recurso chamando o método `com.adobe.repository.infomodel.bean.Resource` do objeto `getId`.

**Consulte também:**

[Criação de pastas](aem-forms-repository.md#creating-folders)

[Start rápido (modo SOAP): Criação de uma pasta usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Criar pastas usando a API de serviço da Web {#create-folders-using-the-web-service-api}

Crie uma pasta usando a API de serviço do Repositório (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o WSDL do Repositório usando base64.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar o cliente de serviço

   Usando o assembly do cliente Microsoft .NET, crie um objeto `RepositoryServiceService` chamando seu construtor padrão. Defina sua propriedade `Credentials` usando um objeto `System.Net.NetworkCredential` que contenha o nome de usuário e a senha.

1. Criar a pasta

   Crie a pasta usando o construtor padrão para a classe `ResourceCollection` e passe os seguintes parâmetros:

   * Um objeto `Id`, que é criado chamando o construtor padrão para a classe `Id` e atribuído ao campo `Resource` do objeto `id`.
   * Um objeto `Lid`, que é criado chamando o construtor padrão para a classe `Lid` e atribuído ao campo `Resource` do objeto `lid`.
   * Uma string contendo o nome da coleção de recursos, que é atribuída ao campo `Resource` `name` do objeto. O nome usado neste exemplo é `"testfolder"`.
   * Uma string contendo a descrição da coleção de recursos, que é atribuída ao campo `Resource` `description` do objeto. A descrição usada neste exemplo é `"test folder"`.

1. Gravar a pasta no repositório

   Chame o método `RepositoryServiceService` do objeto `writeResource` e passe os seguintes parâmetros:

   * O caminho onde a pasta será criada.
   * O objeto `ResourceCollection` que representa a pasta.
   * Passe `null` para os outros dois parâmetros.

**Consulte também:**

[Criação de pastas](aem-forms-repository.md#creating-folders)

[Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Gravando recursos {#writing-resources}

Você pode criar recursos em um determinado local no repositório. O tamanho natural do arquivo está sujeito às limitações do banco de dados e ao tempo limite da sessão. Para a configuração padrão, os arquivos estão limitados a 25 MB. Para aumentar ou diminuir o tamanho máximo do arquivo, é necessário alterar a configuração do banco de dados.

Gravar recursos equivale a armazenar dados no repositório. Depois que você gravar um recurso no repositório, ele se tornará acessível a todos os clientes no ecossistema do repositório. Quando você grava recursos, como schemas XML, arquivos XDP e arquivos XSD, no repositório, o conteúdo é analisado com base no tipo MIME. Se o tipo MIME for suportado, o analisador determinará se há uma relação implícita com outro conteúdo. Por exemplo, se uma folha de estilos em cascata (CSS) tiver um URL relativo que faz referência a um CSS comum, espera-se que você envie o CSS comum também para o repositório. A relação entre os dois recursos é armazenada como uma relação pendente por um período não ajustável de 30 dias. Quando você envia o CSS comum para o repositório dentro do período de 30 dias, a relação é formada.

Quando você cria um recurso, a lista do controle de acesso (ACL) é herdada da pasta pai. A pasta raiz tem permissões no nível do sistema até que um recurso ou pasta inicial seja criado, e nesse ponto o recurso ou a pasta recebe permissões de ACL padrão.

Você pode gravar recursos programaticamente usando a API Java do serviço do Repositório ou a API do serviço da Web.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Repositório, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para gravar um recurso, siga estas etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço do Repositório.
1. Especifique o URI do recurso a ser lido.
1. Leia o recurso.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de poder ler programaticamente um recurso, você deve estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Especificar o URI da pasta do público alvo para o recurso**

Crie uma string contendo o URI do recurso a ser lido. A sintaxe inclui barras, como neste exemplo: &quot;/*path*/*folder*&quot;.

**Criar o recurso**

Chame o método do serviço Repositório para criar o recurso e preencha o recurso com informações de identificação, incluindo sua UUID, nome do recurso e descrição.

**Especificar o conteúdo do recurso**

Chame o método do serviço Repositório para criar conteúdo de recurso e armazená-lo no recurso.

**Gravar o recurso na pasta do público alvo**

Chame o método do serviço Repositório para gravar o recurso, especificando o URI da pasta do público alvo.

**Consulte também:**

[Gravar recursos usando a API Java](aem-forms-repository.md#write-resources-using-the-java-api)

[Gravar recursos usando a API de serviço da Web](aem-forms-repository.md#write-resources-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Gravar recursos usando a API Java {#write-resources-using-the-java-api}

Grave um recurso usando a API de serviço do Repositório (Java):

1. Incluir arquivos de projeto

   Inclua os arquivos JAR do cliente no caminho de classe do seu projeto Java.

1. Criar o cliente de serviço

   Crie um objeto `ResourceRepositoryClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Especificar o URI da pasta do público alvo para o recurso

   Especifique o URI da pasta do público alvo para o recurso. Nesse caso, como o recurso chamado `testResource` será armazenado na pasta chamada `testFolder`, o URI da pasta é `"/testFolder"`. O URI é armazenado como um objeto `java.lang.String`.

1. Criar o recurso

   Para criar um recurso, você deve primeiro criar um objeto `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`.

   Chame o método `RepositoryInfomodelFactoryBean` do objeto `newResource`, que cria um objeto `com.adobe.repository.infomodel.bean.Resource`. Neste exemplo, os seguintes parâmetros são fornecidos:

   * Um objeto `com.adobe.repository.infomodel.Id`, que é criado chamando o construtor padrão para a classe `Id`.
   * Um objeto `com.adobe.repository.infomodel.Lid`, que é criado chamando o construtor padrão para a classe `Lid`.
   * Um `java.lang.String` contendo o nome do arquivo do recurso.

   Para especificar a descrição do recurso, chame o método `Resource` do objeto `setDescription` e passe uma string contendo a descrição. Neste exemplo, a descrição é `"test resource"`.

1. Especificar o conteúdo do recurso

   Para criar conteúdo para o recurso, chame o método `RepositoryInfomodelFactoryBean` do objeto `newResourceContent`, que retorna um objeto `com.adobe.repository.infomodel.bean.ResourceContent`. Adicione conteúdo ao objeto `ResourceContent`. Neste exemplo, isso é feito com as seguintes tarefas:

   * Invocando o método `ResourceContent` do objeto `setDataDocument` e transmitindo um objeto `com.adobe.idp.Document`
   * Invocando o método `ResourceContent` do objeto `setSize` e transmitindo o tamanho em bytes do objeto `Document`

   Adicione o conteúdo ao recurso chamando o método `Resource` do objeto `setContent` e transmitindo o objeto `ResourceContent`. Para obter mais informações, consulte [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Gravar o recurso na pasta do público alvo

   Chame o método `ResourceRepositoryClient` do objeto `writeResource` e passe no URI da pasta, bem como o objeto `Resource`.

**Consulte também:**

[Gravando recursos](aem-forms-repository.md#writing-resources)

[Start rápido (modo SOAP): Gravação de um recurso usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Gravar recursos usando a API de serviço da Web {#write-resources-using-the-web-service-api}

Grave um recurso usando a API de serviço do Repositório (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o WSDL do Repositório usando base64.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar o cliente de serviço

   Usando o assembly do cliente Microsoft .NET, crie um objeto `RepositoryServiceService` chamando seu construtor padrão. Defina sua propriedade `Credentials` usando um objeto `System.Net.NetworkCredential` contendo o nome de usuário e a senha.

1. Especificar o URI da pasta do público alvo para o recurso

   Especifique o URI da pasta do público alvo para o recurso. Nesse caso, como o recurso chamado `testResource` será armazenado na pasta chamada `testFolder`, o URI da pasta é `"/testFolder"`. Ao usar um idioma compatível com o Microsoft .NET Framework (por exemplo, C#), armazene o URI em um objeto `System.String`.

1. Criar o recurso

   Para criar um recurso, chame o construtor padrão para a classe `Resource`. Neste exemplo, as seguintes informações são armazenadas no objeto `Resource`:

   * Um objeto `com.adobe.repository.infomodel.Id`, que é criado chamando o construtor padrão para a classe `Id` e atribuído ao campo `Resource` do objeto `id`.
   * Um objeto `com.adobe.repository.infomodel.Lid`, que é criado chamando o construtor padrão para a classe `Lid` e atribuído ao campo `Resource` do objeto `lid`.
   * Uma string contendo o nome do arquivo do recurso, que é atribuído ao campo `Resource` `name` do objeto. O nome usado neste exemplo é `"testResource"`.
   * Uma string contendo a descrição do recurso, que é atribuída ao campo `Resource` `description` do objeto. A descrição usada neste exemplo é `"test resource"`.

1. Especificar o conteúdo do recurso

   Para criar conteúdo para o recurso, chame o construtor padrão para a classe `ResourceContent`. Em seguida, adicione conteúdo ao objeto `ResourceContent`. Neste exemplo, isso é feito com as seguintes tarefas:

   * Atribuindo um objeto `BLOB` contendo um documento ao campo `ResourceContent` `dataDocument` do objeto.
   * Atribuindo o tamanho em bytes do objeto `BLOB` ao campo `ResourceContent` `size` do objeto.

   Adicione o conteúdo ao recurso atribuindo o objeto `ResourceContent` ao campo `Resource` `content` do objeto.

1. Gravar o recurso na pasta do público alvo

   Chame o método `RepositoryServiceService` do objeto `writeResource` e passe no URI da pasta, bem como o objeto `Resource`. Passe `null` para os outros dois parâmetros.

**Consulte também:**

[Gravando recursos](aem-forms-repository.md#writing-resources)

[Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Listando recursos {#listing-resources}

Você pode descobrir recursos ao listar recursos. Um query é executado no repositório para localizar todos os recursos relacionados a uma determinada coleção de recursos.

Depois de organizar seus recursos, você pode inspecionar a estrutura que criou ao ver uma ramificação específica da estrutura, como faria em um sistema operacional.

Os recursos de listagem operam por relacionamento: os recursos são membros de pastas. A associação é representada por uma relação do tipo &quot;membro de&quot;. Ao lista de recursos em uma determinada pasta, você está consultando os recursos relacionados a uma determinada pasta pelo &quot;membro de&quot; da relação. Os relacionamentos são direcionais: um membro de um relacionamento tem uma fonte que é membro do público alvo. A fonte é o recurso; o público alvo é a pasta pai.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Repositório, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-2}

Para lista de recursos, siga estas etapas:

1. Incluir arquivos de projeto.
1. Crie o cliente de serviço.
1. Especifique o caminho da pasta.
1. Recupere a lista de recursos.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de criar programaticamente uma coleção de recursos, você deve estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Especificar o caminho da pasta**

Crie uma string contendo o caminho da pasta que contém os recursos. A sintaxe inclui barras, como neste exemplo: &quot;/*path*/*folder*&quot;.

**Recuperar a lista de recursos**

Chame o método do serviço Repositório para recuperar a lista de recursos, especificando o caminho da pasta do público alvo.

**Consulte também:**

[Recursos de lista usando a API Java](aem-forms-repository.md#list-resources-using-the-java-api)

[Recursos de lista usando a API de serviço da Web](aem-forms-repository.md#list-resources-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Recursos de lista usando a API Java {#list-resources-using-the-java-api}

Recursos de lista usando a API de serviço do Repositório (Java):

1. Incluir arquivos de projeto

   Inclua os arquivos JAR do cliente no caminho de classe do seu projeto Java.

1. Criar o cliente de serviço

   Crie um objeto `ResourceRepositoryClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Especificar o caminho da pasta

   Especifique o URI da coleção de recursos a ser consultada. Nesse caso, seu URI é `"/testFolder"`. O URI é armazenado como um objeto `java.lang.String`.

1. Recuperar a lista de recursos

   Chame o método `ResourceRepositoryClient` do objeto `listMembers` e passe para o URI da pasta.

   O método retorna um `java.util.List` de `com.adobe.repository.infomodel.bean.Resource` objetos que são a origem de um `com.adobe.repository.infomodel.bean.Relation` do tipo `Relation.TYPE_MEMBER_OF` e que têm o URI de coleção de recursos como o público alvo. Você pode iterar por meio deste `List` para recuperar cada um dos recursos. Neste exemplo, o nome e a descrição de cada recurso são exibidos.

**Consulte também:**

[Listando recursos](aem-forms-repository.md#listing-resources).

[Start rápido (modo SOAP): Listar recursos usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recursos de lista usando a API de serviço da Web {#list-resources-using-the-web-service-api}

Recursos de lista usando a API de serviço do Repositório (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o WSDL do Repositório.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar o cliente de serviço

   Usando o assembly do cliente Microsoft .NET, crie um objeto `RepositoryServiceService` chamando seu construtor padrão. Defina sua propriedade `Credentials` usando um objeto `System.Net.NetworkCredential` contendo o nome de usuário e a senha.

1. Especificar o caminho da pasta

   Especifique uma string que contenha o URI da pasta a ser consultada. Nesse caso, seu URI é `"/testFolder"`. Ao usar um idioma compatível com o Microsoft .NET Framework (por exemplo, C#), armazene o URI em um objeto `System.String`.

1. Recuperar a lista de recursos

   Chame o método `RepositoryServiceService` do objeto `listMembers` e passe o URI da pasta como o primeiro parâmetro. Passe `null` para os outros dois parâmetros.

   O método retorna uma matriz de objetos que podem ser convertidos em `Resource` objetos. É possível iterar pela matriz de objetos para recuperar cada um dos recursos relacionados. Neste exemplo, o nome e a descrição de cada recurso são exibidos.

**Consulte também:**

[Listando recursos](aem-forms-repository.md#listing-resources).

[Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Lendo recursos {#reading-resources}

Você pode recuperar recursos de um determinado local no repositório para ler o conteúdo e os metadados. O fluxo de trabalho é finalizado pela frente por um formulário de inicialização. O processo tem todas as permissões necessárias para ler o formulário. O sistema recupera o formulário de dados e lê o conteúdo do repositório. O repositório concede acesso ao conteúdo e aos metadados (a capacidade de saber se o recurso existe).

O repositório tem os quatro tipos de permissão a seguir:

* **transversal**: permite que você lista recursos; ou seja, para ler metadados de recursos, mas não conteúdo de recursos
* **deve ler**-se: permite que você leia o conteúdo do recurso
* **gravar**: permite gravar conteúdo de recurso
* **gerenciamento de controles de acesso (ACLs)**: permite manipular ACLs em recursos

Os usuários só podem executar processos quando tiverem permissão para executar o processo. Os usuários do IDE precisam de permissões de leitura e peregrinação para sincronizar com o repositório. As ACLs se aplicam somente no momento do design, pois o tempo de execução ocorre no contexto do sistema.

Você pode ler os recursos de forma programática usando a API Java do serviço do Repositório ou a API do serviço da Web.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Repositório, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-3}

Para ler um recurso, siga estas etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço do Repositório.
1. Especifique o URI do recurso a ser lido.
1. Leia o recurso.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de poder ler programaticamente um recurso, você deve estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Especificar o URI do recurso a ser lido**

Crie uma string contendo o URI do recurso a ser lido. A sintaxe inclui barras, como neste exemplo: &quot;/*path*/*resource*&quot;.

**Ler o recurso**

Chame o método de serviço Repositório para ler o recurso, especificando o URI.

**Consulte também:**

[Ler recursos usando a API Java](aem-forms-repository.md#read-resources-using-the-java-api)

[Lendo recursos usando a API de serviço da Web](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Leia os recursos usando a API Java {#read-resources-using-the-java-api}

Leia um recurso usando a API de serviço do Repositório (Java):

1. Incluir arquivos de projeto

   Inclua os arquivos JAR do cliente no caminho de classe do seu projeto Java.

1. Criar o cliente de serviço

   Crie um objeto `ResourceRepositoryClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Especificar o URI do recurso a ser lido

   Especifique um valor de string que represente o URI do recurso a ser recuperado. Por exemplo, supondo que o recurso seja chamado *testResource*, que esteja localizado em uma pasta chamada *testFolder*, especifique `/testFolder/testResource`.

1. Ler o recurso

   Chame o método `ResourceRepositoryClient` do objeto `readResource` e passe o URI do recurso como um parâmetro. Este método retorna uma instância `Resource` que representa o recurso.

**Consulte também:**

[Lendo recursos](aem-forms-repository.md#reading-resources)

[Start rápido (modo SOAP): Ler um recurso usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Lendo recursos usando a API de serviço da Web {#reading-resources-using-the-web-service-api}

Leia um recurso usando a API de serviço do Repositório (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o WSDL do Repositório. (Consulte [Criação de um assembly de cliente .NET que usa a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)
   * Faça referência ao assembly do cliente Microsoft .NET. (Consulte [Criação de um assembly de cliente .NET que usa a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Criar o cliente de serviço

   Usando o assembly do cliente Microsoft .NET, crie um objeto `RepositoryServiceService` chamando seu construtor padrão. Defina sua propriedade `Credentials` usando um objeto `System.Net.NetworkCredential` contendo o nome de usuário e a senha.

1. Especificar o URI do recurso a ser lido

   Especifique uma string que contenha o URI do recurso a ser recuperado. Nesse caso, como o recurso chamado `testResource` está na pasta chamada `testFolder`, seu URI é `"/testFolder/testResource"`. Ao usar um idioma compatível com o Microsoft .NET Framework (por exemplo, C#), armazene o URI em um objeto `System.String`.

1. Ler o recurso

   Chame o método `RepositoryServiceService` do objeto `readResource` e passe o URI do recurso como o primeiro parâmetro. Passe `null` para os outros dois parâmetros.

**Consulte também:**

[Lendo recursos](aem-forms-repository.md#reading-resources)

[Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Atualização de recursos {#updating-resources}

Você pode recuperar e atualizar o conteúdo dos recursos no repositório. Quando você atualiza recursos, o controle de acesso para esses recursos permanece inalterado entre as versões. Ao executar uma atualização, você tem a opção de aumentar a versão principal. Se você não optar por incrementar a versão principal, a versão secundária será atualizada automaticamente.

Quando você atualiza um recurso, a nova versão é criada com base nos atributos de recurso especificados. Ao atualizar um recurso, você especifica dois parâmetros importantes: o URI do público alvo e uma instância de recurso que contém todos os metadados atualizados. É importante observar que se você não estiver alterando um determinado atributo (por exemplo, o nome), o atributo ainda será necessário na instância transmitida. As relações criadas ao analisar o conteúdo são adicionadas à versão específica e não são encaminhadas, a menos que especificado.

Por exemplo, se você atualizar um arquivo XDP e ele contiver referências a outros recursos, essas referências adicionais também serão registradas. Suponha que form.xdp versão 1.0 tenha duas referências externas: um logotipo e uma folha de estilos, e você atualiza subsequentemente o form.xdp para que agora tenha três referências: um logotipo, uma folha de estilos e um arquivo de schema. Durante a atualização, o repositório adicionará a terceira relação (ao arquivo do schema) à tabela de relação pendente. Quando o arquivo de schema estiver presente no repositório, a relação será formada automaticamente. Entretanto, se form.xdp versão 2.0 não usar mais o logotipo, form.xdp versão 2.0 não terá uma relação com o logotipo.

Todas as operações de atualização são atômicas e transacionais. Por exemplo, se dois usuários lerem o mesmo recurso e ambos decidirem atualizar a versão 1.0 para a versão 2.0, um deles terá êxito e um deles falhará, a integridade do repositório será mantida e ambos receberão uma mensagem confirmando o sucesso ou a falha. Se a transação não for confirmada, ela será revertida em caso de falha no banco de dados e expirará ou reverterá dependendo do servidor de aplicativos.

Você pode atualizar recursos programaticamente usando a API Java do serviço do Repositório ou a API do serviço da Web.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Repositório, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-4}

Para atualizar um recurso, siga estas etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço do Repositório.
1. Recupere o recurso a ser atualizado.
1. Atualize o recurso.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de poder ler programaticamente um recurso, você deve estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Recuperar o recurso a ser atualizado**

Leia o recurso. Para obter mais informações, consulte [Lendo recursos](aem-forms-repository.md#reading-resources).

**Atualizar o recurso**

Defina as novas informações no recurso e chame o método do serviço Repositório para atualizar o recurso, especificando o URI, o recurso atualizado e como as informações da versão devem ser atualizadas.

**Consulte também:**

[Atualizar recursos usando a API Java](aem-forms-repository.md#update-resources-using-the-java-api)

[Atualizar recursos usando a API de serviço da Web](aem-forms-repository.md#update-resources-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Atualizar recursos usando a API Java {#update-resources-using-the-java-api}

Atualize um recurso usando a API de serviço do Repositório (Java):

1. Incluir arquivos de projeto

   Inclua os arquivos JAR do cliente no caminho de classe do seu projeto Java.

1. Criar o cliente de serviço

   Crie um objeto `ResourceRepositoryClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Recuperar o recurso a ser atualizado

   Especifique o URI do recurso para recuperar e ler o recurso. Neste exemplo, o URI do recurso é `"/testFolder/testResource"`.

1. Atualizar o recurso

   Atualize as informações do objeto `Resource`. Neste exemplo, para atualizar a descrição, chame o método `Resource` do objeto e passe a nova string de descrição como parâmetro.`setDescription`

   Em seguida, chame o método `ServiceClientFactory` do objeto `updateResource` e passe os seguintes parâmetros:

   * Um objeto `java.lang.String` contendo o URI do recurso.
   * O objeto `Resource` que contém as informações atualizadas do recurso.
   * Um valor `boolean` que indica se a versão principal ou secundária deve ser atualizada. Neste exemplo, um valor de `true` é passado para indicar que a versão principal deve ser aumentada.

**Consulte também:**

[Atualização de recursos](aem-forms-repository.md#updating-resources)

[Start rápido (modo SOAP): Atualização de um recurso usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Atualizar recursos usando a API de serviço da Web {#update-resources-using-the-web-service-api}

Atualize um recurso usando a API do repositório (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o WSDL do Repositório.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar o cliente de serviço

   Usando o assembly do cliente Microsoft .NET, crie um objeto `RepositoryServiceService` chamando seu construtor padrão. Defina sua propriedade `Credentials` usando um objeto `System.Net.NetworkCredential` contendo o nome de usuário e a senha.

1. Recuperar o recurso a ser atualizado

   Especifique o URI do recurso a ser recuperado e leia o recurso. Neste exemplo, o URI do recurso é `"/testFolder/testResource"`. Para obter mais informações, consulte [Lendo recursos](aem-forms-repository.md#reading-resources).

1. Atualizar o recurso

   Atualize as informações do objeto `Resource`. Neste exemplo, para atualizar a descrição, atribua um novo valor ao campo `Resource` `description` do objeto.

1. Chame o método `RepositoryServiceService` do objeto `updateResource` e passe os seguintes parâmetros:

   * Um objeto `System.String` contendo o URI do recurso.
   * O objeto `Resource` que contém as informações atualizadas do recurso.
   * Um valor `boolean` que indica se a versão principal ou secundária deve ser atualizada. Neste exemplo, um valor de `true` é passado para indicar que a versão principal deve ser aumentada.
   * Passe `null` para os dois parâmetros restantes.

**Consulte também:**

[Atualização de recursos](aem-forms-repository.md#updating-resources)

[Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Procurando por Recursos {#searching-for-resources}

É possível construir query usados para procurar recursos no repositório, incluindo histórico, recursos relacionados e propriedades.

É possível recuperar recursos relacionados para determinar dependências entre um formulário e seus fragmentos. Por exemplo, se você tiver um formulário, poderá determinar quais fragmentos ou recursos externos ele utiliza. Se você tiver uma imagem, também poderá descobrir quais formulários usam a imagem. Também é possível pesquisar recursos relacionados usando a filtragem com base nas propriedades. Por exemplo, é possível pesquisar por todos os formulários que usam uma imagem com um nome especificado ou localizar qualquer imagem usada por um formulário com um nome especificado. Também é possível pesquisar usando propriedades de recursos. Por exemplo, você pode conduzir um query para localizar todos os formulários ou recursos cujo nome start com uma determinada sequência de caracteres que podem incluir curingas &quot;%&quot; e &quot;_&quot;. Lembre-se de que as pesquisas baseadas em propriedades não se baseiam em relações; essas pesquisas são baseadas na suposição de que você tem conhecimento específico sobre um determinado recurso.

**declarações de query**

Um *query* contém uma ou mais declarações que são logicamente associadas a condições. Uma *instrução* consiste em um operando esquerdo, um operador e um operando direito. Além disso, você pode especificar a ordem de classificação a ser usada para os resultados da pesquisa. A *ordem de classificação* contém informações equivalentes a uma cláusula SQL `ORDER BY` e é composta por elementos que contêm os atributos nos quais a pesquisa se baseou, bem como um valor que indica se a ordem crescente ou decrescente deve ser usada.

Você pode procurar recursos de forma programática usando a API Java do serviço do Repositório. No momento, não é possível usar a API de serviço da Web para procurar recursos.

**Comportamento de classificação**

A ordem de classificação não é respeitada ao invocar o método `ResourceRepositoryClient` do objeto `searchProperties` e especificar uma ordem de classificação. Por exemplo, suponha que você crie um recurso com três propriedades personalizadas, onde os nomes de atributos sejam `name`, `secondName` e `asecondName`. Em seguida, você cria um elemento de ordem de classificação no nome do atributo e define o valor `ascending` como `true`.

Em seguida, você chama o método `ResourceRepositoryClient` do objeto `searchProperties` e passa na ordem de classificação. A pesquisa retorna o recurso certo, com as três propriedades. No entanto, as propriedades não são classificadas pelo nome do atributo. Eles são devolvidos na ordem em que foram adicionados: `name`, `secondName` e `asecondName`.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Repositório, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-5}

Para procurar recursos, siga estas etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço do Repositório.
1. Especifique a pasta do público alvo para a pesquisa.
1. Especifique os atributos usados na pesquisa.
1. Crie o query usado na pesquisa.
1. Crie a ordem de classificação para os resultados da pesquisa.
1. Procure os recursos.
1. Recupere os recursos do resultado da pesquisa.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de poder ler programaticamente um recurso, você deve estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Especificar a pasta de públicos alvos para a pesquisa**

Crie uma string contendo o caminho base a partir do qual realizar a pesquisa. A sintaxe inclui barras, como neste exemplo: &quot;/*path*/*folder*&quot;.

**Especificar os atributos usados na pesquisa**

Você pode basear sua pesquisa nos atributos contidos nos recursos. Especifique os valores dos atributos nos quais realizar a pesquisa.

**Criar o query usado na pesquisa**

Construa um query usando declarações e condições. Cada instrução especificará o atributo no qual basear a pesquisa, a condição a ser usada e o valor do atributo a ser usado na pesquisa.

**Criar a ordem de classificação para os resultados da pesquisa**

A ordem de classificação é composta de elementos, cada um dos quais contém um dos atributos usados na pesquisa e um valor que indica se a ordem crescente ou decrescente deve ser usada.

**Procurar recursos**

Procure os recursos usando a pasta, o query e a ordem de classificação. Além disso, indique a profundidade da pesquisa e um limite máximo do número de resultados a serem retornados.

**Recuperar os recursos do resultado da pesquisa**

Iterar por meio da lista de recursos retornada e extrair as informações para processamento posterior.

**Consulte também:**

[Procurar recursos usando a API Java](aem-forms-repository.md#search-for-resources-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Procure recursos usando a API Java {#search-for-resources-using-the-java-api}

Procure um recurso usando a API de serviço do Repositório (Java):

1. Incluir arquivos de projeto

   Inclua os arquivos JAR do cliente no caminho de classe do seu projeto Java.

1. Criar o cliente de serviço

   Crie um objeto `ResourceRepositoryClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Especificar a pasta de públicos alvos para a pesquisa

   Especifique o URI do caminho base a partir do qual a pesquisa será executada. Neste exemplo, o URI do recurso é `/testFolder`.

1. Especificar os atributos usados na pesquisa

   Especifique os valores dos atributos nos quais realizar a pesquisa. Os atributos existem em um objeto `com.adobe.repository.infomodel.bean.Resource`. Neste exemplo, a pesquisa será realizada no atributo name; portanto, um `java.lang.String` contendo o nome do objeto `Resource` é usado, que é `testResource` nesse caso.

1. Criar o query usado na pesquisa

   Para criar um query, crie um objeto `com.adobe.repository.query.Query` chamando o construtor padrão para a classe `Query` e adicione instruções ao query.

   Para criar uma instrução, chame o construtor para a classe `com.adobe.repository.query.Query.Statement` e passe os seguintes parâmetros:

   * Um operando esquerdo que contém a constante de atributo de recurso. Neste exemplo, como o nome do recurso é usado como a base para a pesquisa, o valor estático `Resource.ATTRIBUTE_NAME` é usado.
   * Um operador que contém a condição usada na pesquisa pelo atributo. O operador deve ser uma das constantes estáticas na classe `Query.Statement`. Neste exemplo, o valor estático `Query.Statement.OPERATOR_BEGINS_WITH` é usado.
   * Um operando direito contendo o valor do atributo no qual realizar a pesquisa. Neste exemplo, o atributo name, um `String` contendo o valor `"testResource"`, é usado.

   Especifique a namespace do operando esquerdo chamando o método `Query.Statement` do objeto `setNamespace` e transmitindo um dos valores estáticos contidos na classe `com.adobe.repository.infomodel.bean.ResourceProperty`. Neste exemplo, `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY` é usado.

   Adicione cada instrução ao query chamando o método `Query` do objeto `addStatement` e transmitindo o objeto `Query.Statement`.

1. Criar a ordem de classificação para os resultados da pesquisa

   Para especificar a ordem de classificação usada nos resultados da pesquisa, crie um objeto `com.adobe.repository.query.sort.SortOrder` chamando o construtor padrão para a classe `SortOrder` e adicione elementos à ordem de classificação.

   Para criar um elemento para a ordem de classificação, chame um dos construtores para a classe `com.adobe.repository.query.sort.SortOrder.Element`. Neste exemplo, como o nome do recurso é usado como a base para a pesquisa, o valor estático `Resource.ATTRIBUTE_NAME` é usado como o primeiro parâmetro e a ordem crescente (um valor `boolean` de `true`) é especificada como o segundo parâmetro.

   Adicione cada elemento à ordem de classificação chamando o método `SortOrder` do objeto `addSortElement` e transmitindo o objeto `SortOrder.Element`.

1. Procurar recursos

   Para pesquisar `resources` com base nas propriedades do atributo, chame o método `ResourceRepositoryClient` `searchProperties` do objeto e passe os seguintes parâmetros:

   * Um `String` contendo o caminho base a partir do qual a pesquisa será executada. Nesse caso, `"/testFolder"` é usado.
   * O query usado na pesquisa.
   * A profundidade da pesquisa. Nesse caso, `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` é usado para indicar que o caminho base e todas as suas pastas devem ser usados.
   * Um valor `int` que indica a primeira linha a partir da qual selecionar o conjunto de resultados não paginados. Neste exemplo, `0` é especificado.
   * Um valor `int` que indica o número máximo de resultados a serem retornados. Neste exemplo, `10` é especificado.
   * A ordem de classificação usada na pesquisa.

   O método retorna um `java.util.List` de `Resource` objetos na ordem de classificação especificada.

1. Recuperar os recursos do resultado da pesquisa

   Para recuperar os recursos contidos no resultado da pesquisa, repita `List` e converta cada objeto em `Resource` para extrair suas informações. Neste exemplo, o nome de cada recurso é exibido.

**Consulte também:**

[Procurando recursos](aem-forms-repository.md#searching-for-resources)

[Start rápido (modo SOAP): Procurando recursos usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Criando Relacionamentos de Recursos {#creating-resource-relationships}

Você pode especificar relacionamentos entre recursos no repositório. Existem três tipos de relações:

* **Dependência**: um relacionamento no qual um recurso depende de outros recursos, o que significa que todos os recursos relacionados são necessários no repositório.
* **Associação (sistema de arquivos)**: uma relação na qual um recurso está localizado em uma determinada pasta.
* **Personalizado**: uma relação especificada entre recursos. Por exemplo, se um recurso tiver sido descontinuado e outro recurso tiver sido introduzido no repositório, você poderá especificar sua própria relação de substituição.

Você pode criar seus próprios relacionamentos personalizados. Por exemplo, se você armazenar um arquivo HTML no repositório e ele usar uma imagem, poderá especificar uma relação personalizada para relacionar o arquivo HTML à imagem (já que normalmente somente os arquivos XML são associados a imagens usando uma relação de dependência definida pelo repositório). Outro exemplo de relacionamento personalizado seria se você quisesse criar uma visualização diferente do repositório com uma estrutura de gráfico cíclica em vez de uma estrutura em árvore. Você poderia definir um gráfico circular junto com um visualizador para atravessar essas relações. Por fim, você pode indicar que um recurso substitui outro, mesmo que os dois recursos sejam completamente diferentes. Nesse caso, você pode definir um tipo de relacionamento fora do intervalo reservado e criar uma relação entre esses dois recursos. Seu aplicativo seria o único cliente que poderia detectar e processar o relacionamento, e poderia ser usado para realizar pesquisas nesse relacionamento.

Você pode especificar programaticamente relações entre recursos usando a API Java do serviço do Repositório ou a API do serviço da Web.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Repositório, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-6}

Para especificar uma relação entre dois recursos, siga estas etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço do Repositório.
1. Especifique os URIs dos recursos a serem relacionados.
1. Crie a relação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de poder ler programaticamente um recurso, você deve estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Especificar os URIs dos recursos a serem relacionados**

Crie strings que contêm os URIs do recurso a ser relacionado. A sintaxe inclui barras, como neste exemplo: &quot;/*path*/*resource*&quot;.

**Criar a relação**

Chame o método de serviço Repositório para criar e especificar o tipo de relacionamento.

**Consulte também:**

[Criar recursos de relacionamento usando a API Java](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[Criar recursos de relacionamento usando a API de serviço da Web](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Criar recursos de relacionamento usando a API Java {#create-relationship-resources-using-the-java-api}

Crie recursos de relacionamento usando a API Java do serviço do Repositório, execute as seguintes tarefas:

1. Incluir arquivos de projeto

   Inclua os arquivos JAR do cliente no caminho de classe do seu projeto Java.

1. Criar o cliente de serviço

   Crie um objeto `ResourceRepositoryClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Especificar os URIs dos recursos a serem relacionados

   Especifique os URIs dos recursos a serem relacionados. Nesse caso, como os recursos são chamados de `testResource1` e `testResource2` e estão localizados na pasta `testFolder`, seus URIs são `"/testFolder/testResource1"` e `"/testFolder/testResource2"`. Os URIs são armazenados como objetos `java.lang.String`. Neste exemplo, os recursos são gravados primeiro no repositório e seus URIs são recuperados. Para obter mais informações sobre como gravar um recurso, consulte [Gravando recursos](aem-forms-repository.md#writing-resources).

1. Criar a relação

   Chame o método `ResourceRepositoryClient` do objeto `createRelationship` e passe os seguintes parâmetros:

   * O URI do recurso de origem.
   * O URI do recurso do público alvo.
   * O tipo de relacionamento, que é uma das constantes estáticas na classe `com.adobe.repository.infomodel.bean.Relation`. Neste exemplo, uma relação de dependência é estabelecida especificando o valor `Relation.TYPE_DEPENDANT_OF`.
   * Um valor `boolean` que indica se o recurso de público alvo é atualizado automaticamente para o identificador `com.adobe.repository.infomodel.Id` baseado no novo recurso de cabeçalho. Neste exemplo, devido à relação de dependência, o valor `true` é especificado.

   Você também pode recuperar uma lista de recursos relacionados para um determinado recurso, invocando o método `ResourceRepositoryClient` `getRelated` do objeto e transmitindo os seguintes parâmetros:

   * O URI do recurso para o qual recuperar recursos relacionados. Neste exemplo, o recurso de origem ( `"/testFolder/testResource1"`) é especificado.
   * Um valor `boolean` que indica se o recurso especificado é o recurso de origem no relacionamento. Neste exemplo, o valor `true` é especificado porque esse é o caso.
   * O tipo de relacionamento, que é uma das constantes estáticas na classe `Relation`. Neste exemplo, uma relação de dependência é especificada usando o mesmo valor usado anteriormente: `Relation.TYPE_DEPENDANT_OF`.

   O método `getRelated` retorna um `java.util.List` de `Resource` objetos através dos quais você pode iterar para recuperar cada um dos recursos relacionados, convertendo os objetos contidos em `List` em `Resource` à medida que você o faz. Neste exemplo, `testResource2` deve estar na lista de recursos retornados.

**Consulte também:**

[Criando Relações de Recursos](aem-forms-repository.md#creating-resource-relationships)

[Start rápido (modo SOAP): Criação de relações entre recursos usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Criar recursos de relacionamento usando a API de serviço da Web {#create-relationship-resources-using-the-web-service-api}

Crie recursos de relacionamento usando a API do repositório (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o WSDL do Repositório.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar o cliente de serviço

   Usando o assembly do cliente Microsoft .NET, crie um objeto `RepositoryServiceService` chamando seu construtor padrão. Defina sua propriedade `Credentials` usando um objeto `System.Net.NetworkCredential` contendo o nome de usuário e a senha.

1. Especificar os URIs dos recursos a serem relacionados

   Especifique os URIs dos recursos a serem relacionados. Nesse caso, como os recursos são chamados de `testResource1` e `testResource2` e estão localizados na pasta `testFolder`, seus URIs são `"/testFolder/testResource1"` e `"/testFolder/testResource2"`. Ao usar um idioma compatível com o Microsoft .NET Framework (por exemplo, C#), os URIs são armazenados como objetos `System.String`. Neste exemplo, os recursos são gravados primeiro no repositório e seus URIs são recuperados. Para obter mais informações sobre como gravar um recurso, consulte [Gravando recursos](aem-forms-repository.md#writing-resources).

1. Criar a relação

   Chame o método `RepositoryServiceService` do objeto `createRelationship` e passe os seguintes parâmetros:

   * O URI do recurso de origem.
   * O URI do recurso do público alvo.
   * O tipo de relacionamento. Neste exemplo, uma relação de dependência é estabelecida especificando o valor `3`.
   * Um valor `boolean` que indica se o tipo de relação foi especificado. Neste exemplo, o valor `true` é especificado.
   * Um valor `boolean` que indica se o recurso de público alvo é atualizado automaticamente para o identificador `Id` baseado no novo recurso de cabeçalho. Neste exemplo, devido à relação de dependência, o valor `true` é especificado.
   * Um valor `boolean` que indica se o cabeçalho do público alvo foi especificado. Neste exemplo, o valor `true` é especificado.
   * Passe `null` para o último parâmetro.

   Você também pode recuperar uma lista de recursos relacionados para um determinado recurso, invocando o método `RepositoryServiceService` `getRelated` do objeto e transmitindo os seguintes parâmetros:

   * O URI do recurso para o qual recuperar recursos relacionados. Neste exemplo, o recurso de origem ( `"/testFolder/testResource1"`) é especificado.
   * Um valor `boolean` que indica se o recurso especificado é o recurso de origem no relacionamento. Neste exemplo, o valor `true` é especificado porque esse é o caso.
   * Um valor `boolean` que indica se o recurso de origem foi especificado. Neste exemplo, o valor `true` é fornecido.
   * Uma matriz de números inteiros contendo os tipos de relacionamento. Neste exemplo, uma relação de dependência é especificada usando o mesmo valor na matriz como foi usado anteriormente: `3`.
   * Passe `null` para os dois parâmetros restantes.

   O método `getRelated` retorna uma matriz de objetos que podem ser convertidos em `Resource` objetos através dos quais você pode iterar para recuperar cada um dos recursos relacionados. Neste exemplo, `testResource2` deve estar na lista de recursos retornados.

**Consulte também:**

[Criando Relações de Recursos](aem-forms-repository.md#creating-resource-relationships)

[Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Bloquear recursos {#locking-resources}

Você pode bloquear um recurso ou conjunto de recursos para uso exclusivo por um usuário específico ou uso compartilhado entre mais de um usuário. Um bloqueio compartilhado é uma indicação de que algo acontecerá com o recurso, mas não impede que mais ninguém tome ações com esse recurso. Um bloqueio compartilhado deve ser considerado um mecanismo de sinalização. Um bloqueio exclusivo significa que o usuário que bloqueou o recurso vai alterar o recurso, e o bloqueio garante que ninguém mais possa fazer isso até que o usuário não precise mais de acesso ao recurso e tenha liberado o bloqueio. Se um administrador do repositório desbloquear um recurso, todos os bloqueios exclusivos e compartilhados nesse recurso serão removidos automaticamente. Esse tipo de ação destina-se a situações em que um usuário não está mais disponível e não desbloqueou o recurso.

Quando um recurso é bloqueado, um ícone de cadeado é exibido quando você visualização a guia Recursos localizada no Workbench, como mostra a ilustração a seguir.

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

Você pode controlar programaticamente o acesso aos recursos usando a API Java do serviço do Repositório ou a API do serviço da Web.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Repositório, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-7}

Para bloquear e desbloquear recursos, siga estas etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço do Repositório.
1. Especifique o URI do recurso a ser bloqueado.
1. Bloquear o recurso.
1. Recupere os bloqueios do recurso.
1. Desbloquear o recurso

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de poder ler programaticamente um recurso, você deve estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Especificar o URI do recurso a ser bloqueado**

Crie uma string contendo o URI do recurso a ser bloqueado. A sintaxe inclui barras, como neste exemplo: &quot;/*path*/*resource*&quot;.

**Bloquear o recurso**

Chame o método de serviço Repositório para bloquear o recurso, especificando o URI, o tipo de bloqueio e a profundidade de bloqueio.

**Recuperar os bloqueios do recurso**

Chame o método de serviço Repositório para recuperar os bloqueios do recurso, especificando o URI.

**Desbloquear o recurso**

Chame o método de serviço Repositório para desbloquear o recurso, especificando o URI.

**Consulte também:**

[Bloquear recursos usando a API Java](aem-forms-repository.md#lock-resources-using-the-java-api)

[Bloquear recursos usando a API de serviço da Web](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Bloquear recursos usando a API Java {#lock-resources-using-the-java-api}

Bloquear recursos usando a API de serviço do Repositório (Java):

1. Incluir arquivos de projeto

   Inclua os arquivos JAR do cliente no caminho de classe do seu projeto Java.

1. Criar o cliente de serviço

   Crie um objeto `ResourceRepositoryClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Especificar o URI do recurso a ser bloqueado

   Especifique o URI do recurso a ser bloqueado. Nesse caso, como o recurso chamado `testResource` está na pasta chamada `testFolder`, seu URI é `"/testFolder/testResource"`. O URI é armazenado como um objeto `java.lang.String`.

1. Bloquear o recurso

   Chame o método `ResourceRepositoryClient` do objeto `lockResource` e passe os seguintes parâmetros:

   * O URI do recurso.
   * O escopo do cadeado. Neste exemplo, como o recurso será bloqueado para uso exclusivo, o escopo de bloqueio é especificado como `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`.
   * A profundidade do cadeado. Neste exemplo, como o bloqueio se aplicará somente ao recurso específico e nenhum de seus membros ou filhos, a profundidade de bloqueio é especificada como `Lock.DEPTH_ZERO`.

   >[!NOTE]
   >
   >A versão sobrecarregada do método `lockResource` que requer quatro parâmetros lança uma exceção. Certifique-se de usar o método `lockResource` que requer três parâmetros, conforme mostrado nesta apresentação.

1. Recuperar os bloqueios do recurso

   Chame o método `ResourceRepositoryClient` do objeto `getLocks` e passe o URI do recurso como um parâmetro. O método retorna uma Lista de objetos Lock pela qual você pode iterar. Neste exemplo, o proprietário, a profundidade e o escopo do bloqueio são impressos para cada objeto, chamando os métodos `getOwnerUserId`, `getDepth` e `getType` de cada objeto de bloqueio, respectivamente.

1. Desbloquear o recurso

   Chame o método `ResourceRepositoryClient` do objeto `unlockResource` e passe o URI do recurso como um parâmetro. Para obter mais informações, consulte a [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Consulte também:**

[Bloquear recursos](aem-forms-repository.md#locking-resources)

[Start rápido (modo SOAP): Bloquear um recurso usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Bloquear recursos usando a API de serviço da Web {#lock-resources-using-the-web-service-api}

Bloquear recursos usando a API de serviço do Repositório (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o WSDL do Repositório usando o Base64.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar o cliente de serviço

   Usando o assembly do cliente Microsoft .NET, crie um objeto `RepositoryServiceService` chamando seu construtor padrão. Defina sua propriedade `Credentials` usando um objeto `System.Net.NetworkCredential` contendo o nome de usuário e a senha.

1. Especificar o URI do recurso a ser bloqueado

   Especifique uma string que contenha o URI do recurso a ser bloqueado. Nesse caso, como o recurso chamado `testResource` está na pasta `testFolder`, seu URI é `"/testFolder/testResource"`. Ao usar um idioma compatível com o Microsoft .NET Framework (por exemplo, C#), armazene o URI em um objeto `System.String`.

1. Bloquear o recurso

   Chame o método `RepositoryServiceService` do objeto `lockResource` e passe os seguintes parâmetros:

   * O URI do recurso.
   * O escopo do cadeado. Neste exemplo, como o recurso será bloqueado para uso exclusivo, o escopo de bloqueio é especificado como `11`.
   * A profundidade do cadeado. Neste exemplo, como o bloqueio se aplicará somente ao recurso específico e nenhum de seus membros ou filhos, a profundidade de bloqueio é especificada como `2`.
   * Um valor `int` que indica o número de segundos até que o bloqueio expire. Neste exemplo, o valor de `1000` é usado.
   * Passe `null` para o último parâmetro.

1. Recuperar os bloqueios do recurso

   Chame o método `RepositoryServiceService` do objeto `getLocks` e passe o URI do recurso como o primeiro parâmetro e `null` como o segundo parâmetro. O método retorna uma matriz `object` contendo objetos `Lock` através dos quais você pode iterar. Neste exemplo, o proprietário, a profundidade e o escopo do bloqueio são impressos para cada objeto acessando os campos `Lock`, `depth` e `type` de cada objeto, respectivamente.`ownerUserId`

1. Desbloquear o recurso

   Chame o método `RepositoryServiceService` do objeto `unlockResource` e passe o URI do recurso como o primeiro parâmetro e `null` como o segundo parâmetro.

**Consulte também:**

[Bloquear recursos](aem-forms-repository.md#locking-resources)

[Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Excluindo Recursos {#deleting-resources}

Você pode excluir programaticamente os recursos de um determinado local no repositório usando a API Java (SOAP) do serviço do Repositório.

Quando você exclui um recurso, a exclusão normalmente é permanente, embora em alguns casos os repositórios ECM possam armazenar as versões do recurso de acordo com seus mecanismos de histórico. Portanto, ao excluir um recurso, é importante ter certeza de que você nunca precisará desse recurso novamente. Os motivos comuns para excluir um recurso incluem a necessidade de aumentar o espaço disponível no banco de dados. É possível excluir uma versão de um recurso, mas se você fizer isso, deverá especificar o identificador do recurso, e não seu identificador lógico (LID) ou caminho. Se você excluir uma pasta, tudo nessa pasta, incluindo subpastas e recursos, será automaticamente excluído.

Os recursos relacionados não são excluídos. Por exemplo, se você tiver um formulário que usa o arquivo logo.gif e excluir logo.gif, uma relação será armazenada na tabela de relacionamento pendente. Como alternativa, para a substituição da versão, defina o status do objeto da versão mais recente como obsoleto.

Uma operação de exclusão não é segura para transações em sistemas ECM. Por exemplo, se você tentar excluir 100 recursos e a operação falhar no 50º recurso, as primeiras 49 instâncias serão excluídas, mas o restante não será. Caso contrário, o comportamento padrão será revertido (sem compromisso).

>[!NOTE]
>
>Ao usar o método `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` com repositório ECM (EMC Documentum Content Server e IBM FileNet P8 Content Manager), a transação não será revertida se a exclusão falhar para um dos recursos especificados, o que significa que os arquivos que foram excluídos não podem ser removidos.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Repositório, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-8}

Para excluir um recurso, siga estas etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço do Repositório.
1. Especifique o URI do recurso a ser excluído.
1. Exclua o recurso.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de poder ler programaticamente um recurso, você deve estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Especificar o URI do recurso a ser excluído**

Crie uma string contendo o URI do recurso a ser excluído. A sintaxe inclui barras, como neste exemplo: &quot;/*path*/*resource*&quot;. Se o recurso a ser excluído for uma pasta, a exclusão será recursiva.

**Excluir o recurso**

Chame o método de serviço Repositório para excluir o recurso, especificando o URI.

**Consulte também:**

[Excluir recursos usando a API Java](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[Excluir recursos usando a API de serviço da Web](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Excluir recursos usando a API Java (SOAP) {#delete-resources-using-the-java-api-soap}

Exclua um recurso usando a API do repositório (Java):

1. Incluir arquivos de projeto

   Inclua os arquivos JAR do cliente no caminho de classe do seu projeto Java.

1. Criar o cliente de serviço

   Crie um objeto `ResourceRepositoryClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Especificar o URI do recurso a ser excluído

   Especifique o URI do recurso a ser recuperado. Nesse caso, como o recurso chamado testResourceToBeDeleted está na pasta chamada testFolder, seu URI é `/testFolder/testResourceToBeDeleted`. O URI é armazenado como um objeto `java.lang.String`. Neste exemplo, o recurso é gravado primeiro no repositório e seu URI é recuperado. Para obter mais informações sobre como gravar um recurso, consulte [Gravando recursos](aem-forms-repository.md#writing-resources).

1. Excluir o recurso

   Chame o método `ResourceRepositoryClient` do objeto `deleteResource` e passe o URI do recurso como um parâmetro.

**Consulte também:**

[Excluindo recursos](aem-forms-repository.md#deleting-resources)

[Start rápido (modo SOAP): Procurando recursos usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Excluir recursos usando a API de serviço da Web {#delete-resources-using-the-web-service-api}

Exclua um recurso usando a API do repositório (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o WSDL do Repositório usando o Base64.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar o cliente de serviço

   Usando o assembly do cliente Microsoft .NET, crie um objeto `RepositoryServiceService` chamando seu construtor padrão. Defina sua propriedade `Credentials` usando um objeto `System.Net.NetworkCredential` contendo o nome de usuário e a senha.

1. Especificar o URI do recurso a ser excluído

   Especifique o URI do recurso a ser recuperado. Nesse caso, como o recurso chamado `testResourceToBeDeleted` está na pasta chamada `testFolder`, seu URI é `"/testFolder/testResourceToBeDeleted"`. Neste exemplo, o recurso é gravado primeiro no repositório e seu URI é recuperado. Para obter mais informações sobre como gravar um recurso, consulte [Gravando recursos](aem-forms-repository.md#writing-resources).

1. Excluir o recurso

   Chame o método `RepositoryServiceService` do objeto `deleteResources` e passe uma matriz `System.String` contendo o URI do recurso como o primeiro parâmetro. Passe `null` para o segundo parâmetro.

**Consulte também:**

[Excluindo recursos](aem-forms-repository.md#deleting-resources)

[Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
