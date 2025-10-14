---
title: Criar layout personalizado da barra de ferramentas
description: Você pode especificar um layout de barra de ferramentas para o formulário. O layout da barra de ferramentas define os comandos e o layout da barra de ferramentas no formulário.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 44516956-00aa-41d5-a7e9-746c7618e5db
solution: "Experience Manager, Experience Manager Forms"
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 5723e9990969dff1b508062d69a68f68a20eb576
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# Criar layout personalizado da barra de ferramentas{#creating-custom-toolbar-layout}

## Layouts da barra de ferramentas {#layout}

Ao criar um formulário adaptável, você pode especificar um layout de barra de ferramentas para o formulário. O layout da barra de ferramentas define os comandos e o layout da barra de ferramentas no formulário.

O layout da barra de ferramentas usa muito o processamento do lado do cliente orientado por códigos JavaScript e CSS complexos. Organizar e otimizar a veiculação desse código pode ser um problema complicado. Para ajudar a lidar com esse problema, o AEM fornece Pastas de bibliotecas do lado do cliente, que permitem armazenar o código do lado do cliente no repositório, organizá-lo em categorias e definir quando e como cada categoria de código deve ser entregue ao cliente. O sistema de biblioteca do lado do cliente cuida de produzir os links corretos na página da Web final para carregar o código correto. Para obter informações detalhadas, consulte [Como as bibliotecas do lado do cliente funcionam no AEM.](/help/sites-developing/clientlibs.md)

![Exemplo de layout da barra de ferramentas](assets/default_toolbar_layout.png)

Exemplo de layout da barra de ferramentas

Os formulários adaptáveis fornecem um conjunto de layouts prontos para uso:

![Layouts de barra de ferramentas disponíveis prontamente &#x200B;](assets/toolbar1.png)

Layouts de barra de ferramentas disponíveis prontos para uso

Além disso, você pode criar um layout de barra de ferramentas personalizado.

O procedimento a seguir detalha as etapas para criar uma barra de ferramentas personalizada que exibe três ações na barra de ferramentas e as outras ações em uma lista suspensa na barra de ferramentas.

O pacote de conteúdo anexado contém o código inteiro descrito abaixo. Após instalar o pacote de conteúdo, abra `/content/forms/af/CustomLayoutDemo.html` para ver a demonstração de layout de barra de ferramentas personalizada.

CustomToolbarLayoutDemo.zip

[Obter arquivo](assets/customtoolbarlayoutdemo.zip)
Demonstração do layout personalizado da barra de ferramentas

## Para criar um layout personalizado da barra de ferramentas {#layout-1}

1. Crie uma pasta para manter os layouts personalizados da barra de ferramentas. Por exemplo:

   `/apps/customlayout/toolbar`.

   Para criar um layout personalizado, você pode usar (e personalizar) um dos layouts predefinidos da barra de ferramentas disponíveis na seguinte pasta:

   `/libs/fd/af/layouts/toolbar`

   Por exemplo, copie o nó `mobileFixedToolbarLayout` da pasta `/libs/fd/af/layouts/toolbar` para a pasta `/apps/customlayout/toolbar`.

   Além disso, copie toolbarCommon.jsp para a pasta `/apps/customlayout/toolbar`.

   >[!NOTE]
   >
   >A pasta criada para manter os layouts personalizados pode ser criada com a pasta `apps`.

1. Renomear o nó copiado, `mobileFixedToolbarLayout`, para `customToolbarLayout.`

   Além disso, forneça uma descrição relevante para o nó. Por exemplo, altere o jcr:description do nó para **Layout personalizado da barra de ferramentas**.

   A propriedade `guideComponentType` do nó determina o tipo de layout. Nesse caso, o tipo de layout é barra de ferramentas, portanto, ele aparece na lista suspensa de seleção de layout da barra de ferramentas.

   ![Um nó com descrição relevante](assets/toolbar3.png)

   Um nó com descrição relevante

   O novo layout personalizado da barra de ferramentas é exibido na configuração da caixa de diálogo **Barra de Ferramentas do Formulário Adaptável**.

   ![Lista de layouts disponíveis da barra de ferramentas](assets/toolbar4.png)

   Lista de layouts disponíveis da barra de ferramentas

   >[!NOTE]
   >
   >A descrição atualizada na etapa anterior é exibida na lista suspensa Layout.

1. Selecione este layout personalizado da barra de ferramentas e clique em OK.

   Adicione clientlib (javascript e css) no nó `/etc/customlayout` e inclua a referência a clientlib no `customToolbarLayout.jsp`.

   ![Caminho do arquivo customToolbarLayout.css](assets/toolbar_3.png)

   Caminho do arquivo customToolbarLayout.css

   Amostra `customToolbarLayout.jsp`:

   ```jsp
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <cq:includeClientLib categories="customtoolbarlayout" />
   <c:if test="${isEditMode}">
           <cq:includeClientLib categories="customtoolbarlayoutauthor" />
   </c:if>
   <div class="guidetoolbar mobileToolbar mobilecustomToolbar" data-guide-position-class="guide-element-hide">
       <div data-guide-scroll-indicator="true"></div>
       <%@include file="../toolbarCommon.jsp" %>
   </div>
   ```

   >[!NOTE]
   >
   >Adicione a classe da barra de ferramentas do guia para o layout. O estilo pronto para uso da barra de ferramentas é definido em relação à classe da barra de ferramentas do guia.

   Amostra `toolBarCommon.jsp`:

   ```jsp
   <%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions"%>
   <%--------------------
   This code iterates over all the tool bar items using the guideToolbar bean.
   If the number of toolbar items are more than 3, then we create a dropdown menu using bootstrap for other actions present in the toolbar.
   In both desktop and mobile devices, the layout is different.
   ---------------------------------%>
   
   <c:forEach items="${guideToolbar.items}" var="toolbarItem" varStatus="loop">
       <c:choose>
         <c:when test="${loop.index gt 2}">
      <c:choose>
       <c:when test="${loop.index eq 3}">
                     <div class="btn-group dropdown">
                       <button type="button" class="btn btn-primary dropdown-toggle label" data-toggle="dropdown">Actions <span class="caret"></code></button>
                       <button type="button" class="btn btn-primary dropdown-toggle icon" data-toggle="dropdown"><span class="glyphicon glyphicon-th-list"></code></button>
             <ul class="dropdown-menu" role="menu">
                           <li>
                               <div id="${toolbarItem.id}_guide-item">
                                 <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
                              </div>
                           </li>
                           <c:if test="${loop.index eq (fn:length(guideToolbar.items)-1)}">
                                </ul>
                                </div>
                           </c:if>
       </c:when>
       <c:when test="${loop.index eq (fn:length(guideToolbar.items)-1)}">
                          <li>
                                     <div id="${toolbarItem.id}_guide-item">
                                         <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
                                     </div>
                           </li>
                       </ul>
                     </div>
   
       </c:when>
       <c:otherwise>
         <li>
          <div id="${toolbarItem.id}_guide-item">
           <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
          </div>
         </li>
       </c:otherwise>
      </c:choose>
         </c:when>
         <c:otherwise>
     <div id="${toolbarItem.id}_guide-item">
           <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
        </div>
         </c:otherwise>
    </c:choose>
   </c:forEach>
   ```

   O CSS presente no nó clientlib:

   ```css
   .mobilecustomToolbar .dropdown {
       display: inline-block;
   }
   
   .mobilecustomToolbar .dropdown {
       float: right;
   }
   
   .mobilecustomToolbar .dropdown > button {
      padding: 6px 12px;
   }
   
   .mobilecustomToolbar .dropdown .guideFieldWidget, .mobilecustomToolbar .dropdown .guideFieldWidget button {
       width: 100%;
   }
   
   .mobilecustomToolbar .dropdown .caret{
       border-bottom: 6px solid;
       border-right: 6px solid transparent;
       border-left: 6px solid transparent;
    border-top: transparent;
   }
   
   .mobilecustomToolbar .dropdown-menu{
    top: auto;
    bottom: 100%;
   }
   
   .mobilecustomToolbar .btn-group {
    vertical-align: super;
   }
   
   .mobilecustomToolbar .glyphicon {
    font-size: 24px;
   }
   
   @media (max-width: 767px){
   
    .mobilecustomToolbar .dropdown .guideButton .iconButton-icon {
      display: none;
       }
   
       .mobilecustomToolbar .dropdown .guideButton .iconButton-label {
      display: inline-block;
       }
   
       .mobilecustomToolbar .dropdown .guideButton button {
      background-color: #013853;
       }
   
    .mobilecustomToolbar .btn-group {
     vertical-align: top;
    }
   
   }
   ```

>[!NOTE]
>
>A descrição atualizada na etapa anterior é exibida na lista suspensa Layout.

![Modo de exibição de área de trabalho da barra de ferramentas de layout personalizada](assets/toolbar_1.png)

Exibição de desktop da barra de ferramentas de layout personalizado
