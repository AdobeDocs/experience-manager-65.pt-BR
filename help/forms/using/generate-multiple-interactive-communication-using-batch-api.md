---
title: Usar a API em lote para gerar várias comunicações interativas
description: Usar a API em lote para gerar várias comunicações interativas
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communication
feature: Interactive Communication
exl-id: f65d8eb9-4d2c-4a6e-825f-45bcfaa7ca75
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '2234'
ht-degree: 1%

---

# Gerar várias comunicações interativas usando a API em lote {#use-batch-api-to-generate-multiple-ic}

Você pode usar a API em lote para produzir várias comunicações interativas de um modelo. O modelo é uma comunicação interativa sem dados. A API em lote combina dados com um modelo para produzir uma comunicação interativa. A API é útil na produção em massa de comunicações interativas. Por exemplo, contas telefônicas, demonstrativos de cartão de crédito para vários clientes.

A API em lote aceita registros (dados) no formato JSON e de um Modelo de dados de formulário. O número de comunicações interativas produzidas é igual aos registros especificados no arquivo JSON de entrada no Modelo de dados de formulário configurado. Você pode usar a API para produzir as saídas Impressão e Web. A opção IMPRIMIR produz um documento PDF e a opção WEB produz dados no formato JSON para cada registro individual.

## Uso da API em lote {#using-the-batch-api}

Você pode usar a API em lote em conjunto com as Pastas vigiadas ou como uma API Rest independente. Você configura um modelo, um tipo de saída (HTML, PRINT ou Ambos), um local, um serviço de preenchimento prévio e o nome das comunicações interativas geradas para usar a API em lote.

Você combina um registro com um template de comunicação interativo para produzir uma comunicação interativa. As APIs em lote podem ler registros (dados para modelos de comunicação interativos) diretamente de um arquivo JSON ou de uma fonte de dados externa acessada por meio do modelo de dados de formulário. Você pode manter cada registro em um arquivo JSON separado ou criar uma matriz JSON para manter todos os registros em um único arquivo.

**Um único registro em um arquivo JSON**

```json
{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}
```

**Vários registros em um arquivo JSON**

```json
[{
   "employee": {
       "name": "John",
       "id": 1,
       "mobileNo": 9871996461,
       "age": 39
   }
},{
   "employee": {
       "name": "Jacob",
       "id": 2,
       "mobileNo": 9871996462,
       "age": 38
   }
},{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}]
```

### Uso da API em lote com pastas vigiadas {#using-the-batch-api-watched-folders}

Para facilitar a experiência da API, o AEM Forms fornece um serviço de Pasta assistida configurado para usar a API em lote, pronto para uso. Você pode acessar o serviço por meio da interface do usuário do AEM Forms para gerar várias comunicações interativas. Você também pode criar serviços personalizados de acordo com suas necessidades. Você pode usar os métodos listados abaixo para usar a API em lote com a pasta Assistida:

* Especificar dados de entrada (registros) no formato de arquivo JSON para produzir uma comunicação interativa
* Usar dados de entrada (registros) salvos em uma fonte de dados externa e acessados por um modelo de dados de formulário para produzir uma comunicação interativa

#### Especificar registros de dados de entrada no formato de arquivo JSON para produzir uma comunicação interativa {#specify-input-data-in-JSON-file-format}

Você combina um registro com um template de comunicação interativo para produzir uma comunicação interativa. Você pode criar um arquivo JSON separado para cada registro ou criar uma matriz JSON para manter todos os registros em um único arquivo:

Para criar comunicação interativa a partir de registros salvos em um arquivo JSON:

1. Crie um [Pasta assistida](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html) e configure-a para usar a API em lote:
   1. Faça logon na instância do autor do AEM Forms.
   1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Forms]** > **[!UICONTROL Configurar pasta assistida]**. Toque **[!UICONTROL Novo]**.
   1. Especifique a **[!UICONTROL Nome]** e físico **[!UICONTROL Caminho]** da pasta. Por exemplo, `c:\batchprocessing`.
   1. Selecione o **[!UICONTROL Serviço]** na **[!UICONTROL Processar arquivo usando]** campo.
   1. Selecione o **[!UICONTROL com.adobe.fd.ccm.multicanal.batch.impl.service.InterativeCommunicationBatchServiceImpl]** no **[!UICONTROL Nome do serviço]** campo.
   1. Especifique um **[!UICONTROL Padrão do arquivo de saída]**. Por exemplo, o %F/ [padrão](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) especifica que a Pasta assistida pode localizar arquivos de entrada em uma subpasta da pasta de entrada\pasta assistida.
1. Configurar parâmetros avançados:
   1. Abra o **[!UICONTROL Avançado]** e adicione as seguintes propriedades personalizadas:

      | Propriedade | Tipo | Descrição |
      |--- |--- |--- |
      | templatePath | Sequência de caracteres | Especifique o caminho do modelo de comunicação interativa a ser usado. Por exemplo, /content/dam/formsanddocuments/testsample/mediumic. É uma propriedade obrigatória. |
      | recordPath | Sequência de caracteres | O valor do campo recordPath ajuda a definir o nome de uma comunicação interativa. Você pode definir o caminho de um campo de um registro como valor do campo recordPath. Por exemplo, se você especificar /employee/Id, o valor do campo de id se tornará o nome da comunicação interativa correspondente. O valor padrão é aleatório [UUID aleatório](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |
      | usePrefillService | Booleano | Defina o valor como False. Você pode usar o parâmetro usePrefillService para preencher previamente a comunicação interativa com os dados obtidos do serviço de preenchimento prévio configurado para a comunicação interativa correspondente. Quando usePrefillService é definido como true, os dados JSON de entrada (para cada registro) são tratados como Argumentos do FDM. O valor padrão é false. |
      | batchType | Sequência de caracteres | Defina o valor como PRINT, WEB ou WEB_AND_PRINT. O valor padrão é WEB_AND_PRINT. |
      | locale | Sequência de caracteres | Especifique o local da comunicação interativa de saída. O serviço pronto para uso não usa a opção de local, mas você pode criar um serviço personalizado para gerar comunicações interativas localizadas. O valor padrão é en_US |

   1. Toque **[!UICONTROL Criar]** A pasta assistida é criada.
1. Use a pasta assistida para gerar comunicação interativa:
   1. Abra a pasta assistida. Navegue até a pasta de entrada.
   1. Crie uma pasta na pasta de entrada e coloque o arquivo JSON na pasta recém-criada.
   1. Aguarde a Pasta assistida processar o arquivo. Quando o processamento é iniciado, o arquivo de entrada e a subpasta contendo o arquivo são movidos para a pasta de preparo.
   1. Abra a pasta de saída para exibir a saída:
      * Quando você especifica a opção IMPRIMIR na Configuração de pasta assistida, a saída do PDF para a comunicação interativa é gerada.
      * Quando você especifica a opção WEB na Configuração de pasta assistida, um arquivo JSON por registro é gerado. Você pode usar o arquivo JSON para [preencher previamente um template da web](#web-template).
      * Quando você especifica as opções IMPRIMIR e WEB, são gerados documentos PDF e um arquivo JSON por registro.

#### Use dados de entrada salvos em uma fonte de dados externa e acessados pelo modelo de dados de formulário para produzir uma comunicação interativa {#use-fdm-as-data-source}

Você combina dados (registros) salvos em uma fonte de dados externa com um template de comunicação interativo para produzir uma comunicação interativa. Ao criar uma comunicação interativa, você a conecta a uma fonte de dados externa por meio de um FDM (Form Data Model) para acessar os dados. Você pode configurar o serviço de processo em lote de pastas vigiadas para buscar dados usando o mesmo Modelo de dados de formulário de uma fonte de dados externa. Para [criar uma comunicação interativa a partir de registros salvos em uma fonte de dados externa](https://docs.adobe.com/content/help/en/experience-manager-64/forms/form-data-model/work-with-form-data-model.html):

1. Configure o Modelo de dados de formulário do modelo:
   1. Abra o Modelo de dados de formulário associado ao modelo de comunicação interativo.
   1. Selecione o OBJETO MODELO DE NÍVEL SUPERIOR e toque em Editar propriedades.
   1. Selecione o serviço de busca ou obtenção no campo Serviço de leitura no painel Editar propriedades .
   1. Toque no ícone de lápis para o argumento do serviço de leitura para vincular o argumento a um Atributo de solicitação e especifique o valor de vínculo. Ele vincula o argumento de serviço ao atributo de vínculo especificado ou ao valor literal, que é passado ao serviço como um argumento para buscar detalhes associados ao valor especificado na fonte de dados.

      <br>
        Neste exemplo, o argumento id pega o valor do atributo id do perfil do usuário e o transmite como um argumento para o serviço de leitura. Ele lerá e retornará valores de propriedades associadas do objeto de modelo de dados de funcionário para a id especificada. Portanto, se você especificar 00250 no campo id do formulário, o serviço de leitura lerá os detalhes do funcionário com a ID 00250 do funcionário.
        <br>

      ![Configurar atributo de solicitação](assets/request-attribute.png)

   1. Salve as propriedades e o Modelo de dados de formulário.
1. Configurar valor para Atributo de solicitação:
   1. Crie um arquivo .json em seu sistema de arquivos e abra-o para edição.
   1. Crie uma matriz JSON e especifique o atributo principal para buscar dados do Modelo de dados de formulário. Por exemplo, o JSON a seguir solicita que o FDM envie dados de registros onde id é 27126 ou 27127:

      ```json
          [
              {
                  "id": 27126
              },
              {
                  "id": 27127
              }
          ]
      ```

   1. Salve e feche o arquivo.

1. Crie um [Pasta assistida](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html) e configure-a para usar o serviço de API em lote:
   1. Faça logon na instância do autor do AEM Forms.
   1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Forms]** > **[!UICONTROL Configurar pasta assistida]**. Toque **[!UICONTROL Novo]**.
   1. Especifique a **[!UICONTROL Nome]** e físico **[!UICONTROL Caminho]** da pasta. Por exemplo, `c:\batchprocessing`.
   1. Selecione o **[!UICONTROL Serviço]** na **[!UICONTROL Processar arquivo usando]** campo.
   1. Selecione o **[!UICONTROL com.adobe.fd.ccm.multicanal.batch.impl.service.InterativeCommunicationBatchServiceImpl]** no **[!UICONTROL Nome do serviço]** campo.
   1. Especifique um **[!UICONTROL Padrão do arquivo de saída]**. Por exemplo, o %F/ [padrão](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) especifica que a Pasta assistida pode localizar arquivos de entrada em uma subpasta da pasta de entrada\pasta assistida.
1. Configurar parâmetros avançados:
   1. Abra o **[!UICONTROL Avançado]** e adicione as seguintes propriedades personalizadas:

      | Propriedade | Tipo | Descrição |
      |--- |--- |--- |
      | templatePath | Sequência de caracteres | Especifique o caminho do modelo de comunicação interativa a ser usado. Por exemplo, /content/dam/formsanddocuments/testsample/mediumic. É uma propriedade obrigatória. |
      | recordPath | Sequência de caracteres | O valor do campo recordPath ajuda a definir o nome de uma comunicação interativa. Você pode definir o caminho de um campo de um registro como valor do campo recordPath. Por exemplo, se você especificar /employee/Id, o valor do campo de id se tornará o nome da comunicação interativa correspondente. O valor padrão é aleatório [UUID aleatório](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |  |
      | usePrefillService | Booleano | Defina o valor como True. O valor padrão é false.  Quando o valor é definido como true, a API em lote lê os dados do Modelo de dados de formulário configurado e os preenche para a comunicação interativa. Quando usePrefillService é definido como true, os dados JSON de entrada (para cada registro) são tratados como Argumentos do FDM. |
      | batchType | Sequência de caracteres | Defina o valor como PRINT, WEB ou WEB_AND_PRINT. O valor padrão é WEB_AND_PRINT. |
      | locale | Sequência de caracteres | Especifique o local da comunicação interativa de saída. O serviço pronto para uso não usa a opção de local, mas você pode criar um serviço personalizado para gerar comunicações interativas localizadas. O valor padrão é en_US. |

   1. Toque **[!UICONTROL Criar]** A pasta assistida é criada.
1. Use a pasta assistida para gerar comunicação interativa:
   1. Abra a pasta assistida. Navegue até a pasta de entrada.
   1. Crie uma pasta na pasta de entrada. Coloque o arquivo JSON criado na Etapa 2 na pasta recém-criada.
   1. Aguarde a Pasta assistida processar o arquivo. Quando o processamento é iniciado, o arquivo de entrada e a subpasta contendo o arquivo são movidos para a pasta de preparo.
   1. Abra a pasta de saída para exibir a saída:
      * Quando você especifica a opção IMPRIMIR na Configuração de pasta assistida, a saída do PDF para a comunicação interativa é gerada.
      * Quando você especifica a opção WEB na Configuração de pasta assistida, um arquivo JSON por registro é gerado. Você pode usar o arquivo JSON para [preencher previamente um template da web](#web-template).
      * Quando você especifica as opções IMPRIMIR e WEB, são gerados documentos PDF e um arquivo JSON por registro.

## Chamar a API em lote usando solicitações REST

Você pode invocar [a API em lote](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/index.html) por meio de solicitações de transferência de estado de representação (REST). Ele permite fornecer um terminal REST para que outros usuários acessem a API e configurem seus próprios métodos de processamento, armazenamento e personalização da comunicação interativa. Você pode desenvolver seu próprio servlet Java personalizado para implantar a API na instância do AEM.

Antes de implantar o servlet Java, verifique se você tem uma comunicação interativa e se os arquivos de dados correspondentes estão prontos. Execute as seguintes etapas para criar e implantar o servlet Java:

1. Faça logon na instância do AEM e crie uma Comunicação interativa. Para utilizar a comunicação interativa mencionada no código de amostra a seguir, [clique aqui](assets/SimpleMediumIC.zip).
1. [Criar e implantar um projeto de AEM usando o Apache Maven](https://helpx.adobe.com/experience-manager/using/maven_arch13.html) na sua instância de AEM.
1. Adicionar [AEM Forms Client SDK versão 6.0.12](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) ou posteriormente na lista de dependências do arquivo POM do projeto AEM. Por exemplo,

   ```xml
       <dependency>
           <groupId>com.adobe.aemfd</groupId>
           <artifactId>aemfd-client-sdk</artifactId>
           <version>6.0.122</version>
       </dependency>
   ```

1. Abra o projeto do Java e crie um arquivo .java, por exemplo, CCMBatchServlet.java. Adicione o seguinte código ao arquivo:

   ```java
           package com.adobe.fd.ccm.multichannel.batch.integration;
   
           import java.io.File;
           import java.io.FileInputStream;
           import java.io.FileOutputStream;
           import java.io.IOException;
           import java.io.InputStream;
           import java.io.PrintWriter;
           import java.util.List;
           import javax.servlet.Servlet;
           import org.apache.commons.io.IOUtils;
           import org.apache.sling.api.SlingHttpServletRequest;
           import org.apache.sling.api.SlingHttpServletResponse;
           import org.apache.sling.api.servlets.SlingAllMethodsServlet;
           import org.json.JSONArray;
           import org.json.JSONObject;
           import org.osgi.service.component.annotations.Component;
           import org.osgi.service.component.annotations.Reference;
   
           import com.adobe.fd.ccm.multichannel.batch.api.builder.BatchConfigBuilder;
           import com.adobe.fd.ccm.multichannel.batch.api.factory.BatchComponentBuilderFactory;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchConfig;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchInput;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchType;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RecordResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RenditionResult;
           import com.adobe.fd.ccm.multichannel.batch.api.service.BatchGeneratorService;
           import com.adobe.fd.ccm.multichannel.batch.util.BatchConstants;
           import java.util.Date;
   
   
           @Component(service=Servlet.class,
           property={
                   "sling.servlet.methods=GET",
                   "sling.servlet.paths="+ "/bin/batchServlet"
           })
           public class CCMBatchServlet extends SlingAllMethodsServlet {
   
               @Reference
               private BatchGeneratorService batchGeneratorService;
               @Reference
               private BatchComponentBuilderFactory batchBuilderFactory;
               public void doGet(SlingHttpServletRequest req, SlingHttpServletResponse resp) {
                   try {
                       executeBatch(req,resp);
                   } catch (Exception e) {
                       e.printStackTrace();
                   }
               }
               private void executeBatch(SlingHttpServletRequest req, SlingHttpServletResponse resp) throws Exception {
                   int count = 0;
                   JSONArray inputJSONArray = new JSONArray();
                   String filePath = req.getParameter("filePath");
                   InputStream is = new FileInputStream(filePath);
                   String data = IOUtils.toString(is);
                   try {
                       // If input file is json object, then create json object and add in json array, if not then try for json array
                       JSONObject inputJSON = new JSONObject(data);
                       inputJSONArray.put(inputJSON);
                   } catch (Exception e) {
                       try {
                           // If input file is json array, then iterate and add all objects into inputJsonArray otherwise throw exception
                           JSONArray inputArray = new JSONArray(data);
                           for(int i=0;i<inputArray.length();i++) {
                               inputJSONArray.put(inputArray.getJSONObject(i));
                           }
                       } catch (Exception ex) {
                           throw new Exception("Invalid JSON Data. File name : " + filePath, ex);
                       }
                   }
                   BatchInput batchInput = batchBuilderFactory.getBatchInputBuilder().setData(inputJSONArray).setTemplatePath("/content/dam/formsanddocuments/[path of the interactive communcation]").build();
                   BatchConfig batchConfig = batchBuilderFactory.getBatchConfigBuilder().setBatchType(BatchType.WEB_AND_PRINT).build();
                   BatchResult batchResult = batchGeneratorService.generateBatch(batchInput, batchConfig);
                   List<RecordResult> recordList = batchResult.getRecordResults();
                   JSONObject result = new JSONObject();
                   for (RecordResult recordResult : recordList) {
                       String recordId = recordResult.getRecordID();
                       for (RenditionResult renditionResult : recordResult.getRenditionResults()) {
                           if (renditionResult.isRecordPassed()) {
                               InputStream output = renditionResult.getDocumentStream().getInputStream();
                               result.put(recordId +"_"+renditionResult.getContentType(), output);
   
                               Date date= new Date();
                               long time = date.getTime();
   
                               // Print output
                               if(getFileExtension(renditionResult.getContentType()).equalsIgnoreCase(".json")) {
                                   File file = new File(time + getFileExtension(renditionResult.getContentType()));
                                   copyInputStreamToFile(output, file);
                               } else
                               {
                                   File file = new File(time + getFileExtension(renditionResult.getContentType()));
                                   copyInputStreamToFile(output, file);
                               }
                           }
                       }
                   }
                   PrintWriter writer = resp.getWriter();
                   JSONObject resultObj = new JSONObject();
                   resultObj.put("result", result);
                   writer.write(resultObj.toString());
               }
   
   
               private static void copyInputStreamToFile(InputStream inputStream, File file)
                       throws IOException {
   
                       try (FileOutputStream outputStream = new FileOutputStream(file)) {
   
                           int read;
                           byte[] bytes = new byte[1024];
   
                           while ((read = inputStream.read(bytes)) != -1) {
                               outputStream.write(bytes, 0, read);
                           }
   
                       }
   
                   }
   
   
               private String getFileExtension(String contentType) {
                   if (contentType.endsWith(BatchConstants.JSON)) {
                       return ".json";
                   } else return ".pdf";
               }
   
   
           }
   ```

1. No código acima, substitua o caminho do modelo (setTemplatePath) pelo caminho do modelo e defina o valor da API setBatchType:
   * Quando você especifica a saída PDF da opção IMPRIMIR para a comunicação interativa é gerada.
   * Quando você especifica a opção WEB, um arquivo JSON por registro é gerado. Você pode usar o arquivo JSON para [preencher previamente um template da web](#web-template).
   * Quando você especifica as opções IMPRIMIR e WEB, são gerados documentos PDF e um arquivo JSON por registro.

1. [Use o maven para implantar o código atualizado na sua instância do AEM](https://helpx.adobe.com/experience-manager/using/maven_arch13.html#BuildtheOSGibundleusingMaven).
1. Chame a API em lote para gerar a comunicação interativa. A API em lote retorna um fluxo de arquivos PDF e .json, dependendo do número de registros. Você pode usar o arquivo JSON para [preencher previamente um template da web](#web-template). Se você usar o código acima, a API será implantada em `http://localhost:4502/bin/batchServlet`. O código imprime e retorna um fluxo de um PDF e arquivos JSON.

### Preencher previamente um modelo da Web {#web-template}

Quando você define o batchType para renderizar o Canal da Web, a API gera um arquivo JSON para cada registro de dados. Você pode usar a seguinte sintaxe para unir o arquivo JSON ao Canal da Web correspondente para gerar uma comunicação interativa:

**Sintaxe**
`http://host:port/<template-path>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=<guide-merged-json-path>`

**Exemplo**
Se o arquivo JSON estiver em `C:\batch\mergedJsonPath.json` e você usa o modelo de comunicação interativa abaixo: `http://host:port/content/dam/formsanddocuments/testsample/mediumic/jcr:content?channel=web`

Em seguida, o seguinte URL no nó de publicação exibe o Canal da Web da comunicação interativa
`http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/batch/mergedJsonData.json`

Além de salvar os dados no sistema de arquivos, você armazena arquivos JSON no repositório CRX, no sistema de arquivos, no servidor da Web ou pode acessar dados por meio do serviço de preenchimento prévio OSGI. Sintaxe para unir dados usando vários protocolos são:

* **Protocolo CRX**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=crx:///tmp/fd/af/mergedJsonData.json`

* **Protocolo de arquivo**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/Users/af/mergedJsonData.json`

* **Pré-carregar protocolo de serviço**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=service://[SERVICE_NAME]/[IDENTIFIER]`

   SERVICE_NAME refere-se ao nome do serviço de preenchimento prévio OSGI. Consulte Criar e executar um serviço de preenchimento prévio.

   IDENTIFIER refere-se a quaisquer metadados exigidos pelo serviço de preenchimento prévio OSGI para buscar os dados de preenchimento prévio. Um identificador para o usuário conectado é um exemplo de metadados que podem ser usados.

* **Protocolo HTTP**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=http://localhost:8000/somesamplexmlfile.xml`

>[!NOTE]
>
>Somente o protocolo CRX é ativado por padrão. Para ativar outros protocolos compatíveis, consulte [Configuração do serviço de preenchimento prévio usando o Configuration Manager](https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#ConfiguringprefillserviceusingConfigurationManager).
