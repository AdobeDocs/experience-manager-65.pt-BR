---
title: Configurando o SSL para o servidor da aplicação JBoss
description: Saiba como configurar o SSL para o JBoss Application Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8eb4f691-a66b-498e-8114-307221f63718
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# Configurando o SSL para o servidor da aplicação JBoss {#configuring-ssl-for-jboss-application-server}

Para configurar o SSL no JBoss Application Server, você precisa de uma credencial SSL para autenticação. Você pode usar a ferramenta de chaves Java para criar uma credencial ou solicitar e importar uma credencial de uma autoridade de certificação (CA). Você deve então ativar o SSL no JBoss.

Você pode executar a ferramenta de chaves usando um único comando que inclui todas as informações necessárias para criar a área de armazenamento de chaves.

Neste procedimento:

* `[appserver root]` é o diretório base do servidor de aplicativos que está executando formulários AEM.
* `[type]` é um nome de pasta que varia, dependendo do tipo de instalação que você realizou.

## Criar uma credencial SSL {#create-an-ssl-credential}

1. Em um prompt de comando, navegue até *[JAVA HOME]*/bin e digite o seguinte comando para criar a credencial e o keystore:

   `keytool -genkey -dname "CN=`*Nome do Host* `, OU=`*Nome do Grupo* `, O=`*Nome da Empresa* `,L=`*Nome da Cidade* `, S=`*Estado* `, C=`Código do País&quot; `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >Substitua `[JAVA_HOME]` pelo diretório onde o JDK está instalado e o texto em itálico por valores que correspondam ao seu ambiente. Nome do Host é o nome de domínio totalmente qualificado do servidor de aplicativos.

1. Digite a `keystore_password` quando for solicitada uma senha. A senha do keystore e a chave devem ser idênticas.

   >[!NOTE]
   >
   >O `keystore_password` *ndigitado nesta etapa pode ter a mesma senha (key_password) inserida na etapa 1 ou ser diferente.*

1. Copie o *keystorename*.keystore para o diretório `[appserver root]/server/[type]/conf` digitando um dos seguintes comandos:

   * (Windows Single Server) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * Cópia `keystorename.keystore[appserver root]\domain\configuration` (Cluster do Windows Server)
   * (Linux Single Server) `cp keystorename.keystore [appserver root]/standalone/configuration`
   * (Cluster de Servidores Linux) `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. Exporte o arquivo de certificado digitando o seguinte comando:

   * (Servidor Único) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * (Cluster de Servidores) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. Digite a *keystore_password* quando for solicitada uma senha.
1. Copie o arquivo AEMForms_cert.cer para o diretório *[raiz do appserver] \conf* digitando o seguinte comando:

   * (Windows Single Server) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * (Cluster do Windows Server) `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * (Linux Single Server) `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * (Cluster de Servidores Linux) `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. Visualize o conteúdo do certificado digitando o seguinte comando:

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. Para fornecer acesso de gravação ao arquivo cacerts em `[JAVA_HOME]\jre\lib\security`, se necessário, execute a seguinte tarefa:

   * (Windows) Clique com o botão direito do mouse no arquivo cacerts, selecione Propriedades e desmarque o atributo Somente leitura.
   * Tipo (Linux) `chmod 777 cacerts`

1. Importe o certificado digitando o seguinte comando:

   `keytool -import -alias "AEMForms Cert" -file`*AEMForms_cert* `.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. Digite `changeit` como senha. Esta senha é a senha padrão para uma instalação do Java e pode ter sido alterada pelo administrador do sistema.
1. Quando solicitado por `Trust this certificate? [no]`, digite `yes`. A confirmação &quot;O certificado foi adicionado ao armazenamento de chaves&quot; é exibida.
1. Se você estiver se conectando por SSL do Workbench, instale o certificado no computador do Workbench.
1. Em um editor de texto, abra os seguintes arquivos para edição:

   * Servidor único - `[appserver root]`/standalone/configuration/lc_&lt;dbname/turnkey>.xml

   * Cluster de Servidores - `[appserver root]`/domain/configuration/host.xml

   * Cluster de Servidores - `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. &#x200B;
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

   Localize a seção `<server>` presente após o seguinte código:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Adicione o seguinte à seção &lt;server> presente após o código acima:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **Para o cluster de servidores,** na [raiz do appserver]\domain\configuration\host.xml em todos os nós, adicione o seguinte após a seção &lt;security-realms>:

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   No nó primário do Cluster de Servidores, no [appserver root]\domain\configuration\domain_&lt;dbname>.xml, localize a seção &lt;server> presente após o seguinte código:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Adicione o seguinte à seção &lt;server> presente após o código acima:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. Altere o valor do atributo `keystoreFile` e do atributo `keystorePass` para a senha do keystore que você especificou quando criou o keystore.
1. Reinicie o servidor de aplicativos:

   * Para instalações prontas para uso:

      * No Painel de Controle do Windows, clique em Ferramentas Administrativas e em Serviços.
      * Selecione JBoss para o Adobe Experience Manager Forms.
      * Selecione Ação > Parar.
      * Aguarde até que o status do serviço apareça como interrompido.
      * Selecione Ação > Iniciar.

   * Para instalações do JBoss pré-configuradas ou configuradas manualmente pelo Adobe:

      * Em um prompt de comando, navegue até *`[appserver root]`*/bin.
      * Pare o servidor digitando o seguinte comando:

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`

      * Aguarde até que o processo JBoss tenha sido totalmente desligado (quando o processo JBoss retornar o controle para o terminal em que foi iniciado).
      * Inicie o servidor digitando o seguinte comando:

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`

1. Para acessar o console de administração usando SSL, digite `https://[host name]:'port'/adminui` em um navegador da Web:

   A porta SSL padrão para JBoss é 8443. A partir daqui, especifique esta porta ao acessar formulários AEM.

## Solicitar uma credencial de uma autoridade de certificação {#request-a-credential-from-a-ca}

1. Em um prompt de comando, navegue até *[JAVA HOME]*/bin e digite o seguinte comando para criar o keystore e a chave:

   `keytool -genkey -dname "CN=`*Nome do Host* `, OU=`*Nome do Grupo* `, O=`*Nome da Empresa* `, L=`*Nome da Cidade* `, S=`*Estado* `, C=`*Código do País*&quot; `-alias "AEMForms Cert"` `-keyalg RSA -keypass`-*chave_senha* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >Substitua *`[JAVA_HOME]`* pelo diretório onde o JDK está instalado e o texto em itálico por valores que correspondam ao seu ambiente.

1. Digite o seguinte comando para gerar uma solicitação de certificado a ser enviada à autoridade de certificação:

   `keytool -certreq -alias` &quot;Certificado de AEMForms&quot; `-keystore`*keystorename* `.keystore -file`*AEMFormscertRequest.csr*

1. Quando a solicitação de um arquivo de certificado for atendida, conclua o próximo procedimento.

## Usar uma credencial obtida de uma CA para habilitar o SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. Em um prompt de comando, navegue até *`[JAVA HOME]`*/bin e digite o seguinte comando para importar o certificado raiz da CA com a qual o CSR foi assinado:

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   Se o certificado raiz não estiver no navegador, importe-o também para lá.

   >[!NOTE]
   >
   >Substitua *`[JAVA_HOME]`pelo diretório onde o JDK está instalado e o texto em itálico por valores que correspondam ao seu ambiente.*

1. Em um prompt de comando, navegue até *`[JAVA HOME]`*/bin e digite o seguinte comando para importar a credencial para o keystore:

   `keytool -import -trustcacerts -file`*CACertificateName* `.crt -keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >* Substitua `[JAVA_HOME]` pelo diretório onde o JDK está instalado e o texto em itálico por valores que correspondam ao seu ambiente.
   >* O certificado assinado CA importado substituirá um certificado público autoassinado, se ele existir.

1. Conclua as etapas 13 a 18 de Criar uma credencial SSL.
