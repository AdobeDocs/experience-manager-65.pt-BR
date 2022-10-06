---
title: Configurar a senha de vinculação LDAP
seo-title: Configure the LDAP bind password
description: Saiba como configurar o campo de senha de vinculação antes de importar o arquivo de configuração para outro sistema.
seo-description: Learn how to configure the bind password field before you import the configuration file into another system.
uuid: 1ab1907c-8b55-4b6f-bd5b-49f22d78b8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 165b3950-b03f-4848-8361-ffb0a26d2658
exl-id: c72794f5-8767-409e-a1df-91a8fdc54d18
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 4%

---

# Configurar a senha de vinculação LDAP{#configure-the-ldap-bind-password}

Para evitar riscos de segurança, o campo de senha de vinculação no arquivo de configuração exportado (config.xml) não está configurado. Antes de importar o arquivo de configuração para outro sistema, configure essa senha. Essa senha substitui uma senha existente armazenada no banco de dados. Uma senha nula não substitui um valor de senha não nula existente.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos de configuração.
1. Para exportar a configuração atual para um arquivo, clique em Exportar e salve o arquivo de configuração em outro local.
1. No arquivo , localize a variável `Domains` > *[Seu nome de domínio]* > `DirectoryConfigs` > `LDAPGroupConfig` nó . Exemplo:

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

1. No arquivo , localize a variável `Domains` > *[Seu nome de domínio]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig` nó . Exemplo:

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
