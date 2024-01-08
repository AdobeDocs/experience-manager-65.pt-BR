---
title: Diretrizes de dimensionamento de hardware
description: Essas diretrizes de dimensionamento oferecem uma aproximação dos recursos de hardware necessários para implantar um projeto AEM.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
docset: aem65
exl-id: 5837ef4f-d4e0-49d7-a671-87d5547e0d98
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '2846'
ht-degree: 0%

---

# Diretrizes de dimensionamento de hardware{#hardware-sizing-guidelines}

Essas diretrizes de dimensionamento oferecem uma aproximação dos recursos de hardware necessários para implantar um projeto AEM. As estimativas de dimensionamento dependem da arquitetura do projeto, da complexidade da solução, do tráfego esperado e dos requisitos do projeto. Este guia ajuda a determinar as necessidades de hardware de uma solução específica ou a encontrar uma estimativa superior e inferior para os requisitos de hardware.

Os fatores básicos a serem considerados são (nesta ordem):

* **Velocidade da rede**

   * Latência de rede
   * Largura de banda disponível

* **Velocidade computacional**

   * Eficiência de armazenamento em cache
   * Tráfego esperado
   * Complexidade de modelos, aplicativos e componentes
   * Autores simultâneos
   * Complexidade da operação de criação (edição simples de conteúdo, implantação do MSM e assim por diante)

* **Desempenho de E/S**

   * Desempenho e eficiência do armazenamento de arquivos ou bancos de dados

* **Disco rígido**

   * pelo menos duas ou três vezes maior que o tamanho do repositório

* **Memória**

   * Tamanho do site (número de objetos de conteúdo, páginas e usuários)
   * Número de usuários/sessões ativos ao mesmo tempo

## Arquitetura {#architecture}

Uma configuração típica do AEM consiste em um autor e um ambiente de publicação. Esses ambientes têm requisitos diferentes em relação ao tamanho do hardware subjacente e à configuração do sistema. As considerações detalhadas para ambos os ambientes estão descritas na seção [ambiente do autor](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations) e [ambiente de publicação](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations) seções.

Em uma configuração de projeto típica, você tem vários ambientes nos quais preparar fases do projeto:

* **Ambiente de desenvolvimento**
Desenvolver novos recursos ou fazer alterações significativas. A prática recomendada é trabalhar usando um ambiente de desenvolvimento por desenvolvedor (instalações locais em seus sistemas pessoais).

* **Ambiente de teste do autor**
Para verificar as alterações. O número de ambientes de teste pode variar dependendo dos requisitos do projeto (por exemplo, separado para controle de qualidade, teste de integração ou teste de aceitação do usuário).

* **Publicar ambiente de teste**
Principalmente para testar casos de uso de colaboração social e/ou a interação entre o autor e várias instâncias de publicação.

* **Ambiente de produção do autor**
Para autores editarem conteúdo.

* **Publicar ambiente de produção**
Para fornecer conteúdo publicado.

Além disso, os ambientes podem variar, desde um sistema de servidor único executando AEM e um servidor de aplicativos até um conjunto altamente dimensionado de instâncias clusterizadas de vários servidores e várias CPUs. A Adobe recomenda que você use um computador separado para cada sistema de produção e que você não execute outros aplicativos nesses computadores.

## Considerações de dimensionamento de hardware genérico {#generic-hardware-sizing-considerations}

As seções abaixo fornecem orientação sobre como calcular os requisitos de hardware, levando em conta várias considerações. Para sistemas grandes, o Adobe sugere que você execute um conjunto simples de testes de desempenho internos em uma configuração de referência.

A otimização de desempenho é uma tarefa fundamental que precisa ser executada antes que qualquer benchmark de um projeto específico possa ser feito. Certifique-se de aplicar o conselho fornecido no [Documentação de otimização de desempenho](/help/sites-deploying/configuring-performance.md) antes de executar qualquer teste de desempenho e usar seus resultados para qualquer cálculo de dimensionamento de hardware.

Os requisitos de dimensionamento de hardware para casos de uso avançados devem se basear em uma avaliação detalhada do desempenho do projeto. As características dos casos de uso avançados que exigem recursos de hardware excepcionais incluem combinações de:

* carga/taxa de transferência de alto conteúdo
* uso abrangente de código personalizado, fluxos de trabalho personalizados ou bibliotecas de software de terceiros
* integração com sistemas externos não compatíveis

### Espaço em disco/disco rígido {#disk-space-hard-drive}

O espaço em disco necessário depende muito do volume e do tipo do aplicativo Web. Os cálculos devem levar em conta o seguinte:

* a quantidade e o tamanho das páginas, dos ativos e de outras entidades armazenadas no repositório, como fluxos de trabalho, perfis etc.
* a frequência estimada de alterações de conteúdo e, portanto, a criação de versões de conteúdo
* o volume de representações de ativos do DAM que será gerado
* o crescimento geral do conteúdo ao longo do tempo

O espaço em disco é monitorado continuamente durante a Limpeza de revisão on-line e off-line. Se o espaço em disco disponível ficar abaixo de um valor crítico, o processo será cancelado. O valor crítico é 25% do espaço em disco atual do repositório e não é configurável. A Adobe recomenda dimensionar o disco pelo menos duas ou três vezes maior que o tamanho do repositório, incluindo o crescimento estimado.

Considere uma configuração de matrizes redundantes de discos independentes (RAID, por exemplo, RAID10) para redundância de dados.

>[!NOTE]
>
>O diretório temporário de uma instância de produção deve ter pelo menos 6 GB de espaço disponível.

#### Virtualização {#virtualization}

O AEM é bem executado em ambientes virtualizados, mas pode haver fatores como CPU ou E/S que não podem ser diretamente comparados ao hardware físico. Uma recomendação é escolher uma velocidade de I/O mais alta (em geral), pois esse é um fator crítico, geralmente. A avaliação comparativa do ambiente é necessária para obter uma compreensão precisa de quais recursos são necessários.

#### Paralelização de instâncias de AEM {#parallelization-of-aem-instances}

**Segurança de falha**

Um site à prova de falhas é implantado em pelo menos dois sistemas separados. Se um sistema falhar, outro sistema poderá assumir o controle e, assim, compensar a falha do sistema.

**Escalabilidade dos recursos do sistema**

Enquanto todos os sistemas estão em execução, um maior desempenho computacional está disponível. Esse desempenho adicional não é necessariamente linear com o número de nós de cluster, pois o relacionamento é altamente dependente do ambiente técnico. Consulte [Documentação do cluster](/help/sites-deploying/recommended-deploys.md) para obter mais informações.

A estimativa de quantos nós de cluster são necessários baseia-se nos requisitos básicos e nos casos de uso específicos do projeto da Web:

* Do ponto de vista da segurança contra falhas, é necessário determinar, para todos os ambientes, o nível crítico de falha e o tempo de compensação com base no tempo necessário para a recuperação de um nó de cluster.
* Para o aspecto da escalabilidade, o número de operações de gravação é basicamente o fator mais importante; consulte [Autores trabalhando em paralelo](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel) para o ambiente de criação e [Social Collaboration](/help/managing/hardware-sizing-guidelines.md#socialcollaborationspecificconsiderations) para o ambiente de publicação. O balanceamento de carga pode ser estabelecido para operações que acessam o sistema apenas para processar operações de leitura; consulte [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR) para obter detalhes.

## Cálculos específicos do ambiente do autor {#author-environment-specific-calculations}

Para fins de benchmark, o Adobe desenvolveu alguns testes de benchmark para instâncias de autor independentes.

* **Teste de referência 1**
Calcule a taxa de transferência máxima de um perfil de carga em que os usuários executam um exercício simples de criação de página sobre uma carga básica de 300 páginas existentes, todas de natureza semelhante. As etapas envolvidas eram fazer logon no site, criar uma página com um SWF e Imagem/Texto, adicionar uma nuvem de tags e ativar a página.

   * **Resultado**
A taxa de transferência máxima para um exercício de criação de página simples, como o acima (considerado como uma transação), foi de 1730 transações/hora.

* **Teste de referência 2**
Calcule a taxa de transferência máxima quando o perfil de carga tiver uma combinação de criação de página nova (10%), modificação de uma página existente (80%) e criação e modificação de uma página em sucessão (10%). A complexidade das páginas permanece a mesma do perfil do teste de benchmark 1. A modificação básica da página é feita adicionando uma imagem e modificando o conteúdo do texto. Novamente, o exercício foi executado sobre uma carga básica de 300 páginas com a mesma complexidade, conforme definido no teste de benchmark 1.

   * **Resultado**
A taxa de transferência máxima para esse cenário de operação de mix foi encontrada em 3252 transações por hora.

>[!NOTE]
>
>A taxa de transferência não distingue entre tipos de transação em um perfil de carga. A abordagem usada para medir o throughput garante que uma proporção fixa de cada tipo de transação seja incluída na carga de trabalho.

Os dois testes acima destacam claramente que o throughput varia de acordo com o tipo de operação. Use as atividades em seu ambiente como base para dimensionar seu sistema. Você obterá uma melhor taxa de transferência com ações menos intensivas, como modificar (o que também é mais comum).

### Armazenamento em cache {#caching}

No ambiente de criação, a eficiência do armazenamento em cache normalmente é muito menor, porque as alterações no site são mais frequentes e também o conteúdo é altamente interativo e personalizado. Usando o Dispatcher, você pode armazenar em cache bibliotecas AEM, arquivos JavaScript, CSS e imagens de layout. Isso acelera alguns aspectos do processo de criação. Configurar o servidor Web para definir cabeçalhos para o cache do navegador nesses recursos também reduz o número de solicitações HTTP e, portanto, melhora a capacidade de resposta do sistema conforme experimentado pelos autores.

### Autores trabalhando em paralelo {#authors-working-in-parallel}

No ambiente de criação, o número de autores que trabalham em paralelo e a carga que suas interações adicionam ao sistema são os principais fatores limitantes. Portanto, a Adobe recomenda dimensionar o sistema com base na taxa de transferência compartilhada de dados.

Para esses cenários, o Adobe executa testes de referência de desempenho em um cluster de dois nós sem compartilhamento de instâncias de autor.

* **Teste de referência 1a**
Com um cluster sem compartilhamento ativo-ativo de 2 instâncias de autor, calcule a taxa de transferência máxima com um perfil de carga em que os usuários executam um exercício de criação de página simples sobre uma carga base de 300 páginas existentes, todas de natureza semelhante.

   * **Resultado**
A taxa de transferência máxima para um exercício de criação de página simples, como o acima, (considerada como uma transação) refere-se a transações de 2016/hora. Isso é um aumento de aproximadamente 16% quando comparado a uma instância de autor independente para o mesmo teste de benchmark.

* **Teste de referência 2b**
Com um cluster sem compartilhamento ativo-ativo de 2 instâncias de autor, calcule a taxa de transferência máxima quando o perfil de carregamento tiver uma combinação de criação de página nova (10%), modificação de uma página existente (80%) e criação e modificação de uma página em sucessão (10%). A complexidade da página permanece a mesma do perfil do teste de benchmark 1. A modificação básica da página é feita adicionando uma imagem e modificando o conteúdo do texto. Novamente, o exercício foi executado sobre uma carga básica de 300 páginas de complexidade, a mesma definida no teste de benchmark 1.

   * **Resultado**
A taxa de transferência máxima para esse cenário de operação mista foi de 6288 transações/hora. Isso é um aumento de aproximadamente 93% quando comparado a uma instância de autor independente para o mesmo teste de benchmark.

>[!NOTE]
>
>A taxa de transferência não distingue entre tipos de transação em um perfil de carga. A abordagem usada para medir o throughput garante que uma proporção fixa de cada tipo de transação seja incluída na carga de trabalho.

Os dois testes acima destacam claramente que o AEM é bem dimensionado para autores que estão realizando operações básicas de edição com AEM. Em geral, o AEM é mais eficaz no dimensionamento de operações de leitura.

Em um site típico, a maioria da criação ocorre durante a fase do projeto. Depois que o site entra em funcionamento, o número de autores trabalhando em paralelo geralmente desce para uma média mais baixa (modo operacional).

Você pode calcular o número de computadores (ou CPUs) necessários para o ambiente de criação da seguinte maneira:

`n = numberOfParallelAuthors / 30`

Essa fórmula pode servir como uma diretriz geral para dimensionar CPUs quando os autores estão executando operações básicas com AEM. Ele pressupõe que o sistema e o aplicativo estejam otimizados. No entanto, a fórmula não será verdadeira para recursos avançados, como MSM ou Ativos (consulte as seções abaixo).

Consulte também [Paralelização](/help/managing/hardware-sizing-guidelines.md#parallelization-of-aem-instances) e [Otimização do desempenho](/help/sites-deploying/configuring-performance.md).

### Recommendations de hardware {#hardware-recommendations}

Normalmente, você pode usar o mesmo hardware para o ambiente de criação que é recomendado para o ambiente de publicação. Normalmente, o tráfego do site é muito menor nos sistemas de criação, mas a eficiência do cache também é menor. No entanto, o fator fundamental aqui é o número de autores trabalhando em paralelo, juntamente com o tipo de ações que estão sendo feitas no sistema. Em geral, o agrupamento de AEM (do ambiente do autor) é mais eficaz no dimensionamento de operações de leitura; em outras palavras, um cluster de AEM é bem dimensionado com autores que estão executando operações básicas de edição.

Os testes de benchmark no Adobe foram executados com o sistema operacional Red Hat® 5.5, em uma plataforma de hardware Hewlett-Packard ProLiant DL380 G5, com a seguinte configuração:

* Duas CPUs Intel Xeon® X5450 de 4 núcleos a 3,00 GHz
* 8 GB de RAM
* Gigabit Ethernet Broadcom NetXtreme II BCM5708
* Controlador RAID HP Smart Array, cache de 256 MB
* Dois discos SAS de 146 GB e 10.000 RPM configurados como um conjunto de distribuição RAID0
* Pontuação do benchmark SPEC CINT2006 Rate é 110

As instâncias de AEM estavam em execução com um tamanho mínimo de heap de 256 M, um tamanho máximo de heap de 1024 M.

## Publicar cálculos específicos de ambiente {#publish-environment-specific-calculations}

### Eficiência e tráfego de cache {#caching-efficiency-and-traffic}

A eficiência do cache é fundamental para a velocidade do site. A tabela a seguir mostra quantas páginas por segundo um sistema AEM otimizado pode lidar com o uso de um proxy reverso, como o Dispatcher:

| Taxa de cache | Páginas/s (pico) | Milhões de páginas/dia (média) |
|---|---|---|
| 100% | 1000-2000 | 35-70 |
| 99% | 910 | 32 |
| 95% | 690 | 25 |
| 90% | 520 | 18 |
| 60% | 220 | 8 |
| 0% | 100 | 3,5 |

>[!CAUTION]
>
>Isenção de responsabilidade: os números são baseados em uma configuração de hardware padrão e podem variar dependendo do hardware específico usado.

A relação de cache é a porcentagem de páginas que o Dispatcher pode retornar sem precisar acessar o AEM. 100% indica que o Dispatcher responde a todas as solicitações, 0% significa que o AEM calcula cada página.

### Complexidade de modelos e aplicativos {#complexity-of-templates-and-applications}

Se você usar modelos complexos, o AEM precisará de mais tempo para renderizar uma página. As páginas retiradas do cache não são afetadas por isso, mas o tamanho da página ainda é relevante ao considerar o tempo de resposta geral. A renderização de uma página complexa pode facilmente levar dez vezes mais tempo do que a renderização de uma página simples.

### Fórmula {#formula}

Usando a seguinte fórmula, você pode calcular uma estimativa da complexidade geral da solução AEM:

`complexity = applicationComplexity + ((1-cacheRatio) * templateComplexity)`

Com base na complexidade, você pode determinar o número de servidores (ou núcleos de CPU) necessários para o ambiente de publicação da seguinte maneira:

`n = (traffic * complexity / 1000 ) * activations`

As variáveis na equação são as seguintes:

<table>
 <tbody>
  <tr>
   <td>tráfego</td>
   <td>O pico de tráfego esperado por segundo. Você pode estimar isso como o número de ocorrências de página por dia, dividido por 35.000.</td>
  </tr>
  <tr>
   <td>applicationComplexity</td>
   <td><p>Use 1 para um aplicativo simples, 2 para um aplicativo complexo ou um valor intermediário:</p>
    <ul>
     <li>1 - um site totalmente anônimo e orientado a conteúdo</li>
     <li>1.1 - um site totalmente anônimo e orientado a conteúdo com personalização do lado do cliente/do Target</li>
     <li>1.5 - um site orientado a conteúdo com seções anônimas e conectadas, personalização do lado do cliente/público-alvo</li>
     <li>1.7 - para um site orientado a conteúdo com seções anônimas e conectadas, personalização do lado do cliente/público-alvo e algum conteúdo gerado pelo usuário</li>
     <li>2 - onde todo o site requer logon, com uso extensivo de conteúdo gerado pelo usuário e várias técnicas de personalização</li>
    </ul> </td>
  </tr>
  <tr>
   <td>cacheRatio</td>
   <td>A porcentagem de páginas que saem do cache do Dispatcher. Use 1 se todas as páginas vierem do cache ou 0 se cada página for calculada pelo AEM.</td>
  </tr>
  <tr>
   <td>templateComplexity</td>
   <td>Use um valor de 1 a 10 para indicar a complexidade dos modelos. Números mais altos indicam modelos mais complexos, usando o valor 1 para sites com uma média de 10 componentes por página, o valor 5 para uma média de páginas de 40 componentes e 10 para uma média de mais de 100 componentes.</td>
  </tr>
  <tr>
   <td>ativações</td>
   <td>Número médio de ativações (replicação de páginas e ativos de tamanho médio do autor para o nível de publicação) por hora dividido por x, em que x é o número de ativações feitas em um sistema sem efeitos colaterais de desempenho para outras tarefas processadas pelo sistema. Também é possível predefinir um valor inicial pessimista como x = 100.<br /> </td>
  </tr>
 </tbody>
</table>

Se você tem um site mais complexo, você também precisa de servidores Web mais potentes para que o AEM possa responder a uma solicitação em um tempo aceitável.

* Complexidade abaixo de 4:
   * RAM JVM de 1024 MB&#42;
   * CPU de baixo a médio desempenho

* Complexidade de 4 a 8:
   * 2048 MB de RAM JVM&#42;
   * CPU de médio a alto desempenho

* Complexidade acima de 8:
   * RAM JVM de 4096 MB&#42;
   * CPU de alto desempenho a alto desempenho

>[!NOTE]
>
>&#42; Reserve RAM suficiente para seu sistema operacional, além da memória necessária para sua JVM.

## Cálculos adicionais específicos de caso de uso {#additional-use-case-specific-calculations}

Além do cálculo de uma aplicação web padrão, talvez seja necessário considerar fatores específicos para os seguintes casos de uso. Os valores calculados devem ser adicionados ao cálculo padrão.

### Considerações específicas de ativos {#assets-specific-considerations}

O processamento extensivo de ativos digitais requer recursos de hardware otimizados. Os fatores mais relevantes são o tamanho da imagem e a taxa de transferência máxima das imagens processadas.

Aloque pelo menos 16 GB de heap e configure o [!UICONTROL Ativo de atualização DAM] fluxo de trabalho para usar o [pacote Camera Raw](/help/assets/camera-raw.md) para a assimilação de imagens brutas.

>[!NOTE]
>
>Um throughput mais alto de imagens significa que os recursos de computação precisam acompanhar o ritmo da E/S do sistema e vice-versa. Por exemplo, se os workflows forem iniciados pela importação de imagens, o upload de muitas imagens via WebDAV poderá causar um backlog de workflows.
>
>O uso de discos separados para TarPM, armazenamento de dados e índice de pesquisa pode ajudar a otimizar o comportamento de I/O do sistema (no entanto, geralmente faz sentido manter o índice de pesquisa localmente).

>[!NOTE]
>
>Consulte também a [Guia de desempenho de ativos](/help/sites-deploying/assets-performance-sizing.md).

### Gerenciador de vários sites {#multi-site-manager}

O consumo de recursos ao usar o AEM MSM em um ambiente de criação depende muito dos casos de uso específicos. Os fatores básicos são:

* Número de Live Copies
* Periodicidade das implantações
* Tamanho da árvore de conteúdo a ser implantada
* Funcionalidade conectada das ações de implantação

Testar o caso de uso planejado com um trecho de conteúdo representativo pode ajudar você a entender melhor o consumo de recursos. Se você extrapolar os resultados com o rendimento planejado, poderá avaliar os recursos adicionais necessários para o MSM AEM.

Além disso, leve em conta os autores que trabalham em paralelo. Eles perceberão os efeitos colaterais do desempenho se os casos de uso de AEM MSM consumirem mais recursos do que o planejado.

### Considerações de dimensionamento do AEM Communities {#aem-communities-sizing-considerations}

Os sites AEM que incluem recursos do AEM Communities (sites da comunidade) têm um alto nível de interação dos visitantes do site (membros) no ambiente de publicação.

As considerações de dimensionamento para um site da comunidade dependem da interação prevista pelos membros da comunidade e se o desempenho ideal para o conteúdo da página é de maior importância.

O conteúdo gerado pelo usuário (UGC) enviado pelos membros é armazenado separadamente do conteúdo da página. Embora a plataforma AEM use um armazenamento de nós que replica o conteúdo do site do autor para a publicação, o AEM Communities usa um armazenamento único e comum para UGC que nunca é replicado.

Para o armazenamento UGC, é necessário escolher um SRP (Storage Resource Provider, provedor de recursos de armazenamento), que influencia a implantação escolhida.
Consulte

* [Armazenamento de conteúdo da comunidade](/help/communities/working-with-srp.md)
* [Topologias recomendadas para comunidades](/help/communities/topologies.md)
