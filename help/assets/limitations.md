---
title: Limitações do Dynamic Media
description: Saiba mais sobre as práticas recomendadas e os limites impostos ao criar um Conjunto de imagens ou um Conjunto de rotação ou carregar um PDF. Saiba mais sobre combinações incompatíveis de navegador da Web e sistema operacional para o Dynamic Media.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Image Sets,Spin Sets,eCatalog
role: User
exl-id: e4d4059e-ac0b-42e7-910c-001310796574
source-git-commit: 886edbf0e98f5cdee176aaa0a7dffcf18b1a7cc2
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 2%

---

# Limitações do Dynamic Media

As seções a seguir descrevem as limitações do Dynamic Media.

Este tópico inclui as seguintes seções:

* [Práticas recomendadas e limites impostos pela Dynamic Media em tipos de ativos](#best-practice-enforced-limits)
* [Combinações de navegador da Web e sistema operacional não compatíveis com o Dynamic Media](#unsupported-browser-os)

## Práticas recomendadas e limites impostos pela Dynamic Media em tipos de ativos {#best-practice-enforced-limits}

Ao criar um Conjunto de rotação ou um Conjunto de imagens, ou fazer upload de PDF para extração de página, o Adobe recomenda as seguintes práticas recomendadas e impõe os seguintes limites:

| Ativo - Tipo de limite | Prática recomendada | Limite imposto |
| --- | --- | --- |
| **Imagem** - Número de cortes inteligentes por imagem | 5 | 100 |
| **Todos os conjuntos** - Número de ativos duplicados por conjunto | Sem duplicatas | 20‡ |
| **Todos os conjuntos** - Número máximo de ativos por conjunto | De 5 a 10 imagens por conjunto | 1000 |
| **Grupo de rotação** - Número máximo de linhas/colunas por conjunto 2D | 12 a 18 imagens por conjunto | 1000 |
| **PDF** - Número máximo de páginas para um PDF a ser considerado para extração |  | 100 (para todos os PDF) |

‡ A prática recomendada é não ter ativos duplicados em um conjunto. O limite é de 20 duplicatas para um único ativo. Se você adicionar outra duplicata para esse ativo — dentro desse conjunto — a solicitação retornará um erro ou ignorará a duplicata.
<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Combinações de navegador da Web e sistema operacional não compatíveis com o Dynamic Media {#unsupported-browser-os}

O Dynamic Media não oferece suporte às seguintes combinações de navegador da Web e sistema operacional.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Atualização do Windows Phone 8.1
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite

## Fim do suporte para Secure Socket Layer 2.0 e 3.0 e Transport Layer Security 1.0 e 1.1 {#tls}

<!-- CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022) -->

A partir de 30 de abril de 2024, o Adobe Dynamic Media encerrará o suporte para o seguinte:

* SSL (Secure Socket Layer) 2.0
* SSL 3.0
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

