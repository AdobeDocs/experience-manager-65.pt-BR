---
title: Migração de conteúdo ocioso
seo-title: Migração de conteúdo ocioso
description: Saiba mais sobre a migração de conteúdo lento no AEM 6.4.
seo-description: Saiba mais sobre a migração de conteúdo lento no AEM 6.4.
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
feature: Upgrading
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 6%

---


# Migração de conteúdo ocioso {#lazy-content-migration}

Para fins de compatibilidade com versões anteriores, o conteúdo e a configuração em **/etc** e **/content** a partir do AEM 6.3 não serão tocados ou transformados imediatamente com a atualização. Isso é feito para garantir que as dependências dos aplicativos do cliente nessas estruturas permaneçam intactas. A funcionalidade relacionada a essas estruturas de conteúdo ainda é a mesma, mesmo que o conteúdo em um AEM 6.5 pronto para uso seja hospedado em outro lugar.

Embora nem todos esses locais possam ser transformados automaticamente, há alguns `CodeUpgradeTasks` atrasados também conhecidos como Migração de conteúdo preguiçoso. Isso permite que os clientes acionem essas transformações automáticas, reiniciando a instância com essa propriedade do sistema:

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

Isso fará com que `CodeUpgradeTasks` seja executado durante a migração.

Embora o objetivo seja uma execução eficiente, esse processo de atualização é síncrono e, portanto, vem com um tempo de inatividade dependendo da quantidade de conteúdo que precisa ser processado. Recomenda-se avaliar os tempos de execução em um ambiente de estágio à frente de um sistema de produção para planejar uma janela de manutenção de acordo.

Como isso normalmente também requer o ajuste do aplicativo, essa atividade deve ser executada junto com a implantação do aplicativo correspondente.

Abaixo está a lista completa de `CodeUpgradeTasks` introduzida na versão 6.5:

| **Nome** | **** **Relevante para AEM versões anteriores a** | **** **MigrationType** | **Detalhes** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5=&quot;&quot;> | Imediato |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | Imediato | Detecta todos os `LiveRelationShips` de `VersionStorage` que foram excluídos e adiciona a propriedade de exclusão ao pai |
| `Cq61CloudServicesContentUpgrade` | &lt; 6=&quot;&quot;> | Imediato | Reestrutura serviços de nuvem para seguro por configuração padrão |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | Imediato | Remove a vinculação baseada em propriedade de **/content** para **/conf** (substituída pelo mecanismo OSGi), gera a configuração OSGi correspondente |
| `Cq62FormsContentUpgrade` | &lt; 6=&quot;&quot;> | Imediato | Devido a merge_preserve, manipulando as substituições da regra de negação segura por padrão, dadas permissões, resultando na necessidade de reordenar na atualização |
| `CQ62Html5SmartFileUpgrade` | &lt; 6=&quot;&quot;> | Imediato | Detecta componentes utilizando o widget Html5SmartFile, pesquisa por usos do componente na persistência de conteúdo e reestruturações, movendo efetivamente o nível binário para baixo e não o armazenando no nível do componente. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6=&quot;&quot;> | Imediato | Move projetos de estilo antigos de **/etc/projects** para **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6=&quot;&quot;> | Imediato | Introduz uma camada de contêiner na hierarquia (Áreas) e ajusta referências. |
| `Cq62TargetContentUpgrade` | &lt; 6=&quot;&quot;> | Imediato | Define nomes de localização fixos para componentes de destino. |
| `Cq62WorkflowContentUpgrade` | &lt; 6=&quot;&quot;> | Imediato | Transformação complexa de modelos de fluxo de trabalho que pré-datam estruturas, instâncias e notificações 6.2 e depois mesclam do local de backup de **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | Imediato | Move ativos, esquemas de metadados personalizados e perfis de processamento de **/apps** para **/conf** e converte o esquema de metadados e os formulários de perfis de metadados do coral2 para o coral3. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6=&quot;&quot;> | Imediato | Move ativos e aspectos de pesquisa personalizados de **/apps** para **/conf** e converte o esquema de metadados e os formulários de perfis de metadados do coral2 para o coral3. |
| `CQ63InboxItemsUpgrade` | &lt; 6=&quot;&quot;> | Imediato | Atualiza InboxItems para ordenar os itens da caixa de entrada (ajustando metadados para classificação eficiente) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6=&quot;&quot;> | Imediato | Ajusta a propriedade metadataSchema na pasta, substituindo os caminhos relativos para **/conf** no lugar de **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6=&quot;&quot;> | Imediato | Ajustar a estrutura de navegação |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6=&quot;&quot;> | Imediato | Move as configurações personalizadas para os painéis de monitoramento de **/libs** e **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6=&quot;&quot;> | Imediato | Traduz a propriedade processingProfile (usada até 6.1) no Assets para corresponder à estrutura 6.3 e posterior. Ajusta também os caminhos relativos do perfil para **/conf** no lugar de **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6=&quot;&quot;> | Imediato | Atualizar tarefa que remove entradas de menu obsoletas do CRXDE Lite e do Console da Web no caso de uma atualização. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6=&quot;&quot;> | Atrasado | Mover configurações de nuvem SRP, configurações de palavras de observação da comunidade, limpa **/etc/social** e **/etc/enablement** (quaisquer referências e dados precisam ser ajustados quando a migração lenta for executada - nenhuma parte do aplicativo deve depender mais dessa estrutura). |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | Atrasado | Limpa **/etc/cloudsettings** (contendo a configuração do ContextHub). A configuração é migrada automaticamente no primeiro acesso. Caso a Migração de conteúdo lento seja iniciada juntamente com a atualização, esse conteúdo em **/etc/cloudsettings** deve ser preservado por meio do pacote antes da atualização e reinstalado para que a transformação implícita seja iniciada, juntamente com uma desinstalação subsequente do pacote após a conclusão. |
| `CQ64UsersTitleFixTask` | &lt; 6=&quot;&quot;> | Atrasado | Ajusta a estrutura de título herdada para o título no nó do perfil do usuário. |
| `CQ64CommerceMigrationTask` | &lt; 6=&quot;&quot;> | Atrasado | Migre o conteúdo de comércio de **/etc/commerce** para **/var/commerce**. Durante a migração, o conteúdo é movido e as referências ao conteúdo movido são atualizadas para refletir o novo local. |
| `CQ65DMMigrationTask` | &lt; 6,5 | Atrasado | Migrar configurações de catálogo herdado e configurações do Dynamic Media Cloud Services de **/etc** para **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6,5 | Atrasado | Limpar clientlibs herdados existentes em **/etc/clientlibs** |
