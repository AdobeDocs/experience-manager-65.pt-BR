---
title: Contribuir para o AEM
seo-title: Contributing to AEM
description: O AEM é desenvolvido de acordo com metodologias comprovadas comumente praticadas em grandes projetos de código aberto
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
ht-degree: 0%

---

# Contribuir para o AEM{#contributing-to-aem}

## Metodologia de desenvolvimento {#development-methodology}

O AEM é desenvolvido de acordo com metodologias comprovadas comumente praticadas em grandes projetos de código aberto. Muitos elementos principais na pilha de tecnologia AEM são, de fato, mantidos como projetos de código aberto ativos, como Sling e Jackrabbit, que contribuíram para a Apache Software Foundation. Um aspecto importante desse espírito que está presente no AEM é que você é incentivado a fazer uso das listas de discussão e fóruns on-line disponíveis para interações diretas com a equipe de desenvolvimento.

Se você está contribuindo com componentes do AEM, deve se familiarizar com o AEM como faria ao contribuir para um projeto de código aberto, e comunicar-se com a equipe principal existente como faria quando pretenderia contribuir para tal projeto.

## Experiência necessária {#required-experience}

O HTTP (HyperText Transfer Protocol) é fundamental para tudo o que fazemos. Portanto, antes de contribuir para o AEM, você deve ter um profundo entendimento do HTTP, idealmente na medida em que seja capaz de escrever sua própria implementação Java de um servidor HTTP multithread com pool de threads. Você também deve ter uma compreensão do comportamento de manutenção de atividade HTTP/1.1 e um conhecimento profundo das interações do lado do servidor/cliente com o JavaScript, especialmente o estilo assíncrono de interação representado pelo AJAX.

Como o dinamismo da página e o conteúdo interativo são fundamentais para a experiência do WM, é essencial que você tenha uma compreensão bastante profunda do Modelo de objeto do documento e seu potencial para manipulação programática em resposta a eventos. Você deve ter algum conhecimento, por exemplo, de manipulação de DOM em tempo real e comportamento de arrastar e soltar em vários documentos do navegador (por exemplo, usando iframes).

Portanto, no nível mais alto, você deve ter uma sólida compreensão sobre:

* o [Protocolo HTTP/1.1](https://www.ietf.org/rfc/rfc2616.txt)
* HTML (de preferência [HTML5](https://dev.w3.org/html5/spec/Overview.html))
* Folhas de estilo em cascata
* XML (Extensible Markup Language - Linguagem de marcação extensível)
* Padrões de design assíncronos de JavaScript e XML (AJAX)
* Anotação de objeto JavaScript (JSON)
* o modelo de objeto do documento
* Interações com estado vs. sem estado
* [Identificadores Uniformes de Recursos](https://www.ietf.org/rfc/rfc2396.txt)
* Cookies do navegador
* e outros conceitos modernos de desenvolvimento na Web

A pilha de tecnologia do Adobe Experience Manager é baseada no [Apache Felix](https://felix.apache.org/) Contêiner OSGI com o [Apache Sling](https://sling.apache.org/site/index.html) estrutura da Web e incorpora um Repositório de conteúdo Java ([JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html)) baseado em [Apache Jackrabbit](https://jackrabbit.apache.org/jcr-api.html). Você deve se familiarizar com esses projetos individuais, bem como com quaisquer outros componentes de código aberto (por exemplo, Apache Lucene) usados na área em que pretende contribuir.

## Conhecimento tribal {#tribal-knowledge}

Certos conceitos e princípios orientadores estão profundamente enraizados na cultura antiga. Esta seção lista alguns dos problemas &quot;profundamente incorporados ao DNA&quot; dos quais você deve estar ciente.

### Tudo é Conteúdo {#everything-is-content}

O conteúdo inclui não apenas todos os dados que o aplicativo web persiste. O código do programa, bibliotecas, scripts, templates, HTML, CSS, imagens e artefatos de todos os tipos, tudo e mais é mantido no Repositório de conteúdo e importado/exportado na forma de pacotes por meio do Gerenciador de pacotes e do Compartilhamento de pacotes.

### Modelo de David {#david-s-model}

A forma como o conteúdo deve ser modelado em um repositório de conteúdo Java requer uma maneira de pensar totalmente diferente do que é a prática comum no setor de software para modelagem de dados no mundo relacional. Leitura essencial para qualquer recém-chegado ao gerenciamento de conteúdo, a maneira JCR é [David&#39;s Model: Um guia para a modelagem de conteúdo](https://wiki.apache.org/jackrabbit/DavidsModel).

### RESTfulness {#restfulness}

A abordagem do REST está profundamente enraizada no que fazemos. Isso significa, entre outras coisas, evitar interações com informações de estado e ter em mente que os URIs são endereços definitivos de conteúdo e serviços.

REST (REpresentational State Transfer) refere-se ao estilo de arquitetura de software no qual a World Wide Web se baseia. Ele descreve os principais elementos que fazem a Web funcionar e, portanto, fornece um conjunto de princípios para como o software baseado na Web deve ser projetado. Ao projetar uma API para ser usada na Web, faz sentido aderir a essas &quot;práticas recomendadas&quot;.

Como o REST fornece a filosofia orientadora por trás de muito do que fazemos, você deve considerar essencial se tornar bem versado nos princípios do design RESTful. Um bom ponto de partida é [Dissertação de Roy Fielding](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm).

### Resolução da solicitação do Sling {#sling-request-resolution}

Um aspecto importante para entender sobre o AEM é como as solicitações recebidas se relacionam ao comportamento do conteúdo e do aplicativo, como o conteúdo é estruturado no repositório de conteúdo e onde o AEM procura a lógica do aplicativo para lidar com a solicitação. Saiba mais sobre o Apache [Decomposição do URL do Sling](https://sling.apache.org/site/url-decomposition.html) e a maneira como ele impõe o estilo de arquitetura REST e suas restrições de sistema sem estado, armazenáveis em cache e em camadas.

Os principais aspectos para entender a resolução de solicitações do Apache Sling são como as solicitações são mapeadas principalmente para um recurso específico no Repositório de conteúdo, como as propriedades adicionais da solicitação, juntamente com as propriedades desses objetos de conteúdo, determinam qual código de aplicativo será chamado para renderizar o conteúdo e como o código em /apps substitui o código em /libs.

### Quickstart {#quickstart}

Nenhuma etapa três: para instalar e executar, basta baixar e clicar duas vezes no arquivo JAR Quickstart. Não há etapa três. Qualquer funcionalidade opcional adicional não deve exigir mais do que a instalação do pacote apropriado do Compartilhamento de pacotes.

Tamanho pequeno do Quickstart: mantém o tamanho mínimo do arquivo JAR do Quickstart. Faça uso inteligente e otimizado de bibliotecas, movendo a funcionalidade opcional para o compartilhamento de pacotes.

Inicialização mais rápida: quando você fizer uma alteração que possa afetar o tempo de inicialização, certifique-se de que ela o tornará mais curto, não mais longo.

### Lean e Mean {#lean-and-mean}

Favorecemos códigos e projetos que sejam leves, pequenos, rápidos e elegantes. &quot;Bom o suficiente&quot; não é bom o suficiente.

Reutilização de código: nossa arquitetura de produto baseada em OSGi e a filosofia &quot;tudo é conteúdo&quot; significam que temos oportunidades incomuns de reutilização de código e artefatos. Tentamos aproveitar esse fato sempre que possível para manter os recursos enxutos.

Acoplamento frouxo: favorecemos interações fracamente acopladas em vez de dependências apertadas e &quot;intimidade indesejada&quot;. O acoplamento frouxo também permite maior reutilização do código.

### Não interrompa a demonstração {#don-t-break-the-demo}

Familiarize-se com scripts de demonstração e funcionalidades de produto que são mostrados com mais frequência em demonstrações. Entenda que, no mínimo, nada que você fizer deve quebrar um recurso de &quot;script de demonstração&quot;. O produto principal deve estar sempre pronto para demonstração, mesmo durante o desenvolvimento.

### Design para confiabilidade {#design-for-reliability}

Nós nos esforçamos para projetar e codificar recursos de modo falho e flexível, para que (por exemplo) um problema com um único elemento DOM não faça com que uma página inteira não seja renderizada. Em outras palavras: Fazer coisas que deveriam ser fatais, fatais. Torne tudo mais sobrevivível. Faça o produto &quot;perdoando&quot;.

### Anormal é o Novo Normal {#abnormal-is-the-new-normal}

Não dependa de ganchos de desligamento, verifique a limpeza na inicialização. O término anormal é o término normal.

`shutdown == kill -9 == power outage`

### Prepare-se para a geração de cluster elástico {#be-ready-for-elastic-clustering}

Esteja sempre pronto para clustering elástico, sempre suponha que haja clustering. Como regra geral, manter tudo que está no repositório de conteúdo significa oferecer suporte a cluster integrado.

### Design para compatibilidade com versões anteriores {#design-for-backward-compatibility}

Nada do que você faz deve quebrar o código antigo de um cliente. Considerar apenas `/libs` para conter o código do produto que pode ser atualizado durante uma atualização. A variável `/apps` do repositório é o código do projeto e a variável `/etc` contém configurações personalizadas que precisam ser preservadas. Geralmente, não substitua nada no `/apps`, `/content` e `/home`. Após uma atualização, o código do projeto antigo, as configurações e o conteúdo devem continuar a funcionar como acontecia antes da atualização.

Projetar para compatibilidade com versões anteriores também garante que a experiência de atualização corresponda à simplicidade da instalação inicial. Basta parar o AEM, substituir o arquivo JAR do Quickstart e iniciar o AEM novamente. Com uma base de instalação em rápido crescimento, a eficiência do upgrade será uma vantagem cada vez mais significativa.

Embora as APIs existentes possam e devam ser marcadas como obsoletas quando mais recentes, a melhor funcionalidade as substitui, todas as APIs que foram tornadas públicas em uma versão 5.x anterior precisam permanecer funcionais, pois podem estar em uso no código de aplicativo personalizado. Essas APIs não devem ser removidas.

A compatibilidade com versões anteriores também deve ser mantida em mente no que diz respeito à consistência geral da estrutura do conteúdo e da experiência do usuário.

## Conceitos principais {#core-concepts}

**Instância do autor** - Normalmente, por motivos de segurança, governança e outros motivos, um site de produção dividirá as instâncias de AEM em instâncias de Autor e Publicação. Para obter mais informações sobre a arquitetura de implantação (incluindo instâncias de Autor/Publicação), consulte a documentação sobre Instâncias AEM.

**Caching, fritura e panificação** - Tradicionalmente, os conceitos de panificação versus fritura são uma distinção importante entre diferentes sistemas de gestão de conteúdo na Web. No jargão do CMS, &quot;assar&quot; refere-se ao conceito de comprometer dados com arquivos estáticos em tempo de publicação, enquanto &quot;fritar&quot; refere-se ao conceito de processar dados para a apresentação final no momento da solicitação (ou seja, apenas no tempo).

**Clustering e balanceamento de carga** - Para aumentar a disponibilidade e melhorar o desempenho de um ambiente de Produção, é comum combinar várias instâncias de Autor e/ou Publicação (em Clusters), disponibilizando-as para diferentes grupos de usuários ou balanceando a carga delas em uma configuração do Dispatcher.

Também é possível combinar várias instâncias do repositório de conteúdo para criar uma *alta disponibilidade* Solução JCR, que pode ser integrada com a solução AEM para maximizar a proteção contra falhas de hardware e software. Consulte [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) para obter mais informações.

**Componente** - No AEM, um componente é um tipo de objeto, instâncias das quais geralmente podem ser criadas arrastando-as e soltando-as do Sidekick, por exemplo. Por exemplo, os componentes prontos para uso que acompanham o AEM incluem os componentes Texto, Título, Tag Cloud, Carrossel, Imagem e Lista, todos disponíveis no Sidekick no tempo de execução.

**Localizador de conteúdo** - No modo de criação, o Localizador de conteúdo é um painel especial (quadro) no lado esquerdo da página que, dependendo da guia selecionada na parte superior, exibe listas de imagens, documentos, ativos de Flash, páginas, parágrafos ou recursos do repositório que você pode arrastar e soltar do Localizador de conteúdo na página em que está trabalhando (à direita).

**Ativos digitais** - No AEM, os ativos digitais são (normalmente) imagens e arquivos de mídia avançada. Para obter mais informações, consulte Trabalhar com ativos digitais no DAM.

**Dispatcher** - O Dispatcher é uma ferramenta de armazenamento em cache e balanceamento de carga, além de fornecer determinadas salvaguardas de segurança.

**Widgets ExtJS** - A maioria dos elementos da interface do usuário no AEM usa ExtJS, que é uma biblioteca de widgets de terceiros escrita em JavaScript. O ExtJS apresenta widgets de interface do usuário personalizáveis de alto desempenho e um modelo de componentes extensível e bem projetado.

**JCR, repositório de conteúdo Java** - A especificação Java Content Repository (JSR-283) fornece um modelo de dados abstratos e uma interface de programação de aplicativos para realizar um repositório de dados NoSQL amplamente escalável que combina recursos de um sistema de arquivos e um banco de dados de objetos. Embora não seja necessário entender a JSR-283 em detalhes exaustivos, você deve dedicar tempo para se familiarizar com os recursos básicos do JCR e o modelo de dados subjacente a ele, porque o JCR é o que torna possível a filosofia &quot;tudo é conteúdo&quot; do AEM.

Em essência, o JCR é um sistema de nós e propriedades, em que os nós podem herdar de outros nós e todo o conteúdo é armazenado como propriedade *valores*. Observe que, além da herança comum, o JCR permite um conceito de nós de &quot;mixin&quot;, que permite a modelagem de herança múltipla.

O JCR tem vários tipos de nó e tipos de propriedade predefinidos, mas em geral o sistema de digitação é bastante flexível e (na verdade) um dos pontos fortes do JCR é que ele permite que o conteúdo estruturado e não estruturado seja armazenado/gerenciado com a mesma facilidade. Ou seja, o JCR pode acomodar dados altamente estruturados, mas também pode acomodar estruturas de dados dinâmicos arbitrárias sem restrições de esquema.

O JavaDoc para a API Java do JCR é [aqui](https://jackrabbit.apache.org/jcr/jcr-api.html).

Antes de tentar ler o JavaDoc ou a especificação do JCR em si, talvez você queira consultar [esta explicação de alto nível](/help/sites-developing/the-basics.md#java-content-repository) do JCR conforme implementado pelos Adobe Experience Services.

**Gerenciador de vários sites (MSM)** - O recurso MSM do AEM ajuda os clientes a lidar com conteúdo multilíngue e multinacional, permitindo que eles equilibrem a identidade visual centralizada com o conteúdo localizado.

**OSGi** - OSGi é a tecnologia de tempo de execução baseada em serviços que fornece a base para o desenvolvimento modularizado do Java no AEM. É uma estrutura que fornece não apenas um ambiente de execução e carregamento de classe altamente dinâmico (e seguro) para recursos de código (conhecidos como pacotes), mas também controle total sobre a visibilidade e o ciclo de vida dos vários serviços expostos pelos pacotes. Um registro de serviço fornece um modelo de cooperação para pacotes que leva em conta a dinâmica do ciclo de vida (e os requisitos de versão). O OSGi resolve muitos dos problemas que os servidores de aplicativos tinham a intenção de resolver, mas o faz de forma leve e altamente dinâmica, possibilitando, por exemplo, a implantação de serviços a quente (tornando o novo código imediatamente disponível sem reiniciar o servidor).

**Parsys, Sistema de parágrafo** - O sistema de parágrafo (parsys) é um componente composto que permite aos autores adicionar componentes de diferentes tipos a uma página e contém outros componentes de parágrafo. Cada tipo de parágrafo é representado como um componente. O próprio sistema de parágrafo também é um componente, que contém os outros componentes de parágrafo.

**Microkernel** - Cada espaço de trabalho no repositório pode ser configurado separadamente para armazenar seus dados por meio de um microkernel específico (uma classe que gerencia a leitura e a gravação dos dados). Da mesma forma, o armazenamento de versão em todo o repositório também pode ser configurado independentemente para usar um microkernel específico. Há vários microkernels diferentes disponíveis, capazes de armazenar dados em uma variedade de formatos de arquivo ou bancos de dados relacionais. (Por exemplo, há gerenciadores de persistência para MongoDB, DB2 ou Oracle) O microkernel padrão para AEM é TarMK (veja mais abaixo).

**Publicar instância** - Por motivos de segurança, governança e outros, um site de produção normalmente dividirá instâncias de AEM em instâncias de Autor e Publicação. Para obter mais informações sobre a arquitetura de implantação (incluindo instâncias de Autor/Publicação), consulte a documentação sobre Instâncias AEM.

**Início rápido** - Ao contrário de muitos outros programas, você instala AEM usando um único arquivo JAR de &quot;Início rápido&quot; autoextraível. Ao clicar duas vezes no arquivo JAR pela primeira vez, tudo o que você precisa é instalado automaticamente. O JAR de início rápido inclui todos os arquivos necessários para o repositório CRX (incluindo recursos administrativos), serviços de repositório virtual, serviços de índice e pesquisa, serviços de fluxo de trabalho, segurança e um servidor Web, além do CQ Servlet Engine (CQSE) e todos os serviços AEM. Não há outros arquivos a serem instalados: o Quickstart é independente.

Na primeira vez que você inicia o Quickstart, ele cria um repositório completo compatível com JCR em segundo plano, o que pode levar vários minutos. Após essa inicialização inicial, as inicializações subsequentes são muito mais rápidas, pois a infraestrutura do repositório já foi estabelecida.

Muitas opções de inicialização (como o número da porta ativa e se a instância do AEM em questão deve ser uma instância de Publicação versus uma instância de Autor e muito mais) podem ser controladas renomeando adequadamente o arquivo Quickstart. Para ver uma lista de opções a esse respeito, execute o JAR com &quot;-help&quot; na linha de comando:

```shell
java -jar <quickstartfilename>.jar -help
```

**Agentes de replicação** : os agentes de replicação são fundamentais para o AEM como o mecanismo usado para publicar (ativar) conteúdo de um autor em um ambiente de publicação; liberar conteúdo do cache do Dispatcher; retornar conteúdo gerado pelo usuário (por exemplo, entrada de formulário) do ambiente de publicação para o ambiente de autor.

**Andaime** - Com o andaime, você pode criar um formulário (um andaime) com campos que refletem a estrutura desejada para as páginas e, em seguida, usar este formulário para criar facilmente páginas com base nessa estrutura.

**Segmentação** - Os visitantes do site têm interesses e objetivos diferentes quando chegam a um site. Entender os objetivos dos visitantes e atender às suas expectativas é um pré-requisito de sucesso importante para o marketing online. A segmentação ajuda a fazer isso analisando e caracterizando os detalhes de um visitante.

**Sidekick** - O Sidekick é uma janela flutuante semelhante a uma paleta que aparece na página editável, da qual novos componentes podem ser arrastados e ações que se aplicam à página podem ser executadas.

**Site Catalyst** : o SiteCatalyst fornece aos profissionais de marketing um local para medir, analisar e otimizar dados integrados de todas as iniciativas online em vários canais de marketing. Você pode usar o Adobe SiteCatalyst para analisar dados de sites AEM.

**Armazenamento de Tar (TarMK)** - TarMK é o sistema de persistência padrão no AEM. Embora o AEM possa ser configurado para usar um sistema de persistência diferente (como o MongoDB), o TarMK tem certas vantagens, pois é otimizado para desempenho em casos de uso típicos de JCR (portanto, é muito rápido), usa um formato de dados padrão do setor e pode ter backup rápido e fácil.

**Modelo** - No AEM, um Modelo especifica um tipo específico de página. Ele define a estrutura de uma página (enquanto também especifica uma imagem em miniatura e várias propriedades). Por exemplo, você pode ter modelos separados para páginas de produtos, mapas de site e informações de contato.

**Fluxo de trabalho** - O sistema de fluxo de trabalho AEM permite a criação de processos automatizados envolvendo páginas ou ativos.
