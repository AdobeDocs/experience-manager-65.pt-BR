---
title: 'Tutorial: Publish seu formulário adaptável'
description: Publish o formulário adaptável como uma página AEM, incorpore o formulário a uma página AEM Sites ou incorpore o formulário adaptável em uma página da Web externa
contentOwner: khsingh
topic-tags: introduction
docset: aem65
feature: Adaptive Forms
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Tutorial: Publish seu formulário adaptável {#tutorial-publish-your-adaptive-form}

![Imagem-herói](do-not-localize/13-publish-your-adaptive-form-small.png)

Este tutorial é uma etapa da série [Criar o primeiro formulário adaptável](https://helpx.adobe.com/br/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso completo do tutorial.

Quando o formulário adaptável estiver pronto, você poderá publicar o formulário para disponibilizá-lo para os usuários finais. Os usuários finais podem abrir o formulário publicado em qualquer dispositivo e navegador de Internet. Quando um formulário adaptável é publicado, o formulário e o conteúdo relacionado são copiados de uma instância de autor AEM para uma instância de publicação AEM. O formulário é disponibilizado ao usuário final por meio da instância de publicação.

Você tem os seguintes métodos para publicar um formulário adaptável:

* [Publish o formulário adaptável como uma página AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incorporar o formulário adaptável em uma página do AEM Sites](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incorpore o formulário adaptável em uma página externa da Web (uma página da Web não AEM hospedada fora do AEM)](../../forms/using/publish-your-adaptive-form.md)

## Antes de começar {#before-you-start}

* **[Configurar uma instância de publicação do AEM Forms](https://helpx.adobe.com/br/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**: a instância de publicação é uma instância pública do AEM [!DNL Forms] em execução no modo de publicação. Em um ambiente de produção, a instância de publicação está fora do firewall da organização.
* **[Configurar replicação e replicação inversa](https://helpx.adobe.com/br/experience-manager/6-3/help/sites-deploying/replication.html)**: a replicação copia o conteúdo da instância do autor para uma instância de publicação e retorna a entrada do usuário (por exemplo, entrada de formulário) da instância de publicação para a instância do autor.

## Publish o formulário adaptável como uma página AEM {#publish-the-adaptive-form-as-an-aem-page}

Quando o formulário adaptável é publicado como uma página AEM, a página da Web inteira contém somente formulários publicados. É possível usar a URL do formulário adaptável para vinculá-lo a partir de outra página da Web. Para publicar o formulário adaptável **delivery-address-add-update-form** como uma página AEM:

1. Faça logon na instância de autor do AEM [!DNL Forms] e localize o formulário adaptável send-address-add-update-form na interface do usuário do AEM [!DNL Forms].
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Selecione o formulário adaptável delivery-address-add-update-form e selecione **[!UICONTROL Publish]**. Uma caixa de diálogo contendo ativos relacionados ao formulário adaptável é exibida. Selecione **[!UICONTROL Publish]**. O formulário adaptável é publicado e uma caixa de diálogo de sucesso é exibida.
1. Abra o formulário na instância de publicação. O formulário está disponível para o usuário final preencher e enviar.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incorporar o formulário adaptável em uma página do AEM Sites {#embed-the-adaptive-form-in-an-aem-sites-page}

O AEM [!DNL Forms] permite que desenvolvedores de formulários incorporem formulários adaptáveis em uma página AEM [!DNL Sites]. O formulário adaptável incorporado é totalmente funcional e os usuários podem preencher e enviar o formulário sem sair da página. Ele ajuda o usuário a permanecer no contexto de outros elementos na página da Web e interagir simultaneamente com o formulário.

O AEM [!DNL Forms] fornece um componente, Contêiner AEM [!DNL Forms], para incorporar um formulário adaptável a uma página AEM [!DNL Sites]. Por padrão, o componente não está visível no contêiner AEM [!DNL Sites]. Execute as seguintes etapas para habilitar o componente de Contêiner AEM [!DNL Forms] e incorporar o formulário adaptável em uma página AEM [!DNL Sites]:

1. Crie e abra uma página no site We.Retail para edição. Por exemplo, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). O formulário adaptável está incorporado à página [!DNL Sites].

   Você também pode incorporar o formulário adaptável em uma página existente do We.Retail [!DNL Site's]. Por exemplo, a página SOBRE EUA [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Economiza tempo para criar uma página. As etapas abaixo usam a página recém-criada.

   O site We.Retail é enviado com AEM. Se você não tiver o site We.Retail instalado, consulte [Implementação de referência We.Retail](https://helpx.adobe.com/br/experience-manager/6-3/help/sites-developing/we-retail.html) para instalar o site.

1. Selecione as informações da página ![propriedades](assets/properties.png) e selecione a opção **[!UICONTROL Editar Modelo]** na página do site We.Retail recém-criada. O modelo da página é aberto em uma nova guia do navegador.
1. Selecione dentro da caixa **[!UICONTROL contêiner de layout]** e selecione ![feedmanagement](assets/feedmanagement.png). Na guia **[!UICONTROL Componentes Permitidos]**, expanda a opção **[!UICONTROL Geral]**, selecione a opção **[!UICONTROL Formulário AEM]** e selecione ![save_icon](assets/save_icon.svg). O componente de Contêiner AEM [!DNL Forms] está habilitado para a página.

1. Abra a guia do navegador contendo a página AEM [!DNL Sites] aberta na etapa 1. Selecione a caixa **[!UICONTROL Arraste componentes aqui]** e selecione **+.** Na caixa **[!UICONTROL Inserir novo componente]**, selecione **[!UICONTROL Formulário AEM]**. O componente **[!UICONTROL Contêiner do AEM Forms]** é adicionado à página.
1. Selecione o componente **[!UICONTROL contêiner de AEM Forms]** e selecione ![configure-icon](assets/configure-icon.svg). Uma caixa de diálogo com propriedades do Contêiner AEM [!DNL Forms] é exibida. No campo **[!UICONTROL Caminho do ativo]**, navegue e selecione o formulário adaptável delivery-address-add-update-form. Selecione ![save_icon](assets/save_icon.svg). O formulário adaptável é incorporado na página.
1. Publish o formulário adaptável e a página [!DNL Sites]. Estes são alguns pontos a serem considerados:

   * Se você publicar a página [!DNL Sites] do AEM pela primeira vez e ela incluir um formulário inserido, publique a página [!DNL Sites] e o formulário inserido.
   * Se você modificar apenas o formulário inserido em uma página de site publicada, publique o formulário original e as alterações refletirão na página de site publicada. A página do site publicada inclui uma referência ao formulário e não requer a republicação da página.
   * Se você modificar a página [!DNL Sites] e o formulário inserido, republique a página [!DNL Sites] e o formulário.

     ![embed-in-aem-sites](assets/embed-in-aem-sites.png)

   Formulário de alteração de endereço de remessa e cobrança adicionado a uma página AEM [!DNL Sites].

## Incorporar o formulário adaptável em uma página da Web externa {#embed-the-adaptive-form-in-an-external-webpage}

É possível incorporar um formulário adaptável a uma página da Web externa (uma página da Web não AEM hospedada fora do AEM) inserindo algumas linhas do JavaScript na página da Web externa. O código JavaScript envia uma solicitação HTTP para o servidor AEM [!DNL Forms] para o formulário adaptável e recursos relacionados e adiciona o formulário adaptável à página da Web. Para obter etapas detalhadas, consulte [incorporar o formulário adaptável a uma página da Web externa](/help/forms/using/embed-adaptive-form-external-web-page.md).
