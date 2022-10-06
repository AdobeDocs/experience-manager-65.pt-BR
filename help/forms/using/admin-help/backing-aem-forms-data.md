---
title: Backup dos dados dos formulários AEM
seo-title: Backing up the AEM forms data
description: Este documento descreve as etapas necessárias para concluir um backup on-line ou ativo do banco de dados de formulários AEM, do GDS e dos diretórios raiz do armazenamento de conteúdo.
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

# Backup dos dados dos formulários AEM {#backing-up-the-aem-forms-data}

Esta seção descreve as etapas necessárias para concluir um backup on-line ou ativo do banco de dados de formulários AEM, do GDS e dos diretórios raiz do armazenamento de conteúdo.

Depois que AEM formulários for instalado e implantado em áreas de produção, o administrador do banco de dados deverá executar um backup inicial completo ou frio do banco de dados. O banco de dados deve ser desligado para esse backup. Em seguida, backups diferenciais ou incrementais (ou ativos) do banco de dados devem ser feitos regularmente.

Para garantir um backup e uma recuperação bem-sucedidos, um backup de imagem do sistema deve estar sempre disponível. Em seguida, se ocorrer uma perda, é possível recuperar todo o ambiente para um estado consistente.

Fazer o backup do banco de dados ao mesmo tempo que os backups do diretório GDS, do repositório AEM e da Raiz do Armazenamento de Conteúdo ajuda a manter esses sistemas sincronizados se a recuperação alguma vez for necessária.

O procedimento de backup descrito nesta seção requer que você entre no modo de backup seguro antes de fazer o backup do banco de dados de formulários AEM, do repositório AEM, do GDS e dos diretórios raiz do armazenamento de conteúdo. Quando o backup é concluído, você deve sair do modo de backup seguro. O modo de backup seguro é usado para marcar documentos persistentes e de longa duração que residem no GDS. Esse modo garante que o mecanismo de limpeza automática de arquivos (o coletor de arquivos) não exclua arquivos expirados até que o modo de backup seguro seja lançado. É necessário manter um backup GDS em sincronização com um backup de banco de dados.

A frequência com que o backup do local GDS deve ser feito depende de como os formulários AEM são usados e das janelas de backup disponíveis. A janela de backup pode ser afetada por processos de longa duração, pois eles podem ser executados por vários dias. Se você estiver alterando, adicionando e removendo continuamente arquivos nesse diretório, faça backup do local GDS com mais frequência.

Se o banco de dados estiver sendo executado em um modo de registro, conforme descrito na seção anterior, os logs do banco de dados também deverão ser copiados com frequência para que possam ser usados para restaurar o banco de dados em caso de falha de mídia.

>[!NOTE]
>
>Os arquivos que não são referenciados podem persistir no diretório GDS após o processo de recuperação. Essa é uma limitação conhecida no momento.

## Faça backup do banco de dados, GDS, repositório AEM e diretórios raiz do armazenamento de conteúdo {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

Você deve colocar AEM formulários no modo de backup seguro (instantâneo) ou no modo de backup contínuo (cobertura contínua). Antes de definir AEM formulários para inserir um dos modos de backup, verifique o seguinte:

* Verifique a versão do sistema e registre os patches ou atualizações aplicadas desde que o último backup completo da imagem do sistema foi executado.
* Se você estiver usando backups em modo de rolagem ou de snapshot, certifique-se de que seu banco de dados esteja configurado com as configurações de log corretas para permitir backups ativos do banco de dados. (Consulte [Banco de dados de formulários AEM](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

Além disso, observe as diretrizes a seguir para o processo de backup/restauração.

* Faça backup do diretório GDS usando um sistema operacional disponível ou um utilitário de backup de terceiros. (Consulte [Localização GDS](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* (Opcional) Faça backup do diretório raiz do armazenamento de conteúdo usando um sistema operacional disponível ou um backup e utilitário de terceiros. (Consulte [Local raiz do armazenamento de conteúdo (ambiente independente)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) ou [Local raiz do armazenamento de conteúdo (ambiente em cluster)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* Faça backup das instâncias de criação e publicação (crx - backup do repositório).

   Para fazer backup do ambiente da Solução de gerenciamento de correspondência, execute as etapas nas instâncias de criação e publicação, conforme descrito em [Backup e restauração](/help/sites-administering/backup-and-restore.md).

   Considere os seguintes pontos ao fazer backup das instâncias de autor e publicação:

   * Certifique-se de que o backup das instâncias de autor e publicação seja sincronizado para iniciar ao mesmo tempo.Embora você possa continuar a usar as instâncias de autor e publicação enquanto o backup estiver sendo executado, é recomendável não publicar nenhum ativo durante o backup para evitar quaisquer alterações não capturadas. Aguarde até que o backup das instâncias de autor e publicação termine antes de publicar novos ativos.
   * O backup completo do nó Autor inclui o backup dos dados do Forms Manager e do AEM Forms Workspace.
   * Os desenvolvedores do Workbench podem continuar trabalhando em seus processos localmente. Eles não devem implantar novos processos durante a fase de backup.
   * A decisão sobre a duração de cada sessão de backup (para o modo de backup em andamento) deve se basear no tempo total necessário para fazer backup de todos os dados em formulários AEM (BD, GDS, repositório AEM e quaisquer outros dados personalizados adicionais).

Você deve fazer backup do banco de dados de formulários AEM, incluindo quaisquer logs de transação. (Consulte [Banco de dados de formulários AEM](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Para obter mais informações, consulte o artigo da base de conhecimento apropriado para seu banco de dados:

* [Backup e recuperação do Oracle para formulários AEM](https://www.adobe.com/go/kb403624)
* [Backup e recuperação do MySQL para formulários AEM](https://www.adobe.com/go/kb403625)
* [Backup e recuperação do Microsoft SQL Server para formulários AEM](https://www.adobe.com/go/kb403623)
* [Backup e recuperação do DB2 para formulários AEM](https://www.adobe.com/go/kb403626)

Esses artigos fornecem orientação para os recursos básicos de banco de dados para backup e recuperação de dados. Eles não são destinados a Guias técnicos abrangentes de um recurso específico de backup e recuperação de banco de dados de um fornecedor. Eles destacam os comandos necessários para criar uma estratégia de backup de banco de dados confiável para seus dados de aplicativo AEM forms.

>[!NOTE]
>
>O backup do banco de dados deve ser concluído antes de você começar a fazer o backup do GDS. Se o backup do banco de dados não estiver concluído, seus dados estarão fora de sincronia.

### Inserir os modos de backup {#entering-the-backup-modes}

Você pode usar o console de administração, o comando LCBackupMode ou a API disponível com a instalação dos formulários AEM para entrar e sair dos modos de backup. Observe que para o backup contínuo (cobertura contínua), a opção de console de administração não está disponível; você deve usar a opção de linha de comando ou a API. <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Se você tiver configurado o SSL no servidor de formulários, não será possível colocar o servidor de formulários no modo de backup usando o script LCBackupMode.CMD.

**Usar o console de administração para entrar no modo de backup seguro**

1. Faça logon no console de administração.
1. Clique em Configurações > Configurações principais do sistema > Utilitários de backup.
1. Selecione Operar no modo de backup seguro e clique em OK.

   Esse método coloca formulários AEM no modo de backup indefinidamente (sem tempo limite) e entra no modo de instantâneo em vez de no modo de backup contínuo.

**Usando a opção de linha de comando para entrar no modo de backup seguro**

Você pode usar a interface da linha de comando `LCBackupMode` scripts para colocar AEM formulários no modo de backup seguro.

1. Defina ADOBE_LIVECYCLE e inicie o servidor de aplicativos.
1. Vá para o `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` pasta.
1. Dependendo do seu sistema operacional, edite a variável `LCBackupMode.cmd` ou `LCBackupMode.sh` para fornecer valores padrão adequados ao seu sistema.
1. No prompt de comando, execute o seguinte comando em uma única linha:

   * (Windows) `LCBackupMode.cmd enter [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*senha* `] [-label=`*labelname* `] [-timeout=`*segundos* `]`
   * (Linux, UNIX) `LCBackupMode.sh enter [-host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*senha* `] [-label=`*labelname* `]`

   Nos comandos anteriores, os espaços reservados são definidos da seguinte maneira:

   `Host` é o nome do host em que AEM formulários está sendo executados.

   `port` é a porta WebServices do servidor de aplicativos em que AEM formulários está sendo executado.

   `user` é o nome de usuário do administrador do AEM forms.

   `password` é a senha do administrador do AEM forms.

   `label` é o rótulo do texto, que pode ser qualquer string, para esse backup.

   `timeout` é o número de segundos após o qual o modo de backup é automaticamente deixado. Pode ser de 0 a 10.080. Se for 0, que é o padrão, o modo de backup nunca expirará.

   Para obter mais informações sobre a interface da linha de comando para o modo de backup, consulte o arquivo Leiame no diretório BackupRestoreCommandline .

### Deixando modos de backup {#leaving-backup-modes}

Você pode usar o console de administração ou a opção de linha de comando para deixar os modos de backup.

**Deixe o modo de backup seguro (modo de instantâneo)**

Para usar o Console de administração para tirar AEM formulários do modo de backup seguro (modo de instantâneo), execute as seguintes tarefas.

1. Faça logon no Console de administração.
1. Clique em Configurações > Configurações principais do sistema > Utilitários de backup.
1. Desmarque Operar no modo de backup seguro e clique em OK.

**Deixe todos os modos de backup**

Você pode usar a interface da linha de comando para retirar AEM formulários do modo de backup seguro (modo de instantâneo) ou para encerrar a sessão atual do modo de backup (modo de acumulado). Observe que você não pode usar o console de administração para sair do modo de backup contínuo. Enquanto no modo de backup contínuo, os controles de Utilitários de Backup no Console de Administração são desativados. Você deve usar uma chamada de API ou o comando LCBackupMode .

1. Vá para o `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` pasta.
1. Dependendo do seu sistema operacional, edite a variável `LCBackupMode.cmd` ou `LCBackupMode.sh` para fornecer valores padrão adequados ao seu sistema.

   >[!NOTE]
   >
   >Você deve definir o diretório JAVA_HOME conforme descrito no capítulo apropriado para seu servidor de aplicativos em [Preparação para instalar formulários AEM](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. Execute o seguinte comando em uma única linha:

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*senha* `]`
   * (Linux, UNIX) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*senha* `]`

      Nos comandos anteriores, os espaços reservados são definidos da seguinte maneira:

      `Host` é o nome do host em que AEM formulários está sendo executados.

      `port` é a porta em que AEM formulários está sendo executado no servidor de aplicativos.

      `user` é o nome de usuário do administrador do AEM forms.

      `password` é a senha do administrador do AEM forms.

      `leaveContinuousCoverage` Use esta opção para desativar completamente o modo de backup em andamento.
   >[!NOTE]
   >
   >Durante o tempo em que o modo de backup estiver desativado, a cobertura contínua não poderá ser restabelecida. Quaisquer alterações durante esse período não serão protegidas.

   >[!NOTE]
   >
   >Se você ativou o armazenamento de documentos no banco de dados, o modo de backup de snapshot e os modos de backup de rolagem não são aplicáveis.

   Para obter mais informações sobre a interface da linha de comando para o modo de backup, consulte o arquivo readme no diretório BackupRestoreCommandline.
