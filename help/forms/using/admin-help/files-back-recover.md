---
title: Arquivos para backup e recuperação
seo-title: Arquivos para backup e recuperação
description: Este documento descreve o aplicativo e os arquivos de dados que devem ser submetidos a backup.
seo-description: Este documento descreve o aplicativo e os arquivos de dados que devem ser submetidos a backup.
uuid: ba04adb9-675a-48f2-ad52-39c1266e423b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f9a294d-24bd-4e4b-b929-2809f5e6cef9
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 0%

---


# Arquivos para fazer backup e recuperar {#files-to-back-up-and-recover}

O aplicativo e os arquivos de dados que devem ser submetidos a backup são descritos com mais detalhes nas seções a seguir.

Considere os seguintes pontos em relação ao backup e à recuperação:

* O backup do banco de dados deve ser feito antes do GDS e AEM repositório.
* Se for necessário desativar os nós em um ambiente clusterizado para backup, verifique se os nós secundários foram desligados antes do nó primário. Caso contrário, pode levar a inconsistência no cluster ou servidor. Além disso, o nó primário deve ser ativado antes de qualquer nó secundário.
* Para a operação de restauração de um cluster, o servidor de aplicativos deve ser interrompido para cada nó no cluster.

## Diretório de Armazenamentos globais {#global-document-storage-directory}

O GDS é um diretório usado para armazenar arquivos de longa duração usados em um processo. A vida útil dos arquivos de longa duração tem o objetivo de abranger uma ou mais inicializações de um sistema de formulários AEM e pode durar dias e até mesmo anos. Esses arquivos de longa duração podem incluir PDFs, políticas e modelos de formulário. Arquivos de longa duração são uma parte essencial do estado geral de muitas implantações de formulários AEM. Se alguns ou todos os documentos de longa duração forem perdidos ou corrompidos, o servidor de formulários poderá ficar instável.

Os documentos de entrada para invocação de tarefa assíncrona também são armazenados no GDS e devem estar disponíveis para solicitações de processamento. Portanto, é importante considerar a confiabilidade do sistema de arquivos que hospeda o GDS e empregar uma matriz redundante de discos independentes (RAID) ou outra tecnologia como apropriada para seus requisitos de qualidade e nível de serviço.

O local do GDS é determinado durante o processo de instalação dos formulários AEM ou posterior usando o console de administração. Além de manter um local de alta disponibilidade para o GDS, também é possível ativar o armazenamento do banco de dados para documentos. Consulte [Opções de backup quando o banco de dados for usado para o armazenamento do documento](files-back-recover.md#backup-options-when-database-is-used-for-document-storage).

### Localização GDS {#gds-location}

Se você deixar a configuração de local vazia durante a instalação, o local assumirá como padrão um diretório na instalação do servidor de aplicativos. É necessário fazer backup do seguinte diretório para o servidor de aplicativos:

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

Se você alterou o local GDS para um local não padrão, poderá determinar o seguinte:

* Faça logon no console de administração e clique em Configurações > Configurações principais do sistema > Configurações.
* Registre o local especificado na caixa Diretório do Armazenamento do Documento Global.

Em um ambiente clusterizado, o GDS normalmente aponta para um diretório que é compartilhado na rede e é acessível para leitura/gravação para cada nó de cluster.

A localização do GDS pode ser alterada durante uma recuperação se a localização original já não estiver disponível. (Consulte [Alteração do local GDS durante a recuperação](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).)

### Opções de backup quando o banco de dados é usado para armazenamento de documento {#backup-options-when-database-is-used-for-document-storage}

Você pode ativar AEM armazenamento de documento de formulários no banco de dados de formulários AEM usando o console de administração. Embora essa opção mantenha todos os documentos persistentes no banco de dados, AEM formulários ainda exigem o diretório GDS baseado no sistema de arquivos porque ele é usado para armazenar arquivos permanentes e temporários e recursos relacionados a sessões e invocações de formulários AEM.

Quando você seleciona a opção &quot;Ativar armazenamento de documento no banco de dados&quot; nas Configurações principais do sistema no console de administração ou usando o Configuration Manager, os formulários AEM não permitem o modo de backup de snapshot e o modo de backup de rolagem. Portanto, não é necessário gerenciar modos de backup usando formulários AEM. Se você usar essa opção, deverá fazer backup do GDS apenas uma vez depois de ativar a opção. Ao recuperar AEM formulários de um backup, não é necessário renomear o diretório de backup para o GDS ou restaurar o GDS.

## Repositório AEM {#aem-repository}

AEM repositório (crx-repository) será criado se o crx-repository estiver configurado durante a instalação AEM formulários. A localização do diretório crx-repository é determinada durante o processo de instalação dos formulários AEM. AEM backup e restauração do repositório é necessário juntamente com o banco de dados e o GDS para dados AEM formulários consistentes em formulários AEM. AEM repositório contém dados para a Solução de gerenciamento de correspondência, o Forms Manager e o AEM Forms Workspace.

### Solução de gerenciamento de correspondência {#correspondence-management-solution}

A Solução de gerenciamento de correspondência centraliza e gerencia a criação, a montagem e o delivery de correspondências seguras, personalizadas e interativas. Ele permite que você monte rapidamente correspondência de conteúdo pré-aprovado e de autoria personalizada em um processo simplificado, da criação ao arquivamento. Como resultado, seus clientes obtêm comunicações oportunas, precisas, convenientes, seguras e relevantes. Sua empresa maximiza o valor das interações com o cliente e minimiza o custo e o risco com um processo que é simplificado para facilitar, acelerar e aumentar a produtividade.

Uma configuração simples da Solução de gerenciamento de correspondência inclui uma instância do autor e uma instância de publicação no mesmo computador ou em máquinas diferentes

### gerenciador de formulários {#forms-manager}

o Gerenciador de formulários simplifica o processo de atualização, gerenciamento e aposentadoria de formulários.

### AEM Forms Workspace {#html-workspace}

O AEM Forms Workspace corresponde aos recursos do Flex Workspace (obsoleto para formulários AEM no JEE) e adiciona novos recursos para estender e integrar o Workspace e torná-lo mais fácil de usar.

>[!NOTE]
>
>O Flex Workspace está obsoleto para AEM versão de formulários.

Ele permite o gerenciamento de tarefas em clientes sem Flash Player e Adobe Reader. Ele facilita a execução de Forms HTML, além de formulários PDF forms e Flex.

## Banco de dados de formulários AEM {#aem-forms-database}

O banco de dados de formulários AEM armazena conteúdo como artefatos de formulário, configurações de serviço, estado do processo e referências de banco de dados a arquivos no GDS e no diretório raiz do Armazenamento de conteúdo (para Serviços de conteúdo). Os backups do banco de dados podem ser executados em tempo real sem interrupção no serviço, e a recuperação pode ser feita em um ponto específico no tempo ou para uma alteração específica. Esta seção descreve como configurar seu banco de dados para que possa ser feito backup em tempo real.

Em um sistema de formulários AEM corretamente configurado, o administrador do sistema e o administrador do banco de dados podem colaborar facilmente para recuperar o sistema para um estado consistente e conhecido.

Para fazer backup do banco de dados em tempo real, você deve usar o modo de instantâneo ou configurar seu banco de dados para execução no modo de log especificado. Isso permite que o backup dos arquivos do banco de dados seja feito enquanto o banco de dados estiver aberto e disponível para uso. Além disso, o banco de dados preserva seu rollback e logs de transações quando estiver sendo executado nesses modos.

>[!NOTE]
>
>O Adobe® LiveCycle® Content Services ES (obsoleto) é um sistema de gestão de conteúdo instalado com o LiveCycle. Ela permite que os usuários criem, gerenciem, monitorem e otimizem processos centrados no ser humano. O suporte aos Serviços de conteúdo (obsoleto) termina em 31/12/2014. Consulte [documento do ciclo de vida do produto do Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html). Para saber mais sobre como configurar o Content Services (obsoleto), consulte [Administração do Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).

### DB2 {#db2}

Configure seu banco de dados DB2 para ser executado no modo de log de arquivamento.

>[!NOTE]
>
>Se seu ambiente de formulários AEM foi atualizado de uma versão anterior de formulários AEM e usa DB2, o backup on-line não é suportado. Nesse caso, você deve encerrar AEM formulários e executar um backup offline. Versões futuras de formulários AEM oferecerão suporte a backup on-line para clientes de atualização.

A IBM tem um conjunto de ferramentas e sistemas de ajuda para ajudar os administradores de bancos de dados a gerenciar suas tarefas de backup e recuperação:

* IBM DB2 Archive Log Accelerator (Consulte [IBM DB2 Archive Log Accelerator for z/OS User&#39;s Guide](https://publib.boulder.ibm.com/infocenter/dzichelp/v2r2/topic/com.ibm.db2tools.alc.doc.ug/alcugb20.pdf?noframes=true).)
* Especialista em IBM DB2 Data Archive (Consulte [IBM DB2 Data Archive Expert User&#39;s Guide and Reference](https://publib.boulder.ibm.com/infocenter/mptoolic/v1r0/topic/com.ibm.db2tools.aeu.doc.ug/ahxugb13.pdf?noframes=true).)

O DB2 tem recursos incorporados para fazer backup de um banco de dados para o Tivoli Armazenamento Manager. Usando o Tivoli Armazenamento Manager, os backups DB2 podem ser armazenados em outras mídias ou no disco rígido local.

Para obter mais informações sobre backup e recuperação do banco de dados DB2, consulte [Desenvolvimento de uma estratégia de backup e recuperação para DB2](https://publib.boulder.ibm.com/infocenter/db2luw/v9/index.jsp?topic=/com.ibm.db2.udb.admin.doc/doc/c0005945.htm).

### Oracle {#oracle}

Use backups de snapshot ou configure seu banco de dados Oracle para ser executado no modo de log de arquivamento. (Consulte [Backup do Oracle: Uma Introdução](https://www.databasedesign-resource.com/oracle-backup.md).) Para obter mais informações sobre como fazer backup e recuperar seu banco de dados Oracle, acesse estes sites:

[Backup e recuperação da oracle: ](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) explica os conceitos de backup e recuperação e as técnicas mais comuns de uso do Recovery Manager (RMAN) para backup, recuperação e relatórios com mais detalhes, além de fornecer mais informações sobre como planejar uma estratégia de backup e recuperação.

[Oracle Database Backup and Recovery User&#39;s Guide:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) fornece informações detalhadas sobre arquitetura RMAN, conceitos e mecanismos de backup e recuperação, técnicas avançadas de recuperação, como recursos point-in-time de recuperação e flashback de banco de dados, e ajuste do desempenho de backup e recuperação. Também abrange backup e recuperação gerenciados pelo usuário, usando recursos de sistema operacional host em vez de RMAN. Esse volume é essencial para backup e recuperação de implantações de bancos de dados mais sofisticadas e para cenários de recuperação avançados.

[Referência de backup e recuperação do oracle Database:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) fornece informações completas sobre sintaxe e semântica para todos os comandos RMAN e descreve as visualizações do banco de dados disponíveis para relatórios em atividades de backup e recuperação.

### SQL Server {#sql-server}

Use backups de snapshot ou configure seu banco de dados SQL Server para execução no modo de log de transações.

O SQL Server também fornece duas ferramentas de backup e recuperação:

* SQL Server Management Studio (GUI)
* T-SQL (linha de comando)

Para obter mais informações, consulte [Backup e restauração](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx).

### MySQL {#mysql}

Use MySQLAdmin ou modifique os arquivos INI no Windows para configurar seu banco de dados MySQL para execução no modo de log binário. (Consulte [Registro binário MySQL](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html).) Uma ferramenta de backup dinâmico para MySQL também está disponível no software InnoBase. (Consulte [Innobase Hot Backup](https://www.innodb.com/hot-backup/features.md).)

>[!NOTE]
>
>O modo de log binário padrão para MySQL é &quot;Instrução&quot;, o que é incompatível com tabelas usadas pelo Content Services (obsoleto). O uso do logon binário nesse modo padrão faz com que o Content Services (obsoleto) falhe. Se o seu sistema incluir o Content Services (obsoleto), use o modo de registro &quot;Misto&quot;. Para ativar o registro &quot;Misto&quot;, adicione o seguinte argumento ao arquivo my.ini: `binlog_format=mixed log-bin=logname`

Você pode usar o utilitário mysqldump para obter o backup completo do banco de dados. Backups completos são necessários, mas nem sempre são convenientes. Eles produzem arquivos de backup grandes e levam tempo para gerar. Para fazer um backup incremental, verifique se você start o servidor com a opção - `log-bin`, conforme descrito na seção anterior. Cada vez que o servidor MySQL é reiniciado, ele para de gravar no log binário atual, cria um novo e, a partir daí, o novo se torna o atual. Você pode forçar um switch manualmente com o comando `FLUSH LOGS SQL`. Após o primeiro backup completo, os backups incrementais subsequentes são feitos usando o utilitário mysqladmin com o comando `flush-logs`, que cria o próximo arquivo de log.

Consulte [Resumo da estratégia de backup](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html).

```text
binlog_format=mixed
log-bin=logname
```

## Diretório raiz do Armazenamento de conteúdo (somente Content Services) {#content-storage-root-directory-content-services-only}

O diretório raiz do Armazenamento de conteúdo contém o repositório Content Services (obsoleto) no qual todos os documentos, artefatos e índices são armazenados. É necessário fazer backup da árvore de diretório raiz do Armazenamento de conteúdo. Esta seção descreve como determinar a localização do diretório raiz do Armazenamento de conteúdo para ambientes independentes e agrupados.

### Localização raiz do Armazenamento de conteúdo (ambiente independente) {#content-storage-root-location-stand-alone-environment}

O diretório raiz do Armazenamento de conteúdo é criado quando o Content Services (obsoleto) é instalado. A localização do diretório raiz do Armazenamento de conteúdo é determinada durante o processo de instalação dos formulários AEM.

O local padrão do diretório raiz do Armazenamento de conteúdo é `[aem-forms root]/lccs_data`.

Faça backup dos seguintes diretórios localizados no diretório raiz do Armazenamento de conteúdo:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Se o diretório /backup-lucene-indexes não estiver presente, faça backup do diretório /lucene-indexes, também localizado no diretório raiz do Armazenamento de conteúdo. Se o diretório /backup-lucene-indexes estiver presente, não faça backup do diretório /lucene-indexes porque pode causar erros.

### Localização raiz do Armazenamento de conteúdo (ambiente clusterizado) {#content-storage-root-location-clustered-environment}

Quando você instala o Content Services (obsoleto) em um ambiente clusterizado, o diretório raiz do Armazenamento de conteúdo é dividido em dois diretórios separados:

**Diretório raiz do Armazenamento de conteúdo:** normalmente, um diretório de rede compartilhado que é acessível para leitura/gravação para todos os nós no cluster

**Diretório raiz de índice:** um diretório criado em cada nó do cluster, sempre com o mesmo caminho e nome de diretório

O local padrão do diretório raiz do Armazenamento de conteúdo é `[GDS root]/lccs_data`, onde `[GDS root]` é o local descrito em [localização GDS](files-back-recover.md#gds-location). Faça backup dos seguintes diretórios localizados no diretório raiz do Armazenamento de conteúdo:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Se o diretório /backup-lucene-indexes não estiver presente, faça backup do diretório /lucene-indexes, também localizado no diretório raiz do Armazenamento de conteúdo. Se o diretório /backup-lucene-indexes estiver presente, não faça backup do diretório /lucene-indexes porque pode causar erros.

O local padrão do diretório Raiz do índice é `[aem-forms root]/lucene-indexes` em cada nó.

## Fontes instaladas pelo cliente {#customer-installed-fonts}

Se você instalou fontes adicionais no ambiente de formulários AEM, é necessário fazer o backup separadamente. Faça backup de todos os diretórios de fontes do Adobe e do cliente especificados no console de administração em Configurações > Sistema principal > Configurações. Certifique-se de fazer backup do diretório de fontes inteiro.

>[!NOTE]
>
>Por padrão, as fontes Adobe instaladas com AEM formulários estão localizadas no diretório `[aem-forms root]/fonts`.

Se você estiver reinicializando o sistema operacional no computador host e quiser usar fontes do sistema operacional anterior, o backup do conteúdo do diretório de fontes do sistema também deverá ser feito. (Para obter instruções específicas, consulte a documentação do seu sistema operacional).
