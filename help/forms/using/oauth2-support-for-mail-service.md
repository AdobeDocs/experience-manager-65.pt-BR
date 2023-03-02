---
title: Configurar a autenticação baseada em OAuth2 para os protocolos de servidor de email do Microsoft® Office 365
description: Configurar a autenticação baseada em OAuth2 para os protocolos de servidor de email do Microsoft® Office 365
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
source-git-commit: d19de2955adef56570378a6d62ec0015718f9039
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 3%

---

# Integrar aos protocolos de servidor de email do Microsoft® Office 365 {#oauth2-support-for-the-microsoft-mail-server-protocols}

Para permitir que as organizações cumpram com os requisitos de segurança de e-mail, a AEM Forms oferece suporte ao OAuth 2.0 para integração com os protocolos de servidor de e-mail do Microsoft® Office 365. Você pode usar o serviço de autenticação OAuth 2.0 do Azure Ative Diretory (Azure AD) para se conectar a vários protocolos, como IMAP, POP ou SMTP, e acessar dados de email para usuários do Office 365. Abaixo estão as instruções passo a passo para configurar os protocolos de servidor de email do Microsoft® Office 365 para autenticação via serviço OAuth 2.0:

1. Logon [https://portal.azure.com/](https://portal.azure.com/) e pesquisar **Azure Ative Diretory** na barra de pesquisa e no resultado.
Como alternativa, você pode navegar diretamente para [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Clique em **Adicionar** > **Registro do aplicativo** > **Novo registro**

   ![Registro do aplicativo](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. Preencha as informações de acordo com suas necessidades e clique em **Registrar**.
   ![Conta suportada](/help/forms/using/assets/azure_suuportedaccountype.png)
No caso acima, 
**Contas em qualquer diretório organizacional (Qualquer diretório Azure AD - Multilocatário) e contas pessoais da Microsoft® (por exemplo, Skype, Xbox)** for selecionada.

   >[!NOTE]
   >
   > * Para **Contas em qualquer diretório organizacional (qualquer diretório do Azure AD - Multilocatário)** aplicativo, é recomendável usar a conta corporativa em vez da conta de email pessoal.
   > * **Somente contas pessoais Microsoft®** aplicativo não é suportado.
   > * É recomendável usar **Conta pessoal e de vários locatários da Microsoft®** aplicação.


1. Em seguida, acesse **Certificados e segredos**, clique em **Novo segredo do cliente** e siga as etapas na tela para criar um segredo. Anote esse valor de secret para uso posterior.

   ![Chave secreta](/help/forms/using/assets/azure_secretkey.png)

1. Para adicionar permissões, vá para o aplicativo recém-criado e selecione **Permissões de API** > **Adicionar uma permissão** > **Gráfico Microsoft®** > **Permissões delegadas**
1. Marque as caixas de seleção das permissões abaixo para o aplicativo e clique em **Adicionar permissão**:

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![Permissão de API](/help/forms/using/assets/azure_apipermission.png)

1. Selecionar **Autenticação** > **Adicionar uma plataforma** > **Web**, e no **URLs de redirecionamento** adicione qualquer um dos URIs abaixo (Identificador universal de recurso) como:
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   Nesse caso, `https://login.microsoftonline.com/common/oauth2/nativeclient` é usado como um URI de redirecionamento.

1. Clique em **Configurar** depois de adicionar cada URL e definir as configurações de acordo com seus requisitos.
   ![URI de redirecionamento](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > É obrigatório selecionar **Tokens de acesso** e **Tokens de ID** caixas de seleção.

1. Clique em **Visão geral** no painel esquerdo e copie os valores de **ID do aplicativo (cliente)**, **ID do diretório (locatário)**, e **Segredo do cliente** para uso posterior.

   ![Visão geral](/help/forms/using/assets/azure_overview.png)

## Geração do código de autorização {#generating-the-authorization-code}

Em seguida, é necessário gerar o código de autorização, explicado nas seguintes etapas:

1. Abra o seguinte URL no navegador após substituir `clientID` com o `<client_id>` e `redirect_uri` com o URI de redirecionamento do seu aplicativo:

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   > No caso do pedido de um único inquilino, substituir `common` com o seu `[tenantid]` no seguinte URL para gerar o código de autorização: `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. Quando digitar o URL acima, você será redirecionado para a tela de logon:
   ![Tela de login](/help/forms/using/assets/azure_loginscreen.png)

1. Insira o email, clique em **Próxima** e a tela de permissão do aplicativo será exibida:

   ![Permitir permissão](/help/forms/using/assets/azure_permission.png)

1. Após permitir a permissão, você será redirecionado para um novo URL como: `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. Copie o valor de `<code>` do URL acima de `0.ASY...` para `&session_state` no URL acima.

## Geração do token de atualização {#generating-the-refresh-token}

Em seguida, você precisa gerar o token de atualização, explicado nas seguintes etapas:

1. Abra o prompt de comando e use o seguinte comando cURL para obter o refreshToken.

1. Substitua o `clientID`, `client_secret` e `redirect_uri` com os valores do aplicativo junto com o valor de `<code>`:

   `curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   > Em um único aplicativo de locatário, para gerar um token de atualização, use o seguinte comando cURL e substitua `common` com o `[tenantid]` em:
   >`curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. Anote o token de atualização.

## Configurar o serviço de e-mail com suporte ao OAuth 2.0 {#configureemailservice}

Agora, você precisa configurar o serviço de e-mail no servidor JEE mais recente fazendo logon na interface do usuário do administrador:

1. Ir para **Início** > **Serviço** > **Aplicativos e serviços** > **Gerenciamento de serviços** > **Serviço de e-mail**, o **Serviço de email de configuração** é exibida, configurada para autenticação básica.

   >[!NOTE]
   >
   > Para habilitar o serviço de autenticação oAuth 2.0, é obrigatório selecionar **Se o servidor SMTP requer autenticação (Autenticação SMTP)** caixa de seleção

1. Definir **Configurações de Autenticação oAuth 2.0** as `True`.
1. Copie os valores de **ID do cliente** e **Segredo do cliente** do Portal do Azure.
1. Copie o valor de gerado **Atualizar token**.
1. Faça logon no **Workbench** e pesquisar **Email 1.0** de **Seletor de atividade**.
1. Três opções estão disponíveis no Email 1.0 como:
   * **Enviar com documento**: envia email com anexos únicos.
   * **Enviar com Mapa de Anexos**: envia email com vários anexos.
   * **Receber**: recebe um email do IMAP.

   >[!NOTE]
   >
   >* O protocolo Transport Security tem valores válidos como: &quot;blank&quot;, &quot;SSL&quot; ou &quot;TLS&quot;. Você deve definir valores de **Segurança de Transporte SMTP** e **Receber Segurança de Transporte** para **TLS** para habilitar o serviço de autenticação oAuth.
   >* **Protocolo POP3** não é compatível com o OAuth ao usar endpoints de email.


   ![Configurações de conexão](/help/forms/using/assets/oauth_connectionsettings.png)

1. Testar o aplicativo selecionando **Enviar com documento**.
1. Fornecer **PARA** e **De** endereços.
1. Chame o aplicativo e o email é enviado usando a autenticação 0Auth 2.0.

   >[!NOTE]
   >
   >Se você quiser alterar a configuração de autenticação Auth 2.0 para autenticação básica para um processo específico em uma bancada, é possível definir o **Autenticação do OAuth 2.0** value como &#39;False&#39; em **Usar configurações globais** no **Configurações de conexão** guia.

## Para ativar notificações de tarefas oAuth {#enable_oauth_task}

1. Ir para **Início** > **Serviços** > **Fluxo de trabalho do formulário** > **Configurações do servidor** > **Configurações de email**
1. Para ativar notificações de tarefas oAuth, selecione a **Habilitar oAuth** caixa de seleção
1. Copie os valores de **ID do cliente** e **Segredo do cliente** do Portal do Azure.
1. Copie o valor de gerado **Atualizar token**.
1. Clique em **Salvar** para salvar os detalhes.

   ![Notificação de Tarefa](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > Para saber mais informações relacionadas às notificações de tarefas, [clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## Para configurar o terminal de email {#configure_email_endpoint}

1. Ir para **Início** > **Serviços** > **Aplicativos e serviços** > **Gerenciamento de Ponto de Extremidade**
1. Para configurar o endpoint de email, defina **Configurações de Autenticação oAuth 2.0** as `True`.
1. Copie os valores de **ID do cliente** e **Segredo do cliente** do Portal do Azure.
1. Copie o valor de gerado **Atualizar token**.
1. Clique em **Salvar** para salvar os detalhes.

   ![Configurações de conexão](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > Para saber mais sobre como configurar endpoints de email, clique em [Configurar um terminal de email](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html).

## Resolução de problemas {#troubleshooting}

* Se o serviço de e-mail não estiver funcionando corretamente. Tente regenerar a variável `Refresh Token` conforme descrito acima. Leva alguns minutos para o novo valor ser implantado.

* Erro ao configurar detalhes do servidor de email no endpoint de email usando o Workbench. Tente configurar o endpoint por meio da interface do usuário de administração em vez do Workbench.
