---
title: Elementos de armazenamento no AEM 6.5
seo-title: Storage Elements in AEM 6.5
description: Saiba mais sobre as implementações de armazenamento de nó disponíveis no AEM 6.5 e como manter o repositório.
seo-description: Learn about the node storage implementations available in AEM 6.5 and how to maintain the repository.
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 52437eb5-f9fb-4945-9950-5a1562fe878d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 1%

---

# Elementos de armazenamento no AEM 6.5{#storage-elements-in-aem}

Neste artigo, cobriremos:

* [Visão geral do armazenamento no AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Manutenção do repositório](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## Visão geral do armazenamento no AEM 6 {#overview-of-storage-in-aem}

Uma das mudanças mais importantes no AEM 6 são as inovações no nível do repositório.

Atualmente, há duas implementações de armazenamento de nó disponíveis no AEM6: Armazenamento Tar e armazenamento MongoDB.

### Armazenamento Tar {#tar-storage}

#### Execução de uma instância de AEM recém-instalada com o Armazenamento de Tar {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>O PID para o armazenamento do nó do segmento foi alterado de org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService em versões anteriores do AEM 6 para org.apache.jackrabbit.oak.segment.SegmentNodeStoreService no AEM 6.3. Certifique-se de fazer os ajustes de configuração necessários para refletir essa alteração.

Por padrão, o AEM 6 usa o armazenamento Tar para armazenar nós e binários, usando as opções de configuração padrão. Para configurar manualmente suas configurações de armazenamento, siga o procedimento abaixo:

1. Baixe o jar do início rápido do AEM 6 e coloque-o em uma nova pasta.
1. Descompacte AEM executando:

   `java -jar cq-quickstart-6.jar -unpack`

1. Crie uma pasta chamada `crx-quickstart\install` no diretório de instalação.

1. Crie um arquivo chamado `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` na pasta recém-criada.

1. Edite o arquivo e defina as opções de configuração. As seguintes opções estão disponíveis para o Armazenamento de nó do segmento, que é a base AEM implementação do armazenamento Tar:

   * `repository.home`: Caminho para a página inicial do repositório no qual vários dados relacionados ao repositório são armazenados. Por padrão, os arquivos de segmento seriam armazenados no diretório crx-quickstart/segmentstore.
   * `tarmk.size`: Tamanho máximo de um segmento em MB. O padrão é 256 MB.

1. Inicie o AEM.

### Armazenamento Mongo {#mongo-storage}

#### Execução de uma instância de AEM recém-instalada com o Mongo Storage {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM 6 pode ser configurado para ser executado com o armazenamento MongoDB seguindo o procedimento abaixo:

1. Baixe o jar do início rápido do AEM 6 e coloque-o em uma nova pasta.
1. Descompacte AEM executando o seguinte comando:

   `java -jar cq-quickstart-6.jar -unpack`

1. Certifique-se de que o MongoDB esteja instalado e uma instância de `mongod` está em execução. Para obter mais informações, consulte [Instalação do MongoDB](https://docs.mongodb.org/manual/installation/).
1. Crie uma pasta chamada `crx-quickstart\install` no diretório de instalação.
1. Configure o armazenamento de nós criando um arquivo de configuração com o nome da configuração que você deseja usar no `crx-quickstart\install` diretório.

   O Document Node Store (que é a base para AEM implementação de armazenamento do MongoDB) usa um arquivo chamado `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. Edite o arquivo e defina as opções de configuração. As opções disponíveis são as seguintes:

   * `mongouri`: O [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) necessário para se conectar ao Banco de Dados Mongo. O padrão é `mongodb://localhost:27017`
   * `db`: Nome do banco de dados Mongo. Por padrão, novas instalações do AEM 6 usam **aem-author** como o nome do banco de dados.
   * `cache`: O tamanho do cache em MB. Isso é distribuído entre vários caches usados no DocumentNodeStore. O padrão é 256.
   * `changesSize`: Tamanho em MB de coleção limitada usada no Mongo para armazenar a saída do diff em cache. O padrão é 256.
   * `customBlobStore`: Valor booleano que indica que um armazenamento de dados personalizado será usado. O padrão é false.

1. Crie um arquivo de configuração com o PID do armazenamento de dados que deseja usar e edite o arquivo para definir as opções de configuração. Para obter mais informações, consulte [Configuração de armazenamentos de nó e armazenamentos de dados](/help/sites-deploying/data-store-config.md).

1. Inicie o jar do AEM 6 com um back-end de armazenamento do MongoDB executando:

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   Onde **`-r`** é o modo de execução de back-end. Neste exemplo, ele começará com o suporte ao MongoDB.

#### Desativar Páginas Enormes e Transparentes {#disabling-transparent-huge-pages}

O Red Hat Linux usa um algoritmo de gerenciamento de memória chamado Transparent Huge Pages (THP). Enquanto o AEM executa leituras e gravações refinadas, o THP é otimizado para operações grandes. Por causa disso, é recomendável desativar o THP no armazenamento Tar e Mongo. Para desativar o algoritmo, siga estas etapas:

1. Abra o `/etc/grub.conf` no editor de texto de sua escolha.
1. Adicione a seguinte linha à **grub.conf** arquivo:

   ```
   transparent_hugepage=never
   ```

1. Finalmente, verifique se a configuração entrou em vigor executando:

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Se THP estiver desativado, a saída do comando acima deve ser:

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>Além disso, você também pode consultar os seguintes recursos:
>
>* Para obter mais informações sobre Páginas Enormes e Transparentes no Red Hat Linux, consulte esta seção [artigo](https://access.redhat.com/solutions/46111).
>* Para ver dicas de ajuste do Linux, consulte esta seção [artigo](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).
>


## Manutenção do repositório {#maintaining-the-repository}

Cada atualização no repositório cria uma nova revisão de conteúdo. Como resultado, a cada atualização o tamanho do repositório aumenta. Para evitar o crescimento descontrolado do repositório, as revisões antigas precisam ser limpas para liberar recursos de disco. Essa funcionalidade de manutenção é chamada de Revisão de limpeza. O mecanismo de Limpeza de Revisão recuperará o espaço em disco, removendo dados obsoletos do repositório. Para obter mais detalhes sobre a Limpeza de Revisão, leia a [Página Limpeza de Revisão](/help/sites-deploying/revision-cleanup.md).
