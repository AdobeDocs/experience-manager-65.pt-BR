---
title: Calculando dados do formulário
seo-title: Calculando dados do formulário
description: Use o serviço Forms para calcular os valores que um usuário digita em um formulário e exibir os resultados. O serviço Forms calcula os valores usando a API Java e a API de serviço da Web.
seo-description: Use o serviço Forms para calcular os valores que um usuário digita em um formulário e exibir os resultados. O serviço Forms calcula os valores usando a API Java e a API de serviço da Web.
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---


# Calculando Dados de Formulário {#calculating-form-data}

**Exemplos e exemplos neste documento são apenas para AEM Forms no ambiente JEE.**

O serviço Forms pode calcular os valores que um usuário digita em um formulário e exibir os resultados. Para calcular os dados do formulário, é necessário executar duas tarefas. Primeiro, crie um script de design de formulário que calcule os dados do formulário. Um design de formulário suporta três tipos de scripts. Um tipo de script é executado no cliente, outro é executado no servidor e o terceiro tipo é executado no servidor e no cliente. O tipo de script discutido neste tópico é executado no servidor. Cálculos do lado do servidor são suportados para transformações HTML, PDF e Guia de formulário (obsoleto).

Como parte do processo de design de formulário, você pode usar cálculos e scripts para proporcionar uma experiência mais avançada ao usuário. Cálculos e scripts podem ser adicionados à maioria dos campos e objetos de formulário. É necessário criar um script de design de formulário para executar operações de cálculo nos dados inseridos pelo usuário em um formulário interativo.

O usuário insere valores no formulário e clica no botão Calcular para visualização dos resultados. O processo a seguir descreve um exemplo de aplicativo que permite que um usuário calcule dados:

* O usuário acessa uma página HTML chamada StartLoan.html que atua como a página de start do aplicativo da Web. Esta página chama um Servlet Java chamado `GetLoanForm`.
* O servlet `GetLoanForm` renderiza um formulário de empréstimo. Este formulário contém um script, campos interativos, um botão calcular e um botão enviar.
* O usuário insere valores nos campos do formulário e clica no botão Calcular. O formulário é enviado para o `CalculateData` Java Servlet onde o script é executado. O formulário é enviado de volta ao usuário com os resultados do cálculo exibidos no formulário.
* O usuário continua inserindo e calculando valores até que um resultado satisfatório seja exibido. Quando satisfeito, o usuário clica no botão Enviar para processar o formulário. O formulário é enviado para outro Java Servlet chamado `ProcessForm` responsável pela recuperação dos dados enviados. (Consulte [Manuseio do Forms](/help/forms/developing/rendering-forms.md#handling-submitted-forms) submetido.)


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
   <td><p>O Java Servlet <code>GetLoanForm</code> é chamado da página de start HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>O <code>GetLoanForm</code> Java Servlet usa a API do cliente de serviço da Forms para renderizar o formulário de empréstimo no navegador da Web do cliente. A diferença entre a renderização de um formulário que contém um script configurado para execução no servidor e a renderização de um formulário que não contém um script é que é necessário especificar o local do público alvo usado para executar o script. Se um local de público alvo não for especificado, um script configurado para execução no servidor não será executado. Por exemplo, considere o aplicativo apresentado nesta seção. O Java Servlet <code>CalculateData</code> é o local do público alvo onde o script é executado.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>O usuário insere dados em campos interativos e clica no botão Calcular. O formulário é enviado para o <code>CalculateData</code> Java Servlet, onde o script é executado. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>O formulário é renderizado de volta ao navegador da Web com os resultados do cálculo exibidos no formulário. </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>O usuário clica no botão Enviar quando os valores são satisfatórios. O formulário é enviado para outro Java Servlet chamado <code>ProcessForm</code>.</p></td>
  </tr>
 </tbody>
</table>

Normalmente, um formulário enviado como conteúdo PDF contém scripts executados no cliente. No entanto, os cálculos do lado do servidor também podem ser executados. Um botão Enviar não pode ser usado para calcular scripts. Nessa situação, os cálculos não são executados porque o serviço Forms considera a interação concluída.

Para ilustrar o uso de um script de design de formulário, esta seção examina um formulário interativo simples que contém um script configurado para execução no servidor. O diagrama a seguir mostra um design de formulário contendo um script que adiciona valores que um usuário digita nos dois primeiros campos e exibe o resultado no terceiro campo.

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.** Um campo chamado NumericField1  **B.** Um campo chamado NumericField2  **C.** Um campo chamado NumericField3

A sintaxe do script localizado neste design de formulário é a seguinte:

```javascript
     NumericField3 = NumericField2 + NumericField1
```

Nesse design de formulário, o botão Calcular é um botão de comando e o script está localizado no evento `Click` desse botão. Quando um usuário digita valores nos dois primeiros campos (NumericField1 e NumericField2) e clica no botão Calcular, o formulário é enviado para o serviço Forms, onde o script é executado. O serviço Forms renderiza o formulário de volta ao dispositivo cliente com os resultados do cálculo exibidos no campo NumericField3.

>[!NOTE]
>
>Para obter informações sobre como criar um script de design de formulário, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para calcular os dados do formulário, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API do Forms Client.
1. Recupere um formulário contendo um script de cálculo.
1. Gravar o fluxo de dados do formulário de volta no navegador da Web do cliente

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Forms Client**

Antes de executar programaticamente uma operação de API do cliente de serviço da Forms, você deve criar um cliente de serviço da Forms. Se você estiver usando a API Java, crie um objeto `FormsServiceClient`. Se você estiver usando a API de serviço da Web da Forms, crie um objeto `FormsServiceService`.

**Recuperar um formulário contendo um script de cálculo**

Use a API do cliente de serviço da Forms para criar uma lógica de aplicativo que manipule um formulário que contenha um script configurado para execução no servidor. O processo é semelhante ao manuseio de um formulário enviado. (Consulte [Manuseio do Forms](/help/forms/developing/handling-submitted-forms.md) submetido.)

Verifique se o estado de processamento associado ao formulário enviado é `1` `(Calculate)`, o que significa que o serviço Forms está executando uma operação de cálculo nos dados do formulário e os resultados devem ser gravados de volta no usuário. Nessa situação, um script configurado para execução no servidor é executado automaticamente.

**Gravar o fluxo de dados do formulário de volta no navegador da Web do cliente**

Depois de verificar se o estado de processamento associado a um formulário enviado é `1`, você deve gravar os resultados de volta no navegador da Web do cliente. Quando o formulário for exibido, o valor calculado aparecerá nos campos apropriados.

**Consulte também:**

[Incluindo ](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[arquivos da biblioteca Java AEM FormsCalcular dados de formulário usando o Java ](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[APICalcular dados de formulário usando o serviço da Web ](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[APISonfigurando ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[as propriedades de conexãoA API do serviço do Forms ](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[Começa a renderizar ](/help/forms/developing/rendering-interactive-pdf-forms.md)
[formulários PDF interativosCriando Aplicações web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Calcular dados de formulário usando a API Java {#calculate-form-data-using-the-java-api}

Calcule os dados do formulário usando a API da Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do Forms Client

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


1. Gravar o fluxo de dados do formulário de volta no navegador da Web do cliente

   * Crie um objeto `javax.servlet.ServletOutputStream` usado para enviar um fluxo de dados de formulário para o navegador da Web do cliente.
   * Crie um objeto `com.adobe.idp.Document` chamando o método `FormsResult` object &#39;s `getOutputContent`.
   * Crie um objeto `java.io.InputStream` invocando o método `com.adobe.idp.Document` do objeto `getInputStream`.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário chamando o método `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o método `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte também:**


[Inclusão de ](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[arquivos da biblioteca Java AEM FormsDefinição de propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Calcular dados de formulário usando a API de serviço da Web {#calculate-form-data-using-the-web-service-api}

Calcule os dados do formulário usando a Forms API (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o serviço Forms WSDL.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto de API do Forms Client

   Crie um objeto `FormsService` e defina os valores de autenticação.

1. Recuperar um formulário contendo um script de cálculo

   * Para recuperar dados de formulário publicados em um Java Servlet, crie um objeto `BLOB` usando seu construtor.
   * Crie um objeto `java.io.InputStream` usando o método `javax.servlet.http.HttpServletResponse` do objeto `getInputStream`.
   * Crie um objeto `java.io.ByteArrayOutputStream` usando seu construtor e transmitindo o comprimento do objeto `java.io.InputStream`.
   * Copie o conteúdo do objeto `java.io.InputStream` no objeto `java.io.ByteArrayOutputStream`.
   * Crie uma matriz de bytes chamando o método `java.io.ByteArrayOutputStream` do objeto `toByteArray`.
   * Preencha o objeto `BLOB` invocando seu método `setBinaryData` e transmitindo a matriz de bytes como um argumento.
   * Crie um objeto `RenderOptionsSpec` usando seu construtor. Defina o valor da localidade chamando o método `RenderOptionsSpec` do objeto `setLocale` e transmitindo um valor de string que especifica o valor da localidade.
   * Chame o método `FormsServiceClient` do objeto `processFormSubmission` e passe os seguintes valores:

      * O objeto `BLOB` que contém os dados do formulário.
      * Um valor de string que especifica variáveis de ambiente incluía todos os cabeçalhos HTTP relevantes. Por exemplo, você pode especificar o seguinte valor de string: `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * Um valor de string que especifica o valor do cabeçalho `HTTP_USER_AGENT`; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Um objeto `RenderOptionsSpec` que armazena opções de tempo de execução. Para obter mais informações, .
      * Um objeto vazio `BLOBHolder` que é preenchido pelo método.
      * Um objeto vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pelo método.
      * Um objeto vazio `BLOBHolder` que é preenchido pelo método.
      * Um objeto vazio `BLOBHolder` que é preenchido pelo método.
      * Um objeto vazio `javax.xml.rpc.holders.ShortHolder` que é preenchido pelo método.
      * Um objeto vazio `MyArrayOf_xsd_anyTypeHolder` que é preenchido pelo método. Esse parâmetro é usado para armazenar anexos de arquivo enviados junto com o formulário.
      * Um objeto vazio `FormsResultHolder` que é preenchido pelo método com o formulário enviado.

      O método `processFormSubmission` preenche o parâmetro `FormsResultHolder` com os resultados do envio do formulário. O método `processFormSubmission` retorna um objeto `FormsResult` contendo os resultados do envio do formulário.

   * Verifique se o estado de processamento associado a um formulário enviado é `1` chamando o método `FormsResult` do objeto `getAction`. Se esse método retornar o valor `1`, o cálculo foi executado e os dados podem ser gravados de volta no navegador da Web do cliente.


1. Gravar o fluxo de dados do formulário de volta no navegador da Web do cliente

   * Crie um objeto `javax.servlet.ServletOutputStream` usado para enviar um fluxo de dados de formulário para o navegador da Web do cliente.
   * Crie um objeto `BLOB` que contenha dados de formulário chamando o método `FormsResult` do objeto `getOutputContent`.
   * Crie uma matriz de bytes e preencha-a chamando o método `BLOB` do objeto `getBinaryData`. Essa tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Chame o método `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte**
[tambémInvocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
