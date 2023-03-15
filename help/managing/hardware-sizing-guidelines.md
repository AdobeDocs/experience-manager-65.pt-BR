---
title: Diretrizes de dimensionamento do hardware
seo-title: Hardware Sizing Guidelines
description: Essas diretrizes de dimensionamento oferecem uma aproximação dos recursos de hardware necessários para implantar um projeto de AEM.
seo-description: These sizing guidelines offer an approximation of the hardware resources required to deploy an AEM project.
uuid: 395f9869-17c4-4b9b-99f8-d35a44dd6256
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 8893306f-4bc0-48eb-8448-36d0214caddf
docset: aem65
exl-id: 5837ef4f-d4e0-49d7-a671-87d5547e0d98
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2816'
ht-degree: 0%

---

# Diretrizes de dimensionamento do hardware {#hardware-sizing-guidelines}

Essas diretrizes de dimensionamento oferecem uma aproximação dos recursos de hardware necessários para implantar um projeto de AEM. As estimativas de dimensionamento dependem da arquitetura do projeto, da complexidade da solução, do tráfego esperado e das necessidades do projeto. Este guia ajuda você a determinar as necessidades de hardware de uma solução específica ou a encontrar uma estimativa superior e inferior para os requisitos de hardware.

Os fatores básicos a serem considerados são (nesta ordem):

* **Velocidade da rede**

   * Latência da rede
   * Largura de banda disponível

* **Velocidade computacional**

   * Eficiência do armazenamento em cache
   * Tráfego esperado
   * Complexidade de modelos, aplicativos e componentes
   * Autores simultâneos
   * Complexidade da operação de criação (edição de conteúdo simples, implantação do MSM etc.)

* **Desempenho de E/S**

   * Desempenho e eficiência do armazenamento de arquivos ou banco de dados

* **Disco rígido**

   * pelo menos duas ou três vezes maior que o tamanho do repositório

* **Memória**

   * Tamanho do site (número de objetos de conteúdo, páginas e usuários)
   * Número de usuários/sessões que estão ativas ao mesmo tempo

## Arquitetura {#architecture}

Uma configuração de AEM típica consiste em um autor e um ambiente de publicação. Esses ambientes têm requisitos diferentes em relação ao tamanho de hardware subjacente e à configuração do sistema. As considerações detalhadas para ambos os ambientes estão descritas na seção [ambiente do autor](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations) e [ambiente de publicação](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations) seções.

Em uma configuração de projeto típica, você tem vários ambientes em que preparar fases do projeto:

* **Ambiente de desenvolvimento**
Desenvolver novos recursos ou fazer alterações significativas. A prática recomendada é trabalhar usando um ambiente de desenvolvimento por desenvolvedor (geralmente instalações locais em seus sistemas pessoais).

* **Ambiente de teste do autor**
Para verificar as alterações. O número de ambientes de teste pode variar dependendo dos requisitos do projeto (por exemplo, separado para controle de qualidade, teste de integração ou teste de aceitação do usuário).

* **Publicar ambiente de teste**
Principalmente para testar casos de uso de colaboração social e/ou a interação entre autor e várias instâncias de publicação.

* **Ambiente de produção do autor**
Para autores editarem conteúdo.

* **Publicar ambiente de produção**
Para veicular conteúdo publicado.

Além disso, os ambientes podem variar, desde um sistema de servidor único executando AEM e um servidor de aplicativos até um conjunto altamente dimensionado de instâncias em cluster de vários servidores e várias CPU. Recomendamos que você use um computador separado para cada sistema de produção e que não execute outros aplicativos nesses computadores.

## Considerações genéricas de dimensionamento de hardware {#generic-hardware-sizing-considerations}

As seções abaixo fornecem orientação sobre como calcular os requisitos de hardware, levando em conta várias considerações. Para sistemas grandes, sugerimos que você execute um conjunto simples de testes de benchmark internos em uma configuração de referência.

A otimização de desempenho é uma tarefa fundamental que precisa ser executada antes que qualquer aferição de desempenho de um projeto específico possa ser feita. Por favor, certifique-se de que aplica as recomendações fornecidas no [Documentação de Otimização de desempenho](/help/sites-deploying/configuring-performance.md) antes de executar qualquer teste de benchmark e usar seus resultados para qualquer cálculo de dimensionamento de hardware.

Os requisitos de dimensionamento de hardware para casos de uso avançado devem basear-se em uma avaliação detalhada do desempenho do projeto. As características de casos de uso avançado que exigem recursos de hardware excepcionais incluem combinações de:

* carga / taxa de transferência de alto conteúdo
* uso extensivo de código personalizado, fluxos de trabalho personalizados ou bibliotecas de software de terceiros
* integração com sistemas externos não compatíveis

### Espaço em disco/disco rígido {#disk-space-hard-drive}

O espaço em disco necessário depende muito do volume e do tipo do aplicativo Web. Os cálculos devem ter em conta:

* a quantidade e o tamanho de páginas, ativos e outras entidades armazenadas no repositório, como fluxos de trabalho, perfis etc.
* a frequência estimada de alterações de conteúdo e, portanto, a criação de versões de conteúdo
* o volume de representações de ativos DAM que serão geradas
* o crescimento global do conteúdo ao longo do tempo

O espaço em disco é continuamente monitorado durante a Limpeza de Revisão Online e Offline. Se o espaço em disco disponível cair abaixo de um valor crítico, o processo será cancelado. O valor crítico é 25% do espaço ocupado pelo disco atual do repositório e não é configurável. Recomenda-se dimensionar o disco pelo menos duas ou três vezes maior que o tamanho do repositório, incluindo o crescimento estimado.

Considere uma configuração de arrays redundantes de discos independentes (RAID, por exemplo RAID10) para redundância de dados.

>[!NOTE]
>
>O diretório temporário de uma instância de produção deve ter pelo menos 6 GB de espaço disponível.

#### Virtualização {#virtualization}

AEM funciona bem em ambientes virtualizados, mas pode haver fatores como CPU ou E/S que não podem ser diretamente equiparados ao hardware físico. Uma recomendação é escolher uma velocidade de E/S mais alta (em geral), pois esse é um fator crítico na maioria dos casos. A aferição comparativa do seu ambiente é necessária para obter uma compreensão precisa de quais recursos serão necessários.

#### Paralelização de instâncias AEM {#parallelization-of-aem-instances}

**Falha de segurança**

Um site seguro contra falhas é implantado em pelo menos dois sistemas separados. Se um sistema for avariado, outro sistema poderá assumir o controle e, assim, compensar a falha do sistema.

**Escalabilidade dos recursos do sistema**

Enquanto todos os sistemas estão em execução, um maior desempenho computacional está disponível. Esse desempenho adicional não é necessariamente linear com o número de nós de cluster, pois o relacionamento é altamente dependente do ambiente técnico; consulte o [Documentação do cluster](/help/sites-deploying/recommended-deploys.md) para obter mais informações.

A estimativa de quantos nós de cluster são necessários baseia-se nos requisitos básicos e em casos de uso específicos do projeto Web específico:

* Do ponto de vista da segurança contra falhas, é necessário determinar, para todos os ambientes, o quão crítica é a falha e o tempo de compensação da falha com base no tempo necessário para um nó de cluster se recuperar.
* Para o aspecto da escalabilidade, o número de operações de gravação é basicamente o fator mais importante; see [Autores trabalhando em paralelo](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel) para o ambiente do autor e [Colaboração social](/help/managing/hardware-sizing-guidelines.md#socialcollaborationspecificconsiderations) para o ambiente de publicação. O equilíbrio da carga pode ser estabelecido para as operações que acessam o sistema unicamente para processar operações de leitura; see [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) para obter detalhes.

## Cálculos específicos do ambiente de criação {#author-environment-specific-calculations}

Para fins de avaliação de desempenho, o Adobe desenvolveu alguns testes de referência para instâncias de autor independentes.

* **Ensaio de referência 1**
Calcule a taxa de transferência máxima de um perfil de carregamento em que os usuários executam um exercício de página de criação simples sobre uma carga básica de 300 páginas existentes, tudo de natureza semelhante. As etapas envolvidas foram fazer logon no site, criar uma página com um SWF e uma Imagem/Texto, adicionar uma nuvem de tags e, em seguida, ativar a página.

   * **Resultado**
A taxa de transferência máxima para um exercício de criação de página simples como o acima (considerado como uma transação) foi de 1730 transações/hora.

* **Ensaio de referência 2**
Calcule a taxa de transferência máxima quando o perfil de carregamento tiver uma combinação de criação de página nova (10%), modificação de uma página existente (80%) e criação e modificação de uma página em sucessão (10%). A complexidade das páginas permanece a mesma do perfil do teste de referência 1. A modificação básica da página é feita adicionando uma imagem e modificando o conteúdo do texto. Novamente, o exercício foi realizado sobre uma carga de base de 300 páginas da mesma complexidade, conforme definido no teste de benchmark 1.

   * **Resultado**
A taxa de transferência máxima para esse cenário de operação de combinação foi de 3252 transações por hora.

>[!NOTE]
>
>A taxa de transferência não diferencia os tipos de transação dentro de um perfil de carregamento. A abordagem utilizada para medir a taxa de transferência garante que uma proporção fixa de cada tipo de transação seja incluída na carga de trabalho.

Os dois testes acima destacam claramente que a taxa de transferência varia de acordo com o tipo de operação. Use as atividades em seu ambiente como base para dimensionar seu sistema. Você obterá melhor throughput com ações menos intensivas, como modificar (o que também é mais comum).

### Armazenamento em cache {#caching}

No ambiente de criação, a eficiência do armazenamento em cache normalmente é muito menor, porque as alterações no site são mais frequentes e também o conteúdo é altamente interativo e personalizado. Com o dispatcher, é possível armazenar em cache AEM bibliotecas, JavaScripts, arquivos CSS e imagens de layout. Isso acelera alguns aspectos do processo de criação. Configurar o servidor da Web para definir cabeçalhos adicionais para o armazenamento em cache do navegador nesses recursos reduzirá o número de solicitações HTTP e, portanto, melhorará a capacidade de resposta do sistema, conforme experimentado pelos autores.

### Autores trabalhando em paralelo {#authors-working-in-parallel}

No ambiente de criação, o número de autores que trabalham em paralelo e o carregamento de suas interações somam ao sistema são os principais fatores limitantes. Portanto, recomendamos que você dimensione seu sistema com base na taxa de transferência compartilhada de dados.

Para esses cenários, o Adobe executou testes de benchmark em um cluster de duas instâncias de autor sem compartilhamento.

* **Ensaio de referência 1a**
Com um cluster ativo-ativo de nada compartilhado de duas instâncias do autor, calcule a taxa de transferência máxima com um perfil de carregamento em que os usuários executam um exercício de página de criação simples sobre um carregamento básico de 300 páginas existentes, tudo de natureza semelhante.

   * **Resultado**
A taxa de transferência máxima para um exercício de criação de página simples, como acima, (considerado como uma transação) é transações/hora de 2016. Esse é um aumento de aproximadamente 16% em comparação a uma instância de autor independente para o mesmo teste de benchmark.

* **Ensaio de referência 2b**
Com um cluster ativo-ativo de nada compartilhado de duas instâncias do autor, calcule a taxa de transferência máxima quando o perfil de carregamento tiver uma combinação de criação de página nova (10%), modificação de uma página existente (80%) e criação e modificação de uma página em sucessão (10%). A complexidade da página permanece a mesma do perfil do teste de benchmark 1. A modificação básica da página é feita adicionando uma imagem e modificando o conteúdo do texto. Novamente, o exercício foi realizado sobre uma carga de base de 300 páginas de complexidade igual à definida no teste de benchmark 1.

   * **Resultado**
A taxa de transferência máxima para esse cenário de operação mista foi de 6288 transações por hora. Esse é um aumento de aproximadamente 93% em comparação a uma instância de autor independente para o mesmo teste de benchmark.

>[!NOTE]
>
>A taxa de transferência não diferencia os tipos de transação dentro de um perfil de carregamento. A abordagem utilizada para medir a taxa de transferência garante que uma proporção fixa de cada tipo de transação seja incluída na carga de trabalho.

Os dois testes acima destacam claramente que o AEM é dimensionado bem para autores que estão realizando operações básicas de edição com AEM. Em geral, AEM é mais eficaz em operações de leitura de escala.

Em um site típico, a maioria da criação acontece durante a fase do projeto. Depois que o site entra em funcionamento, o número de autores trabalhando em paralelo geralmente cai para uma média mais baixa (modo operacional).

Você pode calcular o número de computadores (ou CPUs) necessários para o ambiente do autor da seguinte maneira:

`n = numberOfParallelAuthors / 30`

Essa fórmula pode servir como diretriz geral para dimensionar CPUs quando os autores estão executando operações básicas com o AEM. Ele pressupõe que o sistema e o aplicativo estejam otimizados. No entanto, a fórmula não será verdadeira para recursos avançados, como MSM ou Assets (consulte as seções abaixo).

Veja também os comentários adicionais em [Paralelização](/help/managing/hardware-sizing-guidelines.md#parallelization-of-aem-instances) e [Otimização de desempenho](/help/sites-deploying/configuring-performance.md).

### Recommendations de hardware {#hardware-recommendations}

Geralmente, você pode usar o mesmo hardware para o ambiente de criação recomendado para o seu ambiente de publicação. Normalmente, o tráfego de site é muito menor nos sistemas de criação, mas a eficiência do cache também é menor. No entanto, o fator fundamental aqui é o número de autores trabalhando em paralelo, juntamente com o tipo de ações que estão sendo feitas no sistema. Em geral, o clustering de AEM (do ambiente do autor) é mais eficaz em escalar operações de leitura; em outras palavras, um cluster AEM é bem dimensionado com autores que estão executando operações básicas de edição.

Os testes de benchmark no Adobe foram realizados com o sistema operacional RedHat 5.5, executado em uma plataforma de hardware Hewlett-Packard ProLiant DL380 G5 com a seguinte configuração:

* Duas CPUs Intel Xeon X5450 quad-core a 3,00 GHz
* 8 GB de RAM
* Ethernet Gigabit Broadcom NetXtreme II BCM5708
* Controlador RAID HP Smart Array, cache de 256 MB
* Dois discos SAS de 146 GB e 10.000 RPM configurados como um conjunto de distribuição RAID0
* Pontuação de benchmark da taxa SPEC CINT2006 é 110

AEM instâncias estavam sendo executadas com um tamanho de heap mínimo de 256M, um tamanho de heap máximo de 1024M.

## Publicar cálculos específicos do ambiente {#publish-environment-specific-calculations}

### Eficiência de armazenamento em cache e tráfego {#caching-efficiency-and-traffic}

A eficiência do cache é fundamental para a velocidade do site. A tabela a seguir mostra quantas páginas por segundo um sistema de AEM otimizado pode lidar usando um proxy reverso, como o dispatcher:

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

A proporção do cache é a porcentagem de páginas que o dispatcher pode retornar sem precisar acessar AEM. 100% indica que o dispatcher responde a todas as solicitações, 0% significa que AEM calcula cada página.

### Complexidade de modelos e aplicativos {#complexity-of-templates-and-applications}

Se você usar modelos complexos, AEM precisará de mais tempo para renderizar uma página. As páginas obtidas do cache não são afetadas por isso, mas o tamanho da página ainda é relevante ao considerar o tempo de resposta geral. A renderização de uma página complexa pode facilmente demorar dez vezes mais do que a renderização de uma página simples.

### Fórmula {#formula}

Usando a seguinte fórmula, você pode calcular uma estimativa para a complexidade geral da sua solução de AEM:

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
     <li>1.1 - um site totalmente anônimo e orientado para conteúdo com personalização do lado do cliente/Target</li>
     <li>1.5 - um site orientado a conteúdo com seções anônimas e conectadas, personalização do cliente/Target</li>
     <li>1.7 - para um site orientado a conteúdo com seções anônimas e conectadas, personalização do lado do cliente/Target e algum conteúdo gerado pelo usuário</li>
     <li>2 - onde todo o site requer logon, com uso extensivo de conteúdo gerado pelo usuário e uma variedade de técnicas de personalização</li>
    </ul> </td>
  </tr>
  <tr>
   <td>cacheRatio</td>
   <td>A porcentagem de páginas que saem do cache do dispatcher. Use 1 se todas as páginas vierem do cache ou 0 se cada página for calculada pelo AEM.</td>
  </tr>
  <tr>
   <td>templateComplexity</td>
   <td>Use um valor entre 1 e 10 para indicar a complexidade de seus modelos. Os números mais altos indicam modelos mais complexos, usando o valor 1 para sites com uma média de 10 componentes por página, o valor 5 para uma média de página de 40 componentes e 10 para uma média de mais de 100 componentes.</td>
  </tr>
  <tr>
   <td>ativações</td>
   <td>Número de ativações médias (replicação de páginas e ativos de tamanho médio do autor para o nível de publicação) por hora dividido por x, onde x é o número de ativações feitas em um sistema sem efeitos colaterais de desempenho para outras tarefas processadas pelo sistema. Você também pode predefinir um valor inicial pessimista como x = 100.<br /> </td>
  </tr>
 </tbody>
</table>

Se você tiver um site mais complexo, também precisará de servidores da Web mais potentes para que o AEM possa responder uma solicitação em um tempo aceitável.

* Complexidade inferior a 4: ・ 1024 MB de RAM JVM&#42;
・ CPU de baixo a médio desempenho

* Complexidade entre 4 e 8: ・ 2048 MB JVM RAM&#42;
・ CPU de médio a alto desempenho

* Complexidade acima de 8: ・ 4096 MB de RAM JVM&#42;
・ CPU de alto a alto desempenho

>[!NOTE]
>
>&#42; Reserve RAM suficiente para seu sistema operacional, além da memória necessária para sua JVM.

## Cálculos adicionais específicos de caso de uso {#additional-use-case-specific-calculations}

Além do cálculo para uma aplicação web padrão, talvez seja necessário considerar fatores específicos para os seguintes casos de uso. Os valores calculados devem ser adicionados ao cálculo padrão.

### Considerações específicas sobre ativos {#assets-specific-considerations}

O processamento abrangente de ativos digitais requer recursos de hardware otimizados, os fatores mais relevantes são o tamanho da imagem e o pico de throughput das imagens processadas.

Aloque pelo menos 16 GB de heap e configure a variável [!UICONTROL Ativo de atualização DAM] para usar o [Pacote Camera Raw](/help/assets/camera-raw.md) para a assimilação de imagens brutas.

>[!NOTE]
>
>Um throughput mais alto de imagens significa que os recursos de computação precisam ser capazes de acompanhar o ritmo da E/S do sistema e vice-versa. Por exemplo, se os workflows forem iniciados pela importação de imagens, o upload de muitas imagens via WebDAV poderá causar um backlog de workflows.
>
>O uso de discos separados para TarPM, armazenamento de dados e índice de pesquisa pode ajudar a otimizar o comportamento de E/S do sistema (no entanto, geralmente faz sentido manter o índice de pesquisa localmente).

>[!NOTE]
>
>Consulte também a [Guia de desempenho de ativos](/help/sites-deploying/assets-performance-sizing.md).

### Gerenciador de vários sites {#multi-site-manager}

O consumo de recursos ao usar AEM MSM em um ambiente de criação depende muito dos casos de uso específicos. Os fatores básicos são:

* Número de Live Copies
* Periodicidade das implantações
* Tamanho da árvore de conteúdo a ser implantada
* Funcionalidade conectada das ações de implantação

Testar o caso de uso planejado com um trecho de conteúdo representativo pode ajudá-lo a entender melhor o consumo de recursos. Se você extrapolar os resultados com o throughput planejado, poderá avaliar os recursos adicionais necessários para o MSM AEM.

Considere também que os autores que trabalham em paralelo perceberão os efeitos colaterais do desempenho se AEM casos de uso de MSM consumirem mais recursos do que o planejado.

### Considerações sobre o dimensionamento do AEM Communities {#aem-communities-sizing-considerations}

AEM sites que incluem recursos do AEM Communities (sites da comunidade) experimentam um alto nível de interação de visitantes do site (membros) no ambiente de publicação.

As considerações de dimensionamento para um site da comunidade dependem da interação esperada pelos membros da comunidade e se o desempenho ideal para o conteúdo da página é de maior importância.

O conteúdo gerado pelo usuário (UGC) enviado pelos membros é armazenado separadamente do conteúdo da página. Embora a plataforma de AEM use uma loja de nós que replica o conteúdo do site do autor para publicar, o AEM Communities usa uma única loja comum para UGC que nunca é replicada.

Para o armazenamento UGC, é necessário escolher um provedor de recursos de armazenamento (SRP), que influencia a implantação escolhida.
Consulte

* [Armazenamento de conteúdo da comunidade](/help/communities/working-with-srp.md)
* [Topologias recomendadas para comunidades](/help/communities/topologies.md)
