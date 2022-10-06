---
title: Configurar o gerenciamento de usuários para um servidor LDAP habilitado para SSL
seo-title: Configure User Management for an SSL-enabled LDAP server
description: Saiba como configurar o Gerenciamento de usuários para um servidor LDAP habilitado para SSL para permitir que a sincronização funcione corretamente no LDAPS.
seo-description: Learn how  to configure User Management for an SSL-enabled LDAP server to enable synchronization to work properly over LDAPS.
uuid: 4b3f8ac7-fa38-4adf-a851-82d55fe431fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e6e7e2fa-579d-4b36-8598-6ced469a94b1
exl-id: 606e84f2-6728-47a9-a439-dbe2e55100ad
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Configurar o gerenciamento de usuários para um servidor LDAP habilitado para SSL {#configure-user-management-for-an-ssl-enabled-ldap-server}

Para que a sincronização funcione corretamente no LDAPS, os certificados LDAP que a autoridade de certificação (CA) emitida devem estar presentes no JRE (Java runtime environment) do servidor de aplicativos. Importe o certificado para o arquivo JRE do servidor de aplicativos, que geralmente está no *[JAVA_HOME]* diretório /jre/lib/security/cacerts.

1. Ative o SSL no servidor de diretório. Para obter detalhes, consulte a documentação fornecida pelo fornecedor do diretório.
1. Exportar um certificado de cliente do servidor de diretório.
1. Use o programa keytool para importar o arquivo de certificado do cliente para o armazenamento de certificado padrão da máquina virtual Java (JVM™) do servidor de aplicativos AEM forms . O procedimento para essa tarefa varia, dependendo dos caminhos de instalação da JVM e do cliente. Por exemplo, se você usar o BEA WebLogic Server com JDK 1.5, em um prompt de comando, digite este texto:

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. Quando solicitado, digite a senha. (Para Java, a senha padrão é `changeit`.) Será exibida uma mensagem informando que o certificado foi importado com êxito.
1. Quando solicitado, digite `Yes` para confiar no certificado.
1. Ative o SSL no Gerenciamento de usuários e, ao definir as configurações de diretório, selecione Sim para a opção SSL e altere a configuração da porta de acordo. O número padrão da porta é 636.

>[!NOTE]
>
>Se você tiver algum problema usando SSL, use um navegador LDAP para verificar se ele pode acessar o sistema LDAP ao usar SSL. Se o navegador LDAP não conseguir acessar, seu certificado ou servidor de aplicativos não será configurado corretamente. Se o navegador LDAP funcionar corretamente e você ainda estiver enfrentando problemas, o Gerenciamento de usuários não será configurado corretamente.
