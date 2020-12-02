---
title: Arquivos de registro
seo-title: Arquivos de registro
description: Eventos como erros de tempo de execução ou inicialização são registrados nos arquivos de log do servidor de aplicativos, que podem ser abertos usando qualquer editor de texto.
seo-description: Eventos como erros de tempo de execução ou inicialização são registrados nos arquivos de log do servidor de aplicativos, que podem ser abertos usando qualquer editor de texto.
uuid: 6ed9fdcd-ff02-4b35-893f-09261a6a557a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cf140483-470f-4bff-8870-304207508aab
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Arquivos de registro {#log-files}

Eventos como erros de tempo de execução ou inicialização são registrados nos arquivos de log do servidor de aplicativos. Se tiver problemas ao implantar no servidor de aplicativos, você pode usar os arquivos de log para ajudar a encontrar o problema. É possível abrir os arquivos de registro usando qualquer editor de texto.

(JBoss) Os seguintes arquivos de log estão localizados no diretório `[appserver root]/server/'server'/log`:

* boot.log
* server.log.*[aaaa-mm-dd]*
* server.log

(WebLogic) Os arquivos de log de domínio estão localizados no diretório `[appserverdomain]` e os arquivos de log de servidor estão localizados no diretório `[appserverdomain]/servers/[appserver name]/logs`:

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) Os seguintes arquivos de log estão localizados no diretório `[appserver root]/profiles/default/logs/[appserver name]`:

* SystemErr.log
* SystemOut.log
* StartServer.log

