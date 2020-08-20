---
title: Configurar o AEM Assets com o Brand Portal
seo-title: Configurar o AEM Assets com o Brand Portal
description: Saiba como configurar o AEM Assets com o Brand Portal para publicar ativos e coleções no Brand Portal.
seo-description: Saiba como configurar o AEM Assets com o Brand Portal para publicar ativos e coleções no Brand Portal.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: 5baef6f4d570aff738444e0620b982729b897f89
workflow-type: tm+mt
source-wordcount: '1996'
ht-degree: 13%

---


# Configurar o AEM Assets com o Brand Portal {#configure-integration-65}

Os ativos Adobe Experience Manager (AEM) são configurados com o Brand Portal via Adobe Developer Console, que obtém um token IMS para autorização do locatário do Brand Portal.

>[!NOTE]
>
>A configuração do AEM Assets com o Brand Portal via Adobe Developer Console é suportada no AEM 6.5.4.0 e superior.
>
>Anteriormente, o Brand Portal era configurado pelo gateway OAuth herdado, que usa a troca de token JWT para obter um Token de acesso IMS para autorização.
>
>A configuração por meio do gateway OAuth herdado não é mais suportada a partir de 6 de abril de 2020 e é alterada para o Console do desenvolvedor do Adobe.


>[!TIP]
>
>***Somente para clientes existentes***
>
>É recomendável continuar usando a configuração existente do gateway OAuth. Caso encontre problemas com a configuração herdada do OAuth Gateway, exclua a configuração existente e crie uma nova configuração por meio do Console do desenvolvedor do Adobe.



Esta ajuda descreve os dois casos de uso a seguir:
* [Nova configuração](#configure-new-integration-65): Se você for um novo usuário do Brand Portal e quiser configurar sua instância de autor do AEM Assets com o Brand Portal, poderá criar configuração no Adobe Developer Console.
* [Configuração](#upgrade-integration-65)de atualização: Se você já for um usuário do Brand Portal com sua instância do autor do AEM Assets configurada com o Brand Portal no gateway OAuth herdado, exclua a configuração existente e crie uma nova configuração no Adobe Developer Console.

As informações fornecidas baseiam-se no pressuposto de que qualquer pessoa que leia esta Ajuda está familiarizada com as seguintes tecnologias:

* Instalação, configuração e administração de pacotes Adobe Experience Manager e AEM.

* Usando sistemas operacionais Linux e Microsoft Windows.

## Pré-requisitos {#prerequisites}

Você precisa do seguinte para configurar o AEM Assets com o Brand Portal:

* Uma instância do autor do AEM Assets ativa e em execução com o Service Pack mais recente.
* Um URL de locatário do Brand Portal.
* Um usuário com privilégios de administrador do sistema na organização IMS do locatário do Brand Portal.


[Baixe e instale o AEM 6.5](#aemquickstart)

[Baixe e instale o AEM Service Pack mais recente](#servicepack)

### Baixe e instale o AEM 6.5 {#aemquickstart}

É recomendável ter AEM 6.5 para configurar uma instância do autor AEM. Se você não tiver AEM funcionando, baixe-o dos seguintes locais:

* Se você já for um cliente AEM, baixe o AEM 6.5 do site [de licenciamento do](http://licensing.adobe.com)Adobe.

* Se você for um parceiro de Adobe, use o Programa [de treinamento de parceiro de](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) Adobe para solicitar AEM 6.5.

Depois de baixar o AEM, para obter instruções sobre como configurar uma instância AEM do autor, consulte [implantação e manutenção](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/deploy.html#default-local-install).

### Baixe e instale AEM Service Pack mais recente {#servicepack}

Para obter instruções detalhadas, consulte

* [Notas de versão do AEM 6.5 Service Pack ](https://docs.adobe.com/content/help/en/experience-manager-65/release-notes/service-pack/sp-release-notes.html)

**Entre em contato com o Atendimento** ao cliente se não conseguir encontrar o pacote AEM ou o Service Pack mais recente.

## Criar configuração {#configure-new-integration-65}

A configuração do AEM Assets com o Brand Portal requer configurações tanto na instância do autor da AEM Assets quanto no Adobe Developer Console.

1. No AEM Assets, crie uma conta IMS e gere um certificado público (chave pública).
1. No Console do desenvolvedor do Adobe, crie um projeto para seu locatário do Brand Portal (organização).
1. No projeto, configure uma API usando a chave pública para criar uma conexão de conta de serviço (JWT).
1. Obtenha as credenciais da conta de serviço e as informações de carga JWT.
1. No AEM Assets, configure a conta IMS usando as credenciais da conta de serviço e a carga JWT.
1. No AEM Assets, configure o serviço em nuvem do Brand Portal usando a conta IMS e o terminal do Brand Portal (URL da organização).
1. Teste sua configuração publicando um ativo do AEM Assets para o Brand Portal.


>[!NOTE]
>
>Uma instância do autor da AEM Assets só deve ser configurada com um locatário do Brand Portal.



Execute as seguintes etapas na sequência listada se você estiver configurando o AEM Assets com o Brand Portal pela primeira vez:
1. [Obter certificado público](#public-certificate)
1. [Criar conexão de conta de serviço (JWT)](#createnewintegration)
1. [Configurar conta IMS](#create-ims-account-configuration)
1. [Configurar o serviço em nuvem](#configure-the-cloud-service)
1. [Testar configuração](#test-integration)

### Criar configuração IMS {#create-ims-configuration}

A configuração IMS autentica seu locatário do Brand Portal com a instância do autor do AEM Assets.

A configuração IMS inclui duas etapas:

* [Obter certificado público](#public-certificate)
* [Configurar conta IMS](#create-ims-account-configuration)

### Obter certificado público {#public-certificate}

O certificado público permite que você autentique seu perfil no Adobe Developer Console.

1. Faça logon na instância do autor do AEM Assets. O URL padrão é
   `http://localhost:4502/aem/start.html`

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

   ![Interface do usuário de configuração de conta do Adobe IMS](assets/ims-config1.png)

1. Na página Configurações de Adobe IMS, clique em **[!UICONTROL Criar]**.

1. Você é redirecionado para a página Configuração **[!UICONTROL técnica da conta do]** Adobe IMS. By default, the **Certificate** tab opens.

   Selecione a solução em nuvem Portal **[!UICONTROL da marca do]** Adobe.

1. Mark the **[!UICONTROL Create new certificate]** checkbox and specify an **alias** for the certificate. O alias atua como nome da caixa de diálogo.

1. Clique em **[!UICONTROL Criar certificado]**. Em seguida, clique em **[!UICONTROL OK]** na caixa de diálogo para gerar o certificado público.

   ![Criar certificado](assets/ims-config2.png)

1. Click **[!UICONTROL Download Public Key]** and save the certificate (.crt) file on your machine.

   O arquivo de certificado será usado posteriormente para configurar a API para o locatário do Brand Portal e gerar credenciais de conta de serviço no Console do desenvolvedor do Adobe.

   ![Baixar certificado](assets/ims-config3.png)

1. Clique em **[!UICONTROL Avançar]**.

   Na guia **Conta** , a conta Adobe IMS é criada, mas para isso você precisará das credenciais da conta de serviço geradas no Console do desenvolvedor do Adobe. Mantenha esta página aberta por enquanto.

   Abra uma nova guia e [crie uma conexão de conta de serviço (JWT) no Adobe Developer Console](#createnewintegration) para obter as credenciais e a carga JWT para configurar a conta IMS.

### Criar conexão de conta de serviço (JWT) {#createnewintegration}

No Console do desenvolvedor do Adobe, os projetos e as APIs são configurados no nível locatário (organização) do Brand Portal. Configurar uma API cria uma conexão de conta de serviço (JWT) no Console do desenvolvedor do Adobe. Há dois métodos para configurar a API, gerando um par de chaves (chaves privadas e públicas) ou carregando uma chave pública. Para configurar o AEM Assets com o Brand Portal, você deve gerar um certificado público (chave pública) no AEM Assets e criar credenciais no Adobe Developer Console fazendo upload da chave pública. Essa chave pública é usada para configurar a API para o locatário do Brand Portal selecionado e gera as credenciais e a carga JWT para a conta de serviço. Essas credenciais são usadas para configurar a conta IMS no AEM Assets. Depois que a conta IMS for configurada, você poderá configurar o serviço em nuvem do Brand Portal no AEM Assets.

Execute as seguintes etapas para gerar as credenciais da conta de serviço e a carga JWT:

1. Faça logon no Adobe Developer Console com privilégios de administrador do sistema na organização IMS (locatário do Brand Portal). O URL padrão é

   [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)


   >[!NOTE]
   >
   >Verifique se você selecionou a organização IMS correta (locatário do Brand Portal) na lista suspensa (organização) localizada no canto superior direito.

1. Click **[!UICONTROL Create new project]**. Um projeto em branco é criado para sua organização.

   Clique em **[!UICONTROL Editar projeto]** para atualizar o Título **[!UICONTROL e a]** Descrição **[!UICONTROL do]** projeto e clique em **[!UICONTROL Salvar]**.

   ![Criar projeto](assets/service-account1.png)

1. Na guia Visão geral **[!UICONTROL do]** projeto, clique em **[!UICONTROL Adicionar API]**.

   ![Adicionar API](assets/service-account2.png)

1. Na janela **** Adicionar uma API, selecione **[!UICONTROL AEM Portal]** de marca e clique em **[!UICONTROL Avançar]**.

   Verifique se você tem acesso ao serviço Portal de marcas AEM.

1. Na janela **[!UICONTROL Configurar API]** , clique em **[!UICONTROL Carregar sua chave]** pública. Em seguida, clique em **[!UICONTROL Selecionar um arquivo]** e faça upload do certificado público (arquivo .crt) que você baixou na seção [obter certificado](#public-certificate) público.

   Clique em **[!UICONTROL Avançar]**.

   ![Carregar chave pública](assets/service-account3.png)

1. Verifique o certificado público e clique em **[!UICONTROL Avançar]**.

1. Selecione o portal **[!UICONTROL de marcas dos]** ativos de perfil do produto padrão e clique em **[!UICONTROL Salvar API]** configurada.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![Selecionar Perfil do produto](assets/service-account4.png)

1. Com a API configurada, você é redirecionado para a visão geral da API. Na navegação à esquerda em **[!UICONTROL Credenciais]**, clique em **[!UICONTROL Service Account (JWT)]**.

   >[!NOTE]
   >
   >Você pode visualização as credenciais e executar outras ações (gerar tokens JWT, copiar detalhes das credenciais, recuperar o segredo do cliente e assim por diante) conforme necessário.

1. Na guia Credenciais **[!UICONTROL do]** cliente, copie a ID **[!UICONTROL do]** cliente.

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![Credenciais da Conta de Serviço](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]**.

Agora você pode usar a ID do cliente (chave da API), o segredo do cliente e a carga JWT para [configurar a conta](#create-ims-account-configuration) IMS no AEM Assets.

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

Execute as seguintes etapas para configurar a conta IMS.

1. Abra a Configuração IMS e navegue até a guia **[!UICONTROL Conta]** . Você manteve a página aberta ao [obter o certificado](#public-certificate)público.

1. Especifique um **[!UICONTROL Título]** para a conta IMS.

   No **[!UICONTROL Servidor de autorização]**, insira o URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Cole a chave **[!UICONTROL da]** API (ID do cliente), o segredo **[!UICONTROL do]** cliente e a carga **[!UICONTROL útil]** (carga JWT) que você copiou ao [criar a conexão](#createnewintegration)da conta de serviço (JWT).

   Clique em **[!UICONTROL Criar]**.

   A conta IMS está configurada.

   ![Configurar a conta IMS](assets/create-new-integration6.png)


1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Clique em **[!UICONTROL Verificar]** na caixa de diálogo. Na configuração bem-sucedida, será exibida uma mensagem informando que o *Token foi recuperado com êxito*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Você deve ter apenas uma configuração IMS.
>
>A configuração IMS deve ser aprovada na verificação de integridade. Se a configuração não for aprovada na verificação de integridade, ela será inválida. Você deve excluí-la e criar uma configuração nova e válida.



### Configurar o serviço em nuvem {#configure-the-cloud-service}

Execute as seguintes etapas para configurar o serviço em nuvem do Brand Portal:

1. Faça logon na instância do autor do AEM Assets.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. Na página Configurações do Brand Portal, clique em **[!UICONTROL Criar]**.

1. Especifique um **[!UICONTROL Título]** para a configuração.

   Selecione a configuração IMS que você criou ao [configurar a conta](#create-ims-account-configuration)IMS.

   In the **[!UICONTROL Service URL]**, enter your Brand Portal tenant (organization URL).

   ![](assets/create-cloud-service.png)

1. Clique em **[!UICONTROL Salvar e fechar]**. A configuração da nuvem é criada.

   Sua instância do autor do AEM Assets agora está configurada com o locatário do Brand Portal.

### Testar configuração{#test-integration}

Execute as seguintes etapas para validar a configuração:

1. Faça logon na instância da nuvem do AEM Assets.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**.

   ![](assets/test-integration1.png)

1. Na página Replicação, clique em **[!UICONTROL Agentes no autor]**.

   ![](assets/test-integration2.png)

1. Quatro agentes de replicação são criados para cada locatário.

   Localize os agentes de replicação do seu locatário do Brand Portal.

   Clique no URL do agente de replicação.

   ![](assets/test-integration3.png)


   >[!NOTE]
   >
   >Os agentes de replicação trabalham em paralelo e compartilham a distribuição de tarefas igualmente, aumentando assim a velocidade de publicação em quatro vezes a velocidade original. Depois que o serviço de nuvem é configurado, não é necessária uma configuração adicional para habilitar os agentes de replicação que são ativados por padrão para habilitar a publicação paralela de vários ativos.


1. Para verificar a conexão entre o AEM Assets e o Brand Portal, clique em **[!UICONTROL Testar conexão]**.

   ![](assets/test-integration4.png)

   Uma mensagem é exibida na parte inferior da página informando que seu *pacote de teste foi entregue com êxito.

   ![](assets/test-integration5.png)

1. Verifique os resultados do teste em todos os quatro agentes de replicação.


   >[!NOTE]
   >
   >Evite desativar qualquer um dos agentes de replicação. Isso pode causar falha na replicação de alguns dos ativos.

Sua instância do autor do AEM Assets foi configurada com êxito com o Brand Portal, agora você pode:

* [Publicar ativos do AEM Assets no Brand Portal](../assets/brand-portal-publish-assets.md)
* [Publicar pastas do AEM Assets no Brand Portal](../assets/brand-portal-publish-folder.md)
* [Publicar coleções do AEM Assets no Brand Portal](../assets/brand-portal-publish-collection.md)
* [Origem de ativos no Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) - Publique ativos do Brand Portal para a AEM Assets.

## Atualizar configuração {#upgrade-integration-65}

Execute as seguintes etapas na sequência listada para atualizar as configurações existentes:
1. [Verificar trabalhos em execução](#verify-jobs)
1. [Excluir configurações existentes](#delete-existing-configuration)
1. [Criar configuração](#configure-new-integration-65)

### Verificar trabalhos em execução {#verify-jobs}

Certifique-se de que nenhum trabalho de publicação esteja em execução na sua instância do autor do AEM Assets antes de fazer qualquer modificação. Para isso, você pode verificar todos os quatro agentes de replicação e garantir que as filas estejam inativas.

1. Faça logon na instância do autor do AEM Assets.

1. No painel **Ferramentas** ![Ferramentas](assets/do-not-localize/tools.png) , navegue até **[!UICONTROL Implantação]** > Replicação **[!UICONTROL de]** implantação.

1. Na página Replicação, clique em **[!UICONTROL Agentes no autor]**.

   ![](assets/test-integration2.png)

1. Localize os agentes de replicação do seu locatário do Brand Portal.

   Certifique-se de que a **Fila esteja inativa** para todos os agentes de replicação; nenhum trabalho de publicação está ativo.

   ![](assets/test-integration3.png)

### Excluir configurações existentes {#delete-existing-configuration}

Você deve executar a seguinte lista de verificação ao excluir as configurações existentes.
* Excluir todos os quatro agentes de replicação
* Excluir serviço em nuvem do Brand Portal
* Excluir usuário MAC

1. Faça logon na instância do autor da AEM Assets e abra o CRX Lite como administrador. O URL padrão é

   `http://localhost:4502/crx/de/index.jsp`

1. Navegue até `/etc/replications/agents.author` e exclua todos os quatro agentes de replicação do seu locatário do Brand Portal.

   ![](assets/delete-replication-agent.png)

1. Navegue até `/etc/cloudservices/mediaportal` e exclua a configuração **do** Cloud Service.

   ![](assets/delete-cloud-service.png)

1. Navegue até `/home/users/mac` e exclua o usuário **** MAC do seu locatário do Brand Portal.

   ![](assets/delete-mac-user.png)


Agora é possível [criar a configuração](#configure-new-integration-65) por meio do Console do desenvolvedor do Adobe na instância do autor do AEM 6.5.



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->


