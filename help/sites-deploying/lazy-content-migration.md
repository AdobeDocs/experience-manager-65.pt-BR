---
title: Migração de conteúdo lento
description: Saiba mais sobre a Migração de conteúdo lento no Adobe Experience Manager 6.4.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: 946c7c2a-806b-4461-a38b-9c2e5ef1e958
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 2%

---

# Migração de conteúdo lento {#lazy-content-migration}

Por motivos de compatibilidade com versões anteriores, conteúdo e configuração no **/etc** e **/content** a partir do Adobe Experience Manager (AEM) 6.3, não serão tocados ou transformados imediatamente com a atualização. Isso é feito para garantir que as dependências dos aplicativos do cliente nessas estruturas permaneçam intactas. A funcionalidade relacionada a essas estruturas de conteúdo ainda é a mesma, mesmo que o conteúdo de um AEM 6.5 pronto para uso seja hospedado em outro lugar.

Embora nem todos esses locais possam ser transformados automaticamente, há alguns atrasados `CodeUpgradeTasks` também chamada de Migração de conteúdo lento. Isso permite que os clientes acionem essas transformações automáticas reiniciando a instância com esta propriedade do sistema:

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

Isso faz com que a `CodeUpgradeTasks` a ser executado durante a migração.

Embora o objetivo seja uma execução eficiente, esse processo de atualização é síncrono e, portanto, vem com um tempo de inatividade dependendo da quantidade de conteúdo que deve ser processado. a Adobe recomenda avaliar os tempos de execução em um ambiente de preparo antes de um sistema de produção para planejar uma janela de manutenção de acordo.

Como isso normalmente também requer o ajuste do aplicativo, essa atividade deve ser executada junto com a implantação do aplicativo correspondente.

Abaixo está a lista completa de `CodeUpgradeTasks` introduzido no ponto 6.5:

| **Nome** | **Relevante** **para versões AEM anteriores** | **Migração** **Tipo** | **Detalhes** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | Imediato |  |
| `Cq60MSMContentUpgrade` | &lt; 6,0 | Imediato | Detecta tudo `LiveRelationShips` de `VersionStorage` que foram excluídas e adicionar a propriedade de exclusão ao pai |
| `Cq61CloudServicesContentUpgrade` | &lt; 6,1 | Imediato | Reestrutura serviços em nuvem para segurança por configuração padrão |
| `Cq62ConfContentUpgrade` | &lt; 6,2 | Imediato | Remove o vínculo baseado em propriedade de **/content** para **/conf** (substituído pelo mecanismo OSGi), gera a configuração OSGi correspondente |
| `Cq62FormsContentUpgrade` | &lt; 6,2 | Imediato | Devido ao manuseio merge_preserve, a regra de negação segura por padrão substitui as permissões fornecidas, resultando na necessidade de reordenar na atualização |
| `CQ62Html5SmartFileUpgrade` | &lt; 6,2 | Imediato | Detecta componentes usando o widget Html5SmartFile, pesquisa usos do componente no conteúdo e reestrutura a persistência, efetivamente movendo o binário um nível para baixo e não armazená-lo no nível do componente. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6,2 | Imediato | Move projetos de estilo antigos de **/etc/projects** para **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6,2 | Imediato | Introduz uma camada de contêiner na hierarquia (Áreas) e ajusta as referências. |
| `Cq62TargetContentUpgrade` | &lt; 6,2 | Imediato | Define nomes de localização fixos para os componentes de destino. |
| `Cq62WorkflowContentUpgrade` | &lt; 6,2 | Imediato | Transformação complexa de modelos de fluxo de trabalho anteriores a 6.2 estruturas, instâncias, notificações e, em seguida, mesclagem do local de backup de **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6,3 | Imediato | Move ativos, esquemas de metadados personalizados e perfis de processamento do **/apps** para **/conf** e traduz o esquema de metadados e os formulários de perfis de metadados de coral2 para coral3. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6,3 | Imediato | Move ativos e aspectos de pesquisa personalizados de **/apps** para **/conf** e traduz o esquema de metadados e os formulários de perfis de metadados de coral2 para coral3. |
| `CQ63InboxItemsUpgrade` | &lt; 6,3 | Imediato | Atualiza InboxItems para ordenar itens da caixa de entrada (ajustando metadados para uma classificação eficiente) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6,3 | Imediato | Ajusta a propriedade metadataSchema na pasta substituindo caminhos relativos a **/conf** em vez de **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6,3 | Imediato | Ajuste da estrutura de navegação |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6,3 | Imediato | Move as configurações personalizadas para os painéis de monitoramento de **/libs** e **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6,3 | Imediato | Traduz a propriedade processingProfile (usada até a versão 6.1) no Assets para corresponder à estrutura da versão 6.3 e posterior. Também ajusta os caminhos relativos do perfil para **/conf** em vez de **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6,3 | Imediato | Tarefa de atualização que remove entradas de menu obsoletas do CRXDE Lite e do Console da Web se houver uma atualização. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6,3 | Atrasado | Movimentação de configurações de nuvem SRP, configurações de palavras de observação da comunidade, limpezas **/etc/social** e **/etc/enablement** (quaisquer referências e dados devem ser ajustados quando a migração lenta for executada; nenhuma parte do aplicativo deve depender mais dessa estrutura). |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6,4 | Atrasado | Limpa **/etc/cloudsettings** (contendo configuração do ContextHub). A configuração é migrada automaticamente no primeiro acesso. Caso a Migração de conteúdo lento seja iniciada junto com a atualização desse conteúdo no **/etc/cloudsettings** deve ser preservado por meio do pacote antes da atualização e reinstalado para que a transformação implícita seja iniciada, juntamente com uma desinstalação subsequente do pacote após a conclusão. |
| `CQ64UsersTitleFixTask` | &lt; 6,4 | Atrasado | Ajusta a estrutura de título herdada ao título no nó do perfil do usuário. |
| `CQ64CommerceMigrationTask` | &lt; 6,4 | Atrasado | Migrar conteúdo comercial de **/etc/commerce** para **/var/commerce**. Durante a migração, o conteúdo é movido e as referências ao conteúdo movido são atualizadas para refletir o novo local. |
| `CQ65DMMigrationTask` | &lt; 6,5 | Atrasado | Migrar configurações do catálogo herdado e configurações do Dynamic Media Cloud Service de **/etc** para **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6,5 | Atrasado | Limpar clientlibs herdadas existentes em **/etc/clientlibs** |
