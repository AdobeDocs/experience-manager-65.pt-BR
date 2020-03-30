---
title: Integração do Form Bridge com o portal personalizado para formulários HTML5
seo-title: Integração do Form Bridge com o portal personalizado para formulários HTML5
description: Você pode usar a API FormBridge para obter ou definir os valores dos campos de formulário na página HTML e enviar o formulário.
seo-description: Você pode usar a API FormBridge para obter ou definir os valores dos campos de formulário na página HTML e enviar o formulário.
uuid: c8911f82-1a25-47a5-9a06-19b5dce74a2c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bd9bf095-d74d-458c-afe7-fab04050849d
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Integração do Form Bridge com o portal personalizado para formulários HTML5{#integrating-form-bridge-with-custom-portal-for-html-forms}

O FormBridge é uma API de ponte de formulários HTML5 que permite interagir com um formulário. Para obter a referência da API FormBridge, consulte Referência [da API do](/help/forms/using/form-bridge-apis.md)FormBridge.

Você pode usar a API FormBridge para obter ou definir os valores dos campos de formulário na página HTML e enviar o formulário. Por exemplo, você pode usar a API para criar uma experiência semelhante a um assistente.

Um aplicativo HTML existente pode aproveitar a API FormBridge para interagir com um formulário e incorporá-lo à página HTML. É possível usar as seguintes etapas para definir o valor de um campo usando a API Form Bridge.

## Integração de formulários HTML5 a uma página da Web {#integrating-html-forms-to-a-web-page}

1. **Escolha um Perfil ou crie um Perfil**

   1. Na interface CRX DE, navegue até: `https://'[server]:[port]'/crx/de`.
   1. Faça logon com as credenciais de administrador.
   1. Crie um perfil ou escolha um perfil existente.

      Para obter detalhes sobre como criar um perfil, consulte [Criação de um novo Perfil](/help/forms/using/custom-profile.md).

1. **Modificar o Perfil HTML**

   Inclua tempo de execução XFA, biblioteca de localidades XFA e trecho HTML de formulário XFA no renderizador de perfis, crie sua página da Web e insira o formulário na página da Web.

   Por exemplo, use o seguinte trecho de código para criar um aplicativo com dois campos de entrada e um formulário para demonstrar a interação entre o formulário e um aplicativo externo.

   ```xml
   <%@ page session="false"
                  contentType="text/html; charset=utf-8"%><%
   %><%@ taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
   %><!DOCTYPE html>
   <html manifest="${param.offlineSpec}">
       <head>
          <cq:include script="formRuntime.jsp"/>
           <!-- Portal Scripts and Styles -->
          <cq:include script="portalheader.jsp"/>
       </head>
       <body>
           <div id="leftdiv" >
               <div id="leftdivcontentarea">
                   <!-- Portal Body -->
                 <cq:include script="portalbody.jsp"/>
               </div>
           </div>
           <div id="rightdiv">
               <div id="formBody">
               <cq:include script="config.jsp"/>
               <!-- Form body -->
               <cq:include script="formBody.jsp"/>
               <!  --To assist in page transitions -- add navigation, based on scrolling -->
               <cq:include  script="../nav/scroll/nav_footer.jsp"/>
               <cq:include script="footer.jsp"/>
               </div>
           </div>
       </body>
   </html>
   ```

   >[!NOTE]
   >
   >A **linha 9** contém referência JSP adicional para estilos CSS e arquivos JavaScript para projetar a página.
   >
   >
   >A tag &lt;div id=&quot;rightdiv&quot;> na **linha 18** contém o trecho HTML do formulário XFA.
   A página tem o estilo de dois container: **esquerda** e **direita**. O container direito tem o formulário. O container esquerdo tem dois campos de entrada e parte da página HTML externa.
   A seguinte captura de tela mostra como o formulário é exibido em um navegador.

   ![portal](assets/portal.jpg)

   O lado esquerdo faz parte da página **** HTML. O lado direito que contém os campos é o formulário **** xfa.

1. **Acessar os campos de formulário na página**

   A seguir está um script de amostra que pode ser adicionado para definir valores em um campo de formulário.

   Por exemplo, se você quiser definir **EmployeeName** usando os valores nos Campos **First Name** e **Last Name**, chame a função **window.formBridge.setFieldValue** .

   Da mesma forma, é possível ler o valor chamando **window.formBridge.getFieldValue** API.

   ```javascript
   $(function() {
               $(".input").blur(function() {
                   window.formBridge.setFieldValue(
                               'xfa.form.form1.#subform[0].EmployeeName',
                                $("#lname").val()+' '+$("#fname").val()
                              )
                   });
           });
   ```

[Entre em contato com o suporte](https://www.adobe.com/account/sign-in.supportportal.html)
