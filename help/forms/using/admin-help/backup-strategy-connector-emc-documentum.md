---
title: Estratégia de backup para o Connector para usuários da EMC Documentum
seo-title: Backup strategy for Connector for EMC Documentum users
description: Verifique como criar uma estratégia de backup para o Connector para usuários da EMC Documentum.
seo-description: Check how to create a backup strategy for Connector for EMC Documentum users.
uuid: 5d8a0476-5231-4e1d-96c4-ae3df68e09f0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e83b1a59-a730-4d22-9d58-1c9c38e5d534
exl-id: b759b936-5907-4311-a5cc-60f321476368
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Estratégia de backup para o Connector para usuários da EMC Documentum {#backup-strategy-for-connector-for-emc-documentum-users}

Se tiver o Connector for EMC Documentum instalado, além das instruções deste capítulo, sua estratégia de backup e recuperação deve incluir backup (ou recuperação) do computador no qual o sistema ECM respectivo está instalado. (Consulte a documentação da ECM Documentum).

Faça o backup do seu ambiente AEM forms usando o repositório ECM e executando as seguintes tarefas:

* Faça o backup AEM formulários seguindo as instruções descritas neste documento.
* Faça backup do sistema ECM Documentum seguindo as instruções em [Faça backup do EMC Documentum Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server).

Restaure AEM ambiente do forms usando o repositório ECM e executando as seguintes tarefas:

* Restaure seu sistema ECM respectivo seguindo as instruções em [Restaurar o EMC Documentum Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server).
* Restaure AEM formulários seguindo as instruções descritas neste documento.
