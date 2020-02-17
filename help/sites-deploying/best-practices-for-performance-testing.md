---
title: Práticas recomendadas para testes de desempenho
seo-title: Práticas recomendadas para testes de desempenho
description: Este artigo descreve as estratégias e metodologias gerais usadas para testes de desempenho, bem como algumas das ferramentas disponíveis para auxiliar no processo.
seo-description: Este artigo descreve as estratégias e metodologias gerais usadas para testes de desempenho, bem como algumas das ferramentas disponíveis para auxiliar no processo.
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Práticas recomendadas para testes de desempenho{#best-practices-for-performance-testing}

## Introdução {#introduction}

O teste de desempenho é uma parte importante de qualquer implantação do AEM. Dependendo das necessidades do cliente, os testes de desempenho podem ser executados nas instâncias de publicação, de autor ou em ambas.

Essa documentação descreverá as estratégias e metodologias gerais de realização de testes de desempenho, bem como algumas das ferramentas disponibilizadas pela Adobe para auxiliar no processo. Por fim, analisaremos algumas das ferramentas disponíveis no AEM 6 para auxiliar no ajuste do desempenho, tanto da perspectiva da análise de código como da configuração do sistema.

### Simular realidade {#simulating-reality}

O que é mais importante ao executar testes de desempenho é garantir que você imite um ambiente de produção o mais próximo possível. Embora isso possa muitas vezes ser difícil, é imperativo garantir a precisão destes testes. Ao trabalhar na criação de testes de desempenho, é importante levar em consideração os seguintes pontos:

* Conteúdo semelhante à produção

Muitas medidas de desempenho no AEM, como o tempo de resposta da consulta, podem ser afetadas pelo tamanho do conteúdo no sistema. É importante garantir que o ambiente de teste tenha o mais próximo possível de uma cópia dos dados de produção.

* Código de produção

A versão do AEM e os hotfixes implantados na produção devem ser os mesmos no ambiente de teste. Também é importante testar a versão do código implantada na produção.

* Configuração de hardware e rede semelhantes à produção

Os testes serão sem sentido sem um ambiente tão próximo quanto possível da produção. Idealmente, as especificações de hardware, as interfaces de rede, os balanceadores de carga e o CDN devem ser idênticos à produção no ambiente de teste.

* Carga de produção

Muitos problemas de desempenho não são observados até que o sistema esteja com carga pesada. Os testes de bom desempenho devem simular a carga em que os sistemas de produção estarão no pico.

### Definindo Metas {#setting-goals}

Antes de iniciar o teste de desempenho, é necessário definir requisitos não funcionais para especificar os tempos de carga e resposta. Se você estiver migrando de um sistema existente, verifique se o tempo de resposta é semelhante aos valores de produção atuais. Para carga, é melhor pegar a carga máxima atual e duplicá-la. Isso garantirá que o site possa continuar a ter um bom desempenho enquanto cresce.

### Ferramentas {#tools}

Há muitas ferramentas de teste de desempenho disponíveis no mercado. Ao executar uma ferramenta geradora de carga, é importante garantir que os computadores que estão executando os testes tenham largura de banda de rede suficiente. Caso contrário, uma vez que a máquina de teste atinge os limites da sua conexão, não será gerada nenhuma carga adicional no ambiente em teste.

#### Ferramentas de teste {#testing-tools}

* A ferramenta **Dia** difícil da Adobe pode ser usada para gerar carga nas instâncias do AEM e coletar dados de desempenho. A equipe de engenharia do AEM da Adobe usa a ferramenta para fazer o teste de carga do próprio produto AEM. Os scripts executados no Dia difícil são configurados por arquivos de propriedade e arquivos XML JMX. Para obter mais informações, consulte a documentação [do Dia](/help/sites-developing/tough-day.md)difícil.

* O AEM fornece ferramentas prontas para ver rapidamente consultas, solicitações e mensagens de erro problemáticas. Para obter mais informações, consulte a seção Ferramentas [de](/help/sites-administering/operations-dashboard.md#diagnosis-tools) diagnóstico na documentação do Painel de operações.
* O Apache fornece um produto chamado **JMeter** que pode ser usado para teste de desempenho e carga, bem como comportamento funcional. É um software de código aberto e gratuito de usar, mas tem um conjunto de recursos menor do que os produtos corporativos e uma curva de aprendizado mais acentuada. O JMeter pode ser encontrado no site do Apache em [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **O Load Runner** é um produto de teste de carga de nível corporativo. Uma versão de avaliação gratuita está disponível. Mais informações estão disponíveis no site [https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* Ferramentas de teste de carga baseadas em nuvem, como [Neustar](https://www.neustar.biz/services/web-performance/load-testing) , também podem ser usadas.
* Quando se trata de testar sites móveis ou responsivos, é necessário usar um conjunto separado de ferramentas. Eles funcionam reduzindo a largura de banda da rede, simulando conexões móveis mais lentas, como 3G ou EDGE. Entre as ferramentas mais usadas estão:

   * **[Condicionador](https://nshipster.com/network-link-conditioner/)**de links de rede - ele fornece uma interface de usuário fácil de usar e funciona em um nível bastante baixo na pilha de rede. Inclui versões para OS X e iOS;[](https://nshipster.com/network-link-conditioner/)
   * [**Charles **](https://www.charlesproxy.com/)- um aplicativo proxy de depuração da Web que, além de vários outros usos, fornece controle de rede. As versões são fornecidas para Windows, OS X e Linux.[](https://www.charlesproxy.com/)

#### Ferramentas de otimização {#optimization-tools}

**Monitoramento**

A documentação de Desempenho [de](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) Monitoramento é um bom recurso para ferramentas e métodos que podem ser usados para diagnosticar problemas e identificar áreas para ajuste.

**Modo de desenvolvedor na interface do usuário de toque**

Um dos novos recursos na interface de usuário de toque do AEM 6 é o Modo de desenvolvedor. Assim como os autores podem alternar entre os modos de edição e visualização, os desenvolvedores podem alternar para o modo desenvolvedor na interface do autor para ver o tempo de renderização de cada um dos componentes na página e para ver os rastreamentos de pilha de quaisquer erros. Para obter mais informações sobre o modo desenvolvedor, consulte esta apresentação [do](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html)CQ Gems.

**Uso do rlog.jar para ler os registros de solicitação**

Para obter uma análise mais abrangente dos registros de solicitação em um sistema AEM, `rlog.jar` é possível usá-los para pesquisar e classificar os `request.log` arquivos gerados pelo AEM. Esse arquivo jar está incluído em uma instalação do AEM na `/crx-quickstart/opt/helpers` pasta. Para obter mais informações sobre a ferramenta de registro e o registro de solicitações em geral, consulte a documentação [Monitoramento e manutenção](/help/sites-deploying/monitoring-and-maintaining.md) .

**A ferramenta Explicar consulta**

A ferramenta [](/help/sites-administering/operations-dashboard.md#explain-query) Explicar consulta em Ferramentas AEM ACS pode ser usada para exibir os índices usados ao executar uma consulta. Isso pode ser muito útil ao otimizar consultas de execução lenta.

**Ferramentas do PageSpeed**

As ferramentas PageSpeed do Google oferecem análise do site para seguir as práticas recomendadas para o desempenho da página, bem como um plug-in que pode ser instalado junto com o dispatcher em uma instância do Apache para obter otimizações adicionais. Para obter mais informações, consulte o site [de ferramentas](https://developers.google.com/speed/pagespeed/)PageSpeed.

## Ambiente de criação {#author-environment}

### Realização de testes {#performing-tests}

Para realizar testes de desempenho no ambiente do autor, é necessário simular a experiência dos autores de produção. Isso significa que as instalações do autor devem conter todos os componentes, pacotes OSGi, personalização da interface do usuário, índices personalizados e quaisquer outras adições que você tenha em vigor para as instâncias do autor da produção.

Há muitas estruturas de automação disponíveis projetadas para teste de desempenho e carga. Os scripts personalizados podem ser gravados nessas ferramentas e reproduzidos para simular um número máximo de autores que executam atividades de criação e ativação de conteúdo semelhantes simultaneamente. É recomendável usar a ferramenta Dia difícil para simular atividades como carregar milhares de ativos ou ativar grandes números de páginas.

Para os tipos de ambientes que têm requisitos de carregamento de ativos pesados ou criação de páginas, é imperativo usar ferramentas como o Dia difícil para garantir que o ambiente opere com eficiência em carga máxima. [O WebDAV](/help/sites-administering/webdav-access.md) é uma ferramenta que não requer scripts e também pode ser usada para carregar grandes quantidades de ativos.

#### Etapas específicas do MongoDB {#mongodb-specific-steps}

Em sistemas com backends MongoDB, o AEM fornece vários MBeans [JMX](/help/sites-administering/jmx-console.md) que precisam ser monitorados ao executar testes de carga ou desempenho:

* O MBean de Estatísticas **de Cache** Consolidado. Ele pode ser acessado diretamente indo até:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

Para o cache chamado **Document-Diff**, a taxa de ocorrência deve ter terminado `.90`. Se a taxa de ocorrência cair abaixo de 90%, é provável que você precise modificar sua `DocumentNodeStoreService` configuração. O suporte ao produto Adobe pode recomendar configurações ideais para seu ambiente.

* O Mbean De Estatísticas **Do Repositório** Oak. Ele pode ser acessado diretamente indo até:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

A seção **ObservationQueueMaxLength** mostrará o número de eventos na fila de observação do Oak nas últimas horas, minutos, segundos e semanas. Encontre o maior número de eventos na seção &quot;por hora&quot;. Esse número precisa ser comparado à `oak.observation.queue-length` configuração que pode ser encontrada no componente **SlingRepositoryManager** no console [](/help/sites-deploying/web-console.md)OSGi. Se o número mais alto mostrado para a fila de observação exceder a `queue-length` configuração, entre em contato com o Suporte da Adobe para obter ajuda para aumentar a configuração. A configuração padrão é 1.000, mas a maioria das implantações geralmente precisa aumentá-la para 20.000 ou 50.000.

## Ambiente de publicação {#publish-environment}

### Realização de testes {#performing-tests-1}

A parte mais importante de uma implantação que precisa ser submetida a testes de carga é o ambiente de publicação ou despachante voltado para o usuário final.

Ferramentas de teste automatizadas de terceiros podem ser usadas para testar o desempenho do site. Essas ferramentas permitirão registrar etapas pelas quais os usuários navegarão no site e executarão muitas dessas sessões ao mesmo tempo para simular a carga típica de um site de produção.

A maioria dos sites de produção tem otimizações no local, como o dispatcher caching e uma rede de entrega de conteúdo no local. Ao testar, verifique se essas otimizações também estão disponíveis para o ambiente de teste. Além de monitorar os tempos de resposta dos usuários finais, também é necessário monitorar as métricas do sistema nos servidores e despachantes de publicação para garantir que o sistema não seja restringido pelos recursos de hardware.

Em um sistema que não requer um alto nível de personalização, o dispatcher deve armazenar a maioria das solicitações em cache. Como resultado, a carga na instância de publicação deve permanecer relativamente simples. Se for necessário um alto nível de personalização, é recomendável usar tecnologias como iFrames ou solicitações AJAX para o conteúdo personalizado, de modo a permitir o máximo de dispatcher em cache possível.

Para testes básicos, o Apache Bench pode ser usado para medir o tempo de resposta do servidor Web e ajudar a criar carga para medir coisas como vazamentos de memória. Para obter mais informações, consulte o exemplo na documentação [](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench)Monitoramento.

## Solução de problemas de desempenho {#troubleshooting-performance-issues}

Depois de executar testes de desempenho na instância do autor, todos os problemas precisarão ser investigados, diagnosticados e abordados. Você pode usar várias ferramentas e técnicas ao executar análises e solucionar problemas:

* Você pode inspecionar o log [de Desempenho da](/help/sites-administering/operations-dashboard.md#request-performance) Solicitação no Painel de Operações. Essa ferramenta pode ser usada para identificar solicitações de página lentas
* Analisar consultas de execução lenta com a ferramenta Desempenho da [consulta](/help/sites-administering/operations-dashboard.md#query-performance)

* Verifique se há erros ou avisos na lista de erros. For more information, see [Logging](/help/sites-deploying/configure-logging.md)
* Monitore os recursos de hardware do sistema, como a utilização de memória e CPU, E/S de disco ou E/S de rede. Esses recursos são frequentemente as causas dos gargalos de desempenho
* Otimizar a arquitetura das páginas e como elas são endereçadas para minimizar o uso de parâmetros de URL para permitir o máximo de armazenamento em cache possível
* Siga a documentação das dicas [de ajuste de otimização](/help/sites-deploying/configuring-performance.md) de [desempenho e](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) desempenho

* Se houver problemas com a edição de determinadas páginas ou componentes em instâncias do autor, use o TouchUI Developer Mode para inspecionar a página em questão. Isso fornecerá um detalhamento de cada área de conteúdo na página, bem como seu tempo de carregamento
* Minifique todos os JS e CSS no site. Para obter mais informações sobre como fazer isso, consulte esta publicação [no](https://blogs.adobe.com/foxes/enable-js-and-css-minification/)blog.
* Elimine o CSS e o JS incorporados dos componentes. Elas devem ser incluídas e minimizadas com as bibliotecas do lado do cliente para minimizar o número de solicitações necessárias para renderizar a página
* Use ferramentas de navegador, como a guia Rede do Chrome, para inspecionar as solicitações do servidor e ver quais estão demorando mais.

Depois que as áreas com problemas são identificadas, o código do aplicativo pode ser inspecionado para verificar se há otimizações de desempenho. Todos os recursos do AEM que não estão funcionando corretamente podem ser abordados com o suporte da Adobe.
