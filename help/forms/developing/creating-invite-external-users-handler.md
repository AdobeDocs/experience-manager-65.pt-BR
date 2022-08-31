---
title: Criando um Manipulador de Usuários Externos de Convite
description: Criando um Manipulador de Usuários Externos de Convite
role: Developer
exl-id: b0416716-dcc9-4f80-986a-b9660a7c8f6b
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1116'
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

## Configurar o ambiente de desenvolvimento {#setting-up-development-environment}

Para configurar seu ambiente de desenvolvimento, você deve criar um novo projeto Java, como um projeto Eclipse. A versão do Eclipse compatível é `3.2.1` ou posterior.

A SPI Rights Management requer o `edc-server-spi.jar` arquivo a ser definido no caminho da classe do seu projeto. Se você não fizer referência a esse arquivo JAR, não poderá usar o SPI do Rights Management em seu projeto Java. Esse arquivo JAR é instalado com o SDK da AEM Forms no `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi` pasta.

Além de adicionar o `edc-server-spi.jar` para o caminho de classe do seu projeto, você também deve adicionar os arquivos JAR necessários para usar a API do serviço do Rights Management. Esses arquivos são necessários para usar a API do Rights Management Service no Manipulador de Usuários Externos do Convite.

## Definir a implementação do manipulador de usuários externos do convite {#define-invite-external-users-handler}

Para desenvolver um manipulador de usuários externos do convite, você deve criar uma classe Java que implemente a variável `com.adobe.edc.server.spi.ersp.InvitedUserProvider` interface. Esta classe contém um método chamado `invitedUser`, que o serviço Rights Management chama quando endereços de email são enviados usando o **Adicionar usuários convidados** página acessível por meio do console de administração.

O `invitedUser` aceita um método `java.util.List` , que contém endereços de email do tipo string que são enviados da **Adicionar usuários convidados** página. O `invitedUser` retorna uma matriz de `InvitedUserProviderResult` objetos , que geralmente é um mapeamento de endereços de email para objetos do usuário (não retornam nulo).

>[!NOTE]
>
>Além de demonstrar como criar um manipulador de usuários externos do convite, esta seção também usa a API do AEM Forms.

A implementação do manipulador de usuários externos do convite contém um método definido pelo usuário chamado `createLocalPrincipalAccount`. Esse método aceita um valor de string que especifica um endereço de email como valor de parâmetro. O `createLocalPrincipalAccount` O método assume a pré-existência de um domínio local chamado `EDC_EXTERNAL_REGISTERED`. Você pode configurar esse nome de domínio para ser o que desejar; no entanto, para um aplicativo de produção, você pode querer integrar com um domínio empresarial.

O `createUsers` O método repete cada endereço de email e cria um objeto de Usuário correspondente (um usuário local no `EDC_EXTERNAL_REGISTERED` domínio). Finalmente, o `doEmails` é chamado. Este método é intencionalmente deixado como um stub na amostra. Em uma implementação de produção, ela conteria a lógica do aplicativo para enviar mensagens de email de convite para os usuários recém-criados. É deixado na amostra para demonstrar o fluxo lógico do aplicativo de um aplicativo real.

### Definir a implementação do manipulador de usuários externos do convite {#user-handler-implementation}

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

## Definição do arquivo XML de componente para o manipulador de autorização {#define-component-xml-authorization-handler}

Você deve definir um arquivo XML de componente para implantar o componente manipulador de usuários externos do convite. Um arquivo XML de componente existe para cada componente e fornece metadados sobre o componente.

O seguinte `component.xml` é usado para o manipulador de usuários externos do convite. Observe que o nome do serviço é `InviteExternalUsersSample` e a operação que este serviço expõe é chamada de `invitedUser`. O parâmetro de entrada é um `java.util.List` e o valor de saída é uma matriz de `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult` instâncias.

### Como definir o arquivo XML do componente para o manipulador de usuários externos do convite {#component-xml-invite-external-users-handler}

```as3
<component xmlns="https://adobe.com/idp/dsc/component/document"> 
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

Para implantar o manipulador de usuários externos do convite no AEM Forms, é necessário disponibilizar o projeto Java em um arquivo JAR. Você deve garantir que os arquivos JAR externos dos quais depende a lógica comercial do manipulador de usuários externos de convite, como o `edc-server-spi.jar` e `adobe-rightsmanagement-client.jar` os arquivos também são incluídos no arquivo JAR. Além disso, o arquivo XML do componente deve estar presente. O `component.xml` Os arquivos JAR e externos devem estar localizados na raiz do arquivo JAR.

>[!NOTE]
>
>Na ilustração abaixo, um `BootstrapImpl` é mostrada. Esta seção não discute como criar uma `BootstrapImpl` classe .

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
1. Clique em **[!UICONTROL Serviços]** > **[!UICONTROL Rights Management]** > **[!UICONTROL Configuração]** > Convidado **[!UICONTROL Registro do usuário]**.
1. Habilite o registro de usuário convidado marcando **[!UICONTROL Habilitar registro de usuário convidado]** caixa. Em **[!UICONTROL Usar o sistema de registro integrado]**, clique em **[!UICONTROL Não]**. Salve as configurações.
1. Na página inicial do console de administração, clique em **[!UICONTROL Configurações]** > **[!UICONTROL Gerenciamento de usuários]** > **[!UICONTROL Gerenciamento de domínio]**.
1. Clique em **[!UICONTROL Novo Domínio Local]**. Na página a seguir, crie um domínio com o nome e o valor do identificador de `EDC_EXTERNAL_REGISTERED`. Salve as alterações.
1. Na página inicial do console de administração, clique em **[!UICONTROL Serviços]** > **[!UICONTROL Rights Management]** > **[!UICONTROL Usuários locais e convidados]**. O **[!UICONTROL Adicionar usuário convidado]** será exibida.
1. Insira endereços de email (como o manipulador de usuários externos do convite atual não envia mensagens de email, o email endereçado não precisa ser válido). Clique em **[!UICONTROL OK]**. Os usuários são convidados para o sistema.
1. Na página inicial do console de administração, clique em **[!UICONTROL Configurações]** > **[!UICONTROL Gerenciamento de usuários]** > **[!UICONTROL Usuários e grupos]**.
1. No **[!UICONTROL Localizar]** , insira um endereço de email especificado. Clique em **[!UICONTROL Localizar]**. O usuário convidado aparece como um usuário no local `EDC_EXTERNAL_REGISTERED` domínio.

>[!NOTE]
>
>O manipulador de usuários externos do convite falhará se o componente for interrompido ou desinstalado.
