---
title: Configurar a sincronização da Live Copy
seo-title: Configurar a sincronização da Live Copy
description: Saiba mais sobre como configurar a sincronização da Live Copy.
seo-description: Saiba mais sobre como configurar a sincronização da Live Copy.
uuid: a5db0bee-a761-4cff-81dc-31b374525f47
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 6bcf0fcc-481a-4283-b30d-80b517701280
docset: aem65
translation-type: tm+mt
source-git-commit: 37c9cb6db35cb941a117a03aadf7a9815809c85e
workflow-type: tm+mt
source-wordcount: '2684'
ht-degree: 78%

---


# Configurar a sincronização da Live Copy{#configuring-live-copy-synchronization}

Execute as tarefas a seguir para controlar como e quando as cópias dinâmicas são sincronizadas com o conteúdo de origem.

* Decida se as configurações de implementação existentes atendem aos seus requisitos ou se você precisa criar uma ou mais.
* Especifique as configurações de implementação a serem usadas para as cópias dinâmicas.

## Configurações instaladas e personalizadas de implementação {#installed-and-custom-rollout-configurations}

Esta seção fornece informações sobre as configurações de implementação instaladas e as ações de sincronização que elas usam, além de como criar configurações personalizadas, se necessário.

### Acionadores de implementação {#rollout-triggers}

Cada configuração de implementação usa um acionador de implementação que faz com que a implementação ocorra. As configurações de implementação podem usar um dos seguintes acionadores:

* **Na distribuição**: o comando **Implementação** é usado na página de blueprint, ou o comando **Sincronizar** é usado na página de Live Copy.

* **Em modificação**: a página de origem é modificada.

* **Em ativação**: a página de origem é ativada.

* **Em desativação**: a página de origem é desativada.

>[!NOTE]
>
>O uso do acionador Em modificação pode afetar o desempenho. Consulte [Práticas recomendadas do MSM](/help/sites-administering/msm-best-practices.md#onmodify) para obter mais informações.

### Configurações de implementação instaladas {#installed-rollout-configurations}

A tabela a seguir lista as configurações de implementação instaladas com o AEM. A tabela inclui as ações de acionador e de sincronização de cada configuração de implementação. Se as ações de configuração de implementação instaladas não atenderem aos requisitos, você poderá [criar uma nova configuração de implementação](#creating-a-rollout-configuration).

<table>
 <tbody>
  <tr>
   <th>Nome</th>
   <th>Descrição</th>
   <th>Acionar</th>
   <th>Ações de sincronização<br /><br />  consulte também <a href="#installed-synchronization-actions">Ações de sincronização instaladas</a></th>
  </tr>
  <tr>
   <td>Configuração de implantação padrão</td>
   <td>A configuração de implementação padrão que permite que o processo de implementação comece com estímulos de implementação e executa as ações: criar, atualizar, excluir conteúdo e ordenar os nós filhos.</td>
   <td>Na implantação</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> productUpdate<br /> orderChildren</td>
  </tr>
  <tr>
   <td>Acionar com a ativação do blueprint</td>
   <td>Publica a Live Copy quando a origem é publicada.</td>
   <td>No modo de ativação</td>
   <td>targetActivate</td>
  </tr>
  <tr>
   <td>Desligar com a desativação do blueprint</td>
   <td>Desativa a Live Copy quando a origem é desativada.</td>
   <td>Ao desativar</td>
   <td>targetDeactivate<br /> </td>
  </tr>
  <tr>
   <td>Forçar modificação</td>
   <td><p>Força o conteúdo à Live Copy quando a origem é modificada.</p> <p>Use esta configuração de implementação com moderação, pois usa o acionador Em modificação.</p> </td>
   <td>Em modificação</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> </td>
  </tr>
  <tr>
   <td>Forçar modificação (superficial)</td>
   <td><p>Força o conteúdo à Live Copy quando a página do blueprint é modificada, sem atualizar referências (por exemplo, para cópias superficiais).</p> <p>Use esta configuração de implementação com moderação, pois usa o acionador Em modificação.</p> </td>
   <td>Em modificação</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> orderChildren</td>
  </tr>
  <tr>
   <td>Promover lançamento</td>
   <td>Configuração de implementação padrão para a promoção de páginas de inicialização.</td>
   <td>Na implantação</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> markLiveRelationship</td>
  </tr>
  <tr>
   <td>Configuração de implementação do conteúdo da página de catálogo</td>
   <td>Aplica modelos de página para um blueprint do catálogo.</td>
   <td>Na implantação</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> productCreateUpdate<br /> orderChildren</td>
  </tr>
  <tr>
   <td>Configuração de implantação da atualização da página de catálogo</td>
   <td>Aplica propriedades de destino a partir de um blueprint do catálogo. Deve ser executado após a Configuração de implementação do conteúdo da página de catálogo.</td>
   <td>Na implantação</td>
   <td>catalogRolloutHooks</td>
  </tr>
  <tr>
   <td>Configuração de implantação da DPS Publications</td>
   <td>A Configuração de implementação de publicação DPS permite iniciar o processo de implementação no acionador de implementação, ao mesmo tempo em que exclui as propriedades de associação FolioProducer na implementação inicial</td>
   <td>Na implantação</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> dpsMetadataFilter</td>
  </tr>
  <tr>
   <td>Configuração de implantação do catálogo herdado (5.6.0).</td>
   <td>Obsoleto.  Use a API Catalog Generator em vez do MSM para implementações de catálogos.</td>
   <td>Na implantação</td>
   <td>editProperties</td>
  </tr>
 </tbody>
</table>

### Ações de sincronização instaladas {#installed-synchronization-actions}

A tabela a seguir lista as ações de sincronização instaladas com o AEM. If the installed actions do not meet your requirements, you can [Create a New Synchronization Action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action).

<table>
 <tbody>
  <tr>
   <th>Nome da ação</th>
   <th>Descrição</th>
   <th>Propriedades<br /> </th>
  </tr>
  <tr>
   <td>contentCopy</td>
   <td>Quando os nós da origem não existem na Live Copy, copia os nós para a Live Copy. <a href="#excluding-properties-and-node-types-from-synchronization">Configure o serviço</a> CQ MSM Content Copy Action para especificar os tipos de nó, os itens de parágrafo e as propriedades da página a serem excluídos. <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentDelete</td>
   <td><p>Exclui nós da live copy que não existem na fonte. <a href="#excluding-properties-and-node-types-from-synchronization">Configure o serviço</a> CQ MSM Content Delete Action para especificar os tipos de nó, os itens de parágrafo e as propriedades da página a serem excluídos. </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentUpdate</td>
   <td>Atualiza o conteúdo da Live Copy com as alterações da origem. <a href="#excluding-properties-and-node-types-from-synchronization">Configure o serviço</a> CQ MSM Content Update Action para especificar os tipos de nó, os itens de parágrafo e as propriedades da página a serem excluídos. <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>editProperties</td>
   <td><p>Edita as propriedades da Live Copy. A propriedade editMap determina quais propriedades são editadas e seu valor. O valor da propriedade editMap deve usar o seguinte formato:</p> <p><code>[property_name_1]#[current_value]#</code>[new_value],<br /> <code>[property_name_2]#[current_value]#</code>[new_value],<br /> ... ,<br /> <code>[property_name_n]#[current_value]#</code>[new_value]</p> <p>The <code>current_value</code> and <code>new_value</code> items are regular expressions. <br /> </p> <p>Por exemplo, considere o seguinte valor para a editMap:</p> <p><code>sling:resourceType#/</code>(contentpage|homepage)#/<br /> mobilecontentpage,<br /> cq:template#/contentpage#/mobilecontentpage</p> <p>Este valor edita as propriedades dos nós de Live Copy da seguinte maneira:</p>
    <ul>
     <li>The <code>sling:resourceType</code> properties that are either set to <code>contentpage</code> or to <code>homepage</code> are set to <code>mobilecontentpage.</code></li>
     <li>As <code>cq:template</code> propriedades definidas como <code>contentpage</code> estão definidas como <code>mobilecontentpage.</code></li>
    </ul> </td>
   <td><p> </p> <p>editMap: (cadeia de caracteres) identifica a propriedade, o valor atual e o novo valor. Consulte a Descrição para obter informações.<br /> </p> </td>
  </tr>
  <tr>
   <td>notify</td>
   <td>Envia um evento de página que a página foi distribuída. Para ser notificado, é necessário primeiro assinar eventos de distribuição.</td>
   <td> </td>
  </tr>
  <tr>
   <td>orderChildren</td>
   <td>Na Live Copy, ordena os filhos (nós), com base na ordem no blueprint<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>referencesUpdate</td>
   <td><p>Na Live Copy, essa ação de sincronização atualiza as referências como links.<br /> Ela procura caminhos nas páginas de Live Copy que apontam para um recurso dentro do blueprint. Quando encontrado, ela atualiza o caminho para apontar para o recurso relacionado dentro da Live Copy (em vez do blueprint). As referências que têm destinos fora do blueprint não são alteradas.</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">Configure o serviço</a> Ação de Atualização de Referências MSM do CQ para especificar os tipos de nó, os itens de parágrafo e as propriedades da página a serem excluídos. </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetVersion</td>
   <td><p>Cria uma versão da Live Copy.</p> <p>Essa ação deve ser a única ação de sincronização incluída em uma configuração de implementação.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetActivate</td>
   <td><p>Ativa a Live Copy.</p> <p>Essa ação deve ser a única ação de sincronização incluída em uma configuração de implementação.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetDeactivate</td>
   <td><p>Desativa a Live Copy.</p> <p>Essa ação deve ser a única ação de sincronização incluída em uma configuração de implementação.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>fluxo de trabalho</td>
   <td><p>Inicia o fluxo de trabalho definido pela propriedade de destino (somente para páginas) e toma a Live Copy como carga.</p> <p>O caminho de destino é o caminho do nó modelo, por exemplo /etc/workflow/models/request_for_activation/jcr:content/model</p> </td>
   <td>target: (cadeia de caracteres) o caminho para o modelo de fluxo de trabalho.<br /> </td>
  </tr>
  <tr>
   <td>mandatory</td>
   <td><p>Define a permissão de várias ACLs na página de Live Copy como somente leitura para um grupo de usuários específico. As ACLs a seguir estão configuradas:</p>
    <ul>
     <li>ActionSet.ACTION_NAME_REMOVE</li>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>Use esta ação somente para páginas.</p> </td>
   <td>target: (cadeia de caracteres) a ID do grupo para o qual você está definindo permissões. <br /> </td>
  </tr>
  <tr>
   <td>mandatoryContent</td>
   <td><p>Define a permissão de várias ACLs na página de Live Copy como somente leitura para um grupo de usuários específico. As ACLs a seguir estão configuradas:</p>
    <ul>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>Use esta ação somente para páginas.</p> </td>
   <td>target: (cadeia de caracteres) a ID do grupo para o qual você está definindo permissões. </td>
  </tr>
  <tr>
   <td>mandatoryStructure</td>
   <td>Define a permissão da ACL ActionSet.ACTION_NAME_REMOVE na página de Live Copy como somente leitura para um grupo de usuários específico. Use esta ação somente para páginas.</td>
   <td>target: (cadeia de caracteres) a ID do grupo para o qual você está definindo permissões. </td>
  </tr>
  <tr>
   <td>VersionCopyAction</td>
   <td>Se a página de blueprint/origem tiver sido publicada pelo menos uma vez, cria uma página de Live Copy usando a versão publicada. Observação: essa ação só está disponível para criar uma página de Live Copy com base em uma página de origem publicada, não para atualizar uma página de Live Copy existente. </td>
   <td> </td>
  </tr>
  <tr>
   <td>PageMoveAction</td>
   <td><p>A PageMoveAction se aplica quando uma página foi movida no blueprint.</p> <p>A ação copia em vez de mover a página LiveCopy (relacionada) do local antes de mover para o local depois.</p> <p>A PageMoveAction não altera a página LiveCopy no local antes da movimentação. Portanto, para RolloutConfigurations consecutivas ele tem o status de um LiveRelationhip sem Blueprint.</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">Configure o serviço de Ação de movimentação de página MSM CQ</a> para especificar os tipos de nó, itens de parágrafo e propriedades de página a serem excluídos. </p> <p>Essa ação deve ser a única ação de sincronização incluída em uma configuração de implementação.</p> </td>
   <td><p>prop_referenceUpdate: (booleano) defina como verdadeiro para atualizar referências. O padrão é verdadeiro.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>productCreateUpdate</td>
   <td>Cria ou atualiza recursos do Produto em um catálogo. Essa ação deve ser usada em uma das seguintes situações:
    <ul>
     <li>Ao gerar ou implantar um catálogo (ou seção de catálogo)</li>
     <li>Um usuário restaura a herança de sincronização de um componente de produto.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>markLiveRelationship</td>
   <td>Indica se existe uma relação dinâmica para conteúdo criado na inicialização.</td>
   <td> </td>
  </tr>
  <tr>
   <td>catalogRolloutHooks</td>
   <td>Executa ganchos de implementação específicos da geração de catálogo. Chama os métodos executePageRolloutHooks e executeProductRolloutHooks do CatalogGenerator.<br /> Consulte com.adobe.cq.commerce.pim.api.CatalogGenerator in the AEM Javadocs.</td>
   <td> </td>
  </tr>
  <tr>
   <td>productUpdate</td>
   <td>Atualiza páginas do produto em uma Live Copy de um catálogo de produtos</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Criar uma configuração de implementação {#creating-a-rollout-configuration}

Você pode [criar uma configuração de implementação](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) quando as configurações de implementação instaladas não atenderem aos requisitos do aplicativo:

* [Criar a configuração de implementação](/help/sites-developing/extending-msm.md#create-the-rollout-configuration).
* [Adicionar ações de sincronização à configuração de implementação](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration).

A nova configuração de implementação estará disponível para você quando definir configurações de implementação em um blueprint ou página de Live Copy.

### Excluir propriedades e tipos de nó da sincronização {#excluding-properties-and-node-types-from-synchronization}

Você pode configurar vários serviços OSGi que suportam ações de sincronização correspondentes para que eles não afetem tipos de nó e propriedades específicos. Por exemplo, muitas propriedades e subnós relacionados ao funcionamento interno do AEM não devem ser incluídos em uma live copy. Somente o conteúdo relevante para o usuário da página deve ser copiado.

When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

A tabela a seguir lista as ações de sincronização para as quais você pode especificar os nós a serem excluídos. A tabela fornece os nomes dos serviços a serem configurados usando o Console na Web e o PID para configurar o usando um nó de repositório.

| Ação de sincronização | Nome do serviço no Console da Web | PID do serviço |
|---|---|---|
| contentCopy | Ação de CQ MSM Content Copy | com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory |
| contentDelete | Ação de exclusão de conteúdo CQ MSM | com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory |
| contentUpdate | Ação de atualização de conteúdo do CQ MSM | com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory |
| PageMoveAction | Ação de Mover página do CQ MSM | com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory |
| referencesUpdate | Ação de Atualização de Referências MSM CQ | com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory |

A tabela a seguir descreve as propriedades que você pode configurar:

<table>
 <tbody>
  <tr>
   <th>Propriedade do Console Web / propriedade OSGi</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td><p>Tipos de nó excluídos</p> <p>cq.wcm.msm.action.excludednodetypes</p> </td>
   <td>Uma expressão regular que corresponde aos tipos de nó a serem excluídos da ação de sincronização.</td>
  </tr>
  <tr>
   <td><p>Itens de parágrafo excluídos</p> <p>cq.wcm.msm.action.excludedparagraphitems</p> </td>
   <td>Uma expressão regular que corresponde aos itens de parágrafo a serem excluídos da ação de sincronização.</td>
  </tr>
  <tr>
   <td><p>Propriedades da página excluída</p> <p>cq.wcm.msm.action.excludedprops</p> </td>
   <td>Uma expressão regular que corresponde às propriedades da página a serem excluídas da ação de sincronização.</td>
  </tr>
  <tr>
   <td><p>Tipos de nó de combinação ignorados</p> <p>cq.wcm.msm.action.ignoredMixin</p> </td>
   <td>Disponível somente para a Ação de atualização de conteúdo CQ MSM. Uma expressão comum que corresponde aos nomes dos tipos de nó mixin a serem excluídos da ação de sincronização.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Na interface do usuário clássica, o ícone de bloqueio que aparece na caixa de diálogo Propriedades da página de páginas LiveCopy não reflete a configuração da propriedade Propriedades de página excluídas. O ícone de bloqueio é exibido até mesmo para propriedades que são excluídas da ação de sincronização.

>[!NOTE]
>
>Na interface otimizada para toque, veja também [Configurar bloqueios do MSM em Propriedades da página (interface do usuário otimizada para toque)](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-pagep-roperties-touch-optimized-ui).

#### Ação de atualização de conteúdo do MSM CQ - Exclusões {#cq-msm-content-update-action-exclusions}

Várias propriedades e tipos de nó são excluídas por padrão, elas são definidas na configuração OSGi da **Ação de atualização de conteúdo do MSM CQ**, em **Propriedades de página excluídas**.

Por padrão, as propriedades que correspondentes às seguintes expressões comuns são excluídas (ou seja, não é atualizada) na implementação:

![chlimage_1](assets/chlimage_1.png)

É possível alterar as expressões definindo a lista de exclusões conforme necessário.

Por exemplo, se você quiser que o **Título** da página seja incluído nas alterações consideradas para implementação, remova `jcr:title` das exclusões. Por exemplo, com o regex:

`jcr:(?!(title)$).*`

### Configurar sincronização para atualizar referências {#configuring-synchronization-for-updating-references}

Você pode configurar vários serviços OSGi que oferecem suporte às ações de sincronização correspondentes relacionadas à atualização de referências.

When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

A tabela a seguir lista as ações de sincronização para as quais você pode especificar a atualização de referência. A tabela fornece os nomes dos serviços a serem configurados usando o Console na Web e o PID para configurar o usando um nó de repositório.

<table>
 <tbody>
  <tr>
   <th>Propriedade do Console Web / propriedade OSGi</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td><p>Atualizar referência em LiveCopies aninhados</p> <p>cq.wcm.msm.impl.action.referencesupdate.prop_updateNested</p> </td>
   <td>Disponível somente para a Ação de atualização de referências CQ MSM. Selecione essa opção (Console da Web) ou defina essa propriedade booleana como true (configuração do repositório) para substituir referências que públicos alvos qualquer recurso que esteja na ramificação do LiveCopy mais avançado.</td>
  </tr>
  <tr>
   <td><p>Atualizar páginas de referência</p> <p>cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate</p> </td>
   <td>Disponível somente para Ação de Mover Página do CQ MSM. Select this option (Web Console) or set this boolean property to <code>true</code> (repository configuration) to update any references to use the original page to instead reference the LiveCopy page.</td>
  </tr>
 </tbody>
</table>

## Especificar as configurações de implementação a serem usadas {#specifying-the-rollout-configurations-to-use}

O MSM permite que você especifique conjuntos de configurações de implementação usados com frequência e, quando necessário, pode substituí-los por cópias dinâmicas específicas. O MSM fornece vários locais para especificar as configurações de implementação a serem usadas. O local determina se a configuração se aplica a uma Live Copy específica.

A lista de locais a seguir em que você pode especificar as configurações de implementação a serem usadas descreve como o MSM determina quais configurações usar para uma Live Copy:

* **[Propriedades da página de Live Copy](/help/sites-administering/msm-sync.md#setting-the-rollout-configurations-for-a-live-copy-page):**quando uma página de Live Copy é configurada para usar uma ou mais configurações de implementação, o MSM usa essas configurações.
* **[Propriedades da página do blueprint](/help/sites-administering/msm-sync.md#setting-the-rollout-configuration-for-a-blueprint-page):**quando uma Live Copy é baseada em um blueprint, e a página de Live Copy não está configurada com uma configuração de implementação, a configuração associada à página de origem do blueprint é usada.
* **Propriedades da página pai da Live Copy:** Quando nem a página live copy nem a página de origem do blueprint estão configuradas com uma configuração de implementação, a configuração de implementação que se aplica à página pai da página live copy é usada.
* **[Padrão](/help/sites-administering/msm-sync.md#setting-the-system-default-rollout-configuration)do sistema:**Quando a configuração de implantação da página pai da live copy não puder ser determinada, a configuração de implantação padrão do sistema será usada.

Por exemplo, um blueprint usa o site de referência We.Retail como conteúdo de origem. Um site é criado a partir do blueprint. Cada item da lista a seguir descreve um cenário diferente sobre o uso de configurações de implementação:

* Nenhuma das páginas do blueprint ou das páginas de Live Copy é configurada para usar uma configuração de implementação. O MSM usa a configuração de implementação padrão do sistema para todas as páginas de Live Copy.
* A página raiz do site de referência We.Retail é configurada com várias configurações de implementação. O MSM usa essas configurações de implementação para todas as páginas de Live Copy.
* A página raiz do Site de referência We.Retail é configurada com várias configurações de implantação e a página raiz do site live copy é configurada com um conjunto diferente de configurações de implantação. O MSM usa as configurações de implementação configuradas na página raiz do site de Live Copy.

### Definir as configurações de implementação de uma página de Live Copy {#setting-the-rollout-configurations-for-a-live-copy-page}

Configure uma página de Live Copy com as configurações de implementação a serem usadas quando a página de origem for distribuída. As páginas secundárias herdam a configuração por padrão. Ao definir a configuração de implementação a ser usada, você estará substituindo a configuração que a página de Live Copy herda de seu pai.

Também é possível definir as configurações de implementação para uma página de Live Copy ao [criar a Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page).

1. Use o console **Sites** para selecionar a página de Live Copy.
1. Selecione **Propriedades** na barra de ferramentas.
1. Open the **Live Copy** tab.

   A seção **Configuração** mostra as configurações de implementação que a página herda.

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. Se necessário, ajuste o sinalizador de **Herança da Live Copy**. Se essa opção for marcada, a configuração da cópias dinâmica terá efeito em todas as páginas secundárias.

1. Desmarque a propriedade **Herdar configuração de implementação do Pai** e selecione uma ou mais configurações de implementação na lista.

   As configurações de implementação selecionadas aparecem abaixo da lista suspensa.

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. Clique ou toque em **Salvar**.

### Definir a configuração de implementação de uma página do blueprint {#setting-the-rollout-configuration-for-a-blueprint-page}

Configure uma página do blueprint com as configurações de implementação a serem usadas quando a página do blueprint for distribuída.

Observe que as páginas secundárias da página do blueprint herdam a configuração. Ao definir a configuração de implementação a ser usada, você pode estar substituindo a configuração que a página herda de seu pai.

1. Use the **Sites** console to select the root page of the blueprint.
1. Selecione **Propriedades** na barra de ferramentas.
1. Abra a guia **Blueprint.**
1. Selecione uma ou mais **configurações de implementação** usando o seletor suspenso.
1. Mantenha suas atualizações com **Salvar**.

### Definir a configuração de implementação padrão do sistema {#setting-the-system-default-rollout-configuration}

Especifique uma configuração de implementação a ser usada como padrão do sistema. Para especificar o padrão, configure o serviço OSGi:

* O PID de serviço do **Gerente de relacionamento dinâmico do WCM CQ do dia**  é 
`com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

Configure the service using either the [Web Console](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) or a [repository node](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

* No console da Web, o nome da propriedade a ser configurada é Configuração de implementação padrão.
* Using a repository node, the name of the property to configure is `liverelationshipmgr.relationsconfig.default`.

Defina esse valor de propriedade como o caminho da configuração de implementação a ser usada como padrão do sistema. The default value is `/etc/msm/rolloutconfigs/default`, which is the **Standard Rollout Config**.
