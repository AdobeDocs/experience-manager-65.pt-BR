---
title: Tarefas de manutenção de pré-atualização
seo-title: Pre-Upgrade Maintenance Tasks
description: Saiba mais sobre as tarefas de pré-atualização no AEM.
seo-description: Learn about the pre-upgrade tasks in AEM.
uuid: 5da1cfc7-8a10-47b1-aafb-2cd112e3f818
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 291c91e5-65ff-473d-ac11-3da480239e76
docset: aem65
feature: Upgrading
exl-id: 37d4aee4-15eb-41ab-ad71-dfbd5c7910f8
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '2030'
ht-degree: 0%

---

# Tarefas de manutenção de pré-atualização{#pre-upgrade-maintenance-tasks}

Antes de iniciar sua atualização, é importante seguir essas tarefas de manutenção para garantir que o sistema esteja pronto e possa ser revertido em caso de problemas:

* [Garantir espaço suficiente em disco](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [Fazer backup completo AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [Fazer backup das alterações em /etc](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [Gerar o arquivo quickstart.properties](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [Configurar a limpeza do workflow e do log de auditoria](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [Instalar, configurar e executar as tarefas de pré-atualização](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [Desativar Módulos de Logon Personalizados](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [Remover Atualizações Do Diretório /install](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [Interromper Instâncias de Espera Fria](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [Desativar Trabalhos Programados Personalizados](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [Executar Limpeza de Revisão Offline](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [Executar coleta de lixo do armazenamento de dados](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [Atualizar o esquema do banco de dados, se necessário](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [Excluir usuários que possam prejudicar a atualização](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [Girar arquivos de log](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## Garantir espaço suficiente em disco {#ensure-sufficient-disk-space}

Ao executar a atualização, além das atividades de atualização de conteúdo e código, é necessário executar uma migração do repositório. A migração cria uma cópia do repositório no novo formato do Segment Tar. Como resultado, você precisa de espaço em disco suficiente para manter uma segunda versão, potencialmente maior, do repositório.

## Fazer backup completo AEM {#fully-back-up-aem}

AEM deve ser feito o backup completo antes de iniciar a atualização. Certifique-se de fazer backup do repositório, da instalação do aplicativo, do armazenamento de dados e das instâncias do Mongo, se aplicável. Para obter mais informações sobre como fazer o backup e restaurar uma instância de AEM, consulte [Backup e restauração](/help/sites-administering/backup-and-restore.md).

## Fazer backup das alterações em /etc {#backup-changes-etc}

O processo de atualização faz um bom trabalho para manter e mesclar o conteúdo e as configurações existentes na `/apps` e `/libs` caminhos no repositório. Para alterações feitas no `/etc` , incluindo as configurações do Context Hub, geralmente é necessário reaplicar essas alterações após a atualização. Embora a atualização faça uma cópia de backup de qualquer alteração que não possa mesclar `/var`, o Adobe recomenda que você faça backup dessas alterações manualmente antes de iniciar a atualização.

## Gerar o arquivo quickstart.properties {#generate-quickstart-properties}

Ao iniciar o AEM a partir do arquivo jar, um `quickstart.properties` arquivo é gerado em `crx-quickstart/conf`. Se AEM tiver sido iniciado apenas com o script de início no passado, esse arquivo não estará presente e a atualização falhará. Verifique a existência desse arquivo e reinicie o AEM do arquivo jar se ele não estiver presente.

## Configurar a limpeza do workflow e do log de auditoria {#configure-wf-audit-purging}

O `WorkflowPurgeTask` e `com.day.cq.audit.impl.AuditLogMaintenanceTask` tarefas exigem configurações OSGi separadas e não podem funcionar sem elas. Se falharem durante a execução da tarefa de pré-atualização, as configurações ausentes serão o motivo mais provável. Portanto, adicione configurações OSGi para essas tarefas ou remova-as completamente da lista de tarefas de otimização de pré-atualização se não quiser executá-las. A documentação para configurar tarefas de limpeza de workflow pode ser encontrada em [Administração de instâncias de fluxo de trabalho](/help/sites-administering/workflows-administering.md) e a configuração da tarefa de manutenção de log de auditoria pode ser encontrada em [Manutenção do registro de auditoria no AEM 6](/help/sites-administering/operations-audit-log.md).

Para limpeza de workflow e log de auditoria no CQ 5.6, bem como limpeza de log de auditoria no AEM 6.0, consulte [Eliminar fluxo de trabalho e nós de auditoria](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html).

## Instalar, configurar e executar as tarefas de pré-atualização {#install-configure-run-pre-upgrade-tasks}

Devido ao nível de AEM de personalização permitido, os ambientes geralmente não seguem uma maneira uniforme de executar atualizações. Assim, a criação de um procedimento padronizado para atualizações torna um processo difícil.

Em versões anteriores, também era difícil para as atualizações de AEM que foram interrompidas ou que não foram retomadas com segurança. Esse problema levou a situações em que o reinício do procedimento de atualização completo era necessário ou em que as atualizações defeituosas eram realizadas sem acionar nenhum aviso.

Para solucionar esses problemas, o Adobe adicionou vários aprimoramentos ao processo de atualização, tornando-o mais resiliente e fácil de usar. As tarefas de manutenção de pré-atualização que antes precisavam ser executadas manualmente estão sendo otimizadas e automatizadas. Além disso, relatórios pós-atualização foram adicionados para que o processo possa ser totalmente examinado, na esperança de que quaisquer problemas sejam encontrados com mais facilidade.

Atualmente, as tarefas de manutenção pré-atualização são distribuídas por várias interfaces que são executadas parcial ou totalmente manualmente. A otimização de manutenção de pré-atualização introduzida no AEM 6.3 permite uma maneira unificada de acionar essas tarefas e poder inspecionar seus resultados sob demanda.

Todas as tarefas incluídas na etapa de otimização pré-atualização são compatíveis com todas as versões a partir AEM 6.0.

### Como configurá-lo {#how-to-set-it-up}

No AEM 6.3 e posterior, as tarefas de otimização de manutenção de pré-atualização são incluídas no jar de início rápido.

<!-- URLs below are all 404s. This content should probably be removed because it is entirely obsolete.

If you are upgrading from an older version of AEM 6, they are made available through separate packages that you can download from the Package Manager.

You can find the packages at these locations:

* [For upgrading from AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [For upgrading from AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [For upgrading from AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62) -->

### Como usá-lo {#how-to-use-it}

O `PreUpgradeTasksMBean` O componente OSGI vem pré-configurado com uma lista de tarefas de manutenção de pré-atualização que podem ser executadas de uma só vez. Você pode configurar as tarefas seguindo o procedimento abaixo:

1. Vá para o Console da Web navegando até *https://serveraddress:serverport/system/console/configMgr*

1. Pesquisar por &quot;**preupgradetask**&quot;, em seguida, clique no primeiro componente correspondente. O nome completo do componente é `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. Modifique a lista de tarefas de manutenção que devem ser executadas conforme mostrado abaixo:

   ![1487758925984](assets/1487758925984.png)

A lista de tarefas difere dependendo do modo de execução que está sendo usado para iniciar a instância. Abaixo está uma descrição do modo de execução para o qual cada tarefa de manutenção foi projetada.

<table>
 <tbody>
  <tr>
   <td><strong>Tarefa</strong></td>
   <td><strong>Modo de execução</strong></td>
   <td><strong>Notas</strong></td>
  </tr>
  <tr>
   <td><code>TarIndexMergeTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>DataStoreGarbageCollectionTask</code></td>
   <td>crx2</td>
   <td>Executa marca e varre. Para armazenamentos de dados compartilhados, remova esta etapa e execute<br /> preparar instâncias manualmente ou adequadamente antes da execução.</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>É necessário configurar o OSGi de Configuração de limpeza de fluxo de trabalho do Adobe Granite antes de executá-lo.</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>Para instâncias do TarMK no AEM 6.0 a 6.2, execute manualmente a Limpeza de Revisão Offline.</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>É necessário configurar a configuração OSGi do Agendador de limpeza do log de auditoria antes da execução.</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>O `DataStoreGarbageCollectionTask` chama uma operação Datastore Garbage Collection com a fase de marcação e varredura, se usada. Para implantações que usam um armazenamento de dados compartilhado, certifique-se de reconfigurá-lo corretamente ou preparar a instância para evitar a exclusão de itens referenciados por outra instância. Esse processo pode exigir a execução manual da fase de marca em todas as instâncias antes de acionar essa tarefa de pré-atualização.

### Configuração padrão das verificações de integridade pré-atualização {#default-configuration-of-the-pre-upgrade-health-checks}

O `PreUpgradeTasksMBeanImpl` O componente OSGI vem pré-configurado com uma lista de tags de verificação de integridade de pré-atualização a serem executadas quando o `runAllPreUpgradeHealthChecks` é chamado:

* **sistema** - a etiqueta utilizada pelos controlos sanitários de manutenção dos granitos

* **pré-atualização** - uma tag personalizada que pode ser adicionada a todas as verificações de integridade que você pode definir para executar antes de uma atualização

A lista é editável. Você pode usar o sinal de mais **(+)** e menos **(-)** além das tags, para adicionar mais tags personalizadas ou remover as tags padrão.

**Métodos do MBean**

A funcionalidade do bean gerenciado pode ser acessada usando o [Console JMX](/help/sites-administering/jmx-console.md).

Você pode acessar os MBeans usando:

1. Ir para o Console JMX em *https://serveraddress:serverport/system/console/jmx*
1. Procurar por **PreUpgradeTasks** e clique no resultado

1. Selecione qualquer método no **Operações** e selecione **Invocar** na janela a seguir.

Abaixo está uma lista de todos os métodos disponíveis que a variável `PreUpgradeTasksMBeanImpl` expõe:

<table>
 <tbody>
  <tr>
   <td><strong>Nome do método</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeTasksNames()</code></td>
   <td>INFO</td>
   <td>Exibe a lista de nomes de tarefas de manutenção pré-atualização disponíveis.</td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeHealthChecksTagNames()</code></td>
   <td>INFO</td>
   <td>Exibe a lista de nomes de tags de verificações de integridade pré-atualização.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeTasks()</code></td>
   <td>AÇÃO</td>
   <td>Executa todas as tarefas de manutenção de pré-atualização na lista.</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>AÇÃO</td>
   <td>Executa a tarefa de manutenção de pré-atualização com o nome dado como parâmetro.</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Verifica se a variável <code>runAllPreUpgradeTasksmaintenance</code> tarefa está em execução.</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Verifica se alguma tarefa de manutenção pré-atualização está em execução e<br /> retorna uma matriz contendo os nomes das tarefas em execução no momento.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>AÇÃO</td>
   <td>Exibe o tempo de execução exato da tarefa de manutenção pré-atualização com o nome dado como o parâmetro.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>AÇÃO</td>
   <td>Exibe o último estado de execução da tarefa de manutenção pré-atualização com o nome dado como o parâmetro.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>AÇÃO</td>
   <td><p>Executa todas as verificações de integridade de pré-atualização e salva seu status em um arquivo chamado <code>preUpgradeHCStatus.properties</code> que está no caminho do sling home. Se a variável <code>shutDownOnSuccess</code> é definido como <code>true</code>, a instância de AEM é encerrada, mas somente se todas as verificações de integridade de pré-atualização tiverem um status OK .</p> <p>O arquivo de propriedades é usado como uma pré-condição para qualquer atualização futura<br /> e o processo de atualização é interrompido se a verificação de integridade pré-atualização<br /> falha na execução. Se desejar ignorar o resultado da pré-atualização<br /> verificações de integridade e iniciar a atualização mesmo assim, você poderá excluir o arquivo.</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>AÇÃO</td>
   <td>Lista todos os pacotes importados que não são mais atendidos quando<br /> atualizando para a versão de AEM especificada. A versão de AEM de destino deve ser<br /> fornecida como parâmetro.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Os métodos MBean podem ser invocados por meio de:
>
>* O console JMX
>* Qualquer aplicativo externo que se conecta ao JMX
>* cURL
>


## Desativar Módulos de Logon Personalizados {#disable-custom-login-modules}

>[!NOTE]
>
>Essa etapa só é necessária se você estiver atualizando de uma versão AEM 5. Ele pode ser ignorado totalmente para atualizações de versões anteriores do AEM 6.

A maneira como personalizar `LoginModules` são configurados para autenticação no nível do repositório e foram alterados fundamentalmente no Apache Oak.

Em AEM versões que usaram a configuração do CRX2 foram colocadas na `repository.xml` , enquanto a partir de AEM 6, é feito no serviço Apache Felix JAAS Configuration Fatory via Web Console.

Portanto, qualquer configuração existente terá que ser desativada e recriada para o Apache Oak após a atualização.

Para desativar os módulos personalizados definidos na configuração JAAS de `repository.xml`, é necessário editar a configuração para usar o padrão `LoginModule`, como no exemplo a seguir:

```xml
<Security >
             ....
          <!--
                 Use LoginModule authenticating against repository itself
                 -->
                 <LoginModule class = "com.day.crx.core.CRXLoginModule" >
                     <param name = "anonymousId" value = "anonymous" />
                     <param name = "adminId" value ="admin" />
                     <param name = "disableNTLMAuth" value = "true" />
                     <param name = "tokenExpiration" value = "43200000" />
                     <!-- param name="trust_credentials_attribute" value="d5b9167e95dad6e7d3b5d6fa8df48af8"/
                -->
                 </LoginModule >
         </ Security>
```

>[!NOTE]
>
>Para obter mais informações, consulte [Autenticação com o módulo de logon externo](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).
>
>Para obter um exemplo de `LoginModule` configuração no AEM 6, consulte [Configuração do LDAP com AEM 6](/help/sites-administering/ldap-config.md).

## Remover Atualizações Do Diretório /install {#remove-updates-install-directory}

>[!NOTE]
>
>Remova apenas pacotes do diretório crx-quickstart/install APÓS desligar a instância do AEM. Esta etapa é uma das últimas antes de iniciar o procedimento de atualização no local.

Remova todos os service packs, pacotes de recursos ou hotfixes que foram implantados por meio do `crx-quickstart/install` no sistema de arquivos local. Isso impede a instalação inadvertida de hotfixes e service packs antigos além da nova versão do AEM após a conclusão da atualização.

## Interromper Instâncias de Espera Fria {#stop-tarmk-coldstandby-instance}

Se estiver usando o modo de espera frio TarMK, pare as instâncias de espera frias. Isso garante uma maneira eficiente de retornar online se houver problemas na atualização. Após a conclusão bem-sucedida da atualização, as instâncias de standby frio devem ser recriadas a partir das instâncias primárias atualizadas.

## Desativar Trabalhos Programados Personalizados {#disable-custom-scheduled-jobs}

Desative quaisquer trabalhos agendados OSGi incluídos no código do seu aplicativo.

## Executar Limpeza de Revisão Offline {#execute-offline-revision-cleanup}

>[!NOTE]
>
>Essa etapa só é necessária para instalações do TarMK

Se estiver usando o TarMK, você deve executar a Limpeza de Revisão Offline antes de atualizar. Isso faz com que a etapa de migração do repositório e as tarefas subsequentes de atualização sejam executadas muito mais rapidamente e ajuda a garantir que a Limpeza de Revisão Online possa ser executada com êxito após a conclusão da atualização. Para obter informações sobre como executar a Limpeza de Revisão Offline, consulte [Executando limpeza de revisão offline](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup).

## Executar coleta de lixo do armazenamento de dados {#execute-datastore-garbage-collection}

>[!NOTE]
>
>Essa etapa só é necessária para instâncias que executam o crx3

Depois de executar a limpeza de revisão em instâncias do CRX3, você deve executar a Coleta de lixo do armazenamento de dados para remover blobs não referenciados no armazenamento de dados. Para obter instruções, consulte a documentação em [Coleta de lixo do armazenamento de dados](/help/sites-administering/data-store-garbage-collection.md).

## Atualizar o esquema do banco de dados, se necessário {#upgrade-the-database-schema-if-needed}

Normalmente, a pilha subjacente do Apache Oak que AEM usa para persistência cuida da atualização do schema do banco de dados, se necessário.

No entanto, podem ocorrer casos em que o schema não pode ser atualizado automaticamente. Esses casos são principalmente ambientes de alta segurança em que o banco de dados está sendo executado sob um usuário com privilégios limitados. Se tal situação ocorrer, o AEM continuará a usar o schema antigo.

Para evitar que tal cenário ocorra, atualize o schema fazendo o seguinte:

1. Desligue a instância de AEM que deve ser atualizada.
1. Atualize o schema do banco de dados. Consulte a documentação do tipo de banco de dados para ver quais ferramentas são necessárias para obter o resultado.

   Para obter mais informações sobre como o Oak lida com atualizações de esquema, consulte [esta página no site do Apache](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade).

1. Continue com o AEM de atualização.

## Excluir usuários que possam prejudicar a atualização {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>Essa tarefa de manutenção pré-atualização só é necessária se:
>
>* Você está atualizando de AEM versões anteriores à AEM 6.3
>* Você encontra qualquer um dos erros mencionados abaixo durante a atualização.
>


Há casos excepcionais em que os usuários do serviço podem acabar sendo marcados incorretamente como usuários regulares em uma versão AEM mais antiga.

Se tal situação ocorrer, a atualização falhará com uma mensagem como a seguinte:

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

Para contornar esse problema, faça o seguinte:

1. Desanexar a instância do tráfego de produção
1. Crie um backup de um ou mais usuários causando o problema. Você pode fazer essa tarefa por meio do Gerenciador de Pacotes. Para obter mais informações, consulte [Como trabalhar com pacotes.](/help/sites-administering/package-manager.md)
1. Exclua um ou mais usuários que estejam causando o problema. Abaixo está uma lista de usuários que podem estar incluídos nesta categoria:

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## Girar arquivos de log {#rotate-log-files}

O Adobe recomenda o arquivamento dos arquivos de log atuais antes de iniciar a atualização. Isso facilita monitorar e verificar seus arquivos de log durante e após a atualização para identificar e resolver qualquer problema que possa ocorrer.
