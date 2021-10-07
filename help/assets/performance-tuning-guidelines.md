---
title: Ajuste de desempenho [!DNL Assets].
description: Sugestões e orientações sobre a configuração [!DNL Experience Manager] e alterações no hardware, software e componentes de rede para remover gargalos e otimizar o desempenho de [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '2741'
ht-degree: 0%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] guia de ajuste de desempenho {#assets-performance-tuning-guide}

Uma configuração [!DNL Experience Manager Assets] contém vários componentes de hardware, software e rede. Dependendo do seu cenário de implantação, você pode exigir alterações específicas na configuração de hardware, software e componentes de rede para remover gargalos de desempenho.

Além disso, identificar e seguir determinadas diretrizes de otimização de hardware e software ajuda a criar uma base sólida que permite que sua [!DNL Experience Manager Assets] implantação atenda às expectativas sobre desempenho, escalabilidade e confiabilidade.

O baixo desempenho em [!DNL Experience Manager Assets] pode afetar a experiência do usuário em relação ao desempenho interativo, processamento de ativos, velocidade de download e outras áreas.

Na verdade, a otimização de desempenho é uma tarefa fundamental que você executa antes de estabelecer métricas de destino para qualquer projeto.

Estas são algumas das principais áreas de foco sobre as quais você descobre e corrige problemas de desempenho antes que eles tenham impacto nos usuários.

## Plataforma {#platform}

Embora o Experience Manager seja compatível com várias plataformas, o Adobe encontrou o maior suporte para ferramentas nativas no Linux e no Windows, o que contribui para um desempenho ideal e para a facilidade de implementação. Idealmente, você deve implantar um sistema operacional de 64 bits para atender aos altos requisitos de memória de uma implantação [!DNL Experience Manager Assets]. Assim como em qualquer implantação do Experience Manager, você deve implementar o TarMK sempre que possível. Embora o TarMK não possa ser dimensionado além de uma única instância de autor, ele tem um desempenho melhor do que o MongoMK. Você pode adicionar instâncias de descarregamento do TarMK para aumentar o poder de processamento do workflow de sua implantação [!DNL Experience Manager Assets].

### Pasta temporária {#temp-folder}

Para melhorar os tempos de upload do ativo, use o armazenamento de alto desempenho para o diretório temporário Java. No Linux e no Windows, uma unidade RAM ou SSD pode ser usada. Em ambientes baseados em nuvem, um tipo de armazenamento de alta velocidade equivalente pode ser usado. Por exemplo, no Amazon EC2, uma unidade [efêmera](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) pode ser usada para a pasta temporária.

Supondo que o servidor tenha ampla memória, configure uma unidade RAM. No Linux, execute estes comandos para criar uma unidade RAM de 8 GB:

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

No sistema operacional Windows, use um driver de terceiros para criar uma unidade RAM ou use apenas armazenamento de alto desempenho, como SSD.

Quando o volume temporário de alto desempenho estiver pronto, defina o parâmetro da JVM `-Djava.io.tmpdir`. Por exemplo, você pode adicionar o parâmetro da JVM abaixo à variável `CQ_JVM_OPTS` no script `bin/start` de [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configuração do Java {#java-configuration}

### Versão do Java {#java-version}

O Adobe recomenda implantar [!DNL Experience Manager Assets] no Java 8 para obter desempenho ideal.

<!-- TBD: Link to the latest official word around Java.
-->

### Parâmetros da JVM {#jvm-parameters}

Defina os seguintes parâmetros da JVM:

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=verdadeiro

## Armazenamento de dados e configuração de memória {#data-store-and-memory-configuration}

### Configuração do armazenamento de dados de arquivo {#file-data-store-configuration}

É recomendável separar o armazenamento de dados do armazenamento de segmentos para todos os usuários [!DNL Experience Manager Assets] . Além disso, configurar os parâmetros `maxCachedBinarySize` e `cacheSizeInMB` pode ajudar a maximizar o desempenho. Defina `maxCachedBinarySize` para o menor tamanho de arquivo que pode ser mantido no cache. Especifique o tamanho do cache na memória a ser usado para o armazenamento de dados em `cacheSizeInMB`. O Adobe recomenda que você defina esse valor entre 2 e 10% do tamanho total do heap. No entanto, o teste de carga/desempenho pode ajudar a determinar a configuração ideal.

### Configurar o tamanho máximo do cache de imagem em buffer {#configure-the-maximum-size-of-the-buffered-image-cache}

Ao fazer upload de grandes quantidades de ativos para [!DNL Adobe Experience Manager], para permitir picos inesperados no consumo de memória e para evitar que a JVM falhe com OutOfMemoryErrors, reduza o tamanho máximo configurado do cache de imagem em buffer. Considere um exemplo de que você tem um sistema com um heap máximo (- `Xmx`param) de 5 GB, um conjunto Oak BlobCache de 1 GB e um cache de documento definido em 2 GB. Nesse caso, o cache em buffer levaria no máximo 1,25 GB e a memória, o que deixaria apenas 0,75 GB de memória para picos inesperados.

Configure o tamanho do cache em buffer no console OSGi da Web. Em `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, defina a propriedade `cq.dam.image.cache.max.memory` em bytes. Por exemplo, 1073741824 é 1 GB (1024 x 1024 x 1024 = 1 GB).

No Experience Manager 6.1 SP1, se estiver usando um nó `sling:osgiConfig` para configurar essa propriedade, defina o tipo de dados como Long. Para obter mais detalhes, consulte [CQBufferedImageCache consome heap durante os uploads de Ativos](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### Armazenamento de dados compartilhados {#shared-data-stores}

A implementação de um S3 ou armazenamento de dados de arquivos compartilhados pode ajudar a economizar espaço em disco e aumentar o throughput da rede em implementações de grande escala. Para obter mais informações sobre os prós e contras do uso de um armazenamento de dados compartilhado, consulte [Guia de dimensionamento de ativos](/help/assets/assets-sizing-guide.md).

### Armazenamento de dados S3 {#s-data-store}

A seguinte configuração do Armazenamento de dados S3 ( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) ajudou o Adobe a extrair 12,8 TB de objetos grandes binários (BLOBs) de um armazenamento de dados de arquivo existente em um armazenamento de dados S3 em um site do cliente:

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

O Adobe recomenda habilitar o HTTPS porque muitas empresas têm firewalls que detectam tráfego HTTP, o que afeta negativamente os uploads e corrompe arquivos. Para uploads de arquivos grandes, verifique se os usuários conectaram-se à rede por fio, pois uma rede WiFi fica rapidamente saturada. Para obter diretrizes sobre como identificar gargalos de rede, consulte [Guia de dimensionamento de ativos](/help/assets/assets-sizing-guide.md). Para avaliar o desempenho da rede analisando a topologia de rede, consulte [Considerações de rede do Assets](/help/assets/assets-network-considerations.md).

Principalmente, sua estratégia de otimização de rede depende da quantidade de largura de banda disponível e da carga em sua instância [!DNL Experience Manager]. Opções comuns de configuração, incluindo firewalls ou proxies, podem ajudar a melhorar o desempenho da rede. Alguns pontos-chave a ter em conta:

* Dependendo do tipo de instância (pequena, moderada, grande), verifique se você tem largura de banda de rede suficiente para a instância do Experience Manager. Adequada alocação de largura de banda é especialmente importante se [!DNL Experience Manager] estiver hospedado no AWS.
* Se sua instância [!DNL Experience Manager] estiver hospedada no AWS, você poderá se beneficiar com uma política de dimensionamento versátil. Atualize a instância se os usuários esperarem carga alta. Faça o download para moderar/baixo carregamento.
* HTTPS: A maioria dos usuários tem firewalls que detectam tráfego HTTP, o que pode afetar negativamente o upload de arquivos ou até mesmo arquivos corrompidos durante a operação de upload.
* Uploads de arquivo grande: Certifique-se de que os usuários tenham conexões com fio à rede (as conexões WiFi se saturam rapidamente).

## Fluxos de trabalhos {#workflows}

### Fluxos de trabalho transitórios {#transient-workflows}

Sempre que possível, defina o fluxo de trabalho [!UICONTROL Ativo de atualização do DAM] como Transitório. A configuração reduz significativamente os custos indiretos necessários para processar workflows, pois, nesse caso, os workflows não precisam passar pelos processos normais de rastreamento e arquivamento.

1. Navegue até `/miscadmin` na implantação [!DNL Experience Manager] em `https://[aem_server]:[port]/miscadmin`.

1. Expanda **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]** > **[!UICONTROL dam]**.

1. Abra **[!UICONTROL Ativo de atualização do DAM]**. No painel de ferramentas flutuante, alterne para a guia **[!UICONTROL Page]** e clique em **[!UICONTROL Propriedades da página]**.

1. Selecione **[!UICONTROL Fluxo de trabalho transitório]** e clique em **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Alguns recursos não suportam fluxos de trabalho transitórios. Se sua implantação [!DNL Assets] exigir esses recursos, não configure fluxos de trabalho transitórios.

Nos casos em que workflows transitórios não podem ser usados, execute a limpeza de workflow regularmente para excluir workflows [!UICONTROL DAM Update Asset] arquivados para garantir que o desempenho do sistema não seja degradado.

Normalmente, executa os workflows de limpeza semanalmente. No entanto, em cenários que consomem muitos recursos, como durante a assimilação de ativos em larga escala, é possível executá-la com mais frequência.

Para configurar a limpeza do fluxo de trabalho, adicione uma nova configuração Adobe Granite Workflow Purge através do console OSGi. Em seguida, configure e agende o workflow como parte da janela de manutenção semanal.

Se a limpeza for muito longa, o tempo limite expirará. Portanto, você deve garantir que os trabalhos de limpeza sejam concluídos para evitar situações em que os workflows de limpeza não são concluídos devido ao alto número de workflows.

Por exemplo, após executar vários workflows não transitórios (que criam nós de instâncias de workflow), é possível executar [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) de forma ad-hoc. Ele remove instâncias de fluxo de trabalho redundantes e concluídas imediatamente, em vez de aguardar a execução do agendador de limpeza de fluxo de trabalho do Adobe Granite.

### Máximo de trabalhos paralelos {#maximum-parallel-jobs}

Por padrão, [!DNL Experience Manager] executa um número máximo de trabalhos paralelos igual ao número de processadores no servidor. O problema com essa configuração é que, durante períodos de carga pesada, todos os processadores são ocupados por [!UICONTROL DAM Update Asset] fluxos de trabalho, retardando a capacidade de resposta da interface do usuário e evitando que [!DNL Experience Manager] execute outros processos que salvaguardem o desempenho e a estabilidade do servidor. Como prática recomendada, defina esse valor para metade dos processadores disponíveis no servidor, executando as seguintes etapas:

1. Em [!DNL Experience Manager] Autor, acesse `https://[aem_server]:[port]/system/console/slingevent`.

1. Clique em **[!UICONTROL Editar]** em cada fila de workflow relevante para sua implementação, por exemplo **[!UICONTROL Fila de Fluxo de Trabalho Transitório do Granite]**.

1. Atualize o valor de **[!UICONTROL Máximo de Trabalhos Paralelos]** e clique em **[!UICONTROL Salvar]**.

Definir uma fila para metade dos processadores disponíveis é uma solução viável para começar. No entanto, talvez seja necessário aumentar ou diminuir esse número para atingir a taxa de transferência máxima e ajustá-lo por ambiente. Há filas separadas para fluxos de trabalho transitórios e não transitórios, bem como outros processos, como fluxos de trabalho externos. Se várias filas definidas como 50% dos processadores estiverem ativas simultaneamente, o sistema poderá ficar sobrecarregado rapidamente. As filas amplamente usadas variam muito entre as implementações do usuário. Portanto, talvez seja necessário configurá-los cuidadosamente para obter o máximo de eficiência sem sacrificar a estabilidade do servidor.

### Configuração do Ativo de atualização DAM {#dam-update-asset-configuration}

O fluxo de trabalho [!UICONTROL Ativo de atualização DAM] contém um conjunto completo de etapas configuradas para tarefas, como geração de PTIFF Dynamic Media e integração [!DNL Adobe InDesign Server]. No entanto, a maioria dos usuários pode não exigir várias dessas etapas. O Adobe recomenda que você crie uma cópia personalizada do modelo de fluxo de trabalho [!UICONTROL Ativo de atualização DAM] e remova quaisquer etapas desnecessárias. Nesse caso, atualize os inicializadores de [!UICONTROL Ativo de atualização do DAM] para apontar para o novo modelo.

A execução intensiva do fluxo de trabalho [!UICONTROL DAM Update Asset] pode aumentar bastante o tamanho do armazenamento de dados do arquivo. Os resultados de um experimento realizado pelo Adobe mostraram que o tamanho do armazenamento de dados pode aumentar em aproximadamente 400 GB se cerca de 5500 workflows forem executados em 8 horas.

É um aumento temporário e o armazenamento de dados é restaurado para seu tamanho original após executar a tarefa de coleta de lixo do armazenamento de dados.

Normalmente, a tarefa de coleta de lixo do armazenamento de dados é executada semanalmente, juntamente com outras tarefas de manutenção programadas.

Se você tiver um espaço em disco limitado e executar os workflows [!UICONTROL Ativo de atualização DAM] intensamente, considere agendar a tarefa de coleta de lixo com mais frequência.

#### Geração de renderização em tempo de execução {#runtime-rendition-generation}

Os clientes usam imagens de vários tamanhos e formatos em seu site ou para distribuição a parceiros comerciais. Como cada representação adiciona ao espaço do ativo no repositório, o Adobe recomenda usar esse recurso criteriosamente. Para reduzir a quantidade de recursos necessários para processar e armazenar imagens, você pode gerar essas imagens em tempo de execução em vez de como representações durante a assimilação.

Muitos clientes do Sites implementam um servlet de imagem que redimensiona e recorta imagens no momento em que são solicitadas, o que impõe carga adicional na instância de publicação. No entanto, enquanto essas imagens puderem ser armazenadas em cache, o desafio poderá ser atenuado.

Uma abordagem alternativa é usar a tecnologia Dynamic Media para manipular totalmente a imagem. Além disso, você pode implantar o Brand Portal que não apenas assume as responsabilidades de geração de representação da infraestrutura [!DNL Experience Manager], como também todo o nível de publicação.

#### ImageMagick {#imagemagick}

Se você personalizar o fluxo de trabalho [!UICONTROL Ativo de atualização do DAM] para gerar representações usando o ImageMagick, o Adobe recomenda modificar o arquivo `policy.xml` em `/etc/ImageMagick/`. Por padrão, o ImageMagick usa todo o espaço em disco disponível no volume do SO e na memória disponível. Faça as seguintes alterações de configuração na seção `policymap` de `policy.xml` para limitar esses recursos.

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
>Uma configuração incorreta pode tornar o servidor instável se o ImageMagick utilizar todo o espaço em disco disponível. As alterações de política necessárias para processar arquivos grandes usando o ImageMagick podem afetar o desempenho [!DNL Experience Manager]. Para obter mais informações, consulte [instalar e configurar o ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>Os arquivos ImageMagick `policy.xml` e `configure.xml` estão disponíveis em `/usr/lib64/ImageMagick-&#42;/config/` em vez de `/etc/ImageMagick/`.Consulte [ImageMagick documentation](https://www.imagemagick.org/script/resources.php) para obter o local dos arquivos de configuração.

Se você estiver usando [!DNL Experience Manager] no Adobe Managed Services (AMS), entre em contato com o Suporte ao cliente do Adobe caso planeje processar muitos arquivos grandes do PSD ou PSB. Trabalhe com o representante de Suporte ao cliente do Adobe para implementar essas práticas recomendadas para a implantação do AMS e escolher as melhores ferramentas e modelos possíveis para os formatos proprietários do Adobe. [!DNL Experience Manager] pode não processar arquivos PSB de alta resolução que tenham mais de 30000 x 23000 pixels.

### Writeback XMP {#xmp-writeback}

XMP write-back atualiza o ativo original sempre que os metadados são modificados em [!DNL Experience Manager], o que resulta no seguinte:

* O próprio ativo é modificado
* Uma versão do ativo é criada
* [!UICONTROL Ativos de atualização do DAM ] executados em relação ao ativo

Os resultados listados consomem recursos consideráveis. Portanto, o Adobe recomenda [desativar XMP Writeback](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html), se não for necessário.

Importar uma grande quantidade de metadados pode resultar em atividade de write-back de XMP que consome muitos recursos se o sinalizador de workflows de execução estiver marcado. Planeje essa importação durante o uso do servidor simplificado para que o desempenho para outros usuários não seja afetado.

## Replicação {#replication}

Ao replicar ativos para um grande número de instâncias de publicação, por exemplo, em uma implementação de Sites, o Adobe recomenda usar a replicação em cadeia. Nesse caso, a instância do autor é replicada para uma única instância de publicação que, por sua vez, é replicada para as outras instâncias de publicação, liberando a instância do autor.

### Configurar replicação em cadeia {#configure-chain-replication}

1. Escolha para qual instância de publicação você deseja usar para encadear as replicações
1. Nessa instância de publicação, adicione agentes de replicação que apontem para as outras instâncias de publicação
1. Em cada um desses agentes de replicação, ative &quot;Ao receber&quot; na guia &quot;Triggers&quot;

>[!NOTE]
>
>O Adobe não recomenda a ativação automática de ativos. No entanto, se necessário, o Adobe recomenda fazer isso como a etapa final em um fluxo de trabalho, geralmente o DAM Update Asset.

## Índices de pesquisa {#search-indexes}

Instale [os Service Packs mais recentes](/help/release-notes/sp-release-notes.md) e os hotfixes relacionados ao desempenho, pois esses hotfixes frequentemente incluem atualizações nos índices do sistema. Consulte [dicas de ajuste de desempenho](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) para obter algumas otimizações de índice.

Crie índices personalizados para consultas executadas com frequência. Para obter detalhes, consulte a metodologia [para analisar consultas lentas](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) e [criar índices personalizados](/help/sites-deploying/queries-and-indexing.md). Para obter insights adicionais sobre as práticas recomendadas de consulta e índice, consulte [Práticas recomendadas para consultas e indexação](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Configurações do índice Lucene {#lucene-index-configurations}

Algumas otimizações podem ser feitas nas configurações do índice Oak que podem ajudar a melhorar o desempenho [!DNL Experience Manager Assets]. Atualize as configurações de índice para melhorar o tempo de reindexação:

1. Abra o CRXDe `/crx/de/index.jsp` e faça logon como um usuário administrativo.
1. Navegue até `/oak:index/lucene`.
1. Adicione uma propriedade `String[]` `excludedPaths` com valores `/var`, `/etc/workflow/instances` e `/etc/replication`.
1. Navegue até `/oak:index/damAssetLucene`. Adicione uma propriedade `String[]` `includedPaths` com o valor `/content/dam`. Salve as alterações.

Se os usuários não precisarem fazer uma pesquisa de texto completo de ativos, por exemplo, pesquisar texto em documentos do PDF e depois desabilitá-lo. Você melhora o desempenho do índice ao desabilitar a indexação de texto completo. Para desativar a extração de texto [!DNL Apache Lucene], siga estas etapas:

1. Na interface [!DNL Experience Manager], acesse [!UICONTROL Gerenciador de Pacotes].
1. Faça upload e instale o pacote disponível em [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Adivinhe total {#guess-total}

Ao criar queries que geram grandes conjuntos de resultados, use o parâmetro `guessTotal` para evitar a utilização de memória pesada ao executá-los.

## Problemas conhecidos {#known-issues}

### Arquivos grandes {#large-files}

Há dois problemas conhecidos principais relacionados a arquivos grandes em [!DNL Experience Manager]. Quando os arquivos atingem tamanhos maiores que 2 GB, a sincronização de espera passiva pode ocorrer em uma situação de falta de memória. Em alguns casos, impede a execução da sincronização de standby. Em outros casos, isso causa falha na instância primária. Esse cenário se aplica a qualquer arquivo em [!DNL Experience Manager] que seja maior que 2 GB, incluindo pacotes de conteúdo.

Da mesma forma, quando os arquivos atingem 2 GB ao usar um armazenamento de dados S3 compartilhado, pode levar algum tempo para que o arquivo seja totalmente persistente do cache para o sistema de arquivos. Como resultado, ao usar a replicação sem binário, é possível que os dados binários não tenham sido persistentes antes da conclusão da replicação. Essa situação pode levar a problemas, especialmente se a disponibilidade dos dados for importante.

## Teste de desempenho {#performance-testing}

Para cada implantação [!DNL Experience Manager], estabeleça um regime de teste de desempenho que possa identificar e resolver gargalos rapidamente. Aqui estão algumas áreas-chave para se concentrar.

### Teste de rede {#network-testing}

Para todas as preocupações de desempenho de rede do cliente, execute as seguintes tarefas:

* Testar o desempenho da rede na rede do cliente
* Teste o desempenho da rede dentro da rede Adobe. Para clientes do AMS, trabalhe com seu CSE para testar dentro da rede do Adobe.
* Testar o desempenho da rede a partir de outro ponto de acesso
* Usando uma ferramenta de benchmark de rede
* Testar em relação ao dispatcher

### [!DNL Experience Manager] teste de implantação {#aem-deployment-testing}

Para minimizar a latência e alcançar alta throughput por meio de utilização eficiente da CPU e compartilhamento de carga, monitore o desempenho da sua implantação [!DNL Experience Manager] regularmente. Em especial:

* Execute testes de carga em relação à implantação [!DNL Experience Manager].
* Monitore o desempenho do upload e a capacidade de resposta da interface do usuário.

## [!DNL Experience Manager Assets] lista de verificação de desempenho e impacto das tarefas de gerenciamento de ativos {#checklist}

* Ative o HTTPS para contornar qualquer farejador de tráfego HTTP corporativo.
* Use uma conexão com fio para fazer upload de ativos pesados.
* Implante no Java 8.
* Defina os parâmetros ideais da JVM.
* Configure um DataStore do Sistema de Arquivos ou um armazenamento de dados S3.
* Desative a geração de subativos. Se estiver ativado, AEM fluxo de trabalho cria um ativo separado para cada página em um ativo de várias páginas. Cada uma dessas páginas é um ativo individual que consome espaço em disco adicional, requer controle de versão e processamento adicional de fluxo de trabalho. Se você não precisar de páginas separadas, desative as atividades de geração de subativos e extração de página.
* Habilite fluxos de trabalho transitórios.
* Ajuste as filas do fluxo de trabalho do Granite para limitar os trabalhos simultâneos.
* Configure [!DNL ImageMagick] para limitar o consumo de recursos.
* Remova etapas desnecessárias do fluxo de trabalho [!UICONTROL Atualizar ativo do DAM].
* Configure a limpeza de fluxo de trabalho e versão.
* Otimize índices com os Service Packs e hotfixes mais recentes. Consulte o Suporte ao cliente do Adobe para obter outras otimizações de índice que possam estar disponíveis.
* Use guessTotal para otimizar o desempenho da consulta.
* Se você configurar [!DNL Experience Manager] para detectar tipos de arquivos a partir do conteúdo dos arquivos (habilitando **[!UICONTROL Day CQ DAM Mime Type Service]** no **[!UICONTROL AEM Web Console]**), faça upload de muitos arquivos em massa durante horas que não sejam de pico, pois ele consome muitos recursos.
