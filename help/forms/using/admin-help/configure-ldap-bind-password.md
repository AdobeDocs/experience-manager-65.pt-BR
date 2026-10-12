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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%
---
# Configurar a senha de associação LDAP{#configure-the-ldap-bind-password}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Para evitar riscos de segurança, o campo vincular senha no arquivo de configuração exportado (config.xml) não está configurado. Antes de importar o arquivo de configuração para outro sistema, configure essa senha. Essa senha substitui uma senha existente armazenada no banco de dados. Uma senha nula não substitui um valor de senha não nulo existente.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos de configuração.
1. Para exportar a definição da configuração atual para um arquivo, clique em Exportar e salve o arquivo de configuração em outro local.
1. No arquivo, localize o nó `Domains` > *[Nome do seu domínio]* > `DirectoryConfigs` > `LDAPGroupConfig`. Veja um exemplo:

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

1. No arquivo, localize o nó `Domains` > *[Nome do seu domínio]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig`. Veja um exemplo:

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
