---
title: Configuração de email
seo-title: Configuring Email
description: Configuração de email para comunidades
seo-description: Email configuration for Communities
uuid: e8422cc2-1594-43b0-b587-82825636cec1
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: b4d38e45-eaa0-4ace-a885-a2e84fdfd5a1
pagetitle: Configuring Email
role: Admin
exl-id: bf97d388-f8ca-4e37-88e2-0c536834311e
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 5%

---

# Configuração de email {#configuring-email}

O AEM Communities usa email para:

* [Notificações de comunidades](notifications.md)
* [Assinaturas das Comunidades](subscriptions.md)

Por padrão, o recurso de email não é funcional, pois requer a especificação de um servidor SMTP e usuário SMTP.

>[!CAUTION]
>
>Email para notificações e subscrições deve ser configurado somente no [editor principal](deploy-communities.md#primary-publisher).

## Configuração padrão do serviço de email {#default-mail-service-configuration}

O serviço de email padrão é necessário para notificações e assinaturas.

* Faça logon no editor principal com privilégio de administrador e acesse o [Console da Web](../../help/sites-deploying/configuring-osgi.md):

   * Por exemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localize a variável `Day CQ Mail Service`.
* Selecione o ícone de edição.

Isso é baseado na documentação de [Configuração de notificação por email](../../help/sites-administering/notification.md), mas com uma diferença nesse campo `"From" address` é *not* obrigatório e deve ficar vazio.

Por exemplo (preenchido com valores somente para fins ilustrativos):

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
* **[!UICONTROL SMTP use SSL]**

   Se marcada, enviará email seguro. Verifique se a porta está definida como 465 ou conforme necessário para o servidor SMTP.
* **[!UICONTROL Depurar email]**

   Se marcada, ativa o registro de interações do servidor SMTP.

## Configuração de email do AEM Communities {#aem-communities-email-configuration}

Uma vez [serviço de email padrão](#default-mail-service-configuration) for configurada, as duas instâncias existentes do `AEM Communities Email Reply Configuration` A configuração do OSGi, incluída na versão, torna-se funcional.

Somente a instância para assinaturas precisa ser configurada posteriormente ao permitir a resposta por email.

1. [Email](#configuration-for-notifications) instância:

   Para notificações, que não são compatíveis com email de resposta e não devem ser alteradas.

1. [Subscriptions-email](#configuration-for-subscriptions) instância:

   Requer configuração para habilitar totalmente a criação de postagem a partir do email de resposta.

Para acessar as instâncias de configuração de email do Communities:

* Faça logon no editor principal com privilégio de administrador e acesse o [Console da Web](../../help/sites-deploying/configuring-osgi.md)

   * Por exemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localizar `AEM Communities Email Reply Configuration`.

![email-reply-config](assets/email-reply-config.png)

### Configuração para notificações {#configuration-for-notifications}

A instância de `AEM Communities Email Reply Configuration` A configuração OSGi com o email Nome é o recurso de notificações. Esse recurso não inclui a resposta por email.

Essa configuração não deve ser alterada.

* Localize a variável `AEM Communities Email Reply Configuration`.
* Selecione o ícone de edição.
* Verifique o **Nome** é `email`.

* Verificar **Criar publicação por email de resposta** é `unchecked`.

![configure-email-reply](assets/configure-email-reply.png)

### Configuração para assinaturas {#configuration-for-subscriptions}

Para assinaturas do Communities, é possível habilitar ou desabilitar a capacidade de um membro postar conteúdo respondendo a um email.

* Localize a variável `AEM Communities Email Reply Configuration`.
* Selecione o ícone de edição.
* Verifique o **Nome** é `subscriptions-email`.

   ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL Nome]**

   *(Obrigatório)* `subscriptions-email`. Não Editar.

* **[!UICONTROL Criar publicação por email de resposta]**

   Se marcada, o recipient do email de assinatura pode publicar o conteúdo enviando uma resposta. O padrão está marcado.
* **[!UICONTROL Adicionar id rastreada ao cabeçalho]**

   O padrão é `Reply-To`.

* **[!UICONTROL Tamanho máximo de]**

   Se a ID do rastreador for adicionada à linha de assunto, esse será o comprimento máximo do assunto, excluindo a id rastreada, depois disso ela será cortada. Observe que isso deve ser o menor possível para evitar que as informações de id rastreada sejam perdidas. O padrão é 200.

* **[!UICONTROL Endereço de email &quot;Responder para&quot;]**

   Endereço usado como endereço de email &quot;Responder para&quot;. O padrão é `no-reply@example.com`.

* **[!UICONTROL Responder para delimitador]**

   Se a ID do rastreador for adicionada ao cabeçalho Responder para , esse delimitador será usado. O padrão é `+` (sinal de mais).

* **[!UICONTROL Prefixo da ID do rastreador no assunto]**

   Se a ID do rastreador for adicionada à linha de assunto, esse prefixo será usado. O padrão é `post#`.

* **[!UICONTROL Prefixo da ID do rastreador no corpo da mensagem]**

   Se a ID do rastreador for adicionada ao corpo da mensagem, esse prefixo será usado. O padrão é `Please do not remove this:`.

* **[!UICONTROL Enviar email como HTML]**: Se marcada, o Tipo de conteúdo do email será definido como `"text/html;charset=utf-8"`. O padrão está marcado.

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

* **[!UICONTROL Importar para Caminho]**&amp;ast;

   *(Obrigatório)* Defina como `/content/usergenerated/mailFolder/postEmails`
navegando até o `postEmails`e selecione **OK**.

* **[!UICONTROL Ativar o intervalo em segundo]**

   *(Opcional)* O servidor de correio configurado para o serviço de correio padrão pode ter requisitos relacionados ao valor do intervalo de atualização. Por exemplo, o Gmail pode exigir um intervalo de `300`.

* **[!UICONTROL Logon]**

   *(Opcional)*

* **[!UICONTROL Senha]**

   *(Opcional)*

* Selecionar **[!UICONTROL OK]**.

### Ajustar Protocolo para Novo Importador de Polling {#adjust-protocol-for-new-polling-importer}

Depois que a nova configuração de pesquisa for salva, é necessário modificar ainda mais as propriedades do importador de email de assinatura para alterar o protocolo de `POP3` para `emailreply`.

Usando [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Faça logon no editor principal com privilégio de administrador e navegue até [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importer/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* Selecione a configuração recém-criada e modifique as seguintes propriedades:

   * **feedType**: Substituir `pop3s` com **`emailreply`**
   * **source**: Substituir o protocolo da origem `pop3s://` com **`emailreply://`**

![protocolo de sondagem](assets/polling-protocol.png)

Os triângulos vermelhos indicam as propriedades modificadas. Certifique-se de salvar as alterações:

* Selecionar **[!UICONTROL Salvar tudo]**.
