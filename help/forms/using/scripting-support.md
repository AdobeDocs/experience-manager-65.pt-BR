---
title: Suporte a scripts para formulários HTML5
seo-title: Suporte a scripts para formulários HTML5
description: JavaScript, propriedades FormCalc e outros métodos compatíveis com o HTML5 Forms.
seo-description: JavaScript, propriedades FormCalc e outros métodos compatíveis com o HTML5 Forms.
uuid: 697d5ec4-c818-41e4-b813-883c01b7ff3a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4ef78c8c-783f-4aac-a499-692cd4acef75
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Suporte a scripts para formulários HTML5 {#scripting-support-for-html-forms}

As propriedades JavaScript, FormCalc e os métodos suportados em formulários HTML5 são os seguintes:

## $event {#event}

<table>
 <tbody>
  <tr>
   <th>Propriedade </th>
   <th>Descrição<br /> </th>
   <th>Exceção</th>
  </tr>
  <tr>
   <td><code>prevText</code></td>
   <td>Especifica o conteúdo do campo antes de sua alteração em resposta a ações de um usuário. Esse valor pode ser retomado, semelhante a um recurso desfazer.</td>
   <td><p>Não funciona para caixas suspensas e listas. <code>PrevText </code>não funciona corretamente nos seguintes casos:</p>
    <ul>
     <li>Ao digitar algumas teclas de caractere especiais (por exemplo $, (,), &amp;, @ e mais) nos campos numéricos no iPad e </li>
     <li>Para o campo Data (quando a data é informada pelo calendário).<br /> </li>
    </ul> <p>Não há suporte para a configuração de valor por meio de script.</p> </td>
  </tr>
  <tr>
   <td><code>target</code></td>
   <td>Especifica o objeto sobre o qual o evento está agindo.</td>
   <td>Não há suporte para a configuração de valor por meio de script.<br /> </td>
  </tr>
  <tr>
   <td><code>newtext</code></td>
   <td>Especifica o conteúdo do campo após a sua alteração em resposta a ações de usuários.</td>
   <td><p>A <code>newText</code> propriedade não funciona corretamente nos seguintes casos:</p>
    <ul>
     <li>Sobre a seleção e a substituição de textos</li>
     <li>Ao excluir, copiar e colar textos.</li>
     <li>Ao digitar algumas teclas de caractere especiais (por exemplo $, (, ), &amp;, @ e muito mais) em campos numéricos<br /> </li>
     <li>Ao usar a combinação shift+alfanumérico. </li>
     <li>Ao usar campos de data/hora.</li>
    </ul>
    <div>
      Não há suporte para a configuração de valor por meio de script.
    </div> </td>
  </tr>
  <tr>
   <td>change</td>
   <td>Especifica o valor que um usuário insere ou cola em um campo imediatamente após executar a ação. </td>
   <td><p>A propriedade change não funciona corretamente nos seguintes casos:</p>
    <ul>
     <li>Sobre a seleção e a substituição de textos</li>
     <li>Ao excluir, copiar e colar textos.</li>
     <li>Ao digitar algumas teclas de caractere especiais (por exemplo $, (,), &amp;, @ e mais) em campos numéricos<br /> </li>
     <li>Ao usar a combinação shift+alfanumérico. </li>
     <li>Ao usar campos de data/hora.</li>
    </ul> <p>Não há suporte para a configuração de valor por meio de script.</p> </td>
  </tr>
  <tr>
   <td>tecla</td>
   <td>Determina se um usuário está pressionando uma tecla de seta para fazer uma seleção. Essa propriedade apenas está disponível em caixas de listagem e listas suspensas.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>modifier</td>
   <td>Determina se a tecla modificadora (por exemplo, Ctrl no Microsoft® Windows®) permanece pressionada quando um evento específico é executado.</td>
   <td>Nenhum</td>
  </tr>
 </tbody>
</table>

### $host {#host}

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Descrição</th>
   <th>Exceção</th>
  </tr>
  <tr>
   <td><code>apptype</code></td>
   <td>Retorna o tipo de aplicativo do host. Disponível somente para aplicativos clientes.</td>
   <td>Retorna <code>HTML 5</code>.</td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>Retorna o nome do aplicativo atual.</td>
   <td>Retorna o nome do navegador e sua versão. Por exemplo, no navegador Chrome, o valor retornado é <code>Chrome &lt;version&gt;.</code></td>
  </tr>
  <tr>
   <td><code>numPages</code></td>
   <td>Retorna o número de páginas no documento.</td>
   <td>A política de paginação de formulários HTML5 não é idêntica à política de paginação de formulários PDF. Portanto, a API numPages pode retornar valores diferentes em ambos os casos.</td>
  </tr>
  <tr>
   <td><code>platform</code></td>
   <td>Retorna uma string que representa a plataforma do computador que executa o script.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>title</code></td>
   <td>Especifica o título do documento. Apenas está disponível para aplicativos clientes.</td>
   <td>Ele retorna o título do documento HTML no formulário, em vez do título dos metadados do formulário, como no caso dos Formulários PDF.</td>
  </tr>
  <tr>
   <td><code>version</code></td>
   <td>Retorna uma string que representa o número da versão do aplicativo atual.</td>
   <td>Retorna a versão do formulário.</td>
  </tr>
  <tr>
   <td><code>calculationsEnabled</code></td>
   <td>Especifica se scripts calculate serão executados.<br /> </td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>validationsEnabled</code></td>
   <td>Specifies whether validation scripts will execute.<br /> </td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>pageUp</code></td>
   <td>Vai para a página anterior.</td>
   <td>Os formulários HTML5 não seguem a mesma política de paginação que o Formulário PDF, portanto, a página anterior de um formulário HTML5 é diferente da página anterior de um Formulário PDF.</td>
  </tr>
  <tr>
   <td><code>pageDown</code></td>
   <td>Vai para a próxima página de um formulário. Use o método pageDown em tempo de execução.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>setFocus</code></td>
   <td>Define o foco do teclado para o campo especificado. O campo é especificado como um objeto ou pela expressão SOM do campo. Apenas está disponível para aplicativos clientes.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>resetdata</code></td>
   <td>Redefine os campos com seus valores padrão em um documento.</td>
   <td>Limpa todos os dados em um formulário com dados unidos, em vez de restaurá-los aos valores padrão.</td>
  </tr>
  <tr>
   <td><code>messageBox</code></td>
   <td>Exibe uma caixa de diálogo na tela. Apenas está disponível para aplicativos clientes</td>
   <td>Caixa de mensagem do tipo Sim/Não é convertida em OK/Cancelar. Não há suporte para a caixa de mensagem com três botões.</td>
  </tr>
  <tr>
   <td>currentPage</td>
   <td><p>Define a página atualmente ativa de um documento no tempo de execução.</p> <p>Os valores de páginas usam 0 como base e, portanto, a primeira página de um documento retorna um valor 0.</p> <p>A propriedade currentPage está disponível quando a propriedade layout:ready é executada em um cliente. Entretanto, não está disponível quando a propriedade layout:ready é executada no servidor porque essa propriedade só será executada quando o layout do formulário for executado.</p> </td>
   <td>Nenhum</td>
  </tr>
 </tbody>
</table>

### campo {#field}

<table>
 <tbody>
  <tr>
   <th><strong><span>Propriedade</span></strong></th>
   <th><strong><span>Descrição<br /> </span></strong></th>
   <th><strong><span>Exceção</span></strong></th>
  </tr>
  <tr>
   <td><code>presence</code></td>
   <td>Controla a participação do objeto associado em diferentes fases de processamento. Se o objeto for um container, o conteúdo do container herdará quaisquer restrições que esse controle aplicar.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>access</code></td>
   <td>Controla o acesso do usuário ao conteúdo.</td>
   <td>Não funciona para o grupo de exclusão. Além disso, os formulários HTML5 dão o mesmo tratamento a objetos não interativos e protegidos.<br /> </td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>Um identificador usado para identificar esse elemento nas expressões de script.</td>
   <td>Formulários HTML5 não permitem definir a propriedade name para objetos. É uma propriedade somente leitura para formulários HTML5.</td>
  </tr>
  <tr>
   <td><code>value</code></td>
   <td>Um elemento de conteúdo que inclui uma única unidade de conteúdo de dados.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>rawValue</code></td>
   <td>Especifica o valor não formatado para este campo.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>formattedValue</code></td>
   <td>Especifica o valor formatado para este campo.</td>
   <td>A configuração <code>formattedValue</code> por script não é suportada.</td>
  </tr>
  <tr>
   <td><code>editValue</code></td>
   <td>Especifica o valor de edição para este campo.</td>
   <td>A configuração <code>editValue </code>por script não é suportada.</td>
  </tr>
  <tr>
   <td><code>formatMessage</code></td>
   <td>Especifica a string da mensagem de validação de formato para esse campo.</td>
   <td>A configuração <code>formatMessage </code>por script não é suportada.</td>
  </tr>
  <tr>
   <td><code>fillcolor</code></td>
   <td>Especifica o valor da cor de plano de fundo para este campo. É necessário definir a propriedade border.fill.presence como visível separadamente.</td>
   <td>Ela não retorna corretamente a cor padrão do campo.</td>
  </tr>
  <tr>
   <td><code>border</code></td>
   <td>O objeto border descreve as bordas que circundam um objeto.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>ui</code></td>
   <td>O objeto ui object engloba a descrição da interface do usuário de um objeto de formulário.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>mandatory</code></td>
   <td>Especifica o valor de nullTest do campo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>borderColor</code></td>
   <td>Especifica o valor de cor da borda desse campo. É necessário definir a propriedade border.edge.presence como visível separadamente.</td>
   <td>Ela não retorna corretamente a cor da borda padrão do campo.</td>
  </tr>
  <tr>
   <td><code>length</code></td>
   <td>O número de itens na lista.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>addItem</code></td>
   <td>Adiciona novos itens ao campo atual.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>clearItem</code></td>
   <td>Remove todos os itens do campo.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>boundItem</code></td>
   <td>Obtém o valor vinculado de um item de exibição específico de uma lista suspensa ou caixa de listagem.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>execCalculate</code></td>
   <td>Executa o script calculate do campo.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>execValidate</code></td>
   <td>Executa o script de validação do campo.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>execEvent</code></td>
   <td>Executa o script de evento do objeto.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>getItemState</code></td>
   <td>Retorna o estado da seleção do item especificado</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>setItemState</code></td>
   <td>Define o estado da seleção do item especificado.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>getDisplayItem</code></td>
   <td>Recupera o texto de exibição do item para o índice de itens especificado.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>getSaveItem</code></td>
   <td>Recupera o valor de dados para o índice de itens especificado.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>deleteItem</code></td>
   <td>Exclui o item no índice especificado.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>setItems</code></td>
   <td>Define os itens especificados no campo atual. Substitui itens pré-existentes.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>h</td>
   <td>Uma medida da altura para o layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>w</td>
   <td>Uma medida que especifica a largura para o layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>x</td>
   <td>Especifica a coordenada X do ponto de ancoragem do container em relação ao canto superior esquerdo do container pai quando posicionado com o layout posicionado.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>y</td>
   <td>Especifica a coordenada Y do ponto de ancoragem de um container em relação ao canto superior esquerdo do container pai quando posicionado com o layout posicionado.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>O objeto caption descreve um rótulo descritivo associado a um objeto de design de formulário.<br /> </td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>validate</td>
   <td>O objeto validate controla a validação dos dados fornecidos pelo usuário em um formulário. O objeto validate pode ser ativado várias vezes durante a vida de um formulário.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>parentSubform</td>
   <td>Especifica o subformulário pai (página) desse campo.</td>
   <td>Sempre retorna o subformulário pai em vez de retornar o primeiro subformulário pai sem escopo.<br /> </td>
  </tr>
  <tr>
   <td>selectedIndex</td>
   <td>O índice do primeiro item selecionado.</td>
   <td>Nenhum</td>
  </tr>
 </tbody>
</table>

## Formulário {#form}

| **Propriedade** | **Descrição** | **Exceção** |
|---|---|---|
| formNodes | Retorna uma lista de todos os objetos de modelo de formulário que estão vinculados a um objeto de dados especificado. |  |

## InstanceManager {#instancemanager}

| Propriedade | Descrição |
|---|---|
| `name` | Um identificador usado para identificar esse elemento nas expressões de script. |
| `occur` | Descreve as restrições sobre o número de instâncias permitidas para seu container de inclusão. |
| `min` | Especifica o número mínimo de instâncias que podem ser instanciadas. |
| `max` | Especifica o número máximo de instâncias que podem ser instanciadas. |
| `count` | Especifica o número atual de instâncias instanciadas. |
| `setInstances` | Adiciona ou remove os subformulários ou conjuntos de subformulários especificados desse nó. |
| `addInstance` | Adiciona uma nova instância de um subformulário ou conjunto de subformulários a esse nó. |
| `removeInstance` | Remove um subformulário ou conjunto de subformulários desse nó. |
| `moveInstance` | Move um objeto filho de um objeto de modelo de formulário para outro local especificado no modelo de formulário. As informações correspondentes do modelo de dados para o objeto também são realocadas no modelo de dados. |
| `insertInstance` | Insere uma nova instância de um subformulário ou conjunto de subformulários nesse nó. |

## list {#list}

| Propriedade | Descrição |
|---|---|
| `length` | O número de elementos na lista. |
| `item` | Um índice com base em zero na coleção. |
| `append` | Anexa um nó ao final da lista de nós. |
| `remove` | Remove um nó da lista de nós. |
| `insert` | Insere um nó antes de um nó específico na lista de nós. |

## node {#node}

| Propriedade | Descrição | Exceção |
|---|---|---|
| createNode | Cria um novo nó com base em um nome de classe válido. | Nenhum |
| `isContainer` | Especifica se esse objeto é um objeto de contêiner. | Nenhum |
| `isNull` | Indica se o valor de dados atual é um valor nulo. | Nenhum |
| `resolveNode` | Avalia a expressão SOM especificada, começando pelo objeto de modelo de objeto de formulário XML atual, e retorna o valor do objeto especificado na expressão SOM. | Nenhum |
| `resolveNodes` | Avalia a expressão SOM especificada, começando pelo objeto de modelo de objeto de formulário XML atual, e retorna o valor do objeto especificado na expressão SOM. | Nenhum |
| oneOfChild | Cria um novo nó com base em um nome de classe válido. | Nenhum |
| getElement | Retorna um objeto filho especificado. | Nenhum |
| getAttribute | Obtém um valor de propriedade especificado. | Nenhum |
| setAttribute | Define o valor de uma propriedade especificada. | Nenhum |

## model {#model}

| Propriedade | Descrição | Exceção |
|---|---|---|
| ND | ND | ND |

## Subformulário {#subform}

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Descrição</th>
   <th>Exceção</th>
  </tr>
  <tr>
   <td>instanceIndex</td>
   <td>Especifica o índice do objeto, em relação às outras instâncias instanciadas.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>execEvent</td>
   <td>Executa o script de evento do objeto.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>getInvalidObjects</td>
   <td>Retorna uma lista de nós contidos no subformulário (inclusive) que falharam no teste de validação.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>border</td>
   <td>O objeto border descreve as bordas que circundam um objeto.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>Especifica o valor de cor da borda desse campo. É necessário definir a propriedade border.edge.presence como visível separadamente.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>h</td>
   <td>Uma medida da altura para o layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>w</td>
   <td>Uma medida que especifica a largura para o layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>x</td>
   <td>Especifica a coordenada X do ponto de ancoragem do container em relação ao canto superior esquerdo do container pai quando posicionado com o layout posicionado.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>y</td>
   <td>Especifica a coordenada Y do ponto de ancoragem de um container em relação ao canto superior esquerdo do container pai quando posicionado com o layout posicionado.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>validate</td>
   <td>O objeto validate controla a validação dos dados fornecidos pelo usuário em um formulário. O objeto validate pode ser ativado várias vezes durante a vida de um formulário.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>name</td>
   <td>Um identificador usado para identificar esse elemento nas expressões de script.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>presence</td>
   <td>Especifica a visibilidade de um objeto.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>access</td>
   <td>Controla o acesso de usuários ao conteúdo de um contêiner , como um subformulário.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>execValidate</td>
   <td>Calcula o índice de um subformulário ou de um conjunto de subformulários com base no local em que está localizado em relação a outras instâncias do mesmo objeto de formulário.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>instanceManager</td>
   <td>O objeto instanceManager gerencia a criação, remoção e movimentação de instâncias de objetos de modelos de formulários.<br /> </td>
   <td>Nenhum</td>
  </tr>
 </tbody>
</table>

### submit {#submit}

| Propriedade | Descrição |
|---|---|
| target | O URL para o qual os dados são enviados. A omissão deste atributo implica que o aplicativo de processamento XFA obtém o URI usando uma técnica específica do produto, como acessar informações específicas do produto no objeto de configuração. |

## árvore {#tree}

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Descrição</th>
   <th>Exceção</th>
  </tr>
  <tr>
   <td>nodes</td>
   <td>Retorna uma lista de todos os objetos filho do objeto atual.</td>
   <td>
    <ul>
     <li>Não suportado para xfa.nodes, desc</li>
     <li>O número de nós relatados para PDF e HTML é diferente. </li>
    </ul> </td>
  </tr>
  <tr>
   <td>name</td>
   <td>Especifica o nome desse nó.</td>
   <td>A configuração do nome usando scripts não é permitida em HTML.</td>
  </tr>
  <tr>
   <td>parent</td>
   <td>Obtém o pai deste nó.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>index</td>
   <td>Retorna a posição desse nó em sua coleção de nós de relacionamento semelhantes, no escopo e semelhantes.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>somExpression</td>
   <td>Obtém a expressão SOM para este nó.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>resolveNode</td>
   <td>Avalia a expressão SOM especificada, começando pelo objeto de modelo de objeto de formulário XML atual, e retorna o valor do objeto especificado na expressão SOM.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>resolveNodes</td>
   <td>Avalia a expressão SOM especificada, começando pelo objeto de modelo de objeto de formulário XML atual, e retorna o valor do objeto especificado na expressão SOM.</td>
   <td>Nenhum</td>
  </tr>
 </tbody>
</table>

## subformset {#subformset}

| Propriedade | Descrição | Exceção |
|---|---|---|
| instanceManager | O objeto instanceManager gerencia a criação, remoção e movimentação de instâncias de objetos de modelos de formulários. | Nenhum |

## content {#content}

| **Propriedade** | **Descrição** | **Exceção** |
|---|---|---|
| isNull | Indica se o valor de dados atual é o valor nulo. |  |

## dataValue {#datavalue}

| **Propriedade** | **Descrição** | **Exceção** |
|---|---|---|
| isNull | Indica se o valor de dados atual é o valor nulo. |  |

## edge {#edge}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade </strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>cor</td>
   <td>A propriedade color descreve uma cor exclusiva para o objeto pattern.</td>
   <td>
    <ul>
     <li>O valor padrão não pode ser recuperado. </li>
     <li>As alterações são refletidas no Modelo e estão disponíveis para scripts, mas não são sincronizadas com elementos HTML. Portanto, as alterações não são refletidas na interface do usuário.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## fill {#fill}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>cor</td>
   <td>As propriedades de cores definem uma cor exclusiva de preenchimento.</td>
   <td>
    <ul>
     <li>O valor padrão não pode ser recuperado. </li>
     <li>As alterações são refletidas no Modelo e estão disponíveis para scripts, mas não são sincronizadas com elementos HTML. Portanto, as alterações não são refletidas na interface do usuário.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## linear {#linear}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>cor</td>
   <td>A propriedade color descreve uma cor exclusiva para um preenchimento de gradiente linear em um formulário.</td>
   <td>
    <ul>
     <li>O valor padrão não pode ser recuperado. </li>
     <li>As alterações são refletidas no Modelo e estão disponíveis para scripts, mas não são sincronizadas com elementos HTML. Portanto, as alterações não são refletidas na interface do usuário.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## linha {#line}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>O objeto edge descreve um arco, linha ou lado de uma borda ou retângulo.<br /> </td>
   <td>Atributos como cor, cap e muito mais não são suportados.<br /> </td>
  </tr>
 </tbody>
</table>

## padrão {#pattern}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>cor</td>
   <td>A propriedade color descreve uma cor exclusiva para o objeto pattern. </td>
   <td>
    <ul>
     <li>O valor padrão não pode ser recuperado. </li>
     <li>As alterações são refletidas no Modelo e estão disponíveis para scripts, mas não são sincronizadas com elementos HTML. Portanto, as alterações não são refletidas na interface do usuário.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## radial {#radial}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>cor</td>
   <td>A propriedade color descreve uma cor exclusiva para o objeto radial</td>
   <td>
    <ul>
     <li>O valor padrão não pode ser recuperado. </li>
     <li>As alterações são refletidas no Modelo e estão disponíveis para scripts, mas não são sincronizadas com elementos HTML. Portanto, as alterações não são refletidas na interface do usuário.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## stipple {#stipple}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>cor</td>
   <td>A propriedade color descreve uma cor exclusiva para o objeto stipple.</td>
   <td>
    <ul>
     <li>O valor padrão não pode ser recuperado. </li>
     <li>As alterações são refletidas no modelo e estão disponíveis para scripts, mas não são sincronizadas com elementos HTML. Portanto, as alterações não são refletidas na interface do usuário.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## draw {#draw}

<table>
 <tbody>
  <tr>
   <td>Propriedade</td>
   <td>Descrição</td>
   <td>Exceção</td>
  </tr>
  <tr>
   <td>ui</td>
   <td>O objeto ui object engloba a descrição da interface do usuário de um objeto de formulário.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>caption</td>
   <td>O objeto caption descreve um rótulo descritivo associado a um objeto de design de formulário.</td>
   <td> </td>
  </tr>
  <tr>
   <td>presence</td>
   <td>Especifica a visibilidade de um objeto.</td>
   <td> </td>
  </tr>
  <tr>
   <td>name</td>
   <td>Especifica um identificador que pode ser usado para especificar esse objeto ou evento em expressões de script.</td>
   <td>Não há suporte para a definição do valor no tempo de execução</td>
  </tr>
  <tr>
   <td>valor</td>
   <td>O objeto valor abrange uma unidade única de conteúdo de dados.<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## corner {#corner}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>cor</td>
   <td>A propriedade color descreve uma cor exclusiva para o objeto corner.</td>
   <td>
    <ul>
     <li>O valor padrão não pode ser recuperado. </li>
     <li>As alterações são refletidas no modelo e estão disponíveis para scripts, mas não são sincronizadas com elementos HTML. Portanto, as alterações não são refletidas na interface do usuário.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## checkButton {#checkbutton}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>border</td>
   <td>O objeto border descreve a borda que envolve o objeto checkButton. </td>
   <td>As alterações são refletidas no modelo e estão disponíveis para scripts, mas não são sincronizadas com elementos HTML. Portanto, as alterações não são refletidas na interface do usuário.<br /> </td>
  </tr>
 </tbody>
</table>

## choiceList {#choicelist}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade<br /> </strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>border</td>
   <td>O objeto border descreve a borda que delimita o objeto choiceList.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## dateTimeEdit {#datetimeedit}

| **Propriedade** | **Descrição** | **Exceção** |
|---|---|---|
| border | O objeto border descreve a borda que delimita o objeto dateTimeEdit. |  |

## Imagem {#image}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>contentType</td>
   <td>Especifica o tipo de conteúdo no documento referenciado, expresso como um tipo MIME.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>name<br /> </td>
   <td>Um identificador usado para identificar esse elemento nas expressões de script.</td>
   <td>Nenhum</td>
  </tr>
 </tbody>
</table>

## imageEdit {#imageedit}

| **Propriedade** | **Descrição** | **Exceção** |
|---|---|---|
| border | O objeto border descreve a borda que envolve o objeto imageEdit. |  |

## numericEdit {#numericedit}

| **Propriedade** | **Descrição** | **Exceção** |
|---|---|---|
| border | O objeto border descreve as bordas que circundam um objeto. | nenhum |

## objeto {#object}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>className</td>
   <td>Determina o nome da classe desse objeto.<br /> </td>
   <td>nenhum</td>
  </tr>
 </tbody>
</table>

## retângulo {#rectangle}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>O objeto edge descreve um arco, linha ou lado de uma borda ou retângulo.<br /> </td>
   <td>Atributos como cor, cap e muito mais não são suportados.</td>
  </tr>
 </tbody>
</table>

## textEdit {#textedit}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>border</td>
   <td>O objeto border descreve as bordas que circundam um objeto.<br /> </td>
   <td>Nenhum</td>
  </tr>
 </tbody>
</table>

## exclGroup {#exclgroup}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>layout</td>
   <td>Especifica a estratégia de layout a ser usada por esse objeto.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>border</td>
   <td>Especifica a borda em torno desse campo.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>mandatory</td>
   <td>Especifica o valor de nullTest do campo.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>Especifica o valor de cor da borda desse campo.Uma borda deve ser definida antes que você possa alterar a cor por script.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>borderWidth</td>
   <td>Especifica a largura da borda desse campo.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>h</td>
   <td>Uma medida da altura para o layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>transient</td>
   <td>Especifica se o aplicativo de processamento deve salvar o valor do grupo de exclusão como parte de uma submissão de formulário ou de uma operação de gravação.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>w</td>
   <td>Uma medida que especifica a largura para o layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>x</td>
   <td>Especifica a coordenada X do ponto de ancoragem do container em relação ao canto superior esquerdo do container pai quando posicionado com o layout posicionado.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>y</td>
   <td>Especifica a coordenada Y do ponto de ancoragem de um container em relação ao canto superior esquerdo do container pai quando posicionado com o layout posicionado.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>O objeto caption descreve um rótulo descritivo associado a um objeto de design de formulário.<br /> </td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>validate</td>
   <td>O objeto validate controla a validação dos dados fornecidos pelo usuário em um formulário. O objeto validate pode ser ativado várias vezes durante a vida de um formulário.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>dataNode</td>
   <td>Obtém o nó de dados para qual um nó de formulário é vinculado após a fusão.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>presence</td>
   <td>Especifica a visibilidade de um objeto.</td>
   <td> </td>
  </tr>
  <tr>
   <td>access</td>
   <td>Controla o acesso de usuários ao conteúdo de um contêiner , como um subformulário.</td>
   <td>Para itens individuais no exclgrp, ele sempre retorna aberto. </td>
  </tr>
  <tr>
   <td>name</td>
   <td>Especifica um identificador que pode ser usado para especificar esse objeto ou evento em expressões de script.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>membros</td>
   <td>Especifique os membros do grupo de exclusão. </td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>selectedMember</td>
   <td>Retorna o membro selecionado de um grupo de exclusão.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>execCalculate</td>
   <td>Executa qualquer script no evento calculate do objeto especificado, e qualquer objeto filho.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>calculate</td>
   <td>O objeto calculate controla o cálculo do valor do campo.<br /> </td>
   <td>Nenhum</td>
  </tr>
 </tbody>
</table>

## arco {#arc}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade<strong></strong></strong></td>
   <td><strong>Descrição<strong></strong></strong></td>
   <td><strong>Exceção<strong></strong></strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>O objeto edge descreve um arco, linha ou lado de uma borda ou retângulo.<br /> </td>
   <td>Atributos como cor, cap e muito mais não são suportados. </td>
  </tr>
 </tbody>
</table>

## border {#border}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade<strong></strong></strong></td>
   <td><strong>Descrição<strong></strong></strong></td>
   <td><strong>Exceção<strong></strong></strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>O objeto edge descreve um arco, linha ou lado de uma borda ou retângulo.<br /> </td>
   <td>Atributos como cor, cap e muito mais não são suportados. </td>
  </tr>
 </tbody>
</table>

## $layout {#layout}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>h</td>
   <td>Determina a altura de um determinado objeto de design de formulário.<br /> </td>
   <td>
    <ul>
     <li>A propriedade Altura (h) não é compatível com a área de página e a área de conteúdo. </li>
     <li>O parâmetro "Deslocamento da primeira área de conteúdo na qual o objeto XFA-Form ocorre" não é suportado.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>w</td>
   <td>Determina a largura de um determinado objeto de design de formulário.</td>
   <td>
    <ul>
     <li>A propriedade de largura (w) não é suportada para área de página e área de conteúdo. </li>
     <li>O parâmetro "Deslocamento da primeira área de conteúdo na qual o objeto XFA-Form ocorre" não é suportado.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>x</td>
   <td>Determina a coordenada x de um determinado objeto de design de formulário em relação ao objeto pai.</td>
   <td>
    <ul>
     <li>A propriedade coordenada x (x) não é compatível com área de página e área de conteúdo. </li>
     <li>O parâmetro "Deslocamento da primeira área de conteúdo na qual o objeto XFA-Form ocorre" não é suportado.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>y</td>
   <td>Determina a coordenada Y de um determinado objeto de design de formulário em relação ao objeto pai.</td>
   <td>
    <ul>
     <li>A propriedade coordenada y (y) não é compatível com a área de página e a área de conteúdo. </li>
     <li>O parâmetro "Deslocamento da primeira área de conteúdo na qual o objeto XFA-Form ocorre" não é suportado.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecount</td>
   <td>Determina o número de páginas do formulário atual.</td>
   <td>
    <ul>
     <li>o método layout.pageCount() retorna valores diferentes para formulários PDF e HTML.</li>
     <li>Ao diminuir a contagem de páginas ocultando um objeto, o método abspagecount retorna um valor incorreto.<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecontent</td>
   <td>Recupera tipos de objetos de design de formulário de determinada página de formulário.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>absPageCount</td>
   <td>Determina a contagem de páginas do formulário atual.</td>
   <td>
    <ul>
     <li>o método layout.pageCount() retorna valores diferentes para formulários PDF e HTML.</li>
     <li>Ao diminuir a contagem de páginas ocultando um objeto, o método abspagecount retorna um valor incorreto.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## items {#items}

| **Propriedade** | **Descrição** | **Exceção** |
|---|---|---|
| presence | Especifica a visibilidade de um objeto. | Nenhum |

## FormCalc {#formcalc}

FormCalc é uma linguagem específica do XFA para criar raízes de lógica e cálculos centradas em forma de e-form. FormCalculation fornece um conjunto avançado de funções de compilação.

### Funções suportadas por FormCalc {#formcalc-supported-functions}

### Suporte de Expressão FormCalc {#formcalc-expression-support}

<table>
 <tbody>
  <tr>
   <td><strong>Categoria </strong></td>
   <td><strong>Descrição </strong></td>
   <td><strong>Amostra </strong></td>
  </tr>
  <tr>
   <td>Expressão simples</td>
   <td>Adicionar, subtrair, multiplicar, dividir e parênteses</td>
   <td>(a+b)*3</td>
  </tr>
  <tr>
   <td>Declaração de variável</td>
   <td>Definir uma variável</td>
   <td>var a<br /> var a=3<br /> a=3</td>
  </tr>
  <tr>
   <td>expressão lógica</td>
   <td>
    <ul>
     <li>Lógica (e/ou)</li>
     <li>Comparação (maior/menor/igual)</li>
    </ul> </td>
   <td>A ou 1<br /> 1 &lt;&gt; 2<br /> A NE B<br /> A ou 1<br /> 1 &lt;&gt; 2<br /> A NE B</td>
  </tr>
  <tr>
   <td>Se expressão</td>
   <td><br type="_moz" /> </td>
   <td>if (a&gt;b) then 2 endif</td>
  </tr>
  <tr>
   <td>while</td>
   <td><br type="_moz" /> </td>
   <td>while (i - lt 5) do i = i + 1 endwhile</td>
  </tr>
  <tr>
   <td>para</td>
   <td><br type="_moz" /> </td>
   <td>para i = 100 downto 1 <br /> do s = s + i endfor</td>
  </tr>
  <tr>
   <td>para cada</td>
   <td><br type="_moz" /> </td>
   <td>para cada i em (1, 2, 3) <br /> do s = s + i endfor</td>
  </tr>
  <tr>
   <td>declaração de função</td>
   <td>Definir uma função personalizada no FormCalc</td>
   <td>func foo(n) do var f = n endfunc</td>
  </tr>
 </tbody>
</table>

### Suporte à API do Acrobat {#acrobat-api-support}

1. **Funções aritméticas**

   1. Abs()
   1. Avg()
   1. Ceil()
   1. Contagem()
   1. Floor()
   1. Máximo()
   1. Mínimo()
   1. Mod()
   1. Round()
   1. Soma()

1. **Funções científicas**

   1. Acos()
   1. Asin()
   1. Atan()
   1. Atan2()
   1. Cos()
   1. Sin()
   1. Tan()
   1. Exp()
   1. Registro()
   1. Pow()
   1. Sqrt()
   1. Deg2Rad()
   1. Rad2Deg()
   1. Pi()

1. **Funções financeiras**

   1. Apr()
   1. Cterm()
   1. Fv()
   1. Ipmt()
   1. Npv()
   1. Pmt()
   1. Ppmt()
   1. Pv()
   1. Rate()
   1. Termo()

1. **Funções lógicas**

   1. Choose()
   1. If()
   1. Oneof()
   1. Within()

1. **Funções de string**

   1. Em()
   1. Concat()
   1. À esquerda()
   1. Len()
   1. Lower()
   1. Ltrim()
   1. Substituir()
   1. Direito()
   1. Rtrim()
   1. Space()
   1. Stuff()
   1. Substr()
   1. Upper()
   1. WordNum()

1. **Data e hora**

   1. Data()
   1. num2date()
   1. DateFmt()

<table>
 <tbody>
  <tr>
   <td><strong>API</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Aberração</strong></td>
  </tr>
  <tr>
   <td>console.println()</td>
   <td>Essa API acrobat descarta a saída para o console javascript.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.alert()</td>
   <td>Essa API acrobat envia uma mensagem de alerta por meio de pop-up javascript.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.beep()</td>
   <td>Faz com que o sistema emita um som.</td>
   <td>Nenhuma ação é executada.</td>
  </tr>
  <tr>
   <td>app.execDialog()</td>
   <td>Apresenta uma caixa de diálogo modal ao usuário. As caixas de diálogo modais devem ser fechadas pelo usuário antes que o aplicativo host possa ser usado diretamente novamente.</td>
   <td>Nenhuma ação é executada.<br /> </td>
  </tr>
  <tr>
   <td>app.launchURL()</td>
   <td>Inicia um URL em uma janela do navegador.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setInterval()</td>
   <td>Especifica um script JavaScript e um período de tempo. O script é executado sempre que o período decorre. O valor de retorno desse método deve ser mantido em uma variável JavaScript. Caso contrário, o objeto de intervalo estará sujeito à coleta de lixo, o que faria com que o relógio parasse. Para encerrar a execução periódica, passe o objeto de intervalo retornado para clearInterval.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setTimeOut()</td>
   <td>Especifica um script JavaScript e um período de tempo. O script é executado apenas uma vez, após o período decorrer.O valor de retorno desse método deve ser mantido em uma variável JavaScript. Caso contrário, o objeto timeout será sujeito à coleta de lixo, o que faria com que o relógio parasse. Para cancelar o evento timeout, passe o objeto timeout retornado para clearTimeOut.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.clearInterval()</td>
   <td>Cancela um intervalo registrado anteriormente definido inicialmente pelo método setInterval.</td>
   <td>Nos formulários HTML5, a API não funciona corretamente.</td>
  </tr>
  <tr>
   <td>app.clearTimeOut()</td>
   <td>Cancela um intervalo de tempo limite registrado anteriormente. Tal intervalo é inicialmente definido por setTimeOut.</td>
   <td>Nos formulários HTML5, a API não funciona corretamente.<br /> </td>
  </tr>
  <tr>
   <td>app.eval()</td>
   <td>Executa um determinado script.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.activeDocs</td>
   <td>Uma matriz que contém o objeto Doc para cada documento ativo. Se nenhum documentos estiver ativo, ativeDocs não retornará nada; ou seja, ele tem o mesmo comportamento de d = new Array(0) no JavaScript principal.</td>
   <td>Retorna uma matriz vazia para formulários HTMl5.</td>
  </tr>
  <tr>
   <td>app.calculate</td>
   <td>Se verdadeiro (o valor padrão), os cálculos podem ser executados. Se falso, os cálculos não são permitidos.</td>
   <td>Sempre verdadeiro para formulários HTMl5.</td>
  </tr>
  <tr>
   <td>app.constants</td>
   <td>Um objeto wrapper para manter vários valores constantes. No momento, essa propriedade retorna um objeto com uma única propriedade, alinhar.</td>
   <td>Formulários HTML5 retornam um objeto de alinhamento vazio.</td>
  </tr>
  <tr>
   <td>app.focusRect</td>
   <td>Ativa e desativa o retângulo de foco. O retângulo de foco é a linha pontilhada esmaecida ao redor de botões, caixas de seleção, botões de opção e assinaturas para indicar que o campo de formulário tem o foco do teclado. Um valor de true ativa o retângulo de foco.</td>
   <td>Sempre verdadeiro para formulários HTML5.</td>
  </tr>
  <tr>
   <td>app.formsVersion</td>
   <td>O número da versão do software de formulários do visualizador. Verifique essa propriedade para determinar se objetos, propriedades ou métodos em versões mais recentes do software estão disponíveis se você deseja manter a compatibilidade com versões anteriores em seus scripts.</td>
   <td>11.001 sempre.</td>
  </tr>
  <tr>
   <td>app.language</td>
   <td>O idioma do visualizador do Acrobat em execução.</td>
   <td>Sempre "ENU" para formulários HTMl5.</td>
  </tr>
 </tbody>
</table>

## eventos XFA suportados {#supported-xfa-events}

Os seguintes eventos XFA do lado do cliente são suportados:

* Inicializar
* Validar
* Calcular
* Clique em
* Enter
* Sair
* Alterar
* EstadoValidação

>[!NOTE]
>
>Os formulários HTML5 são renderizados no lado do cliente (navegador). Recomenda-se usar a **validação** e o **cálculo** de scripts no cliente em vez de scripts no servidor.
