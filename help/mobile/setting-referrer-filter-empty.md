---
title: Configurando seu filtro de referenciador para permitir vazio
description: Saiba mais sobre Filtro referenciador. Para permitir que o Visualizador de aplicativos para dispositivos móveis do Adobe Experience Manager (AEM) exiba aplicativos na instância do Autor, você deve definir o filtro do referenciador do HTML como "permitir vazio".
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
solution: Experience Manager
feature: Mobile
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%
---
# Configurando seu filtro de referenciador para permitir vazio{#setting-your-referrer-filter-to-allow-empty}

{{ue-over-mobile}}

Para permitir que o Visualizador de aplicativos para dispositivos móveis do Adobe Experience Manager (AEM) exiba aplicativos na instância do Autor, você deve definir o filtro do referenciador do HTML como &quot;permitir vazio&quot;.

Se você não pretende usar o Visualizador de Aplicativos para revisar aplicativos nos estados de desenvolvimento e preparo, não é necessário alterar a configuração padrão do filtro referenciador.

Na instância do Autor do AEM em execução, navegue até: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) e pesquise por &quot;Filtro do referenciador Apache Sling&quot;. Clique para editar o filtro de referenciador e marque a caixa de seleção &quot;permitir vazio&quot; (consulte a imagem abaixo). Em seguida, clique no botão Salvar e feche a página do navegador.

![Configurações de Filtro do Referenciador](assets/chlimage_1-106.png)
