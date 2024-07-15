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
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Configurar mensagens {#configure-messaging}

## Visão geral {#overview}

O recurso de mensagens do AEM Communities fornece aos visitantes do site conectados (membros) a capacidade de enviar mensagens entre si que são acessíveis quando conectados ao site.

As mensagens estão habilitadas para um site da comunidade marcando uma caixa durante a [criação do site da comunidade](/help/communities/sites-console.md).

Esta página contém informações sobre a configuração padrão e possíveis ajustes.

Para obter informações adicionais para desenvolvedores, consulte [Messaging Essentials](/help/communities/essentials-messaging.md).

## Serviço de Operações de Mensagens {#messaging-operations-service}

A configuração [Serviço de Operações de Mensagens da AEM Communities](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) identifica o ponto de extremidade que lida com solicitações relacionadas a mensagens, as pastas que o serviço deve usar para armazenar mensagens e, se as mensagens puderem incluir anexos de arquivo, quais tipos de arquivo são permitidos.

Para sites de comunidade criados usando o `Communities Sites console`, existe uma instância do serviço, com a caixa de entrada definida como `/mail/inbox`.

### Serviço de operações de mensagens da comunidade {#community-messaging-operations-service}

Como mostrado abaixo, existe uma configuração do serviço para sites criados com o [assistente de criação de sites](/help/communities/sites-console.md). A configuração pode ser visualizada ou editada selecionando o ícone de lápis ao lado da configuração.

![operações-mensagens](assets/messaging-operations.png)

### Adicionar nova configuração {#add-new-configuration}

Para adicionar uma configuração, selecione o ícone de adição &#39;**+**&#39; ao lado do nome do serviço:

* **Inclui na lista de permissões de Campos de Mensagem**

  Especifica as propriedades do componente Compor mensagem que os usuários podem editar e manter. Se novos elementos de formulário forem adicionados, a ID do elemento deverá ser adicionada se desejar que seja armazenada em SRP. O padrão é duas entradas: *assunto* e *conteúdo*.

* **Limite de tamanho da caixa de mensagens**

  O número máximo de bytes na caixa de mensagem de cada usuário. O padrão é *1073741824* (1 GB).

* **Limite de contagem de mensagens**

  O número total de mensagens permitidas por usuário. Um valor -1 indica que um número ilimitado de mensagens é permitido, sujeito ao limite de tamanho da caixa de mensagem. O padrão é *10000* (10k).

* **Notificar falha de entrega**

  Se marcado, notificará o remetente se a entrega da mensagem falhar para alguns destinatários. O padrão é *marcado*.

* **ID do remetente da entrega com falha**

  Nome do remetente que aparece na mensagem de falha de entrega. O padrão é *failureNotifier*.

* **Caminho do modelo de mensagem de falha**

  Caminho absoluto para a raiz do modelo de mensagem de falha de entrega. O padrão é */etc/notification/messaging/default*.

* **Nº de tentativas**

  Número de vezes para tentar reenviar a mensagem que não foi entregue. O padrão é *3*.

* **Aguardar entre tentativas**

  Número de segundos a aguardar entre tentativas de reenviar a mensagem após falha de envio. O padrão é *100* (segundos).

* **Contar tamanho do pool de atualização**

  Número de threads simultâneos usados para atualização de contagem. O padrão é *10*.

* **Caminho da caixa de entrada**

  (*Obrigatório*) O caminho relativo ao nó do usuário (/home/users/*username*) a ser usado para a pasta `inbox`. O caminho NÃO deve terminar com uma barra &#39;/&#39;. O padrão é */caixa de entrada/correio*.

* **Caminho dos itens enviados**

  (*Obrigatório*) O caminho relativo ao nó do usuário (/home/users/*username*) a ser usado para a pasta `sent items`. O caminho NÃO deve terminar com uma barra &#39;/&#39;. O padrão é */mail/sentiitems*.

* **Anexos de suporte**

  Se marcados, os usuários poderão adicionar anexos às suas mensagens. O padrão é *marcado*.

* **Habilitar mensagens de grupo**

  Se essa opção for selecionada, os usuários registrados poderão enviar mensagens em massa para um grupo de membros. O padrão é *desmarcado*.

* **Número máximo. do total de destinatários**

  Se as mensagens de grupo estiverem ativadas, especifique o número máximo de recipients para os quais as mensagens de grupo podem ser enviadas de cada vez. O padrão é *100*.

* **Tamanho do lote**

  Número de mensagens a serem agrupadas para um envio ao enviar para um grande grupo de recipients. O padrão é *100*.

* **Tamanho total do anexo**

  Se supportAttachments estiver marcado, este valor especifica o tamanho total máximo permitido (em bytes) de todos os anexos. O padrão é *104857600* (100 MB).

* incluir na lista de bloqueios **Pesquisa de tipo de anexo**

  Um incluo na lista de bloqueios de extensões de nome de arquivo com o prefixo &#39;**.**&#39;, que foi rejeitado pelo sistema. Incluir na lista de bloqueios Se não houver alteração, a extensão será permitida. É possível adicionar ou remover extensões usando os ícones &#39;**+**&#39; e &#39;**-**&#39;.

* **Tipos de anexo permitidos**

  incluir na lista de permissões incluir na lista de bloqueios **(*Ação necessária*)** Uma pesquisa de extensões de nome de arquivo, o oposto do arquivo de pesquisa. Incluir na lista de bloqueios Para permitir todas as extensões de nome de arquivo, exceto as realçadas, use o ícone &#39;**-**&#39; para remover a única entrada vazia.

* **Seletor de serviços**

  (*Obrigatório*) Um caminho absoluto (ponto de extremidade) pelo qual o serviço é chamado (um recurso virtual). A raiz do caminho escolhido deve ser uma incluída na configuração *Caminhos de Execução* da configuração OSGi [`Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), como `/bin/`, `/apps/` e `/services/`. Para selecionar essa configuração para o recurso de mensagens de um site, esse ponto de extremidade é fornecido como o valor **`Service selector`** para `Message List and Compose Message components` (consulte [Recurso de Mensagem](/help/communities/configure-messaging.md)).

  O padrão é */bin/messaging*.

* **Inclui na lista de permissões de campo**

  Usar **Inclui na lista de permissões de Campos de Mensagem**.

>[!CAUTION]
>
>Cada vez que uma configuração `Messaging Operations Service` é aberta para edição, se `allowedAttachmentTypes.name` tiver sido removido, uma entrada vazia será lida para tornar a propriedade configurável. Uma única entrada vazia efetivamente desativa os anexos de arquivo.
>
>Incluir na lista de bloqueios Para permitir todas as extensões de nome de arquivo, exceto as realçadas, use o ícone &#39;**-**&#39; para (novamente) remover a única entrada vazia antes de clicar em **Salvar**.

## Mensagens de grupo {#group-messaging}

Para permitir que usuários registrados enviem mensagens diretas em massa para grupos de usuários, certifique-se de **Habilitar mensagens de grupo** nas duas instâncias a seguir da configuração dos **Serviços de Operação de Mensagens**:

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Serviço de Operações de Mensagens: console social**

![social-console-op-service](assets/social-console-op-service.png)

**Serviço de Operações de Mensagens: mensagens sociais**

![social-message-op-service](assets/social-message-op-service.png)

## Resolução de problemas {#troubleshooting}

Uma maneira de solucionar problemas é habilitar [mensagens de depuração no log.](/help/sites-administering/troubleshooting.md)

Consulte também [Loggers e Gravadores de Serviços Individuais](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

O pacote a monitorar é `com.adobe.cq.social.messaging`.
