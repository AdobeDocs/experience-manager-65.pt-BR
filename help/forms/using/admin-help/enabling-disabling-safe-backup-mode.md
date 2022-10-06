---
title: Ativação e desativação do modo de backup seguro
seo-title: Enabling and disabling safe backup mode
description: Na página Configurações de Backup, é possível operar AEM formulários no modo de backup seguro para que você possa fazer backup confiável de seu banco de dados e do diretório GDS (Global Document Storage, Armazenamento de Documentos Global). Saiba como ativar e desativar o modo de backup seguro.
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

# Ativação e desativação do modo de backup seguro {#enabling-and-disabling-safe-backup-mode}

Na página Configurações de Backup, é possível operar AEM formulários no modo de backup seguro para que você possa fazer backup confiável de seu banco de dados e do diretório GDS (Global Document Storage, Armazenamento de Documentos Global).

Embora AEM formulários esteja no modo de backup seguro, ele opera normalmente, exceto que não remove arquivos ativamente do diretório GDS.

>[!NOTE]
>
>A configuração dessa opção não faz backup do sistema; ele prepara seu sistema para backup.

## Ativar o modo de cópia de segurança {#enable-safe-backup-mode}

1. No console de administração, clique em Configurações > Configurações de sistemas principais > Configurações de backup.
1. Na página Configurações de backup, selecione Operar no modo de backup seguro e clique em OK.

>[!NOTE]
>
>Se o sistema já estiver em execução no modo de backup seguro, uma nova reserva não será criada quando você clicar em OK.

## Desativar modo de cópia de segurança {#disable-safe-backup-mode}

1. No console de administração, clique em Configurações > Configurações de sistemas principais > Configurações de backup.
1. Na página Configurações de backup, desmarque Operar no modo de backup seguro e clique em OK.
