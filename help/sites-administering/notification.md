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
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 1%

---


# Configuração de notificação por email{#configuring-email-notification}

AEM envia notificações por email para usuários que:

* Inscreveram-se em eventos de página, por exemplo, modificação ou replicação. A seção Caixa de entrada [de](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) notificação descreve como assinar esses eventos.

* Inscreveram-se nos eventos do fórum.
* É necessário executar uma etapa em um fluxo de trabalho. A seção Etapa [do](/help/sites-developing/workflows-step-ref.md#participant-step) participante descreve como acionar a notificação por email em um fluxo de trabalho.

Pré-requisitos:

* O(s) usuário(s) precisa(m) ter um endereço de email válido definido em seu perfil.
* O Serviço **de Correio do** Day CQ precisa ser configurado corretamente.

Quando um usuário é notificado, ele recebe um email no idioma definido em seu perfil. Cada linguagem tem seu próprio modelo que pode ser personalizado. Novos modelos de e-mail podem ser adicionados para novos idiomas.

>[!NOTE]
>
>When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

## Configuração do serviço de e-mail {#configuring-the-mail-service}

Para que o AEM possa enviar emails, o **Day CQ Mail Service** precisa ser configurado corretamente. Você pode visualização a configuração no console da Web. When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

As seguintes restrições se aplicam:

* A porta **do servidor** SMTP deve ser 25 ou superior.

* O nome **do host do servidor** SMTP não deve estar em branco.
* O endereço **** &quot;De&quot; não deve estar em branco.

Para ajudá-lo a depurar um problema com o **Day CQ Mail Service**, você pode observar os registros do serviço:

`com.day.cq.mailer.DefaultMailService`

A configuração é a seguinte no console da Web:

![chlimage_1-276](assets/chlimage_1-276.png)

## Configuração do Canal de notificação por email {#configuring-the-email-notification-channel}

Quando você assina notificações de eventos de página ou de fórum, o endereço de e-mail de é definido como `no-reply@acme.com` por padrão. Você pode alterar esse valor configurando o serviço de Canal **de Email de** Notificação no Console da Web.

Para configurar o endereço de e-mail do, adicione um `sling:OsgiConfig` nó ao repositório. Use o seguinte procedimento para adicionar o nó diretamente usando o CRXDE Lite:

1. No CRXDE Lite, adicione uma pasta com o nome `config` abaixo da pasta do aplicativo.
1. Na pasta de configuração, adicione um nó chamado:

   `com.day.cq.wcm.notification.email.impl.EmailChannel` do tipo `sling:OsgiConfig`

1. Adicione uma `String` propriedade ao nó nomeado `email.from`. Para o valor, especifique o endereço de email que deseja usar.

1. Clique em **Salvar tudo**.

Use o seguinte procedimento para definir o nó nas pastas de origem do pacote de conteúdo:

1. Em seu site `jcr_root/apps/*app_name*/config folder`, crie um arquivo chamado `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

1. Adicione o seguinte XML para representar o nó:

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. Substitua o valor do `email.from` atributo ( `name@server.com`) pelo seu endereço de email.

1. Salve o arquivo.

## Configuração do Serviço de Notificação por Email do Fluxo de Trabalho {#configuring-the-workflow-email-notification-service}

Quando você recebe notificações por e-mail do fluxo de trabalho, tanto o endereço de e-mail de e-mail quanto o prefixo do URL do host são definidos como valores padrão. Você pode alterar esses valores configurando o Serviço **de Notificação por Email do Fluxo de Trabalho do** Day CQ no Console da Web. Se você fizer isso, é recomendável persistir na alteração no repositório.

A configuração padrão é a seguinte no Console da Web:

![chlimage_1-277](assets/chlimage_1-277.png)

### Modelos de e-mail para notificação de página {#email-templates-for-page-notification}

Os modelos de e-mail para notificações de página estão localizados abaixo:

`/etc/notification/email/default/com.day.cq.wcm.core.page`

O modelo padrão em inglês ( `en.txt`) é definido como a seguir:

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

Em que &lt;text_x> pode ser uma combinação de texto estático e variáveis de string dinâmica. As variáveis a seguir podem ser usadas no modelo de email para notificações de página:

* `${time}`, a data e a hora do evento.

* `${userFullName}`, o nome completo do usuário que acionou o evento.

* `${userId}`, a ID do usuário que acionou o evento.
* `${modifications}`, descreve o tipo de evento de página e o caminho da página no formato:

   &lt;tipo de evento da página> => &lt;caminho da página>

   Por exemplo:

   PageModified => /content/geometrixx/br/products

### Modelos de e-mail para notificação do fórum {#email-templates-for-forum-notification}

Os modelos de e-mail para notificações de fórum estão localizados em:

`/etc/notification/email/default/com.day.cq.collab.forum`

O modelo padrão em inglês ( `en.txt`) é definido como a seguir:

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

#### Personalização de modelos de e-mail para notificação do fórum {#customizing-email-templates-for-forum-notification}

Para personalizar o modelo de email em inglês para notificação do fórum:

1. No CRXDE, abra o arquivo:

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

Onde `<text_x>` pode ser uma combinação de texto estático e variáveis de string dinâmica.

As variáveis a seguir podem ser usadas no modelo de email para notificações do fórum:

* `${time}`, a data e a hora do evento.

* `${forum.path}`, o caminho para a página do fórum.

### Modelos de e-mail para notificação de fluxo de trabalho {#email-templates-for-workflow-notification}

O modelo de e-mail para notificações de fluxo de trabalho (inglês) está localizado em:

`/etc/workflow/notification/email/default/en.txt`

É definido como segue:

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

#### Personalização de modelos de e-mail para notificação de fluxo de trabalho {#customizing-email-templates-for-workflow-notification}

Para personalizar o modelo de e-mail em inglês para notificação de evento de fluxo de trabalho:

1. No CRXDE, abra o arquivo:

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
>Onde `<text_x>` pode ser uma combinação de texto estático e variáveis de string dinâmica. Cada linha de um `<text_x>` item precisa ser encerrada com uma barra invertida ( `\`), exceto pela última instância, quando a ausência da barra invertida indicar o fim da variável de `<text_x>` string.
>
>Mais informações sobre o formato do modelo podem ser encontradas nos [javadocs do método Properties.load()](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-) .

O método `${payload.path.open}` revela o caminho para a carga do item de trabalho. Por exemplo, para uma página em Sites, então `payload.path.open` seria semelhante a `/bin/wcmcommand?cmd=open&path=…`.; isso sem o nome do servidor, razão pela qual o modelo prepara isso com `${host.prefix}`.

As seguintes variáveis podem ser usadas no modelo de email:

* `${event.EventType}`, tipo de evento
* `${event.TimeStamp}`, data e hora do evento
* `${event.User}`, o usuário que acionou o evento
* `${initiator.home}`, o caminho do nó iniciador

* `${initiator.name}`, o nome do iniciador

* `${initiator.email}`, endereço de email do iniciador
* `${item.id}`, a ID do item de trabalho
* `${item.node.id}`, ID do nó no modelo de fluxo de trabalho associado a este item de trabalho
* `${item.node.title}`, título do item de trabalho
* `${participant.email}`, endereço de e-mail do participante
* `${participant.name}`nome do participante
* `${participant.familyName}`, nome da família do participante
* `${participant.id}`, id do participante
* `${participant.language}`, a língua do participante
* `${instance.id}`, a ID do fluxo de trabalho
* `${instance.state}`, o estado do fluxo de trabalho
* `${model.title}`, título do modelo de fluxo de trabalho
* `${model.id}`, a ID do modelo de fluxo de trabalho

* `${model.version}`, a versão do modelo de fluxo de trabalho
* `${payload.data}`, a carga

* `${payload.type}`, o tipo de carga
* `${payload.path}`, o caminho da carga
* `${host.prefix}`, prefixo do host, por exemplo: http://localhost:4502

### Adicionando um modelo de email para um novo idioma {#adding-an-email-template-for-a-new-language}

Para adicionar um modelo para um novo idioma:

1. No CRXDE, adicione um arquivo `<language-code>.txt` abaixo:

   * `/etc/notification/email/default/com.day.cq.wcm.core.page` : para notificações de página
   * `/etc/notification/email/default/com.day.cq.collab.forum` : para notificações do fórum
   * `/etc/workflow/notification/email/default` : para notificações de fluxo de trabalho

1. Adapte o arquivo ao idioma.
1. Salve as alterações.

>[!NOTE]
>
>O nome de arquivo `<language-code>` usado como o modelo de email precisa ser um código de idioma em minúsculas de duas letras reconhecido pela AEM. Para códigos de idioma, AEM depende do ISO-639-1.

## Configuração de notificações por email da AEM Assets {#assetsconfig}

Quando as coleções no AEM Assets são compartilhadas ou não, os usuários podem receber notificações por email da AEM. Para configurar notificações por email, siga estas etapas.

1. Configure o serviço de e-mail, conforme descrito acima em [Configuração do serviço](/help/sites-administering/notification.md#configuring-the-mail-service)de e-mail.
1. Efetue login no AEM como um administrador. Clique em **Ferramentas** > **Operações** > Console **da Web** para abrir a Configuração do console da Web.
1. Editar Servlet **de Coleta de Recursos CQ DAM** Dia. Selecione **enviar e-mail**. Clique em **Salvar**.

