---
title: Implantação de comunidades
description: Saiba como implantar comunidades e recursos da comunidade no Adobe Experience Manager.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 5b3d572d-e73d-4626-b664-c985949469c9
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1658'
ht-degree: 0%

---

# Implantação de comunidades {#deploying-communities}

## Pré-requisitos {#prerequisites}

* [Plataforma AEM 6.5](/help/sites-deploying/deploy.md)

* Licença do AEM Communities

* Licenças opcionais para:

   * [Recursos do Adobe Analytics for Communities](/help/communities/analytics.md)
   * [MongoDB para MSRP](/help/communities/msrp.md)
   * [Adobe Cloud para ASRP](/help/communities/asrp.md)

## Lista de verificação de instalação {#installation-checklist}

**Para a [plataforma AEM](/help/sites-deploying/deploy.md#what-is-aem)**

* Instalar as [Atualizações do AEM 6.5](#aem64updates) mais recentes

* Se não estiver usando as portas padrão (4502, 4503), [configure os agentes de replicação](#replication-agents-on-author)
* [Replicar a chave de criptografia](#replicate-the-crypto-key)
* Se for compatível com a globalização, [configure a tradução automática](/help/sites-administering/translation.md)
(a configuração de exemplo é fornecida para desenvolvimento)

**Para o [recurso Comunidades](/help/communities/overview.md)**

* Se estiver implantando um [farm de publicação](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [identifique o publicador principal](#primary-publisher)

* [Habilitar o serviço de túnel](#tunnel-service-on-author)
* [Habilitar logon social](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Configurar Adobe Analytics](/help/communities/analytics.md)
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
      * [Selecionar DSRP](/help/communities/srp-config.md)

   * Se Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * Trabalhe com seu representante de conta para obter provisionamento
      * [Selecionar ASRP](/help/communities/srp-config.md)

   * Se JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * Não é um armazenamento UGC (Conteúdo Gerado pelo Usuário) compartilhado:

         * O UGC nunca é replicado
         * O UGC só é visível na instância ou cluster AEM em que foi inserido

         * O padrão é JSRP

## Versões mais recentes {#latest-releases}

O AEM 6.5 Communities GA inclui o pacote Communities. Para saber mais sobre atualizações no AEM 6.5 [Comunidades](/help/release-notes/release-notes.md#experiencemanagercommunities), consulte as [Notas de versão do AEM 6.5](/help/release-notes/release-notes.md#communities-release-notes.html).

### Atualizações do AEM 6.5 {#aem-updates}

A partir do AEM 6.4, as atualizações das Comunidades são fornecidas como parte do AEM Cumulative Fix Packs e Service Packs.

Para obter as atualizações mais recentes do AEM 6.5, consulte [Cumulative Fix Packs e Service Packs do Adobe Experience Manager 6.4](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates).

### Histórico da versão {#version-history}

Assim como no AEM 6.4 e posteriores, os recursos e hotfixes do AEM Communities fazem parte dos cumulative fix packs e service packs da AEM Communities. Portanto, não há pacotes de recursos separados.

### Driver JDBC para MySQL {#jdbc-driver-for-mysql}

O recurso One Communities usa um banco de dados MySQL:

* Para [DSRP](/help/communities/dsrp.md): armazenando UGC

O conector MySQL deve ser obtido e instalado separadamente.

As etapas necessárias são:

1. Baixe o arquivo ZIP de [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * A versão deve ser >= 5.1.38

1. Extraia mysql-connector-java-&lt;version>-bin.jar (pacote) do arquivo
1. Use o console da Web para instalar e iniciar o pacote:

   * Por exemplo, https://localhost:4502/system/console/bundles
   * Selecionar **`Install/Update`**
   * Procurar... para selecionar o pacote extraído do arquivo ZIP baixado
   * Verifique se o *Driver JDBC da Oracle Corporation para MySQLcom.mysql.jdbc* está ativo, caso contrário, inicie-o (ou verifique os logs)

1. Se estiver instalando em uma implantação existente após a configuração do JDBC, vincule novamente o JDBC ao novo conector, salvando novamente a configuração do JDBC no console da Web:
   * Por exemplo, https://localhost:4502/system/console/configMgr
   * Localizar configuração de `Day Commons JDBC Connections Pool`
   * Selecione para abrir
   * Selecionar `Save`

1. Repita as etapas 3 e 4 em todas as instâncias de autor e publicação

Mais informações sobre a instalação de pacotes estão disponíveis na página [Console da Web](/help/sites-deploying/web-console.md).

#### Exemplo: conjunto de conectores MySQL instalado {#example-installed-mysql-connector-bundle}

![conjunto de conectores](assets/connector-bundle.png)



### MLS avançado para AEM {#aem-advanced-mls}

Para que a coleção SRP (MSRP ou DSRP) seja compatível com a pesquisa multilíngue avançada (MLS), novos plug-ins Solr são necessários, além de um esquema personalizado e uma configuração Solr. Todos os itens necessários são empacotados em um arquivo zip para download.

O download avançado do MLS (também conhecido como `phasetwo`) está disponível no repositório Adobe:

* AEM-SOLR-MLS-phasetwo

  Para obter o pacote MLS Avançado, consulte [MLS Avançado do AEM](deploy-communities.md#aem-advanced-mls) na seção de implantação da documentação.

   * Versão 1.2.40, 6 de abril de 2016
   * Baixe o AEM-SOLR-MLS-phasetwo-1.2.40.zip

Para obter detalhes e informações sobre a instalação, visite [Configuração Solr](/help/communities/solr.md) para SRP.

### Sobre links para compartilhamento de pacotes {#about-links-to-package-share}

**Pacotes Visíveis na Nuvem do Adobe AEM**

Os links para pacotes nesta página não exigem instância em execução do AEM, pois são necessários para o Compartilhamento de Pacotes em `adobeaemcloud.com`. Enquanto os pacotes estiverem visíveis, o botão `Install` será usado para instalar os pacotes em um site hospedado em Adobe. Se você pretende instalar o em uma instância de AEM local, selecionar `Install` resultará em um erro.

**Como instalar em uma instância de AEM local**

Para instalar os pacotes visíveis em `adobeaemcloud.com` em uma instância de AEM local, o pacote deve primeiro ser baixado em um disco local:

* Selecione a guia **Assets**
* Selecione **baixar para disco**

Na instância local do AEM, use o Gerenciador de Pacotes (por exemplo, [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)) para carregar no repositório de pacotes locais do AEM.

Como alternativa, ao acessar o pacote usando o Compartilhamento de Pacotes da instância de AEM local (por exemplo, [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), o botão `Download` é baixado para o repositório de pacotes da instância de AEM local.

Quando estiver no repositório de pacotes da instância local do AEM, use o Gerenciador de pacotes para instalar o pacote.

Para obter mais informações, visite [Como trabalhar com pacotes](/help/sites-administering/package-manager.md#package-share).

## Implantações recomendadas {#recommended-deployments}

No AEM Communities, um armazenamento comum é usado para armazenar UGC e geralmente é chamado de [provedor de recursos de armazenamento (SRP)](/help/communities/working-with-srp.md). A implantação recomendada se concentra na escolha de uma opção SRP para o armazenamento comum.

O repositório comum oferece suporte à moderação e análise de UGC no ambiente de publicação, eliminando a necessidade de [replicação](/help/communities/sync.md) de UGC.

* [Repositório de Conteúdo da Comunidade](/help/communities/working-with-srp.md) : discute as opções de armazenamento SRP para o AEM Communities

* [Topologias Recomendadas](/help/communities/topologies.md) : discute a topologia a ser usada, dependendo do caso de uso e da escolha de SRP

## Atualizando {#upgrading}

Ao atualizar para a plataforma AEM 6.5 de versões anteriores do AEM, é importante ler [Atualização para o AEM 6.5](/help/sites-deploying/upgrade.md).

Além de atualizar a plataforma, leia [Atualização para o AEM Communities 6.5](/help/communities/upgrade.md) para saber mais sobre as alterações nas comunidades.

## Configurações {#configurations}

### Editor primário {#primary-publisher}

Quando a implantação escolhida é um [farm de publicação](/help/communities/topologies.md#tarmk-publish-farm), uma instância de publicação AEM deve ser identificada como **`primary publisher`** para atividades que não devem ocorrer em todas as instâncias. Por exemplo, recursos que dependem de **notificações** ou **Adobe Analytics**.

Por padrão, a configuração OSGi `AEM Communities Publisher Configuration` é configurada com a caixa de seleção **`Primary Publisher`** marcada, de modo que todas as instâncias de publicação em um farm de publicação se autoidentifiquem como primárias.

Portanto, é necessário **editar a configuração em todas as instâncias de publicação secundárias** para desmarcar a caixa de seleção **`Primary Publisher`**.

![editor-primário](assets/primary-publisher.png)

Para todas as outras instâncias de publicação (secundárias) em um farm de publicação:

* Entrar com privilégios de administrador
* Acessar o [console da Web](/help/sites-deploying/configuring-osgi.md)

   * Por exemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* Localizar o `AEM Communities Publisher Configuration`
* Selecione o ícone de edição
* Desmarque a caixa **Editor primário**
* Selecione **Salvar**

### Agentes de replicação no autor {#replication-agents-on-author}

A replicação é usada para o conteúdo do site criado no ambiente de publicação, como grupos da comunidade e gerenciamento de membros e grupos de membros do ambiente de criação usando o [serviço de túnel](#tunnel-service-on-author).

Para o publicador principal, verifique se a [Configuração do Agente de Replicação](/help/sites-deploying/replication.md) identifica corretamente o servidor de publicação e o usuário autorizado. O usuário autorizado padrão, `admin,`, já tem as permissões apropriadas (é membro de `Communities Administrators`).

Para que outro usuário tenha as permissões apropriadas, ele deve ser adicionado como membro do grupo de usuários `administrators` (também como membro de `Communities Administrators`).

Há dois agentes de replicação no ambiente de autor que precisam da configuração de transporte para serem configurados corretamente.

* Acessar o console Replicação no autor

   * Na navegação global, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]** > **[!UICONTROL Agentes no autor]**

* Siga o mesmo procedimento para ambos os agentes:

   * **Agente padrão (publicação)**
   * **Agente de Replicação Reversa (publicar reversa)**

      1. Selecione o agente
      1. Selecionar **editar**
      1. Selecione a guia **Transporte**
      1. Se não for a porta `4503`, edite o **URI** para especificar a porta correta

      1. Se não for usuário `admin`, edite o **Usuário** e a **Senha** para especificar um membro do grupo de usuários `administrators`

As imagens a seguir mostram os resultados da alteração da porta de 4503 para 6103 por:

#### Agente padrão (publicação) {#default-agent-publish}

![default-agent-publish](assets/default-agent-publish.png)

#### Reverter agente de replicação (publicar reverso) {#reverse-replication-agent-publish-reverse}

![agente-replicação-reversa](assets/reverse-replication-agent.png)

### Serviço de Túnel no Autor {#tunnel-service-on-author}

Ao usar o ambiente de criação para [criar sites](/help/communities/sites-console.md), [modificar propriedades do site](/help/communities/sites-console.md#modifying-site-properties) ou [gerenciar membros da comunidade](/help/communities/members.md), é necessário acessar membros (usuários) registrados no ambiente de publicação, não usuários registrados no autor.

O serviço de túnel fornece esse acesso usando o agente de replicação no autor.

Para habilitar o serviço de túnel:

* Faça logon com privilégios administrativos na instância do autor.
* Se o publicador não for localhost:4503 ou o usuário de transporte não for `admin`,
em seguida [configure o agente de replicação](#replication-agents-on-author)

* Acessar o [Console da Web](/help/sites-deploying/configuring-osgi.md)

   * Por exemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* Localizar o `AEM Communities Publish Tunnel Service`
* Selecione o ícone de edição
* Marque a caixa **habilitar**
* Selecione **Salvar**

  ![serviço-túnel](assets/tunnel-service.png)

### Replicar a chave de criptografia {#replicate-the-crypto-key}

Há dois recursos do AEM Communities que exigem que todas as instâncias do servidor AEM usem as mesmas chaves de criptografia. Estes são [Analytics](/help/communities/analytics.md) e [ASRP](/help/communities/asrp.md).

A partir do AEM 6.3, o material principal é armazenado no sistema de arquivos e não mais no repositório.

Para copiar o material principal do Autor para todas as outras instâncias, é necessário:

* Acesse a instância do AEM - normalmente uma instância do Autor - que contém o material principal a ser copiado

   * Localizar o pacote `com.adobe.granite.crypto.file` no sistema de arquivos local,
por exemplo,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * O arquivo `bundle.info` identifica o pacote

   * Navegue até a pasta de dados,
por exemplo,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * Copie os arquivos hmac e do nó primário

* Para cada instância de AEM de destino

   * Navegue até a pasta de dados,
por exemplo,

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

   * Cole os dois arquivos copiados anteriormente
   * É necessário [atualizar o pacote de Criptografia do Granite](#refresh-the-granite-crypto-bundle) se a instância do AEM de destino estiver em execução

>[!CAUTION]
>
>Se outro recurso de segurança já tiver sido configurado com base nas chaves de criptografia, a replicação dessas chaves poderá danificar a configuração. Para obter ajuda, [entre em contato com o atendimento ao cliente](https://experienceleague.adobe.com/pt-br?support-solution=General&amp;support-tab=home#support).

#### Replicação do repositório {#repository-replication}

Ter o material principal armazenado no repositório, como foi o caso do AEM 6.2 e anterior, pode ser preservado. Especifique a propriedade do sistema `-Dcom.adobe.granite.crypto.file.disable=true` na primeira inicialização de cada instância do AEM (que cria o repositório inicial).

>[!NOTE]
>
>Verifique se o [agente de replicação no Autor](#replication-agents-on-author) está configurado corretamente.

Com o material principal armazenado no repositório, a maneira de replicar a chave criptográfica do autor para outras instâncias é a seguinte:

Usando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Navegue até [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* Selecionar `/etc/key`
* Abrir guia `Replication`
* Selecionar `Replicate`

* [Atualizar o pacote de criptografia do Granite](#refresh-the-granite-crypto-bundle)

  ![replicare-repository](assets/replicare-repository.png)

#### Atualizar o pacote de criptografia do Granite {#refresh-the-granite-crypto-bundle}

* Em cada instância de publicação, acesse o [Console da Web](/help/sites-deploying/configuring-osgi.md)

   * Por exemplo, [https://&lt;servidor>:&lt;porta>/sistema/console/pacotes](https://localhost:4503/system/console/bundles)

* Localizar conjunto `Adobe Granite Crypto Support` (com.adobe.granite.crypto)
* Selecionar **Atualizar**

  ![granite-crypto](assets/granite-crypto.png)

* Depois de um momento, a caixa de diálogo **Êxito** deverá ser exibida:
  `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

Se estiver usando o servidor HTTP Apache, certifique-se de usar o nome correto do servidor para todas as entradas relevantes.

Em particular, tenha cuidado para usar o nome de servidor correto, não `localhost`, no `RedirectMatch`.

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

Se estiver usando uma Dispatcher, consulte:

* Documentação do AEM [Dispatcher](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates)
* [Instalação do Dispatcher](https://experienceleague.adobe.com/pt-br/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install)
* [Configuração do Dispatcher para comunidades](/help/communities/dispatcher.md)
* [Problemas conhecidos](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Documentação de comunidades relacionadas {#related-communities-documentation}

* Visite [Administrando sites de comunidades](/help/communities/administer-landing.md) para saber mais sobre como criar um site de comunidade, configurar modelos de site de comunidade, moderar o conteúdo da comunidade, gerenciar membros e configurar mensagens.

* Visite [Comunidades de Desenvolvimento](/help/communities/communities.md), onde você pode saber mais sobre a estrutura do componente social (SCF) e sobre como personalizar componentes e recursos das Comunidades.

* Visite [Criação de componentes das comunidades](/help/communities/author-communities.md), onde você pode aprender a criar e configurar componentes das comunidades.
