---
title: Formulário definido em AEM Forms
seo-title: Formulário definido em AEM Forms
description: Este artigo introduz um conjunto de formulários e explica como criar conjuntos de formulários unindo formulários HTML5. Este artigo também explica como é possível pré-preencher dados xml para um conjunto de formulários e como é possível usar conjuntos de formulários no gerenciamento de processos.
seo-description: Este artigo introduz um conjunto de formulários e explica como criar conjuntos de formulários unindo formulários HTML5. Este artigo também explica como é possível pré-preencher dados xml para um conjunto de formulários e como é possível usar conjuntos de formulários no gerenciamento de processos.
uuid: a1a2f267-26a9-4f45-bcfc-dbdedad95973
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 80e3eec4-95e0-4731-a0e5-a617e9bcb069
docset: aem65
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '2860'
ht-degree: 0%

---


# Formulário definido em AEM Forms{#form-set-in-aem-forms}

## Visão geral {#overview}

Seus clientes geralmente são obrigados a enviar vários formulários para solicitar um serviço ou benefício. Trata-se de encontrar todas as formas relevantes; e preenchê-los, enviá-los e rastreá-los separadamente. Além disso, é necessário que eles preencham detalhes comuns várias vezes nos formulários. Todo o processo fica complicado e sujeito a erros se envolver um grande número de formulários. O recurso de conjunto de formulários do AEM Forms pode ajudar a simplificar a experiência do usuário em tais cenários.

Um conjunto de formulários é uma coleção de formulários HTML5 agrupados e apresentados como um único conjunto de formulários para os usuários finais. Quando os usuários finais start para preencher um conjunto de formulários, eles são perfeitamente transitados de um formulário para outro. No final, eles podem enviar todos os formulários com apenas um clique.

O AEM Forms fornece aos autores de formulário uma interface de usuário intuitiva para criar, configurar e gerenciar conjuntos de formulários. Como autor, você pode solicitar formulários em uma sequência específica que deseja que os usuários finais sigam. Além disso, você pode aplicar condições ou expressões de qualificação em formulários individuais para controlar sua visibilidade com base em entradas do usuário. Por exemplo, é possível configurar o formulário de detalhes do cônjuge para que apareça somente quando o status civil especificar como Casado.

Além disso, é possível configurar campos comuns em diferentes formulários para compartilhar vínculos de dados comuns. Com vínculos de dados adequados em vigor, os usuários finais devem preencher informações comuns somente uma vez que sejam preenchidas automaticamente em formulários subsequentes.

Os conjuntos de formulários também são suportados no aplicativo AEM Forms, permitindo que a força de trabalho de campo coloque um conjunto de formulários offline, visite os clientes, insira dados e sincronize posteriormente com o servidor AEM Forms para enviar dados de formulários aos processos comerciais.

## Criação e gerenciamento do conjunto de formulários {#creating-and-managing-form-set}

É possível associar vários XDPs ou Modelos de formulário criados usando o Designer em um conjunto de formulários. Os conjuntos de formulários podem ser usados para renderizar seletivamente os XDPs com base nos valores inseridos pelos usuários nos formulários iniciais e seus perfis.

Use a interface [de usuário do](../../forms/using/introduction-managing-forms.md) AEM Forms para gerenciar todos os formulários, conjuntos de formulários e ativos relacionados.

### Criar um conjunto de formulários {#create-a-form-set}

Para criar um conjunto de formulários, faça o seguinte:

1. Selecione Forms > Forms e Documentos.
1. Selecione Criar > Conjunto de formulários.

1. Na página Adicionar propriedades, adicione os detalhes a seguir e clique em Avançar.

   * Título: Especifica o título do documento. O título ajuda a identificar o conjunto de formulários na interface do usuário do AEM Forms.
   * Descrição: Especifica as informações detalhadas sobre o documento.
   * Tags: Especifica tags para identificar exclusivamente o conjunto de formulários. As tags ajudam na pesquisa do conjunto de formulários. Para criar tags, digite novos nomes de tags na caixa Tags.
   * Enviar URL: Especifica o URL no qual os dados enviados são postados para o caso de renderização independente do conjunto de formulários (caso de uso de aplicativo não-AEM Forms). Os dados são enviados para este terminal como dados multipart/formdata com o seguinte parâmetro de solicitação:
   * dataXML: Esse parâmetro contém uma representação XML dos dados enviados do conjunto de formulários. Se todos os formulários no conjunto de formulários usarem um schema comum, o XML será gerado de acordo com esse schema. Caso contrário, a tag raiz XML contém uma tag filho para cada formulário preenchido no conjunto de formulários que contém dados para os anexos do formulário.
   * formsetPath: O caminho do conjunto de formulários no CRXDE, que foi enviado.
   * Perfil de renderização HTML: É possível configurar determinadas opções, como campos flutuantes, anexos e suporte a rascunho (para execução de conjunto de formulários independente) para personalizar a aparência, o comportamento e as interações do conjunto de formulários. Você pode personalizar ou estender o perfil existente para alterar quaisquer configurações de perfil de formulário HTML.

   ![Conjunto de formulários: adicionar propriedades](assets/createformset1.png)

1. A tela Selecionar formulário(s) exibe os formulários XDP ou arquivos XDP disponíveis. Pesquise e selecione os formulários a serem incluídos no conjunto de formulários e clique em Adicionar ao conjunto de formulários. Se necessário, pesquise novamente os formulários a serem adicionados. Depois de adicionar todos os formulários ao conjunto de formulários, clique em Avançar.

   >[!NOTE]
   >
   >Certifique-se de que os nomes de campo nos formulários XDP não contenham o caractere de ponto. Caso contrário, os scripts que tentam resolver os campos, que têm caracteres de ponto, não poderão resolvê-los.

1. Na página Configurar formulários, é possível fazer o seguinte:

   * Pedido de formulário: Arraste e solte os formulários para reorganizá-los. A ordem do formulário define a ordem na qual os formulários são mostrados ao usuário final no aplicativo AEM Forms e na execução independente.
   * Identificador de formulário: Especifica uma identidade exclusiva para os formulários a serem usados nas expressões de qualificação.
   * Raiz de dados: Para cada formulário no conjunto de formulários, o Autor pode configurar o XPATH no qual os dados desse formulário específico são posicionados no XML enviado. Por padrão, o valor é /. Se todos os formulários no conjunto de formulários estiverem vinculados ao schema e compartilharem o mesmo schema XML, é possível alterar esse valor. É recomendável que cada campo no formulário tenha um vínculo de dados adequado especificado no XDP. Se dois campos em dois formulários diferentes compartilharem o vínculo de dados comum, o campo no segundo formulário mostrará valores pré-preenchidos do primeiro formulário. Não vincule dois subformulários com o mesmo conteúdo interno ao mesmo nó XML. Para obter mais informações sobre a estrutura XML do conjunto de formulários, consulte [Preencher XML para conjunto](../../forms/using/formset-in-aem-forms.md#p-prefill-xml-for-form-set-p)de formulários.
   * expressão de qualificação: Especifica uma expressão JavaScript que avalia um valor booliano e indica se um formulário no conjunto de formulários está qualificado para preenchimento. Se falso, o usuário não é solicitado ou nem mesmo exibido para preencher o formulário. Normalmente, a expressão se baseia nos valores dos campos capturados antes deste formulário. O Expressão também contém chamadas para o conjunto de formulários API fs.valueOf para extrair os valores preenchidos pelo usuário em um campo de um formulário do conjunto de formulários:

   *fs.valueOf(&lt;Identificador de formulário>, &lt;expressão fieldSom>) > &lt;valor>*

   Por exemplo, se você tiver dois formulários no conjunto de formulários: despesas de negócios e despesas de viagem, você pode adicionar um trecho do JavaScript no campo Expressão Elegibilidade para ambos os formulários para verificar a entrada do usuário quanto ao tipo de despesa em um formulário. Se o usuário escolher Despesa de Negócios, o formulário Despesa de Negócios será renderizado para o usuário final. Ou se o usuário escolher despesas de viagem, um formulário diferente será renderizado para o usuário final. Para obter mais informações, consulte Expressão de qualificação.

   Além disso, o Autor também pode optar por remover um formulário do conjunto de formulários usando o ícone Excluir presente no canto direito de cada linha ou adicionar outro conjunto de formulários usando o ícone &quot;**+**&quot; na barra de ferramentas. Este ícone &#39;**+**&#39; direciona o usuário de volta para a etapa anterior do assistente, que foi usada para &#39;Selecionar formulário(s)&#39;. As seleções existentes são mantidas e qualquer seleção adicional feita deve ser adicionada ao conjunto de formulários usando o ícone Adicionar ao conjunto de formulários nessa página.

   ![Conjunto de formulários: Configurar formulários](assets/createformset2.png)

   >[!NOTE]
   >
   >Todos os formulários usados no conjunto de formulários são gerenciados pela interface do usuário do AEM Forms.

### Gerenciamento de um conjunto de formulários {#managing-a-form-set}

Depois que um conjunto de formulários é criado, é possível executar as seguintes ações nesse conjunto de formulários:

* Clique uma vez: Quando o conjunto de formulários é criado e listado na página principal do ativo, você pode clicar uma vez no conjunto de formulários para visualização. Um conjunto de formulários é aberto e exibe todos os modelos de formulário (XDPs) nesse conjunto de formulários.
* Editar: Ao clicar em Editar após selecionar um conjunto de formulários, a tela Configurar formulários, que é mostrada acima em Etapas para criar um conjunto de formulários, é aberta. Você pode realizar todas as funcionalidades descritas aqui.
* Copiar + Colar: Isso permite copiar o conjunto de formulários inteiro de um local e colá-lo ao mesmo tempo ou em qualquer outro local ou pasta.
* Download: É possível baixar o conjunto de formulários com todas as suas dependências.
* Revisão de Start/gerenciamento: Depois que o conjunto de formulários é criado, você pode configurar sua revisão clicando em Revisão do Start. Depois que a revisão for iniciada para um conjunto de formulários, a opção Gerenciar revisão será exibida para o usuário. Na tela Gerenciar revisão, você pode atualizar/encerrar a revisão. Para as revisões adicionadas, você pode verificar a revisão e adicionar comentários, se necessário.
* Excluir: Exclui o conjunto de formulários completo. Os formulários no conjunto de formulários excluído permanecem no repositório.
* Publicar/Cancelar publicação: Isso publica/cancela a publicação do conjunto de formulários juntamente com todos os formulários que ele contém e os ativos relacionados desses formulários.
* Pré-visualização: A Pré-visualização oferece duas opções: Pré-visualização como HTML (sem dados) e pré-visualização personalizada com dados de amostra.
* Propriedades de Visualização/edição: É possível visualização/editar as propriedades de metadados de um conjunto de formulários selecionado.

![createformset3](assets/createformset3.png)

### Editar um conjunto de formulários {#edit-a-form-set}

Para editar um conjunto de formulários, faça o seguinte:

1. Selecione Forms > Forms e Documentos.
1. Localize o conjunto de formulários que deseja editar. Passe o mouse sobre ele e selecione Editar ( ![diticon](assets/editicon.png)).
1. Na página Configurar formulários, é possível editar o seguinte:

   * Pedido de formulário
   * Formulário Identificador
   * Raiz de dados
   * expressão de qualificação

   Você também pode clicar no ícone Excluir relevante para excluir o formulário do Conjunto de formulários.

## Conjunto de formulários no Process Management {#form-set-in-process-management}

Depois de criar um conjunto de formulários usando a interface de usuário do Gerenciamento de AEM Forms, você pode usar o conjunto de formulários em um Ponto de Start ou Atribuir atividade de Tarefa usando o Workbench.

### Uso do conjunto de formulários no ponto de Tarefa ou Start {#using-form-set-in-task-or-start-point}

1. Ao projetar um processo, na seção Apresentação e dados de Atribuir Tarefa/Ponto de Start, selecione **usar um ativo** CRX. O navegador CRX Asset é exibido.

   ![Projete um processo: usar um ativo CRX](assets/formsetinprocessmgmt1.png)

1. Selecione o conjunto de formulários para filtrar o conjunto de formulários AEM repositório (CRX).

   ![Projete um processo: Caixa de diálogo Selecionar ativo do formulário](assets/formsetinprocessmgmt2.png)

1. Seleciona um conjunto de formulários e clique em OK.

## Expressões de qualificação {#eligibility-expressions}

As expressões de qualificação em um conjunto de formulários são usadas para definir e controlar dinamicamente os formulários exibidos para um usuário. Por exemplo, para exibir um formulário específico somente se o usuário pertencer a um grupo etário específico. Especifique e edite uma expressão de qualificação usando o gerenciador de formulários.

Uma expressão de qualificação pode ser qualquer instrução JavaScript válida que retorna um valor booliano. A última instrução no trecho de código JavaScript é tratada como um valor booliano que determina a elegibilidade do formulário com base no processamento no restante (linhas anteriores) do trecho de código JavaScript. Se o valor da expressão for verdadeiro, o formulário estará qualificado para ser exibido ao usuário. Esses formulários são conhecidos como formulários elegíveis.

>[!NOTE]
>
>A expressão de qualificação para o primeiro formulário no conjunto de formulários não é executada. O primeiro formulário é sempre exibido independentemente de sua expressão de qualificação.

Além das funções padrão do JavaScript, o conjunto de formulários também expõe a API fs.valueOf que fornece acesso ao valor de um campo de um formulário em um conjunto de formulários. Use essa API para acessar o valor de um campo de formulário em um conjunto de formulários. A sintaxe da API é fs.valueOf (formUid, fieldSOM), onde:

* formUid (string): Uma ID exclusiva de um formulário no conjunto de formulários. É possível especificá-lo ao criar o conjunto de formulários na interface do usuário do gerenciador de formulários. Por padrão, é o nome do formulário.
* fieldSOM (string): Uma expressão SOM do campo no formulário especificado por formUid. A expressão SOM ou a expressão de Modelo de objeto de script é usada para fazer referência a valores, propriedades e métodos em um DOM (Modelo de objeto de documento) específico. É possível visualização no Designer de formulários na guia Scripts enquanto o campo está selecionado.

>[!NOTE]
>
>Os parâmetros formUid e fieldSOM devem ser literais de string.

### Exemplos {#examples}

Uso válido da API:

`fs.valueOf("form1", "xfa.form.form1.subform1.field1")`

Uso inválido da API:

```javascript
var formUid = "form1";
 var fieldSOM = “xfa.form.form1.subform1.field1"; fs.valueOf(formUid, fieldSOM);
```

## Preencher XML para conjunto de formulários {#prefill-xml-for-form-set}

O conjunto de formulários é uma coleção de vários formulários HTML5 que têm schemas comuns ou diferentes. O conjunto de formulários suporta o pré-preenchimento de campos de formulário usando um arquivo XML. É possível associar um arquivo XML a um conjunto de formulários para que, ao abrir um formulário no conjunto de formulários, alguns dos campos no formulário sejam pré-polulados.

O arquivo XML de preenchimento prévio é especificado usando o parâmetro dataRef do URL do conjunto de formulários. O parâmetro dataRef especifica o caminho absoluto do arquivo XML de dados que é unido ao conjunto de formulários.

Por exemplo, você tem três formulários (formulário1, formulário2 e formulário3), no conjunto de formulários com a seguinte estrutura:

form1

campoForma1

form2

fieldform2field

form3

campoFormato3campo

Cada formulário tem um campo com nome comum, chamado &quot;field&quot; e um campo com nome exclusivo, chamado &quot;form&lt;i>field&quot;.

É possível pré-preencher esse conjunto de formulários usando um XML com a seguinte estrutura:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<formSetRootTag>
 <field>common field value</field>
 <form1field>value1</form1field>
 <form2field>value2</form2field>
 <form3field>value3</form3field>
</formSetRootTag>
```

>[!NOTE]
>
>A tag raiz XML pode ter qualquer nome, mas as tags de elemento correspondentes aos campos devem ter o mesmo nome do campo. A hierarquia do XML deve imitar a hierarquia do formulário, o que significa que o XML deve ter tags correspondentes para o vínculo de subformulários.

O trecho XML acima mostra que o XML de preenchimento prévio para o conjunto de formulários é uma união dos trechos XML de preenchimento prévio dos formulários individuais. Se determinados campos nos diferentes formulários tiverem hierarquia/schema de dados semelhante, os campos serão preenchidos com os mesmos valores. Neste exemplo, os três formulários recebem o mesmo valor do campo comum, &quot;field&quot;. Essa é uma maneira simples de transmitir dados de um formulário para o seguinte. Isso também pode ser feito vinculando os campos ao mesmo schema ou referência de dados. Se desejar separar os dados do conjunto de formulários com base no schema dos formulários. Isso pode ser feito especificando o atributo &quot;raiz de dados&quot; do formulário durante a criação do conjunto de formulários (o valor padrão é &quot;/&quot;, que mapeia para a tag raiz do conjunto de formulários).

No exemplo anterior, se você especificar as raízes de dados: &quot;/form1&quot;, &quot;/form2&quot; e &quot;/form3&quot; respectivamente para os três formulários, é necessário usar um XML de preenchimento prévio da seguinte estrutura:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<formSetRootTag>
 <form1>
  <field>field value1</field>
  <form1field>value1</form1field>
 </form1>
 <form2>
  <field>field value2</field>
  <form2field>value2</form2field>
 </form2>
 <form3>
  <field>field value3</field>
  <form3field>value3</form3field>
 </form3>
</formSetRootTag>
```

Em um conjunto de formulários, o XML definiu um schema XML com a seguinte sintaxe:

```xml
<formset>
 <fs_data>
  <xdp:xdp xmlns:xdp="https://ns.adobe.com/xdp/">
  <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
   <xfa:data>
   <rootElement>
    ... data ....
   </rootElement>
   </xfa:data>
  </xfa:datasets>
  </xdp:xdp>
 </fs_data>
 <fs_draft>
  ... private data...
 </fs_draft>
</formset>
```

>[!NOTE]
>
>Se houver dois formulários com raízes de dados sobrepostas, ou a hierarquia de elementos de um formulário se sobrepuser à hierarquia de raiz de dados de outro formulário, no xml de preenchimento prévio, os valores dos elementos sobrepostos serão unidos. O XML de envio tem estrutura semelhante ao XML de preenchimento prévio, mas o XML de envio tem mais tags de invólucro e algumas tags de dados de contexto de conjunto de formulários anexadas no final.

### Preencher descrição dos elementos XML {#prefill-xml-elements-description}

Regras de sintaxe para criar um arquivo XML de preenchimento prévio:

* elementos principais: elemento(s) que pode ser seu pai, onde nulo indica que o elemento pode estar na raiz do XML.
* cardinalidade: representa o número de vezes que o elemento pode ser usado dentro de seu elemento pai.
* submitXML: indica se o elemento está sempre presente (P) ou opcional(O) no XML de envio.
* prefillXML: indica se o elemento é obrigatório(R) ou opcional(O) no XML de preenchimento prévio.
* crianças: indica quais elementos podem ser seus filhos.

### FORMSET {#formset}

`parent elements:`

`null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: fs_data`

O elemento raiz do conjunto de formulários XML. É recomendável não usar essa palavra como o nome do rootSubform de qualquer formulário no conjunto de formulários.

### FS_DATA {#fs-data}

`parent elements:`

`formset`

cardinalidade: [1]

submitXML: P

prefillXML: O

`children: xdp:xdp/rootElement`

A subárvore indica os dados dos formulários no conjunto de formulários. O elemento é opcional no XML de preenchimento prévio somente se o elemento do conjunto de formulários não estiver presente

### XDP:XDP {#xdp-xdp}

`parent elements: fs_data/null`

`cardinality: [0,1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:datasets`

Essa tag indica o start de HTML5 Form XML. Isso é adicionado no XML de envio se ele estiver presente no XML de preenchimento prévio ou se não houver um XML de preenchimento prévio. Essa tag pode ser removida do XML de preenchimento prévio.

### XFA:CONJUNTOS DE DADOS {#xfa-datasets}

`parent elements: xdp:xdp`

`cardinality: [1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:data`

### XFA:DADOS {#xfa-data}

`parent elements: xfa:datasets`

`cardinality: [1]`

`submitXML: O`

`prefillXML: O`

`children: rootElement`

### ROOTELEMENT {#rootelement}

`parent elements: xfa:datasets/fs_data/null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: controlled by the Forms in Form set`

O nome rootElement é apenas um espaço reservado. O nome real é escolhido a partir dos formulários usados no conjunto de formulários. A subárvore que start com rootElement contém os dados dos campos e subformulários dentro do Forms no conjunto de formulários. Há vários fatores que determinam a estrutura do rootElement e de seus filhos.

No XML de pré-preenchimento, essa tag é opcional, mas se estiver ausente, o XML inteiro será ignorado.

NOME DA MARCA DE ELEMENTO RAIZ

Se houver um elemento raiz no XML de preenchimento prévio, o nome desse elemento também será obtido no XML de envio. Nos casos em que não há um xml de preenchimento prévio, o nome do rootElement é o nome do Subformulário raiz do primeiro formulário no conjunto de formulários que tem uma propriedade dataRoot definida como &quot;/&quot;. Se esse formulário não existir, o nome rootElement será **fs_dummy_root**, que é uma palavra-chave reservada.

## Formulário definido no aplicativo AEM Forms {#formset-in-workspace-app}

O aplicativo AEM Forms permite que trabalhadores de campo sincronizem seus dispositivos móveis com um servidor AEM Forms e trabalhem em suas tarefas. O aplicativo funciona mesmo quando o dispositivo está offline, salvando dados localmente no dispositivo. Usando recursos de anotação, como fotografias, os trabalhadores de campo podem fornecer informações precisas para integrar-se aos processos comerciais.

<!-- Update link as it is a 404 - For more information on AEM Forms app, see [AEM Forms app overview](/help/forms/using/mobile-workspace-overview.md).-->

## Limitações conhecidas - padrões sem suporte total no conjunto de formulários {#known-limitations-patterns-not-fully-supported-in-form-set}

Os seguintes padrões de dados não são totalmente suportados no Conjunto de formulários:

<table>
 <tbody>
  <tr>
   <td><strong>O padrão não é totalmente compatível com o conjunto de formulários</strong></td>
   <td><strong>Exemplo</strong></td>
  </tr>
  <tr>
   <td>Tamanho de entrada e tamanho de padrão incompatíveis</td>
   <td><p>Quando pattern= num{z,zzz}</p> <p>E input=</p> <p>12 345 ou</p> <p>1,23</p> </td>
  </tr>
  <tr>
   <td>Padrões de cláusula de imagem com colchetes "(" ")"</td>
   <td>num{(zz,zzz)}</td>
  </tr>
  <tr>
   <td>Vários padrões de dados</td>
   <td>num{zz,zzz} | num{z,zzz,zzz}</td>
  </tr>
  <tr>
   <td>Padrões abreviados </td>
   <td><p>num.integer{},</p> <p>num.decimal{},</p> <p>num.percent{} ou</p> <p>num.currency{}</p> </td>
  </tr>
 </tbody>
</table>

