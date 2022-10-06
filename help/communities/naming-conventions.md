---
title: Convenções de nomenclatura
seo-title: Naming Conventions
description: Hifens no nome do pacote Java
seo-description: Hyphens in Java Package Name
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 3%

---

# Convenções de nomenclatura {#naming-conventions}

## Hifens no nome do pacote Java {#hyphens-in-java-package-name}

Ao criar um local para uma classe Java, esteja ciente de que o nome do pacote deve corresponder ao do local da pasta do repositório com quaisquer hifens no caminho escapado corretamente.

Embora o uso de hifens nos nomes dos itens do repositório seja uma prática recomendada AEM desenvolvimento, os hifens são ilegais nos nomes dos pacotes Java.

A plataforma CRX subjacente deve ser capaz de distinguir entre um sublinhado real `_ `e um hífen `-`. Assim, no JCR, o hífen deve ser substituído pelo seu valor unicode (u002d) e escapado com um sublinhado `_`.

Por exemplo, se o caminho do repositório for **/apps/my-example/component/info/Info.java**, o nome do pacote deve ser `java package apps.my_002dexample.component.info;`

Observe que um sublinhado deve ser evitado de forma semelhante, de modo que `_` become `_005f`.
