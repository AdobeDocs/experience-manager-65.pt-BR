---
title: Gerenciar  [!DNL Adobe Stock] ativos
description: Pesquise, busque, licencie e gerencie  [!DNL Adobe Stock] ativos no  [!DNL Adobe Experience Manager]. Use os ativos licenciados como qualquer outro ativo digital.
contentOwner: Vishabh Gupta
feature: Search, Adobe Stock
role: User, Admin
exl-id: 8ec597df-bb64-4768-bf9c-e8cca4fea25b
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '2191'
ht-degree: 2%

---

# Usar [!DNL Adobe Stock] ativos em [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/aem-assets-adobe-stock.html?lang=en) |
| AEM 6.5 | Este artigo |

<!-- old content

[!DNL Experience Manager Assets] provides users the ability to search, preview, save, and license [!DNL Adobe Stock] assets directly from [!DNL Experience Manager].. 

Organizations can integrate their [!DNL Adobe Stock] enterprise plan with [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for their creative and marketing projects, with the powerful asset management capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock] service provides designers and businesses with access to millions of high-quality, curated, royalty-free photos, vectors, illustrations, videos, templates, and 3D assets for all their creative projects. [!DNL Experience Manager] users are able to quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in [!DNL Experience Manager], without leaving the [!DNL Experience Manager] interface.
-->

<!-- New overview content
-->

O serviço [!DNL Adobe Stock] fornece aos designers e empresas acesso a milhões de fotos, vetores, ilustrações, vídeos, modelos e ativos 3D de alta qualidade, com curadoria e isentos de royalties para todos os seus projetos criativos.

A oferta [!DNL Adobe Stock] para corporações, por padrão, inclui direitos de compartilhamento em toda a organização. Depois que um ativo é licenciado por um usuário da organização, outros usuários da organização podem identificar, baixar e usar esse ativo sem precisar licenciá-lo novamente. Depois que um ativo é licenciado pela sua organização, o direito de usá-lo é perpétuo.

As organizações podem integrar seu plano corporativo [!DNL Adobe Stock] ao [!DNL Experience Manager Assets] para garantir que os ativos licenciados estejam amplamente disponíveis para seus projetos criativos e de marketing, com os poderosos recursos de gerenciamento de ativos do [!DNL Experience Manager]. Os usuários do [!DNL Experience Manager] podem rapidamente encontrar, visualizar e licenciar os ativos do Adobe Stock que são salvos no [!DNL Experience Manager], sem sair da interface do [!DNL Experience Manager].

<!-- Old content
## Prerequisites {#prerequisites}

The integration requires an [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/).
-->

## Pré-requisitos para integrar [!DNL Experience Manager] e [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

O [!DNL Experience Manager Assets] fornece aos usuários a capacidade de pesquisar, visualizar, salvar e licenciar ativos do [!DNL Adobe Stock] diretamente do [!DNL Experience Manager].

Atenda aos seguintes requisitos para habilitar essa integração:

* Um plano da empresa [!DNL Adobe Stock].
* Um usuário com permissões em [!DNL Admin Console] para o perfil de produto padrão do Stock.
* Um usuário com permissões para o [!DNL Developer Access profile] para criar a integração no [!DNL Adobe Developer Console].

Um plano da empresa [!DNL Adobe Stock],

* Fornece direitos de produto para [!DNL Adobe Stock] (Estoques conectados ao Experience Manager).
* Créditos comprados em [!DNL Adobe Admin Console] para o seu direito a ações.
* Habilita o gerenciamento global de créditos e licenciamento de dentro de [!DNL Adobe Admin Console].

Dentro do direito, um perfil de produto padrão para [!DNL Adobe Stock] existe em [!DNL Admin Console]. Vários perfis podem ser criados, e esses perfis determinam quem pode licenciar os ativos do Stock. Um usuário com acesso direto ao perfil de produto pode acessar o [https://stock.adobe.com/](https://stock.adobe.com/) e licenciar os ativos do Stock. Já há outro método de usar o Developer Access para criar uma integração (API). Esta integração autentica a comunicação entre [!DNL Experience Manager Assets] e [!DNL Adobe Stock].

<!-- old content
## Integrate [!DNL Experience Manager] and [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] provides users the ability to search, preview, save, and license [!DNL Adobe Stock] assets directly from [!DNL Experience Manager].

**Prerequisites**

The integration requires: 

* An [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/)
* A user with permissions in Admin Console to the default Stock product profile
* A user with permissions to the Developer Access profile for creating integration in Adobe Developer Console

An enterprise [!DNL Adobe Stock] plan,

* Provides product entitlement for [!DNL Adobe Stock] (Stocks connected to Experience Manager)
* Credits purchased into the [!DNL Adobe Admin Console] for your stock entitlement
* Enables Service Account (JWT) authentication within [!DNL Adobe Developer Console] for your stock entitlement
* Enables managing the credits and licensing globally from within [!DNL Adobe Admin Console]

Within the entitlement, a default product profile for [!DNL Adobe Stock] exists in [!DNL Admin Console]. Multiple profiles can be created, and these profiles determines who can license Stock assets. A user having access directly to the product profile can access [https://stock.adobe.com/](https://stock.adobe.com/) and license Stock assets. Whereas there is another method of using the Developer Access to create integration (API) to authenticate communication between [!DNL Experience Manager] and [!DNL Adobe Stock].

>[!NOTE]
>
>The Stock service account (JWT) authentication comes with the enterprise Stock entitlement.
>
>The integration does not support Oauth authentication for enterprise Stock entitlement.

<!-- old content
To allow communication between [!DNL Experience Manager] and [!DNL Adobe Stock], create an IMS configuration and an [!DNL Adobe Stock] configuration in [!DNL Experience Manager].

>[!NOTE]
>
>Only [!DNL Experience Manager] administrators and [!DNL Admin Console] administrators for an organization can perform the integration as it requires administrator privileges.
-->

## Integrar [!DNL Experience Manager] e [!DNL Adobe Stock] {#integrate-adobe-stock-with-aem-assets}

Como desenvolvedor, execute as etapas a seguir para integrar o [!DNL Adobe Experience Manager] e o [!DNL Adobe Stock].

1. [Configurar um programa em [!DNL Developer Console]](#set-up-a-program-in-developer-console)
1. [Adicionar configuração na instância do autor  [!DNL AEM] &#x200B;](#add-configuration-in-the-aem-author-instance)

### Configurar um programa em [!DNL Developer Console] {#set-up-a-program-in-developer-console}

Execute as seguintes etapas para configurar um programa no [!DNL Developer Console]:
1. Navegue até [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/14431/user/servicesandapis) e faça logon em sua organização.
1. Selecione **[!UICONTROL Criar novo projeto]** disponível no painel **[!UICONTROL Projetos]**.
   ![integrar o aem assets ao adobe stock](/help/assets/assets/create-new-project-in-adobe-dev-console.png)
1. Clique em **[!UICONTROL Adicionar ao projeto]** e selecione **[!UICONTROL API]**.
1. Selecione **[!UICONTROL Adobe Stock]** e clique em **[!UICONTROL Avançar]**.
1. Especifique um **[!UICONTROL Nome da credencial]**, verifique se o **[!UICONTROL Servidor para Servidor OAuth]** está selecionado e clique em **[!UICONTROL Avançar]**.
1. Selecione **[!UICONTROL AEM Assets]** **[!UICONTROL Perfil de produto]** e clique em **[!UICONTROL Salvar API configurada]**. Uma mensagem de sucesso é exibida para confirmar que você criou um projeto no [!DNL Developer Console]. O painel do seu projeto é aberto, exibindo o nome do projeto na parte superior, **[!UICONTROL Adobe Stock]** em **[!UICONTROL APIS]** e **[!UICONTROL AEM Assets]** em **[!UICONTROL Perfil do produto]** e **[!UICONTROL Cartão de credencial OAuth de servidor para servidor]** em **[!UICONTROL Credenciais conectadas]**.
   ![integrar o aem assets e o adobe stock](/help/assets/assets/adc-project-name.png)
1. Selecione o cartão de credenciais **[!UICONTROL Servidor a Servidor OAuth]** e os **[!UICONTROL detalhes da credencial]** serão exibidos. Use estes [!DNL OAuth Server-to-Server] detalhes de credencial do seu projeto, como **[!UICONTROL ID do Cliente]**, **[!UICONTROL Segredo do Cliente]**, **[!UICONTROL Escopo]**, **[!UICONTROL Nome da Credencial]**, **[!UICONTROL ID da Conta Técnica]**, **[!UICONTROL ID da Organização]** para [adicionar configuração na instância do autor do AEM](#add-configuration-in-the-aem-author-instance).
   ![aem assets e adobe stock](/help/assets/assets/oauth-server-server-credentials-details-page.png)

### Adicionar configuração na instância do autor [!DNL AEM] {#add-configuration-in-the-aem-author-instance}

Execute as seguintes etapas para adicionar a configuração à sua instância do autor [!DNL AEM]:

1. [Configurar um novo [!DNL Adobe Stock IMS configuration] na sua [!DNL AEM] instância do autor](#set-up-adobe-stock-ims-configuration-in-aem-author-instance)
1. [Adicionar a configuração da nuvem para se conectar a  [!DNL Adobe Stock]](#add-cloud-configuration-to-connect-adobe-stock)

#### Configurar um novo [!DNL Adobe Stock IMS configuration] na sua instância de [!DNL AEM author] {#set-up-adobe-stock-ims-configuration-in-aem-author-instance}

Execute as seguintes etapas para configurar um novo [!DNL Adobe Stock IMS configuration] na sua instância do autor [!DNL AEM]:
1. Navegue até a instância do autor [!DNL AEM].
1. Clique em ![aem assets e adobe stock](/help/assets/assets/Hammer.svg), selecione **[!UICONTROL Segurança]** e selecione **[!UICONTROL Configurações do Adobe IMS]**.
1. Clique em **[!UICONTROL Criar]** para criar uma nova configuração IMS. A página **[!UICONTROL Configuração de conta técnica do Adobe IMS]** exibe vários campos, como **[!UICONTROL Solução da nuvem]**, **[!UICONTROL Título]**, **[!UICONTROL Servidor de autorização]**, **[!UICONTROL ID do cliente]**, **[!UICONTROL Segredo do cliente]**, **[!UICONTROL Escopo]** e **[!UICONTROL ID da organização]**. Siga estas instruções para especificar os detalhes nestes campos:
   * **[!UICONTROL Solução da nuvem]**: selecione **[!UICONTROL Adobe Stock]**.
   * **[!UICONTROL Título]**: especifique um nome para esta integração.
   * **[!UICONTROL Servidor de autorização]**: adicionar [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/) como o servidor de autorização.
   * **[!UICONTROL ID do Cliente]**: Navegue até o painel do projeto, clique na opção **[!UICONTROL Servidor para Servidor OAuth]** disponível no painel esquerdo, selecione **[!UICONTROL Detalhes da credencial]**, copie a **[!UICONTROL ID do Cliente]** e cole-a aqui (consulte a [etapa 7](#set-up-a-program-in-developer-console)).

   * **[!UICONTROL Segredo do Cliente]**: Navegue até o painel do projeto, clique na opção **[!UICONTROL Servidor para Servidor OAuth]** disponível no painel esquerdo, selecione **[!UICONTROL Detalhes da credencial]**, clique em **[!UICONTROL Recuperar Segredo do Cliente]**, copie o **[!UICONTROL segredo do cliente]** e cole-o aqui (consulte a [etapa 7](#set-up-a-program-in-developer-console)).

   * **[!UICONTROL Escopo]**: Navegue até o painel do projeto, clique na opção **[!UICONTROL Servidor para Servidor OAuth]** disponível no painel esquerdo, selecione **[!UICONTROL Detalhes da credencial]**, copie o **[!UICONTROL Escopo]** e cole-o aqui (consulte a [etapa 7](#set-up-a-program-in-developer-console)).

   * **[!UICONTROL ID da Organização]**: Navegue até o painel do projeto, clique na opção **[!UICONTROL Servidor para Servidor OAuth]** disponível no painel esquerdo, selecione **[!UICONTROL Detalhes da credencial]**, copie a **[!UICONTROL ID da Organização]** e cole-a aqui (consulte a [etapa 7](#set-up-a-program-in-developer-console)).
     ![aem assets e adobe stock](/help/assets/assets/adobe-ims-technical-account-configuration.png)
1. Clique em **[!UICONTROL Criar]**, a página **[!UICONTROL Configurações do Adobe IMS]** será aberta e exibirá a integração [!DNL Adobe Stock] criada.

#### Adicionar a configuração da nuvem para se conectar a [!DNL Adobe Stock] {#add-cloud-configuration-to-connect-adobe-stock}

Execute as seguintes etapas para adicionar a configuração de nuvem para se conectar ao [!DNL Adobe Stock]:

1. Navegue até a instância [!DNL AEM author].
1. Clique em ![aem assets e adobe stock](/help/assets/assets/Hammer.svg), selecione **[!UICONTROL Cloud Services]**, procure e selecione **[!UICONTROL Adobe Stock]**.
   ![usando o adobe stock com o aem](/help/assets/assets/adding-cloud-config-to-adobe-stock.png)
1. Clique em **[!UICONTROL Criar]** e a página **[!UICONTROL Configuração do Adobe Stock]** exibirá vários campos. Siga estas instruções para especificar os detalhes nestes campos:
   * **[!UICONTROL Título]**: Navegue até a página **[!UICONTROL Configuração de conta técnica do Adobe IMS]** (consulte [etapa 3](#set-up-adobe-stock-ims-configuration-in-aem-author-instance)), copie o título e cole-o aqui.
   * **[!UICONTROL Configuração IMS da Adobe Associada]**: Selecione a integração [!DNL Adobe Stock] que você criou.
   * **[!UICONTROL Local]**: Selecione **[!UICONTROL Inglês (Estados Unidos)]**.
1. Clique em **[!UICONTROL Salvar e fechar]**.
   ![usando o adobe stock com o aem](/help/assets/assets/adobe-stock-config-page.png)
<!-- old content
## Steps to integrate [!DNL Experience Manager] and [!DNL Adobe Stock] {#integration-steps}

To integrate [!DNL Experience Manager] and [!DNL Adobe Stock], perform the following steps in the listed sequence: 

1. [Obtain public certificate](#public-certificate)
   
   In [!DNL Experience Manager], create an IMS account and generate a public certificate (public key).

1. [Create service account (JWT) connection](#createnewintegration) 
   
   In [!DNL Adobe Developer Console], create a project for your [!DNL Adobe Stock] organization. Under the project, configure an API using the public key to create a service account (JWT) connection. Get the service account credentials and JWT payload information.

1. [Configure IMS account](#create-ims-account-configuration)

   In [!DNL Experience Manager], configure the IMS account using the service account credentials and JWT payload.

1. [Configure cloud service](#configure-the-cloud-service)

   In [!DNL Experience Manager], configure an [!DNL Adobe Stock] cloud service using the IMS account.


### Create an IMS configuration {#create-an-ims-configuration}

The IMS configuration authenticates your [!DNL Experience Manager Assets] author instance with the [!DNL Adobe Stock] entitlement. 

IMS configuration includes two steps:

* [Obtain public certificate](#public-certificate) 
* [Configure IMS account](#create-ims-account-configuration)

### Obtain public certificate {#public-certificate}

The public key (certificate) authenticates your product profile in Adobe Developer Console.

1. Log in to your [!DNL Experience Manager Assets] author instance. The default URL is `http://localhost:4502/aem/start.html`.

1. From the **[!UICONTROL Tools]** panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

1. In Adobe IMS Configurations page, click **[!UICONTROL Create]**. The **[!UICONTROL Adobe IMS Technical Account Configuration]** page opens. 

1. In the **[!UICONTROL Certificate]** tab, select **[!UICONTROL Adobe Stock]** from the **[!UICONTROL Cloud Solution]** dropdown list.  

1. You can create a certificate or reuse an existing certificate for the configuration. 

   To create a certificate, select the **[!UICONTROL Create new certificate]** check box and specify an **alias** for the public key. The alias serves as name of the public key. 

1. Click **[!UICONTROL Create certificate]**. Then, click **[!UICONTROL OK]** to generate the public key.

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (.crt) file on your machine. The public key is used later to configure API for your Brand Portal tenant and generate service account credentials in Adobe Developer Console.

   Click **[!UICONTROL Next]**.

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. In the **Account** tab, Adobe IMS account is created which requires the service account credentials.

   Open a new tab and [create a service account (JWT) connection in Adobe Developer Console](#createnewintegration). 

### Create service account (JWT) connection {#createnewintegration}

In Adobe Developer Console, projects and APIs are configured at organization level. Configuring an API creates a service account (JWT) connection. There are two methods to configure API, by generating a key pair (private and public keys) or by uploading a public key. In this example, the service account credentials are generated by uploading the public key.

To generate the service account credentials and JWT payload:

1. Log in to Adobe Developer Console with system administrator privileges. The default URL is [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   Ensure that you have selected the correct IMS organization (Stock entitlement) from the dropdown (organization) list.

1. Click **[!UICONTROL Create new project]**. A blank project with a system-generated name is created for your organization. 

   Click **[!UICONTROL Edit project]**. Update the **[!UICONTROL Project Title]** and **[!UICONTROL Description]**, and then click **[!UICONTROL Save]**.
   
1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL Adobe Stock]**. Click **[!UICONTROL Next]**. 

1. In the **[!UICONTROL Configure API]** window, select **[!UICONTROL Service Account (JWT)]** authentication. Click **[!UICONTROL Next]**.

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. Click **[!UICONTROL Upload your public key]**. Click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section. Click **[!UICONTROL Next]**.

1. Verify the public key and click **[!UICONTROL Next]**.

1. Select the default **[!UICONTROL Adobe Stock]** product profile and click **[!UICONTROL Save configured API]**. 

1. Once the API is configured, you are redirected to the API overview page. From the left navigation under **[!UICONTROL Credentials]**, click the **[!UICONTROL Service Account (JWT)]** option. Here, you can view the credentials and perform actions such as generate JWT tokens, copy credential details, and retrieve client secret.

1. From the **[!UICONTROL Client Credentials]** tab, copy the **[!UICONTROL client ID]**. 

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information. 

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in [!DNL Experience Manager Assets].

### Configure IMS account {#create-ims-account-configuration}

You must have the [certificate](#public-certificate) and [service account (JWT) credentials](#createnewintegration) to configure the IMS account.

To configure the IMS account: 

1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. You kept the page open while [obtaining the public certificate](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In the **[!UICONTROL Authorization Server]** field, enter the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).  

   Enter the client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

1. Click **[!UICONTROL Create]**. An IMS account configuration is created. 

   ![configure-ims-acount](assets/aem-stock-ims-config.png)
   
1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Click **[!UICONTROL Check]** in the dialog box. On successful configuration, a message appears that the *Token is retrieved successfully*.

   ![health-check](assets/aem-stock-healthcheck.png)


### Configure cloud service {#configure-the-cloud-service}

To configure the [!DNL Adobe Stock] cloud service:

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.

1. In the [!DNL Adobe Stock Configurations] page, click **[!UICONTROL Create]**.

1. Specify a **[!UICONTROL Title]** for the cloud configuration. 

   Select the IMS configuration that you have created while [configuring the IMS account](#create-ims-account-configuration).

   Select your locale from the dropdown list.

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. Click **[!UICONTROL Save & Close]**. 
 -->
Sua instância de autor [!DNL Experience Manager Assets] agora está integrada com [!DNL Adobe Stock]. Você pode criar várias configurações do [!DNL Adobe Stock] (por exemplo, configurações baseadas em localidade). Agora você pode acessar, pesquisar e licenciar os ativos do [!DNL Adobe Stock] na interface do usuário do [!DNL Experience Manager].

![ativos-de-estoque-pesquisa](assets/aem-stock-searchstocks.png)

>[!NOTE]
>
>Neste estágio da integração, somente os administradores podem acessar os ativos do [!DNL Adobe Stock], pesquisar ativos do Stock (usando omnisearch) e licenciar os ativos do [!DNL Adobe Stock].
>
>Os administradores podem adicionar usuários ou grupos ao serviço de nuvem [!DNL Adobe Stock] e conceder permissões a esses usuários não administradores no [!DNL Experience Manager] para acessar a configuração do Stock.

1. Para adicionar usuários ou grupos, selecione a configuração de nuvem [!DNL Adobe Stock] e clique em **[!UICONTROL Propriedades]**.

1. Pesquise para adicionar os usuários ou grupos aos quais você atribuiu permissões para acessar a configuração do Adobe Stock. Consulte [atribuir permissões ao grupo de usuários](#assign-permissions-to-group).


## Atribuir permissões ao grupo de usuários {#assign-permissions-to-group}

Os administradores podem criar grupos de usuários e conceder permissões a determinados usuários ou grupos para acessar o serviço de nuvem [!DNL Adobe Stock].

A seguir estão as permissões necessárias para que um usuário pesquise e licencie ativos do Adobe Stock:

* Configurar o caminho: `/conf/global/settings/stock`
* Privilégios: `jcr:read`
* Tipo de Permissão: `Allow`

Você pode criar um grupo de usuários ou atribuir permissões a um grupo de usuários existente. As permissões podem ser atribuídas pela interface [!DNL Experience Manager Assets] ou pelo Console [!DNL User Admin].

**Para fornecer acesso a um grupo de usuários a partir de [!DNL Experience Manager]:**

1. Na interface de usuário do [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Grupos]**. Criar um grupo de usuários para [!DNL Adobe Stock].

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Permissões]**.

1. Procure o grupo de usuários no painel esquerdo e adicione a nova **[!UICONTROL Entrada de Controle de Acesso (ACE)]** para o Adobe Stock.

   * Configurar o caminho: `/conf/global/settings/stock`
   * Privilégios: `jcr:read`
   * Tipo de Permissão: `Allow`

   Clique em **[!UICONTROL Adicionar]**.

   ![permissões de usuário](assets/aem-stock-user-permissions.png)

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços na Nuvem]** > **[!UICONTROL Adobe Stock]**. Selecione a configuração de nuvem [!DNL Adobe Stock] e clique em **[!UICONTROL Propriedades]**.

1. Adicione o grupo de usuários recém-criado à configuração [!DNL Adobe Stock]. Clique em **[!UICONTROL Salvar e fechar]**.

   ![atribuir-usuário](assets/aem-stock-adduser.png)

**Para fornecer acesso a um usuário a partir de [!DNL User Admin Console]:**

1. Abra o Admin Console do Usuário [!DNL Experience Manager]. A URL padrão é `http://localhost:4502/userdamin`.

1. No painel esquerdo, pesquise pelo usuário inserindo o `user_id` ou `name`. Clique duas vezes para abrir as propriedades do usuário.

1. Navegue até a guia **[!UICONTROL Permissões]** e permita `read` permissões para a configuração de nuvem [!DNL Adobe Stock]: `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >Se a configuração da nuvem não for permitida, o usuário só poderá acessar o **[!UICONTROL Assets]** na interface [!DNL Experience Manager].
   >
   >Para permitir o acesso aos ativos do [!UICONTROL Assets] e do [!DNL Adobe Stock], verifique se a configuração da nuvem é permitida para o usuário.

1. Clique em **[!UICONTROL Salvar]** para atualizar as permissões.

   ![atribuir-usuário-em-usuário-administrador](assets/aem-stock-user-admin-console.png)

1. Adicione o usuário ou grupo à configuração de nuvem [!DNL Adobe Stock].

## Acessar ativos do Adobe Stock {#access-stock-assets}

Um usuário não administrador com permissões para a configuração de nuvem do [!DNL Adobe Stock] pode pesquisar e licenciar os ativos do [!DNL Adobe Stock] na interface do [!DNL Experience Manager].

O usuário precisa executar uma etapa extra para ativar a configuração de nuvem [!DNL Adobe Stock] antes de acessar [!DNL Adobe Stock] ativos. É uma atividade única. Se o usuário tiver permissões atribuídas em várias configurações de nuvem do [!DNL Adobe Stock], ele poderá selecionar a configuração desejada nas **[!UICONTROL Preferências do Usuário]**.

Para ativar a configuração de nuvem do [!DNL Adobe Stock]:

1. Faça logon em [!DNL Experience Manager].

1. Clique no ícone do usuário no canto superior direito e em **[!UICONTROL Minhas preferências]**. A janela **[!UICONTROL Preferências do Usuário]** é aberta.

1. Selecione a **[!UICONTROL Configuração do Stock]** desejada na lista suspensa e clique em **[!UICONTROL Aceitar]** para ativar a configuração.

   ![preferências-usuário](assets/aem-stock-preferences.png)

1. Navegue até **[!UICONTROL Assets]** > **[!UICONTROL Adobe Stock]**. Agora você pode exibir, pesquisar e licenciar [!DNL Adobe Stock] ativos.

A tabela a seguir explica como as permissões de usuário funcionam ao acessar os ativos do [!DNL Adobe Stock]:

| Usuário | Grupo | Permissões | Aceitar a configuração do Stock nas Preferências do Usuário | Acessar o Assets | Acessar o Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| admin | N/A | Todos | N/A | Sim | Sim |
| test-doc1 | Usuário do DAM | /conf/global /settings/stock/cloud-config | Sim | Sim | Sim |
| test-doc1 | Usuário do DAM | /conf/global /settings/stock/cloud-config | Não | Erro: falha ao carregar dados | Não |
| test-doc1 | Usuário do DAM | **permitir**: /conf/global /settings/stock     **negar**: /cloud-config | A configuração do Stock não está visível | Sim | Não |


## Usar e gerenciar [!DNL Adobe Stock] ativos em [!DNL Experience Manager] {#usemanage}

Usando este recurso, as organizações podem permitir que seus usuários trabalhem usando os ativos do [!DNL Adobe Stock] no [!DNL Experience Manager Assets]. Na interface de usuário do [!DNL Experience Manager], os usuários podem pesquisar [!DNL Adobe Stock] ativos e licenciar os ativos necessários.

Depois que um ativo [!DNL Adobe Stock] é licenciado em [!DNL Experience Manager], ele pode ser usado e gerenciado como um ativo típico. No [!DNL Experience Manager], os usuários podem pesquisar e visualizar os ativos; copiar e publicar os ativos; compartilhar os ativos no [!DNL Brand Portal]; acessar e usar os ativos por meio do aplicativo de desktop do [!DNL Experience Manager] e assim por diante.

![Pesquise por [!DNL Adobe Stock] ativos e filtre os resultados do seu espaço de trabalho [!DNL Adobe Experience Manager]](assets/adobe-stock-search-results-workspace.png)

**A.** Pesquise ativos semelhantes aos ativos cuja ID [!DNL Adobe Stock] é fornecida. **B.** Pesquise ativos que correspondem à seleção de forma ou orientação. **C.** Pesquise por um dos tipos de ativos com suporte **D.** Abra ou recolha o painel de filtros **E.** Licencie e salve o ativo selecionado em [!DNL Experience Manager] **F.** Salve o ativo em [!DNL Experience Manager] com a marca d&#39;água **G.** Explore ativos no site [!DNL Adobe Stock] que sejam semelhantes ao ativo selecionado **H.** Exiba os ativos selecionados no site [!DNL Adobe Stock] **I.** Número de ativos selecionados dos resultados da pesquisa **J.** Alternar entre exibição de Cartão e exibição de Lista

### Localizar ativos {#find-assets}

Seus usuários do [!DNL Experience Manager], podem pesquisar por ativos no [!DNL Experience Manager] e no [!DNL Adobe Stock]. Quando o local de pesquisa não está limitado a [!DNL Adobe Stock], os resultados da pesquisa de [!DNL Experience Manager] e [!DNL Adobe Stock] são exibidos.

* Para pesquisar por [!DNL Adobe Stock] ativos, clique em **[!UICONTROL Navegação]** > **[!UICONTROL Assets]** > **[!UICONTROL Pesquisar Adobe Stock]**.

* Para pesquisar ativos em [!DNL Adobe Stock] e [!DNL Experience Manager Assets], clique em pesquisar ![pesquisar](assets/do-not-localize/search_icon.png).

Como alternativa, comece digitando `Location: Adobe Stock` na barra de pesquisa para selecionar [!DNL Adobe Stock] ativos. O [!DNL Experience Manager] oferece recursos de filtragem avançados nos ativos pesquisados, permitindo que os usuários definam rapidamente os ativos necessários usando filtros, como tipos de ativos com suporte, orientação de imagem e estado licenciado.

>[!NOTE]
>
>Assets pesquisados a partir de [!DNL Adobe Stock] são exibidos em [!DNL Experience Manager]. [!DNL Adobe Stock] ativos são buscados e armazenados no repositório do [!DNL Experience Manager] somente depois que um usuário [salva um ativo](/help/assets/aem-assets-adobe-stock.md#saveassets) ou [licencia e salva um ativo](/help/assets/aem-assets-adobe-stock.md#licenseassets). Os Assets que já estão armazenados em [!DNL Experience Manager] são exibidos e destacados para facilitar a referência e o acesso. Além disso, os ativos [!DNL Stock] são salvos com alguns metadados adicionais para indicar a origem como [!DNL Stock].

![Filtros de pesquisa em [!DNL Experience Manager] e realçou [!DNL Adobe Stock] ativos nos resultados da pesquisa](assets/aem-search-filters2.jpg)

### Salvar e exibir os ativos necessários {#saveassets}

Selecione um ativo que você deseja salvar em [!DNL Experience Manager]. Clique em [!UICONTROL Salvar] na barra de ferramentas na parte superior e forneça o nome e o local do ativo. Os ativos não licenciados são salvos localmente com uma marca d&#39;água.

Na próxima vez em que você pesquisar ativos, os ativos salvos serão destacados com uma medalha, para indicar que esses ativos estão disponíveis em [!DNL Experience Manager Assets].

>[!NOTE]
>
>Os ativos adicionados recentemente exibem um selo Novo em vez de um selo Licenciado.

### Ativos de licença {#licenseassets}

Os usuários podem licenciar [!DNL Adobe Stock] ativos usando a cota do plano corporativo [!DNL Adobe Stock]. Ao licenciar um ativo, ele é salvo sem uma marca d&#39;água e está disponível para pesquisa e uso no [!DNL Experience Manager Assets].

![Caixa de diálogo para licenciar e salvar [!DNL Adobe Stock] ativos em [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### Acessar propriedades de metadados e ativos {#access-metadata-and-asset-properties}

Os usuários podem acessar e visualizar os metadados, incluindo as propriedades de metadados [!DNL Adobe Stock] dos ativos salvos em [!DNL Experience Manager], e adicionar **[!UICONTROL Referências de licença]** para um ativo. No entanto, as atualizações da referência de licença não são sincronizadas entre o site [!DNL Experience Manager] e o site [!DNL Adobe Stock].

Os usuários podem ver as propriedades de ativos licenciados e não licenciados.

![Exibir e acessar metadados e referências de licença de ativos salvos](assets/metadata_properties.jpg)


## Limitações conhecidas {#known-limitations}

* **Problemas na integração com o [!DNL Experience Manager] Service Pack 6.5.7.0 e posterior**: um problema inesperado foi identificado durante a integração com o [!DNL Experience Manager] 6.5.7.0 e posterior. O problema está sendo testado e espera-se que esteja disponível em [!DNL Experience Manager] 6.5.11.0. Contate [!DNL Customer Support] para obter um hotfix imediato.

* A **funcionalidade para restringir usuários de licenciamento não está funcionando corretamente**: todos os usuários com `read` permissões para a configuração de estoque podem pesquisar e licenciar os ativos do [!DNL Adobe Stock].

* **Usuários não administradores precisam ativar manualmente a [!DNL Adobe Stock] configuração de nuvem**: na janela **[!UICONTROL Preferências do Usuário]**, a **[!UICONTROL Configuração do Stock]** mostra a configuração de nuvem [!DNL Adobe Stock] como habilitada, mas não funciona para um usuário não administrador. O usuário precisa clicar no botão **[!UICONTROL Aceitar]** para ativar a configuração do Stock. Na ausência desta etapa, o sistema reflete uma mensagem de erro ao acessar o **[!UICONTROL Assets]**.

* **O aviso de imagem editorial não é exibido**: ao licenciar uma imagem, os usuários não podem verificar se uma imagem é Somente para Uso Editorial. Para evitar possíveis usos indevidos, os administradores podem desativar o acesso a ativos editoriais do Admin Console.

* **Tipo de licença incorreto exibido**: é possível que um tipo de licença incorreto seja exibido em [!DNL Experience Manager] para um ativo. Os usuários podem fazer logon no site [!DNL Adobe Stock] para ver o tipo de licença.

* **Os campos de referência e os metadados não estão sincronizados**: quando um usuário atualiza um campo de referência de licença, as informações de referência de licença são atualizadas em [!DNL Experience Manager], mas não no site [!DNL Adobe Stock]. Da mesma forma, se o usuário atualizar os campos de referência no site [!DNL Adobe Stock], as atualizações não serão sincronizadas em [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Tutorial em vídeo sobre o uso de [!DNL Adobe Stock] ativos com [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] ajuda do plano da empresa](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] Perguntas frequentes](https://helpx.adobe.com/stock/faq.html)


<!--old content

### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

-->

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in [!UICONTROL User Preferences] panel. To access the panel from [!DNL Experience Manager] home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.
-->

