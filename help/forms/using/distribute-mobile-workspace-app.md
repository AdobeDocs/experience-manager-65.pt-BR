---
title: Distribuir aplicativo AEM Forms
seo-title: Distribuir aplicativo AEM Forms
description: Use o MDM (Mobile Device Management, gerenciamento de dispositivos móveis) para a implantação em larga escala de aplicativos em dispositivos móveis.
seo-description: Use o MDM (Mobile Device Management, gerenciamento de dispositivos móveis) para a implantação em larga escala de aplicativos em dispositivos móveis.
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Distribuir aplicativo AEM Forms {#distribute-aem-forms-app}

O MDM (Mobile Device Management, gerenciamento de dispositivos móveis) permite a implantação em larga escala de aplicativos em dispositivos móveis.

>[!NOTE]
>
>Essa distribuição é aplicável somente para dispositivos iOS e Android.

## Principais recursos geralmente fornecidos pelas soluções MDM: {#main-features-generally-provided-by-mdm-solutions}

* Ativar a inscrição de dispositivos no ambiente corporativo
* Permitir a configuração e atualização das configurações do dispositivo
* Impor conformidade com a segurança.
* Acesso móvel seguro aos recursos corporativos

Uma solução MDM junto com o Gerenciamento de aplicativos móveis permite gerenciar aplicativos internos, públicos e comprados em todos os dispositivos móveis da sua empresa.

O administrador do MDM pode carregar arquivos ipa e apk no servidor MDM e controlar os usuários que podem acessar os arquivos ipa ou apk. O administrador também pode controlar a configuração do perfil correspondente a cada aplicativo.

## Configurações de Perfil que afetam o aplicativo AEM Forms {#profile-settings-affecting-the-aem-forms-app-br}

As seguintes configurações de Perfil em seu dispositivo afetarão o funcionamento do aplicativo AEM Forms em seu dispositivo:

* **Permitir uso da câmera** na seção **Funcionalidade** do dispositivo

Se você desativar **Permitir uso de câmera**, o recurso de câmera da anotação [](/help/forms/using/add-attachments.md) Fotografia não funcionará. É necessário ativar essa opção para usar a câmera no aplicativo.

* **Exigir senha no dispositivo** na seção Políticas de senha

Para ativar a **criptografia de dados** do aplicativo, é recomendável ativar a **senha** no dispositivo. Se a senha não estiver definida no dispositivo, os dados do aplicativo armazenados no dispositivo não serão criptografados.
