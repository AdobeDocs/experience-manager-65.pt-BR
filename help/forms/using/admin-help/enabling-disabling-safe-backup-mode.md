---
title: Ativando e desativando o modo de backup seguro
description: Na página Configurações de backup, você pode operar formulários AEM no modo de backup seguro, para fazer backup confiável do banco de dados e do diretório GDS (Armazenamento global de documentos). Saiba como ativar e desativar o modo de backup seguro.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# Ativando e desativando o modo de backup seguro {#enabling-and-disabling-safe-backup-mode}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Na página Configurações de backup, você pode operar formulários AEM no modo de backup seguro, para fazer backup confiável do banco de dados e do diretório GDS (Armazenamento global de documentos).

Enquanto o AEM Forms estiver no modo de backup seguro, ele funciona normalmente, exceto que não remove ativamente os arquivos do diretório GDS.

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
