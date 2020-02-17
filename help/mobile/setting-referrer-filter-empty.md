---
title: Configuração do filtro do referenciador para permitir vazio
seo-title: Configuração do filtro do referenciador para permitir vazio
description: Siga esta página para saber mais sobre o Filtro de referenciador. Para permitir que o AEM Mobile Application Viewer visualize aplicativos na instância do autor, é necessário definir o filtro do referenciador HTML para 'permitir vazio'.
seo-description: Siga esta página para saber mais sobre o Filtro de referenciador. Para permitir que o AEM Mobile Application Viewer visualize aplicativos na instância do autor, é necessário definir o filtro do referenciador HTML para 'permitir vazio'.
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuração do filtro do referenciador para permitir vazio{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>A Adobe recomenda usar o Editor SPA para projetos que exigem renderização do lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Para permitir que o AEM Mobile Application Viewer visualize aplicativos na instância do autor, é necessário definir o filtro do referenciador HTML para &#39;permitir vazio&#39;.

Se você não pretende usar o Application Viewer para revisar aplicativos nos estados de desenvolvimento e armazenamento temporário, não é necessário alterar a configuração padrão do filtro de referenciador.

Na instância do autor em execução do AEM, navegue até: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) e pesquise por &quot;Apache Sling Referrer Filter&quot;. Clique para editar o filtro do referenciador e marque a caixa de seleção &#39;permitir vazio&#39; (veja a imagem abaixo). Em seguida, pressione o botão salvar e feche a página do navegador.

![Configurações do filtro do referenciador](assets/chlimage_1-106.png)
