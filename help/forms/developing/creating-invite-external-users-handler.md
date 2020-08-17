---
title: Criando um Manipulador de Usuários Externos de Convite
description: Criando um Manipulador de Usuários Externos de Convite
translation-type: tm+mt
source-git-commit: 92e5cc0b1934dad641357a22894e70a3660b774a
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 0%

---


# Criando um Manipulador de Usuários Externos de Convite {#create-invite-external-users-handler}

Você pode criar um Manipulador de convidados para usuários externos para o serviço Rights Management. Um Manipulador de Usuários Externos de Convite permite que o serviço Rights Management convide usuários externos a se tornarem usuários do Rights Management. Depois que um usuário se torna Rights Management, ele é capaz de executar tarefas, como abrir um documento PDF protegido por política. Depois que o Manipulador de Usuários Externos de Convite for implantado na AEM Forms, você poderá usar o console de administração para interagir com ele.

>[!NOTE]
>
>Um Manipulador de Usuários Externos de Convite é um componente AEM Forms. Antes de criar um Manipulador de Usuários Externos de Convite, recomenda-se que você se familiarize com a criação de componentes.

**Resumo das etapas**

Para desenvolver um Manipulador de Usuários Externos de Convite, execute as seguintes etapas:

1. Configure seu ambiente de desenvolvimento.
1. Defina a implementação Convidar usuários externos para o Manipulador.
1. Defina o arquivo XML do componente.
1. Implante o Manipulador Convidar usuários externos.
1. Teste o Manipulador de convidados para usuários externos.

## Configuração do seu ambiente de desenvolvimento {#setting-up-development-environment}

Para configurar seu ambiente de desenvolvimento, você deve criar um novo projeto Java, como um projeto Eclipse. A versão do Eclipse compatível é `3.2.1` ou posterior.

O Rights Management SPI requer que o `edc-server-spi.jar` arquivo seja definido no caminho de classe do seu projeto. Se você não fizer referência a esse arquivo JAR, não poderá usar o Rights Management SPI em seu projeto Java. Esse arquivo JAR é instalado com o SDK do AEM Forms na `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi` pasta.

Além de adicionar o `edc-server-spi.jar` arquivo ao caminho de classe do seu projeto, você também deve adicionar os arquivos JAR necessários para usar a API de serviço de Rights Management. Esses arquivos são necessários para usar a API de serviço de Rights Management dentro do Manipulador de Usuários Externos do Convite.

## Definição da implementação do manipulador de usuários externos do convite {#define-invite-external-users-handler}

Para desenvolver um manipulador de usuários externos de convite, é necessário criar uma classe Java que implemente a `com.adobe.edc.server.spi.ersp.InvitedUserProvider` interface. Essa classe contém um método chamado `invitedUser`, que o serviço Rights Management chama quando endereços de email são enviados usando a página **Adicionar usuários** convidados acessível por meio do console de administração.

O `invitedUser` método aceita uma `java.util.List` instância, que contém endereços de email com caracteres digitados que são enviados da página **Adicionar usuários** convidados. O `invitedUser` método retorna uma matriz de `InvitedUserProviderResult` objetos, que geralmente é um mapeamento de endereços de email para objetos de Usuário (não retorna nulo).

>[!NOTE]
>
>Além de demonstrar como criar um manipulador de usuários externos de convite, esta seção também usa a API do AEM Forms.

A implementação do manipulador de usuários externos do convite contém um método definido pelo usuário chamado `createLocalPrincipalAccount`. Esse método aceita um valor de string que especifica um endereço de email como valor de parâmetro. O `createLocalPrincipalAccount` método assume a preexistência de um domínio local chamado `EDC_EXTERNAL_REGISTERED`. Você pode configurar esse nome de domínio para ser qualquer coisa que desejar; no entanto, para um aplicativo de produção, talvez você queira se integrar a um domínio corporativo.

O `createUsers` método repete cada endereço de email e cria um objeto de usuário correspondente (um usuário local no `EDC_EXTERNAL_REGISTERED` domínio). Finalmente, o `doEmails` método é chamado. Este método é intencionalmente deixado como um stub na amostra. Em uma implementação de produção, conteria a lógica do aplicativo para enviar mensagens de email de convite aos usuários recém-criados. É deixado na amostra para demonstrar o fluxo lógico do aplicativo de um aplicativo real.

### Definição da implementação do manipulador de usuários externos do convite {#user-handler-implementation}

A implementação do manipulador de convidados para usuários externos a seguir aceita endereços de email enviados da página Adicionar usuários convidados acessíveis por meio do console de administração.

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

## Definição do arquivo XML de componente para o manipulador de autorização {#define-component-xml-authorization-handler}

Você deve definir um arquivo XML de componente para implantar o componente gerenciador de usuários externos do convite. Existe um arquivo XML de componente para cada componente e fornece metadados sobre o componente.

O seguinte `component.xml` arquivo é usado para o manipulador de usuários externos do convite. Observe que o nome do serviço é `InviteExternalUsersSample` e a operação que este serviço expõe é chamada `invitedUser`. O parâmetro input é uma `java.util.List` instância e o valor de saída é uma matriz de `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult` instâncias.

### Definição do arquivo XML de componente para o manipulador de usuários externos do convite {#component-xml-invite-external-users-handler}

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

## Como empacotar o manipulador de usuários externos do convite {#packaging-invite-external-users-handler}

Para implantar o manipulador de usuários externos do convite na AEM Forms, é necessário disponibilizar seu projeto Java em um arquivo JAR. Você deve garantir que os arquivos JAR externos dos quais depende a lógica comercial do manipulador de usuários externos do convite, como os arquivos `edc-server-spi.jar` e `adobe-rightsmanagement-client.jar` os arquivos, também sejam incluídos no arquivo JAR. Além disso, o arquivo XML do componente deve estar presente. O arquivo `component.xml` e os arquivos JAR externos devem estar localizados na raiz do arquivo JAR.

>[!NOTE]
>
>Na ilustração abaixo, uma `BootstrapImpl` classe é mostrada. Esta seção não discute como criar uma `BootstrapImpl` classe.

A ilustração a seguir mostra o conteúdo do projeto Java empacotado no arquivo JAR do manipulador de usuários externos do convite.

![Convidar usuários](assets/ci_ci_InviteUsers.png)

A. Arquivos JAR externos exigidos pelo componente B. Arquivo JAVA

Você deve disponibilizar o manipulador de usuários externos do convite em um arquivo JAR. No diagrama anterior, observe que os arquivos .JAVA estão listados. Depois de compactados em um arquivo JAR, os arquivos .CLASS correspondentes também devem ser especificados. Sem os arquivos .CLASS, o manipulador de autorização não funciona.

>[!NOTE]
>
>Depois de disponibilizar o manipulador de autorização externo em um arquivo JAR, é possível implantar o componente na AEM Forms. Somente um manipulador de usuários externos de convite pode ser implantado em um determinado momento.

>[!NOTE]
>
>Também é possível implantar um componente de forma programática.

## Testando o manipulador de usuários externos do convite {#testing-invite-external-users-handler}

Para testar o manipulador de usuários externos do convite, você pode adicionar usuários externos para convidar usando o console de administração.

Para adicionar usuários externos para convidar usando o console de administração:

1. Implante o arquivo JAR do manipulador de usuários externos do convite usando o Workbench.
1. Reinicie o servidor de aplicativos.
1. Faça logon no console de administração.
1. Clique em **[!UICONTROL Serviços]** > **[!UICONTROL Rights Management]** > **[!UICONTROL Configuração]** > Registro **[!UICONTROL de]** usuário convidado.
1. Habilite o registro de usuário convidado marcando a caixa **[!UICONTROL Habilitar registro]** de usuário convidado. Em **[!UICONTROL Usar sistema]** de registro integrado, clique em **[!UICONTROL Não]**. Salve suas configurações.
1. No home page do console de administração, clique em **[!UICONTROL Configurações]** > Gerenciamento **** do usuário > Gerenciamento **[!UICONTROL de]** domínio.
1. Clique em **[!UICONTROL Novo domínio]** local. Na página a seguir, crie um domínio com o nome e o valor do identificador de `EDC_EXTERNAL_REGISTERED`. Salve as alterações.
1. No home page do console de administração, clique em **[!UICONTROL Serviços]** > **[!UICONTROL Rights Management]** > Usuários **** convidados e locais. A página **[!UICONTROL Adicionar usuário]** convidado é exibida.
1. Insira endereços de email (como o manipulador de usuários externos do convite atual não envia mensagens de email, o email endereçado não precisa ser válido). Clique em **[!UICONTROL OK]**. Os usuários são convidados para o sistema.
1. No home page do console de administração, clique em **[!UICONTROL Configurações]** > Gerenciamento **** do usuário > **[!UICONTROL Usuários e grupos]**.
1. No campo **[!UICONTROL Localizar]** , digite um endereço de email que você especificou. Clique em **[!UICONTROL Localizar]**. O usuário convidado aparece como um usuário no `EDC_EXTERNAL_REGISTERED` domínio local.

>[!NOTE]
>
>O manipulador de usuários externos do convite falhará se o componente for interrompido ou desinstalado.
