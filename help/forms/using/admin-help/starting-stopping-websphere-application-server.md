---
title: Iniciando e interrompendo o WebSphere Application Server
description: Vários procedimentos exigem que você interrompa ou inicie a instância do WebSphere na qual deseja implantar produtos de formulários AEM. Este documento descreve como iniciar e parar o WebSphere Application Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# Iniciando e interrompendo o WebSphere Application Server {#starting-and-stopping-websphere-application-server}

Vários procedimentos exigem que você interrompa ou inicie a instância do WebSphere na qual deseja implantar produtos de formulários AEM. Se não tiver certeza se o servidor de aplicativos foi iniciado, você poderá exibir primeiro o status do WebSphere Application Server.

## Exibir o status do WebSphere Application Server {#view-the-status-of-websphere-application-server}

1. Em um prompt de comando, vá para a `[appserver root]/bin` diretório.
1. Digite o seguinte comando, substituindo *server_name* com o nome do WebSphere Application Server:

   * (Windows) `serverStatus.bat`*server_name*
   * (Linux, UNIX) ./ `serverStatus.sh`*server_name*

## Iniciar o WebSphere Application Server {#start-websphere-application-server}

1. Em um prompt de comando, vá para a `[appserver root]/bin` diretório.
1. Digite o seguinte comando, substituindo *server_name* com o nome do WebSphere Application Server:

   * (Windows) `startServer.bat`*server_name*
   * (Linux, UNIX) ./ `startServer.sh`*server_name*

## Interromper o Servidor de Aplicativos WebSphere {#stop-websphere-application-server}

1. Em um prompt de comando, vá para a `[appserver root]/bin` diretório.
1. Digite o seguinte comando, substituindo *server_name* com o nome do WebSphere Application Server:

   * (Windows) `stopServer.bat`*server_name*
   * (Linux, UNIX) ./ `stopServer.sh`*server_name*
