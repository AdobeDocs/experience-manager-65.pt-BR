---
title: Layout responsivo para suas páginas de conteúdo
description: O Adobe Experience Manager permite que você tenha um layout responsivo para suas páginas.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: 760b8419-5cf8-49c5-8d4f-6691f5256c53
source-git-commit: 0aa929021aa724e4ec18d49fea26f8c0b0538bdc
workflow-type: tm+mt
source-wordcount: '1798'
ht-degree: 59%

---

# Layout responsivo{#responsive-layout}

O AEM permite que você tenha um layout responsivo para suas páginas usando o **Contêiner de layout** componente.

Isso fornece um sistema de parágrafo que permite posicionar componentes em uma grade responsiva. Essa grade pode reorganizar o layout de acordo com o tamanho e o formato do dispositivo/janela. O componente é usado em conjunto com o [**Layout** modo](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode), que permite criar e editar o layout responsivo dependendo do dispositivo.

O container de layout:

* Fornece a opção de encaixe horizontal na grade, juntamente com a capacidade de posicionar componentes lado a lado na grade e definir quando devem ser recolhidos/refluídos.
* Usa pontos de interrupção predefinidos (por exemplo, para telefone, tablet e assim por diante) para permitir que você defina o comportamento necessário do conteúdo para dispositivos/orientações relacionadas.

   * Por exemplo, você pode personalizar o tamanho do componente ou se ele pode ser visualizado em dispositivos específicos.

* Pode ser aninhado para permitir o controle de coluna.

O usuário pode ver como o conteúdo será renderizado para dispositivos específicos usando o emulador.

>[!CAUTION]
>
>Embora o componente de Contêiner de layout esteja disponível na interface clássica, sua funcionalidade completa só está disponível e é compatível na interface habilitada para toque.

O AEM permite um layout responsivo para suas páginas usando uma combinação de mecanismos:

* Componente [**Contêiner de layout**](#adding-a-layout-container-and-its-content-edit-mode)

  Este componente está disponível no [navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser) O e o fornecem um sistema de parágrafo de grade para permitir adicionar e posicionar componentes em uma grade responsiva. Ele também pode ser definido como o sistema de parágrafos padrão na sua página.

* [**Modo de layout**](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)

  Depois que o container de layout é posicionado na página, você pode usar o modo **Layout** para posicionar conteúdo na grade responsiva.

* [**Emulador**](#selecting-a-device-to-emulate)
Isso permite criar e editar sites responsivos que reorganizam o layout de acordo com o tamanho do dispositivo ou da janela, redimensionando componentes interativamente. O usuário pode ver como o conteúdo será renderizado usando o emulador.

Com esses mecanismos de grade responsivos, você pode:

* Usar pontos de interrupção para definir layouts de conteúdo diferentes com base na largura do dispositivo (de acordo com o tipo e a orientação do dispositivo).
* Usar os mesmos pontos de interrupção e layouts de conteúdo para certificar-se de que o conteúdo responde ao tamanho da janela do navegador no desktop.
* Usar o alinhamento com a grade para permitir colocar componentes na grade, redimensionar como necessário e definir quando devem ser recolhidos/refluir para ficarem lado a lado ou acima/abaixo.
* Ocultar componentes de layouts específicos de dispositivos.
* Executar o controle da coluna.

Dependendo do projeto, o Contêiner de layout pode ser usado como o sistema de parágrafo padrão para suas páginas, ou como um componente disponível para ser adicionado à sua página por meio do navegador componente (ou ambos).

>[!NOTE]
>
>Adobe fornece [Documentação do GitHub](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) do layout responsivo como uma referência que pode ser fornecida para desenvolvedores de front-end permitindo que usem a grade AEM fora do AEM, por exemplo, ao criar modelos de HTML estáticos para um futuro site de AEM.

>[!NOTE]
>
>O uso dos mecanismos acima é habilitado pela configuração no modelo. Consulte [Configuração de layout responsivo](/help/sites-administering/configuring-responsive-layout.md) para obter mais informações.

## Definições de layout, emulação de dispositivo e pontos de interrupção {#layout-definitions-device-emulation-and-breakpoints}

Ao criar o conteúdo do seu site, você quer garantir que o conteúdo seja exibido apropriadamente no dispositivo usado para exibi-lo.

O AEM permite definir layouts dependendo da largura do dispositivo:

* O emulador permite simular esses layouts em vários dispositivos. Além do tipo de dispositivo, a orientação, selecionada pela opção **Girar dispositivo**, pode afetar o ponto de interrupção selecionado à medida que a largura muda.
* Os pontos de interrupção são pontos que separam as definições de layout.

   * Eles definem efetivamente a largura máxima (em pixels) de qualquer dispositivo com um layout específico.
   * Normalmente, os pontos de interrupção são válidos para alguns dispositivos, dependendo da largura das telas.
   * O alcance do ponto de interrupção se estende da esquerda até o próximo ponto de interrupção.
   * Não é possível selecionar um ponto de interrupção específico, pois o ponto de interrupção apropriado é selecionado quando você seleciona um dispositivo e uma orientação.

Um dispositivo de **desktop** que não possui uma largura específica utiliza o ponto de interrupção padrão (isto é, todos os itens acima do último ponto de interrupção configurado).

>[!NOTE]
>
>Seria possível definir pontos de interrupção para cada dispositivo individual, mas isso aumentaria consideravelmente o trabalho necessário para a definição e a manutenção do layout.

Ao usar o emulador, você seleciona um dispositivo específico para emulação e definição de layout e o ponto de interrupção relacionado também será destacado. Quaisquer alterações de layout efetuadas serão aplicáveis a outros dispositivos aos quais o ponto de interrupção se aplica, isto é, quaisquer dispositivos posicionados à esquerda do marcador do ponto de interrupção ativo, mas antes do próximo marcador do ponto de interrupção.

Por exemplo, ao selecionar o dispositivo **iPhone 6 Plus** (definido com uma largura de 540 pixels) para emulação e layout, o ponto de interrupção **Telefone** (definido como 768 pixels) também será ativado. Quaisquer alterações de layout feitas na **IPHONE 6** serão aplicáveis a outros dispositivos no âmbito do **Telefones** ponto de interrupção, como **IPHONE 5** (definido como 320 pixels).

![screen_shot_2018-03-23at084058](assets/screen_shot_2018-03-23at084058.png)

## Selecionar um dispositivo para emular {#selecting-a-device-to-emulate}

1. Abra a página que deseja editar. Por exemplo:

   `http://localhost:4502/editor.html/content/we-retail/us/en/experience.html`

1. Selecione o ícone **Emulador** na barra de ferramentas superior:

   ![Emulador](do-not-localize/screen_shot_2018-03-23at084256.png)

1. A barra de ferramentas do emulador se abre.

   ![screen_shot_2018-03-23at084551](assets/screen_shot_2018-03-23at084551.png)

   A barra de ferramentas do emulador exibe opções adicionais de layout:

   * **Girar dispositivo** - Permite girar um dispositivo de orientação vertical (retrato) para a orientação horizontal (paisagem) e vice-versa.

     ![Girar dispositivo](do-not-localize/screen_shot_2018-03-23at084612.png) ![Girar dispositivo](do-not-localize/screen_shot_2018-03-23at084637.png)

   * **Selecionar dispositivo** - defina um dispositivo específico para emular de uma lista (consulte a próxima etapa para obter detalhes)

     ![Selecionar dispositivo](do-not-localize/screen_shot_2018-03-23at084743.png)

1. Para selecionar um dispositivo específico para emular, você pode:

   * Usar o ícone Selecionar dispositivo e escolher um na lista suspensa.
   * Clique no indicador do dispositivo na barra de ferramentas do emulador.

   ![screen_shot_2018-03-23at084818](assets/screen_shot_2018-03-23at084818.png)

1. Depois que um dispositivo específico é selecionado, você pode: 

   * Visualizar o marcador ativo do dispositivo selecionado, como **iPad.**
   * Visualizar o marcador ativo do [ponto de interrupção apropriado](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) como **Tablet.**

   ![screen_shot_2018-03-23at084932](assets/screen_shot_2018-03-23at084932.png)

   * A linha pontilhada azul representa o *dobrar* para o dispositivo selecionado (aqui, um **IPHONE 6**).

   ![screen_shot_2018-03-23at084947](assets/screen_shot_2018-03-23at084947.png)

   * A dobra também pode ser considerada a quebra de linha da página (não deve ser confundida com os [pontos de interrupção](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints)) do conteúdo. Isso é exibido para maior comodidade, a fim de mostrar qual parte do conteúdo o usuário verá no dispositivo antes de rolar a tela.
   * A linha da dobra não será mostrada se a altura do dispositivo que está sendo emulado for maior que o tamanho da tela.
   * A dobra é mostrada para a conveniência do autor e não é mostrada na página publicada.

## Adicionar um contêiner de layout e seu conteúdo (Modo de edição) {#adding-a-layout-container-and-its-content-edit-mode}

Um **Contêiner de layout** é um sistema de parágrafos que:

* Contém outros componentes.
* Define o layout.
* Responde às alterações.

>[!NOTE]
>
>Se ainda não estiver disponível, a variável **Contêiner de layout** deve ser explicitamente [ativado para um sistema/página de parágrafo](/help/sites-administering/configuring-responsive-layout.md) (por exemplo, usando [**Design** modo](/help/sites-authoring/default-components-designmode.md)).

1. O **Contêiner de layout** está disponível como um componente padrão no [Navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser). Aqui, você pode arrastá-lo até o local desejado na página, onde verá o espaço reservado **Arrastar componentes aqui**.
1. Em seguida, você pode adicionar componentes ao container de layout. Esses componentes conterão o conteúdo real:

   ![screen_shot_2018-03-23at085500](assets/screen_shot_2018-03-23at085500.png)

## Selecionar e executar ações em um contêiner de layout (modo Editar) {#selecting-and-taking-action-on-a-layout-container-edit-mode}

Assim como em outros componentes, você pode selecionar e executar ações (recortar, copiar ou excluir) em um Contêiner de layout (no modo **Editar**):

>[!CAUTION]
>
>Visto que um container de layout é um sistema de parágrafo, a exclusão do componente excluirá a grade de layout e todos os componentes (e seu conteúdo) inclusos no container.

1. Se você passar o mouse sobre ou selecionar o espaço reservado da grade, o menu de ação será exibido.

   ![screen_shot_2018-03-23at085357](assets/screen_shot_2018-03-23at085357.png)

   É preciso selecionar a opção **Pai**.

   ![Opção Pai](do-not-localize/screen_shot_2018-03-23at085417.png)

1. Se o componente de layout estiver aninhado, selecione o **Pai** A opção apresenta uma seleção suspensa, que permite selecionar o contêiner de layout aninhado ou seu(s) pai(s).

   Ao passar o mouse sobre os nomes do container no menu suspenso, suas estruturas de tópicos serão exibidas na página.

   * O menor contêiner aninhado do layout será contornado em preto.
   * O próximo contêiner aninhado de layout mais baixo estará em cinza escuro.
   * Cada contêiner sucessivo será destacado por uma sombra mais clara de cinza.

   ![screen_shot_2018-03-23at085636](assets/screen_shot_2018-03-23at085636.png)

1. Essa ação destacará a grade inteira e seu conteúdo. A barra de ferramentas da ação será exibida, na qual é possível selecionar uma ação, como **Excluir.**

   ![screen_shot_2018-03-23at085724](assets/screen_shot_2018-03-23at085724.png)

## Definição de layouts (modo Layout) {#defining-layouts-layout-mode}

>[!NOTE]
>
>Você pode definir um layout separado para cada [ponto de interrupção](#layout-definitions-device-emulation-and-breakpoints) (como determinado pelo tipo e pela orientação do dispositivo emulado).

Para configurar o layout de uma grade responsiva implementada com o Contêiner de layout, use o modo **Layout**.

O modo **Layout** pode ser iniciado de duas maneiras.

* Ao usar o [modo de menu na barra de ferramentas](/help/sites-authoring/author-environment-tools.md#page-modes) e escolher o modo **Layout**

   * Selecione o modo **Layout** da mesma maneira que você alternaria para o modo de **Edição** ou o modo de **Segmentação**.
   * O modo **Layout** permanece persistente e você não sai do modo **Layout** até que você selecione outro modo por meio do seletor de modo.

* Quando [editar um componente individual.](/help/sites-authoring/editing-content.md#edit-component-layout)

   * Ao usar a opção **Layout** no menu de ação rápida do componente, é possível alternar para o modo **Layout**.
   * O modo **Layout** persiste ao editar o componente e reverte para o modo **Editar** assim que o foco muda para outro componente.

Quando estiver no modo de layout, você poderá executar várias ações em uma grade:

* Redimensione os componentes de conteúdo usando os pontos azuis. O redimensionamento sempre se ajustará à grade. Ao redimensionar, a grade de plano de fundo é mostrada para auxiliar o alinhamento:

  ![screen_shot_2018-03-23at090140](assets/screen_shot_2018-03-23at090140.png)

  >[!NOTE]
  >
  >As proporções e as taxas são mantidas quando os componentes como **Imagens** são redimensionados.

* Clique em um componente de conteúdo, a barra de ferramentas permite:

   * **Pai**

     Permite selecionar o componente do contêiner de layout inteiro para executar uma ação em tudo.

   * **Flutuar para a nova linha**

     O componente será movido para uma nova linha, dependendo do espaço disponível na grade.

   * **Ocultar componente**

     O componente ficará invisível (ele pode ser restaurado na barra de ferramentas do contêiner de layout).

  ![screen_shot_2018-03-23at090246](assets/screen_shot_2018-03-23at090246.png)

* Entrada **Layout** você pode clicar no botão **Arraste os componentes para cá** para selecionar o componente inteiro. Isso mostrará a barra de ferramentas para esse modo.

  A barra de ferramentas terá opções diferentes dependendo do estado do componente de layout e dos componentes que pertencem a ele. Por exemplo:

   * **Pai** - seleciona o componente do pai.

     ![Pai](do-not-localize/screen_shot_2018-03-23at090823.png)

   * **Mostrar componentes ocultos** - Revelar todos os componentes ou componentes individuais. O número indica quantos componentes ocultos há atualmente. o contador mostra quantos componentes estão ocultos.

     ![Mostrar componentes ocultos](do-not-localize/screen_shot_2018-03-23at091007.png)

   * **Reverter layout do ponto de interrupção**: reverte para o layout padrão. Isso significa que nenhum layout personalizado será imposto.

     ![Inverter layout do ponto de interrupção](do-not-localize/screen_shot_2018-03-23at091013.png)

   * **Flutuar para uma nova linha** - move o componente uma posição acima, se o espaço permitir.

     ![screen_shot_2018-03-23at090829](assets/screen_shot_2018-03-23at090829.png)

   * **Ocultar componente** - oculta o componente atual.

     ![Ocultar componente](do-not-localize/screen_shot_2018-03-23at090834.png)

     >[!NOTE]
     >
     >No exemplo acima, as ações flutuar e ocultar estão disponíveis porque este Contêiner de layout está aninhado em um Contêiner de layout pai.

   * **Revelar componentes** Selecione os componentes principais para mostrar a barra de ferramentas de ação com a opção **Mostrar componentes ocultos**. Neste exemplo, dois componentes estão ocultos.

     ![screen_shot_2018-03-23at091200](assets/screen_shot_2018-03-23at091200.png)

  Selecionar a opção **Mostrar componentes ocultos** exibirá em azul os componentes que estão ocultos no momento em suas posições originais.

  ![screen_shot_2018-03-23at091224](assets/screen_shot_2018-03-23at091224.png)

  Selecionar **Restaurar tudo** revelará todos os componentes ocultos.
