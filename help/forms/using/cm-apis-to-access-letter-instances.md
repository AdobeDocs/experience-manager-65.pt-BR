---
title: APIs para acessar instâncias de cartas
seo-title: APIs para acessar instâncias de cartas
description: Saiba como usar APIs para acessar instâncias de carta.
seo-description: Saiba como usar APIs para acessar instâncias de carta.
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
feature: Gerenciamento de correspondência
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---


# APIs para acessar instâncias de carta {#apis-to-access-letter-instances}

## Visão geral {#overview}

Usando a interface Criar correspondência do gerenciamento de correspondência, é possível salvar rascunhos de instâncias de carta em andamento e há instâncias de carta enviadas.

O Gerenciamento de correspondência fornece APIs usando as quais você pode criar a interface de listagem para trabalhar com instâncias ou rascunhos de cartas enviadas. As APIs listam e abrem instâncias de carta enviadas e de rascunho de um agente, para que o agente possa continuar trabalhando nas instâncias de rascunho ou de carta enviada.

## Buscando instâncias de carta {#fetching-letter-instances}

O Gerenciamento de correspondência expõe APIs para buscar instâncias de carta por meio do serviço LetterInstanceService.

| Método | Descrição |
|--- |--- |
| getAllLetterInstances | Busca instâncias de carta com base no parâmetro de consulta de entrada. Para buscar todas as instâncias de letra, passe o parâmetro de consulta como nulo. |
| getLetterInstance | Busca a instância de letra especificada com base na ID da instância de letra. |
| letterInstanceExists | Verifica se uma LetterInstance existe pelo nome fornecido. |

>[!NOTE]
>
>O LetterInstanceService é um serviço OSGI e sua instância pode ser recuperada usando @Reference no Java
>Classe ou sling.getService(LetterInstanceService). Classe ) no JSP.

### Uso de getAllLetterInstances {#using-nbsp-getallletterinstances}

A API a seguir encontra as instâncias de carta com base no objeto de consulta (Enviado e Rascunho). Se o objeto de consulta for nulo, retornará todas as instâncias de letra. Essa API retorna a lista de objetos [LetterInstanceVO](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html), que podem ser usados para extrair informações adicionais da instância de letra

**Sintaxe**:  `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>Parâmetro</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>query</td>
   <td>O parâmetro de consulta é usado para localizar/filtrar a instância da Carta. Aqui a consulta suporta apenas atributos/propriedades de nível superior do objeto. A consulta consiste em instruções e o "attributeName" usado no objeto Instrução deve ser o nome da propriedade no objeto de instância Letter.<br /> </td>
  </tr>
 </tbody>
</table>

#### Exemplo 1: Buscar todas as instâncias de letra do tipo ENVIADO {#example-fetch-all-the-letter-instances-of-type-submitted}

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

#### Exemplo 2: buscar todas as instâncias de carta enviadas por um usuário e o tipo de instância de carta é DRAFT {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

O código a seguir tem várias instruções na mesma query para obter os resultados filtrados com base em critérios diferentes, como a instância de carta enviada (atributo enviado por) por um usuário e o tipo de letterInstanceType é DRAFT.

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

Busque a instância da carta identificada pela id de instância da carta fornecida. Retorna &quot;null se a ID da instância não corresponder.

**Sintaxe:** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### Verificando se a LetterInstance existe {#verifying-if-letterinstance-exist}

Verifique se existe uma Instância de Carta com o nome especificado

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

## A abrir instâncias de carta {#opening-letter-instances}

A Instância da Carta pode ser do tipo Enviado ou Rascunho. Abrir ambos os tipos de instância de letra mostra comportamentos diferentes:

* No caso de instância de carta enviada, um PDF que representa a instância de carta é aberto. A instância da Carta Enviada persistente no servidor também contém o dataXML &amp; processado XDP, que pode ser usado para realizar e personalizar ainda mais um caso, como criar um PDF/A.
* No caso de instância de carta de rascunho, a interface do usuário de criação de correspondência é recarregada para o estado anterior exato, como durante o momento em que o rascunho foi criado

### Abrindo Instância de Carta de Rascunho  {#opening-draft-letter-instance-nbsp}

A interface do usuário do CCR é compatível com o parâmetro cmLetterInstanceId, que pode ser usado para recarregar a letra.

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>Não é necessário especificar o cmLetterId ou cmLetterName/State/Version ao recarregar uma correspondência, pois os dados enviados já contêm todos os detalhes sobre a correspondência recarregada. RandomNo é usado para evitar problemas de cache do navegador, você pode usar o carimbo de data e hora como um número aleatório.

### Abrindo instância de carta enviada {#opening-submitted-letter-instance}

O PDF enviado pode ser aberto diretamente usando a ID da instância da carta:

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
