---
title: Iniciando e interrompendo o WebSphere Application Server
description: Vários procedimentos exigem que você interrompa ou inicie a instância do WebSphere em que deseja implantar os produtos do AEM Forms. Este documento descreve como iniciar e parar o WebSphere Application Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
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
source-wordcount: '180'
ht-degree: 0%
---
# Iniciando e interrompendo o WebSphere Application Server {#starting-and-stopping-websphere-application-server}

Vários procedimentos exigem que você interrompa ou inicie a instância do WebSphere em que deseja implantar os produtos do AEM Forms. Se não tiver certeza se o servidor de aplicativos foi iniciado, você poderá exibir primeiro o status do WebSphere Application Server.

## Exibir o status do WebSphere Application Server {#view-the-status-of-websphere-application-server}

1. Em um prompt de comando, vá para o diretório `[appserver root]/bin`.
1. Digite o seguinte comando, substituindo *server_name* pelo nome do WebSphere Application Server:

   * (Windows) `serverStatus.bat`*nome_do_servidor*
   * (Linux, UNIX) ./ `serverStatus.sh`*nome_do_servidor*

## Iniciar o WebSphere Application Server {#start-websphere-application-server}

1. Em um prompt de comando, vá para o diretório `[appserver root]/bin`.
1. Digite o seguinte comando, substituindo *server_name* pelo nome do WebSphere Application Server:

   * (Windows) `startServer.bat`*nome_do_servidor*
   * (Linux, UNIX) ./ `startServer.sh`*nome_do_servidor*

## Interromper o Servidor de Aplicativos WebSphere {#stop-websphere-application-server}

1. Em um prompt de comando, vá para o diretório `[appserver root]/bin`.
1. Digite o seguinte comando, substituindo *server_name* pelo nome do WebSphere Application Server:

   * (Windows) `stopServer.bat`*nome_do_servidor*
   * (Linux, UNIX) ./ `stopServer.sh`*nome_do_servidor*
