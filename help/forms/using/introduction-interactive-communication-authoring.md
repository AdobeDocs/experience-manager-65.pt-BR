---
title: Introdução à interface de criação da comunicação interativa
description: Uma introdução aos vários elementos da interface do usuário que você pode usar para criar a Comunicação interativa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
docset: aem65
feature: Interactive Communication
exl-id: 3d15a723-df6c-4b4a-992e-a6636f4cf3dc
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 10%

---

# Introdução à interface de criação da comunicação interativa{#introduction-to-interactive-communication-authoring-ui}

A interface de usuário para criação [Comunicação interativa](/help/forms/using/interactive-communications-overview.md) O é intuitivo e fornece o seguinte para criação de canais de impressão e da Web da Comunicação interativa:

* Editor de documento de arrastar e soltar WYSIWYG
* Repositório integrado para ativos - os ativos carregados e criados no servidor estão disponíveis no navegador de ativos da interface de criação da Comunicação interativa

Quando você [criar ou editar uma comunicação interativa existente](../../forms/using/create-interactive-communication.md), você usa os seguintes elementos de interface do usuário:

* [Barra lateral](#sidebar)
* [Barra de ferramentas da página](#page-toolbar)
* [Barra de ferramentas Componente](#component-toolbar)
* Área de conteúdo

![interface do usuário de criação de comunicação interativa](assets/form-editor.png)

**A.** Barra lateral **B.** Barra de ferramentas da página **C** Área de conteúdo

## Barra lateral {#sidebar}

![Barra lateral](assets/sidebar-comps-2.png)

**A.** Navegador do canal **B.** Navegador de conteúdo **C** Navegador de propriedades **D.** Navegador de ativos **E** Navegador de componentes **F** Navegador de fontes de dados - Modelo de dados **G.** Navegador de Fontes de dados - Conteúdo principal

<!-- Click to enlarge

![sidebar-comps-3](assets/sidebar-comps-3.png)-->

A barra lateral inclui o seguinte:

* **Navegador do canal**

O navegador Canal ajuda a alternar entre os canais de impressão e da Web da Comunicação interativa. Com base no canal selecionado no navegador do canal, os navegadores, como Conteúdo e Componentes, exibem as opções.

* **Navegador de conteúdo**
No navegador de conteúdo, é possível ver a hierarquia de objetos do documento para o canal selecionado. O autor pode navegar até um componente específico tocando nesse elemento na Árvore de objetos de documento. O autor pode pesquisar objetos no canal da Web e reorganizá-los a partir dessa árvore.

* **Navegador de propriedades**

  Permite editar as propriedades de um componente. As propriedades mudam de acordo com o componente. Por exemplo, para ver as propriedades do container do documento: selecione um componente e, em seguida, ![nível de campo](assets/field-level.png) > **Contêiner de documentos** e selecione ![cmppr](assets/cmppr.png).

* **Navegador de ativos**
Segrega diferentes tipos de conteúdo, como fragmentos de layout, imagens, documentos, páginas e vídeos. O autor pode arrastar e soltar ativos na Comunicação interativa.

* **Navegador de componentes**
Inclui componentes que você pode usar para criar os canais de impressão e da Web de um documento. Você pode arrastar os componentes para a Comunicação interativa para adicionar elementos e configurar os elementos adicionados de acordo com os requisitos. A tabela a seguir descreve os componentes listados no navegador Componentes para canais de impressão e da Web:

| **Componente** | **Canal de impressão** | **Canal da Web** | **Funcionalidade** |
|---|---|---|---|
| Gráfico | ✓ | ✓ | Adiciona um gráfico que pode ser usado em uma Comunicação interativa para representação visual de dados bidimensionais recuperados de um item de coleção de modelo de dados de formulário. |
| Fragmento do documento | ✓ | ✓ | Permite adicionar um componente, texto, lista ou condição reutilizáveis a uma comunicação interativa. O componente reutilizável adicionado a uma comunicação interativa pode ser baseado em modelo de dados de formulário ou sem um modelo de dados de formulário. |
| Imagem | ✓ | ✓ | Permite inserir uma imagem. |
| Painel | - | ✓ | O componente Painel é um espaço reservado para agrupar outros componentes e controla como um grupo de componentes é apresentado em uma Comunicação interativa. Um componente do painel também permite fazer com que um grupo de componentes seja repetível para o usuário final, como em várias entradas necessárias para preencher credenciais educacionais. Também é uma boa prática usar um painel para cada guia de uma comunicação interativa com várias guias. |
| Tabela | &#42; | ✓ | Adiciona uma tabela que permite organizar dados em linhas e colunas. |
| Área de destino | &#42;&#42; | ✓ | Insere uma área de destino em um canal da Web para organizar os componentes específicos do canal da Web. |
| Texto | - | ✓ | Adiciona texto ao canal da Web de uma Comunicação interativa. O texto pode usar objetos de modelo de dados de formulário para tornar o conteúdo dinâmico. |

&#42; Use fragmentos de layout no canal de impressão para adicionar tabelas.

&#42;&#42; No canal de impressão, as áreas de destino são predefinidas no modelo XDP/impressão. Não é possível adicionar novas áreas de destino usando a interface de criação da Comunicação interativa.

* **Navegador de fontes de dados**
O Navegador de fontes de dados exibe as fontes de dados disponíveis no modelo de dados de formulário selecionado ao criar a Comunicação interativa.

### Pontos principais para trabalhar com componentes {#key-points-for-working-with-components}

Os principais pontos ao trabalhar com componentes de comunicação interativa são os seguintes:

* Cada componente tem propriedades associadas que controlam sua aparência e funcionalidade. Para configurar as propriedades de um componente, selecione o componente e ![cmppr](assets/cmppr.png) para abrir as propriedades do componente no navegador Propriedades.
* Um componente é identificado com seu nome de elemento. Ao selecionar ![cmppr](assets/cmppr.png), você pode alterar o nome do componente alterando o valor do campo Nome do elemento no navegador de propriedades. O campo Nome do elemento aceita somente letras, números, hifens (-) e sublinhados (_). Outros caracteres especiais não são permitidos e o nome do elemento deve começar com uma letra.
* Você pode modificar a propriedade Title de um componente de Comunicação interativa em linha no editor sem abrir o navegador Propriedades, desde que o título esteja visível na Comunicação interativa. Para fazer isso:

   1. Selecione para selecionar um componente que tenha uma propriedade Title e cuja propriedade Hide title esteja desativada.
   1. Selecionar ![aem_6_3_edit](assets/aem_6_3_edit.png) para tornar o título editável.

   1. Modifique o título e selecione a tecla Return ou selecione qualquer lugar fora do componente para salvar as alterações. Selecione a tecla Esc para descartar as alterações.

## Barra de ferramentas Componente {#component-toolbar}

![Rótulos da barra de ferramentas do componente](do-not-localize/component_toolbar_labels_new.png)

Ao selecionar um componente, você vê uma barra de ferramentas que permite trabalhar com ele. Há opções para recortar, colar, mover e especificar as propriedades dos componentes. As opções são:

A.**Configurar**: Ao selecionar **Configurar**, as propriedades do componente ficam visíveis na barra lateral.

B.**Editar regras**: Quando você seleciona Editar regras, o Editor de regras é exibido no qual você pode editar e criar regras para o componente selecionado. No Editor de regras, você também pode selecionar outros objetos de formulário (componentes) e editar/criar regras para esses objetos de formulário.

C **Copiar**: você pode usar a opção de cópia para copiar um componente e colá-lo em outros locais na Comunicação interativa.

D.**Recortar**: Você pode usar a opção de recortar para mover um componente de um local para outro na Comunicação interativa.

E **Excluir**: permite excluir o componente da Comunicação interativa.

F **Inserir componente**: permite inserir um componente acima do componente selecionado.

G. **Colar**: permite colar o componente recortado ou copiado usando as opções descritas acima.

H. **Grupo**: permite selecionar vários componentes se você deseja cortar, copiar ou colar mais de um componente.

I. **Pai**: permite selecionar o primário de um componente.

J. **Exibir expressão SOM:** Permite exibir o [Expressão SOM](../../forms/using/using-som-expressions-adaptive-forms.md) para o componente.

K: **Agrupar objetos no Painel:** Permite agrupar os componentes em um painel para poder executar operações nesses componentes simultaneamente. Para obter detalhes, consulte [Agrupar objetos no Painel](create-interactive-communication.md#groupobjectspanel).

L. **Adicionar painel secundário** (somente para painéis): permite adicionar um painel secundário ao painel.

M: **Adicionar a barra de ferramentas do painel** (somente para painéis):Permite adicionar a barra de ferramentas para o componente Painel. Em seguida, você poderá executar outras ações na barra de ferramentas.

Além disso, a **Substituir** A opção na barra de ferramentas permite substituir o componente existente por um componente alternativo. A opção não está disponível para o componente Painel.

## Barra de ferramentas da página {#page-toolbar}

A barra de ferramentas Página na parte superior fornece opções que permitem visualizar a Comunicação interativa e alterar suas propriedades. Você pode visualizar a comunicação interativa ao criá-la e fazer as alterações apropriadas. Na barra de ferramentas da página, você observa:

* Ativar/desativar painel lateral ![ativar/desativar painel lateral](assets/toggle-side-panel.png): permite mostrar ou ocultar a Barra lateral.
* Informações da página ![pageinformationad](assets/pageinformationad.png): permite a exibição das propriedades da página.
* Emulador ![régua](assets/ruler.png): permite emular a aparência da sua comunicação interativa para diferentes tamanhos de exibição, como tablets e telefones.
* Editar: permite selecionar outros modos, como Editar, Estilo, Desenvolvedor e Design.

   * Editar: permite editar as propriedades da Comunicação interativa e seus componentes. Por exemplo, adicionar um componente, soltar uma imagem e especificar campos obrigatórios.
   * Estilo: permite estilizar a aparência dos componentes da sua Comunicação interativa. Por exemplo, no modo de estilo, é possível selecionar um painel e especificar a cor do plano de fundo.
   * Desenvolvedor: permite que um desenvolvedor:

      * Descubra o que a comunicação interativa é composta.
      * Depure onde e quando está acontecendo, o que, por vezes, ajuda a resolver problemas.

   * Target: permite ativar ou desativar componentes personalizados ou componentes prontos para uso que não estão listados na Barra lateral.

* Visualização: permite que você visualize a aparência da comunicação interativa ao publicá-la.
