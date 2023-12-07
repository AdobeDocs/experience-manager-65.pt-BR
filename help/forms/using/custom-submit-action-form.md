---
title: Gravação da ação enviar personalizada para formulários adaptáveis
description: O AEM Forms permite criar a ação Enviar personalizada para formulários adaptáveis. Este artigo descreve o procedimento para adicionar uma ação enviar personalizada para formulários adaptáveis.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 7c3d0dac-4e19-4eb3-a43d-909d526acd55
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 1%

---

# Gravação da ação enviar personalizada para formulários adaptáveis{#writing-custom-submit-action-for-adaptive-forms}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/custom-submit-action-form.html) |
| AEM 6.5 | Este artigo |

Os formulários adaptáveis exigem ações de envio para processar dados especificados pelo usuário. A ação Enviar determina a tarefa executada nos dados enviados por meio de um formulário adaptável. O Adobe Experience Manager (AEM) inclui [Ações de envio OOTB](../../forms/using/configuring-submit-actions.md) que demonstram tarefas personalizadas que podem ser executadas usando os dados enviados pelo usuário. Por exemplo, você pode executar tarefas, como enviar emails ou armazenar dados.

## Fluxo de trabalho para uma ação Enviar {#workflow-for-a-submit-action}

O fluxograma representa o fluxo de trabalho de uma ação Enviar acionada ao clicar no botão **[!UICONTROL Enviar]** em um formulário adaptável. Os arquivos no componente Anexo de arquivo são carregados no servidor e os dados de formulário são atualizados com as URLs dos arquivos carregados. No cliente, os dados são armazenados no formato JSON. O cliente envia uma solicitação Ajax para um servlet interno que massageia os dados especificados e os retorna no formato XML. O cliente coleta esses dados com campos de ação. Ele envia os dados para o servlet final (servlet de Envio do Guia) por meio de uma ação de Envio de Formulário. Em seguida, o servlet encaminha o controle para a ação Enviar. A ação Enviar pode encaminhar a solicitação para um recurso do sling diferente ou redirecionar o navegador para outro URL.

![Fluxograma que descreve o fluxo de trabalho para a ação Enviar](assets/diagram1.png)

### Formato de dados XML {#xml-data-format}

Os dados XML são enviados para o servlet usando o **`jcr:data`** parâmetro de solicitação. As ações enviar podem acessar o parâmetro para processar os dados. O código a seguir descreve o formato dos dados XML. Os campos vinculados ao modelo de formulário aparecem na variável **`afBoundData`** seção. Os campos não vinculados aparecem no `afUnoundData`seção. Para obter mais informações sobre o formato do `data.xml` arquivo, consulte [Introdução ao preenchimento prévio de campos de formulário adaptáveis](../../forms/using/prepopulate-adaptive-form-fields.md).

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<!-- xml corresponding to the Form Model /XML Schema -->
</afBoundData>
</afData>
```

### Campos de ação {#action-fields}

Uma ação Enviar pode adicionar campos de entrada ocultos (usando o HTML [entrada](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input) tag) para o HTML de formulário renderizado. Esses campos ocultos podem conter valores necessários ao processar o envio do formulário. Ao enviar o formulário, esses valores de campo são postados de volta como parâmetros de solicitação que a ação Enviar pode usar durante o manuseio do envio. Os campos de entrada são chamados de campos de ação.

Por exemplo, uma ação Enviar que também capture o tempo necessário para preencher um formulário pode adicionar os campos de entrada ocultos `startTime` e `endTime`.

Um script pode fornecer os valores de `startTime` e `endTime` campos quando o formulário é renderizado e antes do envio do formulário, respectivamente. O ActionScript de envio `post.jsp` Em seguida, o pode acessar esses campos usando parâmetros de solicitação e calcular o tempo total necessário para preencher o formulário.

### Anexos de arquivo {#file-attachments}

As ações de envio também podem usar os anexos de arquivo carregados por meio do componente Anexo de arquivo. Os scripts de ação de envio podem acessar esses arquivos usando o sling [API RequestParameter](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html). A variável [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) O método da API ajuda a identificar se o parâmetro de solicitação é um campo de arquivo ou de formulário. Você pode repetir os parâmetros da Solicitação em uma ação Enviar para identificar os parâmetros de Anexo de Arquivo.

O código de exemplo a seguir identifica os anexos de arquivo na solicitação. Em seguida, lê os dados no arquivo usando o [Obter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). Por fim, ele cria um objeto Documento usando os dados e o anexa a uma lista.

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### Caminho de encaminhamento e URL de redirecionamento {#forward-path-and-redirect-url}

Depois de executar a ação necessária, o servlet Submit encaminha a solicitação para o caminho de encaminhamento. Uma ação usa a API setForwardPath para definir o caminho de encaminhamento no servlet Guide Submit.

Se a ação não fornecer um caminho de encaminhamento, o servlet Submit redirecionará o navegador usando o URL de redirecionamento. O autor configura o URL de redirecionamento usando a configuração da página de agradecimento na caixa de diálogo Edição do formulário adaptável. Você também pode configurar o URL de redirecionamento por meio da ação Enviar ou da API setRedirectUrl no servlet Guide Submit. Você também pode configurar os parâmetros de Solicitação enviados para o URL de redirecionamento usando a API setRedirectParameters no servlet de Envio do guia.

>[!NOTE]
>
>Um autor fornece o URL de redirecionamento (usando a Configuração da página de agradecimento). [Ações de envio OOTB](../../forms/using/configuring-submit-actions.md) use o URL de redirecionamento para redirecionar o navegador a partir do recurso ao qual o caminho de encaminhamento faz referência.
>
>Você pode escrever uma ação Enviar personalizada que encaminhe uma solicitação para um recurso ou servlet. A Adobe recomenda que o script que executa o tratamento de recursos para o caminho de encaminhamento redirecione a solicitação para o URL de redirecionamento quando o processamento for concluído.

## Ação de envio {#submit-action}

Uma ação Enviar é uma sling:Folder que inclui o seguinte:

* **addfields.jsp**: esse script fornece os campos de ação que são adicionados ao arquivo de HTML durante a representação. Use esse script para adicionar os parâmetros de entrada ocultos necessários durante o envio no script post.POST.jsp.
* **dialog.xml**: Esse script é semelhante à caixa de diálogo Componente CQ. Ela fornece informações de configuração que o autor personaliza. Os campos são exibidos na guia Enviar ações na caixa de diálogo Editar formulário adaptável ao selecionar a ação Enviar.
* **post.POST.jsp**: O servlet Submit chama esse script com os dados enviados e os dados adicionais nas seções anteriores. Qualquer menção de executar uma ação nesta página implica executar o script post.POST.jsp. Para registrar a ação Enviar com os formulários adaptáveis a serem exibidos na caixa de diálogo Editar formulário adaptável, adicione essas propriedades ao sling:Folder:

   * **guideComponentType** do tipo String e valor **fd/af/components/guidesubmittype**
   * **guideDataModel** do tipo String que especifica o tipo de formulário adaptável ao qual a ação Enviar se aplica. **xfa** é compatível com formulários adaptáveis baseados em XFA enquanto **xsd** O é compatível com formulários adaptáveis baseados em XSD. **básico** O é compatível com formulários adaptáveis que não usam XDP ou XSD. Para exibir a ação em vários tipos de formulários adaptáveis, adicione as cadeias de caracteres correspondentes. Separe cada string por vírgula. Por exemplo, para tornar uma ação visível em formulários adaptáveis baseados em XFA e XSD, especifique os valores **xfa** e **xsd** respectivamente.

   * **jcr:description** do tipo String. O valor dessa propriedade é exibido na lista Ação de envio na guia Ações de envio da caixa de diálogo Edição do formulário adaptável. As ações OOTB estão presentes no repositório CRX no local **/libs/fd/af/components/guidesubmittype**.

## Criar uma ação enviar personalizada {#creating-a-custom-submit-action}

Execute as seguintes etapas para criar uma ação enviar personalizada que salve os dados no repositório CRX e envie um email a você. O formulário adaptável contém o conteúdo de armazenamento da ação Enviar OOTB (desaprovado) que salva os dados no repositório CRX. Além disso, o CQ fornece uma [E-mail](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=pt-BR) API que pode ser usada para enviar emails. Antes de usar a API de e-mail, [configurar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=en&amp;wcmmode=disabled) o serviço Day CQ Mail através do console do sistema. Você pode reutilizar a ação Armazenar conteúdo (obsoleto) para armazenar os dados no repositório. A ação Armazenar conteúdo (desaprovado) está disponível no local /libs/fd/af/components/guidesubmittype/store no repositório CRX.

1. Faça logon no CRXDE Lite no URL https://&lt;server>:&lt;port>/crx/de/index.jsp. Crie um nó com a propriedade sling:Folder e o nome store_and_mail na pasta /apps/custom_submit_action. Crie a pasta custom_submit_action se ela ainda não existir.

   ![Captura de tela que representa a criação de um nó com a propriedade sling:Folder](assets/step1.png)

1. **Forneça os campos de configuração obrigatórios.**

   Adicione a configuração exigida pela ação Armazenar. Copie o **cq:dialog** nó da ação Armazenar de /libs/fd/af/components/guidesubmittype/store para a pasta de ação em /apps/custom_submit_action/store_and_email.

   ![Captura de tela mostrando a cópia do nó da caixa de diálogo para a pasta de ação](assets/step2.png)

1. **Forneça campos de configuração para solicitar ao autor a configuração de email.**

   O formulário adaptável também fornece uma ação de Email que envia emails para os usuários. Personalize esta ação com base em suas necessidades. Navegue até /libs/fd/af/components/guidesubmittype/email/dialog. Copie os nós no nó cq:dialog para o nó cq:dialog da ação Enviar (/apps/custom_submit_action/store_and_email/dialog).

   ![Personalização da ação de email](assets/step3.png)

1. **Disponibilize a ação na caixa de diálogo Edição do formulário adaptável.**

   Adicione as seguintes propriedades no nó store_and_email:

   * **guideComponentType** do tipo **String** e valor **fd/af/components/guidesubmittype**

   * **guideDataModel** do tipo **String** e valor **xfa, xsd, básico**

   * **jcr:description** do tipo **String** e valor **Ação de armazenamento e email**

1. Abra qualquer formulário adaptável. Clique em **Editar** botão ao lado de **Início** para abrir o **Editar** caixa de diálogo do contêiner de formulário adaptável. A nova ação é exibida na janela **Ações de envio** Guia. Selecionar o **Ação de armazenamento e email** exibe a configuração adicionada no nó de diálogo.

   ![Caixa de diálogo Enviar configuração de ação](assets/store_and_email_submit_action_dialog.jpg)

1. **Use a ação para concluir uma tarefa.**

   Adicione o script post.POST.jsp à sua ação. (/apps/custom_submit_action/store_and_mail/).

   Execute a ação de armazenamento OOTB (script post.POST.jsp). Use o [FormsHelper.runAction](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=pt-BR)API (java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse) que o CQ fornece no código para executar a ação Armazenar. Adicione o seguinte código no arquivo JSP:

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   Para enviar o email, o código lê o endereço de email do recipient na configuração. Para buscar o valor de configuração no script da ação, leia as propriedades do recurso atual usando o código a seguir. Da mesma forma, você pode ler os outros arquivos de configuração.

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   Por fim, use a API de email do CQ para enviar o email. Use o [SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) para criar o Objeto de email conforme representado abaixo:

   >[!NOTE]
   >
   >Verifique se o arquivo JSP tem o nome post.POST.jsp.

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   Selecione a ação no formulário adaptável. A ação envia um email e armazena os dados.
