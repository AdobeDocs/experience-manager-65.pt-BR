---
title: Convenções de nomenclatura no nome do pacote Java
description: Hífens no nome do pacote Java
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 1%

---

# Convenções de nomenclatura {#naming-conventions}

## Hífens no nome do pacote Java {#hyphens-in-java-package-name}

Ao criar um local para uma classe Java, esteja ciente de que o nome do pacote deve corresponder ao do local da pasta do repositório com todos os hifens no caminho escapados corretamente.

Embora o uso de hifens nos nomes dos itens do repositório seja uma prática recomendada no desenvolvimento de AEM, os hifens são ilegais nos nomes dos pacotes Java.

A plataforma CRX subjacente deve ser capaz de distinguir entre um sublinhado real `_ `e um hífen `-`. Assim, no JCR, o hífen deve ser substituído pelo seu valor unicode (u002d) e evitado com um sublinhado `_`.

Por exemplo, se o caminho do repositório for **/apps/my-example/component/info/Info.java**, o nome do pacote deve ser `java package apps.my_002dexample.component.info;`

Observe que um sublinhado deve ser evitado de forma semelhante, de modo que `_` torna-se `_005f`.
