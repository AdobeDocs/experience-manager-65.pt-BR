---
title: Portais e portlets AEM
description: Saiba como configurar e administrar o AEM como um portal e como configurar e exibir conteúdo de AEM em um portlet.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: b5f3d3a6-39c0-4aa5-8562-3cc6fa2b9e46
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '6073'
ht-degree: 0%

---

# Portais e portlets AEM{#aem-portals-and-portlets}

Este documento descreve o seguinte:

* Arquitetura do portal AEM
* Administração e configuração do AEM como portal
* Usando o AEM como portal
* Instalação, configuração e exibição de conteúdo AEM em um portlet (por exemplo, um servidor Web)

## Arquitetura de portal do AEM {#aem-portal-architecture}

A arquitetura de portal AEM inclui definições de portais e portlets.

### O que é um portal? {#what-is-a-portal}

Um portal é um aplicativo da Web que fornece personalização, logon único, integração de conteúdo de diferentes fontes e hospeda a camada de apresentação dos sistemas de informações.

Você pode executar portlets compatíveis com JSR 286 no AEM. O componente de portlet permite incorporar um portlet na página. Consulte [Administrar o portlet de conteúdo do AEM](#administeringthecqcontentportlet).

### O que é um portlet? {#what-is-a-portlet}

Portlets são componentes da Web implantados em um container que geram conteúdo dinâmico. A interface do portlet é empacotada e implantada como um arquivo .war dentro de um contêiner de portlet. Se você estiver executando o AEM como um portal, precisará do arquivo .war do portlet para executá-lo.

Para configurar o conteúdo AEM para aparecer em um portal, consulte [Instalando, Configurando e Usando AEM em um portlet](#installingconfiguringandusingcqinaportlet).

### Director do portal AEM {#aem-portal-director}

>[!CAUTION]
>
>O AEM Portal Director está obsoleto a partir do AEM 6.4. Consulte [Recursos Preteridos e Removidos](https://helpx.adobe.com/br/experience-manager/6-4/release-notes/deprecated-removed-features.html).

## Administrar o portlet de conteúdo do AEM {#administering-the-aem-content-portlet}

O portlet de conteúdo AEM permite exibir conteúdo AEM em um portal. O portlet está disponível em `/crx-quickstart/opt/portal` e pode ser personalizado de várias maneiras. Por exemplo, você pode personalizar a manipulação de SSO/Autenticação implantando seu próprio serviço de autenticação, gerando as informações de autenticação necessárias para que o AEM substitua o comportamento padrão. Os plug-ins usam uma API definida que permite adicionar sua própria funcionalidade, criando o plug-in na API. O plug-in pode ser implantado no portlet em execução. Para funcionar corretamente, ela precisa de uma configuração do autor e da instância de publicação do AEM junto com o caminho do conteúdo para ser exibido na inicialização.

Algumas das configurações podem ser alteradas por meio das preferências do portlet e outras por meio das configurações do serviço OSGi. Você altera essas configurações usando arquivos de **configuração** ou o console da Web OSGi.

### Preferências de portlet {#portlet-preferences}

As preferências do portlet podem ser configuradas no momento da implantação no servidor do portal ou ao editar o arquivo **WEB-INF/portlet.xml** antes de implantar o aplicativo Web do portlet. Por padrão, o arquivo portlet.xml é exibido da seguinte maneira:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<portlet-app xmlns="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd /opt/SUNWps/dtd/portlet.xsd"
             version="1.0">
   <portlet>
      <portlet-name>RSSWeatherPortlet</portlet-name>
      <portlet-class>org.jboss.portlet.weather.WeatherPortlet</portlet-class>
      <init-param>
         <name>default_zipcode</name>
         <value>05673</value>
      </init-param>
      <init-param>
         <name>RSS_XSL</name>
         <value>/WEB-INF/Rss.xsl</value>
      </init-param>
      <init-param>
         <name>base_url</name>
         <value>https://xml.weather.yahoo.com/forecastrss?p=</value>
      </init-param>
      <expiration-cache>180</expiration-cache>
      <supports>
         <mime-type>text/html</mime-type>
         <portlet-mode>VIEW</portlet-mode>
         <portlet-mode>EDIT</portlet-mode>
      </supports>
      <portlet-info>
         <title>Weather Portlet</title>
      </portlet-info>
      <portlet-preferences>
         <preference>
            <name>expires</name>
            <value>180</value>
         </preference>
         <preference>
            <name>RssXml</name>
            <value>https://xml.weather.yahoo.com/forecastrss?p=33145</value>
            <read-only>false</read-only>
         </preference>
      </portlet-preferences>
   </portlet>
</portlet-app>
```

O portlet pode ser configurado com as seguintes preferências:

<table>
 <tbody>
  <tr>
   <td>startPath</td>
   <td><p>Esse é o caminho inicial do portlet: ele define o conteúdo que é exibido inicialmente.</p> <p><strong>Importante</strong>: se o portlet estiver configurado para conectar-se a instâncias de autor e publicação do AEM que estejam em execução em um caminho de contexto diferente de <strong> /</strong>, será necessário habilitar a opção forçar <strong>CQUrlInfo</strong> na configuração do Gerenciador de Biblioteca Html dessas instâncias AEM (por exemplo, via Felix Webconsole) ou a edição não funcionará e a caixa de diálogo de preferências não será exibida.</p> </td>
  </tr>
  <tr>
   <td>htmlSelector</td>
   <td>O seletor que é anexado a cada URL. Por padrão, este é o <strong>portlet</strong>. Portanto, todas as solicitações para páginas html usam urls terminando em <strong>.portlet.html.</strong> Isso permite o uso de scripts personalizados dentro do AEM para renderização de portlet.</td>
  </tr>
  <tr>
   <td>addCssToPortalHeader</td>
   <td><p>Por padrão, os arquivos css incluídos na página HTML do AEM são incluídos no portlet. Desativar essa opção exclui os arquivos css padrão.</p> <p>Se essa opção estiver ativada, os arquivos CSS são adicionados ao cabeçalho da página html ou incorporados à página html, dependendo do comportamento do portal.</p> </td>
  </tr>
  <tr>
   <td>includeToolbar</td>
   <td>Por padrão, uma barra de ferramentas é renderizada no portlet de conteúdo para a funcionalidade de gerenciamento. Ao desabilitar esta opção, nenhuma barra de ferramentas é renderizada.</td>
  </tr>
  <tr>
   <td>urlParameterNames</td>
   <td><p>Lista de nomes alternativos de parâmetros de URL que podem conter o novo URL de conteúdo para ser exibido no portlet. A lista é processada de cima para baixo; o primeiro parâmetro contendo um valor é usado. Se nenhum URL for encontrado, o parâmetro de URL padrão será usado. O URL fornecido é usado, como está, sem qualquer modificação adicional.</p> <p>Essa configuração é por portlet implantado - também é necessário definir globalmente alguns parâmetros de url na configuração OSGi para o "Day Portal Director Portlet Bridge".</p> </td>
  </tr>
  <tr>
   <td>preferredDialog</td>
   <td>Caminho para a caixa de diálogo de preferências no AEM - se permanecer vazia, a caixa de diálogo de preferências incorporada será usada. O padrão é /libs/portal/content/prefs.html.</td>
  </tr>
  <tr>
   <td>initialRedirect</td>
   <td>Por padrão, o portlet executa um redirecionamento de javascript de toda a página do portal na primeira invocação. Isso é para oferecer suporte ao cenário de arrastar e soltar de servidores de portal modernos. Na produção, esse redirecionamento raramente é necessário e, portanto, pode ser desativado com essa preferência sendo definida como <em>false</em>.</td>
  </tr>
 </tbody>
</table>

#### Console da Web OSGi {#osgi-web-console}

Supondo que o servidor do portal esteja em execução no host localhost, na porta 8080 e que o aplicativo Web portlet AEM esteja montado no contexto de aplicativo Web *cqportlet*, a URL do console da Web será `https://localhost:8080/cqportlet/cqbridge/system/console`. O usuário e a senha padrão é **admin**.

Abra a guia **Configurações** e selecione **Configuração do Servidor CQ do Diretório de Portal**. Aqui você especifica o URL base para o autor e a instância de publicação. Este procedimento está descrito em [Configurando o Portlet](#configuring-the-portlet).

>[!NOTE]
>
>O console da Web OSGi se destina apenas a alterar configurações durante o desenvolvimento (ou teste). Bloqueie solicitações no console para sistemas de produção.

### Fornecer configurações {#providing-configurations}

Para oferecer suporte a implantações automatizadas e provisionamento de configuração, o portlet de conteúdo AEM tem suporte de configuração integrado que tenta ler as configurações do classpath fornecido para o aplicativo do portlet.

Na inicialização, a propriedade do sistema **com.day.cq.portet.config** é lida para detectar o ambiente atual. Normalmente, o valor desta propriedade é algo como **dev**, **prod**, **test**, e assim por diante. Se nenhum ambiente estiver definido, nenhuma configuração será lida.

Se um ambiente for definido, um arquivo de configuração será pesquisado no classpath em ***com/day/cq/portlet/{env}.config**, onde **env** é substituído pelo valor real do ambiente. Esse arquivo deve listar todos os arquivos de configuração desse ambiente. Esses arquivos são pesquisados de acordo com o local do arquivo de configuração. Por exemplo, se o arquivo contiver uma linha `my.service.xml,`, este arquivo será lido do classpath em `com/day/cq/portlet/my.service.config.`. O nome do arquivo consiste na ID de persistência do serviço, seguida por **.config**. No exemplo anterior, a ID de persistência é **my.service**. O formato do arquivo de configuração é o formato usado pelo instalador do OSGi do Apache Sling.

Isso significa que, para cada ambiente, um arquivo de configuração correspondente precisa ser adicionado. Uma configuração que deve ser aplicada a todos os ambientes precisa ser inserida em todos esses arquivos. Se for apenas para um único ambiente, ela será inserida nesse arquivo. Esse mecanismo garante o controle total sobre qual configuração é lida em qual ambiente.

É possível usar uma propriedade do sistema diferente para detectar o ambiente. Especifique a propriedade do sistema **com.day.cq.portet.configproperty** que contém o nome da propriedade do sistema a ser usada em vez de **com.day.cq.portet.config**.

#### Armazenamento em cache e invalidação de armazenamento em cache {#caching-and-caching-invalidation}

O portlet, em sua configuração padrão, armazena em cache as respostas recebidas do AEM WCM em um cache específico do usuário. Os caches precisam ser invalidados quando ocorrerem alterações no conteúdo da instância de publicação. Para essa finalidade, no WCM do AEM, um agente de replicação deve ser configurado na instância do autor. O cache também pode ser liberado manualmente. Esta seção descreve ambos os procedimentos.

O portlet pode ser configurado com seu próprio cache, de modo que o conteúdo no portlet seja exibido sem a necessidade de acesso ao AEM. O portal está disponível como conteúdo em /libs/portal/diretor. Para acessar o conteúdo, inicie uma instância do AEM e baixe, usando o CRXDE Lite ou o Webdav, o arquivo desse local.

Você pode implantar este pacote em tempo de execução ou adicioná-lo ao aplicativo Web do portlet em `WEB-INF/lib/resources/bundles` antes da implantação.

Depois que o cache é implantado, o portlet armazena em cache o conteúdo da instância de publicação. O cache do portlet pode ser invalidado com uma liberação do dispatcher do AEM. Para configurar o portlet para usar seu próprio cache:

1. Configure um agente de replicação no autor que se destina ao servidor do portal.
1. Supondo que o servidor do portal esteja em execução no host **localhost**, **porta 8080 &#x200B;** e o aplicativo Web do portlet AEM esteja montado no contexto **cqportlet**, a URL para liberar o cache é `https://localhost:8080/cqportlet/cqbridge/cqpcache?Path=$(path)`. Use GET como método.
   **Observação:** Em vez de usar um parâmetro de solicitação, você pode enviar um cabeçalho http chamado **Caminho**.

#### Liberando o cache pelo Agente de Replicação {#flushing-the-cache-via-replication-agent}

Assim como na invalidação normal do dispatcher, um agente de replicação pode ser configurado para direcionar o cache do portlet AEM do portal. Após configurar o agente de replicação, cada ativação de página regular libera o cache do portal.

Se você operar vários nós de portal executando o portlet AEM, será necessário criar um agente para cada nó, conforme descrito neste procedimento.

Para configurar um agente de replicação para o portal:

1. Faça logon na instância do autor.
1. Na guia Sites, clique na guia *Ferramentas*.
1. Clique em **Nova página...** no menu **Nova...** dos agentes de replicação.

   ![screen_shot_2012-02-15at40647pm](assets/screen_shot_2012-02-15at40647pm.png)

1. Em *Modelo*, selecione *Agente de Replicação* e digite um nome para o agente. Clique em *Criar*.

   ![screen_shot_2012-02-15at40817pm](assets/screen_shot_2012-02-15at40817pm.png)

1. Clique duas vezes no agente de replicação criado. É exibido como inválido, pois ainda não foi configurado.

   ![screen_shot_2012-02-15at41001pm](assets/screen_shot_2012-02-15at41001pm.png)

1. Clique em **Editar.**
1. Na guia **Configurações**, marque a caixa de seleção **Habilitadas**, selecione **Liberação do Dispatcher** como o tipo de serialização e insira um tempo limite de repetição (por exemplo, 60000).

   ![screen_shot_2012-02-15at42101pm](assets/screen_shot_2012-02-15at42101pm.png)

1. Clique na guia **Transporte**.
1. No campo **URI**, digite o URI (URL) de liberação do portlet. O URI está no seguinte formato:

   ```xml
   https://<wps-host>:<port>/<wps-context>/<cq5-portlet-context>/cqbridge/cqpcache
   ```

   ![screen_shot_2012-02-15at42322pm](assets/screen_shot_2012-02-15at42322pm.png)

1. Clique na guia **Extended**.

   ![screen_shot_2012-02-15at42515pm](assets/screen_shot_2012-02-15at42515pm.png)

1. No campo **Método HTTP**, digite **GET**.
1. No campo **HTTP Headers**, clique em **+** para adicionar uma nova entrada e digite **Path: {path}**.
1. Se necessário, clique na guia **Proxy** e insira informações de proxy para o agente.
1. Clique em **OK** para salvar as alterações.
1. Para testar a conexão, clique no link **Testar Conexão**. Uma mensagem de log é exibida indicando se o teste de replicação foi bem-sucedido. Por exemplo:

   ![screen_shot_2012-02-15at42639pm](assets/screen_shot_2012-02-15at42639pm.png)

#### Liberando manualmente o cache do portlet {#manually-flushing-the-portlet-cache}

Você pode liberar manualmente o cache do portlet acessando o mesmo URL configurado para o agente de replicação. Consulte [Liberando o Cache](#flushing-the-cache-via-replication-agent) para obter o formulário da URL. Além disso, o URL precisa ser estendido com um parâmetro de URL Path=&lt;path> para indicar o que deve ser liberado.

Por exemplo:

`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=*` libera todo o cache. `https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=/content/mypage/xyz` libera `/content/mypage/xyz` do cache.

### Segurança do portal {#portal-security}

O portal é o mecanismo de autenticação responsável. Você pode fazer logon no AEM com um usuário técnico, o usuário do portal, um grupo e assim por diante. O portlet não tem acesso à senha do usuário no portal. Portanto, se o portlet não souber todas as credenciais para fazer logon com êxito em um usuário, uma solução SSO deverá ser usada. Nesse caso, o portlet AEM encaminha todas as informações necessárias para o AEM, que, por sua vez, encaminha essas informações para o repositório subjacente do AEM. Esse comportamento pode ser conectado e personalizado.

### Autenticação no Publish {#authentication-on-publish}

Esta seção descreve os modos de autenticação disponíveis que o portlet pode usar na comunicação com as instâncias WCM AEM subjacentes.

Por padrão, nenhuma informação do usuário é enviada para a instância de publicação do AEM; o conteúdo é sempre exibido como o usuário anônimo. Se informações específicas do usuário devem ser entregues por AEM ou se a autenticação do usuário para publicação for necessária, isso deve ser ativado.

#### Acessando a configuração de autenticação do portlet {#accessing-the-portlet-s-authentication-configuration}

As opções de configuração de autenticação que o portlet usa nas instâncias WCM do AEM estão disponíveis no console da Web (configuração OSGi).

>[!NOTE]
>
>Ao trabalhar com o AEM, há vários métodos de gerenciamento das definições de configuração para serviços OSGi (nós do console ou do repositório).
>
>Consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos.

Para acessar a configuração de autenticação do portlet:

1. Acesse o console da Web no seguinte URL:

   `https://localhost:8080/cqportlet/cqbridge/system/console`

   Por exemplo, em sua configuração padrão:

   `https://wps-host:10040/wps/PA_CQ5_Portlet/cqbridge/system/console`

1. Faça logon no console da Web. As credenciais padrão são `admin/admin`.
1. No console, selecione **Configuração**.
1. No menu **Configuração**, selecione um serviço específico a ser configurado. Os serviços são fornecidos pelo portlet na estrutura OSGi.

   | Nome do serviço | Descrição |
   |---|---|
   | Autenticador do Director do portal do dia | Configure qual modo de autenticação é usado para instâncias WCM AEM. Dependendo do modo selecionado, um usuário técnico ou o nome do cookie SSO podem ser especificados. Além disso, a autenticação para instâncias de publicação do WCM no AEM pode ser ativada. |
   | Cache de Arquivos do Director do Portal Diário | Configure os parâmetros de como o portlet armazena em cache as respostas que recebe das instâncias WCM do AEM. |
   | Serviço de Cliente HTTP Director do Portal do Dia | Configure como o portlet se conecta via HTTP a instâncias WCM AEM subjacentes. Você pode, por exemplo, especificar um servidor proxy. |
   | Manipulador local do Director do portal do dia | Configure as localidades suportadas pelo portlet. As solicitações para instâncias AEM WCM são baseadas na localidade do usuário; por exemplo, o idioma do usuário *Alemão *solicitaria `/content/geometrixx/de/`.... |
   | Gerenciador de Privilégios do Director do Portal do Dia | Configure se o portlet deve testar a guia Sites com base no usuário conectado no momento. |
   | Renderizador da barra de ferramentas do Director do portal diário | Personalize a renderização da barra de ferramentas do portlet. |

1. Além disso, você pode configurar o console da Web e o serviço de log. Por exemplo, você pode alterar as credenciais de administrador do console da Web clicando no link Console de gerenciamento do Apache Felix OSGi.

#### Modo de usuário técnico {#technical-user-mode}

No modo padrão, todas as solicitações emitidas pelo portlet para a instância do autor do WCM no AEM são autenticadas usando o mesmo usuário técnico, independentemente do usuário atual do portal. O modo Usuário técnico é ativado por padrão. Você ativa/desativa esse modo na respectiva tela de configuração no console de gerenciamento OSGi:

O usuário técnico especificado deve existir na instância de autor do WCM AEM e na instância de publicação se a **Autenticar no Publish** estiver habilitada. Conceda ao usuário privilégios de acesso suficientes para o trabalho de criação.

#### SSO {#sso}

O portlet suporta SSO com AEM pronto para uso. O serviço autenticador pode ser configurado para usar o SSO e transmitir o usuário atual do portal com o formato **Básico** como um cookie chamado `cqpsso` para AEM. O AEM deve ser configurado para usar o manipulador de autenticação SSO para o caminho /. O nome do cookie também precisa ser configurado aqui.

O repositório do `crx-quickstart/repository/repository.xml` for AEM precisa ser configurado adequadamente:

```xml
<LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
  ...
  <param name="trust_credentials_attribute" value="TrustedInfo"/>
  <param name="anonymous_principal" value="anonymous"/>
</LoginModule>
```

#### Modo de Autenticação SSO {#sso-authentication-mode}

O portlet pode autenticar para o WCM do AEM usando o esquema de Logon único (SSO). Nesse modo, o usuário conectado no momento ao portal é encaminhado ao WCM do AEM na forma de um cookie SSO. Se o modo SSO for usado, todos os usuários do portal com acesso ao portlet AEM deverão ser conhecidos pelas instâncias subjacentes do WCM AEM, mais comumente na forma de WCM AEM conectado ao LDAP ou por ter criado os usuários manualmente com antecedência. Além disso, antes de habilitar o SSO no portlet, a instância subjacente do autor do WCM do AEM (e a instância de publicação, se a opção **Autenticar no Publish** estiver habilitada) precisará ser configurada para aceitar solicitações baseadas em SSO.

Para configurar o portlet para usar o modo de autenticação SSO, conclua as seguintes etapas (descritas detalhadamente nas seções a seguir):

* Habilite o repositório do WCM do AEM para aceitar credenciais confiáveis.
* Ative a autenticação SSO no WCM do AEM.
* Ative a autenticação SSO no portlet AEM.

#### Ativação do repositório WCM do AEM para aceitar credenciais confiáveis {#enabling-aem-wcm-s-repository-to-accept-trusted-credentials}

Antes que o SSO possa ser ativado para o WCM do AEM, o repositório subjacente precisa ser configurado para aceitar as credenciais confiáveis fornecidas pelo WCM do AEM. Para fazer isso, configure AEM repository.xml.

1. No sistema de arquivos em que o AEM WCM está instalado, abra o seguinte arquivo:

   `//crx-quickstart/repository/repository.xml`

1. No arquivo XML, localize a entrada para o **LoginModule** e adicione o trust_credentials_attribute à sua configuração:

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
     <param name="anonymous_principal" value="anonymous"/>
   </LoginModule>
   ```

1. Reinicie o AEM WCM para que as alterações entrem em vigor.

#### Ativação da autenticação SSO no WCM do AEM {#enabling-sso-authentication-in-the-aem-wcm}

Para ativar o SSO no WCM do AEM, acesse a entrada de configuração relevante no Apache Felix Web Management Console (OSGi) do AEM WCM:

1. Acesse o console por meio do URI em https://&lt;AEM-host>:&lt;port>/system/console.
1. No menu Configuração, selecione Manipulador de autenticação SSO. Neste exemplo, o manipulador de SSO aceita solicitações de SSO para todos os caminhos com base no cookie fornecido pelo portlet AEM. Sua configuração pode variar.

   | Caminho | / | Habilita o manipulador SSO para todas as solicitações |
   |---|---|---|
   | Nomes de cookies | cqpsso | Nome do cookie fornecido pelo portlet conforme configurado no console OSGi do portlet. |

1. Clique em **Salvar** para habilitar o SSO. O SSO agora é o esquema de autenticação principal.

Para cada solicitação recebida pelo AEM WCM, primeiro tenta-se a autenticação baseada em SSO. Na falha, é realizado um fallback para o esquema de autenticação básico usual. Dessa forma, as conexões normais com o AEM WCM sem SSO permanecem possíveis.

#### Ativação da autenticação SSO em um portlet AEM {#enabling-sso-authentication-in-a-aem-portlet}

Para que a instância subjacente do WCM AEM aceite solicitações SSO, o modo de autenticação do portlet deve ser alternado de **Technical** para **SSO**.

Para habilitar a autenticação SSO em um portlet AEM:

1. Acesse o console por meio do URI em https://&lt;aem-host>:&lt;port>/system/console.
1. No menu Configuração, selecione Day Portal Director Authenticator na lista de configurações disponíveis.
1. Em Modo, selecione SSO. Deixe os outros parâmetros com seus valores padrão.

   ![chlimage_1-135](assets/chlimage_1-135.png)

1. Clique em Salvar para ativar o SSO para o portlet.

   Para fins de teste, acesse o portlet com o usuário administrativo do portal depois de criar o mesmo usuário no WCM do AEM com privilégios de administrador.

Após executar esse procedimento, as solicitações são autenticadas usando o SSO. Um trecho típico da comunicação HTTP revela a presença dos seguintes cabeçalhos específicos de SSO e Portlet:

```xml
C-12-#001898 -> [GET /mynet/en/_jcr_content/par/textimage/image.img.png HTTP/1.1 ]
C-12-#001963 -> [cq5:locale: en ]
C-12-#001979 -> [cq5:used-locale: en ]
C-12-#002000 -> [cq5:locales: en,en_US ]
C-12-#002023 -> [cqp:user: wpadmin ]
C-12-#002042 -> [cqp:portal: IBM WebSphere Portal/6.1 ]
C-12-#002080 -> [cqp:windowid: 7_CGAH47L000CE302V2KFNOG0084 ]
C-12-#002124 -> [cqp:windowstate: normal ]
C-12-#002149 -> [cqp:portletmode: view ]
C-12-#002172 -> [User-Agent: Jakarta Commons-HttpClient/3.1 ]
C-12-#002216 -> [Host: 10.0.0.68:4502 ]
C-12-#002238 -> [Cookie: $Version=0; cqpsso=Basic+d3BhZG1pbg%3D%3D ]
C-12-#002289 -> [ ]
```

### Habilitando autenticação do PIN {#enabling-pin-authentication}

Se você não estiver usando os recursos de edição em linha padrão do portlet de conteúdo AEM, mas quiser a parte de criação e administração do portlet fora do portal diretamente na instância de autor AEM, habilite a autenticação PIN. Você também precisa alterar a configuração dos botões de gerenciamento.

Para abrir a página de administração do site ou editar uma página do portlet, o portlet de conteúdo AEM usa a nova autenticação de pin. Por padrão, a autenticação de pin está desabilitada, portanto, as seguintes alterações de configuração devem ser feitas no AEM:

1. Ative a autenticação confiável no AEM adicionando as informações confiáveis no arquivo repository.xml:

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
   </LoginModule>
   ```

1. No console de configuração OSGi, por padrão localizado em https://localhost:4502/system/console/configMgr, selecione **Manipulador de autenticação do PIN CQ** no menu suspenso.
1. Edite o parâmetro **Caminho Raiz da URL** para conter apenas o valor único **/**.

### Privilégios {#privileges}

Algumas funções do portlet são protegidas por privilégios. O usuário atual precisa ter esse privilégio para acessar esta função. Há os seguintes privilégios predefinidos:

* &quot;toolbar&quot; : este é o privilégio geral para ver/usar a barra de ferramentas no portlet.
* &quot;prefs&quot; : se o usuário tiver esse privilégio, ele poderá ver/alterar as preferências do portlet.
* &quot;cq-author:edit&quot; : com esse privilégio, o usuário pode chamar a exibição de edição do conteúdo.
* &quot;cq-author:preview&quot; : Com esse privilégio, o usuário pode ver a visualização.
* &quot;cq-author:siteadmin&quot; : com esse privilégio, o usuário pode abrir o siteadmin no AEM.

A melhor abordagem para gerenciar os privilégios é usar funções de portal e atribuir funções a esses privilégios. Isso pode ser feito por meio de uma configuração OSGi. O &quot;Gerenciador de privilégios do Director do portal diário&quot; pode ser configurado com um conjunto de funções para cada privilégio. Se o usuário tiver uma das atribuições, ele terá o privilégio correspondente.

Além disso, é possível definir esse acesso baseado em função em uma base de instância por portlet. A caixa de diálogo de preferências do portlet contém um campo de entrada para cada um dos privilégios acima. Para cada privilégio, uma lista separada por vírgulas de funções de portlet pode ser configurada. Se um valor for configurado, isso substituirá a configuração global do serviço &quot;Gerenciador de privilégios do Director do portal diário&quot; e poderá ser necessário adicionar as mesmas funções dessa configuração global, pois as funções não são mescladas! Se nenhum valor for especificado, a configuração global será usada.

### Personalização do aplicativo portlet AEM {#customizing-the-aem-portlet-application}

O aplicativo de portlet AEM fornecido inicia um contêiner OSGi dentro do aplicativo da Web da mesma forma que o AEM. Essa arquitetura permite usar todos os benefícios do OSGi:

* Fácil de atualizar e estender
* Fornece atualizações do portlet sem nenhuma interação do servidor do portal
* Fácil de personalizar o portlet

### Botões da barra de ferramentas {#toolbar-buttons}

A barra de ferramentas e seus botões são configuráveis e podem ser personalizados. Você pode adicionar seus próprios botões à barra de ferramentas ou definir quais botões são exibidos em qual modo. Cada botão é um serviço OSGi configurável por meio de uma configuração OSGi.

O console da Web OSGi lista todas as configurações de botão na guia **Configuração**. Para cada botão, você pode definir em qual modo esse botão é exibido. Isso permite desabilitar um botão removendo todos os modos, por exemplo.

Por padrão, o portlet de conteúdo AEM usa a funcionalidade de edição em linha. No entanto, se você preferir alternar para a instância de autor AEM para edição, habilite o **Botão SiteAdmin** e o **Botão ContentFinder**, mas desabilite o **Botão Editar**. Nesse caso, configure corretamente a autenticação do PIN no AEM.

O layout da barra de ferramentas do portlet pode ser personalizado por meio da instalação de um pacote através do Felix Web Console do portlet, que contém CSS/HTML personalizado em um local predefinido.

#### Estrutura do pacote {#bundle-structure}

Este é um exemplo de estrutura de pacote:

```xml
$ jar tvf target/toolbarlayout-0.0.1-SNAPSHOT.jar | awk '{print $8}'
META-INF/
META-INF/MANIFEST.MF
/com/day/cq/portlet/toolbar/layout/
/com/day/cq/portlet/toolbar/layout/author.gif
/com/day/cq/portlet/toolbar/layout/back.gif
/com/day/cq/portlet/toolbar/layout/button.html
/com/day/cq/portlet/toolbar/layout/edit.gif
/com/day/cq/portlet/toolbar/layout/manage.html
/com/day/cq/portlet/toolbar/layout/publish.html
/com/day/cq/portlet/toolbar/layout/refresh.gif
/com/day/cq/portlet/toolbar/layout/siteadmin.gif
/com/day/cq/portlet/toolbar/layout/toolbar.css
```

A pasta META-INF contém o arquivo MANIFEST.MF exigido pelo OSGi para identificá-lo como um pacote. Ela aparece da seguinte forma:

```xml
Manifest-Version: 1.0
Built-By: djaeggi
Created-By: Apache Maven Bundle Plugin
Import-Package: com.day.cq.portlet.toolbar.layout
Bnd-LastModified: 1234178347159
Export-Package: com.day.cq.portlet.toolbar.layout
Bundle-Version: 0.0.1.SNAPSHOT
Bundle-Name: Company CQ5 Portal Director Portlet Toolbar Layout
Bundle-Description: This bundle provides a custom layout for the CQ5 P
 ortal Director Portlet Toolbar.
Build-Jdk: 1.5.0_16
Bundle-ManifestVersion: 2
Bundle-SymbolicName: com.day.cq.portlet.company.toolbarlayout
Tool: Bnd-0.0.255
```

O fato de que o HTML/CSS/images está na pasta /com/day/cq/portlet/toolbar/layout é obrigatório pelo portlet e não pode ser alterado. Na mesma linha, os cabeçalhos Import-Package e Export-Package no MANIFEST.MF também devem ser chamados de /com/day/cq/portlet/toolbar/layout. Bundle-SymbolicName deve ser um nome de pacote exclusivo e totalmente qualificado.

Você pode criá-lo usando uma ferramenta, como o maven, ou criar manualmente esse arquivo jar com o conjunto de cabeçalhos relevante, conforme mostrado nesta seção.

#### Exibições da barra de ferramentas do portlet {#portlet-toolbar-views}

A barra de ferramentas do portlet tem basicamente dois estados de visualização. Cada visualização e botões associados podem ser personalizados com um respectivo arquivo HTML.

#### Visualização do Publish {#publish-view}

A exibição de publicação tem apenas um botão que alterna a barra de ferramentas para a exibição Gerenciar. A exibição de publicação é representada pelo arquivo publish.html no [pacote anterior](/help/sites-deploying/configuring-osgi.md#bundles). No HTML, é possível usar os seguintes espaços reservados, que são substituídos pelo portlet com o respectivo conteúdo quando renderizados:

#### Espaços Reservados para Exibição do Publish {#publish-view-placeholders}

| String de espaço reservado | Descrição |
|---|---|
| {buttonManage} | O espaço reservado é substituído pelo botão **Gerenciar**, que alterna o estado do portlet para o estado de gerenciamento. |

#### Gerenciar exibição {#manage-view}

A exibição de gerenciamento tem quatro botões: Edit, Websites tab, Refresh e Back. A exibição manage é representada pelo arquivo manage.html no [pacote anterior](/help/sites-deploying/configuring-osgi.md#bundles). No HTML, é possível usar os seguintes espaços reservados, que são substituídos pelo portlet com o respectivo conteúdo quando renderizados:

#### Gerenciar marcadores de posição de exibição {#manage-view-placeholders}

| String de espaço reservado | Descrição |
|---|---|
| {buttonEdit} | O espaço reservado é substituído pelo botão **Editar**, que abre uma nova janela com a página atual no modo de edição do AEM. |
| {buttonWebsites tab} | Espaço reservado, substituído por um botão que abre a guia Sites do WCM do AEM. |
| {buttonRefresh} | Atualiza a exibição atual. |
| {buttonBack} | Alterna o portlet de volta para a visualização de publicação. |

#### Botões {#buttons}

Os botões, seja qual for a exibição exibida, usam o mesmo HTML comum, definido em button.html.

No HTML, é possível usar os seguintes espaços reservados, que são substituídos pelo portlet com o respectivo conteúdo quando renderizados:

#### Botões de exibição Gerenciar e Publish {#manage-and-publish-view-buttons}

| String de espaço reservado | Descrição |
|---|---|
| {name} | Nome do botão, por exemplo,**autor, voltar, atualizar** e assim por diante. |
| {id} | ID CSS do botão. |
| {url} | URL do destino do botão. |
| {text} | Etiqueta do botão. |
| {onclick} | Função **onclick** do JavaScript (contém {url}). |

Exemplo de um arquivo button.html:

```xml
<div class="cqp_button">

 <a href="#" onclick="{onclick}">

 <img src="/wps/PA_CQ5_Portlet/cqbridge/static/{id}.gif" alt="{text}"
title="{text}"/>

 </a>
</div>
```

#### Instalar um layout personalizado {#installing-a-custom-layout}

Para instalar um layout personalizado, acesse a seção **Pacotes** do console OSGI da Web do portlet e faça upload do pacote.

#### Pacotes {#packages}

Se precisar fazer upload ou criar pacotes para a instalação, consulte Gerenciador de pacotes na documentação do AEM para obter instruções detalhadas.

### Tratamento de links {#link-handling}

Todos os links são reescritos para funcionar no contexto do portal. Por padrão, os links com parâmetros de renderização são usados. Em vez disso, o Reescritor de HTML do Portal Director pode ser configurado para usar links de ação.

Você também pode definir parâmetros de solicitação adicionais a serem consultados para o caminho do conteúdo a ser exibido. Isso é útil, por exemplo, se houver um link externo para um conteúdo específico.

Além disso, o Rewriter de HTML do Portal Director pode ser configurado com uma lista de exclusões definidas de expressões regulares para a reescrita de links. Por exemplo, se você tiver links relativos para sistemas externos, deverá adicioná-los a essa lista de exclusão.

### Localização {#localization}

O portlet de conteúdo AEM tem um recurso de localização integrado, que garante que o conteúdo do AEM esteja no idioma correto.

Isso é feito em duas etapas:

1. O Detector de Localidade do Diretório de Portal detecta a localidade do usuário do portal obtendo a configuração de localidade do portal. Esse serviço deve ser configurado com a lista de idiomas disponíveis no AEM.
1. O Manipulador de localidade do Director do Portal lida com a localização da solicitação atual. Pega o caminho do conteúdo solicitado, por exemplo, `/content/geometrixx/en/company.html` e, de acordo com a configuração, substitui o **en** pela localidade real do usuário.

O Manipulador de localidade do Director do Portal pode ser configurado com os caminhos para verificar informações de localidade - geralmente isso inclui tudo em `/content` e com a posição das informações de localidade no caminho. Por padrão, o manipulador de local segue a recomendação de estruturar sites multilíngues no AEM.

Se o site não tiver uma regra estrita para manipular as informações de local no caminho, será possível substituir o manipulador de local pela sua própria implementação.

### Serviços OSGi opcionais {#optional-osgi-services}

Os serviços OSGi opcionais podem ser implementados para personalizar várias partes do portlet. Cada serviço corresponde a uma interface Java. Essa interface pode ser implementada e implantada por meio de um pacote no portlet.

<table>
 <tbody>
  <tr>
   <td>RequestTracker</td>
   <td>O rastreador de solicitações é notificado sempre que o conteúdo é exibido pelo portlet. Isso permite que você acompanhe as invocações do portlet.</td>
  </tr>
  <tr>
   <td>InvocationContextListener</td>
   <td>Ouvinte chamado no início e no fim de cada solicitação para o portlet. O ouvinte pode ser usado para alterar ou adicionar informações para a solicitação atual.<br /> </td>
  </tr>
  <tr>
   <td>ErrorHandler</td>
   <td>Manipulador de erros personalizado para erros durante a fase de renderização.</td>
  </tr>
  <tr>
   <td>ProcessadorHttp</td>
   <td>Esse serviço pode ser usado para adicionar informações a cada invocação http ao AEM.</td>
  </tr>
  <tr>
   <td>PortletAction</td>
   <td>Adicione uma própria ação ao portlet - essa ação pode ser chamada por meio de um link de ação do portlet.</td>
  </tr>
  <tr>
   <td>PortletDecoratorService</td>
   <td>Esse serviço pode ser usado para decorar o conteúdo do portlet.</td>
  </tr>
  <tr>
   <td>ProvedorDoRecurso</td>
   <td>Adicione seu próprio provedor de recursos para entregar algum recurso ao cliente por meio de um link de recurso do portlet.</td>
  </tr>
  <tr>
   <td>TextMapper</td>
   <td>Permite publicar arquivos de HTML, CSS e JavaScript de processo.</td>
  </tr>
  <tr>
   <td>ToolbarButton</td>
   <td>Adicione seu próprio botão à barra de ferramentas.</td>
  </tr>
  <tr>
   <td>UrlMapper</td>
   <td>Adicione um serviço para aplicar um mapeamento ou regravação de url personalizado.</td>
  </tr>
  <tr>
   <td>UserInfoProvider</td>
   <td>Adicione suas próprias informações sobre o usuário. Esse serviço pode ser usado para obter informações do portal para o portlet.</td>
  </tr>
 </tbody>
</table>

#### Substituição de serviços padrão {#replacing-default-services}

Os serviços a seguir têm uma implementação padrão no portlet de conteúdo (com uma interface Java correspondente). Para personalizar, um pacote contendo a nova implementação do serviço precisa ser implantado no aplicativo do portlet.

Ao implementar esse serviço, defina a propriedade **service.ranking** do serviço com um valor positivo. A implementação padrão usa a classificação **&#x200B; 0** e o portlet usa o serviço com a classificação mais alta.

| **Nome** | **Descrição** | **Comportamento padrão** |
|---|---|---|
| Autenticador | Fornece as informações de autenticação para AEM | Usa um usuário técnico configurável para criar e publicar. Ou SSO pode ser usado. |
| HTMLRewriter | Substitui links e imagens | Substitui links AEM para links de portal, pode ser estendido por um UrlMapper e um TextMapper |
| HttpClientService | Gerencia todas as conexões http | Implementação padrão |
| LocaleHandler | Gerencia as informações de local | Substitui um link para o conteúdo em relação ao local. |
| LocaleDetector | Detecta a localidade do usuário. | Usa o local fornecido pelo portal. |
| PrivilegeManager | Verifica os direitos do usuário | Verifica o acesso à instância do autor se o usuário tiver permissão para editar conteúdo |
| ToolbarRenderer | Renderiza a barra de ferramentas | Adiciona uma funcionalidade de barra de ferramentas |

### Eventos do Portlet {#portlet-events}

A API do portlet (JSR-286) especifica eventos de portlet. O portlet de conteúdo AEM tem uma ponte integrada, distribuindo eventos de portlet para o portlet AEM como eventos OSGi - isso torna conectável o manuseio de eventos de portlet.

Se quiser manipular eventos específicos, declare que eles recebem eventos no descritor de deployment (ou configure-o pelo servidor do portal) e implemente um serviço OSGi que declare a interface EventHandler (consulte a especificação OSGi EventAdmin).

Sempre que ocorrer um evento de portlet, um evento OSGi específico será enviado chamando o manipulador. O manipulador obtém todas as informações de contexto e pode atualizar o status do portlet de acordo ou enviar novos eventos. Basicamente, dentro do método de manipulação, toda a funcionalidade da fase de evento do portlet pode ser usada.

## Uso do AEM como portal {#using-aem-as-a-portal}

Use o componente Portlet para adicionar janelas de portlet a páginas AEM. As bibliotecas compartilhadas que você instala no servidor de aplicativos permitem que o componente Portlet detecte aplicativos de portlet implantados.

Para usar o AEM como um portal, execute as seguintes tarefas:

1. Instale o componente Portlet e as bibliotecas compartilhadas.
1. Adicione o componente Portlet ao Sidekick.
1. Configure e implante a aplicação Web que contém os portlets que você deseja que apareçam no componente Portal.
1. Adicione o componente Portlet a uma página e selecione o portlet a ser exibido.

>[!NOTE]
>
>Você pode usar o componente de portlet somente quando o AEM é implantado como um aplicativo web. ([Consulte Instalação de AEM com um Servidor de Aplicativos](/help/sites-deploying/application-server-install.md).)

### Instalar o componente do portlet {#installing-the-portlet-component}

O arquivo JAR AEM Quickstart contém os arquivos de componente do portlet. Para obter os arquivos (cq-portlet-components.zip), você pode executar o Início rápido ou extrair o conteúdo.

1. Execute ou extraia o conteúdo do arquivo JAR Quickstart e localize o arquivo cq-portlet-components.zip de acordo:

   * Executar Quickstart: crx-quickstart/opt/portal
   * Extrair conteúdo de início rápido: estático/opcional/portal

1. Abra o Gerenciador de pacotes da instância do autor do CQ5 que está implantada no servidor de aplicativos. (https://*appserverhost*:*port*/cq5author/crx/packmgr)

1. Use o Gerenciador de pacotes para [Carregar e instalar](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) o pacote cq-portlets-components.zip.

   O pacote instala o cq-portlet-diretor-sharedlibs-x.x.x.jar na pasta /libs/portal/diretor no repositório.

1. Copie cq-portlet-diretor-sharedlibs-x.x.x.jar no disco rígido. Use qualquer meio para obter o arquivo, por exemplo, FileVault ou um cliente WebDAV.
1. Mova o arquivo cq-portlet-diretor-sharedlibs.x.x.x.jar para a pasta da biblioteca compartilhada do seu servidor de aplicativos, de modo que as classes estejam disponíveis para aplicativos de portlet implantados.

### Adicionar o componente Portlet ao Sidekick {#adding-the-portlet-component-to-sidekick}

Adicione o componente de portlet ao sistema de parágrafos para que ele fique disponível aos autores.

1. No Sidekick, clique no ícone da régua para entrar no modo Design.
1. Ao lado do cabeçalho `Design of par` acima do primeiro parágrafo, clique em **Editar**.

1. Na categoria de componentes **Geral**, marque a caixa de seleção ao lado do componente Portlet e clique em OK.

![chlimage_1-25](assets/chlimage_1-25.jpeg)

### Configurar e implantar aplicativos de portlet {#configuring-and-deploying-your-portlet-applications}

Implante os portlets no contêiner da Web do servidor de aplicativos para que eles fiquem disponíveis para o componente Portal. Antes de implantar o aplicativo do portlet, é necessário configurar o aplicativo para que ele carregue o servlet container do portal AEM. Essa configuração permite que o componente Portlet acesse os portlets.

1. Extraia o conteúdo do arquivo WAR do aplicativo portlet.

   **Dica:** o comando jar xf *nameofapp*.war extrai os arquivos.

1. Abra o arquivo web.xml em um editor de texto.
1. Adicione a seguinte configuração de servlet no elemento web-app:

   ```xml
   <servlet>
           <servlet-name>slingportal</servlet-name>
           <servlet-class>org.apache.sling.portal.container.api.ContainerServlet</servlet-class>
           <load-on-startup>1</load-on-startup>
   </servlet>
   <servlet-mapping>
           <servlet-name>slingportal</servlet-name>
           <url-pattern>/SlingPortletInvoker</url-pattern>
   </servlet-mapping>
   ```

1. Salve o arquivo web.xml e empacote novamente o arquivo WAR.

   **Dica:** o comando `jar cvf nameofapp.war *` adiciona conteúdo do diretório atual ao arquivo nameofapp.war.

1. Implante o aplicativo do portlet no servidor de aplicativos. Para obter informações, consulte a documentação do servidor de aplicativos.

### Adicionar portlets à página AEM {#adding-portlets-to-your-aem-page}

Use o componente Portal para adicionar uma janela de portlet à página da Web. Use as propriedades do componente para especificar o portlet a ser exibido.

1. Na página da Web, arraste o componente **Portlet** do grupo Geral no Sidekick para a página.

   >[!NOTE]
   >
   >Depois de arrastar o componente para a página, recarregue a página para garantir que funcione corretamente.

1. Clique duas vezes no componente para abrir as propriedades do Portlet.
1. No menu suspenso **Entidade do portlet**, selecione o portlet na lista.
1. Marque ou desmarque a caixa de seleção **Ocultar barra de título** se desejar visualizar a barra de título do portlet.
1. No campo **Janela do Portlet**, digite uma ID exclusiva da Janela do Portlet, se desejar.

   >[!NOTE]
   >
   >Se você planeja usar o mesmo portlet mais de uma vez na mesma página, forneça a cada portlet uma ID de janela diferente.

1. Clique em **OK**. O portlet é exibido na página do AEM.

   ![chlimage_1-136](assets/chlimage_1-136.png)

## Instalação, configuração e uso do AEM em um portlet {#installing-configuring-and-using-aem-in-a-portlet}

Para acessar o conteúdo fornecido pelo AEM WCM, o servidor do portal precisa ser equipado com o AEM Portal Director Portlet. Para fazer isso, instale, configure e adicione o portlet à página do portal usando as etapas fornecidas nesta seção.

Por padrão, o portlet se conecta à instância de publicação em localhost:4503 e à instância de autor em localhost:4502. Esses valores podem ser alterados durante a implantação do portlet. O diretor do portal está disponível como conteúdo no repositório em /libs/portal/diretory. Baixe o arquivo WAR do aplicativo antes de usá-lo.

### Baixando o arquivo WAR {#downloading-the-war-file}

1. Usando o Webdav ou o CRXDE Lite, navegue até /libs/portal/diretor.

1. Baixe *cq-portlet-webapp.war*.

>[!NOTE]
>
>Esses procedimentos usam o portal Websphere como exemplo, embora sejam o mais genéricos possível; os procedimentos variam para outros portais da web. Embora as etapas sejam essencialmente idênticas para todos os portais da Web, é necessário redefinir as etapas de um portal da Web específico.

#### Instalar o portlet {#installing-the-portlet}

Para instalar o portlet:

1. Efetue login no portal com privilégios de administrador.
1. Navegue até a parte Gerenciamento de portlet do portal da Web.
1. Clique em Instalar e navegue até o aplicativo do portlet AEM (cq-portlet-webapp.war) que você baixou e insira outras informações importantes sobre o portlet.

   Para outras informações essenciais do portlet, você pode aceitar os padrões ou alterar os valores. Se você aceitar os valores padrão, o portlet estará disponível em https://&lt;wps-host>:&lt;port>/wps/PA_CQ5_Portlet. O console de administração do OSGi fornecido pelo portlet está disponível em https://&lt;wps-host>:&lt;port>/wps/ PA_CQ5_Portlet/cqbridge/system/console (o nome de usuário/senha padrão é admin/admin).

1. Certifique-se de que o aplicativo de portlet seja iniciado automaticamente marcando essa opção ou caixa de seleção e salve as alterações. Você verá uma mensagem informando que a instalação foi bem-sucedida.

#### Configurar o portlet {#configuring-the-portlet}

Depois de instalar o portlet, você precisa configurá-lo para que ele saiba os URLs das instâncias AEM subjacentes (autor e publicação). Você também pode configurar outras opções.

Para configurar o portlet:

1. Na janela Portal administration do servidor de aplicativos, navegue até portlet management, onde todos os portlets são listados e selecione o portlet AEM Portal Director.
1. Configure o portlet, conforme necessário. Por exemplo, talvez seja necessário alterar a URL das instâncias de autor e publicação e a URL do caminho inicial. As configurações padrão estão descritas em [Preferências do Portlet](/help/sites-administering/aem-as-portal.md#portlet-preferences).

   >[!NOTE]
   >
   >Se o portlet estiver configurado para conectar-se a instâncias de autor e publicação do AEM que estejam em execução em um caminho de contexto diferente de **/**, será necessário habilitar a força **CQUrlInfo** na configuração do Gerenciador de Biblioteca Html dessas instâncias AEM (por exemplo, via Felix Webconsole) ou a edição não funcionará e a caixa de diálogo de preferências não aparecerá.

1. Salve as alterações de configuração no servidor de aplicativos.

1. Navegue até o Admin Console OSGI do portlet. O local padrão é `https://<wps-host>:<port>/wps/PA_CQ5_Portlet/cqbridge/system/console/configMgr`. O nome de usuário/senha padrão é **admin/admin**.

1. Selecione a configuração **Day Portal Director CQ Server Configuration** e edite os seguintes valores:

   * **URL Base do Autor**: a URL base da instância do autor AEM.
   * **URL Base do Publish**: a URL base da instância de publicação AEM.
   * **Autor Usado como Publish**: A instância do autor é usada como uma publicação
instância (para desenvolvimento)?

   ![chlimage_1-137](assets/chlimage_1-137.png)

1. Clique em **Salvar**. Agora você pode adicionar o portlet às páginas do portal e usar o portal.

### URLs de conteúdo {#content-urls}

Quando o conteúdo é solicitado do AEM, o portlet usa o modo de exibição atual (publicação ou autor) e o caminho atual para montar um URL completo. Com os valores padrão, a primeira url é `https://localhost:4503/content/geometrixx/en.portlet.html`. O valor de `htmlSelector` é automaticamente adicionado à URL antes da extensão.

Se o portlet alternar para o modo de ajuda e o `appendHelpViewModeAsSelector` for selecionado, o seletor `help` também será anexado, por exemplo, `https://localhost:4503/content/geometrixx/en.portlet.html.help`. Se a janela do portlet estiver maximizada e o `appendMaxWindowStateAsSelector` estiver selecionado, o seletor também será anexado, por exemplo, `https://localhost:4503/content/geometrixx/en.portlet.max.help`.

Os seletores podem ser avaliados em AEM e um template diferente pode ser usado para seletores diferentes.

### Utilização de um mapa de URL de conteúdo no AEM {#using-a-content-url-map-in-aem}

Normalmente, o caminho de início aponta diretamente para o conteúdo no AEM. No entanto, se você quiser manter os caminhos de início no AEM, em vez de nas preferências do portlet, você pode apontar o caminho de início para um mapa de conteúdo no AEM, como `/var/portlets`. Nesse caso, um script em execução no AEM pode usar as informações enviadas do portlet para decidir qual URL é o URL inicial. Ele deve emitir um redirecionamento para o URL correto.

#### Adicionar o portlet à página do portal {#adding-the-portlet-to-the-portal-page}

Para adicionar o portlet à página do portal:

1. Verifique se você está na janela de administração do servidor de aplicativos e navegue até o local onde gerencia as páginas. (por exemplo, no WebSphere 6.1, clique em **Gerenciar páginas**).
1. Selecione o nome do portlet e uma página existente ou crie uma página.
1. Edite o layout da página.
1. Selecione o portlet e adicione-o a um container.
1. Salve as alterações.

#### Uso do Portlet {#using-the-portlet}

Para acessar a página adicionada ao portlet:

1. No menu de personalização do portlet, configure-o conforme foi configurado no portal.
1. Abra a configuração (O portlet exibe o URL inicial de publicação configurado na configuração do portlet), faça as edições necessárias e, em seguida, salve-as.
