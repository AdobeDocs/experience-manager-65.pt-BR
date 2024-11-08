---
title: Nomeação de convenções no nome do pacote Java&trade;
description: Saiba mais sobre convenções de nomenclatura e o uso de hifens no nome do pacote Java&trade;.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 1%

---

# Convenções de nomenclatura {#naming-conventions}

## Hífens no nome do pacote Java™ {#hyphens-in-java-package-name}

Ao criar um local para uma classe Java™, o nome do pacote deve corresponder ao do local da pasta do repositório com todos os hifens no caminho escapados corretamente.

Embora o uso de hifens nos nomes dos itens do repositório seja uma prática recomendada no desenvolvimento de AEM, os hifens são ilegais nos nomes dos pacotes Java™.

A plataforma subjacente do CRX deve ser capaz de distinguir entre um sublinhado real `_ ` e um hífen `-`. Portanto, no JCR, o hífen deve ser substituído pelo seu valor Unicode (u002d) e evitado com um sublinhado `_`.

Por exemplo, se o caminho do repositório for **/apps/my-example/component/info/Info.java**, o nome do pacote deverá ser `java package apps.my_002dexample.component.info;`

Observe que um sublinhado deve ser escapado da mesma forma, de modo que `_` se torne `_005f`.
