---
title: Sua caixa de entrada
seo-title: Sua caixa de entrada
description: Você pode receber notificações de várias áreas do AEM, como notificações sobre itens de trabalho ou tarefas que representam ações que você precisa executar no conteúdo da página.
seo-description: Você pode receber notificações de várias áreas do AEM, como notificações sobre itens de trabalho ou tarefas que representam ações que você precisa executar no conteúdo da página.
uuid: e7ba9150-957d-4f84-a570-2f3d83792472
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: ce2a1475-49cf-43e6-bfb9-006884ce3881
docset: aem65
translation-type: tm+mt
source-git-commit: bcb1840d23ae538c183eecb0678b6a75d346aa50
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 93%

---


# Sua caixa de entrada{#your-inbox}

Você pode receber notificações de várias áreas do AEM, como notificações sobre itens de trabalho ou tarefas que representam ações que você precisa executar no conteúdo da página.

Você recebe essas notificações em duas caixas de entrada, que são separadas pelo tipo de notificações:

* Uma caixa de entrada onde é possível visualizar as notificações recebidas como resultado das assinaturas está descrita na próxima seção.
* Uma caixa de entrada especializada para itens de fluxo de trabalho está descrita no documento [Participação em Workflows](/help/sites-classic-ui-authoring/classic-workflows-participating.md).

## Viewing Your Notifications {#viewing-your-notifications}

Para exibir suas notificações:

1. Abra a caixa de entrada de notificação: no console **Sites,** clique no botão de usuário no canto superior direito e selecione **Caixa de entrada de notificação**.

   ![screen_shot_2012-02-08at105226am](assets/screen_shot_2012-02-08at105226am.png)

   >[!NOTE]
   >
   >Você também pode acessar o console diretamente no seu navegador; por exemplo:
   >
   >
   >` https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. Suas notificações serão listadas. Você pode executar ações conforme necessário:

   * [Se inscrever para receber notificações](#subscribing-to-notifications)
   * [Processar suas notificações](#processing-your-notifications)

   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

## Se inscrever para receber notificações {#subscribing-to-notifications}

Para assinar notificações:

1. Abra a caixa de entrada de notificação: no console **Sites,** clique no botão de usuário no canto superior direito e selecione **Caixa de entrada de notificação**.

   ![screen_shot_2012-02-08at105226am-1](assets/screen_shot_2012-02-08at105226am-1.png)

   >[!NOTE]
   >
   >Você também pode acessar o console diretamente no seu navegador; por exemplo:
   >
   >
   >`https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. Clique em **Configurar...** no canto superior esquerdo para abrir a caixa de diálogo de configuração.

   ![screen_shot_2012-02-08at11056am](assets/screen_shot_2012-02-08at111056am.png)

1. Selecione o canal de notificação:

   * **Caixa de entrada**: as notificações serão exibidas na sua caixa de entrada do AEM.
   * **Email**: as notificações serão enviadas por email para o endereço definido no seu perfil de usuário.

   >[!NOTE]
   >
   >Algumas configurações precisam ser definidas para serem notificadas por email. Também é possível personalizar o modelo de email ou adicionar um modelo de email para um novo idioma. Consulte [Configurar a notificação por email](/help/sites-administering/notification.md#configuringemailnotification) para configurar as notificações por email no AEM.

1. Selecione as ações de página para as quais você deseja ser notificado:

   * Ativada: quando uma página é ativada.
   * Desativada: quando uma página é desativada.
   * Excluída (sindicalização): quando uma página é excluída-replicada, isto é, quando uma ação de exclusão executada em uma página é replicada. Quando uma página é excluída ou movida, uma ação de exclusão é replicada automaticamente: a página é excluída na instância de origem em que a ação de exclusão foi executada e na instância de destino definida pelos agentes de replicação.

   * Modificada: quando uma página é modificada.
   * Criada: quando uma página é criada.
   * Excluída: quando uma página é excluída por meio da ação de exclusão de página.
   * Distribuída: quando uma página é distribuída.

1. Defina os caminhos das páginas sobre as quais você será notificado:

   * Clique em **Adicionar** para adicionar uma nova linha à tabela.
   * Clique na célula da tabela **Caminho** e insira o caminho, por exemplo, `/content/docs`.

   * Para ser notificado sobre todas as páginas pertencentes à subárvore, defina **Exata?** como **Não**.
Para ser notificado somente sobre ações na página definidas pelo caminho, defina **Exata?** como **Sim**.

   * Para permitir a regra, defina **Regra** como **Permitir**. Se definida como **Negar**, a regra será negada, mas não removida e poderá ser permitida depois.

   Para remover uma definição, selecione a linha clicando em uma célula de tabela e clique em **Excluir**.

1. Clique em **OK** para salvar a configuração.

## Processar suas notificações {#processing-your-notifications}

Se você tiver optado por receber notificações na sua caixa de entrada do AEM, essa caixa ficará cheia de notificações. É possível [exibir suas notificações, ](#viewing-your-notifications) em seguida, selecionar as notifcações necessárias para:

* Para aprovar, clique em **Aprovar**: o valor na coluna **Leitura** é definido como **verdadeiro**.

* Para excluir, clique em **Excluir**.

![chlimage_1-5](assets/chlimage_1-5.jpeg)
