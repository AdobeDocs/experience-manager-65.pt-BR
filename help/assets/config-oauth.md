---
title: Configurar a marcação de ativos usando o Serviço de conteúdo inteligente
description: Saiba como configurar a marcação inteligente e a marcação inteligente aprimorada no  [!DNL Adobe Experience Manager], usando o Serviço de Conteúdo Inteligente.
role: Admin
feature: Tagging,Smart Tags
solution: Experience Manager, Experience Manager Assets
exl-id: 9caee314-697b-4a7b-b991-10352da17f2c
source-git-commit: ab9292c491cc9dfcd8f239ba279b1e0ae6d1560f
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 6%

---

# Solução de problemas de tags inteligentes para credenciais do OAuth {#oauth-config}

Uma configuração de autorização aberta é necessária para aprovar o consentimento para que o aplicativo [!DNL Adobe Experience Manager] interaja com os Serviços de Conteúdo Inteligente de maneira segura.

>[!NOTE]
>
> Não é possível criar novas credenciais JWT a partir de junho de 2024. De agora em diante, somente as credenciais OAuth de servidor para servidor são criadas.
> A integração do JWT continua funcionando até janeiro de 2025 somente para os usuários existentes do AMS e no local.

## Configuração do OAuth para os novos usuários do AMS {#oauth-config-existing-ams-users}

Consulte [configuração de serviços de conteúdo inteligente](#integrate-adobe-io) para obter a configuração de serviços OAuth para um novo usuário. Depois de concluído, siga estas [etapas](#prereqs-config-oauth-onprem).

>[!NOTE]
>
>Se necessário, você pode enviar um tíquete de suporte seguindo o [processo de suporte](https://experienceleague.adobe.com/pt-br?lang=en&amp;support-tab=home#support).

## Configuração do OAuth para os usuários existentes do AMS {#oauth-config-new-ams-users}

Antes de executar qualquer uma das etapas dessa metodologia, é necessário implementar o seguinte:

### Pré-requisitos {#prereqs-config-oauth-onprem}

Uma configuração OAuth requer os seguintes pré-requisitos:

* Crie uma nova integração OAuth no [Developer Console](https://developer.adobe.com/console/user/servicesandapis). Use o `ClientID`, `ClientSecret`, `OrgID` e outras propriedades nas etapas abaixo:
* Os seguintes arquivos podem ser encontrados neste caminho `/apps/system/config in crx/de`:
   * `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`
   * `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`

### Configuração do OAuth para o AMS existente e usuários locais {#steps-config-oauth-onprem}

As etapas abaixo podem ser executadas pelo administrador do sistema no **CRXDE**. O cliente AMS pode entrar em contato com o representante da Adobe ou enviar um tíquete de suporte seguindo o [processo de suporte](https://experienceleague.adobe.com/pt-br?lang=en&amp;support-tab=home#support).

1. Adicionar ou atualizar as propriedades abaixo em `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`:

   * `auth.token.provider.authorization.grants="client_credentials"`
   * `auth.token.provider.orgId="<OrgID>"`
   * `auth.token.provider.default.claims=("\"iss\"\ :\ \"<OrgID>\"")`
   * `auth.token.provider.scope="read_pc.dma_smart_content,\ openid,\ AdobeID,\ additional_info.projectedProductContext"`

     `auth.token.validator.type="adobe-ims-similaritysearch"`
   * Atualize o `auth.token.provider.client.id` com a ID de cliente da nova configuração OAuth.
   * Atualizar `auth.access.token.request` para `"https://ims-na1.adobelogin.com/ims/token/v3"`
1. Renomeie o arquivo para `com.adobe.granite.auth.oauth.accesstoken.provider-<randomnumber>.config`.

   >[!IMPORTANT]
   >
   >Substitua o ponto (.) pelo hífen (-) como um prefixo de `<randomnumber>`.

1. Execute as etapas abaixo em `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`:
   * Atualize a propriedade auth.ims.client.secret com o Segredo do cliente da nova integração OAuth.
   * Renomear o arquivo para `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl-<randomnumber>.config`
1. Salve todas as alterações no console de desenvolvimento do repositório de conteúdo, por exemplo, CRXDE.
<!--
1. Navigate to `/system/console/configMgr` and replace the OSGi configuration from `.<randomnumber>` to `-<randomnumber>`.
1. Delete the old OSGi configuration for `"Access Token provider name: adobe-ims-similaritysearch"` in `/system/console/configMgr`.
-->
1. No `System/console/configMgr`, você pode ver arquivos de configuração novos e antigos. Exclua as configurações mais antigas de `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl` e o nome do provedor de Token de Acesso `adobe-ims-similaritysearch`. Verifique se apenas a configuração atualizada está em vigor, em vez das configurações mais antigas.
1. Reinicie o console.

## Validar a configuração {#validate-the-configuration}

Após concluir a configuração, você pode usar um MBean JMX para validar a configuração. Para validar, siga estas etapas.

1. Acesse seu servidor [!DNL Experience Manager] em `https://[aem_server]:[port]`.

1. Acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]** para abrir o console OSGi. Clique em **[!UICONTROL Principal] > [!UICONTROL JMX]**.

1. Clique em `com.day.cq.dam.similaritysearch.internal.impl`. Ele abre **[!UICONTROL Tarefas Diversas de SimilaritySearch]**.

1. Clique em `validateConfigs()`. Na caixa de diálogo **[!UICONTROL Validar Configurações]**, clique em **[!UICONTROL Chamar]**.

Os resultados da validação são exibidos no mesmo diálogo.

>[!NOTE]
>
>Se ocorrer o erro `unsupported_grant_type`, tente instalar o hotfix do Granite. Consulte [migração da conta de serviço (JWT) para as credenciais de servidor para servidor do OAuth](https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-24660).

## Integrar ao Adobe Developer Console {#integrate-adobe-io}

Como um novo usuário, ao integrar com o Adobe Developer Console, o servidor [!DNL Experience Manager] autentica suas credenciais de serviço no gateway do Adobe Developer Console antes de encaminhar sua solicitação ao Serviço de Conteúdo Inteligente. Para integrar o, você precisa de uma conta do Adobe ID com privilégios de administrador para a organização e uma licença do Serviço de conteúdo inteligente adquirida e ativada para a organização.

Para configurar o Serviço de conteúdo inteligente, siga estas etapas de nível superior:

<!--![Experience Manager Smart Content Service dialog to provide content service URL](assets/config-oauth.png)-->

1. Para gerar uma chave pública, [crie uma configuração do Serviço de Conteúdo Inteligente](#oauth-config) em [!DNL Experience Manager]. [Baixe um certificado público](#oauth-config) para integração com o OAuth.

1. *[Não aplicável se você for um usuário existente]* [criar uma integração no Adobe Developer Console](#create-adobe-i-o-integration).

1. [Configure sua implantação](#configure-smart-content-service) usando a chave de API e outras credenciais da Adobe Developer Console.

1. [Teste a configuração](#validate-the-configuration).

## Baixar um certificado público criando a configuração do Serviço de conteúdo inteligente {#download-public-certificate}

Um certificado público permite autenticar seu perfil na Adobe Developer Console.

1. Na interface de usuário do [!DNL Experience Manager], acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Service herdados]**.

1. Na página Cloud Service, clique em **[!UICONTROL Configurar agora]** em **[!UICONTROL Tags inteligentes da Assets]**.

1. Na caixa de diálogo **[!UICONTROL Criar Configuração]**, especifique um título e nome para a configuração de Tags Inteligentes. Clique em **[!UICONTROL Criar]**.

1. Na caixa de diálogo **[!UICONTROL Serviço de Conteúdo Inteligente do AEM]**, use os seguintes valores:

   **[!UICONTROL URL de Serviço]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   Por exemplo, `https://smartcontent.adobe.io/apac`. Você pode especificar `na`, `emea` ou `apac` como as regiões onde a instância do autor do Experience Manager está hospedada.

   >[!NOTE]
   >
   >Se o Serviço gerenciado de Experience Manager for provisionado antes de 1° de setembro de 2022, use o seguinte URL de serviço:
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Servidor de autorização]**: `https://ims-na1.adobelogin.com`

   Deixe os outros campos em branco por enquanto (a serem fornecidos posteriormente). Clique em **[!UICONTROL OK]**.

   ![Caixa de diálogo do Serviço de Conteúdo Inteligente do Experience Manager para fornecer a URL do serviço de conteúdo](assets/aem_scs12.png)

   *Figura: caixa de diálogo Serviço de Conteúdo Inteligente para fornecer a URL do serviço de conteúdo*

   >[!NOTE]
   >
   >A URL fornecida como [!UICONTROL URL de Serviço] não pode ser acessada pelo navegador e gera um erro 404. A configuração funciona bem com o mesmo valor do parâmetro [!UICONTROL URL de Serviço]. Para obter o status geral do serviço e o agendamento de manutenção, consulte [https://status.adobe.com](https://status.adobe.com).

1. Clique em **[!UICONTROL Baixar Certificado Público para Integração com o OAuth]** e baixe o arquivo de certificado público `AEM-SmartTags.crt`. Além disso, você não precisa mais fazer upload desse certificado no console do Adobe Developer.

   ![Uma representação das configurações criadas para o serviço de marcação inteligente](assets/smart-tags-download-public-cert1.png)

   *Figura: Configurações do serviço de marcação inteligente.*

## Criar integração do Adobe Developer Console {#create-adobe-i-o-integration}

Para usar APIs do Serviço de Conteúdo Inteligente, crie uma integração no Adobe Developer Console para obter a [!UICONTROL Chave de API] (gerada no campo [!UICONTROL ID do CLIENTE] da integração com o Adobe Developer Console), a [!UICONTROL ID da CONTA TÉCNICA], a [!UICONTROL ID DA ORGANIZAÇÃO] e o [!UICONTROL SEGREDO DO CLIENTE] para as [!UICONTROL Configurações do Serviço de Marcação Inteligente da Assets] da configuração de nuvem em [!DNL Experience Manager].

1. Acesse [https://developer.adobe.com/console/](https://developer.adobe.com/console/) em um navegador. Selecione a conta e verifique se a organização associada tem a função de administrador do sistema.

1. Crie um projeto com o nome que quiser. Clique em **[!UICONTROL Adicionar API]**.

1. Na página **[!UICONTROL Adicionar uma API]**, selecione **[!UICONTROL Experience Cloud]** e escolha **[!UICONTROL Conteúdo inteligente]**. Clique em **[!UICONTROL Avançar]**.

1. Escolha o método de autenticação **[!UICONTROL Servidor a Servidor do OAuth]**.

1. Adicione/modifique o **[!UICONTROL Nome da Credencial]** conforme necessário. Clique em **[!UICONTROL Avançar]**.

1. Selecione o perfil de produto **[!UICONTROL Serviços de Conteúdo Inteligente]**. Clique em **[!UICONTROL Salvar API configurada]**. A API OAuth é adicionada às credenciais conectadas para uso posterior. Você pode copiar a [!UICONTROL Chave de API (ID do Cliente)] ou [!UICONTROL Gerar token de acesso] a partir dela.
<!--
1. On the **[!UICONTROL Select product profiles]** page, select **[!UICONTROL Smart Content Services]**. Click **[!UICONTROL Save configured API]**.

   A page displays more information about the configuration. Keep this page open to copy and add these values in [!UICONTROL Assets Smart Tagging Service Settings] of cloud configuration in [!DNL Experience Manager] to configure smart tags.

   ![In the Overview tab, you can review the information provided for integration.](assets/integration_details.png)


   *Figure: Details of integration in Adobe Developer Console*
-->

![configuração de oauth](assets/oauth-config.png)
*Figura: servidor OAuth configurado para servidor no Adobe Developer Console*

## Configurar o serviço de conteúdo inteligente {#configure-smart-content-service}

Para configurar a integração, use os valores dos campos [!UICONTROL ID DA CONTA TÉCNICA], [!UICONTROL ID DA ORGANIZAÇÃO], [!UICONTROL SEGREDO DO CLIENTE] e [!UICONTROL ID DO CLIENTE] da integração com o Adobe Developer Console. Criar uma configuração de nuvem de Tags Inteligentes permite a autenticação de solicitações de API da implantação [!DNL Experience Manager].

1. Em [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Services herdados]** para abrir o console [!UICONTROL Cloud Services].

1. Nas **[!UICONTROL Tags inteligentes do Assets]**, abra a configuração criada acima. Na página de configurações do serviço, clique em **[!UICONTROL Editar]**.

1. Na caixa de diálogo **[!UICONTROL Serviço de conteúdo inteligente do AEM]**, use os valores pré-preenchidos nos campos **[!UICONTROL URL do serviço]** e **[!UICONTROL Servidor de autorização]**.

1. Para os campos [!UICONTROL Chave da API], [!UICONTROL ID da Conta Técnica], [!UICONTROL ID da Organização] e [!UICONTROL Segredo do Cliente], copie e use os seguintes valores gerados na [integração com o Adobe Developer Console](#create-adobe-i-o-integration).

   | [!UICONTROL Configurações do Serviço de Marcação Inteligente do Assets] | Campos de integração do [!DNL Adobe Developer Console] |
   |--- |--- |
   | [!UICONTROL Chave de API] | [!UICONTROL ID DO CLIENTE] |
   | [!UICONTROL ID da Conta Técnica] | [!UICONTROL ID DA CONTA TÉCNICA] |
   | [!UICONTROL ID da Organização] | [!UICONTROL ID DA ORGANIZAÇÃO] |
   | [!UICONTROL Segredo do cliente] | [!UICONTROL SEGREDO DO CLIENTE] |

>[!MORELIKETHIS]
>
>* [Visão geral e como treinar Tags Inteligentes](enhanced-smart-tags.md)
>* [Configurar marcação inteligente](config-smart-tagging.md)
>* [Tutorial em vídeo sobre marcas inteligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html?lang=pt-BR)
