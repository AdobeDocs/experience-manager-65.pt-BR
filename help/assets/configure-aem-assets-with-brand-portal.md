---
title: Configurar o AEM Assets com o Brand Portal
seo-title: Configure AEM Assets with Brand Portal
description: Saiba como configurar o AEM Assets com o Brand Portal para publicar ativos e coleções no Brand Portal.
seo-description: Learn how to configure AEM Assets with Brand Portal for publishing assets and Collections to Brand Portal.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
feature: Brand Portal
role: Admin
exl-id: ae33181c-9eec-421c-be55-4bd019de40b8
source-git-commit: d995173140237f34a03c8e84128ad9d657c9a026
workflow-type: tm+mt
source-wordcount: '2053'
ht-degree: 10%

---

# Configurar o AEM Assets com o Brand Portal {#configure-integration-65}

O Adobe Experience Manager Assets Brand Portal permite publicar ativos de marca aprovados do Adobe Experience Manager Assets no Brand Portal e distribuí-los aos usuários do Brand Portal.

O AEM Assets é configurado com o Brand Portal por meio do Adobe Developer Console, que obtém um token de conta do Adobe Identity Management Services (IMS) para autorização do locatário do Brand Portal.

>[!NOTE]
>
>A configuração do AEM Assets com Brand Portal por meio do Console do desenvolvedor do Adobe é compatível com o AEM 6.5.4.0 e superior.
>
>Anteriormente, o Brand Portal era configurado por meio do Gateway OAuth herdado, que usa a troca JSON Web Token (JWT) para obter um token de Acesso IMS para autorização.
>
>A configuração por meio do Gateway OAuth herdado não é mais compatível a partir de 6 de abril de 2020 e é alterada para Console do desenvolvedor do Adobe.

>[!TIP]
>
>***Somente para clientes existentes***
>
>É recomendável continuar usando a configuração existente do Gateway OAuth. Caso encontre problemas com a configuração herdada do Gateway OAuth, exclua a configuração existente e crie uma nova configuração por meio do Console do desenvolvedor do Adobe.

Esta ajuda descreve os dois casos de uso a seguir:

* [Nova configuração](#configure-new-integration-65): Se você for um novo usuário do Brand Portal e quiser configurar a instância do autor do AEM Assets com o Brand Portal, poderá criar a configuração por meio do Console do desenvolvedor do Adobe.
* [Atualizar configuração](#upgrade-integration-65): Se você for um usuário existente do Brand Portal com configuração no Gateway OAuth herdado, exclua a configuração existente e crie uma nova configuração por meio do Console do desenvolvedor do Adobe.

As informações fornecidas baseiam-se no pressuposto de que qualquer pessoa que leia esta Ajuda está familiarizada com as seguintes tecnologias:

* Instalação, configuração e administração de pacotes Adobe Experience Manager e AEM.

* Usando sistemas operacionais Linux e Microsoft Windows.

## Pré-requisitos {#prerequisites}

Você precisa do seguinte para configurar o AEM Assets com o Brand Portal:

* Uma instância do autor do AEM Assets ativa e em execução com o Service Pack mais recente
* Um URL de locatário do Brand Portal
* Um usuário com privilégios de administrador do sistema na organização IMS do locatário do Brand Portal

[Baixe e instale o AEM 6.5](#aemquickstart)

[Baixe e instale o AEM Service Pack mais recente](#servicepack)

### Baixe e instale o AEM 6.5 {#aemquickstart}

É recomendável ter o AEM 6.5 para configurar uma instância de autor AEM. Se você não tiver o AEM ativado e em execução, baixe-o dos seguintes locais:

* Se você for um cliente AEM existente, baixe o AEM 6.5 do [site de licenciamento do Adobe](http://licensing.adobe.com).

* Se você for um parceiro de Adobe, use [Adobe Partner Training Program](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) para solicitar AEM 6.5.

Depois de baixar o AEM, para obter instruções sobre como configurar uma instância de autor de AEM, consulte [implantar e manter](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html#default-local-install).

### Baixe e instale AEM Service Pack mais recente {#servicepack}

Para obter instruções detalhadas, consulte

* [Notas de versão do AEM 6.5 Service Pack ](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html?lang=pt-BR)

**Entre em contato com o** Suporte se não conseguir encontrar o pacote de AEM ou o Service Pack mais recente.

## Criar configuração {#configure-new-integration-65}

A configuração do AEM Assets com Brand Portal requer configurações em ambas as instâncias, na instância de autor do AEM Assets e no Console do desenvolvedor do Adobe.

1. No AEM Assets, crie uma conta IMS e gere um certificado público (chave pública).
1. No Console do desenvolvedor do Adobe, crie um projeto para seu locatário do Brand Portal (organização).
1. No projeto, configure uma API usando a chave pública para criar uma conexão de conta de serviço (JWT).
1. Obtenha as credenciais da conta de serviço e as informações de carga JWT.
1. No AEM Assets, configure a conta IMS usando as credenciais da conta de serviço e a carga JWT.
1. No AEM Assets, configure o serviço de nuvem da Brand Portal usando a conta IMS e o terminal Brand Portal (URL da organização).
1. Teste sua configuração publicando um ativo do AEM Assets para o Brand Portal.

>[!NOTE]
>
>Uma instância de autor do AEM Assets só deve ser configurada com um locatário do Brand Portal.

Execute as seguintes etapas na sequência listada se estiver configurando o AEM Assets com Brand Portal pela primeira vez:
1. [Obter certificado público](#public-certificate)
1. [Criar conexão de conta de serviço (JWT)](#createnewintegration)
1. [Configurar conta IMS](#create-ims-account-configuration)
1. [Configurar o serviço em nuvem](#configure-the-cloud-service)
1. [Testar configuração](#test-integration)

### Criar configuração IMS {#create-ims-configuration}

A configuração IMS autentica a instância do autor do AEM Assets com o locatário do Brand Portal.

A configuração IMS inclui duas etapas:

* [Obter certificado público](#public-certificate)
* [Configurar conta IMS](#create-ims-account-configuration)

### Obter certificado público {#public-certificate}

A chave pública (certificado) autentica seu perfil no Console do desenvolvedor do Adobe.

1. Faça logon na instância do autor do AEM Assets. O URL padrão é `http://localhost:4502/aem/start.html`.

1. No painel **Ferramentas** ![Ferramentas](assets/do-not-localize/tools.png), navegue até **[!UICONTROL Segurança]** > **[!UICONTROL Configurações do Adobe IMS]**.

1. Na página Configurações do Adobe IMS , clique em **[!UICONTROL Criar]**. Ele redirecionará para a página **[!UICONTROL Configuração de conta técnica do Adobe IMS]**. Por padrão, a guia **Certificate** é aberta.

1. Selecione **[!UICONTROL Adobe Brand Portal]** na lista suspensa **[!UICONTROL Cloud Solution]**.

1. Marque a caixa de seleção **[!UICONTROL Create new certificate]** e especifique um **alias** para a chave pública. O alias serve como nome da chave pública.

1. Clique em **[!UICONTROL Criar certificado]**. Em seguida, clique em **[!UICONTROL OK]** para gerar a chave pública.

   ![Criar certificado](assets/ims-config2.png)

1. Clique no ícone **[!UICONTROL Baixar chave pública]** e salve o arquivo de chave pública (.crt) no computador.

   A chave pública será usada posteriormente para configurar a API para o locatário do Brand Portal e gerar credenciais de conta de serviço no Console do desenvolvedor do Adobe.

   ![Baixar certificado](assets/ims-config3.png)

1. Clique em **[!UICONTROL Avançar]**.

   Na guia **Account**, é criada a conta Adobe IMS que requer as credenciais da conta de serviço geradas no Console do Desenvolvedor do Adobe. Mantenha esta página aberta por enquanto.

   Abra uma nova guia e [crie uma conexão de conta de serviço (JWT) no Console do Desenvolvedor do Adobe](#createnewintegration) para obter as credenciais e a carga JWT para configurar a conta IMS.

### Criar conexão de conta de serviço (JWT) {#createnewintegration}

No Console do desenvolvedor do Adobe, os projetos e as APIs são configurados no nível de locatário (organização) do Brand Portal. Configurar uma API cria uma conexão de conta de serviço (JWT). Há dois métodos para configurar a API, gerando um par de chaves (chaves privadas e públicas) ou carregando uma chave pública. Para configurar o AEM Assets com o Brand Portal, você deve gerar uma chave pública (certificado) no AEM Assets e criar credenciais no Console do desenvolvedor do Adobe fazendo upload da chave pública. Essas credenciais são necessárias para configurar a conta IMS no AEM Assets. Após configurar a conta IMS, é possível configurar o serviço de nuvem da Brand Portal no AEM Assets.

Execute as seguintes etapas para gerar as credenciais da conta de serviço e a carga JWT:

1. Faça logon no Console do desenvolvedor do Adobe com privilégios de administrador de sistema na organização IMS (locatário do Brand Portal). O URL padrão é [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Certifique-se de ter selecionado a organização IMS correta (locatário do Brand Portal) na lista suspensa (organização) localizada no canto superior direito.

1. Clique em **[!UICONTROL Criar novo projeto]**. Um projeto em branco com um nome gerado pelo sistema é criado para sua organização.

   Clique em **[!UICONTROL Editar projeto]** para atualizar o **[!UICONTROL Título do projeto]** e **[!UICONTROL Descrição]** e clique em **[!UICONTROL Salvar]**.

1. Na guia **[!UICONTROL Visão geral do projeto]**, clique em **[!UICONTROL Adicionar API]**.

1. Na janela **[!UICONTROL Adicionar uma API]**, selecione **[!UICONTROL AEM Brand Portal]** e clique em **[!UICONTROL Próximo]**.

   Certifique-se de ter acesso ao serviço AEM Brand Portal.

1. Na janela **[!UICONTROL Configure API]**, clique em **[!UICONTROL Upload your public key]**. Em seguida, clique em **[!UICONTROL Selecione um Arquivo]** e faça upload da chave pública (arquivo .crt) que você baixou na seção [obter certificado público](#public-certificate).

   Clique em **[!UICONTROL Avançar]**.

   ![Fazer upload da chave pública](assets/service-account3.png)

1. Verifique a chave pública e clique em **[!UICONTROL Next]**.

1. Selecione **[!UICONTROL Assets Brand Portal]** como o perfil de produto padrão e clique em **[!UICONTROL Salvar API configurada]**.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![Selecionar Perfil de Produto](assets/service-account4.png)

1. Depois que a API for configurada, você será redirecionado para a página de visão geral da API. Na navegação à esquerda em **[!UICONTROL Credentials]**, clique na opção **[!UICONTROL Service Account (JWT)]**.

   >[!NOTE]
   >
   >Você pode exibir as credenciais e executar ações como gerar tokens JWT, copiar detalhes da credencial, recuperar o segredo do cliente e assim por diante.

1. Na guia **[!UICONTROL Credenciais do cliente]** , copie o **[!UICONTROL ID do cliente]**.

   Clique em **[!UICONTROL Recuperar Segredo do Cliente]** e copie o **[!UICONTROL segredo do cliente]**.

   ![Credenciais da Conta de Serviço](assets/service-account5.png)

1. Navegue até a guia **[!UICONTROL Generate JWT]** e copie as informações **[!UICONTROL JWT Payload]**.

Agora você pode usar a ID do cliente (chave de API), o segredo do cliente e a carga JWT para [configurar a conta IMS](#create-ims-account-configuration) no AEM Assets.

<!--
### Create Adobe I/O integration {#createnewintegration}

Adobe I/O integration generates API Key, Client Secret, and Payload (JWT) which is required in setting up the IMS Account configurations.

1. Login to Adobe I/O Console with system administrator privileges on the IMS organization of the Brand Portal tenant.

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

   The API Key, Client Secret key, and JWT payload information will be used to create IMS account configuration.
-->

### Configurar conta IMS {#create-ims-account-configuration}

Verifique se você executou as seguintes etapas:

* [Obter certificado público](#public-certificate)
* [Criar conexão de conta de serviço (JWT)](#createnewintegration)

Execute as etapas a seguir para configurar a conta IMS.

1. Abra a Configuração IMS e navegue até a guia **[!UICONTROL Account]**. Você manteve a página aberta enquanto [obtinha o certificado público](#public-certificate).

1. Especifique um **[!UICONTROL Título]** para a conta IMS.

   No campo **[!UICONTROL Servidor de autorização]**, especifique o URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   Especifique a ID do cliente no campo **[!UICONTROL Chave da API]**, **[!UICONTROL Segredo do Cliente]** e **[!UICONTROL Carga]** (Carga JWT) que copiou enquanto [cria a conexão da conta de serviço (JWT)](#createnewintegration).

   Clique em **[!UICONTROL Criar]**.

   A conta IMS está configurada.

   ![Configurar a conta IMS](assets/create-new-integration6.png)

1. Selecione a configuração da conta IMS e clique em **[!UICONTROL Verificar integridade]**.

   Clique em **[!UICONTROL Marcar]** na caixa de diálogo. Na configuração bem-sucedida, uma mensagem é exibida informando que o token *foi recuperado com êxito*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Você deve ter apenas uma configuração IMS.
>
>A configuração IMS deve ser aprovada na verificação de integridade. Se a configuração não for aprovada na verificação de integridade, ela será inválida. Você deve excluí-la e criar uma configuração nova e válida.

### Configurar o serviço em nuvem {#configure-the-cloud-service}

Execute as seguintes etapas para configurar o serviço de nuvem do Brand Portal:

1. Faça logon na instância do autor do AEM Assets.

1. No painel **Ferramentas** ![Ferramentas](assets/do-not-localize/tools.png), navegue até **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. Na página Configurações do Brand Portal , clique em **[!UICONTROL Criar]**.

1. Especifique um **[!UICONTROL Título]** para a configuração.

   Selecione a configuração IMS que você criou ao [configurar a conta IMS](#create-ims-account-configuration).

   No campo **[!UICONTROL URL do serviço]**, especifique o URL do locatário (organização) do Brand Portal.

   ![](assets/create-cloud-service.png)

1. Clique em **[!UICONTROL Salvar e fechar]**. A configuração da nuvem é criada.

   A instância do autor do AEM Assets agora está configurada com o locatário do Brand Portal.

### Testar configuração {#test-integration}

Execute as seguintes etapas para validar a configuração:

1. Faça logon na instância da nuvem do AEM Assets.

1. No painel **Ferramentas** ![Ferramentas](assets/do-not-localize/tools.png), navegue até **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]**.

   ![](assets/test-integration1.png)

1. Na página Replicação , clique em **[!UICONTROL Agentes no autor]**.

   ![](assets/test-integration2.png)

   Você pode ver os quatro agentes de replicação criados para o seu locatário do Brand Portal.

   Localize os agentes de replicação do seu locatário do Brand Portal e clique no URL do agente de replicação.

   ![](assets/test-integration3.png)

   >[!NOTE]
   >
   >Os agentes de replicação trabalham em paralelo e compartilham a distribuição de tarefas igualmente, aumentando assim a velocidade de publicação em quatro vezes a velocidade original. Depois que o serviço de nuvem é configurado, não é necessária configuração adicional para habilitar os agentes de replicação que são ativados por padrão para habilitar a publicação paralela de vários ativos.

1. Para verificar a conexão entre o AEM Assets e o Brand Portal, clique no ícone **[!UICONTROL Testar conexão]**.

   ![](assets/test-integration4.png)

   Aparece uma mensagem de que seu *pacote de teste foi entregue com êxito*.

   ![](assets/test-integration5.png)

1. Verifique os resultados do teste em todos os quatro agentes de replicação.


   >[!NOTE]
   >
   >Evite desabilitar qualquer um dos agentes de replicação, pois isso pode causar falha na replicação dos ativos (em execução na fila).
   >
   >Certifique-se de que todos os quatro agentes de replicação estejam configurados para evitar o erro de tempo limite. Consulte [solucionar problemas na publicação paralela no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout).
   >
   >Não modifique configurações geradas automaticamente.

Agora você pode:

* [Publicar ativos do AEM Assets no Brand Portal](../assets/brand-portal-publish-assets.md)
* [Publicar ativos do Brand Portal no AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html)  - Origem de ativos no Brand Portal
* [Publicar pastas do AEM Assets no Brand Portal](../assets/brand-portal-publish-folder.md)
* [Publicar coleções do AEM Assets no Brand Portal](../assets/brand-portal-publish-collection.md)
* [Publicar predefinições, esquemas e aspectos no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicar marcações no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

Consulte a [documentação do Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para obter mais informações.


## Atualizar configuração {#upgrade-integration-65}

Execute as seguintes etapas na sequência listada para atualizar suas configurações existentes para o Console do desenvolvedor do Adobe:
1. [Verificar trabalhos em execução](#verify-jobs)
1. [Excluir configurações existentes](#delete-existing-configuration)
1. [Criar configuração](#configure-new-integration-65)

### Verificar trabalhos em execução {#verify-jobs}

Certifique-se de que nenhum trabalho de publicação esteja em execução na instância do autor do AEM Assets antes de fazer qualquer modificação. Para isso, você pode verificar o status de trabalhos ativos em todos os quatro agentes de replicação e garantir que as filas estejam inativas.

1. Faça logon na instância do autor do AEM Assets.

1. No painel **Ferramentas** ![Ferramentas](assets/do-not-localize/tools.png), navegue até **[!UICONTROL Implantação]** > **[!UICONTROL Replicação de Implantação]**.

1. Na página Replicação , clique em **[!UICONTROL Agentes no autor]**.

   ![](assets/test-integration2.png)

1. Localize os agentes de replicação do seu locatário do Brand Portal.

   Certifique-se de que a **Fila esteja inativa** para todos os agentes de replicação, nenhum trabalho de publicação está ativo.

   ![](assets/test-integration3.png)

### Excluir configurações existentes {#delete-existing-configuration}

Você deve executar a seguinte lista de verificação ao excluir as configurações existentes:
* Excluir todos os quatro agentes de replicação
* Excluir o serviço em nuvem Brand Portal
* Excluir usuário MAC

1. Faça logon na instância de autor do AEM Assets e abra o CRX Lite como administrador. O URL padrão é `http://localhost:4502/crx/de/index.jsp`.

1. Navegue até `/etc/replications/agents.author` e exclua todos os quatro agentes de replicação do seu locatário do Brand Portal.

   ![](assets/delete-replication-agent.png)

1. Navegue até `/etc/cloudservices/mediaportal` e exclua a configuração do serviço de nuvem do Brand Portal.

   ![](assets/delete-cloud-service.png)

1. Navegue até `/home/users/mac` e exclua o **usuário MAC** do seu locatário do Brand Portal.

   ![](assets/delete-mac-user.png)


Agora você pode [criar configuração](#configure-new-integration-65) por meio do Console do desenvolvedor do Adobe na instância do autor do AEM 6.5.



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
