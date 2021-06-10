---
title: Configuração de notificação por email
seo-title: Configuração de notificação por email
description: Saiba como configurar a Notificação por email no AEM.
seo-description: Saiba como configurar a Notificação por email no AEM.
uuid: 6cbdc312-860b-4a69-8bbe-2feb32204a27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6466d7b8-e308-43c5-acdc-dec15f796f64
exl-id: 918fcbbc-a78a-4fab-a933-f183ce6a907f
source-git-commit: 2a866e82a059184ea86f22646e4a20406ad109e8
workflow-type: tm+mt
source-wordcount: '2097'
ht-degree: 1%

---

# Configurar a notificação por email{#configuring-email-notification}

O AEM envia notificações por email para usuários que:

* Inscreveram-se em eventos de página, por exemplo, modificação ou replicação. A seção [Caixa de entrada de notificações](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) descreve como assinar esses eventos.

* Inscreveram-se nos eventos do fórum.
* É necessário executar uma etapa em um fluxo de trabalho. A seção [Etapa do participante](/help/sites-developing/workflows-step-ref.md#participant-step) descreve como acionar a notificação por email em um workflow.

Pré-requisitos:

* Os usuários precisam ter um endereço de email válido definido em seu perfil.
* O **Day CQ Mail Service** precisa ser configurado corretamente.

Quando um usuário é notificado, ele recebe um email no idioma definido em seu perfil. Cada idioma tem seu próprio modelo que pode ser personalizado. Novos modelos de email podem ser adicionados para novos idiomas.

>[!NOTE]
>
>Ao trabalhar com AEM, existem vários métodos de gestão das definições de configuração para esses serviços; consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

## Configuração do serviço de email {#configuring-the-mail-service}

Para que o AEM possa enviar emails, o **Day CQ Mail Service** precisa ser configurado corretamente. Você pode exibir a configuração no console da Web. Ao trabalhar com AEM, existem vários métodos de gestão das definições de configuração para esses serviços; consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

As seguintes restrições se aplicam:

* A **porta do servidor SMTP** deve ser 25 ou superior.

* O **nome do host do servidor SMTP** não deve estar em branco.
* O endereço **&quot;From&quot;** não deve estar em branco.

Para ajudar você a depurar um problema com o **Day CQ Mail Service**, você pode assistir aos logs do serviço:

`com.day.cq.mailer.DefaultMailService`

A configuração é a seguinte no console da Web:

![chlimage_1-276](assets/chlimage_1-276.png)

## Configuração do canal de notificação por email {#configuring-the-email-notification-channel}

Ao assinar notificações de eventos de página ou de fórum, o endereço de email de formulário é definido como `no-reply@acme.com` por padrão. Você pode alterar esse valor configurando o serviço **Canal de email de notificação** no Console da Web.

Para configurar o endereço de e-mail from, adicione um nó `sling:OsgiConfig` ao repositório. Use o procedimento a seguir para adicionar o nó diretamente usando o CRXDE Lite:

1. No CRXDE Lite, adicione uma pasta chamada `config` abaixo da pasta do aplicativo.
1. Na pasta de configuração, adicione um nó chamado:

   `com.day.cq.wcm.notification.email.impl.EmailChannel` de tipo  `sling:OsgiConfig`

1. Adicione uma propriedade `String` ao nó chamado `email.from`. Para o valor , especifique o endereço de email que deseja usar.

1. Clique em **Salvar tudo**.

Use o procedimento a seguir para definir o nó nas pastas de origem do pacote de conteúdo:

1. Em `jcr_root/apps/*app_name*/config folder`, crie um arquivo chamado `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

1. Adicione o seguinte XML para representar o nó:

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. Substitua o valor do atributo `email.from` ( `name@server.com`) pelo seu endereço de email.

1. Salve o arquivo.

## Configuração do Serviço de Notificação por Email do Workflow {#configuring-the-workflow-email-notification-service}

Quando você recebe notificações por email do workflow, o endereço de email de e o prefixo do URL de host são definidos como valores padrão. Você pode alterar esses valores configurando o **Day CQ Workflow Email Notification Service** no Console da Web. Se isso for feito, é recomendável manter a alteração no repositório.

A configuração padrão é a seguinte no Console da Web:

![chlimage_1-277](assets/chlimage_1-277.png)

### Modelos de email para notificação de página {#email-templates-for-page-notification}

Os modelos de email para notificações de página estão localizados abaixo:

`/etc/notification/email/default/com.day.cq.wcm.core.page`

O modelo inglês padrão ( `en.txt`) é definido da seguinte maneira:

```xml
subject=[CQ Page Event Notification]: Page Event

header=-------------------------------------------------------------------------------------\n \
Time: ${time}\n \
User: ${userFullName} (${userId})\n \
-------------------------------------------------------------------------------------\n\n

message=The following pages were affected by the event: \n \
 \n \
${modifications} \n \
 \n\n
footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### Personalização de modelos de email para notificação de página {#customizing-email-templates-for-page-notification}

Para personalizar o modelo de email em inglês para notificação de página:

1. No CRXDE, abra o arquivo :

   `/etc/notification/email/default/com.day.cq.wcm.core.page/en.txt`

1. Modifique o arquivo de acordo com suas necessidades.
1. Salve as alterações.

O modelo precisa ter o seguinte formato:

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

Onde &lt;text_x> pode ser uma combinação de texto estático e variáveis de sequência dinâmica. As variáveis a seguir podem ser usadas no modelo de email para notificações de página:

* `${time}`, a data e a hora do evento.

* `${userFullName}`, o nome completo do usuário que acionou o evento.

* `${userId}`, a ID do usuário que acionou o evento.
* `${modifications}`, descreve o tipo do evento de página e o caminho da página no formato :

   &lt;page event=&quot;&quot; type=&quot;&quot;> =>  &lt;page path=&quot;&quot;>

   Por exemplo:

   PageModified => /content/geometrixx/en/products

### Modelos de email para notificação do fórum {#email-templates-for-forum-notification}

Os modelos de email para notificações de fórum estão localizados em:

`/etc/notification/email/default/com.day.cq.collab.forum`

O modelo inglês padrão ( `en.txt`) é definido da seguinte maneira:

```xml
subject=[CQ Forum Notification]

header=-------------------------------------------------------------------------------------\n \
Time: Time: ${time}\n \
Forum Page Path: ${forum.path}\n \
-------------------------------------------------------------------------------------\n\n

message=Page: ${host.prefix}${forum.path}.html\n

footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### Personalização de modelos de email para notificação do fórum {#customizing-email-templates-for-forum-notification}

Para personalizar o modelo de email em inglês para notificação do fórum:

1. No CRXDE, abra o arquivo :

   `/etc/notification/email/default/com.day.cq.collab.forum/en.txt`

1. Modifique o arquivo de acordo com suas necessidades.
1. Salve as alterações.

O modelo precisa ter o seguinte formato:

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

Onde `<text_x>` pode ser uma combinação de texto estático e variáveis de sequência dinâmica.

As variáveis a seguir podem ser usadas no modelo de email para notificações do fórum:

* `${time}`, a data e a hora do evento.

* `${forum.path}`, o caminho para a página do fórum.

### Modelos de email para notificação de fluxo de trabalho {#email-templates-for-workflow-notification}

O modelo de email para notificações de workflow (inglês) está localizado em:

`/etc/workflow/notification/email/default/en.txt`

É definido da seguinte forma:

```xml
subject=Workflow notification: ${event.EventType}

header=-------------------------------------------------------------------------------------\n \
Time: ${event.TimeStamp}\n \
Step: ${item.node.title}\n \
User: ${participant.name} (${participant.id})\n \
Workflow: ${model.title}\n \
-------------------------------------------------------------------------------------\n\n

message=Content: ${host.prefix}${payload.path.open}\n

footer=\n \
-------------------------------------------------------------------------------------\n \
View the overview in your ${host.prefix}/aem/inbox\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### Personalização de modelos de email para notificação de fluxo de trabalho {#customizing-email-templates-for-workflow-notification}

Para personalizar o modelo de email em inglês para notificação de evento de workflow:

1. No CRXDE, abra o arquivo :

   `/etc/workflow/notification/email/default/en.txt`

1. Modifique o arquivo de acordo com suas necessidades.
1. Salve as alterações.

O modelo precisa ter o seguinte formato:

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>Onde `<text_x>` pode ser uma combinação de texto estático e variáveis de sequência dinâmica. Cada linha de um item `<text_x>` precisa ser finalizada com uma barra invertida ( `\`), exceto para a última instância, quando a ausência da barra invertida indicar o fim da variável da string `<text_x>`.
>
>Mais informações sobre o formato do modelo podem ser encontradas no [javadocs do método Properties.load()](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-).

O método `${payload.path.open}` revela o caminho para a carga do item de trabalho. Por exemplo, para uma página em Sites , então `payload.path.open` seria semelhante a `/bin/wcmcommand?cmd=open&path=…`.; isso é sem o nome do servidor, e é por isso que o modelo prepara isso com `${host.prefix}`.

As variáveis a seguir podem ser usadas no modelo de email:

* `${event.EventType}`, tipo de evento
* `${event.TimeStamp}`, data e hora do evento
* `${event.User}`, o usuário que acionou o evento
* `${initiator.home}`, o caminho do nó iniciador

* `${initiator.name}`, o nome do iniciador

* `${initiator.email}`, endereço de email do iniciador
* `${item.id}`, a id do item de trabalho
* `${item.node.id}`, id do nó no modelo de fluxo de trabalho associado a este item de trabalho
* `${item.node.title}`, título do item de trabalho
* `${participant.email}`, endereço de e-mail do participante
* `${participant.name}`nome do participante
* `${participant.familyName}`, nome familiar do participante
* `${participant.id}`, id do participante
* `${participant.language}`, a língua do participante
* `${instance.id}`, a id do fluxo de trabalho
* `${instance.state}`, o estado do fluxo de trabalho
* `${model.title}`, título do modelo de fluxo de trabalho
* `${model.id}`, a id do modelo de fluxo de trabalho

* `${model.version}`, a versão do modelo de fluxo de trabalho
* `${payload.data}`, a carga

* `${payload.type}`, o tipo de carga
* `${payload.path}`, caminho da carga
* `${host.prefix}`, prefixo do host, por exemplo: http://localhost:4502

### Adicionar um modelo de email para um novo idioma {#adding-an-email-template-for-a-new-language}

Para adicionar um modelo para um novo idioma:

1. No CRXDE, adicione um arquivo `<language-code>.txt` abaixo:

   * `/etc/notification/email/default/com.day.cq.wcm.core.page` : para notificações de página
   * `/etc/notification/email/default/com.day.cq.collab.forum` : para notificações do fórum
   * `/etc/workflow/notification/email/default` : para notificações de fluxo de trabalho

1. Adapte o arquivo ao idioma.
1. Salve as alterações.

>[!NOTE]
>
>O `<language-code>` usado como o nome do arquivo para o modelo de email precisa ser um código de idioma em letras minúsculas com duas letras reconhecido pelo AEM. Para códigos de idioma, o AEM depende do ISO-639-1.

## Configuração de notificações de email do AEM Assets {#assetsconfig}

Quando as coleções no AEM Assets são compartilhadas ou não, os usuários podem receber notificações por email do AEM. Para configurar notificações por email, siga estas etapas.

1. Configure o serviço de email, conforme descrito acima em [Configuração do serviço de email](/help/sites-administering/notification.md#configuring-the-mail-service).
1. Faça logon no AEM como administrador. Clique em **Ferramentas** > **Operações** > **Console da Web** para abrir a Configuração do Console da Web.
1. Edite **Day CQ DAM Resource Collection Servlet**. Selecione **enviar email**. Clique em **Salvar**.

## Configurando o OAuth {#setting-up-oauth}

O AEM oferece suporte ao OAuth2 para seu serviço de email integrado, a fim de permitir que as organizações adiram para proteger os requisitos de email.

Você pode configurar o OAuth para vários provedores de email, conforme descrito abaixo.

### Gmail {#gmail}

1. Crie seu projeto em `https://console.developers.google.com/projectcreate`
1. Selecione o projeto e vá para **APIs &amp; Services** - **Dashboard - Credenciais**
1. Configure a tela de consentimento do OAuth de acordo com seus requisitos
1. Na tela de atualização, adicione estes dois escopos:
   * `https://mail.google.com/`
   * `https://www.googleapis.com//auth/gmail.send`
1. Depois de adicionar os escopos, volte para **Credentials** no menu à esquerda e, em seguida, vá para **Create Credentials** - **OAuth Client ID** - **Desktop app**
1. Uma nova janela será aberta contendo a ID do cliente e o Segredo do cliente.
1. Salve essas credenciais.

**Configurações AEM Lado**

>[!NOTE]
>
>Os clientes do Adobe Managed Service podem trabalhar com o engenheiro de atendimento ao cliente para fazer essas alterações em ambientes de produção.

Primeiro, configure o Serviço de email:

1. Abra o Console da Web AEM acessando `http://serveraddress:serverport/system/console/configMgr`
1. Procure e clique em **Day CQ Mail Service**
1. Adicione as seguintes configurações:
   * Nome do host do servidor SMTP: `smtp.gmail.com`
   * Porta do Servidor SMTP: `25` ou `587`, dependendo dos requisitos
   * Marque as caixas de seleção para **SMPT use StarTLS** e **SMTP requer StarTLS**
   * Marque **Fluxo OAuth** e clique em **Salvar**.

Em seguida, configure seu provedor SMTP OAuth seguindo o procedimento abaixo:

1. Abra o Console da Web AEM acessando `http://serveraddress:serverport/system/console/configMgr`
1. Procure e clique em **Provedor SMTP OAuth2 do Corretor do CQ Mailer**
1. Preencha as informações necessárias da seguinte maneira:
   * URL de autorização: `https://accounts.google.com/o/oauth2/auth`
   * URL do token: `https://accounts.google.com/o/oauth2/token`
   * Escopos: `https://www.googleapis.com/auth/gmail.send` e `https://mail.google.com/`. Você pode adicionar mais de um escopo pressionando o botão **+** no lado direito de cada escopo configurado.
   * ID do cliente e Segredo do cliente: configure esses campos com os valores recuperados conforme descrito no parágrafo acima.
   * URL do token de atualização: `https://accounts.google.com/o/oauth2/token`
   * Atualizar Expiração do Token: never
1. Clique em **Salvar**.

<!-- clarify refresh token expiry, currrently not present in the UI -->

Depois de configuradas, as configurações devem ficar assim:

![provedor smtp oauth](assets/oauth-smtpprov2.png)

Agora, ative os componentes do OAuth. Você pode fazer isso ao:

1. Acesse o console Componentes acessando este URL: `http://serveraddress:serverport/system/console/components`
1. Procure os seguintes componentes
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. Pressione o ícone Reproduzir à esquerda dos componentes

   ![componentes](assets/oauth-components-play.png)

Finalmente, confirme a configuração ao:

1. Vá para o endereço da instância de publicação e faça logon como administrador.
1. Abra uma nova guia no navegador e vá para `http://serveraddress:serverport/services/mailer/oauth2/authorize`. Isso o redirecionará para a página do seu provedor SMTP, neste caso Gmail.
1. Logon e consentimento para fornecer as permissões necessárias
1. Após o consentimento, o token será armazenado no repositório. Você pode acessá-lo em `accessToken` acessando diretamente esse URL na sua instância de publicação: `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth2 `
1. Repita o procedimento acima para cada instância de publicação

<!-- clarify if the ip/server address in the last procedure is that of the publish instance -->

### Microsoft Outlook {#microsoft-outlook}

1. Vá para [https://portal.azure.com/](https://portal.azure.com/) e faça logon.
1. Procure por **Azure Ative Diretory** na barra de pesquisa e clique no resultado. Como alternativa, você pode navegar diretamente para [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Clique em **Registro do Aplicativo** - **Novo Registro**

   ![](assets/oauth-outlook1.png)

1. Preencha as informações de acordo com seus requisitos e clique em **Register**
1. Vá para o aplicativo recém-criado e selecione **Permissões da API**
1. Vá para **Adicionar permissão** - **Permissão de gráfico** - **Permissões delegadas**
1. Selecione as permissões abaixo para seu aplicativo e clique em **Adicionar permissão**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. Vá para **Authentication** - **Add a platform** - **Web** e, na seção **Redirect Urls**, adicione o seguinte URL para redirecionar o código OAuth e pressione **Configure**:
   * `http://localhost:4503/services/mailer/oauth2/token`
1. Repita o procedimento acima para cada instância de publicação
1. Defina as configurações de acordo com seus requisitos
1. Em seguida, vá para **Certificados e Segredos**, clique em **Novo segredo de cliente** e siga as etapas na tela para criar um segredo. Anote este segredo para uso posterior
1. Pressione **Visão geral** no painel esquerdo e copie os valores para **ID de aplicativo (cliente)** e **ID de diretório (locatário)** para uso posterior

Para recapitular, você precisará das seguintes informações para configurar o OAuth2 para o serviço de Mailer no lado do AEM:

* O URL de autenticação, que será construído com a ID do locatário. Ele terá este formulário: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* O URL do token, que será construído com a ID do locatário. Ele terá este formulário: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* O URL de atualização, que será construído com a ID do locatário. Ele terá este formulário: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* A ID do cliente
* O Segredo Do Cliente

**Configurações AEM Lado**

Em seguida, integre suas configurações do OAuth2 com o AEM:

1. Vá para o Console da Web da sua instância local navegando para `http://serveraddress:serverport/system/console/configMgr`
1. Procure e clique em **Day CQ Mail Service**
1. Adicione as seguintes configurações:
   * Nome do host do servidor SMTP: `smtp.office365.com`
   * Usuário SMTP: seu nome de usuário no formato de email
   * Endereço &quot;De&quot;: O endereço de email a ser usado no campo &quot;De:&quot; das mensagens enviadas pelo remetente
   * Porta do Servidor SMTP: `25` ou `587` dependendo dos requisitos
   * Marque as caixas de seleção para **SMPT use StarTLS** e **SMTP requer StarTLS**
   * Marque **Fluxo OAuth** e clique em **Salvar**.
1. Procure e clique em **Provedor SMTP OAuth2 do Corretor do CQ Mailer**
1. Preencha as informações necessárias da seguinte maneira:
   * Preencha o Url de Autorização, o Url de Token e o URL de Token de Atualização, construindo-os conforme descrito em [no final deste procedimento](#microsoft-outlook)
   * ID do cliente e Segredo do cliente: configure esses campos com os valores recuperados conforme descrito acima.
   * Adicione os seguintes escopos à configuração:
      * openid
      * offline_access
      * `https://outlook.office365.com/Mail.Send`
      * `https://outlook.office365.com/Mail.Read`
      * `https://outlook.office365.com/SMTP.Send`
   * Url De Redirecionamento AuthCode: `http://localhost:4503/services/mailer/oauth2/token`
   * Atualizar URL do token: isso deve ter o mesmo valor do Url de Token acima
1. Clique em **Salvar**.

Depois de configuradas, as configurações devem ficar assim:

![](assets/oauth-outlook-smptconfig.png)

Agora, ative os componentes do OAuth. Você pode fazer isso ao:

1. Acesse o console Componentes acessando este URL: `http://serveraddress:serverport/system/console/components`
1. Procure os seguintes componentes
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. Pressione o ícone Reproduzir à esquerda dos componentes

![componentes2](assets/oauth-components-play.png)

Finalmente, confirme a configuração ao:

1. Vá para o endereço da instância de publicação e faça logon como administrador.
1. Abra uma nova guia no navegador e vá para `http://serveraddress:serverport/services/mailer/oauth2/authorize`. Isso o redirecionará para a página do seu provedor SMTP, neste caso Gmail.
1. Logon e consentimento para fornecer as permissões necessárias
1. Após o consentimento, o token será armazenado no repositório. Você pode acessá-lo em `accessToken` acessando diretamente esse URL na sua instância de publicação: `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth2 `