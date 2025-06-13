---
title: Guia de desempenho do Assets
description: Saiba como determinar o dimensionamento ideal de hardware para uma nova configuração do Gerenciamento de ativos digitais (DAM) e como solucionar problemas de desempenho
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
exl-id: fbe15e1b-830b-4752-bd02-0d239a90bc68
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 0%

---

# Guia de desempenho do Assets{#assets-performance-guide}

O Gerenciamento de ativos digitais (DAM) é usado com frequência nos casos em que o desempenho é importante. No entanto, a configuração típica do DAM contém vários componentes de hardware e software que podem afetar o desempenho. Este documento fornece o seguinte:

* Informações para administradores de sistema sobre como determinar o dimensionamento ideal de hardware para uma nova configuração do Gerenciamento de ativos digitais
* Informações para desenvolvedores de software que procuram solucionar problemas de instâncias de DAM com problemas de desempenho

## Problemas de desempenho {#performance-issues}

O baixo desempenho do gerenciamento de ativos digitais pode afetar a experiência do usuário de três maneiras: desempenho interativo, processamento de ativos e velocidade de download. Para melhorar o desempenho, é importante medir o desempenho observado corretamente e estabelecer métricas de destino.

**1. Pesquisa e navegação interativas** Os usuários estão procurando ativos ou navegando no Localizador DAM e reclamam de tempos de resposta lentos ou de que os resultados da pesquisa não são exibidos imediatamente. Esse é um problema de desempenho interativo.

O desempenho interativo é medido em termos de tempo de resposta da página. Esse é o tempo que leva desde o recebimento da solicitação HTTP até o fechamento da resposta HTTP, que pode ser determinado a partir dos arquivos de log da solicitação. O desempenho de destino típico é um tempo de resposta de página abaixo de dois segundos.

**2. Processamento de ativos** Um problema de processamento de ativos ocorre quando usuários estão carregando ativos e leva alguns minutos até que os ativos sejam prontamente convertidos e assimilados no DAM do Adobe Experience Manager (AEM).

O desempenho do processamento de ativos é medido em termos de tempo médio de conclusão do processo de fluxo de trabalho. Esse é o tempo que leva da chamada do processo de fluxo de trabalho Atualização de ativos até sua conclusão, que pode ser determinado a partir da interface do usuário dos relatórios do fluxo de trabalho. O desempenho típico do público-alvo depende do tamanho e do tipo de ativos processados e do número de representações. Exemplos de desempenhos alvo podem ser os seguintes:

* abaixo de dez segundos para imagens menores que 1280x1280 pixels usando representações padrão
* abaixo de um minuto para imagens menores que 100 MB usando representações padrão
* abaixo de cinco minutos para vídeos de alta definição com menos de um minuto

**3. Velocidade de download** Um problema de taxa de transferência ocorre ao baixar do AEM DAM, que demora muito e as miniaturas não são exibidas imediatamente ao navegar pelo Administrador do DAM ou pelo Localizador do DAM.

O desempenho da taxa de transferência é medido em termos de taxa de transferência, em kilobits por segundo. O desempenho normal é de 300 Kbps para 100 downloads simultâneos.

**4. Fatores que influenciam o desempenho de processamento de ativos**

Para estimar qual hardware é necessário para processar ativos, os seguintes aspectos devem ser considerados:

* A resolução de imagens no número de pixels
* O heap atribuído ao processo do AEM

O número de pixels contidos na imagem determina o tempo de processamento - mais pixels significa que o processamento leva mais tempo.
O tipo de imagem, a taxa de compactação ou o tamanho relacionado do arquivo em que a imagem está armazenada não influenciam significativamente o desempenho geral.

O heap foi identificado como o fator de limitação mais importante. Sempre que o ativo exceder a memória livre disponível, o desempenho do processamento cairá rapidamente.

Os processos DAM são adequados para serem executados em paralelo para grandes quantidades. O upload de ativos em um lote e em processadores multi-núcleo acelera o tempo absoluto gasto por ativo.

**5. Estimativa de requisitos de hardware para execução do processamento de ativos**

O processamento extensivo de ativos digitais requer recursos de hardware otimizados. Os fatores mais relevantes são o tamanho da imagem e a taxa de transferência máxima das imagens processadas.

Aloque pelo menos 16 GB de heap e configure o fluxo de trabalho do [!UICONTROL Ativo de atualização do DAM] para usar o [pacote do Camera Raw](/help/assets/camera-raw.md) para a assimilação de imagens brutas.

## Noções básicas do sistema {#understanding-the-system}

Uma configuração típica do DAM consiste em usuários finais acessando o DAM por meio de um balanceador de carga. A instância do DAM pode fazer parte de uma configuração em cluster, em que cada instância do DAM é executada em um processo de máquina virtual Java™ em uma máquina física ou virtual. O armazenamento DAM é fornecido por um disco RAID, se houver configurações de uma única máquina, ou por um armazenamento gerenciado conectado à rede, se houver configurações em cluster.

A legenda a seguir descreve as possíveis áreas de armadilha de desempenho com algumas soluções, conforme apropriado.

**Conexão de rede para o usuário final** Uma conexão de rede lenta pode causar problemas de taxa de transferência e, em alguns casos raros, também problemas de latência. Às vezes, o usuário tem uma conexão lenta do ISP, especialmente em intranets. Este é um sinal de topologia de rede incorreta.

**Sistema de Arquivos Temporário** Um sistema de arquivos local lento pode causar problemas de desempenho interativos, especialmente durante a pesquisa, pois os índices de pesquisa são armazenados no disco local. Isso também poderá causar problemas no processamento de ativos se o processo de linha de comando estiver sendo usado.

**Localizador de DAM do AEM** Problemas de desempenho interativos, geralmente enfrentados em pesquisas, são causados pela alta utilização do CPU devido a muitos usuários simultâneos ou outros processos que consomem o CPU na mesma instância. Migrar de máquinas virtuais para máquinas dedicadas e garantir que nenhum outro serviço seja executado na máquina pode ajudar a melhorar o desempenho. Se a alta carga do CPU for causada pelo processamento de ativos e muitos usuários simultâneos, Day recomenda adicionar outros nós de cluster.

**Fluxo de trabalho do AEM DAM** Processos de fluxo de trabalho de longa duração durante a assimilação de ativos causam problemas de desempenho no processamento de ativos. Dependendo do tipo de ativos que está sendo processado, isso pode indicar a superutilização do CPU. Day recomenda que você reduza o número de outros processos em execução no sistema e aumente o número de CPUs disponíveis adicionando nós de cluster.

**Conectividade NAS** A baixa conectividade de rede com o NAS causa problemas de desempenho interativos, pois o acesso a novos nós durante o processamento de ativos fica lento devido à latência de rede. Além disso, o throughput lento da rede afeta negativamente o throughput, mas também o desempenho do processamento de ativos, pois o carregamento e o salvamento de representações ficam lentos.

Os motivos para a latência e o throughput ruins em um NAS são a topologia da rede ou a superutilização do NAS por outros serviços.

**Armazenamento Conectado à Rede** Sistemas de armazenamento conectado à rede superutilizados podem causar uma matriz de problemas:

* Pouco espaço em disco é um problema encontrado com frequência que pode ser evitado por meio do dimensionamento adequado de um projeto DAM.
* A alta latência de disco se propaga em tempos de acesso lentos para o CRX e pode resultar em problemas interativos de desempenho.
* A baixa taxa de transferência de disco pode resultar em baixo desempenho para o DAM CQ5.

## Teste de desempenho {#testing-for-performance}

Para cada projeto do DAM, certifique-se de estabelecer um regime de teste de desempenho que possa identificar e resolver gargalos rapidamente. Para fazer isso, considere os seguintes pontos de verificação:

1. Testes de desempenho completos usando o JMeter - simulam um exemplo de sessão de pesquisa e navegação para detectar problemas interativos de desempenho.
1. Testes de taxa de transferência e latência usando o JMeter - A execução em um computador cliente garante que não haja problemas relacionados à topologia.
1. Testes de processamento de ativos padronizados - Assimile alguns ativos de exemplo e meça o tempo. Isso deve incluir a integração de workflow externo.
1. Monitore a utilização de CPU, Disco e memória de cada nó de cluster.
1. Diagnóstico de desempenho de leitura/gravação do CRX para identificar problemas relacionados ao não processamento.
1. Monitore a latência e o throughput da rede do cluster DAM para o NAS.
1. Teste, leia e grave o desempenho e a latência de disco diretamente no NAS, se possível.

## Gargalos de Ajuste {#tweaking-bottlenecks}

Os seguintes ajustes de desempenho foram usados em projetos até o momento:

* Geração de representação seletiva: gere apenas as representações necessárias adicionando condições ao fluxo de trabalho de processamento de ativos, para que representações mais caras sejam geradas apenas para ativos selecionados.
* Armazenamento de dados compartilhado entre instâncias: quando há pouco espaço em disco, isso pode reduzir consideravelmente a quantidade de espaço em disco necessária, ao custo de maiores esforços de configuração e da perda da limpeza automática do armazenamento de dados.
