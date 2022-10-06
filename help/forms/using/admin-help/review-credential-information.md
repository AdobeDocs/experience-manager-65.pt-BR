---
title: Revisar informações de uso de credenciais
seo-title: Review credential use information
description: Saiba como revisar informações de uso de credenciais.
seo-description: Learn how to review credential use information.
uuid: 02af75f9-c235-470d-a98b-a2102aa31381
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cdf61cff-768b-49f7-9926-400bc96b0708
exl-id: a8e16cf8-f3c8-48ce-87da-2f0de0b10a6e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# Revisar informações de uso de credenciais {#review-credential-use-information}

A credencial contém informações descrevendo seu uso pretendido e que podem ser acessadas por meio do aplicativo da Web do usuário final das extensões do Acrobat Reader DC. Você pode usar essas informações para determinar o tipo de credencial instalada (avaliação ou produção) e suas datas de validade.

1. Abra um navegador da Web e insira este URL:

   http://localhost:port/ReaderExtensions (onde *porta* é o número da porta do servidor de aplicativos)

1. Faça logon usando o nome de usuário e a senha padrão:

   Nome do usuário: administrador

   Senha: senha

   >[!NOTE]
   >
   >Você deve ter privilégios de administrador ou superusuário para fazer logon usando o nome de usuário e a senha padrão. Para permitir que outros usuários acessem extensões do Acrobat Reader DC, crie as contas de usuário no Gerenciamento de usuários e conceda aos usuários a função de extensões do Acrobat Reader DC Web Application.

1. Selecione o alias da credencial na lista Selecionar Credencial e revise as informações incluídas na Data de Expiração e no Aviso de Uso Pretendido.

>[!NOTE]
>
>A data de expiração da credencial também está disponível na página Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais do console de administração, em Data de expiração.
