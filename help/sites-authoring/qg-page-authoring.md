---
title: Guia rápido para a criação de páginas
seo-title: Quick Guide to Authoring Pages
description: Um guia rápido de alto nível para as principais ações de criação de conteúdo de página
seo-description: A quick, high-level guide to the key actions of authoring page content
uuid: ef7ab691-f80d-4eeb-9f4a-afbf1bc83669
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 2d35a2a4-0c8c-4b16-99a6-c6e6d66446dc
docset: aem65
exl-id: a7e16555-9bbe-4da2-817c-4495a0193f3f
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 73%

---

# Guia rápido para a criação de páginas{#quick-guide-to-authoring-pages}

Esses procedimentos são destinados como um guia rápido (alto nível) para as principais ações de criação de conteúdo de página no AEM.

Eles:

* Não são destinados a uma cobertura abrangente.
* Forneça links para a documentação detalhada.

Para obter os detalhes completos sobre a criação com o AEM, consulte:

* [Primeiras etapas para autores](/help/sites-authoring/first-steps.md)
* [Criação de páginas](/help/sites-authoring/page-authoring.md)

## Algumas dicas rápidas {#a-few-quick-hints}

Antes de dar a visão geral das especificidades, veja uma pequena coleção de dicas gerais que vale a pena considerar.

### Console do Sites {#sites-console}

* **Criar**

   * Esse botão está disponível em vários consoles; as opções apresentadas são sensíveis ao contexto, portanto podem variar de acordo com o cenário.

* Reorganização de páginas em uma pasta

   * Isso pode ser feito na [Exibição de lista](/help/sites-authoring/basic-handling.md#list-view). As alterações são aplicadas e visíveis em outras exibições.

#### Criação de página {#page-authoring}

* Links de navegação

   * ***Os links não estão disponíveis para navegação*** quando você estiver em modo **Editar**. Para navegar com links, é necessário [visualizar a página](/help/sites-authoring/editing-content.md#previewing-pages) usando:

      * [Modo de visualização](/help/sites-authoring/editing-content.md#preview-mode)
      * [Exibir como publicado](/help/sites-authoring/editing-content.md#view-as-published)

* As versões não são iniciadas/criadas pelo editor de página; agora isso é feito no console Sites (por meio de **Criar** ou [Linha do tempo](/help/sites-authoring/basic-handling.md#timeline) para um recurso selecionado).

>[!NOTE]
>
>Há vários atalhos de teclado que podem facilitar a experiência de criação.
>
>* [Atalhos de teclado ao editar páginas](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
>* [Atalhos de teclado para Consoles](/help/sites-authoring/keyboard-shortcuts.md)
>

### Encontrar a sua página {#finding-your-page}

Há vários aspectos para localizar uma página. Você pode navegar e/ou pesquisar:

1. Abra o **Sites** console (usando o **Sites** opção no [Navegação global](/help/sites-authoring/basic-handling.md#global-navigation)) - é acionado (lista suspensa) ao selecionar o link do Adobe Experience Manager (parte superior esquerda).

1. Navegue para baixo na árvore, tocando/clicando na página apropriada. A forma como os recursos da página são apresentados depende da exibição usada ([Cartão, Lista ou Coluna](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)):

   ![screen_shot_2018-03-21at160214](assets/screen_shot_2018-03-21at160214.png)

1. Navegue até a árvore usando [a navegação estrutural no cabeçalho](/help/sites-authoring/basic-handling.md#theheaderwithbreadcrumbs), que permite retornar ao local selecionado:

   ![qgtap-01](assets/qgtap-01.png)

1. Você também pode [Pesquisar](/help/sites-authoring/search.md) por uma página. É possível selecionar sua página a partir dos resultados mostrados.

   ![qgtap-03](assets/qgtap-03.png)

### Criar uma nova página {#creating-a-new-page}

Para [criar uma página](/help/sites-authoring/managing-pages.md#creating-a-new-page):

1. [Navegue até o local](#finding-your-page) onde você deseja criar a página.
1. Use o ícone **Criar** e selecione **Página** na lista:

   ![qgtap-02](assets/qgtap-02.png)

1. Isso abrirá o assistente que guiará você pela coleta das informações necessárias ao [criar sua nova página](/help/sites-authoring/managing-pages.md#creating-a-new-page). Siga as instruções na tela.

### Selecionar sua página para mais ações   {#selecting-your-page-for-further-action}

Você pode selecionar uma página para poder executar ações nela. Selecionar uma página atualizará automaticamente a barra de ferramentas para que as ações relevantes para esse recurso sejam exibidas.

Como selecionar uma página depende da exibição usada no console:

1. Exibição de coluna:

   * Toque/clique na miniatura do recurso desejado - a miniatura será sobreposta com uma marca de verificação para mostrar que a opção foi selecionada.

1. Exibição de lista:

   * Toque/clique na miniatura do recurso desejado - a miniatura será sobreposta com uma marca de verificação para mostrar que a opção foi selecionada.

1. Exibição de cartão:

   * Entrar no modo de seleção por [selecionar o recurso desejado](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) com:

      * Dispositivo móvel: toque e segure
      * Desktop: o [ação rápida](/help/sites-authoring/basic-handling.md#quick-actions) - ícone de marca de verificação:

   ![screen_shot_2018-03-21at160503](assets/screen_shot_2018-03-21at160503.png)

   * O cartão será sobreposto como uma marca de verificação para mostrar que a página foi selecionada.

   >[!NOTE]
   >
   >Uma vez no modo de seleção, a variável **Selecionar** O ícone (uma marca de verificação) será alterado para a variável **Desmarcar** ícone (uma cruz).

### Ações rápidas (apenas a exibição de cartão/desktop) {#quick-actions-card-view-desktop-only}

As [ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions) estão disponíveis:

1. [Navegue até a página](#finding-your-page) que deseja realizar a ação.
1. Passe o mouse sobre o cartão que representa o recurso desejado; as ações rápidas são mostradas:

   ![screen_shot_2018-03-21at160503-1](assets/screen_shot_2018-03-21at160503-1.png)

### Editar o seu conteúdo da página {#editing-your-page-content}

1. [Navegue até a página](#finding-your-page) que deseja editar.
1. [Abra a página para edição](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing) usando o ícone Editar (lápis):

   ![screen_shot_2018-03-21at160607](assets/screen_shot_2018-03-21at160607.png)

   Essa opção pode ser acessada com:

   * As [Ações rápidas (apenas a exibição de cartão/área de trabalho)](#quick-actions-card-view-desktop-only) do recurso adequado.
   * A barra de ferramenta quando a sua [página é selecionada](#selectiingyourpageforfurtheraction).

1. Quando o editor for aberto, você poderá:

   * [Adicionar um novo componente para a página](/help/sites-authoring/editing-content.md#inserting-a-component) ao:

      * abrir o painel lateral
      * selecionar a guia componentes (a guia [navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser))
      * arrastar o componente desejado para a página.

     O painel lateral pode ser aberto (ou fechado) com:

     ![Abrir painel lateral](do-not-localize/screen_shot_2018-03-21at160738.png)

   * [Editar o conteúdo de um componente existente](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) na página:

      * Abra a barra de ferramentas do componente com um toque ou clique. Use o ícone de **Editar** (lápis) para abrir a caixa de diálogo.
      * Abra o editor local do componente clicando e segurando ou com um clique duplo e lento. As ações disponíveis serão exibidas (para alguns componentes, será uma seleção limitada).
      * Para ver todas as ações disponíveis, entre no modo de tela cheia utilizando:

     ![Modo de tela cheia](do-not-localize/screen_shot_2018-03-21at160706.png)

   * [Configurar as propriedades de um componente existente](/help/sites-authoring/editing-content.md#component-edit-dialog)

      * Abra a barra de ferramentas do componente com um toque ou clique. Use o ícone de **Configurar** (chave inglesa) para abrir a caixa de diálogo.

   * [Mover um componente](/help/sites-authoring/editing-content.md#moving-a-component):

      * Arrastando o componente desejado para o novo local.
      * Abra a barra de ferramentas do componente com um toque ou clique. Use os ícones **Cortar** e **Colar** conforme necessário.

   * [Copiar (e Colar)](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) um componente:

      * Abra a barra de ferramentas do componente com um toque ou clique. Use os ícones **Copiar** e **Colar** conforme necessário.

   >[!NOTE]
   >
   >Você pode **Colar** os componentes na mesma página ou em uma diferente. Ao colar em uma página diferente que já foi aberta antes da operação de cortar/copiar, essa página precisará de uma atualização. 

   * [Excluir](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) um componente:

      * Abra a barra de ferramentas do componente com um toque ou clique, em seguida, use o ícone **Excluir**.

   * [Adicionar anotações](/help/sites-authoring/annotations.md#annotations) à página:

      * Selecione o modo **Anotar** (ícone de balão de fala). Adicione anotações usando o ícone de **Adicionar anotação** (mais). Saia do modo de anotação usando o X na parte superior direita.

     ![Anotar](do-not-localize/screen_shot_2018-03-21at160813.png)

   * [Visualizar uma página](/help/sites-authoring/editing-content.md#preview-mode) (para ver como ela aparecerá no ambiente de publicação)

      * Selecione **Visualizar** na barra de ferramentas.

   * Retorne ao modo de edição (ou selecione outro modo) usando o seletor suspenso **Editar**.

   >[!NOTE]
   >
   >Para navegar usando links no conteúdo, você deve usar [Modo de visualização](/help/sites-authoring/editing-content.md#preview-mode).

### Editar as propriedades da página   {#editing-the-page-properties}

Existem dois métodos (principais) de [editar propriedades da página](/help/sites-authoring/editing-page-properties.md):

* No console **Sites**:

   1. [Navegue até a página](#finding-your-page) que deseja publicar.
   1. Selecione o ícone de **Propriedades**:

      * As [Ações rápidas (apenas a exibição de cartão/área de trabalho)](#quick-actions-card-view-desktop-only) do recurso adequado.
      * A barra de ferramenta quando a sua [página é selecionada](#selectiingyourpageforfurtheraction).

  ![screen_shot_2018-03-21at160850](assets/screen_shot_2018-03-21at160850.png)

   1. As propriedades da página serão exibidas. É possível fazer atualizações conforme necessário, em seguida, usar a opção Salvar para continuar

* Ao [editar sua página](#editing-your-page-content):

   1. Abra o menu de **Informações da página**.
   1. Selecione **Abrir propriedades** para abrir a caixa de diálogo para editar as propriedades.

  ![screen_shot_2018-03-21at160920](assets/screen_shot_2018-03-21at160920.png)

### Publicar sua página (ou desfazer a publicação) {#publishing-your-page-or-unpublishing}

Existem dois métodos principais de [publicar sua página](/help/sites-authoring/publishing-pages.md) (e também de desfazer a publicação):

* No console **Sites**:

   1. [Navegue até a página](#finding-your-page) que deseja publicar.
   1. Selecione o ícone **Publicação rápida** por meio de:

      * As [Ações rápidas (apenas a exibição de cartão/área de trabalho)](#quick-actions-card-view-desktop-only) do recurso adequado.
      * A barra de ferramentas quando a sua [página é selecionada](#selectiingyourpageforfurtheraction) (também fornece o acesso à opção [Publicar mais tarde](/help/sites-authoring/publishing-pages.md#main-pars-title-12)).

  ![screen_shot_2018-03-21at160957](assets/screen_shot_2018-03-21at160957.png)

* Ao [editar sua página](#editing-your-page-content):

   1. Abra o menu de **Informações da página**.
   1. Selecione **Publicar página**.

  ![screen_shot_2018-03-21at161026](assets/screen_shot_2018-03-21at161026.png)

* Desfazer a publicação de uma página do console só pode ser feito por meio da opção **Gerenciar publicação**, que está disponível somente na barra de ferramentas (não pelas ações rápidas).

  A opção **Cancelar publicação da página** ainda está disponível por meio do menu **Informações da página** no editor.

  ![screen_shot_2018-03-21at161059](assets/screen_shot_2018-03-21at161059.png)

  Consulte [Publicar páginas](/help/sites-authoring/publishing-pages.md#unpublishing-pages) para obter mais informações.

### Mover, copiar e colar ou excluir sua página   {#move-copy-and-paste-or-delete-your-page}

Essas ações podem ser acionadas por:

1. [Navegue até a página](#finding-your-page) que deseja mover, copiar e colar ou excluir.
1. Selecione o ícone copiar (e colar), mover ou excluir, conforme necessário, usando:

   * As [Ações rápidas (apenas a exibição de cartão/área de trabalho)](#quick-actions-card-view-desktop-only) do recurso desejado.
   * A barra de ferramenta quando a sua [página é selecionada](#selecting-your-page-for-further-action).

   Em seguida, depende da sua ação:

   * Copiar:

      * Navegue até o novo local e cole.

   * Mover:

      * O assistente é aberto para coletar as informações necessárias para mover a página. Siga as instruções na tela.

   * Exclua:

      * Você receberá uma solicitação para confirmar a ação.

   >[!NOTE]
   >
   >A opção Excluir não está disponível como uma Ação rápida.

### Bloquear sua página (em seguida, desbloquear) {#locking-your-page-then-unlocking}

[Bloquear uma página](/help/sites-authoring/editing-content.md#locking-a-page) impede que outros autores trabalhem nela enquanto você estiver trabalhando. O ícone/botão Bloquear (e Desbloquear) pode ser encontrado:

* A barra de ferramenta quando a sua [página é selecionada](#selecting-your-page-for-further-action).
* O [menu suspenso Informações da Página](#editing-the-page-properties) ao editar uma página.
* A barra de ferramentas da página ao editar uma página (quando a página estiver bloqueada)

Por exemplo, o ícone de bloqueio tem a seguinte aparência:

![screen_shot_2018-03-21at161124](assets/screen_shot_2018-03-21at161124.png)

### Acessar as referências da página {#accessing-page-references}

[Acesso rápido às referências](/help/sites-authoring/author-environment-tools.md#references) para uma página ou de uma página estão disponíveis no Trilho de referências.

1. Selecione a **Referências** usando o ícone da barra de ferramentas (antes ou depois de [selecionar a página](#selecting-your-page-for-further-action)): 

   ![screen_shot_2018-03-21at161210](assets/screen_shot_2018-03-21at161210.png)

   Uma lista de tipos de referência será exibida:

   ![screen-shot_2019-03-05at114412](assets/screen-shot_2019-03-05at114412.png)

1. Toque/clique no tipo de referência necessário para mostrar mais detalhes e (quando apropriado) executar outras ações.

### Criar uma versão da sua página   {#creating-a-version-of-your-page}

Para criar uma [versão](/help/sites-authoring/working-with-page-versions.md) da página:

1. Para abrir o painel Linha do tempo, selecione **[Linha do tempo](/help/sites-authoring/basic-handling.md#timeline)** usando o ícone da barra de ferramentas (antes ou depois de [selecionar a página](#selecting-your-page-for-further-action)): 

   ![screen_shot_2018-03-21at161355](assets/screen_shot_2018-03-21at161355.png)

1. Toque/clique na seta para cima na parte inferior direita da coluna Linha do tempo para exibir os botões extras; incluindo **Salvar como versão**.

   ![screen-shot_2019-03-05at114600](assets/screen-shot_2019-03-05at114600.png)

1. Selecione **Salvar como versão**, em seguida, **Criar**.

### Restaurar/comparar uma versão da sua página {#restoring-comparing-a-version-of-your-page}

O mesmo mecanismo básico é usado ao restaurar e/ou comparar as versões da sua página:

1. Selecione a **[Linha do tempo](/help/sites-authoring/basic-handling.md#timeline)** usando o ícone da barra de ferramentas (antes ou depois de [selecionar a página](#selecting-your-page-for-further-action)): 

   ![screen_shot_2018-03-21at161355-1](assets/screen_shot_2018-03-21at161355-1.png)

   Se uma versão da sua página já foi salva, ela será listada na Linha do tempo.

1. Toque/clique na versão que deseja restaurar - isso revelará botões de ação adicionais:

   * **Reverter para essa versão**

      * A versão foi restaurada.

   * **Exibir diferenças**

      * A página será aberta com as diferenças (entre as duas versões) destacadas.
