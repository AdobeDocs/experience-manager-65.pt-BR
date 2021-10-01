---
title: Como executar AEM com o TarMK Cold Standby
seo-title: How to Run AEM with TarMK Cold Standby
description: Saiba como criar, configurar e manter uma configuração do TarMK Cold Standby.
seo-description: Learn how to create, configure and maintain a TarMK Cold Standby setup.
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
feature: Configuring
exl-id: dadde3ee-d60c-4b87-9af0-a12697148161
source-git-commit: 687203bf418962877a63b2fe77d8bdd3791cd4d9
workflow-type: tm+mt
source-wordcount: '2733'
ht-degree: 0%

---

# Como executar AEM com o TarMK Cold Standby{#how-to-run-aem-with-tarmk-cold-standby}

## Introdução {#introduction}

A capacidade de Espera Fria do Tar Micro Kernel permite que uma ou mais instâncias de AEM standby se conectem a uma instância primária. O processo de sincronização é uma maneira única de significar que é feito somente das instâncias primárias às de standby.

A finalidade das instâncias em standby é garantir uma cópia dos dados em tempo real do repositório principal e garantir um switch rápido sem perda de dados caso o principal não esteja disponível por qualquer motivo.

O conteúdo é sincronizado linearmente entre as instâncias primárias e de standby, sem qualquer verificação de integridade de corrupção de arquivo ou repositório. Devido a esse design, as instâncias em standby são cópias exatas da instância principal e não podem ajudar a atenuar inconsistências em instâncias primárias.

>[!NOTE]
>
>O recurso Cold Standby serve para proteger cenários em que alta disponibilidade é necessária em instâncias **author**. Para situações em que alta disponibilidade é necessária em instâncias **publish** usando o Tar Micro Kernel, o Adobe recomenda usar um farm de publicação.
>
>Para obter informações sobre mais implantações disponíveis, consulte a página [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md) .

>[!NOTE]
>
>Quando a instância Standby é configurada ou derivada do nó Primary , ela só permite acesso aos dois consoles a seguir (para atividades relacionadas à administração):
>
>* CRXDE Lite
>* Console da Web OSGI

>
>Outros consoles não estão acessíveis.

## Como funciona {#how-it-works}

Na instância principal do AEM, uma porta TCP é aberta e está ouvindo mensagens recebidas. Atualmente, há dois tipos de mensagens que os escravos enviarão ao principal:

* uma mensagem solicitando a ID de segmento do cabeçalho atual
* uma mensagem solicitando dados de segmento com uma ID especificada

O standby solicita periodicamente a ID do segmento do cabeçalho atual do primário. Se o segmento for localmente desconhecido, ele será recuperado. Se já estiver presente, os segmentos são comparados e os segmentos referenciados também serão solicitados, se necessário.

>[!NOTE]
>
>As instâncias de standby não estão recebendo nenhum tipo de solicitação, pois estão sendo executadas no modo de somente sincronização. A única seção disponível em uma instância standby é o Console da Web, para facilitar a configuração de pacotes e serviços.

Uma implantação típica do TarMK Cold Standby:

![chlimage_1](assets/chlimage_1.png)

## Outras características {#other-characteristics}

### Robustez {#robustness}

O fluxo de dados foi projetado para detectar e lidar automaticamente com problemas relacionados à conexão e à rede. Todos os pacotes são empacotados com somas de verificação e assim que ocorrem problemas com a conexão ou pacotes danificados, os mecanismos de repetição são acionados.

#### Show {#performance}

Ativar o TarMK Cold Standby na instância primária quase não tem impacto mensurável no desempenho. O consumo adicional da CPU é muito baixo e o disco rígido extra e a E/S de rede não devem gerar problemas de desempenho.

No modo de espera, você pode esperar alto consumo de CPU durante o processo de sincronização. Devido ao fato de o procedimento não ser multisegmentado, ele não pode ser acelerado usando vários núcleos. Se nenhum dado for alterado ou transferido, não haverá atividade mensurável. A velocidade da conexão varia dependendo do hardware e do ambiente de rede, mas não depende do tamanho do repositório ou do uso do SSL. Lembre-se disso ao estimar o tempo necessário para uma sincronização inicial ou quando muitos dados foram alterados enquanto isso no nó principal.

#### Segurança {#security}

Supondo que todas as instâncias são executadas na mesma zona de segurança da intranet, o risco de violação de segurança é muito reduzido. No entanto, é possível adicionar uma camada de segurança adicional, permitindo conexões SSL entre os escravos e o principal. Isso reduz a possibilidade de os dados serem comprometidos por um homem no meio.

Além disso, você pode especificar as instâncias de standby que podem se conectar, restringindo o endereço IP das solicitações recebidas. Isso deve ajudar a garantir que ninguém na intranet possa copiar o repositório.

>[!NOTE]
>
>É recomendável adicionar um balanceador de carga entre o Dispatcher e os servidores que fazem parte da configuração do Coldy Standby. O balanceador de carga deve ser configurado para direcionar o tráfego do usuário somente para a instância **primary** para garantir a consistência e impedir que o conteúdo seja copiado na instância de standby por outros meios que não o mecanismo Cold Standby.

## Criação de uma configuração AEM TarMK Cold Standby {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>O PID para o armazenamento do nó de segmento e o serviço de armazenamento Standby foram alterados no AEM 6.3 em comparação às versões anteriores da seguinte maneira:
>
>* de org.apache.jackrabbit.oak.**plugins**.segment.standby.store.StandbyStoreService para org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* de org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService para org.apache.jackrabbit.oak.segment.SegmentNodeStoreService

>
>Certifique-se de fazer os ajustes de configuração necessários para refletir essa alteração.

Para criar uma configuração TarMK de standby frio, primeiro é necessário criar as instâncias de standby executando uma cópia do sistema de arquivos de toda a pasta de instalação do principal em um novo local. Em seguida, você pode iniciar cada instância com um modo de execução que especificará sua função ( `primary` ou `standby`).

Abaixo está o procedimento que precisa ser seguido para criar uma configuração com uma instância principal e uma standby:

1. Instalar AEM.

1. Desligue sua instância e copie sua pasta de instalação para o local onde a instância do standby frio será executada. Mesmo que sejam executadas a partir de máquinas diferentes, atribua a cada pasta um nome descritivo (como *aem-primary* ou *aem-standby*) para diferenciar as instâncias.
1. Vá para a pasta de instalação da instância primária e:

   1. Verifique e exclua quaisquer configurações OSGi anteriores que você possa ter em `aem-primary/crx-quickstart/install`

   1. Crie uma pasta chamada `install.primary` em `aem-primary/crx-quickstart/install`

   1. Crie as configurações necessárias para o armazenamento de nó preferido e o armazenamento de dados em `aem-primary/crx-quickstart/install/install.primary`
   1. Crie um arquivo chamado `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` no mesmo local e configure-o adequadamente. Para obter mais informações sobre as opções de configuração, consulte [Configuração](/help/sites-deploying/tarmk-cold-standby.md#configuration).

   1. Se estiver usando uma instância AEM TarMK com um armazenamento de dados externo, crie uma pasta chamada `crx3` em `aem-primary/crx-quickstart/install` chamada `crx3`

   1. Coloque o arquivo de configuração do armazenamento de dados na pasta `crx3`.

   Se, por exemplo, você estiver executando uma instância AEM TarMK com um File Data Store externo, será necessário esses arquivos de configuração:

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   Abaixo você encontrará configurações de amostra para a instância principal:

   **Exemplo de** **oforg.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **Exemplo de org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="primary"
   port=I"8023"
   ```

   **Exemplo de org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. Inicie o primário certificando-se de especificar o modo de execução principal:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Crie um novo Apache Sling Logging Logger para o pacote **org.apache.jackrabbit.oak.segment** . Defina o nível de log como &quot;Depuração&quot; e aponte a saída do log para um arquivo de log separado, como */logs/tarmk-coldstandby.log*. Para obter mais informações, consulte [Registro](/help/sites-deploying/configure-logging.md).
1. Vá para o local da instância **standby** e inicie-a executando o jar.
1. Crie a mesma configuração de log para o primário. Em seguida, pare a instância .
1. Em seguida, prepare a instância de standby. Você pode fazer isso executando as mesmas etapas da instância primária:

   1. Exclua todos os arquivos que você possa ter em `aem-standby/crx-quickstart/install`.
   1. Crie uma nova pasta chamada `install.standby` em `aem-standby/crx-quickstart/install`

   1. Crie dois arquivos de configuração chamados:

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   1. Crie uma nova pasta chamada `crx3` em `aem-standby/crx-quickstart/install`

   1. Crie a configuração do armazenamento de dados e coloque-a em `aem-standby/crx-quickstart/install/crx3`. Neste exemplo, o arquivo que você precisa criar é:

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
   1. Edite os arquivos e crie as configurações necessárias.

   Abaixo estão exemplos de arquivos de configuração para uma instância de standby típica:

   **Exemplo de org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **Exemplo de org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="standby"
   primary.host="127.0.0.1"
   port=I"8023"
   secure=B"false"
   interval=I"5"
   standby.autoclean=B"true"
   ```

   **Exemplo de org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. Inicie a instância **standby** usando o modo de execução standby:

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

O serviço também pode ser configurado por meio do Console da Web:

1. Ir para o Console da Web em: *https://serveraddress:serverport/system/console/configMgr*
1. Procurando um serviço chamado **Apache Jackrabbit Oak Segment Tar Cold Standby Service** e clique duas vezes nele para editar as configurações.
1. Salvar as configurações e reiniciar as instâncias para que as novas configurações tenham efeito.

>[!NOTE]
>
>Você pode verificar a função de uma instância a qualquer momento verificando a presença dos modos de execução **primary** ou **standby** no Console da Web das Configurações do Sling.
>
>Isso pode ser feito indo até *https://localhost:4502/system/console/status-slingsettings* e verificando a linha **&quot;Run Modes&quot;**.

## Primeira sincronização {#first-time-synchronization}

Depois que a preparação estiver concluída e o standby for iniciado pela primeira vez, haverá tráfego intenso de rede entre as instâncias, já que o standby chega ao primário. Você pode consultar os logs para observar o status da sincronização.

No standby *tarmk-coldstandby.log*, você verá entradas como estas:

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

No *error.log* do standby, você deverá ver uma entrada como esta:

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

No trecho de log acima, *10.20.30.40* é o endereço IP do primário.

No **primário** *tarmk-coldstandby.log*, você verá entradas como estas:

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

Nesse caso, o &quot;cliente&quot; mencionado no log é a instância **standby**.

Quando essas entradas deixarem de aparecer no log, você pode assumir com segurança que o processo de sincronização está concluído.

Embora as entradas acima mostrem que o mecanismo de sondagem está funcionando corretamente, muitas vezes é útil entender se há dados sendo sincronizados enquanto a pesquisa está ocorrendo. Para fazer isso, procure entradas como as seguintes:

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

Além disso, ao executar com um `FileDataStore` não compartilhado, mensagens como a seguir confirmarão que os arquivos binários estão sendo transmitidos corretamente:

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### Configuração {#configuration}

As seguintes configurações OSGi estão disponíveis para o serviço Cold Standby:

* **Persistir configuração:** se estiver ativada, essa configuração será armazenada no repositório em vez dos arquivos de configuração OSGi tradicionais. Recomenda-se manter essa configuração desativada nos sistemas de produção para que a configuração primária não seja retirada pelo standby.

* **Modo (`mode`):** essa opção escolherá o modo de execução da instância.

* **Porta (porta):** a porta a ser usada para comunicação. O padrão é `8023`.

* **Host principal (`primary.host`):**  - o host da instância principal. Esta configuração só é aplicável para o modo de espera.
* **Intervalo de sincronização (`interval`):**  - essa configuração determina o intervalo entre a solicitação de sincronização e é aplicável somente para a instância de standby.

* **Intervalos de IP permitidos (`primary.allowed-client-ip-ranges`):**  - os intervalos de IP dos quais o principal permitirá conexões.
* **Seguro (`secure`):** ative a criptografia SSL. Para usar essa configuração, ela deve estar ativada em todas as instâncias.
* **Tempo limite de leitura em standby (`standby.readtimeout`):** Tempo limite para solicitações emitidas da instância de standby em milissegundos. O valor padrão usado é 60000 (um minuto).

* **Limpeza automática em espera (`standby.autoclean`):** chame o método de limpeza se o tamanho da loja aumentar em um ciclo de sincronização.

>[!NOTE]
>
>É altamente recomendável que o repositório principal e o standby tenham IDs de repositório diferentes para torná-las separadamente identificáveis para serviços como Descarregamento.
>
>A melhor maneira de garantir que isso seja coberto é excluindo o arquivo *sling.id* no standby e reiniciando a instância.

## Procedimentos de failover {#failover-procedures}

Caso a instância primária falhe por qualquer motivo, você pode definir uma das instâncias de standby para assumir a função do primário alterando o modo de execução de início conforme detalhado abaixo:

>[!NOTE]
>
>Os arquivos de configuração também precisam ser modificados para que correspondam às configurações usadas para a instância primária.

1. Vá para o local onde a instância do standby está instalada e pare-a.

1. Caso tenha um balanceador de carga configurado com a configuração, você poderá remover o principal da configuração do balanceador de carga neste ponto.
1. Faça backup da pasta `crx-quickstart` da pasta de instalação do standby. Pode ser usado como ponto de partida ao configurar um novo standby.

1. Reinicie a instância usando o modo de execução `primary`:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Adicione o novo primário ao balanceador de carga.
1. Crie e inicie uma nova instância de standby. Para obter mais informações, consulte o procedimento acima em [Criação de uma Configuração do TarMK Cold Standby AEM](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## Aplicação de hotfixes a uma configuração do Cold Standby {#applying-hotfixes-to-a-cold-standby-setup}

A maneira recomendada de aplicar hotfixes a uma configuração de stanby frio é instalá-los na instância primária e cloná-los em uma nova instância de standby frio com os hotfixes instalados.

Você pode fazer isso seguindo as etapas descritas abaixo:

1. Pare o processo de sincronização na instância do standby frio indo para o Console JMX e usando o **org.apache.jackrabbit.oak: Status (&quot;Standby&quot;)**bean. Para obter mais informações sobre como fazer isso, consulte a seção em [Monitoring](#monitoring).
1. Pare a instância de espera fria.
1. Instale o hotfix na instância primária. Para obter mais detalhes sobre como instalar um hotfix, consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md).
1. Teste a instância para problemas após a instalação.
1. Remova a instância de standby frio excluindo a pasta de instalação.
1. Pare a instância primária e clone-a executando uma cópia do sistema de arquivos de toda a pasta de instalação no local do standby frio.
1. Reconfigure o clone recém-criado para atuar como uma instância de espera fria. Para obter detalhes adicionais, consulte [Criação de uma Configuração AEM TarMK Cold Standby.](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. Inicie as instâncias de standby primário e frio.

## Monitoramento {#monitoring}

O recurso expõe informações usando JMX ou MBeans. Fazendo isso, você pode inspecionar o estado atual do standby e o principal usando o [JMX console](/help/sites-administering/jmx-console.md). As informações podem ser encontradas em um MBean de `type org.apache.jackrabbit.oak:type="Standby"`nomeado `Status`.

**Espera**

Observando uma instância de standby, você exporá um nó. Normalmente, a ID é um UUID genérico.

Este nó tem cinco atributos somente leitura:

* `Running:` valor booleano indicando se o processo de sincronização está em execução ou não.

* `Mode:` Cliente: seguido pela UUID usada para identificar a instância. Observe que essa UUID será alterada sempre que a configuração for atualizada.

* `Status:` uma representação textual do estado atual (como  `running` ou  `stopped`).

* `FailedRequests:`o número de erros consecutivos.
* `SecondsSinceLastSuccess:` o número de segundos desde a última comunicação bem-sucedida com o servidor. Ele exibirá `-1` se nenhuma comunicação bem-sucedida tiver sido feita.

Há também três métodos faturáveis:

* `start():` inicia o processo de sincronização.
* `stop():` interrompe o processo de sincronização.
* `cleanup():` executa a operação de limpeza no modo de espera.

**Principal**

A observação do primário expõe algumas informações gerais por meio de um MBean cujo valor de ID é o número da porta que o serviço de standby TarMK está usando (8023 por padrão). A maioria dos métodos e atributos é igual ao modo de espera, mas alguns diferem:

* `Mode:` sempre mostrará o valor  `primary`.

Além disso, podem ser recuperadas informações para até 10 clientes (instâncias em standby) conectados ao principal. A ID do MBean é o UUID da instância. Não há métodos faturáveis para esses MBeans, mas alguns atributos muito úteis somente leitura:

* `Name:` a ID do cliente.
* `LastSeenTimestamp:` o carimbo de data e hora da última solicitação em uma representação textual.
* `LastRequest:` a última solicitação do cliente.
* `RemoteAddress:` o endereço IP do cliente.
* `RemotePort:` a porta que o cliente usou para a última solicitação.
* `TransferredSegments:` o número total de segmentos transferidos para este cliente.
* `TransferredSegmentBytes:`o número total de bytes transferidos para este cliente.

## Manutenção do Repositório Cold Standby {#cold-standby-repository-maintenance}

### Limpeza de revisão {#revision-clean}

>[!NOTE]
>
>Se você executar [Limpeza de Revisão Online](/help/sites-deploying/revision-cleanup.md) na instância primária, o procedimento manual apresentado abaixo não será necessário. Além disso, se estiver usando a Limpeza de Revisão Online, a operação `cleanup ()` na instância de standby será executada automaticamente.

>[!NOTE]
>
>Não execute a limpeza de revisão offline no modo de espera. Não é necessário e não reduzirá o tamanho do armazenamento de segmentos.

O Adobe recomenda executar a manutenção regularmente para evitar o crescimento excessivo do repositório ao longo do tempo. Para executar manualmente a manutenção do repositório de standby frio, siga as etapas abaixo:

1. Pare o processo de standby na instância de standby indo para o Console JMX e usando o **org.apache.jackrabbit.oak: Status (&quot;Standby&quot;)** Bean. Para obter mais informações sobre como fazer isso, consulte a seção acima em [Monitoring](/help/sites-deploying/tarmk-cold-standby.md#monitoring).

1. Pare a instância principal do AEM.
1. Execute a ferramenta de compactação oak na instância primária. Para obter mais detalhes, consulte [Manutenção do Repositório](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. Inicie a instância principal.
1. Inicie o processo de standby na instância de standby usando o mesmo Bean JMX descrito na primeira etapa.
1. Assista aos logs e aguarde a conclusão da sincronização. É possível que um crescimento substancial no repositório stand-by seja observado neste momento.
1. Execute a operação `cleanup()` na instância de standby, usando o mesmo bean JMX descrito na primeira etapa.

Pode demorar mais do que o normal para a instância standby concluir a sincronização com a compactação primária como offline efetivamente reescreve o histórico do repositório, fazendo com que o cálculo das alterações nos repositórios leve mais tempo. Além disso, é de notar que, uma vez concluído esse processo, o tamanho do repositório no standby será basicamente o mesmo tamanho do repositório no principal.

Como alternativa, o repositório principal pode ser copiado para o standby manualmente após executar a compactação no principal, essencialmente reconstruindo o standby sempre que a compactação for executada.

### Coleta de lixo do armazenamento de dados {#data-store-garbage-collection}

É importante executar a coleta de lixo nas instâncias do armazenamento de dados de arquivos de vez em quando, caso contrário, os binários excluídos permanecerão no sistema de arquivos, acabando por preencher a unidade. Para executar a coleta de lixo, siga o procedimento abaixo:

1. Execute a manutenção do repositório de standby frio conforme descrito na seção [acima](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. Após a conclusão do processo de manutenção e reinício das instâncias:

   * No principal, execute a coleta de lixo do armazenamento de dados por meio do bean JMX relevante, conforme descrito em [this article](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * No standby, a coleta de lixo do armazenamento de dados está disponível somente por meio do **BlobGarbageCollection** MBean - `startBlobGC()`. O **RepositoryManagement **MBean não está disponível no standby.

   >[!NOTE]
   >
   >Caso não esteja usando um armazenamento de dados compartilhado, a coleta de lixo terá que ser executada primeiro no primário e depois no standby.
