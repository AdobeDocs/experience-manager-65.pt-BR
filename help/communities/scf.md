---
title: Estrutura do componente social
seo-title: Estrutura do componente social
description: A estrutura de componentes sociais (SCF) simplifica o processo de configuração, personalização e extensão de componentes das Comunidades
seo-description: A estrutura de componentes sociais (SCF) simplifica o processo de configuração, personalização e extensão de componentes das Comunidades
uuid: 23b4418d-b91c-46fc-bf42-1154ef79fe5a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d7b5b5e3-2d84-4a6b-bcc2-d490882ff3ed
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 0%

---


# Estrutura do componente social {#social-component-framework}

A estrutura de componentes sociais (SCF) simplifica o processo de configuração, personalização e extensão de componentes das Comunidades tanto do lado do servidor quanto do cliente.

Os benefícios do quadro:

* **Funcional**: Facilidade imediata de integração com pouca ou nenhuma personalização para 80% dos casos de uso.
* **Inclinável**: Uso consistente de atributos HTML para estilização de CSS.
* **Extensível**: A implementação do componente é orientada a objetos e tem como base a lógica comercial - fácil adicionar logon de negócios incremental no servidor.
* **Flexível**: Modelos simples de javascript sem lógica que são facilmente sobrepostos e personalizados.
* **Acessível**: A API HTTP oferece suporte à publicação de qualquer cliente, incluindo aplicativos móveis.
* **Portátil**: Integre/incorpore em qualquer página da Web criada em qualquer tecnologia.

Explore uma instância de autor ou publicação usando o guia [interativo Componentes da](components-guide.md)comunidade.

## Visão geral {#overview}

No SCF, um componente é composto de um POJO do SocialComponent, um Modelo JS do Handlebars (para renderizar o componente) e CSS (para estilizar o componente).

Um Modelo JS Handlebars pode estender os componentes JS modelo/visualização para lidar com a interação do usuário com o componente no cliente.

Se um componente precisar suportar a modificação de dados, a implementação da API do SocialComponent pode ser gravada para suportar a edição/salvamento de dados semelhantes aos objetos de modelo/dados em aplicativos da Web tradicionais. Além disso, operações (controladores) e um serviço de operação podem ser adicionados para lidar com solicitações de operação, executar lógica comercial e invocar as APIs nos objetos de modelo/dados.

A API do SocialComponent pode ser estendida para fornecer dados exigidos por um cliente para uma camada de visualização ou um cliente HTTP.

### Como as páginas são renderizadas para o cliente {#how-pages-are-rendered-for-client}

![renderização de página de scf](assets/scf-overview.png)

### Personalização e extensão de componentes {#component-customization-and-extension}

Para personalizar ou estender os componentes, você grava somente as sobreposições e extensões no diretório /apps, o que simplifica o processo de atualização para versões futuras.

* Para esfolamento:
   * Somente o [CSS precisa de edição](client-customize.md#skinning-css).
* Para aparência e sentimento:
   * Altere o modelo JS e o CSS.
* Para aparência, toque e UX:
   * Altere o modelo JS, o CSS e [estenda/substitua o Javascript](client-customize.md#extending-javascript).
* Para modificar as informações disponíveis para o Modelo JS ou para o terminal do GET:
   * Estenda o [SocialComponent](server-customize.md#socialcomponent-interface).
* Para adicionar processamento personalizado durante operações:
   * Escreva uma [OperationExtension](server-customize.md#operationextension-class).
* Para adicionar uma nova operação personalizada:
   * Criar uma nova Operação [de publicação de](server-customize.md#postoperation-class)sling.
   * Use [OperationServices](server-customize.md#operationservice-class) existente, conforme necessário.
   * Adicione o código Javascript para chamar sua operação do lado do cliente, conforme necessário.

## Estrutura do lado do servidor {#server-side-framework}

A estrutura fornece APIs para acessar a funcionalidade no servidor e suportar a interação entre o cliente e o servidor.

### APIs Java {#java-apis}

As APIs Java fornecem classes abstratas e interfaces que são facilmente herdadas ou subclassificadas.

As classes principais são descritas na página Personalização [](server-customize.md) do servidor.

Visite Visão geral [do provedor de recursos do](srp.md) Armazenamento para saber mais sobre como trabalhar com o UGC.

### API HTTP {#http-api}

A API HTTP oferece suporte à facilidade de personalização e à escolha de plataformas clientes para aplicativos PhoneGap, aplicativos nativos e outras integrações e mashups. Além disso, a API HTTP permite que um site da comunidade seja executado como um serviço sem um cliente, de modo que os componentes da estrutura possam ser integrados em qualquer página da Web criada em qualquer tecnologia.

### API HTTP - Solicitações de GET {#http-api-get-requests}

Para cada SocialComponent, a estrutura fornece um terminal de API baseado em HTTP. O ponto de extremidade é acessado enviando uma solicitação de GET para o recurso com um seletor + extensão &#39;.social.json&#39;. Usando o Sling, a solicitação é entregue ao `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. Passa o recurso (resourceType) para o `SocialComponentFactoryManager` e recebe um SocialComponentFactory capaz de selecionar um `SocialComponent` representante do recurso.

1. Chama a fábrica e recebe uma `SocialComponent` capacidade de manusear o recurso e a solicitação.
1. Chama o `SocialComponent`, que processa a solicitação e retorna uma representação JSON dos resultados.
1. Retorna a resposta JSON ao cliente.

**`GET Request`**

Um servlet de GET padrão escuta solicitações .social.json às quais o SocialComponent responde com JSON personalizável.

![scf-framework](assets/scf-framework.png)

### API HTTP - Solicitações de POST {#http-api-post-requests}

Além das operações de GET (Leitura), a estrutura define um padrão de ponto de extremidade para permitir outras operações em um componente, incluindo Criar, Atualizar e Excluir. Esses pontos finais são APIs HTTP que aceitam entrada e respondem com códigos de status HTTP ou com um objeto de resposta JSON.

Esse padrão de endpoint da estrutura torna as operações CUD extensíveis, reutilizáveis e testáveis.

**`POST Request`**

Há uma operação Sling POST:para cada operação SocialComponent. A lógica comercial e o código de manutenção de cada operação são vinculados em um OperationService que é acessível por meio da API HTTP ou de outro lugar como um serviço OSGi. Os ganchos são fornecidos com suporte para extensões de operação conectáveis para ações anteriores/posteriores.

![scf-post-request](assets/scf-post-request.png)

### Provedor de recursos do armazenamento (SRP) {#storage-resource-provider-srp}

Para saber mais sobre como lidar com o UGC armazenado na loja [de conteúdo da](working-with-srp.md)comunidade, consulte:

* [Visão geral](srp.md) do provedor de recursos do armazenamento - Introdução e visão geral de uso do repositório.
* [SRP e UGC Essentials](srp-and-ugc.md) - métodos e exemplos do utilitário de API SRP.
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - diretrizes de codificação.

### Personalizações do servidor {#server-side-customizations}

Visite Personalizações [do lado do](server-customize.md) servidor para obter informações sobre como personalizar a lógica comercial e o comportamento de um componente Comunidades no lado do servidor.

## Idioma de Modelos JS do Handlebars {#handlebars-js-templating-language}

Uma das mudanças mais notáveis na nova estrutura é o uso da linguagem de modelo [Handlebars JS (HBS)](https://www.handlebarsjs.com/), uma tecnologia de código aberto popular para renderização de servidor-cliente.

Os scripts HBS são simples, sem lógica, compilados no servidor e no cliente, são fáceis de sobrepor e personalizar e se vinculam naturalmente ao UX do cliente porque o HBS suporta renderização no cliente.

A estrutura fornece vários [handlebars auxiliares](handlebars-helpers.md) que são úteis ao desenvolver SocialComponents.

No servidor, quando o Sling resolve uma solicitação de GET, ele identifica o script que será usado para responder à solicitação. Se o script for um modelo HBS (.hbs), o Sling delegará a solicitação ao Mecanismo de barras de mão. O Mecanismo de barras de mão obterá o SocialComponent do SocialComponentFactory apropriado, criará um contexto e renderizará o HTML.

### Sem restrição de acesso {#no-access-restriction}

Os arquivos de modelo do Handlebars (HBS) (.hbs) são análogos aos arquivos de modelo .jsp e .html, exceto que podem ser usados para renderização tanto no navegador cliente quanto no servidor. Portanto, um navegador cliente que solicita um modelo do lado do cliente receberá um arquivo .hbs do servidor.

Isso requer que todos os modelos HBS no caminho de pesquisa de sling (quaisquer arquivos .hbs em /libs/ ou /apps) possam ser buscados por qualquer usuário do autor ou publicação.

O acesso HTTP a arquivos .hbs pode não ser proibido.

### Adicionar ou incluir um componente Comunidades {#add-or-include-a-communities-component}

A maioria dos componentes das Comunidades deve ser *adicionada* como um recurso endereçável Sling. Alguns dos componentes Comunidades podem ser *incluídos* em um modelo como um recurso não existente para permitir a inclusão dinâmica e a personalização do local no qual gravar o conteúdo gerado pelo usuário (UGC).

Em ambos os casos, as bibliotecas [de cliente](clientlibs.md) necessárias do componente também devem estar presentes.

**Adicionar um componente**

Adicionar um componente refere-se ao processo de adicionar uma instância de um recurso (componente), como quando arrastado do navegador de componente (sidekick) para uma página no modo de edição do autor.

O resultado é um nó filho JCR sob um nó par, que é endereçável para Sling.

**Incluir um componente**

A inclusão de um componente refere-se ao processo de adição de uma referência a um recurso [](srp.md#for-non-existing-resources-ners) &quot;não existente&quot; (nenhum nó JCR) dentro do modelo, como o uso de uma linguagem de script.

A partir do AEM 6.1, quando um componente é incluído dinamicamente em vez de adicionado, é possível editar as propriedades do componente no modo *design *do autor.

Somente alguns componentes AEM Communities selecionados podem ser incluídos dinamicamente. São eles:

* [Comentários](essentials-comments.md)
* [Classificação](rating-basics.md)
* [Revisões](reviews-basics.md)
* [Votação](essentials-voting.md)

O Guia [de componentes da](components-guide.md) comunidade permite que componentes incluíveis sejam alternados de serem adicionados à inclusão.

**Ao usar o idioma de modelo do Handlebars** , o recurso não existente é incluído usando o auxiliar [include](handlebars-helpers.md#include) especificando o resourceType:

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**Ao usar o JSP**, um recurso é incluído usando a tag [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>Para adicionar um componente a uma página dinamicamente, em vez de adicioná-lo ou incluí-lo em um modelo, consulte Sideload [de componentes](sideloading.md).

### Auxiliares de guiadores {#handlebars-helpers}

Consulte Auxiliares [de barras de mão](handlebars-helpers.md) SCF para obter uma lista e uma descrição dos auxiliares personalizados disponíveis no SCF.

## Estrutura do lado do cliente {#client-side-framework}

### Estrutura Javascript de Visualização modelo {#model-view-javascript-framework}

A estrutura inclui uma extensão do [Backbone.js](https://www.backbonejs.org/), uma estrutura JavaScript de visualização de modelo, para facilitar o desenvolvimento de componentes avançados e interativos. A natureza orientada a objetos suporta uma estrutura extensível/reutilizável. A comunicação entre o cliente e o servidor é simplificada por meio da API HTTP.

A estrutura utiliza modelos Handlebars do lado do servidor para renderizar os componentes do cliente. Os modelos são baseados nas respostas JSON geradas pela API HTTP. As visualizações se vinculam ao HTML gerado pelos modelos Handlebars e fornecem interatividade.

### Convenções CSS {#css-conventions}

As convenções recomendadas a seguir para definir e usar classes CSS são as seguintes:

* Use nomes de seletores de classe CSS claramente nomeados e evite nomes genéricos como &#39;cabeçalho&#39;, &#39;imagem&#39; etc.
* Defina estilos de seletor de classe específicos para que as folhas de estilos CSS funcionem bem com outros elementos e estilos na página. Por exemplo: `.social-forum .topic-list .li { color: blue; }`
* Manter classes CSS para estilização separadas das classes CSS para UX orientadas pelo JavaScript.

### Personalizações do lado do cliente {#client-side-customizations}

Para personalizar a aparência e o comportamento de um componente Comunidades no lado do cliente, consulte Personalizações [do lado do](client-customize.md)cliente, que inclui informações sobre:

* [Sobreposições](client-customize.md#overlays)
* [Extensões](client-customize.md#extensions)
* [Marcação HTML](client-customize.md#htmlmarkup)
* [CSS de capa](client-customize.md#skinning-css)
* [Extensão do Javascript](client-customize.md#extending-javascript)
* [Clientlibs para SCF](client-customize.md#clientlibs-for-scf)

## Recursos e componentes básicos {#feature-and-component-essentials}

As informações essenciais para desenvolvedores estão descritas na seção [Recursos e componentes essenciais](essentials.md) .

Informações adicionais sobre o desenvolvedor podem ser encontradas na seção [Coding Guidelines (Diretrizes](code-guide.md) de codificação).

## Resolução de problemas {#troubleshooting}

As preocupações comuns e os problemas conhecidos são descritos na seção [Solução de problemas](troubleshooting.md) .

