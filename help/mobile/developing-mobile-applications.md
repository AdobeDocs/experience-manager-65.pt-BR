---
title: Desenvolvimento de aplicativos móveis no AEM
seo-title: Developing Mobile Applications in AEM
description: Siga esta página para começar a desenvolver aplicativos móveis no AEM usando o Adobe PhoneGap Enterprise.
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
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

O AEM aproveita as soluções de publicação do Adobe PhoneGap e do Adobe, permitindo criar e gerenciar aplicativos móveis de várias plataformas, ricos em conteúdo e utilitários:

* Gerencie todos os aplicativos móveis de sua empresa em um único lugar.
* Revise aplicativos em ambientes de desenvolvimento e de preparo sem as complexidades dos perfis de provisionamento e o esforço extra para criar e carregar seu aplicativo para compartilhamento.
* Use o ambiente de criação de AEM para criar e gerenciar conteúdo avançado para seus aplicativos.
* Use o HTML5 com Adobe PhoneGap para criar experiências avançadas com recursos nativos do dispositivo.
* Apresente webviews do HTML5 para novas ou pré-existentes **nativo** aplicativos por meio do Cordova WebViews.
* Crie, prepare e compartilhe conteúdo multimídia rico em todos os canais de entrega, incluindo Web, Web móvel, aplicativo móvel e impressão.

AEM integra-se ao Adobe **[Serviço de PhoneGap Build](https://build.phonegap.com/)** para simplificar o processo de criação e implantação do aplicativo.

**Adobe ContentSync** permite que os usuários baixem facilmente atualizações de página e conteúdo no ar (OTA) para seus dispositivos sem precisar reinstalar o aplicativo ou baixar da appStore, Google Play ou outras fontes de aplicativos.

**Adobe Analytics** O é totalmente integrado aos AEM aplicativos e permite o rastreamento detalhado da distribuição, geolocalização, sistemas operacionais, dispositivos, fluxos de cliques, rastreamento iBeacon e muito mais.

## Criação de aplicativos {#creating-apps}

Os desenvolvedores podem usar o [AEM Kit inicial do PhoneGap](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) juntamente com recursos adicionais encontrados em [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) para inicializar AEM aplicativos com PhoneGap, incluindo um aplicativo nativo de referência que executa o Cordova Webviews.

O readme para o repositório Git do Starter Kit inclui um tutorial para o uso do kit inicial:

* Personalizar a marca
* Destinos de criação e implantação de amostra do Maven
* Configuração do repositório de controle de origem
* Instalar e implantar em instâncias de AEM locais ou remotas
* Desinstalar de AEM

>[!NOTE]
>
>Outra fonte de implementação de referência, incluindo laboratórios, pode ser encontrada no GitHub [here](https://github.com/adobe-marketing-cloud-apps) e, a fonte da &quot;pia de cozinha&quot; [here](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Desenvolvimento de hosts IOS 9 e HTTP {#developing-for-ios-and-http-hosts}

Os desenvolvedores do iOS devem estar cientes de um problema aberto com aplicativos Cordova em execução no iOS 9. Esse problema impede que solicitações sejam feitas em hosts inseguros (como *http://localhost:4502*). Esse problema será resolvido com uma versão futura do cordova-ios (consumida pela CLI do Cordova), mas enquanto isso, há duas soluções alternativas disponíveis:

1. Como solução alternativa imediata, ainda é possível usar qualquer um dos simuladores do iOS 8 sem problemas.
1. Se precisar usar o iOS 9, seus aplicativos - Info.plist (encontrado após a execução `cordova platform add ios` em &quot;&lt;app root=&quot;&quot;>/platform/ios/&lt;app name=&quot;&quot;>/&lt;app name=&quot;&quot;>-Info.plist&quot;) pode ser editado manualmente para incluir a seguinte propriedade:

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Para obter mais detalhes sobre &quot;App Transport Security&quot;, consulte a seguinte seção de [Documentos de pré-lançamento do iOS9 da Apple](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) e isto [discussão sobre estouro de pilha](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

## Desenvolvimento de aplicativos móveis no AEM {#developing-mobile-applications-in-aem-1}

* [Iniciando AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [Criação de aplicativos móveis](/help/mobile/building-app-mobile-phonegap.md)
* [Estrutura de um aplicativo](/help/mobile/phonegap-structure-an-app.md)
* [Criação e edição de aplicativos usando o console Aplicativos](/help/mobile/phonegap-apps-console.md)
* [Aplicativos de página única](/help/mobile/phonegap-single-page-applications.md)
* [Desenvolvimento de aplicativos com CLI PhoneGap](/help/mobile/phonegap-apps-pg-cli.md)
* [Acessar recursos do dispositivo](/help/mobile/phonegap-access-device-features.md)
* [Rastrear o desempenho do aplicativo com o Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
* [Adicionar o Adobe Analytics ao seu aplicativo móvel](/help/mobile/phonegap-add-analytics-to-apps.md)
* [Notificações push](/help/mobile/phonegap-push-notifications.md)
* [Personalização de conteúdo do AEM Mobile](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [A Anatomia de um aplicativo](/help/mobile/phonegap-apps-arch.md)
* [O seu aplicativo híbrido está pronto para o AEM Mobile?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Criação para Adobe PhoneGap Enterprise com AEM](/help/mobile/phonegap.md)
* [Administração de conteúdo para Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)
