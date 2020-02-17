---
title: Usar o salvamento automático no aplicativo AEM Forms
seo-title: Usar o salvamento automático no aplicativo AEM Forms
description: Saiba como usar o recurso de salvar automaticamente no aplicativo AEM Forms que permite evitar perda de dados.
seo-description: Saiba como usar o recurso de salvar automaticamente no aplicativo AEM Forms que permite evitar perda de dados.
uuid: 00fe6a10-1a72-443d-a840-0415dc769199
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2c71cc28-b7c8-4785-9fc2-b47fa80cbd70
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Usar o salvamento automático no aplicativo AEM Forms{#using-autosave-in-aem-forms-app}

Quando um usuário digita dados no aplicativo Adobe Experience Manager Forms, o recurso de salvamento automático os salva em intervalos regulares. O recurso de salvar automaticamente no aplicativo AEM Forms ajuda a evitar perda de dados se o aplicativo for fechado acidentalmente.

Seu aplicativo pode fechar acidentalmente:

* Se o seu dispositivo desligar devido a bateria fraca
* Se o usuário matar o aplicativo
* Se ocorrer uma falha inesperada

Você pode especificar os intervalos após os quais o aplicativo salva os dados digitados.

>[!NOTE]
>
>Selecione a frequência de salvamento automático criteriosamente. Operações frequentes de salvamento automático podem ter um impacto notável no desempenho do dispositivo.

Execute as seguintes etapas para usar o recurso de gravação automática no aplicativo AEM Forms:

1. Faça logon no aplicativo e navegue até **Configurações > Geral**.
1. Na tela Geral, use a opção Frequência **de** salvamento automático para selecionar os intervalos nos quais deseja que o aplicativo salve os dados digitados.
   [ ![Configuração da frequência de salvamento automático](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. Ao reiniciar o aplicativo e fazer logon com o mesmo usuário, você será solicitado a restaurar sua tarefa com a caixa de diálogo Recuperar tarefa não salva. Clique em **OK** na caixa de diálogo Recuperar tarefa não salva para retomar o trabalho com a tarefa salva. Você pode clicar em **Cancelar** para excluir os dados salvos correspondentes ao último salvamento automático acionado e começar a trabalhar com uma nova tarefa.

   Quando você clica em **OK**, a tarefa é restaurada com os dados correspondentes ao salvamento automático mais recente acionado antes que o aplicativo falhe. Inclui os dados do formulário e todos os anexos associados à tarefa.
   [![](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)****A** obtenção de uma tarefa **recuperadaA. Um formulário de trabalho em andamento** B. O aplicativo fechou com força **C.** O aplicativo foi reiniciado com a caixa de diálogo Recuperar tarefa não salva **D. Formulário restaurado com dados originais

