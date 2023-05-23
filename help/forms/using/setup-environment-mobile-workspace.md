---
title: Configurar ambiente para o aplicativo AEM Forms
seo-title: Set up environment for AEM Forms app
description: Hardware, software e licenças para criar e implantar o aplicativo AEM Forms.
seo-description: Hardware, software, and licenses to build and deploy the AEM Forms app.
uuid: 4123a6b7-5766-476c-9afb-f57029b148ad
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e6b01ade-7ea3-42a7-872d-cc35a3d2782a
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Configurar ambiente para o aplicativo AEM Forms{#set-up-environment-for-aem-forms-app}

Você precisa do seguinte hardware, software e licenças para criar e implantar o aplicativo AEM Forms:

## Para dispositivos Windows {#for-windows-devices}

* Microsoft Windows 10
* Microsoft Visual Studio 2015
* Ferramentas do Microsoft Visual Studio para Apache Cordova

## Para dispositivos iOS {#for-ios-devices}

* Mac Apple baseado em Intel executando o Mac OS X 10.9.5 ou superior
* iOS SDK 8.4 ou superior
* Versão do Xcode: Xcode 6.4 para OS X ou superior
* Associação ao programa iOS Developer Enterprise
* Certificado empresarial para distribuição de aplicativos iOS internos
* Apple iPad com iOS 8.4 ou posterior

## Para dispositivos Android {#for-android-devices}

* Android Development Toolkit (pacote ADT) que pode ser baixado em [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)
* Se o ambiente estiver configurado em um sistema MAC, o ADT deverá ser instalado na pasta Aplicativos.
* Se o ADT estiver instalado em qualquer outro local no MAC ou se o ambiente estiver configurado em um sistema Windows, o caminho do SDK do ADT precisará ser atualizado em `local.properties` arquivo que está disponível em `src\android` pasta no arquivo de origem extraído `mobileworkspace-src.zip`. Neste arquivo, aponte para `sdk.dir` variável para o local do SDK do ADT no desktop.

>[!NOTE]
>
>O adobe-lc-mobileworkspace-src.zip contém PhoneGap SDK 5.0. Verifique se o SDK do PhoneGap não está pré-instalado.
