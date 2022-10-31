---
title: Amostra para integrar o componente de rascunhos e envios ao banco de dados
seo-title: Sample for integrating drafts & submissions component with database
description: Faça referência à implementação de dados e serviços de metadados personalizados para integrar rascunhos e componentes de envios a um banco de dados.
seo-description: Reference implementation of customized data and metadata services to integrate drafts and submissions component with a database.
uuid: ccdb900e-2c2e-4ed3-8a88-5c97aa0092a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: da96d3d8-a338-470a-8d20-55ea39bd15bf
exl-id: 2e4f8f51-df02-4bbb-99bb-30181facd1e0
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1467'
ht-degree: 1%

---

# Amostra para integrar o componente de rascunhos e envios ao banco de dados {#sample-for-integrating-drafts-submissions-component-with-database}

## Visão geral da amostra {#sample-overview}

O componente de rascunhos e envios do portal do AEM Forms permite que os usuários salvem seus formulários como rascunhos e enviem posteriormente de qualquer dispositivo. Além disso, os usuários podem exibir os formulários enviados no portal. Para habilitar essa funcionalidade, o AEM Forms fornece serviços de dados e metadados para armazenar os dados preenchidos por um usuário no formulário e os metadados associados aos rascunhos e formulários enviados. Esses dados são armazenados no repositório CRX, por padrão. No entanto, à medida que os usuários interagem com formulários por meio AEM instância de publicação, que geralmente está fora do firewall da empresa, as organizações podem querer personalizar o armazenamento de dados para que ele seja mais seguro e confiável.

A amostra, discutida neste documento, é uma implementação de referência de dados e serviços de metadados personalizados para integrar rascunhos e componentes de envios a um banco de dados. O banco de dados usado na implementação de amostra é **MySQL 5.6.24**. No entanto, é possível integrar o componente de rascunhos e envios a qualquer banco de dados de sua escolha.

>[!NOTE]
>
>* Os exemplos e as configurações explicadas neste documento são de acordo com o MySQL 5.6.24 e você deve substituí-los adequadamente no seu sistema de banco de dados.
>* Certifique-se de ter instalado a versão mais recente do pacote complementar do AEM Forms. Para obter a lista de pacotes disponíveis, consulte o [Versões do AEM Forms](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) artigo 10. o
>* O pacote de amostra funciona somente com ações de envio adaptáveis do Forms.


## Configurar e configurar a amostra {#set-up-and-configure-the-sample}

Execute as seguintes etapas, em todas as instâncias de autor e publicação, para instalar e configurar o exemplo :

1. Baixe o seguinte **aem-fp-db-integration-sample-pkg-6.1.2.zip** para seu sistema de arquivos.

   Pacote de exemplo para integração de banco de dados

[Obter arquivo](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. Vá para AEM gerenciador de pacotes em https://[*host*]:[*porta*]/crx/packmgr/.
1. Clique em **[!UICONTROL Fazer upload do pacote]**.

1. Navegue para selecionar o **aem-fp-db-integration-sample-pkg-6.1.2.zip** e clique em **[!UICONTROL OK]**.
1. Clique em **[!UICONTROL Instalar]** ao lado do pacote para instalar o pacote.
1. Ir para **[!UICONTROL Configuração do Console da Web AEM]**
página em https://[*host*]:[*porta*]/system/console/configMgr.
1. Clique para abrir **[!UICONTROL Configuração de rascunho e envio do portal do Forms]** no modo de edição.

1. Especifique os valores para as propriedades, conforme descrito na tabela a seguir:

   | **Propriedade** | **Descrição** | **Valor** |
   |---|---|---|
   | Serviço de dados de rascunho do Forms Portal | Identificador do serviço de dados de rascunho | formsportal.sampledataservice |
   | Serviço de Metadados de Rascunho do Forms Portal | Identificador do serviço de metadados de rascunho | formsportal.samplemetadataservice |
   | Serviço de dados de envio do Forms Portal | Identificador para envio do serviço de dados | formsportal.sampledataservice |
   | Serviço de Metadados de Envio do Portal Forms | Identificador para enviar serviço de metadados | formsportal.samplemetadataservice |
   | Serviço de Dados de Assinatura Pendente do Forms Portal | Identificador do serviço de dados de Assinatura pendente | formsportal.sampledataservice |
   | Serviço de Metadados de Assinatura Pendente do Forms Portal | Identificador do serviço de metadados de Assinatura pendente | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >Os serviços são resolvidos pelos nomes mencionados como valor da variável `aem.formsportal.impl.prop` Chave da seguinte maneira:

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   Você pode alterar nomes das tabelas de dados e metadados.

   Para fornecer um nome diferente para a tabela de metadados:

   * Na Configuração do Console da Web, localize e clique em Implementação de amostra do serviço de metadados do Forms Portal. Você pode alterar os valores da fonte de dados, dos metadados/do nome de tabela de metadados adicionais.

   Para fornecer um nome diferente para a tabela de dados:

   * Na Configuração do console da Web, localize e clique em Implementação de amostra do serviço de dados do Forms Portal. É possível alterar os valores da fonte de dados e do nome da tabela de dados.
   >[!NOTE]
   >
   >Se você alterar os nomes da tabela, forneça-os na configuração do Portal de formulários.

1. Deixe outras configurações como estão e clique em **[!UICONTROL Salvar]**.

1. A conexão de banco de dados pode ser feita por meio da fonte de dados agrupada da conexão Apache Sling.
1. Para conexão Apache Sling, localize e clique para abrir **[!UICONTROL Fonte de dados agrupada da conexão Apache Sling]** no modo de edição na Configuração do Console da Web. Especifique os valores para as propriedades, conforme descrito na tabela a seguir:

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Valor</strong></td>
  </tr>
  <tr>
   <td>Nome da fonte de dados</td>
   <td><p>Um nome de fonte de dados para filtrar drivers do pool de fonte de dados</p> <p><strong>Observação: </strong><em>A implementação de exemplo usa o FormsPortal como o nome da fonte de dados.</em></p> </td>
  </tr>
  <tr>
   <td>Classe de driver JDBC</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>URI de conexão JDBC<br /> </td>
   <td>jdbc:mysql://[<em>host</em>]:[<em>porta</em>]/[<em>nome_do_esquema</em>]</td>
  </tr>
  <tr>
   <td>Nome de usuário</td>
   <td>Um nome de usuário para autenticar e executar ações em tabelas de banco de dados</td>
  </tr>
  <tr>
   <td>Senha</td>
   <td>Senha associada ao nome de usuário</td>
  </tr>
  <tr>
   <td>Isolamento de transação</td>
   <td>READ_BUTED</td>
  </tr>
  <tr>
   <td>Máximo de conexões ativas</td>
   <td>1000</td>
  </tr>
  <tr>
   <td>Máximo de conexões inativas</td>
   <td>100</td>
  </tr>
  <tr>
   <td>Conexões Inativas Mínimas</td>
   <td>10</td>
  </tr>
  <tr>
   <td>Tamanho inicial</td>
   <td>10º</td>
  </tr>
  <tr>
   <td>Espera máx.</td>
   <td>100000</td>
  </tr>
  <tr>
   <td>Teste em linha de crédito</td>
   <td>Marcado</td>
  </tr>
  <tr>
   <td>Testar enquanto estiver inativo</td>
   <td>Marcado</td>
  </tr>
  <tr>
   <td>Consulta de validação</td>
   <td>Os valores de exemplo são SELECT 1(mysql), select 1 from dual(oracle), SELECT 1(MS Sql Server) (validationQuery)</td>
  </tr>
  <tr>
   <td>Tempo limite da consulta de validação</td>
   <td>10000</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* O driver JDBC para MySQL não é fornecido com a amostra. Certifique-se de ter provisionado para ele e forneça as informações necessárias para configurar o pool de conexão JDBC.
>* Aponte suas instâncias de autor e publicação para usar o mesmo banco de dados. O valor do campo URI de conexão JDBC deve ser o mesmo para todas as instâncias de autor e publicação.


1. Deixe outras configurações como estão e clique em **[!UICONTROL Salvar]**.

1. Se já tiver uma tabela no schema do banco de dados, pule para a próxima etapa.

   Caso contrário, se você ainda não tiver uma tabela no schema do banco de dados, execute as seguintes instruções SQL para criar tabelas separadas para dados, metadados e metadados adicionais no schema do banco de dados:

   >[!NOTE]
   >
   >Não é necessário bancos de dados diferentes para instâncias de autor e publicação. Use o mesmo banco de dados em todas as instâncias de autor e publicação.

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

   **instrução SQL para metadados adicionais**

   ```sql
   CREATE TABLE `additionalmetadatatable` (
   `value` text,
   `key` varchar(255) NOT NULL,
   `id` varchar(60) NOT NULL,
   PRIMARY KEY (`id`,`key`),
   CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
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

1. Se você já tiver as tabelas (dados, metadados e metadados adicionais) no schema do banco de dados, execute as seguintes queries de tabela futura:

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
   >A consulta de adição de metadados ALTER TABLE falhará se você já a tiver executado e a coluna markedforDeletion estiver presente na tabela.

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

   **Instrução SQL para alterar a tabela de metadados adicionais**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

A implementação de amostra agora está configurada, o que você pode usar para listar seus rascunhos e envios enquanto armazena todos os dados e metadados em um banco de dados. Agora vamos ver como os dados e os serviços de metadados são configurados na amostra.

## Instale o arquivo mysql-connector-java-5.1.39-bin.jar {#install-mysql-connector-java-bin-jar-file}

Execute as seguintes etapas, em todas as instâncias de autor e publicação, para instalar o arquivo mysql-connector-java-5.1.39-bin.jar:

1. Navegar para `https://'[server]:[port]'/system/console/depfinder` e procure pelo pacote com.mysql.jdbc .
1. Na coluna Exportado por , verifique se o pacote foi exportado por qualquer pacote.

   Continue se o pacote não for exportado por nenhum pacote.

1. Navegar para `https://'[server]:[port]'/system/console/bundles` e clique em **[!UICONTROL Instalar/atualizar]**.
1. Clique em **[!UICONTROL Escolher arquivo]** e navegue para selecionar o arquivo mysql-connector-java-5.1.39-bin.jar. Além disso, selecione **[!UICONTROL Iniciar Pacote]** e **[!UICONTROL Atualizar pacotes]** caixas de seleção.
1. Clique em **[!UICONTROL Instalar ou atualizar]**. Após a conclusão, reinicie o servidor.
1. (*Somente Windows*) Desligue o firewall do sistema para seu sistema operacional.

## Código de exemplo para dados do portal de formulários e serviço de metadados {#sample-code-for-forms-portal-data-and-metadata-service}

O zip a seguir contém `FormsPortalSampleDataServiceImpl` e `FormsPortalSampleMetadataServiceImpl` (classes de implementação) para interfaces de serviço de metadados e dados. Além disso, contém todas as classes necessárias para a compilação das classes de implementação mencionadas acima.

[Obter arquivo](assets/sample_package.zip)

## Verifique o comprimento do nome do arquivo  {#verify-length-of-the-file-name}

A implementação do banco de dados do Portal Forms usa tabela de metadados adicional. A tabela tem uma chave primária composta com base nas colunas Chave e ID da tabela. O MySQL permite chaves primárias até o comprimento de 255 caracteres. Você pode usar o seguinte script de validação do lado do cliente para verificar o comprimento do nome de arquivo anexado ao widget de arquivo. A validação é executada quando um arquivo é anexado. O script fornecido no procedimento a seguir exibe uma mensagem, quando o nome do arquivo for maior que 150 (incluindo extensão). Você pode modificar o script para verificá-lo para um número diferente de caracteres.

Execute as etapas a seguir para criar [uma biblioteca do cliente](/help/sites-developing/clientlibs.md) e usar o script:

1. Faça logon no CRXDE e navegue até /etc/clientlibs/
1. Criar um nó do tipo **cq:ClientLibraryFolder** e forneça o nome do nó. Por exemplo, `validation`.

   Clique em **[!UICONTROL Salvar tudo]**.

1. Clique com o botão direito do mouse no nó e clique em **[!UICONTROL criar novo arquivo]** e criar um arquivo com a extensão .txt. Por exemplo, `js.txt`Adicione o seguinte código ao arquivo .txt recém-criado e clique em **[!UICONTROL Salvar tudo]**.

   ```javascript
   #base=util
    util.js
   ```

   No código acima, `util` é o nome da pasta e `util.js` nome do arquivo no `util` pasta. O `util` pasta e `util.js` são criados em etapas subsequentes.

1. Clique com o botão direito do mouse no `cq:ClientLibraryFolder` nó criado na etapa 2, selecione Criar > Criar pasta. Crie uma pasta chamada `util`. Clique em **[!UICONTROL Salvar tudo]**. Clique com o botão direito do mouse no `util` selecione Criar > Criar arquivo. Crie um arquivo com o nome `util.js`. Clique em **[!UICONTROL Salvar tudo]**.

1. Adicione o seguinte código ao arquivo util.js e clique em **[!UICONTROL Salvar tudo]**. O comprimento da validação do código do nome do arquivo.

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
   >O script é para o componente de widget de anexo pronto para uso (OOTB). Se você personalizou o widget de anexo OOTB, altere o script acima para incorporar as respectivas alterações.

1. Adicione a seguinte propriedade à pasta criada na etapa 2 e clique em **[!UICONTROL Salvar tudo]**.

   * **[!UICONTROL Nome:]** categorias

   * **[!UICONTROL Tipo:]** String

   * **[!UICONTROL Valor:]** fp.validation

   * **[!UICONTROL várias opções:]** Ativado

1. Navegar para `/libs/fd/af/runtime/clientlibs/guideRuntime`e anexe o `fp.validation` à propriedade embed.

1. Navegue para /libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA e anexe a variável `fp.validation` propriedade embed.

   >[!NOTE]
   >
   >Se você estiver usando bibliotecas de clientes personalizadas em vez das bibliotecas de clientes guideRuntime e guideRuntimeWithXfa, use o nome da categoria para incorporar a biblioteca de clientes criada neste procedimento às bibliotecas personalizadas carregadas no tempo de execução.

1. Clique em **[!UICONTROL Salvar tudo.]** Agora, quando o nome do arquivo for maior que 150 caracteres (incluindo extensão), uma mensagem será exibida.
