---
title: Sincronização de usuários das comunidades
description: Saiba como a sincronização de usuários funciona no Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: ecd30f5d-ad31-4482-96d3-c92f1cf91336
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2403'
ht-degree: 0%

---

# Sincronização de usuários das comunidades {#communities-user-synchronization}

## Introdução {#introduction}

Nas Comunidades Adobe Experience Manager (AEM), do ambiente Publish (dependendo das permissões configuradas), *visitantes do site* podem se tornar *membros*, criar *grupos de usuários* e editar seu *perfil de membro* .

*Os dados do usuário* referem-se a *usuários*, *perfis de usuários* e *grupos de usuários*.

*Os membros* referem-se a *usuários* registrados no ambiente Publish, em oposição aos usuários registrados no ambiente de criação.

Para obter mais informações sobre dados do usuário, visite [Gerenciando Usuários e Grupos de Usuários](/help/communities/users.md).

## Sincronização de usuários em um farm do Publish {#synchronizing-users-across-a-publish-farm}

Por design, os dados do usuário criados no ambiente do Publish não aparecem no ambiente do Autor.

A maioria dos dados do usuário criados no ambiente do Autor deve permanecer no ambiente do Autor e não é sincronizada nem replicada para instâncias do Publish.

Quando a [topologia](/help/communities/topologies.md) é um [farm de publicação](/help/sites-deploying/recommended-deploys.md#tarmk-farm), o registro e as modificações feitas em uma instância do Publish devem ser sincronizados com outras instâncias do Publish. Os membros devem poder fazer logon e ver os dados em qualquer nó do Publish.

Quando a sincronização de usuários está habilitada, os dados do usuário são sincronizados automaticamente nas instâncias do Publish no farm.

### Instruções de Configuração da Sincronização de Usuário {#user-sync-setup-instructions}

Para obter instruções detalhadas passo a passo sobre como habilitar a sincronização em um farm de publicação, consulte [Sincronização de Usuário](/help/sites-administering/sync.md).

## Sincronização do usuário em segundo plano {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **pacote vlt**

  É um arquivo zip de todas as alterações feitas em um Editor e deve ser distribuído entre os editores. As alterações em um publicador geram eventos que são escolhidos pelo ouvinte de eventos de alteração. Isso cria um pacote vlt que contém todas as alterações.

* **pacote de distribuição**

  Ele contém informações de distribuição do Sling. Essas são as informações sobre onde o conteúdo deve ser distribuído e quando ele foi distribuído por último.

## O Que Acontece Quando... {#what-happens-when}

### Site do Publish no console Sites de comunidades {#publish-site-from-communities-sites-console}

Quando um site da comunidade é publicado pelo [console de Sites de Comunidades](/help/communities/sites-console.md), o efeito é [replicar](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) as páginas associadas e o Sling distribui os grupos de usuários da comunidade criados dinamicamente, incluindo sua associação.

### O usuário é criado ou edita o perfil no Publish {#user-is-created-or-edits-profile-on-publish}

Por design, os usuários e perfis criados no ambiente do Publish (como por autorregistro, logon social, autenticação LDAP) não aparecem no ambiente do Autor.

Quando a topologia é um [farm de publicação](/help/communities/topologies.md) e a sincronização de usuário foi configurada corretamente, o *usuário* e o *perfil de usuário* são sincronizados no farm de publicação usando a distribuição Sling.

### O novo grupo da comunidade é criado no Publish {#new-community-group-is-created-on-publish}

Embora iniciada a partir de uma instância do Publish, a criação do grupo da comunidade, que resulta em novas páginas do site e um novo grupo de usuários, ocorre na instância do Autor.

Como parte do processo, as novas páginas do site são replicadas para todas as instâncias do Publish. O grupo de usuários da comunidade criado dinamicamente e seus membros são Sling distribuídos para todas as instâncias do Publish.

### Usuários ou grupos de usuários são criados usando o Console de segurança {#users-or-user-groups-are-created-using-security-console}

Por design, os dados do usuário criados no ambiente de publicação não aparecem no ambiente do Autor e vice-versa.

Quando o console [Administração e Segurança do Usuário](/help/sites-administering/security.md) é usado para adicionar novos usuários no ambiente de publicação, a sincronização de usuários sincroniza os novos usuários e suas associações de grupo para outras instâncias de publicação, se necessário. A sincronização de usuários também sincroniza grupos de usuários criados por meio do console de segurança.

### O usuário publica conteúdo no Publish {#user-posts-content-on-publish}

Para conteúdo gerado pelo usuário (UGC), os dados inseridos em uma instância de publicação são acessados por meio do [SRP configurado](/help/communities/srp-config.md).

## Práticas recomendadas {#bestpractices}

Por padrão, a sincronização do usuário está **desabilitada**. A habilitação da sincronização de usuários envolve a modificação de *configurações OSGi* existentes. Nenhuma nova configuração deve ser adicionada como resultado da ativação da sincronização do usuário.

A sincronização de usuários depende do ambiente do autor para gerenciar as distribuições de dados do usuário, mesmo que os dados do usuário não sejam criados no autor.

**Pré-requisitos**

1. Se usuários e grupos de usuários já tiverem sido criados em um editor, é recomendável [sincronizar manualmente](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) os dados do usuário para todos os editores antes de configurar e habilitar a sincronização de usuários.

   Depois que a sincronização de usuários estiver habilitada, somente os usuários e grupos recém-criados serão sincronizados.

1. Verifique se o código mais recente foi instalado:

   * [Atualizações da plataforma AEM](https://helpx.adobe.com/br/experience-manager/kb/aem62-available-hotfixes.html)
   * [Atualizações do AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

As configurações a seguir são necessárias para habilitar a sincronização de usuários no AEM Communities. Verifique se essas configurações estão corretas para evitar a falha da distribuição de conteúdo do sling.

### Apache Sling Distribution Agent - Fábrica de agentes de sincronização {#apache-sling-distribution-agent-sync-agents-factory}

Essa configuração busca o conteúdo a ser sincronizado entre os editores. A configuração está na instância do Autor. O Autor tem que acompanhar todos os editores que estão lá e onde sincronizar todas as informações.

Os valores padrão na configuração são para uma única instância de publicação. Como a sincronização de usuários é útil para sincronizar várias instâncias de publicação, como em um farm de publicação, instâncias de publicação adicionais precisam ser adicionadas à configuração.

**Como o conteúdo é sincronizado?**

A instância do autor realiza ping no ponto de extremidade do exportador dos editores. Sempre que um usuário é criado ou atualizado em editores específicos (n), o Autor obtém o conteúdo de seus endpoints de exportador e [envia o conteúdo](/help/communities/sync.md#main-pars-image-1413756164) para outros editores (n-1, ou seja, além dos editores dos quais o conteúdo é obtido).

Para configurar os agentes de sincronização do Apache Sling:

1. Faça logon com privilégios de administrador na instância de autor do AEM.
1. Acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md). Por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Localize o **Agente de Distribuição Apache Sling - Fábrica de Agentes de Sincronização**.

   * Selecione a configuração existente a ser aberta para edição (ícone de lápis).

     Verificar nome: **socialpubsync.**

   * Marque a caixa de seleção **Ativado**.
   * Selecione **Usar Várias Filas.**
   * Especifique **Endpoints do exportador** e **Endpoints do importador** (você pode adicionar mais endpoints do exportador e do importador).

     Esses endpoints definem de onde você deseja obter o conteúdo e onde você deseja enviar o conteúdo. O autor busca o conteúdo do endpoint do exportador especificado e o envia por push para os editores (diferente do editor do qual buscou o conteúdo).

   ![fato-agente-sincronização](assets/sync-agent-fact.png)

### Distribuição do Adobe Granite - Provedor secreto de transporte de senha criptografada {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

Ele permite que o autor identifique o usuário autorizado como tendo permissão para sincronizar dados do usuário a partir do autor para publicar.

O [usuário autorizado criado](/help/sites-administering/sync.md#createauthuser) em todas as instâncias de publicação ajuda os publicadores a se conectarem com o autor e configurarem a distribuição de Sling no autor. Este usuário autorizado tem todas as [ACLs](/help/sites-administering/sync.md#howtoaddacl) necessárias.

Sempre que os dados devem ser instalados ou obtidos de editores, o autor se conecta com os editores usando as credenciais (nome de usuário e senha) definidas nessa configuração.

Para conectar o autor com editores usando o usuário autorizado:

1. Faça logon com privilégios de administrador na instância de autor do AEM.
1. Acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md).

   Por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Localizar **Distribuição Do Granite Do Adobe - Provedor Secreto De Transporte De Senha Criptografada.**
1. Selecione a configuração existente a ser aberta para edição (ícone de lápis).

   Verificar propriedade **socialpubsync** - **publishUser.**

1. Defina o nome de usuário e a senha para o [usuário autorizado](/help/sites-administering/sync.md#createauthorizeduser).

   Por exemplo, **usersync - admin**

![granite-password-trans](assets/granite-paswrd-trans.png)

### Apache Sling Distribution Agent - Fábrica de agentes de fila {#apache-sling-distribution-agent-queue-agents-factory}

Essa configuração é usada para configurar os dados que você deseja sincronizar entre editores. Quando os dados são criados/atualizados em caminhos especificados em **Raízes permitidas**, o &quot;var/community/distribution/diff&quot; é ativado e o replicador criado busca os dados de um editor e os instala em outros editores.

Para configurar os dados (caminhos de nó) a serem sincronizados:

1. Faça logon com privilégios de administrador na instância de publicação.
1. Acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md).

   Por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Localize o **Agente de Distribuição Apache Sling - Fábrica de Agentes de Fila**.
1. Selecione a configuração existente a ser aberta para edição (ícone de lápis).

   Verificar Nome: **socialpubsync -reverse**

1. Marque a caixa de seleção **Habilitado** e salve.
1. Especifique os caminhos de nó que serão replicados em **Raízes permitidas**.
1. Repita para cada instância de **publicação**.

   ![fato-de-agentes-de-fila](assets/queue-agents-fact.png)

### Distribuição do Granite Adobe - Diff Observer Fatory {#adobe-granite-distribution-diff-observer-factory}

Essa configuração sincroniza a associação de grupo entre editores.
Se a alteração da associação de um grupo em um editor não atualizar sua associação em outros editores, verifique se **ref :member** foi adicionado a **nomes de propriedades pesquisados**.

Para garantir a sincronização de membros:

1. Faça logon com privilégios de administrador na instância de publicação.
1. Acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md).

   Por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Localize **Distribuição Do Granite De Adobe - Fábrica De Observadores Diff**.
1. Selecione a configuração existente a ser aberta para edição (ícone de lápis).

   Verifique o nome do agente **socialpubsync -reverse**.

1. Marque a caixa de seleção **Ativado**.
1. Especifique **rep:member** como descrição para propertyName em **nomes de propriedades pesquisados** e Salve.

   ![trabalhos de comparação](assets/diff-obs.png)

### Acionador de distribuição do Apache Sling - Fábrica de acionadores programados {#apache-sling-distribution-trigger-scheduled-triggers-factory}

Essa configuração permite configurar o intervalo de pesquisa (após o qual os editores recebem ping e as alterações são obtidas pelo autor) para sincronizar as alterações entre editores.

O autor pesquisa editores a cada 30 segundos (padrão). Se algum pacote estiver presente na pasta `/var/sling/distribution/packages/  socialpubsync -  vlt /shared`, ele buscará esses pacotes e os instalará em outros editores.

Para alterar o intervalo de pesquisa:

1. Faça logon com privilégios de administrador na instância de autor do AEM.
1. Acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md), por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Localize O **Acionador De Distribuição Do Apache Sling - Fábrica De Acionadores Agendados**

   * Selecione a configuração existente a ser aberta para edição (ícone de lápis).

     Verificar **socialpubsync -scheduled-trigger**

   * Defina o Intervalo em Segundos com o intervalo desejado e salve.

   ![acionador agendado](assets/scheduled-trigger.png)

### Ouvinte de sincronização de usuário do AEM Communities {#aem-communities-user-sync-listener}

Para problemas na distribuição Sling em que há uma discrepância nas assinaturas e nas informações a seguir, verifique se as seguintes propriedades nas configurações do **Ouvinte de sincronização de usuário do AEM Communities** estão definidas:

* NodeTypes
* IgnorableProperties
* IgnorableNodes
* PastasDistribuídas

Para sincronizar assinaturas, seguidores e notificações

Em cada instância de publicação do AEM:

1. Faça logon com privilégios de administrador.
1. Acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md). Por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Localize O **Ouvinte De Sincronização De Usuário Do AEM Communities**.
1. Selecione a configuração existente para abrir para edição (ícone de lápis)

   Verificar Nome: **socialpubsync -scheduled-trigger**

1. Defina os **NodeTypes** a seguir:

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   Os tipos de nó especificados nesta propriedade são sincronizados, e as informações de notificações (blogs e configurações seguidas) são sincronizadas entre editores diferentes.

1. Adicione todas as pastas a serem sincronizadas em **DistributedFolders**. Por exemplo,

   `segments/scoring`

   `social/relationships`

   `activities`

1. Defina os **ignorablenodes** para:

   `.tokens`

   `system`

   `rep:cache` (como as sessões adesivas são usadas, você não precisa sincronizar este nó para editores diferentes).

   ![ouvinte-de-sincronização-de-usuário](assets/user-sync-listner.png)

### ID exclusiva do Sling {#unique-sling-id}

A instância do autor AEM usa a Sling ID para identificar de onde os dados estão vindo e para quais editores ela precisa (ou não) enviar o pacote de volta.

Verifique se todos os editores em um farm de publicação têm uma ID do Sling exclusiva. Se a ID do Sling for a mesma para várias instâncias de publicação em um farm de publicação, a sincronização do usuário falhará. Como o autor não sabe de onde buscar o pacote e onde instalá-lo.

Para garantir uma ID de Sling exclusiva de editores no farm de publicação, em cada instância do Publish:

1. Navegue até [https://_host:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings).
1. Verifique o valor de **Sling ID**.

   ![slingid](assets/slingid.png)

   Se a Sling ID de uma instância do Publish corresponder à Sling ID de qualquer outra instância do Publish, então:

1. Pare uma das instâncias do Publish que tenha uma Sling ID correspondente.
1. No diretório `crx-quickstart/launchpad/felix`, procure e exclua o arquivo denominado *sling.id.file.*

   Por exemplo, em um sistema Linux:

   `rm -i $(find . -type f -name sling.id.file)`

   Por exemplo, em um sistema Windows:

   Usar o Windows Explorer e pesquisar por `sling.id.file`

1. Inicie a instância do Publish. Na inicialização, uma nova ID do Sling é atribuída a ele.
1. Valide se a **ID do Sling** agora é exclusiva.

Repita essas etapas até que todas as instâncias do Publish tenham uma Sling ID exclusiva.

### Fábrica do Package Builder do Vault {#vault-package-builder-factory}

Para que as atualizações sejam sincronizadas corretamente, é necessário modificar o construtor de pacotes do Vault para sincronização do usuário.
Em `/home/users`, um nó `*/rep:cache` é criado. É um cache usado para descobrir que, se consultarmos o nome principal de um nó, esse cache poderá ser usado diretamente.

A sincronização de usuários pode ser interrompida se `rep :cache` nós forem sincronizados entre editores.

Para garantir que as atualizações sejam sincronizadas corretamente entre editores, em cada instância do Publish AEM:

1. Acessar o [Console da Web](/help/sites-deploying/configuring-osgi.md)

   Por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Localize o **Empacotamento de Distribuição do Apache Sling - Fábrica do Construtor de Pacotes do Vault**

   Nome do construtor: socialpubsync-vlt.

1. Selecione o ícone de edição.
1. Adicionar dois filtros de nó de pacote:
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. Manuseio de política
   * Para substituir nós rep :policy existentes por novos, adicione um terceiro Filtro de Pacote: `/home/users|+.*/rep:policy`
   * Para impedir que políticas sejam distribuídas, defina: `Acl Handling: IGNORE`

   ![Fábrica do construtor de pacotes do Vault](assets/vault-package-builder-factory.png)

## Solução de problemas de distribuição de Sling no AEM Communities {#troubleshoot-sling-distribution-in-aem-communities}

Se a distribuição do Sling falhar, tente as seguintes etapas de depuração:

1. **Verificar [configurações adicionadas incorretamente](/help/sites-administering/sync.md#improperconfig)**

   Certifique-se de que várias configurações não sejam adicionadas ou editadas. Em vez disso, as configurações padrão existentes devem ser editadas.
1. **Verificar configurações**

   Verifique se todas as [configurações](/help/communities/sync.md#bestpractices) estão definidas adequadamente na instância do autor do AEM, conforme mencionado nas [Práticas recomendadas](/help/communities/sync.md#main-pars-header-863110628).

1. **Verificar permissões de usuário autorizado**

   Se os pacotes não forem instalados corretamente, verifique se o [usuário autorizado](/help/sites-administering/sync.md#createauthuser) criado na primeira instância do Publish tem as ACLs corretas.

   Para validar isso, em vez do [usuário autorizado criado](/help/sites-administering/sync.md#createauthuser), altere a configuração do [Distribuição do Granite do Adobe - Provedor Secreto de Transporte de Senha Criptografado](/help/sites-administering/sync.md#adobegraniteencpasswrd) na instância do Autor para usar credenciais de usuário administrador. Agora tente instalar os pacotes novamente. Se a sincronização do usuário funcionar bem com credenciais de administrador, significa que o usuário de publicação criado não tinha ACLs apropriadas.

1. **Verificar configuração do Diff Observer Fatory**

   Se apenas nós específicos não forem sincronizados no farm de publicação - por exemplo, os membros do grupo não serão sincronizados - verifique se a configuração [Distribuição do Granite de Adobe - Fábrica de Observadores de Diferenças](/help/sites-administering/sync.md#diffobserver) está habilitada e se **rep: membros** estão definidos em **nomes de propriedades procurados**.

1. **Verifique a configuração do Ouvinte de sincronização de usuário do AEM Communities.** Se os usuários criados estiverem sincronizados, mas as assinaturas e o seguinte não estiverem funcionando, verifique se a configuração Ouvinte de sincronização de usuário do AEM Communities:

   * Tipos de nó - definidos como **rep:User, nt:unstructured**, **nt:resource**, **rep:ACL**, **sling:Folder** e **sling:OrderedFolder**.
   * Nós ignoráveis - definidos como **.tokens**, **system** e **rep :cache**.
   * Pastas distribuídas - defina as pastas que deseja distribuir.

1. **Verificar logs gerados na criação de usuários na instância do Publish**

   Se as configurações acima estiverem definidas corretamente, mas a sincronização do usuário não estiver funcionando, verifique os logs gerados na criação do usuário.

   Verifique se a ordem dos logs é a mesma, como demonstrado a seguir:

   ```shell
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ2: ADD paths=[/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK], user=communities-user-admin
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ3: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy], user=communities-user-admin
   15.05.2016 18:33:01.757 *INFO* [sling-oak-observation-7431] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_ebb27ad9-a861-4405-9342-d64c916654e2:0.0.1
   15.05.2016 18:33:01.820 *INFO* [sling-oak-observation-7422] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_58811273-5861-48fe-95d2-4aff367b99c3:0.0.1
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK/profile]
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ4: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK/profile], user=communities-user-admin
   15.05.2016 18:33:02.273 *INFO* [sling-oak-observation-7430] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337182039_f34f4fa6-10b9-42eb-8740-4da9d4d38f99:0.0.1
   ```

Para depurar:

1. Desabilitar a sincronização de usuário:
1. Na instância do autor AEM, faça logon com privilégios de administrador.

   1. Acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md). Por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Localize a configuração **Apache Sling Distribution Agent - Fábrica de Agentes de Sincronização**.
   1. Desmarque a caixa de seleção **Habilitado**.

      Ao desativar a sincronização de usuário na instância do autor (exportador e importador), os endpoints são desativados e a instância do autor é estática. Os pacotes **vlt** não foram obtidos por ping nem por autor.

      Agora, se um usuário for criado na instância de publicação, o pacote **vlt** será criado no nó */var/sling/distribution/packages/ socialpubsync - vlt /data*. E se esses pacotes forem encaminhados pelo autor para outro serviço. Você pode baixar e extrair esses dados para verificar quais propriedades são enviadas para outros serviços.

1. Ir para um editor e criar um usuário no editor. Como resultado, eventos são criados.
1. Verifique a [ordem dos logs](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities) criados na criação do usuário.
1. Verifique se um pacote **vlt** foi criado em **/var/sling/distribution/packages/socialpubsync-vlt/data**.
1. Agora, ative a sincronização do usuário na instância do autor AEM.
1. No publicador, altere os pontos de extremidade do exportador ou do importador no **Apache Sling Distribution Agent - Sync Agents Fatory**.
Podemos baixar e extrair dados do pacote para verificar todas as propriedades que são enviadas para outros editores e quais dados são perdidos.
