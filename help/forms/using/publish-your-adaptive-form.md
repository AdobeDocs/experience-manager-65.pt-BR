---
title: "Tutorial: publique seu formulário adaptável"
seo-title: "Tutorial: Publish your adaptive form"
description: Publicar o formulário adaptável como uma página AEM, incorporar o formulário a uma página do AEM Sites ou incorporar o formulário adaptável em uma página da Web externa
seo-description: Publish the adaptive form as an AEM page, embed the form to an AEM Sites page, or embed the adaptive form in an external webpage
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
feature: Adaptive Forms
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Tutorial: publique seu formulário adaptável {#tutorial-publish-your-adaptive-form}

![Imagem principal](do-not-localize/13-publish-your-adaptive-form-small.png)

Este tutorial é uma etapa da [Criar O Primeiro Formulário Adaptável](https://helpx.adobe.com/br/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) série. É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso completo do tutorial.

Quando o formulário adaptável estiver pronto, você poderá publicar o formulário para disponibilizá-lo para os usuários finais. Os usuários finais podem abrir o formulário publicado em qualquer dispositivo e navegador de Internet. Quando um formulário adaptável é publicado, o formulário e o conteúdo relacionado são copiados de uma instância de autor AEM para uma instância de publicação AEM. O formulário é disponibilizado ao usuário final por meio da instância de publicação.

Você tem os seguintes métodos para publicar um formulário adaptável:

* [Publicar o formulário adaptável como uma página AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incorporar o formulário adaptável em uma página do AEM Sites](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incorpore o formulário adaptável em uma página externa da Web (uma página da Web não AEM hospedada fora do AEM)](../../forms/using/publish-your-adaptive-form.md)

## Antes de começar {#before-you-start}

* **[Configurar uma instância de publicação do AEM Forms](https://helpx.adobe.com/br/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**: a instância de publicação é uma instância pública do AEM [!DNL Forms] execução no modo de publicação. Em um ambiente de produção, a instância de publicação está fora do firewall da organização.
* **[Configurar replicação e replicação reversa](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**: a replicação copia o conteúdo da instância do autor para uma instância de publicação e retorna a entrada do usuário (por exemplo, entrada de formulário) da instância de publicação para a instância do autor.

## Publicar o formulário adaptável como uma página AEM {#publish-the-adaptive-form-as-an-aem-page}

Quando o formulário adaptável é publicado como uma página AEM, a página da Web inteira contém somente formulários publicados. É possível usar a URL do formulário adaptável para vinculá-lo a partir de outra página da Web. Para publicar o **endereço-entrega-adicionar-atualizar-formulário** formulário adaptável como uma página AEM:

1. Fazer logon no AEM [!DNL Forms] instância do autor e localize o formulário adaptável delivery-address-add-update-form no AEM [!DNL Forms] IU.
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Selecione o formulário adaptável delivery-address-add-update-form e selecione **[!UICONTROL Publish]**. Uma caixa de diálogo contendo ativos relacionados ao formulário adaptável é exibida. Selecionar **[!UICONTROL Publish]**. O formulário adaptável é publicado e uma caixa de diálogo de sucesso é exibida.
1. Abra o formulário na instância de publicação. O formulário está disponível para o usuário final preencher e enviar.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incorporar o formulário adaptável em uma página do AEM Sites {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] permite que os desenvolvedores de formulários incorporem formulários adaptáveis em um AEM [!DNL Sites] página. O formulário adaptável incorporado é totalmente funcional e os usuários podem preencher e enviar o formulário sem sair da página. Ele ajuda o usuário a permanecer no contexto de outros elementos na página da Web e interagir simultaneamente com o formulário.

AEM [!DNL Forms] fornecer um componente, AEM [!DNL Forms] Contêiner, para incorporar um formulário adaptável a um AEM [!DNL Sites] página. Por padrão, o componente não está visível no AEM [!DNL Sites] recipiente. Execute as seguintes etapas para ativar o AEM [!DNL Forms] Componente de container e para incorporar o formulário adaptável em um AEM [!DNL Sites] Página:

1. Crie e abra uma página no site We.Retail para edição. Por exemplo, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). O formulário adaptável é incorporado ao [!DNL Sites] página.

   Você também pode incorporar o formulário adaptável em um We.Retail existente [!DNL Site's] página. Por exemplo, a página SOBRE os EUA [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Economiza tempo para criar uma página. As etapas abaixo usam a página recém-criada.

   O site We.Retail é enviado com AEM. Se você não tiver o site We.Retail instalado, consulte [Implementação de referência do We.Retail](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) instalar o site.

1. Selecionar ![propriedades](assets/properties.png) informações da página e selecione o **[!UICONTROL Editar modelo]** opção na página do site We.Retail recém-criada. O modelo da página é aberto em uma nova guia do navegador.
1. Selecione dentro do **[!UICONTROL contêiner de layout]** e selecione ![gerenciamento de feeds](assets/feedmanagement.png). No **[!UICONTROL Componentes permitidos]** , expanda a **[!UICONTROL Geral]** selecione a opção **[!UICONTROL Formulário AEM]** e selecione ![save_icon](assets/save_icon.svg). O AEM [!DNL Forms] O componente de container é ativado para a página.

1. Abra a guia do navegador que contém AEM [!DNL Sites] página aberta na etapa 1. Selecione o **[!UICONTROL Arraste os componentes para cá]** e selecione **+.** No **[!UICONTROL Inserir novo componente]** , selecione **[!UICONTROL Formulário AEM]**. A variável **[!UICONTROL Contêiner do AEM Forms]** componente é adicionado à página.
1. Selecione o **[!UICONTROL Contêiner AEM Forms]** e selecione ![configure-icon](assets/configure-icon.svg). Uma caixa de diálogo com propriedades do AEM [!DNL Forms] O contêiner é exibido. No **[!UICONTROL Caminho do ativo]** e selecione o formulário adaptável delivery-address-add-update-form. Selecionar ![save_icon](assets/save_icon.svg). O formulário adaptável é incorporado na página.
1. Publicar o formulário adaptável e [!DNL Sites] página. Estes são alguns pontos a serem considerados:

   * Se você publicar o AEM [!DNL Sites] página pela primeira vez e incluir um formulário incorporado, publique o [!DNL Sites] e o formulário incorporado.
   * Se você modificar apenas o formulário inserido em uma página de site publicada, publique o formulário original e as alterações refletirão na página de site publicada. A página do site publicada inclui uma referência ao formulário e não requer a republicação da página.
   * Se você modificar a variável [!DNL Sites] e o formulário incorporado, publique novamente a [!DNL Sites] página e o formulário.

     ![incorporado no aem-sites](assets/embed-in-aem-sites.png)

   Formulário de alteração de endereço de remessa e cobrança adicionado a um AEM [!DNL Sites] página.

## Incorporar o formulário adaptável em uma página da Web externa {#embed-the-adaptive-form-in-an-external-webpage}

Você pode incorporar um formulário adaptável a uma página da Web externa (uma página da Web não AEM hospedada fora do AEM) inserindo algumas linhas de JavaScript na página da Web externa. O código JavaScript envia uma solicitação HTTP para o AEM [!DNL Forms] para o formulário adaptável e recursos relacionados e adiciona o formulário adaptável à página da Web. Para obter etapas detalhadas, consulte [incorporar o formulário adaptável a uma página externa da web](/help/forms/using/embed-adaptive-form-external-web-page.md).
