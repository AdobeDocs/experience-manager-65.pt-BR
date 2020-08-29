---
title: Trabalhar com pontos de partida
seo-title: Trabalhar com pontos de partida
description: Etapas para trabalhar com um processo AEM Forms a partir do dispositivo móvel definido no Workbench.
seo-description: Etapas para trabalhar com um processo AEM Forms a partir do dispositivo móvel definido no Workbench.
uuid: 1c4b4c86-cbdb-4e72-b0eb-7f8a2f5dcdde
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 1ea60fb2-cf9f-4a87-bd8e-98150e668456
docset: aem65
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Trabalhar com pontos de partida{#working-with-startpoints}

Um ponto de partida chama um processo criado no Workbench. Ele é associado a um formulário que chama o processo quando o formulário é enviado.

>[!NOTE]
>
>Os termos pontos de partida, processo de start e formulário são usados de forma intercambiável ao se referirem a esse conceito.

Para iniciar um processo a partir do aplicativo AEM Forms, é necessário ter um ponto de partida do tipo **Workspace** em seu processo. Além disso, é necessário selecionar a opção **[!UICONTROL Visível no Mobile Workspace]** para o ponto de partida.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Para start de um processo definido no Workbench**

1. Para visualização dos pontos de partida disponíveis no aplicativo AEM Forms, vá para a tela [inicial](../../forms/using/home-screen.md).
1. Na tela **[!UICONTROL Início]** , por padrão, a lista **[!UICONTROL Todos os Forms]** é exibida.

   O ponto de partida está associado a um formulário. Toque no formulário associado ao ponto de partida na lista para abri-lo.

   O formulário associado ao ponto de partida é aberto.

1. Insira os detalhes no formulário **[!UICONTROL Ponto de partida]** .

   É possível adicionar anotações a essa tarefa usando o botão [anexo](../../forms/using/add-attachments.md) .

1. Depois de preencher o formulário, toque no botão **[!UICONTROL Enviar]** .

Se o aplicativo estiver offline, o formulário e seus dados serão salvos na pasta Caixa de saída.

Se o aplicativo estiver online, a tarefa será sincronizada com o servidor AEM Forms e atribuída ao usuário especificado no processo.

Para trabalhar com a tarefa na lista da tarefa, consulte [Abrindo uma tarefa](/help/forms/using/open-task.md).
