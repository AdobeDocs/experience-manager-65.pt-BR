---
title: Princípios básicos para mensagens
seo-title: Princípios básicos para mensagens
description: Visão geral do componente de mensagens
seo-description: Visão geral do componente de mensagens
uuid: e0dad45e-d84d-4b28-b357-aded1c5d2605
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 98f70093-e786-4555-8aaa-d0df4c977dc0
docset: aem65
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Princípios básicos para mensagens {#messaging-essentials}

Esta página documentos os detalhes de como trabalhar com o componente Mensagens para incluir um recurso de mensagem em um site.

## Essenciais para o lado do cliente {#essentials-for-client-side}

**Escrever mensagem**

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/mensagens/componentes/hbs/composemessessasocial</p> </td>
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
   <td>consulte <a href="/help/communities/configure-messaging.md" target="_blank">Configurar mensagens</a></td>
  </tr>
  <tr>
   <td><strong>configuração do administrador</strong></td>
   <td><a href="/help/communities/messaging.md">Configurar mensagens</a></td>
  </tr>
 </tbody>
</table>

**Lista de mensagens**

(para Caixa de entrada, Enviado e Lixeira)

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/mensagens/componentes/hbs/caixa de mensagem</p> </td>
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
   <td>consulte <a href="/help/communities/configure-messaging.md" target="_blank">Configurar mensagens</a></td>
  </tr>
  <tr>
   <td><strong>configuração do administrador</strong></td>
   <td><a href="/help/communities/messaging.md" target="_blank">Configurar mensagens</a></td>
  </tr>
 </tbody>
</table>

Consulte também Personalizações do lado do [cliente](/help/communities/client-customize.md)

## Fundamentos para servidor {#essentials-for-server-side}

* [Configuração de mensagens](/help/communities/configure-messaging.md)
* [APIs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) de cliente de mensagens para componentes SCF
* [APIs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/api/package-summary.html) de mensagens para o serviço
* [Pontos finais de mensagens](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)
* [Personalizações do servidor](/help/communities/server-customize.md)

>[!CAUTION]
>
>O parâmetro String *não* deve conter uma barra final &quot;/&quot; para os seguintes métodos do MessageBuilder:
>
>* `setInboxPath`()
>* `setSentItemsPath`()
>
>
Por exemplo:
>
>
```>
>valid: mb.setInboxPath( "/mail/inbox" );
> not valid: mb.setInboxPath( "/mail/inbox/" );
>```>



### Site da comunidade {#community-site}

Uma estrutura de site da comunidade, criada usando o assistente, inclui o recurso de mensagens quando selecionado. Consulte `User Management` Configurações do console [Sites da](/help/communities/sites-console.md#user-management)comunidade.

### Código de exemplo: Notificação de mensagem recebida {#sample-code-message-received-notification}

O recurso Mensagens sociais lança eventos para operações, por exemplo `send`, `marking read`, `marking delete`. Esses eventos podem ser capturados e as ações executadas nos dados contidos no evento.

O exemplo a seguir é de um manipulador de eventos que escuta o `message sent` evento e envia um email para todos os recipient de mensagens que usam o `Day CQ Mail Service`.

Para tentar o script de amostra do servidor, é necessário um ambiente de desenvolvimento e a capacidade de criar um pacote OSGi:

1. Faça logon como administrador do ` [CRXDE|Lite](https://localhost:4502/crx/de)`.
1. Crie uma `bundle node`entrada `/apps/engage/install` com nomes arbitrários, como:

   * Nome simbólico: `com.engage.media.social.messaging.MessagingNotification`
   * Nome: Notificação de mensagem do tutorial de introdução
   * Descrição: Um exemplo de serviço para enviar uma notificação por email aos usuários quando eles receberem uma mensagem
   * Pacote: `com.engage.media.social.messaging.notification`

1. Navegue até `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification`e, em seguida:

   1. Exclua a `Activator.java` classe criada automaticamente.
   1. Criar classe `MessageEventHandler.java`.
   1. Copie e cole o código abaixo em `MessageEventHandler.java`.

1. Clique em **Salvar tudo**.
1. Navegue até `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd`e adicione todas as instruções de importação conforme gravadas no `MessageEventHandler.java` código.
1. Construa o pacote.
1. Verifique se o serviço `Day CQ Mail Service`OSGi está configurado.
1. Efetue logon como um usuário de demonstração e envie um email para outro usuário.
1. O recipient recebe um email com relação a uma nova mensagem.

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

