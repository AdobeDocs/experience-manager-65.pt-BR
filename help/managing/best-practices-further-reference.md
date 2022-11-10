---
title: Lista de verificação - mais referência
seo-title: The Checklist - Further Reference
description: Saiba mais sobre detalhes que desenvolvem e/ou aumentam os documentos e princípios abordados pela Lista de verificação de gerenciamento de projetos - práticas recomendadas.
seo-description: Learn about further details that elaborate on and/or augment the documents and principles covered by the Managing Projects - Best Practices Checklist.
uuid: 58a8b4ab-e447-4a12-b9e9-4cd3db11e06a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist
content-type: reference
discoiquuid: 6fc2751e-f42a-4519-bc8c-695057f21b69
exl-id: 36620e3e-ecdf-4062-bbef-65513362d691
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '3755'
ht-degree: 2%

---

# Lista de verificação - mais referência{#the-checklist-further-reference}

Esta página fornece mais detalhes para elaborar e/ou aumentar os documentos e princípios cobertos pela [Gerenciamento de projetos - Lista de verificação de práticas recomendadas](/help/managing/best-practices.md).

## AEM - O que você usará? {#aem-what-will-you-be-using}

>[!CAUTION]
>
>As listas desta subseção não são exaustivas, mas destinam-se a uma introdução.

### Recursos no AEM {#features-within-aem}

Ao implementar AEM (especialmente pela primeira vez), será necessário revisar a variável [recursos e fluxos de trabalho de AEM](https://www.adobe.com/br/marketing/experience-manager.html) para ter certeza de quais áreas você deseja/precisa.

Considere os recursos de AEM que você usará e o impacto em seu design; por exemplo:

* [Commerce](/help/commerce/cif-classic/administering/ecommerce.md)
* [Screens](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=pt-BR)
* [Assets](/help/assets/assets.md)
* [Tags](/help/sites-administering/tags.md)
* [Gerenciamento e tradução de vários sites](/help/sites-administering/msm-and-translation.md)
* [Forms](/help/forms/home.md)
* [Communities](/help/communities/deploy-communities.md)
* [Livefyre](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)

Além disso, verifique o [Notas de versão](/help/release-notes/release-notes.md), para as várias versões do AEM, para ver quando novos recursos foram adicionados.

### Integrações {#integrations}

AEM pode ser integrado a outros produtos de Adobe e/ou serviços de terceiros. Isso pode aumentar a potência e a funcionalidade à sua disposição.

Consulte [Integração de soluções](/help/sites-administering/integration.md) para obter informações completas.

## Migrar ou atualizar? {#migrate-or-upgrade}

Uma consideração importante é se você deseja:

* Atualize a instalação existente no local.
* Migre o conteúdo do sistema atual para uma nova instalação nova e nova.

Ao migrar de uma versão anterior para a atual, há duas opções:

* Use o [Gerenciador de pacotes](/help/sites-administering/package-manager.md) para exportar todo o conteúdo e o código do aplicativo do sistema antigo para o novo.
* [Atualizar](/help/sites-deploying/upgrade.md) o sistema antigo no local. Essa é a opção recomendada na maioria dos casos.

## Regras básicas de base {#basic-ground-rules}

Tal como acontece com qualquer projeto, é fundamental estabelecer regras básicas o mais rapidamente possível. Dentre elas:

>[!NOTE]
>
>Esses pontos são genéricos, a variável [Lista de verificação de práticas recomendadas](/help/managing/best-practices.md) trata de especificações relacionadas a AEM.

* **Funções**

   Estes devem ser claramente definidos e comunicados a todos os participantes no projeto. Além disso, é conveniente destacar:

   * Tomadores de decisão
   * Pontos de Contato

* **Responsabilidades**

   * Para cada função, uma definição clara das responsabilidades relacionadas ao seu projeto ajuda a evitar confusão.

* **Envolvimento**

   Ao envolver as partes interessadas o mais rapidamente possível, pode incentivá-las a *partes interessadas* no projeto, aumentando assim o seu compromisso para com o seu sucesso.

   * No lado do cliente, isso inclui os autores - que terão de trabalhar com o sistema diariamente.
   * No âmbito da sua equipe de projeto, esta incluirá também as pessoas responsáveis pelo controlo de qualidade. Quanto mais eles entenderem as necessidades do cliente, melhor poderão planejar os testes.

* **Caminhos de comunicação**

   * Embora estas não devam ser excessivamente formalizadas, as definições específicas devem assegurar que as pessoas-chave sejam sempre informadas e, por conseguinte, atualizadas. Deve ser dada especial atenção à comunicação com as partes externas.

* **Processos**

   Os processos a serem definidos dependerão do projeto individual. Mais uma vez, tente manter esses itens simples, considerando:

   * Definir processos (e vias de comunicação) para interagir com terceiros; Por exemplo, agências de concepção e fornecedores de software de terceiros, entre outros.
   * Geralmente, o cliente terá seus próprios procedimentos e ferramentas de Gerenciamento de projetos e Relatórios .

* **Ferramentas de rastreamento**

   Há muitas ferramentas disponíveis para rastrear informações sobre bugs, tarefas e outros aspectos do seu projeto - consulte [Visão geral de ferramentas potenciais](#overview-of-potential-tools) para obter mais detalhes.

   * O ponto principal a ser observado aqui é manter apenas uma cópia das informações e compartilhar as informações (e, portanto, acessar a ferramenta usada). Isso facilitará a manutenção e ajudará a evitar discrepâncias.

* **Escopo**

   Definir claramente o que deve ser abrangido pelo projeto a vários níveis:

   * as versões individuais (se um processo de versão iterativa for usado e independentemente de serem entregues aos clientes ou à sua equipe de teste interna).
   * o projeto AEM.
   * todo o projeto; incluindo qualquer software de terceiros, seu impacto em testes, problemas organizacionais e muitos outros.
   * Em certos aspectos, também pode ser útil indicar o que é *not* no âmbito do projeto. Tal pode contribuir para evitar confusões e pressupostos incorretos, embora deva limitar-se a questões essenciais.

* **Relatório**

   Defina claramente quais informações você reportará, de que forma, com que frequência e para quem.

* **Terminologia**

   * Defina qualquer abreviação e/ou terminologia específica do cliente a ser usada.

* **Pressupostos**

   * Defina as suposições que estão sendo feitas.

Estas informações podem ser definidas no Manual do Projeto; o uso de um Wiki também pode ajudar a garantir que as mudanças em curso sejam tratadas com eficiência. Sempre que estes forem definidos, os principais fatores são os seguintes:

* As informações são definidas e mantidas
* As informações são claramente comunicadas a todas as pessoas em causa. Embora a prática padrão do Gerenciamento de projetos não possa ser repetida com frequência suficiente para que uma definição clara de função e uma boa comunicação possam tornar ou quebrar um projeto.
* Apenas é conservada uma versão das informações que são objeto de acompanhamento; por exemplo, rastreamento de erros, rastreamento de problemas etc.

## Principais indicadores de desempenho e métricas de meta {#key-performance-indicators-and-target-metrics}

As organizações usam os Indicadores-chave de desempenho (KPIs) para avaliar seu sucesso em atingir metas. Estes indicadores são valores mensuráveis que podem ser utilizados para demonstrar a eficácia do cumprimento de objetivos específicos.

Esses indicadores podem ser:

* Negócios:

   * Usado para medir objetivos-chave de negócios.
   * É importante escolher os KPIs apropriados para sua empresa/cenário com definições claras do que são, como serão medidos, como serão usados e por quem.

* Show:

   * Defina como medir o desempenho do sistema.
   * Alguns exemplos incluem tempo de carregamento de página, tempo de resposta do servidor e desempenho de consulta do banco de dados.

Alguns indicadores, mas não todos, podem se basear nas métricas de meta que você identificar e definir.

### Métricas de meta {#target-metrics}

As métricas são usadas para definir medidas quantitativas para a qualidade de seu site - são basicamente uma definição das metas de desempenho que você deseja alcançar e que podem ser usadas para definir sua [KPIs (Principais indicadores de desempenho)](#key-performance-indicators-and-target-metrics).

Muitas métricas podem ser definidas, mas muitas vezes as que você define cobrem suas metas de desempenho e simultaneidade. Em especial, fatores que podem ser difíceis de quantificar e que são frequentemente susceptíveis de *emocional* avaliação:

* &quot;nosso site é *muito lento* hoje&quot; - quando *lento* qualificar?

* &quot;tudo *parada* quando meu colega faz logon&quot; - quantos usuários simultâneos o sistema pode suportar?
* &quot;quando pesquisar, o sistema *parada* &quot; - que tipo de solicitações de pesquisa estão afetando o sistema?
* &quot;é necessário *ages* para baixar o arquivo&quot; - quais são os tempos de download aceitáveis (em condições normais de rede)?

As Métricas de destino são definidas no início de um projeto para:

* indicar as dimensões esperadas do site que você oferecerá
* indica a qualidade mínima que deseja alcançar
* definir como esses fatores serão realmente medidos
* como base para a [Principais indicadores de desempenho](#key-performance-indicators-and-target-metrics)

Como sempre, é necessário ter cuidado ao definir as métricas de destino:

* se estiver definido como muito alto, pode ser completamente inatingível
* se definido como flutuações muito baixas, pode não ser realçado
* para garantir que possam ser medidos de forma repetida e consistente
* proporcionar um equilíbrio entre os diferentes fatores que estão a ser medidos
* determinadas métricas se relacionarão a um ambiente de teste, mas algumas devem refletir os cenários da vida real, pois devem ser mensuráveis e reprodutíveis, no seu site em produção
* priorizar as métricas de acordo com sua significância para o site
* limitar as métricas a um conjunto que possa ser realisticamente monitorado

Durante o desenvolvimento do projeto, podem ser atualizadas e ajustadas conforme adequado. Depois que o projeto for implementado com êxito, eles poderão ser usados para ajudá-lo a controlar sua instalação e monitorar/manter os níveis de serviço necessários para a operação contínua.

Quando usadas adequadamente, essas métricas podem fornecer uma ferramenta útil; quando utilizados de forma irresponsável, podem ser uma distração que desperdiça tempo. Como sempre, você precisa entender o que está medindo, como está medindo e por quê.

>[!NOTE]
>
>A presente seção aborda os princípios básicos e as questões a considerar. Cada instalação é diferente, então os valores reais a serem medidos serão diferentes.

### Tudo depende do design do projeto {#everything-rests-on-your-project-design}

Todas as métricas a serem medidas serão, de alguma forma, afetadas pelo design do seu projeto. Por outro lado, muitos problemas serão melhor resolvidos por meio de alterações de design.

Portanto, você deve definir suas métricas de meta *before* decisão sobre seu design. Isso permite otimizar seu design com base nesses fatores. Uma vez desenvolvido o seu projeto, será difícil introduzir alterações nos princípios básicos de concepção.

Ao criar a estrutura para o site, siga a estrutura recomendada para AEM sites. Certifique-se de entender os seguintes problemas e/ou princípios:

* Como estruturar o conteúdo do site.
* Como os modelos e componentes funcionam.
* Como o armazenamento em cache funciona.
* Os impactos do conteúdo personalizado.
* Como a função de pesquisa funciona.
* Como você pode usar o CSS e as tecnologias relacionadas para criar um código de HTML compacto e não redundante.

Se você achar que o seu design não segue as diretrizes ou se não tiver certeza sobre algumas das implicações, clarifique essas questões antes de iniciar a fase de programação ou de preencher o conteúdo.

### Infraestrutura {#infrastructure}

Para definir ou avaliar a infraestrutura, ajudará a definir valores-alvo, como:

* visitantes/dia; média e pico
* ocorrências/dia; média e pico
* número de páginas web que estão sendo disponibilizadas
* volume de conteúdo da Web

Dependendo da sua situação e do significado estratégico do site, isso ajudará você a avaliar e escolher sua infraestrutura:

* número de servidores
* número de instâncias AEM (autor e publicação)

### Show {#performance}

Há vários fatores de desempenho que podem ser avaliados:

* tempos de resposta para páginas individuais, levando em conta:

   * tempos de resposta em um ambiente do autor
   * tempos de resposta no ambiente de publicação

* tempos de resposta para solicitações de pesquisa

Esta seção pode ser lida juntamente com [Otimização de desempenho](/help/sites-deploying/configuring-performance.md) que amplia os detalhes técnicos de realmente medir o desempenho.

#### Tempos de resposta para páginas individuais {#response-times-for-individual-pages}

Um problema importante é o tempo que seu site leva para responder às solicitações do visitante.

Embora esse valor varie para cada solicitação, um valor médio de público-alvo pode ser definido. Uma vez que esse valor seja comprovadamente alcançável e sustentável, ele poderá ser usado para monitorar o desempenho do site e indicar o desenvolvimento de possíveis problemas

Diferentes metas em ambientes de criação e publicação

Os tempos de resposta que você desejará serão diferentes nos ambientes de criação e publicação, refletindo o público-alvo:

* **Ambiente de criação**

   Esse ambiente é usado pelos autores que inserem e atualizam o conteúdo, portanto, deve:

   * atenda a um pequeno número de usuários que geram um alto número de solicitações ao atualizar páginas de conteúdo e os elementos individuais nessas páginas
   * seja o mais rápido possível para maximizar a produtividade para obter o conteúdo em seu site

* **Ambiente de publicação**

   Esse ambiente contém conteúdo que você disponibiliza para seus usuários:

   * a velocidade ainda é vital, mas é muitas vezes mais lenta do que um ambiente do autor
   * são frequentemente aplicados mecanismos adicionais de melhoria do desempenho:

      * o conteúdo é armazenado em cache
      * O balanceamento de carga é aplicado

#### Definição dos tempos de resposta do target {#setting-target-response-times}

Então, como você pode decidir sobre tempos de resposta (médios) alcançáveis? Geralmente, isso é uma questão de experiência:

* experiência passada no seu site
* experiência com AEM
* reconhecer páginas complexas que têm tempos de resposta acima da média (elas devem ser otimizadas individualmente, se possível)

Contudo, (em circunstâncias controladas), podem ser aplicadas as seguintes orientações:

* 70% das solicitações de páginas devem responder em menos de 100 ms.
* 25% das solicitações de páginas devem responder em menos de 100 ms a 300 ms.
* 4% das solicitações de páginas devem responder em menos de 300 ms a 500 ms.
* 1% das solicitações de páginas devem responder em menos de 500 ms-1000 ms.
* Nenhuma página deve responder mais lentamente do que 1 segundo.

Os números acima assumem as seguintes condições:

* medido na publicação (sem ambiente de criação e/ou sobrecarga de CFC)
* medido no servidor (sem sobrecarga de rede)
* não armazenado em cache (sem cache de saída AEM, sem cache do Dispatcher)
* somente para itens complexos com muitas dependências (HTML, JS, PDF, ...)
* nenhuma outra carga no sistema

Há vários mecanismos que você pode usar para monitorar os tempos de resposta:

* **Monitoramento dos tempos de resposta com o AEM request.log**

   Um bom ponto de partida para análise de desempenho é o log de solicitação. Entre outras informações, você pode usar isso para ver os tempos de resposta de solicitações individuais. Consulte [Otimização de desempenho](/help/sites-deploying/configuring-performance.md) para obter mais detalhes.

* **Monitoramento dos tempos de resposta com comentários do HTML**

   Os comentários do HTML podem ser usados para incluir informações do tempo de resposta na origem de cada página:

   `</body> </html>v <-- Page took 58 milliseconds to be rendered by the server --> Response times for search requests`

#### Solicitações de pesquisa {#search-requests}

As solicitações de pesquisa podem ter um impacto significativo no seu site, em termos de:

* Tempo de resposta da pesquisa real

   * Uma função de pesquisa rápida é uma meta de qualidade para o seu site

* Impacto no desempenho geral

   * Como uma função de pesquisa deve verificar (potencialmente grande) seções do conteúdo ou um índice extraído especialmente, isso pode afetar o desempenho de todo o sistema se não for otimizado

Definir alvos para solicitações de pesquisa é, novamente, uma questão de experiência, dependendo de:

* experiência de AEM
* uma avaliação da frequência com que a pesquisa será usada em comparação com outros objetivos
* seu gerenciador de persistência
* seu índice de pesquisa
* a complexidade da sua função de pesquisa; uma função de pesquisa básica que permite que somente um termo de pesquisa seja inserido será mais rápida que uma pesquisa avançada, permitindo que o usuário crie instruções de pesquisa complexas usando AND/OR/NOT.

Eles devem ser planejados e integrados desde o início do seu projeto. Os mecanismos disponíveis para a monitorização incluem:

* **Monitorar os tempos de resposta da pesquisa com o AEM request.log**

   Novamente, o request.log pode ser usado para monitorar os tempos de resposta das solicitações de pesquisa; see [Otimização de desempenho](/help/sites-deploying/configuring-performance.md) para obter mais detalhes.

* **Mecanismos programados para medir os tempos de resposta da pesquisa**

   Para personalizar as informações coletadas sobre as solicitações de pesquisa e seu desempenho, é recomendável incluir a coleta de informações no código-fonte do projeto; see [Otimização de desempenho](/help/sites-deploying/configuring-performance.md) para obter mais detalhes.

### Simultaneidade {#concurrency}

Seu site será disponibilizado para vários usuários/visitantes, nos ambientes de criação e publicação. Geralmente, os números são mais altos do que você usou no teste, mas também flutuantes e difíceis de prever. Seu site precisará ser projetado para um número médio de usuários/visitantes simultâneos sem notar um impacto negativo no desempenho. Novamente, a variável `request.log` podem ser utilizados para efetuar testes de simultaneidade; see [Otimização de desempenho](/help/sites-deploying/configuring-performance.md) para obter mais detalhes.

As metas para o número de usuários simultâneos dependem do tipo de ambiente:

* **Ambiente de criação**

   * Geralmente, o número de usuários simultâneos pode ser estimado com precisão. Você saberá quantos autores tem no total, no entanto (provavelmente) nem todos estarão ativos ao mesmo tempo.

* **Ambiente de publicação**

   * Isso é mais difícil de prever, portanto, você deve selecionar um valor de meta. Novamente, isso deve se basear na experiência do seu site atual, juntamente com expectativas realistas do seu novo site.
   * Eventos especiais (por exemplo, quando você publica conteúdo novo e muito popular) podem exceder as expectativas, ou até mesmo os recursos (como por vezes reportado na imprensa quando ingressos para determinados eventos são disponibilizados para venda).

### Capacidade e volume {#capacity-and-volume}

Antes de discutir as métricas relacionadas, uma definição rápida dos termos:

* **Volume**

   * A quantidade de saída que é processada e entregue pelo sistema.

* **Capacidade**

   * A capacidade do sistema de fornecer o volume.
   * Em cada etapa, a capacidade e o volume são medidos de forma diferente, conforme mostrado na tabela abaixo. Para obter o melhor desempenho, verifique se a capacidade corresponde ao volume em cada etapa e se a capacidade e o volume são compartilhados em todas as etapas. Por exemplo, você pode ser capaz de calcular a navegação no computador cliente ou colocá-la no cache, em vez de computá-la no servidor para cada solicitação.

* **Capacidade e volume**

   | O que / Onde | Capacidade | Volume |
   |---|---|---|
   | Cliente | Potência computacional do computador do usuário. | Complexidade do layout da página. |
   | Rede | Largura de banda de rede. | Tamanho da página (código, imagens e assim por diante). |
   | Cache do Dispatcher | Memória do servidor Web (memória principal e disco rígido). | Servidor Web (memória principal e disco rígido). Número e tamanho das páginas em cache. |
   | Cache de saída | Memória do servidor AEM (memória principal e disco rígido). | Número e tamanho das páginas no cache de saída, o número de dependências por página. O cache do dispatcher baixa esse volume. |
   | Servidor Web | Potência computacional do servidor Web. | Quantidade de solicitações. O armazenamento em cache reduz esse volume. |
   | Modelo | Potência computacional do servidor Web. | Complexidade dos modelos. |
   | Repositório | Desempenho do repositório. | Número de páginas carregadas do repositório. |

### Outras métricas {#other-metrics}

As seções anteriores detalham as métricas principais a serem definidas.

Dependendo das suas necessidades específicas, pode ser útil definir métricas adicionais, isoladamente ou levando em conta as classificações acima.

No entanto, é preferível ter um pequeno conjunto de métricas principais e precisas que funcionam de forma fácil e confiável, em vez de tentar medir e definir cada aspecto do seu site. Por sua natureza, seu site começará a mudar e evoluir assim que for entregue aos usuários.

## Segurança {#security}

A segurança é crucial e um desafio cada vez maior. It ***must*** ser considerada e planejada desde as primeiras etapas do projeto.

O [Lista de verificação de segurança](/help/sites-administering/security-checklist.md) detalha as etapas que você deve tomar para garantir que sua instalação do AEM seja segura quando implantada. Outros aspectos de segurança são abrangidos por [Segurança (ao desenvolver)](/help/sites-developing/security.md) e [Administração e segurança do usuário](/help/sites-administering/security.md).

## Tarefas paralelas e iterativas {#parallel-and-iterative-tasks}

>[!NOTE]
>
>O seguinte:
>
>* Oferece uma visão geral relacionada ao *first* Implementação de um projeto AEM.
>* Destina-se a uma visão geral abstrata; consulte o [Lista de verificação do projeto](/help/managing/best-practices.md) para fases/etapas/tarefas específicas.
>* Qualquer escala de tempo é teórica.
>


Para uma nova implementação de um projeto de AEM padrão, você precisará considerar tarefas como:

* Transferir do processo de vendas.
* Implementação do aplicativo do cliente (**Desenvolvimento**).
* Instalação e configuração da infraestrutura (e processos relacionados) no local do cliente (**Infraestrutura**).
* Criação (ou migração) do conteúdo (**Conteúdo**).
* Transferir para operações (**Manutenção/suporte**).
* Versões de acompanhamento.

![chlimage_1-2](assets/chlimage_1-2.png)

Para todos os aspectos, é recomendável usar uma abordagem iterativa:

![chlimage_1-3](assets/chlimage_1-3.png)

>[!NOTE]
>
>Divida o lançamento do projeto em **Lançamento(s) suave(s)** (disponibilidade reduzida, várias iterações) e **Inicialização forçada** (disponibilidade total - ao vivo) para permitir o ajuste, a otimização e a formação dos utilizadores em condições realistas no ambiente de produção.

>[!NOTE]
>
>Consulte a [Lista de verificação do projeto](/help/managing/best-practices.md) para obter exemplos de tarefas que você deve executar (ou avaliar) durante o ciclo de vida do seu projeto.

Alguns pontos a serem observados para cada categoria são:

* **Desenvolvimento**

   * Defina a arquitetura base primeiro.
   * Use várias iterações (gravações) para desenvolvimento:

      * A primeira impressão equivale ao primeiro ciclo completo de desenvolvimento.
      * A primeira etapa resulta na primeira implantação no ambiente de teste.
      * Todas as fontes têm um resultado que pode ser executado.
      * Cada fonte recebe uma aprovação do cliente (mínimo de teste estruturado com feedback).
   * Plano para a eventualidade de uma atualização da versão AEM disponível durante o projeto.
   * Plano de testes e otimização durante as impressões.
   * Plano para as fases de estabilização e otimização.
   * Crie um log de itens a serem planejados para outras versões.
   * Plano de participação e transferência dos parceiros.


* **Infraestrutura**

   * Defina a arquitetura base primeiro:

      * Defina os requisitos de desempenho.
      * Defina as metas de desempenho (ou seja, defina claramente as expectativas).
      * Definir a arquitetura de hardware e infraestrutura; incluindo dimensionamento.
      * Defina a implantação.
   * Usar várias iterações; para a primeira configuração inicial e de configuração inicial, prepare:

      * Ambiente de desenvolvimento.
      * Processo de desenvolvimento.
      * Ambiente de teste.
      * Processo de implantação (incluindo gerenciamento de configuração).
   * Planejar vários testes de carga.
   * Plano de testes e otimização durante as impressões.
   * Plano para uma fase de estabilização e otimização.
   * Implante no ambiente de produção o mais rápido possível (deixe que a equipe de operações configure o sistema para ganhar experiência).
   * Use usuários nomeados e funções definidas o mais rápido possível.
   * Plano de treinamento (por exemplo, treinamento de administrador).
   * Plano de entrega para operações.



* **Conteúdo**

   * A arquitetura básica:
      * Direciona a hierarquia de conteúdo.
      * Ajuda a definir o conceito de conteúdo.
      * Define o uso e o layout do MSM.
      * Define funções, grupos, fluxos de trabalho e permissões.
   * Considere se a criação de página offline será útil.
   * Plano para a criação antecipada de primeiras páginas e conteúdo (para uso em testes e feedback).
   * Plano de migração de conteúdo existente.
   * Plano de &quot;migração automática&quot; após a refatoração.
   * Planejar &quot;detalhamento de conteúdo&quot; (mapa do site para conteúdo ativo).

## Estimando o tempo e o esforço {#estimating-time-and-effort}

Dependendo da lista de tarefas resultante, é possível fazer estimativas iniciais de tempo e esforço para definições de tarefas (de alto nível). Isso deve incluir uma indicação de quem (cliente ou parceiro) fará o que e quando.

A lista a seguir mostra aproximações padrão e inter-relações de esforço envolvidas e, portanto, custos:

>[!CAUTION]
>
>Estes valores só podem ser utilizados para estimativas iniciais. Um desenvolvedor de AEM experiente deve fazer a análise detalhada.

| Fase | Esforço |
|---|---|
| Desenvolvimento | Uma estimativa aproximada de 2 a 4 horas para cada nó do componente cobrirá todos os requisitos de desenvolvimento. |
| Teste do desenvolvedor | 15% do Desenvolvimento |
| Acompanhamento | 10% do Desenvolvimento |
| Documentação | 15% do Desenvolvimento |
| Documentação do JavaDoc | 10% do Desenvolvimento |
| Correção de erros | 15% do Desenvolvimento |
| Gerenciamento de projeto | 20% dos custos do projeto para a gestão e governação de projetos em curso |

O planeamento detalhado pode então relacionar os recursos disponíveis ou necessários com prazos e custos.

## Arquitetura de referência {#reference-architecture}

A arquitetura de referência é fornecida para fornecer uma solução de modelo para a arquitetura de AEM. A arquitetura de referência soluciona problemas comuns encontrados para sistemas corporativos, incluindo dimensionamento, confiabilidade e segurança.

As seguintes métricas do site devem ser definidas:

| Classificação | Definição |
|---|---|
| Número de sítios Internet |  |
| Número de sites da intranet |  |
| Número de bases de código (por exemplo, se a Internet e a intranet forem diferentes) |  |
| Número de páginas individuais |  |
| Número de visitas ao site/dia |  |
| Número de exibições de página/dia |  |
| Volume (em GB) de transferência de dados/dia |  |
| Número de usuários simultâneos (grupo de usuários fechado) |  |
| Número de visitantes simultâneos (publicação) |  |
| Número de autores simultâneos |  |
| Número de autores registrados |  |
| Número de ativações de página/dia útil |  |
| Número de ativações de página durante a implantação |  |

## Visão geral de ferramentas potenciais {#overview-of-potential-tools}

A lista a seguir é fornecida para informá-lo sobre as ferramentas que podem ser usadas. Trata-se de uma introdução, não de uma lista de recomendações extensa, e certamente não deve dissuadi-lo de utilizar quaisquer outros instrumentos que preferir.

<table>
 <tbody>
  <tr>
   <td><strong>Produto</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>AEM</td>
   <td><p>O AEM fornece uma variedade de mecanismos para ajudá-lo a monitorar, testar, investigar e depurar seu aplicativo; incluindo:</p>
    <ul>
     <li><a href="/help/sites-developing/developer-mode.md">Modo de desenvolvedor</a></li>
     <li>O <a href="/help/sites-developing/hobbes.md">Console de teste</a></li>
     <li><a href="/help/sites-administering/operations-dashboard.md">Painel de operações</a></li>
     <li><a href="/help/sites-authoring/content-insights.md">Content Insight</a></li>
     <li>O <a href="/help/sites-authoring/author-environment-tools.md#content-tree">Árvore de conteúdo</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Selênio</td>
   <td><a href="https://docs.seleniumhq.org/">Selênio</a> O é uma ferramenta de teste Open Source. Os testes são executados diretamente no navegador, emulando o funcionamento dos usuários.</td>
  </tr>
  <tr>
   <td>Projeto Microsoft</td>
   <td>Uma ferramenta de gerenciamento de projeto comumente usada.</td>
  </tr>
  <tr>
   <td>Jira</td>
   <td><a href="https://www.atlassian.com/software/jira">Jira</a> O é uma ferramenta de fonte aberta para rastrear e gerenciar detalhes de seus bugs de software. Os workflows podem ser impostos aos detalhes do bug, conforme necessário.</td>
  </tr>
  <tr>
   <td>Git</td>
   <td><a href="https://git-scm.com/">Git</a> é um software de controle de revisão.</td>
  </tr>
  <tr>
   <td>Eclipse</td>
   <td><p>O Eclipse é um IDE de código aberto, composto de vários projetos. Eles se concentram na criação de uma plataforma de desenvolvimento aberta composta de estruturas, ferramentas e tempos de execução extensíveis para a criação, implantação e gerenciamento de software durante todo o ciclo de vida.</p> <p>Consulte <a href="/help/sites-developing/howto-projects-eclipse.md">Como desenvolver projetos AEM usando o Eclipse</a> para obter mais informações.</p> </td>
  </tr>
  <tr>
   <td>IntelliJ</td>
   <td><p>Um IDE profissional (e, portanto, responsável pelos custos de licenciamento) que oferece uma ampla gama de recursos. </p> <p>Consulte <a href="/help/sites-developing/ht-intellij.md">Como desenvolver projetos AEM usando o IntelliJ IDEA</a> para obter mais informações.</p> </td>
  </tr>
  <tr>
   <td>Maven</td>
   <td><a href="https://maven.apache.org/">Maven</a> é uma ferramenta de gerenciamento e compreensão de projetos de software que pode gerenciar o processo de criação de um projeto (software e documentação).</td>
  </tr>
 </tbody>
</table>

## Leitura adicional {#further-reading}

Além disso, são de especial interesse as seguintes seções:

* [Introdução](/help/sites-deploying/deploy.md#getting-started)
* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Monitoramento e manutenção da instância](/help/sites-deploying/monitoring-and-maintaining.md)

### Práticas recomendadas     {#best-practices}

O Adobe fornece mais Práticas recomendadas para todas as fases e públicos-alvo:

* [Implantação](/help/sites-deploying/best-practices.md)
* [Criação  ](/help/sites-authoring/best-practices.md)
* [Administração](/help/sites-administering/administer-best-practices.md)
* [Desenvolvimento](/help/sites-developing/best-practices.md)
* [Gerenciamento de projeto](/help/managing/best-practices.md)
