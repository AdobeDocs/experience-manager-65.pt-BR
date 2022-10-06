---
title: Iniciando e parando o WebSphere Application Server
seo-title: Starting and stopping WebSphere Application Server
description: Vários procedimentos exigem que você pare ou inicie a instância do WebSphere onde deseja implantar AEM produtos de formulários. Este documento descreve como iniciar e parar o WebSphere Application Server.
seo-description: Several procedures require you to stop or start the instance of WebSphere where you want to deploy AEM forms products. This document describes how to start and stop the WebSphere Application Server.
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Iniciando e parando o WebSphere Application Server {#starting-and-stopping-websphere-application-server}

Vários procedimentos exigem que você pare ou inicie a instância do WebSphere onde deseja implantar AEM produtos de formulários. Se não tiver certeza se o servidor de aplicativos foi iniciado, primeiro poderá visualizar o status do WebSphere Application Server.

## Exibir o status do WebSphere Application Server {#view-the-status-of-websphere-application-server}

1. Em um prompt de comando, acesse `[appserver root]/bin` diretório.
1. Digite o seguinte comando, substituindo *server_name* com o nome do WebSphere Application Server:

   * (Windows) `serverStatus.bat`*server_name*
   * (Linux, UNIX) ./ `serverStatus.sh`*server_name*

## Iniciar WebSphere Application Server {#start-websphere-application-server}

1. Em um prompt de comando, acesse `[appserver root]/bin` diretório.
1. Digite o seguinte comando, substituindo *server_name* com o nome do WebSphere Application Server:

   * (Windows) `startServer.bat`*server_name*
   * (Linux, UNIX) ./ `startServer.sh`*server_name*

## Parar o WebSphere Application Server {#stop-websphere-application-server}

1. Em um prompt de comando, acesse `[appserver root]/bin` diretório.
1. Digite o seguinte comando, substituindo *server_name* com o nome do WebSphere Application Server:

   * (Windows) `stopServer.bat`*server_name*
   * (Linux, UNIX) ./ `stopServer.sh`*server_name*
