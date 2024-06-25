---
title: Aplicar assinaturas eletrônicas a um formulário usando assinaturas escritas
description: Saiba como assinar o AEM Adaptive Forms usando a assinatura de rabisco. Você pode usar a etapa de assinatura à mão para desenhar a assinatura em um formulário.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 096f61b0-59f4-4699-9093-8fb1ed81fded
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---

# Aplicar assinaturas eletrônicas a um formulário usando assinaturas escritas{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>


| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble.html) |
| AEM 6.5 | Este artigo |


Você pode usar o **Rabiscar a assinatura** componente e **Etapa de assinatura** componente para desenhar (Rabiscar) assinatura em um formulário adaptável. O componente Etapa de assinatura exibe uma versão PDF do formulário adaptável. Você precisa de uma opção Documento de registro ativada ou de formulários adaptáveis baseados em modelo de formulário para usar o componente Etapa de assinatura.

![Caixa de diálogo Scribble sign](/help/forms/using/assets/scribble-signature.png)

## Várias opções disponíveis na Janela de assinatura

* **R:** Clique em **Pincel de pintura** ícone para desenhar sua assinatura na tela.
* **B:** Clique em **Limpar** ícone para limpar a assinatura na tela.
* **C:** Clique em **Localização geográfica** ícone para adicionar a localização geográfica junto com a assinatura.
* **D:** Clique em **Teclado** ícone para digitar seu nome na tela.

Depois de selecionar Concluído![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) ícone na janela Assinatura, não é possível editar a assinatura. No caso, se você quiser editar a assinatura, desconsidere a assinatura atual e assine novamente usando a opção Pincel/Teclado acima.

É possível selecionar a variável **Configurar** ![configurar](assets/configure.png) ícone para definir a proporção da tela Assinatura Escrita.
* Quando a proporção da tela Assinatura Escrita for menor que 1, as informações de localização geográfica serão adicionadas na parte inferior da tela Assinatura Escrita.

* Quando a proporção da tela Assinatura Escrita for maior que 1, as informações de geolocalização serão adicionadas ao lado direito da tela Assinatura Escrita.

![rabisco inferior de assinatura](/help/forms/using/assets/scribble-signature-aspectratio.PNG)


>[!NOTE]
>
>As assinaturas são sempre salvas em formato PNG.
>

## Configurar um formulário adaptável para usar a assinatura escritas {#configure-an-adaptive-form-to-use-scribble-signature}

1. Opção Criar um documento de registro ativada ou formulário adaptável baseado em modelo de formulário. Para obter informações passo a passo, consulte [Criação de um formulário adaptável](../../forms/using/creating-adaptive-form.md).
1. Arraste e solte a variável **Rabiscar a assinatura** componente do navegador de componentes ao formulário adaptável.
1. Selecione o **Configurar** ![configurar](assets/configure.png) ícone. Ele abre as propriedades do navegador e exibe as propriedades do componente Assinatura Escrita. Configure as propriedades do componente Assinatura Escrita.
1. Arraste e solte o componente Etapa de assinatura do navegador de componentes para o formulário adaptável.

   >[!NOTE]
   >
   >O componente Etapa de assinatura ocupa toda a largura disponível para o formulário. É recomendável não ter nenhum outro componente na seção que contém o componente Etapa de assinatura.
   >

1. No Navegador de conteúdo, selecione **Contêiner de formulário** e selecione a variável **Configurar** ![configurar](/help/forms/using/assets/configure.png) ícone. Ela abre as propriedades do navegador e exibe as propriedades do contêiner do Formulário adaptável. Navegue até **Contêiner de formulário adaptável** > **Assinatura eletrônica** e desmarque a opção **Ativar o Adobe Sign** opção. Selecione o Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) ícone para salvar as alterações.

   >[!NOTE]
   >
   >Quando você adiciona um componente Etapa de assinatura a um formulário adaptável, a opção Habilitar Adobe Sign é selecionada automaticamente.
   >

1. Selecione o **Configurar** ![configurar](assets/configure.png) ícone. Ele abre o navegador de propriedades e exibe as propriedades da etapa Assinatura. Configure as seguintes propriedades:

   * **Nome do elemento**: especifique o nome do componente.

   * **Título:** Especifique o título exclusivo do componente.
   * **Mensagem do modelo:** Especifique a mensagem a ser exibida enquanto o PDF de assinatura estiver sendo carregado. Os serviços da Adobe Sign demoram algum tempo para preparar e carregar o PDF de assinatura.
   * **Serviço de assinatura:** Selecione o **Rabiscar a assinatura** opção.

   * **Classe CSS**: especifique a classe CSS da biblioteca do cliente, se houver. Uso [temas](../../forms/using/themes.md) e [estilos em linha](../../forms/using/inline-style-adaptive-forms.md) em vez da classe CSS.

   Selecione o Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) ícone para salvar as alterações. A Assinatura foi configurada com êxito.

   Agora, quando você preenche um formulário, uma versão de PDF do formulário adaptável é exibida e as opções para assinar o documento de PDF são fornecidas. Para obter informações detalhadas, consulte [Assinar um formulário adaptável usando a Assinatura Escrita](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Assinar um formulário adaptável usando a Assinatura Escrita {#sign-an-adaptive-form-using-scribble-signature}

1. Depois de preencher um formulário adaptável e chegar à página Etapa de assinatura, a tela de assinatura é exibida.

   ![Caixa de diálogo Scribble sign](/help/forms/using/assets/esignscribblesign.jpg)

1. Clique em **[!UICONTROL Sign]**. A caixa de diálogo assinar é exibida. Assine o formulário e clique no link Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) ícone para salvar a assinatura.

   ![Caixa de diálogo Scribble sign](/help/forms/using/assets/scribblewidget.png)

1. Clique em Concluir para concluir o processo de assinatura.

   ![Concluir o processo de assinatura](/help/forms/using/assets/scribblecomplete.jpg)

As assinaturas são adicionadas ao formulário e o controle do formulário é movido para o próximo painel.
