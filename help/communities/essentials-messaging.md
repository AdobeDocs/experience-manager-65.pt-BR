---
title: Fundamentos das mensagens
seo-title: Messaging Essentials
description: Visão geral do componente Mensagens
seo-description: Messaging component overview
uuid: e0dad45e-d84d-4b28-b357-aded1c5d2605
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 98f70093-e786-4555-8aaa-d0df4c977dc0
docset: aem65
exl-id: b941b5e0-f768-4393-9a9d-ded2cd7d10c4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 3%

---

# Fundamentos das mensagens {#messaging-essentials}

Esta página documenta os detalhes de como trabalhar com o componente Mensagens para incluir um recurso de mensagens em um site.

## Fundamentos para o lado do cliente {#essentials-for-client-side}

**Escrever mensagem**

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/mensagens/componentes/hbs/composição</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientllibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/composemessage.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/clientlibs/composemessage.css</td>
  </tr>
  <tr>
   <td><strong>propriedades</strong></td>
   <td>Consulte <a href="/help/communities/configure-messaging.md" target="_blank">Configuração de mensagens</a></td>
  </tr>
  <tr>
   <td><strong>configuração do administrador</strong></td>
   <td><a href="/help/communities/messaging.md">Configuração de mensagens</a></td>
  </tr>
 </tbody>
</table>

**Lista de mensagens**

(para Caixa de entrada, Enviado e Lixeira)

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/mensagens/componentes/hbs/messagebox</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientllibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/messagebox.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/clientlibs/messagebox.css</td>
  </tr>
  <tr>
   <td><strong>propriedades</strong></td>
   <td>Consulte <a href="/help/communities/configure-messaging.md" target="_blank">Configuração de mensagens</a></td>
  </tr>
  <tr>
   <td><strong>configuração do administrador</strong></td>
   <td><a href="/help/communities/messaging.md" target="_blank">Configuração de mensagens</a></td>
  </tr>
 </tbody>
</table>

Consulte também [Personalizações do lado do cliente](/help/communities/client-customize.md)

## Fundamentos para o lado do servidor {#essentials-for-server-side}

* [Configuração de mensagens](/help/communities/configure-messaging.md)
* [Mensagens das APIs do cliente](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) para componentes do SCF
* [APIs de mensagens](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/api/package-summary.html) para o serviço
* [Endpoints de mensagens](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)
* [Personalizações do lado do servidor](/help/communities/server-customize.md)

>[!CAUTION]
>
>O parâmetro String deve *not* contém uma barra à direita &quot;/&quot; para os seguintes métodos do MessageBuilder:
>
>* `setInboxPath`()
>* `setSentItemsPath`()
>
>Por exemplo:
>
>
```
>valid: mb.setInboxPath( "/mail/inbox" );
> not valid: mb.setInboxPath( "/mail/inbox/" );
>```

### Site da comunidade {#community-site}

Uma estrutura de site da comunidade, criada por meio do assistente, inclui o recurso de mensagens quando selecionado. Consulte `User Management` de [Console de sites da comunidade](/help/communities/sites-console.md#user-management).

### Código de exemplo: Notificação recebida {#sample-code-message-received-notification}

O recurso Mensagens sociais lança eventos para operações, por exemplo `send`, `marking read`, `marking delete`. Esses eventos podem ser capturados e as ações executadas nos dados contidos no evento.

O exemplo a seguir é de um manipulador de eventos que escuta a variável `message sent` e envia um email para todos os recipients da mensagem usando o `Day CQ Mail Service`.

Para tentar o script de amostra do lado do servidor, é necessário um ambiente de desenvolvimento e a capacidade de criar um pacote OSGi:

1. Faça logon como administrador para ` [CRXDE|Lite](https://localhost:4502/crx/de)`.
1. Crie um `bundle node`em `/apps/engage/install` com nomes arbitrários, como:

   * Nome simbólico: `com.engage.media.social.messaging.MessagingNotification`
   * Nome: Notificação de mensagem do tutorial de introdução
   * Descrição: Um exemplo de serviço para enviar uma notificação por email aos usuários quando eles receberem uma mensagem
   * Pacote: `com.engage.media.social.messaging.notification`

1. Navegar para `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification`e depois:

   1. Exclua o `Activator.java` classe criada automaticamente.
   1. Criar classe `MessageEventHandler.java`.
   1. Copie e cole o código abaixo em `MessageEventHandler.java`.

1. Clique em **Salvar tudo**.
1. Navegar para `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd`e adicione todas as declarações de importação como gravadas no `MessageEventHandler.java` código.
1. Crie o pacote.
1. Garantir `Day CQ Mail Service`O serviço OSGi está configurado.
1. Faça logon como um usuário de demonstração e envie um email para outro usuário.
1. O recipient recebe um e-mail com relação a uma nova mensagem.

#### MessageEventHandler.java {#messageeventhandler-java}

```java
package com.engage.media.social.messaging.notification;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.api.resource.Resource;
import org.apache.commons.mail.Email;
import org.apache.commons.mail.EmailException;
import org.apache.commons.mail.SimpleEmail;
import org.apache.commons.mail.HtmlEmail;
import java.util.List;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import com.adobe.cq.social.messaging.api.Message;
import com.adobe.cq.social.messaging.api.MessagingEvent;
import com.day.cq.mailer.MessageGatewayService;
import com.day.cq.mailer.MessageGateway;

@Component(immediate=true)
@Service(EventHandler.class)
@Properties({
        @Property(name = "event.topics", value = "com/adobe/cq/social/message")
})
public class MessagingEventHandler implements EventHandler {
    private Logger logger = LoggerFactory.getLogger(MessagingEventHandler.class);

    @Reference
    ResourceResolverFactory resourceResolverFactory;

    @Reference
    private MessageGatewayService messageGatewayService;

    ResourceResolver resourceResolver=null;
    MessageGateway messageGateway=null;

    public void sendMail(String from, String to,String subject, String content){
        Email email = new SimpleEmail();
        messageGateway = messageGatewayService.getGateway(SimpleEmail.class);
        try {
         email.addTo(to);
            email.addReplyTo(from);
            email.setFrom(from);
            email.setMsg(content);
            email.setSubject(subject);
         messageGateway.send(email);
        } catch(EmailException ex) {
            logger.error("MessageNotificaiton : Error sending email : "+ex.getMessage());
        }
        logger.info("**** MessageNotification **** Mail sent to " + to);
    }

    public void handleEvent(Event event) {
        //Get Message Path and originator User's ID from event
        String messagePath = (String) event.getProperty("path");
        String senderId = (String) event.getProperty("userId");
        MessagingEvent.MessagingActions action = (MessagingEvent.MessagingActions) event.getProperty("action");
        try{
            if(MessagingEvent.MessagingActions.MessageSent.equals(action)){
                resourceResolver = resourceResolverFactory.getAdministrativeResourceResolver(null);

                //Read message
                Resource resource = resourceResolver.getResource(messagePath);
                Message msg = resource.adaptTo(Message.class);

                //Get list of recipient Ids from message
                //For Getting Started Tutorial, Id is same as email. If that is not the case in your site,
                //an additional step is needed to retrieve the email for the Id
                List<String> reclist = msg.getRecipientIdList();
                for(int i=0;i<reclist.size();i++){
                    //Send Email using Mailing Service
                    sendMail("admin@cqadmin.qqq",reclist.get(i),"New message on Getting Started Tutorial", "Hi\nYou have received a new message from  " +  senderId + ". To read it, sign in to Getting Started Tutorial.\n\n-Engage Admin");
                }
            }
        } catch(Exception ex){
            logger.error("Error getting message info : " + ex.getMessage());
        } finally {
            resourceResolver.close();
        }

    }
}
```
