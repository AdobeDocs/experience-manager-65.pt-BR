---
title: Instalação do servidor de aplicativos
seo-title: Instalação do servidor de aplicativos
description: Saiba como instalar AEM com um servidor de aplicativos.
seo-description: Saiba como instalar AEM com um servidor de aplicativos.
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
translation-type: tm+mt
source-git-commit: 0a082d3cff66b82ef6de551a735a16a001446a1e
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 1%

---


# Instalação do servidor de aplicativos{#application-server-install}

>[!NOTE]
>
>`JAR` e `WAR` são os tipos de arquivos AEM são lançados. Esses formatos estão passando por uma garantia de qualidade para acomodar os níveis de suporte que a Adobe comprometeu.


Esta seção informa como instalar o Adobe Experience Manager (AEM) com um servidor de aplicativos. Consulte a seção Plataformas [](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) suportadas para ver os níveis de suporte específicos fornecidos para os servidores de aplicativos individuais.

As etapas de instalação dos seguintes Servidores de aplicativos estão descritas:

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

Consulte a documentação apropriada do servidor de aplicativos para obter mais informações sobre como instalar aplicativos da Web, configurações do servidor e como start e parar o servidor.

>[!NOTE]
>
>Se você estiver usando o Dynamic Media em uma implantação WAR, consulte a documentação [do](/help/assets/config-dynamic.md#enabling-dynamic-media)Dynamic Media.

## Descrição geral {#general-description}

### Comportamento padrão ao instalar AEM em um Servidor de aplicativos {#default-behaviour-when-installing-aem-in-an-application-server}

AEM vem como um único arquivo de guerra para implantar.

Se implantado, o seguinte ocorrerá por padrão:

* o modo de execução é `author`
* a instância (Repository, Felix OSGI ambiente, pacotes etc.) está instalado no `${user.dir}/crx-quickstart`local em que `${user.dir}` está o diretório de trabalho atual, este caminho para crx-quickstart é chamado `sling.home`

* a raiz de contexto é o nome do arquivo de guerra, por exemplo: `aem-6`

#### Configuração {#configuration}

Você pode alterar o comportamento padrão da seguinte maneira:

* modo de execução : configure o `sling.run.modes` `WEB-INF/web.xml` parâmetro no arquivo do arquivo de guerra AEM antes da implantação

* sling.home: configure o `sling.home` parâmetro no `WEB-INF/web.xml`arquivo do arquivo AEM war antes da implantação

* raiz de contexto: renomear o arquivo AEM war

#### Publicar instalação {#publish-installation}

Para obter uma instância de publicação implantada, é necessário definir o modo de execução para publicar:

* Desempacotar o WEB-INF/web.xml do arquivo de guerra AEM
* Alterar o parâmetro sling.run.mode para publicar
* Reempacotar o arquivo web.xml em AEM arquivo de guerra
* Implantar AEM arquivo de guerra

#### Verificação da instalação {#installation-check}

Para verificar se tudo está instalado, você pode:

* exclua o `error.log`arquivo para ver se todo o conteúdo está instalado
* verifique se todos os pacotes estão instalados `/system/console`

#### Duas instâncias no mesmo servidor de aplicativos {#two-instances-on-the-same-application-server}

Para fins de demonstração, pode ser apropriado instalar o autor e publicar a instância em um servidor de aplicativos. Para isso, faça o seguinte:

1. Altere as variáveis sling.home e sling.run.mode da instância de publicação.
1. Descompacte o arquivo WEB-INF/web.xml do arquivo AEM war.
1. Altere o parâmetro sling.home para um caminho diferente (caminhos absolutos e relativos são possíveis).
1. Altere sling.run.mode para publicar para a instância de publicação.
1. Reempacotar o arquivo web.xml.
1. Renomeie os arquivos de guerra para que eles tenham nomes diferentes: Por exemplo, uma renomeia para aemauthor.war e a outra para aempublish.war.
1. Use configurações de memória mais altas, por exemplo, para instâncias de AEM padrão, use, por exemplo: -Xmx3072m
1. Implante os dois aplicativos da Web.
1. Após a implantação, pare os dois aplicativos da Web.
1. Nas instâncias de autor e publicação, verifique se nos arquivos sling.properties a propriedade felix.service.urlhandlers=false está definida como false (o padrão é que ela esteja definida como true).
1. Start os dois aplicativos da Web novamente.

## Procedimentos de instalação dos servidores de aplicativos {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

Antes de uma implantação, leia a Descrição [](#general-description) geral acima.

**Preparação do servidor**

* Deixe que os Cabeçalhos básicos de autenticação passem por:

   * Uma maneira de permitir que AEM autenticem um usuário é desabilitar a segurança administrativa global do servidor WebSphere, para fazer isso: vá para Segurança -> Segurança global e desmarque a caixa de seleção Ativar segurança administrativa, salve e reinicie o servidor.

* set `"JAVA_OPTS= -Xmx2048m"`
* Se você quiser instalar AEM usando a raiz de contexto = /, primeiro é necessário alterar a raiz de contexto do aplicativo Web padrão existente

**Implantar AEM aplicativo da Web**

* Baixar AEM arquivo de guerra
* Faça suas configurações em web.xml, se necessário (consulte acima na Descrição geral)

   * Desempacotar arquivo WEB-INF/web.xml
   * alterar o parâmetro sling.run.mode para publicar
   * exclua o comentário do parâmetro inicial sling.home e defina esse caminho conforme necessário
   * Repack arquivo web.xml

* Implantar AEM arquivo de guerra

   * Escolha uma raiz de contexto (se desejar definir os modos de execução de sling, você precisa selecionar as etapas detalhadas do assistente de implantação e, em seguida, especificá-la na etapa 6 do assistente)

* Start AEM aplicação Web

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

Antes de uma implantação, leia a Descrição [](#general-description) geral acima.

**Preparar servidor JBoss**

Defina os argumentos da memória no arquivo conf (por exemplo, `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

se você usar o deployment-scanner para instalar o aplicativo da Web AEM, talvez seja bom aumentar o valor `deployment-timeout,` desse conjunto de um `deployment-timeout` atributo no arquivo xml da sua instância (por exemplo `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**Implantar AEM aplicativo da Web**

* Carregue o aplicativo da Web AEM no console de administração do JBoss.

* Ative o aplicativo da Web AEM.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

Antes de uma implantação, leia a Descrição [](#general-description) geral acima.

Isso usa um layout de servidor simples com apenas um servidor de administração.

**Preparação do WebLogic Server**

* Em `${myDomain}/config/config.xml`adicionar à seção de configuração de segurança:

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` consulte em [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) para obter a posição correta (por padrão, para posicioná-la no final da seção está ok)

* Aumente as configurações de memória da VM:

   * open `${myDomain}/bin/setDomainEnv.cmd` (resp.sh)search for WLS_MEM_ARGS, defina por exemplo set `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * reiniciar o WebLogic Server

* Criar em `${myDomain}` uma pasta de pacotes e dentro de uma pasta cq e nela uma pasta Plano

**Implantar AEM aplicativo da Web**

* Baixar AEM arquivo de guerra
* Coloque o arquivo de guerra AEM na pasta ${myDomain}/packages/cq
* Faça com que suas configurações sejam ativadas `WEB-INF/web.xml` (consulte acima na Descrição geral)

   * Desempacotar `WEB-INF/web.xml`arquivo
   * alterar o parâmetro sling.run.mode para publicar
   * exclua o comentário do parâmetro inicial sling.home e defina esse caminho conforme necessário (consulte Descrição geral)
   * Repack arquivo web.xml

* Implantar AEM arquivo de guerra como um aplicativo (para outras configurações, use as configurações padrão)
* A instalação pode demorar...
* Verifique se a instalação terminou conforme mencionado acima na Descrição geral (por exemplo, ajustando o error.log)
* Você pode alterar a raiz de contexto na guia Configuração do aplicativo da Web no WebLogic `/console`

#### Tomcat 8/8.5 {#tomcat}

Antes de uma implantação, leia a Descrição [](#general-description) geral acima.

* **Preparar servidor Tomcat**

   * Aumente as configurações de memória da VM:

      * Em `bin/catalina.bat` (resp `catalina.sh` on unix), adicione a seguinte configuração:
      * `set "JAVA_OPTS= -Xmx2048m`
   * O Tomcat não permite acesso de administrador nem de gerente na instalação. Portanto, é necessário editar manualmente `tomcat-users.xml` para permitir o acesso a essas contas:

      * Edite `tomcat-users.xml` para incluir o acesso do administrador e do gerente. A configuração deve ser semelhante ao seguinte exemplo:

         ```xml
         <?xml version='1.0' encoding='utf-8'?>
         <tomcat-users>
         role rolename="manager"/>
         role rolename="tomcat"/>
         <role rolename="admin"/>
         <role rolename="role1"/>
         <role rolename="manager-gui"/>
         <user username="both" password="tomcat" roles="tomcat,role1"/>
         <user username="tomcat" password="tomcat" roles="tomcat"/>
         <user username="admin" password="admin" roles="admin,manager-gui"/>
         <user username="role1" password="tomcat" roles="role1"/>
         </tomcat-users>
         ```
   * Se você quiser implantar AEM com a raiz de contexto &quot;/&quot;, é necessário alterar a raiz de contexto do aplicativo Web ROOT existente:

      * Parar e desimplantar o aplicativo Web ROOT
      * Renomear pasta ROOT.war na pasta de aplicativos da Web do tomcat
      * Aplicativo Web do start novamente
   * Se você instalar o aplicativo da Web AEM usando o manager-gui, precisará aumentar o tamanho máximo de um arquivo carregado, já que o padrão permite apenas o tamanho de upload de 50 MB. Para isso, abra o web.xml do aplicativo da Web do gerenciador,

      `webapps/manager/WEB-INF/web.xml`

      e aumentar o tamanho máximo de arquivo e o tamanho máximo de solicitação para pelo menos 500 MB, veja o `multipart-config` exemplo a seguir de um arquivo como esse `web.xml` .

      ```xml
      <multipart-config>
      <!-- 500MB max -->
      <max-file-size>524288000</max-file-size>
      <max-request-size>524288000</max-request-size>
      <file-size-threshold>0</file-size-threshold>
      </multipart-config>
      ```




* **Implantar AEM aplicativo da Web**

   * Baixar AEM arquivo de guerra
   * Faça suas configurações em web.xml, se necessário (consulte acima na Descrição geral)

      * Desempacotar arquivo WEB-INF/web.xml
      * alterar o parâmetro sling.run.mode para publicar
      * exclua o comentário do parâmetro inicial sling.home e defina esse caminho conforme necessário
      * Repack arquivo web.xml
   * Renomeie AEM arquivo de guerra para ROOT.war se desejar implantá-lo como aplicativo Web raiz, renomeie-o como, por exemplo, aemauthor.war se desejar que aemauthor seja uma raiz de contexto
   * copie-o para a pasta de aplicativos Web do tomcat
   * aguarde até que AEM esteja instalado


## Resolução de problemas {#troubleshooting}

Para obter informações sobre como lidar com problemas que podem surgir durante a instalação, consulte:

* [Resolução de Problemas](/help/sites-deploying/troubleshooting.md)
