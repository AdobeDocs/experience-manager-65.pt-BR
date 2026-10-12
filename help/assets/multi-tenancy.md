---
title: Multilocação de coleções, trechos e modelos de trecho
description: Saiba como o recurso de multilocação permite segregar o conteúdo no repositório do CRX com base na organização do cliente para impedir o acesso não autorizado.
contentOwner: AG
role: Developer, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: c73531c3-4c05-471e-beff-cefb35857910
    internal-label: Collections
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 2%
---
# Multilocação de coleções, trechos e modelos de trecho {#multi-tenancy-for-collections-snippets-and-snippet-templates}

O recurso de multilocação permite segregar o conteúdo no CRX com base no prefixo da organização e na ID da organização para proteger o conteúdo contra acesso não autorizado por usuários de outras organizações.

[!DNL Adobe Experience Manager Assets] armazena dados de cada organização em um caminho diferente. Cada caminho específico da organização é identificado pelo prefixo e pela ID da organização
que está incluído no local tradicional em que diferentes tipos de ativos são armazenados no CRX.

Por exemplo, se você criar uma pasta chamada `Demo`, o [!DNL Experience Manager] assets tradicionalmente armazena a pasta em `../content/dam/Demo`. Com a multilocação habilitada, agora você pode armazenar os dados em `../content/dam/<organization prefix>/<organization id>Demo`

Por exemplo, se para [!DNL Adobe Marketing Cloud] usuários de [!DNL Assets] (sob demanda) atribuídos à organização `aodpremium`, você pode usar o recurso de multilocação para configurar o caminho `../content/dam/<mac>/<aodpremium>Demo` para segregar seu conteúdo. Neste exemplo, `mac` é o prefixo da organização e `aodpremium` é a ID da organização.

Com base na organização e ID do usuário, esse caminho qualificado é exibido na interface [!DNL Assets] e em vários assistentes, incluindo os assistentes de criação de Movimentação e Trecho para impor a segregação.

O recurso Multilocação permite segregar os seguintes tipos de ativos e componentes:

* Coleções
* Coleções públicas
* Catálogos (incluindo o assistente Adicionar/Selecionar página)
* Modelos
* Modelos de trecho
* Lightbox
