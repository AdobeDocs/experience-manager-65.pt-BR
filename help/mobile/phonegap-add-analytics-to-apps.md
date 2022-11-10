---
title: Adicionar o Adobe Analytics ao seu aplicativo móvel
seo-title: Add Adobe Analytics to your Mobile Application
description: Siga esta página para saber mais sobre como usar a Análise de aplicativos móveis em seus aplicativos AEM ao integrar com o Adobe Mobile Services.
seo-description: Follow this page to learn about how you can use Mobile App Analytics in your AEM Apps by integrating with Adobe Mobile Services.
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# Adicionar o Adobe Analytics ao seu aplicativo móvel{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Deseja criar experiências envolventes e relevantes para os usuários de aplicativos móveis? Se você não estiver usando o SDK do Adobe Mobile Services para monitorar e medir o ciclo de vida e o uso do aplicativo, em que você está baseando suas decisões? Onde estão seus clientes mais fiéis? Como você pode garantir que permanece relevante e que otimiza as conversões?

Seus usuários estão acessando todo o conteúdo? Eles estão abandonando o aplicativo e, em caso afirmativo, onde? Com que frequência eles ficam no aplicativo e com que frequência eles voltam para usar o aplicativo? Que alterações você pode introduzir e medir que aumentam a retenção? E quanto às taxas de falhas, seu aplicativo está travando para seus usuários?

Tire proveito de [Análise de aplicativos móveis](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) em seus aplicativos AEM, integrando com [Adobe Mobile Services](https://www.adobe.com/marketing-cloud/mobile-marketing.html).

Integre seus aplicativos de AEM para rastrear, relatar e entender como os usuários interagem com seu aplicativo e conteúdo móveis e para medir medições de ciclo de vida importantes, como inicializações, tempo no aplicativo e taxa de falha.

Esta seção descreve como AEM *Desenvolvedores* pode:

* Integre o Mobile Analytics ao seu aplicativo móvel
* Testar o rastreamento de análises com o Bloodhound

## Pré-requisitos {#prerequisties}

O AEM Mobile requer uma conta do Adobe Analytics para coletar e relatar dados de rastreamento no aplicativo. Como parte da configuração do AEM *Administrador* precisará primeiro de :

* Configure uma conta do Adobe Analytics e crie um conjunto de relatórios para seu aplicativo no Mobile Services.
* Configure um AMS Cloud Service no Adobe Experience Manager (AEM).

## Para desenvolvedores - Integre o Mobile Analytics ao seu aplicativo {#for-developers-integrate-mobile-analytics-into-your-app}

### Configurar o ContentSync para obter o arquivo de configuração {#configure-contentsync-to-pull-in-configuration-file}

Após a configuração da conta do Analytics, é necessário criar uma configuração de Sincronização de conteúdo para inserir o conteúdo no aplicativo móvel.

Para obter mais detalhes, consulte Configuração do conteúdo de sincronização. A configuração precisará instruir a Sincronização de conteúdo para colocar ADBMobileConfig no diretório /www. Por exemplo, no aplicativo Geometrixx Outdoors, a configuração da Sincronização de conteúdo está localizada em: */content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-config/ams-ADBMobileConfig*. Há também uma configuração para o desenvolvimento; no entanto, é idêntica à configuração de não desenvolvimento no caso de Geometrixx Outdoors.

Para obter mais detalhes sobre como baixar o ADBMobileConfig do painel Aplicativos do Mobile Application AEM, consulte Arquivo de configuração do SDK do Analytics - Mobile Services - Adobe Mobile Services .

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

Cada plataforma requer que ADBMobileConfig seja copiado para um local específico.

Se estiver criando com a CLI do PhoneGap, isso pode ser feito com um script de gancho de compilação do cordova. Isso pode ser visto no aplicativo Geometrixx Outdoors em:*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

Para o iOS, o arquivo precisará ser copiado para o **Recursos** diretório (por exemplo, &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;). Se o aplicativo for direcionado para Android, o caminho para o qual copiar será &quot;platforms/android/assets/ADBMobileConfig.json&quot;. Para obter mais detalhes sobre o uso de ganchos durante a build da CLI do PhoneGap, consulte [Três ganchos que seu projeto Cordova/PhoneGap precisa](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/).

```xml
///////////////////////////
//          iOS
///////////////////////////
    ios : [
        {
            "www/ADBMobileConfig.json": "platforms/ios/<YOUR_APP_NAME>/Resources/ADBMobileConfig.json"
        }
    ],
///////////////////////////
//          ANDROID
///////////////////////////
    android: [
        {
            "www/ADBMobileConfig.json": "platforms/android/assets/ADBMobileConfig.json"
        }
    ]
```

### Adicionar o plug-in AMS no aplicativo {#add-the-ams-plugin-in-the-app}

Para que o aplicativo colete os dados, o plug-in Adobe Mobile Services (AMS) precisa ser incluído como parte do aplicativo. Ao incluir o plug-in como um recurso no config.xml do aplicativo, outro gancho do Cordova pode ser usado para adicionar automaticamente o plug-in durante o processo de compilação do PhoneGap.

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

O Geometrixx Outdoors App config.xml está localizado em */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. O exemplo acima solicita uma versão específica do plug-in a ser usada adicionando um &#39;#&#39; e um valor de tag após o URL do plug-in. Essa é uma boa prática a ser seguida para garantir que problemas não esperados não apareçam devido à adição de plug-ins não testados durante uma criação.

Após executar essas etapas, seu aplicativo será ativado para relatar todas as medições de ciclo de vida fornecidas pelo Adobe Analytics. Isso inclui dados como inicializações, falhas e instalações. Se esses são os únicos dados com os quais você se preocupa então você está pronto. Se quiser coletar dados personalizados, será necessário instrumentar seu código.

### Instrumente seu código para o rastreamento completo do aplicativo {#instrument-your-code-for-full-app-tracking}

Há várias APIs de rastreamento fornecidas no [API de plug-in do Phonegap do AMS.](https://experienceleague.adobe.com/docs/mobile-services/ios/phonegap-ios/phonegap-methods.html)

Isso permitirá rastrear estados e ações, como onde páginas os usuários estão navegando no aplicativo, quais controles estão sendo mais usados. A maneira mais fácil de instruir seu aplicativo para rastreamento é usar as APIs do Analytics fornecidas pelo plug-in do AMS.

* ADB.trackState()
* ADB.trackAction()

Para referência, consulte o código no aplicativo Geometrixx Outdoors. No aplicativo Geometrixx Outdoors, todas as navegações da página são rastreadas usando o método ADB.trackState() . Para obter mais detalhes, consulte o código-fonte de /libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js

Ao instrumentar seu código-fonte com essas chamadas de método, você pode coletar métricas completas em relação ao seu aplicativo.

#### Propriedades para conexão com o AMS {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.MobileServicesHttpClientImp* l expõe as seguintes propriedades para conexão com o AMS:

| **Etiqueta** | **Descrição** | **Padrão** |
|---|---|---|
| Endpoint da API | O URL básico das APIs HTTP do Adobe Mobile Services | https://api.omniture.com |
| Endpoint de configuração | O URL usado para recuperar a Configuração móvel do ADB para a ID de conjunto de relatórios específica | /ams/1.0/app/config/ |
| Aplicativos do Mobile Service | Obter uma lista de aplicativos dentro da empresa de usuários | /ams/1.0/apps |
