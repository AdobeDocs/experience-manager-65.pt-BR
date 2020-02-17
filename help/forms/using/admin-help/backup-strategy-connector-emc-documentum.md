---
title: Estratégia de backup para usuários do Connector para EMC Documentum
seo-title: Estratégia de backup para usuários do Connector para EMC Documentum
description: Verifique como criar uma estratégia de backup para usuários do Connector para EMC Documentum.
seo-description: Verifique como criar uma estratégia de backup para usuários do Connector para EMC Documentum.
uuid: 5d8a0476-5231-4e1d-96c4-ae3df68e09f0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e83b1a59-a730-4d22-9d58-1c9c38e5d534
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Estratégia de backup para usuários do Connector para EMC Documentum {#backup-strategy-for-connector-for-emc-documentum-users}

Se você tiver o Connector for EMC Documentum instalado, além das instruções neste capítulo, sua estratégia de backup e recuperação deverá incluir o backup (ou recuperação) do computador no qual o sistema ECM está instalado. (Consulte a documentação do ECM Documentum).

Faça backup do ambiente de formulários do AEM usando o repositório ECM e executando as seguintes tarefas:

* Faça backup dos formulários do AEM seguindo as instruções descritas neste documento.
* Faça backup do sistema ECM Documentum seguindo as instruções em [Fazer backup do EMC Documentum Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server).

Restaure o ambiente de formulários AEM usando o repositório ECM e executando as seguintes tarefas:

* Restaure seu sistema ECM respectivo seguindo as instruções em [Restaurar o EMC Documentum Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server).
* Restaure formulários AEM seguindo as instruções descritas neste documento.

