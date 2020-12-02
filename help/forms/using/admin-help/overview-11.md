---
title: Visão geral do Monitor de integridade
seo-title: Visão geral do Monitor de integridade
description: Este documento fornece a visão geral do Monitor de integridade e detalhes sobre como acessá-lo.
seo-description: Este documento fornece a visão geral do Monitor de integridade e detalhes sobre como acessá-lo.
uuid: 5934fd2d-80a5-4c6d-b3ee-882c2865705b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c303e967-944d-40b0-96ca-f91e2f42a0d0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# Visão geral do Monitor de integridade {#overview-of-health-monitor}

O Monitor de integridade fornece informações essenciais sobre o sistema de formulários AEM, como informações do servidor, uso da memória e uso do processador. Também estão disponíveis estatísticas do Gerenciador de Trabalho, como o número de itens de trabalho ou trabalhos na fila e seus status. É possível executar as seguintes tarefas usando o Monitor de integridade:

* Verifique se o sistema está funcionando corretamente
* Informações de visualização para ajudar a diagnosticar problemas do sistema à medida que ocorrem
* Executar operações em itens de trabalho ou trabalhos que exibem problemas
* Limpar registros obsoletos do banco de dados do Gerenciador de Jobs

A página Monitor de integridade no console de administração tem três guias:

* A guia Sistema exibe gráficos de monitoramento de recursos e informações sobre o servidor de formulários (ou nó em um ambiente agrupado). (Consulte [Informações do sistema de Visualização](/help/forms/using/admin-help/view-system-information.md#view-system-information).)
* A guia Gerenciador de Trabalho exibe dados relacionados ao Gerenciador de Trabalho, como o número de itens de trabalho na fila do Gerenciador de Trabalho. Você pode filtrar as informações usando vários critérios ou gerenciar itens de trabalho individuais usando as ferramentas de operação. (Consulte [Estatísticas de Visualização relacionadas ao Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* A guia Scheduler de Expurgação de Job permite que você expurgue registros obsoletos do banco de dados do Gerenciador de Jobs. (Consulte [Limpar registros da base de dados do Gerenciador de Tarefas](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)

A página da Web do Monitor de integridade é preenchida com estatísticas obtidas por meio de uma API Gemfire. Esta API detecta automaticamente todos os nós em um cluster. Ele também resolve problemas de segurança que ocorrem ao coletar estatísticas de servidores proxy ou balanceadores de carga. As opções Java estão disponíveis para ajustar o Monitor de integridade, diminuindo o impacto no desempenho do ambiente de formulários AEM. (Consulte [Ajuste do desempenho do Monitor de Integridade](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance).)

**Monitor de integridade de acesso**

1. No console de administração, clique em Monitor de integridade no canto superior direito da página.

