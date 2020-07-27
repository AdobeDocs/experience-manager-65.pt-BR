---
title: Configurar mensagens
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
translation-type: tm+mt
source-git-commit: eb5317be52eec39b947ccb3c456d21d567ef2841
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 1%

---


# Configurar mensagens {#configure-messaging}

## Visão geral {#overview}

O recurso de mensagens para AEM Communities fornece a capacidade de visitantes (membros) de sites conectados enviarem mensagens para outros que sejam acessíveis quando conectados ao site.

As mensagens são ativadas para um site da comunidade marcando uma caixa durante a criação [do site da](/help/communities/sites-console.md)comunidade.

Esta página tem informações sobre a configuração padrão e possíveis ajustes.

Para obter informações adicionais para desenvolvedores, consulte [Messaging Essentials](/help/communities/essentials-messaging.md).

## Serviço de Operações de Mensagens {#messaging-operations-service}

O Serviço [de Operações de Mensagens do](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) AEM Communities de configuração identifica o ponto de extremidade que lida com solicitações relacionadas a mensagens, as pastas que o serviço deve usar para armazenar mensagens e, se as mensagens podem incluir anexos de arquivo, quais tipos de arquivos são permitidos.

Para sites da comunidade criados usando o `Communities Sites console`, já existe uma instância do serviço, com a caixa de entrada definida como `/mail/inbox`.

### Serviço de Operações de Mensagens da Comunidade {#community-messaging-operations-service}

Como mostrado abaixo, existe uma configuração do serviço para sites criados com o assistente [de criação de](/help/communities/sites-console.md)sites. A configuração pode ser visualizada ou editada selecionando o ícone de lápis ao lado da configuração.

![operações de mensagens](assets/messaging-operations.png)

### Adicionar nova configuração {#add-new-configuration}

Para adicionar uma nova configuração, selecione o ícone de adição &quot;**+**&quot; ao lado do nome do serviço:

* **Campos de mensagem Lista de permissões**

   Especifica as propriedades do componente Compor mensagem que os usuários podem editar e persistir. Se novos elementos de formulário forem adicionados, a ID do elemento precisará ser adicionada se desejar ser armazenada no SRP. O padrão são duas entradas: *assunto* e *conteúdo*.

* **Limite de tamanho da caixa de mensagem**

   O número máximo de bytes na caixa de mensagem de cada usuário. O padrão é *1073741824* (1 GB).

* **Limite de contagem de mensagens**

   O número total de mensagens permitidas por usuário. Um valor de -1 indica que um número ilimitado de mensagens é permitido, sujeito ao limite de tamanho da caixa de mensagem. O padrão é *10000* (10 mil).

* **Notificar falha do delivery**

   Se marcada, notifique o remetente se o delivery da mensagem falhar para alguns recipient. O padrão está *marcado*.

* **Id do remetente do delivery com falha**

   Nome do remetente que aparece na mensagem de falha do delivery. O padrão é *failureNotifier*.

* **Caminho do modelo de mensagem de falha**

   Caminho absoluto para a raiz do modelo de mensagem com falha do delivery. O padrão é */etc/notification/messaging/default*.

* **Número de tentativas**

   Número de vezes para tentar reenviar a mensagem que não foi entregue. O padrão é *3*.

* **Aguardar entre tentativas**

   Número de segundos de espera entre as tentativas de reenviar a mensagem após falha no envio. O padrão é *100* (segundos).

* **Contagem do tamanho do pool de atualizações**

   Número de threads simultâneos usados para atualização de contagem. O padrão é *10*.

* **Caminho da caixa de entrada**

   (*Obrigatório*) O caminho, relativo ao nó do usuário (/home/users/*username*), a ser usado para a `inbox` pasta. O caminho NÃO deve terminar com uma barra à direita &#39;/&#39;. O padrão é */mail/caixa de entrada*.

* **Caminho dos itens enviados**

   (*Obrigatório*) O caminho, relativo ao nó do usuário (/home/users/*username*), a ser usado para a `sent items` pasta. O caminho NÃO deve terminar com uma barra à direita &#39;/&#39;. O padrão é */mail/sentitems* .

* **Anexos de suporte**

   Se marcada, os usuários poderão adicionar anexos às suas mensagens. O padrão está *marcado*.

* **Ativar mensagens de grupo**

   Se selecionado, os usuários registrados podem enviar mensagens em massa para um grupo de membros. O padrão está *desmarcado*.

* **Nº máximo do total de recipient**

   Se as mensagens de grupo estiverem ativadas, especifique o número máximo de recipient para os quais as mensagens de grupo podem ser enviadas por vez. O padrão é *100*.

* **Tamanho do lote**

   Número de mensagens a serem agrupadas em lote para um envio ao enviar para um grande grupo de recipient. O padrão é *100*.

* **Tamanho total do anexo**

   Se supportAttachments estiver marcado, esse valor especificará o tamanho total máximo permitido (em bytes) de todos os anexos. O padrão é *104857600* (100 MB).

* **Tipo de anexo lista de bloqueios**

   Uma lista de bloqueios de extensões de nome de arquivo, com prefixo &#39;**.**&quot;, isso será rejeitado pelo sistema. Se não for incluir na lista de bloqueios, a extensão será permitida. As extensões podem ser adicionadas ou removidas usando os ícones &quot;**+**&quot; e &quot;**-**&quot;.

* **Tipos de anexos permitidos**

   **(*Ação necessária*)** Uma lista de permissões de extensões de nome de arquivo, o oposto da  lista de bloqueios. Para permitir todas as extensões de nome de arquivo, exceto aquelas incluir na lista de bloqueios, use o ícone &quot;**-**&quot; para remover a única entrada vazia.

* **Seletor de serviços**

   (*Obrigatório*) Um caminho absoluto (ponto final) pelo qual o serviço é chamado (um recurso virtual). A raiz do caminho escolhido deve ser uma incluída na configuração Caminhos *de execução* da configuração do OSGi [ , como `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), `/bin/`e `/apps/``/services/`. Para selecionar essa configuração para o recurso de mensagens de um site, esse terminal é fornecido como o **`Service selector`** valor para o `Message List and Compose Message components` (consulte Recurso [](/help/communities/configure-messaging.md)de mensagem).

   O padrão é */bin/messaging* .

* **de campo Lista de permissões**

   Usar campos **de mensagem Lista de permissões**.

>[!CAUTION]
>
>Sempre que uma `Messaging Operations Service` configuração é aberta para edição, se `allowedAttachmentTypes.name` foi removida, uma entrada vazia é adicionada novamente para tornar a propriedade configurável. Uma única entrada vazia efetivamente desativa anexos de arquivo.
>
>Para permitir todas as extensões de nome de arquivo, exceto aquelas incluir na lista de bloqueios, use o ícone &quot;**-**&quot; para (novamente) remover a única entrada vazia antes de clicar em **Salvar**.


## Group Messaging {#group-messaging}

Para permitir que usuários registrados enviem mensagens diretas em massa para grupos de usuários, certifique-se de **Ativar mensagens** de grupo nas duas instâncias de configuração dos Serviços **de Operação de** Mensagens a seguir:

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Serviço de Operações de Mensagens: console social**

![social-console-op-service](assets/social-console-op-service.png)

**Serviço de Operações de Mensagens: mensagens sociais**

![social-message-op-service](assets/social-message-op-service.png)

## Resolução de Problemas{#troubleshooting}

Uma maneira de solucionar problemas é ativar a [depuração de mensagens no registro.](/help/sites-administering/troubleshooting.md)

Consulte também [Loggers e Writers for Individual Services](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

O pacote a ser monitorado é `com.adobe.cq.social.messaging`.
