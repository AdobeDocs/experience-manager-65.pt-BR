---
title: Integrar com o Adobe Search & Promote
description: Saiba como integrar com o Adobe Search & Promote.
uuid: 7e9384d9-9e4f-4e00-a1c9-35547de6ceb8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: aca444f6-418a-4c01-ae19-663b4e04fab9
docset: aem65
exl-id: 15f45978-a983-49a0-91cf-c7610fc37eef
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 1%

---

# Integrar com o Adobe Search &amp; Promote{#integrating-with-adobe-search-promote}

Para chamar o serviço Adobe Search &amp; Promote de seu site, execute as seguintes tarefas:

1. Especifique o URL da nuvem.
1. Configure a conexão com o serviço Search &amp; Promote.
1. Adicionar componentes do Search &amp; Promote ao Sidekick.
1. Use os componentes para criar o conteúdo. (Consulte [Adicionar recursos do Search &amp; Promote a uma página da Web](/help/sites-authoring/search-and-promote.md).)
1. Adicione banners às suas páginas. Imagens de banner são sensíveis aos dados do Search &amp; Promote.
1. Gere um mapa de site para o serviço Search &amp; Promote ser consumido.

>[!NOTE]
>
>Se você estiver usando o Search &amp; Promote com uma configuração de proxy personalizada, deverá configurar ambas as configurações de proxy do cliente HTTP, pois algumas funcionalidades do Adobe Experience Manager estão usando as APIs 3.x e outras as APIs 4.x:
>
>* 3.x está configurado com [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x está configurado com [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



## Alterar o URL do serviço Search &amp; Promote {#changing-the-search-promote-service-url}

O URL padrão configurado para o serviço Search &amp; Promote é `https://searchandpromote.omniture.com/px/`. Para usar um serviço diferente, use o console OSGi para especificar um URL diferente.

1. Abra o console OSGi e selecione a guia **[!UICONTROL Configuração]**. ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Selecione o item Configuração do Search &amp; Promote Day CQ .
1. Insira o URL na caixa URI do servidor remoto e selecione **[!UICONTROL Save]**.

## Configure a conexão com o Search &amp; Promote {#configuring-the-connection-to-search-promote}

Configure uma ou mais conexões com o Search &amp; Promote para que suas páginas da Web possam interagir com o serviço. Para se conectar, você precisa da identificação do membro e do número da conta do Search &amp; Promote.

1. No Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > selecione **[!UICONTROL Cloud Services]**.

   Se você estiver em um computador local, o URL do painel será semelhante ao seguinte:

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. Na página Cloud Services, selecione o link Adobe Search &amp; Promote ou o ícone Search &amp; Promote.

1. Se você estiver configurando o Adobe Search &amp; Promote pela primeira vez, selecione **[!UICONTROL Configurar agora]** para abrir o painel Criar configuração.

   Para saber mais sobre o Search &amp; Promote, selecione **[!UICONTROL Saiba mais]**.

   ![](assets/chlimage_1-59.png)

1. Insira um **[!UICONTROL Título]** que seja reconhecível aos autores da página e insira um **[!UICONTROL Nome]** exclusivo.
1. Selecione **[!UICONTROL Criar]**.

   Além disso, a Configuração recém-criada aparece abaixo de **Configurações disponíveis** no item de lista **Cloud Services dashboard** Adobe.

   ![](assets/chlimage_1-60.png)

1. Na caixa de diálogo **[!UICONTROL Editar componente]**, adicione o seguinte aos campos.

   * **ID de membro**
   * **Número da conta**

   >[!NOTE]
   >
   >Para obter essas informações **você mesmo,** primeiro deve fazer logon em
   >
   >[https://searchandpromote.omniture.com/center/](https://searchandpromote.omniture.com/center/)
   >
   >
   >usando suas credenciais válidas do Search&amp;Promote (email/senha).
   >Em seguida, você deve examinar o url na barra de endereços do navegador, que deve ser semelhante a:
   >[](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >**Em que:**
   >
   >    * **** XXXXXXXX corresponde à sua** ID do membro**
   >    * **** spAAAAcorresponde ao seu número  **de conta**


1. Selecione **[!UICONTROL Conectar ao Search &amp; Promote]**.

   Quando a mensagem de sucesso de conexão for exibida, selecione **[!UICONTROL OK]**.

   (Após a conexão, o texto do botão muda para** Reconectar ao Search &amp; Promote**.)

1. Selecione **[!UICONTROL OK]**. A página Configurações do Search &amp; Promote é exibida para a configuração que você criou.

## Configurar o data center {#configuring-the-data-center}

Se sua conta do Search &amp; Promote estiver na Ásia ou na Europa, você deverá alterar o data center padrão para que ele aponte para o correto (o data center padrão é para contas da América do Norte).

**Para configurar o data center:**

1. Navegue até o console da Web em `https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`

   ![](assets/chlimage_1-61.png)

1. Dependendo do local do servidor, altere o URI para um dos seguintes:

   * América do Norte: [https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA: [https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC: [https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. Selecione **[!UICONTROL Salvar]**.

## Adicionar componentes do Search &amp; Promote ao Sidekick {#adding-search-promote-components-to-sidekick}

No modo Design, edite um componente **par** para permitir os componentes do Search &amp; Promote no Sidekick. (Consulte a documentação [Componentes](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode) para obter mais informações.)

Para obter informações sobre como usar os componentes, consulte [Adicionar recursos do Search &amp; Promote a uma página da Web](/help/sites-authoring/search-and-promote.md).)

## Especifique o serviço de Search &amp; Promote que suas páginas usam {#specifying-the-search-promote-service-that-your-pages-use}

Configure as páginas da Web para que elas usem um serviço específico do Search &amp; Promote. Os componentes do Search &amp; Promote usam automaticamente o serviço de sua página de host.

Quando você configura as propriedades do Search &amp; Promote para uma página, todas as páginas secundárias herdam as configurações. Se necessário, você pode configurar páginas filhas para substituir as configurações herdadas.

>[!NOTE]
>
>A conexão de serviço deve ser configurada com antecedência. (Consulte [Configurar a conexão com Search &amp; Promote](#connection).)

1. Abra a caixa de diálogo **[!UICONTROL Propriedades da página]**. Por exemplo, na página** Sites**, clique com o botão direito do mouse na página e selecione **[!UICONTROL Propriedades]**.
1. Selecione a guia **[!UICONTROL Cloud Services]**.
1. Para desativar a herança das configurações dos serviços de nuvem de uma página pai, selecione o ícone de cadeado ao lado do caminho de herança.

   ![](assets/sandpinheritpadlock.png)

1. Selecione **[!UICONTROL Adicionar Serviço]**.
1. Selecione **[!UICONTROL Adobe Search &amp; Promote]** e selecione **[!UICONTROL OK]**.
1. Selecione a configuração de conexão da sua conta Search &amp; Promote e selecione **OK**.

## Feed do produto {#product-feed}

A integração do Search &amp; Promote permite fazer o seguinte:

* Use a API de eCommerce, independentemente da estrutura de repositório subjacente e da plataforma de comércio.
* Use o recurso Conector de índice do Search &amp; Promote para ter um feed de produto no formato XML.
* Use o recurso de Controle remoto do Search &amp; Promote se desejar executar solicitações sob demanda ou programadas do feed do produto.
* Geração de feed para diferentes contas do Search &amp; Promote, configuradas como configurações de serviços em nuvem.

Para obter mais informações, consulte [Feed do produto](/help/sites-administering/product-feed.md).
