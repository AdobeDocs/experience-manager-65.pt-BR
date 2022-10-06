---
title: AEM Conceitos principais
seo-title: The Basics
description: Uma visão geral dos conceitos principais de como o AEM é estruturado e como desenvolvê-lo, incluindo a compreensão do JCR, Sling, OSGi, o dispatcher, os workflows e o MSM
seo-description: An overview of the core concepts of how AEM is structured and how to develop on top of it including understanding the JCR, Sling, OSGi, the dispatcher, workflows, and MSM
uuid: e49f29db-a5d6-48a0-af32-f8785156746e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6e913190-be92-4862-a8b9-517f8bde0044
exl-id: f6f32290-422e-4037-89d8-d9f414332e8e
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '3334'
ht-degree: 1%

---

# AEM Conceitos principais {#aem-core-concepts}

>[!NOTE]
>
>Antes de mergulhar nos conceitos principais de AEM, o Adobe recomenda concluir o tutorial WKND na [Introdução ao desenvolvimento do AEM Sites](/help/sites-developing/getting-started.md) documento para obter uma visão geral do processo de desenvolvimento de AEM e introdução aos conceitos principais.

## Pré-requisitos para desenvolvimento em AEM {#prerequisites-for-developing-on-aem}

Você precisará das seguintes habilidades para desenvolver no AEM:

* Conhecimento básico das técnicas de aplicação Web, incluindo:

   * o ciclo request-response (XMLHttpRequest / XMLHttpResponse)
   * HTML
   * CSS
   * JavaScript

* Conhecimento prático do Experience Server (CRX), incluindo o Content Explorer
* Para desenvolvimento na interface clássica, também é necessário o conhecimento básico de JSP (JavaServer Pages), incluindo a capacidade de entender e modificar exemplos simples de JSP.

Também é recomendável ler e seguir o [Diretrizes e práticas recomendadas](/help/sites-developing/dev-guidelines-bestpractices.md).

## Repositório de conteúdo Java {#java-content-repository}

O padrão Java Content Repository (JCR), [JSR 283](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html), especifica uma maneira independente de fornecedor e de implementação para acessar o conteúdo de forma bidirecional em um nível granular em um repositório de conteúdo.

O chumbo da especificação é detido pela Adobe Research (Suíça) AG.

O [API JCR 2.0](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html) pacote, javax.jcr.&amp;ast; é usada para acesso direto e manipulação do conteúdo do repositório.

## Experience Server (CRX) e Jackrabbit {#experience-server-crx-and-jackrabbit}

O Experience Server fornece os Experience Services, que AEM são criados e que podem ser aproveitados para criar aplicativos personalizados, e incorpora o Repositório de Conteúdo com base no Jackrabbit.

[Apache Jackrabbit](https://jackrabbit.apache.org/) é uma implementação de código aberto, totalmente em conformidade com a API 2.0 do JCR.

## Processamento de solicitação Sling {#sling-request-processing}

### Introdução ao Sling {#introduction-to-sling}

AEM é criado usando [Sling](https://sling.apache.org/site/index.html), uma estrutura de aplicação web baseada em princípios REST que fornece fácil desenvolvimento de aplicativos orientados a conteúdo. O Sling usa um repositório JCR, como Apache Jackrabbit, ou, no caso de AEM, o Repositório de Conteúdo CRX, como seu armazenamento de dados. O Sling tem contribuído para a Apache Software Foundation - mais informações podem ser encontradas no Apache.

Usando o Sling, o tipo de conteúdo a ser renderizado não é a primeira consideração de processamento. Em vez disso, a principal consideração é se o URL resolve um objeto de conteúdo para o qual um script pode ser encontrado para executar a renderização. Isso oferece excelente suporte para autores de conteúdo da Web criarem páginas que são facilmente personalizadas para suas necessidades.

As vantagens dessa flexibilidade são visíveis em aplicativos com uma grande variedade de elementos de conteúdo diferentes, ou quando você precisa de páginas que possam ser facilmente personalizadas. Em particular, ao implementar um sistema de Gerenciamento de conteúdo da Web, como o WCM na solução de AEM.

Consulte [Discover Sling em 15 minutos](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) para os primeiros passos para o desenvolvimento com o Sling.

O diagrama a seguir explica a resolução do script Sling: ele mostra como obter da solicitação HTTP para o nó de conteúdo, do nó de conteúdo para o tipo de recurso, do tipo de recurso para o script e quais variáveis de script estão disponíveis.

![Noções básicas sobre a resolução do script Apache Sling](assets/sling-cheatsheet-01.png)

O diagrama a seguir explica todos os parâmetros de solicitação ocultos, mas poderosos, que você pode usar ao lidar com o SlingPostServlet, o manipulador padrão para todas as solicitações do POST que oferece opções infinitas para criar, modificar, excluir, copiar e mover nós no repositório.

![Uso do SlingPostServlet](assets/sling-cheatsheet-02.png)

### O Sling é centrado no conteúdo {#sling-is-content-centric}

O Sling é *centrado no conteúdo*. Isso significa que o processamento está focado no conteúdo, já que cada solicitação (HTTP) é mapeada no conteúdo na forma de um recurso JCR (um nó de repositório):

* o primeiro target é o recurso (nó JCR) que contém o conteúdo
* em segundo lugar, a representação, ou script, está localizada nas propriedades do recurso em combinação com determinadas partes da solicitação (por exemplo, seletores e/ou a extensão)

### Sling RESTful {#restful-sling}

Devido à filosofia centrada no conteúdo, o Sling implementa um servidor orientado por REST e, portanto, apresenta um novo conceito em estruturas de aplicativos Web. As vantagens são:

* Muito RESTful, não apenas à superfície; recursos e representações são modelados corretamente no servidor
* remove um ou mais modelos de dados

   * anteriormente, as seguintes condições eram necessárias: Estrutura de URL, objetos de negócios, esquema de banco de dados;
   * isso agora está reduzido a: URL = recurso = estrutura JCR

### Decomposição de URL {#url-decomposition}

No Sling, o processamento é orientado pelo URL da solicitação do usuário. Isso define o conteúdo a ser exibido pelos scripts apropriados. Para fazer isso, as informações são extraídas do URL.

Se analisarmos o seguinte URL:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Podemos dividi-lo em suas partes compósitas:

| protocolo | host | caminho do conteúdo | seletor(s) | extensão |  | sufixo |  | param(s) |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | ferramentas/espião | .printable.a4. | html | / | a/b | ? | x=12 |

**protocolo** HTTP

**host** Nome do site.

**caminho do conteúdo** Caminho que especifica o conteúdo a ser renderizado. É usado em combinação com a extensão; neste exemplo, eles traduzem para tools/spy.html.

**seletor(s)** Usado para métodos alternativos de renderização do conteúdo; neste exemplo, uma versão compatível com a impressora no formato A4.

**extensão** Formato do conteúdo; especifica também o script a ser usado para renderização.

**sufixo** Pode ser usado para especificar informações adicionais.

**param(s)** Quaisquer parâmetros necessários para o conteúdo dinâmico.

#### Do URL para conteúdo e scripts {#from-url-to-content-and-scripts}

Usando estes princípios:

* o mapeamento usa o caminho de conteúdo extraído da solicitação para localizar o recurso
* quando o recurso apropriado está localizado, o tipo de recurso sling é extraído e usado para localizar o script a ser usado para renderizar o conteúdo

A figura abaixo ilustra o mecanismo utilizado, que será discutido mais detalhadamente nas seções seguintes.

![chlimage_1-86](assets/chlimage_1-86a.png)

Com o Sling, você especifica qual script renderiza uma determinada entidade (definindo a variável `sling:resourceType` no nó JCR). Esse mecanismo oferece mais liberdade do que uma em que o script acessa as entidades de dados (como uma instrução SQL em um script PHP faria), pois um recurso pode ter várias representações.

#### Mapeamento de solicitações para recursos {#mapping-requests-to-resources}

O pedido é dividido e as informações necessárias são extraídas. O repositório é pesquisado pelo recurso solicitado (nó de conteúdo):

* O primeiro Sling verifica se há um nó no local especificado na solicitação; por exemplo `../content/corporate/jobs/developer.html`
* se nenhum nó for encontrado, a extensão será removida e a pesquisa será repetida; por exemplo `../content/corporate/jobs/developer`
* se nenhum nó for encontrado, o Sling retornará o código http 404 (Não encontrado).

O Sling também permite que outras coisas além dos nós JCR sejam recursos, mas esse é um recurso avançado.

### Localização do script {#locating-the-script}

Quando o recurso apropriado (nó de conteúdo) estiver localizado, a variável **tipo de recurso sling** é extraído. Este é um caminho, que localiza o script a ser usado para renderizar o conteúdo.

O caminho especificado pela variável `sling:resourceType` pode ser:

* absoluto
* relativo, para um parâmetro de configuração

   Os caminhos relativos são recomendados pelo Adobe, pois aumentam a portabilidade.

Todos os scripts Sling são armazenados em subpastas de `/apps` ou `/libs`, que será pesquisado nesta ordem (consulte [Personalização de componentes e outros elementos](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

Alguns outros pontos são:

* quando o Método (GET, POST) é necessário, ele será especificado em maiúsculas de acordo com a especificação HTTP, por exemplo, jobs.POST.esp (veja abaixo)
* vários mecanismos de script são compatíveis:

   * HTL (Linguagem de modelo de HTML - Sistema de modelo preferencial e recomendado da Adobe Experience Manager para o HTML): `.html`
   * Páginas ECMAScript (JavaScript) (execução no lado do servidor): `.esp, .ecma`
   * Páginas do servidor Java (execução do lado do servidor): `.jsp`
   * Compilador de Servlet Java (execução do lado do servidor): `.java`
   * Templates JavaScript (execução no lado do cliente): `.jst`

A lista de mecanismos de script compatíveis com a instância específica de AEM é listada no Console de Gerenciamento do Felix ( `http://<host>:<port>/system/console/slingscripting`).

Além disso, o Apache Sling oferece suporte à integração com outros mecanismos de script populares (por exemplo, Groovy, JRuby, Freemarker) e fornece uma maneira de integrar novos mecanismos de script.

Usando o exemplo acima, se a variável `sling:resourceType` é `hr/jobs` em seguida para:

* Solicitações de GET/HEAD e URLs que terminam em .html (tipos de solicitação padrão, formato padrão)

   O script será /apps/hr/jobs/jobs.esp; a última seção do sling:resourceType forma o nome do arquivo.

* Solicitações de POST (todos os tipos de solicitação exceto GET/HEAD, o nome do método deve estar em maiúsculas)

   POST será usado no nome do script.

   O script será `/apps/hr/jobs/jobs.POST.esp`.

* URLs em outros formatos, sem terminar com .html

   Por exemplo `../content/corporate/jobs/developer.pdf`

   O script será `/apps/hr/jobs/jobs.pdf.esp`; o sufixo é adicionado ao nome do script.

* URLs com seletores

   Os seletores podem ser usados para exibir o mesmo conteúdo em um formato alternativo. Por exemplo, uma versão amigável para a impressora, um feed rss ou um resumo.

   Se observarmos uma versão amigável da impressora, onde o seletor pode ser *print*; como em `../content/corporate/jobs/developer.print.html`

   O script será `/apps/hr/jobs/jobs.print.esp`; o seletor é adicionado ao nome do script.

* Se nenhum sling:resourceType tiver sido definido, então:

   * o caminho do conteúdo será usado para procurar um script apropriado (se o ResourceTypeProvider baseado no caminho estiver ativo).

      Por exemplo, o script para `../content/corporate/jobs/developer.html` geraria uma pesquisa em `/apps/content/corporate/jobs/`.

   * o tipo de nó primário será usado.

* Se nenhum script for encontrado, o script padrão será usado.

   A representação padrão é suportada atualmente como texto sem formatação (.txt), HTML (.html) e JSON (.json), e todos listarão as propriedades do nó (devidamente formatado). A representação padrão da extensão .res, ou solicitações sem uma extensão de solicitação, é spool do recurso (quando possível).
* Para tratamento de erros http (códigos 403 ou 404), o Sling procurará um script em:

   * o local /apps/sling/servlet/errorhandler para [scripts personalizados](/help/sites-developing/customizing-errorhandler-pages.md)
   * ou o local dos scripts padrão /libs/sling/servlet/errorhandler/403.esp, ou 404.esp, respectivamente.

Se vários scripts se aplicarem a uma determinada solicitação, o script com a melhor correspondência será selecionado. Quanto mais específico for o jogo, melhor será; em outras palavras, quanto mais seletor corresponder melhor, independentemente de qualquer extensão de solicitação ou correspondência de nome de método.

Por exemplo, considere uma solicitação para acessar o recurso
`/content/corporate/jobs/developer.print.a4.html`
de tipo
`sling:resourceType="hr/jobs"`

Supondo que tenhamos a seguinte lista de scripts no local correto:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Em seguida, a ordem de preferência seria (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Além dos tipos de recursos (definidos principalmente pela variável `sling:resourceType` (propriedade) também há o super tipo de recurso. Isso geralmente é indicado pela variável `sling:resourceSuperType` propriedade. Esses supertipos também são considerados ao tentar encontrar um script. A vantagem dos supertipos de recursos é que eles podem formar uma hierarquia de recursos em que o tipo de recurso padrão `sling/servlet/default` (usado pelos servlets padrão) é efetivamente a raiz.

O supertipo de recurso de um recurso pode ser definido de duas formas:

* pela `sling:resourceSuperType` propriedade do recurso.
* pela `sling:resourceSuperType` propriedade do nó para o qual `sling:resourceType` pontos.

Por exemplo:

* /

   * uma sessão gerenciada no quadro branco
   * b

      * sling:resourceSuperType = a
   * c

      * sling:resourceSuperType = b
   * x

      * sling:resourceType = c
   * y

      * sling:resourceType = c
      * sling:resourceSuperType = a




A hierarquia do tipo de:

* `/x`
   * é `[ c, b, a, <default>]`
* para `/y`
   * a hierarquia é `[ c, a, <default>]`

Isso ocorre porque `/y` tem `sling:resourceSuperType` propriedade `/x` não o faz e, portanto, seu supertipo é retirado de seu tipo de recurso.

#### Scripts Sling não podem ser chamados diretamente {#sling-scripts-cannot-be-called-directly}

No Sling, os scripts não podem ser chamados diretamente, pois isso quebraria o conceito restrito de um servidor REST; você misturaria recursos e representações.

Se você chamar a representação (o script) diretamente, oculta o recurso dentro do script, de modo que a estrutura (Sling) não saiba mais sobre ela. Assim, você perde determinados recursos:

* tratamento automático de métodos http diferentes do GET, incluindo:

   * POST, PUT, DELETE, que são manipulados com uma implementação padrão do sling
   * o `POST.jsp` script no local sling:resourceType

* sua arquitetura de código não é mais tão limpa ou tão claramente estruturada quanto deveria ser; de importância primordial para o desenvolvimento em larga escala

### API Sling {#sling-api}

Isso usa o pacote da API do Sling, org.apache.sling.&amp;ast; e bibliotecas de tags.

### Referência a elementos existentes usando sling:include {#referencing-existing-elements-using-sling-include}

Uma consideração final é a necessidade de fazer referência a elementos existentes nos scripts.

Scripts mais complexos (agregação de scripts) podem precisar acessar vários recursos (por exemplo, navegação, barra lateral, rodapé, elementos de uma lista) e fazer isso incluindo a variável *recurso*.

Para fazer isso, você pode usar o sling:include(&quot;/&lt;path>/&lt;resource>&quot;). Isso incluirá efetivamente a definição do recurso referenciado, como na declaração a seguir, que faz referência a uma definição existente para a renderização de imagens:

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

O OSGi define uma arquitetura para o desenvolvimento e implantação de aplicativos e bibliotecas modulares (também conhecida como Dynamic Module System for Java). Os contêineres OSGi permitem dividir o aplicativo em módulos individuais (são arquivos jar com informações meta adicionais e chamados de pacotes na terminologia OSGi) e gerenciar as dependências cruzadas entre eles com:

* serviços implementados no contêiner
* um contrato entre o contêiner e seu aplicativo

Esses serviços e contratos fornecem uma arquitetura que permite que elementos individuais se descubram dinamicamente para colaboração.

Em seguida, uma estrutura OSGi oferece carregamento/descarregamento dinâmico, configuração e controle desses pacotes, sem a necessidade de reinicializações.

>[!NOTE]
>
>Informações completas sobre a tecnologia OSGi podem ser encontradas no site [Site do OSGi](https://www.osgi.org).
>
>Em particular, a página de Educação Básica contém uma coleção de apresentações e tutoriais.

Essa arquitetura permite estender o Sling com módulos específicos de aplicativo. O Sling e, portanto, o CQ5 usam o [Apache Felix](https://felix.apache.org/) implementação de OSGI (iniciativa de gateway de serviços abertos) e é baseada nas Especificações OSGi Service Platform Versão 4.2. Ambos são coleções de pacotes OSGi executados em uma estrutura OSGi.

Isso permite executar as seguintes ações em qualquer um dos pacotes da instalação:

* instalar
* start
* stop
* atualizar
* desinstalar
* consulte o status atual
* acesse informações mais detalhadas (por exemplo, nome simbólico, versão, localização, etc.) sobre os pacotes específicos

Consulte [o Console da Web](/help/sites-deploying/web-console.md), [Configuração OSGI](/help/sites-deploying/configuring-osgi.md) e [Configurações do OSGi](/help/sites-deploying/osgi-configuration-settings.md) para obter mais informações.

## Objetos de desenvolvimento no ambiente de AEM {#development-objects-in-the-aem-environment}

São de interesse para o desenvolvimento:

**Item** Um item é um nó ou uma propriedade.

Para obter informações detalhadas sobre como manipular objetos Item, consulte o [Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) da interface javax.jcr.Item

**Nó (e suas propriedades)** Os nós e suas propriedades são definidos na especificação JCR API 2.0 (JSR 283). Eles armazenam conteúdo, definições de objeto, scripts de renderização e outros dados.

Os nós definem a estrutura do conteúdo e suas propriedades armazenam o conteúdo e os metadados reais.

Os nós de conteúdo direcionam a renderização. O Sling obtém o nó de conteúdo da solicitação de entrada. A propriedade sling:resourceType desse nó aponta para o componente de renderização do Sling a ser usado.

Um nó, que é um nome JCR, também é chamado de recurso no ambiente Sling.

Por exemplo, para obter as propriedades do nó atual, é possível usar o seguinte código no script:

`PropertyIterator properties = currentNode.getProperties();`

Com currentNode sendo o objeto de nó atual.

Para obter mais informações sobre como manipular objetos de Nó, consulte o [Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html).

**Widget** AEM todas as entradas de usuários são gerenciadas por widgets. Geralmente, eles são usados para controlar a edição de um conteúdo.

As caixas de diálogo são criadas combinando widgets.

AEM foi desenvolvido usando a biblioteca ExtJS de widgets.

**Diálogo** Uma caixa de diálogo é um tipo especial de widget.

Para editar conteúdo, AEM usa caixas de diálogo definidas pelo desenvolvedor do aplicativo. Eles combinam uma série de widgets para apresentar ao usuário todos os campos e ações necessários para editar o conteúdo relacionado.

As caixas de diálogo também são usadas para editar metadados e por várias ferramentas administrativas.

**Componente** Um componente de software é um elemento de sistema que oferece um serviço ou evento predefinido e é capaz de se comunicar com outros componentes.

No AEM, um componente é frequentemente usado para renderizar o conteúdo de um recurso. Quando o recurso é uma página, a renderização do componente é chamada de um Componente de nível superior ou um Componente de página. No entanto, um componente não precisa renderizar o conteúdo nem estar vinculado a um recurso específico; por exemplo, um componente de navegação exibirá informações sobre vários recursos.

A definição de um componente inclui:,

* o código usado para renderizar o conteúdo
* uma caixa de diálogo para a entrada do usuário e a configuração do conteúdo resultante.

**Modelo** Um modelo é a base para um tipo específico de página. Ao criar uma página na guia Sites , o usuário precisa selecionar um modelo. A nova página é então criada copiando esse modelo.

Um modelo é uma hierarquia de nós que tem a mesma estrutura que a página a ser criada, mas sem nenhum conteúdo real.

Ela define o componente de página usado para renderizar a página e o conteúdo padrão (conteúdo primário de nível superior). O conteúdo define como ele é renderizado como AEM centrado no conteúdo.

**Componente de página (componente de nível superior)** O componente a ser usado para renderizar a página.

**Página** Uma página é uma &quot;instância&quot; de um modelo.

Uma página tem um nó de hierarquia do tipo cq:Page e um nó de conteúdo do tipo cq:PageContent. A propriedade sling:resourceType do nó de conteúdo aponta para o Componente de página usado para renderizar a página.

Por exemplo, para obter o nome da página atual, é possível usar o seguinte código no script:

S`tring pageName = currentPage.getName();`

Com currentPage sendo o objeto de página atual. Para obter mais informações sobre como manipular objetos Page , consulte o [Javadocs](https://helpx.adobe.com/br/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html).

**Gerenciador de página** O gerenciador de página é uma interface que fornece métodos para operações no nível da página.

Por exemplo, para obter a página que contém um recurso, é possível usar o seguinte código no script:

Página myPage = pageManager.getContainsPage(myResource);

Com o pageManager sendo o objeto do gerenciador de páginas e myResource um objeto de recurso. Para obter mais informações sobre os métodos fornecidos pelo gerenciador de páginas, consulte o [Javadocs](https://helpx.adobe.com/br/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html).

## Estrutura no Repositório {#structure-within-the-repository}

A lista a seguir fornece uma visão geral da estrutura que será exibida no repositório.

>[!CAUTION]
>
>As alterações nessa estrutura, ou nos arquivos dentro dela, devem ser feitas com cuidado.
>
>As alterações são necessárias durante o desenvolvimento, mas você deve tomar cuidado para compreender totalmente as implicações de quaisquer alterações feitas.

>[!CAUTION]
>
>Você não deve alterar nada na variável `/libs` caminho. Para configuração e outras alterações, copie o item de `/libs` para `/apps` e fazer quaisquer alterações no `/apps`.

* `/apps`

   Aplicativo relacionado; O inclui definições de componentes específicas para o seu site. Os componentes desenvolvidos podem ser baseados nos componentes prontos para uso disponíveis em `/libs/foundation/components`.

* `/content`

   Conteúdo criado para o seu site.

* `/etc`

* `/home`

   Informações do usuário e do grupo.

* `/libs`

   Bibliotecas e definições que pertencem ao núcleo da AEM. As subpastas em `/libs` representam os recursos AEM prontos para uso como, por exemplo, pesquisa ou replicação. O conteúdo em `/libs` não deve ser modificado, pois afeta a maneira como AEM funciona. Os recursos específicos do seu site devem ser desenvolvidos em `/apps` (consulte [Personalização de componentes e outros elementos](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

* `/tmp`

   Área de trabalho temporária.

* `/var`

   Arquivos que mudam e são atualizados pelo sistema; como logs de auditoria, estatísticas, tratamento de eventos.

## Ambientes {#environments}

Com AEM, um ambiente de produção geralmente consiste em dois tipos diferentes de instâncias: um [Instâncias de autor e publicação](/help/sites-deploying/deploy.md#author-and-publish-installs).

## O Dispatcher {#the-dispatcher}

O Dispatcher é uma ferramenta Adobe para armazenamento em cache e/ou balanceamento de carga. Para mais informações, consultar o ponto [o Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html).

## FileVault (sistema de revisão de origem) {#filevault-source-revision-system}

O FileVault fornece o repositório JCR com mapeamento do sistema de arquivos e controle de versão. Ele pode ser usado para gerenciar projetos de desenvolvimento AEM com suporte total para armazenamento e controle de versão de código do projeto, conteúdo, configurações e assim por diante, em sistemas de controle de versão padrão (por exemplo, Subversão).

Consulte a [Ferramenta FileVault](/help/sites-developing/ht-vlttool.md) documentação para obter informações detalhadas.

## Fluxos de trabalhos {#workflows}

O conteúdo geralmente está sujeito a processos organizacionais, incluindo etapas como aprovação e aprovação por vários participantes. Esses processos podem ser representados como fluxos de trabalho, [definido e desenvolvido no AEM](/help/sites-developing/workflows-models.md), em seguida, aplicada ao [páginas de conteúdo apropriadas](/help/sites-administering/workflows.md) ou [ativos digitais](/help/assets/assets-workflow.md) conforme necessário.

O Mecanismo de fluxo de trabalho é usado para gerenciar a implementação dos fluxos de trabalho e seu aplicativo subsequente para o conteúdo.

## Gerenciamento de vários sites {#multi-site-management}

O Multi Site Manager (MSM) permite que você gerencie facilmente vários sites que compartilham conteúdo comum. O MSM permite definir relações entre os sites, de modo que as alterações de conteúdo em um site sejam replicadas automaticamente em outros sites.

Por exemplo, os sites geralmente são fornecidos em vários idiomas para públicos internacionais. Quando o número de sites no mesmo idioma é baixo (de três a cinco), é possível um processo manual para sincronizar o conteúdo entre sites. No entanto, assim que o número de sites aumentar ou quando vários idiomas estiverem envolvidos, torna-se mais eficiente automatizar o processo.

* Gerencie com eficiência diferentes versões de idiomas de um site.
* Atualizar automaticamente um ou mais sites com base em um site de origem:

   * Imponha uma estrutura básica comum e use conteúdo comum em vários sites.
   * Maximize o uso dos recursos disponíveis.
   * Mantenha uma aparência comum.
   * Concentre esforços no gerenciamento do conteúdo que difere entre os sites.

Para obter mais informações, consulte [Gerenciador de vários sites](/help/sites-administering/msm.md).
