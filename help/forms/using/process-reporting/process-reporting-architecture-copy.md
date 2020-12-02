---
title: Como o Relatórios de processo funciona
seo-title: Como o Relatórios de processo funciona
description: Descrição dos serviços que compõem o Relatórios AEM Forms on JEE Process e uma introdução à interface do Relatórios Process
seo-description: Descrição dos serviços que compõem o Relatórios AEM Forms on JEE Process e uma introdução à interface do Relatórios Process
uuid: 4631b734-a679-495c-a708-2348bf22c1f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a1af9920-5d2a-462f-bdee-ccec4c047c5b
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Como o Relatórios de processo funciona {#how-process-reporting-works}

O Process Relatórios é o módulo relatórios do AEM Forms no JEE.

O Process Relatórios permite que você execute relatórios em processos e tarefas AEM Forms.

O Process Relatórios usa o repositório incorporado do Process Relatórios para publicar dados do Forms. Em seguida, ele usa esses dados para executar relatórios.

O Relatórios de processo consiste nos seguintes módulos:

* [Serviço ProcessDataPublisher](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatapublisher-service-br-p)
* [Serviço ProcessDataStorage](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatastorageprovider-service-br-p)
* [Serviço OSGi](/help/forms/using/process-reporting/process-reporting-architecture.md#p-osgi-service-br-p)
* [Servlet de dados de query](/help/forms/using/process-reporting/process-reporting-architecture.md#p-querydataservlet-service-br-p)
* [Processar interface do usuário do Relatórios](/help/forms/using/process-reporting/process-reporting-architecture.md#p-process-reporting-user-interface-br-p)

## Processar arquitetura de Relatórios {#process-reporting-architecture-br}

![arquitetura processreporting](assets/processreportingarchitecture.png)

## Processar módulos de Relatórios {#process-reporting-modules}

### Serviço ProcessDataPublisher {#processdatapublisher-service-br}

O servidor ProcessDataPublisher é executado periodicamente no banco de dados AEM Forms e extrai os dados que foram alterados desde a última execução do serviço. Em seguida, publica os dados no serviço de Armazenamento de Dados do Processo.

Para obter detalhes sobre como configurar o serviço, consulte [Configurar o serviço ProcessDataPublisher](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p).

### Serviço ProcessDataStorageProvider {#processdatastorageprovider-service-br}

O serviço ProcessDataStorageProvider recebe dados do processo do serviço ProcessDataPublisher e salva os dados no repositório do Relatórios Process.

Para obter detalhes sobre como configurar o serviço, consulte [Configurar o serviço ProcessDataStorageProvider](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p).

### Serviço OSGi {#osgi-service-br}

O QueryDataServlet usa esse serviço para obter os dados do relatórios do repositório do Relatórios Process.

### Serviço QueryDataServlet {#querydataservlet-service-br}

O serviço QueryDataServlet aceita query da interface do usuário do Relatórios Process.

O serviço usa os serviços OSGi para obter os dados relevantes do relatórios, processar os dados e retornar os dados à interface do usuário.

### Processar interface de usuário do Relatórios {#process-reporting-user-interface-br}

A interface do usuário do Process Relatórios é uma interface baseada em navegador da Web. Use essa interface para visualização de informações de processo e tarefa publicadas no banco de dados da AEM Forms.

### Serviço QueryDataServlet {#querydataservlet-service-br-1}

O serviço QueryDataServlet aceita query da interface do usuário do Relatórios Process.

O serviço usa os serviços OSGi para obter os dados relevantes do relatórios, processar os dados e retornar os dados à interface do usuário.

### Relatórios Personalizados {#custom-reports-br}

Você pode criar seus próprios relatórios personalizados e exibi-los na guia Relatórios personalizados da interface do usuário do Process Relatórios.

Para obter as etapas para criar um relatório personalizado, consulte Criar um relatório personalizado no artigo [Relatórios personalizados no Relatórios de processo](/help/forms/using/process-reporting/process-reporting-custom-reports.md).
