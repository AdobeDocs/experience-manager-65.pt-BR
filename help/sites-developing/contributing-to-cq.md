---
title: Contribuição para AEM
seo-title: Contribuição para AEM
description: O AEM é desenvolvido de acordo com metodologias comprovadas comumente utilizadas em grandes projetos de código aberto
seo-description: O AEM é desenvolvido de acordo com metodologias comprovadas comumente utilizadas em grandes projetos de código aberto
uuid: ffef60ae-8a9a-4c4b-8cbd-3cd72792a42e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f52402df-f6dc-4c62-82bc-cbce489b2b74
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2726'
ht-degree: 1%

---


# Contribuição para AEM{#contributing-to-aem}

## Metodologia de desenvolvimento {#development-methodology}

O AEM é desenvolvido de acordo com metodologias comprovadas, geralmente utilizadas em grandes projetos de código aberto. Muitos elementos fundamentais AEM pilha de tecnologia são, de fato, mantidos como projetos ativos de código aberto, como Sling e Jackrabbit, que foram contribuídos para a Apache Software Foundation. Um aspecto importante desse espírito que está presente no AEM é que você é encorajado a usar as listas de e-mail e os fóruns online disponíveis para interações diretas com a equipe de desenvolvimento.

Se você estiver contribuindo com componentes de AEM, deverá se familiarizar com AEM como faria ao contribuir para um projeto de código aberto e se comunicar com a equipe principal existente como você faria quando você pretendesse contribuir com tal projeto.

## Experiência exigida {#required-experience}

O protocolo HTTP (HyperText Transfer Protocol) é central para tudo o que fazemos. Portanto, antes de contribuir para AEM, você deve ter uma compreensão profunda do HTTP, idealmente na medida em que seja capaz de escrever sua própria implementação Java de um servidor HTTP multisegmentado com thread-pooling. Você também deve conhecer o comportamento de manutenção de atividade HTTP/1.1 e deve ter um conhecimento profundo das interações do servidor/cliente com JavaScript, especialmente o estilo assíncrono de interação representado pela AJAX.

Como o dinamismo da página e o conteúdo interativo são fundamentais para a experiência WM, é essencial que você tenha uma compreensão bastante profunda do Modelo de objeto de Documento e seu potencial para manipulação programática em resposta a eventos. Você deve ter algum conhecimento, por exemplo, de manipulação DOM em tempo real e comportamento de arrastar e soltar em vários documentos do navegador (por exemplo, usando iframes).

No nível mais alto, então, você deve ter uma sólida compreensão de:

* o protocolo [HTTP/1.1](https://www.ietf.org/rfc/rfc2616.txt)
* HTML (preferencialmente [HTML5](https://dev.w3.org/html5/spec/Overview.html))
* Folhas de estilos em cascata
* Linguagem de marcação extensível (XML)
* Padrões de design assíncronos do JavaScript e XML (AJAX)
* JSON (JavaScript Object Notation)
* o Modelo de objeto de Documento
* Interações com status e sem estado
* [Identificadores de recursos uniformes](https://www.ietf.org/rfc/rfc2396.txt)
* Cookies do navegador
* e outros conceitos modernos de desenvolvimento web

A pilha de tecnologia da Adobe Experience Manager é baseada no container OSGI [Apache Felix](https://felix.apache.org/) com a estrutura da Web [Apache Sling](https://sling.apache.org/site/index.html) e incorpora um Repositório de Conteúdo Java ([JCR](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html)) com base em [Apache Jackrabbit](https://jackrabbit.apache.org/jcr-api.html). Você deve se familiarizar com esses projetos individuais, bem como com quaisquer outros componentes de código aberto (por exemplo, Apache Lucene) usados na área em que você pretende contribuir.

## Conhecimento Tribal {#tribal-knowledge}

Alguns conceitos e princípios orientadores estão profundamente enraizados na antiga cultura do Dia. Esta seção lista algumas das questões &quot;profundamente embutidas pelo DNA&quot; de que você deve estar ciente.

### Tudo é Conteúdo {#everything-is-content}

O conteúdo inclui não apenas todos os dados que o aplicativo da Web persiste. O código do programa, bibliotecas, scripts, modelos, HTML, CSS, imagens e artefatos de todos os tipos, qualquer coisa e tudo é mantido no Repositório de conteúdo e importado/exportado na forma de pacotes por meio do Gerenciador de pacotes e Compartilhamento de pacotes.

### Modelo de David {#david-s-model}

A forma como o conteúdo deve ser modelado em um repositório de conteúdo Java requer uma forma de pensar totalmente diferente da prática comum no setor de software para modelagem de dados no mundo relacional. A leitura essencial para qualquer recém-chegado para gestão de conteúdo do caminho do JCR é [Modelo de David: Um guia para modelagem de conteúdo](https://wiki.apache.org/jackrabbit/DavidsModel).

### RESThance {#restfulness}

A abordagem REST está profundamente enraizada no que fazemos. Isso significa, entre outras coisas, evitar interações de estado e ter em mente que URIs são endereços definitivos para conteúdo e serviços.

REST (REpresentational State Transfer) refere-se ao estilo arquitetônico de software no qual se baseia a World Wide Web. Descreve os principais elementos que fazem com que a Web funcione, e assim fornece um conjunto de princípios para como o software baseado na Web deve ser projetado. Ao projetar uma API para ser usada na Web, faz sentido seguir essas &quot;práticas recomendadas&quot;.

Como REST fornece a filosofia orientadora por trás de tanto do que fazemos, você deve considerar essencial se tornar versado nos princípios do design RESTful. Um bom lugar para start é com a dissertação de Roy Fielding[.](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)

### Resolução de solicitação Sling {#sling-request-resolution}

Um aspecto essencial para entender sobre AEM é como as solicitações recebidas se relacionam ao comportamento do conteúdo e do aplicativo, como o conteúdo é estruturado no repositório de conteúdo e onde AEM procura a lógica do aplicativo para lidar com a solicitação. Saiba mais sobre o Apache [Sling URL decomposition](https://sling.apache.org/site/url-decomposition.html) e sobre a forma como ele aplica o estilo arquitetônico REST e suas restrições de sistema sem estado, acessíveis e em camadas.

Os aspectos principais para entender sobre a resolução de solicitação do Apache Sling são como as solicitações são mapeadas primariamente para um recurso específico no Repositório de conteúdo, como as propriedades adicionais da solicitação, juntamente com as propriedades desses objetos de conteúdo, determinam qual código de aplicativo será chamado para renderizar o conteúdo e como o código em /apps substitui o código em /libs.

### Início rápido {#quickstart}

Sem etapa três: Para instalar e executar, basta baixar e clicar no duplo no arquivo JAR Quickstart. Não há etapa três. Qualquer funcionalidade opcional adicional deve exigir apenas a instalação do pacote apropriado do Compartilhamento de pacotes.

Tamanho pequeno de Início Rápido: Mantenha o tamanho do arquivo JAR do Quickstart no mínimo. Faça uso inteligente e otimizado de bibliotecas, movendo a funcionalidade opcional para o compartilhamento de pacotes.

Tempo de inicialização mais rápido: Quando você fizer uma alteração que possa afetar o tempo de inicialização, verifique se ela ficará mais curta e não mais longa.

### Lean e Mean {#lean-and-mean}

Nós favorecemos o código e projetos que são leves, pequenos, rápidos e elegantes. &quot;Bons o suficiente&quot; não é bom o suficiente.

Reutilização de código: Nossa arquitetura de produto baseada no OSGi e a filosofia &quot;tudo é conteúdo&quot; significam que temos oportunidades excepcionais de reutilização de códigos e artefatos. Tentamos tirar proveito desse fato sempre que possível para manter os recursos magros e medianos.

Acoplamento com perda: Somos a favor de interações vagamente ligadas sobre dependências apertadas e &quot;intimidade indesejada&quot;. A união solta também permite mais reutilização do código.

### Não interromper o demo {#don-t-break-the-demo}

Familiarize-se com scripts de demonstração e funcionalidades de produtos que são mostrados com mais frequência nas demonstrações. Entenda que, no mínimo, nada que você faça deve quebrar um recurso de &quot;script de demonstração&quot;. O produto principal deve estar sempre pronto para demonstração, mesmo durante o desenvolvimento.

### Design para confiabilidade {#design-for-reliability}

Nós nos esforçamos para criar e codificar recursos de forma flexível, para que (por exemplo) um problema com um único elemento DOM não faça com que uma página inteira não seja renderizada. Por outras palavras: Faça coisas que devem ser fatais, fatais. Torne tudo mais sobrevivível. Faça o produto &quot;perdoar&quot;.

### Anormal é Novo Normal {#abnormal-is-the-new-normal}

Não dependa dos ganchos de desligamento, assegure a limpeza na inicialização. Terminação anormal é terminação normal.

`shutdown == kill -9 == power outage`

### Esteja pronto para o agrupamento elástico {#be-ready-for-elastic-clustering}

Esteja sempre pronto para o agrupamento elástico, sempre assuma que existe agrupamento. Como regra geral, respeitar tudo no repositório de conteúdo significa suporte a clusters incorporado.

### Design para compatibilidade com versões anteriores {#design-for-backward-compatibility}

Nada que você faça deve quebrar o código antigo de um cliente. Considere apenas `/libs` para conter o código do produto que pode ser atualizado durante uma atualização. A seção `/apps` do repositório é o código do projeto, e a seção `/etc` contém configurações personalizadas que precisam ser preservadas. Geralmente, não substitua nada em `/apps`, `/content` e `/home`. Após uma atualização, o código do projeto antigo, as configurações e o conteúdo devem continuar a funcionar como antes da atualização.

Projetar para compatibilidade com versões anteriores também garante que a experiência de atualização corresponda à simplicidade da instalação inicial. Basta parar o AEM, substituir o arquivo JAR do Quickstart e iniciar o AEM novamente deve ser suficiente. Com uma base de instalação em rápido crescimento, a eficiência da atualização será uma vantagem cada vez maior.

Embora as APIs existentes possam e devam ser marcadas como obsoletas quando mais recentes, a melhor funcionalidade as substitui, todas as APIs que foram tornadas públicas em uma versão 5.x anterior precisam permanecer funcionais, pois podem estar em uso no código de aplicativo personalizado. Essas APIs não devem ser removidas.

A compatibilidade com versões anteriores deve igualmente ser tida em conta no que respeita à coerência geral da estrutura do conteúdo e da experiência do utilizador.

## Conceitos principais {#core-concepts}

**Instância**  do autor - Normalmente, por motivos de segurança, controle e outros, um site de produção dividirá instâncias de AEM em instâncias de autor e publicação. Para obter mais informações sobre a arquitetura de implantação (incluindo instâncias de autor/publicação), consulte a documentação sobre instâncias AEM.

**Armazenamento em cache, fritura e assar**  - Tradicionalmente, os conceitos de cozinhar contra fritar são uma importante distinção entre os diferentes sistemas de Gestões de conteúdo da Web. No jargão CMS, &quot;baking&quot; refere-se ao conceito de envio de dados para arquivos estáticos em tempo de publicação, enquanto &quot;frying&quot; se refere ao conceito de processamento de dados para apresentação final em tempo de solicitação (ou seja, apenas em tempo).

**Cluster e balanceamento**  de carga - Para aumentar a disponibilidade e melhorar o desempenho de um ambiente de produção, é comum combinar várias instâncias de autor e/ou publicação (em clusters), disponibilizando-as para grupos diferentes de usuários ou balanceando a carga atrás de uma configuração do Dispatcher.

Também é possível combinar várias instâncias do repositório de conteúdo para criar uma *solução JCR de alta disponibilidade*, que pode ser integrada à sua solução AEM para maximizar a proteção contra falhas de hardware e software. Consulte [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) para obter mais informações.

**Componente**  - No AEM, um Componente é um tipo de objeto, cujas instâncias geralmente podem ser criadas arrastando-as e soltando-as, por exemplo, do Sidekick. Por exemplo, os componentes predefinidos fornecidos com AEM incluem os componentes Texto, Título, Tag Cloud, Carrossel, Imagem e Lista, todos disponíveis no Sidekick em tempo de execução.

**Localizador**  de conteúdo - No modo de criação, o Localizador de conteúdo é um painel especial (quadro) no lado esquerdo da página que, dependendo da guia selecionada na parte superior, exibe listas de imagens, documentos, ativos do Flash, páginas, parágrafos ou recursos do repositório que você pode arrastar e soltar do Localizador de conteúdo para a página em que está trabalhando (à direita).

**Ativos**  digitais - no AEM, os Ativos digitais são (normalmente) imagens e arquivos de mídia avançada. Para obter mais informações, consulte Trabalhar com ativos digitais no DAM.

**Dispatcher**  - O Dispatcher é uma ferramenta de cache e balanceamento de carga, além de fornecer certas salvaguardas de segurança.

**Widgets**  ExtJS - A maioria dos elementos da interface do usuário no AEM usam ExtJS, que é uma biblioteca de widget de terceiros escrita em JavaScript. O ExtJS possui widgets de interface de usuário personalizáveis de alto desempenho e um modelo de componente bem projetado e extensível.

**JCR, repositório**  de conteúdo Java - A especificação do repositório de conteúdo Java (JSR-283) fornece um modelo de dados abstrato e uma interface de programação de aplicativos para realizar um repositório de dados NoSQL massivamente escalável que combina recursos de um sistema de arquivos e um banco de dados de objetos. Embora você não precise entender o JSR-283 em detalhes exaustivos, você deve levar tempo para se familiarizar com os recursos básicos do JCR e o modelo de dados subjacente, pois o JCR é o que torna possível a filosofia &quot;tudo é conteúdo&quot; da AEM.

Essencialmente, o JCR é um sistema de nós e propriedades, no qual os nós podem herdar de outros nós e todo o conteúdo é armazenado como propriedade *values*. Observe que, além da herança normal, o JCR permite um conceito de nós &quot;mixin&quot;, que permite modelagem de várias heranças.

O JCR tem vários tipos de nó predefinidos e tipos de propriedade, mas em geral o sistema de digitação é bastante flexível e (na verdade) um dos pontos fortes do JCR é permitir que o conteúdo estruturado e não estruturado seja armazenado/gerenciado com a mesma facilidade. Ou seja, o JCR pode acomodar dados altamente estruturados, mas também pode acomodar estruturas de dados dinâmicas arbitrárias sem restrições de schema.

O JavaDoc para a API Java do JCR é [here](http://jackrabbit.apache.org/jcr/jcr-api.html).

Antes de tentar ler o JavaDoc ou a especificação do JCR em si, você pode consultar [essa explicação de alto nível](/help/sites-developing/the-basics.md#java-content-repository) do JCR conforme implementada pelo Adobe Experience Services.

**Multi-Site Manager (MSM)**  - O recurso MSM do AEM ajuda os clientes a lidar com conteúdo multilíngue e multinacional, permitindo que eles equilibrem a marca centralizada com conteúdo localizado.

**OSGi** - OSGi é a tecnologia de tempo de execução baseada em serviços que fornece a base para o desenvolvimento modularizado de Java em AEM. É uma estrutura que fornece não apenas um ambiente de execução e carregamento de classe altamente dinâmico (e seguro) para recursos de código (conhecidos como pacotes), mas também controle total sobre a visibilidade e o ciclo de vida dos vários serviços expostos pelos pacotes. Um registro de serviços fornece um modelo de cooperação para pacotes que leva em conta a dinâmica do ciclo de vida (e os requisitos de versão). O OSGi soluciona muitos dos problemas que os servidores de aplicativos pretendiam resolver, mas o faz de forma leve e altamente dinâmica, possibilitando, por exemplo, a implantação dinâmica de serviços (disponibilizando o novo código imediatamente sem reiniciar o servidor).

**Parsys, Sistema**  de parágrafo - O sistema de parágrafo (parsys) é um componente composto que permite aos autores adicionar componentes de tipos diferentes a uma página e contém outros componentes de parágrafo. Cada tipo de parágrafo é representado como um componente. O próprio sistema de parágrafo também é um componente, que contém os outros componentes de parágrafo.

**Microkernel**  - Cada espaço de trabalho no repositório pode ser configurado separadamente para armazenar seus dados por meio de um microkernel específico (uma classe que gerencia a leitura e a gravação dos dados). Da mesma forma, o repositório de versões em todo o repositório também pode ser configurado de forma independente para usar um determinado microkernel. Há vários microkernels diferentes disponíveis, capazes de armazenar dados em diversos formatos de arquivo ou bancos de dados relacionais. (Por exemplo, existem gerentes de persistência para MongoDB, DB2 ou Oracle) O microkernel padrão para AEM é TarMK (veja mais abaixo).

**Instância**  de publicação - Por motivos de segurança, controle e outros, um site de produção normalmente divide instâncias de AEM em instâncias de Autor e Publicação. Para obter mais informações sobre a arquitetura de implantação (incluindo instâncias de autor/publicação), consulte a documentação sobre instâncias AEM.

**Início rápido**  - Ao contrário de muitos outros programas, você instala AEM usando um único arquivo JAR autoextraível &quot;Início rápido&quot;. Ao clicar com o duplo no arquivo JAR pela primeira vez, tudo o que você precisa é instalado automaticamente. O JAR de início rápido inclui todos os arquivos necessários para o repositório CRX (incluindo instalações administrativas), serviços de repositório virtual, serviços de índice e pesquisa, serviços de fluxo de trabalho, segurança e um servidor Web, além do CQ Servlet Engine (CQSE) e todos os serviços AEM. Não há outros arquivos para instalar: o Início Rápido é autocontido.

Na primeira vez que você start o Quickstart, ele cria um repositório compatível com JCR inteiro em segundo plano, que pode levar vários minutos. Após essa inicialização inicial, as inicializações subsequentes são muito mais rápidas, já que a infraestrutura do repositório já foi estabelecida.

Muitas opções de inicialização (como o número da porta ativa e se a instância AEM em questão deve ser uma instância de Publicação versus uma instância de Autor; e muito mais) podem ser controlados com a renomeação apropriada do arquivo Quickstart. Para ver uma lista de opções a este respeito, execute o JAR com &quot;-help&quot; na linha de comando:

```shell
java -jar <quickstartfilename>.jar -help
```

**Agentes**  de replicação - Os agentes de replicação são fundamentais para AEM como mecanismo usado para publicar (ativar) conteúdo de um autor para um ambiente de publicação; liberar conteúdo do cache do Dispatcher; retornar conteúdo gerado pelo usuário (por exemplo, entrada de formulário) do ambiente Publicar para o ambiente Autor.

**Andaime**  - Com o andaime, você pode criar um formulário (um andaime) com campos que refletem a estrutura desejada para suas páginas e, em seguida, usar esse formulário para criar páginas facilmente com base nessa estrutura.

**Segmentação**  - os visitantes do site têm interesses e objetivos diferentes quando chegam a um site. Compreender as metas dos visitantes e atender às suas expectativas é um pré-requisito importante para o sucesso do marketing online. A segmentação ajuda a alcançar isso ao analisar e caracterizar os detalhes de um visitante.

**Sidekick**  - O Sidekick é uma janela flutuante semelhante à paleta que aparece na página editável, da qual novos componentes podem ser arrastados e as ações que se aplicam à página podem ser executadas.

**Site Catalyst**  - O SiteCatalyst fornece aos comerciantes um único local para medir, analisar e otimizar dados integrados de todas as iniciativas online em vários canais de marketing. Você pode usar o Adobe SiteCatalyst para analisar dados de sites AEM.

**Armazenamento Tar (TarMK)**  - TarMK é o sistema de persistência padrão no AEM. Embora AEM possa ser configurado para usar um sistema de persistência diferente (como o MongoDB), o TarMK tem certas vantagens, já que ele é otimizado para desempenho para casos de uso típicos do JCR (portanto, é muito rápido), usa um formato de dados padrão do setor e pode ser feito backup rápido e fácil.

**Modelo**  - Em AEM, um Modelo especifica um tipo específico de página. Ela define a estrutura de uma página (ao mesmo tempo que também especifica uma imagem em miniatura e várias propriedades). Por exemplo, você pode ter modelos separados para páginas de produtos, mapas de sites e informações de contato.

**Fluxo de trabalho**  - O sistema de Fluxo de trabalho AEM permite a criação de processos automatizados envolvendo páginas ou ativos.
