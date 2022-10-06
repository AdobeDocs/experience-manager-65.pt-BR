---
title: Cálculo dos dados de formulário
seo-title: Calculating Form Data
description: Use o serviço Forms para calcular valores que um usuário insere em um formulário e exibir os resultados. O serviço Forms calcula os valores usando a API Java e a API do serviço da Web.
seo-description: Use the Forms service to calculate values that a user enters into a form and display the results. Forms service calculates the values using the Java API and Web Service API.
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
role: Developer
exl-id: 28abf044-6c8e-4578-ae2e-54cdbd694c5f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 0%

---

# Cálculo dos dados de formulário {#calculating-form-data}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

O serviço Forms pode calcular os valores que um usuário insere em um formulário e exibir os resultados. Para calcular os dados do formulário, você deve executar duas tarefas. Primeiro, crie um script de design de formulário que calcula os dados do formulário. Um design de formulário é compatível com três tipos de scripts. Um tipo de script é executado no cliente, outro é executado no servidor e o terceiro tipo é executado no servidor e no cliente. O tipo de script discutido neste tópico é executado no servidor. Os cálculos do lado do servidor são compatíveis com transformações HTML, PDF e form Guide (obsoleto).

Como parte do processo de design de formulário, você pode usar cálculos e scripts para fornecer uma experiência do usuário mais rica. Cálculos e scripts podem ser adicionados à maioria dos campos e objetos de formulário. É necessário criar um script de design de formulário para executar operações de cálculo nos dados inseridos por um usuário em um formulário interativo.

O usuário insere valores no formulário e clica no botão Calcular para visualizar os resultados. O processo a seguir descreve um aplicativo de exemplo que permite ao usuário calcular dados:

* O usuário acessa uma HTML page chamada StartLoan.html que atua como a página inicial do aplicativo web. Esta página chama um Servlet Java chamado `GetLoanForm`.
* O `GetLoanForm` servlet renderiza um formulário de empréstimo. Este formulário contém um script, campos interativos, um botão calcular e um botão enviar.
* O usuário insere valores nos campos do formulário e clica no botão Calcular . O formulário é enviado para o `CalculateData` Java Servlet onde o script é executado. O formulário é enviado de volta ao usuário com os resultados do cálculo exibidos no formulário.
* O usuário continua inserindo e calculando valores até que um resultado satisfatório seja exibido. Quando satisfeito, o usuário clica no botão Enviar para processar o formulário. O formulário é enviado para outro Servlet Java chamado `ProcessForm` responsável pela recuperação dos dados enviados. (Consulte [Manuseio de Forms Enviado](/help/forms/developing/rendering-forms.md#handling-submitted-forms).)


O diagrama a seguir mostra o fluxo lógico do aplicativo.

![cf_cf_finsrv_loancalcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

A tabela a seguir descreve as etapas neste diagrama.

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
   <td><p>O <code>GetLoanForm</code> O Java Servlet é chamado da página inicial do HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>O <code>GetLoanForm</code> O Java Servlet usa a API do cliente de serviço do Forms para renderizar o formulário de empréstimo para o navegador da Web do cliente. A diferença entre a renderização de um formulário que contém um script configurado para execução no servidor e a renderização de um formulário que não contém um script é que você deve especificar o local de destino usado para executar o script. Se um local de destino não for especificado, um script configurado para execução no servidor não será executado. Por exemplo, considere o aplicativo introduzido nesta seção. O <code>CalculateData</code> Java Servlet é o local de destino onde o script é executado.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>O usuário insere dados em campos interativos e clica no botão Calcular . O formulário é enviado para o <code>CalculateData</code> Java Servlet, onde o script é executado. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>O formulário é renderizado de volta ao navegador da Web com os resultados do cálculo exibidos no formulário. </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>O usuário clica no botão Enviar quando os valores são satisfatórios. O formulário é enviado para outro Servlet Java chamado <code>ProcessForm</code>.</p></td>
  </tr>
 </tbody>
</table>

Normalmente, um formulário enviado como conteúdo PDF contém scripts que são executados no cliente. No entanto, cálculos do lado do servidor também podem ser executados. Um botão Enviar não pode ser usado para calcular scripts. Nessa situação, os cálculos não são executados porque o serviço da Forms considera a interação como concluída.

Para ilustrar o uso de um script de design de formulário, esta seção examina um formulário interativo simples que contém um script configurado para execução no servidor. O diagrama a seguir mostra um design de formulário contendo um script que adiciona valores que um usuário insere nos dois primeiros campos e exibe o resultado no terceiro campo.

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.** Um campo chamado NumericField1 **B.** Um campo chamado NumericField2 **C.** Um campo denominado NumericField3

A sintaxe do script localizado neste design de formulário é a seguinte:

```javascript
     NumericField3 = NumericField2 + NumericField1
```

Nesse design de formulário, o botão Calcular é um botão de comando e o script está localizado no botão `Click` evento. Quando um usuário insere valores nos dois primeiros campos (NumericField1 e NumericField2) e clica no botão Calculate , o formulário é enviado para o serviço Forms, onde o script é executado. O serviço Forms renderiza o formulário de volta ao dispositivo cliente com os resultados do cálculo exibidos no campo NumericField3 .

>[!NOTE]
>
>Para obter informações sobre como criar um script de design de formulário, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para calcular dados de formulário, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Recupere um formulário contendo um script de cálculo.
1. Gravar o fluxo de dados do formulário de volta no navegador da Web cliente

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente do Forms**

Antes de executar programaticamente uma operação de API do cliente de serviço do Forms, é necessário criar um cliente de serviço do Forms. Se estiver usando a API do Java, crie um `FormsServiceClient` objeto. Se estiver usando a API do serviço da Web da Forms, crie um `FormsServiceService` objeto.

**Recuperar um formulário contendo um script de cálculo**

Use a API do cliente de serviço do Forms para criar a lógica do aplicativo que lida com um formulário que contém um script configurado para execução no servidor. O processo é semelhante ao manuseio de um formulário enviado. (Consulte [Manuseio de Forms Enviado](/help/forms/developing/handling-submitted-forms.md).)

Verifique se o estado de processamento associado ao formulário enviado está `1` `(Calculate)`, o que significa que o serviço Forms está executando uma operação de cálculo nos dados do formulário e os resultados devem ser gravados de volta no usuário. Nessa situação, um script configurado para ser executado no servidor é executado automaticamente.

**Gravar o fluxo de dados do formulário de volta no navegador da Web cliente**

Depois de verificar se o estado de processamento associado a um formulário enviado é `1`, você deve gravar os resultados novamente no navegador da Web do cliente. Quando o formulário for exibido, o valor calculado aparecerá no(s) campo(s) apropriado(s).

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Calcular dados de formulário usando a API Java](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[Calcular dados de formulário usando a API do serviço da Web](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[Início rápido da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)
[Criação de aplicativos Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Calcular dados de formulário usando a API Java {#calculate-form-data-using-the-java-api}

Calcule os dados do formulário usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar no caminho de classe do seu projeto Java.

1. Criar um objeto de API do cliente do Forms

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `FormsServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Recuperar um formulário contendo um script de cálculo

   * Para recuperar dados de formulário que contenham um script de cálculo, crie um `com.adobe.idp.Document` usando seu construtor e chamando o `javax.servlet.http.HttpServletResponse` do objeto `getInputStream` do construtor.
   * Chame o `FormsServiceClient` do objeto `processFormSubmission` e transmita os seguintes valores:

      * O `com.adobe.idp.Document` objeto que contém os dados do formulário.
      * Um valor de string que especifica variáveis de ambiente, incluindo todos os cabeçalhos HTTP relevantes. Você deve especificar o tipo de conteúdo a ser tratado especificando um ou mais valores para a variável `CONTENT_TYPE` variável de ambiente. Por exemplo, para manipular dados XML e PDF, especifique o seguinte valor de string para esse parâmetro: `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * Um valor de string que especifica a variável `HTTP_USER_AGENT` valor do cabeçalho; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` objeto que armazena opções de tempo de execução.

      O `processFormSubmission` método retorna um `FormsResult` objeto contendo os resultados do envio do formulário.

   * Verifique se o estado de processamento associado a um formulário enviado está `1` chamando o `FormsResult` do objeto `getAction` método . Se esse método retornar o valor `1`, o cálculo foi executado e os dados podem ser gravados de volta no navegador da Web do cliente.


1. Gravar o fluxo de dados do formulário de volta no navegador da Web cliente

   * Crie um `javax.servlet.ServletOutputStream` objeto usado para enviar um fluxo de dados de formulário para o navegador da Web cliente.
   * Crie um `com.adobe.idp.Document` chamando o `FormsResult` objeto &quot;s `getOutputContent` método .
   * Crie um `java.io.InputStream` chamando o `com.adobe.idp.Document` do objeto `getInputStream` método .
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, chamando o `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

**Consulte também**


[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Calcular dados de formulário usando a API do serviço da Web {#calculate-form-data-using-the-web-service-api}

Calcule os dados do formulário usando a API do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o WSDL do serviço Forms.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto de API do cliente do Forms

   Crie um `FormsService` e definir valores de autenticação.

1. Recuperar um formulário contendo um script de cálculo

   * Para recuperar dados de formulário publicados em um Servlet Java, crie um `BLOB` usando seu construtor.
   * Crie um `java.io.InputStream` usando o `javax.servlet.http.HttpServletResponse` do objeto `getInputStream` método .
   * Crie um `java.io.ByteArrayOutputStream` usando seu construtor e passando o comprimento da variável `java.io.InputStream` objeto.
   * Copie o conteúdo do `java.io.InputStream` no objeto `java.io.ByteArrayOutputStream` objeto.
   * Crie uma matriz de bytes chamando o `java.io.ByteArrayOutputStream` do objeto `toByteArray` método .
   * Preencha o `BLOB` ao invocar seu `setBinaryData` e transmitindo a matriz de bytes como um argumento.
   * Crie um `RenderOptionsSpec` usando seu construtor. Defina o valor da localidade chamando a variável `RenderOptionsSpec` do objeto `setLocale` e transmitindo um valor de string que especifica o valor de localidade.
   * Chame o `FormsServiceClient` do objeto `processFormSubmission` e transmita os seguintes valores:

      * O `BLOB` objeto que contém os dados do formulário.
      * Um valor de string que especifica variáveis de ambiente incluído em todos os cabeçalhos HTTP relevantes. Por exemplo, você pode especificar o seguinte valor da string: `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * Um valor de string que especifica a variável `HTTP_USER_AGENT` valor do cabeçalho; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` objeto que armazena opções de tempo de execução. Para obter mais informações, .
      * Um vazio `BLOBHolder` objeto preenchido pelo método .
      * Um vazio `javax.xml.rpc.holders.StringHolder` objeto preenchido pelo método .
      * Um vazio `BLOBHolder` objeto preenchido pelo método .
      * Um vazio `BLOBHolder` objeto preenchido pelo método .
      * Um vazio `javax.xml.rpc.holders.ShortHolder` objeto preenchido pelo método .
      * Um vazio `MyArrayOf_xsd_anyTypeHolder` objeto preenchido pelo método . Esse parâmetro é usado para armazenar anexos de arquivo enviados junto com o formulário.
      * Um vazio `FormsResultHolder` objeto preenchido pelo método com o formulário enviado.

      O `processFormSubmission` O método preenche a variável `FormsResultHolder` com os resultados do envio do formulário. O `processFormSubmission` método retorna um `FormsResult` objeto contendo os resultados do envio do formulário.

   * Verifique se o estado de processamento associado a um formulário enviado está `1` chamando o `FormsResult` do objeto `getAction` método . Se esse método retornar o valor `1`, o cálculo foi executado e os dados podem ser gravados de volta no navegador da Web do cliente.


1. Gravar o fluxo de dados do formulário de volta no navegador da Web cliente

   * Crie um `javax.servlet.ServletOutputStream` objeto usado para enviar um fluxo de dados de formulário para o navegador da Web cliente.
   * Crie um `BLOB` objeto que contém dados de formulário chamando o `FormsResult` do objeto `getOutputContent` método .
   * Crie uma matriz de bytes e preencha-a chamando a variável `BLOB` do objeto `getBinaryData` método . Essa tarefa atribui o conteúdo da `FormsResult` para a matriz de bytes.
   * Chame o `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

**Consulte também**
[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
