---
title: Arquivos para backup e recuperação
seo-title: Files to back up and recover
description: Este documento descreve o aplicativo e os arquivos de dados que devem ser copiados em backup.
seo-description: This document describes the application and data files that must be backed up.
uuid: ba04adb9-675a-48f2-ad52-39c1266e423b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f9a294d-24bd-4e4b-b929-2809f5e6cef9
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 0%

---

# Arquivos para backup e recuperação {#files-to-back-up-and-recover}

O aplicativo e os arquivos de dados que devem ser submetidos a backup são descritos com mais detalhes nas seções a seguir.

Considere os seguintes pontos em relação ao backup e à recuperação:

* O backup do banco de dados deve ser feito antes do GDS e AEM repositório.
* Se precisar desativar os nós em um ambiente clusterizado em cluster para backup, verifique se os nós secundários são desligados antes do nó principal. Caso contrário, pode levar à inconsistência no cluster ou no servidor. Além disso, o nó principal deve ser ativado antes de qualquer nó secundário.
* Para a operação de restauração de um cluster, o servidor de aplicativos deve ser interrompido para cada nó no cluster.

## Diretório de armazenamento de documentos global {#global-document-storage-directory}

O GDS é um diretório usado para armazenar arquivos de longa duração usados em um processo. O tempo de vida dos arquivos de longa duração destina-se a cobrir uma ou mais inicializações de um sistema de formulários de AEM e pode durar dias e até anos. Esses arquivos de longa duração podem incluir PDF, políticas e modelos de formulário. Arquivos de longa duração são uma parte essencial do estado geral de muitas implantações de formulários AEM. Se alguns ou todos os documentos de longa duração forem perdidos ou corrompidos, o servidor de formulários poderá se tornar instável.

Os documentos de entrada para invocação assíncrona de trabalho também são armazenados no GDS e devem estar disponíveis para processar solicitações. Portanto, é importante que você considere a confiabilidade do sistema de arquivos que hospeda o GDS e utilize uma matriz redundante de discos independentes (RAID) ou outra tecnologia, conforme apropriado para seus requisitos de qualidade e nível de serviço.

O local do GDS é determinado durante o processo de instalação dos formulários AEM ou posteriormente usando o console de administração. Além de manter um local de alta disponibilidade para GDS, você também pode ativar o armazenamento de banco de dados para documentos. Consulte [Opções de backup quando o banco de dados é usado para armazenamento de documentos](files-back-recover.md#backup-options-when-database-is-used-for-document-storage).

### Localização GDS {#gds-location}

Se você deixar a configuração de localização vazia durante a instalação, o local assumirá como padrão um diretório na instalação do servidor de aplicativos. Você deve fazer backup do seguinte diretório para o seu servidor de aplicativos:

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

Se você alterou o local GDS para um local não padrão, é possível determiná-lo da seguinte maneira:

* Faça logon no console de administração e clique em Configurações > Configurações principais do sistema > Configurações.
* Registre o local especificado na caixa Diretório de Armazenamento de Documento Global.

Em um ambiente em cluster, o GDS normalmente aponta para um diretório que é compartilhado na rede e é acessível para leitura/gravação em cada nó do cluster.

A localização do GDS pode ser alterada durante uma recuperação se a localização original já não estiver disponível. (Consulte [Alteração da localização do GDS durante a recuperação](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).)

### Opções de backup quando o banco de dados é usado para armazenamento de documentos {#backup-options-when-database-is-used-for-document-storage}

Você pode habilitar AEM armazenamento de documentos de formulários no banco de dados de formulários AEM usando o console de administração. Embora essa opção mantenha todos os documentos persistentes no banco de dados, AEM formulários ainda exigem o diretório GDS baseado no sistema de arquivos porque é usado para armazenar arquivos permanentes e temporários e recursos relacionados a sessões e invocações de AEM formulários.

Ao selecionar a opção &quot;Ativar armazenamento de documentos no banco de dados&quot; nas Configurações do Sistema Principal no console de administração ou usando o Configuration Manager, os formulários AEM não permitem o modo de backup de snapshot e o modo de backup contínuo. Portanto, não é necessário gerenciar modos de backup usando formulários AEM. Se você usar essa opção, deverá fazer backup do GDS apenas uma vez depois de habilitar a opção. Ao recuperar formulários AEM de um backup, não é necessário renomear o diretório de backup para o GDS ou restaurar o GDS.

## Repositório AEM {#aem-repository}

AEM repositório (crx-repository) será criado se o crx-repository estiver configurado ao instalar AEM formulários. A localização do diretório crx-repository é determinada durante o processo de instalação do AEM forms. AEM backup e restauração do repositório é necessário juntamente com o banco de dados e o GDS para obter dados de formulários AEM consistentes em AEM formulários. AEM repositório contém dados para a Solução de gerenciamento de correspondência, Forms Manager e AEM Forms Workspace.

### Solução de gerenciamento de correspondência {#correspondence-management-solution}

A Solução de gerenciamento de correspondência centraliza e gerencia a criação, montagem e delivery de correspondências seguras, personalizadas e interativas. Ele permite reunir rapidamente correspondência de conteúdo pré-aprovado e de autoria personalizada em um processo simplificado, da criação ao arquivamento. Como resultado, seus clientes obtêm comunicações oportunas, precisas, convenientes, seguras e relevantes. Sua empresa maximiza o valor das interações do cliente e minimiza o custo e o risco com um processo simplificado para facilidade, velocidade e produtividade.

Uma configuração simples de Solução de gerenciamento de correspondência inclui uma instância de autor e uma instância de publicação no mesmo computador ou em máquinas diferentes

### gerenciador de formulários {#forms-manager}

o gerente de formulários simplifica o processo de atualização, gerenciamento e aposentação de formulários.

### AEM Forms Workspace {#html-workspace}

O AEM Forms Workspace corresponde aos recursos do Flex Workspace (obsoleto para formulários AEM no JEE) e adiciona novos recursos para estender e integrar o Workspace e torná-lo mais fácil de usar.

>[!NOTE]
>
>O Flex Workspace está obsoleto para a versão AEM formulários.

Permite o gerenciamento de tarefas em clientes sem o Flash Player e o Adobe Reader. Ele facilita a representação do HTML Forms, além de formulários PDF forms e Flex.

## Banco de dados de formulários AEM {#aem-forms-database}

O banco de dados de formulários de AEM armazena conteúdo, como artefatos de formulário, configurações de serviço, estado do processo e referências de banco de dados a arquivos no GDS e no diretório raiz do armazenamento de conteúdo (para Serviços de conteúdo). Os backups do banco de dados podem ser executados em tempo real, sem interrupção do serviço, e a recuperação pode chegar a um ponto específico no tempo ou a uma alteração específica. Esta seção descreve como configurar o banco de dados para que seja possível fazer backup dele em tempo real.

Em um sistema de formulários AEM corretamente configurado, o administrador do sistema e o administrador do banco de dados podem colaborar facilmente para recuperar o sistema para um estado consistente e conhecido.

Para fazer o backup do banco de dados em tempo real, você deve usar o modo de instantâneo ou configurar o banco de dados para ser executado no modo de log especificado. Isso permite que o backup dos arquivos do banco de dados seja feito enquanto o banco de dados estiver aberto e disponível para uso. Além disso, o banco de dados preserva seu rollback e logs de transações quando ele está em execução nesses modos.

>[!NOTE]
>
>O Adobe® LiveCycle® Content Services ES (obsoleto) é um sistema de gerenciamento de conteúdo instalado com o LiveCycle. Ele permite que os usuários criem, gerenciem, monitorem e otimizem processos centrados em seres humanos. O suporte aos Serviços de conteúdo (obsoleto) termina em 31/12/2014. Consulte [Documento de ciclo de vida do produto Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

### DB2 {#db2}

Configure seu banco de dados do DB2 para ser executado no modo de log de arquivamento.

>[!NOTE]
>
>Se o seu ambiente de AEM forms tiver sido atualizado de uma versão anterior de AEM forms e usar DB2, o backup online não será suportado. Nesse caso, você deve encerrar AEM formulários e executar um backup offline. As versões futuras de formulários AEM oferecerão suporte a backup online para clientes de atualização.

A IBM tem um conjunto de ferramentas e sistemas de ajuda para ajudar os administradores de bancos de dados a gerenciar suas tarefas de backup e recuperação:

* Acelerador de registro do arquivo IBM DB2
* Especialista em arquivamento de dados IBM DB2

O DB2 tem recursos incorporados para fazer backup de um banco de dados no Tivoli Storage Manager. Ao usar o Tivoli Storage Manager, os backups do DB2 podem ser armazenados em outras mídias ou no disco rígido local.

### Oracle {#oracle}

Use backups de snapshot ou configure o banco de dados do Oracle para ser executado no modo de log de arquivamento. (Consulte [Backup do Oracle: Uma Introdução](https://www.databasedesign-resource.com/oracle-backup.md).) Para obter mais informações sobre como fazer backup e recuperar o banco de dados do Oracle, acesse estes sites:

[Backup e recuperação do Oracle:](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) Explica os conceitos de backup e recuperação e as técnicas mais comuns de uso do RMAN (Recovery Manager, Gerenciador de Recuperação) para backup, recuperação e emissão de relatórios com mais detalhes, além de fornecer mais informações sobre como planejar uma estratégia de backup e recuperação.

[Oracle Database Backup and Recovery User&#39;s Guide:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) Fornece informações detalhadas sobre arquitetura RMAN, conceitos e mecanismos de backup e recuperação, técnicas avançadas de recuperação, como recursos point-in-time de recuperação e flashback de banco de dados, e ajuste do desempenho de backup e recuperação. Também abrange backup e recuperação gerenciados pelo usuário, usando recursos do sistema operacional host em vez de RMAN. Esse volume é essencial para backup e recuperação de implantações de banco de dados mais sofisticadas e para cenários de recuperação avançados.

[Referência de Backup e Recuperação do Banco de Dados do Oracle:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) Fornece informações completas sobre sintaxe e semântica para todos os comandos RMAN e descreve as visualizações de banco de dados disponíveis para relatórios sobre atividades de backup e recuperação.

### SQL Server {#sql-server}

Use backups de snapshot ou configure o banco de dados do SQL Server para ser executado no modo de log de transações.

O SQL Server também fornece duas ferramentas de backup e recuperação:

* SQL Server Management Studio (GUI)
* T-SQL (linha de comando)

Para obter mais informações, consulte [Backup e restauração](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx).

### MySQL {#mysql}

Use MySQLAdmin ou modifique os arquivos INI no Windows para configurar seu banco de dados MySQL para ser executado no modo de log binário. (Consulte [Registro binário do MySQL](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html).) Uma ferramenta de hot backup para MySQL também está disponível no software InnoBase. (Consulte [Innobase Hot Backup](https://www.innodb.com/hot-backup/features.md).)

>[!NOTE]
>
>O modo de log binário padrão do MySQL é &quot;Instrução&quot;, que é incompatível com as tabelas usadas pelos Content Services (obsoleto). Usar o logon binário nesse modo padrão faz com que os Serviços de conteúdo (obsoleto) falhem. Se o seu sistema incluir Serviços de conteúdo (obsoleto), use o modo de registro &quot;Misto&quot;. Para ativar o registro &quot;Mixed&quot;, adicione o seguinte argumento ao arquivo my.ini: `binlog_format=mixed log-bin=logname`

Você pode usar o utilitário mysqldump para obter o backup completo do banco de dados. São necessários backups completos, mas nem sempre são convenientes. Eles produzem arquivos de backup grandes e levam tempo para gerar. Para fazer um backup incremental, certifique-se de iniciar o servidor com o - `log-bin` conforme descrito na seção anterior. Cada vez que o servidor MySQL é reiniciado, ele para de escrever no log binário atual, cria um novo e, a partir daí, o novo se torna o atual. Você pode forçar um switch manualmente com o `FLUSH LOGS SQL` comando. Após o primeiro backup completo, os backups incrementais subsequentes são feitos usando o utilitário mysqladmin com o `flush-logs` , que cria o próximo arquivo de log.

Consulte [Resumo da estratégia de backup](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html).

```text
binlog_format=mixed
log-bin=logname
```

## Diretório raiz do armazenamento de conteúdo (somente Serviços de conteúdo) {#content-storage-root-directory-content-services-only}

O diretório raiz do armazenamento de conteúdo contém o repositório Content Services (obsoleto), onde todos os documentos, artefatos e índices são armazenados. É necessário fazer backup da árvore de diretório raiz do armazenamento de conteúdo. Esta seção descreve como determinar a localização do diretório raiz do armazenamento de conteúdo para ambientes independentes e em cluster.

### Local raiz do armazenamento de conteúdo (ambiente independente) {#content-storage-root-location-stand-alone-environment}

O diretório raiz do armazenamento de conteúdo é criado quando o Content Services (obsoleto) é instalado. A localização do diretório raiz do armazenamento de conteúdo é determinada durante o processo de instalação dos formulários AEM.

O local padrão do diretório raiz do armazenamento de conteúdo é `[aem-forms root]/lccs_data`.

Faça backup dos seguintes diretórios localizados no diretório raiz do armazenamento de conteúdo:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Se o diretório /backup-lucene-indexes não estiver presente, faça backup do diretório /lucene-indexes, também localizado no diretório raiz do armazenamento de conteúdo. Se o diretório /backup-lucene-indexes estiver presente, não faça backup do diretório /lucene-indexes porque pode causar erros.

### Local raiz do armazenamento de conteúdo (ambiente em cluster) {#content-storage-root-location-clustered-environment}

Quando você instala os Serviços de conteúdo (obsoletos) em um ambiente em cluster, o diretório Raiz do armazenamento de conteúdo é dividido em dois diretórios separados:

**Diretório raiz do armazenamento de conteúdo:** Normalmente, um diretório de rede compartilhado que é acessível para leitura/gravação para todos os nós no cluster

**Diretório raiz de índice:** Um diretório criado em cada nó no cluster, sempre com o mesmo caminho e nome de diretório

O local padrão do diretório raiz do armazenamento de conteúdo é `[GDS root]/lccs_data`, onde `[GDS root]` é o local descrito em [Localização GDS](files-back-recover.md#gds-location). Faça backup dos seguintes diretórios localizados no diretório raiz do armazenamento de conteúdo:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Se o diretório /backup-lucene-indexes não estiver presente, faça backup do diretório /lucene-indexes, também localizado no diretório raiz do armazenamento de conteúdo. Se o diretório /backup-lucene-indexes estiver presente, não faça backup do diretório /lucene-indexes porque pode causar erros.

O local padrão do diretório Raiz de Índice é `[aem-forms root]/lucene-indexes` em cada nó.

## Fontes instaladas pelo cliente {#customer-installed-fonts}

Se você instalou fontes adicionais no seu ambiente de formulários AEM, é necessário fazer backup delas separadamente. Faça o backup de todos os diretórios de fontes do Adobe e do cliente especificados no console de administração em Configurações > Sistema principal > Configurações. Certifique-se de fazer backup do diretório de fonte inteiro.

>[!NOTE]
>
>Por padrão, as fontes do Adobe instaladas com AEM formulários estão localizadas na variável `[aem-forms root]/fonts` diretório.

Se você estiver reinicializando o sistema operacional no computador host e quiser usar fontes do sistema operacional anterior, o conteúdo do diretório de fontes do sistema também deverá ser copiado em backup. (Para obter instruções específicas, consulte a documentação do seu sistema operacional).
