---
title: Várias tendências para coleções, trechos e modelos de trechos
description: Saiba como o recurso de multitendência permite separar o conteúdo no repositório CRX com base na organização do cliente para impedir o acesso não autorizado.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---


# Multi-tenancy para coleções, snippets e modelos de snippet {#multi-tenancy-for-collections-snippets-and-snippet-templates}

O recurso de multitendência permite separar o conteúdo no CRX com base no prefixo da organização e na ID da organização para proteger o conteúdo do acesso não autorizado por usuários de outras organizações.

[!DNL Adobe Experience Manager Assets] armazena dados para cada organização em um caminho diferente. Cada caminho específico da organização é identificado pelo prefixo da organização e pela ID da organização
que está incluído no local tradicional onde diferentes tipos de ativos são armazenados no CRX.

Por exemplo, se você criar uma pasta chamada `Demo`, os ativos [!DNL Experience Manager] tradicionalmente armazenam a pasta em `../content/dam/Demo`. Com a multilocalidade ativada, agora é possível armazenar os dados em `../content/dam/<organization prefix>/<organization id>Demo`

Por exemplo, se para [!DNL Adobe Marketing Cloud] usuários de [!DNL Assets] (sob demanda) atribuídos à organização `aodpremium`, você pode usar o recurso de multitendência para configurar o caminho `../content/dam/<mac>/<aodpremium>Demo` para separar seu conteúdo. Neste exemplo, `mac` é o prefixo da organização e `aodpremium` é a ID da organização.

Com base na organização e ID do usuário, esse caminho qualificado é exibido na interface [!DNL Assets] e em vários assistentes, incluindo os assistentes de criação Mover e Snippet para aplicar a segregação.

O recurso Multi-tenancy permite separar os seguintes tipos de ativos e componentes:

* Coleções
* Coleções públicas
* Catálogos (incluindo o assistente para Adicionar/Selecionar página)
* Modelos
* Modelos de fragmento
* Lightbox
