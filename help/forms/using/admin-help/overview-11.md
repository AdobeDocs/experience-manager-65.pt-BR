---
title: Visão Geral do Monitor de Integridade
seo-title: Overview of Health Monitor
description: Este documento fornece a visão geral do Monitor de integridade e detalhes sobre como você pode acessá-lo.
seo-description: This document provides the overview of the Health monitor, and details about how you can access it.
uuid: 5934fd2d-80a5-4c6d-b3ee-882c2865705b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c303e967-944d-40b0-96ca-f91e2f42a0d0
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Visão Geral do Monitor de Integridade {#overview-of-health-monitor}

O Monitor de integridade fornece informações críticas sobre o sistema de formulários de AEM, como informações do servidor, uso de memória e uso do processador. Também estão disponíveis estatísticas do Gerenciador de Trabalho, como o número de itens de trabalho ou tarefas na fila e seus status. Você pode executar as seguintes tarefas usando o Monitor de Integridade:

* Verifique se o sistema está funcionando corretamente
* Veja informações para ajudar a diagnosticar problemas do sistema à medida que ocorrem
* Executar operações em itens de trabalho ou trabalhos que exibem problemas
* Limpar registros obsoletos do banco de dados do Gerenciador de Jobs

A página Monitor de integridade no console de administração tem três guias:

* A guia Sistema exibe gráficos de monitoramento de recursos e informações sobre o servidor de formulários (ou nó em um ambiente em cluster). (Consulte [Exibir informações do sistema](/help/forms/using/admin-help/view-system-information.md#view-system-information).)
* A guia Gerenciador de trabalho exibe dados relacionados ao Gerenciador de trabalho, como o número de itens de trabalho na fila do Gerenciador de trabalho. Você pode filtrar as informações usando vários critérios ou gerenciar itens de trabalho individuais usando as ferramentas de operação. (Consulte [Exibir estatísticas relacionadas ao Gerenciador de Trabalho](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* A guia Agendador de Expurgação de Job permite que você expurgue registros obsoletos do banco de dados do Gerenciador de Jobs. (Consulte [Limpar registros do banco de dados do Gerenciador de Jobs](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)

A página da Web Monitor de integridade é preenchida com estatísticas coletadas por meio de uma API do Gemfire. Essa API descobre automaticamente todos os nós em um cluster. Ele também resolve problemas de segurança que ocorrem ao coletar estatísticas de servidores proxy ou balanceadores de carga. As opções de Java estão disponíveis para ajustar o Monitor de integridade, diminuindo o impacto no desempenho do seu ambiente de formulários AEM. (Consulte [Ajustando o desempenho do Monitor de Integridade](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance).)

**Monitor de integridade de acesso**

1. No console de administração, clique em Monitor de integridade no canto superior direito da página.
