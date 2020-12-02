---
title: APIs para acessar instâncias de carta
seo-title: APIs para acessar instâncias de carta
description: Saiba como usar APIs para acessar instâncias de carta.
seo-description: Saiba como usar APIs para acessar instâncias de carta.
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---


# APIs para acessar instâncias de carta {#apis-to-access-letter-instances}

## Visão geral {#overview}

Usando a interface Criar correspondência do Gerenciamento de correspondência, é possível salvar rascunhos de instâncias de carta em andamento e há instâncias de carta enviadas.

O Gerenciamento de correspondência fornece APIs que podem ser usadas para criar a interface de listagem e trabalhar com instâncias de carta enviadas ou rascunhos. As APIs listas e abrem instâncias de carta enviada e de rascunho de um agente, para que o agente possa continuar trabalhando nas instâncias de rascunho ou carta enviada.

## A obter instâncias de carta {#fetching-letter-instances}

O Gerenciamento de correspondência expõe as APIs para buscar instâncias de carta pelo serviço LetterInstanceService.

| Método | Descrição |
|--- |--- |
| getAllLetterInstances | Obtém instâncias de carta com base no parâmetro de query de entrada. Para obter todas as instâncias de carta, passe o parâmetro do query como nulo. |
| getLetterInstance | Obtém a instância da carta especificada com base na ID da instância da carta. |
| letterInstanceExists | Verifica se uma LetterInstance existe pelo nome especificado. |

>[!NOTE]
>
>LetterInstanceService é um serviço OSGI e sua instância pode ser recuperada usando @Reference no Java
>Class ou sling.getService(LetterInstanceService). Classe ) em JSP.

### Usando getAllLetterInstances {#using-nbsp-getallletterinstances}

A API a seguir encontra as instâncias de carta com base no objeto de query (Enviado e Rascunho). Se o objeto query for nulo, retornará todas as instâncias de letra. Essa API retorna a lista de [objetos LetterInstanceVO](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html), que pode ser usada para extrair informações adicionais da instância da carta

**Sintaxe**:  `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>Parâmetro</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>query</td>
   <td>O parâmetro query é usado para localizar/filtrar a instância Carta. Aqui, o query suporta apenas os atributos/propriedades de nível superior do objeto. O query consiste em instruções e o "attributeName" usado no objeto Statement deve ser o nome da propriedade no objeto de instância Letter.<br /> </td>
  </tr>
 </tbody>
</table>

#### Exemplo 1: Encontre todas as instâncias de letras do tipo ENVIADO {#example-fetch-all-the-letter-instances-of-type-submitted}

O código a seguir retorna a lista de instâncias de carta enviadas. Para obter somente rascunhos, altere `LetterInstanceType.COMPLETE.name()` para `LetterInstanceType.DRAFT.name().`

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

#### Exemplo 2: todas as instâncias de letras enviadas por um usuário e o tipo de instância de letra é DRAFT {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

O código a seguir tem várias declarações no mesmo query para obter os resultados filtrados com base em critérios diferentes, como a instância de carta enviada (atributo enviado por) por um usuário e o tipo de letterInstanceType é DRAFT.

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

### Usando getLetterInstance {#using-nbsp-getletterinstance}

Procure a instância da carta identificada pela ID da instância da carta especificada. Retorna &quot;null se a id da instância não for correspondida.

**Sintaxe:** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### Verificando se a LetterInstance existe {#verifying-if-letterinstance-exist}

Verificar se existe uma Instância de Carta pelo nome fornecido

**Sintaxe**:  `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **Parâmetro** | **Descrição** |
|---|---|
| letterInstanceName | Nome da instância da carta que você deseja verificar se ela existe. |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## Instâncias de carta de abertura {#opening-letter-instances}

A Instância da carta pode ser do tipo Enviado ou Rascunho. A abertura dos dois tipos de instância de letras mostra comportamentos diferentes:

* No caso de instância da carta enviada, um PDF que representa a instância da carta será aberto. A instância de Carta Submetida persistiu no servidor também contém os dados XML e XDP processados, que podem ser usados para realizar e usar mais um caso como a criação de um PDF/A.
* No caso de instância da carta de rascunho, a interface de usuário para criação de correspondência é recarregada para o estado anterior exato como era durante o momento em que o rascunho foi criado

### Abrindo Instância de Carta de Rascunho  {#opening-draft-letter-instance-nbsp}

A interface do usuário CCR suporta o parâmetro cmLetterInstanceId, que pode ser usado para recarregar a letra.

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>Não é necessário especificar cmLetterId ou cmLetterName/State/Version ao recarregar uma correspondência, pois os dados enviados já contêm todos os detalhes sobre a correspondência que é recarregada. AleatórioNão é usado para evitar problemas de cache do navegador, você pode usar o carimbo de data e hora como um número aleatório.

### Abrindo instância de carta enviada {#opening-submitted-letter-instance}

O PDF enviado pode ser aberto diretamente usando a ID da instância da carta:

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
