---
title: Publicação de páginas de conteúdo
description: Saiba como publicar páginas de conteúdo no Adobe Experience Manager 6.5.
exl-id: 61144bbe-6710-4cae-a63e-e708936ff360
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 6f3c4f4aa4183552492c6ce5039816896bd67495
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 64%

---

# Publicar páginas {#publishing-pages}

Depois de criar e revisar seu conteúdo no ambiente de criação, [disponibilize-o em seu site público](/help/sites-authoring/author.md#concept-of-authoring-and-publishing) (seu ambiente de publicação).

Isso é chamado de publicação de uma página. Quando você deseja remover uma página do ambiente de publicação, este é o processo de desfazer a publicação. Ao publicar ou desfazer a publicação, a página permanecerá disponível no ambiente do autor para mais alterações até ser excluída.

Você também pode publicar/desfazer a publicação de uma página imediatamente ou em uma data/hora predefinida posteriormente.

>[!NOTE]
>
>Alguns termos relacionados à publicação podem ser confundidos:
>
>* **Publicar/Desfazer a publicação**
>  Esses são os termos principais para as ações que tornam o conteúdo publicamente disponível no ambiente de publicação (ou não).
>
>* **Ativar / Desativar**
>  Estes termos são sinônimos de publicar/desfazer a publicação.
>
>* **Replicar / Replicação**
>  Esses são os termos técnicos que descrevem a movimentação de dados (por exemplo, conteúdo da página, arquivos, código, comentários do usuário) de um ambiente para outro, como ao publicar ou reverter a replicação de comentários do usuário.

## Privilégios Insuficientes {#insufficient-privileges}

Se você não tiver os privilégios necessários para publicar uma página específica:

* Um fluxo de trabalho será acionado para notificar a pessoa apropriada sobre sua solicitação de publicação.
* Este [fluxo de trabalho pode ter sido personalizado](/help/sites-developing/workflows-models.md#main-pars-procedure-6fe6) pela sua equipe de desenvolvimento.
* Uma mensagem será exibida brevemente para notificar que o fluxo de trabalho foi disparado.

## Publicar páginas {#publishing-pages-1}

Dependendo do seu local, é possível publicar:

* [No editor de páginas](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor)
* [No console do Sites](/help/sites-authoring/publishing-pages.md#publishing-from-the-console)

### Publicação por meio do Editor {#publishing-from-the-editor}

Se você estiver editando uma página, ela poderá ser publicada diretamente do editor.

1. Selecione o ícone **Informações da página** para abrir o menu e depois a opção **Publicar página**.

   ![screen_shot_2018-03-21at152734](assets/screen_shot_2018-03-21at152734.png)

1. Se a página tiver referências que precisam de publicação:

   * A página será publicada diretamente se não existirem referências a serem publicadas.
   * Caso a página tenha referências que precisam ser publicadas, elas serão listadas no **Assistente de publicação,** onde é possível:

      * Especifique quais dos ativos ou tags você deseja publicar junto com a página e, em seguida, use o **Publish** para concluir o processo.

      * Usar a opção **Cancelar** para suspender a ação.

   ![chlimage_1](assets/chlimage_1.png)

1. Se você selecionar **Publicar**, replicará a página no ambiente de publicação. No editor de páginas, será mostrado um banner de informações confirmando a ação de publicação.

   ![screen_shot_2018-03-21at152840](assets/screen_shot_2018-03-21at152840.png)

   Ao visualizar a mesma página no console, o status da publicação atualizada estará visível.

   ![pp-01](assets/pp-01.png)

>[!NOTE]
>
>A publicação por meio do editor é um processo superficial, ou seja, somente as páginas selecionadas são publicadas, sem incluir páginas filhas.

>[!NOTE]
>
>Páginas acessadas por [aliases](/help/sites-authoring/editing-page-properties.md#advanced) no editor não podem ser publicadas. As opções de publicação no editor só estão disponíveis para páginas acessadas por meio de seus caminhos reais.

### Publicação por meio do Console {#publishing-from-the-console}

No console do Sites, há duas opções para publicação:

* [Publicação rápida   ](/help/sites-authoring/publishing-pages.md#quick-publish)
* [Gerenciar publicação   ](/help/sites-authoring/publishing-pages.md#manage-publication)

#### Publicação rápida    {#quick-publish}

A **Publicação rápida** serve para casos simples e publica as páginas selecionadas imediatamente, sem qualquer outra interação. Por esse motivo, qualquer referências que ainda não tiver sido publicada, será automaticamente.

Para publicar uma página com a Publicação rápida:

1. Selecione as páginas no console de sites e clique no botão **Publish Rápido**.

   ![pp-02](assets/pp-02.png)

1. Na caixa de diálogo Quick Publish, confirme a publicação clicando em **Publish** ou cancele clicando em **Cancelar**. Lembre-se de que todas as referências não publicadas também serão publicadas automaticamente.

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. Quando a página é publicada, um alerta é exibido confirmando a publicação.

>[!NOTE]
>
>A Publicação rápida é uma publicação superficial, ou seja, somente a(s) página(s) selecionada(s) é(são) publicada(s), mas qualquer página secundária que houver não será.

#### Gerenciar publicação    {#manage-publication}

**Gerenciar Publicação** oferece mais opções do que o Quick Publish, permitindo a inclusão de páginas secundárias, a personalização das referências e o início de qualquer fluxo de trabalho aplicável, além de oferecer a opção de publicação em uma data posterior.

Para publicar ou desfazer a publicação de uma página usando Gerenciar publicação:

1. Selecione as páginas no console de sites e clique no botão **Gerenciar publicação**.

   ![pp-02-1](assets/pp-02-1.png)

1. O assistente para **Gerenciar publicação** é iniciado. A primeira etapa, **Opções**, permite:

   * Optar por publicar ou desfazer a publicação de páginas selecionadas.
   * Escolha executar essa ação agora ou em uma data posterior.

   Publicar mais tarde inicia um fluxo de trabalho para publicar a(s) página(s) selecionada(s) no horário especificado. Por outro lado, desfazer a publicação mais tarde inicia um fluxo de trabalho para desfazer a publicação da(s) página(s) selecionada(s) no horário especificado.

   Caso deseje cancelar a publicação/desfazer a publicação mais tarde, acesse o [Console do Fluxo de trabalhos](/help/sites-administering/workflows.md) para encerrar o fluxo de trabalho correspondente.

   ![chlimage_1-2](assets/chlimage_1-2.png)

   Clique em **Avançar** para continuar.

1. Na próxima etapa do assistente Gerenciar Publicação, **Escopo**, você pode definir o escopo da publicação/despublicação, por exemplo, incluindo páginas filhas e/ou referências.

   ![screen_shot_2018-03-21at153354](assets/screen_shot_2018-03-21at153354.png)

   Você pode usar o botão **Adicionar conteúdo** para adicionar outras páginas à lista de páginas a serem publicadas caso tenha se esquecido de selecionar uma antes de iniciar o assistente para Gerenciar publicação.

   Clicar no botão Adicionar conteúdo inicia o [navegador de caminho](/help/sites-authoring/author-environment-tools.md#path-browser) para permitir a seleção de conteúdo.

   Escolha as páginas necessárias e clique em **Selecionar** para adicionar o conteúdo ao assistente ou em **Cancelar** para cancelar a seleção e retornar ao assistente.

   De volta ao assistente, é possível selecionar um item na lista para configurar suas outras opções, como:

   * Incluir seus filhos.
   * Remova-o da seleção.
   * Gerenciar as referências publicadas.

   ![pp-03](assets/pp-03.png)

   Clicar em **Incluir filhos** abre uma caixa de diálogo que permite:

   * Incluir somente tarefas derivadas imediatas.
   * Incluir somente as páginas modificadas.
   * Incluir somente páginas já publicadas.

   Clique em **Adicionar** para adicionar as páginas filhas à lista de páginas a serem publicadas ou não, com base nas opções de seleção. Clique em **Cancelar** para cancelar a seleção e retornar ao assistente.

   ![chlimage_1-3](assets/chlimage_1-3.png)

   Ao retornar ao assistente, você verá as páginas adicionadas com base na sua escolha de opções na caixa de diálogo Incluir filhos.

   É possível visualizar e modificar as referências a serem publicadas ou não para uma página. Basta selecionar a referência desejada e clicar no botão **Referências publicadas**.

   ![pp-04](assets/pp-04.png)

   A caixa de diálogo **Referências publicadas** exibe as referências para o conteúdo selecionado. Por padrão, todas elas são selecionadas e serão publicadas/não publicadas, mas você pode desmarcá-las para desativá-las e evitar que elas sejam incluídas na ação.

   Clique em **Concluído** para salvar suas alterações ou em **Cancelar** para cancelar a seleção e retornar ao assistente.

   De volta ao assistente, a coluna **Referências** será atualizada para refletir sua seleção de referências a serem publicadas ou não publicadas.

   ![pp-05](assets/pp-05.png)

1. Clique em **Publicar** para concluir.

   De volta ao console de sites, uma mensagem de notificação confirmará a publicação.

1. Se as páginas publicadas estiverem associadas a fluxos de trabalho, elas poderão ser exibidas em uma etapa final de **Fluxos de trabalho** do assistente de publicação.

   >[!NOTE]
   >
   >A etapa **Fluxos de trabalho** é mostrada com base em quais direitos seu usuário pode ou não ter.
   >
   >Consulte as seções [Privilégios Insuficientes](/help/sites-authoring/publishing-pages.md#insufficient-privileges), [Gerenciando o Acesso aos Fluxos de Trabalho](/help/sites-administering/workflows-managing.md) e [Aplicando Fluxos de Trabalho a Páginas](/help/sites-authoring/workflows-applying.md#main-pars-text-5-bvhbkh-refd) para obter detalhes.

   Os recursos são agrupados pelos workflows acionados e cada um recebe opções para:

   * Defina o título do fluxo de trabalho.
   * Manter o pacote de fluxo de trabalho, desde que o fluxo de trabalho tenha [suporte para vários recursos](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support).
   * Definir um título do pacote de fluxo de trabalho se a opção para manter esse pacote tiver sido escolhida.

   Clique em **Publicar** ou **Publicar mais tarde** para concluir a publicação.

   ![chlimage_1-4](assets/chlimage_1-4.png)

## Desfazer a publicação de páginas {#unpublishing-pages}

Desfazer a publicação de uma página fará com que ela seja removida do seu ambiente de publicação, deixando de estar disponível aos seus leitores.

De uma [maneira semelhante à publicação](/help/sites-authoring/publishing-pages.md#publishing-pages), uma ou mais páginas podem ter a publicação desfeita:

* [No editor de páginas](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-editor)
* [Do console do Sites](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-console)

### Desfazer a publicação por meio do editor    {#unpublishing-from-the-editor}

Ao editar uma página, se quiser desfazer a publicação, selecione **Desfazer a publicação da página** no menu **Informações da página**, da mesma maneira que faria para [publicar essa página](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor).

>[!NOTE]
>
>Páginas acessadas por [aliases](/help/sites-authoring/editing-page-properties.md#advanced) no editor não podem ter a publicação desfeita. As opções de publicação no editor só estão disponíveis para páginas acessadas por meio de seus caminhos reais.

### Desfazer a publicação por meio do Console  {#unpublishing-from-the-console}

Da mesma forma que você [usa a opção Gerenciar publicação para publicar](/help/sites-authoring/publishing-pages.md#manage-publication), também pode usá-la para desfazer a publicação.

1. Selecione as páginas no console de sites e clique no botão **Gerenciar publicação**.
1. O assistente para **Gerenciar publicação** é iniciado. Na primeira etapa, **Opções**, selecione **Desfazer a publicação** em vez da opção padrão **Publicar**.

   ![chlimage_1-5](assets/chlimage_1-5.png)

   Da mesma forma que a opção para publicar mais tarde inicia um fluxo de trabalho para publicar essa versão de página no horário especificado, a opção para desativar mais tarde inicia um fluxo de trabalho para desfazer a publicação das páginas selecionadas em um momento específico.

   Caso deseje cancelar a publicação/desfazer a publicação mais tarde, acesse o [Console de Fluxos de trabalho](/help/sites-administering/workflows.md) para encerrar o fluxo de trabalho correspondente.

1. Para concluir o cancelamento da publicação, prossiga com o assistente como faria para [publicar a página](/help/sites-authoring/publishing-pages.md#manage-publication).

## Publicar e desfazer a publicação de uma Árvore {#publishing-and-unpublishing-a-tree}

Quando você tiver inserido ou atualizado um número considerável de páginas de conteúdo, todas residentes na mesma página raiz, pode ser mais fácil publicar toda a árvore em uma única ação.

É possível usar a opção [Gerenciar publicação](/help/sites-authoring/publishing-pages.md#manage-publication) no console do Sites para fazer isso.

1. No console do Sites, selecione a página raiz da árvore que deseja publicar ou desfazer a publicação e selecione **Gerenciar publicação**.
1. O assistente para **Gerenciar publicação** é iniciado. Escolha publicar ou desfazer a publicação e quando isso deve ocorrer e selecione **Próximo** para continuar.
1. Na etapa **Escopo**, selecione a página raiz e selecione **Incluir tarefas derivadas**.

   ![chlimage_1-6](assets/chlimage_1-6.png)

1. Na caixa de diálogo **Incluir Filhos**, desmarque as opções:

   * Incluir somente filhos imediatos
   * Incluir somente páginas já publicadas

   Essas opções são selecionadas por padrão e, portanto, você deve se lembrar de desmarcá-las. Clique em **Adicionar** para confirmar e adicionar o conteúdo à publicação/ao cancelamento da publicação.

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. O assistente **Gerenciar Publicação** lista o conteúdo da árvore para revisão. É possível personalizar ainda mais a seleção adicionando outras páginas ou removendo as selecionadas.

   ![screen_shot_2018-03-21at154237](assets/screen_shot_2018-03-21at154237.png)

   Lembre-se de que você também pode rever as referências a serem publicadas por meio da opção **Referências publicadas**.

1. [Continue o assistente Gerenciar Publicação como de costume](#manage-publication) para concluir a publicação ou o cancelamento da publicação da árvore.

## Determinação do status de publicação {#determining-publication-status}

É possível determinar o status de publicação de uma página:

* Nas [informações de visão geral de recursos do console de sites](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

  ![captura de tela_2019-03-05at112019](assets/screen-shot_2019-03-05at112019.png)

  O status da publicação é mostrado nas exibições [cartão](/help/sites-authoring/basic-handling.md#card-view), [coluna](/help/sites-authoring/basic-handling.md#column-view) e [lista](/help/sites-authoring/basic-handling.md#list-view) do console de sites.

* Na [linha do tempo](/help/sites-authoring/basic-handling.md#timeline)

  ![screen_shot_2018-03-21at154420](assets/screen_shot_2018-03-21at154420.png)

* No menu [Informações da página](/help/sites-authoring/author-environment-tools.md#page-information), ao editar uma página

  ![screen_shot_2018-03-21at154456](assets/screen_shot_2018-03-21at154456.png)
