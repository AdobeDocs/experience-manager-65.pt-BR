---
title: Estratégia para backup e restauração em um ambiente em cluster
seo-title: Strategy for backup and restore in a clustered environment
description: Se a implementação do AEM forms armazenar dados personalizados adicionais em um banco de dados diferente, será necessário implementar uma estratégia para fazer backup desses dados, garantindo que eles permaneçam sincronizados com os dados AEM forms.
seo-description: If your AEM forms implementation stores additional custom data in a different database, you must implement a strategy to back up this data ensuring that it remains in sync with the AEM forms data.
uuid: c29b989c-30ed-4a8e-bab8-9b7746291a33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c332985b-4556-4056-961a-fce2356da88d
exl-id: 98c96349-f253-475f-b646-352269814a38
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 0%

---

# Estratégia para backup e restauração em um ambiente em cluster {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>Se a implementação do AEM forms armazenar dados personalizados adicionais em um banco de dados diferente, será necessário implementar uma estratégia para fazer backup desses dados, garantindo que eles permaneçam sincronizados com os dados AEM forms. Além disso, o aplicativo deve ser projetado de forma que seja robusto o suficiente para lidar com um cenário em que os bancos de dados adicionais fiquem fora de sincronia. É altamente recomendável que qualquer operação de banco de dados executada seja feita no contexto de uma transação para ajudar a manter um estado consistente.

Você precisa fazer o backup das seguintes partes do sistema de formulários AEM para recuperar qualquer erro:

* Banco de dados usado por formulários AEM
* GDS que tem dados de longa duração e outros documentos persistentes
* Banco de dados AEM (crx-repository)

>[!NOTE]
>
>É necessário fazer backup de todos os outros dados que estão sendo usados pela configuração de formulários AEM, como fontes de clientes, dados de conectores e assim por diante.

## Faça backup de um ambiente em cluster {#back-up-a-clustered-environment}

Este tópico discute as seguintes estratégias para fazer backup de qualquer ambiente em cluster de formulários AEM:

* Backup offline com tempo de inatividade
* Backup offline sem tempo de inatividade (backup de um nó secundário que está desligado)
* Backup on-line sem tempo de inatividade, mas com atraso na resposta
* Faça o backup do arquivo de propriedades do Bootstrap

### Backup offline com tempo de inatividade {#offline-backup-with-downtime}

1. Encerre todo o cluster e serviços relacionados. (consulte [Iniciar e parar serviços](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Em qualquer nó, faça backup do banco de dados, GDS e Connectors. (consulte [Arquivos para backup e recuperação](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Execute as seguintes etapas para fazer backup AEM repositório offline:

   1. Para cada nó do cluster, faça backup do arquivo que contém o ID do nó do cluster.
   1. Faça backup de todos os arquivos de qualquer nó do cluster secundário, incluindo subdiretórios.
   1. Faça backup do repositório/ID do sistema de cada nó do cluster separadamente.

   Para obter etapas detalhadas, consulte [Backup e restauração](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

1. Faça o backup de quaisquer outros dados, como fontes do cliente.
1. Inicie o cluster novamente.

### Backup offline sem tempo de inatividade {#offline-backup-with-no-downtime}

1. Entre no modo de backup em andamento. (consulte [Inserir os modos de backup](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Observe que precisamos sair do modo de backup contínuo após uma recuperação.

1. Desligue qualquer um dos nós secundários do cluster em relação ao AEM. (consulte [Iniciar e parar serviços](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Em qualquer nó, faça backup do banco de dados, GDS e Connectors. (consulte [Arquivos para backup e recuperação](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Execute as seguintes etapas para fazer backup AEM repositório offline:

   1. Para cada nó do cluster, faça backup do arquivo que contém o ID do nó do cluster.
   1. Faça backup de todos os arquivos de qualquer nó do cluster secundário, incluindo subdiretórios.
   1. Faça backup repository/system.id de cada nó do cluster separadamente.

   Para obter etapas detalhadas, consulte [Backup e restauração](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

1. Faça o backup de quaisquer outros dados, como fontes do cliente.
1. Inicie o cluster novamente.

### Backup on-line sem tempo de inatividade, mas com atraso na resposta {#online-backup-with-no-downtime-but-delay-in-response}

1. Entre no modo de backup em andamento. (consulte [Inserir os modos de backup](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Observe que é necessário deixar o modo de backup contínuo após uma recuperação.

1. Desligue qualquer um dos nós secundários do cluster em relação ao AEM. (consulte [Iniciar e parar serviços](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Em qualquer nó, faça backup do banco de dados, GDS e Connectors. (consulte [Arquivos para backup e recuperação](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Execute as seguintes etapas para fazer backup AEM repositório online:

   1. Para cada nó do cluster, faça backup do arquivo que contém o cluster_node.id.
   1. Faça backup repository/system.id de cada nó do cluster separadamente.
   1. Em qualquer nó secundário, faça um backup on-line do repositório para obter etapas detalhadas, consulte Backup on-line.

1. Faça o backup de quaisquer outros dados, como fontes do cliente.
1. Inicie o cluster novamente.

### Faça o backup do arquivo de propriedades do Bootstrap {#back-up-the-bootstrap-properties-file}

Quando criamos um cluster AEM, um arquivo de propriedades é criado no servidor de aplicativos para todos os nós secundários. É recomendável fazer o backup do arquivo de propriedades do Bootstrap. Você pode encontrar o arquivo no seguinte local no servidor de aplicativos:

* JBoss: no diretório BIN
* WebLogic: no diretório de domínio
* WebSphere: no diretório do perfil

Você precisa fazer o backup do arquivo para o cenário de recuperação de desastres AEM nó secundário e substituí-lo no local especificado no servidor de aplicativos, se restaurado.

## Recuperação em um ambiente em cluster {#recovery-in-a-clustered-environment}

Em caso de falha de todo o cluster ou de um único nó, é necessário restaurá-lo usando o backup.

Para uma recuperação de nó único, basta encerrar o nó único e executar o procedimento de recuperação de nó único.

Caso todo o cluster falhe devido a falhas como falha do banco de dados, é necessário executar as seguintes etapas. A restauração depende do método de backup usado.

### Restaurar um único nó {#restoring-a-single-node}

1. Pare o nó corrompido.

   >[!NOTE]
   >
   >Se o nó corrompido for um nó primário AEM, encerre todo o nó do cluster.

1. Recrie o sistema físico a partir de uma imagem do sistema.
1. Aplique patches ou atualizações AEM formulários que foram aplicados desde que a imagem foi feita. Essas informações foram registradas durante o procedimento de backup. Os formulários AEM devem ser recuperados no mesmo nível de patch que quando o backup do sistema foi feito.
1. (*Opcional*) Se todos os outros nós estiverem funcionando bem, é possível que o repositório de AEM também esteja corrompido. Nesse caso, você verá uma mensagem de cancelamento de sincronização do repositório no arquivo error.log do repositório AEM.

   Para restaurar o repositório, execute as seguintes etapas.

   >[!NOTE]
   >
   >Se um backup compactado crx-repository foi colocado online, descompacte-o em qualquer local e siga o processo de restauração offline.

   1. Exclua os diretórios de repositório, compartilhados, versão e espaços de trabalho no diretório clusterNode do nó .
   1. Restaure o backup do nó do cluster (incluindo subdiretórios) para o nó .
   1. Exclua o arquivo clusterNode/revision.log no nó .
   1. Exclua o .lock no nó , se existir.
   1. Exclua o repository/system.id no nó , se existir.
   1. Exclua os arquivos &amp;ast;&amp;ast;/listener.properties no nó, se existir.
   1. Restaure repository/cluster_node.id para nós de cluster individuais.

>[!NOTE]
>
>Considere os seguintes pontos:

* Se o nó com falha foi um nó primário AEM, copie todo o conteúdo da pasta do repositório secundário (crx-repository\crx.0000 onde 0000 pode ser qualquer dígito) para a pasta crx-repository\ repository e exclua a pasta do repositório secundário.
* Antes de reiniciar qualquer nó do cluster, certifique-se de excluir o repositório /clustered.txt do nó principal.
* Certifique-se de que o nó principal seja iniciado primeiro e, uma vez completamente ativado, inicie outros nós.

### Restaurar todo o cluster {#restoring-the-entire-cluster}

1. Pare todos os nós do cluster.
1. Recrie o sistema físico a partir de uma imagem do sistema.
1. Aplique patches ou atualizações AEM formulários do AEM que foram aplicados desde que a imagem foi feita. Essas informações foram registradas na etapa 1 do procedimento de backup. Os formulários AEM devem ser recuperados no mesmo nível de patch que quando o backup do sistema foi feito.
1. Restaure o banco de dados, GDS e Connectors.
1. Faça o seguinte para recuperar o repositório AEM offline:

   >[!NOTE]
   >
   >Se um backup compactado crx-repository foi colocado online, descompacte-o em qualquer local e siga o processo de restauração offline.

   1. Em todos os nós do cluster, exclua os diretórios de repositório, compartilhado, versão e espaços de trabalho no diretório clusterNode .
   1. Exclua todos os arquivos e diretórios no diretório compartilhado.
   1. Restaure o backup do nó do cluster (incluindo subdiretórios) para um nó do cluster.
   1. Copie todos os arquivos do nó do cluster restaurado para todos os outros nós do cluster. Depois de concluído, cada nó do cluster contém os mesmos dados.
   1. Exclua o arquivo clusterNode/revision.log em todos os nós do cluster.
   1. Exclua o .lock em todos os nós do cluster, se existir.
   1. Exclua o repository/system.id todos os nós do cluster, se existir.
   1. Exclua os arquivos &amp;ast;&amp;ast;/listener.properties em todos os nós do cluster, se existirem.
   1. Restaure repository/cluster_node.id para nós de cluster individuais.

>[!NOTE]
>
>Considere os seguintes pontos:

* Se o nó com falha foi um nó primário AEM, copie todo o conteúdo da pasta do repositório secundário (parece crx-repository\crx.0000, onde 0000 pode ser qualquer dígito) para a pasta crx-repository\ repository.
* Antes de reiniciar qualquer nó do cluster, certifique-se de excluir o repositório /clustered.txt do nó principal.
* Certifique-se de que o nó principal seja iniciado primeiro e, uma vez completamente ativado, inicie outros nós.

## Fazer backup e restaurar o nó de publicação da Solução de gerenciamento de correspondência {#back-up-and-restore-correspondence-management-solution-publish-node}

O nó do editor não tem nenhuma relação primária-secundária em um ambiente em cluster. Você pode fazer backup de qualquer nó do Editor seguindo [Backup e restauração](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

### Recuperar um único nó do editor {#recover-a-single-publisher-node}

1. Desligue o nó que precisa ser recuperado e não faça nenhuma atividade de publicação até que o nó esteja ativo novamente.
1. Restaure o nó Publicar usando [Restaurar o Backup](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring o backup).

### Recuperar um cluster {#recover-a-cluster}

1. Desligue o cluster.
1. Restaure o nó Publicar usando [Restaurar o Backup](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring o backup).
1. Inicie o nó principal seguido pelo nó secundário do cluster de criação.
