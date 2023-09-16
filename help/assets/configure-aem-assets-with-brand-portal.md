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
source-git-commit: b00ed4ed146b89aece9af1d267c890a360a236e9
workflow-type: tm+mt
source-wordcount: '2130'
ht-degree: 10%

---


# Configurar o AEM Assets com o Brand Portal {#configure-integration-65}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

O Adobe Experience Manager Assets Brand Portal permite publicar os ativos da marca aprovados do Adobe Experience Manager Assets na Brand Portal e distribuí-los aos usuários da Brand Portal.

O AEM Assets é configurado com o Brand Portal por meio do Adobe Developer Console, que obtém um token de conta Adobe Identity Management Services (IMS) para autorização do locatário do Brand Portal.

>[!NOTE]
>
>A configuração do AEM Assets com o Console do Adobe Developer AEM é compatível com o Brand Portal 6.5.4.0 e superior.
>
>Anteriormente, o Brand Portal era configurado por meio do Gateway OAuth herdado, que usa a troca do JSON Web Token (JWT) para obter um token de acesso IMS para autorização.
>
>A configuração por meio do gateway OAuth herdado não é mais compatível a partir de 6 de abril de 2020 e foi alterada para o Console do Adobe Developer.

>[!TIP]
>
>***Somente para clientes existentes***
>
>A Adobe recomenda que você continue a usar a configuração existente do gateway OAuth herdada. Se você encontrar problemas com a configuração herdada do Gateway OAuth, exclua a configuração existente e crie uma configuração por meio do Console do Adobe Developer.

Esta ajuda descreve os dois casos de uso a seguir:

* [Nova configuração](#configure-new-integration-65): se você for um novo usuário do Brand Portal e quiser configurar sua instância do AEM Assets Author com o Brand Portal, poderá criar uma configuração por meio do Console do Adobe Developer.
* [Configuração de atualização](#upgrade-integration-65): se você for um usuário existente do Brand Portal com configuração no Gateway OAuth herdado, exclua a configuração existente e crie uma configuração por meio do Console do Adobe Developer.

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

* Se você for um cliente do AEM, baixe o AEM 6.5 da [Site de licenciamento do Adobe](https://licensing.adobe.com).

* Se você for um parceiro de Adobe, use o [Programa de treinamento para parceiros Adobe](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) para solicitar o AEM 6.5.

Depois de baixar o AEM, para obter instruções sobre como configurar uma instância de autor AEM, consulte [implantação e manutenção](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html#default-local-install).

### Baixar e instalar o Service Pack mais recente do AEM {#servicepack}

Para obter instruções detalhadas, consulte a tabela [Notas de versão do AEM 6.5 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=pt-BR).

**Entre em contato com o Suporte ao cliente do Adobe** se você não conseguir encontrar o pacote AEM ou o Service Pack mais recente.

## Criar configuração {#configure-new-integration-65}

A configuração do AEM Assets com Brand Portal requer configurações na instância do AEM Assets Author e no Console do Adobe Developer.

1. No AEM Assets, crie uma conta IMS e gere um certificado público (chave pública).
1. No Console do Adobe Developer, crie um projeto para seu locatário do Brand Portal (organização).
1. No projeto, configure uma API usando a chave pública para criar uma conexão de conta de serviço (JWT).
1. Obtenha as credenciais da conta de serviço e as informações de carga JWT.
1. No AEM Assets, configure a conta IMS usando as credenciais da conta de serviço e a carga JWT.
1. No AEM Assets, configure o serviço em nuvem da Brand Portal usando a conta IMS e o terminal Brand Portal (URL da organização).
1. Teste sua configuração publicando um ativo do AEM Assets no Brand Portal.

>[!NOTE]
>
>Uma instância de autor do AEM Assets só deve ser configurada com um locatário do Brand Portal.

Execute as seguintes etapas na sequência listada se estiver configurando o AEM Assets com o Brand Portal pela primeira vez:

1. [Obter um certificado público](#public-certificate)
1. [Criar conexão de conta de serviço (JWT)](#createnewintegration)
1. [Configurar uma conta IMS](#create-ims-account-configuration)
1. [Configurar o serviço em nuvem](#configure-the-cloud-service)
1. [Testar configuração](#test-integration)

### Criar configuração IMS {#create-ims-configuration}

A configuração IMS autentica sua instância do AEM Assets Author com o locatário do Brand Portal.

A configuração IMS inclui duas etapas:

* [Obter um certificado público](#public-certificate)
* [Configurar uma conta IMS](#create-ims-account-configuration)

### Obter certificado público {#public-certificate}

A chave pública (certificado) autentica seu perfil no Console do Adobe Developer.

1. Faça logon na sua instância do AEM Assets Author. O URL padrão é `http://localhost:4502/aem/start.html`.

1. No **Ferramentas** ![Ferramentas](assets/do-not-localize/tools.png) , navegue até **[!UICONTROL Segurança]** > **[!UICONTROL Configurações do Adobe IMS]**.

1. Na página Configurações do Adobe IMS, clique em **[!UICONTROL Criar]**. Ele redireciona para a guia **[!UICONTROL Configurações da conta técnica do Adobe IMS]** página. Por padrão, a variável **Certificado** é aberta.

1. Selecionar **[!UICONTROL Adobe Brand Portal]** no **[!UICONTROL Solução em nuvem]** lista suspensa.

1. Selecione o **[!UICONTROL Criar novo certificado]** e especifique um **alias** para a chave pública. O alias serve como o nome da chave pública.

1. Clique em **[!UICONTROL Criar certificado]**. Em seguida, clique em **[!UICONTROL OK]** para gerar a chave pública.

   ![Criar certificado](assets/ims-config2.png)

1. Clique em **[!UICONTROL Baixar chave pública]** e salve o arquivo de chave pública (.crt) em sua máquina.

   A chave pública é usada posteriormente para configurar a API do locatário do Brand Portal e gerar credenciais de conta de serviço no Adobe Developer Console.

   ![Baixar certificado](assets/ims-config3.png)

1. Clique em **[!UICONTROL Avançar]**.

   No **Conta** , uma conta do Adobe IMS é criada e requer as credenciais da conta de serviço geradas no Console do Adobe Developer. Mantenha esta página aberta por enquanto.

   Abra uma nova guia e [criar uma conexão de conta de serviço (JWT) no console do Adobe Developer](#createnewintegration) para obter as credenciais e a carga JWT para configurar a conta do IMS.

### Criar a conexão da conta de serviço (JWT) {#createnewintegration}

No Console do Adobe Developer, os projetos e as APIs são configurados no nível do locatário do Brand Portal (organização). Configurar uma API cria uma conexão de conta de serviço (JWT). Há dois métodos para configurar a API: eles geram um par de chaves (chaves privadas e públicas) ou fazem upload de uma chave pública. Para configurar o AEM Assets com o Brand Portal, você deve gerar uma chave pública (certificado) no AEM Assets e criar credenciais no Console do Adobe Developer fazendo upload da chave pública. Essas credenciais são necessárias para configurar a conta do IMS no AEM Assets. Depois que a conta IMS é configurada, você pode configurar o serviço de nuvem da Brand Portal no AEM Assets.

Para criar as credenciais da conta de serviço e a carga JWT, faça o seguinte:

1. Faça logon no Console do Adobe Developer com privilégios de administrador de sistema na organização IMS (locatário do Brand Portal). O URL padrão é [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Verifique se você selecionou a organização IMS correta (locatário do Brand Portal) na lista suspensa (organização) no canto superior direito.

1. Clique em **[!UICONTROL Criar novo projeto]**. Um projeto em branco com um nome gerado pelo sistema é criado para sua organização.

   Clique em **[!UICONTROL Editar projeto]** para que você possa atualizar o **[!UICONTROL Título do projeto]** e **[!UICONTROL Descrição]** e clique em **[!UICONTROL Salvar]**.

1. No **[!UICONTROL Visão geral do projeto]** clique em **[!UICONTROL Adicionar API]**.

1. No **[!UICONTROL Adicionar uma janela de API]**, selecione **[!UICONTROL AEM Brand Portal]** e clique em **[!UICONTROL Próxima]**.

   Verifique se você tem acesso ao serviço do AEM Brand Portal.

1. No **[!UICONTROL Configurar API]** clique em **[!UICONTROL Fazer upload da sua chave pública]**. Em seguida, clique em **[!UICONTROL Selecionar um arquivo]** e faça upload da chave pública (arquivo .crt) que você baixou na [obter certificado público](#public-certificate) seção.

   Clique em **[!UICONTROL Avançar]**.

   ![Fazer upload da chave pública](assets/service-account3.png)

1. Verifique a chave pública e clique em **[!UICONTROL Próxima]**.

1. Selecionar **[!UICONTROL Assets Brand Portal]** como o perfil de produto padrão e clique em **[!UICONTROL Salvar API configurada]**.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![Selecionar perfil de produto](assets/service-account4.png)

1. Após configurar a API, você é redirecionado para a página Visão geral da API. Na navegação à esquerda, em **[!UICONTROL Credenciais]**, clique no link **[!UICONTROL Conta de serviço (JWT)]** opção.

   >[!NOTE]
   >
   >Você pode exibir as credenciais e executar ações, como gerar tokens JWT, copiar detalhes da credencial e recuperar segredo do cliente.

1. No **[!UICONTROL Credenciais do cliente]** , copie o **[!UICONTROL ID do cliente]**.

   Clique em **[!UICONTROL Recuperar segredo do cliente]** e copie o **[!UICONTROL segredo do cliente]**.

   ![Credenciais da Conta de Serviço](assets/service-account5.png)

1. Navegue até a **[!UICONTROL Gerar JWT]** e copie a guia **[!UICONTROL Carga JWT]** informações.

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

### Configurar a conta IMS {#create-ims-account-configuration}

Verifique se você já executou as seguintes etapas:

* [Obter um certificado público](#public-certificate)
* [Criar conexão de conta de serviço (JWT)](#createnewintegration)

Para configurar a conta IMS:

1. Abra a Configuração IMS e navegue até o **[!UICONTROL Conta]** guia. Você manteve a página aberta enquanto [obtenção do certificado público](#public-certificate).

1. Especifique um **[!UICONTROL Título]** para a conta IMS.

   No **[!UICONTROL Servidor de autorização]** especifique o URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   Especifique a ID do cliente no **[!UICONTROL Chave de API]** campo, **[!UICONTROL Segredo do cliente]**, e **[!UICONTROL Carga]** (carga JWT) que você copiou enquanto [criação da conexão da conta de serviço (JWT)](#createnewintegration).

   Clique em **[!UICONTROL Criar]**.

   A conta IMS está configurada.

   ![Configurar a conta IMS](assets/create-new-integration6.png)

1. Selecione a configuração da conta IMS e clique em **[!UICONTROL Verificar integridade]**.

   Clique em **[!UICONTROL Marcar]** na caixa de diálogo. Na configuração bem-sucedida, é exibida a mensagem de que a variável *O token foi recuperado com sucesso*.

   ![Caixa de diálogo de confirmação Configuração íntegra](assets/create-new-integration5.png)

>[!CAUTION]
>
>Você deve ter apenas uma configuração IMS.
>
>A configuração IMS deve ser aprovada na verificação de integridade. Se a configuração não for aprovada na verificação de integridade, ela será inválida. Exclua-a e crie outra configuração válida.

### Configurar o serviço em nuvem Brand Portal {#configure-the-cloud-service}

1. Faça logon na sua instância do AEM Assets Author.

1. No **Ferramentas** ![Ferramentas](assets/do-not-localize/tools.png) , navegue até **[!UICONTROL Cloud Service]** > **[!UICONTROL AEM Brand Portal]**.

1. Na página Configurações do Brand Portal, clique em **[!UICONTROL Criar]**.

1. Especifique um **[!UICONTROL Título]** para a configuração.

   Selecione a configuração IMS criada enquanto [configuração da conta IMS](#create-ims-account-configuration).

   No **[!UICONTROL URL do serviço]** especifique o URL do locatário (organização) do Brand Portal.

   ![Janela Configuração do Brand Portal](assets/create-cloud-service.png)

1. Clique em **[!UICONTROL Salvar e fechar]**. A configuração da nuvem é criada.

   Sua instância do autor do AEM Assets agora está configurada com o locatário do Brand Portal.

### Testar e validar a configuração {#test-integration}

1. Faça logon na instância da nuvem do AEM Assets.

1. No **Ferramentas** ![Ferramentas](assets/do-not-localize/tools.png) , navegue até **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]**.

   ![O painel Ferramentas](assets/test-integration1.png)

1. Na página Replicação, clique em **[!UICONTROL Agentes sobre o autor]**.

   ![Página Replicação](assets/test-integration2.png)

   Você pode ver os quatro agentes de replicação criados para seu locatário do Brand Portal.

   Localize os agentes de replicação do seu locatário do Brand Portal e clique no URL do agente de replicação.

   ![Configuração de replicação de ativos](assets/test-integration3.png)

   >[!NOTE]
   >
   >Os agentes de replicação funcionam em paralelo e compartilham a distribuição de tarefas igualmente, de modo que aumentam a velocidade de publicação em quatro vezes a velocidade original. Após a configuração do Cloud Service, não é necessária uma configuração adicional para habilitar os agentes de replicação ativados por padrão para permitir a publicação paralela de vários ativos.

1. Para verificar a conexão entre o AEM Assets e o Brand Portal, clique no link **[!UICONTROL Testar conexão]** ícone.

   ![Verificar as configurações de replicação de ativos](assets/test-integration4.png)

   Será exibida uma mensagem informando que o *o pacote de teste foi entregue com sucesso*.

   ![Saída de confirmação de teste](assets/test-integration5.png)

1. Verifique os resultados do teste em todos os quatro agentes de replicação.


   >[!NOTE]
   >
   >Evite desativar qualquer um dos agentes de replicação, pois isso pode causar falha na replicação dos ativos (em execução na fila).
   >
   >Verifique se todos os quatro agentes de replicação estão configurados para evitar erro de tempo limite. Consulte [solucionar problemas na publicação paralela no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout).
   >
   >Não modifique nenhuma configuração gerada automaticamente.

Agora você pode:

* [Publicar ativos do AEM Assets no Brand Portal](../assets/brand-portal-publish-assets.md)
* [Publicar ativos do Brand Portal no AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=pt-BR) - Origem de ativos no Brand Portal
* [Publicar pastas do AEM Assets no Brand Portal](../assets/brand-portal-publish-folder.md)
* [Publicar coleções do AEM Assets no Brand Portal](../assets/brand-portal-publish-collection.md)
* [Publicar predefinições, esquemas e aspectos no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicar marcações no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

Consulte a [Documentação do Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para obter mais informações.


## Configuração de atualização {#upgrade-integration-65}

Para atualizar suas configurações existentes para o Console do Adobe Developer, siga as etapas abaixo, na sequência listada:

1. [Verificar trabalhos em execução](#verify-jobs)
1. [Excluir configurações existentes](#delete-existing-configuration)
1. [Criar configuração](#configure-new-integration-65)

### Verificar trabalhos em execução {#verify-jobs}

Certifique-se de que nenhum trabalho de publicação esteja em execução na instância do autor do AEM Assets antes de fazer edições. Para isso, você pode verificar o status de processos ativos em todos os quatro agentes de replicação e garantir que as filas estejam ociosas.

1. Faça logon na sua instância do AEM Assets Author.

1. No **Ferramentas** ![Ferramentas](assets/do-not-localize/tools.png) , navegue até **[!UICONTROL Implantação]** > **[!UICONTROL Replicação de implantação]**.

1. Na página Replicação, clique em **[!UICONTROL Agentes sobre o autor]**.

   ![Agentes de replicação para ativos](assets/test-integration2.png)

1. Localize os agentes de replicação do seu locatário do Brand Portal.

   Certifique-se de que o **A fila está ociosa** para todos os agentes de replicação e nenhum trabalho de publicação está ativo.

   ![Configurações da fila de replicação](assets/test-integration3.png)

### Excluir configurações existentes {#delete-existing-configuration}

Execute a seguinte lista de verificação ao excluir as configurações existentes:

* Excluir todos os quatro agentes de replicação
* Excluir o Brand Portal Cloud Service
* Excluir usuário do Mac

1. Faça logon na instância do AEM Assets Author e abra o CRX Lite como administrador. O URL padrão é `http://localhost:4502/crx/de/index.jsp`.

1. Navegue até `/etc/replications/agents.author` e exclua todos os quatro agentes de replicação do seu locatário do Brand Portal.

   ![Agente de replicação no CRXDE](assets/delete-replication-agent.png)

1. Navegue até `/etc/cloudservices/mediaportal` e exclua a configuração do Brand Portal cloud service.

   ![Detalhes do agente de replicação no CRXDE](assets/delete-cloud-service.png)

1. Navegue até `/home/users/mac` e exclua a variável **usuário do Mac** do seu locatário do Brand Portal.

   ![Mais detalhes do agente de replicação no CRXDE](assets/delete-mac-user.png)


Agora você pode [criar uma configuração](#configure-new-integration-65) por meio do Console do Adobe Developer na instância do autor do AEM 6.5.



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
