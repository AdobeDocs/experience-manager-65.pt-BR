---
title: Multilocação de coleções, trechos e modelos de trecho
description: Saiba como o recurso de multilocação permite segregar o conteúdo no repositório do CRX com base na organização do cliente para impedir o acesso não autorizado.
contentOwner: AG
role: Developer, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

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
