---
title: Configuração do filtro de Quem indicou para permitir vazio
seo-title: Configuração do filtro de Quem indicou para permitir vazio
description: Siga esta página para saber mais sobre o Filtro de Quem indicou. Para permitir que o AEM Mobile Application Viewer visualização aplicativos na instância do autor, é necessário definir o filtro de quem indicou HTML para 'permitir vazio'.
seo-description: Siga esta página para saber mais sobre o Filtro de Quem indicou. Para permitir que o AEM Mobile Application Viewer visualização aplicativos na instância do autor, é necessário definir o filtro de quem indicou HTML para 'permitir vazio'.
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Configuração do filtro de Quem indicou para permitir vazio{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Para permitir que o AEM Mobile Application Viewer visualização aplicativos na instância do autor, é necessário definir o filtro de quem indicou HTML para &#39;permitir vazio&#39;.

Se você não pretende usar o Application Viewer para revisar aplicativos nos estados de desenvolvimento e armazenamento temporário, não é necessário alterar a configuração padrão do filtro de quem indicou.

Na instância do autor em execução do AEM, navegue até: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) e procure por &#39;Filtro de Quem indicou Apache Sling&#39;. Clique para editar o filtro de quem indicou e marque a caixa de seleção &#39;permitir vazio&#39; (veja a imagem abaixo). Em seguida, pressione o botão salvar e feche a página do navegador.

![Configurações do filtro de quem indicou](assets/chlimage_1-106.png)
