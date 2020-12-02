---
title: Ativação e desativação do modo de backup seguro
seo-title: Ativação e desativação do modo de backup seguro
description: Na página Configurações de backup, você pode operar formulários AEM no modo de backup seguro para que possa fazer backup confiável do banco de dados e do diretório GDS (Global Documento Armazenamento). Saiba como ativar e desativar o modo de backup seguro.
seo-description: Na página Configurações de backup, você pode operar formulários AEM no modo de backup seguro para que possa fazer backup confiável do banco de dados e do diretório GDS (Global Documento Armazenamento). Saiba como ativar e desativar o modo de backup seguro.
uuid: 2fdeaeaf-e969-40a4-8aee-1f2b627d3942
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fda71e4-78a1-4581-9d02-bf06a75c3bcb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# Ativando e desativando o modo de backup seguro {#enabling-and-disabling-safe-backup-mode}

Na página Configurações de backup, você pode operar formulários AEM no modo de backup seguro para que possa fazer backup confiável do banco de dados e do diretório GDS (Global Documento Armazenamento).

Embora AEM formulários esteja no modo de backup seguro, ele opera normalmente, exceto que não remove arquivos ativamente do diretório GDS.

>[!NOTE]
>
>A configuração dessa opção não faz backup do sistema; ele prepara seu sistema para backup.

## Habilitar modo de backup seguro {#enable-safe-backup-mode}

1. No console de administração, clique em Configurações > Principais configurações de sistemas > Configurações de backup.
1. Na página Configurações de backup, selecione Operar no modo de backup seguro e clique em OK.

>[!NOTE]
>
>Se o sistema já estiver sendo executado no modo de backup seguro, uma nova reserva não será criada quando você clicar em OK.

## Desativar modo de backup seguro {#disable-safe-backup-mode}

1. No console de administração, clique em Configurações > Principais configurações de sistemas > Configurações de backup.
1. Na página Configurações de backup, desmarque Operar no modo de backup seguro e clique em OK.

