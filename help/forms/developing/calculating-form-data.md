---
title: Cálculo dos dados de formulário
seo-title: Cálculo dos dados de formulário
description: Use o serviço Forms para calcular valores que um usuário insere em um formulário e exibir os resultados. O serviço Forms calcula os valores usando a API de Java e a API de serviço da Web.
seo-description: Use o serviço Forms para calcular valores que um usuário insere em um formulário e exibir os resultados. O serviço Forms calcula os valores usando a API de Java e a API de serviço da Web.
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1917'
ht-degree: 0%

---


# Calculando dados de formulário {#calculating-form-data}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

O serviço Forms pode calcular os valores que um usuário insere em um formulário e exibir os resultados. Para calcular os dados do formulário, você deve executar duas tarefas. Primeiro, crie um script de design de formulário que calcula os dados do formulário. Um design de formulário é compatível com três tipos de scripts. Um tipo de script é executado no cliente, outro é executado no servidor e o terceiro tipo é executado no servidor e no cliente. O tipo de script discutido neste tópico é executado no servidor. Cálculos do lado do servidor são suportados para transformações de HTML, PDF e Guia do formulário (obsoleto).

Como parte do processo de design de formulário, você pode usar cálculos e scripts para fornecer uma experiência do usuário mais rica. Cálculos e scripts podem ser adicionados à maioria dos campos e objetos de formulário. É necessário criar um script de design de formulário para executar operações de cálculo nos dados inseridos por um usuário em um formulário interativo.

O usuário insere valores no formulário e clica no botão Calcular para visualizar os resultados. O processo a seguir descreve um aplicativo de exemplo que permite ao usuário calcular dados:

* O usuário acessa uma página HTML chamada StartLoan.html que atua como a página inicial do aplicativo web. Esta página chama um Servlet Java chamado `GetLoanForm`.
* O servlet `GetLoanForm` renderiza um formulário de empréstimo. Este formulário contém um script, campos interativos, um botão calcular e um botão enviar.
* O usuário insere valores nos campos do formulário e clica no botão Calcular . O formulário é enviado para o `CalculateData` Java Servlet onde o script é executado. O formulário é enviado de volta ao usuário com os resultados do cálculo exibidos no formulário.
* O usuário continua inserindo e calculando valores até que um resultado satisfatório seja exibido. Quando satisfeito, o usuário clica no botão Enviar para processar o formulário. O formulário é enviado para outro Servlet Java chamado `ProcessForm` que é responsável pela recuperação dos dados enviados. (Consulte [Manuseio de Forms](/help/forms/developing/rendering-forms.md#handling-submitted-forms) Enviado.)


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
   <td><p>O <code>GetLoanForm</code> Servlet Java é chamado da página inicial HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>O <code>GetLoanForm</code> Servlet Java usa a API do cliente de serviço do Forms para renderizar o formulário de empréstimo para o navegador da Web do cliente. A diferença entre a renderização de um formulário que contém um script configurado para execução no servidor e a renderização de um formulário que não contém um script é que você deve especificar o local de destino usado para executar o script. Se um local de destino não for especificado, um script configurado para execução no servidor não será executado. Por exemplo, considere o aplicativo introduzido nesta seção. O <code>CalculateData</code> Servlet Java é o local de destino onde o script é executado.</p></td>
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

**A.** Um campo denominado NumericField1  **B.** Um campo denominado NumericField2  **C.** Um campo denominado NumericField3

A sintaxe do script localizado neste design de formulário é a seguinte:

```javascript
     NumericField3 = NumericField2 + NumericField1
```

Nesse design de formulário, o botão Calcular é um botão de comando e o script está localizado no evento `Click` desse botão. Quando um usuário insere valores nos dois primeiros campos (NumericField1 e NumericField2) e clica no botão Calculate , o formulário é enviado para o serviço Forms, onde o script é executado. O serviço Forms renderiza o formulário de volta ao dispositivo cliente com os resultados do cálculo exibidos no campo NumericField3 .

>[!NOTE]
>
>Para obter informações sobre como criar um script de design de formulário, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para calcular dados de formulário, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Recupere um formulário contendo um script de cálculo.
1. Gravar o fluxo de dados do formulário de volta no navegador da Web cliente

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente do Forms**

Antes de executar programaticamente uma operação de API do cliente de serviço do Forms, é necessário criar um cliente de serviço do Forms. Se estiver usando a API do Java, crie um objeto `FormsServiceClient` . Se estiver usando a API do serviço da Web da Forms, crie um objeto `FormsServiceService` .

**Recuperar um formulário contendo um script de cálculo**

Use a API do cliente de serviço do Forms para criar a lógica do aplicativo que lida com um formulário que contém um script configurado para execução no servidor. O processo é semelhante ao manuseio de um formulário enviado. (Consulte [Manuseio de Forms](/help/forms/developing/handling-submitted-forms.md) Enviado.)

Verifique se o estado de processamento associado ao formulário enviado é `1` `(Calculate)`, o que significa que o serviço Forms está executando uma operação de cálculo nos dados do formulário e os resultados devem ser gravados de volta ao usuário. Nessa situação, um script configurado para ser executado no servidor é executado automaticamente.

**Gravar o fluxo de dados do formulário de volta no navegador da Web cliente**

Depois de verificar se o estado de processamento associado a um formulário enviado é `1`, você deve gravar os resultados de volta no navegador da Web do cliente. Quando o formulário for exibido, o valor calculado aparecerá no(s) campo(s) apropriado(s).

**Consulte também:**

[Inclusão de ](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[arquivos de biblioteca Java do AEM FormsCalcule os dados de formulário usando a ](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[APIC JavaCalcule os dados de formulário usando o serviço da Web ](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[APISdefinindo ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[propriedades de conexãoAPI do serviço do Forms ](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[Inícios de renderização de ](/help/forms/developing/rendering-interactive-pdf-forms.md)
[formulários PDF interativosCriando aplicativos da Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Calcule os dados do formulário usando a API Java {#calculate-form-data-using-the-java-api}

Calcule os dados do formulário usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar no caminho de classe do seu projeto Java.

1. Criar um objeto de API do cliente do Forms

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recuperar um formulário contendo um script de cálculo

   * Para recuperar dados de formulário que contenham um script de cálculo, crie um objeto `com.adobe.idp.Document` usando seu construtor e chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getInputStream` de dentro do construtor.
   * Chame o método `FormsServiceClient` do objeto `processFormSubmission` e passe os seguintes valores:

      * O objeto `com.adobe.idp.Document` que contém os dados do formulário.
      * Um valor de string que especifica variáveis de ambiente, incluindo todos os cabeçalhos HTTP relevantes. Você deve especificar o tipo de conteúdo a ser tratado especificando um ou mais valores para a variável de ambiente `CONTENT_TYPE`. Por exemplo, para manipular dados XML e PDF, especifique o seguinte valor de string para esse parâmetro: `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * Um valor de string que especifica o valor do cabeçalho `HTTP_USER_AGENT`; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Um objeto `RenderOptionsSpec` que armazena opções de tempo de execução.

      O método `processFormSubmission` retorna um objeto `FormsResult` contendo os resultados do envio do formulário.

   * Verifique se o estado de processamento associado a um formulário enviado é `1` chamando o método `FormsResult` do objeto `getAction`. Se esse método retornar o valor `1`, o cálculo foi executado e os dados podem ser gravados de volta no navegador da Web do cliente.


1. Gravar o fluxo de dados do formulário de volta no navegador da Web cliente

   * Crie um objeto `javax.servlet.ServletOutputStream` usado para enviar um fluxo de dados de formulário para o navegador da Web do cliente.
   * Crie um objeto `com.adobe.idp.Document` chamando o método `FormsResult` object &#39;s `getOutputContent`.
   * Crie um objeto `java.io.InputStream` chamando o método `com.adobe.idp.Document` `getInputStream` do objeto.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, chamando o método `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o método `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Passe a matriz de bytes para o método `write` .

**Consulte também:**


[Inclusão de ](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[arquivos da biblioteca Java AEM FormsDefinição de propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Calcular dados de formulário usando a API do serviço da Web {#calculate-form-data-using-the-web-service-api}

Calcule os dados do formulário usando a API do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o WSDL do serviço Forms.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto de API do cliente do Forms

   Crie um objeto `FormsService` e defina os valores de autenticação.

1. Recuperar um formulário contendo um script de cálculo

   * Para recuperar dados de formulário publicados em um Servlet Java, crie um objeto `BLOB` usando seu construtor.
   * Crie um objeto `java.io.InputStream` usando o método `javax.servlet.http.HttpServletResponse` `getInputStream` do objeto.
   * Crie um objeto `java.io.ByteArrayOutputStream` usando seu construtor e passando o comprimento do objeto `java.io.InputStream`.
   * Copie o conteúdo do objeto `java.io.InputStream` no objeto `java.io.ByteArrayOutputStream`.
   * Crie uma matriz de bytes chamando o método `java.io.ByteArrayOutputStream` do objeto `toByteArray`.
   * Preencha o objeto `BLOB` chamando seu método `setBinaryData` e passando a matriz de bytes como um argumento.
   * Crie um objeto `RenderOptionsSpec` usando seu construtor. Defina o valor da localidade chamando o método `RenderOptionsSpec` do objeto `setLocale` e passando um valor de string que especifica o valor da localidade.
   * Chame o método `FormsServiceClient` do objeto `processFormSubmission` e passe os seguintes valores:

      * O objeto `BLOB` que contém os dados do formulário.
      * Um valor de string que especifica variáveis de ambiente incluído em todos os cabeçalhos HTTP relevantes. Por exemplo, você pode especificar o seguinte valor da string: `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * Um valor de string que especifica o valor do cabeçalho `HTTP_USER_AGENT`; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Um objeto `RenderOptionsSpec` que armazena opções de tempo de execução. Para obter mais informações, .
      * Um objeto vazio `BLOBHolder` que é preenchido pelo método .
      * Um objeto vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pelo método .
      * Um objeto vazio `BLOBHolder` que é preenchido pelo método .
      * Um objeto vazio `BLOBHolder` que é preenchido pelo método .
      * Um objeto vazio `javax.xml.rpc.holders.ShortHolder` que é preenchido pelo método .
      * Um objeto vazio `MyArrayOf_xsd_anyTypeHolder` que é preenchido pelo método . Esse parâmetro é usado para armazenar anexos de arquivo enviados junto com o formulário.
      * Um objeto vazio `FormsResultHolder` que é preenchido pelo método com o formulário enviado.

      O método `processFormSubmission` preenche o parâmetro `FormsResultHolder` com os resultados do envio do formulário. O método `processFormSubmission` retorna um objeto `FormsResult` contendo os resultados do envio do formulário.

   * Verifique se o estado de processamento associado a um formulário enviado é `1` chamando o método `FormsResult` do objeto `getAction`. Se esse método retornar o valor `1`, o cálculo foi executado e os dados podem ser gravados de volta no navegador da Web do cliente.


1. Gravar o fluxo de dados do formulário de volta no navegador da Web cliente

   * Crie um objeto `javax.servlet.ServletOutputStream` usado para enviar um fluxo de dados de formulário para o navegador da Web do cliente.
   * Crie um objeto `BLOB` que contenha dados de formulário chamando o método `FormsResult` do objeto `getOutputContent`.
   * Crie uma matriz de bytes e preencha-a chamando o método `BLOB` do objeto `getBinaryData`. Essa tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Chame o método `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Passe a matriz de bytes para o método `write` .

**Consulte**
[tambémChamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
