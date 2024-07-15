---
title: Criando um Manipulador de Usuários Externos para Convidar
description: Saiba como criar um Manipulador de usuários externos para convite. Ele permite que o serviço Rights Management convide usuários externos para se tornarem usuários Rights Management.
role: Developer
exl-id: b0416716-dcc9-4f80-986a-b9660a7c8f6b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---

# Criando um Manipulador de Usuários Externos para Convidar {#create-invite-external-users-handler}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

Você pode criar um Manipulador de usuários externos para o serviço Rights Management. Rights Management Um Manipulador de usuários externos para convidar usuários externos para se tornarem usuários Rights Management. Depois que um usuário se torna um usuário Rights Management, ele pode executar tarefas, como abrir um documento PDF protegido por política. Depois que o Manipulador para usuários externos do Convite é implantado no AEM Forms, você pode usar o console de administração para interagir com ele.

>[!NOTE]
>
>Um Manipulador de usuários externos para convite é um componente do AEM Forms. Antes de criar um Manipulador de usuários externos, é recomendável que você se familiarize com a criação de componentes.

**Resumo das etapas**

Para desenvolver um Handler de Usuários Externos do Convite, você deve executar as seguintes etapas:

1. Configure seu ambiente de desenvolvimento.
1. Defina a implementação do Manipulador de usuários externos do Convite.
1. Defina o arquivo XML do componente.
1. Implante o Manipulador de Usuários Externos do Convite.
1. Testar o Manipulador de usuários externos para convite.

## Configurar o ambiente de desenvolvimento {#setting-up-development-environment}

Para configurar seu ambiente de desenvolvimento, você deve criar um projeto Java, como um projeto Eclipse. A versão do Eclipse com suporte é `3.2.1` ou posterior.

O SPI do Rights Management exige que o arquivo `edc-server-spi.jar` seja definido no caminho de classe do seu projeto. Se você não fizer referência a esse arquivo JAR, não poderá usar o SPI do Rights Management no projeto Java. Este arquivo JAR está instalado com o SDK do AEM Forms na pasta `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi`.

Além de adicionar o arquivo `edc-server-spi.jar` ao caminho de classe do seu projeto, você também deve adicionar os arquivos JAR necessários para usar a API de serviço de Rights Management. Esses arquivos são necessários para usar a API do Serviço Rights Management no Manipulador de usuários externos do convite.

## Definição da implementação do manipulador de convidar usuários externos {#define-invite-external-users-handler}

Para desenvolver um manipulador de convidar usuários externos, você deve criar uma classe Java que implemente a interface `com.adobe.edc.server.spi.ersp.InvitedUserProvider`. Esta classe contém um método chamado `invitedUser`, que o serviço Rights Management invoca quando endereços de email são enviados usando a página **Adicionar Usuários Convidados**, acessível pelo console de administração.

O método `invitedUser` aceita uma instância `java.util.List`, que contém endereços de email do tipo cadeia de caracteres enviados da página **Adicionar Usuários Convidados**. O método `invitedUser` retorna uma matriz de objetos `InvitedUserProviderResult`, que geralmente é um mapeamento de endereços de email para objetos do Usuário (não retorne nulo).

>[!NOTE]
>
>Além de demonstrar como criar um manipulador para convidar usuários externos, esta seção também usa a API do AEM Forms.

A implementação do manipulador convidar usuários externos contém um método definido pelo usuário chamado `createLocalPrincipalAccount`. Este método aceita um valor de string que especifica um endereço de email como um valor de parâmetro. O método `createLocalPrincipalAccount` presume a pré-existência de um domínio local chamado `EDC_EXTERNAL_REGISTERED`. Você pode configurar esse nome de domínio como o que desejar; no entanto, para um aplicativo de produção, convém integrar a um domínio corporativo.

O método `createUsers` repete todos os endereços de email e cria um objeto Usuário correspondente (um usuário local no domínio `EDC_EXTERNAL_REGISTERED`). Finalmente, o método `doEmails` é chamado. Esse método é intencionalmente deixado como um stub na amostra. Em uma implementação de produção, ela conteria a lógica do aplicativo para enviar mensagens de email de convite para os usuários recém-criados. Ele é deixado na amostra para demonstrar o fluxo lógico da aplicação de uma aplicação real.

### Definição da implementação do manipulador de convidar usuários externos {#user-handler-implementation}

A seguinte implementação do manipulador para convidar usuários externos aceita endereços de email enviados da página Adicionar usuários convidados acessível pelo console de administração.

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

## Definição do arquivo XML do componente para o manipulador de autorização {#define-component-xml-authorization-handler}

Refinar um arquivo XML do componente para implantar o componente do manipulador de usuários externos do convite. Existe um arquivo XML componente para cada componente e ele fornece metadados sobre o componente.

O seguinte arquivo `component.xml` é usado para o manipulador de convidar usuários externos. Observe que o nome do serviço é `InviteExternalUsersSample` e a operação que esse serviço expõe é chamada `invitedUser`. O parâmetro de entrada é uma instância `java.util.List` e o valor de saída é uma matriz de instâncias `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult`.

### Definindo o arquivo XML do componente para o manipulador de convidar usuários externos {#component-xml-invite-external-users-handler}

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

## Empacotamento do manipulador de usuários externos do convite {#packaging-invite-external-users-handler}

Para implantar o manipulador convidar usuários externos para o AEM Forms, você deve empacotar o projeto Java em um arquivo JAR. Verifique se os arquivos JAR externos dos quais depende a lógica de negócios do manipulador de usuários externos do convite, como os arquivos `edc-server-spi.jar` e `adobe-rightsmanagement-client.jar`, também estão incluídos no arquivo JAR. Além disso, o componente XML file deve estar presente. O arquivo `component.xml` e os arquivos JAR externos devem estar localizados na raiz do arquivo JAR.

>[!NOTE]
>
>Na ilustração abaixo, uma classe `BootstrapImpl` é mostrada. Esta seção não discute como criar uma classe `BootstrapImpl`.

A ilustração a seguir mostra o conteúdo do projeto Java que é empacotado no arquivo JAR do manipulador de usuários externos do convite.

![Convidar usuários](assets/ci_ci_InviteUsers.png)

A. Arquivos JAR externos necessários para o componente B. Arquivo JAVA

Empacote o manipulador convidar usuários externos em um arquivo JAR. No diagrama anterior, observe que os arquivos .JAVA estão listados. Uma vez empacotado em um arquivo JAR, os arquivos .CLASS correspondentes também devem ser especificados. Sem os arquivos .CLASS, o manipulador de autorização não funciona.

>[!NOTE]
>
>Depois de criar um pacote do manipulador de autorização externa em um arquivo JAR, você pode implantar o componente no AEM Forms. Somente um manipulador de usuários externos convidados pode ser implantado em um determinado momento.

>[!NOTE]
>
>Você também pode implantar programaticamente um componente.

## Teste do manipulador para usuários externos convidados {#testing-invite-external-users-handler}

Para testar o manipulador convidar usuários externos, é possível adicionar usuários externos ao convite usando o console de administração.

Para adicionar usuários externos a convidar usando o console de administração:

1. Implante o arquivo JAR do manipulador de usuários externos do convite usando o Workbench.
1. Reinicie o servidor de aplicativos.

   >[!NOTE]
   >
   > É recomendável usar o comando &quot;Ctrl + C&quot; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

1. Faça logon no console de administração.
1. Clique em **[!UICONTROL Serviços]** > **[!UICONTROL Rights Management]** > **[!UICONTROL Configuração]** > Convidado **[!UICONTROL Registro de Usuário]**.
1. Habilite o registro de usuários convidados marcando a caixa **[!UICONTROL Habilitar registro de usuários convidados]**. Em **[!UICONTROL Usar sistema de registro interno]**, clique em **[!UICONTROL Não]**. Salve suas configurações.
1. Na home page do console de administração, clique em **[!UICONTROL Configurações]** > **[!UICONTROL Gerenciamento de Usuários]** > **[!UICONTROL Gerenciamento de Domínios]**.
1. Clique em **[!UICONTROL Novo Domínio Local]**. Na página a seguir, crie um domínio com o nome e o valor de identificador `EDC_EXTERNAL_REGISTERED`. Salve as alterações.
1. Na home page do console de administração, clique em **[!UICONTROL Serviços]** > **[!UICONTROL Rights Management]** > **[!UICONTROL Usuários Convidados e Locais]**. A página **[!UICONTROL Adicionar Usuário Convidado]** é exibida.
1. Insira endereços de email (como o manipulador de usuários externos do convite atual não envia mensagens de email, o email endereçado não precisa ser válido). Clique em **[!UICONTROL OK]**. Os usuários são convidados para o sistema.
1. Na home page do console de administração, clique em **[!UICONTROL Configurações]** > **[!UICONTROL Gerenciamento de Usuários]** > **[!UICONTROL Usuários e Grupos]**.
1. No campo **[!UICONTROL Localizar]**, digite um endereço de email especificado. Clique em **[!UICONTROL Localizar]**. O usuário que você convidou aparece como um usuário no domínio `EDC_EXTERNAL_REGISTERED` local.

>[!NOTE]
>
>O manipulador de convidar usuários externos falhará se o componente for interrompido ou desinstalado.
