---
title: Práticas recomendadas
seo-title: Best Practices
description: Siga esta página para saber mais sobre as práticas recomendadas e as diretrizes que ajudarão desenvolvedores de AEM experientes nos sites que desejam criar modelos e componentes de aplicativos móveis.
seo-description: Follow this page to  learn best practices and guidelines that will help experienced AEM developers for sites, who want to build mobile app templates and components.
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# Práticas recomendadas     {#best-practices}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

A criação de um aplicativo do AEM Mobile On-demand Services é diferente da criação de um aplicativo que é executado diretamente no shell do Cordova (ou PhoneGap). Os desenvolvedores devem estar familiarizados com:

* Plug-ins compatíveis prontos para uso, bem como os plug-ins específicos do AEM Mobile.

>[!NOTE]
>
>Para saber mais sobre plug-ins, consulte os seguintes recursos:
>
>* [Uso de plug-ins do Cordova no AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [Uso de plug-ins do Cordova específicos para AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>


* Os modelos que usam funcionalidade de plug-in devem ser escritos de forma que ainda sejam autorais no navegador, sem a presença da ponte de plug-in.

   * Por exemplo, espere a variável *deviceready* antes de tentar acessar a API de um plug-in.

## Diretrizes para desenvolvedores de AEM {#guidelines-for-aem-developers}

As diretrizes a seguir ajudarão desenvolvedores de AEM experientes em sites que desejam criar modelos e componentes de aplicativos móveis:

**Estrutura AEM modelos de sites para incentivar a reutilização e a extensibilidade**

* Preferir vários arquivos de script de componente por um único monolítico

   * Vários pontos de extensão vazios são fornecidos, como *customheaderlibs.html* e *customfooterlibs.html*, que permitem que o desenvolvedor altere o modelo da página enquanto duplica o menor código principal possível
   * Os modelos podem ser estendidos e personalizados por meio do Sling *sling:resourceSuperType* mecanismo

* Preferir Sightly/HTL sobre JSP como a linguagem de modelo

   * Usar isso incentiva a separação do código da marcação, oferece proteção XSS e tem uma sintaxe mais familiar

**Otimizar para o desempenho no dispositivo**

* O script específico do artigo e as folhas de estilos devem ser incluídos na carga do artigo, usando o modelo contentsync de artigo dps
* Os scripts e as folhas de estilos compartilhados por mais de um artigo devem ser incluídos nos recursos compartilhados, por meio do modelo contentsync dps-HTMLResources
* Não faça referência a nenhum script externo que seja bloqueio de renderização

>[!NOTE]
>
>Você pode saber mais detalhadamente sobre scripts externos de bloqueio de renderização [here](https://developers.google.com/speed/docs/insights/BlockingJS).

**Preferir bibliotecas JS e CSS do cliente específicas do aplicativo em relação a Web**

* Para evitar sobrecarga em bibliotecas como jQuery Mobile para lidar com uma grande variedade de dispositivos e navegadores
* Quando um modelo está sendo executado em uma visualização da Web de um aplicativo, você tem controle sobre as plataformas e versões que o aplicativo vai suportar, bem como sobre o conhecimento de que o suporte a JavaScript estará presente. Por exemplo, prefira Iônico (talvez apenas o CSS) em vez do jQuery Mobile e da interface do usuário Onsen em vez do Bootstrap.

>[!NOTE]
>
>Para saber mais sobre o jQuery móvel, clique em [here](https://jquerymobile.com/browser-support/1.4/).

**Preferir microbibliotecas em vez de pilha completa**

* O tempo que leva para colocar o conteúdo no vidro do dispositivo será retardado por cada biblioteca da qual seus artigos dependem. Esse atraso é agravado quando uma nova visualização da Web é usada para renderizar cada artigo, de modo que cada biblioteca deve ser inicializada novamente do zero
* Se os artigos não forem criados como SPA (aplicativos de página única), provavelmente não será necessário incluir uma biblioteca de pilha completa, como o Angular
* Preferir bibliotecas menores e de finalidade única para ajudar a adicionar a interatividade necessária para sua página, como [Rastreamento](https://github.com/ftlabs/fastclick) ou [Velocity.js](https://velocityjs.org)

**Minimizar o tamanho da carga do artigo**

* Use os menores ativos possíveis que possam cobrir efetivamente o maior visor que você estará suportando, em uma resolução razoável
* Usar uma ferramenta como *ImageOptim* em suas imagens para remover qualquer metadado em excesso

## Avançar {#getting-ahead}

Para entender mais sobre as outras duas funções e responsabilidades, consulte os recursos abaixo:

* [Administrador](/help/mobile/aem-mobile.md)
* [Autor](/help/mobile/aem-mobile-on-demand.md)
