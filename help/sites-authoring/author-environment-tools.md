---
title: Criação - o ambiente e as ferramentas no AEM
description: O ambiente de criação do AEM fornece vários mecanismos para organização e edição de conteúdo.
uuid: 23a8aa93-b3d2-423b-b402-9e5f3f273d9a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: f488ba79-5bda-46e9-9c15-9a8c3dbfa2ce
docset: aem65
exl-id: 3b3c118b-ca35-484b-a62e-7bec98953123
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '2245'
ht-degree: 40%

---

# Criação - o ambiente e as ferramentas{#authoring-the-environment-and-tools}

O ambiente de criação do AEM fornece vários mecanismos para organização e edição de conteúdo. As ferramentas fornecidas são acessadas de vários consoles e editores de página.

## Gerenciar o site {#managing-your-site}

A variável **Sites** O console permite navegar e gerenciar o site, usando a barra de cabeçalho, a barra de ferramentas, os ícones de ação (aplicáveis ao recurso selecionado), as navegações estruturais e, quando selecionados, os painéis secundários (por exemplo, linha do tempo e referências).

Por exemplo, exibição de coluna:

![ateat-01](assets/ateat-01.png)

## Editar conteúdo da página {#editing-page-content}

É possível editar uma página com o editor de páginas. Por exemplo:

`https://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

![ateat-02](assets/ateat-02.png)

>[!NOTE]
>
>Na primeira vez que você abrir uma página para edição, uma série de slides fornecerá um tour pelos recursos.
>
>Você pode ignorar o tour, se desejar, e repeti-lo a qualquer momento, selecionando um dos **Informações da página** menu.

## Acessar ajuda   {#accessing-help}

Ao editar uma página, a **Ajuda** pode ser acessada de:

* o [**Informações da página**](/help/sites-authoring/editing-page-properties.md#page-properties) seletor; isso mostrará os slides de introdução (como na primeira vez que você acessa o editor).
* o [configuração](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) para componentes específicos (usando o ícone na barra de ferramentas da caixa de diálogo); isso mostrará a ajuda sensível ao contexto.

Mais [os recursos relacionados à ajuda estão disponíveis nos consoles](/help/sites-authoring/basic-handling.md#accessing-help).

## Navegador de componentes   {#components-browser}

O navegador de componentes mostra todos os componentes disponíveis para uso na página atual. Elas podem ser arrastadas para o local apropriado e, em seguida, editadas para adicionar o conteúdo.

O navegador de componentes é uma guia dentro do painel lateral (junto com o [navegador de ativos](/help/sites-authoring/author-environment-tools.md#assets-browser) e a [árvore de conteúdo](/help/sites-authoring/author-environment-tools.md#content-tree)). Para abrir (ou fechar) o painel lateral, use o ícone na parte superior esquerda da barra de ferramentas:

![ateat-03](assets/ateat-03.png)

Ao abrir o painel lateral, ele deslizará do lado esquerdo (selecione a opção **Componentes** se necessário). Ao abrir o, você pode navegar por todos os componentes disponíveis para a sua página.

A aparência e o manuseio real dependem do tipo de dispositivo usado:

>[!NOTE]
>
>Um dispositivo móvel é detectado quando a largura é menor que 1024px. Esse também pode ser o caso de uma janela de desktop pequena.

* **Dispositivo móvel (por exemplo, iPad)**

  O navegador de componentes cobre completamente a página que está sendo editada.

  Para adicionar um componente à sua página, toque e segure o componente desejado e mova-o para a direita - o navegador de componentes será fechado para mostrar a página novamente - onde você pode posicionar o componente.

  ![ateat-04](assets/ateat-04.png)

* **Dispositivo de desktop**

  O navegador de componentes é aberto no lado esquerdo da janela.

  Para adicionar um componente à sua página, clique no componente desejado e arraste-o para o local desejado.

  ![ateat-05](assets/ateat-05.png)

  Os componentes são representados por

   * Nome do componente
   * Grupo do componente (em cinza)
   * Ícone ou abreviação

      * Os ícones dos componentes padrão são monocromáticos.
      * As abreviações são sempre os dois primeiros caracteres do nome do componente.

  Na barra de ferramentas superior, no navegador **Componentes**, é possível:

   * Filtrar componentes por nome.
   * Limitar a exibição para um grupo específico usando a seleção suspensa.

  Para obter uma descrição mais detalhada do componente, clique ou toque no ícone de informações ao lado do componente no navegador **Componentes** (se disponível). Por exemplo, para o **Contêiner de layout**:

  ![ateat-06](assets/ateat-06.png)

  Para mais informações sobre os componentes disponíveis para você, consulte o [Console de componentes](/help/sites-authoring/default-components-console.md).

## Navegador de ativos {#assets-browser}

O navegador de ativos mostra todas as [ativos](/help/assets/home.md) que estão disponíveis para uso direto na sua página atual.

O navegador de ativos é uma guia dentro do painel lateral juntamente com o [componentes procurar](/help/sites-authoring/author-environment-tools.md#components-browser)r e [árvore de conteúdo](/help/sites-authoring/author-environment-tools.md#content-tree). Para abrir ou fechar o painel lateral, use o ícone na parte superior esquerda da barra de ferramentas:

![ateat-03-1](assets/ateat-03-1.png)

Ao abrir o painel lateral, ele deslizará do lado esquerdo. Selecione a guia **Ativos** se necessário.

![ateat-07](assets/ateat-07.png)

Quando o navegador de ativos está aberto, você pode navegar por todos os ativos disponíveis para sua página. A rolagem infinita é usada para expandir a lista quando necessário.

![ateat-08](assets/ateat-08.png)

Para adicionar um ativo à página, selecione e arraste para o local desejado. Pode ser:

* Um componente existente do tipo apropriado.

   * Por exemplo, você pode arrastar um ativo de imagem para um componente de imagem.

* Um [espaço reservado](/help/sites-authoring/editing-content.md#component-placeholder) no sistema de parágrafo para criar um novo componente do tipo adequado.

   * Por exemplo, você pode arrastar um ativo de imagem para o sistema de parágrafo para criar um componente de imagem.

>[!NOTE]
>
>Isso está disponível para ativos específicos e tipos de componentes. Consulte [Inserir um componente usando o Navegador de ativos](/help/sites-authoring/editing-content.md#inserting-a-component-using-the-assets-browser) para obter mais detalhes.

Na barra de ferramentas superior do navegador de ativos, é possível filtrar os ativos ao:

* Nome
* Caminho
* Tipo de ativo, como imagens, manuscritos, documentos, vídeos, páginas, parágrafos e produtos
* Características do ativo, como Orientação (Retrato, Paisagem, Quadrado) e Estilo (Cor, Monocromático, Tons de cinza)

   * Disponível somente para certos tipos de ativos

A aparência e o manuseio real dependem do tipo de dispositivo usado:

>[!NOTE]
>
>Um dispositivo móvel é detectado quando a largura é menor do que 1024px; ou seja, também está em uma janela de desktop pequena.

* **Dispositivo móvel, como o iPad**

  O navegador de ativos cobre completamente a página que está sendo editada.

  Para adicionar um ativo à página, toque e segure o ativo necessário e mova-o para a direita: o navegador de ativos fechará para mostrar a página novamente, onde é possível adicionar o ativo ao componente necessário.

  ![ateat-09](assets/ateat-09.png)

* **Dispositivo de desktop**

  O navegador de ativos é aberto no lado esquerdo da janela.

  Para adicionar um ativo à página, clique no ativo necessário e arraste-o para o componente ou local necessário.

  ![ateat-10](assets/ateat-10.png)

Se você precisar fazer uma alteração rápida em um ativo, pode iniciar o [editor de ativos](/help/assets/manage-assets.md) diretamente do navegador de ativos, clicando no ícone de edição mostrado ao lado do nome do ativo.

![Dispositivo desktop do navegador de ativos](do-not-localize/screen_shot_2018-03-22at142448.png)

## Árvore de conteúdo {#content-tree}

A variável **Árvore de conteúdo** fornece uma visão geral de todos os componentes na página em uma hierarquia para que você possa ver rapidamente como a página é composta.

A Árvore de conteúdo é uma guia dentro do painel lateral (junto com o navegador de componentes e ativos). Para abrir (ou fechar) o painel lateral, use o ícone na parte superior esquerda da barra de ferramentas:

![Árvore de conteúdo](do-not-localize/screen_shot_2018-03-22at142042.png)

Ao abrir o painel lateral, ele deslizará para ser aberto (a partir do lado esquerdo). Selecione a guia **Árvore de conteúdo**, se necessário. Ao abrir, é possível ver uma representação em exibição de árvore da página ou do modelo, para que seja mais fácil entender como o conteúdo é estruturado hierarquicamente. Além disso, em uma página complexa, facilita a alternância entre componentes da página.

![ateat-11](assets/ateat-11.png)

Uma página pode ser facilmente composta por vários componentes do mesmo tipo, portanto a árvore de conteúdo (componente) exibe o texto descritivo (em cinza) após o nome do tipo de componente (em preto). O texto descritivo vem das propriedades comuns do componente, como título ou texto.

Os tipos de componentes serão mostrados no idioma do usuário, enquanto o texto de descrição do componente vem do idioma da página.

Clicar na divisa ao lado de um componente recolherá ou expandirá esse nível.

![screen_shot_2018-03-22at142559](assets/screen_shot_2018-03-22at142559.png)

>[!NOTE]
>
>A Árvore de conteúdo não ficará disponível se você estiver editando uma página em um dispositivo móvel (se a largura do navegador for menor do que 1024px).

Clicar no componente destacará o componente no editor de páginas. As ações disponíveis dependerão do estado da página:

* Por exemplo, uma página básica:

  `https://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html`

  ![ateat-12](assets/ateat-12.png)

  Se o componente que você clicar na árvore for editável, um ícone de chave inglesa aparecerá à direita do nome. Clicar nesse ícone iniciará diretamente a caixa de diálogo de edição do componente.

  ![Ícone de chave inglesa - Editar](do-not-localize/screen_shot_2018-03-22at142725.png)

* Ou uma página que faça parte de um [livecopy](/help/sites-administering/msm.md), em que os componentes são herdados de outra página; por exemplo:

  `https://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

  ![ateat-13](assets/ateat-13.png)

## Fragmentos: navegador do conteúdo associado {#fragments-associated-content-browser}

Se a página contiver Fragmentos do conteúdo, então você também terá acesso ao [navegador para o conteúdo associado](/help/sites-authoring/content-fragments.md#using-associated-content).

## Referências {#references}

**Referências** mostra conexões com a página selecionada:

* Blueprints
* Lançamentos
* Live copies
* Cópias de idioma
* Links de entrada
* Uso do componente de referência: conteúdo emprestado e concedido
* Referências às páginas de produtos (no console Comércio - Produtos)

Abra o console e navegue até o recurso desejado, e abra **Referências** usando:

![screen_shot_2018-03-22at153653](assets/screen_shot_2018-03-22at153653.png)

[Selecione o recurso desejado](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) para mostrar uma lista de tipos de referências relevantes para esse recurso:

![ateat-22](assets/ateat-22.png)

Selecione o tipo de referência apropriado para obter mais informações. Em determinadas situações, outras ações estão disponíveis ao selecionar uma referência específica, incluindo:

* **Links de entrada**, fornecem uma lista de páginas que fazem referência à página, junto com acesso direto a **Editar** uma dessas páginas ao selecionar um link específico

* Instâncias de conteúdo emprestado e concedido usando o componente **Referência**, daqui você pode navegar até a página de referência/referenciada

* [Referências às páginas de produto](/help/commerce/cif-classic/administering/generic.md#showing-product-references) (disponível no console Commerce-Products)
* [Lançamentos](/help/sites-authoring/launches.md), fornecem acesso a lançamentos relacionados
* As [Live Copies](/help/sites-administering/msm.md) exibem os caminhos de todas as live copies que são baseadas no recurso selecionado.
* [Blueprint](/help/sites-administering/msm-best-practices.md), fornece detalhes e várias ações
* [Cópias de idiomas](/help/sites-administering/tc-manage.md#creating-translation-projects-using-the-references-panel), fornece detalhes e várias ações

Por exemplo, você pode corrigir uma referência quebrada em um componente Referência:

![ateat-14](assets/ateat-14.png)

## Eventos - Linha do tempo {#events-timeline}

Para os recursos adequados (por exemplo, as páginas no console **Sites** ou os ativos no console **Ativos**), a [linha do tempo pode ser usada para mostrar a atividade recente de qualquer item selecionado](/help/sites-authoring/basic-handling.md#timeline).

Abra o console e navegue até o recurso desejado, e abra **Linha do tempo** usando:

![ateat-15](assets/ateat-15.png)

[Selecione o recurso desejado](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources), em seguida escolha **Exibir todos** ou **Atividades** para listar as ações recentes nos recursos selecionados:

![ateat-16](assets/ateat-16.png)

## Informações da página {#page-information}

O botão Informações da página (ícone de equalizador) abre um menu que também fornece detalhes sobre a última edição e a última publicação. Dependendo das características da página, de seu site e instância, mais ou menos opções podem estar disponíveis:

![ateat-17](assets/ateat-17.png)

* [Abrir propriedades](/help/sites-authoring/editing-page-properties.md)
* [Página de implantação](/help/sites-administering/msm.md#msm-from-the-ui)
* [Iniciar fluxo de trabalho](/help/sites-authoring/workflows-applying.md#starting-a-workflow-from-the-page-editor)
* [Bloquear página](/help/sites-authoring/editing-content.md#locking-a-page)
* [Publicar página](/help/sites-authoring/publishing-pages.md#main-pars-title-10)
* [Desfazer a publicação da página](/help/sites-authoring/publishing-pages.md#main-pars-title-5)
* [Editar modelo](/help/sites-authoring/templates.md); quando a página for baseada em um [modelo editável](/help/sites-authoring/templates.md#editable-and-static-templates)

* [Exibir como publicado](/help/sites-authoring/editing-content.md#view-as-published)
* Exibir no Admin; abre a página no [console de sites](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)
* [Ajuda](/help/sites-authoring/basic-handling.md#accessing-help)

Por exemplo, quando apropriado, **Informações da página** O também tem as opções:

* [Promover lançamento](/help/sites-authoring/launches-promoting.md) se a página for um lançamento.
* [Abrir na interface clássica](/help/sites-authoring/select-ui.md#switching-to-classic-ui-when-editing-a-page) se essas opções tiverem sido [habilitado por um administrador](/help/sites-administering/enable-classic-ui-editor.md)

Além disso, **Informações da página** O pode fornecer acesso a análises e recomendações, quando apropriado.

## Modos de página   {#page-modes}

Há vários modos ao editar uma página que permitem ações diferentes:

* [Editar](/help/sites-authoring/editing-content.md) - o modo a ser usado ao editar o conteúdo da página.
* [Layout](/help/sites-authoring/responsive-layout.md) - permite que você crie e edite seu layout responsivo dependente do dispositivo (se a página for baseada em um contêiner de layout)

* [Andaime](/help/sites-authoring/scaffolding.md) - ajudá-lo a criar um grande conjunto de páginas que compartilham a mesma estrutura, mas têm conteúdo diferente.
* [Desenvolvedor](/help/sites-developing/developer-mode.md) - permite executar várias ações (requer privilégios). Isso inclui a inspeção dos detalhes técnicos de uma página e seus componentes.

* [Design](/help/sites-authoring/default-components-designmode.md) - permite ativar/desativar componentes para uso em uma página e configurar o design do componente (se a página for baseada em um [modelo estático](/help/sites-authoring/templates.md#editable-and-static-templates)).

* [Direcionamento](/help/sites-authoring/content-targeting-touch.md) - aumentar a relevância do conteúdo por meio do direcionamento e da medição em todos os canais.
* [Activity Map](/help/sites-authoring/page-analytics-using.md#analyticsvisiblefromthepageeditor) - mostra os dados do Analytics para a página.

* [Timewarp](/help/sites-authoring/working-with-page-versions.md#timewarp) - permite exibir um estado de páginas em um momento específico.
* [Status da Live Copy](/help/sites-authoring/editing-content.md#live-copy-status) - permite uma visão geral rápida do status da live copy e de quais componentes não são herdados.
* [Visualização](/help/sites-authoring/editing-content.md#previewing-pages)- o modo usado para visualizar a página da forma que será exibida no ambiente de publicação; ou navegar usando os links no conteúdo.

* [Anotar](/help/sites-authoring/annotations.md) - usado para adicionar ou exibir anotações na página.

Você pode acessar esses itens usando os ícones no canto superior direito. O ícone real será alterado para refletir o modo usado no momento:

![ateat-18](assets/ateat-18.png)

>[!NOTE]
>
>* Dependendo das características da página, alguns modos podem não estar disponíveis.
>* O acesso a alguns modos requer as permissões/privilégios apropriados.
>* O modo de desenvolvedor não está disponível em dispositivos móveis devido a restrições de espaço.
>* Existe um [atalho de teclado](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) ( `Ctrl-Shift-M`) para alternar entre o modo de **Visualização** e o atualmente selecionado (por exemplo, **Editar**, **Layout** etc.).
>

## Seleção de caminho {#path-selection}

Geralmente, durante a criação, é necessário selecionar outro recurso, como ao definir um link para outra página ou recurso ou selecionar uma imagem. Para selecionar facilmente um caminho, [campos de caminho](/help/sites-authoring/author-environment-tools.md#path-fields) O preenchimento automático da oferta e o [navegador de caminho](/help/sites-authoring/author-environment-tools.md#path-browser) permite uma seleção mais robusta.

### Campos de caminho   {#path-fields}

O exemplo usado aqui para ilustrar é o componente de imagem. Para obter mais informações sobre o uso e a edição de componentes, consulte [Componentes para criação de página](/help/sites-authoring/default-components.md).

Agora, os campos de caminho têm funcionalidade antecipada e de preenchimento automático, para facilitar a localização de um recurso.

Clicar no botão **Abrir caixa de diálogo** no campo de caminho abre a caixa de diálogo [navegador de caminho](/help/sites-authoring/author-environment-tools.md#path-browser) para permitir opções mais detalhadas de seleção.

![Abrir caixa de diálogo da Seleção](do-not-localize/screen_shot_2018-03-22at154427.png)

Como alternativa, comece a digitar no campo de caminho e o AEM oferecerá caminhos correspondentes à medida que você digita.

![ateat-19](assets/ateat-19.png)

### Navegador de caminhos {#path-browser}

O navegador de caminho é organizado da mesma maneira que a [exibição de coluna](/help/sites-authoring/basic-handling.md#column-view) do console de sites, permitindo uma seleção mais detalhada dos recursos.

![screen_shot_2018-03-22at154521](assets/screen_shot_2018-03-22at154521.png)

* Após selecionar um recurso, a variável **Selecionar** no canto superior direito da caixa de diálogo se torna ativo. Clique ou toque para confirmar a seleção ou **Cancelar** para suspender.
* Se o contexto permite a seleção de vários recursos, selecionar um recurso também ativa o botão **Selecionar**, mas, além disso, adiciona uma contagem do número de recursos selecionados no canto superior direito da janela. Clique no **X** ao lado do número para desmarcar tudo.
* Ao navegar pela árvore, sua localização é refletida na navegação estrutural na parte superior da caixa de diálogo. Essas navegações estruturais também podem ser usadas para saltar rapidamente dentro da hierarquia de recursos.
* A qualquer momento, você pode usar o campo de pesquisa na parte superior da caixa de diálogo. Clique em **X** no campo de pesquisa para limpar a pesquisa.
* Para limitar sua pesquisa, você pode revelar as opções de filtro e filtrar seus resultados com base em um determinado caminho.

  ![ateat-21](assets/ateat-21.png)

## Atalhos de teclado {#keyboard-shortcuts}

Vários [atalhos de teclado](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) estão disponíveis.
