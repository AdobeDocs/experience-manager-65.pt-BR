---
title: Condição embutida e repetição em Comunicações interativas e letras
seo-title: Condição embutida e repetição em Comunicações interativas e letras
description: Usando condições embutidas e repetidas em Comunicações interativas e letras, você pode criar comunicações altamente contextuais e bem estruturadas.
seo-description: Usando condições embutidas e repetidas em Comunicações interativas e letras, você pode criar comunicações altamente contextuais e bem estruturadas.
uuid: 32b48a8b-431d-4f9c-9f51-8e7e9ac624a0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: interactive-communications, correspondence-management
discoiquuid: bbaba39b-e15a-4143-b6fc-7789fa2917b4
docset: aem65
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 0%

---


# Condição embutida e repetição em Comunicações interativas e letras{#inline-condition-and-repeat-in-interactive-communications-and-letters}

## Condições em linha {#inline-conditions}

A AEM Forms permite usar condições embutidas em módulos de texto para automatizar a renderização de texto que depende do contexto ou dos dados associados ao modelo de dados de formulário (em Comunicação interativa) ou ao dicionário de dados (em letras). A condição embutida exibe conteúdo específico com base na avaliação da condição sendo true ou false.

As condições executam cálculos nos valores de dados fornecidos pelo modelo de dados do formulário/Dicionário de dados ou pelos usuários finais. Usando condições em linha, você pode economizar tempo e reduzir erros humanos, ao mesmo tempo em que cria comunicações/letras interativas altamente contextuais e personalizadas.

Para obter mais informações, consulte:

* [Criar uma comunicação interativa](../../forms/using/create-interactive-communication.md)
* [Visão geral do gerenciamento de correspondência](/help/forms/using/cm-overview.md)
* [Texto em Comunicações Interativas](../../forms/using/texts-interactive-communications.md)

### Exemplo: Uso de regras para condicionar o texto em linha no Interative Communication {#example-using-rules-to-conditionalize-inline-text-in-interactive-communication}

Para condicionalizar uma frase, parágrafo ou string de texto em uma Comunicação interativa, é possível criar uma regra no fragmento de documento de texto apropriado. O exemplo a seguir usa uma regra para exibir um número gratuito somente para os recipient dos EUA da Comunicação interativa.

Para obter mais informações, consulte Criar regra em texto em [Textos em Comunicações](../../forms/using/texts-interactive-communications.md)Interativas.

Depois que você incluir o fragmento de texto em uma Comunicação interativa e o Agente usar a interface do usuário do agente para preparar uma Comunicação interativa, os dados (modelo de dados de formulário) dos recipient serão avaliados e o texto será mostrado somente para os recipient nos EUA.

### Exemplo: Uso da condição em linha em uma carta para renderizar o endereço apropriado  {#example-using-inline-condition-in-a-letter-to-render-the-appropriate-address}

É possível inserir uma condição em linha em uma carta inserindo a condição em linha no módulo de texto apropriado. O exemplo a seguir usa duas condições para avaliar e exibir o endereço apropriado, Senhor ou Senhora, em uma carta com base no elemento DD Gênero. Usando etapas semelhantes, é possível criar outras condições.

>[!NOTE]
>
>Se os ativos existentes incluírem expressões de condição antiga/repetida (pré 6.2 SP1 CFP 4), os ativos exibirão a sintaxe antiga de condição e serão repetidos. No entanto, a condição antiga/repetição funciona. As expressões novas e antigas de condição/repetição são compatíveis entre si para criar uma combinação aninhada de expressões antigas e novas de condição/repetição.

1. No módulo de texto relevante, selecione a parte do texto que deseja condicionar e toque em **Condição**.

   ![1_select](assets/1_selecttext.png)

   A caixa de diálogo Condição é exibida com uma condição vazia.

   ![Caixa de diálogo 2_condicional](assets/2_conditiondialog.png)

   >[!NOTE]
   >
   >Não é possível salvar expressões condicionais vazias ou inválidas. Tem de haver uma expressão condicional válida dentro `${}` para salvar a expressão.

1. Faça o seguinte para criar uma condição para avaliar se o texto selecionado/condicionado aparece na carta e, em seguida, toque na marca de seleção para salvar a expressão:

   Toque no duplo em um elemento DD para inseri-lo na condição. Insira o operador apropriado e construa a seguinte condição na caixa de diálogo.

   ```javascript
   ${DD_creditcard_Gender=="Male"}
   ```

   Para obter mais informações sobre como criar a expressão, consulte **Criar expressões e funções remotas com o expressão** Builder no [Expressão Builder](../../forms/using/expression-builder.md). O valor especificado na expressão deve ser suportado para o elemento no dicionário de dados. Para obter mais informações, consulte Dicionário [de](../../forms/using/data-dictionary.md)dados.

   Depois que a condição é inserida, você pode passar o mouse sobre a alça à esquerda da condição para visualização a condição. Você pode tocar na alça para visualização no menu pop-up da condição, que permite editar ou remover a condição.

   ![3_hoveridentificador](assets/3_hoverhandle.png) ![4_editcondiciontionremoveconditionpopup](assets/4_editconditionremoveconditionpopup.png)

1. Insira uma condição semelhante selecionando o texto `Ma'am`.

   ```javascript
   ${DD_creditcard_Gender == "Female"}
   ```

1. Pré-visualização a letra relevante e observe que o texto é renderizado de acordo com a condição em linha. Você pode inserir o valor do elemento DD Gênero usando:

   * Um arquivo de dados XML de amostra criado com base no dicionário de dados relevante ao visualizar a carta com dados de amostra.
   * Um arquivo de dados XML anexado ao dicionário de dados relevante.

   Para obter mais informações, consulte Dicionário [de](../../forms/using/data-dictionary.md)dados.

   ![5_letteroutput](assets/5_letteroutput.png)

## Repetir {#repeat}

Você pode ter informações dinâmicas em sua Comunicação/carta interativa, como transações em um demonstrativo de cartão de crédito, cuja instância ou ocorrência pode continuar alterando com cada carta gerada. Usando repetir, é possível formatar e estruturar essas informações dinâmicas no fragmento do documento de texto.

Além disso, você pode especificar a regra/condição dentro da construção repetida para condicionar as informações/entradas renderizadas na Comunicação interativa/letra.

### Exemplo: Uso de repetição em uma Comunicação interativa para formatar, estruturar e exibir uma lista de transações de cartão de crédito {#example-using-repeat-in-an-interactive-communication-to-format-structure-and-display-a-list-of-credit-card-transactions}

O exemplo a seguir fornece as etapas para usar repetir para estruturar e renderizar as transações de cartão de crédito em uma Comunicação Interativa.

1. Em um fragmento de documento de texto baseado em modelo de dados de formulário, insira os objetos relevantes do modelo de dados de formulário (e o texto incorporado necessário para os rótulos, como neste exemplo):

   ![1_elementstext](assets/1_elementstext.png)

   >[!NOTE]
   >
   >O conteúdo repetível deve incluir pelo menos uma propriedade do tipo Coleção.

1. Selecione o conteúdo no qual aplicar repetição.

   ![2_select](assets/2_selection.png)

1. Toque em Repetir.

   A caixa de diálogo Repetir é exibida.

   ![Caixa de diálogo 3_repetitivo](assets/3_repeatdialog.png)

1. Selecione Quebra de linha como separador e, se necessário, toque em Adicionar condição para criar uma regra. Também é possível usar o texto como separador e especificar os caracteres de texto a serem usados como separador.

   A caixa de diálogo Criar regra é exibida.

1. Crie uma regra para exibir transações datadas de 28 de fevereiro de 2018 para incluir as transações somente para o mês de março na Comunicação interativa.

   >[!NOTE]
   >
   >Este exemplo supõe que o Agente criará a declaração no final de março de 2018. Caso contrário, você poderá criar outra regra para incluir transações antes de 2018-04-01 para excluir transações após março de 2018.

   ![4_createrule](assets/4_createrule.png)

1. Salve a condição/regra e salve a repetição. A repetição condicional é aplicada ao conteúdo selecionado.

   ![5_onmouseovercondicionalidade rule](assets/5_onmouseoverconditionrule.png)

   Ao passar o mouse, o fragmento do documento de texto exibe a Condição e o separador usado na repetição aplicada ao conteúdo.

1. Salve o fragmento do documento de texto e pré-visualização a Comunicação Interativa relevante. Dependendo dos dados no modelo de dados de formulário, a repetição aplicada nos elementos renderiza os detalhes da transação da seguinte forma na pré-visualização:

   ![screen_shot_2018-03-09at155516copy](assets/screen_shot_2018-03-09at155516copy.png)

### Exemplo: Usar a repetição em uma carta para formatar, estruturar e exibir uma lista de transações de cartão de crédito {#example-using-repeat-in-a-letter-to-format-structure-and-display-a-list-of-credit-card-transactions}

O exemplo a seguir fornece as etapas para usar repetir para estruturar e renderizar as transações de cartão de crédito em uma carta. Usando etapas semelhantes, você pode usar repetir em um cenário diferente.

1. Abra (ao editar ou criar) um módulo de texto que tenha elementos DD que renderizam dados repetidos/dinâmicos e incorporem o texto necessário ao redor dos elementos DD. Por exemplo, um módulo de texto tem os seguintes elementos DD para criar uma declaração de transações em um cartão de crédito:

   ```javascript
   {^DD_creditcard_TransactionDate^} {^DD_creditcard_TransactionAmount^}
   {^DD_creditcard_TransactionType^}
   ```

   Estes elementos de DD renderizam uma lista das transações efetuadas no cartão de crédito com as seguintes informações:

   Data da transação, Quantia da transação e Tipo de transação (Débito ou Crédito)

1. Incorpore o texto aos elementos DD para tornar a declaração mais legível, como a seguir:

   ![1_repetir](assets/1_repeat.png)

   ```javascript
   Date: {^DD_creditcard_TransactionDate^} Amount (USD): {^DD_creditcard_TransactionAmount^} Transaction Type: {^DD_creditcard_TransactionType^}
   ```

   No entanto, o trabalho de renderização de uma declaração bem formatada ainda não foi feito. Se você renderizar uma carta com base no trabalho feito até o momento, ela será exibida como a seguir:

   ![1_1renderização sem repetição](assets/1_1renderwithoutrepeat.png)

   Para repetir o texto estático junto com os elementos DD, é necessário aplicar a repetição conforme explicado nas etapas seguintes.

1. Selecione o texto estático e os elementos de DD que deseja repetir, conforme mostrado abaixo:

   ![2_again_select](assets/2_repeat_selecttext.png)

1. Toque em **Repetir**. A caixa de diálogo Repetir é exibida com uma condição em linha vazia.

   ![3_again_dialog](assets/3_repeat_dialog.png)

1. Se necessário, insira uma condição para renderizar seletivamente as transações, como para renderizar quantias de transação maiores que 50 centavos:

   ```javascript
   ${DD_creditcard_TransactionAmount > 0.5}
   ```

   Caso contrário, se você não precisar renderizar as informações (aqui as transações) seletivamente, mantenha a condição vazia, excluindo o seguinte na caixa de diálogo: `${}`. Salvar uma expressão repetida é ativado quando a janela de expressão repetida está vazia (sem ${} quando nenhuma repetição é necessária) ou quando contém uma condição válida para repetição.

1. Selecione um separador para formatar o texto dinâmico e toque na marca de seleção para salvar:

   * **Quebra** de linha: Insere quebra de linha após cada entrada de transação na carta de saída.
   * **Texto**: Insere o caractere de texto especificado após cada entrada de transação na letra de saída.

   Depois que a condição é inserida, o texto com repetição é realçado em vermelho e uma alça é exibida à esquerda. Você pode passar o mouse sobre a alça à esquerda da repetição para visualização da construção repetida.

   ![4_again_hoverdetail](assets/4_repeat_hoverdetail.png)

   Você pode tocar na alça para visualização no menu pop-up da repetição, o que permite que você edite ou remova a construção repetida.

   ![5_repetieditremove](assets/5_repeateditremove.png)

1. Pré-visualização a carta relevante e observe que o texto é renderizado de acordo com a repetição. Você pode inserir o valor dos elementos DD usando:

   * Um arquivo de dados XML de amostra criado com base no dicionário de dados relevante ao visualizar a carta com dados de amostra.
   * Um arquivo de dados XML anexado ao dicionário de dados relevante.

   Para obter mais informações, consulte Dicionário [de](https://helpx.adobe.com/aem-forms/6-2/data-dictionary.html)dados.

   ![Visualização 6_repetipupupupupuputar](assets/6_repeatoutputpreview.png)

   O texto estático se repete com os detalhes da transação. A repetição do texto estático é facilitada pela repetição aplicada ao texto neste procedimento. A condição, ${DD_creditcard_TransactionAmount > 0.5}, garante que as transações abaixo de USD.5 não sejam renderizadas na carta.

   >[!NOTE]
   >
   >Você pode inserir a condição e repetir somente ao criar ou editar o módulo de texto relevante. Ao visualizar a carta, embora seja possível fazer edições no módulo de texto, não é possível inserir a condição ou repetir.

## Uso de condição em linha e repetição - alguns casos de uso  {#using-inline-condition-and-repeat-some-use-cases}

### Repetir dentro da condição {#repeat-within-condition}

Pode ser necessário repetir o uso em uma condição. O Gerenciamento de correspondência permite usar a repetição em uma construção de condição em linha.

Por exemplo, a seguir é repetida (formatada em vermelho) em uma condição (formatada em verde).

Enquanto a repetição renderiza as transações de cartão de crédito, a condição ${DD_creditcard_nooftransactions > 0} garante que a construção repetida seja renderizada somente se houver pelo menos uma transação.

![repetiwitincondition](assets/repeatwitincondition.png)

Da mesma forma, de acordo com seu requisito, você pode criar:

* Uma ou mais condições em uma condição
* Uma ou mais condições em uma repetição
* Uma combinação de condições e repetição dentro de uma condição ou repetição

### Condição em linha vazia {#empty-inline-condition}

Talvez seja necessário inserir condições em linha vazias e incorporar texto e elementos DD posteriormente. O Gerenciamento de correspondência permite fazer isso.

![emptycondition](assets/emptycondition.png)

No entanto, é recomendável que, se possível, você insira os elementos de texto e DD primeiro no módulo de texto com a formatação pretendida, como marcadores, e aplique uma condição em linha depois disso.
