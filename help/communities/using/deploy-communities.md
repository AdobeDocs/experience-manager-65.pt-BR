---
title: Implantação de comunidades
seo-title: Implantação de comunidades
description: Como implantar o AEM Communities
seo-description: Como implantar o AEM Communities
uuid: 18d9b424-004d-43b2-968a-318e27a93759
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: c8d7355f-5a70-40d1-bf22-62fab8002ea0
docset: aem65
translation-type: tm+mt
source-git-commit: 7e05502b590fb2c7c36919f94611efe999262d32
workflow-type: tm+mt
source-wordcount: '1890'
ht-degree: 1%

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

**Para a plataforma[AEM](/help/sites-deploying/deploy.md#what-is-aem)**

* instale as atualizações mais recentes [AEM 6.5](#aem64updates)

* se não estiver usando as portas padrão (4502, 4503), [configure os agentes de replicação](#replication-agents-on-author)
* [replicar a chave de criptografia](#replicate-the-crypto-key)
* se estiver suportando a globalização, [configure a tradução](/help/sites-administering/translation.md)automática (a configuração de amostra é fornecida para desenvolvimento)

**Capacidade das[Comunidades](/help/communities/overview.md)**

* se estiver implantando um farm [de](/help/sites-deploying/recommended-deploys.md#tarmk-farm)publicação, [identifique o editor principal](#primary-publisher)

* [ativar o serviço de túnel](#tunnel-service-on-author)
* [ativar login social](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [configurar Adobe Analytics](/help/communities/analytics.md)
* configurar um serviço de email [padrão](/help/communities/email.md)
* identificar a escolha do armazenamento [UGC](/help/communities/working-with-srp.md) compartilhado (**SRP**)

   * se MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [instalar e configurar o MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [configurar Solr](/help/communities/solr.md)
      * [selecionar MSRP](/help/communities/srp-config.md)
   * se SRP [(DSRP) de banco de dados relacional](/help/communities/dsrp.md)

      * [instale o driver JDBC para MySQL](#jdbc-driver-for-mysql)
      * [instalar e configurar o MySQL para DSRP](/help/communities/dsrp-mysql.md)
      * [configurar Solr](/help/communities/solr.md)
      * [selecione DSRP](/help/communities/srp-config.md)
   * se Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * trabalhe com seu representante de conta para provisionamento
      * [selecionar ASRP](/help/communities/srp-config.md)
   * se JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * não é um repositório UGC compartilhado :

         * O UGC nunca é replicado
         * UGC visível somente na instância AEM ou cluster em que foi inserido
      * o padrão é JSRP

   Para o recurso de **[ativação](/help/communities/overview.md#enablement-community)**

   * [instalar e configurar FFmpeg](/help/communities/ffmpeg.md)
   * [instale o driver JDBC para MySQL](#jdbc-driver-for-mysql)
   * [instale o AEM Communities SCORM-Engine](#scorm-package)
   * [instalar e configurar o MySQL para ativação](/help/communities/mysql.md)






## Latest Releases {#latest-releases}

AEM 6,5 Communities GA é fornecido com o pacote Communities. Para saber mais sobre atualizações para AEM 6.5 [Comunidades](/help/release-notes/release-notes.md#experiencemanagercommunities), consulte [AEM Notas](/help/release-notes/release-notes.md#communities-release-notes.html)de versão 6.5.

### AEM 6.5 Atualizações {#aem-updates}

A partir do AEM 6.4, as atualizações nas Comunidades são fornecidas como parte AEM Cumulative Fix Packs e Service Packs.

Para obter as atualizações mais recentes do AEM 6.5, consulte Pacotes de correções cumulativos e Service Packs [do](https://helpx.adobe.com/br/experience-manager/aem-releases-updates.html)Adobe Experience Manager 6.4.

### Histórico da versão {#version-history}

Como em AEM 6.4 e mais, os recursos e hotfixes da AEM Communities fazem parte dos pacotes de reparos cumulativos e service packs da AEM Communities. Por conseguinte, não existem pacotes de elementos separados.

### Driver JDBC para MySQL {#jdbc-driver-for-mysql}

Dois recursos das Comunidades usam um banco de dados MySQL:

* para [ativação](/help/communities/enablement.md) : gravando atividades e alunos SCORM
* para [DSRP](/help/communities/dsrp.md) : armazenamento de conteúdo gerado pelo usuário (UGC)

O conector MySQL deve ser obtido e instalado separadamente.

As etapas necessárias são:

1. faça download do arquivo ZIP em [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * deve ser >= 5.1.38

1. extraia mysql-Connector-java-&lt;version>-bin.jar (pacote) do arquivo
1. use o console da Web para instalar e start o pacote:

   * por exemplo, https://localhost:4502/system/console/bundles
   * select **`Install/Update`**
   * Procurar... para selecionar o pacote extraído do arquivo ZIP baixado
   * verifique se o* Driver JDBC da Oracle Corporation para MySQLcom.mysql.jdbc* está ativo e start-o se não estiver (ou verifique os registros)

1. se a instalação for feita em uma implantação existente depois que o JDBC tiver sido configurado, refaça o JDBC para o novo conector, salvando a configuração do JDBC do console da Web:

   * por exemplo, https://localhost:4502/system/console/configMgr
   * localizar `Day Commons JDBC Connections Pool` configuração
   * selecionar para abrir
   * select `Save`

1. Repita as etapas 3 e 4 em todas as instâncias de autor e publicação

Mais informações sobre a instalação de pacotes estão disponíveis na página Console [da](/help/sites-deploying/web-console.md#bundles) Web.

#### Exemplo: Pacote do Conector MySQL instalado {#example-installed-mysql-connector-bundle}

![](../assets/chlimage_1-125.png)

### Pacote SCORM {#scorm-package}

O Shareable Content Object Reference Model (SCORM) é uma coleção de padrões e especificações para e-learning. O SCORM também define como o conteúdo pode ser empacotado em um arquivo ZIP transferível.

O mecanismo AEM Communities SCORM é necessário para o recurso de [ativação](/help/communities/overview.md#enablement-community) . Pacotes de pontuação compatíveis com AEM 6.5 Comunidades:

* [cq-social-scorm-package, versão 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) que inclui o mecanismo [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) .

**Para instalar um pacote SCORM**

1. Instale o [cq-social-scorm-package, versão 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg)do Compartilhamento de pacotes
1. Baixe `/libs/social/config/scorm/database_scormengine_data.sql` da instância cq e execute-a no servidor mysql para criar um schema scormEngineDB atualizado.
1. Adicione `/content/communities/scorm/RecordResults` a propriedade Caminhos excluídos no filtro CSRF de `https://<hostname>:<port>/system/console/configMgr` em editores.

#### Registro SCORM {#scorm-logging}

Conforme instalado, toda a atividade de ativação é perfeitamente conectada ao console do sistema.

Se desejado, o nível de log pode ser definido como WARN para o `RusticiSoftware.*` pacote.

Para trabalhar com registros, consulte [Trabalhar com registros de auditoria e arquivos](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)de registro.

### AEM Advanced MLS {#aem-advanced-mls}

Para a coleção SRP (MSRP ou DSRP) suportar pesquisa multilíngue avançada (MLS), novos plug-ins Solr são necessários além de uma configuração personalizada de schema e Solr. Todos os itens necessários são empacotados em um arquivo zip baixável.

O download avançado do MLS (também conhecido como &#39;phasetwo&#39;) está disponível no repositório do Adobe :

* [AEM-SOLR-MLS-phasetwo](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * versão 1.2.40, 6 de abril de 2016
   * download AEM-SOLR-MLS-phasetwo-1.2.40.zip

Para obter detalhes e informações sobre instalação, consulte Configuração [](/help/communities/solr.md) solar para SRP.

### Sobre links para compartilhamento de pacotes {#about-links-to-package-share}

**Pacotes visíveis na Adobe AEM Cloud**

Os links para pacotes nesta página não exigem nenhuma instância em execução de AEM, pois estão para compartilhamento de pacotes `adobeaemcloud.com`. Enquanto os pacotes são visualizáveis, o `Install`botão é para instalar os pacotes em um site hospedado no Adobe. Se você pretende instalar em uma instância AEM local, a seleção `Install`resultará em um erro.

**Como instalar na instância AEM local**

Para instalar os pacotes visíveis `adobeaemcloud.com` em uma instância AEM local, o pacote deve ser baixado primeiro em um disco local:

* select the **Assets** tab
* selecionar **download para disco**

Na instância AEM local, use o gerenciador de pacote (por exemplo, [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)) para fazer upload para o repositório de pacote AEM local.

Como alternativa, ao acessar o pacote usando o compartilhamento de pacote da instância de AEM local (por exemplo, [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), o `Download`botão baixará para o repositório de pacote da instância AEM local.

Uma vez no repositório de pacotes da instância AEM local, use o gerenciador de pacotes para instalar o pacote.

Para obter mais informações, consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md#package-share).

## Implantações recomendadas {#recommended-deployments}

No AEM Communities, uma loja comum é usada para armazenar conteúdo gerado pelo usuário (UGC) e é geralmente chamada de provedor de recursos do [armazenamento (SRP)](/help/communities/working-with-srp.md). A implantação recomendada centra-se na escolha de uma opção SRP para a loja comum.

A loja comum oferece suporte à moderação e análise do UGC no ambiente de publicação, eliminando a necessidade de [replicação](/help/communities/sync.md) do UGC.

* [Repositório](/help/communities/working-with-srp.md) de conteúdo da comunidade: discute as opções de armazenamento SRP para comunidades AEM

* [Topologias](/help/communities/topologies.md) recomendadas: discute a topologia a ser usada, dependendo do caso de uso e da escolha do SRP

## Atualização {#upgrading}

Ao atualizar para a plataforma AEM 6.5 de versões anteriores do AEM, é importante ler [Atualização para AEM 6.5](/help/sites-deploying/upgrade.md).

Além de atualizar a plataforma, leia [Atualização para o AEM Communities 6.5](/help/communities/upgrade.md) para saber mais sobre as mudanças nas Comunidades.

## Configurações {#configurations}

### Editor principal {#primary-publisher}

Quando a implantação escolhida é um farm [de](/help/communities/topologies.md#tarmk-publish-farm)publicação, uma instância de publicação AEM deve ser identificada como **`primary publisher`** para atividades que não devem ocorrer em todas as instâncias, como recursos que dependem de **notificações **ou **Adobe Analytics**.

Por padrão, a configuração do `AEM Communities Publisher Configuration` OSGi é configurada com a **`Primary Publisher`** caixa de seleção marcada, de modo que todas as instâncias de publicação em um farm de publicação se autoidentificariam como a principal.

Portanto, é necessário **editar a configuração em todas as instâncias** de publicação secundárias para desmarcar a caixa de seleção **`Primary Publisher`** .

![](../assets/chlimage_1-126.png)

Para todas as outras instâncias de publicação (secundárias) em um farm de publicação:

* fazer logon com privilégios de administrador
* acessar o console [da Web](/help/sites-deploying/configuring-osgi.md)

   * por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* localize a variável `AEM Communities Publisher Configuration`
* selecione o ícone de edição
* desmarque a caixa Editor **** primário
* select **Save**

### Agentes de Replicação no Autor {#replication-agents-on-author}

A replicação é usada para o conteúdo do site criado no ambiente de publicação, como grupos da comunidade, bem como para gerenciar membros e grupos de membros do ambiente autor usando o serviço [de](#tunnel-service-on-author)túnel.

Para o editor principal, verifique se a Configuração [do Agente de](/help/sites-deploying/replication.md) Replicação identifica corretamente o servidor de publicação e o usuário autorizado. O usuário autorizado padrão `admin,` já tem as permissões apropriadas (é membro de `Communities Administrators`).

Para que outro usuário tenha as permissões apropriadas, ele deve ser adicionado como membro ao grupo de `administrators` usuários (também como membro do `Communities Administrators`).

Há dois agentes de replicação no ambiente do autor que precisam que a configuração de transporte seja configurada corretamente.

* acessar o console Replicação no autor

   * da navegação global : **Ferramentas, Implantação, Replicação, Agentes no autor**

* seguir o mesmo procedimento para ambos os agentes:

   * **Agente padrão (publicar)**
   * **Agente de Replicação Reversa (publicar reverso)**

      1. selecione o agente
      1. select **edit**
      1. select the **Transport** tab
      1. se não houver porta `4503`, edite o **URI** para especificar a porta correta

      1. se não for usuário `admin`, edite **Usuário** e **Senha** para especificar um membro do grupo de `administrators` usuários

As imagens a seguir mostram os resultados da alteração da porta de 4503 para 6103 por:

#### Agente padrão (publicar) {#default-agent-publish}

![configurar limites](../assets/configure-limits.png)

#### Agente de Replicação Reversa (publicar reverso) {#reverse-replication-agent-publish-reverse}

![](../assets/chlimage_1-128.png)

### Serviço de túnel no autor {#tunnel-service-on-author}

Ao usar o ambiente do autor para [criar sites](/help/communities/sites-console.md), [modificar as propriedades](/help/communities/sites-console.md#modifying-site-properties) do site ou [gerenciar membros](/help/communities/members.md)da comunidade, é necessário acessar os membros (usuários) registrados no ambiente de publicação, e não os usuários registrados no autor.

O serviço de túnel fornece esse acesso usando o agente de replicação do autor.

Para ativar o serviço de túnel:

* sobre o **autor**
* fazer logon com privilégios administrativos
* se o editor não for localhost:4503 ou o usuário de transporte não for `admin`, [configure o agente de replicação](#replication-agents-on-author)

* acessar o console [da Web](/help/sites-deploying/configuring-osgi.md)

   * por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* localize a variável `AEM Communities Publish Tunnel Service`
* selecione o ícone de edição
* marque a **caixa ativar **caixa
* select **Save**

![](../assets/chlimage_1-129.png)

### Replicar a chave de criptografia {#replicate-the-crypto-key}

Há dois recursos do AEM Communities que exigem que todas as instâncias do servidor AEM usem as mesmas chaves de criptografia. Esses são [Analytics](/help/communities/analytics.md) e [ASRP](/help/communities/asrp.md).

A partir do AEM 6.3, o material principal é armazenado no sistema de arquivos e não mais no repositório.

Para copiar o material principal do autor para todas as outras instâncias, é necessário:

* acesse a instância AEM, normalmente uma instância do autor, que contém o material principal a ser copiado

   * localize o `com.adobe.granite.crypto.file` pacote no sistema de arquivos local, por exemplo,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * o `bundle.info` arquivo identificará o pacote
   * navegue até a pasta de dados, por exemplo,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * copiar os arquivos hmac e do nó primário



* para cada instância AEM do público alvo

   * navegue até a pasta de dados, por exemplo,

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * colar os 2 arquivos copiados anteriormente
   * é necessário [atualizar o pacote](#refresh-the-granite-crypto-bundle) Granite Crypto se a instância AEM do público alvo estiver em execução no momento


>[!CAUTION]
>
>Se outro recurso de segurança já tiver sido configurado com base nas chaves criptografadas, a replicação das chaves criptografadas poderá danificar a configuração. Para obter ajuda, [entre em contato com o Atendimento](https://helpx.adobe.com/br/marketing-cloud/contact-support.html)ao cliente.

#### Replicação do repositório {#repository-replication}

Ter o material principal armazenado no repositório, como era o caso do AEM 6.2 e anterior, pode ser preservado especificando-se a seguinte propriedade do sistema na primeira inicialização de cada instância AEM (que cria o repositório inicial):

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>É importante verificar se o agente de [replicação do autor](#replication-agents-on-author) está configurado corretamente.

Com o material principal armazenado no repositório, a maneira de replicar a chave de criptografia do autor para outras instâncias é a seguinte:

Usando o [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* navegue até [https://&lt;servidor>:&lt;porta>/crx/de](https://localhost:4502/crx/de)
* select `/etc/key`
* abrir `Replication` guia
* select `Replicate`

* [atualizar o pacote Granite Crypto](#refresh-the-granite-crypto-bundle)

![](../assets/chlimage_1-130.png)

#### Atualizar o pacote Cripto Granite {#refresh-the-granite-crypto-bundle}

* em cada instância de publicação, acesse o Console [da Web](/help/sites-deploying/configuring-osgi.md)

   * por exemplo, [https://&lt;servidor>:&lt;porta>/system/console/bundles](https://localhost:4503/system/console/bundles)

* localizar `Adobe Granite Crypto Support` pacote (com.adobe.granite.crypto)
* selecionar **Atualizar**

![](../assets/chlimage_1-131.png)

* após um momento, uma **caixa de diálogo **Êxito **deve aparecer :
   `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

Se estiver usando o servidor HTTP Apache, certifique-se de usar o nome correto do servidor para todas as entradas relevantes.

Em particular, tenha cuidado para usar o nome correto do servidor, não `localhost`, no `RedirectMatch`.

#### httpd.conf exemplo {#httpd-conf-sample}

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

Se estiver usando um Dispatcher, consulte:

* Documentação [do Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) AEM
* [Instalação do Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [Configuração do Dispatcher para Comunidades](/help/communities/dispatcher.md)
* [Problemas conhecidos](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Documentação das Comunidades relacionadas {#related-communities-documentation}

* Visite [Administrando sites](/help/communities/administer-landing.md) de comunidades para saber mais sobre como criar um site da comunidade, configurar modelos de site da comunidade, moderar o conteúdo da comunidade, gerenciar membros e configurar mensagens.

* Visite Comunidades [em desenvolvimento](/help/communities/communities.md) para saber mais sobre a estrutura de componentes sociais (SCF) e como personalizar componentes e recursos das Comunidades.

* Visite Componentes [de comunidades de](/help/communities/author-communities.md) criação para saber como criar e configurar componentes de Comunidades.

