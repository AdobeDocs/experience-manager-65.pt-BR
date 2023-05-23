---
title: Trabalhar com pontos iniciais
seo-title: Working with Startpoints
description: Etapas para trabalhar com um processo do AEM Forms no dispositivo móvel definido no Workbench.
seo-description: Steps to work with a AEM Forms process from your Mobile device defined in Workbench.
uuid: 1c4b4c86-cbdb-4e72-b0eb-7f8a2f5dcdde
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 1ea60fb2-cf9f-4a87-bd8e-98150e668456
docset: aem65
exl-id: d5970f90-2899-43a5-a3a0-61a2c844d919
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Trabalhar com pontos iniciais{#working-with-startpoints}

Um ponto inicial invoca um processo criado no Workbench. Está associado a um formulário que chama o processo quando o formulário é enviado.

>[!NOTE]
>
>Os termos pontos de partida, processo de início e formulário são usados alternadamente ao fazer referência a esse conceito.

Para iniciar um processo no aplicativo AEM Forms, é necessário ter um ponto de partida do tipo **Workspace** em seu processo. Além disso, é necessário selecionar a variável **[!UICONTROL Visível no Espaço de trabalho móvel]** para o ponto de partida.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Para iniciar um processo definido na Bancada**

1. Para exibir os pontos iniciais disponíveis no aplicativo AEM Forms, acesse [Tela inicial](../../forms/using/home-screen.md).
1. No **[!UICONTROL Início]** por padrão, a variável **[!UICONTROL Todos os Forms]** é exibida.

   O ponto inicial está associado a um formulário. Toque no ponto de partida associado ao formulário na lista para abri-lo.

   O formulário associado ao ponto inicial é aberto.

1. Insira os detalhes na **[!UICONTROL Ponto inicial]** formulário.

   É possível adicionar anotações a essa tarefa usando o [anexo](../../forms/using/add-attachments.md) botão.

1. Depois de preencher o formulário, toque no **[!UICONTROL Enviar]** botão.

Se o aplicativo estiver offline, o formulário e seus dados serão salvos na pasta Caixa de saída.

Se o aplicativo estiver online, a tarefa será sincronizada com o servidor do AEM Forms e atribuída ao usuário especificado no processo.

Para trabalhar com a tarefa na sua lista de tarefas, consulte [Abrindo uma tarefa](/help/forms/using/open-task.md).
