---
title: Introdução à extensão AEM para PWA Studio
description: Saiba como implantar um projeto de conteúdo e comércio sem cabeçalho AEM com o PWA Studio.
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
exl-id: de7b8f05-b6b7-4105-84a5-940c16ebf2b4
source-git-commit: e05f6cd7cf17f4420176cf76f28cb469bcee4a0a
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Introdução à extensão AEM para PWA Studio {#getting-started-pwa}

Imediatamente, o PWA Studio integra-se perfeitamente com o Adobe Commerce por meio do GraphQL, fornecendo opções ilimitadas para criar vitrines inovadoras e envolventes e outras experiências digitais.

Fragmentos de conteúdo são partes de conteúdo com uma estrutura predefinida que permite que sejam consumidas de maneira headless usando o GraphQL como API em diferentes formatos (por exemplo, JSON, Markdown) e renderizadas de maneira independente. Os fragmentos de conteúdo incluem todos os tipos de dados e campos necessários para que o GraphQL garanta que seu aplicativo somente solicite o que está disponível e receba o que é esperado. A flexibilidade que eles oferecem em termos de como são estruturados os torna perfeitos para uso em vários locais e em vários canais.

Projetar a estrutura necessária é fácil com o Editor do modelo de fragmento de conteúdo no Adobe Experience Manager. O principal desafio para integrar os Fragmentos de conteúdo do Adobe Experience Manager (ou quaisquer outros dados) ao seu aplicativo PWA Studio é buscar dados de vários endpoints do GraphQL. O motivo é que, pronto para uso, o PWA Studio funciona com um único terminal Adobe Commerce GraphQL.

## Arquitetura {#architecture}

![Arquitetura PWA sem periféricos](/help/commerce/cif/assets/pwa-studio/PWA-Studio_Architecture.png)

## PWA Studio de configuração {#setup-pwa}

Para configurar seu aplicativo do PWA Studio, siga o guia Adobe Commerce [Documentação do PWA Studio](https://developer.adobe.com/commerce/pwa-studio/tutorials/).

Para conectar o PWA Studio ao terminal de AEM da GraphQL, você pode usar o [AEM extensão para PWA Studio](https://github.com/adobe/aem-pwa-studio-extensions).

1. Confira o repositório

1. No aplicativo PWA Studio, adicione a extensão como uma dependência de desenvolvimento.

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. Adicione o invólucro Apollo Link ao seu aplicativo PWA Studio. Em pwa-root/src/index.js, faça as seguintes alterações:

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   Você pode encontrar mais detalhes sobre a personalização do cliente Apollo em [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js).

1. Para estender o componente de navegação com uma entrada Blog, adicione as seguintes adaptações a pwa-root/local-intercept.js:

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   Você pode encontrar mais detalhes sobre a personalização do componente Navegação no [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) e na [Estrutura de extensibilidade](https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/extensibility/) documentação do PWA Studio.

1. O cliente Apollo espera o terminal AEM GraphQL em `<https://pwa-studio/endpoint.js>`. Para mapear o ponto de extremidade para esse local, personalize a configuração UPWARD do aplicativo PWA Studio: a. Para `pwa-root/.env`, adicione a variável AEM_CFM_GRAPHQL e adapte-a ao ponto de extremidade AEM do GraphQL de Fragmentos de conteúdo .

   Exemplo: AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>

   b. Adicione um resolvedor de proxy à sua configuração UPWARD. Uma amostra de configuração UPWARD poderia ser semelhante a:

```json
   response:
     resolver: conditional
     when:
       - matches: request.url.pathname
         pattern: ^/endpoint.json(/|$)
         use: aemProxy
     default: veniaResponse

   aemProxy:
     resolver: proxy
     target: env.AEM_CFM_GRAPHQL
     ignoreSSLErrors: true

   status: response.status
   headers: response.headers
   body: response.body
```

## AEM de configuração {#setup-aem}

Siga a documentação AEM Fragmentos do conteúdo para configurar um terminal GraphQL para o seu projeto AEM. Além disso, no projeto do AEM, adicione as seguintes configurações para permitir que o aplicativo PWA Studio acesse o terminal GraphQL:

* Política de compartilhamento de recursos entre origens do Adobe Granite (com.adobe.granite.cors.impl.CORSPolicyImpl)

   Defina as `allowedorigin` propriedade para o nome de host completo do aplicativo PWA.

   Exemplo:  `<https://pwa-studio-test-vflyn.local.pwadev:9366>`

* Filtro de referenciador do Apache Sling (org.apache.sling.security.impl.ReferrerFilter.cfg.json)

   Defina a propriedade allow.hosts para o nome do host do seu aplicativo PWA.

   Exemplo: pwa-studio-test-vflyn.local.pwadev

Você pode encontrar exemplos completos de ambas as configurações aqui: <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

Para mostrar o terminal GraphQL, o Adobe preparou algumas amostras de modelos e dados do Fragmento de conteúdo por meio de um pacote de conteúdo. Essas peças funcionam junto com os Componentes de reação fornecidos com a extensão PWA Studio.

## Como usar {#how-to-use}

Essa extensão é considerada um exemplo de implementação de como conectar um aplicativo do PWA Studio com AEM para recuperar e renderizar conteúdo por meio do GraphQL.

Dependendo do caso de uso, você deseja criar seus próprios modelos de Fragmento de conteúdo personalizados, que resultam em um esquema GraphQL personalizado que pode ser consumido por seus próprios componentes do React.

As configurações de produção podem variar em vários aspectos.

* Você pode ter um único terminal GraphQL federado que combina dados AEM e Adobe Commerce GraphQL em vez de personalizar o cliente Apollo.
* Seu aplicativo PWA Studio pode usar o URL do ponto de extremidade AEM GraphQL diretamente, sem um proxy com UPWARD. O proxy também pode ser movido para uma camada diferente (por exemplo, CDN).
* A abordagem adequada para você também depende muito de como você entrega o aplicativo PWA Studio para o usuário final.

Essa extensão vem com dois exemplos.

### Blog {#blog}

Exiba postagens do blog com base em alguns modelos de Fragmento de conteúdo . Além disso, contém exemplos de como configurar o cliente Apollo para trabalhar com o terminal GraphQL AEM e como estender o componente de navegação no PWA Studio. Consulte [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) para obter mais detalhes.

### Enriquecimento PDP {#pdp-enrichment}

Permite que os profissionais de marketing enriqueçam facilmente as PDPs com conteúdo adicional, gerenciado como Fragmentos de conteúdo. Consulte [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) para obter mais detalhes.
