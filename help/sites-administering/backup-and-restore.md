---
title: Backup e restauração
seo-title: Backup e restauração
description: Saiba como fazer backup e restaurar seu conteúdo AEM.
seo-description: Saiba como fazer backup e restaurar seu conteúdo AEM.
uuid: 446a466f-f508-4430-9e50-42cd4463760e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: eb8bbb85-ca2f-4877-8ee0-bb1ee8b7d8de
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '2295'
ht-degree: 0%

---


# Backup e restauração{#backup-and-restore}

Há duas maneiras de fazer backup e restaurar o conteúdo do repositório no AEM:

* Você pode criar um backup externo do repositório e armazená-lo em um local seguro. Se o repositório for detalhado, você poderá restaurá-lo para o estado anterior.
* Você pode criar versões internas do conteúdo do repositório. Essas versões são armazenadas no repositório juntamente com o conteúdo, de modo que você possa restaurar rapidamente os nós e as árvores que você alterou ou excluiu.

## Geral {#general}

A abordagem descrita aqui se aplica ao backup e à recuperação do sistema.

Se precisar fazer backup e/ou recuperar uma pequena quantidade de conteúdo, que é perdida, a recuperação do sistema não é necessária:

* Você pode obter os dados de outro sistema por meio de um pacote
* ou você restaura o backup em um sistema temporário, cria um pacote de conteúdo e o implanta no sistema, onde esse conteúdo está ausente.

Para obter detalhes, consulte [Backup do pacote](/help/sites-administering/backup-and-restore.md#package-backup) abaixo.

## Tempo {#timing}

Não execute o backup em paralelo à coleta de lixo do armazenamento de dados, pois isso pode prejudicar os resultados de ambos os processos.

## Backup offline {#offline-backup}

Você sempre pode fazer um backup offline. Isso requer um tempo de inatividade de AEM, mas pode ser bastante eficiente em termos de tempo necessário em comparação a um backup on-line.

Na maioria dos casos, você usará um instantâneo do sistema de arquivos para criar uma cópia somente leitura do armazenamento nesse momento. Para criar um backup offline, execute estas etapas:

* interromper o aplicativo
* fazer um backup de snapshot
* start do aplicativo

Como o backup de snapshot geralmente leva apenas alguns segundos, o tempo de inatividade total é menor que alguns minutos.

## Backup on-line {#online-backup}

Este método de backup cria um backup de todo o repositório, incluindo quaisquer aplicativos implantados sob ele, como AEM. O backup inclui conteúdo, histórico de versões, configuração, software, hotfixes, aplicativos personalizados, arquivos de registro, índices de pesquisa e assim por diante. Se você estiver usando clustering e se a pasta compartilhada for um subdiretório de `crx-quickstart` (fisicamente ou usando um softlink), o diretório compartilhado também terá backup.

Você pode restaurar o repositório inteiro (e quaisquer aplicativos) posteriormente.

Este método opera como um backup &quot;ativo&quot; ou &quot;on-line&quot; para que possa ser executado enquanto o repositório estiver em execução. Portanto, o repositório é utilizável enquanto o backup está em execução. Esse método funciona para as instâncias padrão do repositório, baseadas em armazenamentos Tar.

Ao criar um backup, você tem as seguintes opções:

* Fazendo backup em um diretório usando AEM ferramenta de backup integrada.
* Fazendo backup em um diretório usando um instantâneo de sistema de arquivos

Em qualquer caso, o backup cria uma imagem (ou um instantâneo) do repositório. Em seguida, o agente de backup de sistemas deve tomar cuidado para transferir essa imagem para um sistema de backup dedicado (unidade de fita).

>[!NOTE]
>
>Se AEM recurso de Backup On-line for usado em uma instância AEM que tenha uma configuração personalizada de blobstore, é recomendável configurar o caminho do armazenamento de dados para que esteja fora do diretório &quot; `crx-quickstart`&quot; e fazer backup do armazenamento de dados separadamente.

>[!CAUTION]
>
>O backup on-line faz backup apenas do sistema de arquivos. Se você armazenar o conteúdo do repositório e/ou os arquivos do repositório em um banco de dados, esse banco de dados precisará fazer backup separadamente. Se você estiver usando AEM com MongoDB, consulte a documentação sobre como usar as [ferramentas de backup nativas MongoDB](https://docs.mongodb.org/manual/tutorial/backup-with-mongodump/).

### AEM Online Backup {#aem-online-backup}

Um backup on-line do repositório permite que você crie, baixe e exclua arquivos de backup. É um recurso de backup &quot;ativo&quot; ou &quot;on-line&quot;, portanto, pode ser executado enquanto o repositório está sendo usado normalmente no modo de leitura/gravação.

>[!CAUTION]
>
>Não execute AEM Backup Online em simultâneo com [Coleta de Lixo de Armazenamento de Dados](/help/sites-administering/data-store-garbage-collection.md) ou [Limpeza de Revisão](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup). Isso afetará negativamente o desempenho do sistema.

Ao iniciar um backup, você pode especificar um **Caminho do Público alvo** e/ou um **Atraso**.

**Caminho** do público alvoOs arquivos de backup geralmente são salvos na pasta pai da pasta que contém o arquivo jar de início rápido (.jar). Por exemplo, se você tiver o arquivo jar AEM localizado em /InstallationKits/AEM, o backup será gerado em /InstallationKits. Você também pode especificar um público alvo para um local de sua escolha.

Se **TargetPath** for um diretório, a imagem do repositório será criada nesse diretório. Se o mesmo diretório for usado várias vezes (ou sempre) para armazenar backup,

* os arquivos modificados no repositório são modificados de acordo com o TargetPath
* os arquivos excluídos no repositório são excluídos no TargetPath
* os arquivos criados no repositório são criados no TargetPath

>[!NOTE]
>
>Se **TargetPath** estiver definido como nome de arquivo com a extensão **.zip**, o backup do repositório será feito em um diretório temporário e o conteúdo desse diretório temporário será compactado e armazenado no arquivo ZIP.
>
>Esta abordagem é desencorajadora, porque
>
>* requer armazenamento de disco adicional durante o processo de backup (diretório temporário mais o arquivo zip)
>* o processo de compactação é feito pelo repositório e pode influenciar seu desempenho.
>* Atrasa o processo de backup.
>* Até o Java 1.6, o Java só pode criar arquivos ZIP com até 4 gigabytes.

>
>
Se precisar criar um ZIP como formato de backup, faça backup em um diretório e use um programa de compactação para criar o arquivo zip.

**** AtrasoIndica um atraso (em milissegundos), para que o desempenho do repositório não seja afetado. Por padrão, o backup do repositório é executado em velocidade máxima. Você pode diminuir a velocidade de criação de um backup on-line, de modo que isso não diminua a velocidade de outras tarefas.

Ao usar um atraso muito grande, verifique se o backup on-line não leva mais de 24 horas. Se o fez, descarte esse backup, pois ele pode não conter todos os binários.
Um atraso de 1 milissegundo normalmente resulta em 10% de uso da CPU e um atraso de 10 milissegundos normalmente resulta em menos de 3% de uso da CPU. O atraso total em segundos pode ser estimado da seguinte forma: Tamanho do repositório em MB, multiplicado pelo atraso em milissegundos, dividido por 2 (se a opção zip for usada) ou dividido por 4 (ao fazer backup em um diretório). Isso significa que o backup em um diretório de um repositório de 200 MB com atraso de 1 ms aumenta o tempo de backup em cerca de 50 segundos.

>[!NOTE]
>
>Consulte [Como o AEM Online Backup funciona](#how-aem-online-backup-works) para obter detalhes internos do processo.

Para criar um backup:

1. Faça logon no AEM como administrador.

1. Vá para **Ferramentas - Operações - Backup.**
1. Clique em **Criar**. O console de backup será aberto.

   ![chlimage_1-1](assets/chlimage_1-1a.png)

1. No console de backup, especifique **[Caminho do Público alvo](#aem-online-backup)** e **[Atraso](#aem-online-backup)**.

   ![chlimage_1-2](assets/chlimage_1-2a.png)

   >[!NOTE]
   >
   >O console de backup também está disponível usando:
   >
   >
   >` https://<*hostname*>:<*port-number*>/libs/granite/backup/content/admin.html`

1. Clique em **Salvar**, uma barra de progresso indicará o progresso do backup.

   >[!NOTE]
   >
   >Você pode **Cancelar** um backup em execução a qualquer momento.

1. Quando o backup for concluído, os arquivos zip serão listados na janela de backup.

   ![chlimage_1-3](assets/chlimage_1-3a.png)

   >[!NOTE]
   >
   >Os arquivos de backup que não são mais necessários podem ser removidos usando o console. Selecione o arquivo de backup no painel esquerdo e clique em **Excluir**.

   >[!NOTE]
   >
   >Se tiver feito backup em um diretório: depois que o processo de backup for concluído, AEM não gravará no diretório do público alvo.

### Automatizando AEM Backup Online {#automating-aem-online-backup}

Se possível, o backup on-line deve ser executado quando houver pouca carga no sistema, por exemplo pela manhã.

Os backups podem ser automatizados usando os clientes HTTP `wget` ou `curl`. Os exemplos a seguir mostram como automatizar o backup usando o curl.

#### Fazendo backup no Diretório de Públicos alvos padrão {#backing-up-to-the-default-target-directory}

>[!CAUTION]
>
>No exemplo a seguir, vários parâmetros no comando `curl` podem precisar ser configurados para sua instância; por exemplo, o nome do host ( `localhost`), a porta ( `4502`), a senha do administrador ( `xyz`) e o nome do arquivo ( `backup.zip`).

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=backup.zip
```

O arquivo/diretório de backup é criado no servidor na pasta pai da pasta que contém a pasta `crx-quickstart` (o mesmo que você estivesse criando o backup usando o navegador). Por exemplo, se você instalou AEM no diretório `/InstallationKits/crx-quickstart/`, o backup é criado no diretório `/InstallationKits`.

O comando curl retorna imediatamente, portanto, você deve monitorar esse diretório para ver quando o arquivo zip está pronto. Enquanto o backup estiver sendo criado, um diretório temporário (com o nome baseado no do arquivo zip final) pode ser visto, no final, isso será zipado. Por exemplo:

* nome do arquivo zip resultante: `backup.zip`
* nome do diretório temporário: `backup.f4d5.temp`

#### Fazendo backup em um Diretório de Públicos alvos não padrão {#backing-up-to-a-non-default-target-directory}

Normalmente, o arquivo/diretório de backup é criado no servidor na pasta pai da pasta que contém a pasta `crx-quickstart`.

Se quiser salvar seu backup (de qualquer uma das classificações) em um local diferente, você pode definir um caminho absoluto &quot;para o parâmetro `target` no comando `curl`.

Por exemplo, para gerar `backupJune.zip` no diretório `/Backups/2012`:

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=/Backups/2012/backupJune.zip"
```

>[!CAUTION]
>
>Ao usar um servidor de aplicativos diferente (como JBoss), o backup on-line pode não funcionar como esperado, pois o diretório do público alvo não é gravável. Nesse caso, entre em contato com o Suporte.

>[!NOTE]
>
>Um backup também pode ser acionado [usando os MBeans fornecidos por AEM](/help/sites-administering/jmx-console.md).

### Backup de Snapshot do Sistema de Arquivos {#filesystem-snapshot-backup}

O processo descrito aqui é especialmente adequado para grandes repositórios.

>[!NOTE]
>
>Se você quiser usar essa abordagem de backup, seu sistema deve oferecer suporte a snapshots do sistema de arquivos. Por exemplo, para Linux, isso significa que seus sistemas de arquivos devem ser colocados em um volume lógico.

1. Execute um instantâneo do AEM do sistema de arquivos implantado.

1. Monte o instantâneo do sistema de arquivos.
1. Execute um backup e desmonte o snapshot.

### Como o AEM Online Backup funciona {#how-aem-online-backup-works}

AEM Online Backup é composto de uma série de ações internas para garantir a integridade dos dados que estão sendo copiados em backup e dos arquivos de backup que estão sendo criados. Estes estão listados abaixo para os interessados.

O backup on-line usa o seguinte algoritmo:

1. Ao criar um arquivo zip, a primeira etapa é criar ou localizar o diretório do público alvo.

   * Se estiver fazendo backup em um arquivo zip, um diretório temporário será criado. O nome do diretório start com `backup.` e termina com `.temp`; por exemplo `backup.f4d3.temp`.
   * Se estiver fazendo backup em um diretório, o nome especificado no caminho do público alvo será usado. Um diretório existente pode ser usado, caso contrário, um novo diretório será criado.

      Um arquivo vazio chamado `backupInProgress.txt` é criado no diretório do público alvo quando o backup é start. Esse arquivo é excluído quando o backup é concluído.

1. Os arquivos são copiados do diretório de origem para o diretório do público alvo (ou diretório temporário ao criar um arquivo zip). O armazenamento de segmentos é copiado antes do armazenamento de dados para evitar danos no repositório. Os dados de índice e cache são omitidos ao criar o backup. Como resultado, os dados de `crx-quickstart/repository/cache` e `crx-quickstart/repository/index` não estão incluídos no backup. O indicador da barra de progresso do processo fica entre 0% - 70% ao criar um arquivo zip, ou 0% - 100% se nenhum arquivo zip for criado.

1. Se o backup estiver sendo feito em um diretório pré-existente, os arquivos &quot;antigos&quot; no diretório do público alvo serão excluídos. Arquivos antigos são arquivos que não existem no diretório de origem.

Os arquivos são copiados para o diretório do público alvo em quatro etapas:

1. Na primeira etapa da cópia (indicador de progresso 0% - 63% ao criar um arquivo zip ou 0% - 90% se nenhum arquivo zip for criado), todos os arquivos serão copiados enquanto o repositório estiver sendo executado normalmente. O processo tem duas fases:

   * Fase A - tudo é copiado, exceto o armazenamento de dados (com atraso).
   * Fase B - somente o armazenamento de dados é copiado (com atraso).

1. Na segunda fase de cópia (indicador de progresso 63% - 65,8% ao criar um arquivo zip ou 90% - 94% se nenhum arquivo zip for criado) apenas os arquivos que foram criados ou modificados no diretório de origem desde que a primeira fase de cópia foi iniciada serão copiados. Dependendo da atividade do repositório, isso pode variar de nenhum arquivo, até um número significativo de arquivos (porque o primeiro estágio de cópia de arquivo geralmente leva muito tempo). O processo de cópia é semelhante ao primeiro estágio (Fase A e Fase B com atraso).
1. Na terceira fase da cópia (indicador de progresso 65,8% - 68,6% ao criar um arquivo zip ou 94% - 98% se nenhum arquivo zip for criado) apenas os arquivos que foram criados ou modificados no diretório de origem desde que a segunda fase da cópia foi iniciada serão copiados. Dependendo da atividade do repositório, talvez não haja arquivos para copiar ou um número muito pequeno de arquivos (porque a segunda etapa de cópia de arquivo é, geralmente, rápida). O processo de cópia é semelhante à segunda fase - Fase A e Fase B, mas sem demora.
1. Os estágios de cópia de arquivo de um a três são todos feitos simultaneamente enquanto o repositório está em execução. Somente os arquivos que foram criados ou modificados no diretório de origem desde que a terceira fase de cópia foi iniciada são copiados. Dependendo da atividade do repositório, talvez não haja arquivos para copiar ou um número muito, muito pequeno de arquivos (porque a segunda etapa de cópia de arquivo normalmente é muito rápida). Indicador de progresso 68,6% - 70% ao criar um arquivo zip ou 98% - 100% se nenhum arquivo zip for criado. O processo de cópia é semelhante à terceira fase.
1. Dependendo do público alvo:

   * Se um arquivo zip tiver sido especificado, ele será criado a partir do diretório temporário. Indicador de progresso 70% - 100%. O diretório temporário é então excluído.
   * Se o público alvo for um diretório, o arquivo vazio chamado `backupInProgress.txt` será excluído para indicar que o backup foi concluído.

## Restaurando o Backup {#restoring-the-backup}

Você pode restaurar um backup da seguinte maneira:

* Caso tenha realizado um Backup de Instantâneo do Sistema de Arquivos, é possível restaurar uma imagem do sistema.
* Caso você tenha criado o backup como um arquivo zip, basta descompactar o conteúdo em uma nova pasta e AEM de start desse local.

## Backup do pacote {#package-backup}

Para fazer backup e restaurar o conteúdo, você pode usar um dos Gerenciador de pacotes, que usa o formato Pacote de conteúdo para fazer backup e restaurar o conteúdo. O Gerenciador de pacotes oferece mais flexibilidade na definição e gerenciamento de pacotes.

Para obter detalhes sobre os recursos e compensações de cada um desses formatos de pacote de conteúdo individual, consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md).

### Escopo do backup {#scope-of-backup}

Quando você faz backup dos nós usando o Gerenciador de pacotes ou o Editor de conteúdo, o CRX salva as seguintes informações:

* O conteúdo do repositório abaixo da árvore selecionada.
* As definições de tipo de nó usadas para o conteúdo do qual você faz backup.
* As definições de Namespace usadas para o conteúdo do backup.

Ao fazer o backup, AEM perde as seguintes informações:

* O histórico da versão.

