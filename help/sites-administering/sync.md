---
title: Sincronização de usuário
seo-title: User Synchronization
description: Saiba mais sobre a sincronização de usuários no AEM.
seo-description: Learn about user synchronization in AEM.
uuid: 0a519daf-21b7-4adc-b419-eeb8c404c54f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: c061b358-8c0d-40d3-8090-dc9800309ab3
docset: aem65
exl-id: 89f55598-e749-42b8-8f2a-496f45face66
feature: Security
source-git-commit: 7803f1df1e05dc838cb458026f8dbd27de9cb924
workflow-type: tm+mt
source-wordcount: '2527'
ht-degree: 5%

---

# Sincronização de usuário{#user-synchronization}

## Introdução {#introduction}

Quando a implantação é uma [publicar farm](/help/sites-deploying/recommended-deploys.md#tarmk-farm), os membros precisam fazer logon e ver os dados em qualquer nó de publicação.

Usuários e grupos de usuários (dados do usuário) criados no ambiente de publicação não são necessários no ambiente de criação.

A maioria dos dados do usuário criados no ambiente do autor destina-se a permanecer no ambiente do autor e não ser copiada para instâncias de publicação.

O registro e as modificações feitas em uma instância de publicação precisam ser sincronizados com outras instâncias de publicação para que elas tenham acesso aos mesmos dados do usuário.

A partir do AEM 6.1, quando a sincronização de usuários é ativada, os dados do usuário são sincronizados automaticamente nas instâncias de publicação no farm e não são criados no autor.

## Distribuição Sling {#sling-distribution}

Os dados do usuário, juntamente com seus [ACLs](/help/sites-administering/security.md), são armazenados no [Oak Core](/help/sites-deploying/platform.md), a camada abaixo do Oak JCR, e são acessadas usando o [API do Oak](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/oak/api/package-tree.html). Com atualizações pouco frequentes, é razoável que os dados do usuário sejam sincronizados com outras instâncias de publicação usando [Distribuição de conteúdo do Sling](https://github.com/apache/sling/blob/trunk/contrib/extensions/distribution/README.md) (Distribuição Sling).

Os benefícios da sincronização de usuários usando a distribuição Sling, em comparação à replicação tradicional, são:

* *usuários*, *perfis de usuário* e *grupos de usuários* criados na publicação não são criados no autor

* A distribuição Sling define propriedades em eventos jcr, permitindo agir em ouvintes de eventos do lado da publicação sem preocupação com loops de replicação infinitos
* A distribuição Sling envia apenas dados do usuário para instâncias de publicação não originárias, eliminando o tráfego desnecessário
* [ACLs](/help/sites-administering/security.md) definidos no nó do usuário são incluídos na sincronização

>[!NOTE]
>
>Se as sessões forem necessárias, é recomendável usar uma solução SSO ou usar uma sessão adesiva e solicitar que os clientes façam logon se forem alternados para outra instância de publicação.

>[!CAUTION]
>
>Sincronização do **administradores** grupo não é suportado, mesmo quando a sincronização do usuário está habilitada. Em vez disso, uma falha ao &quot;importar o diferencial&quot; será registrada no log de erros.
>
>Portanto, quando a implantação for um farm de publicação, se um usuário for adicionado ou removido da variável **administradores** , a modificação deve ser feita manualmente em cada instância de publicação.

## Habilitar Sincronização de Usuário {#enable-user-sync}

>[!NOTE]
>
>Por padrão, a sincronização do usuário é `disabled`.
>
>A habilitação da sincronização de usuários envolve a modificação *existente* Configurações do OSGi.
>
>Nenhuma nova configuração deve ser adicionada como resultado da ativação da sincronização do usuário.

A sincronização de usuários depende do ambiente do autor para gerenciar as distribuições de dados do usuário, mesmo que os dados do usuário não sejam criados no autor. Grande parte, mas não toda, da configuração ocorre no ambiente de criação e cada etapa identifica claramente se deve ser executada no autor ou na publicação.

A seguir estão as etapas necessárias para habilitar a sincronização de usuários, seguidas por uma [Solução de problemas](#troubleshooting) seção:

### Pré-requisitos {#prerequisites}

1. Se usuários e grupos de usuários já tiverem sido criados em uma instância de publicação, é recomendável [sincronizar manualmente](#manually-syncing-users-and-user-groups) os dados do usuário em todas as instâncias de publicação antes de configurar e ativar a sincronização de usuários.

Quando a sincronização de usuários estiver habilitada, somente os usuários e grupos recém-criados serão sincronizados.

1. Verifique se o código mais recente foi instalado:

* [Atualizações da plataforma AEM](https://helpx.adobe.com/br/experience-manager/kb/aem62-available-hotfixes.html)
* [Atualizações do AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

### 1. Apache Sling Distribution Agent - Fábrica de agentes de sincronização {#apache-sling-distribution-agent-sync-agents-factory}

**Habilitar sincronização de usuário**

* **no autor**

   * entrar com privilégios de administrador
   * acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

      * por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * localizar `Apache Sling Distribution Agent - Sync Agents Factory`

      * selecionar a configuração existente a ser aberta para edição (ícone de lápis) Verificar `name`: **`socialpubsync`**

      * selecione o `Enabled` caixa de seleção
      * selecionar `Save`

![Apache Sling Distribution Agent](assets/chlimage_1-20.png)

### 2. Criar usuário autorizado {#createauthuser}

**Configurar permissões**
Este usuário autorizado será usado na etapa 3 para configurar a distribuição do Sling no autor.

* **em cada instância de publicação**

   * entrar com privilégios de administrador
   * acesse o [Console de segurança](/help/sites-administering/security.md)

      * por exemplo, [https://localhost:4503/useradmin](https://localhost:4503/useradmin)

   * criar um novo usuário

      * por exemplo, `usersync-admin`

   * adicionar este usuário à **`administrators`** grupo de usuários
   * [adicionar ACL para este usuário ao /home](#howtoaddacl)

      * `Allow jcr:all` com restrição `rep:glob=*/activities/*`

>[!CAUTION]
>
>Um novo usuário deve ser criado.
>
>* O usuário padrão atribuído é **`admin`**.
>* Não usar `communities-user-admin user.`
>

#### Como adicionar ACL {#addacls}

* CRXDE Lite de acesso

   * por exemplo, [https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* selecionar `/home` nó
* no painel direito, selecione a `Access Control` guia
* selecione o `+` botão para adicionar uma entrada ACL

   * **Principal**: *pesquisar usuário criado para sincronização de usuários*
   * **Tipo**: `Allow`
   * **Privilégios**: `jcr:all`
   * **Restrições** rep:glob: `*/activities/*`
   * selecionar **OK**

* selecionar **Salvar tudo**

![Janela Adicionar ACL](assets/chlimage_1-21.png)

Consulte também:

* [Gerenciamento de direitos de acesso](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* Seção Solução de problemas [Modificar Exceção de Operação Durante o Processamento de Resposta](#modify-operation-exception-during-response-processing).

### 3. Distribuição do Adobe Granite - Provedor secreto de transporte de senha criptografada {#adobegraniteencpasswrd}

**Configurar permissões**

Quando um usuário autorizado, um membro da **`administrators`** grupo de usuários, foi criado em todas as instâncias de publicação, esse usuário autorizado deve ser identificado no autor como tendo permissão para sincronizar dados do usuário do autor para publicação.

* **no autor**

   * entrar com privilégios de administrador
   * acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

      * por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * localizar `com.adobe.granite.distribution.core.impl.CryptoDistributionTransportSecretProvider.name`
   * selecionar a configuração existente a ser aberta para edição (ícone de lápis) Verificar `property name`: **`socialpubsync-publishUser`**

   * defina o nome de usuário e a senha para a variável [usuário autorizado](#createauthuser) criado ao publicar na etapa 2

      * por exemplo, `usersync-admin`

![Provedor de Segredo de Transporte de Senha Criptografado](assets/chlimage_1-22.png)

### 4. Apache Sling Distribution Agent - Fábrica de agentes de fila {#apache-sling-distribution-agent-queue-agents-factory}

**Habilitar sincronização de usuário**

* **em cada instância de publicação**:

   * entrar com privilégios de administrador
   * acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

      * por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * localizar `Apache Sling Distribution Agent - Queue Agents Factory`

      * selecionar a configuração existente a ser aberta para edição (ícone de lápis) Verificar `Name`: `socialpubsync-reverse`

      * selecione o `Enabled` caixa de seleção
      * selecionar `Save`

   * **repeat** para cada instância de publicação

![Fábrica de agentes de fila](assets/chlimage_1-23.png)

### 5. Adobe Social Sync - Diff Observer Fatory {#diffobserver}

**Habilitar sincronização de grupo**

* **em cada instância de publicação**:

   * entrar com privilégios de administrador
   * acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

      * por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * localizar **`Adobe Social Sync - Diff Observer Factory`**

      * selecionar a configuração existente a ser aberta para edição (ícone de lápis)

        Verificar `agent name`: `socialpubsync-reverse`

      * selecione o `Enabled` caixa de seleção
      * selecionar `Save`

![Fábrica de Observadores do Diff](assets/screen-shot_2019-05-24at090809.png)

### 6. Acionador de distribuição do Apache Sling - Fábrica de acionadores programados {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**(Opcional) modificar intervalo de pesquisa**

Por padrão, o autor buscará alterações a cada 30 segundos. Para alterar esse intervalo:

* **no autor**

   * entrar com privilégios de administrador
   * acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

      * por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * localizar `Apache Sling Distribution Trigger - Scheduled Triggers Factory`

      * selecionar a configuração existente a ser aberta para edição (ícone de lápis)

         * Verificar `Name`: `socialpubsync-scheduled-trigger`

      * defina o `Interval in Seconds` para o intervalo desejado
      * selecionar `Save`

![Fábrica de acionadores programados](assets/chlimage_1-24.png)

## Configurar para várias instâncias de publicação {#configure-for-multiple-publish-instances}

A configuração padrão é para uma única instância de publicação. Como o motivo para habilitar a sincronização de usuários é sincronizar várias instâncias de publicação, como em um farm de publicação, as instâncias de publicação adicionais precisarão ser adicionadas ao Sync Agents Fatory.

### 7. Apache Sling Distribution Agent - Fábrica de agentes de sincronização {#apache-sling-distribution-agent-sync-agents-factory-1}

**Adicionar instâncias de publicação:**

* **no autor**

   * entrar com privilégios de administrador
   * acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

      * por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * localizar `Apache Sling Distribution Agent - Sync Agents Factory`

      * selecionar a configuração existente a ser aberta para edição (ícone de lápis) Verificar `Name`: `socialpubsync`

![Fábrica de agentes de sincronização](assets/chlimage_1-25.png)

* **Endpoints do exportador**
Deve haver um terminal de exportador para cada instância de publicação. Por exemplo, se houver 2 instâncias de publicação, localhost:4503 e 4504, deverá haver 2 entradas:

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **Endpoints do importador**
Deve haver um endpoint de importador para cada instância de publicação. Por exemplo, se houver 2 instâncias de publicação, localhost:4503 e 4504, deverá haver 2 entradas:

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* selecionar `Save`

### 8. Ouvinte de sincronização de usuário do AEM Communities {#aem-communities-user-sync-listener}

**(Opcional) Sincronizar nós JCR adicionais**

Se houver dados personalizados que você deseja sincronizar em várias instâncias de publicação, então:

* **em cada instância de publicação**:

   * entrar com privilégios de administrador
   * acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

      * por exemplo, `https://localhost:4503/system/console/configMgr`

   * localizar `AEM Communities User Sync Listener`
   * selecionar a configuração existente a ser aberta para edição (ícone de lápis) Verificar `Name`: `socialpubsync-scheduled-trigger`

![Ouvinte de sincronização de usuário do AEM Communities](assets/chlimage_1-26.png)

* **Tipos de nós**
Esta é a lista de tipos de nó que serão sincronizados. Qualquer tipo de nó diferente de sling:Folder precisa ser listado aqui (sling:folder é manipulado separadamente).
Lista padrão de tipos de nó a serem sincronizados:

   * rep:Usuário
   * nt:unstructured
   * nt:resource

* **Propriedades ignoráveis**
Esta é a lista de propriedades que serão ignoradas se qualquer alteração for detectada. As alterações nessas propriedades podem ser sincronizadas como um efeito colateral de outras alterações (já que a sincronização está sempre no nível do nó), mas as alterações nessas propriedades não acionarão a sincronização sozinhas.
Propriedade padrão a ignorar:

   * cq:lastModified

* **Nós ignoráveis**
Subcaminhos que serão totalmente ignorados durante a sincronização. Nada nesses subcaminhos será sincronizado a qualquer momento.
Nós padrão a ignorar:

   * .tokens
   * system

* **Pastas Distribuídas**
A maioria das sling:Folders é ignorada porque a sincronização não é necessária. As poucas exceções estão listadas aqui.
Pastas padrão a serem sincronizadas

   * segmentos/pontuação
   * social/relacionamentos
   * atividades

### 9. ID exclusiva do Sling {#unique-sling-id}

>[!CAUTION]
>
>Se a ID do Sling corresponder entre duas ou mais instâncias de publicação, a sincronização do grupo de usuários falhará.

Se a ID do Sling for a mesma para várias instâncias de publicação em um farm de publicação, os grupos de usuários não serão sincronizados.

Para validar se todos os valores de ID do Sling diferem, em cada instância de publicação:

1. navegar até `http://<host>:<port>/system/console/status-slingsettings`
1. verifique o valor de **ID do Sling**

![Verificação do valor da ID do Sling](assets/chlimage_1-27.png)

Se a Sling ID de uma instância de publicação corresponder à Sling ID de qualquer outra instância de publicação, então:

1. parar uma das instâncias de publicação que tenha uma Sling ID correspondente
1. no diretório crx-quickstart/launch/felix

   * procure e exclua o arquivo chamado *sling.id.file*

      * por exemplo, em um sistema Linux:
        `rm -i $(find . -type f -name sling.id.file)`

      * por exemplo, em um sistema Windows:
        `use windows explorer and search for *sling.id.file*`

1. iniciar a instância de publicação

   * na inicialização, ele receberá uma nova ID do Sling

1. validar que o **ID do Sling** agora é único

Repita essas etapas até que todas as instâncias de publicação tenham uma Sling ID exclusiva.

## Fábrica do Package Builder do Vault {#vault-package-builder-factory}

Para que as atualizações sejam sincronizadas corretamente, é necessário modificar o construtor de pacotes do Vault para sincronização do usuário:

* em cada instância de publicação do AEM
* acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

   * por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* localize o `Apache Sling Distribution Packaging - Vault Package Builder Factory`

   * `Builder name: socialpubsync-vlt`

* selecionar o ícone editar
* adicionar dois `Package Node Filters`:

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* tratamento de políticas:

   * para substituir os nós rep:policy existentes por novos, adicione um terceiro Filtro de Pacote:

      * `/home/users|+.*/rep:policy`

   * para impedir a distribuição de políticas, defina

      * `Acl Handling:` `IGNORE`

![Fábrica do Package Builder do Vault](assets/vault-package-builder-factory.png)

## O Que Acontece Quando... {#what-happens-when}

### O usuário se registra ou edita o perfil ao publicar {#user-self-registers-or-edits-profile-on-publish}

Por design, os usuários e perfis criados no ambiente de publicação (autorregistro) não aparecem no ambiente de criação.

Quando a topologia é uma [publicar farm](/help/sites-deploying/recommended-deploys.md#tarmk-farm) e a sincronização do usuário tiver sido configurada corretamente, a variável *usuário* e *perfil do usuário* é sincronizado no farm de publicação usando a Distribuição Sling.

### Usuários ou grupos de usuários são criados usando o Console de segurança {#users-or-user-groups-are-created-using-security-console}

Por design, os dados do usuário criados no ambiente de publicação não aparecem no ambiente de criação e vice-versa.

Quando a variável [Administração e segurança do usuário](/help/sites-administering/security.md) O console é usado para adicionar novos usuários no ambiente de publicação. A sincronização de usuários sincronizará os novos usuários e sua associação de grupo com outras instâncias de publicação, se necessário. A sincronização de usuários também sincronizará grupos de usuários criados por meio do console de segurança.

## Resolução de problemas {#troubleshooting}

### Como colocar a sincronização de usuários off-line {#how-to-take-user-sync-offline}

Para colocar a sincronização do usuário off-line, para [remover uma instância de publicação](#how-to-remove-a-publish-instance) ou [sincronizar dados manualmente](#manually-syncing-users-and-user-groups), a fila de distribuição deve estar vazia e silenciosa.

Para verificar o estado da fila de distribuição:

* no autor:

   * usar [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)

      * procurar entradas em `/var/sling/distribution/packages`

         * nós de pasta nomeados com o padrão `distrpackage_*`

   * usar [Gerenciador de pacotes](/help/sites-administering/package-manager.md)

      * procurar pacotes pendentes (ainda não instalados)

         * nomeado com o padrão `socialpubsync-vlt*`
         * criado por `communities-user-admin`

Quando a fila de distribuição estiver vazia, desabilitar sincronização de usuário:

* no autor

   * *desmarque *a opção `Enabled` caixa de seleção para [Apache Sling Distribution Agent - Fábrica de agentes de sincronização](#apache-sling-distribution-agent-sync-agents-factory)

Quando as tarefas forem concluídas, para reativar a sincronização de usuários:

* no autor

   * verifique a `Enabled` caixa de seleção para [Apache Sling Distribution Agent - Fábrica de agentes de sincronização](#apache-sling-distribution-agent-sync-agents-factory)

### Diagnóstico de sincronização de usuário {#user-sync-diagnostics}

O Diagnóstico de sincronização de usuário é uma ferramenta que verifica a configuração e tenta identificar quaisquer problemas.

Na criação, basta navegar do console principal até **Ferramentas, Operações, Diagnóstico, Diagnóstico de sincronização de usuário.**

Basta inserir o console Diagnóstico de sincronização de usuário para exibir os resultados.

Isso é exibido quando a Sincronização de Usuário não foi habilitada:

![Aviso de que o Diagnóstico de Sincronização de Usuário não está habilitado](assets/chlimage_1-28.png)

#### Como executar diagnósticos para instâncias de publicação {#how-to-run-diagnostics-for-publish-instances}

Quando o diagnóstico for executado no ambiente do autor, os resultados de aprovação/falha incluirão uma [INFORMAÇÕES] exibindo a lista de instâncias de publicação configuradas para confirmação.

Está incluído na lista um URL para cada instância de publicação que executará o diagnóstico para essa instância. O parâmetro de URL `syncUser` é anexado ao URL de diagnóstico com o valor definido como *usuário de sincronização autorizado* criado em [Etapa 2](#createauthuser).

**Nota**: antes de iniciar o URL, a variável *usuário de sincronização autorizado* já deve estar conectado a essa instância de publicação.

![Diagnóstico para instâncias de publicação](assets/chlimage_1-29.png)

### Configuração adicionada incorretamente {#configuration-improperly-added}

Quando a sincronização de usuários falha ao funcionar, o problema mais comum é que configurações adicionais foram *adicionado*. Em vez disso, a configuração padrão *existente *deve ter sido *editado*.

Veja a seguir como as configurações padrão editadas devem aparecer no Console da Web. Se mais de uma instância for exibida, a configuração adicionada deverá ser removida.

#### (autor) One Apache Sling Distribution Agent - Fábrica de agentes de sincronização {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![Exibição das configurações padrão editadas no Console da Web](assets/chlimage_1-30.png)

#### (autor) Credenciais de transporte de distribuição do Apache Sling - credenciais do usuário com base em DistributionTransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![Exibição das configurações padrão editadas no Console da Web](assets/chlimage_1-31.png)

#### (publicar) Um Agente de distribuição de sling do Apache - Fábrica de agentes de fila {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![Exibição das configurações padrão editadas no Console da Web](assets/chlimage_1-32.png)

#### (publicar) One Adobe Social Sync - Diff Observer Fatory {#publish-one-adobe-social-sync-diff-observer-factory}

![Exibição das configurações padrão editadas no Console da Web](assets/chlimage_1-33.png)

#### (autor) Um acionador de distribuição do Apache Sling - Fábrica de acionadores programados {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![Exibição das configurações padrão editadas no Console da Web](assets/chlimage_1-34.png)

### Modificar Exceção de Operação Durante o Processamento de Resposta {#modify-operation-exception-during-response-processing}

Se o seguinte estiver visível no log:

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

Em seguida, verifique se [2. Criar usuário autorizado](#createauthuser) foi seguido corretamente.

Esta seção descreve como criar um usuário autorizado, que existe em todas as instâncias de publicação, e identificá-lo na configuração OSGi &quot;Provedor secreto&quot; no autor. Por padrão, o `admin`.

O usuário autorizado deve se tornar membro do **`administrators`** o grupo de usuários e as permissões para esse grupo não devem ser alteradas.

O usuário autorizado deve ter explicitamente os seguintes privilégios e restrições em todas as instâncias de publicação:

| **caminho** | **jcr:all** | **representante:glob** |
|---|---|---|
| /home | X | &#42;/atividades/&#42; |
| /home/users | X | &#42;/atividades/&#42; |
| /home/groups | X | &#42;/atividades/&#42; |

Como membro do `administrators` o usuário autorizado deve ter os seguintes privilégios em todas as instâncias de publicação:

| **caminho** | **jcr:all** | **jcr:read** | **rep:write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### Falha na sincronização do grupo de usuários {#user-group-sync-failed}

Se a ID do Sling corresponder entre duas ou mais instâncias de publicação, a sincronização do grupo de usuários falhará.

Consulte a seção [9. ID exclusiva do Sling](#unique-sling-id)

### Sincronizando usuários e grupos de usuários manualmente {#manually-syncing-users-and-user-groups}

* em instâncias de publicação nas quais existem usuários e grupos de usuários:

   * [se ativado, desativa a sincronização de usuários](#how-to-take-user-sync-offline)
   * [criar um pacote](/help/sites-administering/package-manager.md#creating-a-new-package) de `/home`

      * ao editar o pacote

         * Guia Filtros: Adicionar filtro: Caminho raiz: `/home`
         * Guia Avançado: Manuseio de AC: `Overwrite`

   * [exportar o pacote](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)

* em outras instâncias de publicação:

   * [importar o pacote](/help/sites-administering/package-manager.md#installing-packages)

Para configurar ou habilitar a sincronização de usuários, vá para a etapa 1: [Apache Sling Distribution Agent - Fábrica de agentes de sincronização](#apache-sling-distribution-agent-sync-agents-factory)

### Quando uma instância de publicação se torna indisponível {#when-a-publish-instance-becomes-unavailable}

Quando uma instância de publicação se tornar indisponível, ela não deverá ser removida se estiver online novamente no futuro. As alterações serão colocadas em fila para a instância de publicação e, quando estiver online novamente, as alterações serão processadas.

Se a instância de publicação nunca estiver online novamente, se estiver offline permanentemente, ela deverá ser removida, pois o acúmulo da fila resultará no uso notável do espaço em disco no ambiente do autor.

Quando uma instância de publicação estiver inativa, o log do autor terá exceções semelhantes a:

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### Como remover uma instância de publicação {#how-to-remove-a-publish-instance}

Para remover uma instância de publicação da [Apache Sling Distribution Agent - Fábrica de agentes de sincronização](#apache-sling-distribution-agent-sync-agents-factory), a fila de distribuição deve estar vazia e silenciosa.

* no autor:

   * [Colocar a sincronização do usuário offline](#how-to-take-user-sync-offline)
   * seguir [etapa 7](#apache-sling-distribution-agent-sync-agents-factory) para remover a instância de publicação de ambas as listas de servidores:

      * `Exporter Endpoints`
      * `Importer Endpoints`

   * reativar sincronização de usuário

      * verifique a `Enabled` caixa de seleção para [Apache Sling Distribution Agent - Fábrica de agentes de sincronização](#apache-sling-distribution-agent-sync-agents-factory)
