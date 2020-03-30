---
title: Recuperar os dados de formulários do AEM
seo-title: Recuperar os dados de formulários do AEM
description: Este documento descreve as etapas necessárias para recuperar os dados dos formulários do AEM.
seo-description: Este documento descreve as etapas necessárias para recuperar os dados dos formulários do AEM.
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Recuperar os dados de formulários do AEM {#recovering-the-aem-forms-data}

Esta seção descreve as etapas necessárias para recuperar os dados dos formulários do AEM. Consulte também Considerações [especiais para backup e recuperação](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>O banco de dados, o GDS, o repositório do AEM e os diretórios raiz do Armazenamento de conteúdo devem ser restaurados para um computador com o mesmo nome DNS do original.

Os formulários do AEM devem se recuperar com confiança das seguintes falhas:

**Falha de disco:** A mídia de backup mais recente é necessária para recuperar o conteúdo do banco de dados.

**Corrupção de dados:** Os sistemas de arquivos não registram transações anteriores e os sistemas podem substituir acidentalmente os dados necessários do processo.

**Erro do usuário:** A recuperação é limitada aos dados disponibilizados pelo banco de dados. Se os dados foram armazenados e estão disponíveis, a recuperação é simplificada.

**Interrupção de energia, Travamento do sistema:** As APIs do sistema de arquivos geralmente não são projetadas ou usadas de forma robusta, protegendo contra falhas inesperadas do sistema. Se ocorrer uma falha de energia ou falha do sistema, o conteúdo do documento armazenado no banco de dados tem maior probabilidade de estar atualizado do que o conteúdo armazenado em um sistema de arquivos.

Se estiver usando o modo de backup em andamento, você ainda estará no modo de backup após a recuperação. Se estiver usando o modo de backup de snapshot, você não estará no modo de backup após a recuperação.

Ao restaurar do backup para um novo sistema, as seguintes configurações podem ser diferentes. Essa diferença não deve afetar uma recuperação bem-sucedida do aplicativo de formulários AEM:

* Endereço IP
* Configuração física do sistema (CPUs, disco, memória)
* Localização GDS

>[!NOTE]
>
>O backup do diretório raiz do Armazenamento de conteúdo deve ser restaurado para o local desse diretório, conforme foi definido durante a configuração do Content Services.

Se um único nó de um cluster de vários nós falhar e os nós restantes do cluster estiverem funcionando corretamente, execute o procedimento de recuperação de nó único do cluster.

## Recuperar os dados dos formulários do AEM {#recover-the-aem-forms-data}

1. Pare os serviços de formulários AEM e o servidor de aplicativos se estiver em execução.
1. Se necessário, recrie o sistema físico a partir de uma imagem do sistema. Por exemplo, essa etapa pode não ser necessária se o motivo da recuperação for um servidor de banco de dados com falha.
1. Aplique patches ou atualizações a formulários AEM que foram aplicados desde que a imagem foi feita. Essas informações foram registradas no procedimento de backup. Os formulários do AEM devem ser corrigidos para o mesmo nível de correção que no momento do backup do sistema.
1. (WebSphere Application Server) Se você estiver se recuperando para uma nova instância do WebSphere Application Server, execute o comando restoreConfig.bat/sh.
1. Recupere o banco de dados de formulários AEM executando primeiro uma operação de restauração do banco de dados usando os arquivos de backup do banco de dados e aplicando os redo logs de transação ao banco de dados recuperado. (Consulte Banco de dados [de formulários do](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)AEM.) Para obter mais informações, consulte um destes artigos da base de conhecimento:

   * [Formulários do Oracle Backup and Recovery for AEM](https://www.adobe.com/go/kb403624)
   * [Backup e recuperação MySQL para formulários AEM](https://www.adobe.com/go/kb403625)
   * [Backup e recuperação do Microsoft SQL Server para formulários AEM](https://www.adobe.com/go/kb403623)
   * [Backup e recuperação de DB2 para formulários AEM](https://www.adobe.com/go/kb403626)

1. Recupere o diretório GDS primeiro excluindo o conteúdo do diretório GDS na instalação existente dos formulários AEM e, em seguida, copiando o conteúdo do diretório GDS do GDS de backup. Se você alterou o local do diretório GDS, consulte [Alteração do local do GDS durante a recuperação](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. Renomeie o diretório de backup GDS a ser restaurado, como mostra estes exemplos:

   >[!NOTE]
   >
   >Se o diretório /restore já existir, faça backup dele e exclua-o antes de renomear o diretório /backup que contém os dados mais recentes.

   * (JBoss) Renomear `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` para:

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * (WebLogic) Renomear `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` para:

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere) Renomeie `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` para:

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. Recupere o diretório raiz do Armazenamento de conteúdo primeiro excluindo o conteúdo do diretório raiz do Armazenamento de conteúdo na instalação existente dos formulários AEM e recupere o conteúdo seguindo as tarefas para ambientes independentes ou agrupados:

   >[!NOTE]
   >
   >O backup do diretório raiz do Armazenamento de conteúdo deve ser restaurado para o local do diretório raiz do Armazenamento de conteúdo, como foi definido durante a configuração do Content Services (obsoleto).

   **Autônomo:** Durante o processo de recuperação, restaure todos os diretórios cujo backup foi feito. Quando esses diretórios forem restaurados, se o diretório /backup-lucene-indexes estiver presente, renomeie-o como /lucene-indexes. Caso contrário, o diretório lucene-index já deverá existir e nenhuma ação será necessária.

   **Agrupado:** Durante o processo de recuperação, restaure todos os diretórios cujo backup foi feito. Para restaurar o diretório raiz de índice, execute as seguintes etapas em cada nó do cluster:

   * Exclua todo o conteúdo do diretório Raiz de índice.
   * Se o diretório /backup-lucene-index estiver presente, copie o conteúdo do diretório *raiz do Armazenamento* de conteúdo/backup-lucene-indexes para o diretório raiz do índice e exclua o diretório raiz do Armazenamento de *conteúdo*/backup-lucene-indexes.
   * Se o diretório /lucene-indexes estiver presente, copie o conteúdo do diretório *raiz do Armazenamento* Conteúdo/lucene-indexes para o diretório raiz do índice.

1. Restaure/recupere o repositório CRX.

   * **Autônomo**

      *Restaurar instâncias* de autor e publicação: Se ocorrer um desastre, você poderá restaurar o repositório para o último estado de backup executando as etapas descritas em [Backup e restauração.](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)

      A restauração completa do nó Autor também verifica a restauração dos dados do Gerenciador de Formulários e do AEM Forms Workspace.

   * **Agrupado**

      Para restaurar em um ambiente agrupado, consulte [Estratégia para backup e restauração em um ambiente](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment)agrupado.

1. Exclua todos os arquivos temporários de formulários AEM criados no diretório java.io.temp ou no diretório temporário da Adobe.
1. Formulários AEM de Start (consulte [Iniciar e parar serviços](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## Alteração do local do GDS durante a recuperação {#changing-the-gds-location-during-recovery}

Se seu GDS for restaurado para um local diferente do local em que ele estava originalmente, execute o script LCSetGDS para definir o GDS para o novo local. O script está na `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` pasta. O script utiliza dois parâmetros `defaultGDS` e `newGDS`. Consulte o `ReadMe.txt` arquivo na mesma pasta para obter instruções sobre como executar o script.

>[!NOTE]
>
>Se você ativou o armazenamento do documento no banco de dados, não é necessário alterar a localização do GDS.

>[!NOTE]
>
>Essa circunstância é a única sob a qual você deve usar esse script para alterar a localização do GDS. Para alterar o local do GDS enquanto os formulários AEM estiverem em execução, use o Console de administração. (Consulte [Configurar configurações](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)gerais de formulários AEM.)

>[!NOTE]
>
>A implantação do componente falhará no Windows se o diretório GDS estiver na raiz da unidade (por exemplo, D:\). Para GDS, verifique se o diretório não está localizado na raiz da unidade, mas em um subdiretório. Por exemplo, o diretório deve ser D:\GDS and not simply D:\.

## Recuperando o GDS em um ambiente agrupado {#recovering-the-gds-to-a-clustered-environment}

Para alterar o local GDS em um ambiente clusterizado, desligue o cluster inteiro e execute o script LCSetGDS em um único nó do cluster. (Consulte [Alteração da localização do GDS durante a recuperação](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) Start somente aquele nó. Quando esse nó for totalmente iniciado, outros nós no cluster poderão ser iniciados com segurança e apontarão corretamente para o novo GDS.

>[!NOTE]
>
>Se você não puder garantir que inicie um nó completamente antes de iniciar outros nós, execute o script LCSetGDS em todos os nós do cluster antes de start do cluster.

