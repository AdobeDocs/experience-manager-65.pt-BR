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

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>


| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |


Você pode usar o componente **Assinatura assinável** e o componente **Etapa de assinatura** para desenhar (Rabiscar) uma assinatura em um formulário adaptável. O componente Etapa de assinatura exibe uma versão PDF do formulário adaptável. Você precisa de uma opção Documento de registro ativada ou de formulários adaptáveis baseados em modelo de formulário para usar o componente Etapa de assinatura.

![Caixa de diálogo Assinar assinatura](/help/forms/using/assets/scribble-signature.png)

## Várias opções disponíveis na Janela de assinatura

* **A:** Clique no ícone **Pincel de Tinta** para desenhar sua assinatura na tela.
* **B:** Clique no ícone **Limpar** para limpar a assinatura na tela.
* **C:** Clique no ícone **Geolocalização** para adicionar a geolocalização junto com a assinatura.
* **D:** Clique no ícone **Teclado** para digitar seu nome na tela.

Depois de selecionar o ícone Concluído![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) na janela Assinatura Escrita, você não poderá editar a assinatura. No caso, se você quiser editar a assinatura, desconsidere a assinatura atual e assine novamente usando a opção Pincel/Teclado acima.

Você pode selecionar o ícone **Configurar** ![configurar](assets/configure.png) para definir a proporção da tela Assinatura Escrita.
* Quando a proporção da tela Assinatura Escrita for menor que 1, as informações de localização geográfica serão adicionadas na parte inferior da tela Assinatura Escrita.

* Quando a proporção da tela Assinatura Escrita for maior que 1, as informações de geolocalização serão adicionadas ao lado direito da tela Assinatura Escrita.

![rabisco de assinatura-fundo](/help/forms/using/assets/scribble-signature-aspectratio.PNG)


>[!NOTE]
>
>As assinaturas são sempre salvas em formato PNG.
>

## Configurar um formulário adaptável para usar a assinatura escritas {#configure-an-adaptive-form-to-use-scribble-signature}

1. Opção Criar um documento de registro ativada ou formulário adaptável baseado em modelo de formulário. Para obter informações passo a passo, consulte [Criação de um formulário adaptável](../../forms/using/creating-adaptive-form.md).
1. Arraste e solte o componente **Assinatura Escrita** do navegador de componentes para o formulário adaptável.
1. Selecione o ícone **Configurar** ![configurar](assets/configure.png). Ele abre as propriedades do navegador e exibe as propriedades do componente Assinatura Escrita. Configure as propriedades do componente Assinatura Escrita.
1. Arraste e solte o componente Etapa de assinatura do navegador de componentes para o formulário adaptável.

   >[!NOTE]
   >
   >O componente Etapa de assinatura ocupa toda a largura disponível para o formulário. É recomendável não ter nenhum outro componente na seção que contém o componente Etapa de assinatura.
   >

1. No Navegador de conteúdo, selecione **Contêiner de formulário** e selecione o ícone **Configurar** ![configurar](/help/forms/using/assets/configure.png). Ela abre as propriedades do navegador e exibe as propriedades do contêiner do Formulário adaptável. Navegue até **Contêiner de formulário adaptável** > **Assinatura eletrônica** e desmarque a opção **Habilitar Adobe Sign**. Selecione o ícone Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para salvar as alterações.

   >[!NOTE]
   >
   >Quando você adiciona um componente Etapa de assinatura a um formulário adaptável, a opção Habilitar Adobe Sign é selecionada automaticamente.
   >

1. Selecione o ícone **Configurar** ![configurar](assets/configure.png). Ele abre o navegador de propriedades e exibe as propriedades da etapa Assinatura. Configure as seguintes propriedades:

   * **Nome do Elemento**: especifique o nome do componente.

   * **Título:** especifique o título exclusivo do componente.
   * **Mensagem de modelo:** especifique a mensagem a ser exibida enquanto o PDF de assinatura estiver sendo carregado. Os serviços da Adobe Sign demoram algum tempo para preparar e carregar o PDF de assinatura.
   * **Serviço de assinatura:** selecione a opção **Assinatura assinável**.

   * **Classe CSS**: especifique a classe CSS da biblioteca do cliente, se houver. Use [temas](../../forms/using/themes.md) e [estilos embutidos](../../forms/using/inline-style-adaptive-forms.md) em vez da Classe CSS.

   Selecione o ícone Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para salvar as alterações. A Assinatura foi configurada com êxito.

   Agora, quando você preenche um formulário, uma versão de PDF do formulário adaptável é exibida e as opções para assinar o documento de PDF são fornecidas. Para obter informações detalhadas, consulte [Assinar um formulário adaptável usando a Assinatura Escrita](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Assinar um formulário adaptável usando a Assinatura Escrita {#sign-an-adaptive-form-using-scribble-signature}

1. Depois de preencher um formulário adaptável e chegar à página Etapa de assinatura, a tela de assinatura é exibida.

   ![Caixa de diálogo Assinar assinatura](/help/forms/using/assets/esignscribblesign.jpg)

1. Clique em **[!UICONTROL Assinar]**. A caixa de diálogo assinar é exibida. Assine o formulário e clique no ícone Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para salvar a assinatura.

   ![Caixa de diálogo Assinar assinatura](/help/forms/using/assets/scribblewidget.png)

1. Clique em Concluir para concluir o processo de assinatura.

   ![Concluir o processo de assinatura](/help/forms/using/assets/scribblecomplete.jpg)

As assinaturas são adicionadas ao formulário e o controle do formulário é movido para o próximo painel.
