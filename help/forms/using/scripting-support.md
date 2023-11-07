---
title: Suporte a script para formulários HTML5
seo-title: Scripting support for HTML5 forms
description: JavaScript, propriedades FormCalc e outros métodos compatíveis com o HTML5 Forms.
seo-description: JavaScript, FormCalc properties, and other methods that are supported in HTML5 Forms.
uuid: 697d5ec4-c818-41e4-b813-883c01b7ff3a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4ef78c8c-783f-4aac-a499-692cd4acef75
feature: Mobile Forms
exl-id: bcb5afc5-2190-4269-aba2-63842db9df3f
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '3888'
ht-degree: 7%

---

# Suporte a script para formulários HTML5 {#scripting-support-for-html-forms}

As propriedades JavaScript, FormCalc e os métodos compatíveis com formulários HTML5 estão listados abaixo:

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
   <td>Especifica o conteúdo do campo antes de ele ser alterado em resposta às ações de um usuário. Esse valor pode ser recuperado, de modo semelhante a um recurso de desfazer.</td>
   <td><p>Não funciona para caixas suspensas e de listagem. <code>PrevText </code>não funciona corretamente nos seguintes casos:</p>
    <ul>
     <li>Ao digitar algumas chaves de caracteres especiais (por exemplo, $, (,), &amp;, @ e mais) em campos Numéricos no iPad e </li>
     <li>Para o campo Date (quando a data é inserida por meio do calendário).<br /> </li>
    </ul> <p>Não há suporte para a configuração de valor por meio do script.</p> </td>
  </tr>
  <tr>
   <td><code>target</code></td>
   <td>Especifica o objeto sobre o qual o evento está agindo.</td>
   <td>Não há suporte para a configuração de valor por meio do script.<br /> </td>
  </tr>
  <tr>
   <td><code>newtext</code></td>
   <td>Especifica o conteúdo do campo depois que ele é alterado em resposta às ações do usuário.</td>
   <td><p>A variável <code>newText</code> A propriedade não funciona corretamente nos seguintes casos:</p>
    <ul>
     <li>Na seleção e substituição de textos</li>
     <li>Sobre exclusão, cópia e colagem de textos.</li>
     <li>Ao digitar algumas chaves de caracteres especiais (por exemplo, $, (, ), &amp;, @ e mais) em campos Numéricos<br /> </li>
     <li>Ao usar a combinação shift+alfanumeric. </li>
     <li>Sobre o uso de campos de data/hora.</li>
    </ul>
    <div>
      Não há suporte para a configuração de valor por meio do script.
    </div> </td>
  </tr>
  <tr>
   <td>alterar</td>
   <td>Especifica o valor que um usuário digita ou cola em um campo imediatamente após executar a ação. </td>
   <td><p>A propriedade de alteração não funciona corretamente nos seguintes casos:</p>
    <ul>
     <li>Na seleção e substituição de textos</li>
     <li>Sobre exclusão, cópia e colagem de textos.</li>
     <li>Ao digitar algumas chaves de caracteres especiais (por exemplo, $, (,), &amp;, @ e mais) em campos Numéricos<br /> </li>
     <li>Ao usar a combinação shift+alfanumeric. </li>
     <li>Sobre o uso de campos de data/hora.</li>
    </ul> <p>Não há suporte para a configuração de valor por meio do script.</p> </td>
  </tr>
  <tr>
   <td>keydown</td>
   <td>Determina se um usuário pressiona uma tecla de seta para fazer uma seleção. Essa propriedade está disponível somente para caixas de listagem e listas suspensas.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>modificador</td>
   <td>Determina se a tecla modificadora (por exemplo, Ctrl no Microsoft® Windows®) é mantida pressionada quando um evento específico é executado.</td>
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
   <td>Retorna o tipo de aplicativo do host. Disponível somente para aplicativos cliente.</td>
   <td>Devoluções <code>HTML 5</code>.</td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>Retorna o nome do aplicativo atual.</td>
   <td>Retorna o nome do navegador e sua versão. Por exemplo, no navegador Chrome, o valor retornado é <code>Chrome &lt;version&gt;.</code></td>
  </tr>
  <tr>
   <td><code>numPages</code></td>
   <td>Retorna o número de páginas no documento.</td>
   <td>A política de paginação de formulários HTML5 não é idêntica à política de paginação PDF forms. Portanto, a API numPages pode retornar valores diferentes em ambos os casos.</td>
  </tr>
  <tr>
   <td><code>platform</code></td>
   <td>Retorna uma cadeia de caracteres que representa a plataforma do computador que está executando o script.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>title</code></td>
   <td>Especifica o título do documento. Ele está disponível somente para aplicativos clientes.</td>
   <td>Ele retorna o título do documento de HTML no formulário, em vez do título dos metadados do formulário, como no caso de PDF forms.</td>
  </tr>
  <tr>
   <td><code>version</code></td>
   <td>Retorna uma cadeia de caracteres que representa o número da versão do aplicativo atual.</td>
   <td>Retorna a versão do formulário.</td>
  </tr>
  <tr>
   <td><code>calculationsEnabled</code></td>
   <td>Especifica se os scripts de cálculo serão executados.<br /> </td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>validationsEnabled</code></td>
   <td>Especifica se os scripts de validação serão executados.<br /> </td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>pageUp</code></td>
   <td>Vai para a página anterior.</td>
   <td>Os formulários HTML5 não seguem a mesma política de paginação que o formulário PDF, portanto, a página anterior de um formulário HTML5 é diferente da página anterior de um formulário PDF.</td>
  </tr>
  <tr>
   <td><code>pageDown</code></td>
   <td>Move para a próxima página de um formulário. Use o método pageDown no tempo de execução.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>setFocus</code></td>
   <td>Define o foco do teclado para o campo especificado. O campo é especificado como um objeto ou pela expressão SOM do campo. Ele está disponível somente para aplicativos clientes.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>resetdata</code></td>
   <td>Redefine os campos para seus valores padrão dentro de um documento.</td>
   <td>Limpa todos os dados em um formulário com dados mesclados, em vez de restaurá-los para os valores padrão.</td>
  </tr>
  <tr>
   <td><code>messageBox</code></td>
   <td>Mostra uma janela na tela. Ele está disponível somente para aplicativos clientes</td>
   <td>Caixa de mensagem do tipo Sim/Não é convertida em OK/Cancelar. A caixa de mensagem com três botões não é compatível.</td>
  </tr>
  <tr>
   <td>currentPage</td>
   <td><p>Define a página atualmente ativa de um documento no tempo de execução.</p> <p>Os valores de página são baseados em 0, portanto, a primeira página de um documento retorna um valor 0.</p> <p>A propriedade currentPage está disponível quando layout:ready é executado em um cliente. No entanto, não está disponível quando layout:ready é executado no servidor, pois a propriedade não será executada até que o layout do formulário seja executado.</p> </td>
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
   <td>Controla a participação do objeto associado em diferentes fases do processamento. Se o objeto for um container, o conteúdo do container herdará as restrições a que esse controle se aplica.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>access</code></td>
   <td>Controla o acesso do usuário ao conteúdo.</td>
   <td>Não funciona para o grupo de exclusão. Além disso, as formas HTML5 dão o mesmo tratamento a objetos não interativos e protegidos.<br /> </td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>Um identificador usado para identificar este elemento em expressões de script.</td>
   <td>formulários HTML5 não permitem definir a propriedade de nome para objetos. É uma propriedade somente leitura para formulários HTML5.</td>
  </tr>
  <tr>
   <td><code>value</code></td>
   <td>Um elemento de conteúdo que contém uma única unidade de conteúdo de dados.</td>
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
   <td>Configuração <code>formattedValue</code> por meio do script não é suportado.</td>
  </tr>
  <tr>
   <td><code>editValue</code></td>
   <td>Especifica o valor de edição desse campo.</td>
   <td>Configuração <code>editValue </code>por meio do script não é suportado.</td>
  </tr>
  <tr>
   <td><code>formatMessage</code></td>
   <td>Especifica a cadeia de caracteres de mensagem de validação de formato para este campo.</td>
   <td>Configuração <code>formatMessage </code>por meio do script não é suportado.</td>
  </tr>
  <tr>
   <td><code>fillcolor</code></td>
   <td>Especifica o valor da cor do plano de fundo para este campo. Você precisa definir a propriedade border.fill.present para visible separadamente.</td>
   <td>Ela não retorna corretamente a cor padrão do campo.</td>
  </tr>
  <tr>
   <td><code>border</code></td>
   <td>O objeto de borda descreve a borda ao redor de um objeto.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>ui</code></td>
   <td>O objeto de interface do usuário contém a descrição da interface do usuário de um objeto de formulário.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>mandatory</code></td>
   <td>Especifica o valor nullTest do campo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>borderColor</code></td>
   <td>Especifica o valor da cor da borda para este campo. Você precisa definir a propriedade border.edge.present como visível separadamente.</td>
   <td>Ela não retorna corretamente a cor de borda padrão do campo.</td>
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
   <td>Obtém o valor associado de um item de exibição específico de uma lista suspensa ou caixa de listagem.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>execCalculate</code></td>
   <td>Executa o script de cálculo do campo.</td>
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
   <td>Retorna o estado de seleção do item especificado</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>setItemState</code></td>
   <td>Define o estado de seleção do item especificado.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>getDisplayItem</code></td>
   <td>Recupera o texto de exibição do item para o índice de item especificado.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><code>getSaveItem</code></td>
   <td>Recupera o valor de dados do índice de item especificado.</td>
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
   <td>Uma medida da altura do layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>w</td>
   <td>Uma medida que especifica a largura do layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>x</td>
   <td>Especifica a coordenada x do ponto de ancoragem do contêiner em relação ao canto superior esquerdo do contêiner pai quando posicionado com o layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>y</td>
   <td>Especifica a coordenada y do ponto de ancoragem de um contêiner em relação ao canto superior esquerdo do contêiner pai quando posicionado com o layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>O objeto de legenda descreve um rótulo descritivo associado a um objeto de design de formulário.<br /> </td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>validar</td>
   <td>O objeto de validação controla a validação dos dados fornecidos pelo usuário em um formulário. O objeto de validação pode ser ativado várias vezes durante a vida útil de um formulário.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>parentSubform</td>
   <td>Especifica o subformulário principal (página) deste campo.</td>
   <td>Sempre retorna o subformulário pai em vez de retornar o primeiro subformulário pai sem escopo.<br /> </td>
  </tr>
  <tr>
   <td>seletedIndex</td>
   <td>O índice do primeiro item selecionado.</td>
   <td>Nenhum</td>
  </tr>
 </tbody>
</table>

## Formulário {#form}

| **Propriedade** | **Descrição** | **Exceção** |
|---|---|---|
| formNodes | Retorna uma lista de todos os objetos de modelo de formulário associados a um objeto de dados especificado. |  |

## InstanceManager {#instancemanager}

| Propriedade | Descrição |
|---|---|
| `name` | Um identificador usado para identificar este elemento em expressões de script. |
| `occur` | Descreve as restrições sobre o número de instâncias permitidas para seu contêiner de inclusão. |
| `min` | Especifica o número mínimo de instâncias que podem ser criadas. |
| `max` | Especifica o número máximo de instâncias que podem ser criadas. |
| `count` | Especifica o número atual de instâncias criadas. |
| `setInstances` | Adiciona ou remove os subformulários ou conjuntos de subformulários especificados deste nó. |
| `addInstance` | Adiciona uma nova instância de um subformulário ou conjunto de subformulários a este nó. |
| `removeInstance` | Remove um subformulário ou conjunto de subformulários deste nó. |
| `moveInstance` | Move um objeto filho de um objeto de modelo de formulário para outro local especificado no modelo de formulário. As informações correspondentes do modelo de dados para o objeto também são realocadas no modelo de dados. |
| `insertInstance` | Insere uma nova instância de um subformulário ou conjunto de subformulários neste nó. |

## list {#list}

| Propriedade | Descrição |
|---|---|
| `length` | O número de elementos na lista. |
| `item` | Um índice baseado em zero na coleção. |
| `append` | Anexa um nó ao final da lista de nós. |
| `remove` | Remove um nó da lista de nós. |
| `insert` | Insere um nó antes de um nó específico na lista de nós. |

## nó {#node}

| Propriedade | Descrição | Exceção |
|---|---|---|
| createNode | Cria um novo nó com base em um nome de classe válido. | Nenhum |
| `isContainer` | Especifica se este objeto é um objeto de contêiner. | Nenhum |
| `isNull` | Indica se o valor de dados atual é um valor nulo. | Nenhum |
| `resolveNode` | Avalia a expressão SOM especificada, começando com o objeto de modelo de objeto de formulário XML atual, e retorna o valor do objeto especificado na expressão SOM. | Nenhum |
| `resolveNodes` | Avalia a expressão SOM especificada, começando com o objeto de modelo de objeto de formulário XML atual, e retorna o valor do objeto especificado na expressão SOM. | Nenhum |
| oneOfChild | Cria um novo nó com base em um nome de classe válido. | Nenhum |
| getElement | Retorna um objeto filho especificado. | Nenhum |
| getAttribute | Obtém um valor de propriedade especificado. | Nenhum |
| setAttribute | Define o valor de uma propriedade especificada. | Nenhum |

## modelo {#model}

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
   <td>Especifica o índice do objeto, relativo às outras instâncias instanciadas.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>execEvent</td>
   <td>Executa o script de evento do objeto.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>getInvalidObjects</td>
   <td>Retorna uma lista de nós contidos no subformulário (inclusivo) que falharam no teste de validação.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>borda</td>
   <td>O objeto de borda descreve a borda ao redor de um objeto.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>Especifica o valor da cor da borda para este campo. Você precisa definir a propriedade border.edge.present como visível separadamente.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>h</td>
   <td>Uma medida da altura do layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>w</td>
   <td>Uma medida que especifica a largura do layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>x</td>
   <td>Especifica a coordenada x do ponto de ancoragem do contêiner em relação ao canto superior esquerdo do contêiner pai quando posicionado com o layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>y</td>
   <td>Especifica a coordenada y do ponto de ancoragem de um contêiner em relação ao canto superior esquerdo do contêiner pai quando posicionado com o layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>validar</td>
   <td>O objeto de validação controla a validação dos dados fornecidos pelo usuário em um formulário. O objeto de validação pode ser ativado várias vezes durante a vida útil de um formulário.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>name</td>
   <td>Um identificador usado para identificar este elemento em expressões de script.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>presença</td>
   <td>Especifica a visibilidade de um objeto.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>acesso</td>
   <td>Controla o acesso do usuário ao conteúdo de um objeto de contêiner, como um subformulário.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>execValidate</td>
   <td>Calcula o índice de um subformulário ou conjunto de subformulários com base em onde ele está localizado em relação a outras instâncias do mesmo objeto de formulário.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>instanceManager</td>
   <td>O objeto instanceManager gerencia a criação, a remoção e a movimentação da instância de objetos de modelo de formulário.<br /> </td>
   <td>Nenhum</td>
  </tr>
 </tbody>
</table>

### enviar {#submit}

| Propriedade | Descrição |
|---|---|
| público alvo | O URL para o qual os dados são enviados. A omissão desse atributo implica que o aplicativo de processamento XFA obtém o URI usando uma técnica específica do produto, como o acesso a informações específicas do produto no objeto de configuração. |

## árvore {#tree}

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Descrição</th>
   <th>Exceção</th>
  </tr>
  <tr>
   <td>nós</td>
   <td>Retorna uma lista de todos os objetos filho do objeto atual.</td>
   <td>
    <ul>
     <li>Não suportado para xfa.nodes, desc</li>
     <li>O número de nós relatados para PDF e HTML é diferente. </li>
    </ul> </td>
  </tr>
  <tr>
   <td>name</td>
   <td>Especifica o nome deste nó.</td>
   <td>Não é permitido definir o nome usando scripts no HTML.</td>
  </tr>
  <tr>
   <td>parent</td>
   <td>Obtém o pai deste nó.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>Índice</td>
   <td>Retorna a posição deste nó em sua coleção de nós de relacionamento como filho, com nomes semelhantes, no escopo.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>somExpression</td>
   <td>Obtém a expressão SOM para este nó.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>resolveNode</td>
   <td>Avalia a expressão SOM especificada, começando com o objeto de modelo de objeto de formulário XML atual, e retorna o valor do objeto especificado na expressão SOM.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>resolveNodes</td>
   <td>Avalia a expressão SOM especificada, começando com o objeto de modelo de objeto de formulário XML atual, e retorna o valor do objeto especificado na expressão SOM.</td>
   <td>Nenhum</td>
  </tr>
 </tbody>
</table>

## subformset {#subformset}

| Propriedade | Descrição | Exceção |
|---|---|---|
| instanceManager | O objeto instanceManager gerencia a criação, a remoção e a movimentação da instância de objetos de modelo de formulário. | Nenhum |

## content {#content}

| **Propriedade** | **Descrição** | **Exceção** |
|---|---|---|
| isNull | Indica se o valor de dados atual é o valor nulo. |  |

## dataValue {#datavalue}

| **Propriedade** | **Descrição** | **Exceção** |
|---|---|---|
| isNull | Indica se o valor de dados atual é o valor nulo. |  |

## borda {#edge}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade </strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>cor</td>
   <td>A propriedade color descreve uma cor exclusiva para o objeto de padrão.</td>
   <td>
    <ul>
     <li>O valor padrão não pode ser recuperado. </li>
     <li>As alterações são refletidas no Modelo e estão disponíveis para script, mas não são sincronizadas com os elementos HTML. Portanto, as alterações não são refletidas na interface do usuário.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## preenchimento {#fill}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>cor</td>
   <td>As propriedades de cor definem uma cor de preenchimento exclusiva.</td>
   <td>
    <ul>
     <li>O valor padrão não pode ser recuperado. </li>
     <li>As alterações são refletidas no Modelo e estão disponíveis para script, mas não são sincronizadas com os elementos HTML. Portanto, as alterações não são refletidas na interface do usuário.</li>
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
   <td>A propriedade color descreve uma cor exclusiva para um preenchimento gradiente linear em um formulário.</td>
   <td>
    <ul>
     <li>O valor padrão não pode ser recuperado. </li>
     <li>As alterações são refletidas no Modelo e estão disponíveis para script, mas não são sincronizadas com os elementos HTML. Portanto, as alterações não são refletidas na interface do usuário.</li>
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
   <td>borda</td>
   <td>O objeto de borda descreve um arco, uma linha ou um lado de uma borda ou um retângulo.<br /> </td>
   <td>Atributos como cor, limite e muito mais não são compatíveis.<br /> </td>
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
   <td>A propriedade color descreve uma cor exclusiva para o objeto de padrão. </td>
   <td>
    <ul>
     <li>O valor padrão não pode ser recuperado. </li>
     <li>As alterações são refletidas no Modelo e estão disponíveis para script, mas não são sincronizadas com os elementos HTML. Portanto, as alterações não são refletidas na interface do usuário.</li>
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
     <li>As alterações são refletidas no Modelo e estão disponíveis para script, mas não são sincronizadas com os elementos HTML. Portanto, as alterações não são refletidas na interface do usuário.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## pontilhado {#stipple}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>cor</td>
   <td>A propriedade color descreve uma cor exclusiva para o objeto pontilhado.</td>
   <td>
    <ul>
     <li>O valor padrão não pode ser recuperado. </li>
     <li>As alterações são refletidas no modelo e estão disponíveis para script, mas não são sincronizadas com os elementos HTML. Portanto, as alterações não são refletidas na interface do usuário.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## desenhar {#draw}

<table>
 <tbody>
  <tr>
   <td>Propriedade</td>
   <td>Descrição</td>
   <td>Exceção</td>
  </tr>
  <tr>
   <td>interface</td>
   <td>O objeto de interface do usuário contém a descrição da interface do usuário de um objeto de formulário.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>caption</td>
   <td>O objeto de legenda descreve um rótulo descritivo associado a um objeto de design de formulário.</td>
   <td> </td>
  </tr>
  <tr>
   <td>presença</td>
   <td>Especifica a visibilidade de um objeto.</td>
   <td> </td>
  </tr>
  <tr>
   <td>name</td>
   <td>Especifica um identificador que pode ser usado para especificar este objeto ou evento em expressões de script.</td>
   <td>Não há suporte para a configuração do valor no tempo de execução</td>
  </tr>
  <tr>
   <td>valor</td>
   <td>O objeto de valor delimita uma única unidade de conteúdo de dados.<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## canto {#corner}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exceção</strong></td>
  </tr>
  <tr>
   <td>cor</td>
   <td>A propriedade color descreve uma cor exclusiva para o objeto de canto.</td>
   <td>
    <ul>
     <li>O valor padrão não pode ser recuperado. </li>
     <li>As alterações são refletidas no modelo e estão disponíveis para script, mas não são sincronizadas com os elementos HTML. Portanto, as alterações não são refletidas na interface do usuário.</li>
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
   <td>borda</td>
   <td>O objeto de borda descreve a borda ao redor do objeto checkButton. </td>
   <td>As alterações são refletidas no modelo e estão disponíveis para script, mas não são sincronizadas com os elementos HTML. Portanto, as alterações não são refletidas na interface do usuário.<br /> </td>
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
   <td>borda</td>
   <td>O objeto de borda descreve a borda ao redor do objeto choiceList.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## dateTimeEdit {#datetimeedit}

| **Propriedade** | **Descrição** | **Exceção** |
|---|---|---|
| borda | O objeto de borda descreve a borda ao redor do objeto dateTimeEdit. |  |

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
   <td>Um identificador usado para identificar este elemento em expressões de script.</td>
   <td>Nenhum</td>
  </tr>
 </tbody>
</table>

## imageEdit {#imageedit}

| **Propriedade** | **Descrição** | **Exceção** |
|---|---|---|
| borda | O objeto de borda descreve a borda ao redor do objeto imageEdit. |  |

## numericEdit {#numericedit}

| **Propriedade** | **Descrição** | **Exceção** |
|---|---|---|
| borda | O objeto de borda descreve a borda ao redor de um objeto. | nenhuma |

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
   <td>Determina o nome da classe deste objeto.<br /> </td>
   <td>nenhuma</td>
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
   <td>borda</td>
   <td>O objeto de borda descreve um arco, uma linha ou um lado de uma borda ou um retângulo.<br /> </td>
   <td>Atributos como cor, limite e muito mais não são compatíveis.</td>
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
   <td>borda</td>
   <td>O objeto de borda descreve a borda ao redor de um objeto.<br /> </td>
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
   <td>Especifica a estratégia de layout a ser usada por este objeto.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>borda</td>
   <td>Especifica a borda em torno deste campo.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>obrigatório</td>
   <td>Especifica o valor nullTest do campo.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>Especifica o valor da cor da borda para este campo.Uma borda deve ser definida antes que você possa alterar a cor por meio de scripts.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>borderWidth</td>
   <td>Especifica a largura da borda deste campo.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>h</td>
   <td>Uma medida da altura do layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>transitório</td>
   <td>Especifica se o aplicativo de processamento deve salvar o valor do grupo de exclusão como parte de um envio de formulário ou de uma operação de salvamento.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>w</td>
   <td>Uma medida que especifica a largura do layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>x</td>
   <td>Especifica a coordenada x do ponto de ancoragem do contêiner em relação ao canto superior esquerdo do contêiner pai quando posicionado com o layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>y</td>
   <td>Especifica a coordenada y do ponto de ancoragem de um contêiner em relação ao canto superior esquerdo do contêiner pai quando posicionado com o layout.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>O objeto de legenda descreve um rótulo descritivo associado a um objeto de design de formulário.<br /> </td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>validar</td>
   <td>O objeto de validação controla a validação dos dados fornecidos pelo usuário em um formulário. O objeto de validação pode ser ativado várias vezes durante a vida útil de um formulário.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>dataNode</td>
   <td>Obtém o nó de dados ao qual um nó de formulário está associado após a mesclagem.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>presença</td>
   <td>Especifica a visibilidade de um objeto.</td>
   <td> </td>
  </tr>
  <tr>
   <td>acesso</td>
   <td>Controla o acesso do usuário ao conteúdo de um objeto de contêiner, como um subformulário.</td>
   <td>Para itens individuais no exclgrp, ele sempre retorna aberto. </td>
  </tr>
  <tr>
   <td>name</td>
   <td>Especifica um identificador que pode ser usado para especificar este objeto ou evento em expressões de script.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>membros</td>
   <td>Especifique os membros do grupo de exclusão. </td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>seletedMember</td>
   <td>Retorna o membro selecionado de um grupo de exclusão.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>execCalculate</td>
   <td>Executa qualquer script no evento de cálculo do objeto especificado e em qualquer objeto filho.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>calcular</td>
   <td>O objeto de cálculo controla o cálculo do valor de um campo.<br /> </td>
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
   <td>borda</td>
   <td>O objeto de borda descreve um arco, uma linha ou um lado de uma borda ou um retângulo.<br /> </td>
   <td>Atributos como cor, limite e muito mais não são compatíveis. </td>
  </tr>
 </tbody>
</table>

## borda {#border}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade<strong></strong></strong></td>
   <td><strong>Descrição<strong></strong></strong></td>
   <td><strong>Exceção<strong></strong></strong></td>
  </tr>
  <tr>
   <td>borda</td>
   <td>O objeto de borda descreve um arco, uma linha ou um lado de uma borda ou um retângulo.<br /> </td>
   <td>Atributos como cor, limite e muito mais não são compatíveis. </td>
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
     <li>A propriedade de altura (h) não é compatível com a área de página e a área de conteúdo. </li>
     <li>O parâmetro 'Deslocamento da primeira área de conteúdo na qual o objeto XFA-Form ocorre' não é compatível.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>w</td>
   <td>Determina a largura de um determinado objeto de design de formulário.</td>
   <td>
    <ul>
     <li>A propriedade de largura (w) não é compatível com a área de página e a área de conteúdo. </li>
     <li>O parâmetro 'Deslocamento da primeira área de conteúdo na qual o objeto XFA-Form ocorre' não é compatível.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>x</td>
   <td>Determina a coordenada x de um determinado objeto de design de formulário em relação ao seu objeto pai.</td>
   <td>
    <ul>
     <li>A propriedade de coordenadas x (x) não é compatível com a área de página e de conteúdo. </li>
     <li>O parâmetro 'Deslocamento da primeira área de conteúdo na qual o objeto XFA-Form ocorre' não é compatível.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>y</td>
   <td>Determina a coordenada y de um determinado objeto de design de formulário em relação ao seu objeto pai.</td>
   <td>
    <ul>
     <li>A propriedade de coordenada y (y) não é compatível com a área de página e de conteúdo. </li>
     <li>O parâmetro 'Deslocamento da primeira área de conteúdo na qual o objeto XFA-Form ocorre' não é compatível.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecount</td>
   <td>Determina o número de páginas do formulário atual.</td>
   <td>
    <ul>
     <li>O método layout.pageCount() retorna valores diferentes para formulários PDF e HTML.</li>
     <li>Ao diminuir a contagem de páginas ocultando um objeto, o método abspagecount retorna um valor incorreto.<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecontent</td>
   <td>Recupera tipos de objetos de design de formulário de uma página especificada de um formulário.</td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td>absPageCount</td>
   <td>Determina a contagem de páginas do formulário atual.</td>
   <td>
    <ul>
     <li>O método layout.pageCount() retorna valores diferentes para formulários PDF e HTML.</li>
     <li>Ao diminuir a contagem de páginas ocultando um objeto, o método abspagecount retorna um valor incorreto.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## itens {#items}

| **Propriedade** | **Descrição** | **Exceção** |
|---|---|---|
| presença | Especifica a visibilidade de um objeto. | Nenhum |

## FormCalc {#formcalc}

FormCalc é uma linguagem específica do XFA para criar lógica centrada no formulário eletrônico e raízes de cálculos. FormCalculation fornece um conjunto avançado de funções de build.

### Funções compatíveis com FormCalc {#formcalc-supported-functions}

### Suporte à expressão FormCalc {#formcalc-expression-support}

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
   <td>Expressão lógica</td>
   <td>
    <ul>
     <li>Lógica (e/ou)</li>
     <li>Comparação (maior/menor/igual)</li>
    </ul> </td>
   <td>A ou 1<br /> 1 &lt;&gt; 2<br /> A NE B<br /> A ou 1<br /> 1 &lt;&gt; 2<br /> A NE B</td>
  </tr>
  <tr>
   <td>Expressão If</td>
   <td><br type="_moz" /> </td>
   <td>se (a&gt;b) então 2 endif</td>
  </tr>
  <tr>
   <td>enquanto</td>
   <td><br type="_moz" /> </td>
   <td>enquanto (i lt 5) do i = i + 1 endwhile</td>
  </tr>
  <tr>
   <td> para </td>
   <td><br type="_moz" /> </td>
   <td>para i = 100 para 1 <br /> do s = s + i endfor</td>
  </tr>
  <tr>
   <td>para cada</td>
   <td><br type="_moz" /> </td>
   <td>para cada i em (1, 2, 3) <br /> do s = s + i endfor</td>
  </tr>
  <tr>
   <td>declaração de função</td>
   <td>Definir uma função personalizada em FormCalc</td>
   <td>func foo(n) do var f = n endfunc</td>
  </tr>
 </tbody>
</table>

### Suporte à API do Acrobat {#acrobat-api-support}

1. **Funções aritméticas**

   1. Abs()
   1. Avg()
   1. Célula()
   1. Contagem()
   1. Piso()
   1. Max()
   1. Mín()
   1. Mod()
   1. Arrendondar()
   1. Soma()

1. **Funções científicas**

   1. Acos()
   1. Asin()
   1. Atan()
   1. Atan2()
   1. Cos()
   1. Sin()
   1. Bronze()
   1. Exp()
   1. Registro()
   1. Pow()
   1. Sqrt()
   1. Deg2Rad()
   1. Rad2Deg()
   1. Pi()

1. **Funções Financeiras**

   1. Abr()
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
   1. Dentro()

1. **Funções de string**

   1. Em()
   1. Concat()
   1. Esquerda()
   1. Len()
   1. Lower()
   1. Ltrim()
   1. Substituir()
   1. Direita()
   1. Rtrim()
   1. Espaço()
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
   <td>Essa API do acrobat despeja a saída no console do JavaScript.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.alert()</td>
   <td>Essa API do Acrobat envia uma mensagem de alerta por meio do pop-up JavaScript.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.beep()</td>
   <td>Faz com que o sistema toque um som.</td>
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
   <td>Especifica um script JavaScript e um período. O script é executado toda vez que o período decorre. O valor de retorno desse método deve ser mantido em uma variável JavaScript. Caso contrário, o objeto do intervalo está sujeito à coleta de lixo, o que faria com que o relógio parasse. Para encerrar a execução periódica, passe o objeto de intervalo retornado para clearInterval.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setTimeOut()</td>
   <td>Especifica um script JavaScript e um período. O script é executado apenas uma vez depois que o período decorre. O valor de retorno desse método deve ser mantido em uma variável JavaScript. Caso contrário, o objeto de tempo limite está sujeito à coleta de lixo, o que faria com que o relógio parasse. Para cancelar o evento de tempo limite, passe o objeto de tempo limite retornado para clearTimeOut.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.clearInterval()</td>
   <td>Cancela um intervalo registrado anteriormente definido inicialmente pelo método setInterval.</td>
   <td>Nos formulários HTML5, a API não funciona corretamente.</td>
  </tr>
  <tr>
   <td>app.clearTimeOut()</td>
   <td>Cancela um intervalo de tempo limite registrado anteriormente. Esse intervalo é definido inicialmente por setTimeOut.</td>
   <td>Nos formulários HTML5, a API não funciona corretamente.<br /> </td>
  </tr>
  <tr>
   <td>app.eval()</td>
   <td>Executa um determinado script.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.activeDocs</td>
   <td>Uma matriz que contém o objeto Doc para cada documento ativo. Se nenhum documento estiver ativo, o ativeDocs não retornará nada; ou seja, ele tem o mesmo comportamento que d = new Array(0) no JavaScript principal.</td>
   <td>Retorna uma matriz vazia para formulários HTMl5.</td>
  </tr>
  <tr>
   <td>app.calculate</td>
   <td>Se true (o valor padrão), os cálculos poderão ser executados. Se false, os cálculos não serão permitidos.</td>
   <td>Sempre verdadeiro para Forms HTMl5.</td>
  </tr>
  <tr>
   <td>app.constants</td>
   <td>Um objeto wrapper para manter vários valores constantes. Atualmente, essa propriedade retorna um objeto com uma única propriedade, align.</td>
   <td>Os formulários HTML5 retornam um objeto de alinhamento vazio.</td>
  </tr>
  <tr>
   <td>app.focusRect</td>
   <td>Ativa e desativa o retângulo de foco. O retângulo de foco é a linha pontilhada esmaecida ao redor de botões, caixas de seleção, botões de opção e assinaturas para indicar que o campo de formulário tem o foco do teclado. Um valor true gira no retângulo de foco.</td>
   <td>Sempre verdadeiro para formulários HTML5.</td>
  </tr>
  <tr>
   <td>app.formsVersion</td>
   <td>O número da versão do software de formulários do visualizador. Marque essa propriedade para determinar se objetos, propriedades ou métodos nas versões mais recentes do software estão disponíveis se você deseja manter a compatibilidade com versões anteriores nos scripts.</td>
   <td>11.001 sempre.</td>
  </tr>
  <tr>
   <td>app.language</td>
   <td>O idioma do visualizador do Acrobat em execução.</td>
   <td>Sempre "ENU" para formulários HTMl5.</td>
  </tr>
 </tbody>
</table>

## Eventos XFA compatíveis {#supported-xfa-events}

Os seguintes eventos XFA do lado do cliente são compatíveis:

* Inicializar
* Validar
* Calcular
* Clique em
* Insira
* Sair
* Alterar
* ValidationState

>[!NOTE]
>
>Os formulários HTML5 são renderizados no lado do cliente (navegador). Usar do lado do cliente **validar** e **calcular** scripts em vez de scripts do lado do servidor.
