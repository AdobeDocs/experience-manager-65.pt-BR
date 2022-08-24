---
title: Configuração do SSL para o Servidor de Aplicativos JBoss
seo-title: Configuring SSL for JBoss Application Server
description: Saiba como configurar o SSL para o Servidor de Aplicativos JBoss.
seo-description: Learn how to configure SSL for JBoss Application Server.
uuid: 7c13cf00-ea89-4894-a4fc-aaeec7ae9f66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c187daa4-41b7-47dc-9669-d7120850cafd
exl-id: 8eb4f691-a66b-498e-8114-307221f63718
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 0%

---

# Configuração do SSL para o Servidor de Aplicativos JBoss {#configuring-ssl-for-jboss-application-server}

Para configurar o SSL no JBoss Application Server, você precisa de uma credencial SSL para autenticação. Você pode usar a ferramenta-chave Java para criar uma credencial ou solicitação e importar uma credencial de uma autoridade de certificação (CA). Em seguida, você deve habilitar o SSL no JBoss.

Você pode executar keytool usando um único comando que inclui todas as informações necessárias para criar o keystore.

Neste procedimento:

* `[appserver root]` é o diretório base do servidor de aplicativos que executa AEM formulários.
* `[type]` é um nome de pasta que varia, dependendo do tipo de instalação realizada.

## Criar uma credencial SSL {#create-an-ssl-credential}

1. Em um prompt de comando, navegue até *[PÁGINA INICIAL DO JAVA]*/bin e digite o seguinte comando para criar a credencial e o armazenamento de chaves:

   `keytool -genkey -dname "CN=`*Nome do host* `, OU=`*Nome do grupo* `, O=`*Nome da empresa* `,L=`*Nome da cidade* `, S=`*Estado* `, C=`Código do país&quot; `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >Substituir `[JAVA_HOME]` com o diretório onde o JDK está instalado e substitua o texto em itálico por valores que correspondam ao seu ambiente. Nome do host é o nome de domínio totalmente qualificado do servidor de aplicativos.

1. Insira o `keystore_password` quando solicitado a fornecer uma senha. A senha do armazenamento de chaves e a chave devem ser idênticas.

   >[!NOTE]
   >
   >O `keystore_password` *Inserido nesta etapa pode ser a mesma senha (key_password) inserida na etapa 1, ou pode ser diferente.*

1. Copie o *keystorename*.keystore para o `[appserver root]/server/[type]/conf` digite um dos seguintes comandos:

   * (Windows Single Server) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * Cópia (Cluster do Windows Server) `keystorename.keystore[appserver root]\domain\configuration`
   * (Servidor único Linux) `cp keystorename.keystore [appserver root]/standalone/configuration`
   * (Cluster do servidor Linux) `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. Exporte o arquivo de certificado digitando o seguinte comando:

   * (Servidor único) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * (Cluster do Servidor) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. Insira o *keystore_password* quando solicitado a fornecer uma senha.
1. Copie o arquivo AEMForms_cert.cer para a *[raiz do appserver] \conf* digite o seguinte comando:

   * (Windows Single Server) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * (Cluster do Windows Server) `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * (Servidor único Linux) `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * (Cluster do servidor Linux) `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. Visualize o conteúdo do certificado digitando o seguinte comando:

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. Para fornecer acesso de gravação ao arquivo cacerts em `[JAVA_HOME]\jre\lib\security`, se necessário, execute a seguinte tarefa:

   * (Windows) Clique com o botão direito do mouse no arquivo de acertos, selecione Propriedades e desmarque o atributo Somente leitura.
   * Tipo (Linux) `chmod 777 cacerts`

1. Importe o certificado digitando o seguinte comando:

   `keytool -import -alias "AEMForms Cert" -file`*AEMForms_cert* `.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. Tipo `changeit` como senha. Esta senha é a senha padrão para uma instalação Java e pode ter sido alterada pelo administrador do sistema.
1. Quando solicitado para `Trust this certificate? [no]`:, tipo `yes`. A confirmação &quot;O certificado foi adicionado ao keystore&quot; é exibida.
1. Se você estiver se conectando por SSL do Workbench, instale o certificado no computador do Workbench.
1. Em um editor de texto, abra os seguintes arquivos para edição:

   * Servidor único - `[appserver root]`/standalone/configuration/lc_&lt;dbname turnkey=&quot;&quot;>.xml

   * Cluster do servidor - `[appserver root]`/domain/configuration/host.xml

   * Cluster do servidor - `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **Para um único servidor,** no lc_&lt;dbaname tunkey=&quot;&quot;>arquivo .xml , adicione o seguinte após &lt;security-realms> seção:

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   Localize a variável `<server>` seção presente após o seguinte código:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Adicione o seguinte ao &lt;server> seção presente depois do código acima:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **Para cluster de servidores,** no [raiz do appserver]\domain\configuration\host.xml em todos os nós, adicione o seguinte após &lt;security-realms> seção:

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   No nó principal do Cluster do Servidor, no [raiz do appserver]\domain\configuration\domain_&lt;dbname>.xml, localize a variável &lt;server> seção presente após o seguinte código:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Adicione o seguinte ao &lt;server> seção presente depois do código acima:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. Altere o valor da variável `keystoreFile` e o `keystorePass` à senha do repositório de chaves que você especificou ao criar o armazenamento de chaves.
1. Reinicie o servidor de aplicativos:

   * Para instalações chave-na-mão:

      * No Painel de Controle do Windows, clique em Ferramentas Administrativas e em Serviços.
      * Selecione JBoss para formulários Adobe Experience Manager.
      * Selecione Ação > Parar.
      * Aguarde até que o status do serviço seja exibido como interrompido.
      * Selecione Ação > Iniciar.
   * Para instalações JBoss pré-configuradas ou configuradas manualmente no Adobe:

      * Em um prompt de comando, navegue até *`[appserver root]`*/bin.
      * Pare o servidor inserindo o seguinte comando:

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * Aguarde até que o processo JBoss tenha sido totalmente desligado (quando o processo JBoss retornar o controle para o terminal em que foi iniciado).
      * Inicie o servidor inserindo o seguinte comando:

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. Para acessar o console de administração usando SSL, digite `https://[host name]:'port'/adminui` em um navegador da Web:

   A porta SSL padrão para JBoss é 8443. A partir daqui, especifique essa porta ao acessar formulários AEM.

## Solicitar uma credencial de uma CA {#request-a-credential-from-a-ca}

1. Em um prompt de comando, navegue até *[PÁGINA INICIAL DO JAVA]*/bin e digite o seguinte comando para criar o armazenamento de chaves e a chave:

   `keytool -genkey -dname "CN=`*Nome do host* `, OU=`*Nome do grupo* `, O=`*Nome da empresa* `, L=`*Nome da cidade* `, S=`*Estado* `, C=`*Código do país*&quot; `-alias "AEMForms Cert"` `-keyalg RSA -keypass`-*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >Substituir *`[JAVA_HOME]`* com o diretório onde o JDK está instalado e substitua o texto em itálico por valores que correspondam ao seu ambiente.

1. Digite o seguinte comando para gerar uma solicitação de certificado para enviar à autoridade de certificação:

   `keytool -certreq -alias` &quot;Certificado AEMForms&quot; `-keystore`*keystorename* `.keystore -file`*AEMFormscertRequest.csr*

1. Quando a solicitação de um arquivo de certificado for atendida, conclua o próximo procedimento.

## Use uma credencial obtida de uma CA para habilitar o SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. Em um prompt de comando, navegue até *`[JAVA HOME]`*/bin e digite o seguinte comando para importar o certificado raiz da CA com a qual a CSR foi assinada:

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   Se o certificado raiz não estiver no navegador, também importe-o lá.

   >[!NOTE]
   >
   >Substituir *`[JAVA_HOME]`com o diretório onde o JDK está instalado e substitua o texto em itálico por valores que correspondam ao seu ambiente.*

1. Em um prompt de comando, navegue até *`[JAVA HOME]`*/bin e digite o seguinte comando para importar a credencial para o armazenamento de chaves:

   `keytool -import -trustcacerts -file`*CACercertificateName* `.crt -keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >* Substituir `[JAVA_HOME]` com o diretório onde o JDK está instalado e substitua o texto em itálico por valores que correspondam ao seu ambiente.
   >* O certificado assinado da CA importada substituirá um certificado público autoassinado se existir.


1. Conclua as etapas 13 a 18 de Criar uma credencial SSL.
