---
title: Criando um Manipulador de Usuários Externos de Convite
description: Criando um Manipulador de Usuários Externos de Convite
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---


# Criando um Manipulador de Usuários Externos de Convite {#create-invite-external-users-handler}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

Você pode criar um Manipulador de Usuários Externos de Convite para o serviço Rights Management. Um Manipulador de Usuários Externos de Convite permite que o serviço Rights Management convide usuários externos a se tornarem usuários do Rights Management. Depois que um usuário se torna Rights Management, ele é capaz de executar tarefas, como abrir um documento PDF protegido por política. Depois que o Manipulador de usuários externos do Convite for implantado no AEM Forms, você poderá usar o console de administração para interagir com ele.

>[!NOTE]
>
>Um Manipulador de Usuários Externos de Convite é um componente do AEM Forms. Antes de criar um Manipulador de Usuários Externos do Convite, recomenda-se familiarizar-se com a criação de componentes.

**Resumo das etapas**

Para desenvolver um Manipulador de Usuários Externos de Convite, você deve executar as seguintes etapas:

1. Configure seu ambiente de desenvolvimento.
1. Defina a implementação do Manipulador de Usuários Externos do Convite.
1. Defina o arquivo XML do componente.
1. Implante o Manipulador de Convidar Usuários Externos.
1. Teste o Manipulador de Usuários Externos do Convite.

## Configurar seu ambiente de desenvolvimento {#setting-up-development-environment}

Para configurar seu ambiente de desenvolvimento, você deve criar um novo projeto Java, como um projeto Eclipse. A versão do Eclipse compatível é `3.2.1` ou posterior.

O SPI Rights Management requer que o arquivo `edc-server-spi.jar` seja definido no caminho de classe do seu projeto. Se você não fizer referência a esse arquivo JAR, não poderá usar o SPI do Rights Management em seu projeto Java. Esse arquivo JAR é instalado com o SDK do AEM Forms na pasta `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi`.

Além de adicionar o arquivo `edc-server-spi.jar` ao caminho de classe do seu projeto, você também deve adicionar os arquivos JAR necessários para usar a API do Rights Management Service. Esses arquivos são necessários para usar a API do Rights Management Service no Manipulador de Usuários Externos do Convite.

## Definição da implementação do manipulador de usuários externos do convite {#define-invite-external-users-handler}

Para desenvolver um manipulador de usuários externos do convite, você deve criar uma classe Java que implemente a interface `com.adobe.edc.server.spi.ersp.InvitedUserProvider`. Essa classe contém um método chamado `invitedUser`, que o serviço Rights Management chama quando endereços de email são enviados usando a página **Adicionar usuários convidados** acessível por meio do console de administração.

O método `invitedUser` aceita uma instância `java.util.List`, que contém endereços de email com tipo string que são enviados da página **Adicionar usuários convidados**. O método `invitedUser` retorna uma matriz de objetos `InvitedUserProviderResult`, que geralmente é um mapeamento de endereços de email para objetos do usuário (não retorna nulo).

>[!NOTE]
>
>Além de demonstrar como criar um manipulador de usuários externos do convite, esta seção também usa a API do AEM Forms.

A implementação do manipulador de usuários externos do convite contém um método definido pelo usuário chamado `createLocalPrincipalAccount`. Esse método aceita um valor de string que especifica um endereço de email como valor de parâmetro. O método `createLocalPrincipalAccount` assume a pré-existência de um domínio local chamado `EDC_EXTERNAL_REGISTERED`. Você pode configurar esse nome de domínio para ser o que desejar; no entanto, para um aplicativo de produção, você pode querer integrar com um domínio empresarial.

O método `createUsers` repete cada endereço de email e cria um objeto Usuário correspondente (um usuário local no domínio `EDC_EXTERNAL_REGISTERED`). Finalmente, o método `doEmails` é chamado. Este método é intencionalmente deixado como um stub na amostra. Em uma implementação de produção, ela conteria a lógica do aplicativo para enviar mensagens de email de convite para os usuários recém-criados. É deixado na amostra para demonstrar o fluxo lógico do aplicativo de um aplicativo real.

### Definição da implementação do manipulador de usuários externos do convite {#user-handler-implementation}

A implementação do manipulador de usuários externos do convite a seguir aceita endereços de email enviados da página Adicionar usuários convidados acessível por meio do console de administração.

```as3
package com.adobe.livecycle.samples.inviteexternalusers.provider; 
 
import com.adobe.edc.server.spi.ersp.*; 
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
import com.adobe.idp.um.api.*; 
import com.adobe.idp.um.api.infomodel.*; 
import com.adobe.idp.um.api.impl.UMBaseLibrary; 
import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient; 
 
import java.util.ArrayList; 
import java.util.Iterator; 
import java.util.List; 
 
public class InviteExternalUsersSample implements InvitedUserProvider 
{ 
       private ServiceClientFactory _factory = null; 
 
       private User createLocalPrincipalAccount(String email_address) throws Exception 
       { 
    String ret = null; 
 
    //  Assume the local domain already exists! 
    String domain = "EDC_EXTERNAL_REGISTERED"; 
         
    List aliases = new ArrayList(); 
    aliases.add( email_address ); 
         
    User local_user = UMBaseLibrary.createUser( email_address, domain, email_address ); 
    local_user.setCommonName( email_address ); 
    local_user.setEmail( email_address ); 
    local_user.setEmailAliases( aliases ); 
         
    //  You may wish to disable the local user until, for example, his registration is processed by a confirmation link 
    //local_user.setDisabled( true ); 
 
    DirectoryManager directory_manager = new DirectoryManagerServiceClient( _factory ); 
    String ret_oid = directory_manager.createLocalUser( local_user, null ); 
     
    if( ret_oid == null ) 
    { 
        throw new Exception( "FAILED TO CREATE PRINCIPAL FOR EMAIL ADDRESS: " + email_address ); 
    } 
 
    return local_user; 
       } 
 
       protected User[] createUsers( List emails ) throws Exception 
       { 
    ArrayList ret_users = new ArrayList(); 
 
    _factory = ServiceClientFactory.createInstance(); 
 
    Iterator iter = emails.iterator(); 
 
    while( iter.hasNext() ) 
    { 
        String current_email = (String)iter.next(); 
 
        ret_users.add( createLocalPrincipalAccount( current_email ) ); 
    } 
 
    return (User[])ret_users.toArray( new User[0] ); 
       } 
 
       protected void doInvitations(List emails) 
       { 
    //  Here you may choose to send the users who were created an invitation email 
    //  This step is completely optional, depending on your requirements.   
       } 
 
       public InvitedUserProviderResult[] invitedUser(List emails) 
       { 
    //  This sample demonstrates the workflow for inviting a user via email 
 
    try 
    { 
 
        User[] principals = createUsers(emails); 
 
        InvitedUserProviderResult[] result = new InvitedUserProviderResult[principals.length]; 
        for( int i = 0; i < principals.length; i++ ) 
        { 
        result[i] = new InvitedUserProviderResult(); 
 
        result[i].setEmail( (String)emails.get( i ) ); 
        result[i].setUser( principals[i] ); 
        } 
 
        doInvitations(emails); 
 
        System.out.println( "SUCCESSFULLY INVITED " + result.length + " USERS" ); 
 
        return result; 
 
    } 
    catch( Exception e ) 
    { 
        System.out.println( "FAILED TO INVITE USERS FOR INVITE USERS SAMPLE" ); 
        e.printStackTrace(); 
 
        return new InvitedUserProviderResult[0]; 
    } 
       } 
}
 
```

>[!NOTE]
>
>Essa classe Java é salva como um arquivo JAVA chamado InviteExternalUsersSample.java.

## Definindo o arquivo XML do componente para o manipulador de autorização {#define-component-xml-authorization-handler}

Você deve definir um arquivo XML de componente para implantar o componente manipulador de usuários externos do convite. Um arquivo XML de componente existe para cada componente e fornece metadados sobre o componente.

O arquivo `component.xml` a seguir é usado para o manipulador de usuários externos do convite. Observe que o nome do serviço é `InviteExternalUsersSample` e a operação que esse serviço expõe é chamada de `invitedUser`. O parâmetro de entrada é uma instância `java.util.List` e o valor de saída é uma matriz de instâncias `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult`.

### Como definir o arquivo XML do componente para o manipulador de usuários externos do convite {#component-xml-invite-external-users-handler}

```as3
<component xmlns="http://adobe.com/idp/dsc/component/document"> 
<component-id>com.adobe.livecycle.samples.inviteexternalusers</component-id> 
<version>1.0</version> 
<bootstrap-class>com.adobe.livecycle.samples.inviteexternalusers.provider.BootstrapImpl</bootstrap-class> 
<descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class> 
<services> 
<service name="InviteExternalUsersSample"> 
<specifications> 
<specification spec-id="com.adobe.edc.server.spi.ersp.InvitedUserProvider"/> 
</specifications> 
<specification-version>1.0</specification-version> 
<implementation-class>com.adobe.livecycle.samples.inviteexternalusers.provider.InviteExternalUsersSample</implementation-class> 
<auto-deploy category-id="Samples" service-id="InviteExternalUsersSample" major-version="1" minor-version="0"/> 
<operations> 
<operation name="invitedUser"> 
<input-parameter name="input" type="java.util.List" required="true"/> 
<output-parameter name="result" type="com.adobe.edc.server.spi.esrp.InvitedUserProviderResult[]"/> 
</operation> 
</operations> 
</service> 
</services> 
</component> 
```

## Empacotando o manipulador de usuários externos do convite {#packaging-invite-external-users-handler}

Para implantar o manipulador de usuários externos do convite no AEM Forms, é necessário disponibilizar o projeto Java em um arquivo JAR. Você deve garantir que os arquivos JAR externos dos quais depende a lógica comercial do manipulador de usuários externos do convite, como os arquivos `edc-server-spi.jar` e `adobe-rightsmanagement-client.jar`, também sejam incluídos no arquivo JAR. Além disso, o arquivo XML do componente deve estar presente. O arquivo `component.xml` e os arquivos JAR externos devem estar localizados na raiz do arquivo JAR.

>[!NOTE]
>
>Na ilustração abaixo, uma classe `BootstrapImpl` é mostrada. Esta seção não discute como criar uma classe `BootstrapImpl`.

A ilustração a seguir mostra o conteúdo do projeto Java empacotado no arquivo JAR do manipulador de usuários externos do convite.

![Convidar usuários](assets/ci_ci_InviteUsers.png)

A. Arquivos JAR externos exigidos pelo componente B. Arquivo JAVA

Você deve empacotar o manipulador de usuários externos do convite em um arquivo JAR. No diagrama anterior, observe que os arquivos .JAVA estão listados. Depois de compactados em um arquivo JAR, os arquivos .CLASS correspondentes também devem ser especificados. Sem os arquivos .CLASS, o manipulador de autorização não funciona.

>[!NOTE]
>
>Depois de empacotar o manipulador de autorização externo em um arquivo JAR, é possível implantar o componente no AEM Forms. Somente um manipulador de usuários externos do convite pode ser implantado em um determinado momento.

>[!NOTE]
>
>Você também pode implantar um componente de forma programática.

## Teste do manipulador de usuários externos do convite {#testing-invite-external-users-handler}

Para testar o manipulador de usuários externos do convite, é possível adicionar usuários externos para convidar usando o console de administração.

Para adicionar usuários externos para convidar usando o console de administração:

1. Implante o arquivo JAR do manipulador de usuários externos do convite usando o Workbench.
1. Reinicie o servidor de aplicativos.
1. Faça logon no console de administração.
1. Clique em **[!UICONTROL Serviços]** > **[!UICONTROL Rights Management]** > **[!UICONTROL Configuração]** > Convite **[!UICONTROL Registro de Utilizador]**.
1. Habilite o registro de usuário convidado marcando a caixa **[!UICONTROL Habilitar registro de usuário convidado]**. Em **[!UICONTROL Usar sistema de registro integrado]**, clique em **[!UICONTROL Não]**. Salve as configurações.
1. Na home page do console de administração, clique em **[!UICONTROL Settings]** > **[!UICONTROL User Management]** > **[!UICONTROL Domain Management]**.
1. Clique em **[!UICONTROL Novo Domínio Local]**. Na página a seguir, crie um domínio com o nome e o valor do identificador `EDC_EXTERNAL_REGISTERED`. Salve as alterações.
1. Na página inicial do console de administração, clique em **[!UICONTROL Services]** > **[!UICONTROL Rights Management]** > **[!UICONTROL Invited and Local Users]**. A página **[!UICONTROL Adicionar usuário convidado]** é exibida.
1. Insira endereços de email (como o manipulador de usuários externos do convite atual não envia mensagens de email, o email endereçado não precisa ser válido). Clique em **[!UICONTROL OK]**. Os usuários são convidados para o sistema.
1. Na página inicial do console de administração, clique em **[!UICONTROL Configurações]** > **[!UICONTROL Gerenciamento de usuários]** > **[!UICONTROL Usuários e grupos]**.
1. No campo **[!UICONTROL Find]**, insira um endereço de email que você especificou. Clique em **[!UICONTROL Localizar]**. O usuário convidado aparece como um usuário no domínio `EDC_EXTERNAL_REGISTERED` local.

>[!NOTE]
>
>O manipulador de usuários externos do convite falhará se o componente for interrompido ou desinstalado.
