---
title: Visão geral do Health Monitor
description: Este documento fornece a visão geral do monitor de Integridade e detalhes sobre como acessá-lo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Visão geral do Health Monitor {#overview-of-health-monitor}

O Health Monitor fornece informações críticas sobre o sistema de formulários AEM, como informações do servidor, uso de memória e uso do processador. Também estão disponíveis estatísticas do Work Manager, como o número de itens de trabalho ou jobs na fila e seus status. Você pode executar as seguintes tarefas usando o Health Monitor:

* Verifique se o sistema está sendo executado corretamente
* Visualize as informações para ajudar a diagnosticar problemas do sistema à medida que ocorrem
* Executar operações em itens de trabalho ou trabalhos que exibem problemas
* Expurgar registros obsoletos do banco de dados do Gerenciador de Jobs

A página Monitor de integridade no console de administração tem três guias:

* A guia Sistema exibe gráficos de monitoramento de recursos e informações sobre o Forms Server (ou nó em um ambiente em cluster). (Consulte [Exibir informações do sistema](/help/forms/using/admin-help/view-system-information.md#view-system-information).)
* A guia Gerenciador de trabalho exibe dados relacionados ao Gerenciador de trabalho, como o número de itens de trabalho na fila do Gerenciador de trabalho. Você pode filtrar as informações usando vários critérios ou gerenciar itens de trabalho individuais usando as ferramentas de operação. (Consulte [Exibir estatísticas relacionadas ao Gerenciador de Trabalho](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* A guia Programador de Expurgação do Job permite que você expurgue registros obsoletos do banco de dados do Gerenciador de Jobs. (Consulte [Limpar registros do banco de dados do Gerenciador de Trabalhos](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)

A página da Web do Health Monitor é preenchida com estatísticas obtidas por meio da API do Gemfire. Essa API descobre automaticamente todos os nós em um cluster. Ele também resolve problemas de segurança que ocorrem ao coletar estatísticas dos servidores proxy ou balanceadores de carga. As opções de Java estão disponíveis para ajustar o Health Monitor, diminuindo o impacto no desempenho do seu ambiente de formulários AEM. (Consulte [Ajustando o desempenho do Monitor de Integridade](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance).)

**Monitor de Integridade de Acesso**

1. No console de administração, clique em Monitor de integridade no canto superior direito da página.
