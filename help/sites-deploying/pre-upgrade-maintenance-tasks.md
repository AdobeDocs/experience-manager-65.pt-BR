---
title: Tarefas de Manutenção de Pré-Atualização
description: Saiba mais sobre as tarefas de pré-atualização recomendadas para o AEM.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: 37d4aee4-15eb-41ab-ad71-dfbd5c7910f8
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 0%

---

# Tarefas de Manutenção de Pré-Atualização{#pre-upgrade-maintenance-tasks}

Antes de iniciar a atualização, é importante seguir estas tarefas de manutenção para garantir que o sistema esteja pronto e possa ser revertido caso ocorram problemas:

* [Garantir espaço suficiente em disco](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [Fazer backup completo do AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [Fazer backup de alterações em /etc](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [Gerar o arquivo quickstart.properties](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [Configurar a limpeza do fluxo de trabalho e do log de auditoria](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [Instalar, Configurar e Executar as Tarefas de Pré-Atualização](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [Desativar módulos de logon personalizados](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [Remover Atualizações Do Diretório /install](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [Interromper Quaisquer Instâncias De Modo De Espera Por Frio](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [Desabilitar Trabalhos Agendados Personalizados](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [Executar limpeza de revisão offline](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [Executar coleta de lixo do armazenamento de dados](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [Fazer Upgrade do Esquema de Banco de Dados, Se Necessário](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [Excluir usuários que podem dificultar a atualização](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [Girar arquivos de registro](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## Garantir espaço suficiente em disco {#ensure-sufficient-disk-space}

Ao executar a atualização, além das atividades de atualização de conteúdo e código, uma migração de repositório deve ser executada. A migração cria uma cópia do repositório no novo formato TAR de segmento. Como resultado, é necessário espaço em disco suficiente para manter uma segunda versão do repositório, possivelmente maior.

## Fazer backup completo do AEM {#fully-back-up-aem}

O backup do AEM deve ser concluído antes do início da atualização. Faça backup do repositório, da instalação do aplicativo, do armazenamento de dados e das instâncias Mongo, se aplicável. Para obter mais informações sobre como fazer backup e restaurar uma instância do AEM, consulte [Backup e Restauração](/help/sites-administering/backup-and-restore.md).

## Fazer backup de alterações em /etc {#backup-changes-etc}

O processo de atualização faz um bom trabalho de manutenção e mesclagem do conteúdo e das configurações existentes nos caminhos do `/apps` e do `/libs` no repositório. Para alterações feitas no caminho `/etc`, incluindo configurações do Context Hub, geralmente é necessário reaplicar essas alterações após a atualização. Embora a atualização faça uma cópia de backup de todas as alterações que não podem ser mescladas no `/var`, a Adobe recomenda que você faça backup dessas alterações manualmente antes de iniciar a atualização.

## Gerar o arquivo quickstart.properties {#generate-quickstart-properties}

Ao iniciar o AEM do arquivo jar, um arquivo `quickstart.properties` é gerado em `crx-quickstart/conf`. Se o AEM só tiver sido iniciado com o script de inicialização no passado, esse arquivo não estará presente e a atualização falhará. Verifique a existência desse arquivo e reinicie o AEM a partir do arquivo jar, se ele não estiver presente.

## Configurar a limpeza do fluxo de trabalho e do log de auditoria {#configure-wf-audit-purging}

As tarefas `WorkflowPurgeTask` e `com.day.cq.audit.impl.AuditLogMaintenanceTask` exigem configurações OSGi separadas e não podem funcionar sem elas. Se eles falharem durante a execução da tarefa de pré-atualização, a falta de configurações será o motivo mais provável. Portanto, adicione configurações OSGi para essas tarefas ou remova-as completamente da lista de tarefas de otimização de pré-atualização se não quiser executá-las. A documentação para configurar tarefas de limpeza de fluxo de trabalho pode ser encontrada em [Administrando Instâncias de Fluxo de Trabalho](/help/sites-administering/workflows-administering.md) e a configuração da tarefa de manutenção de log de auditoria pode ser encontrada em [Manutenção de Log de Auditoria no AEM 6](/help/sites-administering/operations-audit-log.md).

## Instalar, Configurar e Executar as Tarefas de Pré-Atualização {#install-configure-run-pre-upgrade-tasks}

Devido ao nível de personalização permitido pelo AEM, os ambientes geralmente não seguem uma maneira uniforme de executar atualizações. Assim, a criação de um procedimento padronizado para atualizações é um processo difícil.

Em versões anteriores, também era difícil para atualizações do AEM que eram interrompidas ou que não eram retomadas com segurança. Esse problema levou a situações em que era necessário reiniciar o procedimento de atualização completo ou em que atualizações com defeito eram realizadas sem disparar avisos.

Para resolver esses problemas, a Adobe adicionou vários aprimoramentos ao processo de atualização, tornando-o mais resiliente e fácil de usar. As tarefas de manutenção pré-atualização que antes tinham de ser realizadas manualmente estão sendo otimizadas e automatizadas. Além disso, foram adicionados relatórios pós-atualização para que o processo possa ser totalmente analisado, na esperança de que quaisquer problemas sejam encontrados mais facilmente.

Atualmente, as tarefas de manutenção pré-atualização estão distribuídas por várias interfaces que são parcial ou totalmente executadas manualmente. A otimização de manutenção de pré-atualização introduzida no AEM 6.3 permite uma maneira unificada de acionar essas tarefas e inspecionar seus resultados sob demanda.

Todas as tarefas incluídas na etapa de otimização de pré-atualização são compatíveis com todas as versões do AEM 6.0 em diante.

### Como configurar {#how-to-set-it-up}

No AEM 6.3 e versões posteriores, as tarefas de otimização de manutenção de pré-atualização são incluídas no jar de início rápido.

<!-- URLs below are all 404s. This content should probably be removed because it is entirely obsolete.

If you are upgrading from an older version of AEM 6, they are made available through separate packages that you can download from the Package Manager.

You can find the packages at these locations:

* [For upgrading from AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [For upgrading from AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [For upgrading from AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62) -->

### Como usá-lo {#how-to-use-it}

O componente OSGI `PreUpgradeTasksMBean` vem pré-configurado com uma lista de tarefas de manutenção de pré-atualização que podem ser executadas todas de uma vez. Você pode configurar as tarefas seguindo o procedimento abaixo:

1. Vá para o Console da Web navegando até *https://serveraddress:serverport/system/console/configMgr*

1. Procure por &quot;**tarefas de pré-atualização**&quot; e clique no primeiro componente correspondente. O nome completo do componente é `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

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
   <td>Executa a marcação e a varredura. Para armazenamentos de dados compartilhados, remova esta etapa e execute o <br /> manualmente ou prepare adequadamente as instâncias antes da execução.</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>É necessário configurar o OSGi de configuração de limpeza de fluxo de trabalho do Adobe Granite antes de executar.</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>Para instâncias TarMK no AEM 6.0 para 6.2, execute manualmente a Limpeza de revisão offline.</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>É necessário definir a configuração OSGi do Agendador de limpeza de log de auditoria antes de executar.</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>O `DataStoreGarbageCollectionTask` chama uma operação de Coleta de Lixo do Datastore com a fase de marcação e varredura, se usada. Para implantações que usam um armazenamento de dados compartilhado, reconfigure-o corretamente ou prepare a instância para evitar a exclusão de itens referenciados por outra instância. Esse processo pode exigir a execução da fase de marcação manualmente em todas as instâncias antes de acionar essa tarefa de pré-atualização.

### Configuração padrão das verificações de integridade de pré-atualização {#default-configuration-of-the-pre-upgrade-health-checks}

O componente OSGI `PreUpgradeTasksMBeanImpl` vem pré-configurado com uma lista de marcas de verificação de integridade de pré-atualização a serem executadas quando o método `runAllPreUpgradeHealthChecks` for chamado:

* **sistema** - a marca usada pelas verificações de integridade de manutenção do Granite

* **pré-atualização** - uma marca personalizada que pode ser adicionada a todas as verificações de integridade que você pode definir para execução antes de uma atualização

A lista é editável. Você pode usar os botões mais **(+)** e menos **(-)** além das marcas para adicionar mais marcas personalizadas ou remover as padrão.

**Métodos MBean**

A funcionalidade do bean gerenciado pode ser acessada usando o [Console JMX](/help/sites-administering/jmx-console.md).

Você pode acessar os MBeans ao:

1. Indo para o Console JMX em *https://serveraddress:serverport/system/console/jmx*
1. Pesquise por **PreUpgradeTasks** e clique no resultado

1. Selecione qualquer método na seção **Operações** e selecione **Chamar** na janela a seguir.

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
   <td>INFO</td>
   <td>Exibe a lista dos nomes das tags de verificação de integridade pré-atualização.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeTasks()</code></td>
   <td>AÇÃO</td>
   <td>Executa todas as tarefas de manutenção de pré-atualização da lista.</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>AÇÃO</td>
   <td>Executa a tarefa de manutenção de pré-atualização com o nome fornecido como o parâmetro.</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Verifica se a tarefa <code>runAllPreUpgradeTasksmaintenance</code> está em execução.</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Verifica se alguma tarefa de manutenção de pré-atualização está em execução e <br /> retorna uma matriz contendo os nomes das tarefas em execução no momento.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>AÇÃO</td>
   <td>Exibe o tempo de execução exato da tarefa de manutenção de pré-atualização com o nome fornecido como parâmetro.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>AÇÃO</td>
   <td>Exibe o último estado de execução da tarefa de manutenção de pré-atualização com o nome fornecido como o parâmetro.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>AÇÃO</td>
   <td><p>Executa todas as verificações de integridade de pré-atualização e salva seu status em um arquivo chamado <code>preUpgradeHCStatus.properties</code> que esteja no caminho do sling home. Se o parâmetro <code>shutDownOnSuccess</code> estiver definido como <code>true</code>, a instância do AEM será desligada, mas somente se todas as verificações de integridade anteriores à atualização tiverem um status OK.</p> <p>O arquivo de propriedades é usado como uma pré-condição para qualquer atualização futura<br /> e o processo de atualização é interrompido se a execução da verificação de integridade de pré-atualização<br /> falhar. Se quiser ignorar o resultado das verificações de integridade de pré-atualização <br /> e iniciar a atualização de qualquer maneira, você poderá excluir o arquivo.</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>AÇÃO</td>
   <td>Lista todos os pacotes importados que não são mais satisfeitos quando <br /> é atualizado para a versão do AEM especificada. A versão de destino do AEM deve ser <br /> fornecida como parâmetro.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Os métodos MBean podem ser chamados por meio de:
>
>* A console JMX
>* Qualquer aplicativo externo que se conecta ao JMX
>* cURL
>

## Desativar módulos de logon personalizados {#disable-custom-login-modules}

>[!NOTE]
>
>Esta etapa só será necessária se você estiver atualizando de uma versão do AEM 5. Ele pode ser ignorado totalmente para atualizações de versões mais antigas do AEM 6.

A forma como os `LoginModules` personalizados são configurados para autenticação no nível do repositório mudou radicalmente no Apache Oak.

Nas versões do AEM que usavam a configuração do CRX2, ela era colocada no arquivo `repository.xml`, enquanto do AEM 6 em diante ela era feita no serviço de fábrica de configuração do Apache Felix JAAS através do console da Web.

Portanto, todas as configurações existentes precisarão ser desativadas e recriadas para o Apache Oak após a atualização.

Para desabilitar os módulos personalizados definidos na configuração JAAS de `repository.xml`, edite a configuração para usar o `LoginModule` padrão, como no exemplo a seguir:

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
>Para obter mais informações, consulte [Autenticação com Módulo de Logon Externo](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).
>
>Para obter um exemplo da configuração `LoginModule` no AEM 6, consulte [Configurando LDAP com AEM 6](/help/sites-administering/ldap-config.md).

## Remover Atualizações Do Diretório /install {#remove-updates-install-directory}

>[!NOTE]
>
>Remova pacotes somente do diretório crx-quickstart/install APÓS desligar a instância do AEM. Esta etapa é uma das últimas antes de iniciar o procedimento de atualização no local.

Remova service packs, pacotes de recursos ou hotfixes que foram implantados por meio do diretório `crx-quickstart/install` no sistema de arquivos local. Isso impede a instalação inadvertida de hotfixes e service packs antigos na nova versão do AEM, após a conclusão da atualização.

## Interromper Quaisquer Instâncias De Modo De Espera Por Frio {#stop-tarmk-coldstandby-instance}

Se estiver usando a espera a frio do TarMK, interrompa todas as instâncias a frio da espera. Isso garante uma maneira eficiente de voltar a ficar online em caso de problemas na atualização. Depois que o upgrade for concluído com sucesso, as instâncias off-line deverão ser recriadas a partir das instâncias principais atualizadas.

## Desabilitar Trabalhos Agendados Personalizados {#disable-custom-scheduled-jobs}

Desative todos os trabalhos agendados OSGi incluídos no código do aplicativo.

## Executar limpeza de revisão offline {#execute-offline-revision-cleanup}

>[!NOTE]
>
>Esta etapa só é necessária para instalações TarMK

Se estiver usando TarMK, você deve executar a Limpeza de revisão offline antes da atualização. Isso torna a etapa de migração do repositório e as tarefas de atualização subsequentes muito mais rápidas e ajuda a garantir que a Limpeza de revisão online possa ser executada com êxito após a conclusão da atualização. Para obter informações sobre como executar a Limpeza de Revisão Offline, consulte [Execução da Limpeza de Revisão Offline](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup).

## Executar coleta de lixo do armazenamento de dados {#execute-datastore-garbage-collection}

>[!NOTE]
>
>Esta etapa só é necessária para instâncias que executam o crx3

Depois de executar a limpeza de revisão nas instâncias do CRX3, você deve executar a Coleta de lixo do armazenamento de dados para remover os blobs não referenciados no armazenamento de dados. Para obter instruções, consulte a documentação em [Coleta de lixo do armazenamento de dados](/help/sites-administering/data-store-garbage-collection.md).

## Fazer Upgrade do Esquema de Banco de Dados, Se Necessário {#upgrade-the-database-schema-if-needed}

Normalmente, a pilha subjacente do Apache Oak que o AEM usa para persistência cuida da atualização do esquema do banco de dados, se necessário.

No entanto, podem surgir casos em que o esquema não pode ser atualizado automaticamente. Esses casos são, em sua maioria, ambientes de alta segurança nos quais o banco de dados é executado sob um usuário com privilégios limitados. Se essa situação ocorrer, o AEM continuará a usar o esquema antigo.

Para evitar que esse cenário aconteça, atualize o esquema fazendo o seguinte:

1. Desligue a instância do AEM que deve ser atualizada.
1. Atualize o esquema do banco de dados. Consulte a documentação do tipo de banco de dados para ver quais ferramentas são necessárias para obter o resultado.

   Para obter mais informações sobre como o Oak lida com atualizações de esquema, consulte [esta página no site do Apache](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade).

1. Continue atualizando o AEM.

## Excluir usuários que podem dificultar a atualização {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>Essa tarefa de manutenção pré-atualização só será necessária se:
>
>* Você está atualizando de versões do AEM anteriores ao AEM 6.3
>* Você encontra qualquer um dos erros mencionados abaixo durante a atualização.
>

Há casos excepcionais em que os usuários de serviço podem acabar sendo marcados incorretamente como usuários regulares em uma versão mais antiga do AEM.

Se tal situação ocorrer, a atualização falhará com uma mensagem como a seguinte:

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

Para contornar esse problema, faça o seguinte:

1. Desanexar a instância do tráfego de produção
1. Crie um backup de um ou mais usuários que causam o problema. Você pode fazer essa tarefa por meio do Gerenciador de pacotes. Para obter mais informações, consulte [Como trabalhar com pacotes.](/help/sites-administering/package-manager.md)
1. Exclua um ou mais usuários que estão causando o problema. Veja abaixo uma lista de usuários que podem se enquadrar nesta categoria:

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## Girar arquivos de registro {#rotate-log-files}

A Adobe recomenda arquivar seus arquivos de log atuais antes de iniciar a atualização. Isso facilita a monitoração e a varredura dos arquivos de registro durante e após a atualização para identificar e resolver quaisquer problemas que possam ocorrer.
