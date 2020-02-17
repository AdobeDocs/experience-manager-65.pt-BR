---
title: Personalização do gesto
seo-title: Personalização do gesto
description: Personalizar os gestos no aplicativo AEM Forms
seo-description: Personalizar os gestos no aplicativo AEM Forms
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personalização do gesto {#gesture-customization}

Você pode personalizar os gestos do aplicativo AEM Forms para fornecer um método distinto de interação com o aplicativo. Por exemplo, você pode adicionar novos gestos para abrir ou fechar uma tarefa ou ponto de partida.

## Como personalizar gestos no aplicativo AEM Forms {#to-customize-gestures-in-aem-forms-app}

No aplicativo AEM Forms, o deslize para a esquerda abre uma nova tarefa ou ponto de partida enquanto o deslize para a direita não faz nada. O exemplo a seguir fornece etapas para abrir uma nova tarefa ou ponto de partida na execução de gestos de deslizamento direito no aplicativo AEM Forms.

1. Abra seu projeto.

   * Para iOS, abra `Capture.xcodeproj` no Xcode
   * Para Android, abra o projeto do Android no Eclipse.
   * Para Windows, abra `MWSWindows.sln` no Visual Studio.

1. Navegue até a pasta de exibições e abra o `task.js` arquivo para edição.

   * No Xcode, navegue até a pasta **Capture > www > wsmobile > js > runtime > views** .
   * No Eclipse, navegue até a pasta **assets > www > wsmobile > js > tempo de execução > exibições** .
   * No Visual Studio, navegue até a pasta **MWSWwindows > www > wsmobile > js > tempo de execução > exibições** .
   >[!NOTE]
   >
   >O arquivo task.js contém a exibição de backbone associada a cada tarefa ou ponto de partida listado nas listas de tarefas ou pontos de partida.

1. No `task.js` arquivo, procure a propriedade events da exibição.

   A propriedade events é um mapa com cada entrada no formato:

   `"EventName Selector": "Function"`

   Quando você aciona um evento Javascript nomeado `EventName`em um elemento HTML especificado por `Selector`, o `Function`é chamado.

1. Localizar

   * &quot;toque em .taskContentArea&quot; : &quot;onTaskClick&quot;,

      &quot;tocar em .taskOpenArea&quot;: &quot;onTaskClick&quot;,

      &quot;toque em .task-content&quot; : &quot;onTaskClick&quot;,

      &quot;toque em .last_empty_div&quot; : &quot;onTaskClick&quot;,
   e substitua por

   * &quot;deslize .taskContentArea&quot; : &quot;onTaskClick&quot;,

      &quot;deslize .taskOpenArea&quot;: &quot;onTaskClick&quot;,

      &quot;arraste com o dedo .task-content&quot;: &quot;onTaskClick&quot;,

      &quot;deslize .last_empty_div&quot; : &quot;onTaskClick&quot;,


1. Salve e feche o `task.js` arquivo.
1. Crie e execute o aplicativo AEM Forms. Agora você pode abrir um usando com o dedo esquerdo e o dedo direito.

Da mesma forma, é possível fazer alterações em outras exibições para várias combinações de gestos, elementos HTML e funções.

**[Contate o suporte](https://www.adobe.com/account/sign-in.supportportal.html)**
