---
title: Arquivos de log
description: Eventos como erros de tempo de execução ou de inicialização são registrados nos arquivos de log do servidor de aplicativos, que podem ser abertos usando qualquer editor de texto.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# Arquivos de log {#log-files}

Eventos como erros de tempo de execução ou de inicialização são registrados nos arquivos de log do servidor de aplicativos. Se você tiver problemas ao implantar no servidor de aplicativos, poderá usar os arquivos de log para ajudá-lo a encontrar o problema. Você pode abrir os arquivos de log usando qualquer editor de texto.

(JBoss) Os seguintes arquivos de log estão no diretório `[appserver root]/server/'server'/log`:

* boot.log
* server.log.*[dd-mm-yyyy]*
* server.log

(WebLogic) Os arquivos de log de domínio estão no diretório `[appserverdomain]` e os arquivos de log do servidor estão no diretório `[appserverdomain]/servers/[appserver name]/logs`:

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) Os seguintes arquivos de log estão no diretório `[appserver root]/profiles/default/logs/[appserver name]`:

* SystemErr.log
* SystemOut.log
* StartServer.log
