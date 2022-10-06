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
ht-degree: 87%

---

# Administração de instâncias do fluxo de trabalho{#administering-workflow-instances}

O console do fluxo de trabalho fornece várias ferramentas para administrar instâncias do fluxo de trabalho e garantir que elas estejam em execução conforme esperado.

>[!NOTE]
>
>O [Console JMX](/help/sites-administering/jmx-console.md#workflow-maintenance) O fornece operações adicionais de manutenção de workflow.

Há vários consoles disponíveis para administrar seus fluxos de trabalho. Use a [navegação global](/help/sites-authoring/basic-handling.md#global-navigation) para abrir o painel **Ferramentas** e selecione **Fluxo de trabalho**:

* **Modelos**: gerenciar definições de fluxo de trabalho
* **Instâncias**: exibir e gerenciar instâncias de fluxos de trabalho em execução
* **Iniciadores**: gerenciar o modo como os fluxos de trabalho devem ser inicializados
* **Arquivo**: exibir o histórico de fluxos de trabalho que foram concluídos com sucesso
* **Falhas**: exibir o histórico de fluxos de trabalho que foram concluídos com erros
* **Atribuição automática**: configurar a atribuição automática de fluxos de trabalho aos modelos

## Monitorar o status de instâncias de fluxo de trabalho {#monitoring-the-status-of-workflow-instances}

1. Usando a navegação, selecione **Ferramentas** e, em seguida, **Fluxo de trabalho**.
1. Selecione **Instâncias** para exibir a lista de instâncias de fluxo de trabalho em andamento.

   ![wf-96](assets/wf-96.png)


## Pesquisar instâncias de fluxo de trabalho {#search-workflow-instances}

1. Usando a navegação, selecione **Ferramentas** e, em seguida, **Fluxo de trabalho**.
1. Selecione **Instâncias** para exibir a lista de instâncias de fluxo de trabalho em andamento. No painel superior, no canto esquerdo, selecione **Filtros**. Como alternativa, você pode pressionar as teclas Alt+1. A seguinte caixa de diálogo é exibida:

   ![wf-99-1](assets/wf-99-1.png)

1. Na caixa de diálogo Filtro, selecione os critérios de pesquisa do fluxo de trabalho. Você pode pesquisar com base nessas entradas:

   * Caminho da carga: selecionar um caminho específico
   * Modelo de fluxo de trabalho: selecionar um modelo de fluxo de trabalho
   * Destinatário: selecionar um destinatário do fluxo de trabalho
   * Tipo: tarefa, item do fluxo de trabalho ou falha do fluxo de trabalho
   * Status da tarefa: ativo, concluído ou encerrado
   * Onde estou: proprietário AND destinatário, somente proprietário, somente destinatário
   * Data inicial: data inicial anterior ou posterior a uma data especificada
   * Data final: Data final anterior ou posterior a uma data especificada
   * Data de vencimento: data de vencimento anterior ou posterior a uma data especificada
   * Data atualizada: data atualizada anterior ou posterior a uma data especificada

## Suspensão, retomada e encerramento de uma instância de fluxo de trabalho {#suspending-resuming-and-terminating-a-workflow-instance}

1. Usando a navegação, selecione **Ferramentas** e, em seguida, **Fluxo de trabalho**.
1. Selecione **Instâncias** para exibir a lista de instâncias de fluxo de trabalho em andamento.

   ![wf-96-1](assets/wf-96-1.png)

1. Selecione um item específico e use **Encerrar**, **Suspender** ou **Retomar**, conforme adequado; é necessária uma confirmação e/ou outros pormenores:

   ![wf-97-1](assets/wf-97-1.png)

## Visualização de fluxos de trabalho arquivados {#viewing-archived-workflows}

1. Usando a navegação, selecione **Ferramentas** e, em seguida, **Fluxo de trabalho**.
1. Selecione **Arquivo** para exibir a lista de instâncias de fluxo de trabalho concluídas com sucesso.

   ![wf-98](assets/wf-98.png)

   >[!NOTE]
   >
   >O status interrompido é considerado um encerramento bem-sucedido, pois ocorre como resultado da ação do usuário; por exemplo:
   >
   >* o uso da ação **Encerrar**
   >* quando uma página que está sujeita a um fluxo de trabalho é excluída (à força), o fluxo de trabalho é encerrado


1. Selecione um item específico e **Abra o histórico** para ver mais detalhes:

   ![wf-99](assets/wf-99.png)

## Correção de falhas na instância do fluxo de trabalho {#fixing-workflow-instance-failures}

Quando um fluxo de trabalho falha, o AEM fornece o console **Falhas**, que permite investigar e tomar as medidas apropriadas após tratar a causa original:

* **Detalhes da falha**
Abre uma janela para mostrar a  
**Mensagem de falha**, **Etapa** e **Pilha de falhas**.

* **Abrir histórico**
Mostra detalhes do histórico do fluxo de trabalho.

* **Repetir etapa** Executa a instância do componente Etapa do script novamente. Use o comando Repetir etapa após corrigir a causa do erro original. Por exemplo, repita a etapa depois de corrigir um erro no script que a Etapa do processo executa.
* **Encerrar** Encerre o fluxo de trabalho se o erro tiver causado uma situação irreversível para o fluxo de trabalho. Por exemplo, o workflow pode depender de condições ambientais, como informações no repositório que não são mais válidas para a instância do workflow.
* **Encerrar e repetir** Semelhante a **Encerrar**, exceto que uma nova instância de fluxo de trabalho é iniciada usando a carga, o título e a descrição originais.

Para investigar falhas e, em seguida, retomar ou encerrar o fluxo de trabalho, use as seguintes etapas:

1. Usando a navegação, selecione **Ferramentas** e, em seguida, **Fluxo de trabalho**.
1. Selecione **Falhas** para exibir a lista de instâncias de fluxo de trabalho que não foram concluídas com sucesso.
1. Selecione um item específico e, em seguida, a ação apropriada:

   ![wf-47](assets/wf-47.png)

## Limpeza regular de instâncias de fluxo de trabalho {#regular-purging-of-workflow-instances}

Minimizar o número de instâncias de fluxo de trabalho aumenta o desempenho do motor de workflow. Portanto, você pode remover regularmente do repositório as instâncias de fluxo de trabalho concluídas ou em execução.

Configure a **Configuração de limpeza de fluxos de trabalho do Adobe Granite** para remover instâncias de fluxo de trabalho de acordo com sua idade e status. Você também pode remover as instâncias de fluxo de trabalho de todos os modelos ou de um modelo específico.

Você também pode criar várias configurações do serviço para remover as instâncias de fluxo de trabalho que satisfaçam critérios diferentes. Por exemplo, crie uma configuração que remova as instâncias de um modelo de fluxo de trabalho específico quando elas estiverem em execução por muito mais tempo do que o esperado. Crie outra configuração que remova todos os fluxos de trabalho concluídos após um determinado número de dias para minimizar o tamanho do repositório.

Para configurar o serviço, você pode usar o [Console da Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ou [adicionar uma configuração OSGi ao repositório](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). A tabela a seguir descreve as propriedades necessárias para qualquer método.

>[!NOTE]
>
>Para adicionar a configuração ao repositório, o PID do serviço é:
>
>`com.adobe.granite.workflow.purge.Scheduler`
>
>Como o serviço é de fábrica, o nome do nó `sling:OsgiConfig` requer um sufixo identificador. Por exemplo:
>
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>Nome da propriedade (console da Web)</th>
   <th>Nome da propriedade OSGi</th>
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
   <td><p>O status das instâncias de fluxo de trabalho a serem removidas. Os seguintes valores são válidos:</p>
    <ul>
     <li>CONCLUÍDO: as instâncias de fluxo de trabalho concluídas são removidas.</li>
     <li>EM EXECUÇÃO: as instâncias de fluxo de trabalho em execução são removidas.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modelos a remover</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>A ID dos modelos de fluxo de trabalho a serem removidos. A ID é o caminho para o nó do modelo, por exemplo:<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> Não especifique nenhum valor para remover instâncias de todos os modelos de fluxo de trabalho.</p> <p>Para especificar vários modelos, clique no botão + no console da Web. </p> </td>
  </tr>
  <tr>
   <td>Idade do fluxo de trabalho</td>
   <td>scheduledpurge.daysold</td>
   <td>A idade das instâncias de fluxo de trabalho a serem removidas, em dias.</td>
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

| Nome da propriedade (console da Web) | Nome da propriedade OSGi |
|---|---|
| Tamanho máximo da consulta da caixa de entrada | granite.workflow.inboxQuerySize |

## Uso de variáveis de fluxo de trabalho para armazenamentos de dados de propriedade do cliente {#using-workflow-variables-customer-datastore}

Os dados processados por fluxos de trabalho são armazenados no armazenamento fornecido pela Adobe (JCR). Esses dados podem ser de natureza sensível. É possível salvar todos os metadados/dados definidos pelo usuário em seu próprio armazenamento gerenciado, em vez de usar o armazenamento fornecido pela Adobe. Essas seções descrevem como configurar essas variáveis para armazenamento externo.

### Definir o modelo para usar o armazenamento externo de metadados {#set-model-for-external-storage}

No nível do modelo de fluxo de trabalho, um sinalizador é fornecido para indicar que o modelo e suas instâncias de tempo de execução têm acesso ao armazenamento externo de metadados. As variáveis de fluxo de trabalho não serão mantidas no JCR para as instâncias de fluxo de trabalho cujos modelos foram marcados para armazenamento externo.

A propriedade *userMetadataPersistenceEnabled* será armazenada no *nó jcr:content* do modelo de fluxo de trabalho. Esse sinalizador será mantido nos metadados do fluxo de trabalho como *cq:userMetaDataCustomPersistenceEnabled*.

A ilustração abaixo mostra como definir o sinalizador em um fluxo de trabalho.

![workflow-externalize-config](assets/workflow-externalize-config.png)

### APIs de metadados no armazenamento externo {#apis-for-metadata-external-storage}

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
