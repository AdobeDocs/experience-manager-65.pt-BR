---
title: Manutenção do registro de auditoria no AEM 6
seo-title: Audit Log Maintenance in AEM 6
description: Saiba mais sobre a manutenção do log de auditoria no AEM.
seo-description: Lear about Audit Log Maintenance in AEM.
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: Operations
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# Manutenção do registro de auditoria no AEM 6{#audit-log-maintenance-in-aem}

AEM eventos qualificados para registro de auditoria geram muitos dados arquivados. Esses dados podem crescer rapidamente ao longo do tempo devido a replicações, uploads de ativos e outras atividades do sistema.

A Manutenção do log de auditoria inclui várias partes da funcionalidade que permite automatizar a manutenção do log de auditoria de acordo com políticas específicas.

Ele é implementado como uma tarefa de manutenção semanal configurável e pode ser acessada por meio do console de monitoramento do Painel de Operações.

Para obter mais informações, consulte [Documentação do Painel de operações](/help/sites-administering/operations-dashboard.md).

Existem três tipos de opções de Expurgação de Log de Auditoria:

1. [Limpeza do log de auditoria da página](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Limpeza do log de auditoria do DAM](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Paginação do Log de Auditoria de Replicação](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

Cada uma pode ser configurada criando regras no Console da Web AEM. Depois que tiverem sido configurados, é possível acioná-los indo até **Ferramentas - Operações - Manutenção - Janela de manutenção semanal** e executar o **Tarefa de Manutenção AuditLog**.

## Configurar a limpeza do log de auditoria da página {#configure-page-audit-log-purging}

Siga estas etapas para configurar a limpeza do log de auditoria:

1. Acesse o administrador do console da Web, apontando seu navegador para `http://localhost:4502/system/console/configMgr/`

1. Pesquisar por um item chamado **Regra de limpeza do log de auditoria de páginas** e clique nele.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. Em seguida, configure o programador de limpeza de acordo com seus requisitos. As opções disponíveis são:

   * **Nome da regra:** O nome da regra da política de auditoria;
   * **Caminho do conteúdo:** o caminho do conteúdo ao qual a regra será aplicada;
   * **Idade mínima:** O tempo em dias que os registros de auditoria devem ser mantidos;
   * **Tipo de log de auditoria:** o tipo de log de auditoria que deve ser removido.

   >[!NOTE]
   >
   >O caminho de conteúdo se aplica somente aos filhos da variável `/var/audit/com.day.cq.wcm.core.page` no repositório.

1. Salve a regra.
1. A regra que você acabou de criar precisa ser exposta no Painel de operações para que seja executada. Para fazer isso, acesse **Ferramentas - Operações - Manutenção** na tela AEM Welcome .

1. Pressione a tecla **Janela de manutenção semanal** cartão.

1. Você encontrará a tarefa de manutenção já presente no **Tarefa de Manutenção AuditLog** cartão.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Você pode inspecionar a data da próxima execução, configurá-la ou executá-la manualmente pressionando o botão Reproduzir.

No AEM 6.3, se a janela de manutenção agendada for fechada antes que a tarefa de limpeza do log de auditoria possa ser concluída, a tarefa será interrompida automaticamente. Ele será retomado quando a próxima janela de manutenção for aberta.

**Com AEM 6.5**, você pode interromper manualmente uma Tarefa de limpeza do log de auditoria em execução clicando no botão **Stop** ícone . Na próxima execução, a tarefa será retomada com segurança.

>[!NOTE]
>
>Parar a tarefa de manutenção significa suspender sua execução sem perder o controle da tarefa já em andamento.

## Configurar limpeza do log de auditoria do DAM {#configure-dam-audit-log-purging}

1. Navegue até o console do sistema em *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Procurar por **Limpeza de log de auditoria do DAM** e clique no resultado.
1. Na próxima janela, configure a regra adequadamente. As opções são:

   * **Nome da regra:** O nome da regra da política de auditoria;
   * **Caminho do conteúdo:** o caminho do conteúdo ao qual a regra será aplicada
   * **Idade mínima:** o tempo em dias que os logs de auditoria precisam ser mantidos
   * **Tipos de evento de Dam de Log de Auditoria:** os tipos de eventos de auditoria do DAM que devem ser removidos.

1. Clique em **Salvar** para salvar sua configuração

## Configurar limpeza do log de auditoria de replicação  {#configure-replication-audit-log-purging}

1. Navegue até o console do sistema em *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Procurar por **Scheduler de limpeza do log de auditoria de replicação** e clique no resultado
1. Na próxima janela, configure a regra adequadamente. As opções são:

   * **Nome da regra:** o nome da regra da política de auditoria
   * **Caminho do conteúdo:** o caminho do conteúdo ao qual a regra será aplicada
   * **Idade mínima:** o tempo em dias que os logs de auditoria precisam ser mantidos
   * **Tipos de evento de Replicação de log de auditoria:** os tipos de eventos de auditoria de Replicação que devem ser removidos

1. Clique em **Salvar** para salvar sua configuração.
