---
title: Introdução à extensão AEM para PWA Studio
description: Saiba como implantar um projeto de conteúdo e comércio sem cabeçalho AEM com o PWA Studio.
topics: Commerce
feature: Estrutura de integração de comércio
thumbnail: 37843.jpg
source-git-commit: 247c521e93990df2c8026da5edd84d163d5d424b
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---


# Introdução à extensão AEM para PWA Studio {#getting-started-pwa}

Imediatamente, o PWA Studio integra-se perfeitamente com o Adobe Commerce via GraphQL, oferecendo opções ilimitadas para criar vitrines inovadoras e envolventes e outras experiências digitais.

Fragmentos de conteúdo são partes de conteúdo com uma estrutura predefinida que permite que sejam consumidas de maneira headless usando GraphQL como API em diferentes formatos (por exemplo, JSON, Markdown) e renderizadas de maneira independente. Os fragmentos de conteúdo incluem todos os tipos de dados e campos necessários para GraphQL para garantir que seu aplicativo somente solicite o que está disponível e receba o que é esperado. A flexibilidade que eles oferecem em termos de como são estruturados os torna perfeitos para uso em vários locais e em vários canais.

Projetar a estrutura necessária é fácil com o Editor do modelo de fragmento de conteúdo no Adobe Experience Manager. O principal desafio para integrar os Fragmentos de conteúdo da Adobe Experience Manager (ou quaisquer outros dados) ao seu aplicativo PWA Studio é buscar dados de vários pontos de extremidade GraphQL. Isso ocorre porque o PWA Studio funciona imediatamente com um único ponto de extremidade GraphQL do Adobe Commerce.

## Arquitetura {#architecture}

![Arquitetura PWA sem periféricos](/help/commerce/cif/assets/pwa-studio/PWA-Studio_Architecture.png)

## PWA Studio de configuração {#setup-pwa}

Siga a documentação do Adobe Commerce [PWA Studio](https://magento.github.io/pwa-studio/tutorials/) para configurar seu aplicativo PWA Studio.

Para conectar o PWA Studio ao ponto de extremidade GraphQL da AEM, você pode usar a [AEM Extensão para PWA Studio](https://github.com/adobe/aem-pwa-studio-extensions).

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

   Você pode encontrar mais detalhes sobre a personalização do componente Navegação em [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) e na documentação do [Estrutura de Extensibilidade](https://magento.github.io/pwa-studio/pwa-buildpack/extensibility-framework/) do PWA Studio.

1. O cliente Apollo espera o ponto de extremidade GraphQL AEM em <https://pwa-studio/endpoint.js>. Para mapear o terminal para esse local, você precisará personalizar a configuração UPWARD do aplicativo PWA Studio:
a. Adicione a variável AEM_CFM_GRAPHQL ao pwa-root/.env e adapte-a ao ponto de extremidade GraphQL dos Fragmentos de Conteúdo AEM.

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

Siga a documentação AEM Fragmentos do conteúdo para configurar um ponto de extremidade GraphQL para o seu projeto AEM. Além disso, em seu projeto de AEM, adicione as seguintes configurações para permitir que o aplicativo PWA Studio acesse o ponto de extremidade GraphQL:

* Política de compartilhamento de recursos entre origens do Adobe Granite (com.adobe.granite.cors.impl.CORSPolicyImpl)

   Defina a propriedade allowedorigin como o nome de host completo do seu aplicativo PWA.

   Exemplo:  <https://pwa-studio-test-vflyn.local.pwadev:9366>

* Filtro de referenciador do Apache Sling (org.apache.sling.security.impl.ReferrerFilter.cfg.json)

   Defina a propriedade allow.hosts para o nome do host do seu aplicativo PWA.

   Exemplo: pwa-studio-test-vflyn.local.pwadev

Você pode encontrar exemplos completos de ambas as configurações aqui: <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

Para mostrar o ponto de extremidade GraphQL, preparamos algumas amostras de modelos e dados do Fragmento de conteúdo por meio de um pacote de conteúdo. Eles funcionam bem junto com os Componentes React fornecidos com a extensão PWA Studio.

## Como usar {#how-to-use}

Essa extensão é considerada um exemplo de implementação de como conectar um aplicativo do PWA Studio com AEM para recuperar e renderizar conteúdo via GraphQL.

Dependendo do caso de uso, você deseja criar seus próprios modelos de Fragmento de conteúdo personalizado, que resultam em um esquema GraphQL personalizado, que pode ser consumido pelos seus próprios componentes do React.

As configurações de produção podem variar em vários aspectos.

* Você pode ter um único ponto de extremidade GraphQL federado que combina dados AEM e Magento GraphQL em vez de personalizar o cliente Apollo.
* Seu aplicativo PWA Studio pode usar o URL do ponto de extremidade GraphQL da AEM diretamente, sem um proxy com UPWARD. O proxy também pode ser movido para uma camada diferente (por exemplo, CDN).
* A abordagem mais adequada para você também depende muito de como você entrega o aplicativo PWA Studio para o usuário final.

Essa extensão vem com dois exemplos.

### Blog {#blog}

Exiba postagens do blog com base em alguns modelos de Fragmento de conteúdo . Além disso, contém exemplos de como configurar o cliente Apollo para trabalhar com o ponto de extremidade GraphQL da AEM e como estender o componente de navegação no PWA Studio. Consulte [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) para obter mais detalhes.

### Enriquecimento PDP {#pdp-enrichment}

Permite que os profissionais de marketing enriqueçam facilmente as PDPs com conteúdo adicional, gerenciado como Fragmentos de conteúdo.  Consulte [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) para obter mais detalhes.
