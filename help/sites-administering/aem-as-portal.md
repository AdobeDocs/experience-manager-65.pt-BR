---
title: Portais e portlets do AEM
seo-title: Portais e portlets do AEM
description: Saiba mais sobre portais e portais no AEM.
seo-description: Saiba mais sobre portais e portais no AEM.
uuid: 7f9e316d-277e-4a1e-b6f3-cd89addc897b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 99528fda-5c8c-4034-bcbe-a4cea42f694b
docset: aem65
translation-type: tm+mt
source-git-commit: b97452eb42275d889a82eb9364b5daf7075fcc41

---


# Portais e portlets do AEM{#aem-portals-and-portlets}

Este documento descreve o seguinte:

* Arquitetura do AEM Portal
* Administração e configuração do AEM como um portal
* Usar o AEM como portal
* Instalação, configuração e exibição de conteúdo AEM em um portlet (por exemplo, um servidor da Web)

## Arquitetura do AEM Portal {#aem-portal-architecture}

A arquitetura do portal do AEM inclui definições de portais e portlets.

### O que é um portal? {#what-is-a-portal}

Um portal é um aplicativo da Web que fornece personalização, logon único, integração de conteúdo de diferentes fontes e hospeda a camada de apresentação dos sistemas de informações.

Você pode executar portlets compatíveis com JSR 286 no AEM. O componente do portlet permite que você incorpore um portlet à página. Consulte [Administração do portlet](#administeringthecqcontentportlet)de conteúdo do AEM.

### O que é um portlet? {#what-is-a-portlet}

Os portlets são componentes da Web implantados dentro de um container que geram conteúdo dinâmico. A interface do portlet é empacotada e implantada como um arquivo .war dentro de um container de portlet. Se você estiver executando o AEM como um portal, precisará do arquivo .war do portlet para executar o portlet.

Para configurar o conteúdo do AEM para aparecer em um portal, consulte [Instalar, configurar e usar o AEM em um portlet](#installingconfiguringandusingcqinaportlet).

### AEM Portal Diretor {#aem-portal-director}

>[!CAUTION]
>
>O AEM Portal Diretor está obsoleto a partir do AEM 6.4. Consulte Recursos [obsoletos e removidos](https://helpx.adobe.com/experience-manager/6-4/release-notes/deprecated-removed-features.html).

## Administração do portlet de conteúdo do AEM {#administering-the-aem-content-portlet}

O portlet de conteúdo do AEM permite que você exiba conteúdo do AEM em um portal. O portlet está disponível em `/crx-quickstart/opt/portal`e pode ser personalizado de várias maneiras. Por exemplo, você pode personalizar a manipulação SSO/Autenticação ao implantar seu próprio serviço de autenticação gerando as informações de autenticação necessárias para o AEM para substituir o comportamento padrão. Os plug-ins usam uma API definida que permite que você adicione sua própria funcionalidade ao criar o plug-in em relação à API. O plug-in pode ser implantado no portlet em execução. Para funcionar corretamente, é necessário ter uma configuração do autor e da instância de publicação do AEM junto com o caminho do conteúdo para ser exibido na inicialização.

Algumas configurações podem ser alteradas através das preferências do portlet e outras através das configurações de serviço OSGi. Você altera essas configurações usando arquivos de **configuração** ou o console da Web OSGi.

### Preferências do portlet {#portlet-preferences}

As preferências de portlet podem ser configuradas no momento da implantação no servidor de portal ou editando o arquivo **WEB-INF/portlet.xml** antes da implantação do aplicativo Web portlet. Por padrão, o arquivo portlet.xml é exibido da seguinte maneira:

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
   <td><p>Este é o caminho de start do portlet: define o conteúdo que é exibido inicialmente.</p> <p><strong>Importante</strong>: Se o portlet estiver configurado para se conectar ao autor do AEM e publicar instâncias que estejam sendo executadas em um caminho de contexto diferente<strong> de /</strong>, será necessário ativar a opção forçar o <strong>CQUrlInfo</strong> na configuração do Html Library Manager dessas instâncias do AEM (por exemplo, via console do Web do Felix) ou a edição não funcionará e a caixa de diálogo de preferências não aparecerá.</p> </td>
  </tr>
  <tr>
   <td>htmlSeletor</td>
   <td>O seletor que é anexado a cada url. Por padrão, este é um <strong>portlet</strong>, portanto, todas as solicitações para páginas html usam urls que terminam em <strong>.portlet.html.</strong> Isso permite o uso de scripts personalizados no AEM para renderização de portlet.</td>
  </tr>
  <tr>
   <td>addCssToPortalHeader</td>
   <td><p>Por padrão, os arquivos css incluídos na página HTML do AEM são incluídos no portlet. A desativação dessa opção exclui os arquivos css padrão.</p> <p>Se essa opção estiver ativada, os arquivos CSS serão adicionados ao cabeçalho da página html ou incorporados à página html, dependendo do comportamento do portal.</p> </td>
  </tr>
  <tr>
   <td>includeToolbar</td>
   <td>Por padrão, uma barra de ferramentas é renderizada dentro do portlet de conteúdo para a funcionalidade de gerenciamento. Ao desativar essa opção, nenhuma barra de ferramentas é renderizada.</td>
  </tr>
  <tr>
   <td>urlParameterNames</td>
   <td><p>Lista de nomes de parâmetros de URL alternativos que podem conter o novo URL de conteúdo a ser exibido para o portlet. A lista é processada de cima para baixo, o primeiro parâmetro que contém um valor é usado. Se nenhum URL for encontrado, o parâmetro de URL padrão será usado. O URL fornecido é usado, como está, sem qualquer modificação adicional.</p> <p>Essa configuração é por portlet implantado - também é para configurar globalmente alguns parâmetros de url na configuração OSGi para a "Ponte do portlet do Day Portal Diretor".</p> </td>
  </tr>
  <tr>
   <td>priorityDialog</td>
   <td>Caminho para a caixa de diálogo de preferências no AEM - se deixado em branco, a caixa de diálogo de preferências incorporadas será usada. O padrão é /libs/portal/content/prefs.html.</td>
  </tr>
  <tr>
   <td>initialRedirect</td>
   <td>Por padrão, o portlet executa um redirecionamento javascript de toda a página do portal na primeira invocação. Isso é para suportar o cenário de arrastar e soltar dos servidores de portal modernos. Na produção, esse redirecionamento raramente é necessário e pode, portanto, ser desativado com essa preferência sendo definida como <em>false</em>.</td>
  </tr>
 </tbody>
</table>

#### Console Web OSGi {#osgi-web-console}

Supondo que o servidor de portal seja executado em host local, porta 8080 e que o aplicativo Web de portlet AEM seja montado no *cportlet* de contexto de aplicativo da Web, o url para para o console da Web será `https://localhost:8080/cqportlet/cqbridge/system/console`. O usuário e a senha padrão são **admin**.

Abra a guia **Configurações** e selecione Configuração **do servidor CQ do diretório** do portal. Aqui, você especifica o URL básico para o autor e a instância de publicação. Este procedimento é descrito em [Configuração do portlet](#configuring-the-portlet).

>[!NOTE]
>
>O console da Web do OSGi é destinado apenas a alterar configurações durante o desenvolvimento (ou testes). Certifique-se de bloquear solicitações no console para sistemas de produção.

### Fornecimento de configurações {#providing-configurations}

Para suportar implantações automatizadas e provisionamento de configuração, o portlet de conteúdo AEM tem suporte de configuração incorporado que tenta ler configurações do classpath fornecido para o aplicativo portlet.

Na inicialização, a propriedade do sistema **com.day.cq.portet.config** é lida para detectar o ambiente atual. Normalmente, o valor dessa propriedade é algo como **dev**, **prod**, **test** e assim por diante. Se nenhum ambiente estiver definido, nenhuma configuração será lida.

Se um ambiente for definido, um arquivo de configuração será pesquisado no classpath em * ***com/day/cq/portlet/{env}.config** , onde **env** é substituído pelo valor real do ambiente. Este arquivo deve lista todos os arquivos de configuração para este ambiente. Esses arquivos são pesquisados em relação ao local do arquivo de configuração. Por exemplo, se o arquivo contém uma linha, `my.service.xml,` esse arquivo é lido do classpath em `com/day/cq/portlet/my.service.config.` O nome do arquivo consiste na ID de persistência do serviço, seguido por **.config**. No exemplo anterior, a ID de persistência é **my.service**. O formato do arquivo de configuração é o formato usado pelo instalador do Apache Sling OSGi.

Isso significa que, para cada ambiente, é necessário adicionar um arquivo de configuração correspondente. Uma configuração que deve ser aplicada a todos os ambientes precisa ser inserida em todos esses arquivos - se for apenas para um único ambiente, ela será inserida nesse arquivo. Esse mecanismo garante controle total sobre qual configuração é lida em qual ambiente.

É possível usar uma propriedade do sistema diferente para detectar o ambiente. Especifique a propriedade do sistema **com.day.cq.portet.configproperty** que contém o nome da propriedade do sistema a ser usada em vez de **com.day.cq.portet.config**.

#### Invalidação de armazenamento em cache e armazenamento em cache {#caching-and-caching-invalidation}

O portlet, em sua configuração padrão, armazena em cache as respostas recebidas do WCM AEM em um cache específico do usuário. Os caches precisam ser invalidados quando houver alterações no conteúdo da instância de publicação. Para essa finalidade, no AEM WCM, um agente de replicação deve ser configurado na instância do autor. O cache também pode ser descarregado manualmente. Esta seção descreve ambos os procedimentos.

O portlet pode ser configurado com seu próprio cache, de modo que o conteúdo no portlet seja exibido sem a necessidade de acesso ao AEM. O portal está disponível como conteúdo em /libs/portal/diretor. Para acessar o conteúdo, start uma instância do AEM e baixe, usando o CRXDE Lite ou o Webdav, o arquivo desse local.

Você pode implantar esse pacote em tempo de execução ou adicioná-lo ao aplicativo da Web portlet em `WEB-INF/lib/resources/bundles` antes da implantação.

Após a implantação do cache, o portlet armazena em cache o conteúdo da instância de publicação. O cache do portlet pode ser invalidado com um despachante do AEM. Para configurar o portlet para usar seu próprio cache:

1. Configure um agente de replicação no autor que público alvo o servidor de portal.
1. Supondo que o servidor de portal seja executado em host **localhost**, **porta 8080 **e que o aplicativo da Web de portlet AEM seja montado no **cqportlet** de contexto, o url para liberar o cache será `https://localhost:8080/cqportlet/cqbridge/cqpcache?Path=$(path)`. Use GET como o método.
   **Observação:** Em vez de usar um parâmetro de solicitação, você pode enviar um cabeçalho http chamado **Caminho**.

#### Liberando o cache pelo agente de replicação {#flushing-the-cache-via-replication-agent}

Assim como a invalidação normal do dispatcher, um agente de replicação pode ser configurado para público alvo do cache do portlet AEM do portal. Depois de configurar o agente de replicação, cada ativação de página regular limpa o cache do portal.

Se você operar vários nós de portal executando o portlet AEM, será necessário criar um agente para cada nó, conforme descrito neste procedimento.

Para configurar um agente de replicação para o portal:

1. Faça logon na instância do autor.
1. Na guia Sites, clique na guia *Ferramentas* .
1. Clique em **Nova página...** nos agentes de replicação **Novo...** menu.

   ![screen_shot_2012-02-15at40647pm](assets/screen_shot_2012-02-15at40647pm.png)

1. Em *Modelo*, selecione Agente *de* Replicação e insira um nome para o agente. Clique em *Criar*.

   ![screen_shot_2012-02-15at40817pm](assets/screen_shot_2012-02-15at40817pm.png)

1. Clique com o Duplo no agente de replicação que você acabou de criar. Ele é exibido como inválido, pois ainda não foi configurado.

   ![screen_shot_2012-02-15at41001pm](assets/screen_shot_2012-02-15at41001pm.png)

1. Clique em **Editar.**
1. Na guia **Configurações** , marque a caixa de seleção **Ativado** , selecione **Dispatcher Flush** como o tipo de serialização e digite um tempo limite de nova tentativa (por exemplo, 60000).

   ![screen_shot_2012-02-15at42101pm](assets/screen_shot_2012-02-15at42101pm.png)

1. Click the **Transport** tab.
1. No campo **URI** , digite o URL (URL) de liberação do portlet. O URI está na seguinte forma:

   ```xml
   https://<wps-host>:<port>/<wps-context>/<cq5-portlet-context>/cqbridge/cqpcache
   ```

   ![screen_shot_2012-02-15at42322pm](assets/screen_shot_2012-02-15at42322pm.png)

1. Click the **Extended** tab.

   ![screen_shot_2012-02-15at42515pm](assets/screen_shot_2012-02-15at42515pm.png)

1. No campo Método **** HTTP, digite **GET**.
1. No campo Cabeçalhos **** HTTP, clique em **+** para adicionar uma nova entrada e digite **Caminho: {path}**.
1. Se necessário, clique na guia **Proxy** e insira informações de proxy para o agente.
1. Click **OK** to save changes.
1. Para testar a conexão, clique no link **Testar conexão** . Uma mensagem de registro é exibida indicando se o teste de replicação foi bem-sucedido. Por exemplo:

   ![screen_shot_2012-02-15at42639pm](assets/screen_shot_2012-02-15at42639pm.png)

#### Limpando manualmente o cache do portlet {#manually-flushing-the-portlet-cache}

É possível liberar manualmente o cache do portlet acessando o mesmo URL configurado para o agente de replicação. Consulte [Limpando o cache](#flushing-the-cache-via-replication-agent) para obter o formulário do URL. Além disso, o URL precisa ser estendido com um parâmetro de URL Path=&lt;path> para indicar o que será descarregado.

Por exemplo:

`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=*` libera o cache completo. `https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=/content/mypage/xyz` libera `/content/mypage/xyz` do cache.

### Segurança do portal {#portal-security}

O portal é o mecanismo de autenticação de direção. Você pode fazer logon no AEM com um usuário técnico, o usuário do portal, um grupo e assim por diante. O portlet não tem acesso à senha para o usuário no portal, portanto, se o portlet não souber todas as credenciais para fazer logon com êxito em um usuário, uma solução SSO deverá ser usada. Nesse caso, o portlet AEM encaminha todas as informações necessárias para o AEM, que, por sua vez, encaminha essas informações para o repositório subjacente do AEM. Esse comportamento é plugável e pode ser personalizado.

### Autenticação ao publicar {#authentication-on-publish}

Esta seção descreve os modos de autenticação disponíveis que o portlet pode usar na comunicação com as instâncias subjacentes do WCM AEM.

Por padrão, nenhuma informação do usuário é enviada para a instância de publicação do AEM; o conteúdo é sempre exibido como o usuário anônimo. Se informações específicas do usuário devem ser entregues pelo AEM ou se a autenticação do usuário para publicação for obrigatória, isso deve ser ativado.

#### Acessar a configuração de autenticação do portlet {#accessing-the-portlet-s-authentication-configuration}

As opções de configuração de autenticação que o portlet usa nas instâncias WCM AEM estão disponíveis no console da Web (configuração OSGi).

>[!NOTE]
>
>Ao trabalhar com o AEM, há vários métodos de gerenciar as configurações dos serviços OSGi (nós do console ou do repositório).
>
>Consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos.

Para acessar a configuração de autenticação do portlet:

1. Acesse o console da Web no seguinte URL:

   `https://localhost:8080/cqportlet/cqbridge/system/console`

   Por exemplo, em sua configuração padrão:

   `https://wps-host:10040/wps/PA_CQ5_Portlet/cqbridge/system/console`

1. Faça logon no console da Web. As credenciais padrão são `admin/admin`.
1. No console, selecione **Configuração**.
1. No menu **Configuração** , selecione um serviço específico para configurar. Os serviços são fornecidos pelo portlet na estrutura OSGi.

   | Nome do serviço | Descrição |
   |---|---|
   | Autenticador do Day Portal Diretor | Configure qual modo de autenticação é usado para instâncias WCM AEM. Dependendo do modo selecionado, é possível especificar um usuário técnico ou o nome do cookie SSO. Além disso, a autenticação para instâncias de publicação do WCM AEM pode ser ativada. |
   | Cache de Arquivo do Diretor do Portal de Dias | Configure os parâmetros de como o portlet armazena em cache as respostas recebidas das instâncias do AEM WCM. |
   | Serviço de Cliente HTTP do Day Portal Diretor | Configure como o portlet se conecta via HTTP às instâncias subjacentes do AEM WCM. Por exemplo, você pode especificar um servidor proxy. |
   | Manipulador de Localidade do Diretor do Portal de Dia | Configure quais localidades o portlet suporta. As solicitações para instâncias do WCM AEM são baseadas na localidade do usuário; por exemplo, idioma do usuário *alemão *solicitaria `/content/geometrixx/de/`.... |
   | Gerente de Privilégio do Diretor do Portal de Dia | Configure se o portlet deve testar a guia Sites com base no usuário conectado no momento. |
   | Renderizador da barra de ferramentas do Day Portal | Personalize a renderização da barra de ferramentas do portlet. |

1. Além disso, você pode configurar o console da Web e o serviço de registro. Por exemplo, você pode alterar as credenciais de administrador para o console da Web clicando no link Console de gerenciamento do Apache Felix OSGi.

#### Modo de usuário técnico {#technical-user-mode}

No modo padrão, todas as solicitações emitidas pelo portlet para a instância do autor do WCM AEM são autenticadas usando o mesmo usuário técnico, independentemente do usuário do portal atual. O modo de Usuário Técnico está ativado por padrão. Você ativa/desativa esse modo na respectiva tela de configuração no console de gerenciamento OSGi:

O usuário técnico especificado deve existir na instância do autor do WCM AEM e na instância de publicação se a opção **Autenticar ao publicar** estiver ativada. Certifique-se de conceder ao usuário privilégios de acesso suficientes para o trabalho de criação.

#### SSO {#sso}

O portlet suporta SSO com AEM pronto para uso. O serviço de autenticação pode ser configurado para usar o SSO e transmitir o usuário atual do portal com o formato **Basic** como um cookie chamado `cqpsso` de AEM. O AEM deve ser configurado para usar o manipulador de autenticação SSO para path /. O nome do cookie também precisa ser configurado aqui.

O repositório `crx-quickstart/repository/repository.xml` do AEM precisa ser configurado de acordo:

```xml
<LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
  ...
  <param name="trust_credentials_attribute" value="TrustedInfo"/>
  <param name="anonymous_principal" value="anonymous"/>
</LoginModule>
```

#### Modo de autenticação SSO {#sso-authentication-mode}

O portlet pode ser autenticado para o AEM WCM usando o esquema Single Sign On (SSO). Nesse modo, o usuário conectado no momento ao portal é encaminhado para o AEM WCM na forma de um cookie SSO. Se o modo SSO for usado, todos os usuários do portal com acesso ao portlet AEM devem ser conhecidos pelas instâncias subjacentes do WCM AEM, mais comumente na forma de WCM AEM conectado ao LDAP, ou por terem criado os usuários manualmente antes. Além disso, antes de habilitar o SSO no portlet, a instância subjacente do autor WCM do AEM (e a instância de publicação, se **Autenticar ao publicar** estiver habilitada) precisa ser configurada para aceitar solicitações baseadas em SSO.

Para configurar o portlet para usar o modo de autenticação SSO, conclua as seguintes etapas (descritas em detalhes nas seções a seguir):

* Ative o repositório do WCM AEM para aceitar credenciais confiáveis.
* Ative a autenticação SSO no WCM AEM.
* Ative a autenticação SSO no portlet AEM.

#### Permitir que o repositório do WCM AEM aceite credenciais confiáveis {#enabling-aem-wcm-s-repository-to-accept-trusted-credentials}

Antes que o SSO possa ser ativado para o AEM WCM, o repositório subjacente precisa ser configurado para aceitar as credenciais confiáveis fornecidas pelo AEM WCM. Para fazer isso, configure o repositório.xml do AEM.

1. No sistema de arquivos onde o AEM WCM está instalado, abra o seguinte arquivo:

   `//crx-quickstart/repository/repository.xml`

1. No arquivo XML, localize a entrada para o **LoginModule** e adicione o trust_entials_attribute à sua configuração:

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
     <param name="anonymous_principal" value="anonymous"/>
   </LoginModule>
   ```

1. Reinicie o AEM WCM para que as alterações entrem em vigor.

#### Ativar a autenticação SSO no AEM WCM {#enabling-sso-authentication-in-the-aem-wcm}

Para ativar o SSO no WCM AEM, acesse a entrada de configuração relevante no console de gerenciamento da Web Apache Felix (OSGi) do AEM WCM:

1. Acesse o console por meio de seu URI em https://&lt;AEM-host>:&lt;porta>/system/console.
1. No menu Configuração, selecione Manipulador de Autenticação SSO. Neste exemplo, o manipulador SSO aceita solicitações SSO para todos os caminhos com base no cookie fornecido pelo portlet AEM. Sua configuração pode variar.

   | Caminho | / | Habilita o manipulador SSO para todas as solicitações |
   |---|---|---|
   | Nomes de cookie | cqpsso | Nome do cookie fornecido pelo portlet, conforme configurado no console OSGi do portlet. |

1. Clique em **Salvar** para ativar o SSO. O SSO agora é o esquema de autenticação principal.

Para cada solicitação que o AEM WCM receber, primeiro a autenticação baseada em SSO é tentada. Em caso de falha, é executado um fallback para o esquema de autenticação básico comum. Como tal, as conexões normais com o AEM WCM sem SSO permanecem possíveis.

#### Ativação da autenticação SSO em um portlet AEM {#enabling-sso-authentication-in-a-aem-portlet}

Para que a instância WCM subjacente do AEM aceite solicitações SSO, o modo de autenticação do portlet deve ser alternado de **Técnico** para **SSO**.

Para ativar a autenticação SSO em um portlet AEM:

1. Acesse o console por meio de seu URI em https://&lt;aem-host>:&lt;porta>/system/console.
1. No menu Configuração, selecione Autenticador do Day Portal Diretor na lista de configurações disponíveis.
1. No modo, selecione SSO. Deixe os outros parâmetros com seus valores padrão.

   ![chlimage_1-135](assets/chlimage_1-135.png)

1. Clique em Salvar para ativar o SSO para o portlet.

   Para fins de teste, acesse o portlet com o usuário administrativo do portal, depois de criar o mesmo usuário no WCM AEM com privilégios de administrador.

Após executar esse procedimento, as solicitações são autenticadas usando o SSO. Um trecho típico da comunicação HTTP revela a presença dos seguintes cabeçalhos SSO e Portlet específicos:

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

### Habilitando autenticação PIN {#enabling-pin-authentication}

Se você não estiver usando os recursos padrão de edição em linha do portlet de conteúdo AEM, mas quiser que a parte de criação e administração do portlet seja feita fora do portal diretamente na instância do autor AEM, ative a autenticação PIN. Também é necessário alterar a configuração dos botões de gerenciamento.

Para abrir a página de administração do site ou editar uma página do portlet, o portlet de conteúdo AEM usa a nova autenticação de pinos. Por padrão, a autenticação de pinos está desativada, portanto, as seguintes alterações de configuração devem ser feitas no AEM:

1. Ative a autenticação confiável no AEM adicionando as informações confiáveis no arquivo repository.xml:

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
   </LoginModule>
   ```

1. No console de configuração do OSGi, por padrão localizado em https://localhost:4502/system/console/configMgr, selecione **CQ PIN Authentication Handler** no menu suspenso.
1. Edite o parâmetro Caminho **raiz do** URL para conter apenas o valor **/**.

### Privilégios {#privileges}

Algumas funções do portlet são protegidas por privilégios. O usuário atual precisa ter esse privilégio para poder acessar essa função. Há os seguintes privilégios predefinidos:

* &quot;barra de ferramentas&quot; : Esse é o privilégio geral de ver/usar a barra de ferramentas no portlet.
* &quot;prefs&quot; : Se o usuário tiver esse privilégio, ele poderá ver/alterar as preferências do portlet.
* &quot;cq-author:edit&quot; : Com esse privilégio, o usuário tem permissão para invocar a visualização de edição do conteúdo.
* &quot;cq-author:pré-visualização&quot; : Com esse privilégio, o usuário tem permissão para ver a pré-visualização.
* &quot;cq-author:siteadmin&quot; : Com esse privilégio, o usuário tem permissão para abrir o siteadmin no AEM.

A melhor abordagem para gerenciar os privilégios é usar funções de portal e atribuir funções a esses privilégios. Isso pode ser feito por meio de uma configuração OSGi. O &quot;Gerenciador de privilégios do Diretor do Portal de Dia&quot; pode ser configurado com um conjunto de funções para cada privilégio. Se o usuário tiver uma das funções, ele terá o privilégio correspondente.

Além disso, é possível definir essa função com base no acesso em uma base de instância por portlet. A caixa de diálogo de preferências do portlet contém um campo de entrada para cada um dos privilégios acima. Para cada privilégio, é possível configurar uma lista separada por vírgulas de funções de portlet. Se um valor for configurado, isso substituirá a configuração global do serviço &quot;Gerenciador de privilégios do Diretor do Portal de Dia&quot; e talvez seja necessário adicionar as mesmas funções dessa configuração global, já que as funções não são mescladas! Se nenhum valor for especificado, a configuração global será usada.

### Personalização do aplicativo de portlet AEM {#customizing-the-aem-portlet-application}

O aplicativo de portlet AEM fornecido start um container OSGi dentro do aplicativo da Web, assim como o AEM faz. Esta arquitetura permite que você utilize todos os benefícios do OSGi:

* Fácil de atualizar e estender
* Fornece atualizações instantâneas do portlet sem nenhuma interação do servidor do portal
* Fácil de personalizar o portlet

### Botões da barra de ferramentas {#toolbar-buttons}

A barra de ferramentas e seus botões são configuráveis e podem ser personalizados. Você pode adicionar seus próprios botões à barra de ferramentas ou definir quais botões serão exibidos em qual modo. Cada botão é um serviço OSGi configurável por meio de uma configuração OSGi.

O console da Web OSGi lista todas as configurações de botão na guia **Configuração** . Para cada botão, você pode definir em qual modo esse botão será exibido. Isso permite desativar um botão removendo todos os modos, por exemplo.

Por padrão, o portlet de conteúdo do AEM usa a funcionalidade de edição em linha. Entretanto, se você preferir alternar para a instância do autor de AEM para edição, ative o botão **** SiteAdmin e o botão **** ContentFinder, mas desative o botão **** Editar. Nesse caso, certifique-se de configurar corretamente a autenticação PIN no AEM.

O layout da barra de ferramentas do portlet pode ser personalizado instalando-se um pacote por meio do console Web Felix do portlet, que contém CSS/HTML personalizado em um local predefinido.

#### Estrutura do pacote {#bundle-structure}

A seguir está uma estrutura de conjunto de exemplos:

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

A pasta META-INF contém o arquivo MANIFEST.MF necessário pelo OSGi para identificá-lo como um pacote. O texto é exibido como segue:

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

O fato de que o HTML/CSS/images está na pasta /com/day/cq/portlet/toolbar/layout é obrigatório pelo portlet e não pode ser alterado. Nas mesmas linhas, os cabeçalhos Import-Package e Export-Package em MANIFEST.MF também devem ser chamados de /com/day/cq/portlet/toolbar/layout. O Bundle-SymbaticName deve ser um nome de pacote exclusivo e totalmente qualificado.

Você pode criá-lo usando uma ferramenta como maven ou criar manualmente um arquivo jar com o cabeçalho relevante definido como mostrado nesta seção.

#### Visualizações da barra de ferramentas do portlet {#portlet-toolbar-views}

A barra de ferramentas do portlet tem basicamente dois estados de visualização. Cada visualização e botões associados podem ser personalizados com um arquivo HTML respectivo.

#### Visualização de publicação {#publish-view}

A visualização de publicação tem apenas um botão que alterna a barra de ferramentas para Gerenciar visualização. A visualização publish é representada pelo arquivo publish.html no pacote [anterior](/help/sites-deploying/configuring-osgi.md#bundles). No HTML, você pode usar os seguintes espaços reservados, que são substituídos pelo portlet pelo respectivo conteúdo quando renderizados:

#### Marcadores de posição da Visualização de publicação {#publish-view-placeholders}

| String de espaço reservado | Descrição |
|---|---|
| {buttonManage} | O espaço reservado é substituído pelo botão **Gerenciar** , que alterna o estado do portlet para o estado de gerenciamento. |

#### Gerenciar Visualização {#manage-view}

A visualização manage tem quatro botões: Editar, guia Sites, Atualizar e Voltar. A visualização manage é representada pelo arquivo manage.html no pacote [anterior](/help/sites-deploying/configuring-osgi.md#bundles). No HTML, você pode usar os seguintes espaços reservados, que são substituídos pelo portlet pelo respectivo conteúdo quando renderizados:

#### Gerenciar marcadores de posição de Visualização {#manage-view-placeholders}

| String de espaço reservado | Descrição |
|---|---|
| {buttonEdit} | O espaço reservado é substituído pelo botão **Editar** , que abre uma nova janela com a página atual no modo de edição do AEM. |
| {guia Websites} | Marcador de posição, substituído por um botão que abre a guia Sites do WCM AEM. |
| {buttonRefresh} | Atualiza a visualização atual. |
| {buttonBack} | Alterna o portlet de volta para a visualização de publicação. |

#### Botões {#buttons}

Os botões, em qualquer visualização que eles aparecerem, usam o mesmo HTML comum, definido em button.html.

No HTML, você pode usar os seguintes espaços reservados, que são substituídos pelo portlet pelo respectivo conteúdo quando renderizados:

#### Botões Gerenciar e publicar Visualização {#manage-and-publish-view-buttons}

| String de espaço reservado | Descrição |
|---|---|
| {name} | Nome do botão, por exemplo, autor**, voltar, atualizar** e assim por diante. |
| {id} | ID CSS do botão. |
| {url} | URL do público alvo do botão. |
| {texto} | Rótulo do botão. |
| {onclick} | Função **onclick** do Javascript (contém {url}). |

Exemplo de um arquivo button.html:

```xml
<div class="cqp_button">

 <a href="#" onclick="{onclick}">

 <img src="/wps/PA_CQ5_Portlet/cqbridge/static/{id}.gif" alt="{text}"
title="{text}"/>

 </a>
</div>
```

#### Instalação de um layout personalizado {#installing-a-custom-layout}

Para instalar um layout personalizado, acesse a seção **Bundles **Bundles ** do console OSGI Web do portlet e faça upload do pacote.

#### Pacotes {#packages}

Se precisar carregar ou criar pacotes para sua instalação, consulte Gerenciador de pacotes na documentação do AEM para obter instruções detalhadas.

### Manuseio de link {#link-handling}

Todos os links são regravados para funcionarem no contexto do portal. Por padrão, links com parâmetros de renderização são usados. O redator HTML do Diretor do Portal pode ser configurado para usar links de ação.

Você também pode definir parâmetros de solicitação adicionais a serem consultados para que o caminho do conteúdo seja exibido. Isso é útil, por exemplo, se houver um link do lado de fora para um conteúdo específico.

Além disso, o Portal Diretor HTML Rewriter pode ser configurado com uma lista de expressões regulares definidas como excluídas para regravação de links. Por exemplo, se você tiver links relativos a sistemas externos, deverá adicioná-los a essa lista de exclusão.

### Localização {#localization}

O portlet de conteúdo do AEM tem um recurso de localização incorporado, que garante que o conteúdo do AEM esteja no idioma correto.

Isso é feito em duas etapas:

1. O Detector de Localidade do Diretório de Portal detecta a localidade do usuário do portal obtendo a configuração de localidade do portal. Esse serviço deve ser configurado com a lista de idiomas disponíveis no AEM.
1. O Manipulador de Localidade do Diretor do Portal lida com a localização da solicitação atual. Ele segue o caminho do conteúdo solicitado, por exemplo, `/content/geometrixx/en/company.html`e, de acordo com a configuração, reescreve a **en** com a localidade real do usuário.

O Manipulador de Localidade do Diretor do Portal pode ser configurado com os caminhos para verificar as informações de localidade - normalmente isso inclui tudo sob `/content` e com a posição das informações de localidade no caminho. Por padrão, o manipulador de localidades segue a recomendação de estruturar sites de vários idiomas no AEM.

Se o site não tiver uma regra estrita para lidar com as informações de localidade dentro do caminho, será possível substituir o manipulador de localidades pela sua própria implementação.

### Serviços OSGi opcionais {#optional-osgi-services}

Os serviços OSGi opcionais podem ser implementados para personalizar várias partes do portlet. Cada serviço corresponde a uma interface Java. Essa interface pode ser implementada e implantada por meio de um pacote no portlet.

<table>
 <tbody>
  <tr>
   <td>RequestTracker</td>
   <td>O rastreador de solicitações é notificado sempre que o conteúdo é exibido pelo portlet. Isso permite rastrear as invocações do portlet.</td>
  </tr>
  <tr>
   <td>InvocationContextListener</td>
   <td>Ouvinte que é chamado no início e no fim de cada solicitação para o portlet. O ouvinte pode ser usado para alterar ou adicionar informações para a solicitação atual.<br /> </td>
  </tr>
  <tr>
   <td>ErrorHandler</td>
   <td>Manipulador de erros personalizado para erros durante a fase de renderização.</td>
  </tr>
  <tr>
   <td>HttpProcessor</td>
   <td>Esse serviço pode ser usado para adicionar informações a cada invocação http ao AEM.</td>
  </tr>
  <tr>
   <td>PortletAction</td>
   <td>Adicionar uma ação própria ao portlet - essa ação pode ser invocada por meio de um link de ação do portlet.</td>
  </tr>
  <tr>
   <td>PortletDecoratorService</td>
   <td>Este serviço pode ser usado para decorar o conteúdo do portlet.</td>
  </tr>
  <tr>
   <td>ResourceProvider</td>
   <td>Adicione seu próprio provedor de recursos para fornecer algum recurso por meio de um link de recurso de portlet para o cliente.</td>
  </tr>
  <tr>
   <td>TextMapper</td>
   <td>Permite que você publique arquivos HTML, CSS e Javascript de processo.</td>
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

Os seguintes serviços têm uma implementação padrão no portlet de conteúdo (com uma interface Java correspondente). Para personalizar, é necessário implantar um pacote contendo a nova implementação do serviço no aplicativo portlet.

Ao implementar tal serviço, certifique-se de definir a propriedade **service.ranking** do serviço com um valor positivo. A implementação padrão usa a classificação** 0** e o portlet usa o serviço com a classificação mais alta.

| **Nome** | **Descrição** | **Comportamento padrão** |
|---|---|---|
| Autenticador | Fornece as informações de autenticação ao AEM | Usa um usuário técnico configurável para autor e publicação. Ou SSO pode ser usado. |
| HTMLRewriter | Substitui links, imagens etc. | Substitui links do AEM por links de portal, que podem ser estendidos por um UrlMapper e um TextMapper |
| HttpClientService | Trata de todas as conexões http | Implementação padrão |
| LocaleHandler | Processa as informações da localidade | Substitui um link do conteúdo em relação à localidade. |
| LocaleDetector | Detecta a localidade do usuário. | Usa a localidade fornecida pelo portal. |
| PrivilegeManager | Verifica os direitos do usuário | Verifica o acesso à instância do autor se o usuário tem permissão para editar conteúdo |
| ToolbarRenderer | Renderiza a barra de ferramentas | Adiciona uma funcionalidade da barra de ferramentas |

### Eventos de portlet {#portlet-events}

A API de portlet (JSR-286) especifica eventos de portlet. O portlet de conteúdo AEM tem uma ponte integrada, distribuindo eventos de portlet para o portlet AEM como eventos OSGi - isso torna possível o manuseio de eventos de portlet.

Se você quiser lidar com eventos específicos, declare-os como eventos de recebimento no descritor de deployment (ou configure-os pelo servidor de portal) e implemente um serviço OSGi declarando a interface EventHandler (consulte a especificação OSGi EventAdmin).

Sempre que um evento de portlet ocorrer, um evento OSGi específico será enviado chamando seu manipulador. O manipulador obtém todas as informações de contexto e pode atualizar o status do portlet de acordo ou enviar novos eventos. Basicamente, dentro do método de identificação, toda a funcionalidade da fase de evento do portlet pode ser usada.

## Usar o AEM como portal {#using-aem-as-a-portal}

Use o componente Portlet para adicionar janelas de portlet a páginas AEM. As bibliotecas compartilhadas que você instala no servidor de aplicativos permitem que o componente Portlet detecte aplicativos de portlet implantados.

Para usar o AEM como portal, execute as seguintes tarefas:

1. Instale o componente Portlet e as bibliotecas compartilhadas.
1. Adicione o componente Portlet ao Sidekick.
1. Configure e implante o aplicativo da Web que contém os portlets que você deseja que apareçam no componente Portal.
1. Adicione o componente Portlet a uma página e selecione o portlet a ser exibido.

>[!NOTE]
>
>Você pode usar o componente portlet somente quando o AEM for implantado como um aplicativo da Web. ([Consulte Instalação do AEM com um servidor](/help/sites-deploying/application-server-install.md)de aplicativos.)

### Instalação do componente portlet {#installing-the-portlet-component}

O arquivo JAR de Início rápido do AEM contém os arquivos de componente do portlet. Para obter os arquivos (cq-portlet-components.zip), você pode executar o Início rápido ou extrair o conteúdo.

1. Execute ou extraia o conteúdo do arquivo JAR do Quickstart e localize o arquivo cq-portlet-components.zip de acordo:

   * Executar Início Rápido: crx-quickstart/opt/portal
   * Extrair conteúdo do Início Rápido: estático/opcional/portal

1. Abra o Gerenciador de pacotes da instância do autor do CQ5 que é implantada no servidor de aplicativos. (https://*appserverhost*:*port*/cq5author/crx/packmgr)

1. Use o Gerenciador de pacotes para [carregar e instalar](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) o pacote cq-portlets-components.zip.

   O pacote instala o cq-portlet-diretor-sharing-libs-x.x.x.jar na pasta /libs/portal/diretor no repositório.

1. Copie cq-portlet-diretor-sharing-libs-x.x.x.jar para o disco rígido. Use qualquer meio para obter o arquivo, por exemplo, FileVault ou um cliente WebDAV.
1. Mova o arquivo cq-portlet-diretor-sharing.x.x.x.jar para a pasta da biblioteca compartilhada do servidor de aplicativos para que as classes fiquem disponíveis para aplicativos de portlet implantados.

### Adicionar o componente Portlet ao Sidekick {#adding-the-portlet-component-to-sidekick}

Adicione o componente portlet ao sistema de parágrafo para que ele esteja disponível aos autores.

1. No Sidekick, clique no ícone de régua para entrar no modo Design.
1. Ao lado do `Design of par` cabeçalho acima do primeiro parágrafo, clique em **Editar**.

1. Na categoria **Geral** do componente, marque a caixa de seleção ao lado do componente Portlet e clique em OK.

![chlimage_1-25](assets/chlimage_1-25.jpeg)

### Configuração e implantação de aplicativos portlet {#configuring-and-deploying-your-portlet-applications}

Implante os portlets no container da Web do servidor de aplicativos para que eles fiquem disponíveis para o componente Portal. Antes de implantar o aplicativo portlet, é necessário configurar o aplicativo para que ele carregue o servlet de container do portal AEM. Essa configuração permite que o componente Portlet acesse os portlets.

1. Extraia o conteúdo do arquivo WAR do aplicativo portlet.

   **Dica:** O comando jar xf *name*.war extrai os arquivos.

1. Abra o arquivo web.xml em um editor de texto.
1. Adicione a seguinte configuração de servlet dentro do elemento de aplicativo da Web:

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

   **Dica:** O `jar cvf nameofapp.war *` comando adiciona o conteúdo do diretório atual ao nome do arquivo ofapp.war.

1. Implante o aplicativo portlet no servidor de aplicativos. Para obter informações, consulte a documentação do servidor de aplicativos.

### Adicionar portlets à sua página do AEM {#adding-portlets-to-your-aem-page}

Use o componente Portal para adicionar uma janela de portlet à sua página da Web. Use as propriedades do componente para especificar o portlet a ser exibido.

1. Na página da Web, arraste o componente **Portlet** do grupo Geral no Sidekick para a página.

   >[!NOTE]
   >
   >Depois de arrastar o componente para a página, recarregue-a para garantir que funcione corretamente.

1. Clique no componente com o Duplo do mouse para abrir as propriedades do Portlet.
1. No menu suspenso **Portlet Entity (Entidade** do portlet), selecione o portlet na lista.
1. Marque ou desmarque a caixa de seleção **Ocultar barra de título **dependendo se deseja ver a barra de título do portlet.
1. No campo Janela **do** portlet, informe uma ID exclusiva da janela do portlet, se desejar.

   >[!NOTE]
   >
   >Se você planeja usar o mesmo portlet mais de uma vez na mesma página, forneça a cada portlet uma ID de janela diferente.

1. Clique em **OK**. O portlet é exibido na página do AEM.

   ![chlimage_1-136](assets/chlimage_1-136.png)

## Instalação, configuração e uso do AEM em um portlet {#installing-configuring-and-using-aem-in-a-portlet}

Para acessar o conteúdo fornecido pelo WCM AEM, o servidor de portal precisa estar equipado com o portlet do diretor do portal do AEM. Para fazer isso, instale, configure e adicione o portlet à página do portal usando as etapas fornecidas nesta seção.

Por padrão, o portlet se conecta à instância de publicação em localhost:4503 e à instância do autor em localhost:4502. Esses valores podem ser alterados durante a implantação do portlet. O diretor do portal está disponível como conteúdo no repositório em /libs/portal/diretory. Você precisará baixar o arquivo de guerra do aplicativo antes de usá-lo.

### Download do arquivo de guerra {#downloading-the-war-file}

1. Usando o Webdav ou o CRXDE Lite, navegue até /libs/portal/diretor.

1. Baixe *cq-portlet-webapp.war*.

>[!NOTE]
>
>Estes procedimentos utilizam como exemplo o portal Webphere, embora sejam o mais genéricos possível; saiba que os procedimentos variam para outros portais da Web. Embora as etapas sejam essencialmente idênticas para todos os portais da Web, é necessário redefinir as etapas do portal da Web específico.

#### Instalação do portlet {#installing-the-portlet}

Para instalar o portlet:

1. Faça logon no portal com privilégios de administrador.
1. Navegue até a parte Gerenciamento de Portlet do portal da Web.
1. Clique em Instalar e navegue até o aplicativo portlet AEM (cq-portlet-webapp.war) que você baixou e insira outras informações importantes sobre o portlet.

   Para outras informações essenciais do portlet, você pode aceitar os padrões ou alterar os valores. Se você aceitar os valores padrão, o portlet estará disponível em https://&lt;wps-host>:&lt;porta>/wps/PA_CQ5_Portlet. O console de administração OSGi fornecido pelo portlet está disponível em https://&lt;wps-host>:&lt;porta>/wps/ PA_CQ5_Portlet/cqbridge/system/console (o nome de usuário/senha padrão é admin/admin).

1. Certifique-se de que o aplicativo portlet seja automaticamente start selecionando essa opção ou caixa de seleção e salvando suas alterações. Você verá uma mensagem informando que sua instalação foi bem-sucedida.

#### Configuração do portlet {#configuring-the-portlet}

Depois de instalar o portlet, é necessário configurá-lo para que ele saiba os URLs das instâncias subjacentes do AEM (autor e publicação). Você também pode configurar outras opções.

Para configurar o portlet:

1. Na janela Administração do portal do servidor de aplicativos, navegue até o gerenciamento de portlets, onde todos os portlets estão listados, e selecione o portlet do AEM Portal Diretor.
1. Configure o portlet, conforme necessário. Por exemplo, talvez seja necessário alterar o URL das instâncias de autor e publicação e o URL do caminho do start. As configurações padrão são descritas em Preferências [](/help/sites-administering/aem-as-portal.md#portlet-preferences)de portlet.

   >[!NOTE]
   >
   >Se o portlet estiver configurado para conectar-se ao autor do AEM e publicar instâncias que estejam sendo executadas em um caminho de contexto diferente de** /**, você precisará ativar o **CQUrlInfo** na configuração do Html Library Manager dessas instâncias do AEM (por exemplo, via console do Web do Felix) ou a edição não funcionará e a caixa de diálogo de preferências não aparecerá.

1. Salve as alterações de configuração no servidor de aplicativos.

1. Navegue até o console de administração OSGI para o portlet. O local padrão é `https://<wps-host>:<port>/wps/PA_CQ5_Portlet/cqbridge/system/console/configMgr`. O nome de usuário/senha padrão é **admin/admin**.

1. Selecione a configuração **do servidor CQ do Diretor do Portal do** Dia e edite os seguintes valores:

   * **URL** básico do autor: O URL base da instância do autor de AEM.
   * **URL** base de publicação: O URL base da instância de publicação do AEM.
   * **Autor É Usado Como Publicação**: A instância do autor é usada como uma instância de publicação (para desenvolvimento)?
   ![chlimage_1-137](assets/chlimage_1-137.png)

1. Clique em **Salvar**. Agora você pode adicionar o portlet às páginas do portal e usar o portal.

### URLs de conteúdo {#content-urls}

Quando o conteúdo é solicitado do AEM, o portlet usa o modo de exibição atual (publicar ou criar) e o caminho atual para montar um URL completo. Com os valores padrão, o primeiro url é `https://localhost:4503/content/geometrixx/en.portlet.html`. O valor da extensão `htmlSelector` é automaticamente adicionado ao URL antes da extensão.

Se o portlet alternar para o modo de ajuda e o `appendHelpViewModeAsSelector` for selecionado, o `help` seletor também será anexado, por exemplo, `https://localhost:4503/content/geometrixx/en.portlet.html.help`. Se a janela do portlet estiver maximizada e a opção `appendMaxWindowStateAsSelector` estiver selecionada, o seletor também será anexado, por exemplo, `https://localhost:4503/content/geometrixx/en.portlet.max.help`.

Os seletores podem ser avaliados no AEM e um modelo diferente pode ser usado para seletores diferentes.

### Usar um Mapa de URL de conteúdo no AEM {#using-a-content-url-map-in-aem}

Normalmente, o caminho do start aponta diretamente para o conteúdo no AEM. Entretanto, se você quiser manter os caminhos do start no AEM em vez de nas preferências do portlet, é possível apontar o caminho do start para um mapa de conteúdo no AEM, como `/var/portlets`. Nesse caso, um script em execução no AEM pode usar as informações enviadas do portlet para decidir qual url é o URL do start. Ele deve emitir um redirecionamento para o URL correto.

#### Adicionar o portlet à página do portal {#adding-the-portlet-to-the-portal-page}

Para adicionar o portlet à página do portal:

1. Certifique-se de estar na janela de administração do servidor de aplicativos e navegue até o local onde você gerencia as páginas. (por exemplo, no WebSphere 6.1, clique em **Gerenciar páginas**).
1. Selecione o nome do portlet e selecione uma página existente ou crie uma nova página.
1. Edite o layout da página.
1. Selecione o portlet e adicione-o a um container.
1. Salve as alterações.

#### Uso do portlet {#using-the-portlet}

Para acessar a página adicionada ao portlet:

1. No menu de personalização do portlet, configure o portlet conforme você o configurou no portal.
1. Abra a configuração (o portlet exibe o URL do start de publicação configurado na configuração do portlet), faça as edições necessárias e, em seguida, salve-as.

