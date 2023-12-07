---
title: Trabalhar com utilitários de XMP
description: Use as APIs de serviços da Web e Java de utilitários do XMP para importar programaticamente metadados do XMP para um documento do PDF e recuperar e salvar metadados do XMP de um documento do PDF.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: cff65f74-ba95-438e-88a4-5ec7d22aafba
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 0%

---

# Trabalhar com utilitários de XMP {#working-with-xmp-utilities}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

**Sobre o serviço de utilitários XMP**

Os documentos PDF contêm metadados, que são informações sobre o documento diferenciadas do conteúdo do documento, como texto e gráficos. A Plataforma de metadados extensíveis (XMP) do Adobe é um padrão para manipular metadados de documentos.

O serviço Utilitários XMP pode recuperar e salvar metadados XMP de documentos PDF e importar metadados XMP para documentos PDF.

Você pode realizar essas tarefas usando o serviço Utilitários XMP:

* Importe metadados em documentos do PDF. (Consulte [Importação de metadados para documentos PDF](xmp-utilities.md#importing-metadata-into-pdf-documents).)
* Exportar metadados de documentos do PDF. (Consulte [Exportar metadados de documentos do PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários XMP, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importação de metadados para documentos PDF {#importing-metadata-into-pdf-documents}

Você pode usar o Java Utilitários XMP e APIs de serviço da web para importar programaticamente metadados XMP em um documento PDF. Os metadados fornecem informações sobre um documento PDF, como o autor do documento e palavras-chave relacionadas ao documento. Os metadados podem ser exibidos na caixa de diálogo Propriedades do documento do documento, conforme mostrado na ilustração a seguir.

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

Para importar metadados de forma programática para um documento PDF, você pode usar um documento XML existente que especifique os valores de metadados ou usar um objeto do tipo `XMPUtilityMetadata`. (Consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

>[!NOTE]
>
>Esta seção discute como usar um documento XML para importar metadados em um documento PDF.

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

Para importar metadados de XMP para um documento do PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente XMPUutilityService.
1. Chame a operação de importação de metadados XMP.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente XMPUutilityService**

Antes de executar programaticamente uma operação de Utilitários XMP, você deve criar um cliente XMPUtilityService. Com a API Java, isso é feito criando um `XMPUtilityServiceClient` objeto. Com a API do serviço Web, isso é feito usando um `XMPUtilityServiceService` objeto.

**Chame a operação de importação de metadados XMP**

Depois de criar o cliente de serviço, você pode chamar uma das operações de importação de metadados XMP para importar os metadados XMP para o documento PDF especificado.

**Consulte também**

[Importar metadados XMP usando a API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importação de metadados XMP usando a API do serviço da Web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importar metadados XMP usando a API Java {#import-xmp-metadata-using-the-java-api}

Importe metadados de XMP usando a API de utilitários XMP (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho de classe do projeto Java.

   >[!NOTE]
   >
   >O arquivo adobe-pdfutility-client.jar contém classes que permitem chamar programaticamente o serviço de Utilitários XMP.

1. Criar um cliente XMPUutilityService

   Criar um `XMPUtilityServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Chame a operação de importação de metadados XMP

   Para modificar os metadados do XMP, chame o `XMPUtilityServiceClient` do objeto `importMetadata` método ou seus `importXMP` método.

   Se você usar o `importMetadata` , passe os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o arquivo PDF.
   * Um `XMPUtilityMetadata` objeto que contém os metadados a serem importados.

   Se você usar o `importXMP` , passe os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o arquivo PDF.
   * A `com.adobe.idp.Document` objeto que representa um arquivo XML que contém os metadados a serem importados.

   Em ambos os casos, o valor retornado é um `com.adobe.idp.Document` objeto que representa o arquivo PDF com os metadados importados recentemente. Em seguida, você pode salvar esse objeto em disco.

**Consulte também**

[Importação de metadados para documentos PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importação de metadados XMP usando a API do serviço da Web {#importing-xmp-metadata-using-the-web-service-api}

Para importar programaticamente metadados de XMP usando a API de serviço Web XMP Utilities, execute as seguintes tarefas:

1. Incluir arquivos de projeto

   * Crie um assembly cliente Microsoft .NET que consuma o arquivo WSDL do serviço de utilitários XMP. (Consulte [Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Referencie o assembly do cliente Microsoft .NET. (Consulte [Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Criar um cliente XMPUutilityService

   Criar um `XMPUtilityServiceService` usando seu construtor de classe de proxy.

1. Chame a operação de importação de metadados XMP

   Para modificar os metadados do XMP, chame o `XMPUtilityServiceService` do objeto `importMetadata` método ou seus `importXMP` método.

   Se você usar o `importMetadata` , passe os seguintes valores:

   * A `BLOB` objeto que representa o arquivo PDF.
   * Um `XMPUtilityMetadata` objeto que contém os metadados a serem importados.

   Se você usar o `importXMP` , passe os seguintes valores:

   * A `BLOB` objeto que representa o arquivo PDF.
   * A `BLOB` objeto que representa um arquivo XML que contém os metadados a serem importados.

   Em ambos os casos, o valor retornado é um `BLOB` objeto que representa o arquivo PDF com os metadados importados recentemente. Em seguida, você pode salvar esse objeto em disco.

**Consulte também**

[Importação de metadados para documentos PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Exportar metadados de documentos do PDF {#exporting-metadata-from-pdf-documents}

Você pode usar o Java Utilitários XMP e APIs de serviço da web para recuperar e salvar programaticamente metadados XMP de um documento PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários XMP, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para exportar metadados XMP de um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente XMPUutilityService.
1. Chame a operação de exportação de metadados XMP.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente XMPUutilityService**

Antes de executar programaticamente uma operação de Utilitários XMP, você deve criar um cliente XMPUtilityService. Com o AP Java, se isso for feito criando um `XMPUtilityServiceClient` objeto. Com a API do serviço Web, isso é feito usando um `XMPUtilityServiceService` objeto.

**Chame a operação de exportação de metadados XMP**

Depois de criar o cliente de serviço, você pode chamar uma das operações de exportação de metadados XMP, que podem ser usadas para inspecionar os metadados XMP ou salvá-los no disco.

**Consulte também**

[Importar metadados XMP usando a API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importação de metadados XMP usando a API do serviço da Web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar metadados XMP usando a API Java {#export-xmp-metadata-using-the-java-api}

Exporte metadados de XMP usando a API de utilitários XMP (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho de classe do projeto Java.

   >[!NOTE]
   >
   >O arquivo adobe-pdfutility-client.jar contém classes que permitem chamar programaticamente o serviço Utilitário XMP.

1. Criar um cliente XMPUutilityService

   Criar um `XMPUtilityServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Chame a operação de importação de metadados XMP

   Para inspecionar os metadados de XMP, chame o `XMPUtilityServiceClient` do objeto `exportMetadata` e transmitem em uma `com.adobe.idp.Document` objeto que representa o arquivo PDF. O método retorna um valor de `XMPUtilityMetadata` objeto que contém os metadados recuperados.

   Para recuperar e salvar os metadados do XMP, chame o `XMPUtilityServiceClient` do objeto `exportXMP` e transmitem em uma `com.adobe.idp.Document` objeto que representa o arquivo PDF. O método retorna um valor de `com.adobe.idp.Document` objeto que contém os metadados recuperados, os quais podem ser salvos em disco como um arquivo XML.

**Consulte também**

[Exportar metadados de documentos do PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar metadados de XMP usando a API do serviço da Web {#export-xmp-metadata-using-the-web-service-api}

Exporte metadados de XMP usando a API de utilitários XMP (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly cliente Microsoft .NET que consuma o arquivo WSDL do serviço de utilitários XMP.
   * Referencie o assembly do cliente Microsoft .NET.

1. Criar um cliente XMPUutilityService

   Criar um `XMPUtilityServiceService` usando seu construtor de classe de proxy.

1. Chame a operação de importação de metadados XMP

   Para inspecionar os metadados de XMP, chame o `XMPUtilityServiceClient` do objeto `exportMetadata` e transmitem em uma `BLOB` objeto que representa o arquivo PDF. O método retorna um valor de `XMPUtilityMetadata` objeto que contém os metadados recuperados.

   Para recuperar e salvar os metadados do XMP, chame o `XMPUtilityServiceClient` do objeto `exportXMP` e transmitem em uma `BLOB` objeto que representa o arquivo PDF. O método retorna um valor de `BLOB` objeto que contém os metadados recuperados, os quais podem ser salvos em disco como um arquivo XML.

**Consulte também**

[Exportar metadados de documentos do PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
