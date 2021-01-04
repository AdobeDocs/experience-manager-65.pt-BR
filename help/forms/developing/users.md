---
title: Gerenciamento de usuários
seo-title: Gerenciamento de usuários
description: Use a API Gerenciamento de usuários para criar aplicativos clientes que possam gerenciar funções, permissões e principais (que podem ser usuários ou grupos), bem como autenticar usuários.
seo-description: Use a API Gerenciamento de usuários para criar aplicativos clientes que possam gerenciar funções, permissões e principais (que podem ser usuários ou grupos), bem como autenticar usuários.
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '6243'
ht-degree: 0%

---


# Gerenciando usuários {#managing-users}

**Sobre o Gerenciamento de usuários**

Você pode usar a API Gerenciamento de usuários para criar aplicativos clientes que podem gerenciar funções, permissões e principais (que podem ser usuários ou grupos), bem como autenticar usuários. A API de gerenciamento de usuários consiste nas seguintes APIs da AEM Forms:

* API de serviço do Gerenciador de diretórios
* API de serviço do Authentication Manager
* API de Serviço do Gerenciador de Autorização

O Gerenciamento de usuários permite que você atribua, remova e determine funções e permissões. Ela também permite que você atribua, remova e query domínios, usuários e grupos. Por fim, você pode usar o Gerenciamento de usuários para autenticar usuários.

Em [Adicionar usuários](users.md#adding-users) você entenderá como adicionar usuários de forma programática. Esta seção usa a API de serviço do Gerenciador de Diretórios.

Em [Excluindo usuários](users.md#deleting-users) você entenderá como excluir usuários de forma programática. Esta seção usa a API de serviço do Gerenciador de Diretórios.

Em [Gerenciar usuários e grupos](users.md#managing-users-and-groups) você entenderá a diferença entre um usuário local e um usuário do diretório e verá exemplos de como usar as APIs de Java e de serviço da Web para gerenciar de forma programática usuários e grupos. Esta seção usa a API de serviço do Gerenciador de Diretórios.

Em [Gerenciando funções e permissões](users.md#managing-roles-and-permissions) você aprenderá sobre as funções e permissões do sistema e o que pode fazer de forma programática para aumentá-las, e verá exemplos de como usar as APIs Java e de serviço da Web para gerenciar programaticamente funções e permissões. Esta seção usa a API de serviço do Gerenciador de Diretórios e a API de serviço do Gerenciador de Autorização.

Em [Autenticando usuários](users.md#authenticating-users) você verá exemplos de como usar as APIs Java e de serviço da Web para autenticar usuários de forma programática. Esta seção usa a API de serviço do Gerenciador de autorização.

**Compreensão do processo de autenticação**

O Gerenciamento de usuários fornece funcionalidade de autenticação integrada e também a capacidade de conectá-la ao seu próprio provedor de autenticação. Quando o Gerenciamento de usuários recebe uma solicitação de autenticação (por exemplo, um usuário tenta fazer logon), ele transmite as informações do usuário ao provedor de autenticação para autenticação. O Gerenciamento de usuários recebe os resultados do provedor de autenticação depois de autenticar o usuário.

O diagrama a seguir mostra a interação entre um usuário final tentando fazer logon, o Gerenciamento de usuários e o provedor de autenticação.

![mu_mu_umauth_process](assets/mu_mu_umauth_process.png)

A tabela a seguir descreve cada etapa do processo de autenticação.

<table>
 <thead>
  <tr>
   <th><p>Etapa</p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Um usuário tenta fazer logon em um serviço que chama Gerenciamento de usuários. O usuário especifica um nome de usuário e senha. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>O Gerenciamento de usuários envia o nome de usuário e a senha, bem como as informações de configuração, para o provedor de autenticação.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>O provedor de autenticação se conecta ao repositório de usuários e autentica o usuário.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>O provedor de autenticação retorna os resultados ao Gerenciamento de usuários.</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>O Gerenciamento de usuários permite que o usuário faça logon ou nega acesso ao produto.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Se o fuso horário do servidor for diferente do fuso horário do cliente, ao consumir o WSDL para o serviço AEM Forms Generate PDF em uma pilha SOAP nativa usando um cliente .NET em um cluster WebSphere Application Server, poderá ocorrer o seguinte erro de autenticação de Gerenciamento de Usuário:

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**Compreensão do gerenciamento de diretório**

O Gerenciamento de usuários é empacotado com um provedor de serviço de diretório (o DiretoryManagerService) que suporta conexões com diretórios LDAP. Se sua organização usar um repositório não LDAP para armazenar registros de usuários, você poderá criar seu próprio provedor de serviço de diretório que funcione com seu repositório.

Os provedores de serviço de diretório recuperam registros de um repositório de usuários a pedido do Gerenciamento de usuários. O Gerenciamento de usuários armazena em cache regularmente os registros de usuários e grupos no banco de dados para melhorar o desempenho.

O provedor de serviço de diretório pode ser usado para sincronizar o banco de dados Gerenciamento de usuários com o repositório de usuários. Esta etapa garante que todas as informações do diretório de usuário e todos os registros de usuário e grupo estejam atualizados.

Além disso, o DiretoryManagerService fornece a você a capacidade de criar e gerenciar domínios. Domínios definem bases de usuários diferentes. O limite de um domínio é geralmente definido de acordo com a forma como sua organização está estruturada ou como sua loja de usuários está configurada. Os domínios de Gerenciamento de usuários fornecem configurações que os provedores de autenticação e os provedores de serviço de diretório usam.

No XML de configuração que o Gerenciamento de usuários exporta, o nó raiz que tem o valor de atributo `Domains` contém um elemento XML para cada domínio definido para o Gerenciamento de usuários. Cada um desses elementos contém outros elementos que definem aspectos do domínio associados a provedores de serviço específicos.

**Noções básicas sobre valores objectSID**

Ao usar o Ative Diretory, é importante entender que um valor `objectSID` não é um atributo exclusivo em vários domínios. Esse valor armazena o identificador de segurança de um objeto. Em um ambiente de domínio múltiplo (por exemplo, uma árvore de domínios), o valor `objectSID` pode ser diferente.

Um valor `objectSID` seria alterado se um objeto fosse movido de um domínio do Ative Diretory para outro domínio. Alguns objetos têm o mesmo valor `objectSID` em qualquer lugar do domínio. Por exemplo, grupos como BUILTIN\Administrators, BUILTIN\Power Users e assim por diante teriam o mesmo valor `objectSID` independentemente dos domínios. Esses valores `objectSID` são bem conhecidos.

## Adicionando usuários {#adding-users}

Você pode usar a API de serviço do Gerenciador de diretórios (Java e serviço da Web) para adicionar usuários programaticamente à AEM Forms. Depois de adicionar um usuário, você pode usá-lo ao executar uma operação de serviço que exija um usuário. Por exemplo, você pode atribuir uma tarefa ao novo usuário.

### Resumo das etapas {#summary-of-steps}

Para adicionar um usuário, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente DiretoryManagerService.
1. Defina as informações do usuário.
1. Adicione o usuário ao AEM Forms.
1. Verifique se o usuário foi adicionado.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar um cliente DiretoryManagerService**

Antes de executar programaticamente uma operação de serviço do Gerenciador de Diretórios, crie um cliente da API de serviço do Gerenciador de Diretórios.

**Definir informações do usuário**

Ao adicionar um novo usuário usando a API de serviço do Gerenciador de Diretórios, defina as informações para esse usuário. Geralmente, ao adicionar um novo usuário, você define os seguintes valores:

* **Nome** do domínio: O domínio ao qual o usuário pertence (por exemplo,  `DefaultDom`).
* **Valor** do identificador do usuário: O valor identificador do usuário (por exemplo,  `wblue`).
* **Tipo** principal: O tipo de usuário (por exemplo, você pode especificar  `USER)`.
* **Nome**: Um determinado nome para o usuário (por exemplo,  `Wendy`).
* **Nome** da família: O nome da família do usuário (por exemplo,  `Blue)`.
* **Local**: Informações de localidade para o usuário.

**Adicionar o usuário ao AEM Forms**

Depois de definir as informações do usuário, é possível adicioná-lo à AEM Forms. Para adicionar um usuário, chame o método `DirectoryManagerServiceClient` do objeto `createLocalUser`.

**Verificar se o usuário foi adicionado**

Você pode verificar se o usuário foi adicionado para garantir que nenhum problema ocorreu. Localize o novo usuário usando o valor do identificador do usuário.

**Consulte também:**

[Adicionar usuários usando a API Java](users.md#add-users-using-the-java-api)

[Adicionar usuários usando a API de serviço da Web](users.md#add-users-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Excluindo usuários](users.md#deleting-users)

### Adicionar usuários usando a API Java {#add-users-using-the-java-api}

Adicione usuários usando a API de serviço do Diretory Manager (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-usermanager-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente DiretoryManagerServices.

   Crie um objeto `DirectoryManagerServiceClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Defina as informações do usuário.

   * Crie um objeto `UserImpl` usando seu construtor.
   * Defina o nome da demanda chamando o método `UserImpl` do objeto `setDomainName`. Passe um valor de string que especifica o nome do domínio.
   * Defina o tipo principal chamando o método `UserImpl` do objeto `setPrincipalType`. Passe um valor de string que especifica o tipo de usuário. Por exemplo, você pode especificar `USER`.
   * Defina o valor do identificador do usuário chamando o método `UserImpl` do objeto `setUserid`. Passe um valor de string que especifica o valor do identificador do usuário. Por exemplo, você pode especificar `wblue`.
   * Defina o nome canônico chamando o método `UserImpl` do objeto `setCanonicalName`. Passe um valor de string que especifica o nome canônico do usuário. Por exemplo, você pode especificar `wblue`.
   * Defina o nome fornecido chamando o método `UserImpl` do objeto `setGivenName`. Passe um valor de string que especifica o nome do usuário. Por exemplo, você pode especificar `Wendy`.
   * Defina o nome da família chamando o método `UserImpl` do objeto `setFamilyName`. Passe um valor de string que especifica o nome da família do usuário. Por exemplo, você pode especificar `Blue`.

   >[!NOTE]
   >
   >Chame um método que pertence ao objeto `UserImpl` para definir outros valores. Por exemplo, você pode definir o valor de localidade chamando o método `UserImpl` do objeto `setLocale`.

1. Adicione o usuário ao AEM Forms.

   Chame o método `DirectoryManagerServiceClient` do objeto `createLocalUser` e passe os seguintes valores:

   * O objeto `UserImpl` que representa o novo usuário
   * Um valor de string que representa a senha do usuário

   O método `createLocalUser` retorna um valor de cadeia de caracteres que especifica o valor do identificador de usuário local.

1. Verifique se o usuário foi adicionado.

   * Crie um objeto `PrincipalSearchFilter` usando seu construtor.
   * Defina o valor do identificador do usuário chamando o método `PrincipalSearchFilter` do objeto `setUserId`. Passe um valor de string que representa o valor do identificador do usuário.
   * Chame o método `DirectoryManagerServiceClient` do objeto `findPrincipals` e passe o objeto `PrincipalSearchFilter`. Este método retorna uma instância `java.util.List`, onde cada elemento é um objeto `User`. Insira a instância `java.util.List` para localizar o usuário.

**Consulte também:**

[Resumo das etapas](users.md#summary-of-steps)

[Start rápido (modo SOAP): Adicionar usuários usando a API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicionar usuários usando a API de serviço da Web {#add-users-using-the-web-service-api}

Adicione usuários usando a API de serviço do Diretory Manager (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL para a referência de serviço: `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente DiretoryManagerService.

   * Crie um objeto `DirectoryManagerServiceClient` usando seu construtor padrão.
   * Crie um objeto `DirectoryManagerServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). Não é necessário usar o atributo `lc_version`. Esse atributo é usado ao criar uma referência de serviço. Certifique-se de especificar `?blob=mtom`.
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `DirectoryManagerServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Defina as informações do usuário.

   * Crie um objeto `UserImpl` usando seu construtor.
   * Defina o nome da demanda atribuindo um valor de string ao campo `UserImpl` `domainName` do objeto.
   * Defina o tipo principal atribuindo um valor de string ao campo `UserImpl` `principalType` do objeto. Por exemplo, você pode especificar `USER`.
   * Defina o valor do identificador do usuário atribuindo um valor de string ao campo `UserImpl` `userid` do objeto.
   * Defina o valor do nome canônico atribuindo um valor de string ao campo `UserImpl` `canonicalName` do objeto.
   * Defina o valor do nome fornecido atribuindo um valor de string ao campo `UserImpl` `givenName` do objeto.
   * Defina o valor do nome da família atribuindo um valor de string ao campo `UserImpl` `familyName` do objeto.

1. Adicione o usuário ao AEM Forms.

   Chame o método `DirectoryManagerServiceClient` do objeto `createLocalUser` e passe os seguintes valores:

   * O objeto `UserImpl` que representa o novo usuário
   * Um valor de string que representa a senha do usuário

   O método `createLocalUser` retorna um valor de cadeia de caracteres que especifica o valor do identificador de usuário local.

1. Verifique se o usuário foi adicionado.

   * Crie um objeto `PrincipalSearchFilter` usando seu construtor.
   * Defina o valor do identificador do usuário atribuindo um valor de string que representa o valor do identificador do usuário ao campo `PrincipalSearchFilter` `userId` do objeto.
   * Chame o método `DirectoryManagerServiceClient` do objeto `findPrincipals` e passe o objeto `PrincipalSearchFilter`. Este método retorna um objeto de coleção `MyArrayOfUser`, em que cada elemento é um objeto `User`. Insira a coleção `MyArrayOfUser` para localizar o usuário.

**Consulte também:**

[Resumo das etapas](users.md#summary-of-steps)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Excluindo usuários {#deleting-users}

Você pode usar a API de serviço do Gerenciador de Diretórios (Java e serviço da Web) para excluir usuários da AEM Forms de forma programática. Após excluir um usuário, ele não poderá mais ser usado para executar uma operação de serviço que exija um usuário. Por exemplo, não é possível atribuir uma tarefa a um usuário excluído.

### Resumo das etapas {#summary_of_steps-1}

Para excluir um usuário, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente DiretoryManagerService.
1. Especifique o usuário a ser excluído.
1. Exclua o usuário do AEM Forms.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar um cliente DiretoryManagerService**

Antes de executar programaticamente uma operação de API de serviço do Gerenciador de Diretórios, crie um cliente de serviço do Gerenciador de Diretórios.

**Especificar o usuário a ser excluído**

Você pode especificar um usuário a ser excluído usando o valor identificador do usuário.

**Excluir o usuário do AEM Forms**

Para excluir um usuário, chame o método `DirectoryManagerServiceClient` do objeto `deleteLocalUser`.

**Consulte também:**

[Excluir usuários usando a API Java](users.md#delete-users-using-the-java-api)

[Excluir usuários usando a API de serviço da Web](users.md#delete-users-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adicionar usuários](users.md#adding-users)

### Excluir usuários usando a API Java {#delete-users-using-the-java-api}

Exclua usuários usando a API de serviço do Gerenciador de Diretórios (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-usermanager-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente DiretoryManagerService.

   Crie um objeto `DirectoryManagerServiceClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Especifique o usuário a ser excluído.

   * Crie um objeto `PrincipalSearchFilter` usando seu construtor.
   * Defina o valor do identificador do usuário chamando o método `PrincipalSearchFilter` do objeto `setUserId`. Passe um valor de string que representa o valor do identificador do usuário.
   * Chame o método `DirectoryManagerServiceClient` do objeto `findPrincipals` e passe o objeto `PrincipalSearchFilter`. Este método retorna uma instância `java.util.List`, onde cada elemento é um objeto `User`. Interaja pela instância `java.util.List` para localizar o usuário a ser excluído.

1. Exclua o usuário do AEM Forms.

   Chame o método `DirectoryManagerServiceClient` do objeto `deleteLocalUser` e passe o valor do campo `User` do objeto `oid`. Chame o método `User` do objeto `getOid`. Use o objeto `User` recuperado da instância `java.util.List`.

**Consulte também:**

[Resumo das etapas](users.md#summary-of-steps)

[Start rápido (modo EJB): Excluir usuários usando a API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Start rápido (modo SOAP): Excluir usuários usando a API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Excluir usuários usando a API de serviço da Web {#delete-users-using-the-web-service-api}

Exclua usuários usando a API de serviço do Gerenciador de Diretórios (serviço da Web):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-usermanager-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente DiretoryManagerService.

   * Crie um objeto `DirectoryManagerServiceClient` usando seu construtor padrão.
   * Crie um objeto `DirectoryManagerServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). Não é necessário usar o atributo `lc_version`. Esse atributo é usado ao criar uma referência de serviço. Certifique-se de especificar `blob=mtom.`
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `DirectoryManagerServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Especifique o usuário a ser excluído.

   * Crie um objeto `PrincipalSearchFilter` usando seu construtor.
   * Defina o valor do identificador do usuário atribuindo um valor de string ao campo `PrincipalSearchFilter` `userId` do objeto.
   * Chame o método `DirectoryManagerServiceClient` do objeto `findPrincipals` e passe o objeto `PrincipalSearchFilter`. Este método retorna um objeto de coleção `MyArrayOfUser`, em que cada elemento é um objeto `User`. Insira a coleção `MyArrayOfUser` para localizar o usuário. O objeto `User` recuperado do objeto de coleção `MyArrayOfUser` é usado para excluir o usuário.

1. Exclua o usuário do AEM Forms.

   Exclua o usuário transmitindo o valor do campo `User` do objeto `oid` para o método `DirectoryManagerServiceClient` do objeto `deleteLocalUser`.

**Consulte também:**

[Resumo das etapas](users.md#summary-of-steps)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Criação de grupos {#creating-groups}

Você pode usar a API de serviço do Gerenciador de Diretórios (Java e serviço da Web) para criar grupos AEM Forms de forma programática. Depois de criar um grupo, você pode usá-lo para executar uma operação de serviço que exija um grupo. Por exemplo, você pode atribuir um usuário ao novo grupo. (Consulte [Gerenciar usuários e grupos](users.md#managing-users-and-groups).)

### Resumo das etapas {#summary_of_steps-2}

Para criar um grupo, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente DiretoryManagerService.
1. Determine se o grupo não existe.
1. Crie o grupo.
1. Execute uma ação com o grupo.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms estiver implantado em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo os arquivos da biblioteca Java da AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente DiretoryManagerService**

Antes de executar programaticamente uma operação de serviço do Gerenciador de Diretórios, crie um cliente da API de serviço do Gerenciador de Diretórios.

**Determine se o grupo existe**

Ao criar um grupo, verifique se ele não existe no mesmo domínio. Ou seja, dois grupos não podem ter o mesmo nome dentro do mesmo domínio. Para executar essa tarefa, faça uma pesquisa e filtre os resultados da pesquisa com base em dois valores. Defina o tipo de principal como `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` para garantir que somente os grupos sejam retornados. Além disso, certifique-se de especificar o nome do domínio.

**Criar o grupo**

Depois de determinar que o grupo não existe no domínio, crie o grupo e especifique os seguintes atributos:

* **CommonName**: O nome do grupo.
* **Domínio**: O domínio no qual o grupo é adicionado.
* **Descrição**: Uma descrição do grupo.

**Executar uma ação com o grupo**

Depois de criar um grupo, você pode executar uma ação usando o grupo. Por exemplo, você pode adicionar um usuário ao grupo. Para adicionar um usuário a um grupo, recupere o valor identificador exclusivo do usuário e do grupo. Passe esses valores para o método `addPrincipalToLocalGroup`.

**Consulte também:**

[Criar grupos usando a API Java](users.md#create-groups-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adicionar usuários](users.md#adding-users)

[Excluindo usuários](users.md#deleting-users)

### Criar grupos usando a API Java {#create-groups-using-the-java-api}

Crie um grupo usando a API de serviço do Diretory Manager (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-usermanager-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente DiretoryManagerService.

   Crie um objeto `DirectoryManagerServiceClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Determine se o grupo existe.

   * Crie um objeto `PrincipalSearchFilter` usando seu construtor.
   * Defina o tipo principal chamando o objeto `PrincipalSearchFilter` do objeto `setPrincipalType`. Passe o valor `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`.
   * Defina o domínio chamando o objeto `PrincipalSearchFilter` do objeto `setSpecificDomainName`. Passe um valor de string que especifica o nome do domínio.
   * Para localizar um grupo, chame o método `DirectoryManagerServiceClient` do objeto `findPrincipals` (um principal pode ser um grupo). Passe o objeto `PrincipalSearchFilter` que especifica o tipo principal e o nome do domínio. Este método retorna uma instância `java.util.List` em que cada elemento é uma instância `Group`. Cada instância do grupo está em conformidade com o filtro especificado usando o objeto `PrincipalSearchFilter`.
   * Iterar pela instância `java.util.List`. Para cada elemento, recupere o nome do grupo. Certifique-se de que o nome do grupo não seja igual ao novo nome do grupo.

1. Crie o grupo.

   * Se o grupo não existir, chame o método `Group` do objeto `setCommonName` e transmita um valor de string que especifica o nome do grupo.
   * Chame o método `Group` do objeto `setDescription` e transmita um valor de string que especifica a descrição do grupo.
   * Chame o método `Group` do objeto `setDomainName` e passe um valor de string que especifique o nome do domínio.
   * Chame o método `DirectoryManagerServiceClient` do objeto `createLocalGroup` e passe a instância `Group`.

   O método `createLocalUser` retorna um valor de cadeia de caracteres que especifica o valor do identificador de usuário local.

1. Execute uma ação com o grupo.

   * Crie um objeto `PrincipalSearchFilter` usando seu construtor.
   * Defina o valor do identificador do usuário chamando o método `PrincipalSearchFilter` do objeto `setUserId`. Passe um valor de string que representa o valor do identificador do usuário.
   * Chame o método `DirectoryManagerServiceClient` do objeto `findPrincipals` e passe o objeto `PrincipalSearchFilter`. Este método retorna uma instância `java.util.List`, onde cada elemento é um objeto `User`. Insira a instância `java.util.List` para localizar o usuário.
   * Adicione um usuário ao grupo chamando o método `DirectoryManagerServiceClient` do objeto `addPrincipalToLocalGroup`. Passe o valor de retorno do método `User` do objeto `getOid`. Passe o valor de retorno do método `Group` dos objetos `getOid` (use a instância `Group` que representa o novo grupo).

**Consulte também:**

[Resumo das etapas](users.md#summary-of-steps)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Gerenciando usuários e grupos {#managing-users-and-groups}

Este tópico descreve como você pode usar (Java) para atribuir, remover e programaticamente atribuir domínios, usuários e grupos ao query.

>[!NOTE]
>
>Ao configurar um domínio, você deve definir o identificador exclusivo para grupos e usuários. O atributo escolhido não deve ser exclusivo no ambiente LDAP, mas deve ser imutável e não será alterado no diretório. Este atributo também deve ser de um tipo de dados de sequência simples (a única exceção atualmente permitida para o Ative Diretory 2000/2003 é `"objectsid"`, que é um valor binário). O atributo Novell eDirectory `"GUID"`, por exemplo, não é um tipo de dados simples de string e, portanto, não funcionará.

* Para o Ative Diretory, use `"objectsid"`.
* Para o SunOne, use `"nsuniqueid"`.

>[!NOTE]
>
>Não há suporte para a criação de vários usuários e grupos locais enquanto uma sincronização de diretório LDAP estiver em andamento. Tentar esse processo pode resultar em erros.

### Resumo das etapas {#summary_of_steps-3}

Para gerenciar usuários e grupos, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente DiretoryManagerService.
1. Chame as operações apropriadas do usuário ou grupo.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente DiretoryManagerService**

Antes de executar programaticamente uma operação de serviço do Gerenciador de Diretórios, você deve criar um cliente de serviço do Gerenciador de Diretórios. Com a API Java, isso é feito criando um objeto `DirectoryManagerServiceClient`. Com a API de serviço da Web, isso é feito criando um objeto `DirectoryManagerServiceService`.

**Chamar as operações apropriadas do usuário ou grupo**

Depois de criar o cliente de serviço, você pode chamar as operações de gerenciamento de usuários ou grupos. O cliente de serviço permite que você atribua, remova e query domínios, usuários e grupos. Observe que é possível adicionar um principal de diretório ou um principal local a um grupo local, mas não é possível adicionar um principal local a um grupo de diretórios.

**Consulte também:**

[Gerenciamento de usuários e grupos usando a API Java](users.md#managing-users-and-groups-using-the-java-api)

[Gerenciamento de usuários e grupos usando a API de serviço da Web](users.md#managing-users-and-groups-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Gerenciador de usuários](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Gerenciamento de usuários e grupos usando a API Java {#managing-users-and-groups-using-the-java-api}

Para gerenciar programaticamente usuários, grupos e domínios usando o (Java), execute as seguintes tarefas:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-usermanager-client.jar, no caminho de classe do seu projeto Java. Para obter informações sobre a localização desses arquivos, consulte [Incluindo os arquivos da biblioteca Java da AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Crie um cliente DiretoryManagerService.

   Crie um objeto `DirectoryManagerServiceClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão. Para obter informações, consulte [Definição de propriedades de ligação ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*.*

1. Chame as operações apropriadas do usuário ou grupo.

   Para localizar um usuário ou grupo, chame um dos métodos do objeto `DirectoryManagerServiceClient` para localizar principais (uma vez que um principal pode ser um usuário ou um grupo). No exemplo abaixo, o método `findPrincipals` é chamado usando um filtro de pesquisa (um objeto `PrincipalSearchFilter`).

   Como o valor de retorno nesse caso é um `java.util.List` contendo `Principal` objetos, repita o resultado e converta os objetos `Principal` em `User` ou `Group`.

   Usando o objeto resultante `User` ou `Group` (que ambos herdam da interface `Principal`), recupere as informações necessárias nos workflows. Por exemplo, os valores de nome de domínio e nome canônico, em combinação, identificam exclusivamente um principal. Eles são recuperados chamando os métodos `Principal` `getDomainName` e `getCanonicalName` do objeto, respectivamente.

   Para excluir um usuário local, chame o método `DirectoryManagerServiceClient` do objeto e passe o identificador do usuário.`deleteLocalUser`

   Para excluir um grupo local, chame o método `DirectoryManagerServiceClient` do objeto e passe o identificador do grupo.`deleteLocalGroup`

**Consulte também:**

[Resumo das etapas](users.md#summary-of-steps)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Gerenciamento de usuários e grupos usando a API de serviço da Web {#managing-users-and-groups-using-the-web-service-api}

Para gerenciar programaticamente usuários, grupos e domínios usando a API de serviço do Diretory Manager (serviço da Web), execute as seguintes tarefas:

1. Incluir arquivos de projeto.

   * Crie um assembly de cliente Microsoft .NET que consuma o WSDL do Gerenciador de Diretórios. (Consulte [Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Faça referência ao assembly do cliente Microsoft .NET. (Consulte [Criação de um assembly de cliente .NET que usa a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Crie um cliente DiretoryManagerService.

   Crie um objeto `DirectoryManagerServiceService` usando o construtor da classe proxy.

1. Chame as operações apropriadas do usuário ou grupo.

   Para localizar um usuário ou grupo, chame um dos métodos do objeto `DirectoryManagerServiceService` para localizar principais (uma vez que um principal pode ser um usuário ou um grupo). No exemplo abaixo, o método `findPrincipalsWithFilter` é chamado usando um filtro de pesquisa (um objeto `PrincipalSearchFilter`). Ao usar um objeto `PrincipalSearchFilter`, os principais locais só serão retornados se a propriedade `isLocal` estiver definida como `true`. Esse comportamento é diferente do que ocorreria com a API Java.

   >[!NOTE]
   >
   >Se o número máximo de resultados não for especificado no filtro de pesquisa (por meio do campo `PrincipalSearchFilter.resultsMax`), um máximo de 1000 resultados será retornado. Esse comportamento é diferente do que ocorre com a API Java, na qual 10 resultados são o máximo padrão. Além disso, os métodos de pesquisa, como `findGroupMembers`, não gerarão resultados, a menos que o número máximo de resultados seja especificado no filtro de pesquisa (por exemplo, por meio do campo `GroupMembershipSearchFilter.resultsMax`). Isso se aplica a todos os filtros de pesquisa herdados da classe `GenericSearchFilter`. Para obter mais informações, consulte [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   Como o valor de retorno nesse caso é um `object[]` contendo `Principal` objetos, repita o resultado e converta os objetos `Principal` em `User` ou `Group`.

   Usando o objeto resultante `User` ou `Group` (que ambos herdam da interface `Principal`), recupere as informações necessárias nos workflows. Por exemplo, os valores de nome de domínio e nome canônico, em combinação, identificam exclusivamente um principal. Eles são recuperados chamando os campos `Principal` `domainName` e `canonicalName` do objeto, respectivamente.

   Para excluir um usuário local, chame o método `DirectoryManagerServiceService` do objeto e passe o identificador do usuário.`deleteLocalUser`

   Para excluir um grupo local, chame o método `DirectoryManagerServiceService` do objeto e passe o identificador do grupo.`deleteLocalGroup`

**Consulte também:**

[Resumo das etapas](users.md#summary-of-steps)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Gerenciando Funções e Permissões {#managing-roles-and-permissions}

Este tópico descreve como você pode usar a API de serviço do Gerenciador de Autorização (Java) para atribuir, remover e determinar programaticamente funções e permissões.

No AEM Forms, uma *role* é um grupo de permissões para acessar um ou mais recursos no nível do sistema. Essas permissões são criadas por meio do Gerenciamento de usuários e aplicadas pelos componentes do serviço. Por exemplo, um Administrador pode atribuir a função de &quot;Autor do conjunto de políticas&quot; a um grupo de usuários. O Rights Management permitiria que os usuários desse grupo com essa função criassem conjuntos de políticas por meio do console de administração.

Há dois tipos de funções: *funções padrão* e *funções personalizadas*. As funções padrão (*funções do sistema)* já estão residentes no AEM Forms. Pressupõe-se que as funções padrão não possam ser excluídas ou modificadas pelo administrador, sendo, portanto, imutáveis. As funções personalizadas criadas pelo administrador, que podem posteriormente modificá-las ou excluí-las, são, portanto, removíveis.

As funções facilitam o gerenciamento de permissões. Quando uma função é atribuída a um principal, um conjunto de permissões é automaticamente atribuído a esse principal, e todas as decisões específicas relacionadas ao acesso do principal são baseadas nesse conjunto geral de permissões atribuídas.

### Resumo das etapas {#summary_of_steps-4}

Para gerenciar funções e permissões, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente AuthorizationManagerService.
1. Chame a função ou as operações de permissão apropriadas.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente AuthorizationManagerService**

Antes de executar programaticamente uma operação AuthorizationManagerService de Gerenciamento de Usuário, você deve criar um cliente AuthorizationManagerService. Com a API Java, isso é feito criando um objeto `AuthorizationManagerServiceClient`.

**Chamar as operações de permissão ou função apropriadas**

Depois de criar o cliente de serviço, você pode chamar a função ou as operações de permissão. O cliente de serviço permite que você atribua, remova e determine funções e permissões.

**Consulte também:**

[Gerenciamento de funções e permissões usando a API Java](users.md#managing-roles-and-permissions-using-the-java-api)

[Gerenciando funções e permissões usando a API de serviço da Web](users.md#managing-roles-and-permissions-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Gerenciador de usuários](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Gerenciando funções e permissões usando a API Java {#managing-roles-and-permissions-using-the-java-api}

Para gerenciar funções e permissões usando a API de serviço do Gerenciador de Autorização (Java), execute as seguintes tarefas:

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-usermanager-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente AuthorizationManagerService.

   Crie um objeto `AuthorizationManagerServiceClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Chame a função ou as operações de permissão apropriadas.

   Para atribuir uma função a um principal, chame o método `AuthorizationManagerServiceClient` do objeto `assignRole` e passe os seguintes valores:

   * Um objeto `java.lang.String` que contém o identificador de função
   * Uma matriz de objetos `java.lang.String` contendo os identificadores principais.

   Para remover uma função de um principal, chame o método `AuthorizationManagerServiceClient` do objeto `unassignRole` e transmita os seguintes valores:

   * Um objeto `java.lang.String` que contém o identificador de função.
   * Uma matriz de objetos `java.lang.String` contendo os identificadores principais.


**Consulte também:**

[Resumo das etapas](users.md#summary-of-steps)

[Start rápido (modo SOAP): Gerenciamento de funções e permissões usando a API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Gerenciando funções e permissões usando a API de serviço da Web {#managing-roles-and-permissions-using-the-web-service-api}

Gerencie funções e permissões usando a API de serviço do Gerenciador de Autorização (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente AuthorizationManagerService.

   * Crie um objeto `AuthorizationManagerServiceClient` usando seu construtor padrão.
   * Crie um objeto `AuthorizationManagerServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`.) Não é necessário usar o atributo `lc_version`. Esse atributo é usado ao criar uma referência de serviço.
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `AuthorizationManagerServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Chame a função ou as operações de permissão apropriadas.

   Para atribuir uma função a um principal, chame o método `AuthorizationManagerServiceClient` do objeto `assignRole` e passe os seguintes valores:

   * Um objeto `string` que contém o identificador de função
   * Um objeto `MyArrayOf_xsd_string` que contém os identificadores principais.

   Para remover uma função de um principal, chame o método `AuthorizationManagerServiceService` do objeto `unassignRole` e transmita os seguintes valores:

   * Um objeto `string` que contém o identificador de função.
   * Uma matriz de objetos `string` contendo os identificadores principais.


**Consulte também:**

[Resumo das etapas](users.md#summary-of-steps)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Autenticando usuários {#authenticating-users}

Este tópico descreve como você pode usar a API de serviço do Authentication Manager (Java) para permitir que seus aplicativos clientes autentiquem usuários de forma programática.

A autenticação do usuário pode ser necessária para interagir com um banco de dados corporativo ou outros repositórios corporativos que armazenam dados protegidos.

Considere, por exemplo, um cenário em que um usuário digita um nome de usuário e senha em uma página da Web e envia os valores para um servidor de aplicativos J2EE que hospeda o Forms. Um aplicativo personalizado Forms pode autenticar o usuário com o serviço Authentication Manager.

Se a autenticação for bem-sucedida, o aplicativo acessa um banco de dados corporativo protegido. Caso contrário, uma mensagem será enviada ao usuário informando que ele não é um usuário autorizado.

O diagrama a seguir mostra o fluxo lógico do aplicativo.

![au_au_umauth_process](assets/au_au_umauth_process.png)

A tabela a seguir descreve as etapas neste diagrama

<table>
 <thead>
  <tr>
   <th><p>Etapa</p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>O usuário acessa um site e especifica um nome de usuário e senha. Essas informações são enviadas a um servidor de aplicativos J2EE que hospeda a AEM Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>As credenciais do usuário são autenticadas com o serviço Gerenciador de autenticação. Se as credenciais do usuário forem válidas, o fluxo de trabalho continuará para a etapa 3. Caso contrário, uma mensagem será enviada ao usuário informando que ele não é um usuário autorizado.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>As informações do usuário e um design de formulário são recuperados de um banco de dados corporativo protegido. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>As informações do usuário são unidas a um design de formulário e o formulário é renderizado para o usuário. </p></td>
  </tr>
 </tbody>
</table>

### Resumo das etapas {#summary_of_steps-5}

Para autenticar programaticamente um usuário, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente AuthenticationManagerService.
1. Chame a operação de autenticação.
1. Se necessário, recupere o contexto para que o aplicativo cliente possa encaminhá-lo para outro serviço da AEM Forms para autenticação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente AuthenticationManagerService**

Antes de poder autenticar programaticamente um usuário, você deve criar um cliente AuthenticationManagerService. Ao usar a API Java, crie um objeto `AuthenticationManagerServiceClient`.

**Chamar a operação de autenticação**

Depois de criar o cliente de serviço, você pode chamar a operação de autenticação. Essa operação precisará de informações sobre o usuário, como o nome e a senha do usuário. Se o usuário não autenticar, uma exceção será lançada.

**Recuperar o contexto de autenticação**

Depois de autenticar o usuário, você pode criar um contexto com base no usuário autenticado. Em seguida, você pode usar o conteúdo para chamar outros serviços da AEM Forms. Por exemplo, você pode usar o contexto para criar um `EncryptionServiceClient` e criptografar um documento PDF com uma senha. Certifique-se de que o usuário que foi autenticado tenha a função `Services User` necessária para chamar um serviço AEM Forms.

**Consulte também:**

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Gerenciador de usuários](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Criptografar Documentos PDF com uma senha](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Autenticar um usuário usando a API Java {#authenticate-a-user-using-the-java-api}

Autentique um usuário usando a Authentication Manager Service API (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-usermanager-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente AuthenticationManagerServices.

   Crie um objeto `AuthenticationManagerServiceClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Chame a operação de autenticação.

   Chame o método `AuthenticationManagerServiceClient` do objeto `authenticate` e passe os seguintes valores:

   * Um objeto `java.lang.String` que contém o nome do usuário.
   * Uma matriz de bytes (um objeto `byte[]`) que contém a senha do usuário. Você pode obter o objeto `byte[]` chamando o método `java.lang.String` do objeto `getBytes`.

   O método authenticate retorna um objeto `AuthResult`, que contém informações sobre o usuário autenticado.

1. Recuperar o contexto de autenticação.

   Chame o método `ServiceClientFactory` do objeto `getContext`, que retornará um objeto `Context`.

   Em seguida, chame o método `Context` do objeto `initPrincipal` e passe o `AuthResult`.

### Autenticar um usuário usando a API de serviço da Web {#authenticate-a-user-using-the-web-service-api}

Autentique um usuário usando a Authentication Manager Service API (serviço da Web):

1. Incluir arquivos de projeto.

   * Crie um assembly de cliente Microsoft .NET que consuma o WSDL do Authentication Manager. (Consulte [Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Faça referência ao assembly do cliente Microsoft .NET. (Consulte &quot;Referenciando o assembly do cliente .NET&quot; em [Invocando o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

1. Crie um cliente AuthenticationManagerService.

   Crie um objeto `AuthenticationManagerServiceService` usando o construtor da classe proxy.

1. Chame a operação de autenticação.

   Chame o método `AuthenticationManagerServiceClient` do objeto `authenticate` e passe os seguintes valores:

   * Um objeto `string` que contém o nome do usuário
   * Uma matriz de bytes (um objeto `byte[]`) que contém a senha do usuário. Você pode obter o objeto `byte[]` convertendo um objeto `string` que contém a senha em uma matriz `byte[]` usando a lógica mostrada no exemplo abaixo.
   * O valor retornado será um objeto `AuthResult`, que pode ser usado para recuperar informações sobre o usuário. No exemplo abaixo, as informações do usuário são recuperadas obtendo primeiro o campo `AuthResult` `authenticatedUser` do objeto e obtendo subsequentemente os campos `User` e `domainName` do objeto resultante.`canonicalName`

**Consulte também:**

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Sincronizando Programaticamente Usuários {#programmatically-synchronizing-users}

Você pode sincronizar os usuários de forma programática usando a API Gerenciamento de usuários. Ao sincronizar usuários, você está atualizando o AEM Forms com os dados do usuário localizados no repositório do usuário. Por exemplo, suponha que você adicione novos usuários ao repositório de usuários. Depois de executar uma operação de sincronização, os novos usuários se tornarão AEM usuários de formulários. Além disso, os usuários que não estão mais em seu repositório de usuários são removidos da AEM Forms.

O diagrama a seguir mostra a sincronização do AEM Forms com um repositório do usuário.

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

A tabela a seguir descreve as etapas neste diagrama

<table>
 <thead>
  <tr>
   <th><p>Etapa</p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>3</p></td>
   <td><p>Um aplicativo cliente solicita que a AEM Forms execute uma operação de sincronização.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>A AEM Forms realiza uma operação de sincronização.</p></td>
  </tr>
  <tr>
   <td><p>1</p></td>
   <td><p>As informações do usuário são atualizadas.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Um usuário pode visualização as informações atualizadas do usuário. </p></td>
  </tr>
 </tbody>
</table>

### Resumo das etapas {#summary_of_steps-6}

Para sincronizar os usuários programaticamente, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente UserManagerUtilServiceClient.
1. Especifique o domínio corporativo.
1. Chame a operação de autenticação.
1. Determine se a operação de sincronização está concluída

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente UserManagerUtilServiceClient**

Antes de sincronizar programaticamente os usuários, é necessário criar um objeto `UserManagerUtilServiceClient`.

**Especificar o domínio corporativo**

Antes de executar uma operação de sincronização usando a API Gerenciamento de usuários, especifique o domínio corporativo ao qual os usuários pertencem. Você pode especificar um ou vários domínios corporativos. Antes de executar uma operação de sincronização programaticamente, é necessário configurar um domínio corporativo usando o Console de administração. (Consulte [ajuda administrativa](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Chamar a operação de sincronização**

Depois de especificar um ou mais domínios corporativos, você pode executar a operação de sincronização. O tempo necessário para executar essa operação depende do número de registros de usuários localizados no repositório de usuários.

**Determine se a operação de sincronização está concluída**

Depois de executar programaticamente uma operação de sincronização, você pode determinar se a operação está concluída.

**Consulte também:**

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Gerenciador de usuários](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Criptografar Documentos PDF com uma senha](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Sincronização programática de usuários usando a API Java {#programmatically-synchronizing-users-using-the-java-api}

Sincronize os usuários usando a API de gerenciamento de usuários (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-usermanager-client.jar e adobe-usermanager-util-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente UserManagerUtilServiceClient.

   Crie um objeto `UserManagerUtilServiceClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Especifique o domínio corporativo.

   * Chame o método `UserManagerUtilServiceClient` do objeto `scheduleSynchronization` para start da operação de sincronização do usuário.
   * Crie uma instância `java.util.Set` usando um construtor `HashSet`. Certifique-se de especificar `String` como o tipo de dados. Esta instância `Java.util.Set` armazena os nomes de domínio aos quais a operação de sincronização se aplica.
   * Para que cada nome de domínio seja adicionado, chame o método add do objeto `java.util.Set` e passe o nome do domínio.

1. Chame a operação de sincronização.

   Chame o método `ServiceClientFactory` do objeto `getContext`, que retornará um objeto `Context`.

   Em seguida, chame o método `Context` do objeto `initPrincipal` e passe o `AuthResult`.

**Consulte também:**

[Sincronizando usuários programaticamente](users.md#programmatically-synchronizing-users)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
