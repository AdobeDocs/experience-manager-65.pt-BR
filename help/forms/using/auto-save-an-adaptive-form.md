---
title: Salvar automaticamente um formulário adaptável
seo-title: Auto-save an adaptive form
description: Você pode configurar um formulário adaptável para começar a salvar automaticamente o conteúdo com base em um evento ou em um intervalo de tempo predefinido
seo-description: You can configure an adaptive form to automatically start saving the content based on an event or a pre-defined time-interval
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
feature: Adaptive Forms
exl-id: 948b2c12-895d-49e3-a943-d8fe87174fc4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Salvar automaticamente um formulário adaptável {#auto-save-an-adaptive-form}

Você pode configurar um formulário adaptável para começar a salvar automaticamente o conteúdo com base em um evento ou em um intervalo de tempo predefinido. Por padrão, o conteúdo de um formulário adaptável é salvo em uma ação do usuário, como ao pressionar o botão Salvar. A opção de salvar automaticamente é útil em:

* Salvar automaticamente o conteúdo para usuários anônimos e conectados
* Salvar o conteúdo de um formulário sem a intervenção mínima do usuário
* Comece a salvar o conteúdo de um formulário com base em um evento de usuário
* Salvar o conteúdo de um formulário repetidamente após um intervalo de tempo especificado

## Ativar o salvamento automático para um formulário adaptável {#enable-autosave-for-an-adaptive-form}

Para um formulário adaptável, a opção de salvamento automático não é ativada imediatamente. Você pode ativar a opção de salvamento automático na **Salvar automaticamente** nas propriedades de um formulário adaptável. O **Salvar automaticamente** seção também fornece várias outras opções de configuração. Execute as seguintes etapas para habilitar e configurar a opção de salvamento automático para um formulário adaptável:

1. Para acessar a seção de salvamento automático nas propriedades, selecione um componente e toque em ![nível de campo](assets/field-level.png) > **[!UICONTROL Contêiner de formulário adaptável]** e toque em ![cmppr](assets/cmppr.png).
1. No **[!UICONTROL Salvar automaticamente]** seção, **[!UICONTROL Habilitar]** a opção salvar automaticamente.
1. No **[!UICONTROL Evento de formulário adaptável]** , especifique 1 ou TRUE para iniciar automaticamente o salvamento do formulário quando o formulário for carregado no navegador. Também é possível especificar uma expressão condicional para um evento, que, quando acionada e retorna true, começa a salvar o conteúdo do formulário.
1. Especifique o Acionador. O salvamento automático é acionado com base em sua configuração. As opções são:

   * **[!UICONTROL Baseado em tempo:]** Selecione a opção para começar a salvar o conteúdo com base em um intervalo de tempo específico.
   * **[!UICONTROL Baseado em evento:]** Selecione a opção para começar a salvar o conteúdo com base em quando um evento for acionado.

   Quando você seleciona um acionador, a caixa Configuração de estratégia é ativada. A caixa Configuração de estratégia permite:

   * Especifique um intervalo de tempo se você selecionar **[!UICONTROL Baseado em tempo]** acionador.
   * Especifique um nome de evento se você selecionar **[!UICONTROL Baseado em evento]** acionador.

   Você também pode criar e adicionar sua própria estratégia personalizada à lista. Para obter detalhes, consulte [Implementar uma estratégia personalizada para salvar os formulários automaticamente](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. (Somente salvamento automático com base em tempo) Execute as seguintes etapas para configurar opções para o salvamento automático com base em tempo.

   1. No **[!UICONTROL Salvar automaticamente neste intervalo]** , especifique o intervalo em segundos. O formulário é salvo repetidamente após o número de segundos especificado na caixa de intervalo expirar.

1. (Somente para salvar automaticamente com base em eventos) Execute as etapas a seguir para configurar opções de Salvar automaticamente com base em eventos.

   1. Em **Salvar automaticamente após esse evento** , especifique um [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) evento. O formulário é salvo sempre que a expressão é avaliada como TRUE.

1. (Opcional) Para salvar automaticamente o conteúdo para usuários anônimos, selecione a variável **Habilitar salvamento automático para usuários anônimos** e clique em **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Para que a opção de salvamento automático funcione para usuários anônimos, certifique-se de configurar o Serviço de Configuração Comum da Forms para permitir que todos os usuários visualizem, verifiquem e assinem formulários.
   >
   >Para configurar o serviço, vá para AEM configuração do Console da Web em `https://server:port/system/console/configMgr` e edite o **[!UICONTROL Serviço de configuração comum do Forms]** para escolher a **[!UICONTROL Todos os usuários]** na **[!UICONTROL Permitir]** e salve a configuração.

## Implementar uma estratégia personalizada para permitir o salvamento automático para formulários adaptáveis {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

Você pode implementar um evento personalizado para acionar a funcionalidade de salvamento automático. Execute as seguintes etapas para criar e implementar o evento personalizado:

1. Crie bibliotecas de clientes e pastas de bibliotecas de clientes. Para obter etapas detalhadas, consulte o [Usar documento de bibliotecas do lado do cliente](/help/sites-developing/clientlibs.md).

   Por exemplo, o script a seguir usa o `emailFocusChange`para acionar a funcionalidade de salvamento automático:

   ```javascript
   window.addEventListener("bridgeInitializeStart", function (){
       guideBridge.connect(function () { guideBridge.on("elementFocusChanged", function (event,data) {
           if(data.target.name === 'Email') {
               guideBridge.trigger("emailFocusChange");
           }
       });
      });
   });
   ```

   >[!NOTE]
   >
   >Uma propriedade category é definida ao criar as pastas da biblioteca do cliente. Mantenha o valor atribuído à propriedade category à disposição.

1. Abra o formulário adaptável no modo de autor.

1. No modo de edição, selecione um componente e toque em ![nível de campo](assets/field-level.png) > **[!UICONTROL Contêiner de formulário adaptável]** e toque em ![cmppr](assets/cmppr.png).
1. Nas propriedades, abra o **[!UICONTROL Básico]** seção. No **[!UICONTROL Categoria da biblioteca do cliente]** digite o valor da propriedade category definida ao criar as pastas da biblioteca do cliente.
1. Abra a seção Salvar automaticamente . No **[!UICONTROL Salvar automaticamente após esse evento]** , especifique um evento personalizado já definido na biblioteca do cliente. Clique em **[!UICONTROL OK]**.
