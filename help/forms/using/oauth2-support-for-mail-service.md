---
title: Suporte OAuth2 para o serviço de email
description: Suporte Oauth2 para o serviço de email
source-git-commit: 081b0c70ceca0502cb84d7e1b68b0b12dc45a4e7
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 47%

---

# Suporte OAuth2 para o serviço de email {#oauth2-support-for-the-mail-service}

O AEM as a Cloud Service oferece suporte do OAuth2 para seu serviço de email integrado, a fim de permitir que as organizações cumpram com os requisitos de segurança de emails.

Você pode configurar o OAuth para vários provedores de email. Abaixo estão as instruções passo a passo para configurar o Serviço de email do AEM para autenticar via OAuth2 com o Microsoft Office 365 Outlook. Outros fornecedores podem ser configurados de maneira semelhante.

## Microsoft Outlook {#microsoft-outlook}

1. Acesse [https://portal.azure.com/](https://portal.azure.com/) e faça logon.
1. Pesquise por **Azure Active Directory** na barra de pesquisa e clique no resultado. Como alternativa, você pode navegar diretamente para [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Clique em **Registro do aplicativo** - **Novo registro**

   ![](/help/forms/using/assets/outh_outlook.PNG)

1. Preencha as informações de acordo com suas necessidades e clique em **Registrar**
1. Acesse o aplicativo recém-criado e selecione **Permissões de API**
1. Vá em **Adicionar permissão** - **Permissão de gráfico** - **Permissões delegadas**
1. Selecione as permissões abaixo para seu aplicativo e clique em **Adicionar permissão**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. Vá em **Autenticação** - **Adicionar uma plataforma** - **Web** e na seção **Redirecionar URLs**, adicione os URLs abaixo - um com e um sem a barra:
   * `http://localhost/`
   * `http://localhost`
1. Pressione **Configurar** depois de adicionar cada URL e defina as configurações de acordo com seus requisitos
1. Em seguida, acesse **Certificados e Segredos**, clique em **Novo segredo de cliente** e siga as etapas na tela para criar um segredo. Anote este segredo para uso posterior
1. Press **Visão geral** no painel esquerdo e copie os valores para **ID do aplicativo (cliente)** para uso posterior.

Para recapitular, você precisa das seguintes informações para configurar o OAuth2 para o serviço de Email no lado do AEM:

* O URL de autenticação no formulário: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/authorize`
* O URL do token no formulário: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* O URL de atualização no formulário: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* A ID do cliente
* O segredo do cliente

### Geração do token de atualização {#generating-the-refresh-token}

Em seguida, é necessário gerar o token de atualização, conforme ilustrado em uma etapa subsequente.

Você pode fazer isso seguindo estas etapas:

1. Abra o seguinte URL no navegador após substituir `clientID` com os valores específicos da sua conta:

   ```https://login.microsoftonline.com/common/oauth2/v2/authorize?client_id=<client_id>&scope=IMAP.AccessAsUser.A;;%20POP.AccessAsUser.All%20SMTP.Send%20User.Read&response_type=code&redirect-uri=http://loginmicrosoftonline.com/common/outh2/nativeclient&prompt=login```

1. Permitir permissão, sempre que necessário.
1. O URL será redirecionado para um novo local, construído neste formato: `http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. Copie o valor de `<code>` no exemplo acima
1. Use o seguinte comando cURL para obter o refreshToken. Substitua clientID, clientSecret pelos valores de sua conta e valor de `<code>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client-id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=M.R3_BAY.1bf609bf-25b3-2fcd-d910-02e02c53bc
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=~1E8Q~cz-m6vgOb9m~SI.eF9jSVTbFUiP5f0” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. Anote o refreshToken e o accessToken.

### Validação dos tokens {#validating-the-tokens}

Antes de continuar a configurar o OAuth no lado do AEM, valide o accessToken e o refreshToken com o procedimento abaixo:

1. Gere o accessToken usando o refreshToken produzido no procedimento anterior. Você pode fazer isso com o seguinte curl e substituir os valores de `<client_id>`,`<client_secret>` juntamente com o `<refreshToken>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client_id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=<code>
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=<client_secret>
   &refresh_token=<refresh_token” 
   -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. Envie um email usando o accessToken para ver se ele está funcionando corretamente.

>[!NOTE]
>
> Você pode obter a coleção da API Postman [deste local](https://docs.microsoft.com/pt-br/azure/active-directory/develop/v2-oauth2-auth-code-flow).

### Configurar o serviço de email com suporte para Auth2.0 {#configureemailservice}

Agora, é necessário configurar o serviço de email no servidor JEE mais recente por meio do logon na interface do usuário do administrador:

1. Ir para **Início** - **Serviço** - **Aplicativos e serviços** - **Gerenciamento de serviços** - **Serviço de email**
1. **Serviço de email de configuração** for exibida, configure **SMPT** e **IMP** servidores para autenticação básica.
1. Para ativar o serviço de autenticação de correio do Outlook, selecione **Configurações de autenticação do oAuth 2.0** caixa de seleção.
1. Copie os valores de **ID do cliente** e **Segredo do cliente** do Portal do Azure.
1. Copie o valor de gerado **Atualizar Token**.
1. Clique em **Salvar** para salvar os detalhes.
1. Fazer logon no workbench e na pesquisa **Email 1.0** from **Seletor de atividade**.
1. Três opções estão disponíveis em Email 1.0 como:
   * **Enviar com Documento**: Envia Email com anexos únicos.
   * **Enviar com o mapa de anexos**: Envia Email com vários anexos.
   * **Receber**: Recebe um email do POP3 ou IMAP.
1. Teste o aplicativo selecionando **Enviar com Documento**
1. Fornecer **PARA** e **De** endereços.
1. Chame o aplicativo e o email é enviado usando a autenticação oAuth2.0.

>[!NOTE]
>
> Se você quiser alterar a configuração de autenticação Auth 2.0 para autenticação básica de um processo específico em um workbench, poderá desmarcar a opção **Autenticação oAuth2.0** caixa de seleção em **Usar configurações globais** no **Configurações de conexão** guia .

### Resolução de problemas {#troubleshooting}

Se o serviço de email não estiver funcionando corretamente, regenere a variável `refreshToken` conforme descrito acima. Leva alguns minutos para o novo valor ser implantado.


