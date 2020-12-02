---
title: Visão geral do editor de SPA
seo-title: Visão geral do editor de SPA
description: Este artigo fornece uma visão geral abrangente do Editor de SPA e de como ele funciona, incluindo workflows detalhados de interação do Editor de SPA no AEM.
seo-description: Este artigo fornece uma visão geral abrangente do Editor de SPA e de como ele funciona, incluindo workflows detalhados de interação do Editor de SPA no AEM.
uuid: c283abab-f5bc-414a-bc81-bf3bdce38534
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 06b8c0be-4362-4bd1-ad57-ea5503616b17
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 0%

---


# Visão Geral do Editor de SPA{#spa-editor-overview}

Aplicativos de página única (SPA) podem oferta experiências interessantes para usuários de sites. Os desenvolvedores querem ser capazes de criar sites usando estruturas SPA e os autores querem editar o conteúdo no AEM para um site criado usando essas estruturas.

O Editor de SPA oferta uma solução abrangente para suporte a SPA no AEM. Esta página fornece uma visão geral de como o suporte SPA é estruturado em AEM, como o Editor de SPA funciona e como a estrutura SPA e AEM permanecem sincronizadas.

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização do cliente baseada em SPA estrutura (por exemplo, Reagir ou Angular).

## Introdução {#introduction}

Os sites criados usando estruturas de SPA comuns, como React e Angular, carregam seu conteúdo por meio do JSON dinâmico e não fornecem a estrutura HTML necessária para que o Editor de página AEM possa colocar controles de edição.

Para habilitar a edição de SPA no AEM, é necessário um mapeamento entre a saída JSON do SPA e o modelo de conteúdo no repositório AEM para salvar as alterações no conteúdo.

SPA suporte no AEM introduz uma fina camada JS que interage com o código JS SPA quando carregado no Editor de páginas com o qual os eventos podem ser enviados e o local dos controles de edição pode ser ativado para permitir a edição no contexto. Esse recurso baseia-se no conceito Endpoint da API do Content Services, pois o conteúdo do SPA precisa ser carregado pelo Content Services.

Para obter mais detalhes sobre SPA em AEM, consulte os seguintes documentos:

* [SPA ](/help/sites-developing/spa-blueprint.md) Blueprintin para os requisitos técnicos de um SPA
* [Introdução ao SPA no ](/help/sites-developing/spa-getting-started-react.md) AEMpara um rápido tour de uma SPA simples

## Design {#design}

O componente de página de um SPA não fornece os elementos HTML de seus componentes filho por meio do arquivo JSP ou HTL. Esta operação é delegada no quadro SPA. A representação dos componentes filhos ou do modelo é buscada como uma estrutura de dados JSON no JCR. Os componentes SPA são adicionados à página de acordo com essa estrutura. Esse comportamento diferencia a composição inicial do corpo do componente de página de parceiros não SPA.

### Gerenciamento do modelo de página {#page-model-management}

A resolução e o gerenciamento do modelo de página são delegados em uma biblioteca `PageModel` fornecida. O SPA deve usar a biblioteca do Modelo de página para ser inicializado e criado pelo Editor de SPA. A biblioteca do Modelo de página foi fornecida indiretamente para o componente Página AEM por meio de `aem-react-editable-components` npm. O Modelo de página é um intérprete entre o AEM e o SPA e, portanto, sempre deve estar presente. Quando a página é criada, uma biblioteca adicional `cq.authoring.pagemodel.messaging` deve ser adicionada para permitir a comunicação com o editor de página.

Se o componente de página SPA herdar do componente principal da página, há duas opções para disponibilizar a categoria de biblioteca do cliente `cq.authoring.pagemodel.messaging`:

* Se o modelo for editável, adicione-o à política de página.
* Ou adicione as categorias usando `customfooterlibs.html`.

Para cada recurso no modelo exportado, o SPA mapeará um componente real que fará o
renderização. O modelo, representado como JSON, é renderizado usando os mapeamentos de componente dentro de um container.
![screen_shot_2018-08-20at144152](assets/screen_shot_2018-08-20at144152.png)

>[!CAUTION]
>
>A inclusão da categoria `cq.authoring.pagemodel.messaging` deve ser limitada ao contexto do Editor de SPA.

### Tipo de dados de comunicação {#communication-data-type}

Quando a categoria `cq.authoring.pagemodel.messaging` for adicionada à página, ela enviará uma mensagem ao Editor de páginas para estabelecer o tipo de dados de comunicação JSON. Quando o tipo de dados de comunicação estiver definido como JSON, as solicitações de GET se comunicarão com os pontos finais do Sling Model de um componente. Depois que uma atualização ocorre no editor de página, a representação JSON do componente atualizado é enviada para a biblioteca do Modelo de página. A biblioteca do Modelo de página informa a SPA de atualizações.

![screen_shot_2018-08-20at143628](assets/screen_shot_2018-08-20at143628.png)

## Fluxo de trabalho {#workflow}

Você pode entender o fluxo da interação entre o SPA e o AEM pensando no Editor SPA como um mediador entre os dois.

* A comunicação entre o editor de páginas e o SPA é feita usando JSON em vez de HTML.
* O editor de página fornece a versão mais recente do modelo de página para o SPA por meio da API de iframe e mensagens.
* O gerenciador de modelo de página notifica o editor de que está pronto para edição e transmite o modelo de página como uma estrutura JSON.
* O editor não altera ou nem acessa a estrutura DOM da página que está sendo criada, em vez de fornecer o modelo de página mais recente.

![screen_shot_2018-08-20at144324](assets/screen_shot_2018-08-20at144324.png)

### Fluxo de Trabalho Básico do Editor de SPA {#basic-spa-editor-workflow}

Tendo em mente os elementos principais do Editor de SPA, o fluxo de trabalho de alto nível de edição de um SPA dentro do AEM é exibido ao autor da seguinte maneira.

![sem título1](assets/untitled1.gif)

1. SPA Editor é carregado.
1. SPA é carregado em um quadro separado.
1. SPA solicita conteúdo JSON e renderiza componentes do lado do cliente.
1. SPA Editor detecta componentes renderizados e gera sobreposições.
1. O autor clica em sobreposição, exibindo a barra de ferramentas de edição do componente.
1. SPA Editor persiste as edições com uma solicitação de POST para o servidor.
1. SPA solicitações do Editor atualizaram o JSON para o SPA Editor, que é enviado para o SPA com um Evento DOM.
1. SPA renderiza novamente o componente em questão, atualizando seu DOM.

>[!NOTE]
>
>Lembre-se:
>
>* O SPA está sempre encarregado de sua exibição.
>* O Editor de SPA está isolado do próprio SPA.
>* Em produção (publicação), o editor de SPA nunca é carregado.

>



### Fluxo de trabalho de edição de página do cliente-servidor {#client-server-page-editing-workflow}

Esta é uma visão geral mais detalhada da interação cliente-servidor ao editar um SPA.

![page_editor_spa_authoringmediator-2](assets/page_editor_spa_authoringmediator-2.png)

1. O SPA inicializa-se e solicita o modelo de página do Exportador do Modelo Sling.
1. O Exportador do Modelo Sling solicita os recursos que compõem a página do repositório.
1. O repositório retorna os recursos.
1. O Exportador do Modelo Sling retorna o modelo da página.
1. O SPA instancia seus componentes com base no modelo de página.
1. **6** aO conteúdo informa ao editor que está pronto para criação.

   **6** bO editor de páginas solicita as configurações de criação de componentes.

   **6** cO editor de páginas recebe as configurações de componentes.
1. Quando o autor edita um componente, o editor de páginas publica uma solicitação de modificação no servlet POST padrão.
1. O recurso é atualizado no repositório.
1. O recurso atualizado é fornecido ao servlet POST.
1. O servlet POST padrão informa ao editor de página que o recurso foi atualizado.
1. O editor de páginas solicita o novo modelo de página.
1. Os recursos que compõem a página são solicitados do repositório.
1. Os recursos que compõem a página são fornecidos pelo repositório ao Exportador do Modelo Sling.
1. O modelo de página atualizado é retornado ao editor.
1. O editor de páginas atualiza a referência do modelo de página do SPA.
1. O SPA atualiza seus componentes com base na nova referência de modelo de página.
1. As configurações de componentes dos editores de página são atualizadas.

   **17** aO SPA sinaliza ao editor de página que o conteúdo está pronto.

   **17** bO editor de páginas fornece ao SPA configurações de componentes.

   **17** cO SPA fornece configurações de componentes atualizadas.

### Fluxo de trabalho de criação {#authoring-workflow}

Esta é uma visão geral mais detalhada que foca na experiência de criação.

![spa_content_authoringmodel](assets/spa_content_authoringmodel.png)

1. O SPA busca o modelo de página.
1. **2** aO modelo de página fornece ao editor os dados necessários para a criação.

   **2** bQuando notificado, o orquestrador de componentes atualiza a estrutura de conteúdo da página.
1. O orquestrador do componente query o mapeamento entre um tipo de recurso AEM e um componente SPA.
1. O orquestrador de componentes instancia dinamicamente o componente SPA com base no modelo de página e no mapeamento de componentes.
1. O editor de páginas atualiza o modelo de página.
1. **6** aO modelo de página fornece dados de criação atualizados para o editor de página.

   **6** bO modelo de página despacha as alterações no orquestrador do componente.
1. O orquestrador de componentes obtém o mapeamento de componentes.
1. O orquestrador de componentes atualiza o conteúdo da página.
1. Quando o SPA concluir a atualização do conteúdo da página, o editor de páginas carregará o ambiente de criação.

## Requisitos e limitações {#requirements-limitations}

Para permitir que o autor use o editor de página para editar o conteúdo de um SPA, seu aplicativo SPA deve ser implementado para interagir com o AEM SPA Editor SDK. Consulte [Introdução ao SPA no documento AEM](/help/sites-developing/spa-getting-started-react.md) para obter o mínimo necessário para a sua execução.

### Estruturas suportadas {#supported-frameworks}

O SPA Editor SDK oferece suporte às seguintes versões mínimas:

* Reagir 16.x e acima
* Angular 6.x e superior

As versões anteriores dessas estruturas podem funcionar com o AEM SPA Editor SDK, mas não são compatíveis.

### Estruturas adicionais {#additional-frameworks}

Estruturas de SPA adicionais podem ser implementadas para trabalhar com o SDK do AEM SPA Editor. Consulte o documento [SPA Blueprint](/help/sites-developing/spa-blueprint.md) para obter os requisitos que uma estrutura deve atender para criar uma camada específica da estrutura composta de módulos, componentes e serviços para trabalhar com o AEM SPA Editor.

### Usando vários seletores {#multiple-selectors}

Seletores personalizados adicionais podem ser definidos e usados como parte de um SPA desenvolvido para o SDK de SPA AEM. No entanto, esse suporte requer que o seletor `model` seja o primeiro seletor e a extensão seja `.json` como [exigido pelo Exportador JSON.](json-exporter-components.md#multiple-selectors)

### Requisitos do Editor de Texto {#text-editor-requirements}

Se você quiser usar o editor no local de um componente de texto criado no SPA, será necessária uma configuração adicional.

1. Defina um atributo (pode ser qualquer) no elemento invólucro do container que contém o texto HTML. No caso do conteúdo de amostra do Journal WKND, ele é um elemento `<div>` e o seletor que foi usado é `data-rte-editelement`.
1. Defina a configuração `editElementQuery` no `cq:InplaceEditingConfig` do componente de texto AEM correspondente que aponta para esse seletor, por exemplo `data-rte-editelement`. Isso permite que o editor saiba qual elemento HTML envolve o texto HTML.

Para obter um exemplo de como isso é feito, consulte o conteúdo de amostra do Journal [WKND.](https://github.com/adobe/aem-sample-we-retail-journal/pull/16/files)

Para obter informações adicionais sobre a propriedade `editElementQuery` e a configuração do editor de Rich Text, consulte [Configurar o Editor de Rich Text.](/help/sites-administering/rich-text-editor.md)

### Limitações           {#limitations}

O AEM SPA Editor SDK foi apresentado com o AEM 6.4 service pack 2. Ele é totalmente suportado pelo Adobe e, como um novo recurso, continua sendo aprimorado e expandido. Os seguintes recursos AEM ainda não são suportados pelo Editor de SPA:

* modo público alvo
* ContextHub
* Edição de imagens embutidas
* Editar configurações (por exemplo, ouvintes)
* Sistema de estilos
* Desfazer / Refazer
* Distorção de hora e diff de página
* Recursos que executam a regravação de HTML no lado do servidor, como o Verificador de links, serviço de regravação de CDN, redução de URL etc.
* Modo de desenvolvedor
* AEM inicializações
