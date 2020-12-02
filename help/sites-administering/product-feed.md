---
title: Feed do produto
seo-title: Feed do produto
description: Saiba mais sobre o Feed de produtos AEM.
seo-description: Saiba mais sobre o Feed de produtos AEM.
uuid: 99eb9bdc-2717-45d4-9203-6394b7d7ddc6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 1f920892-c52e-42ca-900c-2c7ab3c503b3
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 2%

---


# Feed do produto {#product-feed}

AEM integra-se com [Search &amp; Promote](https://www.adobe.com/solutions/testing-targeting/searchandpromote.html) e permite que você:

* use a API eCommerce, independentemente da estrutura do repositório subjacente e da plataforma de comércio.
* aproveite o recurso Conector de índice do Search &amp; Promote para fornecer um feed de produto no formato XML.
* aproveitar o recurso de Controle remoto do Search &amp; Promote para executar solicitações sob demanda ou programadas do feed do produto
* geração de feed para diferentes contas de Search &amp; Promote, configurada como configurações de serviços em nuvem.

É necessário ter uma conta válida e [configurar a conexão com o Search &amp; Promote](/help/sites-administering/search-and-promote.md#configuring-the-connection-to-search-promote). Você também deve verificar se está usando o [data center](/help/sites-administering/search-and-promote.md#configuring-the-data-center) correto e se o **URI do servidor remoto **está configurado.

## Configurar o Feed de produto {#set-up-the-product-feed}

Primeiro, é necessário inserir uma raiz do site e um atributo de identificador. Para fazer isso:

1. Navegue até sua configuração de Search &amp; Promote.
1. Clique em **[!UICONTROL Editar]**.
1. Clique na guia **[!UICONTROL Configuração de feed do conector de índice]**.
1. Digite o atributo **[!UICONTROL raiz do site]** e **[!UICONTROL Identificador]**.

   >[!NOTE]
   >
   >A **[!UICONTROL raiz do site]** é a raiz do site de comércio eletrônico, por exemplo `/content/geometrixx-outdoors/en`.
   >
   >O atributo **[!UICONTROL Identifier]** é uma propriedade JCR que identifica exclusivamente o produto: `identifier`.

1. Clique em **[!UICONTROL OK]**.

Em seguida, você também precisa editar duas configurações no Console da Web antes de gerar feeds de produtos.

### Configuração da implementação do rastreador de produtos do Day CQ para Geometrixx {#configuring-the-day-cq-search-promote-products-crawler-implementation-for-geometrixx}

1. Navegue até [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Clique em **[!UICONTROL Implementação do rastreador de produtos do Day CQ para Geometrixx]**.
1. Especifique o número da conta de Search &amp; Promote à qual este rastreador está vinculado. Ele será usado para procurar a configuração de serviços em nuvem usada por esse rastreador.
1. Clique em **[!UICONTROL Salvar]**.

### Configuração do Gerador de Feed de Produtos do Day CQ para o Geometrixx {#configuring-the-day-cq-search-promote-products-feed-generator-for-geometrixx}

1. Navegue até [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Clique em **[!UICONTROL Gerador de feed de produtos do Day CQ para Geometrixx]**.
1. Especifique o número da conta de Search &amp; Promote à qual este gerador está ligado. Ele será usado para procurar a configuração de serviços em nuvem usada por esse gerador.
1. Clique em **[!UICONTROL Salvar]**.

## Agendar o Feed de produto {#schedule-the-product-feed}

Para ativar a geração de feed programada, é necessário configurar um scheduler para ela.
Um scheduler é configurado como uma configuração secundária da configuração específica dos serviços da Search &amp; Promote Cloud.

1. Navegue até sua configuração de Search &amp; Promote.
1. Clique em **[!UICONTROL +]** ao lado de **[!UICONTROL configuração do Scheduler]**.
1. Insira um **[!UICONTROL Title]** que seja reconhecível para autores de página e um **[!UICONTROL Nome]** exclusivo.
1. Clique em **[!UICONTROL Criar]**. Uma caixa de diálogo é aberta.

   ![chlimage_1-108](assets/chlimage_1-108a.png)

1. Digite a **[!UICONTROL Senha do controle remoto]**. É a senha que você configurou em sua conta do Search&amp;Pronote.

   >[!NOTE]
   >
   >Esta não é a senha da sua conta do Search &amp; Promote. Você pode encontrar e alterar essa senha fazendo logon em sua conta do Search &amp; Promote e indo para **[!UICONTROL Index]** e, em seguida, para **[!UICONTROL Controle remoto]**.

1. Marque a caixa **[!UICONTROL Habilitar programação]**.
1. Selecione um **[!UICONTROL Agendamento]**. É o cronograma real de geração de feed.
1. Ative a **[!UICONTROL indexação sob demanda]** ou não. Esse recurso é usado para chamar manualmente o índice de Search &amp; Promote. Se **[!UICONTROL Solicitar feed de produtos completos]** estiver marcado, o Search &amp; Promote solicitará um feed de produtos completo. Caso contrário, um feed de produtos incrementais será solicitado.

   >[!NOTE]
   >
   >O recurso de indexação sob demanda utiliza o recurso de Controle remoto do Search &amp; Promote. Quando uma indexação remota é chamada, a indexação não será start imediatamente, mas uma solicitação de indexação será postada no Search &amp; Promote usando o recurso de controle remoto.

1. Clique em **[!UICONTROL OK]**.

Agora que você configurou tudo, é possível visualizar uma página XML contendo todos os produtos sob a raiz do site configurado: [http://localhost:4502/etc/commerce/searchpromote/feed/full](http://localhost:4502/etc/commerce/searchpromote/feed/full).
