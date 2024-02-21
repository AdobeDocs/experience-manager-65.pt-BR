---
title: Ajuste de desempenho [!DNL Assets].
description: Sugestões e orientações sobre [!DNL Experience Manager] configuração, alterações de hardware, software e componentes de rede para remover gargalos e otimizar o desempenho de [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
source-git-commit: 80e85ed78a26d784f4aa8e36c7de413cf9c03fa2
workflow-type: tm+mt
source-wordcount: '2728'
ht-degree: 0%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] guia de ajuste de desempenho {#assets-performance-tuning-guide}

Um [!DNL Experience Manager Assets] a instalação contém vários componentes de hardware, software e rede. Dependendo do cenário de implantação, você pode precisar de alterações específicas de configuração de hardware, software e componentes de rede para remover gargalos de desempenho.

Além disso, a identificação e o cumprimento de determinadas diretrizes de otimização de hardware e software ajudam a criar uma base sólida que permita [!DNL Experience Manager Assets] para atender às expectativas de desempenho, escalabilidade e confiabilidade.

Baixo desempenho no [!DNL Experience Manager Assets] O pode afetar a experiência do usuário em relação ao desempenho interativo, processamento de ativos, velocidade de download e outras áreas.

Na verdade, a otimização de desempenho é uma tarefa fundamental executada antes de estabelecer métricas de direcionamento para qualquer projeto.

Estas são algumas das principais áreas de foco nas quais você descobre e corrige problemas de desempenho antes que eles afetem os usuários.

## Platform {#platform}

Embora o Experience Manager seja suportado em várias plataformas, o Adobe encontrou o maior suporte para ferramentas nativas no Linux e no Windows, o que contribui para um desempenho ideal e para a facilidade de implementação. Idealmente, você deve implantar um sistema operacional de 64 bits para atender aos requisitos de alta memória de um [!DNL Experience Manager Assets] implantação. Como em qualquer implantação de Experience Manager, você deve implementar o TarMK sempre que possível. Embora o TarMK não possa ser dimensionado além de uma única instância de autor, seu desempenho é melhor do que o MongoMK. Você pode adicionar instâncias de descarregamento do TarMK para aumentar o poder de processamento do fluxo de trabalho do [!DNL Experience Manager Assets] implantação.

### Pasta temporária {#temp-folder}

Para melhorar os tempos de upload de ativos, use o armazenamento de alto desempenho para o diretório temporário Java. No Linux e no Windows, uma unidade RAM ou SSD pode ser usada. Em ambientes baseados em nuvem, um tipo equivalente de armazenamento de alta velocidade pode ser usado. Por exemplo, no Amazon EC2, uma variável [unidade efêmera](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) pode ser usada para a pasta temporária.

Supondo que o servidor tenha memória suficiente, configure uma unidade RAM. No Linux, execute estes comandos para criar uma unidade RAM de 8 GB:

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

No sistema operacional Windows, use um driver de terceiros para criar uma unidade de RAM ou use apenas armazenamento de dados de alto desempenho, como SSD.

Quando o volume temporário de alto desempenho estiver pronto, defina o parâmetro JVM `-Djava.io.tmpdir`. Por exemplo, você pode adicionar o parâmetro JVM abaixo à `CQ_JVM_OPTS` na variável `bin/start` script de [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configuração do Java {#java-configuration}

### Versão do Java {#java-version}

O Adobe recomenda a implantação [!DNL Experience Manager Assets] no Java 8 para obter o desempenho ideal.

<!-- TBD: Link to the latest official word around Java.
-->

### Parâmetros JVM {#jvm-parameters}

Defina os seguintes parâmetros JVM:

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## Armazenamento de dados e configuração de memória {#data-store-and-memory-configuration}

### Configuração do armazenamento de dados do arquivo {#file-data-store-configuration}

É recomendável separar o armazenamento de dados do armazenamento de segmentos para todos [!DNL Experience Manager Assets] usuários. Além disso, configurar o `maxCachedBinarySize` e `cacheSizeInMB` podem ajudar a maximizar o desempenho. Definir `maxCachedBinarySize` ao menor tamanho de arquivo que pode ser mantido no cache. Especifique o tamanho do cache em memória a ser usado para o armazenamento de dados no `cacheSizeInMB`. A Adobe recomenda que você defina esse valor entre 2 e 10 por cento do tamanho total do heap. No entanto, o teste de carga/desempenho pode ajudar a determinar a configuração ideal.

### Configurar o tamanho máximo do cache de imagens armazenadas em buffer {#configure-the-maximum-size-of-the-buffered-image-cache}

Ao fazer upload de grandes quantidades de ativos para [!DNL Adobe Experience Manager], para permitir picos inesperados no consumo de memória e evitar falhas de JVM com OutOfMemoryErrors, reduza o tamanho máximo configurado do cache de imagens armazenadas em buffer. Considere um exemplo de que você tem um sistema com um heap máximo (- `Xmx`param) de 5 GB, um Oak BlobCache definido em 1 GB e cache de documentos definido em 2 GB. Nesse caso, o cache em buffer levaria no máximo 1,25 GB e a memória, o que deixaria apenas 0,75 GB de memória para picos inesperados.

Configure o tamanho do cache em buffer no Console da Web do OSGi. Em `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, defina a propriedade `cq.dam.image.cache.max.memory` em bytes. Por exemplo, 1073741824 é de 1 GB (1024 x 1024 x 1024 = 1 GB).

Do Experience Manager 6.1 SP1, se você estiver usando um `sling:osgiConfig` para configurar essa propriedade, defina o tipo de dados como Longo. Para obter mais detalhes, consulte [CQBufferedImageCache consome heap durante uploads de ativos](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### Armazenamento de dados compartilhado {#shared-data-stores}

A implementação de um armazenamento de dados S3 ou de arquivo compartilhado pode ajudar a economizar espaço em disco e aumentar a taxa de transferência da rede em implementações de grande escala. Para obter mais informações sobre os prós e contras do uso de um armazenamento de dados compartilhado, consulte [Guia de dimensionamento de ativos](/help/assets/assets-sizing-guide.md).

### Armazenamento de dados S3 {#s-data-store}

A seguinte configuração do armazenamento de dados S3 ( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) ajudou o Adobe a extrair 12,8 TB de BLOBs (Binary Large Objects, grandes objetos binários) de um armazenamento de dados de arquivos existente em um armazenamento de dados S3 no local do cliente:

```conf
accessKey=<snip>
 secretKey=<snip>
 s3Bucket=<snip>
 s3Region=us-standard
 s3EndPoint=<a href="https://s3.amazonaws.com/">s3.amazonaws.com</a>
 connectionTimeout=120000
 socketTimeout=120000
 maxConnections=80
 writeThreads=60
 concurrentUploadsThreads=30
 asyncUploadLimit=30
 maxErrorRetry=1000
 path=/opt/author/crx-quickstart/repository/datastore
 s3RenameKeys=false
 s3Encryption=SSE_S3
 proactiveCaching=true
 uploadRetries=1000
 migrateFailuresCount=400
```

## Otimização de rede {#network-optimization}

A Adobe recomenda ativar o HTTPS porque muitas empresas têm firewalls que farejam tráfego HTTP, o que afeta negativamente os uploads e corrompe os arquivos. Para uploads de arquivos grandes, assegure-se de que os usuários tenham conexões com fio à rede, pois uma rede WiFi se torna rapidamente saturada. Para obter diretrizes sobre como identificar gargalos de rede, consulte [Guia de dimensionamento de ativos](/help/assets/assets-sizing-guide.md). Para avaliar o desempenho da rede analisando a topologia da rede, consulte [Considerações sobre a rede de ativos](/help/assets/assets-network-considerations.md).

Basicamente, sua estratégia de otimização de rede depende da quantidade de largura de banda disponível e da carga em sua [!DNL Experience Manager] instância. Opções comuns de configuração, incluindo firewalls ou proxies, podem ajudar a melhorar o desempenho da rede. Alguns pontos importantes a serem considerados:

* Dependendo do tipo de instância (pequena, moderada, grande), verifique se você tem largura de banda de rede suficiente para a instância do Experience Manager. A alocação adequada da largura de banda é especialmente importante se [!DNL Experience Manager] O está hospedado no AWS.
* Se o seu [!DNL Experience Manager] for hospedada no AWS, você poderá se beneficiar com uma política de dimensionamento versátil. Faça upload da instância se os usuários esperarem alta carga. Faça downsize para carga moderada/baixa.
* HTTPS: a maioria dos usuários tem firewalls que sniff tráfego HTTP, que pode afetar negativamente o upload de arquivos ou até mesmo arquivos corrompidos durante a operação de upload.
* Carregamentos de arquivos grandes: verifique se os usuários têm conexões com fio à rede (as conexões WiFi ficam saturadas rapidamente).

## Fluxos de trabalhos {#workflows}

### Workflows transitórios {#transient-workflows}

Sempre que possível, defina as [!UICONTROL Ativo de atualização DAM] fluxo de trabalho para Temporário. A configuração reduz significativamente as despesas gerais necessárias para processar workflows porque, nesse caso, os workflows não precisam passar pelos processos normais de rastreamento e arquivamento.

1. Navegue até `/miscadmin` no [!DNL Experience Manager] implantação em `https://[aem_server]:[port]/miscadmin`.

1. Expandir **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]** > **[!UICONTROL dam]**.

1. Abertura **[!UICONTROL Ativo de atualização DAM]**. No painel de ferramentas flutuante, alterne para a **[!UICONTROL Página]** e clique em **[!UICONTROL Propriedades da página]**.

1. Selecionar **[!UICONTROL Fluxo de trabalho transitório]** e clique em **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Alguns recursos não são compatíveis com fluxos de trabalho transitórios. Se o seu [!DNL Assets] A implantação requer esses recursos, não configure fluxos de trabalho transitórios.

Nos casos em que não for possível usar fluxos de trabalho transitórios, execute a limpeza regular do fluxo de trabalho para excluir os arquivados [!UICONTROL Ativo de atualização DAM] fluxos de trabalho para garantir que o desempenho do sistema não seja prejudicado.

Normalmente, execute os workflows de limpeza semanalmente. No entanto, em cenários de uso intensivo de recursos, como durante a assimilação de ativos em larga escala, é possível executá-los com mais frequência.

Para configurar a limpeza de fluxos de trabalho, adicione uma nova configuração de limpeza de fluxos de trabalho do Adobe Granite por meio do console OSGi. Em seguida, configure e programe o workflow como parte da janela de manutenção semanal.

Se a limpeza for executada por muito tempo, o tempo limite expirará. Portanto, você deve garantir que seus trabalhos de limpeza sejam concluídos para evitar situações em que a limpeza de workflows falhe devido ao alto número de workflows.

Por exemplo, após executar vários workflows não transitórios (que criam nós de instância de fluxo de trabalho), é possível executar [Removedor de fluxo de trabalho ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) numa basead hoc. Ele remove instâncias de fluxo de trabalho redundantes e concluídas imediatamente em vez de esperar que o programador de Limpeza de fluxo de trabalho do Adobe Granite seja executado.

### Máximo de trabalhos paralelos {#maximum-parallel-jobs}

Por padrão, [!DNL Experience Manager] O executa um número máximo de trabalhos paralelos igual ao número de processadores no servidor. O problema com essa configuração é que, durante períodos de carga pesada, todos os processadores são ocupados por [!UICONTROL Ativo de atualização DAM] fluxos de trabalho, retardando a capacidade de resposta da interface do usuário e evitando [!DNL Experience Manager] executar outros processos que protegem o desempenho e a estabilidade do servidor. Como prática recomendada, defina esse valor como metade dos processadores disponíveis no servidor, executando as seguintes etapas:

1. Ligado [!DNL Experience Manager] Autor, acesso `https://[aem_server]:[port]/system/console/slingevent`.

1. Clique em **[!UICONTROL Editar]** em cada fila de workflow relevante para sua implementação, por exemplo, **[!UICONTROL Fila de fluxo de trabalho transitório do Granite]**.

1. Atualize o valor de **[!UICONTROL Máximo de Trabalhos Paralelos]** e clique em **[!UICONTROL Salvar]**.

Para começar, definir uma fila como metade dos processadores disponíveis é uma solução viável. No entanto, talvez seja necessário aumentar ou diminuir esse número para atingir o throughput máximo e ajustá-lo por ambiente. Há filas separadas para fluxos de trabalho transitórios e não transitórios e outros processos, como fluxos de trabalho externos. Se várias filas definidas para 50% dos processadores estiverem ativas simultaneamente, o sistema pode ficar sobrecarregado rapidamente. As filas muito usadas variam muito entre as implementações do usuário. Portanto, talvez seja necessário configurá-los cuidadosamente para obter o máximo de eficiência sem sacrificar a estabilidade do servidor.

### Configuração do ativo de atualização DAM {#dam-update-asset-configuration}

A variável [!UICONTROL Ativo de atualização DAM] O fluxo de trabalho do contém um conjunto completo de etapas configuradas para tarefas, como geração de PTIFF do Dynamic Media e [!DNL Adobe InDesign Server] integração. No entanto, a maioria dos usuários pode não exigir várias dessas etapas. A Adobe recomenda criar uma cópia personalizada do [!UICONTROL Ativo de atualização DAM] fluxo de trabalho e remova todas as etapas desnecessárias. Nesse caso, atualize os iniciadores para [!UICONTROL Ativo de atualização DAM] para apontar para o novo modelo.

Execução da [!UICONTROL Ativo de atualização DAM] intensivamente pode aumentar drasticamente o tamanho do armazenamento de dados de arquivos. Os resultados de um experimento executado pelo Adobe mostraram que o tamanho do armazenamento de dados pode aumentar em aproximadamente 400 GB se cerca de 5.500 workflows forem executados em 8 horas.

É um aumento temporário e o armazenamento de dados é restaurado ao seu tamanho original após a execução da tarefa de coleta de lixo do armazenamento de dados.

Normalmente, a tarefa de coleta de lixo do armazenamento de dados é executada semanalmente, juntamente com outras tarefas de manutenção programadas.

Se você tiver um espaço limitado em disco e executar [!UICONTROL Ativo de atualização DAM] fluxos de trabalho intensivamente, considere agendar a tarefa de coleta de lixo com mais frequência.

#### Geração de representação em tempo de execução {#runtime-rendition-generation}

Os clientes usam imagens de vários tamanhos e formatos em todo o site ou para distribuição a parceiros comerciais. Como cada representação aumenta o espaço ocupado pelo ativo no repositório, a Adobe recomenda usar esse recurso criteriosamente. Para reduzir a quantidade de recursos necessários para processar e armazenar imagens, você pode gerar essas imagens em tempo de execução, em vez de representações durante a assimilação.

Muitos clientes do Sites implementam um servlet de imagem que redimensiona e recorta imagens no momento em que são solicitadas, o que impõe carga adicional na instância de publicação. No entanto, desde que essas imagens possam ser armazenadas em cache, o desafio pode ser atenuado.

Uma abordagem alternativa é usar a tecnologia Dynamic Media para transmitir completamente a manipulação de imagem. Além disso, é possível implantar o Brand Portal que não apenas assume as responsabilidades de geração de representação da [!DNL Experience Manager] infraestrutura, mas também todo o nível de publicação.

#### ImageMagick {#imagemagick}

Se você personalizar a variável [!UICONTROL Ativo de atualização DAM] para gerar representações usando o ImageMagick, a Adobe recomenda que você modifique a variável `policy.xml` arquivo em `/etc/ImageMagick/`. Por padrão, o ImageMagick usa todo o espaço em disco disponível no volume do SO e a memória disponível. Faça as seguintes alterações de configuração no `policymap` seção de `policy.xml` para limitar esses recursos.

```xml
<policymap>
  <!-- <policy domain="system" name="precision" value="6"/> -->
  <policy domain="resource" name="temporary-path" value="/ephemeral0/imagemagick_tmp"/>
  <policy domain="resource" name="memory" value="1000MiB"/>
  <policy domain="resource" name="map" value="1000MiB"/>
  <!-- <policy domain="resource" name="area" value="1gb"/> -->
  <policy domain="resource" name="disk" value="10000MiB"/>
  <!-- <policy domain="resource" name="file" value="768"/> -->
  <policy domain="resource" name="thread" value="1"/>
  <policy domain="resource" name="throttle" value="50"/>
  <!-- <policy domain="resource" name="time" value="3600"/> -->
</policymap>
```

Além disso, defina o caminho da pasta temporária do ImageMagick no `configure.xml` arquivo (ou definindo a variável de ambiente `MAGICK_TEMPORARY_PATH`) para uma partição de disco que tenha espaço suficiente e IOPS.

>[!CAUTION]
>
>Uma configuração incorreta pode tornar o servidor instável se o ImageMagick usar todo o espaço disponível em disco. As alterações de política necessárias para processar arquivos grandes usando o ImageMagick podem afetar o [!DNL Experience Manager] desempenho. Para obter mais informações, consulte [instalar e configurar o ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>O ImageMagick `policy.xml` e `configure.xml` os arquivos estão disponíveis em `/usr/lib64/ImageMagick-&#42;/config/` em vez de `/etc/ImageMagick/`.Consulte [Documentação do ImageMagick](https://www.imagemagick.org/script/resources.php) para localização dos arquivos de configuração.

Se você estiver usando [!DNL Experience Manager] no Adobe Managed Services (AMS), entre em contato com o Suporte ao cliente do Adobe se planejar processar muitos arquivos PSD ou PSB grandes. Trabalhe com o representante do Suporte ao cliente da Adobe para implementar essas práticas recomendadas para a implantação do AMS e escolher as melhores ferramentas e modelos possíveis para os formatos proprietários do Adobe. [!DNL Experience Manager] O não pode processar arquivos PSB de resolução muito alta com mais de 30.000 x 23.000 pixels.

### Writeback XMP {#xmp-writeback}

O writeback XMP atualiza o ativo original sempre que os metadados forem modificados no [!DNL Experience Manager], que resulta no seguinte:

* O ativo em si é modificado
* Uma versão do ativo é criada
* [!UICONTROL Ativo de atualização DAM] é executado no ativo

Os resultados listados consomem recursos consideráveis. Portanto, o Adobe recomenda desativar o writeback XMP se não for necessário. Para obter mais informações, consulte [Writeback XMP](/help/assets/xmp-writeback.md).

A importação de uma grande quantidade de metadados pode resultar em uma atividade de writeback XMP com muitos recursos se o sinalizador executar workflows estiver marcado. Planejar essa importação durante o uso do servidor enxuto para que o desempenho de outros usuários não seja afetado.

## Replicação {#replication}

Ao replicar ativos para um grande número de instâncias de publicação, por exemplo, em uma implementação do Sites, o Adobe recomenda usar a replicação em cadeia. Nesse caso, a instância do autor é replicada para uma única instância de publicação que, por sua vez, é replicada para as outras instâncias de publicação, liberando a instância do autor.

### Configurar replicação em cadeia {#configure-chain-replication}

1. Escolha a instância de publicação que deseja usar para encadear as replicações
1. Nessa instância de publicação, adicione agentes de replicação que apontem para as outras instâncias de publicação
1. Em cada um desses agentes de replicação, ative a opção &quot;No recebimento&quot; na guia &quot;Acionadores&quot;

>[!NOTE]
>
>O Adobe não recomenda a ativação automática de ativos. No entanto, se necessário, o Adobe recomenda fazer isso como a etapa final em um fluxo de trabalho, geralmente Atualizar ativo do DAM.

## Pesquisar índices {#search-indexes}

Instalar [os Service Packs mais recentes](/help/release-notes/release-notes.md) e hotfixes relacionados ao desempenho, pois esses geralmente incluem atualizações de índices do sistema. Consulte [dicas de ajuste de desempenho](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/performance-tuning-guidelines.html?lang=en) para algumas otimizações de índice.

Crie índices personalizados para consultas executadas com frequência. Para obter detalhes, consulte [metodologia para analisar consultas lentas](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) e [criação de índices personalizados](/help/sites-deploying/queries-and-indexing.md). Para obter insights adicionais sobre as práticas recomendadas de consulta e índice, consulte [Práticas recomendadas para consultas e indexação](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Configurações de índice Lucene {#lucene-index-configurations}

Algumas otimizações podem ser feitas nas configurações de índice do Oak que podem ajudar a melhorar o [!DNL Experience Manager Assets] desempenho. Atualize as configurações de índice para melhorar o tempo de reindexação:

1. Abrir CRXDe `/crx/de/index.jsp` e efetuar login como um usuário administrativo.
1. Navegue até `/oak:index/lucene`.
1. Adicionar um `String[]` propriedade `excludedPaths` com valores `/var`, `/etc/workflow/instances`, e `/etc/replication`.
1. Navegue até `/oak:index/damAssetLucene`. Adicionar um `String[]` propriedade `includedPaths` com valor `/content/dam`. Salve as alterações.

Se os usuários não precisarem fazer uma pesquisa de texto completo de ativos, por exemplo, pesquisar texto em documentos do PDF e desativá-la. Você melhora o desempenho do índice desabilitando a indexação de texto completo. Para desativar [!DNL Apache Lucene] para extração de texto, siga estas etapas:

1. Entrada [!DNL Experience Manager] interface, acesso [!UICONTROL Gerenciador de pacotes].
1. Carregue e instale o pacote disponível em [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Estimar Total {#guess-total}

Ao criar consultas que geram grandes conjuntos de resultados, use o `guessTotal` para evitar a utilização intensa da memória durante sua execução.

## Problemas conhecidos {#known-issues}

### Arquivos grandes {#large-files}

Há dois problemas principais conhecidos relacionados a arquivos grandes no [!DNL Experience Manager]. Quando os arquivos atingem tamanhos maiores que 2 GB, a sincronização em espera forçada pode ficar em uma situação de falta de memória. Em alguns casos, impede a execução da sincronização em standby. Em outros casos, isso causa uma falha na instância principal. Este cenário se aplica a qualquer arquivo em [!DNL Experience Manager] maior que 2 GB, incluindo pacotes de conteúdo.

Da mesma forma, quando os arquivos atingem 2 GB de tamanho ao usar um armazenamento de dados S3 compartilhado, pode levar algum tempo para que o arquivo seja totalmente mantido do cache para o sistema de arquivos. Como resultado, ao usar a replicação sem binários, é possível que os dados binários não tenham sido mantidos antes da conclusão da replicação. Essa situação pode levar a problemas, especialmente se a disponibilidade dos dados for importante.

## Teste de desempenho {#performance-testing}

Para cada [!DNL Experience Manager] estabelecer um regime de testes de desempenho que possa identificar e resolver gargalos rapidamente. Estas são algumas áreas importantes para se concentrar.

### Teste de rede {#network-testing}

Para todas as questões de desempenho de rede do cliente, execute as seguintes tarefas:

* Testar o desempenho da rede na rede do cliente
* Teste o desempenho da rede na rede Adobe. Para clientes do AMS, trabalhe com seu CSE para testar na rede Adobe.
* Testar o desempenho da rede de outro ponto de acesso
* Ao usar uma ferramenta de referencial de rede
* Testar no dispatcher

### [!DNL Experience Manager] teste de implantação {#aem-deployment-testing}

Para minimizar a latência e alcançar alto throughput através da utilização eficiente da CPU e do compartilhamento de carga, monitore o desempenho do [!DNL Experience Manager] regularmente. Em especial:

* Executar testes de carga em relação ao [!DNL Experience Manager] implantação.
* Monitore o desempenho do upload e a capacidade de resposta da interface.

## [!DNL Experience Manager Assets] lista de verificação de desempenho e impacto das tarefas de gerenciamento de ativos {#checklist}

* Habilite o HTTPS para contornar qualquer farejador de tráfego HTTP corporativo.
* Use uma conexão com fio para uploads pesados de ativos.
* Implantar no Java 8.
* Defina os parâmetros JVM ideais.
* Configure um DataStore do Sistema de Arquivos ou um armazenamento de dados S3.
* Desative a geração de subativos. Se estiver ativado, o fluxo de trabalho do AEM cria um ativo separado para cada página em um ativo de várias páginas. Cada uma dessas páginas é um ativo individual que consome mais espaço em disco, requer controle de versão e processamento adicional de fluxo de trabalho. Se você não precisar de páginas separadas, desative as atividades de geração de subativos e extração de página.
* Habilite fluxos de trabalho transitórios.
* Ajuste as filas de fluxo de trabalho do Granite para limitar as tarefas simultâneas.
* Configurar [!DNL ImageMagick] para limitar o consumo de recursos.
* Remova etapas desnecessárias do [!UICONTROL Ativo de atualização DAM] fluxo de trabalho.
* Configure a limpeza de fluxo de trabalho e versão.
* Otimize índices com os Service Packs e hotfixes mais recentes. Consulte o Suporte ao cliente do Adobe para obter as otimizações de índice adicionais que podem estar disponíveis.
* Use guessTotal para otimizar o desempenho da consulta.
* Se você configurar [!DNL Experience Manager] para detectar tipos de arquivos a partir do conteúdo dos arquivos (habilitando **[!UICONTROL Serviço de tipo DAM Mime do DAM do Day CQ]** no **[!UICONTROL Console da Web AEM]**), carregue muitos arquivos em massa durante horas que não sejam de pico, pois consome muitos recursos.
