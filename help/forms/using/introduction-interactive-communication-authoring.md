---
title: Introdução à interface de criação de comunicação interativa
seo-title: Uma introdução aos vários elementos da interface do usuário que podem ser usados para criar o Interative Communication
description: Uma introdução aos vários elementos da interface do usuário que podem ser usados para criar o Interative Communication
seo-description: Uma introdução aos vários elementos da interface do usuário que podem ser usados para criar o Interative Communication
uuid: e8c5b1e8-b2bb-46b4-b42e-1f343192641a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
discoiquuid: 5855d21b-340c-4139-aabe-c3a534cedb98
docset: aem65
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# Introdução à interface de criação de comunicação interativa{#introduction-to-interactive-communication-authoring-ui}

A interface do usuário para criação de Comunicação [](/help/forms/using/interactive-communications-overview.md) interativa é intuitiva e fornece o seguinte para criação de canais de impressão e da Web da Comunicação interativa:

* Editor de documentos de arrastar e soltar WYSIWYG
* Repositório integrado para ativos - os ativos carregados e criados no servidor estão disponíveis no navegador Asset da interface de criação Interative Communication

Quando você [cria uma nova Comunicação](../../forms/using/create-interactive-communication.md)interativa ou edita uma Comunicação interativa existente, usa os seguintes elementos da interface do usuário:

* [Barra lateral](#sidebar)
* [Barra de ferramentas da página](#page-toolbar)
* [Barra de ferramentas Componente](#component-toolbar)
* Área de conteúdo

![interface do usuário de criação de comunicação interativa](assets/form-editor.png)

**A.** Barra lateral **B.** Barra de ferramentas da página **C.** Área de conteúdo

## Barra lateral {#sidebar}

![Barra lateral](assets/sidebar-comps-2.png)

**A.** Navegador de Canais **B.** Navegador de conteúdo **C.** Propriedades navegador **D.** Navegador de ativos **E.** Navegador de componentes **F.** Navegador de Fontes de Dados - Modelo de Dados **G.** Navegador de Fontes de Dados - Conteúdo Mestre

<!-- Click to enlarge

![sidebar-comps-3](assets/sidebar-comps-3.png)-->

A barra lateral inclui o seguinte:

* **Navegador de Canais**

O navegador de Canais ajuda a alternar entre os canais de impressão e da Web da Comunicação interativa. Com base no canal selecionado no navegador do canal, os navegadores, como Conteúdo e Componentes, exibem as opções.

* **Navegador** de conteúdo No navegador de conteúdo, é possível ver a hierarquia de objetos do documento para o canal selecionado. O autor pode navegar até um componente específico tocando nesse elemento na Árvore de objetos do Documento. O autor pode pesquisar objetos no canal da Web e reorganizá-los a partir dessa árvore.

* **Navegador de propriedades**

   Permite editar as propriedades de um componente. As propriedades mudam de acordo com o componente. Por exemplo, para ver as propriedades do container do documento:
Selecione um componente, toque em nível ![de](assets/field-level.png) campo > Container **do** Documento e, em seguida, em ![cmppr](assets/cmppr.png).

* **Navegador** de ativosSegrega diferentes tipos de conteúdo, como fragmentos de layout, imagens, documentos, páginas, vídeos. O autor pode arrastar e soltar ativos na Comunicação interativa.

* **Navegador** de componentesInclui componentes que podem ser usados para criar canais de impressão e da Web de um documento. Você pode arrastar componentes para a Comunicação interativa para adicionar elementos e configurar elementos adicionados de acordo com os requisitos. A tabela a seguir descreve os componentes listados no navegador Componentes para canais impressos e da Web:

| **Componente** | **Canal de impressão** | **Canal da Web** | **Funcionalidade** |
|---|---|---|---|
| Gráfico | ✓ | ✓ | Adds a chart that you can use in an Interactive Communication for visual representation of two-dimensional data retrieved from an form data model collection item. |
| Fragmento do documento | ✓ | ✓ | Permite adicionar um componente reutilizável, texto, lista ou condição, a uma Comunicação interativa. O componente reutilizável adicionado a uma Comunicação interativa pode ser baseado em modelo de dados de formulário ou sem um modelo de dados de formulário. |
| Imagem | ✓ | ✓ | Permite inserir uma imagem. |
| Painel | - | ✓ | O componente Painel é um espaço reservado para agrupar outros componentes e controla como um grupo de componentes é apresentado em uma Comunicação interativa. Um componente de painel também permite tornar um grupo de componentes repetíveis para o usuário final, como em várias entradas necessárias para o preenchimento de credenciais educacionais. Também é uma boa prática usar um painel cada para uma guia de uma Comunicação interativa com várias guias. |
| Tabela | * | ✓ | Adiciona uma tabela que permite organizar dados em linhas e colunas. |
| Área de destino | ** | ✓ | Insere uma área de público alvo em um canal da Web para organizar os componentes específicos do canal da Web. |
| Texto | - | ✓ | Adiciona texto ao canal da Web de uma Comunicação Interativa. O texto pode usar objetos de modelo de dados de formulário para tornar o conteúdo dinâmico. |

* Use Fragmentos de layout no canal Imprimir para adicionar tabelas.

** No canal de impressão, as áreas do público alvo são predefinidas no modelo XDP/print. Não é possível adicionar novas áreas de público alvo usando a interface de usuário de criação de Comunicação interativa.

* **O Navegador de Fontes** de Dados do Navegador de Fontes de Dados exibe as fontes de dados disponíveis no modelo de dados de formulário selecionado ao criar a Comunicação Interativa.

### Pontos chave para trabalhar com componentes {#key-points-for-working-with-components}

Os pontos principais ao trabalhar com componentes de comunicação interativa são os seguintes:

* Cada componente tem propriedades associadas que controlam sua aparência e funcionalidade. Para configurar as propriedades de um componente, toque no componente e em ![cmppr](assets/cmppr.png) para abrir as propriedades do componente no navegador Propriedades.
* Um componente é identificado com seu nome de elemento. Ao tocar em ![cmppr](assets/cmppr.png), é possível alterar o nome do componente alterando o valor do campo Nome do elemento no navegador de propriedades. O campo Nome do elemento aceita somente letras, números, hífens (-) e sublinhados (_). Outros caracteres especiais não são permitidos e o nome do elemento deve começar com uma letra.
* É possível modificar a propriedade Título de um componente de Comunicação interativa em linha no editor sem abrir o navegador Propriedades, desde que o título esteja visível na Comunicação interativa. Para isso:

   1. Toque para selecionar um componente que tenha uma propriedade Título e cuja propriedade Ocultar título esteja desativada.
   1. Toque em ![aem_6_3_edit](assets/aem_6_3_edit.png) para tornar o título editável.

   1. Modifique o título e toque na tecla Return ou toque em qualquer lugar fora do componente para salvar as alterações. Toque na tecla Esc para descartar as alterações.

## Component toolbar {#component-toolbar}

![Rótulos da barra de ferramentas do componente](do-not-localize/component_toolbar_labels_new.png)

Ao selecionar um componente, você verá uma barra de ferramentas que permite trabalhar com ele. Você obtém opções para recortar, colar, mover e especificar propriedades dos componentes. Suas opções são:

A.**Configurar**: Quando você toca em **Configurar**, as propriedades do componente ficam visíveis na barra lateral.

B.**Editar regras**: Quando você toca em Editar regras, o Editor de regras é exibido no qual você pode editar e criar regras para o componente selecionado. No Editor de regras, também é possível selecionar outros objetos de formulário (componentes) e editar/criar regras para esses objetos de formulário.

C.**Copy**: Você pode usar a opção de cópia para copiar um componente e colá-lo em outros locais no Interative Communication.

D.**Cortar**: Você pode usar a opção de corte para mover um componente de um local para outro na Comunicação interativa.

E. **Excluir**: Permite que você exclua o componente da Comunicação interativa.

F. Componente **Inserir**: Permite inserir um componente acima do componente selecionado.

G. **Colar**: Permite colar o componente que você recortou ou copiou usando as opções descritas acima.

H. **Grupo**: Permite selecionar vários componentes se você deseja recortar, copiar ou colar mais de um componente juntos.

Eu. **Pai**: Permite selecionar o pai de um componente.

J. Expressão SOM da **Visualização:** Permite que você visualização a expressão [](../../forms/using/using-som-expressions-adaptive-forms.md) SOM do componente.

K: Agrupar objetos **no Painel:** Permite agrupar os componentes em um painel para poder executar operações nesses componentes simultaneamente. Para obter detalhes, consulte [Agrupar objetos no Painel](create-interactive-communication.md#groupobjectspanel).

L. **Adicionar painel** filho (somente para painéis): Permite adicionar um painel filho ao painel.

M: **Adicionar barra de ferramentas** do painel (somente para painéis):Permite adicionar a barra de ferramentas para o componente Painel. Em seguida, é possível executar outras ações na barra de ferramentas.

Além disso, a opção **Substituir** na barra de ferramentas permite substituir o componente existente por um componente alternativo. A opção não está disponível para o componente Painel.

## Barra de ferramentas da página {#page-toolbar}

A barra de ferramentas Página na parte superior fornece opções que permitem que você pré-visualização a Comunicação interativa e altere suas propriedades. Você pode pré-visualização a Comunicação interativa ao criá-la e fazer alterações de acordo. Na barra de ferramentas da página, você verá:

* Alternar painel lateral ![alternar painel](assets/toggle-side-panel.png): Permite mostrar ou ocultar a barra lateral.
* Informações da página ![pageinformationad](assets/pageinformationad.png): Permite visualização das propriedades da página.
* Régua ![de emulador](assets/ruler.png): Permite que você emule a aparência da sua Comunicação interativa para tamanhos de exibição diferentes, como tablets e telefones.
* Editar: Permite selecionar outros modos, como: Editar, Estilo, Desenvolvedor e Design.

   * Editar: Permite editar as propriedades da Comunicação interativa e seus componentes. Por exemplo, adicionar um componente, soltar uma imagem e especificar campos obrigatórios.
   * Estilo: Permite estilizar a aparência dos componentes de sua Comunicação interativa. Por exemplo, no modo de estilo, é possível selecionar um painel e especificar sua cor de plano de fundo.
   * Desenvolvedor: Permite que um desenvolvedor:

      * Descubra de que comunicação interativa é composta.
      * Depurar o que está acontecendo onde e quando, o que por sua vez ajuda a resolver problemas.
   * Público alvo: Permite ativar ou desativar componentes personalizados ou componentes prontos para uso que não estejam listados na barra lateral.


* Pré-visualização: Permite que você pré-visualização a aparência da Comunicação interativa ao publicá-la.

