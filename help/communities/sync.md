---
title: Sincronização de usuários das comunidades
seo-title: Sincronização de usuários das comunidades
description: Como a sincronização do usuário funciona
seo-description: Como a sincronização do usuário funciona
uuid: 772b82bd-a66c-4c1d-b80b-dcff77c873a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 97286c2c-f6e3-43ec-b1a9-2abb58616778
docset: aem65
translation-type: tm+mt
source-git-commit: acc758b83486e8c623e31bb4a68f3c29dd4848ba

---


# Sincronização de usuários das comunidades {#communities-user-synchronization}

## Introdução {#introduction}

No AEM Communities, a partir do ambiente de publicação (dependendo das permissões configuradas), os visitantes *do* site podem se tornar *membros*, criar grupos *de* usuários e editar o perfil ** membro.

*Os dados* do usuário são um termo usado para se referir a *usuários*, perfis ** do usuário e grupos *de* usuários.

*Membros* é um termo usado para se referir a *usuários* registrados no ambiente publish, em vez de usuários registrados no ambiente author.

Para obter mais informações sobre os dados do usuário, visite [Gerenciar usuários e grupos](/help/communities/users.md)de usuários.

## Sincronizando usuários em um farm de publicação {#synchronizing-users-across-a-publish-farm}

Por padrão, os dados do usuário criados no ambiente de publicação não aparecem no ambiente do autor.

A maioria dos dados do usuário criados no ambiente do autor deve permanecer no ambiente do autor e não é sincronizada nem replicada para publicar instâncias.

Quando a [topologia](/help/communities/topologies.md) é um farm [de](/help/sites-deploying/recommended-deploys.md#tarmk-farm)publicação, o registro e as modificações feitas em uma instância de publicação precisam ser sincronizados com outras instâncias de publicação. Os membros precisam fazer logon e ver seus dados em qualquer nó de publicação.

Quando a sincronização do usuário é ativada, os dados do usuário são sincronizados automaticamente entre as instâncias de publicação no farm.

### Instruções de configuração de sincronização do usuário {#user-sync-setup-instructions}

Para obter instruções detalhadas, passo a passo, sobre como ativar a sincronização em um farm de publicação, consulte:

* [Sincronização do usuário](/help/sites-administering/sync.md)

## Sincronização do usuário em segundo plano {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **pacote vlt**

   É um arquivo zip de todas as alterações feitas em um editor, que precisam ser distribuídas entre os editores. As alterações em um editor geram eventos que são selecionados pelo ouvinte de alteração de evento. Isso cria um pacote vlt que contém todas as alterações.

* **pacote de distribuição**

   Ele contém informações de distribuição para Sling. Essas são informações sobre onde o conteúdo precisa ser distribuído e quando foi distribuído por último.

## O Que Acontece Quando... {#what-happens-when}

### Publicar site do console Sites de comunidades {#publish-site-from-communities-sites-console}

No autor, quando um site da comunidade é publicado no console [Sites da](/help/communities/sites-console.md)Comunidade, o efeito é [replicar](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) as páginas associadas e o Sling distribuir os grupos de usuários da comunidade criados dinamicamente, incluindo sua associação.

### O usuário é criado ou edita o Perfil na publicação {#user-is-created-or-edits-profile-on-publish}

Por padrão, os usuários e perfis criados no ambiente de publicação (por exemplo, por autoinscrição, login social, autenticação LDAP) não aparecem no ambiente do autor.

Quando a topologia é um farm [de](/help/communities/topologies.md) publicação e a sincronização do usuário foi configurada corretamente, o *usuário* e o perfil *do* usuário são sincronizados no farm de publicação usando a distribuição Sling.

### O novo grupo da comunidade é criado na publicação {#new-community-group-is-created-on-publish}

Embora tenha sido iniciado a partir de uma instância de publicação, a criação de grupo da comunidade, que resulta em novas páginas do site e em um novo grupo de usuários, na verdade ocorre na instância do autor.

Como parte do processo, as novas páginas do site são replicadas para todas as instâncias de publicação. O grupo de usuários da comunidade criado dinamicamente e sua associação são Sling distribuídos para todas as instâncias de publicação.

### Usuários ou grupos de usuários são criados usando o console de segurança {#users-or-user-groups-are-created-using-security-console}

Por padrão, os dados do usuário criados no ambiente de publicação não aparecem no ambiente do autor e vice-versa.

Quando o console Administração e segurança [do](/help/sites-administering/security.md) usuário for usado para adicionar novos usuários ao ambiente de publicação, a sincronização do usuário sincronizará os novos usuários e sua associação de grupo com outras instâncias de publicação, se necessário. A sincronização do usuário também sincronizará os grupos de usuários criados por meio do console de segurança.

### O usuário publica conteúdo na publicação {#user-posts-content-on-publish}

Para conteúdo gerado pelo usuário (UGC), os dados inseridos em uma instância de publicação são acessados por meio do SRP [](/help/communities/srp-config.md)configurado.

## Best practices {#bestpractices}

Por padrão, a sincronização do usuário é **desativada**. A ativação da sincronização do usuário envolve a modificação das configurações *existentes* do OSGi. Nenhuma nova configuração deve ser adicionada como resultado da ativação da sincronização do usuário.

A sincronização do usuário depende do ambiente do autor para gerenciar as distribuições de dados do usuário, mesmo que os dados do usuário não sejam criados no autor.

**Pré-requisitos**

1. Se usuários e grupos de usuários já tiverem sido criados em um editor, é recomendável sincronizar [](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) manualmente os dados do usuário com todos os editores antes de configurar e ativar a sincronização do usuário.

   Quando a sincronização do usuário estiver ativada, somente os usuários e grupos recém-criados serão sincronizados.

1. Verifique se o código mais recente foi instalado:

   * [Atualizações da plataforma AEM](https://helpx.adobe.com/br/experience-manager/kb/aem62-available-hotfixes.html)
   * [Atualizações do AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

As seguintes configurações são necessárias para permitir a sincronização do usuário no AEM Communities. Certifique-se de que essas configurações estejam corretas para evitar que a distribuição do conteúdo seja reprovada.

### Apache Sling Distribution Agent - Fábrica de agentes de sincronização {#apache-sling-distribution-agent-sync-agents-factory}

Essa configuração busca o conteúdo a ser sincronizado entre os editores. A configuração está na instância Author. O autor deve acompanhar todos os editores que estão lá e onde sincronizar todas as informações.

Os valores padrão na configuração são para uma única instância de publicação. Como a sincronização do usuário é útil para sincronizar várias instâncias de publicação, como para um farm de publicação, outras instâncias de publicação precisam ser adicionadas à configuração.

**Como o conteúdo é sincronizado?**

A instância do autor faz o ping do ponto de extremidade do exportador dos editores. Sempre que um usuário é criado ou atualizado em editores específicos (n), o Autor obtém o conteúdo dos pontos de extremidade do exportador e [envia o conteúdo](/help/communities/sync.md#main-pars-image-1413756164) para outros editores (n-1, ou seja, além dos editores a partir dos quais o conteúdo é obtido).

Para configurar os Agentes de Sincronização Apache Sling:

1. Faça logon com privilégios de administrador na sua instância do autor de AEM.
1. Acesse o Console [da Web](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html). Por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Localize o **Apache Sling Distribution Agent - Fábrica** de agentes de sincronização.

   * Selecione a configuração existente para abrir para edição (ícone de lápis).

      Verificar nome: **socialpubsync.**

   * Marque a caixa de seleção **Ativado** .
   * Selecione **Usar várias filas.**
   * Especifique os Endpoints **de** Exportador e os Endpoints **de** Importador (você pode adicionar mais pontos finais de exportador e importador).

      Esses pontos de extremidade definem de onde você deseja obter o conteúdo e de onde deseja encaminhar o conteúdo. O autor busca o conteúdo do ponto de extremidade do exportador especificado e o envia para os editores (diferente do editor a partir do qual o conteúdo foi obtido).
   ![sync-agent-actual](assets/sync-agent-fact.png)

### Distribuição do Adobe Granite - Provedor secreto de transporte de senha criptografado {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

Ela permite que o autor identifique o usuário autorizado, como tendo permissão para sincronizar os dados do usuário do autor para publicar.

O usuário [autorizado criado](/help/sites-administering/sync.md#createauthuser) em todas as instâncias de publicação ajuda os editores a se conectar ao autor e configurar a distribuição Sling no autor. Esse usuário autorizado tem todas as [ACLs](/help/sites-administering/sync.md#howtoaddacl)necessárias.

Sempre que os dados devem ser instalados ou obtidos de editores, o autor se conecta com os editores usando as credenciais (nome de usuário e senha) definidas nesta configuração.

Para conectar o autor com editores usando o usuário autorizado:

1. Faça logon com privilégios de administrador na sua instância do autor de AEM.
1. Acesse o Console [da Web](/help/sites-deploying/configuring-osgi.md).

   Por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Localizar distribuição **do Adobe Granite - Provedor secreto de transporte de senha criptografado.**
1. Selecione a configuração existente para abrir para edição (ícone de lápis).

   Verifique a propriedade **socialpubsync** - **publishUser.**

1. Defina o nome de usuário e a senha para o usuário [](/help/sites-administering/sync.md#createauthorizeduser)autorizado.

   Por exemplo, **usersync - admin**

![granito-pasword-trans](assets/granite-paswrd-trans.png)

### Apache Sling Distribution Agent - Fábrica de agentes da fila {#apache-sling-distribution-agent-queue-agents-factory}

Essa configuração é usada para configurar os dados que você deseja sincronizar entre os editores. Quando os dados são criados/atualizados em caminhos especificados em Raízes **** permitidas, a variável &quot;var/community/distribution/diff&quot; é ativada e o replicador criado obtém os dados de um editor e os instala em outros editores.

Para configurar os dados (caminhos de nó) para sincronizar:

1. Faça logon com privilégios de administrador na sua instância do autor.
1. Acesse o Console [da Web](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html).

   Por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Localize o **Apache Sling Distribution Agent - Fábrica** de agentes da fila.
1. Selecione a configuração existente para abrir para edição (ícone de lápis).

   Verificar nome: **socialpubsync - reverso**

1. Marque a caixa de seleção **Ativado** e salve.
1. Especifique os caminhos de nó que devem ser replicados nas raízes **** permitidas.
1. Repita o procedimento para cada instância de **publicação** .

   ![agentes de fila-fato](assets/queue-agents-fact.png)

### Distribuição do Adobe Granite - Fábrica de Observadores Diff {#adobe-granite-distribution-diff-observer-factory}

Essa configuração sincroniza a associação de grupo entre editores.
Se a alteração da associação de um grupo em um editor não atualizar sua associação em outros editores, verifique se **ref :Members** foi adicionado aos nomes **de propriedades** aparentes.

Para garantir a sincronização de membros:

1. Faça logon com privilégios de administrador na sua instância do autor de AEM.
1. Acesse o Console [da Web](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html).

   Por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Localize **Adobe Granite Distribution - Fábrica** de Observadores Diff.
1. Selecione a configuração existente para abrir para edição (ícone de lápis).

   Verifique o nome **do agente: socialpubsync - reverso**.

1. Marque a caixa de seleção **Ativado** .
1. Especifique **rep:Members** como descrição para propertyName em nomes **de propriedades** aparadas e Salvar.

   ![diff-obs](assets/diff-obs.png)

### Apache Sling Distribution Trigger - Fábrica de Acionadores Programados {#apache-sling-distribution-trigger-scheduled-triggers-factory}

Essa configuração permite que você configure o intervalo de sondagem (após o qual os editores são pingados e as alterações são feitas pelo autor) para sincronizar as alterações entre os editores.

O autor pesquisa os editores a cada 30 segundos (padrão). Se algum pacote estiver presente na pasta `/var/sling/distribution/packages/  socialpubsync -  vlt /shared`, ele irá buscar esses pacotes e instalá-los em outros editores.

Para alterar o intervalo de sondagem:

1. Faça logon com privilégios de administrador na sua instância do autor de AEM.
1. Acesse o console [da](/help/sites-deploying/configuring-osgi.md)Web, por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Localize o Apache Sling Distribution Trigger - Fábrica de acionadores programados ****

   * Selecione a configuração existente para abrir para edição (ícone de lápis).

      Verificar **socialpubsync -agendado-trigger**

   * Defina o intervalo em segundos para o intervalo desejado e salve.
   ![acionador agendado](assets/scheduled-trigger.png)

### Ouvinte de sincronização de usuário do AEM Communities {#aem-communities-user-sync-listener}

Para problemas na distribuição Sling em que há uma discrepância no subscrição e seguintes, verifique se as seguintes propriedades nas configurações do Ouvinte de sincronização de usuário do **** AEM Communities estão definidas:

* NodeTypes
* IgnorableProperties
* IgnorableNodes
* DistributedFolders

Para sincronizar subscrições, seguidores e notificações

Em cada instância de publicação do AEM:

1. Faça logon com privilégios de administrador.
1. Acesse o Console [da Web](/help/sites-deploying/configuring-osgi.md). Por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Localize o ouvinte **de sincronização do usuário do** AEM Communities.
1. Selecione a configuração existente para abrir para edição (ícone de lápis)

   Verificar nome: **socialpubsync - agendado-trigger**

1. Defina os seguintes **NodeTypes**:

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   Os tipos de nó especificados nesta propriedade serão sincronizados e as informações de notificações (blogs e configurações seguidas) serão sincronizadas entre diferentes editores.

1. Adicione todas as pastas para sincronizar em **DistributedFolders**. Por exemplo,

   `segments/scoring`

   `social/relationships`

   `activities`

1. Defina **ignorablenodes** como:

   `.tokens`

   `system`

   `rep:cache` (como usamos sessões adesivas, não precisamos sincronizar esse nó com editores diferentes).

   ![user-sync-listner](assets/user-sync-listner.png)

### ID de Sling exclusiva {#unique-sling-id}

A instância do autor do AEM usa a ID de Sling para identificar de onde os dados estão vindo e para quais editores precisa enviar o pacote de volta (ou não precisa).

Verifique se todos os editores em um farm de publicação têm uma Sling ID exclusiva. Se a Sling ID for a mesma para várias instâncias de publicação em um farm de publicação, a sincronização do usuário falhará. Como o autor não saberá de onde buscar o pacote e de onde instalar o pacote.

Para garantir uma ID de Sling exclusiva de editores no farm de publicação, em cada instância de publicação:

1. Navegue até [https://_host:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings).
1. Verifique o valor da **Sling ID**.

   ![slingid](assets/slingid.png)

   Se a Sling ID de uma instância de publicação corresponder à Sling ID de qualquer outra instância de publicação, então:

1. Pare uma das instâncias de publicação com uma ID de Sling correspondente.
1. No `crx-quickstart/launchpad/felix` diretório, procure e exclua o arquivo chamado *sling.id.file.*

   Por exemplo, em um sistema Linux:

   `rm -i $(find . -type f -name sling.id.file)`

   Por exemplo, em um sistema Windows:

   Usar o Windows Explorer e pesquisar por `sling.id.file`

1. Start da instância de publicação. Na inicialização, será atribuída uma nova ID de Sling.
1. Valide se a **Sling ID** agora é exclusiva.

Repita essas etapas até que todas as instâncias de publicação tenham uma Sling ID exclusiva.

### Fábrica do Criador de pacotes Vault {#vault-package-builder-factory}

Para que as atualizações sejam sincronizadas corretamente, é necessário modificar o construtor de pacote do cofre para sincronização do usuário.
Em `/home/users`, um `*/rep:cache` nó é criado. É um cache que é usado para descobrir que, se formos query no nome principal de um nó, esse cache poderá ser usado diretamente.

A sincronização do usuário pode parar se `rep :cache` os nós forem sincronizados entre os editores.

Para garantir que as atualizações sejam sincronizadas corretamente entre os editores, em cada instância de publicação do AEM:

1. Acesse o console [da Web](/help/sites-deploying/configuring-osgi.md)

   Por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Localize o Apache Sling Distribution Packaging - Fatory do Criador de pacotes do Vault ****

   Nome do construtor: socialpubsync-vlt.

1. Selecione o ícone de edição.
1. Adicione dois Filtros de nó do pacote:
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. Manuseio de políticas
   * Para substituir os nós rep existentes:policy por novos, adicione um terceiro Filtro de Pacote: `/home/users|+.*/rep:policy`
   * Para impedir que as políticas sejam distribuídas, defina: `Acl Handling: IGNORE`
   ![Fábrica do construtor de pacotes de cofre](assets/vault-package-builder-factory.png)

## Solução de problemas de distribuição Sling em AEM Communities {#troubleshoot-sling-distribution-in-aem-communities}

Se a distribuição Sling falhar, tente as seguintes etapas de depuração:

1. **Verifique se há configurações adicionadas[incorretamente](/help/sites-administering/sync.md#improperconfig)**

   Verifique se várias configurações não foram adicionadas ou editadas, em vez disso, as configurações padrão existentes devem ser editadas.
1. **Verificar configurações**

   Certifique-se de que todas as [configurações](/help/communities/sync.md#bestpractices) estejam adequadamente definidas na instância do autor de AEM, conforme mencionado nas [Práticas recomendadas](/help/communities/sync.md#main-pars-header-863110628).

1. **Verificar permissões de usuário autorizado**

   Se os pacotes não estiverem instalados corretamente, verifique se o usuário [](/help/sites-administering/sync.md#createauthuser) autorizado criado na primeira instância de Publicação possui as ACLs corretas.

   Para validar isso, em vez da configuração do usuário [autorizado](/help/sites-administering/sync.md#createauthuser) criado, altere a Distribuição do [Adobe Granite - Distribuição criptografada do provedor](/help/sites-administering/sync.md#adobegraniteencpasswrd) secreto de transporte de senha na instância do autor para usar as credenciais do usuário administrador. Agora tente instalar os pacotes novamente. Se a sincronização do usuário funcionar bem com as credenciais de administrador, isso significa que o usuário de publicação criado não tinha ACLs apropriadas.

1. **Verifique a configuração do Fatory do Observador Diff**

   Se apenas nós específicos não forem sincronizados no farm de publicação - por exemplo, os membros do grupo não serão sincronizados - verifique se a configuração [Adobe Granite Distribution - Diff Observer Fatory](/help/sites-administering/sync.md#diffobserver) está ativada e **rep: os membros** são definidos em nomes **de propriedades** procuradas.

1. **Verifique a configuração do ouvinte de sincronização do usuário do AEM Communities.** Se os usuários criados estiverem sincronizados, mas o subscrição e os seguintes itens não estiverem funcionando, verifique se a configuração do AEM Communities User Sync Listener possui:

   * Tipos de nó - definidos como **rep:User, nt:unstructed**, **nt:resource**, **rep:ACL**, **sling:Folder** e **sling:OrderedFolder**.
   * Nós ignoráveis - definidos como **.tokens**, **system** e **rep:cache**.
   * Pastas distribuídas - defina para as pastas que você deseja que sejam distribuídas.

1. **Verificar logs gerados na criação de usuários na instância Publicar**

   Se as configurações acima estiverem adequadamente definidas e a sincronização do usuário não estiver funcionando, verifique os logs gerados na criação do usuário.

   Verifique se a ordem dos registros é a mesma, como segue:

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

1. Desativar a sincronização do usuário:
1. Na instância do autor de AEM, faça logon com privilégios de administrador.

   1. Acesse o Console [da Web](/help/sites-deploying/configuring-osgi.md). Por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Localize a configuração **Apache Sling Distribution Agent - Sync Agents Fatory**.
   1. Desmarque a caixa de seleção **Ativado** .

      Ao desativar a sincronização do usuário na instância do autor, os pontos finais (exportador e importador) são desativados e a instância do autor é estática. Os pacotes **vlt** não são pingados ou buscados pelo autor.

      Agora, se um usuário for criado na instância de publicação, o pacote **vlt** será criado no nó */var/sling/distribution/packages/ socialpubsync - vlt /data* . E se esses pacotes forem encaminhados pelo autor para outro serviço. Você pode baixar e extrair esses dados para verificar quais propriedades são enviadas para outros serviços.

1. Vá até um editor e crie um usuário no editor. Como resultado, eventos são criados.
1. Verifique a [ordem dos logs](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities)criados na criação do usuário.
1. Verifique se um pacote **vlt** foi criado em **/var/sling/distribution/packages/socialpubsync-vlt/data**.
1. Agora, ative a sincronização do usuário na instância do autor de AEM.
1. No editor, altere os pontos de extremidade do exportador ou importador no **Apache Sling Distribution Agent - Sync Agents Fatory**.
Podemos baixar e extrair dados do pacote para verificar quais propriedades são enviadas para outros editores e quais dados são perdidos.
