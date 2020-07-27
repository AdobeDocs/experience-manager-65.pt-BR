---
title: Listar formulários em uma página da Web usando APIs
seo-title: Listar formulários em uma página da Web usando APIs
description: query programaticamente o Gerenciador de Formulários para recuperar uma lista filtrada de formulários e exibir em suas próprias páginas da Web.
seo-description: query programaticamente o Gerenciador de Formulários para recuperar uma lista filtrada de formulários e exibir em suas próprias páginas da Web.
uuid: e51cb2d4-816f-4e6d-a081-51e4999b00ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 515ceaf6-c132-4e1a-b3c6-5d2c1ccffa7c
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 1%

---


# Listar formulários em uma página da Web usando APIs {#listing-forms-on-a-web-page-using-apis}

O AEM Forms fornece uma API de pesquisa baseada em REST que os desenvolvedores da Web podem usar para query e recuperação de um conjunto de formulários que atende aos critérios de pesquisa. Você pode usar APIs para pesquisar formulários com base em vários filtros. O objeto response contém atributos de formulário, propriedades e pontos finais de formulários.

Para pesquisar formulários usando a REST API, envie uma solicitação GET ao servidor com os parâmetros de query `https://'[server]:[port]'/libs/fd/fm/content/manage.json` descritos abaixo.

## Query parameters {#query-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>Nome do atributo<br /> </strong></td>
   <td><strong>Descrição<br /> </strong></td>
  </tr>
  <tr>
   <td>func<br /> </td>
   <td><p>Especifica a função a ser chamada. Para pesquisar formulários, defina o valor do <code>func </code>atributo como <code>searchForms</code>.</p> <p>Por exemplo, <code class="code">
       URLParameterBuilder entityBuilder=new URLParameterBuilder ();
       entityBuilder.add("func", "searchForms");</code></p> <p><strong>Observação:</strong> <em>Este parâmetro é obrigatório.</em><br /> </p> </td>
  </tr>
  <tr>
   <td>appPath<br /> </td>
   <td><p>Especifica o caminho do aplicativo para pesquisar formulários. Por padrão, o atributo appPath pesquisa todos os aplicativos disponíveis no nível do nó raiz.<br /> </p> <p>Você pode especificar vários caminhos de aplicativo em um único query de pesquisa. Separe vários caminhos com um caractere de barra vertical (|). </p> </td>
  </tr>
  <tr>
   <td>cutPoints<br /> </td>
   <td><p>Especifica as propriedades a serem buscadas com os ativos. Você pode usar asterisco (*) para buscar todas as propriedades de uma vez. Use o operador pipe (|) para especificar várias propriedades. </p> <p>Por exemplo, <code>cutPoints=propertyName1|propertyName2|propertyName3</code></p> <p><strong>Nota</strong>: </p>
    <ul>
     <li><em>Propriedades como id, caminho e nome são sempre buscadas. </em></li>
     <li><em>Cada ativo tem um conjunto diferente de propriedades. Propriedades como formUrl, pdfUrl e guideUrl não dependem do atributo cutpoints. Essas propriedades dependem do tipo de ativo e são buscadas de acordo. </em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>relation<br /> </td>
   <td>Especifica os ativos relacionados a serem obtidos junto com os resultados da pesquisa. Você pode escolher uma das seguintes opções para buscar ativos relacionados:
    <ul>
     <li><strong>NO_RELATION</strong>: Não buscar ativos relacionados.</li>
     <li><strong>IMEDIATO</strong>: Obtém ativos que estão diretamente relacionados aos resultados da pesquisa.</li>
     <li><strong>TUDO</strong>: Buscar ativos direta e indiretamente relacionados.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxSize</td>
   <td>Especifica o número máximo de formulários a serem buscados.</td>
  </tr>
  <tr>
   <td>deslocamento</td>
   <td>Especifica o número de formulários a serem ignorados do start.</td>
  </tr>
  <tr>
   <td>returnCount</td>
   <td>Especifica se os resultados da pesquisa que correspondem aos critérios especificados devem ou não ser retornados. </td>
  </tr>
  <tr>
   <td>demonstrativos</td>
   <td><p>Especifica a lista de instruções. Os query são executados na lista das declarações especificadas no formato JSON. </p> <p>Por exemplo,</p> <p><code class="code">JSONArray statementArray=new JSONArray();
       JSONObject statement=new JSONObject();
       statement.put("name", "title");
       statement.put("value", "SimpleSurveyAF");
       statement.put("operator", "EQ"); statementArray.put(statement);</code></p> <p>No exemplo acima, </p>
    <ul>
     <li><strong>name</strong>: especifica o nome da propriedade a ser pesquisada.</li>
     <li><strong>valor</strong>: especifica o valor da propriedade a ser pesquisada.</li>
     <li><strong>operador</strong>: especifica o operador a ser aplicado durante a pesquisa. Os seguintes operadores são suportados:
      <ul>
       <li>EQ - Igual a </li>
       <li>NEQ - Diferente de</li>
       <li>GT - Maior que</li>
       <li>LT - Menor que</li>
       <li>GTEQ - maior que ou igual a</li>
       <li>LTEQ - menor que ou igual a</li>
       <li>CONTAINS - A contém B se B faz parte de A</li>
       <li>FULLTEXT - Pesquisa de texto completo</li>
       <li>STARTSWITH - A start com B se B for a parte inicial de A</li>
       <li>ENDSWITH - A termina com B se B for a parte final de A</li>
       <li>LIKE - Implementa o operador LIKE</li>
       <li>AND - Combine várias declarações</li>
      </ul> <p><strong>Observação:</strong> <em>Os operadores GT, LT, GTEQ e LTEQ são aplicáveis para propriedades de tipo linear, como LONG, DUPLO e DATE.</em></p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>pedidos<br /> </td>
   <td><p>Especifica os critérios de ordem para os resultados da pesquisa. Os critérios são definidos no formato JSON. É possível classificar os resultados da pesquisa em mais de um campo. Os resultados são classificados na ordem à medida que os campos aparecem no query.</p> <p>Por exemplo,</p> <p>Para recuperar os resultados do query ordenados pela propriedade title na ordem crescente, adicione o seguinte parâmetro: </p> <p><code class="code">JSONArray orderingsArray=new JSONArray();
       JSONObject orderings=new JSONObject();
       orderings.put("name", "title");
       orderings.put("criteria", "ASC");
       orderingsArray.put(orderings);
       entityBuilder.add("orderings", orderingsArray.toString());</code></p>
    <ul>
     <li><strong>name</strong>: Especifica o nome da propriedade a ser usada para ordenar os resultados da pesquisa.</li>
     <li><strong>critérios</strong>: Especifica a ordem dos resultados. O atributo order aceita os seguintes valores:
      <ul>
       <li>ASC - Use o ASC para organizar os resultados na ordem crescente.<br /> </li>
       <li>DES - Use DES para organizar os resultados na ordem decrescente.</li>
      </ul> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>includeXdp</td>
   <td>Especifica se o conteúdo binário deve ser recuperado ou não. O <code>includeXdp</code> atributo é aplicável para ativos do tipo <code>FORM</code>, <code>PDFFORM</code>e <code>PRINTFORM</code>.</td>
  </tr>
  <tr>
   <td>assetType</td>
   <td>Especifica os tipos de ativos a serem recuperados de todos os ativos publicados. Use o operador pipe (|) para especificar vários tipos de ativos. Os tipos de ativos válidos são FORM, PDFFORM, PRINTFORM, RESOURCE e GUIA.</td>
  </tr>
 </tbody>
</table>

## Solicitação de amostra {#sample-request}

```json
func : searchForms
appPath : /content/dam/formsanddocuments/MyApplication23
cutPoints : title|description|author|status|creationDate|lastModifiedDate|activationDate|expiryDate|tags|allowedRenderFormat|formmodel
relation : NO_RELATION
includeXdp : false
maxSize : 10
offset : 0
returnCount : true
statements: [{"name":"name","value":"*Claim.xdp","operator":"CONTAINS"},
                {"name":"","value":"Expense","operator":"FULLTEXT"},
                {"name":"description","value":"ABCD*","operator":"CONTAINS"},
                {"name":"status","value":"false","operator":"EQ"},
                {"name":"lastModifiedDate","value":"01/09/2013","operator":"GTEQ"},
                {"name":"lastModifiedDate","value":"01/18/2013","operator":"LTEQ"}]
orderings:[{"name" :“lastModifiedDate“:”order”:”ASC”}]
```

## Amostra de resposta {#sample-response}

```json
[
{"resultCount":2},
    {"assetType":"FORM","name":"ExpenseClaim.xdp","id":"509fa2d5-e3c9-407b-b8dc-fa0ba08eb0ce",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDEFGIJK","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"5477a127-8bbf-4cec-8f81-2689e5cb4a15",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/Image.gif","resourceSize":0}],
       "status":false,"creationDate":1358429845623,"lastModifiedDate":1358429846771},
{"assetType":"FORM","name":"ExpenseClaim.xdp","id":"4312239b-b666-4d36-95bc-641b3a39ddd4",
       "path":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDefghijklm","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"118a2e3f-7097-4d8c-85d1-651306de284a",
       "path":"/content/dam/formsanddocuments/MyApplication23/Image.gif","resourceSize":0}],"status":false,
       "creationDate":1358429856690,"lastModifiedDate":1358430109023}
]
```

## Artigos relacionados

* [Ativar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md)
* [Criar página do portal de formulários](/help/forms/using/creating-form-portal-page.md)
* [Lista de formulários em uma página da Web usando APIs](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar componente Rascunhos e envios](/help/forms/using/draft-submission-component.md)
* [Personalizar o armazenamento de rascunhos e formulários enviados](/help/forms/using/draft-submission-component.md)
* [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md)
* [Personalização de modelos para componentes do portal de formulários](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introdução à publicação de formulários em um portal](/help/forms/using/introduction-publishing-forms.md)