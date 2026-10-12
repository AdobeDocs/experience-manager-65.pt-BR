---
title: Estratégia de backup para o Connector para usuários do EMC Documentum&reg;
description: Verifique como criar uma estratégia de backup para o Connector para usuários do EMC Documentum&reg;.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b759b936-5907-4311-a5cc-60f321476368
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
source-wordcount: '155'
ht-degree: 0%
---
# Estratégia de backup para o Connector para usuários do EMC Documentum® {#backup-strategy-for-connector-for-emc-documentum-users}

Se você tiver o Connector for EMC Documentum® instalado, além das instruções neste capítulo, sua estratégia de backup e recuperação deve incluir backup (ou recuperação) do computador em que o sistema ECM está instalado. (Consulte a documentação do ECM Documentum®).

Faça backup do ambiente AEM Forms usando o repositório ECM e executando as seguintes tarefas:

* Faça backup dos formulários do AEM seguindo as instruções descritas neste documento.
* Faça backup do sistema ECM Documentum® seguindo as instruções em [Fazer backup do EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server).

Restaurar o ambiente do AEM Forms usando o repositório ECM e executando as seguintes tarefas:

* Restaure o respectivo sistema de ECM seguindo as instruções em [Restaurar o EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server).
* Restaure os formulários do AEM seguindo as instruções descritas neste documento.
