---
title: Elementos do armazenamento no AEM 6.5
seo-title: Elementos do armazenamento no AEM 6.5
description: Saiba mais sobre as implementações de armazenamento de nó disponíveis no AEM 6.5 e como manter o repositório.
seo-description: Saiba mais sobre as implementações de armazenamento de nó disponíveis no AEM 6.5 e como manter o repositório.
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---


# Elementos de armazenamento no AEM 6.5{#storage-elements-in-aem}

Neste artigo, cobriremos:

* [Visão geral do Armazenamento no AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Manutenção do repositório](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## Visão geral do Armazenamento no AEM 6 {#overview-of-storage-in-aem}

Uma das alterações mais importantes no AEM 6 são as inovações a nível do repositório.

Atualmente, há duas implementações de armazenamento de nó disponíveis no AEM6: Armazenamento Tar e armazenamento MongoDB.

### Armazenamento de barra {#tar-storage}

#### Execução de uma instância AEM recém-instalada com o Armazenamento Tar {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>O PID do armazenamento de nó Segmento foi alterado de org.apache.Jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService em versões anteriores do AEM 6 para org.apache.Jackrabbit.oak.segment.SegmentNodeStoreService no AEM 6.3. Certifique-se de fazer os ajustes de configuração necessários para refletir essa alteração.

Por padrão, o AEM 6 usa o armazenamento Tar para armazenar nós e binários, usando as opções de configuração padrão. Para configurar manualmente suas configurações de armazenamento, siga o procedimento abaixo:

1. Baixe o AEM 6 quickstart jar e coloque-o em uma nova pasta.
1. Desempacotar AEM executando:

   `java -jar cq-quickstart-6.jar -unpack`

1. Crie uma pasta chamada `crx-quickstart\install` no diretório de instalação.

1. Crie um arquivo chamado `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` na pasta recém-criada.

1. Edite o arquivo e defina as opções de configuração. As opções a seguir estão disponíveis para a Loja de Nó de Segmento, que é a base AEM implementação do armazenamento Tar:

   * `repository.home`: Caminho para a home do repositório no qual vários dados relacionados ao repositório são armazenados. Por padrão, os arquivos de segmento seriam armazenados no diretório crx-quickstart/segmentstore.
   * `tarmk.size`: Tamanho máximo de um segmento em MB. O padrão é 256 MB.

1. Start AEM.

### Armazenamento Mongo {#mongo-storage}

#### Execução de uma instância AEM recém-instalada com o Armazenamento Mongo {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM 6 pode ser configurado para execução com o armazenamento MongoDB seguindo o procedimento abaixo:

1. Baixe o AEM 6 quickstart jar e coloque-o em uma nova pasta.
1. Desempacotar AEM executando o seguinte comando:

   `java -jar cq-quickstart-6.jar -unpack`

1. Verifique se MongoDB está instalado e se uma instância de `mongod` está em execução. Para obter mais informações, consulte [Instalando MongoDB](https://docs.mongodb.org/manual/installation/).
1. Crie uma pasta chamada `crx-quickstart\install` no diretório de instalação.
1. Configure o armazenamento de nós criando um arquivo de configuração com o nome da configuração que você deseja usar no diretório `crx-quickstart\install`.

   O Documento Node Store (que é a base para a implementação AEM armazenamento MongoDB) usa um arquivo chamado `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. Edite o arquivo e defina suas opções de configuração. As opções disponíveis são as seguintes:

   * `mongouri`: O  [](https://docs.mongodb.org/manual/reference/connection-string/) MongoURI é necessário para se conectar ao Banco de Dados Mongo. O padrão é `mongodb://localhost:27017`
   * `db`: Nome do banco de dados Mongo. Por padrão, as novas instalações AEM 6 usam **aem-author** como o nome do banco de dados.
   * `cache`: O tamanho do cache em MB. Isso é distribuído entre vários caches usados no DocumentNodeStore. O padrão é 256.
   * `changesSize`: Tamanho em MB da coleção com limites usada no Mongo para armazenar a saída do diff em cache. O padrão é 256.
   * `customBlobStore`: Valor booliano que indica que um armazenamento de dados personalizado será usado. O padrão é false.

1. Crie um arquivo de configuração com o PID do armazenamento de dados que deseja usar e edite o arquivo para definir as opções de configuração. Para obter mais informações, consulte [Configuração de armazenamento de nó e armazenamento de dados](/help/sites-deploying/data-store-config.md).

1. Start o jar AEM 6 com um backend de armazenamento MongoDB executando:

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   Onde **`-r`** é o modo de execução de backend. Neste exemplo, ele será start com suporte a MongoDB.

#### Desabilitando páginas imensas transparentes {#disabling-transparent-huge-pages}

O Red Hat Linux usa um algoritmo de gerenciamento de memória chamado THP (Transparent Huge Pages). Enquanto AEM realiza leituras e gravações de granulação fina, o THP é otimizado para operações grandes. Por isso, é recomendável desativar o THP tanto no armazenamento Tar quanto no Mongo. Para desativar o algoritmo, siga estas etapas:

1. Abra o arquivo `/etc/grub.conf` no editor de texto de sua escolha.
1. Adicione a seguinte linha ao arquivo **grub.conf**:

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
>* Para obter mais informações sobre páginas enormes transparentes no Red Hat Linux, consulte este [artigo](https://access.redhat.com/solutions/46111).
>* Para obter dicas de ajuste do Linux, consulte este [artigo](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

>



## Manutenção do repositório {#maintaining-the-repository}

Cada atualização no repositório cria uma nova revisão de conteúdo. Como resultado, a cada atualização o tamanho do repositório aumenta. Para evitar o crescimento descontrolado do repositório, é necessário limpar revisões antigas para liberar recursos de disco. Esta funcionalidade de manutenção é chamada de Limpeza de revisão. O mecanismo de Limpeza de revisão recuperará o espaço em disco ao remover dados obsoletos do repositório. Para obter mais detalhes sobre a Limpeza de revisão, leia a página [Limpeza de revisão](/help/sites-deploying/revision-cleanup.md).
