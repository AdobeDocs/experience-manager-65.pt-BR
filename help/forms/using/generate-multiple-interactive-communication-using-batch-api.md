---
title: Usar a API de lote para gerar várias comunicações interativas
description: Usar a API de lote para gerar várias comunicações interativas
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communication
feature: Interactive Communication
exl-id: f65d8eb9-4d2c-4a6e-825f-45bcfaa7ca75
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 1%

---

# Gerar várias comunicações interativas usando a API em lote {#use-batch-api-to-generate-multiple-ic}

Você pode usar a API de lote para produzir várias comunicações interativas a partir de um modelo. O template é uma comunicação interativa sem dados. A API de lote combina dados com um modelo para produzir uma comunicação interativa. A API é útil na produção em massa de comunicações interativas. Por exemplo, contas de telefone, demonstrativos de cartão de crédito para vários clientes.

A API de lote aceita registros (dados) no formato JSON e de um modelo de dados de formulário. O número de comunicações interativas produzidas é igual aos registros especificados no arquivo JSON de entrada no Modelo de Dados de Formulário configurado. Você pode usar a API para produzir saídas de impressão e da Web. A opção IMPRIMIR produz um documento PDF e a opção WEB produz dados no formato JSON para cada registro individual.

## Uso da API em lote {#using-the-batch-api}

Você pode usar a API de lote com Pastas monitoradas ou como uma API Rest independente. Você configura um modelo, tipo de saída (HTML, PRINT ou Ambos), localidade, serviço de preenchimento prévio e nome para as comunicações interativas geradas para usar a API em lote.

Você combina um registro com um modelo de comunicação interativa para produzir uma comunicação interativa. As APIs em lote podem ler registros (dados para modelos de comunicação interativa) diretamente de um arquivo JSON ou de uma fonte de dados externa acessada por meio do modelo de dados de formulário. Você pode manter cada registro em um arquivo JSON separado ou criar uma matriz JSON para manter todos os registros em um único arquivo.

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

### Uso da API de lote com pastas monitoradas {#using-the-batch-api-watched-folders}

Para facilitar a experiência da API, o AEM Forms fornece um serviço de Pasta monitorada configurado para usar a API de lote, imediatamente. Você pode acessar o serviço por meio da interface do usuário do AEM Forms para gerar várias comunicações interativas. Você também pode criar serviços personalizados de acordo com suas necessidades. Você pode usar os métodos listados abaixo para usar a API em lote com a pasta monitorada:

* Especifique os dados de entrada (registros) no formato de arquivo JSON para poder produzir uma comunicação interativa.
* Use dados de entrada (registros) salvos em uma fonte de dados externa e acessados por meio de um modelo de dados de formulário para produzir uma comunicação interativa.

#### Especificar registros de dados de entrada no formato de arquivo JSON para produzir uma comunicação interativa {#specify-input-data-in-JSON-file-format}

Você combina um registro com um modelo de comunicação interativa para produzir uma comunicação interativa. Você pode criar um arquivo JSON separado para cada registro ou criar uma matriz JSON para manter todos os registros em um único arquivo:

Para criar a comunicação interativa a partir de registros salvos em um arquivo JSON:

1. Crie uma [Pasta monitorada](/help/forms/using/creating-configure-watched-folder.md) e configure-a para usar a API em lote:
   1. Faça logon na instância de autor do AEM Forms.
   1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Forms]** > **[!UICONTROL Configurar a Pasta Monitorada]**. Selecione **[!UICONTROL Novo]**.
   1. Especifique o **[!UICONTROL Nome]** e o **[!UICONTROL Caminho]** físico da pasta. Por exemplo, `c:\batchprocessing`.
   1. Selecione a opção **[!UICONTROL Serviço]** no campo **[!UICONTROL Processar Arquivo Usando]**.
   1. Selecione o serviço **[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InterativeCommunicationBatchServiceImpl]** no campo **[!UICONTROL Nome do Serviço]**.
   1. Especifique um **[!UICONTROL Padrão de Arquivo de Saída]**. Por exemplo, o %F/ [padrão](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/administrator-help/configuring-watched-folder-endpoints.html?lang=pt-BR#about-file-patterns) especifica que a Pasta monitorada pode localizar arquivos de entrada em uma subpasta da pasta Pasta monitorada\entrada.
1. Configurar parâmetros avançados:
   1. Abra a guia **[!UICONTROL Avançado]** e adicione as seguintes propriedades personalizadas:

      | Propriedade | Tipo | Descrição |
      |--- |--- |--- |
      | templatePath | String | Especifique o caminho do modelo de comunicação interativa a ser usado. Por exemplo, `/content/dam/formsanddocuments/testsample/mediumic`. É uma propriedade obrigatória. |
      | recordPath | String | O valor do campo recordPath ajuda a definir o nome de uma comunicação interativa. É possível definir o caminho de um campo de um registro como o valor do campo recordPath. Por exemplo, se você especificar /employee/Id, o valor do campo id se torna nome para a comunicação interativa correspondente. O valor padrão é um [UUID aleatório](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |
      | usePrefillService | Booleano | Defina o valor como Falso. Você pode usar o parâmetro usePrefillService para preencher previamente a comunicação interativa com dados obtidos do serviço de preenchimento prévio configurado para a comunicação interativa correspondente. Quando usePrefillService é definido como true, os dados JSON de entrada (para cada registro) são tratados como Argumentos FDM. O valor padrão é false. |
      | batchType | String | Defina o valor como PRINT, WEB ou WEB_AND_PRINT. O valor padrão é WEB_AND_PRINT. |
      | localidade | String | Especifique a localidade da comunicação interativa de saída. O serviço pronto para uso não usa a opção de local, mas você pode criar um serviço personalizado para gerar comunicações interativas localizadas. O valor padrão é en_US |

   1. Selecione **[!UICONTROL Criar]**.
1. Usar a pasta monitorada criada para gerar comunicação interativa:
   1. Abra a Pasta monitorada. Navegue até a pasta de entrada.
   1. Crie uma pasta na pasta de entrada e coloque o arquivo JSON na pasta recém-criada.
   1. Aguarde a Pasta monitorada processar o arquivo. Quando o processamento é iniciado, o arquivo de entrada e a subpasta que contém o arquivo são movidos para a pasta de preparo.
   1. Abra a pasta de saída para exibir a saída:
      * Quando você especifica a opção PRINT na Configuração de pasta monitorada, a saída do PDF para a comunicação interativa é gerada.
      * Quando você especifica a opção da WEB na Configuração da pasta monitorada, um arquivo JSON por registro é gerado. Você pode usar o arquivo JSON para [preencher previamente um modelo da Web](#web-template).
      * Quando você especifica as opções IMPRIMIR e WEB, ambos os documentos PDF e um arquivo JSON por registro são gerados.

#### Usar dados de entrada salvos em uma fonte externa de dados e acessados por meio do modelo de dados de formulário para produzir uma comunicação interativa {#use-fdm-as-data-source}

Você combina dados (registros) salvos em uma fonte de dados externa com um modelo de comunicação interativa para produzir uma comunicação interativa. Ao criar uma comunicação interativa, você a conecta a uma fonte de dados externa por meio de um Modelo de dados de formulário (FDM) para acessar os dados. Você pode configurar o serviço de processo em lote Pastas monitoradas para buscar dados usando o mesmo modelo de dados de formulário de uma fonte de dados externa. Para [criar uma comunicação interativa a partir de registros salvos em uma fonte de dados externa](/help/forms/using/work-with-form-data-model.md):

1. Configure o Modelo de dados de formulário do modelo:
   1. Abra o Modelo de dados de formulário associado ao modelo de comunicação interativa.
   1. Selecione o OBJETO DE MODELO DE NÍVEL SUPERIOR e selecione Editar propriedades.
   1. Selecione a busca ou obtenção do serviço no campo Serviço de leitura no painel Editar propriedades.
   1. Selecione o ícone de lápis para o argumento do serviço de leitura para vincular o argumento a um Atributo de solicitação e especifique o valor da vinculação. Ele vincula o argumento service ao atributo de vinculação especificado ou ao valor literal, que é transmitido ao serviço como um argumento para buscar detalhes associados ao valor especificado da fonte de dados.

      Neste exemplo, o argumento id pega o valor do atributo id do perfil do usuário e o passa como um argumento para o serviço de leitura. Ele lê e retorna valores de propriedades associadas do objeto de modelo de dados do funcionário para a id especificada. Portanto, se você especificar 00250 no campo id do formulário, o serviço de leitura lerá os detalhes do funcionário com a ID de funcionário 00250.

      ![Configurar atributo de solicitação](assets/request-attribute.png)

   1. Salve as propriedades e o Modelo de dados do formulário.
1. Configure o valor para o Atributo de solicitação:
   1. Crie um arquivo .json em seu sistema de arquivos e abra-o para edição.
   1. Crie uma matriz JSON e especifique o atributo primário para que você possa buscar dados do modelo de dados de formulário. Por exemplo, o JSON a seguir solicita que o FDM envie dados de registros nos quais a ID é 27126 ou 27127:

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

   1. Salvar e fechar o arquivo.

1. Crie uma [Pasta monitorada](/help/forms/using/creating-configure-watched-folder.md) e configure-a para usar o serviço de API em lote:
   1. Faça logon na instância de autor do AEM Forms.
   1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Forms]** > **[!UICONTROL Configurar a Pasta Monitorada]**. Selecione **[!UICONTROL Novo]**.
   1. Especifique o **[!UICONTROL Nome]** e o **[!UICONTROL Caminho]** físico da pasta. Por exemplo, `c:\batchprocessing`.
   1. Selecione a opção **[!UICONTROL Serviço]** no campo **[!UICONTROL Processar Arquivo Usando]**.
   1. Selecione o serviço **[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InterativeCommunicationBatchServiceImpl]** no campo **[!UICONTROL Nome do Serviço]**.
   1. Especifique um **[!UICONTROL Padrão de Arquivo de Saída]**. Por exemplo, o %F/ [padrão](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/administrator-help/configuring-watched-folder-endpoints.html?lang=pt-BR#about-file-patterns) especifica que a Pasta monitorada pode localizar arquivos de entrada em uma subpasta da pasta Pasta monitorada\entrada.
1. Configurar parâmetros avançados:
   1. Abra a guia **[!UICONTROL Avançado]** e adicione as seguintes propriedades personalizadas:

      | Propriedade | Tipo | Descrição |
      |--- |--- |--- |
      | templatePath | String | Especifique o caminho do modelo de comunicação interativa a ser usado. Por exemplo, /content/dam/formsanddocuments/testsample/mediumic. É uma propriedade obrigatória. |
      | recordPath | String | O valor do campo recordPath ajuda a definir o nome de uma comunicação interativa. É possível definir o caminho de um campo de um registro como o valor do campo recordPath. Por exemplo, se você especificar /employee/Id, o valor do campo id se torna nome para a comunicação interativa correspondente. O valor padrão é um [UUID aleatório](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |
      | usePrefillService | Booleano | Defina o valor como True. O valor padrão é false. Quando o valor é definido como true, a API de lote lê os dados do modelo de dados de formulário configurado e os preenche para a comunicação interativa. Quando usePrefillService é definido como true, os dados JSON de entrada (para cada registro) são tratados como Argumentos FDM. |
      | batchType | String | Defina o valor como PRINT, WEB ou WEB_AND_PRINT. O valor padrão é WEB_AND_PRINT. |
      | localidade | String | Especifique a localidade da comunicação interativa de saída. O serviço pronto para uso não usa a opção de local, mas você pode criar um serviço personalizado para gerar comunicações interativas localizadas. O valor padrão é en_US. |

   1. Selecione **[!UICONTROL Criar]**.
1. Usar a pasta monitorada criada para gerar comunicação interativa:
   1. Abra a Pasta monitorada. Navegue até a pasta de entrada.
   1. Crie uma pasta na pasta de entrada. Coloque o arquivo JSON criado na Etapa 2 na pasta recém-criada.
   1. Aguarde a Pasta monitorada processar o arquivo. Quando o processamento é iniciado, o arquivo de entrada e a subpasta que contém o arquivo são movidos para a pasta de preparo.
   1. Abra a pasta de saída para exibir a saída:
      * Quando você especifica a opção PRINT na Configuração de pasta monitorada, a saída do PDF para a comunicação interativa é gerada.
      * Quando você especifica a opção da WEB na Configuração da pasta monitorada, um arquivo JSON por registro é gerado. Você pode usar o arquivo JSON para [preencher previamente um modelo da Web](#web-template).
      * Quando você especifica as opções IMPRIMIR e WEB, ambos os documentos PDF e um arquivo JSON por registro são gerados.

## Chame a API de lote usando solicitações REST

Você pode invocar [a API de lote](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/index.html) por meio de solicitações de Transferência de Estado Representacional (REST). Ele permite que você forneça um terminal REST a outros usuários para acessar a API e configurar seus próprios métodos para processar, armazenar e personalizar a comunicação interativa. Você pode desenvolver seu próprio servlet Java™ personalizado para implantar a API em sua instância do AEM.

Antes de implantar o servlet Java™, certifique-se de que você tenha uma comunicação interativa e que os arquivos de dados correspondentes estejam prontos. Execute as seguintes etapas para criar e implantar o servlet Java™:

1. Faça logon na instância do AEM e crie uma Comunicação interativa. Para usar a comunicação interativa mencionada no código de exemplo fornecido abaixo, [clique aqui](assets/SimpleMediumIC.zip).
1. [Crie e implante um projeto do AEM usando o Apache Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/aem-project-archetype.html?lang=pt-BR) na sua instância do AEM.
1. Adicione o [AEM Forms Client SDK versão 6.0.12 ou posterior](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR) à lista de dependências do arquivo POM do seu projeto do AEM. Por exemplo,

   ```xml
       <dependency>
           <groupId>com.adobe.aemfd</groupId>
           <artifactId>aemfd-client-sdk</artifactId>
           <version>6.0.122</version>
       </dependency>
   ```

1. Abra o projeto Java™, crie um arquivo .java, por exemplo, CCMBatchServlet.java. Adicione o seguinte código ao arquivo:

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
   * Quando você especifica a opção PRINT do PDF, a saída para a comunicação interativa é gerada.
   * Quando você especifica a opção da WEB, um arquivo JSON por registro é gerado. Você pode usar o arquivo JSON para [preencher previamente um modelo da Web](#web-template).
   * Quando você especifica as opções IMPRIMIR e WEB, ambos os documentos PDF e um arquivo JSON por registro são gerados.

1. [Use o Maven para implantar o código atualizado em sua instância do AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/aem-project-archetype.html?lang=pt-BR).
1. Para gerar a comunicação interativa, chame a API em lote. A API de lote imprime um fluxo de arquivos PDF e .json dependendo do número de registros. Você pode usar o arquivo JSON para [preencher previamente um modelo da Web](#web-template). Se você usar o código acima, a API será implantada em `http://localhost:4502/bin/batchServlet`. O código imprime e retorna um fluxo de um PDF e um arquivo JSON.

### Preencher previamente um modelo da Web {#web-template}

Ao definir o batchType para renderizar o Canal da Web, a API gera um arquivo JSON para cada registro de dados. Você pode usar a seguinte sintaxe para mesclar o arquivo JSON ao canal da Web correspondente a fim de gerar uma comunicação interativa:

**Sintaxe**
`http://host:port/<template-path>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=<guide-merged-json-path>`

**Exemplo**
Se o arquivo JSON estiver em `C:\batch\mergedJsonPath.json` e você usar o modelo de comunicação interativa abaixo: `http://host:port/content/dam/formsanddocuments/testsample/mediumic/jcr:content?channel=web`

Em seguida, o URL a seguir no nó de publicação exibe o Canal da Web da comunicação interativa
`http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/batch/mergedJsonData.json`

Além de salvar os dados no sistema de arquivos, você armazena arquivos JSON no repositório do CRX, no sistema de arquivos, no servidor da Web ou pode acessar dados por meio do serviço de preenchimento prévio OSGI. A sintaxe para mesclar dados usando vários protocolos é:

* **Protocolo CRX**
  `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=crx:///tmp/fd/af/mergedJsonData.json`

* **Protocolo de arquivo**
  `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/Users/af/mergedJsonData.json`

* **Preencher o protocolo do serviço**
  `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=service://[SERVICE_NAME]/[IDENTIFIER]`

  SERVICE_NAME refere-se ao nome do serviço de preenchimento prévio OSGI. Consulte Criar e executar um serviço de preenchimento prévio.

  IDENTIFIER refere-se a quaisquer metadados necessários pelo serviço de preenchimento prévio OSGI para buscar os dados de preenchimento prévio. Um identificador para o usuário conectado é um exemplo de metadados que podem ser usados.

* **Protocolo HTTP**
  `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=http://localhost:8000/somesamplexmlfile.xml`

>[!NOTE]
>
>Somente o protocolo CRX é ativado por padrão. Para habilitar outros protocolos com suporte, consulte [Configurando o serviço de preenchimento prévio usando o Gerenciador de Configurações](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/prepopulate-adaptive-form-fields.html?lang=pt-BR).
