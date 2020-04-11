---
title: Adicionar anexos
seo-title: Adicionar anexos
description: Adicione fotografias e notas de script como anotações à sua tarefa no aplicativo AEM Forms
seo-description: Adicione fotografias e notas de script como anotações à sua tarefa no aplicativo AEM Forms
uuid: 3d2738b4-fd43-44ec-8eaf-a2ad4b7e5af5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: d5976ed2-4482-495c-bf77-6d192379cfef
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Adicionar anexos{#adding-attachments}

## Adicionar anexos em formulários sincronizados com o servidor de fluxo de trabalho do AEM Forms (AEM Forms no JEE) {#adding-annotations}

O aplicativo AEM Forms permite anexar imagens, notas com script e notas de texto ao formulário sincronizado com o servidor JEE do AEM Forms. Se o formulário for carregado de um servidor de fluxo de trabalho do AEM Forms, seus anexos serão adicionados ao formulário. Você pode tocar no botão de anexo ![anexos-aplicativo](assets/attachments-app.png) para ver todos os anexos em um formulário juntos. A notificação vermelha especifica o número de anexos no formulário. Se não houver anexos no formulário, você não poderá ver o botão de notificações vermelhas. Se não houver anexos no formulário, quando você tocar no botão de anexos ![anexar](assets/attch.png), você obterá opções para anexar fotos ou scripts.

Suas opções são:

* **Galeria**: Permite que você adicione uma imagem das imagens salvas no seu dispositivo.

* **Câmera**: Permite tirar uma foto e adicioná-la ao formulário.

* **Notas**: Permite adicionar um script ou uma nota de texto. Use o ![scribble](assets/scribble.png) para adicionar um scribble e o ![teclado](assets/keyboard.png) para adicionar uma nota de texto.

>[!NOTE]
>
>Os anexos adicionados por um usuário estão visíveis para outros usuários do aplicativo AEM Forms. Outros usuários não podem excluir anexos adicionados por um usuário.


### A tela Anexos {#the-attachments-screen}

Para ver todos os anexos em um lugar, toque em ![anexos-aplicativo](assets/attachments-app.png). Você pode adicionar, renomear e excluir anexos aqui.

![Todos os anexos em um local](assets/attachments-screen.png)

Você pode usar o botão **+** na tela Anexos para anexar outra imagem, um script ou um texto.

### Adicionar uma fotografia {#adding-a-photograph}

Você pode usar a câmera do seu dispositivo móvel ou imagens salvas no seu dispositivo para anexar uma foto no formulário.

1. Toque no botão de anexo ![se encaixe](assets/attch.png) na parte inferior da janela.
1. Toque em **Galeria** ou **Câmera** no pop-up exibido.
1. Com base na opção selecionada, execute o seguinte procedimento:

   1. Se você selecionar **Câmera**.

      Tire uma foto. Em seguida, toque no botão **Use** ![use-pic](assets/use-pic.png) .

      Ou toque no botão **Retake** ![retake](assets/retake.png) (Retirar) para refazer a fotografia.

   1. Se você selecionar **Galeria**.

      O navegador de imagem do dispositivo é exibido. No navegador de imagens do seu dispositivo, toque na imagem que deseja anexar.

### Adicionar uma observação {#adding-a-note}

A opção **Anotações** permite adicionar rabiscos à mão livre e anexos de texto no formulário.

1. Toque no botão de anexo ![se encaixe](assets/attch.png) na parte inferior da janela.
1. Toque em **Notas** no pop-up exibido.
1. Na interface do usuário do Notes que é iniciada, capture um script à mão livre.

   ![Interface do script](assets/scribble-ui.png)

   Rabisco

   Você pode usar as seguintes opções na interface do Scribble:

   * **Limpar**: Limpa a tela.
   * **Botão** Concluído: Anexa o script atual.
   * **Botão** Cancelar: Descarta o script atual e sai da interface do usuário do Scribble.
   * ![teclado](assets/keyboard.png): Limpa o rabisco e permite que você adicione uma nota de texto.
   ![Teclado no script do aplicativo AEM Forms](assets/keyboard-inapp.png)

## Anexos em formulários sincronizados com os servidores de formulários AEM sem fluxo de trabalho de formulários AEM (formulários AEM no OSGi) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

Os anexos para formulários móveis sincronizados com os servidores OSGi do AEM Forms funcionam de forma semelhante aos servidores JEE do AEM Forms.

Os anexos de nível de formulário não são suportados para formulários adaptáveis carregados no aplicativo a partir de um servidor OSGi do AEM Forms. Para anexar imagens ou notas de texto, ative os anexos de nível de campo no formulário ao criá-lo. Arraste e solte o componente de anexo de arquivo do navegador de componentes no campo.

No caso de formulários adaptáveis, você pode visualização os arquivos anexados no documento de registro (DoR). Consulte [Gerar Documento de registro para formulários](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)adaptáveis não XFA.
