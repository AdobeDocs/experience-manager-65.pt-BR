---
title: Backup e restauração
description: Saiba como fazer backup e restaurar o conteúdo e as configurações do AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: dd26dade-b769-483e-bc11-dcfa5ed1f87e
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2314'
ht-degree: 0%

---

# Backup e restauração{#backup-and-restore}

Há duas maneiras de fazer backup e restaurar o conteúdo do repositório no AEM:

* Você pode criar um backup externo do repositório e armazená-lo em um local seguro. Se o repositório falhar, é possível restaurá-lo para o estado anterior.
* Você pode criar versões internas do conteúdo do repositório. Essas versões são armazenadas no repositório juntamente com o conteúdo, para que você possa restaurar rapidamente os nós e árvores alterados ou excluídos.

## Geral {#general}

A abordagem descrita aqui aplica-se ao backup e à recuperação do sistema.

Se você precisar fazer backup e/ou recuperar uma pequena quantidade de conteúdo perdido, a recuperação do sistema não será necessariamente necessária:

* Você pode buscar os dados de outro sistema por meio de um pacote
* Para restaurar o backup em um sistema temporário, crie um pacote de conteúdo e implante-o no sistema, onde esse conteúdo está ausente.

Para obter detalhes, consulte [Backup do pacote](/help/sites-administering/backup-and-restore.md#package-backup) abaixo.

## Horário {#timing}

Não execute o backup em paralelo com a coleta de lixo do armazenamento de dados, pois isso pode prejudicar os resultados de ambos os processos.

## Backup off-line {#offline-backup}

Você sempre pode fazer um backup off-line. Isso requer um tempo de inatividade do AEM, mas pode ser bastante eficiente em termos de tempo necessário em comparação a um backup on-line.

Na maioria dos casos, você usará um instantâneo do sistema de arquivos para criar uma cópia somente leitura do armazenamento naquele momento. Para criar um backup off-line, execute estas etapas:

* parar o aplicativo
* fazer um backup de instantâneo
* iniciar o aplicativo

Como o backup de snapshot geralmente leva apenas alguns segundos, todo o tempo de inatividade é de menos de alguns minutos.

## Backup on-line {#online-backup}

Esse método de backup cria um backup de todo o repositório, incluindo todos os aplicativos implantados nele, como AEM. O backup inclui conteúdo, histórico de versões, configuração, software, hotfixes, aplicativos personalizados, arquivos de registro, índices de pesquisa e assim por diante. Se você estiver usando clustering e se a pasta compartilhada for um subdiretório de `crx-quickstart` (fisicamente ou usando um softlink), também é feito backup do diretório compartilhado.

É possível restaurar todo o repositório (e qualquer aplicativo) posteriormente.

Esse método opera como um backup &quot;ativo&quot; ou &quot;on-line&quot; para que possa ser executado enquanto o repositório está em execução. Portanto, o repositório é utilizável enquanto o backup está em execução. Esse método funciona para as instâncias de repositório padrão baseadas em armazenamento Tar.

Ao criar um backup, você tem as seguintes opções:

* Backup em um diretório usando a ferramenta de backup integrada AEM.
* Fazendo backup em um diretório usando um instantâneo do sistema de arquivos

Em qualquer caso, o backup cria uma imagem (ou instantâneo) do repositório. Em seguida, o agente de backup de sistemas deve tomar cuidado para realmente transferir essa imagem para um sistema de backup dedicado (unidade de fita).

>[!NOTE]
>
>Se o recurso AEM Online Backup for usado em uma instância AEM que tenha uma configuração personalizada de armazenamento de blobs, é recomendável configurar o caminho do armazenamento de dados para ficar fora do &quot; `crx-quickstart`&quot; e faça backup do armazenamento de dados separadamente.

>[!CAUTION]
>
>O backup on-line faz backup apenas do sistema de arquivos. Se você armazenar o conteúdo do repositório e/ou os arquivos do repositório em um banco de dados, será necessário fazer backup desse banco de dados separadamente. Se estiver usando AEM com MongoDB, consulte a documentação sobre como usar o [Ferramentas de backup nativas do MongoDB](https://docs.mongodb.org/manual/tutorial/backup-with-mongodump/).

### Backup online do AEM {#aem-online-backup}

Um backup on-line do repositório permite criar, fazer download e excluir arquivos de backup. É um recurso de backup &quot;ativo&quot; ou &quot;on-line&quot;, portanto, pode ser executado enquanto o repositório está sendo usado normalmente no modo de leitura e gravação.

>[!CAUTION]
>
>Não execute o AEM Online Backup simultaneamente com [Coleta de lixo do armazenamento de dados](/help/sites-administering/data-store-garbage-collection.md) ou [Limpeza de revisão](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup). Isso afetará negativamente o desempenho do sistema.

Ao iniciar um backup, você pode especificar um **Caminho de destino** e/ou um **Atraso**.

**Caminho de destino** Normalmente, os arquivos de backup são salvos na pasta principal da pasta que contém o arquivo jar de início rápido (.jar). Por exemplo, se você tiver o arquivo jar do AEM localizado em /InstallationKits/AEM, o backup será gerado em /InstallationKits. Você também pode especificar um destino para um local de sua escolha.

Se a variável **TargetPath** for um diretório, a imagem do repositório será criada nesse diretório. Se o mesmo diretório for usado várias vezes (ou sempre) para armazenar o backup,

* os arquivos modificados no repositório são modificados adequadamente no TargetPath
* os arquivos excluídos no repositório são excluídos no TargetPath
* os arquivos criados no repositório são criados no TargetPath

>[!NOTE]
>
>Se **TargetPath** está definido como nome de arquivo com a extensão **.zip**, o backup do repositório é feito em um diretório temporário e, em seguida, o conteúdo desse diretório temporário é compactado e armazenado no arquivo ZIP.
>
>Esta abordagem é desencorajada, porque
>
>* ele requer armazenamento em disco adicional durante o processo de backup (diretório temporário mais o arquivo zip)
>* o processo de compactação é feito pelo repositório e pode influenciar seu desempenho.
>* Isso atrasa o processo de backup.
>* Até o Java 1.6, o Java só é capaz de criar arquivos ZIP de até 4 gigabytes.
>
>Se precisar criar um ZIP como formato de backup, você deve fazer backup em um diretório e usar um programa de compactação para criar o arquivo zip.

**Atraso** Indica um atraso (em milissegundos) para que o desempenho do repositório não seja afetado. Por padrão, o backup do repositório é executado em velocidade total. Você pode retardar a criação de um backup on-line, de modo que ele não retarde outras tarefas.

Ao usar um atraso muito grande, certifique-se de que o backup on-line não leve mais de 24 horas. Se tiver feito, descarte esse backup, pois pode não conter todos os binários.
Um atraso de 1 milissegundo normalmente resulta em 10% de uso da CPU, e um atraso de 10 milissegundos geralmente resulta em menos de 3% de uso da CPU. O atraso total em segundos pode ser estimado da seguinte forma: Tamanho do repositório em MB, multiplicado pelo atraso em milissegundos, dividido por 2 (se a opção zip for usada) ou dividido por 4 (ao fazer backup em um diretório). Isso significa que um backup em um diretório de um repositório de 200 MB com atraso de 1 ms aumenta o tempo de backup em cerca de 50 segundos.

>[!NOTE]
>
>Consulte [Como funciona o AEM Online Backup](#how-aem-online-backup-works) para obter detalhes internos do processo.

Para criar um backup:

1. Faça logon no AEM como administrador.

1. Ir para **Ferramentas - Operações - Backup.**
1. Clique em **Criar**. O console de backup se abre.

   ![chlimage_1-1](assets/chlimage_1-1a.png)

1. No console de backup, especifique o **[Caminho de destino](#aem-online-backup)** e **[Atraso](#aem-online-backup)**.

   ![chlimage_1-2](assets/chlimage_1-2a.png)

   >[!NOTE]
   >
   >O console de backup também está disponível usando:
   >
   >
   >` https://<*hostname*>:<*port-number*>/libs/granite/backup/content/admin.html`

1. Clique em **Salvar**, uma barra de andamento indicará o andamento do backup.

   >[!NOTE]
   >
   >Você pode **Cancelar** um backup em execução a qualquer momento.

1. Quando o backup estiver concluído, os arquivos zip serão listados na janela de backup.

   ![chlimage_1-3](assets/chlimage_1-3a.png)

   >[!NOTE]
   >
   >Os arquivos de backup que não são mais necessários podem ser removidos usando o console. Selecione o arquivo de backup no painel esquerdo e clique em **Excluir**.

   >[!NOTE]
   >
   >Se tiver feito backup em um diretório: após a conclusão do processo de backup, o AEM não gravará no diretório de destino.

### Automatização do backup on-line do AEM {#automating-aem-online-backup}

Se possível, o backup on-line deve ser executado quando houver pouca carga no sistema, por exemplo, de manhã.

Os backups podem ser automatizados usando o `wget` ou `curl` Clientes HTTP. Veja a seguir exemplos de como automatizar o backup usando curl.

#### Backup no diretório de destino padrão {#backing-up-to-the-default-target-directory}

>[!CAUTION]
>
>No exemplo a seguir, vários parâmetros na variável `curl` pode precisar ser configurado para sua instância; por exemplo, o nome do host ( `localhost`), porta ( `4502`), senha do administrador ( `xyz`) e nome do arquivo ( `backup.zip`).

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=backup.zip
```

O arquivo/diretório de backup é criado no servidor na pasta pai da pasta que contém o `crx-quickstart` pasta (igual ao que ocorreria se você estivesse criando o backup usando o navegador). Por exemplo, se você instalou o AEM no diretório `/InstallationKits/crx-quickstart/`, o backup será criado na variável `/InstallationKits` diretório.

O comando curl retorna imediatamente; portanto, é necessário monitorar esse diretório para ver quando o arquivo zip está pronto. Enquanto o backup está sendo criado, um diretório temporário (com o nome baseado no do arquivo zip final) pode ser visto, no final, ele será compactado. Por exemplo:

* nome do arquivo zip resultante: `backup.zip`
* nome do diretório temporário: `backup.f4d5.temp`

#### Backup em um Diretório de Destino não padrão {#backing-up-to-a-non-default-target-directory}

Normalmente, o arquivo/diretório de backup é criado no servidor na pasta principal da pasta que contém o `crx-quickstart` pasta.

Se quiser salvar seu backup (de qualquer tipo) em um local diferente, você pode definir um caminho absoluto &quot;para o `target` parâmetro no `curl` comando.

Por exemplo, para gerar `backupJune.zip` no diretório `/Backups/2012`:

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=/Backups/2012/backupJune.zip"
```

>[!CAUTION]
>
>Ao usar um servidor de aplicativos diferente (como JBoss), o backup on-line pode não funcionar conforme o esperado, pois o diretório de destino não é gravável. Nesse caso, entre em contato com o Suporte.

>[!NOTE]
>
>Um backup também pode ser acionado [usando os MBeans fornecidos pelo AEM](/help/sites-administering/jmx-console.md).

### Backup de snapshot do sistema de arquivos {#filesystem-snapshot-backup}

O processo descrito aqui é especialmente adequado para repositórios grandes.

>[!NOTE]
>
>Se você quiser usar essa abordagem de backup, o sistema deverá oferecer suporte a snapshots do sistema de arquivos. Por exemplo, para Linux, isso significa que os sistemas de arquivos devem ser colocados em um volume lógico.

1. Fazer um instantâneo do AEM do sistema de arquivos no qual ele está implantado.

1. Monte o instantâneo do sistema de arquivos.
1. Faça um backup e desmonte o snapshot.

### Como funciona o AEM Online Backup {#how-aem-online-backup-works}

O AEM Online Backup é composto de uma série de ações internas para garantir a integridade dos dados dos quais está sendo feito backup e dos arquivos de backup que estão sendo criados. Eles estão listados abaixo para os interessados.

O backup on-line utiliza o seguinte algoritmo:

1. Ao criar um arquivo zip, a primeira etapa é criar ou localizar o diretório de destino.

   * Se estiver fazendo backup em um arquivo zip, um diretório temporário será criado. O nome do diretório começa com `backup.` e termina com `.temp`; por exemplo, `backup.f4d3.temp`.
   * Se estiver fazendo backup em um diretório, o nome especificado no caminho de destino será usado. Um diretório existente pode ser usado, caso contrário, um novo diretório será criado.

     Um arquivo vazio chamado `backupInProgress.txt` é criado no diretório de destino quando o backup é iniciado. Este arquivo é excluído quando o backup é concluído.

1. Os arquivos são copiados do diretório de origem para o diretório de destino (ou diretório temporário ao criar um arquivo zip). O armazenamento de segmentos é copiado antes do armazenamento de dados para evitar a corrupção do repositório. Os dados de índice e cache são omitidos ao criar o backup. Como resultado, dados de `crx-quickstart/repository/cache` e `crx-quickstart/repository/index` não está incluído no backup. O indicador da barra de progresso do processo está entre 0% e 70% ao criar um arquivo zip, ou 0% e 100% se nenhum arquivo zip for criado.

1. Se o backup estiver sendo feito em um diretório pré-existente, os arquivos &quot;antigos&quot; no diretório de destino serão excluídos. Arquivos antigos são arquivos que não existem no diretório de origem.

Os arquivos são copiados para o diretório de destino em quatro estágios:

1. Na primeira etapa de cópia (indicador de progresso 0% - 63% ao criar um arquivo zip ou 0% - 90% se nenhum arquivo zip for criado), todos os arquivos são copiados enquanto o repositório está em execução normalmente. O processo tem duas fases:

   * Fase A - tudo é copiado, exceto o armazenamento de dados (com atraso).
   * Fase B — somente o armazenamento de dados é copiado (com atraso).

1. No segundo estágio de cópia (indicador de progresso 63% - 65,8% ao criar um arquivo zip ou 90% - 94% se nenhum arquivo zip for criado), somente os arquivos que foram criados ou modificados no diretório de origem desde que o primeiro estágio de cópia foi iniciado são copiados. Dependendo da atividade do repositório, pode variar de nenhum arquivo até um número significativo de arquivos (porque o primeiro estágio de cópia de arquivo geralmente leva mais tempo). O processo de cópia é semelhante ao primeiro estágio (Fases A e B com atraso).
1. Na terceira etapa de cópia (indicador de andamento 65,8% - 68,6% ao criar um arquivo zip ou 94% - 98% se nenhum arquivo zip for criado), somente os arquivos criados ou modificados no diretório de origem desde que a segunda etapa de cópia foi iniciada são copiados. Dependendo da atividade do repositório, pode não haver arquivos a serem copiados ou um número muito pequeno de arquivos (porque o segundo estágio de cópia de arquivo geralmente é rápido). O processo de cópia é semelhante ao segundo estágio - Fase A e Fase B, mas sem demora.
1. Os estágios de cópia de arquivo, de um a três, são todos feitos simultaneamente enquanto o repositório está em execução. Somente os arquivos que foram criados ou modificados no diretório de origem desde o início do terceiro estágio de cópia são copiados. Dependendo da atividade do repositório, pode não haver arquivos para copiar ou um número muito, muito pequeno de arquivos (porque o segundo estágio de cópia de arquivos geralmente é muito rápido). Indicador de progresso 68,6% - 70% ao criar um arquivo zip ou 98% - 100% se nenhum arquivo zip for criado. O processo de cópia é semelhante ao terceiro estágio.
1. Dependendo do público alvo:

   * Se um arquivo zip foi especificado, ele agora é criado a partir do diretório temporário. Indicador de progresso 70% - 100%. O diretório temporário é então excluído.
   * Se o destino era um diretório, o arquivo vazio chamado `backupInProgress.txt` é excluído para indicar que o backup foi concluído.

## Restaurando o backup {#restoring-the-backup}

Você pode restaurar um backup da seguinte maneira:

* Caso tenha executado um backup de snapshot do sistema de arquivos, você pode simplesmente restaurar uma imagem do sistema.
* Caso tenha criado o backup como um arquivo zip, basta descompactar o conteúdo em uma nova pasta e iniciar o AEM nesse local.

## Backup do pacote {#package-backup}

Para fazer backup e restaurar conteúdo, você pode usar um dos gerenciadores de pacotes, que usa o formato do pacote de conteúdo para fazer backup e restaurar conteúdo. O Gerenciador de pacotes oferece mais flexibilidade ao definir e gerenciar pacotes.

Para obter detalhes sobre os recursos e as compensações de cada um desses formatos de pacote de conteúdo individual, consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md).

### Escopo do backup {#scope-of-backup}

Quando você faz backup de nós usando o Gerenciador de pacotes ou o Zipper de conteúdo, o CRX salva as seguintes informações:

* O conteúdo do repositório abaixo da árvore selecionada.
* As definições de tipo de Nó que são usadas para o conteúdo do qual você faz backup.
* As definições de namespace que são usadas para o conteúdo do qual você faz backup.

Durante o backup, o AEM perde as seguintes informações:

* O histórico de versões.
