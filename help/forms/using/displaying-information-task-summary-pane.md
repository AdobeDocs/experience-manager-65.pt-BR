---
title: Exibindo informações no painel Resumo da Tarefa
seo-title: Displaying information in the Task Summary pane
description: Na área de trabalho do AEM Forms, um painel de Resumo de tarefas pode ser configurado para resumir a tarefa ou exibir qualquer outra página da Web.
seo-description: In AEM Forms workspace, a Task Summary pane can be configured to summarize the task or display any other web page.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Exibindo informações no painel Resumo da Tarefa {#displaying-information-in-the-task-summary-pane}

Ao abrir uma tarefa no espaço de trabalho do AEM Forms, um painel Resumo de tarefas pode exibir um resumo da tarefa. Essas informações adicionais e relevantes para uma tarefa adicionam mais valor ao usuário final do espaço de trabalho do AEM Forms.

O espaço de trabalho do AEM Forms permite exibir uma página da Web de sua escolha no painel Resumo de tarefas . Um processo pode ser criado para exibir um painel Resumo de tarefas usando o Workbench.

1. Crie um processo Atribuir tarefa no Workbench. Para obter mais detalhes sobre a operação Atribuir tarefa, consulte o tópico Referência de serviço em [Ajuda do Workbench](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/).

   >[!NOTE]
   >
   >Se houver um URL de Resumo de Tarefas, a exibição Resumo de Tarefas será aberta por padrão em vez da exibição Formulário. Nesse caso, mesmo quando um usuário ativa a opção &quot;Abrir o formulário no modo maximizado&quot; em Atribuir tarefa, o formulário não abre no modo maximizado.

1. Configure o campo URL do resumo da tarefa . Você pode especificar um valor literal, um modelo, uma variável ou uma expressão XPath.
1. Um exemplo de exibição das informações na página Resumo da tarefa está abaixo.

   * Faça logon no ambiente CRXDE Lite em `https://'[server]:[port]'/lc/crx/de`.
   * `Create a node`**SampleSummary** ` under `/conteúdo` with type `nt:unstructured`. In the properties of this node, add `sling:resourceType` of type String and value `SampleSummary`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr:read` privileges.`
   * `Create a folder`**SampleSummary** under `/apps`. Na Lista de Controle de Acesso de `/apps/SampleSummary`, adicione uma entrada para `PERM_WORKSPACE_USER` permitir `jcr:readprivileges`.
   * `Create a file `html.esp` at `/apps/SampleSummary`. For example, add the following lines in `html.esp`.`

   ```html
   <html>
       <body>
           <h1>Sample Summary</h1>
           <br/>
           <p>Hello Sir!
               <br/>
               This is sample summary page for this task.
           </p>
       </body>
   </html>
   ```

   * Defina o valor do url de resumo de tarefa como `/lc/content/SampleSummary.html` na etapa Atribuir tarefa .
   * Quando a tarefa associada a esta etapa Atribuir Tarefa é aberta no espaço de trabalho do AEM Forms, a variável `html.esp` at `/apps/SampleSummary` é renderizado no painel de resumo da tarefa.
