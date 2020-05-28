---
title: Aplicar assinaturas eletrônicas a um formulário usando assinaturas rabiscadas
seo-title: Aplicar assinaturas eletrônicas a um formulário usando assinaturas rabiscadas
description: Assinar formulários usando script
seo-description: Assinar formulários usando script
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
translation-type: tm+mt
source-git-commit: 68ea2335a8466c3c23b766efb1a04b6a38d7f670
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---


# Aplicar assinaturas eletrônicas a um formulário usando assinaturas rabiscadas{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

Você pode usar o componente Assinatura **em** script e o componente Etapa **da** assinatura para desenhar (Script) a assinatura em um formulário adaptável. O componente Etapa de assinatura exibe uma versão PDF do formulário adaptável. Para usar o componente Etapa de assinatura, é necessário ativar uma opção Documento de registro ou formulários adaptáveis baseados em modelo de formulário.

Ambos os componentes fornecem uma janela, conforme exibido abaixo, para assinar um formulário. Você também pode clicar no ícone geolocalização ![aem_6_3_geolocation](assets/aem_6_3_geolocation.png) para adicionar geolocalização à assinatura.

![Caixa de diálogo de sinal de rabisco](assets/scribble-signature.png)

## Configurar um formulário adaptável para usar a assinatura em script {#configure-an-adaptive-form-to-use-scribble-signature}

1. Crie um Documento de opção Registro ativada ou formulário adaptável baseado em modelo de formulário. Para obter informações detalhadas, consulte [Criação de um formulário](../../forms/using/creating-adaptive-form.md)adaptável.
1. Arraste e solte o componente de Assinatura **** de script do navegador de componentes para o formulário adaptável.
1. Toque no ícone **Configurar** ![configuração](assets/configure.png) . Ele abre o navegador de propriedades e exibe as propriedades do componente Assinatura de script. Configure as propriedades do componente Assinatura do script.
1. Arraste e solte o componente Signature Step do navegador de componentes para o formulário adaptável.

   >[!NOTE]
   >
   >O componente Etapa de assinatura ocupa a largura total disponível para o formulário. É recomendável não ter nenhum outro componente na seção que contém o componente Etapa de assinatura.

1. No navegador de conteúdo, toque em Container **de** formulário e toque no ícone **Configurar** ![](/help/forms/using/assets/configure.png) . Ele abre o navegador de propriedades e exibe as propriedades do container de formulário adaptável. Navegue até Container **de formulário** adaptável > Assinatura **** eletrônica e desmarque a opção **Ativar o Adobe Sign** . Toque no ícone ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) concluído para salvar as alterações.

   >[!NOTE]
   >
   >Quando você adiciona um componente Etapa de assinatura a um formulário adaptável, a opção Habilitar Adobe Sign é selecionada automaticamente.

1. Toque no ícone **Configurar** ![configuração](assets/configure.png) . Ele abre o navegador de propriedades e exibe as propriedades da etapa de assinatura. Configure as seguintes propriedades:

   * **Nome** do elemento: Especifique o nome do componente.

   * **Título:** Especifique um título exclusivo do componente.
   * **Mensagem do modelo:** Especifique a mensagem a ser exibida enquanto o PDF de assinatura estiver sendo carregado. Os serviços Adobe Sign levam algum tempo para preparar e carregar um PDF de assinatura.
   * **Serviço de assinatura:** Selecione a opção **Assinaturas** com script.

   * **Classe** CSS: Especifique a classe CSS da biblioteca do cliente, se houver. É recomendável usar [temas](../../forms/using/themes.md) e estilos [](../../forms/using/inline-style-adaptive-forms.md) em linha, em vez da Classe CSS.
   Toque no ícone ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) concluído para salvar as alterações. A Assinatura foi configurada com êxito.

   Agora, ao preencher um formulário, uma versão PDF do formulário adaptável é exibida e as opções para assinar o documento PDF são fornecidas. Para obter informações detalhadas, consulte [Assinar um formulário adaptável usando Assinatura](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature)em forma de script.

## Assinar um formulário adaptável usando a Assinatura de script {#sign-an-adaptive-form-using-scribble-signature}

1. Depois que você preencher um formulário adaptável e chegar à página Etapa de assinatura, a tela de assinatura será exibida.

   ![Tela de assinatura para a página do EchoSign](assets/esignscribblesign.jpg)

1. Clique em **[!UICONTROL Assinar]**. A caixa de diálogo do sinal de script é exibida. Assine o formulário e clique no ícone ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) concluído para salvar a assinatura.

   ![Caixa de diálogo de sinal de rabisco](assets/scribblewidget.jpg)

1. Clique em Concluir para concluir o processo de assinatura.

   ![Concluir o processo de assinatura](assets/scribblecomplete.jpg)

As assinaturas são adicionadas ao formulário e o controle do formulário é movido para o próximo painel.

