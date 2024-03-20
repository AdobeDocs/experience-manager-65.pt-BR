---
title: Configurar o gerenciamento de usuários para um servidor LDAP habilitado para SSL
description: Saiba como configurar o Gerenciamento de usuários para um servidor LDAP habilitado para SSL para que a sincronização funcione corretamente em LDAPS.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 606e84f2-6728-47a9-a439-dbe2e55100ad
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Configurar o gerenciamento de usuários para um servidor LDAP habilitado para SSL {#configure-user-management-for-an-ssl-enabled-ldap-server}

Para que a sincronização funcione corretamente em LDAPS, os certificados LDAP emitidos pela CA (autoridade de certificação) devem estar presentes no JRE (Java runtime environment) do servidor de aplicativos. Importe o certificado para o arquivo JRE cacerts do servidor de aplicativos, que geralmente está no *[JAVA_HOME]* diretório /jre/lib/security/cacerts.

1. Ative o SSL no servidor de diretório. Para obter detalhes, consulte a documentação fornecida pelo fornecedor do diretório.
1. Exporte um certificado de cliente do servidor de diretório.
1. Use o programa keytool para importar o arquivo de certificado do cliente para o armazenamento de certificado da máquina virtual Java (JVM™) padrão do servidor de aplicativos de formulários AEM. O procedimento para essa tarefa varia, dependendo dos caminhos de instalação do cliente e da JVM. Por exemplo, se você usar o BEA WebLogic Server com JDK 1.5, a partir de um prompt de comando, digite este texto:

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. Quando solicitado, digite a senha. (Para Java, a senha padrão é `changeit`.) Será exibida uma mensagem informando que o certificado foi importado com êxito.
1. Quando solicitado, digite `Yes` para confiar no certificado.
1. Ative o SSL no Gerenciamento de usuários e, ao definir as configurações de diretório, selecione Sim para a opção SSL e altere a configuração de porta de acordo. O número de porta padrão é 636.

>[!NOTE]
>
>Se você tiver algum problema usando SSL, use um navegador LDAP para verificar se ele pode acessar o sistema LDAP ao usar SSL. Se o navegador LDAP não puder obter acesso, o certificado ou o servidor de aplicativos não estará configurado corretamente. Se o navegador LDAP funcionar corretamente e você ainda estiver com problemas, o Gerenciamento de usuários não será configurado corretamente.
