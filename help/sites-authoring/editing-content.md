---
title: Editar conteúdo da página
seo-title: Editar conteúdo da página
description: Uma vez que a sua página é criada, você poderá editar o conteúdo para fazer atualizações necessárias
seo-description: Uma vez que a sua página é criada, você poderá editar o conteúdo para fazer atualizações necessárias
uuid: 5b4f0a8f-5196-42ea-8413-203783a0b77b
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: f92ed674-5865-4a53-8c3a-369536861f14
docset: aem65
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '3064'
ht-degree: 94%

---


# Editar conteúdo da página{#editing-page-content}

Assim que a página for criada (nova ou como parte de um lançamento ou uma live copy), você pode editar o conteúdo para fazer as atualizações necessárias.

O conteúdo é adicionado usando [componentes](/help/sites-authoring/default-components-console.md) (adequados ao tipo de conteúdo) que podem ser arrastados para a página. Estes podem então ser editados no local, movidos ou excluídos. 

>[!NOTE]
>
>Sua conta precisa dos [direitos de acesso apropriados](/help/sites-administering/security.md) e das [permissões](/help/sites-administering/security.md#permissions) para editar páginas.
>
>Caso encontre algum problema, sugerimos que você entre em contato com o administrador do sistema.

>[!NOTE]
>
>Se a página e/ou o modelo foi configurado corretamente, é possível usar o [layout responsivo](/help/sites-authoring/responsive-layout.md) durante a edição.

>[!NOTE]
>
>Quando estiver no modo de **Edição**, os links em seu conteúdo ficam visíveis, mas **não ficam acessíveis**. Use o [modo de Visualização](#previewingpagestouchoptimizedui) se você deseja navegar usando os links no seu conteúdo.

## Barra de ferramentas da página {#page-toolbar}

A barra de ferramentas da página oferece acesso à funcionalidade adequada, dependendo da configuração da página.

![screen_shot_2018-03-22at111338](assets/screen_shot_2018-03-22at111338.png)

A barra de ferramentas oferece acesso a várias opções. Dependendo do contexto e das configurações atuais, algumas opções podem não estar disponíveis.

* **Ativar/desativar painel lateral**

   Isso abre/fecha o painel lateral, que contém o [Navegador de ativos](/help/sites-authoring/author-environment-tools.md#assets-browser), o [Navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser) e a [Árvore de conteúdo](/help/sites-authoring/author-environment-tools.md#content-tree).

   ![](do-not-localize/screen_shot_2018-03-22at111425.png)

* **Informações da página**

   Fornece acesso ao menu [Informações da página](/help/sites-authoring/author-environment-tools.md#page-information) que inclui os detalhes e as ações da página que podem ser criados na página que incluem a visualizar e editar as informações da página, propriedades de visualização da página e publicar/remover a publicação da página.

   ![](do-not-localize/screen_shot_2018-03-22at111437.png)

* **Emulador**

   Alterna a [barra de ferramentas do emulador](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate), que é usada para emular a aparência da página em outro dispositivo. Isso é alternado automaticamente no modo de layout.

   ![](do-not-localize/screen_shot_2018-03-22at111442.png)

* **ContextHub**

   Abre o [hub de contexto](/help/sites-authoring/ch-previewing.md). Disponível somente no modo de Visualização.

   ![screen_shot_2018-03-22at111543](assets/screen_shot_2018-03-22at111543.png)

* **Título da página**

   Isso é puramente informativo.

   ![screen_shot_2018-03-22at11554](assets/screen_shot_2018-03-22at111554.png)

* **Seletor de modo**

   Indica o [modo](/help/sites-authoring/author-environment-tools.md#page-modes) atual e permite que você selecione outro modo como editar, layout, distorção de tempo ou definição de metas.

   ![chlimage_1-120](assets/chlimage_1-120.png)

* **Visualizar**

   Ativa o [modo de visualização](/help/sites-authoring/editing-content.md#preview-mode). Isso mostra a página da maneira que ela será exibida quando publicada.

   ![chlimage_1-121](assets/chlimage_1-121.png)

* **Anotar**

   Permite adicionar [anotações](/help/sites-authoring/annotations.md) para a página; por exemplo, ao revisar uma página. Após a primeira anotação, o ícone mudará para um número, indicando o número de anotações na página.

   ![](do-not-localize/screen_shot_2018-03-22at111638.png)

### Notificação de status {#status-notification}

Se uma página é parte de um [fluxo de trabalho](/help/sites-authoring/workflows.md) ou de vários fluxos de trabalho, essas informações serão exibidas em uma barra de notificação na parte superior da tela ao editar a página.

![screen_shot_2018-03-22at11739](assets/screen_shot_2018-03-22at111739.png)

>[!NOTE]
>
>A barra de status é visível somente para as contas de usuário com privilégios adequados.

A notificação lista o fluxo de trabalho que está sendo executado em relação à página. Se o usuário estiver envolvido na etapa atual do fluxo de trabalho, opções para [afetar o status do fluxo de trabalho](/help/sites-authoring/workflows-participating.md) e para obter mais informações sobre o fluxo de trabalho também ficarão disponíveis, como:

* **Concluir** - Abre a caixa de diálogo **Concluir item de trabalho**

* **Delegar** - abre a caixa de diálogo **Concluir item** de trabalho

* **Exibir detalhes** - abre a janela **Detalhes** do fluxo de trabalho

Concluir e delegar etapas do fluxo de trabalho por meio da barra de notificação funciona da mesma maneira como ao [participar de fluxos de trabalho](/help/sites-authoring/workflows-participating.md) por meio da caixa de entrada de Notificações.

Se a página estiver sujeita a vários fluxos de trabalho, o número de fluxos de trabalho será exibido na extremidade direita da notificação, junto a botões de seta para permitir que você navegue pelos fluxos de trabalho.

![chlimage_1-122](assets/chlimage_1-122.png)

## Espaço reservado do componente {#component-placeholder}

O placeholder do componente indica onde um componente será posicionado quando você soltá-lo, acima do componente apontado pelo mouse.

* Ao adicionar um novo componente à página (arrastando a partir do navegador do componente):

   ![screen_shot_2018-03-22at111928](assets/screen_shot_2018-03-22at111928.png)

* Ao mover um componente existente:

   ![screen_shot_2018-03-22at112445](assets/screen_shot_2018-03-22at112445.png)

## Inserir um componente {#inserting-a-component}

### Inserir um componente do navegador de componentes {#inserting-a-component-from-the-components-browser}

É possível adicionar um novo componente, usando o [navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser). O [placeholder do componente](#component-placeholder) mostra onde o componente será posicionado:

1. Certifique-se de que a página está no modo de [**edição**](/help/sites-authoring/author-environment-tools.md#page-modes).
1. Abra o [navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser).
1. Arraste o componente para a [posição desejada](#component-placeholder).

1. [Edite](#editmovecopypastedelete) o componente.

>[!NOTE]
>
>Em um dispositivo móvel, o navegador de componentes preencherá a tela inteira. Depois que você começa a arrastar um componente, o navegador será fechado para mostrar a página novamente, para que você possa colocar o componente.

### Inserir um componente do Sistema de parágrafos {#inserting-a-component-from-the-paragraph-system}

É possível adicionar um novo componente, usando a caixa **Arraste componentes aqui**:

1. Certifique-se de que a página está no modo de [**edição**](/help/sites-authoring/author-environment-tools.md#page-modes).
1. Há duas maneiras de selecionar e adicionar um novo componente do sistema de parágrafo:

   * Selecione a opção **Inserir componente** (+) na barra de ferramentas de um componente existente ou na caixa **Arrastar componentes aqui**.

   ![screen_shot_2018-03-22at112536](assets/screen_shot_2018-03-22at112536.png)

   * Se você estiver em um dispositivo de desktop, clique duas vezes na caixa **Arraste componentes aqui**.

   A caixa de diálogo **Inserir novo componente** será aberta para permitir que você selecione o componente desejado: 

   ![screen_shot_2018-03-22at112650](assets/screen_shot_2018-03-22at112650.png)

1. O componente selecionado será adicionado à parte inferior da página. [Edite](#editmovecopypastedelete) o componente conforme necessário.

### Inserir um componente usando o Navegador de ativos   {#inserting-a-component-using-the-assets-browser}

Você também pode adicionar um novo componente à página, arrastando um ativo a partir do [navegador de ativos](/help/sites-authoring/author-environment-tools.md#assets-browser). Isto criará automaticamente um novo componente do tipo apropriado (e que contém o ativo).

Isso é válido para os seguintes tipos de ativos (alguns dependerão do sistema de página/parágrafo):

<table>
 <tbody>
  <tr>
   <th><strong>Tipo de ativo</strong></th>
   <th><strong>Tipo de componente resultante</strong></th>
  </tr>
  <tr>
   <td>Imagem</td>
   <td>Imagem</td>
  </tr>
  <tr>
   <td>Documento</td>
   <td>Download</td>
  </tr>
  <tr>
   <td>Produto</td>
   <td>Produto</td>
  </tr>
  <tr>
   <td>Vídeo</td>
   <td>Flash</td>
  </tr>
  <tr>
   <td>Fragmento de conteúdo</td>
   <td>Fragmento de conteúdo<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Esse comportamento pode ser configurado para a instalação. Consulte [Configuração de um sistema de parágrafo para que a arrastar um ativo crie uma instância de componente](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) para obter mais detalhes.

Para criar um componente arrastando um dos tipos de ativos acima:

1. Certifique-se de que a página está no modo de [**edição**](/help/sites-authoring/author-environment-tools.md#page-modes).
1. Abra o [navegador de ativos](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. Arraste o ativo para a posição desejada. O [placeholder do componente](#component-placeholder) mostra onde o componente será posicionado.

   Um componente, apropriado para o tipo de ativo, será criado no local exigido, e ele conterá o ativo selecionado.

1. [Edite](#editmovecopypastedelete) o componente, se necessário.

>[!NOTE]
>
>Em um dispositivo móvel, o navegador de ativos preencherá a tela inteira. Depois que você começa a arrastar um ativo, o navegador será fechado para mostrar a página novamente, para que você possa colocar o ativo.

Se, durante a navegação pelos ativos, você perceber que precisa fazer uma alteração rápida a um ativo, é possível inicializar o [editor de ativos](/help/assets/manage-assets.md) diretamente do navegador, clicando no ícone de edição ao lado do nome do ativo.

![screen_shot_2018-03-22at112735](assets/screen_shot_2018-03-22at112735.png)

## Editar/configurar/copiar/cortar/excluir/colar {#edit-configure-copy-cut-delete-paste}

Selecionar um componente abrirá a barra de ferramentas. Isto proporciona acesso a várias ações que podem ser executadas no componente.

As ações reais disponíveis para o usuário serão mostradas conforme apropriado, e nem todas as ações podem estar descritas aqui.

![screen_shot_2018-03-22at112909](assets/screen_shot_2018-03-22at112909.png)

* **Editar**

   [Dependendo do tipo de componente,](/help/sites-authoring/default-components.md) permitirá a [edição do conteúdo do componente](#edit-content). Muitas vezes será disponibilizada uma barra de ferramentas.

   ![](do-not-localize/screen_shot_2018-03-22at112936.png)

* **Configurar**

   [Dependendo do tipo de componente,](/help/sites-authoring/default-components.md) permitirá a edição e configuração das propriedades do componente. Frequentemente uma caixa de diálogo será aberta.

   ![](do-not-localize/screen_shot_2018-03-22at112955.png)

* **Copiar**

   Isso copiará o componente para a área de transferência. Após a ação de colar, o componente original será mantido.

   ![](do-not-localize/screen_shot_2018-03-22at113000.png)

* **Recortar**

   Isso copiará o componente para a área de transferência. Após a ação de colar, o componente original será removido.

   ![screen_shot_2018-03-22at113007](assets/screen_shot_2018-03-22at113007.png)

* **Excluir**

   Isso excluirá o componente da página com a sua confirmação.

   ![](do-not-localize/screen_shot_2018-03-22at113012.png)

* **Inserir componente**

   Isso abre a caixa de diálogo para [adicionar um novo componente](/help/sites-authoring/editing-content.md#inserting-a-component-from-the-paragraph-system).

   ![](do-not-localize/screen_shot_2018-03-22at113017.png)

* **Colar**

   Isso colará o componente da área de transferência para a página. O original permanecerá dependendo do uso das funções copiar ou colar.

   * Você pode colar na mesma página ou em uma diferente.
   * O item colado será colocado acima do item no qual você seleciona a ação de colar.
   * A ação de Colar será mostrada somente se houver conteúdo na área de transferência.

   ![screen_shot_2018-03-22at113553](assets/screen_shot_2018-03-22at113553.png)

   >[!NOTE]
   >
   >Se você colar em uma página diferente que já estava aberta antes da operação recortar/copiar, será necessário atualizar a página para ver o conteúdo colado.

* **Grupo**

   Essa ação permite selecionar vários componentes de uma só vez. O mesmo pode ser feito em um dispositivo de desktop ao **manter a tecla Ctrl** ou **Command** pressionada e clicar.

   ![](do-not-localize/screen_shot_2018-03-22at113240.png)

* **Pai**

   Permite que você selecione o componente principal do componente selecionado.

   ![screen_shot_2018-03-22at113028](assets/screen_shot_2018-03-22at113028.png)

* **Layout**

   Isso permite modificar o [layout](/help/sites-authoring/editing-content.md#edit-component-layout) do componente selecionado. Isso se aplica somente ao componente selecionado e não ativa o [modo de layout](/help/sites-authoring/author-environment-tools.md#page-modes) para toda a página.

   ![](do-not-localize/screen_shot_2018-03-22at113044.png)

* **Converta em uma variação de fragmento de experiência**

   Isso permite criar um novo [fragmento de experiência](/help/sites-authoring/experience-fragments.md) do componente selecionado ou adicioná-lo a um fragmento de experiência existente.

   ![](do-not-localize/screen_shot_2018-03-22at113033.png)

## Editar (conteúdo) {#edit-content}

Existem dois métodos de adição e/ou edição do conteúdo dos componentes:

* Abra a caixa de diálogo de [componentes para editar](#component-edit-dialog).
* [Arraste e solte um ativo](#draganddropintocomponent) do navegador de ativos para adicionar diretamente o conteúdo.

### Caixa de diálogo de edição de componente   {#component-edit-dialog}

Você pode abrir um componente para editar o conteúdo usando o [ícone Editar (lápis) na barra de ferramentas do componente](#edit-configure-copy-cut-delete-paste).

As opções de edição exatas dependerão do componente. Para alguns componentes, [todas as ações só estarão disponíveis em modo de tela cheia](#edit-content-full-screen-mode). Por exemplo:

* [Componente de texto](/help/sites-authoring/rich-text-editor.md#main-pars-title-24)

   ![screen_shot_2018-03-22at120215](assets/screen_shot_2018-03-22at120215.png)

* Componente de imagem

   ![screen_shot_2018-03-22at120252](assets/screen_shot_2018-03-22at120252.png)

   >[!NOTE]
   >
   >A edição não funciona em um componente de imagem vazio.
   >
   >
   >Você deve [arrastar ou fazer upload de uma imagem (usando a opção Configurar)](/help/sites-authoring/default-components-foundation.md#image) antes de começar a editá-la.

* Componente de imagem- tela cheia

   [Entrar no modo de tela cheia](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode) para o componente de imagem permite mais espaço para editar a imagem, bem como mostrar opções de edição adicionais como **Inicializar mapa** e **Restaurar zoom**. Além disso, a tela cheia permite selecionar predefinições de corte.

   ![screen_shot_2018-03-22at120529](assets/screen_shot_2018-03-22at120529.png)

* Componentes construídos a partir de mais de um componente básico, como o [componente básico Texto e imagem](/help/sites-authoring/default-components-foundation.md#text-image), primeiro pedem para confirmar qual conjunto de opções de edição você deseja usar:

   ![chlimage_1-123](assets/chlimage_1-123.png)

### Arraste e solte ativos no componente {#drag-and-drop-assets-into-component}

Para tipos de componentes específicos, você pode arrastar e soltar os ativos do navegador de ativos diretamente no componente para atualizar o conteúdo:

| **Tipo de ativo** | **Tipo de componente** |
|---|---|
| Imagem | Imagem |
| Documento | Download |
| Produto | Produto |
| Vídeo | Flash |
| Fragmento de conteúdo | Fragmento do conteúdo |

## Editar (conteúdo) Modo de tela cheia {#edit-content-full-screen-mode}

Para todos os componentes, o modo de tela cheia pode ser acessado com (e fechado de):

![](do-not-localize/chlimage_1-20.png)

Por exemplo, o componente de **Texto:**

![screen_shot_2018-03-22at121616](assets/screen_shot_2018-03-22at121616.png)

>[!NOTE]
>
>Para alguns componentes, o modo de tela cheia terá mais opções disponíveis do que o editor básico no local.

## Mover um componente {#moving-a-component}

Para mover um componente de parágrafo:

1. Selecione o parágrafo a ser movido tocando/clicando e segurando:
1. Arraste o parágrafo para o novo local. O AEM indica onde o parágrafo pode ser colocado. Solte-o no local desejado.

   ![screen_shot_2018-03-22at121821](assets/screen_shot_2018-03-22at121821.png)

1. Seu parágrafo foi movido.

>[!NOTE]
>
>Também é possível usar [Cortar e colar](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) para mover um componente.

## Editar layout de componente {#edit-component-layout}

Em vez de repetidamente alternar entre os modos de edição e de [layout](/help/sites-authoring/responsive-layout.md) para ajustar um componente, você pode selecionar a ação **Layout** referente a um componente para alterar o layout do componente e poupar tempo, uma vez que não é preciso sair do modo de edição.

1. Quando estiver no modo de **Edição** do console de sites, selecionar um componente revela a barra de ferramentas do componente.

   ![screen_shot_2018-03-22at133756](assets/screen_shot_2018-03-22at133756.png)

   Clique ou toque na ação **Layout** para definir o layout do componente.

   ![](do-not-localize/chlimage_1-21.png)

1. Uma vez que a ação Layout é selecionada:

   * As alças de redimensionamento do componente são exibidas.
   * A barra de ferramentas do emulador é exibida na parte superior da tela.
   * As ações de Layout são exibidas na barra de ferramentas do componente no lugar das ações padrão de edição.

   ![screen_shot_2018-03-22at133843](assets/screen_shot_2018-03-22at133843.png)

   Agora é possível modificar o layout do componente da mesma maneira que você faria no [modo de layout](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode).

1. Após fazer as alterações necessárias no layout, clique no botão **Fechar** no menu de ação de componente para concluir a modificação do layout do componente. A barra de ferramentas do componente retornará ao seu estado normal de edição.

   ![](do-not-localize/screen_shot_2018-03-22at133920.png)

>[!NOTE]
>
>O escopo da ação Layout é limitada ao componente selecionado. Por exemplo, se você estiver editando o layout de um componente e clicar em outro componente, a barra de ferramentas de edição padrão (não a barra de ferramentas do layout) será exibida para o componente recém-selecionado e as alças de redimensionamento, bem como a barra de ferramentas do emulador, desaparecerão.
>
>Se precisar editar o layout geral da página, afetando vários componentes, alterne para o [modo de layout](/help/sites-authoring/responsive-layout.md).

## Componentes herdados {#inherited-components}

Componentes herdados podem ser o resultado de vários cenários, incluindo:

* [Gerenciamento de vários sites](/help/sites-administering/msm.md)
* [Lançamentos](/help/sites-authoring/launches.md) (quando com base na live copy).
* Componentes específicos como o Sistema de parágrafo herdado no Geometrixx.

Você pode cancelar (e depois reativar) a herança. Dependendo do componente, essa ação pode estar disponível em:

* **Live Copy**

   A barra de ferramenta do componente, se este estiver em uma página que faça parte de uma live copy ou lançamento (com base em uma live copy). Por exemplo:

   ![screen_shot_2018-03-22at134339](assets/screen_shot_2018-03-22at134339.png)

   A opção Cancelar herança está disponível:

   ![](do-not-localize/screen_shot_2018-03-22at134406.png)

   Ou reativar herança se já foi cancelada:

   ![](do-not-localize/screen_shot_2018-03-22at134417.png)

   A ação de Rollout também está disponível no blueprint ou na Live Copy de origem:

   ![](do-not-localize/screen_shot_2018-03-22at134516.png)

* **Um sistema de parágrafo herdado**

   A caixa de diálogo de configuração. Por exemplo, o Sistema de parágrafo herdado:

   ![chlimage_1-124](assets/chlimage_1-124.png)

## Editar o modelo da página {#editing-the-page-template}

Se a página for baseada em um [modelo editável](/help/sites-authoring/templates.md#editable-and-static-templates), você pode facilmente alternar para o [editor de modelo](/help/sites-authoring/templates.md#editing-templates-template-authors), selecionando **Editar modelo** no [menu de Informações de página](/help/sites-authoring/author-environment-tools.md#page-information).

If the page is based on a [static template](/help/sites-authoring/templates.md#editable-and-static-templates), you can switch to [Design mode](/help/sites-authoring/default-components-designmode.md) using the [page mode selector](/help/sites-authoring/author-environment-tools.md#page-modes) on the toolbar to enable/disable components for use on the page.

É possível ver em qual modelo a página é baseada ao selecionar a página na [Exibição de coluna](/help/sites-authoring/basic-handling.md#column-view) ou na [Exibição de lista](/help/sites-authoring/basic-handling.md#list-view).

## Status da Live Copy   {#live-copy-status}

O modo de página [Status da Live Copy](/help/sites-authoring/author-environment-tools.md#page-modes) permite ter uma visão geral rápida do status da live copy e quais componentes são/não são herdados:

* Borda verde: Herdado
* Borda rosa: Herança cancelada

Por exemplo:

![screen_shot_2018-03-22at134820](assets/screen_shot_2018-03-22at134820.png)

## Adicionar anotações {#adding-annotations}

As [anotações ](/help/sites-authoring/annotations.md) permitem que revisores e outros autores forneçam feedback sobre o seu conteúdo. Isso é usado frequentemente para fins de análise e validação.

## Visualizar páginas   {#previewing-pages}

Existem duas opções para a visualização de uma página:

* [Modo de visualização](#preview-mode) - uma visualização rápida, no local

* [Exibir como publicada](#view-as-published) - uma visualização completa que abre a página em uma nova guia

>[!NOTE]
>
>* Os links no conteúdo são visíveis, mas não são acessíveis no modo Editar.
>* Use qualquer uma das opções de visualização, caso deseje navegar usando os links.
>* Use o [atalho de teclado](/help/sites-authoring/keyboard-shortcuts.md) `Ctrl-Shift-M` para alternar entre a visualização e o último modo selecionado.

>



>[!NOTE]
>
>O cookie do Modo de WCM está definido para ambas as opções.

### Modo de visualização {#preview-mode}

Ao editar o conteúdo, você pode visualizar a página usando o [modo](/help/sites-authoring/author-environment-tools.md#page-modes) de visualização. Este modo:

* Oculta vários mecanismos de edição para fornecer uma visualização rápida de como a página aparecerá na publicação.
* Permite que você use os links para navegação.
* **Não** atualiza o conteúdo da página.

Ao criar, o modo de visualização estará disponível utilizando o ícone no canto superior direito do editor de página:

![chlimage_1-125](assets/chlimage_1-125.png)

### Exibir como publicado {#view-as-published}

A opção **Exibir como publicada** está disponível no menu [Informações da página](/help/sites-authoring/author-environment-tools.md#page-information). Isto abre a página em uma nova guia, atualiza o conteúdo e mostra as páginas exatamente como elas aparecerão no ambiente de publicação.

## Bloquear uma página {#locking-a-page}

O AEM permite bloquear uma página, de modo que ninguém mais possa modificar o conteúdo. Isso é útil quando você está fazendo diversas edições para uma página específica ou quando precisa congelar uma página por pouco tempo.

Uma página pode ser bloqueada através do:

* **Console de sites**

   1. Selecione a página no [modo de seleção](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
   1. Selecione o ícone de bloqueio.

   ![screen_shot_2018-03-22at134928](assets/screen_shot_2018-03-22at134928.png)

* **Editor de página**

   1. Selecione o ícone **Informações da página** para abrir o menu.
   1. Selecione a opção **Bloquear página.**

Uma vez bloqueadas, as informações de exibição do console são atualizadas e, ao editar, um símbolo de cadeado é apresentado na barra de ferramentas.

![screen_shot_2018-03-22at135010](assets/screen_shot_2018-03-22at135010.png)

>[!CAUTION]
>
>O bloqueio de uma página pode ser executado quando se [representa um usuário](/help/sites-administering/security.md#impersonating-another-user). No entanto, uma página bloqueada dessa maneira só pode ser desbloqueada pelo usuário que foi representado ou pelo usuário administrador.
>
>Páginas não podem ser desbloqueadas representando o usuário que as bloqueou.

## Desbloquear uma página {#unlocking-a-page}

Desbloquear uma página é muito semelhante a [bloquear uma página](#locking-a-page). Uma vez bloqueada, as opções de bloqueio são substituídas por ações de desbloqueio.

O menu de Informações da página lista **Desbloquear** como uma opção, e o ícone Bloquear no console de sites é substituído pelo ícone **Desbloquear**.

![screen_shot_2018-03-22at134942](assets/screen_shot_2018-03-22at134942.png)

>[!CAUTION]
>
>O bloqueio de uma página pode ser executado quando se [representa um usuário](/help/sites-administering/security.md#impersonating-another-user). No entanto, uma página bloqueada dessa maneira só pode ser desbloqueada pelo usuário que foi representado ou pelo usuário administrador.
>
>Páginas não podem ser desbloqueadas representando o usuário que as bloqueou.

## Desfazer e refazer edições de página {#undoing-and-redoing-page-edits}

Os ícones a seguir permitem desfazer ou refazer uma ação. Os seguintes itens são mostrados na barra de ferramentas, quando apropriado: 

![](do-not-localize/screen_shot_2018-03-23at093614.png)

>[!NOTE]
>
>O [atalho de teclado](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) `Ctrl-Z` também pode ser usado para desfazer ações de edições em páginas.
>
>The keyboard shortcut `Ctrl-Y` is also availalbe to redo page edit actions.

>[!NOTE]
>
>Consulte [Desfazer e refazer edições de página - A teoria](#undoing-and-redoing-page-edits-the-theory) para obter todos os detalhes do que é possível fazer ao desfazer e refazer edições de página.

## Desfazer e refazer edições de página - a teoria {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>O administrador do sistema pode [configurar vários aspectos dos recursos desfazer/refazer](/help/sites-administering/config-undo.md) de acordo com os requisitos de sua ocorrência.

O AEM armazena um histórico de ações que você executa e a sequência executada. Assim, você desfaz várias ações na ordem executada, bem como refazer para aplicar novamente uma ou mais ações.

Se um elemento na página de conteúdo estiver selecionado (po exemplo, como um componente de texto), o comando de desfazer e refazer será aplicado ao item selecionado.

O comportamento dos comandos desfazer e refazer é semelhante à de outros programas de software. Use os comandos para restaurar o estado recente da sua página Web, conforme você decide sobre o conteúdo. Por exemplo, caso mova um parágrafo de texto para um local diferente na página, você pode usar o comando desfazer para mover o parágrafo de volta. Se você decidir que a posição anterior era melhor, use o comando refazer para “desfazer o desfeito”.

>[!NOTE]
>
>É possível:
>
>* Refazer ações, contanto que não tenha feito uma edição de página desde que usou o comando desfazer.
>* Desfazer um máximo de 20 ações de edição (configuração padrão).
>* Usar também os [Atalhos de teclado](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) para desfazer e refazer.

>



Você pode usar os comandos desfazer e refazer para os seguintes tipos de alterações de páginas:

* Adicionar, editar, remover e mover parágrafos
* Edição no local do conteúdo do parágrafo
* Copiar, recortar e colar itens dentro de uma página

Os campos do formulário que formam a renderização dos componentes não são destinados a terem valores especificados durante a criação páginas. Portanto, os comandos desfazer e refazer não afetam as alterações feitas aos valores desses tipos de componentes. Por exemplo, não é possível desfazer a seleção de um valor em uma lista suspensa.

>[!NOTE]
>
>Permissões especiais são necessárias para desfazer e refazer as alterações nos arquivos e imagens.

>[!NOTE]
>
>O histórico de alterações em arquivos e imagens dura um mínimo de dez horas. Entretanto, além desse tempo, desfazer as alterações não é garantido. O administrador pode alterar a duração padrão de dez horas.

