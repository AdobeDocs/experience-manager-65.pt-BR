---
title: Salvar automaticamente um formulário adaptável
description: Você pode configurar um formulário adaptável para começar a salvar automaticamente o conteúdo com base em um evento ou um intervalo de tempo predefinido
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms,Foundation Components
exl-id: ff9bf466-228d-40e6-9389-15c1f2ed1d2e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Salvar automaticamente um formulário adaptável {#auto-save-an-adaptive-form}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

Você pode configurar um formulário adaptável para começar a salvar automaticamente o conteúdo com base em um evento ou um intervalo de tempo predefinido. Por padrão, o conteúdo de um formulário adaptável é salvo em uma ação do usuário, como ao pressionar o botão Salvar. A opção de salvamento automático é útil em:

* Salvando automaticamente o conteúdo para usuários anônimos e conectados
* Salvamento do conteúdo de um formulário sem a mínima intervenção do usuário
* Começar a salvar o conteúdo de um formulário com base em um evento do usuário
* Salvamento repetido do conteúdo de um formulário após um intervalo de tempo especificado

## Ativar salvamento automático para um formulário adaptável {#enable-autosave-for-an-adaptive-form}

Para um formulário adaptável, a opção de salvamento automático não é ativada imediatamente. Você pode ativar a opção de salvamento automático na **Salvamento automático** nas propriedades de um formulário adaptável. A variável **Salvamento automático** também fornece várias outras opções de configuração. Execute as seguintes etapas para ativar e configurar a opção de salvamento automático para um formulário adaptável:

1. Para acessar a seção de salvamento automático nas propriedades, selecione um componente e ![nível de campo](assets/field-level.png) > **[!UICONTROL Contêiner de formulário adaptável]** e selecione ![cmppr](assets/cmppr.png).
1. No **[!UICONTROL Salvamento automático]** seção, **[!UICONTROL Ativar]** a opção salvar automaticamente.
1. No **[!UICONTROL Evento de formulário adaptável]** especifique 1 ou TRUE para começar a salvar o formulário automaticamente quando o formulário for carregado no navegador. Você também pode especificar uma expressão condicional para um evento, que, quando acionado e retornar true, inicia o salvamento do conteúdo do formulário.
1. Especifique o Acionador. O salvamento automático é acionado com base na sua configuração. As opções são:

   * **[!UICONTROL Baseado em tempo:]** Selecione a opção para começar a salvar o conteúdo com base em um intervalo de tempo específico.
   * **[!UICONTROL Baseado em evento:]** Selecione a opção para começar a salvar o conteúdo com base em quando um evento é acionado.

   Ao selecionar um acionador, a caixa Configuração de estratégia é ativada. A caixa de configuração de estratégia permite:

   * Especifique um intervalo de tempo se você selecionar **[!UICONTROL Baseado em tempo]** acionador.
   * Especifique um nome de evento se você selecionar **[!UICONTROL Baseado em evento]** acionador.

   Você também pode criar e adicionar sua própria estratégia personalizada à lista. Para obter detalhes, consulte [Implementar uma estratégia personalizada para salvar automaticamente os formulários](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. (Somente salvamento automático baseado em tempo) Execute as seguintes etapas para configurar opções para o salvamento automático baseado em tempo.

   1. No **[!UICONTROL Salvamento automático neste intervalo]** especifique o intervalo em segundos. O formulário é salvo repetidamente depois que o número de segundos especificado na caixa intervalo decorrer.

1. (Somente salvamento automático baseado em evento) Execute as seguintes etapas para configurar opções para o salvamento automático baseado em evento.

   1. Na **Salvamento automático após o evento** , especifique um [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) evento. O formulário é salvo sempre que a expressão é avaliada como TRUE.

1. (Opcional) Para salvar automaticamente o conteúdo para usuários anônimos, selecione a **Ativar salvamento automático para usuários anônimos** e clique em **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Para que a opção de salvamento automático funcione para usuários anônimos, certifique-se de configurar o Serviço de configuração comum da Forms para permitir que todos os usuários visualizem, verifiquem e assinem formulários.
   >
   >Para configurar o serviço, vá para a configuração do Console da Web do AEM em `https://server:port/system/console/configMgr` e edite o **[!UICONTROL Serviço de configuração comum do Forms]** para escolher o **[!UICONTROL Todos os usuários]** opção no **[!UICONTROL Permitir]** e salve a configuração.

## Implementar uma estratégia personalizada para ativar o salvamento automático para formulários adaptáveis {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

Você pode implementar um evento personalizado para acionar a funcionalidade de salvamento automático. Execute as seguintes etapas para criar e implementar o evento personalizado:

1. Criar pastas de bibliotecas de clientes e bibliotecas de clientes. Para obter etapas detalhadas, consulte [Usar documento de bibliotecas do lado do cliente](/help/sites-developing/clientlibs.md).

   Por exemplo, o script a seguir usa o script personalizado `emailFocusChange`para acionar a funcionalidade de salvamento automático:

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
   >Uma propriedade de categoria é definida ao criar as pastas da biblioteca do cliente. Mantenha útil o valor atribuído à propriedade de categoria.

1. Abra o formulário adaptável no modo de autor.

1. No modo de edição, selecione um componente e selecione ![nível de campo](assets/field-level.png) > **[!UICONTROL Contêiner de formulário adaptável]** e selecione ![cmppr](assets/cmppr.png).
1. Nas propriedades, abra **[!UICONTROL Básico]** seção. No **[!UICONTROL Categoria da biblioteca cliente]** , digite o valor da propriedade category definida ao criar as pastas da biblioteca do cliente.
1. Abra a seção Salvamento automático. No **[!UICONTROL Salvamento automático após o evento]** especifique um evento personalizado já definido na biblioteca do cliente. Clique em **[!UICONTROL OK]**.
