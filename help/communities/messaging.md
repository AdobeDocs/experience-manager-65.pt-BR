---
title: Configurar mensagens
description: Saiba mais sobre o recurso de mensagens no AEM Communities que fornece a capacidade de visitantes do site conectados (membros) enviarem mensagens entre si.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: ee94f093-fd14-49f2-9990-fbe853d924b1
source-git-commit: 00b6f2f03470aca7f87717818d0dfcd17ac16bed
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 1%

---

# Configurar mensagens {#configure-messaging}

## Visão geral {#overview}

O recurso de mensagens do AEM Communities fornece aos visitantes do site conectados (membros) a capacidade de enviar mensagens entre si que são acessíveis quando conectados ao site.

As mensagens são ativadas para um site da comunidade marcando uma caixa durante [criação de site da comunidade](/help/communities/sites-console.md).

Esta página contém informações sobre a configuração padrão e possíveis ajustes.

Para obter informações adicionais para desenvolvedores, consulte [Fundamentos de mensagens](/help/communities/essentials-messaging.md).

## Serviço de Operações de Mensagens {#messaging-operations-service}

A configuração [Serviço de operações de mensagens do AEM Communities](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) identifica o endpoint que lida com solicitações relacionadas a mensagens, as pastas que o serviço deve usar para armazenar mensagens e, se as mensagens puderem incluir anexos de arquivo, quais tipos de arquivo são permitidos.

Para sites da comunidade criados usando o `Communities Sites console`, uma instância do serviço existe, com a caixa de entrada definida como `/mail/inbox`.

### Serviço de operações de mensagens da comunidade {#community-messaging-operations-service}

Como mostrado abaixo, existe uma configuração do serviço para sites criados com o [assistente de criação de site](/help/communities/sites-console.md). A configuração pode ser visualizada ou editada selecionando o ícone de lápis ao lado da configuração.

![messaging-operations](assets/messaging-operations.png)

### Adicionar nova configuração {#add-new-configuration}

Para adicionar uma configuração, selecione o sinal de mais &quot;**+**&#x200B;Ícone &#39; ao lado do nome do serviço:

* **Campos de mensagem Incluir na lista de permissões**

  Especifica as propriedades do componente Compor mensagem que os usuários podem editar e manter. Se novos elementos de formulário forem adicionados, a ID do elemento deverá ser adicionada se desejar que seja armazenada em SRP. O padrão é duas entradas: *assunto* e *conteúdo*.

* **Limite de tamanho da caixa de mensagens**

  O número máximo de bytes na caixa de mensagem de cada usuário. O padrão é *1073741824* (1 GB).

* **Limite de contagem de mensagens**

  O número total de mensagens permitidas por usuário. Um valor -1 indica que um número ilimitado de mensagens é permitido, sujeito ao limite de tamanho da caixa de mensagem. O padrão é *10000* (10-K).

* **Notificar falha de entrega**

  Se marcado, notificará o remetente se a entrega da mensagem falhar para alguns destinatários. O padrão é *marcado*.

* **ID do remetente da entrega com falha**

  Nome do remetente que aparece na mensagem de falha de entrega. O padrão é *failureNotifier*.

* **Caminho do modelo de mensagem de falha**

  Caminho absoluto para a raiz do modelo de mensagem de falha de entrega. O padrão é */etc/notification/messaging/default*.

* **Número de tentativas**

  Número de vezes para tentar reenviar a mensagem que não foi entregue. O padrão é *3*.

* **Aguardar entre tentativas**

  Número de segundos a aguardar entre tentativas de reenviar a mensagem após falha de envio. O padrão é *100* (segundos).

* **Contar tamanho do pool de atualização**

  Número de threads simultâneos usados para atualização de contagem. O padrão é *10*.

* **Caminho da caixa de entrada**

  (*Obrigatório*) O caminho, relativo ao nó do usuário (/home/users/*nome de usuário*), para usar para o `inbox` pasta. O caminho NÃO deve terminar com uma barra &#39;/&#39;. O padrão é */mail/inbox*.

* **Caminho dos itens enviados**

  (*Obrigatório*) O caminho, relativo ao nó do usuário (/home/users/*nome de usuário*), para usar para o `sent items` pasta. O caminho NÃO deve terminar com uma barra &#39;/&#39;. O padrão é */mail/sentiitems* .

* **Anexos de suporte**

  Se marcados, os usuários poderão adicionar anexos às suas mensagens. O padrão é *marcado*.

* **Ativar mensagens de grupo**

  Se essa opção for selecionada, os usuários registrados poderão enviar mensagens em massa para um grupo de membros. O padrão é *desmarcado*.

* **Nº máximo do total de recipients**

  Se as mensagens de grupo estiverem ativadas, especifique o número máximo de recipients para os quais as mensagens de grupo podem ser enviadas de cada vez. O padrão é *100*.

* **Tamanho do lote**

  Número de mensagens a serem agrupadas para um envio ao enviar para um grande grupo de recipients. O padrão é *100*.

* **Tamanho total do anexo**

  Se supportAttachments estiver marcado, este valor especifica o tamanho total máximo permitido (em bytes) de todos os anexos. O padrão é *104857600* (100 MB).

* **Incluir na lista de bloqueios Tipo de anexo personalizado**

  Um incluo na lista de bloqueios ➡ de extensões de nome de arquivo, com o prefixo &#39;**.**&quot;, que é rejeitado pelo sistema. Incluir na lista de bloqueios Se não houver alteração, a extensão será permitida. É possível adicionar ou remover extensões usando o **+**&#39; e &#39;**-**&#x200B;Ícones &#39;.

* **Tipos de anexo permitidos**

  **(*Ação necessária*)** Um incluo na lista de permissões ➡ de extensões de nome de arquivo, o oposto do arquivo de inclui na lista de bloqueios. Incluir na lista de bloqueios Para permitir todas as extensões de nome de arquivo, exceto as, use o caractere &#39;**-**&#x200B;Ícone &quot; para remover a única entrada vazia.

* **Seletor de serviços**

  (*Obrigatório*) Um caminho absoluto (endpoint) pelo qual o serviço é chamado (um recurso virtual). A raiz do caminho escolhido deve ser uma incluída no *Caminhos de execução* definição da configuração OSGi [`Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), como `/bin/`, `/apps/`, e `/services/`. Para selecionar essa configuração para o recurso de mensagens de um site, esse endpoint é fornecido como o **`Service selector`** valor para o `Message List and Compose Message components` (consulte [Recurso de mensagem](/help/communities/configure-messaging.md)).

  O padrão é */bin/messaging* .

* **Campo ➡ Incluir na lista de permissões**

  Uso **Campos de mensagem Incluir na lista de permissões**.

>[!CAUTION]
>
>Cada vez que um `Messaging Operations Service` a configuração é aberta para edição, se `allowedAttachmentTypes.name` foi removido, uma entrada vazia é lida para tornar a propriedade configurável. Uma única entrada vazia efetivamente desativa os anexos de arquivo.
>
>Incluir na lista de bloqueios Para permitir todas as extensões de nome de arquivo, exceto as, use o caractere &#39;**-**&#x200B;Ícone &quot; para (novamente) remover a única entrada vazia antes de clicar em **Salvar**.

## Mensagens de grupo {#group-messaging}

Para permitir que os usuários registrados enviem mensagens diretas em massa para grupos de usuários, verifique se **Ativar mensagens de grupo** nos dois casos seguintes de **Serviços de Operação de Mensagens** configuração:

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Serviço de operações de mensagens: console social**

![social-console-op-service](assets/social-console-op-service.png)

**Serviço de operações de mensagens: mensagens sociais**

![social-message-op-service](assets/social-message-op-service.png)

## Resolução de problemas {#troubleshooting}

Uma maneira de solucionar problemas é habilitar [depurando mensagens no log.](/help/sites-administering/troubleshooting.md)

Consulte também [Registradores e Gravadores para Serviços Individuais](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

O pacote a ser monitorado é `com.adobe.cq.social.messaging`.
