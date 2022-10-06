---
title: Limitações do Dynamic Media
description: Saiba mais sobre as práticas recomendadas e os limites impostos ao criar um Conjunto de imagens ou um Conjunto de rotação ou carregar um PDF. Saiba também sobre navegador da Web e combinações de sistema operacional não compatíveis com visualizadores do Dynamic Media.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Viewers,Image Sets,Spin Sets,eCatalog
role: User
exl-id: e4d4059e-ac0b-42e7-910c-001310796574
source-git-commit: 098c52720d08ad294a745addb8bd3ca3f1c63b5c
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 5%

---

# Limitações do Dynamic Media

As seções a seguir descrevem as limitações no Dynamic Media.

Este tópico inclui as seguintes seções:

* [Práticas recomendadas e limites impostos pela Dynamic Media sobre os tipos de ativos](#best-practice-enforced-limits)
* [Navegador da Web não suportado e combinações de sistema operacional para Visualizadores do Dynamic Media](#unsupported-browser-os)

## Práticas recomendadas e limites impostos pela Dynamic Media sobre os tipos de ativos {#best-practice-enforced-limits}

Quando você cria um Conjunto de rotação ou um Conjunto de imagens, ou faz upload de PDF para extração de página, o Adobe recomenda as seguintes práticas recomendadas e impõe os seguintes limites:

| Ativo - Tipo de limite | Prática recomendada | Limite imposto | Alteração do limite em 31 de dezembro de 2022 |
| --- | --- | --- | --- |
| **Imagem** - Número de Smart Crops por imagem | 5 | 100 | 20 |
| **Todos os conjuntos** - Número de ativos duplicados por conjunto | Sem duplicatas | 20º | Não aplicável |
| **Todos os conjuntos** - Número máximo de ativos por conjunto | 5 a 10 imagens por conjunto | 1000 | Não aplicável |
| **Conjunto de rotação** - Número máximo de linhas/colunas por conjunto 2D | 12 a 18 imagens por conjunto | 1000 | Não aplicável |
| **PDF** - Número máximo de páginas para um PDF a ser considerado para extração |  | 5000 (para novos uploads) | 100 (para todos os PDF) |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Navegador da Web não suportado e combinações de sistema operacional para Visualizadores do Dynamic Media {#unsupported-browser-os}

Os visualizadores do Dynamic Media não são compatíveis com as seguintes combinações de navegador da Web e sistema operacional.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Atualização do Internet Explorer 11 + Windows Phone 8.1
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite

## Fim de suporte para TLS 1.0 e 1.1 {#tls}

<!-- CQDOC-19433 -->

A partir de 30 de setembro de 2022, os visualizadores do Adobe Dynamic Media encerrarão o suporte para o seguinte:

* TLS (Transport Layer Security) 1.0 e 1.1
* As seguintes cifras fracas no TLS 1.2:
   * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
   * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
   * `TLS_RSA_WITH_AES_256_GCM_SHA384`
   * `TLS_RSA_WITH_AES_256_CBC_SHA256`
   * `TLS_RSA_WITH_AES_256_CBC_SHA`
   * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
   * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
   * `TLS_RSA_WITH_AES_128_GCM_SHA256`
   * `TLS_RSA_WITH_AES_128_CBC_SHA256`
   * `TLS_RSA_WITH_AES_128_CBC_SHA`
   * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
   * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
   * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
   * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

