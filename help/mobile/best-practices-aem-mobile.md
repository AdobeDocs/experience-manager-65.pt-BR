---
title: Práticas recomendadas para o AEM Mobile On-demand Services
description: Saiba mais sobre as práticas recomendadas e as diretrizes que ajudam os desenvolvedores competentes do Adobe Experience Manager (AEM) para sites que desejam criar modelos e componentes de aplicativos para dispositivos móveis.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Práticas recomendadas {#best-practices}

{{ue-over-mobile}}

Criar um aplicativo AEM Mobile On-demand Services é diferente de criar um aplicativo que é executado diretamente no shell Cordova (ou PhoneGap). Os desenvolvedores devem estar familiarizados com:

* Plug-ins prontos para uso e plug-ins específicos para dispositivos móveis do Adobe Experience Manager (AEM).

>[!NOTE]
>
>Para saber mais detalhes sobre plug-ins, consulte os seguintes recursos:
>
>* [Usando plug-ins do Cordova no AEM Mobile](https://helpx.adobe.com/br/digital-publishing-solution/help/cordova-api.html)
>* [Usando plug-ins habilitados para Cordova específicos do AEM Mobile](https://helpx.adobe.com/br/digital-publishing-solution/help/app-runtime-api.html)
>

* Os modelos que usam a funcionalidade de plug-in devem ser escritos de forma que ainda sejam autoráveis no navegador, sem que a ponte do plug-in esteja presente.

   * Por exemplo, aguarde a função *deviceready* antes de tentar acessar a API de um plug-in.

## Diretrizes para desenvolvedores do AEM {#guidelines-for-aem-developers}

As seguintes diretrizes ajudam os desenvolvedores de AEM competentes para sites que desejam criar modelos e componentes de aplicativos móveis:

**Estruturar modelos de sites AEM para incentivar a reutilização e a extensibilidade**

* Preferir vários arquivos de script de componente em vez de um único arquivo monolítico

   * Vários pontos de extensão vazios são fornecidos, como *customheaderlibs.html* e *customfooterlibs.html*, que permitem que o desenvolvedor altere o modelo da página enquanto duplica o mínimo possível de código principal
   * Os modelos podem ser estendidos e personalizados pelo mecanismo *sling:resourceSuperType* do Sling

* Prefira Sightly/HTL a JSP como a linguagem de modelo

   * O uso dessa opção incentiva a separação do código da marcação, oferece proteção XSS integrada e tem uma sintaxe mais familiar

**Otimizar para desempenho no dispositivo**

* As folhas de estilos e scripts específicos do artigo devem ser incluídas na carga do artigo, usando o template dps-article contentsync
* As folhas de scripts e estilos compartilhadas por mais de um artigo devem ser incluídas em recursos compartilhados, por meio do modelo dps-HTMLResources contentsync
* Não fazer referência a nenhum script externo que esteja bloqueando a renderização

>[!NOTE]
>
>Você pode saber mais detalhes sobre os scripts externos de bloqueio de renderização [aqui](https://developers.google.com/speed/docs/insights/BlockingJS).

**Prefira JS e bibliotecas CSS específicas do cliente para o aplicativo a bibliotecas específicas da Web**

* Para evitar sobrecarga em bibliotecas como jQuery Mobile para lidar com uma grande variedade de dispositivos e navegadores
* Quando um modelo está em execução na visualização da Web de um aplicativo, você tem controle sobre as plataformas e versões compatíveis com o aplicativo e sabe que o suporte do JavaScript estará presente. Por exemplo, prefira o Ionic (apenas o CSS) ao jQuery Mobile e à interface do usuário do Onsen ao Bootstrap.

>[!NOTE]
>
>Para saber mais detalhes sobre o jQuery mobile, clique [aqui](https://jquerymobile.com/browser-support/1.4/).

**Preferir bibliotecas micro sobre pilha completa**

* O tempo que leva para colocar seu conteúdo no vidro do dispositivo é reduzido por cada biblioteca da qual seus artigos dependem. Esse atraso é agravado quando uma nova visualização da Web é usada para renderizar cada artigo, de modo que cada biblioteca deve ser inicializada novamente do zero
* Se seus artigos não forem criados como SPA (aplicativos de página única), você provavelmente não precisará incluir uma biblioteca de pilha completa, como o Angular
* Prefira bibliotecas menores de uso único que ajudem a adicionar a interatividade exigida pela sua página, como o [Fastclick](https://github.com/ftlabs/fastclick) ou o [Velocity.js](https://velocityjs.org)

**Minimizar tamanho da carga do artigo**

* Use os menores ativos possíveis que possam cobrir efetivamente o maior visor que você estiver apoiando, com uma resolução razoável
* Use uma ferramenta como o *ImageOptim* nas imagens para remover qualquer excesso de metadados

## Avançando {#getting-ahead}

Para entender mais sobre as outras duas funções e responsabilidades, consulte os recursos abaixo:

* [Administrador](/help/mobile/aem-mobile.md)
* [Autor](/help/mobile/aem-mobile-on-demand.md)
