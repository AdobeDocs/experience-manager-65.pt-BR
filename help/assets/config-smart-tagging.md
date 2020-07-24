---
title: Configure a marcação de ativos usando o Serviço de conteúdo inteligente.
description: Saiba como configurar a marcação inteligente e a marcação inteligente aprimorada [!DNL Adobe Experience Manager], usando o Serviço de conteúdo inteligente.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 29cf202b2522b4e624960e8b911f77ec7f291e24
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 43%

---


# Configurar a marcação de ativos usando o Serviço de conteúdo inteligente {#configure-asset-tagging-using-the-smart-content-service}

Você pode fazer a integração [!DNL Adobe Experience Manager] com o Smart Content Service usando o Adobe Developer Console. Use essa configuração para acessar o Serviço de conteúdo inteligente de dentro [!DNL Experience Manager].

O artigo detalha as seguintes tarefas principais que são necessárias para configurar o Serviço de conteúdo inteligente. At the back end, the [!DNL Experience Manager] server authenticates your service credentials with the Adobe Developer Console gateway before forwarding your request to the Smart Content Service.

1. Create a Smart Content Service configuration in [!DNL Experience Manager] to generate a public key. [Obtenha um certificado público](#obtain-public-certificate) para a integração OAuth.
1. [Crie uma integração no Console do desenvolvedor](#create-adobe-i-o-integration) e faça upload da chave pública gerada.
1. [Configure sua implantação](#configure-smart-content-service) usando a chave da API e outras credenciais do Adobe Developer Console.
1. [Teste a configuração](#validate-the-configuration).
1. Optionally, [enable auto-tagging on asset upload](#enable-smart-tagging-in-the-update-asset-workflow-optional).

## Pré-requisitos {#prerequisites}

Antes de usar o Serviço de conteúdo inteligente, verifique o seguinte para criar uma integração no Adobe Developer Console:

* Existência de uma Adobe ID com privilégios de administrador para a organização.
* O serviço Smart Content Service está habilitado para sua organização.

Para habilitar Tags inteligentes aprimoradas, além do acima, instale também o service pack [mais recente do](https://helpx.adobe.com/br/experience-manager/aem-releases-updates.html)AEM.

## Obter certificado público {#obtain-public-certificate}

Um certificado público permite autenticar seu perfil no Console do desenvolvedor.

1. Na interface do [!DNL Experience Manager] usuário, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Service]** herdados.

1. In the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.
1. Na caixa de diálogo **[!UICONTROL Criar configuração]** , especifique um título e um nome para a configuração de Tags inteligentes. Clique em **[!UICONTROL Criar]**.
1. Na caixa de diálogo Serviço **[!UICONTROL de conteúdo inteligente do]** AEM, use os seguintes valores:

   **[!UICONTROL URL do serviço]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Servidor de autorização]**: `https://ims-na1.adobelogin.com`

   Deixe os outros campos em branco por enquanto (a ser fornecido posteriormente). Clique em **[!UICONTROL OK]**.

   ![caixa de diálogo Serviço de conteúdo inteligente do Experience Manager para fornecer o URL do serviço de conteúdo](assets/aem_scs.png)

   >[!NOTE]
   >
   >O URL fornecido como URL  de serviço não pode ser acessado pelo navegador e gera um erro 404. A configuração funciona bem com o mesmo valor do parâmetro de URL [!UICONTROL do] serviço. Para obter o status geral do serviço e a programação de manutenção, consulte [https://status.adobe.com](https://status.adobe.com).

1. Clique em **[!UICONTROL Baixar certificado público para integração]** OAuth e baixe o arquivo de certificado público `AEM-SmartTags.crt`.

   ![Uma representação das configurações criadas para o serviço de marcação inteligente](assets/smart-tags-download-public-cert.png)

### Reconfigure when a certificate expires {#certrenew}

Depois que um certificado expira, ele não é mais confiável. Não é possível renovar um certificado expirado. Para adicionar um novo certificado, siga estas etapas.

1. Faça logon na implantação do [!DNL Experience Manager] como administrador. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.

1. Localize o usuário **[!UICONTROL dam-update-service]** e clique nele. Clique na guia **[!UICONTROL Armazenamento de chaves]**.
1. Exclua o armazenamento de chaves **[!UICONTROL similaritysearch]** existente com o certificado expirado. Clique em **[!UICONTROL Salvar e fechar]**.

   ![Exclua a entrada de pesquisa de similaridade existente no Keystore para adicionar um novo certificado de segurança](assets/smarttags_delete_similaritysearch_keystore.png)

   *Figura: exclua a entrada`similaritysearch`existente no Armazenamento de chaves para adicionar um novo certificado de segurança.*

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços da nuvem]** > **[!UICONTROL Serviços da nuvem herdados]**. Clique em **[!UICONTROL Tags inteligentes de ativos]** > **[!UICONTROL Mostrar configuração]** > **[!UICONTROL Configurações disponíveis]**. Clique na configuração necessária.

1. To download a public certificate, click **[!UICONTROL Download Public Certificate for OAuth Integration]**.
1. Acesse [https://console.adobe.io](https://console.adobe.io) e navegue até os Serviços de conteúdo inteligente existentes na página **[!UICONTROL Integrações]** . Carregue o novo certificado. For more information, see the instructions in [Create Adobe Developer Console integration](#create-adobe-i-o-integration).

## Criar integração do Adobe Developer Console {#create-adobe-i-o-integration}

Para usar as APIs do Serviço de conteúdo inteligente, crie uma integração no Adobe Developer Console para gerar a chave de API, a ID da conta técnica, a ID da organização e o segredo do cliente.

1. Acesse [https://console.adobe.io](https://console.adobe.io/) em um navegador. Selecione a conta e verifique se a organização associada tem a função de administrador do sistema.
1. Crie um projeto com o nome que quiser. Clique em **[!UICONTROL Adicionar API]**.
1. Na página **[!UICONTROL Adicionar uma API]**, selecione **[!UICONTROL Experience Cloud]** e escolha **[!UICONTROL Conteúdo inteligente]**. Clique em **[!UICONTROL Avançar]**.
1. Selecione **[!UICONTROL Fazer upload da sua chave pública]**. Forneça o arquivo de certificado baixado do [!DNL Experience Manager]. Será exibida a mensagem [!UICONTROL Chave(s) pública(s) carregada(s) com êxito]. Clique em **[!UICONTROL Avançar]**.
1. A página [!UICONTROL Criar uma nova credencial de conta de serviço (JWT)] exibe a chave pública da conta de serviço recém-configurada. Clique em **[!UICONTROL Avançar]**.
1. Na página **[!UICONTROL Selecionar perfis de produtos]**, selecione **[!UICONTROL Serviços de conteúdo inteligente]**. Clique em **[!UICONTROL Salvar API configurada]**. Uma página exibe mais informações sobre a configuração. Para continuar configurando as Tags inteligentes no [!DNL Experience Manager], mantenha essa página aberta para copiar e adicionar esses valores no Experience Manager.

   ![Na guia Visão geral, é possível revisar as informações da integração.](assets/integration_details.png)

## Configurar o Serviço de conteúdo inteligente {#configure-smart-content-service}

Para configurar a integração, use os valores dos campos ID da conta técnica, ID da organização, segredo do cliente, servidor de autorização e chave da API da integração do Adobe Developer Console. A criação de uma configuração em nuvem de Tags inteligentes permite a autenticação de solicitações de API da [!DNL Experience Manager] implantação.

1. Em [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > Cloud Service **** herdados para abrir o console [!UICONTROL Cloud Service] .
1. Em Tags **[!UICONTROL inteligentes de]** ativos, abra a configuração criada acima. Na página de configurações do serviço, clique em **[!UICONTROL Editar]**.
1. Na caixa de diálogo **[!UICONTROL Serviço de conteúdo inteligente do AEM]**, use os valores pré-preenchidos nos campos **[!UICONTROL URL do serviço]** e **[!UICONTROL Servidor de autorização]**.
1. Nos campos **[!UICONTROL Chave da API]**, **[!UICONTROL ID da conta técnica]**, **[!UICONTROL ID da organização]** e **[!UICONTROL Segredo do cliente]**, use os valores gerados acima.

## Validar a configuração {#validate-the-configuration}

Depois de concluir a configuração, você pode usar um MBean JMX para validar a configuração. Para validar, siga estas etapas.

1. Acesse seu [!DNL Experience Manager] servidor em `https://[aem_server]:[port]`.
1. Vá até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > Console **[!UICONTROL da]** Web para abrir o console do OSGi. Clique em **[!UICONTROL Principal]>[!UICONTROL JMX]**.
1. Clique em `com.day.cq.dam.similaritysearch.internal.impl`. Ele abre **[!UICONTROL SemelhançaPesquise Tarefas]** diversas.
1. Clique em `validateConfigs()`. Na caixa de diálogo **[!UICONTROL Validar configurações]** , clique em **[!UICONTROL Chamar]**. Os resultados da validação são exibidos na mesma caixa de diálogo.

## Habilitar marcação inteligente no fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM (Opcional) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. In [!DNL Experience Manager], go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. Na página **[!UICONTROL Modelos de fluxo de trabalho]**, selecione o modelo de fluxo de trabalho **[!UICONTROL Ativo de atualização DAM]**.
1. Clique em **[!UICONTROL Editar]** na barra de ferramentas.
1. Expanda o painel lateral para exibir as etapas. Arraste a etapa **[!UICONTROL Ativo de tag inteligente]** disponível na seção Fluxo de trabalho do DAM e coloque-a após a etapa **[!UICONTROL Processar miniaturas]**.

   ![Etapa para adicionar ativo de tag inteligente após a etapa de miniatura do processo no fluxo de trabalho Ativo de atualização DAM](assets/smart-tag-in-dam-update-asset-workflow.png)

   *Figura: etapa para adicionar ativo de tag inteligente após a etapa de miniatura do processo no fluxo de trabalho Ativo de atualização DAM*

1. Abra a etapa no modo de edição. Em **[!UICONTROL Configurações avançadas]**, verifique se a opção **[!UICONTROL Avanço do manipulador]** está selecionada.

   ![Configurar o fluxo de trabalho do Ativo de atualização do DAM e adicionar a etapa da tag inteligente](assets/smart-tag-step-properties-workflow1.png)

1. Na guia **[!UICONTROL Argumentos]**, selecione **[!UICONTROL Ignorar erros]** se desejar que o fluxo de trabalho seja concluído mesmo se a etapa de marcação automática falhar.

   Para marcar os ativos quando eles forem carregados independentemente de a marcação inteligente estar ativada nas pastas, selecione **[!UICONTROL Ignorar sinalizador de tag inteligente]**.

   ![Configurar o fluxo de trabalho do Ativo de atualização do DAM para adicionar a etapa da tag inteligente e selecionar ignorar sinalizador da tag inteligente](assets/smart-tag-step-properties-workflow2.png)

1. Clique em **[!UICONTROL OK]** para fechar a etapa do processo e salve o fluxo de trabalho.

>[!MORELIKETHIS]
>
>* [Gerenciar tags inteligentes](managing-smart-tags.md)
>* [Visão geral e como treinar Tags inteligentes](enhanced-smart-tags.md)
>* [Diretrizes e regras para treinamento do Serviço de conteúdo inteligente](smart-tags-training-guidelines.md)
>* [Tutorial em vídeo sobre como configurar tags inteligentes](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

