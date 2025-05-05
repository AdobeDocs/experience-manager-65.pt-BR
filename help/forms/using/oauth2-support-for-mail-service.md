---
title: Configurar a autenticação baseada em OAuth2 para o Microsoft&reg (Forms JEE OAuth); protocolos de servidor de email do Office 365
description: Configurar a autenticação baseada em OAuth2 para o Microsoft&reg (Forms JEE OAuth); protocolos de servidor de email do Office 365
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 5%

---

# Integrar o AEM Forms com os protocolos de servidor de email do Microsoft® Office 365 {#oauth2-support-for-the-microsoft-mail-server-protocols}

Para permitir que as organizações cumpram com os requisitos de segurança de e-mail, a AEM Forms oferece suporte ao OAuth 2.0 para integração com os protocolos de servidor de e-mail do Microsoft® Office 365. Você pode usar o serviço de autenticação OAuth 2.0 do Azure Ative Diretory (Azure AD) para se conectar a vários protocolos, como IMAP, POP ou SMTP, e acessar dados de email para usuários do Office 365. Abaixo estão as instruções passo a passo para configurar os protocolos de servidor de email do Microsoft® Office 365 para autenticação através do serviço OAuth 2.0:

1. Faça logon em [https://portal.azure.com/](https://portal.azure.com/) e pesquise por **Azure Ative Diretory** na barra de pesquisa e clique no resultado.
Como alternativa, você pode navegar diretamente para [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Clique em **Adicionar** > **Registro do Aplicativo** > **Novo Registro**.

   ![Registro do aplicativo](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. Preencha as informações de acordo com suas necessidades e clique em **Registrar**.
   ![Conta com Suporte](/help/forms/using/assets/azure_suuportedaccountype.png)
No caso acima, a opção **Contas em qualquer diretório organizacional (Qualquer diretório do Azure AD - Multilocatário) e contas pessoais da Microsoft® (por exemplo, Skype, Xbox)** está selecionada.

   >[!NOTE]
   >
   > * Para **Contas em qualquer diretório organizacional (Qualquer diretório do Azure AD - Multilocatário)**, a Adobe recomenda que você use uma conta corporativa em vez de uma conta de email pessoal.
   > * O aplicativo **Somente contas pessoais Microsoft®** não é suportado.
   > * A Adobe recomenda que você use o aplicativo **Conta pessoal e de vários locatários da Microsoft®**.

1. Em seguida, acesse **Certificados e segredos**, clique em **Novo segredo de cliente** e siga as etapas na tela para criar um segredo. Anote esse valor de secret para uso posterior.

   ![Chave secreta](/help/forms/using/assets/azure_secretkey.png)

1. Para adicionar permissões, vá para o aplicativo recém-criado e selecione **Permissões de API** > **Adicionar uma Permissão** > **Gráfico Microsoft®** > **Permissões Delegadas**.
1. Marque as caixas de seleção das permissões abaixo para o aplicativo e clique em **Adicionar permissão**:

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![Permissão de API](/help/forms/using/assets/azure_apipermission.png)

1. Selecione **Autenticação** > **Adicionar uma plataforma** > **Web** e, na seção **Redirecionar URLs**, adicione qualquer um dos URIs abaixo (Identificador Universal de Recursos) como:
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   Nesse caso, `https://login.microsoftonline.com/common/oauth2/nativeclient` é usado como um URI de redirecionamento.

1. Clique em **Configurar** depois de adicionar cada URL e defina suas configurações de acordo com seus requisitos.
   ![URI de redirecionamento](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > É obrigatório marcar as caixas de seleção **Tokens de acesso** e **Tokens de ID**.

1. Clique em **Visão geral** no painel esquerdo e copie os valores de **ID do Aplicativo (cliente)**, **ID do Diretório (locatário)** e **Segredo do Cliente** para uso posterior.

   ![Visão geral](/help/forms/using/assets/azure_overview.png)

## Geração do código de autorização {#generating-the-authorization-code}

Em seguida, você deve gerar o código de autorização, explicado nas seguintes etapas:

1. Abra a seguinte URL no navegador depois de substituir `clientID` por `<client_id>` e `redirect_uri` pelo URI de redirecionamento do seu aplicativo:

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   > Se houver um único aplicativo de locatário, substitua `common` por `[tenantid]` na seguinte URL para gerar o código de autorização: `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. Ao digitar o URL acima, você é redirecionado para a tela de logon:
   ![Tela de Login](/help/forms/using/assets/azure_loginscreen.png)

1. Digite o email, clique em **Avançar** e a tela de permissão do aplicativo será exibida:

   ![Permitir Permissão](/help/forms/using/assets/azure_permission.png)

1. Ao permitir permissão, você será redirecionado para uma nova URL como: `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. Copie o valor de `<code>` da URL acima de `0.ASY...` para `&session_state` na URL acima.

## Geração do token de atualização {#generating-the-refresh-token}

Em seguida, você deve gerar o token de atualização, explicado nas seguintes etapas:

1. Abra o prompt de comando e use o seguinte comando cURL para obter o refreshToken.

1. Substitua os `clientID`, `client_secret` e `redirect_uri` pelos valores do seu aplicativo junto com o valor de `<code>`:

   `curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   > Em um único aplicativo de locatário, para gerar um token de atualização, use o seguinte comando cURL e substitua `common` por `[tenantid]` em:
   >`curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. Anote o token de atualização.

## Configurar o serviço de e-mail com suporte ao OAuth 2.0 {#configureemailservice}

Agora, configure o serviço de e-mail no servidor JEE mais recente fazendo logon na interface do usuário do administrador:

1. Vá para **Início** > **Serviço** > **Aplicativos e Serviços** > **Gerenciamento de Serviços** > **Serviço de Email**, a janela **Serviço de Email de Configuração** é exibida, configurada para autenticação básica.

   >[!NOTE]
   >
   > Para habilitar o serviço de autenticação oAuth 2.0, é obrigatório marcar **Se o servidor SMTP requer autenticação (Autenticação SMTP)**.

1. Definir **Configurações de Autenticação 2.0** como `True`.
1. Copie os valores de **ID do Cliente** e **Segredo do Cliente** do Portal do Azure.
1. Copie o valor do **Token de Atualização** gerado.
1. Faça logon no **Workbench** e pesquise o **Email 1.0** no **Seletor de atividades**.
1. Três opções estão disponíveis no Email 1.0 como:
   * **Enviar com Documento**: Envia emails com anexos únicos.
   * **Enviar com Mapa de Anexos**: envia emails com vários anexos.
   * **Receber**: recebe um email do IMAP.

   >[!NOTE]
   >
   >* O protocolo Transport Security tem os seguintes valores válidos: &quot;blank&quot;, &quot;SSL&quot; ou &quot;TLS&quot;. Defina os valores de **Segurança de Transporte SMTP** e **Segurança de Transporte de Recebimento** como **TLS** para habilitar o serviço de autenticação oAuth.
   >* O **protocolo POP3** não tem suporte para OAuth ao usar pontos de extremidade de email.

   ![Configurações de Conexão](/help/forms/using/assets/oauth_connectionsettings.png)

1. Teste o aplicativo selecionando **Enviar com Documento**.
1. Forneça os endereços **TO** e **From**.
1. Chame o aplicativo e um email será enviado usando a autenticação 0Auth 2.0.

   >[!NOTE]
   >
   >Se desejar, é possível alterar a configuração Autenticação 2.0 para autenticação básica para um processo específico em um workbench. Para fazer isso, defina o valor **Autenticação OAuth 2.0** como &#39;Falso&#39; em **Usar configurações globais** na guia **Configurações de Conexão**.

## Para ativar notificações de tarefas oAuth {#enable_oauth_task}

1. Ir para **Página Inicial** > **Serviços** > **Fluxo de Trabalho do Formulário** > **Configurações do Servidor** > **Configurações de Email**
1. Para habilitar notificações de tarefas oAuth, marque a caixa de seleção **Habilitar oAuth**.
1. Copie os valores de **ID do Cliente** e **Segredo do Cliente** do Portal do Azure.
1. Copie o valor do **Token de Atualização** gerado.
1. Clique em **Salvar** para salvar os detalhes.

   ![Notificação de tarefa](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > Para saber mais informações relacionadas às notificações de tarefas, [clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/administrator-help/configuring-email-endpoints.html?lang=pt-BR#create-an-email-endpoint-for-the-complete-task-service).

## Para configurar o terminal de email {#configure_email_endpoint}

1. Ir para **Página Inicial** > **Serviços** > **Aplicativos e Serviços** > **Gerenciamento de Ponto de Extremidade**
1. Para configurar o ponto de extremidade de email, defina **oAuth 2.0 Configurações de Autenticação** como `True`.
1. Copie os valores de **ID do Cliente** e **Segredo do Cliente** do Portal do Azure.
1. Copie o valor do **Token de Atualização** gerado.
1. Clique em **Salvar** para salvar os detalhes.

   ![Configurações de Conexão](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > Para saber mais sobre como configurar pontos de extremidade de email, clique em [Configurar um ponto de extremidade de email](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/administrator-help/configuring-email-endpoints.html?lang=pt-BR).

## Resolução de problemas {#troubleshooting}

* Se o serviço de email não estiver funcionando corretamente, tente gerar novamente o `Refresh Token` conforme descrito acima. Levará alguns minutos para o novo valor ser implantado.

* Erro ao configurar detalhes do servidor de email no endpoint de email usando o Workbench. Tente configurar o endpoint por meio da interface do Administrador em vez do Workbench.
