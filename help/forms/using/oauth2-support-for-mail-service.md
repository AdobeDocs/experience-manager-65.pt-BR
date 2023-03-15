---
title: Configurar a autenticação baseada em OAuth2 para os protocolos de servidor de e-mail do Microsoft® Office 365
description: Configurar a autenticação baseada em OAuth2 para os protocolos de servidor de e-mail do Microsoft® Office 365
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
source-git-commit: d19de2955adef56570378a6d62ec0015718f9039
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 3%

---

# Integrar com os protocolos de servidor de e-mail do Microsoft® Office 365 {#oauth2-support-for-the-microsoft-mail-server-protocols}

Para permitir que as organizações adiram aos requisitos de email seguros, a AEM Forms oferece suporte ao OAuth 2.0 para integração com os protocolos de servidor de email Microsoft® Office 365. Você pode usar o serviço de autenticação OAuth 2.0 do Azure Ative Diretory (Azure AD) para se conectar com vários protocolos, como IMAP, POP ou SMTP, e acessar dados de email para usuários do Office 365. Abaixo estão as instruções passo a passo para configurar os protocolos do servidor de e-mail do Microsoft® Office 365 para autenticar via serviço OAuth 2.0:

1. Logon [https://portal.azure.com/](https://portal.azure.com/) e procurar **Ative Diretory do Azure** na barra de pesquisa e clique no resultado.
Como alternativa, você pode navegar diretamente para [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Clique em **Adicionar** > **Registro do aplicativo** > **Novo registro**

   ![Registro do aplicativo](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. Preencha as informações de acordo com seus requisitos e clique em **Registrar**.
   ![Conta Suportada](/help/forms/using/assets/azure_suuportedaccountype.png)
No caso acima, 
**Contas em qualquer diretório organizacional (Qualquer diretório do Azure AD - Multilocatário) e contas pessoais do Microsoft® (por exemplo, Skype, Xbox)** está selecionada.

   >[!NOTE]
   >
   > * Para **Contas em qualquer diretório organizacional (Qualquer diretório do Azure AD - Multilocatário)** , é recomendável usar a conta do trabalho em vez da conta de email pessoal.
   > * **Somente contas pessoais Microsoft®** não é suportado.
   > * Recomenda-se a utilização de **Vários locatários e conta pessoal da Microsoft®** aplicativo.


1. Em seguida, acesse **Certificados e Segredos**, clique em **Novo segredo de cliente** e siga as etapas na tela para criar um segredo. Anote esse valor de segredo para uso posterior.

   ![Chave secreta](/help/forms/using/assets/azure_secretkey.png)

1. Para adicionar permissões, acesse o aplicativo recém-criado e selecione **Permissões de API** > **Adicionar uma permissão** > **Gráfico Microsoft®** > **Permissões delegadas**
1. Marque as caixas de seleção para as permissões abaixo para o aplicativo e clique em **Adicionar permissão**:

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![Permissão da API](/help/forms/using/assets/azure_apipermission.png)

1. Selecionar **Autenticação** > **Adicionar uma plataforma** > **Web** e no **Urls De Redirecionamento** , adicione qualquer um dos URIs abaixo (Identificador de Recurso Universal) como:
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   Nesse caso, `https://login.microsoftonline.com/common/oauth2/nativeclient` é usado como um URI de redirecionamento.

1. Clique em **Configurar** depois de adicionar cada URL e definir suas configurações de acordo com seus requisitos.
   ![URI de redirecionamento](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > É obrigatório selecionar **Tokens de acesso** e **Tokens de ID** caixas de seleção.

1. Clique em **Visão geral** no painel esquerdo e copie os valores para **ID do aplicativo (cliente)**, **ID do diretório (locatário)** e **Segredo do cliente** para uso posterior.

   ![Visão geral](/help/forms/using/assets/azure_overview.png)

## Gerando o código de autorização {#generating-the-authorization-code}

Em seguida, você precisa gerar o código de autorização, explicado nas seguintes etapas:

1. Abra o seguinte URL no navegador após substituir `clientID` com o `<client_id>` e `redirect_uri` com o URI de redirecionamento do seu aplicativo:

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   > No caso do aplicativo de único locatário, substitua `common` com seu `[tenantid]` no seguinte URL para gerar código de autorização: `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. Quando você digitar o URL acima, será redirecionado para a tela de logon:
   ![Tela de logon](/help/forms/using/assets/azure_loginscreen.png)

1. Insira o email, clique em **Próximo** A tela de permissão e do aplicativo é exibida:

   ![Permitir permissão](/help/forms/using/assets/azure_permission.png)

1. Depois de permitir permissão, você é redirecionado para um novo URL como: `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. Copie o valor de `<code>` do URL acima de `0.ASY...` para `&session_state` no URL acima.

## Geração do token de atualização {#generating-the-refresh-token}

Em seguida, você precisa gerar o token de atualização, explicado nas seguintes etapas:

1. Abra o prompt de comando e use o seguinte comando cURL para obter o refreshToken.

1. Substitua o `clientID`, `client_secret` e `redirect_uri` com os valores para seu aplicativo, juntamente com o valor de `<code>`:

   `curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   > Em um único aplicativo de locatário, para gerar o token de atualização, use o seguinte comando cURL e substitua `common` com o `[tenantid]` em:
   >`curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. Anote o token de atualização.

## Configurar o serviço de email com suporte ao OAuth 2.0 {#configureemailservice}

Agora, é necessário configurar o serviço de email no servidor JEE mais recente por meio do logon na interface do usuário do administrador:

1. Ir para **Início** > **Serviço** > **Aplicativos e serviços** > **Gerenciamento de serviços** > **Serviço de email**, o **Serviço de email de configuração** for exibida, configurada para autenticação básica.

   >[!NOTE]
   >
   > Para ativar o serviço de autenticação oAuth 2.0, é obrigatório selecionar **Se o servidor SMTP requer autenticação (Autenticação SMTP)** caixa de seleção.

1. Definir **Configurações de autenticação do oAuth 2.0** as `True`.
1. Copie os valores de **ID do cliente** e **Segredo do cliente** do Portal do Azure.
1. Copie o valor de gerado **Atualizar Token**.
1. Faça logon em **Workbench** e pesquisa **Email 1.0** from **Seletor de atividade**.
1. Três opções estão disponíveis em Email 1.0 como:
   * **Enviar com Documento**: Envia Email com anexos únicos.
   * **Enviar com o mapa de anexos**: Envia Email com vários anexos.
   * **Receber**: Recebe um email do IMAP.

   >[!NOTE]
   >
   >* O protocolo de Segurança de Transporte tem valores válidos como: &#39;blank&#39;, &#39;SSL&#39; ou &#39;TLS&#39;. Você deve definir valores de **Segurança de transporte SMTP** e **Segurança de transporte de recepção** para **TLS** para habilitar o serviço de autenticação oAuth.
   >* **Protocolo POP3** não é compatível com o OAuth ao usar pontos de extremidade de email.


   ![Configurações de conexão](/help/forms/using/assets/oauth_connectionsettings.png)

1. Teste o aplicativo selecionando **Enviar com Documento**.
1. Fornecer **PARA** e **De** endereços.
1. Chame o aplicativo e o email é enviado usando a autenticação 0Auth 2.0.

   >[!NOTE]
   >
   >Se você quiser alterar a configuração de autenticação Auth 2.0 para autenticação básica de um processo específico em um workbench, poderá definir a variável **Autenticação OAuth 2.0** valor como &#39;False&#39; em **Usar configurações globais** no **Configurações de conexão** guia .

## Para ativar notificações de tarefa oAuth {#enable_oauth_task}

1. Ir para **Início** > **Serviços** > **Fluxo de trabalho do formulário** > **Configurações do servidor** > **Configurações de email**
1. Para ativar as notificações de tarefa oAuth, selecione o **Ativar oAuth** caixa de seleção.
1. Copie os valores de **ID do cliente** e **Segredo do cliente** do Portal do Azure.
1. Copie o valor de gerado **Atualizar Token**.
1. Clique em **Salvar** para salvar os detalhes.

   ![Notificação de tarefa](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > Para saber mais informações relacionadas a notificações de tarefa, [clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## Para configurar o ponto de extremidade de email {#configure_email_endpoint}

1. Ir para **Início** > **Serviços** > **Aplicativos e serviços** > **Gerenciamento de pontos de extremidade**
1. Para configurar o terminal de email, defina **Configurações de autenticação do oAuth 2.0** as `True`.
1. Copie os valores de **ID do cliente** e **Segredo do cliente** do Portal do Azure.
1. Copie o valor de gerado **Atualizar Token**.
1. Clique em **Salvar** para salvar os detalhes.

   ![Configurações de conexão](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > Para saber mais sobre como configurar endpoints de email, clique em [Configurar um ponto de extremidade de email](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html).

## Resolução de problemas {#troubleshooting}

* Se o serviço de email não estiver funcionando corretamente. Tente gerar novamente o `Refresh Token` conforme descrito acima. Leva alguns minutos para o novo valor ser implantado.

* Erro ao configurar os detalhes do servidor de email no ponto de extremidade do email usando o Workbench.Tente configurar o ponto de extremidade por meio da interface do usuário do administrador em vez do Workbench.
