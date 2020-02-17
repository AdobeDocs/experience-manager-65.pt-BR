---
title: Migração de conteúdo ociosa
seo-title: Migração de conteúdo ociosa
description: Saiba mais sobre a migração de conteúdo ocioso no AEM 6.4.
seo-description: Saiba mais sobre a migração de conteúdo ocioso no AEM 6.4.
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
translation-type: tm+mt
source-git-commit: 7d93df515bf98f0a947428b8093e059d63b21a34

---


# Migração de conteúdo ociosa {#lazy-content-migration}

Para fins de compatibilidade com versões anteriores, o conteúdo e a configuração em **/etc** e **/content** a partir do AEM 6.3 não serão tocados nem transformados imediatamente com a atualização. Isso é feito para garantir que as dependências dos aplicativos do cliente nessas estruturas permaneçam intactas. A funcionalidade relacionada a essas estruturas de conteúdo ainda é a mesma, mesmo que o conteúdo em um AEM 6.5 seja hospedado em outro lugar.

Embora nem todos esses locais possam ser transformados automaticamente, há alguns atrasos `CodeUpgradeTasks` também chamados de Migração de conteúdo ocioso. Isso permite que os clientes acionem essas transformações automáticas reiniciando a instância com esta propriedade do sistema:

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

Isso fará com que o teste seja executado durante `CodeUpgradeTasks` a migração.

Embora o objetivo seja uma execução eficiente, esse processo de atualização é síncrono e, portanto, vem com um tempo de inatividade dependendo da quantidade de conteúdo que precisa ser processada. É recomendável avaliar os tempos de execução em um ambiente de estágio antes de um sistema de produção para planejar uma janela de manutenção de acordo.

Como isso normalmente requer o ajuste do aplicativo, essa atividade deve ser executada junto com a implantação do aplicativo correspondente.

A lista completa de `CodeUpgradeTasks` medicamentos apresentada em 6.5 é a seguinte:

| **Nome** | **Relevante** **para versões do AEM anteriores a** | **** Tipo de migração **** | **Detalhes** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | Imediato |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | Imediato | Detecta todas as `LiveRelationShips` das `VersionStorage` que foram excluídas e adiciona a propriedade de exclusão ao pai |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | Imediato | Reestrutura serviços em nuvem para configuração segura por padrão |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | Imediato | Remove a vinculação baseada em propriedade de **/content** para **/conf** (substituída pelo mecanismo OSGi), gera a configuração OSGi correspondente |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | Imediato | Devido a merge_preserve, o gerenciamento da regra de negação segura por padrão substitui as permissões dadas, levando à necessidade de reordenar na atualização |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | Imediato | Detecta componentes que utilizam o widget Html5SmartFile, pesquisa por usos do componente na persistência do conteúdo e reestrutura, movendo efetivamente o nível binário para baixo e não armazená-lo no nível do componente. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | Imediato | Move projetos de estilo antigo de **/etc/projects** para **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | Imediato | Introduz uma camada de contêiner na hierarquia (Áreas) e ajusta as referências. |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | Imediato | Define nomes de localização fixos para componentes de destino. |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | Imediato | Transformação complexa de modelos de fluxo de trabalho que pré-datam estruturas 6.2, instâncias, notificações e, em seguida, mesclam de volta do local de backup de **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | Imediato | Move ativos, esquemas de metadados personalizados e perfis de processamento de **/apps** para **/conf** e converte os formulários de esquema de metadados e perfis de metadados de coral2 para coral3. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | Imediato | Move ativos e aspectos de pesquisa personalizados de **/apps** para **/conf** e converte os formulários de esquema de metadados e perfis de metadados de coral2 para coral3. |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | Imediato | Atualiza InboxItems para ordenar itens da caixa de entrada (ajustando metadados para classificação eficiente) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | Imediato | Ajusta a propriedade metadataSchema na pasta substituindo caminhos relativos para **/conf** no lugar de **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | Imediato | Ajustar a estrutura de navegação |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | Imediato | Move configurações personalizadas para painéis de monitoramento de **/libs** e **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | Imediato | Traduz a propriedade processingProfile (usada até 6.1) em Ativos para corresponder à estrutura 6.3 e posterior. Também ajusta os caminhos relativos do perfil para **/conf** no lugar de **/aplicativos**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | Imediato | Tarefa de atualização que remove entradas obsoletas do menu CRXDE Lite e Console da Web no caso de uma atualização. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | Atrasado | Mover configurações em nuvem do SRP, configurações de palavras de observação da comunidade, limpa **/etc/social** e **/etc/ativlement** (todas as referências e dados precisam ser ajustados quando a migração lenta for executada - nenhuma parte do aplicativo deve depender mais dessa estrutura). |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | Atrasado | Limpa **/etc/cloudsettings** (contendo a configuração do ContextHub). A configuração é automaticamente migrada no primeiro acesso. Caso a Migração de conteúdo lento seja iniciada juntamente com a atualização, esse conteúdo deve ser preservado em **/etc/cloudsettings** antes da atualização e reinstalado para que a transformação implícita seja iniciada, juntamente com uma desinstalação subsequente do pacote após a conclusão. |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | Atrasado | Ajusta a estrutura de título herdada ao título no nó do perfil do usuário. |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | Atrasado | Migre o conteúdo de comércio de **/etc/commerce** para **/var/commerce**. Durante a migração, o conteúdo é movido e as referências ao conteúdo movido são atualizadas para refletir o novo local. |
| `CQ65DMMigrationTask` | &lt; 6,5 | Atrasado | Migrar configurações de catálogo herdado e configurações de serviços de nuvem de mídia dinâmica de **/etc** para **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6,5 | Atrasado | Limpar clientlibs herdados existentes em **/etc/clientlibs** |
