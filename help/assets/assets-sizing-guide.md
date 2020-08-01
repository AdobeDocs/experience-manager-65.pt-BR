---
title: Guia de dimensionamento do [!DNL Assets]
description: Práticas recomendadas para determinar métricas eficientes para estimar a infraestrutura e os recursos necessários para a implantação [!DNL Adobe Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '1616'
ht-degree: 0%

---


# [!DNL Assets] guia de dimensionamento {#assets-sizing-guide}

Ao dimensionar o ambiente para uma [!DNL Adobe Experience Manager Assets] implementação, é importante garantir que haja recursos suficientes disponíveis em termos de disco, CPU, memória, E/S e throughput da rede. Dimensionar muitos desses recursos requer uma compreensão de quantos ativos estão sendo carregados no sistema. Se uma métrica melhor não estiver disponível, é possível dividir o tamanho da biblioteca existente pela idade da biblioteca para localizar a taxa na qual os ativos são criados.

## Disco {#disk}

### DataStore {#datastore}

Um erro comum cometido ao dimensionar o espaço em disco necessário para uma [!DNL Assets] implementação é basear os cálculos no tamanho das imagens brutas a serem ingeridas no sistema. Por padrão, [!DNL Experience Manager] cria três execuções além da imagem original para uso na renderização dos elementos da interface do [!DNL Experience Manager] usuário. Em implementações anteriores, essas execuções assumiram o dobro do tamanho dos ativos que são assimilados.

A maioria dos usuários define representações personalizadas, além de execuções prontas. Além das representações, [!DNL Assets] permite extrair subativos de tipos de arquivos comuns, como [!DNL Adobe InDesign] e [!DNL Adobe Illustrator].

Por fim, os recursos de controle de versão dos duplicados da [!DNL Experience Manager] loja dos ativos no histórico de versões. Você pode configurar as versões a serem removidas com frequência. Entretanto, muitos usuários optam por reter versões no sistema por um longo tempo, o que consome mais espaço no armazenamento.

Considerando esses fatores, você precisa de uma metodologia para calcular um espaço de armazenamento com precisão aceitável para armazenar os ativos do usuário.

1. Determine o tamanho e o número de ativos que serão carregados no sistema.
1. Obtenha uma amostra representativa dos ativos a serem carregados [!DNL Experience Manager]. Por exemplo, se você planeja carregar arquivos PSD, JPG, AI e PDF no sistema, é necessário várias imagens de amostra de cada formato de arquivo. Além disso, essas amostras devem ser representativas dos diferentes tamanhos de arquivo e complexidades das imagens.
1. Defina as representações a serem usadas.
1. Crie as execuções em [!DNL Experience Manager] aplicativos [!DNL ImageMagick] ou [!DNL Adobe Creative Cloud] . Além das representações que os usuários especificam, crie execuções prontas para uso. Para usuários que implementam o Scene7, você pode usar o binário IC para gerar as execuções PTIFF a serem armazenadas no Experience Manager.
1. Se você planeja usar subativos, gere-os para os tipos de arquivo apropriados.
1. Compare o tamanho das imagens de saída, representações e subativos com as imagens originais. Ele permite gerar um fator de crescimento esperado quando o sistema é carregado. Por exemplo, se você gerar representações e subativos com um tamanho combinado de 3 GB após o processamento de 1 GB de ativos, o fator de crescimento da representação será 3.
1. Determine o tempo máximo durante o qual as versões de ativos devem ser mantidas no sistema.
1. Determine com que frequência os ativos existentes são modificados no sistema. Se [!DNL Experience Manager] for usado como um hub de colaboração em workflows criativos, a quantidade de alterações é alta. Se apenas os ativos finalizados forem carregados no sistema, esse número será muito menor.
1. Determine quantos ativos são carregados no sistema a cada mês. Se não tiver certeza, verifique o número de ativos que estão disponíveis no momento e divida o número pela idade do ativo mais antigo para calcular um número aproximado.

A execução das etapas acima ajuda a determinar o seguinte:

* Tamanho bruto dos ativos a serem carregados.
* Número de ativos a serem carregados.
* Fator de crescimento da representação.
* Número de modificações de ativos feitas por mês.
* Número de meses para manter versões de ativos.
* Número de novos ativos carregados mensalmente.
* Anos de crescimento para alocação de espaço no armazenamento.

Você pode especificar esses números na planilha Dimensionamento de rede para determinar o espaço total necessário para o armazenamento de dados. Também é uma ferramenta útil para determinar o impacto da manutenção de versões de ativos ou da modificação de ativos [!DNL Experience Manager] no crescimento do disco.

O exemplo de dados preenchido na ferramenta demonstra a importância de executar as etapas mencionadas. Se você dimensionar o armazenamento de dados com base apenas nas imagens brutas carregadas (1 TB), talvez tenha subestimado o tamanho do repositório em um fator de 15.

[Obter arquivo](assets/disk_sizing_tool.xlsx)

### Repositórios de dados compartilhados {#shared-datastores}

Para grandes armazenamentos de dados, você pode implementar um armazenamento de dados compartilhado por meio de um armazenamento de dados de arquivo compartilhado em uma unidade conectada à rede ou por meio de um armazenamento de dados Amazon S3. Nesse caso, as instâncias individuais não precisam manter uma cópia dos binários. Além disso, um armazenamento de dados compartilhado facilita a replicação sem binários e ajuda a reduzir a largura de banda usada para replicar ativos para publicar ambientes.

#### Casos de uso {#use-cases}

O armazenamento de dados pode ser compartilhado entre uma instância de autor principal e em espera para minimizar o tempo necessário para atualizar a instância em espera com as alterações feitas na instância principal. Você também pode compartilhar o armazenamento de dados entre as instâncias de autor e publicação para minimizar o tráfego durante a replicação.

#### Desvantagens {#drawbacks}

Devido a algumas armadilhas, o compartilhamento de um armazenamento de dados não é recomendado em todos os casos.

#### Ponto único de falha {#single-point-of-failure}

Com um armazenamento de dados compartilhado, apresenta um único ponto de falha em uma infraestrutura. Considere um cenário em que seu sistema tenha uma e duas instâncias de publicação, cada uma com seu próprio armazenamento de dados. Se algum deles falhar, os outros dois ainda poderão continuar em execução. No entanto, se o armazenamento de dados for compartilhado, uma única falha de disco poderá derrubar toda a infraestrutura. Portanto, certifique-se de manter um backup do armazenamento de dados compartilhado de onde você pode restaurar o armazenamento de dados rapidamente.

É preferível implantar o serviço AWS S3 para armazenamentos de dados compartilhados, pois reduz significativamente a probabilidade de falha em comparação às arquiteturas de disco normais.

#### Maior complexidade {#increased-complexity}

Os armazenamentos de dados compartilhados também aumentam a complexidade das operações, como a coleta de lixo. Normalmente, a coleta de lixo para um armazenamento de dados independente pode ser iniciada com um único clique. No entanto, os armazenamentos de dados compartilhados exigem operações de varredura de marca em cada membro que usa o armazenamento de dados, além de executar a coleção real em um único nó.

Para operações AWS, a implementação de um único local central (via Amazon S3), em vez de construir uma matriz RAID de volumes EBS, pode compensar significativamente a complexidade e os riscos operacionais no sistema.

#### Problemas de desempenho {#performance-concerns}

Um armazenamento de dados compartilhado exige que os binários sejam armazenados em uma unidade montada em rede que seja compartilhada entre todas as instâncias. Como esses binários são acessados em uma rede, o desempenho do sistema é afetado negativamente. Você pode atenuar parcialmente o impacto usando uma conexão de rede rápida para um array rápido de discos. No entanto, esta é uma proposta dispendiosa. No caso de operações AWS, todos os discos são remotos e exigem conectividade de rede. Os volumes efêmeros perdem dados quando a instância é start ou interrompida.

#### Latência {#latency}

A latência em implementações S3 é introduzida pelos threads de escrita em segundo plano. Os procedimentos de backup devem levar em conta essa latência. Além disso, os índices Lucene podem ficar incompletos ao fazer um backup. Ele se aplica a qualquer arquivo que faz distinção de tempo gravado no armazenamento de dados S3 e acessado de outra instância.

### Loja de nós ou documento {#node-store-document-store}

É difícil obter números precisos de dimensionamento para um NodeStore ou DocumentStore devido aos recursos consumidos pelos seguintes:

* Metadados do ativo
* Versões de ativos
* Logs de auditoria
* workflows arquivados e ativos

Como os binários são armazenados no armazenamento de dados, cada binário ocupa algum espaço. A maioria dos repositórios tem menos de 100 GB. No entanto, pode haver repositórios maiores de até 1 TB de tamanho. Além disso, para executar compactação offline, é necessário espaço livre suficiente no volume para regravar o repositório compactado junto com a versão pré-compactada. Uma boa regra é dimensionar o disco para 1,5 vezes o tamanho esperado para o repositório.

Para o repositório, use SSDs ou discos com um nível IOPS superior a 3000. Para eliminar as chances de o IOPS introduzir gargalos no desempenho, monitore os níveis de espera de E/S da CPU para obter os primeiros sinais de problemas.

[Obter arquivo](assets/aem_environment_sizingtool.xlsx)

## Rede {#network}

[!DNL Assets] tem vários casos de uso que tornam o desempenho da rede mais importante do que em muitos de nossos [!DNL Experience Manager] projetos. Um cliente pode ter um servidor rápido, mas se a conexão de rede não for grande o suficiente para suportar a carga dos usuários que estão carregando e baixando ativos do sistema, ele ainda parecerá estar lento. Há uma boa metodologia para determinar o ponto de estrangulamento na conexão de rede de um usuário às considerações do [!DNL Experience Manager] Assets para experiência do usuário, dimensionamento da instância, avaliação do fluxo de trabalho e topologia [](/help/assets/assets-network-considerations.md)de rede.

## Limitações           {#limitations}

Ao dimensionar uma implementação, é importante ter em mente as limitações do sistema. Se a implementação proposta exceder essas limitações, empregue estratégias criativas, como a divisão dos ativos em várias [!DNL Assets] implementações.

O tamanho do arquivo não é o único fator que contribui para problemas de falta de memória (OOM). Também depende das dimensões da imagem. Você pode evitar problemas de OOM fornecendo um tamanho de heap maior ao start [!DNL Experience Manager].

Além disso, você pode editar a propriedade de tamanho limite do `com.day.cq.dam.commons.handler.StandardImageHandler` componente no Configuration Manager para usar um arquivo temporário intermediário maior que zero.

## Número máximo de ativos {#maximum-number-of-assets}

O limite para o número de arquivos que podem existir em um armazenamento de dados pode ser de 2,1 bilhões devido às limitações do sistema de arquivos. É provável que o repositório encontre problemas devido ao grande número de nós muito antes de atingir o limite do armazenamento de dados.

Se as renderizações forem geradas incorretamente, use a biblioteca Camera Raw. Entretanto, nesse caso, o lado mais longo da imagem não deve ser maior que 65000 pixels. Além disso, a imagem não deve conter mais de 512 MP (512 x 1024 x 1024 pixels). O tamanho do ativo não importa.

É difícil estimar com precisão o tamanho do arquivo TIFF compatível out-of-the-box com um heap específico para o [!DNL Experience Manager] porque fatores adicionais, como o tamanho dos pixels, influenciam o processamento. É possível que [!DNL Experience Manager] seja possível processar um arquivo de 255 MB out-of-the-box, mas não é possível processar um tamanho de arquivo de 18 MB porque este último é composto de um número invulgarmente maior de pixels em comparação ao primeiro.

## Dimensão dos ativos {#size-of-assets}

Por padrão, [!DNL Experience Manager] permite carregar ativos de tamanho de arquivo de até 2 GB. Para fazer upload de ativos muito grandes no [!DNL Experience Manager], consulte [Configuração para fazer upload de ativos](managing-video-assets.md#configuration-to-upload-assets-that-are-larger-than-gb)muito grandes.
