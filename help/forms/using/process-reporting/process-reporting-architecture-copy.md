---
title: Como Funciona o Relatório de Processo
seo-title: How Process Reporting Works
description: Descrição dos serviços que compõem o AEM Forms no JEE Process Reporting e uma introdução à interface do Process Reporting
seo-description: Description of the services that make up the AEM Forms on JEE Process Reporting and an introduction to the Process Reporting UI
uuid: 4631b734-a679-495c-a708-2348bf22c1f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a1af9920-5d2a-462f-bdee-ccec4c047c5b
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# Como Funciona o Relatório de Processo {#how-process-reporting-works}

Process Reporting é o módulo de relatório do AEM Forms no JEE.

Process Reporting permite executar relatórios em processos e tarefas do AEM Forms.

O Process Reporting usa o repositório incorporado do Process Reporting para publicar dados do Forms. Em seguida, ele usa esses dados para executar relatórios.

O Relatório de processos consiste nos seguintes módulos:

* [Serviço ProcessDataPublisher](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatapublisher-service-br-p)
* [serviço ProcessDataStorage](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatastorageprovider-service-br-p)
* [Serviço OSGi](/help/forms/using/process-reporting/process-reporting-architecture.md#p-osgi-service-br-p)
* [Servlet de dados de consulta](/help/forms/using/process-reporting/process-reporting-architecture.md#p-querydataservlet-service-br-p)
* [Interface do usuário do Relatório de processos](/help/forms/using/process-reporting/process-reporting-architecture.md#p-process-reporting-user-interface-br-p)

## Arquitetura de relatórios de processos {#process-reporting-architecture-br}

![processreportingarchitecture](assets/processreportingarchitecture.png)

## Módulos de relatório de processo {#process-reporting-modules}

### Serviço ProcessDataPublisher {#processdatapublisher-service-br}

O servidor ProcessDataPublisher é executado periodicamente no banco de dados do AEM Forms e extrai os dados alterados desde a última execução do serviço. Em seguida, ele publica os dados no serviço de Armazenamento de dados de processos.

Para obter detalhes sobre a configuração do serviço, consulte [Configurar o serviço ProcessDataPublisher](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p).

### Serviço ProcessDataStorageProvider {#processdatastorageprovider-service-br}

O serviço ProcessDataStorageProvider recebe dados do processo do serviço ProcessDataPublisher e salva os dados no repositório do Process Reporting.

Para obter detalhes sobre a configuração do serviço, consulte [Configurar o serviço ProcessDataStorageProvider](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p).

### Serviço OSGi {#osgi-service-br}

O QueryDataServlet usa esse serviço para obter os dados de relatório do repositório do Process Reporting.

### Serviço QueryDataServlet {#querydataservlet-service-br}

O serviço QueryDataServlet aceita consultas da interface do usuário do Process Reporting.

O serviço usa serviços OSGi para obter os dados de relatório relevantes, processa os dados e retorna os dados à interface do usuário.

### Interface do usuário do Relatório de processos {#process-reporting-user-interface-br}

A interface do usuário de Relatórios do processo é baseada em navegador da Web. Use essa interface para exibir informações sobre processos e tarefas publicadas no banco de dados do AEM Forms.

### Serviço QueryDataServlet {#querydataservlet-service-br-1}

O serviço QueryDataServlet aceita consultas da interface do usuário do Process Reporting.

O serviço usa serviços OSGi para obter os dados de relatório relevantes, processa os dados e retorna os dados à interface do usuário.

### Relatórios personalizados {#custom-reports-br}

Você pode criar seus próprios relatórios personalizados e exibi-los na guia Relatórios personalizados da interface do usuário Processar relatórios.

Para obter as etapas para criar um relatório personalizado, consulte Para criar um relatório personalizado no artigo [Relatórios personalizados em relatórios de processo](/help/forms/using/process-reporting/process-reporting-custom-reports.md).
