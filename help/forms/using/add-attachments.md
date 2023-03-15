---
title: Adição de anexos
seo-title: Adding attachments
description: Adicione fotografias e observações de rabisco como anotações à sua tarefa no aplicativo AEM Forms
seo-description: Add photographs and scribble notes as annotations to your task in the AEM Forms app
uuid: 3d2738b4-fd43-44ec-8eaf-a2ad4b7e5af5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: d5976ed2-4482-495c-bf77-6d192379cfef
docset: aem65
exl-id: 82282e2d-63a1-47e9-b2ec-f50a4bd32bd3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# Adição de anexos{#adding-attachments}

## Adicionar anexos em formulários sincronizados com o servidor de fluxo de trabalho do AEM Forms (AEM Forms no JEE) {#adding-annotations}

O aplicativo AEM Forms permite anexar imagens, notas rabiscadas e notas de texto ao seu formulário sincronizado com o servidor AEM Forms JEE. Se o formulário for carregado a partir de um servidor de fluxo de trabalho do AEM Forms, os anexos serão adicionados ao formulário. Toque no botão anexo ![anexos-aplicativo](assets/attachments-app.png) para ver todos os anexos em um formulário juntos. A notificação vermelha especifica o número de anexos no formulário. Se não houver anexos no formulário, você não poderá ver o botão de notificações vermelhas. Se não houver anexos no formulário, ao tocar no botão anexos ![trava](assets/attch.png), você terá opções para anexar fotos ou scripts.

As opções são:

* **Galeria**: Permite adicionar uma imagem das imagens salvas em seu dispositivo.

* **Câmera**: Permite tirar uma imagem e adicioná-la ao formulário.

* **Notas**: Permite adicionar um rabisco ou uma nota de texto. Use ![rabisco](assets/scribble.png) para adicionar um rabisco, e ![teclado](assets/keyboard.png) para adicionar uma nota de texto.

>[!NOTE]
>
>Os anexos adicionados por um usuário ficam visíveis para outros usuários do aplicativo AEM Forms. Outros usuários não podem excluir anexos adicionados por um usuário.

### A tela Anexos {#the-attachments-screen}

Para ver todos os anexos em um local, toque em ![anexos-aplicativo](assets/attachments-app.png). Você pode adicionar, renomear e excluir anexos aqui.

![Todos os anexos num local](assets/attachments-screen.png)

Você pode usar o **+** no ecrã Anexos para anexar outra imagem, rabisco ou texto.

### Adicionar uma fotografia {#adding-a-photograph}

Você pode usar a câmera de seu dispositivo móvel ou imagens salvas em seu dispositivo para anexar uma imagem no formulário.

1. Toque no botão de anexo ![trava](assets/attch.png) na parte inferior da janela.
1. Toque **Galeria** ou **Câmera** na janela pop-up exibida.
1. Com base na opção selecionada, execute o seguinte procedimento:

   1. Se você selecionar **Câmera**.

      Tire uma foto. Em seguida, toque no **Use** ![pic de uso](assets/use-pic.png) botão.

      Ou toque no **Retorne** ![tentativa](assets/retake.png) botão para retomar a fotografia.

   1. Se você selecionar **Galeria**.

      O navegador de imagens do dispositivo é exibido. No navegador de imagens do seu dispositivo, toque na imagem que deseja anexar.

### Adicionar uma observação {#adding-a-note}

O **Notas** A opção permite adicionar rabiscos à mão livre e anexos de texto no formulário.

1. Toque no botão de anexo ![trava](assets/attch.png) na parte inferior da janela.
1. Toque **Notas** na janela pop-up exibida.
1. Na interface do usuário do Notes que é iniciada, capture um rabisco à mão livre.

   ![Interface de rabisco](assets/scribble-ui.png)

   rabisco

   Você pode usar as seguintes opções na interface do Scribble:

   * **Limpar**: Apaga a tela.
   * **Botão Concluído**: Anexa o rabisco atual.
   * **Botão Cancelar**: Descarta o script atual e sai da interface do usuário do Scribble.
   * ![teclado](assets/keyboard.png): Apaga o rabisco e permite que você adicione uma nota de texto.

   ![Teclado no rabisco do aplicativo AEM Forms](assets/keyboard-inapp.png)

## Anexos em formulários sincronizados com os servidores da AEM Forms sem fluxo de trabalho do AEM Forms (AEM Forms no OSGi) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

Os anexos de formulários móveis sincronizados com os servidores OSGi da AEM Forms funcionam de forma semelhante aos servidores AEM Forms JEE.

Os anexos no nível do formulário não são suportados em formulários adaptáveis carregados no aplicativo a partir de um servidor OSGi da AEM Forms. Para anexar imagens ou notas de texto, ative anexos em nível de campo no formulário ao criá-lo. Arraste e solte o componente de anexo de arquivo do navegador de componentes no campo .

No caso de formulários adaptáveis, é possível exibir os arquivos anexados no documento de registro (DoR). Consulte [Gerar Documento de Registro para formulários adaptáveis não XFA](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).
