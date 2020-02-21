---
title: Introdução ao Process Reporting
seo-title: Introdução ao Process Reporting
description: As etapas que você precisa seguir para começar a usar o AEM Forms no JEE Process Reporting
seo-description: As etapas que você precisa seguir para começar a usar o AEM Forms no JEE Process Reporting
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
translation-type: tm+mt
source-git-commit: 8ae69f5bb67d51d759f143a076fef4f5f0375809

---


# Introdução ao Process Reporting{#getting-started-with-process-reporting}

O Process Reporting dá aos usuários do AEM Forms a capacidade de consultar informações sobre processos do AEM Forms que estão definidos na implementação do AEM Forms. Entretanto, o Process Reporting não acessa dados diretamente do repositório do AEM Forms. Os dados são publicados pela primeira vez no repositório do Process Reporting de forma programada (*pelos* serviços ProcessDataPublisher e ProcessDataStorage). Os relatórios e consultas no Process Reporting são gerados a partir dos dados do Process Reporting publicados no repositório. O Process Reporting é instalado como parte do módulo do Forms Workflow.

Este artigo detalha as etapas para ativar a publicação de dados do AEM Forms no repositório do Process Reporting. Depois disso, você poderá usar o Process Reporting para executar relatórios e consultas. O artigo também aborda as opções disponíveis para configurar os serviços do Process Reporting.

## Pré-requisitos do Process Reporting {#process-reporting-pre-requisites}

### Limpar processos não essenciais {#purge-non-essential-processes}

Se você estiver usando o Fluxo de trabalho do Forms, o banco de dados do AEM Forms pode conter uma grande quantidade de dados

Os serviços de publicação do Process Reporting publicarão todos os dados do AEM Forms disponíveis no momento no banco de dados. Isso implica que, se o banco de dados contiver dados herdados nos quais você não deseja executar relatórios e consultas, todos esses dados também serão publicados no repositório, mesmo que não sejam necessários para relatórios. É recomendável expurgar esses dados antes de executar os serviços para publicar os dados no repositório do Process Reporting. Isso melhorará o desempenho do serviço do editor e do serviço que consulta os dados para relatório.

Para obter detalhes sobre como expurgar dados de processo do AEM Forms, consulte [Expurgando dados](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html)do processo.

>[!NOTE]
>
>Para obter as dicas e truques do Utilitário de Expurgação, consulte o artigo do Adobe Developer Connection sobre [Expurgação de processos e trabalhos](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf).

## Configuração dos serviços de Relatórios de Processo {#configuring-process-reporting-services}

### Agendar publicação de dados do processo {#schedule-process-data-publishing}

Os serviços do Process Reporting publicam dados do banco de dados do AEM Forms para o repositório do Process Reporting de forma programada.

Essa operação pode consumir muitos recursos e afetar o desempenho dos servidores do AEM Forms. É recomendável agendar isso fora dos horários ocupados do servidor do AEM Forms.

Por padrão, a publicação de dados está programada para ser executada todos os dias às 2h00.

Execute as seguintes etapas para alterar o cronograma de publicação:

>[!NOTE]
>
>Se você estiver executando sua implementação do AEM Forms em um cluster, execute as seguintes etapas em cada nó do cluster.

1. Pare a instância do servidor do AEM Forms.
1. &#x200B;

   * (Para Windows) Abra o `[JBoss root]/bin/run.conf.bat` arquivo em um editor.
   * (Para Linux, AIX e Solaris) `[JBoss root]/bin/run.conf.sh` em um editor.

1. Adicione o argumento JVM `-Dreporting.publisher.cron = <expression>.`

   Exemplo: A seguinte expressão cron faz com que o Process Reporting publique dados do AEM Forms no repositório do Process Reporting a cada 5 horas:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Salve e feche o `run.conf.bat` arquivo.

1. Reinicie a instância do servidor do AEM Forms.

1. Pare a instância do servidor do AEM Forms.
1. Faça logon no Console administrativo do WebSphere. Na árvore de navegação, clique em **Servidores** > Servidores **de** aplicativos e, no painel direito, clique no nome do servidor.

1. Em Infraestrutura do servidor, clique em **Java e em Gerenciamento** do processo > Definição **do** processo.

1. Em Propriedades adicionais, clique em **Java Virtual Machine**.

   Na caixa Argumentos JVM genéricos, adicione o argumento `-Dreporting.publisher.cron = <expression>.`

   **Exemplo**: A seguinte expressão cron faz com que o Process Reporting publique dados do AEM Forms no repositório do Process Reporting a cada 5 horas:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Clique em **Aplicar**, clique em OK e em **Salvar diretamente na configuração** mestre.
1. Reinicie a instância do servidor do AEM Forms.
1. Pare a instância do servidor do AEM Forms.
1. Faça logon no Console de administração do WebLogic. O endereço padrão do Console de administração do WebLogic é `https://[hostname]:[port]/console`.
1. Em Centro de alterações, clique em **Bloquear e editar**.
1. Em Estrutura do domínio, clique em **Ambiente** > **Servidores** e, no painel direito, clique no nome do servidor gerenciado.
1. Na tela seguinte, clique na guia **Configuração** > Guia Início **** do servidor.
1. Na caixa Argumentos, adicione o argumento JVM `-Dreporting.publisher.cron = <expression>`.

   **Exemplo**: A seguinte expressão cron faz com que o Process Reporting publique dados do AEM Forms no repositório do Process Reporting a cada 5 horas:

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Clique em **Salvar** e em **Ativar alterações**.
1. Reinicie a instância do servidor do AEM Forms.

![processamento datapubiterservice](assets/processdatapublisherservice.png)

### Serviço ProcessDataStorage {#processdatastorage-service}

O serviço ProcessDataStorageProvider recebe dados do processo do serviço ProcessDataPublisher e salva os dados no repositório do Process Reporting.

Em cada ciclo de publicação, os dados são salvos em subpastas de uma pasta raiz predefinida.

Você pode usar o console Administração para configurar a raiz (**padrão**: `/content/reporting/pm`) local e subpasta (**padrão**: `/yyyy/mm/dd/hh/mi/ss`) formato de hierarquia em que os dados do processo seriam armazenados.

#### Para configurar os locais do repositório do Process Reporting {#to-configure-the-process-reporting-repository-locations}

1. Faça logon no Console **** de administração com credenciais de administrador. O URL padrão do Console de administração é `https://[server]:[port]/adminui`
1. Navegue até **Início** > **Serviços** > **Aplicativos e serviços** > Gerenciamento **** de serviços e abra o serviço **ProcessDataStorageProvider** .

   ![process-data-storage-service](assets/process-data-storage-service.png)

   **PastadaRaiz**

   O local CRX dentro do qual os dados do processo seriam armazenados para relatório.

   `Default`: `/content/reporting/pm`

   **Hierarquia da pasta**

   A hierarquia de pastas dentro da qual os dados do processo seriam armazenados com base no tempo de criação do processo.

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. Clique em **Salvar**.

### Serviço ReportConfiguration {#reportconfiguration-service}

O serviço ReportConfiguration é usado pelo Process Reporting para configurar o serviço de consulta de relatório de processo.

#### To configure the ReportingConfiguration service {#to-configure-the-reportingconfiguration-service}

1. Faça logon no **Configuration Manager** com credenciais de administrador do CRX. O URL padrão do Configuration Manager é `https://[server]:[port]/lc/system/console/configMgr`
1. Abra o serviço **ReportingConfiguration** .
1. **Número de registros**

   Ao executar uma consulta no repositório, um resultado pode conter potencialmente um grande número de registros. Se o conjunto de resultados for grande, a execução da consulta poderá consumir recursos do servidor.

   Para lidar com grandes conjuntos de resultados, o serviço ReportConfiguration divide o processamento da consulta em lotes de registros. Isso reduz a carga do sistema.

   `Default`: `1000`

   **Caminho de armazenamento CRX**

   O local CRX dentro do qual os dados do processo devem ser armazenados para relatório.

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >Esse é o mesmo local especificado na opção de configuração ProcessDataStorage, Pasta **raiz**.
   >
   >
   >Se você atualizar a opção Pasta raiz na configuração ProcessDataStorage, precisará atualizar o local do Caminho de armazenamento CRX no serviço ReportConfiguration.

1. Clique em **Salvar** e feche o **CQ Configuration Manager**.

### Serviço ProcessDataPublisher {#processdatapublisher-service}

O serviço ProcessDataPublisher importa dados do processo do banco de dados do AEM Forms e publica os dados no serviço ProcessDataStorageProvider para armazenamento.

#### Para configurar o serviço ProcessDataPublisher {#to-configure-processdatapublisher-service-nbsp}

1. Faça logon no Console **** de administração com credenciais de administrador.

   O URL padrão é `https://[server]:port]/adminui/`.

1. Navegue até **Início** > **Serviços** > **Aplicativos e serviços** > Gerenciamento **** de serviços e abra o serviço **ProcessDataPublisher** .

![processdatapubelebpublisherservice-1](assets/processdatapublisherservice-1.png)

**Publicar dados**

Ative essa opção para iniciar a publicação de dados do processo. Por padrão, a opção está desativada.

Habilitar Relatórios de Processos somente quando todas as configurações relacionadas aos componentes do Process Reporting estiverem configuradas adequadamente.

Como alternativa, use essa opção para desativar o processo de publicação de dados quando não for mais necessário.

`Default`: `Off`

**Intervalo de Lote (seg)**

Cada vez que o serviço ProcessDataPublisher é executado, o serviço divide primeiro o tempo desde a última execução do serviço pelo Intervalo em Lote. O serviço processa cada intervalo de dados do AEM Forms separadamente.

Isso ajuda a controlar o tamanho dos dados que os processos do editor terminam durante cada execução (lote) em um ciclo.

Por exemplo, se o editor é executado todos os dias, em vez de processar os dados inteiros por um dia em uma única execução, por padrão, divide o processamento em 24 lotes de uma hora cada.

`Default`: `3600`

`Unit`: `Seconds`

**Tempo limite de bloqueio (s)**

O serviço do editor adquire um bloqueio quando inicia o processamento de dados para que várias instâncias do editor não iniciem a execução e o processamento de dados simultaneamente.

Se um serviço do editor que adquiriu um bloqueio estiver inativo pelo número de segundos definido pelo valor de Tempo limite de bloqueio, seu bloqueio será liberado para que outras instâncias do serviço do editor possam continuar o processamento.

`Default`: `3600`

`Unit`: `Seconds`

**Publicar dados de**

O ambiente do AEM Forms contém dados do momento em que o ambiente foi configurado.

Por padrão, o serviço ProcessDataPublisher importa todos os dados do banco de dados do AEM Forms.

Dependendo das suas necessidades de relatórios, se você planeja executar relatórios e consultas em dados após uma determinada data e hora, é recomendável especificar a data e a hora. O serviço de publicação publicará a data a partir desse momento.

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## Acessar a interface do usuário do Process Reporting {#accessing-the-process-reporting-user-interface}

A interface do usuário do Process Reporting é baseada em navegador.

Depois de configurar o Process Reporting, você pode começar a trabalhar com o Process Reporting no seguinte local na instalação do AEM Forms:

`https://<server>:<port>/lc/pr`

### Fazer logon no Process Reporting {#log-in-to-process-reporting}

Quando você navega até o URL do Process Reporting (https://&lt;servidor>:&lt;porta>/lc/pr), a tela de logon é exibida.

Especifique suas credenciais para fazer logon no módulo Process Reporting.

>[!NOTE]
>
>Para fazer logon na interface do usuário do Process Reporting, é necessário ter a seguinte permissão de AEM Forms:
>
>`PERM_PROCESS_REPORTING_USER`

![Logon para Processar Relatório](assets/capture1_new.png)

Quando você faz logon no Process Reporting, a tela **[!UICONTROL Home]** é exibida.

### Tela inicial do Process Reporting {#process-reporting-home-screen}

![relatório de processo-tela inicial](assets/process-reporting-home-screen.png)

**** Visualização da árvore do Process Reporting: A exibição em árvore no lado esquerdo da tela Início contém os itens dos módulos de Relatório de processo.

A visualização em árvore consiste nos seguintes itens de nível superior:

**** Relatórios: Este item contém os relatórios predefinidos que acompanham o Relatório de processos.

Para obter detalhes sobre os relatórios predefinidos, consulte Relatórios [predefinidos em andamento](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md).

**** Consultas ad hoc: Este item contém opções para executar pesquisa baseada em filtro para processos e tarefas.

Para obter detalhes sobre consultas ad-hoc, consulte Consultas [ad-hoc em Relatórios](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md)de processo.

**** Personalizado: O nó Personalizado exibe relatórios personalizados que você cria.

Para obter o procedimento de criação e exibição de relatórios personalizados, consulte Relatórios [personalizados em andamento](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

**** Barra de título do Process Reporting: A barra de título Relatório de processo contém algumas opções genéricas que podem ser usadas ao trabalhar na interface do usuário.

**** Título do Relatório do Processo: O título Relatório de processo é exibido no canto esquerdo da barra de título.

Clique no título a qualquer momento para voltar à tela inicial.

**** Hora da última atualização: Os dados do processo são publicados do banco de dados do AEM Forms para o repositório do Process Reporting de forma programada.

A Hora da Última Atualização exibe a última data e hora até as quais as atualizações de dados foram enviadas para o repositório do Process Reporting.

Para obter detalhes sobre o serviço de publicação de dados e como agendar esse serviço, consulte [Agendar publicação](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) de dados do processo no artigo Introdução ao Relatório de processos.

**** Usuário do Process Reporting: O nome de usuário conectado é exibido à direita da hora da Última atualização.

**** Lista suspensa da barra de título Relatório de Processos: A lista suspensa no canto direito da barra de título Relatório de processo contém as seguintes opções:

* **[!UICONTROL Sincronizar]**: Sincronize o repositório incorporado do Process Reporting com o banco de dados do AEM Forms.
* **[!UICONTROL Ajuda]**: Consulte a documentação da Ajuda sobre o Process Reporting.
* **[!UICONTROL Logout]**: Fazer logout do relatório de processos

[Contate o suporte](https://www.adobe.com/account/sign-in.supportportal.html)
