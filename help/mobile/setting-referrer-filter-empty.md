---
title: Configurando seu filtro de referenciador para permitir vazio
seo-title: Setting Your Referrer Filter to Allow Empty
description: Siga esta página para saber mais sobre o Filtro referenciador. Para permitir que o Visualizador de aplicativos da AEM Mobile exiba aplicativos na instância do Autor, será necessário definir o filtro de referenciador de HTML como "permitir vazio".
seo-description: Follow this page to learn about Referrer Filter. In order to allow the AEM Mobile Application Viewer to view apps on your Author instance, you'll need to set your HTML referrer filter to 'allow empty'.
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 3%

---

# Configurando seu filtro de referenciador para permitir vazio{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Para permitir que o Visualizador de aplicativos da AEM Mobile exiba aplicativos na instância do Autor, será necessário definir o filtro de referenciador de HTML como &quot;permitir vazio&quot;.

Se você não pretende usar o Visualizador de Aplicativos para revisar aplicativos nos estados de desenvolvimento e preparo, não é necessário alterar a configuração padrão do filtro referenciador.

Na instância do autor do AEM em execução, navegue até: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) e pesquise por &quot;Filtro referenciador do Apache Sling&quot;. Clique para editar o filtro de referenciador e marque a caixa de seleção &quot;permitir vazio&quot; (consulte a imagem abaixo). Em seguida, clique no botão Salvar e feche a página do navegador.

![Configurações do Filtro referenciador](assets/chlimage_1-106.png)
