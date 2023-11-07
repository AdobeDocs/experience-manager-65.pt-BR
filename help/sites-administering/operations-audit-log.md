---
title: Manutenção do registro de auditoria no AEM 6
seo-title: Audit Log Maintenance in AEM 6
description: Saiba mais sobre a Manutenção do log de auditoria no Adobe Experience Manager (AEM).
seo-description: Learn about Audit Log Maintenance in Adobe Experience Manager (AEM).
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: Operations
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# Manutenção do registro de auditoria no AEM 6{#audit-log-maintenance-in-aem}

Eventos AEM qualificados para registro de auditoria geram muitos dados arquivados. Esses dados podem crescer rapidamente com o tempo devido a replicações, uploads de ativos e outras atividades do sistema.

A Manutenção do registro de auditoria inclui várias partes da funcionalidade que permite a capacidade de automatizar a manutenção do registro de auditoria sob políticas específicas.

Ela é implementada como uma tarefa de manutenção semanal configurável e pode ser acessada por meio do console de monitoramento do Painel de operações.

Para obter mais informações, consulte [Documentação do Painel de Operações](/help/sites-administering/operations-dashboard.md).

Há três tipos de opções de Expurgação de Log de Auditoria:

1. [Limpeza do log de auditoria da página](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Limpeza do log de auditoria do DAM](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Limpeza do Log de Auditoria de Replicação](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

Cada uma pode ser configurada criando regras no console da Web do AEM. Após a configuração, é possível acioná-los acessando **Ferramentas - Operações - Manutenção - Janela de manutenção semanal** e a execução da **Tarefa de manutenção do AuditLog**.

## Configurar a limpeza do log de auditoria da página {#configure-page-audit-log-purging}

Siga estas etapas para configurar a Expurgação de Log de Auditoria:

1. Vá para o Administrador do console da Web apontando seu navegador para `http://localhost:4502/system/console/configMgr/`

1. Pesquisar um item chamado **Regra de limpeza de log de auditoria de páginas** e clique nela.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. Em seguida, configure o programador de expurgação de acordo com suas necessidades. As opções disponíveis são:

   * **Nome da regra:** o nome da regra de política de auditoria;
   * **Caminho do conteúdo:** o caminho do conteúdo ao qual a regra será aplicada;
   * **Idade mínima:** o tempo, em dias, durante o qual os registros de auditoria têm de ser mantidos;
   * **Tipo de log de auditoria:** o tipo de log de auditoria que deve ser removido.

   >[!NOTE]
   >
   >O caminho do conteúdo se aplica somente aos filhos de `/var/audit/com.day.cq.wcm.core.page` no repositório.

1. Salve a regra.
1. A regra criada precisa ser exposta no Painel de operações para ser executada. Para fazer isso, acesse **Ferramentas - Operações - Manutenção** na tela de boas-vindas AEM.

1. Pressione a **Janela de manutenção semanal** cartão.

1. Você encontrará a tarefa de manutenção já presente no **Tarefa de manutenção do AuditLog** cartão.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Você pode inspecionar a data da próxima execução, configurá-la ou executá-la manualmente pressionando o botão Play.

No AEM 6.3, se a janela de manutenção programada for fechada antes que a tarefa de Expurgação de Log de Auditoria seja concluída, a tarefa será interrompida automaticamente. Ele será retomado quando a próxima janela de manutenção for aberta.

**Com AEM 6.5**, você pode interromper manualmente uma Tarefa de Expurgação de Log de Auditoria em execução clicando no **Parar** ícone. Na próxima execução, a tarefa será retomada com segurança.

>[!NOTE]
>
>Interromper a tarefa de manutenção significa suspender sua execução sem perder o controle do trabalho já em andamento.

## Configurar a limpeza de log de auditoria do DAM {#configure-dam-audit-log-purging}

1. Navegue até o console do sistema em *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Pesquisar por **Limpeza do log de auditoria do DAM** e clique no resultado.
1. Na próxima janela, configure sua regra de acordo. As opções são:

   * **Nome da regra:** o nome da regra de política de auditoria;
   * **Caminho do conteúdo:** o caminho do conteúdo ao qual a regra será aplicada
   * **Idade mínima:** o tempo em dias em que os logs de auditoria precisam ser mantidos
   * **Tipos de evento do DAM de Log de Auditoria:** os tipos de eventos de auditoria do DAM que devem ser removidos.

1. Clique em **Salvar** para salvar sua configuração

## Configurar Limpeza do Log de Auditoria de Replicação  {#configure-replication-audit-log-purging}

1. Navegue até o console do sistema em *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Pesquisar por **Agendador de Limpeza de Log de auditoria de replicação** e clique no resultado
1. Na próxima janela, configure sua regra de acordo. As opções são:

   * **Nome da regra:** o nome da regra de política de auditoria
   * **Caminho do conteúdo:** o caminho do conteúdo ao qual a regra será aplicada
   * **Idade mínima:** o tempo em dias em que os logs de auditoria precisam ser mantidos
   * **Tipos de evento de Replicação de log de auditoria:** os tipos de eventos de auditoria de Replicação que devem ser removidos

1. Clique em **Salvar** para salvar sua configuração.
