---
title: Práticas recomendadas para testes de desempenho
description: Saiba mais sobre as estratégias e metodologias gerais usadas para testes de desempenho e algumas das ferramentas disponíveis para ajudar no processo.
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
source-git-commit: 18f843ed3ffb719d168b67826baaffd926ffd2dd
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 1%

---

# Práticas recomendadas para testes de desempenho{#best-practices-for-performance-testing}

## Introdução {#introduction}

O teste de desempenho é uma parte importante de qualquer implantação do AEM. Dependendo dos requisitos do cliente, o teste de desempenho pode ser executado nas instâncias de publicação, instâncias de autor ou ambas.

Esta documentação descreve as estratégias e metodologias gerais de execução de testes de desempenho e algumas das ferramentas disponibilizadas pelo Adobe para ajudar no processo. Por fim, leia uma análise das ferramentas disponíveis no AEM 6 para auxiliar no ajuste do desempenho, tanto da perspectiva da análise de código quanto da configuração do sistema.

### Simulação da realidade {#simulating-reality}

Ao fazer testes de desempenho, certifique-se de imitar um ambiente de produção o mais próximo possível. Embora essa tarefa possa, muitas vezes, ser difícil, é imperativo garantir a precisão desses testes. Ao trabalhar na criação de testes de desempenho, é importante levar em consideração os seguintes pontos:

* Conteúdo semelhante à produção

Muitas medidas de desempenho no AEM, como o tempo de resposta da consulta, podem ser afetadas pelo tamanho do conteúdo no sistema. É importante garantir que o ambiente de teste tenha uma cópia dos dados de produção o mais próxima possível.

* Código de produção

A versão do AEM e os hotfixes implantados na produção devem ser os mesmos no ambiente de teste. Também é importante testar a versão do código implantada na produção.

* Configuração de rede e hardware semelhantes a produção

Os testes não têm sentido sem um ambiente que se assemelhe o mais possível à produção. Idealmente, as especificações de hardware, as interfaces de rede, os balanceadores de carga e a CDN devem ser idênticas à produção no ambiente de teste.

* Carga de produção

Muitos problemas de desempenho não são observados até que o sistema esteja sobrecarregado. Bons testes de desempenho devem simular a carga que os sistemas de produção estão sob no pico.

### Definição de Metas {#setting-goals}

Antes de começar o teste de desempenho, é necessário definir requisitos não funcionais para especificar a carga e os tempos de resposta. Se estiver migrando de um sistema existente, verifique se os tempos de resposta são semelhantes aos valores atuais de produção. Para carga, é melhor pegar o pico de carga atual e dobrá-lo. Isso garante que o site possa continuar a ter um bom desempenho à medida que crescer.

### Ferramentas {#tools}

Existem muitas ferramentas de teste de desempenho disponíveis comercialmente no mercado. Ao executar uma ferramenta de geração de carga, é importante garantir que os computadores que estão realizando os testes tenham largura de banda de rede suficiente. Caso contrário, uma vez que a máquina de teste atinja os limites de sua conexão, nenhuma carga adicional será gerada no ambiente em teste.

#### Ferramentas de teste {#testing-tools}

* Adobe **Dia difícil** A ferramenta pode ser usada para gerar carga em instâncias AEM e coletar dados de desempenho. A equipe de engenharia do Adobe AEM usa a ferramenta para fazer o teste de carga do próprio produto AEM. Os scripts executados no Dia Difícil são configurados por meio de arquivos de propriedade e arquivos XML JMX. Para obter mais informações, consulte [Documentação do Dia Difícil](/help/sites-developing/tough-day.md).

* O AEM fornece ferramentas prontas para uso para ver rapidamente consultas, solicitações e mensagens de erro problemáticas. Para obter mais informações, consulte [Ferramentas de diagnóstico](/help/sites-administering/operations-dashboard.md#diagnosis-tools) seção da documentação do Painel de operações.
* O Apache fornece um produto chamado **JMeter** que pode ser usado para testes de desempenho e carga e comportamento funcional. É um software de código aberto e gratuito, mas tem um conjunto de recursos menor do que os produtos empresariais e uma curva de aprendizado mais acentuada. O JMeter pode ser encontrado no site do Apache em [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Load Runner** O é um produto de teste de carga de nível empresarial. Uma versão de avaliação gratuita está disponível. Mais informações podem ser encontradas em [https://www.microfocus.com/en-us/portfolio/performance-engineering/overview](https://www.microfocus.com/en-us/portfolio/performance-engineering/overview)

* Ferramentas de teste de carregamento de site como [Vercara](https://vercara.com/website-performance-management) também pode ser usado.
* Ao testar sites móveis ou responsivos, um conjunto separado de ferramentas deve ser usado. Elas funcionam acelerando a largura de banda da rede, simulando conexões móveis mais lentas, como 3G ou EDGE. Entre as ferramentas mais usadas estão as seguintes:

   * **[Condicionador de Link de Rede](https://nshipster.com/network-link-conditioner/)** - fornece uma interface fácil de usar e funciona em um nível relativamente baixo na pilha de rede. Ele inclui versões para OS X e iOS;
   * [**Charles**](https://www.charlesproxy.com/) - um aplicativo proxy de depuração da web que, além de vários outros usos, fornece limitação de rede. São fornecidas versões para Windows, OS X e Linux®.

#### Ferramentas de otimização {#optimization-tools}

**Monitoramento**

A variável [Monitorando o desempenho](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) A documentação do é um bom recurso para ferramentas e métodos que podem ser usados para diagnosticar problemas e identificar áreas para ajuste.

**Modo de desenvolvedor na interface para toque**

Um dos novos recursos na interface de toque do AEM 6 é o Modo de desenvolvedor. Da mesma forma que os autores podem alternar entre os modos de edição e pré-visualização, os desenvolvedores podem alternar para o modo de desenvolvedor na interface do autor. Isso permite que você veja o tempo de renderização de cada um dos componentes na página e veja os rastreamentos de pilha de quaisquer erros. Para obter mais informações sobre o modo de desenvolvedor, consulte esta [Apresentação do CQ Gems](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-developer-mode.html?lang=en).

**Usar o rlog.jar para ler os logs de solicitação**

Para obter uma análise mais abrangente dos registros de solicitações em um sistema AEM, `rlog.jar` pode ser usado para pesquisar e classificar a variável `request.log` arquivos gerados pelo AEM. Esse arquivo jar está incluído com uma instalação AEM no `/crx-quickstart/opt/helpers` pasta. Para obter mais informações sobre a ferramenta rlog e o log de solicitação em geral, consulte [Monitoramento e manutenção](/help/sites-deploying/monitoring-and-maintaining.md) documentação.

**A Ferramenta Explicar Consulta**

A variável [Ferramenta Explicar consulta](/help/sites-administering/operations-dashboard.md#explain-query) no ACS AEM, as Ferramentas podem ser usadas para exibir os índices usados ao executar um query. Essa ferramenta é útil ao otimizar consultas de execução lenta.

**Ferramentas PageSpeed**

As ferramentas do Google PageSpeed oferecem análise do site para adesão às práticas recomendadas para o desempenho da página e um plug-in que pode ser instalado junto com o Dispatcher em uma instância do Apache para otimizações adicionais.
Consulte a [PageSpeed Tools Site](https://developers.google.com/speed).

## Ambiente de criação {#author-environment}

### Realização de testes {#performing-tests}

Para realizar testes de desempenho no ambiente de criação, é necessário simular a experiência dos autores de produção. Ou seja, as instalações do autor devem conter todos os componentes, pacotes OSGi, personalização da interface, índices personalizados e quaisquer outras adições que você tenha em vigor para as instâncias do autor de produção.

Há muitas estruturas de automação disponíveis que foram projetadas para testes de desempenho e carga. Os scripts personalizados podem ser registrados nessas ferramentas e reproduzidos para simular um número máximo de autores executando atividades semelhantes de criação e ativação de conteúdo simultaneamente. É recomendável usar a ferramenta Dia difícil para simular atividades como carregar milhares de ativos ou ativar um grande número de páginas.

Para os tipos de ambientes que têm requisitos de carregamento pesado de ativos ou criação de página, é fundamental usar ferramentas como o Dia Difícil. Isso garante que o ambiente opere com eficiência no pico de carga. [WebDAV](/help/sites-administering/webdav-access.md) O é uma ferramenta que não requer script e também pode ser usada para carregar grandes quantidades de ativos.

#### Etapas específicas do MongoDB {#mongodb-specific-steps}

Em sistemas com back-ends MongoDB, AEM fornece vários [JMX](/help/sites-administering/jmx-console.md) MBeans que devem ser monitorados ao executar testes de carga ou desempenho:

* A variável **Estatísticas consolidadas de cache** MBean. Ele pode ser acessado diretamente em:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

Para o cache chamado **Document-Diff**, a taxa de ocorrência deve estar acima de `.90`. Se a taxa de ocorrência ficar abaixo de 90%, é provável que você precise editar o `DocumentNodeStoreService` configuração. O suporte a produtos Adobe pode recomendar configurações ideais para seu ambiente.

* A variável **Estatísticas do repositório Oak** Mbean. Ele pode ser acessado diretamente em:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

A variável **ComprimentoMáxFilaObservação** A seção mostra o número de eventos na fila de observação do Oak nas últimas horas, minutos, segundos e semanas. Encontre o maior número de eventos na seção &quot;por hora&quot;. Compare esse número com o `oak.observation.queue-length` configuração. Se o número mais alto mostrado para a fila de observação exceder o `queue-length` configuração:

1. Crie um arquivo com o nome: `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` contendo o parâmetro `oak.observation.queue‐length=50000`
1. Coloque-o na pasta /crx-quickstart/install.

>[!NOTE]
>Consulte [AEM 6.x | Dicas para ajustar o desempenho](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=pt-BR)

A configuração padrão é 10.000, mas a maioria das implantações deve elevá-la para 20.000 ou 50.000.

## Ambiente de publicação {#publish-environment}

### Realização de testes {#performing-tests-1}

A parte mais importante de uma implantação que deve estar sujeita a testes de carga é o ambiente de publicação ou Dispatcher voltado para o usuário final.

Ferramentas de teste automatizado de terceiros podem ser usadas para testar o desempenho do site. Essas ferramentas permitem registrar as etapas que os usuários passam no site e executar muitas dessas sessões ao mesmo tempo para simular a carga típica de um site de produção.

A maioria dos sites de produção tem otimizações em vigor, como o armazenamento em cache do Dispatcher e uma rede de entrega de conteúdo em vigor. Ao testar, verifique se essas otimizações também estão disponíveis para o ambiente de teste. Além de monitorar os tempos de resposta para os usuários finais, monitore as métricas do sistema nos servidores de publicação e nos dispatchers para garantir que o sistema não seja restringido pelos recursos de hardware.

Em um sistema que não requer um alto nível de personalização, o Dispatcher deve armazenar em cache a maioria das solicitações. Como resultado, a carga na instância de publicação deve permanecer relativamente plana. Se um alto nível de personalização for necessário, é recomendável usar tecnologias como iFrames ou solicitações de AJAX para o conteúdo personalizado a fim de permitir o máximo possível de armazenamento em cache do Dispatcher.

Para testes básicos, o Apache Bench pode ser usado para medir os tempos de resposta do servidor da Web e ajudar a criar carga para medir coisas como vazamentos de memória. Veja o exemplo na [Documentação de monitoramento](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## Solução de problemas de desempenho {#troubleshooting-performance-issues}

Após a execução dos testes de desempenho na instância do autor, todos os problemas devem ser investigados, diagnosticados e abordados. Você pode usar várias ferramentas e técnicas ao executar análises e resolver problemas:

* Você pode inspecionar o [Log de desempenho da solicitação](/help/sites-administering/operations-dashboard.md#request-performance) no Painel de operações. Essa ferramenta pode ser usada para identificar solicitações de página lentas
* Analise consultas de execução lenta com o [Ferramenta Desempenho da consulta](/help/sites-administering/operations-dashboard.md#query-performance)

* Verifique se há erros ou avisos no log de erros. Para obter mais informações, consulte [Logs](/help/sites-deploying/configure-logging.md).
* Monitore recursos de hardware do sistema, como utilização de memória e CPU, E/S de disco ou E/S de rede. Esses recursos geralmente são as causas dos gargalos de desempenho.
* Otimize a arquitetura das páginas e como elas são endereçadas para minimizar o uso de parâmetros de URL para permitir o máximo de armazenamento em cache possível.
* Siga as [Otimização do desempenho](/help/sites-deploying/configuring-performance.md) e [Dicas para melhorar o desempenho](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=pt-BR) documentação.

* Se houver problemas com a edição de determinadas páginas ou componentes em instâncias de autor, use o Modo de desenvolvedor da interface para toque para inspecionar a página em questão. Isso fornece um detalhamento de cada área de conteúdo na página e seu tempo de carregamento.
* Reduza todos os JS e CSS no site. Veja isto [publicação do blog](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* Elimine o CSS e o JS incorporados dos componentes. Eles devem ser incluídos e minificados com as bibliotecas do lado do cliente para minimizar o número de solicitações necessárias para renderizar a página.
* Para inspecionar as solicitações do servidor e ver quais estão demorando mais, use ferramentas de navegador, como a guia Rede do Chrome.

Depois que as áreas problemáticas são identificadas, o código do aplicativo pode ser inspecionado quanto a otimizações de desempenho. Qualquer recurso de AEM pronto para uso que não esteja funcionando corretamente pode ser tratado com Suporte para Adobe.
