---
title: Atualização do JBoss EAP da 7.4.10 para 7.4.23 para AEM Forms no JEE
description: Etapas para atualizar o JBoss EAP da versão 7.4.10 para a 7.4.23 para o AEM Forms em ambientes independentes do JEE.
SEO Description: Upgrade JBoss EAP from 7.4.10 to 7.4.23 for AEM Forms on JEE standalone environments.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
exl-id: 8f4c2a91-6b3d-4e7f-9c12-5d8e1f0a2b34
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms Upgrade,AEM Forms on JEE
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: d49d6117-dd89-469c-a774-cc96b7eee433
    internal-label: Administration
subfeature_v2:
  - id: b9cdd520-e7a7-4af9-a95f-296f28882b69
    internal-label: AEM Forms upgrade
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 1%
---
# Atualização do JBoss EAP da 7.4.10 para 7.4.23 para AEM Forms no JEE {#upgrade-jboss-eap-from-7-4-10-to-7-4-23}

## Visão geral {#overview}

Atualize o JBoss EAP da versão 7.4.10 para 7.4.23 em um ambiente AEM Forms no JEE independente. A atualização requer a migração dos arquivos de configuração, credenciais do banco de dados e do repositório do CRX para a nova instalação do JBoss e a execução do Configuration Manager para concluir a configuração.

## Aplica-se a {#applies-to}

Este artigo aplica-se a:

* AEM Forms no JEE executado no JBoss EAP 7.4.10 em um ambiente independente
* Modos de instalação completa e parcial no Windows e Linux

## Pré-requisitos {#prerequisites}

Antes de começar:

* Baixe o pacote JBoss 7.4.23 do [Portal de Distribuição de Software da Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fjboss-eap-7.4.23-1.0.17.zip).
* Verifique se você tem acesso administrativo ao ambiente de destino.
* Faça um backup completo da instalação existente do JBoss.

## Etapas {#steps}

Para atualizar o JBoss EAP da versão 7.4.10 para a 7.4.23, execute as seguintes etapas:

### Baixar e extrair JBoss {#download-and-extract-jboss}

1. Baixe o pacote ZIP JBoss 7.4.23 no Portal de distribuição de software da Adobe.
1. Extraia o arquivo ZIP para um diretório local.
1. Renomeie a pasta JBoss extraída para corresponder ao nome exato do diretório de instalação JBoss existente.

### Fazer backup da instalação existente {#back-up-the-existing-installation}

1. Crie um backup completo do diretório de instalação atual do JBoss.
1. Verifique se o backup inclui todos os arquivos de configuração e personalizações.

### Configurar arquivos de banco de dados {#configure-database-files}

1. Navegue até o diretório de configuração:

   * Windows: `<JBoss_Home>\standalone\configuration`
   * Linux: `<JBoss_Home>/standalone/configuration`

1. Configure os arquivos de banco de dados com base no seu modo de instalação:

   **Modo Turnkey:**

   1. Renomear `lc_mysql.xml` para `lc_turnkey.xml`.
   1. Exclua os seguintes arquivos:

      * `lc_oracle.xml`
      * `lc_mssql.xml`

   **Modo parcial turnkey:**

   1. Mantenha somente o arquivo `lc_db.xml` que corresponde ao mecanismo de banco de dados.
   1. Exclua os outros dois arquivos de configuração `lc_db.xml`.

### Atualizar credenciais do banco de dados {#update-database-credentials}

1. Abra o arquivo `lc_turnkey.xml` a partir da instalação JBoss em backup.
1. Copie os seguintes valores:

   * URL da fonte de dados
   * Usuário do banco de dados
   * Senha do banco de dados

1. Atualize as entradas correspondentes no novo arquivo `lc_turnkey.xml`.

### Migrar repositório do CRX {#migrate-crx-repository}

1. Navegue até o seguinte diretório na instalação antiga do JBoss:

   `<old_jboss>\bin\`

1. Copie a pasta `crx-quickstart`.
1. Cole a pasta em:

   `<new_jboss>\bin\`

### Executar o Gerenciador de configurações {#run-configuration-manager}

1. Inicie o ambiente JBoss atualizado.
1. Inicie o LiveCycle Configuration Manager (LCM).
1. Execute o fluxo de trabalho completo do Configuration Manager.
1. Verifique se todas as tarefas de configuração foram concluídas com êxito.

### Validação pós-atualização {#post-upgrade-validation}

Após a atualização, confirme o seguinte:

* Todos os serviços foram iniciados com êxito.
* A conectividade com o banco de dados foi verificada.
* A funcionalidade do aplicativo está validada.
