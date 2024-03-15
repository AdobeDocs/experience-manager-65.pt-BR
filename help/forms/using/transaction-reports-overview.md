---
title: Visão Geral dos Relatórios de Transação
description: Manter uma contagem de todos os formulários enviados, comunicação interativa renderizada, Documentos convertidos em um formato para outro e muito mais
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Transaction Reports
exl-id: bb812614-f4d8-4f57-bea2-8f7d31457039
source-git-commit: d0db00de6b767a12a9492bbbcec49a8c5d25ff27
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Relatórios de transação para o AEM Forms no OSGi {#transaction-reports-overview}

<!--## Introduction {#introduction}

Transaction reports in AEM Forms let you keep a count of all transactions taken place since a specified date on your AEM Forms deployment. The objective is to provide information about product usage and help business stakeholders understand their digital processing volumes. Examples of a transaction include:

* Submission of an adaptive form, an HTML5 Form, or a form set
* Rendition of a print or a web version of an interactive communication
* Conversion of a document from one file format to another

For more information on what is considered a transaction, see [Billable APIs](../../forms/using/transaction-reports-billable-apis.md).-->

A gravação de transação está desabilitada por padrão. Você pode [habilitar registro de transação](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) no console da Web AEM. Você pode exibir relatórios de transações nas instâncias de autor, processamento ou publicação. Exiba relatórios de transações nas instâncias de autor ou de processamento para obter uma soma agregada de todas as transações. Exiba relatórios de transações nas instâncias de publicação para obter uma contagem de todas as transações que ocorrem somente nessa instância de publicação de onde o relatório é executado.

Não crie conteúdo (crie formulários adaptáveis, comunicação interativa, temas e outras atividades de criação) e processe documentos (use fluxos de trabalho, serviços de documentos e outras atividades de processamento) na mesma instância do AEM. Mantenha a gravação da transação desativada para os servidores do AEM Forms usados para criar conteúdo. Mantenha a gravação da transação ativada para os servidores do AEM Forms usados para processar documentos.

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

Uma transação permanece no buffer por um período especificado (Tempo do Buffer de Liberação + Tempo de replicação reversa). Por padrão, leva aproximadamente 90 segundos para a contagem de transações ser refletida no relatório de transações.

Ações como enviar um Formulário PDF, usar a interface do usuário do agente para visualizar uma comunicação interativa ou usar métodos de envio de formulário não padrão não são contabilizadas como transações. O AEM Forms fornece uma API para registrar essas transações. Chame a API a partir das implementações personalizadas para registrar uma transação.

## Topologia suportada {#supported-topology}

Os relatórios de transação estão disponíveis somente no AEM Forms em ambientes OSGi. Ela oferece suporte às topologias author-publish, author-processing-publish e somente ao processamento de topologias. Por exemplo, topologias, consulte [Arquitetura e topologias de implantação do AEM Forms](../../forms/using/transaction-reports-overview.md).

A contagem de transações é revertida e replicada das instâncias de publicação para as instâncias de autoria ou processamento. Uma topologia indicativa de publicação do autor é exibida abaixo:

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>Os relatórios de transação do AEM Forms não suportam topologias que contêm apenas instâncias de publicação.

### Diretrizes para o uso de relatórios de transação {#guidelines-for-using-transaction-reports}

* Desative os relatórios de transações em todas as instâncias de autor, pois os relatórios sobre instâncias de autor incluem transações registradas durante as atividades de criação.
* Ativar o **Mostrar transações somente a partir da publicação** opção na instância do autor para exibir transações cumulativas de todas as instâncias de publicação. Você também pode exibir relatórios de transações em cada instância de publicação para transações reais somente nessa instância de publicação específica.
* Não use instâncias do autor para executar fluxos de trabalho e processar documentos.
* Antes de usar o relatório de transações, se você tiver uma topologia com servidores de publicação, verifique se a replicação inversa está ativada para todas as instâncias de publicação.
* Os dados da transação são revertidos e replicados de uma instância de publicação para somente o autor ou instância de processamento correspondente. A instância de autoria ou processamento não pode replicar dados para outra instância. Por exemplo, se você tiver a topologia author-processing-publish, os dados de transação agregados serão replicados somente na instância de processamento.

## Artigos relacionados {#related-articles}

* [Visualização e noções básicas de um relatório de transações do AEM Forms no OSGi](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [APIs faturáveis de relatórios de transação para o AEM Forms no OSGi](../../forms/using/transaction-reports-billable-apis.md)
* [Registrar uma transação para implementações personalizadas do AEM Forms no OSGi](/help/forms/using/record-transaction-custom-implementation.md)
