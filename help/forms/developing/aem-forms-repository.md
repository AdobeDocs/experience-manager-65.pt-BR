---
title: Trabalhar com o repositório do AEM Forms
description: Gerencie o repositório do AEM Forms para criar recursos de pastas, gravação, lista, leitura, atualização e pesquisa usando a API Java e a API de serviço da Web. Além disso, saiba como criar relações de recursos, bloquear e excluir recursos.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: a07e51ca-fea0-4719-8071-1b7e805de2ae
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '9036'
ht-degree: 0%

---

# Trabalhar com o repositório do AEM Forms {#working-with-aem-forms-repository}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

**Sobre o Serviço de repositório**

O serviço Repository fornece serviços de armazenamento e gerenciamento de recursos para a AEM Forms. Quando os desenvolvedores criam um *AEM Forms* aplicativo, eles podem implantar os ativos no repositório em vez do sistema de arquivos. Os ativos podem incluir qualquer tipo de material adicional, incluindo formulários XML, PDF forms (incluindo formulários Acrobat), fragmentos de formulário, imagens, perfis, políticas, arquivos SWF, arquivos DDX, esquemas XML, arquivos WSDL e dados de teste.

Por exemplo, considere o seguinte aplicativo do Forms chamado *Aplicativos/FormuláriosAplicativo*:

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

Observe que há um arquivo chamado Loan.xdp na FormsFolder. Para acessar este design de formulário, especifique o caminho completo (incluindo a versão): `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Para obter informações sobre como criar um aplicativo Forms usando o Workbench, consulte [Ajuda do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

O caminho para um recurso no repositório do AEM Forms é:

`Applications/Application-name/Application-version/Folder.../Filename`

Os seguintes valores mostram alguns exemplos de valores de URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>Você pode navegar pelo repositório do AEM Forms usando um navegador da Web. Para navegar no repositório, insira o seguinte URL em um navegador da Web `https://[server name]:[server port]/repository`. Você pode verificar os resultados de início rápido associados à seção Trabalho com o repositório do AEM Forms usando um navegador da Web. Por exemplo, se você adicionar conteúdo ao Repositório do AEM Forms, poderá ver o conteúdo em um navegador da Web. (Consulte [Início rápido (modo SOAP): Gravação de um recurso usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

A API do repositório fornece várias operações que você pode usar para armazenar e recuperar informações do repositório. Por exemplo, você pode obter uma lista de recursos ou recuperar recursos específicos armazenados no repositório quando um recurso é necessário como parte do processamento de um aplicativo.

>[!NOTE]
>
>A API do repositório não pode ser usada para interagir com os Serviços de conteúdo (descontinuado). Para interagir com os Serviços de conteúdo (obsoleto), use a API de gerenciamento de documentos.

Usando a API de serviço do Repositório, você pode realizar as seguintes tarefas:

* Criar pastas. Consulte [Criação de pastas](aem-forms-repository.md#creating-folders).
* Gravar recursos e suas propriedades. Consulte [Recursos de gravação](aem-forms-repository.md#writing-resources).
* Listar recursos em uma determinada coleção ou relacionados a outros recursos. Consulte [Listando recursos](aem-forms-repository.md#listing-resources).
* Leia os recursos e suas propriedades. Consulte [Recursos de leitura](aem-forms-repository.md#reading-resources).
* Atualizar recursos e suas propriedades. Consulte [Atualização de recursos](aem-forms-repository.md#updating-resources).
* Pesquise recursos, incluindo seu histórico, recursos relacionados e propriedades. Consulte [Pesquisando Recursos](aem-forms-repository.md#searching-for-resources).
* Especificar relações entre recursos. Consulte [Criando Relações de Recursos](aem-forms-repository.md#creating-resource-relationships).
* Gerencie o controle de acesso a recursos, incluindo bloqueio e desbloqueio de recursos, além de ler e gravar listas de controle de acesso (ACLs). Consulte [Bloquear recursos](aem-forms-repository.md#locking-resources).
* Excluir recursos e suas propriedades. Consulte [Exclusão de recursos](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>Usando a API do repositório, não é possível gerenciar o controle de acesso a recursos, pesquisar recursos ou especificar relações de recursos usando um repositório ECM.

>[!NOTE]
>
>Quando um PDF criptografado é gravado no repositório, o recurso de extração automatizada de relacionamento não pode ser usado. Caso contrário, um PDF criptografado poderá ser armazenado no repositório e recuperado posteriormente. O recuperador pode optar por descriptografar o PDF após ser recuperado do repositório.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de repositório, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Criação de pastas {#creating-folders}

Pastas (coleções de recursos) são usadas para armazenar objetos (arquivos ou recursos) em agrupamentos organizados. As pastas podem conter recursos e outras pastas, também conhecidas como subpastas. Os recursos só podem ser armazenados em uma pasta por vez.

Os arquivos herdam ACLs (listas de controle de acesso) de pastas, e as subpastas herdam ACLs de suas pastas principais. Portanto, as pastas principais devem existir antes que você possa criar pastas secundárias. O IDE permite interagir somente pasta por pasta, não arquivo por arquivo. Não é possível criar a versão das pastas e não há necessidade de fazer isso; uma pasta não contém dados propriamente ditos. Em vez disso, ele é apenas um container para recursos que contêm dados. A ACL padrão é a permissão no nível do sistema, o que significa que os usuários devem ter permissões no nível do sistema (ler, gravar, atravessar, gerenciar ACLs) até que alguém lhes dê permissões para uma pasta específica. As ACLs funcionam somente no IDE.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de repositório, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para criar uma pasta, siga estas etapas:

1. Incluir arquivos de projeto.
1. Criar o cliente de serviço.
1. Crie a pasta.
1. Grave a pasta no repositório.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de criar programaticamente uma coleção de recursos, você deve estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Criar a pasta**

Chame o método de serviço Repositório para criar a coleção de recursos e preencha a coleção de recursos com informações de identificação, incluindo UUID, nome da pasta e descrição.

**Gravar a pasta no repositório**

Chame o método do Serviço de repositório para gravar a coleção de recursos, especificando o URI da pasta de destino.

**Consulte também**

[Criar pastas usando a API Java](aem-forms-repository.md#create-folders-using-the-java-api)

[Criar pastas usando a API do serviço Web](aem-forms-repository.md#create-folders-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Criar pastas usando a API Java {#create-folders-using-the-java-api}

Crie uma pasta usando a API de serviço do Repositório (Java):

1. Incluir arquivos de projeto

   Inclua arquivos de projeto no caminho de classe do seu projeto Java.

1. Criar o cliente de serviço

   Criar um `ResourceRepositoryClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Criar a pasta

   Para criar uma coleção de recursos, primeiro crie uma `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` objeto.

   Chame o `repositoryInfomodelFactoryBean` do objeto `newResourceCollection` e transmita os seguintes parâmetros:

   * A `com.adobe.repository.infomodel.Id` Identificador UUID a ser atribuído ao recurso.
   * A `com.adobe.repository.infomodel.Lid` Identificador UUID a ser atribuído ao recurso.
   * A `java.lang.String` contendo o nome da coleção de recursos. Por exemplo, `FormsFolder`.

   O método retorna um valor de `com.adobe.repository.infomodel.bean.ResourceCollection` objeto que representa a nova pasta.

   Defina a descrição da pasta usando o `setDescription` e passe no seguinte parâmetro:

   * A `String` que descreve a coleção de recursos. Neste exemplo, `"test Folder"` é usado `.`

1. Gravar a pasta no repositório

   Chame o `ResourceRepositoryClient` do objeto `writeResource` e transmita o URI da pasta e a variável `ResourceCollection` objeto. Por exemplo, o URI para a pasta pode ser o seguinte valor `/Applications/FormsApplication/1.0/`.

   O método retorna uma instância do recém-criado `com.adobe.repository.infomodel.bean.Resource` objeto. Você pode, por exemplo, recuperar o valor do identificador do novo recurso chamando o `com.adobe.repository.infomodel.bean.Resource` do objeto `getId` método.

**Consulte também**

[Criação de pastas](aem-forms-repository.md#creating-folders)

[Início rápido (modo SOAP): criação de uma pasta usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Criar pastas usando a API do serviço Web {#create-folders-using-the-web-service-api}

Crie uma pasta usando a API de serviço do Repositório (serviço Web):

1. Incluir arquivos de projeto

   * Crie um assembly cliente Microsoft .NET que consuma o WSDL do repositório usando base64.
   * Referencie o assembly do cliente Microsoft .NET.

1. Criar o cliente de serviço

   Usando o assembly cliente Microsoft .NET, crie um `RepositoryServiceService` chamando seu construtor padrão. Defina suas `Credentials` propriedade usando um `System.Net.NetworkCredential` objeto que contém o nome de usuário e a senha.

1. Criar a pasta

   Crie a pasta usando o construtor padrão para o `ResourceCollection` e transmitem os seguintes parâmetros:

   * Um `Id` objeto, que é criado chamando o construtor padrão para o `Id` e atribuído à `Resource` do objeto `id` campo.
   * Um `Lid` objeto, que é criado chamando o construtor padrão para o `Lid` e atribuído à `Resource` do objeto `lid` campo.
   * Uma string que contém o nome da coleção de recursos, que é atribuída à variável `Resource` do objeto `name` campo. O nome usado neste exemplo é `"testfolder"`.
   * Uma string que contém a descrição da coleção de recursos atribuída ao `Resource` do objeto `description` campo. A descrição usada neste exemplo é `"test folder"`.

1. Gravar a pasta no repositório

   Chame o `RepositoryServiceService` do objeto `writeResource` e transmita os seguintes parâmetros:

   * O caminho onde a pasta deve ser criada.
   * A variável `ResourceCollection` objeto que representa a pasta.
   * Aprovado `null` para os outros dois parâmetros.

**Consulte também**

[Criação de pastas](aem-forms-repository.md#creating-folders)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Recursos de gravação {#writing-resources}

Você pode criar recursos em um determinado local no repositório. O tamanho natural do arquivo está sujeito às limitações do banco de dados e ao tempo limite da sessão. Para a configuração padrão, os arquivos são limitados a 25 MB. Para aumentar ou diminuir o tamanho máximo do arquivo, você deve alterar a configuração do banco de dados.

Os recursos de gravação são equivalentes ao armazenamento de dados no repositório. Depois de gravar um recurso no repositório, ele se torna acessível a todos os clientes no ecossistema do repositório. Quando você grava recursos, como esquemas XML, arquivos XDP e arquivos XSD no repositório, o conteúdo é analisado com base no tipo MIME. Se o tipo MIME for compatível, o analisador determinará se há uma relação implícita com outro conteúdo. Por exemplo, se uma folha de estilos em cascata (CSS) tiver um URL relativo que faça referência a um CSS comum, espera-se que você também envie o CSS comum para o repositório. O relacionamento entre os dois recursos é armazenado como um relacionamento pendente por um período não ajustável de 30 dias. Quando você envia o CSS comum para o repositório no período de 30 dias, a relação é formada.

Quando você cria um recurso, a lista de controle de acesso (ACL) é herdada da pasta principal. A pasta raiz tem permissões no nível do sistema até que um recurso ou pasta inicial seja criado, momento em que o recurso ou pasta recebe permissões ACL padrão.

Você pode gravar recursos de forma programática usando a API Java do serviço de repositório ou a API do serviço da Web.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de repositório, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para gravar um recurso, siga estas etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço de Repositório.
1. Especifique o URI do recurso a ser lido.
1. Leia o recurso.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de ler programaticamente um recurso, é necessário estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Especifique o URI da pasta de destino para o recurso**

Crie uma cadeia de caracteres contendo o URI do recurso a ser lido. A sintaxe inclui barras, como neste exemplo: &quot;/*caminho*/*pasta*&quot;.

**Criar o recurso**

Chame o método de serviço do Repositório para criar o recurso e preencha o recurso com informações de identificação, incluindo sua UUID, nome do recurso e descrição.

**Especificar o conteúdo do recurso**

Chame o método de serviço do Repositório para criar conteúdo de recurso e armazenar esse conteúdo no recurso.

**Gravar o recurso na pasta de destino**

Chame o método do Serviço de repositório para gravar o recurso, especificando o URI da pasta de destino.

**Consulte também**

[Gravar recursos usando a API Java](aem-forms-repository.md#write-resources-using-the-java-api)

[Gravar recursos usando a API do serviço Web](aem-forms-repository.md#write-resources-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Gravar recursos usando a API Java {#write-resources-using-the-java-api}

Grave um recurso usando a API de serviço do Repositório (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente no caminho de classe do projeto Java.

1. Criar o cliente de serviço

   Criar um `ResourceRepositoryClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Especifique o URI da pasta de destino para o recurso

   Especifique o URI da pasta de destino do recurso. Nesse caso, como o recurso chamado `testResource` será armazenado na pasta chamada `testFolder`, o URI da pasta é `"/testFolder"`. O URI é armazenado como um `java.lang.String` objeto.

1. Criar o recurso

   Para criar um recurso, primeiro crie um `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` objeto.

   Chame o `RepositoryInfomodelFactoryBean` do objeto `newResource` que cria um `com.adobe.repository.infomodel.bean.Resource` objeto. Neste exemplo, os seguintes parâmetros são fornecidos:

   * A `com.adobe.repository.infomodel.Id` objeto, que é criado chamando o construtor padrão para o `Id` classe.
   * A `com.adobe.repository.infomodel.Lid` objeto, que é criado chamando o construtor padrão para o `Lid` classe.
   * A `java.lang.String` contendo o nome de arquivo do recurso.

   Para especificar a descrição do recurso, chame o `Resource` do objeto `setDescription` e transmita uma string contendo a descrição. Neste exemplo, a descrição é `"test resource"`.

1. Especificar o conteúdo do recurso

   Para criar conteúdo para o recurso, chame o `RepositoryInfomodelFactoryBean` do objeto `newResourceContent` método, que retorna um `com.adobe.repository.infomodel.bean.ResourceContent` objeto. Adicionar conteúdo à `ResourceContent` objeto. Neste exemplo, isso é realizado fazendo as seguintes tarefas:

   * Chamar o `ResourceContent` do objeto `setDataDocument` e transmitindo em um `com.adobe.idp.Document` objeto
   * Chamar o `ResourceContent` do objeto `setSize` e transmitindo o tamanho em bytes do método `Document` objeto

   Adicione o conteúdo ao recurso chamando o `Resource` do objeto `setContent` e transmitindo o `ResourceContent` objeto. Para obter mais informações, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Gravar o recurso na pasta de destino

   Chame o `ResourceRepositoryClient` do objeto `writeResource` e transmita o URI da pasta, e a variável `Resource` objeto.

**Consulte também**

[Recursos de gravação](aem-forms-repository.md#writing-resources)

[Início rápido (modo SOAP): Gravação de um recurso usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Gravar recursos usando a API do serviço Web {#write-resources-using-the-web-service-api}

Grave um recurso usando a API de serviço do Repositório (serviço Web):

1. Incluir arquivos de projeto

   * Crie um assembly cliente Microsoft .NET que consuma o WSDL do repositório usando base64.
   * Referencie o assembly do cliente Microsoft .NET.

1. Criar o cliente de serviço

   Usando o assembly cliente Microsoft .NET, crie um `RepositoryServiceService` chamando seu construtor padrão. Defina suas `Credentials` propriedade usando um `System.Net.NetworkCredential` objeto que contém o nome de usuário e a senha.

1. Especifique o URI da pasta de destino para o recurso

   Especifique o URI da pasta de destino do recurso. Nesse caso, como o recurso chamado `testResource` será armazenado na pasta chamada `testFolder`, o URI da pasta é `"/testFolder"`. Ao usar uma linguagem compatível com o Microsoft .NET Framework (por exemplo, C#), armazene o URI em uma `System.String` objeto.

1. Criar o recurso

   Para criar um recurso, chame o construtor padrão para o `Resource` classe. Neste exemplo, as seguintes informações são armazenadas na variável `Resource` objeto:

   * A `com.adobe.repository.infomodel.Id` objeto, que é criado chamando o construtor padrão para o `Id` e atribuído à `Resource` do objeto `id` campo.
   * A `com.adobe.repository.infomodel.Lid` objeto, que é criado chamando o construtor padrão para o `Lid` e atribuído à `Resource` do objeto `lid` campo.
   * Uma string contendo o nome de arquivo do recurso, que é atribuída à variável `Resource` do objeto `name` campo. O nome usado neste exemplo é `"testResource"`.
   * Uma string que contém a descrição do recurso, que é atribuída à variável `Resource` do objeto `description` campo. A descrição usada neste exemplo é `"test resource"`.

1. Especificar o conteúdo do recurso

   Para criar conteúdo para o recurso, chame o construtor padrão para o `ResourceContent` classe. Em seguida, adicione o conteúdo ao `ResourceContent` objeto. Neste exemplo, isso é realizado fazendo as seguintes tarefas:

   * Atribuição de um `BLOB` objeto que contém um documento para o `ResourceContent` do objeto `dataDocument` campo.
   * Atribuição do tamanho em bytes do `BLOB` objeto para o `ResourceContent` do objeto `size` campo.

   Adicione o conteúdo ao recurso atribuindo o `ResourceContent` objeto para o `Resource` do objeto `content` campo.

1. Gravar o recurso na pasta de destino

   Chame o `RepositoryServiceService` do objeto `writeResource` e transmita o URI da pasta, e a variável `Resource` objeto. Aprovado `null` para os outros dois parâmetros.

**Consulte também**

[Recursos de gravação](aem-forms-repository.md#writing-resources)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Listando recursos {#listing-resources}

Você pode descobrir recursos listando-os. Uma consulta é executada no repositório para localizar todos os recursos relacionados a uma determinada coleção de recursos.

Depois de organizar os recursos, é possível inspecionar a estrutura criada vendo uma ramificação específica da estrutura, como faria em um sistema operacional.

Listando recursos opera por relacionamento: os recursos são membros de pastas. A associação é representada por um relacionamento do tipo &quot;membro de&quot;. Ao listar recursos em uma determinada pasta, você está consultando recursos que estão relacionados a uma determinada pasta pelo relacionamento &quot;membro de&quot;. As relações são direcionais: um membro de uma relação tem uma origem que é membro do destino. A origem é o recurso; o destino é a pasta principal.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de repositório, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-2}

Para listar recursos, siga estas etapas:

1. Incluir arquivos de projeto.
1. Criar o cliente de serviço.
1. Especifique o caminho da pasta.
1. Recuperar a lista de recursos.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de criar programaticamente uma coleção de recursos, você deve estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Especificar o caminho da pasta**

Crie uma cadeia de caracteres que contenha o caminho da pasta que contém os recursos. A sintaxe inclui barras, como neste exemplo: &quot;/*caminho*/*pasta*&quot;.

**Recuperar a lista de recursos**

Chame o método do Serviço de repositório para recuperar a lista de recursos, especificando o caminho da pasta de destino.

**Consulte também**

[Listar recursos usando a API Java](aem-forms-repository.md#list-resources-using-the-java-api)

[Listar recursos usando a API do serviço Web](aem-forms-repository.md#list-resources-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Listar recursos usando a API Java {#list-resources-using-the-java-api}

Liste recursos usando a API de serviço do Repositório (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente no caminho de classe do projeto Java.

1. Criar o cliente de serviço

   Criar um `ResourceRepositoryClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Especificar o caminho da pasta

   Especifique o URI da coleção de recursos a ser consultada. Nesse caso, seu URI é `"/testFolder"`. O URI é armazenado como um `java.lang.String` objeto.

1. Recuperar a lista de recursos

   Chame o `ResourceRepositoryClient` do objeto `listMembers` e passe no URI da pasta.

   O método retorna um valor de `java.util.List` de `com.adobe.repository.infomodel.bean.Resource` objetos que são a origem de um `com.adobe.repository.infomodel.bean.Relation` do tipo `Relation.TYPE_MEMBER_OF` e têm o URI da coleção de recursos como destino. Você pode iterar através disso `List` para recuperar cada recurso. Neste exemplo, o nome e a descrição de cada recurso são exibidos.

**Consulte também**

[Listando recursos](aem-forms-repository.md#listing-resources).

[Início rápido (modo SOAP): listar recursos usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Listar recursos usando a API do serviço Web {#list-resources-using-the-web-service-api}

Liste recursos usando a API de serviço do Repositório (serviço Web):

1. Incluir arquivos de projeto

   * Crie um assembly cliente Microsoft .NET que consuma o WSDL do repositório.
   * Referencie o assembly do cliente Microsoft .NET.

1. Criar o cliente de serviço

   Usando o assembly cliente Microsoft .NET, crie um `RepositoryServiceService` chamando seu construtor padrão. Defina suas `Credentials` propriedade usando um `System.Net.NetworkCredential` objeto que contém o nome de usuário e a senha.

1. Especificar o caminho da pasta

   Especifique uma cadeia de caracteres que contenha o URI da pasta a ser consultada. Nesse caso, seu URI é `"/testFolder"`. Ao usar uma linguagem compatível com o Microsoft .NET Framework (por exemplo, C#), armazene o URI em uma `System.String` objeto.

1. Recuperar a lista de recursos

   Chame o `RepositoryServiceService` do objeto `listMembers` e transmita o URI da pasta como o primeiro parâmetro. Aprovado `null` para os outros dois parâmetros.

   O método retorna uma matriz de objetos que podem ser convertidos em `Resource` objetos. É possível iterar por meio da matriz de objetos para recuperar cada um dos recursos relacionados. Neste exemplo, o nome e a descrição de cada recurso são exibidos.

**Consulte também**

[Listando recursos](aem-forms-repository.md#listing-resources).

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Recursos de leitura {#reading-resources}

Você pode recuperar recursos de um determinado local no repositório para ler seu conteúdo e metadados. O workflow é front-end por um formulário de inicialização. O processo tem todas as permissões necessárias para ler o formulário. O sistema recupera o formulário de dados e lê o conteúdo do repositório. O repositório concede acesso ao conteúdo e aos metadados (a capacidade de até mesmo saber se o recurso existe).

O repositório tem quatro tipos de permissão:

* **travessia**: permite listar recursos; ou seja, ler metadados de recursos, mas não conteúdo de recursos
* **ler**: permite ler o conteúdo do recurso
* **gravação**: permite gravar o conteúdo do recurso
* **gerenciando listas de controle de acesso (ACLs)**: permite manipular ACLs em recursos

Os usuários só podem executar processos quando têm permissão para executar o processo. Os usuários do IDE precisam de permissões de travessia e leitura para sincronizar com o repositório. As ACLs se aplicam somente em tempo de design, pois o tempo de execução ocorre no contexto do sistema.

Você pode ler recursos programaticamente usando a API Java do serviço de repositório ou a API do serviço da Web.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de repositório, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-3}

Para ler um recurso, siga estas etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço de Repositório.
1. Especifique o URI do recurso a ser lido.
1. Leia o recurso.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de ler programaticamente um recurso, é necessário estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Especifique o URI do recurso a ser lido**

Crie uma cadeia de caracteres contendo o URI do recurso a ser lido. A sintaxe inclui barras, como neste exemplo: &quot;/*caminho*/*recurso*&quot;.

**Ler o recurso**

Chame o método do Serviço de repositório para ler o recurso, especificando o URI.

**Consulte também**

[Ler recursos usando a API Java](aem-forms-repository.md#read-resources-using-the-java-api)

[Lendo recursos usando a API do serviço Web](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Ler recursos usando a API Java {#read-resources-using-the-java-api}

Leia um recurso usando a API de serviço do repositório (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente no caminho de classe do projeto Java.

1. Criar o cliente de serviço

   Criar um `ResourceRepositoryClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Especifique o URI do recurso a ser lido

   Especifique um valor de string que represente o URI do recurso a ser recuperado. Por exemplo, supondo que o recurso seja nomeado como *testResource* que está em uma pasta chamada *testFolder*, especificar `/testFolder/testResource`.

1. Ler o recurso

   Chame o `ResourceRepositoryClient` do objeto `readResource` e transmita o URI do recurso como um parâmetro. Este método retorna um valor de `Resource` instância que representa o recurso.

**Consulte também**

[Recursos de leitura](aem-forms-repository.md#reading-resources)

[Início rápido (modo SOAP): Leitura de um recurso usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Lendo recursos usando a API do serviço Web {#reading-resources-using-the-web-service-api}

Leia um recurso usando a API de serviço do Repositório (serviço Web):

1. Incluir arquivos de projeto

   * Crie um assembly cliente Microsoft .NET que consuma o WSDL do repositório. (Consulte [Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)
   * Referencie o assembly do cliente Microsoft .NET. (Consulte [Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Criar o cliente de serviço

   Usando o assembly cliente Microsoft .NET, crie um `RepositoryServiceService` chamando seu construtor padrão. Defina suas `Credentials` propriedade usando um `System.Net.NetworkCredential` objeto que contém o nome de usuário e a senha.

1. Especifique o URI do recurso a ser lido

   Especifique uma cadeia de caracteres que contenha o URI do recurso a ser recuperado. Nesse caso, como o recurso chamado `testResource` está na pasta chamada `testFolder`, seu URI é `"/testFolder/testResource"`. Ao usar uma linguagem compatível com o Microsoft .NET Framework (por exemplo, C#), armazene o URI em uma `System.String` objeto.

1. Ler o recurso

   Chame o `RepositoryServiceService` do objeto `readResource` e transmita o URI do recurso como o primeiro parâmetro. Aprovado `null` para os outros dois parâmetros.

**Consulte também**

[Recursos de leitura](aem-forms-repository.md#reading-resources)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Atualização de recursos {#updating-resources}

Você pode recuperar e atualizar o conteúdo dos recursos no repositório. Ao atualizar recursos, o controle de acesso a esses recursos permanece inalterado entre as versões. Ao executar uma atualização, você tem a opção de incrementar a versão principal. Se você não optar por incrementar a versão principal, a versão secundária será atualizada automaticamente.

Quando você atualiza um recurso, a nova versão é criada com base nos atributos de recurso especificados. Ao atualizar um recurso, você especifica dois parâmetros importantes: o URI de destino e uma instância de recurso que contém todos os metadados atualizados. É importante observar que, se você não estiver alterando um determinado atributo (por exemplo, o nome ), ele ainda será necessário na instância transmitida. As relações que são criadas ao analisar o conteúdo são adicionadas à versão específica e não são apresentadas a menos que especificado.

Por exemplo, se você atualizar um arquivo XDP e ele contiver referências a outros recursos, essas referências adicionais também serão registradas. Suponha que o form.xdp versão 1.0 tenha duas referências externas: um logotipo e uma folha de estilos, e você atualiza subsequentemente o form.xdp para que ele agora tenha três referências: um logotipo, uma folha de estilos e um arquivo de esquema. Durante a atualização, o repositório adicionará a terceira relação (ao arquivo de esquema) à tabela de relação pendente. Quando o arquivo de esquema estiver presente no repositório, a relação será formada automaticamente. No entanto, se a versão 2.0 do form.xdp não usar mais o logotipo, a versão 2.0 do form.xdp não terá uma relação com o logotipo.

Todas as operações de atualização são atômicas e transacionais. Por exemplo, se dois usuários lerem o mesmo recurso e decidirem atualizar a versão 1.0 para a versão 2.0, um deles terá êxito e um deles falhará, a integridade do repositório será mantida e ambos receberão uma mensagem confirmando o sucesso ou a falha. Se a transação não for submetida a commit, ela será revertida caso haja uma falha no banco de dados e sofrerá timeout ou rollback, dependendo do servidor de aplicativos.

Você pode atualizar recursos de forma programática usando a API Java do serviço de repositório ou a API do serviço da Web.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de repositório, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-4}

Para atualizar um recurso, siga estas etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço de Repositório.
1. Recupere o recurso a ser atualizado.
1. Atualize o recurso.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de ler programaticamente um recurso, é necessário estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Recuperar o recurso a ser atualizado**

Leia o recurso. Para obter mais informações, consulte [Recursos de leitura](aem-forms-repository.md#reading-resources).

**Atualizar o recurso**

Defina as novas informações no recurso e chame o método de serviço de Repositório para atualizar o recurso, especificando o URI, o recurso atualizado e como as informações da versão devem ser atualizadas.

**Consulte também**

[Atualizar recursos usando a API Java](aem-forms-repository.md#update-resources-using-the-java-api)

[Atualizar recursos usando a API de serviço Web](aem-forms-repository.md#update-resources-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Atualizar recursos usando a API Java {#update-resources-using-the-java-api}

Atualize um recurso usando a API de serviço do Repositório (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente no caminho de classe do projeto Java.

1. Criar o cliente de serviço

   Criar um `ResourceRepositoryClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Recuperar o recurso a ser atualizado

   Especifique o URI do recurso para recuperar e ler o recurso. Neste exemplo, o URI do recurso é `"/testFolder/testResource"`.

1. Atualizar o recurso

   Atualize o `Resource` informações do objeto. Neste exemplo, para atualizar a descrição, chame o `Resource` do objeto `setDescription` e transmita a nova string de descrição como um parâmetro.

   Em seguida, chame o `ServiceClientFactory` do objeto `updateResource` e transmita os seguintes parâmetros:

   * A `java.lang.String` objeto que contém o URI do recurso.
   * A variável `Resource` objeto que contém as informações de recurso atualizadas.
   * A `boolean` valor que indica se a versão principal ou secundária deve ser atualizada. Neste exemplo, um valor de `true` é transmitido para indicar que a versão principal deve ser incrementada.

**Consulte também**

[Atualização de recursos](aem-forms-repository.md#updating-resources)

[Início rápido (modo SOAP): atualização de um recurso usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Atualizar recursos usando a API de serviço Web {#update-resources-using-the-web-service-api}

Atualize um recurso usando a API do repositório (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly cliente Microsoft .NET que consuma o WSDL do repositório.
   * Referencie o assembly do cliente Microsoft .NET.

1. Criar o cliente de serviço

   Usando o assembly cliente Microsoft .NET, crie um `RepositoryServiceService` chamando seu construtor padrão. Defina suas `Credentials` propriedade usando um `System.Net.NetworkCredential` objeto que contém o nome de usuário e a senha.

1. Recuperar o recurso a ser atualizado

   Especifique o URI do recurso a ser recuperado e leia o recurso. Neste exemplo, o URI do recurso é `"/testFolder/testResource"`. Para obter mais informações, consulte [Recursos de leitura](aem-forms-repository.md#reading-resources).

1. Atualizar o recurso

   Atualize o `Resource` informações do objeto. Neste exemplo, para atualizar a descrição, atribua um novo valor à variável `Resource` do objeto `description` campo.

1. Chame o `RepositoryServiceService` do objeto `updateResource` e transmita os seguintes parâmetros:

   * A `System.String` objeto que contém o URI do recurso.
   * A variável `Resource` objeto que contém as informações de recurso atualizadas.
   * A `boolean` valor que indica se a versão principal ou secundária deve ser atualizada. Neste exemplo, um valor de `true` é transmitido para indicar que a versão principal deve ser incrementada.
   * Aprovado `null` para os dois parâmetros restantes.

**Consulte também**

[Atualização de recursos](aem-forms-repository.md#updating-resources)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Pesquisando Recursos {#searching-for-resources}

Você pode criar consultas usadas para pesquisar recursos no repositório, incluindo histórico, recursos relacionados e propriedades.

Você pode recuperar recursos relacionados para determinar as dependências entre um formulário e seus fragmentos. Por exemplo, se você tiver um formulário, poderá determinar quais fragmentos ou recursos externos ele usa. Se você tiver uma imagem, também poderá descobrir quais formulários usam a imagem. Também é possível pesquisar recursos relacionados usando a filtragem com base nas propriedades. Por exemplo, você pode pesquisar todos os formulários que usam uma imagem com um nome especificado ou localizar qualquer imagem usada por um formulário com um nome especificado. Também é possível pesquisar usando as propriedades dos recursos. Por exemplo, você pode realizar uma consulta para localizar todos os formulários ou recursos cujo nome comece com uma determinada string que pode incluir os curingas &quot;%&quot; e &quot;_&quot;. Lembre-se de que as pesquisas baseadas em propriedades não são baseadas em relações; essas pesquisas são baseadas na suposição de que você tem conhecimento específico sobre um determinado recurso.

**Instruções de consulta**

A *query* contém uma ou mais instruções logicamente unidas com condições. A *instrução* consiste em um operando à esquerda, um operador e um operando à direita. Além disso, você pode especificar a ordem de classificação a ser usada para os resultados da pesquisa. A variável *ordem de classificação* contém informações equivalentes a um SQL `ORDER BY` e é composto de elementos que contêm os atributos nos quais a pesquisa foi baseada e um valor indicando se a ordem crescente ou decrescente deve ser usada.

Você pode pesquisar recursos de forma programática usando a API Java do serviço de repositório. No momento, não é possível usar a API do serviço Web para pesquisar recursos.

**Comportamento de classificação**

A ordem de classificação não é respeitada ao invocar o `ResourceRepositoryClient` do objeto `searchProperties` e especificar uma ordem de classificação. Por exemplo, suponha que você crie um recurso com três propriedades personalizadas, em que os nomes dos atributos sejam `name`, `secondName`, e `asecondName`. Em seguida, você cria um elemento de ordem de classificação no nome do atributo e define o `ascending` valor para `true`.

Em seguida, chame o `ResourceRepositoryClient` do objeto `searchProperties` e passar na ordem de classificação. A pesquisa retorna o recurso correto, com as três propriedades. No entanto, as propriedades não são classificadas por nome de atributo. Eles são retornados na ordem em que foram adicionados: `name`, `secondName`, e `asecondName`.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de repositório, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-5}

Para pesquisar recursos, siga estas etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço de Repositório.
1. Especifique a pasta de destino da pesquisa.
1. Especifique os atributos usados na pesquisa.
1. Crie a query usada na pesquisa.
1. Criar a ordem de classificação dos resultados da pesquisa.
1. Procure os recursos.
1. Recuperar os recursos do resultado da pesquisa.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de ler programaticamente um recurso, é necessário estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Especificar a pasta de destino da pesquisa**

Crie uma string contendo o caminho base a partir do qual a pesquisa será conduzida. A sintaxe inclui barras, como neste exemplo: &quot;/*caminho*/*pasta*&quot;.

**Especificar os atributos usados na pesquisa**

Você pode basear sua pesquisa nos atributos contidos nos recursos. Especifique os valores dos atributos nos quais a pesquisa será conduzida.

**Criar a consulta usada na pesquisa**

Construir uma consulta usando instruções e condições. Cada instrução especificará o atributo no qual basear a pesquisa, a condição a ser usada e o valor do atributo a ser usado na pesquisa.

**Criar a ordem de classificação dos resultados da pesquisa**

A ordem de classificação é composta por elementos, cada um contendo um dos atributos usados na pesquisa e um valor indicando se a ordem crescente ou decrescente deve ser usada.

**Pesquisar os recursos**

Pesquise os recursos usando a pasta, a consulta e a ordem de classificação. Além disso, indique a profundidade da pesquisa e um limite superior no número de resultados a serem retornados.

**Recuperar os recursos do resultado da pesquisa**

Repita a lista de recursos retornada e extraia as informações para processamento adicional.

**Consulte também**

[Pesquisar recursos usando a API Java](aem-forms-repository.md#search-for-resources-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Pesquisar recursos usando a API Java {#search-for-resources-using-the-java-api}

Procure um recurso usando a API de serviço do Repositório (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente no caminho de classe do projeto Java.

1. Criar o cliente de serviço

   Criar um `ResourceRepositoryClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Especificar a pasta de destino da pesquisa

   Especifique o URI do caminho base a partir do qual a pesquisa será executada. Neste exemplo, o URI do recurso é `/testFolder`.

1. Especificar os atributos usados na pesquisa

   Especifique os valores dos atributos nos quais a pesquisa será conduzida. Os atributos existem em um `com.adobe.repository.infomodel.bean.Resource` objeto. Neste exemplo, a pesquisa será conduzida no atributo name; portanto, um `java.lang.String` contendo o `Resource` o nome do objeto é usado, que é `testResource` neste caso.

1. Criar a consulta usada na pesquisa

   Para criar um query, crie um `com.adobe.repository.query.Query` chamando o construtor padrão para o `Query` e adicionar instruções à consulta.

   Para criar uma instrução, chame o construtor para o `com.adobe.repository.query.Query.Statement` e transmitem os seguintes parâmetros:

   * Um operando esquerdo que contém a constante de atributo de recurso. Neste exemplo, como o nome do recurso é usado como a base para a pesquisa, o valor estático `Resource.ATTRIBUTE_NAME` é usada.
   * Um operador que contém a condição usada na pesquisa pelo atributo. O operador deve ser uma das constantes estáticas no `Query.Statement` classe. Neste exemplo, o valor estático `Query.Statement.OPERATOR_BEGINS_WITH` é usada.
   * Um operando direito que contém o valor do atributo no qual a pesquisa será conduzida. Neste exemplo, o atributo name, a `String` contendo o valor `"testResource"`, é usada.

   Especifique o namespace do operando esquerdo chamando o `Query.Statement` do objeto `setNamespace` e transmitindo um dos valores estáticos contidos na variável `com.adobe.repository.infomodel.bean.ResourceProperty` classe. Neste exemplo, `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY` é usada.

   Adicione cada instrução à consulta invocando o `Query` do objeto `addStatement` e transmitindo o `Query.Statement` objeto.

1. Criar a ordem de classificação dos resultados da pesquisa

   Para especificar a ordem de classificação usada nos resultados da pesquisa, crie uma `com.adobe.repository.query.sort.SortOrder` chamando o construtor padrão para o `SortOrder` e adicionar elementos à ordem de classificação.

   Para criar um elemento para a ordem de classificação, chame um dos construtores para o `com.adobe.repository.query.sort.SortOrder.Element` classe. Neste exemplo, como o nome do recurso é usado como a base para a pesquisa, o valor estático `Resource.ATTRIBUTE_NAME` é usado como o primeiro parâmetro e a ordem crescente (uma variável `boolean` valor de `true`) é especificado como o segundo parâmetro.

   Adicione cada elemento à ordem de classificação chamando o `SortOrder` do objeto `addSortElement` e transmitindo o `SortOrder.Element` objeto.

1. Pesquisar os recursos

   Para pesquisar por `resources` com base nas propriedades do atributo, chame o `ResourceRepositoryClient` do objeto `searchProperties` e transmita os seguintes parâmetros:

   * A `String` contendo o caminho base a partir do qual a pesquisa será executada. Nesse caso, `"/testFolder"` é usada.
   * A consulta usada na pesquisa.
   * A profundidade da pesquisa. Nesse caso, `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` é usado para indicar que o caminho base e todas as suas pastas devem ser usados.
   * Um `int` valor que indica a primeira linha a partir da qual o conjunto de resultados não paginado será selecionado. Neste exemplo, `0` é especificado.
   * Um `int` valor que indica o número máximo de resultados a serem retornados. Neste exemplo, `10` é especificado.
   * A ordem de classificação usada na pesquisa.

   O método retorna um valor de `java.util.List` de `Resource` objetos na ordem de classificação especificada.

1. Recuperar os recursos do resultado da pesquisa

   Para recuperar os recursos contidos no resultado da pesquisa, repita através da `List` e converta cada objeto em um `Resource` para extrair suas informações. Neste exemplo, o nome de cada recurso é exibido.

**Consulte também**

[Pesquisando Recursos](aem-forms-repository.md#searching-for-resources)

[Início rápido (modo SOAP): procurando recursos usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Criando Relações de Recursos {#creating-resource-relationships}

Você pode especificar relações entre os recursos no repositório. Há três tipos de relações:

* **Dependência**: uma relação na qual um recurso depende de outros recursos, o que significa que todos os recursos relacionados são necessários no repositório.
* **Associação (sistema de arquivos)**: uma relação na qual um recurso está localizado em uma determinada pasta.
* **Personalizado**: uma relação especificada entre recursos. Por exemplo, se um recurso tiver sido descontinuado e outro recurso introduzido no repositório, você poderá especificar sua própria relação de substituição.

Você pode criar seus próprios relacionamentos personalizados. Por exemplo, se você armazenar um arquivo de HTML no repositório e ele usar uma imagem, você poderá especificar uma relação personalizada para relacionar o arquivo de HTML com a imagem (já que normalmente somente arquivos XML são associados a imagens usando uma relação de dependência definida pelo repositório). Outro exemplo de relacionamento personalizado seria se você quisesse criar uma visualização diferente do repositório com uma estrutura de gráfico cíclica em vez de uma estrutura em árvore. Você pode definir um gráfico circular junto com um visualizador para percorrer esses relacionamentos. Por fim, você pode indicar que um recurso substitui outro mesmo que os dois recursos sejam completamente diferentes. Nesse caso, você poderia definir um tipo de relacionamento fora do intervalo reservado e criar um relacionamento entre esses dois recursos. Seu aplicativo seria o único cliente que poderia detectar e processar a relação, e poderia ser usado para realizar pesquisas nessa relação.

Você pode especificar relações programaticamente entre recursos usando a API Java do serviço de repositório ou a API do serviço da Web.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de repositório, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-6}

Para especificar uma relação entre dois recursos, siga estas etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço de Repositório.
1. Especifique os URIs dos recursos que serão relacionados.
1. Crie o relacionamento.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de ler programaticamente um recurso, é necessário estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Especifique os URIs dos recursos que serão relacionados**

Crie cadeias de caracteres que contenham os URIs do recurso a ser relacionado. A sintaxe inclui barras, como neste exemplo: &quot;/*caminho*/*recurso*&quot;.

**Criar o relacionamento**

Chame o método de serviço do Repositório para criar e especificar o tipo de relacionamento.

**Consulte também**

[Criar recursos de relacionamento usando a API Java](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[Criar recursos de relacionamento usando a API de serviço Web](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Criar recursos de relacionamento usando a API Java {#create-relationship-resources-using-the-java-api}

Para criar recursos de relacionamento usando a API Java do serviço de Repositório, execute as seguintes tarefas:

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente no caminho de classe do projeto Java.

1. Criar o cliente de serviço

   Criar um `ResourceRepositoryClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Especifique os URIs dos recursos que serão relacionados

   Especifique os URIs dos recursos que serão relacionados. Nesse caso, porque os recursos são nomeados como `testResource1` e `testResource2` e estão na pasta chamada `testFolder`, seus URIs são `"/testFolder/testResource1"` e `"/testFolder/testResource2"`. Os URIs são armazenados como um `java.lang.String` objetos. Neste exemplo, os recursos são gravados pela primeira vez no repositório e seus URIs são recuperados. Para obter mais informações sobre como gravar um recurso, consulte [Recursos de gravação](aem-forms-repository.md#writing-resources).

1. Criar o relacionamento

   Chame o `ResourceRepositoryClient` do objeto `createRelationship` e transmita os seguintes parâmetros:

   * O URI do recurso de origem.
   * O URI do recurso de destino.
   * O tipo de relação, que é uma das constantes estáticas no `com.adobe.repository.infomodel.bean.Relation` classe. Neste exemplo, uma relação de dependência é estabelecida especificando o valor `Relation.TYPE_DEPENDANT_OF`.
   * A `boolean` valor que indica se o recurso de destino é atualizado automaticamente para o `com.adobe.repository.infomodel.Id`identificador baseado em do novo recurso head. Neste exemplo, por causa da relação de dependência, o valor `true` é especificado.

   Você também pode recuperar uma lista de recursos relacionados para um determinado recurso chamando o `ResourceRepositoryClient` do objeto `getRelated` e transmitindo os seguintes parâmetros:

   * O URI do recurso para o qual recuperar recursos relacionados. Neste exemplo, o recurso de origem ( `"/testFolder/testResource1"`) é especificado.
   * A `boolean` valor que indica se o recurso especificado é o recurso de origem na relação. Neste exemplo, o valor `true` é especificado porque esse é o caso.
   * O tipo de relacionamento, que é uma das constantes estáticas no `Relation` classe. Neste exemplo, uma relação de dependência é especificada usando o mesmo valor usado anteriormente: `Relation.TYPE_DEPENDANT_OF`.

   A variável `getRelated` o método retorna um `java.util.List` de `Resource` objetos por meio dos quais você pode iterar para recuperar cada um dos recursos relacionados, convertendo os objetos contidos na variável `List` para `Resource` como você faz. Neste exemplo, `testResource2` deve estar na lista de recursos retornados.

**Consulte também**

[Criando Relações de Recursos](aem-forms-repository.md#creating-resource-relationships)

[Início rápido (modo SOAP): criação de relacionamentos entre recursos usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Criar recursos de relacionamento usando a API de serviço Web {#create-relationship-resources-using-the-web-service-api}

Crie recursos de relacionamento usando a API do repositório (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly cliente Microsoft .NET que consuma o WSDL do repositório.
   * Referencie o assembly do cliente Microsoft .NET.

1. Criar o cliente de serviço

   Usando o assembly cliente Microsoft .NET, crie um `RepositoryServiceService` chamando seu construtor padrão. Defina suas `Credentials` propriedade usando um `System.Net.NetworkCredential` objeto que contém o nome de usuário e a senha.

1. Especifique os URIs dos recursos que serão relacionados

   Especifique os URIs dos recursos que serão relacionados. Nesse caso, porque os recursos são nomeados como `testResource1` e `testResource2` e estão na pasta chamada `testFolder`, seus URIs são `"/testFolder/testResource1"` e `"/testFolder/testResource2"`. Ao usar uma linguagem compatível com o Microsoft .NET Framework (por exemplo, C#), os URIs são armazenados como um `System.String` objetos. Neste exemplo, os recursos são gravados pela primeira vez no repositório e seus URIs são recuperados. Para obter mais informações sobre como gravar um recurso, consulte [Recursos de gravação](aem-forms-repository.md#writing-resources).

1. Criar o relacionamento

   Chame o `RepositoryServiceService` do objeto `createRelationship` e transmita os seguintes parâmetros:

   * O URI do recurso de origem.
   * O URI do recurso de destino.
   * O tipo de relacionamento. Neste exemplo, uma relação de dependência é estabelecida especificando o valor `3`.
   * A `boolean` valor que indica se o tipo de relacionamento foi especificado. Neste exemplo, o valor `true` é especificado.
   * A `boolean` valor que indica se o recurso de destino é atualizado automaticamente para o `Id`identificador baseado em do novo recurso head. Neste exemplo, por causa da relação de dependência, o valor `true` é especificado.
   * A `boolean` valor que indica se o cabeçalho de destino foi especificado. Neste exemplo, o valor `true` é especificado.
   * Aprovado `null` para o último parâmetro.

   Você também pode recuperar uma lista de recursos relacionados para um determinado recurso chamando o `RepositoryServiceService` do objeto `getRelated` e transmitindo os seguintes parâmetros:

   * O URI do recurso para o qual recuperar recursos relacionados. Neste exemplo, o recurso de origem ( `"/testFolder/testResource1"`) é especificado.
   * A `boolean` valor que indica se o recurso especificado é o recurso de origem na relação. Neste exemplo, o valor `true` é especificado porque esse é o caso.
   * A `boolean` valor que indica se o recurso de origem foi especificado. Neste exemplo, o valor `true` é fornecido.
   * Uma matriz de inteiros que contém os tipos de relacionamento. Neste exemplo, uma relação de dependência é especificada usando o mesmo valor na matriz que foi usado anteriormente: `3`.
   * Aprovado `null` para os dois parâmetros restantes.

   A variável `getRelated` método retorna uma matriz de objetos que podem ser convertidos em `Resource` objetos por meio dos quais você pode iterar para recuperar cada um dos recursos relacionados. Neste exemplo, `testResource2` deve estar na lista de recursos retornados.

**Consulte também**

[Criando Relações de Recursos](aem-forms-repository.md#creating-resource-relationships)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Bloquear recursos {#locking-resources}

É possível bloquear um recurso ou conjunto de recursos para uso exclusivo por um usuário específico ou para uso compartilhado entre mais de um usuário. Um bloqueio compartilhado é uma indicação de que algo acontecerá com o recurso, mas não impede que outra pessoa execute ações com esse recurso. Um bloqueio compartilhado deve ser considerado um mecanismo de sinalização. Um bloqueio exclusivo significa que o usuário que bloqueou o recurso vai alterar o recurso, e o bloqueio garante que ninguém mais possa fazer isso até que o usuário não precise mais de acesso ao recurso e tenha liberado o bloqueio. Se um administrador do repositório desbloquear um recurso, todos os bloqueios exclusivos e compartilhados nesse recurso serão removidos automaticamente. Esse tipo de ação se destina a situações em que um usuário não está mais disponível e não desbloqueou o recurso.

Quando um recurso é bloqueado, um ícone de bloqueio é exibido quando você exibe a guia Recursos na Bancada, conforme mostrado na ilustração a seguir.

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

Você pode controlar programaticamente o acesso aos recursos usando a API Java do serviço de repositório ou a API do serviço da Web.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de repositório, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-7}

Para bloquear e desbloquear recursos, siga estas etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço de Repositório.
1. Especifique o URI do recurso a ser bloqueado.
1. Bloquear o recurso.
1. Recupere os bloqueios do recurso.
1. Desbloquear o recurso

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de ler programaticamente um recurso, é necessário estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Especifique o URI do recurso a ser bloqueado**

Crie uma cadeia de caracteres que contenha o URI do recurso a ser bloqueado. A sintaxe inclui barras, como neste exemplo: &quot;/*caminho*/*recurso*&quot;.

**Bloquear o recurso**

Chame o método do serviço do Repositório para bloquear o recurso, especificando o URI, o tipo de bloqueio e a profundidade do bloqueio.

**Recuperar os bloqueios do recurso**

Chame o método do Serviço de repositório para recuperar os bloqueios do recurso, especificando o URI.

**Desbloquear o recurso**

Chame o método do Serviço de repositório para desbloquear o recurso, especificando o URI.

**Consulte também**

[Bloquear recursos usando a API Java](aem-forms-repository.md#lock-resources-using-the-java-api)

[Bloquear recursos usando a API de serviço Web](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Bloquear recursos usando a API Java {#lock-resources-using-the-java-api}

Bloqueie recursos usando a API de serviço do repositório (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente no caminho de classe do projeto Java.

1. Criar o cliente de serviço

   Criar um `ResourceRepositoryClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Especifique o URI do recurso a ser bloqueado

   Especifique o URI do recurso a ser bloqueado. Nesse caso, como o recurso chamado `testResource` está na pasta chamada `testFolder`, seu URI é `"/testFolder/testResource"`. O URI é armazenado como um `java.lang.String` objeto.

1. Bloquear o recurso

   Chame o `ResourceRepositoryClient` do objeto `lockResource` e transmita os seguintes parâmetros:

   * O URI do recurso.
   * O escopo de bloqueio. Neste exemplo, como o recurso será bloqueado para uso exclusivo, o escopo de bloqueio é especificado como `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`.
   * A profundidade da trava. Neste exemplo, como o bloqueio será aplicado somente ao recurso específico e a nenhum de seus membros ou filhos, a profundidade do bloqueio é especificada como `Lock.DEPTH_ZERO`.

   >[!NOTE]
   >
   >A versão sobrecarregada do `lockResource` que requer quatro parâmetros aciona uma exceção. Certifique-se de usar o `lockResource` que requer três parâmetros, conforme mostrado nesta apresentação.

1. Recuperar os bloqueios do recurso

   Chame o `ResourceRepositoryClient` do objeto `getLocks` e transmita o URI do recurso como um parâmetro. O método retorna uma Lista de objetos Lock pela qual você pode iterar. Neste exemplo, o proprietário, a profundidade e o escopo do bloqueio são impressos para cada objeto, chamando cada propriedade do objeto Lock `getOwnerUserId`, `getDepth`, e `getType` métodos, respectivamente.

1. Desbloquear o recurso

   Chame o `ResourceRepositoryClient` do objeto `unlockResource` e transmita o URI do recurso como um parâmetro. Para obter mais informações, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Consulte também**

[Bloquear recursos](aem-forms-repository.md#locking-resources)

[Início rápido (modo SOAP): bloqueio de um recurso usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Bloquear recursos usando a API de serviço Web {#lock-resources-using-the-web-service-api}

Bloqueie recursos usando a API de serviço do Repositório (serviço Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o WSDL do Repositório usando Base64.
   * Referencie o assembly do cliente Microsoft .NET.

1. Criar o cliente de serviço

   Usando o assembly cliente Microsoft .NET, crie um `RepositoryServiceService` chamando seu construtor padrão. Defina suas `Credentials` propriedade usando um `System.Net.NetworkCredential` objeto que contém o nome de usuário e a senha.

1. Especifique o URI do recurso a ser bloqueado

   Especifique uma cadeia de caracteres que contenha o URI do recurso a ser bloqueado. Nesse caso, como o recurso chamado `testResource` está na pasta `testFolder`, seu URI é `"/testFolder/testResource"`. Ao usar uma linguagem compatível com o Microsoft .NET Framework (por exemplo, C#), armazene o URI em uma `System.String` objeto.

1. Bloquear o recurso

   Chame o `RepositoryServiceService` do objeto `lockResource` e transmita os seguintes parâmetros:

   * O URI do recurso.
   * O escopo de bloqueio. Neste exemplo, como o recurso será bloqueado para uso exclusivo, o escopo de bloqueio é especificado como `11`.
   * A profundidade da trava. Neste exemplo, como o bloqueio será aplicado somente ao recurso específico e a nenhum de seus membros ou filhos, a profundidade do bloqueio é especificada como `2`.
   * Um `int` valor que indica o número de segundos até o bloqueio expirar. Neste exemplo, o valor de `1000` é usada.
   * Aprovado `null` para o último parâmetro.

1. Recuperar os bloqueios do recurso

   Chame o `RepositoryServiceService` do objeto `getLocks` e transmita o URI do recurso como o primeiro parâmetro e `null` para o segundo parâmetro. O método retorna um valor de `object` matriz que contém `Lock` objetos pelos quais você pode iterar. Neste exemplo, o proprietário, a profundidade e o escopo do bloqueio são impressos para cada objeto acessando cada `Lock` do objeto `ownerUserId`, `depth`, e `type` campos, respectivamente.

1. Desbloquear o recurso

   Chame o `RepositoryServiceService` do objeto `unlockResource` e transmita o URI do recurso como o primeiro parâmetro e `null` para o segundo parâmetro.

**Consulte também**

[Bloquear recursos](aem-forms-repository.md#locking-resources)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Exclusão de recursos {#deleting-resources}

Você pode excluir recursos de forma programática de um determinado local no repositório usando a API Java (SOAP) do serviço do Repositório.

Quando você exclui um recurso, a exclusão normalmente é permanente, embora, em alguns casos, os repositórios ECM possam armazenar as versões do recurso de acordo com seus mecanismos de histórico. Portanto, ao excluir um recurso, é importante ter certeza de que você nunca precisará dele novamente. Os motivos comuns para excluir um recurso incluem a necessidade de aumentar o espaço disponível no banco de dados. Você pode excluir uma versão de um recurso, mas, se fizer isso, deverá especificar o identificador de recurso, e não seu LID (identificador lógico) ou caminho. Se você excluir uma pasta, tudo nessa pasta, incluindo subpastas e recursos, será excluído automaticamente.

Os recursos relacionados não são excluídos. Por exemplo, se você tiver um formulário que use o arquivo logo.gif e excluir logo.gif, um relacionamento será armazenado na tabela de relacionamento pendente. Como alternativa, para descontinuação de versão, defina o status do objeto da versão mais recente como descontinuado.

Uma operação de exclusão não é segura para transações em sistemas ECM. Por exemplo, se você tentar excluir 100 recursos e a operação falhar no 50º recurso, as primeiras 49 instâncias serão excluídas, mas o restante não. Caso contrário, o comportamento padrão será a reversão (não compromisso).

>[!NOTE]
>
>Ao usar o `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` com o repositório ECM (EMC Documentum Content Server e IBM FileNet P8 Content Manager), a transação não será revertida se a exclusão falhar para um dos recursos especificados, o que significa que os arquivos que foram excluídos não poderão ter sua exclusão cancelada.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de repositório, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-8}

Para excluir um recurso, siga estas etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço de Repositório.
1. Especifique o URI do recurso a ser excluído.
1. Exclua o recurso.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar o cliente de serviço**

Antes de ler programaticamente um recurso, é necessário estabelecer uma conexão e fornecer credenciais. Isso é feito criando um cliente de serviço.

**Especifique o URI do recurso a ser excluído**

Crie uma cadeia de caracteres que contenha o URI do recurso a ser excluído. A sintaxe inclui barras, como neste exemplo: &quot;/*caminho*/*recurso*&quot;. Se o recurso a ser excluído for uma pasta, a exclusão será recursiva.

**Excluir o recurso**

Chame o método do serviço de Repositório para excluir o recurso, especificando o URI.

**Consulte também**

[Excluir recursos usando a API Java](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[Excluir recursos usando a API de serviço Web](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Repositório](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Excluir recursos usando a API do Java (SOAP) {#delete-resources-using-the-java-api-soap}

Exclua um recurso usando a API do repositório (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente no caminho de classe do projeto Java.

1. Criar o cliente de serviço

   Criar um `ResourceRepositoryClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Especifique o URI do recurso a ser excluído

   Especifique o URI do recurso a ser recuperado. Nesse caso, como o recurso chamado testResourceToBeDeleted está na pasta chamada testFolder, seu URI é `/testFolder/testResourceToBeDeleted`. O URI é armazenado como um `java.lang.String` objeto. Neste exemplo, o recurso é gravado primeiro no repositório e seu URI é recuperado. Para obter mais informações sobre como gravar um recurso, consulte [Recursos de gravação](aem-forms-repository.md#writing-resources).

1. Excluir o recurso

   Chame o `ResourceRepositoryClient` do objeto `deleteResource` e transmita o URI do recurso como um parâmetro.

**Consulte também**

[Exclusão de recursos](aem-forms-repository.md#deleting-resources)

[Início rápido (modo SOAP): procurando recursos usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Excluir recursos usando a API de serviço Web {#delete-resources-using-the-web-service-api}

Exclua um recurso usando a API do repositório (serviço Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o WSDL do Repositório usando Base64.
   * Referencie o assembly do cliente Microsoft .NET.

1. Criar o cliente de serviço

   Usando o assembly cliente Microsoft .NET, crie um `RepositoryServiceService` chamando seu construtor padrão. Defina suas `Credentials` propriedade usando um `System.Net.NetworkCredential` objeto que contém o nome de usuário e a senha.

1. Especifique o URI do recurso a ser excluído

   Especifique o URI do recurso a ser recuperado. Nesse caso, como o recurso chamado `testResourceToBeDeleted` está na pasta chamada `testFolder`, seu URI é `"/testFolder/testResourceToBeDeleted"`. Neste exemplo, o recurso é gravado primeiro no repositório e seu URI é recuperado. Para obter mais informações sobre como gravar um recurso, consulte [Recursos de gravação](aem-forms-repository.md#writing-resources).

1. Excluir o recurso

   Chame o `RepositoryServiceService` do objeto `deleteResources` e transmita um `System.String` matriz que contém o URI do recurso como o primeiro parâmetro. Aprovado `null` para o segundo parâmetro.

**Consulte também**

[Exclusão de recursos](aem-forms-repository.md#deleting-resources)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
