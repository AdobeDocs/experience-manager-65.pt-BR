---
title: Uso do GraphiQL IDE no AEM
description: Saiba como usar o GraphiQL IDE no Adobe Experience Manager.
source-git-commit: 42ef4694a3301ae1cd34766ce4c19f4b0e2f2c38
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 97%

---

# Uso do GraphiQL IDE {#graphiql-ide}

Uma implementação do [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) IDE padrão está disponível para uso com a API GraphQL do Adobe Experience Manager (AEM).

>[!NOTE]
>
>O GraphiQL é incluído em todos os ambientes do AEM (mas só se torna acessível/visível quando você configura os pontos de acesso).
>
>Em versões anteriores, era necessário um pacote para instalar o GraphiQL IDE. Se você o instalou, agora é possível removê-lo.

>[!NOTE]
>Você deve [configurar os endpoints](/help/assets/content-fragments/graphql-api-content-fragments.md#graphql-aem-endpoint) no [navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md) antes de usar o GraphiQL IDE.

A ferramenta **GraphiQL** permite testar e depurar as consultas de GraphQL, possibilitando:

* selecionar o **endpoint** apropriado à configuração de Sites que deseja usar para as consultas
* inserir diretamente novas consultas
* criar e acessar **[consultas persistentes](/help/assets/content-fragments/persisted-queries.md)**
* executar as consultas para ver os resultados imediatamente
* gerenciar **variáveis de consulta**
* salvar e gerenciar **consultas persistentes**
* publicar ou desfazer a publicação de **consultas persistentes** (por exemplo, para/do `dev-publish`)
* consultar o **histórico** de consultas anteriores
* usar o **Explorador de documentação** para acessar a documentação; ajudando você a conhecer e entender quais métodos estão disponíveis.

É possível acessar o editor de consultas por meio de:

* **Ferramentas** -> **Geral** -> **Editor de consultas GraphQL**
* diretamente; por exemplo, `http://localhost:4502/aem/graphiql.html`

![Interface GraphiQL](assets/cfm-graphiql-interface.png "Interface GraphiQL")

Você pode usar o GraphiQL no sistema para que as consultas possam ser solicitadas pelo aplicativo cliente usando solicitações GET e para publicar consultas. Para o uso em produção, é possível [mover as consultas para o ambiente de produção](/help/assets/content-fragments/persisted-queries.md#transfer-persisted-query-production). Inicialmente ao autor de produção para validação do conteúdo recém-criado com as consultas e, finalmente, à produção de publicação para consumo em tempo real.

## Seleção do endpoint {#selecting-endpoint}

Como primeira etapa, é preciso selecionar o **[endpoint](/help/assets/content-fragments/graphql-api-content-fragments.md#graphql-aem-endpoint)** que deseja usar para as consultas. O endpoint é apropriado para a configuração dos Sites que você deseja usar para as consultas.

Isso está disponível na lista suspensa na parte superior direita.

## Criação e persistência de uma nova consulta {#creating-new-query}

Você pode inserir a nova consulta no editor, que está no painel central esquerdo, diretamente sob o logotipo do GraphiQL.

>[!NOTE]
>
>Se você tiver uma consulta persistente já selecionada que está sendo exibida no painel do editor, selecione `+` (ao lado de **Consultas persistentes**) para esvaziar o editor para sua nova consulta.

Basta começar a digitar. O editor também:

* mostra informações adicionais sobre os elementos ao passar o mouse sobre eles
* fornece recursos como realce de sintaxe, preenchimento automático, sugestão automática

>[!NOTE]
>
>As consultas de GraphQL normalmente começam com um caractere `{`.
>
>Linhas que começam com `#` são ignoradas.

Use a opção **Salvar como** para criar uma consulta persistente.

## Atualização da consulta persistente {#updating-persisted-query}

Selecione a consulta que deseja atualizar na lista do painel **[Consultas persistentes](/help/assets/content-fragments/persisted-queries.md)** (lado esquerdo).

A consulta será exibida no painel do editor. Faça as alterações necessárias e use a opção **Salvar** para confirmar as atualizações da consulta persistente.

## Execução de consultas {#running-queries}

Você pode executar uma nova consulta imediatamente ou pode carregar e executar uma consulta persistente. Para carregar uma consulta persistente, selecione-a na lista — a consulta será exibida no painel do editor.

Em ambos os casos, a consulta exibida no painel do editor é a que será executada quando você:

* clicar/tocar no ícone **Executar consulta**
* usar a combinação de teclado `Control-Enter`

## Variáveis de consulta {#query-variables}

<!-- more details needed here? -->

O GraphiQL IDE também permite gerenciar as [Variáveis de consulta](/help/assets/content-fragments/graphql-api-content-fragments.md#graphql-variables).

Por exemplo:

![Variáveis GraphQL](assets/cfm-graphqlapi-03.png "Variáveis GraphQL")

<!--
## Managing cache for your persisted queries {#managing-cache}

[Persisted queries](/help/headless/graphql-api/persisted-queries.md) are recommended as they can be cached at the dispatcher and CDN layers, ultimately improving the performance of the requesting client application. By default AEM will invalidate the Content Delivery Network (CDN) cache based on a default Time To Live (TTL).

>[!NOTE]
>
>Custom rewrite rules on the Dispatcher might override defaults from AEM publish. 
>
>In the case that you are sending TTL-based cache-control headers from the dispatcher, based on a location match pattern, then, if necessary, you might want to exclude `/graphql/execute.json/*` from the matches.

Using GraphQL you can configure the HTTP Cache Headers  to control these parameters for your individual persisted query.

1. The **Headers** option is accessible via the three vertical dots to the right of the persisted query name (far left panel):

   ![Persisted Query HTTP Cache Headers](assets/cfm-graphqlapi-headers-01.png "Persisted Query HTTP Cache Headers")

1. Selecting this will open the **Cache Configuration** dialog:

   ![Persisted Query HTTP Cache Header Settings](assets/cfm-graphqlapi-headers-02.png "Persisted Query HTTP Cache Header Settings")

1. Select the appropriate parameter, then adjust the value as required:

   * **cache-control** - **max-age**
     Caches can store this content for specified number of seconds. Typically this is the browser TTL (Time To Live).
   * **surrogate-control** - **s-maxage**
     Same as max-age but applies specifically to proxy caches.
   * **surrogate-control** - **stale-while-revalidate**
     Caches may continue to serve a cached response after it becomes stale, for up to the specified number of seconds.
   * **surrogate-control** - **stale-if-error**
     Caches may continue to serve a cached response in case of or origin error, for up to the specified number of seconds.

1. Select **Save** to persist the changes.
-->

## Publicação de consultas persistentes {#publishing-persisted-queries}

Depois de selecionar o [consulta persistente](/help/assets/content-fragments/persisted-queries.md) na lista (painel esquerdo), é possível usar o **Publicar** e **Cancelar publicação** ações. Isso as ativará no ambiente de publicação (por exemplo, `dev-publish`) para facilitar o acesso de seus aplicativos durante os testes.

>[!NOTE]
>
>A definição do cache da consulta persistente `Time To Live` {&quot;cache-control&quot;:&quot;parameter&quot;:value} tem um valor padrão de 2 horas (7200 segundos).

## Copiar o URL para acessar a consulta diretamente {#copy-url}

A opção **Copiar URL** permite simular uma consulta copiando o URL usado para acessar diretamente a consulta persistente e ver os resultados. Essa opção pode ser usada para testes; por exemplo, acessando em um navegador:

<!--
  >[!NOTE]
  >
  >The URL will need [encoding before using programmatically](/help/headless/graphql-api/persisted-queries.md#encoding-query-url).
  >
  >The target environment might need adjusting, depending on your requirements.
-->

Por exemplo:

`http://localhost:4502/graphql/execute.json/global/article-list-01`

Ao usar esse URL em um navegador, é possível confirmar os resultados:

![GraphiQL - Copiar URL](assets/cfm-graphiql-copy-url.png "GraphiQL - Copiar URL")

A opção **Copiar URL** é acessível por meio dos três pontos verticais à direita do nome da consulta persistente (painel à esquerda):

![GraphiQL - Copiar URL](assets/cfm-graphiql-persisted-query-options.png "GraphiQL - Copiar URL")

## Exclusão de consultas persistentes {#deleting-persisted-queries}

A opção **Excluir** também é acessível por meio dos três pontos verticais à direita do nome da consulta persistente (painel à esquerda).

<!-- what happens if you try to delete something that is still published? -->


## Instalação da consulta persistente na produção {#installing-persisted-query-production}

Depois de desenvolver e testar a consulta persistente com o GraphiQL, o objetivo final é [transferi-la para o ambiente de produção](/help/assets/content-fragments/persisted-queries.md#transfer-persisted-query-production) para que os aplicativos possam usá-la.

## Atalhos de teclado {#keyboard-shortcuts}

Há uma série de atalhos de teclado que fornecem acesso direto aos ícones de ação no IDE:

* Adornar a consulta: `Shift-Control-P`
* Mesclar consulta: `Shift-Control-M`
* Executar consulta: `Control-Enter`
* Preenchimento automático: `Control-Space`

>[!NOTE]
>
>Em alguns teclados, a tecla `Control` é rotulada como `Ctrl`.
