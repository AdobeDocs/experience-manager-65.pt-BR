---
title: Como executar AEM com TarMK Cold Standby
description: Saiba como criar, configurar e manter uma configuração de Modo de espera forçado TarMK.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
feature: Administering
exl-id: dadde3ee-d60c-4b87-9af0-a12697148161
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 3aa55b88f589749fb49d5ff46340b0912d490157
workflow-type: tm+mt
source-wordcount: '2673'
ht-degree: 0%

---

# Como executar AEM com TarMK Cold Standby{#how-to-run-aem-with-tarmk-cold-standby}

## Introdução {#introduction}

A capacidade de espera a frio do Tar Micro Kernel permite que uma ou mais instâncias de Adobe Experience Manager em standby (AEM) se conectem a uma instância primária. O processo de sincronização é apenas unidirecional, o que significa que ele só é feito das instâncias principal para as stand-by.

A finalidade das instâncias em standby é garantir uma cópia de dados em tempo real do repositório mestre e garantir uma troca rápida sem perda de dados, caso o mestre não esteja disponível por algum motivo.

O conteúdo é sincronizado linearmente entre a instância principal e as instâncias standby sem qualquer verificação de integridade para corrupção de arquivos ou repositórios. Por causa desse design, as instâncias em espera são cópias exatas da instância principal e não podem ajudar a atenuar inconsistências nas instâncias principais.

>[!NOTE]
>
>O recurso de Espera a Frio destina-se a proteger cenários em que a alta disponibilidade é necessária em instâncias do **Author**. Para situações em que a alta disponibilidade é necessária em instâncias do **Publish** usando o Tar Micro Kernel, a Adobe recomenda o uso de um farm de publicação.
>
>Para obter informações sobre mais implantações disponíveis, consulte a página [Implantações Recomendadas](/help/sites-deploying/recommended-deploys.md).

>[!NOTE]
>
>Quando a instância em Standby é configurada ou derivada do nó Principal, ela permite acesso somente à seguinte console (para atividades relacionadas à administração):
>
>* Console da Web OSGI
>
>Outros consoles não estão acessíveis.

## Como funciona {#how-it-works}

Na instância primária do AEM, uma porta TCP é aberta e está escutando as mensagens recebidas. Atualmente, há dois tipos de mensagens que os escravos enviam ao mestre:

* uma mensagem solicitando a ID de segmento do cabeçalho atual
* uma mensagem solicitando dados de segmento com uma ID especificada

O standby solicita periodicamente o ID do segmento do cabeçalho atual do principal. Se o segmento for desconhecido localmente, ele será recuperado. Se já estiver presente, os segmentos serão comparados e os segmentos referenciados também serão solicitados, se necessário.

>[!NOTE]
>
>As instâncias em espera não estão recebendo nenhum tipo de solicitação porque estão sendo executadas no modo somente sincronização. A única seção disponível em uma instância em standby é o Console da Web, para facilitar a configuração de pacotes e serviços.

Uma implantação típica de TarMK em espera forçada:

![chlimage_1](assets/chlimage_1.png)

## Outras características {#other-characteristics}

### Robustez {#robustness}

O fluxo de dados é projetado para detectar e lidar automaticamente com problemas de conexão e relacionados à rede. Todos os pacotes são agrupados com somas de verificação e quando ocorrem problemas com a conexão ou pacotes danificados, os mecanismos de repetição são acionados.

#### Desempenho {#performance}

A ativação do TarMK Cold Standby na instância principal quase não tem impacto mensurável no desempenho. O consumo adicional de CPU é baixo e o disco rígido extra e a E/S de rede não devem produzir problemas de desempenho.

No standby, você pode esperar um alto consumo de CPU durante o processo de sincronização. Como o procedimento não é multithread, ele não pode ser acelerado com o uso de vários núcleos. Se nenhum dado for alterado ou transferido, não haverá atividade mensurável. A velocidade da conexão varia dependendo do hardware e do ambiente de rede, mas não depende do tamanho do repositório ou do uso do SSL. Lembre-se disso ao estimar o tempo necessário para uma sincronização inicial ou quando muitos dados foram alterados enquanto isso no nó principal.

#### Segurança {#security}

Supondo que todas as instâncias sejam executadas na mesma zona de segurança da intranet, o risco de violação de segurança é bastante reduzido. No entanto, você pode adicionar uma camada de segurança extra, habilitando conexões SSL entre os subordinados e o principal. Isso reduz a possibilidade de os dados serem comprometidos por um homem no meio.

Além disso, você pode especificar as instâncias em standby que têm permissão para se conectar, restringindo o endereço IP das solicitações recebidas. Isso deve ajudar a garantir que ninguém na intranet possa copiar o repositório.

>[!NOTE]
>
>É recomendável que um balanceador de carga seja adicionado entre o Dispatcher e os servidores que fazem parte da configuração de Espera a frio. O balanceador de carga deve ser configurado para direcionar o tráfego de usuários somente para a instância **principal**. Isso é necessário para garantir a consistência e impedir que o conteúdo seja copiado na instância em espera por outros meios que não o mecanismo de Espera Interrompida.

## Criação de uma configuração de espera a frio AEM TarMK {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>O PID para o armazenamento de nó de segmento e o serviço de armazenamento em espera foi alterado no AEM 6.3 em comparação às versões anteriores, da seguinte maneira:
>
>* de org.apache.jackrabbit.oak.**plugins**.segment.standby.store.StandbyStoreService para org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* de org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService para org.apache.jackrabbit.oak.segment.SegmentNodeStoreService
>
>Faça os ajustes de configuração necessários para que reflitam essa alteração.

Para criar uma configuração de standby frio do TarMK, primeiro crie as instâncias de standby executando uma cópia do sistema de arquivos de toda a pasta de instalação do principal para um novo local. Você pode iniciar cada instância com um modo de execução que especifique sua função ( `primary` ou `standby`).

Abaixo está o procedimento que deve ser seguido para criar uma configuração com uma instância mestre e uma instância standby:

1. Instale o AEM.

1. Desative a instância e copie a pasta de instalação para o local de onde a instância em espera desativada é executada. Mesmo se você estiver executando em máquinas diferentes, dê a cada pasta um nome descritivo (como *aem-primary* ou *aem-standby*) para diferenciar as instâncias.
1. Vá para a pasta de instalação da instância primária e:

   1. Verifique e exclua todas as configurações de OSGi anteriores que você possa ter em `aem-primary/crx-quickstart/install`

   1. Criar uma pasta chamada `install.primary` em `aem-primary/crx-quickstart/install`

   1. Crie as configurações necessárias para o armazenamento de nó preferencial e o armazenamento de dados em `aem-primary/crx-quickstart/install/install.primary`
   1. Crie um arquivo chamado `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` no mesmo local e configure-o adequadamente. Para obter mais informações sobre as opções de configuração, consulte [Configuração](/help/sites-deploying/tarmk-cold-standby.md#configuration).

   1. Se você estiver usando uma instância AEM TarMK com um armazenamento de dados externo, crie uma pasta chamada `crx3` em `aem-primary/crx-quickstart/install` chamada `crx3`

   1. Coloque o arquivo de configuração do armazenamento de dados na pasta `crx3`.

   Por exemplo, se estiver executando uma instância AEM TarMK com um Armazenamento de dados de arquivo externo, você precisará desses arquivos de configuração:

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   Abaixo, encontre configurações de exemplo para a instância primária:

   **Amostra de** **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **Amostra de org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="primary"
   port=I"8023"
   ```

   **Amostra de org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. Inicie o principal certificando-se de especificar o modo de execução principal:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Crie um Agente de log do Apache Sling para o pacote **org.apache.jackrabbit.oak.segment**. Defina o nível de log como &quot;Depurar&quot; e aponte sua saída de log para um arquivo de log separado, como */logs/tarmk-coldstandby.log*. Para obter mais informações, consulte [Log](/help/sites-deploying/configure-logging.md).
1. Vá para o local da instância **standby** e inicie-a executando o jar.
1. Crie a mesma configuração de log para o principal. Em seguida, pare a instância.
1. Em seguida, prepare a instância standby. Você pode fazer isso executando as mesmas etapas da instância primária:

   1. Exclua todos os arquivos que você possa ter em `aem-standby/crx-quickstart/install`.
   1. Criar uma pasta chamada `install.standby` em `aem-standby/crx-quickstart/install`

   1. Crie dois arquivos de configuração chamados:

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`

   1. Criar uma pasta chamada `crx3` em `aem-standby/crx-quickstart/install`

   1. Crie a configuração do repositório de dados e coloque-a em `aem-standby/crx-quickstart/install/crx3`. Neste exemplo, o arquivo que você deve criar é:

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config

   1. Edite os arquivos e crie as configurações necessárias.

   Abaixo estão exemplos de arquivos de configuração para uma instância standby típica:

   **Amostra de org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **Amostra de org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="standby"
   primary.host="127.0.0.1"
   port=I"8023"
   secure=B"false"
   interval=I"5"
   standby.autoclean=B"true"
   ```

   **Amostra de org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. Inicie a instância **em espera** usando o modo de execução em espera:

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

O serviço também pode ser configurado por meio do Console da Web, através:

1. Acessando o Console da Web em: *https://serveraddress:serverport/system/console/configMgr*
1. Procurando um serviço chamado **Apache Jackrabbit Oak Segment Tar Cold Standby Service** e clique duas vezes nele para editar as configurações.
1. Salvar as configurações e reiniciar as instâncias para que as novas configurações tenham efeito.

>[!NOTE]
>
>Você pode verificar a função de uma instância a qualquer momento verificando a presença dos modos de execução **principal** ou **standby** no Console da Web de Configurações do Sling.
>
>Isso pode ser feito indo até *https://localhost:4502/system/console/status-slingsettings* e verificando a linha **&quot;Modos de Execução&quot;**.

## Primeira sincronização {#first-time-synchronization}

Após a conclusão da preparação e o stand-by ser iniciado pela primeira vez, há um tráfego de rede pesado entre as instâncias, à medida que o stand-by alcança o principal. Você pode consultar os logs para observar o status da sincronização.

No *tarmk-coldstandby.log* em espera, você pode ver entradas como estas:

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

No *error.log* do standby, você deve ver uma entrada como esta:

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

No trecho de log acima, *10.20.30.40* é o endereço IP do primário.

No **primary** *tarmk-coldstandby.log*, você vê entradas como estas:

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message 's.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd' from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

Nesse caso, o &quot;cliente&quot; mencionado no log é a instância **standby**.

Quando essas entradas deixarem de aparecer no log, você poderá presumir com segurança que o processo de sincronização está concluído.

Embora as entradas acima mostrem que o mecanismo de pesquisa está funcionando corretamente, geralmente é útil compreender se há dados sendo sincronizados à medida que a pesquisa ocorre. Para fazer isso, procure entradas como as seguintes:

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

Além disso, ao executar com um `FileDataStore` não compartilhado, mensagens como a seguir confirmam que os arquivos binários estão sendo transmitidos corretamente:

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### Configuração {#configuration}

As seguintes configurações de OSGi estão disponíveis para o serviço de Espera a Frio:

* **Persistir Configuração:** se habilitada, armazena a configuração no repositório em vez dos arquivos de configuração OSGi tradicionais. A Adobe recomenda que você mantenha essa configuração desativada nos sistemas de produção para que a configuração principal não seja obtida pelo standby.

* **Modo (`mode`):** esta opção escolhe o modo de execução da instância.

* **Porta (port):** a porta a ser usada para comunicação. O padrão é `8023`.

* **Host primário (`primary.host`):** - o host da instância primária. Essa configuração só é aplicável para o standby.
* **Intervalo de sincronização (`interval`):** - esta configuração determina o intervalo entre a solicitação de sincronização e só é aplicável para a instância em espera.

* **Intervalos IP permitidos (`primary.allowed-client-ip-ranges`):** - os intervalos IP dos quais o primário permite conexões.
* **Seguro (`secure`):** Habilitar criptografia SSL. Para usar essa configuração, ela deve ser ativada em todas as instâncias.
* **Tempo Limite de Leitura em Espera (`standby.readtimeout`):** Tempo limite para solicitações emitidas da instância em espera em milissegundos. O valor padrão usado é 60000 (um minuto).

* **Limpeza Automática em Espera (`standby.autoclean`):** Chame o método de limpeza se o tamanho do repositório aumentar em um ciclo de sincronização.

>[!NOTE]
>
>A Adobe recomenda que o principal e o standby tenham IDs de repositório diferentes para identificá-los separadamente para serviços como Descarregamento.
>
>A melhor maneira de garantir que isso seja coberto é excluir *sling.id* no modo de espera e reiniciar a instância.

## Procedimentos de failover {#failover-procedures}

Caso a instância principal falhe por algum motivo, você poderá definir uma das instâncias stand-by para assumir a atribuição da principal alterando o modo de execução inicial conforme detalhado abaixo:

>[!NOTE]
>
>Edite os arquivos de configuração de forma que eles correspondam às configurações usadas para a instância primária.

1. Vá para o local onde a instância stand-by está instalada e interrompa-a.

1. Caso tenha um balanceador de carga configurado, é possível remover o primário da configuração do balanceador nesse ponto.
1. Faça backup da pasta `crx-quickstart` a partir da pasta de instalação em espera. Ele pode ser usado como ponto de partida ao configurar um novo standby.

1. Reinicie a instância usando o modo de execução `primary`:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Adicione o novo principal ao balanceador de carga.
1. Crie e inicie uma nova instância standby. Para obter mais informações, consulte o procedimento acima em [Criando uma Instalação de Espera a Frio AEM TarMK](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## Aplicando Hotfixes a uma Configuração de Modo de Espera a Frio {#applying-hotfixes-to-a-cold-standby-setup}

A maneira recomendada de aplicar hotfixes a uma configuração de standby inativo é instalando-os na instância primária e clonando-a em uma nova instância de standby inativo com os hotfixes instalados.

Você pode fazer isso seguindo as etapas descritas abaixo:

1. Interrompa o processo de sincronização na instância em espera desativada acessando a Console JMX e usando o bean **org.apache.jackrabbit.oak: Status (&quot;Standby&quot;)**. Para obter mais informações sobre como fazer isso, consulte a seção sobre [Monitoramento](#monitoring).
1. Interrompa a instância em espera desativada.
1. Instale o hotfix na instância primária. Para obter mais detalhes sobre como instalar uma correção, consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md).
1. Teste a instância em busca de problemas após a instalação.
1. Remova a instância em espera ativa excluindo sua pasta de instalação.
1. Interrompa a instância principal e clone-a executando uma cópia do sistema de arquivos de toda a pasta de instalação no local do standby frio.
1. Reconfigure o clone recém-criado para que ele atue como uma instância em espera inativa. Consulte [Criando uma Instalação de Modo de Espera a Frio AEM TarMK.](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. Inicie as instâncias principal e stand-by frio.

## Monitoramento {#monitoring}

O recurso expõe informações usando JMX ou MBeans. Dessa forma, você pode inspecionar o estado atual do standby e do master usando o [console JMX](/help/sites-administering/jmx-console.md). As informações podem ser encontradas em um MBean de `type org.apache.jackrabbit.oak:type="Standby"`chamado `Status`.

**Em Espera**

Observando uma instância standby, você expõe um nó. A ID geralmente é um UUID genérico.

Este nó tem cinco atributos somente leitura:

* `Running:` valor booleano indicando se o processo de sincronização está em execução ou não.

* Cliente `Mode:`: seguido pela UUID usada para identificar a instância. Essa UUID é alterada sempre que a configuração é atualizada.

* `Status:` uma representação textual do estado atual (como `running` ou `stopped`).

* `FailedRequests:`o número de erros consecutivos.
* `SecondsSinceLastSuccess:` o número de segundos desde a última comunicação bem-sucedida com o servidor. Ele exibe `-1` se nenhuma comunicação bem-sucedida foi feita.

Há também três métodos que podem ser chamados:

* `start():` inicia o processo de sincronização.
* `stop():` para o processo de sincronização.
* `cleanup():` executa a operação de limpeza no modo de espera.

**Principal**

A observação do principal expõe algumas informações gerais por meio de um MBean cujo valor de ID é o número da porta que o serviço de standby TarMK está usando (8023 por padrão). A maioria dos métodos e atributos são os mesmos do standby, mas alguns diferem:

* `Mode:` sempre mostra o valor `primary`.

Além disso, é possível recuperar informações para até dez clientes (instâncias stand-by) conectados ao mestre. A ID do MBean é a UUID da instância. Não há métodos chamáveis para esses MBeans, mas alguns atributos úteis somente leitura:

* `Name:` a ID do cliente.
* `LastSeenTimestamp:` o carimbo de data/hora da última solicitação em uma representação textual.
* `LastRequest:` a última solicitação do cliente.
* `RemoteAddress:` o endereço IP do cliente.
* `RemotePort:` a porta que o cliente usou para a última solicitação.
* `TransferredSegments:` o número total de segmentos transferidos para este cliente.
* `TransferredSegmentBytes:`o número total de bytes transferidos para este cliente.

## Manutenção do repositório de espera a frio {#cold-standby-repository-maintenance}

### Limpeza de revisão {#revision-clean}

>[!NOTE]
>
>Se você executar a [Limpeza de Revisão Online](/help/sites-deploying/revision-cleanup.md) na instância primária, o procedimento manual apresentado abaixo não será necessário. Além disso, se você estiver usando a Limpeza de revisão online, a operação `cleanup ()` na instância em espera será executada automaticamente.

>[!NOTE]
>
>Não execute a limpeza de revisão off-line no standby. Ela não é necessária e não reduz o tamanho do armazenamento de segmentos.

A Adobe recomenda executar a manutenção regularmente para evitar o crescimento excessivo do repositório ao longo do tempo. Para executar manualmente a manutenção do repositório em standby frio, siga as etapas abaixo:

1. Interrompa o processo em espera na instância em espera acessando o Console JMX e usando o bean **org.apache.jackrabbit.oak: Status (&quot;Standby&quot;)**. Para obter mais informações sobre como fazer isso, consulte a seção acima em [Monitoramento](/help/sites-deploying/tarmk-cold-standby.md#monitoring).

1. Interrompa a instância primária do AEM.
1. Execute a ferramenta de compactação Oak na instância primária. Para obter mais detalhes, consulte [Manutenção do Repositório](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. Inicie a instância primária.
1. Inicie o processo standby na instância standby usando o mesmo bean JMX, conforme descrito na primeira etapa.
1. Assista aos logs e aguarde a conclusão da sincronização. É possível que o crescimento substancial no repositório em standby seja visto atualmente.
1. Execute a operação `cleanup()` na instância em espera usando o mesmo bean JMX descrito na primeira etapa.

Pode levar mais tempo do que o normal para a instância standby concluir a sincronização com o principal, já que a compactação offline efetivamente reescreve o histórico do repositório, tornando o cálculo das alterações nos repositórios mais demorado. Após a conclusão desse processo, o tamanho do repositório no stand-by será aproximadamente do mesmo tamanho do repositório no principal.

Como alternativa, o repositório principal pode ser copiado manualmente para o stand-by depois de executar a compactação no principal, essencialmente reconstruindo o stand-by sempre que a compactação for executada.

### Coleta de lixo do armazenamento de dados {#data-store-garbage-collection}

É importante executar a coleta de lixo nas instâncias do armazenamento de dados de arquivos de tempos em tempos, caso contrário, os binários excluídos permanecerão no sistema de arquivos, eventualmente preenchendo a unidade. Para executar a coleta de lixo, siga o procedimento abaixo:

1. Execute a manutenção do repositório em espera forçada conforme descrito na seção [acima](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. Após a conclusão do processo de manutenção e a reinicialização das instâncias:

   * Na principal, execute a coleta de lixo do armazenamento de dados por meio do bean JMX relevante, conforme descrito em [Executando a coleta de lixo do armazenamento de dados pelo Console JMX](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * No modo de espera, a coleta de lixo do armazenamento de dados está disponível somente por meio do **BlobGarbageCollection** MBean - `startBlobGC()`. O MBean **RepositoryManagement** não está disponível no modo de espera.

   >[!NOTE]
   >
   >Caso não esteja usando um armazenamento de dados compartilhado, execute a coleta de lixo primeiro no principal e, em seguida, no stand-by.
