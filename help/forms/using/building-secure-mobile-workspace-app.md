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
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Criação de um aplicativo AEM Forms seguro para iOS {#building-a-secure-aem-forms-app-for-ios}

É necessário arquivar o projeto Xcode para o aplicativo AEM Forms para criar o instalador (um arquivo .ipa) e um arquivo de lista de propriedade (um arquivo .plist). O arquivo de lista de propriedade contém informações de configuração do aplicativo interno hospedado, como o nome e o local de hospedagem do aplicativo. Para obter mais informações sobre o arquivo de lista de propriedade, consulte [Sobre arquivos](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)de Lista de propriedades de informações.

1. Faça logon no seguinte site:

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. Criar uma ID do aplicativo. Para obter etapas detalhadas para criar uma ID do aplicativo, consulte [Criação e configuração de IDs](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html)do aplicativo.
1. Para configurar o identificador do pacote para o aplicativo iOS para seu aplicativo, clique em **[!UICONTROL Configurar ID]** do aplicativo.
1. Na parte inferior da página da Web, selecione **[!UICONTROL Ativar para proteção]** de dados. Especifique as opções de proteção de dados.

   Clique em **[!UICONTROL Concluído]**.

1. Navegue até Provisionamento->Distribuição e crie um novo Perfil usando a ID do aplicativo configurada na etapa 3.
1. Baixe e adicione o perfil de provisionamento ao Xcode e ao iPad.
1. Faça logon em sua máquina Mac com o Xcode e o SDK do iOS instalado e configurado.
1. Abra o `AEM Forms.xcodeproj` projeto no Xcode.
1. Clique em **[!UICONTROL AEM Forms]**, em **[!UICONTROL PÚBLICOS ALVOS]**, selecione **[!UICONTROL AEM Forms]**. Selecione a guia Configurações **[!UICONTROL de]** compilação, localize a seção Direito **[!UICONTROL de assinatura de]** código e, na lista suspensa Direitos, selecione a opção Empresa **** LC.
1. Localize e abra o `LC Enterprise.entitlements` arquivo no Xcode para edição. Em direitos **** XCode, adicione o mesmo par de valor chave que está presente no perfil de provisionamento.
1. Na guia **[!UICONTROL Build Settings (Configurações]** de criação), clique em **[!UICONTROL All (Todos]** ) e, em seguida, clique em **[!UICONTROL Combinado]**.
1. Na lista **[!UICONTROL Configurações]** , expanda Assinatura **[!UICONTROL de código]**.
1. Para Identidade **[!UICONTROL de assinatura de]** código, selecione a assinatura apropriada. Certifique-se de que a mesma assinatura esteja selecionada para **[!UICONTROL Depurar]**, **[!UICONTROL Liberar]** e **[!UICONTROL Qualquer SDK]** do iOS.
1. Em **[!UICONTROL PROJECT]**, selecione **[!UICONTROL AEM Forms]** e certifique-se de que a assinatura apropriada esteja selecionada para Identidade **[!UICONTROL de assinatura de]** código, **[!UICONTROL Depuração]**, **[!UICONTROL Liberação]** **** e Qualquer SDK do iOS.
1. Crie e distribua o aplicativo AEM Forms. Para obter instruções detalhadas sobre como criar e distribuir o aplicativo AEM Forms, consulte [Criar o instalador para o aplicativo](/help/forms/using/setup-xcode-project-build-installer.md#main-pars-text-12)AEM Forms.
