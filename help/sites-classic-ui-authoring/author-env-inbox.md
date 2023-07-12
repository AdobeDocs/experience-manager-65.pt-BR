---
title: Sua caixa de entrada
description: Você pode receber notificações de várias áreas do AEM, como notificações sobre itens de trabalho ou tarefas que representam ações que você deve executar no conteúdo da página.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 52ea2ca2-eb1c-4bed-b52d-feef37c6afd6
source-git-commit: fd937341e26edd0c3edfced8e862066ebc30f9a3
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Sua caixa de entrada{#your-inbox}

Você pode receber notificações de várias áreas do AEM, como notificações sobre itens de trabalho ou tarefas que representam ações que você deve executar no conteúdo da página.

Você recebe essas notificações em duas caixas de entrada, que são separadas pelo tipo de notificações:

* Uma caixa de entrada onde você pode ver as notificações que recebe como resultado de assinaturas é descrita na seção a seguir.
* Uma caixa de entrada especializada para itens de workflow está descrita na [Participar de fluxos de trabalho](/help/sites-classic-ui-authoring/classic-workflows-participating.md) documento.

## Exibir suas notificações {#viewing-your-notifications}

Para exibir suas notificações:

1. Abra a caixa de entrada de notificações: no **Sites** clique no botão de usuário no canto superior direito e selecione **Caixa de entrada de notificações**.

   ![screen_shot_2012-02-08at105226am](assets/screen_shot_2012-02-08at105226am.png)

   >[!NOTE]
   >
   >Você também pode acessar o console diretamente no seu navegador; por exemplo:
   >
   >
   >` https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. Suas notificações estão listadas. É possível realizar ações conforme necessário:

   * [Assinando notificações](#subscribing-to-notifications)
   * [Processamento de notificações](#processing-your-notifications)

   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

## Assinando notificações {#subscribing-to-notifications}

Para assinar notificações:

1. Abra a caixa de entrada de notificações: no **Sites** clique no botão de usuário no canto superior direito e selecione **Caixa de entrada de notificações**.

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

   * **Caixa de entrada**: as notificações são exibidas na Caixa de entrada AEM.
   * **E-mail**: as notificações são enviadas por email para o endereço definido em seu perfil de usuário.

   >[!NOTE]
   >
   >Algumas configurações devem ser definidas para serem notificadas por email. Também é possível personalizar o template de email ou adicionar um template de email para um novo idioma. Consulte [Configuração da notificação por e-mail](/help/sites-administering/notification.md#configuringemailnotification) para configurar notificações por email no AEM.

1. Selecione as ações de página para as quais deseja ser notificado:

   * Ativado: quando uma página é ativada.
   * Desativado: quando uma página é desativada.
   * Excluída (sindicalização): quando uma página é excluída-replicada, ou seja, quando uma ação de exclusão executada em uma página é replicada.
Quando uma página é excluída ou movida, uma ação de exclusão é automaticamente replicada: a página é excluída na instância de origem em que a ação de exclusão foi executada e na instância de destino definida pelos agentes de replicação.

   * Modificado: quando uma página é modificada.
   * Criado: quando uma página é criada.
   * Excluída: quando uma página é excluída por meio da ação de exclusão da página.
   * Implantada: quando uma página é implantada.

1. Defina os caminhos das páginas para as quais você será notificado:

   * Clique em **Adicionar** para adicionar uma nova linha à tabela.
   * Clique em **Caminho** célula da tabela e insira o caminho, por exemplo, `/content/docs`.

   * Para ser notificado para todas as páginas pertencentes à subárvore, defina **Exata?** para **Não**.
Para ser notificado somente para ações na página definida pelo caminho, defina **Exata?** para **Sim**.

   * Para permitir a regra, defina **Regra** para **Permitir**. Se definida como **Negar**, a regra é negada, mas não removida, e pode ser permitida posteriormente.

   Para remover uma definição, selecione a linha clicando em uma célula de tabela e clique em **Excluir**.

1. Clique em **OK** para salvar a configuração.

## Processamento de notificações {#processing-your-notifications}

Se você optou por receber notificações na Caixa de entrada do AEM, a caixa de entrada estará cheia de notificações. Você pode [exibir suas notificações](#viewing-your-notifications), em seguida, selecione as notificações necessárias para:

* Aprove-a clicando em **Aprovar**: o valor no **Ler** a coluna está definida como **true**.

* Exclua-a clicando em **Excluir**.

![chlimage_1-5](assets/chlimage_1-5.jpeg)
