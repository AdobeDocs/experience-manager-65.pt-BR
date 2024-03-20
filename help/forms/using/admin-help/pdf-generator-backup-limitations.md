---
title: Limitações de backup de PDF Generator
description: Saiba mais sobre as limitações de backup de PDF Generator. Não é possível fazer backup do diretório temporário que o PDF Generator usa, pois ele limpa o conteúdo em intervalos definidos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
exl-id: a23db58d-1236-4689-93fc-dea508f8eb81
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 0%

---

# Limitações de backup de PDF Generator {#pdf-generator-backup-limitations}

Não é possível fazer backup do diretório temporário usado pelo PDF Generator para converter arquivos. Mesmo que o serviço seja restaurado corretamente, os dados podem ser perdidos porque o PDF Generator revisa e limpa o conteúdo do diretório temporário em intervalos definidos.
