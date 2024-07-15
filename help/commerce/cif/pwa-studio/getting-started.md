---
title: Introdução à extensão AEM para PWA Studio
description: Saiba como implantar um projeto de Commerce e conteúdo AEM headless com o PWA Studio.
topics: Commerce
feature: Commerce Integration Framework
exl-id: de7b8f05-b6b7-4105-84a5-940c16ebf2b4
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---

# Introdução à extensão AEM para PWA Studio {#getting-started-pwa}

Pronto para uso, o PWA Studio integra-se perfeitamente com o Adobe Commerce via GraphQL, fornecendo opções ilimitadas para criar vitrines inovadoras e envolventes e outras experiências digitais.

Fragmentos de conteúdo são partes de conteúdo com uma estrutura predefinida que permite seu consumo headless usando o GraphQL como API em diferentes formatos (por exemplo, JSON, Markdown) e renderizados de forma independente. Os fragmentos de conteúdo incluem todos os tipos de dados e campos necessários para que o GraphQL garanta que seu aplicativo solicite somente o que está disponível e receba o que é esperado. A flexibilidade que eles fornecem em termos de como são estruturados os torna perfeitos para uso em vários locais e em vários canais.

Projetar a estrutura necessária é fácil com o Editor de modelos de fragmentos de conteúdo no Adobe Experience Manager. O principal desafio para integrar os Fragmentos de conteúdo do Adobe Experience Manager (ou quaisquer outros dados) ao aplicativo PWA Studio é buscar dados de vários endpoints do GraphQL. O motivo é que o PWA Studio funciona com um único terminal Adobe Commerce GraphQL pronto para uso.

## Arquitetura {#architecture}

![arquitetura headless PWA](/help/commerce/cif/assets/pwa-studio/PWA-Studio_Architecture.png)

## Configurar PWA Studio {#setup-pwa}

Para configurar o aplicativo PWA Studio, siga a [documentação do PWA Studio](https://developer.adobe.com/commerce/pwa-studio/tutorials/) do Adobe Commerce.

Para conectar o PWA Studio com o ponto de extremidade GraphQL do AEM, você pode usar a Extensão [AEM para o PWA Studio](https://github.com/adobe/aem-pwa-studio-extensions).

1. Verificar o repositório

1. No aplicativo PWA Studio, adicione a extensão como uma dependência de desenvolvimento.

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. Adicione o invólucro do Link Apollo ao aplicativo PWA Studio. Em pwa-root/src/index.js, faça as seguintes alterações:

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   Você pode encontrar mais detalhes sobre a personalização do cliente Apollo em [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js).

1. Para estender o componente de navegação com uma entrada de Blog, adicione as seguintes adaptações a pwa-root/local-intercept.js:

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   Você pode encontrar mais detalhes sobre a personalização do componente de Navegação em [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) e na documentação [Estrutura de Extensibilidade](https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/extensibility/) do PWA Studio.

1. O cliente Apollo espera o ponto de extremidade AEM GraphQL em `<https://pwa-studio/endpoint.js>`. Para mapear o endpoint para esse local, personalize a configuração ASCENDENTE do aplicativo PWA Studio:
a. Para `pwa-root/.env`, adicione a variável AEM_CFM_GRAPHQL e adapte-a para apontar para o ponto de extremidade do AEM Content Fragments GraphQL.

   Exemplo: AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>

   b. Adicione um resolvedor de proxy à configuração ASCENDENTE. Um exemplo de configuração ASCENDENTE pode ter esta aparência:

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

## Configurar AEM {#setup-aem}

Siga a documentação dos Fragmentos de conteúdo do AEM para configurar um endpoint do GraphQL para seu projeto AEM. Além disso, no projeto AEM, adicione as seguintes configurações para permitir que o aplicativo PWA Studio acesse o endpoint do GraphQL:

* Política de compartilhamento de recursos entre origens do Adobe Granite (com.adobe.granite.cors.impl.CORSPolicyImpl)

  Defina a propriedade `allowedorigin` como o nome de host completo do aplicativo PWA.

  Exemplo: `<https://pwa-studio-test-vflyn.local.pwadev:9366>`

* Filtro referenciador do Apache Sling (org.apache.sling.security.impl.ReferrerFilter.cfg.json)

  Defina a propriedade allow.hosts com o nome de host do aplicativo PWA.

  Exemplo: pwa-studio-test-vflyn.local.pwadev

Você pode encontrar exemplos completos de ambas as configurações aqui: <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

Para mostrar o endpoint do GraphQL, o Adobe preparou alguns modelos de amostras de modelos e dados de fragmento de conteúdo por meio de um pacote de conteúdo. Essas partes funcionam em conjunto com os componentes do React fornecidos com a extensão PWA Studio.

## Como usar {#how-to-use}

Essa extensão é considerada um exemplo de implementação de como conectar um aplicativo PWA Studio com AEM para recuperar e renderizar conteúdo via GraphQL.

Dependendo do caso de uso, você deseja criar seus próprios modelos de Fragmento de conteúdo personalizados, que resultam em um esquema GraphQL personalizado que pode ser consumido pelos seus próprios componentes do React.

As configurações de produção podem variar em vários aspectos.

* Você pode ter um único endpoint federado do GraphQL que combina dados do AEM e do Adobe Commerce GraphQL em vez de personalizar o cliente Apollo.
* Seu aplicativo PWA Studio poderia usar o URL do endpoint AEM GraphQL diretamente, sem um proxy com UPWARD. O proxy também pode ser movido para uma camada diferente (por exemplo, CDN).
* A abordagem que se encaixa melhor para você também depende muito de como você fornece o aplicativo PWA Studio para o usuário final.

Essa extensão vem com dois exemplos.

### Blog {#blog}

Exibir postagens de blog com base em alguns modelos de Fragmento de conteúdo. Além disso, contém exemplos de como configurar o cliente Apollo para funcionar com o terminal AEM GraphQL e como estender o componente de navegação no PWA Studio. Consulte [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) para obter mais detalhes.

### Enriquecimento de PDP {#pdp-enrichment}

Permite que os profissionais de marketing enriqueçam facilmente os PDPs com conteúdo adicional gerenciado como Fragmentos de conteúdo. Consulte [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) para obter mais detalhes.
