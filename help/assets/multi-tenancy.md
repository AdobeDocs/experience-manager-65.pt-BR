---
title: Multilocação para coleções, trechos e modelos de trecho
description: Saiba como o recurso de multilocação permite segregar o conteúdo no repositório CRX com base na organização do cliente para impedir o acesso não autorizado.
contentOwner: AG
role: Architect, Administrator, Leader
feature: Collections
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 1%

---


# Multilocação para coleções, trechos e modelos de trecho {#multi-tenancy-for-collections-snippets-and-snippet-templates}

O recurso de multilocação permite separar o conteúdo no CRX com base no prefixo da organização e na ID da organização para proteger o conteúdo do acesso não autorizado por usuários de outras organizações.

[!DNL Adobe Experience Manager Assets] armazena dados de cada organização em um caminho diferente. Cada caminho específico da organização é identificado pelo prefixo da organização e pela ID da organização
que está incluído no local tradicional em que diferentes tipos de ativos são armazenados no CRX.

Por exemplo, se você criar uma pasta chamada `Demo`, [!DNL Experience Manager] os ativos tradicionalmente armazenam a pasta em `../content/dam/Demo`. Com a multilocação ativada, agora é possível armazenar os dados em `../content/dam/<organization prefix>/<organization id>Demo`

Por exemplo, se para [!DNL Adobe Marketing Cloud] usuários de [!DNL Assets] (sob demanda) atribuídos à organização `aodpremium`, você pode usar o recurso de multilocação para configurar o caminho `../content/dam/<mac>/<aodpremium>Demo` para segregar seu conteúdo. Neste exemplo, `mac` é o prefixo da organização e `aodpremium` é a ID da organização.

Com base na organização e na ID do usuário, esse caminho qualificado é exibido na interface [!DNL Assets] e em vários assistentes, incluindo os assistentes de criação Mover e Snippet para aplicar a segregação.

O recurso Multilocação permite separar os seguintes tipos de ativos e componentes:

* Coleções
* Coleções públicas
* Catálogos (incluindo o assistente Adicionar/Selecionar página )
* Modelos
* Modelos de trecho
* Lightbox
