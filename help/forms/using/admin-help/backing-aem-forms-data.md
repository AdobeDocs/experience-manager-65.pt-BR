---
title: Como fazer backup dos dados dos formulários AEM
seo-title: Como fazer backup dos dados dos formulários AEM
description: Este documento descreve as etapas necessárias para concluir um backup ativo ou on-line do banco de dados de formulários AEM, do GDS e dos diretórios raiz do Armazenamento de conteúdo.
seo-description: Este documento descreve as etapas necessárias para concluir um backup ativo ou on-line do banco de dados de formulários AEM, do GDS e dos diretórios raiz do Armazenamento de conteúdo.
uuid: ac7856be-e3b7-4b81-b8b9-fc909b5907b4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 52187196-b091-4683-85ae-cc7c250dee54
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---


# Fazer backup dos dados dos formulários AEM {#backing-up-the-aem-forms-data}

Esta seção descreve as etapas necessárias para concluir um backup ativo ou on-line do banco de dados de formulários AEM, do GDS e dos diretórios raiz do Armazenamento de conteúdo.

Depois que AEM formulários for instalado e implantado em áreas de produção, o administrador do banco de dados deverá executar um backup inicial completo ou frio do banco de dados. O banco de dados deve ser desligado para esse backup. Em seguida, backups diferenciais ou incrementais (ou quentes) do banco de dados devem ser feitos regularmente.

Para garantir um backup e recuperação bem-sucedidos, um backup de imagem do sistema deve estar disponível o tempo todo. Em seguida, se ocorrer uma perda, você poderá recuperar o ambiente inteiro para um estado consistente.

O backup do banco de dados ao mesmo tempo que os backups de diretório GDS, repositório AEM e raiz do Armazenamento de conteúdo ajuda a manter esses sistemas sincronizados se a recuperação for necessária.

O procedimento de backup descrito nesta seção requer que você entre no modo de backup seguro antes de fazer backup do banco de dados de formulários AEM, do repositório AEM, do GDS e dos diretórios raiz do Armazenamento de conteúdo. Quando o backup estiver concluído, você deverá sair do modo de backup seguro. O modo de backup seguro é usado para marcar documentos duradouros e persistentes que residem no GDS. Esse modo garante que o mecanismo de limpeza de arquivos automatizado (o coletor de arquivos) não exclua arquivos expirados até que o modo de backup seguro seja lançado. É necessário manter um backup GDS sincronizado com um backup de banco de dados.

A frequência com que o backup do local GDS deve ser feito depende de como os formulários AEM são usados e das janelas de backup disponíveis. A janela de backup pode ser afetada por processos de longa duração, pois eles podem ser executados por vários dias. Se você estiver alterando, adicionando e removendo continuamente arquivos neste diretório, é necessário fazer backup do local GDS com mais frequência.

Se o banco de dados estiver sendo executado em um modo de log, conforme descrito na seção anterior, os logs do banco de dados também deverão ser copiados em backup com frequência para que possam ser usados para restaurar o banco de dados em caso de falha de mídia.

>[!NOTE]
>
>Os arquivos que não são referenciados podem persistir no diretório GDS após o processo de recuperação. Esta é uma limitação conhecida neste momento.

## Faça backup do banco de dados, do GDS, do repositório AEM e dos diretórios raiz do Armazenamento de conteúdo {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

Você deve colocar AEM formulários no modo de backup seguro (snapshot) ou no modo de backup em andamento (cobertura contínua). Antes de configurar AEM formulários para inserir um dos modos de backup, verifique o seguinte:

* Verifique a versão do sistema e registre os patches ou atualizações aplicados desde que o último backup completo de imagem do sistema foi executado.
* Se você estiver usando backups em modo de rolagem ou de snapshot, verifique se o banco de dados está configurado com as configurações de log corretas para permitir backups em tempo real do banco de dados. (Consulte [AEM banco de dados de formulários](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

Além disso, observe as diretrizes a seguir para o processo de backup/restauração.

* Faça backup do diretório GDS usando um sistema operacional disponível ou um utilitário de backup de terceiros. (Consulte [Localização GDS](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* (Opcional) Faça backup do diretório raiz do Armazenamento de conteúdo usando um sistema operacional disponível ou um utilitário e backup de terceiros. (Consulte [Localização raiz do Armazenamento de conteúdo (ambiente independente)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) ou [Localização raiz do Armazenamento de conteúdo (ambiente agrupado)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* Fazer backup   instâncias de autor e publicação (crx - backup de repositório).

   Para fazer backup do ambiente da Solução de Gerenciamento de Correspondência, execute as etapas nas instâncias de autor e publicação, conforme descrito em [Backup e Restauração](/help/sites-administering/backup-and-restore.md).

   Considere os seguintes pontos ao fazer backup das instâncias de autor e publicação:

   * Certifique-se de que o backup das instâncias de autor e publicação esteja sincronizado com o start ao mesmo tempo.Embora você possa continuar a usar as instâncias de autor e publicação enquanto o backup estiver sendo executado, recomenda-se não publicar qualquer ativo durante o backup para evitar alterações não capturadas. Aguarde até que o backup das instâncias de autor e publicação termine antes de publicar novos ativos.
   * O backup completo do nó Autor inclui backup dos dados do Forms Manager e do AEM Forms Workspace.
   * Os desenvolvedores do Workbench podem continuar trabalhando em seus processos localmente. Eles não devem implantar novos processos durante a fase de backup.
   * A decisão sobre a duração de cada sessão de backup (para o modo de backup em andamento) deve se basear no tempo total necessário para fazer backup de todos os dados em formulários AEM (BD, GDS, repositório AEM e quaisquer outros dados personalizados adicionais).

É necessário fazer backup do banco de dados de formulários AEM, incluindo quaisquer logs de transações. (Consulte [AEM banco de dados de formulários](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Para obter mais informações, consulte o artigo da base de conhecimento apropriado para seu banco de dados:

* [Backup e recuperação oracle para formulários AEM](https://www.adobe.com/go/kb403624)
* [Backup e recuperação MySQL para formulários AEM](https://www.adobe.com/go/kb403625)
* [Backup e recuperação do Microsoft SQL Server para formulários AEM](https://www.adobe.com/go/kb403623)
* [Backup e recuperação de DB2 para formulários AEM](https://www.adobe.com/go/kb403626)

Esses artigos fornecem orientação para os recursos básicos do banco de dados para backup e recuperação de dados. Eles não são destinados aos Guias técnicos completos de um recurso específico de backup e recuperação de banco de dados do fornecedor. Eles destacam comandos necessários para criar uma estratégia de backup de banco de dados confiável para seus dados de aplicativo de formulários AEM.

>[!NOTE]
>
>O backup do banco de dados deve ser concluído antes que você comece a fazer o backup do GDS. Se o backup do banco de dados não estiver concluído, seus dados estarão fora de sincronia.

### Inserir os modos de backup {#entering-the-backup-modes}

Você pode usar o console de administração, o comando LCBackupMode ou a API disponível com a instalação de formulários AEM para entrar e sair dos modos de backup. Observe que para backup de rolagem (cobertura contínua), a opção de console de administração não está disponível; você deve usar a opção de linha de comando ou a API. <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Se você tiver configurado o SSL no servidor de formulários, não será possível colocar o servidor de formulários no modo de backup usando o script LCBackupMode.CMD.

**Usar o console de administração para entrar no modo de backup seguro**

1. Faça logon no console de administração.
1. Clique em Configurações > Configurações principais do sistema > Utilitários de backup.
1. Selecione Operar no modo de backup seguro e clique em OK.

   Esse método coloca formulários AEM no modo de backup indefinidamente (sem tempo limite) e entra no modo de snapshot em vez do modo de backup em andamento.

**Uso da opção de linha de comando para entrar no modo de backup seguro**

Você pode usar os scripts `LCBackupMode` da interface de linha de comando para colocar formulários AEM no modo de backup seguro.

1. Defina ADOBE_LIVECYCLE e start o servidor de aplicativos.
1. Vá para a pasta `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`.
1. Dependendo do seu sistema operacional, edite o script `LCBackupMode.cmd` ou `LCBackupMode.sh` para fornecer valores padrão adequados ao seu sistema.
1. No prompt de comando, execute o seguinte comando em uma única linha:

   * (Windows) `LCBackupMode.cmd enter [-Host=`*nome do host* `] [-port=`*número do porta* `] [-user=`*nome do usuário* `] [-password=`*senha* `] [-label=`*nome do rótulo* `] [-timeout=`*segundos* `]`
   * (Linux, UNIX) `LCBackupMode.sh enter [-host=`*nome do host* `] [-port=`*número de porta* `] [-user=`*nome do usuário* `] [-password=`*senha* `] [-label=`*nome do rótulo* `]`

   Nos comandos anteriores, os espaços reservados são definidos da seguinte forma:

   `Host` é o nome do host no qual os formulários AEM estão sendo executados.

   `port` é a porta WebServices do servidor de aplicativos na qual os formulários AEM estão sendo executados.

   `user` é o nome de usuário do administrador de formulários AEM.

   `password` é a senha do administrador dos formulários AEM.

   `label` é o rótulo do texto, que pode ser qualquer string, para esse backup.

   `timeout` é o número de segundos após o qual o modo de backup é automaticamente deixado. Pode ser de 0 a 10.080. Se for 0, que é o padrão, o modo de backup nunca expira.

   Para obter mais informações sobre a interface da linha de comando para o modo de backup, consulte o arquivo Readme no diretório BackupRestoreCommandline.

### Deixando os modos de backup {#leaving-backup-modes}

Você pode usar o console de administração ou a opção de linha de comando para deixar os modos de backup.

**Deixe o modo de backup seguro (modo de instantâneo)**

Para usar o Console de administração para retirar AEM formulários do modo de backup seguro (modo de snapshot), execute as seguintes tarefas.

1. Faça logon no Console de administração.
1. Clique em Configurações > Configurações principais do sistema > Utilitários de backup.
1. Desmarque Operar no modo de backup seguro e clique em OK.

**Deixe todos os modos de backup**

Você pode usar a interface de linha de comando para retirar AEM formulários do modo de backup seguro (modo de snapshot) ou para encerrar a sessão do modo de backup atual (modo de rolagem). Observe que não é possível usar o console de administração para sair do modo de backup em andamento. Durante o modo de backup em andamento, os controles de Utilitários de Backup no Console de Administração são desativados. Você deve usar uma chamada de API ou o comando LCBackupMode.

1. Vá para a pasta `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`.
1. Dependendo do seu sistema operacional, edite o script `LCBackupMode.cmd` ou `LCBackupMode.sh` para fornecer valores padrão adequados ao seu sistema.

   >[!NOTE]
   >
   >Você deve definir o diretório JAVA_HOME conforme descrito no capítulo apropriado para o servidor de aplicativos em [Preparando para instalar formulários AEM](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. Execute o seguinte comando em uma única linha:

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*nome do host* `] [-port=`*número do porta* `] [-user=`*nome do usuário* `] [-password=`*senha* `]`
   * (Linux, UNIX) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*nome do host* `] [-port=`*número de porta* `] [-user=`*nome do usuário* `] [-password=`*senha* `]`

      Nos comandos anteriores, os espaços reservados são definidos da seguinte forma:

      `Host` é o nome do host no qual os formulários AEM estão sendo executados.

      `port` é a porta na qual os formulários AEM estão sendo executados no servidor de aplicativos.

      `user` é o nome de usuário do administrador de formulários AEM.

      `password` é a senha do administrador dos formulários AEM.

      `leaveContinuousCoverage` Use esta opção para desativar completamente o modo de backup de rolagem.
   >[!NOTE]
   >
   >Enquanto o modo de backup estiver desativado, a cobertura contínua não poderá ser restabelecida. Quaisquer alterações durante esse período não serão protegidas.

   >[!NOTE]
   >
   >Se você ativou o armazenamento do documento no banco de dados, os modos de backup de snapshot e backup de rolagem não são aplicáveis.

   Para obter mais informações sobre a interface da linha de comando para o modo de backup, consulte o arquivo readme no diretório BackupRestoreCommandline.

