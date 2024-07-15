---
title: Cálculo de dados de formulário
description: Use o serviço Forms para calcular os valores que um usuário insere em um formulário e exibir os resultados. O serviço Forms calcula os valores usando a API Java e a API de serviço da Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
role: Developer
exl-id: 28abf044-6c8e-4578-ae2e-54cdbd694c5f
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1858'
ht-degree: 0%

---

# Cálculo de dados de formulário {#calculating-form-data}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

O serviço Forms pode calcular os valores que um usuário insere em um formulário e exibir os resultados. Para calcular dados de formulário, você deve executar duas tarefas. Primeiro, crie um script de design de formulário que calcula os dados de formulário. Um design de formulário é compatível com três tipos de scripts. Um tipo de script é executado no cliente, outro é executado no servidor e o terceiro é executado no servidor e no cliente. O tipo de script discutido neste tópico é executado no servidor. Os cálculos do lado do servidor são compatíveis com as transformações de HTML, PDF e Guia de forma (obsoleto).

Como parte do processo de design do formulário, você pode usar cálculos e scripts para fornecer uma experiência do usuário mais avançada. Cálculos e scripts podem ser adicionados à maioria dos campos e objetos de formulário. Crie um script de design de formulário para executar operações de cálculo nos dados que um usuário insere em um formulário interativo.

O usuário insere valores no formulário e clica no botão Calculate para exibir os resultados. O processo a seguir descreve um aplicativo de exemplo que permite ao usuário calcular dados:

* O usuário acessa uma página de HTML chamada StartLoan.html que atua como a página inicial da aplicação Web. Esta página chama um Servlet Java chamado `GetLoanForm`.
* O servlet `GetLoanForm` renderiza um formulário de empréstimo. Este formulário contém um script, campos interativos, um botão calcular e um botão enviar.
* O usuário insere valores nos campos do formulário e clica no botão Calcular. O formulário é enviado para o Servlet Java `CalculateData` onde o script é executado. O formulário é enviado de volta ao usuário com os resultados do cálculo exibidos no formulário.
* O usuário continua informando e calculando valores até que um resultado satisfatório seja exibido. Quando satisfeito, o usuário clica no botão Submit para processar o formulário. O formulário é enviado para outro Servlet Java chamado `ProcessForm`, que é responsável por recuperar os dados enviados. (Consulte [Manipulação de Forms Enviada](/help/forms/developing/rendering-forms.md#handling-submitted-forms).)


O diagrama a seguir mostra o fluxo lógico do aplicativo.

![cf_cf_finsrv_loancalcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

A tabela a seguir descreve as etapas deste diagrama.

<table>
 <thead>
  <tr>
   <th><p>Etapa</p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>O Servlet Java <code>GetLoanForm</code> é chamado a partir da página inicial do HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>O Servlet Java <code>GetLoanForm</code> usa a API do cliente do serviço Forms para renderizar o formulário de empréstimo para o navegador Web do cliente. A diferença entre renderizar um formulário que contém um script configurado para ser executado no servidor e renderizar um formulário que não contém um script é que você deve especificar o local de destino usado para executar o script. Se um local de destino não for especificado, um script configurado para ser executado no servidor não será executado. Por exemplo, considere o aplicativo introduzido nesta seção. O Servlet Java <code>CalculateData</code> é o local de destino onde o script é executado.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>O usuário insere os dados em campos interativos e clica no botão Calcular. O formulário é enviado para o Servlet Java <code>CalculateData</code>, onde o script é executado. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>O formulário é renderizado no navegador da web com os resultados do cálculo exibidos no formulário. </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>O usuário clica no botão Submit quando os valores forem satisfatórios. O formulário é enviado para outro Servlet Java chamado <code>ProcessForm</code>.</p></td>
  </tr>
 </tbody>
</table>

Normalmente, um formulário enviado como conteúdo de PDF contém scripts que são executados no cliente. No entanto, os cálculos do lado do servidor também podem ser executados. Um botão Enviar não pode ser usado para calcular scripts. Nessa situação, os cálculos não são executados porque o serviço do Forms considera a interação concluída.

Para ilustrar o uso de um script de design de formulário, esta seção examina um formulário interativo simples que contém um script configurado para execução no servidor. O diagrama a seguir mostra um design de formulário contendo um script que adiciona valores inseridos por um usuário nos dois primeiros campos e exibe o resultado no terceiro campo.

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.** Um campo chamado NumericField1 **B.** Um campo chamado NumericField2 **C.** Um campo chamado NumericField3

A sintaxe do script nesse design de formulário é a seguinte:

```javascript
     NumericField3 = NumericField2 + NumericField1
```

Neste design de formulário, o botão Calcular é um botão de comando, e o script está no evento `Click` desse botão. Quando um usuário insere valores nos dois primeiros campos (NumericField1 e NumericField2) e clica no botão Calcular, o formulário é enviado ao serviço do Forms, onde o script é executado. O serviço Forms renderiza o formulário de volta para o dispositivo cliente com os resultados do cálculo exibidos no campo NumericField3.

>[!NOTE]
>
>Para obter informações sobre como criar um script de design de formulário, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para calcular dados de formulário, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Recupere um formulário que contenha um script de cálculo.
1. Gravar o fluxo de dados do formulário de volta no navegador da Web do cliente

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente do Forms**

Antes de executar programaticamente uma operação da API do cliente de serviço do Forms, você deve criar um cliente de serviço do Forms. Se você estiver usando a API Java, crie um objeto `FormsServiceClient`. Se você estiver usando a API de serviço Web Forms, crie um objeto `FormsServiceService`.

**Recuperar um formulário que contenha um script de cálculo**

Use a API do cliente de serviço do Forms para criar uma lógica de aplicativo que manipula um formulário que contém um script configurado para execução no servidor. O processo é semelhante ao manuseio de um formulário enviado. (Consulte [Manipulação de Forms Enviada](/help/forms/developing/handling-submitted-forms.md).)

Verifique se o estado de processamento associado ao formulário enviado é `1` `(Calculate)`, o que significa que o serviço Forms está executando uma operação de cálculo nos dados do formulário e os resultados devem ser gravados de volta para o usuário. Nessa situação, um script configurado para ser executado no servidor é executado automaticamente.

**Gravar o fluxo de dados de formulário de volta no navegador Web cliente**

Depois de verificar se o estado de processamento associado a um formulário enviado é `1`, você deve gravar os resultados no navegador da Web do cliente. Quando o formulário for exibido, o valor calculado será exibido nos campos apropriados.

**Consulte também**

[Incluindo arquivos da biblioteca AEM Forms Java](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Calcular dados do formulário usando a API Java](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[Calcular dados de formulário usando a API de serviço Web](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[Início Rápido da API de Serviço do Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[Renderizando PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)
[Criando Aplicativos Web que Renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Calcular dados do formulário usando a API Java {#calculate-form-data-using-the-java-api}

Calcule dados de formulário usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do projeto Java.

1. Criar um objeto da API do cliente do Forms

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recuperar um formulário que contenha um script de cálculo

   * Para recuperar dados de formulário que contenham um script de cálculo, crie um objeto `com.adobe.idp.Document` usando seu construtor e invocando o método `getInputStream` do objeto `javax.servlet.http.HttpServletResponse` de dentro do construtor.
   * Invoque o método `processFormSubmission` do objeto `FormsServiceClient` e passe os seguintes valores:

      * O objeto `com.adobe.idp.Document` que contém os dados de formulário.
      * Um valor de string que especifica variáveis de ambiente, incluindo todos os cabeçalhos HTTP relevantes. Especifique o tipo de conteúdo a ser manipulado especificando um ou mais valores para a variável de ambiente `CONTENT_TYPE`. Por exemplo, para manipular dados XML e PDF, especifique o seguinte valor de cadeia de caracteres para este parâmetro: `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * Um valor de cadeia de caracteres que especifica o valor do cabeçalho `HTTP_USER_AGENT`; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Um objeto `RenderOptionsSpec` que armazena opções de tempo de execução.

     O método `processFormSubmission` retorna um objeto `FormsResult` contendo os resultados do envio do formulário.

   * Verifique se o estado de processamento associado a um formulário enviado é `1` invocando o método `getAction` do objeto `FormsResult`. Se esse método retornar o valor `1`, o cálculo foi executado e os dados podem ser gravados no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário de volta no navegador da Web do cliente

   * Crie um objeto `javax.servlet.ServletOutputStream` usado para enviar um fluxo de dados de formulário ao navegador da Web cliente.
   * Crie um objeto `com.adobe.idp.Document` invocando o método `getOutputContent` do objeto `FormsResult`.
   * Crie um objeto `java.io.InputStream` invocando o método `getInputStream` do objeto `com.adobe.idp.Document`.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados de formulário, chamando o método `read` do objeto `InputStream` e transmitindo a matriz de bytes como argumento.
   * Invoque o método `write` do objeto `javax.servlet.ServletOutputStream` para enviar o fluxo de dados de formulário para o navegador Web cliente. Passar a matriz de bytes para o método `write`.

**Consulte também**


[Incluindo arquivos da biblioteca AEM Forms Java](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Calcular dados do formulário usando a API do serviço Web {#calculate-form-data-using-the-web-service-api}

Calcule dados de formulário usando a API do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes de proxy Java que consomem o serviço WSDL do Forms.
   * Inclua as classes de proxy Java no caminho da classe.

1. Criar um objeto da API do cliente do Forms

   Crie um objeto `FormsService` e defina valores de autenticação.

1. Recuperar um formulário que contenha um script de cálculo

   * Para recuperar dados de formulário postados em um Servlet Java, crie um objeto `BLOB` usando seu construtor.
   * Crie um objeto `java.io.InputStream` usando o método `getInputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie um objeto `java.io.ByteArrayOutputStream` usando seu construtor e transmitindo o comprimento do objeto `java.io.InputStream`.
   * Copie o conteúdo do objeto `java.io.InputStream` no objeto `java.io.ByteArrayOutputStream`.
   * Crie uma matriz de bytes invocando o método `toByteArray` do objeto `java.io.ByteArrayOutputStream`.
   * Preencha o objeto `BLOB` invocando seu método `setBinaryData` e transmitindo a matriz de bytes como um argumento.
   * Crie um objeto `RenderOptionsSpec` usando seu construtor. Defina o valor da localidade invocando o método `setLocale` do objeto `RenderOptionsSpec` e transmitindo um valor de cadeia de caracteres que especifique o valor da localidade.
   * Invoque o método `processFormSubmission` do objeto `FormsServiceClient` e passe os seguintes valores:

      * O objeto `BLOB` que contém os dados de formulário.
      * Um valor de string que especifica variáveis de ambiente incluídas em todos os cabeçalhos HTTP relevantes. Por exemplo, você pode especificar o seguinte valor de cadeia de caracteres: `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * Um valor de cadeia de caracteres que especifica o valor do cabeçalho `HTTP_USER_AGENT`; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Um objeto `RenderOptionsSpec` que armazena opções de tempo de execução. Para obter mais informações, .
      * Um objeto `BLOBHolder` vazio preenchido pelo método.
      * Um objeto `javax.xml.rpc.holders.StringHolder` vazio preenchido pelo método.
      * Um objeto `BLOBHolder` vazio preenchido pelo método.
      * Um objeto `BLOBHolder` vazio preenchido pelo método.
      * Um objeto `javax.xml.rpc.holders.ShortHolder` vazio preenchido pelo método.
      * Um objeto `MyArrayOf_xsd_anyTypeHolder` vazio preenchido pelo método. Esse parâmetro é usado para armazenar anexos de arquivo enviados junto com o formulário.
      * Um objeto `FormsResultHolder` vazio que é preenchido pelo método com o formulário enviado.

     O método `processFormSubmission` preenche o parâmetro `FormsResultHolder` com os resultados do envio do formulário. O método `processFormSubmission` retorna um objeto `FormsResult` contendo os resultados do envio do formulário.

   * Verifique se o estado de processamento associado a um formulário enviado é `1` invocando o método `getAction` do objeto `FormsResult`. Se esse método retornar o valor `1`, o cálculo foi executado e os dados podem ser gravados no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário de volta no navegador da Web do cliente

   * Crie um objeto `javax.servlet.ServletOutputStream` usado para enviar um fluxo de dados de formulário ao navegador da Web cliente.
   * Crie um objeto `BLOB` que contenha dados de formulário invocando o método `getOutputContent` do objeto `FormsResult`.
   * Crie uma matriz de bytes e preencha-a chamando o método `getBinaryData` do objeto `BLOB`. Esta tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Invoque o método `write` do objeto `javax.servlet.http.HttpServletResponse` para enviar o fluxo de dados de formulário para o navegador Web cliente. Passar a matriz de bytes para o método `write`.

**Consulte também**
[Invocando o AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
