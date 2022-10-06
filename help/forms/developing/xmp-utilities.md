---
title: Trabalhar com utilitários XMP
seo-title: Working with XMP Utilities
description: Use os Utilitários XMP APIs do Java e do serviço da Web para importar programaticamente metadados XMP em um documento do PDF e recuperar e salvar XMP metadados de um documento do PDF.
seo-description: Use the XMP Utilities Java and Web Service APIs to programmatically import XMP metadata into a PDF document and retrieve and save XMP metadata from a PDF document.
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
role: Developer
exl-id: cff65f74-ba95-438e-88a4-5ec7d22aafba
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 0%

---

# Trabalhar com utilitários XMP {#working-with-xmp-utilities}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

**Sobre o Serviço de Utilitários XMP**

Os documentos do PDF contêm metadados, que são informações sobre o documento como distinto do conteúdo do documento, como texto e gráficos. A Plataforma de metadados extensível do Adobe (XMP) é um padrão para manipular metadados de documento.

O serviço Utilitários de XMP pode recuperar e salvar metadados XMP de documentos PDF e importar XMP metadados para documentos PDF.

Você pode realizar essas tarefas usando o serviço Utilitários XMP:

* Importe metadados em documentos PDF. (Consulte [Importação de metadados para documentos do PDF](xmp-utilities.md#importing-metadata-into-pdf-documents).)
* Exporte metadados de documentos PDF. (Consulte [Exportação de metadados de documentos do PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários XMP, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importação de metadados para documentos do PDF {#importing-metadata-into-pdf-documents}

Você pode usar o Java Utilitários XMP e as APIs de serviço da Web para importar programaticamente metadados XMP em um documento do PDF. Os metadados fornecem informações sobre um documento PDF, como o autor do documento e palavras-chave relacionadas ao documento. Os metadados podem ser localizados na caixa de diálogo Propriedades do documento, conforme mostrado na ilustração a seguir.

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

Para importar metadados programaticamente para um documento PDF, você pode usar um documento XML existente que especifica os valores de metadados ou pode usar um objeto do tipo `XMPUtilityMetadata`. (Consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

>[!NOTE]
>
>Esta seção discute como usar um documento XML para importar metadados para um documento PDF.

O código XML a seguir contém valores de metadados que correspondem à ilustração anterior. Por exemplo, observe os itens em negrito, que especificam palavras-chave.

```xml
 <?xpacket begin="?" id="W5M0MpCehiHzreSzNTczkc9d"?>
 <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="Adobe XMP Core 4.2-jc015 52.349034, 2008 Jun 20 00:30:39-PDT (debug)">
       <rdf:RDF xmlns:rdf="https://www.w3.org/1999/02/22-rdf-syntax-ns#">
          <rdf:Description rdf:about=""
                xmlns:xmp="https://ns.adobe.com/xap/1.0/">
             <xmp:MetadataDate>2008-10-22T10:52:21-04:00</xmp:MetadataDate>
             <xmp:CreatorTool>AEM Forms</xmp:CreatorTool>
             <xmp:ModifyDate>2008-10-22T10:52:21-04:00</xmp:ModifyDate>
             <xmp:CreateDate>2008-02-13T11:00:18-05:00</xmp:CreateDate>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:pdf="https://ns.adobe.com/pdf/1.3/">
             <pdf:Producer>AEM Forms</pdf:Producer>
             <pdf:Keywords>keyword1, keyword2, keyword3,keyword4</pdf:Keywords>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:xmpMM="https://ns.adobe.com/xap/1.0/mm/">
             <xmpMM:DocumentID>uuid:1cce1f84-331e-4d8d-8538-15441c271dd7</xmpMM:DocumentID>
             <xmpMM:InstanceID>uuid:cdda0ca6-7c91-4771-9dc9-796c8fe59350</xmpMM:InstanceID>
          </rdf:Description>
          <rdf:Description rdf:about=""
                >
             <dc:format>application/pdf</dc:format>
             <dc:description>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Adobe Designer Sample</rdf:li>
                </rdf:Alt>
             </dc:description>
             <dc:title>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Grant Application</rdf:li>
                </rdf:Alt>
             </dc:title>
             <dc:creator>
                <rdf:Seq>
                   <rdf:li>Tony Blue</rdf:li>
                </rdf:Seq>
             </dc:creator>
             <dc:subject>
                <rdf:Bag>
                   <rdf:li>keyword1</rdf:li>
                   <rdf:li>keyword2</rdf:li>
                   <rdf:li>keyword3</rdf:li>
                   <rdf:li>keyword4</rdf:li>
                </rdf:Bag>
             </dc:subject>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:desc="https://ns.adobe.com/xfa/promoted-desc/">
             <desc:version rdf:parseType="Resource">
                <rdf:value>1.0</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:version>
             <desc:contact rdf:parseType="Resource">
                <rdf:value>Adobe Systems Incorporated</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:contact>
          </rdf:Description>
       </rdf:RDF>
 </x:xmpmeta>
```

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários XMP, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para importar metadados de XMP para um documento PDF, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente XMPUUtilityService.
1. Chame a operação de importação de metadados de XMP.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente XMPUtilmentService**

Antes de poder executar programaticamente uma operação Utilitários de XMP, você deve criar um cliente XMPUUtilityService. Com a API do Java, isso é feito criando uma `XMPUtilityServiceClient` objeto. Com a API do serviço da Web, isso é feito usando um `XMPUtilityServiceService` objeto.

**Chame a operação de importação de metadados de XMP**

Após criar o cliente de serviço, você pode invocar uma das operações de importação de metadados XMP para importar os metadados XMP para o documento PDF especificado.

**Consulte também**

[Importar metadados de XMP usando a API do Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importação de metadados de XMP usando a API do serviço da Web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importar metadados de XMP usando a API do Java {#import-xmp-metadata-using-the-java-api}

Importe XMP metadados usando a API de utilitários XMP (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho da classe do seu projeto Java.

   >[!NOTE]
   >
   >O arquivo adobe-pdfutility-client.jar contém classes que permitem chamar programaticamente o serviço Utilitários de XMP.

1. Criar um cliente XMPUtilmentService

   Crie um `XMPUtilityServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Chame a operação de importação de metadados de XMP

   Para modificar os metadados de XMP, chame o `XMPUtilityServiceClient` do objeto `importMetadata` método ou `importXMP` método .

   Se você usar a variável `importMetadata` , passe os seguintes valores:

   * A `com.adobe.idp.Document` que representa o arquivo PDF.
   * Um `XMPUtilityMetadata` objeto que contém os metadados a serem importados.

   Se você usar a variável `importXMP` , passe os seguintes valores:

   * A `com.adobe.idp.Document` que representa o arquivo PDF.
   * A `com.adobe.idp.Document` objeto que representa um arquivo XML que contém os metadados a serem importados.

   Em ambos os casos, o valor retornado é uma `com.adobe.idp.Document` que representa o arquivo PDF com os metadados recém-importados. Em seguida, você pode salvar esse objeto em disco.

**Consulte também**

[Importação de metadados para documentos do PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importação de metadados de XMP usando a API do serviço da Web {#importing-xmp-metadata-using-the-web-service-api}

Para importar XMP metadados de maneira programática usando a API do serviço da Web XMP Utilitários, execute as seguintes tarefas:

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o arquivo WSDL do serviço Utilitários XMP. (Consulte [Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Faça referência ao assembly do cliente Microsoft .NET. (Consulte [Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Criar um cliente XMPUtilmentService

   Crie um `XMPUtilityServiceService` usando seu construtor de classe proxy.

1. Chame a operação de importação de metadados de XMP

   Para modificar os metadados de XMP, chame o `XMPUtilityServiceService` do objeto `importMetadata` método ou `importXMP` método .

   Se você usar a variável `importMetadata` , passe os seguintes valores:

   * A `BLOB` que representa o arquivo PDF.
   * Um `XMPUtilityMetadata` objeto que contém os metadados a serem importados.

   Se você usar a variável `importXMP` , passe os seguintes valores:

   * A `BLOB` que representa o arquivo PDF.
   * A `BLOB` objeto que representa um arquivo XML que contém os metadados a serem importados.

   Em ambos os casos, o valor retornado é uma `BLOB` que representa o arquivo PDF com os metadados recém-importados. Em seguida, você pode salvar esse objeto em disco.

**Consulte também**

[Importação de metadados para documentos do PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Exportação de metadados de documentos do PDF {#exporting-metadata-from-pdf-documents}

Você pode usar o Java Utilitários XMP e as APIs de serviço da Web para recuperar e salvar programaticamente XMP metadados de um documento do PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários XMP, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para exportar XMP metadados de um documento PDF, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente XMPUUtilityService.
1. Chame a operação de exportação de metadados de XMP.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente XMPUtilmentService**

Antes de poder executar programaticamente uma operação Utilitários de XMP, você deve criar um cliente XMPUUtilityService. Com a API do Java, se isso for feito com a criação de um `XMPUtilityServiceClient` objeto. Com a API do serviço da Web, isso é feito usando um `XMPUtilityServiceService` objeto.

**Chame a operação de exportação de metadados de XMP**

Após criar o cliente de serviço, você pode invocar uma das operações de exportação de metadados de XMP, que pode ser usada para inspecionar os metadados de XMP ou salvá-los em disco.

**Consulte também**

[Importar metadados de XMP usando a API do Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importação de metadados de XMP usando a API do serviço da Web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar metadados de XMP usando a API Java {#export-xmp-metadata-using-the-java-api}

Exporte XMP metadados usando a API de utilitários XMP (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho da classe do seu projeto Java.

   >[!NOTE]
   >
   >O arquivo adobe-pdfutility-client.jar contém classes que permitem chamar programaticamente o serviço Utilitário de XMP.

1. Criar um cliente XMPUtilmentService

   Crie um `XMPUtilityServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Chame a operação de importação de metadados de XMP

   Para inspecionar os metadados de XMP, chame o `XMPUtilityServiceClient` do objeto `exportMetadata` e passar em um `com.adobe.idp.Document` que representa o arquivo PDF. O método retorna um `XMPUtilityMetadata` objeto que contém os metadados recuperados.

   Para recuperar e salvar os metadados do XMP, chame o `XMPUtilityServiceClient` do objeto `exportXMP` e passar em um `com.adobe.idp.Document` que representa o arquivo PDF. O método retorna um `com.adobe.idp.Document` objeto que contém os metadados recuperados, que podem ser salvos posteriormente em disco como um arquivo XML.

**Consulte também**

[Exportação de metadados de documentos do PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar metadados XMP usando a API de serviço da Web {#export-xmp-metadata-using-the-web-service-api}

Exporte XMP metadados usando a API de Utilitários XMP (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o arquivo WSDL do serviço Utilitários XMP.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar um cliente XMPUtilmentService

   Crie um `XMPUtilityServiceService` usando seu construtor de classe proxy.

1. Chame a operação de importação de metadados de XMP

   Para inspecionar os metadados de XMP, chame o `XMPUtilityServiceClient` do objeto `exportMetadata` e passar em um `BLOB` que representa o arquivo PDF. O método retorna um `XMPUtilityMetadata` objeto que contém os metadados recuperados.

   Para recuperar e salvar os metadados do XMP, chame o `XMPUtilityServiceClient` do objeto `exportXMP` e passar em um `BLOB` que representa o arquivo PDF. O método retorna um `BLOB` objeto que contém os metadados recuperados, que podem ser salvos posteriormente em disco como um arquivo XML.

**Consulte também**

[Exportação de metadados de documentos do PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
