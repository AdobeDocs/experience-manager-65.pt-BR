---
title: Introdução à interface do usuário de criação de Comunicações interativas
seo-title: An introduction to the various user interface elements you can use to author Interactive Communication
description: Uma introdução aos vários elementos da interface do usuário que você pode usar para criar Comunicação interativa
seo-description: An introduction to the various user interface elements you can use to author Interactive Communication
uuid: e8c5b1e8-b2bb-46b4-b42e-1f343192641a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
discoiquuid: 5855d21b-340c-4139-aabe-c3a534cedb98
docset: aem65
feature: Interactive Communication
exl-id: 3d15a723-df6c-4b4a-992e-a6636f4cf3dc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 14%

---

# Introdução à interface do usuário de criação de Comunicações interativas{#introduction-to-interactive-communication-authoring-ui}

A interface do usuário para criação [Comunicação interativa](/help/forms/using/interactive-communications-overview.md) O é intuitivo e oferece o seguinte para criação de canal de impressão e Web da Comunicação interativa:

* Editor de documento de arrastar e soltar WYSIWYG
* Repositório integrado de ativos - os ativos carregados e criados no servidor estão disponíveis no navegador Ativo da interface de criação do Interative Communication

Quando você [criar ou editar uma comunicação interativa existente](../../forms/using/create-interactive-communication.md), use os seguintes elementos da interface do usuário:

* [Barra lateral](#sidebar)
* [Barra de ferramentas da página](#page-toolbar)
* [Barra de ferramentas Componente](#component-toolbar)
* Área de conteúdo

![interface do usuário de criação de comunicações interativas](assets/form-editor.png)

**A.** Barra lateral **B.** Barra de ferramentas da página **C.** Área de conteúdo

## Barra lateral {#sidebar}

![Barra lateral](assets/sidebar-comps-2.png)

**A.** Navegador de canal **B.** Navegador de conteúdo **C.** Navegador de propriedades **D.** Navegador de ativos **E.** Navegador de componentes **F.** Navegador de fontes de dados - Modelo de dados **G.** Navegador de fontes de dados - Conteúdo Principal

<!-- Click to enlarge

![sidebar-comps-3](assets/sidebar-comps-3.png)-->

A barra lateral inclui o seguinte:

* **Navegador de canal**

O navegador Canal ajuda você a alternar entre os canais de impressão e da Web da Comunicação interativa. Com base no canal selecionado no navegador de canais, os navegadores, como Conteúdo e Componentes, exibem as opções.

* **Navegador de conteúdo**
No navegador de conteúdo, é possível ver a hierarquia de objetos do documento para o canal selecionado. O autor pode navegar até um componente específico tocando nesse elemento na Árvore de objetos de documento. O autor pode pesquisar objetos no canal da Web e reorganizá-los a partir dessa árvore.

* **Navegador de propriedades**

   Permite editar as propriedades de um componente. As propriedades mudam de acordo com o componente. Por exemplo, para ver as propriedades do contêiner de documento: Selecione um componente e toque em ![nível de campo](assets/field-level.png) > **Contêiner de documento** e toque em ![cmppr](assets/cmppr.png).

* **Navegador de ativos**
Segmenta diferentes tipos de conteúdo, como fragmentos de layout, imagens, documentos, páginas, vídeos. O autor pode arrastar e soltar ativos na Comunicação interativa.

* **Navegador de componentes**
Inclui componentes que podem ser usados para criar os canais de impressão e da Web de um documento. Você pode arrastar componentes para a Comunicação interativa para adicionar elementos e configurar o elemento adicionado de acordo com os requisitos. A tabela a seguir descreve os componentes listados no navegador Componentes para canais de impressão e da Web:

| **Componente** | **Canal de impressão** | **Canal da Web** | **Funcionalidade** |
|---|---|---|---|
| Gráfico | ✓ | ✓ | Adiciona um gráfico que pode ser usado em uma Comunicação Interativa para representação visual de dados bidimensionais recuperados de um item de coleção de modelo de dados de formulário. |
| Fragmento do documento | ✓ | ✓ | Permite adicionar um componente, texto, lista ou condição reutilizável a uma Comunicação interativa. O componente reutilizável adicionado a uma Comunicação interativa pode ser baseado em modelo de dados de formulário ou sem um modelo de dados de formulário. |
| Imagem | ✓ | ✓ | Permite inserir uma imagem. |
| Painel | - | ✓ | O componente Painel é um espaço reservado para agrupar outros componentes e controla como um grupo de componentes é apresentado em uma Comunicação interativa. Um componente de painel também permite tornar um grupo de componentes repetíveis para o usuário final, como em várias entradas necessárias para preencher as credenciais educacionais. Também é uma boa prática usar um painel cada para uma guia de Comunicação interativa com várias guias. |
| Tabela | &#42; | ✓ | Adiciona uma tabela que permite organizar dados em linhas e colunas. |
| Área de destino | &#42;&#42; | ✓ | Insere uma área de destino em um canal da Web para organizar os componentes específicos do canal da Web. |
| Texto | - | ✓ | Adiciona texto ao canal da Web de uma Comunicação interativa. O texto pode usar objetos de modelo de dados de formulário para tornar o conteúdo dinâmico. |

&#42; Use Fragmentos de layout no canal de impressão para adicionar tabelas.

&#42;&#42; No canal Impressão, as áreas de destino são predefinidas no modelo XDP/impressão. Não é possível adicionar novas áreas de destino usando a interface do usuário de criação Comunicação interativa .

* **Navegador de fontes de dados**
O Navegador de Fontes de Dados exibe as fontes de dados disponíveis no modelo de dados de formulário selecionado durante a criação da Comunicação Interativa.

### Pontos principais para trabalhar com componentes {#key-points-for-working-with-components}

Os pontos principais ao trabalhar com componentes de comunicação interativos são os seguintes:

* Cada componente tem propriedades associadas que controlam sua aparência e funcionalidade. Para configurar as propriedades de um componente, toque no componente e toque em ![cmppr](assets/cmppr.png) para abrir as propriedades do componente no navegador Propriedades.
* Um componente é identificado com seu nome de elemento. Ao tocar ![cmppr](assets/cmppr.png), é possível alterar o nome do componente alterando o valor do campo Nome do elemento no navegador de propriedades. O campo Nome do elemento aceita somente letras, números, hifens (-) e sublinhados (_). Outros caracteres especiais não são permitidos e o nome do elemento deve começar com uma letra.
* Você pode modificar a propriedade Título de um componente Comunicação interativa em linha no editor sem abrir o navegador Propriedades , desde que o título esteja visível na Comunicação interativa. Para fazer isso:

   1. Toque para selecionar um componente que tenha uma propriedade de Título e cuja propriedade Ocultar título esteja desativada.
   1. Toque ![aem_6_3_edit](assets/aem_6_3_edit.png) para tornar o título editável.

   1. Modifique o título e toque na tecla Return ou em qualquer lugar fora do componente para salvar as alterações. Toque na chave Esc para descartar as alterações.

## Barra de ferramentas Componente {#component-toolbar}

![Rótulos da barra de ferramentas do componente](do-not-localize/component_toolbar_labels_new.png)

Ao selecionar um componente, você verá uma barra de ferramentas que permite trabalhar com ele. Há opções para recortar, colar, mover e especificar as propriedades dos componentes. As opções são:

A.**Configurar**: ao tocar em **Configurar**, as propriedades do componente ficam visíveis na barra lateral.

B.**Editar regras**: Ao tocar em Editar regras, o Editor de regras é exibido, onde você pode editar e criar regras para o componente selecionado. No Editor de regras, também é possível selecionar outros objetos de formulário (componentes) e editar/criar regras para esses objetos de formulário.

C.**Copiar**: Você pode usar a opção de copiar para copiar um componente e colá-lo em outros locais na Comunicação interativa.

D.**Recortar**: Você pode usar a opção de recorte para mover um componente de um local para outro na Comunicação interativa.

E. **Excluir**: Permite excluir o componente da Comunicação interativa.

F. **Inserir componente**: Permite inserir um componente acima do componente selecionado.

G. **Colar**: Permite colar o componente cortado ou copiado usando as opções descritas acima.

H. **Grupo**: permite selecionar vários componentes se você deseja cortar, copiar ou colar mais de um componente.

I. **Página principal**: permite selecionar a página principal de um componente.

J. **Exibir expressão SOM:** Permite que você visualize a variável [Expressão SOM](../../forms/using/using-som-expressions-adaptive-forms.md) para o componente.

K: **Agrupar objetos no Painel:** Permite agrupar os componentes em um painel para poder executar operações nesses componentes simultaneamente. Para obter detalhes, consulte [Agrupar objetos no Painel](create-interactive-communication.md#groupobjectspanel).

L. **Adicionar painel filho** (apenas para painéis): Permite adicionar um painel filho ao painel.

M: **Adicionar barra de ferramentas do painel** (somente para painéis):Permite adicionar a Barra de ferramentas do componente Painel . Em seguida, é possível executar outras ações na barra de ferramentas.

Além disso, a variável **Substituir** na barra de ferramentas permite substituir o componente existente por um componente alternativo. A opção não está disponível para o componente Painel .

## Barra de ferramentas da página {#page-toolbar}

A barra de ferramentas Página na parte superior fornece opções que permitem que você visualize a Comunicação interativa e altere suas propriedades. Você pode visualizar a Comunicação interativa ao criá-la e fazer alterações de acordo. Na barra de ferramentas da página, você observa:

* Alternar painel lateral![ alternar-painel-lateral](assets/toggle-side-panel.png): Permite exibir ou ocultar a Barra Lateral.
* Informações da página ![pageinformationad](assets/pageinformationad.png): Permite visualizar as propriedades da página.
* Emulador ![régua](assets/ruler.png): Permite que você emule a aparência de sua Comunicação interativa para diferentes tamanhos de exibição, como tablets e telefones.
* Editar: permite selecionar outros modos, como: Editar, Estilo, Desenvolvedor e Design.

   * Editar: Permite editar as propriedades da Comunicação interativa e seus componentes. Por exemplo, adicionar um componente, soltar uma imagem e especificar campos obrigatórios.
   * Estilo: Permite estilizar a aparência dos componentes da Comunicação interativa. Por exemplo, no modo de estilo, é possível selecionar um painel e especificar a cor do plano de fundo.
   * Desenvolvedor: permite que um desenvolvedor:

      * Descubra o componente de Comunicação interativa.
      * Depure onde e quando está acontecendo, o que, por vezes, ajuda a resolver problemas.
   * Target: Permite ativar ou desativar componentes personalizados ou componentes prontos para uso que não estejam listados na Barra lateral.


* Visualizar: Permite que você visualize a aparência da Comunicação interativa ao publicá-la.
