---
title: Gerenciar usuários
seo-title: Managing Users
description: Use a API de gerenciamento de usuários para criar aplicativos clientes que possam gerenciar funções, permissões e principais (que podem ser usuários ou grupos), bem como autenticar usuários.
seo-description: Use the User Management API to create client applications that can manage roles, permissions, and principals (which can be users or groups), as well as authenticate users.
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
role: Developer
exl-id: d7c5bb84-a988-4b2e-a587-f4e5b50fea58
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '6228'
ht-degree: 0%

---

# Gerenciar usuários {#managing-users}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

**Sobre o Gerenciamento de usuários**

Você pode usar a API de gerenciamento de usuários para criar aplicativos clientes que possam gerenciar funções, permissões e principais (que podem ser usuários ou grupos), bem como autenticar usuários. A API de gerenciamento de usuários consiste nas seguintes APIs do AEM Forms:

* API de Serviço do Gerenciador de Diretórios
* API de Serviço do Gerenciador de Autenticação
* API de Serviço do Gerenciador de Autorização

O Gerenciamento de usuários permite que você atribua, remova e determine funções e permissões. Ela também permite atribuir, remover e consultar domínios, usuários e grupos. Por fim, você pode usar o Gerenciamento de usuários para autenticar usuários.

Em [Adicionar usuários](users.md#adding-users) você saberá como adicionar usuários de forma programática. Esta seção usa a API do Serviço do Gerenciador de Diretórios.

Em [Excluir usuários](users.md#deleting-users) você saberá como excluir usuários por programação. Esta seção usa a API do Serviço do Gerenciador de Diretórios.

Em [Gerenciar usuários e grupos](users.md#managing-users-and-groups) você entenderá a diferença entre um usuário local e um usuário de diretório, e verá exemplos de como usar as APIs de serviço da Web e Java para gerenciar usuários e grupos de forma programática. Esta seção usa a API do Serviço do Gerenciador de Diretórios.

Em [Gerenciamento de funções e permissões](users.md#managing-roles-and-permissions) você aprenderá sobre as funções e permissões do sistema e o que poderá fazer de forma programática para aumentá-las, e verá exemplos de como usar as APIs do Java e do serviço da Web para gerenciar programaticamente funções e permissões. Esta seção utiliza a API de Serviço do Gerenciador de Diretórios e a API de Serviço do Gerenciador de Autorizações.

Em [Autenticando usuários](users.md#authenticating-users) você verá exemplos de como usar as APIs do Java e do serviço da Web para autenticar usuários programaticamente. Esta seção usa a API de serviço do Gerenciador de autorizações.

**Noções básicas sobre o processo de autenticação**

O Gerenciamento de usuários fornece funcionalidade de autenticação integrada e também fornece a capacidade de conectá-la a seu próprio provedor de autenticação. Quando o Gerenciamento de usuários recebe uma solicitação de autenticação (por exemplo, um usuário tenta fazer logon), ele transmite as informações do usuário ao provedor de autenticação para autenticação. O Gerenciamento de usuários recebe os resultados do provedor de autenticação depois que ele autentica o usuário.

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
   <td><p>Um usuário tenta fazer logon em um serviço que chama o Gerenciamento de usuários. O usuário especifica um nome de usuário e senha. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>O Gerenciamento de usuários envia o nome de usuário e a senha, bem como informações de configuração, para o provedor de autenticação.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>O provedor de autenticação se conecta ao armazenamento de usuários e autentica o usuário.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>O provedor de autenticação retorna os resultados para o Gerenciamento de usuários.</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>O Gerenciamento de usuários permite que o usuário faça logon ou negue acesso ao produto.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Se o fuso horário do servidor for diferente do fuso horário do cliente, ao consumir o WSDL para o serviço Gerar PDF da AEM Forms em uma pilha SOAP nativa usando um cliente .NET em um cluster do WebSphere Application Server, o seguinte erro de autenticação do Gerenciamento de Usuário poderá ocorrer:

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**Entendendo o gerenciamento de diretórios**

O Gerenciamento de usuários é empacotado com um provedor de serviço de diretório (o DiretoryManagerService) que oferece suporte a conexões com diretórios LDAP. Se sua organização usar um repositório não LDAP para armazenar registros de usuários, você poderá criar seu próprio provedor de serviços de diretório que funcione com seu repositório.

Os provedores de serviços de diretório recuperam registros de um armazenamento de usuários a pedido do Gerenciamento de usuários. O Gerenciamento de usuários armazena em cache regularmente registros de usuários e grupos no banco de dados para melhorar o desempenho.

O provedor de serviço de diretório pode ser usado para sincronizar o banco de dados do Gerenciamento de usuários com o repositório de usuários. Essa etapa garante que todas as informações do diretório de usuário e todos os registros de usuário e grupo estejam atualizados.

Além disso, o DiretoryManagerService fornece a capacidade de criar e gerenciar domínios. Os domínios definem bases de usuários diferentes. O limite de um domínio geralmente é definido de acordo com a maneira como sua organização está estruturada ou como sua loja de usuários está configurada. Os domínios Gerenciamento de usuários fornecem configurações que provedores de autenticação e provedores de serviço de diretório usam.

No XML de configuração que o Gerenciamento de usuários exporta, o nó raiz que tem o valor de atributo de `Domains` contém um elemento XML para cada domínio definido para o Gerenciamento de usuários. Cada um desses elementos contém outros elementos que definem os aspectos do domínio associados a provedores de serviços específicos.

**Como entender valores de objectSID**

Ao usar o Ative Diretory, é importante entender que uma `objectSID` não é um atributo exclusivo em vários domínios. Esse valor armazena o identificador de segurança de um objeto. Em um ambiente de vários domínios (por exemplo, uma árvore de domínios), a variável `objectSID` pode ser diferente.

Um `objectSID` seria alterado se um objeto fosse movido de um domínio do Ative Diretory para outro. Alguns objetos têm o mesmo `objectSID` em qualquer lugar do domínio. Por exemplo, grupos como BUILTIN\Administrators, BUILTIN\Power Users e assim por diante teriam o mesmo `objectSID` independentemente dos domínios. Esses `objectSID` são bem conhecidos.

## Adicionar usuários {#adding-users}

Você pode usar a API do Serviço do Gerenciador de Diretórios (Java e serviço da Web) para adicionar usuários de forma programática ao AEM Forms. Depois de adicionar um usuário, você pode usá-lo ao executar uma operação de serviço que requer um usuário. Por exemplo, você pode atribuir uma tarefa ao novo usuário.

### Resumo das etapas {#summary-of-steps}

Para adicionar um usuário, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente DiretoryManagerService.
1. Defina as informações do usuário.
1. Adicione o usuário ao AEM Forms.
1. Verifique se o usuário foi adicionado.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar um cliente DiretoryManagerService**

Antes de executar programaticamente uma operação de serviço do Diretory Manager, crie um cliente de API do Serviço do Diretory Manager.

**Definir informações do usuário**

Ao adicionar um novo usuário usando a API do Serviço do Gerenciador de Diretórios, defina as informações para esse usuário. Normalmente, quando você adiciona um novo usuário, você define os seguintes valores:

* **Nome do domínio**: O domínio ao qual o usuário pertence (por exemplo, `DefaultDom`).
* **Valor do identificador do usuário**: O valor identificador do usuário (por exemplo, `wblue`).
* **Tipo principal**: O tipo de usuário (por exemplo, você pode especificar `USER)`.
* **Nome**: Um determinado nome para o usuário (por exemplo, `Wendy`).
* **Nome da família**: O nome da família do usuário (por exemplo, `Blue)`.
* **Localidade**: Informações de localidade para o usuário.

**Adicionar o usuário ao AEM Forms**

Após definir as informações do usuário, é possível adicioná-lo ao AEM Forms. Para adicionar um usuário, chame a função `DirectoryManagerServiceClient` do objeto `createLocalUser` método .

**Verificar se o usuário foi adicionado**

Você pode verificar se o usuário foi adicionado para garantir que nenhum problema ocorreu. Localize o novo usuário usando o valor do identificador do usuário.

**Consulte também**

[Adicionar usuários usando a API do Java](users.md#add-users-using-the-java-api)

[Adicionar usuários usando a API de serviço da Web](users.md#add-users-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Excluir usuários](users.md#deleting-users)

### Adicionar usuários usando a API do Java {#add-users-using-the-java-api}

Adicione usuários usando a API do Serviço do Gerenciador de Diretórios (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-usermanager-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente DiretoryManagerServices.

   Crie um `DirectoryManagerServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Defina as informações do usuário.

   * Crie um `UserImpl` usando seu construtor.
   * Defina o nome do domínio chamando a função `UserImpl` do objeto `setDomainName` método . Passe um valor de string que especifica o nome de domínio.
   * Defina o tipo principal chamando a função `UserImpl` do objeto `setPrincipalType` método . Passe um valor de string que especifica o tipo de usuário. Por exemplo, você pode especificar `USER`.
   * Defina o valor do identificador do usuário chamando a função `UserImpl` do objeto `setUserid` método . Passe um valor de string que especifica o valor do identificador do usuário. Por exemplo, você pode especificar `wblue`.
   * Defina o nome canônico chamando a função `UserImpl` do objeto `setCanonicalName` método . Passe um valor de string que especifica o nome canônico do usuário. Por exemplo, você pode especificar `wblue`.
   * Defina o nome fornecido chamando a função `UserImpl` do objeto `setGivenName` método . Passe um valor de string que especifica o nome do usuário. Por exemplo, você pode especificar `Wendy`.
   * Defina o nome da família chamando a função `UserImpl` do objeto `setFamilyName` método . Passe um valor de string que especifica o nome da família do usuário. Por exemplo, você pode especificar `Blue`.

   >[!NOTE]
   >
   >Chame um método que pertence ao `UserImpl` para definir outros valores. Por exemplo, é possível definir o valor da localidade chamando a variável `UserImpl` do objeto `setLocale` método .

1. Adicione o usuário ao AEM Forms.

   Chame o `DirectoryManagerServiceClient` do objeto `createLocalUser` e transmita os seguintes valores:

   * O `UserImpl` objeto que representa o novo usuário
   * Um valor da string que representa a senha do usuário

   O `createLocalUser` retorna um valor de string que especifica o valor do identificador de usuário local.

1. Verifique se o usuário foi adicionado.

   * Crie um `PrincipalSearchFilter` usando seu construtor.
   * Defina o valor do identificador do usuário chamando a função `PrincipalSearchFilter` do objeto `setUserId` método . Passe um valor de string que representa o valor do identificador do usuário.
   * Chame o `DirectoryManagerServiceClient` do objeto `findPrincipals` e passe o `PrincipalSearchFilter` objeto. Esse método retorna um `java.util.List` instância , em que cada elemento é um `User` objeto. Iterar por meio do `java.util.List` para localizar o usuário.

**Consulte também**

[Resumo das etapas](users.md#summary-of-steps)

[Início rápido (modo SOAP): Adicionar usuários usando a API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Adicionar usuários usando a API de serviço da Web {#add-users-using-the-web-service-api}

Adicione usuários usando a API do Serviço do Gerenciador de Diretórios (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Use a seguinte definição WSDL para a referência de serviço: `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um cliente DiretoryManagerService.

   * Crie um `DirectoryManagerServiceClient` usando seu construtor padrão.
   * Crie um `DirectoryManagerServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. Certifique-se de especificar `?blob=mtom`.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `DirectoryManagerServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Defina as informações do usuário.

   * Crie um `UserImpl` usando seu construtor.
   * Defina o nome do domínio atribuindo um valor de string à variável `UserImpl` do objeto `domainName` campo.
   * Defina o tipo principal atribuindo um valor de string à variável `UserImpl` do objeto `principalType` campo. Por exemplo, você pode especificar `USER`.
   * Defina o valor do identificador do usuário atribuindo um valor de string à variável `UserImpl` do objeto `userid` campo.
   * Defina o valor do nome canônico atribuindo um valor de string à variável `UserImpl` do objeto `canonicalName` campo.
   * Defina o valor de nome fornecido atribuindo um valor de string à variável `UserImpl` do objeto `givenName` campo.
   * Defina o valor do nome da família atribuindo um valor de string à variável `UserImpl` do objeto `familyName` campo.

1. Adicione o usuário ao AEM Forms.

   Chame o `DirectoryManagerServiceClient` do objeto `createLocalUser` e transmita os seguintes valores:

   * O `UserImpl` objeto que representa o novo usuário
   * Um valor da string que representa a senha do usuário

   O `createLocalUser` retorna um valor de string que especifica o valor do identificador de usuário local.

1. Verifique se o usuário foi adicionado.

   * Crie um `PrincipalSearchFilter` usando seu construtor.
   * Defina o valor do identificador do usuário atribuindo um valor de string que represente o valor do identificador do usuário para a variável `PrincipalSearchFilter` do objeto `userId` campo.
   * Chame o `DirectoryManagerServiceClient` do objeto `findPrincipals` e passe o `PrincipalSearchFilter` objeto. Esse método retorna um `MyArrayOfUser` objeto de coleção, em que cada elemento é um `User` objeto. Iterar por meio do `MyArrayOfUser` coleção para localizar o usuário.

**Consulte também**

[Resumo das etapas](users.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Excluir usuários {#deleting-users}

Você pode usar a API do Serviço do Gerenciador de Diretórios (Java e serviço da Web) para excluir programaticamente usuários do AEM Forms. Após excluir um usuário, ele não poderá mais ser usado para executar uma operação de serviço que requer um usuário. Por exemplo, não é possível atribuir uma tarefa a um usuário excluído.

### Resumo das etapas {#summary_of_steps-1}

Para excluir um usuário, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente DiretoryManagerService.
1. Especifique o usuário a ser excluído.
1. Exclua o usuário do AEM Forms.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar um cliente DiretoryManagerService**

Antes de executar programaticamente uma operação de API do Serviço do Gerenciador de Diretórios, crie um cliente de serviço do Gerenciador de Diretórios.

**Especificar o usuário a ser excluído**

Você pode especificar um usuário a ser excluído usando o valor identificador do usuário.

**Excluir o usuário do AEM Forms**

Para excluir um usuário, chame o `DirectoryManagerServiceClient` do objeto `deleteLocalUser` método .

**Consulte também**

[Excluir usuários usando a API do Java](users.md#delete-users-using-the-java-api)

[Excluir usuários usando a API de serviço da Web](users.md#delete-users-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adicionar usuários](users.md#adding-users)

### Excluir usuários usando a API do Java {#delete-users-using-the-java-api}

Exclua usuários usando a API do Serviço do Gerenciador de Diretórios (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-usermanager-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente DiretoryManagerService.

   Crie um `DirectoryManagerServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Especifique o usuário a ser excluído.

   * Crie um `PrincipalSearchFilter` usando seu construtor.
   * Defina o valor do identificador do usuário chamando a função `PrincipalSearchFilter` do objeto `setUserId` método . Passe um valor de string que representa o valor do identificador do usuário.
   * Chame o `DirectoryManagerServiceClient` do objeto `findPrincipals` e passe o `PrincipalSearchFilter` objeto. Esse método retorna um `java.util.List` instância , em que cada elemento é um `User` objeto. Iterar por meio do `java.util.List` instância para localizar o usuário a ser excluído.

1. Exclua o usuário do AEM Forms.

   Chame o `DirectoryManagerServiceClient` do objeto `deleteLocalUser` e transmita o valor da variável `User` do objeto `oid` campo. Chame o `User` do objeto `getOid` método . Use o `User` objeto recuperado do `java.util.List` instância.

**Consulte também**

[Resumo das etapas](users.md#summary-of-steps)

[Início rápido (modo EJB): Exclusão de usuários usando a API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Início rápido (modo SOAP): Exclusão de usuários usando a API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Excluir usuários usando a API de serviço da Web {#delete-users-using-the-web-service-api}

Excluir usuários usando a API do Serviço do Gerenciador de Diretórios (serviço da Web):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-usermanager-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente DiretoryManagerService.

   * Crie um `DirectoryManagerServiceClient` usando seu construtor padrão.
   * Crie um `DirectoryManagerServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. Certifique-se de especificar `blob=mtom.`
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `DirectoryManagerServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Especifique o usuário a ser excluído.

   * Crie um `PrincipalSearchFilter` usando seu construtor.
   * Defina o valor do identificador do usuário atribuindo um valor de string à variável `PrincipalSearchFilter` do objeto `userId` campo.
   * Chame o `DirectoryManagerServiceClient` do objeto `findPrincipals` e passe o `PrincipalSearchFilter` objeto. Esse método retorna um `MyArrayOfUser` objeto de coleção, em que cada elemento é um `User` objeto. Iterar por meio do `MyArrayOfUser` coleção para localizar o usuário. O `User` objeto recuperado do `MyArrayOfUser` objeto de coleção é usado para excluir o usuário.

1. Exclua o usuário do AEM Forms.

   Exclua o usuário transmitindo a variável `User` do objeto `oid` valor do campo para `DirectoryManagerServiceClient` do objeto `deleteLocalUser` método .

**Consulte também**

[Resumo das etapas](users.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Criação de grupos {#creating-groups}

Você pode usar a API do Serviço do Gerenciador de Diretórios (Java e serviço da Web) para criar grupos do AEM Forms de forma programática. Depois de criar um grupo, você pode usar esse grupo para executar uma operação de serviço que requer um grupo. Por exemplo, você pode atribuir um usuário ao novo grupo. (Consulte [Gerenciar usuários e grupos](users.md#managing-users-and-groups).)

### Resumo das etapas {#summary_of_steps-2}

Para criar um grupo, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente DiretoryManagerService.
1. Determine se o grupo não existe.
1. Crie o grupo.
1. Execute uma ação com o grupo.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente DiretoryManagerService**

Antes de executar programaticamente uma operação de serviço do Diretory Manager, crie um cliente de API do Serviço do Diretory Manager.

**Determine se o grupo existe**

Ao criar um grupo, verifique se o grupo não existe no mesmo domínio. Ou seja, dois grupos não podem ter o mesmo nome no mesmo domínio. Para executar essa tarefa, faça uma pesquisa e filtre os resultados da pesquisa com base em dois valores. Defina o tipo principal como `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` para garantir que somente grupos sejam retornados. Além disso, especifique o nome de domínio.

**Criar o grupo**

Depois de determinar que o grupo não existe no domínio, crie o grupo e especifique os seguintes atributos:

* **CommonName**: O nome do grupo.
* **Domínio**: O domínio no qual o grupo é adicionado.
* **Descrição**: Uma descrição do grupo.

**Executar uma ação com o grupo**

Depois de criar um grupo, você pode executar uma ação usando o grupo . Por exemplo, você pode adicionar um usuário ao grupo. Para adicionar um usuário a um grupo, recupere o valor identificador exclusivo do usuário e do grupo. Passe esses valores para a `addPrincipalToLocalGroup` método .

**Consulte também**

[Criar grupos usando a API do Java](users.md#create-groups-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adicionar usuários](users.md#adding-users)

[Excluir usuários](users.md#deleting-users)

### Criar grupos usando a API do Java {#create-groups-using-the-java-api}

Crie um grupo usando a API do Serviço do Gerenciador de Diretórios (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-usermanager-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente DiretoryManagerService.

   Crie um `DirectoryManagerServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Determine se o grupo existe.

   * Crie um `PrincipalSearchFilter` usando seu construtor.
   * Defina o tipo principal chamando a função `PrincipalSearchFilter` do objeto `setPrincipalType` objeto. Transmita o valor `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`.
   * Defina o domínio chamando o `PrincipalSearchFilter` do objeto `setSpecificDomainName` objeto. Passe um valor de string que especifica o nome de domínio.
   * Para localizar um grupo, chame o `DirectoryManagerServiceClient` do objeto `findPrincipals` (um principal pode ser um grupo). Passe o `PrincipalSearchFilter` que especifica o tipo principal e o nome de domínio. Esse método retorna um `java.util.List` instância em que cada elemento é um `Group` instância. Cada instância de grupo está em conformidade com o filtro especificado usando o `PrincipalSearchFilter` objeto.
   * Iterar por meio do `java.util.List` instância. Para cada elemento, recupere o nome do grupo. Certifique-se de que o nome do grupo não seja igual ao novo nome do grupo.

1. Crie o grupo.

   * Caso o grupo não exista, chame a função `Group` do objeto `setCommonName` e transmita um valor de string que especifica o nome do grupo.
   * Chame o `Group` do objeto `setDescription` e transmita um valor de string que especifica a descrição do grupo.
   * Chame o `Group` do objeto `setDomainName` e transmita um valor de string que especifica o nome do domínio.
   * Chame o `DirectoryManagerServiceClient` do objeto `createLocalGroup` e passe o `Group` instância.

   O `createLocalUser` retorna um valor de string que especifica o valor do identificador de usuário local.

1. Execute uma ação com o grupo.

   * Crie um `PrincipalSearchFilter` usando seu construtor.
   * Defina o valor do identificador do usuário chamando a função `PrincipalSearchFilter` do objeto `setUserId` método . Passe um valor de string que representa o valor do identificador do usuário.
   * Chame o `DirectoryManagerServiceClient` do objeto `findPrincipals` e passe o `PrincipalSearchFilter` objeto. Esse método retorna um `java.util.List` instância , em que cada elemento é um `User` objeto. Iterar por meio do `java.util.List` para localizar o usuário.
   * Adicione um usuário ao grupo, chamando a função `DirectoryManagerServiceClient` do objeto `addPrincipalToLocalGroup` método . Passe o valor de retorno do `User` do objeto `getOid` método . Passe o valor de retorno do `Group` dos objetos `getOid` (use o `Group` que representa o novo grupo).

**Consulte também**

[Resumo das etapas](users.md#summary-of-steps)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Gerenciar usuários e grupos {#managing-users-and-groups}

Este tópico descreve como você pode usar o (Java) para atribuir, remover e consultar domínios, usuários e grupos de forma programática.

>[!NOTE]
>
>Ao configurar um domínio, você deve definir o identificador exclusivo para grupos e usuários. O atributo que é escolhido não só deve ser exclusivo no ambiente LDAP, como também deve ser imutável e não será alterado no diretório. Este atributo também deve ser de um tipo de dados de sequência simples (a única exceção atualmente permitida para o Ative Diretory 2000/2003 é `"objectsid"`, que é um valor binário). O atributo Novell eDirectory `"GUID"`, por exemplo, não é um tipo de dados de string simples e, portanto, não funcionará.

* Para o Ative Diretory, use `"objectsid"`.
* Para SunOne, use `"nsuniqueid"`.

>[!NOTE]
>
>Não há suporte para a criação de vários usuários e grupos locais enquanto uma sincronização de diretório LDAP está em andamento. Tentar esse processo pode resultar em erros.

### Resumo das etapas {#summary_of_steps-3}

Para gerenciar usuários e grupos, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente DiretoryManagerService.
1. Chame as operações apropriadas do usuário ou grupo.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente DiretoryManagerService**

Antes de executar programaticamente uma operação de serviço do Diretory Manager, você deve criar um cliente de serviço do Diretory Manager. Com a API Java, isso é feito criando uma `DirectoryManagerServiceClient` objeto. Com a API do serviço da Web, isso é feito criando um `DirectoryManagerServiceService` objeto.

**Chamar as operações apropriadas do usuário ou grupo**

Depois de criar o cliente de serviço, você pode invocar as operações de gerenciamento de usuários ou grupos. O cliente de serviço permite atribuir, remover e consultar domínios, usuários e grupos. Observe que é possível adicionar um principal de diretório ou um principal local a um grupo local, mas não é possível adicionar um principal local a um grupo de diretórios.

**Consulte também**

[Gerenciamento de usuários e grupos usando a API do Java](users.md#managing-users-and-groups-using-the-java-api)

[Gerenciamento de usuários e grupos usando a API de serviço da Web](users.md#managing-users-and-groups-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Gerenciador de usuários](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Gerenciamento de usuários e grupos usando a API do Java {#managing-users-and-groups-using-the-java-api}

Para gerenciar de forma programática usuários, grupos e domínios usando o (Java), execute as seguintes tarefas:

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-usermanager-client.jar, no caminho de classe do seu projeto Java. Para obter informações sobre a localização desses arquivos, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Crie um cliente DiretoryManagerService.

   Crie um `DirectoryManagerServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão. Para obter mais informações, consulte [Configuração das propriedades de conexão ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*.*

1. Chame as operações apropriadas do usuário ou grupo.

   Para localizar um usuário ou grupo, chame um dos `DirectoryManagerServiceClient` métodos do objeto para localizar entidades principais (já que uma entidade principal pode ser um usuário ou um grupo). No exemplo abaixo, a variável `findPrincipals` é chamado usando um filtro de pesquisa (um `PrincipalSearchFilter` objeto).

   Como o valor de retorno, nesse caso, é um `java.util.List` contendo `Principal` objetos, percorra o resultado e projete a variável `Principal` objetos para `User` ou `Group` objetos.

   Uso do resultante `User` ou `Group` objeto (que ambos herdam do `Principal` , recupere as informações necessárias em seus fluxos de trabalho. Por exemplo, o nome de domínio e os valores de nome canônico, combinados, identificam exclusivamente um principal. Eles são recuperados chamando o `Principal` do objeto `getDomainName` e `getCanonicalName` métodos, respectivamente.

   Para excluir um usuário local, chame o `DirectoryManagerServiceClient` do objeto `deleteLocalUser` e transmita o identificador do usuário.

   Para excluir um grupo local, chame o `DirectoryManagerServiceClient` do objeto `deleteLocalGroup` e passe o identificador do grupo.

**Consulte também**

[Resumo das etapas](users.md#summary-of-steps)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Gerenciamento de usuários e grupos usando a API de serviço da Web {#managing-users-and-groups-using-the-web-service-api}

Para gerenciar de forma programática usuários, grupos e domínios usando a API do serviço do Diretory Manager (serviço da Web), execute as seguintes tarefas:

1. Inclua arquivos de projeto.

   * Crie um assembly de cliente Microsoft .NET que consuma o WSDL do Gerenciador de Diretórios. (Consulte [Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Faça referência ao assembly do cliente Microsoft .NET. (Consulte [Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Crie um cliente DiretoryManagerService.

   Crie um `DirectoryManagerServiceService` usando o construtor da classe proxy.

1. Chame as operações apropriadas do usuário ou grupo.

   Para localizar um usuário ou grupo, chame um dos `DirectoryManagerServiceService` métodos do objeto para localizar entidades principais (já que uma entidade principal pode ser um usuário ou um grupo). No exemplo abaixo, a variável `findPrincipalsWithFilter` é chamado usando um filtro de pesquisa (um `PrincipalSearchFilter` objeto). Ao usar um `PrincipalSearchFilter` objeto, os principais locais só serão retornados se a variável `isLocal` está definida como `true`. Esse comportamento é diferente do que ocorria com a API do Java.

   >[!NOTE]
   >
   >Se o número máximo de resultados não for especificado no filtro de pesquisa (por meio do `PrincipalSearchFilter.resultsMax` ), no máximo 1000 resultados serão retornados. Esse é um comportamento diferente do que ocorre com a API do Java, em que 10 resultados são o máximo padrão. Além disso, os métodos de pesquisa, como `findGroupMembers` não produzirá resultados, a menos que o número máximo de resultados seja especificado no filtro de pesquisa (por exemplo, através da variável `GroupMembershipSearchFilter.resultsMax` campo ). Isso se aplica a todos os filtros de pesquisa herdados do `GenericSearchFilter` classe . Para obter mais informações, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   Como o valor de retorno, nesse caso, é uma `object[]` contendo `Principal` objetos, percorra o resultado e projete a variável `Principal` objetos para `User` ou `Group` objetos.

   Uso do resultante `User` ou `Group` objeto (que ambos herdam do `Principal` , recupere as informações necessárias em seus fluxos de trabalho. Por exemplo, o nome de domínio e os valores de nome canônico, combinados, identificam exclusivamente um principal. Eles são recuperados chamando o `Principal` do objeto `domainName` e `canonicalName` , respectivamente.

   Para excluir um usuário local, chame o `DirectoryManagerServiceService` do objeto `deleteLocalUser` e transmita o identificador do usuário.

   Para excluir um grupo local, chame o `DirectoryManagerServiceService` do objeto `deleteLocalGroup` e passe o identificador do grupo.

**Consulte também**

[Resumo das etapas](users.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Gerenciamento de funções e permissões {#managing-roles-and-permissions}

Este tópico descreve como você pode usar a API de serviço do Gerenciador de autorização (Java) para atribuir, remover e determinar funções e permissões de forma programática.

No AEM Forms, uma *função* é um grupo de permissões para acessar um ou mais recursos no nível do sistema. Essas permissões são criadas por meio do Gerenciamento de usuários e são aplicadas pelos componentes do serviço. Por exemplo, um Administrador pode atribuir a função de &quot;Autor do conjunto de políticas&quot; a um grupo de usuários. O Rights Management permitiria que os usuários desse grupo com essa função criassem conjuntos de políticas por meio do console de administração.

Há dois tipos de funções: *funções padrão* e *funções personalizadas*. Funções padrão (*funções do sistema)* já residam no AEM Forms. Pressupõe-se que as funções padrão não possam ser excluídas ou modificadas pelo administrador e, portanto, sejam imutáveis. As funções personalizadas criadas pelo administrador, que podem posteriormente modificá-las ou excluí-las, são mutáveis.

As funções facilitam o gerenciamento de permissões. Quando uma função é atribuída a um principal, um conjunto de permissões é automaticamente atribuído a esse principal e todas as decisões específicas relacionadas ao acesso do principal são baseadas nesse conjunto geral de permissões atribuídas.

### Resumo das etapas {#summary_of_steps-4}

Para gerenciar funções e permissões, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente AuthorizationManagerService.
1. Chame a função ou as operações de permissão apropriadas.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente AuthorizationManagerService**

Antes de poder executar programaticamente uma operação User Management AuthorizationManagerService, tem de criar um cliente AuthorizationManagerService. Com a API Java, isso é feito criando uma `AuthorizationManagerServiceClient` objeto.

**Chamar a função ou as operações de permissão apropriadas**

Depois de criar o cliente de serviço, você pode invocar as operações de função ou permissão. O cliente de serviço permite atribuir, remover e determinar funções e permissões.

**Consulte também**

[Gerenciamento de funções e permissões usando a API do Java](users.md#managing-roles-and-permissions-using-the-java-api)

[Gerenciamento de funções e permissões usando a API de serviço da Web](users.md#managing-roles-and-permissions-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Gerenciador de usuários](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Gerenciamento de funções e permissões usando a API do Java {#managing-roles-and-permissions-using-the-java-api}

Para gerenciar funções e permissões usando a API do Serviço do Gerenciador de Autorização (Java), execute as seguintes tarefas:

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-usermanager-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente AuthorizationManagerService.

   Crie um `AuthorizationManagerServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Chame a função ou as operações de permissão apropriadas.

   Para atribuir uma função a um principal, chame o `AuthorizationManagerServiceClient` do objeto `assignRole` e transmita os seguintes valores:

   * A `java.lang.String` objeto que contém o identificador da função
   * Uma matriz de `java.lang.String` objetos que contêm os identificadores principais.

   Para remover uma função de um principal, chame o `AuthorizationManagerServiceClient` do objeto `unassignRole` e transmita os seguintes valores:

   * A `java.lang.String` objeto que contém o identificador da função.
   * Uma matriz de `java.lang.String` objetos que contêm os identificadores principais.


**Consulte também**

[Resumo das etapas](users.md#summary-of-steps)

[Início rápido (modo SOAP): Gerenciamento de funções e permissões usando a API do Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Gerenciamento de funções e permissões usando a API de serviço da Web {#managing-roles-and-permissions-using-the-web-service-api}

Gerencie funções e permissões usando a API do Serviço do Gerenciador de Autorizações (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um cliente AuthorizationManagerService.

   * Crie um `AuthorizationManagerServiceClient` usando seu construtor padrão.
   * Crie um `AuthorizationManagerServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `AuthorizationManagerServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Chame a função ou as operações de permissão apropriadas.

   Para atribuir uma função a um principal, chame o `AuthorizationManagerServiceClient` do objeto `assignRole` e transmita os seguintes valores:

   * A `string` objeto que contém o identificador da função
   * A `MyArrayOf_xsd_string` objeto que contém os identificadores principais.

   Para remover uma função de um principal, chame o `AuthorizationManagerServiceService` do objeto `unassignRole` e transmita os seguintes valores:

   * A `string` objeto que contém o identificador da função.
   * Uma matriz de `string` objetos que contêm os identificadores principais.


**Consulte também**

[Resumo das etapas](users.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Autenticando usuários {#authenticating-users}

Este tópico descreve como você pode usar a API do Serviço do Gerenciador de Autenticação (Java) para permitir que seus aplicativos cliente autenticem usuários programaticamente.

A autenticação do usuário pode ser necessária para interagir com um banco de dados corporativo ou outros repositórios corporativos que armazenam dados protegidos.

Considere, por exemplo, um cenário em que um usuário insere um nome de usuário e senha em uma página da Web e envia os valores a um servidor de aplicativos J2EE que hospeda o Forms. Um aplicativo personalizado do Forms pode autenticar o usuário com o serviço do Gerenciador de autenticação.

Se a autenticação for bem-sucedida, o aplicativo acessa um banco de dados corporativo seguro. Caso contrário, uma mensagem será enviada ao usuário informando que ele não é um usuário autorizado.

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
   <td><p>O usuário acessa um site e especifica um nome de usuário e senha. Essas informações são enviadas para um servidor de aplicativos J2EE que hospeda a AEM Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>As credenciais do usuário são autenticadas com o serviço do Gerenciador de Autenticação. Se as credenciais do usuário forem válidas, o fluxo de trabalho prosseguirá para a etapa 3. Caso contrário, uma mensagem será enviada ao usuário informando que ele não é um usuário autorizado.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>As informações do usuário e um design de formulário são recuperadas de um banco de dados corporativo seguro. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>As informações do usuário são unidas a um design de formulário e o formulário é renderizado para o usuário. </p></td>
  </tr>
 </tbody>
</table>

### Resumo das etapas {#summary_of_steps-5}

Para autenticar um usuário programaticamente, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente AuthenticationManagerService.
1. Chame a operação de autenticação.
1. Se necessário, recupere o contexto para que o aplicativo cliente possa encaminhá-lo para outro serviço da AEM Forms para autenticação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente AuthenticationManagerService**

Antes de poder autenticar programaticamente um usuário, você deve criar um cliente AuthenticationManagerService . Ao usar a API do Java, crie um `AuthenticationManagerServiceClient` objeto.

**Chamar a operação de autenticação**

Depois de criar o cliente de serviço, você pode invocar a operação de autenticação. Essa operação precisará de informações sobre o usuário, como o nome e a senha do usuário. Se o usuário não autenticar, uma exceção será lançada.

**Recuperar o contexto de autenticação**

Depois de autenticar o usuário, você pode criar um contexto com base no usuário autenticado. Em seguida, você pode usar o conteúdo para chamar outros serviços da AEM Forms. Por exemplo, você pode usar o contexto para criar um `EncryptionServiceClient` e criptografe um documento PDF com uma senha. Certifique-se de que o usuário que foi autenticado tenha a função nomeada `Services User` que é necessário para chamar um serviço AEM Forms.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Gerenciador de usuários](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Criptografar documentos do PDF com uma senha](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Autenticar um usuário usando a API do Java {#authenticate-a-user-using-the-java-api}

Autentique um usuário usando a API do Serviço do Gerenciador de Autenticação (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-usermanager-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente AuthenticationManagerServices.

   Crie um `AuthenticationManagerServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Chame a operação de autenticação.

   Chame o `AuthenticationManagerServiceClient` do objeto `authenticate` e transmita os seguintes valores:

   * A `java.lang.String` objeto que contém o nome do usuário.
   * Uma matriz de bytes (um `byte[]` ) contendo a senha do usuário. Você pode obter a variável `byte[]` chamando o `java.lang.String` do objeto `getBytes` método .

   O método de autenticação retorna um `AuthResult` objeto , que contém informações sobre o usuário autenticado.

1. Recupere o contexto de autenticação.

   Chame o `ServiceClientFactory` do objeto `getContext` , que retornará um `Context` objeto.

   Em seguida, chame o `Context` do objeto `initPrincipal` e passe o `AuthResult`.

### Autenticar um usuário usando a API do serviço da Web {#authenticate-a-user-using-the-web-service-api}

Autentique um usuário usando a API do Serviço do Gerenciador de Autenticação (serviço da Web):

1. Inclua arquivos de projeto.

   * Crie um conjunto de clientes Microsoft .NET que consuma o WSDL do Gerenciador de Autenticação. (Consulte [Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Faça referência ao assembly do cliente Microsoft .NET. (Consulte &quot;Fazendo referência ao assembly do cliente .NET&quot; em [Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

1. Crie um cliente AuthenticationManagerService.

   Crie um `AuthenticationManagerServiceService` usando o construtor da classe proxy.

1. Chame a operação de autenticação.

   Chame o `AuthenticationManagerServiceClient` do objeto `authenticate` e transmita os seguintes valores:

   * A `string` objeto que contém o nome do usuário
   * Uma matriz de bytes (um `byte[]` ) contendo a senha do usuário. Você pode obter a variável `byte[]` convertendo um objeto `string` objeto que contém a senha para um `byte[]` usando a lógica mostrada no exemplo abaixo.
   * O valor retornado será um `AuthResult` objeto , que pode ser usado para recuperar informações sobre o usuário. No exemplo abaixo, as informações do usuário são recuperadas primeiro obtendo o `AuthResult` do objeto `authenticatedUser` e, posteriormente, obter o resultado `User` do objeto `canonicalName` e `domainName` campos.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Sincronização programática de usuários {#programmatically-synchronizing-users}

Você pode sincronizar usuários por programação usando a API de gerenciamento de usuários. Ao sincronizar usuários, você está atualizando o AEM Forms com dados de usuários localizados no repositório de usuários. Por exemplo, suponha que você adicione novos usuários ao repositório de usuários. Após executar uma operação de sincronização, os novos usuários se tornarão usuários AEM formulários. Além disso, os usuários que não estão mais em seu repositório de usuários são removidos do AEM Forms.

O diagrama a seguir mostra a sincronização do AEM Forms com um repositório de usuários.

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
   <td><p>1</p></td>
   <td><p>Um aplicativo cliente solicita que o AEM Forms execute uma operação de sincronização.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>O AEM Forms executa uma operação de sincronização.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>As informações do usuário são atualizadas.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Um usuário pode exibir as informações atualizadas do usuário. </p></td>
  </tr>
 </tbody>
</table>

### Resumo das etapas {#summary_of_steps-6}

Para sincronizar usuários programaticamente, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente UserManagerUtilServiceClient .
1. Especifique o domínio empresarial.
1. Chame a operação de autenticação.
1. Determine se a operação de sincronização foi concluída

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente UserManagerUtilServiceClientclient**

Antes de sincronizar usuários programaticamente, você deve criar um `UserManagerUtilServiceClient` objeto.

**Especificar o domínio empresarial**

Antes de executar uma operação de sincronização usando a API de gerenciamento de usuários, especifique o domínio corporativo ao qual os usuários pertencem. Você pode especificar um ou vários domínios corporativos. Antes de executar uma operação de sincronização programaticamente, é necessário configurar um domínio corporativo usando o Console de Administração. (Consulte [ajuda administrativa](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Chamar a operação de sincronização**

Após especificar um ou mais domínios corporativos, é possível executar a operação de sincronização. O tempo necessário para executar essa operação depende do número de registros de usuário localizados no repositório de usuários.

**Determine se a operação de sincronização foi concluída**

Após executar uma operação de sincronização programaticamente, você pode determinar se a operação foi concluída.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Gerenciador de usuários](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Criptografar documentos do PDF com uma senha](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Sincronização programática de usuários usando a API do Java {#programmatically-synchronizing-users-using-the-java-api}

Sincronize usuários usando a API de gerenciamento de usuários (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-usermanager-client.jar e adobe-usermanager-util-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente UserManagerUtilServiceClient .

   Crie um `UserManagerUtilServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Especifique o domínio empresarial.

   * Chame o `UserManagerUtilServiceClient` do objeto `scheduleSynchronization` para iniciar a operação de sincronização do usuário.
   * Crie um `java.util.Set` usando uma `HashSet` construtor. Certifique-se de especificar `String` como tipo de dados. Essa `Java.util.Set` A instância armazena os nomes de domínio aos quais a operação de sincronização se aplica.
   * Para cada nome de domínio a ser adicionado, chame o `java.util.Set` adicione o método do objeto e passe o nome do domínio.

1. Chame a operação de sincronização.

   Chame o `ServiceClientFactory` do objeto `getContext` , que retornará um `Context` objeto.

   Em seguida, chame o `Context` do objeto `initPrincipal` e passe o `AuthResult`.

**Consulte também**

[Sincronização programática de usuários](users.md#programmatically-synchronizing-users)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
