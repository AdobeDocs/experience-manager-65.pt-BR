---
title: Detalhes de documento para renderizador
description: Informações conceituais sobre como os renderizadores funcionam no espaço de trabalho do AEM Forms para renderizar os vários tipos de formulário e arquivo compatíveis.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# Detalhes de documento para renderizador {#document-details-for-renderer}

## Introdução {#introduction}

No espaço de trabalho do AEM Forms, vários tipos de formulário são totalmente compatíveis. Dentre elas:

* PDF forms (XDP / Acroform / PDF plana)
* Novos formulários de HTML
* Imagens
* Aplicativos de terceiros (por exemplo, Gerenciamento de correspondência)

Este documento explica o funcionamento desses renderizadores a partir da perspectiva de personalização semântica/reutilização de componentes, de modo que os requisitos do cliente sejam atendidos sem interromper nenhuma representação. Embora o espaço de trabalho do AEM Forms permita alterações na interface do usuário/semântica, é recomendável que a lógica de renderização de diferentes tipos de formulário não seja alterada, caso contrário, os resultados podem ser imprevisíveis. Este documento é para orientação/conhecimento a fim de suportar a renderização do mesmo formulário, usando os mesmos componentes do espaço de trabalho em portais diferentes, e não para modificar a própria lógica de renderização.

## PDF forms {#pdf-forms}

Os PDF forms são renderizados por `PdfTaskForm View`.

Quando um formulário XDP é renderizado como PDF, um JavaScript™ `FormBridge` é adicionado pelo serviço FormsAugmenter. Este JavaScript™ (dentro do formulário PDF) ajuda a executar ações como enviar formulário, salvar formulário ou usar o formulário offline.

No espaço de trabalho do AEM Forms, a exibição PDFTaskForm se comunica com o `FormBridge`JavaScript, por meio de um HTML intermediário presente em `/lc/libs/ws/libs/ws/pdf.html`. O fluxo é:

**modo de exibição PDFTaskForm - pdf.html**

Comunica-se usando o `window.postMessage` / `window.attachEvent('message')`

Esse método é a maneira padrão de comunicação entre um quadro pai e um iframe. Os ouvintes de eventos existentes dos PDF forms abertos anteriormente são removidos antes de adicionar um novo. Essa limpeza também considera a alternância entre a guia de formulário e a guia de histórico na visualização de detalhes da tarefa.

**pdf.html - `FormBridge`JavaScript dentro do PDF renderizado**

Comunica-se usando o `pdfObject.postMessage` / `pdfObject.messageHandler`

Esse método é a maneira padrão de comunicação com um PDFJavaScript de um HTML. A exibição PdfTaskForm também cuida de um PDF simples e o renderiza sem formatação.

>[!NOTE]
>
>Não é recomendável editar o pdf.html / conteúdo da exibição PdfTaskForm.

## Novo HTML Forms {#new-html-forms}

Novos formulários de HTML são renderizados pela visualização NewHTMLTaskForm.

Quando um Formulário XDP é renderizado como HTML usando o pacote de formulários móveis implantado no CRX, ele também adiciona `FormBridge`JavaScript ao formulário, o que expõe diferentes métodos para salvar e enviar dados de formulário.

Esse JavaScript é diferente do mencionado nos PDF forms acima, mas tem um propósito semelhante.

>[!NOTE]
>
>O Adobe não recomenda editar o conteúdo da visualização NewHTMLTaskForm.

## Flex Forms e Guias {#flex-forms-and-guides}

O Flex Forms é renderizado pelo SwfTaskForm e os guias são renderizados pelas Exibições do HtmlTaskForm, respectivamente.

No espaço de trabalho do AEM Forms, essas exibições se comunicam com o SWF real que compõe o Flex® form/guia usando um SWF intermediário presente em `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

A comunicação ocorre usando o `swfObject.postMessage` / `window.flexMessageHandler`.

Este protocolo é definido pelo `WsNextAdapter.swf`. O `flexMessageHandlers`objeto da janela existente, de formulários de SWF abertos anteriormente, é removido antes da adição de um novo. A lógica também considera a alternância entre a guia de formulário e a guia de histórico na visualização de detalhes da tarefa. O `WsNextAdapter.swf` é usado para executar várias ações de formulário, como salvar ou enviar.

>[!NOTE]
>
>Não é recomendável modificar `WSNextAdapter.swf` ou o conteúdo da exibição SwfTaskForm / HtmlTaskForm.

## Aplicativos de terceiros (por exemplo, Gerenciamento de correspondência) {#third-party-applications-for-example-correspondence-management}

Os aplicativos de terceiros são renderizados usando a exibição ExtAppTaskForm.

**Aplicativo de terceiros para comunicação com o espaço de trabalho do AEM Forms**

O espaço de trabalho do AEM Forms escuta em `window.global.postMessage([Message],[Payload])`

[A mensagem] pode ser uma cadeia de caracteres especificada como `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`no `runtimeMap`. Os aplicativos de terceiros devem usar essa interface para notificar o espaço de trabalho do AEM Forms conforme necessário. O uso dessa interface é obrigatório, pois o espaço de trabalho do AEM Forms deve saber quando a tarefa é enviada para que possa limpar a janela da tarefa.

**espaço de trabalho do AEM Forms para comunicação com aplicativos de terceiros**

Se os botões de ação direta do espaço de trabalho do AEM Forms estiverem visíveis, ele chamará `window.[External-App-Name].getMessage([Action])`, em que `[Action]` é lido do `routeActionMap`. O aplicativo de terceiros deve escutar nesta interface e, em seguida, notificar o espaço de trabalho do AEM Forms por meio da API `postMessage ()`.

Por exemplo, um aplicativo do Flex pode definir `ExternalInterface.addCallback('getMessage', listener)` para dar suporte a essa comunicação. Se o aplicativo de terceiros quiser lidar com o envio de formulários por meio de seus próprios botões, especifique `hideDirectActions = true() in the runtimeMap` e você poderá ignorar esse ouvinte. Portanto, essa construção é opcional.

Você pode ler mais sobre a integração de aplicativos de terceiros relacionados ao Gerenciamento de correspondência em [Integrando o Gerenciamento de correspondência no espaço de trabalho do AEM Forms](/help/forms/using/integrating-correspondence-management-html-workspace.md).
