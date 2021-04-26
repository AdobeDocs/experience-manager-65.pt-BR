---
title: Armazenamento em cache e desempenho
description: Saiba mais sobre as diferentes configurações disponíveis para habilitar o GraphQL e o armazenamento em cache de conteúdo para otimizar o desempenho da sua implementação de comércio.
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 96%

---

# Armazenamento em cache e desempenho {#caching}

## Armazenamento em Cache de Componente e Resposta GraphQL {#graphql}

Os Componentes principais da CIF do AEM já contam com suporte integrado para o armazenamento em cache de respostas GraphQL para componentes individuais. Esse recurso pode ser usado para reduzir consideravelmente o número de chamadas GraphQL de back-end. Um armazenamento em cache eficaz pode ser obtido especialmente para consultas repetitivas, como recuperar a árvore de categoria de um componente de navegação ou buscar todos os valores de agregações/facetas disponíveis, exibidos nas páginas de pesquisa e categoria do produto.

Para os Componentes principais da CIF do AEM, o armazenamento em cache é configurado de acordo com os componentes, portanto é possível controlar se (e por quanto tempo) as solicitações/respostas de GraphQL estão sendo armazenadas em cache para cada componente. Também é possível definir o comportamento do armazenamento em cache de serviços OSGi usando o cliente GraphQL.

### Configuração

Depois de configurado para um determinado componente, o cache começa a armazenar consultas e respostas GraphQL conforme definido por cada entrada de configuração do cache. O tamanho do cache e a duração do armazenamento em cache de cada entrada devem ser definidos de acordo com o projeto, dependendo, por exemplo, da frequência com que os dados do catálogo podem mudar, da importância de um componente sempre exibir os dados mais recentes possíveis etc. Observe que não há nenhuma invalidação de cache, portanto, tenha cuidado ao definir a duração do cache.

Ao configurar o armazenamento em cache de componentes, o nome do cache deve ser o nome dos componentes **proxy** definidos no projeto.

Antes de enviar uma solicitação GraphQL, o cliente verificará se já há uma solicitação GraphQL **exatamente igual** armazenada em cache e possivelmente retornará a resposta em cache. Para que haja correspondência, a solicitação GraphQL deve ser exatamente igual, ou seja, a consulta, o nome da operação (se houver), as variáveis (se houver) devem ser iguais à solicitação em cache. Além disso, todos os cabeçalhos HTTP personalizados que podem ser definidos devem ser iguais. Por exemplo, o cabeçalho `Store` da Magento deve ser igual.

### Exemplos

Recomendamos configurar algum armazenamento em cache para o serviço de pesquisa que busca todos os valores de agregações/facetas disponíveis exibidos nas páginas de pesquisa e categoria de produto. Normalmente, esses valores só mudam quando um novo atributo é adicionado aos produtos, por exemplo, para que a duração dessa entrada de cache possa ser &quot;grande&quot; se o conjunto de atributos do produto não for alterado com frequência. Embora seja uma configuração específica de cada projeto, recomendamos valores de alguns minutos em fases de desenvolvimento do projeto e de algumas horas em sistemas de produção estáveis.

Normalmente, esses valores são configurados com a seguinte entrada de cache:

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

O uso do recurso de armazenamento em cache GraphQl também é recomendado no componente de navegação porque envia a mesma consulta GraphQL em todas as páginas. Nesse caso, a entrada do cache normalmente seria definida como:

```
venia/components/structure/navigation:true:10:600
```

quando a [loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia) é usada. Observe o uso do nome proxy do componente `venia/components/structure/navigation`, e **não** o nome do componente de navegação na CIF (`core/cif/components/structure/navigation/v1/navigation`).

O armazenamento em cache para outros componentes deve ser definido de acordo com o projeto, geralmente junto com o armazenamento em cache configurado no Dispatcher. Lembre-se de que não há nenhuma invalidação ativa desses caches, portanto a duração do armazenamento em cache deve ser cuidadosamente definida. Não há valores de &quot;tamanho único&quot; que correspondam a todos os projetos e casos de uso possíveis. Defina a melhor estratégia de armazenamento em cache segundo as exigências do seu projeto.

## Cache do Dispatcher {#dispatcher}

O armazenamento em cache de páginas ou fragmentos do AEM no [AEM Dispatcher](https://docs.adobe.com/content/help/pt-BR/experience-manager-dispatcher/using/dispatcher.html) é uma prática recomendada para qualquer projeto do AEM. Normalmente, ele depende de técnicas de invalidação que garantem que qualquer conteúdo alterado no AEM seja atualizado corretamente no Dispatcher. É um recurso principal da estratégia de armazenamento em cache do AEM Dispatcher.

Além da CIF de conteúdo puro gerenciado pelo AEM, a página pode exibir dados comerciais que são buscados dinamicamente na Magento via GraphQL. Embora a estrutura da página em si nunca mude, o conteúdo comercial pode mudar se alguns dados do produto (nome, preço, etc.) forem alterados na Magento.

Para garantir que as páginas da CIF possam ser armazenadas em cache por um período limitado no AEM Dispatcher, recomendamos o uso da [Invalidação de cache de acordo com o tempo](https://docs.adobe.com/content/help/pt-BR/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl) (também conhecida como cache com base em TTL) ao armazenar páginas da CIF no AEM Dispatcher. Esse recurso pode ser configurado no AEM com o uso do pacote adicional [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/).

Com o armazenamento em cache com base em TTL, o desenvolvedor normalmente define uma ou várias durações de armazenamento em cache para determinadas páginas do AEM. Com essa definição, as páginas da CIF são armazenadas em cache somente no AEM Dispatcher pela duração configurada e o conteúdo é atualizado com frequência.

>[!NOTE]
>
>Embora os dados do lado do servidor possam ser armazenados em cache pelo AEM Dispatcher, alguns componentes da CIF, como `product`, `productlist` e `searchresults` normalmente tornam a buscar os preços do produto em uma solicitação do navegador do lado do cliente quando a página é carregada. Assim, o conteúdo dinâmico essencial é sempre buscado no carregamento da página.

## Recursos adicionais

- [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia)
- [Configuração de armazenamento em cache GraphQL](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM Dispatcher](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html)
