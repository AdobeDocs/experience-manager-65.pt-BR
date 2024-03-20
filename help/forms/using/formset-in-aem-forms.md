---
title: Formulário definido no AEM Forms
description: Este artigo apresenta o conjunto de formulários e explica como criar conjuntos de formulários unindo formulários HTML5. Este artigo também explica como preencher previamente dados xml em um conjunto de formulários e como usar conjuntos de formulários no gerenciamento de processos.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms
exl-id: 039afdf3-013b-41b2-8821-664d28617f61
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2804'
ht-degree: 0%

---

# Formulário definido no AEM Forms{#form-set-in-aem-forms}

## Visão geral {#overview}

Os clientes geralmente precisam enviar vários formulários para solicitar um serviço ou benefício. Isso envolve encontrar todos os formulários relevantes e preenchê-los, enviá-los e rastreá-los separadamente. Além disso, eles são necessários para preencher detalhes comuns várias vezes em formulários. Todo o processo se torna complicado e sujeito a erros se envolve um grande número de formulários. O recurso de conjunto de formulários do AEM Forms pode ajudar a simplificar a experiência do usuário em tais cenários.

Um conjunto de formulários é uma coleção de formulários HTML5 agrupados e apresentados como um único conjunto de formulários para os usuários finais. Quando os usuários finais começam a preencher um conjunto de formulários, eles são perfeitamente transferidos de um formulário para outro. No final, eles podem enviar todos os formulários em apenas um clique.

O AEM Forms fornece aos autores de formulários uma interface de usuário intuitiva para criar, configurar e gerenciar conjuntos de formulários. Como autor, você pode solicitar formulários em uma sequência específica que os usuários finais devem seguir. Além disso, você pode aplicar condições ou expressões de qualificação em formulários individuais para controlar sua visibilidade com base nas entradas do usuário. Por exemplo, você pode configurar o formulário de detalhes do cônjuge para que apareça somente quando o estado civil especificar como Casado.

Além disso, você pode configurar campos comuns em diferentes formulários para compartilhar associações de dados comuns. Com vinculações de dados adequadas em vigor, os usuários finais precisam preencher informações comuns apenas uma vez que forem preenchidas automaticamente em formulários subsequentes.

Os conjuntos de formulários também são compatíveis com o aplicativo AEM Forms, permitindo que a força de trabalho de campo coloque um conjunto de formulários offline, visite clientes, insira dados e sincronize posteriormente com o servidor do AEM Forms para enviar dados de formulários para processos de negócios.

## Criação e gerenciamento de conjunto de formulários {#creating-and-managing-form-set}

Você pode associar vários XDPs ou Modelos de formulário, criados usando o Designer, em um conjunto de formulários. Os conjuntos de formulários podem ser usados para renderizar seletivamente os XDPs com base nos valores inseridos pelos usuários nos formulários iniciais e em seus perfis.

Uso [Interface do usuário do AEM Forms](../../forms/using/introduction-managing-forms.md) para gerenciar todos os formulários, conjuntos de formulários e ativos relacionados.

### Criar um conjunto de formulários {#create-a-form-set}

Para criar um conjunto de formulários, faça o seguinte:

1. Selecione Forms > Forms e Documentos.
1. Selecione Criar > Conjunto de formulários.

1. Na página Adicionar propriedades, adicione os seguintes detalhes e clique em Próximo.

   * Título: especifica o título do documento. O título ajuda a identificar o conjunto de formulários na interface do usuário do AEM Forms.
   * Descrição: Especifica as informações detalhadas sobre o documento.
   * Tags: especifica tags para identificar exclusivamente o conjunto de formulários. Ajuda das tags na pesquisa do conjunto de formulários. Para criar tags, digite novos nomes de tag na caixa Tags.
   * Enviar URL: especifica o URL no qual os dados enviados são publicados para o caso de representação independente do conjunto de formulários (caso de uso de aplicativo não-AEM Forms). Os dados são enviados para esse endpoint como multipart/formdata com o seguinte parâmetro de solicitação:
   * dataXML: esse parâmetro contém uma representação XML dos dados enviados do conjunto de formulários. Se todos os formulários no conjunto de formulários usarem um esquema comum, o XML será gerado de acordo com esse esquema. Caso contrário, a tag raiz XML contém uma tag secundária para cada formulário preenchido no conjunto de formulários que contém dados para os anexos do formulário.
   * formsetPath: o caminho do conjunto de formulários no CRXDE, que foi enviado.
   * Perfil de renderização do HTML: você pode configurar determinadas opções, como campos flutuantes, anexos e suporte a rascunhos (para representação independente do conjunto de formulários) para personalizar a aparência, o comportamento e as interações do conjunto de formulários. É possível personalizar ou estender o perfil existente para alterar qualquer configuração de perfil do HTML Form.

   ![Conjunto de formulários: adicionar propriedades](assets/createformset1.png)

1. A tela Selecionar formulário(s) exibe os formulários XDP ou arquivos XDP disponíveis. Pesquise e selecione os formulários a serem incluídos no conjunto de formulários e clique em Adicionar ao conjunto de formulários. Se necessário, pesquise novamente os formulários a serem adicionados. Depois de adicionar todos os formulários ao conjunto de formulários, clique em Avançar.

   >[!NOTE]
   >
   >Verifique se os nomes de campo nos formulários XDP não contêm o caractere de ponto. Caso contrário, os scripts que tentarem resolver os campos, que têm caracteres de ponto, não poderão resolvê-los.

1. Na página Configurar formulário(s), você pode fazer o seguinte:

   * Ordem dos formulários: arraste e solte os formulários para reorganizá-los. A ordem do formulário define a ordem em que os formulários são mostrados ao usuário final no aplicativo AEM Forms e na representação independente.
   * Identificador de formulário: especifica uma identidade exclusiva para os formulários a serem usados em expressões de qualificação.
   * Raiz de dados: para cada formulário no conjunto de formulários, o Autor pode configurar o XPATH onde os dados desse formulário específico estão posicionados no XML enviado. Por padrão, o valor é /. Se todos os formulários no conjunto de formulários estiverem vinculados a um esquema e compartilharem o mesmo esquema XML, você poderá alterar esse valor. Recomenda-se que cada campo no formulário tenha a vinculação de dados adequada especificada no XDP. Se dois campos em dois formulários diferentes compartilharem a associação de dados comum, o campo no segundo formulário mostrará valores preenchidos previamente do primeiro formulário. Não vincule dois subformulários com o mesmo conteúdo interno ao mesmo nó XML. Para obter mais informações sobre a estrutura XML do conjunto de formulários, consulte [Preencher previamente XML para o conjunto de formulários](../../forms/using/formset-in-aem-forms.md#p-prefill-xml-for-form-set-p).
   * Expressão de elegibilidade: especifica uma expressão JavaScript que avalia um valor booleano e indica se um formulário no conjunto de formulários é elegível para preenchimento. Se falso, o usuário não será solicitado ou nem receberá o formulário para preencher. Normalmente, a expressão é baseada nos valores dos campos capturados antes desse formulário. As expressões também contêm chamadas para o conjunto de formulários API fs.valueOf para extrair os valores preenchidos pelo usuário em um campo de um formulário do conjunto de formulários:

   *fs.valueOf()&lt;form identifier=&quot;&quot;>, &lt;fieldsom expression=&quot;&quot;>) > &lt;value>*

   Por exemplo, se você tiver dois formulários no conjunto de formulários: despesa de negócios e despesa de viagem, é possível adicionar um trecho JavaScript no campo Expressão de elegibilidade para ambos os formulários para verificar a entrada do usuário para o tipo de despesa em um formulário. Se o usuário escolher Despesa Comercial, o formulário Despesa Comercial é renderizado para o usuário final. Ou se o usuário escolher despesas de viagem, um formulário diferente será renderizado para o usuário final. Para obter mais informações, consulte Expressão de qualificação.

   Além disso, o Autor também pode optar por remover um formulário do conjunto de formulários usando o ícone Excluir presente no canto direito de cada linha ou adicionar outro conjunto de formulários usando o caractere &#39;**+**&#39; na barra de ferramentas. Este &#39;**+** O ícone &quot; direciona o usuário de volta à etapa anterior do assistente, que foi usada para &quot;Selecionar formulário(s)&quot;. As seleções existentes são mantidas e qualquer seleção adicional feita deve ser adicionada ao conjunto de formulários usando o ícone Adicionar ao conjunto de formulários nessa página.

   ![Conjunto de formulários: configurar formulário (s)](assets/createformset2.png)

   >[!NOTE]
   >
   >Todos os formulários usados no conjunto de formulários são gerenciados pela interface do usuário do AEM Forms.

### Gerenciamento de um conjunto de formulários {#managing-a-form-set}

Depois que um conjunto de formulários é criado, você pode executar as seguintes ações nesse conjunto de formulários:

* Clique uma vez: quando o conjunto de formulários é criado e listado na página principal do ativo, você pode clicar uma vez no conjunto de formulários para visualizá-lo. Um conjunto de formulários é aberto e exibe todos os modelos de formulário (XDPs) nesse conjunto de formulários.
* Editar: ao clicar em Editar após selecionar um conjunto de formulários, a tela Configurar formulário (s) mostrada acima em Etapas para criar um conjunto de formulários é aberta. Você pode executar todas as funcionalidades descritas nesse ponto.
* Copiar + Colar: permite copiar todo o conjunto de formulários de um local e colá-lo no mesmo local ou em qualquer outro local ou pasta.
* Download: é possível baixar o conjunto de formulários com todas as suas dependências.
* Iniciar/Gerenciar revisão: uma vez criado o conjunto de formulários, você pode configurar sua revisão clicando em Iniciar revisão. Depois que a revisão de um conjunto de formulários for iniciada, a opção Gerenciar revisão será exibida para o usuário. Na tela Gerenciar revisão, você pode atualizar/encerrar a revisão. Para as revisões adicionadas, é possível verificar a revisão e adicionar comentários, se necessário.
* Excluir: exclui o conjunto completo de formulários. Os formulários no conjunto de formulários excluído permanecem no repositório.
* Publicar/Desfazer publicação: publica/desfaz a publicação do conjunto de formulários juntamente com todos os formulários que ele contém e os ativos relacionados desses formulários.
* Pré-visualização: A pré-visualização fornece duas opções: Pré-visualização como HTML (sem dados) e pré-visualização personalizada com dados de amostra.
* Exibir/editar propriedades: é possível exibir/editar as propriedades de metadados de um conjunto de formulários selecionado.

![createformset3](assets/createformset3.png)

### Editar um conjunto de formulários {#edit-a-form-set}

Para editar um conjunto de formulários, faça o seguinte:

1. Selecione Forms > Forms e Documentos.
1. Localize o conjunto de formulários que deseja editar. Passe o mouse sobre ele e selecione Editar ( ![editicon](assets/editicon.png)).
1. Na página Configurar formulário(s), você pode editar o seguinte:

   * Pedido de formulários
   * Identificador de formulário
   * Raiz de dados
   * Expressão de qualificação

   Você também pode clicar no ícone Excluir relevante para excluir o formulário do conjunto de formulários.

## Conjunto de formulários no Gerenciamento de processos {#form-set-in-process-management}

Depois de criar um conjunto de formulários usando a interface do usuário do AEM Forms Management, você pode usar o conjunto de formulários em um Ponto Inicial ou na atividade Atribuir Tarefa usando a Bancada.

### Usando o conjunto de formulários na Tarefa ou no ponto inicial {#using-form-set-in-task-or-start-point}

1. Ao projetar um processo, na seção Apresentação e dados de Atribuir tarefa/Ponto inicial, selecione **usar um ativo CRX**. O navegador CRX Asset é exibido.

   ![Criar um processo: usar um ativo CRX](assets/formsetinprocessmgmt1.png)

1. Selecione o conjunto de formulários para filtrar o conjunto de formulários no repositório AEM (CRX).

   ![Criar um processo: caixa de diálogo Selecionar ativo de formulário](assets/formsetinprocessmgmt2.png)

1. Selecione um conjunto de formulários e clique em OK.

## Expressões de qualificação {#eligibility-expressions}

As expressões de qualificação em um conjunto de formulários são usadas para definir e controlar dinamicamente os formulários exibidos para um usuário. Por exemplo, para exibir um formulário específico somente se o usuário pertencer a uma faixa etária específica. Especifique e edite uma expressão de qualificação usando o gerenciador de formulários.

Uma expressão de elegibilidade pode ser qualquer instrução JavaScript válida que retorne um valor booleano. A última instrução no trecho de código JavaScript é tratada como um valor booleano que determina a qualificação do formulário com base no processamento no restante (linhas anteriores) do trecho de código JavaScript. Se o valor da expressão for true, o formulário estará qualificado para ser exibido ao usuário. Tais formulários são conhecidos como formulários elegíveis.

>[!NOTE]
>
>A expressão de qualificação para o primeiro formulário no conjunto de formulários não é executada. O primeiro formulário é sempre exibido independentemente da sua expressão de qualificação.

Além das funções JavaScript padrão, o conjunto de formulários também expõe a API fs.valueOf que fornece acesso ao valor de um campo de um formulário em um conjunto de formulários. Use esta API para acessar o valor de um campo de formulário em um conjunto de formulários. A sintaxe da API é fs.valueOf (formUid, fieldSOM), onde:

* formUid (string): uma ID exclusiva de um formulário no conjunto de formulários. Você pode especificá-lo ao criar o conjunto de formulários na interface do usuário do gerenciador de formulários. Por padrão, é o nome do formulário.
* fieldSOM (string): uma expressão SOM do campo no formulário especificado por formUid. A expressão SOM ou a expressão Modelo de Objeto de Script é usada para fazer referência a valores, propriedades e métodos em um modelo de objeto de documento (DOM) específico. Você pode exibi-lo no Designer de formulários na guia Scripts enquanto o campo estiver selecionado.

>[!NOTE]
>
>Os parâmetros formUid e fieldSOM devem ser literais de cadeia de caracteres.

### Exemplos {#examples}

Uso válido da API:

`fs.valueOf("form1", "xfa.form.form1.subform1.field1")`

Uso inválido da API:

```javascript
var formUid = "form1";
 var fieldSOM = "xfa.form.form1.subform1.field1"; fs.valueOf(formUid, fieldSOM);
```

## Preencher previamente XML para o conjunto de formulários {#prefill-xml-for-form-set}

O conjunto de formulários é uma coleção de vários formulários HTML5 que têm esquemas comuns ou diferentes. O conjunto de formulários suporta o pré-preenchimento de campos de formulário usando um arquivo XML. Você pode associar um arquivo XML a um conjunto de formulários, de modo que, ao abrir um formulário no conjunto de formulários, alguns dos campos no formulário sejam pré-preenchidos.

O arquivo XML de preenchimento prévio é especificado usando o parâmetro dataRef da URL do conjunto de formulários. O parâmetro dataRef especifica o caminho absoluto do arquivo XML de dados mesclado com o conjunto de formulários.

Por exemplo, você tem três formulários (formulário1, formulário2 e formulário3), no conjunto de formulários com a seguinte estrutura:

formulário1

campo formulário1campo

formulário2

campo formulário2campo

formulário3

campo formulário3campo

Cada formulário tem um campo nomeado comum, chamado &quot;campo&quot;, e um campo nomeado exclusivamente chamado &quot;formfield&quot;.

É possível preencher previamente esse conjunto de formulários usando um XML com a seguinte estrutura:

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
>A marca raiz XML pode ter qualquer nome, mas as marcas de elemento correspondentes aos campos devem ter o mesmo nome que o campo. A hierarquia do XML deve imitar a hierarquia do formulário, o que significa que o XML deve ter tags correspondentes para quebrar subformulários.

O trecho XML acima mostra que o XML de preenchimento prévio do conjunto de formulários é uma união dos trechos XML de preenchimento prévio dos formulários individuais. Se determinados campos nos diferentes formulários tiverem hierarquia/esquema de dados semelhantes entre si, os campos serão pré-preenchidos com os mesmos valores. Neste exemplo, todos os três formulários são preenchidos previamente com o mesmo valor para o campo comum, &quot;campo&quot;. Essa é uma maneira simples de transportar dados de um formulário para o próximo. Isso também pode ser feito vinculando os campos ao mesmo schema ou referência de dados. Se quiser segregar os dados do conjunto de formulários com base no schema dos formulários. Isso pode ser feito especificando o atributo &quot;raiz de dados&quot; do formulário, durante a criação do conjunto de formulários (o valor padrão é &quot;/&quot;, que mapeia para a tag raiz do conjunto de formulários).

No exemplo anterior, se você especificar as raízes de dados: &quot;/form1&quot;, &quot;/form2&quot; e &quot;/form3&quot; respectivamente para os três formulários, será necessário usar um XML de preenchimento prévio da seguinte estrutura:

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

Em um conjunto de formulários, o XML definiu um esquema XML com a seguinte sintaxe:

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
>Se houver dois formulários com raízes de dados sobrepostas ou a hierarquia de elementos de um formulário se sobrepor à hierarquia raiz de dados de outro formulário, no xml de preenchimento prévio, os valores dos elementos sobrepostos serão mesclados. O XML de envio tem uma estrutura semelhante ao XML de preenchimento prévio, mas o XML de envio tem mais tags wrapper e algumas tags de dados de contexto de conjunto de formulários foram anexadas no final.

### Preencher previamente a descrição dos elementos XML {#prefill-xml-elements-description}

Regras de sintaxe para criar um arquivo XML de preenchimento prévio:

* parent elements: elemento(s) que pode(m) ser seu(s) pai, em que null indica que o elemento pode estar na raiz do XML.
* cardinalidade: representa o número de vezes que o elemento pode ser usado dentro do elemento principal.
* submitXML: indica se o elemento está sempre presente (P) ou é opcional (O) no XML de envio.
* prefillXML: indica se o elemento é obrigatório(R) ou opcional(O) no XML de preenchimento prévio.
* filhos: indica quais elementos podem ser seus filhos.

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

A subárvore indica os dados dos formulários no conjunto de formulários. O elemento é opcional no XML de preenchimento prévio somente se o elemento de conjunto de formulários não estiver presente

### XDP:XDP {#xdp-xdp}

`parent elements: fs_data/null`

`cardinality: [0,1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:datasets`

Essa tag indica o início do formulário XML HTML5. Isso é adicionado no XML de envio se estiver presente no XML de preenchimento prévio ou se não houver XML de preenchimento prévio. Essa tag pode ser removida do XML de preenchimento prévio.

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

O nome rootElement é apenas um espaço reservado. O nome real é separado dos formulários usados no conjunto de formulários. A subárvore que começa com rootElement contém os dados dos campos e subformulários dentro do Forms no conjunto de formulários. Há vários fatores que determinam a estrutura do rootElement e seus filhos.

No XML pré-preenchido, essa tag é opcional, mas se estiver ausente, o XML inteiro será ignorado.

NOME DA TAG DO ELEMENTO RAIZ

Caso haja um elemento raiz no XML de preenchimento prévio, o nome desse elemento também será usado no XML de envio. Nos casos em que não há xml de preenchimento prévio, o nome do rootElement é o nome do Subformulário raiz do primeiro formulário no conjunto de formulários que tem uma propriedade dataRoot definida como &quot;/&quot;. Se não houver tal formulário, o nome do rootElement será **fs_dummy_root**, que é uma palavra-chave reservada.

## Formulário definido no aplicativo AEM Forms {#formset-in-workspace-app}

O aplicativo AEM Forms permite que os funcionários de campo sincronizem seus dispositivos móveis com um servidor AEM Forms e trabalhem em suas tarefas. O aplicativo funciona mesmo quando o dispositivo está offline, salvando os dados localmente no dispositivo. Usando recursos de anotação, como fotografias, os trabalhadores de campo podem fornecer informações precisas para integrar aos processos de negócios.

<!-- Update link as it is a 404 - For more information on AEM Forms app, see [AEM Forms app overview](/help/forms/using/mobile-workspace-overview.md).-->

## Limitações conhecidas: padrões não totalmente compatíveis no conjunto de formulários {#known-limitations-patterns-not-fully-supported-in-form-set}

Os seguintes padrões de dados não são totalmente compatíveis com o conjunto de formulários:

<table>
 <tbody>
  <tr>
   <td><strong>Padrão não totalmente compatível no conjunto de formulários</strong></td>
   <td><strong>Exemplo</strong></td>
  </tr>
  <tr>
   <td>Incompatibilidade de tamanho de entrada e tamanho de padrão</td>
   <td><p>Quando pattern= num{z,zzz}</p> <p>E input=</p> <p>12,345 ou</p> <p>1,23</p> </td>
  </tr>
  <tr>
   <td>Padrões de Cláusula de Imagem com colchetes "(" ")"</td>
   <td>num{(zz,zzz)}</td>
  </tr>
  <tr>
   <td>Vários padrões de dados</td>
   <td>num{zz,zzz} | num{z,zzz,zzz}</td>
  </tr>
  <tr>
   <td>Padrões curtos </td>
   <td><p>num.integer{},</p> <p>num.decimal{},</p> <p>num.percent{}ou</p> <p>num.currency{}</p> </td>
  </tr>
 </tbody>
</table>
