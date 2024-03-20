---
title: Amostra para integrar o componente de rascunhos e envios ao banco de dados
description: Implementação de referência de dados personalizados e serviços de metadados para integrar o componente de rascunhos e envios a um banco de dados.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
exl-id: 2e4f8f51-df02-4bbb-99bb-30181facd1e0
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 1%

---

# Amostra para integrar o componente de rascunhos e envios ao banco de dados {#sample-for-integrating-drafts-submissions-component-with-database}

## Visão geral de exemplo {#sample-overview}

O componente de rascunhos e envios do portal do AEM Forms permite que os usuários salvem seus formulários como rascunhos e os enviem posteriormente de qualquer dispositivo. Além disso, os usuários podem exibir seus formulários enviados no portal. Para ativar essa funcionalidade, a AEM Forms fornece serviços de dados e metadados para armazenar os dados preenchidos por um usuário no formulário e os metadados do formulário associados aos rascunhos e formulários enviados. Esses dados são armazenados no repositório CRX, por padrão. No entanto, como os usuários interagem com formulários por meio da instância de publicação do AEM, que geralmente está fora do firewall corporativo, as organizações podem querer personalizar o armazenamento de dados para que seja mais seguro e confiável.

A amostra, discutida neste documento, é uma implementação de referência de dados personalizados e serviços de metadados para integrar rascunhos e componentes de envios a um banco de dados. O banco de dados usado na implementação de amostra é **MySQL 5.6.24**. No entanto, é possível integrar o componente de rascunhos e envios a qualquer banco de dados de sua escolha.

>[!NOTE]
>
>* Os exemplos e as configurações explicadas neste documento são de acordo com o MySQL 5.6.24 e você deve substituí-los apropriadamente pelo seu sistema de banco de dados.
>* Verifique se você instalou a versão mais recente do pacote complementar do AEM Forms. Para obter a lista de pacotes disponíveis, consulte [Versões do AEM Forms](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) artigo.
>* O pacote de amostra funciona somente com ações de envio do Adaptive Forms.

## Definir e configurar a amostra {#set-up-and-configure-the-sample}

Execute as seguintes etapas, em todas as instâncias de autor e publicação, para instalar e configurar a amostra:

1. Baixar o seguinte **aem-fp-db-integration-sample-pkg-6.1.2.zip** para o seu sistema de arquivos.

   Exemplo de pacote para integração de banco de dados

[Obter arquivo](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. Acesse o gerenciador de pacotes do AEM em https://[*host*]:[*porta*]/crx/packmgr/
1. Clique em **[!UICONTROL Fazer upload do pacote]**.

1. Navegue para selecionar o **aem-fp-db-integration-sample-pkg-6.1.2.zip** e clique em **[!UICONTROL OK]**.
1. Clique em **[!UICONTROL Instalar]** ao lado do pacote para instalar o pacote.
1. Ir para **[!UICONTROL Configuração do console da Web AEM]**
página em https://[*host*]:[*porta*]/system/console/configMgr
1. Clique para abrir **[!UICONTROL Configuração de rascunho e envio do Forms Portal]** no modo de edição.

1. Especifique os valores das propriedades conforme descrito na tabela a seguir:

   | **Propriedade** | **Descrição** | **Valor** |
   |---|---|---|
   | Serviço de Dados de Rascunho do Portal do Forms | Identificador do serviço de dados de rascunho | formsportal.sampledataservice |
   | Serviço de Metadados de Rascunho do Portal do Forms | Identificador do serviço de metadados de rascunho | formsportal.samplemetadataservice |
   | Serviço de Envio de Dados do Forms Portal | Identificador para enviar serviço de dados | formsportal.sampledataservice |
   | Serviço de metadados de envio do portal do Forms | Identificador para enviar serviço de metadados | formsportal.samplemetadataservice |
   | Serviço de Dados com Assinatura Pendente do Portal Forms | Identificador do serviço de dados com assinatura pendente | formsportal.sampledataservice |
   | Serviço de Metadados de Assinatura Pendente do Forms Portal | Identificador do serviço de metadados com assinatura pendente | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >Os serviços são resolvidos pelos nomes mencionados como valor para o `aem.formsportal.impl.prop` da seguinte forma:

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   É possível alterar os nomes das tabelas de dados e de metadados.

   Para fornecer um nome diferente para a tabela de metadados:

   * Na Configuração do console da Web, localize e clique em Implementação de amostra do serviço de metadados do portal do Forms. Você pode alterar os valores da fonte de dados, metadados/nome da tabela de metadados adicionais.

   Para fornecer um nome diferente para a tabela de dados:

   * Na Configuração do console da Web, localize e clique em Implementação de amostra do Forms Portal Data Service. Você pode alterar os valores da fonte de dados e o nome da tabela de dados.

   >[!NOTE]
   >
   >Se você alterar os nomes das tabelas, forneça-os na configuração do Portal de formulários.

1. Deixe as outras configurações como estão e clique em **[!UICONTROL Salvar]**.

1. A conexão do banco de dados pode ser feita por meio da fonte de dados agrupada da conexão Apache Sling.
1. Para conexão com o Apache Sling, localize e clique para abrir **[!UICONTROL Fonte de dados agrupada da conexão Apache Sling]** no modo de edição, na Configuração do console da Web. Especifique os valores das propriedades conforme descrito na tabela a seguir:

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Valor</strong></td>
  </tr>
  <tr>
   <td>Nome da fonte de dados</td>
   <td><p>Um nome de fonte de dados para filtrar drivers do pool de fonte de dados</p> <p><strong>Nota: </strong><em>A implementação de amostra usa FormsPortal como o nome da fonte de dados.</em></p> </td>
  </tr>
  <tr>
   <td>Classe de driver JDBC</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>URI da conexão JDBC<br /> </td>
   <td>jdbc:mysql://[<em>host</em>]:[<em>porta</em>]/[<em>schema_name</em>]</td>
  </tr>
  <tr>
   <td>Nome de usuário</td>
   <td>Um nome de usuário para autenticar e executar ações em tabelas do banco de dados</td>
  </tr>
  <tr>
   <td>Senha</td>
   <td>Senha associada ao nome de usuário</td>
  </tr>
  <tr>
   <td>Isolamento de transação</td>
   <td>READ_COMMITTED</td>
  </tr>
  <tr>
   <td>Máximo de conexões ativas</td>
   <td>1000</td>
  </tr>
  <tr>
   <td>Máximo de Conexões Ociosas</td>
   <td>100</td>
  </tr>
  <tr>
   <td>Mínimo de conexões ociosas</td>
   <td>10</td>
  </tr>
  <tr>
   <td>Tamanho inicial</td>
   <td>10</td>
  </tr>
  <tr>
   <td>Espera Máxima</td>
   <td>100000</td>
  </tr>
  <tr>
   <td>Teste ao tomar emprestado</td>
   <td>Marcado</td>
  </tr>
  <tr>
   <td>Teste enquanto ocioso</td>
   <td>Marcado</td>
  </tr>
  <tr>
   <td>Consulta de validação</td>
   <td>Os valores de exemplo são SELECT 1(mysql), select 1 from dual(oracle), SELECT 1(MS Sql Server) (validationQuery)</td>
  </tr>
  <tr>
   <td>Tempo limite de consulta de validação</td>
   <td>10000</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* O driver JDBC para MySQL não é fornecido com a amostra. Certifique-se de que você o provisionou e forneça as informações necessárias para configurar o pool de conexões JDBC.
>* Aponte suas instâncias de autor e publicação para usar o mesmo banco de dados. O valor do campo URI da conexão JDBC deve ser o mesmo para todas as instâncias do autor e de publicação.

1. Deixe as outras configurações como estão e clique em **[!UICONTROL Salvar]**.

1. Se você já tiver uma tabela no esquema do banco de dados, pule para a próxima etapa.

   Caso contrário, se você ainda não tiver uma tabela no esquema do banco de dados, execute as seguintes instruções SQL para criar tabelas separadas para dados, metadados e metadados adicionais no esquema do banco de dados:

   >[!NOTE]
   >
   >Você não precisa de bancos de dados diferentes para as instâncias de criação e publicação. Use o mesmo banco de dados em todas as instâncias de autor e publicação.

   **Instrução SQL para tabela de dados**

   ```sql
   CREATE TABLE `data` (
   `owner` varchar(255) DEFAULT NULL,
   `data` longblob,
   `metadataId` varchar(45) DEFAULT NULL,
   `id` varchar(45) NOT NULL,
   PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **Instrução SQL para tabela de metadados**

   ```sql
   CREATE TABLE `metadata` (
   `formPath` varchar(1000) DEFAULT NULL,
   `formType` varchar(100) DEFAULT NULL,
   `description` text,
   `formName` varchar(255) DEFAULT NULL,
   `owner` varchar(255) DEFAULT NULL,
   `enableAnonymousSave` varchar(45) DEFAULT NULL,
   `renderPath` varchar(1000) DEFAULT NULL,
   `nodeType` varchar(45) DEFAULT NULL,
   `charset` varchar(45) DEFAULT NULL,
   `userdataID` varchar(45) DEFAULT NULL,
   `status` varchar(45) DEFAULT NULL,
   `formmodel` varchar(45) DEFAULT NULL,
   `markedForDeletion` varchar(45) DEFAULT NULL,
   `showDorClass` varchar(255) DEFAULT NULL,
   `sling:resourceType` varchar(1000) DEFAULT NULL,
   `attachmentList` longtext,
   `draftID` varchar(45) DEFAULT NULL,
   `submitID` varchar(45) DEFAULT NULL,
   `id` varchar(60) NOT NULL,
   `profile` varchar(255) DEFAULT NULL,
   `submitUrl` varchar(1000) DEFAULT NULL,
   `xdpRef` varchar(1000) DEFAULT NULL,
   `agreementId` varchar(255) DEFAULT NULL,
   `nextSigners` varchar(255) DEFAULT NULL,
   `eSignStatus` varchar(45) DEFAULT NULL,
   `pendingSignID` varchar(45) DEFAULT NULL,
   `agreementDataId` varchar(255) DEFAULT NULL,
   `enablePortalSubmit` varchar(45) DEFAULT NULL,
   `submitType` varchar(45) DEFAULT NULL,
   `dataType` varchar(45) DEFAULT NULL,
   `jcr:lastModified` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`id`),
   UNIQUE KEY `ID_UNIQUE` (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **Instrução SQL para metadatatable adicional**

   ```sql
   CREATE TABLE `additionalmetadatatable` (
   `value` text,
   `key` varchar(255) NOT NULL,
   `id` varchar(60) NOT NULL,
   PRIMARY KEY (`id`,`key`),
   CONSTRAINT 'additionalmetadatatable_fk' FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **Instrução SQL para tabela de comentários**

   ```sql
   CREATE TABLE `commenttable` (
   `commentId` varchar(255) DEFAULT NULL,
   `comment` text DEFAULT NULL,
   `ID` varchar(255) DEFAULT NULL,
   `commentowner` varchar(255) DEFAULT NULL,
   `time` varchar(255) DEFAULT NULL);
   ```

1. Se você já tiver as tabelas (dados, metadados e metadatáveis adicionais) no esquema de banco de dados, execute as seguintes consultas de tabela de alteração:

   **Instrução SQL para alterar a tabela de dados**

   ```sql
   ALTER TABLE `data` CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **Instrução SQL para alterar a tabela de metadados**

   ```sql
   ALTER TABLE metadata add markedForDeletion varchar(45) DEFAULT NULL
   ```

   >[!NOTE]
   >
   >A consulta de adição de metadados ALTER TABLE falhará se você já a tiver executado e se a coluna markedforDeletion estiver presente na tabela.

   ```sql
   ALTER TABLE metadata add agreementId varchar(255) DEFAULT NULL,
   add nextSigners varchar(255) DEFAULT NULL,
   add eSignStatus varchar(45) DEFAULT NULL,
   add pendingSignID varchar(45) DEFAULT NULL,
   add agreementDataId varchar(255) DEFAULT NULL,
   add enablePortalSubmit varchar(45) DEFAULT NULL,
   add submitType varchar(45) DEFAULT NULL,
   add dataType varchar(45) DEFAULT NULL;
   ```

   ```sql
   ALTER TABLE `metadata` CHANGE `formPath` `formPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formType` `formType` VARCHAR(100) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `description` `description` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formName` `formName` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `renderPath` `renderPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `showDorClass` `showDorClass` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `sling:resourceType` `sling:resourceType` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `profile` `profile` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `submitUrl` `submitUrl` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `xdpRef` `xdpRef` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **Instrução SQL para alterar a tabela de metadados adicional**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

A implementação de amostra agora está configurada, que você pode usar para listar seus rascunhos e envios enquanto armazena todos os dados e metadados em um banco de dados. Agora vamos ver como os serviços de dados e metadados são configurados na amostra.

## Instale o arquivo mysql-connector-java-5.1.39-bin.jar {#install-mysql-connector-java-bin-jar-file}

Execute as seguintes etapas, em todas as instâncias de autor e publicação, para instalar o arquivo mysql-connector-java-5.1.39-bin.jar:

1. Navegue até `https://'[server]:[port]'/system/console/depfinder` e procure pelo pacote com.mysql.jdbc.
1. Na coluna Exportado por, verifique se o pacote foi exportado por algum pacote.

   Continue se o pacote não for exportado por um pacote.

1. Navegue até `https://'[server]:[port]'/system/console/bundles` e clique em **[!UICONTROL Instalar/Atualizar]**.
1. Clique em **[!UICONTROL Escolher arquivo]** e navegue para selecionar o arquivo mysql-connector-java-5.1.39-bin.jar. Além disso, **[!UICONTROL Iniciar pacote]** e **[!UICONTROL Atualizar pacotes]** caixas de seleção.
1. Clique em **[!UICONTROL Instalar ou atualizar]**. Após a conclusão, reinicie o servidor.
1. (*Somente Windows*) Desative o firewall do sistema para o seu sistema operacional.

>[!NOTE]
>
> É recomendável usar o comando &quot;Ctrl + C&quot; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

## Exemplo de código para o serviço de dados e metadados do portal de formulários {#sample-code-for-forms-portal-data-and-metadata-service}

O zip a seguir contém `FormsPortalSampleDataServiceImpl` e `FormsPortalSampleMetadataServiceImpl` (classes de implementação) para interfaces de serviço de dados e metadados. Além disso, contém todas as classes necessárias para a compilação das classes de implementação mencionadas acima.

[Obter arquivo](assets/sample_package.zip)

## Verificar comprimento do nome do arquivo  {#verify-length-of-the-file-name}

A implementação do banco de dados do Forms Portal usa uma tabela de metadados adicional. A tabela tem uma chave primária composta com base nas colunas Chave e id da tabela. O MySQL permite chaves primárias com até 255 caracteres. Você pode usar o script de validação do lado do cliente a seguir para verificar o comprimento do nome de arquivo anexado ao dispositivo de arquivo. A validação é executada quando um arquivo é anexado. O script fornecido no procedimento a seguir exibe uma mensagem quando o nome do arquivo é maior que 150 (incluindo a extensão). Você pode modificar o script para verificá-lo quanto a um número diferente de caracteres.

Execute as seguintes etapas para criar [uma biblioteca do cliente](/help/sites-developing/clientlibs.md) e use o script:

1. Faça logon no CRXDE e navegue até /etc/clientlibs/
1. Criar um nó do tipo **cq:ClientLibraryFolder** e forneça o nome do nó. Por exemplo, `validation`.

   Clique em **[!UICONTROL Salvar tudo]**.

1. Clique com o botão direito do mouse no nó e clique em **[!UICONTROL criar novo arquivo]**, e crie um arquivo com a extensão .txt. Por exemplo, `js.txt`Adicione o seguinte código ao arquivo .txt recém-criado e clique em **[!UICONTROL Salvar tudo]**.

   ```javascript
   #base=util
    util.js
   ```

   No código acima, `util` é o nome da pasta e `util.js` nome do arquivo na variável `util` pasta. A variável `util` pasta e `util.js` O arquivo será criado nas etapas seguintes.

1. Clique com o botão direito do mouse no `cq:ClientLibraryFolder` criado na etapa 2, selecione Criar > Criar pasta. Crie uma pasta chamada `util`. Clique em **[!UICONTROL Salvar tudo]**. Clique com o botão direito do mouse no `util` selecione Criar > Criar arquivo. Crie um arquivo chamado `util.js`. Clique em **[!UICONTROL Salvar tudo]**.

1. Adicione o seguinte código ao arquivo util.js e clique em **[!UICONTROL Salvar tudo]**. O comprimento de validação do código do nome do arquivo.

   ```javascript
   /*
    * ADOBE CONFIDENTIAL
    * ___________________
    *
    * Copyright 2016 Adobe Systems Incorporated
    * All Rights Reserved.
    *
    * NOTICE:  All information contained herein is, and remains
    * the property of Adobe Systems Incorporated and its suppliers,
    * if any.  The intellectual and technical concepts contained
    * herein are proprietary to Adobe Systems Incorporated and its
    * suppliers and may be covered by U.S. and Foreign Patents,
    * patents in process, and are protected by trade secret or copyright law.
    * Dissemination of this information or reproduction of this material
    * is strictly forbidden unless prior written permission is obtained
    * from Adobe Systems Incorporated.
    *
    */
   (function () {
       var connectWithGuideBridge = function (gb) {
           gb.connect(function () {
               //For first time load
               window.guideBridge.on("elementValueChanged" , function(event, payload) {
           var component = payload.target; // Field whose value has changed
                   if(component.name == 'fileAttachment' && component.parent) {
                       var fileItems = $('#'+payload.target.parent.id).find(".guide-fu-fileItem");
                       for (i = 0;i<fileItems.length;i++) {
                           var filename = $(fileItems[i]).find(".guide-fu-fileName").text();
                           //check whether it is previously attached file or a newly  attached one
                           if(filename.length > 150 && filename.indexOf("fp.attach.jsp") < 0) {
                               window.alert("filename is larger than 150 : "+filename);
                                $(fileItems[i]).find(".guide-fu-fileClose.close").click();
                           }
                       }
                   }
   
      });
           });
       };
   
       if (window.guideBridge) {
           connectWithGuideBridge(window.guideBridge);
       } else {
           window.addEventListener("bridgeInitializeStart", function (event) {
               connectWithGuideBridge(event.detail.guideBridge);
           });
       }
   })();
   ```

   >[!NOTE]
   >
   >O script é para o componente de widget de anexo pronto para uso. Se você personalizou o widget de anexo pronto para uso, altere o script acima para incorporar as respectivas alterações.

1. Adicione a seguinte propriedade à pasta criada na etapa 2 e clique em **[!UICONTROL Salvar tudo]**.

   * **[!UICONTROL Nome:]** categorias

   * **[!UICONTROL Tipo:]** String

   * **[!UICONTROL Valor:]** fp.validation

   * **[!UICONTROL multiopção:]** Ativado

1. Navegue até `/libs/fd/af/runtime/clientlibs/guideRuntime`e anexe a variável `fp.validation` para a propriedade embed.

1. Navegue até /libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA e anexe o `fp.validation` valor para incorporar a propriedade.

   >[!NOTE]
   >
   >Se você estiver usando bibliotecas de clientes personalizadas em vez das bibliotecas de clientes guideRuntime e guideRuntimeWithXfa, use o nome da categoria para incorporar a biblioteca de clientes criada neste procedimento às bibliotecas personalizadas carregadas no tempo de execução.

1. Clique em **[!UICONTROL Salvar tudo.]** Agora, quando o nome do arquivo tiver mais de 150 caracteres (incluindo a extensão), uma mensagem será exibida.
