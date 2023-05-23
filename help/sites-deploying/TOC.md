---
cloud: Experience Cloud
product: adobe experience manager
solution: Experience Manager, Experience Manager Sites
audience: end-user
user-guide-title: Guia de implementação do AEM 6.5
breadcrumb-title: Guia de implementação
user-guide-description: Saiba mais sobre a instalação, implantação e arquitetura do Adobe Experience Manager 6.5, incluindo a implantação do Adobe Managed Services na nuvem.
feature: Deploying
role: Architect
source-git-commit: f29612ee633d2a62144b770f3c225fc82b9174f8
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 12%

---


# Guia do usuário para implantação do AEM 6.5 {#deploying}

+ [Guia de implementação do usuário](home.md)
+ Introdução à plataforma AEM {#introduction}
   + [Introdução à plataforma AEM](platform.md)
   + [Requisitos técnicos](technical-requirements.md)
   + [Elementos de armazenamento no AEM 6.5](storage-elements-in-aem-6.md)
   + [AEM com MongoDB](aem-with-mongodb.md)
+ Implantação do AEM {#deploying}
   + [Implantação e manutenção](deploy.md)
   + [Implantações recomendadas](recommended-deploys.md)
   + [Instalação do Servidor de Aplicativos](application-server-install.md)
   + [Instalação Personalizada Independente](custom-standalone-install.md)
   + [Início e Interrupção da Linha de Comando](command-line-start-and-stop.md)
   + [Configuração de armazenamentos de nós e armazenamentos de dados no AEM 6](data-store-config.md)
   + [Limpeza de revisão](revision-cleanup.md)
   + [Consultas e indexação do Oak](queries-and-indexing.md)
   + [Como executar AEM com TarMK Cold Standby](tarmk-cold-standby.md)
   + [Suporte RDBMS no AEM 6.5](rdbms-support-in-aem.md)
   + [Indexação através do Oak-run Jar](indexing-via-the-oak-run-jar.md)
   + [Casos de uso de indexação do Oak-run.jar](oak-run-indexing-usecases.md)
   + [Solução de problemas de índices Oak](troubleshooting-oak-indexes.md)
   + [Ativando A Coleta De Estatísticas De Uso Agregado](opt-in-aggregated-usage-statistics.md)
   + [Resolução de problemas](troubleshooting.md)
+ Configuração do AEM {#configuring}
   + [Conceitos básicos de configuração](configuring.md)
   + [Logs](configure-logging.md)
   + [Configuração do OSGi](configuring-osgi.md)
   + [Configurações do OSGi](osgi-configuration-settings.md)
   + [Modos de execução](configure-runmodes.md)
   + [Console da Web](web-console.md)
   + [Replicação](replication.md)
   + [Replicação usando SSL mútuo](mssl-replication.md)
   + [Solução de problemas de replicação](troubleshoot-rep.md)
   + [Expiração de objetos estáticos](expiration-static-objects.md)
   + [Limpeza de versão](version-purging.md)
   + [Monitoramento e manutenção da instância do AEM](monitoring-and-maintaining.md)
   + [Descarregamento de trabalhos](offloading.md)
   + [Logon único](single-sign-on.md)
   + [Mapeamento de recursos](resource-mapping.md)
   + [Habilitar HTTP por SSL](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/ssl-by-default.html)
   + [Verificações de consistência e passagem](consistency-check.md)
   + [Diretrizes de desempenho](performance-guidelines.md)
   + [Otimização do desempenho](configuring-performance.md)
   + [Guia de desempenho de ativos](assets-performance-sizing.md)
   + [Artigos de instruções sobre configuração](ht-deploy.md)
   + [Configuração do console da Web](configuring-web-console.md)
+ Atualização para o AEM 6.5 {#upgrading}
   + [Atualização para o AEM 6.5](upgrade.md)
   + [Planejando sua atualização](upgrade-planning.md)
   + [Avaliando a complexidade da atualização com o Detector de padrões](pattern-detector.md)
   + [Compatibilidade com versões anteriores no AEM 6.5](backward-compatibility.md)
   + [Procedimento de atualização](upgrade-procedure.md)
   + [Execução de uma atualização no local](in-place-upgrade.md)
   + [Usar a reindexação offline para reduzir o tempo de inatividade durante uma atualização](upgrade-offline-reindexing.md)
   + [Migração de conteúdo lento](lazy-content-migration.md)
   + [Uso da ferramenta de migração CRX2Oak](using-crx2oak.md)
   + [Tarefas de Manutenção de Pré-Atualização](pre-upgrade-maintenance-tasks.md)
   + [Verificações pós-atualização e solução de problemas](post-upgrade-checks-and-troubleshooting.md)
   + [Atualização do Forms de pesquisa personalizada](upgrading-custom-search-forms.md)
   + [Atualizações sustentáveis](sustainable-upgrades.md)
   + [Atualização de código e personalizações](upgrading-code-and-customizations.md)
   + [Etapas de Atualização para Instalações de Servidor de Aplicativos](app-server-upgrade.md)
   + [Lista de pacotes obsoletos desinstalados após a atualização](obsolete-bundles.md)
+ Reestruturação do repositório {#restructuring}
   + [Reestruturação do repositório no AEM 6.5](repository-restructuring.md)
   + [Reestruturação do repositório comum no AEM 6.5](all-repository-restructuring-in-aem-6-5.md)
   + [Reestruturação do repositório de sites no AEM 6.5](sites-repository-restructuring-in-aem-6-5.md)
   + [Reestruturação do repositório de ativos no AEM 6.5](assets-repository-restructuring-in-aem-6-5.md)
   + [Reestruturação do repositório Dynamic Media no AEM 6.5](dynamicmedia-repository-restructuring-in-aem-6-5.md)
   + [Reestruturação do repositório Forms no AEM 6.5](forms-repository-restructuring-in-aem-6-5.md)
   + [Reestruturação do repositório de comércio eletrônico no AEM 6.5](ecommerce-repository-restructuring-in-aem-6-5.md)
   + [Reestruturação do repositório para o AEM Communities no 6.5](communities-repository-restructuring-in-aem-6-5.md)
+ Práticas recomendadas     {#practices}
   + [Implantação de práticas recomendadas](best-practices.md)
   + [Árvore de desempenho](performance-tree.md)
   + [Práticas recomendadas para testes de desempenho](best-practices-for-performance-testing.md)
   + [Práticas recomendadas para consultas e indexação](best-practices-for-queries-and-indexing.md)
   + [Interface do usuário do Recommendations para clientes](ui-recommendations.md)
   + [Desempenho e escalabilidade](performance.md)
