---
title: Introdução ao Relatório de processos
seo-title: Getting Started with Process Reporting
description: As etapas que você precisa seguir para começar a usar o AEM Forms no JEE Process Reporting
seo-description: The steps you need to follow to get started with AEM Forms on JEE Process Reporting
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
exl-id: 1272e854-fa64-4bfd-b073-8fbcf210e9b5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 0%

---

# Introdução ao Relatório de processos{#getting-started-with-process-reporting}

O Relatório de processos fornece aos usuários do AEM Forms a capacidade de consultar informações sobre processos do AEM Forms que estão definidos atualmente na implementação do AEM Forms. No entanto, o Process Reporting não acessa os dados diretamente do repositório do AEM Forms. Os dados são publicados pela primeira vez no repositório do Process Reporting de forma programada (*pelo serviço ProcessDataPublisher e ProcessDataStorage* s). Os relatórios e queries no Process Reporting são gerados a partir dos dados do Process Reporting publicados no repositório. O Process Reporting é instalado como parte do módulo Forms Workflow.

Este artigo detalha as etapas para permitir a publicação de dados do AEM Forms no repositório do Process Reporting. Depois disso, você poderá usar o Relatório do Processo para executar relatórios e consultas. O artigo também aborda as opções disponíveis para configurar os serviços de Relatório de Processos.

## Pré-requisitos do Process Reporting {#process-reporting-pre-requisites}

### Eliminar processos não essenciais {#purge-non-essential-processes}

Se você estiver usando o Forms Workflow no momento, o banco de dados do AEM Forms poderá conter uma grande quantidade de dados

Os serviços de publicação do Process Reporting publicarão todos os dados do AEM Forms disponíveis no banco de dados. Isso implica que, se o banco de dados contiver dados herdados nos quais você não deseja executar relatórios e queries, todos esses dados também serão publicados no repositório, mesmo que não sejam necessários para os relatórios. É recomendável limpar esses dados antes de executar os serviços para publicar os dados no repositório do Process Reporting. Isso melhorará o desempenho do serviço do editor e do serviço que consulta os dados para relatórios.

Para obter detalhes sobre como limpar dados de processo do AEM Forms, consulte [Limpeza de dados do processo](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html).

>[!NOTE]
>
>Para obter as dicas e truques do Utilitário de limpeza, consulte o artigo da Adobe Developer Connection sobre [Limpeza de processos e trabalhos](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf).

## Configuração dos serviços de Relatório de Processos {#configuring-process-reporting-services}

### Agendar publicação de dados do processo {#schedule-process-data-publishing}

Os serviços do Process Reporting publicam dados do banco de dados do AEM Forms no repositório do Process Reporting de forma programada.

Essa operação pode consumir muitos recursos e afetar o desempenho dos servidores da AEM Forms. Você deve agendar isso fora dos slots de tempo ocupados do servidor AEM Forms.

Por padrão, a publicação de dados está agendada para ser executada todos os dias às 2:00.

Execute as seguintes etapas para alterar o cronograma de publicação:

>[!NOTE]
>
>Se você estiver executando a implementação do AEM Forms em um cluster, execute as seguintes etapas em cada nó do cluster.

1. Pare a instância do servidor do AEM Forms.
1. &#x200B;

   * (Para Windows) Abra o `[JBoss root]/bin/run.conf.bat` em um editor.
   * (Para Linux, AIX e Solaris) `[JBoss root]/bin/run.conf.sh` em um editor.

1. Adicionar o argumento JVM `-Dreporting.publisher.cron = <expression>.`

   Exemplo: A seguinte expressão cron faz com que o Process Reporting publique os dados do AEM Forms no repositório do Process Reporting a cada 5 horas:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Salve e feche o `run.conf.bat` arquivo.

1. Reinicie a instância do servidor do AEM Forms.

1. Pare a instância do servidor do AEM Forms.
1. Faça logon no Console Administrativo do WebSphere. Na árvore de navegação, clique em **Servidores** > **Servidores de aplicativos** e, no painel direito, clique no nome do servidor.

1. Em Infraestrutura do servidor, clique em **Gerenciamento de Java e processos** > **Definição de Processo**.

1. Em Propriedades adicionais, clique em **Máquina Virtual Java**.

   Na caixa Generic JVM arguments, adicione o argumento `-Dreporting.publisher.cron = <expression>.`

   **Exemplo**: A seguinte expressão cron faz com que o Process Reporting publique os dados do AEM Forms no repositório do Process Reporting a cada 5 horas:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Clique em **Aplicar**, clique em OK e, em seguida, clique em **Salvar diretamente na configuração principal**.
1. Reinicie a instância do servidor do AEM Forms.
1. Pare a instância do servidor do AEM Forms.
1. Faça logon no Console de administração do WebLogic. O endereço padrão do Console de Administração do WebLogic é `https://[hostname]:[port]/console`.
1. Em Centro de alterações, clique em **Bloquear e editar**.
1. Em Estrutura de domínio, clique em **Ambiente** > **Servidores** e, no painel direito, clique no nome do servidor gerenciado.
1. Na próxima tela, clique no botão **Configuração** guia > **Início do servidor** guia .
1. Na caixa Argumentos , adicione o argumento JVM `-Dreporting.publisher.cron = <expression>`.

   **Exemplo**: A seguinte expressão cron faz com que o Process Reporting publique os dados do AEM Forms no repositório do Process Reporting a cada 5 horas:

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Clique em **Salvar** e, em seguida, clique em **Ativar alterações**.
1. Reinicie a instância do servidor do AEM Forms.

![processdatapublisherservice](assets/processdatapublisherservice.png)

### Serviço ProcessDataStorage {#processdatastorage-service}

O serviço ProcessDataStorageProvider recebe dados do processo do serviço ProcessDataPublisher e salva os dados no repositório do Process Reporting.

Em cada ciclo de publicação, os dados são salvos em subpastas de uma pasta raiz predefinida.

Você pode usar o Console de administração para configurar a raiz (**default**: `/content/reporting/pm`) local e subpasta (**default**: `/yyyy/mm/dd/hh/mi/ss`) formato de hierarquia em que os dados do processo seriam armazenados.

#### Para configurar os locais do repositório do Process Reporting {#to-configure-the-process-reporting-repository-locations}

1. Faça logon em **Console de administração** com credenciais de administrador. O URL padrão do Console de administração é `https://'[server]:[port]'/adminui`
1. Navegar para **Início** > **Serviços** > **Aplicativos e serviços** >**Gerenciamento de serviços** e abra o **ProcessDataStorageProvider** serviço.

   ![process-data-storage-service](assets/process-data-storage-service.png)

   **PastaRaiz**

   O local do CRX dentro do qual os dados do processo seriam armazenados para relatório.

   `Default`: `/content/reporting/pm`

   **Hierarquia de pastas**

   A hierarquia de pastas dentro da qual os dados do processo seriam armazenados com base no tempo de criação do processo.

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. Clique em **Salvar**.

### Serviço ReportConfiguration {#reportconfiguration-service}

O serviço ReportConfiguration é usado pelo Process Reporting para configurar o serviço de consulta de relatório de processos.

#### Para configurar o serviço ReportingConfiguration {#to-configure-the-reportingconfiguration-service}

1. Faça logon em **Gerenciador de configuração** com credenciais de administrador do CRX. O URL padrão do Configuration Manager é `https://'[server]:[port]'/lc/system/console/configMgr`
1. Abra o **Configuração de relatórios** serviço.
1. **Número de registros**

   Ao executar um query no repositório, um resultado pode conter um grande número de registros. Se o conjunto de resultados for grande, a execução da consulta poderá consumir recursos do servidor.

   Para lidar com grandes conjuntos de resultados, o serviço ReportConfiguration divide o processamento da consulta em lotes de registros. Isso reduz a carga do sistema.

   `Default`: `1000`

   **Caminho de armazenamento CRX**

   O local do CRX dentro do qual os dados do processo devem ser armazenados para relatório.

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >Este é o mesmo local especificado na opção de configuração ProcessDataStorage **Pasta raiz**.
   >
   >
   >Se você atualizar a opção Pasta Raiz na configuração ProcessDataStorage, precisará atualizar o local do Caminho de Armazenamento CRX no serviço ReportConfiguration.

1. Clique em **Salvar** e fechar **Gerenciador de configuração CQ**.

### Serviço ProcessDataPublisher {#processdatapublisher-service}

O serviço ProcessDataPublisher importa dados do processo do banco de dados do AEM Forms e publica os dados no serviço ProcessDataStorageProvider para armazenamento.

#### Para configurar o serviço ProcessDataPublisher   {#to-configure-processdatapublisher-service-nbsp}

1. Faça logon em **Console de administração** com credenciais de administrador.

   O URL padrão é `https://'server':port]/adminui/`.

1. Navegar para **Início** > **Serviços** > **Aplicativos e serviços** >**Gerenciamento de serviços** e abra o **ProcessDataPublisher** serviço.

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**Publicar dados**

Ative essa opção para iniciar a publicação de dados do processo. Por padrão, a opção está desativada.

Habilitar Relatórios de Processos somente quando todas as configurações relacionadas aos componentes do Process Reporting estiverem configuradas adequadamente.

Como alternativa, use esta opção para desativar o processo de publicação de dados quando não for mais necessário.

`Default`: `Off`

**Intervalo do Lote (s)**

Cada vez que o serviço ProcessDataPublisher é executado, o serviço primeiro divide o tempo desde a última execução do serviço pelo Intervalo em Lote. Em seguida, o serviço processa cada intervalo de dados do AEM Forms separadamente.

Isso ajuda a controlar o tamanho dos dados que os processos do editor terminam durante cada execução (lote) em um ciclo.

Por exemplo, se o editor for executado todos os dias, em vez de processar os dados inteiros por um dia em uma única execução, por padrão, ele dividirá o processamento em 24 lotes de uma hora cada.

`Default`: `3600`

`Unit`: `Seconds`

**Tempo Limite de Bloqueio (s)**

O serviço do editor adquire um bloqueio ao iniciar o processamento de dados para que várias instâncias do editor não comecem a executar e processar dados simultaneamente.

Se um serviço do editor que adquiriu um bloqueio, estiver inativo para o número de segundos definido pelo valor Tempo Limite de Bloqueio , seu bloqueio será lançado para que outras instâncias do serviço do editor possam continuar o processamento.

`Default`: `3600`

`Unit`: `Seconds`

**Publicar dados de**

O ambiente AEM Forms contém dados do momento em que o ambiente foi configurado.

Por padrão, o serviço ProcessDataPublisher importa todos os dados do banco de dados do AEM Forms.

Dependendo das suas necessidades de relatórios, se você planeja executar relatórios e consultas sobre dados após uma determinada data e hora, é recomendável especificar a data e a hora. O serviço de publicação publicará a data a partir dessa data.

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## Acesso à interface do usuário do Process Reporting {#accessing-the-process-reporting-user-interface}

A interface do usuário para Relatórios de Processo é baseada em navegador.

Depois de configurar o Process Reporting, você pode começar a trabalhar com o Process Reporting no seguinte local da instalação do AEM Forms:

`https://<server>:<port>/lc/pr`

### Logon no Relatório do Processo {#log-in-to-process-reporting}

Ao navegar até o URL do Relatório de Processo (https://)&lt;server>:&lt;port>/lc/pr), a tela de logon é exibida.

Especifique suas credenciais para fazer logon no módulo Relatório de Processo.

>[!NOTE]
>
>Para fazer logon na interface do usuário do Process Reporting, você precisa da seguinte permissão do AEM Forms:
>
>`PERM_PROCESS_REPORTING_USER`

![Logon no Relatório do Processo](assets/capture1_new.png)

Ao fazer logon no Process Reporting, a variável **[!UICONTROL Início]** será exibida.

### Tela inicial do Relatório de Processos {#process-reporting-home-screen}

![tela inicial de relatórios do processo](assets/process-reporting-home-screen.png)

**Visualização da árvore do Process Reporting:** A exibição em árvore no lado esquerdo da tela inicial contém os itens para os módulos de Relatório de Processo.

A visualização em árvore consiste nos seguintes itens de nível superior:

**Relatórios:** Este item contém os relatórios prontos para uso que acompanham o Relatório de processos.

Para obter detalhes sobre os relatórios predefinidos, consulte [Relatórios predefinidos em andamento](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md).

**Consultas adhoc:** Este item contém opções para executar a pesquisa baseada em filtro para processos e tarefas.

Para obter detalhes sobre consultas ad hoc, consulte [Consultas ad-hoc em relatórios de processo](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md).

**Personalizado:** O nó Personalizado exibe relatórios personalizados que você cria.

Para obter o procedimento para criar e exibir relatórios personalizados, consulte [Relatórios Personalizados no Processo](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

**Barra de título do Relatório de Processos:** A barra de título Relatório de Processo contém algumas opções genéricas que podem ser usadas ao trabalhar na interface do usuário.

**Título do Relatório do Processo:** O título Relatório do processo é exibido no canto esquerdo da barra de título.

Clique no título a qualquer momento para retornar à tela inicial.

**Hora da Última Atualização:** Os dados do processo são publicados do banco de dados do AEM Forms para o repositório do Process Reporting de forma programada.

A Hora da Última Atualização exibe a última data e hora até as quais as atualizações de dados foram enviadas para o repositório do Process Reporting.

Para obter detalhes sobre o serviço de publicação de dados e como agendar esse serviço, consulte [Agendar publicação de dados do processo](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) no artigo Introdução ao Process Reporting .

**Usuário do Process Reporting:** O nome de usuário conectado é exibido à direita da Hora da última atualização.

**Lista suspensa da barra de título Relatórios de processos:** A lista suspensa no canto direito da barra de título Relatório do Processo contém as seguintes opções:

* **[!UICONTROL Sincronizar]**: Sincronize o repositório incorporado do Process Reporting com o banco de dados do AEM Forms.
* **[!UICONTROL Ajuda]**: Visualize a documentação da Ajuda em Relatórios do Processo.
* **[!UICONTROL Logout]**: Fazer logoff do Relatório do Processo
