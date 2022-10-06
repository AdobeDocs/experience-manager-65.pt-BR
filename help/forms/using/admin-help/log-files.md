---
title: Arquivos de log
seo-title: Log files
description: Eventos como erros de tempo de execução ou de inicialização são registrados nos arquivos de log do servidor de aplicativos, que podem ser abertos usando qualquer editor de texto.
seo-description: Events such as run-time or startup errors are recorded to the application server log files, which can be  opened using any text editor.
uuid: 6ed9fdcd-ff02-4b35-893f-09261a6a557a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cf140483-470f-4bff-8870-304207508aab
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Arquivos de log {#log-files}

Eventos como erros de tempo de execução ou de inicialização são registrados nos arquivos de log do servidor de aplicativos. Se tiver problemas ao implantar no servidor de aplicativos, você poderá usar os arquivos de log para ajudá-lo a encontrar o problema. Você pode abrir os arquivos de log usando qualquer editor de texto.

(JBoss) Os seguintes arquivos de log estão localizados na variável `[appserver root]/server/'server'/log` diretório:

* boot.log
* server.log.*[aaaa-mm-dd]*
* server.log

(WebLogic) Os arquivos de log de domínio estão localizados na `[appserverdomain]` os arquivos de log do servidor e do diretório estão localizados na `[appserverdomain]/servers/[appserver name]/logs` diretório:

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) Os seguintes arquivos de log estão localizados na `[appserver root]/profiles/default/logs/[appserver name]` diretório:

* SystemErr.log
* SystemOut.log
* StartServer.log
