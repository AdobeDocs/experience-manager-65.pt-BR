---
title: Distribuir aplicativo AEM Forms
seo-title: Distribute AEM Forms app
description: Use o Gerenciamento de dispositivos móveis (MDM) para a implantação em grande escala de aplicativos em dispositivos móveis.
seo-description: Use Mobile Device Management (MDM) for the large-scale deployment of apps on mobile devices.
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Distribuir aplicativo AEM Forms {#distribute-aem-forms-app}

O Gerenciamento de dispositivos móveis (MDM) permite a implantação em grande escala de aplicativos em dispositivos móveis.

>[!NOTE]
>
>Essa distribuição é aplicável somente para dispositivos iOS e Android.

## Principais recursos geralmente fornecidos pelas soluções MDM: {#main-features-generally-provided-by-mdm-solutions}

* Ativar a inscrição de dispositivos no ambiente empresarial
* Permitir a configuração e a atualização das definições do dispositivo
* Impor conformidade com a segurança.
* Acesso móvel seguro aos recursos corporativos

Uma solução MDM juntamente com o Gerenciamento de aplicativos móveis permite gerenciar aplicativos internos, públicos e comprados em todos os dispositivos móveis da empresa.

O administrador do MDM pode fazer upload de arquivos ipa e apk para o servidor MDM e controlar os usuários que podem acessar os arquivos ipa ou apk. O administrador também pode controlar a configuração de perfil correspondente a cada aplicativo.

## Configurações de perfil que afetam o aplicativo AEM Forms {#profile-settings-affecting-the-aem-forms-app-br}

As seguintes configurações de Perfil no seu dispositivo afetarão o funcionamento do aplicativo AEM Forms no seu dispositivo:

* **Permitir a utilização da câmara** no **Funcionalidade do dispositivo** seção

Se você desativar **Permitir a utilização da câmara**, o recurso de câmera do [Anotação de fotos](/help/forms/using/add-attachments.md) não funcionará. Você precisa ativar esta opção para usar a câmera no aplicativo.

* **Exigir senha no dispositivo** na seção Políticas de código

Para ativar **criptografia de dados de aplicativos**, é recomendável ativar a variável **passcode** no seu dispositivo. Se a senha não estiver definida no dispositivo, os dados do aplicativo armazenados no dispositivo não serão criptografados.
