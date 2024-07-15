---
title: Configurar o AEM Assets com o Brand Portal
description: Saiba como configurar o AEM Assets com o Brand Portal para publicar ativos e coleções no Brand Portal.
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
docset: aem65
feature: Brand Portal
role: Admin
exl-id: ae33181c-9eec-421c-be55-4bd019de40b8
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 2a6cf0e85aace1516818ce87bc35b1b35f3da6e8
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 5%

---


# Configurar o AEM Assets com o Brand Portal {#configure-integration-65}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

O Adobe Experience Manager Assets Brand Portal permite publicar os ativos da marca aprovados do Adobe Experience Manager Assets para a Brand Portal e distribuí-los aos usuários da Brand Portal.

O AEM Assets é configurado com o Brand Portal via Adobe Developer Console, que obtém um token de conta Adobe Identity Management Services (IMS) para autorização do locatário do Brand Portal.

>[!NOTE]
>
>A configuração do AEM Assets com o Brand Portal via Adobe Developer Console é compatível com o AEM 6.5.4.0 e superior.
>
<!--
>Earlier, Brand Portal was configured via legacy OAuth Gateway, which uses the JSON Web Token (JWT) exchange to obtain an IMS Access token for authorization. 
>
>Configuration via legacy OAuth Gateway is no longer supported from April 6, 2020, and is changed to Adobe Developer Console.
-->

>[!TIP]
>
>***Somente para clientes existentes***
>
>A Adobe recomenda que você continue a usar a configuração existente do gateway OAuth herdada. Se você encontrar problemas com a configuração herdada do Gateway OAuth, exclua a configuração existente e crie uma configuração por meio do Adobe Developer Console.

<!--
This help describes the following two use-cases:

* [New configuration](#configure-new-integration-65): If you are a new Brand Portal user and want to configure your AEM Assets Author instance with Brand Portal, you can create a configuration by way of the Adobe Developer Console. 
* [Upgrade configuration](#upgrade-integration-65): If you are an existing Brand Portal user having configuration on legacy OAuth Gateway, delete the existing configuration and create a configuration by way of Adobe Developer Console.
-->
As informações fornecidas baseiam-se na suposição de que qualquer pessoa que leia esta Ajuda está familiarizada com as seguintes tecnologias:

* Instalação, configuração e administração de pacotes Adobe Experience Manager e AEM.

* Uso dos sistemas operacionais Linux® e Microsoft® Windows.

## Pré-requisitos {#prerequisites}

Você precisa do seguinte para configurar o AEM Assets com o Brand Portal:

* Uma instância ativa e em execução do AEM Assets Author com o Service Pack mais recente.
* Um URL de locatário do Brand Portal
* Um usuário com privilégios de administrador do sistema na organização IMS do locatário do Brand Portal

[Baixe e instale o AEM 6.5](#aemquickstart)

[Baixe e instale o Service Pack AEM mais recente](#servicepack)

### Baixe e instale o AEM 6.5 {#aemquickstart}

É recomendável ter o AEM 6.5 para configurar uma instância de autor AEM. Se você não tiver o AEM em execução, baixe-o dos seguintes locais:

* Se você for um cliente AEM existente, baixe AEM 6.5 do [site de Licenciamento Adobe](https://licensing.adobe.com).

* Se você for um parceiro de Adobe, use o [Programa de Treinamento de Parceiros de Adobe](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) para solicitar o AEM 6.5.

Depois de baixar o AEM, para obter instruções sobre como configurar uma instância de Autor AEM, consulte [implantação e manutenção](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html#default-local-install).

### Baixar e instalar o Service Pack mais recente do AEM {#servicepack}

Para obter instruções detalhadas, consulte as [Notas de versão atuais do Service Pack do AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=pt-BR).

**Entre em contato com o Suporte ao Cliente do Adobe** se não conseguir encontrar o pacote AEM ou o Service Pack mais recente.

## Criar configuração {#configure-new-integration-65}

>[!NOTE]
>
>Não é possível criar novas credenciais JWT a partir de junho de 2024. De agora em diante, somente as credenciais do OAuth são criadas. Consulte mais criação de uma configuração OAuth.

A configuração do AEM Assets com Brand Portal requer configurações na instância do AEM Assets Author e na Adobe Developer Console.

1. No Adobe Developer Console, crie um projeto para seu locatário do Brand Portal (organização).
1. No Experience Manager Assets, configure o serviço em nuvem da Brand Portal usando a conta IMS e o terminal Brand Portal (URL da organização).
1. Teste sua configuração publicando um ativo do Experience Manager Assets no Brand Portal.

<!--
1. In AEM Assets, create an IMS account and generate a public certificate (public key).
1. In Adobe Developer Console, create a project for your Brand Portal tenant (organization).
1. Under the project, configure an API using the public key to create a service account (JWT) connection.
1. Get the service account credentials and JWT payload information.
1. In AEM Assets, configure the IMS account using the service account credentials and JWT payload.
1. In AEM Assets, configure the Brand Portal cloud service using the IMS account and Brand Portal endpoint (organization URL).
1. Test your configuration by publishing an asset from AEM Assets to Brand Portal.
-->

>[!NOTE]
>
>Uma instância de autor do AEM Assets só deve ser configurada com um locatário do Brand Portal.

Execute as seguintes etapas na sequência listada se estiver configurando o AEM Assets com o Brand Portal pela primeira vez:

### Criar uma nova configuração {#create-new-configuration}

Execute as seguintes etapas na sequência especificada para configurar o Experience Manager Assets com o Brand Portal.

1. [Configurar as credenciais do OAuth no Adobe Developer Console](#config-oauth)
1. [Criar uma nova integração do Adobe IMS usando o OAuth](#create-ims-account-configuration)
1. [Configurar o serviço em nuvem](#configure-cloud-service)

#### Configurar as credenciais do OAuth no Adobe Developer Console {#config-oauth}

[Configure as credenciais do OAuth no Adobe Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/setting-up-ims-integrations-for-aem#credentials-in-the-developer-console) e selecione a API do Brand Portal.

#### Criar nova integração do Adobe IMS usando o OAuth {#create-ims-account-configuration}

[Crie uma nova Integração do Adobe IMS usando o OAuth](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/setting-up-ims-integrations-for-aem#creating-oauth-configuration) e selecione Brand Portal no menu suspenso.

#### Configurar o serviço em nuvem {#configure-cloud-service}

<!--
1. [Obtain a public certificate](#public-certificate)
1. [Create service account (JWT) connection](#createnewintegration) 
1. [Configure an IMS account](#create-ims-account-configuration)
1. [Configure cloud service](#configure-cloud-service)
1. [Test configuration](#test-integration)
-->
<!--
### Create IMS configuration {#create-ims-configuration}

The IMS configuration authenticates your AEM Assets Author instance with the Brand Portal tenant. 

IMS configuration includes two steps:

* [Obtain a public certificate](#public-certificate) 
* [Configure an IMS account](#create-ims-account-configuration)

### Obtain public certificate {#public-certificate}

The public key (certificate) authenticates your profile on Adobe Developer Console.

1. Log in to your AEM Assets Author instance. The default URL is `http://localhost:4502/aem/start.html`.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

1. In the Adobe IMS Configurations page, click **[!UICONTROL Create]**. It redirects to the **[!UICONTROL Adobe IMS Technical Account Configuration]** page. By default, the **Certificate** tab opens.

1. Select **[!UICONTROL Adobe Brand Portal]** in the **[!UICONTROL Cloud Solution]** dropdown list.  

1. Select the **[!UICONTROL Create new certificate]** check box and specify an **alias** for the public key. The alias serves as the name of the public key. 

1. Click **[!UICONTROL Create certificate]**. Then, click **[!UICONTROL OK]** to generate the public key.

   ![Create Certificate](assets/ims-config2.png)

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (.crt) file on your machine. 

   The public key is used later to configure the API for your Brand Portal tenant and generate service account credentials in Adobe Developer Console.

   ![Download Certificate](assets/ims-config3.png)

1. Click **[!UICONTROL Next]**. 

   In the **Account** tab, an Adobe IMS account is created which requires the service account credentials that are generated in Adobe Developer Console. Keep this page open for now.

   Open a new tab and [create a service account (JWT) connection in Adobe Developer Console](#createnewintegration) so you can get the credentials and JWT payload for configuring the IMS account. 

### Create the service account (JWT) connection {#createnewintegration}

In Adobe Developer Console, projects and APIs are configured at the Brand Portal tenant (organization) level. Configuring an API creates a service account (JWT) connection. There are two methods to configure the API, by generating a key pair (private and public keys) or by uploading a public key. To configure AEM Assets with Brand Portal, you must generate a public key (certificate) in AEM Assets and create credentials in Adobe Developer Console by uploading the public key. These credentials are required to configure the IMS account in AEM Assets. Once the IMS account is configured, you can configure the Brand Portal cloud service in AEM Assets.

To create the service account credentials and JWT payload, do the following:

1. Log in to Adobe Developer Console with system administrator privileges on the IMS organization (Brand Portal tenant). The default URL is [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Ensure that you have selected the correct IMS organization (Brand Portal tenant) from the drop-down (organization) list in the upper-right corner.

1. Click **[!UICONTROL Create new project]**. A blank project with a system-generated name is created for your organization. 

   Click **[!UICONTROL Edit project]** so you can update the **[!UICONTROL Project Title]** and **[!UICONTROL Description]**, and click **[!UICONTROL Save]**.
   
1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Next]**. 

   Ensure that you have access to the AEM Brand Portal service.

1. In the **[!UICONTROL Configure API]** window, click **[!UICONTROL Upload your public key]**. Then, click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section. 

   Click **[!UICONTROL Next]**.

   ![Upload Public Key](assets/service-account3.png)

1. Verify the public key and click **[!UICONTROL Next]**.

1. Select **[!UICONTROL Assets Brand Portal]** as the default product profile and click **[!UICONTROL Save configured API]**. 
-->
<!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->
<!--
   ![Select Product Profile](assets/service-account4.png)

1. Once the API is configured, you are redirected to the API overview page. From the left navigation under **[!UICONTROL Credentials]**, click the **[!UICONTROL Service Account (JWT)]** option.

   >[!NOTE]
   >
   >You can view the credentials and perform actions such as generate JWT tokens, copy credential details, and retrieve client secret.

1. From the **[!UICONTROL Client Credentials]** tab, copy the **[!UICONTROL client ID]**. 

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![Service Account Credentials](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information. 

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in AEM Assets.

<!--
### Create Adobe I/O integration {#createnewintegration}

Adobe I/O integration generates API Key, Client Secret, and Payload (JWT) which is required in setting up the IMS Account configurations.

1. Login to Adobe Developer Console with system administrator privileges on the IMS organization of the Brand Portal tenant.

   Default URL: [https://console.adobe.io/](https://console.adobe.io/) 

1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information that is used to create IMS account configuration.
-->
<!--
### Configure the IMS account {#create-ims-account-configuration}

Ensure that you have already performed the following steps:

* [Obtain a public certificate](#public-certificate)
* [Create service account (JWT) connection](#createnewintegration)

To configure the IMS account: 

1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. You kept the page open while [obtaining the public certificate](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In the **[!UICONTROL Authorization Server]** field, specify the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).  

   Specify client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

   Click **[!UICONTROL Create]**.

   The IMS account is configured. 

   ![IMS Account configuration](assets/create-new-integration6.png)
   
1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Click **[!UICONTROL Check]** in the dialog box. On successful configuration, a message appears that the *Token is retrieved successfully*.

   ![Healthy Configuration confirmation dialog](assets/create-new-integration5.png)

>[!CAUTION]
>
>You must have only one IMS configuration.
>
>Ensure that the IMS configuration passes the health check. If the configuration does not pass the health check, it is invalid. Delete it and create another valid configuration.
-->

1. Faça logon na sua instância do AEM Assets Author.

1. No painel **Ferramentas** ![Ferramentas](assets/do-not-localize/tools.png), navegue até **[!UICONTROL Cloud Service]** > **[!UICONTROL AEM Brand Portal]**.

1. Na página Configurações do Brand Portal, clique em **[!UICONTROL Criar]**.

1. Especifique um **[!UICONTROL Título]** para a configuração.

   Selecione a configuração IMS criada ao [configurar a conta IMS](#create-ims-account-configuration).

   No campo **[!UICONTROL URL do Serviço]**, especifique a URL do locatário (organização) da Brand Portal.

   ![Janela de configuração do Brand Portal](assets/create-cloud-service.png)

1. Clique em **[!UICONTROL Salvar e fechar]**. A configuração da nuvem é criada.

   Sua instância do autor do AEM Assets agora está configurada com o locatário do Brand Portal.

<!--

### Test and validate the configuration {#test-integration}

1. Log in to your AEM Assets cloud instance.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**.

   ![The Tools panel](assets/test-integration1.png)

1. In the Replication page, click **[!UICONTROL Agents on Author]**.

   ![Replication page](assets/test-integration2.png)

   You can see the four replication agents created for your Brand Portal tenant. 

   Locate the replication agents of your Brand Portal tenant and click the replication agent URL. 

   ![Assets replication configuration](assets/test-integration3.png)

   >[!NOTE]
   >
   >The replication agents work in parallel and share the job distribution equally, so that it increases the publishing speed by four times the original speed. After the cloud service is configured, additional configuration is not required to enable the replication agents that are activated by default to enable parallel publishing of multiple assets.

1. To verify the connection between AEM Assets and Brand Portal, click the **[!UICONTROL Test Connection]** icon.

   ![Verifying the assets replication settings](assets/test-integration4.png)

   A message appears that your *test package is successfully delivered*.

   ![Test confirmation output](assets/test-integration5.png)

1. Verify the test results on all four replication agents.


   >[!NOTE]
   >
   >Avoid disabling any of the replication agents, as it can cause the replication of the assets (running-in-queue) to fail.
   >
   >Ensure that all the four replication agents are configured to avoid timeout error. See [troubleshoot issues in parallel publishing to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout).
   >
   >Do not modify any autogenerated settings.

You can now:

* [Publish assets from AEM Assets to Brand Portal](../assets/brand-portal-publish-assets.md)
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) - Asset Sourcing in Brand Portal 
* [Publish folders from AEM Assets to Brand Portal](../assets/brand-portal-publish-folder.md)
* [Publish collections from AEM Assets to Brand Portal](../assets/brand-portal-publish-collection.md) 
* [Publish presets, schemas, and facets to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publish tags to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

See the [Brand Portal documentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) for more information.

-->
<!--
## Upgrade configuration {#upgrade-integration-65}

To upgrade your existing configurations to Adobe Developer Console, do the following steps, in the listed sequence : 

1. [Verify running jobs](#verify-jobs)
1. [Delete existing configurations](#delete-existing-configuration)
1. [Create configuration](#configure-new-integration-65)

### Verify running jobs {#verify-jobs}

Ensure that no publishing job is running on your AEM Assets Author instance before you make any edits. For that, you can verify the status of active jobs on all the four replication agents and ensure that the queues are idle.  

1. Log in to your AEM Assets Author instance.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Deployment Replication]**.

1. In the Replication page, click **[!UICONTROL Agents on Author]**.

   ![Replication agents for assets](assets/test-integration2.png)

1. Locate the replication agents of your Brand Portal tenant. 
   
   Ensure that the **Queue is Idle** for all the replication agents, and no publishing job is active. 

   ![Replication queue settings](assets/test-integration3.png)

### Delete existing configurations {#delete-existing-configuration}

Run the following checklist while deleting the existing configurations:

* Delete all four replication agents
* Delete Brand Portal cloud service
* Delete Mac user 

1. Log in to your AEM Assets Author instance and open CRX Lite as an administrator. The default URL is `http://localhost:4502/crx/de/index.jsp`.

1. Navigate to `/etc/replications/agents.author` and delete all the four replication agents of your Brand Portal tenant.

   ![Replication agent in CRXDE](assets/delete-replication-agent.png)

1. Navigate to `/etc/cloudservices/mediaportal` and delete the Brand Portal cloud service configuration.

   ![Detail of replication agent in CRXDE](assets/delete-cloud-service.png)

1. Navigate to `/home/users/mac` and delete the **Mac user** of your Brand Portal tenant.

   ![More detail of replication agent in CRXDE](assets/delete-mac-user.png)


You can now [create a configuration](#configure-new-integration-65) by way of the Adobe Developer Console on your AEM 6.5 Author instance. 
-->
