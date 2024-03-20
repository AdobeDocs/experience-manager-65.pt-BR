---
title: Lista de verificação - Referência adicional
description: Saiba mais sobre detalhes que detalham e/ou aumentam os documentos e princípios cobertos pela Lista de verificação de gerenciamento de projetos - práticas recomendadas.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist
content-type: reference
exl-id: 36620e3e-ecdf-4062-bbef-65513362d691
solution: Experience Manager, Experience Manager 6.5
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '3699'
ht-degree: 1%

---

# Lista de verificação - Referência adicional{#the-checklist-further-reference}

Esta página fornece mais detalhes para elaborar e/ou aumentar os documentos e princípios cobertos pela [Gerenciamento de projetos - Lista de verificação de práticas recomendadas](/help/managing/best-practices.md).

## AEM - O que você vai usar? {#aem-what-will-you-be-using}

>[!CAUTION]
>
>As listas desta subseção não são exaustivas, mas destinam-se a ser uma introdução.

### Recursos no AEM {#features-within-aem}

Ao implementar o AEM (particularmente pela primeira vez), [recursos e fluxos de trabalho do AEM](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html) para ter certeza de quais áreas você deseja ou precisa.

Considere os recursos do AEM que você está usando e o impacto no design; por exemplo:

* [Commerce](/help/commerce/cif-classic/administering/ecommerce.md)
* [Screens](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=pt-BR)
* [Assets](/help/assets/assets.md)
* [Tags](/help/sites-administering/tags.md)
* [Gerenciamento e tradução de vários sites](/help/sites-administering/msm-and-translation.md)
* [Forms](/help/forms/using/introduction-aem-forms.md)
* [Communities](/help/communities/deploy-communities.md)

Além disso, verifique a [Notas de versão](/help/release-notes/release-notes.md), para as várias versões do AEM, para ver quando novos recursos foram adicionados.

### Integrações {#integrations}

O AEM pode ser integrado a outros produtos de Adobe, ou a serviços de terceiros, ou ambos. Esses workflows podem aumentar a potência e a funcionalidade à sua disposição.

Consulte [Integração de soluções](/help/sites-administering/integration.md) para obter informações completas.

## Migrar ou atualizar? {#migrate-or-upgrade}

Uma consideração importante é se você deseja:

* Atualizar a instalação existente no local.
* Migre o conteúdo do sistema atual para uma nova instalação.

Ao mudar de uma versão anterior para a versão atual, há duas opções:

* Use o [Gerenciador de pacotes](/help/sites-administering/package-manager.md) para exportar todo o conteúdo e código do aplicativo do sistema antigo para o novo.
* [Atualizar](/help/sites-deploying/upgrade.md) o sistema antigo no local. Este método é geralmente a escolha recomendada.

## Regras Básicas de Base {#basic-ground-rules}

Como acontece com qualquer projeto, é fundamental estabelecer regras básicas o mais rápido possível. Essas regras incluem:

>[!NOTE]
>
>Estes pontos são genéricos, a [Lista de verificação de práticas recomendadas](/help/managing/best-practices.md) trata de aspectos específicos relacionados com o AEM.

* **Funções**

  As funções devem ser claramente definidas e comunicadas a todos os envolvidos no projeto. Além disso, é aconselhável destacar:

   * Tomadores de decisão
   * Pontos de contato

* **Responsabilidades**

   * Para cada função, uma definição clara das responsabilidades relacionadas ao projeto ajuda a evitar confusão.

* **Envolvimento**

  Ao envolver as partes interessadas o mais rapidamente possível, pode incentivá-las a *partes interessadas* no projeto. Fazer isso aumenta o compromisso deles com o sucesso.

   * No lado do cliente, essa função inclui os autores que trabalham com o sistema diariamente
   * Em sua própria equipe de projeto, esse envolvimento também inclui as pessoas responsáveis pela garantia de qualidade. Quanto mais eles entenderem as necessidades do cliente, melhor poderão planejar os testes.

* **Caminhos de comunicação**

   * Embora as vias de comunicação não devam ser formalizadas de forma excessiva, as definições específicas devem garantir que as pessoas-chave são sempre informadas e, por conseguinte, mantidas atualizadas. Deve ser dada especial atenção à comunicação com terceiros.

* **Processos**

  Os processos definidos dependem do seu projeto individual. Novamente, tente manter esses processos simples, considerando:

   * Definição de processos (e caminhos de comunicação) para interagir com terceiros; por exemplo, agências de design e fornecedores de software de terceiros, entre outros.
   * Geralmente, o cliente tem seus próprios procedimentos e ferramentas de gerenciamento e geração de relatórios de projetos.

* **Ferramentas de rastreamento**

  Há muitas ferramentas disponíveis para rastrear informações sobre bugs, tarefas e outros aspectos do seu projeto - consulte [Visão geral de ferramentas em potencial](#overview-of-potential-tools) para obter mais detalhes.

   * O ponto principal a ser observado aqui é manter apenas uma cópia das informações e compartilhá-las (e, portanto, o acesso à ferramenta que está sendo usada). Esse fluxo de trabalho facilita a manutenção e ajuda a evitar discrepâncias.

* **Escopo**

  Definir claramente o que deve ser abrangido pelo projeto a vários níveis:

   * as versões individuais (se um processo de versão iterativa for usado e independentemente de serem entregues aos clientes ou à equipe interna de teste).
   * o projeto AEM.
   * todo o projeto; incluindo qualquer software de terceiros, seu impacto nos testes, problemas organizacionais e muitos outros.
   * Para certos aspectos, pode também ser útil indicar o que é *não* no âmbito do projeto. Essa ideia pode ajudar a evitar confusão e suposições incorretas, embora deva se limitar a questões essenciais.

* **Relatório**

  Defina claramente quais informações você deseja reportar, em que formato, com que frequência e para quem.

* **Terminologia**

   * Defina quaisquer abreviações e/ou terminologia específica do cliente a ser usada.

* **Suposições**

   * Defina quaisquer suposições que estejam sendo feitas.

Essas informações podem ser definidas em um Manual do projeto; o uso de um wiki também pode ajudar a garantir que as alterações contínuas sejam tratadas de forma eficiente. Sempre que essas suposições forem definidas, os principais fatores serão:

* As informações são definidas e mantidas
* A informação é claramente comunicada a todas as pessoas envolvidas. Embora seja uma prática padrão de Gerenciamento de projetos, ela não pode ser repetida com frequência suficiente para que uma definição de função clara e uma boa comunicação possam criar ou interromper um projeto.
* Somente uma versão é mantida de qualquer informação que esteja sendo rastreada; por exemplo, rastreamento de erros e rastreamento de problemas.

## Indicadores-chave de desempenho e métricas de direcionamento {#key-performance-indicators-and-target-metrics}

As organizações usam Indicadores-chave de desempenho (KPIs) para avaliar seu sucesso em atingir metas. Esses indicadores são valores mensuráveis que podem ser usados para demonstrar o quão efetivamente objetivos específicos estão sendo cumpridos.

Esses indicadores podem ser:

* Empresas:

   * Usado para medir os principais objetivos de negócios.
   * É importante escolher KPIs apropriados para seus negócios/cenários com definições claras do que são, como são medidos, como são usados e por quem.

* Desempenho:

   * Defina como medir o desempenho do sistema.
   * Alguns exemplos incluem tempo de carregamento de página, tempo de resposta do servidor e desempenho de consulta do banco de dados.

Alguns indicadores, mas não todos, podem ser baseados nas métricas de direcionamento que você identifica e define.

### Métricas do Target {#target-metrics}

Métricas são usadas para definir medidas quantitativas para a qualidade do seu site. Elas são basicamente uma definição das metas de desempenho que você deseja atingir e podem ser usadas para definir seus [KPIs (Indicadores-chave de desempenho)](#key-performance-indicators-and-target-metrics).

Muitas métricas podem ser definidas, mas com frequência as que você define abrangem suas metas de desempenho e simultaneidade. Em especial, fatores que podem ser difíceis de quantificar e são frequentemente *emocional* avaliação:

* &quot;o site é *muito lento* hoje&quot; - quando o faz *lento* qualificar?

* &quot;tudo *trituração até à paragem* quando meu colega fizer login&quot; - quantos usuários simultâneos o sistema pode suportar?
* &quot;quando eu pesquiso, o sistema *trituração até à paragem* &quot; - que solicitações de pesquisa estão afetando o sistema?
* &quot;é necessário *idades* para baixar o arquivo&quot; - quais são os tempos de download aceitáveis (em condições normais de rede)?

As métricas do Target são definidas no início de um projeto para:

* indique as dimensões esperadas do site que você pode oferecer
* indique a qualidade mínima que deseja atingir
* definir como esses fatores são medidos
* ser utilizado como base para a [Indicadores-chave de desempenho](#key-performance-indicators-and-target-metrics)

Como sempre, é preciso ter cuidado ao definir as métricas de direcionamento:

* se definido como muito alto, pode ser inatingível
* se forem definidas flutuações muito baixas, não é possível realçá-las
* assegurar que possam ser repetida e consistentemente avaliadas
* para proporcionar um equilíbrio entre os diferentes fatores que estão a ser
* determinadas métricas estão relacionadas a um ambiente de teste, mas algumas devem refletir cenários reais, pois devem ser mensuráveis e reproduzíveis no site de produção
* priorize as métricas de acordo com sua importância para o site
* limitar as métricas a um conjunto que possa ser monitorado

Durante o desenvolvimento do projeto, eles podem ser atualizados e ajustados conforme apropriado. Após a implementação bem-sucedida do projeto, eles podem ser usados para ajudá-lo a controlar sua instalação e monitorar/manter os níveis de serviço necessários para a operação contínua.

Quando usadas corretamente, essas métricas podem fornecer uma ferramenta útil; quando usadas de forma irresponsável, elas podem ser uma distração que desperdiça tempo. Como sempre, entenda o que você está medindo, como você está medindo isso e por quê.

>[!NOTE]
>
>Esta seção discute os princípios básicos e as questões que devem ser consideradas. Cada instalação é diferente, portanto, os valores reais a serem medidos tendem a diferir.

### Tudo depende do design do seu projeto {#everything-rests-on-your-project-design}

Todas as métricas medidas são afetadas pelo design do seu projeto. Por outro lado, muitos problemas são melhor resolvidos por alterações de design.

Portanto, defina suas métricas de direcionamento *antes* decidir sobre o seu design. Isso permite otimizar seu design com base nesses fatores. Depois que seu projeto é desenvolvido, para os princípios básicos de design é desafiador.

Ao criar a estrutura do site, siga a estrutura recomendada para sites com AEM. Compreenda os seguintes problemas e/ou princípios:

* Como estruturar o conteúdo do site.
* Como os modelos e componentes funcionam.
* Como funciona o armazenamento em cache?
* Os impactos do conteúdo personalizado.
* Como a função de pesquisa funciona.
* Como você pode usar o CSS e tecnologias relacionadas para criar código de HTML compacto e não redundante.

Se você achar que o seu design não segue as diretrizes ou se não tiver certeza sobre algumas das implicações, esclareça esses problemas. Faça isso antes de iniciar a fase de programação ou de preencher o conteúdo.

### Infraestrutura {#infrastructure}

Para definir ou avaliar a infraestrutura, ajuda a definir valores de destino como:

* visitantes/dia; médio e pico
* ocorrências/dia; média e pico
* número de páginas da Web sendo disponibilizadas
* volume de conteúdo da Web

Dependendo da sua situação e do significado estratégico do site, a definição da infraestrutura pode ajudá-lo a avaliar e escolher sua infraestrutura:

* número de servidores
* número de instâncias do AEM (autor e publicação)

### Desempenho {#performance}

Há vários fatores de desempenho que podem ser avaliados:

* tempos de resposta para páginas individuais, considerando:

   * tempos de resposta em um ambiente de autor
   * tempos de resposta no ambiente de publicação

* tempos de resposta para solicitações de pesquisa

Esta seção pode ser lida com [Otimização do desempenho](/help/sites-deploying/configuring-performance.md) isso expande os detalhes técnicos para medir realmente o desempenho.

#### Tempos de resposta para páginas individuais {#response-times-for-individual-pages}

Um problema importante é o tempo que o site leva para responder às solicitações do visitante.

Embora esse valor varie para cada solicitação, um valor de target médio pode ser definido. Quando esse valor puder ser obtido e mantido, poderá ser usado para monitorar o desempenho do site e indicar o desenvolvimento de possíveis problemas

Destinos diferentes em ambientes de autor e publicação

Os tempos de resposta almejados são diferentes nos ambientes de criação e publicação, refletindo o público-alvo:

* **Ambiente do autor**

  Esse ambiente é usado pelos autores que inserem e atualizam conteúdo, portanto, ele deve:

   * Atender a alguns usuários que geram um alto número de solicitações ao atualizar páginas de conteúdo e os elementos individuais nessas páginas
   * seja o mais rápido possível para maximizar a produtividade e colocar seu conteúdo em seu site

* **Ambiente de publicação**

  Esse ambiente contém conteúdo que você disponibiliza para os usuários:

   * a velocidade ainda é vital, mas geralmente é mais lenta do que um ambiente de criação
   * mecanismos adicionais de melhoria do desempenho são frequentemente aplicados:

      * o conteúdo é armazenado em cache
      * balanceamento de carga aplicado

#### Definição de tempos de resposta de target {#setting-target-response-times}

Como você pode decidir sobre tempos de resposta viáveis (médios)? A pergunta e a resposta geralmente são uma questão de experiência:

* experiência no seu site
* experiência com AEM
* reconhecer páginas complexas que têm tempos de resposta acima da média (se possível, essas páginas devem ser otimizadas individualmente)

No entanto, em circunstâncias controladas, as seguintes diretrizes podem ser aplicadas:

* 70% das solicitações de páginas devem responder em menos de 100 ms.
* 25% das solicitações para páginas devem responder em menos de 100 ms a 300 ms.
* 4% das solicitações para páginas devem responder em menos de 300 ms a 500 ms.
* 1% das solicitações para páginas deve responder em menos de 500 ms a 1000 ms.
* Nenhuma página deve responder mais lentamente do que um segundo.

Os números acima assumem as seguintes condições:

* medido na publicação (sem ambiente de criação e/ou sobrecarga do CFC)
* medido no servidor (sem sobrecarga da rede)
* não armazenado em cache (sem cache de saída AEM, sem cache do Dispatcher)
* somente para itens complexos com muitas dependências (HTML, JS, PDF, ...)
* nenhuma outra carga no sistema

Há vários mecanismos que você pode usar para monitorar os tempos de resposta:

* **Monitoramento dos tempos de resposta com o request.log do AEM**

  Um bom ponto de partida para a análise de desempenho é o registro de solicitações. Entre outras informações, você pode ver os tempos de resposta de solicitações individuais. Consulte [Otimização do desempenho](/help/sites-deploying/configuring-performance.md) para obter mais detalhes.

* **Monitoramento dos tempos de resposta com comentários de HTML**

  Os comentários de HTML podem ser usados para incluir informações de tempo de resposta na fonte de cada página:

  `</body> </html>v <-- Page took 58 milliseconds to be rendered by the server --> Response times for search requests`

#### Solicitações de pesquisa {#search-requests}

As solicitações de pesquisa podem ter um impacto significativo no seu site, em termos de:

* Tempo de resposta da pesquisa real

   * Uma função de pesquisa rápida é um objetivo de qualidade para o seu site

* Impacto no desempenho geral

   * Como uma função de pesquisa deve verificar (potencialmente grandes) seções do conteúdo ou um índice especialmente extraído, essa capacidade pode afetar o desempenho do sistema inteiro, se não for otimizada

Definir alvos para solicitações de pesquisa é, novamente, uma questão de experiência, dependendo do seguinte:

* experiência do AEM
* uma avaliação da frequência com que a pesquisa é usada em comparação a outras metas
* seu gerenciador de persistência
* seu índice de pesquisa
* a complexidade de sua função de pesquisa; uma função de pesquisa básica que permite a inserção de um termo de pesquisa é mais rápida do que uma pesquisa avançada que permite que o usuário crie instruções de pesquisa complexas usando E/OU/NÃO.

Essas solicitações de pesquisa devem ser planejadas e integradas desde o início do projeto. Os mecanismos disponíveis para monitoramento incluem:

* **Monitoramento dos tempos de resposta de pesquisa com o request.log do AEM**

  Novamente, o request.log pode ser usado para monitorar os tempos de resposta para solicitações de pesquisa; consulte [Otimização do desempenho](/help/sites-deploying/configuring-performance.md) para obter mais detalhes.

* **Mecanismos programados para medir os tempos de resposta de pesquisa**

  Para personalizar as informações coletadas sobre as solicitações de pesquisa e seu desempenho, é recomendável incluir a coleta de informações no código-fonte do projeto; consulte [Otimização do desempenho](/help/sites-deploying/configuring-performance.md) para obter mais detalhes.

### Simultaneidade {#concurrency}

Disponibilize o site para alguns usuários e visitantes nos ambientes do autor e de publicação. Geralmente, os números são maiores do que os usados nos testes, mas também flutuantes e difíceis de prever. Crie seu site para um número médio de usuários e visitantes simultâneos sem notar um impacto negativo no desempenho. Novamente, use o `request.log` para fazer testes de simultaneidade. Consulte [Otimização do desempenho](/help/sites-deploying/configuring-performance.md) para obter mais detalhes.

As metas para o número de usuários simultâneos dependem do tipo de ambiente:

* **Ambiente do autor**

   * Normalmente, o número de usuários simultâneos pode ser estimado com precisão. Você pode saber quantos autores você tem no total, embora (provavelmente) nem todos estejam ativos ao mesmo tempo.

* **Ambiente de publicação**

   * O ambiente de publicação é mais difícil de prever, portanto, você deve selecionar um valor de destino. Novamente, deve se basear na experiência do seu site atual, juntamente com expectativas realistas do seu novo site.
   * Eventos especiais (por exemplo, quando você publica conteúdo novo e popular) podem exceder as expectativas - ou até mesmo os recursos (como às vezes relatado na imprensa, quando os ingressos para certos eventos são disponibilizados para venda).

### Capacidade e volume {#capacity-and-volume}

Antes de discutir as métricas relacionadas, forneça uma definição rápida dos termos:

* **Volume**

   * A quantidade de saída processada e entregue pelo sistema.

* **Capacidade**

   * A capacidade do sistema de fornecer o volume.
   * Em cada etapa, a capacidade e o volume são medidos de forma diferente, conforme mostrado na tabela abaixo. Para obter o melhor desempenho, verifique se a capacidade corresponde ao volume em cada etapa e se a capacidade e o volume são compartilhados em todas as etapas. Por exemplo, você pode calcular a navegação no computador cliente ou colocá-la no cache, em vez de computá-la no servidor para cada solicitação.

* **Capacidade e volume**

  | O que/onde | Capacidade | Volume |
  |---|---|---|
  | Cliente | Potência computacional do computador do usuário. | Complexidade do layout da página. |
  | Rede | Largura de banda de rede. | Tamanho da página (código, imagens e assim por diante). |
  | Cache do Dispatcher | Memória do servidor Web (memória principal e disco rígido). | Servidor da Web (memória principal e disco rígido). Número e tamanho das páginas em cache. |
  | Cache de saída | Memória do servidor AEM (memória principal e disco rígido). | Número e tamanho das páginas no cache de saída, o número de dependências por página. O cache do Dispatcher reduz esse volume. |
  | Servidor Web | Potência computacional do servidor Web. | Número de solicitações. O armazenamento em cache diminui esse volume. |
  | Modelo | Potência computacional do servidor Web. | Complexidade dos modelos. |
  | Repositório | Desempenho do repositório. | Número de páginas carregadas do repositório. |

### Outras métricas {#other-metrics}

As seções anteriores detalham as principais métricas a serem definidas.

Dependendo dos seus requisitos específicos, pode ser útil definir métricas adicionais isoladamente ou considerando as classificações acima.

No entanto, é preferível ter um pequeno conjunto de métricas principais e precisas que funcionem de forma fácil e confiável, em vez de tentar medir e definir cada aspecto do seu site. Por sua natureza, seu site começa a mudar e evoluir quando é entregue aos seus usuários.

## Segurança {#security}

A segurança é crucial e um desafio cada vez maior. É ***deve*** ser consideradas e planejadas desde as primeiras etapas do projeto.

A variável [Lista de verificação de segurança](/help/sites-administering/security-checklist.md) detalhes etapas que você deve seguir para garantir que sua instalação do AEM esteja segura quando implantada. Outros aspectos de segurança são abrangidos pelo [Segurança (ao desenvolver)](/help/sites-developing/security.md) e [Administração e segurança do usuário](/help/sites-administering/security.md).

## Tarefas Paralelas e Iterativas {#parallel-and-iterative-tasks}

>[!NOTE]
>
>O seguinte:
>
>* Oferece uma visão geral relacionada ao *primeiro* implementação de um projeto AEM.
>* É destinado a ser uma visão geral abstrata; consulte a [Lista de verificação do projeto](/help/managing/best-practices.md) para fases/etapas/tarefas específicas.
>* Qualquer escala de tempo é teórica.
>

Para uma nova implementação de um projeto AEM padrão, considere tarefas como:

* Transferência do processo de vendas.
* Implementação do aplicativo do cliente (**Desenvolvimento**).
* Instalação e configuração da infraestrutura (e processos relacionados) no local do cliente (**Infraestrutura**).
* Criação (ou migração) do conteúdo (**Conteúdo**).
* Transferência para operações (**Manutenção/suporte**).
* Acompanhe as versões.

![chlimage_1-2](assets/chlimage_1-2.png)

Em todos os aspectos, recomenda-se a utilização de uma abordagem iterativa:

![chlimage_1-3](assets/chlimage_1-3.png)

>[!NOTE]
>
>Para permitir o ajuste, a otimização e o treinamento do usuário em condições realistas no ambiente de produção, divida o lançamento do projeto em **Inicialização suave** (disponibilidade reduzida, várias iterações) e **Inicialização rígida** (disponibilidade total - Em tempo real).

>[!NOTE]
>
>Consulte a [Lista de verificação do projeto](/help/managing/best-practices.md) para obter exemplos de tarefas que você deve executar (ou avaliar) durante o ciclo de vida do seu projeto.

Alguns pontos a observar para cada categoria são:

* **Desenvolvimento**

   * Defina primeiro a arquitetura básica.
   * Use várias iterações (sprints) para desenvolvimento:

      * First sprint equivale ao primeiro ciclo completo de desenvolvimento.
      * O primeiro sprint resulta na primeira implantação em seu ambiente de teste.
      * Cada sprint tem um resultado executável.
      * Cada sprint recebe uma aprovação do cliente (mínimo de teste estruturado com feedback).

   * Planeje a eventualidade de uma atualização da versão disponível do AEM durante o projeto.
   * Planejar testes e otimização durante sprints.
   * Plano para as fases de estabilização e otimização.
   * Criar um log de itens a serem planejados para outras versões.
   * Planeje a participação do parceiro e a entrega.

* **Infraestrutura**

   * Defina primeiro a arquitetura básica:

      * Definir requisitos de desempenho.
      * Definir metas de desempenho (ou seja, definir claramente as expectativas).
      * Definir a arquitetura de hardware e infraestrutura, incluindo dimensionamento.
      * Defina a implantação.

   * Use várias iterações; para o primeiro sprint e a configuração inicial, prepare:

      * Ambiente de desenvolvimento.
      * Processo de desenvolvimento.
      * Ambiente de teste.
      * Processo de implantação (incluindo gerenciamento de configuração).

   * Planejar vários testes de carga.
   * Planejar testes e otimização durante sprints.
   * Planejar uma fase de estabilização e otimização.
   * Implantar no ambiente de produção o mais rápido possível (permitir que a equipe de operações configure o sistema para ganhar experiência).
   * Use usuários nomeados e funções definidas o mais cedo possível.
   * Plano de treinamento (por exemplo, treinamento de administrador).
   * Planejar a transferência para operações.

* **Conteúdo**

   * A arquitetura básica:
      * Direciona a hierarquia de conteúdo.
      * Ajuda a definir o conceito de conteúdo.
      * Define o uso e o layout do MSM.
      * Define funções, grupos, fluxos de trabalho e permissões.
   * Considere se a criação de página offline é útil.
   * Planeje a criação antecipada das primeiras páginas e conteúdo (para uso em testes e feedback).
   * Planeje a migração do conteúdo existente.
   * Planeje a migração rápida após a refatoração.
   * Planejar &quot;burndown de conteúdo&quot; (mapa do site para conteúdo de ativação).

## Estimativa de tempo e esforço {#estimating-time-and-effort}

Dependendo da lista de tarefas resultante, é possível fazer estimativas iniciais de tempo e esforço para definições de tarefas (de alto nível). Essas estimativas devem incluir uma indicação de quem (cliente ou parceiro) faz o que e quando.

A lista a seguir mostra as aproximações padrão e as inter-relações de esforço envolvidas e, portanto, os custos:

>[!CAUTION]
>
>Esses números só podem ser usados para estimativas iniciais. Um desenvolvedor de AEM experiente deve fazer a análise detalhada.

| Fase | Esforço |
|---|---|
| Desenvolvimento | Uma estimativa aproximada de 2 a 4 horas para cada nó de componente que abrange todos os requisitos de desenvolvimento. |
| Teste do desenvolvedor | 15% do desenvolvimento |
| Acompanhamento | 10% do desenvolvimento |
| Documentação | 15% do desenvolvimento |
| Documentação do JavaDoc | 10% do desenvolvimento |
| Correção de erros | 15% do desenvolvimento |
| Gerenciamento de projeto | 20% dos custos do projeto para gerenciamento e governança contínuos de projetos |

O planejamento detalhado pode então relacionar recursos disponíveis ou necessários a prazos e custos.

## Arquitetura de referência {#reference-architecture}

A arquitetura de referência é fornecida para fornecer uma solução de modelo para a arquitetura AEM. A arquitetura de referência aborda problemas comuns encontrados em sistemas corporativos, incluindo dimensionamento, confiabilidade e segurança.

As seguintes métricas do site devem ser definidas:

| Classificação | Definição |
|---|---|
| Número de sites da Internet |  |
| Número de sites da intranet |  |
| Número de bases de código (por exemplo, se a Internet e a intranet forem diferentes) |  |
| Número de páginas individuais |  |
| Número de visitas ao site/dia |  |
| Número de visualizações de página por dia |  |
| Volume (em GB) de transferência de dados/dia |  |
| Número de usuários simultâneos (Grupo de Usuários Fechado) |  |
| Número de visitantes simultâneos (publicação) |  |
| Número de autores simultâneos |  |
| Número de autores registrados |  |
| Número de ativações de página/dia útil |  |
| Número de ativações de página durante a implantação |  |

## Visão geral de ferramentas em potencial {#overview-of-potential-tools}

A lista a seguir é fornecida para informá-lo sobre as ferramentas que podem ser usadas. Ela serve como uma introdução, não como uma lista de recomendações extensa, e não deve impedir você de usar outras ferramentas.

<table>
 <tbody>
  <tr>
   <td><strong>Produto</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>AEM</td>
   <td><p>O próprio AEM fornece uma variedade de mecanismos para ajudá-lo a monitorar, testar, investigar e depurar seu aplicativo; incluindo:</p>
    <ul>
     <li><a href="/help/sites-developing/developer-mode.md">Modo de desenvolvedor</a></li>
     <li>A variável <a href="/help/sites-developing/hobbes.md">Console de teste</a></li>
     <li><a href="/help/sites-administering/operations-dashboard.md">Painel de operações</a></li>
     <li><a href="/help/sites-authoring/content-insights.md">Content Insight</a></li>
     <li>A variável <a href="/help/sites-authoring/author-environment-tools.md#content-tree">Árvore de conteúdo</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Selênio</td>
   <td><a href="https://www.selenium.dev/">Selênio</a> O é uma ferramenta de teste de Código aberto. Os testes são executados diretamente no navegador, emulando o funcionamento dos usuários.</td>
  </tr>
  <tr>
   <td>Projeto Microsoft®</td>
   <td>Uma ferramenta de gerenciamento de projetos usada com frequência.</td>
  </tr>
  <tr>
   <td>Jira</td>
   <td><a href="https://www.atlassian.com/software/jira">Jira</a> O é uma ferramenta de código aberto para rastrear e gerenciar detalhes de bugs de software. Os workflows podem ser impostos aos detalhes do bug, conforme necessário.</td>
  </tr>
  <tr>
   <td>Git</td>
   <td><a href="https://git-scm.com/">Git</a> O é um software de controle de revisão.</td>
  </tr>
  <tr>
   <td>Eclipse</td>
   <td><p>Eclipse é um IDE de código aberto, composto por vários projetos. Ele se concentra na criação de uma plataforma de desenvolvimento aberta composta de estruturas, ferramentas e tempos de execução extensíveis para a criação, implantação e gerenciamento de software durante todo o ciclo de vida.</p> <p>Consulte <a href="/help/sites-developing/howto-projects-eclipse.md">Como desenvolver projetos de AEM usando o Eclipse</a> para obter mais informações.</p> </td>
  </tr>
  <tr>
   <td>IntelliJ</td>
   <td><p>Um IDE profissional (e, portanto, sujeito a custos de licenciamento) que oferece uma ampla variedade de recursos. </p> <p>Consulte <a href="/help/sites-developing/ht-intellij.md">Como desenvolver projetos AEM usando o IntelliJ IDEA</a> para obter mais informações.</p> </td>
  </tr>
  <tr>
   <td>Maven</td>
   <td><a href="https://maven.apache.org/">Maven</a> O é uma ferramenta de gerenciamento e compreensão de projetos de software que pode gerenciar o processo de criação de um projeto (software e documentação).</td>
  </tr>
 </tbody>
</table>

## Leitura adicional {#further-reading}

Além disso, as seguintes seções são de especial interesse:

* [Introdução](/help/sites-deploying/deploy.md#getting-started)
* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Monitoramento e manutenção de sua instância](/help/sites-deploying/monitoring-and-maintaining.md)

### Práticas recomendadas {#best-practices}

O Adobe fornece práticas recomendadas adicionais para todas as fases e públicos-alvo:

* [Implantar](/help/sites-deploying/best-practices.md)
* [Criação  ](/help/sites-authoring/best-practices.md)
* [Administração](/help/sites-administering/administer-best-practices.md)
* [Desenvolvimento](/help/sites-developing/best-practices.md)
* [Gerenciamento de projeto](/help/managing/best-practices.md)
