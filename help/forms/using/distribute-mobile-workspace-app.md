---
title: Distribuir o aplicativo AEM Forms
seo-title: Distribute AEM Forms app
description: Use o Gerenciamento de dispositivos móveis (MDM) para a implantação em larga escala de aplicativos em dispositivos móveis.
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

# Distribuir o aplicativo AEM Forms {#distribute-aem-forms-app}

O Gerenciamento de dispositivos móveis (MDM) permite a implantação em larga escala de aplicativos em dispositivos móveis.

>[!NOTE]
>
>Essa distribuição é aplicável somente para dispositivos iOS e Android.

## Principais recursos geralmente fornecidos pelas soluções MDM: {#main-features-generally-provided-by-mdm-solutions}

* Habilitar o registro de dispositivos no ambiente corporativo
* Permitir a definição e atualização das configurações do dispositivo
* Imponha a conformidade de segurança.
* Acesso móvel seguro a recursos corporativos

Uma solução MDM, juntamente com o Gerenciamento de aplicativos móveis, permite gerenciar aplicativos internos, públicos e adquiridos nos dispositivos móveis de sua empresa.

O administrador do MDM pode fazer upload de arquivos ipa e apk para o servidor MDM e controlar os usuários que podem acessar os arquivos ipa ou apk. O administrador também pode controlar a configuração de perfil correspondente a cada aplicativo.

## Configurações de perfil que afetam o aplicativo AEM Forms {#profile-settings-affecting-the-aem-forms-app-br}

As seguintes configurações de perfil no dispositivo afetarão o funcionamento do aplicativo AEM Forms no dispositivo:

* **Permitir o uso da câmera** no **Funcionalidade do dispositivo** seção

Se você desativar o **Permitir o uso da câmera**, o recurso de câmera do [Anotação de fotografia](/help/forms/using/add-attachments.md) não funcionará. Você precisa ativar esta opção para usar a câmera no aplicativo.

* **Exigir senha no dispositivo** na seção Políticas de senha

Para habilitar **criptografia de dados de aplicativos**, é recomendável ativar o **senha** no seu dispositivo. Se a senha não estiver definida no dispositivo, os dados do aplicativo armazenados no dispositivo não serão criptografados.
