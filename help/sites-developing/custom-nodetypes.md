---
title: Tipos de nó personalizados
seo-title: Tipos de nó personalizados
description: O AEM é baseado no Sling e usa um repositório JCR com tipos de nó oferecidos por ambos, mas o AEM também fornece diversos tipos de nó personalizados
seo-description: O AEM é baseado no Sling e usa um repositório JCR com tipos de nó oferecidos por ambos, mas o AEM também fornece diversos tipos de nó personalizados
uuid: f2022504-e433-4b42-9cc1-eef41086483a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: aae186eb-e059-4a9d-b02d-86a86c86589d
translation-type: tm+mt
source-git-commit: 07eb53f19cf7c7c2799c95ba9df54f4673d72fdc
workflow-type: tm+mt
source-wordcount: '1918'
ht-degree: 9%

---


# Tipos de nó personalizados{#custom-node-types}

Como o AEM é baseado no Sling e usa um repositório JCR, os tipos de nó oferecidos por ambos estão disponíveis para uso:

* [Tipos de Nó JCR](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Tipos de Nó Sling](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

Além disso. O AEM fornece diversos tipos de nó personalizados.

## Auditoria {#audit}

### cq:AuditEvent {#cq-auditevent}

**Descrição**

Define o tipo de nó de um nó de evento de auditoria.

* `@prop cq:time`
* `@prop cq:userid`
* `@prop cq:path`
* `@prop cq:type`
* `@prop cq:category`
* `@prop cq:properties`

**Definição**

* `[cq:AuditEvent]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
* `- cq:time (date)`
* `- cq:userid (string)`
* `- cq:path (string)`
* `- cq:type (string)`
* `- cq:category (string)`
* `- cq:properties (binary)`

## Comentário {#comment}

### cq:Comentário {#cq-comment}

**Descrição**

Define o tipo de nó de um nó de comentário.

* `@prop userIdentifier`

**Definição**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq:CommentAttachment {#cq-commentattachment}

**Descrição**

Define o tipo de nó de um `commentattachment` nó

**Definição**

* `[cq:CommentAttachment] > nt:file`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq:CommentContent {#cq-commentcontent}

**Descrição**

Define o tipo de nó de um nó de conteúdo de comentário

**Definição**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq:GeoLocation {#cq-geolocation}

**Descrição**

Uma mistura que define uma localização geográfica em graus decimais (DD)

* `@prop latitude` - latitude codificada como duplo, utilizando graus decimais
* `@prop longitude` - longitude codificada como duplo, utilizando graus decimais

**Definição**

* `[cq:GeoLocation] mixin`
* `- latitude (double)`
* `- longitude (double)`

### cq:Trackback {#cq-trackback}

**Descrição**

Define o tipo de nó de um nó de trackback.

**Definição**

* `[cq:Trackback] > mix:title, mix:created, mix:language, nt:unstructured`

## Núcleo {#core}

### cq:Page {#cq-page}

**Descrição**

Define a página padrão do CQ.

* `@node jcr:content` - Conteúdo principal da página.

**Definição**

* `[cq:Page] > nt:hierarchyNode orderable`
   * `+ jcr:content (nt:base) = nt:unstructured copy primary`
   * `+ * (nt:base) = nt:base version`

### cq:PseudoPage {#cq-pseudopage}

**Descrição**

Define um tipo de combinação que marca os nós como pseudo-páginas. Isso significa que eles podem ser adaptados para o suporte à edição de página e WCM.

**Definição**

* `[cq:PseudoPage] mixin`

### cq:PageContent {#cq-pagecontent}

**Descrição**

Define o nó padrão para o conteúdo da página, com as propriedades mínimas usadas pelo WCM.

* `@prop jcr:title` - Título da página.
* `@prop jcr:description` - Descrição desta página.
* `@prop cq:template` - Caminho para o modelo usado para criar a página.
* `@prop cq:allowedTemplates` - Lista de expressões regulares usadas para determinar os caminhos para o modelo permitido.
* `@prop pageTitle` - Título geralmente exibido na `<title>` tag .
* `@prop navTitle` - Título normalmente usado na navegação.
* `@prop hideInNav` - Especifica se a página deve estar oculta na navegação.
* `@prop onTime` - Hora em que esta página se torna válida.
* `@prop offTime` - Hora em que esta página se torna inválida.
* `@prop cq:lastModified` - A data em que a página (ou seus parágrafos) foi modificada pela última vez.
* `@prop cq:lastModifiedBy` - Último usuário a alterar a página (ou seus parágrafos).
* `@prop jcr:language` - O idioma do conteúdo da página.

>[!NOTE]
>
>Não é obrigatório que o conteúdo da página use esse tipo.

**Definição**
* `[cq:PageContent] > nt:unstructured, mix:title, mix:created, cq:OwnerTaggable, sling:VanityPath, cq:ReplicationStatus, sling:Resource orderable`
   * `- cq:template (string)`
   * `- cq:allowedTemplates (string) multiple`
   * `- pageTitle (string)`
   * `- navTitle (string)`
   * `- hideInNav (boolean)`
   * `- onTime (date)`
   * `- offTime (date)`
   * `- cq:lastModified (date)`
   * `- cq:lastModifiedBy (string)`
   * `- cq:designPath (string)`
   * `- jcr:language (string)`

### cq:Template {#cq-template}

**Descrição**

Define um modelo de CQ.

* `@node jcr:content` - Conteúdo padrão para novas páginas.
* `@node icon.png` - Um arquivo que contém um ícone característico.
* `@node thumbnail.png` - Um arquivo que contém uma imagem em miniatura característica.
* `@node workflows` - Atribuir automaticamente a configuração do fluxo de trabalho. A configuração seguirá a estrutura abaixo:
   * `+ workflows`
      * `+ name1`
         * `- cq:path`
            * `- cq:workflowName`
* `@prop allowedParents` - Padrões de expressão regulares para determinar os caminhos para modelos permitidos como modelos pai.
* `@prop allowedChildren` - Padrões de expressão regulares para determinar os caminhos para modelos permitidos como modelos secundários.
* `@prop ranking` - Posição na lista de modelos na caixa de diálogo Criar página.

**Definição**

* `[cq:Template] > nt:hierarchyNode, mix:title`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
   * `+ jcr:content (nt:base) copy`
   * `+ icon.png (nt:file) copy`
   * `+ thumbnail.png (nt:file) copy`
   * `+ workflows (nt:base) copy`
   * `- allowedParents (string) multiple`
   * `- allowedChildren (string) multiple`
   * `- ranking (long)`

### cq:Component {#cq-component}

**Descrição**

Define um componente CQ.

* `@prop jcr:title` - Título do componente.
* `@prop jcr:description` - Descrição do componente.
* `@node dialog` - Caixa de diálogo principal.
* `@prop dialogPath` - Caminho da caixa de diálogo primária (alternativo à caixa de diálogo).
* `@node design_dialog` - Caixa de diálogo Design.
* `@prop cq:cellName` - Nome da célula de projeto.
* `@prop cq:isContainer` - Indica se este é um componente de container. Isso faz com que os nomes das células dos componentes filhos sejam usados em vez de nomes de caminho. Por exemplo, o componente `parsys` é um container. Se esse valor não for definido, a verificação será feita com base na existência de um `cq:childEditConfig`.
* `@prop cq:noDecoration` - Se verdadeiro, nenhuma `div` tag de decoração será desenhada ao incluir esse componente.
* `@node cq:editConfig` - A configuração que define os parâmetros da barra de edição.
* `@node cq:childEditConfig` - A configuração de edição herdada pelos componentes filhos.
* `@node cq:htmlTag` - Define atributos de tag adicionais que são adicionados à `div` tag &quot;adjacente&quot; quando o componente é incluído.
* `@node icon.png`- Um arquivo que contém um ícone característico.
* `@node thumbnail.png` - Um arquivo que contém uma imagem em miniatura característica.
* `@prop allowedParents` - Padrões de expressão regulares para determinar os caminhos dos componentes que são permitidos como componentes principais.
* `@prop allowedChildren` - Padrões de expressão regulares para determinar os caminhos dos componentes permitidos como componentes filhos.
* `@node virtual` - Contém subnós que refletem componentes virtuais usados para o componente arrastar e soltar.
* `@prop componentGroup` - Nome do grupo de componentes, usado para o componente arrastar e soltar.
* `@node cq:infoProviders` - Contém subnós, cada um com uma propriedade `className` que se refere a um `PageInfoProvider`.

**Definição**

* `[cq:Component] > nt:folder, mix:title, sling:ResourceSuperType`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
   * `+ dialog (nt:base) = nt:unstructured copy`
   * `- dialogPath (string)`
   * `+ design_dialog (nt:base) = nt:unstructured copy`
   * `- cq:cellName (string)`
   * `- cq:isContainer (boolean)`
   * `- cq:noDecoration (boolean)`
   * `+ cq:editConfig (cq:EditConfig) = cq:EditConfig copy`
   * `+ cq:childEditConfig (cq:EditConfig) = cq:EditConfig copy`
   * `+ cq:htmlTag (nt:base) = nt:unstructured copy`
   * `+ icon.png (nt:file) copy`
   * `+ thumbnail.png (nt:file) copy`
   * `- allowedParents (string) multiple`
   * `- allowedChildren (string) multiple`
   * `+ virtual (nt:base) = sling:Folder copy`
   * `- componentGroup (string)`
   * `+ cq:infoProviders (nt:base) = nt:unstructured copy`

### cq:ComponentMixin {#cq-componentmixin}

**Descrição**

Define um componente CQ como tipo de combinação.

**Definição**

`[cq:ComponentMixin] > cq:Component mixin`

### cq:EditConfig {#cq-editconfig}

**Descrição**

Define a configuração para a &quot;barra de edição&quot;.

* `@prop cq:dialogMode` - Modo da caixa de diálogo:
   * `floating` - para uma caixa de diálogo flutuante normal
   * `inline` - edição em linha
   * `auto` - detecção automática (dependendo do espaço disponível)
* `@node cq:inplaceEditing` - Inserir configuração de edição para este componente.
* `@prop cq:layout`- Layout da barra de edição:
   * `editbar` - barra de edição
   * `rollover` - rolar sobre o quadro
   * `auto` - detecção automática
* `@node cq:formParameters`- Parâmetros adicionais para adicionar ao formulário de diálogo.
* `@prop cq:actions`- Lista de ações (botões da barra de edição ou itens de menu).
* `@node cq:actionConfigs` - Configurações de widget para itens de barra de edição ou menu.
* `@prop cq:emptyText` - Texto a ser exibido se nenhum conteúdo visual estiver presente.
* `@node cq:dropTargets` - Coleção de `{@link cq:DropTargetConfig}` nós.

**Definição**

* `[cq:EditConfig] > nt:unstructured, nt:hierarchyNode orderable`
   * `- cq:dialogMode (string) < 'auto', 'floating', 'inline'`
   * `- cq:layout (string) < 'editbar', 'rollover', 'auto' + cq:formParameters (nt:base) = nt:unstructured`
   * `- cq:actions (string) multiple`
   * `+ cq:actionConfigs (nt:base) = nt:unstructured`
   * `- cq:emptyText (string)`
   * `+ cq:dropTargets (nt:base) = nt:unstructured`
   * `+ cq:listeners (nt:base) = cq:EditListenersConfig`

### cq:DropTargetConfig {#cq-droptargetconfig}

**Descrição**

Configura um público alvo de queda de um componente. O nome desse nó será usado como uma ID para arrastar e soltar.

* `@prop accept` - Lista de tipos MIME aceites por este público alvo; por exemplo, `["image/*"]`
* `@prop groups` - Lista de grupos de arrastar e soltar que aceitam uma fonte.
* `@prop propertyName` - Nome da propriedade usada para armazenar a referência.

**Definição**

* `[cq:DropTargetConfig] > nt:unstructured orderable`
   * `- accept (string) multiple`
   * `- groups (string) multiple`
   * `- propertyName (string)`
   * `+ parameters (nt:base) = nt:unstructured`

### cq:VirtualComponent {#cq-virtualcomponent}

**Descrição**

Define um componente CQ virtual. Atualmente, eles são usados apenas para o novo componente do assistente de arrastar e soltar.

* `@prop jcr:title` - Título deste componente.
* `@prop jcr:description` - Descrição deste componente.
* `@node cq:editConfig` - Edite a configuração que define os parâmetros da barra de edição.
* `@node cq:childEditConfig`- Edite a configuração herdada pelos componentes filhos.
* `@node icon.png` - Um arquivo que contém um ícone característico.
* `@node thumbnail.png` - Um arquivo que contém uma imagem em miniatura característica.
* `@prop allowedParents` - Padrões de expressão regulares para determinar os caminhos dos componentes que são permitidos como componentes principais.
* `@prop allowedChildren` - Padrões de expressão regulares para determinar os caminhos dos componentes que são permitidos como componentes filhos.
* `@prop componentGroup` - Nome do grupo de componentes para o componente arrastar e soltar.

**Definição**

`[cq:VirtualComponent] > nt:folder, mix:title`
`- * (undefined)`
`- * (undefined) multiple`
`+ * (nt:base) = nt:base multiple version`
`+ cq:editConfig (cq:EditConfig) = cq:EditConfig copy`
`+ icon.png (nt:file) copy`
`+ thumbnail.png (nt:file) copy`
`- allowedParents (string) multiple`
`- allowedChildren (string) multiple`
`- componentGroup (string)`

### cq:EditListenersConfig {#cq-editlistenersconfig}

**Descrição**

Define os ouvintes (do lado do cliente) a serem executados em um evento de edição. Os valores devem referenciar uma função de ouvinte do lado do cliente válida ou conter um atalho predefinido:

* `REFRESH_PAGE`
* `REFRESH_SELF`
* `REFRESH_PARENT`

* `@prop aftercreate` - Acionado após a criação de um componente.
* `@prop afteredit` - Acionado depois que um componente é editado (modificado).
* `@prop afterdelete` - Acionado após a exclusão de um componente.
* `@prop afterinsert` - Acionado após a adição de um componente ao container.
* `@prop afterremove` - Acionado após a remoção de um componente deste container.
* `@prop aftermove` - Acionado após a mudança dos componentes neste container.

**Definição**

* `[cq:EditListenersConfig]`
   * `- &ast; (undefined)`
   * `- &ast; (undefined) multiple`
   * `+ &ast; (nt:base) = nt:base multiple version`
   * `- aftercreate (string)`
   * `- afteredit (string)`
   * `- afterdelete (string)`
   * `- afterinsert (string)`
   * `- afterremove (string)`
   * `- aftermove (string)`

## DAM {#dam}

### dam:AssetContent {#dam-assetcontent}

**Descrição**

Conteúdo de um ativo DAM.

**Definição**

* `[dam:AssetContent] > nt:unstructured`
   * `+ metadata (nt:unstructured)`
   * `+ renditions (nt:folder)`

### dam:Asset {#dam-asset}

**Descrição**

Ativo DAM.

**Definição**

`[dam:Asset] > nt:hierarchyNode`
`+ jcr:content (dam:AssetContent) = dam:AssetContent copy primary`
`+ * (nt:base) = nt:base version`

### dam:Miniatura {#dam-thumbnail}

**Descrição**

Miniatura para representar um ativo DAM.

**Definição**

* `[dam:Thumbnails]`
   * `mixin`
   * `+ dam:thumbnails (nt:folder)`

## Lista Container Delivery {#delivery-container-list}

### cq:containerList {#cq-containerlist}

**Descrição**

Lista do Container.

**Definição**

* `[cq:containerList]`
   * `mixin`

## Página do Delivery {#delivery-page}

### cq:Cq4PageAttributes {#cq-cq-pageattributes}

**Descrição**

`cq:attributes` é o tipo de nó das tags de versão ContentBus. Este nó tem apenas uma série de propriedades; dos quais três são predefinidos &quot;created&quot;, &quot;csd&quot; e &quot;timestampe&quot;.

* `@prop created (long) mandatory copy` - Carimbo de data e hora da criação das informações da versão, geralmente a hora do check-in da versão anterior ou a hora da criação da página.
* `@prop csd (string) mandatory copy` - atributo padrão csd, cópia da propriedade cq:csd do nó da página
* `@prop timestamp (long) mandatory copy` - Carimbo de data e hora da última modificação da versão, em geral, tempo de check-in.
* `@prop * (string) copy` - Atributos adicionais, controle de versão com o nó pai.

**Definição**

* `[cq:Cq4PageAttributes] > nt:base`
   * `- created (long) mandatory copy`
   * `- csd (string) mandatory copy`
   * `- timestamp (long) mandatory copy`
   * `- &ast; (string) copy`

### cq:Cq4ContentPage {#cq-cq-contentpage}

**Descrição**

O tipo de nó `cq:contentPage` contém as definições de propriedade e nó filho para páginas de conteúdo ContentBus. Somente quando esse tipo de combinação é adicionado a um nó do tipo `cq:page`, um nó se torna uma página de conteúdo ContentBus.

Os itens em um `cq:Cq4ContentPage` são:

* `@prop cq:csd` - A CVM ContentBus da página.
* `@node cq:content` - O conteúdo da página. Esse nó filho não existe se o nó de página estiver no estado &quot;Existente sem conteúdo&quot; ou &quot;Excluído&quot;.
* `@node cq:attributes` - A lista de atributos de página, anteriormente conhecidos como tags de versão. Esse nó é obrigatório para o tipo cq:contentPage. O nó de atributos tem controle de versão quando a página é um nó com controle de versão.

**Definição**

* `[cq:Cq4ContentPage]`
   * `- cq:csd (string) mandatory copy`
   * `+ cq:attributes (cq:Cq4PageAttributes)`

## Importador {#importer}

### cq:PollConfig {#cq-pollconfig}

**Descrição**

Configuração da pesquisa.

* `@prop source (String) mandatory` - URI da fonte de dados, obrigatório e não vazio
* `@prop target (String)` - O local do público alvo onde os dados recuperados da fonte de dados são armazenados. Isso é opcional e o padrão é o nó cq:PollConfig.
* `@prop interval (Long)` - O intervalo em segundos no qual pesquisar dados novos ou atualizados da fonte de dados. Isso é opcional e o padrão é 30 minutos (1800 segundos).
* [Criação de serviços personalizados do Importador de dados para o Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/polling.html)

**Definição**

* `[cq:PollConfig]
   * `mixin`
   * `- source (String) mandatory`
   * `- target (String)`
   * `- interval (Long)`

### cq:PollConfigFolder {#cq-pollconfigfolder}

**Descrição**

O tipo de nó primário de conveniência para criar facilmente nós de configuração de pesquisa.

**Definição**

`[cq:PollConfigFolder] > sling:Folder, cq:PollConfig`

## Local {#location}

### cq:GeoLocation {#cq-geolocation-1}

**Descrição**

Uma mistura que define uma localização geográfica em graus decimais (DD).

* `@prop latitude` - Latitude codificado como duplo usando graus decimais.
* `@prop longitude` - Longitude codificada como duplo usando graus decimais.

**Definição**

* `[cq:GeoLocation]
   * `mixin`
   * `- latitude (double)`
   * `- longitude (double)`

## Correio {#mailer}

### cq:mailerMessage {#cq-mailermessage}

**Descrição**

Nódulos MailerService. O remetente usa nós que têm essa mistura como nós raiz das definições de mensagem.

**Definição**

* `[cq:mailerMessage]`
   * `mixin`
   * `- messageStatus (string)`
   * `= 'new'`
   * `mandatory autocreated`

## MSM {#msm}

### cq:LiveRelationship {#cq-liverelationship}

**Descrição**

Define uma combinação do LiveRelationship. Um nó de origem primária (controle) e um nó de cópia ativa (controlado) podem ser virtualmente vinculados por meio de um LiveRelationship.

**Definição**

* `[cq:LiveRelationship] mixin`
   * `- cq:lastRolledout (date)`
   * `- cq:lastRolledoutBy (string)`
   * `- cq:sourceUUID (string)`

### cq:LiveSync {#cq-livesync}

**Descrição**

Define uma combinação do LiveSync. Se um nó estiver envolvido em um LiveRelationship com um nó de origem primária (controle) e um nó de cópia ativa (controlado), ele será marcado como um LiveSync.

* `@prop cq:master` - Caminho da fonte primária (controle) do LiveRelationship.
* `@prop cq:isDeep` - Define se a relação está disponível para filhos.
* `@prop cq:syncTrigger` - Define quando a sincronização é acionada.
* `@node * LiveSyncAction` - Ações a serem executadas na sincronização

**Definição**

`[cq:LiveSync] > cq:LiveRelationship mixin orderable`
`+ * (cq:LiveSyncAction) = cq:LiveSyncAction`
`+ cq:LiveSyncConfig (nt:base) = cq:LiveSyncConfig`

### cq:LiveSyncCancalled {#cq-livesynccancelled}

**Descrição**

Define uma combinação LiveSyncCanceling. Cancele o comportamento do LiveSync de um nó de live copy (controlado) que pode estar envolvido em um LiveRelationship devido a um de seus pais.

* `@prop cq:isCancelledForChildren` - Define se um LiveSync é cancelado; também para crianças.

**Definição**

* `[cq:LiveSyncCancelled] > cq:LiveRelationship mixin`
   * `- cq:isCancelledForChildren (boolean)`

### cq:LiveSyncAction {#cq-livesyncaction}

**Descrição**

Define um LiveSyncAction anexado a um LiveSync.

* `@prop name` - Nome da ação
* `@prop value` - Valor de ação

**Definição**

* `[cq:LiveSyncAction] > nt:unstructured`

### cq:LiveSyncConfig {#cq-livesyncconfig}

**Descrição**

Configuração do Live Sync.

**Definição**

* `[cq:LiveSyncConfig]`
   * `- cq:master (string) mandatory`
   * `- cq:isDeep (boolean)`
   * `- cq:trigger (string) /** deprecated **/`

Para o AEM 5.4, adicione ao final da lista:

* `- cq:rolloutConfigs (string) multiple /** deprecated **/`

### cq:BlueprintAction {#cq-blueprintaction}

**Descrição**

Ação de Blueprint

**Definição**

* `[cq:BlueprintAction] > nt:unstructured`

## Plataforma {#platform}

### cq:Console {#cq-console}

**Descrição**

Define o tipo de nó de um nó de console.

**Definição**

* `[cq:Console] > sling:VanityPath, mix:title`
   * `mixin`

## Replicação {#replication}

### cq:ReplicationStatus {#cq-replicationstatus}

**Descrição**

Define a mistura de informações de status de replicação.

* `@prop cq:lastPublished`- A data em que a página foi publicada pela última vez (não é mais usada).
* `@prop cq:lastPublishedBy`- O usuário que publicou a página por último (não é mais usado).
* `@prop cq:lastReplicated` - A data em que a página foi replicada pela última vez.
* `@prop cq:lastReplicatedBy` - O usuário que replicou a página por último.
* `@prop cq:lastReplicationAction` - A ação de replicação: ativar ou desativar.
* `@prop cq:lastReplicationStatus` - O status de replicação (não é mais usado).

**Definição**

* `[cq:ReplicationStatus]
   * `mixin`
   * `- cq:lastPublished (date) ignore`
   * `- cq:lastPublishedBy (string) ignore`
   * `- cq:lastReplicated (date) ignore`
   * `- cq:lastReplicatedBy (string) ignore`
   * `- cq:lastReplicationAction (string) ignore`
   * `- cq:lastReplicationStatus (string) ignore`

## Segurança {#security}

### cq:ApplicationPrivilege {#cq-applicationprivilege}

**Descrição**

Define um privilégio de aplicativo.

**Definição**

* `[cq:ApplicationPrivilege] mixin`

### cq:PrivilegeAcl {#cq-privilegeacl}

**Descrição**

Define uma ACL de privilégio do aplicativo.

* `@prop cq:isPathDependent`
* `@node * ACEs`

**Definição**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq:PrivilegeAce {#cq-privilegeace}

**Descrição**

Define um ACE de privilégio de aplicativo.

* `@prop path`
* `@prop deny`

**Definição**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

### cq:ApplicationPrivilege {#cq-applicationprivilege-1}

**Descrição**

Define um privilégio de aplicativo.

**Definição**

* `[cq:ApplicationPrivilege] mixin`

### cq:PrivilegeAcl {#cq-privilegeacl-1}

**Descrição**

Define uma ACL de privilégio do aplicativo.

* `@prop cq:isPathDependent`
* `@node * ACEs`

**Definição**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq:PrivilegeAce {#cq-privilegeace-1}

**Descrição**

Define um ACE de privilégio de aplicativo.

* `@prop path`
* `@prop deny`

**Definição**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

## Importador de sites {#site-importer}

### cq:ComponentExtratorSource {#cq-componentextractorsource}

**Descrição**

Define um tipo de mixin que marca arquivos que podem ser abertos com o extrator de componentes.

**Definição**

`[cq:ComponentExtractorSource] mixin`

## Marcação com tags {#tagging}

### cq:Tag {#cq-tag}

**Descrição**

Define uma única tag, mas também pode conter tags, criando assim uma taxonomia

**Definição**

* `[cq:Tag] > nt:base, mix:title`
   * `- sling:resourceType (String)`
   * `- * (undefined) multiple`
   * `- * (undefined)`
   * `+ * (nt:base) = cq:Tag version`

### cq:Taggable {#cq-taggable}

**Descrição**

Mistura básica abstrata para conteúdo passível de marcação.

* `@node cq:tags`

**Definição**

* `[cq:Taggable]`
   * `- cq:tags (string) multiple`

### cq:OwnerTaggable {#cq-ownertaggable}

**Descrição**

Somente autores/proprietários têm permissão para marcar o conteúdo (marcação moderada/administrada).

**Definição**

* `[cq:OwnerTaggable] > cq:Taggable`

### cq:UserTaggable {#cq-usertaggable}

**Descrição**

Qualquer site público/usuário pode marcar o conteúdo (estilo Web2.0), usado em cq:userContent.

**Definição**

* `[cq:UserTaggable] > cq:Taggable`
   * `mixin`

### cq:AllowsUserContent {#cq-allowsusercontent}

**Descrição**

Adiciona um `cq:userContent` subnó que pode ser modificado pelos usuários. Cada usuário terá seu próprio `cq:userContent/<userid>` subnó, que normalmente tem a combinação `cq:UserTaggable`.

**Definição**

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (nt:unstructured)`

Variante estendida, definindo mais explicitamente a `cq:userContent` árvore

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (cq:UserContent)`

### cq:UserContent {#cq-usercontent}

**Descrição**

Pode ser modificado pelos usuários.

**Definição**

* `[cq:UserContent] > nt:unstructured`
   * `// userids`
   * `+ * (cq:UserData)`
   * `// other content`
   * `+ * (nt:base)`

### cq:UserData {#cq-userdata}

**Descrição**

Dados do usuário

**Definição**

* `[cq:UserData] > nt:unstructured, cq:UserTaggable`

## Widgets {#widgets}

### cq:ClientLibraryFolder {#cq-clientlibraryfolder}

**Descrição**

Pasta da biblioteca do cliente

**Definição**

* `[cq:ClientLibraryFolder] > sling:Folder`
   * `- categories (string) multiple`
   * `- dependencies (string) multiple`

### cq:Widget {#cq-widget}

**Descrição**

Widget

**Definição**

* `[cq:Widget] > nt:unstructured orderable`
   * `- xtype (string)`
   * `- name (string)`
   * `- title (string)`
   * `+ items (nt:base) = cq:WidgetCollection copy`

### cq:WidgetCollection {#cq-widgetcollection}

**Descrição**

Coleção de widgets

**Definição**

* `[cq:WidgetCollection] > nt:unstructured`
   * `orderable`
   * `+ * (cq:Widget) = cq:Widget copy`

### cq:Dialog {#cq-dialog}

**Descrição**

Caixa de diálogo

**Definição**

* `[cq:Dialog] > cq:Widget orderable`

### cq:Panel {#cq-panel}

**Descrição**

Painel

**Definição**

`[cq:Panel] > cq:Widget orderable`

### cq:TabPanel {#cq-tabpanel}

**Descrição**

Painel Guia

**Definição**

* &#39;[cq:TabPanel] > cq:Panel orderable&#39;
   * `- activeTab (long)`

### cq:Field {#cq-field}

**Descrição**

Texto

**Definição**

* `[cq:Field] > cq:Widget orderable`
   * `- fieldLabel (string)`
   * `- value (string)`
   * `- ignoreData (boolean)`

## Wiki {#wiki}

### wiki:Tópico {#wiki-topic}

**Descrição**

Tópico Wiki

**Definição**

* `[wiki:Topic] > nt:unstructured, nt:hierarchyNode, mix:versionable, mix:lockable`
   * `+ * (wiki:Topic) version`
   * `+ wiki:attachments (nt:folder) = nt:folder version`
   * `+ wiki:properties (wiki:Properties) = wiki:Properties copy`
   * `- wiki:text (string) mandatory primary`
   * `- wiki:lastModified (date) mandatory`
   * `- wiki:lastModifiedBy (string) mandatory`
   * `- wiki:topicName`
   * `- wiki:topicTitle`
   * `- wiki:lockedBy`
   * `- wiki:logMessage (string)`
   * `- wiki:quietSave (boolean)`

### wiki:Usuário {#wiki-user}

**Descrição**

Usuário Wiki

**Definição**

* `[wiki:User] mixin`
   * `- wiki:subscriptions (string) multiple`

### wiki:Propriedades {#wiki-properties}

**Descrição**

Propriedades Wiki

**Definição**

* `[wiki:Properties]`
   * `- wiki:isGlobal (boolean)`
   * `- * (undefined)`

## Fluxo de trabalho {#workflow}

### cq:Workflow {#cq-workflow}

**Descrição**

Representa uma instância de fluxo de trabalho.

**Definição**

* `[cq:Workflow] > nt:base, mix:referenceable`
   * `- modelId (String)`
   * `- modelVersion (String)`
   * `- startTime (Date)`
   * `- endTime (Date)`
   * `- initiator (String)`
   * `- &ast; (undefined)`
   * `- &ast; (undefined) multiple`
   * `- sling:resourceType (String) = "cq/workflow/components/instance" mandatory autocreated`
   * `+ workflowStack (nt:unstructured)`
   * `+ wait (nt:unstructured)`
   * `+ orTab (nt:unstructured)`
   * `+ data (cq:WorkflowData)`
   * `+ history (nt:unstructured)`
   * `+ metaData (nt:unstructured)`
   * `+ workItems (nt:unstructured)`

### cq:WorkItem {#cq-workitem}

**Descrição**

Item de trabalho.

**Definição**

* `[cq:WorkItem]`
   * `- assignee (String)`
   * `- workflowId (String)`
   * `- nodeId (String)`
   * `- startTime (Date)`
   * `- endTime (Date)`
   * `- dueTime (Date)`
   * `- sling:resourceType (String) = "cq/workflow/components/workitem" mandatory autocreated`
   * `+ metaData (nt:unstructured)`

### cq:carga {#cq-payload}

**Descrição**

Carga

**Definição**

* `[cq:Payload]`
   * `- path (Path)`
   * `- uuid (String)`
   * `- jcr:url (String)`
   * `- binary (Binary)`
   * `- javaObject (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq:WorkflowData {#cq-workflowdata}

**Descrição**

Dados do fluxo de trabalho

**Definição**

* `[cq:WorkflowData]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ payload (cq:Payload)`
   * `+ metaData (nt:unstructured) copy`

### cq:WorkflowModel {#cq-workflowmodel}

**Descrição**

Atribuição automática da configuração do fluxo de trabalho. A configuração seguirá esta estrutura abaixo:
* `workflows`
   * `+ name1`
      * `- cq:path`
      * `- cq:workflowName`
   * `+ workflows (nt:base)`

**Definição**

* `[cq:WorkflowModel] > nt:base, mix:versionable`
   * `orderable`
   * `- title (String)`
   * `- description (String)`
   * `- sling:resourceType (String) = "cq/workflow/components/model" mandatory autocreated`
   * `+ nodes (nt:unstructured)`
      * `copy`
   * `+ transitions (nt:unstructured)`
      * `copy`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq:WorkflowNode {#cq-workflownode}

**Descrição**

Nó de fluxo de trabalho

**Definição**

* `[cq:WorkflowNode] orderable`
   * `- title (String)`
   * `- description (String)`
   * `- maxIdleTime (long)`
   * `- type (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ metaData (nt:unstructured)`
      * `copy`
   * `+ timeoutConfiguration (nt:unstructured)`
      * `copy`

### cq:WorkflowTransition {#cq-workflowtransition}

**Descrição**

transição do fluxo de trabalho

**Definição**

* `[cq:WorkflowTransition] orderable`
   * `- from (String)`
   * `- to (String)`
   * `- rule (String)`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq:OrTab {#cq-ortab}

**Descrição**

Guia Ou

**Definição**

* `[cq:OrTab]`
   * `- workflowId (String) // not compulsory as this node will already be attached to the workflow node`
   * `- nodeId (String)`

### cq:Wait {#cq-wait}

**Descrição**

Aguardar

**Definição**

* `[cq:Wait]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- destNodeId (String)`
   * `- fromNodeId (String)`

### cq:WorkflowStack {#cq-workflowstack}

**Descrição**

Pilha de fluxo de trabalho

**Definição**

* `[cq:WorkflowStack]`
   * `- containeeInstanceId (String)`
   * `- parentInstanceId (String)`
   * `- nodeId (String)`

### cq:ProcessStack {#cq-processstack}

**Descrição**

Pilha de processos

**Definição**

* `[cq:ProcessStack]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- containerWorkflowModelId (String)`
   * `- containerWorkflowNodeId`
   * `- containerWorkflowEndNodeId // still needed (if name already defines that id)`

### cq:WorkflowLauncher {#cq-workflowlauncher}

**Descrição**

Iniciador de fluxo de trabalho

**Definição**

* `[cq:WorkflowLauncher]`
   * `- nodetype (String)`
   * `- glob (String)`
   * `- eventType (Long)`
   * `- description (String)`
   * `- condition (String)`
   * `- workflow (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`
