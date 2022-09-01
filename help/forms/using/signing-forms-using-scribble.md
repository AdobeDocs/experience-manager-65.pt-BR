---
title: Aplicar assinaturas eletrônicas a um formulário usando assinaturas do scribble
seo-title: Apply electronic signatures to a form using scribble signatures
description: Assinar formulários usando o scribble
seo-description: Signing forms using scribble
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
feature: Adaptive Forms
exl-id: 096f61b0-59f4-4699-9093-8fb1ed81fded
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# Aplicar assinaturas eletrônicas a um formulário usando assinaturas do scribble{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

Você pode usar o **Assinatura do Scribble** componente e **Etapa de assinatura** componente para desenhar (Scribble) assinatura em um formulário adaptável. O componente Etapa de assinatura exibe uma versão PDF do formulário adaptável. É necessário ativar uma opção Documento de registro ou formulários adaptáveis baseados em modelo de formulário para usar o componente Etapa de assinatura.

![Caixa de diálogo de sinal de rabisco](/help/forms/using/assets/scribble-signature.png)

## Várias opções disponíveis na Janela de assinatura

* **A:** Clique no botão **Pincel de tinta** ícone para desenhar sua assinatura na tela.
* **B:** Clique no botão **Limpar** ícone para limpar a assinatura na tela.
* **C:** Clique no botão **Geolocalização** ícone para adicionar a geolocalização junto com a assinatura.
* **D:** Clique no botão **Teclado** ícone para digitar seu nome na tela.

Depois de tocar em Concluído![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) na janela Scribble signature , não é possível editar a assinatura. Caso deseje editar a assinatura, desconsidere a assinatura atual e assine novamente usando a opção Pincel/teclado acima.

Toque em **Configurar** ![configure](assets/configure.png) ícone para definir a proporção da tela de assinatura do Scribble.
* Quando a proporção da tela de assinatura do Scribble for menor que 1, as informações de geolocalização serão adicionadas na parte inferior da tela de assinatura do Scribble.

* Quando a proporção da tela de assinatura do Scribble for superior a 1, as informações de geolocalização serão adicionadas ao lado direito da tela de assinatura do Scribble.

![rabisco de assinatura inferior](/help/forms/using/assets/scribble-signature-aspectratio.PNG)


>[!NOTE]
>
>As assinaturas são sempre salvas em um formato PNG.

## Configurar um formulário adaptável para usar a Assinatura do Scribble {#configure-an-adaptive-form-to-use-scribble-signature}

1. Crie uma opção Documento de registro ativada ou um formulário adaptável baseado em modelo de formulário. Para obter informações passo a passo, consulte [Criação de um formulário adaptável](../../forms/using/creating-adaptive-form.md).
1. Arraste e solte a **Assinatura do Scribble** componente do navegador de componentes para o formulário adaptável.
1. Toque no **Configurar** ![configure](assets/configure.png) ícone . Ele abre o navegador de propriedades e exibe as propriedades do componente Assinatura do rabisco. Configure as propriedades do componente Assinatura do Scribble.
1. Arraste e solte o componente Etapa de assinatura do navegador de componentes para o formulário adaptável.

   >[!NOTE]
   >
   >O componente Etapa de assinatura ocupa a largura total disponível para o formulário. É recomendável não ter nenhum outro componente na seção que contenha o componente Etapa de assinatura.

1. No navegador Conteúdo, toque em **Contêiner de formulário** e toque no **Configurar** ![](/help/forms/using/assets/configure.png) ícone . Ele abre o navegador de propriedades e exibe as propriedades do contêiner do Formulário adaptável. Navegar para **Contêiner de formulário adaptável** > **Assinatura eletrônica** e desmarque a opção **Ativar o Adobe Sign** opção. Toque em Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para salvar as alterações.

   >[!NOTE]
   >
   >Quando você adiciona um componente Etapa de assinatura a um formulário adaptável, a opção Habilitar Adobe Sign é selecionada automaticamente.

1. Toque no **Configurar** ![configure](assets/configure.png) ícone . Ele abre o navegador de propriedades e exibe as propriedades da etapa Assinatura. Configure as seguintes propriedades:

   * **Nome do elemento**: Especifique o nome do componente.

   * **Título:** Especifique o título exclusivo do componente.
   * **Mensagem do modelo:** Especifique a mensagem a ser exibida enquanto o PDF de assinatura está sendo carregado. Os serviços da Adobe Sign levam algum tempo para preparar e carregar o PDF de assinatura.
   * **Serviço de assinatura:** Selecione o **Assinatura do Scribble** opção.

   * **Classe CSS**: Especifique a classe CSS da biblioteca do cliente, se houver. Recomenda-se a utilização de [temas](../../forms/using/themes.md) e [estilos em linha](../../forms/using/inline-style-adaptive-forms.md) em vez de Classe CSS.

   Toque em Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para salvar as alterações. A Assinatura é configurada com êxito.

   Agora, ao preencher um formulário, é exibida uma versão PDF do formulário adaptável e são fornecidas opções para assinar o documento PDF. Para obter informações detalhadas, consulte [Assinar um formulário adaptável usando a Assinatura do Scribble](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Assinar um formulário adaptável usando a Assinatura do Scribble {#sign-an-adaptive-form-using-scribble-signature}

1. Depois de preencher um formulário adaptável e chegar à página Etapa de assinatura, a tela de assinatura é exibida.

   ![Caixa de diálogo de sinal de rabisco](/help/forms/using/assets/esignscribblesign.jpg)

1. Clique em **[!UICONTROL Sign]**. A caixa de diálogo de sinal de rabisco é exibida. Assine o formulário e clique em Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para salvar a assinatura.

   ![Caixa de diálogo de sinal de rabisco](/help/forms/using/assets/scribblewidget.png)

1. Clique em concluir para concluir o processo de assinatura.

   ![Concluir o processo de assinatura](/help/forms/using/assets/scribblecomplete.jpg)

As assinaturas são adicionadas ao formulário e o controle do formulário é movido para o próximo painel.
