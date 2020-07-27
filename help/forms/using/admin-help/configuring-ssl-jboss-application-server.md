---
title: Configuração do SSL para JBoss Application Server
seo-title: Configuração do SSL para JBoss Application Server
description: Saiba como configurar o SSL para o JBoss Application Server.
seo-description: Saiba como configurar o SSL para o JBoss Application Server.
uuid: 7c13cf00-ea89-4894-a4fc-aaeec7ae9f66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c187daa4-41b7-47dc-9669-d7120850cafd
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---


# Configuração do SSL para JBoss Application Server {#configuring-ssl-for-jboss-application-server}

Para configurar o SSL no JBoss Application Server, você precisa de uma credencial SSL para autenticação. Você pode usar a ferramenta-chave Java para criar uma credencial ou solicitar e importar uma credencial de uma autoridade de certificação (CA). Em seguida, você deve ativar o SSL no JBoss.

Você pode executar keytool usando um único comando que inclui todas as informações necessárias para criar o keystore.

Neste procedimento:

* `[appserver root]` é o diretório inicial do servidor de aplicativos que executa formulários AEM.
* `[type]` é um nome de pasta que varia, dependendo do tipo de instalação executada.

## Criar uma credencial SSL {#create-an-ssl-credential}

1. Em um prompt de comando, navegue até *[JAVA HOME]*/bin e digite o seguinte comando para criar a credencial e o keystore:

   `keytool -genkey -dname "CN=`*Nome *do host Nome`, OU=`*do* grupo Nome `, O=`*da *Empresa Nome`,L=`*da* cidade Nome `, S=`*do *estado`, C=`Código do`-alias "AEMForms Cert"``-keyalg RSA -keypass`** `-keystore`*país&quot;key_passwordkeystorename *`.keystore`

   >[!NOTE]
   >
   >Substitua `[JAVA_HOME]` pelo diretório onde o JDK está instalado e substitua o texto em itálico por valores que correspondam ao seu ambiente. Nome do host é o nome de domínio totalmente qualificado do servidor de aplicativos.

1. Digite a senha `keystore_password` quando solicitado. A senha para o armazenamento de chaves e a chave deve ser idêntica.

   >[!NOTE]
   >
   >A `keystore_password` *digitada nesta etapa pode ser a mesma senha (key_password) que você digitou na etapa 1 ou pode ser diferente.*

1. Copie o *keystorename*.keystore para o `[appserver root]/server/[type]/conf` diretório digitando um dos seguintes comandos:

   * (Windows Single Server) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * Cópia (Cluster do Windows Server) `keystorename.keystore[appserver root]\domain\configuration`
   * (Servidor único Linux) `cp keystorename.keystore [appserver root]/standalone/configuration`
   * (Cluster do servidor Linux) `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. Exporte o arquivo de certificado digitando o seguinte comando:

   * (Servidor único) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * (Cluster do Servidor) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. Digite *keystore_password* quando solicitado a fornecer uma senha.
1. Copie o arquivo AEMForms_cert.cer para o diretório raiz *[\conf]do *appserver digitando o seguinte comando:

   * (Windows Single Server) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * (Cluster do Windows Server) `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * (Servidor único Linux) `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * (Cluster do servidor Linux) `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. Visualização o conteúdo do certificado digitando o seguinte comando:

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. Para fornecer acesso de gravação ao arquivo cacerts em `[JAVA_HOME]\jre\lib\security`, se necessário, execute a seguinte tarefa:

   * (Windows) Clique com o botão direito do mouse no arquivo cacerts, selecione Propriedades e desmarque o atributo Somente leitura.
   * (Linux) Tipo `chmod 777 cacerts`

1. Importe o certificado digitando o seguinte comando:

   `keytool -import -alias “AEMForms Cert” -file`*AEMForms_cert *`.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. Digite `changeit` como a senha. Esta senha é a senha padrão para uma instalação Java e pode ter sido alterada pelo administrador do sistema.
1. Quando solicitado para `Trust this certificate? [no]`:, digite `yes`. A confirmação &quot;Certificado adicionado ao keystore&quot; é exibida.
1. Se você estiver se conectando por SSL do Workbench, instale o certificado no computador do Workbench.
1. Em um editor de texto, abra os seguintes arquivos para edição:

   * Servidor único - `[appserver root]`/independente/configuration/lc_&lt;dbname/turnkey>.xml

   * Cluster do servidor - `[appserver root]`/domain/configuration/host.xml

   * Cluster do servidor - `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **Para um único servidor,** no arquivo lc_&lt;dbaname/tunkey>.xml, adicione o seguinte após a seção &lt;security-realms>:

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   Localize a `<server>` seção presente depois do seguinte código:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Adicione o seguinte à seção &lt;server> presente depois do código acima:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **Para o cluster de servidores,** na raiz [\domain\configuration\host.xml do]appserver em todos os nós, adicione o seguinte após a seção &lt;security-realms>:

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   No nó primário do Cluster do Servidor, na raiz [\domain\configuration\domain_&lt;dbname>.xml do]appserver, localize a seção &lt;server> presente após o seguinte código:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Adicione o seguinte à seção &lt;server> presente depois do código acima:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. Altere o valor do `keystoreFile` atributo e o `keystorePass` atributo para a senha do armazenamento de chaves que você especificou ao criar o armazenamento de chaves.
1. Reinicie o servidor de aplicativos:

   * Para instalações chave na mão:

      * No Painel de controle do Campaign do Windows, clique em Ferramentas administrativas e em Serviços.
      * Selecione JBoss para formulários Adobe Experience Manager.
      * Selecione Ação > Parar.
      * Aguarde até que o status do serviço seja exibido como interrompido.
      * Selecione Ação > Start.
   * Para instalações JBoss pré-configuradas ou configuradas manualmente da Adobe:

      * Em um prompt de comando, navegue até *`[appserver root]`*/bin.
      * Pare o servidor inserindo o seguinte comando:

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * Aguarde até que o processo JBoss tenha sido completamente desligado (quando o processo JBoss retornar o controle ao terminal em que foi iniciado).
      * Start o servidor inserindo o seguinte comando:

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. Para acessar o console de administração usando SSL, digite `https://[host name]:'port'/adminui` em um navegador da Web:

   A porta SSL padrão para JBoss é 8443. Aqui em diante, especifique essa porta ao acessar formulários AEM.

## Solicitar uma credencial de uma CA {#request-a-credential-from-a-ca}

1. Em um prompt de comando, navegue até *[JAVA HOME]*/bin e digite o seguinte comando para criar o keystore e a tecla:

   `keytool -genkey -dname "CN=`*Nome *do host Nome`, OU=`*do* grupo Nome `, O=`*da *Empresa Nome`, L=`*da* cidade Nome `, S=`*do *estado`, C=`*do host Código* do `-alias "AEMForms Cert"` `-keyalg RSA -keypass`** `-keystore`*país&quot; -País_chave senhakeystorename *`.keystore`

   >[!NOTE]
   >
   >Substitua *`[JAVA_HOME]`* pelo diretório onde o JDK está instalado e substitua o texto em itálico por valores que correspondam ao seu ambiente.

1. Digite o seguinte comando para gerar uma solicitação de certificado para enviar à autoridade de certificação:

   `keytool -certreq -alias` &quot;AEMForms Cert&quot; `-keystore`*keystorename *`.keystore -file`*AEMFormscertRequest.csr*

1. Quando sua solicitação de um arquivo de certificado for atendida, conclua o procedimento seguinte.

## Usar uma credencial obtida de uma CA para habilitar o SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. Em um prompt de comando, navegue até *`[JAVA HOME]`*/bin e digite o seguinte comando para importar o certificado raiz da CA com a qual o CSR foi assinado:

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   Se o certificado raiz não estiver no navegador, importe-o também para lá.

   >[!NOTE]
   >
   >Substitua *`[JAVA_HOME]`pelo diretório onde o JDK está instalado e substitua o texto em itálico por valores que correspondam ao seu ambiente.*

1. Em um prompt de comando, navegue até *`[JAVA HOME]`*/bin e digite o seguinte comando para importar a credencial para o keystore:

   `keytool -import -trustcacerts -file`*CACertificateName *`.crt -keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >* Substitua `[JAVA_HOME]` pelo diretório onde o JDK está instalado e substitua o texto em itálico por valores que correspondam ao seu ambiente.
   >* O certificado assinado da CA importado substituirá um certificado público autoassinado se ele existir.


1. Complete as etapas 13 - 18 de Criar uma credencial SSL.
