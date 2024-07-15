---
title: Preparar e enviar a comunicação interativa usando a interface do usuário do agente
description: A interface do usuário do agente permite que os agentes preparem e enviem a comunicação interativa para o processo posterior. O agente faz as modificações necessárias conforme permitido e envia a comunicação interativa para um processo posterior, como email ou impressão.
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Interactive Communication
exl-id: 4fb82e9b-f870-47db-ac92-2d7510acace8
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2010'
ht-degree: 0%

---

# Preparar e enviar a comunicação interativa usando a interface do usuário do agente {#prepare-and-send-interactive-communication-using-the-agent-ui}

A interface do usuário do agente permite que os agentes preparem e enviem a comunicação interativa para o processo posterior. O agente faz as modificações necessárias conforme permitido e envia a comunicação interativa para um processo posterior, como email ou impressão.

## Visão geral {#overview}

Depois que uma comunicação interativa é criada, o agente pode abrir a comunicação interativa na interface do agente e preparar uma cópia específica do destinatário inserindo dados e gerenciando conteúdo e anexos. Por fim, o agente pode enviar a comunicação interativa para um processo posterior.

Ao preparar a Comunicação interativa usando a interface do agente, o agente gerencia os seguintes aspectos da Comunicação interativa na interface do agente antes de enviá-la para um processo de publicação:

* **Dados**: a guia Dados da interface do usuário do Agente exibe quaisquer variáveis editáveis do agente e propriedades do modelo de dados de formulário desbloqueadas na Comunicação Interativa. Essas variáveis/propriedades são criadas ao editar ou criar fragmentos de documento incluídos na Comunicação interativa. A guia Data também inclui todos os campos criados no modelo de canal XDP/impressão. A guia Dados é exibida somente quando há variáveis, propriedades do modelo de dados de formulário ou campos na Comunicação interativa que podem ser editados pelo agente.
* **Conteúdo**: na guia Conteúdo, o Agente gerencia o conteúdo, como fragmentos de documentos e variáveis de conteúdo, na Comunicação Interativa. O agente pode fazer as alterações no fragmento do documento conforme permitido, ao criar a Comunicação interativa nas propriedades desses fragmentos de documento. O agente também pode reordenar, adicionar/remover um fragmento de documento e adicionar quebras de página, se permitido.
* **Anexos**: a guia Anexos será exibida na interface do usuário do Agente somente se a Comunicação Interativa tiver anexos ou se o Agente tiver acesso à biblioteca. O agente pode ou não ter permissão para alterar ou editar os anexos.

## Preparar a comunicação interativa usando a interface do usuário do agente {#prepare-interactive-communication-using-the-agent-ui}

1. Selecione **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione a comunicação interativa apropriada e selecione **[!UICONTROL Abrir interface do usuário do agente]**.

   >[!NOTE]
   >
   >A IU do agente funciona somente se a comunicação interativa selecionada tiver um canal de impressão.

   ![openagentiui](assets/openagentiui.png)

   Com base no conteúdo e nas propriedades da comunicação interativa, a interface do usuário do agente é exibida com as três guias a seguir: Dados, Conteúdo e Anexo.

   ![agentuitabs](assets/agentuitabs.png)

   Continue a inserir dados, gerenciar o conteúdo e gerenciar os anexos.

### Inserir dados {#enter-data}

1. Na guia Dados, insira os dados de variáveis, propriedades do modelo de dados de formulário e campos do modelo de impressão (XDP), conforme necessário. Preencha todos os campos obrigatórios marcados com um asterisco (&amp;ast;) para habilitar o botão **Enviar**.

   Selecione um valor de campo de dados na visualização de Comunicação interativa para realçar o campo de dados correspondente na guia Dados ou vice-versa.

### Gerenciar conteúdo {#manage-content}

Na guia Conteúdo, gerencie o conteúdo, como fragmentos de documento e variáveis de conteúdo na Comunicação interativa.

1. Selecione **[!UICONTROL Conteúdo]**. A guia de conteúdo da Comunicação interativa é exibida.

   ![agentuicontenttab](assets/agentuicontenttab.png)

1. Edite os fragmentos do documento, conforme necessário, na guia Conteúdo. Para focalizar o fragmento relevante na hierarquia de conteúdo, você pode selecionar a linha ou o parágrafo relevante na pré-visualização da Comunicação interativa ou selecionar o fragmento diretamente na hierarquia de conteúdo.

   Por exemplo, o fragmento do documento com a linha &quot;Faça um pagamento online agora ...&quot; é selecionado na pré-visualização no gráfico abaixo e o mesmo fragmento do documento foi selecionado na guia Conteúdo.

   ![contentmodulefocus](assets/contentmodulefocus.png)

   Na guia Conteúdo ou Dados, ao tocar em Realçar Módulos Selecionados no Conteúdo ( ![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png)) no canto superior esquerdo da visualização, você pode desabilitar ou habilitar a funcionalidade para ir para o fragmento do documento quando o texto, parágrafo ou campo de dados relevante for tocado/selecionado na visualização.

   Os fragmentos que podem ser editados pelo agente ao criar a Comunicação interativa têm o ícone Editar conteúdo selecionado ( ![iconeditselectedcontent](assets/iconeditselectedcontent.png)). Selecione o ícone Editar conteúdo selecionado para iniciar o fragmento no modo de edição e fazer alterações nele. Use as seguintes opções para formatar e gerenciar texto:

   * [Opções de formatação](#formattingtext)

      * [Copiar e colar texto formatado de outros aplicativos](#pasteformattedtext)
      * [Realçar partes do texto](#highlightemphasize)

   * [Caracteres especiais](#specialcharacters)
   * [Atalhos de teclado](/help/forms/using/keyboard-shortcuts.md)

   Para obter mais informações sobre as ações disponíveis para vários fragmentos de documento na interface do usuário do Agente, consulte [Ações e informações disponíveis na interface do usuário do Agente](#actionsagentui).

1. Para adicionar uma quebra de página à saída de impressão da Comunicação Interativa, coloque o cursor onde deseja inserir uma quebra de página e selecione Quebra de Página Antes ou Quebra de Página Depois ( ![pagebreakbeforeafter](assets/pagebreakbeforeafter.png)).

   Um espaço reservado para quebra de página explícita é inserido na Comunicação interativa. Para ver como uma quebra de página explícita afeta a Comunicação interativa, consulte a visualização de impressão.

   ![expltpagebreak](assets/explicitpagebreak.png)

   Continue gerenciando os anexos da Comunicação interativa.

### Gerenciar anexos {#manage-attachments}

1. Selecione **[!UICONTROL Anexo]**. A interface do usuário do agente exibe os anexos disponíveis conforme configurados ao criar a Comunicação interativa.

   Você pode optar por não enviar um anexo juntamente com a Comunicação interativa tocando no ícone de exibição e pode selecionar a cruz no anexo para excluí-lo (se o agente tiver permissão para excluir ou ocultar o anexo) da Comunicação interativa. Para os anexos especificados como obrigatórios ao criar a Comunicação interativa, os ícones Exibir e Excluir são desativados.

   ![attachmentsagentui](assets/attachmentsagentui.png)

1. Selecione o ícone de Acesso à biblioteca ( ![libraryaccess](assets/libraryaccess.png)) para acessar a Biblioteca de conteúdo e inserir ativos DAM como anexos.

   >[!NOTE]
   >
   >O ícone Acesso à biblioteca estará disponível somente se o acesso à biblioteca tiver sido habilitado durante a criação da Comunicação interativa (nas propriedades Contêiner de documentos do canal Imprimir).

1. Se a ordem dos anexos não tiver sido bloqueada durante a criação da Comunicação interativa, você poderá reordenar os anexos selecionando um anexo e tocando nas setas para baixo e para cima.
1. Use a Visualização da Web e a Visualização de impressão para ver se as duas saídas estão de acordo com sua necessidade.

   Se você achar as visualizações satisfatórias, selecione **[!UICONTROL Enviar]** para enviar/enviar a Comunicação interativa para um processo de publicação. Ou, para fazer alterações, saia da visualização para voltar para a criação de alterações.

## Formatação de texto {#formattingtext}

Ao editar um fragmento de texto na interface do agente, a barra de ferramentas muda dependendo do tipo de edições que você escolher fazer: Fonte, Parágrafo ou Lista:

![typeofformattingtoolbar](assets/typeofformattingtoolbar.png) ![Barra de ferramentas de fontes](do-not-localize/fonttoolbar.png)

Barra de ferramentas Fonte

![Barra de ferramentas de parágrafo](do-not-localize/paragraphtoolbar.png)

Barra de ferramentas Parágrafo

![Barra de ferramentas da lista](do-not-localize/listtoolbar.png)

Barra de ferramentas Lista

### Realçar/Enfatizar partes do texto {#highlightemphasize}

Para destacar\enfatizar partes do texto em um fragmento editável, selecione o texto e selecione Realçar cor.

![highlighttextagentui](assets/highlighttextagentui.png)

### Colar texto formatado {#pasteformattedtext}

![texto colado](assets/pastedtext.png)

### Inserir caracteres especiais no texto {#specialcharacters}

A interface do usuário do agente tem suporte integrado para 210 caracteres especiais. O administrador pode [adicionar suporte para mais caracteres especiais/personalizados através da personalização](/help/forms/using/custom-special-characters.md).

#### Entrega do anexo {#attachmentdelivery}

* Quando a Comunicação interativa é renderizada usando APIs do lado do servidor como um PDF interativo ou não interativo, o PDF renderizado contém anexos como anexos de PDF.
* Quando um processo de publicação associado a uma Comunicação interativa é carregado como parte do Enviar usando a interface do usuário do agente, os anexos são passados como o parâmetro List&lt;com.adobe.idp.Document> inAttachmentDocs.
* Os workflows do mecanismo de entrega, como email e impressão, também fornecem anexos junto com a versão PDF da Comunicação interativa.

## Ações e informações disponíveis na interface do usuário do agente {#actionsagentui}

### Fragmentos do documento {#document-fragments}

![ ](do-not-localize/contentoptionsdocfragments.png)

* **Setas para cima/para baixo**: setas para mover fragmentos de documento para cima ou para baixo na Comunicação Interativa.
* **Excluir**: se permitido, exclua o fragmento do documento da Comunicação Interativa.
* **Quebra de Página Antes de** (aplicável a fragmentos filho da área de destino): insere a quebra de página antes do fragmento do documento.
* **Recuo**: aumentar ou diminuir o recuo de um fragmento de documento.
* **Quebra de Página Após** (aplicável a fragmentos filho da área de destino): insere a quebra de página após o fragmento do documento.

![docfragoptions](assets/docfragoptions.png)

* Editar (somente fragmentos de texto): abra o editor de rich text para editar o fragmento do documento de texto. Para obter mais informações, consulte [Formatando texto](#formattingtext).

* Seleção (ícone de olho): Inclui\exclui fragmento de documento da Comunicação interativa.
* Valores não preenchidos (informações): indica o número de variáveis não preenchidas no fragmento do documento.

### Listar fragmentos de documento {#list-document-fragments}

![opções da lista](assets/listoptions.png)

* Inserir linha em branco: insere uma nova linha em branco.
* Seleção (ícone de olho): Inclui\exclui fragmento de documento da Comunicação interativa.
* Ignorar marcadores/numerações: ative se quiser ignorar marcadores/numeração no fragmento do documento de lista.
* Valores não preenchidos (informações): indica o número de variáveis não preenchidas no fragmento do documento.

## Salvar as comunicações interativas como rascunho {#save-as-draft}

Você pode usar a interface do usuário do agente para salvar um ou mais rascunhos para cada Comunicação interativa e recuperar o rascunho posteriormente para continuar trabalhando nela. Você pode especificar um nome diferente para cada rascunho para identificá-lo.

A Adobe recomenda executar essas instruções em sequência para salvar com êxito uma Comunicação interativa como rascunho.

### Ativar o recurso Salvar como rascunho {#before-save-as-draft}

Por padrão, o recurso Salvar como rascunho não está ativado. Execute as seguintes etapas para ativar o recurso:

1. Implemente a SPI (Interface do Provedor de Serviços) [ccrDocumentInstance](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/ccr/ccrDocumentInstance/api/services/CCRDocumentInstanceService.html).

   A SPI permite salvar a versão de rascunho da Comunicação interativa no banco de dados com uma ID de rascunho como o identificador exclusivo. Essas instruções pressupõem que você tenha conhecimento prévio sobre como criar um pacote OSGi usando um projeto Maven.

   Para obter exemplos de implementação SPI, consulte [Exemplo de implementação SPI ccrDocumentInstance](#sample-ccrDocumentInstance-spi).
1. Abra `http://<hostname>:<port>/ system/console/bundles` e selecione **[!UICONTROL Instalar/Atualizar]** para carregar o pacote OSGi. Verifique se o status do pacote carregado é exibido como **Ativo**. Reinicie o servidor se o status do pacote não for exibido como **Ativo**.
1. Acesse `https://'[server]:[port]'/system/console/configMgr`.
1. Selecione **[!UICONTROL Criar configuração de correspondência]**.
1. Selecione **[!UICONTROL Habilitar Salvar Usando CCRDocumentInstanceService]** e selecione **[!UICONTROL Salvar]**.

### Salvar uma comunicação interativa como rascunho {#save-as-draft-agent-ui}

Execute as seguintes etapas para salvar uma Comunicação interativa como rascunho:

1. Selecione uma comunicação interativa no Forms Manager e selecione **[!UICONTROL Abrir interface do usuário do agente]**.

1. Faça as alterações apropriadas na interface do usuário do Agente e selecione **[!UICONTROL Salvar como Rascunho]**.

1. Especifique o nome do Rascunho no campo **[!UICONTROL Nome]** e selecione **[!UICONTROL Concluído]**.

Depois de salvar a Comunicação interativa como rascunho, selecione **[!UICONTROL Salvar alterações]** para salvar as alterações adicionais feitas no rascunho.

### Recuperar o rascunho de uma comunicação interativa {#retrieve-draft}

Depois de salvar uma comunicação interativa como rascunho, você pode recuperá-la para continuar trabalhando nela. Recupere a comunicação interativa usando:

`https://server:port/aem/forms/createcorrespondence.hmtl?draftid=[draftid]`

[draftid] refere-se ao identificador exclusivo da versão de rascunho que é gerado após salvar uma Comunicação Interativa como rascunho.

### Exemplo de implementação de SPI ccrDocumentInstance {#sample-ccrDocumentInstance-spi}

Implemente a SPI `ccrDocumentInstance` para salvar uma Comunicação Interativa como rascunho. Este é um exemplo de implementação da SPI `ccrDocumentInstance`.

```javascript
package Implementation;

import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.exception.CCRDocumentException;
import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.model.CCRDocumentInstance;
import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.services.CCRDocumentInstanceService;
import org.apache.commons.lang3.StringUtils;
import org.osgi.service.component.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.*;


@Component(service = CCRDocumentInstanceService.class, immediate = true)
public class CCRDraftService implements CCRDocumentInstanceService {

    private static final Logger logger = LoggerFactory.getLogger(CCRDraftService.class);

    private HashMap<String, Object> draftDataMap = new HashMap<>();

    @Override
    public String save(CCRDocumentInstance ccrDocumentInstance) throws CCRDocumentException {
        String documentInstanceName = ccrDocumentInstance.getName();
        if (StringUtils.isNotEmpty(documentInstanceName)) {
            logger.info("Saving ccrData with name : {}", ccrDocumentInstance.getName());
            if (!CCRDocumentInstance.Status.SUBMIT.equals(ccrDocumentInstance.getStatus())) {
                ccrDocumentInstance = mySQLDataBaseServiceCRUD(ccrDocumentInstance,null, "SAVE");
            }
        } else {
            logger.error("Could not save data as draft name is empty");
        }
        return ccrDocumentInstance.getId();
    }

    @Override
    public void update(CCRDocumentInstance ccrDocumentInstance) throws CCRDocumentException {
        String documentInstanceName = ccrDocumentInstance.getName();
        if (StringUtils.isNotEmpty(documentInstanceName)) {
            logger.info("Saving ccrData with name : {}", documentInstanceName);
            mySQLDataBaseServiceCRUD(ccrDocumentInstance, ccrDocumentInstance.getId(), "UPDATE");
        } else {
            logger.error("Could not save data as draft Name is empty");
        }
    }

    @Override
    public CCRDocumentInstance get(String id) throws CCRDocumentException {
        CCRDocumentInstance cCRDocumentInstance;
        if (StringUtils.isEmpty(id)) {
            logger.error("Could not retrieve data as draftId is empty");
            cCRDocumentInstance = null;
        } else {
            cCRDocumentInstance = mySQLDataBaseServiceCRUD(null, id,"GET");
        }
        return cCRDocumentInstance;
    }

    @Override
    public List<CCRDocumentInstance> getAll(String userId, Date creationTime, Date updateTime,
                                            Map<String, Object> optionsParams) throws CCRDocumentException {
        List<CCRDocumentInstance> ccrDocumentInstancesList = new ArrayList<>();

        HashMap<String, Object> allSavedDraft = mySQLGetALLData();
        for (String key : allSavedDraft.keySet()) {
            ccrDocumentInstancesList.add((CCRDocumentInstance) allSavedDraft.get(key));
        }
        return ccrDocumentInstancesList;
    }

    //The APIs call the service in the database using the following section.
    private CCRDocumentInstance mySQLDataBaseServiceCRUD(CCRDocumentInstance ccrDocumentInstance,String draftId, String method){
        if(method.equals("SAVE")){

            String autoGenerateId = draftDataMap.size() + 1 +"";
            ccrDocumentInstance.setId(autoGenerateId);
            draftDataMap.put(autoGenerateId, ccrDocumentInstance);
            return ccrDocumentInstance;

        }else if (method.equals("UPDATE")){

            draftDataMap.put(ccrDocumentInstance.getId(), ccrDocumentInstance);
            return ccrDocumentInstance;

        }else if(method.equals("GET")){

            return (CCRDocumentInstance) draftDataMap.get(draftId);

        }
        return null;
    }

    private HashMap<String, Object> mySQLGetALLData(){
        return draftDataMap;
    }
}
```

As operações `save`, `update`, `get` e `getAll` chamam o serviço de banco de dados para salvar uma Comunicação Interativa como rascunho, atualizar uma Comunicação Interativa, recuperar dados do banco de dados e recuperar dados para todas as Comunicações Interativas disponíveis no banco de dados. Este exemplo usa `mySQLDataBaseServiceCRUD` como o nome do serviço de banco de dados.

A tabela a seguir explica a implementação da SPI `ccrDocumentInstance` de exemplo. Demonstra como as operações `save`, `update`, `get` e `getAll` chamam o serviço de banco de dados na implementação de amostra.

<table> 
 <tbody>
 <tr>
  <td><p><strong>Operação</strong></p></td>
  <td><p><strong>Exemplos de serviço de banco de dados</strong></p></td> 
   </tr>
  <tr>
   <td><p>Você pode criar um rascunho para uma Comunicação interativa ou enviá-lo diretamente. A API para a operação de salvamento verifica se a Comunicação interativa é enviada como um rascunho e inclui um nome de rascunho. A API chama o serviço mySQLDataBaseServiceCRUD com Salvar como o método de entrada.</p></br><img src="assets/save-as-draft-save-operation.png"/></td>
   <td><p>O serviço mySQLDataBaseServiceCRUD verifica Salvar como o método de entrada e gera uma ID de rascunho gerada automaticamente e a retorna ao AEM. A lógica para gerar uma ID de rascunho pode variar com base no banco de dados.</p></br><img src="assets/save-operation-service.png"/></td>
   </tr>
  <tr>
   <td><p>A API da operação de atualização recupera o status do rascunho da Comunicação interativa e verifica se a Comunicação interativa inclui um nome de rascunho. A API chama o serviço mySQLDataBaseServiceCRUD para atualizar esse status no Banco de Dados.</p></br><img src="assets/save-as-draft-update-operation.png"/></td>
   <td><p>O serviço mySQLDataBaseServiceCRUD verifica Update como o método de entrada e salva o status do rascunho de Comunicação Interativa no banco de dados.</br></p><img src="assets/update-operation-service.png"/></td>
   </tr>
   <tr>
   <td><p>A API para a operação get verifica se a Comunicação interativa inclui uma ID de rascunho. A API chama o serviço mySQLDataBaseServiceCRUD com Get como o método de entrada para recuperar os dados da comunicação interativa.</br></p><img src="assets/save-as-draft-get-operation.png"/></td>
   <td><p>O serviço mySQLDataBaseServiceCRUD verifica Get como o método de entrada e recupera os dados para a Comunicação Interativa com base na ID de rascunho.</p></br><img src="assets/get-operation-service.png"/></td>
   </tr>
   <tr>
   <td><p>A API da operação getAll chama o serviço mySQLGetALLData para recuperar dados de todas as Comunicações interativas salvas no banco de dados.</br></p><img src="assets/save-as-draft-getall-operation.png"/></td>
   <td><p>O serviço mySQLGetALLData recupera dados de todas as Comunicações Interativas salvas no banco de dados.</p></br><img src="assets/getall-operation-service.png"/></td>
   </tr>
  </tbody>
</table>

Este é um exemplo do arquivo `pom.xml` que faz parte da implementação:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0"
         xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.adobe.livecycle</groupId>
    <artifactId>draft-sample</artifactId>
    <version>2.0.0-SNAPSHOT</version>

    <name>Interact</name>
    <packaging>bundle</packaging>

    <dependencies>
        <dependency>
            <groupId>com.adobe.aemfd</groupId>
            <artifactId>aemfd-client-sdk</artifactId>
            <version>6.0.160</version>
        </dependency>
    </dependencies>


    <!-- ====================================================================== -->
    <!-- B U I L D D E F I N I T I O N -->
    <!-- ====================================================================== -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.felix</groupId>
                <artifactId>maven-bundle-plugin</artifactId>
                <version>3.3.0</version>
                <extensions>true</extensions>
                <executions>
                    <!--Configure extra execution of 'manifest' in process-classes phase to make sure SCR metadata is generated before unit test runs-->
                    <execution>
                        <id>scr-metadata</id>
                        <goals>
                            <goal>manifest</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <exportScr>true</exportScr>
                    <instructions>
                        <!-- Enable processing of OSGI DS component annotations -->
                        <_dsannotations>*</_dsannotations>
                        <!-- Enable processing of OSGI metatype annotations -->
                        <_metatypeannotations>*</_metatypeannotations>
                        <Bundle-SymbolicName>${project.groupId}-${project.artifactId}</Bundle-SymbolicName>
                    </instructions>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>8</source>
                    <target>8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
    <profiles>
        <profile>
            <id>autoInstall</id>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.apache.sling</groupId>
                        <artifactId>maven-sling-plugin</artifactId>
                        <executions>
                            <execution>
                                <id>install-bundle</id>
                                <phase>install</phase>
                                <goals>
                                    <goal>install</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
    </profiles>

</project>
```

>[!NOTE]
>
>Atualize a dependência `aemfd-client-sdk` para 6.0.160 no arquivo `pom.xml`.
