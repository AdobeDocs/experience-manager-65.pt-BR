---
title: Configuração do SSL para o WebLogic Server
seo-title: Configuring SSL for WebLogic Server
description: Saiba como criar uma credencial SSL para uso no servidor WebLogic e como configurar o SSL para o WebLogic Server.
seo-description: Learn how to create an SSL credential for use on WebLogic server and how to configure SSL for WebLogic Server.
uuid: 8ee979fd-2615-451b-a607-4f73ecfed4f9
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 968c2574-ec9a-45ca-9c64-66f4caeec285
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 1%

---


# Configuração do SSL para o WebLogic Server {#configuring-ssl-for-weblogic-server}

Para configurar o SSL no WebLogic Server, você precisa de uma credencial SSL para autenticação. Você pode usar a ferramenta-chave Java para executar as seguintes tarefas para criar uma credencial:

* Crie um par de chaves públicas/privadas, envolva a chave pública em um certificado autoassinado X.509 v1 armazenado como uma cadeia de certificados de elemento único e armazene a cadeia de certificados e a chave privada em um novo armazenamento de chaves. Esse armazenamento de chaves é o armazenamento de chaves de identidade personalizada do servidor de aplicativos.
* Extraia o certificado e insira-o em um novo armazenamento de chaves. Esse armazenamento de chaves é o armazenamento de chaves Custom Trust do servidor de aplicativos.

Em seguida, configure o WebLogic para que ele use o repositório de chaves Custom Identity e o repositório de chaves Custom Trust que você criou. Além disso, desative o recurso Verificação do nome de host WebLogic porque o nome distinto usado para criar os arquivos do repositório de chaves não incluía o nome do computador que hospeda o WebLogic.

## Criação de uma credencial SSL para uso no WebLogic Server {#creating-an-ssl-credential-for-use-on-weblogic-server}

O comando keytool geralmente está localizado no diretório Java jre/bin e deve incluir várias opções e valores de opções, que estão listados na tabela a seguir.

<table>
 <thead>
  <tr>
   <th><p>Opção de ferramenta-chave</p></th>
   <th><p>Descrição</p></th>
   <th><p>Valor de opção</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>-alias</p></td>
   <td><p>O alias do armazenamento de chaves.</p></td>
   <td>
    <ul>
     <li><p>Armazenamento de chaves de identidade personalizada: <code>ads-credentials</code></p></li>
     <li><p>Armazenamento de chaves de confiança personalizada: <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>O algoritmo a ser usado para gerar o par de chaves.</p></td>
   <td><p>RSA</p><p>Você pode usar um algoritmo diferente, dependendo da política da sua empresa.</p></td>
  </tr>
  <tr>
   <td><p>keystore</p></td>
   <td><p>O local e o nome do arquivo do repositório de chaves.</p><p>O local pode incluir o caminho absoluto do arquivo. Ou pode ser relativo ao diretório atual do prompt de comando, onde o comando keytool é inserido.</p></td>
   <td>
    <ul>
     <li><p>Armazenamento de chaves de identidade personalizada: <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[nome do servidor]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>Armazenamento de chaves de confiança personalizada: <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[nome do servidor]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-file</p></td>
   <td><p>O local e o nome do arquivo de certificado.</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>validade</p></td>
   <td><p>O número de dias que o certificado é considerado válido.</p></td>
   <td><p>3650</p><p>Você pode usar um valor diferente, dependendo da política da sua empresa.</p></td>
  </tr>
  <tr>
   <td><p>cegonha</p></td>
   <td><p>A senha que protege o conteúdo do repositório de chaves. </p></td>
   <td>
    <ul>
     <li><p>Armazenamento de chaves de identidade personalizada: A senha do repositório de chaves deve corresponder à senha da credencial SSL especificada para o componente Armazenamento de Confiança do Console de Administração.</p></li>
     <li><p>Armazenamento de chaves de confiança personalizada: Use a mesma senha que você usou para o armazenamento de chaves Identidade personalizada.</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>A senha que protege a chave privada do par de chaves.</p></td>
   <td><p>Use a mesma senha que você usou para o <code>-storepass</code> opção. A senha da chave deve ter pelo menos seis caracteres.</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>O nome distinto que identifica a pessoa proprietária do repositório de chaves.</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> é a identificação do usuário que possui o repositório de chaves.</p></li>
     <li><p><code><i>[Group Name]</i></code> é a identificação do grupo corporativo ao qual o proprietário do repositório de chaves pertence.</p></li>
     <li><p><code><i>[Company Name]</i></code> é o nome da sua organização.</p></li>
     <li><p><code><i>[City Name]</i></code> é a cidade onde sua organização está localizada.</p></li>
     <li><p><code><i>[State or province]</i></code> é o estado ou província em que a organização está localizada.</p></li>
     <li><p><code><i>[Country Code]</i></code> é o código de duas letras do país onde sua organização está localizada.</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

Para obter mais informações sobre como usar o comando keytool, consulte o arquivo keytool.html que faz parte de sua documentação JDK.

## Crie armazenamentos de chaves de identidade e confiança personalizadas {#create-the-custom-identity-and-trust-keystores}

1. Em um prompt de comando, navegue até *[appserverdomain]*/adobe/*[nome do servidor]*.
1. Digite o seguinte comando:

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >Substituir `[JAVA_HOME]`*com o diretório onde o JDK está instalado e substitua o texto em itálico por valores que correspondam ao seu ambiente.*

   Por exemplo:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   O arquivo de repositório de chaves da Identidade Personalizada chamado &quot;ads-credentials.jks&quot; é criado no [appserverdomain]/adobe/[nome do servidor] diretório.

1. Extraia o certificado do repositório de chaves de credenciais de anúncios digitando o seguinte comando:

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**password**

   >[!NOTE]
   >
   >Substituir `[JAVA_HOME]` com o diretório onde o JDK está instalado e substitua `store`*_* `password`* com a senha do repositório de chaves de identidade personalizada.*

   Por exemplo:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   O arquivo de certificado chamado &quot;ads-ca.cer&quot; é criado no [appserverdomain]/adobe/[*nome do servidor*] diretório.

1. Copie o arquivo ads-ca.cer para qualquer computador host que precise de comunicação segura com o servidor de aplicativos.
1. Insira o certificado em um novo arquivo de repositório de chaves (o repositório de chaves da Confiança Personalizada), inserindo o seguinte comando:

   [JAVA_HOME] `/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >Substituir `[JAVA_HOME]` com o diretório onde o JDK está instalado e substitua `store`*_* `password` e `key`*_* `password` *com suas próprias senhas.*

   Por exemplo:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

O arquivo de repositório de chaves da Confiança personalizada chamado &quot;ads-ca.jks&quot; é criado no [appserverdomain]diretório /adobe/&#39;server&#39;.

Configure o WebLogic para usar o repositório de chaves de Identidade personalizada e o repositório de chaves de Confiança personalizada que você criou. Além disso, desative o recurso Verificação do nome de host WebLogic porque o nome distinto usado para criar os arquivos do repositório de chaves não incluía o nome do computador que hospeda o WebLogic Server.

## Configurar o WebLogic para usar SSL {#configure-weblogic-to-use-ssl}

1. Inicie o console de administração do WebLogic Server digitando `https://`*[nome do host ]*`:7001/console` na linha URL de um navegador da Web.
1. Em Ambiente, em Configurações de domínio, selecione **Servidores > &#39;servidor&#39; > Configuração > Geral**.
1. Em Geral, em Configuração, verifique se **Porta de escuta habilitada** e **Porta de escuta SSL habilitada** são selecionadas. Se não estiver ativado, faça o seguinte:

   1. Em Centro de alterações, clique em **Bloquear e editar** para modificar seleções e valores.
   1. Verifique a **Porta de escuta habilitada** e **Porta de escuta SSL habilitada** caixas de seleção.

1. Se esse servidor for um servidor gerenciado, altere a Porta de escuta para um valor de porta não utilizado (como 8001) e a Porta de escuta SSL para um valor de porta não utilizado (como 8002). Em um servidor independente, a porta SSL padrão é 7002.
1. Clique em **Configuração da versão**.
1. Em Ambiente, em Configurações de domínio, clique em **Servidores > [*Servidor gerenciado*] > Configuração > Geral**.
1. Em Geral, em Configuração, selecione **Armazenamento de chaves**.
1. Em Centro de alterações, clique em **Bloquear e editar** para modificar seleções e valores.
1. Clique em **Alterar** para obter a lista de armazenamento de chaves como lista suspensa e selecione **Identidade Personalizada E Confiança Personalizada**.
1. Em Identidade, especifique os seguintes valores:

   **Armazenamento de chaves de identidade personalizada**: *[appserverdomain]*/adobe/*[nome do servidor]*/ads-credentials.jks, onde *[appserverdomain] *é o caminho real e *[nome do servidor]* é o nome do servidor de aplicativos.

   **Tipo de armazenamento de chaves de identidade personalizada**: JKS

   **Senha do repositório de chaves de identidade personalizado**: *mypassword* (senha personalizada do repositório de chaves de identidade)

1. Em Confiança, especifique os seguintes valores:

   **Nome do Arquivo do Armazenamento de Chaves de Confiança Personalizado**: `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`, onde `*[appserverdomain]*` é o caminho real

   **Tipo de Armazenamento de Chaves de Confiança Personalizado**: JKS

   **Frase de Passe do Armazenamento de Chaves de Confiança Personalizado**: *mypassword* (senha da chave de confiança personalizada)

1. Em Geral, em Configuração, selecione **SSL**.
1. Por padrão, o Armazenamento de chaves é selecionado para Locais de identidade e confiança. Caso contrário, altere para keystore.
1. Em Identidade, especifique os seguintes valores:

   **Alias da chave privada**: ads-credentials

   **Senha**: *mypassword*

1. Clique em **Configuração da versão**.

## Desative o recurso de verificação do nome de host {#disable-the-hostname-verification-feature}

1. Na guia Configuração, clique em SSL.
1. Em Avançado, selecione Nenhum na lista Verificação do nome do host.

   Se a Verificação do Nome do Host não estiver desativada, o Nome Comum (CN) deverá conter o nome do host do servidor.

1. Em Centro de alterações, clique em Bloquear e editar para modificar seleções e valores.
1. Reinicie o servidor de aplicativos.

