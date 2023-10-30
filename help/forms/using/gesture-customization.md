---
title: Personalização de gesto
description: Saiba como personalizar os gestos no aplicativo AEM Forms. É possível personalizar os gestos para fornecer um método distinto de interação com o aplicativo.
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Personalização de gesto {#gesture-customization}

É possível personalizar os gestos do aplicativo AEM Forms para fornecer um método distinto de interação com o aplicativo. Por exemplo, é possível adicionar novos gestos para abrir ou fechar uma tarefa ou um ponto inicial.

## Para personalizar gestos no aplicativo AEM Forms {#to-customize-gestures-in-aem-forms-app}

No aplicativo AEM Forms, o deslizamento para a esquerda abre uma nova tarefa ou um ponto inicial, enquanto o deslizamento para a direita não faz nada. O exemplo a seguir fornece etapas para abrir uma nova tarefa ou ponto de partida ao executar os gestos de deslizar com o botão direito do mouse no aplicativo AEM Forms.

1. Abra o projeto.

   * Para o iOS, abra `Capture.xcodeproj` no Xcode
   * Para Android, abra o projeto Android no Eclipse.
   * Para Windows, abra `MWSWindows.sln` no Visual Studio.

1. Navegue até a pasta de exibições e abra a `task.js` arquivo para edição.

   * No XCode, navegue até a guia **Capture > www > wsmobile > js > tempo de execução > exibições** pasta.
   * No Eclipse, navegue até o **ativos > www > wsmobile > js > tempo de execução > exibições** pasta.
   * No Visual Studio, navegue até o **MWSWindows > www > wsmobile > js > tempo de execução > exibições** pasta.

   >[!NOTE]
   >
   >O arquivo task.js contém a exibição de backbone associada a cada tarefa ou Startpoint listado nas listas tarefa ou Startpoint.

1. No `task.js` arquivo, procure a propriedade events da visualização.

   A propriedade events é um mapa com cada entrada no formato:

   `"EventName Selector": "Function"`

   Quando você aciona um evento JavaScript chamado `EventName`em um elemento HTML especificado por `Selector`, o `Function`é chamado.

1. Localizar

   * &quot;toque em .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;toque em .taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;toque em .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;tap .last_empty_div&quot; : &quot;onTaskClick&quot;,

   e substitua por

   * &quot;swipe .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .last_empty_div&quot; : &quot;onTaskClick&quot;,

1. Salve e feche o `task.js` arquivo.
1. Crie e execute o aplicativo AEM Forms. Agora você pode abrir um usando o com o deslizamento para a esquerda e para a direita.

Da mesma forma, é possível fazer alterações em outras exibições para várias combinações de gestos, elementos HTML e funções.
