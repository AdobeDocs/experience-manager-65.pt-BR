---
title: Monitorando Recursos do Servidor Usando o Console JMX
seo-title: Monitorando Recursos do Servidor Usando o Console JMX
description: Saiba como monitorar os recursos do servidor usando o console JMX.
seo-description: Saiba como monitorar os recursos do servidor usando o console JMX.
uuid: 0a28aafe-61b2-472b-8f8f-2cd6540cbfee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 873ce073-0055-4e1b-b3c6-ae7967700894
docset: aem65
translation-type: tm+mt
source-git-commit: f64eb57a69f2124523bd6eaed3e2f58a54c1ea8e
workflow-type: tm+mt
source-wordcount: '4989'
ht-degree: 1%

---


# Monitorando Recursos do Servidor Usando o Console JMX{#monitoring-server-resources-using-the-jmx-console}

O Console JMX permite que você monitore e gerencie serviços no servidor CRX. As seções a seguir resumem os atributos e operações expostos por meio da estrutura JMX.

Para obter informações sobre como usar os controles do console, consulte [Uso do console](#using-the-jmx-console)JMX. Para obter informações sobre JMX, consulte a página da tecnologia [](https://www.oracle.com/technetwork/java/javase/tech/javamanagement-140525.html) Java Management Extensions (JMX) no site da Oracle.

Para obter informações sobre como criar MBeans para gerenciar seus serviços usando o Console JMX, consulte [Integrar serviços ao console](/help/sites-developing/jmx-integration.md)JMX.

## Manutenção do fluxo de trabalho {#workflow-maintenance}

Operações para administrar instâncias de fluxo de trabalho em execução, concluídas, obsoletas e com falha.

* Domínio: com.adobe.granite.workflow
* Tipo: Manutenção

>[!NOTE]
>
>Consulte o console [de](/help/sites-administering/workflows-administering.md) fluxo de trabalho para obter ferramentas adicionais de administração de fluxo de trabalho e descrições de possíveis status de instâncias de fluxo de trabalho.

### Operações {#operations}

**listRunningWorkflowsPerModel** Lista o número de instâncias de fluxo de trabalho que estão sendo executadas para cada modelo de fluxo de trabalho.

* Argumentos: none
* Valor retornado: Dados tabulares contendo as colunas Count e ModelId.

**listCompletedWorkflowsPerModel** Lista o número de instâncias de fluxo de trabalho concluídas para cada modelo de fluxo de trabalho.

* Argumentos: none
* Valor retornado: Dados tabulares contendo as colunas Count e ModelId.

**returnWorkflowQueueInfo** Lista informações sobre itens de fluxo de trabalho que foram processados e que estão na fila para processamento.

* Argumentos: none
* Valor retornado: Dados tabulares contendo as seguintes colunas:

   * Tarefas
   * Nome da fila
   * Tarefas ativas
   * Tempo Médio de Processamento
   * Tempo médio de espera
   * Trabalhos cancelados
   * Trabalhos com falhas
   * Trabalhos concluídos
   * Trabalhos processados
   * Tarefas em Fila

**Listas returnWorkflowJobTopicInfo** processam informações para trabalhos de fluxo de trabalho, organizadas por tópico.

* Argumentos: none
* Valor retornado: Dados tabulares contendo as seguintes colunas:

   * Nome do tópico
   * Tempo Médio de Processamento
   * Tempo médio de espera
   * Trabalhos cancelados
   * Trabalhos com falhas
   * Trabalhos concluídos
   * Trabalhos processados

**returnFailedWorkflowCount** Mostra o número de instâncias de fluxo de trabalho que falharam. Você pode especificar um modelo de fluxo de trabalho para query ou recuperar informações para todos os modelos de fluxo de trabalho.

* Argumentos:

   * modelo: A ID do modelo para o query. Para ver uma contagem de instâncias de fluxo de trabalho com falha para todos os modelos de fluxo de trabalho, não especifique nenhum valor. A ID é o caminho para o nó modelo, por exemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor retornado: O número de instâncias de fluxo de trabalho com falha.

**returnFailedWorkflowCountPerModel** Mostra o número de instâncias de fluxo de trabalho que falharam para cada modelo de fluxo de trabalho.

* Argumentos: nenhum.
* Valor retornado: Dados tabulares contendo as colunas Contagem e ID do modelo.

**termineAs instâncias de fluxo de trabalho de terminação** deInstânciasque falharam. Você pode encerrar todas as instâncias que falharam ou apenas as que falharam para um modelo específico. Como opção, você pode reiniciar as instâncias depois que elas forem terminadas. Você também pode testar a operação para ver os resultados sem realmente executar a operação.

* Argumentos:

   * Reinicie a instância: (Opcional) Especifique um valor de `true` para reiniciar as instâncias depois de terminadas. O valor padrão de não `false` resulta na reinicialização de instâncias de fluxo de trabalho finalizadas.
   * Corrida seca: (Opcional) Especifique um valor de `true` para ver os resultados da operação sem realmente executar a operação. O valor padrão de `false` faz com que a operação seja executada.
   * Modelo: (Opcional) A ID do modelo ao qual a operação é aplicada. Não especifique nenhum modelo para aplicar a operação às instâncias que falharam de todos os modelos de fluxo de trabalho. A ID é o caminho para o nó modelo, por exemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor retornado: Dados tabulares sobre as instâncias terminadas, contendo as seguintes colunas:

   * Iniciador
   * InstanceId
   * ModelId
   * Carga
   * StartComment
   * WorkflowTitle

**retryFailedWorkItems** Tenta executar etapas de item de trabalho que falharam. Você pode repetir todos os itens de trabalho com falha ou apenas os itens de trabalho com falha para um modelo de fluxo de trabalho específico. Você opcionalmente testa a operação para ver os resultados sem executar a operação.

* Argumentos:

   * Corrida seca: (Opcional) Especifique um valor de `true` para ver os resultados da operação sem realmente executar a operação. O valor padrão de `false` faz com que a operação seja executada.
   * Modelo: (Opcional) A ID do modelo ao qual a operação é aplicada. Não especifique nenhum modelo para aplicar a operação aos itens de trabalho com falha de todos os modelos de fluxo de trabalho. A ID é o caminho para o nó modelo, por exemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor retornado: Dados tabulares sobre os itens de trabalho com falha que são repetidos, incluindo as seguintes colunas:

   * Iniciador
   * InstanceId
   * ModelId
   * Carga
   * StartComment
   * WorkflowTitle

**ExpurgarAtivo** Remove instâncias de fluxo de trabalho ativas de uma página específica. Você pode expurgar instâncias ativas para todos os modelos ou apenas as instâncias para um modelo específico. Como opção, você pode testar a operação para ver os resultados sem realmente executar a operação.

* Argumentos:

   * Modelo: (Opcional) A ID do modelo ao qual a operação é aplicada. Não especifique nenhum modelo para aplicar a operação às instâncias de fluxo de trabalho de todos os modelos de fluxo de trabalho. A ID é o caminho para o nó modelo, por exemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Número de dias desde que o fluxo de trabalho foi iniciado: A idade das instâncias do fluxo de trabalho a serem expurgadas, em dias.
   * Corrida seca: (Opcional) Especifique um valor de `true` para ver os resultados da operação sem realmente executar a operação. O valor padrão de `false` faz com que a operação seja executada.

* Valor retornado: Dados tabulares sobre as instâncias de fluxo de trabalho ativas que são expurgadas, incluindo as seguintes colunas:

   * Iniciador
   * InstanceId
   * ModelId
   * Carga
   * StartComment
   * WorkflowTitle

**countStaleWorkflows** Retorna o número de instâncias de fluxo de trabalho que são obsoletas. Você pode recuperar o número de instâncias obsoletas para todos os modelos de fluxo de trabalho ou para um modelo específico.

* Argumentos:

   * Modelo: (Opcional) A ID do modelo ao qual a operação é aplicada. Não especifique nenhum modelo para aplicar a operação às instâncias de fluxo de trabalho de todos os modelos de fluxo de trabalho. A ID é o caminho para o nó modelo, por exemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor retornado: O número de instâncias de fluxo de trabalho obsoletas.

**restartStaleWorkflows** Reinicializa instâncias de fluxo de trabalho obsoletas. É possível reiniciar todas as instâncias obsoletas ou apenas as obsoletas para um modelo específico. Você também pode testar a operação para ver os resultados sem realmente executar a operação.

* Argumentos:

   * Modelo: (Opcional) A ID do modelo ao qual a operação é aplicada. Não especifique nenhum modelo para aplicar a operação às instâncias obsoletas de todos os modelos de fluxo de trabalho. A ID é o caminho para o nó modelo, por exemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Corrida seca: (Opcional) Especifique um valor de `true` para ver os resultados da operação sem realmente executar a operação. O valor padrão de `false` faz com que a operação seja executada.

* Valor retornado: Uma lista de instâncias de fluxo de trabalho que são reiniciadas.

**fetchModelList** Lista todos os modelos de fluxo de trabalho.

* Argumentos: none
* Valor retornado: Dados tabulares que identificam os modelos de fluxo de trabalho, incluindo as colunas ModelId e ModelName.

**countRunningWorkflows** Retorna o número de instâncias de fluxo de trabalho que estão sendo executadas. Você pode recuperar o número de instâncias em execução para todos os modelos de fluxo de trabalho ou para um modelo específico.

* Argumentos:

   * Modelo: (Opcional) A ID do modelo para o qual o número de instâncias em execução é retornado. Não especifique nenhum modelo para retornar o número de instâncias em execução de todos os modelos de fluxo de trabalho. A ID é o caminho para o nó modelo, por exemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor retornado: O número de instâncias de fluxo de trabalho em execução.

**countCompletedWorkflows** Retorna o número de instâncias de fluxo de trabalho concluídas. Você pode recuperar o número de instâncias concluídas para todos os modelos de fluxo de trabalho ou para um modelo específico.

* Argumentos:

   * Modelo: (Opcional) A ID do modelo para o qual o número de instâncias concluídas é retornado. Não especifique nenhum modelo para retornar o número de instâncias concluídas de todos os modelos de fluxo de trabalho. A ID é o caminho para o nó modelo, por exemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor retornado: O número de instâncias de fluxo de trabalho concluídas.

**purgeCompletedRemove registros de workflows concluídos de uma página específica do repositório.** Use essa operação periodicamente para minimizar o tamanho do repositório quando você fizer uso intenso de workflows. Você pode expurgar instâncias concluídas para todos os modelos ou apenas as instâncias para um modelo específico. Como opção, você pode testar a operação para ver os resultados sem realmente executar a operação.

* Argumentos:

   * Modelo: (Opcional) A ID do modelo ao qual a operação é aplicada. Não especifique nenhum modelo para aplicar a operação às instâncias de fluxo de trabalho de todos os modelos de fluxo de trabalho. A ID é o caminho para o nó modelo, por exemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Número de dias desde a conclusão do fluxo de trabalho: O número de dias em que as instâncias do fluxo de trabalho estão no estado concluído.
   * Corrida seca: (Opcional) Especifique um valor de `true` para ver os resultados da operação sem realmente executar a operação. O valor padrão de `false` faz com que a operação seja executada.

* Valor retornado: Dados tabulares sobre as instâncias de fluxo de trabalho concluídas que são expurgadas, incluindo as seguintes colunas:

   * Iniciador
   * InstanceId
   * ModelId
   * Carga
   * StartComment
   * WorkflowTitle

## Repositório {#repository}

Informações sobre o repositório CRX

* Domínio: com.adobe.granite
* Tipo: Repositório

### Atributos {#attributes}

**Nome** O nome da implementação do repositório JCR. Somente leitura.

**Versão** A versão de implementação do repositório. Somente leitura.

**HomeDir** O diretório no qual o repositório está localizado. O local padrão é &lt;QuickStart_Jar_Location>/crx-quickstart/repository. Somente leitura.

**Nome** do cliente O nome do cliente para o qual a licença de software é emitida. Somente leitura.

**LicenseKey** A chave de licença exclusiva para esta instalação do repositório. Somente leitura.

**AvailableDiskSpace** O espaço em disco disponível para esta instância do repositório, em Mbytes. Somente leitura.

**MaximumNumberOfOpenFiles** O número de arquivos que podem ser abertos de uma vez. Somente leitura.

**SessionTracker** O valor da variável de sistema crx.debug.session. true indica uma sessão de depuração. false indica uma sessão normal. Leitura/gravação.

**Descritores** Um conjunto de pares de valores chave que representam as propriedades do repositório. Todas as propriedades são somente leitura.

<table>
 <tbody>
  <tr>
   <th>Chave</th>
   <th>Valor</th>
  </tr>
  <tr>
   <td>option.node.and.property.with.same.name.supported</td>
   <td>Indica se um nó e uma propriedade do nó podem ter o mesmo nome. true indica que os mesmos nomes são suportados; false indica que não é suportado. </td>
  </tr>
  <tr>
   <td>identifier.stability</td>
   <td>Indica a estabilidade dos identificadores de nó não referenciáveis. Os seguintes valores são possíveis:
    <ul>
     <li>identifier.stability.indefined.duration: Os identificadores não são alterados.</li>
     <li>identifier.stability.method.duration: Os identificadores podem alterar entre chamadas de método.</li>
     <li>identifier.stability.save.duration: Os identificadores não são alterados em um ciclo de salvamento/atualização.</li>
     <li>identifier.stability.session.duration: Os identificadores não são alterados durante uma sessão.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>query.xpath.pos.index</td>
   <td>Indica se o idioma do query JCR 1.0 XPath é suportado. true indica suporte e false indica que não há suporte.</td>
  </tr>
  <tr>
   <td>crx.repository.systemid</td>
   <td>O identificador do sistema, conforme encontrado no arquivo system.id.</td>
  </tr>
  <tr>
   <td>option.query.sql.supported</td>
   <td>Indica se o idioma do query JCR 1.0 XPath é suportado. true indica suporte e false indica que não há suporte.</td>
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
   <td>Indica se o gerenciamento de tipo de nó é suportado. true indica que é suportado e false indica que não há suporte.</td>
  </tr>
  <tr>
   <td>node.type.management.overrides.supported</td>
   <td>Indica se você pode substituir a propriedade herdada ou a definição de nó filho de um tipo de nó. true indica que as substituições são suportadas e false indica que não há substituições.</td>
  </tr>
  <tr>
   <td>option.observation.supported</td>
   <td>true indica que há suporte para a observação assíncrona de alterações no repositório. O suporte à observação assíncrona permite que os aplicativos recebam e respondam a notificações sobre cada alteração à medida que elas ocorrem.</td>
  </tr>
  <tr>
   <td>query.jcrscore</td>
   <td><p>true indica que a pseudo-propriedade jcr:score está disponível em query XPath e SQL que incluem uma função jcrfn:contains (in XPath) ou CONTAINS (in SQL) para executar uma pesquisa de texto completo.</p> </td>
  </tr>
  <tr>
   <td>option.simple.versioning.supported</td>
   <td>true indica que o repositório oferece suporte ao controle de versão simples. Com o controle de versão simples, o repositório mantém uma série sequencial de versões de um nó.</td>
  </tr>
  <tr>
   <td>option.workspace.management.supported</td>
   <td>true indica que o repositório oferece suporte à criação e exclusão de espaços de trabalho usando APIs.</td>
  </tr>
  <tr>
   <td>option.update.mixin.node.types.supported</td>
   <td>true indica que o repositório oferece suporte à adição e remoção de tipos de nós de mixin de um nó existente.</td>
  </tr>
  <tr>
   <td>node.type.management.primary.item.name.supported</td>
   <td>true indica que o repositório permite que as definições de nó contenham um item principal como filho. Um item principal é acessível usando a API sem saber o nome do item.</td>
  </tr>
  <tr>
   <td>level.2.supported</td>
   <td>true indica que LEVEL_1_SUPPORTED e OPTION_XML_IMPORT_SUPPORTED são verdadeiros.</td>
  </tr>
  <tr>
   <td>write.supported</td>
   <td>true indica que o repositório fornece acesso de gravação usando a API. false indica acesso somente leitura.</td>
  </tr>
  <tr>
   <td>node.type.management.update.in.use.supported</td>
   <td>true indica que você pode alterar as definições de nó que estão em uso pelos nós existentes.</td>
  </tr>
  <tr>
   <td>jcr.specification.version</td>
   <td>A versão da especificação JCR que o repositório implementa.</td>
  </tr>
  <tr>
   <td>option.journaled.observation.supported</td>
   <td>true indica que os aplicativos podem executar observação em log do repositório. com observação em diário, pode ser obtido um conjunto de notificações de variações por um período de tempo específico. </td>
  </tr>
  <tr>
   <td>query.languages</td>
   <td>Os idiomas de query suportados pelo repositório. Nenhum valor indica que não há suporte para query.</td>
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
   <td>true indica que o repositório oferece suporte ao controle de acesso, para definir e determinar os privilégios do usuário para acesso a nós.</td>
  </tr>
  <tr>
   <td>option.baselines.supported</td>
   <td>true indica que o repositório suporta configurações e linhas de base.</td>
  </tr>
  <tr>
   <td>option.shareable.nodes.supported</td>
   <td>true indica que o repositório suporta a criação de nós compartilháveis.</td>
  </tr>
  <tr>
   <td>crx.cluster.id</td>
   <td>O identificador do cluster do repositório.</td>
  </tr>
  <tr>
   <td>query.stored.queries.supported</td>
   <td>true indica que o repositório suporta query armazenados.</td>
  </tr>
  <tr>
   <td>query.full.text.search.supported</td>
   <td>true indica que o repositório oferece suporte à pesquisa de texto completo.</td>
  </tr>
  <tr>
   <td>node.type.management.inheritance</td>
   <td><p>Indica o nível de suporte do repositório para a herança do tipo de nó. Os seguintes valores são possíveis:</p> <p>node.type.management.hereitance.Minimum: O registro dos tipos de nó primário é limitado àqueles que têm apenas nt:base como um supertipo. O registro de tipos de nó de mistura é limitado àqueles sem supertipo.</p> <p>node.type.management.hereitance.single: O registro dos tipos de nó primário é limitado àqueles com um supertipo. O registro de tipos de nó de mistura é limitado àqueles com no máximo um supertipo.</p> <p><br /> node.type.management.hereitance.multiple: Os tipos de nós primários podem ser registrados com um ou mais supertipos. Os tipos de nós de mistura podem ser registrados com zero ou mais supertipos.</p> </td>
  </tr>
  <tr>
   <td>crx.cluster.preferredMaster</td>
   <td>true indica que esse nó de cluster é o mestre preferencial do cluster.</td>
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
   <td>true indica que o repositório suporta restrições de valor para propriedades de nó.</td>
  </tr>
  <tr>
   <td>node.type.management.property.types</td>
   <td>uma matriz de constantes javax.jcr.PropertyType que representam os tipos de propriedade que um tipo de nó registrado pode especificar. Uma matriz de comprimento zero indica que os tipos de nó registrados não podem especificar definições de propriedade. Os tipos de propriedade são STRING, URI, BOOLEAN, LONG, DUPLO, DECIMAL, BINARY, DATE, NAME, PATH, WEAKREFERENCE, REFERENCE e UNDEFINED (se suportado)</td>
  </tr>
  <tr>
   <td>node.type.management.orderable.child.nodes.supported</td>
   <td>true indica que o repositório oferece suporte à preservação da ordem dos nós secundários.</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor</td>
   <td>O nome do fornecedor do repositório.</td>
  </tr>
  <tr>
   <td>query.joins</td>
   <td><p>O nível de suporte para joins em query. Os seguintes valores são possíveis:</p>
    <ul>
     <li>query.joins.none: Não há suporte para joins. Query podem usar um seletor.</li>
     <li>query.joins.inner: Suporte para entradas internas.</li>
     <li>query.joins.inner.external: Suporte para entradas internas e externas.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>org.apache.jackrabbit.spi.commons.AdditionalEventInfo</td>
   <td> </td>
  </tr>
  <tr>
   <td>query.xpath.doc.order</td>
   <td>true indica que o repositório suporta a linguagem do query XPath 1.0.</td>
  </tr>
  <tr>
   <td>query.jcrpath</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.xml.import.supported</td>
   <td>true indica que o repositório suporta a importação do código XML como conteúdo.</td>
  </tr>
  <tr>
   <td>node.type.management.same.name.siblings.supported</td>
   <td>true indica que o repositório suporta nós irmãos (nós com o mesmo pai) com os mesmos nomes.</td>
  </tr>
  <tr>
   <td>node.type.management.residual.definitions.supported</td>
   <td>true indica que o repositório suporta propriedades de nome com definições residuais. Quando suportado, o atributo name de uma definição de item pode ser um asterisco ("*").</td>
  </tr>
  <tr>
   <td>node.type.management.autocreated.definitions.supported</td>
   <td>true indica que o repositório suporta a criação automática de itens filhos (nós ou propriedades) de um nó quando o nó é criado.</td>
  </tr>
  <tr>
   <td>crx.cluster.master</td>
   <td>true indica que esse nó de repositório é o nó mestre do cluster.</td>
  </tr>
  <tr>
   <td>level.1.supported</td>
   <td>true indica que option.xml.export.support é true e query.languages tem comprimento diferente de zero.</td>
  </tr>
  <tr>
   <td>option.unfiled.content.supported</td>
   <td>true indica que o repositório suporta conteúdo não arquivado. Os nós não arquivados não fazem parte da hierarquia do repositório.</td>
  </tr>
  <tr>
   <td>jcr.specification.name</td>
   <td>O nome da especificação JCR que o repositório implementa.</td>
  </tr>
  <tr>
   <td>option.versioning.supported</td>
   <td>true indica que o repositório oferece suporte ao controle de versão completo.</td>
  </tr>
  <tr>
   <td>jcr.repository.name</td>
   <td>O nome do repositório.</td>
  </tr>
  <tr>
   <td>option.locking.supported</td>
   <td>true indica que o repositório suporta o bloqueio de nós. O bloqueio permite que um usuário impeça temporariamente outros usuários de fazer alterações.</td>
  </tr>
  <tr>
   <td>jcr.repository.version.display</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.activities.supported</td>
   <td>true indica que o repositório suporta atividade. O Atividade é um conjunto de alterações executadas em um espaço de trabalho que são mescladas em outro espaço de trabalho.</td>
  </tr>
  <tr>
   <td>node.type.management.multivalued.properties.supported</td>
   <td>true indica que o repositório suporta propriedades de nó que podem ter zero ou mais valores.</td>
  </tr>
  <tr>
   <td>option.retention.supported</td>
   <td>true indica que o repositório suporta o uso de aplicativos externos de gerenciamento de retenção para aplicar políticas de retenção ao conteúdo e oferece suporte para retenção e liberação.</td>
  </tr>
  <tr>
   <td>option.lifecycle.supported</td>
   <td>true indica que o repositório oferece suporte ao gerenciamento do ciclo de vida.</td>
  </tr>
 </tbody>
</table>

**WorkspaceNames** Os nomes dos espaços de trabalho no repositório. Somente leitura.

**DataStoreGarbageCollectionDelay** A quantidade de tempo em milissegundos que a coleta de lixo dorme após a varredura de cada décimo nó. Leitura/gravação.

**BackupDelay** A quantidade de tempo em milissegundos que o processo de backup permanece entre cada etapa do backup. Leitura/gravação.

**BackupInProgress** Um valor true indica que um processo de backup está sendo executado. Somente leitura.

**BackupProgress** Para o backup atual, a porcentagem de todos os arquivos que foram submetidos a backup. Somente leitura.

**CurrentBackupTarget** Para o backup atual, o arquivo ZIP no qual os arquivos de backup estão sendo armazenados. Quando um backup não está em andamento, nenhum valor é exibido. Somente leitura.

**BackupwasSuccessful** Um valor true indica que não ocorreram erros durante o backup atual ou que nenhum backup está em andamento. false indica que ocorreu um erro durante o backup atual. Somente leitura.

**BackupResult** O status do backup atual. Os seguintes valores são possíveis:

* Backup em andamento: Um backup está sendo executado no momento.
* Backup cancelado: O backup foi cancelado.
* Backup concluído com erro: Ocorreu um erro durante o backup. A mensagem de erro fornece informações sobre a causa.
* Backup concluído: O backup foi bem-sucedido.
* Nenhum backup executado até o momento: Não há backup em andamento.

Somente leitura.

**TarOtimizationRunningSince** A hora em que o processo de otimização de arquivo TAR atual começou. Somente leitura.

**TarOtimizationDelay** A quantidade de tempo em milissegundos que o processo de otimização TAR permanece entre cada etapa do processo. Leitura/gravação.

**ClusterProperties** Um conjunto de pares de valores chave que representam propriedades e valores do cluster. Cada linha na tabela representa uma propriedade de cluster. Somente leitura.

**ClusterNodes** Os membros do cluster de repositório.

**ClusterId** O identificador deste cluster de repositório. Somente leitura.

**ClusterMasterId** O identificador do nó mestre deste cluster de repositório. Somente leitura.

**ClusterNodeId** O identificador deste nó do cluster de repositório. Somente leitura.

### Operações {#operations-1}

**createWorkspace** Cria um espaço de trabalho neste repositório.

* Argumentos:

   * name: Um valor String que representa o nome do novo espaço de trabalho.

* Valor retornado: none

**runDataStoreGarbageCollection** Executa a coleta de lixo nos nós do repositório.

* Argumentos:

   * excluir: Um valor booliano que indica se os itens do repositório não utilizados devem ser excluídos. Um valor true causa a exclusão de nós e propriedades não utilizados. Um valor de false faz com que todos os nós sejam digitalizados, mas nenhum é excluído.

* Valor retornado: none

**stopDataStoreGarbageCollection** Interrompe uma coleta de lixo do armazenamento de dados em execução.

* Argumentos: none
* Valor retornado: representação de string do status atual

**startBackup** faz backup dos dados do repositório em um arquivo ZIP.

* Argumentos:

   * `target`: (Opcional) Um `String` valor que representa o nome do arquivo ZIP ou diretório no qual arquivar os dados do repositório. Para usar um arquivo ZIP, inclua a extensão do nome do arquivo ZIP. Para usar um diretório, não inclua nenhuma extensão de nome de arquivo.

      Para executar um backup incremental, especifique o diretório que foi usado anteriormente para o backup.

      Você pode especificar um caminho absoluto ou relativo. Os caminhos relativos são relativos ao pai do diretório crx-quickstart.

      Quando você não especifica nenhum valor, o valor padrão de `backup-currentdate.zip` é usado, onde `currentdate` está no formato `yyyyMMdd-HHmm`.

* Valor retornado: none

**cancelBackup** Interrompe o processo de backup atual e exclui o arquivamento temporário criado pelo processo para arquivamento de dados.

* Argumentos: none
* Valor retornado: none

**blockRepositoryWrites** Bloqueia alterações nos dados do repositório. Todos os ouvintes de backup do repositório são notificados do bloqueio.

* Argumentos: none
* Valor retornado: none

**unblockRepositoryWrites** Remove o bloco do repositório. Todos os ouvintes de backup do repositório são notificados da remoção do bloco.

* Argumentos: none
* Valor retornado: none

**startTarOtimization** Start o processo de otimização de arquivos TAR usando o valor padrão para tarOtimizationDelay.

* Argumentos: none
* Valor retornado: none

**stopTarOtimization** Interrompe a otimização do arquivo TAR.

* Argumentos: none
* Valor retornado: none

**tarIndexMerge** mescla os arquivos de índice principais de todos os conjuntos TAR. Os arquivos de índice principais são arquivos com versões principais diferentes. Por exemplo, os seguintes arquivos são mesclados no arquivo index_3_1.tar: index_1_1.tar, index_2_0.tar, index_3_0.tar. Os arquivos que foram mesclados são excluídos (no exemplo anterior, index_1_1.tar, index_2_0.tar e index_3_0.tar são excluídos).

* Argumentos:

   * `background`: Um valor booliano que indica se a operação deve ser executada em segundo plano para que o Console da Web possa ser utilizado durante a execução. Um valor de true executa a operação em segundo plano.

* Valor retornado: none

**tornarClusterMaster** Define este nó de repositório como o nó mestre do cluster. Se ainda não for mestre, esse comando interrompe o ouvinte da instância mestre atual e start um ouvinte mestre no nó atual. Esse nó é definido como o nó mestre e reiniciado, fazendo com que todos os outros nós do cluster (ou seja, aqueles controlados pelo mestre) se conectem a essa instância.

* Argumentos: none
* Valor retornado: none

**joinCluster** Adiciona este repositório a um cluster como um nó controlado pelo mestre de cluster. Você deve fornecer um nome de usuário e senha para fins de autenticação. A conexão usa autenticação básica. As credenciais de segurança são codificadas em base 64 antes de serem enviadas para o servidor.

* Argumentos:

   * `master`: Um valor de string que representa o endereço IP ou o nome do computador do computador que executa o nó do repositório mestre.
   * `username`: O nome a ser usado para autenticação com o cluster.
   * `password`: A senha a ser usada para autenticação.

* Valor retornado: none

**traversalCheck** Atravesses e, opcionalmente, corrige inconsistências em uma subárvore que começa em um nó específico. Isso é abordado em detalhes na documentação sobre Gerentes de persistência.

**verificaçãoConsistência** Verifica e, opcionalmente, corrige a consistência no armazenamento de dados. Isso é abordado em detalhes na documentação do Datastore.

## Estatísticas do repositório (TimeSeries) {#repository-statistics-timeseries}

O valor do campo TimeSeries para cada tipo de estatística que `org.apache.jackrabbit.api.stats.RepositoryStatistics` define.

* Domínio: `com.adobe.granite`
* Tipo: `TimeSeries`
* Nome: Um dos seguintes valores da classe `org.apache.jackrabbit.api.stats.RepositoryStatistics.Type` Enum:

   * BUNDLE_CACHE_ACCESS_COUNTER
   * BUNDLE_CACHE_MISS_MÉDIA
   * BUNDLE_CACHE_MISS_COUNTER
   * BUNDLE_CACHE_MISS_DURATION
   * BUNDLE_CACHE_SIZE_COUNTER
   * BUNDLE_COUNTER
   * BUNDLE_READ_COUNTER
   * BUNDLE_WRITE_MÉDIA
   * BUNDLE_WRITE_COUNTER
   * BUNDLE_WRITE_DURATION
   * BUNDLE_WS_SIZE_COUNTER
   * QUERY_MÉDIA
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

* ValuePerSecond: O valor medido por segundo no último minuto. Somente leitura.
* ValorPorMinuto: O valor medido por minuto durante a última hora. Somente leitura.
* ValorPorHora: O valor medido por hora na última semana. Somente leitura.
* ValorPorSemana: O valor medido por semana durante os últimos três anos. Somente leitura.

## Estatísticas do Query do repositório {#repository-query-stats}

Informações estatísticas sobre query de repositório.

* Domínio: com.adobe.granite
* Tipo: QueryStat

### Atributos {#attributes-2}

**SlowQueries** Informações sobre os query do repositório que demoraram mais tempo para serem concluídos. Somente leitura.

**SlowQueriesQueueSize** O número máximo de query a serem incluídos na lista SlowQueries. Leitura-gravação.

**PopularQueries** Informações sobre os query do repositório que mais ocorreram. Somente leitura.

**PopularQueriesQueueSize** O número máximo de query na lista PopularQueries. Leitura-gravação.

### Operações {#operations-2}

**clearSlowQueriesQueue** Remove todos os query da lista SlowQueries.

* Argumentos: none
* Valor retornado: none

**clearPopularQueriesQueue** Remove todos os query da lista PopularQueries.

* Argumentos: none
* Valor retornado: none

## Agentes de replicação {#replication-agents}

Monitore os serviços de cada agente de replicação. Quando você cria um agente de replicação, o serviço aparece automaticamente no console JMX.

* **Domínio:** com.adobe.granite.Replication
* **Tipo:** agente
* **Nome:** sem valor
* **Propriedades:** {id=&quot;*Name*&quot;}, onde *Name* é o valor da propriedade agent Name.

### Atributos {#attributes-3}

**Id** Um valor String que representa o identificador da configuração do agente de replicação. Vários agentes podem usar a mesma configuração. Somente leitura.

**Válido** Um valor booliano que indica se o agente está configurado corretamente:

* `true`: Configuração válida.
* `false` : A configuração contém erros.

Somente leitura.

**Ativado** Um valor booliano que indica se o agente está ativado:

* `true`: Ativado.
* `false`: Desativado.

**QueueBlocked** Um valor booliano que indica se a fila existe e está bloqueada:

* `true`: Bloqueado. Uma nova tentativa automática está pendente.
* `false`: Não bloqueado ou não existe.

Somente leitura.

**QueuePaused** Um valor booliano que indica se a fila de trabalhos está pausada:

* `true`: Pausado (suspenso)
* `false`: Não pausado ou não existe.

Leitura-gravação.

**QueueNumEntries** Um valor int que representa o número de trabalhos na fila do agente. Somente leitura.

**QueueStatusTime** Um valor de Data que indica a hora no servidor quando os valores de status exibidos foram obtidos. O valor corresponde ao tempo que a página foi carregada. Somente leitura.

**QueueNextRetryTime** Para filas bloqueadas, um valor de Data que indica quando a próxima nova tentativa automática ocorre. Quando nenhuma hora for exibida, a fila não será bloqueada. Somente leitura.

**QueueProcessingSince** Um valor de Data que indica quando o processamento começou para a tarefa atual. Quando nenhuma hora for exibida, a fila estará bloqueada ou ociosa. Somente leitura.

**QueueLastProcessTime** Um valor de Data que indica quando o trabalho anterior foi concluído. Somente leitura.

### Operações {#operations-3}

**queueForceRetry** Para filas bloqueadas, emite o comando tentar novamente para a fila.

* Argumentos: none
* Valor retornado: none

**queueClear** Remove todos os trabalhos da fila.

* Argumentos: none
* Valor retornado: none

## Mecanismo Sling {#sling-engine}

Fornece estatísticas sobre solicitações HTTP para que você possa monitorar o desempenho do serviço SlingRequestProcessor.

* Domínio: org.apache.sling
* Tipo: motor
* Propriedades: {service=RequestProcessor}

### Atributos {#attributes-4}

**RequestsCount** O número de solicitações que ocorreram desde a última redefinição das estatísticas.

**MinRequestDurationMsec** O menor tempo (em milissegundos) necessário para processar uma solicitação desde a última redefinição das estatísticas.

**MaxRequestDuratioMsec** O maior tempo (em milissegundos) necessário para processar uma solicitação desde que as estatísticas foram redefinidas pela última vez.

**StandardDeviationDurationMsec** O desvio padrão da quantidade de tempo necessário para processar solicitações. O desvio padrão é calculado usando todas as solicitações desde a última redefinição das estatísticas.

**MeanRequestDurationMsec** O tempo médio necessário para processar uma solicitação. A média é calculada usando todas as solicitações desde que as estatísticas foram redefinidas pela última vez

### Operações {#operations-4}

**resetStatistics** Define todas as estatísticas como zero. Redefina as estatísticas quando precisar analisar o desempenho do processamento da solicitação durante um período de tempo específico.

* Argumentos: none
* Valor retornado: none

**id** A representação String da ID do pacote.

**instalado** Um valor booliano que indica se o pacote está instalado:

* `true`: Instalado.
* `false`: Não instalado.

**installedBy** A ID do usuário que instalou o pacote pela última vez.

**installedDate** A data em que o pacote foi instalado pela última vez.

**tamanho** Um valor longo que retém o tamanho do pacote em bytes.


## Iniciador do Quickstart {#quickstart-launcher}

Informações sobre o processo de inicialização e o iniciador do Quickstart.

* Domínio: com.adobe.granite.quickstart
* Tipo: Iniciador

### Operações {#operations-5}

**registro**

Exibe uma mensagem na janela QuickStart.

Argumentos:

* p1: Um `String` valor que representa a mensagem a ser exibida. A ilustração a seguir mostra o resultado da chamada `log` com um valor p1 de `this is a log message`.

![lavoura](assets/launcheruilog.png)

* Valor retornado: none

**startupFinished**

Chama o método startupFinished do iniciador do servidor. O método tenta abrir a página de boas-vindas em um navegador da Web.

* Argumentos: none
* Valor retornado: none

**startupProgress**

Define o valor de conclusão do processo de inicialização do servidor. A barra de progresso na janela QuickStart representa o valor de conclusão.

* Argumentos:

   * p1: Um valor flutuante que representa quanto do processo de inicialização é concluído, como uma fração. O valor deve estar entre zero e um. Por exemplo, 0.3 indica 30% de conclusão.

* Valor retornado: nenhum.

![lavoura](assets/launcherprogress.png)

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
   <td>ImplementaçãoJMI</td>
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
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/package-summary.html">pacote javax.management</a></td>
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
   <td><a href="https://osgi.org/specification/osgi.enterprise/7.0.0/service.jmx.html#d0e42567">org.osgi.jmx.framework</a> package</td>
  </tr>
 </tbody>
</table>

## Usando o console JMX {#using-the-jmx-console}

O Console JMX exibe informações sobre vários serviços que estão sendo executados no servidor:

* Atributos: Propriedades do serviço, como configurações ou dados de tempo de execução. Os atributos podem ser somente leitura ou leitura/gravação.
* Operações: Comandos que você pode chamar no serviço.

Os MBeans implantados com um serviço OSGi expõem os atributos e as operações do serviço ao console. O MBean determina os atributos e as operações que são expostos e se os atributos são somente leitura ou leitura/gravação.

A página principal do console JMX inclui uma tabela de serviços. Cada linha na tabela representa um serviço exposto por um MBean.

1. Abra o Console da Web e clique na guia JMX. ([http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
2. Clique em um valor de célula para um serviço para ver os atributos e as operações do serviço.
3. Para alterar um valor de atributo, clique no valor, especifique o valor na caixa de diálogo exibida e clique em Salvar.
4. Para invocar uma operação de serviço, clique no nome da operação, especifique os valores do argumento na caixa de diálogo que é exibida e clique em Chamar.

## Uso de aplicativos JMX externos para monitoramento {#using-external-jmx-applications-for-monitoring}

O CRX permite que aplicativos externos interajam com o Managed Beans (MBeans) via JMX ( [Java Management Extensions)](https://docs.oracle.com/javase/6/docs/technotes/guides/management/overview.html). O uso de consoles genéricos, como o [JConsole](https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html) ou aplicativos de monitoramento específicos do domínio, permite obter e definir configurações e propriedades do CRX, bem como o monitoramento do desempenho e do uso de recursos.

### Usando o JConsole para se conectar ao CRX {#using-jconsole-to-connect-to-crx}

Para se conectar ao CRX usando o JConsole, siga estas etapas:

1. Abra uma janela de terminal.
1. Digite o seguinte comando:

   `jconsole`

O JConsole será start e a janela JConsole será exibida.

### Conexão com um processo CRX local {#connecting-to-a-local-crx-process}

O JConsole exibirá uma lista de processos locais do Java Virtual Machine. A lista conterá dois processos de início rápido. Selecione o processo de início rápido &quot;CRIANÇA&quot; na lista de processos locais (geralmente aquele com PID superior).

![screen_shot_2012-03-26at114557am](assets/screen_shot_2012-03-26at114557am.png)

### Conexão a um processo CRX remoto {#connecting-to-a-remote-crx-process}

Para se conectar a um processo CRX remoto, a JVM que hospeda o processo CRX remoto precisará ser habilitada para aceitar conexões JMX remotas.

Para habilitar conexões JMX remotas, a seguinte propriedade do sistema deve ser definida ao iniciar a JVM:

`com.sun.management.jmxremote.port=portNum`

Na propriedade acima, `portNum` é o número da porta através da qual você deseja ativar conexões RMI JMX. Especifique um número de porta não utilizado. Além de publicar um conector RMI para acesso local, definir essa propriedade publica um conector RMI adicional em um registro privado somente leitura na porta especificada usando um nome conhecido, &quot;jmxrmi&quot;.

Por padrão, quando você ativa o agente JMX para monitoramento remoto, ele usa a autenticação de senha com base em um arquivo de senha que precisa ser especificado usando a seguinte propriedade do sistema ao iniciar a VM Java:

`com.sun.management.jmxremote.password.file=pwFilePath`

Consulte a documentação [JMX](https://docs.oracle.com/javase/6/docs/technotes/guides/management/agent.html) relevante para obter instruções detalhadas sobre como configurar um arquivo de senha.

Exemplo:

```shell
$ java
  -Dcom.sun.management.jmxremote.password.file=pwFilePath
  -Dcom.sun.management.jmxremote.port=8463
  -jar ./cq-quickstart.jar
```

### Uso dos MBeans fornecidos pelo CRX {#using-the-mbeans-provided-by-crx}

Depois de conectar-se ao processo de início rápido, o JConsole fornece uma variedade de ferramentas gerais de monitoramento para a JVM na qual o CRX está sendo executado.

![screen_shot_2012-03-26at115056am](assets/screen_shot_2012-03-26at115056am.png)

Para acessar as opções internas de monitoramento e configuração do CRX, vá para a guia MBeans e, na árvore de conteúdo hierárquico à esquerda, selecione a seção Atributos ou Operações na qual você está interessado. Por exemplo, a seção com.adobe.granite/Repository/Operations.

Nessa seção, selecione o atributo ou a operação desejada no painel esquerdo.

![screen_shot_2012-03-26at115728am](assets/screen_shot_2012-03-26at115728am.png)

