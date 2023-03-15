---
title: Diretrizes de desempenho
seo-title: Performance Guidelines
description: Este artigo fornece diretrizes gerais sobre como otimizar o desempenho da implantação do AEM.
seo-description: This article provides general guidelines on how to optimize the performance of your AEM deployment.
uuid: 38cf8044-9ff9-48df-a843-43f74b0c0133
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 9ccbc39e-aea7-455e-8639-9193abc1552f
feature: Configuring
exl-id: 5a305a5b-0c3d-413b-88c1-1f5abf7e1579
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2976'
ht-degree: 6%

---

# Diretrizes de desempenho{#performance-guidelines}

Esta página fornece diretrizes gerais sobre como otimizar o desempenho da implantação do AEM. Se você não AEM, passe o mouse sobre as seguintes páginas antes de começar a ler as diretrizes de desempenho:

* [AEM conceitos básicos](/help/sites-deploying/deploy.md#basic-concepts)
* [Visão geral do armazenamento em AEM](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)

Ilustradas abaixo estão as opções de implantação disponíveis para AEM (rolar para exibir todas as opções):

<table>
 <tbody>
  <tr>
   <td><p><strong>AEM</strong></p> <p><strong>Produto</strong></p> </td>
   <td><p><strong>Topologia</strong></p> </td>
   <td><p><strong>Sistema Operacional</strong></p> </td>
   <td><p><strong>Servidor de aplicativos</strong></p> </td>
   <td><p><strong>JRE</strong></p> </td>
   <td><p><strong>Segurança</strong></p> </td>
   <td><p><strong>Micro kernel</strong></p> </td>
   <td><p><strong>Armazenamento de dados</strong></p> </td>
   <td><p><strong>Indexação</strong></p> </td>
   <td><p><strong>Servidor Web</strong></p> </td>
   <td><p><strong>Navegador</strong></p> </td>
   <td><p><strong>Marketing Cloud</strong></p> </td>
  </tr>
  <tr>
   <td><p>Sites</p> </td>
   <td><p>Não-HA</p> </td>
   <td><p>Windows</p> </td>
   <td><p>CQSE</p> </td>
   <td><p>Oracle</p> </td>
   <td><p>LDAP</p> </td>
   <td><p>Tar</p> </td>
   <td><p>Segmento</p> </td>
   <td><p>Propriedade</p> </td>
   <td><p>Apache</p> </td>
   <td><p>Edge</p> </td>
   <td><p>Destino</p> </td>
  </tr>
  <tr>
   <td><p>Assets</p> </td>
   <td><p>Publicar-HA</p> </td>
   <td><p>Solaris</p> </td>
   <td><p>WebLogic</p> </td>
   <td><p>IBM</p> </td>
   <td><p>SAML</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p>Arquivo</p> </td>
   <td><p>Lucene</p> </td>
   <td><p>IIS</p> </td>
   <td><p>IE</p> </td>
   <td><p>Analytics</p> </td>
  </tr>
  <tr>
   <td><p>Communities</p> </td>
   <td><p>Autor-CS</p> </td>
   <td><p>Chapéu Vermelho</p> </td>
   <td><p>WebSphere</p> </td>
   <td><p>HP</p> </td>
   <td><p>Oauth</p> </td>
   <td><p>RDB/Oracle</p> </td>
   <td><p>S3/Azure</p> </td>
   <td><p>Solr</p> </td>
   <td><p>iPlanet</p> </td>
   <td><p>FireFox</p> </td>
   <td><p>Campaign</p> </td>
  </tr>
  <tr>
   <td><p>Forms</p> </td>
   <td><p>Author-Offload</p> </td>
   <td><p>HP-UX</p> </td>
   <td><p>Tomcat</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/DB2</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Chrome</p> </td>
   <td><p>Social</p> </td>
  </tr>
  <tr>
   <td><p>Móvel</p> </td>
   <td><p>Cluster de Autores</p> </td>
   <td><p>IBM AIX</p> </td>
   <td><p>JBoss</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/MySQL</p> </td>
   <td><p>RDBMS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Safari</p> </td>
   <td><p>Público</p> </td>
  </tr>
  <tr>
   <td><p>Vários sites</p> </td>
   <td><p>ASRP</p> </td>
   <td><p>SUSE</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/SQLServer</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Assets</p> </td>
  </tr>
  <tr>
   <td><p>Commerce</p> </td>
   <td><p>MSRP</p> </td>
   <td><p>Apple OS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Ativação</p> </td>
  </tr>
  <tr>
   <td><p>Dynamic Media</p> </td>
   <td><p>JSRP</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Móvel</p> </td>
  </tr>
  <tr>
   <td><p>Brand Portal</p> </td>
   <td><p>J2E</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>AoD</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>LiveFyre</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Screens</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Segurança de documento</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Gerenciamento de processos</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Aplicativo de desktop do  </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>As diretrizes de desempenho se aplicam principalmente ao AEM Sites.

## Quando utilizar as diretrizes de desempenho {#when-to-use-the-performance-guidelines}

Você deve usar as diretrizes de desempenho nas seguintes situações:

* **Implantação pela primeira vez**: Ao planejar a implantação do AEM Sites ou do Assets pela primeira vez, é importante entender as opções disponíveis ao configurar o Micro Kernel, a Loja de nós e a Loja de dados (em comparação com as configurações padrão). Por exemplo, alterar as configurações padrão do Data Store para TarMK para File Data Store.
* **Atualização para uma nova versão**: Ao atualizar para uma nova versão, é importante entender as diferenças de desempenho em comparação ao ambiente em execução. Por exemplo, atualização do AEM 6.1 para 6.2 ou do AEM 6.0 CRX2 para 6.2 OAK.
* **O tempo de resposta é lento**: Quando a arquitetura do Nodestore selecionada não estiver atendendo aos seus requisitos, é importante compreender as diferenças de desempenho em comparação com outras opções de topologia. Por exemplo, implantar o TarMK em vez do MongoMK ou usar um File Data Store em vez de um Amazon S3 ou Microsoft Azure Data Store.
* **Adicionar mais autores**: Quando a topologia TarMK recomendada não atende aos requisitos de desempenho e o redimensionamento do nó Autor atingiu a capacidade máxima disponível, é importante entender as diferenças de desempenho em comparação ao uso do MongoMK com três ou mais nós Autor. Por exemplo, implantar MongoMK em vez de TarMK.
* **Adicionar mais conteúdo**: Quando a arquitetura recomendada do Data Store não atender aos seus requisitos, é importante compreender as diferenças de desempenho em comparação com outras opções do Data Store. Exemplo: usando o Amazon S3 ou o Microsoft Azure Data Store em vez de um File Data Store.

## Introdução {#introduction}

Este capítulo fornece uma visão geral da arquitetura de AEM e seus componentes mais importantes. Ele também fornece diretrizes de desenvolvimento e descreve os cenários de teste usados nos testes de benchmark TarMK e MongoMK.

### A plataforma AEM {#the-aem-platform}

A plataforma de AEM consiste nos seguintes componentes:

![chlimage_1](assets/chlimage_1a.png)

Para obter mais informações sobre a plataforma de AEM, consulte [O que é AEM](/help/sites-deploying/deploy.md#what-is-aem).

### A arquitetura AEM {#the-aem-architecture}

Há três blocos fundamentais importantes para uma implantação de AEM. O **Instância do autor** , que é usada por autores, editores e aprovadores de conteúdo para criar e revisar conteúdo. Quando o conteúdo é aprovado, ele é publicado em um segundo tipo de instância chamado de **Instância de publicação** de onde é acessado pelos usuários finais. O terceiro bloco de construção é o **Dispatcher** que é um módulo que lida com o armazenamento em cache e a filtragem de URL e é instalado no servidor da Web. Para obter mais informações sobre a arquitetura de AEM, consulte [Cenários típicos de implantação](/help/sites-deploying/deploy.md#typical-deployment-scenarios).

![chlimage_1-1](assets/chlimage_1-1a.png)

### Micro Kernels {#micro-kernels}

Micro Kernels atuam como gerentes de persistência em AEM. Existem três tipos de Micro Kernels usados com AEM: TarMK, MongoDB e Banco de Dados Relacional (sob suporte restrito). Escolher um que atenda às suas necessidades depende da finalidade de sua ocorrência e do tipo de implantação que você esteja considerando. Para obter mais informações sobre Micro Kernels, consulte o [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md) página.

![chlimage_1-2](assets/chlimage_1-2a.png)

### Nodestore {#nodestore}

No AEM, os dados binários podem ser armazenados independentemente dos nós de conteúdo. O local onde os dados binários são armazenados é chamado de **Armazenamento de dados**, enquanto a localização dos nós e propriedades de conteúdo é chamada de **Loja de nós**.

>[!NOTE]
>
>O Adobe recomenda que o TarMK seja a tecnologia de persistência padrão usada pelos clientes para as instâncias de Autor do AEM e Publicação.

>[!CAUTION]
>
>O Micro Kernel do Banco de Dados Relacional está sob suporte restrito. Contato [Atendimento ao cliente do Adobe](https://helpx.adobe.com/br/marketing-cloud/contact-support.html) antes de usar esse tipo de Micro Kernel.

![chlimage_1-3](assets/chlimage_1-3a.png)

### Armazenamento de dados {#data-store}

Ao lidar com um grande número de binários, é recomendável usar um armazenamento de dados externo em vez dos armazenamentos de nó padrão para maximizar o desempenho. Por exemplo, se o projeto exigir um grande número de ativos de mídia, armazená-los no Arquivo ou no Data Store do Azure/S3 fará com que o acesso seja mais rápido do que armazená-los diretamente em um MongoDB.

Para obter mais detalhes sobre as opções de configuração disponíveis, consulte [Configuração de nós e armazenamentos de dados](/help/sites-deploying/data-store-config.md).

>[!NOTE]
>
>O Adobe recomenda escolher a opção de implantar AEM no Azure ou no Amazon Web Services (AWS) usando o Adobe Managed Services, onde os clientes se beneficiarão de uma equipe que tem a experiência e as habilidades de implantar e operar AEM nesses ambientes de computação em nuvem. Consulte a [documentação adicional sobre o Adobe Managed Services](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t).
>
>Para recomendações sobre como implantar AEM no Azure ou no AWS, fora do Adobe Managed Services, recomendamos trabalhar diretamente com o provedor de nuvem ou um de nossos parceiros que oferecem suporte à implantação do AEM no ambiente de nuvem de sua escolha. O provedor ou parceiro de nuvem selecionado é responsável pelas especificações de dimensionamento, pelo design e pela implementação da arquitetura que ele oferecerá suporte para atender aos requisitos específicos de desempenho, carga, escalabilidade e segurança.
>
>Para obter detalhes adicionais, consulte também a seção [requisitos técnicos](/help/sites-deploying/technical-requirements.md#supported-platforms) página.

### Pesquisar {#search-features}

Listados nesta seção são os provedores de índice personalizados usados com o AEM. Para saber mais sobre indexação, consulte [Consultas e indexação do Oak](/help/sites-deploying/queries-and-indexing.md).

>[!NOTE]
>
>Para a maioria das implantações, o Adobe recomenda o uso do Índice Lucene. Você deve usar o Solr somente para escalabilidade em implantações especializadas e complexas.

![chlimage_1-4](assets/chlimage_1-4a.png)

### Diretrizes de desenvolvimento {#development-guidelines}

Você deve desenvolver AEM com o objetivo de **desempenho e escalabilidade**. Apresentamos abaixo uma série de práticas recomendadas que podem ser seguidas:

**DO**

* Aplicar separação de apresentação, lógica e conteúdo
* Use APIs AEM existentes (por exemplo: Sling) e ferramentas (ex: Replicação)
* Desenvolver no contexto do conteúdo real
* Desenvolver para otimizar a capacidade de armazenamento em cache
* Minimize o número de salvamentos (por exemplo: ao usar workflows transitórios)
* Certifique-se de que todos os pontos finais HTTP sejam RESTful
* Restringir o escopo da observação do JCR
* Considere o encadeamento assíncrono

**NÃO**

* Não use APIs JCR diretamente, se você puder
* Não altere /libs, mas use sobreposições
* Não use consultas sempre que possível
* Não use o Sling Bindings para obter serviços OSGi no código Java, mas use:

   * @Reference em um componente DS
   * @Inject em um Modelo Sling
   * sling.getService() em uma Classe de Uso Sightly
   * sling.getService() em um JSP
   * um ServiceTracker
   * acesso direto ao registro do serviço OSGi

Para obter mais detalhes sobre o desenvolvimento no AEM, leia [Desenvolvimento - Noções básicas](/help/sites-developing/the-basics.md). Para obter mais práticas recomendadas, consulte [Práticas recomendadas de desenvolvimento](/help/sites-developing/best-practices.md).

### Cenários de referência {#benchmark-scenarios}

>[!NOTE]
>
>Todos os testes de benchmark exibidos nesta página foram executados em uma configuração de laboratório.

Os cenários de teste detalhados abaixo são usados para as seções de benchmark dos capítulos TarMK, MongoMk e TarMK vs MongoMk. Para ver qual cenário foi usado para um teste de referencial específico, leia o campo Cenário da [Especificações técnicas](/help/sites-deploying/performance-guidelines.md#tarmk-performance-benchmark) tabela.

**Cenário de produto único**

AEM Assets:

* Interações do usuário: Pesquise ativos / Pesquise ativos / Baixe ativos / Leia metadados do ativo / Atualize metadados do ativo / Carregar ativo / Executar fluxo de trabalho de upload de ativo
* Modo de execução: usuários simultâneos, única interação por usuário

**Cenário de combinação de produtos**

AEM Sites + Ativos:

* Interações do usuário do Sites: Ler Página Do Artigo / Ler Página / Criar Parágrafo / Editar Parágrafo / Criar Página De Conteúdo / Ativar Página De Conteúdo / Pesquisar Do Autor
* Interações do usuário do Assets: Pesquise ativos / Pesquise ativos / Baixe ativos / Leia metadados do ativo / Atualize metadados do ativo / Carregar ativo / Executar fluxo de trabalho de upload de ativo
* Modo de execução: usuários simultâneos, interações mistas por usuário

**Cenário de caso de uso vertical**

Mídia:

* Ler Página Do Artigo (27.4%), Página De Leitura (10.9%), Criar Sessão (2.6%), Ativar Página De Conteúdo (1.7%), Criar Página De Conteúdo (0.4%), Criar Parágrafo (4.3%), Editar Parágrafo (0.9%), Componente De Imagem (0.9%), Pesquisar Ativos (20%), Ler Metadados De Ativos (8.5 %), Baixar Ativo (4.2%), Pesquisar Ativo (0.2%), Atualizar Metadados De Ativo (2.4%), Fazer Upload De Ativo (1.2%), Procurar Projeto (4.9%), Ler Projeto (6.6%), Adicionar Ativo (1.2%), Adicionar Projeto (1.2%), Criar Projeto (0.1%), Pesquisa Do Autor )
* Modo de execução: usuários simultâneos, interações mistas por usuário

## TarMK {#tarmk}

Este capítulo fornece diretrizes gerais de desempenho para o TarMK, especificando os requisitos mínimos de arquitetura e a configuração das configurações. Os testes de referência são também fornecidos para maior clarificação.

O Adobe recomenda que o TarMK seja a tecnologia de persistência padrão usada pelos clientes em todos os cenários de implantação, tanto para as instâncias de Autor e Publicação do AEM.

Para obter mais informações sobre TarMK, consulte [Cenários de implantação](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) e [Armazenamento Tar](/help/sites-deploying/storage-elements-in-aem-6.md#tar-storage).

### Diretrizes de arquitetura mínima do TarMK {#tarmk-minimum-architecture-guidelines}

>[!NOTE]
>
>As diretrizes mínimas de arquitetura apresentadas abaixo são para ambientes de produção e sites de alto tráfego. Estes **not** o [especificações mínimas](/help/sites-deploying/technical-requirements.md#prerequisites) necessário para executar o AEM.

Para estabelecer um bom desempenho ao usar o TarMK, você deve começar com a seguinte arquitetura:

* Uma instância de autor
* Duas instâncias de publicação
* Dois Dispatchers

As diretrizes de arquitetura para AEM sites e AEM Assets estão ilustradas abaixo.

>[!NOTE]
>
>A replicação sem binário deve ser desativada **ATIVADO** se o armazenamento de dados do arquivo for compartilhado.

**Diretrizes de arquitetura Tar para a AEM Sites**

![chlimage_1-5](assets/chlimage_1-5a.png)

**Diretrizes de arquitetura Tar para a AEM Assets**

![chlimage_1-6](assets/chlimage_1-6a.png)

### Diretriz de configurações do TarMK {#tarmk-settings-guideline}

Para um bom desempenho, você deve seguir as diretrizes de configuração apresentadas abaixo. Para obter instruções sobre como alterar as configurações, [veja esta página](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

<table>
 <tbody>
  <tr>
   <td><strong>Configuração</strong></td>
   <td><strong>Parâmetro</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Filas de Trabalho Sling</td>
   <td><code>queue.maxparallel</code></td>
   <td>Defina o valor para metade do número de núcleos da CPU. </td>
   <td>Por padrão, o número de threads simultâneos por fila de trabalhos é igual ao número de núcleos da CPU.</td>
  </tr>
  <tr>
   <td>Fila de Fluxo de Trabalho Transitório do Granite</td>
   <td><code>Max Parallel</code></td>
   <td>Defina o valor para metade do número de núcleos da CPU</td>
   <td> </td>
  </tr>
  <tr>
   <td>Parâmetros da JVM</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>Verdadeiro</p> </td>
   <td>Adicione esses parâmetros da JVM no script de início de AEM para impedir que consultas expansivas sobrecarreguem os sistemas.</td>
  </tr>
  <tr>
   <td>Configuração do índice Lucene</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Ativado</p> <p>Ativado</p> <p>Ativado</p> </td>
   <td>Para obter mais detalhes sobre os parâmetros disponíveis, consulte <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">esta página</a>.</td>
  </tr>
  <tr>
   <td>Armazenamento de dados = Armazenamento de dados S3</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576 (1MB) ou menor</p> <p>2-10% do tamanho máximo do heap</p> </td>
   <td>Consulte também <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">Configurações do armazenamento de dados</a>.</td>
  </tr>
  <tr>
   <td>Fluxo de trabalho do Ativo de atualização DAM</td>
   <td><code>Transient Workflow</code></td>
   <td>verificado</td>
   <td>Esse fluxo de trabalho controla a atualização de ativos.</td>
  </tr>
  <tr>
   <td>Writeback de metadados DAM</td>
   <td><code>Transient Workflow</code></td>
   <td>verificado</td>
   <td>Esse workflow gerencia XMP write-back para o binário original e define a data da última modificação no JCR.</td>
  </tr>
 </tbody>
</table>

### Benchmark de desempenho do TarMK {#tarmk-performance-benchmark}

#### Especificações técnicas {#technical-specifications}

Os testes de benchmark foram realizados com as seguintes especificações:

|  | **Nó do autor** |
|---|---|
| Servidor | Hardware de metal nu (HP) |
| Sistema Operacional | RedHat Linux |
| CPU / núcleos | CPU Intel(R) Xeon(R) CPU E5-2407 @2,40GHz, 8 núcleos |
| RAM | 32GB |
| Disco | Magnético |
| Java | Oracle JRE versão 8 |
| Heap da JVM | 16GB |
| Produto | AEM 6.2 |
| Nodestore | TarMK |
| Armazenamento de dados | DS de arquivo |
| Cenário | Produto único: Ativos / 30 threads simultâneos |

#### Resultados do benchmark de desempenho {#performance-benchmark-results}

>[!NOTE]
>
>Os números apresentados abaixo foram normalizados para 1 como linha de base e não são os números reais da taxa de transferência.

![chlimage_1-7](assets/chlimage_1-7a.png) ![chlimage_1-8](assets/chlimage_1-8a.png)

## MongoMK {#mongomk}

O motivo principal para escolher o back-end de persistência do MongoMK sobre o TarMK é dimensionar as instâncias horizontalmente. Isso significa ter duas ou mais instâncias de autor ativas em execução contínua e usar o MongoDB como o sistema de armazenamento de persistência. A necessidade de executar mais de uma instância de autor geralmente resulta do fato de que a CPU e a capacidade de memória de um único servidor, suportando todas as atividades de criação simultâneas, não são mais sustentáveis.

Para obter mais informações sobre TarMK, consulte [Cenários de implantação](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) e [Armazenamento Mongo](/help/sites-deploying/storage-elements-in-aem-6.md#mongo-storage).

### Diretrizes de arquitetura mínima do MongoMK {#mongomk-minimum-architecture-guidelines}

Para estabelecer um bom desempenho ao usar o MongoMK, você deve começar com a seguinte arquitetura:

* Três instâncias de autor
* Duas instâncias de publicação
* Três instâncias do MongoDB
* Dois Dispatchers

>[!NOTE]
>
>Em ambientes de produção, o MongoDB sempre será usado como um conjunto de réplicas com um primário e dois segundos. Leituras e gravações vão para o primário e as leituras podem ir para os secundários. Se o armazenamento não estiver disponível, um dos secundários pode ser substituído por um árbitro, mas os conjuntos de réplicas do MongoDB devem sempre ser compostos por um número ímpar de instâncias.

>[!NOTE]
>
>A replicação sem binário deve ser desativada **ATIVADO** se o armazenamento de dados do arquivo for compartilhado.

![chlimage_1-9](assets/chlimage_1-9a.png)

### Diretrizes de configurações do MongoMK {#mongomk-settings-guidelines}

Para um bom desempenho, você deve seguir as diretrizes de configuração apresentadas abaixo. Para obter instruções sobre como alterar as configurações, [veja esta página](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

<table>
 <tbody>
  <tr>
   <td><strong>Configuração</strong></td>
   <td><strong>Parâmetro</strong></td>
   <td><strong>Value (padrão)</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Filas de Trabalho Sling</td>
   <td><code>queue.maxparallel</code></td>
   <td>Defina o valor para metade do número de núcleos da CPU. </td>
   <td>Por padrão, o número de threads simultâneos por fila de trabalhos é igual ao número de núcleos da CPU.</td>
  </tr>
  <tr>
   <td>Fila de Fluxo de Trabalho Transitório do Granite</td>
   <td><code>Max Parallel</code></td>
   <td>Defina o valor para metade do número de núcleos da CPU.</td>
   <td> </td>
  </tr>
  <tr>
   <td>Parâmetros da JVM</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> <p><code>Doak.mongo.maxQueryTimeMS</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>Verdadeiro</p> <p>60000</p> </td>
   <td>Adicione esses parâmetros da JVM no script de início de AEM para impedir que consultas expansivas sobrecarreguem os sistemas.</td>
  </tr>
  <tr>
   <td>Configuração do índice Lucene</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Ativado</p> <p>Ativado</p> <p>Ativado</p> </td>
   <td>Para obter mais detalhes sobre os parâmetros disponíveis, consulte <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">esta página</a>.</td>
  </tr>
  <tr>
   <td>Armazenamento de dados = Armazenamento de dados S3</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576 (1MB) ou menor</p> <p>2-10% do tamanho máximo do heap</p> </td>
   <td>Consulte também <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">Configurações do armazenamento de dados</a>.</td>
  </tr>
  <tr>
   <td>DocumentNodeStoreService</td>
   <td><p><code>cache</code></p> <p><code>nodeCachePercentage</code></p> <p><code>childrenCachePercentage</code></p> <p><code>diffCachePercentage</code></p> <p><code>docChildrenCachePercentage</code></p> <p><code>prevDocCachePercentage</code></p> <p><code>persistentCache</code></p> </td>
   <td><p>2048</p> <p>35 (25)</p> <p>20 (10)</p> <p>30 (5)</p> <p>10 (3)</p> <p>4 (4)</p> <p>./cache,size=2048,binary=0,-compact,-compress</p> </td>
   <td><p>O tamanho padrão do cache é definido como 256 MB.</p> <p>Tem impacto no tempo necessário para executar a invalidação do cache.</p> </td>
  </tr>
  <tr>
   <td>oak-observation</td>
   <td><p><code>thread pool</code></p> <p><code>length</code></p> </td>
   <td><p>mín. e máx. = 20</p> <p>50000</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Benchmark de desempenho do MongoMK {#mongomk-performance-benchmark}

### Especificações técnicas {#technical-specifications-1}

Os testes de benchmark foram realizados com as seguintes especificações:

|  | **Nó Autor** | **Nó MongoDB** |
|---|---|---|
| Servidor | Hardware de metal nu (HP) | Hardware de metal nu (HP) |
| Sistema Operacional | RedHat Linux | RedHat Linux |
| CPU / núcleos | CPU Intel(R) Xeon(R) CPU E5-2407 @2,40GHz, 8 núcleos | CPU Intel(R) Xeon(R) CPU E5-2407 @2,40GHz, 8 núcleos |
| RAM | 32GB | 32GB |
| Disco | Magnético - >IOPS de 1k | Magnético - >IOPS de 1k |
| Java | Oracle JRE versão 8 | N/A |
| Heap da JVM | 16GB | N/A |
| Produto | AEM 6.2 | MongoDB 3.2 WiredTiger |
| Nodestore | MongoMK | N/A |
| Armazenamento de dados | DS de arquivo | N/A |
| Cenário | Produto único: Ativos / 30 threads simultâneos | Produto único: Ativos / 30 threads simultâneos |

### Resultados do benchmark de desempenho {#performance-benchmark-results-1}

>[!NOTE]
>
>Os números apresentados abaixo foram normalizados para 1 como linha de base e não são os números reais da taxa de transferência.

![chlimage_1-10](assets/chlimage_1-10a.png) ![chlimage_1-11](assets/chlimage_1-11a.png)

## TarMK vs MongoMK {#tarmk-vs-mongomk}

A regra básica que precisa ser levada em conta ao escolher entre os dois é que o TarMK foi projetado para desempenho, enquanto o MongoMK é usado para escalabilidade. O Adobe recomenda que o TarMK seja a tecnologia de persistência padrão usada pelos clientes em todos os cenários de implantação, tanto para as instâncias de Autor e Publicação do AEM.

O motivo principal para escolher o back-end de persistência do MongoMK sobre o TarMK é dimensionar as instâncias horizontalmente. Isso significa ter duas ou mais instâncias de autor ativas em execução contínua e usar o MongoDB como o sistema de armazenamento de persistência. A necessidade de executar mais de uma instância de autor geralmente resulta do fato de que a CPU e a capacidade de memória de um único servidor, suportando todas as atividades de criação simultâneas, não são mais sustentáveis.

Para obter mais detalhes sobre TarMK vs MongoMK, consulte [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md#microkernels-which-one-to-use).

### Diretrizes do TarMK vs MongoMk {#tarmk-vs-mongomk-guidelines}

**Benefícios do TarMK**

* Propósito criado para aplicativos de gerenciamento de conteúdo
* Os arquivos são sempre consistentes e podem ser copiados em backup usando qualquer ferramenta de backup baseada em arquivo
* Fornece um mecanismo de failover - consulte [Modo de espera a frio](/help/sites-deploying/tarmk-cold-standby.md) para obter mais detalhes
* Fornece alto desempenho e armazenamento de dados confiável com o mínimo de sobrecarga operacional
* TCO mais baixo (custo total de propriedade)

**Critérios para escolher MongoMK**

* Número de usuários nomeados conectados em um dia: nos milhares ou mais
* Número de usuários simultâneos: nas centenas ou mais
* Volume de ingestões de ativos por dia: em centenas de milhares ou mais
* Volume de edições de página por dia: em centenas de milhares ou mais
* Volume de pesquisas por dia: em dezenas de milhares ou mais

### TarMK vs. Benchmarks do MongoMK {#tarmk-vs-mongomk-benchmarks}

>[!NOTE]
>
>Os números apresentados abaixo foram normalizados para 1 como linha de base e não são números reais da taxa de transferência.

### Especificações técnicas do cenário 1 {#scenario-technical-specifications}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Nó OAK do autor</strong></td>
   <td><strong>Nó MongoDB</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td>Servidor</td>
   <td>Hardware de metal nu (HP)</td>
   <td>Hardware de metal nu (HP)</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sistema Operacional</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
   <td> </td>
  </tr>
  <tr>
   <td>CPU / núcleos</td>
   <td>CPU Intel(R) Xeon(R) CPU E5-2407 @2,40GHz, 8 núcleos</td>
   <td>CPU Intel(R) Xeon(R) CPU E5-2407 @2,40GHz, 8 núcleos</td>
   <td> </td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>32GB</td>
   <td>32GB</td>
   <td> </td>
  </tr>
  <tr>
   <td>Disco</td>
   <td>Magnético - &gt;IOPS de 1k</td>
   <td>Magnético - &gt;IOPS de 1k</td>
   <td> </td>
  </tr>
  <tr>
   <td>Java</td>
   <td>Oracle JRE versão 8</td>
   <td>N/A</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM Heap16GB</td>
   <td>16GB</td>
   <td>N/A</td>
   <td> </td>
  </tr>
  <tr>
   <td>Produto </td>
   <td>AEM 6.2</td>
   <td>MongoDB 3.2 WiredTiger</td>
   <td> </td>
  </tr>
  <tr>
   <td>Nodestore</td>
   <td>TarMK ou MongoMK</td>
   <td>N/A</td>
   <td> </td>
  </tr>
  <tr>
   <td>Armazenamento de dados</td>
   <td>DS de arquivo </td>
   <td>N/A</td>
   <td> </td>
  </tr>
  <tr>
   <td>Cenário</td>
   <td><p><br /> Produto único: Ativos / 30 threads simultâneos por execução</p> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Resultados do benchmark de desempenho do cenário 1 {#scenario-performance-benchmark-results}

![chlimage_1-12](assets/chlimage_1-12a.png)

### Cenário 2 Especificações técnicas {#scenario-technical-specifications-1}

>[!NOTE]
>
>Para ativar o mesmo número de Autores com MongoDB como com um sistema TarMK, você precisa de um cluster com dois nós AEM. Um cluster MongoDB de quatro nós pode lidar com 1,8 vezes o número de Autores de uma instância TarMK. Um cluster MongoDB de oito nós pode lidar com 2,3 vezes o número de Autores de uma instância TarMK.

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Nó TarMK do autor</strong></td>
   <td><strong>Nó MongoMK do autor</strong></td>
   <td><strong>Nó MongoDB</strong></td>
  </tr>
  <tr>
   <td>Servidor</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
  </tr>
  <tr>
   <td>Sistema Operacional</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
  </tr>
  <tr>
   <td>CPU / núcleos</td>
   <td>32</td>
   <td>32</td>
   <td>32</td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>60GB</td>
   <td>60GB</td>
   <td>60GB</td>
  </tr>
  <tr>
   <td>Disco</td>
   <td>SSD - IOPS de 10 mil</td>
   <td>SSD - IOPS de 10 mil</td>
   <td>SSD - IOPS de 10 mil</td>
  </tr>
  <tr>
   <td>Java</td>
   <td>Oracle JRE versão 8</td>
   <td><br /> Oracle JRE versão 8</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td>JVM Heap16GB</td>
   <td>30GB</td>
   <td>30GB</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td>Produto </td>
   <td>AEM 6.2</td>
   <td>AEM 6.2</td>
   <td><br /> MongoDB 3.2 WiredTiger</td>
  </tr>
  <tr>
   <td>Nodestore</td>
   <td>TarMK </td>
   <td>MongoMK</td>
   <td><br /> N/A</td>
  </tr>
  <tr>
   <td>Armazenamento de dados</td>
   <td>DS de arquivo </td>
   <td><br /> DS de arquivo</td>
   <td><br /> N/A</td>
  </tr>
  <tr>
   <td>Cenário</td>
   <td><p><br /> <br /> Caso de uso vertical: Mídia / 2000 threads simultâneos</p> </td>
   <td></td>
   <td></td>
  </tr>
 </tbody>
</table>

### Resultados do benchmark de desempenho do cenário 2 {#scenario-performance-benchmark-results-1}

![chlimage_1-13](assets/chlimage_1-13a.png)

### Diretrizes De Escalabilidade Da Arquitetura Para AEM Sites E Ativos {#architecture-scalability-guidelines-for-aem-sites-and-assets}

![chlimage_1-14](assets/chlimage_1-14a.png)

## Resumo das diretrizes de desempenho  {#summary-of-performance-guidelines}

As diretrizes apresentadas nesta página podem ser resumidas da seguinte maneira:

* **TarMK com armazenamento de dados de arquivo** é a arquitetura recomendada para a maioria dos clientes:

   * Topologia mínima: uma instância de Autor, duas instâncias de Publicação, dois Dispatchers
   * Replicação sem binário ativada se o armazenamento de dados do arquivo for compartilhado

* **MongoMK com armazenamento de dados de arquivo** é a arquitetura recomendada para a escalabilidade horizontal do nível Autor:

   * Topologia mínima: três instâncias de Autor, três instâncias de MongoDB, duas instâncias de Publicação, dois Dispatchers
   * Replicação sem binário ativada se o armazenamento de dados do arquivo for compartilhado

* **Nodestore** deve ser armazenado no disco local, não em um NAS (Network Attached Storage, armazenamento conectado à rede)
* Ao usar **Amazon S3**:

   * O armazenamento de dados do Amazon S3 é compartilhado entre a camada Autor e Publicação
   * A replicação sem binário deve ser ativada
   * A coleta de lixo do armazenamento de dados requer uma primeira execução em todos os nós Autor e Publicação e, em seguida, uma segunda execução no Autor

* **O índice personalizado deve ser criado além do índice predefinido** com base nas pesquisas mais comuns

   * Índices Lucene devem ser usados para índices personalizados

* **A personalização do fluxo de trabalho pode melhorar substancialmente o desempenho**, por exemplo, remoção da etapa de vídeo no fluxo de trabalho &quot;Atualizar ativo&quot;, desativação de ouvintes que não são usados etc.

Para obter mais detalhes, leia também a [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md) página.
