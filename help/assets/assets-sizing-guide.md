---
title: "[!DNL Assets] guia de dimensionamento"
description: Práticas recomendadas para determinar métricas eficientes para estimar a infraestrutura e os recursos necessários para a implantação [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Asset Management
exl-id: fd58ead9-5e18-4f55-8d20-1cf4402fad97
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 0%

---

# [!DNL Assets] guia de dimensionamento {#assets-sizing-guide}

Ao dimensionar o ambiente para um [!DNL Adobe Experience Manager Assets] é importante garantir que haja recursos suficientes disponíveis em termos de disco, CPU, memória, E/S e throughput de rede. O dimensionamento de muitos desses recursos requer a compreensão de quantos ativos estão sendo carregados no sistema. Se uma métrica melhor não estiver disponível, você poderá dividir o tamanho da biblioteca existente pela idade da biblioteca para encontrar a taxa em que os ativos são criados.

## Disco {#disk}

### DataStore {#datastore}

Um erro comum cometido ao dimensionar o espaço em disco necessário para um [!DNL Assets] A implementação é basear os cálculos no tamanho das imagens brutas a serem assimiladas no sistema. Por padrão, [!DNL Experience Manager] O cria três representações além da imagem original para uso na renderização da [!DNL Experience Manager] elementos da interface do usuário. Em implementações anteriores, observou-se que essas representações assumem o dobro do tamanho dos ativos que são assimilados.

A maioria dos usuários define representações personalizadas, além das representações predefinidas. Além das representações, [!DNL Assets] O permite extrair subativos de tipos de arquivos comuns, como [!DNL Adobe InDesign] e [!DNL Adobe Illustrator].

Por fim, os recursos de controle de versão do [!DNL Experience Manager] armazenar duplicatas dos ativos no histórico de versões. Você pode configurar as versões a serem removidas com frequência. No entanto, muitos usuários optam por manter versões no sistema por muito tempo, o que consome espaço de armazenamento adicional.

Considerando esses fatores, você precisa de uma metodologia para calcular um espaço de armazenamento aceitável e preciso para armazenar os ativos do usuário.

1. Determine o tamanho e o número de ativos carregados no sistema.
1. Obtenha uma amostra representativa dos ativos a serem carregados no [!DNL Experience Manager]. Por exemplo, se você planeja carregar arquivos de PSD, JPG, AI e PDF no sistema, são necessárias várias imagens de amostra de cada formato de arquivo. Além disso, essas amostras devem ser representativas dos diferentes tamanhos de arquivo e complexidades de imagens.
1. Defina as representações que serão usadas.
1. Criar as representações no [!DNL Experience Manager] usar [!DNL ImageMagick] ou [!DNL Adobe Creative Cloud] aplicativos. Além das representações especificadas pelos usuários, crie representações predefinidas. Para usuários que implementam o Dynamic Media, é possível usar o binário IC para gerar as representações PTIFF a serem armazenadas no Experience Manager.
1. Se você planeja usar subativos, gere-os para os tipos de arquivos apropriados.
1. Compare o tamanho das imagens de saída, das representações e dos subativos com as imagens originais. Ele permite gerar um fator de crescimento esperado quando o sistema for carregado. Por exemplo, se você gerar representações e subativos com um tamanho combinado de 3 GB após o processamento de 1 GB de ativos, o fator de crescimento de representação será 3.
1. Determine o tempo máximo durante o qual as versões de ativos devem ser mantidas no sistema.
1. Determine com que frequência os ativos existentes são modificados no sistema. Se [!DNL Experience Manager] for usado como um hub de colaboração em fluxos de trabalho criativos, a quantidade de alterações será alta. Se apenas os ativos concluídos forem carregados no sistema, esse número será muito menor.
1. Determine quantos ativos são carregados no sistema a cada mês. Se não tiver certeza, verifique o número de ativos disponíveis no momento e divida o número pela idade do ativo mais antigo para calcular um número aproximado.

A execução das etapas acima ajuda a determinar o seguinte:

* Tamanho bruto dos ativos a serem carregados.
* Número de ativos a serem carregados.
* Fator de crescimento de representação.
* Número de modificações de ativos feitas por mês.
* Número de meses para manter versões de ativos.
* Número de novos ativos carregados a cada mês.
* Anos de crescimento para alocação de espaço de armazenamento.

Você pode especificar esses números na planilha Dimensionamento de Rede para determinar o espaço total necessário para seu armazenamento de dados. Também é uma ferramenta útil para determinar o impacto de manter versões de ativos ou modificá-los no [!DNL Experience Manager] sobre o crescimento do disco.

Os dados de exemplo preenchidos na ferramenta demonstram a importância de executar as etapas mencionadas. Se você dimensionar o armazenamento de dados exclusivamente com base nas imagens brutas que estão sendo carregadas (1 TB), pode ter subestimado o tamanho do repositório em um fator de 15.

[Obter arquivo](assets/disk_sizing_tool.xlsx)

### Armazenamentos de dados compartilhados {#shared-datastores}

Para grandes armazenamentos de dados, é possível implementar um armazenamento de dados compartilhado por meio de um armazenamento de dados de arquivo compartilhado em uma unidade conectada à rede ou por meio de um armazenamento de dados Amazon S3. Nesse caso, as instâncias individuais não precisam manter uma cópia dos binários. Além disso, um armazenamento de dados compartilhado facilita a replicação sem binários e ajuda a reduzir a largura de banda usada para replicar ativos em ambientes de publicação.

#### Casos de uso {#use-cases}

O armazenamento de dados pode ser compartilhado entre uma instância de autor principal e stand-by para minimizar o tempo necessário para atualizar a instância stand-by com alterações feitas na instância principal. Você também pode compartilhar o armazenamento de dados entre as instâncias de autor e publicação para minimizar o tráfego durante a replicação.

#### Desvantagens {#drawbacks}

Devido a algumas armadilhas, o compartilhamento de um armazenamento de dados não é recomendado em todos os casos.

#### Ponto único de falha {#single-point-of-failure}

Ter um armazenamento de dados compartilhado introduz um ponto único de falha em uma infraestrutura. Considere um cenário em que seu sistema tem uma instância de autor e duas instâncias de publicação, cada uma com seu próprio armazenamento de dados. Se algum deles falhar, os outros dois ainda poderão continuar em execução. No entanto, se o armazenamento de dados for compartilhado, uma única falha de disco pode desativar toda a infraestrutura. Portanto, mantenha um backup do armazenamento de dados compartilhado de onde você possa restaurá-lo rapidamente.

É preferível implantar o serviço AWS S3 para armazenamentos de dados compartilhados porque ele reduz significativamente a probabilidade de falha em comparação às arquiteturas de disco normais.

#### Maior complexidade {#increased-complexity}

Os armazenamentos de dados compartilhados também aumentam a complexidade das operações, como a coleta de lixo. Normalmente, a coleta de lixo para um armazenamento de dados independente pode ser iniciada com um único clique. No entanto, os armazenamentos de dados compartilhados exigem operações de varredura de marca em cada membro que usa o armazenamento de dados, além de executar a coleção real em um único nó.

Para operações AWS, a implementação de um único local central (via Amazon S3), em vez da criação de um array RAID de volumes EBS, pode compensar significativamente a complexidade e os riscos operacionais do sistema.

#### Questões de desempenho {#performance-concerns}

Um armazenamento de dados compartilhado exige que os binários sejam armazenados em uma unidade montada em rede que seja compartilhada entre todas as instâncias. Como esses binários são acessados em uma rede, o desempenho do sistema é afetado negativamente. Você pode reduzir parcialmente o impacto usando uma conexão de rede rápida a uma matriz rápida de discos. Mas essa é uma proposta cara. Se houver operações AWS, todos os discos serão remotos e exigirão conectividade de rede. Volumes efêmeros perdem dados quando a instância é iniciada ou interrompida.

#### Latência {#latency}

A latência em implementações S3 é introduzida pelas threads de gravação em segundo plano. Os procedimentos de backup devem considerar essa latência. Além disso, os índices Lucene podem permanecer incompletos ao fazer um backup. Ela se aplica a qualquer arquivo com detecção de tempo gravado no armazenamento de dados S3 e acessado de outra instância.

### Armazenamento de nó ou armazenamento de documento {#node-store-document-store}

É difícil chegar a números de dimensionamento precisos para um NodeStore ou DocumentStore devido aos recursos consumidos pelo seguinte:

* Metadados do ativo
* Versões do ativo
* Logs de auditoria
* Fluxos de trabalho arquivados e ativos

Como os binários são armazenados no armazenamento de dados, cada binário ocupa algum espaço. A maioria dos repositórios tem menos de 100 GB. No entanto, pode haver repositórios maiores de até 1 TB. Além disso, para executar a compactação offline, é necessário espaço livre suficiente no volume para regravar o repositório compactado junto com a versão pré-compactada. Uma boa regra geral é dimensionar o disco para 1,5 vez o tamanho esperado para o repositório.

Para o repositório, use SSDs ou discos com um nível de IOPS superior a 3000. Para eliminar as chances de IOPS introduzirem gargalos de desempenho, monitore os níveis de espera de E/S da CPU para detectar os primeiros sinais de problemas.

[Obter arquivo](assets/aem_environment_sizingtool.xlsx)

## Rede {#network}

[!DNL Assets] O tem vários casos de uso que tornam o desempenho da rede mais importante do que em muitos de nossos [!DNL Experience Manager] projetos. Um cliente pode ter um servidor rápido, mas se a conexão de rede não for grande o suficiente para suportar a carga dos usuários que estão fazendo upload e baixando ativos do sistema, ela ainda parecerá lenta. Há uma boa metodologia para determinar o ponto de bloqueio na conexão de rede de um usuário ao [!DNL Experience Manager] em [Considerações de ativos para experiência do usuário, dimensionamento de instâncias, avaliação de fluxo de trabalho e topologia de rede](/help/assets/assets-network-considerations.md).

## Limitações {#limitations}

Ao dimensionar uma implementação, é importante ter em mente as limitações do sistema. Se a implementação proposta exceder essas limitações, empregue estratégias criativas, como particionar os ativos em vários [!DNL Assets] implementações.

O tamanho do arquivo não é o único fator que contribui para problemas de falta de memória (OOM). Também depende das dimensões da imagem. Você pode evitar problemas de OOM fornecendo um tamanho de heap maior ao iniciar [!DNL Experience Manager].

Além disso, você pode editar a propriedade threshold size do `com.day.cq.dam.commons.handler.StandardImageHandler` componente no Configuration Manager para usar arquivo temporário intermediário maior que zero.

## Número máximo de ativos {#maximum-number-of-assets}

O limite para o número de arquivos que podem existir em um armazenamento de dados pode ser de 2,1 bilhões devido às limitações do sistema de arquivos. É provável que o repositório encontre problemas devido ao grande número de nós muito antes de atingir o limite do armazenamento de dados.

Se as representações forem geradas incorretamente, use a biblioteca Camera Raw. No entanto, nesse caso, o lado mais longo da imagem não deve ser superior a 65000 pixels. Além disso, a imagem não deve conter mais de 512 MP (512 x 1024 x 1024 pixels). O tamanho do ativo não importa.

É difícil estimar com precisão o tamanho do arquivo de TIFF suportado prontamente com um heap específico para [!DNL Experience Manager] porque fatores adicionais, como o tamanho do pixel, influenciam o processamento. É possível que [!DNL Experience Manager] O pode processar um arquivo de tamanho 255 MB prontos para uso, mas o não pode processar um tamanho de arquivo de 18 MB porque o último é composto por um número de pixels excepcionalmente maior em comparação ao primeiro.

## Tamanho dos ativos {#size-of-assets}

Por padrão, [!DNL Experience Manager] permite carregar ativos com tamanho de arquivo de até 2 GB. Para fazer upload de ativos muito grandes no [!DNL Experience Manager], consulte [Configuração para carregar ativos muito grandes](managing-video-assets.md#configuration-to-upload-assets-that-are-larger-than-gb).
