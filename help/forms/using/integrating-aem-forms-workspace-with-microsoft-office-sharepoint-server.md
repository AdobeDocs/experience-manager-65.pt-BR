---
title: Integração da área de trabalho de formulários AEM com o Microsoft Office SharePoint Server
seo-title: Integração da área de trabalho de formulários AEM com o Microsoft Office SharePoint Server
description: 'É possível integrar AEM espaço de trabalho de formulários com o Microsoft Office SharePoint Server. '
seo-description: 'É possível integrar AEM espaço de trabalho de formulários com o Microsoft Office SharePoint Server. '
uuid: 69d51bdf-729f-4eea-8fae-1e2b8aacaae6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8990b422-f4f6-4080-871a-33cdf7ca6455
docset: aem65
translation-type: tm+mt
source-git-commit: 21623c615ebe69226cfaf84baf4cfb1717b449f4
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---


# Integração AEM espaço de trabalho de formulários com o Microsoft Office SharePoint Server{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**- Requisitos**

**Pré-requisito**
conhecimentoAntes de poder adicionar o AEM Forms Workspace ao SharePoint Server, tem de ter acesso ao SharePoint Server com os privilégios adequados e tem de saber o URL para aceder ao Workspace. As etapas abaixo pressupõem que você tenha conhecimento do SharePoint Server. Para obter mais informações sobre Web Parts no SharePoint Server, consulte Web Parts no Windows SharePoint Services.

**User**
levelBeginning

Você pode usar o AEM Forms Workspace como uma Web Part no Microsoft Office SharePoint Server (por exemplo, Microsoft Office SharePoint Server 2007). Os usuários podem acessar o AEM Forms Workspace se conectarem ao seu SharePoint Server usando um navegador da Web para fornecer uma experiência unificada. Neste artigo, você aprenderá as etapas básicas para exibir o AEM Forms Workspace como uma Web Part no Microsoft Office SharePoint Server. Você pode executar as etapas descritas neste artigo para fornecer uma experiência unificada para que os usuários que se conectam ao seu servidor SharePoint possam acessar o AEM Forms Workspace a partir da mesma porta.

>[!NOTE]
>
>As etapas listadas neste artigo são específicas do Microsoft SharePoint Server 2007. Você também pode configurar o HTML Workspace com outras versões compatíveis do Microsoft SharePoint.

## Integrar o AEM Forms Workspace ao Microsoft Office SharePoint Server 2007 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

Execute as seguintes etapas para integrar o AEM Forms Workspace a uma Web Part:

1. Em um navegador da Web, navegue até o site do SharePoint, como `https://[myMOSSserver]:44299/default.aspx`, onde `[myMOSSserver]` é o nome ou o endereço IP do servidor Sharepoint.

   >[!NOTE]
   >
   >44299 é o número de porta padrão para o servidor SharePoint. O número da porta depende da instalação do SharePoint Server.

1. No lado superior direito da página da Web, clique em **Ações do site** e selecione **Editar página**.
1. Clique no botão **Adicionar uma Web Part**.
1. Na caixa de diálogo Adicionar Web Parts - caixa de diálogo da página da Web, em Miscelânea, selecione **Web Part do Visualizador de Página** e clique em **Adicionar**.
1. Na caixa Web Part do Visualizador de páginas, clique em **edit** e selecione **Modificar Web Part compartilhada**.

   >[!NOTE]
   >
   >A caixa Web Part do Visualizador de páginas é exibida sob o botão **Adicionar uma Web Part** que você clicou na etapa 3, conforme mostrado na ilustração a seguir (Figura 1):

   ![Caixa de Web Part do Visualizador de Página no Microsoft Office SharePoint Server.](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   Figura 1. - A caixa Web Part do Visualizador de Página no servidor do Microsoft Office SharePoint.

1. Na página Visualizador de páginas, execute as seguintes tarefas:

   1. Na caixa Link, digite o URL do AEM Forms Workspace, como `https://[AEM_forms_Server]:8080/lc/ws` onde `[AEM_forms_Server]` representa o IP ou o Nome do servidor de formulários AEM.
   1. Clique em **Aparência** e modifique a altura, a largura e o título para que você possa ver toda a interface do usuário do Workspace. Por exemplo, é possível definir a altura e a largura como 6 polegadas e 11 polegadas, respectivamente.
   1. Clique em **Testar link**. Uma nova janela do navegador da Web é exibida com o Workspace exibido.
   1. (Opcional) Clique em **Layout** e modifique o layout do Workspace na Web Part.
   1. (Opcional) Clique em **Avançado** e modifique outras configurações, como a descrição e se o Workspace pode ser minimizado ou fechado na Web Part.

      Clique em **Aplicar**.

1. Clique em **Sair do Modo de edição** e verifique se você pode acessar o Workspace.

Após concluir as etapas acima, seu site do SharePoint será semelhante à ilustração a seguir (Figura 2):

![AEM Forms Workspace integrado ao Microsoft Office SharePoint Server](assets/aem-forms-workspace.jpg)

Figura 2: AEM Forms Workspace integrado ao Microsoft Office SharePoint Server

