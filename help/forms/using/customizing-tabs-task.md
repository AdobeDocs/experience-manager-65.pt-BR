---
title: Personalizando guias para uma tarefa
description: Como personalizar os nomes das guias para suas tarefas no espaço de trabalho do LiveCycle AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '101'
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
