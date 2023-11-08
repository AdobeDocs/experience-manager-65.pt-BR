---
title: Configurar a sincronização da Live Copy
seo-title: Configuring Live Copy Synchronization
description: Saiba como configurar a sincronização da Live Copy.
seo-description: Learn about configuring Live Copy Synchronization.
uuid: a5db0bee-a761-4cff-81dc-31b374525f47
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 6bcf0fcc-481a-4283-b30d-80b517701280
docset: aem65
feature: Multi Site Manager
exl-id: ac24b8b4-b3ed-47fa-9a73-03f0c9e68ac8
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '2694'
ht-degree: 36%

---

# Configurar a sincronização da Live Copy{#configuring-live-copy-synchronization}

Execute as seguintes tarefas para controlar como e quando as live copies são sincronizadas com seu conteúdo de origem.

* Decida se as configurações de implantação existentes atendem aos seus requisitos ou se é necessário criar um ou mais.
* Especifique as configurações de implantação a serem usadas para suas live copies.

## Configurações de implantação instaladas e personalizadas {#installed-and-custom-rollout-configurations}

Esta seção fornece informações sobre as configurações de implantação instaladas e as ações de sincronização que elas usam, e como criar configurações personalizadas, se necessário.

>[!CAUTION]
>
>Atualizar ou alterar uma configuração de implantação pronta para uso (instalada) é **não** recomendado. Se houver um requisito para uma ação ativa personalizada, ela deverá ser adicionada em uma configuração de implantação personalizada.

### Acionadores de implantação {#rollout-triggers}

Cada configuração de implantação usa um acionador de implantação que ocasiona a implantação. As configurações de implantação podem usar um dos seguintes acionadores:

* **Na implantação**: A variável **Implantação** for usado na página de blueprint ou na guia **Sincronizar** é usado na página da live copy.

* **Em modificação**: a página de origem é modificada.

* **Em ativação**: a página de origem é ativada.

* **Em desativação**: a página de origem é desativada.

>[!NOTE]
>
>O uso do acionador Ao modificar pode afetar o desempenho. Consulte [Práticas recomendadas do MSM](/help/sites-administering/msm-best-practices.md#onmodify) para obter mais informações.

### Configurações de implantação instaladas {#installed-rollout-configurations}

A tabela a seguir lista as configurações de implantação instaladas com AEM. A tabela inclui as ações de acionador e de sincronização de cada configuração de implementação. Se as ações de configuração de implantação instaladas não atenderem aos seus requisitos, você poderá [criar uma configuração de implantação](#creating-a-rollout-configuration).

<table>
 <tbody>
  <tr>
   <th>Nome</th>
   <th>Descrição</th>
   <th>Acionar</th>
   <th>Ações de sincronização<br /> <br /> consulte também <a href="#installed-synchronization-actions">Ações de Sincronização Instaladas</a></th>
  </tr>
  <tr>
   <td>Configuração de implantação padrão</td>
   <td>A configuração de implementação padrão que permite que o processo de implementação comece com estímulos de implementação e executa as ações: criar, atualizar, excluir conteúdo e ordenar os nós filhos.</td>
   <td>Na implantação</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> productUpdate<br /> orderChildren</td>
  </tr>
  <tr>
   <td>Acionar com a ativação do blueprint</td>
   <td>Publica a live copy quando a origem é publicada.</td>
   <td>No modo de ativação</td>
   <td>targetActivate</td>
  </tr>
  <tr>
   <td>Desligar com a desativação do blueprint</td>
   <td>Desativa a live copy quando a origem é desativada.</td>
   <td>Ao desativar</td>
   <td>targetDeactivate<br /> </td>
  </tr>
  <tr>
   <td>Forçar modificação</td>
   <td><p>Envia o conteúdo para a live copy quando a origem é modificada.</p> <p>Use essa configuração de implantação com moderação, pois ela usa o acionador Ao modificar.</p> </td>
   <td>Em modificação</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> </td>
  </tr>
  <tr>
   <td>Forçar modificação (superficial)</td>
   <td><p>Envia o conteúdo para a live copy quando a página do blueprint é modificada, sem atualizar referências (por exemplo, para cópias superficiais).</p> <p>Use essa configuração de implantação com moderação, pois ela usa o acionador Ao modificar.</p> </td>
   <td>Em modificação</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> orderChildren</td>
  </tr>
  <tr>
   <td>Promover lançamento</td>
   <td>Configuração de implantação padrão para a promoção de páginas de lançamento.</td>
   <td>Na implantação</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> markLiveRelationship</td>
  </tr>
  <tr>
   <td>Configuração de implantação do conteúdo da página de catálogo</td>
   <td>Aplica modelos de página para um blueprint do catálogo.</td>
   <td>Na implantação</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> productCreateUpdate<br /> orderChildren</td>
  </tr>
  <tr>
   <td>Configuração de implantação da atualização da página de catálogo</td>
   <td>Aplica propriedades de direcionamento de um blueprint do catálogo. Deve ser executado após a Configuração de implantação do conteúdo da página de catálogo.</td>
   <td>Na implantação</td>
   <td>catalogRolloutHooks</td>
  </tr>
  <tr>
   <td>Configuração de implantação da DPS Publications</td>
   <td>Configuração de implantação da publicação do DPS que permite iniciar o processo de implantação com o acionador de implantação e excluir as propriedades de ligação do FolioProducer na implantação inicial</td>
   <td>Na implantação</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> dpsMetadataFilter</td>
  </tr>
  <tr>
   <td>Configuração de implantação do catálogo herdado (5.6.0)</td>
   <td>Obsoleto.  Use a API Catalog Generator em vez do MSM para implementações de catálogos.</td>
   <td>Na implantação</td>
   <td>editProperties</td>
  </tr>
 </tbody>
</table>

### Ações de Sincronização Instaladas {#installed-synchronization-actions}

A tabela a seguir lista as ações de sincronização instaladas com o AEM. Se as ações instaladas não atenderem aos seus requisitos, você poderá [Criar uma Nova Ação de Sincronização](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action).

<table>
 <tbody>
  <tr>
   <th>Nome da ação</th>
   <th>Descrição</th>
   <th>Propriedades<br /> </th>
  </tr>
  <tr>
   <td>contentCopy</td>
   <td>Quando os nós da origem não existem na live copy, o copia os nós para a live copy. <a href="#excluding-properties-and-node-types-from-synchronization">Configure o serviço de Ação de cópia de conteúdo MSM CQ</a> para especificar os tipos de nó, itens de parágrafo e propriedades de página a serem excluídos. <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentDelete</td>
   <td><p>Exclui nós da live copy que não existem na origem. <a href="#excluding-properties-and-node-types-from-synchronization">Configure o serviço de Ação de exclusão de conteúdo MSM CQ</a> para especificar os tipos de nó, itens de parágrafo e propriedades de página a serem excluídos. </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentUpdate</td>
   <td>Atualiza o conteúdo da live copy com as alterações da origem. <a href="#excluding-properties-and-node-types-from-synchronization">Configure o serviço de Ação de atualização de conteúdo MSM CQ</a> para especificar os tipos de nó, itens de parágrafo e propriedades de página a serem excluídos. <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>editProperties</td>
   <td><p>Edita propriedades da live copy. A propriedade editMap determina quais propriedades são editadas e seus valores. O valor da propriedade editMap deve usar o seguinte formato:</p> <p><code>[property_name_1]#[current_value]#</code>[new_value],<br /> <code>[property_name_2]#[current_value]#</code>[new_value],<br /> ... ,<br /> <code>[property_name_n]#[current_value]#</code>[novo_valor]</p> <p>A variável <code>current_value</code> e <code>new_value</code> itens são expressões regulares. <br /> </p> <p>Por exemplo, considere o seguinte valor para editMap:</p> <p><code>sling:resourceType#/</code>(contentpage|homepage)#/<br /> mobilecontentpage,<br /> cq:template#/contentpage#/mobilecontentpage</p> <p>Esse valor edita as propriedades dos nós de live copy da seguinte maneira:</p>
    <ul>
     <li>A variável <code>sling:resourceType</code> propriedades que estão definidas como <code>contentpage</code> ou para <code>homepage</code> estão definidos como <code>mobilecontentpage.</code></li>
     <li>As propriedades <code>cq:template</code> definidas como <code>contentpage</code> são definidas como <code>mobilecontentpage.</code></li>
    </ul> </td>
   <td><p> </p> <p>editMap: (String) identifica a propriedade, o valor atual e o novo valor. Consulte a Descrição para obter informações.<br /> </p> </td>
  </tr>
  <tr>
   <td>notificar</td>
   <td>Envia um evento de página informando que a página foi implantada. Para ser notificado, é necessário primeiro assinar os eventos de implantação.</td>
   <td> </td>
  </tr>
  <tr>
   <td>orderChildren</td>
   <td>Na live copy, ela ordena os filhos (nós), com base na ordem no blueprint<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>referencesUpdate</td>
   <td><p>Na live copy, essa ação de sincronização atualiza referências como links.<br /> Ela procura caminhos nas páginas de live copy que apontam para um recurso dentro do blueprint. Quando encontrado, ele atualiza o caminho para apontar para o recurso relacionado dentro da live copy (em vez do blueprint). As referências que têm destinos fora do blueprint não são alteradas.</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">Configure o serviço de Ação de atualização de referências MSM CQ</a> para especificar os tipos de nó, itens de parágrafo e propriedades de página a serem excluídos. </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetVersion</td>
   <td><p>Cria uma versão da live copy.</p> <p>Essa ação deve ser a única ação de sincronização incluída em uma configuração de implementação.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetActivate</td>
   <td><p>Ativa a live copy.</p> <p>Essa ação deve ser a única ação de sincronização incluída em uma configuração de implementação.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetDeactivate</td>
   <td><p>Desativa a live copy.</p> <p>Essa ação deve ser a única ação de sincronização incluída em uma configuração de implementação.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>fluxo de trabalho</td>
   <td><p>Inicia o fluxo de trabalho definido pela propriedade de direcionamento (somente para páginas) e toma a live copy como carga.</p> <p>O caminho de destino é o caminho do nó do modelo.</p> </td>
   <td>target: (String) O caminho para o modelo de fluxo de trabalho.<br /> </td>
  </tr>
  <tr>
   <td>obrigatório</td>
   <td><p>Define a permissão de várias ACLs na página da live copy como somente leitura para um grupo de usuários específico. As seguintes ACLs são configuradas:</p>
    <ul>
     <li>ActionSet.ACTION_NAME_REMOVE</li>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>Use esta ação somente para páginas.</p> </td>
   <td>target: (String) A ID do grupo para o qual você está definindo permissões. <br /> </td>
  </tr>
  <tr>
   <td>mandatoryContent</td>
   <td><p>Define a permissão de várias ACLs na página da live copy como somente leitura para um grupo de usuários específico. As seguintes ACLs são configuradas:</p>
    <ul>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>Use esta ação somente para páginas.</p> </td>
   <td>target: (String) A ID do grupo para o qual você está definindo permissões. </td>
  </tr>
  <tr>
   <td>mandatoryStructure</td>
   <td>Define a permissão da ACL ActionSet.ACTION_NAME_REMOVE na página da live copy como somente leitura para um grupo de usuários específico. Use esta ação somente para páginas.</td>
   <td>target: (String) A ID do grupo para o qual você está definindo permissões. </td>
  </tr>
  <tr>
   <td>VersionCopyAction</td>
   <td>Se a página de blueprint/origem tiver sido publicada pelo menos uma vez, o cria uma página de live copy usando a versão publicada. Observação: essa ação só está disponível para criar uma página de live copy com base em uma página de origem publicada, não para atualizar uma página de live copy existente. </td>
   <td> </td>
  </tr>
  <tr>
   <td>AçãoDeMovimentaçãoDePágina</td>
   <td><p>A PageMoveAction se aplica quando uma página foi movida no blueprint.</p> <p>A ação copia, em vez de mover, a página da Live Copy (relacionada) do local anterior à movimentação para o local posterior.</p> <p>PageMoveAction não altera a página da Live Copy no local antes de mover. Portanto, para configurações de implantação consecutivas, ela tem o status de um LiveRelationship sem blueprint.</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">Configure o serviço de Ação de movimentação de página MSM CQ</a> para especificar os tipos de nó, itens de parágrafo e propriedades de página a serem excluídos. </p> <p>Essa ação deve ser a única ação de sincronização incluída em uma configuração de implementação.</p> </td>
   <td><p>prop_referenceUpdate: (booleano) defina como verdadeiro para atualizar referências. O padrão é verdadeiro.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>productCreateUpdate</td>
   <td>Cria ou atualiza recursos de Produto em um catálogo. Esta ação deve ser usada em uma das seguintes situações:
    <ul>
     <li>Geração ou implantação de um catálogo (ou seção de catálogo)</li>
     <li>Um usuário restaura a herança da sincronização de um componente de produto.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>markLiveRelationship</td>
   <td>Indica que existe um relacionamento dinâmico para conteúdo criado na inicialização.</td>
   <td> </td>
  </tr>
  <tr>
   <td>catalogRolloutHooks</td>
   <td>Executa ganchos de implantação específicos de geração de catálogo. Chama os métodos executePageRolloutHooks e executeProductRolloutHooks do CatalogGenerator.<br /> Consulte com.adobe.cq.commerce.pim.api.CatalogGenerator nos Javadocs AEM.</td>
   <td> </td>
  </tr>
  <tr>
   <td>productUpdate</td>
   <td>Atualiza páginas de produto em uma live copy de um catálogo de produtos</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Criação de uma configuração de implantação {#creating-a-rollout-configuration}

Você pode [criar uma configuração de implantação](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) quando as configurações de implantação instaladas não atenderem aos requisitos do aplicativo:

* [Criar a configuração de implantação](/help/sites-developing/extending-msm.md#create-the-rollout-configuration).
* [Adicionar ações de sincronização à configuração de implantação](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration).

A nova configuração de implantação está então disponível ao definir configurações de implantação em uma página de blueprint ou Live Copy.

### Excluir propriedades e tipos de nó da sincronização {#excluding-properties-and-node-types-from-synchronization}

Você pode configurar vários serviços OSGi que suportam ações de sincronização correspondentes para que eles não afetem tipos de nó e propriedades específicos. Por exemplo, muitas propriedades e nós secundários relacionados ao funcionamento interno do AEM não devem ser incluídos em uma live copy. Somente o conteúdo relevante para o usuário da página deve ser copiado.

Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

A tabela a seguir lista as ações de sincronização para as quais você pode especificar os nós a serem excluídos. A tabela fornece os nomes dos serviços a serem configurados usando o console da Web e o PID para configurar usando um nó de repositório.

| Ação de sincronização | Nome do serviço no Console da web | PID do serviço |
|---|---|---|
| contentCopy | Ação de cópia de conteúdo MSM CQ | com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory |
| contentDelete | Ação de exclusão de conteúdo MSM CQ | com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory |
| contentUpdate | Ação de atualização de conteúdo do MSM CQ | com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory |
| AçãoDeMovimentaçãoDePágina | Ação de movimentação de página MSM CQ | com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory |
| referencesUpdate | Ação de atualização de referências MSM CQ | com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory |

A tabela a seguir descreve as propriedades que você pode configurar:

<table>
 <tbody>
  <tr>
   <th>Propriedade do console da Web / propriedade OSGi</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td><p>Nodetypes Excluídos</p> <p>cq.wcm.msm.action.excludednodetypes</p> </td>
   <td>Uma expressão regular que corresponde aos nomes dos tipos de nó que serão excluídos da ação de sincronização.</td>
  </tr>
  <tr>
   <td><p>Itens de parágrafo excluídos</p> <p>cq.wcm.msm.action.excludedparagraphitems</p> </td>
   <td>Uma expressão regular que corresponde aos itens de parágrafo que serão excluídos da ação de sincronização.</td>
  </tr>
  <tr>
   <td><p>Propriedades da página excluída</p> <p>cq.wcm.msm.action.excludedprops</p> </td>
   <td>Uma expressão regular que corresponde às propriedades de página que serão excluídas da ação de sincronização.</td>
  </tr>
  <tr>
   <td><p>Tipos de nó Mixin ignorados</p> <p>cq.wcm.msm.action.ignoredMixin</p> </td>
   <td>Disponível somente para Ação de atualização de conteúdo MSM CQ. Uma expressão regular que corresponde aos nomes dos tipos de nó mixin que serão excluídos da ação de sincronização.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Na interface clássica, o ícone de bloqueio exibido na caixa de diálogo Propriedades da página para páginas do Live Copy não reflete a configuração da propriedade Propriedades da página excluídas. O ícone de bloqueio aparece mesmo para propriedades que são excluídas da ação de sincronização.

>[!NOTE]
>
>Na interface otimizada para toque, consulte também [Configuração de bloqueios do MSM nas propriedades da página (interface otimizada para toque)](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-pagep-roperties-touch-optimized-ui).

#### Ação de atualização de conteúdo do MSM CQ - Exclusões {#cq-msm-content-update-action-exclusions}

Várias propriedades e tipos de nó são excluídos por padrão. Eles são definidos na configuração OSGi da **Ação de atualização de conteúdo do MSM CQ**, em **Propriedades da página excluída**.

Por padrão, as propriedades que correspondem às seguintes expressões regulares são excluídas (ou seja, não são atualizadas) na implantação:

![Ação de atualização de conteúdo do MSM CQ](assets/chlimage_1.png)

É possível alterar as expressões definindo a lista de exclusões conforme necessário.

Por exemplo, se você quiser que o **Título** da página seja incluído nas alterações consideradas para implementação, remova `jcr:title` das exclusões. Por exemplo, com o regex:

`jcr:(?!(title)$).*`

### Configurar sincronização para atualizar referências {#configuring-synchronization-for-updating-references}

Você pode configurar vários serviços OSGi que oferecem suporte às ações de sincronização correspondentes relacionadas à atualização de referências.

Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

A tabela a seguir lista as ações de sincronização para as quais você pode especificar a atualização de referência. A tabela fornece os nomes dos serviços a serem configurados usando o console da Web e o PID para configurar usando um nó de repositório.

<table>
 <tbody>
  <tr>
   <th>Propriedade do console da Web / propriedade OSGi</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td><p>Atualizar referência entre LiveCopies aninhadas</p> <p>cq.wcm.msm.impl.action.referencesupdate.prop_updateNested</p> </td>
   <td>Disponível somente para a Ação de atualização de referências MSM CQ. Selecione esta opção (Console da Web) ou defina esta propriedade boolean como true (configuração do repositório) para substituir referências que se destinam a qualquer recurso que esteja dentro da ramificação da Live Copy mais elevada.</td>
  </tr>
  <tr>
   <td><p>Atualizar páginas de referência</p> <p>cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate</p> </td>
   <td>Disponível somente para a Ação de movimentação de página MSM CQ. Selecione esta opção (Console da Web) ou defina esta propriedade booleana como <code>true</code> (configuração do repositório) para atualizar todas as referências para usar a página original para fazer referência à página Live Copy.</td>
  </tr>
 </tbody>
</table>

## Especificar as configurações de implementação a serem usadas {#specifying-the-rollout-configurations-to-use}

O MSM permite especificar conjuntos de configurações de implantação usados com frequência e, quando necessário, você pode substituí-los por live copies específicas. O MSM fornece vários locais para especificar as configurações de implementação a serem usadas. O local determina se a configuração se aplica a uma live copy específica.

A seguinte lista de locais onde você pode especificar as configurações de implantação a serem usadas descreve como o MSM determina quais configurações de implantação usar para uma live copy:

* **[Propriedades da página de Live Copy](/help/sites-administering/msm-sync.md#setting-the-rollout-configurations-for-a-live-copy-page):** Quando uma página de live copy é configurada para usar uma ou mais configurações de implantação, o MSM usa essas configurações.
* **[Propriedades da página de blueprint](/help/sites-administering/msm-sync.md#setting-the-rollout-configuration-for-a-blueprint-page):** Quando uma live copy é baseada em um blueprint e a página de live copy não está definida com uma configuração de implantação, a configuração associada à página de origem do blueprint é usada.
* **Propriedades da página principal da Live Copy:** Quando nenhuma página de live copy ou página de origem do blueprint é definida com uma configuração de implantação, a configuração que se aplica à página principal da página de live copy é usada.
* **[Padrão do sistema](/help/sites-administering/msm-sync.md#setting-the-system-default-rollout-configuration):** Quando a configuração de implantação da página principal da live copy não pode ser determinada, a configuração padrão do sistema é usada.

Por exemplo, um blueprint usa o site de referência We.Retail como conteúdo de origem. Um site é criado a partir do blueprint. Cada item na lista a seguir descreve um cenário diferente com relação ao uso de configurações de implantação:

* Nenhuma das páginas do blueprint ou das páginas de live copy está definida para usar uma configuração de implantação. O MSM usa a configuração de implantação padrão do sistema para todas as páginas de live copy.
* A página raiz do site de referência We.Retail está configurada com várias configurações de implantação. O MSM usa essas configurações de implantação para todas as páginas de live copy.
* A página raiz do site de referência We.Retail está configurada com várias configurações de implantação, e a página raiz do site de live copy está configurada com um conjunto diferente de configurações de implantação. O MSM usa as configurações de implantação definidas na página raiz do site de live copy.

### Definir as configurações de implementação de uma página de Live Copy {#setting-the-rollout-configurations-for-a-live-copy-page}

Defina uma página de live copy com as configurações de implantação a serem usadas quando a página de origem for implantada. As páginas secundárias herdam a configuração por padrão. Ao definir a configuração de implantação a ser usada, você substituirá a configuração que a página de live copy herdará da página principal.

Você também pode definir as configurações de implantação para uma página de live copy ao [criar a live copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page).

1. Use o **Sites** para selecionar a página live copy.
1. Selecione **Propriedades** na barra de ferramentas.
1. Abra a guia **Live Copy**.

   A seção **Configuração** mostra as configurações de implementação que a página herda.

   ![Configuração](assets/chlimage_1-1.png)

1. Se necessário, ajuste a variável **Herança da Live Copy** sinalizador. Se essa opção for marcada, a configuração da live copy terá efeito em todas as tarefas derivadas.

1. Limpe a propriedade **Herdar configurações de implantação da página principal** e selecione uma ou mais configurações de implantação na lista.

   As configurações de implantação selecionadas aparecem abaixo da lista suspensa.

   ![Configurações de implantação selecionadas](assets/chlimage_1-2.png)

1. Clique ou toque em **Salvar**.

### Definir a configuração de implantação de uma página do blueprint {#setting-the-rollout-configuration-for-a-blueprint-page}

Configure uma página de blueprint com as configurações de implantação a serem usadas quando a página de blueprint for implantada.

As páginas secundárias da página do blueprint herdam a configuração. Ao definir a configuração de implantação a ser usada, você pode estar substituindo a configuração que a página herdará da página principal.

1. Use o console **Sites** para selecionar a página raiz do blueprint.
1. Selecione **Propriedades** na barra de ferramentas.
1. Abra a guia **Blueprint.**
1. Selecione uma ou mais **configurações de implantação** usando o seletor suspenso.
1. Mantenha suas atualizações com **Salvar**.

### Definir a configuração de implementação padrão do sistema {#setting-the-system-default-rollout-configuration}

Especifique uma configuração de implantação a ser usada como padrão do sistema. Para especificar o padrão, configure o serviço OSGi:

* **Gerente de relacionamento dinâmico do WCM CQ do dia**
o PID do serviço é `com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

Configure o serviço usando a variável [Console da Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ou um [nó do repositório](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

* No console da web, o nome da propriedade a ser configurada é Configuração de implantação padrão.
* Ao usar um nó de repositório, o nome da propriedade a ser configurada é `liverelationshipmgr.relationsconfig.default`.

Defina esse valor de propriedade como o caminho da configuração de implementação a ser usada como padrão do sistema. O valor padrão é `/libs/msm/wcm/rolloutconfigs/default`, que é a **Configuração de implantação padrão**.
