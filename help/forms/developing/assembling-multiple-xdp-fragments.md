---
title: Montagem de vários fragmentos XDP
seo-title: Assembling Multiple XDP Fragments
description: Monte vários fragmentos XDP em um único documento XDP usando a API do Java e a API do serviço da Web.
seo-description: Assemble multiple XDP fragments into a single XDP document using the Java API and Web Service API.
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
role: Developer
exl-id: 54d98c69-2b2e-46cb-9f6a-7e9bdbe5c378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 0%

---

# Montagem de vários fragmentos XDP{#assembling-multiple-xdp-fragments}

Você pode reunir vários fragmentos XDP em um único documento XDP. Por exemplo, considere fragmentos XDP em que cada arquivo XDP contém um ou mais subformulários usados para criar um formulário de integridade. A ilustração a seguir mostra a exibição de estrutura (representa o arquivo tuc018_template_flowed.xdp usado na variável *Montagem de vários fragmentos XDP* início rápido):

![am_am_format](assets/am_am_forma.png)

A ilustração a seguir mostra a seção do paciente (representa o arquivo tuc018_contact.xdp usado no *Montagem de vários fragmentos XDP* início rápido):

![am_am_formb](assets/am_am_formb.png)

A ilustração a seguir mostra a seção de saúde do paciente (representa o arquivo tuc018_paciente.xdp usado no *Montagem de vários fragmentos XDP* início rápido):

![am_am_formc](assets/am_am_formc.png)

Esse fragmento contém dois subformulários nomeados *subPacienteFísico* e *subPatientHealth*. Ambos os subformulários são referenciados no documento DDX que é passado para o serviço Assembler. Usando o serviço Assembler, você pode combinar todos esses fragmentos XDP em um único documento XDP, conforme mostrado na ilustração a seguir.

![am_am_formd](assets/am_am_formd.png)

O documento DDX a seguir monta vários fragmentos XDP em um documento XDP.

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

O documento DDX contém um XDP `result` que especifica o nome do resultado. Nessa situação, o valor é `tuc018result.xdp`. Esse valor é referenciado na lógica do aplicativo usada para recuperar o documento XDP depois que o serviço Assembler retorna o resultado. Por exemplo, considere a seguinte lógica de aplicativo Java usada para recuperar o documento XDP montado (observe que o valor está em negrito):

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

O `XDP source` especifica o arquivo XDP que representa um documento XDP completo que pode ser usado como um container para adicionar fragmentos XDP ou como um de vários documentos que são anexados juntos em ordem. Nessa situação, o documento XDP é usado somente como um contêiner (a primeira ilustração mostrada em *Montagem de vários fragmentos XDP*). Ou seja, os outros arquivos XDP são colocados no contêiner XDP.

Para cada subformulário, é possível adicionar um `XDPContent` (esse elemento é opcional). No exemplo acima, observe que há três subformulários: `subPatientContact`, `subPatientPhysical`e `subPatientHealth`. Ambos os `subPatientPhysical` e o `subPatientHealth` subformulários estão localizados no mesmo arquivo XDP, tuc018_paciente.xdp. O elemento do fragmento especifica o nome do subformulário, conforme definido no Designer.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para montar vários fragmentos XDP, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um cliente Assembler PDF.
1. Faça referência a um documento DDX existente.
1. Faça referência aos documentos XDP.
1. Defina as opções de tempo de execução.
1. Monte os vários documentos XDP.
1. Recupere o documento XDP montado.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

**Criar um cliente do Assembler do PDF**

Antes de executar programaticamente uma operação Assembler, crie um cliente de serviço Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para reunir vários documentos XDP. Este documento DDX deve conter `XDP result`, `XDP source`e `XDPContent` elementos.

**Referência aos documentos XDP**

Para montar vários documentos XDP, faça referência a todos os arquivos XDP usados para montar o documento XDP resultante. Certifique-se de que o nome do subformulário contido no documento XDP referenciado pelo `source` é especificado na variável `fragment` atributo. Um subformulário é definido no Designer. Por exemplo, considere o seguinte XML.

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

O subformulário nomeado *subPacientContact* deve estar localizado no arquivo XDP chamado *tuc018_contact.xdp*.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrua o serviço Assembler a continuar processando um trabalho se um erro for encontrado.

**Montar os vários documentos XDP**

Para reunir vários arquivos XDP, chame a função `invokeDDX` operação. O serviço Assembler retorna o documento XDP montado em um objeto de coleção.

**Recuperar o documento XDP montado**

Um documento XDP montado é retornado em um objeto de coleção. Itere pelo objeto de coleção e salve o documento XDP como um arquivo XDP. Você também pode passar o documento XDP para outro serviço da AEM Forms, como Saída.

**Consulte também**

[Monte vários fragmentos XDP usando a API Java](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[Montar vários fragmentos XDP usando a API do serviço da Web](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[Criação de documentos do PDF usando fragmentos](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Monte vários fragmentos XDP usando a API Java {#assemble-multiple-xdp-fragments-using-the-java-api}

Monte vários fragmentos XDP usando a API do Serviço de Assembler (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente Assembler PDF.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `AssemblerServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Faça referência a um documento DDX existente.

   * Crie um `java.io.FileInputStream` objeto que representa o documento DDX usando seu construtor e passando um valor de string que especifica o local do arquivo DX.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Faça referência aos documentos XDP.

   * Crie um `java.util.Map` objeto usado para armazenar documentos XDP de entrada usando um `HashMap` construtor.
   * Crie um `com.adobe.idp.Document` e transmita o `java.io.FileInputStream` objeto que contém o arquivo XDP de entrada (repita essa tarefa para cada arquivo XDP).
   * Adicione uma entrada à `java.util.Map` ao invocar seu `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor `source` valor do elemento especificado no documento DDX (repita essa tarefa para cada arquivo XDP).
      * A `com.adobe.idp.Document` objeto que contém o documento XDP que corresponde ao `source` (repita essa tarefa para cada arquivo XDP).

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` que armazena opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos seus requisitos de negócios, chamando um método que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, chame a função `AssemblerOptionSpec` do objeto `setFailOnError` método e pass `false`.

1. Monte os vários documentos XDP.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX a ser usado
   * A `java.util.Map` objeto que contém os arquivos XDP de entrada
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log da tarefa

   O `invokeDDX` método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém o documento XDP montado.

1. Recupere o documento XDP montado.

   Para obter o documento XDP montado, execute as seguintes ações:

   * Chame o `AssemblerResult` do objeto `getDocuments` método . Esse método retorna um `java.util.Map` objeto.
   * Iterar por meio do `java.util.Map` até encontrar o resultante `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento XDP montado.

**Consulte também**

[Montagem de vários fragmentos XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[Início rápido (modo SOAP): Montagem de vários fragmentos XDP usando a API do Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montar vários fragmentos XDP usando a API do serviço da Web {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Monte vários fragmentos XDP usando a API do Serviço de Assembler (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL ao definir uma referência de serviço:

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um cliente Assembler PDF.

   * Crie um `AssemblerServiceClient` usando seu construtor padrão.
   * Crie um `AssemblerServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço da AEM Forms, como `https://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `AssemblerServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao `AssemblerServiceClient.ClientCredentials.UserName.UserName` campo.
      * Atribua o valor da senha correspondente ao `AssemblerServiceClient.ClientCredentials.UserName.Password`campo.
      * Atribua o `HttpClientCredentialType.Basic` valor constante para `BasicHttpBindingSecurity.Transport.ClientCredentialType`campo.
      * Atribua o `BasicHttpSecurityMode.TransportCredentialOnly` valor constante para `BasicHttpBindingSecurity.Security.Mode`campo.

1. Faça referência a um documento DDX existente.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento DDX.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento DX e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` método . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Faça referência aos documentos XDP.

   * Para cada arquivo XDP de entrada, crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o arquivo de entrada.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo de entrada e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` método . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.
   * Crie um `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de coleção é usado para armazenar arquivos de entrada necessários para criar um documento XDP montado.
   * Para cada arquivo de entrada, crie um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Atribua um valor de string que represente o nome da chave à variável `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `key` campo. Esse valor deve corresponder ao valor do elemento especificado no documento DDX. (Execute esta tarefa para cada arquivo XDP de entrada.)
   * Atribua o `BLOB` que armazena o arquivo de entrada no `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `value` campo. (Execute esta tarefa para cada arquivo XDP de entrada.)
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` para `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o `MyMapOf_xsd_string_To_xsd_anyType` do objeto `Add` e passe o `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Execute esta tarefa para cada documento XDP de entrada.)

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` que armazena opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos da empresa, atribuindo um valor a um membro de dados pertencente à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, atribua `false` para `AssemblerOptionSpec` do objeto `failOnError` membro de dados.

1. Monte os vários documentos XDP.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e transmita os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX
   * O `MyMapOf_xsd_string_To_xsd_anyType` objeto que contém os arquivos necessários
   * Um `AssemblerOptionSpec` objeto que especifica as opções de tempo de execução

   O `invokeDDX` retorna um método `AssemblerResult` objeto que contém os resultados da tarefa e quaisquer exceções que ocorreram.

1. Recupere o documento XDP montado.

   Para obter o documento XDP recém-criado, execute as seguintes ações:

   * Acesse o `AssemblerResult` do objeto `documents` , que é um `Map` objeto que contém os documentos PDF resultantes.
   * Iterar por meio do `Map` para obter cada documento resultante. Em seguida, converta esse membro da matriz `value` para `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando seu `BLOB` do objeto `MTOM` propriedade. Isso retorna uma matriz de bytes que você pode gravar em um arquivo XDP.

**Consulte também**

[Montagem de vários fragmentos XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
