---
title: Configurar a senha de ligação LDAP
seo-title: Configurar a senha de ligação LDAP
description: Saiba como configurar o campo de senha de associação antes de importar o arquivo de configuração para outro sistema.
seo-description: Saiba como configurar o campo de senha de associação antes de importar o arquivo de configuração para outro sistema.
uuid: 1ab1907c-8b55-4b6f-bd5b-49f22d78b8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 165b3950-b03f-4848-8361-ffb0a26d2658
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 3%

---


# Configurar a senha de ligação LDAP{#configure-the-ldap-bind-password}

Para evitar riscos de segurança, o campo de senha de ligação no arquivo de configuração exportado (config.xml) não está configurado. Antes de importar o arquivo de configuração para outro sistema, certifique-se de configurar essa senha. Essa senha substitui uma senha existente armazenada no banco de dados. Uma senha nula não substitui um valor de senha não nulo existente.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos de configuração.
1. Para exportar a configuração atual para um arquivo, clique em Exportar e salve o arquivo de configuração em outro local.
1. No arquivo, localize o nó `Domains` > *[Seu nome]* de domínio > `DirectoryConfigs` > `LDAPGroupConfig` . Exemplo:

   ```xml
    <node name="LDAPGroupConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="batchSize" value="200" />
            <entry key="binduser" value="cn=Directory Manager" />
            <entry key="bindpassword" value="" />
        </map>
   ```

   Digite um valor para `bindpassword` e salve as alterações.

1. No arquivo, localize o nó `Domains` > *[Seu nome]* de domínio > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig` . Exemplo:

   ```xml
    <node name="LDAPUserConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="batchSize" value="200" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="bindpassword" value="" />
            <entry key="binduser" value="cn=Directory Manager" />
        </map>
   ```

   Digite um valor para `bindpassword` e salve as alterações.

1. Para importar o arquivo atualizado, em Gerenciamento de usuários, clique em Configuração > Importar e exportar arquivos de configuração.
1. Clique em Procurar para localizar o arquivo, clique em Importar e em OK.

