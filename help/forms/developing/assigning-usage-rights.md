---
title: Atribuição de direitos de uso
seo-title: Assigning Usage Rights
description: Use a API do cliente Java das extensões do Acrobat Reader DC e a API do serviço da Web para aplicar e remover os direitos de uso dos documentos do PDF.
seo-description: Use the Acrobat Reader DC extensions Java Client API and Web Service API to apply and remove usage rights from PDF documents.
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
role: Developer
exl-id: 6af148eb-427a-4b54-9c5f-8750736882d8
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '3918'
ht-degree: 0%

---

# Atribuição de direitos de uso {#assigning-usage-rights}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

## Sobre o serviço de extensões da Acrobat Reader DC {#about-the-acrobat-reader-dc-extensions-service}

O serviço de extensões da Acrobat Reader DC permite que sua organização compartilhe facilmente documentos PDF interativos, estendendo a funcionalidade do Adobe Reader. O serviço de extensões da Acrobat Reader DC oferece suporte total a qualquer documento PDF, até o PDF 1.7 (inclusive). Funciona com o Adobe Reader 7.0 e posteriores. O serviço adiciona direitos de uso a um documento PDF, ativando recursos que normalmente não estão disponíveis quando um documento PDF é aberto usando o Adobe Reader. Usuários de terceiros não precisam de software ou plug-ins adicionais para trabalhar com documentos habilitados por direitos.

Você pode realizar essas tarefas usando o serviço de extensões da Acrobat Reader DC:

* Aplicar direitos de uso a documentos do PDF. Para obter informações, consulte [Aplicação de direitos de uso a documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* Remova os direitos de uso dos documentos do PDF. Para obter informações, consulte [Remoção de direitos de uso de documentos do PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* Recuperar detalhes da credencial. Para obter informações, consulte [Recuperando Informações de Credencial](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Para obter mais informações sobre o serviço de extensões da Acrobat Reader DC, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Aplicação de direitos de uso a documentos PDF {#applying-usage-rights-to-pdf-documents}

Você pode aplicar direitos de uso a documentos do PDF usando a API de cliente Java de extensões do Acrobat Reader DC e o serviço da Web. Os direitos de uso pertencem à funcionalidade que está disponível por padrão no Acrobat, mas não no Adobe Reader, como a capacidade de adicionar comentários a um formulário ou preencher campos de formulário e salvar o formulário. os documentos PDF que têm direitos de uso aplicados a eles são chamados de documentos habilitados por direitos. Um usuário que abre um documento com direitos ativados no Adobe Reader pode executar operações ativadas para esse documento específico.

>[!NOTE]
>
>Ao aplicar direitos de uso a documentos PDF usando o `applyUsageRights` que faz parte da API Java, é possível definir o método `isModeFinal` parâmetro do `ReaderExtensionsOptionSpec` objeto para `false`. Isso resulta na não atualização do contador de formulários processados e em uma melhoria no desempenho. Se você não estiver preocupado com a atualização do contador de formulários processados, é recomendável definir o `isModeFinal` parâmetro para `false`.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de extensões da Acrobat Reader DC, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para aplicar direitos de uso a um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto Cliente de extensões do Acrobat Reader DC.
1. Recupere um documento PDF.
1. Especifique os direitos de uso a serem aplicados.
1. Aplique direitos de uso ao documento PDF.
1. Salve o documento PDF habilitado para direitos.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto Cliente de extensões do Acrobat Reader DC**

Para executar programaticamente uma operação do serviço de extensões da Acrobat Reader DC, você deve criar um objeto cliente do serviço de extensões da Acrobat Reader DC. Se estiver usando as extensões do Acrobat Reader DC para a API Java, crie uma `ReaderExtensionsServiceClient` objeto. Se estiver usando a API de serviço Web de extensões do Acrobat Reader DC, crie uma `ReaderExtensionsServiceService` objeto.

**Recuperar um documento PDF**

Você deve recuperar um documento PDF para aplicar os direitos de uso. Os documentos de PDF ativados por direitos contêm um dicionário de direitos de uso. Quando o Adobe Reader abre um documento contendo esse dicionário, ele ativa os direitos de uso especificados no dicionário somente para esse documento. Se o documento não contiver um dicionário de direitos de uso, o serviço de extensões da Acrobat Reader DC criará um. Se já contiver um dicionário, o serviço de extensões da Acrobat Reader DC substituirá os direitos de uso existentes pelos que você especificar. O dicionário especifica quais direitos de uso estão ativados. Quando um usuário abre o documento no Adobe Reader, somente os direitos de uso especificados no dicionário são permitidos.

**Especificar direitos de uso a serem aplicados**

Os direitos de uso que você pode definir são determinados por uma credencial que você compra na Adobe Systems Incorporated. As credenciais normalmente fornecem permissão para definir um grupo de direitos de uso relacionados, como aqueles pertencentes aos formulários interativos. Cada credencial fornece o direito de criar um determinado número de documentos PDF habilitados para direitos. Uma credencial de avaliação dá o direito de criar um número ilimitado de documentos de rascunho.

>[!NOTE]
>
>Se você tentar atribuir um direito de uso que não seja permitido pela sua credencial, você causará uma exceção.

**Aplicar direitos de uso ao documento PDF**

Para aplicar direitos de uso a um documento PDF, você faz referência ao alias da credencial que está usando para aplicar direitos de uso (normalmente, uma credencial é instalada durante a instalação do AEM Forms). Além disso, você deve especificar o documento PDF ao qual os direitos de uso são aplicados. Para obter informações sobre como configurar uma credencial, consulte o guia de instalação e implantação do seu servidor de aplicativos.

**Salve o documento PDF habilitado para direitos**

Depois que o serviço de extensões da Acrobat Reader DC aplicar direitos de uso a um documento PDF, você poderá salvar o documento PDF habilitado para direitos como um arquivo PDF.

**Consulte também**

[Aplicar direitos de uso usando a API Java](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Aplicar direitos de uso usando a API de serviço Web](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço de extensões do Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Aplicar direitos de uso usando a API Java {#apply-usage-rights-using-the-java-api}

Aplique direitos de uso a um documento PDF usando a API de extensões do Acrobat Reader DC (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-reader-extensions-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `ReaderExtensionsServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere um documento PDF.

   * Criar um `java.io.FileInputStream` objeto que representa o documento PDF usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Especifique os direitos de uso a serem aplicados.

   * Criar um `UsageRights` objeto que representa os direitos de uso usando seu construtor.
   * Para cada direito de uso a ser aplicado, chame um método correspondente que pertença a `UsageRights` objeto. Por exemplo, para adicionar a variável `enableFormFillIn` direito de uso, chame o `UsageRights` do objeto `enableFormFillIn` e passar `true`. (Repita essa etapa para cada direito de uso a ser aplicado).

1. Aplique direitos de uso ao documento PDF.

   * Criar um `ReaderExtensionsOptionSpec` usando seu construtor. Esse objeto contém opções de tempo de execução exigidas pelo serviço de extensões da Acrobat Reader DC. Ao chamar esse construtor, você deve especificar os seguintes valores:

      * A variável `UsageRights` objeto que contém os direitos de uso a serem aplicados ao documento.
      * Um valor de string que especifica uma mensagem que um usuário vê quando o documento PDF com direitos ativados é aberto no Adobe Reader 7.x. Esta mensagem não é exibida no Adobe Reader 8.0.

   * Aplique direitos de uso ao documento PDF invocando o `ReaderExtensionsServiceClient` do objeto `applyUsageRights` e transmitindo os seguintes valores:

      * A variável `com.adobe.idp.Document` objeto que contém o documento PDF ao qual os direitos de uso são aplicados.
      * Um valor de string que especifica o alias da credencial que permite aplicar direitos de uso.
      * Um valor de string que especifica o valor de senha correspondente. (Atualmente, esse parâmetro é ignorado. Você pode passar `null`.)

   * A variável `ReaderExtensionsOptionSpec` objeto que contém opções de tempo de execução.

   A variável `applyUsageRights` o método retorna um `com.adobe.idp.Document` objeto que contém o documento PDF habilitado para direitos.

1. Salve o documento PDF habilitado para direitos.

   * Criar um `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `com.adobe.idp.Document` ao arquivo (certifique-se de usar o `com.adobe.idp.Document` objeto que foi retornado pelo `applyUsageRights` método).

**Consulte também**

[Aplicação de direitos de uso a documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Início rápido (modo SOAP):aplicação de direitos de uso usando a API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplicar direitos de uso usando a API de serviço Web {#apply-usage-rights-using-the-web-service-api}

Aplique direitos de uso a um documento PDF usando a API de extensões do Acrobat Reader DC (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   * Criar um `ReaderExtensionsServiceClient` usando seu construtor padrão.
   * Criar um `ReaderExtensionsServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Certifique-se de especificar `?blob=mtom`.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `ReaderExtensionsServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere um documento PDF.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar um documento PDF ao qual são aplicados direitos de uso.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` método. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Especifique os direitos de uso a serem aplicados.

   * Criar um `UsageRights` objeto que representa os direitos de uso usando seu construtor.
   * Atribua o valor a cada direito de uso a ser aplicado `true` ao membro de dados correspondente que pertence ao `UsageRights` objeto. Por exemplo, para adicionar a variável `enableFormFillIn` direito de uso, atribuir `true` para o `UsageRights` do objeto `enableFormFillIn` membro de dados. (Repita essa etapa para cada direito de uso a ser aplicado).

1. Aplique direitos de uso ao documento PDF.

   * Criar um `ReaderExtensionsOptionSpec` usando seu construtor. Esse objeto contém opções de tempo de execução exigidas pelo serviço de extensões da Acrobat Reader DC.
   * Atribua a `UsageRights` objeto para o `ReaderExtensionsOptionSpec` do objeto `usageRights` membro de dados.
   * Atribua um valor de string que especifique a mensagem que um usuário vê quando o documento PDF habilitado para direitos é aberto no Adobe Reader para o `ReaderExtensionsOptionSpec` do objeto `message` membro de dados.
   * Aplique direitos de uso ao documento PDF invocando o `ReaderExtensionsServiceClient` do objeto `applyUsageRights` e transmitindo os seguintes valores:

      * A variável `BLOB` objeto que contém o documento PDF ao qual os direitos de uso são aplicados.
      * Um valor de string que especifica o alias da credencial que permite aplicar direitos de uso.
      * Um valor de string que especifica o valor de senha correspondente. (Atualmente, esse parâmetro é ignorado. Você pode passar `null`.)

   * A variável `ReaderExtensionsOptionSpec` objeto que contém opções de tempo de execução.

   A variável `applyUsageRights` o método retorna um `BLOB` objeto que contém o documento PDF habilitado para direitos.

1. Salve o documento PDF habilitado para direitos.

   * Criar um `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do documento PDF habilitado para direitos.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi retornado pelo `applyUsageRights` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Aplicação de direitos de uso a documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Remoção de direitos de uso de documentos do PDF {#removing-usage-rights-from-pdf-documents}

Você pode remover direitos de uso de um documento habilitado para direitos. A remoção de direitos de uso de um documento de PDF habilitado para direitos também é necessária para executar outras operações do AEM Forms. Por exemplo, você deve assinar digitalmente (ou certificar) um documento PDF antes de definir os direitos de uso. Portanto, se você quiser executar operações em um documento habilitado para direitos, remova os direitos de uso do documento PDF, execute as outras operações, como assinar digitalmente o documento e reaplique os direitos de uso ao documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de extensões da Acrobat Reader DC, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para remover direitos de uso de um documento de PDF habilitado para direitos, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto Cliente de extensões do Acrobat Reader DC.
1. Recupere um documento PDF habilitado para direitos.
1. Remova os direitos de uso do documento PDF.
1. Salve o documento PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto Cliente de extensões do Acrobat Reader DC**

Antes de executar programaticamente uma operação de serviço de extensões da Acrobat Reader DC, você deve criar um objeto cliente de serviço de extensões da Acrobat Reader DC. Se estiver usando a API Java, crie uma `ReaderExtensionsServiceClient` objeto. Se estiver usando a API de serviço Web de extensões do Acrobat Reader DC, crie uma `ReaderExtensionsServiceService` objeto.

**Recuperar um documento PDF habilitado para direitos**

Recupere um documento PDF habilitado para direitos para remover direitos de uso.

**Remover direitos de uso do documento PDF**

Depois de recuperar um documento de PDF habilitado para direitos, você pode remover os direitos de uso. Após remover os direitos de uso, o documento PDF não terá nenhuma funcionalidade adicional enquanto for visualizado no Adobe Reader.

**Salve o documento PDF**

Você pode salvar o documento PDF que não contém mais direitos de uso como um arquivo PDF. Depois de salvo como um arquivo PDF, o documento PDF pode ser visualizado no Adobe Reader ou Acrobat.

**Consulte também**

[Remover direitos de uso usando a API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Remover direitos de uso usando a API de serviço Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço de extensões do Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Aplicação de direitos de uso a documentos PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Remover direitos de uso usando a API Java {#remove-usage-rights-using-the-java-api}

Remova os direitos de uso de um documento PDF habilitado para direitos usando a API de extensões do Acrobat Reader DC (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-reader-extensions-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   Criar um `ReaderExtensionsServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Recupere um documento PDF.

   * Criar um `java.io.FileInputStream` objeto que representa o documento de PDF habilitado para direitos usando seu construtor e transmitindo um valor de string que especifica o local do documento de PDF.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Remova os direitos de uso do documento PDF.

   Remova os direitos de uso do documento PDF invocando o `ReaderExtensionsServiceClient` do objeto `removeUsageRights` e transmitindo o `com.adobe.idp.Document` objeto que contém o documento PDF habilitado para direitos. Este método retorna um valor de `com.adobe.idp.Document` objeto que contém um documento PDF que não tem direitos de uso.

1. Aplique direitos de uso ao documento PDF.

   * Criar um `java.io.File` e verifique se a extensão do arquivo é .PDF.
   * Chame o `Document` do objeto `copyToFile` método para copiar o conteúdo do `Document` ao arquivo (certifique-se de usar o `Document` objeto que foi retornado pelo `removeUsageRights` método).

**Consulte também**

[Remoção de direitos de uso de documentos do PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Início rápido (modo SOAP): remoção de direitos de uso de um documento PDF usando a API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Remover direitos de uso usando a API de serviço Web {#remove-usage-rights-using-the-web-service-api}

Remova os direitos de uso de um documento PDF habilitado para direitos usando a API de extensões do Acrobat Reader DC (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   * Criar um `ReaderExtensionsServiceClient` usando seu construtor padrão.
   * Criar um `ReaderExtensionsServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Certifique-se de especificar `?blob=mtom`.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `ReaderExtensionsServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere um documento PDF.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` O objeto é usado para armazenar o documento de PDF habilitado para direitos do qual os direitos de uso são removidos.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Remova os direitos de uso do documento PDF.

   Remova os direitos de uso do documento PDF invocando o `ReaderExtensionsServiceClient` do objeto `removeUsageRights` e transmitindo o `BLOB` objeto que contém o documento PDF habilitado para direitos. Este método retorna um valor de `BLOB` objeto que contém um documento PDF que não tem direitos de uso.

1. Aplique direitos de uso ao documento PDF.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo PDF.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi retornado pelo `removeUsageRights` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.

**Consulte também**

[Remoção de direitos de uso de documentos do PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recuperando Informações de Credencial {#retrieving-credential-information}

Você pode recuperar informações sobre a credencial usada para aplicar direitos de uso a um documento de PDF habilitado para direitos. Ao recuperar informações sobre uma credencial, você pode obter informações como a data após a qual o certificado não é mais válido.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de extensões da Acrobat Reader DC, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-2}

Para recuperar informações sobre a credencial usada para aplicar direitos de uso a um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto Cliente de extensões do Acrobat Reader DC.
1. Recupere um documento PDF habilitado para direitos.
1. Recuperar informações sobre a credencial.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto Cliente de extensões do Acrobat Reader DC**

Antes de executar programaticamente uma operação de serviço de extensões da Acrobat Reader DC, você deve criar um objeto cliente de serviço de extensões da Acrobat Reader DC. Se estiver usando a API Java, crie uma `ReaderExtensionsServiceClient` objeto. Se estiver usando a API de serviço Web de extensões do Acrobat Reader DC, crie uma `ReaderExtensionsServiceService` objeto.

**Recuperar um documento PDF habilitado para direitos**

Você deve recuperar um documento de PDF habilitado para direitos para recuperar informações sobre a credencial. Você também pode recuperar informações sobre uma credencial especificando seu alias; no entanto, se quiser recuperar informações sobre uma credencial usada para aplicar direitos de uso a um documento de PDF habilitado para direitos específicos, você deverá recuperar o documento.

**Recuperar informações sobre a credencial**

Depois de recuperar um documento de PDF habilitado para direitos, você pode obter informações sobre a credencial usada para aplicar direitos de uso a ele. Você pode obter as seguintes informações sobre a credencial:

* A mensagem exibida no Adobe Reader quando o documento PDF habilitado para direitos é aberto.
* A data após a qual a credencial não é mais válida.
* A data antes da qual a credencial não é válida.
* Os direitos de uso que foram definidos para este documento de PDF habilitado para direitos.
* O número de vezes que a credencial foi usada.

**Consulte também**

[Remover direitos de uso usando a API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Remover direitos de uso usando a API de serviço Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço de extensões do Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Recuperar informações de credencial usando a API Java {#retrieve-credential-information-using-the-java-api}

Recupere informações de credencial usando a API de extensões da Acrobat Reader DC (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-reader-extensions-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   Criar um `ReaderExtensionsServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Recupere um documento PDF.

   * Criar um `java.io.FileInputStream` objeto que representa o documento PDF habilitado para direitos usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF habilitado para direitos.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Remova os direitos de uso do documento PDF.

   * Recupere informações sobre a credencial usada para aplicar direitos de uso ao documento PDF chamando o `ReaderExtensionsServiceClient` do objeto `getDocumentUsageRights` e transmitindo o `com.adobe.idp.Document` objeto que contém o documento PDF habilitado para direitos. Este método retorna um valor de `GetUsageRightsResult` objeto que contém informações de credencial.
   * Recupere a data após a qual a credencial não será mais válida chamando o `GetUsageRightsResult` do objeto `getNotAfter` método. Este método retorna um valor de `java.util.Date` objeto que representa a data após a qual a credencial não é mais válida.
   * Recupere a mensagem que é exibida no Adobe Reader quando o documento de PDF habilitado para direitos for aberto chamando o `GetUsageRightsResult` do objeto `getMessage` método. Esse método retorna um valor de string que representa a mensagem.

**Consulte também**

[Recuperando Informações de Credencial](assigning-usage-rights.md#retrieving-credential-information)

[Início rápido (modo SOAP): recuperação de informações de credencial usando a API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar informações de credencial usando a API do serviço Web {#retrieve-credential-information-using-the-web-service-api}

Recupere informações de credencial usando a API de extensões do Acrobat Reader DC (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   * Criar um `ReaderExtensionsServiceClient` usando seu construtor padrão.
   * Criar um `ReaderExtensionsServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Certifique-se de especificar `?blob=mtom`.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `ReaderExtensionsServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere um documento PDF.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` é usado para armazenar um documento PDF habilitado para direitos.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF habilitado para direitos e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Remova os direitos de uso do documento PDF.

   * Recupere informações sobre a credencial usada para aplicar direitos de uso ao documento PDF chamando o `ReaderExtensionsServiceClient` do objeto `getDocumentUsageRights` e transmitindo o `com.adobe.idp.Document` objeto que contém o documento PDF habilitado para direitos. Este método retorna um valor de `GetUsageRightsResult` objeto que contém informações de credencial.
   * Recupere a data após a qual a credencial não é mais válida obtendo o valor de `GetUsageRightsResult` do objeto `notAfter` membro de dados. O tipo de dados deste membro de dados é `System.DateTime`.
   * Recupere a mensagem exibida quando o documento de PDF habilitado para direitos for aberto no Adobe Reader obtendo o valor do `GetUsageRightsResult` do objeto `message` membro de dados. O tipo de dados deste membro de dados é uma string.
   * Recuperar o número de vezes que a credencial é usada obtendo o valor de `GetUsageRightsResult` do objeto `useCount` membro de dados. O tipo de dados deste membro de dados é um inteiro.

**Consulte também**

[Recuperando Informações de Credencial](assigning-usage-rights.md#retrieving-credential-information)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
