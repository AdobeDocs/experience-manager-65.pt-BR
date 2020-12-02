---
title: Manutenção do registro de auditoria no AEM 6
seo-title: Manutenção do registro de auditoria no AEM 6
description: Saiba mais sobre a manutenção do registro de auditoria em AEM.
seo-description: Saiba mais sobre a manutenção do registro de auditoria em AEM.
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---


# Manutenção do Log de Auditoria no AEM 6{#audit-log-maintenance-in-aem}

AEM eventos qualificados para registro de auditoria geram muitos dados arquivados. Esses dados podem crescer rapidamente com o tempo devido a replicações, uploads de ativos e outras atividades do sistema.

A Manutenção do registro de auditoria inclui várias partes da funcionalidade que permite automatizar a manutenção do registro de auditoria de acordo com políticas específicas.

Ele é implementado como uma tarefa de manutenção semanal configurável e pode ser acessado pelo console de monitoramento do Operations Painel.

Para obter mais informações, consulte a [Documentação do Painel de Operações](/help/sites-administering/operations-dashboard.md).

Existem três tipos de opções de Expurgação do Log de Auditoria:

1. [Expurgação do Log de Auditoria da Página](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Expurgação do Log de Auditoria do DAM](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Cálculo do Log de Auditoria de Replicação](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

Cada um pode ser configurado criando regras no Console da Web AEM. Depois de configurados, você pode acioná-los indo até **Ferramentas - Operações - Manutenção - Janela de manutenção semanal** e executando a **Tarefa de manutenção do AuditLog**.

## Configurar a Limpeza do Log de Auditoria de Página {#configure-page-audit-log-purging}

Siga estas etapas para configurar a Expurgação do Log de Auditoria:

1. Vá para o Admin do Console Web apontando seu navegador para `http://localhost:4502/system/console/configMgr/`

1. Procure um item chamado **Regra de Expurgação do Log de Auditoria de Páginas** e clique nele.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. Em seguida, configure o scheduler de expurgação de acordo com seus requisitos. As opções disponíveis são:

   * **Nome da regra:** o nome da regra da política de auditoria;
   * **Caminho do conteúdo:** o caminho do conteúdo ao qual a regra será aplicada;
   * **Idade mínima:** o tempo em dias em que os registros de auditoria devem ser conservados;
   * **Tipo de log de auditoria:** o tipo de log de auditoria que deve ser removido.

   >[!NOTE]
   >
   >O caminho do conteúdo se aplica somente aos filhos do nó `/var/audit/com.day.cq.wcm.core.page` no repositório.

1. Salve a regra.
1. A regra que você acabou de criar precisa ser exposta no Painel Operações para que seja executada. Para fazer isso, vá **Ferramentas - Operações - Manutenção** da tela de boas-vindas AEM.

1. Pressione a placa **Janela de manutenção semanal**.

1. Você encontrará a tarefa de manutenção já presente na placa **Tarefa de manutenção do AuditLog**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Você pode inspecionar a data da próxima execução, configurá-la ou executá-la manualmente pressionando o botão play.

No AEM 6.3, se a janela de manutenção programada for fechada antes que a tarefa de Expurgação do Log de Auditoria possa ser concluída, a tarefa será interrompida automaticamente. Ele será retomado quando a próxima janela de manutenção for aberta.

**Com AEM 6.5**, você pode interromper manualmente uma Tarefa de Expurgação do Log de Auditoria em execução clicando no  **** Stopicon. Na próxima execução, a tarefa será retomada com segurança.

>[!NOTE]
>
>Parar a tarefa de manutenção significa suspender sua execução sem perder o controle da tarefa já em andamento.

## Configurar a depuração do registro de auditoria do DAM {#configure-dam-audit-log-purging}

1. Navegue até o console do sistema em *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Procure a regra **Expurgação do Log de auditoria do DAM** e clique no resultado.
1. Na próxima janela, configure sua regra de acordo. As opções são:

   * **Nome da regra:** o nome da regra da política de auditoria;
   * **Caminho do conteúdo:** o caminho do conteúdo ao qual a regra será aplicada
   * **Idade mínima:** o tempo em dias que os registros de auditoria precisam ser mantidos
   * **Tipos de evento de barragem de registro de auditoria:** os tipos de eventos de auditoria DAM que devem ser removidos.

1. Clique em **Salvar** para salvar sua configuração

## Configurar a Limpeza do Log de Auditoria de Replicação {#configure-replication-audit-log-purging}

1. Navegue até o console do sistema em *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Procure **Scheduler de Expurgação do Log de Auditoria de Replicação** e clique no resultado
1. Na próxima janela, configure sua regra de acordo. As opções são:

   * **Nome da regra:** o nome da regra da política de auditoria
   * **Caminho do conteúdo:** o caminho do conteúdo ao qual a regra será aplicada
   * **Idade mínima:** o tempo em dias que os registros de auditoria precisam ser mantidos
   * **Tipos de evento de Replicação de Log de Auditoria:** os tipos de eventos de auditoria Replicação que devem ser removidos

1. Clique em **Salvar** para salvar sua configuração.

