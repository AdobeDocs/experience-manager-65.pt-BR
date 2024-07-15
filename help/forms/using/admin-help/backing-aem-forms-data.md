---
title: Backup dos dados do Adobe Experience Manager Forms
description: Este documento descreve as etapas necessárias para concluir um backup on-line ou ativo do banco de dados de formulários do Adobe Experience Manager (AEM), do GDS e dos diretórios raiz de armazenamento de conteúdo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 536615a4-ab42-4b72-83b1-fad110b011ee
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 0%

---

# Backup dos dados do Forms do Adobe Experience Manager (AEM) {#backing-up-the-aem-forms-data}

<!-- back up is two words when used as a verb; backup is one word when used as an adjective or noun. -->

Esta seção descreve as etapas necessárias para concluir um backup on-line ou ativo do banco de dados do AEM Forms, dos diretórios GDS e da raiz de armazenamento de conteúdo.

Depois que o AEM Forms for instalado e implantado em áreas de produção, o administrador do banco de dados deverá executar um backup inicial completo ou inativo do banco de dados. O banco de dados deve ser desativado para este backup. Em seguida, backups diferenciais ou incrementais (ou ativos) do banco de dados devem ser feitos regularmente.

Para garantir um backup e uma recuperação bem-sucedidos, um backup de imagem do sistema deve estar sempre disponível. Em seguida, se ocorrer uma perda, é possível recuperar todo o ambiente para um estado consistente.

Fazer backup do banco de dados ao mesmo tempo que os backups do diretório GDS, do repositório AEM e do diretório raiz do armazenamento de conteúdo ajuda a manter esses sistemas sincronizados, caso a recuperação seja necessária.

O procedimento de backup descrito nesta seção exige que você entre no modo de backup seguro antes de fazer backup do banco de dados AEM Forms, do repositório AEM, do GDS e dos diretórios Raiz de armazenamento de conteúdo. Quando o backup estiver concluído, você deverá sair do modo de backup seguro. O modo de backup seguro é usado para marcar documentos persistentes e de longa duração que residem no GDS. Esse modo garante que o mecanismo de limpeza automática de arquivos (o coletor de arquivos) não exclua arquivos expirados até que o modo de backup seguro seja liberado. É necessário manter um backup de GDS em sincronização com um backup de banco de dados.

A frequência com que o backup do local GDS deve ser feito depende de como o AEM Forms é usado e das janelas de backup disponíveis. A janela de backup pode ser afetada por processos de longa duração, pois eles podem ser executados por vários dias. Se você estiver sempre alterando, adicionando e removendo arquivos nesse diretório, faça backup do local GDS com mais frequência.

Se o banco de dados estiver sendo executado em um modo de log, conforme descrito na seção anterior, também será necessário fazer backup dos logs do banco de dados com frequência para que eles possam ser usados para restaurar o banco de dados se houver falha de mídia.

>[!NOTE]
>
>Os arquivos não referenciados podem persistir no diretório GDS após o processo de recuperação. Essa é uma limitação conhecida no momento.

## Fazer backup do banco de dados, do repositório GDS, do repositório AEM e dos diretórios raiz do armazenamento de conteúdo {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

Coloque o AEM Forms no modo de backup seguro (instantâneo) ou no modo de backup contínuo (cobertura contínua). Antes de configurar o AEM Forms para inserir um dos modos de backup, verifique o seguinte:

* Verifique a versão do sistema e registre os patches ou atualizações que foram aplicados desde a execução do último backup completo de imagem do sistema.
* Se você estiver usando backups em modo de rolagem ou de snapshot, certifique-se de que seu banco de dados esteja configurado com as definições de log corretas para permitir backups do banco de dados com o sistema em funcionamento. (Consulte [banco de dados AEM Forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

Além disso, observe as seguintes diretrizes para o processo de backup/restauração.

* Faça backup do diretório GDS usando um sistema operacional disponível ou um utilitário de backup de terceiros. (Consulte [Local do GDS](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* (Opcional) Faça backup do diretório raiz de armazenamento de conteúdo usando um sistema operacional disponível ou um backup e utilitário de terceiros. (Consulte [Local raiz do armazenamento de conteúdo (ambiente independente)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) ou [Local raiz do armazenamento de conteúdo (ambiente em cluster)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* Fazer backup   instâncias de criação e publicação ( crx - backup do repositório).

  Para fazer backup do ambiente da Solução de gerenciamento de correspondência, execute as etapas nas instâncias de criação e publicação conforme descrito em [Backup e restauração](/help/sites-administering/backup-and-restore.md).

  Considere os seguintes pontos ao fazer backup das instâncias de autor e publicação:

   * Certifique-se de que o backup das instâncias do autor e de publicação esteja sincronizado para iniciar ao mesmo tempo. Embora seja possível continuar a usar as instâncias de criação e publicação enquanto o backup está sendo executado, é recomendável não publicar nenhum ativo durante o backup para evitar alterações não capturadas. Aguarde o término do backup das instâncias do autor e de publicação antes de publicar novos ativos.
   * O backup completo do nó Author inclui o backup do Forms Manager e dos dados do AEM Forms Workspace.
   * Os desenvolvedores do Workbench podem continuar trabalhando em seus processos localmente. Eles não devem implantar novos processos durante a fase de backup.
   * A decisão sobre a duração de cada sessão de backup (para o modo de backup contínuo) deve ser baseada no tempo total gasto para fazer backup de todos os dados no AEM Forms (BD, GDS, repositório AEM e quaisquer outros dados personalizados adicionais).

Fazer backup do banco de dados do AEM Forms, incluindo todos os logs de transações. Consulte [banco de dados AEM Forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).

Para obter mais informações, consulte o artigo apropriado da base de dados de conhecimento para seu banco de dados:
<!-- The four URLs below are all 404s; checked July 19, 2023 -->
* [Backup e recuperação do Oracle para AEM Forms](https://www.adobe.com/go/kb403624)
* [Backup e recuperação do MySQL para AEM Forms](https://www.adobe.com/go/kb403625)
* [Backup e recuperação do Microsoft® SQL Server para AEM Forms](https://www.adobe.com/go/kb403623)
* [Backup e recuperação do DB2® para AEM Forms](https://www.adobe.com/go/kb403626)

Esses artigos fornecem orientação para os recursos básicos do banco de dados para backup e recuperação de dados. Eles não são destinados como guias técnicos completos do recurso de backup e recuperação de banco de dados de um fornecedor específico. Eles descrevem os comandos necessários para criar uma estratégia confiável de backup de banco de dados para os dados de aplicativos do AEM Forms.

>[!NOTE]
>
>O backup do banco de dados deve ser concluído antes de você iniciar o backup do GDS. Se o backup do banco de dados não estiver concluído, os dados estarão fora de sincronia.

### Entrando nos modos de backup {#entering-the-backup-modes}

Você pode usar o console de administração, o comando LCBackupMode ou a API disponível com a instalação do AEM Forms para entrar e sair dos modos de backup. Para backup contínuo (cobertura contínua), a opção de console de administração não está disponível; você deve usar a opção de linha de comando ou a API. <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM Forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Se você tiver configurado o SSL no Forms Server, não será possível colocar o Forms Server no modo de backup usando o script LCBackupMode.CMD.

**Usando o console de administração para entrar no modo de backup seguro**

1. Faça logon no console de administração.
1. Clique em Configurações > Configurações principais do sistema > Utilitários de backup.
1. Selecione Operar no modo de backup seguro e clique em OK.

   Esse método coloca o AEM Forms no modo de backup indefinidamente (sem tempo limite) e entra no modo de instantâneo em vez do modo de backup contínuo.

**Usando a opção de linha de comando para entrar no modo de backup seguro**

Você pode usar os scripts da interface de linha de comando `LCBackupMode` para colocar o AEM Forms no modo de backup seguro.

1. Defina ADOBE_LIVECYCLE e inicie o servidor de aplicativos.
1. Vá para a pasta `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`.
1. Dependendo do seu sistema operacional, edite o script `LCBackupMode.cmd` ou `LCBackupMode.sh` para fornecer valores padrão apropriados para o seu sistema.
1. No prompt de comando, execute o seguinte comando em uma única linha:

   * (Windows) `LCBackupMode.cmd enter [-Host=`*nome do host* `] [-port=`*número da porta* `] [-user=`*nome do usuário* `] [-password=`*senha* `] [-label=`*nome do rótulo* `] [-timeout=`*segundos* `]`
   * (Linux®, UNIX®) `LCBackupMode.sh enter [-host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `] [-label=`*labelname* `]`

   Nos comandos anteriores, os espaços reservados são definidos da seguinte maneira:

   `Host` é o nome do host onde o AEM Forms está sendo executado.

   `port` é a porta WebServices do servidor de aplicativos no qual o AEM Forms está sendo executado.

   `user` é o nome de usuário do administrador do AEM Forms.

   `password` é a senha do administrador do AEM Forms.

   `label` é o rótulo de texto, que pode ser qualquer cadeia de caracteres, para este backup.

   `timeout` é o número de segundos após o qual o modo de backup é deixado automaticamente. Pode ser de 0 a 10.080. Se for 0, que é o padrão, o modo de backup nunca expirará.

   Para obter mais informações sobre a interface de linha de comando para o modo de backup, consulte o arquivo Readme no diretório BackupRestoreCommandline.

### Saindo dos modos de backup {#leaving-backup-modes}

Você pode usar o console de administração ou a opção de linha de comando para deixar os modos de backup.

**Sair do modo de backup seguro (modo de instantâneo)**

Para usar o Console de administração para remover o AEM Forms do modo de backup seguro (modo instantâneo), execute as seguintes tarefas.

1. Faça logon no Console de administração.
1. Clique em Configurações > Configurações principais do sistema > Utilitários de backup.
1. Desmarque a opção Operar no modo de backup seguro e clique em OK.

**Sair de todos os modos de backup**

Você pode usar a interface de linha de comando para tirar o AEM Forms do modo de backup seguro (modo de instantâneo) ou para encerrar a sessão do modo de backup atual (modo contínuo). Não é possível usar o console de administração para sair do modo de backup contínuo. No modo de backup contínuo, os controles de Utilitários de Backup do Console de Administração são desativados. Use a chamada de API ou o comando LCBackupMode.

1. Vá para a pasta `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`.
1. Dependendo do seu sistema operacional, edite o script `LCBackupMode.cmd` ou `LCBackupMode.sh` para fornecer valores padrão apropriados para o seu sistema.

   >[!NOTE]
   >
   >Defina o diretório JAVA_HOME conforme descrito no capítulo apropriado para seu servidor de aplicativos em [Preparando-se para Instalar o AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. Execute o seguinte comando em uma única linha:

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*nome do host* `] [-port=`*número da porta* `] [-user=`*nome do usuário* `] [-password=`*senha* `]`
   * (Linux®, UNIX®) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*nome do host* `] [-port=`*número da porta* `] [-user=`*nome do usuário* `] [-password=`*senha* `]`

     Nos comandos anteriores, os espaços reservados são definidos da seguinte maneira:

     `Host` é o nome do host onde o AEM Forms está sendo executado.

     `port` é a porta em que o AEM Forms está sendo executado no servidor de aplicativos.

     `user` é o nome de usuário do administrador do AEM Forms.

     `password` é a senha do administrador do AEM Forms.

     `leaveContinuousCoverage` Use esta opção para desabilitar completamente o modo de backup contínuo.

   >[!NOTE]
   >
   >Durante o período em que o modo de backup estiver desativado, a cobertura contínua não poderá ser restabelecida. Quaisquer alterações durante esse período não serão protegidas.

   >[!NOTE]
   >
   >Se você ativou o armazenamento de documentos no banco de dados, o modo de backup de instantâneo e os modos de backup rotativo não são aplicáveis.

   Para obter mais informações sobre a interface de linha de comando para o modo de backup, consulte o arquivo readme no diretório BackupRestoreCommandline.
