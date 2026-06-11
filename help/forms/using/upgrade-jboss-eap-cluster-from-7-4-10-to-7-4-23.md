---
title: Atualização do cluster JBoss EAP de 7.4.10 para 7.4.23 para AEM Forms no JEE
description: Etapas adicionais para atualizar um cluster JBoss EAP de 7.4.10 para 7.4.23 para AEM Forms no JEE.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
exl-id: 2c9e7f41-a8d6-4b03-8e5c-1a4f6d9e0b72
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms Upgrade,AEM Forms on JEE
role: User, Developer
source-git-commit: 652162941dd716ae797ce50709e91757dad99054
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 1%

---

# Atualização do cluster JBoss EAP de 7.4.10 para 7.4.23 para AEM Forms no JEE {#upgrade-jboss-eap-cluster-from-7-4-10-to-7-4-23}

## Visão geral {#overview}

Quando você atualiza um cluster JBoss EAP da versão 7.4.10 para a 7.4.23 para AEM Forms no JEE, é necessária uma configuração adicional além das etapas de atualização independentes. As configurações específicas do cluster, como localizadores de cache, autenticação master-slave, vinculações de host e configuração do controlador de domínio devem ser atualizadas na nova instalação do JBoss.

## Aplica-se a {#applies-to}

Este artigo aplica-se a:

* AEM Forms no JEE executado no JBoss EAP 7.4.10 em um ambiente de cluster
* Configurações de EAP JBoss master-slave no Windows e Linux

## Pré-requisitos {#prerequisites}

Conclua todas as etapas no [Atualizar JBoss EAP da versão 7.4.10 para a 7.4.23 para AEM Forms no JEE](/help/forms/using/upgrade-jboss-eap-from-7-4-10-to-7-4-23.md), incluindo a cópia da URL de conexão, do nome de usuário e da senha da instalação existente para os novos arquivos de configuração.

## Etapas {#steps}

Execute as seguintes etapas adicionais específicas do cluster:

### Atualizar domain.conf.bat {#update-domain-conf-bat}

1. No `domain.conf.bat`, adicione as informações de localizadores da configuração existente ao novo arquivo:

   ```text
   set "JAVA_OPTS=%JAVA_OPTS% -Doak.documentMK.maxServerTimeDiffMillis=-1"
   set "JAVA_OPTS=%JAVA_OPTS% -Dadobe.cache.cluster-locators=<ip-address-master>[22345],<ip-address-slave>[22345]"
   set "JAVA_OPTS=%JAVA_OPTS% -DentityExpansionLimit=10000"
   ```

### Configurar autenticação master-slave {#configure-master-slave-authentication}

1. Crie um novo usuário para autenticação mestre-escravo no nó mestre.
1. Nos nós subordinados, atualize a senha do usuário em `host.xml`:

   ```xml
   <server-identities>
       <secret value="Y2hhbmdlaXQ="/>
   </server-identities>
   ```

### Atualizar endereços IP no host.xml {#update-ip-addresses-in-host-xml}

1. Atualize os endereços IP dos nós mestre e subordinado em `host.xml`:

   ```xml
   <interfaces>
       <interface name="management">
           <inet-address value="${jboss.bind.address.management:<ip-address>}"/>
       </interface>
       <interface name="public">
           <inet-address value="${jboss.bind.address:<ip-address>}"/>
       </interface>
   </interfaces>
   ```

### Remover implantações da configuração de domínio {#remove-deployments-from-domain-configuration}

1. Verifique se não há seção `<deployments>` no novo arquivo `domain_<db>.xml`.
1. Não copie o seguinte bloco da configuração existente:

   ```xml
   <deployments>
       <deployment name="adobe-forms-ivs-jboss.ear" runtime-name="adobe-forms-ivs-jboss.ear"/>
       <deployment name="adobe-livecycle-cq-author.ear" runtime-name="adobe-livecycle-cq-author.ear"/>
       <deployment name="adobe-livecycle-jboss.ear" runtime-name="adobe-livecycle-jboss.ear"/>
       <deployment name="adobe-livecycle-native-jboss-x86_win32.ear" runtime-name="adobe-livecycle-native-jboss-x86_win32.ear"/>
       <deployment name="adobe-livecycle-native-jboss-x86_win64.ear" runtime-name="adobe-livecycle-native-jboss-x86_win64.ear"/>
       <deployment name="adobe-output-ivs-jboss.ear" runtime-name="adobe-output-ivs-jboss.ear"/>
       <deployment name="adobe-workspace-client.ear" runtime-name="adobe-workspace-client.ear"/>
   </deployments>
   ```

### Atualizar classe de driver na configuração de domínio {#update-driver-class-in-domain-configuration}

1. Atualize a seção de classe de driver em `domain_<db>.xml` com base no mecanismo de banco de dados:

   **MSSQL:**

   ```xml
   <xa-datasource-class>com.microsoft.sqlserver.jdbc.SQLServerXADataSource</xa-datasource-class>
   ```

   **Oracle:**

   ```xml
   <xa-datasource-class>oracle.jdbc.xa.client.OracleXADataSource</xa-datasource-class>
   ```

### Atualizar controlador de domínio em nós subordinados {#update-domain-controller-on-slave-nodes}

1. Atualize o bloco do controlador de domínio no nó subordinado em `host.xml` com o endereço IP mestre, porta `9999`, nome de usuário `slave1` e domínio `ManagementRealm`:

   ```xml
   <remote host="<ip-address>" port="9999" username="slave1" realm="ManagementRealm"/>
   ```

### Atualizar jboss-cli.xml {#update-jboss-cli-xml}

1. Atualize a entrada `<host>` em `jboss-cli.xml` nos nós mestre e escravo.
