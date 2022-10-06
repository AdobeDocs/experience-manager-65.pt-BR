---
title: Como a geração de relatórios de processo funciona
seo-title: How Process Reporting Works
description: Descrição dos serviços que compõem a AEM Forms no JEE Process Reporting e uma introdução à interface do usuário de Relatórios do Processo
seo-description: Description of the services that make up the AEM Forms on JEE Process Reporting and an introduction to the Process Reporting UI
uuid: 37e31985-088a-4ef6-ba57-10a01597a873
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a6ff50df-273d-48f7-b0c6-0e69e900b97f
docset: aem65
exl-id: 66dfac36-5b7e-40be-9921-efa9f2a9521c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# Como a geração de relatórios de processo funciona{#how-process-reporting-works}

O Process Reporting é o módulo de relatórios da AEM Forms no JEE.

O Relatório de processos permite que você execute relatórios em processos e tarefas do AEM Forms.

O Process Reporting usa o repositório incorporado do Process Reporting para publicar os dados do Forms. Em seguida, ele usa esses dados para executar relatórios.

O Process Reporting consiste nos seguintes módulos:

* [Serviço ProcessDataPublisher](#processdatapublisher-service-br-p)
* [Serviço ProcessDataStorage](#processdatastorageprovider-service-br-p)
* [Serviço OSGi](#osgi-service-br-p)
* [Servlet de dados de consulta](#querydataservlet-service-br-p)
* [Interface do usuário do Process Reporting](#process-reporting-user-interface-br-p)

## Arquitetura de relatórios de processos {#process-reporting-architecture-br}

![processreportingarchitecture](assets/processreportingarchitecture.png)

## Módulos de Relatório de Processos {#process-reporting-modules}

### Serviço ProcessDataPublisher {#processdatapublisher-service-br}

O servidor ProcessDataPublisher é executado periodicamente no banco de dados do AEM Forms e extrai os dados alterados desde a última execução do serviço. Em seguida, ele publica os dados no serviço de Armazenamento de Dados de Processo.

Para obter detalhes sobre como configurar o serviço, consulte [Configurar o serviço ProcessDataPublisher](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p).

### Serviço ProcessDataStorageProvider {#processdatastorageprovider-service-br}

O serviço ProcessDataStorageProvider recebe dados do processo do serviço ProcessDataPublisher e salva os dados no repositório do Process Reporting.

Para obter detalhes sobre como configurar o serviço, consulte [Configurar o serviço ProcessDataStorageProvider](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p).

### Serviço OSGi {#osgi-service-br}

O QueryDataServlet usa esse serviço para obter os dados de relatório do repositório do Process Reporting.

### Serviço QueryDataServlet {#querydataservlet-service-br}

O serviço QueryDataServlet aceita consultas da interface do usuário do Process Reporting.

O serviço usa os serviços OSGi para obter os dados de relatório relevantes, processar os dados e retornar os dados à interface do usuário.

### Interface do usuário do Process Reporting {#process-reporting-user-interface-br}

A interface do usuário do Process Reporting é uma interface baseada em navegador da Web. Use essa interface para exibir informações de processo e tarefa publicadas no banco de dados do AEM Forms.

Para obter uma introdução à interface do usuário do Process Reporting, consulte [Interface do usuário do Process Reporting](/help/forms/using/process-reporting/introduction-process-reporting.md).

### Serviço QueryDataServlet {#querydataservlet-service-br-1}

O serviço QueryDataServlet aceita consultas da interface do usuário do Process Reporting.

O serviço usa os serviços OSGi para obter os dados de relatório relevantes, processar os dados e retornar os dados à interface do usuário.

### Relatórios personalizados {#custom-reports-br}

Você pode criar seus próprios relatórios personalizados e exibi-los na guia Relatórios personalizados da interface do usuário do Relatório de processo .

Para obter as etapas para criar um relatório personalizado, consulte Criar um relatório personalizado no artigo [Relatórios Personalizados no Processo](/help/forms/using/process-reporting/process-reporting-custom-reports.md).
