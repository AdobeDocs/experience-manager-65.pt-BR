---
title: Como os relatórios de processo funcionam
seo-title: Como os relatórios de processo funcionam
description: Descrição dos serviços que compõem o AEM Forms no JEE Process Reporting e uma introdução à interface do usuário do Process Reporting
seo-description: Descrição dos serviços que compõem o AEM Forms no JEE Process Reporting e uma introdução à interface do usuário do Process Reporting
uuid: 37e31985-088a-4ef6-ba57-10a01597a873
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a6ff50df-273d-48f7-b0c6-0e69e900b97f
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Como os relatórios de processo funcionam{#how-process-reporting-works}

Process Reporting é o módulo de relatório do AEM Forms no JEE.

O Process Reporting permite que você execute relatórios em processos e tarefas do AEM Forms.

O Process Reporting usa o repositório incorporado do Process Reporting para publicar dados do Forms. Em seguida, ele usa esses dados para executar relatórios.

O Process Reporting consiste nos seguintes módulos:

* [Serviço ProcessDataPublisher](#processdatapublisher-service-br-p)
* [Serviço ProcessDataStorage](#processdatastorageprovider-service-br-p)
* [Serviço OSGi](#osgi-service-br-p)
* [Servlet Dados de consulta](#querydataservlet-service-br-p)
* [Interface do usuário do Process Reporting](#process-reporting-user-interface-br-p)

## Arquitetura do Process Reporting {#process-reporting-architecture-br}

![arquitetura processreporting](assets/processreportingarchitecture.png)

## Processar módulos de relatório {#process-reporting-modules}

### Serviço ProcessDataPublisher {#processdatapublisher-service-br}

O servidor ProcessDataPublisher é executado periodicamente no banco de dados do AEM Forms e extrai os dados que foram alterados desde a última execução do serviço. Em seguida, publica os dados no serviço de armazenamento de dados do processo.

Para obter detalhes sobre como configurar o serviço, consulte [Configurar o serviço](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p)ProcessDataPublisher.

### Serviço ProcessDataStorageProvider {#processdatastorageprovider-service-br}

O serviço ProcessDataStorageProvider recebe dados do processo do serviço ProcessDataPublisher e salva os dados no repositório do Process Reporting.

Para obter detalhes sobre como configurar o serviço, consulte [Configurar o serviço](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p)ProcessDataStorageProvider.

### Serviço OSGi {#osgi-service-br}

O QueryDataServlet usa esse serviço para obter os dados de relatório do repositório do Process Reporting.

### Serviço QueryDataServlet {#querydataservlet-service-br}

O serviço QueryDataServlet aceita consultas da interface de usuário do Process Reporting.

O serviço então usa os serviços OSGi para obter os dados de relatório relevantes, processar os dados e retornar os dados à interface do usuário.

### Interface do usuário do Process Reporting {#process-reporting-user-interface-br}

A interface do usuário do Process Reporting é uma interface baseada em navegador da Web. Use essa interface para exibir informações de processo e tarefa publicadas no banco de dados do AEM Forms.

Para obter uma introdução à interface do usuário do Process Reporting, consulte Interface [do usuário do](/help/forms/using/process-reporting/introduction-process-reporting.md)Process Reporting.

### Serviço QueryDataServlet {#querydataservlet-service-br-1}

O serviço QueryDataServlet aceita consultas da interface de usuário do Process Reporting.

O serviço então usa os serviços OSGi para obter os dados de relatório relevantes, processar os dados e retornar os dados à interface do usuário.

### Relatórios personalizados {#custom-reports-br}

Você pode criar seus próprios relatórios personalizados e exibi-los na guia Relatórios personalizados da interface do usuário do Process Reporting.

Para obter as etapas de criação de um relatório personalizado, consulte Criar um relatório personalizado no artigo Relatórios [personalizados em relatórios](/help/forms/using/process-reporting/process-reporting-custom-reports.md)de processo.

[Contate o suporte](https://www.adobe.com/account/sign-in.supportportal.html)
