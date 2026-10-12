---
title: Revisar informações de uso da credencial
description: Saiba como revisar as informações de uso de credencial. As informações de uso de credencial, que descrevem seu uso, podem ser acessadas por meio da extensão do Acrobat Reader.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8e16cf8-f3c8-48ce-87da-2f0de0b10a6e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%
---
# Revisar informações de uso da credencial {#review-credential-use-information}

A credencial contém informações descrevendo seu uso pretendido que podem ser acessadas por meio do aplicativo web do usuário final de extensões do Acrobat Reader DC. Você pode usar essas informações para determinar o tipo de credencial instalada (avaliação ou produção) e suas datas de validade.

1. Abra um navegador da Web e insira este URL:

   http://localhost:port/ReaderExtensions (onde *porta* é o número da porta do seu servidor de aplicativos)

1. Efetue login usando o nome de usuário e a senha padrão:

   Nome de usuário: administrador

   Senha: senha

   >[!NOTE]
   >
   >Você deve ter privilégios de administrador ou superusuário para efetuar login usando o nome de usuário e a senha default. Para permitir que outros usuários acessem extensões do Acrobat Reader DC, crie as contas de usuário no Gerenciamento de usuários e conceda aos usuários a função de Aplicativo da Web de extensões do Acrobat Reader DC.

1. Selecione o alias da credencial na lista Selecionar credencial e revise as informações incluídas na Data de expiração e no Aviso de uso pretendido.

>[!NOTE]
>
>A data de expiração da credencial também está disponível na página Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais do console de administração, em Data de expiração.
