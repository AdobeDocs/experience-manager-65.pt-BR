---
title: Recursos do Monitoring Server usando a console JMX
seo-title: Monitoring Server Resources Using the JMX Console
description: Saiba como monitorar recursos do servidor usando o console JMX.
seo-description: Learn how to monitor server resources using the JMX console.
uuid: 0a28aafe-61b2-472b-8f8f-2cd6540cbfee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 873ce073-0055-4e1b-b3c6-ae7967700894
docset: aem65
exl-id: eabd8335-6140-4c15-8cff-21608719aa5f
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '4962'
ht-degree: 1%

---

# Recursos do Monitoring Server usando a console JMX{#monitoring-server-resources-using-the-jmx-console}

A Console JMX permite que você monitore e gerencie serviços no servidor CRX. As seções a seguir resumem os atributos e operações que são expostos por meio da estrutura JMX.

Para obter informações sobre como usar os controles do console, consulte [Usando a console JMX](#using-the-jmx-console). Para obter informações de fundo sobre JMX, consulte [Tecnologia Java Management Extensions (JMX)](https://www.oracle.com/technetwork/java/javase/tech/javamanagement-140525.html) página no site do Oracle.

Para obter informações sobre como criar MBeans para gerenciar seus serviços usando a Console JMX, consulte [Integração de serviços com o console JMX](/help/sites-developing/jmx-integration.md).

## Manutenção do fluxo de trabalho {#workflow-maintenance}

Operações para administrar instâncias de fluxos de trabalho em execução, concluídas, obsoletas e com falha.

* Domínio: com.adobe.granite.workflow
* Tipo: manutenção

>[!NOTE]
>
>Consulte a [console de fluxo de trabalho](/help/sites-administering/workflows-administering.md) para obter ferramentas adicionais de administração de workflow e descrições de possíveis status de instância de workflow.

### Operações {#operations}

**listRunningWorkflowsPerModel** Lista o número de instâncias de fluxo de trabalho em execução para cada modelo de fluxo de trabalho.

* Argumentos: nenhum
* Valor retornado: dados tabulares contendo as colunas Count e ModelId.

**listCompletedWorkflowsPerModel** Lista o número de instâncias concluídas para cada modelo de fluxo de trabalho.

* Argumentos: nenhum
* Valor retornado: dados tabulares contendo as colunas Count e ModelId.

**returnWorkflowQueueInfo** Lista informações sobre itens de fluxo de trabalho que foram processados e que estão na fila de processamento.

* Argumentos: nenhum
* Valor retornado: dados tabulares contendo as seguintes colunas:

   * Tarefas
   * Nome da Fila
   * Tarefas ativas
   * Tempo Médio de Processamento
   * Tempo médio de espera
   * Trabalhos cancelados
   * Trabalhos com falhas
   * Trabalhos Concluídos
   * Trabalhos processados
   * Trabalhos em fila

**returnWorkflowJobTopicInfo** Lista as informações de processamento para tarefas de workflow, organizadas por tópico.

* Argumentos: nenhum
* Valor retornado: dados tabulares contendo as seguintes colunas:

   * Nome do tópico
   * Tempo Médio de Processamento
   * Tempo médio de espera
   * Trabalhos cancelados
   * Trabalhos com falhas
   * Trabalhos Concluídos
   * Trabalhos processados

**returnFailedWorkflowCount** Mostra o número de instâncias de fluxo de trabalho que falharam. Você pode especificar um modelo de fluxo de trabalho para consultar ou recuperar informações de todos os modelos de fluxo de trabalho.

* Argumentos:

   * model: a ID do modelo a ser consultado. Para ver uma contagem de instâncias de fluxo de trabalho com falha para todos os modelos de fluxo de trabalho, não especifique nenhum valor. A ID é o caminho para o nó do modelo, por exemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor retornado: o número de instâncias de fluxo de trabalho com falha.

**returnFailedWorkflowCountPerModel** Mostra o número de instâncias de fluxo de trabalho que falharam para cada modelo de fluxo de trabalho.

* Argumentos: nenhum.
* Valor retornado: dados tabulares contendo as colunas Contagem e ID do modelo.

**terminateFailedInstances** Encerrar instâncias de fluxo de trabalho que falharam. Você pode encerrar todas as instâncias com falha ou somente as instâncias com falha de um modelo específico. Opcionalmente, é possível reiniciar as instâncias após serem encerradas. Você também pode testar a operação para ver os resultados sem realmente executar a operação.

* Argumentos:

   * Reinicie a instância: (opcional) especifique um valor de `true` para reiniciar as instâncias após serem encerradas. O valor padrão de `false` não causa a reinicialização de instâncias de fluxo de trabalho encerradas.
   * simulação: (opcional) especifique um valor de `true` para ver os resultados da operação sem realmente executá-la. O valor padrão de `false` faz com que a operação seja executada.
   * Modelo: (opcional) a ID do modelo ao qual a operação é aplicada. Especifique nenhum modelo para aplicar a operação às instâncias com falha de todos os modelos de fluxo de trabalho. A ID é o caminho para o nó do modelo, por exemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor retornado: dados tabulares sobre as instâncias terminadas, contendo as seguintes colunas:

   * Iniciador
   * InstanceId
   * ModelId
   * Carga
   * IniciarComentário
   * WorkflowTitle

**retryFailedWorkItems** Tentativas de executar etapas de item de trabalho que falharam. Você pode repetir todos os itens de trabalho com falha ou somente os itens de trabalho com falha de um modelo de fluxo de trabalho específico. Opcionalmente, você testa a operação para ver os resultados sem realmente executar a operação.

* Argumentos:

   * simulação: (opcional) especifique um valor de `true` para ver os resultados da operação sem realmente executá-la. O valor padrão de `false` faz com que a operação seja executada.
   * Modelo: (opcional) a ID do modelo ao qual a operação é aplicada. Especifique nenhum modelo para aplicar a operação aos itens de trabalho com falha de todos os modelos de fluxo de trabalho. A ID é o caminho para o nó do modelo, por exemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor retornado: dados tabulares sobre os itens de trabalho com falha que são repetidos, incluindo as seguintes colunas:

   * Iniciador
   * InstanceId
   * ModelId
   * Carga
   * IniciarComentário
   * WorkflowTitle

**LimparAtivo** Remove instâncias de fluxo de trabalho ativas de uma página específica. Você pode remover as instâncias ativas de todos os modelos ou apenas as instâncias de um modelo específico. Opcionalmente, você pode testar a operação para ver os resultados sem realmente executar a operação.

* Argumentos:

   * Modelo: (opcional) a ID do modelo ao qual a operação é aplicada. Especifique nenhum modelo para aplicar a operação às instâncias de fluxo de trabalho de todos os modelos de fluxo de trabalho. A ID é o caminho para o nó do modelo, por exemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Número de dias desde o início do workflow: a idade das instâncias de workflow a serem removidas, em dias.
   * simulação: (opcional) especifique um valor de `true` para ver os resultados da operação sem realmente executá-la. O valor padrão de `false` faz com que a operação seja executada.

* Valor retornado: dados tabulares sobre as instâncias de fluxo de trabalho ativas que são removidas, incluindo as seguintes colunas:

   * Iniciador
   * InstanceId
   * ModelId
   * Carga
   * IniciarComentário
   * WorkflowTitle

**countStaleWorkflows** Retorna o número de instâncias de fluxo de trabalho obsoletas. Você pode recuperar o número de instâncias obsoletas para todos os modelos de fluxo de trabalho ou para um modelo específico.

* Argumentos:

   * Modelo: (opcional) a ID do modelo ao qual a operação é aplicada. Especifique nenhum modelo para aplicar a operação às instâncias de fluxo de trabalho de todos os modelos de fluxo de trabalho. A ID é o caminho para o nó do modelo, por exemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor retornado: o número de instâncias de fluxo de trabalho obsoletas.

**restartStaleWorkflows** Reinicia instâncias de fluxo de trabalho obsoletas. Você pode reiniciar todas as instâncias obsoletas ou apenas as instâncias obsoletas de um modelo específico. Você também pode testar a operação para ver os resultados sem realmente executar a operação.

* Argumentos:

   * Modelo: (opcional) a ID do modelo ao qual a operação é aplicada. Especifique nenhum modelo para aplicar a operação às instâncias obsoletas de todos os modelos de fluxo de trabalho. A ID é o caminho para o nó do modelo, por exemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * simulação: (opcional) especifique um valor de `true` para ver os resultados da operação sem realmente executá-la. O valor padrão de `false` faz com que a operação seja executada.

* Valor retornado: uma lista de instâncias de fluxo de trabalho que são reiniciadas.

**fetchModelList** Lista todos os modelos de workflow.

* Argumentos: nenhum
* Valor retornado: dados tabulares que identificam os modelos de fluxo de trabalho, incluindo as colunas ModelId e ModelName.

**countRunningWorkflows** Retorna o número de instâncias de fluxo de trabalho em execução. Você pode recuperar o número de instâncias em execução para todos os modelos de fluxo de trabalho ou para um modelo específico.

* Argumentos:

   * Modelo: (opcional) a ID do modelo para o qual o número de instâncias em execução é retornado. Especifique nenhum modelo para retornar o número de instâncias em execução de todos os modelos de fluxo de trabalho. A ID é o caminho para o nó do modelo, por exemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor retornado: o número de instâncias de fluxo de trabalho em execução.

**countCompletedWorkflows** Retorna o número de instâncias de fluxo de trabalho concluídas. Você pode recuperar o número de instâncias concluídas para todos os modelos de fluxo de trabalho ou para um modelo específico.

* Argumentos:

   * Modelo: (opcional) a ID do modelo para o qual o número de instâncias concluídas é retornado. Especifique nenhum modelo para retornar o número de instâncias concluídas de todos os modelos de fluxo de trabalho. A ID é o caminho para o nó do modelo, por exemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor retornado: o número de instâncias de fluxo de trabalho concluídas.

**purgeCompleted** Remove registros de fluxos de trabalho concluídos de uma página específica do repositório. Use essa operação periodicamente para minimizar o tamanho do repositório ao usar workflows. Você pode remover as instâncias concluídas de todos os modelos ou apenas as instâncias de um modelo específico. Opcionalmente, você pode testar a operação para ver os resultados sem realmente executar a operação.

* Argumentos:

   * Modelo: (opcional) a ID do modelo ao qual a operação é aplicada. Especifique nenhum modelo para aplicar a operação às instâncias de fluxo de trabalho de todos os modelos de fluxo de trabalho. A ID é o caminho para o nó do modelo, por exemplo:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Número de dias desde a conclusão do fluxo de trabalho: o número de dias em que as instâncias de fluxo de trabalho estiveram no estado concluído.
   * simulação: (opcional) especifique um valor de `true` para ver os resultados da operação sem realmente executá-la. O valor padrão de `false` faz com que a operação seja executada.

* Valor retornado: dados tabulares sobre as instâncias de fluxo de trabalho concluídas que são removidas, incluindo as seguintes colunas:

   * Iniciador
   * InstanceId
   * ModelId
   * Carga
   * IniciarComentário
   * WorkflowTitle

## Repositório {#repository}

Informações sobre o repositório CRX

* Domínio: com.adobe.granite
* Tipo: Repositório

### Atributos {#attributes}

**Nome** O nome da implementação do repositório JCR. Somente leitura.

**Versão** A versão de implementação do repositório. Somente leitura.

**HomeDir** O diretório onde o repositório está localizado. O local padrão é &lt;quickstart_jar_location>/crx-quickstart/repository. Somente leitura.

**NomeCliente** O nome do cliente para o qual a licença de software é emitida. Somente leitura.

**LicenseKey** A chave de licença exclusiva para esta instalação do repositório. Somente leitura.

**EspaçoDisponívelEmDisco** O espaço em disco disponível para esta instância do repositório, em Mbytes. Somente leitura.

**NúmeroMáximoDeArquivosAbertos** O número de arquivos que podem ser abertos de uma vez. Somente leitura.

**SessionTracker** O valor da variável de sistema crx.debug.sessions. true indica uma sessão de depuração. false indica uma sessão normal. Leitura/gravação.

**Descritores** Um conjunto de pares de valores chave que representam propriedades do repositório. Todas as propriedades são somente leitura.

<table>
 <tbody>
  <tr>
   <th>Chave</th>
   <th>Valor</th>
  </tr>
  <tr>
   <td>option.node.and.property.with.same.name.supported</td>
   <td>Indica se um nó e uma propriedade do nó podem ter o mesmo nome. true indica que há suporte para os mesmos nomes, false indica que não há suporte. </td>
  </tr>
  <tr>
   <td>identifier.stability</td>
   <td>Indica a estabilidade de identificadores de nó não referenciáveis. Os seguintes valores são possíveis:
    <ul>
     <li>identifier.stable.indefinite.duration: os identificadores não são alterados.</li>
     <li>identifier.stable.method.duration: os identificadores podem ser alterados entre chamadas de método.</li>
     <li>identifier.stable.save.duration: os identificadores não são alterados em um ciclo de salvar/atualizar.</li>
     <li>identifier.stable.session.duration: os identificadores não são alterados durante uma sessão.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>query.xpath.pos.index</td>
   <td>Indica se há suporte para a linguagem de consulta XPath do JCR 1.0. verdadeiro indica suporte, e falso indica nenhum suporte.</td>
  </tr>
  <tr>
   <td>crx.repository.systemid</td>
   <td>O identificador do sistema foi encontrado no arquivo system.id.</td>
  </tr>
  <tr>
   <td>option.query.sql.supported</td>
   <td>Indica se há suporte para a linguagem de consulta XPath do JCR 1.0. verdadeiro indica suporte, e falso indica nenhum suporte.</td>
  </tr>
  <tr>
   <td>jcr.repository.version</td>
   <td>A versão da implementação do repositório.</td>
  </tr>
  <tr>
   <td>option.update.primary.node.type.supported</td>
   <td>Indica se o tipo de nó primário de um nó pode ser alterado. true indica que você pode alterar o tipo de nó primário e false indica que a alteração não é suportada.</td>
  </tr>
  <tr>
   <td>option.node.type.management.supported</td>
   <td>Indica se há suporte para o gerenciamento de tipo de nó. true indica que é compatível e false indica que não há suporte.</td>
  </tr>
  <tr>
   <td>node.type.management.overrides.supported</td>
   <td>Indica se você pode substituir a propriedade herdada ou a definição de nó filho de um tipo de nó. true indica que há suporte para substituições e false indica que não há substituições.</td>
  </tr>
  <tr>
   <td>option.observation.supported</td>
   <td>true indica que a observação assíncrona de alterações no repositório é suportada. O suporte à observação assíncrona permite que os aplicativos recebam e respondam a notificações sobre cada alteração à medida que elas ocorrem.</td>
  </tr>
  <tr>
   <td>query.jcrscore</td>
   <td><p>true indica que a pseudopropriedade jcr:score está disponível em consultas XPath e SQL que incluem uma função jcrfn:contains (em XPath) ou CONTAINS (em SQL) para executar uma pesquisa de texto completo.</p> </td>
  </tr>
  <tr>
   <td>option.simple.versioning.supported</td>
   <td>true indica que o repositório suporta o controle de versão simples. Com o controle de versão simples, o repositório mantém uma série sequencial de versões de um nó.</td>
  </tr>
  <tr>
   <td>option.workspace.management.supported</td>
   <td>true indica que o repositório oferece suporte à criação e exclusão de espaços de trabalho usando APIs.</td>
  </tr>
  <tr>
   <td>option.update.mixin.node.types.supported</td>
   <td>true indica que o repositório oferece suporte à adição e remoção de tipos de nó mixin de um nó existente.</td>
  </tr>
  <tr>
   <td>node.type.management.primary.item.name.supported</td>
   <td>true indica que o repositório permite que as definições de nó contenham um item primário como filho. Um item principal pode ser acessado usando a API sem saber o nome do item.</td>
  </tr>
  <tr>
   <td>nível.2.suportado</td>
   <td>true indica que LEVEL_1_SUPPORTED e OPTION_XML_IMPORT_SUPPORTED são true.</td>
  </tr>
  <tr>
   <td>write.supported</td>
   <td>true indica que o repositório fornece acesso de gravação usando a API. false indica acesso somente leitura.</td>
  </tr>
  <tr>
   <td>node.type.management.update.in.use.supported</td>
   <td>true indica que você pode alterar as definições de nó em uso pelos nós existentes.</td>
  </tr>
  <tr>
   <td>jcr.specification.version</td>
   <td>A versão da especificação do JCR que o repositório implementa.</td>
  </tr>
  <tr>
   <td>option.journaled.observation.supported</td>
   <td>true indica que os aplicativos podem executar a observação registrada do repositório. com a observação registrada, um conjunto de notificações de alteração pode ser obtido por um período específico. </td>
  </tr>
  <tr>
   <td>query.languages</td>
   <td>Os idiomas de consulta compatíveis com o repositório. Nenhum valor indica que não há suporte para consulta.</td>
  </tr>
  <tr>
   <td>option.xml.export.supported</td>
   <td>true indica que o repositório suporta a exportação de nós como código XML.</td>
  </tr>
  <tr>
   <td>node.type.management.multiple.binary.properties.supported</td>
   <td>true indica que o repositório suporta o registro de tipos de nó que têm várias propriedades binárias. false indica que uma única propriedade binária é suportada para um tipo de nó.</td>
  </tr>
  <tr>
   <td>option.access.control.supported</td>
   <td>true indica que o repositório oferece suporte ao controle de acesso, para configurar e determinar privilégios de usuário para acesso ao nó.</td>
  </tr>
  <tr>
   <td>option.baselines.supported</td>
   <td>true indica que o repositório suporta configurações e linhas de base.</td>
  </tr>
  <tr>
   <td>option.shareable.nodes.supported</td>
   <td>true indica que o repositório oferece suporte à criação de nós compartilháveis.</td>
  </tr>
  <tr>
   <td>crx.cluster.id</td>
   <td>O identificador do cluster do repositório.</td>
  </tr>
  <tr>
   <td>query.stored.queries.supported</td>
   <td>true indica que o repositório suporta consultas armazenadas.</td>
  </tr>
  <tr>
   <td>query.full.text.search.supported</td>
   <td>true indica que o repositório suporta pesquisa de texto completo.</td>
  </tr>
  <tr>
   <td>node.type.management.inheritance</td>
   <td><p>Indica o nível de suporte de repositório para herança de tipo de nó. Os seguintes valores são possíveis:</p> <p>node.type.management.inheritance.minimal: o registro de tipos de nós primários é limitado àqueles que têm apenas nt:base como supertipo. O registro de tipos de nó mixin é limitado àqueles sem supertipo.</p> <p>node.type.management.inheritance.single: o registro de tipos de nó primário é limitado àqueles com um supertipo. O registro de tipos de nó mixin é limitado àqueles com no máximo um supertipo.</p> <p><br /> node.type.management.inheritance.multiple: os tipos de nó primário podem ser registrados com um ou mais supertipos. Os tipos de nó mixin podem ser registrados com zero ou mais supertipos.</p> </td>
  </tr>
  <tr>
   <td>crx.cluster.preferredMaster</td>
   <td>true indica que este nó de cluster é o mestre preferencial do cluster.</td>
  </tr>
  <tr>
   <td>option.transactions.supported</td>
   <td>true indica que o repositório suporta transações.</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor.url</td>
   <td>O URL do fornecedor do repositório.</td>
  </tr>
  <tr>
   <td>node.type.management.value.constraints.supported</td>
   <td>true indica que o repositório aceita restrições de valor para propriedades do nó.</td>
  </tr>
  <tr>
   <td>node.type.management.property.types</td>
   <td>uma matriz de constantes javax.jcr.PropertyType que representa os tipos de propriedade que um tipo de nó registrado pode especificar. Uma matriz de comprimento zero indica que os tipos de nó registrados não podem especificar definições de propriedade. Os tipos de propriedade são STRING, URI, BOOLEAN, LONG, DOUBLE, DECIMAL, BINARY, DATE, NAME, PATH, WEAKREFERENCE, REFERENCE e UNDEFINED (se houver suporte)</td>
  </tr>
  <tr>
   <td>node.type.management.orderable.child.nodes.supported</td>
   <td>true indica que o repositório aceita a preservação da ordem dos nós filhos.</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor</td>
   <td>O nome do fornecedor do repositório.</td>
  </tr>
  <tr>
   <td>query.joins</td>
   <td><p>O nível de suporte para associações em consultas. Os seguintes valores são possíveis:</p>
    <ul>
     <li>query.joins.none: não há suporte para junções. As consultas podem usar um seletor.</li>
     <li>query.joins.inner: suporte para junções internas.</li>
     <li>query.joins.inner.outer: suporte para associações internas e externas.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>org.apache.jackrabbit.spi.commons.AdditionalEventInfo</td>
   <td> </td>
  </tr>
  <tr>
   <td>query.xpath.doc.order</td>
   <td>true indica que o repositório suporta o idioma de consulta XPath 1.0.</td>
  </tr>
  <tr>
   <td>query.jcrpath</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.xml.import.supported</td>
   <td>true indica que o repositório aceita a importação do código XML como conteúdo.</td>
  </tr>
  <tr>
   <td>node.type.management.same.name.siblings.supported</td>
   <td>true indica que o repositório suporta nós irmãos (nós com o mesmo pai) com os mesmos nomes.</td>
  </tr>
  <tr>
   <td>node.type.management.residual.definitions.supported</td>
   <td>true indica que o repositório suporta propriedades de nome com definições residuais. Quando suportado, o atributo de nome de uma definição de item pode ser um asterisco ("*").</td>
  </tr>
  <tr>
   <td>node.type.management.autocreated.definitions.supported</td>
   <td>true indica que o repositório oferece suporte à criação automática de itens secundários (nós ou propriedades) de um nó quando ele é criado.</td>
  </tr>
  <tr>
   <td>crx.cluster.master</td>
   <td>true indica que este nó de repositório é o nó mestre do cluster.</td>
  </tr>
  <tr>
   <td>level.1.supported</td>
   <td>true indica que option.xml.export.support é true e query.languages tem comprimento diferente de zero.</td>
  </tr>
  <tr>
   <td>option.unfiled.content.supported</td>
   <td>true indica que o repositório suporta conteúdo não arquivado. Nós não arquivados não fazem parte da hierarquia do repositório.</td>
  </tr>
  <tr>
   <td>jcr.specification.name</td>
   <td>O nome da especificação JCR que o repositório implementa.</td>
  </tr>
  <tr>
   <td>option.versioning.supported</td>
   <td>true indica que o repositório suporta controle de versão completo.</td>
  </tr>
  <tr>
   <td>jcr.repository.name</td>
   <td>O nome do repositório.</td>
  </tr>
  <tr>
   <td>option.locking.supported</td>
   <td>true indica que o repositório suporta o bloqueio de nós. O bloqueio permite que um usuário impeça temporariamente que outros usuários façam alterações.</td>
  </tr>
  <tr>
   <td>jcr.repository.version.display</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.activities.supported</td>
   <td>true indica que o repositório suporta atividades. Atividades são um conjunto de alterações realizadas em um espaço de trabalho mesclado a outro espaço de trabalho.</td>
  </tr>
  <tr>
   <td>node.type.management.multivalued.properties.supported</td>
   <td>true indica que o repositório suporta propriedades de nó que podem ter zero ou mais valores.</td>
  </tr>
  <tr>
   <td>option.retention.supported</td>
   <td>true indica que o repositório aceita o uso de aplicativos externos de gerenciamento de retenção para aplicar políticas de retenção ao conteúdo e aceita a retenção e a liberação.</td>
  </tr>
  <tr>
   <td>option.lifecycle.supported</td>
   <td>true indica que o repositório é compatível com o gerenciamento do ciclo de vida.</td>
  </tr>
 </tbody>
</table>

**WorkspaceNames** Os nomes dos espaços de trabalho no repositório. Somente leitura.

**DataStoreGarbageCollectionDelay** O tempo em milissegundos que a coleta de lixo fica em espera após a varredura a cada décimo nó. Leitura/gravação.

**BackupDelay** O tempo em milissegundos que o processo de backup fica suspenso entre cada etapa do backup. Leitura/gravação.

**BackupEmAndamento** Um valor true indica que um processo de backup está em execução. Somente leitura.

**Andamento do backup** Para o backup atual, o percentual de todos os arquivos que foram submetidos a backup. Somente leitura.

**DestinoDoBackupAtual** Para o backup atual, o arquivo ZIP onde os arquivos de backup estão sendo armazenados. Quando um backup não está em andamento, nenhum valor é exibido. Somente leitura.

**BackupWasSuccessful** Um valor true indica que não ocorreram erros durante o backup atual ou que nenhum backup está em andamento. false indica que ocorreu um erro durante o backup atual. Somente leitura.

**BackupResult** O status do backup atual. Os seguintes valores são possíveis:

* Backup em andamento: um backup está sendo executado no momento.
* Backup cancelado: o backup foi cancelado.
* Backup concluído com erro: erro durante o backup. A mensagem de erro fornece informações sobre a causa.
* Backup concluído: o backup foi bem-sucedido.
* Nenhum backup executado até o momento: não há backup em andamento.

Somente leitura.

**TarOtimizationRunningSince** A hora em que o processo atual de otimização de arquivos TAR começou. Somente leitura.

**TarOtimizationDelay** O tempo em milissegundos que o processo de otimização de TAR aguarda entre cada etapa do processo. Leitura/gravação.

**ClusterProperties** Um conjunto de pares de valores-chave que representam as propriedades e os valores do cluster. Cada linha na tabela representa uma propriedade de cluster. Somente leitura.

**ClusterNodes** Os membros do cluster do repositório.

**ClusterId** O identificador deste cluster de repositório. Somente leitura.

**ClusterMasterId** O identificador do nó mestre deste cluster de repositório. Somente leitura.

**ClusterNodeId** O identificador deste nó do cluster do repositório. Somente leitura.

### Operações {#operations-1}

**createWorkspace** Cria um espaço de trabalho neste repositório.

* Argumentos:

   * name: um valor de string que representa o nome do novo espaço de trabalho.

* Valor retornado: nenhum

**runDataStoreGarbageCollection** Executa a coleta de lixo nos nós do repositório.

* Argumentos:

   * excluir: um valor booleano que indica se os itens do repositório não utilizados devem ser excluídos. Um valor true causa a exclusão de nós e propriedades não usados. Um valor false faz com que todos os nós sejam verificados, mas nenhum é excluído.

* Valor retornado: nenhum

**stopDataStoreGarbageCollection** Interrompe uma coleta de lixo do armazenamento de dados em execução.

* Argumentos: nenhum
* Valor retornado: representação da string do status atual

**startBackup** Faz backup dos dados do repositório em um arquivo ZIP.

* Argumentos:

   * `target`: (Opcional) A `String` valor que representa o nome do arquivo ZIP ou diretório em que os dados do repositório serão arquivados. Para usar um arquivo ZIP, inclua a extensão de nome de arquivo ZIP. Para usar um diretório, inclua nenhuma extensão de nome de arquivo.

     Para executar um backup incremental, especifique o diretório usado anteriormente para o backup.

     Você pode especificar um caminho absoluto ou relativo. Os caminhos relativos são relativos ao pai do diretório crx-quickstart.

     Quando você não especificar nenhum valor, o valor padrão de `backup-currentdate.zip` é utilizada, onde `currentdate` está no formato `yyyyMMdd-HHmm`.

* Valor retornado: nenhum

**cancelBackup** Interrompe o processo de backup atual e exclui o arquivo temporário criado pelo processo para arquivar dados.

* Argumentos: nenhum
* Valor retornado: nenhum

**blockRepositoryWrites** Bloqueia alterações nos dados do repositório. Todos os ouvintes de backup do repositório são notificados sobre o bloco.

* Argumentos: nenhum
* Valor retornado: nenhum

**unblockRepositoryWrites** Remove o bloco do repositório. Todos os ouvintes de backup do repositório são notificados sobre a remoção do bloco.

* Argumentos: nenhum
* Valor retornado: nenhum

**startTarOtimization** Inicia o processo de otimização do arquivo TAR usando o valor padrão para tarOtimizationDelay.

* Argumentos: nenhum
* Valor retornado: nenhum

**stopTarOtimization** Interrompe a otimização do arquivo TAR.

* Argumentos: nenhum
* Valor retornado: nenhum

**tarIndexMerge** Mescla os arquivos de índice superiores de todos os conjuntos TAR. Os principais arquivos de índice são arquivos com diferentes versões principais. Por exemplo, os seguintes arquivos são mesclados no arquivo index_3_1.tar: index_1_1.tar, index_2_0.tar, index_3_0.tar. Os arquivos mesclados são excluídos (no exemplo anterior, index_1_1.tar, index_2_0.tar e index_3_0.tar são excluídos).

* Argumentos:

   * `background`: um valor booliano que indica se a operação deve ser executada em segundo plano para que o Console da Web possa ser usado durante a execução. Um valor true executa a operação em segundo plano.

* Valor retornado: nenhum

**makeClusterMaster** Define este nó de repositório como o nó mestre do cluster. Se ainda não tiver sido mestre, este comando interrompe o listener da instância mestre atual e inicia um listener mestre no nó atual. Em seguida, esse nó é definido como o nó principal e reiniciado, fazendo com que todos os outros nós no cluster (ou seja, aqueles que são controlados pelo mestre) se conectem a essa instância.

* Argumentos: nenhum
* Valor retornado: nenhum

**joinCluster** Adiciona este repositório a um cluster como um nó controlado pelo cluster mestre. Você deve fornecer um nome de usuário e senha para fins de autenticação. A conexão usa autenticação básica. As credenciais de segurança são codificadas na base 64 antes de serem enviadas ao servidor.

* Argumentos:

   * `master`: um valor de string que representa o endereço IP ou o nome do computador que executa o nó do repositório principal.
   * `username`: O nome a ser usado para autenticar com o cluster.
   * `password`: a senha a ser usada para autenticação.

* Valor retornado: nenhum

**traversalCheck** Atravessa e, opcionalmente, corrige inconsistências em uma subárvore que começa em um nó específico. Isso é abordado em detalhes completos na documentação dos Gerenciadores de persistência.

**consistencyCheck** Verificações e, opcionalmente, correções de consistência no Datastore. Isso é abordado em detalhes completos na documentação sobre o armazenamento de dados.

## Estatísticas do repositório (TimeSeries) {#repository-statistics-timeseries}

O valor do campo TimeSeries para cada tipo de estatística `org.apache.jackrabbit.api.stats.RepositoryStatistics` define.

* Domínio: `com.adobe.granite`
* Tipo: `TimeSeries`
* Nome: um dos seguintes valores do `org.apache.jackrabbit.api.stats.RepositoryStatistics.Type` Classe Enum:

   * BUNDLE_CACHE_ACCESS_COUNTER
   * BUNDLE_CACHE_MISS_AVERAGE
   * BUNDLE_CACHE_MISS_COUNTER
   * BUNDLE_CACHE_MISS_DURATION
   * BUNDLE_CACHE_SIZE_COUNTER
   * BUNDLE_COUNTER
   * BUNDLE_READ_COUNTER
   * BUNDLE_WRITE_AVERAGE
   * BUNDLE_WRITE_COUNTER
   * BUNDLE_WRITE_DURATION
   * BUNDLE_WS_SIZE_COUNTER
   * QUERY_AVERAGE
   * QUERY_COUNT
   * QUERY_DURATION
   * SESSION_COUNT
   * SESSION_LOGIN_COUNTER
   * SESSION_READ_AVERAGE
   * SESSION_READ_COUNTER
   * SESSION_READ_DURATION
   * SESSION_WRITE_AVERAGE
   * SESSION_WRITE_COUNTER
   * SESSION_WRITE_DURATION

### Atributos {#attributes-1}

Os seguintes atributos são fornecidos para cada tipo de estatística reportado:

* ValuePerSecond: o valor medido por segundo durante o último minuto. Somente leitura.
* ValuePerMinute: o valor medido por minuto na última hora. Somente leitura.
* ValuePerHour: o valor medido por hora na última semana. Somente leitura.
* ValuePerWeek: O valor medido por semana nos últimos três anos. Somente leitura.

## Estatísticas de consulta do repositório {#repository-query-stats}

Informações estatísticas sobre consultas de repositório.

* Domínio: com.adobe.granite
* Tipo: QueryStat

### Atributos {#attributes-2}

**SlowQueries** Informações sobre as consultas do repositório que levaram mais tempo para serem concluídas. Somente leitura.

**TamanhoLentoDaFilaDeConsultas** O número máximo de consultas a serem incluídas na lista SlowQueries. Leitura-gravação.

**PopularQueries** Informações sobre as consultas do repositório que mais ocorreram. Somente leitura.

**PopularQueriesQueueSize** O número máximo de consultas na lista PopularQueries. Leitura-gravação.

### Operações {#operations-2}

**clearSlowQueriesQueue** Remove todas as consultas da lista de consultas lentas.

* Argumentos: nenhum
* Valor retornado: nenhum

**clearPopularQueriesQueue** Remove todas as consultas da lista PopularQueries.

* Argumentos: nenhum
* Valor retornado: nenhum

## Agentes de replicação {#replication-agents}

Monitore os serviços para cada agente de replicação. Quando você cria um agente de replicação, o serviço aparece automaticamente no console JMX.

* **Domínio:** com.adobe.granite.replication
* **Tipo:** agente
* **Nome:** sem valor
* **Propriedades:** {id=&quot;*Nome*&quot;}, onde *Nome* é o valor da propriedade Name do agente.

### Atributos {#attributes-3}

**ID** Um valor de String que representa o identificador da configuração do agente de replicação. Vários agentes podem usar a mesma configuração. Somente leitura.

**Válido** Um valor booleano que indica se o agente está configurado corretamente:

* `true`: configuração válida.
* `false` : a configuração contém erros.

Somente leitura.

**Ativado** Um valor booleano que indica se o agente está ativado:

* `true`: Habilitado.
* `false`: Desativado.

**FilaBloqueada** Um valor booleano que indica se a fila existe e está bloqueada:

* `true`: Bloqueado. Uma nova tentativa automática está pendente.
* `false`: Não bloqueado ou não existe.

Somente leitura.

**QueuePaused** Um valor booleano que indica se a fila de trabalhos está pausada:

* `true`: Pausado (suspenso)
* `false`: Não pausado ou não existe.

Leitura-gravação.

**QueueNumEntries** Um valor int que representa o número de trabalhos na fila do agente. Somente leitura.

**QueueStatusTime** Um valor de Date que indica a hora no servidor quando os valores de status exibidos foram obtidos. O valor corresponde à hora em que a página foi carregada. Somente leitura.

**EnfileirarPróximaTentativaHora** Para filas bloqueadas, um valor de Data que indica quando ocorre a próxima tentativa automática. Quando nenhuma hora for exibida, a fila não será bloqueada. Somente leitura.

**EnfileirarProcessamentoDesde** Um valor de Data que indica quando o processamento começou para a tarefa atual. Quando não aparecer nenhuma hora, a fila será bloqueada ou ficará ociosa. Somente leitura.

**TempoÚltimoProcessoFila** Um valor de Data que indica quando o trabalho anterior foi concluído. Somente leitura.

### Operações {#operations-3}

**queueForceRetry** Para filas bloqueadas, o emite o comando retry para a fila.

* Argumentos: nenhum
* Valor retornado: nenhum

**queueClear** Remove todas as tarefas da fila.

* Argumentos: nenhum
* Valor retornado: nenhum

## Mecanismo Sling {#sling-engine}

Fornece estatísticas sobre solicitações HTTP para que você possa monitorar o desempenho do serviço SlingRequestProcessor.

* Domínio: org.apache.sling
* Tipo: mecanismo
* Propriedades: {service=RequestProcessor}

### Atributos {#attributes-4}

**RequestsCount** O número de solicitações que ocorreram desde que as estatísticas foram redefinidas pela última vez.

**MinRequestDurationMsec** O menor tempo (em milissegundos) necessário para processar uma solicitação desde a última redefinição das estatísticas.

**MaxRequestDurationMsec** O tempo mais longo (em milissegundos) necessário para processar uma solicitação desde a última redefinição das estatísticas.

**DuraçãodeDesvioPadrãoMS** O desvio padrão da quantidade de tempo que foi necessária para processar solicitações. O desvio padrão é calculado usando todas as solicitações desde que as estatísticas foram redefinidas pela última vez.

**DuraçãodeSolicitaçãodeMédiaMS** O tempo médio necessário para processar uma solicitação. A média é calculada usando todas as solicitações desde a última redefinição das estatísticas

### Operações {#operations-4}

**resetStatistics** Define todas as estatísticas como zero. Redefina as estatísticas quando precisar analisar o desempenho do processamento de solicitações durante um período específico.

* Argumentos: nenhum
* Valor retornado: nenhum

**id** A representação da string da ID do pacote.

**instalado** Um valor booleano que indica se o pacote está instalado:

* `true`: Instalado.
* `false`: Não instalado.

**installedBy** A ID do último usuário que instalou o pacote.

**installedDate** A data em que o pacote foi instalado pela última vez.

**tamanho** Um valor longo que armazena o tamanho do pacote em bytes.


## Quickstart Launcher {#quickstart-launcher}

Informações sobre o processo de inicialização e o Quickstart launcher.

* Domínio: com.adobe.granite.quickstart
* Tipo: Iniciador

### Operações {#operations-5}

**log**

Exibe uma mensagem na janela QuickStart.

Argumentos:

* p1: A `String` que representa a mensagem a ser exibida.
* Valor retornado: nenhum

**startupFinished**

Chama o método startupFinished do inicializador de servidor. O método tenta abrir a página de Boas-vindas em um navegador da Web.

* Argumentos: nenhum
* Valor retornado: nenhum

**startupProgress**

Define o valor de conclusão do processo de inicialização do servidor. A barra de progresso na janela QuickStart representa o valor de conclusão.

* Argumentos:
   * p1: um valor flutuante que representa quanto do processo de inicialização está concluído, como uma fração. O valor deve estar entre zero e um. Por exemplo, 0,3 indica 30% concluído.
* Valor retornado: nenhum.

## Serviços de terceiros {#third-party-services}

Vários recursos de servidor de terceiros instalam MBeans que expõem atributos e operações ao console JMX. A tabela a seguir lista os recursos de terceiros e fornece links para mais informações.

<table>
 <tbody>
  <tr>
   <th>Domínio</th>
   <th>Tipo</th>
   <th>Classe MBean</th>
  </tr>
  <tr>
   <td>Implementação JMI</td>
   <td>MBeanServerDelegate</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/MBeanServerDelegate.html">javax.management.MBeanServerDelegate</a></td>
  </tr>
  <tr>
   <td>com.sun.management</td>
   <td>HotSpotDiagnostic</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/jre/api/management/extension/com/sun/management/HotSpotDiagnosticMXBean.html">com.sun.management.HotSpotDiagnosticMXBean</a></td>
  </tr>
  <tr>
   <td>java.lang</td>
   <td>
    <ul>
     <li>ClassLoading</li>
     <li>Compilação</li>
     <li>GarbageCollector</li>
     <li>Memória</li>
     <li>MemoryManager</li>
     <li>MemoryPool</li>
     <li>OperatingSystem</li>
     <li>Tempo de execução</li>
     <li>Threading</li>
    </ul> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/package-summary.html">javax.management</a> pacote</td>
  </tr>
  <tr>
   <td>java.util.logging</td>
   <td> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/java/util/logging/LoggingMXBean.html">java.util.logging.LoggingMXBean</a></td>
  </tr>
  <tr>
   <td>osgi.core</td>
   <td>
    <ul>
     <li>bundleState</li>
     <li>estrutura</li>
     <li>packageState</li>
     <li>serviceState</li>
    </ul> </td>
   <td><a href="https://osgi.org/specification/osgi.enterprise/7.0.0/service.jmx.html#d0e42567">org.osgi.jmx.framework</a> pacote</td>
  </tr>
 </tbody>
</table>

## Usando a console JMX {#using-the-jmx-console}

A Console JMX exibe informações sobre vários serviços que estão sendo executados no servidor:

* Atributos: propriedades de serviço, como configurações ou dados de tempo de execução. Os atributos podem ser somente leitura ou leitura-gravação.
* Operações: Comandos que podem ser chamados no serviço.

Os MBeans implantados com um serviço OSGi expõem os atributos e as operações do serviço para o console. O MBean determina os atributos e operações que são expostos e se os atributos são somente leitura ou leitura-gravação.

A página principal do console JMX inclui uma tabela de serviços. Cada linha na tabela representa um serviço exposto por um MBean.

1. Abra o Console da Web e clique na guia JMX. ([http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
2. Clique em um valor de célula para um serviço para ver os atributos e as operações do serviço.
3. Para alterar um valor de atributo, clique no valor, especifique o valor na caixa de diálogo exibida e clique em Salvar.
4. Para chamar uma operação de serviço, clique no nome da operação, especifique valores de argumento na caixa de diálogo exibida e clique em Chamar.

## Usando aplicações JMX externas para monitoramento {#using-external-jmx-applications-for-monitoring}

O CRX permite que aplicativos externos interajam com Beans gerenciados (MBeans) via [Java Management Extensions (JMX)](https://docs.oracle.com/javase/6/docs/technotes/guides/management/overview.html). Usar consoles genéricos, como [JConsole](https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html) ou aplicativos de monitoramento específicos do domínio, permite obter e definir configurações e propriedades de CRX, além de monitorar o desempenho e o uso de recursos.

### Utilização do JConsole para se conectar ao CRX {#using-jconsole-to-connect-to-crx}

Para se conectar ao CRX usando o JConsole, siga estas etapas:

1. Abra uma janela de terminal.
1. Digite o seguinte comando:

   `jconsole`

O JConsole será iniciado e a janela JConsole será exibida.

### Conexão com um processo CRX local {#connecting-to-a-local-crx-process}

O JConsole exibirá uma lista de processos locais da Java Virtual Machine. A lista conterá dois processos de início rápido. Selecione o processo de início rápido &quot;CHILD&quot; na lista de processos locais (geralmente aquele com o PID mais alto).

![screen_shot_2012-03-26at114557am](assets/screen_shot_2012-03-26at114557am.png)

### Conectando-se a um processo CRX remoto {#connecting-to-a-remote-crx-process}

Para conectar-se a um processo CRX remoto, a JVM que hospeda o processo CRX remoto deve ser ativada para aceitar conexões JMX remotas.

Para ativar conexões JMX remotas, a seguinte propriedade do sistema deve ser definida ao iniciar a JVM:

`com.sun.management.jmxremote.port=portNum`

Na propriedade acima, `portNum` é o número da porta através da qual você deseja ativar as conexões JMX RMI. Certifique-se de especificar um número de porta não utilizado. Além de publicar um conector RMI para acesso local, a definição dessa propriedade publica um conector RMI adicional em um registro somente leitura privado na porta especificada usando um nome bem conhecido, &quot;jmxrmi&quot;.

Por padrão, quando você ativa o agente JMX para monitoramento remoto, ele usa a autenticação de senha com base em um arquivo de senha que precisa ser especificado usando a seguinte propriedade do sistema ao iniciar a Java VM:

`com.sun.management.jmxremote.password.file=pwFilePath`

Consulte a [documentação JMX relevante](https://docs.oracle.com/javase/6/docs/technotes/guides/management/agent.html) para obter instruções detalhadas sobre como configurar um arquivo de senha.

Exemplo:

```shell
$ java
  -Dcom.sun.management.jmxremote.password.file=pwFilePath
  -Dcom.sun.management.jmxremote.port=8463
  -jar ./cq-quickstart.jar
```

### Uso dos MBeans fornecidos pelo CRX {#using-the-mbeans-provided-by-crx}

Depois de se conectar ao processo de início rápido, o JConsole fornece uma variedade de ferramentas gerais de monitoramento para a JVM em que o CRX está sendo executado.

![screen_shot_2012-03-26at115056am](assets/screen_shot_2012-03-26at115056am.png)

Para acessar as opções internas de monitoramento e configuração do CRX, vá para a guia MBeans e, na árvore de conteúdo hierárquico à esquerda, selecione a seção Attributes or Operations na qual está interessado. Por exemplo, a seção com.adobe.granite/Repository/Operations.

Nessa seção, selecione o atributo ou a operação desejada no painel esquerdo.

![screen_shot_2012-03-26at115728am](assets/screen_shot_2012-03-26at115728am.png)
