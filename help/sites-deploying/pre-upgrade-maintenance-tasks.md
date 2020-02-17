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
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Tarefas de manutenção de pré-atualização{#pre-upgrade-maintenance-tasks}

Antes de iniciar a atualização, é importante seguir essas tarefas de manutenção para garantir que o sistema esteja pronto e possa ser revertido em caso de problemas:

* [Garantir espaço em disco suficiente](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [Fazer backup completo do AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [Fazer backup das alterações em /etc](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [Gerar o arquivo quickstart.properties](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [Configurar o fluxo de trabalho e a remoção do registro de auditoria](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [Instalar, configurar e executar as tarefas de pré-atualização](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [Desativar Módulos de Logon Personalizados](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [Remover Atualizações Do Diretório /install](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [Parar instâncias de espera frias](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [Desativar Tarefas Agendadas Personalizadas](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [Executar Limpeza de Revisão Offline](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [Executar coleta de lixo do armazenamento de dados](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [Atualizar o esquema do banco de dados, se necessário](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [Excluir usuários que possam prejudicar a atualização](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [Girar arquivos de registro](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## Garantir espaço em disco suficiente {#ensure-sufficient-disk-space}

Ao executar a atualização, além das atividades de atualização de código e conteúdo, será necessário executar uma migração de repositório. A migração criará uma cópia do repositório no novo formato Segment Tar. Como resultado, você precisará de espaço em disco suficiente para manter uma segunda versão, potencialmente maior, do repositório.

## Fazer backup completo do AEM {#fully-back-up-aem}

O backup do AEM deve ser feito antes de iniciar a atualização. Certifique-se de fazer backup do repositório, da instalação do aplicativo, do armazenamento de dados e das instâncias Mongo, se aplicável. Para obter mais informações sobre como fazer backup e restaurar uma instância do AEM, consulte [Backup e restauração](/help/sites-administering/backup-and-restore.md).

## Fazer backup das alterações em /etc {#backup-changes-etc}

O processo de atualização faz um bom trabalho para manter e mesclar o conteúdo e as configurações existentes nos caminhos `/apps` e `/libs` no repositório. Para alterações feitas no `/etc` caminho, incluindo configurações do Context Hub, geralmente é necessário reaplicar essas alterações após a atualização. Embora a atualização faça uma cópia de backup de todas as alterações que não possam ser mescladas, recomendamos fazer o backup dessas alterações manualmente antes de iniciar a atualização. `/var`

## Gerar o arquivo quickstart.properties {#generate-quickstart-properties}

Ao iniciar o AEM a partir do arquivo jar, um `quickstart.properties` arquivo será gerado em `crx-quickstart/conf`. Se o AEM só tiver sido iniciado com o script de inicialização no passado, esse arquivo não estará presente e a atualização falhará. Verifique a existência desse arquivo e reinicie o AEM do arquivo jar se ele não estiver presente.

## Configurar o fluxo de trabalho e a remoção do registro de auditoria {#configure-wf-audit-purging}

As `WorkflowPurgeTask` `com.day.cq.audit.impl.AuditLogMaintenanceTask` tarefas e as configurações exigem configurações OSGi separadas e não funcionarão sem elas. Se falharem durante a execução da tarefa de pré-atualização, configurações ausentes serão o motivo mais provável. Portanto, certifique-se de adicionar configurações OSGi para essas tarefas ou removê-las completamente da lista de tarefas de otimização de pré-atualização, caso não deseje executá-las. A documentação para configurar tarefas de remoção de fluxo de trabalho pode ser encontrada em [Administração de instâncias](/help/sites-administering/workflows-administering.md) de fluxo de trabalho e a configuração da tarefa de manutenção de log de auditoria pode ser encontrada em Manutenção de log de [auditoria no AEM 6](/help/sites-administering/operations-audit-log.md).

Para obter fluxo de trabalho e expurgação de log de auditoria no CQ 5.6, bem como expurgação de log de auditoria no AEM 6.0, consulte [Expurgar fluxo de trabalho e nós](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html)de auditoria.

## Instalar, configurar e executar as tarefas de pré-atualização {#install-configure-run-pre-upgrade-tasks}

Devido ao nível de personalização que o AEM permite, os ambientes geralmente não seguem uma maneira uniforme de executar atualizações. Isso torna difícil a criação de um procedimento padronizado para atualizações.

Em versões anteriores, também era difícil para as atualizações do AEM que foram interrompidas ou que não foram retomadas com segurança. Isso levou a situações em que era necessário reiniciar o procedimento completo de atualização ou em que atualizações defeituosas eram realizadas sem acionar avisos.

Para solucionar esses problemas, a Adobe adicionou várias melhorias ao processo de atualização, tornando-o mais resiliente e fácil de usar. As tarefas de manutenção de pré-atualização que antes precisavam ser executadas manualmente estão sendo otimizadas e automatizadas. Além disso, os relatórios pós-atualização foram adicionados para que o processo possa ser totalmente examinado na esperança de que quaisquer problemas sejam encontrados mais facilmente.

As tarefas de manutenção de pré-atualização estão distribuídas por várias interfaces que são parcial ou completamente executadas manualmente. A otimização de manutenção de pré-atualização introduzida no AEM 6.3 permite uma maneira unificada de acionar essas tarefas e inspecionar seus resultados sob demanda.

Todas as tarefas incluídas na etapa de otimização de pré-atualização são compatíveis com todas as versões do AEM 6.0 em diante.

### Como configurar {#how-to-set-it-up}

No AEM 6.3 e posterior, as tarefas de otimização de manutenção pré-atualização são incluídas no jar de início rápido. Se você estiver atualizando de uma versão anterior do AEM 6, eles serão disponibilizados por pacotes separados que você pode baixar do Gerenciador de pacotes.

Você pode encontrar os pacotes nesses locais:

* [Para atualizar do AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [Para atualizar do AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [Para atualizar do AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62)

### How to Use It {#how-to-use-it}

O componente `PreUpgradeTasksMBean` OSGI vem pré-configurado com uma lista de tarefas de manutenção de pré-atualização que podem ser executadas de uma só vez. Você pode configurar as tarefas seguindo o procedimento abaixo:

1. Vá para o Console da Web navegando até *https://serveraddress:serverport/system/console/configMgr*

1. Procure &quot;**preupgradetask**&quot; e clique no primeiro componente correspondente. O nome completo do componente é `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. Modifique a lista de tarefas de manutenção que precisam ser executadas, conforme mostrado abaixo:

   ![1487758925984](assets/1487758925984.png)

A lista de tarefas difere dependendo do modo de execução usado para iniciar a instância. Abaixo está uma descrição do modo de execução para o qual cada tarefa de manutenção foi projetada.

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
   <td>Vai fazer a marca e varrer. Para armazenamentos de dados compartilhados, remova essa etapa e execute<br /> as instâncias de preparação manual ou adequada antes de executá-las.</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>É necessário configurar o OSGi de Configuração de Expurgação do Fluxo de Trabalho do Adobe Granite antes da execução.</td>
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
   <td>É necessário configurar a configuração OSGi do Agendador de Expurgação do Log de Auditoria antes da execução.</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>`DataStoreGarbageCollectionTask` O está chamando uma operação de Coleta de Lixo do Datastore com a fase de marcação e varredura, se usada. Para implantações que usam um armazenamento de dados compartilhado, certifique-se de reconfigurá-lo ou prepará-lo corretamente ou preparar a instância para evitar a exclusão de itens referenciados por outra instância. Isso pode exigir a execução manual da fase de marcação em todas as instâncias antes de acionar essa tarefa de pré-atualização.

### Configuração padrão das verificações de integridade pré-atualização {#default-configuration-of-the-pre-upgrade-health-checks}

O componente `PreUpgradeTasksMBeanImpl` OSGI vem pré-configurado com uma lista de tags de verificação de integridade pré-atualização a serem executadas quando o `runAllPreUpgradeHealthChecks` método é chamado:

* **sistema** - a tag usada pelas verificações de integridade da manutenção do granito

* **pré-atualização** - esta é uma tag personalizada que pode ser adicionada a todas as verificações de integridade que você pode definir para executar antes de uma atualização

A lista é editável. Você pode usar os botões mais **(+)** e menos **(-)** além das tags para adicionar mais tags personalizadas ou remover as padrão.

**Métodos do MBean**

A funcionalidade do bean gerenciado pode ser acessada usando o Console [](/help/sites-administering/jmx-console.md)JMX.

Você pode acessar os MBeans:

1. Ir para o console JMX em *https://serveraddress:serverport/system/console/jmx*
1. Procure por **PreUpgradeTasks** e clique no resultado

1. Selecione qualquer método na seção **Operações** e selecione **Chamar** na janela a seguir.

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
   <td>Exibe a lista de nomes de tarefas de manutenção de pré-atualização disponíveis.</td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeHealthChecksTagNames()</code></td>
   <td>INFO</td>
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
   <td>Executa a tarefa de manutenção de pré-atualização com o nome fornecido como parâmetro.</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Verifica se a <code>runAllPreUpgradeTasksmaintenance</code> tarefa está em execução no momento.</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Verifica se alguma tarefa de manutenção de pré-atualização está em execução no momento e<br /> retorna um storage contendo os nomes das tarefas em execução no momento.</td>
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
   <td><p>Executa todas as verificações de integridade pré-atualização e salva seu status em um arquivo chamado <code>preUpgradeHCStatus.properties</code> que está localizado no caminho inicial do sling. Se o <code>shutDownOnSuccess</code> parâmetro estiver definido como <code>true</code>, a instância do AEM será desligada, mas somente se todas as verificações de integridade anteriores à atualização tiverem um status OK.</p> <p>O arquivo de propriedades será usado como pré-condição para qualquer atualização<br /> futura e o processo de atualização será interrompido se a execução da verificação<br /> de integridade da pré-atualização falhar. Se quiser ignorar o resultado das verificações de integridade de pré-atualização<br /> e iniciar a atualização assim mesmo, você pode excluir o arquivo.</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>AÇÃO</td>
   <td>Lista todos os pacotes importados que não serão mais satisfeitos ao atualizar para<br /> a versão do AEM especificada. A versão de destino do AEM deve ser<br /> fornecida como parâmetro.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Os métodos MBean podem ser chamados via:
>
>* O console JMX
>* Qualquer aplicativo externo que se conecte ao JMX
>* cURL
>



## Desativar Módulos de Logon Personalizados {#disable-custom-login-modules}

>[!NOTE]
>
>Esta etapa só é necessária se você estiver atualizando de uma versão do AEM 5. Ele pode ser ignorado totalmente para atualizações de versões anteriores do AEM 6.

A forma como os personalizados `LoginModules` são configurados para autenticação no nível do repositório foi alterada fundamentalmente no Apache Oak.

Nas versões do AEM que usavam a configuração do CRX2 era colocada no `repository.xml` arquivo, enquanto a partir do AEM 6 ela é feita no serviço Apache Felix JAAS Configuration Fatory via Web Console.

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
>Para obter mais informações, consulte [Autenticação com o módulo](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)de logon externo.
>
>Para obter um exemplo de `LoginModule` configuração no AEM 6, consulte [Configuração do LDAP com o AEM 6](/help/sites-administering/ldap-config.md).

## Remover Atualizações Do Diretório /install {#remove-updates-install-directory}

>[!NOTE]
>
>Remova apenas os pacotes do diretório crx-quickstart/install APÓS encerrar a instância do AEM. Esta será uma das últimas etapas antes de iniciar o procedimento de atualização no local.

Remova todos os service packs, pacotes de recursos ou hotfixes que foram implantados pelo `crx-quickstart/install` diretório no sistema de arquivos local. Isso impedirá a instalação inadvertida de hotfixes e service packs antigos na nova versão do AEM após a atualização ser concluída.

## Parar instâncias de espera frias {#stop-tarmk-coldstandby-instance}

Se estiver usando o modo de espera frio TarMK, pare as instâncias de espera frias. Isso garantirá uma maneira eficiente de retornar online em caso de problemas na atualização. Depois que a atualização for concluída com êxito, as instâncias de espera frias precisarão ser recriadas a partir das instâncias primárias atualizadas.

## Desativar Tarefas Agendadas Personalizadas {#disable-custom-scheduled-jobs}

Desative quaisquer trabalhos programados OSGi que estejam incluídos no código do aplicativo.

## Executar Limpeza de Revisão Offline {#execute-offline-revision-cleanup}

>[!NOTE]
>
>Esta etapa só é necessária para instalações TarMK

Se estiver usando o TarMK, você deve executar a Limpeza de revisão offline antes de atualizar. Isso tornará a etapa de migração do repositório e as tarefas subsequentes de atualização mais rápidas e ajudará a garantir que a Limpeza de revisão online possa ser executada com êxito após a conclusão da atualização. Para obter informações sobre como executar a Limpeza de revisão offline, consulte [Executando limpeza](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup)de revisão offline.

## Executar coleta de lixo do armazenamento de dados {#execute-datastore-garbage-collection}

>[!NOTE]
>
>Esta etapa só é necessária para instâncias que executam o crx3

Depois de executar a limpeza de revisão em instâncias do CRX3, você deve executar a Coleta de Lixo do Repositório de Dados para remover quaisquer blobs não referenciados no armazenamento de dados. Para obter instruções, consulte a documentação sobre a coleta [de lixo do](/help/sites-administering/data-store-garbage-collection.md)Data Store.

## Atualizar o esquema do banco de dados, se necessário {#upgrade-the-database-schema-if-needed}

Normalmente, a pilha subjacente do Apache Oak que o AEM usa para persistência cuidará da atualização do esquema do banco de dados, se necessário.

No entanto, podem surgir casos em que o esquema não pode ser atualizado automaticamente. Esses são principalmente ambientes de alta segurança em que o banco de dados está sendo executado sob um usuário com privilégios muito limitados. Se isso acontecer, o AEM continuará a usar o esquema antigo.

Para evitar que isso aconteça, é necessário atualizar o esquema seguindo o procedimento abaixo:

1. Desligue a instância do AEM que precisa ser atualizada.
1. Atualize o esquema do banco de dados. Consulte a documentação do tipo de banco de dados para ver qual é a ferramenta que você precisa usar para conseguir isso.

   Para obter mais informações sobre como o Oak lida com atualizações de esquema, consulte [esta página no site](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade)do Apache.

1. Prossiga com a atualização do AEM.

## Excluir usuários que possam prejudicar a atualização {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>Esta tarefa de manutenção pré-atualização só é necessária se:
>
>* Você está atualizando de versões do AEM anteriores ao AEM 6.3
>* Você encontra qualquer um dos erros mencionados abaixo durante a atualização.
>



Há casos excepcionais em que os usuários do serviço podem acabar sendo marcados incorretamente como usuários comuns em versões anteriores do AEM.

Se isso acontecer, a atualização falhará com uma mensagem como esta:

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

Para contornar esse problema, certifique-se de fazer o seguinte:

1. Desanexar a instância do tráfego de produção
1. Crie um backup dos usuários que causam o problema. Isso pode ser feito por meio do Gerenciador de pacotes. Para obter mais informações, consulte [Como trabalhar com pacotes.](/help/sites-administering/package-manager.md)
1. Exclua os usuários que estão causando o problema. Abaixo está uma lista de usuários que podem estar incluídos nesta categoria:

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## Girar arquivos de registro {#rotate-log-files}

Recomendamos o arquivamento dos arquivos de registro atuais antes de iniciar a atualização. Isso facilitará o monitoramento e a verificação dos arquivos de registro durante e após a atualização para identificar e resolver quaisquer problemas que possam ocorrer.
