---
title: Convenções de nomenclatura
seo-title: Convenções de nomenclatura
description: Hífens no nome do pacote Java
seo-description: Hífens no nome do pacote Java
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
translation-type: tm+mt
source-git-commit: 22e853ecaf2696c7329a81bb9d375b1dbc74452c

---


# Naming Conventions {#naming-conventions}

## Hífens no nome do pacote Java {#hyphens-in-java-package-name}

Ao criar um local para uma classe Java, lembre-se de que o nome do pacote deve corresponder ao do local da pasta do repositório com qualquer hífen no caminho que tenha sido escapado corretamente.

Embora o uso de hífens nos nomes de itens do repositório seja uma prática recomendada no desenvolvimento do AEM, os hífens são ilegais nos nomes dos pacotes Java.

A plataforma CRX subjacente deve ser capaz de distinguir entre um sublinhado real `_ `e um hífen `-`. Assim, no JCR, o hífen deve ser substituído pelo seu valor unicode (u002d) e escapado com um sublinhado `_`.

Por exemplo, se o caminho do repositório for **/apps/my-example/component/info/Info.java**, o nome do pacote deverá ser `java package apps.my_002dexample.component.info;`

Observe que um sublinhado deve ser evitado da mesma forma, tal que `_` se torna `_005f`.
