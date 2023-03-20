---
title: Práticas recomendadas para testes de desempenho
seo-title: Best Practices for Performance Testing
description: Este artigo descreve as estratégias e metodologias gerais usadas para testes de desempenho, bem como algumas das ferramentas disponíveis para auxiliar no processo.
seo-description: This article outlines the overall strategies and methodologies used for performance testing as well as some of the tools that are available to assist in the process.
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 0%

---

# Práticas recomendadas para testes de desempenho{#best-practices-for-performance-testing}

## Introdução {#introduction}

O teste de desempenho é uma parte importante de qualquer implantação de AEM. Dependendo dos requisitos do cliente, o teste de desempenho pode ser realizado nas instâncias de publicação, nas instâncias do autor ou em ambos.

Essa documentação destacará estratégias e metodologias gerais de realização de testes de desempenho, bem como algumas das ferramentas disponibilizadas pelo Adobe para auxiliar no processo. Por fim, vamos analisar algumas das ferramentas disponíveis no AEM 6 para auxiliar no ajuste do desempenho, tanto de uma análise de código como da perspectiva de configuração do sistema.

### Simular realidade {#simulating-reality}

O que é mais importante ao executar testes de desempenho é garantir que você imite um ambiente de produção o mais próximo possível. Embora isso possa ser frequentemente difícil, é imperativo garantir a exatidão desses testes. Ao trabalhar na criação de testes de desempenho, é importante ter os seguintes pontos em consideração:

* Conteúdo semelhante à produção

Muitas medidas de desempenho no AEM, como o tempo de resposta da consulta, podem ser afetadas pelo tamanho do conteúdo no sistema. É importante garantir que o ambiente de teste tenha o mais próximo possível de uma cópia dos dados de produção.

* Código de produção

A versão AEM e os hotfixes implantados em produção devem ser os mesmos no ambiente de teste. Também é importante testar a versão do código implantada na produção.

* Configuração de hardware e rede semelhante à produção

Os testes serão sem sentido sem um ambiente que se assemelhe ao da produção. Idealmente, as especificações de hardware, as interfaces de rede, os balanceadores de carga e a CDN devem ser idênticos à produção no ambiente de teste.

* Carga de produção

Muitos problemas de desempenho não são vistos até que o sistema esteja sob carga pesada. Os bons ensaios de desempenho devem simular a carga em que os sistemas de produção estarão no seu pico.

### Definir metas {#setting-goals}

Antes de iniciar os ensaios de desempenho, é necessário definir requisitos não funcionais para especificar os tempos de carga e resposta. Se você estiver migrando de um sistema existente, verifique se o tempo de resposta é semelhante aos valores de produção atuais. Para carga, é melhor pegar a carga de pico atual e duplicá-la. Isso garantirá que o site possa continuar a ter um bom desempenho enquanto cresce.

### Ferramentas {#tools}

Há muitas ferramentas de teste de desempenho disponíveis comercialmente no mercado. Ao executar uma ferramenta de geração de carga, é importante garantir que os computadores que estão executando os testes tenham largura de banda de rede suficiente. Caso contrário, quando a máquina de teste atingir os limites de sua conexão, nenhuma carga adicional será gerada no ambiente em teste.

#### Ferramentas de teste {#testing-tools}

* Adobe **Dia difícil** A ferramenta pode ser usada para gerar carga em instâncias AEM e coletar dados de desempenho. A equipe de engenharia do Adobe usa o teste de carga do próprio produto. Os scripts executados em Tough Day são configurados por meio de arquivos de propriedade e arquivos XML JMX. Para obter mais informações, consulte o [Documentação do Dia difícil](/help/sites-developing/tough-day.md).

* AEM fornece ferramentas prontas para uso para ver rapidamente consultas, solicitações e mensagens de erro problemáticas. Para obter mais informações, consulte o [Ferramentas de diagnóstico](/help/sites-administering/operations-dashboard.md#diagnosis-tools) seção da documentação do Painel de operações.
* O Apache fornece um produto chamado **JMeter** que podem ser usados para testes de desempenho e carga, bem como comportamento funcional. Ele é um software de código aberto e gratuito, mas tem um conjunto de recursos menor do que os produtos corporativos e uma curva de aprendizado mais acentuada. O JMeter pode ser encontrado no site do Apache em [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Carregar Executador** é um produto de teste de carga de nível empresarial. Uma versão de avaliação gratuita está disponível. Mais informações podem ser encontradas em [https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* Ferramentas de teste de carga baseadas em nuvem como [Neustar](https://www.neustar.biz/services/web-performance/load-testing) também pode ser usado.
* Quando se trata de testar sites móveis ou responsivos, um conjunto separado de ferramentas precisa ser usado. Eles funcionam diminuindo a largura de banda da rede, simulando conexões móveis mais lentas, como 3G ou EDGE. Entre as ferramentas mais utilizadas estão:

   * **[Condicionador de links de rede](https://nshipster.com/network-link-conditioner/)** - fornece uma interface de usuário fácil de usar e funciona em um nível relativamente baixo na pilha de rede. Ele inclui versões para OS X e iOS;
   * [**Charles**](https://www.charlesproxy.com/) - um aplicativo proxy de depuração da Web que, além de várias outras utilizações, fornece controle de rede. As versões são fornecidas para Windows, OS X e Linux.

#### Ferramentas de otimização {#optimization-tools}

**Monitoramento**

O [Monitorar desempenho](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) a documentação é um bom recurso para ferramentas e métodos que podem ser usados para diagnosticar problemas e identificar áreas para ajuste.

**Modo de desenvolvedor na interface do usuário de toque**

Um dos novos recursos na interface de toque do AEM 6 é o Modo de desenvolvedor. Da mesma forma que os autores podem alternar entre os modos de edição e visualização, os desenvolvedores podem alternar para o modo desenvolvedor na interface do autor para ver o tempo de renderização de cada um dos componentes na página e ver rastreamentos de pilha de quaisquer erros. Para obter mais informações sobre o modo de desenvolvedor, consulte este [Apresentação de Gems CQ](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-developer-mode.html?lang=en).

**Usar o rlog.jar para ler os logs de solicitação**

Para obter uma análise mais abrangente dos logs de solicitação em um sistema de AEM, `rlog.jar` pode ser usado para pesquisar e classificar o `request.log` arquivos que AEM gerados. Este arquivo jar é incluído com uma instalação AEM no `/crx-quickstart/opt/helpers` pasta. Para obter mais informações sobre a ferramenta de log e o log de solicitações em geral, consulte o [Monitoramento e manutenção](/help/sites-deploying/monitoring-and-maintaining.md) documentação.

**A ferramenta Explain Query**

O [Explique a ferramenta Query](/help/sites-administering/operations-dashboard.md#explain-query) em ACS AEM Tools podem ser usados para exibir os índices usados ao executar um query. Isso pode ser muito útil ao otimizar consultas de execução lenta.

**Ferramentas PageSpeed**

As ferramentas Google PageSpeed oferecem análise do site para seguir as práticas recomendadas de desempenho da página, bem como um plug-in que pode ser instalado junto com o dispatcher em uma instância do Apache para obter otimizações adicionais. Para obter mais informações, consulte o [Site de ferramentas do PageSpeed](https://developers.google.com/speed/pagespeed/).

## Ambiente de criação {#author-environment}

### Realização de testes {#performing-tests}

Para realizar testes de desempenho no ambiente do autor, é necessário simular a experiência dos autores de produção. Isso significa que as instalações do autor devem conter todos os componentes, pacotes OSGi, personalização da interface do usuário, índices personalizados e quaisquer outras adições que você tenha em vigor para as instâncias do autor de produção.

Há muitas estruturas de automação disponíveis projetadas para testes de desempenho e carga. Os scripts personalizados podem ser gravados nessas ferramentas e reproduzidos para simular um número máximo de autores que executam atividades de ativação e criação de conteúdo semelhantes simultaneamente. É recomendável usar a ferramenta Tough Day para simular atividades como o upload de milhares de ativos ou a ativação de um grande número de páginas.

Para os tipos de ambientes que têm requisitos de carregamento pesado de ativos ou criação de páginas, é fundamental usar ferramentas como Tough Day para garantir que o ambiente opere com eficiência em carga de pico. [WebDAV](/help/sites-administering/webdav-access.md) é uma ferramenta que não requer scripts e também pode ser usada para carregar grandes quantidades de ativos.

#### Etapas específicas do MongoDB {#mongodb-specific-steps}

Em sistemas com back-end do MongoDB, o AEM fornece vários [JMX](/help/sites-administering/jmx-console.md) MBeans que precisam ser monitoradas ao executar testes de carga ou desempenho:

* O **Estatísticas de Cache Consolidadas** MBean. Ele pode ser acessado diretamente indo até:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

Para o cache nomeado **Document-Diff**, a taxa de ocorrência deve estar acima `.90`. Se a taxa de ocorrência cair abaixo de 90%, é provável que você precise modificar seu `DocumentNodeStoreService` configuração. O suporte ao produto Adobe pode recomendar configurações ideais para seu ambiente.

* O **Estatísticas do Repositório Oak** Feijão. Ele pode ser acessado diretamente indo até:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

O **ObservationQueueMaxLength** A seção mostrará o número de eventos na fila de observação do Oak nas últimas horas, minutos, segundos e semanas. Encontre o maior número de eventos na seção &quot;por hora&quot;. Esse número precisa ser comparado ao `oak.observation.queue-length` configuração. Se o número mais elevado mostrado para a fila de observação exceder o valor de `queue-length` configuração:

1. Crie um arquivo chamado: `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` contendo o parâmetro `oak.observation.queue‐length=50000`
1. Coloque-o na pasta /crx-quickstart/install.

>[!NOTE]
>Veja também o artigo KB sobre [AEM 6.x | Dicas de ajuste de desempenho](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

A configuração padrão é 10.000, mas a maioria das implantações geralmente precisa aumentá-la para 20.000 ou 50.000.

## Ambiente de publicação {#publish-environment}

### Realização de testes {#performing-tests-1}

A parte mais importante de uma implantação que precisa ser submetida a testes de carga é o ambiente de publicação ou dispatcher voltado para o usuário final.

Ferramentas de testes automatizados de terceiros podem ser usadas para testar o desempenho do site. Essas ferramentas permitirão registrar as etapas pelas quais os usuários passarão no site e executar muitas dessas sessões ao mesmo tempo para simular a carga típica de um site de produção.

A maioria dos sites de produção tem otimizações em vigor, como o armazenamento em cache do dispatcher e uma rede de entrega de conteúdo em vigor. Ao testar, você precisa garantir que essas otimizações também estejam disponíveis para o ambiente de teste. Além de monitorar os tempos de resposta para os usuários finais, também é necessário monitorar as métricas do sistema nos servidores de publicação e despachantes para garantir que o sistema não seja restrito pelos recursos de hardware.

Em um sistema que não requer um alto nível de personalização, o dispatcher deve armazenar a maioria das solicitações em cache. Como resultado, a carga na instância de publicação deve permanecer relativamente plana. Se um alto nível de personalização for necessário, é recomendável usar tecnologias como iFrames ou solicitações de AJAX para o conteúdo personalizado, de forma a permitir o máximo possível de armazenamento em cache do dispatcher.

Para testes básicos, o Apache Bench pode ser usado para medir os tempos de resposta do servidor da Web e ajudar a criar carga para medir coisas como vazamentos de memória. Para obter mais informações, consulte o exemplo na [Documentação de monitoramento](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## Solução de problemas de desempenho {#troubleshooting-performance-issues}

Após executar testes de desempenho na instância do autor, todos os problemas precisarão ser investigados, diagnosticados e resolvidos. Você pode usar várias ferramentas e técnicas ao executar análises e solucionar problemas:

* Você pode inspecionar o [Log de desempenho da solicitação](/help/sites-administering/operations-dashboard.md#request-performance) no Painel de operações. Essa ferramenta pode ser usada para identificar solicitações de página lentas
* Analise consultas de execução lenta com o [Ferramenta Desempenho da Consulta](/help/sites-administering/operations-dashboard.md#query-performance)

* Observe a lista de erros em busca de erros ou avisos. Para obter mais informações, consulte [Registro](/help/sites-deploying/configure-logging.md)
* Monitore recursos de hardware do sistema, como utilização de memória e CPU, E/S de disco ou E/S de rede. Esses recursos são frequentemente as causas de gargalos de desempenho
* Otimize a arquitetura das páginas e como elas são endereçadas para minimizar o uso de parâmetros de URL para permitir o maior armazenamento em cache possível
* Siga as [Otimização de desempenho](/help/sites-deploying/configuring-performance.md) e [Dicas para ajuste de desempenho](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) documentação

* Se houver problemas com a edição de determinadas páginas ou componentes em instâncias do autor, use o Modo de desenvolvedor da interface sensível ao toque para inspecionar a página em questão. Isso fornecerá um detalhamento de cada área de conteúdo na página, bem como seu tempo de carregamento
* Reduza todos os JS e CSS no site. Para obter mais informações sobre como fazer isso, consulte esta seção [publicação do blog](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* Elimine o CSS e o JS incorporados dos componentes. Eles devem ser incluídos e minificados com as bibliotecas do lado do cliente para minimizar o número de solicitações necessárias para renderizar a página
* Use ferramentas do navegador, como a guia Rede do Chrome para inspecionar as solicitações do servidor e ver quais estão demorando mais.

Depois que as áreas com problemas são identificadas, o código do aplicativo pode ser inspecionado para obter otimizações de desempenho. Qualquer recurso pronto para uso AEM que não esteja funcionando corretamente pode ser resolvido com o Suporte ao Adobe.
