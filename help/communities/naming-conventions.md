---
title: Nomeação de convenções no nome do pacote Java&trade;
description: Saiba mais sobre as convenções de nomenclatura e o uso de hifens no nome do pacote Java&trade;.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 1%
---
# Convenções de nomenclatura {#naming-conventions}

## Hífens no nome do pacote Java™ {#hyphens-in-java-package-name}

Ao criar um local para uma classe Java™, o nome do pacote deve corresponder ao do local da pasta do repositório com todos os hifens no caminho escapados corretamente.

Embora o uso de hifens nos nomes dos itens do repositório seja uma prática recomendada no desenvolvimento do AEM, os hifens são ilegais nos nomes dos pacotes Java™.

A plataforma subjacente do CRX deve ser capaz de distinguir entre um sublinhado real `_ ` e um hífen `-`. Portanto, no JCR, o hífen deve ser substituído pelo seu valor Unicode (u002d) e evitado com um sublinhado `_`.

Por exemplo, se o caminho do repositório for **/apps/my-example/component/info/Info.java**, o nome do pacote deverá ser `java package apps.my_002dexample.component.info;`

Observe que um sublinhado deve ser escapado da mesma forma, de modo que `_` se torne `_005f`.
