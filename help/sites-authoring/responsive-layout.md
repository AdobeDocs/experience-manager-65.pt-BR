---
title: Layout responsivo
seo-title: Layout responsivo
description: O AEM permite que você crie um layout responsivo para suas páginas
seo-description: O AEM permite que você crie um layout responsivo para suas páginas
uuid: 4db45d78-9fca-4251-b504-ae3481fd9a8b
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 668d1a8a-c757-4c9f-833f-e5dada4d0384
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Layout responsivo{#responsive-layout}

O AEM permite ter um layout responsivo em suas páginas usando o componente **Contêiner de layout.**

Este componente fornece um sistema de parágrafo que permite posicionar os componentes dentro de uma grade responsiva. Esta grade pode reorganizar o layout de acordo com o dispositivo/tamanho e formato da janela. The component is used in conjunction with the [**Layout **mode](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode), which allows you to create and edit your responsive layout dependent on device.

O contêiner de layout:

* Fornece encaixe horizontal na grade, em conjunto com a capacidade de posicionar os componentes lado a lado na grade e definir quando devem se recolher/refluir.
* Usa pontos de interrupção predefinidos (por exemplo para smartphone, tablet etc.) para permitir que você defina o comportamento obrigatório do conteúdo para dispositivos/orientações relacionados.

   * Por exemplo, você pode personalizar o tamanho do componente ou se o componente pode ser visto em dispositivos específicos.

* Podem ser aninhados para permitir o controle da coluna.

O usuário pode então ver como o conteúdo será processado para dispositivos específicos, usando o emulador.

>[!CAUTION]
>
>Embora o componente do contêiner de layout esteja disponível na interface do usuário clássica, as suas funcionalidades estão disponíveis apenas na interface do usuário habilitada para toque.

O AEM permite um layout responsivo para suas páginas usando uma combinação de mecanismos:

* [**Componente Contêiner **](#adding-a-layout-container-and-its-content-edit-mode)de layout

   This component is available in the [component browser](/help/sites-authoring/author-environment-tools.md#components-browser) and provides a grid-paragraph system to allow you to add and position components within a responsive grid. Ele também pode ser definido como o sistema de parágrafos padrão na sua página.

* [**Modo de layout **](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)

   Once the layout container is positioned on your page you can use the **Layout** mode to position content within the responsive grid.

* [**Emulador **](#selecting-a-device-to-emulate)Permite criar e editar sites responsivos que reorganizam o layout de acordo com o tamanho do dispositivo ou da janela, redimensionando componentes interativamente. O usuário pode observar como o conteúdo será renderizado utilizando o Emulador.

Com estes mecanismos de grade responsivos você pode:

* Usar pontos de interrupção para definir layouts de conteúdo diferentes com base na largura do dispositivo (relacionado ao tipo e à orientação do dispositivo).
* Usar os mesmos pontos de interrupção e layouts de conteúdo para certificar-se de que o conteúdo responde ao tamanho da janela do navegador na área de trabalho.
* Usar o alinhamento com a grade para permitir colocar componentes na grade, redimensionar como necessário e definir quando devem ser recolhidos/refluir para ficarem lado a lado ou acima/abaixo.
* Ocultar componentes de layouts específicos de dispositivos.
* Executar o controle da coluna.

Dependendo do seu projeto, o Contêiner de layout pode ser usado como o sistema de parágrafo padrão para suas páginas ou como um componente disponível para ser adicionado à sua página por meio do navegador de componentes (ou ambos).

>[!NOTE]
>
>Adobe provides [GitHub documentation](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) of the responsive layout as a reference that can be given to front-end developers allowing them to use the AEM grid outside of AEM, for example when creating static HTML mock-ups for a future AEM site.

>[!NOTE]
>
>O uso dos mecanismos acima é habilitado pela configuração no modelo. See [Configuring Responsive Layout](/help/sites-administering/configuring-responsive-layout.md) for further information.

## Definições de layout, emulação de dispositivo e pontos de interrupção {#layout-definitions-device-emulation-and-breakpoints}

Ao criar o conteúdo do seu site, você quer garantir que o conteúdo seja exibido apropriadamente no dispositivo usado para exibi-lo.

O AEM permite que você defina layouts dependendo da largura do dispositivo:

* O emulador permite que você emule esses layouts em vários dispositivos. In addition to the device type, the orientation, selected by the **Rotate device** option, can impact the breakpoint selected as the width changes.
* Os pontos de interrupção são pontos que separam as definições de layout.

   * Eles definem efetivamente a largura máxima (em pixels) de qualquer dispositivo com um layout específico.
   * Normalmente, os pontos de interrupção são válidos para alguns dispositivos, dependendo da largura das telas.
   * O alcance do ponto de interrupção se estende da esquerda até o próximo ponto de interrupção.
   * Não é possível selecionar um ponto de interrupção específico, pois o ponto de interrupção apropriado é selecionado quando você seleciona um dispositivo e uma orientação.

O dispositivo **Desktop** sem uma largura específica e que está relacionado ao ponto de interrupção padrão (isto é, todos os itens acima do último ponto de interrupção configurado).

>[!NOTE]
>
>Seria possível definir pontos de interrupção para cada dispositivo individual, mas isso aumentaria consideravelmente o trabalho necessário para a definição e a manutenção do layout.

Ao usar o emulador, é possível selecionar um dispositivo específico para emulação e definição de layout, sendo que o ponto de interrupção também será selecionado. Quaisquer alterações de layout efetuadas serão aplicáveis a outros dispositivos em que o ponto de interrupção se aplica, isto é, quaisquer dispositivos posicionados à esquerda do marcador do ponto de interrupção ativo, mas antes do próximo marcador do ponto de interrupção.

Por exemplo, com a seleção do dispositivo **iPhone 6 Plus** (definido com largura de 540 pixels) para emulação e layout, o ponto de interrupção **Celular** (definido como 768 pixels) também será ativado. Quaisquer mudanças de layout efetuadas para o **iPhone 6** serão aplicáveis a outros dispositivos no ponto de interrupção **Celulares**, como o **iPhone 5** (definido como 320 pixels).

![screen_shot_2018-03-23at084058](assets/screen_shot_2018-03-23at084058.png)

## Selecting a Device to Emulate {#selecting-a-device-to-emulate}

1. Abra a página para edição. Por exemplo:

   `http://localhost:4502/editor.html/content/we-retail/us/en/experience.html`

1. Selecione o ícone **Emulador** na barra de ferramentas superior:

   ![](do-not-localize/screen_shot_2018-03-23at084256.png)

1. A barra de ferramentas do emulador abre.

   ![screen_shot_2018-03-23at084551](assets/screen_shot_2018-03-23at084551.png)

   A barra de ferramentas do emulador exibe opções adicionais de layout:

   * **Girar dispositivo** - permite que você gire um dispositivo de orientação vertical (retrato) para a orientação horizontal (paisagem) e vice-versa.
   ![](do-not-localize/screen_shot_2018-03-23at084612.png) ![](do-not-localize/screen_shot_2018-03-23at084637.png)

   * **Selecionar dispositivo** - defina um dispositivo específico para emular de uma lista (consulte a próxima etapa para obter detalhes)
   ![](do-not-localize/screen_shot_2018-03-23at084743.png)

1. Para selecionar um dispositivo específico a fim de emulá-lo, é possível:

   * Use o ícone Selecionar dispositivo e selecione em um seletor suspenso.
   * Toque/clique no indicador do dispositivo na barra de ferramentas do emulador.
   ![screen_shot_2018-03-23at084818](assets/screen_shot_2018-03-23at084818.png)

1. Depois que um dispositivo específico é selecionado, você pode: 

   * See the active marker for the selected device, such as **iPad.**
   * See the active marker for the appropriate [breakpoint](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) such as **Tablet.**
   ![screen_shot_2018-03-23at084932](assets/screen_shot_2018-03-23at084932.png)

   * A linha pontilhada azul representa a *dobra* referente ao dispositivo selecionado (aqui, um **iPhone 6**).
   ![screen_shot_2018-03-23at084947](assets/screen_shot_2018-03-23at084947.png)

   * A dobra também pode ser considerada a linha de quebra de página (não confundir com [pontos de interrupção ](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints)) para o conteúdo. Isso é exibido para praticidade em mostrar que parte do conteúdo será vista pelo usuário no dispositivo antes da rolagem de página.
   * A linha para a dobra não será exibida se a altura do dispositivo que está sendo emulado for maior do que o tamanho da tela.
   * A dobra é mostrada para a conveniência do autor e não é mostrada na página publicada.



## Adding a Layout Container and its Content (Edit mode) {#adding-a-layout-container-and-its-content-edit-mode}

Um **Contêiner de layout** é um sistema de parágrafos que:

* Contém outros componentes.
* Define o layout.
* Responde às alterações.

>[!NOTE]
>
>Se ainda não estiver disponível, o **Contêiner de layout** deve ser ativado [explicitamente em um sistema/página de parágrafos](/help/sites-administering/configuring-responsive-layout.md) (por exemplo, quando você usar [**o modo **Design](/help/sites-authoring/default-components-designmode.md)).

1. O **Contêiner de layout** está disponível como um componente padrão no [Navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser). Aqui, você pode arrastá-lo até o local exigido na página, em seguida, é possível observar o espaço reservado **Arrastar componentes aqui**.
1. Em seguida, você pode adicionar componentes ao contêiner de layout. Esses componentes contêm o conteúdo real:

   ![screen_shot_2018-03-23at085500](assets/screen_shot_2018-03-23at085500.png)

## Selecionar e executar ações em um contêiner de layout (modo Editar) {#selecting-and-taking-action-on-a-layout-container-edit-mode}

Assim como em outros componentes, você pode selecionar e executar ações (recortar, copiar ou excluir) em um Contêiner de layout (no modo **Editar**):

>[!CAUTION]
>
>Como o contêiner de layout é um sistema de parágrafos, com a exclusão do componente a grade do layout e todos os componentes (e seu conteúdo) no contêiner são excluídos.

1. Se você tocar ou passar o mouse sobre o espaço reservado da grade, o menu de ação será exibido.

   ![screen_shot_2018-03-23at085357](assets/screen_shot_2018-03-23at085357.png)

   You need to select the **Parent** option.

   ![](do-not-localize/screen_shot_2018-03-23at085417.png)

1. Se o componente de layout estiver aninhado, selecionar a opção **Pai** apresenta uma seleção suspensa, que permite que você selecione o contêiner aninhado do layout ou seus pais.

   Quando você passa o mouse sobre os nomes de contêiner na lista suspensa, os contornos correspondentes serão exibidos na página.

   * O menor contêiner aninhado do layout será contornado em preto.
   * O segundo menor contêiner aninhado do layout estará em um cinza escuro.
   * Cada contêiner sucessivo será destacado por uma sombra mais clara de cinza.
   ![screen_shot_2018-03-23at085636](assets/screen_shot_2018-03-23at085636.png)

1. Essa ação destacará a grade inteira e seu conteúdo. The action toolbar will be shown, from where you can select an action such as **Delete.**

   ![screen_shot_2018-03-23at085724](assets/screen_shot_2018-03-23at085724.png)

## Definição de layouts (modo Layout) {#defining-layouts-layout-mode}

>[!NOTE]
>
>Você pode definir um layout separado para cada [ponto de interrupção](#layout-definitions-device-emulation-and-breakpoints) (como determinado pelo tipo e pela orientação do dispositivo emulado).

To configure the layout of a responsive grid implemented with the Layout Container you need to use the **Layout** mode.

O modo **Layout** pode ser iniciado de duas maneiras.

* By using the [mode menu in the toolbar](/help/sites-authoring/author-environment-tools.md#page-modes) and choosing **Layout** mode

   * Select the **Layout** mode just as you would switch to **Edit** mode or **Targeting** mode.
   * **O modo Layout** permanece persistente e você não sai do modo **Layout** até selecionar outro modo pelo seletor de modo.

* Ao [editar um componente individual.](/help/sites-authoring/editing-content.md#edit-component-layout)

   * Ao usar a opção **Layout** no menu de ações rápidas do componente, é possível alternar para o modo **Layout**.
   * O modo **Layout** é mantido ao editar o componente e é revertido para o modo de **Edição** quando o foco muda para outro componente.

No modo de layout, é possível executar várias ações em uma grade:

* Redimensione os componentes do conteúdo usando os pontos azuis. O redimensionamento sempre se ajusta à grade. A grade do fundo será exibida quando você redimensionar para auxiliar no alinhamento:

   ![screen_shot_2018-03-23at090140](assets/screen_shot_2018-03-23at090140.png)

   >[!NOTE]
   >
   >As proporções e as taxas são mantidas quando os componentes como **Imagens** são redimensionados.

* Clique/toque em um componente de conteúdo, a barra de ferramenta permite que você:

   * **Pai**

      Permite que você selecione o componente de contêiner de layout inteiro para executar ações em todo o processo.

   * **Flutuar até a nova linha**

      O componente será movido para uma nova linha, dependendo do espaço disponível na grade.

   * **Ocultar componente**

      O componente ficará invisível (pode ser restaurado da barra de ferramentas do contêiner de layout).
   ![screen_shot_2018-03-23at090246](assets/screen_shot_2018-03-23at090246.png)

* In **Layout** mode you can tap/click on the **Drag components here** to select the entire component. Isso mostrará a barra de ferramentas para este modo.

   A barra de ferramentas tem opções diferentes, dependendo do status do componente de layout e componentes que pertencem a ela. Por exemplo:

   * **Pai** - Selecione o componente pai.
   ![](do-not-localize/screen_shot_2018-03-23at090823.png)

   * **Mostrar componentes** ocultos - revelar todos os componentes ou os individuais. O número indica quantos componentes ocultos existem atualmente.o contador mostra quantos componentes estão ocultos.
   ![](do-not-localize/screen_shot_2018-03-23at091007.png)

   * **Reverter layout** do ponto de interrupção - Reverte para o layout padrão. Isso significa que nenhum layout personalizado será imposto.
   ![](do-not-localize/screen_shot_2018-03-23at091013.png)

   * **Flutuar para uma nova linha** - Move o componente para cima em uma posição se o espaçamento permitir.
   ![screen_shot_2018-03-23at090829](assets/screen_shot_2018-03-23at090829.png)

   * **Ocultar componente** - Oculta o componente atual.
   ![](do-not-localize/screen_shot_2018-03-23at090834.png)

   >[!NOTE]
   >
   >No exemplo acima, as ações flutuar e ocultar estão disponíveis porque este Contêiner de layout está aninhado em um Contêiner de layout pai.

   * **Revelar componentes** Selecione os componentes principais para mostrar a barra de ferramentas de ação com a opção **Mostrar componentes ocultos**. Neste exemplo, dois componentes estão ocultos.
   ![screen_shot_2018-03-23at091200](assets/screen_shot_2018-03-23at091200.png)

   Selecionar a opção **Mostrar componentes ocultos** exibirá em azul os componentes que estão ocultos no momento em suas posições originais.

   ![screen_shot_2018-03-23at091224](assets/screen_shot_2018-03-23at091224.png)

   Selecionar **Restaurar tudo** revelará todos os componentes ocultos.

