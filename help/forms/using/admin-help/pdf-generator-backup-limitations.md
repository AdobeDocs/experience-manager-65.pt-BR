---
title: Limitações de backup de PDF Generator
description: Saiba mais sobre as limitações de backup de PDF Generator. Não é possível fazer backup do diretório temporário que o PDF Generator usa, pois ele limpa o conteúdo em intervalos definidos.
uuid: 9537ffde-4396-46d1-81ea-edcd25923ffb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 23386353-b2bf-49f1-947a-dd7587bba175
noindex: true
exl-id: a23db58d-1236-4689-93fc-dea508f8eb81
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 0%

---

# Limitações de backup de PDF Generator {#pdf-generator-backup-limitations}

Não é possível fazer backup do diretório temporário usado pelo PDF Generator para converter arquivos. Mesmo que o serviço seja restaurado corretamente, os dados podem ser perdidos porque o PDF Generator revisa e limpa o conteúdo do diretório temporário em intervalos definidos.
