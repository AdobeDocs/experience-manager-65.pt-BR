---
title: Como personalizar guias para uma tarefa
seo-title: Como personalizar guias para uma tarefa
description: Como personalizar os nomes das guias para suas tarefas, na área de trabalho do LiveCycle AEM Forms.
seo-description: Como personalizar os nomes das guias para suas tarefas, na área de trabalho do LiveCycle AEM Forms.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Como personalizar guias para uma tarefa {#customizing-tabs-for-a-task}

Você pode personalizar nomes de guias para o `Start Process` componente na visualização `Start Process` Uber e o `Task Details` componente na visualização `ToDo` Uber.

1. Siga as etapas [genéricas para personalização](/help/forms/using/generic-steps-html-workspace-customization.md)da área de trabalho do AEM Forms.
1. Altere o valor de `tabname`no `translation.json` arquivo.

   Por exemplo, mude `/apps/ws/locales/en-US/translation.json` para inglês para o seguinte.

   * Para tarefas iniciadas no processo de start, use o seguinte trecho do `"startprocess" : {}` bloco.

   ```
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Para tarefa em tarefas a fazer, use o seguinte snippet do `"todo" : {}` bloco.

   ```
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
   >Adicione um par de valor de chave correspondente para todos os idiomas suportados.
