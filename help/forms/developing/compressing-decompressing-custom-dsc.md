---
title: Como transmitir credenciais usando cabeçalhos WS-security?
description: Saiba como transmitir credenciais usando cabeçalhos WS-security
source-git-commit: 730ae7cd6cd04eb6377b37eafe29db597e93cce3
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Compactar e descompactar arquivos usando uma AEM Forms no JEE Custom DSC {#compressing-decompressing-files}

## Conhecimento pré-requisito {#prerequisites}

Experimente o AEM Forms no JEE Process Management, programação básica do Java e criação de componente personalizado.

**Outros produtos necessários**

Editor Java como [Eclipse](https://www.eclipse.org/) ou [Netbeans IDE](https://netbeans.apache.org/)

## Nível do usuário {#user-level}

Intermediário

O AEM Forms no JEE permite que os desenvolvedores criem DSC personalizados (Contêiner do serviço de documento) para criar recursos enriquecidos prontos para uso. A criação desses componentes pode ser conectada à AEM Forms no ambiente de tempo de execução JEE e serve o propósito pretendido. Este artigo explica como criar um Serviço ZIP personalizado que pode ser usado para compactar uma lista de arquivos em um arquivo .zip e descompactar um .zip em uma lista de documentos.

## Criação de um componente DSC personalizado {#create-custom-dsc-component}

Crie um componente DSC personalizado com duas operações de serviço para compactar e descompactar a lista de documentos. Este componente usa o pacote java.util.zip para compactação e descompactação. Siga as etapas abaixo para criar um componente personalizado:

1. Adicionar o arquivo adobe-livecycle-client.jar à biblioteca
1. Adicionar os ícones necessários
1. Criar uma classe pública
1. Crie dois métodos públicos chamados UnzipDocument &amp; ZipDocuments
1. Escreva a lógica de Compactação e Descompactação

O código pode ser encontrado aqui:

```java
/*
 * Custom DSC : ZIP Utility
 * Purpose: This is a LiveCycle ES2 custom component used to Compress & Decompress List of Documents
 * Author: Nithiyanandam Dharmadass
 * Organization: Ministry of Finance, Kingdom of Bahrain
 * Last modified Date: 18/Apr/2011
 */
package nith.lces2.dsc;

import java.util.zip.ZipEntry;
import java.util.zip.ZipInputStream;
import com.adobe.idp.Document;
import java.io.ByteArrayOutputStream;
import java.io.InputStream;
import java.util.ArrayList;
import java.util.List;
import java.util.zip.ZipOutputStream;

public class ZIPService {

    static final int BUFFER = 2048; // 2MB buffer size

    public java.util.List UnzipDocument(com.adobe.idp.Document zipDocument) throws Exception {
        ZipInputStream zis = new ZipInputStream(zipDocument.getInputStream());

        ZipEntry zipFile;

        List resultList = new ArrayList();

        while ((zipFile = zis.getNextEntry()) != null) {

            ByteArrayOutputStream byteArrayOutStream = new ByteArrayOutputStream();

            int count;  // an int variable to hold the number of bytes read from input stream
            byte data[] = new byte[BUFFER];
            while ((count = zis.read(data, 0, BUFFER)) != -1) {
                byteArrayOutStream.write(data, 0, count);   // write to byte array
            }

            com.adobe.idp.Document unzippedDoc = new Document(byteArrayOutStream.toByteArray());  // create an idp document
            unzippedDoc.setAttribute("file", zipFile.getName());
            unzippedDoc.setAttribute("wsfilename", zipFile.getName());  // update the wsfilename attribute
            resultList.add(unzippedDoc);
        }
        return resultList;  // List of uncompressed documents
    }

    public com.adobe.idp.Document ZipDocuments(java.util.List listOfDocuments,java.lang.String zipFileName) throws Exception {

        if (listOfDocuments == null || listOfDocuments.size() == 0) {
            return null;
        }

        ByteArrayOutputStream byteArrayOutStream = new ByteArrayOutputStream();
        ZipOutputStream zos = new ZipOutputStream(byteArrayOutStream);  // ZIP Output Stream

        for (int i = 0; i < listOfDocuments.size(); i++) {
            Document doc = (Document) listOfDocuments.get(i);
            InputStream docInputStream = doc.getInputStream();
            ZipEntry zipEntry = new ZipEntry(doc.getAttribute("file").toString());
            zos.putNextEntry(zipEntry);
            int count;
            byte data[] = new byte[BUFFER];
            while ((count = docInputStream.read(data, 0, BUFFER)) != -1) {
                zos.write(data, 0, count);  // Read document content and add to zip entry
            }
            zos.closeEntry();
        }
        zos.flush();
        zos.close();

        Document zippedDoc = new Document(byteArrayOutStream.toByteArray());
        if(zipFileName==null || zipFileName.equals(""))
        {
            zipFileName = "CompressedList.zip";
        }
        zippedDoc.setAttribute("file", zipFileName);
        return zippedDoc;
    }
}
```

## Criação de um arquivo Component.XML {#create-component-xml-file}

Um arquivo component.xml deve ser criado dentro da pasta raiz do pacote que definiu as operações de serviço e seus parâmetros.

O arquivo component.xml é mostrado aqui:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<component xmlns="http://adobe.com/idp/dsc/component/document">
<!-- Unique id identifying this component -->
   <component-id>ZipService</component-id>

<!-- Version -->
   <version>1.0</version>

<!-- Start of the Service definition -->
   <services>
<!-- Unique name for service descriptor.
           The value is used as the default name for
           deployed services -->
      <service name="ZipService">
<!-- service implementation class definition -->
        <implementation-class>nith.lces2.dsc.ZIPService</implementation-class>

<!-- description -->
        <description>Compress or Decompress list of documents</description>

<!--  You can provide your own icons for a distinct look   -->
          <small-icon>icons/Zip_icon16.png</small-icon>
          <large-icon>icons/Zip_icon32.png</large-icon>


<!-- automatically deploys the service and starts it after installation -->
         <auto-deploy service-id="ZipService" />

         <operations>
<!-- method name in the interface setSmtpHost-->
            <operation name="UnzipDocument">
<!-- input parameters to the "send" method -->
              <input-parameter name="zipDocument" title="Input ZIP Document" type="com.adobe.idp.Document">
                    <hint>A ZIP File to be decompressed</hint>
                </input-parameter>
                <output-parameter name="resultList" title="Decompressed list of documents" type="java.util.List">
                    <hint>Decompressed ZIP list</hint>
                </output-parameter>
            </operation>
            <operation name="ZipDocuments">
<!-- input parameters to the "send" method -->
              <input-parameter name="listOfDocuments" title="List of Documents" type="java.util.List">
                    <hint>A list of documents to be Compressed</hint>
                </input-parameter>
                <input-parameter name="zipFileName" title="Result File Name" type="java.lang.String">
                    <hint>The name of compressed file (optional)</hint>
                </input-parameter>

                <output-parameter name="zippedDoc" title="Compressed Zip file" type="com.adobe.idp.Document">
                    <hint>Compressed ZIP File</hint>
                </output-parameter>
            </operation>
             </operations>
      </service>
   </services>
</component>
```

## Empacotamento e implantação do componente {#packaging-deploying-component}

1. Compile o projeto java e crie um arquivo .JAR.
1. Implante o componente (arquivo .JAR) na AEM Forms no tempo de execução do JEE por meio do Workbench.
1. Inicie o serviço no Workbench (consulte a Figura abaixo).

![Design do processo](assets/process-design.jpg)

## Uso do serviço ZIP em workflows {#using-zip-service-in-workflows}

A operação UnzipDocument do serviço personalizado agora pode aceitar uma variável de documento como entrada e retornar uma lista de variáveis de documento como saída.

![Descompactar documento](assets/unzip-doc.jpg)

Da mesma forma, a operação ZipDocuments do componente personalizado pode aceitar uma lista de documentos como entrada, compactá-los como um arquivo zip e retornar o documento compactado.

![Documento zip](assets/zip-doc.jpg)

A orquestração de fluxo de trabalho a seguir mostra como descompactar o arquivo ZIP fornecido, compactá-lo novamente em outro arquivo ZIP e retornar a saída (consulte a Figura abaixo).

![Fluxo de trabalho Descompactar CEP](assets/unzip-zip-process.jpg)

## Alguns casos de uso comercial {#business-use-cases}

Você pode usar esse Serviço ZIP nos seguintes casos de uso:

* Localize todos os arquivos em uma determinada pasta e retorne os arquivos como um documento compactado.

* Forneça um arquivo ZIP contendo vários documentos PDF que podem ser estendidos pelo leitor após descompactá-los. Isso requer o módulo AEM Forms no JEE Reader Extensions .

* Forneça um arquivo ZIP contendo um tipo heterogêneo de documento que pode ser descompactado e convertido como documento PDF usando o serviço Gerar PDF.

* A política protege uma lista de documentos e retorna como um arquivo ZIP.

* Permita que os usuários baixem todos os anexos de uma instância de processo como um único arquivo ZIP.



