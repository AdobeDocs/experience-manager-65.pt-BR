---
title: Configurar a marcação de ativos usando o Serviço de conteúdo inteligente
description: Saiba como configurar a marcação inteligente e a marcação inteligente aprimorada no [!DNL Adobe Experience Manager], utilizando o Serviço de conteúdo inteligente.
role: Admin
feature: Tagging,Smart Tags
solution: Experience Manager, Experience Manager Assets
source-git-commit: d8d821a64b39b312168733126de8929c04016ff1
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 6%

---

# Solução de problemas de tags inteligentes para credenciais do OAuth {#oauth-config}

Uma configuração de autorização aberta é necessária para adotar o consentimento para o [!DNL Adobe Experience Manager] aplicativo para interagir com os Serviços de conteúdo inteligente de forma segura.

>[!NOTE]
>
> Não é possível criar novas credenciais JWT a partir de junho de 2024. De agora em diante, somente as credenciais OAuth de servidor para servidor são criadas.
> A integração do JWT continua funcionando até janeiro de 2025 somente para os usuários existentes do AMS e no local.

## Configuração do OAuth para os novos usuários do AMS {#oauth-config-existing-ams-users}

Consulte [configuração de serviços de conteúdo inteligente](#integrate-adobe-io) para a configuração dos serviços OAuth para um novo usuário. Depois de concluído, siga estes [etapas](#prereqs-config-oauth-onprem).

>[!NOTE]
>
>Se necessário, você pode enviar um tíquete de suporte seguindo o [processo de suporte](https://experienceleague.adobe.com/?lang=en&amp;support-tab=home#support).

## Configuração do OAuth para os usuários existentes do AMS {#oauth-config-new-ams-users}

Antes de executar qualquer uma das etapas dessa metodologia, é necessário implementar o seguinte:

### Pré-requisitos {#prereqs-config-oauth-onprem}

Uma configuração OAuth requer os seguintes pré-requisitos:

* Crie uma nova integração OAuth no [Console do desenvolvedor](https://developer.adobe.com/console/user/servicesandapis). Use o `ClientID`, `ClientSecret`, `OrgID`e outras propriedades nas etapas abaixo:
* Os seguintes arquivos podem ser encontrados neste caminho `/apps/system/config in crx/de`:
   * `com.**adobe**.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`
   * `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`

### Configuração do OAuth para o AMS existente e usuários locais {#steps-config-oauth-onprem}

As etapas abaixo podem ser executadas pelo administrador do sistema. O cliente AMS pode entrar em contato com o representante da Adobe ou enviar um tíquete de suporte seguindo o [processo de suporte](https://experienceleague.adobe.com/?lang=en&amp;support-tab=home#support).

1. Adicione ou atualize as propriedades abaixo em `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`:

   * `auth.token.provider.authorization.grants="client_credentials"`
   * `auth.token.provider.orgId="<OrgID>"`
   * `auth.token.provider.default.claims=("\"iss\"\ :\ \"<OrgID>\"")`
   * `auth.token.provider.scope="read_pc.dma_smart_content,\ openid,\ AdobeID,\ additional_info.projectedProductContext"`
     `auth.token.validator.type="adobe-ims-similaritysearch"`
   * Atualize o `auth.token.provider.client.id` com a ID do cliente da nova configuração do OAuth.
   * Atualizar `auth.access.token.request` para `"https://ims-na1.adobelogin.com/ims/token/v3"`
1. Renomeie o arquivo para `com.adobe.granite.auth.oauth.accesstoken.provider-<randomnumber>.config`.
1. Execute as etapas abaixo em `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`:
   * Atualize a propriedade auth.ims.client.secret com o Segredo do cliente da nova integração OAuth.
   * Renomeie o arquivo para `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl-<randomnumber>.config`
1. Salve todas as alterações no console de desenvolvimento do repositório de conteúdo, por exemplo, CRXDE.
<!--
1. Navigate to `/system/console/configMgr` and replace the OSGi configuration from `.<randomnumber>` to `-<randomnumber>`.
1. Delete the old OSGi configuration for `"Access Token provider name: adobe-ims-similaritysearch"` in `/system/console/configMgr`.
-->
1. Entrada `System/console/configMgr`, exclua as configurações antigas de `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl` e nome do provedor de token de acesso `adobe-ims-similaritysearch`.
1. Reinicie o console.

## Validar a configuração {#validate-the-configuration}

Após concluir a configuração, você pode usar um MBean JMX para validar a configuração. Para validar, siga estas etapas.

1. Acessar o [!DNL Experience Manager] servidor em `https://[aem_server]:[port]`.

1. Ir para **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]** para abrir o console OSGi. Clique em **[!UICONTROL Principal] > [!UICONTROL JMX]**.

1. Clique em `com.day.cq.dam.similaritysearch.internal.impl`. Ele abre **[!UICONTROL Tarefas Diversas de SimilaritySearch]**.

1. Clique em `validateConfigs()`. No **[!UICONTROL Validar configurações]** clique em **[!UICONTROL Chamar]**.

Os resultados da validação são exibidos no mesmo diálogo.

## Integração com o console do Adobe Developer {#integrate-adobe-io}

Como um novo usuário, ao integrar com o Console do Adobe Developer, a variável [!DNL Experience Manager] O servidor do autentica suas credenciais de serviço no gateway do Console do Adobe Developer antes de encaminhar sua solicitação ao Serviço de conteúdo inteligente. Para integrar o, você precisa de uma conta do Adobe ID com privilégios de administrador para a organização e uma licença do Serviço de conteúdo inteligente adquirida e ativada para a organização.

Para configurar o Serviço de conteúdo inteligente, siga estas etapas de nível superior:

1. Para gerar uma chave pública, [criar um serviço de conteúdo inteligente](#obtain-public-certificate) configuração no [!DNL Experience Manager]. [Baixar um certificado público](#obtain-public-certificate) para integração OAuth.

1. *[Não aplicável se você for um usuário existente]* [criar uma integração no console do Adobe Developer](#create-adobe-i-o-integration).

1. [Configurar a implantação](#configure-smart-content-service) usar a chave de API e outras credenciais do Console do Adobe Developer.

1. [Teste a configuração](#validate-the-configuration).

## Baixar um certificado público criando a configuração do Serviço de conteúdo inteligente {#download-public-certificate}

Um certificado público permite autenticar seu perfil no Console do Adobe Developer.

1. No [!DNL Experience Manager] interface de usuário, acesso **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Service herdados]**.

1. Na página Cloud Service, clique em **[!UICONTROL Configurar agora]** em **[!UICONTROL Tags inteligentes de ativos]**.

1. No **[!UICONTROL Criar configuração]** especifique um título e nome para a configuração de Tags inteligentes. Clique em **[!UICONTROL Criar]**.

1. No **[!UICONTROL Serviço de conteúdo inteligente AEM]** use os seguintes valores:

   **[!UICONTROL URL do serviço]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   Por exemplo, `https://smartcontent.adobe.io/apac`. Você pode especificar `na`, `emea`ou, `apac` como as regiões onde a instância do autor do Experience Manager está hospedada.

   >[!NOTE]
   >
   >Se o Serviço gerenciado de Experience Manager for provisionado antes de 1° de setembro de 2022, use o seguinte URL de serviço:
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Servidor de autorização]**: `https://ims-na1.adobelogin.com`

   Deixe os outros campos em branco por enquanto (a serem fornecidos posteriormente). Clique em **[!UICONTROL OK]**.

   ![Caixa de diálogo Serviço de conteúdo inteligente do Experience Manager para fornecer URL do serviço de conteúdo](assets/aem_scs12.png)

   *Figura: Caixa de diálogo Serviço de conteúdo inteligente para fornecer URL do serviço de conteúdo*

   >[!NOTE]
   >
   >O URL fornecido como [!UICONTROL URL do serviço] O não é acessível por meio do navegador e gera um erro 404. A configuração funciona bem com o mesmo valor de [!UICONTROL URL do serviço] parâmetro. Para obter o status geral do serviço e a programação de manutenção, consulte [https://status.adobe.com](https://status.adobe.com).

1. Clique em **[!UICONTROL Baixar certificado público para a integração com o OAuth]** e baixe o arquivo de certificado público `AEM-SmartTags.crt`. Além disso, você não é mais obrigado a carregar esse certificado no console do desenvolvedor do Adobe.

   ![Uma representação das configurações criadas para o serviço de marcação inteligente](assets/smart-tags-download-public-cert1.png)

   *Figura: configurações do serviço de marcação inteligente.*

## Criar integração do Console do Adobe Developer {#create-adobe-i-o-integration}

Para usar as APIs do Serviço de conteúdo inteligente, crie uma integração no Console do Adobe Developer para obter [!UICONTROL Chave de API] (gerado em [!UICONTROL ID DO CLIENTE] campo de integração do Adobe Developer Console), [!UICONTROL ID DA CONTA TÉCNICA], [!UICONTROL ID DA ORGANIZAÇÃO], e [!UICONTROL SEGREDO DO CLIENTE] para [!UICONTROL Configurações do serviço de marcação inteligente de ativos] da configuração de nuvem no [!DNL Experience Manager].

1. Access [https://developer.adobe.com/console/](https://developer.adobe.com/console/) em um navegador. Selecione a conta e verifique se a organização associada tem a função de administrador do sistema.

1. Crie um projeto com o nome que quiser. Clique em **[!UICONTROL Adicionar API]**.

1. Na página **[!UICONTROL Adicionar uma API]**, selecione **[!UICONTROL Experience Cloud]** e escolha **[!UICONTROL Conteúdo inteligente]**. Clique em **[!UICONTROL Avançar]**.

1. Escolha o **[!UICONTROL Servidor OAuth para servidor]** método de autenticação.

1. Adicionar/modificar o **[!UICONTROL Nome da credencial]** conforme necessário. Clique em **[!UICONTROL Avançar]**.

1. Selecione o perfil do produto **[!UICONTROL Serviços de conteúdo inteligente]**. Clique em **[!UICONTROL Salvar API configurada]**. A API OAuth é adicionada nas credenciais conectadas para uso posterior. Você pode copiar o [!UICONTROL Chave da API (ID do cliente)] ou [!UICONTROL Gerar token de acesso] dele.
<!--
1. On the **[!UICONTROL Select product profiles]** page, select **[!UICONTROL Smart Content Services]**. Click **[!UICONTROL Save configured API]**.

   A page displays more information about the configuration. Keep this page open to copy and add these values in [!UICONTROL Assets Smart Tagging Service Settings] of cloud configuration in [!DNL Experience Manager] to configure smart tags.

   ![In the Overview tab, you can review the information provided for integration.](assets/integration_details.png)


   *Figure: Details of integration in Adobe Developer Console*
-->

![configuração de oauth](assets/oauth-config.png)
*Figura: configuração de servidor para servidor do OAuth no console do Adobe Developer*

## Configurar o serviço de conteúdo inteligente {#configure-smart-content-service}

Para configurar a integração, use os valores de [!UICONTROL ID DA CONTA TÉCNICA], [!UICONTROL ID DA ORGANIZAÇÃO], [!UICONTROL SEGREDO DO CLIENTE], e [!UICONTROL ID DO CLIENTE] da integração do Console do Adobe Developer. A criação de uma configuração de nuvem de Tags inteligentes permite a autenticação de solicitações de API do [!DNL Experience Manager] implantação.

1. Entrada [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Service herdados]** para abrir o [!UICONTROL Cloud Service] console.

1. No **[!UICONTROL Tags inteligentes de ativos]**, abra a configuração criada acima. Na página de configurações do serviço, clique em **[!UICONTROL Editar]**.

1. Na caixa de diálogo **[!UICONTROL Serviço de conteúdo inteligente do AEM]**, use os valores pré-preenchidos nos campos **[!UICONTROL URL do serviço]** e **[!UICONTROL Servidor de autorização]**.

1. Para os campos [!UICONTROL Chave da API], [!UICONTROL ID da conta técnica], [!UICONTROL ID da organização], e [!UICONTROL Segredo do cliente], copie e use os seguintes valores gerados em [Integração do console do Adobe Developer](#create-adobe-i-o-integration).

   | [!UICONTROL Configurações do serviço de marcação inteligente de ativos] | [!DNL Adobe Developer Console] campos de integração |
   |--- |--- |
   | [!UICONTROL Chave da API] | [!UICONTROL ID DO CLIENTE] |
   | [!UICONTROL ID da conta técnica] | [!UICONTROL ID DA CONTA TÉCNICA] |
   | [!UICONTROL ID da organização] | [!UICONTROL ID DA ORGANIZAÇÃO] |
   | [!UICONTROL Segredo do cliente] | [!UICONTROL SEGREDO DO CLIENTE] |

>[!MORELIKETHIS]
>
>* [Visão geral e como treinar tags inteligentes](enhanced-smart-tags.md)
>* [Configurar marcação inteligente](config-smart-tagging.md)
>* [Tutorial em vídeo sobre tags inteligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)
