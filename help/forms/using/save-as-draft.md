---
title: Salvamento de uma tarefa ou formulário como rascunho
description: Etapas para salvar uma cópia de rascunho de uma tarefa ou um formulário no aplicativo AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: b4a23b2e-ab18-402c-8dfa-2533ee692912
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# Salvamento de uma tarefa ou formulário como rascunho {#saving-a-task-or-form-as-a-draft}

A opção salvar como rascunho salva um instantâneo de uma tarefa ou formulário junto com os dados preenchidos no formulário associado. Você também pode criar um rascunho de um modelo. Os rascunhos são salvos no dispositivo móvel e sincronizados com o servidor do Adobe Experience Manager Forms para uma recuperação posterior.

Você pode [atualizar o formulário](/help/forms/using/working-with-form.md), [anotar](/help/forms/using/add-attachments.md) com fotografias e notas escritas. À medida que você continua a atualizar um formulário, é recomendável salvá-lo como rascunho. Para situações em que você decide enviar um formulário preenchido posteriormente, é útil salvá-lo como rascunho.

Para ativar o recurso Salvar como rascunho para formulários salvos no portal de formulários, consulte [Salvamento de um formulário HTML 5 como rascunho](/help/forms/using/saving-html5-form-draft.md).
Para configurar o envio de formulários adaptáveis, consulte [Rascunhos e componentes de envios](/help/forms/using/draft-submission-component.md). (Não válido para formulários sincronizados com o servidor AEM Forms JEE.)

Para criar um rascunho, abra o formulário e selecione a **Salvar como rascunho** ![salvar como rascunho](assets/save-as-draft.png). Forneça o nome do rascunho e selecione **Salvar**. O rascunho é salvo na pasta Rascunhos e sincronizado com o servidor. Ele é salvo na pasta Caixa de saída se o aplicativo estiver offline.

Se você atualizar o formulário correspondente posteriormente, as alterações serão refletidas imediatamente. Ao sincronizar o aplicativo do AEM Forms com o servidor do AEM Forms, o rascunho é carregado no servidor do AEM Forms. Além disso, o rascunho é movido da Caixa de saída para a pasta Tarefas ou Rascunhos. Um ícone de edição é exibido ao lado dele.

À medida que você continua trabalhando em várias tarefas e pontos de partida e as salva, os rascunhos são salvos. Cada vez que seu aplicativo é sincronizado com o servidor do AEM Forms, o rascunho é salvo no servidor. Ele garante que, a qualquer momento, você possa recuperar os rascunhos com base na última data e hora salvas. Por exemplo, se você reinstalar o aplicativo ou alterar o dispositivo móvel, poderá baixar o rascunho do servidor.

## Excluir um rascunho {#delete-a-draft}

A pasta de rascunhos lista todos os rascunhos. Você pode usar a opção Excluir rascunho para excluir permanentemente os rascunhos do dispositivo móvel e do servidor.

A opção para excluir rascunhos criados de uma tarefa não está disponível. Ao excluir um rascunho criado de uma tarefa, a tarefa é abandonada.

É possível descartar rascunhos nos modos off-line e on-line. Ao descartar os rascunhos no modo offline, eles são excluídos do servidor somente quando a conexão com o servidor é restaurada.

Execute as seguintes etapas para deletar um rascunho:

1. No aplicativo AEM Forms, navegue até **Forms.**
1. Selecionar **Rascunhos** no menu suspenso ao lado de Pesquisar.
1. Um formulário com o ícone de edição ![edit-draft-app](assets/edit-draft-app.png) indica um rascunho. Selecione as reticências horizontais ao lado do rascunho.
1. Nas opções exibidas ao selecionar as reticências horizontais, selecione **Excluir rascunho**.
