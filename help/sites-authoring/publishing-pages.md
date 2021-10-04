---
title: Publicar páginas
seo-title: Publishing Pages
description: Publicar páginas
seo-description: null
uuid: 57795e4a-e528-4e74-ad9c-e13f868daebb
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1f5eb646-acc7-49d5-b839-e451e68ada9e
docset: aem65
exl-id: 61144bbe-6710-4cae-a63e-e708936ff360
source-git-commit: 9946bfd3c2701a37d13e6eb6b4c19562ef77d24c
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 85%

---

# Publicar páginas {#publishing-pages}

Depois de criar (e revisar) seu conteúdo no ambiente de criação, o objetivo é [disponibilizá-lo em seu site público ](/help/sites-authoring/author.md#concept-of-authoring-and-publishing)(seu ambiente de publicação).

Isso é referido como a publicação de uma página. Quando você deseja remover uma página do ambiente de publicação, este é o processo de desfazer a publicação. Ao publicar e desfazer a publicação, a página permanece disponível no ambiente de criação para modificações adicionais até que você a exclua.

Você também pode publicar/desfazer a publicação de uma página imediatamente ou em uma data/hora predefinida posteriormente.

>[!NOTE]
>
>Certos termos relacionados à publicação podem ser confundidos:
>
>* **Publicar/Desfazer a publicação**
   >  Esses são os termos principais para as ações que tornam o conteúdo publicamente disponível no ambiente de publicação (ou não).
>
>* **Ativar / Desativar**
   >  Estes termos são sinônimos de publicar/desfazer a publicação.
>
>* **Replicar / Replicação**
   >  Esses são os termos técnicos que descrevem a movimentação de dados (por exemplo, conteúdo da página, arquivos, código, comentários do usuário) de um ambiente para outro, como ao publicar ou reverter a replicação de comentários do usuário.
>


>[!NOTE]
>
>Caso não tenha os privilégios necessários para a publicação de uma página específica:
>
>* Um fluxo de trabalho será acionado para notificar a pessoa adequada sobre a sua solicitação para publicação.
>* Esse [fluxo de trabalho pode ter sido personalizado](/help/sites-developing/workflows-models.md#main-pars-procedure-6fe6) pela sua equipe de desenvolvimento.
>* Uma mensagem será exibida brevemente para notificar que o fluxo de trabalho foi disparado.

>


## Publicar páginas {#publishing-pages-1}

Dependendo da sua localização, você pode publicar:

* [No editor de páginas](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor)
* [Do console de sites](/help/sites-authoring/publishing-pages.md#publishing-from-the-console)

### Publicação por meio do Editor {#publishing-from-the-editor}

Se você estiver editando uma página, ela poderá ser publicada diretamente do editor.

1. Selecione o ícone **Informações da página** para abrir o menu e depois a opção **Publicar página**.

   ![screen_shot_2018-03-21at152734](assets/screen_shot_2018-03-21at152734.png)

1. Se a página tiver referências que precisam de publicação:

   * A página será publicada diretamente se não existirem referências a serem publicadas.
   * Caso a página tenha referências que precisam ser publicadas, elas serão listadas no **Assistente de publicação,** onde é possível:

      * Especificar qual dos ativos/tags/etc. você deseja publicar junto com a página. Em seguida, use **Publicar** para concluir o processo.

      * Usar a opção **Cancelar** para suspender a ação.

   ![chlimage_1](assets/chlimage_1.png)

1. Se você selecionar **Publicar**, replicará a página no ambiente de publicação. No editor de páginas, será mostrado um banner de informações confirmando a ação de publicação.

   ![screen_shot_2018-03-21at152840](assets/screen_shot_2018-03-21at152840.png)

   Ao visualizar a mesma página no console, o status da publicação atualizada estará visível.

   ![pp-01](assets/pp-01.png)

>[!NOTE]
>
>A publicação por meio do Editor é um processo superficial, ou seja, apenas as páginas selecionadas são publicadas, sem incluir páginas filhas.

>[!NOTE]
>
>As páginas acessadas por [aliases](/help/sites-authoring/editing-page-properties.md#advanced) no editor não podem ser publicadas. As opções de publicação no editor só estão disponíveis para páginas acessadas por meio de seus caminhos reais.

### Publicação por meio do Console {#publishing-from-the-console}

No console de sites, existem duas opções para publicação:

* [Publicação rápida   ](/help/sites-authoring/publishing-pages.md#quick-publish)
* [Gerenciar publicação   ](/help/sites-authoring/publishing-pages.md#manage-publication)

#### Publicação rápida    {#quick-publish}

A **Publicação rápida** serve para casos simples e publica as páginas selecionadas imediatamente, sem qualquer outra interação. Por isso, quaisquer referências não publicadas também serão publicadas automaticamente.

Para publicar uma página com a Publicação rápida:

1. Selecione as páginas no console de sites e clique no botão **Publicação rápida**.

   ![pp-02](assets/pp-02.png)

1. Na caixa de diálogo Publicação rápida, confirme a publicação clicando em **Publicar** ou cancele clicando em **Cancelar**. Lembre-se de que todas as referências não publicadas também serão publicadas automaticamente.

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. Quando a página é publicada, é mostrado um alerta confirmando a publicação.

>[!NOTE]
>
>A Publicação rápida é uma publicação superficial, ou seja, apenas as páginas selecionadas são publicadas, sem incluir páginas filhas.

#### Gerenciar publicação    {#manage-publication}

A opção **Gerenciar publicação** oferece mais opções do que a Publicação rápida, permitindo a inclusão de páginas filhas, a personalização das referências e o início de qualquer fluxo de trabalho aplicável, além de oferecer a opção de publicação em uma data posterior.

Para publicar ou desfazer a publicação de uma página usando Gerenciar publicação:

1. Selecione as páginas no console Sites e clique no botão **Gerenciar publicação**.

   ![pp-02-1](assets/pp-02-1.png)

1. O assistente para **Gerenciar publicação** é iniciado. A primeira etapa, **Opções**, permite fazer o seguinte:

   * Optar por publicar ou desfazer a publicação de páginas selecionadas.
   * Optar por realizar a ação agora ou em uma data posterior.

   A publicação posterior inicia um fluxo de trabalho para publicar as páginas selecionadas no horário especificado. Por outro lado, o cancelamento posterior da publicação inicia um fluxo de trabalho para desfazer a publicação das páginas selecionadas em um horário específico.

   Caso deseje cancelar a publicação/desfazer a publicação mais tarde, acesse o [console Sites](/help/sites-administering/workflows.md) para encerrar o fluxo de trabalho correspondente.

   ![chlimage_1-2](assets/chlimage_1-2.png)

   Clique em **Avançar** para continuar.

1. Na próxima etapa do assistente Gerenciar publicação, **Escopo**, você pode definir o escopo da publicação ou do cancelamento da publicação, por exemplo, incluindo páginas filhas e/ou referências.

   ![screen_shot_2018-03-21at153354](assets/screen_shot_2018-03-21at153354.png)

   Você pode usar o botão **Adicionar conteúdo** para adicionar outras páginas à lista de páginas a serem publicadas caso tenha se esquecido de selecionar uma antes de iniciar o assistente para Gerenciar publicação.

   Clicar no botão Adicionar conteúdo inicia o [navegador de caminho](/help/sites-authoring/author-environment-tools.md#path-browser) para permitir a seleção de conteúdo.

   Escolha as páginas necessárias e clique em **Selecionar** para adicionar o conteúdo ao assistente ou em **Cancelar** para cancelar a seleção e retornar ao assistente.

   De volta ao assistente, é possível selecionar um item na lista para configurar suas opções adicionais, como:

   * Incluir seus filhos.
   * Removê-lo da seleção.
   * Gerenciar suas referências publicadas.

   ![pp-03](assets/pp-03.png)

   Clicar em **Incluir filhos** abre uma caixa de diálogo que permite:

   * Incluir somente filhos imediatos.
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
   >A etapa **Fluxos de trabalho** será mostrada com base em quais direitos seu usuário pode ou não possuir. Consulte a observação anterior [nesta página](/help/sites-authoring/publishing-pages.md#main-pars-note-0-ejsjqg-refd) sobre privilégios de publicação, bem como [Gerenciamento do acesso a fluxos de trabalho](/help/sites-administering/workflows-managing.md) e [Aplicação de fluxos de trabalho a páginas](/help/sites-authoring/workflows-applying.md#main-pars-text-5-bvhbkh-refd) para obter detalhes.

   Os recursos são agrupados pelos fluxos de trabalho acionados e cada uma das opções especificadas para:

   * Definir o título do fluxo de trabalho.
   * Manter o pacote de fluxo de trabalho, desde que o fluxo de trabalho tenha [suporte a vários recursos](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support).
   * Definir um título do pacote de fluxo de trabalho se a opção para manter esse pacote tiver sido escolhida.

   Clique em **Publicar** ou **Publicar mais tarde** para concluir a publicação.

   ![chlimage_1-4](assets/chlimage_1-4.png)

## Desfazer a publicação de páginas {#unpublishing-pages}

Desfazer a publicação de uma página fará com que ela seja removida do seu ambiente de publicação, deixando de estar disponível aos seus leitores.

De uma [maneira semelhante à publicação](/help/sites-authoring/publishing-pages.md#publishing-pages), uma ou mais páginas podem ter a publicação desfeita:

* [No editor de páginas](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-editor)
* [Do console de sites](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-console)

### Desfazer a publicação por meio do editor    {#unpublishing-from-the-editor}

Ao editar uma página, se quiser desfazer a publicação, selecione **Desfazer a publicação da página** no menu **Informações da página**, da mesma maneira que faria para [publicar essa página](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor).

>[!NOTE]
>
>As páginas acessadas por [aliases](/help/sites-authoring/editing-page-properties.md#advanced) no editor não podem ter a publicação desfeita. As opções de publicação no editor só estão disponíveis para páginas acessadas por meio de seus caminhos reais.

### Desfazer a publicação por meio do Console  {#unpublishing-from-the-console}

Da mesma forma que você [usa a opção Gerenciar publicação para publicar](/help/sites-authoring/publishing-pages.md#manage-publication), também pode usá-la para desfazer a publicação.

1. Selecione as páginas no console Sites e clique no botão **Gerenciar publicação**.
1. O assistente para **Gerenciar publicação** é iniciado. Na primeira etapa, **Opções**, selecione **Desfazer a publicação** em vez da opção padrão **Publicar**.

   ![chlimage_1-5](assets/chlimage_1-5.png)

   Da mesma forma que a opção para publicar mais tarde inicia um fluxo de trabalho para publicar essa versão de página no horário especificado, a opção para desativar mais tarde inicia um fluxo de trabalho para desfazer a publicação das páginas selecionadas em um momento específico.

   Caso deseje cancelar a publicação/desfazer a publicação mais tarde, acesse o [console Sites](/help/sites-administering/workflows.md) para encerrar o fluxo de trabalho correspondente.

1. Para concluir o cancelamento da publicação, prossiga com o assistente como faria para [publicar a página](/help/sites-authoring/publishing-pages.md#manage-publication).

## Publicar e desfazer a publicação de uma Arvore {#publishing-and-unpublishing-a-tree}

Ao inserir ou atualizar um número considerável de páginas de conteúdo, todas residentes na mesma página raiz, pode ser mais fácil publicar a árvore inteira em uma única ação.

Você pode usar a opção [Gerenciar publicação](/help/sites-authoring/publishing-pages.md#manage-publication) no console de sites para fazer isso.

1. No console de sites, selecione a página raiz da árvore que você deseja publicar ou desfazer a publicação e depois selecione **Gerenciar publicação**.
1. O assistente para **Gerenciar publicação** é iniciado. Opte por publicar ou desfazer a publicação e quando a ação deve ocorrer. Em seguida, selecione **Próximo** para continuar.
1. Na etapa **Escopo**, selecione a página raiz e selecione **Incluir filhos**.

   ![chlimage_1-6](assets/chlimage_1-6.png)

1. Na caixa de diálogo **Incluir filhos**, desmarque as opções:

   * Incluir somente filhos imediatos
   * Incluir somente páginas já publicadas

   Essas opções são selecionadas por padrão e, portanto, você deve se lembrar de desmarcá-las. Clique em **Adicionar** para confirmar e adicionar o conteúdo à publicação ou ao cancelamento da publicação.

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. O assistente para **Gerenciar publicação** lista o conteúdo da árvore para revisão. Você pode personalizar ainda mais a seleção, adicionando outras páginas ou removendo as selecionadas.

   ![screen_shot_2018-03-21at154237](assets/screen_shot_2018-03-21at154237.png)

   Lembre-se de que você também pode rever as referências a serem publicadas por meio da opção **Referências publicadas**.

1. [Prossiga com o assistente Gerenciar publicação como de ](#manage-publication) costume para concluir a publicação ou o cancelamento da publicação da árvore.

## Determinação do status de publicação {#determining-publication-status}

Você pode determinar o status de publicação de uma página:

* Nas [informações de visão geral de recursos do console de sites](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

   ![screen-shot_2019-03-05at112019](assets/screen-shot_2019-03-05at112019.png)

   O status da publicação é mostrado nas exibições [cartão](/help/sites-authoring/basic-handling.md#card-view), [coluna](/help/sites-authoring/basic-handling.md#column-view) e [lista](/help/sites-authoring/basic-handling.md#list-view) do console de sites.

* Na [linha do tempo](/help/sites-authoring/basic-handling.md#timeline)

   ![screen_shot_2018-03-21at154420](assets/screen_shot_2018-03-21at154420.png)

* No menu [Informações da página](/help/sites-authoring/author-environment-tools.md#page-information), ao editar uma página

   ![screen_shot_2018-03-21at154456](assets/screen_shot_2018-03-21at154456.png)
