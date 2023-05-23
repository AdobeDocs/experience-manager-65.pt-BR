---
title: Desenvolvimento de aplicativos móveis no AEM
seo-title: Developing Mobile Applications in AEM
description: Siga esta página para começar a desenvolver aplicativos para dispositivos móveis no AEM usando o Adobe PhoneGap Enterprise.
seo-description: Follow this page to start developing mobile application in AEM using Adobe PhoneGap Enterprise.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 1%

---

# Desenvolvimento de aplicativos móveis no AEM {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

O AEM aproveita as soluções de publicação do Adobe PhoneGap e do Adobe, permitindo que você crie e gerencie aplicativos móveis ricos em conteúdo e baseados em utilitários em várias plataformas:

* Gerencie todos os aplicativos móveis de suas empresas em um único local.
* Analise os aplicativos em ambientes de desenvolvimento e de preparo sem as complexidades dos perfis de provisionamento e o esforço extra para criar e carregar seu aplicativo para compartilhamento.
* Use o ambiente de criação do AEM para criar e gerenciar conteúdo avançado para seus aplicativos.
* Use o HTML5 com Adobe PhoneGap para criar experiências avançadas com recursos nativos do dispositivo.
* Apresentar o HTML5 Webviews a versões novas ou pré-existentes **nativo** aplicativos por meio do Cordova WebViews.
* Crie, prepare e compartilhe conteúdo multimídia avançado em todos os canais de entrega, incluindo internet, internet móvel, aplicativo para dispositivos móveis e impressão.

O AEM integra-se ao Adobe **[Serviço de PhoneGap Build](https://build.phonegap.com/)** para simplificar o processo de criação e implantação de aplicativos.

**Adobe ContentSync** O permite que os usuários baixem facilmente atualizações de página e conteúdo OTA (Over-the-Air) para seus dispositivos sem precisar reinstalar o aplicativo ou baixá-las da appStore, do Google Play ou de outras fontes de aplicativo.

**Adobe Analytics** O é totalmente integrado a aplicativos AEM e permite o rastreamento detalhado de distribuição, geolocalização, sistemas operacionais, dispositivos, fluxos de cliques, rastreamento de iBeacon e muito mais.

## Criação de aplicativos {#creating-apps}

Os desenvolvedores podem usar o [Kit inicial do PhoneGap para AEM](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) juntamente com os recursos adicionais encontrados no [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) para inicializar aplicativos AEM com PhoneGap, incluindo um aplicativo nativo de referência que executa o Cordova Webviews.

O readme do repositório Git do Starter Kit inclui um tutorial para usar o starter kit:

* Personalizar a identidade visual
* Destinos de build e implantação da amostra Maven
* Configuração do repositório de controle de origem
* Instalar e implantar em instâncias locais ou remotas do AEM
* Desinstalar do AEM

>[!NOTE]
>
>Uma fonte adicional de implementação de referência, incluindo laboratórios, pode ser encontrada no GitHub [aqui](https://github.com/adobe-marketing-cloud-apps) e, a fonte &quot;cozinha-pia&quot; [aqui](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Desenvolvimento para IOS 9 e hosts HTTP {#developing-for-ios-and-http-hosts}

Os desenvolvedores do iOS devem estar cientes de um problema em aberto com aplicativos Cordova em execução no iOS 9. Esse problema impede que solicitações sejam feitas a hosts inseguros (como *http://localhost:4502*). Esse problema será resolvido com uma próxima versão do cordova-ios (consumida pela CLI do Cordova), mas enquanto isso há duas soluções alternativas disponíveis:

1. Como solução alternativa imediata, você ainda pode usar qualquer um dos simuladores do iOS 8 sem problemas.
1. Se você precisar usar o iOS 9, seus aplicativos -Info.plist (encontrados após a execução `cordova platform add ios` em &quot;&lt;app root=&quot;&quot;>/platforms/ios/&lt;app name=&quot;&quot;>/&lt;app name=&quot;&quot;>O arquivo &quot;-Info.plist&quot;) pode ser editado manualmente para incluir a seguinte propriedade:

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Para obter mais detalhes sobre &quot;App Transport Security&quot;, consulte a seguinte seção de [Documentos de pré-lançamento do iOS9 da Apple](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) e este [Discussão de Estouro de Pilha](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

## Desenvolvimento de aplicativos móveis no AEM {#developing-mobile-applications-in-aem-1}

* [Iniciando o AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [Desenvolvimento de aplicativos móveis](/help/mobile/building-app-mobile-phonegap.md)
* [Estruturar um aplicativo](/help/mobile/phonegap-structure-an-app.md)
* [Criação e edição de aplicativos usando o console Aplicativos](/help/mobile/phonegap-apps-console.md)
* [Aplicativos de página única](/help/mobile/phonegap-single-page-applications.md)
* [Desenvolvimento de aplicativos com a CLI do PhoneGap](/help/mobile/phonegap-apps-pg-cli.md)
* [Recursos do dispositivo de acesso](/help/mobile/phonegap-access-device-features.md)
* [Acompanhe o desempenho do aplicativo com o Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
* [Adicionar o Adobe Analytics ao seu aplicativo para dispositivos móveis](/help/mobile/phonegap-add-analytics-to-apps.md)
* [Notificações push](/help/mobile/phonegap-push-notifications.md)
* [Personalização de conteúdo do AEM Mobile](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [A anatomia de um aplicativo](/help/mobile/phonegap-apps-arch.md)
* [Seu aplicativo híbrido está pronto para o AEM Mobile?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Criação para Adobe PhoneGap Enterprise com AEM](/help/mobile/phonegap.md)
* [Administração de conteúdo para o Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)
