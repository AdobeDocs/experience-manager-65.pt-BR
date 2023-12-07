---
title: Integração do Form Bridge com o portal personalizado para formulários HTML5
description: Você pode usar a API FormBridge para obter ou definir os valores dos campos de formulário na página HTML e enviar o formulário.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: Mobile Forms
exl-id: 89118bb8-6ec8-4048-b3d6-5c73a9eea33e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# Integração do Form Bridge com o portal personalizado para formulários HTML5{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge é uma API de ponte de formulários HTML5 que permite interagir com um formulário. Para obter a referência da API FormBridge, consulte [Referência da API do FormBridge](/help/forms/using/form-bridge-apis.md).

Você pode usar a API FormBridge para obter ou definir os valores dos campos de formulário na página HTML e enviar o formulário. Por exemplo, você pode usar a API para criar uma experiência semelhante a um assistente.

Um aplicativo HTML existente pode usar a API FormBridge para interagir com um formulário e incorporá-lo na página HTML. Você pode usar as seguintes etapas para definir o valor de um campo usando a API do Form Bridge.

## Integração de formulários HTML5 a uma página da Web {#integrating-html-forms-to-a-web-page}

1. **Escolha um perfil ou crie um perfil**

   1. Na interface do CRX DE, acesse: `https://'[server]:[port]'/crx/de`.
   1. Faça logon com credenciais de administrador.
   1. Crie um perfil ou escolha um perfil existente.

      Para obter detalhes sobre como criar um perfil, consulte [Criar um perfil](/help/forms/using/custom-profile.md).

1. **Modificar o perfil do HTML**

   Inclua o tempo de execução XFA, a biblioteca de localidades XFA e o trecho de HTML do formulário XFA no renderizador de perfil, crie sua página da Web e coloque o formulário dentro da página da Web.

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
   >A variável **linha 9**, contém referências JSP adicionais para estilos CSS e arquivos JavaScript para criar a página.
   >
   >
   >A variável &lt;div id=&quot;rightdiv&quot;> tag ativada **linha 18** contém o trecho HTML do formulário XFA.
   >
   >
   A página tem o estilo de dois contêineres: **left** e **direita**. O contêiner direito tem o formulário. O container esquerdo tem dois campos de entrada e parte da página de HTML externa.
   >
   >
   A captura de tela a seguir mostra como o formulário é exibido em um navegador.

   ![portal](assets/portal.jpg)

   O lado esquerdo faz parte da **página HTML**. O lado direito que contém os campos é o **formulário xfa**.

1. **Acesso aos campos de formulário da página**

   Este é um exemplo de script que você pode adicionar para definir valores em um campo de formulário.

   Por exemplo, se você deseja definir a variável **EmployeeName** utilização dos valores nos Campos **Nome** e **Sobrenome**, chame o **window.formBridge.setFieldValue** função.

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
