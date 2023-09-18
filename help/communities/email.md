---
title: Configuração de email
description: Configuração de email para Comunidades
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
pagetitle: Configuring Email
role: Admin
exl-id: bf97d388-f8ca-4e37-88e2-0c536834311e
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 3%

---

# Configuração de email {#configuring-email}

O AEM Communities usa o email para:

* [Notificações das comunidades](notifications.md)
* [Assinaturas das Comunidades](subscriptions.md)

Por padrão, o recurso de email não é funcional, pois requer a especificação de um servidor SMTP e usuário SMTP.

>[!CAUTION]
>
>O email para notificações e assinaturas deve ser configurado somente no [editor principal](deploy-communities.md#primary-publisher).

## Configuração do serviço de e-mail padrão {#default-mail-service-configuration}

O serviço de email padrão é necessário para notificações e assinaturas.

* Faça logon no editor principal com privilégio de administrador e acesse o [Console da Web](../../help/sites-deploying/configuring-osgi.md):

   * Por exemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localize o `Day CQ Mail Service`.
* Selecione o ícone de edição.

Isso se baseia na documentação do [Configuração da notificação por e-mail](../../help/sites-administering/notification.md), mas com uma diferença de que o campo `"From" address` é *não* necessário e deve ser deixado em branco.

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
* **[!UICONTROL SMTP usa SSL]**

  Quando marcado, envia um email seguro. Verifique se a porta está definida como 465 ou conforme exigido para um servidor SMTP.
* **[!UICONTROL Depurar email]**

  Se essa opção for marcada, ativará o registro das interações do servidor SMTP.

## Configuração de email do AEM Communities {#aem-communities-email-configuration}

Quando a variável [serviço de e-mail padrão](#default-mail-service-configuration) estiver configurado, as duas instâncias existentes da variável `AEM Communities Email Reply Configuration` A configuração do OSGi, incluída na versão, torna-se funcional.

Somente a instância para assinaturas deve ser configurada posteriormente ao permitir a resposta por email.

1. [E-mail](#configuration-for-notifications) instância:

   Para notificações, que não aceitam email de resposta e não devem ser alteradas.

1. [Assinaturas - email](#configuration-for-subscriptions) instância:

   Requer configuração para habilitar totalmente a criação de publicação a partir do email de resposta.

Para acessar as instâncias de configuração de email das Comunidades:

* Faça logon no editor principal com privilégio de administrador e acesse o [Console da Web](../../help/sites-deploying/configuring-osgi.md)

   * Por exemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localizar `AEM Communities Email Reply Configuration`.

![email-reply-config](assets/email-reply-config.png)

### Configuração de notificações {#configuration-for-notifications}

A instância de `AEM Communities Email Reply Configuration` A configuração OSGi com o email Name é o recurso de notificações diretas. Esse recurso não inclui resposta por email.

Não altere esta configuração.

* Localize o `AEM Communities Email Reply Configuration`.
* Selecione o ícone de edição.
* Verifique se **Nome** é `email`.

* Verifique se **Criar publicação do email de resposta** é `unchecked`.

![configure-email-reply](assets/configure-email-reply.png)

### Configuração de assinaturas {#configuration-for-subscriptions}

Para assinaturas Communities, é possível habilitar ou desabilitar a capacidade de um membro publicar conteúdo respondendo a um email.

* Localize o `AEM Communities Email Reply Configuration`.
* Selecione o ícone de edição.
* Verifique se **Nome** é `subscriptions-email`.

  ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL Nome]**

  *(Obrigatório)* `subscriptions-email`. Não Editar.

* **[!UICONTROL Criar publicação do email de resposta]**

  Se marcado, o recipient de um email de assinatura poderá postar conteúdo enviando uma resposta. O padrão está marcado.
* **[!UICONTROL Adicionar id rastreada ao cabeçalho]**

  O padrão é `Reply-To`.

* **[!UICONTROL Tamanho máximo de]**

  Se a ID do rastreador for adicionada à linha de assunto, esse será o comprimento máximo do assunto, excluindo a ID rastreada, após o qual ele será aparado. Deve ser o menor possível para evitar a perda de informações de ID rastreadas. O padrão é 200.

* **[!UICONTROL Endereço de email &quot;Responder para&quot;]**

  Endereço usado como endereço de email de &quot;Resposta&quot;. O padrão é `no-reply@example.com`.

* **[!UICONTROL Delimitador de resposta]**

  Se a ID do rastreador for adicionada ao cabeçalho Reply-to, esse delimitador será usado. O padrão é `+` (sinal de mais).

* **[!UICONTROL Prefixo da ID do rastreador no assunto]**

  Se a ID do rastreador for adicionada à linha de assunto, esse prefixo será usado. O padrão é `post#`.

* **[!UICONTROL Prefixo da ID do rastreador no corpo da mensagem]**

  Se a ID do rastreador for adicionada ao corpo da mensagem, esse prefixo será usado. O padrão é `Please do not remove this:`.

* **[!UICONTROL Enviar por e-mail como HTML]**: Se marcada, o Content-Type do email será definido como `"text/html;charset=utf-8"`. O padrão está marcado.

* **[!UICONTROL Nome de usuário padrão]**

  Esse nome é usado para usuários sem nome. O padrão é `no-reply@example.com`.

* **[!UICONTROL Caminho raiz dos modelos]**

  O email é criado usando um modelo armazenado nesse caminho raiz. O padrão é `/etc/community/templates/subscriptions-email`.

## Configurar o importador de pesquisa {#configure-polling-importer}

Para que o email seja trazido para o repositório, é necessário configurar um importador de pesquisa e configurar as propriedades no repositório manualmente.

### Adicionar novo importador de pesquisa {#add-new-polling-importer}

* Faça logon no editor principal com privilégio de administrador e navegue até o console do importador de pesquisa:

  Por exemplo, [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* Selecionar **[!UICONTROL Adicionar]**

  ![polling-import](assets/polling-importer.png)

* **[!UICONTROL Tipo]**

  *(Obrigatório)* Puxe para baixo para selecionar `POP3 (over SSL)`.

* **[!UICONTROL URL]**

  *(Obrigatório)* O servidor de email de saída. Por exemplo, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`.

* **[!UICONTROL Importar para caminho]**&amp;ast;

  *(Obrigatório)* Defina como `/content/usergenerated/mailFolder/postEmails`
ao navegar até o `postEmails`e selecione **OK**.

* **[!UICONTROL Ativar o intervalo em segundo]**

  *(Opcional)* O servidor de email configurado para o serviço de email padrão pode ter requisitos relacionados ao valor do intervalo de atualização. Por exemplo, o Gmail pode exigir um intervalo de `300`.

* **[!UICONTROL Logon]**

  *(Opcional)*

* **[!UICONTROL Senha]**

  *(Opcional)*

* Selecionar **[!UICONTROL OK]**.

### Ajustar protocolo para o novo importador de pesquisa {#adjust-protocol-for-new-polling-importer}

Depois que a nova configuração de pesquisa for salva, será necessário modificar ainda mais as propriedades do importador de email de assinatura para alterar o protocolo de `POP3` para `emailreply`.

Usar [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Faça logon no editor principal com privilégio de administrador e navegue até [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importer/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* Selecione a configuração recém-criada e modifique as seguintes propriedades:

   * **feedType**: Substituir `pop3s` com **`emailreply`**
   * **origem**: Substituir protocolo de origem `pop3s://` com **`emailreply://`**

![polling-protocol](assets/polling-protocol.png)

Os triângulos vermelhos indicam as propriedades modificadas. Certifique-se de salvar as alterações:

* Selecionar **[!UICONTROL Salvar tudo]**.
