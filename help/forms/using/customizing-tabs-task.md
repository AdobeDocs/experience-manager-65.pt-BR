---
title: Personalizar guias para uma tarefa
seo-title: Personalizar guias para uma tarefa
description: Como personalizar os nomes das guias para suas tarefas, na área de trabalho do LiveCycle AEM Forms.
seo-description: Como personalizar os nomes das guias para suas tarefas, na área de trabalho do LiveCycle AEM Forms.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personalizar guias para uma tarefa {#customizing-tabs-for-a-task}

Você pode personalizar nomes de guias para o `Start Process` componente na exibição `Start Process` Uber e o `Task Details` componente na exibição `ToDo` Uber.

1. Siga as etapas [genéricas para personalização](/help/forms/using/generic-steps-html-workspace-customization.md)da área de trabalho do AEM Forms.
1. Altere o valor de `tabname`no `translation.json` arquivo.

   Por exemplo, mude `/apps/ws/locales/en-US/translation.json` para inglês para o seguinte.

   * Para tarefas iniciadas no processo de início, use o seguinte trecho do `"startprocess" : {}` bloco.

   ```
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Para tarefas em Tarefas em Tarefas pendentes, use o seguinte trecho do `"todo" : {}` bloco.

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

[Contate o suporte](https://www.adobe.com/account/sign-in.supportportal.html)
