---
title: Contribuição para AEM
seo-title: Contributing to AEM
description: O AEM é desenvolvido segundo metodologias comprovadas geralmente utilizadas em grandes projetos de código aberto
seo-description: AEM is developed following proven methodologies commonly practiced in large open source projects
uuid: ffef60ae-8a9a-4c4b-8cbd-3cd72792a42e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f52402df-f6dc-4c62-82bc-cbce489b2b74
exl-id: 43fb4fa3-269a-4635-b055-4b7d787da21f
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '2709'
ht-degree: 1%

---

# Contribuição para AEM{#contributing-to-aem}

## Metodologia de desenvolvimento {#development-methodology}

O AEM é desenvolvido de acordo com metodologias comprovadas geralmente utilizadas em grandes projetos de código aberto. Muitos elementos principais AEM pilha de tecnologia são, de fato, mantidos como projetos ativos de código aberto, como Sling e Jackrabbit, que foram contribuídos para a Apache Software Foundation. Um aspecto importante desse espírito que está presente no AEM é que você é encorajado a usar as listas de endereços e fóruns online disponíveis para interações diretas com a equipe de desenvolvimento.

Se estiver contribuindo com componentes de AEM, você deve se familiarizar com AEM como faria ao contribuir com um projeto de código aberto e se comunicar com a equipe principal existente como faria quando você pretendia contribuir com tal projeto.

## Experiência necessária {#required-experience}

O protocolo HTTP (HyperText Transfer Protocol) é fundamental para tudo o que fazemos. Portanto, antes de contribuir com AEM, você deve ter uma compreensão profunda do HTTP, idealmente na medida em que seria capaz de escrever sua própria implementação do Java de um servidor HTTP multisegmentado com thread pooling. Você também deve conhecer o comportamento de manutenção de atividade do HTTP/1.1 e deve ter um conhecimento profundo das interações do lado do servidor/cliente com o JavaScript, especialmente o estilo assíncrono de interação representado pelo AJAX.

Como o dinamismo da página e o conteúdo interativo são fundamentais para a experiência de WM, é essencial que você tenha uma compreensão bastante profunda do Modelo de objeto de documento e seu potencial para manipulação programática em resposta aos eventos. Você deve ter conhecimento, por exemplo, de manipulação de DOM em tempo real e do comportamento de arrastar e soltar em vários documentos do navegador (por exemplo, usando iframes).

Portanto, no nível mais alto, você deve ter uma compreensão sólida de:

* o [Protocolo HTTP/1.1](https://www.ietf.org/rfc/rfc2616.txt)
* HTML (de preferência [HTML5](https://dev.w3.org/html5/spec/Overview.html))
* Folhas de estilos em cascata
* Linguagem de marcação extensível (XML)
* Padrões de design assíncronos do JavaScript e XML (AJAX)
* Notação de objeto JavaScript (JSON)
* o Modelo de objeto de documento
* Interações com estado e sem estado
* [Identificadores de Recurso Uniforme](https://www.ietf.org/rfc/rfc2396.txt)
* Cookies do navegador
* e outros conceitos modernos de desenvolvimento da Web

A pilha de tecnologia do Adobe Experience Manager é baseada no [Apache Felix](https://felix.apache.org/) Contêiner OSGI com [Apache Sling](https://sling.apache.org/site/index.html) estrutura da Web e incorpora um repositório de conteúdo Java ([JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html)) com base em [Apache Jackrabbit](https://jackrabbit.apache.org/jcr-api.html). Você deve se familiarizar com esses projetos individuais, bem como com quaisquer outros componentes de código aberto (por exemplo, Apache Lucene) usados na área em que pretende contribuir.

## Conhecimento Tribal {#tribal-knowledge}

Certos conceitos e princípios orientadores estão profundamente enraizados na antiga cultura do Dia. Esta seção lista alguns dos problemas &quot;profundamente incorporados ao DNA&quot; que você deve conhecer.

### Tudo é Conteúdo {#everything-is-content}

O conteúdo não inclui apenas todos os dados que o aplicativo web mantém. O código do programa, bibliotecas, scripts, templates, HTML, CSS, imagens e artefatos de todos os tipos, tudo e mais é mantido no Repositório de conteúdo e importado/exportado no formato de pacotes por meio do Gerenciador de pacotes e do Compartilhamento de pacotes.

### Modelo de David {#david-s-model}

A forma como o conteúdo deve ser modelado em um Java Content Repository requer uma maneira de pensar totalmente diferente da prática comum no setor de software para modelagem de dados no mundo relacional. Leitura essencial para qualquer novato no gerenciamento de conteúdo a maneira JCR é [Modelo de David: Um guia para modelagem de conteúdo](https://wiki.apache.org/jackrabbit/DavidsModel).

### RESTStatus {#restfulness}

A abordagem REST está profundamente enraizada no que fazemos. Isso significa, entre outras coisas, evitar interações de estado e ter em mente que os URIs são endereços definitivos para conteúdo e serviços.

REST (REpresentational State Transfer) refere-se ao estilo de arquitetura de software no qual se baseia a World Wide Web. Ele descreve os principais elementos que fazem a Web funcionar e, portanto, fornece um conjunto de princípios para como o software baseado na Web deve ser projetado. Ao projetar uma API para ser usada na Web, portanto, faz sentido seguir essas &quot;práticas recomendadas&quot;.

Como REST fornece a filosofia orientadora por trás de tanto do que fazemos, você deve considerar essencial se tornar bem versado nos princípios do design RESTful. Um bom ponto de partida é com [Dissertação de Roy Fielding](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm).

### Resolução de Solicitação Sling {#sling-request-resolution}

Um aspecto essencial para entender o AEM é como as solicitações recebidas estão relacionadas ao comportamento do conteúdo e do aplicativo, como o conteúdo é estruturado no repositório de conteúdo e onde AEM procura a lógica do aplicativo para lidar com a solicitação. Saiba mais sobre o Apache [Descontinuação do URL de sling](https://sling.apache.org/site/url-decomposition.html) e a forma como aplica o estilo arquitetônico REST e suas restrições de sistema sem estado, armazenável em cache e em camadas.

Os aspectos principais para entender sobre a resolução de solicitação do Apache Sling são como as solicitações são mapeadas primariamente para um recurso específico no Repositório de Conteúdo, como as propriedades adicionais da solicitação, juntamente com as propriedades desses objetos de conteúdo, determinam qual código de aplicativo será chamado para renderizar o conteúdo e como o código em /apps substitui o código em /libs.

### Quickstart {#quickstart}

Sem etapa três: Para instalar e executar, basta baixar e clicar duas vezes no arquivo JAR do Quickstart. Não há etapa três. Qualquer funcionalidade opcional adicional não deve exigir mais do que instalar o pacote apropriado do Compartilhamento de pacotes.

Tamanho pequeno do Início rápido: Mantenha o tamanho do arquivo JAR do Quickstart no mínimo. Use bibliotecas de maneira inteligente e otimizada, movendo a funcionalidade opcional para o compartilhamento de pacotes.

Tempo de inicialização mais rápido: Ao fazer uma alteração que possa afetar o tempo de inicialização, certifique-se de que ela seja mais curta e não mais longa.

### Lean e Mean {#lean-and-mean}

Nós favorecemos códigos e projetos que são leves, pequenos, rápidos e elegantes. &quot;Bom o suficiente&quot; não é bom o suficiente.

Reutilização de código: Nossa arquitetura de produto baseada em OSGi e a filosofia &quot;tudo é conteúdo&quot; significam que temos oportunidades excepcionalmente boas para reutilizar código e artefatos. Tentamos aproveitar esse fato sempre que possível para manter recursos fáceis e médios.

Ligação de rosca: Defendemos interações vagamente acopladas sobre dependências restritas e &quot;intimidade indesejada&quot;. O acoplamento de perda também permite mais reutilização do código.

### Não interrompa a demonstração {#don-t-break-the-demo}

Familiarize-se com os scripts de demonstração e as funcionalidades do produto mostradas com mais frequência nas demonstrações. Entenda que, no mínimo, nada que você faça deve quebrar um recurso de &quot;script de demonstração&quot;. O produto principal deve estar sempre pronto para demonstração, mesmo durante o desenvolvimento.

### Design para confiabilidade {#design-for-reliability}

Nos esforçamos para criar e codificar recursos de maneira flexível, de modo que (por exemplo) um problema com um único elemento DOM não faça com que uma página inteira não seja renderizada. Por outras palavras: Faça coisas que devem ser fatais, fatais. Torne tudo o resto sobrevivível. Faça o produto &quot;perdoar&quot;.

### Anormal é o Novo Normal {#abnormal-is-the-new-normal}

Não dependa dos ganchos de desligamento, assegure a limpeza na inicialização. Término anormal é terminação normal.

`shutdown == kill -9 == power outage`

### Esteja pronto para o clustering elástico {#be-ready-for-elastic-clustering}

Esteja sempre pronto para o clustering elástico, sempre suponha que há clustering. Como regra geral, atender a tudo no repositório de conteúdo significa ter suporte incorporado em cluster.

### Design para compatibilidade com versões anteriores {#design-for-backward-compatibility}

Nada que você faça deve quebrar o código antigo de um cliente. Considerar somente `/libs` para conter o código do produto que pode ser atualizado durante uma atualização. O `/apps` seção do repositório é o código do projeto e a variável `/etc` contém configurações personalizadas que precisam ser preservadas. Geralmente, não substitua nada em `/apps`, `/content` e `/home`. Após uma atualização, o código do projeto, as configurações e o conteúdo antigos devem continuar a funcionar da mesma maneira que antes da atualização.

Projetar para compatibilidade com versões anteriores também garante que a experiência de atualização corresponda à simplicidade da instalação inicial. Basta parar o AEM, substituir o arquivo JAR do Quickstart e iniciar o AEM novamente deve ser suficiente. Com uma base de instalação em rápido crescimento, a eficiência da atualização será uma vantagem cada vez mais significativa.

Embora as APIs existentes possam e devam ser marcadas como obsoletas quando mais recentes, a melhor funcionalidade as substitui, todas as APIs que foram tornadas públicas em uma versão 5.x anterior precisam permanecer funcionais, já que podem estar em uso no código de aplicativo personalizado. Essas APIs não devem ser removidas.

Deve também ter-se em conta a compatibilidade com versões anteriores no que respeita à coerência geral da estrutura de conteúdo e da experiência do utilizador.

## Conceitos principais {#core-concepts}

**Instância do autor** - Normalmente, por motivos de segurança, governança e outros, um site de produção dividirá instâncias de AEM em instâncias de Autor e Publicação. Para obter mais informações sobre a arquitetura de implantação (incluindo instâncias de Autor/Publicação), consulte a documentação sobre Instâncias de AEM.

**Armazenamento em cache, fritura e cozedura** - Tradicionalmente, os conceitos de cozinhar ou fritar são uma distinção importante entre os diferentes sistemas de gestão de conteúdo da Web. No jargão CMS, &quot;cozinhar&quot; refere-se ao conceito de confirmação de dados em arquivos estáticos no momento da publicação, enquanto &quot;fritar&quot; se refere ao conceito de processamento de dados para apresentação final no momento da solicitação (ou seja, apenas no tempo).

**Clustering e balanceamento de carga** - Para aumentar a disponibilidade e melhorar o desempenho de um ambiente de Produção, é comum combinar várias instâncias de Autor e/ou Publicação (em Clusters), tornando-as disponíveis para diferentes grupos de usuários ou balanceando a carga com base em uma configuração do Dispatcher.

Também é possível combinar várias instâncias do repositório de conteúdo para criar um *alta disponibilidade* Solução JCR, que pode ser integrada à sua solução de AEM para maximizar a proteção contra falhas de hardware e software. Consulte [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) para obter mais informações.

**Componente** - Em AEM, um Componente é um tipo de objeto, cujas instâncias geralmente podem ser criadas arrastando-as e soltando-as, por exemplo, do Sidekick. Assim, por exemplo, os componentes prontos para uso que acompanham o AEM incluem os componentes Texto, Título, Tag Cloud, Carrossel, Imagem e Lista, todos disponíveis no Sidekick no tempo de execução.

**Localizador de conteúdo** - No modo de criação, o Localizador de conteúdo é um painel especial (quadro) no lado esquerdo da página que, dependendo da guia selecionada na parte superior, exibe listas de imagens, documentos, ativos do Flash, páginas, parágrafos ou recursos do repositório que você pode arrastar e soltar do Localizador de conteúdo para a página em que está trabalhando (à direita).

**Ativos digitais** - No AEM, os Ativos digitais são (normalmente) imagens e arquivos de mídia avançada. Para obter mais informações, consulte Trabalhar com ativos digitais no DAM.

**Dispatcher** - O Dispatcher é um instrumento de armazenamento em cache e de balanceamento de carga, bem como fornece determinadas salvaguardas de segurança.

**Widgets ExtJS** - A maioria dos elementos da interface do usuário no AEM usam ExtJS, que é uma biblioteca de widgets de terceiros escrita em JavaScript. O ExtJS apresenta widgets de interface de usuário personalizáveis de alto desempenho e um modelo de componente bem projetado e extensível.

**JCR, repositório de conteúdo Java** - A especificação Java Content Repository (JSR-283) fornece um modelo de dados abstrato e uma Interface de Programação de Aplicativos para realizar um repositório de dados NoSQL massivamente escalável que combina recursos de um sistema de arquivos e um banco de dados de objetos. Embora você não precise entender o JSR-283 em detalhes exaustivos, é necessário tempo para se familiarizar com os recursos básicos do JCR e o modelo de dados subjacente, pois o JCR é o que torna possível a filosofia de AEM &quot;tudo é conteúdo&quot;.

Em essência, o JCR é um sistema de nós e propriedades, em que os nós podem herdar de outros nós e todo o conteúdo é armazenado como propriedade *values*. Observe que, além da herança comum, o JCR permite um conceito de nós &quot;mixin&quot;, o que permite a modelagem de várias heranças.

O JCR tem vários tipos de nó predefinidos e tipos de propriedade, mas em geral o sistema de digitação é bastante flexível e (na verdade) uma das forças do JCR é que ele permite que conteúdo estruturado e não estruturado sejam armazenados/gerenciados com igual facilidade. Ou seja, o JCR pode acomodar dados altamente estruturados, mas também pode acomodar estruturas de dados dinâmicos arbitrárias sem restrições de esquema.

O JavaDoc para a API Java do JCR é [here](https://jackrabbit.apache.org/jcr/jcr-api.html).

Antes de tentar ler a especificação do JavaDoc ou do JCR propriamente dito, você pode consultar [esta explicação de alto nível](/help/sites-developing/the-basics.md#java-content-repository) do JCR conforme implementado pelo Adobe Experience Services.

**Multi-Site Manager (MSM)** - O recurso MSM do AEM ajuda os clientes a lidar com conteúdo multilíngue multinacional, permitindo que eles equilibrem a marca centralizada com conteúdo localizado.

**OSGi** - OSGi é a tecnologia de tempo de execução baseada em serviços que fornece a base para o desenvolvimento modularizado do Java no AEM. É uma estrutura que fornece não apenas um ambiente de carregamento de classe e execução seguro altamente dinâmico para recursos de código (conhecidos como pacotes), mas também controle total sobre a visibilidade e o ciclo de vida dos vários serviços expostos por pacotes. Um registro de serviços fornece um modelo de cooperação para pacotes que leva em consideração a dinâmica do ciclo de vida (e os requisitos de versão). O OSGi soluciona muitos dos problemas que os servidores de aplicativos deveriam resolver, mas faz isso de uma maneira leve e altamente dinâmica, possibilitando, por exemplo, a implantação de serviços em operação (disponibilizando o novo código imediatamente sem reiniciar o servidor).

**Parsys, Sistema de parágrafo** - O sistema de parágrafo (parsys) é um componente composto que permite aos autores adicionar componentes de diferentes tipos a uma página e contém outros componentes de parágrafo. Cada tipo de parágrafo é representado como um componente. O próprio sistema de parágrafo também é um componente, que contém os outros componentes de parágrafo.

**Microkernel** - Cada espaço de trabalho no repositório pode ser configurado separadamente para armazenar seus dados por meio de um microkernel específico (uma classe que gerencia a leitura e a gravação dos dados). Da mesma forma, o repositório de versões em todo o repositório também pode ser configurado de maneira independente para usar um microkernel específico. Há vários microkernels diferentes disponíveis, capazes de armazenar dados em diversos formatos de arquivo ou bancos de dados relacionais. (Por exemplo, há gerentes de persistência para MongoDB, DB2 ou Oracle) O microkernel padrão para AEM é TarMK (veja mais abaixo).

**Instância de publicação** - Por motivos de segurança, governança e outros, um site de produção normalmente dividirá instâncias de AEM em instâncias de Autor e Publicação. Para obter mais informações sobre a arquitetura de implantação (incluindo instâncias de Autor/Publicação), consulte a documentação sobre Instâncias de AEM.

**Início rápido** - Ao contrário de muitos outros programas, você instala o AEM usando um único arquivo JAR autoextraível &quot;Quickstart&quot;. Ao clicar duas vezes no arquivo JAR pela primeira vez, tudo o que você precisa é instalado automaticamente. O JAR de início rápido inclui todos os arquivos necessários para o repositório CRX (incluindo instalações administrativas), serviços de repositório virtual, serviços de índice e pesquisa, serviços de fluxo de trabalho, segurança e um servidor Web, além do CQ Servlet Engine (CQSE) e todos os serviços de AEM. Não há outros arquivos para instalar: o Quickstart é autocontido.

Na primeira vez que você inicia o Quickstart, ele cria um repositório compatível com JCR inteiro em segundo plano, que pode levar vários minutos. Após essa inicialização inicial, as inicializações subsequentes são muito mais rápidas, pois a infraestrutura do repositório já foi estabelecida.

Muitas opções de inicialização (como o número da porta ativa e se a instância de AEM em questão deve ser uma Instância de publicação versus uma instância de autor; e muito mais) podem ser controladas ao renomear adequadamente o arquivo Quickstart . Para ver uma lista de opções a esse respeito, execute o JAR com &quot;-help&quot; na linha de comando:

```shell
java -jar <quickstartfilename>.jar -help
```

**Agentes de replicação** - Os agentes de replicação são fundamentais para AEM como mecanismo usado para Publicar (ativar) conteúdo de um autor em um ambiente de publicação; liberar conteúdo do cache do Dispatcher; retorne o conteúdo gerado pelo usuário (por exemplo, entrada de formulário) do ambiente Publish para o ambiente Author .

**Andaime** - Com o scaffolding, você pode criar um formulário (um scaffold) com os campos que refletem a estrutura desejada para suas páginas e usar esse formulário para criar facilmente páginas com base nessa estrutura.

**Segmentação** - Os visitantes têm interesses e objetivos diferentes quando chegam a um site. Entender as metas dos visitantes e atender às expectativas é um pré-requisito importante para o sucesso do marketing online. A segmentação ajuda a conseguir isso ao analisar e caracterizar os detalhes do visitante.

**Sidekick** - O Sidekick é uma janela flutuante semelhante à paleta, exibida na página editável, da qual novos componentes podem ser arrastados e ações que se aplicam à página podem ser executadas.

**Site Catalyst** - O SiteCatalyst fornece aos profissionais de marketing um único local para medir, analisar e otimizar dados integrados de todas as iniciativas online em vários canais de marketing. Você pode usar o Adobe SiteCatalyst para analisar dados de sites AEM.

**Armazenamento Tar (TarMK)** - TarMK é o sistema de persistência padrão no AEM. Embora AEM possa ser configurado para usar um sistema de persistência diferente (como o MongoDB), o TarMK tem certas vantagens, na medida em que é otimizado para desempenho para casos de uso típicos do JCR (assim é muito rápido), usa um formato de dados padrão do setor e pode ser feito backup de forma rápida e fácil.

**Modelo** - Em AEM, um Modelo especifica um tipo específico de página. Ela define a estrutura de uma página (enquanto também normalmente especifica uma imagem em miniatura e várias propriedades). Por exemplo, você pode ter modelos separados para páginas de produtos, mapas de sites e informações de contato.

**Fluxo de trabalho** - O sistema Fluxo de trabalho AEM permite a criação de processos automatizados envolvendo páginas ou ativos.
