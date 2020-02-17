---
title: Práticas recomendadas
seo-title: Práticas recomendadas
description: Siga esta página para saber mais sobre as práticas recomendadas e as diretrizes que ajudarão desenvolvedores experientes do AEM para sites que desejam criar modelos e componentes de aplicativos móveis.
seo-description: Siga esta página para saber mais sobre as práticas recomendadas e as diretrizes que ajudarão desenvolvedores experientes do AEM para sites que desejam criar modelos e componentes de aplicativos móveis.
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Práticas recomendadas {#best-practices}

>[!NOTE]
>
>A Adobe recomenda usar o Editor SPA para projetos que exigem renderização do lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Criar um aplicativo de serviços sob demanda do AEM Mobile é diferente de criar um aplicativo que é executado diretamente no shell do Cordova (ou PhoneGap). Os desenvolvedores devem estar familiarizados com:

* Plug-ins compatíveis prontos para uso, bem como plug-ins específicos do AEM Mobile.

>[!NOTE]
>
>Para saber mais sobre plug-ins, consulte os seguintes recursos:
>
>* [Usar plug-ins do Cordova no AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [Usar plug-ins do Cordova específicos para o AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>



* Os modelos que usam a funcionalidade de plug-in devem ser gravados de forma que ainda sejam autoráveis no navegador, sem a presença da ponte de plug-in.

   * Por exemplo, aguarde a função *deviceready* antes de tentar acessar a API de um plug-in.

## Diretrizes para desenvolvedores do AEM {#guidelines-for-aem-developers}

As diretrizes a seguir ajudarão desenvolvedores AEM experientes para sites que desejam criar modelos e componentes de aplicativos móveis:

**Estruturar modelos de sites do AEM para incentivar a reutilização e a extensibilidade**

* Preferir vários arquivos de script de componente em um único monolítico

   * São fornecidos vários pontos de extensão vazios, como *customheaderlibs.html* e *customfooterlibs.html*, que permitem ao desenvolvedor alterar o modelo de página ao duplicar o menor código principal possível
   * Os modelos podem ser estendidos e personalizados por meio do mecanismo Sling: *resourceSuperType* do Sling

* Preferir Sightly/HTL sobre JSP como a linguagem de modelo

   * Usar isso incentiva uma separação do código da marcação, oferece proteção XSS integrada e tem uma sintaxe mais familiar

**Otimizar para o desempenho no dispositivo**

* O script específico do artigo e as folhas de estilo devem ser incluídos na carga do artigo, usando o modelo sincronia de conteúdo dps-article
* O script e as folhas de estilo compartilhadas por mais de um artigo devem ser incluídos nos recursos compartilhados, por meio do modelo de sincronia de conteúdo dps-HTMLResources
* Não faça referência a nenhum script externo que esteja bloqueando renderização

>[!NOTE]
>
>Você pode aprender mais detalhes sobre scripts externos de bloqueio de renderização [aqui](https://developers.google.com/speed/docs/insights/BlockingJS).

**Preferir bibliotecas JS e CSS do cliente específicas do aplicativo em relação a bibliotecas específicas da Web**

* Para evitar sobrecarga em bibliotecas como o jQuery Mobile para lidar com uma grande variedade de dispositivos e navegadores
* Quando um modelo é executado na visualização da Web de um aplicativo, você tem controle sobre as plataformas e versões que o aplicativo vai suportar, bem como sobre o conhecimento de que o suporte a JavaScript estará presente. Por exemplo, preferir Ionic (talvez apenas o CSS) em vez do jQuery Mobile e da interface do usuário Onsen em vez do Bootstrap.

>[!NOTE]
>
>Para saber mais sobre o jQuery Mobile, clique [aqui](https://jquerymobile.com/browser-support/1.4/).

**Preferir microbibliotecas em relação à pilha completa**

* O tempo necessário para colocar o conteúdo no vidro do dispositivo será reduzido em cada biblioteca de que seus artigos dependem. Essa desaceleração é agravada quando uma nova visualização da Web é usada para renderizar cada artigo, portanto, cada biblioteca deve ser inicializada novamente do zero
* Se seus artigos não forem criados como SPAs (aplicativos de página única), provavelmente não será necessário incluir uma biblioteca de pilha completa, como Angular
* Preferir bibliotecas menores e de propósito único para ajudar a adicionar a interatividade que sua página exige, como o [Fastclick](https://github.com/ftlabs/fastclick) ou o [Velocity.js](https://velocityjs.org)

**Minimizar o tamanho da carga do artigo**

* Use os menores ativos possíveis que possam cobrir efetivamente o maior visor que você estará suportando, em uma resolução razoável
* Use uma ferramenta como *ImageOptim* em suas imagens para remover qualquer excesso de metadados

## Como avançar {#getting-ahead}

Para entender mais sobre as outras duas funções e responsabilidades, consulte os recursos abaixo:

* [Administrador](/help/mobile/aem-mobile.md)
* [Autor](/help/mobile/aem-mobile-on-demand.md)
