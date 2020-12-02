---
title: '"Tutorial: Publicar seu formulário adaptativo"'
seo-title: '"Tutorial: Publicar seu formulário adaptativo"'
description: Publique o formulário adaptável como uma página AEM, incorpore-o a uma página do AEM Sites ou incorpore-o a uma página da Web externa
seo-description: Publique o formulário adaptável como uma página AEM, incorpore-o a uma página do AEM Sites ou incorpore-o a uma página da Web externa
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
translation-type: tm+mt
source-git-commit: 1a816672b3e97346f5a7a984fcb4dc0df1a5b0da
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 1%

---


# Tutorial: Publicar o formulário adaptativo {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

Este tutorial é uma etapa da série [Criar seu primeiro formulário adaptável](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso do tutorial completo.

Depois que o formulário adaptável estiver pronto, você poderá publicá-lo para disponibilizá-lo aos usuários finais. Os usuários finais podem abrir o formulário publicado em qualquer dispositivo e navegador da Internet. Quando um formulário adaptável é publicado, o formulário e o conteúdo relacionado são copiados de uma instância do autor AEM para uma instância AEM. O formulário é disponibilizado ao usuário final por meio da instância de publicação.

Você tem os seguintes métodos para publicar um formulário adaptável:

* [Publicar o formulário adaptativo como uma página AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incorporar o formulário adaptável em uma página do AEM Sites](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incorporar o formulário adaptativo em uma página da Web externa (uma página da Web não AEM hospedada fora do AEM)](../../forms/using/publish-your-adaptive-form.md)

## Antes de você iniciar {#before-you-start}

* **[Configure uma instância](https://helpx.adobe.com/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)** de publicação do AEM Forms: A instância de publicação é uma instância pública voltada para AEM  [!DNL Forms] executada no modo de publicação. Em um ambiente de produção, a instância de publicação está fora do firewall da organização.
* **[Configurar replicação e replicação](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)** reversa: A replicação copia o conteúdo da instância do autor para uma instância de publicação e retorna a entrada do usuário (por exemplo, entrada de formulário) da instância de publicação para a instância do autor.

## Publicar o formulário adaptativo como uma Página AEM {#publish-the-adaptive-form-as-an-aem-page}

Quando o formulário adaptativo é publicado como uma Página AEM, a página da Web inteira contém apenas o formulário publicado. Você pode usar o URL do formulário adaptável para vinculá-lo a partir de outra página da Web. Para publicar o formulário adaptativo **Shipping-address-add-update-form** como uma Página AEM:

1. Efetue login na instância do autor AEM [!DNL Forms] e localize o formulário adaptável Shipping-address-add-update-form na interface do usuário AEM [!DNL Forms].
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Selecione o formulário adaptável de entrega-address-add-update-form e toque em **[!UICONTROL Publicar]**. Uma caixa de diálogo contendo ativos relacionados ao formulário adaptativo é exibida. Toque em **[!UICONTROL Publicar]**. O formulário adaptável é publicado e uma caixa de diálogo de sucesso é exibida.
1. Abra o formulário na instância de publicação. O formulário está disponível para preenchimento e envio pelo usuário final.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incorporar o formulário adaptável em uma página do AEM Sites {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] permite que desenvolvedores de formulários incorporem formulários adaptativos sem problemas em uma página AEM [!DNL Sites]. O formulário adaptativo incorporado está totalmente funcional e os usuários podem preencher e enviar o formulário sem sair da página. Ajuda o usuário a permanecer no contexto de outros elementos na página da Web e a interagir simultaneamente com o formulário.

AEM [!DNL Forms] fornece um componente, AEM [!DNL Forms] Container, para incorporar um formulário adaptável a uma página AEM [!DNL Sites]. Por padrão, o componente não está visível no container AEM [!DNL Sites]. Execute as seguintes etapas para habilitar o componente de Container AEM [!DNL Forms] e incorporar o formulário adaptável em uma página AEM [!DNL Sites]:

1. Crie e abra uma página no site We.Retail para edição. Por exemplo, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). O formulário adaptável é incorporado à página [!DNL Sites].

   Você também pode incorporar o formulário adaptativo em uma página We.Retail [!DNL Site's] existente. Por exemplo, a página ABOUT US [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Ele economiza tempo para criar uma página. As etapas abaixo usam a página recém-criada.

   O site We.Retail é enviado com AEM. Se você não tiver o site We.Retail instalado, consulte [Implementação de referência We.Retail](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) instalar o site.

1. Toque em ![propriedades](assets/properties.png) nas informações da página e selecione a opção **[!UICONTROL Editar modelo]** na página do site We.Retail recém-criada. O modelo da página é aberto em uma nova guia do navegador.
1. Toque na caixa **[!UICONTROL container de layout]** e toque em ![gerenciamento de recursos](assets/feedmanagement.png). Na guia **[!UICONTROL Componentes permitidos]**, expanda o acordeão **[!UICONTROL Geral]**, selecione a opção **[!UICONTROL AEM Formulário]** e toque em ![save_icon](assets/save_icon.svg). O componente de Container AEM [!DNL Forms] está ativado para a página.

1. Abra a guia do navegador que contém AEM página [!DNL Sites] aberta na etapa 1. Toque na caixa **[!UICONTROL Arraste os componentes aqui]** e toque em **+.** Na  **[!UICONTROL caixa Inserir novo]** componente, toque em  **[!UICONTROL AEM formulário]**. O componente **[!UICONTROL Container AEM Forms]** é adicionado à página.
1. Toque no componente **[!UICONTROL container AEM Forms]** e toque em ![configure-icon](assets/configure-icon.svg). Uma caixa de diálogo com propriedades de AEM [!DNL Forms] Container é exibida. No campo **[!UICONTROL Caminho do ativo]**, procure e selecione o formulário adaptável de formulário de endereço de entrega-add-update-form. Toque em ![save_icon](assets/save_icon.svg). O formulário adaptável é incorporado na página.
1. Publique o formulário adaptável e as páginas [!DNL Sites]. Estes são alguns pontos que devem ser levados em consideração:

   * Se você publicar a página AEM [!DNL Sites] pela primeira vez e ela incluir um formulário incorporado, publique a página [!DNL Sites] e o formulário incorporado.
   * Se você modificar apenas o formulário incorporado em uma página do site publicada, publique o formulário original e as alterações serão refletidas na página do site publicado. A página do site publicada inclui uma referência ao formulário e não requer a republicação da página.
   * Se você modificar a página [!DNL Sites] e o formulário incorporado, publique novamente a página [!DNL Sites] e o formulário.

      ![embed-in-aem-sites](assets/embed-in-aem-sites.png)
   Formulário de Alteração de Endereço de Entrega e Faturamento adicionado a uma página AEM [!DNL Sites].

## Incorporar o formulário adaptativo em uma página da Web externa {#embed-the-adaptive-form-in-an-external-webpage}

É possível incorporar um formulário adaptável a uma página da Web externa (uma página da Web não AEM hospedada fora do AEM) inserindo algumas linhas do JavaScript na página da Web externa. O código JavaScript envia uma solicitação HTTP ao servidor AEM [!DNL Forms] para o formulário adaptável e recursos relacionados e adiciona o formulário adaptável à página da Web. Para obter etapas detalhadas, consulte [incorporar o formulário adaptável a uma página da Web externa](/help/forms/using/embed-adaptive-form-external-web-page.md).
