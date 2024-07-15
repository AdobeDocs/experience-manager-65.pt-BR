---
title: Distribuir o aplicativo AEM Forms
description: Use o Gerenciamento de dispositivos móveis (MDM) para a implantação em larga escala de aplicativos em dispositivos móveis.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Distribuir o aplicativo AEM Forms {#distribute-aem-forms-app}

O Gerenciamento de dispositivos móveis (MDM) permite a implantação em larga escala de aplicativos em dispositivos móveis.

>[!NOTE]
>
>Essa distribuição é aplicável somente para dispositivos iOS e Android™.

## Principais recursos fornecidos pelas soluções MDM: {#main-features-generally-provided-by-mdm-solutions}

* Habilitar o registro de dispositivos no ambiente corporativo
* Permitir a definição e atualização das configurações do dispositivo
* Imponha a conformidade de segurança.
* Acesso móvel seguro a recursos corporativos

Uma solução MDM, juntamente com o Gerenciamento de aplicativos móveis, permite gerenciar aplicativos internos, públicos e adquiridos em todos os dispositivos móveis da empresa.

O administrador do MDM pode fazer upload de arquivos ipa e apk para o servidor MDM e controlar os usuários que podem acessar os arquivos ipa ou apk. O administrador também pode controlar as configurações de perfil que correspondem a cada aplicativo.

## Configurações de perfil que afetam o aplicativo AEM Forms {#profile-settings-affecting-the-aem-forms-app-br}

As seguintes configurações de perfil no seu dispositivo afetam o funcionamento do aplicativo AEM Forms no seu dispositivo:

* **Permitir o uso da câmera** na seção **Funcionalidade do dispositivo**

Se você desabilitar **Permitir o uso da câmera**, o recurso de câmera da [Anotação da fotografia](/help/forms/using/add-attachments.md) não funcionará. Ative esta opção para usar a câmera no aplicativo.

* **Exigir senha no dispositivo** na seção de políticas de senha

Para habilitar a **criptografia de dados de aplicativo**, é recomendável habilitar a **senha** em seu dispositivo. Se a senha não estiver definida no dispositivo, os dados do aplicativo armazenados no dispositivo não serão criptografados.
