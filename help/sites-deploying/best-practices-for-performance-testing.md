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
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 0%

---

# Práticas recomendadas para testes de desempenho{#best-practices-for-performance-testing}

## Introdução {#introduction}

O teste de desempenho é uma parte importante de qualquer implantação de AEM. Dependendo dos requisitos do cliente, o teste de desempenho pode ser realizado nas instâncias de publicação, nas instâncias do autor ou em ambos.

Esta documentação descreve as estratégias e metodologias gerais de realização de testes de desempenho e algumas das ferramentas disponibilizadas pelo Adobe para ajudar no processo. Por fim, leia uma análise das ferramentas disponíveis no AEM 6 para auxiliar no ajuste do desempenho, tanto em uma análise de código quanto em uma perspectiva de configuração do sistema.

### Simular realidade {#simulating-reality}

Ao fazer testes de desempenho, imite um ambiente de produção o mais próximo possível. Embora essa tarefa possa ser muitas vezes difícil, é imperativo garantir a precisão desses testes. Ao trabalhar na criação de testes de desempenho, é importante ter os seguintes pontos em consideração:

* Conteúdo semelhante à produção

Muitas medidas de desempenho no AEM, como o tempo de resposta da consulta, podem ser afetadas pelo tamanho do conteúdo no sistema. É importante garantir que o ambiente de teste tenha o mais próximo possível de uma cópia dos dados de produção.

* Código de produção

A versão AEM e os hotfixes implantados em produção devem ser os mesmos no ambiente de teste. Também é importante testar a versão do código implantada na produção.

* Configuração de hardware e rede semelhante à produção

Os testes são irrelevantes sem um ambiente que se assemelhe ao da produção. Idealmente, as especificações de hardware, as interfaces de rede, os balanceadores de carga e o CDN devem ser idênticos à produção no ambiente de teste.

* Carga de produção

Muitos problemas de desempenho não são vistos até que o sistema esteja sob carga pesada. Os bons ensaios de desempenho devem simular a carga em que os sistemas de produção se encontram no seu pico.

### Definir metas {#setting-goals}

Antes de iniciar os ensaios de desempenho, é necessário definir requisitos não funcionais para especificar os tempos de carga e resposta. Se você estiver migrando de um sistema existente, verifique se os tempos de resposta são semelhantes aos valores de produção atuais. Para carga, é melhor pegar a carga de pico atual e duplicá-la. Isso garante que o site possa continuar a ter um bom desempenho enquanto cresce.

### Ferramentas {#tools}

Há muitas ferramentas de teste de desempenho disponíveis comercialmente no mercado. Ao executar uma ferramenta de geração de carga, é importante garantir que os computadores que estão executando os testes tenham largura de banda de rede suficiente. Caso contrário, quando a máquina de teste atingir os limites de sua conexão, nenhuma carga adicional será gerada no ambiente em teste.

#### Ferramentas de teste {#testing-tools}

* Adobe **Dia difícil** A ferramenta pode ser usada para gerar carga em instâncias AEM e coletar dados de desempenho. A equipe de engenharia do Adobe usa o teste de carga do próprio produto. Os scripts executados em Tough Day são configurados por meio de arquivos de propriedade e arquivos XML JMX. Para obter mais informações, consulte o [Documentação do Dia difícil](/help/sites-developing/tough-day.md).

* AEM fornece ferramentas prontas para uso para ver rapidamente consultas problemáticas, solicitações e mensagens de erro. Para obter mais informações, consulte o [Ferramentas de diagnóstico](/help/sites-administering/operations-dashboard.md#diagnosis-tools) seção da documentação do Painel de operações.
* O Apache fornece um produto chamado **JMeter** que podem ser usados para testes de desempenho e carga e comportamento funcional. Ele é um software de código aberto e gratuito, mas tem um conjunto de recursos menor do que os produtos corporativos e uma curva de aprendizado mais acentuada. O JMeter pode ser encontrado no site do Apache em [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Carregar Executador** é um produto de teste de carga de nível empresarial. Uma versão de avaliação gratuita está disponível. Mais informações podem ser encontradas em [https://www.microfocus.com/en-us/portfolio/performance-engineering/overview](https://www.microfocus.com/en-us/portfolio/performance-engineering/overview)

* Ferramentas de teste de carregamento de site como [Neustar](https://neustarsecurityservices.com/web-performance-management) também pode ser usado.
* Ao testar sites móveis ou responsivos, um conjunto separado de ferramentas deve ser usado. Eles funcionam diminuindo a largura de banda da rede, simulando conexões móveis mais lentas, como 3G ou EDGE. Entre as ferramentas mais utilizadas estão:

   * **[Condicionador de links de rede](https://nshipster.com/network-link-conditioner/)** - fornece uma interface de usuário fácil de usar e funciona em um nível relativamente baixo na pilha de rede. Ele inclui versões para OS X e iOS;
   * [**Charles**](https://www.charlesproxy.com/) - um aplicativo proxy de depuração da Web que, além de várias outras utilizações, fornece controle de rede. As versões são fornecidas para Windows, OS X e Linux®.

#### Ferramentas de otimização {#optimization-tools}

**Monitoramento**

O [Monitorar desempenho](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) a documentação é um bom recurso para ferramentas e métodos que podem ser usados para diagnosticar problemas e identificar áreas para ajuste.

**Modo de desenvolvedor na interface do usuário de toque**

Um dos novos recursos na interface de toque do AEM 6 é o Modo de desenvolvedor. Assim como os autores podem alternar entre os modos de edição e visualização, os desenvolvedores podem alternar para o modo desenvolvedor na interface do usuário do autor. Isso permite ver o tempo de renderização de cada um dos componentes na página e ver os rastreamentos de pilha de qualquer erro. Para obter mais informações sobre o modo de desenvolvedor, consulte este [Apresentação de Gems CQ](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-developer-mode.html?lang=en).

**Usar o rlog.jar para ler os logs de solicitação**

Para obter uma análise mais abrangente dos logs de solicitação em um sistema de AEM, `rlog.jar` pode ser usado para pesquisar e classificar o `request.log` arquivos que AEM gerados. Este arquivo jar é incluído com uma instalação AEM no `/crx-quickstart/opt/helpers` pasta. Para obter mais informações sobre a ferramenta de log e o log de solicitações em geral, consulte o [Monitoramento e manutenção](/help/sites-deploying/monitoring-and-maintaining.md) documentação.

**A ferramenta Explain Query**

O [Explique a ferramenta Query](/help/sites-administering/operations-dashboard.md#explain-query) em ACS AEM Tools podem ser usados para exibir os índices usados ao executar um query. Essa ferramenta é útil para otimizar consultas de execução lenta.

**Ferramentas PageSpeed**

As ferramentas Google PageSpeed oferecem análise do site para seguir as práticas recomendadas para o desempenho da página e um plug-in que pode ser instalado junto com o Dispatcher em uma instância do Apache para obter otimizações adicionais.
Consulte a [Site de ferramentas do PageSpeed](https://developers.google.com/speed).

## Ambiente de criação {#author-environment}

### Realização de testes {#performing-tests}

Para realizar testes de desempenho no ambiente do autor, é necessário simular a experiência dos autores de produção. Ou seja, as instalações do autor devem conter todos os componentes, pacotes OSGi, personalização da interface do usuário, índices personalizados e quaisquer outras adições que você tenha em vigor para as instâncias do autor de produção.

Há muitas estruturas de automação disponíveis projetadas para testes de desempenho e carga. Os scripts personalizados podem ser gravados nessas ferramentas e reproduzidos para simular um número máximo de autores que executam atividades de ativação e criação de conteúdo semelhantes simultaneamente. É recomendável usar a ferramenta Tough Day para simular atividades como o upload de milhares de ativos ou a ativação de um grande número de páginas.

Para os tipos de ambientes que têm requisitos de carregamento pesado de ativos ou criação de página, é fundamental usar ferramentas como Dia difícil. Isso garante que o ambiente opere eficientemente sob carga máxima. [WebDAV](/help/sites-administering/webdav-access.md) é uma ferramenta que não requer scripts e também pode ser usada para carregar grandes quantidades de ativos.

#### Etapas específicas do MongoDB {#mongodb-specific-steps}

Em sistemas com back-end do MongoDB, o AEM fornece vários [JMX](/help/sites-administering/jmx-console.md) MBeans que devem ser monitoradas durante a realização de testes de carga ou desempenho:

* O **Estatísticas de Cache Consolidadas** MBean. Ele pode ser acessado diretamente indo até:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

Para o cache nomeado **Document-Diff**, a taxa de ocorrência deve estar acima `.90`. Se a taxa de ocorrência cair abaixo de 90%, é provável que você precise editar sua `DocumentNodeStoreService` configuração. O suporte ao produto Adobe pode recomendar configurações ideais para seu ambiente.

* O **Estatísticas do Repositório Oak** Feijão. Ele pode ser acessado diretamente indo até:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

O **ObservationQueueMaxLength** mostra o número de eventos na fila de observação do Oak nas últimas horas, minutos, segundos e semanas. Encontre o maior número de eventos na seção &quot;por hora&quot;. Comparar esse número ao `oak.observation.queue-length` configuração. Se o número mais elevado mostrado para a fila de observação exceder o valor de `queue-length` configuração:

1. Crie um arquivo chamado: `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` contendo o parâmetro `oak.observation.queue‐length=50000`
1. Coloque-o na pasta /crx-quickstart/install.

>[!NOTE]
>Consulte [AEM 6.x | Dicas de ajuste de desempenho](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=en)

A configuração padrão é 10.000, mas a maioria das implantações deve elevá-la para 20.000 ou 50.000.

## Ambiente de publicação {#publish-environment}

### Realização de testes {#performing-tests-1}

A parte mais importante de uma implantação que deve ser submetida a testes de carga é o ambiente de publicação ou Dispatcher voltado para o usuário final.

Ferramentas de testes automatizados de terceiros podem ser usadas para testar o desempenho do site. Essas ferramentas permitem registrar as etapas pelas quais os usuários passam no site e executar muitas dessas sessões ao mesmo tempo para simular a carga típica de um site de produção.

A maioria dos sites de produção tem otimizações em vigor, como o armazenamento em cache do Dispatcher e uma rede de entrega de conteúdo em vigor. Ao testar, verifique se essas otimizações também estão disponíveis para o ambiente de teste. Além de monitorar os tempos de resposta para os usuários finais, monitore as métricas do sistema nos servidores de publicação e despachantes para garantir que o sistema não seja restrito pelos recursos de hardware.

Em um sistema que não requer um alto nível de personalização, o Dispatcher deve armazenar a maioria das solicitações em cache. Como resultado, a carga na instância de publicação deve permanecer relativamente plana. Se um alto nível de personalização for necessário, é recomendável usar tecnologias como iFrames ou solicitações AJAX para o conteúdo personalizado para permitir o máximo possível de armazenamento em cache do Dispatcher.

Para testes básicos, o Apache Bench pode ser usado para medir os tempos de resposta do servidor da Web e ajudar a criar carga para medir coisas como vazamentos de memória. Veja o exemplo no [Documentação de monitoramento](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## Solução de problemas de desempenho {#troubleshooting-performance-issues}

Após executar testes de desempenho na instância do autor, todos os problemas devem ser investigados, diagnosticados e resolvidos. Você pode usar várias ferramentas e técnicas ao executar análises e solucionar problemas:

* Você pode inspecionar o [Log de desempenho da solicitação](/help/sites-administering/operations-dashboard.md#request-performance) no Painel de operações. Essa ferramenta pode ser usada para identificar solicitações de página lentas
* Analise consultas de execução lenta com o [Ferramenta Desempenho da Consulta](/help/sites-administering/operations-dashboard.md#query-performance)

* Observe o log de erros em busca de erros ou avisos. Para obter mais informações, consulte [Registro](/help/sites-deploying/configure-logging.md).
* Monitore recursos de hardware do sistema, como utilização de memória e CPU, E/S de disco ou E/S de rede. Esses recursos são frequentemente as causas de gargalos de desempenho.
* Otimize a arquitetura das páginas e como elas são endereçadas para minimizar o uso de parâmetros de URL para permitir o máximo possível de armazenamento em cache.
* Siga as [Otimização de desempenho](/help/sites-deploying/configuring-performance.md) e [Dicas para ajuste de desempenho](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=en) documentação.

* Se houver problemas com a edição de determinadas páginas ou componentes em instâncias do autor, use o Modo de desenvolvedor da interface sensível ao toque para inspecionar a página em questão. Isso fornece um detalhamento de cada área de conteúdo na página e seu tempo de carregamento.
* Reduza todos os JS e CSS no site. Veja isso [publicação do blog](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* Elimine o CSS e o JS incorporados dos componentes. Eles devem ser incluídos e minificados com as bibliotecas do lado do cliente para minimizar o número de solicitações necessárias para renderizar a página.
* Para inspecionar as solicitações do servidor e ver quais estão demorando mais, use as ferramentas do navegador, como a guia Rede do Chrome.

Depois que as áreas com problemas são identificadas, o código do aplicativo pode ser inspecionado para obter otimizações de desempenho. Qualquer recurso pronto para uso AEM que não esteja funcionando corretamente pode ser resolvido com o Suporte ao Adobe.
