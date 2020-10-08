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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 3%

---


# Configuração de email {#configuring-email}

A AEM Communities usa email para:

* [Notificações de comunidades](notifications.md)
* [Subscrições de comunidades](subscriptions.md)

Por padrão, o recurso de email não está funcionando, pois exige a especificação de um servidor SMTP e de um usuário SMTP.

>[!CAUTION]
>
>O email para notificações e subscrições deve ser configurado somente no editor [principal](deploy-communities.md#primary-publisher).

## Configuração padrão do serviço de correio {#default-mail-service-configuration}

O serviço de correio padrão é necessário para notificações e subscrições.

* Faça logon no editor principal com privilégio de administrador e acesse o Console [](../../help/sites-deploying/configuring-osgi.md)da Web:

   * Por exemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localize o `Day CQ Mail Service`.
* Selecione o ícone de edição.

Isso se baseia na documentação de [Configuração da notificação](../../help/sites-administering/notification.md)por email, mas com uma diferença de que o campo `"From" address` não ** é obrigatório e deve ficar vazio.

Por exemplo (preenchido com valores apenas para fins ilustrativos):

![email-config](assets/email-config.png)

* **[!UICONTROL Nome do host do servidor SMTP]**

   *(Obrigatório)* O servidor SMTP a ser usado.

* **[!UICONTROL Porta do servidor SMTP]**

   *(Obrigatório)* A porta do servidor SMTP deve ser 25 ou superior.

* **[!UICONTROL Usuário SMTP]**

   *(Obrigatório)* O usuário SMTP.

* **[!UICONTROL Senha SMTP]**

   *(Obrigatório)* A senha do usuário SMTP.

* **[!UICONTROL Endereço &quot;De&quot;]**

   Deixe em branco
* **[!UICONTROL Uso de SSL pelo SMTP]**

   Se marcada, enviará email seguro. Verifique se a porta está definida como 465 ou conforme necessário para o servidor SMTP.
* **[!UICONTROL Depurar email]**

   Se marcada, ativa o registro de interações com o servidor SMTP.

## Configuração de e-mail da AEM Communities {#aem-communities-email-configuration}

Depois que o serviço [de email](#default-mail-service-configuration) padrão é configurado, as duas instâncias existentes da configuração do `AEM Communities Email Reply Configuration` OSGi, incluídas na versão, tornam-se funcionais.

Somente a instância do subscrição precisa ser configurada posteriormente ao permitir a resposta por email.

1. [Instância de email](#configuration-for-notifications) :

   Para notificações, que não suportam e-mail de resposta, e que não devem ser alteradas.

1. [Instância de email](#configuration-for-subscriptions) do Subscrição:

   Requer configuração para ativar totalmente a criação de postagem a partir do email de resposta.

Para acessar as instâncias de configuração de email das Comunidades:

* Faça logon no editor principal com privilégio de administrador e acesse o Console [da Web](../../help/sites-deploying/configuring-osgi.md)

   * Por exemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localize `AEM Communities Email Reply Configuration`.

![email-reply-config](assets/email-reply-config.png)

### Configuração para notificações {#configuration-for-notifications}

A instância da configuração do `AEM Communities Email Reply Configuration` OSGi com o e-mail Nome é o recurso de notificações. Esse recurso não inclui resposta por email.

Esta configuração não deve ser alterada.

* Localize o `AEM Communities Email Reply Configuration`.
* Selecione o ícone de edição.
* Verifique se o **Nome** está `email`.

* Verifique se **Create post from reply email** is `unchecked`.

![configure-email-reply](assets/configure-email-reply.png)

### Configuração para Subscrição {#configuration-for-subscriptions}

Para subscrições de Comunidades, é possível ativar ou desativar a capacidade de um membro postar conteúdo respondendo a um email.

* Localize o `AEM Communities Email Reply Configuration`.
* Selecione o ícone de edição.
* Verifique se o **Nome** está `subscriptions-email`.

   ![configure-email-subscrição](assets/configure-email-subscriptions.png)

* **[!UICONTROL Nome]**

   *(Obrigatório)* `subscriptions-email`. Não Editar.

* **[!UICONTROL Criar postagem a partir do email de resposta]**

   Se marcada, o recipient de e-mail de subscrição pode postar conteúdo enviando uma resposta. O padrão está marcado.
* **[!UICONTROL Adicionar ID rastreada ao cabeçalho]**

   O padrão é `Reply-To`.

* **[!UICONTROL Tamanho máximo de]**

   Se a ID do rastreador for adicionada à linha do assunto, esse será o comprimento máximo do assunto, exceto a ID rastreada, após a qual será cortada. Observe que isso deve ser o mínimo possível para evitar que as informações de ID rastreadas sejam perdidas. O padrão é 200.

* **[!UICONTROL Endereço de email &quot;Responder para&quot;]**

   Endereço usado como endereço de email &quot;Responder para&quot;. O padrão é `no-reply@example.com`.

* **[!UICONTROL Responder ao delimitador]**

   Se a ID do rastreador for adicionada ao cabeçalho Responder, esse delimitador será usado. O padrão é `+` (sinal de mais).

* **[!UICONTROL Prefixo da ID do rastreador no assunto]**

   Se a ID do rastreador for adicionada à linha de assunto, esse prefixo será usado. O padrão é `post#`.

* **[!UICONTROL Prefixo de ID do rastreador no corpo da mensagem]**

   Se a ID do rastreador for adicionada ao corpo da mensagem, esse prefixo será usado. O padrão é `Please do not remove this:`.

* **[!UICONTROL Enviar por email como HTML]**: Se marcada, o Tipo de conteúdo do email será definido como `"text/html;charset=utf-8"`. O padrão está marcado.

* **[!UICONTROL Nome de usuário padrão]**

   Esse nome será usado para usuários sem nome. O padrão é `no-reply@example.com`.

* **[!UICONTROL Caminho raiz dos modelos]**

   O e-mail é criado usando o modelo armazenado neste caminho raiz. O padrão é `/etc/community/templates/subscriptions-email`.

## Configurar Importador de Pesquisa {#configure-polling-importer}

Para que o email seja trazido para o repositório, é necessário configurar um importador de pesquisa e configurar suas propriedades no repositório manualmente.

### Adicionar novo importador de pesquisa {#add-new-polling-importer}

* Faça logon no editor principal com privilégio de administrador e navegue até o console do importador de pesquisa:

   Por exemplo, [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* Selecionar **[!UICONTROL Adicionar]**

   ![importador de votos](assets/polling-importer.png)

* **[!UICONTROL Tipo]**

   *(Obrigatório)* Puxe para baixo para selecionar `POP3 (over SSL)`.

* **[!UICONTROL URL]**

   *(Obrigatório)* O servidor de correio de saída. Por exemplo, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`.

* **[!UICONTROL Importar para o Caminho]**&amp;ast;

   *(Obrigatório)* Defina como `/content/usergenerated/mailFolder/postEmails`navegando até a `postEmails`pasta e selecione **OK**.

* **[!UICONTROL Ativar o intervalo em segundo]**

   *(Opcional)* O servidor de correio configurado para o serviço de correio padrão pode ter requisitos relacionados ao valor do intervalo de atualização. Por exemplo, o Gmail pode exigir um intervalo de `300`.

* **[!UICONTROL Logon]**

   *(Opcional)*

* **[!UICONTROL Senha]**

   *(Opcional)*

* Selecione **[!UICONTROL OK]**.

### Ajustar protocolo para o novo importador de pesquisa {#adjust-protocol-for-new-polling-importer}

Quando a nova configuração de pesquisa for salva, será necessário modificar ainda mais as propriedades do importador de e-mail de subscrição para alterar o protocolo de `POP3` para `emailreply`.

Usando o [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Faça logon no editor principal com privilégio de administrador e navegue até [https://&lt;servidor>:&lt;porta>/crx/de/index.jsp#/etc/imported/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* Selecione a configuração recém-criada e modifique as seguintes propriedades:

   * **feedType**: Substituir `pop3s` por **`emailreply`**
   * **fonte**: Substituir o protocolo da fonte `pop3s://` por **`emailreply://`**

![protocolo de votação](assets/polling-protocol.png)

Os triângulos vermelhos indicam as propriedades modificadas. Certifique-se de salvar as alterações:

* Selecione **[!UICONTROL Salvar tudo]**.

