---
title: Instalação do servidor de aplicativos
seo-title: Application Server Install
description: Saiba como instalar o AEM com um servidor de aplicativos.
seo-description: Learn how to install AEM with an application server.
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 0%

---

# Instalação do servidor de aplicativos{#application-server-install}

>[!NOTE]
>
>`JAR` e `WAR` são os tipos de arquivo AEM é lançado em. Estes formatos estão a ser objeto de garantia de qualidade para acomodar os níveis de suporte a que o Adobe se comprometeu.

Esta seção informa como instalar o Adobe Experience Manager (AEM) com um servidor de aplicativos. Consulte o [Plataformas compatíveis](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) para ver os níveis de suporte específicos fornecidos para os servidores de aplicativos individuais.

As etapas de instalação dos seguintes Servidores de Aplicativos estão descritas:

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

Consulte a documentação apropriada do servidor de aplicativos para obter mais informações sobre a instalação de aplicativos da Web, configurações do servidor e como iniciar e parar o servidor.

>[!NOTE]
>
>Se você estiver usando o Dynamic Media em uma implantação WAR, consulte o [Documentação do Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

## Descrição geral {#general-description}

### Comportamento padrão ao instalar AEM em um Servidor de Aplicativos {#default-behaviour-when-installing-aem-in-an-application-server}

AEM vem como um único arquivo war para implantar.

Se implantado, o seguinte ocorrerá por padrão:

* o modo de execução é `author`
* a instância (Repositório, ambiente Felix OSGI, pacotes etc.) está instalado no `${user.dir}/crx-quickstart`em que `${user.dir}` é o diretório de trabalho atual, esse caminho para crx-quickstart é chamado `sling.home`

* a raiz de contexto é o nome do arquivo war, por exemplo : `aem-6`

#### Configuração {#configuration}

Você pode alterar o comportamento padrão da seguinte maneira:

* modo de execução : configure o `sling.run.modes` no `WEB-INF/web.xml` arquivo do arquivo war AEM antes da implantação

* sling.home: configure o `sling.home` no `WEB-INF/web.xml`arquivo do arquivo war AEM antes da implantação

* raiz de contexto: renomeie o arquivo AEM war

#### Publicar instalação {#publish-installation}

Para obter uma instância de publicação implantada, é necessário definir o modo de execução para publicar:

* Descompacte o WEB-INF/web.xml do arquivo AEM war
* Alterar o parâmetro sling.run.modes para publicação
* Recompacte o arquivo web.xml em AEM arquivo war
* Implantar AEM arquivo war

#### Verificação da instalação {#installation-check}

Para verificar se tudo está instalado, é possível:

* tail `error.log`para ver que todo o conteúdo está instalado
* examinar `/system/console` que todos os pacotes estão instalados

#### Duas instâncias no mesmo servidor de aplicativos {#two-instances-on-the-same-application-server}

Para fins de demonstração, pode ser apropriado instalar a instância de criação e publicação em um servidor de aplicativos. Para isso, faça o seguinte:

1. Altere as variáveis sling.home e sling.run.modes da instância de publicação.
1. Descompacte o arquivo WEB-INF/web.xml do arquivo AEM war.
1. Altere o parâmetro sling.home para um caminho diferente (caminhos absolutos e relativos são possíveis).
1. Altere sling.run.modes para publicar para a instância de publicação.
1. Recompacte o arquivo web.xml.
1. Renomeie os arquivos war, de modo que eles tenham nomes diferentes: por exemplo, uma renomeação para aemauthor.war e a outra para aempublish.war.
1. Use configurações de memória mais altas, por exemplo, para instâncias de AEM padrão usar, por exemplo: -Xmx3072m
1. Implante as duas aplicações web.
1. Depois da implantação, pare os dois aplicativos Web.
1. Nas instâncias de autor e de publicação, certifique-se de que, nos arquivos sling.properties , a propriedade felix.service.urlhandlers=false está definida como false (o padrão é que esteja definida como true).
1. Inicie as duas aplicações Web novamente.

## Procedimentos de instalação dos servidores de aplicativos {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

Antes de ler a implantação [Descrição geral](#general-description) acima.

**Preparação do servidor**

* Deixe que os cabeçalhos básicos de autenticação passem:

   * Uma maneira de permitir que o AEM autentique um usuário é desabilitar a segurança administrativa global do servidor WebSphere, para fazer isso: acesse Segurança -> Segurança global e desmarque a caixa de seleção Ativar segurança administrativa, salve e reinicie o servidor.

* set `"JAVA_OPTS= -Xmx2048m"`
* Se você quiser instalar AEM usando context root = /, primeiro altere a raiz de contexto do aplicativo Web padrão existente

**Implantar AEM aplicação web**

* Baixar AEM arquivo war
* Faça suas configurações em web.xml se necessário (veja acima na Descrição geral)

   * Descompactar arquivo WEB-INF/web.xml
   * alterar o parâmetro sling.run.modes para publicar
   * exclua o parâmetro inicial sling.home e defina esse caminho conforme necessário
   * Recompacte o arquivo web.xml

* Implantar AEM arquivo war

   * Escolha uma raiz de contexto (se desejar definir os modos de execução do sling, é necessário selecionar as etapas detalhadas do assistente de implantação e especificá-lo na etapa 6 do assistente)

* Iniciar AEM aplicação Web

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

Antes de ler a implantação [Descrição geral](#general-description) acima.

**Preparar o servidor JBoss**

Defina argumentos de memória no seu arquivo conf (por exemplo, `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

se você usar o scanner de implantação para instalar o aplicativo web AEM, talvez seja bom aumentar a variável `deployment-timeout,` para esse conjunto de `deployment-timeout` no arquivo xml da sua instância (por exemplo, `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**Implantar AEM aplicação web**

* Faça upload do aplicativo Web AEM no Console de administração do JBoss.

* Habilite o aplicativo Web AEM.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

Antes de ler a implantação [Descrição geral](#general-description) acima.

Ele usa um layout de servidor simples com apenas um servidor de administração.

**Preparação do WebLogic Server**

* Em `${myDomain}/config/config.xml`adicione à seção configuração de segurança:

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` ver em [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) para a posição correta (por padrão, posicioná-la no final da seção está ok)

* Aumente as configurações de memória da VM:

   * open `${myDomain}/bin/setDomainEnv.cmd` (resp.sh)pesquisar WLS_MEM_ARGS, definir, por exemplo, definir `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * reiniciar o WebLogic Server

* Criar em `${myDomain}` uma pasta de pacotes e dentro de uma pasta cq e nela uma pasta Plan

**Implantar AEM aplicação web**

* Baixar AEM arquivo war
* Coloque o arquivo war AEM na pasta ${myDomain}/packages/cq
* Faça suas configurações em `WEB-INF/web.xml` se necessário (veja acima na Descrição geral)

   * Descompactar `WEB-INF/web.xml`arquivo
   * alterar o parâmetro sling.run.modes para publicar
   * exclua o parâmetro inicial sling.home e defina esse caminho conforme necessário (consulte Descrição geral)
   * Recompacte o arquivo web.xml

* Implantar AEM arquivo war como um Aplicativo (para outras configurações, use as configurações padrão)
* A instalação pode demorar..
* Verifique se a instalação terminou conforme mencionado acima na Descrição geral (por exemplo, acompanhando o error.log)
* Você pode alterar a raiz de contexto na guia Configuração da aplicação Web no WebLogic `/console`

#### Tomcat 8/8.5 {#tomcat}

Antes de ler a implantação [Descrição geral](#general-description) acima.

* **Preparar o servidor Tomcat**

   * Aumente as configurações de memória da VM:

      * Em `bin/catalina.bat` (resp `catalina.sh` no unix) adicione a seguinte configuração:
      * `set "JAVA_OPTS= -Xmx2048m`
   * O Tomcat não ativa o acesso do administrador nem do gerente na instalação. Portanto, é necessário editar manualmente `tomcat-users.xml` para permitir o acesso a estas contas:

      * Editar `tomcat-users.xml` para incluir o acesso do administrador e do gerente. A configuração deve ser semelhante ao seguinte exemplo:

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
   * Se você quiser implantar AEM com a raiz de contexto &quot;/&quot;, será necessário alterar a raiz de contexto do aplicativo Web ROOT existente:

      * Parar e desimplantar o aplicativo web ROOT
      * Renomeie a pasta ROOT.war na pasta webapps do tomcat
      * Iniciar o aplicativo Web novamente
   * Se você instalar o aplicativo Web AEM usando o gerenciador-gui, precisará aumentar o tamanho máximo de um arquivo carregado, já que o padrão permite apenas o tamanho de upload de 50 MB. Para isso, abra o web.xml do aplicativo web gerenciador,

      `webapps/manager/WEB-INF/web.xml`

      e aumente o tamanho máximo do arquivo e o tamanho máximo da solicitação para pelo menos 500 MB, consulte o seguinte `multipart-config` exemplo de uma `web.xml` arquivo.

      ```xml
      <multipart-config>
      <!-- 500MB max -->
      <max-file-size>524288000</max-file-size>
      <max-request-size>524288000</max-request-size>
      <file-size-threshold>0</file-size-threshold>
      </multipart-config>
      ```




* **Implantar AEM aplicação web**

   * Baixar AEM arquivo war
   * Faça suas configurações em web.xml se necessário (veja acima na Descrição geral)

      * Descompactar arquivo WEB-INF/web.xml
      * alterar o parâmetro sling.run.modes para publicar
      * exclua o parâmetro inicial sling.home e defina esse caminho conforme necessário
      * Recompacte o arquivo web.xml
   * Renomeie AEM arquivo war para ROOT.war se desejar implantá-lo como webapp raiz, renomeie-o para aemauthor.war se desejar ter aemauthor como context root
   * copie-o na pasta webapps do tomcat
   * aguarde até que o AEM esteja instalado


## Resolução de problemas {#troubleshooting}

Para obter informações sobre como lidar com problemas que podem surgir durante a instalação, consulte:

* [Resolução de problemas](/help/sites-deploying/troubleshooting.md)
