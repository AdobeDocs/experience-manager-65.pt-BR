---
title: Desenvolvimento de aplicativos móveis em AEM
seo-title: Desenvolvimento de aplicativos móveis em AEM
description: Siga esta página para desenvolver aplicativos móveis de start em AEM usando o Adobe PhoneGap Enterprise.
seo-description: Siga esta página para desenvolver aplicativos móveis de start em AEM usando o Adobe PhoneGap Enterprise.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# Desenvolvimento de aplicativos móveis em AEM {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

AEM aproveita a Adobe PhoneGap e a Adobe Publishing Solutions, permitindo que você crie e gerencie aplicativos móveis ricos em conteúdo e baseados em utilitários:

* Gerencie todos os aplicativos móveis do empresa em um único lugar.
* Revise os aplicativos em ambientes de desenvolvimento e armazenamento temporário sem as complexidades de perfis de provisionamento e o esforço extra para criar e carregar seu aplicativo para compartilhamento.
* Use o ambiente de criação de AEM para criar e gerenciar conteúdo avançado para seus aplicativos.
* Use o HTML5 com Adobe PhoneGap para criar experiências avançadas com recursos nativos do dispositivo.
* Apresente webviews HTML5 a aplicativos **nativos** novos ou pré-existentes por meio do Cordova WebViews.
* Crie, prepare e compartilhe conteúdo multimídia avançado em todos os canais de delivery, incluindo Web, Web móvel, aplicativo móvel e impressão.

AEM integra-se com o Adobe **[serviço de PhoneGap Build](https://build.phonegap.com/)** para simplificar o processo de criação e implantação de aplicativos.

**Adobe** ContentSyncenpermite que os usuários baixem facilmente as atualizações de página e conteúdo Over-the-Air (OTA) em seus dispositivos sem precisar reinstalar o aplicativo ou baixar da appStore, do Google Play ou de outras fontes de aplicativos.

**O Adobe** Analytics está totalmente integrado aos aplicativos AEM e permite o rastreamento detalhado da distribuição, localização geográfica, sistemas operacionais, dispositivos, streams de cliques, rastreamento do iBeacon e muito mais.

## Criação de aplicativos {#creating-apps}

Os desenvolvedores podem usar o [AEM PhoneGap Starter Kit](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) juntamente com recursos adicionais encontrados em [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) para inicializar AEM aplicativos com PhoneGap, incluindo um aplicativo nativo de referência que executa Visualizações Web do Cordova.

O readme para o repositório do Starter Kit Git inclui um tutorial para o uso do kit inicial:

* Personalizar a marca
* Públicos alvos de criação e implantação de amostra
* Configuração do repositório do controle de origem
* Instalar e implantar em instâncias de AEM locais ou remotas
* Desinstalar do AEM

>[!NOTE]
>
>A fonte de implementação de referência adicional, incluindo laboratórios, pode ser encontrada no GitHub [aqui](https://github.com/adobe-marketing-cloud-apps) e, a fonte de &quot;dissipador de cozinha&quot; [aqui](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Desenvolvimento para hosts IOS 9 e HTTP {#developing-for-ios-and-http-hosts}

Os desenvolvedores do IOS devem estar cientes de um problema aberto com aplicativos do Cordova em execução no iOS 9. Esse problema impede que solicitações sejam feitas em hosts inseguros (como *http://localhost:4502*). Esse problema será resolvido com uma próxima versão do cordova-ios (consumida pela CLI do Cordova), mas, entretanto, há duas soluções alternativas disponíveis:

1. Como uma solução alternativa imediata, você ainda pode usar qualquer um dos simuladores iOS 8 sem problemas.
1. Se você precisar usar o iOS 9, seu arquivo apps -Info.plist (encontrado após executar `cordova platform add ios` em &quot;&lt;app root>/platform/ios/&lt;app name>/&lt;app name>-Info.plist&quot;) pode ser editado manualmente para incluir a seguinte propriedade:

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Para obter mais detalhes sobre &quot;App Transport Security&quot;, consulte a seguinte seção de [documentos de pré-lançamento do iOS9 da Apple](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) e esta [discussão sobre estouro de pilha](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

## Desenvolvimento de aplicativos móveis em AEM {#developing-mobile-applications-in-aem-1}

* [Iniciando AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [Criação de aplicativos móveis](/help/mobile/building-app-mobile-phonegap.md)
* [Estruturar um aplicativo](/help/mobile/phonegap-structure-an-app.md)
* [Criação e edição de aplicativos usando o console Aplicativos](/help/mobile/phonegap-apps-console.md)
* [Aplicativos de página única](/help/mobile/phonegap-single-page-applications.md)
* [Desenvolvimento de aplicativos com CLI PhoneGap](/help/mobile/phonegap-apps-pg-cli.md)
* [Recursos do dispositivo de acesso](/help/mobile/phonegap-access-device-features.md)
* [Acompanhe o desempenho do aplicativo com o Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
* [Adicionar Adobe Analytics ao seu aplicativo móvel](/help/mobile/phonegap-add-analytics-to-apps.md)
* [Notificações push](/help/mobile/phonegap-push-notifications.md)
* [Personalização de conteúdo do AEM Mobile](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [Anatomia de um aplicativo](/help/mobile/phonegap-apps-arch.md)
* [Seu aplicativo híbrido está pronto para AEM Mobile?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Criação para Adobe PhoneGap Enterprise com AEM](/help/mobile/phonegap.md)
* [Administração de conteúdo para Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)
