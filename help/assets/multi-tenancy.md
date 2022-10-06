---
title: Multilocação para coleções, trechos e modelos de trecho
description: Saiba como o recurso de multilocação permite segregar o conteúdo no repositório CRX com base na organização do cliente para impedir o acesso não autorizado.
contentOwner: AG
role: Architect, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---

# Multilocação para coleções, trechos e modelos de trecho {#multi-tenancy-for-collections-snippets-and-snippet-templates}

O recurso de multilocação permite separar o conteúdo no CRX com base no prefixo da organização e na ID da organização para proteger o conteúdo do acesso não autorizado por usuários de outras organizações.

[!DNL Adobe Experience Manager Assets] armazena dados de cada organização em um caminho diferente. Cada caminho específico da organização é identificado pelo prefixo da organização e pela ID da organização incluída no local tradicional em que diferentes tipos de ativos são armazenados no CRX.

Por exemplo, se você criar uma pasta chamada `Demo`, [!DNL Experience Manager] os ativos tradicionalmente armazenam a pasta em `../content/dam/Demo`. Com a multilocação ativada, agora é possível armazenar os dados em `../content/dam/<organization prefix>/<organization id>Demo`

Por exemplo, se for [!DNL Adobe Marketing Cloud] usuários de [!DNL Assets] (sob demanda) atribuído ao `aodpremium` organização, você pode usar o recurso de multilocação para configurar `../content/dam/<mac>/<aodpremium>Demo` caminho para segregar seu conteúdo. Neste exemplo, `mac` é o prefixo da organização e `aodpremium` é a ID da organização.

Com base na organização e na ID do usuário, esse caminho qualificado é exibido na variável [!DNL Assets] e vários assistentes, incluindo os assistentes de criação Mover e Snippet para aplicar a segregação.

O recurso Multilocação permite separar os seguintes tipos de ativos e componentes:

* Coleções
* Coleções públicas
* Catálogos (incluindo o assistente Adicionar/Selecionar página )
* Modelos
* Modelos de trecho
* Lightbox
