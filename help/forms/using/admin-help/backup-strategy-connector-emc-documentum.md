---
title: Estratégia de backup para o Connector para usuários do EMC Documentum&reg;
description: Verifique como criar uma estratégia de backup para o Connector para usuários do EMC Documentum&reg;.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b759b936-5907-4311-a5cc-60f321476368
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Estratégia de backup para o Connector para usuários do EMC Documentum® {#backup-strategy-for-connector-for-emc-documentum-users}

Se você tiver o Connector for EMC Documentum® instalado, além das instruções neste capítulo, sua estratégia de backup e recuperação deve incluir backup (ou recuperação) do computador em que o sistema ECM está instalado. (Consulte a documentação do ECM Documentum®).

Faça backup do ambiente de formulários AEM usando o repositório ECM e executando as seguintes tarefas:

* Faça backup dos formulários AEM seguindo as instruções descritas neste documento.
* Faça backup do sistema ECM Documentum® seguindo as instruções em [Faça backup do EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server).

Restaure o ambiente de formulários AEM usando o repositório ECM e executando as seguintes tarefas:

* Restaure o respectivo sistema de ECM seguindo as instruções em [Restaurar o EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server).
* Restaure os formulários AEM seguindo as instruções descritas neste documento.
