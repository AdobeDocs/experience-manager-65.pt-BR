---
title: Edição e conversão de domínios existentes
description: Saiba como alterar as configurações para domínios existentes na página Gerenciamento de domínio. Converta um domínio enterprise existente em um domínio híbrido ou vice-versa.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 34ac5f8b-f209-4f99-ad71-4df6f2c88c1e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Edição e conversão de domínios existentes{#editing-and-converting-existing-domains}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Você pode alterar as configurações para domínios existentes na página Gerenciamento de domínio. Você também pode converter um domínio enterprise existente em um domínio híbrido.

## Editar um domínio existente {#edit-an-existing-domain}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. Clique no nome do domínio para editar.
1. Para alterar o nome do domínio, altere o texto na caixa Nome.
1. Para alterar as informações de autenticação de um domínio enterprise ou híbrido, clique no nome de autenticação apropriado na parte inferior da página. Na página Editar autenticação, altere as configurações conforme necessário. (Consulte [Configurações de autenticação](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Para alterar as informações de diretório de um domínio enterprise, clique no nome de diretório apropriado na parte inferior da página. Na página Editar Diretório, altere as definições conforme necessário. (Consulte [Adição de diretórios ou SPIs personalizadas](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Ao concluir as alterações, clique em OK.

## Converter um domínio enterprise em um domínio híbrido {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. Clique no nome do domínio enterprise a ser convertido.
1. Clique em Converter para domínio híbrido.
1. Revise as informações exibidas sobre os dados do usuário e do grupo e a autenticação dos usuários e clique em OK.
1. Edite as configurações do domínio híbrido e clique em OK.

>[!NOTE]
>
>Se o domínio enterprise que você está convertendo não contiver definições de diretório, as definições de autenticação LDAP serão perdidas.

## Converter um domínio híbrido em um domínio enterprise {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. Clique no nome do domínio híbrido a ser convertido.
1. Clique em Converter para domínio Enterprise.
1. Revise as informações exibidas sobre os dados do usuário e do grupo e a autenticação dos usuários e clique em OK.
1. Clique em Adicionar diretório e configure as informações de diretório necessárias. (Consulte [Adição de diretórios ou SPIs personalizadas](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
