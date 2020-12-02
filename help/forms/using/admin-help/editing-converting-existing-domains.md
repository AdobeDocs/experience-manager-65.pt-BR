---
title: Editar e converter domínios existentes
seo-title: Editar e converter domínios existentes
description: Saiba como alterar as configurações de domínios existentes na página Gerenciamento de domínio. Converta um domínio empresarial existente em um domínio híbrido ou vice-versa.
seo-description: Saiba como alterar as configurações de domínios existentes na página Gerenciamento de domínio. Converta um domínio empresarial existente em um domínio híbrido ou vice-versa.
uuid: 4cc9547e-b4ec-4588-b1cf-18720f06149a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 44dec184-3ef7-4ba6-a87f-ad171d3cb188
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---


# Editar e converter domínios existentes{#editing-and-converting-existing-domains}

É possível alterar as configurações de domínios existentes na página Gerenciamento de domínio. Você também pode converter um domínio empresarial existente em um domínio híbrido.

## Editar um domínio existente {#edit-an-existing-domain}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique no nome do domínio a ser editado.
1. Para alterar o nome do domínio, altere o texto na caixa Nome.
1. Para alterar as informações de autenticação de um domínio corporativo ou híbrido, clique no nome de autenticação apropriado na parte inferior da página. Na página Editar autenticação, altere as configurações conforme necessário. (Consulte [Configurações de autenticação](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Para alterar as informações do diretório de um domínio corporativo, clique no nome do diretório apropriado na parte inferior da página. Na página Editar diretório, altere as configurações conforme necessário. (Consulte [Adicionar diretórios ou SPIs personalizados](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Ao concluir as alterações, clique em OK.

## Converter um domínio corporativo em um domínio híbrido {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique no nome do domínio corporativo a ser convertido.
1. Clique em Converter em domínio híbrido.
1. Revise as informações que aparecem com relação aos dados de usuário e grupo e à autenticação de usuários e clique em OK.
1. Edite as configurações do domínio híbrido e clique em OK.

>[!NOTE]
>
>Se o domínio corporativo que você está convertendo não contiver configurações de diretório, quaisquer configurações de autenticação LDAP serão perdidas.

## Converter um domínio híbrido em um domínio corporativo {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique no nome do domínio híbrido a ser convertido.
1. Clique em Converter em domínio corporativo.
1. Revise as informações que aparecem com relação aos dados de usuário e grupo e à autenticação de usuários e clique em OK.
1. Clique em Adicionar diretório e configure as informações necessárias do diretório. (Consulte [Adicionar diretórios ou SPIs personalizados](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)

