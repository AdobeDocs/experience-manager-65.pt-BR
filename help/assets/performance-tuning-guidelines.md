---
title: Ajuste de desempenho para [!DNL Adobe Experience Manager Assets].
description: Sugestões e orientações [!DNL Experience Manager] sobre configuração, alterações no hardware, software e componentes de rede para remover gargalos e otimizar o desempenho [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 5a421c66930d8c7a9eb633c707b4b51d4549b303
workflow-type: tm+mt
source-wordcount: '2746'
ht-degree: 0%

---


<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] guia de ajuste de desempenho {#assets-performance-tuning-guide}

Uma [!DNL Experience Manager Assets] configuração contém vários componentes de hardware, software e rede. Dependendo do cenário de implantação, talvez você precise de alterações específicas na configuração de hardware, software e componentes de rede para remover gargalos de desempenho.

Além disso, identificar e seguir determinadas diretrizes de otimização de hardware e software ajuda a criar uma base sólida que permite que sua [!DNL Experience Manager Assets] implantação atenda às expectativas de desempenho, escalabilidade e confiabilidade.

O baixo desempenho no pode [!DNL Experience Manager Assets] afetar a experiência do usuário em relação ao desempenho interativo, processamento de ativos, velocidade de download e outras áreas.

Na verdade, a otimização do desempenho é uma tarefa fundamental que você executa antes de estabelecer métricas de público alvo para qualquer projeto.

Estas são algumas áreas de foco chave em torno das quais você descobre e corrige problemas de desempenho antes que eles afetem os usuários.

## Plataforma {#platform}

Embora o Experience Manager seja suportado em várias plataformas, o Adobe encontrou o maior suporte para ferramentas nativas no Linux e no Windows, o que contribui para o desempenho otimizado e para a facilidade de implementação. Idealmente, você deve implantar um sistema operacional de 64 bits para atender aos altos requisitos de memória de uma [!DNL Experience Manager Assets] implantação. Assim como com qualquer implantação de Experience Manager, você deve implementar o TarMK sempre que possível. Embora o TarMK não possa ser dimensionado além de uma única instância do autor, ele tem um desempenho melhor do que o MongoMK. Você pode adicionar instâncias de descarregamento TarMK para aumentar o poder de processamento do fluxo de trabalho de sua [!DNL Experience Manager Assets] implantação.

### Pasta temporária {#temp-folder}

Para melhorar os tempos de upload de ativos, use o armazenamento de alto desempenho para o diretório temporário Java. No Linux e no Windows, uma unidade de RAM ou SSD pode ser usada. Em ambientes baseados em nuvem, um tipo de armazenamento de alta velocidade equivalente pode ser usado. Por exemplo, no Amazon EC2, uma unidade [efêmera](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) pode ser usada para a pasta temporária.

Supondo que o servidor tenha ampla memória, configure uma unidade RAM. No Linux, execute estes comandos para criar uma unidade de 8 GB de RAM:

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

No SO Windows, use um driver de terceiros para criar uma unidade RAM ou use apenas um armazenamento de alto desempenho, como SSD.

Quando o volume temporário de alto desempenho estiver pronto, defina o parâmetro JVM `-Djava.io.tmpdir`. Por exemplo, você pode adicionar o parâmetro JVM abaixo à `CQ_JVM_OPTS` variável no `bin/start` script de [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configuração do Java {#java-configuration}

### Versão do Java {#java-version}

A Adobe recomenda implantar [!DNL Experience Manager Assets] no Java 8 para obter desempenho ideal.

<!-- TBD: Link to the latest official word around Java.
-->

### Parâmetros JVM {#jvm-parameters}

Defina os seguintes parâmetros JVM:

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=verdadeiro

## Configuração do armazenamento de dados e da memória {#data-store-and-memory-configuration}

### Configuração do armazenamento de dados de arquivo {#file-data-store-configuration}

É recomendável separar o armazenamento de dados do armazenamento de segmentos para todos os [!DNL Experience Manager Assets] usuários. Além disso, configurar os parâmetros `maxCachedBinarySize` e `cacheSizeInMB` pode ajudar a maximizar o desempenho. Defina `maxCachedBinarySize` para o menor tamanho de arquivo que pode ser mantido no cache. Especifique o tamanho do cache na memória a ser usado para o armazenamento de dados no `cacheSizeInMB`. O Adobe recomenda que você defina esse valor entre 2 a 10% do tamanho total do heap. No entanto, o teste de carga/desempenho pode ajudar a determinar a configuração ideal.

### Configurar o tamanho máximo do cache de imagem em buffer {#configure-the-maximum-size-of-the-buffered-image-cache}

Ao fazer upload de grandes quantidades de ativos para [!DNL Adobe Experience Manager], para permitir picos inesperados no consumo de memória e para evitar falhas de JVM com OutOfMemoryErrors, reduza o tamanho máximo configurado do cache de imagem em buffer. Considere um exemplo de que você tem um sistema com um heap ( `Xmx`param) máximo de 5 GB, um BlobCache Oak definido em 1 GB e um cache de documento definido em 2 GB. Nesse caso, o cache armazenado em buffer levaria no máximo 1,25 GB e memória, o que deixaria apenas 0,75 GB de memória para picos inesperados.

Configure o tamanho do cache armazenado em buffer no console da Web OSGi. Em `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, defina a propriedade `cq.dam.image.cache.max.memory` em bytes. Por exemplo, 1073741824 é 1 GB (1024 x 1024 x 1024 = 1 GB).

No Experience Manager 6.1 SP1, se você estiver usando um `sling:osgiConfig` nó para configurar essa propriedade, certifique-se de definir o tipo de dados como Longo. Para obter mais detalhes, consulte [CQBufferedImageCache consome heap durante os uploads](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)do ativo.

### Armazenamentos de dados compartilhados {#shared-data-stores}

A implementação de um armazenamento de dados de arquivos compartilhados ou S3 pode ajudar a economizar espaço em disco e aumentar o throughput da rede em implementações de larga escala. Para obter mais informações sobre os prós e contras de usar um armazenamento de dados compartilhado, consulte o guia [de dimensionamento de](/help/assets/assets-sizing-guide.md)ativos.

### S3 data store {#s-data-store}

A seguinte configuração do S3 Data Store ( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) ajudou a Adobe extrair 12,8 TB de BLOBs (objetos grandes binários) de um armazenamento de dados de arquivo existente para um armazenamento de dados S3 em um local do cliente:

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

## Otimização da rede {#network-optimization}

O Adobe recomenda habilitar o HTTPS porque muitas empresas têm firewalls que cheiram o tráfego HTTP, o que afeta negativamente os uploads e corrompe os arquivos. Para fazer uploads de arquivos grandes, verifique se os usuários têm conexões com fio à rede, pois uma rede WiFi fica rapidamente saturada. Para obter diretrizes sobre como identificar gargalos de rede, consulte o guia [de dimensionamento de](/help/assets/assets-sizing-guide.md)ativos. Para avaliar o desempenho da rede analisando a topologia da rede, consulte Considerações [de rede do](/help/assets/assets-network-considerations.md)Assets.

Primariamente, sua estratégia de otimização de rede depende da quantidade de largura de banda disponível e da carga da sua [!DNL Experience Manager] instância. Opções comuns de configuração, incluindo firewalls ou proxies, podem ajudar a melhorar o desempenho da rede. Estes são alguns pontos-chave que devem ser levados em conta:

* Dependendo do tipo de instância (pequena, moderada, grande), verifique se você tem largura de banda de rede suficiente para a instância do Experience Manager. A alocação de largura de banda adequada é especialmente importante se [!DNL Experience Manager] for hospedada no AWS.
* Se sua [!DNL Experience Manager] instância estiver hospedada no AWS, você poderá se beneficiar se tiver uma política de dimensionamento versátil. Atualize a instância se os usuários esperarem carga alta. Baixe-o para uma carga moderada/baixa.
* HTTPS: A maioria dos usuários tem firewalls que cheiram o tráfego HTTP, o que pode afetar negativamente o carregamento de arquivos ou até mesmo arquivos corrompidos durante a operação de upload.
* Carregamentos de arquivos grandes: Verifique se os usuários têm conexões com fio à rede (as conexões WiFi se saturam rapidamente).

## Fluxos de trabalhos {#workflows}

### Workflows transitórios {#transient-workflows}

Sempre que possível, defina o fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM como Transitório. A configuração reduz significativamente os custos indiretos necessários para processar workflows porque, nesse caso, os workflows não precisam passar pelos processos normais de rastreamento e arquivamento.

1. Navegue até `/miscadmin` na [!DNL Experience Manager] implantação em `https://[aem_server]:[port]/miscadmin`.

1. Expanda **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]** > **[!UICONTROL dam]**.

1. Abra Ativo **[!UICONTROL de atualização do]** DAM. No painel de ferramentas flutuante, alterne para a guia **[!UICONTROL Página]** e clique em Propriedades **** da página.

1. Select **[!UICONTROL Transient Workflow]** and click **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Alguns recursos não suportam workflows transitórios. Se sua [!DNL Assets] implantação exigir esses recursos, não configure workflows transitórios.

Nos casos em que workflows transitórios não podem ser usados, execute a remoção regular do fluxo de trabalho para excluir workflows arquivados de ativos [!UICONTROL de atualização de] DAM para garantir que o desempenho do sistema não diminua.

Geralmente, execute os workflows de expurgação semanalmente. No entanto, em cenários com uso intenso de recursos, como durante a assimilação de ativos em larga escala, você pode executá-los com mais frequência.

Para configurar a expurgação do fluxo de trabalho, adicione uma nova configuração de Expurgação do fluxo de trabalho de Adobe Granite por meio do console OSGi. Em seguida, configure e agende o fluxo de trabalho como parte da janela de manutenção semanal.

Se a limpeza for longa demais, ela expira. Portanto, você deve garantir que as tarefas de purga sejam concluídas para evitar situações em que workflows de expurgação não sejam concluídos devido ao alto número de workflows.

Por exemplo, após executar vários workflows não transitórios (que criam nós de instância do fluxo de trabalho), você pode executar o [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) de forma ad-hoc. Ele remove instâncias de fluxo de trabalho redundantes e concluídas imediatamente, em vez de aguardar a execução do scheduler Adobe Granite Workflow Purge.

### Máximo de trabalhos paralelos {#maximum-parallel-jobs}

Por padrão, [!DNL Experience Manager] executa um número máximo de trabalhos paralelos igual ao número de processadores no servidor. O problema com essa configuração é que durante períodos de carga pesada, todos os processadores são ocupados por workflows de ativos [!UICONTROL de atualização do] DAM, retardando a capacidade de resposta da interface do usuário e impedindo a execução [!DNL Experience Manager] de outros processos que salvaguardem o desempenho e a estabilidade do servidor. Como prática recomendada, defina esse valor para metade dos processadores disponíveis no servidor, executando as seguintes etapas:

1. Em [!DNL Experience Manager] Autor, acesse `https://[aem_server]:[port]/system/console/slingevent`.

1. Clique em **[!UICONTROL Editar]** em cada fila de fluxo de trabalho relevante para sua implementação, por exemplo, Fila **[!UICONTROL de fluxo de trabalho temporário de]** granite.

1. Atualize o valor de **[!UICONTROL Máximo de Trabalhos]** Paralelos e clique em **[!UICONTROL Salvar]**.

Configurar uma fila para metade dos processadores disponíveis é uma solução viável para o start. No entanto, talvez seja necessário aumentar ou diminuir esse número para atingir o throughput máximo e ajustá-lo por ambiente. Há filas separadas para workflows transitórios e não transitórios, bem como outros processos, como workflows externos. Se várias filas definidas como 50% dos processadores estiverem ativos simultaneamente, o sistema poderá ser sobrecarregado rapidamente. As filas muito usadas variam muito entre as implementações do usuário. Portanto, talvez seja necessário configurá-los cuidadosamente para obter a máxima eficiência sem sacrificar a estabilidade do servidor.

### Configuração do ativo de atualização do DAM {#dam-update-asset-configuration}

O fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM contém um conjunto completo de etapas configuradas para tarefa, como geração e integração do Scene7 PTIFF [!DNL Adobe InDesign Server] . No entanto, a maioria dos usuários pode não exigir várias dessas etapas. O Adobe recomenda que você crie uma cópia personalizada do modelo de fluxo de trabalho Atualizar ativo  DAM e remova quaisquer etapas desnecessárias. Nesse caso, atualize os iniciadores do Ativo [!UICONTROL de atualização do] DAM para apontar para o novo modelo.

A execução intensiva do fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM pode aumentar consideravelmente o tamanho do armazenamento de dados do arquivo. Os resultados de uma experiência realizada pelo Adobe demonstraram que o tamanho do armazenamento de dados pode aumentar aproximadamente 400 GB se cerca de 5500 workflows forem executados em 8 horas.

É um aumento temporário e o armazenamento de dados é restaurado para seu tamanho original depois que você executa a tarefa de coleta de lixo do armazenamento de dados.

Normalmente, a tarefa de coleta de lixo do armazenamento de dados é executada semanalmente junto com outras tarefas de manutenção programadas.

Se você tiver um espaço em disco limitado e executar workflows de ativos [!UICONTROL de atualização de] DAM intensamente, considere programar a tarefa de coleta de lixo com mais frequência.

#### Geração de execução em tempo de execução {#runtime-rendition-generation}

Os clientes usam imagens de vários tamanhos e formatos em seu site ou para distribuição a parceiros comerciais. Como cada representação adiciona ao espaço ocupado do ativo no repositório, o Adobe recomenda usar esse recurso de forma criteriosa. Para reduzir a quantidade de recursos necessários para processar e armazenar imagens, é possível gerar essas imagens em tempo de execução em vez de representações durante a ingestão.

Muitos clientes do Sites implementam um servlet de imagem que redimensiona e corta imagens no momento em que são solicitadas, o que impõe carga adicional na instância de publicação. Entretanto, enquanto essas imagens puderem ser armazenadas em cache, o desafio poderá ser atenuado.

Uma abordagem alternativa é usar a tecnologia Scene7 para entregar a manipulação da imagem totalmente. Além disso, você pode implantar o Brand Portal que não somente assume as responsabilidades de geração de execução da [!DNL Experience Manager] infraestrutura, mas também toda a camada de publicação.

#### ImageMagick {#imagemagick}

Se você personalizar o fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM para gerar representações usando o ImageMagick, o Adobe recomenda que você modifique o `policy.xml` arquivo em `/etc/ImageMagick/`. Por padrão, o ImageMagick usa todo o espaço em disco disponível no volume do SO e na memória disponível. Faça as seguintes alterações de configuração na `policymap` seção de `policy.xml` para limitar esses recursos.

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

Além disso, defina o caminho da pasta temporária do ImageMagick no arquivo `configure.xml` (ou definindo a variável de ambiente `MAGIC_TEMPORARY_PATH`) para uma partição de disco que tenha espaço suficiente e IOPS.

>[!CAUTION]
>
>Uma configuração incorreta pode tornar o servidor instável se o ImageMagick usar todo o espaço em disco disponível. As alterações de política necessárias para processar arquivos grandes usando o ImageMagick podem afetar o desempenho do Experience Manager [!DNLE] . Para obter mais informações, consulte [instalar e configurar o ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>Os arquivos ImageMagick `policy.xml` e `configure.xml` ImageMagick estão disponíveis em `/usr/lib64/ImageMagick-&#42;/config/` vez de `/etc/ImageMagick/`.Consulte a documentação [do](https://www.imagemagick.org/script/resources.php) ImageMagick para obter o local dos arquivos de configuração.

Se você estiver usando [!DNL Experience Manager] o Adobe Managed Services (AMS), entre em contato com o Atendimento ao cliente do Adobe se planeja processar vários arquivos PSD ou PSB grandes. Trabalhe com o representante do Atendimento ao cliente da Adobe para implementar essas práticas recomendadas para sua implantação do AMS e escolher as melhores ferramentas e modelos possíveis para os formatos proprietários do Adobe. [!DNL Experience Manager] pode não processar arquivos PSB de alta resolução com mais de 30000 x 23000 pixels.

### XMP writeback {#xmp-writeback}

XMP write-back atualiza o ativo original sempre que os metadados são modificados em [!DNL Experience Manager], o que resulta no seguinte:

* O próprio ativo é modificado
* Uma versão do ativo é criada
* [!UICONTROL O Ativo] de atualização DAM é executado no ativo

Os resultados listados consomem recursos consideráveis. Portanto, o Adobe recomenda [desativar XMP Writeback](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html), se não for necessário.

A importação de uma grande quantidade de metadados pode resultar em atividade de repetição de gravação de XMP com muitos recursos se o sinalizador workflows de execução estiver marcado. Planeje tal importação durante o uso de servidor simplificado para que o desempenho para outros usuários não seja afetado.

## Replicação {#replication}

Ao replicar ativos para um grande número de instâncias de publicação, por exemplo em uma implementação do Sites, o Adobe recomenda o uso da replicação em cadeia. Nesse caso, a instância do autor é replicada para uma única instância de publicação que, por sua vez, é replicada para outras instâncias de publicação, liberando a instância do autor.

### Configurar replicação em cadeia {#configure-chain-replication}

1. Escolha a instância de publicação que deseja usar para encadear as replicações em
1. Nessa instância de publicação, adicione agentes de replicação que apontem para outras instâncias de publicação
1. Em cada um desses agentes de replicação, ative &quot;Ao receber&quot; na guia &quot;Acionadores&quot;

>[!NOTE]
>
>O Adobe não recomenda a ativação automática de ativos. No entanto, se necessário, o Adobe recomenda fazer isso como a etapa final em um fluxo de trabalho, normalmente o Ativo de atualização do DAM.

## Índices de pesquisa {#search-indexes}

Certifique-se de implementar os service packs mais recentes e os hotfixes relacionados ao desempenho, pois eles frequentemente incluem atualizações para índices do sistema. Consulte Dicas [de ajuste de](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) desempenho para obter algumas otimizações de índice.

Crie índices personalizados para query executados com frequência. Para obter detalhes, consulte a [metodologia para analisar query](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) lentos e [criar índices](/help/sites-deploying/queries-and-indexing.md)personalizados. Para obter informações adicionais sobre as práticas recomendadas de query e índice, consulte Práticas [recomendadas para Query e indexação](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Configurações do índice Lucene {#lucene-index-configurations}

Algumas otimizações podem ser feitas nas configurações de índice Oak que podem ajudar a melhorar o [!DNL Experience Manager Assets] desempenho. Atualize as configurações de índice para melhorar o tempo de reindexação:

1. Abra o CRXDe `/crx/de/index.jsp` faça logon como um usuário administrativo.
1. Navegue até `/oak:index/lucene`.
1. Adicione uma `String[]` propriedade `excludedPaths` com valores `/var`, `/etc/workflow/instances`e `/etc/replication`.
1. Navegue até `/oak:index/damAssetLucene`. Adicione uma `String[]` propriedade `includedPaths` com valor `/content/dam`. Salve as alterações.

Se os usuários não precisarem fazer uma pesquisa de texto completo de ativos, por exemplo, pesquisar texto em documentos PDF e desativá-lo. Você aprimora o desempenho do índice ao desativar a indexação de texto completo. Para desativar a extração [!DNL Apache Lucene] de texto, siga estas etapas:

1. Na [!DNL Experience Manager] interface, acesse [!UICONTROL Gerenciador]de pacotes.
1. Carregue e instale o pacote disponível em [disable_indexingbinarytextextract-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Total de suposições {#guess-total}

Ao criar query que geram grandes conjuntos de resultados, use o `guessTotal` parâmetro para evitar a utilização de memória pesada ao executá-los.

## Problemas conhecidos {#known-issues}

### Arquivos grandes {#large-files}

Há dois problemas conhecidos principais relacionados a arquivos grandes em [!DNL Experience Manager]. Quando os arquivos atingem tamanhos superiores a 2 GB, a sincronização em espera fria pode ocorrer em uma situação de falta de memória. Em alguns casos, impede que a sincronização em espera seja executada. Em outros casos, isso faz com que a instância primária falhe. Esse cenário se aplica a qualquer arquivo com [!DNL Experience Manager] mais de 2 GB, incluindo pacotes de conteúdo.

Da mesma forma, quando os arquivos atingem 2 GB ao usar um armazenamento de dados S3 compartilhado, pode levar algum tempo para que o arquivo seja totalmente persistente do cache para o sistema de arquivos. Como resultado, ao usar replicação sem binários, é possível que os dados binários não tenham sido persistentes antes da conclusão da replicação. Essa situação pode levar a problemas, especialmente se a disponibilidade de dados for importante.

## Teste de desempenho {#performance-testing}

Para cada [!DNL Experience Manager] implantação, estabeleça um regime de teste de desempenho que possa identificar e resolver gargalos rapidamente. Aqui estão algumas áreas-chave para se focar.

### Teste de rede {#network-testing}

Para todas as preocupações de desempenho de rede do cliente, execute as seguintes tarefas:

* Teste o desempenho da rede na rede do cliente
* Teste o desempenho da rede a partir da rede Adobe. Para clientes do AMS, trabalhe com seu CSE para testar a partir da rede do Adobe.
* Testar o desempenho da rede de outro ponto de acesso
* Usando uma ferramenta de benchmark de rede
* Teste contra o expedidor

### [!DNL Experience Manager] teste implantação {#aem-deployment-testing}

Para minimizar a latência e alcançar alta throughput através da utilização eficiente da CPU e do compartilhamento de carga, monitore o desempenho da sua [!DNL Experience Manager] implantação regularmente. Nomeadamente:

* Execute testes de carga na [!DNL Experience Manager] implantação.
* Monitore o desempenho de upload e a capacidade de resposta da interface do usuário.

## [!DNL Experience Manager Assets] lista de verificação de desempenho e impacto das tarefas de gerenciamento de ativos {#checklist}

* Ative o HTTPS para contornar qualquer farejador de tráfego HTTP corporativo.
* Use uma conexão com fio para fazer upload de ativos pesados.
* Implantar no Java 8.
* Defina os parâmetros JVM ideais.
* Configure um DataStore do sistema de arquivos ou um armazenamento de dados S3.
* Desabilitar a geração de subativos. Se estiver ativado, AEM fluxo de trabalho cria um ativo separado para cada página em um ativo de várias páginas. Cada uma dessas páginas é um ativo individual que consome mais espaço em disco, requer controle de versão e processamento de fluxo de trabalho adicional. Se você não precisar de páginas separadas, desabilite a geração de subativos e atividades de extração de página.
* Ative workflows transitórios.
* Ajuste as filas de fluxo de trabalho Granite para limitar as tarefas simultâneas.
* Configure [!DNL ImageMagick] para limitar o consumo de recursos.
* Remova etapas desnecessárias do fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM.
* Configure o fluxo de trabalho e a remoção de versão.
* Otimize índices com os service packs e hotfixes mais recentes. Consulte o Atendimento ao cliente do Adobe para obter outras otimizações de índice que possam estar disponíveis.
* Use a opção supyTotal para otimizar o desempenho do query.
* If you configure [!DNL Experience Manager] to detect file types from the content of the files (by enabling **[!UICONTROL Day CQ DAM Mime Type Service]** in the **[!UICONTROL AEM Web Console]**), upload many files in bulk during non-peak hours as it is resource-intensive.
