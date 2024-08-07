---
title: Instalação do Servidor de Aplicativos
description: Saiba como instalar o Adobe Experience Manager com um servidor de aplicativos.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 0%

---

# Instalação do Servidor de Aplicativos{#application-server-install}

>[!NOTE]
>
>`JAR` e `WAR` são os tipos de arquivo em que o Adobe Experience Manager (AEM) é lançado. Esses formatos estão passando por controle de qualidade para acomodar os níveis de suporte com os quais o Adobe se comprometeu.
>

Esta seção informa como instalar o Adobe Experience Manager (AEM) com um servidor de aplicativos. Consulte a seção [Plataformas com Suporte](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) para ler sobre os níveis de suporte específicos fornecidos para os servidores de aplicativos individuais.

As etapas de instalação dos seguintes Servidores de Aplicações são descritas:

* [WebSphere](#websphere)
* [JBoss](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

Consulte a documentação apropriada do servidor de aplicativos para obter mais informações sobre a instalação de aplicativos web, configurações do servidor e como iniciar e parar o servidor.

>[!NOTE]
>
>Se você estiver usando o Dynamic Media em uma implantação WAR, consulte [documentação do Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

## Descrição geral {#general-description}

### Comportamento padrão ao instalar o AEM em um servidor de aplicativos {#default-behaviour-when-installing-aem-in-an-application-server}

O AEM vem como um único arquivo WAR a ser implantado.

Se implantado, o seguinte acontece por padrão:

* o modo de execução é `author`
* a instância (Repositório, ambiente Felix OSGI, pacotes, etc.) está instalada em `${user.dir}/crx-quickstart`onde `${user.dir}` é o diretório de trabalho atual, este caminho para crx-quickstart é chamado `sling.home`

* a raiz do contexto é o nome do arquivo war, por exemplo, `aem-6`

#### Configuração {#configuration}

Você pode alterar o comportamento padrão da seguinte maneira:

* modo de execução : configurar o parâmetro `sling.run.modes` no arquivo `WEB-INF/web.xml` do arquivo AEM war antes da implantação

* sling.home: configure o parâmetro `sling.home` no `WEB-INF/web.xml` arquivo do arquivo AEM war antes da implantação

* raiz de contexto: renomear o arquivo AEM war

#### Instalação do Publish {#publish-installation}

Para implantar uma instância de publicação, é necessário definir o modo de execução para publicar:

* Descompacte o WEB-INF/web.xml do arquivo AEM war
* Alterar o parâmetro sling.run.modes para publicar
* Recompacte o arquivo web.xml no arquivo AEM war
* Implantar arquivo AEM war

#### Verificação da instalação {#installation-check}

Para verificar se tudo está instalado, é possível:

* finalizar o arquivo `error.log` para ver se todo o conteúdo está instalado
* verifique em `/system/console` se todos os pacotes estão instalados

#### Duas instâncias no mesmo servidor de aplicativos {#two-instances-on-the-same-application-server}

Para fins de demonstração, pode ser apropriado instalar a instância do autor e da publicação em um servidor de aplicativos. Para isso, faça o seguinte:

1. Altere as variáveis sling.home e sling.run.modes da instância de publicação.
1. Descompacte o arquivo WEB-INF/web.xml do arquivo AEM war.
1. Altere o parâmetro sling.home para um caminho diferente (caminhos absolutos e relativos são possíveis).
1. Altere sling.run.modes para publicar para a instância de publicação.
1. Recompacte o arquivo web.xml.
1. Renomeie os arquivos war para que eles tenham nomes diferentes. Por exemplo, um é renomeado para aemauthor.war e o outro para aempublish.war.
1. Use configurações mais altas de memória. Por exemplo, as instâncias padrão do AEM usam `-Xmx3072m`
1. Implante as duas aplicações web.
1. Após a Implantação, interrompa as duas aplicações Web.
1. Tanto em instâncias de autor quanto de publicação, certifique-se de que, nos arquivos sling.properties, a propriedade felix.service.urlhandlers=false esteja definida como false (o padrão é que ela esteja definida como true).
1. Inicie as duas aplicações web novamente.

## Procedimentos de Instalação de Servidores de Aplicativos {#application-servers-installation-procedures}

### WebSphere® 8.5 {#websphere}

Antes de uma implantação ler a [Descrição Geral](#general-description) acima.

**Preparação do Servidor**

* Permitir a passagem de Cabeçalhos de Autenticação Básicos:

   * Uma maneira de permitir que o AEM autentique um usuário é desabilitar a segurança administrativa global do servidor WebSphere®. Para fazer isso: vá para Security > Global Security e desmarque a caixa de seleção Enable administrative security, salve e reinicie o servidor.

* conjunto `"JAVA_OPTS= -Xmx2048m"`
* Se você deseja instalar o AEM usando raiz de contexto = /, altere a raiz de contexto do Default web application existente.

**Implantar o aplicativo Web AEM**

* Baixar arquivo AEM war
* Faça as configurações em web.xml, se necessário (veja acima a Descrição geral)

   * Descompactar arquivo WEB-INF/web.xml
   * altere o parâmetro sling.run.modes para publish
   * remova o comentário do parâmetro inicial sling.home e defina este caminho conforme necessário
   * Recompactar arquivo web.xml

* Implantar arquivo AEM war

   * Escolha uma raiz de contexto (se quiser definir os modos de execução do sling, selecione as etapas detalhadas do assistente de implantação e especifique na etapa 6 do assistente)

* Iniciar aplicativo web AEM

#### JBoss® EAP 6.3.0/6.4.0 {#jboss-eap}

Antes de uma implantação ler a [Descrição Geral](#general-description) acima.

**Preparar servidor JBoss®**

Definir argumentos de memória no arquivo conf (por exemplo, `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

Se você usar o verificador de implantação para instalar o aplicativo Web AEM, talvez seja bom aumentar o `deployment-timeout,` para que defina um atributo `deployment-timeout` no arquivo xml da sua instância (por exemplo, `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**Implantar o aplicativo Web AEM**

* Faça upload da aplicação web AEM no Console de administração JBoss®.

* Habilite o aplicativo web AEM.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

Antes de uma implantação ler a [Descrição Geral](#general-description) acima.

Usa um layout de servidor simples com apenas um servidor de administração.

**Preparação do WebLogic Server**

* Em `${myDomain}/config/config.xml`adicione à seção de configuração de segurança:

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` consulte em [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) para obter a posição correta (por padrão, posicioná-la no final da seção está ok)

* Aumentar configurações de Memória da VM:

   * abrir a pesquisa `${myDomain}/bin/setDomainEnv.cmd` (resp.sh) de WLS_MEM_ARGS, definir, por exemplo, definir `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * reiniciar o WebLogic Server

* Crie em `${myDomain}` uma pasta de pacotes e dentro de uma pasta cq e, nela, uma pasta Plano

**Implantar o aplicativo Web AEM**

* Baixar arquivo AEM war
* Coloque o arquivo AEM war na pasta ${myDomain}/packages/cq
* Faça suas configurações em `WEB-INF/web.xml`, se necessário (veja acima a Descrição geral)

   * Descompactar `WEB-INF/web.xml` arquivo
   * altere o parâmetro sling.run.modes para publish
   * remova o comentário do parâmetro inicial sling.home e defina este caminho conforme necessário (consulte Descrição geral)
   * Recompactar arquivo web.xml

* Implantar arquivo AEM WAR como um aplicativo (para as outras configurações, use as configurações padrão)
* A instalação pode demorar...
* Verifique se a instalação foi concluída conforme mencionado acima na Descrição geral (por exemplo, seguido do error.log)
* Você pode alterar a raiz do contexto na guia Configuração do aplicativo Web no WebLogic `/console`

#### Tomcat 8/8.5 {#tomcat}

Antes de uma implantação ler a [Descrição Geral](#general-description) acima.

* **Preparar servidor Tomcat**

   * Aumente as configurações de memória da VM:

      * Em `bin/catalina.bat` (resp `catalina.sh` no UNIX®), adicione a seguinte configuração:
      * `set "JAVA_OPTS= -Xmx2048m`

   * O Tomcat não permite o acesso de administrador ou gerente na instalação. Portanto, você precisa editar manualmente o `tomcat-users.xml` para permitir o acesso a estas contas:

      * Edite `tomcat-users.xml` para incluir acesso para administrador e gerente. A configuração deve ser semelhante ao seguinte exemplo:

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

   * Se você gosta de implantar AEM com raiz de contexto &quot;/&quot;, então você tem que alterar a raiz de contexto do aplicativo web RAIZ existente:

      * Parar e desimplantar o aplicativo web ROOT
      * Renomeie a pasta ROOT.war na pasta de aplicativos Web do Tomcat
      * Iniciar o aplicativo Web novamente

   * Se você instalar o aplicativo web AEM usando o manager-gui, será necessário aumentar o tamanho máximo de um arquivo carregado, pois o padrão permite apenas o tamanho de upload de 50 MB. Para isso, abra o web.xml da aplicação Web gerenciadora,

     `webapps/manager/WEB-INF/web.xml`

     e aumente o max-file-size e o max-request-size para pelo menos 500 MB, consulte o seguinte exemplo `multipart-config` desse arquivo `web.xml`.

     ```xml
     <multipart-config>
     <!-- 500MB max -->
     <max-file-size>524288000</max-file-size>
     <max-request-size>524288000</max-request-size>
     <file-size-threshold>0</file-size-threshold>
     </multipart-config>
     ```

* **Implantar o aplicativo Web AEM**

   * Baixe o arquivo AEM war.
   * Faça as configurações em web.xml, se necessário (veja acima na Descrição geral).

      * Descompacte o arquivo WEB-INF/web.xml.
      * Altere o parâmetro sling.run.modes para publish.
      * Remova o comentário do parâmetro inicial sling.home e defina este caminho conforme necessário.
      * Recompacte o arquivo web.xml.

   * Renomeie o arquivo AEM war como ROOT.war se desejar implantá-lo como aplicativo Web raiz. Renomeie-o para aemauthor.war se desejar que o aemauthor seja a raiz de contexto.
   * Copie-o na pasta de aplicativos da Web do Tomcat.
   * Espere até que o AEM seja instalado.

## Resolução de problemas {#troubleshooting}

Para obter informações sobre como lidar com problemas que podem surgir durante a instalação, consulte:

* [Resolução de problemas](/help/sites-deploying/troubleshooting.md)
