---
title: Tarefas de manutenção pré-atualização
seo-title: Tarefas de manutenção pré-atualização
description: Saiba mais sobre as tarefas de pré-atualização no AEM.
seo-description: Saiba mais sobre as tarefas de pré-atualização no AEM.
uuid: 5da1cfc7-8a10-47b1-aafb-2cd112e3f818
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 291c91e5-65ff-473d-ac11-3da480239e76
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '2158'
ht-degree: 0%

---


# Tarefas de manutenção de pré-atualização{#pre-upgrade-maintenance-tasks}

Antes de iniciar a atualização, é importante seguir essas tarefas de manutenção para garantir que o sistema esteja pronto e possa ser revertido em caso de problemas:

* [Garantir espaço em disco suficiente](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [Fazer backup completo AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [Fazer backup das alterações em /etc](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [Gerar o arquivo quickstart.properties](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [Configurar o fluxo de trabalho e a remoção do registro de auditoria](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [Instalar, configurar e executar as Tarefas de pré-atualização](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [Desativar Módulos de Logon Personalizados](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [Remover Atualizações Do Diretório /install](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [Parar instâncias de espera frias](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [Desativar Tarefas Agendadas Personalizadas](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [Executar Limpeza de Revisão Offline](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [Executar coleta de lixo do armazenamento de dados](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [Atualize o Schema do banco de dados se necessário](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [Excluir usuários que possam prejudicar a atualização](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [Girar arquivos de registro](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## Garantir espaço suficiente em disco {#ensure-sufficient-disk-space}

Ao executar a atualização, além das atividades de atualização de conteúdo e código, será necessário executar uma migração de repositório. A migração criará uma cópia do repositório no novo formato Segment Tar. Como resultado, você precisará de espaço em disco suficiente para reter uma segunda versão, potencialmente maior, do repositório.

## Faça backup total AEM {#fully-back-up-aem}

AEM deve ser feito o backup completo antes de iniciar a atualização. Certifique-se de fazer backup do repositório, da instalação do aplicativo, do armazenamento de dados e das instâncias Mongo, se aplicável. Para obter mais informações sobre como fazer backup e restaurar uma instância AEM, consulte [Backup e restauração](/help/sites-administering/backup-and-restore.md).

## Fazer backup das alterações em /etc {#backup-changes-etc}

O processo de atualização faz um bom trabalho para manter e mesclar conteúdo e configurações existentes nos caminhos `/apps` e `/libs` no repositório. Para alterações feitas no caminho `/etc`, incluindo configurações do Context Hub, geralmente é necessário reaplicar essas alterações após a atualização. Embora a atualização faça uma cópia de backup de todas as alterações que não possam ser mescladas em `/var`, recomendamos fazer backup dessas alterações manualmente antes de iniciar a atualização.

## Gerar o arquivo quickstart.properties {#generate-quickstart-properties}

Ao iniciar o AEM do arquivo jar, um arquivo `quickstart.properties` será gerado em `crx-quickstart/conf`. Se o AEM tiver sido iniciado somente com o script do start no passado, esse arquivo não estará presente e a atualização falhará. Verifique a existência desse arquivo e reinicie o AEM do arquivo jar se ele não estiver presente.

## Configurar o fluxo de trabalho e a remoção do registro de auditoria {#configure-wf-audit-purging}

As tarefas `WorkflowPurgeTask` e `com.day.cq.audit.impl.AuditLogMaintenanceTask` exigem configurações OSGi separadas e não funcionarão sem elas. Se falharem durante a execução da tarefa de pré-atualização, as configurações ausentes serão o motivo mais provável. Portanto, adicione configurações OSGi para essas tarefas ou remova-as completamente da lista de otimização de pré-atualização da tarefa se você não desejar executá-las. A documentação para configurar as tarefas de expurgação do fluxo de trabalho pode ser encontrada em [Administrando Instâncias do Fluxo de Trabalho](/help/sites-administering/workflows-administering.md) e a configuração da tarefa de manutenção do log de auditoria pode ser encontrada em [Manutenção do Log de Auditoria no AEM 6](/help/sites-administering/operations-audit-log.md).

Para obter fluxo de trabalho e expurgação de log de auditoria no CQ 5.6, bem como expurgação de log de auditoria no AEM 6.0, consulte [Expurgar fluxo de trabalho e nós de auditoria](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html).

## Instalar, configurar e executar as Tarefas de pré-atualização {#install-configure-run-pre-upgrade-tasks}

Devido ao nível de AEM de personalização permitido, os ambientes geralmente não seguem uma maneira uniforme de executar atualizações. Isso torna difícil a criação de um procedimento padronizado para atualizações.

Em versões anteriores, também era difícil para atualizações AEM que foram interrompidas ou que não foram retomadas com segurança. Isso levou a situações em que era necessário reiniciar o procedimento completo de atualização ou em que atualizações defeituosas eram realizadas sem acionar avisos.

Para resolver esses problemas, o Adobe adicionou várias melhorias ao processo de atualização, tornando-o mais resiliente e fácil de usar. As tarefas de manutenção de pré-atualização que antes precisavam ser executadas manualmente estão sendo otimizadas e automatizadas. Além disso, os relatórios pós-atualização foram adicionados para que o processo possa ser totalmente examinado na esperança de que quaisquer problemas sejam encontrados mais facilmente.

As tarefas de manutenção de pré-atualização estão distribuídas por várias interfaces que são parcial ou completamente executadas manualmente. A otimização de manutenção de pré-atualização introduzida no AEM 6.3 permite uma maneira unificada de acionar essas tarefas e inspecionar seus resultados sob demanda.

Todas as tarefas incluídas na etapa de otimização pré-atualização são compatíveis com todas as versões a partir AEM 6.0.

### Como configurá-lo {#how-to-set-it-up}

No AEM 6.3 e posterior, as tarefas de otimização de manutenção pré-atualização são incluídas no jar de início rápido. Se você estiver atualizando de uma versão anterior do AEM 6, eles serão disponibilizados por pacotes separados que você pode baixar do Gerenciador de pacotes.

Você pode encontrar os pacotes nesses locais:

* [Para atualização do AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [Para atualização do AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [Para atualização do AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62)

### Como usá-la {#how-to-use-it}

O componente `PreUpgradeTasksMBean` OSGI vem pré-configurado com uma lista de tarefas de manutenção de pré-atualização que podem ser executadas de uma só vez. Você pode configurar as tarefas seguindo o procedimento abaixo:

1. Vá para o Console da Web navegando até *https://serveraddress:serverport/system/console/configMgr*

1. Procure por &quot;**preupgradetask**&quot; e clique no primeiro componente correspondente. O nome completo do componente é `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. Modifique a lista das tarefas de manutenção que precisam ser executadas, conforme mostrado abaixo:

   ![1487758925984](assets/1487758925984.png)

A lista da tarefa difere dependendo do modo de execução usado para start da instância. Abaixo está uma descrição do modo de execução para o qual cada tarefa de manutenção foi projetada.

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
   <td>Vai fazer a marca e varrer. Para armazenamentos de dados compartilhados, remova essa etapa e execute<br /> preparar instâncias manualmente ou adequadamente antes de executá-las.</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>É necessário configurar o OSGi de Configuração de Expurgação do Fluxo de Trabalho do Adobe Granite antes de executá-lo.</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>Para instâncias do TarMK no AEM 6.0 a 6.2, execute manualmente a Limpeza de revisão offline.</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>É necessário configurar a configuração OSGi do Scheduler de Expurgação do Log de Auditoria antes da execução.</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>`DataStoreGarbageCollectionTask` O está chamando uma operação de Coleta de Lixo do Datastore com a fase de marcação e varredura, se usada. Para implantações que usam um armazenamento de dados compartilhado, certifique-se de reconfigurá-lo ou prepará-lo corretamente ou preparar a instância para evitar a exclusão de itens referenciados por outra instância. Isso pode exigir a execução manual da fase de marca em todas as instâncias antes de disparar essa tarefa de pré-atualização.

### Configuração padrão das verificações de integridade pré-atualização {#default-configuration-of-the-pre-upgrade-health-checks}

O componente `PreUpgradeTasksMBeanImpl` OSGI vem pré-configurado com uma lista de tags de verificação de integridade pré-atualização a serem executadas quando o método `runAllPreUpgradeHealthChecks` é chamado:

* **sistema**  - a etiqueta utilizada pelos controlos sanitários de manutenção dos granitos

* **pré-atualização**  - esta é uma tag personalizada que pode ser adicionada a todas as verificações de integridade que você pode definir para executar antes de uma atualização

A lista é editável. Você pode usar os botões mais **(+)** e menos **(-)** além das tags para adicionar mais tags personalizadas ou remover as padrão.

**Métodos do MBean**

A funcionalidade do bean gerenciado pode ser acessada usando o [Console JMX](/help/sites-administering/jmx-console.md).

Você pode acessar os MBeans:

1. Ir para o console JMX em *https://serveraddress:serverport/system/console/jmx*
1. Procure **PreUpgradeTasks** e clique no resultado

1. Selecione qualquer método na seção **Operações** e selecione **Chamar** na seguinte janela.

Abaixo está uma lista de todos os métodos disponíveis que `PreUpgradeTasksMBeanImpl` expõe:

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
   <td>Exibe a lista de nomes de tarefas de manutenção de pré-atualização disponíveis.</td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeHealthChecksTagNames()</code></td>
   <td>INFORMAÇÕES</td>
   <td>Exibe a lista de nomes de tags de verificação de integridade pré-atualização.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeTasks()</code></td>
   <td>AÇÃO</td>
   <td>Executa todas as tarefas de manutenção de pré-atualização na lista.</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>AÇÃO</td>
   <td>Executa a tarefa de manutenção pré-atualização com o nome fornecido como parâmetro.</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Verifica se a tarefa <code>runAllPreUpgradeTasksmaintenance</code> está em execução no momento.</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Verifica se alguma tarefa de manutenção pré-atualização está em execução no momento e<br /> retorna um storage contendo os nomes do tarefa em execução no momento.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>AÇÃO</td>
   <td>Exibe o tempo de execução exato da tarefa de manutenção pré-atualização com o nome fornecido como parâmetro.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>AÇÃO</td>
   <td>Exibe o último estado de execução da tarefa de manutenção pré-atualização com o nome fornecido como parâmetro.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>AÇÃO</td>
   <td><p>Executa todas as verificações de integridade pré-atualização e salva seu status em um arquivo chamado <code>preUpgradeHCStatus.properties</code> que está localizado no caminho inicial do sling. Se o parâmetro <code>shutDownOnSuccess</code> estiver definido como <code>true</code>, a instância AEM será desligada, mas somente se todas as verificações de integridade anteriores à atualização tiverem um status OK.</p> <p>O arquivo de propriedades será usado como uma pré-condição para qualquer atualização futura<br /> e o processo de atualização será interrompido se a execução da verificação de integridade anterior à atualização<br /> falhar. Se quiser ignorar o resultado das verificações de integridade anteriores à atualização<br /> e iniciar a atualização assim mesmo, você poderá excluir o arquivo.</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>AÇÃO</td>
   <td>Lista todos os pacotes importados que não serão mais satisfeitos ao atualizar para a versão AEM especificada. <br /> A versão do público alvo AEM deve ser<br /> fornecida como parâmetro.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Os métodos MBean podem ser chamados por meio de:
>
>* O console JMX
>* Qualquer aplicativo externo que se conecte ao JMX
>* cURL

>



## Desabilitar Módulos de Logon Personalizados {#disable-custom-login-modules}

>[!NOTE]
>
>Esta etapa só é necessária se você estiver atualizando de uma versão AEM 5. Ele pode ser ignorado totalmente para atualizações de versões anteriores AEM 6.

A forma como os `LoginModules` personalizados são configurados para autenticação no nível do repositório foi fundamentalmente alterada no Apache Oak.

Em AEM versões que usavam a configuração CRX2 foram colocadas no arquivo `repository.xml`, enquanto a partir AEM 6 é feito no serviço Apache Felix JAAS Configuration Fatory via Web Console.

Portanto, quaisquer configurações existentes terão de ser desativadas e recriadas para o Apache Oak após a atualização.

Para desativar os módulos personalizados definidos na configuração JAAS de `repository.xml`, é necessário modificar a configuração para usar o padrão `LoginModule`, como neste exemplo:

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
>Para obter mais informações, consulte [Autenticação com o Módulo de logon externo](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).
>
>Para obter um exemplo da configuração `LoginModule` no AEM 6, consulte [Configuração do LDAP com AEM 6](/help/sites-administering/ldap-config.md).

## Remover Atualizações Do Diretório /install {#remove-updates-install-directory}

>[!NOTE]
>
>Remova apenas os pacotes do diretório crx-quickstart/install APÓS desligar a instância AEM. Esta será uma das últimas etapas antes de iniciar o procedimento de atualização no local.

Remova todos os service packs, pacotes de recursos ou hotfixes que foram implantados pelo diretório `crx-quickstart/install` no sistema de arquivos local. Isso impedirá a instalação inadvertida de hotfixes e service packs antigos sobre a nova versão AEM após a atualização ser concluída.

## Parar quaisquer instâncias de espera frias {#stop-tarmk-coldstandby-instance}

Se estiver usando o modo de espera frio TarMK, pare as instâncias de espera frias. Isso garantirá uma maneira eficiente de retornar online em caso de problemas na atualização. Depois que a atualização for concluída com êxito, as instâncias de espera frias precisarão ser recriadas a partir das instâncias primárias atualizadas.

## Desativar Tarefas Agendadas Personalizadas {#disable-custom-scheduled-jobs}

Desative quaisquer trabalhos programados OSGi que estejam incluídos no código do aplicativo.

## Executar Limpeza de Revisão Offline {#execute-offline-revision-cleanup}

>[!NOTE]
>
>Esta etapa só é necessária para instalações TarMK

Se estiver usando o TarMK, você deve executar a Limpeza de revisão offline antes de atualizar. Isso fará com que a etapa de migração do repositório e as tarefas subsequentes de atualização sejam executadas muito mais rapidamente e ajudará a garantir que a Limpeza de revisão online possa ser executada com êxito após a conclusão da atualização. Para obter informações sobre como executar a Limpeza de revisão offline, consulte [Executando a Limpeza de revisão offline](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup).

## Execute a coleta de lixo do armazenamento de dados {#execute-datastore-garbage-collection}

>[!NOTE]
>
>Esta etapa só é necessária para instâncias que executam o crx3

Depois de executar a limpeza de revisão em instâncias do CRX3, você deve executar a Coleta de Lixo do Repositório de Dados para remover quaisquer blobs não referenciados no armazenamento de dados. Para obter instruções, consulte a documentação em [Coleta de lixo do Data Store](/help/sites-administering/data-store-garbage-collection.md).

## Atualize o Schema do banco de dados se necessário {#upgrade-the-database-schema-if-needed}

Normalmente, a pilha subjacente do Apache Oak AEM usa para persistência cuidará da atualização do schema do banco de dados, se necessário.

No entanto, podem surgir casos em que o schema não pode ser atualizado automaticamente. Esses são ambientes de alta segurança em que o banco de dados está sendo executado sob um usuário com privilégios muito limitados. Se isso acontecer, AEM continuará a usar o schema antigo.

Para evitar que isso aconteça, é necessário atualizar o schema seguindo o procedimento abaixo:

1. Desligue a instância AEM que precisa ser atualizada.
1. Atualize o schema do banco de dados. Consulte a documentação do tipo de banco de dados para ver qual é a ferramenta que você precisa usar para conseguir isso.

   Para obter mais informações sobre como o Oak lida com atualizações de schemas, consulte [esta página no site do Apache](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade).

1. Continue com a atualização do AEM.

## Excluir usuários que possam prejudicar a atualização {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>Esta tarefa de manutenção pré-atualização só é necessária se:
>
>* Você está atualizando de versões AEM anteriores à AEM 6.3
>* Você encontra qualquer um dos erros mencionados abaixo durante a atualização.

>



Há casos excepcionais em que os usuários do serviço podem acabar sendo marcados incorretamente como usuários comuns em versões mais antigas AEM.

Se isso acontecer, a atualização falhará com uma mensagem como esta:

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

Para contornar esse problema, certifique-se de fazer o seguinte:

1. Desanexar a instância do tráfego de produção
1. Crie um backup dos usuários que causam o problema. Isso pode ser feito por meio do Gerenciador de pacotes. Para obter mais informações, consulte [Como trabalhar com pacotes.](/help/sites-administering/package-manager.md)
1. Exclua os usuários que estão causando o problema. Abaixo está uma lista de usuários que podem se encaixar nesta categoria:

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## Girar arquivos de registro {#rotate-log-files}

Recomendamos o arquivamento dos arquivos de registro atuais antes de iniciar a atualização. Isso facilitará o monitoramento e a verificação dos arquivos de registro durante e após a atualização para identificar e resolver quaisquer problemas que possam ocorrer.
