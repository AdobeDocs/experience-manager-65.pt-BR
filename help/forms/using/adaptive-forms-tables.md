---
title: Tabelas em formulários adaptáveis
description: O componente Tabela no AEM Forms permite criar tabelas em formulários adaptáveis que são responsivos a layouts móveis e também permite usar componentes de tabela XDP.
topic-tags: author
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 1a139530-27bd-44da-8bf4-5b375e75cf32
source-git-commit: d85fc98d9a31bc4014aef4311ba0f838c7ef619a
workflow-type: tm+mt
source-wordcount: '2459'
ht-degree: 0%

---

# Tabelas em formulários adaptáveis{#tables-in-adaptive-forms}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/adaptive-forms-tables.html) |
| AEM 6.5 | Este artigo |


O uso de tabelas é uma maneira eficaz, simplificada e organizada de apresentar dados complexos. Ele ajuda os usuários a identificar informações facilmente e fornecer entradas em uma organização ordenada de linhas e colunas. A maioria dos formulários de serviços financeiros e organizações governamentais exigem grandes tabelas de dados para colocar números e realizar cálculos.

O AEM Forms fornece um componente Tabela no navegador de componentes na barra lateral que permite criar tabelas em formulários adaptáveis. Alguns dos principais recursos que ele oferece são:

* Layout responsivo em dispositivos móveis
* Linhas e colunas configuráveis
* Adição e exclusão dinâmicas de linhas no tempo de execução
* Combinar ou mesclar e dividir células
* Acessíveis por leitores de tela
* Layout personalizado usando CSS
* Compatível e mapeado com o componente de tabela XDP
* Suporte para adicionar linhas ou células usando elementos de tipo complexo XSD
* Mesclar dados de um arquivo XML

## Criar uma tabela {#create-a-table}

Para criar uma tabela, arraste e solte o componente Tabela do navegador de componentes no sidekick do formulário adaptável. Por padrão, a tabela contém duas colunas e três linhas, incluindo a linha de cabeçalho.

![Componente de tabela na barra lateral do AEM](assets/sidebar-tables.png)

### Sobre as células do cabeçalho e do corpo {#about-header-and-body-cells}

As células de cabeçalho são campos de texto. Para alterar o rótulo de um cabeçalho, clique com o botão direito do mouse na célula de cabeçalho e clique em **Editar**. Na caixa de diálogo Editar, atualize o rótulo na **Valor** e clique em **OK**.

Por padrão, as células do corpo são caixas de texto. Você pode substituir uma célula do corpo por qualquer outro componente de formulários adaptáveis disponível no sidekick, como uma caixa numérica, seletor de datas ou lista suspensa.

Por exemplo, a primeira linha do corpo na tabela a seguir inclui componentes de caixa de texto, seletor de datas e lista suspensa como células.

![tipos-célula-linha](assets/row-cell-types.png)

É possível mesclar duas ou mais células do corpo selecionando as células que deseja mesclar, clicando com o botão direito do mouse e selecionando **Mesclar**. Além disso, é possível dividir uma célula mesclada clicando com o botão direito do mouse nela e selecionando **Dividir células**.

### Adicionar, excluir, mover linhas e colunas {#add-delete-move-rows-and-columns}

Você pode adicionar e excluir uma linha ou coluna e mover uma linha para cima e para baixo em uma tabela.

Para adicionar ou excluir uma linha ou coluna ou mover uma linha, clique em qualquer célula na linha ou coluna. Um menu suspenso é exibido na parte superior da coluna e à esquerda da linha. O menu na parte superior fornece opções para adicionar ou excluir a coluna, enquanto o menu à esquerda permite adicionar, excluir ou mover a linha.

* A operação Add adiciona uma linha abaixo ou uma coluna à direita da linha ou coluna selecionada.
* A operação Delete exclui a linha ou coluna selecionada.
* A operação Mover para Cima e Mover para Baixo move a linha selecionada para cima e para baixo.

O menu suspenso da linha também fornece a operação Editar para editar propriedades, configurações e opções de estilo de linhas.

![add-delete-move-row-column](assets/add-delete-move-row-column.png)

>[!NOTE]
>
>Embora seja possível adicionar qualquer número de linhas a uma tabela, o número máximo de colunas que podem ser adicionadas é seis. Além disso, não é possível excluir a linha de cabeçalho da tabela.

### Adicionar descrição da tabela {#add-table-description}

É possível adicionar uma descrição da tabela para explicar como as informações são organizadas que os leitores de tela podem interpretar e ler. Para adicionar a descrição:

1. Selecione a tabela e selecione ![cmppr](assets/cmppr.png) para ver suas propriedades na barra lateral.
1. Especifique o resumo na guia Acessibilidade.
1. Clique em **Concluído**.

### Classificar colunas em uma tabela {#sortcolumnstable}

Você pode classificar dados com base em qualquer coluna em uma tabela no formulário adaptável. Os valores na coluna podem ser classificados em ordem crescente ou decrescente.

A classificação pode ser aplicada às colunas da tabela que contêm:

* Texto estático
* Propriedades do objeto de modelo de dados
* Combinação de texto estático e propriedades do objeto de modelo de dados

Para aplicar a classificação nas colunas da tabela, as células da coluna da tabela devem conter qualquer um dos seguintes componentes: Caixa Numérica, Escalonador Numérico, Campo de Entrada de Data, Seletor de Data, Texto ou Caixa de Texto.

Para ativar a classificação:

1. Selecione a tabela e selecione ![configure_icon](assets/configure_icon.png) (Configurar). Também é possível selecionar a tabela usando o **Conteúdo** no sidekick da Comunicação interativa.
1. Selecionar **Ativar classificação**.
1. Selecionar ![done_icon](assets/done_icon.png) para salvar as propriedades da tabela. Os ícones de classificação, setas para cima e para baixo, nos cabeçalhos das colunas, representam que a classificação foi ativada.

   ![Ativar classificação](assets/enable_sorting_new.png)

1. Alterne para a **Visualizar** para exibir a saída. A tabela é classificada automaticamente com base na primeira coluna da tabela.
1. Clique no cabeçalho da coluna para classificar os valores com base na coluna.

   Um cabeçalho de coluna com uma seta para cima representa que a tabela é classificada com base nessa coluna. Além disso, os valores na coluna são exibidos na ordem crescente.

   ![Classificação em ordem crescente](assets/sorting_ascending_new.png)

   Da mesma forma, um cabeçalho de coluna com uma seta para baixo representa que os valores na coluna são exibidos na ordem decrescente.

   Também é possível fazer alterações na tabela no **Visualizar** e clique no cabeçalho da coluna novamente para classificar os valores da coluna.

## Definir a largura da coluna de uma tabela {#set-column-width}

Execute as seguintes etapas para definir a largura da coluna para uma tabela:

1. No **[!UICONTROL Conteúdo]** , selecione a **[!UICONTROL Tabela]** e selecione o botão Configurar (![Configurar](assets/configure-icon.svg))ícone.

1. Insira a lista separada por vírgulas de valores na **[!UICONTROL Largura da coluna]** para especificar a largura proporcional de cada coluna na tabela. Por exemplo, para uma tabela que inclui 3 colunas, especificando 2,4,6 como o valor na variável **[!UICONTROL Largura da coluna]** o campo resulta na definição da largura das colunas como 2/12 para a primeira coluna, 4/12 para a segunda coluna e 6/12 para a terceira coluna. 2/12 como a largura da primeira coluna refere-se a um sexto da largura do quadro. Da mesma forma, 4/12 define a largura da segunda coluna como um terço da largura da tabela, e 6/12 define a largura da terceira coluna como metade da largura da tabela.

## Configurar estilo da tabela {#configure}

Você pode definir o estilo de uma tabela usando o modo Estilo na barra de ferramentas da página. Execute as seguintes etapas para alternar para o modo de estilo e editar o estilo da tabela

1. Na barra de ferramentas da página, antes de Visualizar, selecione ![tela suspensa](assets/canvas-drop-down.png) > **Estilo**.

1. Na barra lateral, selecione tabela e clique no botão Editar ![botão editar](assets/edit-button.png).
Você pode ver as propriedades de estilo na barra lateral.

![Propriedades de estilo de uma tabela](assets/style-table.png)

>[!NOTE]
>
>Você pode alterar o tema de cores das linhas de cabeçalho e corpo alterando os valores das variáveis LESS. Para obter mais informações, consulte [Temas no AEM Forms](/help/forms/using/themes.md).

## Adicionar ou excluir uma linha dinamicamente {#add-or-delete-a-row-dynamically}

As tabelas fornecem suporte pronto para adicionar ou excluir dinamicamente linhas no tempo de execução.

1. Selecione uma linha de tabela e selecione ![cmppr](assets/cmppr.png).
1. Na guia Configurações de repetição, especifique as contagens mínima e máxima para limitar o número de linhas na tabela.
1. Clique em **Concluído**.

No tempo de execução, você verá **+** e *-* botões para adicionar ou excluir uma linha.

![add-delete-rows-dynamically](assets/add-delete-rows-dynamically.png)

>[!NOTE]
>
>A adição ou exclusão dinâmica de uma linha não é suportada em cabeçalhos no layout móvel esquerdo das tabelas.

## Expressões em uma tabela {#expressions-in-a-table}

As tabelas em formulários adaptáveis permitem escrever expressões em JavaScript para induzir comportamentos, como mostrar ou ocultar uma tabela ou uma linha, adicionar todos os números e mostrar o total em uma célula, habilitar ou desabilitar uma célula, validar a entrada do usuário e assim por diante. Essas expressões usam APIs de modelo de script de formulários adaptáveis.

Embora tabelas e linhas suportem apenas expressões de visibilidade para controlar sua visibilidade com base no valor retornado por uma expressão, as células suportam as seguintes expressões:

* **Script de inicialização:** para executar uma ação na inicialização de um campo.
* **Script de confirmação de valor:** para alterar os componentes de um formulário depois que o valor de um campo é alterado.

>[!NOTE]
>
>Se o script de alteração/saída do XFA também for aplicado ao mesmo campo, o script de alteração/saída do XFA será executado antes do script de confirmação de valor.

* **Calcular expressões**: para calcular automaticamente o valor de um campo.
* **Expressões de validação**: para validar um campo.
* **Acessar expressões**: para ativar/desativar um campo.
* **Expressão de visibilidade**: para controlar a visibilidade de um campo e painel.

A expressão de visibilidade de uma tabela ou linha pode ser definida na guia de propriedades Painel da caixa de diálogo Editar componente correspondente. As expressões de uma célula podem ser definidas na guia Script da caixa de diálogo Editar componente.

Para obter a lista completa de classes de formulários adaptáveis, eventos, objetos e APIs públicas, consulte [Referência da API da biblioteca JavaScript para formulários adaptáveis](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

## Layouts móveis {#mobile-layouts}

As tabelas em formulários adaptáveis fornecem dispositivos móveis de experiência incomparáveis devido a seus layouts fluidos e responsivos. O AEM Forms oferece dois tipos de layouts móveis para tabelas: Cabeçalhos à esquerda e Colunas flexíveis.

É possível configurar um layout móvel para uma tabela na guia Estilo da caixa de diálogo Editar componente para uma tabela.

### Cabeçalhos à esquerda {#headers-on-left}

No layout Cabeçalhos à esquerda, o cabeçalho da tabela é transposto à esquerda com apenas uma célula que aparece em relação a um cabeçalho. Cada linha neste layout aparece como uma seção distinta. As imagens a seguir comparam uma tabela em um desktop com aquela em um dispositivo móvel.

![exibição da área de trabalho](assets/desktopview_new.png)

Exibição de desktop de uma tabela com cabeçalho no layout esquerdo

![Cabeçalhos à esquerda](assets/headersontheleft_new.png)

Exibição móvel de uma tabela com Cabeçalho no layout esquerdo

### Layout de colunas flexíveis {#collapsible-columns-layout}

No layout de coluna Recolhível, as colunas na tabela são recolhidas para mostrar uma ou duas colunas, dependendo do tamanho do dispositivo, enquanto as outras colunas são recolhidas. Você pode clicar no ícone recolher/expandir para exibir outras colunas na tabela.

>[!NOTE]
>
>Embora o Layout de coluna flexível seja otimizado para dispositivos móveis, ele também funcionará no desktop, se a largura disponível não for suficiente para mostrar todas as colunas em uma tabela.

As imagens a seguir comparam como uma tabela é exibida em um dispositivo com colunas recolhidas e expandidas.

![coluna recolhida](assets/collapsed-column.png)

Colunas recolhidas de uma tabela com apenas duas colunas exibidas em um dispositivo móvel

![coluna_recolhível](assets/collapsible_column.png)

Coluna expandida de uma tabela em um dispositivo móvel

## Mesclar dados em uma tabela {#merge-data-in-a-table}

Tabelas em formulários adaptáveis permitem preencher a tabela no tempo de execução usando dados de um arquivo XML. O arquivo XML de dados pode residir no sistema de arquivos local da máquina em que o servidor do AEM Forms está sendo executado ou no repositório CRX.

Vamos ver um exemplo da tabela de resumo de transações bancárias a seguir que queremos preencher com dados de um arquivo XML.

![data-merge-table](assets/data-merge-table.png)

Neste exemplo, a propriedade Element name para:

* a linha é **Linha1**
* a célula do corpo em Data da transação é **tableItem1**
* a célula do corpo em Descrição é **tableItem2**
* a célula do corpo em Transaction type é **type**
* a célula do corpo em Valor em USD é **tableItem3**

O arquivo XML que contém dados no seguinte formato:

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
 <typeSelect>0</typeSelect>
 <Row1>
      <tableItem1>2015-01-08</tableItem1>
      <tableItem2>Purchase laptop</tableItem2>
      <type>0</type>
      <tableItem3>12000</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-05</tableItem1>
      <tableItem2>Transport expense</tableItem2>
      <type>0</type>
      <tableItem3>120</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2014-01-08</tableItem1>
      <tableItem2>Laser printer</tableItem2>
      <type>0</type>
      <tableItem3>500</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2014-12-08</tableItem1>
      <tableItem2>Credit card payment</tableItem2>
      <type>0</type>
      <tableItem3>300</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-06</tableItem1>
      <tableItem2>Interest earnings</tableItem2>
      <type>1</type>
      <tableItem3>12000</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-05</tableItem1>
      <tableItem2>Payment from a client</tableItem2>
      <type>1</type>
      <tableItem3>500</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-08</tableItem1>
      <tableItem2>Food expense</tableItem2>
      <type>0</type>
      <tableItem3>120</tableItem3>
 </Row1>
 </data>
  </afUnboundData>
  <afBoundData>
    <data/>
  </afBoundData>
  <afBoundData/>
</afData>
```

No exemplo XML, os dados de uma linha são definidos pela variável `<Row1>` tags, que é o nome do elemento para a linha na tabela. No prazo de `<Row1>` tag, os dados de cada célula são definidos na tag para seu nome de elemento, como `<tableItem1>`, `<tableItem2>`, `<tableItem3>`, e `<type>`.

Para mesclar esses dados com a tabela no tempo de execução, precisamos apontar o formulário adaptável que contém a tabela para o local XML absoluto com o wcmmode desativado. Por exemplo, se o formulário adaptável estiver em *https://localhost:4502/myForms/bankTransaction.html* e o arquivo XML de dados é salvo em *C:/myTransactions/bankSummary.xml*, você pode visualizar a tabela com os dados no seguinte URL:

*https://localhost:4502/myForms/bankTransaction.html?dataRef=file:/// C:/myTransactions/bankSummary.xml&amp;wcmmode=disabled*

![dados-mesclados-tabela](assets/data-merged-table.png)

## Usar componentes XDP e tipos complexos de XSD {#use-xdp-components-and-xsd-complex-types}

Se você criou um formulário adaptável com base em um modelo de formulário XFA, os elementos XFA estarão disponíveis na guia Modelo de dados do Localizador de conteúdo do AEM. Você pode arrastar e soltar esses elementos XFA, incluindo tabelas, no formulário adaptável.

O elemento da tabela XFA é mapeado para o componente Tabela e funciona pronto para uso em formulários adaptáveis. Todas as propriedades e funcionalidades da tabela XDP são preservadas quando movidas para o formulário adaptável e você pode executar qualquer operação nela, como faz com a tabela de formulário adaptável nativa. Por exemplo, se uma linha em uma tabela XDP for marcada como repetível, ela também será repetida quando solta em formulários adaptáveis.

Além disso, você pode arrastar e soltar o subformulário XDP para adicionar uma nova linha na tabela. No entanto, observe que soltar um subformulário aninhado não funciona.

>[!NOTE]
>
>Uma tabela XDP sem uma linha de cabeçalho não será mapeada para o componente de tabela de formulário adaptável. Em vez disso, ele será mapeado para o componente Painel de formulário adaptável com layout fluido. Além disso, ao adicionar uma tabela aninhada de um XDP a um formulário adaptável, a tabela externa é convertida em um painel enquanto mantém a tabela interna.

Além disso, você pode arrastar e soltar um grupo de elementos de tipo complexo XSD para criar uma linha de tabela. Uma nova linha é criada logo abaixo da linha em que você soltou os elementos. As células criadas usando os elementos de tipo complexo XSD mantêm uma referência de ligação ao XSD. Você também pode substituir uma célula do corpo por um elemento de tipo complexo XSD soltando o elemento na célula.

>[!NOTE]
>
>O número de elementos em um componente de tabela XDP, um subformulário ou um tipo complexo XSD não pode exceder o número de células em uma linha. Por exemplo, você não pode soltar quatro elementos em uma linha que tenha apenas três células. Isso resultará em um erro.
>
>Se o número de elementos for menor que o número de células em uma linha, a nova linha primeiro adicionará células com base nos elementos e, em seguida, as células padrão serão adicionadas para preencher as células restantes na linha. Por exemplo, se você soltar um grupo de três elementos em uma linha que tem quatro células, as primeiras três células serão baseadas nos elementos soltos e a célula restante será a célula padrão da tabela.

## Principais considerações {#key-considerations}

* Se você mover linhas para cima e para baixo durante a criação de uma tabela baseada em XSD, alguma perda de dados das linhas da tabela será vista no XML de dados gerado no envio do formulário.
* Cada célula do corpo em uma tabela padrão tem um nome de elemento predefinido associado a ela. Se adicionar outra tabela no formulário adaptável, as células de corpo padrão na nova tabela terão o mesmo nome de elemento da primeira tabela. Nesse cenário, os dados gerados no envio do formulário incluirão dados nas células do corpo padrão de apenas uma das tabelas. Portanto, renomeie os nomes dos elementos para as células do corpo padrão para mantê-los exclusivos nas tabelas e evitar perda de dados.

  Observe que isso é aplicável somente às células do corpo padrão. Se você adicionar mais linhas ou colunas a uma tabela, gerará automaticamente nomes de elementos exclusivos para células de corpo fora do padrão.
