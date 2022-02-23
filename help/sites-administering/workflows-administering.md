---
title: Administração de instâncias do fluxo de trabalho
seo-title: Administering Workflow Instances
description: Saiba como administrar instâncias de fluxo de trabalho.
seo-description: Lear how to administer Workflow Instances.
uuid: 81e53ef5-fe62-4ed4-b2d4-132aa986d5aa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d9c96e7f-9416-48e1-a6af-47384f7bee92
exl-id: 90923d39-3ac5-4028-976c-d011f0404476
source-git-commit: 8b4459c69b73159ce5afd819dfb772df5c51cd16
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 0%

---

# Administração de instâncias do fluxo de trabalho{#administering-workflow-instances}

O console Fluxo de trabalho fornece várias ferramentas para administrar instâncias do fluxo de trabalho, para garantir que elas estejam em execução conforme esperado.

>[!NOTE]
>
>O [Console JMX](/help/sites-administering/jmx-console.md#workflow-maintenance) O fornece operações adicionais de manutenção de workflow.

Há vários consoles disponíveis para administrar seus fluxos de trabalho. Use o [navegação global](/help/sites-authoring/basic-handling.md#global-navigation) para abrir o **Ferramentas** painel e selecione **Fluxo de trabalho**:

* **Modelos**: Gerenciar definições de fluxo de trabalho
* **Instâncias**: Exibir e gerenciar a execução de instâncias de fluxo de trabalho
* **Lançadores**: Gerenciar como os workflows devem ser iniciados
* **Arquivar**: Exibir o histórico de fluxos de trabalho concluídos com êxito
* **Falhas**: Exibir o histórico de fluxos de trabalho concluídos com erros
* **Atribuição automática**: Configurar workflows de atribuição automática para modelos

## Monitorar o status de instâncias de fluxo de trabalho {#monitoring-the-status-of-workflow-instances}

1. Usar navegação selecione **Ferramentas**, em seguida **Fluxo de trabalho**.
1. Selecionar **Instâncias** para exibir a lista de instâncias de fluxo de trabalho em andamento.

   ![wf-96](assets/wf-96.png)


## Pesquisar instâncias do fluxo de trabalho {#search-workflow-instances}

1. Usar navegação selecione **Ferramentas**, em seguida **Fluxo de trabalho**.
1. Selecionar **Instâncias** para exibir a lista de instâncias de fluxo de trabalho em andamento. No painel superior, no canto esquerdo, selecione **Filtros**. Como alternativa, você pode usar os pressionamentos de tecla alt+1. A seguinte caixa de diálogo é exibida:

   ![wf-99-1](assets/wf-99-1.png)

1. Na caixa de diálogo Filtro , selecione os critérios de pesquisa do fluxo de trabalho. Você pode pesquisar com base nessas entradas:

   * Caminho da carga: Selecionar um caminho específico
   * Modelo de fluxo de trabalho: Selecionar um modelo de fluxo de trabalho
   * Destinatário: Selecionar um Destinatário do fluxo de trabalho
   * Tipo: Tarefa, item de fluxo de trabalho ou falha de fluxo de trabalho
   * Status da tarefa: Ativo, concluído ou encerrado
   * Onde Estou: Proprietário E Destinatário, somente Proprietário, Somente Destinatário
   * Data de início: Data inicial antes ou depois de uma data especificada
   * Data final: Data final antes ou depois de uma data especificada
   * Data de Vencimento: Data de vencimento antes ou depois de uma data especificada
   * Data de atualização: Data atualizada antes ou depois de uma data especificada

## Suspensão, retomada e Encerramento de uma Instância de Fluxo de Trabalho {#suspending-resuming-and-terminating-a-workflow-instance}

1. Usar navegação selecione **Ferramentas**, em seguida **Fluxo de trabalho**.
1. Selecionar **Instâncias** para exibir a lista de instâncias de fluxo de trabalho em andamento.

   ![wf-96-1](assets/wf-96-1.png)

1. Selecione um item específico e use **Encerrar**, **Suspender** ou **Retomar**, conforme adequado; é necessária confirmação e/ou mais pormenores:

   ![wf-97-1](assets/wf-97-1.png)

## Visualização de fluxos de trabalho arquivados {#viewing-archived-workflows}

1. Usar navegação selecione **Ferramentas**, em seguida **Fluxo de trabalho**.
1. Selecionar **Arquivar** para exibir a lista de instâncias de fluxo de trabalho concluídas com êxito.

   ![wf-98](assets/wf-98.png)

   >[!NOTE]
   >
   >O status abort é considerado como uma terminação bem-sucedida, pois ocorre como resultado da ação do usuário; por exemplo:
   >
   >* utilização do **Encerrar** ação
   >* quando uma página, que está sujeita a um fluxo de trabalho, é (forçar) excluída, o fluxo de trabalho será encerrado


1. Selecione um item específico e **Abrir Histórico** para ver mais detalhes:

   ![wf-99](assets/wf-99.png)

## Correção de falhas na instância do fluxo de trabalho {#fixing-workflow-instance-failures}

Quando um fluxo de trabalho falhar, o AEM fornece a variável **Falhas** console para permitir investigar e tomar as medidas apropriadas assim que a causa original for tratada:

* **Detalhes da falha**
Abre uma janela para mostrar a variável 
**Mensagem de falha**, **Etapa** e **Pilha de falhas**.

* **Abrir Histórico**
Mostra detalhes do histórico do fluxo de trabalho.

* **Etapa de nova tentativa** Executa a instância do componente Etapa do script novamente. Use o comando Repetir etapa após corrigir a causa do erro original. Por exemplo, tente novamente a etapa depois de corrigir um erro no script que a Etapa do processo executa.
* **Encerrar** Encerre o fluxo de trabalho se o erro tiver causado uma situação irreversível para o fluxo de trabalho. Por exemplo, o workflow pode depender de condições ambientais, como informações no repositório que não são mais válidas para a instância do workflow.
* **Encerrar e Tentar Novamente** Semelhante a **Encerrar** exceto que uma nova instância de workflow é iniciada usando a carga, o título e a descrição originais.

Para investigar falhas e, em seguida, retomar ou encerrar o fluxo de trabalho depois, use as seguintes etapas:

1. Usar navegação selecione **Ferramentas**, em seguida **Fluxo de trabalho**.
1. Selecionar **Falhas** para exibir a lista de instâncias de fluxo de trabalho que não foram concluídas com êxito.
1. Selecione um item específico e, em seguida, a ação apropriada:

   ![wf-47](assets/wf-47.png)

## Limpeza regular de instâncias de fluxo de trabalho {#regular-purging-of-workflow-instances}

Minimizar o número de instâncias de fluxo de trabalho aumenta o desempenho do mecanismo de fluxo de trabalho, para que você possa limpar regularmente as instâncias de fluxo de trabalho concluídas ou em execução do repositório.

Configurar **Configuração de limpeza de fluxo de trabalho do Adobe Granite** para limpar instâncias do fluxo de trabalho de acordo com sua idade e status. Você também pode limpar instâncias de fluxo de trabalho de todos os modelos ou de um modelo específico.

Você também pode criar várias configurações do serviço para limpar instâncias de fluxo de trabalho que satisfaçam critérios diferentes. Por exemplo, crie uma configuração que limpe as instâncias de um modelo de fluxo de trabalho específico quando elas estiverem em execução por muito mais tempo do que o tempo esperado. Crie outra configuração que elimine todos os workflows concluídos após um determinado número de dias para minimizar o tamanho do repositório.

Para configurar o serviço, você pode usar o [Console da Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ou [adicionar uma configuração OSGi ao repositório](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). A tabela a seguir descreve as propriedades necessárias para qualquer método.

>[!NOTE]
>
>Para adicionar a configuração ao repositório, o PID do serviço é:
>
>`com.adobe.granite.workflow.purge.Scheduler`
>
>Como o serviço é de fábrica, o nome da variável `sling:OsgiConfig` o nó requer um sufixo identificador, por exemplo:
>
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>Nome da propriedade (Console da Web)</th>
   <th>Nome da Propriedade OSGi</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>Nome da tarefa</td>
   <td>scheduledpurge.name</td>
   <td>Um nome descritivo para a limpeza agendada.</td>
  </tr>
  <tr>
   <td>Status do fluxo de trabalho</td>
   <td>scheduledpurge.workflowStatus</td>
   <td><p>O status das instâncias do fluxo de trabalho a serem removidas. Os seguintes valores são válidos:</p>
    <ul>
     <li>CONCLUÍDO: As instâncias de fluxo de trabalho concluídas são removidas.</li>
     <li>EM EXECUÇÃO: A execução de instâncias de fluxo de trabalho é eliminada.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modelos a serem limpos</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>A ID dos modelos de fluxo de trabalho a serem limpos. A ID é o caminho para o nó do modelo, por exemplo:<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> Especifique nenhum valor para limpar instâncias de todos os modelos de fluxo de trabalho.</p> <p>Para especificar vários modelos, clique no botão + no Console da Web. </p> </td>
  </tr>
  <tr>
   <td>Idade do fluxo de trabalho</td>
   <td>scheduledpurge.daysold</td>
   <td>A idade das instâncias do fluxo de trabalho a serem removidas, em dias.</td>
  </tr>
 </tbody>
</table>

## Configuração do tamanho máximo da caixa de entrada {#setting-the-maximum-size-of-the-inbox}

Você pode definir o tamanho máximo da caixa de entrada configurando o **Serviço de fluxo de trabalho do Adobe Granite**, usando o [Console da Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ou [adicionar uma configuração OSGi ao repositório](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). A tabela a seguir descreve a propriedade configurada para qualquer método.

>[!NOTE]
>
>Para adicionar a configuração ao repositório, o PID do serviço é:
>
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| Nome da propriedade (Console da Web) | Nome da Propriedade OSGi |
|---|---|
| Tamanho máximo da consulta da caixa de entrada | granite.workflow.inboxQuerySize |

## Uso de variáveis de fluxo de trabalho para armazenamentos de dados de propriedade do cliente {#using-workflow-variables-customer-datastore}

Os dados processados por workflows são armazenados no JCR (Adobe provided storage, armazenamento fornecido pelo JCR). Esses dados podem ser confidenciais por natureza. Você pode salvar todos os metadados/dados definidos pelo usuário em seu próprio armazenamento gerenciado, em vez do armazenamento fornecido pelo Adobe. Essas seções descrevem como configurar essas variáveis para armazenamento externo.

### Definir o modelo para usar o armazenamento externo de metadados {#set-model-for-external-storage}

No nível do modelo de fluxo de trabalho, é fornecido um sinalizador para indicar que o modelo (e suas instâncias de tempo de execução) tem armazenamento externo de metadados. As variáveis de workflow não serão persistentes no JCR para as instâncias de workflow dos modelos marcados para armazenamento externo.

A propriedade *userMetadataPersistenceEnabled* será armazenado no *jcr:content node* do modelo de fluxo de trabalho. Esse sinalizador será mantido nos metadados do workflow como *cq:userMetaDataCustomPersistenceEnabled*.

A ilustração abaixo mostra ter que definir o sinalizador em um workflow.

![workflow-externalize-config](assets/workflow-externalize-config.png)

### APIs para metadados em armazenamento externo {#apis-for-metadata-external-storage}

Para armazenar as variáveis externamente, você deve implementar as APIs que o fluxo de trabalho expõe.

UserMetaDataPersistenceContext

Os exemplos a seguir mostram como usar a API.

```
@ProviderType
public interface UserMetaDataPersistenceContext {
 
    /**
     * Gets the workflow for persistence
     * @return workflow
     */
    Workflow getWorkflow();
 
    /**
     * Gets the workflow id for persistence
     * @return workflowId
     */
    String getWorkflowId();
 
    /**
     * Gets the user metadata persistence id
     * @return userDataId
     */
    String getUserDataId();
}
```

UserMetaDataPersistenceProvider

```
/**
 * This provider can be implemented to store the user defined workflow-data metadata in a custom storage location
 */
@ConsumerType
public interface UserMetaDataPersistenceProvider {
 
   /**
    * Retrieves the metadata using a unique identifier
    * @param userMetaDataPersistenceContext
    * @param metaDataMap of user defined workflow data metaData
    * @throws WorkflowException
    */
   void get(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
   /**
    * Stores the given metadata to the custom storage location
    * @param userMetaDataPersistenceContext
    * @param metaDataMap metadata map
    * @return the unique identifier that can be used to retrieve metadata. If null is returned, then workflowId is used.
    * @throws WorkflowException
    */
   String put(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
} 
```
