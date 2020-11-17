---
title: Como executar AEM com o modo de espera refrigerado TarMK
seo-title: Como executar AEM com o modo de espera refrigerado TarMK
description: Saiba como criar, configurar e manter uma configuração TarMK Cold Standby.
seo-description: Saiba como criar, configurar e manter uma configuração TarMK Cold Standby.
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
translation-type: tm+mt
source-git-commit: a99c5794cee88d11ca3fb9eeed443c4d0178c7b3
workflow-type: tm+mt
source-wordcount: '2731'
ht-degree: 0%

---


# Como executar AEM com o modo de espera refrigerado TarMK{#how-to-run-aem-with-tarmk-cold-standby}

## Introdução {#introduction}

A capacidade de Espera Fria do Tar Micro Kernel permite que uma ou mais instâncias de AEM stand-by se conectem a uma instância primária. O processo de sincronização é uma forma somente de fazer isso apenas das instâncias primárias às de espera.

A finalidade das instâncias stand-by é garantir uma cópia de dados em tempo real do repositório principal e garantir um switch rápido sem perda de dados, caso o principal não esteja disponível por qualquer motivo.

O conteúdo é sincronizado linearmente entre a instância principal e as instâncias stand-by, sem qualquer verificação de integridade para detecção de danos no arquivo ou repositório. Devido a esse design, as instâncias stand-by são cópias exatas da instância principal e não podem ajudar a atenuar inconsistências em instâncias primárias.

>[!NOTE]
>
>O recurso Modo de espera frio é projetado para proteger cenários em que a alta disponibilidade é necessária em instâncias do **autor** . Para situações em que a alta disponibilidade é necessária em instâncias de **publicação** usando o Tar Micro Kernel, o Adobe recomenda o uso de um farm de publicação.
>
>Para obter informações sobre implantações mais disponíveis, consulte a página Implantações [](/help/sites-deploying/recommended-deploys.md) recomendadas.

## Como funciona {#how-it-works}

Na instância principal do AEM, uma porta TCP é aberta e está ouvindo mensagens recebidas. Atualmente, há dois tipos de mensagens que os escravos enviarão ao principal:

* uma mensagem solicitando a ID do segmento do cabeçalho atual
* uma mensagem solicitando dados de segmento com uma ID especificada

O modo de espera solicita periodicamente a ID do segmento do cabeçalho atual do primário. Se o segmento for localmente desconhecido, ele será recuperado. Se já estiver presente, os segmentos serão comparados e os segmentos referenciados também serão solicitados, se necessário.

>[!NOTE]
>
>As instâncias em espera não recebem nenhum tipo de solicitação, pois estão sendo executadas no modo somente sincronização. A única seção disponível em uma instância stand-by é o Console da Web, para facilitar a configuração de pacotes e serviços.

Uma implantação típica do TarMK Cold Standby:

![chlimage_1](assets/chlimage_1.png)

## Outras características {#other-characteristics}

### Robustez {#robustness}

O fluxo de dados é projetado para detectar e lidar automaticamente com problemas relacionados à conexão e à rede. Todos os pacotes são agrupados com somas de verificação e assim que ocorrem problemas com a conexão ou pacotes danificados, os mecanismos de nova tentativa são acionados.

#### Show {#performance}

A ativação do TarMK Cold Standby na instância primária quase não tem impacto mensurável no desempenho. O consumo adicional da CPU é muito baixo e o disco rígido extra e a E/S de rede não devem gerar problemas de desempenho.

No modo de espera, você pode esperar alto consumo de CPU durante o processo de sincronização. Devido ao fato de o procedimento não ser multisegmentado, ele não pode ser acelerado usando vários núcleos. Se nenhum dado for alterado ou transferido, não haverá atividade mensurável. A velocidade da conexão varia dependendo do hardware e do ambiente da rede, mas não depende do tamanho do repositório ou do uso do SSL. Lembre-se disso ao estimar o tempo necessário para uma sincronização inicial ou quando muitos dados foram alterados enquanto isso no nó primário.

#### Segurança {#security}

Supondo que todas as instâncias ocorrem na mesma zona de segurança da intranet, o risco de violação de segurança é muito reduzido. No entanto, é possível adicionar uma camada de segurança adicional, permitindo conexões SSL entre os escravos e os principais. Isso reduz a possibilidade de os dados serem comprometidos por um homem no meio.

Além disso, você pode especificar as instâncias stand-by que podem se conectar restringindo o endereço IP das solicitações recebidas. Isso deve ajudar a garantir que ninguém na intranet possa copiar o repositório.

>[!NOTE]
>
>É recomendável adicionar um balanceador de carga entre o Dispatcher e os servidores que fazem parte da configuração do Coldy Standby. O balanceador de carga deve ser configurado para direcionar o tráfego do usuário somente para a instância **principal** , a fim de garantir a consistência e impedir que o conteúdo seja copiado na instância stand-by por outros meios que não o mecanismo de modo de espera frio.

## Criando uma configuração AEM TarMK Cold Standby {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>O PID para o armazenamento do nó Segmento e o serviço de armazenamento Standby foram alterados no AEM 6.3 em comparação às versões anteriores da seguinte forma:
>
>* de org.apache.Jackrabbit.oak.**plugins**.segment.standby.store.StandbyStoreService para org.apache.Jackrabbit.oak.segment.standby.store.StandbyStoreService
>* de org.apache.Jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService para org.apache.Jackrabbit.oak.segment.SegmentNodeStoreService

>
>
Certifique-se de fazer os ajustes de configuração necessários para refletir essa alteração.

Para criar uma configuração TarMK Easy standby, primeiro é necessário criar as instâncias stand-by, executando uma cópia do sistema de arquivos de toda a pasta de instalação do principal em um novo local. Em seguida, você pode start cada instância com um modo de execução que especificará sua função ( `primary` ou `standby`).

Abaixo está o procedimento que precisa ser seguido para criar uma configuração com uma instância principal e uma em espera:

1. Instale o AEM.

1. Encerre a instância e copie a pasta de instalação para o local de onde a instância de espera fria será executada. Mesmo se executado de máquinas diferentes, certifique-se de atribuir um nome descritivo a cada pasta (como *aem-Primary* ou *aem-standby*) para diferenciar entre as instâncias.
1. Vá para a pasta de instalação da instância principal e:

   1. Verifique e exclua quaisquer configurações OSGi anteriores nas quais você possa ter `aem-primary/crx-quickstart/install`

   1. Criar uma pasta chamada `install.primary` em `aem-primary/crx-quickstart/install`

   1. Crie as configurações necessárias para o armazenamento de nó preferencial e o armazenamento de dados em `aem-primary/crx-quickstart/install/install.primary`
   1. Crie um arquivo chamado `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` no mesmo local e configure-o de acordo. Para obter mais informações sobre as opções de configuração, consulte [Configuração](/help/sites-deploying/tarmk-cold-standby.md#configuration).

   1. Se você estiver usando uma instância AEM TarMK com um armazenamento de dados externo, crie uma pasta com o nome `crx3` em `aem-primary/crx-quickstart/install` `crx3`

   1. Coloque o arquivo de configuração do armazenamento de dados na `crx3` pasta.

   Se, por exemplo, você estiver executando uma instância AEM TarMK com um File Data Store externo, precisará dos seguintes arquivos de configuração:

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   Abaixo, você encontrará configurações de amostra para a instância principal:

   **Amostra** de **org.apache.Jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **Amostra de org.apache.Jackrabbit.oak.segment.standby.store.StandbyStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="primary"
   port=I"8023"
   ```

   **Exemplo de org.apache.Jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. Start o principal, certificando-se de especificar o modo de execução principal:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Crie um novo Apache Sling Logging Logger para o pacote **org.apache.Jackrabbit.oak.segment** . Defina o nível de log como &quot;Depurar&quot; e aponte a saída de log para um arquivo de log separado, como */logs/tarmk-coldstandby.log*. For more information, see [Logging](/help/sites-deploying/configure-logging.md).
1. Vá para o local da instância **standby** e start-a executando o jar.
1. Crie a mesma configuração de registro que para o principal. Em seguida, pare a instância.
1. Em seguida, prepare a instância de espera. É possível fazer isso executando as mesmas etapas da instância primária:

   1. Exclua os arquivos que possam estar em `aem-standby/crx-quickstart/install`.
   1. Criar uma nova pasta chamada `install.standby` em `aem-standby/crx-quickstart/install`

   1. Crie dois arquivos de configuração chamados:

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   1. Criar uma nova pasta chamada `crx3` em `aem-standby/crx-quickstart/install`

   1. Crie a configuração do armazenamento de dados e coloque-a em `aem-standby/crx-quickstart/install/crx3`. Neste exemplo, o arquivo que você precisa criar é:

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
   1. Edite os arquivos e crie as configurações necessárias.

   Abaixo estão exemplos de arquivos de configuração para uma instância stand-by típica:

   **Exemplo de org.apache.Jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **Amostra de org.apache.Jackrabbit.oak.segment.standby.store.StandbyStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="standby"
   primary.host="127.0.0.1"
   port=I"8023"
   secure=B"false"
   interval=I"5"
   standby.autoclean=B"true"
   ```

   **Exemplo de org.apache.Jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. Start a instância **standby** usando o modo de execução standby:

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

O serviço também pode ser configurado por meio do Console da Web:

1. Ir para o Web Console em: *https://serveraddress:serverport/system/console/configMgr*
1. Procurando um serviço chamado Serviço **de espera por frio do segmento Oak do** Apache Jackrabbit Oak e clique no duplo para editar as configurações.
1. Salvar as configurações e reiniciar as instâncias para que as novas configurações tenham efeito.

>[!NOTE]
>
>Você pode verificar a função de uma instância a qualquer momento verificando a presença dos modos de execução **principal** ou **stand-by** no console da Web Sling Settings.
>
>Isso pode ser feito indo até *https://localhost:4502/system/console/status-slingsettings* e verificando a linha **&quot;Modos de execução&quot;** .

## Primeira sincronização {#first-time-synchronization}

Depois que a preparação estiver concluída e o modo de espera for iniciado pela primeira vez, haverá um tráfego intenso na rede entre as instâncias, uma vez que o modo de espera atingirá o nível principal. Você pode consultar os registros para observar o status da sincronização.

No standby *tarmk-coldstandby.log*, você verá entradas como estas:

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

No **principal** *tarmk-coldstandby.log*, você verá entradas como estas:

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

Nesse caso, o &quot;cliente&quot; mencionado no registro é a instância **standby** .

Depois que essas entradas pararem de aparecer no log, você poderá assumir com segurança que o processo de sincronização está concluído.

Embora as entradas acima mostrem que o mecanismo de pesquisa está funcionando corretamente, geralmente é útil entender se há dados sendo sincronizados enquanto a pesquisa está ocorrendo. Para fazer isso, procure entradas como as seguintes:

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

Além disso, ao executar com um arquivo não compartilhado, mensagens como `FileDataStore`a seguir confirmarão que os arquivos binários estão sendo transmitidos corretamente:

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### Configuração {#configuration}

As seguintes configurações OSGi estão disponíveis para o serviço de Modo de Espera Frio:

* **Configuração persistente:** se ativada, a configuração será armazenada no repositório em vez dos arquivos de configuração OSGi tradicionais. É recomendável manter essa configuração desativada nos sistemas de produção para que a configuração primária não seja puxada pelo modo de espera.

* **Modo (`mode`):** isso escolherá o modo de execução da instância.

* **Porta (porta):** a porta a ser usada para comunicação. O padrão é `8023`.

* **Host primário (`primary.host`):** - o host da instância principal. Esta definição só é aplicável para o modo de espera.
* **Intervalo de sincronização (`interval`):** - essa configuração determina o intervalo entre a solicitação de sincronização e é aplicável somente para a instância stand-by.

* **Intervalos de IP permitidos (`primary.allowed-client-ip-ranges`):** - os intervalos IP dos quais o principal permitirá conexões.
* **Seguro (`secure`):** Ative a criptografia SSL. Para usar essa configuração, ela deve estar ativada em todas as instâncias.
* **Tempo limite de leitura em espera (`standby.readtimeout`):** Tempo limite para solicitações emitidas da instância stand-by em milissegundos. A configuração de tempo limite recomendada é 43200000. Geralmente, recomenda-se que você defina o tempo limite para um valor de pelo menos 12 horas.

* **Limpeza automática em espera (`standby.autoclean`):** Chame o método de limpeza se o tamanho da loja aumentar em um ciclo de sincronização.

>[!NOTE]
>
>É altamente recomendável que o principal e o standby tenham IDs de repositório diferentes para torná-los separadamente identificáveis para serviços como Descarregamento.
>
>A melhor maneira de garantir que isso seja abordado é excluindo o arquivo *sling.id* no modo de espera e reiniciando a instância.

## Procedimentos de failover {#failover-procedures}

Se a instância primária falhar por qualquer motivo, você pode definir uma das instâncias stand-by para assumir a função do principal alterando o modo de execução do start, conforme detalhado abaixo:

>[!NOTE]
>
>Os arquivos de configuração também precisam ser modificados para que correspondam às configurações usadas para a instância primária.

1. Vá para o local onde a instância standby está instalada e pare-a.

1. Caso tenha um balanceador de carga configurado com a configuração, você pode remover o principal da configuração do balanceador de carga neste ponto.
1. Faça backup da `crx-quickstart` pasta da pasta de instalação stand-by. Pode ser usado como ponto de partida ao configurar um novo modo de espera.

1. Reinicie a instância usando o `primary` modo de execução:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Adicione o novo primário ao balanceador de carga.
1. Crie e start uma nova instância stand-by. Para obter mais informações, consulte o procedimento acima em [Criar uma configuração](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)AEM TarMK Cold Standby.

## Aplicação de hotfixes a uma configuração de espera fria {#applying-hotfixes-to-a-cold-standby-setup}

A maneira recomendada de aplicar hotfixes a uma configuração de espera fria é instalá-los na instância principal e cloná-los em uma nova instância de espera fria com os hotfixes instalados.

Você pode fazer isso seguindo as etapas descritas abaixo:

1. Pare o processo de sincronização na instância do modo de espera frio indo para o console JMX e usando o **org.apache.Jackrabbit.oak: Status (&quot;Standby&quot;)**bean. Para obter mais informações sobre como fazer isso, consulte a seção sobre [Monitoramento](#monitoring).
1. Pare a instância do modo de espera frio.
1. Instale o hotfix na instância principal. Para obter mais detalhes sobre como instalar uma correção, consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md).
1. Teste a instância para problemas após a instalação.
1. Remova a instância de espera fria excluindo sua pasta de instalação.
1. Pare a instância principal e clone-a executando uma cópia do sistema de arquivos de toda a pasta de instalação para o local do modo de espera frio.
1. Reconfigure o clone recém-criado para agir como uma instância de espera fria. Para obter detalhes adicionais, consulte [Criação de uma configuração AEM TarMK Cold Standby.](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. Start das instâncias principal e de espera fria.

## Monitoramento {#monitoring}

O recurso expõe informações usando JMX ou MBeans. Fazendo isso, você pode inspecionar o estado atual do modo de espera e o estado principal usando o console [](/help/sites-administering/jmx-console.md)JMX. As informações podem ser encontradas em um MBean `type org.apache.jackrabbit.oak:type="Standby"`nomeado `Status`.

**Espera**

Observando uma instância stand-by, você exporá um nó. Normalmente, a ID é um UUID genérico.

Este nó tem cinco atributos somente leitura:

* `Running:` valor booliano que indica se o processo de sincronização está em execução ou não.

* `Mode:` Cliente: seguido pela UUID usada para identificar a instância. Observe que essa UUID será alterada sempre que a configuração for atualizada.

* `Status:` uma representação textual do estado atual (como `running` ou `stopped`).

* `FailedRequests:`o número de erros consecutivos.
* `SecondsSinceLastSuccess:` o número de segundos desde a última comunicação bem-sucedida com o servidor. Ele será exibido `-1` se nenhuma comunicação for bem-sucedida.

Há também três métodos chamáveis:

* `start():` start o processo de sincronização.
* `stop():` interrompe o processo de sincronização.
* `cleanup():` executa a operação de limpeza no modo de espera.

**Primário**

A observação do primário expõe algumas informações gerais por meio de um MBean cujo valor de ID é o número da porta que o serviço de espera TarMK está usando (8023 por padrão). A maioria dos métodos e atributos são os mesmos do modo de espera, mas alguns diferem:

* `Mode:` sempre mostrará o valor `primary`.

Além disso, podem ser obtidas informações para até 10 clientes (instâncias em espera) ligados ao principal. A ID MBean é o UUID da instância. Não há métodos chamáveis para esses MBeans, mas alguns atributos somente leitura muito úteis:

* `Name:` a ID do cliente.
* `LastSeenTimestamp:` o carimbo de data e hora da última solicitação em uma representação textual.
* `LastRequest:` a última solicitação do cliente.
* `RemoteAddress:` o endereço IP do cliente.
* `RemotePort:` a porta que o cliente usou para a última solicitação.
* `TransferredSegments:` o número total de segmentos transferidos para este cliente.
* `TransferredSegmentBytes:`o número total de bytes transferidos para este cliente.

## Manutenção do Repositório Standby Frio {#cold-standby-repository-maintenance}

### Limpeza de revisão {#revision-clean}

>[!NOTE]
>
>Se você executar a Limpeza [de revisão](/help/sites-deploying/revision-cleanup.md) online na instância principal, o procedimento manual apresentado abaixo não é necessário. Além disso, se você estiver usando a Limpeza de revisão on-line, a operação na instância `cleanup ()` em espera será executada automaticamente.

>[!NOTE]
>
>Não execute a limpeza de revisão offline no modo de espera. Não é necessário e não reduzirá o tamanho do armazenamento de segmentos.

A Adobe recomenda executar a manutenção regularmente para evitar o crescimento excessivo do repositório ao longo do tempo. Para executar manualmente a manutenção do repositório em modo de espera frio, siga as etapas abaixo:

1. Pare o processo de espera na instância stand-by indo para o Console JMX e usando o **org.apache.Jackrabbit.oak: Bean de status (&quot;Standby&quot;)** . Para obter mais informações sobre como fazer isso, consulte a seção acima sobre [Monitoramento](/help/sites-deploying/tarmk-cold-standby.md#monitoring).

1. Pare a instância AEM principal.
1. Execute a ferramenta de compactação de carvalho na instância principal. Para obter mais detalhes, consulte [Manutenção do repositório](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. Start da instância principal.
1. Start o processo de espera na instância stand-by usando o mesmo bean JMX como descrito na primeira etapa.
1. Assista aos registros e aguarde a conclusão da sincronização. É possível que, neste momento, se verifique um crescimento substancial no repositório de espera.
1. Execute a `cleanup()` operação na instância stand-by, usando o mesmo bean JMX como descrito na primeira etapa.

Pode demorar mais do que o normal para que a instância stand-by conclua a sincronização com a compactação primária como off-line, reescrevendo efetivamente o histórico do repositório, fazendo com que o cálculo das alterações nos repositórios leve mais tempo. É também de notar que, quando esse processo for concluído, o tamanho do repositório no modo de espera será aproximadamente o mesmo tamanho do repositório no principal.

Como alternativa, o repositório principal pode ser copiado manualmente para o modo de espera após executar a compactação no principal, essencialmente reconstruindo o modo de espera sempre que a compactação for executada.

### Coleta de lixo do armazenamento de dados {#data-store-garbage-collection}

É importante executar a coleta de lixo em instâncias de armazenamento de dados de arquivos de vez em quando, caso contrário, os binários excluídos permanecerão no sistema de arquivos, eventualmente preenchendo a unidade. Para executar a coleta de lixo, siga o procedimento abaixo:

1. Execute a manutenção do repositório em modo de espera a frio, conforme descrito na seção [acima](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. Após a conclusão do processo de manutenção e a reinicialização das instâncias:

   * No principal, execute a coleta de lixo do armazenamento de dados por meio do bean JMX relevante, conforme descrito [neste artigo](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * No modo de espera, a coleta de lixo do armazenamento de dados está disponível somente por meio do MBean **BlobGarbageCollection** - `startBlobGC()`. O **RepositoryManagement **MBean não está disponível no modo de espera.

   >[!NOTE]
   >
   >Se você não estiver usando um armazenamento de dados compartilhado, a coleta de lixo terá que ser executada primeiro no primário e depois no modo de espera.

