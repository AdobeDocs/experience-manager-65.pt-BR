---
title: Estratégia para backup e restauração em um ambiente agrupado
seo-title: Estratégia para backup e restauração em um ambiente agrupado
description: Se a implementação de formulários do AEM armazenar dados personalizados adicionais em um banco de dados diferente, será necessário implementar uma estratégia para fazer backup desses dados, garantindo que eles permaneçam sincronizados com os dados de formulários do AEM.
seo-description: Se a implementação de formulários do AEM armazenar dados personalizados adicionais em um banco de dados diferente, será necessário implementar uma estratégia para fazer backup desses dados, garantindo que eles permaneçam sincronizados com os dados de formulários do AEM.
uuid: c29b989c-30ed-4a8e-bab8-9b7746291a33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c332985b-4556-4056-961a-fce2356da88d
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 0%

---


# Estratégia para backup e restauração em um ambiente agrupado {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>Se a implementação de formulários do AEM armazenar dados personalizados adicionais em um banco de dados diferente, será necessário implementar uma estratégia para fazer backup desses dados, garantindo que eles permaneçam sincronizados com os dados de formulários do AEM. Além disso, o aplicativo deve ser projetado de modo que seja robusto o suficiente para lidar com um cenário em que os bancos de dados adicionais fiquem fora de sincronia. É altamente recomendável que qualquer operação de banco de dados executada seja feita no contexto de uma transação para ajudar a manter um estado consistente.

É necessário fazer backup das seguintes partes do sistema de formulários do AEM para recuperar-se de qualquer erro:

* Banco de dados usado por formulários do AEM
* GDS com dados de longa duração e outros documentos persistentes
* Banco de dados AEM (crx-repository)

>[!NOTE]
>
>É necessário fazer backup de todos os outros dados que estão sendo usados pela configuração de formulários do AEM, como fontes do cliente, dados do conector e assim por diante.

## Faça backup de um ambiente agrupado {#back-up-a-clustered-environment}

Este tópico discute as seguintes estratégias para fazer backup de qualquer ambiente agrupado de formulários AEM:

* Backup offline com tempo de inatividade
* Backup offline sem tempo de inatividade (backup de um nó secundário que é desligado)
* Backup on-line sem tempo de inatividade, mas atraso na resposta
* Fazer backup do arquivo de propriedades do Bootstrap

### Backup offline com tempo de inatividade {#offline-backup-with-downtime}

1. Encerre todo o cluster e os serviços relacionados. (consulte [Iniciar e parar serviços](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Em qualquer nó, faça backup do banco de dados, GDS e Conectores. (consulte [Arquivos para backup e recuperação](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Execute as seguintes etapas para fazer backup do repositório do AEM off-line:

   1. Para cada nó de cluster, faça backup do arquivo que contém a id do nó de cluster.
   1. Faça backup de todos os arquivos de qualquer nó de cluster secundário, incluindo subdiretórios.
   1. Faça backup do repositório/ID do sistema de cada nó de cluster separadamente.

   Para obter etapas detalhadas, consulte [Backup e restauração](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

1. Faça backup de quaisquer outros dados, como fontes do cliente.
1. Start o cluster novamente.

### Backup offline sem tempo de inatividade {#offline-backup-with-no-downtime}

1. Insira o modo de backup em andamento. (consulte [Entrando nos modos](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes)de backup)

   Observe que precisamos sair do modo de backup em andamento após uma recuperação.

1. Desative qualquer um dos nós secundários do cluster em relação ao AEM. (consulte [Iniciar e parar serviços](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Em qualquer nó, faça backup do banco de dados, GDS e Conectores. (consulte [Arquivos para backup e recuperação](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Execute as seguintes etapas para fazer backup do repositório do AEM off-line:

   1. Para cada nó de cluster, faça backup do arquivo que contém a id do nó de cluster.
   1. Faça backup de todos os arquivos de qualquer nó de cluster secundário, incluindo subdiretórios.
   1. Faça backup repository/system.id de cada nó de cluster separadamente.

   Para obter etapas detalhadas, consulte [Backup e restauração](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

1. Faça backup de quaisquer outros dados, como fontes do cliente.
1. Start o cluster novamente.

### Backup on-line sem tempo de inatividade, mas atraso na resposta {#online-backup-with-no-downtime-but-delay-in-response}

1. Insira o modo de backup em andamento. (consulte [Entrando nos modos](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes)de backup)

   Observe que é necessário sair do modo de backup em andamento após uma recuperação.

1. Desative qualquer um dos nós secundários do cluster em relação ao AEM. (consulte [Iniciar e parar serviços](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Em qualquer nó, faça backup do banco de dados, GDS e Conectores. (consulte [Arquivos para backup e recuperação](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Execute as seguintes etapas para fazer backup do repositório do AEM on-line:

   1. Para cada nó de cluster, faça backup do arquivo que contém o cluster_node.id.
   1. Faça backup repository/system.id de cada nó de cluster separadamente.
   1. Em qualquer nó secundário, faça um backup on-line do repositório para obter etapas detalhadas, consulte Backup on-line.

1. Faça backup de quaisquer outros dados, como fontes do cliente.
1. Start o cluster novamente.

### Fazer backup do arquivo de propriedades do Bootstrap {#back-up-the-bootstrap-properties-file}

Quando criamos um cluster AEM, um arquivo de propriedades é criado no servidor de aplicativos para todos os nós secundários. É recomendável fazer backup do arquivo de propriedades do Bootstrap. Você pode encontrar o arquivo no seguinte local no servidor de aplicativos:

* JBoss: no diretório BIN
* WebLogic: no diretório de domínio
* WebSphere: no diretório do perfil

É necessário fazer backup do arquivo para o cenário de recuperação de desastres do nó secundário do AEM e substituí-lo no local especificado no servidor de aplicativos, se restaurado.

## Recuperação em um ambiente clusterizado {#recovery-in-a-clustered-environment}

Em caso de falha de todo o cluster ou de um único nó, é necessário restaurá-lo usando o backup.

Para uma recuperação de nó único, basta encerrar o nó único e executar o procedimento de recuperação de nó único.

Se o cluster inteiro falhar devido a falhas como falhas no banco de dados, é necessário executar as seguintes etapas. A restauração depende do método de backup usado.

### Restaurar um único nó {#restoring-a-single-node}

1. Pare o nó corrompido.

   >[!NOTE]
   >
   >Se o nó corrompido for um nó primário AEM, desligue o nó de cluster inteiro.

1. Recrie o sistema físico a partir de uma imagem do sistema.
1. Aplique patches ou atualizações a formulários AEM que foram aplicados desde que a imagem foi feita. Essas informações foram registradas durante o procedimento de backup. Os formulários AEM devem ser recuperados no mesmo nível de correção que no momento em que o sistema foi feito o backup.
1. (*Opcional*) Se todos os outros nós estiverem funcionando bem, é possível que o repositório do AEM também esteja corrompido. Nesse caso, você verá uma mensagem de não sincronização do repositório no arquivo error.log do repositório do AEM.

   Para restaurar o repositório, execute as seguintes etapas.

   >[!NOTE]
   >
   >Se um backup compactado do repositório crx foi colocado on-line, descompacte-o em qualquer local e siga o processo de restauração off-line.

   1. Exclua os diretórios de repositório, compartilhado, versão e espaços de trabalho no diretório clusterNode do nó.
   1. Restaure o backup do nó de cluster (incluindo subdiretórios) para o nó.
   1. Exclua o arquivo clusterNode/revision.log no nó.
   1. Exclua o .lock no nó, se houver.
   1. Exclua o diretório repository/system.id no nó, se houver.
   1. Exclua os arquivos &amp;ast;&amp;ast;/listener.properties no nó, se houver.
   1. Restaure repository/cluster_node.id para nós de cluster individuais.

>[!NOTE]
>
>Considere os seguintes pontos:

* Se o nó com falha for um nó primário do AEM, copie todo o conteúdo da pasta do repositório secundário (crx-repository\crx.0000, onde 0000 pode ser qualquer dígito) para a pasta do repositório crx-repository\ e exclua a pasta do repositório secundário.
* Antes de reiniciar qualquer nó de cluster, certifique-se de excluir o repositório /clustered.txt do nó primário.
* Certifique-se de que o nó primário seja iniciado primeiro e depois de completamente ativado, start outros nós.

### Restaurar todo o cluster {#restoring-the-entire-cluster}

1. Pare todos os nós do cluster.
1. Recrie o sistema físico a partir de uma imagem do sistema.
1. Aplique patches ou atualizações a formulários AEM que foram aplicados desde que a imagem foi feita. Essas informações foram registradas na etapa 1 do procedimento de backup. Os formulários AEM devem ser recuperados no mesmo nível de correção que no momento em que o sistema foi feito o backup.
1. Restaure o banco de dados, GDS e Conectores.
1. Faça o seguinte para recuperar o repositório do AEM off-line:

   >[!NOTE]
   >
   >Se um backup compactado do repositório crx foi colocado on-line, descompacte-o em qualquer local e siga o processo de restauração off-line.

   1. Em todos os nós de cluster, exclua os diretórios de repositório, compartilhado, versão e espaços de trabalho no diretório clusterNode.
   1. Exclua todos os arquivos e diretórios no diretório compartilhado.
   1. Restaure o backup do nó de cluster (incluindo subdiretórios) para um nó de cluster.
   1. Copie todos os arquivos do nó de cluster restaurado para todos os outros nós de cluster. Depois de concluído, cada nó de cluster contém os mesmos dados.
   1. Exclua o arquivo clusterNode/revision.log em todos os nós de cluster.
   1. Exclua o .lock em todos os nós do cluster, se houver.
   1. Exclua repository/system.id todos os nós de cluster, se houver.
   1. Exclua os arquivos &amp;ast;&amp;ast;/listener.properties em todos os nós de cluster, se houver.
   1. Restaure repository/cluster_node.id para nós de cluster individuais.

>[!NOTE]
>
>Considere os seguintes pontos:

* Se o nó com falha for um nó primário do AEM, copie todo o conteúdo da pasta do repositório secundário (parece crx-repository\crx.0000, onde 0000 pode ser qualquer dígito) para a pasta do repositório crx-repository\.
* Antes de reiniciar qualquer nó de cluster, certifique-se de excluir o repositório /clustered.txt do nó primário.
* Certifique-se de que o nó primário seja iniciado primeiro e depois de completamente ativado, start outros nós.

## Fazer backup e restaurar o nó de publicação da Solução de gerenciamento de correspondência {#back-up-and-restore-correspondence-management-solution-publish-node}

O nó do editor não tem nenhuma relação primário-secundário em um ambiente clusterizado. Você pode fazer backup de qualquer nó do Publisher seguindo o [Backup e a Restauração](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

### Recuperar um único nó do editor {#recover-a-single-publisher-node}

1. Desligue o nó que precisa ser recuperado e não faça nenhuma atividade de publicação até que o nó esteja ativo novamente.
1. Restaure o nó Publicar usando [Restaurar o Backup](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring o Backup).

### Recuperar um cluster {#recover-a-cluster}

1. Desligue o cluster.
1. Restaure o nó Publicar usando [Restaurar o Backup](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring o Backup).
1. Start o nó primário seguido pelo nó secundário do cluster do autor.

