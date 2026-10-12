---
title: Uso do salvamento automático no aplicativo AEM Forms
description: Saiba como usar o recurso de salvamento automático no aplicativo AEM Forms que permite evitar perda de dados.
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 1603eef1-d7c8-47d3-8cfa-55ec3eaadd64
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%
---
# Uso do salvamento automático no aplicativo AEM Forms{#using-autosave-in-aem-forms-app}

>[!NOTE]
>
>O aplicativo AEM Forms está obsoleto no momento. Para perguntas ou ajuda, contate [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

Quando um usuário insere dados no aplicativo Adobe Experience Manager Forms, o recurso de salvamento automático os salva em intervalos regulares. O recurso de salvamento automático no aplicativo AEM Forms ajuda a evitar a perda de dados se o aplicativo for fechado acidentalmente.

Seu aplicativo pode fechar acidentalmente:

* Se o dispositivo for desligado devido à bateria fraca
* Se o usuário matar o aplicativo
* Se ocorrer uma falha inesperada

Você pode especificar os intervalos após os quais o aplicativo salva os dados inseridos.

>[!NOTE]
>
>Selecione a frequência de salvamento automático criteriosamente. Operações frequentes de salvamento automático podem ter um impacto notável no desempenho do dispositivo.

Execute as seguintes etapas para usar o recurso de salvamento automático no aplicativo AEM Forms:

1. Faça logon no aplicativo e navegue até **Configurações > Geral**.
1. Na tela Geral, use a opção **Frequência de salvamento automático** para selecionar os intervalos em que deseja que o aplicativo salve os dados inseridos.
   [![Definindo frequência de salvamento automático](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. Ao reiniciar o aplicativo e fazer logon com o mesmo usuário, você será solicitado a restaurar a tarefa com a caixa de diálogo Recuperar tarefa não salva. Clique em **OK** na caixa de diálogo Recuperar tarefa não salva para continuar a trabalhar com a tarefa salva. Você pode clicar em **Cancelar** para excluir os dados salvos correspondentes ao último salvamento automático acionado e começar a trabalhar com uma nova tarefa.

   Ao clicar em **OK**, a tarefa é restaurada com os dados correspondentes ao salvamento automático mais recente acionados antes da falha do aplicativo. Inclui os dados de formulário e todos os anexos associados à tarefa.
   [![Recuperando uma tarefa &#x200B;](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**A.** Um formulário de trabalho em andamento **B.** O aplicativo foi fechado à força **C.** O aplicativo foi reiniciado com a caixa de diálogo Recuperar Tarefa Não Salva **D.** Formulário restaurado com dados originais
