---
title: Salvar uma tarefa ou formulário como rascunho
seo-title: Saving a task or form as a draft
description: Etapas para salvar uma cópia de rascunho de uma tarefa ou um formulário no aplicativo AEM Forms
seo-description: Steps to save a draft copy of a task or a form in the AEM Forms app
uuid: 1192d2c2-05a4-4a96-9015-e56111aa2646
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9950288c-b5a2-4945-afad-be9ce2abc8e9
exl-id: b4a23b2e-ab18-402c-8dfa-2533ee692912
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# Salvar uma tarefa ou formulário como rascunho {#saving-a-task-or-form-as-a-draft}

A opção Salvar como rascunho salva um instantâneo de uma tarefa ou formulário junto com os dados preenchidos no formulário associado. Você também pode criar um rascunho a partir de um template. Os rascunhos são salvos no dispositivo móvel e sincronizados com o servidor Adobe Experience Manager Forms para uma recuperação posterior.

Você pode [atualizar o formulário](/help/forms/using/working-with-form.md), [anotá-lo](/help/forms/using/add-attachments.md) com fotografias e notas de rabisco. Como você continua atualizando um formulário, é recomendável salvá-lo como rascunho. Para situações em que você decide enviar um formulário preenchido posteriormente, é útil salvá-lo como rascunho.

Para permitir salvar como recurso de rascunho para formulários salvos no portal de formulários, consulte [Como salvar um formulário HTML5 como rascunho](/help/forms/using/saving-html5-form-draft.md).
Para configurar o envio de formulários adaptáveis, consulte [Componentes de rascunhos e envios](/help/forms/using/draft-submission-component.md). (Não é válido para formulários sincronizados com o servidor AEM Forms JEE.)

Para criar um rascunho, abra o formulário e toque no **Salvar como rascunho** ![salvar como rascunho](assets/save-as-draft.png). Forneça o nome do rascunho e toque em **Salvar**. O rascunho é salvo na pasta Rascunhos e sincronizado com o servidor. Ele é salvo na pasta Caixa de saída se o aplicativo estiver offline.

Se o formulário correspondente for atualizado posteriormente, as alterações serão refletidas imediatamente. Ao sincronizar o aplicativo do AEM Forms com o servidor do AEM Forms, o rascunho é carregado no servidor do AEM Forms. Além disso, o rascunho é movido da Caixa de saída para a pasta Tarefas ou Rascunhos . Um ícone de edição é exibido ao lado dele.

À medida que você continua trabalhando em várias tarefas e pontos de início e as salva, os rascunhos são salvos. Cada vez que seu aplicativo é sincronizado com o servidor do AEM Forms, o rascunho é salvo no servidor. Isso garante que, a qualquer momento, você possa recuperar os rascunhos com base na última data e hora salvas. Por exemplo, se você reinstalar o aplicativo ou alterar seu dispositivo móvel, poderá baixar o rascunho do servidor.

## Excluir um rascunho {#delete-a-draft}

A pasta rascunhos lista todos os rascunhos. Você pode usar a opção Excluir rascunho para excluir permanentemente os rascunhos do dispositivo móvel e do servidor.

A opção para excluir rascunhos criados de uma tarefa não está disponível. Ao excluir um rascunho criado de uma tarefa, a tarefa é abandonada.

Você pode descartar rascunhos no modo offline e online. Ao descartar os rascunhos no modo offline, os rascunhos são excluídos do servidor somente quando a conexão com o servidor é restaurada.

Execute as seguintes etapas para excluir um rascunho:

1. No aplicativo AEM Forms, navegue até **Forms.**
1. Selecionar **Rascunhos** no menu suspenso ao lado de Pesquisar.
1. Um formulário com o ícone de edição ![editar-rascunho-aplicativo](assets/edit-draft-app.png) indica um rascunho. Toque nas reticências horizontais ao lado do rascunho.
1. Nas opções que aparecem ao tocar nas reticências horizontais, toque em **Excluir rascunho**.
