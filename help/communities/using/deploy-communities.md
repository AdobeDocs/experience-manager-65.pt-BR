---
title: Implantação de comunidades
seo-title: Deploying Communities
description: Como implantar o AEM Communities
seo-description: How to deploy AEM Communities
content-type: reference
topic-tags: deploying
source-git-commit: 14a33b14043869614efcdbf8cb413333d0fa644b
workflow-type: tm+mt
source-wordcount: '1881'
ht-degree: 2%

---


# Implantação de comunidades{#deploying-communities}

## Pré-requisitos {#prerequisites}

* [Plataforma AEM 6.5](/help/sites-deploying/deploy.md)

* Licença AEM Communities

* Licenças opcionais para:

   * [Recursos do Adobe Analytics for Communities](/help/communities/analytics.md)
   * [MongoDB para MSRP](/help/communities/msrp.md)
   * [Adobe Cloud para ASRP](/help/communities/asrp.md)

## Lista de verificação da instalação {#installation-checklist}

**Para a plataforma  [AEM](/help/sites-deploying/deploy.md#what-is-aem)**:

* Instale as atualizações mais recentes do [AEM 6.5](#aem64updates).

* Se não estiver usando as portas padrão (4502, 4503), então [configure os agentes de replicação](#replication-agents-on-author).
* [Replicar chave de criptografia](#replicate-the-crypto-key)
* Se estiver dando suporte à globalização, [configure a tradução automatizada](/help/sites-administering/translation.md)
(a configuração de amostra é fornecida para desenvolvimento).

**Para o recurso  [Comunidades](/help/communities/overview.md)**:

* Se estiver implantando um [farm de publicação](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [identifique o editor principal](#primary-publisher)

* [Ativar o serviço de túnel](#tunnel-service-on-author)
* [Ativar o logon social](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Configurar o Adobe Analytics](/help/communities/analytics.md)
* Configurar um [serviço de email padrão](/help/communities/email.md)
* Identifique a opção para [armazenamento UGC compartilhado](/help/communities/working-with-srp.md) (**SRP**)

   * Se MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [Instalar e configurar o MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [Configurar Solr](/help/communities/solr.md)
      * [Selecionar MSRP](/help/communities/srp-config.md)
   * Se o banco de dados relacional SRP [(DSRP)](/help/communities/dsrp.md)

      * [Instale o driver JDBC para MySQL](#jdbc-driver-for-mysql)
      * [Instalar e configurar o MySQL para DSRP](/help/communities/dsrp-mysql.md)
      * [Configurar Solr](/help/communities/solr.md)
      * [Selecione DSRP](/help/communities/srp-config.md)
   * Se Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * Entre em contato com seu representante de conta para obter o provisionamento.
      * [Selecionar ASRP](/help/communities/srp-config.md)
   * Se JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * Não é um repositório UGC compartilhado:

         * O UGC nunca é replicado.
         * O UGC só é visível AEM instância ou cluster no qual foi inserido.
      * O padrão é JSRP

   Para o **[recurso de ativação](/help/communities/overview.md#enablement-community)**

   * [Instalar e configurar o FFmpeg](/help/communities/ffmpeg.md)
   * [Instale o driver JDBC para MySQL](#jdbc-driver-for-mysql)
   * [Instalar o AEM Communities SCORM-Engine](#scorm-package)
   * [Instalar e configurar o MySQL para ativação](/help/communities/mysql.md)






## Versões mais recentes {#latest-releases}

AEM 6.5 Communities GA inclui o pacote Communities. Para saber mais sobre atualizações para AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities), consulte [AEM Notas de versão 6.5](/help/release-notes/release-notes.md#communities-release-notes.html).

### Atualizações do AEM 6.5 {#aem-updates}

A partir do AEM 6.4, as atualizações nas Comunidades são fornecidas como parte AEM Pacotes de correções cumulativas e Service Packs.

Para obter as atualizações mais recentes do AEM 6.5, consulte [Pacotes de Correção Cumulativa e Service Packs do Adobe Experience Manager 6.4](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=pt-BR).

### Histórico da versão {#version-history}

Como em AEM 6.4 e mais, os recursos e hotfixes do AEM Communities fazem parte dos fix packs cumulativos do AEM Communities e service packs. Portanto, não há pacotes de recursos separados.

### Driver JDBC para MySQL {#jdbc-driver-for-mysql}

Dois recursos do Communities usam um banco de dados MySQL :

* Para [ativação](/help/communities/enablement.md): registrando atividades e aprendentes do SCORM
* Para [DSRP](/help/communities/dsrp.md): armazenamento de conteúdo gerado pelo usuário (UGC)

O conector MySQL deve ser obtido e instalado separadamente.

As etapas necessárias são:

1. Baixe o arquivo ZIP de [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * A versão deve ser >= 5.1.38

1. Extrair `mysql-connector-java-&lt;version&gt;-bin.jar (bundle) from the archive`
1. Use o console da Web para instalar e iniciar o pacote :

   * Por exemplo, https://localhost:4502/system/console/bundles
   * Selecionar **`Install/Update`**
   * Navegue... para selecionar o pacote extraído do arquivo ZIP baixado
   * Verifique se *Driver JDBC da Oracle Corporation para MySQLcom.mysql.jdbc* está ativo e inicie-o se não estiver (ou verifique os logs)

1. Se a instalação for feita em uma implantação existente depois que o JDBC tiver sido configurado, revincule o JDBC ao novo conector, salvando a configuração do JDBC no console da Web :

   * Por exemplo, https://localhost:4502/system/console/configMgr
   * Localize a configuração `Day Commons JDBC Connections Pool` e selecione para abrir a configuração.
   * Selecionar `Save`.

1. Repita as etapas 3 e 4 em todas as instâncias de autor e publicação.

Mais informações sobre a instalação de pacotes podem ser encontradas na página [Console da Web](/help/sites-deploying/web-console.md#bundles).

#### Exemplo : Pacote do Conector MySQL Instalado {#example-installed-mysql-connector-bundle}

![](../assets/mysql-connector.png)

### Pacote SCORM {#scorm-package}

O Shareable Content Object Reference Model (SCORM) é uma coleção de padrões e especificações para e-learning. O SCORM também define como o conteúdo pode ser empacotado em um arquivo ZIP transferível.

O mecanismo AEM Communities SCORM é necessário para o recurso [enablement](/help/communities/overview.md#enablement-community). Pacotes de pontuação compatíveis com AEM 6.5 Comunidades:

* [cq-social-scorm-package, versão 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) que inclui o mecanismo  [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) .

**Para instalar um pacote SCORM**

1. Instale o [cq-social-scorm-package, versão 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) do Compartilhamento de pacotes
1. Baixe `/libs/social/config/scorm/database_scormengine_data.sql` da instância do cq e execute-a no servidor mysql para criar um esquema scormEngineDB atualizado.
1. Adicione `/content/communities/scorm/RecordResults` na propriedade Caminhos excluídos no filtro CSRF de `https://<hostname>:<port>/system/console/configMgr` em editores.

#### Registro de SCORM {#scorm-logging}

Conforme instalado, todas as atividades de ativação são registradas no console do sistema.

Se desejar, o nível de log pode ser definido como AVISO para o pacote `RusticiSoftware.*`.

Para trabalhar com logs, consulte [Trabalhar com registros de auditoria e arquivos de log](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

### AEM MLS avançado {#aem-advanced-mls}

Para que a coleção SRP (MSRP ou DSRP) ofereça suporte a pesquisa multilíngue avançada (MLS), são necessários novos plug-ins Solr além de um esquema personalizado e uma configuração Solr. Todos os itens necessários são empacotados em um arquivo zip que pode ser baixado.

O download MLS avançado (também conhecido como &quot;phasetwo&quot;) está disponível no repositório do Adobe :

* [AEM-SOLR-MLS-phasetwo](https://repo1.maven.org/maven2/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * Versão 1.2.40, 6 de abril de 2016
   * Baixar AEM-SOLR-MLS-phasetwo-1.2.40.zip

Para obter detalhes e informações de instalação, visite [Configuração Solr](/help/communities/solr.md) para SRP.

### Sobre links para o compartilhamento de pacotes {#about-links-to-package-share}

**Pacotes visíveis no Adobe AEM Cloud**

Os links para pacotes nesta página não exigem nenhuma instância em execução do AEM, pois são para compartilhar pacotes em `adobeaemcloud.com`. Embora os pacotes possam ser visualizados, o botão `Install` é para instalar os pacotes em um site Adobe hospedado. Se você quiser instalar em uma instância de AEM local, selecionar `Install` resultará em um erro.

**Como instalar na instância de AEM local**

Para instalar os pacotes visíveis em `adobeaemcloud.com` em uma instância de AEM local, o pacote deve ser baixado primeiro em um disco local :

* Selecione a guia **Assets**
* Selecione **transferir para o disco**

Na instância de AEM local, use o gerenciador de pacotes (por exemplo [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)), para fazer upload para o repositório de pacotes AEM local.

Como alternativa, acessando o pacote usando o compartilhamento de pacote da instância de AEM local (por exemplo, [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), o botão `Download` será baixado para o repositório de pacotes da instância de AEM local.

Uma vez no repositório de pacotes da instância de AEM local, use o gerenciador de pacotes para instalar o pacote.

Para obter mais informações, visite [Como trabalhar com pacotes](/help/sites-administering/package-manager.md#package-share).

## Implantações recomendadas {#recommended-deployments}

No AEM Communities, uma loja comum é usada para armazenar conteúdo gerado pelo usuário (UGC) e geralmente é chamada de [storage resource provider (SRP)](/help/communities/working-with-srp.md). Os centros de implantação recomendados escolhem uma opção SRP para a loja comum.

A loja comum oferece suporte à moderação e ao analytics no UGC no ambiente de publicação, ao mesmo tempo em que elimina a necessidade de [replicação](/help/communities/sync.md) do UGC.

* [Armazenamento](/help/communities/working-with-srp.md)  de conteúdo da comunidade: discute as opções de armazenamento de SRP para comunidades AEM

* [Topologias](/help/communities/topologies.md)  recomendadas: discute a topologia a ser usada, dependendo do caso de uso e da escolha da SRP

## Atualização {#upgrading}

Ao atualizar para a plataforma AEM 6.5 a partir de versões anteriores do AEM, é importante ler [Atualização para AEM 6.5](/help/sites-deploying/upgrade.md).

Além de atualizar a plataforma, leia [Atualização para o AEM Communities 6.5](/help/communities/upgrade.md) para saber mais sobre as alterações do Communities.

## Configurações {#configurations}

### Editor principal {#primary-publisher}

Quando a implantação escolhida é um [publish farm](/help/communities/topologies.md#tarmk-publish-farm), uma instância de publicação AEM deve ser identificada como o **`primary publisher`** para atividades que não devem ocorrer em todas as instâncias, como recursos que dependem de **notificações** ou **Adobe Analytics**.

Por padrão, a configuração do OSGi `AEM Communities Publisher Configuration` é configurada com a caixa de seleção **`Primary Publisher`** marcada, de modo que todas as instâncias de publicação em um farm de publicação se autoidentifiquem como a primária.

Portanto, é necessário **editar a configuração em todas as instâncias de publicação secundárias** para desmarcar a caixa de seleção **`Primary Publisher`**.

![](../assets/primary-publisher.png)

Para todas as outras instâncias de publicação (secundárias) em um farm de publicação :

* Fazer logon com privilégios de administrador
* Acesse o [console da Web](/help/sites-deploying/configuring-osgi.md)

   * Por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* Localize o `AEM Communities Publisher Configuration`
* Selecione o ícone de edição
* Desmarque a caixa de seleção **Publicador primário**
* Selecione **Salvar**

### Agentes de Replicação no Autor {#replication-agents-on-author}

A replicação é usada para o conteúdo do site criado no ambiente de publicação, como grupos da comunidade, bem como para gerenciar membros e grupos de membros do ambiente de criação usando o [túnel service](#tunnel-service-on-author).

Para o editor principal, verifique se o [Replication Agent Config](/help/sites-deploying/replication.md) identifica corretamente o servidor de publicação e o usuário autorizado. O usuário autorizado padrão, `admin` já tem as permissões apropriadas (é membro de `Communities Administrators`).

Para que outro usuário tenha as permissões apropriadas, ele deve ser adicionado como membro ao grupo de usuários `administrators` (também membro de `Communities Administrators`).

Há dois agentes de replicação no ambiente de criação que precisam que a configuração de transporte seja configurada corretamente.

* Acesse o console Replicação no autor

   * Na navegação global : **Ferramentas, Implantação, Replicação, Agentes no autor**

* Siga o mesmo procedimento para ambos os agentes:

   * **Agente padrão (publicar)**
   * **Agente de replicação inversa (publicar inverso)**

      1. Selecione o agente.
      1. Selecione **edit**.
      1. Selecione a guia **Transporte**
      1. Se não a porta `4503`, edite o **URI** para especificar a porta correta.

      1. Se não for o usuário `admin`, edite as **Usuário** e **Senha** para especificar um membro do grupo de usuários `administrators`.

As imagens a seguir mostram os resultados da alteração da porta de 4503 para 6103 por :

#### Agente padrão (publicar) {#default-agent-publish}

![configure-limits](../assets/default-agent-publish.png)

#### Agente de replicação inversa (publicar inverso) {#reverse-replication-agent-publish-reverse}

![](../assets/reverse-replication-agent.png)

### Serviço de Túnel no Autor {#tunnel-service-on-author}

Ao usar o ambiente de criação para [criar sites](/help/communities/sites-console.md), [modificar propriedades do site](/help/communities/sites-console.md#modifying-site-properties) ou [gerenciar membros da comunidade](/help/communities/members.md), é necessário acessar membros (usuários) registrados no ambiente de publicação, não usuários registrados no autor.

O serviço de túnel fornece esse acesso usando o agente de replicação do autor.

Para habilitar o serviço de túnel :

* Em **author**, faça logon com privilégios administrativos.
* Se o editor não for localhost:4503 ou o usuário de transporte não for `admin`,
em seguida, [configure o agente de replicação](#replication-agents-on-author).

* Acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

   * Por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* Localize o `AEM Communities Publish Tunnel Service`
* Selecione o ícone de edição
* Marque a caixa de seleção **enable**
* selecione **Salvar**

![](../assets/tunnel-service.png)

### Replicar a chave de criptografia {#replicate-the-crypto-key}

Há dois recursos do AEM Communities que exigem que todas as instâncias do servidor AEM usem as mesmas chaves de criptografia. Esses são [Analytics](/help/communities/analytics.md) e [ASRP](/help/communities/asrp.md).

A partir do AEM 6.3, o material principal é armazenado no sistema de arquivos e não mais no repositório.

Para copiar o material principal do autor para todas as outras instâncias, é necessário:

* Acesse a instância do AEM, normalmente uma instância do autor, que contém o material principal a ser copiado

   * Localize o pacote `com.adobe.granite.crypto.file` no sistema de arquivos local

      Por exemplo,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * O arquivo `bundle.info` identificará o pacote
   * Navegar até a pasta de dados
por exemplo,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * Copie os arquivos hmac e primary node .



* Para cada instância do AEM do target

   * Navegar até a pasta de dados
por exemplo,

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * Cole os 2 arquivos copiados anteriormente
   * É necessário [atualizar o pacote do Granite Crypto](#refresh-the-granite-crypto-bundle) se a instância do AEM de destino estiver em execução no momento.


>[!CAUTION]
>
>Se já tiver sido configurado outro recurso de segurança baseado nas chaves de criptografia, a replicação das chaves de criptografia poderá danificar a configuração. Para obter ajuda, [entre em contato com o atendimento ao cliente](https://helpx.adobe.com/br/marketing-cloud/contact-support.html).

#### Replicação de Repositório {#repository-replication}

Ter o material principal armazenado no repositório, como era o caso da AEM 6.2 e anterior, pode ser preservado especificando a seguinte propriedade do sistema na primeira inicialização de cada instância de AEM (que cria o repositório inicial) :

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>É importante verificar se o [agente de replicação no autor](#replication-agents-on-author) está configurado corretamente.

Com o material principal armazenado no repositório, a maneira de replicar a chave de criptografia do autor para outras instâncias é a seguinte:

Usando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* Navegue até [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* Selecionar `/etc/key`
* Abrir a guia `Replication`
* Selecionar `Replicate`

* [atualizar o pacote Granite Crypto](#refresh-the-granite-crypto-bundle)

![](../assets/replicare-repository.png)

#### Atualizar o pacote do Granite Crypto {#refresh-the-granite-crypto-bundle}

* Em cada instância de publicação, acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

   * Por exemplo, [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* Localize o pacote `Adobe Granite Crypto Support` (com.adobe.granite.crypto)
* Selecione **Atualizar**

![](../assets/refresh-granite-bundle.png)

* Após um momento, uma caixa de diálogo **Sucesso** deve aparecer:
   `Operation completed successfully.`

### Servidor HTTP Apache {#apache-http-server}

Se estiver usando o servidor HTTP Apache, certifique-se de usar o nome correto do servidor para todas as entradas relevantes.

Em particular, tenha cuidado para usar o nome correto do servidor, não `localhost`, no `RedirectMatch`.

#### exemplo de httpd.conf {#httpd-conf-sample}

```shell
<IfModule alias_module>
     # XAMPP does not have a favicon; this prevents any 404 errors which may arise.
     Redirect 404 /favicon.ico
     <Location /favicon.ico>
         ErrorDocument 404 "No favicon"
     </Location>

    # Return from "Sign Out" generates response header directing you to "/", generating a 404 error
    # The RedirectMatch resolves it correctly when modified for the target Community Site :
    RedirectMatch ^/$ https://[server name]/content/sites/engage/en.html
 ...
 </IfModule>
```

### Dispatcher {#dispatcher}

Se estiver usando um Dispatcher, consulte :

* AEM a documentação [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)
* [Instalação do Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [Configuração do Dispatcher para Comunidades](/help/communities/dispatcher.md)
* [Problemas conhecidos](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Documentação de comunidades relacionadas {#related-communities-documentation}

* Visite [Administrando sites das comunidades](/help/communities/administer-landing.md) para saber mais sobre como criar um site da comunidade, configurar modelos de site da comunidade, moderar o conteúdo da comunidade, gerenciar membros e configurar mensagens.

* Visite [Desenvolvimento de comunidades](/help/communities/communities.md) para saber mais sobre a estrutura de componentes sociais (SCF) e a personalização de componentes e recursos das Comunidades.

* Visite [Criação de componentes do Communities](/help/communities/author-communities.md) para saber como criar com e configurar componentes do Communities.

