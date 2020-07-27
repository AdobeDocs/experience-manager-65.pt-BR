---
title: Criação de uma ação personalizada da barra de ferramentas
seo-title: Criação de uma ação personalizada da barra de ferramentas
description: Os desenvolvedores de formulários podem criar ações personalizadas da barra de ferramentas para formulários adaptáveis no AEM Forms. O uso de ações personalizadas por autores de formulários pode fornecer mais workflows e opções aos usuários finais.
seo-description: Os desenvolvedores de formulários podem criar ações personalizadas da barra de ferramentas para formulários adaptáveis no AEM Forms. O uso de ações personalizadas por autores de formulários pode fornecer mais workflows e opções aos usuários finais.
uuid: cd785cfb-e1bb-4158-be9b-d99e04eccc02
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 4beca23f-dbb0-4e56-8047-93e4f1775418
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---


# Criação de uma ação personalizada da barra de ferramentas{#creating-a-custom-toolbar-action}

## Pré-requisitos {#prerequisite}

Antes de criar uma ação personalizada da barra de ferramentas, familiarize-se com [Usar bibliotecas](/help/sites-developing/clientlibs.md) do lado do cliente e [Desenvolver com o CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## O que é uma ação {#what-is-an-action-br}

Um formulário adaptável fornece uma barra de ferramentas que permite ao autor configurar um conjunto de opções. Essas opções são definidas como ações para o formulário adaptável. Clique no botão Editar na barra de ferramentas do Painel para definir as ações suportadas pelos formulários adaptáveis.

![Ações padrão da barra de ferramentas](assets/default_toolbar_actions.png)

Além do conjunto de ações fornecido por padrão, você pode criar ações personalizadas na barra de ferramentas. Por exemplo, é possível adicionar uma ação para permitir que o usuário revise todos os campos do formulário adaptável antes do envio do formulário.

## Etapas para criar uma ação personalizada em formulários adaptáveis {#steps}

Para ilustrar a criação de uma ação personalizada da barra de ferramentas, as etapas a seguir o orientam a criar um botão para que os usuários finais revisem todos os campos do formulário adaptável antes de enviar um formulário preenchido.

1. Todas as ações padrão suportadas por formulários adaptáveis estão presentes na `/libs/fd/af/components/actions` pasta. No CRXDE, copie o `fileattachmentlisting` nó de `/libs/fd/af/components/actions/fileattachmentlisting` para `/apps/customaction`.

1. Depois de copiar o nó para a `apps/customaction` pasta, renomeie o nome do nó para `reviewbeforesubmit`. Além disso, altere as propriedades `jcr:title` e `jcr:description` do nó.

   A `jcr:title` propriedade contém o nome da ação exibida na caixa de diálogo da barra de ferramentas. A `jcr:description` propriedade contém mais informações que são exibidas quando um usuário posiciona o ponteiro sobre a ação.

   ![Hierarquia de nós para personalização da barra de ferramentas](assets/action3.png)

1. Selecione `cq:template` nó no `reviewbeforesubmit` nó. Verifique se o valor da `guideNodeClass` propriedade é `guideButton` e altere a `jcr:title` propriedade de acordo.
1. Altere a propriedade type no `cq:Template` nó. No exemplo atual, altere a propriedade type para button.

   O valor de tipo é adicionado como uma classe CSS no HTML gerado para o componente. Os usuários podem usar essa Classe CSS para criar um estilo para suas ações. O estilo padrão para dispositivos móveis e de desktop é fornecido para os valores de tipo de botão, botão, enviar, redefinir e salvar.

1. Selecione a ação personalizada na caixa de diálogo da barra de ferramentas de edição de formulário adaptável. Um botão Revisar é exibido na barra de ferramentas do painel.

   ![A ação personalizada está disponível na barra](assets/custom_action_available_in_toolbar.png) de ferramentas ![Exibindo a ação da barra de ferramentas criada personalizada](assets/action7.png)

1. Para fornecer funcionalidade ao botão Revisar, adicione algum código JavaScript e CSS e código do lado do servidor no arquivo init.jsp, presente no `reviewbeforesubmit` nó.

   Adicione o seguinte código em `init.jsp`.

   ```jsp
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <guide:initializeBean name="guideField" className="com.adobe.aemds.guide.common.GuideButton"/>
   
   <c:if test="${not isEditMode}">
           <cq:includeClientLib categories="reviewsubmitclientlibruntime" />
   </c:if>
   
   <%--- BootStrap Modal Dialog  --------------%>
   <div class="modal fade" id="reviewSubmit" tabindex="-1">
       <div class="modal-dialog">
           <div class="modal-content">
               <div class="modal-header">
                   <h3>Review the Form Fields</h3>
               </div>
               <div class="modal-body">
                   <div class="modal-list">
                       <table class="table table-bordered">
                           <tr class="name">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Name is: </label>
                               </td>
                           </tr>
                           <tr class="pan">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Pan Number is: </label>
                               </td>
                           </tr>
                           <tr class="dob">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Date Of Birth is: </label>
                               </td>
                           </tr>
                           <tr class="80cdeclaration">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Total 80C Declaration Amount is: </label>
                               </td>
                           </tr>
                           <tr class="rentpaid">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Total HRA Amount is: </label>
                               </td>
                           </tr>
                       </table>
                   </div>
               </div><!-- /.modal-body -->
               <div class="modal-footer">
                   <div class="fileAttachmentListingCloseButton col-md-2 col-xs-2 col-sm-2">
                       <button data-dismiss="modal">Close</button>
                   </div>
               </div>
           </div><!-- /.modal-content -->
       </div><!-- /.modal-dialog -->
   </div><!-- /.modal -->
   ```

   Adicione o seguinte código no `ReviewBeforeSubmit.js` arquivo.

   ```javascript
   /*anonymous function to handle show of review before submit view */
   $(function () {
       if($("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").length > 0) {
           $("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").click(function(){
               // Create the options object to be passed to the getElementProperty API
               var options = {},
                   result = [];
               options.somExpressions = [];
               options.propertyName = "value";
               guideBridge.visit(function(model){
                   if(model.name === "name" || model.name === "pan" || model.name === "dateofbirth" || model.name === "total" || model.name === "totalmonthlyrent"){
                           options.somExpressions.push(model.somExpression);
                   }
               }, this);
               result = guideBridge.getElementProperty(options);
   
               $('#reviewSubmit .reviewlabel').each(function(index, item){
                   var data = ((result.data[index] == null) ? "No Data Filled" : result.data[index]);
                   if($(this).next().hasClass("reviewlabelvalue")){
                       $(this).next().html(data);
                   } else {
                       $(this).after($("<td></td>").addClass("reviewlabelvalue col-md-6 active").html(data));
                   }
               });
               // added because in mobile devices it was causing problem of backdrop
               $("#reviewSubmit").appendTo('body');
               $("#reviewSubmit").modal("show");
           });
       }
   });
   ```

   Adicione o seguinte código ao `ReviewBeforeSubmit.css` arquivo.

   ```css
   .modal-list .reviewlabel {
       white-space: normal;
       text-align: right;
       padding:2px;
   }
   
   .modal-list .reviewlabelvalue {
       border: #cde0ec 1px solid;
       padding:2px;
   }
   
   /* Adding icon for this action in mobile devices */
   /* This is the glyphicon provided by bootstrap eye-open */
   /* .<type> .iconButton-icon */
   .reviewbeforesubmit .iconButton-icon {
       position: relative;
       top: -8px;
       font-family: 'Glyphicons Halflings';
       font-style: normal;
   }
   
   .reviewbeforesubmit .iconButton-icon:before {
       content: "\e105"
   }
   ```

1. Para verificar a funcionalidade da ação personalizada, abra o formulário adaptável no modo de Pré-visualização e clique em Revisar na barra de ferramentas.

   >[!NOTE]
   >
   >A `GuideBridge` biblioteca não é carregada no modo de criação. Portanto, essa ação personalizada não funciona no modo de criação.

   ![Demonstração da ação do botão de revisão personalizado](assets/action9.png)

## Amostras {#samples}

O arquivo a seguir contém um pacote de conteúdo. O pacote inclui um formulário adaptável relacionado à demonstração acima da ação personalizada da barra de ferramentas.

[Obter arquivo](assets/customtoolbaractiondemo.zip)
