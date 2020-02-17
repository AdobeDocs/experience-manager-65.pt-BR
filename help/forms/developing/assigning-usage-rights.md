---
title: Atribuindo direitos de uso
seo-title: Atribuindo direitos de uso
description: 'null'
seo-description: 'null'
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Atribuindo direitos de uso {#assigning-usage-rights}

## Sobre o serviço de extensões do Acrobat Reader DC {#about-the-acrobat-reader-dc-extensions-service}

O serviço de extensões do Acrobat Reader DC permite que sua organização compartilhe facilmente documentos PDF interativos estendendo a funcionalidade do Adobe Reader. O serviço de extensões do Acrobat Reader DC oferece suporte total a qualquer documento PDF, até PDF 1.7 inclusive. Funciona com o Adobe Reader 7.0 e posterior. O serviço adiciona direitos de uso a um documento PDF, ativando recursos que geralmente não estão disponíveis quando um documento PDF é aberto usando o Adobe Reader. Usuários de terceiros não exigem software ou plug-ins adicionais para trabalhar com os documentos habilitados por direitos.

É possível realizar essas tarefas usando o serviço de extensões do Acrobat Reader DC:

* Aplique direitos de uso a documentos PDF. Para obter informações, consulte [Aplicar direitos de uso a documentos](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)PDF.
* Remova os direitos de uso de documentos PDF. Para obter informações, consulte [Remoção de direitos de uso de documentos](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)PDF.
* Recuperar detalhes da credencial. Para obter informações, consulte [Recuperando informações](assigning-usage-rights.md#retrieving-credential-information)de credenciais.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de extensões do Acrobat Reader DC, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

## Aplicar direitos de uso a documentos PDF {#applying-usage-rights-to-pdf-documents}

Você pode aplicar direitos de uso a documentos PDF usando a API Java Client e o serviço da Web do Acrobat Reader DC extensões. Os direitos de uso pertencem à funcionalidade que está disponível por padrão no Acrobat, mas não no Adobe Reader, como a capacidade de adicionar comentários a um formulário ou preencher campos de formulário e salvar o formulário. Os documentos PDF que têm direitos de uso aplicados a eles são chamados de documentos habilitados por direitos. Um usuário que abre um documento habilitado para direitos no Adobe Reader pode executar operações ativadas para esse documento específico.

>[!NOTE]
>
>Ao aplicar direitos de uso a documentos PDF usando o `applyUsageRights` método, que faz parte da API Java, é possível definir o `isModeFinal` parâmetro do `ReaderExtensionsOptionSpec` objeto como `false`. Isso resulta na atualização do contador de formulários processados e na melhoria do desempenho. Se você não estiver preocupado com a atualização do contador de formulários processados, é recomendável definir o `isModeFinal` parâmetro como `false`.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de extensões do Acrobat Reader DC, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary-of-steps}

Para aplicar direitos de uso a um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto Cliente de extensões do Acrobat Reader DC.
1. Recuperar um documento PDF.
1. Especifique os direitos de uso a serem aplicados.
1. Aplique direitos de uso ao documento PDF.
1. Salve o documento PDF com direitos ativados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto Cliente de extensões do Acrobat Reader DC**

Para executar programaticamente uma operação de serviço de extensões do Acrobat Reader DC, é necessário criar um objeto cliente de serviço de extensões do Acrobat Reader DC. Se você estiver usando a API Java de extensões do Acrobat Reader DC, crie um `ReaderExtensionsServiceClient` objeto. Se você estiver usando a API de serviço da Web de extensões do Acrobat Reader DC, crie um `ReaderExtensionsServiceService` objeto.

**Recuperar um documento PDF**

Você deve recuperar um documento PDF para aplicar direitos de uso. Documentos PDF com direitos ativados contêm um dicionário de direitos de uso. Quando o Adobe Reader abre um documento que contém esse dicionário, ele ativa os direitos de uso especificados no dicionário apenas para esse documento. Se o documento não contiver um dicionário de direitos de uso, o serviço de extensões do Acrobat Reader DC criará um. Se já contiver um dicionário, o serviço de extensões do Acrobat Reader DC substituirá os direitos de uso existentes pelos direitos especificados. O dicionário especifica quais direitos de uso estão ativados. Quando um usuário abre o documento no Adobe Reader, somente os direitos de uso especificados no dicionário são permitidos.

**Especificar direitos de uso a serem aplicados**

Os direitos de uso que você pode definir são determinados por uma credencial que você compra da Adobe Systems Incorporated. Normalmente, as credenciais fornecem permissão para definir um grupo de direitos de uso relacionados, como os que pertencem a formulários interativos. Cada credencial fornece o direito de criar um determinado número de documentos PDF com direitos ativados. Uma credencial de avaliação dá o direito de criar um número ilimitado de documentos de rascunho.

>[!NOTE]
>
>Se você tentar atribuir um direito de uso que não é permitido por sua credencial, causará uma exceção.

**Aplicar direitos de uso ao documento PDF**

Para aplicar direitos de uso a um documento PDF, consulte o alias da credencial que você está usando para aplicar direitos de uso (uma credencial geralmente é instalada durante a instalação do AEM Forms). Também é necessário especificar o documento PDF ao qual os direitos de uso são aplicados. Para obter informações sobre como configurar uma credencial, consulte o guia de instalação e implantação do servidor de aplicativos.

**Salvar o documento PDF com direitos ativados**

Depois que o serviço de extensões do Acrobat Reader DC aplicar direitos de uso a um documento PDF, você poderá salvar o documento PDF habilitado para direitos como um arquivo PDF.

**Consulte também:**

[Aplicar direitos de uso usando a API Java](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Aplicar direitos de uso usando a API de serviço da Web](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Acrobat Reader DC Extensions Service](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Aplicar direitos de uso usando a API Java {#apply-usage-rights-using-the-java-api}

Aplique direitos de uso a um documento PDF usando a API de extensões do Acrobat Reader DC (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-reader-extensions-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `ReaderExtensionsServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recuperar um documento PDF.

   * Crie um `java.io.FileInputStream` objeto que represente o documento PDF usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Especifique os direitos de uso a serem aplicados.

   * Crie um `UsageRights` objeto que represente direitos de uso usando seu construtor.
   * Para cada direito de uso a ser aplicado, chame um método correspondente que pertence ao `UsageRights` objeto. Por exemplo, para adicionar o direito de `enableFormFillIn` uso, chame o `UsageRights` método do objeto e passe `enableFormFillIn` `true`. (Repita essa etapa para cada direito de uso a ser aplicado).

1. Aplique direitos de uso ao documento PDF.

   * Crie um `ReaderExtensionsOptionSpec` objeto usando seu construtor. Este objeto contém opções de tempo de execução exigidas pelo serviço de extensões do Acrobat Reader DC. Ao invocar esse construtor, você deve especificar os seguintes valores:

      * O `UsageRights` objeto que contém os direitos de uso a serem aplicados ao documento.
      * Um valor de string que especifica uma mensagem que um usuário vê quando o documento PDF habilitado para direitos é aberto no Adobe Reader 7.x. Esta mensagem não é exibida no Adobe Reader 8.0.
   * Aplique direitos de uso ao documento PDF, chamando o método do `ReaderExtensionsServiceClient` objeto `applyUsageRights` e transmitindo os seguintes valores:

      * O `com.adobe.idp.Document` objeto que contém o documento PDF ao qual os direitos de uso são aplicados.
      * Um valor de string que especifica o alias da credencial que permite aplicar direitos de uso.
      * Um valor de string que especifica o valor de senha correspondente. (Atualmente, esse parâmetro é ignorado. Você pode passar `null`.)
   * O `ReaderExtensionsOptionSpec` objeto que contém opções de tempo de execução.
   O `applyUsageRights` método retorna um `com.adobe.idp.Document` objeto que contém o documento PDF com direitos ativados.

1. Salve o documento PDF com direitos ativados.

   * Crie um `java.io.File` objeto e verifique se a extensão do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` método do `copyToFile` objeto para copiar o conteúdo do `com.adobe.idp.Document` objeto para o arquivo (certifique-se de usar o `com.adobe.idp.Document` objeto retornado pelo `applyUsageRights` método).

**Consulte também:**

[Aplicar direitos de uso a documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Início rápido (modo SOAP):Aplicar direitos de uso usando a API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplicar direitos de uso usando a API de serviço da Web {#apply-usage-rights-using-the-web-service-api}

Aplique direitos de uso a um documento PDF usando a Acrobat Reader DC Extensions API (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   * Crie um `ReaderExtensionsServiceClient` objeto usando seu construtor padrão.
   * Crie um `ReaderExtensionsServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Certifique-se de especificar `?blob=mtom`.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `ReaderExtensionsServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperar um documento PDF.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar um documento PDF ao qual os direitos de uso são aplicados.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` objeto `Read` . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` objeto atribuindo sua `MTOM` propriedade ao conteúdo da matriz de bytes.

1. Especifique os direitos de uso a serem aplicados.

   * Crie um `UsageRights` objeto que represente direitos de uso usando seu construtor.
   * Para cada direito de uso a ser aplicado, atribua o valor `true` ao membro de dados correspondente que pertence ao `UsageRights` objeto. Por exemplo, para adicionar o direito de `enableFormFillIn` uso, atribua `true` ao membro de `UsageRights` dados do `enableFormFillIn` objeto. (Repita essa etapa para cada direito de uso a ser aplicado).

1. Aplique direitos de uso ao documento PDF.

   * Crie um `ReaderExtensionsOptionSpec` objeto usando seu construtor. Este objeto contém opções de tempo de execução exigidas pelo serviço de extensões do Acrobat Reader DC.
   * Atribua o `UsageRights` objeto ao membro de `ReaderExtensionsOptionSpec` dados do `usageRights` objeto.
   * Atribua um valor de string que especifica a mensagem que um usuário vê quando o documento PDF habilitado para direitos é aberto no Adobe Reader para o membro de `ReaderExtensionsOptionSpec` dados do `message` objeto.
   * Aplique direitos de uso ao documento PDF, chamando o método do `ReaderExtensionsServiceClient` objeto `applyUsageRights` e transmitindo os seguintes valores:

      * O `BLOB` objeto que contém o documento PDF ao qual os direitos de uso são aplicados.
      * Um valor de string que especifica o alias da credencial que permite aplicar direitos de uso.
      * Um valor de string que especifica o valor de senha correspondente. (Atualmente, esse parâmetro é ignorado. Você pode passar `null`.)
   * O `ReaderExtensionsOptionSpec` objeto que contém opções de tempo de execução.
   O `applyUsageRights` método retorna um `BLOB` objeto que contém o documento PDF com direitos ativados.

1. Salve o documento PDF com direitos ativados.

   * Crie um `System.IO.FileStream` objeto chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF habilitado para direitos.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `applyUsageRights` método. Preencha a matriz de bytes obtendo o valor do membro de `BLOB` dados do `MTOM` objeto.
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método do `System.IO.BinaryWriter` objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Aplicar direitos de uso a documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Invocar formulários AEM usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Remoção de direitos de uso de documentos PDF {#removing-usage-rights-from-pdf-documents}

Você pode remover direitos de uso de um documento habilitado para direitos. A remoção de direitos de uso de um documento PDF habilitado para direitos também é necessária para executar outras operações do AEM Forms nele. Por exemplo, você deve assinar digitalmente (ou certificar) um documento PDF antes de definir direitos de uso. Portanto, se você quiser executar operações em um documento com direitos ativados, remova os direitos de uso do documento PDF, execute as outras operações, como assinar digitalmente o documento e aplique novamente os direitos de uso ao documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de extensões do Acrobat Reader DC, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary_of_steps-1}

Para remover direitos de uso de um documento PDF com direitos ativados, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto Cliente de extensões do Acrobat Reader DC.
1. Recupere um documento PDF com direitos ativados.
1. Remova os direitos de uso do documento PDF.
1. Salve o documento PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto Cliente de extensões do Acrobat Reader DC**

Antes de executar programaticamente uma operação de serviço de extensões do Acrobat Reader DC, é necessário criar um objeto cliente de serviço de extensões do Acrobat Reader DC. Se você estiver usando a API Java, crie um `ReaderExtensionsServiceClient` objeto. Se você estiver usando a API de serviço da Web de extensões do Acrobat Reader DC, crie um `ReaderExtensionsServiceService` objeto.

**Recuperar um documento PDF com direitos**

Recupere um documento PDF com direitos ativados para remover direitos de uso.

**Remover direitos de uso do documento PDF**

Depois de recuperar um documento PDF com direitos ativados, você pode remover direitos de uso. Após remover os direitos de uso, o documento PDF não terá nenhuma funcionalidade adicional enquanto for visualizado no Adobe Reader.

**Salvar o documento PDF**

É possível salvar o documento PDF que não contém mais direitos de uso como um arquivo PDF. Depois de salvo como um arquivo PDF, o documento PDF pode ser exibido no Adobe Reader ou no Acrobat.

**Consulte também:**

[Remova os direitos de uso usando a API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Remover direitos de uso usando a API de serviço da Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Acrobat Reader DC Extensions Service](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Aplicar direitos de uso a documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Remova os direitos de uso usando a API Java {#remove-usage-rights-using-the-java-api}

Remova os direitos de uso de um documento PDF com direitos ativados usando a API de extensões do Acrobat Reader DC (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-reader-extensions-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   Crie um `ReaderExtensionsServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contenha propriedades de conexão.

1. Recuperar um documento PDF.

   * Crie um `java.io.FileInputStream` objeto que represente o documento PDF com direitos ativados usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Remova os direitos de uso do documento PDF.

   Remova os direitos de uso do documento PDF invocando o `ReaderExtensionsServiceClient` método do objeto `removeUsageRights` e transmitindo o `com.adobe.idp.Document` objeto que contém o documento PDF habilitado para direitos. Esse método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF que não tem direitos de uso.

1. Aplique direitos de uso ao documento PDF.

   * Crie um `java.io.File` objeto e verifique se a extensão do arquivo é .PDF.
   * Chame o `Document` método do `copyToFile` objeto para copiar o conteúdo do `Document` objeto para o arquivo (certifique-se de usar o `Document` objeto retornado pelo `removeUsageRights` método).

**Consulte também:**

[Remoção de direitos de uso de documentos PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Início rápido (modo SOAP): Remoção de direitos de uso de um documento PDF usando a API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Remover direitos de uso usando a API de serviço da Web {#remove-usage-rights-using-the-web-service-api}

Remova os direitos de uso de um documento PDF com direitos ativados usando a API de extensões do Acrobat Reader DC (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   * Crie um `ReaderExtensionsServiceClient` objeto usando seu construtor padrão.
   * Crie um `ReaderExtensionsServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Certifique-se de especificar `?blob=mtom`.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `ReaderExtensionsServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperar um documento PDF.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento PDF com direitos ativados a partir do qual os direitos de uso são removidos.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo sua `MTOM` propriedade ao conteúdo da matriz de bytes.

1. Remova os direitos de uso do documento PDF.

   Remova os direitos de uso do documento PDF invocando o `ReaderExtensionsServiceClient` método do objeto `removeUsageRights` e transmitindo o `BLOB` objeto que contém o documento PDF habilitado para direitos. Esse método retorna um `BLOB` objeto que contém um documento PDF que não tem direitos de uso.

1. Aplique direitos de uso ao documento PDF.

   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo PDF.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `removeUsageRights` método. Preencha a matriz de bytes obtendo o valor do membro de `BLOB` dados do `MTOM` objeto.
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.

**Consulte também:**

[Remoção de direitos de uso de documentos PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Invocar formulários AEM usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recuperando Informações de Credenciais {#retrieving-credential-information}

Você pode recuperar informações sobre a credencial usada para aplicar direitos de uso a um documento PDF com direitos ativados. Ao recuperar informações sobre uma credencial, você pode obter informações como a data após a qual o certificado não é mais válido.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de extensões do Acrobat Reader DC, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary_of_steps-2}

Para recuperar informações sobre a credencial usada para aplicar direitos de uso a um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto Cliente de extensões do Acrobat Reader DC.
1. Recupere um documento PDF com direitos ativados.
1. Recuperar informações sobre a credencial.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto Cliente de extensões do Acrobat Reader DC**

Antes de executar programaticamente uma operação de serviço de extensões do Acrobat Reader DC, é necessário criar um objeto cliente de serviço de extensões do Acrobat Reader DC. Se você estiver usando a API Java, crie um `ReaderExtensionsServiceClient` objeto. Se você estiver usando a API de serviço da Web de extensões do Acrobat Reader DC, crie um `ReaderExtensionsServiceService` objeto.

**Recuperar um documento PDF com direitos**

Você deve recuperar um documento PDF com direitos ativados para recuperar informações sobre a credencial. Você também pode recuperar informações sobre uma credencial especificando seu alias; no entanto, se você quiser recuperar informações sobre uma credencial que foi usada para aplicar direitos de uso a um documento PDF habilitado para direitos específicos, recupere o documento.

**Recuperar informações sobre a credencial**

Depois de recuperar um documento PDF com direitos ativados, você pode obter informações sobre a credencial usada para aplicar direitos de uso a ele. Você pode obter as seguintes informações sobre a credencial:

* A mensagem que é exibida no Adobe Reader quando o documento PDF com direitos ativados é aberto.
* A data após a qual a credencial não é mais válida.
* A data antes da qual a credencial não é válida.
* Os direitos de uso que foram definidos para este documento PDF com direitos ativados.
* O número de vezes que a credencial foi usada.

**Consulte também:**

[Remova os direitos de uso usando a API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Remover direitos de uso usando a API de serviço da Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Acrobat Reader DC Extensions Service](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Recuperar informações de credenciais usando a API Java {#retrieve-credential-information-using-the-java-api}

Recupere informações de credenciais usando a API de extensões do Acrobat Reader DC (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-reader-extensions-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   Crie um `ReaderExtensionsServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contenha propriedades de conexão.

1. Recuperar um documento PDF.

   * Crie um `java.io.FileInputStream` objeto que represente o documento PDF com direitos ativados usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF com direitos ativados.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Remova os direitos de uso do documento PDF.

   * Recupere informações sobre a credencial usada para aplicar direitos de uso ao documento PDF chamando o `ReaderExtensionsServiceClient` método do `getDocumentUsageRights` objeto e transmitindo o `com.adobe.idp.Document` objeto que contém o documento PDF habilitado para direitos. Este método retorna um `GetUsageRightsResult` objeto que contém informações de credenciais.
   * Recupere a data após a qual a credencial não é mais válida invocando o `GetUsageRightsResult` método do `getNotAfter` objeto. Este método retorna um `java.util.Date` objeto que representa a data após a qual a credencial não é mais válida.
   * Recupere a mensagem que é exibida no Adobe Reader quando o documento PDF habilitado para direitos é aberto chamando o `GetUsageRightsResult` método do `getMessage` objeto. Esse método retorna um valor de string que representa a mensagem.

**Consulte também:**

[Recuperando Informações de Credenciais](assigning-usage-rights.md#retrieving-credential-information)

[Início rápido (modo SOAP): Recuperando informações de credenciais usando a API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar informações de credenciais usando a API de serviço da Web {#retrieve-credential-information-using-the-web-service-api}

Recupere informações de credenciais usando a API de extensões do Acrobat Reader DC (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   * Crie um `ReaderExtensionsServiceClient` objeto usando seu construtor padrão.
   * Crie um `ReaderExtensionsServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Certifique-se de especificar `?blob=mtom`.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `ReaderExtensionsServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperar um documento PDF.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar um documento PDF com direitos ativados.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF habilitado para direitos e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo sua `MTOM` propriedade ao conteúdo da matriz de bytes.

1. Remova os direitos de uso do documento PDF.

   * Recupere informações sobre a credencial usada para aplicar direitos de uso ao documento PDF chamando o `ReaderExtensionsServiceClient` método do `getDocumentUsageRights` objeto e transmitindo o `com.adobe.idp.Document` objeto que contém o documento PDF habilitado para direitos. Este método retorna um `GetUsageRightsResult` objeto que contém informações de credenciais.
   * Recupere a data após a qual a credencial não é mais válida obtendo o valor do membro de `GetUsageRightsResult` dados do `notAfter` objeto. O tipo de dados desse membro de dados é `System.DateTime`.
   * Recupere a mensagem que é exibida quando o documento PDF com direitos ativados é aberto no Adobe Reader obtendo o valor do membro de `GetUsageRightsResult` dados do `message` objeto. O tipo de dados desse membro de dados é uma string.
   * Recupere o número de vezes que a credencial é usada obtendo o valor do membro de `GetUsageRightsResult` dados do `useCount` objeto. O tipo de dados desse membro de dados é um número inteiro.

**Consulte também:**

[Recuperando Informações de Credenciais](assigning-usage-rights.md#retrieving-credential-information)

[Invocar formulários AEM usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
