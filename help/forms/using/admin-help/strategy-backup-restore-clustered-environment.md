---
title: Estratégia de backup e restauração em um ambiente em cluster
description: Se a implementação do AEM Forms armazenar dados personalizados adicionais em um banco de dados diferente, você deverá implementar uma estratégia para fazer backup desses dados, garantindo que eles permaneçam sincronizados com os dados do AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 98c96349-f253-475f-b646-352269814a38
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1396'
ht-degree: 0%

---

# Estratégia de backup e restauração em um ambiente em cluster {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>Se a implementação do AEM Forms armazenar dados personalizados adicionais em um banco de dados diferente, você deverá implementar uma estratégia para fazer backup desses dados, garantindo que eles permaneçam sincronizados com os dados do AEM Forms. Além disso, o aplicativo deve ser projetado de modo que seja robusto o suficiente para lidar com um cenário em que os bancos de dados adicionais fiquem fora de sincronia. É altamente recomendável que qualquer operação de banco de dados executada seja feita no contexto de uma transação para ajudar a manter um estado consistente.

Você precisa fazer backup das seguintes partes do sistema de formulários AEM para se recuperar de qualquer erro:

* Banco de dados usado por formulários AEM
* GDS com dados de longa vida e outros documentos persistentes
* Banco de dados AEM (crx-repository)

>[!NOTE]
>
>Você precisa fazer backup de quaisquer outros dados que estejam sendo usados pela configuração do AEM Forms, como fontes do cliente, dados de conectores e assim por diante.

## Fazer backup de um ambiente em cluster {#back-up-a-clustered-environment}

Este tópico discute as seguintes estratégias para fazer backup de qualquer ambiente em cluster de formulários AEM:

* Backup off-line com tempo de inatividade
* Backup off-line sem tempo de inatividade (backup de um nó secundário que está desligado)
* Backup on-line sem tempo de inatividade, mas com atraso na resposta
* Faça backup do arquivo de propriedades do Bootstrap

### Backup off-line com tempo de inatividade {#offline-backup-with-downtime}

1. Desligue todo o cluster e os serviços relacionados. (consulte [Iniciar e parar serviços](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Em qualquer nó, faça backup do banco de dados, do GDS e dos Conectores. (consulte [Arquivos para backup e recuperação](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Para fazer backup do repositório AEM off-line, execute as seguintes etapas:

   1. Para cada nó de cluster, faça backup do arquivo que contém a ID do nó de cluster.
   1. Faça backup de todos os arquivos de qualquer nó de cluster secundário, incluindo subdiretórios.
   1. Faça backup do repositório/ID do sistema de cada nó de cluster separadamente.

   Para obter etapas detalhadas, consulte [Backup e restauração](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. Faça backup de todos os outros dados, como fontes de clientes.
1. Inicie o cluster novamente.

### Backup off-line sem tempo de inatividade {#offline-backup-with-no-downtime}

1. Entre no modo de backup contínuo. (consulte [Entrando nos modos de backup](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Sair do modo de backup contínuo após uma recuperação.

1. Desligue qualquer um dos nós secundários do cluster em relação ao AEM. (consulte [Iniciar e parar serviços](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Em qualquer nó, faça backup do banco de dados, do GDS e dos Conectores. (consulte [Arquivos para backup e recuperação](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Para fazer backup do repositório AEM off-line, execute as seguintes etapas:

   1. Para cada nó de cluster, faça backup do arquivo que contém a ID do nó de cluster.
   1. Faça backup de todos os arquivos de qualquer nó de cluster secundário, incluindo subdiretórios.
   1. Faça backup do repository/system.id de cada nó de cluster separadamente.

   Para obter etapas detalhadas, consulte [Backup e restauração](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. Faça backup de todos os outros dados, como fontes de clientes.
1. Inicie o cluster novamente.

### Backup on-line sem tempo de inatividade, mas com atraso na resposta {#online-backup-with-no-downtime-but-delay-in-response}

1. Entre no modo de backup contínuo. (consulte [Entrando nos modos de backup](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Sair do modo de backup contínuo após uma recuperação.

1. Desligue qualquer um dos nós secundários do cluster em relação ao AEM. (consulte [Iniciar e parar serviços](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Em qualquer nó, faça backup do banco de dados, do GDS e dos Conectores. (consulte [Arquivos para backup e recuperação](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Para fazer backup do repositório AEM on-line, execute as seguintes etapas:

   1. Para cada nó de cluster, faça backup do arquivo que contém o cluster_node.id.
   1. Faça backup do repository/system.id de cada nó de cluster separadamente.
   1. Em qualquer nó secundário, faça um backup on-line do repositório. Para obter etapas detalhadas, consulte Backup on-line.

1. Faça backup de todos os outros dados, como fontes de clientes.
1. Inicie o cluster novamente.

### Faça backup do arquivo de propriedades do Bootstrap {#back-up-the-bootstrap-properties-file}

Quando criamos um cluster AEM, um arquivo de propriedades é criado no servidor de aplicativos para todos os nós secundários. É recomendável fazer backup do arquivo de propriedades do Bootstrap. Você pode encontrar o arquivo no seguinte local no servidor de aplicativos:

* JBoss®: no diretório BIN
* WebLogic: no diretório de domínio
* WebSphere®: no diretório do perfil

Faça backup do arquivo para o cenário de recuperação de desastres do nó secundário AEM e substitua-o no local especificado no servidor de aplicativos, se restaurado.

## Recuperação em um ambiente em cluster {#recovery-in-a-clustered-environment}

Se houver qualquer falha do cluster inteiro ou de um único nó, restaure-o usando o backup.

Para uma recuperação de um único nó, desative o único nó e execute o procedimento de recuperação de um único nó.

Caso todo o cluster falhe devido a falhas como falha no banco de dados, execute as etapas a seguir. A restauração depende do método de backup usado.

### Restauração de um único nó {#restoring-a-single-node}

1. Interrompa o nó corrompido.

   >[!NOTE]
   >
   >Se o nó corrompido for um nó primário AEM, desative todo o nó do cluster.

1. Recrie o sistema físico a partir de uma imagem do sistema.
1. Aplique patches ou atualizações aos formulários AEM que foram aplicados desde que a imagem foi criada. Essas informações foram registradas durante o procedimento de backup. Os formulários AEM devem ser recuperados no mesmo nível de patch que tinham quando foi feito o backup do sistema.
1. (*Opcional*) Se todos os outros nós estiverem funcionando bem, é possível que o repositório do AEM também esteja corrompido. Nesse caso, você verá uma mensagem de dessincronização do repositório no arquivo error.log do repositório AEM.

   Para restaurar o repositório, execute as etapas a seguir.

   >[!NOTE]
   >
   >Se um backup de repositório crx compactado foi colocado online, descompacte-o em qualquer local e siga o processo de restauração offline.

   1. Exclua os diretórios de repositório, compartilhado, versão e espaços de trabalho no diretório clusterNode do nó.
   1. Restaure o backup do nó de cluster (incluindo subdiretórios) para o nó.
   1. Exclua o arquivo clusterNode/revision.log no nó.
   1. Exclua o arquivo .lock no nó, se existir.
   1. Exclua o repository/system.id no nó, se existir.
   1. Exclua os arquivos &amp;ast;&amp;ast;/listener.properties no nó, se existir.
   1. Restaure repository/cluster_node.id para nós de cluster individuais.

>[!NOTE]
>
>Considere os seguintes pontos:

* Se o nó com falha era um nó primário AEM, copie todo o conteúdo da pasta do repositório secundário (crx-repository\crx.0000, onde 0000 pode conter qualquer dígito) para a pasta do repositório crx-repository\ e exclua a pasta do repositório secundário.
* Antes de reiniciar qualquer nó de cluster, certifique-se de excluir o repositório /clustered.txt do nó primário.
* Certifique-se de que o nó primário seja iniciado primeiro e, depois de ativado, inicie os outros nós.

### Restaurando todo o cluster {#restoring-the-entire-cluster}

1. Interrompa todos os nós de cluster.
1. Recrie o sistema físico a partir de uma imagem do sistema.
1. Aplique patches ou atualizações aos formulários AEM AEM que foram aplicados desde que a imagem foi criada. Essas informações foram registradas na etapa 1 do procedimento de backup. Os formulários AEM devem ser recuperados no mesmo nível de patch que tinham quando foi feito o backup do sistema.
1. Restaure o banco de dados, o GDS e os Conectores.
1. Faça o seguinte para recuperar o repositório AEM off-line:

   >[!NOTE]
   >
   >Se um backup de repositório crx compactado foi colocado online, descompacte-o em qualquer local e siga o processo de restauração offline.

   1. Em todos os nós de cluster, exclua os diretórios de repositório, compartilhado, versão e espaços de trabalho no diretório clusterNode.
   1. Exclua todos os arquivos e diretórios no diretório compartilhado.
   1. Restaure o backup do nó de cluster (incluindo subdiretórios) para um nó de cluster.
   1. Copie todos os arquivos do nó de cluster restaurado para todos os outros nós de cluster. Depois de concluído, cada nó de cluster contém os mesmos dados.
   1. Exclua o arquivo clusterNode/revision.log em todos os nós de cluster.
   1. Exclua o .lock em todos os nós de cluster, se existir.
   1. Exclua os nós de cluster repository/system.id, se existirem.
   1. Exclua os arquivos &amp;ast;&amp;ast;/listener.properties em todos os nós do cluster, se existirem.
   1. Restaure repository/cluster_node.id para nós de cluster individuais.

>[!NOTE]
>
>Considere os seguintes pontos:

* Se o nó com falha era um nó primário AEM, copie todo o conteúdo da pasta do repositório secundário (parece crx-repository\crx.0000, em que 0000 pode conter qualquer dígito) para a pasta do repositório crx-repository\.
* Antes de reiniciar qualquer nó de cluster, certifique-se de excluir o repositório /clustered.txt do nó primário.
* Certifique-se de que o nó primário seja iniciado primeiro e, depois de ativado, inicie os outros nós.

## Fazer backup e restaurar nó de publicação da Solução de gerenciamento de correspondência {#back-up-and-restore-correspondence-management-solution-publish-node}

O nó publicador não tem nenhuma relação primário-secundário em um ambiente clusterizado. Você pode fazer backup de qualquer nó do Publisher seguindo [Backup e restauração](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### Recuperar um único nó de editor {#recover-a-single-publisher-node}

1. Desligue o nó que deve ser recuperado e não faça nenhuma atividade de publicação até que o nó esteja ativo novamente.
1. Restaurar o nó do Publish usando [Restaurando o backup](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### Recuperar um cluster {#recover-a-cluster}

1. Desligue o cluster.
1. Restaurar o nó do Publish usando [Restaurando o backup](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).
1. Inicie o nó primário seguido pelo nó secundário do cluster do autor.
