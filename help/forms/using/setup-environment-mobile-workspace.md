---
title: Configurar ambiente para o aplicativo AEM Forms
description: Hardware, software e licenças para criar e implantar o aplicativo AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%
---
# Configurar ambiente para o aplicativo AEM Forms{#set-up-environment-for-aem-forms-app}

>[!NOTE]
>
>O aplicativo AEM Forms está obsoleto no momento. Para perguntas ou ajuda, contate [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

Você precisa do seguinte hardware, software e licenças para criar e implantar o aplicativo AEM Forms:

## Para dispositivos Windows {#for-windows-devices}

* Microsoft® Windows 10
* Microsoft® Visual Studio 2015
* Ferramentas do Microsoft® Visual Studio para Apache Cordova

## Para dispositivos iOS {#for-ios-devices}

* Mac Apple baseado em Intel executando o macOS X 10.9.5 ou superior
* iOS SDK 8.4 ou superior
* Versão do Xcode: Xcode 6.4 para OS X ou superior
* Associação ao programa iOS Developer Enterprise
* Certificado empresarial para distribuição de aplicativos iOS internos
* Apple iPad com iOS 8.4 ou posterior

## Para dispositivos Android™ {#for-android-devices}

* Android™ Development Toolkit (pacote ADT) que pode ser baixado de [https://developer.android.com/studio](https://developer.android.com/studio)
* Se o ambiente estiver configurado em um sistema Mac, o ADT deverá ser instalado na pasta Aplicativos.
* Se o ADT estiver instalado em qualquer outro local no Mac ou se o ambiente estiver configurado em um sistema Windows, o caminho do ADT SDK deverá ser atualizado no arquivo `local.properties`. Este arquivo está disponível na pasta `src\android` no arquivo morto de origem `mobileworkspace-src.zip` extraído. Neste arquivo, aponte a variável `sdk.dir` para a localização do ADT SDK na área de trabalho.

>[!NOTE]
>
>O adobe-lc-mobileworkspace-src.zip contém o PhoneGap SDK 5.0. Verifique se o PhoneGap SDK não está pré-instalado.
