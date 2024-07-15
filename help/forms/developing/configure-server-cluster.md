---
title: Como configurar e solucionar problemas de um AEM Forms no cluster de servidores JEE
description: Saiba como configurar e solucionar problemas de um Forms Adobe Experience Manager (AEM) no cluster de servidores JEE.
exl-id: 230fc2f1-e6e5-4622-9950-dae9449ed3f6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '3945'
ht-degree: 0%

---

# Configuração e solução de problemas de um cluster de servidores AEM Forms no JEE {#configuring-troubleshooting-aem-forms-jee-server-cluster}

## Conhecimento de pré-requisito {#prerequisites}

Familiaridade com os servidores de aplicativos Adobe Experience Manager (AEM) Forms em JEE, JBoss®, WebSphere® e WebLogic, servidores de bancos de dados Red Hat® Linux®, SUSE® Linux®, Microsoft® Windows, IBM® AIX® ou Sun Solaris™, Oracle, servidores de bancos de dados IBM® DB2® ou SQL Server e ambientes da Web.

## Nível do usuário {#user-level}

Avançado 

Um AEM Forms no Cluster JEE é uma topologia projetada para permitir que o AEM Forms no JEE seja resiliente à falha de um cluster. Também permite que a topologia dimensione a capacidade do sistema além das capacidades de um único nó. Um cluster combina vários nós em um único sistema lógico que compartilha dados e permite que as transações abranjam vários nós em sua execução. Um cluster é a maneira mais geral de dimensionar o AEM Forms no JEE, na medida em que qualquer combinação de serviços que lidam com qualquer combinação de cargas de trabalho pode ser compatível. Um cluster AEM Forms no JEE não é necessariamente o melhor ajuste para todos os tipos de implantações e, uma arquitetura de balanceamento de carga de servidor sem cluster pode ser apropriada.

Este documento discute os requisitos específicos de configuração e as possíveis áreas de problema que você pode encontrar com um cluster do AEM Forms no JEE.

## O que há em um cluster? {#what-is-in-cluster}

Os nós de cluster do AEM Forms no JEE se comunicam entre si e compartilham informações para permitir que o cluster como um todo tenha um único estado consistente de configuração e aplicação. O compartilhamento de informações no cluster é feito de várias maneiras diferentes simultaneamente, usadas em contextos diferentes. Os métodos básicos de compartilhamento de informações estão ilustrados na Figura abaixo:

![Cluster do Servidor de Aplicativos](assets/application-server-cluster.jpg)

### Cluster do servidor de aplicativos {#application-server-cluster}

Um cluster do AEM Forms no JEE depende dos recursos de cluster subjacentes do servidor de aplicativos. Os clusters do servidor de aplicativos permitem que a configuração do cluster seja gerenciada como um todo e fornecem serviços de cluster de baixo nível, como Java™ Naming and Diretory Interface (JNDI), que permitem que os componentes de software se encontrem no cluster. A sofisticação dos serviços de cluster e as dependências técnicas subjacentes que o servidor de aplicativos possui dependem do servidor de aplicativos. O WebSphere® e o WebLogic têm recursos de gerenciamento sofisticados para clusters, enquanto o JBoss® tem uma abordagem básica.

### Cache do GemFire {#gemfire-cache}

O cache do GemFire é um mecanismo de cache distribuído implementado em cada nó de cluster. Os nós se encontram e criam um único cache lógico que é mantido coerente entre os nós. Os nós que se encontram unem-se para manter um único cache nocional mostrado como uma nuvem na Figura 1. Ao contrário do GDS e do banco de dados, o cache é uma entidade puramente fictícia. O conteúdo real em cache é armazenado na memória e no diretório `LC_TEMP` em cada um dos nós de cluster.

### Banco de dados {#database}

O banco de dados AEM Forms no JEE - que é acessado por meio das fontes de dados JDBC IDP_DS, EDC_DS e outros - é compartilhado por todos os nós do cluster. A maioria dos dados persistentes sobre o estado do AEM Forms no JEE, como quais transações estão em andamento, os dados do usuário associados às transações em andamento e os dados sobre como as configurações do sistema foram definidas, estão neste banco de dados.

### Armazenamento global de documentos {#global-document-storage}

O Armazenamento global de documentos (GDS) é uma área de armazenamento baseada em sistema de arquivos usada pelo Gerenciador de documentos (classe IDPDocument) no AEM Forms no JEE. O GDS armazena arquivos de vida curta e de vida longa que devem ser acessíveis a todos os nós do cluster.

### Outros itens {#other-items}

Além desses principais recursos compartilhados, há outros itens que têm um comportamento específico de cluster, como o Quartz. O Quartz é um subsistema do scheduler usado pelo AEM Forms no JEE e usa tabelas de banco de dados para manter seu conhecimento sobre o que foi agendado e quais atividades agendadas estão sendo executadas. O Quartz deve ser configurado de forma diferente para instalações e clusters de nó único, e ele segue as dicas de outros AEM Forms nas configurações do JEE.

## Problemas comuns de configuração {#common-configuration}

Uma das coisas mais frustrantes sobre a manutenção ou a solução de problemas de um AEM Forms em um cluster JEE é que não há um único local para procurar confirmar positivamente que o cluster está íntegro. Para confirmar que tudo está bem no cluster, é necessário fazer algumas investigações e análises, e há vários modos de falha para a operação do cluster, dependendo do que está errado com a configuração do cluster. A figura abaixo ilustra um cluster mal configurado no qual vários recursos compartilhados são compartilhados incorretamente.

![Cluster configurado incorretamente](assets/bad-configuration-cluster.png)

Entenda como a organização por clusters funciona e os tipos de coisas que você pode procurar e verificar em um cluster, mesmo que não pretenda executar o AEM Forms no JEE em um cluster. O motivo é que algumas partes do AEM Forms no JEE podem receber dicas sobre como operar em um cluster incorretamente e assumir o comportamento do cluster que você não espera.

Então, o que há de errado com a configuração de compartilhamento da Figura acima? As seções a seguir descrevem os problemas:

### (1) Configuração do cluster GemFire {#gemfire-cluster-configuration}

Várias coisas podem dar errado com o cache do Gemfire. Dois cenários típicos são:

* Os nós que devem ser capazes de encontrar um ao outro não podem fazer isso.

* Os nós clusterizados podem se encontrar e compartilhar um cache quando não deveriam.

Se você tiver nós que pretende agrupar, eles precisarão encontrar um ao outro na rede. Por padrão, eles fazem isso com mensagens UDP de multicast. Cada nó envia mensagens de transmissão anunciando que está presente e qualquer nó que receba essa mensagem começa a conversar com os outros nós encontrados. Esse tipo de método de autodescoberta é comum, e muitos tipos de software e appliances fazem isso.

Um problema comum com a descoberta automática é que as mensagens multicast podem ser filtradas pela rede. Isso pode ser parte de uma política de rede, devido a regras de firewall de software ou porque elas não podem rotear pela rede existente entre nós. Devido à dificuldade geral em fazer com que a descoberta automática de UDP funcione em redes complexas, é prática comum que as implantações de produção usem um método de descoberta alternativo: os localizadores de TCP. Uma discussão geral dos localizadores TCP pode ser encontrada nas referências.

**Como saber se estou usando localizadores ou UDP?**

As seguintes propriedades da JVM controlam o método que o cache do GemFire usa para localizar outros nós.

Configurações de multicast:

* `adobe.cache.multicast-port`: A porta multicast usada para se comunicar com outros membros do sistema distribuído. Se for definido como zero, o multicast será desabilitado para descoberta e distribuição de membros.

* `gemfire.mcast-address` (opcional): substitui o endereço IP padrão usado pelo Gemfire.

Configurações do Localizador de TCP:

* `adobe.cache.cluster-locators`: O endereço IP/nome de host do localizador TCP e a porta do localizador TCP para todos os localizadores usados por membros do sistema para comunicação com localizadores em execução.

A lista deve incluir todos os localizadores em uso e deve ser configurada de forma consistente para cada membro do sistema de cluster.

Se a lista do TCP Locator estiver vazia, os localizadores não são usados e o método de multicast é usado.

**Como posso verificar se meu localizador TCP está em execução?**

Primeiro, se os localizadores TCP estiverem em uso, você deverá listar seus localizadores TCP na seguinte propriedade JVM em todos os nós do cluster:

`-Dadobe.cache.cluster-locators=aix01.adobe.com[22345],aix02.adobe.com[22345]`

Não é necessário executar os localizadores no AEM Forms em nós de cluster JEE. Eles podem ser executados em outros sistemas separados do cluster, se desejado. Mais de um sistema pode executar endereços. Além disso, considera-se prática recomendada ter localizadores em execução em dois locais em comparação com a possibilidade de que uma única falha dos localizadores possa causar um problema com a reinicialização do cluster. Em cada um dos sistemas que executam localizadores, você deve poder verificar se eles estão sendo executados usando os seguintes comandos nesses computadores:

`netstat -an | grep 22345`

A resposta esperada deve ser esta:

`tcp 0 0 *.22345 *.* LISTEN`

Outro comando de verificação é este:

`ps -ef | grep gemfire`

A resposta esperada deve ser semelhante a:

`livecycl 331984 1 0 10:14:51 pts/0 0:03 java -cp ./gemfire.jar: -Dgemfire.license-type=production -Dlocators=localhost[22345] com.gemstone.gemfire.distributed.Locator 22345`

**Como vejo quais nós o GemFire acha que estão no cluster?**

O GemFire produz informações de registro que podem ser usadas para diagnosticar quais membros do cluster foram encontrados e adotados pelo cache do GemFire. Isso pode ser usado para verificar se todos os membros de cluster corretos foram encontrados e se nenhuma descoberta de nó de cluster extra ou incorreta está acontecendo. O arquivo de log do GemFire está no diretório temporário configurado do AEM Forms no JEE:

`.../LC_TEMP/adobeZZ__123456/Caching/Gemfire.log`

A sequência numérica após `adobeZZ_` é exclusiva ao nó do servidor e, portanto, você deve pesquisar o conteúdo real do diretório temporário. Os dois caracteres após `adobe` dependem do tipo de servidor de aplicativo: `wl`, `jb` ou `ws`.

Os seguintes logs de amostra mostram o que acontece quando um cluster de dois nós se encontra.

No primeiro nó, AP-HP8:

```xml
[config 2011/08/05 09:28:09.143 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] This member, ap-hp8(4268):18763, is becoming group coordinator.
[info 2011/08/05 09:28:09.151 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Entered into membership in group GF6.5.1.17 with ID ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.152 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Starting DistributionManager ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449]
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:09.154 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] ap-hp8(4268)<v0>:18763/56449 is the elder and the only member.
[info 2011/08/05 09:28:09.163 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Did not hear back from any other system. I am the first one.
[info 2011/08/05 09:28:09.164 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] DistributionManager ap-hp8(4268)<v0>:18763/56449 started on 239.192.81.1[33456]. There were 0 other DMs. others: []
[info 2011/08/05 09:28:20.841 EDT GemfireCacheAdapter <Pooled Message Processor 1> tid=0xc4] New administration member detected at ap-hp7(2821)<v1>:19498/59136.
```

No outro nó, AP-HP7:

```xml
[info 2011/08/05 09:28:09.830 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Attempting to join distributed system whose membership coordinator is ap-hp8(4268)<v0>:18763 using membership ID ap-hp7(2821):19498
[info 2011/08/05 09:28:10.058 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Entered into membership in group GF6.5.1.17 with ID ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.059 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Starting DistributionManager ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449, ap-hp7(2821)<v1>:19498/59136]
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp7(2821)<v1>:19498/59136>. Now there are 2 non-admin member(s).
[info 2011/08/05 09:28:10.128 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] DistributionManager ap-hp7(2821)<v1>:19498/59136 started on 239.192.81.1[33456]. There were 1 other DMs. others: [ap-hp8(4268)<v0>:18763/56449]
```

**E se o GemFire estiver localizando nós que não deveria?**

Cada cluster distinto que compartilha uma rede corporativa deve usar um conjunto separado de localizadores TCP, se os localizadores TCP forem usados, ou um número de porta UDP separado, se a configuração UDP de multicast for usada. Como a descoberta automática de UDP é a configuração padrão para o AEM Forms no JEE e a mesma porta padrão 33456 está em uso por vários clusters, é possível que os clusters que não devem estar tentando se comunicar possam estar fazendo isso inesperadamente. Por exemplo, os clusters de produção e controle de qualidade devem permanecer separados, mas podem se conectar entre si por meio de multicast de UDP.

A situação mais comum quando você pode descobrir portas duplicadas em uma rede para a qual o GemFire está criando clusters incorretamente é durante o Bootstrap de um cluster. O que você pode descobrir é que o processo de Bootstrap falha sem uma causa clara. Normalmente, erros como esse são vistos:

```xml
Caused by: com.ibm.ejs.container.UnknownLocalException: nested exception is: com.adobe.pof.schema.ObjectTypeNotFoundException: Object Type: dsc.sc_service_configuration not found.
                at com.adobe.pof.schema.POFDefaultDomain.getObjectType(POFDefaultDomain.java:93)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.serviceConfigAuditAttributeExists(DSCInitializerBean.java:225)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.installSchema(DSCInitializerBean.java:186)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.bootstrap(DSCInitializerBean.java:94)
                at com.adobe.idp.dsc.initializer.EJSLocalStatelessDSCInitializerBeanLocalEJB_7bb34e85.bootstrap(Unknown Source)
                at com.adobe.livecycle.bootstrap.bootstrappers.DSCBootstrapper.bootstrap(DSCBootstrapper.java:68)
```

Nesse caso, o bootstrapper está trabalhando com o GemFire para acessar as tabelas necessárias. E há uma inconsistência entre as tabelas acessadas pelo JDBC e as informações da tabela em cache retornadas pelo GemFire, que vem de um cluster diferente com um banco de dados subjacente diferente.

Embora uma porta duplicada se torne evidente durante o Bootstrap, é possível que essa situação seja exibida posteriormente. Isso pode ocorrer quando um cluster é reiniciado após ser desativado quando o Bootstrap do outro cluster ocorreu. Ou, quando a configuração da rede for alterada para tornar visíveis entre si os clusters que estavam isolados anteriormente, para fins de multicast.

Para diagnosticar essas situações, examine os logs do GemFire e considere cuidadosamente se apenas os nós esperados estão sendo encontrados. Para corrigir o problema, é necessário alterar a propriedade `adobe.cache.multicast-port` para um valor diferente em um ou ambos os clusters.

### 2) Partilha de GDS {#gds-sharing}

O compartilhamento de GDS é configurado fora do AEM Forms no próprio JEE, no nível do S/O, onde você deve organizar para que a mesma estrutura de diretório compartilhado esteja disponível para todos os nós de cluster. Em sistemas do tipo Windows, isso é realizado configurando um compartilhamento de arquivos de um nó para o outro ou de um sistema de arquivos remoto, como um dispositivo NAS, para todos os nós. Em sistemas UNIX®, o compartilhamento GDS normalmente é realizado por meio de compartilhamento de arquivos NFS, novamente, de um nó para o outro ou de um dispositivo NAS.

Um possível modo de falha para o cluster é se este compartilhamento de arquivos remoto se tornar indisponível ou tiver problemas sutis. A montagem remota pode falhar devido a problemas de rede, configurações de segurança ou configuração incorreta. Uma reinicialização do sistema pode fazer com que as alterações de configuração feitas dias ou semanas antes entrem em vigor e isso pode causar surpresas.

**O que aconteceria se um compartilhamento NFS falhasse na montagem?**

No UNIX®, a maneira como as montagens do NFS são mapeadas para a estrutura de diretório pode permitir que um diretório GDS aparentemente utilizável esteja disponível, mesmo que a montagem falhe. Considere:

* Servidor NAS: pasta compartilhada NFS /u01/iapply/livecycle_gds
* Nó 1: um ponto de montagem para a pasta compartilhada (hospedada no servidor do banco de dados) localizada aqui: /u01/iapply/livecycle_gds
* Nó 2: um ponto de montagem para a pasta compartilhada (hospedada no servidor do banco de dados) localizada aqui: /u01/iapply/livecycle_gds

* LCES especifica o caminho para GDS: /u01/iapply/livecycle_gds

Se a montagem no Nó 1 falhar, a estrutura de diretório ainda conterá um caminho `/u01/iapply/livecycle_gds` para o ponto de montagem vazio e o nó parecerá estar sendo executado corretamente. Mas como o conteúdo do GDS não está sendo compartilhado com o outro nó, o cluster não funciona corretamente. Isso pode e acontece, e o resultado é que o cluster falha de maneiras misteriosas.

A prática recomendada é organizar as coisas para que o ponto de montagem do Linux® não seja usado como a raiz do GDS, mas, em vez disso, algum diretório dentro dele seja usado como a raiz do GDS:

* Se você tiver um servidor NFS, ele poderá ter um diretório: /some/storage/lc_cluster_dev/LC_GDS
* E no nó do cluster você tem um ponto de montagem: /u01/iapply/shared
* Montar nfs_server: /some/storage/lc_cluster_dev/u01/iapply/shared
* Aponte seu GDS para /u01/iapply/shared/LC_GDS

Agora, se por algum motivo a montagem não for bem-sucedida, o ponto de montagem simples não conterá um diretório LC_GDS e seu cluster falhará previsivelmente porque não consegue encontrar nenhum GDS.

**Como posso verificar se todos os nós veem o mesmo GDS e têm permissões?**

A verificação do acesso e compartilhamento de GDS é melhor feita acessando cada um dos nós como um usuário interativo. Você pode fazer isso por meio de SSH ou telnet para nós UNIX®, ou por meio de área de trabalho remota para sistemas Windows. Você deve ser capaz de navegar até o diretório GDS ou sistema de arquivos configurado em cada nó e criar arquivos de teste a partir de cada nó que esteja visível em todos os outros nós.

Preste atenção à ID de usuário com a qual o AEM Forms no JEE opera. Em instalações prontas para uso do Windows, isso é feito como administrador local. No UNIX®, pode ser um usuário de serviço específico configurado no script de inicialização ou na configuração do servidor de aplicativos. É importante que essa ID de usuário possa criar e manipular arquivos GDS igualmente em todos os nós.

Em sistemas UNIX®, as configurações de NFS geralmente assumem como padrão a desconfiança da propriedade raiz ou dos direitos de acesso raiz a arquivos e objetos. Se você estiver executando o servidor de aplicativos como o usuário raiz, poderá descobrir que deve especificar opções no servidor NFS, no nó que está montando os arquivos ou em ambos. Isso permite acesso bilateral e controle de arquivos criados por um nó e acessados por outro.

### (3) Partilha de bases de dados {#database-sharing}

Para que um cluster funcione corretamente, o mesmo banco de dados deve ser compartilhado por todos os membros do cluster. A possibilidade de cometer esse erro é aproximadamente:

* definir acidentalmente o IDP_DS, EDC_DS, AdobeDefaultSA_DS ou outras fontes de dados necessárias de forma diferente em nós de cluster separados, para que os nós apontem para bancos de dados diferentes.
* configuração acidental de vários nós separados para compartilhar um banco de dados quando não deveriam.

Dependendo do servidor de aplicações, pode ser natural que a conexão JDBC seja definida em um escopo de cluster, de modo que definições diferentes não sejam possíveis em nós diferentes. No JBoss®, no entanto, é totalmente possível configurar para que uma fonte de dados, como IDP_DS, aponte para um banco de dados no nó 1, mas aponte para algo mais no nó 2.

O problema inverso é mais comum. Ou seja, uma situação em que vários nós independentes (ou de cluster) do AEM Forms no JEE apontam acidentalmente para o mesmo esquema quando não é a intenção. Isso acontece com mais frequência quando um DBA fornece, sem saber, uma única AEM Forms nas informações de conexão do banco de dados JEE para as equipes de configuração de DEV e QA. Nenhuma das equipes percebe que as instâncias de DEV e QA exigem bancos de dados separados.

## Cluster do servidor de aplicativos {#application-server-cluster-1}

Para que um AEM Forms no cluster JEE seja bem-sucedido, o servidor de aplicativos deve ser configurado e operar corretamente como um cluster. No WebSphere® e no WebLogic, esse é um processo simples e bem documentado. No JBoss®, a configuração de cluster é um pouco mais prática, e garantir que os nós estejam configurados para atuar como um cluster e realmente encontrem e se comuniquem entre si pode ser um desafio. O JBoss® depende internamente do JGroups, que usa multicast UDP para localizar e coordenar com nós de correspondentes. Alguns dos problemas mencionados com o GemFire podem ocorrer, como nós que não conseguem encontrar um ao outro quando deveriam, ou encontrar um ao outro quando não deveriam.

Referências:

* [Serviços empresariais de alta disponibilidade por meio de clusters JBoss®](https://docs.jboss.org/jbossas/jboss4guide/r4/html/cluster.chapt.html)

* [Oracle WebLogic Server-Uso de clusters](https://docs.oracle.com/cd/E12840_01/wls/docs103/pdf/cluster.pdf)

### Como verifico se o JBoss® está sendo agrupado corretamente? {#check-jboss-clustering}

Quando o JBoss® é inicializado, à medida que os membros do cluster são descobertos, as mensagens de nível INFO sobre o nó que está ingressando no cluster são registradas no arquivo/console de log.

Se um nome de cluster tiver sido especificado por meio da opção de linha de comando -g na execução, você verá mensagens semelhantes às seguintes:

```xml
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster)
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster-HAPartitionCache)
and ones like:

[org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Number of cluster members: 1
2011-07-14 11:34:03,072 INFO  [org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Other members: 0
2011-07-14 11:34:03,138 INFO  [org.jboss.cache.RPCManagerImpl] (main) Received new cluster view: [10.36.34.44:55200|0] [10.36.34.44:55200]
2011-07-14 11:34:03,139 INFO  [org.jboss.cache.RPCManagerImpl] (main) Cache local address is 10.36.34.44:55200
```

### Quartz scheduler {#quartz-scheduler}

Geralmente, o uso do Quartz scheduler interno do AEM Forms no JEE em um cluster deve seguir automaticamente a configuração global do cluster do AEM Forms no JEE em geral. Há, no entanto, um bug, #2794033, que faz com que a configuração automática de cluster do Quartz falhe se os localizadores TCP estiverem sendo usados para Gemfire em vez de autodescoberta de multicast. Nesse caso, o Quartz é executado incorretamente em um modo não clusterizado. Isso cria bloqueios e corrupção de dados nas tabelas do Quartz. Os efeitos colaterais são piores na versão 8.2.x do que 9.0, pois o quartzo não é usado tanto, mas ainda está lá.

As correções estão disponíveis para este problema: 8.2.1.2 QF2.143 e 9.0.0.2 QF2.44.

Também há uma solução alternativa, que é definir essas duas propriedades:

* `-Dadobe.cache.cluster.locators=xxx`

* `-Dadobe.cache.cluster-locators=xxx`

Uma configuração usa um ponto entre &quot;cluster&quot; e &quot;localizadores&quot; e a outra usa um hífen. Isso é fácil de implementar e menos arriscado do que aplicar um patch de software, mas envolve criar artificialmente uma configuração adicional e confusa.

### Como verificar se o Quartz está sendo executado como um único nó ou cluster? {#check-quartz}

Para determinar como o Quartz se configurou, você deve observar as mensagens geradas pelo serviço AEM Forms no JEE Scheduler durante a inicialização. Essas mensagens são geradas na severidade INFO e pode ser necessário ajustar o nível de log e reiniciar para obter as mensagens. Na sequência de inicialização do AEM Forms no JEE, a inicialização do quartzo começa com a seguinte linha:

INFO `[com.adobe.idp.scheduler.SchedulerServiceImpl]` IDPSchedulerService onLoad
É importante localizar essa primeira linha nos logs. O motivo é que alguns servidores de aplicativos também usam o Quartz, e suas instâncias do Quartz não devem ser confundidas com as instâncias que estão sendo usadas pelo serviço AEM Forms no JEE Scheduler. Esta é a indicação de que o serviço Scheduler está sendo iniciado e as linhas que o seguem informam se ele está sendo iniciado no modo clusterizado adequadamente. Várias mensagens são exibidas nessa sequência, e essa é a última mensagem &quot;iniciada&quot; que revela como o Quartz é configurado:

Aqui o nome da instância Quartz é fornecido: `IDPSchedulerService_$_ap-hp8.ottperflab.adobe.com1312883903975`. O nome da instância Quartz do agendador sempre começa com a cadeia de caracteres `IDPSchedulerService_$_`. A string anexada ao final deste informa se o Quartz está sendo executado no modo agrupado. O identificador exclusivo longo gerado pelo nome do host do nó e uma longa cadeia de dígitos, aqui `ap-hp8.ottperflab.adobe.com1312883903975`, indica que ele está operando em um cluster. Se estiver operando como um único nó, o identificador será um número de dois dígitos, &quot;20&quot;:

INFORMAÇÃO `[org.quartz.core.QuartzScheduler]` Agendador `IDPSchedulerService_$_20` iniciado.
Essa verificação deve ser feita em todos os nós de cluster separadamente, pois o programador de cada nó determina independentemente se operará no modo de cluster.

### Que tipos de problemas ocorrem se o Quartz estiver sendo executado no modo errado? {#quartz-running-in-wrong-mode}

Se o Quartz estiver configurado para ser executado como um único nó, mas o estiver sendo executado em um cluster e compartilhando tabelas de banco de dados do Quartz com outros nós, isso resultará na operação não confiável do AEM Forms no serviço do Agendador do JEE. E é frequentemente acompanhada por impasses no banco de dados. Este é um rastreamento de pilha bastante típico que você pode ver nesta situação:

```xml
[1/20/11 10:40:57:584 EST] 00000035 ErrorLogger   E org.quartz.core.ErrorLogger schedulerError An error occured while marking executed job complete. job= 'Asynchronous.TaskFormDataSaved:12955380518320.5650479324757354'
 org.quartz.JobPersistenceException: Could not remove trigger: ORA-00060: deadlock detected while waiting for resource  [See nested exception: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource ]
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.removeTrigger(JobStoreSupport.java:1405)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2888)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$38.execute(JobStoreSupport.java:2872)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$40.execute(JobStoreSupport.java:3628)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3662)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3624)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2868)
        at org.quartz.core.QuartzScheduler.notifyJobStoreJobComplete(QuartzScheduler.java:1698)
        at org.quartz.core.JobRunShell.run(JobRunShell.java:273)
        at org.quartz.simpl.SimpleThreadPool$WorkerThread.run(SimpleThreadPool.java:529)
Caused by: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource
```

### Como sincronizo os relógios do sistema em um cluster? {#synchronize-system-clocks-cluster}

Para que um cluster funcione sem problemas, os relógios em todos os nós do cluster devem ser sincronizados. Isso não pode ser feito adequadamente à mão e tem de ser feito por alguma forma de serviço de sincronização de tempo que é executado regularmente. Os relógios em todos os nós devem estar dentro de um segundo um do outro. A prática recomendada determina que não apenas os nós do cluster, mas também o balanceador de carga, o servidor de banco de dados, o servidor GDS NAS e quaisquer outros componentes sejam sincronizados.

A sincronização de horário do Windows tende a ser com o controlador de domínio. Os sistemas UNIX® podem sincronizar usando NTP para uma origem de tempo diferente. É melhor se todos os sistemas — tanto o AEM Forms em nós JEE quanto outros componentes do sistema — forem sincronizados com a mesma origem, se possível.

Não é suficiente, mesmo nos ambientes de teste mais temporários, definir manualmente os relógios nos nós. Ajustar manualmente os relógios não dá sincronização precisa suficiente, e os relógios nos dois nós inevitavelmente se desviam um em relação ao outro, mesmo durante um período de apenas um dia. Um mecanismo de sincronização de tempo ativo é essencial para uma operação de cluster confiável.

### Balanceador de carga {#load-balancer}

Um requisito típico de um cluster que fornece serviços interativos ao usuário é um balanceador de carga HTTP que distribui solicitações HTTP pelo cluster. O uso bem-sucedido de um balanceador de carga com um AEM Forms no cluster JEE requer a configuração do seguinte:

* adesão à sessão

* Regras de regravação de URL

* verificação de integridade do nó

### O que devo fazer sobre a minha função de verificação de integridade do balanceador de carga? {#load-balancer-health-check}

Alguns balanceadores de carga podem ser configurados para executar uma verificação de integridade periódica nos nós que estão sendo balanceados. Normalmente, esse é um URL para uma função de aplicativo que o balanceador de carga tenta acessar. Se a carga tiver êxito, o nó será considerado íntegro e será mantido no conjunto de balanceamento de carga. Se o URL falhar ao carregar, o nó será considerado com falha e será eliminado do conjunto. Geralmente, o URL de verificação de integridade é conectado à página de logon da AEM Forms no JEE AdminUI. Esta não é uma verificação de integridade ideal para um membro de cluster e seria melhor implementar um processo de curta duração e usar o URL da API REST como a função de verificação de integridade.

## Caminho de arquivo temporário e configurações de cluster semelhantes {#temporary-file-path-cluster-settings}

Determinadas configurações de caminho de arquivo no AEM Forms no JEE são estabelecidas em todo o cluster e têm a mesma configuração efetiva em cada nó, mas são interpretadas independentemente em cada nó para fazer referência a arquivos locais. As principais são as configurações de caminho de fonte e as configurações de diretório temporárias. Acesse a tela Configurações principais da interface do administrador (Início > Configurações > Sistema principal > Configurações principais)

As seguintes configurações devem ser verificadas:

1. Localização do diretório temporário
1. Localização do diretório Adobe Server Fonts
1. Localização do diretório de fontes do cliente
1. Localização do diretório de Fontes do Sistema
1. Localização do arquivo de configuração dos serviços de dados

O cluster tem apenas uma única definição de caminho para cada uma dessas definições de configuração. Por exemplo, o local do diretório Temp pode ser `/home/project/QA2/LC_TEMP`. Em um cluster, é necessário que cada nó realmente tenha esse caminho específico acessível. Se um nó tiver o caminho de arquivo temporário esperado e outro nó não tiver, o nó que não tiver, funcionará incorretamente.

Embora esses arquivos e caminhos possam ser compartilhados entre os nós ou localizados separadamente, ou em sistemas de arquivos remotos, é prática recomendada que eles sejam cópias locais no armazenamento em disco do nó local.

O caminho do Diretório temporário, em particular, não deve ser compartilhado entre os nós. Um procedimento semelhante ao descrito para verificar se o GDS deve ser usado para verificar se o diretório temporário não está sendo compartilhado. Vá para cada nó, crie um arquivo temporário no caminho indicado pela configuração de caminho e verifique se os outros nós não compartilham o arquivo. O caminho do diretório temporário deve se referir ao armazenamento em disco local em cada nó, se possível, e deve ser verificado.

Para cada uma das configurações de caminho, verifique se o caminho realmente existe e está acessível de cada nó no cluster, usando a identidade de uso eficaz sob a qual o AEM Forms no JEE é executado. O conteúdo do diretório de fontes deve ser legível. O diretório temporário deve permitir leitura, gravação e controle.
