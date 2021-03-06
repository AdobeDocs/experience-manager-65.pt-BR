---
title: Sincronização de usuários
seo-title: Sincronização de usuários
description: Saiba mais sobre a sincronização de usuários no AEM.
seo-description: Saiba mais sobre a sincronização de usuários no AEM.
uuid: 0a519daf-21b7-4adc-b419-eeb8c404c54f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: c061b358-8c0d-40d3-8090-dc9800309ab3
docset: aem65
exl-id: 89f55598-e749-42b8-8f2a-496f45face66
feature: Security
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '2437'
ht-degree: 3%

---

# Sincronização de usuários{#user-synchronization}

## Introdução {#introduction}

Quando a implantação é um [publish farm](/help/sites-deploying/recommended-deploys.md#tarmk-farm), os membros precisam conseguir fazer logon e ver seus dados em qualquer nó de publicação.

Usuários e grupos de usuários (dados de usuários) criados no ambiente de publicação não são necessários no ambiente de criação.

A maioria dos dados do usuário criados no ambiente de criação tem o objetivo de permanecer no ambiente de criação e não ser copiada para as instâncias de publicação.

O registro e as modificações feitas em uma instância de publicação precisam ser sincronizados com outras instâncias de publicação para que elas tenham acesso aos mesmos dados do usuário.

A partir do AEM 6.1, quando a sincronização do usuário é ativada, os dados do usuário são sincronizados automaticamente entre as instâncias de publicação no farm e não são criados no autor.

## Distribuição Sling {#sling-distribution}

Os dados do usuário, juntamente com suas [ACLs](/help/sites-administering/security.md), são armazenados no [Oak Core](/help/sites-deploying/platform.md), a camada abaixo do Oak JCR, e são acessados usando a [Oak API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/oak/api/package-tree.html). Com atualizações pouco frequentes, é razoável que os dados do usuário sejam sincronizados com outras instâncias de publicação usando [Distribuição de conteúdo de sling](https://github.com/apache/sling/blob/trunk/contrib/extensions/distribution/README.md) (distribuição do Sling).

Os benefícios da sincronização de usuários usando a distribuição do Sling, em comparação com a replicação tradicional são:

* *usuários*, perfis  *de usuários e grupos* de usuários  ** criados na publicação não são criados no autor

* A distribuição do Sling define propriedades em eventos jcr, permitindo agir dentro de ouvintes de eventos do lado da publicação sem preocupação com loops de replicação infinitos
* A distribuição do Sling envia apenas dados do usuário para instâncias de publicação não originárias, eliminando tráfego desnecessário
* [](/help/sites-administering/security.md) As ACLs definidas no nó do usuário são incluídas na sincronização

>[!NOTE]
>
>Se as sessões forem necessárias, é recomendável usar uma solução de SSO ou usar uma sessão fixa e fazer com que os clientes façam logon se mudarem para outro editor.

>[!CAUTION]
>
>A sincronização do grupo ***administradores*** não é suportada, mesmo quando a sincronização do usuário está ativada. Em vez disso, uma falha em &#39;importar o diff&#39; será registrada no log de erros.
>
>Portanto, quando a implantação é um farm de publicação, se um usuário for adicionado ou removido do grupo ***administrators**, a modificação deverá ser feita manualmente em cada instância de publicação.

## Habilitar Sincronização de Usuário {#enable-user-sync}

>[!NOTE]
>
>Por padrão, a sincronização do usuário é `disabled`.
>
>A ativação da sincronização do usuário envolve a modificação das configurações *existentes* OSGi.
>
>Nenhuma nova configuração deve ser adicionada como resultado da ativação da sincronização do usuário.

A sincronização de usuários depende do ambiente de criação para gerenciar as distribuições de dados do usuário, mesmo que os dados do usuário não sejam criados no autor. Muitas, mas não todas, das configurações ocorrem no ambiente de criação e cada etapa identifica claramente se elas devem ser executadas no autor ou na publicação.

A seguir estão as etapas necessárias para habilitar a sincronização do usuário, seguido por uma seção [Solução de problemas](#troubleshooting):

### Pré-requisitos {#prerequisites}

1. Se usuários e grupos de usuários já tiverem sido criados em um editor, é recomendável sincronizar [manualmente](#manually-syncing-users-and-user-groups) os dados do usuário para todos os editores antes de configurar e ativar a sincronização do usuário.

Quando a sincronização do usuário estiver ativada, somente os usuários e grupos recém-criados serão sincronizados.

1. Verifique se o código mais recente foi instalado:

* [Atualizações da plataforma AEM](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=pt-BR)
* [Atualizações do AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

### 1. Apache Sling Distribution Agent - Sync Agents Fatory {#apache-sling-distribution-agent-sync-agents-factory}

**Ativar sincronização de usuários**

* **sobre o autor**

   * fazer logon com privilégios de administrador
   * acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

      * por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * localizar `Apache Sling Distribution Agent - Sync Agents Factory`

      * selecione a configuração existente a ser aberta para edição (ícone de lápis)
Verificar `name`: **`socialpubsync`**

      * marque a caixa de seleção `Enabled`
      * select `Save`


![](assets/chlimage_1-20.png)

### 2. Criar Usuário Autorizado {#createauthuser}

**Configurar**
permissõesEsse usuário autorizado será usado na etapa 3 para configurar a distribuição do Sling no autor.

* **em cada instância de publicação**

   * fazer logon com privilégios de administrador
   * acesse o [Console de Segurança](/help/sites-administering/security.md)

      * por exemplo, [https://localhost:4503/useradmin](https://localhost:4503/useradmin)
   * criar um novo usuário

      * por exemplo, `usersync-admin`
   * adicionar este usuário ao grupo de usuários **`administrators`**
   * [adicionar ACL a este usuário para /home](#howtoaddacl)

      * `Allow jcr:all` com restrição  `rep:glob=*/activities/*`



>[!CAUTION]
>
>Um novo usuário deve ser criado.
>
>* O usuário padrão atribuído é **`admin`**.
>* Não use `communities-user-admin user.`

>



#### Como adicionar ACL {#addacls}

* CRXDE Lite de acesso

   * por exemplo, [https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* selecione o nó `/home`
* no painel direito, selecione a guia `Access Control`
* selecione o botão `+` para adicionar uma entrada ACL

   * **Principal**:  *procurar usuário criado para sincronização de usuário*
   * **Tipo**: `Allow`
   * **Privilégios**:  `jcr:all`
   * **** Restrictionsrep:glob:  `*/activities/*`
   * selecione **OK**

* selecione **Salvar tudo**

![](assets/chlimage_1-21.png)

Consulte também:

* [Gerenciamento de direitos de acesso](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* Seção Solução de problemas [Modificar Exceção de Operação Durante o Processamento de Resposta](#modify-operation-exception-during-response-processing).

### 3. Distribuição de Adobe Granite - Provedor secreto de transporte de senha criptografado {#adobegraniteencpasswrd}

**Configurar permissões**

Depois que um usuário autorizado, um membro do grupo de usuários **`administrators`**tiver sido criado em todas as instâncias de publicação, esse usuário autorizado deverá ser identificado no autor como tendo permissão para sincronizar os dados do usuário do autor para publicação.

* **sobre o autor**

   * fazer logon com privilégios de administrador
   * acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

      * por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * localizar `com.adobe.granite.distribution.core.impl.CryptoDistributionTransportSecretProvider.name`
   * selecione a configuração existente a ser aberta para edição (ícone de lápis)
Verificar `property name`: **`socialpubsync-publishUser`**

   * defina o nome de usuário e a senha para o [usuário autorizado](#createauthuser) criado em publicar na etapa 2

      * por exemplo, `usersync-admin`


![](assets/chlimage_1-22.png)

### 4. Apache Sling Distribution Agent - Fábrica de Agentes de Fila {#apache-sling-distribution-agent-queue-agents-factory}

**Ativar sincronização de usuários**

* **ao publicar**:

   * fazer logon com privilégios de administrador
   * acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

      * por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * localizar `Apache Sling Distribution Agent - Queue Agents Factory`

      * selecione a configuração existente a ser aberta para edição (ícone de lápis)
Verificar `Name`: `socialpubsync-reverse`

      * marque a caixa de seleção `Enabled`
      * selecione `Save`
   * **repetir **para cada instância de publicação



![](assets/chlimage_1-23.png)

### 5. Adobe Social Sync - Fábrica do Observador Diff {#diffobserver}

**Ativar sincronização de grupos**

* **em cada instância** de publicação:

   * fazer logon com privilégios de administrador
   * acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

      * por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * localizar **`Adobe Social Sync - Diff Observer Factory`**

      * selecione a configuração existente a ser aberta para edição (ícone de lápis)

         Verificar `agent name`: `socialpubsync-reverse`

      * marque a caixa de seleção `Enabled`
      * selecione `Save`


![](assets/screen-shot_2019-05-24at090809.png)

### 6. Acionador de distribuição do Apache Sling - Acionadores agendados de fábrica {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**(Opcional) modificar o intervalo de sondagem**

Por padrão, o autor pesquisará as alterações a cada 30 segundos. Para alterar esse intervalo:

* **sobre o autor**

   * fazer logon com privilégios de administrador
   * acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

      * por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * localizar `Apache Sling Distribution Trigger - Scheduled Triggers Factory`

      * selecione a configuração existente a ser aberta para edição (ícone de lápis)

         * Verificar `Name`: `socialpubsync-scheduled-trigger`
      * defina o `Interval in Seconds` para o intervalo desejado
      * selecione `Save`



![](assets/chlimage_1-24.png)

## Configurar para várias instâncias de publicação {#configure-for-multiple-publish-instances}

A configuração padrão é para uma única instância de publicação. Como o motivo para ativar a sincronização do usuário é sincronizar várias instâncias de publicação, como para um farm de publicação, as instâncias de publicação adicionais precisarão ser adicionadas à Fábrica de agentes de sincronização.

### 7. Apache Sling Distribution Agent - Sync Agents Fatory {#apache-sling-distribution-agent-sync-agents-factory-1}

**Adicionar instâncias de publicação:**

* **sobre o autor**

   * fazer logon com privilégios de administrador
   * acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

      * por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * localizar `Apache Sling Distribution Agent - Sync Agents Factory`

      * selecione a configuração existente a ser aberta para edição (ícone de lápis)
Verificar `Name`: `socialpubsync`


![](assets/chlimage_1-25.png)

* **Exportador**
EndpointsDeve haver um ponto de extremidade de exportador para cada editor. Por exemplo, se houver 2 editores, localhost:4503 e 4504, deverá haver 2 entradas:

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **Endpoints**
do importadorDeve haver um endpoint de importador para cada editor. Por exemplo, se houver 2 editores, localhost:4503 e 4504, deverá haver 2 entradas:

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* selecione `Save`

### 8. Ouvinte de sincronização de usuários do AEM Communities {#aem-communities-user-sync-listener}

**(Opcional) Sincronizar nós JCR adicionais**

Se houver dados personalizados que desejam ser sincronizados em várias instâncias de publicação, então:

* **em cada instância** de publicação:

   * fazer logon com privilégios de administrador
   * acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

      * por exemplo, `https://localhost:4503/system/console/configMgr`
   * localizar `AEM Communities User Sync Listener`
   * selecione a configuração existente a ser aberta para edição (ícone de lápis)
Verificar `Name`: `socialpubsync-scheduled-trigger`


![](assets/chlimage_1-26.png)

* ****
Tipos de nóEsta é a lista de tipos de nó que serão sincronizados. Qualquer tipo de nó diferente de sling:Folder precisa ser listado aqui (sling:folder é manipulado separadamente).
Lista padrão de tipos de nó a serem sincronizados:

   * rep:User
   * nt:unstructured
   * nt:resource

* ****
Propriedades ignoráveis: é a lista de propriedades que serão ignoradas se qualquer alteração for detectada. As alterações nessas propriedades podem ser sincronizadas como um efeito colateral de outras alterações (já que a sincronização está sempre no nível do nó), mas as alterações nessas propriedades não acionarão a sincronização por si só.
Propriedade padrão a ser ignorada:

   * cq:lastModified

* **Ignorable**
NodesSubpaths que serão totalmente ignorados durante a sincronização. Nada nesses subcaminhos será sincronizado a qualquer momento.
Nós padrão a serem ignorados:

   * .tokens
   * sistema

* **Pastas**
distribuídasA maioria das sling:Folders é ignorada porque a sincronização não é necessária. As poucas exceções estão listadas aqui.
Pastas padrão para sincronizar

   * segmentos/pontuação
   * relações sociais
   * atividades

### 9. ID de Sling exclusiva {#unique-sling-id}

>[!CAUTION]
>
>Se a ID do Sling corresponder entre duas ou mais instâncias de publicação, a sincronização do grupo de usuários falhará.

Se a ID do Sling for a mesma para várias instâncias de publicação em um farm de publicação, os grupos de usuários não serão sincronizados.

Para validar se todos os valores da ID do Sling são diferentes, em cada instância de publicação:

1. navegue até `http://<host>:<port>/system/console/status-slingsettings`
1. verifique o valor de **Sling ID**

![](assets/chlimage_1-27.png)

Se a ID do Sling de uma instância de publicação corresponder à ID do Sling de qualquer outra instância de publicação, então:

1. pare uma das instâncias de publicação que tenha uma ID do Sling correspondente
1. no diretório crx-quickstart/launchpad/felix

   * pesquise e exclua o arquivo chamado *sling.id.file*

      * por exemplo, em um sistema Linux:
         `rm -i $(find . -type f -name sling.id.file)`

      * por exemplo, em um sistema Windows:
         `use windows explorer and search for *sling.id.file*`

1. inicie a instância de publicação

   * na inicialização, será atribuído um novo Sling ID

1. verifique se o **Sling ID** agora é exclusivo

Repita essas etapas até que todas as instâncias de publicação tenham uma ID do Sling exclusiva.

## Compilador de pacote de cofre de fábrica {#vault-package-builder-factory}

Para que as atualizações sejam sincronizadas corretamente, é necessário modificar o construtor de pacotes de cofre para sincronização do usuário:

* em cada instância de publicação de AEM
* acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

   * por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* localize o `Apache Sling Distribution Packaging - Vault Package Builder Factory`

   * `Builder name: socialpubsync-vlt`

* selecione o ícone editar
* adicione dois `Package Node Filters`:

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* Tratamento de políticas:

   * para substituir os nós rep:policy existentes por novos, adicione um terceiro Filtro de Pacote:

      * `/home/users|+.*/rep:policy`
   * para evitar que as políticas sejam distribuídas, defina

      * `Acl Handling:` `IGNORE`


![Compilador de pacote de cofre de fábrica](assets/vault-package-builder-factory.png)

## O que acontece quando ... {#what-happens-when}

### Perfil de autoregistro ou edições do usuário na publicação {#user-self-registers-or-edits-profile-on-publish}

Por design, usuários e perfis criados no ambiente de publicação (autoregistro) não aparecem no ambiente do autor.

Quando a topologia é um [publish farm](/help/sites-deploying/recommended-deploys.md#tarmk-farm) e a sincronização do usuário foi configurada corretamente, o *usuário *e *perfil do usuário* são sincronizados no farm de publicação usando a distribuição do Sling.

### Usuários ou grupos de usuários são criados usando o Console de segurança {#users-or-user-groups-are-created-using-security-console}

Por design, os dados do usuário criados no ambiente de publicação não aparecem no ambiente de criação e vice-versa.

Quando o console [Administração e segurança do usuário](/help/sites-administering/security.md) é usado para adicionar novos usuários no ambiente de publicação, a sincronização do usuário sincronizará os novos usuários e sua associação de grupo com outras instâncias de publicação, se necessário. A sincronização de usuários também sincronizará os grupos de usuários criados pelo console de segurança.

## Resolução de problemas {#troubleshooting}

### Como remover a sincronização de usuários offline {#how-to-take-user-sync-offline}

Para colocar a sincronização do usuário offline, para [remover um editor](#how-to-remove-a-publisher) ou [sincronizar dados manualmente](#manually-syncing-users-and-user-groups), a fila de distribuição deve estar vazia e silenciosa.

Para verificar o estado da fila de distribuição:

* sobre o autor:

   * usando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)

      * procurar entradas em `/var/sling/distribution/packages`

         * nós de pasta nomeados com o padrão `distrpackage_*`
   * usando [Gerenciador de Pacotes](/help/sites-administering/package-manager.md)

      * procurar pacotes pendentes (ainda não instalados)

         * nomeado com o padrão `socialpubsync-vlt*`
         * criado por `communities-user-admin`


Quando a fila de distribuição estiver vazia, desative a sincronização do usuário:

* sobre o autor

   * *desmarque *a caixa de seleção `Enabled` para [Apache Sling Distribution Agent - Sync Agents Fatory](#apache-sling-distribution-agent-sync-agents-factory)

Depois que as tarefas forem concluídas, para reativar a sincronização do usuário:

* sobre o autor

   * marque a caixa de seleção `Enabled` para [Apache Sling Distribution Agent - Sync Agents Fatory](#apache-sling-distribution-agent-sync-agents-factory)

### Diagnóstico de sincronização de usuário {#user-sync-diagnostics}

O User Sync Diagnostics é uma ferramenta que verifica a configuração e tenta identificar qualquer problema.

Na criação, basta navegar do console principal por meio de **Ferramentas, Operações, Diagnóstico, Diagnóstico de Sincronização de Usuário.**

Basta entrar no console do Diagnóstico de sincronização do usuário para exibir os resultados.

O que é exibido quando a Sincronização de usuários não foi habilitada:

![](assets/chlimage_1-28.png)

#### Como executar diagnósticos para editores {#how-to-run-diagnostics-for-publishers}

Quando o diagnóstico é executado a partir do ambiente do autor, os resultados de aprovação/falha incluirão uma seção [INFO] exibindo a lista de instâncias de publicação configuradas para confirmação.

Incluído na lista é um URL para cada instância de publicação que executará o diagnóstico para essa instância. O parâmetro de url `syncUser` é anexado ao URL de diagnóstico com seu valor definido como *usuário de sincronização autorizado* criado em [Etapa 2](#createauthuser).

**Observação**: antes de iniciar o URL, o  *usuário de sincronização* autorizado já deve estar conectado a essa instância de publicação.

![](assets/chlimage_1-29.png)

### Configuração adicionada incorretamente {#configuration-improperly-added}

Quando a sincronização do usuário falha ao funcionar, o problema mais comum é que configurações adicionais eram *adicionadas*. Em vez disso, a *configuração *padrão existente deveria ter sido *editada*.

A seguir estão as exibições de como as configurações padrão editadas devem aparecer no Console da Web. Se mais de uma instância for exibida, a configuração adicionada deverá ser removida.

#### (autor) Um Apache Sling Distribution Agent - Sync Agents Fatory {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![](assets/chlimage_1-30.png)

#### (autor) Uma Credenciais de Transporte de Distribuição do Apache Sling - Credenciais de Usuário baseadas em DistributionTransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![](assets/chlimage_1-31.png)

#### (publish) One Apache Sling Distribution Agent - Queue Agents Fatory {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![](assets/chlimage_1-32.png)

#### (publicar) Uma sincronização Adobe Social - Fábrica de Observadores Diff {#publish-one-adobe-social-sync-diff-observer-factory}

![](assets/chlimage_1-33.png)

#### (autor) Um Acionador de Distribuição do Apache Sling - Acionadores agendados de fábrica {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![](assets/chlimage_1-34.png)

### Modificar Exceção da Operação Durante o Processamento de Resposta {#modify-operation-exception-during-response-processing}

Se o seguinte estiver visível no log:

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

Em seguida, verifique se a seção [2. Criar Usuário Autorizado](#createauthuser) foi seguido apropriadamente.

Esta seção descreve como criar um usuário autorizado, que existe em todas as instâncias de publicação e identificá-lo na configuração OSGi do &quot;Provedor secreto&quot; no autor. Por padrão, o usuário é `admin`.

O usuário autorizado deve se tornar um membro do grupo de usuários **`administrators`** e as permissões desse grupo não devem ser alteradas.

O usuário autorizado deve ter explicitamente os seguintes privilégios e restrições em todas as instâncias de publicação:

| **path** | **jcr:all** | **rep:glob** |
|---|---|---|
| /home | X | */atividades/* |
| /home/users | X | */atividades/* |
| /home/groups | X | */atividades/* |

Como membro do grupo `administrators`, o usuário autorizado deve ter os seguintes privilégios em todas as instâncias de publicação:

| **caminho** | **jcr:all** | **jcr:read** | **rep:write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### Falha na Sincronização do Grupo de Usuários {#user-group-sync-failed}

Se a ID do Sling corresponder entre duas ou mais instâncias de publicação, a sincronização do grupo de usuários falhará.

Consulte a seção [9. ID exclusiva do Sling](#unique-sling-id)

### Sincronizando manualmente usuários e grupos de usuários {#manually-syncing-users-and-user-groups}

* no editor em que existem usuários e grupos de usuários:

   * [se ativado, desabilitar a sincronização do usuário](#how-to-take-user-sync-offline)
   * [criar um ](/help/sites-administering/package-manager.md#creating-a-new-package) pacote de  `/home`

      * ao editar o pacote

         * Guia Filters : Adicionar filtro: Caminho raiz: `/home`
         * Guia Avançado : Manuseio de AC: `Overwrite`
   * [exportar o pacote](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)


* em outras instâncias de publicação:

   * [importar o pacote](/help/sites-administering/package-manager.md#installing-packages)

Para configurar ou habilitar a sincronização do usuário, vá para a etapa 1: [Apache Sling Distribution Agent - Sync Agents Fatory](#apache-sling-distribution-agent-sync-agents-factory)

### Quando um editor se torna indisponível {#when-a-publisher-becomes-unavailable}

Quando uma instância de publicação se tornar indisponível, ela não deverá ser removida se estiver novamente online no futuro. As alterações serão colocadas em fila para o editor e, uma vez online novamente, as alterações serão processadas.

Se a instância de publicação nunca voltar a ficar online, se estiver offline permanentemente, ela deverá ser removida, pois a construção de fila resultará no uso notável do espaço em disco no ambiente do autor.

Quando um editor estiver inativo, o log de autor terá exceções semelhantes a:

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### Como remover um editor {#how-to-remove-a-publisher}

Para remover um editor do [Apache Sling Distribution Agent - Sync Agents Fatory](#apache-sling-distribution-agent-sync-agents-factory), a fila de distribuição deve estar vazia e silenciosa.

* sobre o autor:

   * [Colocar a sincronização de utilizador offline](#how-to-take-user-sync-offline)
   * siga [etapa 7](#apache-sling-distribution-agent-sync-agents-factory) para remover o publicador de ambas as listas de servidores:

      * `Exporter Endpoints`
      * `Importer Endpoints`
   * reativar sincronização de usuários

      * marque a caixa de seleção `Enabled` para [Apache Sling Distribution Agent - Sync Agents Fatory](#apache-sling-distribution-agent-sync-agents-factory)
