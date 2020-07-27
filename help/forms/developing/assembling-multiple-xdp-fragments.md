---
title: Montagem de vários fragmentos XDP
seo-title: Montagem de vários fragmentos XDP
description: 'null'
seo-description: 'null'
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1876'
ht-degree: 0%

---


# Montagem de vários fragmentos XDP{#assembling-multiple-xdp-fragments}

Você pode reunir vários fragmentos XDP em um único documento XDP. Por exemplo, considere fragmentos XDP nos quais cada arquivo XDP contenha um ou mais subformulários usados para criar um formulário de integridade. A ilustração a seguir mostra a visualização do outline (representa o arquivo tuc018_template_flow.xdp usado no start rápido *Montagem de vários fragmentos* XDP):

![am_am_pro](assets/am_am_forma.png)

A ilustração a seguir mostra a seção do paciente (representa o arquivo tuc018_contact.xdp usado no start rápido *Montagem de vários fragmentos* XDP):

![am_am_formb](assets/am_am_formb.png)

A ilustração a seguir mostra a seção de integridade do paciente (representa o arquivo tuc018_paciente.xdp usado no start rápido *Montagem de vários fragmentos* XDP):

![am_am_formc](assets/am_am_formc.png)

Este fragmento contém dois subformulários chamados *subPatientPhysical* e *subPatientHealth*. Ambos os subformulários são referenciados no documento DDX que é passado ao serviço Assembler. Usando o serviço Assembler, você pode combinar todos esses fragmentos XDP em um único documento XDP, como mostrado na ilustração a seguir.

![am_am_formd](assets/am_am_formd.png)

O seguinte documento DDX monta vários fragmentos XDP em um documento XDP.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <XDP result="tuc018result.xdp">
            <XDP source="tuc018_template_flowed.xdp">
             <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/>
            </XDP>
         </XDP>
 </DDX>
```

O documento DDX contém uma `result` tag XDP que especifica o nome do resultado. Nessa situação, o valor é `tuc018result.xdp`. Esse valor é referenciado na lógica do aplicativo usada para recuperar o documento XDP depois que o serviço Assembler retorna o resultado. Por exemplo, considere a seguinte lógica do aplicativo Java usada para recuperar o documento XDP montado (observe que o valor está em negrito):

```java
 //Iterate through the map object to retrieve the result XDP document
 for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
     // Retrieve the Map object’s value
     Map.Entry e = (Map.Entry)i.next();
     //Get the key name as specified in the
     //DDX document
     String keyName = (String)e.getKey();
     if (keyName.equalsIgnoreCase("tuc018result.xdp"))
                 {
         Object o = e.getValue();
         outDoc = (Document)o;
         //Save the result PDF file
         File myOutFile = new File("C:\\AssemblerResultXDP.xdp");
         outDoc.copyToFile(myOutFile);
     }
 }
```

A `XDP source` tag especifica o arquivo XDP que representa um documento XDP completo que pode ser usado como um container para adicionar fragmentos XDP ou como um de vários documentos que são anexados juntos em ordem. Nessa situação, o documento XDP é usado somente como um container (a primeira ilustração é mostrada na *Montagem de vários fragmentos* XDP). Ou seja, os outros arquivos XDP são colocados dentro do container XDP.

Para cada subformulário, é possível adicionar um `XDPContent` elemento (esse elemento é opcional). No exemplo acima, observe que há três subformulários: `subPatientContact`, `subPatientPhysical`e `subPatientHealth`. O `subPatientPhysical` subformulário e o `subPatientHealth` subformulário estão localizados no mesmo arquivo XDP, tuc018_paciente.xdp. O elemento de fragmento especifica o nome do subformulário, conforme definido no Designer.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para montar vários fragmentos XDP, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente do Montador de PDF.
1. Faça referência a um documento DDX existente.
1. Consulte os documentos XDP.
1. Defina as opções de tempo de execução.
1. Monte os vários documentos XDP.
1. Recupere o documento XDP montado.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se os AEM Forms forem implantados em JBoss)
* jbossall-client.jar (obrigatório se os AEM Forms forem implantados em JBoss)

**Criar um cliente de Montador de PDF**

Antes de executar programaticamente uma operação de Assembler, crie um cliente de serviço de Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para montar vários documentos XDP. Esse documento DDX deve conter `XDP result`, `XDP source`e `XDPContent` elementos.

**Referência aos documentos XDP**

Para montar vários documentos XDP, consulte todos os arquivos XDP usados para montar o documento XDP resultante. Verifique se o nome do subformulário contido no documento XDP referenciado pelo `source` atributo está especificado no `fragment` atributo. Um subformulário é definido no Designer. Por exemplo, considere o seguinte XML.

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

O subformulário chamado *subPatientContact* deve estar localizado no arquivo XDP chamado *tuc018_contact.xdp*.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando uma tarefa se um erro for encontrado.

**Montar os vários documentos XDP**

Para montar vários arquivos XDP, chame a `invokeDDX` operação. O serviço Assembler retorna o documento XDP montado dentro de um objeto de coleção.

**Recuperar o documento XDP montado**

Um documento XDP montado é retornado dentro de um objeto de coleção. Insira o objeto da coleção e salve o documento XDP como um arquivo XDP. Você também pode passar o documento XDP para outro serviço AEM Forms, como Saída.

**Consulte também:**

[Montar vários fragmentos XDP usando a API Java](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[Montar vários fragmentos XDP usando a API de serviço da Web](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[Criação de Documentos PDF usando fragmentos](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Montar vários fragmentos XDP usando a API Java {#assemble-multiple-xdp-fragments-using-the-java-api}

Montar vários fragmentos XDP usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente do Montador de PDF.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `AssemblerServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Faça referência a um documento DDX existente.

   * Crie um `java.io.FileInputStream` objeto que represente o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DX.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Consulte os documentos XDP.

   * Crie um `java.util.Map` objeto usado para armazenar documentos XDP de entrada usando um `HashMap` construtor.
   * Crie um `com.adobe.idp.Document` objeto e passe o `java.io.FileInputStream` objeto que contém o arquivo XDP de entrada (repita essa tarefa para cada arquivo XDP).
   * Adicione uma entrada ao `java.util.Map` objeto chamando seu `put` método e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do `source` elemento especificado no documento DDX (repita essa tarefa para cada arquivo XDP).
      * Um `com.adobe.idp.Document` objeto que contém o documento XDP que corresponde ao `source` elemento (repita essa tarefa para cada arquivo XDP).

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios chamando um método que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, chame o `AssemblerOptionSpec` método do `setFailOnError` objeto e passe `false`.

1. Monte os vários documentos XDP.

   Chame o `AssemblerServiceClient` método do `invokeDDX` objeto e passe os seguintes valores obrigatórios:

   * Um `com.adobe.idp.Document` objeto que representa o documento DX a ser usado
   * Um `java.util.Map` objeto que contém os arquivos XDP de entrada
   * Um `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log de trabalhos

   O `invokeDDX` método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém o documento XDP montado.

1. Recupere o documento XDP montado.

   Para obter o documento XDP montado, execute as seguintes ações:

   * Chame o `AssemblerResult` método do `getDocuments` objeto. Esse método retorna um `java.util.Map` objeto.
   * Iterar pelo `java.util.Map` objeto até encontrar o `com.adobe.idp.Document` objeto resultante.
   * Chame o método do `com.adobe.idp.Document` `copyToFile` objeto para extrair o documento XDP montado.

**Consulte também:**

[Montagem de Vários Fragmentos](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)XDP[Start Rápido (modo SOAP): Montagem de vários fragmentos XDP usando a API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)Java[Incluindo arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java AEM Forms[Configuração de propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montar vários fragmentos XDP usando a API de serviço da Web {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Monte vários fragmentos XDP usando a API de serviço do Assembler (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL ao definir uma referência de serviço:

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Crie um cliente do Montador de PDF.

   * Crie um `AssemblerServiceClient` objeto usando seu construtor padrão.
   * Crie um `AssemblerServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço de AEM Forms, como `https://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar o `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço.
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `AssemblerServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao `AssemblerServiceClient.ClientCredentials.UserName.UserName` campo.
      * Atribua o valor da senha correspondente ao `AssemblerServiceClient.ClientCredentials.UserName.Password`campo.
      * Atribua o valor `HttpClientCredentialType.Basic` constante ao `BasicHttpBindingSecurity.Transport.ClientCredentialType`campo.
      * Atribua o valor `BasicHttpSecurityMode.TransportCredentialOnly` constante ao `BasicHttpBindingSecurity.Security.Mode`campo.

1. Faça referência a um documento DDX existente.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento DDX.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento DX e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` objeto `Read` . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` objeto atribuindo sua `MTOM` propriedade ao conteúdo da matriz de bytes.

1. Consulte os documentos XDP.

   * Para cada arquivo XDP de entrada, crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o arquivo de entrada.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do arquivo de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` objeto `Read` . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Este objeto de coleção é usado para armazenar arquivos de entrada necessários para criar um documento XDP montado.
   * Para cada arquivo de entrada, crie um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Atribua um valor de string que representa o nome da chave ao campo do `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto `key` . Esse valor deve corresponder ao valor do elemento especificado no documento DX. (Execute esta tarefa para cada arquivo XDP de entrada.)
   * Atribua o `BLOB` objeto que armazena o arquivo de entrada ao `MyMapOf_xsd_string_To_xsd_anyType_Item` campo do `value` objeto. (Execute esta tarefa para cada arquivo XDP de entrada.)
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto ao `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o `MyMapOf_xsd_string_To_xsd_anyType` método do objeto `Add` e passe o `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Execute esta tarefa para cada documento XDP de entrada.)

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios, atribuindo um valor a um membro de dados que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, atribua `false` ao membro de `AssemblerOptionSpec` dados do objeto `failOnError` .

1. Monte os vários documentos XDP.

   Chame o método do `AssemblerServiceClient` objeto `invokeDDX` e passe os seguintes valores:

   * Um `BLOB` objeto que representa o documento DDX
   * O `MyMapOf_xsd_string_To_xsd_anyType` objeto que contém os arquivos necessários
   * Um `AssemblerOptionSpec` objeto que especifica opções de tempo de execução

   O `invokeDDX` método retorna um `AssemblerResult` objeto que contém os resultados da tarefa e quaisquer exceções que ocorreram.

1. Recupere o documento XDP montado.

   Para obter o documento XDP recém-criado, execute as seguintes ações:

   * Acesse o `AssemblerResult` campo do `documents` objeto, que é um `Map` objeto que contém os documentos PDF resultantes.
   * Iterar pelo `Map` objeto para obter cada documento resultante. Em seguida, converta o membro do storage `value` em um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando a propriedade do `BLOB` objeto `MTOM` . Isso retorna uma matriz de bytes que você pode gravar em um arquivo XDP.

**Consulte também:**

[Montagem de vários fragmentos](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)XDP[Chamando AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)