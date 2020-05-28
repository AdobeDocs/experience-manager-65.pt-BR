---
title: Conceitos principais do AEM
seo-title: Noções básicas
description: Uma visão geral dos conceitos principais de como o AEM está estruturado e como desenvolvê-lo, incluindo a compreensão do JCR, Sling, OSGi, o dispatcher, workflows e MSM
seo-description: Uma visão geral dos conceitos principais de como o AEM está estruturado e como desenvolvê-lo, incluindo a compreensão do JCR, Sling, OSGi, o dispatcher, workflows e MSM
uuid: e49f29db-a5d6-48a0-af32-f8785156746e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6e913190-be92-4862-a8b9-517f8bde0044
translation-type: tm+mt
source-git-commit: fc09ba6cb923d9ea25ec14af093d7f86a4835d85
workflow-type: tm+mt
source-wordcount: '3365'
ht-degree: 0%

---


# Conceitos principais do AEM {#aem-core-concepts}

>[!NOTE]
>
>Antes de acessar os conceitos principais do AEM, a Adobe recomenda concluir o tutorial da WKND no documento [Introdução ao desenvolvimento do AEM Sites](/help/sites-developing/getting-started.md) para obter uma visão geral do processo de desenvolvimento do AEM e introdução aos conceitos principais.

## Pré-requisitos para o desenvolvimento no AEM {#prerequisites-for-developing-on-aem}

Você precisará das seguintes habilidades para desenvolver no AEM:

* Conhecimento básico das técnicas de aplicação web, incluindo:

   * o ciclo request -response (XMLHttpRequest / XMLHttpResponse)
   * HTML
   * CSS
   * JavaScript

* Conhecimento prático do Experience Server (CRX), incluindo o Content Explorer
* Para desenvolver na interface clássica, também é necessário o conhecimento básico do JSP (JavaServer Pages), incluindo a capacidade de entender e modificar exemplos simples de JSP.

Também é recomendável ler e seguir as [Diretrizes e Práticas recomendadas](/help/sites-developing/dev-guidelines-bestpractices.md).

## Repositório de conteúdo Java {#java-content-repository}

O padrão Java Content Repository (JCR), [JSR 283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html), especifica uma maneira independente do fornecedor e de implementação para acessar o conteúdo de forma bidirecional em um nível granular em um repositório de conteúdo.

O guia de especificação é detido pela Adobe Research (Suíça) AG.

O pacote [JCR API 2.0](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html) , javax.jcr.&amp;ast; é usada para acesso direto e manipulação do conteúdo do repositório.

## Experience Server (CRX) e Jackrabbit {#experience-server-crx-and-jackrabbit}

O Experience Server fornece os Experience Services nos quais o AEM é criado e que podem ser aproveitados para criar aplicativos personalizados, além de incorporar o Repositório de conteúdo baseado no Jackrabbit.

[Apache Jackrabbit](https://jackrabbit.apache.org/) é uma implementação de código aberto, totalmente em conformidade, da API JCR 2.0.

## Processamento de solicitação Sling {#sling-request-processing}

### Introdução ao Sling {#introduction-to-sling}

O AEM é criado usando o [Sling](https://sling.apache.org/site/index.html), uma estrutura de Aplicação web baseada em princípios REST que oferece fácil desenvolvimento de aplicativos orientados a conteúdo. O Sling usa um repositório JCR, como o Apache Jackrabbit, ou, no caso do AEM, o repositório de conteúdo CRX, como seu armazenamento de dados. A Sling contribuiu para a Apache Software Foundation - mais informações estão disponíveis no Apache.

Usando o Sling, o tipo de conteúdo a ser renderizado não é a primeira consideração de processamento. Em vez disso, a principal consideração é se o URL é resolvido para um objeto de conteúdo para o qual um script pode ser encontrado para executar a renderização. Isso oferece excelente suporte para autores de conteúdo da Web para criar páginas que são facilmente personalizadas para suas necessidades.

As vantagens dessa flexibilidade são evidentes em aplicativos com uma grande variedade de elementos de conteúdo diferentes, ou quando você precisa de páginas que possam ser facilmente personalizadas. Especificamente, ao implementar um sistema de Gestão de conteúdo da Web, como o WCM na solução AEM.

Consulte [Discover Sling em 15 minutos](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) para obter os primeiros passos para o desenvolvimento com o Sling.

O diagrama a seguir explica a resolução do script Sling: ele mostra como obter da solicitação HTTP para o nó de conteúdo, do nó de conteúdo para o tipo de recurso, do tipo de recurso para o script e quais variáveis de script estão disponíveis.

![chlimage_1-84](assets/chlimage_1-97.png)

O diagrama a seguir explica todos os parâmetros de solicitação ocultos, mas poderosos, que você pode usar ao lidar com o SlingPostServlet, o manipulador padrão para todas as solicitações POST que oferece opções intermináveis para criar, modificar, excluir, copiar e mover nós no repositório.

![chlimage_1-85](assets/chlimage_1-98.png)

### Sling é centrado no conteúdo {#sling-is-content-centric}

O Sling é centrado no *conteúdo*. Isso significa que o processamento está focado no conteúdo, já que cada solicitação (HTTP) está mapeada para o conteúdo na forma de um recurso JCR (um nó de repositório):

* o primeiro público alvo é o recurso (nó JCR) que contém o conteúdo
* em segundo lugar, a representação, ou o script, está localizado nas propriedades do recurso em combinação com certas partes da solicitação (por exemplo, seletores e/ou a extensão)

### Sling RESTful {#restful-sling}

Devido à filosofia centrada no conteúdo, o Sling implementa um servidor orientado a REST e, portanto, apresenta um novo conceito em estruturas de aplicativos da Web. As vantagens são:

* Muito RESTful, não apenas na superfície; recursos e representações são modelados corretamente dentro do servidor
* remove um ou mais modelos de dados

   * anteriormente, eram necessários: Estrutura de URL, objetos de negócios, schema DB;
   * isso agora se reduz a: URL = recurso = estrutura JCR

### Decomposição de URL {#url-decomposition}

No Sling, o processamento é conduzido pelo URL da solicitação do usuário. Isso define o conteúdo a ser exibido pelos scripts apropriados. Para fazer isso, as informações são extraídas do URL.

Se analisarmos o seguinte URL:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Podemos dividi-lo em suas partes compostas:

| protocolo | host | caminho do conteúdo | seletor(s) | extensão |  | sufixo |  | param(s) |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | ferramentas/espião | .printable.a4. | html | / | a/b | ? | x=12 |

**protocolo** HTTP

**nome do host** do site.

**caminho** do conteúdo Caminho que especifica o conteúdo a ser renderizado. É utilizado em combinação com a extensão; neste exemplo, eles traduzem para tools/spy.html.

**Seletor(s)** usado(s) para métodos alternativos de renderização do conteúdo; neste exemplo, uma versão compatível com a impressora em formato A4.

**Formato de extensão** do conteúdo; especifica também o script a ser usado para renderização.

**sufixo** Pode ser usado para especificar informações adicionais.

**param(s)** Quaisquer parâmetros necessários para o conteúdo dinâmico.

#### Do URL ao conteúdo e scripts {#from-url-to-content-and-scripts}

Usando estes princípios:

* o mapeamento usa o caminho de conteúdo extraído da solicitação para localizar o recurso
* quando o recurso apropriado está localizado, o tipo de recurso sling é extraído e usado para localizar o script a ser usado para renderizar o conteúdo

A figura abaixo ilustra o mecanismo utilizado, que será discutido mais pormenorizadamente nas seções seguintes.

![chlimage_1-86](assets/chlimage_1-86a.png)

Com Sling, você especifica qual script renderiza uma determinada entidade (definindo a `sling:resourceType` propriedade no nó JCR). Esse mecanismo oferta mais liberdade do que uma em que o script acessa as entidades de dados (como uma instrução SQL em um script PHP faria), pois um recurso pode ter várias execuções.

#### Mapeamento de solicitações para recursos {#mapping-requests-to-resources}

O pedido é discriminado e as informações necessárias são extraídas. O repositório é pesquisado pelo recurso solicitado (nó de conteúdo):

* O primeiro Sling verifica se existe um nó no local especificado na solicitação; por exemplo, `../content/corporate/jobs/developer.html`
* se nenhum nó for encontrado, a extensão será ignorada e a pesquisa repetida; por exemplo, `../content/corporate/jobs/developer`
* se nenhum nó for encontrado, o Sling retornará o código http 404 (Não encontrado).

O Sling também permite que outros nós que não o JCR sejam recursos, mas esse é um recurso avançado.

### Localização do script {#locating-the-script}

Quando o recurso apropriado (nó de conteúdo) está localizado, o tipo **de recurso** sling é extraído. Esse é um caminho, que localiza o script a ser usado para renderizar o conteúdo.

O caminho especificado pelo `sling:resourceType` pode ser:

* absoluto
* relativo, a um parâmetro de configuração

   Os caminhos relativos são recomendados pela Adobe, pois aumentam a portabilidade.

Todos os scripts Sling são armazenados em subpastas de `/apps` ou `/libs`, que serão pesquisados nessa ordem (consulte [Personalizando componentes e outros elementos](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

Alguns outros pontos são:

* quando o Método (GET, POST) for necessário, ele será especificado em maiúsculas de acordo com a especificação HTTP, por exemplo, jobs.POST.esp (consulte abaixo)
* vários mecanismos de script são suportados:

   * `.esp, .ecma`: Páginas ECMAScript (JavaScript) (execução no servidor)
   * `.jsp`: Java Server Pages (execução no servidor)
   * `.java`: Java Servlet Compiler (execução no servidor)
   * `.jst`: Modelos JavaScript (execução no cliente)

A lista de mecanismos de script suportados pela instância específica do AEM está listada no Console de gerenciamento Felix ( `http://<host>:<port>/system/console/slingscripting`).

Além disso, o Apache Sling oferece suporte à integração com outros mecanismos de script populares (por exemplo, Groovy, JRuby, Freemarker) e fornece uma maneira de integrar novos mecanismos de script.

Usando o exemplo acima, se o `sling:resourceType` for `hr/jobs` :

* Solicitações GET/HEAD e URLs terminando em .html (tipos de solicitação padrão, formato padrão)

   O script será /apps/hr/jobs/jobs.esp; a última seção de sling:resourceType forma o nome do arquivo.

* Solicitações POST (todos os tipos de solicitação exceto GET/HEAD, o nome do método deve estar em maiúsculas)

   O POST será usado no nome do script.

   O script será `/apps/hr/jobs/jobs.POST.esp`.

* URLs em outros formatos, sem terminar com .html

   Por exemplo `../content/corporate/jobs/developer.pdf`

   O script será `/apps/hr/jobs/jobs.pdf.esp`; o sufixo é adicionado ao nome do script.

* URLs com seletores

   Os seletores podem ser usados para exibir o mesmo conteúdo em um formato alternativo. Por exemplo, uma versão compatível com a impressora, um feed rss ou um resumo.

   Se olharmos para uma versão fácil para a impressora onde o seletor pode ser *impresso*; como em `../content/corporate/jobs/developer.print.html`

   O script será `/apps/hr/jobs/jobs.print.esp`; o seletor é adicionado ao nome do script.

* Se nenhum sling:resourceType tiver sido definido, então:

   * o caminho do conteúdo será usado para procurar um script apropriado (se o ResourceTypeProvider baseado em caminho estiver ativo).

      Por exemplo, o script para `../content/corporate/jobs/developer.html` geraria uma pesquisa em `/apps/content/corporate/jobs/`.

   * o tipo de nó primário será usado.

* Se nenhum script for encontrado, o script padrão será usado.

   Atualmente, a representação padrão é compatível com texto sem formatação (.txt), HTML (.html) e JSON (.json), todos os quais serão listas nas propriedades do nó (formatados adequadamente). A renderização padrão para a extensão .res, ou solicitações sem uma extensão de solicitação, é para spool do recurso (quando possível).
* Para a manipulação de erros http (códigos 403 ou 404), o Sling procurará um script em:

   * o local /apps/sling/servlet/errorhandler para scripts [personalizados](/help/sites-developing/customizing-errorhandler-pages.md)
   * ou o local dos scripts padrão /libs/sling/servlet/errorhandler/403.esp, ou 404.esp, respectivamente.

Se vários scripts se aplicarem a uma determinada solicitação, o script com a melhor correspondência será selecionado. Quanto mais específico for o jogo, melhor será; em outras palavras, quanto mais o seletor corresponder melhor, independentemente de qualquer extensão de solicitação ou nome de método correspondente.

Por exemplo, considere uma solicitação para acessar o recurso`/content/corporate/jobs/developer.print.a4.html`do tipo
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

Além dos tipos de recursos (definidos primariamente pela `sling:resourceType` propriedade), há também o supertipo de recurso. Isso é geralmente indicado pela `sling:resourceSuperType` propriedade. Esses supertipos também são considerados ao tentar encontrar um script. A vantagem dos supertipos de recursos é que eles podem formar uma hierarquia de recursos na qual o tipo de recurso padrão `sling/servlet/default` (usado pelos servlets padrão) é efetivamente a raiz.

O supertipo de recurso de um recurso pode ser definido de duas formas:

* pela `sling:resourceSuperType` propriedade do recurso.
* pela `sling:resourceSuperType` propriedade do nó para o qual os `sling:resourceType` pontos são posicionados.

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




A hierarquia de tipos de:

* `/x`
   * é `[ c, b, a, <default>]`
* while for `/y`
   * a hierarquia é `[ c, a, <default>]`

Isso ocorre porque `/y` tem a `sling:resourceSuperType` propriedade, enquanto `/x` não, e portanto seu supertipo é retirado de seu tipo de recurso.

#### Scripts Sling não podem ser chamados diretamente {#sling-scripts-cannot-be-called-directly}

No Sling, os scripts não podem ser chamados diretamente, pois isso quebraria o conceito restrito de servidor REST. você misturaria recursos e representações.

Se você chamar a representação (o script) diretamente, oculta o recurso dentro do script, de modo que a estrutura (Sling) não saiba mais sobre ele. Assim, você perde determinados recursos:

* tratamento automático de métodos http diferentes de GET, incluindo:

   * POST, PUT, DELETE que são manipulados com uma implementação padrão de sling
   * o `POST.jsp` script no local sling:resourceType

* sua arquitetura de código não é mais tão limpa e tão claramente estruturada quanto deveria ser; de importância primordial para o desenvolvimento em larga escala

### API Sling {#sling-api}

Isso usa o pacote Sling API, org.apache.sling.&amp;ast; e bibliotecas de tags.

### Referência a elementos existentes usando sling:include {#referencing-existing-elements-using-sling-include}

Uma consideração final é a necessidade de fazer referência aos elementos existentes nos scripts.

Scripts mais complexos (como a agregação de scripts) podem precisar acessar vários recursos (por exemplo, navegação, barra lateral, rodapé, elementos de uma lista) e fazer isso incluindo o *recurso*.

Para fazer isso, você pode usar o comando sling:include(&quot;/&lt;caminho>/&lt;recurso>&quot;). Isso incluirá efetivamente a definição do recurso referenciado, como na seguinte declaração que faz referência a uma definição existente para a renderização de imagens:

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

O OSGi define uma arquitetura para desenvolver e implantar aplicativos e bibliotecas modulares (também conhecida como o Dynamic Module System for Java). Os container OSGi permitem que você divida seu aplicativo em módulos individuais (são arquivos jar com informações meta adicionais e chamados de pacotes na terminologia OSGi) e gerencie as dependências cruzadas entre eles com:

* serviços implementados no container
* um contrato entre o container e a sua aplicação

Esses serviços e contratos fornecem uma arquitetura que permite que elementos individuais se descubram dinamicamente para colaboração.

Em seguida, uma estrutura OSGi oferta o carregamento/descarregamento dinâmico, a configuração e o controle desses pacotes - sem a necessidade de reinicializações.

>[!NOTE]
>
>Para informações completas sobre a tecnologia OSGi, consultar o sítio web [do](https://www.osgi.org)OSGi.
>
>Em particular, a página de Educação Básica contém uma coleção de apresentações e tutoriais.

Essa arquitetura permite estender o Sling com módulos específicos do aplicativo. A Sling e, portanto, o CQ5, usa a implementação do [Apache Felix](https://felix.apache.org/) do OSGI (Open Services Gateway) e se baseia nas Especificações da OSGi Service Platform Release 4.2. Ambos são coleções de pacotes OSGi executados em uma estrutura OSGi.

Isso permite executar as seguintes ações em qualquer um dos pacotes da sua instalação:

* install
* start
* stop
* atualizar
* desinstalar
* ver o status atual
* acesse informações mais detalhadas (por exemplo, nome simbólico, versão, localização etc.) sobre os pacotes específicos

Consulte [o Console](/help/sites-deploying/web-console.md)da Web, Configuração [](/help/sites-deploying/configuring-osgi.md) OSGI e Configurações [OSGi para obter mais informações](/help/sites-deploying/osgi-configuration-settings.md) .

## Objetos de desenvolvimento no Ambiente AEM {#development-objects-in-the-aem-environment}

São de interesse para o desenvolvimento:

**Item** Um item é um nó ou uma propriedade.

Para obter informações detalhadas sobre como manipular objetos de Item, consulte os [Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) da Interface javax.jcr.Item

**Nó (e suas propriedades)** Os nós e suas propriedades são definidos na especificação JCR API 2.0 (JSR 283). Eles armazenam conteúdo, definições de objetos, scripts de renderização e outros dados.

Os nós definem a estrutura do conteúdo e suas propriedades armazenam o conteúdo e os metadados reais.

Os nós de conteúdo direcionam a renderização. O Sling obtém o nó de conteúdo da solicitação de entrada. A propriedade sling:resourceType desse nó aponta para o componente de renderização Sling a ser usado.

Um nó, que é um nome JCR, também é chamado de recurso no ambiente Sling.

Por exemplo, para obter as propriedades do nó atual, você pode usar o seguinte código no script:

`PropertyIterator properties = currentNode.getProperties();`

Com currentNode sendo o objeto node atual.

Para obter mais informações sobre como manipular objetos de Nó, consulte os [Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html).

**Widget** No AEM, toda a entrada do usuário é gerenciada por widgets. Geralmente, eles são usados para controlar a edição de um conteúdo.

As caixas de diálogo são criadas pela combinação de widgets.

O AEM foi desenvolvido usando a biblioteca de widgets ExtJS.

**Diálogo** Uma caixa de diálogo é um tipo especial de widget.

Para editar conteúdo, o AEM usa caixas de diálogo definidas pelo desenvolvedor do aplicativo. Eles combinam uma série de widgets para apresentar ao usuário todos os campos e ações necessários para editar o conteúdo relacionado.

As caixas de diálogo também são usadas para editar metadados e por várias ferramentas administrativas.

**Componente** Um componente de software é um elemento do sistema que oferece um serviço ou evento predefinido e é capaz de se comunicar com outros componentes.

No AEM, um componente é frequentemente usado para renderizar o conteúdo de um recurso. Quando o recurso é uma página, a renderização do componente é chamada de Componente de nível superior ou Componente de página. No entanto, um componente não precisa renderizar conteúdo nem estar vinculado a um recurso específico; por exemplo, um componente de navegação exibirá informações sobre vários recursos.

A definição de um componente inclui:

* o código usado para renderizar o conteúdo
* uma caixa de diálogo para a entrada do usuário e a configuração do conteúdo resultante.

**Modelo** Um modelo é a base para um tipo específico de página. Ao criar uma página na guia Sites, o usuário precisa selecionar um modelo. A nova página é criada copiando esse modelo.

Um modelo é uma hierarquia de nós que tem a mesma estrutura que a página a ser criada, mas sem nenhum conteúdo real.

Ela define o componente de página usado para renderizar a página e o conteúdo padrão (conteúdo primário de nível superior). O conteúdo define como ele é renderizado, pois o AEM é centrado no conteúdo.

**Componente de página (Componente de nível superior)** O componente a ser usado para renderizar a página.

**Página** A é uma &quot;instância&quot; de um modelo.

Uma página tem um nó de hierarquia do tipo cq:Page e um nó de conteúdo do tipo cq:PageContent. A propriedade sling:resourceType do nó de conteúdo aponta para o Componente de página usado para renderizar a página.

Por exemplo, para obter o nome da página atual, você pode usar o seguinte código em seu script:

S`tring pageName = currentPage.getName();`

Com currentPage sendo o objeto de página atual. Para obter mais informações sobre como manipular objetos de Página, consulte os [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html).

**Gerenciador** de páginas O gerenciador de páginas é uma Interface que fornece métodos para operações de nível de página.

Por exemplo, para obter a página que contém um recurso, você pode usar o seguinte código em seu script:

Página myPage = pageManager.getContainPage(myResource);

Com pageManager sendo o objeto do gerenciador de páginas e myResource um objeto de recurso. Para obter mais informações sobre os métodos fornecidos pelo gerenciador de páginas, consulte os [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html).

## Estrutura no repositório {#structure-within-the-repository}

A lista a seguir fornece uma visão geral da estrutura que você verá no repositório.

>[!CAUTION]
>
>As alterações nesta estrutura, ou nos arquivos nela contidos, devem ser feitas com cuidado.
>
>As alterações são necessárias quando você está se desenvolvendo, mas você deve tomar cuidado para entender totalmente as implicações de quaisquer alterações feitas.

>[!CAUTION]
>
>Você não deve alterar nada no `/libs` caminho. Para a configuração e outras alterações, copie o item de `/libs` para `/apps` e faça quaisquer alterações dentro `/apps`.

* `/apps`

   Aplicações relacionadas; inclui definições de componentes específicas ao seu site. Os componentes que você desenvolve podem ser baseados nos componentes prontos disponíveis em `/libs/foundation/components`.

* `/content`

   Conteúdo criado para seu site.

* `/etc`

* `/home`

   Informações do usuário e do grupo.

* `/libs`

   Bibliotecas e definições que pertencem ao núcleo do AEM. As subpastas em `/libs` representam os recursos predefinidos do AEM como, por exemplo, pesquisa ou replicação. O conteúdo em não `/libs` deve ser modificado, pois afeta a maneira como o AEM funciona. Os recursos específicos do seu site devem ser desenvolvidos em `/apps` (consulte [Personalizando componentes e outros elementos](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

* `/tmp`

   Área de trabalho temporária.

* `/var`

   Arquivos que mudam e são atualizados pelo sistema; como registros de auditoria, estatísticas, tratamento de eventos. A subpasta `/var/classes` contém os servlets java em formulários de origem e compilados que foram gerados a partir dos scripts de componentes.

## Ambientes {#environments}

Com o AEM, um ambiente de produção geralmente consiste em dois tipos diferentes de instâncias: um [Autor e uma instância](/help/sites-deploying/deploy.md#author-and-publish-installs)de Publicação.

## O Dispatcher {#the-dispatcher}

O Dispatcher é a ferramenta da Adobe para armazenamento em cache e/ou balanceamento de carga. Informações adicionais podem ser encontradas sob [o Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html).

## FileVault (sistema de revisão da fonte) {#filevault-source-revision-system}

O FileVault fornece ao repositório JCR mapeamento do sistema de arquivos e controle de versão. Ele pode ser usado para gerenciar projetos de desenvolvimento do AEM com suporte total para armazenamento e controle de versão de código de projeto, conteúdo, configurações e assim por diante, em sistemas de controle de versão padrão (por exemplo, Subversão).

Consulte a documentação da ferramenta [](/help/sites-developing/ht-vlttool.md) FileVault para obter informações detalhadas.

## Fluxos de trabalhos {#workflows}

Seu conteúdo geralmente está sujeito a processos organizacionais, incluindo etapas como aprovação e aprovação por vários participantes. Esses processos podem ser representados como workflows, [definidos e desenvolvidos no AEM](/help/sites-developing/workflows-models.md)e, em seguida, aplicados às páginas [de conteúdo](/help/sites-administering/workflows.md) apropriadas ou aos ativos [](/help/assets/assets-workflow.md) digitais, conforme necessário.

O Motor de workflow é usado para gerenciar a implementação de seus workflows e de seus aplicativos subsequentes para seu conteúdo.

## Gerenciamento de vários sites {#multi-site-management}

O Multi Site Manager (MSM) permite gerenciar facilmente vários sites que compartilham conteúdo comum. O MSM permite que você defina relações entre os sites para que as alterações de conteúdo em um site sejam replicadas automaticamente em outros sites.

Por exemplo, os sites geralmente são fornecidos em vários idiomas para audiências internacionais. Quando o número de sites no mesmo idioma é baixo (três a cinco), um processo manual para sincronizar conteúdo entre sites é possível. No entanto, assim que o número de sites cresce ou quando vários idiomas estão envolvidos, torna-se mais eficiente automatizar o processo.

* Gerencie com eficiência diferentes versões de idiomas de um site.
* Atualizar automaticamente um ou mais sites com base em um site de origem:

   * Impor uma estrutura básica comum e usar conteúdo comum em vários sites.
   * Maximize o uso dos recursos disponíveis.
   * Mantenha uma aparência comum.
   * Concentre os esforços no gerenciamento do conteúdo que difere entre os sites.

Para obter mais informações, consulte [Multi Site Manager](/help/sites-administering/msm.md).