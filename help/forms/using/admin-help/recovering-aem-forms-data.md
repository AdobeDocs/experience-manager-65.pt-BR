---
title: Recuperação dos dados de formulários de AEM
seo-title: Recovering the AEM forms data
description: Este documento descreve as etapas necessárias para recuperar os dados dos formulários de AEM.
seo-description: This document describes the steps required to recover the AEM forms data.
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
exl-id: 9e648bab-9284-4fda-abb4-8bd7cd085981
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 0%

---

# Recuperação dos dados de formulários de AEM {#recovering-the-aem-forms-data}

Esta seção descreve as etapas necessárias para recuperar os dados dos formulários AEM. Consulte também [Considerações especiais para backup e recuperação](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>O banco de dados, GDS, repositório AEM e diretórios raiz do armazenamento de conteúdo devem ser restaurados para um computador com o mesmo nome DNS do original.

Os formulários AEM devem se recuperar com confiança das seguintes falhas:

**Falha do disco:** A mídia de backup mais recente é necessária para recuperar o conteúdo do banco de dados.

**Corrupção de dados:** Os sistemas de arquivos não registram transações anteriores e os sistemas podem substituir acidentalmente os dados necessários do processo.

**Erro do usuário:** A recuperação está limitada aos dados disponibilizados pelo banco de dados. Se os dados foram armazenados e estão disponíveis, a recuperação é simplificada.

**Interrupção de energia, falha do sistema:** As APIs do sistema de arquivos geralmente não são projetadas ou usadas de forma robusta, o que protege contra falhas inesperadas do sistema. Se ocorrer uma falha de energia ou do sistema, o conteúdo do documento armazenado no banco de dados provavelmente estará atualizado em relação ao conteúdo armazenado em um sistema de arquivos.

Se estiver usando o modo de backup contínuo, você ainda estará no modo de backup após a recuperação. Se estiver usando o modo de backup de snapshot, você não estará no modo de backup após a recuperação.

Ao restaurar do backup para um novo sistema, as seguintes configurações podem ser diferentes. Essa diferença não deve afetar uma recuperação bem-sucedida do aplicativo AEM forms:

* Endereço IP
* Configuração física do sistema (CPUs, disco, memória)
* Localização GDS

>[!NOTE]
>
>O backup do diretório raiz do armazenamento de conteúdo deve ser restaurado para o local desse diretório, como foi definido durante a configuração dos Serviços de conteúdo.

Se um único nó de um cluster de vários nós falhar e os nós restantes do cluster estiverem funcionando corretamente, execute o procedimento de recuperação de nó único do cluster.

## Recuperar os dados dos formulários de AEM {#recover-the-aem-forms-data}

1. Pare os serviços de formulários AEM e o servidor de aplicativos se estiver em execução.
1. Se necessário, recrie o sistema físico a partir de uma imagem do sistema. Por exemplo, essa etapa pode não ser necessária se o motivo da recuperação for um servidor de banco de dados com falha.
1. Aplique patches ou atualizações AEM formulários que foram aplicados desde que a imagem foi feita. Essas informações foram registradas no procedimento de backup. AEM formulários devem ser corrigidos no mesmo nível de patch que no momento em que o backup do sistema foi feito.
1. (WebSphere Application Server) Se estiver se recuperando para uma nova instância do WebSphere Application Server, execute o comando restoreConfig.bat/sh.
1. Recupere o banco de dados de formulários de AEM executando primeiro uma operação de restauração de banco de dados usando os arquivos de backup do banco de dados e aplicando os redo logs de transação ao banco de dados recuperado. (Consulte [Banco de dados de formulários AEM](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Para obter mais informações, consulte um destes artigos da base de conhecimento:

   * [Backup e recuperação do Oracle para formulários AEM](https://www.adobe.com/go/kb403624)
   * [Backup e recuperação do MySQL para formulários AEM](https://www.adobe.com/go/kb403625)
   * [Backup e recuperação do Microsoft SQL Server para formulários AEM](https://www.adobe.com/go/kb403623)
   * [Backup e recuperação do DB2 para formulários AEM](https://www.adobe.com/go/kb403626)

1. Recupere o diretório GDS primeiro excluindo o conteúdo do diretório GDS na instalação existente de formulários AEM e copiando o conteúdo do diretório GDS do GDS com backup. Se você alterou o local do diretório GDS, consulte [Alteração da localização do GDS durante a recuperação](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. Renomeie o diretório de backup GDS a ser restaurado, conforme mostrado nestes exemplos:

   >[!NOTE]
   >
   >Se o diretório /restore já existir, faça o backup e depois o exclua antes de renomear o diretório /backup que contém os dados mais recentes.

   * (JBoss) Renomear `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` para:

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * (WebLogic) Renomear `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` para:

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere) Renomear `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` para:

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. Recupere o diretório raiz do armazenamento de conteúdo excluindo primeiro o conteúdo do diretório raiz do armazenamento de conteúdo na instalação existente de formulários AEM e recuperando o conteúdo seguindo as tarefas de ambientes autônomos ou em cluster:

   >[!NOTE]
   >
   >O backup do diretório raiz do armazenamento de conteúdo deve ser restaurado para o local do diretório raiz do armazenamento de conteúdo, pois foi definido durante a configuração do Content Services (obsoleto).

   **Independente:** Durante o processo de recuperação, restaure todos os diretórios que foram submetidos a backup. Quando esses diretórios forem restaurados, se o diretório /backup-lucene-indexes estiver presente, renomeie-o para /lucene-indexes. Caso contrário, o diretório lucene-indexes já deve existir e nenhuma ação é necessária.

   **Em cluster:** Durante o processo de recuperação, restaure todos os diretórios que foram submetidos a backup. Para restaurar o diretório Raiz do Índice, execute as seguintes etapas em cada nó do cluster:

   * Exclua todo o conteúdo do diretório Raiz de índice.
   * Se o diretório /backup-lucene-indexes estiver presente, copie o conteúdo da variável *Diretório raiz do armazenamento de conteúdo*/backup-lucene-indexes diretory para o diretório Raiz do Índice e exclua o *Diretório raiz do armazenamento de conteúdo* diretório /backup-lucene-indexes.
   * Se o diretório /lucene-indexes estiver presente, copie o conteúdo do *Diretório raiz do armazenamento de conteúdo*/lucene-indexes para o diretório Raiz de Índice.

1. Restaure/recupere o repositório CRX.

   * **Independente**

      *Restaurar instâncias de autor e publicação*: Se ocorrer um desastre, é possível restaurar o repositório para o último estado do backup executando as etapas descritas em [Backup e restauração.](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)

      A restauração completa do nó Autor também verifica a restauração dos dados do Forms Manager e do AEM Forms Workspace.

   * **Cluster**

      Para restauração em um ambiente em cluster, consulte [Estratégia para backup e restauração em um ambiente em cluster](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. Exclua todos os arquivos temporários de formulários AEM que foram criados no diretório java.io.temp ou no diretório temporário do Adobe.
1. Iniciar AEM formulários (consulte [Iniciar e parar serviços](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## Alteração da localização do GDS durante a recuperação {#changing-the-gds-location-during-recovery}

Se o GDS for restaurado para um local diferente de onde ele foi originalmente, execute o script LCSetGDS para definir o GDS para o novo local. O script está no `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` pasta. O script utiliza dois parâmetros, `defaultGDS` e `newGDS`. Consulte a `ReadMe.txt` na mesma pasta para obter instruções sobre como executar o script.

>[!NOTE]
>
>Se você ativou o armazenamento de documentos no banco de dados, não é necessário alterar o local do GDS.

>[!NOTE]
>
>Essa circunstância é a única sob a qual você deve usar esse script para alterar a localização do GDS. Para alterar o local do GDS enquanto AEM formulários estiver em execução, use o Console de administração. (Consulte [Definir configurações gerais do AEM forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).)

>[!NOTE]
>
>A implantação do componente falhará no Windows se o diretório GDS estiver na raiz da unidade (por exemplo, D:\). Para GDS, você deve verificar se o diretório não está localizado na raiz da unidade, mas em um subdiretório. Por exemplo, o diretório deve ser D:\GDS and not simply D:\.

## Recuperação do GDS para um ambiente em cluster {#recovering-the-gds-to-a-clustered-environment}

Para alterar o local do GDS em um ambiente em cluster, encerre todo o cluster e execute o script LCSetGDS em um único nó do cluster. (Consulte [Alteração da localização do GDS durante a recuperação](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) Inicie apenas esse nó. Quando esse nó for totalmente iniciado, outros nós no cluster poderão ser iniciados com segurança e apontarão corretamente para o novo GDS.

>[!NOTE]
>
>Se não conseguir garantir que um nó seja iniciado completamente antes de iniciar outros nós, você deverá executar o script LCSetGDS em cada nó no cluster antes de iniciar o cluster.
