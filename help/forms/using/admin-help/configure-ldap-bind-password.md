---
title: Configurar a senha de associação LDAP
description: Saiba como configurar o campo vincular senha antes de importar o arquivo de configuração para outro sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c72794f5-8767-409e-a1df-91a8fdc54d18
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Configurar a senha de associação LDAP{#configure-the-ldap-bind-password}

Para evitar riscos de segurança, o campo vincular senha no arquivo de configuração exportado (config.xml) não está configurado. Antes de importar o arquivo de configuração para outro sistema, configure essa senha. Essa senha substitui uma senha existente armazenada no banco de dados. Uma senha nula não substitui um valor de senha não nulo existente.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos de configuração.
1. Para exportar a definição da configuração atual para um arquivo, clique em Exportar e salve o arquivo de configuração em outro local.
1. No arquivo, localize o `Domains` > *[Nome do domínio]* > `DirectoryConfigs` > `LDAPGroupConfig` nó. Veja um exemplo:

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

1. No arquivo, localize o `Domains` > *[Nome do domínio]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig` nó. Veja um exemplo:

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

1. Para importar o arquivo atualizado, no Gerenciamento de usuários, clique em Configuração > Importar e exportar arquivos de configuração.
1. Clique em Procurar para localizar o arquivo, clique em Importar e em OK.
