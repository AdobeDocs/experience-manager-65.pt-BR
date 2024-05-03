---
title: Backup e recuperação do repositório EMC Documentum
description: Este documento descreve as tarefas necessárias para fazer backup e recuperar o repositório do EMC Documentum configurado para seu ambiente de formulários AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: bc21659f-88d6-4dff-8baf-12746e1b3ed9
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 0%

---

# Backup e recuperação do repositório EMC Documentum {#backing-up-and-recovering-the-emc-documentum-repository}

Esta seção descreve as tarefas necessárias para fazer backup e recuperar o repositório do EMC Documentum configurado para seu ambiente de formulários AEM.

>[!NOTE]
>
>Essas instruções pressupõem que os formulários AEM com Connectors for ECM e EMC Documentum Content Server estejam instalados e configurados conforme necessário.

Para os processos de backup e restauração, há duas tarefas principais:

* Backup (ou restauração) do ambiente de formulários AEM.
* Backup (ou restauração) do EMC Documentum Content Server.

>[!NOTE]
>
>Faça backup dos dados de formulários AEM antes de fazer backup do sistema EMC Documentum e, posteriormente, restaure o sistema EMC Documentum antes de restaurar o ambiente de formulários AEM.

## Requisitos de software {#software-requirements}

Para executar as tarefas de backup necessárias no EMC Documentum Content Server, adquira um utilitário apropriado de terceiros, como o EMC NetWorker da EMC ou o CYA SmartRecovery for EMC Documentum da CYA. As instruções a seguir descrevem as etapas de uso do EMC NetWorker Module versão 7.2.2.

Você precisa dos seguintes módulos do EMC NetWorker:

* Módulo do NetWorker
* Assistente de configuração do NetWorker
* Assistente de configuração do dispositivo NetWorker
* Módulo do NetWorker para o tipo de banco de dados usado por seu Content Server
* Módulo do NetWorker para Documentum

## Preparando o EMC Document Content Server para backup e recuperação {#preparing-the-emc-document-content-server-for-backup-and-recovery}

Esta seção descreve a instalação e configuração do software EMC NetWorker no Content Server.

**Preparar o servidor EMC Documentum para backup**

1. No EMC Documentum Content Server, instale os módulos do EMC NetWorker, aceitando todos os padrões.

   Durante os processos de instalação, será solicitado que você digite o nome do servidor do computador do Servidor de conteúdo como *Nome do servidor NetWorker*. Ao instalar o EMC NetWorker Module for your database, escolha uma instalação &quot;completa&quot;.

1. Usando o conteúdo de exemplo abaixo, crie um arquivo de configuração chamado *nsrnmd_win.cfg* e salve-o em um local acessível no Servidor de conteúdo. Esse arquivo será chamado pelos comandos backup e restore.

   O texto a seguir contém caracteres de formatação para quebras de linha. Se você copiar este texto para um local fora deste documento, copie uma parte de cada vez e remova os caracteres de formatação quando colá-la no novo local.

   ```shell
    ################################################
    # NetWorker Module for Documentum v1.2 nsrnmd_win.cfg D5.3+ example with
    # typical set of working parameters.  THIS FILE MUST BE SITE-CUSTOMISED.
    #
    # Parameters not shown can be set in this file (as per site customisation) #or from the command-line.
    #
    # See the user Guides for details on all parameters, including
    # those not listed below.
    # Note: DCTM environment for D6 is slightly different from D5, refer to D6
    # Installation Guide to update the values.
    ################################################
    #Can get values for most of below from doing as the dctm inst owner: cmd> set DOCUMENTUM=C:\Documentum
    DM_HOME=C:\Documentum\product\6.0
    JAVA_HOME=C:\Progra~1\Documentum\java\1.5.0_12
    JAVA_PATH=C:\Progra~1\Documentum\java\1.5.0_12\bin
    PATH=C:\WINNT\system32;C:\WINNT;C:\WINNT\system32\WBEM;C:\Documentum\product\6.0\bin;C:\Documentum\fulltext\fast;C:\Documentum\product\6.0\fusion;C:\Program Files\Documentum\Shared;C:\Program Files\Legato\nsr\bin;C:\Program Files\Microsoft SQL Server\80\Tools\Binn;C:\Program Files\Microsoft SQL Server\90\DTS\Binn\;C:\Program Files\Microsoft SQL Server\90\Tools\binn;C:\Program Files\Microsoft SQL Server\90\Tools\Binn\VSShell\Common7\IDE;C:\Program Files\Documentum\java\1.5.0_12\bin;C:\Documentum\config;C:\Documentum
    #See also manifest dctm.jar file for class path locations
    CLASSPATH=.;C:\Program Files\Legato\nsr\bin;C:\Program Files\Legato\nsr\bin\nsrnmdde.jar;C:\Program Files\Documentum\java\1.5.0_12\lib\tools.jar;C:\Program Files\Documentum\Shared\dfc.jar;C:\Program Files\Documentum\Shared\aspectjrt.jar;C:\Program Files\Documentum\dctm.jar;C:\Program Files\Documentum\Shared\workflow.jar;C:\Program Files\Documentum\Shared\log4j.jar;C:\Program Files\Documentum\java\1.5.0_12\lib\dt.jar;C:\Documentum\config
   
    ################################################
    #If not using nsrnmdsv -m ALL|DB|DB_LOG|FTI|FTI_ALL|ICF|SA|SA_ALL, set #for backup
    NMD_SCOPE=ALL
    #Mandatory when scope (backup or restore) is FTI/SA without -a option
    #NMD_OBJECT_NAME=filestore_01
    ################################################
    NMDDE_DM_DOCBASE=Docbase
    NMDDE_DM_USER=Administrator
    #NMDDE_DM_PASSWD must be set via running: nsrnmdsv -f <nmdcfg> -P <pwd>.
    ################################################
    #DB related hooks to invoke arbitrary scripts:
    #Set if DB is on a remote host
    #NMD_DB_HOST=dbhost
    #Pure basename implies remote host execution; absolute path ... local
    #execution as in NMD v1.0.
    #
    #Remote execution requires script be put in remote nsrexecd bin directory
    #and D5.3+ host be added to remote nsr\res\servers file w/ nsrexecd recycled
    #
    #Refer to user Guides for sample script code.
    NMD_DB_FULL_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbf.bat
    NMD_DB_LOG_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbl.bat
    NMD_DB_INCR_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbi.bat
    ################################################
    #For D5.3+ only: NMD_FTI_INCLUDED, NMD_FTI_HOST, NMD_FTI_USER,
    #NMD_FTI_PASSWD & NMD_FTI_SUBDIRS.
    #Optional for remote D5.3+ FTI server
    NMD_FTI_INCLUDED=no
    #NMD_FTI_HOST=ftihost
    #Recommended for D5.3+ FTI server quiesce/unquiesce
    #NMD_FTI_USER=ftiadmin
    #The index name: optional for D5.3+ FTI server, used with -M FTI_ALL or
    #-M ALL
    #NMD_FTI_NAME=rep_name_ftindex_01
    #Recommended for D5.3+ FTI server quiesce/unquiesce
    #NMDDE_FTI_PASSWD must be set via running: nsrnmdsv -f <nmdcfg> -P <pwd>
    #-M FTI.
    #Pure basename implies remote host execution; absolute path ... local execution
    #as in NMD v1.0.
    #
    #Remote execution requires script be put in remote nsrexecd bin directory
    #and D5.3+ host be added to remote nsr\res\servers file w/ nsrexecd
    #recycled.
    #
    #See example nsrnmdfti*.bat examples.
    #
    #Mandatory for D5.3+
    #NMD_BACKUP_FTI_QUIESCE=nsrnmdftiq.bat
    #NMD_BACKUP_FTI_UNQUIESCE=nsrnmdftiu.bat
    #Used for D5.3+ to get InstallProfile.xml FTI file in multinode
    #discovery.
    #Optional, if not specified, will treat as single-node FTI.
    #NMD_FTI_GET_INSTPROF=nsrnmdfti_instprof.bat
    #Mandatory for D5.3+. No spaces in paths or around comma separators.
    #For remote FTI, paths must be valid at the FTI host.
    #NMD_FTI_SUBDIRS=F:\Documentum_idx\data\fulltext\fixml,F:\Documentum_idx
    #\data\fulltext\index
    ################################################
    #Mandatory. No spaces in paths or before comma
    #separators in NMD_ICF_SUBDIRS_xxx:
    #NMD_ICF_INCLUDED=yes
    #NMD_ICF_SUBDIRS=C:\Documentum\dba,C:\Documentum\product\5.3
    ################################################
    NMD_FILEREPORT_INCLUDED=yes
    NMDDE_METADATA_OUTPUT_DEST=C:\docbase_freports\
    ################################################
    #Other misc recommended NMD_xxx parameters
    #Recommended to get more meaningful saveset names
    NMD_USE_DEFAULT_SAVESET_NAMES=yes
    #Use following to skip unwanted ICF, FTI and non-SnapImage SA dirs/files.
    #For example, "<</>> +skip: dm_ftwork_dir" line will skip non-data
    #files.
    #
    #The path will be the same and must exist on D5.3+, remote FTI host, and
    #RCS hosts correspondingly if used.
    #NMD_DIRECTIVES_FILE=E:\Program Files\Legato\nsr\res\nsrnmddirectives.txt
    #For non-SnapImage SA backup
    #NMD_SA_FULL_NUM_SAVESET=16
    #NMD_SA_INCR_NUM_SAVESET=4
    #NMD_USE_SNAPIMAGE=yes
    ################################################
    # DSA setup
    ################################################
    # Name of the config file at the remote sites;
    # Mandatory, listed in the config file at the primary host.
    # (if skipped, backup is treated as local)
    # NMD_RCS_CFG_FILE=rep_name_rcs.cfg
   
    # SA-host mapping add, optional, will override far-store list info.
    # No space around comma.
    # NMD_HOST_SAS_MAP=host01,sa_01,sa_02
    # NMD_HOST_SAS_MAP=host02,sa_03
    ################################################
    NSR_SERVER=con-dctm
    #NSR_CLIENT=d5svrhost
    NSR_GROUP=Default
    NSR_DATA_VOLUME_POOL=Default
    #NSR_SNAPIMAGE_DATA_VOLUME_POOL=Default
    #Relocation dir will be the same on D5+ and remote FTI/SA hosts.
    NSR_RELOCATION=C:\reloc
    #NSR_PARALLELISM=16
    NSR_DEBUG_FILE=C:\Program Files\Legato\nsr\applogs\nmd.log
    NSR_DEBUG_LEVEL=9
    ################################################
    NMDDE_DM_PASSWD=XAtup9pl
   ```

   Manter o campo de senha do arquivo de configuração `NMDDE_DM_PASSWD` em branco. Você definirá a senha na próxima etapa.

1. Defina a senha do arquivo de configuração da seguinte maneira:

   * Abra um prompt de comando e altere para `[NetWorker_root]\Legato\nsr\bin`.
   * Execute o seguinte comando: `-nsrnmdsv.exe -f`*&lt;path_to_cfg_file> -P &lt;password>*

1. Crie os arquivos executáveis em lote (.bat) usados para fazer backup do banco de dados. (Consulte a documentação do NetWorker.) Defina os detalhes nos arquivos em lote de acordo com sua instalação.

   * Backup completo do banco de dados (nsrnmddbf.bat):

     `NetWorker_database_module_root` `-s`*&lt;networker_server_name>* `-U``[username]` `-P`*[senha ]*`-l full`*&lt;database_name>*

   * Backup incremental do banco de dados (nsrnmddbi.bat):

     `[NetWorker_database_module_root]` `-s`*&lt;NetWorker_Server_Name>* `-U``[username]` `-P``[password]` `-l 1 -R`*&lt;database_name>*

   * Backup de log do banco de dados (nsrnmddbl.bat):

     `[NetWorker_database_module_root]` `-s``<NetWorker_Server_Name>` `-U``[username]` `-P``[password]` `-l incr -R`*&lt;database_name>*

     Em que:

     `[NetWorker_database_module_root]` é o diretório de instalação do módulo NetWorker. Por exemplo, o diretório de instalação padrão do NetWorker Module for SQL Server é C:\Program Files\Legato\nsr\bin\nsrsqlsv.

     `NetWorker_Server_Name` é o servidor no qual o NetWorker está instalado.

     `username` &amp; `password` são o nome de usuário e a senha do usuário administrador do banco de dados.

     `database_name` é o nome do banco de dados do qual se fará backup.

**Criar um dispositivo de backup**

1. Crie um diretório no servidor EMC Documentum e compartilhe a pasta dando direitos completos a todos os usuários.
1. Inicie o EMC NetWorker Administrator e clique em Media Management > Devices.
1. Clique com o botão direito do mouse em Dispositivos e selecione Criar.
1. Insira os seguintes valores e clique em OK:

   **Nome:** O caminho completo do diretório compartilhado

   **Tipo de mídia:** `File`

1. Clique com o botão direito do mouse no novo dispositivo e selecione Operações.
1. Clique em Rótulo, digite um nome, clique em OK e, em seguida, clique em Montar.

Um dispositivo é adicionado ao qual os arquivos de backup serão salvos. É possível adicionar vários dispositivos de formatos diferentes.

## Faça backup do EMC Documentum Content Server {#back-up-the-emc-documentum-content-server}

Execute as seguintes tarefas depois de concluir um backup completo dos dados de formulários AEM. (Consulte [Backup dos dados de formulários AEM](/help/forms/using/admin-help/backing-aem-forms-data.md#backing-up-the-aem-forms-data).)

>[!NOTE]
>
>Os scripts de comando exigem o caminho completo para o arquivo nsrnmd_win.cfg criado no [Preparando o EMC Document Content Server para backup e recuperação](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery).

1. Abra um prompt de comando e altere para `[NetWorker_root]\Legato\nsr\bin`.
1. Execute o seguinte comando:

   ```shell
    - nsrnmdsv.exe -f <path_to_cfg_file>
   ```

## Restaurar o EMC Documentum Content Server {#restore-the-emc-documentum-content-server}

Execute as seguintes tarefas antes de restaurar os dados de formulários AEM. (Consulte [Recuperação dos dados de formulários do AEM](/help/forms/using/admin-help/recovering-aem-forms-data.md#recovering-the-aem-forms-data).)

>[!NOTE]
>
>Os scripts de comando exigem o caminho completo para o arquivo nsrnmd_win.cfg criado no [Preparando o EMC Document Content Server para backup e recuperação](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery).

1. Pare o serviço Docbase que você está restaurando.
1. Inicie o NetWorker User Utility para seu módulo de banco de dados (por exemplo, *Usuário do NetWorker para SQL Server*).
1. Clique na ferramenta Restaurar e selecione Normal.
1. No lado esquerdo da tela, selecione o banco de dados para sua Docbase e clique no botão Iniciar na barra de ferramentas.
1. Quando o banco de dados for restaurado, reinicie o serviço Docbase.
1. Abra um prompt de comando e altere para *[NetWorker_root]*\Legato\nsr\bin
1. Execute o seguinte comando:

   ```shell
    - nsrnmdrs.exe -B <docbase_name> -f <path_to_cfg_file> -C SA
   ```
