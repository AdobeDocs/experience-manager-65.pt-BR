---
title: Criação de layout personalizado da barra de ferramentas
seo-title: Creating custom toolbar layout
description: É possível especificar um layout da barra de ferramentas para o formulário. O layout da barra de ferramentas define os comandos e o layout da barra de ferramentas no formulário.
seo-description: You can specify a toolbar layout for the form. The toolbar layout defines the commands and the layout of the toolbar on the form.
uuid: 389a715a-4c91-4a63-895d-bb2d0f1054eb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 0d817a7e-2758-4308-abda-6194716c2d97
docset: aem65
exl-id: 44516956-00aa-41d5-a7e9-746c7618e5db
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Criação de layout personalizado da barra de ferramentas{#creating-custom-toolbar-layout}

## Layouts da barra de ferramentas {#layout}

Ao criar um formulário adaptável, é possível especificar um layout da barra de ferramentas para o formulário. O layout da barra de ferramentas define os comandos e o layout da barra de ferramentas no formulário.

O layout da barra de ferramentas depende muito do processamento no lado do cliente impulsionado por códigos complexos de JavaScript e CSS. Organizar e otimizar a veiculação desse código pode ser um problema complicado. Para ajudar a lidar com esse problema, o AEM fornece Pastas de biblioteca do lado do cliente, que permitem armazenar o código do lado do cliente no repositório, organizá-lo em categorias e definir quando e como cada categoria de código deve ser apresentada ao cliente. O sistema de biblioteca do lado do cliente cuida da produção dos links corretos na página da Web final para carregar o código correto. Para obter informações detalhadas, consulte [Como as bibliotecas do lado do cliente funcionam no AEM.](/help/sites-developing/clientlibs.md)

![Layout de exemplo da barra de ferramentas](assets/default_toolbar_layout.png)

Layout de exemplo da barra de ferramentas

Os formulários adaptáveis fornecem um conjunto de layouts prontos para uso:

![Layouts de barra de ferramentas disponíveis prontos para uso ](assets/toolbar1.png)

Layouts de barra de ferramentas disponíveis prontos para uso

Além disso, é possível criar um layout personalizado da barra de ferramentas.

O procedimento a seguir detalha as etapas para criar uma barra de ferramentas personalizada que exibe três ações na barra de ferramentas e as outras ações em uma lista suspensa na barra de ferramentas.

O pacote de conteúdo anexado contém o código inteiro descrito abaixo. Após instalar o pacote de conteúdo, abra `/content/forms/af/CustomLayoutDemo.html` para exibir a demonstração do layout personalizado da barra de ferramentas.

CustomToolbarLayoutDemo.zip

[Obter arquivo](assets/customtoolbarlayoutdemo.zip)
Layout da barra de ferramentas personalizada de demonstração

## Para criar um layout personalizado da barra de ferramentas {#layout-1}

1. Crie uma pasta para manter os layouts personalizados da barra de ferramentas. Por exemplo:

   `/apps/customlayout/toolbar`.

   Para criar um layout personalizado, você pode usar (e personalizar) um dos layouts predefinidos da barra de ferramentas disponíveis na seguinte pasta:

   `/libs/fd/af/layouts/toolbar`

   Por exemplo, copie a variável `mobileFixedToolbarLayout` nó a partir do `/libs/fd/af/layouts/toolbar` para `/apps/customlayout/toolbar` pasta.

   Além disso, copie a barra de ferramentasCommon.jsp para o `/apps/customlayout/toolbar` pasta.

   >[!NOTE]
   >
   >A pasta que você cria para manter os layouts personalizados pode ser criada com o `apps` pasta.

1. Renomeie o nó copiado, `mobileFixedToolbarLayout`para `customToolbarLayout.`

   Além disso, forneça uma descrição relevante para o nó. Por exemplo, altere jcr:description do nó para **Layout personalizado para a barra de ferramentas**.

   O `guideComponentType` a propriedade do nó determina o tipo de layout. Nesse caso, o tipo de layout é a barra de ferramentas, portanto, ele aparece na lista suspensa de seleção do layout da barra de ferramentas.

   ![Um nó com descrição relevante](assets/toolbar3.png)

   Um nó com descrição relevante

   O novo layout personalizado da barra de ferramentas é exibido no **Barra de ferramentas de formulário adaptável** configuração da caixa de diálogo.

   ![Lista de layouts disponíveis da barra de ferramentas](assets/toolbar4.png)

   Lista de layouts disponíveis da barra de ferramentas

   >[!NOTE]
   >
   >A descrição atualizada na etapa anterior é exibida na lista suspensa Layout .

1. Selecione este layout personalizado da barra de ferramentas e clique em OK.

   Adicione clientlib (javascript e css) na `/etc/customlayout` e incluir a referência da clientlib na `customToolbarLayout.jsp`.

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
   >Adicione a classe da barra de ferramentas de guia para o layout. O estilo pronto para uso da barra de ferramentas é definido em relação à classe da barra de ferramentas de guidetolbar.

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
>A descrição atualizada na etapa anterior é exibida na lista suspensa Layout .

![Exibição de desktop da barra de ferramentas de layout personalizada](assets/toolbar_1.png)

Exibição de desktop da barra de ferramentas de layout personalizada
