---
title: Práticas recomendadas para o AEM Mobile On-demand Services
description: Saiba mais sobre as práticas recomendadas e as diretrizes que ajudam desenvolvedores experientes de AEM em sites que desejam criar modelos e componentes de aplicativos móveis.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---

# Práticas recomendadas     {#best-practices}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Criar um aplicativo AEM Mobile On-demand Services é diferente de criar um aplicativo que é executado diretamente no shell Cordova (ou PhoneGap). Os desenvolvedores devem estar familiarizados com:

* Plug-ins imediatamente compatíveis e plug-ins específicos do AEM Mobile.

>[!NOTE]
>
>Para saber mais detalhes sobre plug-ins, consulte os seguintes recursos:
>
>* [Utilização de plug-ins do Cordova no AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [Uso de plug-ins específicos do AEM Mobile habilitados para Cordova](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>

* Os modelos que usam a funcionalidade de plug-in devem ser escritos de forma que ainda sejam autoráveis no navegador, sem que a ponte do plug-in esteja presente.

   * Por exemplo, aguarde o *device ready* antes de tentar acessar a API de um plugin.

## Diretrizes para desenvolvedores do AEM {#guidelines-for-aem-developers}

As diretrizes a seguir ajudam desenvolvedores experientes de AEM em sites que desejam criar modelos e componentes de aplicativos móveis:

**Estruturar modelos de sites AEM para incentivar a reutilização e a extensibilidade**

* Preferir vários arquivos de script de componentes em vez de um único arquivo monolítico

   * Vários pontos de extensão vazios são fornecidos, como *customheaderlibs.html* e *customfooterlibs.html*, que permitem que o desenvolvedor altere o modelo da página enquanto duplica o mínimo possível de código principal
   * Os modelos podem ser estendidos e personalizados por meio do *sling:resourceSuperType* mecanismo

* Prefira Sightly/HTL a JSP como a linguagem de modelo

   * O uso dessa opção incentiva a separação do código da marcação, oferece proteção XSS integrada e tem uma sintaxe mais familiar

**Otimizar para desempenho no dispositivo**

* As folhas de estilos e scripts específicos do artigo devem ser incluídas na carga do artigo, usando o template dps-article contentsync
* As folhas de scripts e estilos compartilhadas por mais de um artigo devem ser incluídas em recursos compartilhados, por meio do modelo dps-HTMLResources contentsync
* Não fazer referência a nenhum script externo que esteja bloqueando a renderização

>[!NOTE]
>
>Você pode saber mais detalhes sobre os scripts externos de bloqueio de renderização [aqui](https://developers.google.com/speed/docs/insights/BlockingJS).

**Prefira JS do lado do cliente específico do aplicativo e bibliotecas CSS específicas da Web**

* Para evitar sobrecarga em bibliotecas como jQuery Mobile para lidar com uma grande variedade de dispositivos e navegadores
* Quando um modelo está em execução na visualização da Web de um aplicativo, você tem controle sobre as plataformas e versões que o aplicativo será compatível e sabe que o suporte ao JavaScript estará presente. Por exemplo, prefira o Ionic (talvez apenas o CSS) ao jQuery Mobile e à interface do usuário do Onsen em vez do Bootstrap.

>[!NOTE]
>
>Para saber mais detalhes sobre o jQuery mobile, clique em [aqui](https://jquerymobile.com/browser-support/1.4/).

**Preferir bibliotecas micro em vez de pilha completa**

* O tempo necessário para colocar seu conteúdo no vidro do dispositivo será reduzido por cada biblioteca da qual seus artigos dependem. Esse atraso é agravado quando uma nova visualização da Web é usada para renderizar cada artigo, de modo que cada biblioteca deve ser inicializada novamente do zero
* Se seus artigos não forem criados como SPA (aplicativos de página única), você provavelmente não precisará incluir uma biblioteca de pilha completa, como o Angular
* Prefira bibliotecas menores de uso único para ajudar a adicionar a interatividade exigida por sua página, como [Fastclick](https://github.com/ftlabs/fastclick) ou [Velocity.js](https://velocityjs.org)

**Minimizar o tamanho da carga do artigo**

* Use os menores ativos possíveis que possam cobrir efetivamente o maior visor que você estiver apoiando, com uma resolução razoável
* Use uma ferramenta como *ImageOptim* nas imagens para remover qualquer excesso de metadados

## Avançando {#getting-ahead}

Para entender mais sobre as outras duas funções e responsabilidades, consulte os recursos abaixo:

* [Administrador](/help/mobile/aem-mobile.md)
* [Autor](/help/mobile/aem-mobile-on-demand.md)
