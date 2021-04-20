---
title: Configuração de mensagens
seo-title: Configuração de mensagens
description: Mensagens das comunidades
seo-description: Mensagens das comunidades
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 1%

---


# Configurar mensagens {#configure-messaging}

## Visão geral {#overview}

O recurso de mensagens para o AEM Communities fornece a capacidade de visitantes (membros) do site conectados enviarem mensagens para outros que sejam acessíveis quando conectados ao site.

As mensagens são ativadas para um site da comunidade marcando uma caixa durante [criação do site da comunidade](/help/communities/sites-console.md).

Esta página tem informações sobre a configuração padrão e possíveis ajustes.

Para obter informações adicionais para desenvolvedores, consulte [Messaging Essentials](/help/communities/essentials-messaging.md).

## Serviço de operações de mensagens {#messaging-operations-service}

A configuração [AEM Communities Messaging Operations Service](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) identifica o ponto de extremidade que lida com solicitações relacionadas a mensagens, as pastas que o serviço deve usar para armazenar mensagens e, se as mensagens puderem incluir anexos de arquivo, quais tipos de arquivo são permitidos.

Para sites da comunidade criados usando o `Communities Sites console`, uma instância do serviço já existe, com a caixa de entrada definida como `/mail/inbox`.

### Serviço de operações de mensagens da comunidade {#community-messaging-operations-service}

Como mostrado abaixo, existe uma configuração do serviço para sites criados com o [assistente de criação de sites](/help/communities/sites-console.md). A configuração pode ser exibida ou editada selecionando o ícone de lápis ao lado da configuração.

![operações de mensagens](assets/messaging-operations.png)

### Adicionar nova configuração {#add-new-configuration}

Para adicionar uma nova configuração, selecione o ícone de adição &#39;**+**&#39; ao lado do nome do serviço :

* **Campos de mensagem Lista de permissões**

   Especifica as propriedades do componente Escrever mensagem que os usuários podem editar e persistir. Se novos elementos de formulário forem adicionados, a ID do elemento precisará ser adicionada se desejar ser armazenada no SRP. O padrão é duas entradas: *subject* e *content*.

* **Limite de tamanho da caixa de mensagem**

   O número máximo de bytes na caixa de mensagem de cada usuário. O padrão é *1073741824* (1 GB).

* **Limite da contagem de mensagens**

   O número total de mensagens permitidas por usuário. Um valor de -1 indica que um número ilimitado de mensagens é permitido, sujeito ao limite de tamanho da caixa de mensagem. O padrão é *10000* (10k).

* **Notificar falha de entrega**

   Se marcada, notifique o remetente se o delivery da mensagem falhar para alguns recipients. O padrão é *marcado*.

* **Falha na ID do remetente do delivery**

   Nome do remetente que aparece na mensagem de falha do delivery. O padrão é *failureNotifier*.

* **Caminho do modelo de mensagem de falha**

   Caminho absoluto para a raiz do modelo de mensagem com falha de delivery. O padrão é */etc/notification/messaging/default*.

* **Número de tentativas**

   Número de vezes para tentar reenviar a mensagem que não foi entregue. O padrão é *3*.

* **Aguardar entre tentativas**

   Número de segundos para aguardar entre tentativas de reenviar a mensagem após falha do envio. O padrão é *100* (segundos).

* **Tamanho do pool de atualizações de contagem**

   Número de threads simultâneos usados para atualização de contagem. O padrão é *10*.

* **Caminho da caixa de entrada**

   (*Obrigatório*) O caminho, relativo ao nó do usuário (/home/users/*nome de usuário*), a ser usado para a pasta `inbox`. O caminho NÃO deve terminar com uma barra à direita &#39;/&#39;. O padrão é */mail/inbox*.

* **Caminho dos itens enviados**

   (*Obrigatório*) O caminho, relativo ao nó do usuário (/home/users/*nome de usuário*), a ser usado para a pasta `sent items`. O caminho NÃO deve terminar com uma barra à direita &#39;/&#39;. O padrão é */mail/sentitems* .

* **Anexos de suporte**

   Se marcada, os usuários poderão adicionar anexos às suas mensagens. O padrão é *marcado*.

* **Ativar mensagens em grupo**

   Se selecionada, os usuários registrados podem enviar uma mensagem em massa para um grupo de membros. O padrão é *desmarcado*.

* **Nº máximo do total de recipients**

   Se as mensagens de grupo estiverem ativadas, especifique o número máximo de recipients para os quais a mensagem de grupo pode ser enviada por vez. O padrão é *100*.

* **Tamanho do lote**

   Número de mensagens a serem agrupadas em lote para um envio ao enviar para um grande grupo de recipients. O padrão é *100*.

* **Tamanho total do anexo**

   Se supportAttachments estiver marcado, esse valor especifica o tamanho total máximo permitido (em bytes) de todos os anexos. O padrão é *104857600* (100 MB).

* **Tipo de anexo lista de bloqueios**

   Uma  lista de bloqueios de extensões de nome de arquivo, com prefixo &#39;**.**&quot;, que será rejeitado pelo sistema. Se não incluir na lista de bloqueios, a extensão será permitida. As extensões podem ser adicionadas ou removidas usando os ícones &#39;**+**&#39; e &#39;**-**&#39;.

* **Tipos de anexos permitidos**

   **(*Ação necessária*)** Uma  lista de permissões de extensões de nome de arquivo, o oposto da lista de bloqueios. Para permitir todas as extensões de nome de arquivo, exceto aquelas incluir na lista de bloqueios, use o ícone &#39;**-**&#39; para remover a única entrada vazia.

* **Seletor de serviços**

   (*Obrigatório*) Um caminho absoluto (ponto final) pelo qual o serviço é chamado (um recurso virtual). A raiz do caminho escolhido deve ser uma incluída na configuração *Caminhos de execução* de configuração do OSGi config [ `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), como `/bin/`, `/apps/` e `/services/`. Para selecionar essa configuração para o recurso de mensagens de um site, esse terminal é fornecido como o valor **`Service selector`** para o `Message List and Compose Message components` (consulte [Recurso de Mensagem](/help/communities/configure-messaging.md)).

   O padrão é */bin/messaging* .

* **de Lista de permissões de campo**

   Use **Campos de Mensagem Lista de permissões**.

>[!CAUTION]
>
>Cada vez que uma configuração `Messaging Operations Service` é aberta para edição, se `allowedAttachmentTypes.name` tiver sido removida, uma entrada vazia é adicionada novamente para tornar a propriedade configurável. Uma única entrada vazia desativa os anexos do arquivo.
>
>Para permitir todas as extensões de nome de arquivo, exceto aquelas incluir na lista de bloqueios, use o ícone &#39;**-**&#39; para (novamente) remover a única entrada vazia antes de clicar em **Salvar**.

## Mensagens de grupo {#group-messaging}

Para permitir que usuários registrados enviem mensagens diretas em massa para grupos de usuários, certifique-se de **Ativar mensagens de grupo** nas duas instâncias a seguir da configuração **Serviços de Operação de Mensagens**:

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Serviço de operações de mensagens: console social**

![social-console-op-service](assets/social-console-op-service.png)

**Serviço de operações de mensagens: mensagens sociais**

![social-message-op-service](assets/social-message-op-service.png)

## Resolução de problemas {#troubleshooting}

Uma maneira de solucionar problemas é ativar [mensagens de depuração no log.](/help/sites-administering/troubleshooting.md)

Consulte também [Registradores e Escritores para Serviços Individuais](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

O pacote a ser monitorado é `com.adobe.cq.social.messaging`.
