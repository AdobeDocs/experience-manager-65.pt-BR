---
title: Otimização do desempenho
description: Saiba como configurar certos aspectos do AEM para otimizar o desempenho.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
feature: Configuring
exl-id: 5b0c9a8c-0f5f-46ee-a455-adb9b9d27270
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 2d6caa10e8f1cf3d0811280e31c2f40bceac20ee
workflow-type: tm+mt
source-wordcount: '6470'
ht-degree: 12%

---

# Otimização do desempenho {#performance-optimization}

>[!NOTE]
>
>Para obter diretrizes gerais sobre desempenho, leia a página [Diretrizes de Desempenho](/help/sites-deploying/performance-guidelines.md).
>
>Para obter mais informações sobre como solucionar e corrigir problemas de desempenho, consulte também a [Árvore de desempenho](/help/sites-deploying/performance-tree.md).
>
>Além disso, você pode consultar um artigo da Base de Dados de Conhecimento sobre [Dicas de Ajuste de Desempenho](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-17466).

Um problema importante é o tempo que o site leva para responder às solicitações do visitante. Embora esse valor varie para cada solicitação, um valor de target médio pode ser definido. Quando esse valor puder ser obtido e mantido, ele poderá ser usado para monitorar o desempenho do site e indicar o desenvolvimento de possíveis problemas.

Os tempos de resposta almejados são diferentes nos ambientes de criação e publicação, refletindo as diferentes características do público-alvo:

## Ambiente de criação {#author-environment}

Esse ambiente é usado pelos autores que inserem e atualizam conteúdo. Ele deve atender a alguns usuários, cada um deles gerando um alto número de solicitações de desempenho intensivo ao atualizar páginas de conteúdo e os elementos individuais nessas páginas.

## Ambiente de publicação {#publish-environment}

Esse ambiente contém conteúdo que você disponibiliza para os usuários. Aqui, o número de solicitações é ainda maior e a velocidade é tão vital. Mas como a natureza das solicitações é menos dinâmica, mecanismos adicionais de aprimoramento de desempenho podem ser aplicados, como armazenamento em cache de conteúdo ou balanceamento de carga.

>[!NOTE]
>
>* Depois de configurar para otimização de desempenho, siga os procedimentos em [Dia difícil](/help/sites-developing/tough-day.md) para testar o ambiente sob carga pesada.
>* Consulte também [Dicas de ajuste de desempenho.](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-17466)

## Metodologia de otimização de desempenho {#performance-optimization-methodology}

Uma metodologia de otimização de desempenho para projetos AEM pode ser resumida em cinco regras simples que podem ser seguidas para evitar problemas de desempenho desde o início:

1. [Planejamento para otimização](#planning-for-optimization)
1. [Simular Realidade](#simulate-reality)
1. [Estabelecer metas sólidas](#establish-solid-goals)
1. [Permanecer relevante](#stay-relevant)
1. [Ciclos de iteração Agile](#agile-iteration-cycles)

Essas regras se aplicam aos projetos da Web em geral e são relevantes para os gerentes de projetos e administradores de sistema, a fim de garantir que seus projetos não enfrentem desafios de desempenho na hora do lançamento.

### Planejamento para otimização {#planning-for-optimization}

![chlimage_1-3](assets/chlimage_1-3.jpeg)

Planeje cerca de 10% do esforço do projeto para a fase de otimização de desempenho. Os requisitos reais de otimização de desempenho dependem do nível de complexidade de um projeto e da experiência da equipe de desenvolvimento. Embora seu projeto possa (em última análise) não exigir o tempo alocado, é uma boa prática planejar sempre a otimização de desempenho na região sugerida.

Sempre que possível, um projeto deve primeiro ser lançado de forma flexível para um público limitado para coletar experiência na vida real e executar outras otimizações, sem a pressão adicional que se segue a um anúncio completo.

Depois que você estiver &quot;ao vivo&quot;, a otimização do desempenho não termina. Agora é quando você enfrenta a carga &quot;real&quot; em seu sistema. É importante planejar ajustes adicionais após o lançamento.

Como a carga do seu sistema muda e os perfis de desempenho do seu sistema mudam com o tempo, um &quot;ajuste&quot; ou &quot;verificação de integridade&quot; de desempenho deve ser programado em intervalos de 6 a 12 meses.

### Simular Realidade {#simulate-reality}

![chlimage_1-4](assets/chlimage_1-4.jpeg)

Se você acessar um site e descobrir, após o lançamento, que teve problemas de desempenho, é provável que seus testes de carga e desempenho não tenham simulado a realidade de maneira suficientemente precisa.

Simular a realidade é difícil e quanto esforço você quer investir para ficar &quot;real&quot; depende da natureza do seu projeto. &quot;Real&quot; significa não apenas &quot;código real&quot; e &quot;tráfego real&quot;, mas também &quot;conteúdo real&quot;, especialmente em relação ao tamanho e à estrutura do conteúdo. Seus modelos podem se comportar de forma diferente dependendo do tamanho e da estrutura do repositório.

### Estabelecer metas sólidas {#establish-solid-goals}

![chlimage_1-5](assets/chlimage_1-5.jpeg)

Não se deve subestimar a importância de estabelecer corretamente os objetivos de desempenho. Muitas vezes, depois que as pessoas se concentram em metas de desempenho específicas, é difícil alterar essas metas posteriormente, mesmo que elas se baseiem em suposições.

Estabelecer metas de desempenho boas e sólidas é realmente uma das áreas mais complicadas. Geralmente, é melhor coletar logs da vida real e benchmarks de um site comparável (por exemplo, o antecessor do novo site).

### Permanecer relevante {#stay-relevant}

![chlimage_1-6](assets/chlimage_1-6.jpeg)

É importante otimizar um gargalo de cada vez. Se você tentar fazer as coisas em paralelo sem validar o impacto de uma otimização, poderá perder o controle de qual medida de otimização ajudou.

### Ciclos de iteração Agile {#agile-iteration-cycles}

![chlimage_1-7](assets/chlimage_1-7.jpeg)

O ajuste de desempenho é um processo iterativo que envolve análise, otimização e validação até que a meta seja atingida. Para levar em conta esse aspecto, implemente um processo de validação ágil na fase de otimização em vez de um processo de teste mais pesado após cada iteração.

Esse foco significa que o desenvolvedor que implementa a otimização deve ter uma maneira rápida de saber se a otimização já atingiu a meta. Essas informações são importantes porque, quando a meta é atingida, a otimização é finalizada.

## Diretrizes básicas de desempenho {#basic-performance-guidelines}

De modo geral, mantenha suas solicitações de html não armazenadas em cache em menos de 100 milissegundos. Mais especificamente, podem servir de orientação os seguintes elementos:

* 70% das solicitações de páginas devem ser respondidas em menos de 100 milissegundos.
* 25% das solicitações de páginas devem receber uma resposta dentro de 100 milissegundos a 300 milissegundos.
* 4% das solicitações de páginas devem receber uma resposta dentro de 300 milissegundos a 500 milissegundos.
* 1% das solicitações para páginas deve receber uma resposta dentro de 500 milissegundos a 1000 milissegundos.
* Nenhuma página deve responder mais lentamente do que um segundo.

Os números acima assumem as seguintes condições:

* Medido na publicação (sem despesas gerais relacionadas a um ambiente de criação)
* Medido no servidor (sem sobrecarga de rede)
* Não armazenado em cache (sem cache de saída AEM, sem cache do Dispatcher)
* Somente para itens complexos com muitas dependências (HTML, JS, PDF, ...)
* Nenhuma outra carga no sistema

Há alguns problemas que contribuem frequentemente para problemas de desempenho, incluindo os seguintes:

* Ineficiência de armazenamento em cache do Dispatcher
* O uso de queries em modelos de exibição normais.

O ajuste do nível de JVM e SO geralmente não resulta em saltos significativos no desempenho e, portanto, deve ser executado no final do ciclo de otimização.

A forma como um repositório de conteúdo é estruturado também pode afetar o desempenho. Para obter o melhor desempenho, o número de nós secundários anexados a nós individuais em um repositório de conteúdo não deve exceder 1.000 (como regra).

Seus melhores amigos durante um exercício normal de otimização de desempenho são:

* O `request.log`
* Tempo baseado em componentes
* Um profiler Java™.

### Desempenho ao carregar e editar o Digital Assets {#performance-when-loading-and-editing-digital-assets}

Devido ao grande volume de dados envolvidos ao carregar e editar ativos digitais, o desempenho pode se tornar um problema.

Dois itens afetam o desempenho aqui:

* CPU - vários núcleos permitem um trabalho mais suave durante a transcodificação
* Disco rígido - discos RAID paralelos alcançam o mesmo

Para melhorar o desempenho, considere o seguinte:

* Quantos ativos serão carregados por dia? Uma boa estimativa pode ser baseada em:

![chlimage_1-77](assets/chlimage_1-77.png)

* O período em que as edições são feitas (normalmente a duração do dia de trabalho, mais para operações internacionais).
* O tamanho médio das imagens carregadas (e o tamanho das representações geradas por imagem) em megabytes.
* Determine a taxa média de dados:

![chlimage_1-78](assets/chlimage_1-78.png)

* 80% de todas as edições são feitas em 20% das vezes, portanto, no horário de pico, você tem quatro vezes a taxa média de dados. Esse desempenho é o seu objetivo.

## Monitoramento de desempenho {#performance-monitoring}

O desempenho (ou a falta dele) é uma das primeiras coisas que os usuários notam, de modo que com qualquer aplicativo com interface do usuário, o desempenho é de importância fundamental. Para otimizar o desempenho da instalação do AEM, monitore vários atributos da instância e seu comportamento.

Para obter informações sobre como executar o monitoramento do desempenho, consulte [Monitoramento do Desempenho](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance).

Os problemas que causam problemas de desempenho geralmente são difíceis de rastrear, mesmo quando seus efeitos são fáceis de ver.

Um ponto de partida básico é um bom conhecimento do seu sistema quando ele está funcionando normalmente. A menos que você saiba a aparência e o comportamento do seu ambiente quando ele funciona corretamente, é difícil localizar o problema quando o desempenho piora. Gaste tempo investigando o sistema quando ele estiver funcionando sem problemas e garanta que a coleta de informações de desempenho seja uma tarefa contínua. Isso fornece uma base de comparação caso o desempenho sofra.

O diagrama a seguir ilustra o caminho que uma solicitação de conteúdo AEM pode tomar e, portanto, o número de diferentes elementos que podem afetar o desempenho.

![chlimage_1-79](assets/chlimage_1-79.png)

O desempenho também é um equilíbrio entre volume e capacidade:

* **Volume** - A quantidade de saída processada e entregue pelo sistema.
* **Capacidade** - A capacidade do sistema de entregar o volume.

O desempenho pode ser ilustrado em vários locais na cadeia da Web.

![chlimage_1-80](assets/chlimage_1-80.png)

Há várias áreas funcionais que geralmente são responsáveis por afetar o desempenho:

* Armazenamento em cache
* Código do aplicativo (seu projeto)
* Funcionalidade de pesquisa

### Regras Básicas De Desempenho {#basic-rules-regarding-performance}

Algumas regras devem ser levadas em conta ao otimizar o desempenho:

* O ajuste de desempenho *deve* fazer parte de todos os projetos.
* Não otimize no início do ciclo de desenvolvimento.
* O desempenho só é tão bom quanto o link mais fraco.
* Sempre pense em capacidade ou volume.
* Otimize coisas importantes primeiro.
* Nunca otimizar sem *metas realistas*.

>[!NOTE]
>
>Lembre-se de que o mecanismo usado para medir o desempenho geralmente afeta exatamente o que você está tentando medir. Tente levar em conta essas discrepâncias e elimine o máximo possível de seu efeito; especialmente, os plug-ins de navegadores devem ser desativados sempre que possível.

## Configuração do para desempenho {#configuring-for-performance}

Certos aspectos do AEM (e/ou do repositório subjacente) podem ser configurados para otimizar o desempenho. Veja a seguir possibilidades e sugestões. Certifique-se de usar a funcionalidade em questão ou de como usá-la antes de fazer alterações.

>[!NOTE]
>
>Consulte [Otimização de desempenho](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=pt-BR).

### Indexação de pesquisa {#search-indexing}

A partir do AEM 6.0, o Adobe Experience Manager usa uma arquitetura de repositório baseada em Oak.

Você pode encontrar as informações de indexação atualizadas aqui:

* [Práticas recomendadas para consultas e indexação](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [Consultas e indexação](/help/sites-deploying/queries-and-indexing.md)

### Processamento de fluxo de trabalho simultâneo {#concurrent-workflow-processing}

Para melhorar o desempenho, limite o número de processos de workflow em execução simultânea. Por padrão, o motor de workflow processa tantos workflows em paralelo quanto há processadores disponíveis para a Java™ VM. Quando as etapas do fluxo de trabalho exigem grandes quantidades de recursos de processamento (RAM ou CPU), a execução de vários desses fluxos de trabalho em paralelo pode colocar altas demandas nos recursos disponíveis do servidor.

Por exemplo, quando imagens (ou ativos DAM em geral) são carregadas, os fluxos de trabalho importam automaticamente as imagens para o DAM. As imagens geralmente têm alta resolução e podem consumir facilmente centenas de MB de heap para processamento. O manuseio dessas imagens em paralelo coloca uma alta carga no subsistema de memória e no coletor de lixo.

O mecanismo de fluxo de trabalho usa as filas de trabalho do Apache Sling para manipular e agendar o processamento do item de trabalho. Os seguintes serviços de fila de trabalhos foram criados por padrão na fábrica do serviço de configuração da fila de trabalhos do Apache Sling para processar trabalhos de fluxo de trabalho:

* Fila de fluxo de trabalho do Granite: a maioria das etapas do fluxo de trabalho, como aquelas que processam ativos DAM, usam o serviço Fila de fluxo de trabalho do Granite.
* Fila de trabalho do processo externo do fluxo de trabalho do Granite: esse serviço é usado para etapas especiais do fluxo de trabalho externo que normalmente são usadas para entrar em contato com um sistema externo e pesquisar resultados. Por exemplo, a etapa Processo de extração de mídia de InDesign é implementada como um processo externo. O mecanismo de workflow usa a fila externa para processar a pesquisa. (Consulte [com.day.cq.workflow.exec.WorkflowExternalProcess](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/exec/WorkflowExternalProcess.html).)

Configure esses serviços para limitar o número máximo de processos de fluxo de trabalho simultâneos.

>[!NOTE]
>
>A configuração dessas filas de trabalhos afeta todos os fluxos de trabalho, a menos que você tenha criado uma fila de trabalhos para um modelo de fluxo de trabalho específico (consulte [Configurar a fila para um modelo de fluxo de trabalho específico](/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow) abaixo).

#### Configuração no repositório {#configuration-in-the-repo}

Se você estiver configurando os serviços [usando um nó sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository), localize o PID dos serviços existentes, por exemplo: org.apache.sling.event.jobs.QueueConfiguration.370aad73-d01b-4a0b-abe4-20198d85f705. Você pode descobrir o PID usando o Console da Web.

Configure a propriedade chamada `queue.maxparallel`.

#### Configuração no console da Web {#configuration-in-the-web-console}

Para configurar esses serviços [usando o Console da Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), localize os itens de configuração existentes abaixo da fábrica do serviço de Configuração da Fila de Trabalhos do Apache Sling.

Configure a propriedade chamada Máximo de Trabalhos Paralelos.

### Configurar a Fila para um Fluxo de Trabalho Específico {#configure-the-queue-for-a-specific-workflow}

Crie uma fila de trabalhos para um modelo de fluxo de trabalho específico para poder configurar o manuseio de trabalhos para esse modelo de fluxo de trabalho. Dessa forma, suas configurações afetam o processamento de um workflow específico, enquanto a configuração da Fila de workflow padrão do Granite controla o processamento de outros workflows.

Quando os modelos de fluxo de trabalho são executados, eles criam trabalhos do Sling para um tópico específico. Por padrão, o tópico corresponde aos tópicos configurados para a Fila geral de fluxos de trabalho do Granite ou a Fila de trabalho do processo externo do Granite:

* `com/adobe/granite/workflow/job*`
* `com/adobe/granite/workflow/external/job*`

Os tópicos de trabalho reais que os modelos de fluxo de trabalho geram incluem o sufixo específico do modelo. Por exemplo, o modelo de fluxo de trabalho **Ativo de atualização do DAM** gera trabalhos com o seguinte tópico:

`com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model`

Portanto, você pode criar uma fila de trabalhos para o tópico que corresponda aos tópicos de trabalho do seu modelo de fluxo de trabalho. A configuração das propriedades relacionadas ao desempenho da fila afeta somente o modelo de fluxo de trabalho que gera as tarefas que correspondem ao tópico da fila.

O procedimento a seguir cria uma fila de trabalhos para um fluxo de trabalho, usando o fluxo de trabalho **Ativo de atualização do DAM** como exemplo.

1. Execute o modelo de fluxo de trabalho para o qual deseja criar a fila de trabalhos, para que as estatísticas de tópico sejam geradas. Por exemplo, adicione uma imagem ao Assets para executar o fluxo de trabalho **Ativo de atualização do DAM**.
1. Abra o console Sling Jobs (`https://<host>:<port>/system/console/slingevent`).
1. Descubra os tópicos relacionados ao fluxo de trabalho no console. Para Ativo de atualização do DAM, os seguintes tópicos são encontrados:

   * `com/adobe/granite/workflow/external/job/etc/workflow/models/dam/update_asset/jcr_content/model`
   * `com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model`
   * `com/adobe/granite/workflow/job/etc/workflow/models/dam-xmp-writeback/jcr_content/model`

1. Crie uma fila de tarefas para cada um desses tópicos. Para criar uma fila de trabalhos, crie uma configuração de fábrica para o serviço de fábrica da Fila de trabalhos do Apache Sling.

   As configurações de fábrica são semelhantes à Fila de Fluxo de Trabalho do Granite descrita em [Processamento de Fluxo de Trabalho Simultâneo](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing), exceto que a propriedade Topics corresponde ao tópico dos seus trabalhos de fluxo de trabalho.

### Serviço de sincronização de ativos DAM do AEM {#cq-dam-asset-synchronization-service}

O `AssetSynchronizationService` é usado para sincronizar ativos de repositórios montados (incluindo LiveLink, Documentum®, entre outros). Por padrão, essa sincronização faz uma verificação regular a cada 300 segundos (5 minutos); portanto, se você não usar repositórios montados, poderá desativar esse serviço.

A desabilitação do serviço é feita por [configuração do serviço OSGi](/help/sites-deploying/configuring-osgi.md) **Serviço de Sincronização de Ativos DAM CQ** para definir o **Período de sincronização** ( `scheduler.period`) para (no mínimo) um ano (definido em segundos).

### Várias instâncias do DAM {#multiple-dam-instances}

A implantação de várias instâncias do DAM pode ajudar no desempenho quando, por exemplo:

* Você tem uma alta carga devido ao carregamento regular de muitos ativos para o ambiente de criação; aqui, uma instância do DAM separada pode ser dedicada ao autor de serviço.
* Você tem várias equipes em locais mundiais (por exemplo, EUA, Europa, Ásia).

Outras considerações são:

* Separação de &quot;trabalho em andamento&quot; no autor de &quot;final&quot; na publicação
* Separação de usuários internos na criação dos visitantes/usuários externos na publicação (por exemplo, agentes, representantes da imprensa, clientes e estudantes).

## Práticas recomendadas para controle de qualidade {#best-practices-for-quality-assurance}

O desempenho é de suma importância para o ambiente de publicação. Portanto, você deve planejar e analisar cuidadosamente os testes de desempenho feitos para o ambiente de publicação ao implementar seu projeto.

Esta seção tem como objetivo fornecer uma visão geral padronizada dos problemas envolvidos na definição de um conceito de teste especificamente para testes de desempenho no seu ambiente *publicar*. Essas informações são de interesse principalmente para engenheiros de controle de qualidade, gerentes de projeto e administradores de sistema.

O documento a seguir aborda uma abordagem padronizada para testes de desempenho de um aplicativo AEM no ambiente *Publish*. Este teste de desempenho envolve as cinco fases a seguir:

* [Verificação do conhecimento](#verification-of-knowledge)
* [Definição de escopo](#scope-definition)
* [Metodologias de teste](#test-methodologies)
* [Definição de metas de desempenho](#defining-the-performance-goals)
* [Otimização](#optimization)

O controle é um processo extra abrangente - necessário, mas não limitado a testes.

### Verificação do conhecimento {#verification-of-knowledge}

Uma primeira etapa é documentar as informações básicas que você deve saber antes de iniciar o teste:

* A arquitetura de seu ambiente de teste
* Um mapa de aplicativos detalhando os elementos internos que precisam de teste (isoladamente e em combinação)

#### Arquitetura de teste {#test-architecture}

Documente a arquitetura do ambiente de teste que está sendo usado para seu teste de desempenho.

Você precisa de uma reprodução do ambiente de produção planejado do Publish, juntamente com o Dispatcher e o Balanceador de carga.

#### Mapa de aplicativos {#application-map}

Obtenha uma visão geral clara a partir da qual é possível criar um mapa do aplicativo inteiro (talvez você já tenha esse mapa a partir de testes no ambiente do Autor).

Uma representação de diagrama dos elementos internos do aplicativo pode fornecer uma visão geral dos requisitos de teste; com a codificação por cores, também pode servir como base para os relatórios.

### Definição do escopo {#scope-definition}

Um aplicativo geralmente tem uma seleção de casos de uso. Alguns casos de uso são importantes, outros menos.

Para focalizar o escopo do teste de desempenho em publicação, a Adobe recomenda que você defina o seguinte:

* Casos de uso de negócios mais importantes
* Casos de uso técnico mais críticos

O número de casos de uso depende de você, mas deve ser limitado a um número facilmente gerenciável (por exemplo, entre 5 e 10).

Depois que os casos de uso principais forem selecionados, os KPIs (indicadores-chave de desempenho) e as ferramentas usadas para medi-los poderão ser definidos para cada caso. Exemplos de KPIs comuns incluem:

* Tempo de resposta de ponta a ponta
* Tempo de resposta do servlet
* Tempo de resposta para um único componente
* Tempo de resposta dos serviços
* Número de threads ociosos no pool de threads
* Número de conexões livres
* Recursos do sistema, como CPU e acesso de E/S

### Metodologias de teste {#test-methodologies}

Este conceito tem quatro cenários usados para definir e testar as metas de desempenho:

* Testes de componente único
* Testes de componente combinado
* Cenário de *ativação*
* Cenários de erro

Com base nos seguintes princípios:

#### Pontos de interrupção do componente {#component-breakpoints}

* Cada componente tem um ponto de interrupção específico quando relacionado ao desempenho. Ou seja, um componente pode mostrar um bom desempenho até que um ponto específico seja atingido, após o qual o desempenho é degradado rapidamente.
* Para obter uma visão geral completa do aplicativo, primeiro verifique seus componentes para determinar quando o ponto de interrupção de cada um é atingido.
* Para descobrir o ponto de interrupção em que é possível executar um teste de carga, no qual, ao longo de um período, é possível aumentar o número de usuários para criar uma carga crescente. Ao monitorar essa carga e a resposta dos componentes, você encontra um comportamento de desempenho específico quando o ponto de interrupção do componente é atingido. O ponto pode ser qualificado pelo número de transações simultâneas por segundo, juntamente com o número de usuários simultâneos (se o componente for sensível a esse KPI).
* Essas informações podem servir como referência para melhorias, indicar a eficiência das medidas usadas e ajudar a definir cenários de teste.

#### Transações {#transactions}

* O termo transação é usado para representar a solicitação de uma página da Web completa, incluindo a própria página e todas as chamadas subsequentes. Ou seja, a solicitação de página, qualquer chamada AJAX, imagem e outros objetos **Solicitar detalhamento**.
* Para analisar totalmente cada solicitação, você pode representar cada elemento da pilha de chamadas e totalizar o tempo médio de processamento para cada um.

### Definir as metas de desempenho {#defining-the-performance-goals}

Após o escopo e os KPIs relacionados serem definidos, as metas de desempenho específicas são definidas. Esse processo envolve a concepção de cenários de teste, juntamente com valores de destino.

Testar o desempenho em condições médias e de pico. Além disso, você precisa de testes de cenário de ativação para garantir que possa atender ao aumento do interesse no site quando ele for disponibilizado pela primeira vez.

Qualquer experiência ou estatística que você tenha coletado de um site existente também pode ser útil para determinar metas futuras. Por exemplo, tráfego superior no seu site ativo.

#### Testes de componente único {#single-component-tests}

Os componentes críticos devem ser ensaiados tanto em condições de média como de pico.

Em ambos os casos, você pode definir o número esperado de transações por segundo quando um número predefinido de usuários estiver usando o sistema.

| Componente | Tipo de teste | Não. de usuários | Tx/s (esperado) | Tx/s (testado) | Descrição |
|---|---|---|---|---|---|
| Usuário único da página inicial | Média | 1 | 1 |  |  |
|   | Pico | 1 | 3 |  |  |
| Página inicial de 100 usuários | Média | 100 | 3 |  |  |
|   | Pico | 100 | 3 |  |

#### Testes de componente combinado {#combined-component-tests}

Testar os componentes em combinação faz com que o comportamento dos aplicativos se reflita melhor. Mais uma vez, as condições médias e de pico devem ser testadas.

| Cenário | Componente | Não. de usuários | Tx/s (esperado) | Tx/s (testado) | Descrição |
|---|---|---|---|---|---|
| Média mista | Página inicial | 10 | 1 |  |  |
|   | Pesquisar | 10 | 1 |  |  |
|   | Notícias | 10 | 2 |  |  |
|   | Eventos | 10 | 1 |  |  |
|   | Ativações | 10 | 3 |  | Simulação do comportamento do autor. |
| Pico misto | Página inicial | 100 | 5 |  |  |
|   | Pesquisar | 50 | 5 |  |  |
|   | Notícias | 100 | 10 |  |  |
|   | Eventos | 100 | 10 |  |  |
|   | Ativações | 20 | 20 |  | Simulação do comportamento do autor. |

#### Testes de ativação {#going-live-tests}

Durante os primeiros dias após o site ser disponibilizado, você pode esperar um aumento no nível de interesse. Esse cenário é ainda maior do que os valores de pico que você está testando. A Adobe recomenda testar os cenários de ativação para garantir que o sistema possa atender a essa situação.

| Cenário | Tipo de teste | Não. de usuários | Tx/s (esperado) | Tx/s (testado) | Descrição |
|---|---|---|---|---|---|
| Pico de ativação | Página inicial | 200 | 20 |  |  |
|   | Pesquisar | 100 | 10 |  |  |
|   | Notícias | 200 | 20 |  |  |
|   | Eventos | 200 | 20 |  |  |
|   | Ativações | 20 | 20 |  | Simulação do comportamento do autor. |

#### Testes de Cenário de Erro {#error-scenario-tests}

Teste cenários de erro para garantir que o sistema reaja corretamente e adequadamente. Não apenas em como o erro em si é tratado, mas o impacto que ele pode ter no desempenho. Por exemplo:

* O que acontece quando o usuário tenta inserir um termo de pesquisa inválido na caixa de pesquisa
* O que acontece quando o termo de pesquisa é tão geral que retorna um número excessivo de resultados

Ao conceber estes testes, deve-se lembrar que nem todos os cenários ocorrem regularmente. No entanto, seu impacto em todo o sistema é importante.

| Cenário de erro | Tipo de erro | Não. de usuários | Tx/s (esperado) | Tx/s (testado) | Descrição |
|---|---|---|---|---|---|
| Sobrecarga do componente de pesquisa | Pesquisar no curinga global (asterisco) | 10 | 1 |  | Somente &ast;&ast;&ast; são pesquisados. |
|   | Palavra de interrupção | 20 | 2 |  | Procurando uma palavra de interrupção. |
|   | String vazia | 10 | 1 |  | Procurando uma cadeia de caracteres vazia. |
|   | Caracteres especiais | 10 | 1 |  | Procurando caracteres especiais. |

#### Testes de resistência {#endurance-tests}

Certos problemas só são encontrados depois que o sistema é executado por um período de tempo contínuo, seja em horas ou dias. Um teste de resistência é usado para testar uma carga média constante durante um período de tempo necessário. Qualquer degradação de desempenho pode ser analisada.

| Cenário | Tipo de teste | Não. de usuários | Tx/s (esperado) | Tx/s (testado) | Descrição |
|---|---|---|---|---|---|
| Ensaio de resistência (72 horas) | Página inicial | 10 | 1 |  |  |
|   | Pesquisar | 10 | 1 |  |  |
|   | Notícias | 20 | 2 |  |  |
|   | Eventos | 10 | 1 |  |  |
|   | Ativações | 1 | 3 |  | Simulação do comportamento do autor. |

### Otimização {#optimization}

Nos estágios posteriores da implementação, otimize o aplicativo para atender e maximizar as metas de desempenho.

Quaisquer otimizações feitas devem ser testadas para garantir que tenham:

* Não afetou a funcionalidade
* Foi verificado com os testes de carga antes de ser liberado

Uma seleção de ferramentas está disponível para ajudá-lo com a geração de carga, monitoramento de desempenho e análise de resultados. Algumas dessas ferramentas incluem o seguinte:

* [JMeter](https://jmeter.apache.org/)
* [Carregar Executor](https://www.microfocus.com/en-us/portfolio/performance-engineering/overview)
* [InfraRED](https://www.infraredsoftware.com/)
* [Perfil interativo Java™](https://jiprof.sourceforge.net/)

Após a otimização, teste novamente para confirmar o impacto.

### Relatório {#reporting}

Relatórios contínuos mantêm todos informados sobre o status. Como mencionado anteriormente com a codificação por cores, o mapa da arquitetura pode ser usado para esse status.

Após a conclusão de todos os testes, relatar o seguinte:

* Todos os erros críticos encontrados
* Problemas não críticos que ainda precisam ser investigados
* Quaisquer suposições feitas durante os testes
* Quaisquer recomendações a serem emitidas a partir do teste

## Otimização do desempenho ao usar o Dispatcher {#optimizing-performance-when-using-the-dispatcher}

O [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR) é uma ferramenta de armazenamento em cache e/ou balanceamento de carga Adobe. Ao usar o Dispatcher, considere otimizar seu site para o desempenho do cache.

>[!NOTE]
>
>As versões do Dispatcher são independentes do AEM, no entanto, a documentação do Dispatcher está incorporada na documentação do AEM. Sempre use a documentação do Dispatcher incorporada à documentação da versão mais recente do AEM.
>
>Você pode ter sido redirecionado para esta página se tiver seguido um link para a documentação do Dispatcher incorporada à documentação de uma versão anterior do AEM.

O Dispatcher oferece vários mecanismos integrados que você pode usar para otimizar o desempenho se o site se beneficiar deles. Esta seção informa como projetar seu site para potencializar os benefícios do armazenamento em cache.

>[!NOTE]
>
>Pode ser útil ter em mente que o Dispatcher armazena o cache em um servidor da Web padrão. Conhecer essas informações significa que você pode armazenar em cache tudo o que pode armazenar como uma página e solicitar usando um URL. Além disso, não é possível armazenar outras coisas, como cookies, dados de sessão e dados de formulário.
>
>Em geral, várias estratégias de armazenamento em cache envolvem selecionar bons URLs e não depender desses dados adicionais.
>
>Com a versão 4.1.11 do Dispatcher, também é possível armazenar cabeçalhos de resposta em cache. Consulte [Armazenamento em cache de cabeçalhos de resposta HTTP](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache).
>

### Cálculo da taxa de cache do Dispatcher {#calculating-the-dispatcher-cache-ratio}

A fórmula da proporção de cache estima a porcentagem de solicitações tratadas pelo cache em relação ao número total de solicitações que entram no sistema. Para calcular a proporção do cache, você precisa do seguinte:

* O número total de solicitações. Essas informações estão disponíveis no Apache `access.log`. Para obter mais detalhes, consulte a [documentação oficial do Apache](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

* O número de solicitações atendidas pela instância do Publish. Essas informações estão disponíveis no `request.log` da instância. Para obter mais detalhes, consulte [Interpretando request.log](/help/sites-deploying/monitoring-and-maintaining.md#interpreting-the-request-log) e [Localizando os Arquivos de Log](/help/sites-deploying/monitoring-and-maintaining.md#finding-the-log-files).

A fórmula para calcular a proporção do cache é:

* (O número total de solicitações **menos** o número de solicitações no Publish) **dividido** pelo número total de solicitações.

Por exemplo, se o número total de solicitações for 129491 e o número de solicitações atendidas pela instância do Publish for 58959, a relação de cache será: **(129491 - 58959)/129491= 54,5%**.

Se você não tiver um emparelhamento de editor/dispatcher um para um, adicione solicitações de todos os dispatchers e editores juntos para obter uma medição precisa. Consulte também [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md).

>[!NOTE]
>
>Para melhor desempenho, a Adobe recomenda uma taxa de cache de 90% a 95%.

#### Uso de codificação de página consistente {#using-consistent-page-encoding}

Com a versão 4.1.11 do Dispatcher, você pode armazenar em cache cabeçalhos de resposta. Se você não estiver armazenando cabeçalhos de resposta em cache no Dispatcher, poderão ocorrer problemas se você armazenar informações de codificação de página no cabeçalho. Nessa situação, quando o Dispatcher fornece uma página do cache, a codificação padrão do servidor Web é usada para a página. Há duas maneiras de evitar esse problema:

* Se você usar apenas uma codificação, verifique se a codificação usada no servidor Web é igual à codificação padrão do site do AEM.
* Para definir a codificação, use uma tag `<META>` na seção `head` do HTML, como no exemplo a seguir:

```xml
        <META http-equiv="Content-Type" content="text/html; charset=EUC-JP">
```

#### Evitar parâmetros de URL {#avoid-url-parameters}

Se possível, evite parâmetros de URL para páginas que você deseja armazenar em cache. Por exemplo, se você tiver uma galeria de imagens, o URL a seguir nunca será armazenado em cache (a menos que o Dispatcher esteja [configurado adequadamente](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache)):

```xml
www.myCompany.com/pictures/gallery.html?event=christmas&amp;page=1
```

No entanto, você pode colocar esses parâmetros no URL da página, da seguinte maneira:

```xml
www.myCompany.com/pictures/gallery.christmas.1.html
```

>[!NOTE]
>
>Esta URL chama a mesma página e o mesmo modelo que `gallery.html`. Na definição do modelo, é possível especificar qual script renderiza a página ou usar o mesmo script para todas as páginas.

#### Personalizar por URL {#customize-by-url}

Se você permitir que os usuários alterem o tamanho da fonte (ou qualquer outra personalização de layout), verifique se as diferentes personalizações são refletidas no URL.

Por exemplo, os cookies não são armazenados em cache. Dessa forma, se você armazenar o tamanho da fonte em um cookie (ou mecanismo semelhante), o tamanho da fonte não será preservado para a página em cache. Como resultado, o Dispatcher retorna documentos de qualquer tamanho de fonte aleatoriamente.

Incluir o tamanho da fonte no URL como um seletor evita esse problema:

```xml
www.myCompany.com/news/main.large.html
```

>[!NOTE]
>
>Para a maioria dos aspectos de layout, também é possível usar folhas de estilos e/ou scripts do lado do cliente. Esses instrumentos funcionam bem com o armazenamento em cache.
>
>Essa estratégia também é útil para uma versão impressa, na qual você pode usar um URL como:
>
>`www.myCompany.com/news/main.print.html`
>
>Usando o recurso de curinga de script da definição do modelo, você pode especificar um script separado que renderize as páginas de impressão.

#### Invalidar arquivos de imagem usados como títulos {#invalidating-image-files-used-as-titles}

Se você renderizar títulos de página, ou outro texto, como imagens, é recomendável armazenar os arquivos para que eles sejam excluídos após uma atualização de conteúdo na página:

1. Coloque o arquivo de imagem na mesma pasta da página.
1. Use o seguinte formato de nomenclatura para o arquivo de imagem:

   `<page file name>.<image file name>`

Por exemplo, você pode armazenar o título da página `myPage.html` em `file myPage.title.gif`. Esse arquivo será automaticamente excluído se a página for atualizada, de modo que qualquer alteração no título da página será refletida automaticamente no cache.

>[!NOTE]
>
>O arquivo de imagem não existe necessariamente fisicamente na instância do AEM. Você pode usar um script que cria dinamicamente o arquivo de imagem. O Dispatcher armazena o arquivo no servidor Web.

#### Invalidar arquivos de imagem usados para navegação {#invalidating-image-files-used-for-navigation}

Se você usar imagens para as entradas de navegação, o método é basicamente o mesmo com títulos, mas ligeiramente mais complexo. Armazene todas as imagens de navegação com as páginas de destino. Se você usar duas imagens para o normal e o ativo, poderá usar os seguintes scripts:

* Um script que exibe a página, como de costume.
* Um script que processa solicitações &quot;.normal&quot; e retorna a imagem normal.
* Um script que processa solicitações &quot;.active&quot; e retorna a imagem ativada.

É importante criar essas imagens com o mesmo identificador de nome da página, para garantir que uma atualização de conteúdo exclua essas imagens e a página.

Para páginas que não são modificadas, as imagens ainda permanecem no cache, embora as próprias páginas sejam invalidadas automaticamente.

#### Personalização {#personalization}

É recomendável limitar a personalização ao local necessário. Para ilustrar o motivo:

* Se você usar uma página inicial personalizável livremente, essa página deverá ser composta sempre que um usuário a solicitar.
* Se, por outro lado, você oferecer a opção de dez páginas iniciais diferentes, poderá armazenar em cache cada uma delas para melhorar o desempenho.

>[!TIP]
>Para obter mais detalhes sobre como configurar o cache do Dispatcher, consulte o [Tutorial de cache do Dispatcher do AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/dispatcher-tutorial/overview.html) e sua seção sobre [Armazenamento em cache de conteúdo protegido.](https://experienceleague.adobe.com/docs/experience-manager-learn/dispatcher-tutorial/chapter-1.html#dispatcher-tips-and-tricks)

Se você personalizar cada página colocando o nome do usuário na barra de título (por exemplo), isso terá um impacto no desempenho.

>[!TIP]
>Para armazenar em cache conteúdo protegido, consulte [Armazenamento em cache de conteúdo protegido](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=pt-BR) no guia do Dispatcher.

Em relação à combinação de conteúdo restrito e público em uma página, considere uma estratégia que use inclusões do lado do servidor no Dispatcher ou inclusões do lado do cliente por meio do Ajax no navegador.

>[!TIP]
>
>Para gerenciar conteúdo misto público e restrito, consulte [Configurar Sling Dynamic Include.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-sling-dynamic-include.html)

#### Conexões adesivas {#sticky-connections}

As [conexões adesivas](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#the-benefits-of-load-balancing) garantem que os documentos de um usuário sejam todos compostos no mesmo servidor. Se um usuário sair dessa pasta e posteriormente retornar a ela, a conexão ainda permanecerá. Para armazenar todos os documentos que exigem conexões adesivas para o site, defina uma pasta. Tente não manter outros documentos nela. Esse cenário afeta o balanceamento de carga se você usar páginas personalizadas e dados de sessão.

#### Tipos MIME {#mime-types}

Há duas maneiras pelas quais um navegador pode determinar o tipo de arquivo:

1. Pela sua extensão (por exemplo, `.html`, `.gif` e `.jpg`).
1. Pelo tipo MIME que o servidor envia com o arquivo.

Para a maioria dos arquivos, o tipo MIME está implícito na extensão de arquivo. Ou seja,

1. Pela sua extensão (por exemplo, `.html`, `.gif` e `.jpg`).
1. Pelo tipo MIME que o servidor envia com o arquivo.

Se o nome do arquivo não tiver extensão, ele será exibido como texto sem formatação.

Com a versão 4.1.11 do Dispatcher, você pode armazenar em cache cabeçalhos de resposta. Se você não armazenar cabeçalhos de resposta em cache no Dispatcher, o tipo MIME fará parte do cabeçalho HTTP. Dessa forma, se o aplicativo AEM retornar arquivos que não têm um final de arquivo reconhecido e depender do tipo MIME, esses arquivos poderão ser exibidos incorretamente.

Para garantir que os arquivos sejam armazenados em cache corretamente, siga estas diretrizes:

* Certifique-se de que os arquivos sempre tenham a extensão adequada.
* Evite scripts de servidor de arquivos genéricos, que tenham URLs como `download.jsp?file=2214`. Para usar URLs contendo a especificação do arquivo, reescreva o script. Para o exemplo anterior, essa regravação é `download.2214.pdf`.

## Desempenho do backup {#backup-performance}

Esta seção apresenta uma série de benchmarks usados para avaliar o desempenho de backups por AEM e os efeitos da atividade de backup sobre o desempenho do aplicativo. Os backups por AEM apresentam uma carga significativa no sistema enquanto ele é executado, e o Adobe mede esse impacto e os efeitos das configurações de atraso de backup que tentam modular esses efeitos. O objetivo é oferecer alguns dados de referência sobre o desempenho esperado dos backups em configurações realistas e quantidades de dados de produção, e fornecer orientação sobre como estimar os tempos de backup para sistemas planejados.

### Ambiente de referência {#reference-environment}

#### Sistema físico {#physical-system}

Os resultados relatados neste documento foram obtidos de benchmarks executados em um ambiente de referência com a seguinte configuração: Essa configuração é semelhante a um ambiente de produção típico em um data center:

* HP ProLiant DL380 G6, 8 CPUs x 2,533 GHz
* Unidades Serial Attached SCSI de 300 GB e 10.000 RPM
* Controlador RAID de hardware; oito unidades em um storage RAID0+5
* CPU de imagem VMware x 2 Intel Xeon® E5540 a 2,53 GHz
* Red Hat® Linux® 2.6.18-194.el5; Java™ 1.6.0_29
* Instância única do autor

O subsistema de discos neste servidor é rápido, representativo de uma configuração RAID de alto desempenho que pode ser usada em um servidor de produção. O desempenho do backup pode ser sensível ao desempenho do disco, e os resultados nesse ambiente refletem o desempenho em uma configuração RAID rápida. A imagem VMWare é configurada para ter um único grande volume de disco que reside fisicamente no armazenamento de disco local, no array RAID.

A configuração do AEM coloca o repositório e o armazenamento de dados no mesmo volume lógico, juntamente com o sistema operacional e o software AEM. O diretório de destino para backups também reside nesse sistema de arquivos lógico.

#### Volumes de dados {#data-volumes}

A tabela a seguir ilustra o tamanho dos volumes de dados usados nos benchmarks de backup. O conteúdo inicial da linha de base é instalado primeiro e, em seguida, quantidades adicionais conhecidas de dados são adicionadas para aumentar o tamanho do conteúdo de backup. Os backups são criados em incrementos específicos para representar um grande aumento no conteúdo e o que pode ser produzido em um dia. A distribuição de conteúdo (páginas, imagens, tags) baseia-se aproximadamente na composição realista do ativo de produção. Páginas, imagens e tags são limitadas a no máximo 800 páginas secundárias. Cada página inclui componentes de título, Flash, texto/imagem, vídeo, apresentação de slides, formulário, tabela, nuvem e carrossel. As imagens são carregadas de um pool de 400 arquivos exclusivos com tamanho de 37 KB a 594 KB.

| Conteúdo | Nós | Páginas | Imagens | Tags |
|---|---|---|---|---|
| Instalação base | 69 610 | 562 | 256 | 237 |
| Conteúdo pequeno para backup incremental |  | +100 | +2 | +2 |
| Grande conteúdo para backup completo |  | +10 000 | +100 | +100 |

O benchmark de backup é repetido com os conjuntos de conteúdo adicionais adicionados a cada repetição.

#### Cenários de benchmark {#benchmark-scenarios}

Os benchmarks de backup abrangem dois cenários principais: backups quando o sistema está sob carga significativa de aplicativos e backups quando o sistema está ocioso. Embora a recomendação geral seja que os backups sejam executados quando o AEM estiver o mais ocioso possível, há situações em que é necessário que o backup seja executado quando o sistema estiver sob carga.

* **Estado Ocioso** - Os backups são executados sem nenhuma outra atividade no AEM.
* **Sob Carregamento** - Os backups são executados enquanto o sistema está sob 80% de carga de processos online. O atraso do backup variou para ver o impacto na carga.

Os tempos de backup e o tamanho do backup resultante são obtidos dos registros do servidor AEM. Normalmente, recomenda-se que os backups sejam agendados para períodos fora do horário de expediente quando o AEM estiver ocioso, por exemplo, no meio da noite. Este cenário é representativo da abordagem recomendada.

O carregamento consiste em páginas criadas, páginas excluídas, percursos e consultas com a maioria das cargas provenientes de percursos e consultas de página. Adicionar e remover muitas páginas aumenta continuamente o tamanho do espaço de trabalho e impede que os backups sejam concluídos. A distribuição de carga que o script usa é de 75% de percursos de página, 24% de consultas e 1% de criações de página (nível único sem subpáginas aninhadas). A média de pico de transações por segundo em um sistema ocioso é alcançada com quatro threads simultâneos, que são usados ao testar backups sob carga.

O impacto da carga no desempenho de backup pode ser estimado pela diferença entre o desempenho com e sem essa carga de aplicativo. O impacto do backup no throughput do aplicativo é encontrado ao comparar o throughput do cenário em transações por hora com e sem um backup simultâneo em andamento e com backups em operação com diferentes configurações de &quot;atraso de backup&quot;.

* **Configuração de Atraso** - Para vários cenários, a configuração de atraso de backup também variou, usando valores de 10 milissegundos (padrão), 1 milissegundo e 0 milissegundo, para explorar como essa configuração afetou o desempenho dos backups.
* **Tipo de Backup** - Todos os backups eram backups externos do repositório feitos em um diretório de backup sem criar um zip, exceto em um caso para comparação em que o comando tar foi usado diretamente. Como os backups incrementais não podem ser criados em um arquivo zip, ou quando o backup completo anterior é um arquivo zip, o método de diretório de backup é o mais usado em situações de produção.

### Resumo dos resultados {#summary-of-results}

#### Tempo e throughput do backup {#backup-time-and-throughput}

O principal resultado desses benchmarks é mostrar como os tempos de backup variam em função do tipo de backup e da quantidade geral de dados. O gráfico a seguir mostra o tempo de backup obtido usando a configuração de backup padrão, em função do número total de páginas.

![chlimage_1-81](assets/chlimage_1-81.png)

Os tempos de backup em uma instância ociosa são bastante consistentes, com uma média de 0,608 MB por segundo, independentemente de backups completos ou incrementais (consulte o gráfico abaixo). O tempo de backup é simplesmente uma função do volume de dados do backup. O tempo para concluir um backup completo aumenta claramente de acordo com o número total de páginas. O tempo para concluir um backup incremental também aumenta com o número total de páginas, mas em uma taxa muito menor. O tempo necessário para concluir o backup incremental é muito menor devido à quantidade relativamente pequena de dados cujo backup está sendo feito.

O tamanho do backup produzido é o principal determinante do tempo necessário para concluir um backup. O gráfico a seguir mostra o tempo gasto em função do tamanho final do backup.

![chlimage_1-82](assets/chlimage_1-82.png)

Este gráfico ilustra que tanto os backups incrementais quanto os completos seguem um padrão simples de tamanho e tempo que o Adobe pode medir como throughput. Os tempos de backup em uma instância ociosa são bastante consistentes, com uma média de 0,61 MB por segundo, independentemente de backups completos ou incrementais no ambiente de benchmark.

#### Atraso de backup {#backup-delay}

O parâmetro de atraso de backup é fornecido para limitar a extensão em que os backups podem interferir nas cargas de trabalho de produção. O parâmetro especifica um tempo de espera em milissegundos, que é alternado para a operação de backup em cada arquivo. O efeito geral depende em parte do tamanho dos arquivos afetados. A medição do desempenho do backup em MB/s oferece uma maneira razoável de comparar os efeitos do atraso no backup.

* A execução simultânea de um backup com a carga normal do aplicativo tem um impacto negativo no throughput da carga normal.
* O impacto pode ser leve (até 5%) ou significativo, causando uma queda de até 75% no throughput. Provavelmente depende mais do aplicativo.
* O backup não é uma carga pesada na CPU e, portanto, as cargas de trabalho de produção com uso intenso da CPU seriam menos afetadas pelo backup do que as de I/O intensivo.

![chlimage_1-83](assets/chlimage_1-83.png)

Para comparação, o throughput obtido usando um backup do sistema de arquivos (&quot;tar&quot;) para fazer backup dos mesmos arquivos do repositório. O desempenho do tar é comparável, mas ligeiramente superior ao do backup com atraso definido como zero. Mesmo um pequeno atraso reduz muito o throughput de backup, e o atraso padrão de 10 milissegundos resulta em um throughput bastante reduzido. Em situações em que os backups podem ser programados quando o uso geral do aplicativo for baixo ou o aplicativo puder estar ocioso, reduza o atraso abaixo do valor padrão para permitir que o backup prossiga mais rapidamente.

O impacto real do throughput de aplicativos de um backup contínuo depende dos detalhes do aplicativo e da infraestrutura. A escolha do valor do atraso deve ser feita por meio da análise empírica do aplicativo, mas deve ser escolhida o menor possível, para que os backups possam ser concluídos o mais rápido possível. Como há apenas uma fraca correlação entre a escolha do valor de atraso e o impacto no throughput do aplicativo, a escolha do atraso deve favorecer tempos gerais de backup mais curtos para minimizar o impacto geral dos backups. Um backup que leva oito horas para ser concluído, mas afeta o throughput em -20%, provavelmente terá um impacto geral maior do que um backup que leva duas horas para ser concluído, mas afeta o throughput em -30%.

### Referências {#references}

* [Administração - Backup e restauração](/help/sites-administering/backup-and-restore.md)
* [Gerenciamento - Capacidade e volume](/help/managing/best-practices-further-reference.md#capacity-and-volume)
