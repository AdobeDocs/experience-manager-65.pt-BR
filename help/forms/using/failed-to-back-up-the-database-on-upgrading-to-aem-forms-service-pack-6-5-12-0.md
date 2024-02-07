---
title: Falha ao fazer backup do banco de dados durante a atualização para 6.5.12.0 para MySQL.
description: Quando um usuário atualiza para o Experience Manager 6.5.12.0 e clica em "Atualizar MySQL", o gerenciador de configurações falha ao fazer backup do banco de dados Experience Manager Forms anterior.
source-git-commit: a9d59e00efe8f0c2cbfca51901c441a2d65b70f2
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Falha ao fazer backup do banco de dados durante a atualização para 6.5.12.0 para MySQL {#issue}

Quando um usuário atualiza para o Experience Manager 6.5.12.0 e clica em &quot;Atualizar MySQL&quot;, o gerenciador de configurações falha ao fazer backup do banco de dados Experience Manager Forms anterior. Ele mostra o erro:

`Failed to backup the previous Adobe Experience Manager Forms Database`


## Aplica-se a {#applies-to}

* Experience Manager 6.5 Forms

## Solução {#solution}

Para resolver o problema, aumente o max_packet_size do banco de dados para 100 M ou conforme necessário no arquivo my.ini localizado em {AEM_HOME}/mysql.
