---
title: Configurar o filtro de referenciador para permitir vazio
seo-title: Setting Your Referrer Filter to Allow Empty
description: Siga esta página para saber mais sobre o Filtro do referenciador. Para permitir que o AEM Mobile Application Viewer exiba aplicativos na instância do Autor, será necessário definir o filtro do HTML referrer para 'permitir vazio'.
seo-description: Follow this page to learn about Referrer Filter. In order to allow the AEM Mobile Application Viewer to view apps on your Author instance, you'll need to set your HTML referrer filter to 'allow empty'.
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 3%

---

# Configurar o filtro de referenciador para permitir vazio{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Para permitir que o AEM Mobile Application Viewer exiba aplicativos na instância do Autor, será necessário definir o filtro do HTML referrer para &#39;permitir vazio&#39;.

Se você não pretende usar o Visualizador de aplicativos para revisar aplicativos em estados de desenvolvimento e de preparo, não é necessário alterar a configuração padrão do filtro referenciador.

Na instância do Autor em execução do AEM, navegue até: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) e procure por &quot;Filtro de referenciador do Apache Sling&quot;. Clique em para editar o filtro do referenciador e marque a caixa de seleção &#39;permitir vazio&#39; (veja a imagem abaixo). Em seguida, pressione o botão Save e feche a página do navegador.

![Configurações do filtro de referência](assets/chlimage_1-106.png)
