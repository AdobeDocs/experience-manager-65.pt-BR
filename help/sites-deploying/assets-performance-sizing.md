---
title: Guia de desempenho de ativos
seo-title: Assets Performance Guide
description: Saiba como determinar o dimensionamento ideal de hardware para uma nova configuração do Gerenciamento de ativos digitais (DAM) e como solucionar problemas de desempenho
seo-description: Learn how to determine the optimal hardware sizing for a new Digital Asset Management (DAM) setup and how to troubleshoot performance issues
uuid: 8291c5b9-c543-41cf-8754-445826200930
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: a79839e2-be39-418b-a3bd-f5457e555172
exl-id: fbe15e1b-830b-4752-bd02-0d239a90bc68
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 0%

---

# Guia de desempenho de ativos{#assets-performance-guide}

A gestão de ativos digitais é frequentemente utilizada nos casos em que o desempenho é importante; no entanto, a configuração típica do DAM contém vários componentes de hardware e software que podem afetar o desempenho. Este documento fornece o seguinte:

* Informações para administradores de sistema sobre como determinar o dimensionamento ideal de hardware para uma nova configuração do Gerenciamento de ativos digitais
* Informações para desenvolvedores de software que procuram solucionar problemas de instâncias do DAM com problemas de desempenho

## Problemas de desempenho {#performance-issues}

O baixo desempenho no gerenciamento de ativos digitais pode afetar a experiência do usuário de três maneiras: desempenho interativo, processamento de ativos e velocidade de download. Para melhorar o desempenho, é importante medir o desempenho observado corretamente e estabelecer métricas de meta.

**1. Pesquisa e navegação interativas** Os usuários estão pesquisando ativos ou navegando pelo DAM Finder e reclamam dos tempos de resposta lentos ou dos resultados da pesquisa não aparecem imediatamente. Este é um problema interativo de desempenho.

O desempenho interativo é medido em termos de tempo de resposta da página. Esse é o tempo que leva para receber a solicitação HTTP para fechar a resposta HTTP, que pode ser determinada a partir dos arquivos de log da solicitação. O desempenho típico do target é um tempo de resposta de página abaixo de dois segundos.

**2. Processamento de ativos** Um problema de processamento de ativos é quando os usuários estão fazendo upload de ativos e leva minutos até que os ativos sejam prontamente convertidos e assimilados AEM DAM.

O desempenho do processamento de ativos é medido em termos do tempo médio de conclusão do processo do fluxo de trabalho. Esse é o tempo que leva desde invocar o processo de fluxo de trabalho de atualização de ativos até sua conclusão, que pode ser determinado a partir da interface do usuário dos relatórios de fluxo de trabalho. O desempenho típico do target depende do tamanho e do tipo dos ativos processados e do número de representações. Os exemplos de desempenho do target podem ser:

* abaixo de dez segundos para imagens menores que 1280x1280 pixels usando representações padrão
* abaixo de um minuto para imagens menores que 100 MB usando representações padrão
* abaixo de cinco minutos para clipes de vídeo de alta definição com menos de um minuto

**3. Velocidade de download** Um problema de taxa de transferência é quando o download AEM DAM demora e as miniaturas não aparecem imediatamente ao navegar pelo DAM Admin ou pelo DAM Finder.

O desempenho da throughput é medido em termos de taxa de download em kilobits por segundo. O desempenho típico do target é de 300 kilobits por segundo para 100 downloads simultâneos.

**4. Fatores que influenciam o desempenho do processamento de ativos**

Para poder estimar qual hardware você precisa para processar ativos, os seguintes aspectos precisam ser levados em consideração:

* A resolução das imagens em quantidade de pixels
* O heap atribuído ao processo de AEM

A quantidade de pixels contidos na imagem determina o tempo de processamento - mais pixels significa que o processamento leva mais tempo.
O tipo de imagem, a taxa de compactação ou o tamanho relacionado do arquivo em que a imagem é armazenada não influenciam significativamente o desempenho geral.

O heap foi identificado como sendo o fator limitante mais importante. Sempre que o ativo excede a memória livre disponível, o desempenho do processamento cai rapidamente.

Os processos DAM são adequados para serem executados em paralelo para grandes quantidades. O upload de ativos em um lote e de processadores de vários núcleos acelera o tempo absoluto gasto por ativo.

**5. Avaliação dos requisitos de hardware para a execução do processamento de ativos**

O processamento abrangente de ativos digitais requer recursos de hardware otimizados, os fatores mais relevantes são o tamanho da imagem e o pico de throughput das imagens processadas.

Aloque pelo menos 16 GB de heap e configure a variável [!UICONTROL Ativo de atualização DAM] para usar o [Pacote Camera Raw](/help/assets/camera-raw.md) para a assimilação de imagens brutas.

## Noções básicas sobre o sistema {#understanding-the-system}

Uma configuração típica do DAM consiste em usuários finais que acessam o DAM por meio de um balanceador de carga. A instância do DAM pode fazer parte de uma configuração em cluster, em que cada instância do DAM é executada em um processo de máquina virtual Java em uma máquina física ou em uma máquina virtual. O armazenamento DAM é fornecido por um disco RAID em casos de configuração de máquina única ou de armazenamento conectado à rede gerenciada em caso de configurações em cluster.

A legenda a seguir descreve as possíveis áreas de desempenho com algumas soluções, conforme apropriado.

**Conexão de rede ao usuário final** Uma conexão de rede lenta pode causar problemas de taxa de transferência. Em alguns casos raros, também podem ocorrer problemas de latência. Às vezes, o usuário tem uma conexão lenta do ISP, especialmente em intranets. Este é um sinal de topologia de rede incorreta.

**Sistema de arquivos temporário** Um sistema de arquivos local lento pode causar problemas de desempenho interativo, especialmente quando se trata de pesquisa, porque os índices de pesquisa são armazenados no disco local. Além disso, pode causar problemas de processamento de ativos se o processo da linha de comando estiver sendo usado.

**Localizador de DAM AEM** Problemas interativos de desempenho, muitas vezes experientes em pesquisas, são causados por alto uso da CPU devido a muitos usuários simultâneos ou outros processos que consomem a CPU na mesma instância. Mudar de máquinas virtuais para máquinas dedicadas e garantir que nenhum outro serviço seja executado na máquina pode ajudar a melhorar o desempenho. Se a alta carga da CPU for causada pelo processamento de ativos e por muitos usuários simultâneos, Day recomenda adicionar outros nós de cluster.

**Fluxo de trabalho AEM DAM** Processos de fluxo de trabalho de longa duração durante a assimilação de ativos causam problemas de desempenho do processamento de ativos. Dependendo do tipo de ativos que estão sendo processados, isso pode indicar sobre-utilização da CPU. Day recomenda reduzir o número de outros processos em execução no sistema e aumentar o número de CPUs disponíveis adicionando nós de cluster.

**Conectividade NAS** A baixa conectividade de rede com o NAS causa problemas de desempenho interativos, pois o acesso a novos nós durante o processamento de ativos é retardado devido à latência da rede. Além disso, a taxa de transferência lenta da rede afeta negativamente a taxa de transferência, mas também o desempenho do processamento de ativos, pois o carregamento e o salvamento de representações são retardados.

Motivos para latência e throughput ruins em um NAS são geralmente topologia de rede ou sobre-utilização de NAS por outros serviços.

**Armazenamento conectado à rede** Sistemas de armazenamento de dados de rede usados em excesso podem causar uma matriz de problemas:

* Baixo espaço em disco é um problema encontrado com frequência que pode ser evitado por meio do dimensionamento adequado de um projeto DAM.
* A alta latência de disco se propagará em tempos de acesso lentos para o CRX e pode resultar em problemas de desempenho interativos.
* A baixa taxa de transferência de disco pode resultar em baixo desempenho para o CQ5 DAM.

## Teste de desempenho {#testing-for-performance}

Para cada projeto do DAM, certifique-se de estabelecer um regime de teste de desempenho que possa identificar e resolver gargalos rapidamente. Para fazer isso, considere os seguintes pontos de verificação:

1. Testes completos de desempenho usando o JMeter - Simule um exemplo de sessão de pesquisa e navegação para detectar problemas de desempenho interativos.
1. Testes de throughput e latência usando o JMeter - A execução em um computador cliente garante que não haja problemas relacionados à topologia.
1. Testes de processamento de ativos padronizados - Aspire um pequeno número de ativos de exemplo e meça o tempo. Isso deve incluir integração de workflow externo.
1. Monitore a utilização da CPU, disco e memória de cada nó do cluster.
1. Diagnósticos de desempenho de leitura/gravação do CRX para identificar problemas relacionados ao não processamento.
1. Monitore a latência de rede e o throughput do cluster DAM para o NAS.
1. Teste o desempenho de leitura e gravação, bem como a latência de disco diretamente no NAS, se possível.

## Ajustando gargalos {#tweaking-bottlenecks}

Os seguintes ajustes de desempenho foram usados em projetos até o momento:

* Geração de representação seletiva: gere somente as renderizações necessárias, adicionando condições ao fluxo de trabalho de processamento de ativos, para que renderizações mais dispendiosas sejam geradas somente para ativos selecionados.
* Armazenamento de dados compartilhados entre instâncias: ao executar pouco espaço em disco, isso pode reduzir consideravelmente a quantidade de espaço em disco necessária ao custo de esforços de configuração mais altos e perder a limpeza automática do armazenamento de dados.

## Leitura adicional {#further-reading}

* [Análise de processos lentos e bloqueados](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)
