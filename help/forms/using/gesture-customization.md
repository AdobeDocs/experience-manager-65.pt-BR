---
title: Personalização de gesto
description: Saiba como personalizar os gestos no aplicativo AEM Forms. É possível personalizar os gestos para fornecer um método distinto de interação com o aplicativo.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Personalização de gesto {#gesture-customization}

É possível personalizar os gestos do aplicativo AEM Forms para fornecer um método distinto de interação com o aplicativo. Por exemplo, é possível adicionar novos gestos para abrir ou fechar uma tarefa ou um ponto inicial.

## Para personalizar gestos no aplicativo AEM Forms {#to-customize-gestures-in-aem-forms-app}

No aplicativo AEM Forms, o deslizamento para a esquerda abre uma nova tarefa ou um ponto inicial, enquanto o deslizamento para a direita não faz nada. O exemplo a seguir fornece etapas para abrir uma nova tarefa ou ponto de partida ao executar os gestos de deslizar com o botão direito do mouse no aplicativo AEM Forms.

1. Abra o projeto.

   * Para o iOS, abra `Capture.xcodeproj` no Xcode
   * Para o Android, abra o projeto Android no Eclipse.
   * Para Windows, abra `MWSWindows.sln` no Visual Studio.

1. Navegue até a pasta de exibições e abra o arquivo `task.js` para edição.

   * No Xcode, navegue até a pasta **Capture > www > wsmobile > js > runtime > views**.
   * No Eclipse, navegue até a pasta **assets > www > wsmobile > js > runtime > views**.
   * No Visual Studio, navegue até a pasta **MWSWindows > www > wsmobile > js > runtime > views**.

   >[!NOTE]
   >
   >O arquivo task.js contém a exibição de backbone associada a cada tarefa ou Startpoint listado nas listas tarefa ou Startpoint.

1. No arquivo `task.js`, pesquise a propriedade events da exibição.

   A propriedade events é um mapa com cada entrada no formato:

   `"EventName Selector": "Function"`

   Quando você aciona um evento JavaScript chamado `EventName` em um elemento HTML especificado por `Selector`, `Function` é chamado.

1. Localizar

   * &quot;select .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;select .taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;select .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;select .last_empty_div&quot; : &quot;onTaskClick&quot;,

   e substitua por

   * &quot;swipe .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .last_empty_div&quot; : &quot;onTaskClick&quot;,

1. Salvar e fechar o arquivo `task.js`.
1. Crie e execute o aplicativo AEM Forms. Agora você pode abrir um usando o com o deslizamento para a esquerda e para a direita.

Da mesma forma, é possível fazer alterações em outras exibições para várias combinações de gestos, elementos HTML e funções.
