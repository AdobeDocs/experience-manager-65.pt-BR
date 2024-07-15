---
title: Manutenção do registro de auditoria no AEM 6
description: Saiba mais sobre a Manutenção do log de auditoria no Adobe Experience Manager (AEM).
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: Operations
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# Manutenção do registro de auditoria no AEM 6{#audit-log-maintenance-in-aem}

Eventos AEM qualificados para registro de auditoria geram muitos dados arquivados. Esses dados podem crescer rapidamente com o tempo devido a replicações, uploads de ativos e outras atividades do sistema.

A Manutenção do registro de auditoria inclui várias partes da funcionalidade que permite a capacidade de automatizar a manutenção do registro de auditoria sob políticas específicas.

Ela é implementada como uma tarefa de manutenção semanal configurável e pode ser acessada por meio do console de monitoramento do Painel de operações.

Para obter mais informações, consulte a [Documentação do Painel de Operações](/help/sites-administering/operations-dashboard.md).

Há três tipos de opções de Expurgação de Log de Auditoria:

1. [Limpeza do log de auditoria da página](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Limpeza do log de auditoria do DAM](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Limpeza do Log de Auditoria de Replicação](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

Cada uma pode ser configurada criando regras no console da Web do AEM. Após a configuração, é possível acioná-los em **Ferramentas - Operações - Manutenção - Janela de Manutenção Semanal** e executando a **Tarefa de Manutenção do AuditLog**.

## Configurar a limpeza do log de auditoria da página {#configure-page-audit-log-purging}

Siga estas etapas para configurar a Expurgação de Log de Auditoria:

1. Vá para o Administrador do Console da Web apontando seu navegador para `http://localhost:4502/system/console/configMgr/`

1. Procure um item chamado **Regra de limpeza de log de auditoria de páginas** e clique nele.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. Em seguida, configure o programador de expurgação de acordo com suas necessidades. As opções disponíveis são:

   * **Nome da regra:** o nome da regra de política de auditoria;
   * **Caminho do conteúdo:** o caminho do conteúdo ao qual a regra será aplicada;
   * **Idade mínima:** o tempo em dias que os logs de auditoria precisam ser mantidos;
   * **Tipo de log de auditoria:** o tipo de log de auditoria que deve ser removido.

   >[!NOTE]
   >
   >O caminho de conteúdo se aplica somente aos filhos do nó `/var/audit/com.day.cq.wcm.core.page` no repositório.

1. Salve a regra.
1. A regra criada precisa ser exposta no Painel de operações para ser executada. Para fazer isso, acesse **Ferramentas - Operações - Manutenção** na tela de boas-vindas do AEM.

1. Pressione o cartão **Janela de manutenção semanal**.

1. Você encontrará a tarefa de manutenção já presente no cartão **Tarefa de manutenção do AuditLog**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Você pode inspecionar a data da próxima execução, configurá-la ou executá-la manualmente pressionando o botão Play.

No AEM 6.3, se a janela de manutenção programada for fechada antes que a tarefa de Expurgação de Log de Auditoria seja concluída, a tarefa será interrompida automaticamente. Ele será retomado quando a próxima janela de manutenção for aberta.

**Com o AEM 6.5**, é possível interromper manualmente uma Tarefa de Limpeza de Log de Auditoria em execução clicando no ícone **Parar**. Na próxima execução, a tarefa será retomada com segurança.

>[!NOTE]
>
>Interromper a tarefa de manutenção significa suspender sua execução sem perder o controle do trabalho já em andamento.

## Configurar a limpeza de log de auditoria do DAM {#configure-dam-audit-log-purging}

1. Navegue até o Console do Sistema em *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Procure a regra **Limpeza de log de auditoria do DAM** e clique no resultado.
1. Na próxima janela, configure sua regra de acordo. As opções são:

   * **Nome da regra:** o nome da regra de política de auditoria;
   * **Caminho do conteúdo:** o caminho do conteúdo ao qual a regra será aplicada
   * **Idade mínima:** o tempo em dias que os logs de auditoria precisam ser mantidos
   * **Tipos de evento DAM de Log de Auditoria:** os tipos de eventos de auditoria DAM que devem ser removidos.

1. Clique em **Salvar** para salvar sua configuração

## Configurar Limpeza do Log de Auditoria de Replicação  {#configure-replication-audit-log-purging}

1. Navegue até o Console do Sistema em *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Pesquise por **Agendador de Limpeza de Log de auditoria de replicação** e clique no resultado
1. Na próxima janela, configure sua regra de acordo. As opções são:

   * **Nome da regra:** o nome da regra de política de auditoria
   * **Caminho do conteúdo:** o caminho do conteúdo ao qual a regra será aplicada
   * **Idade mínima:** o tempo em dias que os logs de auditoria precisam ser mantidos
   * **Tipos de evento de Replicação de log de auditoria:** os tipos de eventos de auditoria de Replicação que devem ser removidos

1. Clique em **Salvar** para salvar sua configuração.
