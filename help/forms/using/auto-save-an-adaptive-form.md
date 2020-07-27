---
title: Salvar automaticamente um formulário adaptável
seo-title: Salvar automaticamente um formulário adaptável
description: Você pode configurar um formulário adaptável para salvar automaticamente o conteúdo do start com base em um evento ou em um intervalo de tempo predefinido
seo-description: Você pode configurar um formulário adaptável para salvar automaticamente o conteúdo do start com base em um evento ou em um intervalo de tempo predefinido
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---


# Salvar automaticamente um formulário adaptável {#auto-save-an-adaptive-form}

Você pode configurar um formulário adaptável para salvar automaticamente o conteúdo do start com base em um evento ou em um intervalo de tempo predefinido. Por padrão, o conteúdo de um formulário adaptável é salvo em uma ação do usuário, como ao pressionar o botão Salvar. A opção de salvar automaticamente é útil em:

* Salvar automaticamente o conteúdo para usuários anônimos e conectados
* Salvar o conteúdo de um formulário sem a intervenção ou o mínimo possível do usuário
* Start que salva o conteúdo de um formulário com base em um evento do usuário
* Salvar o conteúdo de um formulário repetidamente após um intervalo de tempo especificado

## Ativar o salvamento automático para um formulário adaptável {#enable-autosave-for-an-adaptive-form}

Para um formulário adaptável, a opção de salvar automaticamente não está ativada na caixa. É possível ativar a opção de salvar automaticamente na seção Salvar **** automaticamente nas propriedades de um formulário adaptável. A seção Salvar **** automaticamente também fornece várias outras opções de configuração. Execute as seguintes etapas para ativar e configurar a opção de salvar automaticamente para um formulário adaptável:

1. Para acessar a seção de salvamento automático nas propriedades, selecione um componente, em seguida, toque em ![campo-level](assets/field-level.png) > **[!UICONTROL Adaptive Form Container]** e, em seguida, toque em ![cmppr](assets/cmppr.png).
1. Na seção Salvar **** automaticamente, **[!UICONTROL ative]** a opção de salvar automaticamente.
1. Na caixa Evento **[!UICONTROL de formulário]** adaptável, especifique 1 ou VERDADEIRO para que o start automaticamente salve o formulário quando ele for carregado no navegador. Também é possível especificar uma expressão condicional para um evento, que, quando acionado e retorna true, salva start no conteúdo do formulário.
1. Especifique o Acionador. O salvamento automático é acionado com base na sua configuração. Suas opções são:

   * **[!UICONTROL Baseado em tempo:]** Selecione a opção para salvar o conteúdo em start com base em um intervalo de tempo específico.
   * **[!UICONTROL Baseado em Eventos:]** Selecione a opção para salvar o conteúdo com base no start quando um evento for acionado.

   Quando você seleciona um acionador, a caixa Configuração de estratégia é ativada. A caixa Configuração de estratégia permite:

   * Especifique um intervalo de tempo se você selecionar acionador baseado **[!UICONTROL em]** tempo.
   * Especifique um nome de evento se você selecionar acionador baseado **[!UICONTROL em]** Eventos.

   Você também pode criar e adicionar sua própria estratégia personalizada à lista. Para obter detalhes, consulte [Implementar uma estratégia personalizada para salvar automaticamente os formulários](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. (Somente salvamento automático com base em tempo) Execute as seguintes etapas para configurar opções para o salvamento automático com base em tempo.

   1. Na caixa Salvar **[!UICONTROL automaticamente nesse intervalo]** , especifique o intervalo de tempo em segundos. O formulário é salvo repetidamente depois que o número de segundos especificado na caixa de intervalo decorre.

1. (Somente para salvar automaticamente com base em Eventos) Execute as seguintes etapas para configurar opções para o salvamento automático com base em Eventos.

   1. Na caixa Salvar **automaticamente após esse evento** , especifique um evento [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) . O formulário é salvo sempre que a expressão é avaliada como VERDADEIRO.

1. (Opcional) Para salvar automaticamente o conteúdo para usuários anônimos, selecione a opção **Ativar salvamento automático para usuários** anônimos e clique em **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Para que a opção de salvamento automático funcione para usuários anônimos, certifique-se de configurar o Serviço de configuração comum do Forms para permitir que todos os usuários possam pré-visualização, verificar e assinar formulários.
   >
   >Para configurar o serviço, vá até Configuração do console da Web do AEM em `https://server:port/system/console/configMgr` e edite o serviço **[!UICONTROL de configuração comum do]** Forms para escolher a opção **[!UICONTROL Todos os usuários]** no campo **[!UICONTROL Permitir]** e salve a configuração.

## Implementar uma estratégia personalizada para habilitar o salvamento automático para formulários adaptáveis {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

Você pode implementar um evento personalizado para acionar a funcionalidade de gravação automática. Execute as seguintes etapas para criar e implementar o evento personalizado:

1. Criar pastas da biblioteca de clientes e da biblioteca de clientes. Para obter etapas detalhadas, consulte o documento [Usando bibliotecas do lado do cliente](/help/sites-developing/clientlibs.md).

   Por exemplo, o script a seguir usa o `emailFocusChange`evento personalizado para acionar a funcionalidade de salvamento automático:

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
   >Uma propriedade de categoria é definida ao criar as pastas da biblioteca do cliente. Mantenha o valor atribuído à propriedade de categoria acessível.

1. Abra o formulário adaptável no modo de autor.

1. No modo de edição, selecione um componente, em seguida, toque em nível ![de](assets/field-level.png) campo > Container **[!UICONTROL de formulário]** adaptável e, em seguida, toque em ![cmppr](assets/cmppr.png).
1. Nas propriedades, abra a seção **[!UICONTROL Básico]** . Na caixa Categoria **[!UICONTROL Biblioteca do]** cliente, digite o valor da propriedade categoria definida ao criar as pastas da biblioteca do cliente.
1. Abra a seção Salvamento automático. Na caixa Salvar **[!UICONTROL automaticamente após esse evento]** , especifique um evento personalizado já definido na biblioteca do cliente. Clique em **[!UICONTROL OK]**.

