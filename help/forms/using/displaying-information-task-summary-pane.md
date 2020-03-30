---
title: Exibição de informações no painel Resumo da Tarefa
seo-title: Exibição de informações no painel Resumo da Tarefa
description: Na área de trabalho do AEM Forms, um painel Resumo da Tarefa pode ser configurado para resumir a tarefa ou exibir qualquer outra página da Web.
seo-description: Na área de trabalho do AEM Forms, um painel Resumo da Tarefa pode ser configurado para resumir a tarefa ou exibir qualquer outra página da Web.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Exibição de informações no painel Resumo da Tarefa {#displaying-information-in-the-task-summary-pane}

Ao abrir uma tarefa na área de trabalho do AEM Forms, um painel Resumo da Tarefa pode exibir um resumo da tarefa. Essas informações adicionais e relevantes para uma tarefa agregam mais valor ao usuário final da área de trabalho do AEM Forms.

A área de trabalho do AEM Forms permite exibir uma página da Web de sua escolha no painel Resumo da Tarefa. Um processo pode ser criado para exibir um painel Resumo da Tarefa usando o Workbench.

1. Criar um processo de Tarefa Atribuir no Workbench. Para obter mais detalhes sobre a operação Atribuir Tarefa, consulte o tópico Referência de serviço na Ajuda [do](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)Workbench.

   >[!NOTE]
   >
   >Se existir um URL do TaskSummary, a visualização Resumo da Tarefa será aberta por padrão, em vez da visualização de formulário. Nesse caso, mesmo quando um usuário ativa a opção &quot;Abrir o formulário no modo maximizado&quot; em Atribuir Tarefa, o formulário não é aberto no modo maximizado.

1. Configure o campo URL de resumo da Tarefa. Você pode especificar um valor literal, um modelo, uma variável ou uma expressão XPath.
1. Um exemplo de exibição das informações na página Resumo da Tarefa é mostrado abaixo.

   * Faça logon no ambiente CRXDE Lite em `https://'[server]:[port]'/lc/crx/de`.
   * `Create a node`**SampleSummary **` under `/` with type `content:`. In the properties of this node, add `unstructuredsling:` of type String and value ``. In the Access Control List of this node, add an entry for `resourceTypeSampleSummaryPERM_WORKSPACE_` allowing `USERjcr:read` privileges.`
   * `Create a folder`**SampleSummary **em`/apps`. Na Lista de Controle de acesso de`/apps/SampleSummary`, adicione uma entrada para`PERM_WORKSPACE_USER`permitir`jcr:readprivileges`.
   * `Create a file `html.esp` at `/apps/`. For example, add the following lines in `SampleSummaryhtml.esp`.`

   ```
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

   * Defina o valor do url de resumo da tarefa como `/lc/content/SampleSummary.html` na etapa Atribuir Tarefa.
   * Quando a tarefa associada à etapa Atribuir Tarefa é aberta na área de trabalho do AEM Forms, a  `html.esp` `/apps/SampleSummary` é renderizada no painel de resumo da tarefa.


[Entre em contato com o suporte](https://www.adobe.com/account/sign-in.supportportal.html)
