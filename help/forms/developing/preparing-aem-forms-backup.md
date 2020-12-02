---
title: Preparação do AEM Forms para backup
seo-title: Preparação do AEM Forms para backup
description: 'null'
seo-description: nulo
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 0%

---


# Preparando o AEM Forms para backup {#preparing-aem-forms-for-backup}

## Sobre o Serviço de Backup e Restauração {#about-the-backup-and-restore-service}

O serviço de Backup e Restauração permite que você coloque a AEM Forms no *modo de backup*, que permite a execução de backups instantâneos. O serviço de Backup e Restauração não executa, na verdade, um backup da AEM Forms ou restaura seu sistema. Em vez disso, coloca o servidor em um estado para oferecer backups consistentes e confiáveis e, ao mesmo tempo, permitir que o servidor continue em execução. Você é responsável pelas ações de backup do Armazenamento Global do Documento (GDS) e do banco de dados conectado ao servidor de formulários. O GDS é um diretório usado para armazenar arquivos usados em um processo de longa duração.

O modo de backup é um estado inserido pelo servidor para que os arquivos no GDS não sejam removidos enquanto um procedimento de backup estiver sendo executado. Em vez disso, os subdiretórios são criados no diretório GDS para manter um registro de arquivos a serem removidos após o fim do modo de backup salvo. Um arquivo é destinado a sobreviver a reinicializações do sistema e pode durar dias, ou até mesmo anos. Esses arquivos são uma parte essencial do estado geral do servidor de formulários e podem incluir arquivos PDF, políticas ou modelos de formulário. Se algum desses arquivos for perdido ou corrompido, os processos no servidor de formulários poderão ficar instáveis e os dados poderão ser perdidos.

Você pode optar por executar backups de snapshot, onde você normalmente entraria no modo de backup por um período e deixaria o modo de backup depois de concluir as atividades de backup. É necessário deixar o modo de backup para que os arquivos possam ser removidos do GDS para garantir que não fiquem grandes desnecessariamente. Você pode deixar o modo de backup explicitamente ou aguardar o tempo de expiração em uma sessão de modo de backup.

Você também pode deixar o servidor no modo de backup perpétuo, que é típico para estratégias de backup para backups em andamento ou cobertura contínua do sistema. O modo de backup em andamento indica que o sistema está sempre no modo de backup, com uma nova sessão de modo de backup iniciada assim que a sessão anterior é lançada. Quando estiver no modo de backup contínuo, um arquivo será removido após duas sessões de modo de backup e não será mais referenciado.

Você pode usar o serviço de Backup e Restauração para adicionar aos aplicativos existentes ou aos novos aplicativos criados para executar backups do GDS ou do banco de dados conectado ao servidor de formulários.

>[!NOTE]
>
>Assim como em qualquer outro aspecto da implementação do AEM Forms, sua estratégia de backup e recuperação deve ser desenvolvida e testada em um ambiente de desenvolvimento ou armazenamento temporário antes de ser usada na produção para garantir que toda a solução esteja funcionando como esperado, sem perda de dados.

Você pode executar essas tarefas usando o serviço de Backup e Restauração:

* Entre no modo de backup.
* Deixe o modo de backup.

>[!NOTE]
>
>Para obter mais informações sobre o que considerar ao executar backups para AEM Forms, consulte [ajuda administrativa](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Backup e Restauração, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Entrando no Modo de Backup no servidor de formulários {#entering-backup-mode-on-the-forms-server}

Você entra no modo de backup para permitir backups instantâneos de um servidor de formulários. Ao entrar no modo de backup, você especifica as seguintes informações com base nos procedimentos de backup de sua organização:

* Um rótulo exclusivo para identificar a sessão do modo de backup que pode ser útil para seus processos de backup.
* A hora da conclusão do procedimento de backup.
* Um sinalizador para indicar se você deve estar no modo de backup contínuo, o que é útil somente se você estiver executando backups em andamento.

Antes de gravar aplicativos para entrar no modo de backup, é recomendável que você entenda os procedimentos de backup que serão usados depois de colocar o servidor de formulários no modo de backup. Para obter mais informações sobre o que considerar ao executar backups para AEM Forms, consulte [ajuda administrativa](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Backup e Restauração, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para criar um aplicativo que entre no modo de backup, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto cliente BackupService.
1. Determine um rótulo exclusivo, a quantidade de tempo para executar o backup e se deve estar no modo de backup contínuo.
1. Entre no modo de backup.
1. (Opcional) Recupere informações sobre a sessão do modo de backup no servidor.
1. Execute o backup do GDS (Global Data Store) e do banco de dados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Esses arquivos são importantes para serem incluídos no seu projeto para a compilação correta do código e o uso da API Serviço de Backup e Restauração.

Para obter informações sobre a localização desses arquivos, consulte [Incluindo os arquivos da biblioteca Java da AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de API do Cliente BackupService**

Para sair programaticamente do modo de backup, crie um objeto cliente BackupService para usar a API Serviço de Backup e Restauração.

**Decida sobre uma etiqueta exclusiva, determine a quantidade de tempo para executar o backup e decida se deve estar no modo de backup contínuo**

Antes de entrar no modo de backup, você deve decidir sobre uma etiqueta exclusiva, determinar o tempo que deseja alocar para executar o backup e decidir se deseja que o servidor de formulários permaneça no modo de backup. Essas considerações são importantes para a integração com os procedimentos de backup estabelecidos pela sua organização. (Consulte [ajuda administrativa](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Entrar no modo de backup**

Insira o modo de backup com os parâmetros que são consistentes com os procedimentos de backup em sua organização.

**Recuperar informações sobre a sessão do modo de backup no servidor**

Depois de entrar no modo de backup, você pode recuperar informações sobre a sessão. Essas informações podem ser usadas para integração com seus procedimentos de backup

**Execute o backup do GDS e do banco de dados**

Depois de entrar com êxito no modo de backup, é possível executar um backup do GDS (Global Documento Armazenamento) e do banco de dados ao qual o servidor de formulários está conectado. Esta etapa é específica da sua organização, já que você pode executar essa etapa manualmente ou outras ferramentas para executar o procedimento de backup.

### Insira o modo de backup usando a API Java {#enter-backup-mode-using-the-java-api}

Entre no modo de backup usando a API Serviço de Backup e Restauração:

1. Incluir arquivos de projeto

   Inclua os arquivos JAR do cliente necessários, como adobe-backup-restore-client-sdk.jar, no caminho de classe do seu projeto Java. Para criar o aplicativo cliente Java, os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (necessário se a AEM Forms estiver implantada no JBoss Application Server)
   * jbossall-client.jar (necessário se o AEM Forms estiver implantado no JBoss Application Server)

1. Criar um objeto de API do Cliente BackupService

   Use um objeto `ServiceClientFactory` e o objeto da API do cliente BackupService juntos.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão. (Consulte [Definição das propriedades de ligação](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crie um objeto `BackupService` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Decida sobre uma etiqueta exclusiva, determine a quantidade de tempo para executar o backup e decida se deve estar no modo de backup contínuo

   Decida sobre uma etiqueta exclusiva, determine o tempo que deseja alocar para executar o backup e decida se deseja que o servidor de formulários permaneça no modo de backup contínuo.

1. Entrar no modo de backup

   Digite o modo de backup chamando o método `enterBackupMode` com os seguintes parâmetros:

   * Um valor `String` que especifica um rótulo exclusivo legível por humanos que identifica a sessão do modo de backup. É recomendável que você não use espaços ou caracteres que não possam ser codificados no formato XML.
   * Um valor `int` que especifica o número de minutos para permanecer no modo de backup. Você pode especificar um valor de `1` a `10080` (o número de minutos em uma semana). Esse valor é ignorado ao usar o modo de backup contínuo.
   * Um valor `Boolean` que especifica se deve estar no modo de backup contínuo. Um valor de `True` especifica para estar no modo de backup contínuo. Quando estiver no modo de backup contínuo, o valor especificado para o número de minutos para permanecer no modo de backup será ignorado.

      O modo de backup contínuo significa que uma nova sessão de modo de backup é iniciada após a sessão atual ser concluída. Um valor de `False` significa que o modo de backup contínuo não é usado e, após sair do modo de backup, a remoção de arquivos do GDS é retomada.

1. Recuperar informações sobre a sessão do modo de backup no servidor

   Recupere informações usando o objeto `BackupModeEntryResult` que é retornado após chamar o método `enterBackupMode`. As informações que podem ser recuperadas depois que você entra no modo de backup podem ser úteis para integração com seus procedimentos de backup. Por exemplo, a etiqueta, a ID de backup e a hora do start podem ser úteis como entrada para nomes de arquivos para o procedimento de backup.

1. Execute o backup do GDS e do banco de dados

   Faça backup do GDS (Global Documento Armazenamento) e do banco de dados ao qual seu servidor de formulários está conectado. As ações para executar o backup não fazem parte do SDK da AEM Forms e podem incluir até mesmo etapas manuais específicas aos procedimentos de backup em sua organização.

### Insira o modo de backup usando a API de serviço da Web {#enter-backup-mode-using-the-web-service-api}

Entre no modo de backup usando o serviço da Web fornecido pela API de Serviço de Backup e Restauração:

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma a WSDL da API de Serviço de Backup e Restauração.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar um objeto de API do Cliente BackupService

   Usando o assembly do cliente Microsoft .NET, crie um objeto `BackupServiceService` chamando seu construtor padrão e especifique as credenciais usando o método `Credentials`.

1. Decida sobre uma etiqueta exclusiva, determine a quantidade de tempo para executar o backup e decida se deve estar no modo de backup contínuo

   Decida sobre uma etiqueta exclusiva, determine o tempo que deseja alocar para executar o backup e decida se deseja que o servidor de formulários permaneça no modo de backup contínuo.

1. Entrar no modo de backup

   Para entrar no modo de backup, chame o método enterBackupMode e passe os seguintes valores:

   * Um valor `String` que especifica um rótulo exclusivo legível por humanos que identifica a sessão do modo de backup. É recomendável que você não use espaços ou caracteres que não possam ser codificados no formato XML.
   * Um valor `Uint32` que especifica o número de minutos para permanecer no modo de backup. Você pode especificar um valor de `1` a `10080` (número de minutos em uma semana). Esse valor é ignorado ao usar o modo de backup contínuo.
   * Um valor `Boolean` que especifica se deve estar no modo de backup contínuo. Um valor de `True` especifica para estar no modo de backup contínuo. Quando estiver no modo de backup contínuo, o valor especificado para o número de minutos para permanecer no modo de backup será ignorado. O modo de backup contínuo significa que uma nova sessão de modo de backup é iniciada após a sessão atual ser concluída.

      Um valor de `False` significa que o modo de backup contínuo não é usado e, após sair do modo de backup, a remoção de arquivos do GDS é retomada.

1. Recuperar informações sobre a sessão do modo de backup no servidor

   Recupere informações sobre a sessão do modo de backup depois de chamar o método enterBackupMode do BackupModeEntryResult que é retornado para verificar se foi bem-sucedido. As informações que podem ser recuperadas depois que você entra no modo de backup podem ser úteis para integração com seus procedimentos de backup. Por exemplo, a etiqueta, a ID de backup e a hora do start podem ser úteis como entrada para nomes de arquivos para o procedimento de backup.

1. Execute o backup do GDS e do banco de dados

   Faça backup do GDS (Global Documento Armazenamento) e do banco de dados ao qual seu servidor de formulários está conectado. As ações para executar o backup não fazem parte do SDK da AEM Forms e podem incluir até mesmo etapas manuais específicas aos procedimentos de backup em sua organização.

## Deixando o Modo de Backup no servidor de formulários {#leaving-backup-mode-on-the-forms-server}

Deixe o modo de backup para que o servidor de formulários continue a remoção de arquivos do GDS (Armazenamento Global do Documento) no servidor de formulários.

Antes de gravar aplicativos para entrar no modo de licença, é recomendável que você entenda os procedimentos de backup usados com a AEM Forms. Para obter mais informações sobre o que considerar ao executar backups para AEM Forms, consulte [ajuda administrativa](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Backup e Restauração, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para sair do modo de backup, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto cliente BackupService.
1. Deixe o modo de backup.
1. (Opcional) Recupere informações sobre a sessão do modo de backup que estava sendo executada no servidor de formulários.

**Incluir arquivos de projeto**

Inclua todos os arquivos necessários em seu projeto de desenvolvimento. Esses arquivos são importantes para a compilação correta do código e o uso da API Serviço de Backup e Restauração.

Para obter informações sobre a localização desses arquivos, consulte [Incluindo os arquivos da biblioteca Java da AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de API do Cliente BackupService**

Para sair programaticamente do modo de backup, crie um objeto cliente BackupService para usar a API Serviço de Backup e Restauração.

**Sair do modo de backup**

Deixe o modo de backup para retomar a limpeza normal dos arquivos do Armazenamento Global do Documento (GDS). Antes de sair do modo de backup, verifique se os procedimentos de backup foram concluídos.

**Recuperar informações sobre a sessão do modo de backup que terminou**

Depois de sair do modo de backup, você pode recuperar informações sobre a sessão. Essas informações podem ser usadas para integração com seus procedimentos de backup.

### Deixe o modo de backup usando a API Java {#leave-backup-mode-using-the-java-api}

Deixe o modo de backup usando a API Serviço de Backup e Restauração (Java):

1. Incluir arquivos de projeto

   Inclua os arquivos JAR do cliente necessários, como adobe-backup-restore-client-sdk.jar, no caminho de classe do seu projeto Java. Para criar o aplicativo cliente Java, os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (necessário se a AEM Forms estiver implantada no JBoss Application Server)
   * jbossall-client.jar (necessário se o AEM Forms estiver implantado no JBoss Application Server)

1. Criar um objeto de API do Cliente BackupService

   Use um objeto `ServiceClientFactory` e o objeto da API do cliente BackupService juntos.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão. (Consulte [Definição das propriedades de ligação](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crie um objeto `BackupService` usando seu construtor e transmitindo o objeto `ServiceClientFactory` como parâmetro.

1. Entrar no modo de backup

   Deixe o modo de backup chamando o método `leaveBackupMode`.

1. Recuperar informações sobre a sessão do modo de backup no servidor

   Obtenha informações sobre a operação usando o objeto `BackupModeResult` que é retornado. As informações que podem ser recuperadas depois que você entra no modo de backup podem ser úteis para integração com seus procedimentos de backup. Por exemplo, a etiqueta, a ID de backup e a hora do start podem ser úteis como entrada para nomes de arquivos para o procedimento de backup.

### Deixe o modo de backup usando a API de serviço da Web {#leave-backup-mode-using-the-web-service-api}

Deixe o modo de backup usando a API Serviço de Backup e Restauração (serviço da Web):

1. Incluir arquivos de projeto

   Para usar os serviços da Web, você deve certificar-se de incluir os arquivos proxy. Siga estas etapas para configurar seu projeto para usar a API de Serviço de Backup e Restauração como um serviço da Web.

   * Crie um assembly de cliente Microsoft .NET que consuma a WSDL da API de Serviço de Backup e Restauração.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar um objeto de API do Cliente BackupService

   Usando o assembly do cliente Microsoft .NET, crie um objeto `BackupServiceService` chamando seu construtor padrão.

1. Entrar no modo de backup

   Deixe o modo de backup chamando a operação `leaveBackupMode` do serviço da Web.

1. Recuperar informações sobre a sessão do modo de backup no servidor

   Recupere o identificador do modo de backup após a operação para verificar se foi bem-sucedida. As informações que podem ser recuperadas após sair do modo de backup podem ser úteis para integração com seus procedimentos de backup.

