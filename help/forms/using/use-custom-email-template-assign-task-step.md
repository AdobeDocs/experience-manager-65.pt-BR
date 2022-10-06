---
title: Usar modelos de email personalizados em uma etapa Atribuir tarefa
seo-title: Use custom email templates in an Assign Task step
description: Modelos de email personalizados para notificações por email do fluxo de trabalho de formulários
seo-description: Custom email templates for forms workflow email notifications
uuid: ba453d54-813f-4a4f-a82e-1a6a28b6939c
topic-tags: publish
discoiquuid: 2ad4b7b5-2162-4599-af3f-9476f1256de6
docset: aem65
exl-id: d4035c91-ee8d-4f12-bdac-e3912be732d7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 1%

---

# Usar modelos de email personalizados em uma etapa Atribuir tarefa{#use-custom-email-templates-in-an-assign-task-step}

Você pode usar a etapa Atribuir tarefa para criar e atribuir tarefas a um usuário ou grupo. Quando uma tarefa é atribuída a um usuário ou grupo, uma notificação por email é enviada ao usuário definido ou a cada membro do grupo definido. Uma notificação de email típica contém um link da tarefa atribuída e informações relacionadas à tarefa. A imagem a seguir exibe um exemplo de notificação por email:

![Notificação por email com modelo pronto para uso](do-not-localize/default_email_template_new.png)

Você pode personalizar a aparência e usar metadados personalizados em uma notificação por email. O AEM Forms fornece um modelo pronto para uso para notificações por email. Você pode personalizar o modelo pronto para uso ou criar um novo modelo do zero.

Os modelos de notificação por email são baseados em [HTML email](https://en.wikipedia.org/wiki/HTML_email). Esses emails se adaptam a diferentes clientes de email e tamanhos de tela. Além disso, o estilo do email é definido no template .

A imagem a seguir exibe uma notificação por email personalizada:

![Notificação por email usando modelo personalizado](do-not-localize/customized-email.png)

## Personalizar o modelo existente {#customize-the-existing-template}

Pronto para uso, o AEM Forms fornece um modelo para notificações por email. O modelo fornece a descrição do título, data de vencimento, prioridade, nome do fluxo de trabalho e link da tarefa atribuída. Você pode personalizar o modelo para alterar a aparência. Execute as seguintes etapas para personalizar o modelo:

1. Faça logon no CRXDE com a conta de administrador.

1. Navegue até /libs/fd/dashboard/templates/email.

1. Abra o arquivo htmlEmailTemplate.txt. Ele contém o template padrão.

1. Substitua o conteúdo do arquivo htmlEmailTemplate.txt por conteúdo personalizado.

   Um modelo de notificação por email é um [HTML email](https://en.wikipedia.org/wiki/HTML_email). Você pode substituir o código html existente pelo seu código personalizado para alterar a aparência do modelo.

1. Salve o arquivo. Agora, o modelo personalizado está pronto para uso.

## Criar um template de email {#create-an-email-template}

Pronto para uso, o AEM Forms fornece um modelo para notificações por email. O modelo fornece a descrição do título, data de vencimento, prioridade, nome do fluxo de trabalho e link da tarefa atribuída. Você também pode adicionar um modelo de email personalizado (seu próprio modelo) para as etapas da tarefa Atribuir. Execute as seguintes etapas para adicionar um modelo de email personalizado:

1. Faça logon no CRXDE com a conta de administrador.

1. Navegue até /libs/fd/dashboard/templates/email.

1. Crie um arquivo .txt. Por exemplo, EmailOnTaskAssign.txt.

1. Adicione o código HTML personalizado ao arquivo.

   Um modelo de notificação por email é um [HTML email](https://en.wikipedia.org/wiki/HTML_email). Você pode adicionar código de HTML personalizado ao arquivo para criar um novo modelo.

1. Salve o arquivo. O modelo está pronto para uso na etapa Atribuir tarefa .

## Usar um modelo de email em uma etapa Atribuir tarefa {#use-an-email-template-in-an-assign-task-step}

Pronto para uso, a etapa Atribuir tarefa está configurada para usar o modelo padrão, htmlEmailTemplate.txt. Você pode optar por usar um modelo personalizado. Para alterar o modelo:

1. Abra a etapa Atribuir tarefa .

1. Navegue até Destinatário > HTML Email Template.

1. Selecione o modelo de email HTML recém-criado.

1. Clique em OK. O modelo é alterado.

Uma notificação por email também usa [metadados](../../forms/using/use-metadata-in-email-notifications.md). Por exemplo, data de vencimento, prioridade, nome do workflow e muito mais. Você também pode configurar o modelo para usar [metadados personalizados](../../forms/using/use-metadata-in-email-notifications.md#using-custom-metadata-in-an-email-notification).
