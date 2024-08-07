---
title: Estrutura do componente social
description: A estrutura do componente social (SCF) simplifica o processo de configuração, personalização e extensão dos componentes do Communities
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5ca58bc3-8505-4d91-9cd1-6b2e2671f1be
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 0%

---

# Estrutura do componente social {#social-component-framework}

A estrutura do componente social (SCF) simplifica o processo de configuração, personalização e extensão dos componentes do Communities no lado do servidor e no lado do cliente.

Os benefícios do quadro:

* **Funcional**: facilidade de integração imediata com pouca ou nenhuma personalização para 80% dos casos de uso.
* **Skinnable**: uso consistente de atributos de HTML para estilo CSS.
* **Extensível**: a implementação de componentes é orientada a objetos e tem uma lógica de negócios clara - é fácil adicionar um logon comercial incremental no servidor.
* **Flexível**: modelos simples de JavaScript sem lógica que são facilmente sobrepostos e personalizados.
* **Acessível**: a API HTTP oferece suporte a postagens de qualquer cliente, incluindo aplicativos móveis.
* **Portátil**: integre/incorpore em qualquer página da Web com base em qualquer tecnologia.

Explore uma instância de autoria ou publicação usando o [guia interativo dos Componentes da comunidade](components-guide.md).

## Visão geral {#overview}

No SCF, um componente é composto de um POJO do SocialComponent, um modelo JS Handlebars (para renderizar o componente) e CSS (para estilizar o componente).

Um modelo JS Handlebars pode estender os componentes JS de modelo/visualização para lidar com a interação do usuário com o componente no cliente.

Se um componente precisar suportar a modificação de dados, a implementação da API do SocialComponent poderá ser gravada para suportar a edição/salvamento de dados semelhantes a objetos de modelo/dados em aplicativos web tradicionais. Além disso, as operações (controladores) e um serviço de operação podem ser adicionados para lidar com solicitações de operação, executar lógica de negócios e chamar as APIs nos objetos de modelo/dados.

A API do SocialComponent pode ser estendida para fornecer dados exigidos por um cliente para uma camada de visualização ou um cliente HTTP.

### Como as páginas são renderizadas para o cliente {#how-pages-are-rendered-for-client}

![scf-page-rendering](assets/scf-overview.png)

### Personalização e extensão de componentes {#component-customization-and-extension}

Para personalizar ou estender os componentes, grave somente as sobreposições e extensões no diretório /apps, o que simplifica o processo de atualização para versões futuras.

* Para esfola:
   * Somente o [CSS precisa ser editado](client-customize.md#skinning-css).
* Para Aparência:
   * Altere o modelo JS e o CSS.
* Para Look, Feel e UX:
   * Altere o Modelo JS, CSS e [estender/substituir JavaScript](client-customize.md#extending-javascript).
* Para modificar as informações disponíveis para o modelo JS ou para o endpoint do GET:
   * Estenda o [SocialComponent](server-customize.md#socialcomponent-interface).
* Para adicionar processamento personalizado durante operações:
   * Gravar uma [OperationExtension](server-customize.md#operationextension-class).
* Para adicionar uma operação personalizada:
   * Crie uma [Operação do Sling Post](server-customize.md#postoperation-class).
   * Use os [OperationServices](server-customize.md#operationservice-class) existentes, conforme necessário.
   * Adicione o código JavaScript para chamar sua operação do lado do cliente, conforme necessário.

## Estrutura do lado do servidor {#server-side-framework}

A estrutura fornece APIs para acessar funcionalidades no servidor e suportar a interação entre o cliente e o servidor.

### APIs Java™ {#java-apis}

As APIs Java™ fornecem classes e interfaces abstratas que são facilmente herdadas ou classificadas em subclasses.

As classes principais são descritas na página [Personalização no lado do servidor](server-customize.md).

Visite [Visão Geral do Provedor de Recursos de Armazenamento](srp.md) para saber mais sobre como trabalhar com UGC.

### API HTTP {#http-api}

A API HTTP facilita a personalização e a escolha de plataformas de clientes para aplicativos PhoneGap, aplicativos nativos e outras integrações e mashups. Além disso, a API HTTP permite que um site da comunidade seja executado como um serviço sem um cliente, de modo que os componentes da estrutura possam ser integrados em qualquer página da Web criada em qualquer tecnologia.

### API HTTP - Solicitações GET {#http-api-get-requests}

Para cada SocialComponent, a estrutura fornece um terminal de API baseado em HTTP. O endpoint é acessado enviando uma solicitação GET para o recurso com um seletor &quot;.social.json&quot; + extensão. Usando o Sling, a solicitação é entregue ao `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. Passa o recurso (resourceType) para `SocialComponentFactoryManager` e recebe um SocialComponentFactory capaz de selecionar um `SocialComponent` representando o recurso.

1. Invoca a fábrica e recebe um `SocialComponent` capaz de manipular o recurso e a solicitação.
1. Invoca o `SocialComponent`, que processa a solicitação e retorna uma representação JSON dos resultados.
1. Retorna a resposta JSON ao cliente.

**`GET Request`**

Um servlet padrão do GET escuta solicitações .social.json às quais o SocialComponent responde com um JSON personalizável.

![estrutura-scf](assets/scf-framework.png)

### API HTTP - Solicitações POST {#http-api-post-requests}

Além das operações de GET (Leitura), a estrutura define um padrão de ponto de extremidade para permitir outras operações em um componente, incluindo Criar, Atualizar e Excluir. Esses endpoints são APIs HTTP que aceitam entrada e respondem com um código de status HTTP ou com um objeto de resposta JSON.

Esse padrão de endpoint da estrutura torna as operações de CUD extensíveis, reutilizáveis e testáveis.

**`POST Request`**

Há um Sling POST:operation para cada operação do SocialComponent. A lógica de negócios e o código de manutenção de cada operação são envolvidos em um OperationService acessível por meio da API HTTP ou de outro lugar como um serviço OSGi. Ganchos são fornecidos com suporte a extensões de operação conectáveis para ações antes/depois.

![scf-pós-solicitação](assets/scf-post-request.png)

### Provedor de recurso de armazenamento (SRP, Storage Resource Provider) {#storage-resource-provider-srp}

Para saber mais sobre a manipulação de UGC armazenados no [repositório de conteúdo da comunidade](working-with-srp.md), consulte:

* [Visão Geral do Provedor de Recursos de Armazenamento](srp.md) - Introdução e visão geral do uso do repositório.
* [Fundamentos de SRP e UGC](srp-and-ugc.md) - Métodos e exemplos do utilitário da API SRP.
* [Acessando UGC com SRP](accessing-ugc-with-srp.md) - Diretrizes de codificação.

### Personalizações do lado do servidor {#server-side-customizations}

Visite [Personalizações do lado do servidor](server-customize.md) para obter informações sobre como personalizar a lógica de negócios e o comportamento de um componente Comunidades no lado do servidor.

## Linguagem de modelo JS do Handlebars {#handlebars-js-templating-language}

Uma das alterações mais notáveis na nova estrutura é o uso da linguagem de modelo `Handlebars JS` (HBS), uma tecnologia de código aberto popular para renderização de servidor-cliente.

Os scripts HBS são simples, sem lógica, compilados no servidor e no cliente, são fáceis de sobrepor e personalizar e se vinculam naturalmente ao UX do cliente, pois o HBS oferece suporte à renderização no lado do cliente.

A estrutura fornece vários [Handlebars helpers](handlebars-helpers.md) que são úteis no desenvolvimento de SocialComponents.

No servidor, quando o Sling resolve uma solicitação do GET, ele identifica o script usado para responder à solicitação. Se o script for um modelo HBS (.hbs), o Sling delegará a solicitação ao mecanismo Handlebars. O mecanismo Handlebars obtém o SocialComponent do SocialComponentFactory apropriado, cria um contexto e renderiza o HTML.

### Sem restrição de acesso {#no-access-restriction}

Os arquivos de modelo Handlebars (HBS) (.hbs) são análogos aos arquivos de modelo .jsp e .html, exceto que podem ser usados para renderização tanto no navegador do cliente quanto no servidor. Portanto, um navegador cliente que solicita um modelo do lado do cliente recebe um arquivo .hbs do servidor.

Isso requer que todos os modelos HBS no caminho de pesquisa do sling (qualquer arquivo .hbs em /libs/ ou /apps) possam ser buscados por qualquer usuário do autor ou da publicação.

O acesso HTTP a arquivos .hbs não pode ser proibido.

### Adicionar ou incluir um componente das comunidades {#add-or-include-a-communities-component}

A maioria dos componentes das comunidades deve ser *adicionada* como um recurso endereçável do Sling. Alguns dos componentes selecionados das Comunidades podem ser *incluídos* em um modelo como um recurso não existente para permitir a inclusão dinâmica e a personalização do local no qual o conteúdo gerado pelo usuário (UGC) será gravado.

Em ambos os casos, as [bibliotecas de clientes necessárias](clientlibs.md) do componente também devem estar presentes.

**Adicionar um componente**

Adicionar um componente refere-se ao processo de adicionar uma instância de um recurso (componente), como quando arrastado do navegador de componentes (sidekick) para uma página no modo de edição do autor.

O resultado é um nó filho JCR em um nó par, que é endereçável Sling.

**Incluir um componente**

A inclusão de um componente refere-se ao processo de adição de uma referência a um recurso [&quot;não existente&quot;](srp.md#for-non-existing-resources-ners) (nenhum nó JCR) dentro do modelo, como o uso de uma linguagem de script.

A partir do Adobe Experience Manager (AEM) 6.1, quando um componente é incluído dinamicamente em vez de adicionado, é possível editar as propriedades do componente no modo autor *design*.

Somente alguns componentes selecionados do AEM Communities podem ser incluídos dinamicamente. São eles:

* [Comentários](essentials-comments.md)
* [Avaliação](rating-basics.md)
* [Revisões](reviews-basics.md)
* [Votação](essentials-voting.md)

O [Guia de Componentes da Comunidade](components-guide.md) permite que componentes incluíveis sejam alternados de adicionados para serem incluídos.

**Ao usar a linguagem de modelo Handlebars**, o recurso não existente é incluído usando o [assistente de inclusão](handlebars-helpers.md#include) especificando seu resourceType:

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**Ao usar o JSP**, um recurso é incluído usando a marca [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>Para adicionar um componente a uma página dinamicamente, em vez de adicioná-lo ou incluí-lo em um modelo, consulte [Sideload de Componentes](sideloading.md).

### Handlebars Helpers {#handlebars-helpers}

Consulte [Auxiliares de Handlebars do SCF](handlebars-helpers.md) para obter uma lista e uma descrição dos auxiliares personalizados disponíveis no SCF.

## Estrutura do lado cliente {#client-side-framework}

### Estrutura do JavaScript de exibição de modelo {#model-view-javascript-framework}

A estrutura inclui uma extensão do [Backbone.js](https://backbonejs.org/), uma estrutura JavaScript de exibição de modelo, para facilitar o desenvolvimento de componentes interativos avançados. A natureza orientada a objetos suporta uma estrutura extensível/reutilizável. A comunicação entre cliente e servidor é simplificada com a API HTTP.

A estrutura usa modelos Handlebars do lado do servidor para renderizar os componentes para o cliente. Os modelos são baseados nas respostas JSON geradas pela API HTTP. As visualizações se vinculam ao HTML gerado pelos modelos Handlebars e fornecem interatividade.

### Convenções CSS {#css-conventions}

As convenções recomendadas a seguir para definir e usar classes CSS:

* Use nomes claros do seletor de classe CSS com namespace e evite nomes genéricos como &quot;cabeçalho&quot; e &quot;imagem&quot;.
* Defina estilos específicos do seletor de classes para que as folhas de estilos CSS funcionem bem com outros elementos e estilos na página. Por exemplo: `.social-forum .topic-list .li { color: blue; }`
* Mantenha as classes CSS para estilização separadas das classes CSS para o UX orientado pelo JavaScript.

### Personalizações do lado do cliente {#client-side-customizations}

Para personalizar a aparência e o comportamento de um componente Communities no lado do cliente, consulte [Personalizações do lado do cliente](client-customize.md), que inclui informações sobre:

* [Sobreposições](client-customize.md#overlays)
* [Extensões ](client-customize.md#extensions)
* [Marcação HTML](client-customize.md#htmlmarkup)
* [Aplicação de capa a CSS](client-customize.md#skinning-css)
* [Extensão do JavaScript](client-customize.md#extending-javascript)
* [Clientlibs para SCF](client-customize.md#clientlibs-for-scf)

## Fundamentos de recursos e componentes {#feature-and-component-essentials}

As informações essenciais para desenvolvedores estão descritas na seção [Recursos e Componentes Essenciais](essentials.md).

Informações adicionais do desenvolvedor podem ser encontradas na seção [Diretrizes de codificação](code-guide.md).

## Resolução de problemas {#troubleshooting}

Problemas comuns e problemas conhecidos são descritos na seção [Solução de problemas](troubleshooting.md).
