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
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Configurar ambiente para o aplicativo AEM Forms{#set-up-environment-for-aem-forms-app}

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
* Se o ADT estiver instalado em qualquer outro local no Mac ou se o ambiente estiver configurado em um sistema Windows, o caminho do SDK do ADT deverá ser atualizado no arquivo `local.properties`. Este arquivo está disponível na pasta `src\android` no arquivo morto de origem `mobileworkspace-src.zip` extraído. Neste arquivo, aponte a variável `sdk.dir` para o local do SDK do ADT na área de trabalho.

>[!NOTE]
>
>O adobe-lc-mobileworkspace-src.zip contém PhoneGap SDK 5.0. Verifique se o SDK do PhoneGap não está pré-instalado.
