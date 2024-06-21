---
title: Conversão de Postscript em documentos PDF
description: Use o serviço Distiller para converter arquivos PostScript®, Encapsulated PostScript (EPS) e PRN para arquivos PDF compactos, confiáveis e mais seguros em uma rede. O serviço Distiller converte grandes volumes de documentos impressos em documentos eletrônicos, como faturas e declarações usando a API Java e a API de serviço da Web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 744df8b2-0c61-410f-89e9-20b8adddbf45
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---

# Conversão de Postscript em documentos PDF {#converting-postscript-to-pdf-documents}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

## Sobre o serviço Distiller {#about-the-distiller-service}

O serviço Distiller® converte arquivos PostScript®, Encapsulated PostScript (EPS) e PRN para arquivos PDF compactos, confiáveis e mais seguros em uma rede. O serviço Distiller é frequentemente usado para converter grandes volumes de documentos impressos em documentos eletrônicos, como faturas e demonstrativos. A conversão de documentos em PDF também permite que as empresas enviem aos seus clientes uma versão em papel e uma versão eletrônica de um documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Distiller, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversão de PostScript em documentos PDF {#converting-postscript-to-pdf-documents-inner}

Este tópico descreve como você pode usar a API de serviço do Distiller (Java e serviço da Web) para converter programaticamente arquivos PostScript (PS), Encapsulated PostScript (EPS) e PRN em documentos PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Distiller, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para converter arquivos PostScript em documentos PDF, um dos itens a seguir precisa ser instalado no servidor que hospeda o AEM Forms: Acrobat 9 ou Microsoft Visual C++ 2005 pacote redistribuível.

### Resumo das etapas {#summary-of-steps}

Para converter qualquer um dos tipos suportados em um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente de serviço Distiller.
1. Recupere o arquivo a ser convertido.
1. Chame a operação de criação de PDF.
1. Salve o documento PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente de serviço Distiller**

Antes de executar programaticamente uma operação de serviço Distiller, você deve criar um cliente de serviço Distiller. Se estiver usando a API Java, crie uma `DistillerServiceClient` objeto. Se estiver usando a API do serviço Web, crie uma `DistillerServiceService` objeto.

**Recuperar o arquivo para converter**

Recupere o arquivo que deseja converter. Por exemplo, para converter um arquivo PS em um documento PDF, você deve recuperar o arquivo PS.

**Chame a operação de criação de PDF**

Depois de criar o cliente de serviço, você pode chamar a operação de criação de PDF. Esta operação precisará de informações sobre o documento a ser convertido, incluindo o caminho para o documento de destino.

**Salve o documento PDF**

Você pode salvar o documento PDF como um arquivo PDF.

**Consulte também**

[Converter um arquivo PostScript em PDF usando a API Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Conversão de um arquivo PostScript em PDF usando a API do serviço da Web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Converter um arquivo PostScript em PDF usando a API Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Converta um arquivo PostScript em um documento PDF usando a API de serviço do Distiller (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-destiller-client.jar, no caminho de classe do projeto Java.

1. Crie um cliente de serviço Distiller.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `DistillerServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere o arquivo a ser convertido.

   * Criar um `java.io.FileInputStream` objeto que representa o arquivo a ser convertido usando seu construtor e transmitindo um valor de string que especifica o local do arquivo.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Chame a operação de criação de PDF.

   Chame o `DistillerServiceClient` do objeto `createPDF` e passe os seguintes valores:

   * A variável `com.adobe.idp.Document` objeto que representa o arquivo PS, EPS ou PRN a ser convertido
   * A `java.lang.String` objeto que contém o nome do arquivo a ser convertido
   * A `java.lang.String` objeto que contém o nome das configurações do Adobe PDF a serem usadas
   * A `java.lang.String` objeto que contém o nome das configurações de segurança a serem usadas
   * Uma opção `com.adobe.idp.Document` objeto que contém configurações a serem aplicadas durante a geração do documento PDF
   * Uma opção `com.adobe.idp.Document` objeto que contém informações de metadados a serem aplicadas ao documento PDF

   A variável `createPDF` o método retorna um `CreatePDFResult` objeto que contém o novo documento PDF e um arquivo de log que pode ser gerado. O arquivo de log geralmente contém mensagens de erro ou aviso que são geradas pela solicitação de conversão.

1. Salve o documento PDF.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Chame o `CreatePDFResult` do objeto `getCreatedDocument` método. Isso retorna um `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para extrair o documento PDF.

   Da mesma forma, para obter o documento de log, execute as ações a seguir.

   * Chame o `CreatePDFResult` do objeto `getLogDocument` método. Isso retorna um `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para extrair o documento de log.

**Consulte também**

[Resumo das etapas](converting-postscript-pdf-documents.md#summary-of-steps)

[Início rápido (modo SOAP): conversão de um arquivo PostScript em um documento PDF usando a API do Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversão de um arquivo PostScript em PDF usando a API do serviço da Web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Converta um arquivo PostScript em um documento PDF usando a API de serviço do Distiller (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente de serviço Distiller.

   * Criar um `DistillerServiceClient` usando seu construtor padrão.
   * Criar um `DistillerServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/DistillerService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `DistillerServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere o arquivo a ser convertido.

   * Criar um `BLOB` usando seu construtor. Este `BLOB` objeto é usado para armazenar o arquivo a ser convertido em um documento PDF.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo e o modo em que o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Chame a operação de criação de PDF.

   Chame o `DistillerServiceService` do objeto `CreatePDF2` e passe os seguintes valores obrigatórios:

   * A variável `BLOB` objeto que representa o arquivo PS a ser convertido
   * Uma string que contém o nome do caminho do arquivo a ser convertido
   * Um objeto de string que contém as configurações do Adobe PDF a serem usadas (por exemplo, `Standard`)
   * Um objeto de string que contém as configurações de segurança a serem usadas (por exemplo, `No Securit`y)
   * Uma opção `BLOB` objeto que contém configurações a serem aplicadas durante a geração do documento PDF
   * Uma opção `BLOB` objeto que contém informações de metadados a serem aplicadas ao documento PDF
   * A `BLOB` parâmetro de saída usado para armazenar o documento PDF
   * A `BLOB` parâmetro de saída usado para armazenar o log

1. Salve o documento PDF.

   * Criar um `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do documento de PDF assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto que foi retornado pelo `CreatePDF2` (o parâmetro de saída). Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
