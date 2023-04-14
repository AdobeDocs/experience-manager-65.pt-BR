---
title: Otimização de desempenho
description: Saiba como configurar certos aspectos do AEM para otimizar o desempenho.
uuid: a4d9fde4-a4c7-4ee5-99b6-29b0ee7dc35b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 80118cd1-73e1-4675-bbdf-85d66d150abc
feature: Configuring
exl-id: 5b0c9a8c-0f5f-46ee-a455-adb9b9d27270
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '6503'
ht-degree: 12%

---

# Otimização de desempenho {#performance-optimization}

>[!NOTE]
>
>Para obter as diretrizes gerais sobre desempenho, leia a [Diretrizes de desempenho](/help/sites-deploying/performance-guidelines.md) página.
>
>Para obter mais informações sobre solução de problemas e correção de problemas de desempenho, consulte também a seção [Árvore de desempenho](/help/sites-deploying/performance-tree.md).
>
>Além disso, você pode revisar um artigo da Base de conhecimento em [Dicas para ajuste de desempenho](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=pt-BR).

Um problema importante é o tempo que seu site leva para responder às solicitações do visitante. Embora esse valor varie para cada solicitação, um valor médio de target pode ser definido. Uma vez que esse valor seja comprovadamente alcançável e sustentável, ele poderá ser usado para monitorar o desempenho do site e indicar o desenvolvimento de possíveis problemas.

Os tempos de resposta almejados são diferentes nos ambientes de criação e publicação, refletindo as diferentes características do público-alvo:

## Ambiente de criação {#author-environment}

Esse ambiente é usado pelos autores que inserem e atualizam o conteúdo. Ela deve atender a alguns usuários que geram um alto número de solicitações de alto desempenho ao atualizar páginas de conteúdo e os elementos individuais nessas páginas.

## Ambiente de publicação {#publish-environment}

Esse ambiente contém conteúdo que você disponibiliza para seus usuários. Neste caso, o número de pedidos é ainda maior e a velocidade é tão vital. Contudo, dado que a natureza dos pedidos é menos dinâmica, podem ser aplicados mecanismos adicionais de melhoria do desempenho; como armazenar em cache o conteúdo ou balanceamento de carga.

>[!NOTE]
>
>* Após configurar para otimização de desempenho, siga os procedimentos em [Dia difícil](/help/sites-developing/tough-day.md) testar o ambiente sob carga pesada.
>* Consulte também [Dicas para melhorar o desempenho.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=pt-BR)


## Metodologia de Otimização de Desempenho {#performance-optimization-methodology}

Uma metodologia de otimização de desempenho para Projetos de AEM pode ser resumida em cinco regras simples que podem ser seguidas para evitar problemas de desempenho desde o início:

1. [Planejamento para otimização](#planning-for-optimization)
1. [Simular Realidade](#simulate-reality)
1. [Estabelecer metas sólidas](#establish-solid-goals)
1. [Permanecer relevante](#stay-relevant)
1. [Ciclos de Iteração Ágil](#agile-iteration-cycles)

Essas regras se aplicam a projetos da Web em geral e são relevantes para gerentes de projeto e administradores de sistema para garantir que seus projetos não enfrentem desafios de desempenho quando chegar o momento da inicialização.

### Planejamento para otimização {#planning-for-optimization}

![chlimage_1-3](assets/chlimage_1-3.jpeg)

Planeje cerca de 10% do esforço do projeto para a fase de otimização de desempenho. Os requisitos reais de otimização de desempenho dependem do nível de complexidade de um projeto e da experiência da equipe de desenvolvimento. Embora seu projeto possa (em última análise) não exigir o tempo alocado, é uma boa prática sempre planejar a otimização de desempenho na região sugerida.

Sempre que possível, um projeto deve ser lançado suavemente para um público-alvo limitado para coletar a experiência real e realizar mais otimizações, sem a pressão adicional que se segue a um anúncio completo.

Depois de &quot;ao vivo&quot;, a otimização de desempenho não acaba. Agora é quando você enfrenta a carga &quot;real&quot; em seu sistema. É importante planejar ajustes adicionais após o lançamento.

Como a carga do sistema muda e os perfis de desempenho do sistema mudam ao longo do tempo, uma &quot;atualização&quot; ou &quot;verificação de integridade&quot; de desempenho deve ser agendada em intervalos de 6 a 12 meses.

### Simular Realidade {#simulate-reality}

![chlimage_1-4](assets/chlimage_1-4.jpeg)

Se você for ao ar com um site e descobrir depois do lançamento que você tem problemas de desempenho, é provável que seus testes de carga e desempenho não simulem a realidade de perto o suficiente.

Simular a realidade é difícil e o esforço que você deseja investir para obter &quot;real&quot; depende da natureza do seu projeto. &quot;Real&quot; significa não apenas &quot;código real&quot; e &quot;tráfego real&quot;, mas também &quot;conteúdo real&quot;, especialmente em relação à dimensão e estrutura do conteúdo. Seus modelos podem se comportar de forma diferente dependendo do tamanho e da estrutura do repositório.

### Estabelecer metas sólidas {#establish-solid-goals}

![chlimage_1-5](assets/chlimage_1-5.jpeg)

A importância de estabelecer adequadamente objetivos de desempenho não deve ser subestimada. Muitas vezes, depois que as pessoas se concentram em metas específicas de desempenho, é difícil alterar essas metas posteriormente, mesmo que elas se baseiem em suposições.

Estabelecer metas de desempenho boas e sólidas é realmente uma das áreas mais difíceis. Geralmente, é melhor coletar registros e benchmarks da vida real de um site comparável (por exemplo, o antecessor do novo site).

### Permanecer relevante {#stay-relevant}

![chlimage_1-6](assets/chlimage_1-6.jpeg)

É importante otimizar um gargalo de cada vez. Se você tentar fazer as coisas em paralelo sem validar o impacto de uma otimização, poderá perder o controle de qual medida de otimização ajudou.

### Ciclos de Iteração Ágil {#agile-iteration-cycles}

![chlimage_1-7](assets/chlimage_1-7.jpeg)

O ajuste de desempenho é um processo iterativo que envolve, medição, análise, otimização e validação até que a meta seja alcançada. Para levar em conta esse aspecto, implemente um processo de validação ágil na fase de otimização, em vez de um processo de teste mais pesado após cada iteração.

Esse foco significa que o desenvolvedor que implementa a otimização deve ter uma maneira rápida de saber se a otimização já atingiu a meta. Essas informações são importantes, pois quando a meta é atingida, a otimização termina.

## Diretrizes básicas de desempenho {#basic-performance-guidelines}

Geralmente, mantenha suas solicitações html não armazenadas em cache para menos de 100 milissegundos. Mais especificamente, os seguintes podem servir como diretriz:

* 70% das solicitações de páginas devem ser respondidas em menos de 100 milissegundos.
* 25% das solicitações de páginas devem receber uma resposta em 100 milissegundos - 300 milissegundos.
* 4% das solicitações de páginas devem receber uma resposta em 300 milissegundos - 500 milissegundos.
* 1% das solicitações de páginas devem receber uma resposta em 500 milissegundos - 1000 milissegundos.
* Nenhuma página deve responder mais lentamente do que 1 segundo.

Os números acima assumem as seguintes condições:

* Medido na publicação (sem custos indiretos relacionados a um ambiente de criação)
* Medido no servidor (sem sobrecarga de rede)
* Não armazenado em cache (sem cache de saída AEM, sem cache do Dispatcher)
* Somente para itens complexos com muitas dependências (HTML, JS, PDF, ...)
* Nenhuma outra carga no sistema

Há alguns problemas que frequentemente contribuem para problemas de desempenho, incluindo o seguinte:

* Ineficiência do armazenamento em cache do Dispatcher
* O uso de consultas em modelos de exibição normais.

O ajuste de nível da JVM e do SO geralmente não gera saltos significativos no desempenho e, portanto, deve ser executado no final do ciclo de otimização.

A maneira como um repositório de conteúdo é estruturado também pode afetar o desempenho. Para melhor desempenho, o número de nós filhos anexados a nós individuais em um repositório de conteúdo não deve exceder 1.000 (como regra).

Seus melhores amigos durante um exercício normal de otimização de desempenho são:

* O `request.log`
* Tempo baseado em componentes
* Um criador de perfis Java™.

### Desempenho ao carregar e editar Ativos digitais {#performance-when-loading-and-editing-digital-assets}

Devido ao grande volume de dados envolvidos ao carregar e editar ativos digitais, o desempenho pode se tornar um problema.

Duas coisas afetam o desempenho aqui:

* CPU - vários núcleos permitem um trabalho mais suave durante a transcodificação
* Disco rígido - discos RAID paralelos alcançam o mesmo

Para melhorar o desempenho, considere o seguinte:

* Quantos ativos serão carregados por dia? Uma boa estimativa pode ser baseada em:

![chlimage_1-77](assets/chlimage_1-77.png)

* O período em que as edições são efetuadas (normalmente, a duração do dia útil, mais para as operações internacionais).
* O tamanho médio das imagens carregadas (e o tamanho das representações geradas por imagem) em megabytes.
* Determine a taxa média de dados:

![chlimage_1-78](assets/chlimage_1-78.png)

* 80% de todas as edições são feitas em 20% do tempo, portanto, no tempo de pico você tem quatro vezes a taxa média de dados. Esse desempenho é o seu objetivo.

## Monitoramento de desempenho {#performance-monitoring}

O desempenho (ou a falta dele) é uma das primeiras coisas que seus usuários notam, de modo que, com qualquer aplicativo com uma interface do usuário, o desempenho é de importância fundamental. Para otimizar o desempenho da instalação do AEM, monitore vários atributos da instância e seu comportamento.

Para obter informações sobre como executar o monitoramento de desempenho, consulte [Monitorar desempenho](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance).

Os problemas que causam problemas de desempenho geralmente são difíceis de serem rastreados, mesmo quando seus efeitos são fáceis de ver.

Um ponto de partida básico é um bom conhecimento do seu sistema quando ele está funcionando normalmente. A menos que você saiba como seu ambiente &quot;parece&quot; e &quot;se comporta&quot; quando ele funciona corretamente, é difícil localizar o problema quando o desempenho se deteriora. Gaste tempo investigando seu sistema quando ele está funcionando sem problemas e garanta que a coleta de informações de desempenho é uma tarefa em andamento. Isso fornece uma base para comparação caso o desempenho seja afetado.

O diagrama a seguir ilustra o caminho que uma solicitação de conteúdo AEM pode tomar e, portanto, o número de elementos diferentes que podem afetar o desempenho.

![chlimage_1-79](assets/chlimage_1-79.png)

O desempenho também é um equilíbrio entre volume e capacidade:

* **Volume** - A quantidade de produção processada e entregue pelo sistema.
* **Capacidade** - A capacidade do sistema de fornecer o volume.

O desempenho pode ser ilustrado em vários locais da cadeia da Web.

![chlimage_1-80](assets/chlimage_1-80.png)

Há várias áreas funcionais que geralmente são responsáveis por afetar o desempenho:

* Armazenamento em cache
* Código do aplicativo (projeto)
* Funcionalidade de pesquisa

### Regras básicas sobre desempenho {#basic-rules-regarding-performance}

Algumas regras devem ser levadas em conta ao otimizar o desempenho:

* Ajuste de desempenho *must* fazer parte de cada projeto.
* Não otimize no início do ciclo de desenvolvimento.
* O desempenho é tão bom quanto o elo mais fraco.
* Sempre pense em capacidade x volume.
* Otimize coisas importantes primeiro.
* Nunca otimizar sem *realista* objetivos.

>[!NOTE]
>
>Lembre-se de que o mecanismo usado para medir o desempenho geralmente afeta exatamente o que você está tentando medir. Tente contabilizar essas discrepâncias e eliminar o máximo possível do seu efeito; em particular, os plug-ins de navegadores devem ser desativados sempre que possível.

## Configuração para desempenho {#configuring-for-performance}

Determinados aspectos do AEM (e/ou do repositório subjacente) podem ser configurados para otimizar o desempenho. Veja a seguir as possibilidades e sugestões, você deve ter certeza se, ou como, usa a funcionalidade em questão antes de fazer alterações.

>[!NOTE]
>
>Consulte [Otimização de desempenho](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=pt-BR).

### Indexação de Pesquisa {#search-indexing}

A partir do AEM 6.0, o Adobe Experience Manager usa uma arquitetura de repositório baseada em Oak.

Você pode encontrar as informações de indexação atualizadas aqui:

* [Práticas recomendadas para consultas e indexação](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [Consultas e indexação](/help/sites-deploying/queries-and-indexing.md)

### Processamento de fluxo de trabalho simultâneo {#concurrent-workflow-processing}

Para melhorar o desempenho, limite o número de processos de fluxo de trabalho executados simultaneamente. Por padrão, o mecanismo de workflow processa tantos workflows em paralelo quanto há processadores disponíveis para a Java™ VM. Quando as etapas do fluxo de trabalho exigem grandes quantidades de recursos de processamento (RAM ou CPU), executar vários desses fluxos de trabalho em paralelo pode colocar altas demandas nos recursos disponíveis do servidor.

Por exemplo, quando imagens (ou ativos DAM em geral) são carregadas, os fluxos de trabalho importam automaticamente as imagens para o DAM. As imagens geralmente são de alta resolução e podem facilmente consumir centenas de MB de heap para processamento. Manipular essas imagens em paralelo coloca uma alta carga no subsistema da memória e no coletor de lixo.

O mecanismo de workflow usa as filas de job do Apache Sling para manusear e agendar o processamento de itens de trabalho. Os seguintes serviços de fila de trabalhos foram criados por padrão a partir do Apache Sling Job Queue Configuration fatory para processar trabalhos de fluxo de trabalho:

* Fila de Fluxo de Trabalho do Granite: A maioria das etapas do fluxo de trabalho, como aquelas que processam ativos DAM, usa o serviço Granite Workflow Queue .
* Fila de Trabalho do Processo Externo do Fluxo de Trabalho Granite: Esse serviço é usado para etapas de fluxo de trabalho externo especiais, que normalmente são usadas para entrar em contato com um sistema externo e pesquisar resultados. Por exemplo, a etapa Processo de extração de mídia do InDesign é implementada como um processo externo. O mecanismo de workflow usa a fila externa para processar a pesquisa. (Consulte [com.day.cq.workflow.exec.WorkflowExternalProcess](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/exec/WorkflowExternalProcess.html).)

Configure esses serviços para limitar o número máximo de processos de workflow em execução simultânea.

>[!NOTE]
>
>A configuração dessas filas de trabalhos afeta todos os fluxos de trabalho, a menos que tenha criado uma fila de trabalhos para um modelo de fluxo de trabalho específico (consulte [Configurar a fila para um modelo de fluxo de trabalho específico](/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow) abaixo).

#### Configuração no Repositório {#configuration-in-the-repo}

Se você estiver configurando os serviços [usando um nó sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository), você deve encontrar o PID dos serviços existentes, por exemplo: org.apache.sling.event.jobs.QueueConfiguration.370aad73-d01b-4a0b-abe4-20198d85f705. Você pode descobrir o PID usando o Console da Web.

Configure a propriedade chamada `queue.maxparallel`.

#### Configuração no Console da Web {#configuration-in-the-web-console}

Para configurar esses serviços [usando o Console da Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), localize os itens de configuração existentes abaixo da fábrica do serviço Configuração da fila de trabalhos do Apache Sling.

Configure a propriedade chamada Maximum Parallel Jobs (Máximo trabalhos paralelos).

### Configurar a fila para um fluxo de trabalho específico {#configure-the-queue-for-a-specific-workflow}

Crie uma fila de trabalhos para um modelo de fluxo de trabalho específico para configurar a manipulação de tarefas para esse modelo de fluxo de trabalho. Dessa forma, suas configurações afetam o processamento de um fluxo de trabalho específico, enquanto a configuração padrão da Fila de fluxo de trabalho do Granite controla o processamento de outros fluxos de trabalho.

Quando modelos de fluxo de trabalho são executados, eles criam trabalhos do Sling para um tópico específico. Por padrão, o tópico corresponde aos tópicos configurados para a fila geral de fluxo de trabalho do Granite ou para a fila de trabalhos do processo externo do fluxo de trabalho do Granite:

* `com/adobe/granite/workflow/job*`
* `com/adobe/granite/workflow/external/job*`

Os tópicos reais do job que os modelos de workflow geram incluem o sufixo específico do modelo. Por exemplo, a variável **Ativo de atualização DAM** modelo de fluxo de trabalho gera trabalhos com o seguinte tópico:

`com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model`

Portanto, você pode criar uma fila de trabalhos para o tópico que corresponda aos tópicos de tarefa do seu modelo de fluxo de trabalho. Configurar as propriedades relacionadas ao desempenho da fila afeta apenas o modelo de fluxo de trabalho que gera trabalhos que correspondem ao tópico da fila.

O procedimento a seguir cria uma fila de trabalhos para um fluxo de trabalho, usando o **Ativo de atualização DAM** como exemplo.

1. Execute o modelo de fluxo de trabalho para o qual deseja criar a fila de trabalhos para que as estatísticas de tópicos sejam geradas. Por exemplo, adicione uma imagem ao Assets para executar a variável **Ativo de atualização DAM** fluxo de trabalho.
1. Abra o console Sling Jobs (`https://<host>:<port>/system/console/slingevent`).
1. Descubra os tópicos relacionados ao fluxo de trabalho no console. Para o Ativo de atualização DAM, os seguintes tópicos são encontrados:

   * `com/adobe/granite/workflow/external/job/etc/workflow/models/dam/update_asset/jcr_content/model`
   * `com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model`
   * `com/adobe/granite/workflow/job/etc/workflow/models/dam-xmp-writeback/jcr_content/model`

1. Crie uma fila de trabalhos para cada um desses tópicos. Para criar uma fila de trabalhos, crie uma configuração de fábrica para o serviço de fábrica Apache Sling Job Queue .

   As configurações de fábrica são semelhantes à Fila de Fluxo de Trabalho do Granite descrita em [Processamento de fluxo de trabalho simultâneo](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing), exceto que a propriedade Tópicos corresponde ao tópico de suas tarefas de fluxo de trabalho.

### Serviço de sincronização de ativos DAM AEM {#cq-dam-asset-synchronization-service}

O `AssetSynchronizationService` O é usado para sincronizar ativos de repositórios montados (incluindo LiveLink, Documentum®, entre outros). Por padrão, essa sincronização faz uma verificação regular a cada 300 segundos (5 minutos), portanto, se você não usar repositórios montados, poderá desativar esse serviço.

A desativação do serviço é feita por [configuração do serviço OSGi](/help/sites-deploying/configuring-osgi.md) **Serviço de sincronização de ativos DAM CQ** para definir a variável **Período de sincronização** ( `scheduler.period`) a (no mínimo, um ano (definido em segundos).

### Várias instâncias do DAM {#multiple-dam-instances}

Implantar várias instâncias de DAM pode ajudar no desempenho quando, por exemplo:

* Você tem uma carga alta devido ao upload regular de muitos ativos para o ambiente do autor; aqui, uma instância separada do DAM pode ser dedicada à manutenção do autor.
* Você tem várias equipes em locais do mundo (por exemplo, EUA, Europa, Ásia).

Considerações adicionais são:

* Separação de &quot;trabalho em andamento&quot; no autor de &quot;final&quot; na publicação
* Separação de usuários internos do autor de visitantes/usuários externos na publicação (por exemplo, agentes, representantes de imprensa, clientes e estudantes).

## Práticas recomendadas para garantia de qualidade {#best-practices-for-quality-assurance}

O desempenho é de extrema importância para o seu ambiente de publicação. Portanto, você deve planejar e analisar cuidadosamente os testes de desempenho feitos para o ambiente de publicação ao implementar seu projeto.

Esta seção tem como objetivo fornecer uma visão geral padronizada dos problemas envolvidos na definição de um conceito de teste especificamente para testes de desempenho em seu *publicar* ambiente. Essas informações são de interesse principalmente para engenheiros de controle de qualidade, gerentes de projeto e administradores de sistema.

Abrange uma abordagem padronizada para testes de desempenho para uma aplicação AEM no *Publicar* ambiente. Este teste de desempenho envolve as cinco fases seguintes:

* [Verificação dos conhecimentos](#verification-of-knowledge)
* [Definição do escopo](#scope-definition)
* [Metodologias de teste](#test-methodologies)
* [Definição de metas de desempenho](#defining-the-performance-goals)
* [Otimização](#optimization)

O controle é um processo extra, abrangente - necessário, mas não limitado a testes.

### Verificação dos conhecimentos {#verification-of-knowledge}

Uma primeira etapa é documentar as informações básicas que você deve saber antes de iniciar os testes:

* A arquitetura do ambiente de teste
* Um mapa de aplicações que detalhe os elementos internos que necessitam de ensaio (isoladamente ou em combinação)

#### Arquitetura de teste {#test-architecture}

Documente a arquitetura do ambiente de teste que está sendo usado para seus testes de desempenho.

Você precisa de uma reprodução do ambiente de publicação de produção planejado, juntamente com o Dispatcher e o Balanceador de carga.

#### Mapa de aplicativos {#application-map}

Obtenha uma visão geral clara da qual você pode criar um mapa de todo o aplicativo (talvez você já tenha esse mapa dos testes no ambiente Autor).

Uma representação gráfica dos elementos internos do pedido pode dar uma visão geral dos requisitos de ensaio; com a codificação por cores, também pode servir de base para o relatório.

### Definição de escopo {#scope-definition}

Um aplicativo geralmente tem uma seleção de casos de uso. Alguns casos de uso são importantes, outros menos.

Para concentrar o escopo do teste de desempenho na publicação, o Adobe recomenda que você defina o seguinte:

* Casos de uso mais importantes da empresa
* Casos de uso técnico mais críticos

O número de casos de uso depende de você, mas deve se limitar a um número facilmente gerenciável (por exemplo, entre 5 e 10).

Depois que os principais casos de uso forem selecionados, os KPI (indicadores-chave de desempenho) e as ferramentas usadas para avaliá-los poderão ser definidos para cada caso. Exemplos de KPIs comuns incluem:

* Tempo de resposta de fim a fim
* Tempo de resposta do servlet
* Tempo de resposta para um único componente
* Tempo de resposta dos serviços
* Número de threads ociosos no conjunto de threads
* Número de conexões gratuitas
* Recursos do sistema, como CPU e acesso de E/S

### Metodologias de teste {#test-methodologies}

Esse conceito tem quatro cenários usados para definir e testar as metas de desempenho:

* Testes de componentes únicos
* Ensaios de componentes combinados
* *Ao vivo* cenário
* Cenários de erro

Baseado nos seguintes princípios:

#### Pontos de interrupção de componente {#component-breakpoints}

* Cada componente tem um ponto de interrupção específico quando relacionado ao desempenho. Ou seja, um componente pode mostrar que o bom desempenho até que um ponto específico seja atingido, após o que o desempenho diminui rapidamente.
* Para obter uma visão geral completa do aplicativo, primeiro verifique seus componentes para determinar quando o ponto de interrupção de cada um é atingido.
* Para encontrar o ponto de interrupção que você pode executar um teste de carga onde, durante um período de tempo, você aumenta o número de usuários para criar uma carga crescente. Ao monitorar essa carga e a resposta dos componentes, você encontra um comportamento de desempenho específico quando o ponto de quebra do componente é atingido. O ponto pode ser qualificado pelo número de transações simultâneas por segundo, juntamente com o número de usuários simultâneos (se o componente for sensível a esse KPI).
* Essas informações podem servir de referência para melhorias, indicar a eficiência das medidas usadas e ajudar a definir cenários de teste.

#### Transações {#transactions}

* O termo transação é usado para representar a solicitação de uma página da Web completa, incluindo a própria página e todas as chamadas subsequentes. Ou seja, a solicitação de página, qualquer chamada de AJAX, imagens e outros objetos **Solicitar Drill-Down**.
* Para analisar completamente cada solicitação, você pode representar cada elemento da pilha de chamadas e, em seguida, totalizar o tempo médio de processamento de cada solicitação.

### Definir as metas de desempenho {#defining-the-performance-goals}

Depois que o escopo e os KPIs relacionados são definidos, as metas de desempenho específicas são definidas. Esse processo envolve a concepção de cenários de teste, juntamente com valores de target.

Testar o desempenho em condições médias e de pico. Além disso, você precisa de testes de cenário do Google Live para garantir que possa atender a um interesse maior em seu site quando ele for disponibilizado pela primeira vez.

Qualquer experiência ou estatística que você tenha coletado de um site existente também pode ser útil para determinar metas futuras. Por exemplo, o tráfego principal de seu site ativo.

#### Testes de componente único {#single-component-tests}

Os componentes críticos devem ser ensaiados em condições médias e de pico.

Em ambos os casos, é possível definir o número esperado de transações por segundo quando um número predefinido de usuários estiver usando o sistema.

| Componente | Tipo de teste | Não. de usuários | Tx/s (Esperado) | Tx/s (Testado) | Descrição |
|---|---|---|---|---|---|
| Página inicial - Usuário único | Média | 1 | 1 |  |  |
|  | Pico | 1 | 3 |  |  |
| Página inicial 100 usuários | Média | 100 | 3 |  |  |
|  | Pico | 100 | 3 |  |

#### Testes de componentes combinados {#combined-component-tests}

Testar os componentes em combinação oferece uma reflexão mais próxima do comportamento dos aplicativos. Devem ser testadas novamente as condições médias e de pico.

| Cenário | Componente | Não. de usuários | Tx/s (Esperado) | Tx/s (Testado) | Descrição |
|---|---|---|---|---|---|
| Média mista | Página inicial | 10 | 1 |  |  |
|  | Pesquisar | 10 | 1 |  |  |
|  | Notícias | 10 | 2 |  |  |
|  | Eventos | 10 | 1 |  |  |
|  | Ativations | 10 | 3 |  | Simulação do comportamento do autor. |
| Pico misto | Página inicial | 100 | 5 |  |  |
|  | Pesquisar | 50 | 5 |  |  |
|  | Notícias | 100 | 10 |  |  |
|  | Eventos | 100 | 10 |  |  |
|  | Ativations | 20 | 20 |  | Simulação do comportamento do autor. |

#### Indo para testes em tempo real {#going-live-tests}

Durante os primeiros dias após o seu site ser disponibilizado, você pode esperar um nível maior de interesse. Esse cenário é ainda maior que os valores de pico que você está testando. O Adobe recomenda que você teste os cenários do Google Live para garantir que o sistema possa atender a essa situação.

| Cenário | Tipo de teste | Não. de usuários | Tx/s (Esperado) | Tx/s (Testado) | Descrição |
|---|---|---|---|---|---|
| Pico em tempo real | Página inicial | 200 | 20 |  |  |
|  | Pesquisar | 100 | 10 |  |  |
|  | Notícias | 200 | 20 |  |  |
|  | Eventos | 200 | 20 |  |  |
|  | Ativations | 20 | 20 |  | Simulação do comportamento do autor. |

#### Testes de cenário de erro {#error-scenario-tests}

Teste os cenários de erro para garantir que o sistema reaja corretamente e adequadamente. Não apenas na forma como o erro em si é tratado, mas no impacto que ele pode ter no desempenho. Por exemplo:

* O que acontece quando o usuário tenta inserir um termo de pesquisa inválido na caixa de pesquisa
* O que acontece quando o termo de pesquisa é tão geral que retorna um número excessivo de resultados

Ao criar esses testes, deve-se lembrar que nem todos os cenários ocorrem regularmente. No entanto, o seu impacto em todo o sistema é importante.

| Cenário de erro | Tipo de erro | Não. de usuários | Tx/s (Esperado) | Tx/s (Testado) | Descrição |
|---|---|---|---|---|---|
| Sobrecarga do componente de pesquisa | Pesquisar no curinga global (asterisco) | 10 | 1 |  | Apenas &amp;ast;&amp;ast;&amp;ast; são pesquisados. |
|  | Palavra de interrupção | 20 | 2 |  | Procurando uma palavra de parada. |
|  | Sequência de caracteres vazia | 10 | 1 |  | Procurando uma string vazia. |
|  | Caracteres especiais | 10 | 1 |  | Pesquisando caracteres especiais. |

#### Testes de resistência {#endurance-tests}

Certos problemas só são encontrados depois que o sistema está em execução por um período de tempo contínuo, horas ou dias. É utilizado um ensaio de resistência para testar uma carga média constante durante um período de tempo necessário. Qualquer degradação de desempenho pode ser analisada.

| Cenário | Tipo de teste | Não. de usuários | Tx/s (Esperado) | Tx/s (Testado) | Descrição |
|---|---|---|---|---|---|
| Ensaio de resistência (72 horas) | Página inicial | 10 | 1 |  |  |
|  | Pesquisar | 10 | 1 |  |  |
|  | Notícias | 20 | 2 |  |  |
|  | Eventos | 10 | 1 |  |  |
|  | Ativations | 1 | 3 |  | Simulação do comportamento do autor. |

### Otimização {#optimization}

Nos estágios posteriores de implementação, otimize o aplicativo para atender e maximizar as metas de desempenho.

Todas as otimizações feitas devem ser testadas para garantir que elas tenham:

* Não afetado pela funcionalidade
* Foi verificado com os testes de carga antes de ser liberado

Uma seleção de ferramentas está disponível para ajudá-lo com a geração de carga, monitoramento de desempenho e análise de resultados. Algumas dessas ferramentas incluem:

* [JMeter](https://jmeter.apache.org/)
* [Carregar Executador](https://www.microfocus.com/en-us/portfolio/performance-engineering/overview)
* [InfraRED](https://www.infraredsoftware.com/)
* [Perfil interativo Java™](https://jiprof.sourceforge.net/)

Após a otimização, teste novamente para confirmar o impacto.

### Relatório {#reporting}

Os relatórios em andamento mantêm todos informados sobre o status. Como mencionado anteriormente com codificação por cores, o mapa de arquitetura pode ser usado para esse status.

Após a conclusão de todos os ensaios, indicar:

* Quaisquer erros críticos encontrados
* Problemas não críticos que ainda necessitam de mais investigação
* Quaisquer suposições feitas durante os testes
* Eventuais recomendações decorrentes do ensaio

## Otimizar o desempenho ao usar o Dispatcher {#optimizing-performance-when-using-the-dispatcher}

O [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR) é a ferramenta de balanceamento de carga e/ou Adobe. Ao usar o Dispatcher, considere otimizar seu site para obter desempenho de cache.

>[!NOTE]
>
>As versões do Dispatcher são independentes do AEM, no entanto, a documentação do Dispatcher está incorporada na documentação do AEM. Sempre use a documentação do Dispatcher incorporada à documentação da versão mais recente do AEM.
>
>Você pode ter sido redirecionado para esta página se tiver seguido um link para a documentação do Dispatcher incorporada à documentação de uma versão anterior do AEM.

O Dispatcher oferece vários mecanismos integrados que você pode usar para otimizar o desempenho se o seu site aproveitar. Esta seção informa como projetar seu site para potencializar os benefícios do armazenamento em cache.

>[!NOTE]
>
>Pode ser útil ter em mente que o Dispatcher armazena o cache em um servidor da Web padrão. Conhecer essas informações significa que você pode armazenar em cache tudo o que pode ser armazenado como uma página e solicitar usando um URL. Além disso, não é possível armazenar outras coisas, como cookies, dados de sessão e dados de formulário.
>
>Em geral, várias estratégias de armazenamento em cache envolvem selecionar bons URLs e não depender desses dados adicionais.
>
>Com o Dispatcher versão 4.1.11, também é possível armazenar em cache os cabeçalhos de resposta, consulte [Armazenamento em cache de cabeçalhos de resposta HTTP](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache).

### Calculando a Taxa de Cache do Dispatcher {#calculating-the-dispatcher-cache-ratio}

A fórmula da taxa de cache estima a porcentagem de solicitações tratadas pelo cache do número total de solicitações que entram no sistema. Para calcular a taxa de cache, você precisa do seguinte:

* O número total de solicitações. Essas informações estão disponíveis no Apache `access.log`. Para obter mais detalhes, consulte a [documentação oficial do Apache](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

* O número de solicitações que a instância de publicação atendeu. Essas informações estão disponíveis na seção `request.log` da instância. Para obter mais detalhes, consulte [Interpretação do request.log](/help/sites-deploying/monitoring-and-maintaining.md#interpreting-the-request-log) e [Encontrar os arquivos de log](/help/sites-deploying/monitoring-and-maintaining.md#finding-the-log-files).

A fórmula para calcular a taxa de cache é:

* (O número total de solicitações **minus** o número de solicitações em Publicar) **dividido** pelo número total de solicitações.

Por exemplo, se o número total de solicitações for 129491 e o número de solicitações atendidas pela instância de publicação for 58959, a taxa de cache será: **(129491 - 58959)/129491= 54,5%**.

Se você não tiver um emparelhamento editor/dispatcher de um para um, adicione solicitações de todos os dispatchers e editores juntos para obter uma medição precisa. Consulte também [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md).

>[!NOTE]
>
>Para melhor desempenho, o Adobe recomenda uma taxa de cache de 90% a 95%.

#### Uso de codificação de página consistente {#using-consistent-page-encoding}

Com o Dispatcher versão 4.1.11, é possível armazenar em cache os cabeçalhos de resposta. Se você não estiver armazenando cabeçalhos de resposta em cache no Dispatcher, poderão ocorrer problemas se você armazenar informações de codificação de página no cabeçalho. Nessa situação, quando o Dispatcher fornece uma página do cache, a codificação padrão do servidor Web é usada para a página. Há duas maneiras de evitar esse problema:

* Se você usar apenas uma codificação, verifique se a codificação usada no servidor Web é igual à codificação padrão do site do AEM.
* Para definir a codificação, use um `<META>` na HTML `head` , como no exemplo a seguir:

```xml
        <META http-equiv="Content-Type" content="text/html; charset=EUC-JP">
```

#### Evitar parâmetros de URL {#avoid-url-parameters}

Se possível, evite parâmetros de URL para páginas que você deseja armazenar em cache. Por exemplo, se você tiver uma galeria de imagens, o URL a seguir nunca será armazenado em cache (a menos que o Dispatcher esteja [configurado adequadamente](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache)):

```xml
www.myCompany.com/pictures/gallery.html?event=christmas&amp;page=1
```

No entanto, você pode colocar esses parâmetros no URL da página, da seguinte maneira:

```xml
www.myCompany.com/pictures/gallery.christmas.1.html
```

>[!NOTE]
>
>Esse URL chama a mesma página e o mesmo modelo de `gallery.html`. Na definição do modelo, é possível especificar qual script renderiza a página ou usar o mesmo script para todas as páginas.

#### Personalizar por URL {#customize-by-url}

Se você permitir que os usuários alterem o tamanho da fonte (ou qualquer outra personalização de layout), verifique se as diferentes personalizações são refletidas no URL.

Por exemplo, os cookies não são armazenados em cache. Dessa forma, se você armazenar o tamanho da fonte em um cookie (ou mecanismo semelhante), o tamanho da fonte não será preservado para a página em cache. Como resultado, o Dispatcher retorna documentos de qualquer tamanho de fonte aleatoriamente.

Incluir o tamanho da fonte no URL como um seletor evita esse problema:

```xml
www.myCompany.com/news/main.large.html
```

>[!NOTE]
>
>Para a maioria dos aspectos de layout, também é possível usar folhas de estilos, scripts do lado do cliente, ou ambos. Estes instrumentos funcionam bem com o armazenamento em cache.
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

Por exemplo, você pode armazenar o título da página `myPage.html` no `file myPage.title.gif`. Esse arquivo será automaticamente excluído se a página for atualizada, de modo que qualquer alteração no título da página será refletida automaticamente no cache.

>[!NOTE]
>
>O arquivo de imagem não existe necessariamente fisicamente na instância do AEM. Você pode usar um script que cria dinamicamente o arquivo de imagem. O Dispatcher armazena o arquivo no servidor Web.

#### Invalidar arquivos de imagem usados para navegação {#invalidating-image-files-used-for-navigation}

Se você usar imagens para as entradas de navegação, o método é basicamente o mesmo que com títulos, mas ligeiramente mais complexo. Armazene todas as imagens de navegação com as páginas de destino. Se você usar duas imagens para o normal e o ativo, poderá usar os seguintes scripts:

* Um script que exibe a página, como de costume.
* Um script que processa solicitações &quot;.normal&quot; e retorna a imagem normal.
* Um script que processa solicitações &quot;.active&quot; e retorna a imagem ativada.

É importante criar essas imagens com o mesmo identificador de nome da página, para garantir que uma atualização de conteúdo exclua essas imagens e a página.

Para páginas que não são modificadas, as imagens permanecem no cache, embora as próprias páginas sejam invalidadas automaticamente.

#### Personalização {#personalization}

É recomendável limitar a personalização ao local necessário. Para ilustrar o motivo:

* Se você usar uma página inicial personalizável livremente, essa página deverá ser composta sempre que um usuário a solicitar.
* Se, por outro lado, você oferecer uma escolha de dez páginas iniciais diferentes, poderá armazenar em cache cada uma delas, melhorando o desempenho.

>[!TIP]
>Para obter mais detalhes sobre como configurar o cache do Dispatcher, consulte o [AEM Tutorial de cache do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-learn/dispatcher-tutorial/overview.html) e a sua seção sobre [Armazenamento em cache de conteúdo protegido.](https://experienceleague.adobe.com/docs/experience-manager-learn/dispatcher-tutorial/chapter-1.html#dispatcher-tips-and-tricks)

Se você personalizar cada página colocando o nome do usuário na barra de título (por exemplo), isso terá um impacto no desempenho.

>[!TIP]
>Para armazenar conteúdo protegido em cache, consulte [Armazenamento em cache de conteúdo protegido](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=pt-BR) no guia do Dispatcher.

Com relação à mistura de conteúdo restrito e público em uma página, considere uma estratégia que usa inclusões do lado do servidor no Dispatcher ou inclusões do lado do cliente por meio do Ajax no navegador.

>[!TIP]
>
>Para saber como lidar com conteúdo misto público e restrito, consulte [Configure Sling Dynamic Include.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-sling-dynamic-include.html)

#### Conexões adesivas {#sticky-connections}

As [conexões adesivas](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=en#the-benefits-of-load-balancing) garantem que os documentos de um usuário sejam todos compostos no mesmo servidor. Se um usuário sair dessa pasta e posteriormente retornar a ela, a conexão ainda permanecerá. Para manter todos os documentos que exigem conexões aderentes para o site, defina uma pasta. Tente não manter outros documentos nela. Esse cenário afeta o balanceamento de carga se você usar páginas personalizadas e dados de sessão.

#### Tipos MIME {#mime-types}

Há duas maneiras pelas quais um navegador pode determinar o tipo de arquivo:

1. Por sua extensão (por exemplo, `.html`, `.gif`e `.jpg`).
1. Pelo tipo MIME que o servidor envia com o arquivo.

Para a maioria dos arquivos, o tipo MIME está implícito na extensão de arquivo. Ou seja,

1. Por sua extensão (por exemplo, `.html`, `.gif`e `.jpg`).
1. Pelo tipo MIME que o servidor envia com o arquivo.

Se o nome do arquivo não tiver extensão, ele será exibido como texto sem formatação.

Com o Dispatcher versão 4.1.11, é possível armazenar em cache os cabeçalhos de resposta. Se você não armazenar em cache os cabeçalhos de resposta no Dispatcher, o tipo MIME fará parte do cabeçalho HTTP. Dessa forma, se o aplicativo de AEM retornar arquivos que não têm um arquivo reconhecido terminado e depender do tipo MIME, esses arquivos poderão ser exibidos incorretamente.

Para garantir que os arquivos sejam armazenados em cache corretamente, siga estas diretrizes:

* Certifique-se de que os arquivos sempre tenham a extensão adequada.
* Evite scripts de servidor de arquivos genéricos, que tenham URLs como `download.jsp?file=2214`. Para usar URLs contendo a especificação do arquivo, regrave o script. No exemplo anterior, essa reescrita é `download.2214.pdf`.

## Desempenho do backup {#backup-performance}

Esta seção apresenta uma série de benchmarks usados para avaliar o desempenho de backups AEM e os efeitos da atividade de backup no desempenho do aplicativo. AEM backups apresentam uma carga significativa no sistema enquanto ele é executado, e o Adobe mede esse impacto e os efeitos das configurações de atraso de backup que tentam modular esses efeitos. O objetivo é oferecer alguns dados de referência sobre o desempenho esperado dos backups em configurações realistas e quantidades de dados de produção, além de fornecer orientação sobre como estimar os tempos de backup para sistemas planejados.

### Ambiente de referência {#reference-environment}

#### Sistema físico {#physical-system}

Os resultados relatados neste documento foram obtidos a partir de benchmarks executados em um ambiente de referência com a seguinte configuração: Essa configuração é semelhante a um ambiente de produção típico em um data center:

* HP ProLiant DL380 G6, 8 CPUs x 2,533 GHz
* SCSI serial conectado 300 GB, 10.000 RPM
* Controlador RAID de hardware; oito unidades em um storage RAID0+5
* CPU de imagem VMware x 2 Intel Xeon® E5540 a 2,53 GHz
* Red Hat® Linux® 2.6.18-194.el5; Java™ 1.6.0_29
* Instância de autor único

O subsistema de disco desse servidor é rápido, representativo de uma configuração RAID de alto desempenho que pode ser usada em um servidor de produção. O desempenho do backup pode ser sensível ao desempenho do disco e os resultados neste ambiente refletem o desempenho em uma configuração RAID rápida. A imagem VMWare é configurada para ter um único grande volume de disco que reside fisicamente no armazenamento de disco local, na matriz RAID.

A configuração de AEM coloca o repositório e o armazenamento de dados no mesmo volume lógico, juntamente com o sistema operacional e o software AEM. O diretório de destino para backups também reside neste sistema de arquivos lógico.

#### Volumes de dados {#data-volumes}

A tabela a seguir ilustra o tamanho dos volumes de dados usados nos benchmarks de backup. O conteúdo da linha de base inicial é instalado pela primeira vez, e quantidades conhecidas de dados adicionais são adicionadas para aumentar o tamanho do conteúdo do backup. Os backups são criados em incrementos específicos para representar um grande aumento no conteúdo e no que pode ser produzido em um dia. A distribuição de conteúdo (páginas, imagens, tags) é basicamente baseada na composição realista do ativo de produção. Páginas, imagens e tags são limitadas a 800 páginas filhas. Cada página inclui componentes de título, Flash, texto/imagem, vídeo, apresentação de slides, formulário, tabela, nuvem e carrossel. As imagens são carregadas de um pool de 400 arquivos exclusivos, de 37 KB a 594 KB.

| Conteúdo | Nós | Páginas | Imagens | Tags |
|---|---|---|---|---|
| Instalação base | 69 610 | 562 | 256 | 237 |
| Conteúdo pequeno para backup incremental |  | +100 | +2 | +2 |
| Conteúdo grande para backup completo |  | +10 000 | +100 | +100 |

O referencial de backup é repetido com os conjuntos de conteúdo adicionais adicionados a cada repetição.

#### Cenários de referência {#benchmark-scenarios}

Os benchmarks de backup abrangem dois cenários principais: backups quando o sistema está sob carga significativa de aplicativos e backups quando o sistema está ocioso. Embora a recomendação geral seja que os backups sejam executados quando AEM estiver o mais ocioso possível, há situações em que é necessário que o backup seja executado quando o sistema estiver sob carregamento.

* **Estado ocioso** - Os backups são executados sem nenhuma outra atividade no AEM.
* **Sob Carregamento** - Os backups são executados enquanto o sistema está sob 80% de carga de processos online. O atraso do backup variou para ver o impacto na carga.

Os tempos de backup e o tamanho do backup resultante são obtidos dos registros do servidor de AEM. Normalmente, é recomendável que os backups sejam programados para horários off-times quando AEM estiver inativo, como no meio da noite. Esse cenário é representativo da abordagem recomendada.

O carregamento consiste em páginas criadas, páginas excluídas, travessias e consultas com a maior carga proveniente de passagens e consultas de página. Adicionar e remover muitas páginas continuamente aumenta o tamanho do espaço de trabalho e impede que as cópias de segurança sejam concluídas. A distribuição do carregamento que o script usa é 75% de traversais de página, 24% de consultas e 1% de criações de página (nível único sem subpáginas aninhadas). O pico médio de transações por segundo em um sistema ocioso é obtido com quatro threads simultâneos, que são usados ao testar backups sob carga.

O impacto da carga no desempenho do backup pode ser estimado pela diferença entre o desempenho com e sem essa carga de aplicativo. O impacto do backup na taxa de transferência do aplicativo é encontrado comparando a taxa de transferência de cenário em transações por hora com e sem um backup simultâneo em andamento e com backups operando com diferentes configurações de &quot;atraso de backup&quot;.

* **Configuração de atraso** - Para vários cenários, a configuração de atraso de backup também foi variada, usando valores de 10 milissegundos (padrão), 1 milissegundos e 0 milissegundos, para explorar como essa configuração afetou o desempenho dos backups.
* **Tipo de backup** - Todos os backups eram backups externos do repositório feitos em um diretório de backup sem criar um zip, exceto em um caso para comparação, onde o comando tar era usado diretamente. Como os backups incrementais não podem ser criados em um arquivo zip ou quando o backup completo anterior é um arquivo zip, o método de diretório de backup é o mais usado em situações de produção.

### Resumo dos resultados {#summary-of-results}

#### Tempo de backup e throughput {#backup-time-and-throughput}

O principal resultado desses benchmarks é mostrar como os tempos de backup variam em função do tipo de backup e da quantidade geral de dados. O gráfico a seguir mostra o tempo de backup obtido usando a configuração de backup padrão, como uma função do número total de páginas.

![chlimage_1-81](assets/chlimage_1-81.png)

Os tempos de backup em uma instância inativa são bastante consistentes, com uma média de 0,608 MB por segundo, independentemente dos backups completos ou incrementais (consulte o gráfico abaixo). O tempo de backup é simplesmente uma função da quantidade de dados que estão sendo copiados em backup. O tempo para concluir um backup completo aumenta claramente com o número total de páginas. O tempo para concluir um backup incremental também aumenta com o número total de páginas, mas a uma taxa muito menor. O tempo necessário para concluir o backup incremental é muito menor devido à quantidade relativamente pequena de dados que estão sendo copiados em backup.

O tamanho do backup produzido é o principal determinante do tempo necessário para concluir um backup. O gráfico a seguir mostra o tempo gasto em função do tamanho final do backup.

![chlimage_1-82](assets/chlimage_1-82.png)

Este gráfico ilustra que tanto os backups incrementais como completos seguem um padrão de tamanho e tempo simples que o Adobe pode medir como throughput. Os tempos de backup em uma instância ociosa são bastante consistentes, com uma média de 0,61 MB por segundo, independentemente dos backups completos ou incrementais no ambiente de benchmark.

#### Atraso de backup {#backup-delay}

O parâmetro de atraso de backup é fornecido para limitar até que ponto os backups podem interferir nas cargas de trabalho de produção. O parâmetro especifica um tempo de espera em milissegundos, que é intercalado na operação de backup com base em arquivo por arquivo. O efeito geral depende em parte do tamanho dos arquivos afetados. Medir o desempenho do backup em MB/s fornece uma maneira razoável de comparar os efeitos do atraso no backup.

* A execução de um backup simultaneamente com a carga regular do aplicativo tem um impacto negativo na taxa de transferência da carga regular.
* O impacto pode ser leve (até 5%) ou significativo, causando até 75% de queda na taxa de transferência. Provavelmente depende mais do aplicativo.
* O backup não é uma carga pesada na CPU e, portanto, as cargas de trabalho de produção que exigem muita CPU seriam menos afetadas pelo backup do que as que exigem muito E/S.

![chlimage_1-83](assets/chlimage_1-83.png)

Para comparar, a taxa de transferência obtida usando um backup do sistema de arquivos (&#39;tar&#39;) para fazer backup dos mesmos arquivos do repositório. O desempenho do tar é comparável, mas ligeiramente maior que o backup com atraso definido como zero. A configuração de até mesmo um pequeno atraso reduz bastante a taxa de transferência do backup e o atraso padrão de 10 milissegundos resulta em uma taxa de transferência muito reduzida. Em situações em que os backups podem ser programados quando o uso geral do aplicativo é baixo ou o aplicativo pode ficar inativo, reduza o atraso abaixo do valor padrão para permitir que o backup continue mais rapidamente.

O impacto real do throughput do aplicativo de um backup contínuo depende dos detalhes do aplicativo e da infraestrutura. A escolha do valor de atraso deve ser feita por análise empírica do aplicativo, mas deve ser escolhida o mais pequeno possível, para que os backups possam ser concluídos o mais rápido possível. Como há apenas uma correlação fraca entre a escolha do valor de atraso e o impacto na taxa de transferência do aplicativo, a escolha do atraso deve favorecer tempos de backup gerais mais curtos para minimizar o impacto geral dos backups. Um backup que leva oito horas para ser concluído, mas afeta a taxa de transferência em -20% provavelmente terá um impacto geral maior do que um, o que leva duas horas para ser concluído, mas afeta a taxa de transferência em -30%.

### Referências {#references}

* [Administração - Fazer backup e restaurar](/help/sites-administering/backup-and-restore.md)
* [Gerenciamento - capacidade e volume](/help/managing/best-practices-further-reference.md#capacity-and-volume)
