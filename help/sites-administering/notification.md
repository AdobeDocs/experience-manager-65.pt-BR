---
title: Configuração da notificação por e-mail
seo-title: Configuring Email Notification
description: Saiba como configurar a Notificação por email no AEM.
seo-description: Learn how to configure Email Notification in AEM.
uuid: 6cbdc312-860b-4a69-8bbe-2feb32204a27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6466d7b8-e308-43c5-acdc-dec15f796f64
exl-id: 918fcbbc-a78a-4fab-a933-f183ce6a907f
source-git-commit: 93dfac20bbb761abd580a004741ade20dc4ee2fe
workflow-type: tm+mt
source-wordcount: '2068'
ht-degree: 12%

---


# Configuração da notificação por e-mail{#configuring-email-notification}

O AEM envia notificações por email para usuários que:

* Ter se inscrito em eventos de página, por exemplo, modificação ou replicação. A variável [Caixa de entrada de notificações](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) descreve como se inscrever nesses eventos.

* Ter se inscrito nos eventos do fórum.
* É necessário executar uma etapa em um fluxo de trabalho. A variável [Etapa do participante](/help/sites-developing/workflows-step-ref.md#participant-step) descreve como acionar a notificação por email em um workflow.

Pré-requisitos:

* O(s) usuário(s) precisa(m) ter um endereço de email válido definido em seu perfil.
* A variável **Serviço de email Day CQ** precisa ser configurado corretamente.

Quando um usuário é notificado, ele recebe um email no idioma definido em seu perfil. Cada idioma tem seu próprio modelo que pode ser personalizado. Novos modelos de email podem ser adicionados para novos idiomas.

>[!NOTE]
>
>Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

## Configurando o serviço de e-mail {#configuring-the-mail-service}

Para que o AEM possa enviar emails, o **Serviço de email Day CQ** precisa ser configurado corretamente. Você pode exibir a configuração no console da Web. Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

As seguintes restrições se aplicam:

* A variável **Porta do servidor SMTP** deve ser 25 ou superior.

* A variável **Nome do host do servidor SMTP** não pode estar em branco.
* A variável **Endereço &quot;De&quot;** não pode estar em branco.

Para ajudar você a depurar um problema com o **Serviço de email Day CQ**, você pode assistir aos logs do serviço:

`com.day.cq.mailer.DefaultMailService`

A configuração tem a seguinte aparência no console da Web:

![A janela de configuração do OSGi do Day CQ Mail Service](assets/chlimage_1-276.png)

## Configuração do canal de notificação por email {#configuring-the-email-notification-channel}

Quando você se inscreve nas notificações de eventos de página ou fórum, o endereço de e-mail do remetente é definido como `no-reply@acme.com` por padrão. Você pode alterar esse valor configurando o **Canal de email de notificação** no Console da Web.

Para configurar o endereço de e-mail da, adicione um `sling:OsgiConfig` para o repositório. Use o procedimento a seguir para adicionar o nó diretamente usando o CRXDE Lite:

1. No CRXDE Lite, adicione uma pasta chamada `config` abaixo da pasta do aplicativo.
1. Na pasta de configuração, adicione um nó chamado:

   `com.day.cq.wcm.notification.email.impl.EmailChannel` do tipo `sling:OsgiConfig`

1. Adicionar um `String` para o nó chamado `email.from`. Para o valor, especifique o endereço de email que deseja usar.

1. Clique em **Salvar tudo**.

Use o procedimento a seguir para definir o nó nas pastas de origem do pacote de conteúdo:

1. No seu `jcr_root/apps/*app_name*/config folder`, crie um arquivo chamado `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

1. Adicione o seguinte XML para representar o nó:

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. Substitua o valor de `email.from` atributo ( `name@server.com`) com seu endereço de email.

1. Salve o arquivo.

## Configurar o serviço de notificação por email do fluxo de trabalho {#configuring-the-workflow-email-notification-service}

Ao receber notificações por email do fluxo de trabalho, o endereço de email do remetente e o prefixo do URL do host são definidos com valores padrão. Você pode alterar esses valores configurando o **Serviço de notificação por email do fluxo de trabalho do Day CQ** no Console da Web. Se você fizer isso, é recomendável manter a alteração no repositório.

A configuração padrão tem a seguinte aparência no Console da Web:

![A janela de configuração do Day CQ Workflow Email Notification Service](assets/chlimage_1-277.png)

### Modelos de email para notificação de página {#email-templates-for-page-notification}

Os modelos de email para notificações de página estão localizados abaixo:

`/libs/settings/notification-templates/com.day.cq.wcm.core.page`

O modelo padrão em inglês ( `en.txt`) é definida da seguinte forma:

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

#### Personalização de modelos de e-mail para notificação de página {#customizing-email-templates-for-page-notification}

Para personalizar o modelo de email em inglês para notificação de página:

1. No CRXDE, abra o arquivo:

   `/libs/settings/notification-templates/com.day.cq.wcm.core.page/en.txt`

1. Modifique o arquivo de acordo com suas necessidades.
1. Salve as alterações.

O template precisa ter o seguinte formato:

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

Onde &lt;text_x> pode ser uma combinação de texto estático e variáveis de string dinâmicas. As seguintes variáveis podem ser usadas no modelo de email para notificações de página:

* `${time}`, a data e a hora do evento.

* `${userFullName}`, o nome completo do usuário que acionou o evento.

* `${userId}`, a ID do usuário que acionou o evento.
* `${modifications}`, descreve o tipo de evento de página e o caminho da página no formato:

  &lt;page event=&quot;&quot; type=&quot;&quot;> => &lt;page path=&quot;&quot;>

  Por exemplo:

  PageModified => /content/geometrixx/en/products

### Modelos de email para notificação de fluxo de trabalho {#email-templates-for-workflow-notification}

O modelo de email para notificações de workflow (inglês) está localizado em:

`/libs/settings/workflow/notification/email/default/en.txt`

Ela é definida da seguinte maneira:

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

#### Personalização de modelos de e-mail para notificação de workflow {#customizing-email-templates-for-workflow-notification}

Para personalizar o template de email em inglês para notificação de eventos de workflow:

1. No CRXDE, abra o arquivo:

   `/libs/settings/workflow/notification/email/default/en.txt`

1. Modifique o arquivo de acordo com suas necessidades.
1. Salve as alterações.

O template precisa ter o seguinte formato:

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>Onde `<text_x>` pode ser uma combinação de texto estático e variáveis de string dinâmicas. Cada linha de um `<text_x>` o item precisa ser encerrado com uma barra invertida ( `\`), exceto na última instância, quando a ausência da barra invertida indicar o fim da `<text_x>` variável da string.
>
>Mais informações sobre o formato do modelo podem ser encontradas no [javadocs de Properties.load()](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-) método.

O método `${payload.path.open}` revela o caminho para a carga útil do item de trabalho. Por exemplo, para uma página no Sites, em seguida, `payload.path.open` seria semelhante a `/bin/wcmcommand?cmd=open&path=…`.; isso ocorre sem o nome do servidor, razão pela qual o modelo anexa isso `${host.prefix}`.

As seguintes variáveis podem ser usadas no template de email:

* `${event.EventType}`, tipo de evento
* `${event.TimeStamp}`, data e hora do evento
* `${event.User}`, o usuário que acionou o evento
* `${initiator.home}`, o caminho do nó do iniciador

* `${initiator.name}`, o nome do iniciador

* `${initiator.email}`, endereço de email do iniciador
* `${item.id}`, a id do item de trabalho
* `${item.node.id}`, id do nó no modelo de fluxo de trabalho associado a este item de trabalho
* `${item.node.title}`, título do item de trabalho
* `${participant.email}`, endereço de e-mail do participante
* `${participant.name}`, nome do participante
* `${participant.familyName}`, nome da família do participante
* `${participant.id}`, id do participante
* `${participant.language}`, o idioma do participante
* `${instance.id}`, a ID do fluxo de trabalho
* `${instance.state}`, o estado do workflow
* `${model.title}`, título do modelo de fluxo de trabalho
* `${model.id}`, a id do modelo de fluxo de trabalho

* `${model.version}`, a versão do modelo de fluxo de trabalho
* `${payload.data}`, a carga útil

* `${payload.type}`, o tipo de conteúdo
* `${payload.path}`, caminho da carga útil
* `${host.prefix}`, prefixo de host, por exemplo: `http://localhost:4502`

### Adicionando um modelo de email para um novo idioma {#adding-an-email-template-for-a-new-language}

Para adicionar um modelo para um novo idioma:

1. No CRXDE, adicione um arquivo `<language-code>.txt` abaixo:

   * `/libs/settings/notification-templates/com.day.cq.wcm.core.page` : para notificações de página
   * `/libs/settings/workflow/notification/email/default` : para notificações de workflow

1. Adapte o arquivo ao idioma.
1. Salve as alterações.

>[!NOTE]
>
>A variável `<language-code>` O usado como nome de arquivo para o modelo de email precisa ser um código de idioma de duas letras minúsculas, reconhecido pelo AEM. Para códigos de idioma, o AEM depende da ISO-639-1.

## Configuração de notificações por email do AEM Assets {#assetsconfig}

Quando as coleções no AEM Assets são compartilhadas ou não, os usuários podem receber notificações por email do AEM. Para configurar notificações por email, siga estas etapas.

1. Configure o serviço de email, conforme descrito acima em [Configurando o serviço de e-mail](/help/sites-administering/notification.md#configuring-the-mail-service).
1. Faça logon no AEM como administrador. Clique em **Ferramentas** >  **Operações** >  **Console da Web** para abrir a Configuração do console da Web.
1. Editar **Servlet de coleção de recursos DAM CQ diário**. Selecionar **enviar email**. Clique em **Salvar**.

## Configuração do OAuth {#setting-up-oauth}

A AEM oferece suporte do OAuth2 para seu serviço de email integrado, a fim de permitir que as organizações cumpram com os requisitos de segurança de emails.

Você pode configurar o OAuth para vários provedores de email, conforme descrito abaixo.

>[!NOTE]
>
>Esse procedimento é um exemplo para uma instância de publicação. Se quiser ativar notificações por email em uma instância de Autor, siga as mesmas etapas no Autor.

### Gmail {#gmail}

1. Crie seu projeto em `https://console.developers.google.com/projectcreate`
1. Selecione seu projeto e vá para **APIs e serviços** - **Painel - Credenciais**
1. Configure a Tela de consentimento do OAuth de acordo com suas necessidades
1. Na tela Atualizar a seguir, adicione estes dois escopos:
   * `https://mail.google.com/`
   * `https://www.googleapis.com//auth/gmail.send`
1. Depois de adicionar os escopos, volte para **Credenciais** no menu à esquerda, vá para **Criar credenciais** - **ID do cliente OAuth** - **Aplicativo de desktop**
1. Uma nova janela será aberta contendo a ID do cliente e o Segredo do cliente.
1. Salve essas credenciais.

**Configurações no lado do AEM**

>[!NOTE]
>
>Os clientes do Adobe Managed Service podem trabalhar com o engenheiro de atendimento ao cliente para fazer essas alterações nos ambientes de produção.

Primeiro, configure o Serviço de e-mail:

1. Abra o console da Web do AEM acessando `http://serveraddress:serverport/system/console/configMgr`
1. Procure por e clique em **Serviço de email Day CQ**
1. Adicione as seguintes configurações:
   * Nome do host do servidor SMTP: `smtp.gmail.com`
   * Porta do servidor SMTP: `25` ou `587`, dependendo dos requisitos
   * Marque as caixas de seleção para **SMPT usa StarTLS** e **SMTP requer StarTLS**
   * Marcar **Fluxo OAuth** e clique em **Salvar**.

Em seguida, configure o provedor SMTP OAuth seguindo o procedimento abaixo:

1. Abra o console da Web do AEM acessando `http://serveraddress:serverport/system/console/configMgr`
1. Procure por e clique em **Provedor OAuth2 SMTP do CQ Mailer**
1. Preencha as informações necessárias da seguinte maneira:
   * URL de autorização: `https://accounts.google.com/o/oauth2/auth`
   * URL do token: `https://accounts.google.com/o/oauth2/token`
   * Escopos: `https://www.googleapis.com/auth/gmail.send` e `https://mail.google.com/`. É possível adicionar mais de um escopo, pressionando o **+** no lado direito de cada escopo configurado.
   * ID do cliente e Segredo do cliente: configure esses campos com os valores que você recuperou, conforme descrito no parágrafo acima.
   * URL do token de atualização: `https://accounts.google.com/o/oauth2/token`
   * Expiração do token de atualização: nunca
1. Clique em **Salvar**.

<!-- clarify refresh token expiry, currently not present in the UI -->

Depois de definidas, as configurações devem ter esta aparência:

![A janela de configuração do Provedor CQ Mailer SMTP Oauth2](assets/oauth-smtpprov2.png)

Agora, ative os componentes OAuth. Você pode fazer isso ao:

1. Acesse o console Componentes visitando este URL: `http://serveraddress:serverport/system/console/components`
1. Procure os seguintes componentes
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. Pressione o ícone Reproduzir à esquerda dos componentes

   ![Lista de componentes que mostram o OAuthCodeGenerateServlet e o OAuthCodeAccessTokenGenerator](assets/oauth-components-play.png)

Por fim, confirme a configuração ao:

1. Ir para o endereço da instância de publicação e fazer logon como administrador.
1. Abra uma nova guia no navegador e vá para `http://serveraddress:serverport/services/mailer/oauth2/authorize`. Você será redirecionado para a página do seu provedor SMTP, neste caso, o Gmail.
1. Logon e consentimento para fornecer as permissões necessárias
1. Após o consentimento, o token será armazenado no repositório. Você pode acessá-lo em `accessToken` ao acessar diretamente esse URL na instância de publicação: `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
1. Repita o procedimento acima para cada instância de publicação

<!-- clarify if the ip/server address in the last procedure is that of the publish instance -->

### Microsoft Outlook {#microsoft-outlook}

1. Acesse [https://portal.azure.com/](https://portal.azure.com/) e faça logon.
1. Pesquise por **Azure Active Directory** na barra de pesquisa e clique no resultado. Como alternativa, você pode navegar diretamente para [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Clique em **Registro do aplicativo** - **Novo registro**

   ![O novo botão de registro ao configurar o Microsoft Outlook](assets/oauth-outlook1.png)

1. Preencha as informações de acordo com suas necessidades e clique em **Registrar**
1. Acesse o aplicativo recém-criado e selecione **Permissões de API**
1. Vá em **Adicionar permissão** - **Permissão de gráfico** - **Permissões delegadas**
1. Selecione as permissões abaixo para seu aplicativo e clique em **Adicionar permissão**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. Ir para **Autenticação** - **Adicionar uma plataforma** - **Web**, e no **URLs de redirecionamento** adicione o seguinte URL para redirecionar o código OAuth e pressione **Configurar**:
   * `http://localhost:4503/services/mailer/oauth2/token`
1. Repita o procedimento acima para cada instância de publicação
1. Defina as configurações de acordo com seus requisitos
1. Em seguida, vá em **Certificados e segredos**, clique em **Novo segredo de cliente** e siga as etapas na tela para criar um segredo. Anote este segredo para uso posterior
1. Pressione **Visão geral** no painel esquerdo e copie os valores de **ID do aplicativo (cliente)** e **ID do diretório (locatário)** para uso posterior

Para recapitular, você precisará das seguintes informações para configurar o OAuth2 para o serviço Mailer no lado do AEM:

* O URL de autenticação, que será construído com a ID do locatário. Ele terá este formato: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* O URL do token, que será construído com a ID do locatário. Ele terá este formato: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* O URL de atualização, que será construído com a ID do locatário. Ele terá este formato: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* A ID do cliente
* O segredo do cliente

**Configurações no lado do AEM**

Em seguida, integre suas configurações do OAuth2 com o AEM:

1. Vá para o Console da Web da instância local navegando até `http://serveraddress:serverport/system/console/configMgr`
1. Procure e clique em **Serviço de email Day CQ**
1. Adicione as seguintes configurações:
   * Nome do host do servidor SMTP: `smtp.office365.com`
   * Usuário SMTP: seu nome de usuário no formato de email
   * Endereço &quot;De&quot;: o endereço de email a ser usado no campo &quot;De:&quot; das mensagens enviadas pelo correio
   * Porta do servidor SMTP: `25` ou `587` dependendo dos requisitos
   * Marque as caixas de seleção para **SMPT usa StarTLS** e **SMTP requer StarTLS**
   * Marcar **Fluxo OAuth** e clique em **Salvar**.
1. Procure por e clique em **Provedor OAuth2 SMTP do CQ Mailer**
1. Preencha as informações necessárias da seguinte maneira:
   * Preencha o URL de autorização, URL do token e URL do token de atualização construindo-os conforme descrito em [no final deste procedimento](#microsoft-outlook)
   * ID do cliente e Segredo do cliente: configure esses campos com os valores que você recuperou, conforme descrito acima.
   * Adicione os seguintes escopos à configuração:
      * openid
      * offline_access
      * `https://outlook.office365.com/Mail.Send`
      * `https://outlook.office365.com/Mail.Read`
      * `https://outlook.office365.com/SMTP.Send`
   * URL de redirecionamento AuthCode: `http://localhost:4503/services/mailer/oauth2/token`
   * URL do token de atualização: deve ter o mesmo valor que o URL do token acima
1. Clique em **Salvar**.

Depois de definidas, as configurações devem ter esta aparência:

![A configuração OAuth2 do SMTP Mailer do CQ concluída](assets/oauth-outlook-smptconfig.png)

Agora, ative os componentes OAuth. Você pode fazer isso ao:

1. Acesse o console Componentes visitando este URL: `http://serveraddress:serverport/system/console/components`
1. Procure os seguintes componentes
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. Pressione o ícone Reproduzir à esquerda dos componentes

![Um trecho da lista de componentes que contém OAuthCodeGenerateServlet e OAuthCodeAccessTokenGenerator](assets/oauth-components-play.png)

Por fim, confirme a configuração ao:

1. Ir para o endereço da instância de publicação e fazer logon como administrador.
1. Abra uma nova guia no navegador e vá para `http://serveraddress:serverport/services/mailer/oauth2/authorize`. Você será redirecionado para a página do provedor SMTP, neste caso, para o Outlook.
1. Logon e consentimento para fornecer as permissões necessárias
1. Após o consentimento, o token será armazenado no repositório. Você pode acessá-lo em `accessToken` ao acessar diretamente esse URL na instância de publicação: `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
