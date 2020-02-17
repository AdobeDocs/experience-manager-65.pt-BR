---
title: Configuração de email
seo-title: Configuração de email
description: Configuração de email para Comunidades
seo-description: Configuração de email para Comunidades
uuid: e8422cc2-1594-43b0-b587-82825636cec1
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: b4d38e45-eaa0-4ace-a885-a2e84fdfd5a1
pagetitle: Configuring Email
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Configuração de email {#configuring-email}

O AEM Communities usa email para

* [Notificações de comunidades](notifications.md)
* [Assinaturas de comunidades](subscriptions.md)

Por padrão, o recurso de email não está funcionando, pois exige a especificação de um servidor SMTP e de um usuário SMTP.

>[!CAUTION]
>
>O email para notificações e assinaturas deve ser configurado somente no editor [principal](deploy-communities.md#primary-publisher).

## Configuração padrão do serviço de correio {#default-mail-service-configuration}

O serviço de email padrão é necessário para notificações e assinaturas.

* No editor principal
* Conectado com privilégios de administrador
* Acesse o console [da Web](../../help/sites-deploying/configuring-osgi.md)

   * Por exemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localize a variável `Day CQ Mail Service`
* Selecionar o ícone de edição

Isso se baseia na documentação de [Configuração da notificação](../../help/sites-administering/notification.md)por email, mas com uma diferença de que o campo `"From" address` não ** é obrigatório e deve ficar vazio.

Por exemplo (preenchido com valores apenas para fins ilustrativos):

![chlimage_1-98](assets/chlimage_1-98.png)

* **[!UICONTROL Nome]** do host do servidor SMTP: *(obrigatório)* O servidor SMTP a ser usado.

* **[!UICONTROL Porta]** do servidor SMTP *(obrigatório)* A porta do servidor SMTP deve ser 25 ou superior.

* **[!UICONTROL Usuário]** SMTP: *(obrigatório)* O usuário SMTP.

* **[!UICONTROL Senha]** SMTP: *(obrigatório)* A senha do usuário SMTP.

* **[!UICONTROL Endereço]**&quot;De&quot;: Deixe em branco
* **[!UICONTROL O SMTP usa SSL]**: Se marcada, enviará email seguro. Verifique se a porta está definida como 465 ou conforme necessário para o servidor SMTP.
* **[!UICONTROL E-mail]** de depuração: Se marcada, ativa o registro de interações com o servidor SMTP.

## Configuração de email do AEM Communities {#aem-communities-email-configuration}

Depois que o serviço [de email](#default-mail-service-configuration) padrão é configurado, as duas instâncias existentes da configuração do `AEM Communities Email Reply Configuration` OSGi, incluídas na versão, tornam-se funcionais.

Somente a instância para assinaturas precisa ser configurada mais detalhadamente ao permitir a resposta por email.

1. ` [email](#configuration-for-notifications)` instance

   para notificações, que não suportam e-mail de resposta, e que não devem ser alteradas

1. ` [subscriptions-email](#configuration-for-subscriptions)` instance

   requer configuração para permitir a criação completa de postagem a partir do email de resposta

Para acessar as instâncias de configuração de email das Comunidades:

* No editor principal
* Conectado com privilégios de administrador
* Acesse o console [da Web](../../help/sites-deploying/configuring-osgi.md)

   * Por exemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localizar `AEM Communities Email Reply Configuration`

![chlimage_1-99](assets/chlimage_1-99.png)

### Configuração para notificações {#configuration-for-notifications}

A instância da configuração do `AEM Communities Email Reply Configuration` OSGi com o e-mail Nome é o recurso de notificações. Esse recurso não inclui resposta por email.

Esta configuração não deve ser alterada.

* Localize a variável `AEM Communities Email Reply Configuration`
* Selecionar o ícone de edição
* Verifique se o **nome** está `email`

* Verifique se o e-mail **Criar** publicação da resposta está `unchecked`

![chlimage_1-100](assets/chlimage_1-100.png)

### Configuração de assinaturas {#configuration-for-subscriptions}

Para assinaturas de Comunidades, é possível ativar ou desativar a capacidade de um membro postar conteúdo respondendo a um email.

* Localize a variável `AEM Communities Email Reply Configuration`
* Selecionar o ícone de edição
* Verifique se o **nome** está `subscriptions-email`

![chlimage_1-101](assets/chlimage_1-101.png)

* **[!UICONTROL Nome]** : *(obrigatório)* `subscriptions-email`. Não Editar.

* **[!UICONTROL Crie uma publicação do email]** de resposta: Se marcada, o destinatário do email de assinatura pode postar o conteúdo enviando uma resposta. O padrão está marcado.
* **[!UICONTROL Adicionar ID rastreada ao cabeçalho]**:O padrão é `Reply-To`.

* **[!UICONTROL Duração máxima do assunto]**: Se a ID do rastreador for adicionada à linha do assunto, esse será o comprimento máximo do assunto, exceto a ID rastreada, após a qual será cortada. Observe que isso deve ser o mínimo possível para evitar que as informações de ID rastreadas sejam perdidas. O padrão é 200.
* **[!UICONTROL Endereço]** de email &quot;De&quot;: *(obrigatório)* Endereço do qual o email de notificação será entregue. Provavelmente o mesmo usuário **** SMTP especificado para o serviço [de email](#configuredefaultmailservice)padrão. O padrão é `no-reply@example.com`.

* **[!UICONTROL Responder ao delimitador]**: Se a ID do rastreador for adicionada ao cabeçalho Responder, esse delimitador será usado. O padrão é `+` (sinal de mais).

* **[!UICONTROL Prefixo da ID do rastreador no assunto]**: Se a ID do rastreador for adicionada à linha de assunto, esse prefixo será usado. O padrão é `post#`.

* **[!UICONTROL Prefixo da ID do rastreador no corpo]** da mensagem: Se a ID do rastreador for adicionada ao corpo da mensagem, esse prefixo será usado. O padrão é `Please do not remove this:`.

* **[!UICONTROL Enviar por email como HTML]**: Se marcada, o Tipo de conteúdo do email será definido como `"text/html;charset=utf-8"`. O padrão está marcado.

* **[!UICONTROL Nome]** de usuário padrão: Esse nome será usado para usuários sem nome. O padrão é `no-reply@example.com`.

* **[!UICONTROL Caminho]** raiz dos modelos: O email é criado usando o modelo armazenado nesse caminho raiz. O padrão é `/etc/community/templates/subscriptions-email`.

## Configurar Importador de Pesquisa {#configure-polling-importer}

Para que o email seja trazido para o repositório, é necessário configurar um importador de pesquisa e configurar suas propriedades no repositório manualmente.

### Adicionar novo importador de pesquisa {#add-new-polling-importer}

* No editor principal
* Conectado com privilégios de administrador
* Navegue até o console do importador de pesquisa. Por exemplo, [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)
* Selecionar **[!UICONTROL Adicionar]**

![chlimage_1-102](assets/chlimage_1-102.png)

* **[!UICONTROL Tipo]**: *(obrigatório)* Puxe para baixo para selecionar `POP3 (over SSL).`

* **[!UICONTROL URL]**: *(obrigatório)* O servidor de correio de saída. Por exemplo, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`

* **[!UICONTROL Importar para o Caminho]**&amp;ast;: *(obrigatório)* Defina como `/content/usergenerated/mailFolder/postEmails`navegando até a `postEmails`pasta e selecione **OK**

* **[!UICONTROL Intervalo de atualização em segundos]**: *(opcional)* O servidor de correio configurado para o serviço de correio padrão pode ter requisitos relacionados ao valor do intervalo de atualização. Por exemplo, o Gmail pode exigir um intervalo de `300`.

* **[!UICONTROL Logon]**: *(opcional)*

* **[!UICONTROL Senha]**: *(opcional)*

* Selecionar **[!UICONTROL OK]**

### Ajustar protocolo para o novo importador de pesquisa {#adjust-protocol-for-new-polling-importer}

Depois que a nova configuração de pesquisa for salva, será necessário modificar ainda mais as propriedades do importador de email de assinatura para alterar o protocolo de `POP3` para `emailreply`

Usando o [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* No editor principal
* Conectado com privilégios de administrador
* Navegue até [https://&lt;servidor>:&lt;porta>/crx/de/index.jsp#/etc/imported/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling)
* Selecionar a configuração recém-criada
* Modifique as seguintes propriedades

   * **feedType**: substituir `pop3s` por **`emailreply`**
   * **fonte**: substituir o protocolo da fonte `pop3s://` por **`emailreply://`**

![chlimage_1-103](assets/chlimage_1-103.png)

Os triângulos vermelhos indicam as propriedades modificadas. Certifique-se de salvar as alterações:

* Selecione **[!UICONTROL Salvar tudo]**

