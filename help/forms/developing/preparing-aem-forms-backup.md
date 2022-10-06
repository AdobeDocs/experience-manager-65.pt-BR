---
title: Preparando o AEM Forms para backup
seo-title: Preparing AEM Forms for Backup
description: Saiba como usar o serviço de Backup e Restauração para entrar e sair do modo de Backup do servidor AEM Forms usando a API Java e a API do serviço da Web.
seo-description: Learn how to use the Backup and Restore service to enter and leave the Backup mode for AEM Forms server using the Java API and the Web Service API.
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
role: Developer
exl-id: aeab003d-ba64-4760-9c56-44638501e9ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2520'
ht-degree: 0%

---

# Preparando o AEM Forms para backup {#preparing-aem-forms-for-backup}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

## Sobre o serviço de backup e restauração {#about-the-backup-and-restore-service}

O serviço de backup e restauração permite que você coloque a AEM Forms em *modo de backup*, que permite a execução de backups em operação. Na verdade, o serviço de Backup e Restauração não executa um backup do AEM Forms nem restaura seu sistema. Em vez disso, coloca o servidor em estado para backups consistentes e confiáveis, permitindo que o servidor continue a ser executado. Você é responsável pelas ações de backup do Armazenamento de documentos global (GDS) e do banco de dados conectado ao servidor de formulários. O GDS é um diretório usado para armazenar arquivos usados em um processo de longa duração.

O modo de backup é um estado que o servidor insere para que os arquivos no GDS não sejam limpos enquanto ocorre um procedimento de backup. Em vez disso, os subdiretórios são criados no diretório GDS para manter um registro de arquivos a serem limpos após o fim do modo de backup salvo. Um arquivo é destinado a sobreviver a reinicializações do sistema e pode durar dias ou até anos. Esses arquivos são uma parte essencial do estado geral do servidor de formulários e podem incluir arquivos PDF, políticas ou modelos de formulário. Se algum desses arquivos for perdido ou corrompido, os processos no servidor de formulários poderão se tornar instáveis e os dados poderão ser perdidos.

Você pode optar por realizar backups de snapshot, onde normalmente entraria no modo de backup por um período e deixaria o modo de backup depois de concluir suas atividades de backup. É necessário deixar o modo de backup para que os arquivos possam ser removidos do GDS para garantir que ele não cresça desnecessariamente. Você pode deixar o modo de backup explicitamente ou esperar o tempo expirar em uma sessão de modo de backup.

Você também pode deixar seu servidor no modo de backup perpétuo, que é típico para estratégias de backup para backups contínuos ou cobertura contínua do sistema. O modo de backup contínuo indica que o sistema está sempre em modo de backup, com uma nova sessão de modo de backup iniciada assim que a sessão anterior é lançada. Quando em modo de backup contínuo, um arquivo é removido após duas sessões de modo de backup e não é mais referenciado.

Você pode usar o serviço de Backup e Restauração para adicionar aplicativos existentes ou novos aplicativos criados por você para executar backups do GDS ou do banco de dados conectado ao servidor de formulários.

>[!NOTE]
>
>Assim como em qualquer outro aspecto de sua implementação da AEM Forms, sua estratégia de backup e recuperação deve ser desenvolvida e testada em um ambiente de desenvolvimento ou de preparo antes de ser usada na produção para garantir que toda a solução funcione conforme o esperado, sem perda de dados.

Você pode executar essas tarefas usando o serviço de Backup e Restauração:

* Entre no modo de backup.
* Deixe o modo de backup.

>[!NOTE]
>
>Para obter mais informações sobre o que considerar ao executar backups para o AEM Forms, consulte [ajuda administrativa](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Backup e Restauração, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Entrando no Modo de Backup no servidor de formulários {#entering-backup-mode-on-the-forms-server}

Você entra no modo de backup para permitir backups em funcionamento de um servidor de formulários. Ao entrar no modo de backup, especifique as seguintes informações com base nos procedimentos de backup de sua organização:

* Um rótulo exclusivo para identificar a sessão do modo de backup que pode ser útil para seus processos de backup.
* A hora de conclusão do procedimento de backup.
* Um sinalizador para indicar se deve estar em modo de backup contínuo, o que é útil somente se você estiver executando backups contínuos.

Antes de gravar aplicativos para entrar no modo de backup, é recomendável compreender os procedimentos de backup que serão usados depois de colocar o servidor de formulários no modo de backup. Para obter mais informações sobre o que considerar ao executar backups para o AEM Forms, consulte [ajuda administrativa](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Backup e Restauração, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para criar um aplicativo que entre no modo de backup, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto cliente BackupService.
1. Determine um rótulo exclusivo, a quantidade de tempo para executar o backup e se deve estar em modo de backup contínuo.
1. Entre no modo de backup.
1. (Opcional) Recupere informações sobre a sessão do modo de backup no servidor.
1. Execute o backup do GDS (Armazenamento de dados global) e do banco de dados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Esses arquivos são importantes para incluir no seu projeto para compilar seu código corretamente e usar a API do serviço de backup e restauração.

Para obter informações sobre a localização desses arquivos, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de API do cliente BackupService**

Para sair programaticamente do modo de backup, crie um objeto cliente BackupService para usar a API do Serviço de Backup e Restauração.

**Decida com base em um rótulo exclusivo, determine a quantidade de tempo para executar o backup e decida se deve estar em modo de backup contínuo**

Antes de entrar no modo de backup, você deve decidir sobre um rótulo exclusivo, determinar o tempo que deseja alocar para executar o backup e decidir se deseja que o servidor de formulários permaneça no modo de backup. Essas considerações são importantes para integrar-se aos procedimentos de backup estabelecidos pela organização. (Consulte [ajuda administrativa](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Entre no modo de backup**

Entre no modo de backup com os parâmetros que são consistentes com os procedimentos de backup em sua organização.

**Recuperar informações sobre a sessão do modo de backup no servidor**

Depois de entrar no modo de backup, é possível recuperar informações sobre a sessão. Essas informações podem ser usadas para integrar com seus procedimentos de backup

**Execute o backup do GDS e do banco de dados**

Depois de entrar no modo de backup com êxito, é possível executar um backup do Global Document Storage (GDS) e do banco de dados ao qual o servidor de formulários está conectado. Esta etapa é específica da sua organização, pois é possível executar essa etapa manualmente ou executar outras ferramentas para executar o procedimento de backup.

### Entre no modo de backup usando a API Java {#enter-backup-mode-using-the-java-api}

Entre no modo de backup usando a API do Serviço de Backup e Restauração:

1. Incluir arquivos de projeto

   Inclua os arquivos JAR do cliente necessários, como adobe-backup-restore-client-sdk.jar, no caminho de classe do seu projeto Java. Para criar o aplicativo cliente Java, os seguintes arquivos JAR devem ser adicionados ao caminho da classe do seu projeto:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
   * jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

1. Criar um objeto de API do cliente BackupService

   Use um `ServiceClientFactory` e o objeto da API do cliente BackupService.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão. (Consulte [Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crie um `BackupService` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Decida com base em um rótulo exclusivo, determine a quantidade de tempo para executar o backup e decida se deve estar em modo de backup contínuo

   Decida sobre um rótulo exclusivo, determine o tempo que deseja alocar para executar o backup e decida se deseja que o servidor de formulários permaneça no modo de backup contínuo.

1. Entre no modo de backup

   Entre no modo de backup chamando o `enterBackupMode` com os seguintes parâmetros:

   * A `String` que especifica um rótulo exclusivo legível que identifica a sessão do modo de backup. É recomendável não usar espaços ou caracteres que não possam ser codificados no formato XML.
   * Um `int` que especifica o número de minutos para permanecer no modo de backup. Você pode especificar um valor de `1` para `10080` (o número de minutos em uma semana). Esse valor é ignorado ao usar o modo de backup contínuo.
   * A `Boolean` que especifica se deve estar em modo de backup contínuo. Um valor de `True` especifica para estar em modo de backup contínuo. Quando no modo de backup contínuo, o valor especificado para o número de minutos para permanecer no modo de backup é ignorado.

      O modo de backup contínuo significa que uma nova sessão de modo de backup é iniciada após a conclusão da atual. Um valor de `False` significa que o modo de backup contínuo não é usado e, depois de sair do modo de backup, a limpeza de arquivos do GDS é retomada.

1. Recuperar informações sobre a sessão do modo de backup no servidor

   Recupere informações usando o `BackupModeEntryResult` objeto que é retornado após chamar o `enterBackupMode` método . As informações que podem ser recuperadas depois de entrar no modo de backup podem ser úteis para integração com seus procedimentos de backup. Por exemplo, o rótulo, a ID de backup e a hora de início podem ser úteis como entrada para nomes de arquivo para o procedimento de backup.

1. Execute o backup do GDS e do banco de dados

   Faça backup do armazenamento global de documentos (GDS) e do banco de dados ao qual o servidor de formulários está conectado. As ações para executar o backup não fazem parte do SDK da AEM Forms e podem incluir até mesmo etapas manuais específicas aos procedimentos de backup em sua organização.

### Entre no modo de backup usando a API do serviço da Web {#enter-backup-mode-using-the-web-service-api}

Entre no modo de backup usando o serviço da Web fornecido pela API do Serviço de Backup e Restauração:

1. Incluir arquivos de projeto

   * Crie um conjunto de clientes Microsoft .NET que consuma o WSDL da API do Serviço de Backup e Restauração.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar um objeto de API do cliente BackupService

   Usando o assembly do cliente Microsoft .NET, crie um `BackupServiceService` chamando seu construtor padrão e especificando as credenciais usando a `Credentials` método .

1. Decida com base em um rótulo exclusivo, determine a quantidade de tempo para executar o backup e decida se deve estar em modo de backup contínuo

   Decida sobre um rótulo exclusivo, determine o tempo que deseja alocar para executar o backup e decida se deseja que o servidor de formulários permaneça no modo de backup contínuo.

1. Entre no modo de backup

   Para entrar no modo de backup, chame o método enterBackupMode e passe os seguintes valores:

   * A `String` que especifica um rótulo exclusivo legível que identifica a sessão do modo de backup. É recomendável não usar espaços ou caracteres que não possam ser codificados no formato XML.
   * A `Uint32` que especifica o número de minutos para permanecer no modo de backup. Você pode especificar um valor de `1` para `10080` (número de minutos em uma semana). Esse valor é ignorado ao usar o modo de backup contínuo.
   * A `Boolean` que especifica se deve estar em modo de backup contínuo. Um valor de `True` especifica para estar em modo de backup contínuo. Quando no modo de backup contínuo, o valor especificado para o número de minutos para permanecer no modo de backup é ignorado. O modo de backup contínuo significa que uma nova sessão de modo de backup é iniciada após a conclusão da atual.

      Um valor de `False` significa que o modo de backup contínuo não é usado e, depois de sair do modo de backup, a limpeza de arquivos do GDS é retomada.

1. Recuperar informações sobre a sessão do modo de backup no servidor

   Recupere informações sobre a sessão do modo de backup após invocar o método enterBackupMode a partir de BackupModeEntryResult retornado para verificar se foi bem-sucedido. As informações que podem ser recuperadas depois de entrar no modo de backup podem ser úteis para integração com seus procedimentos de backup. Por exemplo, o rótulo, a ID de backup e a hora de início podem ser úteis como entrada para nomes de arquivo para o procedimento de backup.

1. Execute o backup do GDS e do banco de dados

   Faça backup do armazenamento global de documentos (GDS) e do banco de dados ao qual o servidor de formulários está conectado. As ações para executar o backup não fazem parte do SDK da AEM Forms e podem incluir até mesmo etapas manuais específicas aos procedimentos de backup em sua organização.

## Deixando o Modo de Backup no servidor de formulários {#leaving-backup-mode-on-the-forms-server}

Você deixa o modo de backup para que o servidor de formulários retome a limpeza de arquivos do GDS (Global Document Storage) no servidor de formulários.

Antes de gravar aplicativos para entrar no modo de licença, é recomendável compreender os procedimentos de backup usados com o AEM Forms. Para obter mais informações sobre o que considerar ao executar backups para o AEM Forms, consulte [ajuda administrativa](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Backup e Restauração, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para sair do modo de backup, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto cliente BackupService.
1. Deixe o modo de backup.
1. (Opcional) Recupere informações sobre a sessão de modo de backup que estava sendo executada no servidor de formulários.

**Incluir arquivos de projeto**

Inclua todos os arquivos necessários no projeto de desenvolvimento. Esses arquivos são importantes para compilar seu código corretamente e usar a API do serviço de backup e restauração.

Para obter informações sobre a localização desses arquivos, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de API do cliente BackupService**

Para sair programaticamente do modo de backup, crie um objeto cliente BackupService para usar a API do Serviço de Backup e Restauração.

**Sair do modo de backup**

Deixe o modo de backup para retomar a limpeza normal dos arquivos do GDS (Global Document Storage, Armazenamento Global de Documentos). Antes de sair do modo de backup, verifique se os procedimentos de backup foram concluídos.

**Recuperar informações sobre a sessão do modo de backup que terminou**

Depois de sair do modo de backup, você pode recuperar informações sobre a sessão. Essas informações podem ser usadas para integrar com seus procedimentos de backup.

### Deixe o modo de backup usando a API Java {#leave-backup-mode-using-the-java-api}

Deixe o modo de backup usando a API do Serviço de Backup e Restauração (Java):

1. Incluir arquivos de projeto

   Inclua os arquivos JAR do cliente necessários, como adobe-backup-restore-client-sdk.jar, no caminho de classe do seu projeto Java. Para criar um aplicativo cliente Java, os seguintes arquivos JAR devem ser adicionados ao caminho da classe do seu projeto:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
   * jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

1. Criar um objeto de API do cliente BackupService

   Use um `ServiceClientFactory` e o objeto da API do cliente BackupService.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão. (Consulte [Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crie um `BackupService` usando seu construtor e passando o `ServiceClientFactory` objeto como parâmetro.

1. Entre no modo de backup

   Deixe o modo de backup chamando o `leaveBackupMode` método .

1. Recuperar informações sobre a sessão do modo de backup no servidor

   Recupere informações sobre a operação usando o `BackupModeResult` objeto que é retornado. As informações que podem ser recuperadas depois de entrar no modo de backup podem ser úteis para integração com seus procedimentos de backup. Por exemplo, o rótulo, a ID de backup e a hora de início podem ser úteis como entrada para nomes de arquivo para o procedimento de backup.

### Deixe o modo de backup usando a API do serviço da Web {#leave-backup-mode-using-the-web-service-api}

Deixe o modo de backup usando a API do Serviço de Backup e Restauração (serviço da Web):

1. Incluir arquivos de projeto

   Para usar serviços da Web, você deve incluir os arquivos proxy. Siga estas etapas para configurar seu projeto para usar a API do serviço de backup e restauração como um serviço da Web.

   * Crie um conjunto de clientes Microsoft .NET que consuma o WSDL da API do Serviço de Backup e Restauração.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar um objeto de API do cliente BackupService

   Usando o assembly do cliente Microsoft .NET, crie um `BackupServiceService` chamando seu construtor padrão.

1. Entre no modo de backup

   Deixe o modo de backup chamando o `leaveBackupMode` operação de serviço da Web.

1. Recuperar informações sobre a sessão do modo de backup no servidor

   Recupere o identificador do modo de backup após a operação para verificar se foi bem-sucedida. As informações que podem ser recuperadas após sair do modo de backup podem ser úteis para integração com seus procedimentos de backup.
