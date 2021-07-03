---
title: Migrar ativos em massa
description: Descreve como trazer ativos para [!DNL Adobe Experience Manager], aplicar metadados, gerar representações e ativá-los para publicar instâncias.
contentOwner: AG
role: Architect, Admin
feature: Migração,Representações,Gerenciamento de Ativos
exl-id: 184f1645-894a-43c1-85f5-8e0d2d77aa73
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 8%

---

# Como migrar ativos em massa {#assets-migration-guide}

Ao migrar ativos para [!DNL Adobe Experience Manager], há várias etapas a serem consideradas. A extração de ativos e metadados de sua página inicial atual está fora do escopo desse documento, pois varia muito entre implementações, mas este documento descreve como trazer esses ativos para [!DNL Experience Manager], aplicar seus metadados, gerar representações e ativá-los para publicar instâncias.

## Pré-requisitos {#prerequisites}

Antes de realmente executar qualquer uma das etapas nesta metodologia, analise e implemente as orientações em [Dicas de ajuste de desempenho do Assets](performance-tuning-guidelines.md). Muitas etapas, como a configuração de trabalhos simultâneos máximos, melhoram muito a estabilidade e o desempenho do servidor sob carga. Outras etapas, como configurar um File Data Store, são muito mais difíceis de executar depois que o sistema é carregado com ativos.

>[!NOTE]
>
>As seguintes ferramentas de migração de ativos não fazem parte de [!DNL Experience Manager] e não são suportadas pelo Adobe:
>
>* Criador de tags de ferramentas AEM ACS
>* Importador de ativos CSV das ferramentas de AEM ACS
>* Gerente de Fluxo de Trabalho em Massa do ACS Commons
>* ACS Commons Fast Action Manager
>* Fluxo de trabalho sintético

>
>
Este software é de código aberto e é coberto pela [Licença Apache v2](https://adobe-consulting-services.github.io/pages/license.html). Para fazer uma pergunta ou relatar um problema, visite os respectivos [Problemas do GitHub para as ferramentas do ACS AEM](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues) e os [ACS AEM Commons](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues).

## Migrar para [!DNL Experience Manager] {#migrating-to-aem}

A migração de ativos para [!DNL Experience Manager] requer várias etapas e deve ser exibida como um processo em fases. As fases da migração são as seguintes:

1. Desative workflows.
1. Carregue tags.
1. Assimilar ativos.
1. Processar representações.
1. Ativar ativos.
1. Habilite workflows.

![chlimage_1-223](assets/chlimage_1-223.png)

### Desativar workflows {#disabling-workflows}

Antes de iniciar a migração, desative os lançadores para o fluxo de trabalho [!UICONTROL Ativo de atualização do DAM]. É melhor assimilar todos os ativos no sistema e, em seguida, executar os workflows em lotes. Se você já estiver ao vivo enquanto a migração estiver ocorrendo, poderá agendar essas atividades para serem executadas fora do horário.

### Carregar tags {#loading-tags}

É possível que você já tenha uma taxonomia de tags em vigor que esteja aplicando às imagens. Embora ferramentas como o Importador de ativos CSV e o suporte [!DNL Experience Manager] para perfis de metadados possam automatizar o processo de aplicação de tags a ativos, as tags precisam ser carregadas no sistema. O recurso [Criador de tags de ferramentas AEM ACS](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) permite preencher tags usando uma planilha do Microsoft Excel carregada no sistema.

### Assimilar ativos {#ingesting-assets}

O desempenho e a estabilidade são questões importantes ao assimilar ativos no sistema. Como você está carregando uma grande quantidade de dados no sistema, certifique-se de que o sistema esteja funcionando da melhor forma possível para minimizar a quantidade de tempo necessária e evitar sobrecarga do sistema, o que pode causar uma falha do sistema, especialmente em sistemas que já estão em produção.

Há duas abordagens para carregar os ativos no sistema: uma abordagem por push usando HTTP ou uma abordagem por pull usando as APIs do JCR.

#### Enviar por HTTP {#pushing-through-http}

A equipe do Managed Services do Adobe usa uma ferramenta chamada Glutton para carregar dados em ambientes do cliente. O Glutton é um pequeno aplicativo Java que carrega todos os ativos de um diretório em outro diretório em uma implantação [!DNL Experience Manager]. Em vez do Glutton, você também pode usar ferramentas como scripts Perl para publicar os ativos no repositório.

Há duas desvantagens principais ao usar a abordagem de passar por https:

1. Os ativos precisam ser transmitidos via HTTP para o servidor. Isso requer bastante sobrecarga e é demorado, prolongando assim o tempo necessário para executar sua migração.
1. Se você tiver tags e metadados personalizados que devem ser aplicados aos ativos, essa abordagem exigirá um segundo processo personalizado que será necessário executar para aplicar esses metadados aos ativos depois que eles forem importados.

A outra abordagem para assimilar ativos é obter ativos do sistema de arquivos local. No entanto, se não for possível obter uma unidade externa ou compartilhamento de rede montado no servidor para executar uma abordagem baseada em pull, publicar os ativos por HTTP é a melhor opção.

#### Buscar no sistema de arquivos local {#pulling-from-the-local-filesystem}

O [Importador de ativos CSV das Ferramentas de AEM ACS](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) extrai ativos do sistema de arquivos e metadados de ativos de um arquivo CSV para a importação de ativos. A API do Experience Manager Asset Manager é usada para importar os ativos para o sistema e aplicar as propriedades de metadados configuradas. Idealmente, os ativos são montados no servidor por meio de uma montagem de arquivo de rede ou por uma unidade externa.

Como os ativos não precisam ser transmitidos por uma rede, o desempenho geral melhora drasticamente e esse método geralmente é considerado a maneira mais eficiente de carregar ativos no repositório. Além disso, como a ferramenta oferece suporte à assimilação de metadados, é possível importar todos os ativos e metadados em uma única etapa, em vez de criar uma segunda etapa para aplicar os metadados por meio de uma ferramenta separada.

### Processar representações {#processing-renditions}

Depois de carregar os ativos no sistema, você precisa processá-los por meio do workflow [!UICONTROL Ativo de atualização do DAM] para extrair metadados e gerar representações. Antes de executar esta etapa, você precisa duplicar e modificar o fluxo de trabalho [!UICONTROL Ativo de atualização do DAM] para atender às suas necessidades. O fluxo de trabalho pronto para uso contém várias etapas que podem não ser necessárias para você, como a geração de PTIFF do Dynamic Media ou a integração [!DNL InDesign Server].

Depois de configurar o workflow de acordo com suas necessidades, você tem duas opções para executá-lo:

1. A abordagem mais simples é [Gerenciador de Fluxo de Trabalho em Massa do ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html). Essa ferramenta permite executar um query e processar os resultados do query por meio de um workflow. Também há opções para definir tamanhos de lote.
1. Use o [ACS Commons Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) em conjunto com [Fluxos de trabalho sintéticos](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html). Embora essa abordagem seja muito mais abrangente, ela permite remover a sobrecarga do mecanismo de workflow [!DNL Experience Manager] e, ao mesmo tempo, otimizar o uso dos recursos do servidor. Além disso, o Fast Action Manager aumenta ainda mais o desempenho, monitorando dinamicamente os recursos do servidor e diminuindo a carga colocada no sistema. Os exemplos de scripts foram fornecidos na página de recursos ACS Commons.

### Ativar ativos {#activating-assets}

Para implantações com um nível de publicação, é necessário ativar os ativos no farm de publicação. Embora o Adobe recomende executar mais de uma única instância de publicação, é mais eficiente replicar todos os ativos para uma única instância de publicação e clonar essa instância. Ao ativar grandes números de ativos, após acionar uma ativação de árvore, talvez seja necessário intervir. Veja o porquê: Ao disparar ativações, os itens são adicionados à fila de trabalhos/eventos do Sling. Depois que o tamanho dessa fila começar a exceder aproximadamente 40.000 itens, o processamento ficará lento drasticamente. Depois que o tamanho dessa fila exceder 100.000 itens, a estabilidade do sistema começará a sofrer.

Para contornar esse problema, você pode usar o [Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) para gerenciar a replicação de ativos. Isso funciona sem usar as filas do Sling, diminuindo a sobrecarga, enquanto limita a carga de trabalho para impedir que o servidor fique sobrecarregado. Um exemplo de uso do FAM para gerenciar a replicação é mostrado na página de documentação do recurso.

Outras opções para obter ativos para o farm de publicação incluem o uso de [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) ou [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run), que são fornecidos como ferramentas, como parte do Jackrabbit. Outra opção é usar uma ferramenta de software livre para sua infraestrutura [!DNL Experience Manager] chamada [Grabbit](https://github.com/TWCable/grabbit), que alega ter desempenho mais rápido do que o vlt.

Para qualquer uma dessas abordagens, o aviso é que os ativos na instância do autor não aparecem como ativados. Para lidar com a sinalização desses ativos com o status de ativação correto, também é necessário executar um script para marcar os ativos como ativados.

>[!NOTE]
>
>O Adobe não mantém nem suporta Grabbit.

### Clonar publicação {#cloning-publish}

Depois que os ativos tiverem sido ativados, você poderá clonar sua instância de publicação para criar quantas cópias forem necessárias para a implantação. A clonagem de um servidor é bastante simples, mas há alguns passos importantes a serem lembrados. Para clonar a publicação:

1. Faça backup da instância de origem e do armazenamento de dados.
1. Restaure o backup da instância e do armazenamento de dados para o local de destino. As etapas a seguir se referem a essa nova instância.
1. Execute uma pesquisa do sistema de arquivos em `crx-quickstart/launchpad/felix` para `sling.id`. Exclua esse arquivo.
1. No caminho raiz do armazenamento de dados, localize e exclua quaisquer arquivos `repository-XXX`.
1. Edite `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` e `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` para apontar para o local do armazenamento de dados no novo ambiente.
1. Inicie o ambiente.
1. Atualize a configuração de qualquer agente de replicação no(s) autor(es) para apontar para as instâncias de publicação corretas ou os agentes de liberação do dispatcher na nova instância para apontar para os dispatchers corretos para o novo ambiente.

### Ativar workflows {#enabling-workflows}

Depois de concluir a migração, os iniciadores dos fluxos de trabalho [!UICONTROL Ativo de atualização do DAM] devem ser reativados para suportar a geração de representação e a extração de metadados para o uso diário do sistema.

## Migrar entre [!DNL Experience Manager] implantações {#migrating-between-aem-instances}

Embora não seja quase tão comum, às vezes é necessário migrar grandes quantidades de dados de uma implantação [!DNL Experience Manager] para outra; por exemplo, ao executar uma atualização de [!DNL Experience Manager], atualize o hardware ou migre para um novo data center, como uma migração do AMS.

Nesse caso, seus ativos já estão preenchidos com metadados e as representações já são geradas. Você pode simplesmente se concentrar em mover ativos de uma instância para outra. Ao migrar entre a implantação [!DNL Experience Manager], você executa as seguintes etapas:

1. Desativar fluxos de trabalho: Como você está migrando representações junto com nossos ativos, deseja desativar os inicializadores do fluxo de trabalho para o fluxo de trabalho [!UICONTROL Ativo de atualização do DAM] .

1. Migrar tags: Como você já tem tags carregadas na implantação de origem [!DNL Experience Manager], é possível criá-las em um pacote de conteúdo e instalar o pacote na instância de destino.

1. Migrar ativos: Há duas ferramentas recomendadas para mover ativos de uma implantação [!DNL Experience Manager] para outra:

   * **Cofre Remote** Copyor vlt rcp, permite utilizar vlt através de uma rede. Você pode especificar um diretório de origem e de destino e o vlt baixa todos os dados do repositório de uma instância e os carrega na outra. O rcp vlt está documentado em [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **** Captura uma ferramenta de sincronização de conteúdo de código aberto, desenvolvida pelo Time Warner Cable para sua  [!DNL Experience Manager] implementação. Como usa fluxos de dados contínuos, em comparação ao vlt rcp, ele tem uma latência mais baixa e alega uma melhoria de velocidade de duas a dez vezes mais rápida que o vlt rcp. O Grabbit também suporta a sincronização somente do conteúdo delta, o que permite sincronizar as alterações depois que uma passagem de migração inicial for concluída.

1. Ativar ativos: Siga as instruções para [ativar ativos](#activating-assets) documentados para a migração inicial para [!DNL Experience Manager].

1. Publicação de clone: Assim como com uma nova migração, carregar uma única instância de publicação e clonar é mais eficiente do que ativar o conteúdo em ambos os nós. Consulte [Clonando publicação.](#cloning-publish)

1. Ativar fluxos de trabalho: Após concluir a migração, reative os iniciadores do fluxo de trabalho [!UICONTROL Ativo de atualização do DAM] para oferecer suporte à geração de representação e extração de metadados para uso diário do sistema.
