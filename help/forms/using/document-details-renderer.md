---
title: Detalhes do documento para renderizador
seo-title: Document details for renderer
description: Informações conceituais sobre como as renderizações funcionam no espaço de trabalho do AEM Forms para renderizar os vários tipos de formulário e arquivo suportados.
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

# Detalhes do documento para renderizador {#document-details-for-renderer}

## Introdução {#introduction}

Na área de trabalho do AEM Forms, vários tipos de formulários são compatíveis perfeitamente. Dentre elas:

* PDF forms (XDP / Acroform / Flat PDF)
* Novos formulários de HTML
* Imagens
* Aplicativos de terceiros (por exemplo, Gerenciamento de correspondência)

Este documento explica o funcionamento desses renderizadores da perspectiva de personalização semântica/reutilização de componentes, de modo que os requisitos do cliente sejam atendidos sem quebrar nenhuma renderização. Embora o espaço de trabalho do AEM Forms permita qualquer interface de usuário/alteração semântica, é recomendável que a lógica de renderização de diferentes tipos de formulário não seja alterada, caso contrário, os resultados podem ser imprevisíveis. Este documento serve para orientação/conhecimento que oferece suporte à renderização do mesmo formulário, usando os mesmos componentes do espaço de trabalho em portais diferentes, e não para modificar a lógica de renderização em si.

## PDF forms {#pdf-forms}

PDF forms são renderizadas por `PdfTaskForm View`.

Quando um formulário XDP é renderizado como PDF, um `FormBridge` O JavaScript™ é adicionado pelo serviço FormsAugmenter. Esse JavaScript™ (dentro do formulário PDF) ajuda a executar ações como enviar formulário, salvar formulário ou tomar formulário offline.

Na área de trabalho do AEM Forms, a exibição do PDFTaskForm se comunica com a variável `FormBridge`javascript, por meio de um HTML intermediário presente em `/lc/libs/ws/libs/ws/pdf.html`. O fluxo é:

**Exibição PDFTaskForm - pdf.html**

Comunica-se usando `window.postMessage` / `window.attachEvent('message')`

Esse método é o modo padrão de comunicação entre um quadro pai e um iframe. Os ouvintes de eventos existentes de PDF forms anteriormente abertos são removidos antes de adicionar um novo. Essa limpeza também considera a alternância entre a guia formulário e a guia Histórico na visualização de detalhes da tarefa.

**pdf.html - `FormBridge`javascript no PDF renderizado**

Comunica-se usando `pdfObject.postMessage` / `pdfObject.messageHandler`

Este método é o modo padrão de comunicação com um PDFJavaScript de um HTML. A exibição PdfTaskForm também cuida de PDF simples e a renderiza claramente.

>[!NOTE]
>
>Não é recomendável modificar o conteúdo do pdf.html / da exibição PdfTaskForm.

## Novo HTML Forms {#new-html-forms}

Os novos formulários HTML são renderizados por NewHTMLTaskForm View.

Quando um formulário XDP é renderizado como HTML usando o pacote de formulários móveis implantado no CRX, ele também adiciona outros `FormBridge`JavaScript para o formulário, que expõe diferentes métodos para salvar e enviar dados do formulário.

Esse JavaScript é diferente daquele mencionado no PDF forms acima, mas tem um propósito semelhante.

>[!NOTE]
>
>Não é recomendável modificar o conteúdo da exibição NewHTMLTaskForm.

## Forms e guias do Flex {#flex-forms-and-guides}

O Flex Forms é renderizado por SwfTaskForm e os guias são renderizados por HtmlTaskForm Views, respectivamente.

No espaço de trabalho do AEM Forms, essas exibições se comunicam com o SWF real que compõe o formulário/guia flexível usando um SWF intermediário presente no `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

A comunicação acontece usando `swfObject.postMessage` / `window.flexMessageHandler`.

Esse protocolo é definido pela variável `WsNextAdapter.swf`. Os `flexMessageHandlers`no objeto window , os formulários SWF abertos anteriormente são removidos antes da adição de um novo. A lógica também considera a alternância entre a guia de formulário e a guia do histórico na exibição de detalhes da tarefa. `WsNextAdapter.swf` é usada para executar várias ações de formulário, como salvar ou enviar.

>[!NOTE]
>
>Não é recomendável modificar `WSNextAdapter.swf` ou o conteúdo da exibição SwfTaskForm / HtmlTaskForm.

## Aplicativos de terceiros (por exemplo, Gerenciamento de correspondência) {#third-party-applications-for-example-correspondence-management}

Os aplicativos de terceiros são renderizados usando a exibição ExtAppTaskForm.

**Aplicativo de terceiros para comunicação do espaço de trabalho do AEM Forms**

O espaço de trabalho do AEM Forms escuta em `window.global.postMessage([Message],[Payload])`

[Mensagem] pode ser uma string especificada como `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`no `runtimeMap`. Os aplicativos de terceiros devem usar essa interface para notificar o espaço de trabalho do AEM Forms conforme necessário. O uso dessa interface é obrigatório, pois o espaço de trabalho do AEM Forms deve saber que quando a tarefa é enviada para que possa limpar a janela de tarefas.

**Espaço de trabalho do AEM Forms para comunicação de aplicativos de terceiros**

Se os botões de ação direta do espaço de trabalho do AEM Forms estiverem visíveis, ele chamará `window.[External-App-Name].getMessage([Action])`, onde `[Action]` é lido do `routeActionMap`. O aplicativo de terceiros deve acompanhar essa interface e notificar o AEM Forms workspace por meio do `postMessage ()` API.

Por exemplo, um aplicativo Flex pode definir `ExternalInterface.addCallback('getMessage', listener)` apoiar a presente comunicação. Se o aplicativo de terceiros quiser manipular o envio do formulário por meio de seus próprios botões, você deverá especificar `hideDirectActions = true() in the runtimeMap` e pode ignorar este ouvinte. Portanto, essa construção é opcional.

Você pode ler mais sobre a integração de aplicativos de terceiros em relação ao Gerenciamento de correspondência em [Integração do gerenciamento de correspondência na área de trabalho do AEM Forms](/help/forms/using/integrating-correspondence-management-html-workspace.md).
