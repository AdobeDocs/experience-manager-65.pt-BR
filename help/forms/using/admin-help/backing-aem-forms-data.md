---
title: Backup dos dados de formulários AEM
seo-title: Backing up the AEM forms data
description: Este documento descreve as etapas necessárias para concluir um backup on-line ou ativo do banco de dados de formulários AEM, os diretórios GDS e Raiz de armazenamento de conteúdo.
seo-description: This document describes the steps that are required to complete a hot, or online, backup of the AEM forms database, the GDS, and Content Storage Root directories.
uuid: ac7856be-e3b7-4b81-b8b9-fc909b5907b4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 52187196-b091-4683-85ae-cc7c250dee54
exl-id: 536615a4-ab42-4b72-83b1-fad110b011ee
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 0%

---

# Backup dos dados de formulários AEM {#backing-up-the-aem-forms-data}

Esta seção descreve as etapas necessárias para concluir um backup on-line ou ativo do banco de dados de formulários AEM, os diretórios GDS e Raiz de armazenamento de conteúdo.

Depois que os formulários AEM forem instalados e implantados nas áreas de produção, o administrador do banco de dados deverá executar um backup inicial completo ou inativo do banco de dados. O banco de dados deve ser desligado para este backup. Em seguida, backups diferenciais ou incrementais (ou ativos) do banco de dados devem ser feitos regularmente.

Para garantir um backup e uma recuperação bem-sucedidos, um backup de imagem do sistema deve estar sempre disponível. Em seguida, se ocorrer uma perda, é possível recuperar todo o ambiente para um estado consistente.

Fazer backup do banco de dados ao mesmo tempo que os backups do diretório GDS, do repositório AEM e do diretório raiz do armazenamento de conteúdo ajuda a manter esses sistemas sincronizados, caso a recuperação seja necessária.

O procedimento de backup descrito nesta seção exige que você entre no modo de backup seguro antes de fazer backup do banco de dados de formulários AEM, do repositório AEM, do GDS e dos diretórios raiz de armazenamento de conteúdo. Quando o backup estiver concluído, você deverá sair do modo de backup seguro. O modo de backup seguro é usado para marcar documentos persistentes e de longa duração que residem no GDS. Esse modo garante que o mecanismo de limpeza automática de arquivo (o coletor de arquivos) não exclua arquivos expirados até que o modo de backup seguro seja liberado. É necessário manter um backup de GDS em sincronização com um backup de banco de dados.

A frequência com que o backup do local GDS deve ser feito depende de como os formulários AEM são usados e das janelas de backup disponíveis. A janela de backup pode ser afetada por processos de longa duração, pois eles podem ser executados por vários dias. Se você estiver sempre alterando, adicionando e removendo arquivos nesse diretório, faça backup do local GDS com mais frequência.

Se o banco de dados estiver sendo executado em um modo de registro, conforme descrito na seção anterior, o backup dos logs do banco de dados também deverá ser feito com frequência para que eles possam ser usados para restaurar o banco de dados em caso de falha de mídia.

>[!NOTE]
>
>Os arquivos não referenciados podem persistir no diretório GDS após o processo de recuperação. Essa é uma limitação conhecida no momento.

## Fazer backup do banco de dados, do repositório GDS, do repositório AEM e dos diretórios raiz do armazenamento de conteúdo {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

Você deve colocar os formulários AEM no modo de backup seguro (instantâneo) ou no modo de backup contínuo (cobertura contínua). Antes de configurar formulários AEM para entrar em um dos modos de backup, verifique o seguinte:

* Verifique a versão do sistema e registre os patches ou atualizações que foram aplicados desde a execução do último backup completo de imagem do sistema.
* Se você estiver usando backups em modo de rolagem ou de snapshot, certifique-se de que seu banco de dados esteja configurado com as definições de log corretas para permitir backups do banco de dados com o sistema em funcionamento. (Consulte [Banco de dados de formulários AEM](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

Além disso, observe as seguintes diretrizes para o processo de backup/restauração.

* Faça backup do diretório GDS usando um sistema operacional disponível ou um utilitário de backup de terceiros. (Consulte [Localização do GDS](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* (Opcional) Faça backup do diretório raiz de armazenamento de conteúdo usando um sistema operacional disponível ou um backup e utilitário de terceiros. (Consulte [Local raiz do armazenamento de conteúdo (ambiente independente)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) ou [Local raiz do armazenamento de conteúdo (ambiente em cluster)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* Faça backup das instâncias do autor e de publicação ( crx - backup do repositório).

   Para fazer backup do ambiente da Solução de gerenciamento de correspondência, execute as etapas nas instâncias de criação e publicação, conforme descrito em [Backup e restauração](/help/sites-administering/backup-and-restore.md).

   Considere os seguintes pontos ao fazer backup das instâncias de autor e publicação:

   * Certifique-se de que o backup das instâncias do autor e de publicação esteja sincronizado para iniciar ao mesmo tempo.Embora você possa continuar a usar as instâncias do autor e de publicação enquanto o backup está sendo executado, é recomendável não publicar nenhum ativo durante o backup para evitar alterações não capturadas. Aguarde o término do backup das instâncias do autor e de publicação antes de publicar novos ativos.
   * O backup completo do nó Author inclui o backup do Forms Manager e dos dados do AEM Forms Workspace.
   * Os desenvolvedores do Workbench podem continuar trabalhando em seus processos localmente. Eles não devem implantar novos processos durante a fase de backup.
   * A decisão sobre a duração de cada sessão de backup (para o modo de backup contínuo) deve ser baseada no tempo total gasto para fazer backup de todos os dados em formulários AEM (BD, GDS, repositório AEM e quaisquer outros dados personalizados adicionais).

Você deve fazer backup do banco de dados de formulários AEM, incluindo todos os logs de transação. (Consulte [Banco de dados de formulários AEM](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Para obter mais informações, consulte o artigo apropriado da base de dados de conhecimento para seu banco de dados:

* [Backup e recuperação de oracles para formulários AEM](https://www.adobe.com/go/kb403624)
* [Backup e recuperação MySQL para formulários AEM](https://www.adobe.com/go/kb403625)
* [Backup e recuperação do Microsoft SQL Server para formulários AEM](https://www.adobe.com/go/kb403623)
* [Backup e recuperação DB2 para formulários AEM](https://www.adobe.com/go/kb403626)

Esses artigos fornecem orientação para os recursos básicos do banco de dados para backup e recuperação de dados. Eles não são destinados como guias técnicos completos do recurso de backup e recuperação de banco de dados de um fornecedor específico. Eles descrevem os comandos necessários para criar uma estratégia confiável de backup de banco de dados para os dados de aplicativos de formulários AEM.

>[!NOTE]
>
>O backup do banco de dados deve ser concluído antes de você iniciar o backup do GDS. Se o backup do banco de dados não for concluído, os dados ficarão fora de sincronia.

### Entrando nos modos de backup {#entering-the-backup-modes}

Você pode usar o console de administração, o comando LCBackupMode ou a API disponível com a instalação do AEM Forms para entrar e sair dos modos de backup. Observe que para o backup contínuo (cobertura contínua), a opção do console de administração não está disponível; você deve usar a opção de linha de comando ou a API. <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Se você tiver configurado o SSL no servidor de formulários, não será possível colocar o servidor de formulários no modo de backup usando o script LCBackupMode.CMD.

**Usar o console de administração para entrar no modo de backup seguro**

1. Faça logon no console de administração.
1. Clique em Configurações > Configurações principais do sistema > Utilitários de backup.
1. Selecione Operar no modo de backup seguro e clique em OK.

   Esse método coloca formulários AEM em modo de backup indefinidamente (sem tempo limite) e entra no modo de instantâneo em vez do modo de backup contínuo.

**Usando a opção de linha de comando para entrar no modo de backup seguro**

Você pode usar a interface de linha de comando `LCBackupMode` para colocar formulários AEM no modo de backup seguro.

1. Defina ADOBE_LIVECYCLE e inicie o servidor de aplicativos.
1. Vá para a `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` pasta.
1. Dependendo do seu sistema operacional, edite a `LCBackupMode.cmd` ou `LCBackupMode.sh` para fornecer os valores padrão apropriados para o seu sistema.
1. No prompt de comando, execute o seguinte comando em uma única linha:

   * (Windows) `LCBackupMode.cmd enter [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*nome de usuário* `] [-password=`*senha* `] [-label=`*labelname* `] [-timeout=`*segundos* `]`
   * (Linux, UNIX) `LCBackupMode.sh enter [-host=`*hostname* `] [-port=`*portnumber* `] [-user=`*nome de usuário* `] [-password=`*senha* `] [-label=`*labelname* `]`

   Nos comandos anteriores, os espaços reservados são definidos da seguinte maneira:

   `Host` é o nome do host onde o AEM Forms está sendo executado.

   `port` é a porta WebServices do servidor de aplicativos no qual os formulários AEM estão sendo executados.

   `user` é o nome de usuário do administrador de formulários AEM.

   `password` é a senha do administrador de formulários AEM.

   `label` é o rótulo do texto, que pode ser qualquer string, para esse backup.

   `timeout` é o número de segundos após o qual o modo de backup é deixado automaticamente. Pode ser de 0 a 10.080. Se for 0, que é o padrão, o modo de backup nunca expirará.

   Para obter mais informações sobre a interface de linha de comando para o modo de backup, consulte o arquivo Readme no diretório BackupRestoreCommandline.

### Saindo dos modos de backup {#leaving-backup-modes}

Você pode usar o console de administração ou a opção de linha de comando para deixar os modos de backup.

**Sair do modo de backup seguro (modo de instantâneo)**

Para usar o Administration Console para retirar os formulários AEM do modo de backup seguro (modo instantâneo), execute as seguintes tarefas.

1. Faça logon no Console de administração.
1. Clique em Configurações > Configurações principais do sistema > Utilitários de backup.
1. Desmarque a opção Operar no modo de backup seguro e clique em OK.

**Deixar todos os modos de backup**

Você pode usar a interface de linha de comando para retirar os formulários AEM do modo de backup seguro (modo instantâneo) ou para encerrar a sessão do modo de backup atual (modo contínuo). Observe que não é possível usar o console de administração para sair do modo de backup contínuo. No modo de backup contínuo, os controles de Utilitários de Backup do Console de Administração são desativados. Você deve usar a chamada de API ou o comando LCBackupMode.

1. Vá para a `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` pasta.
1. Dependendo do seu sistema operacional, edite a `LCBackupMode.cmd` ou `LCBackupMode.sh` para fornecer os valores padrão apropriados para o seu sistema.

   >[!NOTE]
   >
   >Você deve definir o diretório JAVA_HOME conforme descrito no capítulo apropriado para o seu servidor de aplicativos em [Preparação para instalar formulários AEM](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. Execute o seguinte comando em uma única linha:

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*nome de usuário* `] [-password=`*senha* `]`
   * (Linux, UNIX) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*nome de usuário* `] [-password=`*senha* `]`

      Nos comandos anteriores, os espaços reservados são definidos da seguinte maneira:

      `Host` é o nome do host onde o AEM Forms está sendo executado.

      `port` é a porta em que o AEM Forms está sendo executado no servidor de aplicativos.

      `user` é o nome de usuário do administrador de formulários AEM.

      `password` é a senha do administrador de formulários AEM.

      `leaveContinuousCoverage` Use esta opção para desativar completamente o modo de backup contínuo.
   >[!NOTE]
   >
   >Durante o período em que o modo de backup estiver desativado, a cobertura contínua não poderá ser restabelecida. Quaisquer alterações durante esse período não serão protegidas.

   >[!NOTE]
   >
   >Se você ativou o armazenamento de documentos no banco de dados, o modo de backup de instantâneo e os modos de backup rotativo não são aplicáveis.

   Para obter mais informações sobre a interface de linha de comando para o modo de backup, consulte o arquivo readme no diretório BackupRestoreCommandline.
