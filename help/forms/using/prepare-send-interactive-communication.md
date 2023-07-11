---
title: Preparar e enviar a comunicação interativa usando a interface do usuário do agente
seo-title: Prepare and send Interactive Communication using the Agent UI
description: A interface do usuário do agente permite que os agentes preparem e enviem a comunicação interativa para o processo posterior. O agente faz as modificações necessárias conforme permitido e envia a comunicação interativa para um processo posterior, como email ou impressão.
seo-description: Prepare and send Interactive Communication using the Agent UI
uuid: d1a19b83-f630-4648-9ad2-a22374e31aa9
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 110c86ea-9bd8-4018-bfcc-ca33e6b3f3ba
feature: Interactive Communication
exl-id: 4fb82e9b-f870-47db-ac92-2d7510acace8
source-git-commit: e9f64722ba7df0a7f43aaf1005161483e04142f5
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 0%

---

# Preparar e enviar a comunicação interativa usando a interface do usuário do agente {#prepare-and-send-interactive-communication-using-the-agent-ui}

A interface do usuário do agente permite que os agentes preparem e enviem a comunicação interativa para o processo posterior. O agente faz as modificações necessárias conforme permitido e envia a comunicação interativa para um processo posterior, como email ou impressão.

## Visão geral {#overview}

Depois que uma comunicação interativa é criada, o agente pode abrir a comunicação interativa na interface do agente e preparar uma cópia específica do destinatário inserindo dados e gerenciando conteúdo e anexos. Por fim, o agente pode enviar a comunicação interativa para um processo posterior.

Ao preparar a Comunicação interativa usando a interface do agente, o agente gerencia os seguintes aspectos da Comunicação interativa na interface do agente antes de enviá-la para um processo de publicação:

* **Dados**: a guia Dados da interface do usuário do agente exibe quaisquer variáveis editáveis do agente e propriedades do modelo de dados de formulário desbloqueadas na Comunicação interativa. Essas variáveis/propriedades são criadas ao editar ou criar fragmentos de documento incluídos na Comunicação interativa. A guia Data também inclui todos os campos criados no modelo de canal XDP/impressão. A guia Dados é exibida somente quando há variáveis, propriedades do modelo de dados de formulário ou campos na Comunicação interativa que podem ser editados pelo agente.
* **Conteúdo**: na guia Conteúdo, o Agente gerencia o conteúdo, como fragmentos de documentos e variáveis de conteúdo, na Comunicação interativa. O agente pode fazer as alterações no fragmento do documento conforme permitido, ao criar a Comunicação interativa nas propriedades desses fragmentos de documento. O agente também pode reordenar, adicionar/remover um fragmento de documento e adicionar quebras de página, se permitido.
* **Anexos**: a guia Anexos será exibida na interface do usuário do Agente somente se a Comunicação Interativa tiver anexos ou se o Agente tiver acesso à biblioteca. O agente pode ou não ter permissão para alterar ou editar os anexos.

## Preparar a comunicação interativa usando a interface do usuário do agente {#prepare-interactive-communication-using-the-agent-ui}

1. Selecionar **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos]**.
1. Selecione a comunicação interativa apropriada e toque em **[!UICONTROL Abrir IU do agente]**.

   >[!NOTE]
   >
   >A IU do agente funciona somente se a comunicação interativa selecionada tiver um canal de impressão.

   ![openagentiui](assets/openagentiui.png)

   Com base no conteúdo e nas propriedades da comunicação interativa, a interface do usuário do agente é exibida com as três guias a seguir: Dados, Conteúdo e Anexo.

   ![agentuitabs](assets/agentuitabs.png)

   Continue a inserir dados, gerenciar o conteúdo e gerenciar os anexos.

### Inserir dados {#enter-data}

1. Na guia Dados, insira os dados de variáveis, propriedades do modelo de dados de formulário e campos do modelo de impressão (XDP), conforme necessário. Preencha todos os campos obrigatórios marcados com um asterisco (&amp;ast;) para habilitar o **Enviar** botão.

   Toque em um valor de campo de dados na visualização de Comunicação interativa para realçar o campo de dados correspondente na guia Dados ou vice-versa.

### Gerenciar conteúdo {#manage-content}

Na guia Conteúdo, gerencie o conteúdo, como fragmentos de documento e variáveis de conteúdo na Comunicação interativa.

1. Selecionar **[!UICONTROL Conteúdo]**. A guia de conteúdo da Comunicação interativa é exibida.

   ![agentuicontenttab](assets/agentuicontenttab.png)

1. Edite os fragmentos do documento, conforme necessário, na guia Conteúdo. Para focalizar o fragmento relevante na hierarquia de conteúdo, você pode tocar na linha ou no parágrafo relevante na pré-visualização da Comunicação interativa ou tocar no fragmento diretamente na hierarquia de conteúdo.

   Por exemplo, o fragmento do documento com a linha &quot;Faça um pagamento online agora ...&quot; é selecionado na pré-visualização no gráfico abaixo e o mesmo fragmento do documento foi selecionado na guia Conteúdo.

   ![contentmodulefocus](assets/contentmodulefocus.png)

   Na guia Conteúdo ou Dados, tocando em Realçar módulos selecionados no conteúdo ( ![highlightselectedmodulesincontentcr](assets/highlightselectedmodulesincontentccr.png)) na parte superior esquerda da visualização, você pode desativar ou ativar a funcionalidade para acessar o fragmento do documento quando o texto, parágrafo ou campo de dados relevante for tocado/selecionado na visualização.

   Os fragmentos que têm permissão para serem editados pelo agente ao criar a Comunicação interativa têm a opção Editar conteúdo selecionado ( ![iconeditselectedcontent](assets/iconeditselectedcontent.png)) ícone. Toque no ícone Editar conteúdo selecionado para iniciar o fragmento no modo de edição e fazer alterações nele. Use as seguintes opções para formatar e gerenciar texto:

   * [Opções de formatação](#formattingtext)

      * [Copiar e colar texto formatado de outros aplicativos](#pasteformattedtext)
      * [Realçar partes do texto](#highlightemphasize)

   * [Caracteres especiais](#specialcharacters)
   * [Atalhos de teclado](/help/forms/using/keyboard-shortcuts.md)

   Para obter mais informações sobre as ações disponíveis para vários fragmentos de documento na interface do usuário do Agente, consulte [Ações e informações disponíveis na interface do usuário do agente](#actionsagentui).

1. Para adicionar uma quebra de página à saída de impressão da Comunicação interativa, coloque o cursor onde deseja inserir uma quebra de página e selecione Quebra de página antes ou Quebra de página depois ( ![pagebreakbefore after](assets/pagebreakbeforeafter.png)).

   Um espaço reservado para quebra de página explícita é inserido na Comunicação interativa. Para ver como uma quebra de página explícita afeta a Comunicação interativa, consulte a visualização de impressão.

   ![expltpagebreak](assets/explicitpagebreak.png)

   Continue gerenciando os anexos da Comunicação interativa.

### Gerenciar anexos {#manage-attachments}

1. Selecionar **[!UICONTROL Anexo]**. A interface do usuário do agente exibe os anexos disponíveis conforme configurados ao criar a Comunicação interativa.

   Você pode optar por não enviar um anexo juntamente com a Comunicação interativa tocando no ícone de exibição e tocar na cruz no anexo para excluí-lo (se o agente tiver permissão para excluir ou ocultar o anexo) da Comunicação interativa. Para os anexos especificados como obrigatórios ao criar a Comunicação interativa, os ícones Exibir e Excluir são desativados.

   ![attachmentsagentui](assets/attachmentsagentui.png)

1. Toque em Acesso à biblioteca ( ![libraryaccess](assets/libraryaccess.png)) para acessar a Biblioteca de conteúdo e inserir ativos DAM como anexos.

   >[!NOTE]
   >
   >O ícone Acesso à biblioteca estará disponível somente se o acesso à biblioteca tiver sido habilitado durante a criação da Comunicação interativa (nas propriedades Contêiner de documentos do canal Imprimir).

1. Se a ordem dos anexos não tiver sido bloqueada durante a criação da Comunicação interativa, você poderá reordenar os anexos selecionando um anexo e tocando nas setas para baixo e para cima.
1. Use a Visualização da Web e a Visualização de impressão para ver se as duas saídas estão de acordo com sua necessidade.

   Se você achar as visualizações satisfatórias, toque em **[!UICONTROL Enviar]** para enviar a Comunicação interativa a um processo de publicação. Ou, para fazer alterações, saia da visualização para voltar para a criação de alterações.

## Formatação de texto {#formattingtext}

Ao editar um fragmento de texto na interface do agente, a barra de ferramentas muda dependendo do tipo de edições que você escolher fazer: Fonte, Parágrafo ou Lista:

![typeofformattingtoolbar](assets/typeofformattingtoolbar.png) ![Barra de ferramentas Fonte](do-not-localize/fonttoolbar.png)

Barra de ferramentas Fonte

![Barra de ferramentas Parágrafo](do-not-localize/paragraphtoolbar.png)

Barra de ferramentas Parágrafo

![Barra de ferramentas Lista](do-not-localize/listtoolbar.png)

Barra de ferramentas Lista

### Realçar/Enfatizar partes do texto {#highlightemphasize}

Para destacar\enfatizar partes do texto em um fragmento editável, selecione o texto e toque em Realçar cor.

![highlighttextagentui](assets/highlighttextagentui.png)

### Colar texto formatado {#pasteformattedtext}

![pastedtext](assets/pastedtext.png)

### Inserir caracteres especiais no texto {#specialcharacters}

A interface do usuário do agente tem suporte integrado para 210 caracteres especiais. O administrador pode [adicionar suporte para mais caracteres especiais/personalizados por personalização](/help/forms/using/custom-special-characters.md).

#### Entrega do anexo {#attachmentdelivery}

* Quando a Comunicação interativa é renderizada usando APIs do lado do servidor como um PDF interativo ou não interativo, o PDF renderizado contém anexos como anexos de PDF.
* Quando um processo de publicação associado a uma Comunicação interativa é carregado como parte do Enviar usando a interface do usuário do agente, os anexos são passados como a Lista&lt;com.adobe.idp.document> parâmetro inAttachmentDocs.
* Os workflows do mecanismo de entrega, como email e impressão, também fornecem anexos junto com a versão PDF da Comunicação interativa.

## Ações e informações disponíveis na interface do usuário do agente {#actionsagentui}

### Fragmentos do documento {#document-fragments}

![document-fragments-ui-operations](do-not-localize/contentoptionsdocfragments.png)

* **Setas para cima/para baixo**: setas para mover fragmentos de documento para cima ou para baixo na Comunicação interativa.
* **Excluir**: Se permitido, exclua o fragmento do documento da Comunicação interativa.
* **Quebra de página antes** (aplicável para fragmentos secundários da área de destino): insere a quebra de página antes do fragmento do documento.
* **Recuar**: Aumenta ou diminui o recuo de um fragmento de documento.
* **Quebra de página após** (aplicável para fragmentos secundários da área de destino): insere a quebra de página após o fragmento do documento.

![docfragoptions](assets/docfragoptions.png)

* Editar (somente fragmentos de texto): abra o editor de rich text para editar o fragmento do documento de texto. Para obter mais informações, consulte [Formatação de texto](#formattingtext).

* Seleção (ícone de olho): Inclui\exclui fragmento de documento da Comunicação interativa.
* Valores não preenchidos (informações): indica o número de variáveis não preenchidas no fragmento do documento.

### Listar fragmentos de documento {#list-document-fragments}

![listoptions](assets/listoptions.png)

* Inserir linha em branco: insere uma nova linha em branco.
* Seleção (ícone de olho): Inclui\exclui fragmento de documento da Comunicação interativa.
* Ignorar marcadores/numerações: permite ignorar marcadores/numeração no fragmento do documento de lista.
* Valores não preenchidos (informações): indica o número de variáveis não preenchidas no fragmento do documento.

## Salvar as comunicações interativas como rascunho {#save-as-draft}

Você pode usar a interface do usuário do agente para salvar um ou mais rascunhos para cada Comunicação interativa e recuperar o rascunho posteriormente para continuar trabalhando nela. Você pode especificar um nome diferente para cada rascunho para identificá-lo.

A Adobe recomenda executar essas instruções em sequência para salvar com êxito uma Comunicação interativa como rascunho.

### Ativar o recurso Salvar como rascunho {#before-save-as-draft}

Por padrão, o recurso Salvar como rascunho não está ativado. Execute as seguintes etapas para ativar o recurso:

1. Implementar o [ccrDocumentInstance](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/ccr/ccrDocumentInstance/api/services/CCRDocumentInstanceService.html) SPI (Interface do provedor de serviços).

   A SPI permite salvar a versão de rascunho da Comunicação interativa no banco de dados com uma ID de rascunho como o identificador exclusivo. Essas instruções pressupõem que você tenha conhecimento prévio sobre como criar um pacote OSGi usando um projeto Maven.

   Para obter exemplos de implementação de SPI, consulte [Exemplo de implementação de SPI ccrDocumentInstance](#sample-ccrDocumentInstance-spi).
1. Abertura `http://<hostname>:<port>/ system/console/bundles` e toque em **[!UICONTROL Instalar/Atualizar]** para fazer upload do pacote OSGi. Verifique se o status do pacote carregado é exibido como **Ativo**. Reinicie o servidor se o status do pacote não for exibido como **Ativo**.
1. Ir para `https://'[server]:[port]'/system/console/configMgr`.
1. Toque **[!UICONTROL Criar configuração de correspondência]**.
1. Selecionar **[!UICONTROL Habilitar Salvar Usando CCRDocumentInstanceService]** e toque em **[!UICONTROL Salvar]**.

### Salvar uma comunicação interativa como rascunho {#save-as-draft-agent-ui}

Execute as seguintes etapas para salvar uma Comunicação interativa como rascunho:

1. Selecione uma Comunicação interativa no Forms Manager e toque em **[!UICONTROL Abrir IU do agente]**.

1. Faça as alterações apropriadas na interface do usuário do agente e toque em **[!UICONTROL Salvar como rascunho]**.

1. Especifique o nome do Rascunho nas **[!UICONTROL Nome]** e toque em **[!UICONTROL Concluído]**.

Depois de salvar a Comunicação interativa como rascunho, toque em **[!UICONTROL Salvar alterações]** para salvar quaisquer alterações adicionais no rascunho.

### Recuperar o rascunho de uma comunicação interativa {#retrieve-draft}

Depois de salvar uma comunicação interativa como rascunho, você pode recuperá-la para continuar trabalhando nela. Recupere a comunicação interativa usando:

`https://server:port/aem/forms/createcorrespondence.hmtl?draftid=[draftid]`

[draftid] refere-se ao identificador exclusivo da versão de rascunho que é gerado após salvar uma Comunicação interativa como rascunho.

### Exemplo de implementação de SPI ccrDocumentInstance {#sample-ccrDocumentInstance-spi}

Implementar o `ccrDocumentInstance` SPI para salvar uma Comunicação interativa como rascunho. Veja a seguir um exemplo de implementação do `ccrDocumentInstance` SPI

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

A variável `save`, `update`, `get`, e `getAll` As operações chamam o serviço de banco de dados para salvar uma Comunicação Interativa como rascunho, atualizar uma Comunicação Interativa, recuperar dados do banco de dados e recuperar dados para todas as Comunicações Interativas disponíveis no banco de dados. Esta amostra usa `mySQLDataBaseServiceCRUD` como o nome do serviço de banco de dados.

A tabela a seguir explica a amostra `ccrDocumentInstance` Implementação da SPI. Demonstra a forma como a `save`, `update`, `get`, e `getAll` As operações chamam o serviço de banco de dados na implementação de amostra.

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

Veja a seguir um exemplo da `pom.xml` arquivo que faz parte da implementação:

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
>Atualize o `aemfd-client-sdk` dependência para 6.0.160 no `pom.xml` arquivo.
