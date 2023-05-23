---
title: Personalizando guias para uma tarefa
seo-title: Customizing tabs for a task
description: Como personalizar os nomes das guias para suas tarefas no espaço de trabalho do LiveCycle AEM Forms.
seo-description: How-to customize the names of the tabs for your tasks, in LiveCycle AEM Forms workspace.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Personalizando guias para uma tarefa {#customizing-tabs-for-a-task}

É possível personalizar os nomes das guias para a `Start Process` componente no `Start Process` Uber view e o `Task Details` componente no `ToDo` Uber view.

1. Siga as [Etapas genéricas para personalização do espaço de trabalho do AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Altere o valor de `tabname`no `translation.json` arquivo.

   Por exemplo, alterar `/apps/ws/locales/en-US/translation.json` para inglês a seguir.

   * Para tarefas iniciadas no processo inicial, use o seguinte trecho da `"startprocess" : {}` bloco.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Para tarefas em Tarefas Pendentes, use o seguinte trecho da `"todo" : {}` bloco.

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
