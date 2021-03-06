---
title: Introdução ao Process Relatórios
seo-title: Introdução ao Process Relatórios
description: As etapas que você precisa seguir para começar a usar a AEM Forms no Relatórios JEE Process
seo-description: As etapas que você precisa seguir para começar a usar a AEM Forms no Relatórios JEE Process
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 0%

---


# Introdução ao Relatórios de processo{#getting-started-with-process-reporting}

O Process Relatórios oferece aos usuários da AEM Forms a capacidade de query de informações sobre os processos da AEM Forms que estão atualmente definidos na implementação da AEM Forms. Entretanto, o Process Relatórios não acessa dados diretamente do repositório AEM Forms. Os dados são publicados pela primeira vez no repositório de Relatórios do Processo de forma programada (*pelo serviço ProcessDataPublisher e ProcessDataStorage* s). Os relatórios e query em andamento são gerados a partir dos dados de Relatórios do processo publicados no repositório. O Relatórios de processo é instalado como parte do módulo Forms Workflow.

Este artigo detalha as etapas para permitir a publicação de dados da AEM Forms no repositório do Process Relatórios. Depois disso, você poderá usar o Processar Relatórios para executar relatórios e query. O artigo também aborda as opções disponíveis para configurar os serviços de Relatórios do Processo.

## Pré-requisitos do Relatórios de processamento {#process-reporting-pre-requisites}

### Expurgar processos não essenciais {#purge-non-essential-processes}

Se você estiver usando o Forms Workflow no momento, o banco de dados AEM Forms pode conter uma grande quantidade de dados

Os serviços de publicação de Relatórios do Processo publicarão todos os dados da AEM Forms disponíveis no momento no banco de dados. Isso implica que, se o banco de dados contiver dados herdados nos quais você não deseja executar relatórios e query, todos esses dados também serão publicados no repositório, mesmo que não sejam necessários para o relatórios. É recomendável expurgar esses dados antes de executar os serviços para publicar os dados no repositório do Process Relatórios. Isso melhorará o desempenho do serviço do editor e do serviço que query os dados para o relatórios.

Para obter detalhes sobre como expurgar dados de processo do AEM Forms, consulte [Expurgando Dados de Processo](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html).

>[!NOTE]
>
>Para obter dicas e truques do Utilitário de Expurgação, consulte o artigo da Adobe Developer Connection sobre [Expurgando processos e trabalhos](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf).

## Configurando os serviços de Relatórios do processo {#configuring-process-reporting-services}

### Agendar publicação de dados do processo {#schedule-process-data-publishing}

Os serviços de Relatórios do Processo publicam dados do banco de dados da AEM Forms no repositório do Relatórios do Processo de forma programada.

Essa operação pode consumir muitos recursos e afetar o desempenho dos servidores AEM Forms. É recomendável agendar isso fora dos horários ocupados do servidor AEM Forms.

Por padrão, a publicação de dados está programada para ser executada todos os dias às 2h00.

Execute as seguintes etapas para alterar o cronograma de publicação:

>[!NOTE]
>
>Se você estiver executando sua implementação do AEM Forms em um cluster, execute as seguintes etapas em cada nó do cluster.

1. Pare a instância do servidor AEM Forms.
1. &#x200B;

   * (Para Windows) Abra o arquivo `[JBoss root]/bin/run.conf.bat` em um editor.
   * (Para Linux, AIX e Solaris) `[JBoss root]/bin/run.conf.sh` em um editor.

1. Adicione o argumento JVM `-Dreporting.publisher.cron = <expression>.`

   Exemplo: A seguinte expressão cron faz com que o Process Relatórios publique dados do AEM Forms no repositório do Process Relatórios a cada 5 horas:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Salve e feche o arquivo `run.conf.bat`.

1. Reinicie a instância do servidor AEM Forms.

1. Pare a instância do servidor AEM Forms.
1. Faça logon no Console administrativo do WebSphere. Na árvore de navegação, clique em **Servidores** > **Servidores de aplicativos** e, no painel direito, clique no nome do servidor.

1. Em Infraestrutura do servidor, clique em **Java and Process Management** > **Definição do processo**.

1. Em Propriedades adicionais, clique em **Java Virtual Machine**.

   Na caixa Argumentos JVM genéricos, adicione o argumento `-Dreporting.publisher.cron = <expression>.`

   **Exemplo**: A seguinte expressão cron faz com que o Process Relatórios publique dados do AEM Forms no repositório do Process Relatórios a cada 5 horas:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Clique em **Aplicar**, clique em OK e em **Salvar diretamente na configuração principal**.
1. Reinicie a instância do servidor AEM Forms.
1. Pare a instância do servidor AEM Forms.
1. Faça logon no Console de administração do WebLogic. O endereço padrão do Console de administração do WebLogic é `https://[hostname]:[port]/console`.
1. Em Centro de alterações, clique em **Bloquear e editar**.
1. Em Estrutura do domínio, clique em **Ambiente** > **Servidores** e, no painel direito, clique no nome do servidor gerenciado.
1. Na tela seguinte, clique na guia **Configuração** > **Start do servidor**.
1. Na caixa Argumentos, adicione o argumento JVM `-Dreporting.publisher.cron = <expression>`.

   **Exemplo**: A seguinte expressão cron faz com que o Process Relatórios publique dados do AEM Forms no repositório do Process Relatórios a cada 5 horas:

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Clique em **Salvar** e, em seguida, clique em **Ativar alterações**.
1. Reinicie a instância do servidor AEM Forms.

![processamento datapubiterservice](assets/processdatapublisherservice.png)

### Serviço ProcessDataStorage {#processdatastorage-service}

O serviço ProcessDataStorageProvider recebe dados do processo do serviço ProcessDataPublisher e salva os dados no repositório do Relatórios Process.

Em cada ciclo de publicação, os dados são salvos em subpastas de uma pasta raiz predefinida.

Você pode usar o console Administração para configurar a raiz (**default**: `/content/reporting/pm`) localização e subpasta (**predefinição**: `/yyyy/mm/dd/hh/mi/ss`) formato de hierarquia no qual os dados do processo seriam armazenados.

#### Para configurar os locais do repositório do Process Relatórios {#to-configure-the-process-reporting-repository-locations}

1. Faça logon em **Console de administração** com credenciais de administrador. O URL padrão do Console de administração é `https://'[server]:[port]'/adminui`
1. Navegue até **Início** > **Serviços** > **Aplicações e Serviços** >**Gestão de Serviços** e abra o serviço **ProcessDataStorageProvider**.

   ![process-data-armazenamento-service](assets/process-data-storage-service.png)

   **PastadaRaiz**

   O local CRX dentro do qual os dados do processo seriam armazenados para o relatórios.

   `Default`: `/content/reporting/pm`

   **Hierarquia da pasta**

   A hierarquia de pastas dentro da qual os dados do processo seriam armazenados com base no tempo de criação do processo.

   `Default`:  `/yyyy/mm/dd/hh/mi/ss`

1. Clique em **Salvar**.

### Serviço ReportConfiguration {#reportconfiguration-service}

O serviço ReportConfiguration é usado pelo Process Relatórios para configurar o serviço de query do relatórios do processo.

#### Para configurar o serviço ReportingConfiguration {#to-configure-the-reportingconfiguration-service}

1. Faça logon em **Configuration Manager** com credenciais de administrador do CRX. O URL padrão do Configuration Manager é `https://'[server]:[port]'/lc/system/console/configMgr`
1. Abra o serviço **ReportingConfiguration**.
1. **Número de registros**

   Ao executar um query no repositório, um resultado pode conter potencialmente um grande número de registros. Se o conjunto de resultados for grande, a execução do query poderá consumir recursos do servidor.

   Para lidar com grandes conjuntos de resultados, o serviço ReportConfiguration divide o processamento do query em lotes de registros. Isso reduz a carga do sistema.

   `Default`:  `1000`

   **Caminho do Armazenamento CRX**

   O local CRX dentro do qual os dados do processo devem ser armazenados para o relatórios.

   `Default`:  `/content/reporting/pm`

   >[!NOTE]
   >
   >Esse é o mesmo local especificado na opção de configuração ProcessDataStorage **Pasta raiz**.
   >
   >
   >Se você atualizar a opção Pasta raiz na configuração ProcessDataStorage, precisará atualizar o local do Caminho do Armazenamento CRX no serviço ReportConfiguration.

1. Clique em **Salvar** e feche **CQ Configuration Manager**.

### Serviço ProcessDataPublisher {#processdatapublisher-service}

O serviço ProcessDataPublisher importa dados do processo do banco de dados da AEM Forms e publica os dados para o serviço ProcessDataStorageProvider do armazenamento.

#### Para configurar o serviço ProcessDataPublisher   {#to-configure-processdatapublisher-service-nbsp}

1. Faça logon em **Console de administração** com credenciais de administrador.

   O URL padrão é `https://'server':port]/adminui/`.

1. Navegue até **Início** > **Serviços** > **Aplicações e Serviços** >**Gestão de Serviços** e abra o serviço **ProcessDataPublisher**.

![processdatapubelebpublisherservice-1](assets/processdatapublisherservice-1.png)

**Publicar dados**

Ative essa opção para start de dados do processo de publicação. Por padrão, a opção está desativada.

Habilite Processar Relatórios somente quando todas as configurações relacionadas aos componentes Processar Relatórios estiverem configuradas adequadamente.

Como alternativa, use essa opção para desativar o processo de publicação de dados quando não for mais necessário.

`Default`:  `Off`

**Intervalo de Lote (seg)**

Cada vez que o serviço ProcessDataPublisher é executado, o serviço divide primeiro o tempo desde a última execução do serviço pelo Intervalo em Lote. Em seguida, o serviço processa cada intervalo de dados da AEM Forms separadamente.

Isso ajuda a controlar o tamanho dos dados que os processos do editor terminam durante cada execução (lote) em um ciclo.

Por exemplo, se o editor é executado todos os dias, em vez de processar os dados inteiros por um dia em uma única execução, por padrão, divide o processamento em 24 lotes de uma hora cada.

`Default`:  `3600`

`Unit`:  `Seconds`

**Tempo limite de bloqueio (s)**

O serviço do editor adquire um bloqueio quando start os dados de processamento para que várias instâncias do editor não start a execução e o processamento de dados simultaneamente.

Se um serviço do editor que adquiriu um bloqueio estiver inativo pelo número de segundos definido pelo valor de Tempo limite de bloqueio, seu bloqueio será liberado para que outras instâncias do serviço do editor possam continuar o processamento.

`Default`:  `3600`

`Unit`:  `Seconds`

**Publicar dados de**

O ambiente AEM Forms contém dados do momento em que o ambiente foi configurado.

Por padrão, o serviço ProcessDataPublisher importa todos os dados do banco de dados da AEM Forms.

Dependendo das necessidades do seu relatórios, se você planeja executar relatórios e query em dados após uma determinada data e hora, é recomendável especificar a data e a hora. O serviço de publicação publicará a data a partir desse momento.

`Default`:  `01-01-1970 00:00:00`

`Format`:  `dd-MM-yyyy HH:mm:ss`

## Acessar a interface de usuário do Relatórios de processo {#accessing-the-process-reporting-user-interface}

A interface do usuário para o Process Relatórios é baseada em navegador.

Depois de configurar o Process Relatórios, você pode start trabalhando com o Process Relatórios no seguinte local na instalação do AEM Forms:

`https://<server>:<port>/lc/pr`

### Faça logon no Relatórios de processamento {#log-in-to-process-reporting}

Quando você navega até o URL do Relatórios do processo (https://&lt;server>:&lt;port>/lc/pr), a tela de logon é exibida.

Especifique suas credenciais para fazer logon no módulo Processar Relatórios.

>[!NOTE]
>
>Para fazer logon na interface do usuário do Process Relatórios, você precisa da seguinte permissão do AEM Forms:
>
>`PERM_PROCESS_REPORTING_USER`

![Logon no Relatórios Process](assets/capture1_new.png)

Quando você faz logon no Processar Relatórios, a tela **[!UICONTROL Início]** é exibida.

### Tela inicial do Relatórios de processamento {#process-reporting-home-screen}

![tela inicial do relatórios do processo](assets/process-reporting-home-screen.png)

**Processar visualização de árvore de Relatórios:** A visualização de árvore no lado esquerdo da tela inicial contém os itens dos módulos de Relatórios Processar.

A visualização em árvore consiste nos seguintes itens de nível superior:

**Relatórios:** Este item contém os relatórios predefinidos que acompanham o Relatórios do processo.

Para obter detalhes sobre os relatórios predefinidos, consulte [Relatórios predefinidos no Relatórios de processamento](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md).

**Query Ad-hoc:** Este item contém opções para executar pesquisa baseada em filtro para processos e tarefas.

Para obter detalhes sobre query ad-hoc, consulte [Query Ad-hoc no Relatórios Process](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md).

**Personalizado:** o nó Personalizado exibe relatórios personalizados que você cria.

Para obter o procedimento de criação e exibição de relatórios personalizados, consulte [Relatórios Relatórios personalizados no processo](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

**Barra de título do Relatórios do processo:** A barra de título do Relatórios do processo contém algumas opções genéricas que podem ser usadas ao trabalhar na interface do usuário.

**Título do Relatórios do processo:** O título do Relatórios do processo é exibido no canto esquerdo da barra de título.

Clique no título a qualquer momento para voltar à tela inicial.

**Hora da última atualização:** os dados do processo são publicados do banco de dados da AEM Forms para o repositório do Relatórios do processo de forma programada.

A Hora da Última Atualização exibe a última data e hora até as quais as atualizações de dados foram enviadas para o repositório do Process Relatórios.

Para obter detalhes sobre o serviço de publicação de dados e como agendar esse serviço, consulte [Agendar publicação de dados do processo](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) no artigo Introdução ao Relatórios de processo.

**Usuário do Relatórios do processo:** o nome de usuário conectado é exibido à direita da hora da última atualização.

**Lista suspensa da barra de título do Relatórios do processo:** A lista suspensa no canto direito da barra de título do Relatórios do processo contém as seguintes opções:

* **[!UICONTROL Sincronizar]**: Sincronize o repositório incorporado do Process Relatórios com o banco de dados AEM Forms.
* **[!UICONTROL Ajuda]**: Visualização na documentação de Ajuda do Process Relatórios.
* **[!UICONTROL Logout]**: Fazer logout do Relatórios Process
