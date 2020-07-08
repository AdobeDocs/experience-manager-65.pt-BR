---
title: Migre ativos [!DNL Adobe Experience Manager Assets] em massa.
description: Descreve como inserir ativos [!DNL Adobe Experience Manager], aplicar metadados, gerar representações e ativá-los para publicar instâncias.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 678e91699523c22a7048bd7b344fa539b849ae8b
workflow-type: tm+mt
source-wordcount: '1800'
ht-degree: 8%

---


# Como migrar ativos em massa {#assets-migration-guide}

Ao migrar ativos para [!DNL Adobe Experience Manager], há várias etapas a serem consideradas. A extração de ativos e metadados para fora de sua casa atual está fora do escopo deste documento, pois varia muito entre implementações, mas este documento descreve como trazer esses ativos para dentro, aplicar seus metadados, gerar representações e ativá-los para publicar instâncias. [!DNL Experience Manager]

## Pré-requisitos {#prerequisites}

Antes de executar qualquer uma das etapas desta metodologia, reveja e implemente as orientações nas dicas [de ajuste de desempenho do](performance-tuning-guidelines.md)Assets. Muitas das etapas, como a configuração de trabalhos simultâneos máximos, melhoram consideravelmente a estabilidade e o desempenho do servidor com carga. Outras etapas, como a configuração de um File Data Store, são muito mais difíceis de executar depois que o sistema é carregado com ativos.

>[!NOTE]
>
>As seguintes ferramentas de migração de ativos não fazem parte da Adobe e não são suportadas por ela [!DNL Experience Manager] :
>
>* Criador de tags de ferramentas AEM ACS
>* Importador de ativos CSV das ferramentas AEM ACS
>* Gerenciador de fluxo de trabalho em massa do ACS
>* Gerenciador de ações rápidas do ACS Commons
>* Fluxo de trabalho sintético

>
>
Este software é de código aberto e é coberto pela [Licença Apache v2](https://adobe-consulting-services.github.io/pages/license.html). Para fazer uma pergunta ou relatar um problema, visite os respectivos [Problemas do GitHub para as ferramentas do ACS AEM](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues) e os [ACS AEM Commons](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues).

## Migrar para [!DNL Experience Manager] {#migrating-to-aem}

A migração de ativos para [!DNL Experience Manager] requer várias etapas e deve ser exibida como um processo em fases. As fases da migração são as seguintes:

1. Desative workflows.
1. Carregar tags.
1. Ativos de assimilação.
1. Processar execuções.
1. Ativar ativos.
1. Ative workflows.

![chlimage_1-223](assets/chlimage_1-223.png)

### Desativar workflows {#disabling-workflows}

Antes de iniciar a migração, desative seus iniciadores para o fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM. É melhor assimilar todos os ativos no sistema e, em seguida, executar os workflows em lotes. Se você já estiver ao vivo enquanto a migração estiver ocorrendo, poderá agendar essas atividades para serem executadas fora do horário de expediente.

### Carregar tags {#loading-tags}

Talvez você já tenha uma taxonomia de tag aplicada às suas imagens. Embora ferramentas como o Importador de ativos CSV e [!DNL Experience Manager] suporte para perfis de metadados possam automatizar o processo de aplicação de tags a ativos, as tags precisam ser carregadas no sistema. O recurso [ACS AEM Tools Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) permite preencher tags usando uma planilha do Microsoft Excel carregada no sistema.

### Ativos de assimilação {#ingesting-assets}

Desempenho e estabilidade são preocupações importantes ao assimilar ativos ao sistema. Como você está carregando uma grande quantidade de dados no sistema, é necessário certificar-se de que o sistema funciona da melhor forma possível para minimizar a quantidade de tempo necessário e evitar sobrecarregar o sistema, o que pode levar a uma falha do sistema, especialmente em sistemas que já estão em produção.

Há duas abordagens para carregar os ativos no sistema: uma abordagem baseada em push usando HTTP ou uma abordagem baseada em pull usando as APIs JCR.

#### Enviar por HTTP {#pushing-through-http}

A equipe de Serviços gerenciados da Adobe usa uma ferramenta chamada Glutton para carregar dados em ambientes do cliente. O Glutton é um pequeno aplicativo Java que carrega todos os ativos de um diretório para outro em uma [!DNL Experience Manager] implantação. Em vez do Glutton, você também pode usar ferramentas como scripts Perl para publicar os ativos no repositório.

Há duas desvantagens principais ao usar a abordagem de passar por https:

1. Os ativos precisam ser transmitidos via HTTP para o servidor. Isso requer bastante sobrecarga e é demorado, aumentando assim o tempo necessário para executar sua migração.
1. Se você tiver tags e metadados personalizados que devem ser aplicados aos ativos, essa abordagem exigirá um segundo processo personalizado que será necessário executar para aplicar esses metadados aos ativos depois que eles forem importados.

A outra abordagem para assimilar ativos é extrair ativos do sistema de arquivos local. No entanto, se você não conseguir que uma unidade externa ou compartilhamento de rede seja montado no servidor para executar uma abordagem baseada em pull, a publicação dos ativos por HTTP é a melhor opção.

#### Buscar no sistema de arquivos local {#pulling-from-the-local-filesystem}

O Importador [de ativos CSV das ferramentas AEM](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) ACS extrai ativos do sistema de arquivos e metadados de ativos de um arquivo CSV para a importação de ativos. A API do Gerenciador de ativos do Experience Manager é usada para importar os ativos para o sistema e aplicar as propriedades de metadados configuradas. Idealmente, os ativos são montados no servidor por meio de uma montagem de arquivos de rede ou por meio de uma unidade externa.

Como os ativos não precisam ser transmitidos através de uma rede, o desempenho geral melhora drasticamente e esse método é geralmente considerado a maneira mais eficiente de carregar ativos no repositório. Além disso, como a ferramenta oferece suporte à ingestão de metadados, você pode importar todos os ativos e metadados em uma única etapa, em vez de criar uma segunda etapa para aplicar os metadados por meio de uma ferramenta separada.

### Processar execuções {#processing-renditions}

Depois de carregar os ativos no sistema, é necessário processá-los por meio do fluxo de trabalho Atualizar ativo [!UICONTROL do] DAM para extrair metadados e gerar execuções. Antes de executar esta etapa, é necessário duplicado e modificar o fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM para atender às suas necessidades. O fluxo de trabalho predefinido contém várias etapas que podem não ser necessárias para você, como geração ou integração do Scene7 PTIFF [!DNL InDesign Server] .

Depois de configurar o fluxo de trabalho de acordo com suas necessidades, você tem duas opções para executá-lo:

1. A abordagem mais simples é o Gerenciador [de Fluxo de Trabalho em Massa da](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html)ACS Commons. Essa ferramenta permite que você execute um query e processe os resultados do query por meio de um fluxo de trabalho. Há opções para definir tamanhos de lote também.
1. Use o [ACS Commons Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) em conjunto com [Fluxos de trabalho sintéticos](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html). While this approach is much more involved, it lets you remove the overhead of the [!DNL Experience Manager] workflow engine while optimizing the use of server resources. Além disso, o Fast Action Manager aumenta ainda mais o desempenho, monitorando dinamicamente os recursos do servidor e diminuindo a carga colocada no sistema. Os exemplos de scripts foram fornecidos na página de recursos ACS Commons.

### Ativar ativos {#activating-assets}

Para implantações com uma camada de publicação, é necessário ativar os ativos fora do farm de publicação. Embora a Adobe recomende a execução de mais de uma única instância de publicação, é mais eficiente replicar todos os ativos para uma única instância de publicação e clonar essa instância. Ao ativar grandes números de ativos, depois de disparar uma ativação em árvore, talvez seja necessário intervir. Eis o porquê: Ao desligar o ativação, os itens são adicionados às tarefas/fila de evento do Sling. Depois que o tamanho desta fila começar a exceder aproximadamente 40.000 itens, o processamento diminuirá drasticamente. Depois que o tamanho desta fila exceder 100.000 itens, a estabilidade do sistema será afetada.

Para contornar esse problema, você pode usar o [Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) para gerenciar a replicação de ativos. Isso funciona sem usar as filas Sling, diminuindo a sobrecarga e, ao mesmo tempo, limitando a carga de trabalho para impedir que o servidor fique sobrecarregado. Um exemplo de uso do FAM para gerenciar a replicação é mostrado na página de documentação do recurso.

Outras opções para obter ativos para o farm de publicação incluem o uso de [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) ou [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run), que são fornecidos como ferramentas, como parte do Jackrabbit. Another option is to use an open-sourced tool for your [!DNL Experience Manager] infrastructure called [Grabbit](https://github.com/TWCable/grabbit), which claims to have faster performance than vlt.

Para qualquer uma dessas abordagens, a advertência é que os ativos na instância do autor não mostram que foram ativados. Para manipular o sinalizador desses ativos com o status de ativação correto, também é necessário executar um script para marcar os ativos como ativados.

>[!NOTE]
>
>A Adobe não mantém nem suporta Grabbit.

### Clonar publicação {#cloning-publish}

Depois que os ativos tiverem sido ativados, você poderá clonar sua instância de publicação para criar quantas cópias forem necessárias para a implantação. A clonagem de um servidor é bastante simples, mas há alguns passos importantes a serem lembrados. Para clonar a publicação:

1. Faça backup da instância de origem e do armazenamento de dados.
1. Restaure o backup da instância e do armazenamento de dados para o local do público alvo. As etapas a seguir referem-se a essa nova instância.
1. Perform a filesystem search under `crx-quickstart/launchpad/felix` for `sling.id`. Exclua esse arquivo.
1. No caminho raiz do armazenamento de dados, localize e exclua quaisquer `repository-XXX` arquivos.
1. Edite `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` e aponte `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` para o local do armazenamento de dados no novo ambiente.
1. Start do ambiente.
1. Atualize a configuração de qualquer agente de replicação no(s) autor(es) para apontar para as instâncias de publicação corretas ou os agentes de descarga do dispatcher na nova instância para apontar para os despachantes corretos para o novo ambiente.

### Ativar workflows {#enabling-workflows}

Após a conclusão da migração, os iniciadores dos workflows de ativos [!UICONTROL de atualização do] DAM devem ser reativados para suportar a geração de execução e a extração de metadados para uso diário contínuo do sistema.

## Migrar entre [!DNL Experience Manager] implantações {#migrating-between-aem-instances}

Embora não seja tão comum, às vezes é necessário migrar grandes quantidades de dados de uma [!DNL Experience Manager] implantação para outra; por exemplo, ao executar uma [!DNL Experience Manager] atualização, atualize seu hardware ou migre para um novo datacenter, como com uma migração do AMS.

Nesse caso, seus ativos já estão preenchidos com metadados e as execuções já são geradas. Você pode simplesmente se concentrar em mover ativos de uma instância para outra. Ao migrar entre [!DNL Experience Manager] a implantação, execute as seguintes etapas:

1. Desativar workflows: Como você está migrando renderizações juntamente com nossos ativos, deseja desativar os iniciadores de fluxo de trabalho para o fluxo de trabalho de Atualização de ativos [!UICONTROL do] DAM.

1. Migrar tags: Como as tags já foram carregadas na [!DNL Experience Manager] implantação de origem, é possível criá-las em um pacote de conteúdo e instalá-las na instância do público alvo.

1. Migrar ativos: Há duas ferramentas recomendadas para mover ativos de uma [!DNL Experience Manager] implantação para outra:

   * **Cofre Remote Copy** ou vlt rcp, permite que você use vlt em uma rede. Você pode especificar um diretório de origem e destino e vlt baixa todos os dados do repositório de uma instância e os carrega na outra. O Vlt rcp está documentado em [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **O Grabbit** é uma ferramenta de sincronização de conteúdo de código aberto desenvolvida pela Time Warner Cable para sua [!DNL Experience Manager] implementação. Como ele usa fluxos contínuos de dados, em comparação ao vlt rcp, ele tem uma latência mais baixa e exige uma melhoria de velocidade de duas a dez vezes mais rápida que o vlt rcp. O Grabbit também oferece suporte apenas à sincronização do conteúdo delta, o que permite sincronizar as alterações após a conclusão de uma passagem de migração inicial.

1. Ativar ativos: Siga as instruções para [ativar ativos](#activating-assets) documentados para a migração inicial para [!DNL Experience Manager].

1. Publicação de clone: Como ocorre com uma nova migração, carregar uma única instância de publicação e clonar é mais eficiente do que ativar o conteúdo em ambos os nós. Consulte [Clonando publicação.](#cloning-publish)

1. Ativar workflows: Depois de concluir a migração, ative novamente os iniciadores para o fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM para suportar a geração de execução e a extração de metadados para uso diário contínuo do sistema.
