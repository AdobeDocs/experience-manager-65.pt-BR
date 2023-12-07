---
title: Introdução aos Relatórios de processos
description: As etapas para começar a usar o AEM Forms nos relatórios do processo JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
docset: aem65
exl-id: 1272e854-fa64-4bfd-b073-8fbcf210e9b5
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 0%

---

# Introdução aos Relatórios de processos{#getting-started-with-process-reporting}

Os Relatórios de processos oferecem aos usuários do AEM Forms a capacidade de consultar informações sobre processos do AEM Forms que estão atualmente definidos na implementação do AEM Forms. No entanto, o Process Reporting não acessa dados diretamente do repositório do AEM Forms. Os dados são publicados pela primeira vez no repositório de Relatórios de processos de forma programada (*pelo serviço ProcessDataPublisher e ProcessDataStorage* s). Os relatórios e consultas em Process Reporting são gerados a partir dos dados de Process Reporting publicados no repositório. O Process Reporting é instalado como parte do módulo Forms Workflow.

Este artigo detalha as etapas para habilitar a publicação de dados do AEM Forms no repositório do Process Reporting. Depois disso, será possível usar o Process Reporting para executar relatórios e consultas. O artigo também aborda as opções disponíveis para configurar o Process Reporting Services.

## Pré-requisitos do Relatório de Processos {#process-reporting-pre-requisites}

### Limpar processos não essenciais {#purge-non-essential-processes}

Se você estiver usando o Forms Workflow, o banco de dados do AEM Forms poderá conter uma grande quantidade de dados

Os serviços de publicação do Process Reporting publicam todos os dados do AEM Forms atualmente disponíveis no banco de dados. Isso implica que, se o banco de dados contiver dados herdados nos quais você não deseja executar relatórios e consultas, todos esses dados também serão publicados no repositório, mesmo que não sejam necessários para relatórios. É recomendável limpar esses dados antes de executar os serviços para publicar os dados no repositório do Process Reporting. Isso melhora o desempenho do serviço do editor e do serviço que consulta os dados para geração de relatórios.

Para obter detalhes sobre a limpeza de dados de processo do AEM Forms, consulte [Expurgando Dados do Processo](/help/forms/using/admin-help/purging-process-data.md).

>[!NOTE]
>
>Para obter as dicas e truques do Purge Utility, consulte o artigo da Adobe Developer Connection sobre [Limpeza de processos e jobs](/help/forms/using/admin-help/purging-process-data.md).

## Configuração de serviços do Process Reporting {#configuring-process-reporting-services}

### Programar publicação de dados do processo {#schedule-process-data-publishing}

Os serviços do Process Reporting publicam dados do banco de dados do AEM Forms no repositório do Process Reporting de forma programada.

Essa operação pode consumir muitos recursos e afetar o desempenho dos servidores da AEM Forms. É recomendável agendar isso fora dos intervalos de tempo ocupados do AEM Forms Server.

Por padrão, a publicação de dados está programada para ser executada todos os dias às 2:00.

Para alterar a programação de publicação, execute as seguintes etapas:

>[!NOTE]
>
>Se estiver executando a implementação do AEM Forms em um cluster, execute as etapas a seguir em cada nó do cluster.

1. Pare a instância do AEM Forms Server.
1. &#x200B;

   * (Para Windows) Abra o `[JBoss root]/bin/run.conf.bat` em um editor.
   * (Para Linux®, AIX® e Solaris™) `[JBoss root]/bin/run.conf.sh` em um editor.

1. Adicionar o argumento JVM `-Dreporting.publisher.cron = <expression>.`

   Exemplo: a seguinte expressão cron faz com que o Process Reporting publique dados do AEM Forms no repositório do Process Reporting a cada cinco horas:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Salve e feche o `run.conf.bat` arquivo.

1. Reinicie a instância do AEM Forms Server.

1. Pare a instância do AEM Forms Server.
1. Faça logon no Console administrativo do WebSphere®. Na árvore de navegação, clique em **Servidores** > **Servidores de aplicativos** e, no painel direito, clique no nome do servidor.

1. Em Infraestrutura do servidor, clique em **Java™ e gerenciamento de processos** > **Definição do processo**.

1. Em Propriedades Adicionais, clique em **Java™ Virtual Machine**.

   Na caixa Generic JVM arguments, adicione o argumento `-Dreporting.publisher.cron = <expression>.`

   **Exemplo**: a seguinte expressão cron faz com que o Process Reporting publique dados do AEM Forms no repositório do Process Reporting a cada cinco horas:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Clique em **Aplicar**, clique em OK e em **Salvar diretamente na configuração principal**.
1. Reinicie a instância do AEM Forms Server.
1. Pare a instância do AEM Forms Server.
1. Faça logon no WebLogic Administration Console. O endereço padrão do Console de Administração do WebLogic é `https://[hostname]:[port]/console`.
1. Em Centro de alterações, clique em **Bloquear e editar**.
1. Em Estrutura do domínio, clique em **Ambiente** > **Servidores** no painel direito, clique no nome do servidor gerenciado.
1. Na próxima tela, clique na guia **Configuração** guia > **Início do servidor** guia.
1. Na caixa Argumentos, adicione o argumento JVM `-Dreporting.publisher.cron = <expression>`.

   **Exemplo**: a seguinte expressão cron faz com que o Process Reporting publique dados do AEM Forms no repositório do Process Reporting a cada cinco horas:

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Clique em **Salvar** e clique em **Ativar alterações**.
1. Reinicie a instância do AEM Forms Server.

![processdatapublisherservice](assets/processdatapublisherservice.png)

### serviço ProcessDataStorage {#processdatastorage-service}

O serviço ProcessDataStorageProvider recebe dados do processo do serviço ProcessDataPublisher e salva os dados no repositório do Process Reporting.

Em cada ciclo de publicação, os dados são salvos em subpastas de uma pasta raiz predefinida.

Você pode usar o Console de administração para configurar a raiz (**padrão**: `/content/reporting/pm`) local e subpasta (**padrão**: `/yyyy/mm/dd/hh/mi/ss`) formato de hierarquia onde os dados do processo seriam armazenados.

#### Para configurar os locais de repositório do Process Reporting {#to-configure-the-process-reporting-repository-locations}

1. Efetue logon no **Console de administração** com credenciais de administrador. O URL padrão do Console de administração é `https://'[server]:[port]'/adminui`
1. Navegue até **Início** > **Serviços** > **Aplicativos e serviços** >**Gerenciamento de serviços** e abra o **ProcessDataStorageProvider** serviço.

   ![process-data-storage-service](assets/process-data-storage-service.png)

   **PastaRaiz**

   O local do CRX no qual os dados do processo seriam armazenados para relatórios.

   `Default`: `/content/reporting/pm`

   **Hierarquia da pasta**

   A hierarquia de pastas dentro da qual os dados do processo seriam armazenados com base no tempo de criação do processo.

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. Clique em **Salvar**.

### Serviço ReportConfiguration {#reportconfiguration-service}

O serviço ReportConfiguration é usado pelo Process Reporting para configurar o serviço de consulta de relatório de processos.

#### Para configurar o serviço ReportingConfiguration {#to-configure-the-reportingconfiguration-service}

1. Efetue logon no **Gerenciador de configurações** com credenciais de administrador do CRX. O URL padrão do Configuration Manager é `https://'[server]:[port]'/lc/system/console/configMgr`
1. Abra o **Configuração de relatórios** serviço.
1. **Número de registros**

   Ao executar uma consulta no repositório, um resultado pode conter muitos registros. Se o conjunto de resultados for grande, a execução da consulta poderá consumir recursos do servidor.

   Para lidar com conjuntos de resultados grandes, o serviço ReportConfiguration divide o processamento de consulta em lotes de registros. Isso reduz a carga do sistema.

   `Default`: `1000`

   **Caminho de armazenamento do CRX**

   O local do CRX no qual os dados do processo devem ser armazenados para relatórios.

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >Esse local é o mesmo especificado na opção de configuração ProcessDataStorage **Pasta raiz**.
   >
   >
   >Se você atualizar a opção Pasta raiz na configuração ProcessDataStorage, será necessário atualizar o local do Caminho de armazenamento do CRX no serviço ReportConfiguration.

1. Clique em **Salvar** e fechar **Gerenciador de configuração do CQ**.

### Serviço ProcessDataPublisher {#processdatapublisher-service}

O serviço ProcessDataPublisher importa dados do processo do banco de dados do AEM Forms e publica os dados no serviço ProcessDataStorageProvider para armazenamento.

#### Para configurar o serviço ProcessDataPublisher   {#to-configure-processdatapublisher-service-nbsp}

1. Efetue logon no **Console de administração** com credenciais de administrador.

   O URL padrão é `https://'server':port]/adminui/`.

1. Navegue até **Início** > **Serviços** > **Aplicativos e serviços** >**Gerenciamento de serviços** e abra o **ProcessDataPublisher** serviço.

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**Publicar dados**

Habilite essa opção para iniciar a publicação dos dados do processo. A opção está desativada por padrão.

Habilite o Process Reporting somente quando todas as configurações relacionadas aos componentes do Process Reporting estiverem configuradas adequadamente.

Como alternativa, use essa opção para desativar a publicação de dados do processo quando ela não for mais necessária.

`Default`: `Off`

**Intervalo de Lote (s)**

Cada vez que o serviço ProcessDataPublisher é executado, o serviço divide pela primeira vez o tempo desde a última execução do serviço pelo Intervalo em lote. O serviço processa cada intervalo de dados do AEM Forms separadamente para ajudar a controlar o tamanho dos dados que o editor processa de ponta a ponta durante cada execução (lote) em um ciclo.

Por exemplo, se o editor é executado todos os dias, em vez de processar os dados inteiros por um dia em uma única execução, por padrão, ele divide o processamento em 24 lotes de uma hora cada.

`Default`: `3600`

`Unit`: `Seconds`

**Tempo Limite de Bloqueio (s)**

O serviço do editor adquire um bloqueio ao iniciar o processamento de dados para que várias instâncias do editor não iniciem a execução e o processamento de dados simultaneamente.

Se um serviço do publicador que adquiriu um bloqueio estiver ocioso pelo número de segundos definido pelo valor Bloquear Tempo Limite, seu bloqueio será liberado para que outras instâncias do serviço do publicador possam continuar o processamento.

`Default`: `3600`

`Unit`: `Seconds`

**Publicar dados de**

O ambiente do AEM Forms contém dados do momento em que o ambiente foi configurado.

Por padrão, o serviço ProcessDataPublisher importa todos os dados do banco de dados do AEM Forms.

Dependendo das suas necessidades de relatórios, se você planeja executar relatórios e consultas em dados após uma determinada data e hora, é recomendável especificar a data e a hora. O serviço de publicação publica a data a partir desse momento.

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## Acesso à interface do usuário do Process Reporting {#accessing-the-process-reporting-user-interface}

A interface de usuário para Relatórios de processos é baseada em navegador.

Depois de configurar o Process Reporting, você pode começar a trabalhar com o Process Reporting no seguinte local da sua instalação do AEM Forms:

`https://<server>:<port>/lc/pr`

### Faça logon para Processar relatórios {#log-in-to-process-reporting}

Ao navegar até o URL de relatórios do processo (https://)&lt;server>:&lt;port>/lc/pr), a tela de logon será exibida.

Para fazer logon no módulo Process Reporting, especifique suas credenciais.

>[!NOTE]
>
>Para fazer logon na interface do usuário do Process Reporting, é necessário ter a seguinte permissão do AEM Forms:
>
>`PERM_PROCESS_REPORTING_USER`

![Fazer logon para processar relatórios](assets/capture1_new.png)

Ao fazer logon no Process Reporting, a variável **[!UICONTROL Início]** é exibida.

### Tela inicial do Relatório de Processo {#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**Exibição de árvore do Relatório de Processo:** A exibição em árvore no lado esquerdo da tela inicial contém os itens dos módulos Process Reporting.

A exibição em árvore consiste nos seguintes itens de nível superior:

**Relatórios:** Esse item contém os relatórios prontos para uso que são enviados com o Process Reporting.

Para obter detalhes sobre os relatórios predefinidos, consulte [Relatórios predefinidos em relatórios de processo](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md).

**Consultas adhoc:** Este item contém opções para executar pesquisa baseada em filtro para processos e tarefas.

Para obter detalhes sobre consultas ad-hoc, consulte [Consultas ad-hoc em relatórios do processo](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md).

**Personalizado:** O nó Personalizado exibe relatórios personalizados que você cria.

Para obter o procedimento para criar e exibir relatórios personalizados, consulte [Relatórios personalizados em relatórios de processo](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

**Barra de título do Relatório de Processo:** A barra de título Relatórios do Processo contém algumas opções genéricas que podem ser usadas ao trabalhar na interface do usuário.

**Título do Relatório de Processo:** O título Relatório do processo é exibido no canto esquerdo da barra de título.

Clique no título a qualquer momento para voltar à tela inicial.

**Hora da última atualização:** Os dados do processo são publicados do banco de dados do AEM Forms para o repositório do Process Reporting de forma programada.

A Hora da Última Atualização exibe a última data e hora até as quais as atualizações de dados foram enviadas para o repositório do Process Reporting.

Para obter detalhes sobre o serviço de publicação de dados e como agendar esse serviço, consulte [Programar publicação de dados do processo](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) no artigo Introdução aos relatórios do processo.

**Usuário de Relatório de Processo:** O nome de usuário conectado é exibido à direita do campo Hora da última atualização.

**Lista suspensa da barra de título do Relatório de Processo:** A lista suspensa no canto direito da barra de título Relatório de processos contém as seguintes opções:

* **[!UICONTROL Sincronizar]**: sincronize o repositório incorporado Process Reporting com o banco de dados do AEM Forms.
* **[!UICONTROL Ajuda]**: visualize a documentação de ajuda em Relatórios do processo.
* **[!UICONTROL Sair]**: Efetuar logout do relatório de processo
