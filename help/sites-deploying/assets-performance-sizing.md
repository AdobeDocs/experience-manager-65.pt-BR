---
title: Guia de desempenho de ativos
seo-title: Guia de desempenho de ativos
description: Saiba como determinar o dimensionamento ideal de hardware para uma nova configuração do Gerenciamento de ativos digitais (DAM) e como solucionar problemas de desempenho
seo-description: Saiba como determinar o dimensionamento ideal de hardware para uma nova configuração do Gerenciamento de ativos digitais (DAM) e como solucionar problemas de desempenho
uuid: 8291c5b9-c543-41cf-8754-445826200930
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: a79839e2-be39-418b-a3bd-f5457e555172
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


# Guia de desempenho de ativos{#assets-performance-guide}

A gestão de ativos digitais é frequentemente utilizada em casos em que o desempenho é importante; no entanto, a configuração típica do DAM contém vários componentes de hardware e software que podem afetar o desempenho. Este documento fornece o seguinte:

* Informações para administradores de sistema sobre como determinar o dimensionamento ideal de hardware para uma nova configuração do Gerenciamento de ativos digitais
* Informações para desenvolvedores de software que procuram resolver problemas de instâncias de DAM com problemas de desempenho

## Problemas de desempenho {#performance-issues}

O baixo desempenho no gerenciamento de ativos digitais pode afetar a experiência do usuário de três formas: desempenho interativo, processamento de ativos e velocidade de download. Para melhorar o desempenho, é importante medir o desempenho observado corretamente e estabelecer métricas de público alvo.

**1. Pesquisas interativas e navegação** Os usuários estão pesquisando ativos ou navegando no DAM Finder e reclamam dos tempos de resposta lentos ou que os resultados da pesquisa não são exibidos imediatamente. Este é um problema de desempenho interativo.

O desempenho interativo é medido em termos de tempo de resposta da página. Esse é o tempo que leva desde o recebimento da solicitação HTTP até o fechamento da resposta HTTP, que pode ser determinado a partir dos arquivos de registro da solicitação. O desempenho típico do público alvo é um tempo de resposta da página abaixo de dois segundos.

**2. Processamento** de ativos Um problema de processamento de ativos é quando os usuários estão fazendo upload de ativos e demora minutos até que os ativos sejam imediatamente convertidos e assimilados no AEM DAM.

O desempenho do processamento do ativo é medido em termos do tempo médio de conclusão do processo do fluxo de trabalho. Esse é o tempo que leva desde a chamada do processo de fluxo de trabalho de atualização de ativos até sua conclusão, que pode ser determinado a partir da interface do usuário dos relatórios de fluxo de trabalho. O desempenho típico do público alvo depende do tamanho e do tipo dos ativos processados e do número de execuções. Exemplos de desempenho do público alvo podem ser os seguintes:

* menos de dez segundos para imagens menores que 1280x1280 pixels usando execuções padrão
* abaixo de um minuto para imagens menores que 100 MB usando execuções padrão
* menos de cinco minutos para clipes de vídeo de alta definição com menos de um minuto

**3. Velocidade** de download Um problema de throughput é que o download do AEM DAM demora e as miniaturas não aparecem imediatamente ao navegar pelo DAM Admin ou pelo DAM Finder.

O desempenho da throughput é medido em termos da taxa de download em kilobits por segundo. O desempenho típico do público alvo é de 300 kilobits por segundo para 100 downloads simultâneos.

**4. Fatores que influenciam o desempenho do processamento de ativos**

Para poder estimar o hardware necessário para processar ativos, os seguintes aspectos precisam ser levados em consideração:

* A resolução das imagens em quantidade de pixels
* O heap atribuído ao processo do AEM

A quantidade de pixels contidos na imagem determina o tempo de processamento - mais pixels significa que o processamento leva um tempo maior.
O tipo de imagem, a taxa de compactação ou o tamanho relacionado do arquivo no qual a imagem é armazenada não influencia significativamente o desempenho geral.

A pilha foi identificada como o fator limitante mais importante. Sempre que o ativo excede a memória livre disponível, o desempenho do processamento cai rapidamente.

Os processos DAM são adequados para serem executados em paralelo para grandes quantidades. Fazer upload de ativos em um lote e em processadores de vários núcleos acelera o tempo absoluto gasto por ativo.

**5. Avaliando os requisitos de hardware para executar o processamento de ativos**

O processamento abrangente de ativos digitais requer recursos de hardware otimizados, os fatores mais relevantes são o tamanho da imagem e o pico de throughput das imagens processadas.

Aloque pelo menos 16 GB de heap e configure o fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM para usar o pacote [do](/help/assets/camera-raw.md) Camera Raw para a ingestão de imagens brutas.

## Como entender o sistema {#understanding-the-system}

Uma configuração típica de DAM consiste em usuários finais acessando o DAM por meio de um balanceador de carga. A instância do DAM pode ser parte de uma configuração clusterizada, em que cada instância do DAM é executada em um processo de máquina virtual Java em uma máquina física ou em uma máquina virtual. O armazenamento DAM é fornecido por um disco RAID nos casos de configurações de uma única máquina ou por um armazenamento conectado à rede gerenciado no caso de configurações agrupadas.

A seguinte legenda descreve as possíveis áreas de desempenho com algumas soluções, conforme apropriado.

**Conexão de rede ao usuário** final Uma conexão de rede lenta pode causar problemas de throughput, em alguns casos raros, também problemas de latência. Às vezes, o usuário tem uma conexão lenta do ISP, especialmente em intranets. Este é um sinal de topologia de rede incorreta.

**Sistema** de arquivos temporário Um sistema de arquivos local lento pode causar problemas de desempenho interativos, especialmente quando se trata de pesquisa, porque os índices de pesquisa são armazenados no disco local. Além disso, pode causar problemas de processamento de ativos se o processo da linha de comando estiver sendo usado.

**AEM DAM Finder** Problemas de desempenho interativos, frequentemente enfrentados em pesquisas, são causados pela alta utilização da CPU devido a muitos usuários simultâneos ou outros processos que consomem a CPU na mesma instância. Mover de máquinas virtuais para máquinas dedicadas e garantir que nenhum outro serviço seja executado na máquina pode ajudar a melhorar o desempenho. Se a alta carga da CPU for causada pelo processamento de ativos e por muitos usuários simultâneos, o Day recomenda a adição de nós de cluster adicionais.

**Fluxo de trabalho** do AEM DAM Processos de fluxo de trabalho de longa duração durante a ingestão de ativos causam problemas de desempenho de processamento de ativos. Dependendo do tipo de ativos que estão sendo processados, isso pode indicar sobre-utilização da CPU. O dia recomenda que você reduza o número de outros processos em execução no sistema e aumente o número de CPUs disponíveis adicionando nós de cluster.

**Conectividade** NAS A falta de conectividade da rede com o NAS causa problemas de desempenho interativos, porque o acesso a novos nós durante o processamento de ativos é retardado devido à latência da rede. Além disso, a throughput lenta da rede afeta negativamente a throughput, mas também o desempenho do processamento de ativos, pois o carregamento e a gravação de representações é retardado.

Motivos para latência e throughput ruins em um NAS são geralmente topologia de rede ou superutilização de NAS por outros serviços.

**Armazenamento** conectado à rede Sistemas armazenamentos conectados à rede usados em excesso podem causar uma série de problemas:

* Pouco espaço em disco é um problema encontrado com frequência que pode ser evitado por meio do dimensionamento adequado de um projeto DAM.
* A alta latência de disco se propagará em tempos de acesso lentos para CRX e pode resultar em problemas de desempenho interativos.
* Baixo throughput do disco pode resultar em baixo desempenho para o CQ5 DAM.

## Teste de desempenho {#testing-for-performance}

Para cada projeto DAM, certifique-se de estabelecer um regime de teste de desempenho que possa identificar e resolver gargalos rapidamente. Para isso, considere os seguintes pontos de verificação:

1. Testes de desempenho completos usando JMeter - Simule um exemplo de sessão de pesquisa e navegação para detectar problemas de desempenho interativos.
1. Testes de throughput e latência usando o JMeter - Executar em um computador cliente garante que não haja problemas relacionados à topologia.
1. Testes de processamento de ativos padronizados - assimile um pequeno número de ativos de exemplo e meça o tempo. Isso deve incluir a integração do fluxo de trabalho externo.
1. Monitore a utilização da CPU, disco e memória de cada nó de cluster.
1. Diagnósticos de desempenho de leitura/gravação do CRX para identificar problemas relacionados a não-processamento.
1. Monitore a latência e o throughput da rede do cluster DAM para o NAS.
1. Teste o desempenho de leitura e gravação, bem como a latência de disco diretamente no NAS, se possível.

## Ajuste de gargalos {#tweaking-bottlenecks}

Os seguintes ajustes de desempenho foram usados em projetos até agora:

* Geração seletiva de representação: gere somente as representações de que você precisa adicionando condições ao fluxo de trabalho de processamento de ativos, de modo que representações mais caras sejam geradas somente para ativos selecionados.
* Armazenamento de dados compartilhado entre instâncias: ao ficar com pouco espaço em disco, isso pode reduzir consideravelmente a quantidade de espaço em disco necessário, ao custo de esforços de configuração mais altos e perda da limpeza automática do armazenamento de dados.

## Leitura adicional {#further-reading}

* [Analisando processos lentos e bloqueados](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

