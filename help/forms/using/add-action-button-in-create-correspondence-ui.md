---
title: Adicionar ação/botão personalizado na interface Criar correspondência
seo-title: Adicionar ação/botão personalizado na interface Criar correspondência
description: Saiba como adicionar ação/botão personalizado na interface Criar correspondência
seo-description: Saiba como adicionar ação/botão personalizado na interface Criar correspondência
uuid: 1b2b00bb-93ef-4bfe-9fc5-25c45e4cb4b1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 046e3314-b436-47ed-98be-43d85f576789
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 1%

---


# Adicionar ação/botão personalizado na interface Criar correspondência {#add-custom-action-button-in-create-correspondence-ui}

## Visão geral {#overview}

A solução Gerenciamento de correspondência permite adicionar ações personalizadas à interface do usuário Criar correspondência.

O cenário neste documento explica como você pode criar um botão na interface Criar usuário de correspondência para compartilhar uma carta como um PDF de revisão anexado a um email.

### Pré-requisitos {#prerequisites}

Para concluir este cenário, você precisa do seguinte:

* Conhecimento sobre CRX e JavaScript
* LiveCycle Server

## Cenário: Crie o botão na interface Criar usuário de correspondência para enviar uma carta para revisão {#scenario-create-the-button-in-the-create-correspondence-user-interface-to-send-a-letter-for-review}

A adição de um botão com uma ação (aqui, enviar carta para revisão) à interface Criar usuário de correspondência inclui:

1. Adicionar o botão à interface Criar usuário de correspondência
1. Adicionar manipulação de ação ao botão
1. Adicionar o processo do LiveCycle para ativar a manipulação de ações

### Adicione o botão à interface do usuário Criar correspondência {#add-the-button-to-the-create-correspondence-user-interface}

1. Vá para `https://'[server]:[port]'/[ContextPath]/crx/de` e faça logon como Administrador.
1. Na pasta apps, crie uma pasta chamada `defaultApp` com caminho/estrutura semelhante à pasta defaultApp (localizada na pasta config). Use as seguintes etapas para criar a pasta:

   1. Clique com o botão direito do mouse na pasta **defaultApp** no seguinte caminho e selecione **Sobrepor nó**:

      /libs/fd/cm/config/defaultApp/

      ![Nó Sobreposição](assets/1_defaultapp.png)

   1. Certifique-se de que a caixa de diálogo Sobrepor nó tenha os seguintes valores:

      **Caminho:** /libs/fd/cm/config/defaultApp/

      **Localização da sobreposição:** /apps/

      **Corresponder tipos de nós:** Verificado

      ![Nó Sobreposição](assets/2_defaultappoverlaynode.png)

   1. Clique em **OK**.
   1. Clique em **Salvar tudo**.

1. Faça uma cópia do arquivo acmExtensionsConfig.xml (existe na ramificação /libs) na ramificação /apps.

   1. Vá para &quot;/libs/fd/cm/config/defaultApp/acmExtensionsConfig.xml&quot;

   1. Clique com o botão direito do mouse no arquivo acmExtensionsConfig.xml e selecione **Copiar**.

      ![Copiar acmExtensionsConfig.xml](assets/3_acmextensionsconfig_xml_copy.png)

   1. Clique com o botão direito do mouse na pasta **defaultApp** em &quot;/apps/fd/cm/config/defaultApp/&quot; e selecione **Colar**.
   1. Clique em **Salvar tudo**.

1. Clique com o Duplo na cópia de acmExtentionsConfig.xml que você criou recentemente na pasta de aplicativos. O arquivo é aberto para edição.
1. Localize o seguinte código:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <extensionsConfig>
       <modelExtensions>
           <modelExtension type="LetterInstance">
     <customAction name="Preview" label="loc.letterInstance.preview.label" tooltip="loc.letterInstance.preview.tooltip" styleName="previewButton"/>
               <customAction name="Submit" label="loc.letterInstance.submit.label" tooltip="loc.letterInstance.submit.tooltip" styleName="submitButton" permissionName="forms-users"/>
               <customAction name="SaveAsDraft" label="loc.letterInstance.saveAsDraft.label" tooltip="loc.letterInstance.saveAsDraft.tooltip" styleName="submitButton" permissionName="forms-users"/>
               <customAction name="Close" label="loc.letterInstance.close.label" tooltip="loc.letterInstance.close.tooltip" styleName="closeButton"/>
           </modelExtension>
       </modelExtensions>
   </extensionsConfig>
   ```

1. Para enviar uma carta por email, você pode usar o LiveCycle Forms Workflow. Adicione uma tag customAction sob a tag modelExtension em acmExtensionsConfig.xml como segue:

   ```xml
    <customAction name="Letter Review" label="Letter Review" tooltip="Letter Review" styleName="" permissionName="forms-users" actionHandler="CM.domain.CCRCustomActionHandler">
         <serviceName>Forms Workflow -> SendLetterForReview/SendLetterForReviewProcess</serviceName>
       </customAction>
   ```

   ![tag customAction](assets/5_acmextensionsconfig_xml.png)

   A tag modelExtension tem um conjunto de tags-filho customAction que configuram a ação, as permissões e a aparência do botão de ação. Veja a seguir a lista das tags de configuração customAction:

   | **Nome** | **Descrição** |
   |---|---|
   | name | O nome alfanumérico da ação a ser executada. O valor dessa tag é obrigatório, deve ser exclusivo (dentro da tag modelExtension) e deve ser start com um alfabeto. |
   | label | O rótulo a ser exibido no botão de ação |
   | tooltip | Texto de dica de ferramenta do botão, que é exibido quando o usuário passa o mouse sobre o botão. |
   | styleName | Nome do estilo personalizado aplicado ao botão de ação. |
   | permissionsName | A ação correspondente é exibida somente se o usuário tiver a permissão especificada por permissionsName. Quando você especifica a propriedade permissionsName como, `forms-users`todos os usuários terão acesso a essa opção. |
   | actionHandler | Nome totalmente qualificado da classe ActionHandler que é chamada quando o usuário clica no botão. |

   Além dos parâmetros acima, pode haver configurações adicionais associadas a um customAction. Essas configurações adicionais são disponibilizadas ao manipulador por meio do objeto CustomAction.

   | **Nome** | **Descrição** |
   |---|---|
   | serviceName | Se um customAction contiver uma tag-filho com o nome serviceName, ao clicar no botão/link relevante, um processo é chamado com o nome representado pela tag serviceName. Certifique-se de que esse processo tenha a mesma assinatura que a Carta PostProcess. Adicione o prefixo &quot;Fluxo de trabalho do Forms ->&quot; no nome do serviço. |
   | Parâmetros que contêm o prefixo cm_ no nome da tag | Se um customAction contiver tags-filho que começam com o nome cm_, então no processo posterior (seja o Processo de publicação de carta ou o processo especial representado pela tag serviceName) esses parâmetros estão disponíveis no código XML de entrada sob a tag relevante com a remoção do prefixo cm_. |
   | actionName | Sempre que um processo de publicação é devido a um clique, o XML enviado contém uma tag especial com nome na tag com o nome da ação do usuário. |

1. Clique em **Salvar tudo**.

#### Criar uma pasta de localidade com arquivo de propriedades na ramificação /apps {#create-a-locale-folder-with-properties-file-in-the-apps-branch}

O arquivo ACMExtensionsMessages.properties inclui rótulos e mensagens de dica de ferramenta de vários campos na interface de usuário Criar correspondência. Para que as ações/botões personalizados funcionem, faça uma cópia desse arquivo na ramificação /apps.

1. Clique com o botão direito do mouse na pasta **local** no seguinte caminho e selecione **Sobrepor nó**:

   /libs/fd/cm/config/defaultApp/locale

1. Certifique-se de que a caixa de diálogo Sobrepor nó tenha os seguintes valores:

   **Caminho:** /libs/fd/cm/config/defaultApp/locale

   **Localização da sobreposição:** /apps/

   **Corresponder tipos de nós:** Verificado

1. Clique em **OK**.
1. Clique em **Salvar tudo**.
1. Clique com o botão direito do mouse no arquivo a seguir e selecione **Copiar**:

   `/libs/fd/cm/config/defaultApp/locale/ACMExtensionsMessages.properties`

1. Clique com o botão direito do mouse na pasta **local** no seguinte caminho e selecione **Colar**:

   `/apps/fd/cm/config/defaultApp/locale/`

   O arquivo ACMExtensionsMessages.properties é copiado na pasta da localidade.

1. Para localizar os rótulos da ação/botão personalizado recém-adicionado, crie o arquivo ACMExtensionsMessages.properties para a localidade relevante em `/apps/fd/cm/config/defaultApp/locale/`.

   Por exemplo, para localizar a ação/botão personalizado criado neste artigo, crie um arquivo chamado ACMExtensionsMessages_fr.properties com a seguinte entrada:

   `loc.letterInstance.letterreview.label=Revue De Lettre`

   Da mesma forma, é possível adicionar mais propriedades, como dicas de ferramentas e estilo, neste arquivo.

1. Clique em **Salvar tudo**.

#### Reinicie o pacote de blocos componentes do Adobe Asset Composer {#restart-the-adobe-asset-composer-building-block-bundle}

Depois de fazer todas as alterações no servidor, reinicie o pacote de blocos componentes do Adobe Asset Composer. Nesse cenário, os arquivos acmExtensionsConfig.xml e ACMExtensionsMessages.properties no lado do servidor são editados e, portanto, o pacote Bloco de construção do Adobe Asset Composer requer uma reinicialização.

>[!NOTE]
>
>Talvez seja necessário limpar o cache do navegador.

1. Ir para `https://[host]:'port'/system/console/bundles`. Se necessário, faça logon como Administrador.

1. Localize o pacote de blocos componentes do Adobe Asset Composer. Reinicie o pacote: clique em Parar e em Start.

   ![Bloco construtor do Adobe Asset Composer](assets/6_assetcomposerbuildingblockbundle.png)

Após reiniciar o pacote Bloco de construção do Adobe Asset Composer, o botão personalizado será exibido na interface Criar usuário de correspondência. Você pode abrir uma carta na interface Criar usuário de correspondência para pré-visualização o botão personalizado.

### Adicionar manipulação de ação ao botão {#add-action-handling-to-the-button}

A interface de usuário Criar correspondência por padrão tem a implementação do ActionHandler no arquivo cm.domain.js no seguinte local:

/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccr/js/cm.domain.js

Para manipulação de ações personalizadas, crie uma sobreposição do arquivo cm.domain.js na ramificação /apps do CRX.

O manuseio da ação/botão ao clicar em ação/botão inclui lógica para:

* Tornando a ação recém-adicionada visível/invisível: feita substituindo a função actionVisible().
* Ativando/desabilitando a ação recém-adicionada: feita substituindo a função actionEnabled().
* Manuseio real da ação quando o usuário clica no botão: feita substituindo a implementação da função identificadorAction().

1. Ir para `https://'[server]:[port]'/[ContextPath]/crx/de`. Se necessário, faça logon como Administrador.

1. Na pasta apps, crie uma pasta chamada `js` na ramificação /apps do CRX com estrutura semelhante à seguinte pasta:

   `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

   Use as seguintes etapas para criar a pasta:

   1. Clique com o botão direito do mouse na pasta **js** no seguinte caminho e selecione **Sobrepor nó**:

      `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

   1. Certifique-se de que a caixa de diálogo Sobrepor nó tenha os seguintes valores:

      **Caminho:** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js

      **Localização da sobreposição:** /apps/

      **Corresponder tipos de nós:** Verificado

   1. Clique em **OK**.
   1. Clique em **Salvar tudo**.

1. Na pasta js, crie um arquivo chamado ccrcustomization.js com o código para a manipulação de ação do botão usando as seguintes etapas:

   1. Clique com o botão direito do mouse na pasta **js** no seguinte caminho e selecione **Criar > Criar arquivo**:

      `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

      Nomeie o arquivo como ccrcustomization.js.

   1. Clique com o Duplo no arquivo crcustomization.js para abri-lo no CRX.
   1. No arquivo, cole o seguinte código e clique em **Salvar tudo**:

      ```javascript
      /* for adding and handling custom actions in Extensible Toolbar.
        * One instance of handler will be created for each action.
        * CM.domain.CCRCustomActionHandler is actionHandler class.
        */
      var CCRCustomActionHandler;
          CCRCustomActionHandler = CM.domain.CCRCustomActionHandler = new Class({
              className: 'CCRCustomActionHandler',
              extend: CCRDefaultActionHandler,
              construct : function(action,model){
              }
          });
          /**
           * Called when user user click an action
           * @param extraParams additional arguments that may be passed to handler (For future use)
           */
          CCRCustomActionHandler.prototype.handleAction = function(extraParams){
              if (this.action.name == CCRCustomActionHandler.SEND_FOR_REVIEW) {
                  var sendForReview = function(){
                      var serviceName = this.action.actionConfig["serviceName"];
                      var inputParams = {};
                      inputParams["dataXML"] = this.model.iccData.data;
                      inputParams["letterId"] = this.letterVO.id;
                      inputParams["letterName"] = this.letterVO.name;
                      inputParams["mailId"] = $('#email').val();
                      /*function to invoke the LivecyleService */
                      ServiceDelegate.callJSONService(this,"lc.icc.renderlib.serviceInvoker.json","invokeProcess",[serviceName,inputParams],this.onProcessInvokeComplete,this.onProcessInvokeFail);
                      $('#ccraction').modal("hide");
                  }
                  if($('#ccraction').length == 0){
                      /*For first click adding popup & setting letterName.*/
                      $("body").append(popUp);
                      $("input[id*='letterName']").val(this.letterVO.name);
                      $(document).on('click',"#submitLetter",$.proxy( sendForReview, this ));
                  }
                  $('#ccraction').modal("show");
              }
          };
          /**
           * Should the action be enabled in toolbar
           * @param extraParams additional arguements that may be passed to handler (For future use)
           * @return flag indicating whether the action should be enabled
           */
         CCRCustomActionHandler.prototype.actionEnabled = function(extraParams){
                  /*can be customized as per user requirement*/
                  return true;
          };
          /**
           * Should the action be visible in toolbar
           * @param extraParams additional arguments that may be passed to handler (For future use)
           * @return flag indicating whether the action should be enabled
           */
          CCRCustomActionHandler.prototype.actionVisible = function(extraParams){
              /*Check can be enabled for Non-Preview Mode.*/
              return true;
          };
          /*SuccessHandler*/
          CCRCustomActionHandler.prototype.onProcessInvokeComplete = function(response) {
              ErrorHandler.showSuccess("Letter Sent for Review");
          };
          /*FaultHandler*/
          CCRCustomActionHandler.prototype.onProcessInvokeFail = function(event) {
              ErrorHandler.showError(event.message);
          };
          CCRCustomActionHandler.SEND_FOR_REVIEW  = "Letter Review";
      /*For PopUp*/
          var popUp = '<div class="modal fade" id="ccraction" tabindex="-1" role="dialog" aria-hidden="true">'+
          '<div class="modal-dialog modal-sm">'+
              '<div class="modal-content">' +
                  '<div class="modal-header">'+
                      '<button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</code></button>'+
                      '<h4 class="modal-title"> Send Review </h4>'+
                  '</div>'+
                  '<div class="modal-body">'+
                      '<form>'+
                          '<div class="form-group">'+
                              '<label class="control-label">Email Id</label>'+
                              '<input type="text" class="form-control" id="email">'+
                          '</div>'+
                          '<div class="form-group">'+
                              '<label  class="control-label">Letter Name</label>'+
                              '<input id="letterName" type="text" class="form-control" readonly>'+
                          '</div>'+
                          '<div class="form-group">'+
                              '<input id="letterData" type="text" class="form-control hide" readonly>'+
                          '</div>'+
                      '</form>'+
                  '</div>'+
                  '<div class="modal-footer">'+
                     '<button type="button" class="btn btn-default" data-dismiss="modal"> Cancel </button>'+
                     '<button type="button" class="btn btn-primary" id="submitLetter"> Submit </button>'+
                  '</div>'+
              '</div>'+
          '</div>'+
      '</div>';
      ```

### Adicionar o processo do LiveCycle para ativar a <span class="acrolinxCursorMarker"></code>manipulação de ações {#add-the-livecycle-process-to-enable-action-span-class-acrolinxcursormarker-span-handling}

Nesse cenário, ative os seguintes componentes, que fazem parte do arquivo components.zip anexado:

* DSC componente jar (DSCSampliar.jar)
* Enviar carta para o processo de revisão LCA (SendLetterForReview.lca)

Baixe e descompacte o arquivo components.zip para obter os arquivos DSCSape.jar e SendLetterForReview.lca. Use esses arquivos conforme especificado nos procedimentos a seguir.
components.zip

#### Configurar o LiveCycle Server para executar o processo LCA {#configure-the-livecycle-server-to-run-the-lca-process}

>[!NOTE]
>
>Esta etapa é necessária somente se você estiver em uma configuração OSGI e a integração LC for necessária para o tipo de personalização que você está implementando.

O processo LCA é executado no servidor do LiveCycle e requer o endereço do servidor e as credenciais de logon.

1. Vá para `https://'[server]:[port]'/system/console/configMgr` e faça logon como Administrador.
1. Localize a Configuração do SDK do Adobe LiveCycle Client e clique em **Editar** (ícone editar). O painel Configurações é aberto.

1. Digite os seguintes detalhes e clique em **Salvar**:

   * **URL** do servidor: URL do servidor LC cujo serviço Enviar para revisão o código do manipulador de ação usa.
   * **Nome de usuário**: Nome de usuário administrador do servidor LC
   * **Senha**: Senha do nome de usuário administrador

   ![Configuração do Adobe LiveCycle Client SDK](assets/3_clientsdkconfiguration.png)

#### Instalar o LiveCycle Archive (LCA) {#install-livecycle-archive-lca}

O processo necessário do LiveCycle que ativa o processo do serviço de email.

>[!NOTE]
>
>Para visualização do que este processo faz ou para criar um processo semelhante ao seu, você precisa do Workbench.

1. Faça logon como Administrador no adminui do Livecycle Server em `https:/[lc server]/:[lc port]/adminui`.

1. Navegue até **Início > Serviços > Aplicativos e serviços > Gerenciamento** de aplicativos.

1. Se o aplicativo SendLetterForReview já estiver presente, pule as etapas restantes neste procedimento; caso contrário, continue para as próximas etapas.

   ![Aplicativo SendLetterForReview na interface do usuário](assets/12_applicationmanagementlc.png)

1. Clique em **Importar**.

1. Clique em **Escolher arquivo** e selecione SendLetterForReview.lca.

   ![Selecione o arquivo SendLetterForReview.lca](assets/14_sendletterforreview_lca.png)

1. Clique em **Pré-visualização**.

1. Selecione **Implantar ativos para tempo de execução quando a importação estiver concluída**.

1. Clique em **Importar**.

#### Adicionando ServiceName à lista do Serviço de Lista de permissões {#adding-servicename-to-the-allowlist-service-list}

Mencione no servidor de AEM os serviços do LiveCycle que você deseja acessar no servidor de AEM.

1. Faça logon como Administrador para `https:/[host]:'port'/system/console/configMgr`.

1. Localize e clique em Configuração **do SDK do cliente** Adobe LiveCycle. O painel Configuração do SDK do Adobe LiveCycle Client é exibido.
1. Na lista Nome do serviço, clique no ícone + e adicione um serviceName **SendLetterForReview/SendLetterForReviewProcess**.

1. Clique em **Salvar**.

#### Configurar o serviço de email {#configure-the-email-service}

Nesse cenário, para que o Gerenciamento de correspondência possa enviar um email, configure o serviço de email no servidor do LiveCycle.

1. Efetue logon com as credenciais de Administrador no adminui do Livecycle Server em `https:/[lc server]:[lc port]/adminui`.

1. Navegue até **Início > Serviços > Aplicativos e serviços > Gerenciamento** de serviços.

1. Localize e clique em **EmailService**.

1. No Host **** SMTP, configure o serviço de email.

1. Clique em **Salvar**.

#### Configurar o serviço DSC {#configure-the-dsc-service}

Para usar a API do Correspondence Management, baixe o DSCSampliar.jar (anexado neste documento como parte de components.zip) e carregue-o no servidor do LiveCycle. Depois que o arquivo DSCSamplie.jar é carregado no servidor do LiveCycle, o servidor do AEM usa o arquivo DSCSamplie.jar para acessar a API renderLetter.

Para obter mais informações, consulte [Conectar AEM Forms ao Adobe LiveCycle](/help/forms/using/aem-livecycle-connector.md).

1. Atualize o URL do servidor AEM em cmsa.properties em DSCSampliar.jar, que está no seguinte local:

   DSCSamplia.jar\com\adobe\livecycle\cmsa.properties

1. Forneça os seguintes parâmetros no arquivo de configuração:

   * **crx.serverUrl**=https:/host:port/[context path]/URL[AEM]
   * **crx.username**= nome de usuário do AEM
   * **crx.password**= senha do AEM
   * **crx.appRoot**=/content/apps/cm

   >[!NOTE]
   >
   >Sempre que você fizer alterações no lado do servidor, reinicie o LiveCycle Server. Para obter informações sobre como criar seu próprio componente do LiveCycle ES, consulte [Extensão do software LiveCycle ES por meio do desenvolvimento](https://www.adobe.com/devnet/livecycle/articles/dsc_development.html)personalizado do DSC.

   O arquivo DSCSamplie.jar usa a API renderLetter. Para obter mais informações sobre a API renderLetter, consulte [Interface LetterRenderService](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/ddg/api/LetterRenderService.html).

#### Importar DSC para o LiveCycle {#import-dsc-to-livecyle}

O arquivo DSCSamplie.jar usa a API renderLetter para renderizar a carta como bytes PDF dos dados XML que C fornece como entrada. Para obter mais informações sobre a renderizaçãoCarta e outras APIs, consulte Serviço [de renderização de](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/ddg/api/LetterRenderService.html)carta.

1. Start Workbench e faça logon.
1. Selecione **Janela > Mostrar Visualizações > Componentes**. A visualização Componentes é adicionada ao Workbench ES2.

1. Clique com o botão direito do mouse em **Componentes** e selecione **Instalar componente**.

1. Selecione o arquivo **DSCSamplie.jar** no navegador de arquivos e clique em **Abrir**.
1. Clique com o botão direito do mouse em **RenderWrapper** e selecione Componente **do** Start. Se o componente for start, uma seta verde será exibida ao lado do nome do componente.

## Enviar carta para revisão {#send-letter-for-review}

Depois de configurar a ação e o botão para enviar a carta para revisão:

1. Limpe o cache do navegador.

1. Na interface Criar correspondência, clique em Revisão **da** carta e especifique a ID de email do revisor.

1. Clique em **Enviar**.

![sendreview](assets/sendreview.png)

O revisor recebe um email do sistema com a carta como um anexo PDF.
