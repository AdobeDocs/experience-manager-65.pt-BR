---
title: Ativando e desativando o modo de backup seguro
seo-title: Enabling and disabling safe backup mode
description: Na página Configurações de backup, você pode operar formulários AEM no modo de backup seguro, para fazer backup confiável do banco de dados e do diretório GDS (Armazenamento global de documentos). Saiba como ativar e desativar o modo de backup seguro.
seo-description: On the Backup Settings page, you can operate AEM forms in safe backup mode so that you can reliably back up your database and Global Document Storage (GDS) (GDS) directory. Learn how to enable and disable safe backup mode.
uuid: 2fdeaeaf-e969-40a4-8aee-1f2b627d3942
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fda71e4-78a1-4581-9d02-bf06a75c3bcb
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Ativando e desativando o modo de backup seguro {#enabling-and-disabling-safe-backup-mode}

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
