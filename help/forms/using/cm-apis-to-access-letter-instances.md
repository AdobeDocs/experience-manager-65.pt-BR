---
title: APIs para acessar instâncias de cartas
description: Descubra APIs e use-as para acessar programaticamente instâncias de cartas no ambiente do AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: 9d43d9d4-5487-416c-b641-e807227ac056
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 1%

---

# APIs para acessar instâncias de cartas {#apis-to-access-letter-instances}

## Visão geral {#overview}

Usando a interface Criar correspondência do Gerenciamento de correspondências, você pode salvar rascunhos de instâncias de cartas em andamento e há instâncias de cartas enviadas.

O Gerenciamento de correspondências fornece APIs com as quais você pode criar a interface de listagem para trabalhar com instâncias de cartas enviadas ou rascunhos. As APIs listam e abrem instâncias de cartas de rascunho e enviadas de um agente, para que o agente possa continuar trabalhando nas instâncias de rascunho ou cartas enviadas.

## Buscando instâncias de cartas {#fetching-letter-instances}

O Gerenciamento de correspondências expõe as APIs para buscar instâncias de cartas por meio do serviço LetterInstanceService.

| Método | Descrição |
|--- |--- |
| getAllLetterInstances | Obtém instâncias de cartas com base no parâmetro de consulta de entrada. Para buscar todas as instâncias de cartas, passe o parâmetro de consulta como nulo. |
| getLetterInstance | Busca a ocorrência de carta especificada com base na ID da ocorrência de carta. |
| letterInstanceExists | Verifica se existe uma LetterInstance com o nome fornecido. |

>[!NOTE]
>
>LetterInstanceService é um serviço OSGI e sua instância pode ser recuperada usando @Reference em Java™
>Class ou sling.getService(LetterInstanceService). Class ) em JSP.

### Uso de getAllLetterInstances {#using-nbsp-getallletterinstances}

A API a seguir encontra as instâncias de correspondência com base no objeto de consulta (Enviado e Rascunho). Se o objeto de consulta for nulo, ele retornará todas as instâncias de letras. Esta API retorna uma lista de objetos [LetterInstanceVO](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html), que podem ser usados para extrair informações adicionais da instância de carta.

**Sintaxe**: `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>Parâmetro</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>query</td>
   <td>O parâmetro de consulta é usado para localizar/filtrar a instância de carta. Aqui, a consulta aceita somente atributos/propriedades de nível superior do objeto. A consulta consiste em instruções e o "attributeName" usado no objeto Statement deve ser o nome da propriedade no objeto Letter instance.<br /> </td>
  </tr>
 </tbody>
</table>

#### Exemplo 1: buscar todas as instâncias de correspondência do tipo ENVIADO {#example-fetch-all-the-letter-instances-of-type-submitted}

O código a seguir retorna a lista de ocorrências de cartas enviadas. Para obter somente rascunhos, altere o `LetterInstanceType.COMPLETE.name()` para `LetterInstanceType.DRAFT.name().`

```java
@Reference
LetterInstanceService letterInstanceService;
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

#### Exemplo 2: buscar todas as instâncias de cartas enviadas por um usuário e o tipo de instância de cartas é RASCUNHO {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

O código a seguir tem várias instruções na mesma consulta para obter os resultados filtrados com base em diferentes critérios, como instância de carta enviada (atributo enviado por) por um usuário e o tipo de letterInstanceType é DRAFT.

```java
@Reference
LetterInstanceService letterInstanceService;

String submittedBy = "tglodman";
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);

Statement statementForSubmittedBy = new Statement();
statementForSubmittedBy .setAttributeName("submittedby");
statementForSubmittedBy .setOperator(Operator.EQUALS);
statementForSubmittedBy .setAttributeValue(submittedBy);
query.addStatement(statementForSubmittedBy );
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

### Uso de getLetterInstance {#using-nbsp-getletterinstance}

Busque a ocorrência de carta identificada pela ID de ocorrência de carta fornecida. Ele retorna &quot;null&quot; se a ID da instância não for correspondente.

**Sintaxe:** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### Verificando se LetterInstance existe {#verifying-if-letterinstance-exist}

Verificar se existe uma Instância de Letra com o nome especificado

**Sintaxe**: `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **Parâmetro** | **Descrição** |
|---|---|
| letterInstanceName | Nome da ocorrência de carta que você deseja verificar se existe. |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## Abertura de instâncias de cartas {#opening-letter-instances}

A Instância da Carta pode ser do tipo Enviado ou Rascunho. A abertura de ambos os tipos de ocorrência de letra mostra comportamentos diferentes:

* Se houver uma ocorrência de carta enviada, um PDF que representa a ocorrência de carta será aberto. A instância de carta enviada persistida no servidor também contém o XML de dados e o XDP processado, que podem ser usados para realizar e personalizar ainda mais o uso de um caso, como a criação de um PDF/A.
* Se houver uma ocorrência de carta de Rascunho, a interface de criação de correspondência será recarregada para o estado anterior exato como estava durante o tempo em que o rascunho foi criado

### Abrindo Instância de Carta de Rascunho  {#opening-draft-letter-instance-nbsp}

A interface do CCR é compatível com o parâmetro cmLetterInstanceId, que pode ser usado para recarregar a carta.

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>Não é necessário especificar o cmLetterId ou cmLetterName/State/Version ao recarregar uma correspondência, pois os dados enviados já contêm todos os detalhes sobre a correspondência que é recarregada. RandomNo é usado para evitar problemas de cache no navegador. Você pode usar um carimbo de data e hora como um número aleatório.

### Abrindo instância de carta enviada {#opening-submitted-letter-instance}

O PDF enviado pode ser aberto diretamente usando a ID de ocorrência da correspondência:

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
