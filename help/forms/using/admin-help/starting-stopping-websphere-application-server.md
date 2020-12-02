---
title: Iniciando e parando o WebSphere Application Server
seo-title: Iniciando e parando o WebSphere Application Server
description: Vários procedimentos exigem que você pare ou start a instância do WebSphere onde deseja implantar AEM produtos de formulários. Este documento descreve como start e interromper o WebSphere Application Server.
seo-description: Vários procedimentos exigem que você pare ou start a instância do WebSphere onde deseja implantar AEM produtos de formulários. Este documento descreve como start e interromper o WebSphere Application Server.
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# Iniciando e parando o WebSphere Application Server {#starting-and-stopping-websphere-application-server}

Vários procedimentos exigem que você pare ou start a instância do WebSphere onde deseja implantar AEM produtos de formulários. Se não tiver certeza se o servidor de aplicativos foi iniciado, você pode primeiro visualização o status do WebSphere Application Server.

## Visualização do status do WebSphere Application Server {#view-the-status-of-websphere-application-server}

1. Em um prompt de comando, vá para o diretório `[appserver root]/bin`.
1. Digite o seguinte comando, substituindo *server_name* pelo nome do seu WebSphere Application Server:

   * (Windows) `serverStatus.bat`*server_name*
   * (Linux, UNIX) ./ `serverStatus.sh`*nome_do_servidor*

## Start WebSphere Application Server {#start-websphere-application-server}

1. Em um prompt de comando, vá para o diretório `[appserver root]/bin`.
1. Digite o seguinte comando, substituindo *server_name* pelo nome do seu WebSphere Application Server:

   * (Windows) `startServer.bat`*server_name*
   * (Linux, UNIX) ./ `startServer.sh`*nome_do_servidor*

## Parar o WebSphere Application Server {#stop-websphere-application-server}

1. Em um prompt de comando, vá para o diretório `[appserver root]/bin`.
1. Digite o seguinte comando, substituindo *server_name* pelo nome do seu WebSphere Application Server:

   * (Windows) `stopServer.bat`*server_name*
   * (Linux, UNIX) ./ `stopServer.sh`*nome_do_servidor*

