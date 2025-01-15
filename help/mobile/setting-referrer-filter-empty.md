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
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Configurando seu filtro de referenciador para permitir vazio{#setting-your-referrer-filter-to-allow-empty}

{{ue-over-mobile}}

Para permitir que o Visualizador de aplicativos para dispositivos móveis do Adobe Experience Manager (AEM) exiba aplicativos na instância do Autor, você deve definir o filtro de referenciador de HTML como &#39;permitir vazio&#39;.

Se você não pretende usar o Visualizador de Aplicativos para revisar aplicativos nos estados de desenvolvimento e preparo, não é necessário alterar a configuração padrão do filtro referenciador.

Na instância do Autor do AEM em execução, navegue até: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) e pesquise por &quot;Filtro referenciador do Apache Sling&quot;. Clique para editar o filtro de referenciador e marque a caixa de seleção &quot;permitir vazio&quot; (consulte a imagem abaixo). Em seguida, clique no botão Salvar e feche a página do navegador.

![Configurações de Filtro do Referenciador](assets/chlimage_1-106.png)
