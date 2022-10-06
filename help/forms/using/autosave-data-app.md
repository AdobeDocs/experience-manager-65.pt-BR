---
title: Usar o salvamento automático no aplicativo AEM Forms
seo-title: Using autosave in AEM Forms app
description: Saiba como usar o recurso de salvamento automático no aplicativo AEM Forms que permite evitar perda de dados.
seo-description: Learn how to use autosave feature in AEM Forms app that lets you avoid data loss.
uuid: 00fe6a10-1a72-443d-a840-0415dc769199
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2c71cc28-b7c8-4785-9fc2-b47fa80cbd70
docset: aem65
exl-id: 1603eef1-d7c8-47d3-8cfa-55ec3eaadd64
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Usar o salvamento automático no aplicativo AEM Forms{#using-autosave-in-aem-forms-app}

Quando um usuário insere dados no aplicativo Adobe Experience Manager Forms, o recurso de salvamento automático os salva em intervalos regulares. O recurso de salvamento automático no aplicativo AEM Forms ajuda você a evitar perda de dados se o aplicativo for fechado acidentalmente.

Seu aplicativo pode fechar acidentalmente:

* Se o seu dispositivo desligar devido a pouca bateria
* Se o usuário matar o aplicativo
* Se ocorrer uma falha inesperada

Você pode especificar os intervalos após os quais o aplicativo salva os dados inseridos.

>[!NOTE]
>
>Selecione a frequência do salvamento automático criteriosamente. Operações frequentes de salvamento automático podem ter um impacto notório no desempenho do dispositivo.

Execute as seguintes etapas para usar o recurso de salvamento automático no aplicativo AEM Forms:

1. Faça logon no aplicativo e navegue até **Configurações > Geral**.
1. Na tela Geral, use o **Frequência de Salvamento Automático** para selecionar os intervalos em que deseja que o aplicativo salve os dados inseridos.
   [ ![Configuração da frequência de salvamento automático](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. Ao reiniciar o aplicativo e fazer logon com o mesmo usuário, você é solicitado a restaurar a tarefa com a caixa de diálogo Recuperar tarefa não salva. Clique em **OK** na caixa de diálogo Recuperar tarefa não salva para retomar o trabalho com a tarefa salva. Você pode clicar em **Cancelar** para excluir os dados salvos correspondentes ao último salvamento automático acionado e começar a trabalhar com uma nova tarefa.

   Ao clicar em **OK**, a tarefa é restaurada com os dados correspondentes ao salvamento automático mais recente acionado antes que o aplicativo travasse. Inclui os dados do formulário e todos os anexos associados à tarefa.
   [ ![Obter uma tarefa recuperada ](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**A.** Um formulário de trabalho em andamento **B.** Aplicativo fechado à força **C.** O aplicativo foi reiniciado com a caixa de diálogo Recuperar tarefa não salva **D.** Formulário restaurado com dados originais
