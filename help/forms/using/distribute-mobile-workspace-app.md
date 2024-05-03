---
title: Distribuir o aplicativo AEM Forms
description: Use o Gerenciamento de dispositivos móveis (MDM) para a implantação em larga escala de aplicativos em dispositivos móveis.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
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

* **Permitir o uso da câmera** no **Funcionalidade do dispositivo** seção

Se você desativar o **Permitir o uso da câmera**, o recurso de câmera do [Anotação de fotografia](/help/forms/using/add-attachments.md) não funciona. Ative esta opção para usar a câmera no aplicativo.

* **Exigir senha no dispositivo** na seção Políticas de senha

Para habilitar **criptografia de dados de aplicativos**, é recomendável ativar o **senha** no seu dispositivo. Se a senha não estiver definida no dispositivo, os dados do aplicativo armazenados no dispositivo não serão criptografados.
