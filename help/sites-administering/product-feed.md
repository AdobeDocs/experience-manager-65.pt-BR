---
title: Feed do produto
seo-title: Feed do produto
description: Saiba mais sobre o Feed de produtos do AEM.
seo-description: Saiba mais sobre o Feed de produtos do AEM.
uuid: 99eb9bdc-2717-45d4-9203-6394b7d7ddc6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 1f920892-c52e-42ca-900c-2c7ab3c503b3
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Product Feed {#product-feed}

O AEM se integra ao [Search&amp;Promote](https://www.adobe.com/solutions/testing-targeting/searchandpromote.html) e permite:

* use a API eCommerce, independentemente da estrutura do repositório subjacente e da plataforma de comércio.
* aproveite o recurso Conector de índice do Search&amp;Promote para fornecer um feed de produto no formato XML.
* aproveitar o recurso de Controle remoto do Search&amp;Promote para executar solicitações sob demanda ou programadas do feed do produto
* geração de feed para diferentes contas do Search&amp;Promote, configuradas como configurações de serviços em nuvem.

É necessário ter uma conta válida e [configurar a conexão com o Search&amp;Promote](/help/sites-administering/search-and-promote.md#configuring-the-connection-to-search-promote). Você também deve verificar se está usando o centro [de](/help/sites-administering/search-and-promote.md#configuring-the-data-center) dados correto e se o **URI do servidor remoto **está configurado.

## Configurar o feed do produto {#set-up-the-product-feed}

Primeiro, é necessário inserir uma raiz do site e um atributo de identificador. Para fazer isso:

1. Navegue até sua configuração do Search&amp;Promote.
1. Clique em **[!UICONTROL Editar]**.
1. Clique na guia Configuração **[!UICONTROL do feed do conector de]** índice.
1. Insira a raiz **[!UICONTROL e o atributo]** **** Identificador do site.

   >[!NOTE]
   >
   >A raiz **[!UICONTROL do site]** da Web é a raiz do site de comércio eletrônico, por exemplo `/content/geometrixx-outdoors/en`.
   >
   >O atributo **** Identifier é uma propriedade JCR que identifica exclusivamente o produto: `identifier`.

1. Clique em **[!UICONTROL OK]**.

Em seguida, você também precisa editar duas configurações no Console da Web antes de gerar feeds de produtos.

### Configuração da implementação do rastreador de produtos do Day CQ Search&amp;Promote para o Geometrixx {#configuring-the-day-cq-search-promote-products-crawler-implementation-for-geometrixx}

1. Navegue até [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Clique em **[!UICONTROL Day CQ Search&amp;Promote products crawler implementation for Geometrixx]**.
1. Especifique o número de conta do Search&amp;Promote ao qual este rastreador está vinculado. Ele será usado para procurar a configuração de serviços em nuvem usada por esse rastreador.
1. Clique em **[!UICONTROL Salvar]**.

### Configuração do Gerador de Feed de Produtos do Search&amp;Promote do Day CQ para o Geometrixx {#configuring-the-day-cq-search-promote-products-feed-generator-for-geometrixx}

1. Navegue até [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Clique em Gerador de feed de produtos do **[!UICONTROL Day CQ Search&amp;Promote para o Geometrixx]**.
1. Especifique o número de conta do Search&amp;Promote ao qual este gerador está vinculado. Ele será usado para procurar a configuração de serviços em nuvem usada por esse gerador.
1. Clique em **[!UICONTROL Salvar]**.

## Agende o feed do produto {#schedule-the-product-feed}

Para ativar a geração de feed programada, é necessário configurar um agendador para ela.
Um programador está configurado como uma configuração secundária da configuração específica dos serviços em nuvem do Search&amp;Promote.

1. Navegue até sua configuração do Search&amp;Promote.
1. Clique em **[!UICONTROL +]** ao lado de Configuração **[!UICONTROL do]** Agendador.
1. Insira um **[!UICONTROL Título]** reconhecível aos autores da página e um **[!UICONTROL Nome]** exclusivo.
1. Clique em **[!UICONTROL Criar]**. Uma caixa de diálogo é aberta.

   ![chlimage_1-108](assets/chlimage_1-108a.png)

1. Digite a senha **[!UICONTROL do controle]** remoto. É a senha que você configurou em sua conta do Search&amp;Pronote.

   >[!NOTE]
   >
   >Esta não é a senha da sua conta do Search&amp;Promote. Você pode localizar e alterar essa senha fazendo logon na sua conta do Search&amp;Promote e indo para **[!UICONTROL Índice]** e, em seguida, para o controle **** remoto.

1. Marque a caixa **[!UICONTROL Ativar agendamento]** .
1. Selecione um **[!UICONTROL agendamento]**. É o cronograma real de geração de feed.
1. Habilite ou não a indexação **** sob demanda. Este recurso é usado para chamar manualmente o índice do Search&amp;Promote. Se a opção **[!UICONTROL Solicitar feed]** completo de produtos estiver marcada, o Search&amp;Promote solicitará um feed completo de produtos. Caso contrário, um feed de produtos incrementais será solicitado.

   >[!NOTE]
   >
   >O recurso de indexação sob demanda utiliza o recurso Controle remoto do Search&amp;Promote. Quando uma indexação remota é chamada, a indexação não é iniciada imediatamente, mas uma solicitação de indexação será publicada no Search&amp;Promote usando o recurso de controle remoto.

1. Clique em **[!UICONTROL OK]**.

Agora que você configurou tudo, é possível visualizar uma página XML contendo todos os produtos sob a raiz do site configurado: [http://localhost:4502/etc/commerce/searchpromote/feed/full](http://localhost:4502/etc/commerce/searchpromote/feed/full).
