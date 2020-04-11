---
title: Estrutura de aparência para formulários adaptáveis e HTML5
seo-title: Estrutura de aparência para formulários adaptáveis e HTML5
description: Formulários móveis renderizam Modelos de formulário como formulários HTML5. Esses formulários usam arquivos jQuery, Backbone.js e Underscore.js para a aparência e para ativar o script.
seo-description: Formulários móveis renderizam Modelos de formulário como formulários HTML5. Esses formulários usam arquivos jQuery, Backbone.js e Underscore.js para a aparência e para ativar o script.
uuid: 183b8d71-44fc-47bf-8cb2-1cf920ffd23a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 3c2a44a7-24e7-49ee-bf18-eab0e44efa42
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Estrutura de aparência para formulários adaptáveis e HTML5 {#appearance-framework-for-adaptive-and-html-forms}

Os formulários (formulários adaptáveis e HTML5) usam as bibliotecas [jQuery](https://jquery.com/), [Backbone.js](https://backbonejs.org/) e [Underscore.js](https://underscorejs.org/) para obter aparência e scripts. Os formulários também usam a arquitetura [jQuery UI](https://jqueryui.com/) **Widgets** para todos os elementos interativos (como campos e botões) no formulário. Essa arquitetura permite que o desenvolvedor de formulários use um conjunto avançado de widgets e plug-ins disponíveis do jQuery no Forms. Você também pode implementar uma lógica específica do formulário enquanto captura dados de usuários como restrições leadDigits/trailDigits ou implementar cláusulas de imagem. Os desenvolvedores de formulários podem criar e usar percepções personalizadas para melhorar a experiência de captura de dados e torná-la mais fácil de usar.

Este artigo destina-se a desenvolvedores com conhecimento suficiente dos widgets jQuery e jQuery. Ele fornece informações sobre a estrutura de aparência e permite que os desenvolvedores criem uma aparência alternativa para um campo de formulário.

A estrutura de aparência depende de várias opções, eventos (acionadores) e funções para capturar as interações do usuário com o formulário e responde às alterações no modelo para informar o usuário final. Além disso:

* A estrutura fornece um conjunto de opções para a aparência de um campo. Essas opções são pares de valores chave e divididas em duas categorias: opções comuns e opções específicas de tipo de campo.
* A aparência, como parte do contrato, aciona um conjunto de eventos como entrada e saída.
* A aparência é necessária para implementar um conjunto de funções. Algumas funções são comuns, enquanto outras são específicas para funções de tipo de campo.

## Opções comuns {#common-options}

A seguir estão as opções globais definidas. Essas opções estão disponíveis para cada campo.

<table>
 <tbody>
  <tr>
   <th>Propriedade </th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>name</td>
   <td>Um identificador usado para especificar esse objeto ou evento nas expressões de script. Por exemplo, essa propriedade especifica o nome do aplicativo host.</td>
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
   <td>Leitores de tela usam esse valor para registrar informações sobre o campo. O formulário fornece o valor e você pode substituí-lo.<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>A posição do campo na sequência de tabulação do formulário. Substitua tabIndex somente se desejar alterar a ordem de tabulação padrão do formulário.</td>
  </tr>
  <tr>
   <td>role</td>
   <td>A função do elemento, por exemplo, Cabeçalho ou Tabela.</td>
  </tr>
  <tr>
   <td>altura</td>
   <td>A altura do widget. É especificado em pixels. </td>
  </tr>
  <tr>
   <td>largura</td>
   <td>A largura do widget. É especificado em pixels.</td>
  </tr>
  <tr>
   <td>access</td>
   <td>Controles usados para acessar o conteúdo de um objeto de container, como um subformulário.</td>
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

Além dessas opções, a estrutura fornece outras opções que variam dependendo do tipo de campo. Os detalhes das opções específicas dos campos estão listados abaixo.

### Interação com a estrutura de formulários {#interaction-with-forms-framework}

Para interagir com a estrutura de formulários, um widget aciona alguns eventos para permitir que o script de formulário funcione. Se o widget não exibir esses eventos, alguns dos scripts gravados no formulário desse campo não funcionarão.

#### Eventos acionados pelo widget {#events-triggered-by-widget}

<table>
 <tbody>
  <tr>
   <th>Evento </th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENTO</td>
   <td>Esse evento é acionado sempre que o campo está em foco. Isso permite que o script "enter" seja executado no campo. A sintaxe para acionar o evento é<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENTO)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENTO</td>
   <td>Esse evento é acionado sempre que o usuário sai do campo. Permite que o mecanismo defina o valor do campo e execute seu script "exit". A sintaxe para acionar o evento é<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENTO)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENTO</td>
   <td>Esse evento é acionado para permitir que o mecanismo execute o script "change" gravado no campo. A sintaxe para acionar o evento é<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENTO)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENTO</td>
   <td>Esse evento é acionado sempre que o campo é clicado. permite que o mecanismo execute o script "click" gravado no campo. A sintaxe para acionar o evento é<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENTO)<br /> </td>
  </tr>
 </tbody>
</table>

#### APIs implementadas pelo widget {#apis-implemented-by-widget}

A estrutura de aparência chama algumas funções do widget que são implementadas nos widgets personalizados. O widget deve implementar as seguintes funções:

<table>
 <tbody>
  <tr>
   <th>Função</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>foco: function()</td>
   <td>Coloca o foco no campo.</td>
  </tr>
  <tr>
   <td>clique em: function()</td>
   <td>Coloca o foco no campo e chama XFA_CLICK_EVENTO.</td>
  </tr>
  <tr>
   <td><p>markError:function(errorMessage, errorType)<br /> <br /> <em>errorMessage: string </em>representando o erro<br /> <em>errorType: string ("warning"/"error")</em></p> <p><strong>Observação</strong>: Aplicável somente para formulários HTML5.</p> </td>
   <td>Envia mensagem de erro e tipo de erro para o widget. O widget exibe o erro.</td>
  </tr>
  <tr>
   <td><p>clearError: function()</p> <p><strong>Observação</strong>: Aplicável somente para formulários HTML5.</p> </td>
   <td>Chamado se os erros no campo foram corrigidos. O widget oculta o erro.</td>
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
   <td>multiline</td>
   <td>True se o campo suportar a inserção de um caractere de nova linha, caso contrário false.</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>Número máximo de caracteres que podem ser inseridos no campo.</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>Observação</strong>: Aplicável somente para formulários HTML5</p> </td>
   <td>Especifica o comportamento do campo de texto quando a largura do texto excede a largura do widget.</td>
  </tr>
 </tbody>
</table>

### ChoiceList: Lista suspensa, Caixa de listagem {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>Opção</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>valor<br /> </td>
   <td>Matriz de valores selecionados.<br /> </td>
  </tr>
  <tr>
   <td>items<br /> </td>
   <td>Matriz de objetos a serem exibidos como opções. Cada objeto contém duas propriedades - salvar<br /> : valor a ser salvo, exibir: valor a ser exibido.<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>editável</p> <p><strong>Observação</strong>: Aplicável somente para formulários HTML5.<br /> </p> </td>
   <td>Se o valor for verdadeiro, a entrada de texto personalizada será ativada no widget.<br /> </td>
  </tr>
  <tr>
   <td>displayValue<br /> </td>
   <td>Matriz de valores a serem exibidos.<br /> </td>
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
   <td><p>addItem:<em> function(itemValues)<br /> itemValues: objeto que contém o valor de exibição e salvamento <br /> {sDisplayVal: &lt;displayValue&gt;, sSaveVal: &lt;salvar valor&gt;}</em></p> </td>
   <td>Adiciona um item à lista.</td>
  </tr>
  <tr>
   <td>deleteItem<em>: function(nIndex)<br /> nIndex: índice do item a ser removido da lista<br /> </em><br /><br /> </td>
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
| dataType | String que representa o tipo de dados do campo (inteiro/decimal). |
| leadDigits | Máximo de dígitos à esquerda permitidos no número decimal. |
| fracDigits | Máximo de dígitos de fração permitidos no número decimal. |
| zero | Representação de string de zero na localidade do campo. |
| decimal | Representação de string de decimal na localidade do campo. |

### CheckButton: RadioButton, CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>Opções</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>values</td>
   <td><p>Matriz de valores (ligado/desligado/neutro).</p> <p>É uma matriz de valores para os diferentes estados de checkButton. valores[0] é o valor quando o estado está ATIVADO, valores[1] é o valor quando o estado está OFF,<br /> valores[2] é o valor quando o estado é NEUTRAL. O comprimento da matriz de valores é igual ao valor da opção de estado.<br /> </p> </td>
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
| dias | Nome de dias localizado para esse campo. |
| meses | Nomes de mês localizados para esse campo. |
| zero | O texto localizado para o número 0. |
| clearText | O texto localizado para o botão limpar. |
