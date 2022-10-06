---
title: "Tutorial: Publicar o formulário adaptável"
seo-title: "Tutorial: Publish your adaptive form"
description: Publicar o formulário adaptável como uma página de AEM, incorporar o formulário a uma página do AEM Sites ou incorporar o formulário adaptável em uma página da Web externa
seo-description: Publish the adaptive form as an AEM page, embed the form to an AEM Sites page, or embed the adaptive form in an external webpage
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
feature: Adaptive Forms
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 2%

---

# Tutorial: Publicar o formulário adaptável {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

Este tutorial é uma etapa do [Criar seu primeiro formulário adaptável](https://helpx.adobe.com/br/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) série. É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso tutorial completo.

Depois que o formulário adaptável estiver pronto, você poderá publicar o formulário para torná-lo disponível para os usuários finais. Os usuários finais podem abrir o formulário publicado em qualquer dispositivo e navegador da Internet. Quando um formulário adaptável é publicado, o formulário e o conteúdo relacionado são copiados de uma instância de autor AEM para uma instância de publicação AEM. O formulário é disponibilizado para o usuário final por meio da instância de publicação.

Você tem os seguintes métodos para publicar um formulário adaptável:

* [Publicar o formulário adaptável como uma página de AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incorporar o formulário adaptável em uma página do AEM Sites](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incorporar o formulário adaptável em uma página da Web externa (uma página da Web que não seja AEM hospedada fora do AEM)](../../forms/using/publish-your-adaptive-form.md)

## Antes de você iniciar {#before-you-start}

* **[Configurar uma instância de publicação do AEM Forms](https://helpx.adobe.com/br/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**: A instância de publicação é uma instância voltada para o público do AEM [!DNL Forms] em execução no modo de publicação. Em um ambiente de produção, a instância de publicação está fora do firewall da organização.
* **[Configurar replicação e replicação inversa](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**: A replicação copia o conteúdo da instância do autor para uma instância de publicação e retorna a entrada do usuário (por exemplo, a entrada de formulário) da instância de publicação para a instância do autor.

## Publicar o formulário adaptável como uma página de AEM {#publish-the-adaptive-form-as-an-aem-page}

Quando o formulário adaptável é publicado como uma Página AEM, a página da Web inteira contém apenas o formulário publicado. Você pode usar o URL do formulário adaptável para vinculá-lo a partir de outra página da Web. Para publicar a **ship-address-add-update-form** formulário adaptável como página AEM:

1. Faça logon no AEM [!DNL Forms] instância do autor e localize o formulário adaptável de delivery-address-add-update-form no AEM [!DNL Forms] IU.
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Selecione o formulário adaptável Taxafe-address-add-update-form e toque em **[!UICONTROL Publicar]**. Uma caixa de diálogo que contém ativos relacionados ao formulário adaptável é exibida. Toque **[!UICONTROL Publicar]**. O formulário adaptável é publicado e uma caixa de diálogo de sucesso é exibida.
1. Abra o formulário na instância de publicação. O formulário está disponível para preenchimento e envio pelo usuário final.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incorporar o formulário adaptável em uma página do AEM Sites {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] permite que desenvolvedores de formulários incorporem formulários adaptáveis de maneira simples em uma AEM [!DNL Sites] página. O formulário adaptável incorporado é totalmente funcional e os usuários podem preencher e enviar o formulário sem sair da página. Ajuda o usuário a permanecer no contexto de outros elementos na página da Web e interagir simultaneamente com o formulário.

AEM [!DNL Forms] fornecer um componente, AEM [!DNL Forms] Contêiner, para incorporar um formulário adaptável a um AEM [!DNL Sites] página. Por padrão, o componente não está visível no AEM [!DNL Sites] contêiner. Execute as seguintes etapas para ativar o AEM [!DNL Forms] Componente de contêiner e para incorporar o formulário adaptável em um AEM [!DNL Sites] Página:

1. Crie e abra uma página no site We.Retail para edição. Por exemplo, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). O formulário adaptável é incorporado ao [!DNL Sites] página.

   Também é possível incorporar o formulário adaptável em um We.Retail existente [!DNL Site's] página. Por exemplo, a página SOBRE EUA [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Ele economiza tempo para criar uma página. As etapas abaixo usam a página recém-criada.

   O site We.Retail é enviado com AEM. Se você não tiver o site We.Retail instalado, consulte [Implementação de referência We.Retail](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) instale o site.

1. Toque ![propriedades](assets/properties.png) e selecione o **[!UICONTROL Editar modelo]** na página recém-criada do site We.Retail. O modelo da página é aberto em uma nova guia do navegador.
1. Toque dentro do **[!UICONTROL contêiner de layout]** e toque em ![gerenciamento de feeds](assets/feedmanagement.png). No **[!UICONTROL Componentes permitidos]** , expanda a **[!UICONTROL Geral]** , selecione a opção **[!UICONTROL Formulário AEM]** e toque em ![save_icon](assets/save_icon.svg). O AEM [!DNL Forms] O componente de contêiner é ativado para a página.

1. Abra a guia do navegador que contém AEM [!DNL Sites] página aberta na etapa 1. Toque no **[!UICONTROL Arraste componentes aqui]** e toque em **+.** No **[!UICONTROL Inserir novo componente]** caixa, toque em **[!UICONTROL Formulário AEM]**. O **[!UICONTROL Contêiner AEM Forms]** é adicionado à página.
1. Toque no **[!UICONTROL Contêiner AEM Forms]** componente e toque ![configure-icon](assets/configure-icon.svg). Uma caixa de diálogo com propriedades de AEM [!DNL Forms] Contêiner é exibido. No **[!UICONTROL Caminho do ativo]** navegue e selecione o formulário adaptável Taxe-address-add-update-form. Toque ![save_icon](assets/save_icon.svg). O formulário adaptável é incorporado na página.
1. Publique o formulário adaptável e [!DNL Sites] página. Estes são alguns pontos que devem ser levados em consideração:

   * Se você publicar a AEM [!DNL Sites] pela primeira vez e inclui um formulário incorporado, publique a variável [!DNL Sites] e o formulário incorporado.
   * Se modificar apenas o formulário incorporado em uma página do site publicada, publique o formulário original e as alterações serão refletidas na página do site publicada. A página do site publicada inclui uma referência ao formulário e não requer a republicação da página.
   * Se você modificar o [!DNL Sites] e o formulário incorporado, republique a variável [!DNL Sites] e o formulário.

      ![embed-in-aem-sites](assets/embed-in-aem-sites.png)
   Formulário de Alteração de Endereço de Entrega e Faturamento adicionado a um AEM [!DNL Sites] página.

## Incorpore o formulário adaptável em uma página da Web externa {#embed-the-adaptive-form-in-an-external-webpage}

Você pode incorporar um formulário adaptável a uma página da Web externa (uma página da Web que não seja AEM hospedada fora do AEM) inserindo algumas linhas de JavaScript na página da Web externa. O código JavaScript envia uma solicitação HTTP para o AEM [!DNL Forms] para o formulário adaptável e recursos relacionados e adiciona o formulário adaptável à página da Web. Para obter etapas detalhadas, consulte [incorporar o formulário adaptável a uma página da Web externa](/help/forms/using/embed-adaptive-form-external-web-page.md).
