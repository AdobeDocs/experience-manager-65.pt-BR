---
title: Limitações do Dynamic Media
description: 'Saiba mais sobre as práticas recomendadas e os limites impostos ao criar um Conjunto de imagens ou um Conjunto de rotação ou carregar um PDF. Saiba também sobre navegador da Web e combinações de sistema operacional não compatíveis com visualizadores do Dynamic Media. '
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Viewers,Image Sets,Spin Sets,eCatalog
role: User
source-git-commit: cd3dcd0232e1ecf69c79b03ab960cfbfc283ee76
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 3%

---

# Limitações do Dynamic Media

As seções a seguir descrevem as limitações no Dynamic Media.

Este tópico inclui as seguintes seções:

* Práticas recomendadas e limites impostos pela Dynamic Media sobre os tipos de ativos

<!-- * Unsupported web browser and operating system combinations for Dynamic Media Viewers -->

## Práticas recomendadas e limites impostos pela Dynamic Media sobre os tipos de ativos

Quando você cria um Conjunto de rotação ou um Conjunto de imagens, ou faz upload de PDF para extração de página, o Adobe recomenda as seguintes práticas recomendadas e impõe os seguintes limites:

| Ativo - Tipo de limite | Prática recomendada | Limite implementado | Alterações no limite de 31 de dezembro de 2022 |
| --- | --- | --- | --- |
| **Imagem** - Número de Smart Crops por imagem | 5 | 100 |  |
| **Conjunto de imagens** - Número de ativos duplicados por conjunto | Sem duplicatas | 100 | 20 |
| **Conjunto de imagens** - Número máximo de imagens por conjunto | 5 a 10 imagens por conjunto | 1000 |
| **Conjunto de rotação** - Número máximo de linhas/colunas por conjunto 2D | 12 a 18 imagens por conjunto | 1000 |
| **PDF** - Número máximo de páginas para um PDF a ser considerado para extração |  | 5000 (para novos uploads) | 100 |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

<!-- ## Unsupported web browser and operating system combinations for Dynamic Media Viewers

Dynamic Media Viewers do not support following combinations of web browser and operating system.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1 Update
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + macOS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + macOS X 10.10 Yosemite -->