---
title: Várias tendências para coleções, trechos e modelos de trechos
description: Saiba como o recurso de multitendência permite separar o conteúdo no repositório CRX com base na organização do cliente para impedir o acesso não autorizado.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Várias tendências para coleções, trechos e modelos de trechos {#multi-tenancy-for-collections-snippets-and-snippet-templates}

O recurso de multitendência permite separar o conteúdo no CRX com base no prefixo da organização e na ID da organização para proteger o conteúdo do acesso não autorizado por usuários de outras organizações.

O Adobe Experience Manager (AEM) Assets armazena dados para cada organização em um caminho diferente. Cada caminho específico da organização é identificado pelo prefixo da organização e pela ID da organização que é incluída no local tradicional onde tipos diferentes de ativos são armazenados no CRX.

Por exemplo, se você criar uma pasta chamada `Demo`, os ativos AEM tradicionalmente armazenam a pasta em `../content/dam/Demo`. Com a multitendência ativada, agora é possível armazenar os dados em `../content/dam/<organization prefix>/<organization id>Demo`

Por exemplo, se para [!DNL Adobe Marketing Cloud] usuários do AEM Assets (sob demanda) que são atribuídos à `aodpremium` organização, você pode usar o recurso de multitendência para configurar o `../content/dam/<mac>/<aodpremium>Demo` caminho para separar seu conteúdo. Neste exemplo, `mac` é o prefixo da organização e `aodpremium` é a ID da organização.

Com base na organização e na ID do usuário, esse caminho qualificado é exibido na interface dos ativos AEM e em vários assistentes, incluindo os assistentes de criação Mover e Snippet para aplicar a segregação.

O recurso Multi-tenancy permite separar os seguintes tipos de ativos e componentes:

* Coleções
* Coleções públicas
* Catálogos (incluindo o assistente para Adicionar/Selecionar página)
* Modelos
* Modelos de fragmento
* Lightbox
