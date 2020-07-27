---
title: Trabalhar com utilitários XMP
seo-title: Trabalhar com utilitários XMP
description: 'null'
seo-description: 'null'
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 1%

---


# Trabalhar com utilitários XMP {#working-with-xmp-utilities}

**Sobre o XMP Utilities Service**

Os documentos PDF contêm metadados, que são informações sobre o documento como distinguido do conteúdo do documento, como texto e gráficos. O Adobe Extensible Metadata Platform (XMP) é um padrão para manipular metadados de documentos.

O serviço XMP Utilities pode recuperar e salvar metadados XMP de documentos PDF e importar metadados XMP para documentos PDF.

Você pode realizar essas tarefas usando o serviço Utilitários XMP:

* Importe metadados para documentos PDF. (Consulte [Importação de metadados para Documentos](xmp-utilities.md#importing-metadata-into-pdf-documents)PDF.)
* Exporte metadados de documentos PDF. (Consulte [Exportação de metadados de Documentos](xmp-utilities.md#exporting-metadata-from-pdf-documents)PDF.)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários XMP, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importação de metadados para Documentos PDF {#importing-metadata-into-pdf-documents}

Você pode usar o Java Utilitários XMP e as APIs de serviço da Web para importar de forma programática metadados XMP para um documento PDF. Os metadados fornecem informações sobre um documento PDF, como o autor do documento e as palavras-chave relacionadas ao documento. Os metadados podem ser localizados na caixa de diálogo Propriedades do Documento, conforme mostrado na ilustração a seguir.

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

Para importar metadados programaticamente para um documento PDF, é possível usar um documento XML existente que especifica os valores de metadados ou usar um objeto do tipo `XMPUtilityMetadata`. (Consulte Referência [da API do](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.)

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
>Para obter mais informações sobre o serviço Utilitários XMP, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para importar metadados XMP para um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente XMPUUtilityService.
1. Chame a operação de importação de metadados XMP.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criação de um cliente XMPUutilityService**

Antes de poder executar programaticamente uma operação de Utilitários XMP, você deve criar um cliente XMPUUtilityService. Com a API Java, isso é feito criando um `XMPUtilityServiceClient` objeto. Com a API de serviço da Web, isso é feito usando um `XMPUtilityServiceService` objeto.

**Chamar a operação de importação de metadados XMP**

Depois de criar o cliente de serviço, você pode chamar uma das operações de importação de metadados XMP para importar os metadados XMP para o documento PDF especificado.

**Consulte também:**

[Importar metadados XMP usando a API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importação de metadados XMP usando a API de serviço da Web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importar metadados XMP usando a API Java {#import-xmp-metadata-using-the-java-api}

Importe metadados XMP usando a XMP Utilities API (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho da classe do seu projeto Java.

   >[!NOTE]
   >
   >O arquivo adobe-pdfutility-client.jar contém classes que permitem chamar programaticamente o serviço Utilitários XMP.

1. Criação de um cliente XMPUutilityService

   Crie um `XMPUtilityServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contenha propriedades de conexão.

1. Chamar a operação de importação de metadados XMP

   Para modificar os metadados XMP, chame o método do `XMPUtilityServiceClient` objeto `importMetadata` ou seu `importXMP` método.

   Se você usar o `importMetadata` método, passe os seguintes valores:

   * Um `com.adobe.idp.Document` objeto que representa o arquivo PDF.
   * Um `XMPUtilityMetadata` objeto que contém os metadados a serem importados.

   Se você usar o `importXMP` método, passe os seguintes valores:

   * Um `com.adobe.idp.Document` objeto que representa o arquivo PDF.
   * Um `com.adobe.idp.Document` objeto que representa um arquivo XML que contém os metadados a serem importados.

   Em ambos os casos, o valor retornado é um `com.adobe.idp.Document` objeto que representa o arquivo PDF com os metadados recém-importados. Em seguida, é possível salvar esse objeto em disco.

**Consulte também:**

[Importação de metadados para Documentos PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importação de metadados XMP usando a API de serviço da Web {#importing-xmp-metadata-using-the-web-service-api}

Para importar de forma programática metadados XMP usando a API de serviço da Web de Utilitários XMP, execute as seguintes tarefas:

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o arquivo WSDL do serviço de Utilitários XMP. (Consulte [Invocando AEM Forms usando a codificação](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)Base64.)
   * Faça referência ao assembly do cliente Microsoft .NET. (Consulte [Criação de um assembly de cliente .NET que usa a codificação](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)Base64.)

1. Criação de um cliente XMPUutilityService

   Crie um `XMPUtilityServiceService` objeto usando seu construtor de classe proxy.

1. Chamar a operação de importação de metadados XMP

   Para modificar os metadados XMP, chame o método do `XMPUtilityServiceService` objeto `importMetadata` ou seu `importXMP` método.

   Se você usar o `importMetadata` método, passe os seguintes valores:

   * Um `BLOB` objeto que representa o arquivo PDF.
   * Um `XMPUtilityMetadata` objeto que contém os metadados a serem importados.

   Se você usar o `importXMP` método, passe os seguintes valores:

   * Um `BLOB` objeto que representa o arquivo PDF.
   * Um `BLOB` objeto que representa um arquivo XML que contém os metadados a serem importados.

   Em ambos os casos, o valor retornado é um `BLOB` objeto que representa o arquivo PDF com os metadados recém-importados. Em seguida, é possível salvar esse objeto em disco.

**Consulte também:**

[Importação de metadados para Documentos PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Invocar AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criação de um assembly de cliente .NET que usa a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Exportação de metadados de Documentos PDF {#exporting-metadata-from-pdf-documents}

Você pode usar o Java Utilitários XMP e as APIs de serviço da Web para recuperar e salvar programaticamente os metadados XMP de um documento PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários XMP, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para exportar metadados XMP de um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente XMPUUtilityService.
1. Chame a operação de exportação de metadados XMP.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criação de um cliente XMPUutilityService**

Antes de poder executar programaticamente uma operação de Utilitários XMP, você deve criar um cliente XMPUUtilityService. Com o Java AP, isso é feito criando um `XMPUtilityServiceClient` objeto. Com a API de serviço da Web, isso é feito usando um `XMPUtilityServiceService` objeto.

**Chamar a operação de exportação de metadados XMP**

Depois de criar o cliente de serviço, você pode chamar uma das operações de exportação de metadados XMP, que podem ser usadas para inspecionar os metadados XMP ou salvá-los em disco.

**Consulte também:**

[Importar metadados XMP usando a API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importação de metadados XMP usando a API de serviço da Web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar metadados XMP usando a API Java {#export-xmp-metadata-using-the-java-api}

Exporte metadados XMP usando a API de utilitários XMP (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho da classe do seu projeto Java.

   >[!NOTE]
   >
   >O arquivo adobe-pdfutility-client.jar contém classes que permitem chamar programaticamente o serviço Utilitário XMP.

1. Criação de um cliente XMPUutilityService

   Crie um `XMPUtilityServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contenha propriedades de conexão.

1. Chamar a operação de importação de metadados XMP

   Para inspecionar os metadados XMP, chame o método do `XMPUtilityServiceClient` objeto `exportMetadata` e transmita um `com.adobe.idp.Document` objeto que representa o arquivo PDF. O método retorna um `XMPUtilityMetadata` objeto que contém os metadados recuperados.

   Para recuperar e salvar os metadados XMP, chame o método do `XMPUtilityServiceClient` objeto `exportXMP` e transmita um `com.adobe.idp.Document` objeto que representa o arquivo PDF. O método retorna um `com.adobe.idp.Document` objeto que contém os metadados recuperados, que podem ser salvos subsequentemente em disco como um arquivo XML.

**Consulte também:**

[Exportação de metadados de Documentos PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar metadados XMP usando a API de serviço da Web {#export-xmp-metadata-using-the-web-service-api}

Exporte metadados XMP usando a XMP Utilities API (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o arquivo WSDL do serviço de Utilitários XMP.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criação de um cliente XMPUutilityService

   Crie um `XMPUtilityServiceService` objeto usando seu construtor de classe proxy.

1. Chamar a operação de importação de metadados XMP

   Para inspecionar os metadados XMP, chame o método do `XMPUtilityServiceClient` objeto `exportMetadata` e transmita um `BLOB` objeto que representa o arquivo PDF. O método retorna um `XMPUtilityMetadata` objeto que contém os metadados recuperados.

   Para recuperar e salvar os metadados XMP, chame o método do `XMPUtilityServiceClient` objeto `exportXMP` e transmita um `BLOB` objeto que representa o arquivo PDF. O método retorna um `BLOB` objeto que contém os metadados recuperados, que podem ser salvos subsequentemente em disco como um arquivo XML.

**Consulte também:**

[Exportação de metadados de Documentos PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Invocar AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criação de um assembly de cliente .NET que usa a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
