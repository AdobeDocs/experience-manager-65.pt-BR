---
title: Integrando AEM espaço de trabalho de formulários com o Microsoft Office SharePoint Server
seo-title: Integrating AEM forms workspace with Microsoft Office SharePoint Server
description: É possível integrar AEM espaço de trabalho de formulários com o Microsoft Office SharePoint Server.
seo-description: You can integrate AEM forms workspace with Microsoft Office SharePoint Server.
uuid: 69d51bdf-729f-4eea-8fae-1e2b8aacaae6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8990b422-f4f6-4080-871a-33cdf7ca6455
docset: aem65
exl-id: d080932f-d5fb-482d-9329-62da5df10362
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Integrando AEM espaço de trabalho de formulários com o Microsoft Office SharePoint Server{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**- Requisitos**

**Conhecimento pré-requisito**
Antes de adicionar o AEM Forms Workspace ao SharePoint Server, você deve ter acesso ao SharePoint Server com os privilégios apropriados e saber o URL para acessar o Workspace. As etapas abaixo pressupõem que você tenha conhecimento do SharePoint Server. Para obter mais informações sobre Web Parts no SharePoint Server, consulte Web Parts no Windows SharePoint Services.

**Nível do usuário**
Início

Você pode usar o AEM Forms Workspace como uma Web Part no Microsoft Office SharePoint Server (Por exemplo, Microsoft Office SharePoint Server 2007). Os usuários podem acessar o AEM Forms Workspace se conectarem ao seu servidor SharePoint por meio de um navegador da Web para fornecer uma experiência unificada. Neste artigo, você aprenderá as etapas básicas para exibir o AEM Forms Workspace como uma Web Part no Microsoft Office SharePoint Server. Você pode executar as etapas descritas neste artigo para fornecer uma experiência unificada para que os usuários que se conectam ao seu servidor do SharePoint possam acessar o AEM Forms Workspace a partir da mesma porta.

>[!NOTE]
>
>As etapas listadas neste artigo são específicas do Microsoft SharePoint Server 2007. Você também pode configurar o HTML Workspace com outras versões compatíveis do Microsoft SharePoint.

## Integrar o AEM Forms Workspace com o Microsoft Office SharePoint Server 2007 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

Execute as seguintes etapas para integrar o AEM Forms Workspace a uma Web Part:

1. Em um navegador da Web, navegue até o site do SharePoint como `https://[myMOSSserver]:44299/default.aspx` em que `[myMOSSserver]` é o nome ou o endereço IP do servidor Sharepoint.

   >[!NOTE]
   >
   >44299 é o número padrão da porta para o servidor SharePoint. O número da porta depende da instalação do SharePoint Server.

1. No lado superior direito da página da Web, clique em **Ações do site** e selecione **Editar página**.
1. Clique no botão **Adicionar uma Web Part** botão.
1. Na caixa de diálogo Adicionar Web Parts - página da Web, em Miscelânea, selecione **Web Part do Visualizador de Páginas** e, em seguida, clique em **Adicionar**.
1. Na caixa Peça Web do Visualizador de Páginas, clique em **editar** e selecione **Modificar Web Part Partilhada**.

   >[!NOTE]
   >
   >A caixa Peça Web do Visualizador de Páginas é exibida abaixo do **Adicionar uma Web Part** botão que você clicou na etapa 3, conforme mostrado na ilustração a seguir (Figura 1):

   ![Caixa Web Part do Visualizador de Página no servidor Microsoft Office SharePoint.](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   Figura 1. - A caixa Peça Web do Visualizador de Páginas no servidor Microsoft Office SharePoint.

1. Na página Visualizador de páginas, execute as seguintes tarefas:

   1. Na caixa Link, digite o URL do AEM Forms Workspace, como `https://[AEM_forms_Server]:8080/lc/ws` em que `[AEM_forms_Server]` representa o IP ou o Nome do servidor de formulários AEM.
   1. Clique em **Aparência** e modifique a altura, a largura e o título para que você possa ver toda a interface do usuário do Workspace. Por exemplo, é possível definir a altura e a largura como 6 polegadas e 11 polegadas, respectivamente.
   1. Clique em **Testar link**. Uma nova janela do navegador da Web é exibida com o Workspace exibido nela.
   1. (Opcional) Clique em **Layout** e modifique o layout do Workspace em Web Part.
   1. (Opcional) Clique em **Avançado** e modifique outras configurações, como a descrição e se o Workspace pode ser minimizado ou fechado na Web Part.

      Clique em **Aplicar**.

1. Clique em **Sair do modo de edição** e verifique se você pode acessar o Workspace.

Após concluir as etapas acima, seu site do SharePoint é semelhante à seguinte ilustração (Figura 2):

![AEM Forms Workspace integrado ao Microsoft Office SharePoint Server](assets/aem-forms-workspace.jpg)

Figura 2: Espaço de trabalho do AEM Forms integrado ao Microsoft Office SharePoint Server
