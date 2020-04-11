---
title: Configurar o ambiente para o aplicativo AEM Forms
seo-title: Configurar o ambiente para o aplicativo AEM Forms
description: Hardware, software e licenças para criar e implantar o aplicativo AEM Forms.
seo-description: Hardware, software e licenças para criar e implantar o aplicativo AEM Forms.
uuid: 4123a6b7-5766-476c-9afb-f57029b148ad
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e6b01ade-7ea3-42a7-872d-cc35a3d2782a
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Configurar o ambiente para o aplicativo AEM Forms{#set-up-environment-for-aem-forms-app}

Você precisa do seguinte hardware, software e licenças para criar e implantar o aplicativo AEM Forms:

## Para dispositivos Windows {#for-windows-devices}

* Microsoft Windows 10
* Microsoft Visual Studio 2015
* Ferramentas do Microsoft Visual Studio para o Apache Cordova

## Para dispositivos iOS {#for-ios-devices}

* Apple Mac baseado em Intel executando Mac OS X 10.9.5 ou superior
* iOS SDK 8.4 ou superior
* Versão Xcode: Xcode 6.4 para OS X ou superior
* Associação ao programa corporativo para desenvolvedores iOS
* Certificado empresarial para distribuição de aplicativos iOS internos
* Apple iPad com iOS 8.4 ou posterior

## Para dispositivos Android {#for-android-devices}

* Android Development Toolkit (pacote ADT) que pode ser baixado de [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)
* Se o ambiente estiver configurado em um sistema MAC, o ADT deverá ser instalado na pasta Aplicativos.
* Se o ADT estiver instalado em qualquer outro local no MAC, ou se o ambiente estiver configurado em um sistema Windows, o caminho do SDK do ADT precisa ser atualizado no `local.properties` arquivo disponível na `src\android` pasta no arquivo de origem extraído `mobileworkspace-src.zip`. Neste arquivo, aponte a `sdk.dir` variável para o local do ADT SDK em sua área de trabalho.

>[!NOTE]
>
>O adobe-lc-mobileworkspace-src.zip contém o PhoneGap SDK 5.0. Certifique-se de que o SDK do PhoneGap não esteja pré-instalado.
