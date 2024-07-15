---
title: Configuração de email
description: Saiba como configurar notificações por email e assinaturas para o Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
pagetitle: Configuring Email
role: Admin
exl-id: bf97d388-f8ca-4e37-88e2-0c536834311e
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Configuração de email {#configuring-email}

O AEM Communities usa o email para:

* [Notificações das comunidades](notifications.md)
* [Assinaturas das Comunidades](subscriptions.md)

Por padrão, o recurso de email não é funcional, pois requer a especificação de um servidor SMTP e usuário SMTP.

>[!CAUTION]
>
>O email para notificações e assinaturas deve ser configurado somente no [publicador principal](deploy-communities.md#primary-publisher).

## Configuração do serviço de e-mail padrão {#default-mail-service-configuration}

O serviço de email padrão é necessário para notificações e assinaturas.

* Faça logon no publicador principal com privilégio de administrador e acesse o [Console da Web](../../help/sites-deploying/configuring-osgi.md):

   * Por exemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localize o `Day CQ Mail Service`.
* Selecione o ícone de edição.

Isso se baseia na documentação de [Configuração de Notificação por Email](../../help/sites-administering/notification.md), mas com uma diferença em que o campo `"From" address` é *não* necessário e deve ser deixado em branco.

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

Depois que o [serviço de email padrão](#default-mail-service-configuration) é configurado, as duas instâncias existentes da configuração OSGi `AEM Communities Email Reply Configuration`, incluídas na versão, tornam-se funcionais.

Somente a instância para assinaturas deve ser configurada posteriormente ao permitir a resposta por email.

1. Instância de [email](#configuration-for-notifications):

   Para notificações, que não aceitam email de resposta e não devem ser alteradas.

1. Instância de [Subscriptions-email](#configuration-for-subscriptions):

   Requer configuração para habilitar totalmente a criação de publicação a partir do email de resposta.

Para acessar as instâncias de configuração de email das Comunidades:

* Faça logon no publicador principal com privilégio de administrador e acesse o [Console da Web](../../help/sites-deploying/configuring-osgi.md)

   * Por exemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localizar `AEM Communities Email Reply Configuration`.

![email-reply-config](assets/email-reply-config.png)

### Configuração de notificações {#configuration-for-notifications}

A instância da configuração OSGi `AEM Communities Email Reply Configuration` com o email Name é o recurso de notificações diretas. Esse recurso não inclui resposta por email.

Não altere esta configuração.

* Localize o `AEM Communities Email Reply Configuration`.
* Selecione o ícone de edição.
* Verifique se o **Nome** é `email`.

* Verifique se **Criar postagem do email de resposta** é `unchecked`.

![configurar-email-resposta](assets/configure-email-reply.png)

### Configuração de assinaturas {#configuration-for-subscriptions}

Para assinaturas Communities, é possível habilitar ou desabilitar a capacidade de um membro publicar conteúdo respondendo a um email.

* Localize o `AEM Communities Email Reply Configuration`.
* Selecione o ícone de edição.
* Verifique se o **Nome** é `subscriptions-email`.

  ![configurar-assinatura-email](assets/configure-email-subscriptions.png)

* **[!UICONTROL Nome]**

  *(Obrigatório)* `subscriptions-email`. Não Editar.

* **[!UICONTROL Criar postagem do email de resposta]**

  Se marcado, o recipient de um email de assinatura poderá postar conteúdo enviando uma resposta. O padrão está marcado.
* **[!UICONTROL Adicionar ID rastreada ao cabeçalho]**

  O padrão é `Reply-To`.

* **[!UICONTROL Tamanho máximo do assunto]**

  Se a ID do rastreador for adicionada à linha de assunto, esse será o comprimento máximo do assunto, excluindo a ID rastreada, após o qual ele será aparado. Deve ser o menor possível para evitar a perda de informações de ID rastreadas. O padrão é 200.

* **[!UICONTROL endereço de email &quot;Responder para&quot;]**

  Endereço usado como endereço de email de &quot;Resposta&quot;. O padrão é `no-reply@example.com`.

* **[!UICONTROL Responder-para-Delimitador]**

  Se a ID do rastreador for adicionada ao cabeçalho Reply-to, esse delimitador será usado. O padrão é `+` (sinal de adição).

* **[!UICONTROL Prefixo da ID do rastreador no assunto]**

  Se a ID do rastreador for adicionada à linha de assunto, esse prefixo será usado. O padrão é `post#`.

* **[!UICONTROL Prefixo de id do rastreador no corpo da mensagem]**

  Se a ID do rastreador for adicionada ao corpo da mensagem, esse prefixo será usado. O padrão é `Please do not remove this:`.

* **[!UICONTROL Email como HTML]**: se marcado, o Tipo de Conteúdo do email será definido como `"text/html;charset=utf-8"`. O padrão está marcado.

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

  ![importador de pesquisa](assets/polling-importer.png)

* **[!UICONTROL Tipo]**

  *(Obrigatório)* Retire para selecionar `POP3 (over SSL)`.

* **[!UICONTROL URL]**

  *(Obrigatório)* O servidor de email de saída. Por exemplo, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`.

* **[!UICONTROL Importar para Caminho]**&amp;ast;

  *(Obrigatório)* Definido como `/content/usergenerated/mailFolder/postEmails`
navegando até a pasta `postEmails` e selecionando **OK**.

* **[!UICONTROL Intervalo de Atualização em Segundos]**

  *(Opcional)* O servidor de email configurado para o serviço de email padrão pode ter requisitos relacionados ao valor do intervalo de atualização. Por exemplo, o Gmail pode exigir um intervalo de `300`.

* **[!UICONTROL Logon]**

  *(Opcional)*

* **[!UICONTROL Senha]**

  *(Opcional)*

* Selecione **[!UICONTROL OK]**.

### Ajustar protocolo para o novo importador de pesquisa {#adjust-protocol-for-new-polling-importer}

Depois que a nova configuração de sondagem for salva, será necessário modificar ainda mais as propriedades do importador de email de assinatura para alterar o protocolo de `POP3` para `emailreply`.

Usando [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Faça logon no publicador principal com privilégio de administrador e navegue até [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importer/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* Selecione a configuração recém-criada e modifique as seguintes propriedades:

   * **feedType**: substituir `pop3s` por **`emailreply`**
   * **origem**: substituir o protocolo da origem `pop3s://` por **`emailreply://`**

![protocolo de sondagem](assets/polling-protocol.png)

Os triângulos vermelhos indicam as propriedades modificadas. Certifique-se de salvar as alterações:

* Selecione **[!UICONTROL Salvar tudo]**.
