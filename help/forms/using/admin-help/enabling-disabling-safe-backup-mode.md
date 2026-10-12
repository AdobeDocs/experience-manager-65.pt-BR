---
title: Ativando e desativando o modo de backup seguro
description: Na página Configurações de backup, você pode operar formulários AEM no modo de backup seguro para poder fazer backup de seu banco de dados e do diretório GDS (Armazenamento global de documentos) de maneira confiável. Saiba como ativar e desativar o modo de backup seguro.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
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
source-wordcount: '208'
ht-degree: 0%
---
# Ativando e desativando o modo de backup seguro {#enabling-and-disabling-safe-backup-mode}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Na página Configurações de backup, você pode operar formulários AEM no modo de backup seguro para poder fazer backup de seu banco de dados e do diretório GDS (Armazenamento global de documentos) de maneira confiável.

Embora o AEM Forms esteja no modo de backup seguro, ele funciona normalmente, exceto por não remover ativamente os arquivos do diretório GDS.

>[!NOTE]
>
>A configuração dessa opção não faz backup do sistema; ela prepara o sistema para backup.

## Ativar modo de backup seguro {#enable-safe-backup-mode}

1. No console de administração, clique em Configurações > Configurações dos sistemas principais > Configurações de backup.
1. Na página Configurações de backup, selecione Operar no modo de backup seguro e clique em OK.

>[!NOTE]
>
>Se o sistema já estiver sendo executado no modo de backup seguro, uma nova reserva não será criada quando você clicar em OK.

## Desabilitar modo de backup seguro {#disable-safe-backup-mode}

1. No console de administração, clique em Configurações > Configurações dos sistemas principais > Configurações de backup.
1. Na página Configurações de backup, desmarque a opção Operar no modo de backup seguro e clique em OK.
