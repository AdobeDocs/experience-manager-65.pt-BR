---
title: Lista de verificação - Referência adicional
seo-title: Lista de verificação - Referência adicional
description: Saiba mais sobre detalhes adicionais que desenvolvem e/ou aumentam os documentos e princípios cobertos pela lista de verificação Gerenciar projetos - práticas recomendadas.
seo-description: Saiba mais sobre detalhes adicionais que desenvolvem e/ou aumentam os documentos e princípios cobertos pela lista de verificação Gerenciar projetos - práticas recomendadas.
uuid: 58a8b4ab-e447-4a12-b9e9-4cd3db11e06a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist
content-type: reference
discoiquuid: 6fc2751e-f42a-4519-bc8c-695057f21b69
translation-type: tm+mt
source-git-commit: 37ec3d8ce779ba392e6a92c828efb5fad749abec
workflow-type: tm+mt
source-wordcount: '3783'
ht-degree: 1%

---


# A Lista de Verificação - Mais Referência{#the-checklist-further-reference}

Esta página fornece mais detalhes para desenvolver e/ou aumentar os documentos e princípios cobertos pela [Lista de verificação de gerenciamento de projetos - práticas recomendadas](/help/managing/best-practices.md).

## AEM - O que você vai usar? {#aem-what-will-you-be-using}

>[!CAUTION]
>
>As listas desta subseção não são exaustivas, mas destinam-se a uma introdução.

### Recursos no AEM {#features-within-aem}

Ao implementar o AEM (especialmente pela primeira vez), você precisará revisar os recursos e workflows [do AEM](https://www.adobe.com/br/marketing/experience-manager.html) para ter certeza de quais áreas deseja/precisa.

Considere os recursos do AEM que você usará e o impacto no seu design; por exemplo:

* [Commerce](/help/sites-administering/ecommerce.md)
* [Telas](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)
* [Assets](/help/assets/assets.md)
* [Tags](/help/sites-administering/tags.md)
* [Gerenciamento e tradução de vários sites](/help/sites-administering/msm-and-translation.md)
* [Forms](/help/forms/home.md)
* [Comunidades](/help/communities/deploy-communities.md)
* [Livefyre](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)

Além disso, verifique as [Notas de versão](/help/release-notes/release-notes.md), para obter as várias versões do AEM, para ver quando novos recursos foram adicionados.

### Integrações {#integrations}

AEM pode ser integrado a outros produtos de Adobe e/ou serviços de terceiros. Eles podem aumentar a potência e a funcionalidade à sua disposição.

Consulte [Integração de soluções](/help/sites-administering/integration.md) para obter informações completas.

## Migrar ou atualizar? {#migrate-or-upgrade}

Uma consideração importante é se você deseja:

* Atualize a instalação existente.
* Migre o conteúdo do sistema atual para uma nova instalação.

Ao mover de uma versão anterior para a atual, há duas opções:

* Use o [Gerenciador de pacotes](/help/sites-administering/package-manager.md) para exportar todo o conteúdo e o código do aplicativo do sistema antigo para o novo.
* [](/help/sites-deploying/upgrade.md) Atualize o sistema antigo no lugar. Essa é a opção recomendada na maioria dos casos.

## Regras básicas de base {#basic-ground-rules}

Tal como acontece com qualquer projeto, é fundamental estabelecer regras básicas o mais rapidamente possível. Dentre elas:

>[!NOTE]
>
>Esses pontos são genéricos, a [Lista de verificação de práticas recomendadas](/help/managing/best-practices.md) trata de detalhes específicos relacionados à AEM.

* **Funções**

   Estas devem ser claramente definidas e divulgadas a todos os participantes no projeto. Além disso, é aconselhável destacar:

   * Tomadores de decisão
   * Pontos de contato

* **Responsabilidades**

   * Para cada função, uma definição clara das responsabilidades relacionadas ao seu projeto ajuda a evitar confusão.

* **Participação**

   Ao envolver as partes interessadas o mais rapidamente possível, você pode incentivá-las a se tornarem *partes interessadas* no projeto, aumentando assim o seu compromisso com o seu sucesso.

   * No lado do cliente, isso inclui os autores - que terão de trabalhar com o sistema diariamente.
   * Dentro da sua equipe de projeto, isso também incluirá os responsáveis pelo controle de qualidade. Quanto mais compreenderem os requisitos do cliente, melhor poderão planejar os testes.

* **Caminhos de comunicação**

   * Embora estas não devam ser excessivamente formalizadas, definições específicas devem assegurar que as pessoas-chave sejam sempre informadas e, por conseguinte, mantidas atualizadas. Deve ser dada especial atenção à comunicação com as partes externas.

* **Processos**

   Os processos a serem definidos dependerão de seu projeto individual. Tente novamente manter esses itens simples, considerando:

   * Definir processos (e vias de comunicação) para interagir com terceiros; Por exemplo, agências de concepção e fornecedores de software de terceiros, entre outros.
   * Muitas vezes, o cliente terá seus próprios procedimentos e ferramentas de gerenciamento de projetos e de Relatórios.

* **Ferramentas de rastreamento**

   Há muitas ferramentas disponíveis para rastrear informações sobre bugs, tarefas e outros aspectos do seu projeto - consulte [Visão geral das ferramentas potenciais](#overview-of-potential-tools) para obter mais detalhes.

   * O ponto principal a ser observado aqui é manter apenas uma cópia das informações e compartilhá-las (e, portanto, o acesso à ferramenta usada). Isso facilitará a manutenção e ajudará a evitar discrepâncias.

* **Escopo**

   Definir claramente o que deve ser abrangido pelo projeto a vários níveis:

   * as versões individuais (se for usado um processo de lançamento iterativo e independentemente de serem entregues aos clientes ou à sua equipe interna de teste).
   * o projeto AEM.
   * todo o projeto; incluindo qualquer software de terceiros, seu impacto em testes, problemas organizacionais e muitos outros.
   * Para certos aspectos, também pode ser útil indicar o que é *e não* no escopo do projeto. Tal pode contribuir para evitar confusões e pressupostos incorretos, embora deva limitar-se a questões essenciais.

* **Relatório**

   Defina claramente que informações você reportará, de que forma, com que frequência e para quem.

* **Terminologia**

   * Defina qualquer abreviação e/ou terminologia específica do cliente a ser usada.

* **Pressupostos**

   * Defina qualquer suposição sendo feita.

Estas informações podem ser definidas no Manual do Projeto; o uso de um Wiki também pode ajudar a garantir que as mudanças em andamento sejam tratadas de forma eficiente. Sempre que forem definidos, os principais fatores são os seguintes:

* As informações são definidas e mantidas
* A informação é claramente comunicada a todas as pessoas relevantes envolvidas. Embora a prática padrão de Gerenciamento de projetos não possa ser repetida com frequência o suficiente para que uma definição clara de função e uma boa comunicação possam criar ou quebrar um projeto.
* Apenas é conservada uma versão de qualquer informação que esteja a ser acompanhada; por exemplo, rastreamento de erros, rastreamento de problemas etc.

## Principais indicadores de desempenho e métricas de Público alvo {#key-performance-indicators-and-target-metrics}

As organizações usam os Indicadores-chave de desempenho (KPIs) para avaliar seu sucesso ao atingir públicos alvos. Estes indicadores são valores mensuráveis que podem ser utilizados para demonstrar a eficácia do cumprimento de objetivos específicos.

Esses indicadores podem ser:

* Negócios:

   * Usado para medir objetivos-chave de negócios.
   * É importante escolher os KPIs adequados à sua empresa/cenário com definições claras do que são, como serão avaliados, como serão usados e por quem.

* Show:

   * Defina como medir o desempenho do sistema.
   * Alguns exemplos incluem tempo de carregamento da página, tempo de resposta do servidor e desempenho do query do banco de dados.

Alguns indicadores, mas não todos, podem ser baseados nas métricas de público alvo que você identifica e define.

### Métricas de público alvo {#target-metrics}

As métricas são usadas para definir medidas quantitativas para a qualidade de seu site - elas são basicamente uma definição das metas de desempenho que você deseja atingir e podem ser usadas para definir seus [KPIs (Indicadores-chave de desempenho)](#key-performance-indicators-and-target-metrics).

Muitas métricas podem ser definidas, mas muitas vezes as que você define cobrem suas metas de desempenho e simultaneidade. Em particular, fatores que podem ser difíceis de quantificar e que muitas vezes estão sujeitos à avaliação *emocional*:

* &quot;nosso site está *muito lento* hoje&quot; - quando *lento* se qualifica?

* &quot;tudo *fica parado* quando meu colega faz logon&quot; - quantos usuários simultâneos podem suportar o sistema?
* &quot;quando eu pesquisar, o sistema *fica parado* &quot; - que tipo de solicitações de pesquisa estão afetando o sistema?
* &quot;é necessário *ages* para fazer o download do arquivo&quot; - quais são os tempos de download aceitáveis (em condições normais de rede)?

As métricas de público alvo são definidas no start de um projeto para:

* indique as dimensões esperadas do site que você vai oferta
* indicar a qualidade mínima que pretende atingir
* definir como esses fatores serão realmente medidos
* ser usado como a base para os [Indicadores-chave de desempenho](#key-performance-indicators-and-target-metrics)

Como sempre, é necessário ter cuidado ao definir as métricas de público alvo:

* se estiver definido como muito alto, pode ser completamente inatingível
* se estiver definido como flutuações muito baixas, talvez não seja realçado
* para garantir que possam ser medidos de forma repetida e consistente
* para proporcionar um equilíbrio entre os diferentes fatores que estão a ser medidos
* determinadas métricas se relacionarão a um ambiente de teste, mas algumas devem refletir os cenários da vida real, pois devem ser mensuráveis e reprodutíveis no site de produção
* priorizar as métricas de acordo com sua importância para o site
* limitar as métricas a um conjunto que possa ser realisticamente monitorado

Durante o desenvolvimento do projeto, podem ser atualizados e ajustados conforme adequado. Depois que o projeto for implementado com êxito, ele poderá ser usado para ajudá-lo a controlar sua instalação e monitorar/manter os níveis de serviço necessários para a operação contínua.

Quando usadas corretamente, essas métricas podem fornecer uma ferramenta útil; quando usados de forma irresponsável, podem ser uma distração que desperdiça tempo. Como sempre, você precisa entender o que está medindo, como está medindo e por quê.

>[!NOTE]
>
>A presente seção aborda os princípios básicos e as questões a considerar. Cada instalação é diferente, portanto os valores reais a serem medidos serão diferentes.

### Tudo está no Projeto {#everything-rests-on-your-project-design}

Todas as métricas a serem medidas serão, de alguma forma, afetadas pelo design do seu projeto. Por outro lado, muitas questões serão melhor resolvidas através de mudanças de design.

Portanto, você deve definir suas métricas de público alvo *antes de* decidir sobre seu design. Isso permite otimizar seu design com base nesses fatores. Uma vez desenvolvido o seu projeto, será difícil introduzir quaisquer alterações nos princípios básicos de concepção.

Ao criar a estrutura para o site, siga a estrutura recomendada para AEM sites. Certifique-se de compreender os seguintes problemas e/ou princípios:

* Como estruturar o conteúdo do site.
* Como os modelos e componentes funcionam.
* Como o cache funciona.
* Os impactos de conteúdo personalizado.
* Como a função de pesquisa funciona.
* Como você pode usar o CSS e as tecnologias relacionadas para criar código HTML compacto e não redundante.

Se você achar que seu design não segue as diretrizes, ou se não tiver certeza sobre algumas das implicações, esclareça essas questões antes de start da fase de programação ou do preenchimento do conteúdo.

### Infraestrutura {#infrastructure}

Para definir ou avaliar a infraestrutura, ajudará a definir valores de público alvo, como:

* visitantes/dia; média e pico
* ocorrências/dia; média e pico
* número de páginas da Web que estão sendo disponibilizadas
* volume de conteúdo da Web

Dependendo da sua situação e do significado estratégico do site, isso o ajudará a avaliar e escolher sua infraestrutura:

* número de servidores
* número de instâncias AEM (autor e publicação)

### Show {#performance}

Há vários fatores de desempenho que podem ser avaliados:

* tempos de resposta para páginas individuais, levando em conta:

   * tempos de resposta em um ambiente do autor
   * tempos de resposta no ambiente de publicação

* tempos de resposta para solicitações de pesquisa

Esta seção pode ser lida em conjunto com [Performance Otimization](/help/sites-deploying/configuring-performance.md), que expande os detalhes técnicos da medição real do desempenho.

#### Tempo de resposta para páginas individuais {#response-times-for-individual-pages}

Um problema chave é o tempo que seu site leva para responder às solicitações do visitante.

Embora esse valor varie para cada solicitação, um valor médio de público alvo pode ser definido. Uma vez que este valor seja comprovadamente alcançável e sustentável, poderá ser utilizado para acompanhar o desempenho do website e indicar o desenvolvimento de potenciais problemas

Diferentes públicos alvos em ambientes de autor e publicação

Os tempos de resposta desejados serão diferentes nos ambientes do autor e publicação, refletindo a audiência do público alvo:

* **Ambiente de criação**

   Esse ambiente é usado pelos autores que inserem e atualizam o conteúdo, portanto, ele deve:

   * atenda a um pequeno número de usuários que geram um grande número de solicitações ao atualizar páginas de conteúdo e os elementos individuais nessas páginas
   * seja o mais rápido possível para maximizar a produtividade para obter o conteúdo em seu site

* **Ambiente de publicação**

   Este ambiente contém conteúdo que você disponibiliza para seus usuários:

   * a velocidade ainda é vital, mas muitas vezes é mais lenta do que um ambiente do autor
   * são frequentemente aplicados mecanismos adicionais de melhoria do desempenho:

      * o conteúdo é armazenado em cache
      * o balanceamento de carga é aplicado

#### Definindo tempos de resposta do público alvo {#setting-target-response-times}

Então, como você pode decidir sobre tempos de resposta alcançáveis (médios)? Isso é frequentemente uma questão de experiência:

* experiência passada em seu site
* experiência com AEM
* reconhecer páginas complexas que têm tempos de resposta acima da média (eles devem ser otimizados individualmente, se possível)

No entanto, (em circunstâncias controladas) podem ser aplicadas as seguintes orientações:

* 70% das solicitações de páginas devem responder em menos de 100 ms.
* 25% das solicitações de páginas devem responder em menos de 100 ms a 300 ms.
* 4% das solicitações de páginas devem responder em menos de 300 ms a 500 ms.
* 1% das solicitações de páginas devem responder em menos de 500 ms a 1000 ms.
* Nenhuma página deve responder mais lentamente que 1 segundo.

Os números acima assumem as seguintes condições:

* medido na publicação (sem ambiente de criação e/ou sobrecarga de CFC)
* medido no servidor (sem sobrecarga de rede)
* não armazenado em cache (sem cache de saída AEM, sem cache do Dispatcher)
* somente para itens complexos com muitas dependências (HTML, JS, PDF, ...)
* nenhuma outra carga no sistema

Existem vários mecanismos que você pode usar para monitorar os tempos de resposta:

* **Monitorando os tempos de resposta com o AEM request.log**

   Um bom ponto de partida para a análise de desempenho é o registro de solicitações. Entre outras informações, você pode usar isso para ver os tempos de resposta de solicitações individuais. Consulte [Otimização de Desempenho](/help/sites-deploying/configuring-performance.md) para obter mais detalhes.

* **Monitoramento de tempos de resposta com comentários HTML**

   Os comentários HTML podem ser usados para incluir informações de tempo de resposta na fonte de cada página:

   `</body> </html>v <-- Page took 58 milliseconds to be rendered by the server --> Response times for search requests`

#### Solicitações de pesquisa {#search-requests}

As solicitações de pesquisa podem ter um impacto significativo em seu site, em termos de:

* Tempo de resposta da pesquisa real

   * Uma função de pesquisa rápida é uma meta de qualidade para seu site

* Impacto no desempenho geral

   * Como uma função de pesquisa deve verificar (potencialmente grande) seções do conteúdo, ou um índice extraído especialmente, isso pode afetar o desempenho de todo o sistema se não for otimizado

A definição de públicos alvos para solicitações de pesquisa é, novamente, uma questão de experiência, dependendo de:

* experiência de AEM
* uma avaliação da frequência com que a pesquisa será usada em comparação com outros objetivos
* seu gerente de persistência
* seu índice de pesquisa
* a complexidade da sua função de pesquisa; uma função de pesquisa básica que permite somente inserir um termo de pesquisa será mais rápida do que uma pesquisa avançada que permite ao usuário criar declarações de pesquisa complexas usando E/OU/NÃO.

Eles devem ser planejados e integrados a partir do próprio start do seu projeto. Os mecanismos disponíveis para acompanhamento incluem:

* **Monitorando tempos de resposta de pesquisa com AEM request.log**

   Novamente, o request.log pode ser usado para monitorar os tempos de resposta das solicitações de pesquisa; consulte [Otimização de Desempenho](/help/sites-deploying/configuring-performance.md) para obter mais detalhes.

* **Mecanismos programados para medir tempos de resposta de pesquisa**

   Para personalizar as informações coletadas sobre solicitações de pesquisa e seu desempenho, é recomendável incluir a coleta de informações no código-fonte do projeto; consulte [Otimização de Desempenho](/help/sites-deploying/configuring-performance.md) para obter mais detalhes.

### Simultaneidade {#concurrency}

Seu site será disponibilizado para vários usuários/visitantes, tanto no autor quanto nos ambientes de publicação. Os números são geralmente mais altos do que você usou ao testar, mas também flutuantes e difíceis de prever. Seu site precisará ser projetado para um número médio de usuários/visitantes simultâneos sem notar um impacto negativo no desempenho. Novamente, `request.log` pode ser usado para fazer testes de simultaneidade; consulte [Otimização de Desempenho](/help/sites-deploying/configuring-performance.md) para obter mais detalhes.

Públicos alvos para o número de usuários simultâneos dependem do tipo de ambiente:

* **Ambiente de criação**

   * Geralmente, o número de usuários simultâneos pode ser estimado com precisão. Você saberá quantos autores tem no total, embora (provavelmente) nem todos estarão ativos ao mesmo tempo.

* **Ambiente de publicação**

   * Isso é mais difícil de prever, portanto você deve selecionar um valor de público alvo. Novamente, isso deve se basear na experiência do seu site atual, juntamente com expectativas realistas do seu novo site.
   * Os eventos especiais (por exemplo, quando você publica novos conteúdos muito populares) podem exceder as expectativas - ou até mesmo as capacidades (conforme reportado na imprensa quando os ingressos para determinados eventos são disponibilizados para venda).

### Capacidade e volume {#capacity-and-volume}

Antes de discutir as métricas relacionadas, uma definição rápida dos termos:

* **Volume**

   * A quantidade de saída processada e entregue pelo sistema.

* **Capacidade**

   * A capacidade do sistema de fornecer o volume.
   * Em cada etapa, a capacidade e o volume são medidos de forma diferente, como mostra a tabela abaixo. Para obter o melhor desempenho, verifique se a capacidade corresponde ao volume em cada etapa e se a capacidade e o volume são compartilhados em todas as etapas. Por exemplo, você pode calcular a navegação no computador cliente ou colocá-la no cache, em vez de calculá-la no servidor para cada solicitação.

* **Capacidade e volume**

   | O quê / Onde | Capacidade | Volume |
   |---|---|---|
   | Cliente | Poder computacional do computador do usuário. | Complexidade do layout da página. |
   | Rede | Largura de banda da rede. | Tamanho da página (código, imagens e assim por diante). |
   | Cache do Dispatcher | Memória do servidor da Web (memória principal e disco rígido). | Servidor Web (memória principal e disco rígido). Número e tamanho das páginas em cache. |
   | Cache de saída | Memória do servidor AEM (memória principal e disco rígido). | Número e tamanho das páginas no cache de saída, o número de dependências por página. O cache do dispatcher diminui esse volume. |
   | Servidor Web | Poder computacional do servidor Web. | Quantidade de solicitações. O cache diminui esse volume. |
   | Modelo | Poder computacional do servidor Web. | Complexidade dos modelos. |
   | Repositório | Desempenho do repositório. | Número de páginas carregadas do repositório. |

### Outras métricas {#other-metrics}

As seções anteriores detalham as principais métricas a serem definidas.

Dependendo das suas necessidades específicas, pode ser útil definir métricas adicionais, isoladas ou levando em conta as classificações acima.

No entanto, é preferível ter um pequeno conjunto de métricas principais e precisas que funcionam de forma fácil e confiável, em vez de tentar medir e definir cada aspecto do site. Pela sua natureza pura, o seu website terá a start de mudar e evoluir assim que for entregue aos seus usuários.

## Segurança {#security}

A segurança é crucial e um desafio cada vez maior. Ele ***deve*** ser considerado e planejado a partir dos estágios iniciais do seu projeto.

A [Lista de verificação de segurança](/help/sites-administering/security-checklist.md) detalha as etapas que você deve seguir para garantir que sua instalação AEM esteja segura quando implantada. Outros aspectos de segurança estão cobertos em [Security (ao desenvolver)](/help/sites-developing/security.md) e [User Administration and Security](/help/sites-administering/security.md).

## Tarefas paralelas e iterativas {#parallel-and-iterative-tasks}

>[!NOTE]
>
>O seguinte:
>
>* Oferta uma visão geral relacionada à implementação *first* de um projeto AEM.
>* É destinado como uma visão geral abstrata; consulte a [Lista de verificação do projeto](/help/managing/best-practices.md) para obter fases/marcos/tarefas específicos.
>* Qualquer escala de tempo é teórica.

>



Para uma nova implementação de um projeto padrão de AEM, é necessário considerar tarefas como:

* Entrega do processo de vendas.
* Implementação do aplicativo do cliente (**Desenvolvimento**).
* Instalação e configuração da infraestrutura (e processos relacionados) no local do cliente (**Infraestrutura**).
* Criação (ou migração) do conteúdo (**Content**).
* Transferir para operações (**Manutenção/Suporte**).
* Versões de acompanhamento.

![chlimage_1-2](assets/chlimage_1-2.png)

Para todos os aspectos, é recomendável usar uma abordagem iterativa:

![chlimage_1-3](assets/chlimage_1-3.png)

>[!NOTE]
>
>Divida a inicialização do projeto em **Inicialização(ões) suave(s)** (disponibilidade reduzida, várias iterações) e **Inicialização forçada** (disponibilidade total - ao vivo) para permitir o ajuste, a otimização e o treinamento do usuário em condições realistas no ambiente de produção.

>[!NOTE]
>
>Consulte a [Lista de verificação do projeto](/help/managing/best-practices.md) para obter exemplos de tarefas que você deve executar (ou avaliar) durante o ciclo de vida do seu projeto.

Alguns pontos a serem observados para cada categoria são:

* **Desenvolvimento**

   * Defina a arquitetura básica primeiro.
   * Use várias iterações (sprints) para o desenvolvimento:

      * A primeira etapa equivale ao primeiro ciclo completo de desenvolvimento.
      * A primeira impressão resulta na primeira implantação do ambiente de teste.
      * Cada sprint tem um resultado que pode ser utilizado.
      * Cada sprint recebe uma aprovação do cliente (mínimo de teste estruturado com feedback).
   * Plano para a eventualidade de uma atualização da versão AEM disponível durante o projeto.
   * Plano de testes e otimização durante as impressões.
   * Plano para as fases de estabilização e otimização.
   * Crie um log de itens a serem planejados para novas versões.
   * Plano de participação e entrega dos parceiros.


* **Infraestrutura**

   * Defina a arquitetura básica primeiro:

      * Defina os requisitos de desempenho.
      * Defina as metas de desempenho (ou seja, defina claramente as expectativas).
      * Definir a arquitetura do hardware e da infraestrutura; incluindo dimensionamento.
      * Defina a implantação.
   * Usar várias iterações; para a primeira impressão e configuração inicial, prepare:

      * Ambiente de desenvolvimento.
      * Processo de desenvolvimento.
      * Ambiente de teste.
      * Processo de implantação (incluindo gerenciamento de configuração).
   * Planejar vários testes de carga.
   * Plano de testes e otimização durante as impressões.
   * Plano para uma fase de estabilização e otimização.
   * Implante para o ambiente de produção o mais cedo possível (permita que a equipe de operações configure o sistema para obter experiência).
   * Use usuários nomeados e funções definidas o mais cedo possível.
   * Plano de treinamento (por exemplo, treinamento de administrador).
   * Planeje a entrega para operações.



* **Conteúdo**

   * A arquitetura básica:
      * Direciona a hierarquia de conteúdo.
      * Ajuda a definir o conceito de conteúdo.
      * Define o uso e o layout do MSM.
      * Define funções, grupos, workflows e permissões.
   * Considere se a criação de página offline será útil.
   * Plano para a criação antecipada de primeiras páginas e conteúdo (para uso em testes e feedback).
   * Plano para a migração do conteúdo existente.
   * Plano de &quot;migração na primavera&quot; após a refatoração.
   * Planeje a &quot;lista suspensa de conteúdo&quot; (mapa do site para conteúdo disponível).

## Estimando tempo e esforço {#estimating-time-and-effort}

Dependendo da lista de tarefa resultante, você pode fazer estimativas iniciais de tempo e esforço para definições de tarefas (de alto nível). Eles devem incluir uma indicação de quem (cliente ou parceiro) fará o que e quando.

A lista a seguir mostra aproximações padrão e inter-relações de esforço envolvido e, portanto, custos:

>[!CAUTION]
>
>Estes valores só podem ser utilizados para estimativas iniciais. Um desenvolvedor AEM experiente deve fazer a análise detalhada.

| Fase | Esforço |
|---|---|
| Desenvolvimento | Uma estimativa aproximada de 2 a 4 horas para cada nó de componente cobrirá todos os requisitos de desenvolvimento. |
| Teste do desenvolvedor | 15% de Desenvolvimento |
| Acompanhamento | 10% de Desenvolvimento |
| Documentação | 15% de Desenvolvimento |
| Documentação do JavaDoc | 10% de Desenvolvimento |
| Correção de erros | 15% de Desenvolvimento |
| Gerenciamento de projeto | 20% dos custos do projeto para gerenciamento e governança de projetos em andamento |

O planeamento detalhado pode então relacionar os recursos disponíveis ou necessários com prazos e custos.

## Arquitetura de referência {#reference-architecture}

A arquitetura de referência é fornecida para fornecer uma solução modelo para a arquitetura AEM. A arquitetura de referência soluciona problemas comumente encontrados para sistemas corporativos, incluindo dimensionamento, confiabilidade e segurança.

As seguintes métricas do site devem ser definidas:

| Classificação | Definição |
|---|---|
| Número de sítios Internet |  |
| Número de sites da intranet |  |
| Número de bases de código (por exemplo, se a Internet e a intranet forem diferentes) |  |
| Número de páginas individuais |  |
| Número de visitas/dia ao site |  |
| Número de visualizações de página/dia |  |
| Volume (em GB) de transferência de dados/dia |  |
| Número de usuários simultâneos (Grupo de usuários fechado) |  |
| Número de visitantes simultâneos (publicar) |  |
| Número de autores simultâneos |  |
| Número de autores registrados |  |
| Número de ativações de página/dia útil |  |
| Número de ativações de página durante a implantação |  |

## Visão geral das ferramentas potenciais {#overview-of-potential-tools}

A lista a seguir é fornecida para informá-lo sobre as ferramentas que podem ser usadas. Ela é uma introdução, não é uma lista de recomendação extensa, e certamente não deve impedir você de usar quaisquer outros instrumentos que você preferir.

<table>
 <tbody>
  <tr>
   <td><strong>Produto</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>AEM</td>
   <td><p>AEM fornece uma variedade de mecanismos para ajudá-lo a monitorar, testar, investigar e depurar seu aplicativo; incluindo:</p>
    <ul>
     <li><a href="/help/sites-developing/developer-mode.md">Modo de desenvolvedor</a></li>
     <li>O <a href="/help/sites-developing/hobbes.md">Console de Teste</a></li>
     <li><a href="/help/sites-administering/operations-dashboard.md">Painel de operações</a></li>
     <li><a href="/help/sites-authoring/content-insights.md">Content Insight</a></li>
     <li>A <a href="/help/sites-authoring/author-environment-tools.md#content-tree">Árvore de conteúdo</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Selênio</td>
   <td><a href="https://docs.seleniumhq.org/">O </a> Seleniumis é uma ferramenta de teste de código aberto. Os testes são executados diretamente no navegador - emulando como os usuários funcionam.</td>
  </tr>
  <tr>
   <td>Microsoft Project</td>
   <td>Uma ferramenta de gerenciamento de projetos comumente usada.</td>
  </tr>
  <tr>
   <td>Jira</td>
   <td><a href="https://www.atlassian.com/software/jira"></a> Jirais é uma ferramenta de código aberto para rastrear e gerenciar detalhes de bugs de software. Workflows podem ser impostos aos detalhes do bug, conforme necessário.</td>
  </tr>
  <tr>
   <td>Git</td>
   <td><a href="https://git-scm.com/"></a> Gite um software de controle de revisão.</td>
  </tr>
  <tr>
   <td>Eclipse</td>
   <td><p>O Eclipse é um IDE de código aberto, composto por vários projetos. Eles estão voltados para a criação de uma plataforma de desenvolvimento aberta, composta de estruturas, ferramentas e tempos de execução extensíveis para a criação, implantação e gerenciamento de software ao longo do ciclo de vida.</p> <p>Consulte <a href="/help/sites-developing/howto-projects-eclipse.md">Como desenvolver projetos AEM usando o Eclipse</a> para obter mais informações.</p> </td>
  </tr>
  <tr>
   <td>IntelliJ</td>
   <td><p>Um IDE profissional (e, portanto, sujeito aos custos de licenciamento) que oferece uma ampla variedade de recursos. </p> <p>Consulte <a href="/help/sites-developing/ht-intellij.md">Como desenvolver projetos AEM usando o IntelliJ IDEA</a> para obter mais informações.</p> </td>
  </tr>
  <tr>
   <td>Maven</td>
   <td><a href="https://maven.apache.org/">O </a> Mavenis é uma ferramenta de gerenciamento e compreensão de projetos de software que pode gerenciar o processo de construção de um projeto (software e documentação).</td>
  </tr>
 </tbody>
</table>

## Leitura adicional {#further-reading}

Além disso, as seções seguintes são de especial interesse:

* [Introdução](/help/sites-deploying/deploy.md#getting-started)
* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Monitoramento e manutenção da instância](/help/sites-deploying/monitoring-and-maintaining.md)

### Práticas recomendadas     {#best-practices}

O Adobe fornece mais Práticas recomendadas para todas as fases e audiências:

* [Implantação](/help/sites-deploying/best-practices.md)
* [Criação  ](/help/sites-authoring/best-practices.md)
* [Administração](/help/sites-administering/administer-best-practices.md)
* [Desenvolvimento](/help/sites-developing/best-practices.md)
* [Gerenciamento de projeto](/help/managing/best-practices.md)