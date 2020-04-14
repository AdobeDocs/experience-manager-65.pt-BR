---
title: 'Diretrizes de dimensionamento do hardware '
seo-title: 'Diretrizes de dimensionamento do hardware '
description: Essas diretrizes de dimensionamento oferta uma aproximação dos recursos de hardware necessários para implantar um projeto do AEM.
seo-description: Essas diretrizes de dimensionamento oferta uma aproximação dos recursos de hardware necessários para implantar um projeto do AEM.
uuid: 395f9869-17c4-4b9b-99f8-d35a44dd6256
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 8893306f-4bc0-48eb-8448-36d0214caddf
docset: aem65
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


# Diretrizes de dimensionamento do hardware{#hardware-sizing-guidelines} 

Essas diretrizes de dimensionamento oferta uma aproximação dos recursos de hardware necessários para implantar um projeto do AEM. Estimativas de dimensionamento dependem da arquitetura do projeto, da complexidade da solução, do tráfego esperado e das necessidades do projeto. Este guia ajuda a determinar as necessidades de hardware de uma solução específica ou a encontrar uma estimativa superior e inferior para os requisitos de hardware.

Os fatores básicos a serem considerados são (nesta ordem):

* **Velocidade da rede**

   * Latência da rede
   * Largura de banda disponível

* **Velocidade computacional**

   * Eficiência do cache
   * Tráfego esperado
   * Complexidade de modelos, aplicativos e componentes
   * Autores simultâneos
   * Complexidade da operação de criação (edição de conteúdo simples, implementação de MSM etc.)

* **Desempenho de E/S**

   * Desempenho e eficiência do armazenamento de arquivo ou banco de dados

* **Disco rígido**

   * pelo menos duas ou três vezes maior que o tamanho do repositório

* **Memória**

   * Tamanho do site (número de objetos de conteúdo, páginas e usuários)
   * Número de usuários/sessões que estão ativos ao mesmo tempo

## Arquitetura {#architecture}

Uma configuração típica do AEM consiste em um autor e um ambiente de publicação. Esses ambientes têm requisitos diferentes em relação ao tamanho do hardware subjacente e à configuração do sistema. As considerações detalhadas para ambos os ambientes são descritas nas seções ambiente [do](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations) autor e [ambiente](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations) de publicação.

Em uma configuração de projeto típica, você tem vários ambientes para preparar fases de projeto:

* **ambiente** para desenvolvimento Para desenvolver novos recursos ou fazer mudanças significativas. A prática recomendada é trabalhar usando um ambiente de desenvolvimento por desenvolvedor (geralmente instalações locais em seus sistemas pessoais).

* **ambiente** de teste do autor Para verificar as alterações. O número de ambientes de teste pode variar de acordo com os requisitos do projeto (por exemplo, separado para controle de qualidade, teste de integração ou teste de aceitação do usuário).

* **Publique o ambiente** de teste principalmente para testar casos de uso de colaboração social e/ou a interação entre o autor e várias instâncias de publicação.

* **ambiente** de produção do autor Para os autores editarem o conteúdo.

* **Publicar ambiente** de produção para servir conteúdo publicado.

Além disso, os ambientes podem variar, desde um sistema de servidor único executando o AEM e um servidor de aplicativos até um conjunto altamente dimensionado de instâncias clusterizadas de várias CPUs e vários servidores. Recomendamos que você use um computador separado para cada sistema de produção e que não execute outros aplicativos nesses computadores.

## Considerações genéricas de dimensionamento de hardware {#generic-hardware-sizing-considerations}

As seções a seguir fornecem orientações sobre como calcular os requisitos de hardware, levando em consideração várias considerações. Para sistemas grandes, sugerimos que você execute um conjunto simples de testes de benchmark internos em uma configuração de referência.

A otimização do desempenho é uma tarefa fundamental que precisa ser realizada antes que qualquer análise comparativa de um projeto específico possa ser feita. Certifique-se de aplicar as recomendações fornecidas na documentação [de Otimização de](/help/sites-deploying/configuring-performance.md) Desempenho antes de executar qualquer teste de benchmark e usar seus resultados para qualquer cálculo de dimensionamento de hardware.

Os requisitos de dimensionamento de hardware para casos de uso avançado precisam ser baseados em uma avaliação detalhada do desempenho do projeto. As características dos casos de uso avançado que exigem recursos de hardware excepcionais incluem combinações de:

* carga / throughput de alto conteúdo
* uso extensivo de código personalizado, workflows personalizados ou bibliotecas de software de terceiros
* integração com sistemas externos não suportados

### Espaço em disco/disco rígido {#disk-space-hard-drive}

O espaço em disco necessário depende muito do volume e do tipo do aplicativo da Web. Os cálculos devem ter em conta:

* a quantidade e o tamanho de páginas, ativos e outras entidades armazenadas no repositório, como workflows, perfis etc.
* a frequência estimada de alterações de conteúdo e, portanto, a criação de versões de conteúdo
* o volume de representações de ativos DAM que serão geradas
* o crescimento global do conteúdo ao longo do tempo

O espaço em disco é monitorado continuamente durante a Limpeza online e offline de revisão. Se o espaço em disco disponível cair abaixo de um valor crítico, o processo será cancelado. O valor crítico é 25% do espaço ocupado em disco atual do repositório e não é configurável. É recomendável dimensionar o disco pelo menos duas ou três vezes maior que o tamanho do repositório, incluindo o crescimento estimado.

Considere uma configuração de storages redundantes de discos independentes (RAID, por exemplo, RAID10) para redundância de dados.

>[!NOTE]
>
>O diretório temporário de uma instância de produção deve ter pelo menos 6 GB de espaço disponível.

#### Virtualização {#virtualization}

O AEM funciona bem em ambientes virtualizados, mas pode haver fatores como CPU ou E/S que não podem ser diretamente equiparados ao hardware físico. Uma recomendação é escolher uma velocidade de E/S mais alta (em geral), pois esse é um fator crítico na maioria dos casos. A análise comparativa do seu ambiente é necessária para se obter uma compreensão precisa dos recursos necessários.

#### Paralelização de instâncias do AEM {#parallelization-of-aem-instances}

**Falha na segurança**

Um site seguro contra falhas é implantado em pelo menos dois sistemas separados. Se um sistema for avariado, outro sistema poderá assumir o controle e, assim, compensar a falha do sistema.

**Escalabilidade dos recursos do sistema**

Enquanto todos os sistemas estão em execução, um desempenho computacional aumentado está disponível. Que o desempenho adicional não é necessariamente linear com o número de nós do cluster, uma vez que a relação é altamente dependente do ambiente técnico; consulte a documentação [do](/help/sites-deploying/recommended-deploys.md) Cluster para obter mais informações.

A estimativa de quantos nós de cluster são necessários baseia-se nos requisitos básicos e nos casos de utilização específicos do projeto Web específico:

* Do ponto de vista da segurança contra falhas, é necessário determinar, para todos os ambientes, o quão crítica é a falha e o tempo de compensação da falha com base no tempo necessário para a recuperação de um nó de cluster.
* Para o aspecto da escalabilidade, o número de operações de gravação é basicamente o fator mais importante; consulte [Autores trabalhando em paralelo](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel) para o ambiente do autor e Colaboração [](/help/managing/hardware-sizing-guidelines.md#socialcollaborationspecificconsiderations) social para o ambiente de publicação. Pode ser estabelecido um equilíbrio de carga para operações que tenham acesso ao sistema exclusivamente para processar operações de leitura; consulte [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) para obter detalhes.

## Cálculos específicos do ambiente do autor {#author-environment-specific-calculations}

Para fins de benchmarking, a Adobe desenvolveu alguns testes de benchmark para instâncias de autor independentes.

* **Teste de benchmark 1** Calcule o throughput máximo de um perfil de carga no qual os usuários executam um simples exercício de criação de página sobre uma carga básica de 300 páginas existentes, todas de natureza semelhante. As etapas envolvidas eram fazer logon no site, criar uma página com um SWF e uma imagem/texto, adicionar uma nuvem de tags e, em seguida, ativar a página.

   * **Resultado** O throughput máximo para um exercício simples de criação de página, como acima (considerado como uma transação), foi encontrado como 1730 transações/hora.

* **Teste de benchmark 2** Calcule o throughput máximo quando o perfil de carga tiver uma combinação de criação de página nova (10%), modificação de uma página existente (80%) e criação e modificação de uma página sucessivamente (10%). A complexidade das páginas permanece a mesma que no perfil do teste de benchmark 1. A modificação básica da página é feita adicionando uma imagem e modificando o conteúdo do texto. Novamente, o exercício foi realizado sobre uma carga de base de 300 páginas da mesma complexidade, conforme definido no teste de referência 1.

   * **Resultado** O throughput máximo para esse cenário de operação de combinação foi de 3252 transações por hora.

>[!NOTE]
>
>A taxa de throughput não distingue entre tipos de transação em um perfil load. A abordagem utilizada para medir o débito garante que uma proporção fixa de cada tipo de transação seja incluída na carga de trabalho.

Os dois testes acima realçam claramente que o débito varia de acordo com o tipo de operação. Use as atividades no seu ambiente como base para dimensionar seu sistema. Você obterá melhor throughput com ações menos intensivas, como modificar (o que também é mais comum).

### Cache {#caching}

No ambiente do autor, a eficiência do cache é geralmente muito menor, porque as alterações no site são mais frequentes e o conteúdo é altamente interativo e personalizado. Usando o dispatcher, você pode armazenar em cache bibliotecas de AEM, JavaScripts, arquivos CSS e imagens de layout. Isso acelera alguns aspectos do processo de criação. Configurar o servidor Web para definir cabeçalhos adicionais para o armazenamento em cache do navegador nesses recursos reduzirá o número de solicitações HTTP e, portanto, melhorará a capacidade de resposta do sistema, conforme experimentado pelos autores.

### Autores trabalhando em paralelo {#authors-working-in-parallel}

No ambiente do autor, o número de autores que trabalham em paralelo e a carga de suas interações agregam ao sistema são os principais fatores limitantes. Portanto, recomendamos que você dimensione seu sistema com base na throughput compartilhada de dados.

Para tais cenários, a Adobe executou testes de benchmark em um cluster de instâncias do autor com dois nós sem compartilhamento.

* **Teste de benchmark 1a** Com um cluster ativo-ativo de nada compartilhado de duas instâncias do autor, calcule o throughput máximo com um perfil load no qual os usuários executam um simples exercício de criação de página sobre uma carga básica de 300 páginas existentes, todas de natureza semelhante.

   * **Resultado** O throughput máximo para um exercício simples de criação de página, como acima, (considerado como uma transação) é 2016 transações/hora. Esse é um aumento de aproximadamente 16% quando comparado a uma instância do autor independente para o mesmo teste de benchmark.

* **Teste de benchmark 2b** Com um cluster de 2 instâncias do autor com compartilhamento ativo-ativo, calcule o throughput máximo quando o perfil de carregamento tiver uma combinação de criação de página nova (10%), modificação de páginas existentes (80%) e criação e modificação de uma página sucessivamente (10%). A complexidade da página permanece a mesma que no perfil do teste de benchmark 1. A modificação básica da página é feita adicionando uma imagem e modificando o conteúdo do texto. Mais uma vez, o exercício foi realizado sobre uma carga de base de 300 páginas de complexidade, a mesma que foi definida no teste de referência 1.

   * **Resultado** A taxa de transferência máxima para um cenário de operação mista desse tipo foi de 6288 transações/hora. Esse é um aumento de aproximadamente 93% quando comparado a uma instância do autor independente para o mesmo teste de benchmark.

>[!NOTE]
>
>A taxa de throughput não distingue entre tipos de transação em um perfil load. A abordagem utilizada para medir o débito garante que uma proporção fixa de cada tipo de transação seja incluída na carga de trabalho.

Os dois testes acima destacam claramente que o AEM é bem dimensionado para autores que executam operações básicas de edição com o AEM. Em geral, o AEM é mais eficaz no dimensionamento de operações de leitura.

Em um site típico, a maioria da criação acontece durante a fase do projeto. Depois que o site entra em funcionamento, o número de autores trabalhando em paralelo geralmente cai para uma média mais baixa (modo operacional).

Você pode calcular o número de computadores (ou CPUs) necessários para o ambiente do autor da seguinte maneira:

`n = numberOfParallelAuthors / 30`

Essa fórmula pode servir como uma diretriz geral para o dimensionamento de CPUs quando os autores executam operações básicas com o AEM. Ele presume que o sistema e o aplicativo estejam otimizados. No entanto, a fórmula não será verdadeira para recursos avançados, como MSM ou Assets (consulte as seções abaixo).

Consulte também os comentários adicionais sobre [Paralelização](/help/managing/hardware-sizing-guidelines.md#parallelization-of-aem-instances) e Otimização [de Desempenho](/help/sites-deploying/configuring-performance.md).

### Recomendações de hardware {#hardware-recommendations}

Geralmente, você pode usar o mesmo hardware para o ambiente do autor que é recomendado para o ambiente de publicação. Normalmente, o tráfego do site é muito menor nos sistemas de criação, mas a eficiência do cache também é menor. No entanto, o fator fundamental aqui é o número de autores que trabalham em paralelo, juntamente com o tipo de ações que estão a ser feitas ao sistema. Em geral, o agrupamento de AEM (do ambiente autor) é mais eficaz para dimensionar operações de leitura; em outras palavras, um cluster do AEM é dimensionado bem com autores que executam operações básicas de edição.

Os testes de benchmark da Adobe foram executados usando o sistema operacional RedHat 5.5, executado em uma plataforma de hardware Hewlett-Packard ProLiant DL380 G5 com a seguinte configuração:

* Duas CPUs Intel Xeon X5450 quad-core a 3,00 GHz
* 8 GB de RAM
* Ethernet Gigabit Broadcom NetXtreme II BCM5708
* Controladora RAID HP Smart Array, cache de 256 MB
* Dois discos SAS de 146 GB e 10.000 RPM configurados como um conjunto de distribuição RAID0
* Pontuação de benchmark SPEC CINT2006 Rate é 110

As instâncias do AEM eram executadas com um tamanho mínimo de heap de 256 M, um tamanho máximo de heap de 1024 M.

## Publicar cálculos específicos do ambiente {#publish-environment-specific-calculations}

### Eficiência de cache e tráfego {#caching-efficiency-and-traffic}

A eficiência do cache é crucial para a velocidade do site. A tabela a seguir mostra quantas páginas por segundo um sistema AEM otimizado pode lidar usando um proxy reverso, como o dispatcher:

| Taxa de cache | Páginas/s (pico) | Milhões de páginas/dia (média) |
|---|---|---|
| 100% | 1000-2000 | 35-70 |
| 99% | 910 | 32 |
| 95% | 690 | 25 |
| 90% | 520 | 18 |
| 60% | 220 | 8 |
| 0% | 100 | 3.5 |

>[!CAUTION]
>
>Isenção de responsabilidade: Os números são baseados em uma configuração de hardware padrão e podem variar dependendo do hardware específico usado.

A taxa de cache é a porcentagem de páginas que o dispatcher pode retornar sem precisar acessar o AEM. 100% indica que o dispatcher responde a todas as solicitações, 0% significa que o AEM calcula cada página.

### Complexidade de modelos e aplicativos {#complexity-of-templates-and-applications}

Se você usar modelos complexos, o AEM precisará de mais tempo para renderizar uma página. As páginas retiradas do cache não são afetadas por isso, mas o tamanho da página ainda é relevante ao considerar o tempo de resposta geral. A renderização de uma página complexa pode levar dez vezes mais tempo do que a renderização de uma página simples.

### Fórmula {#formula}

Usando a seguinte fórmula, você pode calcular uma estimativa para a complexidade geral da sua solução AEM:

`complexity = applicationComplexity + ((1-cacheRatio) * templateComplexity)`

Com base na complexidade, você pode determinar o número de servidores (ou núcleos de CPU) necessários para o ambiente de publicação da seguinte maneira:

`n = (traffic * complexity / 1000 ) * activations`

As variáveis na equação são as seguintes:

<table>
 <tbody>
  <tr>
   <td>tráfego</td>
   <td>O pico de tráfego esperado por segundo. É possível estimar isso como o número de ocorrências de página por dia, dividido por 35.000.</td>
  </tr>
  <tr>
   <td>applicationComplexity</td>
   <td><p>Use 1 para um aplicativo simples, 2 para um aplicativo complexo ou um valor intermediário:</p>
    <ul>
     <li>1 - um site totalmente anônimo e orientado para conteúdo</li>
     <li>1.1 - um site totalmente anônimo e orientado por conteúdo com personalização do cliente/Público alvo</li>
     <li>1.5 - um site orientado a conteúdo com seções anônimas e conectadas, personalização do cliente/Público alvo</li>
     <li>1.7 - para um site orientado a conteúdo com seções anônimas e conectadas, personalização do cliente/Público alvo e algum conteúdo gerado pelo usuário</li>
     <li>2 - onde todo o site requer logon, com uso extensivo de conteúdo gerado pelo usuário e uma variedade de técnicas de personalização</li>
    </ul> </td>
  </tr>
  <tr>
   <td>cacheRatio</td>
   <td>A porcentagem de páginas que saem do cache do dispatcher. Use 1 se todas as páginas vierem do cache ou 0 se cada página for calculada pelo AEM.</td>
  </tr>
  <tr>
   <td>templateComplexity</td>
   <td>Use um valor entre 1 e 10 para indicar a complexidade de seus modelos. Números mais altos indicam modelos mais complexos, usando o valor 1 para sites com uma média de 10 componentes por página, o valor 5 para uma média de página de 40 componentes e 10 para uma média de mais de 100 componentes.</td>
  </tr>
  <tr>
   <td>ativações</td>
   <td>Número de ativações médias (replicação de páginas e ativos de tamanho médio do autor para a camada de publicação) por hora dividido por x, onde x é o número de ativações feitas em um sistema sem efeitos colaterais de desempenho para outras tarefas processadas pelo sistema. Você também pode predefinir um valor inicial pessimista como x = 100.<br /> </td>
  </tr>
 </tbody>
</table>

Se você tiver um site mais complexo, também precisará de servidores da Web mais potentes para que o AEM possa responder uma solicitação em um tempo aceitável.

* Complexidade abaixo de 4:
・ 1024 MB JVM RAM* ・ CPU de baixo a médio desempenho

* Complexidade entre 4 e 8:
・ 2048 MB JVM RAM* ・ meio a CPU de alto desempenho

* Complexidade acima de 8:
・ 4096 MB JVM RAM* ・ CPU de alto a alto desempenho

>[!NOTE]
>
>* Reserve RAM suficiente para seu sistema operacional, além da memória necessária para sua JVM.

## Cálculos adicionais específicos do caso de utilização {#additional-use-case-specific-calculations}

Além do cálculo para um aplicativo da Web padrão, talvez seja necessário considerar fatores específicos para os seguintes casos de uso. Os valores calculados devem ser adicionados ao cálculo padrão.

### Considerações específicas dos ativos {#assets-specific-considerations}

O processamento abrangente de ativos digitais requer recursos de hardware otimizados, os fatores mais relevantes são o tamanho da imagem e o pico de throughput das imagens processadas.

Aloque pelo menos 16 GB de heap e configure o fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM para usar o pacote [do](/help/assets/camera-raw.md) Camera Raw para a ingestão de imagens brutas.

>[!NOTE]
Um throughput mais alto de imagens significa que os recursos de computação precisam acompanhar o ritmo da E/S do sistema e vice-versa. Por exemplo, se os workflows forem iniciados pela importação de imagens, o upload de muitas imagens via WebDAV pode causar um backlog de workflows.
O uso de discos separados para TarPM, armazenamento de dados e índice de pesquisa pode ajudar a otimizar o comportamento de E/S do sistema (no entanto, normalmente faz sentido manter o índice de pesquisa localmente).

>[!NOTE]
Consulte também o Guia [de desempenho dos](/help/sites-deploying/assets-performance-sizing.md)ativos.

### Gerenciador de vários sites {#multi-site-manager}

O consumo de recursos ao usar o AEM MSM em um ambiente de criação depende muito dos casos de uso específicos. Os fatores básicos são:

* Número de Live-Copies
* Periodicidade dos lançamentos
* Tamanho da árvore de conteúdo a ser distribuído
* Funcionalidade conectada das ações de implantação

Testar o caso de uso planejado com um trecho de conteúdo representativo pode ajudá-lo a entender melhor o consumo de recursos. Se você extrapolar os resultados com o throughput planejado, poderá avaliar os recursos adicionais necessários para o AEM MSM.

Considere também que os autores trabalhando em paralelo perceberão os efeitos colaterais do desempenho se os casos de uso do AEM MSM consumirem mais recursos do que o planejado.

### Considerações sobre o dimensionamento do AEM Communities {#aem-communities-sizing-considerations}

Os sites AEM que incluem recursos do AEM Communities (sites da comunidade) experimentam um alto nível de interação de visitantes do site (membros) no ambiente de publicação.

As considerações de dimensionamento para um site da comunidade dependem da interação esperada dos membros da comunidade e se o desempenho ideal para o conteúdo da página é de maior importância.

O conteúdo gerado pelo usuário (UGC) é armazenado separadamente do conteúdo da página. Enquanto a plataforma AEM usa uma loja de nós que replica o conteúdo do site do autor para a publicação, o AEM Communities usa uma única loja comum para UGC que nunca é replicada.

Para a loja UGC, é necessário escolher um provedor de recursos do armazenamento (SRP), que influencia a implantação escolhida.
Consulte

* [Armazenamento de conteúdo da comunidade](/help/communities/working-with-srp.md)
* [Topologias recomendadas para comunidades](/help/communities/topologies.md)

