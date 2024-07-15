---
title: Configurando seu filtro de referenciador para permitir vazio
description: Saiba mais sobre Filtro referenciador. Para permitir que o Visualizador de aplicativos para dispositivos móveis do Adobe Experience Manager (AEM) exiba aplicativos na instância do Autor, você deve definir o filtro de referenciador de HTML como 'permitir vazio'.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# Configurando seu filtro de referenciador para permitir vazio{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Para permitir que o Visualizador de aplicativos para dispositivos móveis do Adobe Experience Manager (AEM) exiba aplicativos na instância do Autor, você deve definir o filtro de referenciador de HTML como &#39;permitir vazio&#39;.

Se você não pretende usar o Visualizador de Aplicativos para revisar aplicativos nos estados de desenvolvimento e preparo, não é necessário alterar a configuração padrão do filtro referenciador.

Na instância do Autor do AEM em execução, navegue até: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) e pesquise por &quot;Filtro referenciador do Apache Sling&quot;. Clique para editar o filtro de referenciador e marque a caixa de seleção &quot;permitir vazio&quot; (consulte a imagem abaixo). Em seguida, clique no botão Salvar e feche a página do navegador.

![Configurações de Filtro do Referenciador](assets/chlimage_1-106.png)
