---
title: Migrar ativos em massa
description: Descreve como trazer ativos para  [!DNL Adobe Experience Manager], aplicar metadados, gerar representações e ativá-los para publicar instâncias.
contentOwner: AG
role: Developer, Admin
feature: Migration,Renditions,Asset Management
exl-id: 184f1645-894a-43c1-85f5-8e0d2d77aa73
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 6%

---

# Como migrar ativos em massa {#assets-migration-guide}

Ao migrar ativos para o [!DNL Adobe Experience Manager], há várias etapas a serem consideradas. Extrair ativos e metadados de sua página inicial atual está fora do escopo deste documento, pois varia muito entre as implementações, mas este documento descreve como trazer esses ativos para [!DNL Experience Manager], aplicar seus metadados, gerar representações e ativá-los para publicar instâncias.

## Pré-requisitos {#prerequisites}

Antes de executar qualquer etapa desta metodologia, revise e implemente a orientação nas [dicas de ajuste de desempenho do Assets](performance-tuning-guidelines.md). Muitas das etapas, como a configuração do máximo de tarefas simultâneas, melhoram muito a estabilidade e o desempenho do servidor sob carga. Outras etapas, como configurar um Armazenamento de dados de arquivo, são muito mais difíceis de executar depois que o sistema é carregado com ativos.

>[!NOTE]
>
>As seguintes ferramentas de migração de ativos não fazem parte do [!DNL Experience Manager] e não têm suporte da Adobe:
>
>* Criador de tags de ferramentas do ACS AEM
>* Importador de ativos CSV de ferramentas do AEM do ACS
>* ACS Commons Bulk Workflow Manager
>* ACS Commons Fast Action Manager
>* Fluxo de trabalho sintético
>
>Este software é de código aberto e é coberto pela [Licença Apache v2](https://adobe-consulting-services.github.io/pages/license.html). Para fazer uma pergunta ou relatar um problema, visite os respectivos [Problemas do GitHub para as ferramentas do ACS AEM](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues) e os [ACS AEM Commons](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues).

## Migrar para [!DNL Experience Manager] {#migrating-to-aem}

A migração de ativos para [!DNL Experience Manager] requer várias etapas e deve ser vista como um processo em fases. As fases da migração são as seguintes:

1. Desative os workflows.
1. Carregar tags.
1. Assimilar ativos.
1. Processar representações.
1. Ativar ativos.
1. Habilite workflows.

![chlimage_1-223](assets/chlimage_1-223.png)

### Desabilitar workflows {#disabling-workflows}

Antes de iniciar a migração, desabilite os iniciadores para o fluxo de trabalho [!UICONTROL Ativo de atualização do DAM]. É melhor assimilar todos os ativos no sistema e executar os fluxos de trabalho em lotes. Se você já estiver vivo enquanto a migração está ocorrendo, poderá agendar essas atividades para serem executadas fora do horário de expediente.

### Carregar tags {#loading-tags}

Talvez você já tenha uma taxonomia de tags em vigor que está aplicando às suas imagens. Embora ferramentas como o Importador de ativos CSV e o suporte [!DNL Experience Manager] para perfis de metadados possam automatizar o processo de aplicação de tags a ativos, as tags precisam ser carregadas no sistema. O recurso [Criador de marcas de ferramentas do AEM do ACS](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) permite preencher marcas usando uma planilha do Microsoft Excel carregada no sistema.

### Assimilar ativos {#ingesting-assets}

O desempenho e a estabilidade são preocupações importantes ao assimilar ativos no sistema. Como você está carregando uma grande quantidade de dados no sistema, é necessário ter certeza de que o sistema funciona bem para minimizar o tempo necessário e evitar sobrecarga do sistema, o que pode causar uma falha, especialmente em sistemas que já estão em produção.

Há duas abordagens para carregar os ativos no sistema: uma abordagem baseada em push usando HTTP ou uma abordagem baseada em pull usando APIs JCR.

#### Enviar por HTTP {#pushing-through-http}

A equipe do Managed Services da Adobe usa uma ferramenta chamada Glutton para carregar dados em ambientes do cliente. Glutton é um pequeno aplicativo Java que carrega todos os ativos de um diretório para outro diretório em uma implantação do [!DNL Experience Manager]. Em vez de Glutton, você também pode usar ferramentas como scripts Perl para publicar os ativos no repositório.

Há duas desvantagens principais em usar a abordagem de envio por https:

1. Os ativos precisam ser transmitidos via HTTP para o servidor. Isso requer bastante sobrecarga e é demorado, aumentando assim o tempo necessário para executar a migração.
1. Se você tiver tags e metadados personalizados que devem ser aplicados aos ativos, essa abordagem exigirá um segundo processo personalizado que você precisará executar para aplicar esses metadados aos ativos depois que eles tiverem sido importados.

A outra abordagem para assimilar ativos é extrair ativos do sistema de arquivos local. No entanto, se você não conseguir que uma unidade externa ou um compartilhamento de rede seja montado no servidor para executar uma abordagem baseada em pull, postar os ativos por HTTP é a melhor opção.

#### Buscar no sistema de arquivos local {#pulling-from-the-local-filesystem}

O [Importador de ativos CSV de Ferramentas do AEM do ACS](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) extrai ativos do sistema de arquivos e metadados de ativos de um arquivo CSV para a importação de ativos. A API do Experience Manager Asset Manager é usada para importar os ativos para o sistema e aplicar as propriedades de metadados configuradas. Idealmente, os ativos são montados no servidor por meio de uma montagem de arquivo de rede ou por meio de uma unidade externa.

Como os ativos não precisam ser transmitidos por uma rede, o desempenho geral melhora consideravelmente, e esse método geralmente é considerado a maneira mais eficiente de carregar ativos no repositório. Além disso, como a ferramenta é compatível com a assimilação de metadados, você pode importar todos os ativos e metadados em uma única etapa, em vez de criar uma segunda etapa para aplicar os metadados por meio de uma ferramenta separada.

### Processar representações {#processing-renditions}

Após carregar os ativos no sistema, é necessário processá-los por meio do fluxo de trabalho [!UICONTROL Ativo de atualização do DAM] para extrair metadados e gerar representações. Antes de executar esta etapa, você precisa duplicar e modificar o fluxo de trabalho do [!UICONTROL Ativo de atualização do DAM] para atender às suas necessidades. O fluxo de trabalho pronto para uso contém muitas etapas que podem não ser necessárias para você, como a geração de PTIFF do Dynamic Media ou a integração de [!DNL InDesign Server].

Após configurar o workflow de acordo com suas necessidades, você tem duas opções para executá-lo:

1. A abordagem mais simples é o [Gerenciador de fluxos de trabalho em massa dos ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html). Essa ferramenta permite executar um query e processar os resultados do query por meio de um workflow. Também há opções para definir tamanhos de lote.
1. Use o [ACS Commons Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) em conjunto com [Fluxos de trabalho sintéticos](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html). Embora essa abordagem seja muito mais abrangente, ela permite remover a sobrecarga do mecanismo de fluxo de trabalho do [!DNL Experience Manager] e, ao mesmo tempo, otimizar o uso dos recursos do servidor. Além disso, o Fast Action Manager aumenta ainda mais o desempenho, monitorando dinamicamente os recursos do servidor e diminuindo a carga colocada no sistema. Os exemplos de scripts foram fornecidos na página de recursos ACS Commons.

### Ativar ativos {#activating-assets}

Para implantações com um nível de publicação, é necessário ativar os ativos no farm de publicação. Embora a Adobe recomende executar mais de uma única instância de publicação, é mais eficiente replicar todos os ativos em uma única instância de publicação e clonar essa instância. Ao ativar um grande número de ativos, depois de acionar uma ativação em árvore, talvez seja necessário intervir. Veja por que: ao desativar ativações, os itens são adicionados à fila de trabalhos/eventos do Sling. Quando o tamanho dessa fila começar a exceder aproximadamente 40.000 itens, o processamento ficará muito lento. Depois que o tamanho dessa fila exceder 100.000 itens, a estabilidade do sistema começará a sofrer.

Para contornar esse problema, você pode usar o [Gerenciador de Ações Rápidas](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) para gerenciar a replicação de ativos. Isso funciona sem usar as filas Sling, reduzindo a sobrecarga e, ao mesmo tempo, limitando a carga de trabalho para evitar que o servidor fique sobrecarregado. Um exemplo de uso do FAM para gerenciar a replicação é mostrado na página de documentação do recurso.

Outras opções para obter ativos para o farm de publicação incluem o uso de [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) ou [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run), que são fornecidos como ferramentas, como parte do Jackrabbit. Outra opção é usar uma ferramenta de código aberto para a infraestrutura do [!DNL Experience Manager] chamada [Grabbit](https://github.com/TWCable/grabbit), que alega ter desempenho mais rápido do que o vlt.

Para qualquer uma dessas abordagens, o problema é que os ativos na instância do autor não aparecem como tendo sido ativados. Para lidar com a sinalização desses ativos com o status de ativação correto, também é necessário executar um script para marcar os ativos como ativados.

>[!NOTE]
>
>A Adobe não mantém nem oferece suporte ao Grabbit.

### Clonar publicação {#cloning-publish}

Depois que os ativos forem ativados, você poderá clonar a instância de publicação para criar quantas cópias forem necessárias para a implantação. A clonagem de um servidor é bastante simples, mas há algumas etapas importantes a serem lembradas. Para clonar a publicação:

1. Faça backup da instância de origem e do armazenamento de dados.
1. Restaure o backup da instância e do armazenamento de dados no local de destino. As etapas a seguir se referem a essa nova instância.
1. Executar uma pesquisa de sistema de arquivos em `crx-quickstart/launchpad/felix` para `sling.id`. Exclua esse arquivo.
1. No caminho raiz do armazenamento de dados, localize e exclua todos os arquivos `repository-XXX`.
1. Edite `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` e `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` para apontar para o local do armazenamento de dados no novo ambiente.
1. Inicie o ambiente.
1. Atualize a configuração de todos os agentes de replicação no(s) autor(es) para apontar para as instâncias de publicação corretas ou agentes de limpeza do dispatcher na nova instância para apontar para os dispatchers corretos para o novo ambiente.

### Habilitar workflows {#enabling-workflows}

Após a conclusão da migração, os iniciadores dos fluxos de trabalho do [!UICONTROL Ativo de atualização do DAM] devem ser reabilitados para oferecer suporte à geração de representação e extração de metadados para o uso diário contínuo do sistema.

## Migrar entre [!DNL Experience Manager] implantações {#migrating-between-aem-instances}

Embora não seja tão comum, às vezes você precisa migrar grandes quantidades de dados de uma implantação do [!DNL Experience Manager] para outra; por exemplo, ao executar uma atualização do [!DNL Experience Manager], atualizar seu hardware ou migrar para um novo datacenter, como o AMS.

Nesse caso, os ativos já estão preenchidos com metadados e as representações já foram geradas. Você pode simplesmente se concentrar em mover ativos de uma instância para outra. Ao migrar entre a implantação do [!DNL Experience Manager], execute as seguintes etapas:

1. Desabilitar fluxos de trabalho: como você está migrando representações junto com nossos ativos, você deseja desabilitar os inicializadores de fluxo de trabalho para o fluxo de trabalho [!UICONTROL Ativo de atualização DAM].

1. Migrar marcas: como você já tem marcas carregadas na implantação de origem [!DNL Experience Manager], é possível criá-las em um pacote de conteúdo e instalar o pacote na instância de destino.

1. Migrar ativos: há duas ferramentas recomendadas para mover ativos de uma implantação do [!DNL Experience Manager] para outra:

   * O **Vault Remote Copy** ou vlt rcp permite usar o vlt em uma rede. Você pode especificar um diretório de origem e destino e o vlt faz o download de todos os dados do repositório de uma instância e os carrega na outra. Vlt rcp está documentado em [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **Grabbit** é uma ferramenta de sincronização de conteúdo de código aberto desenvolvida pela Time Warner Cable para sua implementação [!DNL Experience Manager]. Como ele usa fluxos de dados contínuos, em comparação ao vlt rcp, ele tem uma latência menor e alega uma melhoria de velocidade de duas a dez vezes mais rápida que o vlt rcp. O Grabbit também oferece suporte à sincronização somente de conteúdo delta, o que permite sincronizar as alterações após a conclusão de uma passagem de migração inicial.

1. Ativar ativos: Siga as instruções para [ativar ativos](#activating-assets) documentadas para a migração inicial para [!DNL Experience Manager].

1. Clonar publicação: assim como em uma nova migração, carregar uma única instância de publicação e cloná-la é mais eficiente do que ativar o conteúdo em ambos os nós. Consulte [Publicação de clonagem.](#cloning-publish)

1. Habilitar fluxos de trabalho: após concluir a migração, habilite novamente os iniciadores do fluxo de trabalho [!UICONTROL Ativo de atualização do DAM] para oferecer suporte à geração de representação e extração de metadados para o uso diário contínuo do sistema.
