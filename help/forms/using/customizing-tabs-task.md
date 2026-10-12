---
title: Personalizando guias para uma tarefa
description: Como personalizar os nomes das guias para suas tarefas, no espaço de trabalho do LiveCycle AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
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
source-wordcount: '104'
ht-degree: 0%
---
# Personalizando guias para uma tarefa {#customizing-tabs-for-a-task}

Você pode personalizar nomes de guia para o componente `Start Process` no modo de exibição Uber `Start Process` e o componente `Task Details` no modo de exibição Uber `ToDo`.

1. Siga as [etapas genéricas para personalização do espaço de trabalho do AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Alterar o valor de `tabname` no arquivo `translation.json`.

   Por exemplo, altere `/apps/ws/locales/en-US/translation.json` para inglês.

   * Para tarefas iniciadas no processo de início, use o seguinte trecho do bloco `"startprocess" : {}`.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Para tarefas em Tarefas Pendentes, use o seguinte trecho do bloco `"todo" : {}`.

   ```json
   "tabname" : {
               "summary" : "Bird's-eye view",
               "history" : "Past",
               "form" : "Form",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Notes"
   }
   ```

   >[!NOTE]
   >
   >Adicione o par de valor principal correspondente para todos os idiomas compatíveis.
