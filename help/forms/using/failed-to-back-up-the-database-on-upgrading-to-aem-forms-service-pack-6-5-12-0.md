---
title: Falha ao fazer backup do banco de dados durante a atualização para 6.5.12.0 para MySQL.
description: Quando um usuário atualiza para o Experience Manager 6.5.12.0 e clica em "Atualizar MySQL", o gerenciador de configurações falha ao fazer backup do banco de dados Experience Manager Forms anterior.
exl-id: 1af000fa-439b-4ffd-8b5a-3ba45f0c524c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%
---
# Falha ao fazer backup do banco de dados durante a atualização para 6.5.12.0 para MySQL {#issue}

Quando um usuário atualiza para o Experience Manager 6.5.12.0 e clica em &quot;Atualizar MySQL&quot;, o gerenciador de configurações falha ao fazer backup do banco de dados Experience Manager Forms anterior. Ele mostra o erro:

`Failed to backup the previous Adobe Experience Manager Forms Database`


## Aplica-se a {#applies-to}

* Experience Manager 6.5 Forms

## Solução {#solution}

Para resolver o problema, aumente o max_packet_size do banco de dados para 100 M ou conforme necessário no arquivo my.ini localizado em {AEM_HOME}/mysql.
