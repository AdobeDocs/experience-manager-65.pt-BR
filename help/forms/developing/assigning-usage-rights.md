---
title: Atribuindo direitos de uso
seo-title: Atribuindo direitos de uso
description: 'null'
seo-description: nulo
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7
workflow-type: tm+mt
source-wordcount: '3895'
ht-degree: 0%

---


# Atribuindo direitos de uso {#assigning-usage-rights}

## Sobre o Serviço de extensões do Acrobat Reader DC {#about-the-acrobat-reader-dc-extensions-service}

O serviço de extensões da Acrobat Reader DC permite que sua organização compartilhe com facilidade documentos PDF interativos estendendo a funcionalidade da Adobe Reader. O serviço de extensões da Acrobat Reader DC oferece suporte total a qualquer documento PDF, até PDF 1.7 inclusive. Funciona com o Adobe Reader 7.0 e posterior. O serviço adiciona direitos de uso a um documento PDF, ativando recursos que geralmente não estão disponíveis quando um documento PDF é aberto usando o Adobe Reader. Usuários de terceiros não exigem software ou plug-ins adicionais para trabalhar com os documentos habilitados para direitos.

É possível realizar essas tarefas usando o serviço de extensões Acrobat Reader DC:

* Aplique direitos de uso a documentos PDF. Para obter informações, consulte [Aplicando direitos de uso a Documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* Remova os direitos de uso de documentos PDF. Para obter informações, consulte [Remoção de direitos de uso de Documentos PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* Recuperar detalhes da credencial. Para obter informações, consulte [Recuperando Informações de Credenciais](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Para obter mais informações sobre o serviço de extensões do Acrobat Reader DC, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Aplicar direitos de uso a Documentos PDF {#applying-usage-rights-to-pdf-documents}

Você pode aplicar direitos de uso a documentos PDF usando a API Java Client de extensões da Acrobat Reader DC e o serviço da Web. Os direitos de uso pertencem à funcionalidade que está disponível por padrão no Acrobat, mas não no Adobe Reader, como a capacidade de adicionar comentários a um formulário ou preencher campos de formulário e salvar o formulário. DOCUMENTOS PDF que têm direitos de uso aplicados a eles são chamados de documentos habilitados por direitos. Um usuário que abre um documento habilitado para direitos no Adobe Reader pode executar operações ativadas para esse documento específico.

>[!NOTE]
>
>Ao aplicar direitos de uso a documentos PDF usando o método `applyUsageRights`, que faz parte da API Java, você pode definir o parâmetro `isModeFinal` do objeto `ReaderExtensionsOptionSpec` como `false`. Isso resulta na atualização do contador de formulários processados e na melhoria do desempenho. Se você não estiver preocupado com a atualização do contador de formulários processados, é recomendável definir o parâmetro `isModeFinal` como `false`.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de extensões do Acrobat Reader DC, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para aplicar direitos de uso a um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto Cliente de extensões do Acrobat Reader DC.
1. Recupere um documento PDF.
1. Especifique os direitos de uso a serem aplicados.
1. Aplique direitos de uso ao documento PDF.
1. Salve o documento PDF com direitos ativados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto Cliente de extensões do Acrobat Reader DC**

Para executar programaticamente uma operação do Acrobat Reader DC extensionsservice, é necessário criar um objeto cliente do serviço de extensões Acrobat Reader DC. Se você estiver usando a API Java de extensões do Acrobat Reader DC, crie um objeto `ReaderExtensionsServiceClient`. Se você estiver usando a API de serviço da Web de extensões do Acrobat Reader DC, crie um objeto `ReaderExtensionsServiceService`.

**Recuperar um documento PDF**

É necessário recuperar um documento PDF para aplicar direitos de uso. Documentos PDF com direitos ativados contêm um dicionário de direitos de uso. Quando a Adobe Reader abre um documento que contém tal dicionário, ela ativa os direitos de uso especificados no dicionário apenas para esse documento. Se o documento não contiver um dicionário de direitos de uso, o serviço de extensões da Acrobat Reader DC criará um. Se já contiver um dicionário, o serviço de extensões da Acrobat Reader DC substituirá os direitos de uso existentes pelos que você especificar. O dicionário especifica quais direitos de uso estão ativados. Quando um usuário abre o documento no Adobe Reader, somente os direitos de uso especificados no dicionário são permitidos.

**Especificar direitos de uso a serem aplicados**

Os direitos de uso que você pode definir são determinados por uma credencial que você compra da Adobe Systems Incorporated. Normalmente, as credenciais fornecem permissão para definir um grupo de direitos de uso relacionados, como os que pertencem a formulários interativos. Cada credencial fornece o direito de criar um determinado número de documentos PDF com direitos ativados. Uma credencial de avaliação dá o direito de criar um número ilimitado de documentos de rascunho.

>[!NOTE]
>
>Se você tentar atribuir um direito de uso que não é permitido por sua credencial, causará uma exceção.

**Aplicar direitos de uso ao documento PDF**

Para aplicar direitos de uso a um documento PDF, consulte o alias da credencial que você está usando para aplicar direitos de uso (uma credencial geralmente é instalada durante a instalação do AEM Forms). Além disso, você deve especificar o documento PDF ao qual os direitos de uso são aplicados. Para obter informações sobre como configurar uma credencial, consulte o guia de instalação e implantação do servidor de aplicativos.

**Salvar o documento PDF com direitos**

Depois que o serviço de extensões da Acrobat Reader DC aplicar direitos de uso a um documento PDF, é possível salvar o documento PDF com direitos ativados como um arquivo PDF.

**Consulte também:**

[Aplicar direitos de uso usando a API Java](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Aplicar direitos de uso usando a API de serviço da Web](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[start rápidos da API do Acrobat Reader DC Extensions Service](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Aplicar direitos de uso usando a API Java {#apply-usage-rights-using-the-java-api}

Aplique direitos de uso a um documento PDF usando a Acrobat Reader DC Extensions API (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-reader-extensions-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `ReaderExtensionsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recupere um documento PDF.

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Especifique os direitos de uso a serem aplicados.

   * Crie um objeto `UsageRights` que represente direitos de uso usando seu construtor.
   * Para cada direito de uso a ser aplicado, chame um método correspondente que pertença ao objeto `UsageRights`. Por exemplo, para adicionar o direito de uso `enableFormFillIn`, chame o método `UsageRights` do objeto `enableFormFillIn` e passe `true`. (Repita essa etapa para cada direito de uso a ser aplicado).

1. Aplique direitos de uso ao documento PDF.

   * Crie um objeto `ReaderExtensionsOptionSpec` usando seu construtor. Este objeto contém opções de tempo de execução exigidas pelo serviço de extensões do Acrobat Reader DC. Ao invocar esse construtor, você deve especificar os seguintes valores:

      * O objeto `UsageRights` que contém os direitos de uso a serem aplicados ao documento.
      * Um valor de string que especifica uma mensagem que um usuário vê quando o documento PDF com direitos ativados é aberto no Adobe Reader 7.x. Esta mensagem não é exibida no Adobe Reader 8.0.
   * Aplique direitos de uso ao documento PDF chamando o método `ReaderExtensionsServiceClient` do objeto `applyUsageRights` e transmitindo os seguintes valores:

      * O objeto `com.adobe.idp.Document` que contém o documento PDF ao qual os direitos de uso são aplicados.
      * Um valor de string que especifica o alias da credencial que permite aplicar direitos de uso.
      * Um valor de string que especifica o valor de senha correspondente. (Atualmente, esse parâmetro é ignorado. Você pode passar `null`.)
   * O objeto `ReaderExtensionsOptionSpec` que contém opções de tempo de execução.

   O método `applyUsageRights` retorna um objeto `com.adobe.idp.Document` que contém o documento PDF com direitos ativados.

1. Salve o documento PDF com direitos ativados.

   * Crie um objeto `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo do objeto `com.adobe.idp.Document` para o arquivo (certifique-se de usar o objeto `com.adobe.idp.Document` retornado pelo método `applyUsageRights`).

**Consulte também:**

[Aplicar direitos de uso a Documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Start rápido (modo SOAP):Aplicar direitos de uso usando a API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplicar direitos de uso usando a API de serviço da Web {#apply-usage-rights-using-the-web-service-api}

Aplique direitos de uso a um documento PDF usando a Acrobat Reader DC Extensions API (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   * Crie um objeto `ReaderExtensionsServiceClient` usando seu construtor padrão.
   * Crie um objeto `ReaderExtensionsServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Certifique-se de especificar `?blob=mtom`.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere um documento PDF.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF ao qual os direitos de uso são aplicados.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` ao conteúdo da matriz de bytes.

1. Especifique os direitos de uso a serem aplicados.

   * Crie um objeto `UsageRights` que represente direitos de uso usando seu construtor.
   * Para cada direito de uso a ser aplicado, atribua o valor `true` ao membro de dados correspondente que pertence ao objeto `UsageRights`. Por exemplo, para adicionar o direito de uso `enableFormFillIn`, atribua `true` ao membro de dados `UsageRights` do objeto `enableFormFillIn`. (Repita essa etapa para cada direito de uso a ser aplicado).

1. Aplique direitos de uso ao documento PDF.

   * Crie um objeto `ReaderExtensionsOptionSpec` usando seu construtor. Este objeto contém opções de tempo de execução exigidas pelo serviço de extensões do Acrobat Reader DC.
   * Atribua o objeto `UsageRights` ao membro de dados `ReaderExtensionsOptionSpec` do objeto `usageRights`.
   * Atribua um valor de string que especifica a mensagem que um usuário vê quando o documento PDF ativado por direitos é aberto no Adobe Reader para o membro de dados `ReaderExtensionsOptionSpec` do objeto `message`.
   * Aplique direitos de uso ao documento PDF chamando o método `ReaderExtensionsServiceClient` do objeto `applyUsageRights` e transmitindo os seguintes valores:

      * O objeto `BLOB` que contém o documento PDF ao qual os direitos de uso são aplicados.
      * Um valor de string que especifica o alias da credencial que permite aplicar direitos de uso.
      * Um valor de string que especifica o valor de senha correspondente. (Atualmente, esse parâmetro é ignorado. Você pode passar `null`.)
   * O objeto `ReaderExtensionsOptionSpec` que contém opções de tempo de execução.

   O método `applyUsageRights` retorna um objeto `BLOB` que contém o documento PDF com direitos ativados.

1. Salve o documento PDF com direitos ativados.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF com direitos ativados.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` que foi retornado pelo método `applyUsageRights`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Aplicar direitos de uso a Documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Remoção de direitos de uso de Documentos PDF {#removing-usage-rights-from-pdf-documents}

Você pode remover direitos de uso de um documento com direitos ativados. A remoção de direitos de uso de um documento PDF habilitado para direitos também é necessária para executar outras operações do AEM Forms nele. Por exemplo, você deve assinar digitalmente (ou certificar) um documento PDF antes de definir direitos de uso. Portanto, se você quiser executar operações em um documento com direitos ativados, remova os direitos de uso do documento PDF, execute as outras operações, como assinar digitalmente o documento e aplique novamente os direitos de uso ao documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de extensões do Acrobat Reader DC, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Antes de executar programaticamente uma operação de serviço de extensões do Acrobat Reader DC, você deve criar um objeto cliente de serviço de extensões do Acrobat Reader DC. Se você estiver usando a API Java, crie um objeto `ReaderExtensionsServiceClient`. Se você estiver usando a API de serviço da Web de extensões do Acrobat Reader DC, crie um objeto `ReaderExtensionsServiceService`.

**Recuperar um documento PDF com direitos**

Recupere um documento PDF com direitos ativados para remover direitos de uso.

**Remover direitos de uso do documento PDF**

Depois de recuperar um documento PDF com direitos ativados, você pode remover direitos de uso. Após remover os direitos de uso, o documento PDF não terá nenhuma funcionalidade adicional enquanto for visualizado no Adobe Reader.

**Salvar o documento PDF**

É possível salvar o documento PDF que não contém mais direitos de uso como um arquivo PDF. Depois de salvo como um arquivo PDF, o documento PDF pode ser exibido no Adobe Reader ou no Acrobat.

**Consulte também:**

[Remova os direitos de uso usando a API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Remover direitos de uso usando a API de serviço da Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[start rápidos da API do Acrobat Reader DC Extensions Service](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Aplicar direitos de uso a Documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Remova os direitos de uso usando a API Java {#remove-usage-rights-using-the-java-api}

Remova os direitos de uso de um documento PDF com direitos ativados usando a API de extensões Acrobat Reader DC (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-reader-extensions-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   Crie um objeto `ReaderExtensionsServiceClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Recupere um documento PDF.

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF com direitos ativados usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Remova os direitos de uso do documento PDF.

   Remova os direitos de uso do documento PDF chamando o método `ReaderExtensionsServiceClient` do objeto `removeUsageRights` e transmitindo o objeto `com.adobe.idp.Document` que contém o documento PDF com direitos ativados. Este método retorna um objeto `com.adobe.idp.Document` que contém um documento PDF que não tem direitos de uso.

1. Aplique direitos de uso ao documento PDF.

   * Crie um objeto `java.io.File` e verifique se a extensão do arquivo é .PDF.
   * Chame o método `Document` do objeto `copyToFile` para copiar o conteúdo do objeto `Document` para o arquivo (certifique-se de usar o objeto `Document` retornado pelo método `removeUsageRights`).

**Consulte também:**

[Remoção de direitos de uso de Documentos PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Start rápido (modo SOAP): Remoção de direitos de uso de um documento PDF usando a API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Remova os direitos de uso usando a API de serviço da Web {#remove-usage-rights-using-the-web-service-api}

Remova os direitos de uso de um documento PDF com direitos ativados usando a API de extensões do Acrobat Reader DC (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   * Crie um objeto `ReaderExtensionsServiceClient` usando seu construtor padrão.
   * Crie um objeto `ReaderExtensionsServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Certifique-se de especificar `?blob=mtom`.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere um documento PDF.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF com direitos ativados a partir do qual os direitos de uso são removidos.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` ao conteúdo da matriz de bytes.

1. Remova os direitos de uso do documento PDF.

   Remova os direitos de uso do documento PDF chamando o método `ReaderExtensionsServiceClient` do objeto `removeUsageRights` e transmitindo o objeto `BLOB` que contém o documento PDF com direitos ativados. Este método retorna um objeto `BLOB` que contém um documento PDF que não tem direitos de uso.

1. Aplique direitos de uso ao documento PDF.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo PDF.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` que foi retornado pelo método `removeUsageRights`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.

**Consulte também:**

[Remoção de direitos de uso de Documentos PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recuperando Informações de Credenciais {#retrieving-credential-information}

Você pode recuperar informações sobre a credencial usada para aplicar direitos de uso a um documento PDF com direitos ativados. Ao recuperar informações sobre uma credencial, você pode obter informações como a data após a qual o certificado não é mais válido.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de extensões do Acrobat Reader DC, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-2}

Para recuperar informações sobre a credencial usada para aplicar direitos de uso a um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto Cliente de extensões do Acrobat Reader DC.
1. Recupere um documento PDF com direitos ativados.
1. Recuperar informações sobre a credencial.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto Cliente de extensões do Acrobat Reader DC**

Antes de executar programaticamente uma operação de serviço de extensões do Acrobat Reader DC, você deve criar um objeto cliente de serviço de extensões do Acrobat Reader DC. Se você estiver usando a API Java, crie um objeto `ReaderExtensionsServiceClient`. Se você estiver usando a API de serviço da Web de extensões do Acrobat Reader DC, crie um objeto `ReaderExtensionsServiceService`.

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

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[start rápidos da API do Acrobat Reader DC Extensions Service](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Recuperar informações de credenciais usando a API Java {#retrieve-credential-information-using-the-java-api}

Recupere informações de credenciais usando a API de extensões da Acrobat Reader DC (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-reader-extensions-client.jar, no caminho da classe do seu projeto Java.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   Crie um objeto `ReaderExtensionsServiceClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Recupere um documento PDF.

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF com direitos ativados usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF com direitos ativados.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Remova os direitos de uso do documento PDF.

   * Recupere informações sobre a credencial usada para aplicar direitos de uso ao documento PDF, invocando o método `ReaderExtensionsServiceClient` do objeto `getDocumentUsageRights` e transmitindo o objeto `com.adobe.idp.Document` que contém o documento PDF habilitado para direitos. Este método retorna um objeto `GetUsageRightsResult` que contém informações de credenciais.
   * Recupere a data após a qual a credencial não é mais válida invocando o método `GetUsageRightsResult` `getNotAfter` do objeto. Este método retorna um objeto `java.util.Date` que representa a data após a qual a credencial não é mais válida.
   * Recupere a mensagem que é exibida no Adobe Reader quando o documento PDF com direitos ativados é aberto chamando o método `GetUsageRightsResult` do objeto `getMessage`. Esse método retorna um valor de string que representa a mensagem.

**Consulte também:**

[Recuperando Informações de Credenciais](assigning-usage-rights.md#retrieving-credential-information)

[Start rápido (modo SOAP): Recuperando informações de credenciais usando a API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar informações de credenciais usando a API de serviço da Web {#retrieve-credential-information-using-the-web-service-api}

Recupere informações de credenciais usando a API de extensões da Acrobat Reader DC (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   * Crie um objeto `ReaderExtensionsServiceClient` usando seu construtor padrão.
   * Crie um objeto `ReaderExtensionsServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Certifique-se de especificar `?blob=mtom`.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere um documento PDF.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF com direitos ativados.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF habilitado para direitos e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` ao conteúdo da matriz de bytes.

1. Remova os direitos de uso do documento PDF.

   * Recupere informações sobre a credencial usada para aplicar direitos de uso ao documento PDF, invocando o método `ReaderExtensionsServiceClient` do objeto `getDocumentUsageRights` e transmitindo o objeto `com.adobe.idp.Document` que contém o documento PDF habilitado para direitos. Este método retorna um objeto `GetUsageRightsResult` que contém informações de credenciais.
   * Recupere a data após a qual a credencial não é mais válida obtendo o valor do membro de dados `GetUsageRightsResult` do objeto `notAfter`. O tipo de dados desse membro de dados é `System.DateTime`.
   * Recupere a mensagem que é exibida quando o documento PDF com direitos ativados é aberto no Adobe Reader obtendo o valor do membro de dados `GetUsageRightsResult` do objeto `message`. O tipo de dados desse membro de dados é uma string.
   * Recupere o número de vezes que a credencial é usada obtendo o valor do membro de dados `GetUsageRightsResult` do objeto `useCount`. O tipo de dados desse membro de dados é um número inteiro.

**Consulte também:**

[Recuperando Informações de Credenciais](assigning-usage-rights.md#retrieving-credential-information)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
