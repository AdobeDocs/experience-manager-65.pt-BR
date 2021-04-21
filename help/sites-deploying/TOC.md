---
cloud: Experience Cloud
product: adobe experience manager
solution: Experience Manager, Experience Manager Sites
audience: end-user
user-guide-title: Guia de implementação do AEM 6.5
breadcrumb-title: Guia de implementação
user-guide-description: Saiba mais sobre a instalação, implantação e arquitetura do Adobe Experience Manager 6.5, incluindo a implantação do Adobe Managed Services na nuvem.
feature: Implantação
role: Architect
translation-type: tm+mt
source-git-commit: ad67634278088f8f953fde61a3543acdd70537dd
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 18%

---


# AEM 6.5 Guia de implantação do usuário {#deploying}

+ [Guia de implantação do usuário](home.md)
+ Introdução à plataforma de AEM {#introduction}
   + [Introdução à plataforma de AEM](platform.md)
   + [Requisitos técnicos](technical-requirements.md)
   + [Elementos de armazenamento no AEM 6.5](storage-elements-in-aem-6.md)
   + [AEM com MongoDB](aem-with-mongodb.md)
+ Implantar AEM {#deploying}
   + [Implantação e manutenção](deploy.md)
   + [Implantações recomendadas](recommended-deploys.md)
   + [Instalação do servidor de aplicativos](application-server-install.md)
   + [Instalação independente personalizada](custom-standalone-install.md)
   + [Início e interrupção da linha de comando](command-line-start-and-stop.md)
   + [Configuração de armazenamentos de nó e armazenamentos de dados no AEM 6](data-store-config.md)
   + [Limpeza de revisão](revision-cleanup.md)
   + [Consultas e indexação do Oak](queries-and-indexing.md)
   + [Como executar AEM com o TarMK Cold Standby](tarmk-cold-standby.md)
   + [Suporte RDBMS no AEM 6.5](rdbms-support-in-aem.md)
   + [Indexação via Jar Oak-run](indexing-via-the-oak-run-jar.md)
   + [Casos de uso da indexação Oak-run.jar](oak-run-indexing-usecases.md)
   + [Solução de problemas de índices do Oak](troubleshooting-oak-indexes.md)
   + [Aceitação Em Coleta De Estatísticas De Uso Agregado](opt-in-aggregated-usage-statistics.md)
   + [Resolução de Problemas](troubleshooting.md)
+ Configurar AEM {#configuring}
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
   + [Monitorar e manter sua instância do AEM](monitoring-and-maintaining.md)
   + [Descarregamento de Tarefas](offloading.md)
   + [Logon único](single-sign-on.md)
   + [Mapeamento de recursos](resource-mapping.md)
   + [Habilitar HTTP por SSL](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/ssl-by-default.html)
   + [Verificações de consistência e passagem](consistency-check.md)
   + [Diretrizes de desempenho](performance-guidelines.md)
   + [Otimização de desempenho](configuring-performance.md)
   + [Guia de desempenho de ativos](assets-performance-sizing.md)
   + [Artigos explicativos de configuração](ht-deploy.md)
   + [Configuração do Console da Web](configuring-web-console.md)
+ Atualização para AEM 6.5 {#upgrading}
   + [Atualização para o AEM 6.5](upgrade.md)
   + [Planejamento da atualização](upgrade-planning.md)
   + [Avaliação da complexidade da atualização com o Detector de padrões](pattern-detector.md)
   + [Compatibilidade com versões anteriores no AEM 6.5](backward-compatibility.md)
   + [Procedimento de atualização](upgrade-procedure.md)
   + [Execução de uma atualização no local](in-place-upgrade.md)
   + [Usar a reindexação offline para reduzir o tempo de inatividade durante uma atualização](upgrade-offline-reindexing.md)
   + [Migração de conteúdo ocioso](lazy-content-migration.md)
   + [Uso da ferramenta de migração CRX2Oak](using-crx2oak.md)
   + [Tarefas de manutenção de pré-atualização](pre-upgrade-maintenance-tasks.md)
   + [Verificação e solução de problemas da pós-atualização](post-upgrade-checks-and-troubleshooting.md)
   + [Atualizar o Forms de pesquisa personalizada](upgrading-custom-search-forms.md)
   + [Atualizações sustentáveis](sustainable-upgrades.md)
   + [Atualização de código e personalizações](upgrading-code-and-customizations.md)
   + [Etapas de atualização para instalações do servidor de aplicativos](app-server-upgrade.md)
   + [Lista de pacotes obsoletos desinstalados após a atualização](obsolete-bundles.md)
+ Reestruturação do Repositório {#restructuring}
   + [Reestruturação do repositório no AEM 6.5](repository-restructuring.md)
   + [Reestruturação comum de repositório no AEM 6.5](all-repository-restructuring-in-aem-6-5.md)
   + [Restruturação do repositório de sites no AEM 6.5](sites-repository-restructuring-in-aem-6-5.md)
   + [Reestruturação do repositório de ativos no AEM 6.5](assets-repository-restructuring-in-aem-6-5.md)
   + [Reestruturação do repositório Dynamic Media no AEM 6.5](dynamicmedia-repository-restructuring-in-aem-6-5.md)
   + [Reestruturação do repositório Forms no AEM 6.5](forms-repository-restructuring-in-aem-6-5.md)
   + [Reestruturação do repositório de comércio eletrônico no AEM 6.5](ecommerce-repository-restructuring-in-aem-6-5.md)
   + [Reestruturação do repositório para AEM Communities no 6.5](communities-repository-restructuring-in-aem-6-5.md)
+ eCommerce {#ecommerce}
   + [Visão geral do eCommerce](ecommerce.md)
   + [Commerce Cloud SAP](sap-commerce-cloud.md)
   + [Salesforce Commerce Cloud](https://github.com/adobe/commerce-salesforce)
   + [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)
+ Práticas recomendadas     {#practices}
   + [Práticas recomendadas de implantação](best-practices.md)
   + [Árvore de desempenho](performance-tree.md)
   + [Práticas recomendadas para testes de desempenho](best-practices-for-performance-testing.md)
   + [Práticas recomendadas para consultas e indexação](best-practices-for-queries-and-indexing.md)
   + [Recommendations da interface do usuário para clientes](ui-recommendations.md)
   + [Desempenho e escalabilidade](performance.md)
