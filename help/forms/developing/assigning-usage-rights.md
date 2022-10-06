---
title: Atribuição de direitos de uso
seo-title: Assigning Usage Rights
description: Use a API do cliente Java e a API do serviço da Web das extensões do Acrobat Reader DC para aplicar e remover direitos de uso de documentos do PDF.
seo-description: Use the Acrobat Reader DC extensions Java Client API and Web Service API to apply and remove usage rights from PDF documents.
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
role: Developer
exl-id: 6af148eb-427a-4b54-9c5f-8750736882d8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3926'
ht-degree: 0%

---

# Atribuição de direitos de uso {#assigning-usage-rights}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

## Sobre o serviço de extensões do Acrobat Reader DC {#about-the-acrobat-reader-dc-extensions-service}

O serviço de extensões Acrobat Reader DC permite que sua organização compartilhe facilmente documentos interativos do PDF, estendendo a funcionalidade do Adobe Reader. O serviço de extensões Acrobat Reader DC oferece suporte total a qualquer documento do PDF, até o PDF 1.7, inclusive. Ele funciona com o Adobe Reader 7.0 e posterior. O serviço adiciona direitos de uso a um documento do PDF, ativando recursos que normalmente não estão disponíveis quando um documento do PDF é aberto usando o Adobe Reader. Usuários de terceiros não exigem software ou plug-ins adicionais para trabalhar com os documentos ativados por direitos.

Você pode realizar essas tarefas usando o serviço de extensões do Acrobat Reader DC:

* Aplicar direitos de uso a documentos PDF. Para obter mais informações, consulte [Aplicação de direitos de uso a documentos do PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* Remova direitos de uso de documentos do PDF. Para obter mais informações, consulte [Removendo direitos de uso de documentos do PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* Recuperar detalhes da credencial. Para obter mais informações, consulte [Recuperando Informações de Credenciais](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Para obter mais informações sobre o serviço de extensões da Acrobat Reader DC, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Aplicação de direitos de uso a documentos do PDF {#applying-usage-rights-to-pdf-documents}

Você pode aplicar direitos de uso a documentos do PDF usando a API do cliente Java do Acrobat Reader DC Extensions e o serviço da Web. Os direitos de uso pertencem a uma funcionalidade que está disponível por padrão no Acrobat, mas não no Adobe Reader, como a capacidade de adicionar comentários a um formulário ou de preencher campos de formulário e salvar o formulário. Os documentos do PDF que têm direitos de uso aplicados a eles são chamados de documentos ativados por direitos. Um usuário que abra um documento com direitos ativados no Adobe Reader pode executar operações ativadas para esse documento específico.

>[!NOTE]
>
>Ao aplicar direitos de uso a documentos do PDF usando o `applyUsageRights` , que faz parte da API do Java, é possível definir a variável `isModeFinal` do `ReaderExtensionsOptionSpec` objeto para `false`. Isso resulta na atualização do contador de formulários processados e em uma melhoria no desempenho. Se você não estiver preocupado com a atualização do contador de formulários processados, é recomendável definir a variável `isModeFinal` para `false`.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de extensões da Acrobat Reader DC, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para aplicar direitos de uso a um documento PDF, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto Cliente de extensões do Acrobat Reader DC.
1. Recupere um documento PDF.
1. Especifique os direitos de uso a serem aplicados.
1. Aplique direitos de uso ao documento PDF.
1. Salve o documento PDF habilitado para direitos.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto Cliente de extensões do Acrobat Reader DC**

Para executar programaticamente uma operação do Acrobat Reader DC Extensions Service, você deve criar um objeto cliente do serviço Acrobat Reader DC Extensions . Se estiver usando a API Java das extensões do Acrobat Reader DC, crie um `ReaderExtensionsServiceClient` objeto. Se estiver usando a API do serviço da Web das extensões do Acrobat Reader DC, crie um `ReaderExtensionsServiceService` objeto.

**Recuperar um documento PDF**

Você deve recuperar um documento do PDF para aplicar direitos de uso. Os documentos do PDF habilitados para direitos contêm um dicionário de direitos de uso. Quando o Adobe Reader abre um documento contendo esse dicionário, ele ativa os direitos de uso especificados no dicionário apenas para esse documento. Se o documento não contiver um dicionário de direitos de uso, o serviço de extensões do Acrobat Reader DC criará um. Se já contiver um dicionário, o serviço de extensões do Acrobat Reader DC substituirá os direitos de uso existentes pelos que você especificar. O dicionário especifica quais direitos de uso estão ativados. Quando um usuário abre o documento no Adobe Reader, somente os direitos de uso especificados no dicionário são permitidos.

**Especificar direitos de uso a serem aplicados**

Os direitos de uso que você pode definir são determinados por uma credencial que você compra no Adobe Systems Incorporated. As credenciais normalmente fornecem permissão para definir um grupo de direitos de uso relacionados, como aqueles pertencentes a formulários interativos. Cada credencial fornece o direito de criar um determinado número de documentos PDF ativados por direitos. Uma credencial de avaliação dá o direito de criar um número ilimitado de documentos preliminares.

>[!NOTE]
>
>Se você tentar atribuir um direito de uso que não é permitido por sua credencial, ocorrerá uma exceção.

**Aplicar direitos de uso ao documento PDF**

Para aplicar direitos de uso a um documento do PDF, você faz referência ao alias da credencial que está usando para aplicar direitos de uso (uma credencial geralmente é instalada durante a instalação do AEM Forms). Você também deve especificar o documento PDF ao qual os direitos de uso são aplicados. Para obter informações sobre como configurar uma credencial, consulte o guia de instalação e implantação do servidor de aplicativos.

**Salve o documento PDF habilitado para direitos**

Depois que o serviço de extensões do Acrobat Reader DC aplica direitos de uso a um documento do PDF, é possível salvar o documento PDF com direitos ativados como um arquivo PDF.

**Consulte também**

[Aplicar direitos de uso usando a API do Java](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Aplicar direitos de uso usando a API do serviço da Web](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Acrobat Reader DC Extensions Service](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Aplicar direitos de uso usando a API do Java {#apply-usage-rights-using-the-java-api}

Aplique direitos de uso a um documento do PDF usando a API de extensões do Acrobat Reader DC (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-reader-extensions-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `ReaderExtensionsServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Recupere um documento PDF.

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF usando seu construtor e passando um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Especifique os direitos de uso a serem aplicados.

   * Crie um `UsageRights` que representa direitos de uso usando seu construtor.
   * Para cada direito de uso a ser aplicado, chame um método correspondente que pertença ao `UsageRights` objeto. Por exemplo, para adicionar a variável `enableFormFillIn` direito de uso, chame o `UsageRights` do objeto `enableFormFillIn` método e pass `true`. (Repita essa etapa para cada direito de uso a ser aplicado).

1. Aplique direitos de uso ao documento PDF.

   * Crie um `ReaderExtensionsOptionSpec` usando seu construtor. Esse objeto contém opções de tempo de execução exigidas pelo serviço de extensões do Acrobat Reader DC. Ao invocar esse construtor, você deve especificar os seguintes valores:

      * O `UsageRights` objeto que contém os direitos de uso a serem aplicados ao documento.
      * Um valor da string que especifica a mensagem que um usuário vê quando o documento do PDF habilitado para direitos é aberto no Adobe Reader 7.x. Esta mensagem não é exibida no Adobe Reader 8.0.
   * Aplique direitos de uso ao documento do PDF chamando o `ReaderExtensionsServiceClient` do objeto `applyUsageRights` e transmitindo os seguintes valores:

      * O `com.adobe.idp.Document` objeto que contém o documento PDF ao qual os direitos de uso são aplicados.
      * Um valor da string que especifica o alias da credencial que permite aplicar direitos de uso.
      * Um valor da string que especifica o valor da senha correspondente. (No momento, esse parâmetro é ignorado. Você pode passar `null`.)
   * O `ReaderExtensionsOptionSpec` objeto que contém opções de tempo de execução.

   O `applyUsageRights` método retorna um `com.adobe.idp.Document` objeto que contém o documento PDF habilitado para direitos.

1. Salve o documento PDF habilitado para direitos.

   * Crie um `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo da `com.adobe.idp.Document` para o arquivo (certifique-se de usar a variável `com.adobe.idp.Document` objeto retornado pelo `applyUsageRights` método ).

**Consulte também**

[Aplicação de direitos de uso a documentos do PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Início rápido (modo SOAP):Aplicação de direitos de uso usando a API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplicar direitos de uso usando a API do serviço da Web {#apply-usage-rights-using-the-web-service-api}

Aplique direitos de uso a um documento do PDF usando a API de extensões do Acrobat Reader DC (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   * Crie um `ReaderExtensionsServiceClient` usando seu construtor padrão.
   * Crie um `ReaderExtensionsServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Certifique-se de especificar `?blob=mtom`.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `ReaderExtensionsServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere um documento PDF.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar um documento PDF ao qual os direitos de uso são aplicados.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` método . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Especifique os direitos de uso a serem aplicados.

   * Crie um `UsageRights` que representa direitos de uso usando seu construtor.
   * Para cada direito de uso a ser aplicado, atribua o valor `true` ao membro de dados correspondente que pertence ao `UsageRights` objeto. Por exemplo, para adicionar a variável `enableFormFillIn` direito de uso, atribuir `true` para `UsageRights` do objeto `enableFormFillIn` membro de dados. (Repita essa etapa para cada direito de uso a ser aplicado).

1. Aplique direitos de uso ao documento PDF.

   * Crie um `ReaderExtensionsOptionSpec` usando seu construtor. Esse objeto contém opções de tempo de execução exigidas pelo serviço de extensões do Acrobat Reader DC.
   * Atribua o `UsageRights` para `ReaderExtensionsOptionSpec` do objeto `usageRights` membro de dados.
   * Atribua um valor de string que especifica a mensagem que um usuário vê quando o documento do PDF habilitado para direitos é aberto no Adobe Reader para a `ReaderExtensionsOptionSpec` do objeto `message` membro de dados.
   * Aplique direitos de uso ao documento do PDF chamando o `ReaderExtensionsServiceClient` do objeto `applyUsageRights` e transmitindo os seguintes valores:

      * O `BLOB` objeto que contém o documento PDF ao qual os direitos de uso são aplicados.
      * Um valor da string que especifica o alias da credencial que permite aplicar direitos de uso.
      * Um valor da string que especifica o valor da senha correspondente. (No momento, esse parâmetro é ignorado. Você pode passar `null`.)
   * O `ReaderExtensionsOptionSpec` objeto que contém opções de tempo de execução.

   O `applyUsageRights` método retorna um `BLOB` objeto que contém o documento PDF habilitado para direitos.

1. Salve o documento PDF habilitado para direitos.

   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento de PDF habilitado para direitos.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `applyUsageRights` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Aplicação de direitos de uso a documentos do PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Removendo direitos de uso de documentos do PDF {#removing-usage-rights-from-pdf-documents}

Você pode remover direitos de uso de um documento habilitado para direitos. A remoção de direitos de uso de um documento de PDF habilitado para direitos também é necessária para executar outras operações do AEM Forms nele. Por exemplo, você deve assinar digitalmente (ou certificar) um documento do PDF antes de definir direitos de uso. Portanto, se você deseja executar operações em um documento com direitos ativados, é necessário remover direitos de uso do documento do PDF, executar as outras operações, como assinar digitalmente o documento e, em seguida, reaplicar direitos de uso ao documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de extensões da Acrobat Reader DC, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para remover direitos de uso de um documento de PDF habilitado para direitos, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto Cliente de extensões do Acrobat Reader DC.
1. Recupere um documento PDF habilitado para direitos.
1. Remova os direitos de uso do documento PDF.
1. Salve o documento PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto Cliente de extensões do Acrobat Reader DC**

Antes de executar programaticamente uma operação de serviço de extensões do Acrobat Reader DC, é necessário criar um objeto cliente do serviço de extensões do Acrobat Reader DC. Se estiver usando a API do Java, crie um `ReaderExtensionsServiceClient` objeto. Se estiver usando a API do serviço da Web das extensões do Acrobat Reader DC, crie um `ReaderExtensionsServiceService` objeto.

**Recuperar um documento de PDF habilitado para direitos**

Recupere um documento de PDF habilitado para direitos para remover direitos de uso.

**Remover direitos de uso do documento PDF**

Depois de recuperar um documento do PDF habilitado para direitos, você pode remover direitos de uso. Após remover os direitos de uso, o documento do PDF não terá nenhuma funcionalidade adicional enquanto for visualizado no Adobe Reader.

**Salve o documento do PDF**

Você pode salvar o documento do PDF que não contém mais direitos de uso como um arquivo PDF. Depois de salvo como um arquivo PDF, o documento do PDF pode ser exibido no Adobe Reader ou no Acrobat.

**Consulte também**

[Remova os direitos de uso usando a API do Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Remover direitos de uso usando a API de serviço da Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Acrobat Reader DC Extensions Service](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Aplicação de direitos de uso a documentos do PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Remova os direitos de uso usando a API do Java {#remove-usage-rights-using-the-java-api}

Remova os direitos de uso de um documento do PDF habilitado para direitos usando a API de extensões do Acrobat Reader DC (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-reader-extensions-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   Crie um `ReaderExtensionsServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Recupere um documento PDF.

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF habilitado para direitos usando seu construtor e passando um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Remova os direitos de uso do documento PDF.

   Remova os direitos de uso do documento do PDF chamando o `ReaderExtensionsServiceClient` do objeto `removeUsageRights` e a aprovação do `com.adobe.idp.Document` objeto que contém o documento PDF habilitado para direitos. Esse método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF que não tem direitos de uso.

1. Aplique direitos de uso ao documento PDF.

   * Crie um `java.io.File` e verifique se a extensão do arquivo é .PDF.
   * Chame o `Document` do objeto `copyToFile` para copiar o conteúdo da `Document` para o arquivo (certifique-se de usar a variável `Document` objeto retornado pelo `removeUsageRights` método ).

**Consulte também**

[Removendo direitos de uso de documentos do PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Início rápido (modo SOAP): Remoção de direitos de uso de um documento do PDF usando a API do Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Remover direitos de uso usando a API de serviço da Web {#remove-usage-rights-using-the-web-service-api}

Remova os direitos de uso de um documento do PDF habilitado para direitos usando a API de extensões do Acrobat Reader DC (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   * Crie um `ReaderExtensionsServiceClient` usando seu construtor padrão.
   * Crie um `ReaderExtensionsServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Certifique-se de especificar `?blob=mtom`.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `ReaderExtensionsServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere um documento PDF.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento de PDF habilitado para direitos do qual os direitos de uso são removidos.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Remova os direitos de uso do documento PDF.

   Remova os direitos de uso do documento do PDF chamando o `ReaderExtensionsServiceClient` do objeto `removeUsageRights` e a aprovação do `BLOB` objeto que contém o documento PDF habilitado para direitos. Esse método retorna um `BLOB` objeto que contém um documento PDF que não tem direitos de uso.

1. Aplique direitos de uso ao documento PDF.

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo PDF.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `removeUsageRights` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.

**Consulte também**

[Removendo direitos de uso de documentos do PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recuperando Informações de Credenciais {#retrieving-credential-information}

Você pode recuperar informações sobre a credencial usada para aplicar direitos de uso a um documento de PDF habilitado para direitos. Ao recuperar informações sobre uma credencial, é possível obter informações como a data após a qual o certificado não é mais válido.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de extensões da Acrobat Reader DC, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-2}

Para recuperar informações sobre a credencial usada para aplicar direitos de uso a um documento do PDF, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto Cliente de extensões do Acrobat Reader DC.
1. Recupere um documento PDF habilitado para direitos.
1. Recupere informações sobre a credencial.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto Cliente de extensões do Acrobat Reader DC**

Antes de executar programaticamente uma operação de serviço de extensões do Acrobat Reader DC, é necessário criar um objeto cliente do serviço de extensões do Acrobat Reader DC. Se estiver usando a API do Java, crie um `ReaderExtensionsServiceClient` objeto. Se estiver usando a API do serviço da Web das extensões do Acrobat Reader DC, crie um `ReaderExtensionsServiceService` objeto.

**Recuperar um documento de PDF habilitado para direitos**

Você deve recuperar um documento do PDF habilitado para direitos para recuperar informações sobre a credencial. Também é possível recuperar informações sobre uma credencial especificando seu alias; no entanto, se você quiser recuperar informações sobre uma credencial que foi usada para aplicar direitos de uso a um documento de PDF com direitos habilitados, deverá recuperar o documento.

**Recuperar informações sobre a credencial**

Depois de recuperar um documento de PDF habilitado para direitos, você pode obter informações sobre a credencial usada para aplicar direitos de uso a ela. Você pode obter as seguintes informações sobre a credencial:

* A mensagem que é exibida no Adobe Reader quando o documento PDF habilitado para direitos é aberto.
* A data após a qual a credencial não é mais válida.
* A data antes da qual a credencial não é válida.
* Os direitos de uso que foram definidos para este documento de PDF habilitado para direitos.
* O número de vezes que a credencial foi usada.

**Consulte também**

[Remova os direitos de uso usando a API do Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Remover direitos de uso usando a API de serviço da Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Acrobat Reader DC Extensions Service](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Recuperar informações da credencial usando a API Java {#retrieve-credential-information-using-the-java-api}

Recupere informações de credenciais usando a API de extensões do Acrobat Reader DC (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-reader-extensions-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   Crie um `ReaderExtensionsServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Recupere um documento PDF.

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF habilitado para direitos usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF habilitado para direitos.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Remova os direitos de uso do documento PDF.

   * Recupere informações sobre a credencial usada para aplicar direitos de uso ao documento do PDF, chamando o `ReaderExtensionsServiceClient` do objeto `getDocumentUsageRights` e a aprovação do `com.adobe.idp.Document` objeto que contém o documento PDF habilitado para direitos. Esse método retorna um `GetUsageRightsResult` objeto que contém informações de credenciais.
   * Recupere a data após a qual a credencial não é mais válida, chamando o `GetUsageRightsResult` do objeto `getNotAfter` método . Esse método retorna um `java.util.Date` objeto que representa a data após a qual a credencial não é mais válida.
   * Recupere a mensagem que é exibida no Adobe Reader quando o documento de PDF habilitado para direitos é aberto, chamando o `GetUsageRightsResult` do objeto `getMessage` método . Esse método retorna um valor de string que representa a mensagem.

**Consulte também**

[Recuperando Informações de Credenciais](assigning-usage-rights.md#retrieving-credential-information)

[Início rápido (modo SOAP): Recuperação de informações de credencial usando a API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar informações de credenciais usando a API do serviço da Web {#retrieve-credential-information-using-the-web-service-api}

Recupere informações de credenciais usando a API de extensões do Acrobat Reader DC (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um objeto Cliente de extensões do Acrobat Reader DC.

   * Crie um `ReaderExtensionsServiceClient` usando seu construtor padrão.
   * Crie um `ReaderExtensionsServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Certifique-se de especificar `?blob=mtom`.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `ReaderExtensionsServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere um documento PDF.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar um documento PDF habilitado para direitos.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento de PDF habilitado para direitos e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Remova os direitos de uso do documento PDF.

   * Recupere informações sobre a credencial usada para aplicar direitos de uso ao documento do PDF, chamando o `ReaderExtensionsServiceClient` do objeto `getDocumentUsageRights` e a aprovação do `com.adobe.idp.Document` objeto que contém o documento PDF habilitado para direitos. Esse método retorna um `GetUsageRightsResult` objeto que contém informações de credenciais.
   * Recupere a data após a qual a credencial não é mais válida obtendo o valor da variável `GetUsageRightsResult` do objeto `notAfter` membro de dados. O tipo de dados desse membro de dados é `System.DateTime`.
   * Recupere a mensagem que é exibida quando o documento do PDF habilitado para direitos é aberto no Adobe Reader obtendo o valor da variável `GetUsageRightsResult` do objeto `message` membro de dados. O tipo de dados desse membro de dados é uma string.
   * Recupere o número de vezes que a credencial é usada obtendo o valor da variável `GetUsageRightsResult` do objeto `useCount` membro de dados. O tipo de dados desse membro de dados é um número inteiro.

**Consulte também**

[Recuperando Informações de Credenciais](assigning-usage-rights.md#retrieving-credential-information)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
