---
title: Adicionando anexos
description: Adicione fotografias e anotações como anotações à sua tarefa no aplicativo AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 82282e2d-63a1-47e9-b2ec-f50a4bd32bd3
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# Adicionando anexos{#adding-attachments}

## Adicionar anexos em formulários sincronizados com o servidor do AEM Forms Workflow (AEM Forms no JEE) {#adding-annotations}

O aplicativo AEM Forms permite anexar imagens, anotações com script e notas de texto ao seu formulário sincronizado com o servidor do AEM Forms JEE. Se o formulário for carregado de um servidor do AEM Forms Workflow, os anexos serão adicionados ao formulário. Você pode tocar no botão de anexo ![anexos-aplicativo](assets/attachments-app.png) para ver todos os anexos em um formulário juntos. A notificação em vermelho especifica o número de anexos no formulário. Se não houver anexos no formulário, você não poderá ver o botão vermelho de notificações. Se não houver anexos no formulário, ao tocar no botão anexos ![anexar](assets/attch.png), você tem opções para anexar fotos ou rabiscos.

As opções são:

* **Galeria**: permite adicionar uma imagem das imagens salvas no dispositivo.

* **Câmera**: Permite tirar uma foto e adicioná-la ao formulário.

* **Notas**: permite adicionar um rabisco ou uma nota de texto. Uso ![rabisco](assets/scribble.png) para adicionar um rabisco e ![teclado](assets/keyboard.png) para adicionar uma nota de texto.

>[!NOTE]
>
>Os anexos adicionados por um usuário ficam visíveis para outros usuários do aplicativo AEM Forms. Outros usuários não podem excluir anexos adicionados por um usuário.
>

### A tela Attachments {#the-attachments-screen}

Para ver todos os anexos em um local, toque em ![anexos-aplicativo](assets/attachments-app.png). Você pode adicionar, renomear e excluir anexos aqui.

![Todos os anexos em um local](assets/attachments-screen.png)

Você pode usar o **+** botão na tela Anexos para anexar outra imagem, rabisco ou texto.

### Adicionar uma fotografia {#adding-a-photograph}

Você pode usar a câmera do dispositivo móvel ou as imagens salvas no dispositivo para anexar uma imagem no formulário.

1. Toque no botão de anexo ![anexar](assets/attch.png) na parte inferior da janela.
1. Toque **Galeria** ou **Câmera** no pop-up exibido.
1. Com base na opção selecionada, execute o seguinte procedimento:

   1. Se você selecionar **Câmera**.

      Tire uma foto. Em seguida, toque no **Uso** ![use-pic](assets/use-pic.png) botão.

      Ou toque no **Refazer** ![retomar](assets/retake.png) botão para tirar a fotografia novamente.

   1. Se você selecionar **Galeria**.

      O navegador de imagens do dispositivo aparece. No navegador de imagens do dispositivo, toque na imagem que deseja anexar.

### Adição de uma observação {#adding-a-note}

A variável **Notas** permite adicionar rabiscos à mão livre e anexos de texto ao formulário.

1. Toque no botão de anexo ![anexar](assets/attch.png) na parte inferior da janela.
1. Toque **Notas** no pop-up exibido.
1. Na interface do usuário do Notes que é iniciada, capture um rabisco à mão livre.

   ![Interface de rabisco](assets/scribble-ui.png)

   Rabiscar

   Você pode usar as seguintes opções na interface Rabiscar:

   * **Limpar**: limpa a tela.
   * **Botão Concluído**: anexa o rabisco atual.
   * **Botão Cancelar**: Descarta o rabisco atual e sai da interface do usuário Rabiscar.
   * ![teclado](assets/keyboard.png): limpa o rabisco e permite adicionar uma nota de texto.

   ![Teclado no rabisco do aplicativo AEM Forms](assets/keyboard-inapp.png)

## Anexos em formulários sincronizados com os servidores do AEM Forms sem o AEM Forms Workflow (AEM Forms no OSGi) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

Os anexos para formulários móveis sincronizados com os servidores OSGi da AEM Forms funcionam de forma semelhante aos servidores AEM Forms JEE.

Os anexos no nível do formulário não são compatíveis com formulários adaptáveis carregados no aplicativo de um servidor OSGi do AEM Forms. Para anexar imagens ou notas de texto, ative os anexos em nível de campo no formulário ao criá-lo. Arraste e solte o componente de anexo de arquivo do navegador de componentes no campo.

Se houver formulários adaptáveis, você poderá visualizar os arquivos anexados no documento de registro (DoR). Consulte [Gerar documento de registro para formulários adaptáveis não XFA](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).
