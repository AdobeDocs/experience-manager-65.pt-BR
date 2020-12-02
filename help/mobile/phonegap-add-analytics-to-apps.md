---
title: Adicionar Adobe Analytics ao seu aplicativo móvel
seo-title: Adicionar Adobe Analytics ao seu aplicativo móvel
description: Siga esta página para saber mais sobre como você pode usar o Mobile App Analytics em seus aplicativos AEM por meio da integração com o Adobe Mobile Services.
seo-description: Siga esta página para saber mais sobre como você pode usar o Mobile App Analytics em seus aplicativos AEM por meio da integração com o Adobe Mobile Services.
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
translation-type: tm+mt
source-git-commit: 8279cd590244a7f2d20cfaf1c7505a3ef57fae4a
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# Adicionar Adobe Analytics ao seu aplicativo móvel{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Deseja criar experiências envolventes e relevantes para seus usuários de aplicativos móveis? Se você não estiver usando o SDK do Adobe Mobile Services para monitorar e medir o ciclo de vida e o uso do aplicativo, então em que você baseia suas decisões? Onde estão seus clientes mais leais? Como você pode garantir que está se mantendo relevante e otimizando as conversões?

Seus usuários estão acessando todo o conteúdo? Eles estão abandonando o aplicativo e, em caso afirmativo, onde? Com que frequência eles ficam no aplicativo e com que frequência voltam para usar o aplicativo? Que mudanças você pode introduzir e medir que aumentam a retenção? E quanto às taxas de falhas, seu aplicativo trava para seus usuários?

Aproveite as vantagens do [Mobile App Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) nos seus aplicativos AEM, integrando-se ao [Adobe Mobile Services](https://www.adobe.com/marketing-cloud/mobile-marketing.html).

Informe seus aplicativos AEM para rastrear, relatar e entender como os usuários se envolvem com seu aplicativo móvel e conteúdo, além de medir as principais medições de ciclo de vida, como inicializações, tempo no aplicativo e taxa de falhas.

Esta seção descreve como AEM *Desenvolvedores* podem:

* Integre o Mobile Analytics ao seu aplicativo móvel
* Teste o rastreamento de análises com o Bloodhound

## Pré-requisitos {#prerequisties}

A AEM Mobile exige uma conta da Adobe Analytics para coletar e relatar dados de rastreamento no aplicativo. Como parte da configuração, o AEM *Administrador* terá primeiro de:

* Configure uma conta da Adobe Analytics e crie um conjunto de relatórios para seu aplicativo no Mobile Services.
* Configure um Cloud Service AMS no Adobe Experience Manager (AEM).

## Para desenvolvedores - Integrar o Mobile Analytics ao seu aplicativo {#for-developers-integrate-mobile-analytics-into-your-app}

### Configure o ContentSync para obter o arquivo de configuração {#configure-contentsync-to-pull-in-configuration-file}

Depois que a conta do Analytics for configurada, será necessário criar uma configuração de Sincronização de conteúdo para inserir o conteúdo no aplicativo móvel.

Para obter detalhes adicionais, consulte Configuração do conteúdo de sincronização. A configuração precisará instruir a Sincronização de conteúdo para colocar ADBMobileConfig no diretório /www. Por exemplo, no aplicativo Geometrixx Outdoors, a configuração de Sincronização de conteúdo está localizada em: */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-config/ams-ADBMobileConfig*. Há também uma configuração para o desenvolvimento. no entanto, é idêntico à configuração de não desenvolvimento no caso de Geometrixx Outdoors.

Para obter mais detalhes sobre como baixar o ADBMobileConfig de seu painel de aplicativos AEM do aplicativo móvel, consulte Arquivo de configuração do Analytics - Mobile Services - Adobe Mobile Services.

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

Cada plataforma requer que o ADBMobileConfig seja copiado para um local específico.

Se estiver criando com a CLI do PhoneGap, isso pode ser feito com scripts de gancho de construção do cordova. Isso pode ser visto no aplicativo Geometrixx Outdoors em:*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

Para iOS, o arquivo precisará ser copiado para o diretório **Resources** do projeto XCode (por exemplo, &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;). Se o aplicativo for direcionado para Android, o caminho para copiar será &quot;platforms/android/assets/ADBMobileConfig.json&quot;. Para obter mais detalhes sobre como usar ganchos durante a compilação da CLI do PhoneGap, consulte [Três ganchos necessários para o projeto do Cordova/PhoneGap](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/).

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

Para que o aplicativo colete os dados, o plug-in Adobe Mobile Services (AMS) precisa ser incluído como parte do aplicativo. Ao incluir o plug-in como um recurso no config.xml do aplicativo, outro gancho do Cordova pode ser usado para adicionar automaticamente o plug-in durante o processo de criação do PhoneGap.

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

O aplicativo Geometrixx Outdoors config.xml está localizado em */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. O exemplo acima solicita uma versão específica do plug-in a ser usado adicionando um &#39;#&#39; e, em seguida, um valor de tag após o URL do plug-in. Esta é uma boa prática a ser seguida para garantir que problemas não previstos não apareçam devido à adição de plug-ins não testados durante uma compilação.

Após executar essas etapas, seu aplicativo será habilitado a relatar todas as medições de ciclo de vida fornecidas pela Adobe Analytics. Isso inclui dados como inicializações, falhas e instalações. Se esses são os únicos dados com os quais você se importa então você está pronto. Se você quiser coletar dados personalizados, será necessário instrumentar seu código.

### Instrumento seu código para o rastreamento completo do aplicativo {#instrument-your-code-for-full-app-tracking}

Existem várias APIs de rastreamento fornecidas na [API Plugin do AMS Phonegap.](https://docs.adobe.com/content/help/en/mobile-services/ios/phonegap-ios/phonegap-methods.html)

Isso permitirá que você rastreie estados e ações, como para onde os usuários estão navegando no aplicativo, quais controles estão sendo mais usados. A maneira mais fácil de instruir seu aplicativo para rastreamento é usar as APIs do Analytics fornecidas pelo plug-in do AMS.

* ADB.trackState()
* ADB.trackAction()

Para referência, você pode observar o código no aplicativo Geometrixx Outdoors. No aplicativo Geometrixx Outdoors, todas as navegações de página são rastreadas usando o método ADB.trackState(). Para obter mais detalhes, consulte o código fonte para /libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js

Ao instrumentar seu código fonte com essas chamadas de método, você pode coletar métricas completas em relação ao seu aplicativo.

#### Propriedades para conexão com AMS {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.* MobileServicesHttpClientImpl expõe as seguintes propriedades para conexão com o AMS:

| **Etiqueta** | **Descrição** | **Padrão** |
|---|---|---|
| Ponto de extremidade da API | O URL básico das APIs HTTP do Adobe Mobile Services | https://api.omniture.com |
| Endpoint de configuração | O URL usado para recuperar a configuração do ADB Mobile para a ID de conjunto de relatórios fornecida | /ams/1.0/app/config/ |
| Aplicativos do Mobile Service | Obter uma lista de aplicativos na empresa dos usuários | /ams/1.0/apps |

