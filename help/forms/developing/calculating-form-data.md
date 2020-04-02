---
title: Calculando dados do formulário
seo-title: Calculando dados do formulário
description: 'null'
seo-description: 'null'
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
translation-type: tm+mt
source-git-commit: 2e4b8ee13257758cba6b76012fed4958f7eabbd7

---


# Calculando dados do formulário {#calculating-form-data}

O serviço Forms pode calcular os valores que um usuário digita em um formulário e exibir os resultados. Para calcular os dados do formulário, é necessário executar duas tarefas. Primeiro, crie um script de design de formulário que calcule os dados do formulário. Um design de formulário suporta três tipos de scripts. Um tipo de script é executado no cliente, outro é executado no servidor e o terceiro tipo é executado no servidor e no cliente. O tipo de script discutido neste tópico é executado no servidor. Cálculos do lado do servidor são suportados para transformações HTML, PDF e Guia de formulário (obsoleto).

Como parte do processo de design de formulário, você pode usar cálculos e scripts para proporcionar uma experiência mais avançada ao usuário. Cálculos e scripts podem ser adicionados à maioria dos campos e objetos de formulário. É necessário criar um script de design de formulário para executar operações de cálculo nos dados inseridos pelo usuário em um formulário interativo.

O usuário insere valores no formulário e clica no botão Calcular para visualização dos resultados. O processo a seguir descreve um exemplo de aplicativo que permite que um usuário calcule dados:

* O usuário acessa uma página HTML chamada StartLoan.html que atua como a página de start do aplicativo da Web. Esta página chama um Servlet Java chamado `GetLoanForm`.
* O `GetLoanForm` servlet renderiza um formulário de empréstimo. Este formulário contém um script, campos interativos, um botão calcular e um botão enviar.
* O usuário insere valores nos campos do formulário e clica no botão Calcular. O formulário é enviado para o `CalculateData` Java Servlet onde o script é executado. O formulário é enviado de volta ao usuário com os resultados do cálculo exibidos no formulário.
* O usuário continua inserindo e calculando valores até que um resultado satisfatório seja exibido. Quando satisfeito, o usuário clica no botão Enviar para processar o formulário. O formulário é enviado para outro Java Servlet `ProcessForm` que é responsável pela recuperação dos dados enviados. (Consulte [Manuseio De Formulários](/help/forms/developing/rendering-forms.md#handling-submitted-forms)Enviados.)


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
   <td><p>O <code>GetLoanForm</code> Java Servlet é chamado da página do start HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>O <code>GetLoanForm</code> Java Servlet usa a API do cliente de serviço do Forms para renderizar o formulário de empréstimo no navegador da Web do cliente. A diferença entre a renderização de um formulário que contém um script configurado para execução no servidor e a renderização de um formulário que não contém um script é que é necessário especificar o local do público alvo usado para executar o script. Se um local de público alvo não for especificado, um script configurado para execução no servidor não será executado. Por exemplo, considere o aplicativo apresentado nesta seção. O Servlet <code>CalculateData</code> Java é o local do público alvo onde o script é executado.</p></td>
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

Normalmente, um formulário enviado como conteúdo PDF contém scripts executados no cliente. No entanto, os cálculos do lado do servidor também podem ser executados. Um botão Enviar não pode ser usado para calcular scripts. Nessa situação, os cálculos não são executados porque o serviço do Forms considera a interação concluída.

Para ilustrar o uso de um script de design de formulário, esta seção examina um formulário interativo simples que contém um script configurado para execução no servidor. O diagrama a seguir mostra um design de formulário contendo um script que adiciona valores que um usuário digita nos dois primeiros campos e exibe o resultado no terceiro campo.

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.** Um campo chamado NumericField1 **B.** Um campo chamado NumericField2 **C.** Um campo chamado NumericField3

A sintaxe do script localizado neste design de formulário é a seguinte:

```as3
     NumericField3 = NumericField2 + NumericField1
```

Nesse design de formulário, o botão Calcular é um botão de comando e o script está localizado no `Click` evento desse botão. Quando um usuário digita valores nos dois primeiros campos (NumericField1 e NumericField2) e clica no botão Calcular, o formulário é enviado para o serviço de Formulários, onde o script é executado. O serviço Forms renderiza o formulário de volta ao dispositivo cliente com os resultados do cálculo exibidos no campo NumericField3.

>[!NOTE]
>
>Para obter informações sobre como criar um script de design de formulário, consulte [Designer](https://www.adobe.com/go/learn_aemforms_designer_63)de formulários.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Formulários, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

## Resumo das etapas {#summary-of-steps}

Para calcular os dados do formulário, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Forms Client.
1. Recupere um formulário contendo um script de cálculo.
1. Gravar o fluxo de dados do formulário de volta no navegador da Web do cliente

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente Forms**

Antes de executar programaticamente uma operação de API do cliente do serviço Forms, é necessário criar um cliente do serviço Forms. Se você estiver usando a API Java, crie um `FormsServiceClient` objeto. Se você estiver usando a API de serviço da Web do Forms, crie um `FormsServiceService` objeto.

**Recuperar um formulário contendo um script de cálculo**

Use a API do cliente do serviço Forms para criar uma lógica de aplicativo que manipule um formulário que contenha um script configurado para execução no servidor. O processo é semelhante ao manuseio de um formulário enviado. (Consulte [Manuseio De Formulários](/help/forms/developing/handling-submitted-forms.md)Enviados.)

Verifique se o estado de processamento associado ao formulário enviado é `1` `(Calculate)`, o que significa que o serviço Forms está executando uma operação de cálculo nos dados do formulário e os resultados devem ser gravados de volta no usuário. Nessa situação, um script configurado para execução no servidor é executado automaticamente.

**Gravar o fluxo de dados do formulário de volta no navegador da Web do cliente**

Depois de verificar se o estado de processamento associado a um formulário enviado está `1`, você deve gravar os resultados de volta no navegador da Web do cliente. Quando o formulário for exibido, o valor calculado aparecerá nos campos apropriados.

**Consulte também:**

[Incluindo arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms[Calcule os dados do formulário usando a API](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)Java[Calcule os dados do formulário usando a API](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)do serviço da Web[Configurando propriedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexão API do serviço[Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)[](/help/forms/developing/rendering-interactive-pdf-forms.md)[Rápido Renderizando formulários PDF interativosComo criar Aplicações web que renderizam formulários](/help/forms/developing/creating-web-applications-renders-forms.md)

## Calcular dados de formulário usando a API Java {#calculate-form-data-using-the-java-api}

Calcule os dados do formulário usando a API de formulários (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto da API do cliente Forms

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `FormsServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recuperar um formulário contendo um script de cálculo

   * Para recuperar dados de formulário que contenham um script de cálculo, crie um `com.adobe.idp.Document` objeto usando seu construtor e chamando o `javax.servlet.http.HttpServletResponse` `getInputStream` método do objeto de dentro do construtor.
   * Chame o método do `FormsServiceClient` objeto `processFormSubmission` e passe os seguintes valores:

      * O `com.adobe.idp.Document` objeto que contém os dados do formulário.
      * Um valor de string que especifica variáveis de ambiente, incluindo todos os cabeçalhos HTTP relevantes. É necessário especificar o tipo de conteúdo a ser tratado especificando um ou mais valores para a variável de `CONTENT_TYPE` ambiente. Por exemplo, para manipular dados XML e PDF, especifique o seguinte valor de string para esse parâmetro: `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * Um valor de string que especifica o valor do `HTTP_USER_AGENT` cabeçalho; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Um `RenderOptionsSpec` objeto que armazena opções de tempo de execução.
      O `processFormSubmission` método retorna um `FormsResult` objeto que contém os resultados do envio do formulário.

   * Verifique se o estado de processamento associado a um formulário enviado é `1` chamando o `FormsResult` método do `getAction` objeto. Se esse método retornar o valor `1`, o cálculo será executado e os dados poderão ser gravados de volta no navegador da Web do cliente.


1. Gravar o fluxo de dados do formulário de volta no navegador da Web do cliente

   * Crie um `javax.servlet.ServletOutputStream` objeto usado para enviar um fluxo de dados de formulário para o navegador da Web do cliente.
   * Crie um `com.adobe.idp.Document` objeto chamando o `FormsResult` método do objeto `getOutputContent` .
   * Crie um `java.io.InputStream` objeto chamando o `com.adobe.idp.Document` método do `getInputStream` objeto.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, invocando o método do `InputStream` objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o método do `javax.servlet.ServletOutputStream` `write` objeto para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o `write` método.

**Consulte também:**


[Incluindo arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms[Configuração de propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Calcular dados de formulário usando a API de serviço da Web {#calculate-form-data-using-the-web-service-api}

Calcule os dados do formulário usando a API de formulários (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o serviço Forms WSDL.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto da API do cliente Forms

   Crie um `FormsService` objeto e defina valores de autenticação.

1. Recuperar um formulário contendo um script de cálculo

   * Para recuperar dados de formulário publicados em um Java Servlet, crie um `BLOB` objeto usando seu construtor.
   * Crie um `java.io.InputStream` objeto usando o `javax.servlet.http.HttpServletResponse` método do `getInputStream` objeto.
   * Crie um `java.io.ByteArrayOutputStream` objeto usando seu construtor e transmitindo o comprimento do `java.io.InputStream` objeto.
   * Copie o conteúdo do `java.io.InputStream` objeto no `java.io.ByteArrayOutputStream` objeto.
   * Crie uma matriz de bytes chamando o `java.io.ByteArrayOutputStream` método do `toByteArray` objeto.
   * Preencha o `BLOB` objeto chamando seu `setBinaryData` método e transmitindo a matriz de bytes como um argumento.
   * Crie um `RenderOptionsSpec` objeto usando seu construtor. Defina o valor da localidade chamando o método do `RenderOptionsSpec` `setLocale` objeto e transmitindo um valor de string que especifica o valor da localidade.
   * Chame o método do `FormsServiceClient` objeto `processFormSubmission` e passe os seguintes valores:

      * O `BLOB` objeto que contém os dados do formulário.
      * Um valor de string que especifica variáveis de ambiente incluía todos os cabeçalhos HTTP relevantes. Por exemplo, você pode especificar o seguinte valor de string: `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * Um valor de string que especifica o valor do `HTTP_USER_AGENT` cabeçalho; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Um `RenderOptionsSpec` objeto que armazena opções de tempo de execução. Para obter mais informações, .
      * Um `BLOBHolder` objeto vazio que é preenchido pelo método.
      * Um `javax.xml.rpc.holders.StringHolder` objeto vazio que é preenchido pelo método.
      * Um `BLOBHolder` objeto vazio que é preenchido pelo método.
      * Um `BLOBHolder` objeto vazio que é preenchido pelo método.
      * Um `javax.xml.rpc.holders.ShortHolder` objeto vazio que é preenchido pelo método.
      * Um `MyArrayOf_xsd_anyTypeHolder` objeto vazio que é preenchido pelo método. Esse parâmetro é usado para armazenar anexos de arquivo enviados junto com o formulário.
      * Um `FormsResultHolder` objeto vazio que é preenchido pelo método com o formulário enviado.
      O `processFormSubmission` método preenche o `FormsResultHolder` parâmetro com os resultados do envio do formulário. O `processFormSubmission` método retorna um `FormsResult` objeto que contém os resultados do envio do formulário.

   * Verifique se o estado de processamento associado a um formulário enviado é `1` chamando o `FormsResult` método do `getAction` objeto. Se esse método retornar o valor `1`, o cálculo será executado e os dados poderão ser gravados de volta no navegador da Web do cliente.


1. Gravar o fluxo de dados do formulário de volta no navegador da Web do cliente

   * Crie um `javax.servlet.ServletOutputStream` objeto usado para enviar um fluxo de dados de formulário para o navegador da Web do cliente.
   * Crie um `BLOB` objeto que contenha dados de formulário chamando o `FormsResult` método do `getOutputContent` objeto.
   * Crie uma matriz de bytes e preencha-a chamando o método do `BLOB` objeto `getBinaryData` . Essa tarefa atribui o conteúdo do `FormsResult` objeto à matriz de bytes.
   * Chame o método do `javax.servlet.http.HttpServletResponse` `write` objeto para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o `write` método.

**Consulte também**[Invocar formulários AEM usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
