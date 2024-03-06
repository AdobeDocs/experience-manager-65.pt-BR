---
title: Implantações recomendadas
description: Este artigo descreve as topologias recomendadas para AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: baec7fc8-d48c-4bc6-b12b-4bf4eff695ea
source-git-commit: 518207a0d8a95ef17b0972855a58f124fb215c85
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 0%

---

# Implantações recomendadas{#recommended-deployments}

>[!NOTE]
>
>Esta página se refere às topologias recomendadas para o AEM. Para obter mais informações sobre recursos de clustering e como configurá-los, consulte [Documentação da API Apache Sling Discovery](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html).

MicroKernels agem como gerenciadores de persistência a partir do AEM 6.2. Escolher um para atender às suas necessidades depende da finalidade da instância e do tipo de implantação que você está considerando.

Os exemplos abaixo são uma indicação de quais são os usos recomendados nas configurações mais comuns do AEM.

## Cenários de implantação {#deployment-scenarios}

### Instância única do TarMK {#single-tarmk-instance}

Nesse cenário, uma única instância TarMK é executada em um único servidor.

**Essa é a implantação padrão para instâncias de autor.**

![chlimage_1-15](assets/chlimage_1-15.png)

Vantagens:

* Simples
* Fácil manutenção
* Bom desempenho

As desvantagens:

* Não dimensionável além dos limites da capacidade do servidor
* Sem capacidade de failover

### Modo de espera a frio TarMK {#tarmk-cold-standby}

Uma instância TarMK atua como a instância primária. O repositório do principal é replicado em um sistema de failover de standby.

O mecanismo de standby inativo também pode ser usado como backup porque o repositório completo é replicado constantemente no servidor de failover. O servidor de failover está sendo executado no modo de espera inativo, o que significa que somente o HttpReceiver da instância está sendo executado.

![chlimage_1-16](assets/chlimage_1-16.png)

Vantagens:

* Simplicidade
* Capacidade de manutenção
* Desempenho
* Failover

As desvantagens:

* Não dimensionável além dos limites da capacidade do servidor
* Um servidor fica ocioso a maior parte do tempo
* O failover não é automático. Ele deve ser detectado externamente antes que o sistema de failover possa iniciar a veiculação de solicitações.

>[!NOTE]
>
>Para obter mais informações sobre como configurar o AEM com o TarMK Cold Standby, consulte [este](/help/sites-deploying/tarmk-cold-standby.md) artigo.

>[!NOTE]
>
>A implantação do Modo de espera desativado neste exemplo do TarMK requer que as instâncias principal e de espera sejam licenciadas separadamente, pois há replicação constante para o servidor de failover. Para obter mais informações sobre licenciamento, consulte o [Termos gerais de licenciamento do Adobe](https://www.adobe.com/legal/terms/enterprise-licensing.html).

### Farm TarMK {#tarmk-farm}

Várias instâncias do Oak são executadas com uma instância TarMK. Os repositórios TarMK são independentes e precisam ser mantidos em sincronia.

Manter os repositórios em sincronia é fornecido com o fato de que o servidor do autor está publicando o mesmo conteúdo para cada membro do farm. Para obter mais informações, consulte [Replicação](/help/sites-deploying/replication.md).

Para o AEM Communities, o conteúdo gerado pelo usuário (UGC) nunca é replicado. Para oferecer suporte a UGC em um farm TarMK, consulte [considerações para o AEM Communities](#considerations-for-aem-communities).

**Essa é a implantação padrão para ambientes de publicação.**

![chlimage_1-17](assets/chlimage_1-17.png)

Vantagens:

* Desempenho
* Escalabilidade para acesso de leitura
* Failover

### Oak Cluster com failover MongoMK para alta disponibilidade em um único data center {#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}

Essa abordagem implica que várias instâncias do Oak acessem um conjunto de réplicas do MongoDB em um único data center, criando, na verdade, um cluster ativo-ativo para o ambiente de autor do AEM. Os conjuntos de réplicas no MongoDB são usados para fornecer alta disponibilidade e redundância em caso de falha de hardware ou rede.

![chlimage_1-18](assets/chlimage_1-18.png)

Vantagens:

* Capacidade de dimensionar horizontalmente com novas instâncias de autor de AEM
* Alta disponibilidade, redundância e failover automatizado da camada de dados

As desvantagens:

* O desempenho pode ser menor do que com TarMK para alguns cenários

### Cluster Oak com failover MongoMK em vários data centers {#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

Essa abordagem implica que várias instâncias do Oak acessem um conjunto de réplicas do MongoDB em vários data centers, criando um cluster ativo-ativo para o ambiente de autor do AEM. Com vários data centers, a replicação MongoDB fornece a mesma alta disponibilidade e redundância, mas agora inclui a capacidade de lidar com uma interrupção no data center.

![oakclustermongofailover2datacenters](assets/oakclustermongofailover2datacenters.png)

Vantagens:

* Capacidade de dimensionar horizontalmente com novas instâncias de autor de AEM
* Alta disponibilidade, redundância e failover automatizado da camada de dados (incluindo paralisações do data center)

>[!NOTE]
>
>No diagrama acima, o Servidor AEM 3 e o Servidor AEM 4 são apresentados com um status de inativo supondo uma latência de rede entre os Servidores AEM no Data Center 2 e o nó primário MongoDB no Data Center 1 que é maior do que o requisito documentado [aqui](/help/sites-deploying/aem-with-mongodb.md#checklists). Se a latência máxima for compatível com os requisitos, por exemplo, por meio do uso de zonas de disponibilidade, os servidores AEM no Data Center 2 também poderão estar ativos, criando um cluster AEM ativo-ativo em vários data centers.

>[!NOTE]
>
>Para obter informações adicionais sobre os conceitos de arquitetura do MongoDB descritos nesta seção, consulte [Replicação do MongoDB](https://docs.mongodb.org/manual/replication/).

## Microkernels: qual usar {#microkernels-which-one-to-use}

A regra básica que precisa ser levada em conta ao escolher entre os dois micronúcleos disponíveis é que o TarMK é projetado para desempenho, enquanto o MongoMK é usado para escalabilidade.

Você pode usar essas matrizes de decisão para estabelecer qual é o melhor tipo de implantação adequado aos seus requisitos.

A Adobe recomenda que o TarMK seja a tecnologia de persistência padrão usada pelos clientes em todos os cenários de implantação, para as instâncias de Autor e Publicação do AEM, exceto nos casos de uso descritos abaixo.

### Exceções para escolher AEM MongoMK em vez de TarMK em instâncias de autor {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}

O principal motivo para escolher o back-end de persistência MongoMK em vez do TarMK é dimensionar as instâncias horizontalmente. Isso significa ter duas ou mais instâncias de autor ativas em execução o tempo todo e usar o MongoDB como o sistema de armazenamento de persistência. A necessidade de executar mais de uma instância de autor geralmente resulta do fato de que a capacidade da CPU e da memória de um único servidor, que suporta todas as atividades de criação simultâneas, não é mais sustentável.

É quase impossível prever qual será o modelo de simultaneidade exato depois que um novo site entrar em funcionamento. Portanto, o Adobe recomenda que você considere os seguintes critérios ao avaliar se deve usar MongoMK e dois ou mais nós ativos do Author:

1. Número de usuários nomeados conectados em um dia: milhares ou mais.
1. Número de usuários simultâneos: em centenas ou mais.
1. Volume de assimilações de ativos por dia: em centenas de milhares ou mais.
1. Volume de edições de página por dia: em centenas de milhares ou mais (incluindo atualizações automatizadas via Gerenciador de vários sites ou assimilações de feed de notícias, por exemplo).
1. Volume de pesquisas por dia: em dezenas de milhares ou mais.

>[!NOTE]
>
>O Dia Difícil pode ser usado para avaliar o desempenho do aplicativo do cliente no contexto da configuração de hardware implantada. Mais informações sobre esta ferramenta estão disponíveis [aqui](/help/sites-developing/tough-day.md).

Uma implantação mínima com MongoDB normalmente envolve a seguinte topologia:

* Um conjunto de réplicas MongoDB que consiste em um nó primário, dois nós secundários com cada uma das instâncias MongoDB em execução em uma zona de disponibilidade com uma latência abaixo de 15 milissegundos em cada nó;
* Um cluster de instâncias do autor com um nó líder, um nó não líder e ambos ativos o tempo todo, com cada uma das instâncias do autor em execução em cada um dos data centers, onde as instâncias primária e secundária do MongoDB estão em execução.

Além disso, é altamente recomendável configurar o armazenamento de dados em um sistema de arquivos compartilhado ou no Amazon S3, de modo que os ativos ou binários não sejam armazenados no MongoDB. Isso garantirá o desempenho ideal na implantação.

Um dos benefícios adicionais de implantar um conjunto de réplicas do MongoDB com um cluster de duas ou mais instâncias de autor é ter um cenário de recuperação automatizada com tempo de inatividade mínimo se houver instâncias de autor, réplica do MongoDB ou uma falha completa do data center. No entanto, a escolha de MongoMK em vez de TarMK não deve ser orientada exclusivamente pelo requisito de recuperação, já que o TarMK também pode fornecer uma solução de tempo de inatividade mínimo com um mecanismo de failover controlado.

Se os critérios acima não forem esperados durante os primeiros 18 meses da implantação, é recomendável primeiro implantar o AEM usando TarMK, reavaliar sua configuração posteriormente quando os critérios acima se aplicarem e, finalmente, determinar se deve permanecer no TarMK ou migrar para MongoMK.

### Exceções para escolher AEM MongoMK em vez de TarMK em instâncias de publicação {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}

Não é recomendável implantar o MongoMK para instâncias de publicação. O nível de publicação da implantação é quase sempre implantado como um farm de instâncias de publicação totalmente independentes que executam o TarMK, que são mantidas em sincronia ao replicar o conteúdo das instâncias de autor. Essa arquitetura de &quot;nada compartilhado&quot;, adequada às instâncias de publicação, permite que a implantação do nível de publicação seja dimensionada horizontalmente de forma linear. A topologia do farm também oferece o benefício de aplicar qualquer atualização ou atualização a instâncias de publicação continuamente, de modo que qualquer alteração no nível de publicação não exigirá tempo de inatividade.

Isso não se aplica ao AEM Communities que usa clusters MongoMK no nível de publicação sempre que houver mais de um editor. Se escolher o JSRP (consulte [Armazenamento de conteúdo da comunidade](/help/communities/working-with-srp.md)), então um cluster MongoMK seria apropriado, como qualquer cluster do lado da publicação, independentemente do MK escolhido, como MongoDB ou RDB.

### Pré-requisitos e Recommendations ao implantar AEM com MongoMK {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}

Um conjunto de pré-requisitos e recomendações está disponível se você estiver considerando uma implantação do MongoMK para AEM:

**Pré-requisitos obrigatórios para implantações do MongoDB:**

1. A arquitetura e o dimensionamento da implantação do MongoDB devem fazer parte da implementação do projeto com a ajuda da Adobe Consulting ou dos arquitetos do MongoDB familiarizados com o AEM;
1. A experiência do MongoDB deve estar presente no parceiro ou na equipe do cliente para ter confiança na capacidade de sustentar e manter um ambiente MongoDB existente ou novo;
1. Você pode optar por implantar a versão comercial ou de código aberto do MongoDB (AEM suporta ambos), mas deve comprar um contrato de Manutenção e Suporte do MongoDB diretamente da MongoDB Inc;
1. Em geral, as arquiteturas e infraestruturas do AEM e do MongoDB devem ser bem definidas e validadas por um Arquiteto do Adobe AEM;
1. Revise o modelo de suporte para implantações de AEM que incluem MongoDB.

**Recomendações fortes para implantações do MongoDB:**

* Consulte o MongoDB para Adobe Experience Manager [artigo](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager);
* Revise a produção do MongoDB [lista de verificação](https://docs.mongodb.org/manual/administration/production-checklist/);
* Participe de uma aula de certificação no MongoDB disponível online [aqui](https://university.mongodb.com/).

>[!NOTE]
>
>Para todas as perguntas adicionais sobre essas diretrizes, pré-requisitos e recomendações, entre em contato com o [Atendimento ao cliente Adobe](https://helpx.adobe.com/br/marketing-cloud/contact-support.html).

### Considerações para o AEM Communities {#considerations-for-aem-communities}

Para sites que planejam implantar [AEM Communities](/help/communities/overview.md), é recomendável [escolher uma implantação](/help/communities/working-with-srp.md#characteristicsofstorageoptions) otimizado para manipular o UGC publicado por membros da comunidade do ambiente de publicação.

Ao usar uma [armazenamento comum](/help/communities/working-with-srp.md), o UGC não precisa ser replicado entre as instâncias de autor e outras instâncias de publicação para obter uma visualização consistente do UGC.

Abaixo estão um conjunto de matrizes de decisão que podem ajudá-lo a escolher o melhor tipo de persistência para sua implantação:

#### Escolha do tipo de implantação para instâncias de autor {#choosing-the-deployment-type-for-author-instances}

![chlimage_1-19](assets/chlimage_1-19.png)

#### Escolha do tipo de implantação para instâncias de publicação {#choosing-the-deployment-type-for-publish-instances}

![chlimage_1-20](assets/chlimage_1-20.png)

>[!NOTE]
>
>MongoDB é um software de terceiros e não está incluído no pacote de licenciamento AEM. Para obter mais informações, consulte a [Política de licenciamento do MongoDB](https://www.mongodb.org/about/licensing/) página.
>
>Para aproveitar ao máximo a implantação do AEM, a Adobe recomenda licenciar a versão MongoDB Enterprise para se beneficiar de suporte profissional.
>
>A licença inclui um conjunto de réplicas padrão, que é composto por uma instância primária e duas secundárias que podem ser usadas para as implantações do autor ou de publicação.
>
>Caso deseje executar o Author e o Publish no MongoDB, duas licenças separadas precisam ser compradas.
>
>Para obter mais informações, consulte [Página do MongoDB para Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
