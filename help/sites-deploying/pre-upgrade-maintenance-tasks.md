---
title: Tarefas de manutenção de pré-atualização
seo-title: Tarefas de manutenção de pré-atualização
description: Saiba mais sobre as tarefas de pré-atualização no AEM.
seo-description: Saiba mais sobre as tarefas de pré-atualização no AEM.
uuid: 5da1cfc7-8a10-47b1-aafb-2cd112e3f818
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 291c91e5-65ff-473d-ac11-3da480239e76
docset: aem65
feature: Atualização
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2159'
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

## Garanta espaço suficiente em disco {#ensure-sufficient-disk-space}

Ao executar a atualização, além das atividades de atualização de conteúdo e código, será necessário executar a migração do repositório. A migração criará uma cópia do repositório no novo formato do Segment Tar. Como resultado, você precisará de espaço em disco suficiente para manter uma segunda versão, potencialmente maior, do repositório.

## Faça o backup completo AEM {#fully-back-up-aem}

AEM deve ser feito o backup completo antes de iniciar a atualização. Certifique-se de fazer backup do repositório, da instalação do aplicativo, do armazenamento de dados e das instâncias do Mongo, se aplicável. Para obter mais informações sobre como fazer backup e restaurar uma instância de AEM, consulte [Backup and Restore](/help/sites-administering/backup-and-restore.md).

## Fazer backup das alterações em /etc {#backup-changes-etc}

O processo de atualização faz um bom trabalho de manter e mesclar conteúdo e configurações existentes dos caminhos `/apps` e `/libs` no repositório. Para alterações feitas no caminho `/etc`, incluindo configurações do Context Hub, geralmente é necessário reaplicar essas alterações após a atualização. Embora a atualização faça uma cópia de backup de qualquer alteração que não possa mesclar em `/var`, recomendamos fazer o backup dessas alterações manualmente antes de iniciar a atualização.

## Gerar o arquivo quickstart.properties {#generate-quickstart-properties}

Ao iniciar AEM a partir do arquivo jar, um arquivo `quickstart.properties` será gerado em `crx-quickstart/conf`. Se AEM tiver sido iniciado apenas com o script de início no passado, esse arquivo não estará presente e a atualização falhará. Verifique a existência desse arquivo e reinicie o AEM do arquivo jar se ele não estiver presente.

## Configurar a limpeza do workflow e do log de auditoria {#configure-wf-audit-purging}

As tarefas `WorkflowPurgeTask` e `com.day.cq.audit.impl.AuditLogMaintenanceTask` exigem configurações OSGi separadas e não funcionarão sem elas. Se falharem durante a execução da tarefa de pré-atualização, as configurações ausentes serão o motivo mais provável. Portanto, adicione configurações OSGi para essas tarefas ou remova-as completamente da lista de tarefas de otimização de pré-atualização se não quiser executá-las. A documentação para configurar tarefas de limpeza de workflow pode ser encontrada em [Administration Workflow Instances](/help/sites-administering/workflows-administering.md) e a configuração da tarefa de manutenção de log de auditoria pode ser encontrada em [Audit Log Maintenance no AEM 6](/help/sites-administering/operations-audit-log.md).

Para limpeza de workflow e log de auditoria no CQ 5.6, bem como limpeza de log de auditoria no AEM 6.0, consulte [Limpar workflow e nós de auditoria](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html).

## Instalar, configurar e executar as tarefas de pré-atualização {#install-configure-run-pre-upgrade-tasks}

Devido ao nível de AEM de personalização permitido, os ambientes geralmente não seguem uma maneira uniforme de executar atualizações. Isso torna difícil a criação de um procedimento padronizado para atualizações.

Em versões anteriores, também era difícil para as atualizações de AEM que foram interrompidas ou que não puderam ser retomadas com segurança. Isso levou a situações em que o reinício do procedimento de atualização completo era necessário ou em que as atualizações defeituosas eram realizadas sem acionar nenhum aviso.

Para solucionar esses problemas, o Adobe adicionou vários aprimoramentos ao processo de atualização, tornando-o mais resiliente e fácil de usar. As tarefas de manutenção de pré-atualização que antes precisavam ser executadas manualmente estão sendo otimizadas e automatizadas. Além disso, relatórios pós-atualização foram adicionados para que o processo possa ser totalmente examinado, na esperança de que quaisquer problemas sejam encontrados com mais facilidade.

Atualmente, as tarefas de manutenção pré-atualização são distribuídas por várias interfaces que são parcial ou completamente executadas manualmente. A otimização de manutenção de pré-atualização introduzida no AEM 6.3 permite uma maneira unificada de acionar essas tarefas e poder inspecionar seus resultados sob demanda.

Todas as tarefas incluídas na etapa de otimização pré-atualização são compatíveis com todas as versões a partir AEM 6.0.

### Como configurá-lo {#how-to-set-it-up}

No AEM 6.3 e posterior, as tarefas de otimização de manutenção de pré-atualização são incluídas no jar de início rápido. Se estiver atualizando de uma versão mais antiga do AEM 6, elas serão disponibilizadas por meio de pacotes separados que você pode baixar no Gerenciador de pacotes.

Você pode encontrar os pacotes nesses locais:

* [Para atualização do AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [Para atualização do AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [Para atualização do AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62)

### Como usá-lo {#how-to-use-it}

O `PreUpgradeTasksMBean` componente OSGI vem pré-configurado com uma lista de tarefas de manutenção de pré-atualização que podem ser executadas de uma só vez. Você pode configurar as tarefas seguindo o procedimento abaixo:

1. Vá para o Console da Web navegando até *https://serveraddress:serverport/system/console/configMgr*

1. Procure por &quot;**preupgradetask**&quot; e clique no primeiro componente correspondente. O nome completo do componente é `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. Modifique a lista de tarefas de manutenção que precisam ser executadas conforme mostrado abaixo:

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
   <td>Corre a marca e varre. Para armazenamentos de dados compartilhados, remova essa etapa e execute<br /> manualmente ou prepare instâncias corretamente antes de executar.</td>
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
>`DataStoreGarbageCollectionTask` O está chamando uma operação de coleta de lixo do armazenamento de dados com a fase de marcação e varredura, se usada. Para implantações que usam um armazenamento de dados compartilhado, certifique-se de reconfigurá-lo ou apropriadamente ou preparar a instância para evitar a exclusão de itens referenciados por outra instância. Isso pode exigir a execução manual da fase de marca em todas as instâncias antes de acionar essa tarefa de pré-atualização.

### Configuração Padrão das Verificações de Integridade de Pré-Atualização {#default-configuration-of-the-pre-upgrade-health-checks}

O componente `PreUpgradeTasksMBeanImpl` OSGI vem pré-configurado com uma lista de tags de verificação de integridade de pré-atualização a serem executadas quando o método `runAllPreUpgradeHealthChecks` é chamado:

* **sistema**  - a tag usada pelas verificações de integridade de manutenção do granite

* **pré-atualização**  - esta é uma tag personalizada que pode ser adicionada a todas as verificações de integridade que você pode definir para serem executadas antes de uma atualização

A lista é editável. Você pode usar os botões de mais **(+)** e menos **(-)** além das tags para adicionar mais tags personalizadas ou remover as padrão.

**Métodos do MBean**

A funcionalidade do bean gerenciado pode ser acessada usando o [Console JMX](/help/sites-administering/jmx-console.md).

Você pode acessar os MBeans usando:

1. Ir para o Console JMX em *https://serveraddress:serverport/system/console/jmx*
1. Procure por **PreUpgradeTasks** e clique no resultado

1. Selecione qualquer método na seção **Operations** e selecione **Invoke** na janela a seguir.

Abaixo está uma lista de todos os métodos disponíveis que o `PreUpgradeTasksMBeanImpl` expõe:

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
   <td>Verifica se a tarefa <code>runAllPreUpgradeTasksmaintenance</code> está em execução no momento.</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Verifica se qualquer tarefa de manutenção de pré-atualização está em execução no momento e <br /> retorna uma matriz contendo os nomes das tarefas em execução no momento.</td>
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
   <td><p>Executa todas as verificações de integridade de pré-atualização e salva seu status em um arquivo chamado <code>preUpgradeHCStatus.properties</code> que está localizado no caminho inicial do sling. Se o parâmetro <code>shutDownOnSuccess</code> for definido como <code>true</code>, a instância AEM será encerrada, mas somente se todas as verificações de integridade pré-atualização tiverem um status OK.</p> <p>O arquivo de propriedades será usado como uma pré-condição para qualquer atualização futura<br /> e o processo de atualização será interrompido se a execução da verificação de integridade de pré-atualização<br /> falhar. Se quiser ignorar o resultado das verificações de integridade pré-atualização<br /> e iniciar a atualização de qualquer maneira, poderá excluir o arquivo.</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>AÇÃO</td>
   <td>Lista todos os pacotes importados que não serão mais cumpridos ao atualizar para a versão de AEM especificada. <br /> A versão do AEM de destino deve ser <br /> fornecida como parâmetro.</td>
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

A maneira como `LoginModules` personalizado é configurado para autenticação no nível do repositório foi alterada fundamentalmente no Apache Oak.

Em AEM versões que usavam a configuração do CRX2, era colocada no arquivo `repository.xml`, enquanto AEM 6 em diante é feita no serviço Apache Felix JAAS Configuration Fatory via Web Console.

Portanto, qualquer configuração existente terá que ser desativada e recriada para o Apache Oak após a atualização.

Para desativar os módulos personalizados definidos na configuração JAAS de `repository.xml`, é necessário modificar a configuração para usar o `LoginModule` padrão, como neste exemplo:

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
>Para obter mais informações, consulte [Autenticação com o Módulo de Logon Externo](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).
>
>Para obter um exemplo de configuração `LoginModule` no AEM 6, consulte [Configuração do LDAP com AEM 6](/help/sites-administering/ldap-config.md).

## Remover Atualizações Do Diretório /install {#remove-updates-install-directory}

>[!NOTE]
>
>Remova apenas pacotes do diretório crx-quickstart/install APÓS desligar a instância do AEM. Esta será uma das últimas etapas antes de iniciar o procedimento de atualização no local.

Remova todos os service packs, pacotes de recursos ou hotfixes que foram implantados por meio do diretório `crx-quickstart/install` no sistema de arquivos local. Isso impedirá a instalação inadvertida de hotfixes e service packs antigos além da nova versão do AEM após a conclusão da atualização.

## Interrompa Todas as Instâncias de Espera Fria {#stop-tarmk-coldstandby-instance}

Se estiver usando o modo de espera frio TarMK, pare as instâncias de espera frias. Isso garantirá uma maneira eficiente de retornar online em caso de problemas na atualização. Após a conclusão bem-sucedida da atualização, as instâncias de standby frio precisarão ser recriadas a partir das instâncias primárias atualizadas.

## Desativar Tarefas Agendadas Personalizadas {#disable-custom-scheduled-jobs}

Desative quaisquer trabalhos agendados OSGi incluídos no código do seu aplicativo.

## Executar Limpeza de Revisão Offline {#execute-offline-revision-cleanup}

>[!NOTE]
>
>Essa etapa só é necessária para instalações do TarMK

Se estiver usando o TarMK, você deve executar a Limpeza de Revisão Offline antes de atualizar. Isso fará com que a etapa de migração do repositório e as tarefas subsequentes de atualização sejam executadas muito mais rapidamente e ajudará a garantir que a Limpeza de Revisão Online possa ser executada com êxito após a conclusão da atualização. Para obter informações sobre como executar a Limpeza de Revisão Offline, consulte [Executando a Limpeza de Revisão Offline](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup).

## Executar coleta de lixo do armazenamento de dados {#execute-datastore-garbage-collection}

>[!NOTE]
>
>Essa etapa só é necessária para instâncias que executam o crx3

Depois de executar a limpeza de revisão em instâncias do CRX3, você deve executar a Coleta de lixo do armazenamento de dados para remover blobs não referenciados no armazenamento de dados. Para obter instruções, consulte a documentação em [Coleta de lixo do armazenamento de dados](/help/sites-administering/data-store-garbage-collection.md).

## Atualize o esquema do banco de dados, se necessário {#upgrade-the-database-schema-if-needed}

Geralmente, a pilha subjacente do Apache Oak AEM usa para persistência cuidará da atualização do schema do banco de dados, se necessário.

No entanto, podem ocorrer casos em que o schema não pode ser atualizado automaticamente. Esses são ambientes de alta segurança, em que o banco de dados está sendo executado sob um usuário com privilégios muito limitados. Se isso acontecer, AEM continuará usando o schema antigo.

Para evitar que isso aconteça, é necessário atualizar o schema seguindo o procedimento abaixo:

1. Desligue a instância de AEM que precisa ser atualizada.
1. Atualize o schema do banco de dados. Consulte a documentação do tipo de banco de dados para ver quais ferramentas você precisa usar para conseguir isso.

   Para obter mais informações sobre como o Oak lida com atualizações de esquema, consulte [esta página no site do Apache](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade).

1. Continue com o AEM de atualização.

## Excluir usuários que possam impedir a atualização {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>Essa tarefa de manutenção pré-atualização só é necessária se:
>
>* Você está atualizando de AEM versões anteriores à AEM 6.3
>* Você encontra qualquer um dos erros mencionados abaixo durante a atualização.

>



Há casos excepcionais em que os usuários do serviço podem acabar sendo marcados incorretamente como usuários regulares em versões AEM mais antigas.

Se isso acontecer, a atualização falhará com uma mensagem como esta:

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

Para contornar esse problema, faça o seguinte:

1. Desanexar a instância do tráfego de produção
1. Crie um backup dos usuários que causam o problema. Você pode fazer isso por meio do Gerenciador de pacotes. Para obter mais informações, consulte [Como trabalhar com pacotes.](/help/sites-administering/package-manager.md)
1. Exclua os usuários que estão causando o problema. Abaixo está uma lista de usuários que podem estar incluídos nesta categoria:

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## Girar arquivos de log {#rotate-log-files}

Recomendamos o arquivamento dos arquivos de log atuais antes de iniciar a atualização. Isso facilitará o monitoramento e a verificação dos arquivos de log durante e após a atualização para identificar e resolver qualquer problema que possa ocorrer.
