---
title: Configuração do SSL para WebLogic Server
seo-title: Configuração do SSL para WebLogic Server
description: Saiba como criar uma credencial SSL para uso no servidor WebLogic e configurar o SSL para o WebLogic Server.
seo-description: Saiba como criar uma credencial SSL para uso no servidor WebLogic e configurar o SSL para o WebLogic Server.
uuid: 8ee979fd-2615-451b-a607-4f73ecfed4f9
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 968c2574-ec9a-45ca-9c64-66f4caeec285
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configuração do SSL para WebLogic Server {#configuring-ssl-for-weblogic-server}

Para configurar o SSL no WebLogic Server, você precisa de uma credencial SSL para autenticação. Você pode usar o Java keytool para executar as seguintes tarefas para criar uma credencial:

* Crie um par de chaves públicas/privadas, vincule a chave pública em um certificado autoassinado X.509 v1 armazenado como uma cadeia de certificados de um único elemento e armazene a cadeia de certificados e a chave privada em um novo armazenamento de chaves. Esse armazenamento de chaves é o armazenamento de chaves de identidade personalizada do servidor de aplicativos.
* Extraia o certificado e insira-o em um novo armazenamento de chaves. Esse armazenamento de chaves é o armazenamento de chaves de Confiança personalizada do servidor de aplicativos.

Em seguida, configure o WebLogic para que ele use o armazenamento de chaves Identidade personalizada e o armazenamento de chaves Confiança personalizada criados. Além disso, desative o recurso Verificação de nome de host WebLogic porque o nome distinto usado para criar os arquivos de armazenamento de chaves não incluía o nome do computador que hospeda o WebLogic.

## Criando uma credencial SSL para uso no WebLogic Server {#creating-an-ssl-credential-for-use-on-weblogic-server}

O comando keytool geralmente está localizado no diretório Java jre/bin e deve incluir várias opções e valores de opções, listados na tabela a seguir.

<table>
 <thead>
  <tr>
   <th><p>Opção Keytool</p></th>
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
     <li><p>Armazenamento de chave de Confiança personalizado: <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>O algoritmo a ser usado para gerar o par de chaves.</p></td>
   <td><p>RSA</p><p>Você pode usar um algoritmo diferente, dependendo da política de sua empresa.</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>O local e o nome do arquivo de armazenamento de chaves.</p><p>O local pode incluir o caminho absoluto do arquivo. Ou pode ser relativo ao diretório atual do prompt de comando no qual o comando keytool é inserido.</p></td>
   <td>
    <ul>
     <li><p>Armazenamento de chaves de identidade personalizada: <code>[</code><i>appserverdomain]</i><code>/adobe/</code><i>[nome do servidor]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>Armazenamento de chave de Confiança personalizado: <code>[</code><i>appserverdomain]</i><code>/adobe/</code><i>[nome do servidor]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-arquivo</p></td>
   <td><p>O local e o nome do arquivo de certificado.</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>-validade</p></td>
   <td><p>O número de dias em que o certificado é considerado válido.</p></td>
   <td><p>3650</p><p>Você pode usar um valor diferente, dependendo da política de sua empresa.</p></td>
  </tr>
  <tr>
   <td><p>-cegonha</p></td>
   <td><p>A senha que protege o conteúdo do armazenamento de chaves. </p></td>
   <td>
    <ul>
     <li><p>Armazenamento de chaves de identidade personalizada: A senha do armazenamento de chaves deve corresponder à senha de credenciais SSL especificada para o componente Armazenamento de Confiança do Console de Administração.</p></li>
     <li><p>Armazenamento de chave de Confiança personalizado: Use a mesma senha que você usou para o armazenamento de chaves de identidade personalizada.</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>A senha que protege a chave privada do par de chaves.</p></td>
   <td><p>Use a mesma senha que você usou para a <code>-storepass</code> opção. A senha da chave deve ter pelo menos seis caracteres.</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>O nome distinto que identifica a pessoa que possui o armazenamento de chaves.</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> é a identificação do usuário proprietário do armazenamento de chaves.</p></li>
     <li><p><code><i>[Group Name]</i></code> é a identificação do grupo corporativo ao qual o proprietário do armazenamento de chaves pertence.</p></li>
     <li><p><code><i>[Company Name]</i></code> é o nome da sua organização.</p></li>
     <li><p><code><i>[City Name]</i></code> é a cidade onde sua organização está localizada.</p></li>
     <li><p><code><i>[State or province]</i></code> é o estado ou província onde sua organização está localizada.</p></li>
     <li><p><code><i>[Country Code]</i></code> é o código de duas letras do país onde sua organização está localizada.</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

Para obter mais informações sobre como usar o comando keytool, consulte o arquivo keytool.html que faz parte da documentação do JDK.

## Crie os armazenamentos de chaves de identidade e confiança personalizadas {#create-the-custom-identity-and-trust-keystores}

1. Em um prompt de comando, navegue até *[appserverdomain]*/adobe/*[server name]*.
1. Digite o seguinte comando:

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >Substitua `[JAVA_HOME]`*pelo diretório onde o JDK está instalado e substitua o texto em itálico por valores que correspondam ao seu ambiente.*

   Por exemplo:

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   O arquivo de armazenamento de chave da Identidade personalizada chamado &quot;ads-entials.jks&quot; é criado no diretório [appserverdomain]/adobe/[server name] .

1. Extraia o certificado do armazenamento de chaves ads-entials digitando o seguinte comando:

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**password**

   >[!NOTE]
   >
   >Substitua `[JAVA_HOME]` pelo diretório onde o JDK está instalado e substitua `store`*_*`password`* pela senha do armazenamento de chaves da Identidade personalizada.*

   Por exemplo:

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   O arquivo de certificado chamado &quot;ads-ca.cer&quot; é criado no diretório [appserverdomain]/adobe/[*server name*] .

1. Copie o arquivo ads-ca.cer para qualquer computador host que precise de comunicação segura com o servidor de aplicativos.
1. Insira o certificado em um novo arquivo de armazenamento de chaves (o armazenamento de chaves de Confiança personalizado) digitando o seguinte comando:

   [JAVA_HOME]`/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >Substitua `[JAVA_HOME]` pelo diretório onde o JDK está instalado e substitua `store`*_*`password`e`key`*_* `password` *por suas próprias senhas.*

   Por exemplo:

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

O arquivo de armazenamento de chave de Confiança personalizada chamado &quot;ads-ca.jks&quot; é criado no diretório [appserverdomain]/adobe/&#39;server&#39;.

Configure o WebLogic para que ele use o armazenamento de chaves Identidade personalizada e o armazenamento de chaves Confiança personalizada criados. Além disso, desative o recurso Verificação de nome de host WebLogic porque o nome distinto usado para criar os arquivos de armazenamento de chaves não incluía o nome do computador que hospeda o WebLogic Server.

## Configurar WebLogic para usar SSL {#configure-weblogic-to-use-ssl}

1. Start o console de administração do WebLogic Server digitando o nome `https://`*[do ]*host`:7001/console`na linha de URL de um navegador da Web.
1. Em Ambiente, em Configurações de domínio, selecione **Servidores > &#39;servidor&#39; > Configuração > Geral**.
1. Em Geral, em Configuração, verifique se a opção Porta de **escuta ativada** e Porta de escuta **SSL ativada** está selecionada. Se não estiver ativado, faça o seguinte:

   1. Em Centro de alterações, clique em **Bloquear e editar** para modificar seleções e valores.
   1. Marque as caixas de seleção Porta de **escuta ativada** e Porta de escuta **SSL ativada** .

1. Se esse servidor for um servidor gerenciado, altere a Porta de escuta para um valor de porta não utilizado (como 8001) e a Porta de escuta SSL para um valor de porta não utilizado (como 8002). Em um servidor independente, a porta SSL padrão é 7002.
1. Clique em **Liberar configuração**.
1. Em Ambiente, em Configurações de domínio, clique em **Servidores > Servidor [**]gerenciado > Configuração > Geral**.
1. Em Geral, em Configuração, selecione **armazenamentos de chaves**.
1. Em Centro de alterações, clique em **Bloquear e editar** para modificar seleções e valores.
1. Clique em **Alterar** para obter a lista do keystore como lista suspensa e selecione Identidade **personalizada e Confiança** personalizada.
1. Em Identidade, especifique os seguintes valores:

   **Armazenamento de chaves** de identidade personalizado: *[appserverdomain]*/adobe/*[server name]*/ads-credentials.jks, onde *[appserverdomain] *é o caminho real e o nome *[do]* servidor é o nome do servidor de aplicativos.

   **Tipo** de armazenamento de chave de identidade personalizado: JKS

   **Senha** personalizada do armazenamento de chave de identidade: *mypassword* (senha personalizada do keystore de identidade)

1. Em Confiança, especifique os seguintes valores:

   **Nome** do Arquivo do Keystore de Confiança Personalizado: `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`, onde `*[appserverdomain]*` é o caminho real

   **Tipo** de armazenamento de chave de confiança personalizado: JKS

   **Frase** de Aprovação do Keystore de Confiança Personalizado: *mypassword* (senha da chave de confiança personalizada)

1. Em Geral, em Configuração, selecione **SSL**.
1. Por padrão, o Keystore é selecionado para Locais de identidade e confiança. Caso contrário, altere para keystore.
1. Em Identidade, especifique os seguintes valores:

   **Alias** da chave privada: publicidades-credenciais

   **Senha**: *mypassword*

1. Clique em **Liberar configuração**.

## Desativar o recurso Verificação do nome do host {#disable-the-hostname-verification-feature}

1. Na guia Configuração, clique em SSL.
1. Em Avançado, selecione Nenhum na lista de verificação do nome do host.

   Se a Verificação do nome do host não estiver desativada, o Nome comum (CN) deverá conter o nome do host do servidor.

1. Em Centro de alterações, clique em Bloquear e editar para modificar seleções e valores.
1. Reinicie o servidor de aplicativos.

