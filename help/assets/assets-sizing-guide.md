---
title: "[!DNL Assets] guia de dimensionamento"
description: Práticas recomendadas para determinar métricas eficientes para estimar a infraestrutura e os recursos necessários para implantar [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Asset Management
exl-id: fd58ead9-5e18-4f55-8d20-1cf4402fad97
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---

# [!DNL Assets] guia de dimensionamento {#assets-sizing-guide}

Ao dimensionar o ambiente para um [!DNL Adobe Experience Manager Assets] na implementação, é importante garantir que haja recursos suficientes disponíveis em termos de disco, CPU, memória, E/S e throughput da rede. Dimensionar muitos desses recursos requer uma compreensão de quantos ativos estão sendo carregados no sistema. Se uma métrica melhor não estiver disponível, você pode dividir o tamanho da biblioteca existente pela idade da biblioteca para encontrar a taxa na qual os ativos são criados.

## Disco {#disk}

### DataStore {#datastore}

Um erro comum foi cometido ao dimensionar o espaço em disco necessário para um [!DNL Assets] a implementação é basear os cálculos no tamanho das imagens brutas a serem assimiladas no sistema. Por padrão, [!DNL Experience Manager] cria três representações além da imagem original para uso na renderização da variável [!DNL Experience Manager] elementos da interface do usuário. Em implementações anteriores, essas representações foram observadas para assumir o dobro do tamanho dos ativos que são assimilados.

A maioria dos usuários define representações personalizadas, além de representações predefinidas. Além das representações, [!DNL Assets] permite extrair subativos de tipos de arquivos comuns, como [!DNL Adobe InDesign] e [!DNL Adobe Illustrator].

Finalmente, os recursos de controle de versão de [!DNL Experience Manager] armazene duplicatas dos ativos no histórico de versões. Você pode configurar as versões a serem removidas com frequência. No entanto, muitos usuários optam por reter versões no sistema por um longo tempo, o que consome espaço de armazenamento adicional.

Considerando esses fatores, você precisa de uma metodologia para calcular um espaço de armazenamento aceitável para armazenar os ativos do usuário.

1. Determine o tamanho e o número de ativos que serão carregados no sistema.
1. Obtenha uma amostra representativa dos ativos que serão carregados no [!DNL Experience Manager]. Por exemplo, se você planeja carregar arquivos PSD, JPG, AI e PDF no sistema, você precisa de várias imagens de amostra de cada formato de arquivo. Além disso, essas amostras devem ser representativas dos diferentes tamanhos de arquivo e complexidades de imagens.
1. Defina as representações a serem usadas.
1. Crie as representações em [!DNL Experience Manager] usar [!DNL ImageMagick] ou [!DNL Adobe Creative Cloud] aplicativos. Além das representações que os usuários especificam, crie representações prontas para uso. Para usuários que implementam o Dynamic Media, você pode usar o binário IC para gerar as renderizações PTIFF a serem armazenadas no Experience Manager.
1. Se você planeja usar subativos, gere-os para os tipos de arquivo apropriados.
1. Compare o tamanho das imagens de saída, representações e subativos com as imagens originais. Ele permite gerar um fator de crescimento esperado quando o sistema é carregado. Por exemplo, se você gerar representações e subativos com um tamanho combinado de 3 GB após o processamento de 1 GB de ativos, o fator de crescimento da representação será 3.
1. Determine o tempo máximo durante o qual as versões de ativos devem ser mantidas no sistema.
1. Determine a frequência com que os ativos existentes são modificados no sistema. If [!DNL Experience Manager] é usado como um hub de colaboração em workflows criativos, a quantidade de alterações é alta. Se apenas os ativos finalizados forem carregados no sistema, esse número será muito menor.
1. Determine quantos ativos são carregados no sistema a cada mês. Se não tiver certeza, verifique o número de ativos disponíveis no momento e divida o número por idade do ativo mais antigo para calcular um número aproximado.

A execução das etapas acima ajuda a determinar o seguinte:

* Tamanho bruto dos ativos a serem carregados.
* Número de ativos a serem carregados.
* Fator de crescimento da representação.
* Número de modificações de ativos efetuadas por mês.
* Número de meses para manter versões de ativos.
* Número de novos ativos carregados a cada mês.
* Anos de crescimento para alocação de espaço de armazenamento.

É possível especificar esses números na planilha de Dimensionamento de Rede para determinar o espaço total necessário para o armazenamento de dados. Também é uma ferramenta útil para determinar o impacto da manutenção de versões de ativos ou da modificação de ativos no [!DNL Experience Manager] no crescimento do disco.

O exemplo de dados preenchido na ferramenta demonstra a importância de executar as etapas mencionadas. Se você dimensionar o armazenamento de dados com base exclusivamente nas imagens brutas que estão sendo carregadas (1 TB), talvez tenha subestimado o tamanho do repositório em um fator de 15.

[Obter arquivo](assets/disk_sizing_tool.xlsx)

### Armazenamento de dados compartilhados {#shared-datastores}

Para grandes armazenamentos de dados, você pode implementar um armazenamento de dados compartilhado por meio de um armazenamento de dados de arquivo compartilhado em uma unidade conectada à rede ou por meio de um armazenamento de dados Amazon S3. Nesse caso, instâncias individuais não precisam manter uma cópia dos binários. Além disso, um armazenamento de dados compartilhado facilita a replicação sem binários e ajuda a reduzir a largura de banda usada para replicar ativos para publicar ambientes.

#### Casos de uso {#use-cases}

O armazenamento de dados pode ser compartilhado entre uma instância de autor primária e de standby para minimizar a quantidade de tempo que leva para atualizar a instância de standby com alterações feitas na instância primária. Você também pode compartilhar o armazenamento de dados entre as instâncias de autor e publicação para minimizar o tráfego durante a replicação.

#### Desvantagens {#drawbacks}

Devido a algumas armadilhas, o compartilhamento de um armazenamento de dados não é recomendado em todos os casos.

#### Ponto único de falha {#single-point-of-failure}

Com um armazenamento de dados compartilhado, o apresenta um único ponto de falha em uma infraestrutura. Considere um cenário em que o sistema tem uma e duas instâncias de publicação, cada uma com seu próprio armazenamento de dados. Se algum deles falhar, os outros dois ainda poderão continuar a funcionar. No entanto, se o armazenamento de dados for compartilhado, uma única falha de disco poderá derrubar toda a infraestrutura. Portanto, assegure-se de manter um backup do armazenamento de dados compartilhado de onde você pode restaurar o armazenamento de dados rapidamente.

A implantação do serviço AWS S3 para armazenamentos de dados compartilhados é preferível, pois reduz significativamente a probabilidade de falha em comparação com arquiteturas de disco normais.

#### Maior complexidade {#increased-complexity}

Os armazenamentos de dados compartilhados também aumentam a complexidade das operações, como a coleta de lixo. Normalmente, a coleta de lixo para um armazenamento de dados independente pode ser iniciada com um único clique. No entanto, os armazenamentos de dados compartilhados exigem operações de varredura de marca em cada membro que usa o armazenamento de dados, além de executar a coleção real em um único nó.

Para operações AWS, a implementação de um único local central (via Amazon S3), em vez de construir uma matriz RAID de volumes EBS, pode compensar significativamente a complexidade e os riscos operacionais no sistema.

#### Problemas de desempenho {#performance-concerns}

Um armazenamento de dados compartilhado requer que os binários sejam armazenados em uma unidade montada em rede compartilhada entre todas as instâncias. Como esses binários são acessados em uma rede, o desempenho do sistema é afetado negativamente. Você pode reduzir parcialmente o impacto usando uma conexão de rede rápida a um array de discos mais rápido. Mas essa é uma proposta cara. No caso de operações AWS, todos os discos são remotos e exigem conectividade de rede. Volumes efêmeros perdem dados quando a instância é iniciada ou interrompida.

#### Latência {#latency}

A latência nas implementações S3 é introduzida pelos threads de escrita em segundo plano. Os procedimentos de backup devem levar em conta essa latência. Além disso, os índices Lucene podem permanecer incompletos ao fazer um backup. Aplica-se a qualquer arquivo com diferenciação de tempo gravado no armazenamento de dados S3 e acessado de outra instância.

### Armazenamento de nós ou armazenamento de documentos {#node-store-document-store}

É difícil obter números de dimensionamento precisos para um NodeStore ou DocumentStore devido aos recursos consumidos pelos seguintes:

* Metadados do ativo
* Versões de ativos
* Logs de auditoria
* Fluxos de trabalho arquivados e ativos

Como os binários são armazenados no armazenamento de dados, cada binário ocupa algum espaço. A maioria dos repositórios tem menos de 100 GB. No entanto, pode haver repositórios maiores de até 1 TB. Além disso, para executar a compactação offline, é necessário espaço livre suficiente no volume para reescrever o repositório compactado junto com a versão pré-compactada. Um princípio básico é dimensionar o disco para 1,5 vezes o tamanho esperado para o repositório.

Para o repositório, use SSDs ou discos com um nível de IOPS superior a 3000. Para eliminar as chances de os IOPS introduzirem gargalos de desempenho, monitore os níveis de espera de E/S da CPU para obter sinais antecipados de problemas.

[Obter arquivo](assets/aem_environment_sizingtool.xlsx)

## Rede {#network}

[!DNL Assets] O tem vários casos de uso que tornam o desempenho da rede mais importante do que em muitos de nossos [!DNL Experience Manager] projetos. Um cliente pode ter um servidor rápido, mas se a conexão de rede não for grande o suficiente para suportar a carga dos usuários que estão carregando e baixando ativos do sistema, ele ainda parecerá estar lento. Há uma boa metodologia para determinar o ponto de estrangulamento na conexão de rede de um usuário para [!DNL Experience Manager] at [Considerações de ativos para experiência do usuário, dimensionamento de instâncias, avaliação de fluxos de trabalho e topologia de rede](/help/assets/assets-network-considerations.md).

## Limitações {#limitations}

Ao dimensionar uma implementação, é importante manter as limitações do sistema em mente. Se a implementação proposta exceder essas limitações, utilize estratégias criativas, como a divisão dos ativos em vários [!DNL Assets] implementações.

O tamanho do arquivo não é o único fator que contribui para problemas de falta de memória (OOM). Também depende das dimensões da imagem. Você pode evitar problemas de OOM fornecendo um tamanho de heap mais alto ao iniciar [!DNL Experience Manager].

Além disso, é possível editar a propriedade threshold size do `com.day.cq.dam.commons.handler.StandardImageHandler` no Configuration Manager para usar um arquivo temporário intermediário maior que zero.

## Número máximo de ativos {#maximum-number-of-assets}

O limite para o número de arquivos que podem existir em um armazenamento de dados pode ser de 2,1 bilhões devido às limitações do sistema de arquivos. É provável que o repositório encontre problemas devido a um grande número de nós muito antes de atingir o limite do armazenamento de dados.

Se as renderizações forem geradas incorretamente, use a biblioteca Camera Raw. No entanto, nesse caso, o lado mais longo da imagem não deve ser maior que 65.000 pixels. Além disso, a imagem não deve conter mais de 512 MP (512 x 1024 x 1024 pixels). O tamanho do ativo não importa.

É difícil estimar com precisão o tamanho do arquivo TIFF pronto para uso com um heap específico para [!DNL Experience Manager] porque fatores adicionais, como tamanho de pixel, influenciam o processamento. É possível que [!DNL Experience Manager] O pode processar um arquivo de tamanho pronto para uso de 255 MB, mas não pode processar um tamanho de arquivo de 18 MB porque o último consiste de um número invulgarmente maior de pixels em comparação ao primeiro.

## Dimensão dos ativos {#size-of-assets}

Por padrão, [!DNL Experience Manager] O permite carregar ativos de até 2 GB. Para fazer upload de ativos muito grandes no [!DNL Experience Manager], consulte [Configuração para fazer upload de ativos muito grandes](managing-video-assets.md#configuration-to-upload-assets-that-are-larger-than-gb).
