---
title: Exibindo informações no painel Resumo da Tarefa
description: No espaço de trabalho do AEM Forms, um painel Resumo da tarefa pode ser configurado para resumir a tarefa ou exibir qualquer outra página da Web.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Exibindo informações no painel Resumo da Tarefa {#displaying-information-in-the-task-summary-pane}

Quando você abre uma tarefa no espaço de trabalho do AEM Forms, um painel Resumo da tarefa pode exibir um resumo da tarefa. Essas informações adicionais e relevantes para uma tarefa agregam mais valor ao usuário final do espaço de trabalho do AEM Forms.

O espaço de trabalho do AEM Forms permite exibir uma página da Web de sua escolha no painel Resumo da tarefa. Um processo pode ser criado para exibir um painel de Resumo da Tarefa usando a Bancada.

1. Crie um processo Atribuir tarefa no Workbench. Para obter mais detalhes sobre a operação Atribuir tarefa, consulte o tópico Referência de serviço na [Ajuda do Workbench](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/).

   >[!NOTE]
   >
   >Se existir um URL de Resumo da Tarefa, o modo de exibição Resumo da Tarefa será aberto por padrão em vez do modo de exibição Formulário. Nesse caso, mesmo quando um usuário ativa a opção &quot;Abrir o formulário no modo maximizado&quot; em Atribuir tarefa, o formulário não abre no modo maximizado.

1. Configure o campo URL do Resumo da tarefa. Você pode especificar um valor literal, um modelo, uma variável ou uma expressão XPath.
1. Um exemplo de exibição das informações na página Resumo da tarefa está abaixo.

   * Faça logon no ambiente CRXDE Lite em `https://'[server]:[port]'/lc/crx/de`.
   * `Create a node`**SampleSummary** ` under `/content` with type `nt:unstructured`. In the properties of this node, add `sling:resourceType` of type String and value `SampleSummary`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr:read` privileges.`
   * `Create a folder`**SampleSummary** em `/apps`. Na Lista de Controle de Acesso de `/apps/SampleSummary`, adicione uma entrada para `PERM_WORKSPACE_USER` permitindo `jcr:readprivileges`.
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

   * Defina o valor da url de resumo da tarefa como `/lc/content/SampleSummary.html` na etapa Atribuir tarefa.
   * Quando a tarefa associada a esta etapa Atribuir Tarefa é aberta no espaço de trabalho do AEM Forms, o `html.esp` em `/apps/SampleSummary` é renderizado no painel de resumo da tarefa.
