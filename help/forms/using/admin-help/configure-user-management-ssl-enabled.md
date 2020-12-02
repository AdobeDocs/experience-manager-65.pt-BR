---
title: Configurar o Gerenciamento de usuários para um servidor LDAP habilitado para SSL
seo-title: Configurar o Gerenciamento de usuários para um servidor LDAP habilitado para SSL
description: Saiba como configurar o Gerenciamento de usuários para um servidor LDAP habilitado para SSL para permitir que a sincronização funcione corretamente no LDAPS.
seo-description: Saiba como configurar o Gerenciamento de usuários para um servidor LDAP habilitado para SSL para permitir que a sincronização funcione corretamente no LDAPS.
uuid: 4b3f8ac7-fa38-4adf-a851-82d55fe431fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e6e7e2fa-579d-4b36-8598-6ced469a94b1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Configurar o Gerenciamento de usuários para um servidor LDAP habilitado para SSL {#configure-user-management-for-an-ssl-enabled-ldap-server}

Para que a sincronização funcione corretamente no LDAPS, os certificados LDAP emitidos pela autoridade de certificação (CA) devem estar presentes no ambiente Java Runtime (JRE) do servidor de aplicativos. Importe o certificado para o arquivo JRE cacerts do servidor de aplicativos, que geralmente está no diretório *[JAVA_HOME]*/jre/lib/security/cacerts.

1. Ative o SSL no servidor de diretório. Para obter detalhes, consulte a documentação fornecida pelo fornecedor do diretório.
1. Exporte um certificado de cliente do servidor de diretório.
1. Use o programa keytool para importar o arquivo de certificado do cliente para o repositório de certificados padrão da máquina virtual Java (JVM™) do servidor de aplicativos para formulários AEM. O procedimento para essa tarefa varia, dependendo dos caminhos de instalação do JVM e do cliente. Por exemplo, se você usar o BEA WebLogic Server com JDK 1.5, em um prompt de comando, digite este texto:

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. Quando solicitado, digite a senha. (Para Java, a senha padrão é `changeit`.) Será exibida uma mensagem informando que o certificado foi importado com êxito.
1. Quando solicitado, digite `Yes` para confiar no certificado.
1. Ative o SSL no Gerenciamento de usuários e, ao definir as configurações de diretório, selecione Sim para a opção SSL e altere a configuração da porta de acordo. O número da porta padrão é 636.

>[!NOTE]
>
>Se tiver problemas ao usar SSL, use um navegador LDAP para verificar se ele pode acessar o sistema LDAP ao usar SSL. Se o navegador LDAP não conseguir acesso, seu certificado ou servidor de aplicativos não será configurado corretamente. Se o navegador LDAP funcionar corretamente e você ainda tiver problemas, o Gerenciamento de usuários não será configurado corretamente.

