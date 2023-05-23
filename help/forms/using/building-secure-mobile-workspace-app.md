---
title: Criação de um aplicativo AEM Forms seguro para o iOS
seo-title: Building a secure AEM Forms app for iOS
description: Etapas para criar um aplicativo AEM Forms seguro.
seo-description: Steps to build a secure AEM Forms app.
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
exl-id: 12cc2027-ae94-40c3-a7d1-553469426114
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# Criação de um aplicativo AEM Forms seguro para o iOS {#building-a-secure-aem-forms-app-for-ios}

Você precisa arquivar o projeto Xcode para o aplicativo AEM Forms para criar o instalador (um arquivo .ipa) e um arquivo de lista de propriedades (um arquivo .plist). O arquivo de lista de propriedades contém informações de configuração do aplicativo interno hospedado, como o nome e o local de hospedagem do aplicativo. Para obter mais informações sobre o arquivo de lista de propriedades, consulte [Sobre os Arquivos da Lista de Propriedades de Informações](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Faça logon no seguinte site:

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. Criar uma ID do aplicativo. Para obter etapas detalhadas sobre como criar uma ID do aplicativo, consulte [Criação e configuração de IDs de aplicativos](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. Para configurar o identificador do pacote para o aplicativo iOS para seu aplicativo, clique em **[!UICONTROL Configurar ID do aplicativo]**.
1. Na parte inferior da página da Web, selecione **[!UICONTROL Ativar para proteção de dados]**. Especifique as opções de proteção de dados.

   Clique em **[!UICONTROL Concluído]**.

1. Navegue até Provisionamento -> Distribuição e crie um Novo perfil usando a ID do aplicativo configurada na etapa 3.
1. Baixe e adicione o perfil de provisionamento ao Xcode e ao iPad.
1. Faça logon no computador Mac que tem o Xcode e o SDK do iOS instalado e configurado.
1. Abra o `AEM Forms.xcodeproj` projeto no Xcode.
1. Clique em **[!UICONTROL AEM Forms]**, em **[!UICONTROL METAS]**, selecione **[!UICONTROL AEM Forms]**. Selecione o **[!UICONTROL Configurações de build]** localize o **[!UICONTROL Direito de assinatura de código]** e, na lista suspensa Direitos, selecione a variável **[!UICONTROL LC Enterprise]** opção.
1. Localize e abra o `LC Enterprise.entitlements` no Xcode para edição. No **Direitos do XCode**, adicione o mesmo par de valor-chave presente no perfil de provisionamento.
1. No **[!UICONTROL Configurações de build]** clique em **[!UICONTROL Todos]** e clique em **[!UICONTROL Combinado]**.
1. No **[!UICONTROL Configurações]** listar, expandir **[!UICONTROL Assinatura de código]**.
1. Para **[!UICONTROL Identidade de assinatura de código]**, selecione a assinatura apropriada. Certifique-se de que a mesma assinatura esteja selecionada para **[!UICONTROL Depurar]**, **[!UICONTROL Versão]**, e **[!UICONTROL Qualquer SDK do iOS]**.
1. Em **[!UICONTROL PROJETO]**, selecione **[!UICONTROL AEM Forms]** e garantir que a assinatura apropriada seja selecionada para **[!UICONTROL Identidade de assinatura de código]**, **[!UICONTROL Depurar]**, **[!UICONTROL Versão]** e **[!UICONTROL Qualquer SDK do iOS]**.
1. Criar e distribuir o aplicativo AEM Forms. Para obter instruções detalhadas sobre como criar e distribuir o aplicativo AEM Forms, consulte [Criar o instalador do aplicativo AEM Forms](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
