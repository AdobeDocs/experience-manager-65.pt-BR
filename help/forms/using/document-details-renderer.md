---
title: Detalhes de documento para renderizador
seo-title: Document details for renderer
description: Informações conceituais sobre como os renderizadores funcionam no espaço de trabalho do AEM Forms para renderizar os vários formulários e tipos de arquivos compatíveis.
seo-description: Conceptual information on how renders work in AEM Forms workspace to render the various supported form and file types.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# Detalhes de documento para renderizador {#document-details-for-renderer}

## Introdução {#introduction}

No espaço de trabalho do AEM Forms, vários tipos de formulário são totalmente compatíveis. Dentre elas:

* PDF forms (XDP / Acroform / PDF plana)
* Novos formulários de HTML
* Imagens
* Aplicativos de terceiros (por exemplo, Gerenciamento de correspondência)

Este documento explica o funcionamento desses renderizadores a partir da perspectiva de personalização semântica/reutilização de componentes, de modo que os requisitos do cliente sejam atendidos sem interromper nenhuma representação. Embora o espaço de trabalho do AEM Forms permita alterações na interface do usuário/semântica, é recomendável que a lógica de renderização de diferentes tipos de formulário não seja alterada, caso contrário, os resultados podem ser imprevisíveis. Este documento é para orientação/conhecimento a fim de oferecer suporte à renderização do mesmo formulário, usando os mesmos componentes do espaço de trabalho em portais diferentes, e não para modificar a própria lógica de renderização.

## PDF forms {#pdf-forms}

PDF forms são renderizados por `PdfTaskForm View`.

Quando um formulário XDP é renderizado como PDF, um `FormBridge` O JavaScript™ é adicionado pelo serviço FormsAugmenter. Esse JavaScript™ (dentro do formulário PDF) ajuda a executar ações como enviar formulário, salvar formulário ou usar o formulário offline.

No espaço de trabalho do AEM Forms, a exibição PDFTaskForm se comunica com o `FormBridge`javascript, por meio de um HTML intermediário presente em `/lc/libs/ws/libs/ws/pdf.html`. O fluxo é:

**Exibição de PDFTaskForm - pdf.html**

Comunica-se usando `window.postMessage` / `window.attachEvent('message')`

Esse método é a maneira padrão de comunicação entre um quadro pai e um iframe. Os ouvintes de eventos existentes dos PDF forms abertos anteriormente são removidos antes de adicionar um novo. Essa limpeza também considera a alternância entre a guia de formulário e a guia de histórico na visualização de detalhes da tarefa.

**pdf.html - `FormBridge`javascript dentro do PDF renderizado**

Comunica-se usando `pdfObject.postMessage` / `pdfObject.messageHandler`

Esse método é a maneira padrão de comunicação com um PDFJavaScript de um HTML. A exibição PdfTaskForm também cuida do PDF simples e o renderiza de maneira simples.

>[!NOTE]
>
>Não é recomendável modificar o pdf.html / conteúdo da exibição PdfTaskForm.

## Novo HTML Forms {#new-html-forms}

Novos formulários de HTML são renderizados pela visualização NewHTMLTaskForm.

Quando um Formulário XDP é renderizado como HTML usando o pacote de formulários móveis implantado no CRX, ele também adiciona mais `FormBridge`JavaScript para o formulário, que expõe diferentes métodos para salvar e enviar dados de formulário.

Esse JavaScript é diferente do mencionado nos PDF forms acima, mas tem um propósito semelhante.

>[!NOTE]
>
>Não é recomendável modificar o conteúdo da exibição NewHTMLTaskForm.

## Flex Forms e Guias {#flex-forms-and-guides}

O Flex Forms é renderizado pelo SwfTaskForm e os guias são renderizados pelas Exibições do HtmlTaskForm, respectivamente.

Na área de trabalho do AEM Forms, essas exibições se comunicam com o SWF real que compõe o formulário/guia flexível usando um SWF intermediário presente em `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

A comunicação ocorre usando `swfObject.postMessage` / `window.flexMessageHandler`.

Esse protocolo é definido pela variável `WsNextAdapter.swf`. O atual `flexMessageHandlers`em objetos de janela, formulários de SWF abertos anteriormente são removidos antes de adicionar um novo. A lógica também considera a alternância entre a guia de formulário e a guia de histórico na visualização de detalhes da tarefa. `WsNextAdapter.swf` é usado para executar várias ações de formulário, como salvar ou enviar.

>[!NOTE]
>
>Não é recomendável modificar `WSNextAdapter.swf` ou o conteúdo da exibição SwfTaskForm / HtmlTaskForm.

## Aplicativos de terceiros (por exemplo, Gerenciamento de correspondência) {#third-party-applications-for-example-correspondence-management}

Os aplicativos de terceiros são renderizados usando a exibição ExtAppTaskForm.

**Aplicativo de terceiros para comunicação do espaço de trabalho do AEM Forms**

O espaço de trabalho do AEM Forms escuta em `window.global.postMessage([Message],[Payload])`

[Mensagem] pode ser uma string especificada como `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`no `runtimeMap`. Os aplicativos de terceiros devem usar essa interface para notificar o espaço de trabalho do AEM Forms conforme necessário. O uso dessa interface é obrigatório, pois o espaço de trabalho do AEM Forms deve saber quando a tarefa é enviada para que possa limpar a janela da tarefa.

**Espaço de trabalho do AEM Forms para comunicação com aplicativos de terceiros**

Se os botões de ação direta do espaço de trabalho do AEM Forms estiverem visíveis, ele chamará `window.[External-App-Name].getMessage([Action])`, onde `[Action]` é lida a partir do `routeActionMap`. O aplicativo de terceiros deve escutar nessa interface e notificar o espaço de trabalho do AEM Forms por meio da `postMessage ()` API.

Por exemplo, um aplicativo do Flex pode definir `ExternalInterface.addCallback('getMessage', listener)` para apoiar esta comunicação. Se o aplicativo de terceiros quiser lidar com o envio de formulários por meio de seus próprios botões, será necessário especificar `hideDirectActions = true() in the runtimeMap` e você pode ignorar esse ouvinte. Portanto, essa construção é opcional.

Você pode ler mais sobre a integração de aplicativos de terceiros em relação ao Gerenciamento de correspondência em [Integração do Gerenciamento de correspondência no espaço de trabalho do AEM Forms](/help/forms/using/integrating-correspondence-management-html-workspace.md).
