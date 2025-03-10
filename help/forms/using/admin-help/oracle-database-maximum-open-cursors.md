---
title: Limite máximo de cursores abertos do banco de dados do Oracle
description: Saiba mais sobre como configurar um valor máximo para cursores abertos no Oracle.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5be26485-afe5-47ac-918c-e2fff4f394b2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Limite máximo de cursores abertos do banco de dados do Oracle {#oracle-database-maximum-open-cursors-threshold}

Para configurar um valor máximo para cursores abertos no Oracle, talvez seja necessário ajustar esse valor para um número apropriado para sua aplicação. É evidente que, sob uma carga moderada, a média de cursores abertos era de 2700. Recomenda-se iniciar com um limite superior de 3000. Para obter mais informações, acesse [https://www.orafaq.com/node/758](https://www.orafaq.com/node/758).
