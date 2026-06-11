---
title: Atualização do JBoss EAP da 7.4.10 para 7.4.23 para AEM Forms no JEE
description: Etapas para atualizar o JBoss EAP da versão 7.4.10 para a 7.4.23 para o AEM Forms em ambientes independentes do JEE.
exl-id: 8f4c2a91-6b3d-4e7f-9c12-5d8e1f0a2b34
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms on JEE
role: User, Developer
source-git-commit: 8f8aed4c653cc286b32c83a38382f2b10370cdc8
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 3%

---

# Atualização do JBoss EAP da 7.4.10 para 7.4.23 para AEM Forms no JEE {#upgrade-jboss-eap-from-7-4-10-to-7-4-23}

## Visão geral {#overview}

Atualize o JBoss EAP da versão 7.4.10 para 7.4.23 em um ambiente AEM Forms no JEE independente. A atualização requer a migração dos arquivos de configuração, credenciais do banco de dados e do repositório do CRX para a nova instalação do JBoss e a execução do Configuration Manager para concluir a configuração.

## Aplica-se a {#applies-to}

Este artigo aplica-se a:

* AEM Forms no JEE executado no JBoss EAP 7.4.10 em um ambiente independente
* Modos de instalação completa e parcial no Windows e Linux

>[!NOTE]
>
> Se você estiver atualizando um ambiente de cluster JBoss, conclua primeiro as etapas deste artigo e execute as etapas adicionais em [Atualizar cluster JBoss EAP da versão 7.4.10 para a 7.4.23 para AEM Forms no JEE](/help/forms/using/upgrade-jboss-eap-cluster-from-7-4-10-to-7-4-23.md).

## Pré-requisitos {#prerequisites}

Antes de começar:

* Baixe o pacote JBoss 7.4.23 do [Portal de Distribuição de Software da Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html).
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
