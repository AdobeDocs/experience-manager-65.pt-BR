---
title: Elementos de armazenamento no AEM 6.5
description: Saiba mais sobre as implementações de armazenamento de nós disponíveis no AEM 6.5 e como fazer a manutenção do repositório.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 52437eb5-f9fb-4945-9950-5a1562fe878d
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: db7830895c8a2d1b7228dc4780296d43f15776df
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# Elementos de armazenamento no AEM 6.5{#storage-elements-in-aem}

Este artigo abrange o seguinte:

* [Visão geral do armazenamento no AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Manutenção do repositório](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## Visão geral do armazenamento no AEM 6 {#overview-of-storage-in-aem}

Uma das mudanças mais importantes no AEM 6 são as inovações no nível dos repositórios.

Atualmente, existem duas implementações de armazenamento de nó disponíveis no AEM6: armazenamento Tar e armazenamento MongoDB.

### Armazenamento Tar {#tar-storage}

#### Executando uma instância do AEM recém-instalada com Armazenamento Tar {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>O PID do armazenamento de nós do segmento foi alterado de org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService em versões anteriores do AEM 6 para org.apache.jackrabbit.oak.segment.SegmentNodeStoreService no AEM 6.3. Verifique se os ajustes de configuração necessários foram feitos para que as alterações sejam refletidas.

Por padrão, o AEM 6 usa o armazenamento Tar para armazenar nós e binários, usando as opções de configuração padrão. Você pode definir manualmente suas configurações de armazenamento fazendo o seguinte:

1. Baixe o jar de início rápido do AEM 6 e coloque-o em uma nova pasta.
1. Descompacte o AEM executando:

   `java -jar cq-quickstart-6.jar -unpack`

1. Crie uma pasta chamada `crx-quickstart\install` no diretório de instalação.

1. Crie um arquivo chamado `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` na pasta recém-criada.

1. Edite o arquivo e defina as opções de configuração. As seguintes opções estão disponíveis para o Armazenamento de nós do segmento, que é a base da implementação do armazenamento Tar do AEM:

   * `repository.home`: Caminho para a página inicial do repositório sob a qual vários dados relacionados ao repositório são armazenados. Por padrão, os arquivos de segmento seriam armazenados no diretório crx-quickstart/segmentstore.
   * `tarmk.size`: Tamanho máximo de um segmento em MB. O padrão é 256 MB.

1. Inicie o AEM.

### Armazenamento Mongo {#mongo-storage}

#### Execução de uma instância do AEM recém-instalada com o Mongo Storage {#running-a-freshly-installed-aem-instance-with-mongo-storage}

O AEM 6 pode ser configurado para ser executado com o armazenamento MongoDB seguindo o procedimento abaixo:

1. Baixe o jar de início rápido do AEM 6 e coloque-o em uma nova pasta.
1. Descompacte o AEM executando o seguinte comando:

   `java -jar cq-quickstart-6.jar -unpack`

1. Verifique se o MongoDB está instalado e se uma instância de `mongod` está em execução. Para obter mais informações, consulte [Instalando MongoDB](https://docs.mongodb.org/manual/installation/).
1. Crie uma pasta chamada `crx-quickstart\install` no diretório de instalação.
1. Configure o armazenamento de nós criando um arquivo de configuração com o nome da configuração que você deseja usar no diretório `crx-quickstart\install`.

   O Document Node Store (que é a base para a implementação de armazenamento MongoDB do AEM) usa um arquivo chamado `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. Edite o arquivo e defina suas opções de configuração. As opções disponíveis são as seguintes:

   * `mongouri`: O [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) necessário para se conectar ao Banco de Dados Mongo. O padrão é `mongodb://localhost:27017`
   * `db`: Nome do banco de dados Mongo. Por padrão, as novas instalações do AEM 6 usam **aem-author** como o nome do banco de dados.
   * `cache`: O tamanho do cache em megabytes. Esse tamanho do cache é distribuído entre vários caches usados no DocumentNodeStore. O padrão é 256.
   * `changesSize`: Tamanho em MB da coleção limitada usada em Mongo para armazenar a saída do diff em cache. O padrão é 256.
   * `customBlobStore`: valor booleano indicando que um armazenamento de dados personalizado está sendo usado. O padrão é false.

1. Crie um arquivo de configuração com o PID do armazenamento de dados que deseja usar e edite o arquivo para definir as opções de configuração. Para obter mais informações, consulte [Configurando Armazenamento de Nós e Armazenamento de Dados](/help/sites-deploying/data-store-config.md).

1. Inicie o jar do AEM 6 com um back-end de armazenamento do MongoDB executando:

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   Quando o modo de execução de back-end é **`-r`**, o exemplo começa com suporte a MongoDB.

#### Desativar páginas grandes transparentes {#disabling-transparent-huge-pages}

O Red Hat® Linux® usa um algoritmo de gerenciamento de memória chamado THP (Transparent Huge Pages). Enquanto o AEM executa leituras e gravações refinadas, o THP é otimizado para operações grandes. Portanto, é recomendável desativar o THP no armazenamento Tar e Mongo. Para desativar o algoritmo, siga estas etapas:

1. Abra o arquivo `/etc/grub.conf` no editor de texto de sua escolha.
1. Adicione a seguinte linha ao arquivo **grub.conf**:

   ```
   transparent_hugepage=never
   ```

1. Por fim, verifique se a configuração foi aplicada executando:

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Se o THP estiver desativado, a saída do comando acima deve ser:

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>Consulte os seguintes recursos:
>
>* Para obter mais informações sobre o Transparent Huge Pages no Red Hat® Linux®, consulte o seguinte artigo no Red Hat® Customer Portal: [Como usar, monitorar e desativar páginas transparentes no Red Hat Enterprise Linux 6, 7 e 8?](https://access.redhat.com/solutions/46111)
>* Para obter dicas de ajuste do Linux®, consulte [Otimização do Desempenho](/help/sites-deploying/configuring-performance.md).
>

## Manutenção do repositório {#maintaining-the-repository}

Cada atualização no repositório cria uma revisão de conteúdo. Como resultado, a cada atualização o tamanho do repositório aumenta. Para evitar o crescimento descontrolado do repositório, as revisões antigas devem ser removidas para liberar recursos de disco. Essa funcionalidade de manutenção é chamada de Limpeza de revisão. O mecanismo de Limpeza de revisão recupera espaço em disco removendo dados obsoletos do repositório. Para obter mais detalhes sobre a Limpeza de revisão, leia a [página Limpeza de revisão](/help/sites-deploying/revision-cleanup.md).
