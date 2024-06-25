---
title: Estrutura de aparência para formulários adaptáveis e HTML5
description: O Mobile Forms renderiza Modelos de formulário como formulários HTML5. Esses formulários usam os arquivos jQuery, Backbone.js e Underscore.js para a aparência e para ativar os scripts.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: 3458471a-9815-463e-8044-68631073863c
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Mobile Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 2%

---

# Estrutura de aparência para formulários adaptáveis e HTML5 {#appearance-framework-for-adaptive-and-html-forms}

Uso do Forms (formulários adaptáveis e formulários HTML5) [jQuery](https://jquery.com/), [Backbone.js](https://backbonejs.org/) e [Underscore.js](https://underscorejs.org/) bibliotecas para aparência e script. Os formulários também usam o [Interface do jQuery](https://jqueryui.com/) **Widgets** para todos os elementos interativos (como campos e botões) no formulário. Essa arquitetura permite que o desenvolvedor de formulários use um conjunto avançado de widgets e plug-ins jQuery disponíveis no Forms. Você também pode implementar a lógica específica do formulário enquanto captura dados de usuários como restrições leadDigits/trailDigits ou implementa cláusulas de figura. Os desenvolvedores de formulários podem criar e usar aparências personalizadas para melhorar a experiência de captura de dados e torná-la mais fácil de usar.

Este artigo é para desenvolvedores com conhecimento suficiente de widgets jQuery e jQuery. Ele fornece informações sobre a estrutura de aparência e permite que os desenvolvedores criem uma aparência alternativa para um campo de formulário.

A estrutura de aparência depende de várias opções, eventos (acionadores) e funções para capturar as interações do usuário com o formulário e responde às alterações do modelo para informar o usuário final. Além disso:

* A estrutura fornece um conjunto de opções para a aparência de um campo. Essas opções são pares de valores chave e divididas em duas categorias: opções comuns e opções específicas do tipo de campo.
* A aparência, como parte do contrato, aciona um conjunto de eventos, como entrar e sair.
* A aparência é necessária para implementar um conjunto de funções. Algumas das funções são comuns, enquanto outras são específicas para funções de tipo de campo.

## Opções comuns {#common-options}

Veja a seguir o conjunto de opções globais. Essas opções estão disponíveis para cada campo.

<table>
 <tbody>
  <tr>
   <th>Propriedade </th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>name</td>
   <td>Um identificador usado para especificar este objeto ou evento em expressões de script. Por exemplo, essa propriedade especifica o nome do aplicativo host.</td>
  </tr>
  <tr>
   <td>valor</td>
   <td>Valor real do campo. </td>
  </tr>
  <tr>
   <td>displayValue</td>
   <td>Esse valor do campo é exibido. </td>
  </tr>
  <tr>
   <td>screenReaderText</td>
   <td>Os Reader de tela usam esse valor para narrar informações sobre o campo. O formulário fornece o valor e você pode substituir o valor.<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>A posição do campo na sequência de guias do formulário. Substitua tabIndex somente se desejar alterar a ordem de tabulação padrão do formulário.</td>
  </tr>
  <tr>
   <td>função</td>
   <td>Função do elemento, por exemplo, cabeçalho ou tabela.</td>
  </tr>
  <tr>
   <td>altura</td>
   <td>A altura do widget. Ele é especificado em pixels. </td>
  </tr>
  <tr>
   <td>largura</td>
   <td>A largura do widget. Ele é especificado em pixels.</td>
  </tr>
  <tr>
   <td>acesso</td>
   <td>Controles usados para acessar o conteúdo de um objeto de contêiner, como um subformulário.</td>
  </tr>
  <tr>
   <td>paraStyles</td>
   <td>A propriedade para de um elemento XFA para o widget.</td>
  </tr>
  <tr>
   <td>dir</td>
   <td>A direção do texto. Os valores possíveis são ltr (esquerda para a direita) e rtl (direita para a esquerda).</td>
  </tr>
 </tbody>
</table>

Além dessas opções, a estrutura fornece algumas outras opções que variam dependendo do tipo de campo. Os detalhes das opções específicas de campo estão listados abaixo.

### Interação com o framework de formulários {#interaction-with-forms-framework}

Para interagir com a estrutura de formulários, um widget aciona alguns eventos para permitir que o script de formulário funcione. Se o widget não lançar esses eventos, alguns dos scripts escritos no formulário para esse campo não funcionarão.

#### Eventos acionados pelo widget {#events-triggered-by-widget}

<table>
 <tbody>
  <tr>
   <th>Evento </th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENT</td>
   <td>Esse evento é acionado sempre que o campo está em foco. Ele permite que o script "enter" seja executado no campo. A sintaxe para acionar o evento é<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td>
   <td>Esse evento é acionado sempre que o usuário deixa o campo. Ele permite que o mecanismo defina o valor do campo e execute seu script "exit". A sintaxe para acionar o evento é<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td>
   <td>Esse evento é acionado para permitir que o mecanismo execute o script "change" gravado no campo. A sintaxe para acionar o evento é<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td>
   <td>Esse evento é acionado sempre que o campo é clicado. ele permite que o mecanismo execute o script "click" gravado no campo. A sintaxe para acionar o evento é<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td>
  </tr>
 </tbody>
</table>

#### APIs implementadas pelo widget {#apis-implemented-by-widget}

A estrutura de aparência chama algumas funções do widget que são implementadas nos widgets personalizados. O dispositivo deve implementar as seguintes funções:

<table>
 <tbody>
  <tr>
   <th>Função</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>focus: function()</td>
   <td>Coloca o foco no campo.</td>
  </tr>
  <tr>
   <td>clique em: function()</td>
   <td>Coloca o foco no campo e chama XFA_CLICK_EVENT.</td>
  </tr>
  <tr>
   <td><p>markError:function(errorMessage, errorType)<br /> <br /> <em>errorMessage: string </em>representando o erro<br /> <em>errorType: string ("aviso"/"erro")</em></p> <p><strong>Nota</strong>: Aplicável somente a formulários HTML5.</p> </td>
   <td>Envia uma mensagem de erro e um tipo de erro para o widget. O widget exibe o erro.</td>
  </tr>
  <tr>
   <td><p>clearError: function()</p> <p><strong>Nota</strong>: Aplicável somente a formulários HTML5.</p> </td>
   <td>Chamado se os erros no campo forem corrigidos. O widget oculta o erro.</td>
  </tr>
 </tbody>
</table>

## Opções específicas para o tipo de campo {#options-specific-to-type-of-field}

Todos os widgets personalizados devem estar em conformidade com as especificações acima. Para usar os recursos de campos diferentes, o widget deve estar em conformidade com as diretrizes desse campo específico.

### TextEdit: Campo de texto {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>Opção</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>multilinha</td>
   <td>Verdadeiro se o campo suportar a inserção de um caractere de nova linha, caso contrário, falso.</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>Número máximo de caracteres que podem ser inseridos no campo.</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>Nota</strong>: Aplicável somente a formulários HTML5</p> </td>
   <td>Especifica o comportamento do campo de texto quando a largura do texto excede a largura do widget.</td>
  </tr>
 </tbody>
</table>

### ChoiceList: DropDownList, ListBox {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>Opção</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>value<br /> </td>
   <td>Matriz de valores selecionados.<br /> </td>
  </tr>
  <tr>
   <td>itens<br /> </td>
   <td>Matriz de objetos a serem exibidos como opções. Cada objeto contém duas propriedades -<br /> save: valor a ser salvo, display: valor a ser exibido.<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>editável</p> <p><strong>Nota</strong>: Aplicável somente a formulários HTML5.<br /> </p> </td>
   <td>Se o valor for true, a entrada de texto personalizado será habilitada no widget.<br /> </td>
  </tr>
  <tr>
   <td>displayValue<br /> </td>
   <td>Matriz de valores a ser exibida.<br /> </td>
  </tr>
  <tr>
   <td>multiselect<br /> </td>
   <td>True se várias seleções forem permitidas, caso contrário, false.<br /> </td>
  </tr>
 </tbody>
</table>

#### API {#api}

<table>
 <tbody>
  <tr>
   <th>Função</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td><p>addItem:<em> function(itemValues)<br /> itemValues: objeto que contém a exibição e o valor salvo <br /> {sDisplayVal: &lt;displayvalue&gt;, sSaveVal: &lt;save value=""&gt;}</em></p> </td>
   <td>Adiciona um item à lista.</td>
  </tr>
  <tr>
   <td>deleteItem<em>: função(nIndex)<br /> nIndex: índice do item a ser removido da lista<br /> </em><br /> <br /> </td>
   <td>Exclui uma opção da lista.</td>
  </tr>
  <tr>
   <td>clearItems:<code> function()</code></td>
   <td>Limpa todas as opções da lista.</td>
  </tr>
 </tbody>
</table>

### NumericEdit: NumericField, DecimalField {#numericedit-numericfield-decimalfield}

| Opções | Descrição |
|---|---|
| dataType | Sequência de caracteres que representa o tipo de dados do campo (inteiro/decimal). |
| leadDigits | Máximo de dígitos à esquerda permitido no número decimal. |
| fracDigits | Máximo de dígitos fracionários permitidos no número decimal. |
| zero | Representação de cadeia de caracteres de zero na localidade do campo. |
| decimal | Representação de cadeia de caracteres do decimal no local do campo. |

### CheckButton: RadioButton, CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>Opções</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>valores</td>
   <td><p>Matriz de valores (ligada/desligada/neutra).</p> <p>É uma matriz de valores para os diferentes estados do checkButton. values[0] é o valor quando o estado é ON, values[1] é o valor quando o estado é OFF,<br /> values[2] é o valor quando o estado é NEUTRAL. O comprimento da matriz de valores é igual ao valor da opção de estado.<br /> </p> </td>
  </tr>
  <tr>
   <td>estados</td>
   <td><p>Número de estados permitidos. </p> <p>Dois para formulários adaptáveis (Ligado, Desligado) e três para formulários HTML5 (Ligado, Desligado, Neutro).</p> </td>
  </tr>
  <tr>
   <td>estado</td>
   <td><p>Estado atual do elemento.</p> <p>Dois para formulários adaptáveis (Ligado, Desligado) e três para formulários HTML5 (Ligado, Desligado, Neutro).</p> </td>
  </tr>
 </tbody>
</table>

### DateTimeEdit: (DateField) {#datetimeedit-datefield}

| Opção | Descrição |
|---|---|
| dias | Nome localizado de dias para esse campo. |
| meses | Nomes de meses localizados para esse campo. |
| zero | O texto localizado para o número 0. |
| clearText | O texto localizado para o botão Limpar. |
