---
title: Adicionar o Adobe Analytics ao seu aplicativo para dispositivos móveis
description: Siga esta página para saber mais sobre como você pode usar o Mobile App Analytics nos seus aplicativos Adobe Experience Manager ao integrar com o Adobe Mobile Services.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 0%

---

# Adicionar o Adobe Analytics ao seu aplicativo para dispositivos móveis{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Deseja criar experiências envolventes e relevantes para os usuários de aplicativos móveis? Se você não estiver usando o SDK do Adobe Mobile Services para monitorar e medir o ciclo de vida e o uso do aplicativo, em que você está baseando suas decisões? Onde estão seus clientes mais fiéis? Como você pode garantir que continua relevante e otimiza conversões?

Seus usuários estão acessando todo o conteúdo? Eles estão abandonando o aplicativo e, em caso afirmativo, onde? Com que frequência eles ficam no aplicativo e com que frequência voltam para usar o aplicativo? Que alterações você pode introduzir e, então, medir que aumentam a retenção? E as taxas de falha? Seu aplicativo está falhando para seus usuários?

Aproveite [Análise de aplicativos móveis](https://business.adobe.com/products/analytics/mobile-marketing.html) em seus aplicativos Adobe Experience Manager (AEM) ao integrar com a [Adobe Mobile Services](https://business.adobe.com/products/campaign/mobile-marketing.html).

Instrumente seus aplicativos AEM para rastrear, relatar e entender como seus usuários se envolvem com seu aplicativo móvel e conteúdo e para medir as principais métricas de ciclo de vida, como inicializações, tempo no aplicativo e taxa de falha.

Esta seção descreve como o AEM *Desenvolvedores* pode:

* Integrar o Mobile Analytics no aplicativo móvel
* Teste o rastreamento de análise com o Bloodhound

## Pré-requisitos {#prerequisties}

O AEM Mobile exige uma conta da Adobe Analytics para coletar e relatar dados de rastreamento no seu aplicativo. Como parte da configuração, o AEM *Administrador* deve primeiro:

* Configure uma conta do Adobe Analytics e crie um conjunto de relatórios para seu aplicativo no Mobile Services.
* Configurar um Cloud Service AMS no Adobe Experience Manager (AEM).

## Para desenvolvedores - Integre o Mobile Analytics ao seu aplicativo {#for-developers-integrate-mobile-analytics-into-your-app}

### Configurar ContentSync para extrair o arquivo de configuração {#configure-contentsync-to-pull-in-configuration-file}

Depois que a conta do Analytics for configurada, crie uma configuração de Sincronização de conteúdo para transferir o conteúdo para o aplicativo móvel.

Para obter detalhes adicionais, consulte Configuração do conteúdo da sincronização de conteúdo. A configuração deve instruir a Sincronização de conteúdo a colocar o ADBMobileConfig no diretório /www. Por exemplo, no aplicativo Geometrixx Outdoors, a configuração da Sincronização de conteúdo está em: */content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-config/ams-ADBMobileConfig*. Também há uma configuração para desenvolvimento. No entanto, é idêntica à configuração que não é de desenvolvimento, se houver Geometrixx Outdoors.

Para obter mais detalhes sobre como baixar o ADBMobileConfig no painel de aplicativos do AEM para aplicativos móveis, consulte Analytics - Mobile Services - Adobe Mobile Services SDK Config File.

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

Cada plataforma exige que o ADBMobileConfig seja copiado para um local específico.

Se estiver criando com a CLI do PhoneGap, isso pode ser feito com um script de gancho de criação do cordova. Isso pode ser visto no aplicativo Geometrixx Outdoors em:*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

Para o iOS, o arquivo deve ser copiado para o do projeto XCode **Recursos** (por exemplo, &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;). Se o aplicativo for direcionado para Android™, o caminho para copiar será &quot;platforms/android/assets/ADBMobileConfig.json&quot;. Para obter mais detalhes sobre como usar ganchos durante a criação da CLI do PhoneGap, consulte [Três ganchos de que seu projeto Cordova/PhoneGap precisa](https://gist.github.com/jlcarvalho/22402d013bc72f795d45a01836ce735c).

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

Para que o aplicativo colete os dados, o plug-in do Adobe Mobile Services (AMS) precisa ser incluído como parte do aplicativo. Ao incluir o plug-in como um recurso no config.xml do aplicativo, outro gancho Cordova pode ser usado para adicionar automaticamente o plug-in durante o processo de criação do PhoneGap.

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

O aplicativo config.xml do Geometrixx Outdoors está localizado em */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. O exemplo acima solicita uma versão específica do plug-in a ser usada adicionando um &#39;#&#39; e, em seguida, um valor de tag após o URL do plug-in. Esta é uma boa prática a ser seguida para garantir que problemas não previstos não apareçam devido à adição de plug-ins não testados durante uma compilação.

Depois de executar essas etapas, seu aplicativo será ativado para relatar todas as medições de ciclo de vida fornecidas pelo Adobe Analytics. Isso inclui dados como inicializações, falhas e instalações. Se esse é o único dado com o qual você se importa, então você está pronto. Se quiser coletar dados personalizados, você deve instrumentar seu código.

### Instrumente seu código para um rastreamento completo do aplicativo {#instrument-your-code-for-full-app-tracking}

Há várias APIs de rastreamento fornecidas no [API do plug-in AMS Phonegap.](https://github.com/Adobe-Marketing-Cloud/mobile-services/blob/master/docs/ios/phonegap/phonegap-methods.md)

Isso permitirá rastrear estados e ações, como para onde os usuários estão navegando em seu aplicativo, quais controles estão sendo mais usados. A maneira mais fácil de instrumentar seu aplicativo para rastreamento é usar as APIs do Analytics fornecidas pelo plug-in AMS.

* ADB.trackState()
* ADB.trackAction()

Para referência, verifique o código no aplicativo Geometrixx Outdoors. No aplicativo Geometrixx Outdoors, toda a navegação da página é rastreada usando o método ADB.trackState(). Para obter mais detalhes, consulte o código-fonte de /libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js

Ao instrumentar seu código-fonte com essas chamadas de método, você pode coletar métricas completas em relação ao seu aplicativo.

#### Propriedades para conexão com o AMS {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.MobileServicesHttpClientImp* l expõe as seguintes propriedades para conexão com o AMS:

| **Etiqueta** | **Descrição** | **Padrão** |
|---|---|---|
| Endpoint da API | O URL de base das APIs HTTP do Adobe Mobile Services | https://api.omniture.com |
| Endpoint de configuração | O URL usado para recuperar a Configuração móvel ADB para a ID de conjunto de relatórios fornecida | /ams/1.0/app/config/ |
| Aplicativos do Mobile Services | Obter uma lista de aplicativos na empresa dos usuários | /ams/1.0/apps |
