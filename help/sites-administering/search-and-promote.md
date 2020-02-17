---
title: Integração com o Adobe Search&Promote
seo-title: Integração com o Adobe Search&Promote
description: Saiba como integrar-se ao Adobe Search&Promote.
seo-description: Saiba como integrar-se ao Adobe Search&Promote.
uuid: 7e9384d9-9e4f-4e00-a1c9-35547de6ceb8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: aca444f6-418a-4c01-ae19-663b4e04fab9
docset: aem65
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Integrating with Adobe Search&amp;Promote{#integrating-with-adobe-search-promote}

Para chamar o serviço Adobe Search&amp;Promote de seu site, execute as seguintes tarefas:

1. Especifique o URL da nuvem.
1. Configure a conexão com o serviço Search&amp;Promote.
1. Adicionar componentes do Search&amp;Promote ao Sidekick.
1. Use os componentes para criar o conteúdo. (Consulte [Adicionar recursos do Search&amp;Promote a uma página](/help/sites-authoring/search-and-promote.md)da Web.)
1. Adicione banners às suas páginas. As imagens de banner são sensíveis aos dados do Search&amp;Promote.
1. Gere um mapa do site para o serviço Search&amp;Promote consumir.

>[!NOTE]
>
>Se você estiver usando o Search&amp;Promote com uma configuração de proxy personalizada, precisará configurar ambas as configurações de proxy do Cliente HTTP, já que algumas funcionalidades do AEM estão usando as APIs 3.x e outras as APIs 4.x:
>
>* 3.x é configurado com [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x é configurado com [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



## Alteração do URL do serviço Search&amp;Promote {#changing-the-search-promote-service-url}

O URL padrão configurado para o serviço Search&amp;Promote é `https://searchandpromote.omniture.com/px/`. Para usar um serviço diferente, use o console OSGi para especificar um URL diferente.

1. Abra o console OSGi e clique na guia Configuração. ([https://localhost:4502/system/console/configMgr.](https://localhost:4502/system/console/configMgr))
1. Clique no item Configuração do Day CQ Search&amp;Promote.
1. Digite o URL na caixa URI do servidor remoto e clique em Salvar.

## Configurar a conexão com o Search&amp;Promote {#configuring-the-connection-to-search-promote}

Configure uma ou mais conexões para o Search&amp;Promote para que suas páginas da Web possam interagir com o serviço. Para se conectar, você precisa da identificação do membro e do número da conta da sua conta do Search&amp;Promote.

1. No ícone **Ferramentas** > **Implantação**, selecione Serviços **em** nuvem.

   Isso leva você ao Painel de serviços em nuvem. Se estiver em uma máquina local, o url do painel terá a seguinte aparência:

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. Na página Serviços em nuvem, clique no link do Adobe Search&amp;Promote ou no ícone do Search&amp;Promote.

1. Se esta for a primeira vez que você estiver configurando o Adobe Search&amp;Promote, clique em **Configurar agora** para abrir o painel Criar configuração.

   Se você quiser saber mais sobre o Search&amp;Promote, clique em **Saiba mais** em vez disso.

   ![](assets/chlimage_1-59.png)

1. Insira um **Título** reconhecível aos autores da página, insira um **Nome** exclusivo e clique em **Criar**.

   The **Edit Component** window opens.

   Além disso, a configuração recém-criada é exibida abaixo de Configurações **** disponíveis no item de lista do painel **Serviços em** nuvem do Adobe Search&amp;Promote.

   ![](assets/chlimage_1-60.png)

1. Adicione o seguinte aos campos na caixa de diálogo **Editar componente** .

   * **ID de membro**
   * **Número da conta**
   >[!NOTE]
   >
   >Para obter essas informações **você mesmo,** primeiro precisa fazer logon
   >
   >[https://searchandpromote.omniture.com/center/](https://searchandpromote.omniture.com/center/)
   >
   >
   >usando suas credenciais válidas do Search&amp;Promote (email/senha).
   >Em seguida, é necessário observar o url na barra de endereços do seu navegador, que deve ser semelhante a:
   >[](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >**Em que:**
   >
   >    * **XXXXXXXX** corresponde à sua** ID de membro**
   >    * **AAAAAAA** corresponde ao número da sua **conta**


1. Click **Connect To Search&amp;Promote**.

   Quando a mensagem de sucesso da conexão for exibida, clique em **OK**.

   (Após a conexão, o texto do botão muda para** Reconectar ao Search&amp;Promote**.)

1. Clique em **OK**. A página Configurações do Search&amp;Promote é exibida para a configuração que você acabou de criar.

## Configuração do data center {#configuring-the-data-center}

Se sua conta do Search&amp;Promote estiver na Ásia ou na Europa, você precisará alterar o data center padrão para que ele aponte para a direita (o data center padrão é para contas norte-americanas).

Para configurar o data center:

1. Navegue até o console da Web em `https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`

   ![](assets/chlimage_1-61.png)

1. Dependendo do local do servidor, altere o URI para um dos seguintes:

   * América do Norte: [https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA: [https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC: [https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. Clique em **Salvar**.

## Adicionar componentes do Search&amp;Promote ao Sidekick {#adding-search-promote-components-to-sidekick}

No modo Design, edite um componente **par** para permitir os componentes do Search&amp;Promote no Sidekick. (See the [Components](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode) documentation for more information.)

Para obter informações sobre como usar os componentes, consulte [Adicionar recursos do Search&amp;Promote a uma página](/help/sites-authoring/search-and-promote.md)da Web.)

## Especificação do serviço Search&amp;Promote que suas páginas usam {#specifying-the-search-promote-service-that-your-pages-use}

Configure páginas da Web para que elas usem um serviço do Search&amp;Promote específico. Os componentes do Search&amp;Promote usam automaticamente o serviço de sua página de host.

Quando você define as propriedades do Search&amp;Promote para uma página, todas as páginas secundárias herdam as configurações. Se necessário, é possível configurar páginas secundárias para substituir as configurações herdadas.

>[!NOTE]
>
>A conexão de serviço já deve estar configurada. (Consulte [Configurar a conexão com o Search&amp;Promote](#connection).)

1. Abra a caixa de diálogo Propriedades **da** página. Por exemplo, na página** Sites**, clique com o botão direito do mouse na página e clique em **Propriedades**.
1. Clique na guia Serviços **em** nuvem.
1. Para desativar a herança das configurações de serviços em nuvem de uma página pai, clique no ícone de cadeado ao lado do caminho de herança.

   ![](assets/sandpinheritpadlock.png)

1. Clique em **Adicionar serviço**, selecione **Adobe Search&amp;Promote** e clique em **OK**.
1. Selecione a configuração de conexão para sua conta do Search&amp;Promote e clique em **OK**.

## Product Feed {#product-feed}

A integração do Search&amp;Promote permite:

* use a API eCommerce, independentemente da estrutura do repositório subjacente e da plataforma de comércio.
* aproveite o recurso Conector de índice do Search&amp;Promote para fornecer um feed de produto no formato XML.
* aproveitar o recurso de Controle remoto do Search&amp;Promote para executar solicitações sob demanda ou programadas do feed do produto
* geração de feed para diferentes contas do Search&amp;Promote, configuradas como configurações de serviços em nuvem.

Para obter mais informações, leia Feed [do](/help/sites-administering/product-feed.md)produto.
