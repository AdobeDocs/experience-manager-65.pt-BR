---
title: Nomeação de convenções no nome do pacote Java&trade;
description: Saiba mais sobre as convenções de nomenclatura e o uso de hifens no nome do pacote Java&trade;.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 1%

---

# Convenções de nomenclatura {#naming-conventions}

## Hífens no nome do pacote Java™ {#hyphens-in-java-package-name}

Ao criar um local para uma classe Java™, o nome do pacote deve corresponder ao do local da pasta do repositório com todos os hifens no caminho escapados corretamente.

Embora o uso de hifens nos nomes dos itens do repositório seja uma prática recomendada no desenvolvimento de AEM, os hifens são ilegais nos nomes dos pacotes Java™.

A plataforma CRX subjacente deve ser capaz de distinguir entre um sublinhado real `_ `e um hífen `-`. Assim, no JCR, o hífen deve ser substituído pelo seu valor Unicode (u002d) e evitado com um sublinhado `_`.

Por exemplo, se o caminho do repositório for **/apps/my-example/component/info/Info.java**, o nome do pacote deve ser `java package apps.my_002dexample.component.info;`

Observe que um sublinhado deve ser evitado de forma semelhante, de modo que `_` torna-se `_005f`.
