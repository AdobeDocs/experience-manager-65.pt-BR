---
title: Criação de um aplicativo AEM Forms seguro para iOS
seo-title: Criação de um aplicativo AEM Forms seguro para iOS
description: Etapas para criar um aplicativo AEM Forms seguro.
seo-description: Etapas para criar um aplicativo AEM Forms seguro.
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---


# Criação de um aplicativo AEM Forms seguro para iOS {#building-a-secure-aem-forms-app-for-ios}

É necessário arquivar o projeto Xcode para o aplicativo AEM Forms para criar o instalador (um arquivo .ipa) e uma lista de propriedade (um arquivo .plist). O arquivo de lista de propriedade contém informações de configuração do aplicativo interno hospedado, como o nome e o local de hospedagem do aplicativo. Para obter mais informações sobre o arquivo de lista de propriedade, consulte [Sobre arquivos de Lista de propriedades de informações](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Faça logon no seguinte site:

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. Criar uma ID do aplicativo. Para obter etapas detalhadas para criar uma ID do aplicativo, consulte [Criar e configurar IDs do aplicativo](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. Para configurar o identificador do pacote para o aplicativo iOS para seu aplicativo, clique em **[!UICONTROL Configurar ID do aplicativo]**.
1. Na parte inferior da página da Web, selecione **[!UICONTROL Ativar para Proteção de Dados]**. Especifique as opções de proteção de dados.

   Clique em **[!UICONTROL Concluído]**.

1. Navegue até Provisionamento->Distribuição e crie um novo Perfil usando a ID do aplicativo configurada na etapa 3.
1. Baixe e adicione o perfil de provisionamento ao Xcode e ao iPad.
1. Faça logon em sua máquina Mac com o Xcode e o SDK do iOS instalado e configurado.
1. Abra o projeto `AEM Forms.xcodeproj` no Xcode.
1. Clique em **[!UICONTROL AEM Forms]**, em **[!UICONTROL PÚBLICOS ALVOS]**, selecione **[!UICONTROL AEM Forms]**. Selecione a guia **[!UICONTROL Criar configurações]**, localize a seção **[!UICONTROL Direito de assinatura de código]** e, na lista suspensa Direitos, selecione a opção **[!UICONTROL LC Enterprise]**.
1. Localize e abra o arquivo `LC Enterprise.entitlements` no Xcode para edição. Em **Direitos XCode**, adicione o mesmo par de valores chave que está presente no perfil de provisionamento.
1. Na guia **[!UICONTROL Build Settings]**, clique em **[!UICONTROL Todos]** e em **[!UICONTROL Combinado]**.
1. Na lista **[!UICONTROL Settings]**, expanda **[!UICONTROL Assinatura de código]**.
1. Para **[!UICONTROL Identidade de assinatura de código]**, selecione a assinatura apropriada. Certifique-se de que a mesma assinatura esteja selecionada para **[!UICONTROL Depurar]**, **[!UICONTROL Versão]** e **[!UICONTROL Qualquer SDK do iOS]**.
1. Em **[!UICONTROL PROJECT]**, selecione **[!UICONTROL AEM Forms]** e certifique-se de que a assinatura apropriada está selecionada para **[!UICONTROL Identidade de assinatura de código]**, **[!UICONTROL Depurar]**, **[!UICONTROL Versão]** e **[!UICONTROL Qualquer SDK do iOS&lt;a1111111/>.]**
1. Crie e distribua aplicativos AEM Forms. Para obter instruções detalhadas sobre como criar e distribuir aplicativos AEM Forms, consulte [Criar o instalador para aplicativos AEM Forms](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
