---
title: Várias tendências para coleções, trechos e modelos de trechos
description: Saiba como o recurso de multitendência permite separar o conteúdo no repositório CRX com base na organização do cliente para impedir o acesso não autorizado.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---


# Várias tendências para coleções, trechos e modelos de trechos {#multi-tenancy-for-collections-snippets-and-snippet-templates}

O recurso de multitendência permite separar o conteúdo no CRX com base no prefixo da organização e na ID da organização para proteger o conteúdo do acesso não autorizado por usuários de outras organizações.

Os ativos Adobe Experience Manager armazenam dados para cada organização em um caminho diferente. Cada caminho específico da organização é identificado pelo prefixo da organização e pela ID da organização que é incluída no local tradicional onde tipos diferentes de ativos são armazenados no CRX.

Por exemplo, se você criar uma pasta chamada `Demo`, os ativos do Experience Manager tradicionalmente armazenam a pasta em `../content/dam/Demo`. Com a multitendência ativada, agora é possível armazenar os dados em `../content/dam/<organization prefix>/<organization id>Demo`

Por exemplo, se para [!DNL Adobe Marketing Cloud] usuários de Ativos (sob demanda) que são atribuídos à `aodpremium` organização, você pode usar o recurso de multitendência para configurar o `../content/dam/<mac>/<aodpremium>Demo` caminho para separar seu conteúdo. Neste exemplo, `mac` é o prefixo da organização e `aodpremium` é a ID da organização.

Com base na organização e na ID do usuário, esse caminho qualificado é exibido na interface de Ativos e em vários assistentes, incluindo os assistentes de criação de Mover e Snippet para aplicar a segregação.

O recurso Multi-tenancy permite separar os seguintes tipos de ativos e componentes:

* Coleções
* Coleções públicas
* Catálogos (incluindo o assistente para Adicionar/Selecionar página)
* Modelos
* Modelos de fragmento
* Lightbox
