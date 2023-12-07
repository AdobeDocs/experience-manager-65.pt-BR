---
title: Arquivos de log
description: Eventos como erros de tempo de execução ou de inicialização são registrados nos arquivos de log do servidor de aplicativos, que podem ser abertos usando qualquer editor de texto.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# Arquivos de log {#log-files}

Eventos como erros de tempo de execução ou de inicialização são registrados nos arquivos de log do servidor de aplicativos. Se você tiver problemas ao implantar no servidor de aplicativos, poderá usar os arquivos de log para ajudá-lo a encontrar o problema. Você pode abrir os arquivos de log usando qualquer editor de texto.

(JBoss) Os seguintes arquivos de log estão na `[appserver root]/server/'server'/log` diretório:

* boot.log
* server.log.*[aaaa-mm-dd]*
* server.log

(WebLogic) Os arquivos de log de domínio estão na `[appserverdomain]` diretório e os arquivos de log do servidor estão no `[appserverdomain]/servers/[appserver name]/logs` diretório:

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) Os seguintes arquivos de log estão na `[appserver root]/profiles/default/logs/[appserver name]` diretório:

* SystemErr.log
* SystemOut.log
* StartServer.log
