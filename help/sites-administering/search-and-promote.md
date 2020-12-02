---
title: Integração com o Adobe
seo-title: Integração com o Adobe
description: Saiba como integrar-se ao Search & Promote Adobe.
seo-description: Saiba como integrar-se ao Search & Promote Adobe.
uuid: 7e9384d9-9e4f-4e00-a1c9-35547de6ceb8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: aca444f6-418a-4c01-ae19-663b4e04fab9
docset: aem65
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 1%

---


# Integração com Adobe Search &amp; Promote{#integrating-with-adobe-search-promote}

Para ligar para o serviço Adobe do seu site, execute as seguintes tarefas:

1. Especifique o URL da nuvem.
1. Configure a conexão com o serviço Search &amp; Promote.
1. Adicione componentes de Search &amp; Promote ao Sidekick.
1. Use os componentes para criar o conteúdo. (Consulte [Adicionar recursos de Search &amp; Promote a uma página da Web](/help/sites-authoring/search-and-promote.md).)
1. Adicione banners às suas páginas. As imagens de banner são sensíveis aos dados do Search &amp; Promote.
1. Gere um mapa do site para o serviço de Search &amp; Promote consumir.

>[!NOTE]
>
>Se você estiver usando um Search &amp; Promote com uma configuração de proxy personalizada, é necessário configurar ambas as configurações de proxy do Cliente HTTP, já que algumas funcionalidades do AEM estão usando as APIs 3.x e outras as APIs 4.x:
>
>* O 3.x está configurado com [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* O 4.x está configurado com [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



## Alteração do URL do serviço do Search &amp; Promote {#changing-the-search-promote-service-url}

O URL padrão configurado para o serviço de Search &amp; Promote é `https://searchandpromote.omniture.com/px/`. Para usar um serviço diferente, use o console OSGi para especificar um URL diferente.

1. Abra o console OSGi e clique na guia Configuração. ([https://localhost:4502/system/console/configMgr.](https://localhost:4502/system/console/configMgr))
1. Clique no item Configuração do Search &amp; Promote Day CQ.
1. Digite o URL na caixa URI do servidor remoto e clique em Salvar.

## Configurar a conexão com o Search &amp; Promote {#configuring-the-connection-to-search-promote}

Configure uma ou mais conexões com o Search &amp; Promote para que suas páginas da Web possam interagir com o serviço. Para conectar-se, você precisa da identificação do membro e do número da conta da sua conta do Search &amp; Promote.

1. No ícone **Ferramentas** > **Implantação**, selecione **Cloud Services**.

   Isso leva você ao Painel Cloud Services. Se estiver em uma máquina local, o url do painel será parecido com isto:

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. Na página Cloud Services, clique no link Adobe Search &amp; Promote ou no ícone Search &amp; Promote.

1. Se esta for a primeira vez que você estiver configurando o Adobe Search &amp; Promote, clique em **Configurar agora** para abrir o painel Criar configuração.

   Se você quiser saber mais sobre o Search &amp; Promote, clique em **Saiba mais** em vez disso.

   ![](assets/chlimage_1-59.png)

1. Insira um **Título** que seja reconhecível aos autores da página, e insira um **Nome** exclusivo, em seguida, clique em **Criar**.

   A janela **Editar componente** é aberta.

   Além disso, a configuração recém-criada é exibida abaixo de **Configurações disponíveis** no item de lista **painel de Cloud Services** Adobe.

   ![](assets/chlimage_1-60.png)

1. Adicione o seguinte aos campos na caixa de diálogo **Editar componente**.

   * **ID de membro**
   * **Número da conta**

   >[!NOTE]
   >
   >Para obter essas informações **você mesmo,** primeiro você precisa fazer logon
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
   >    * **** XXXXXXXX corresponde ao seu** ID de membro**
   >    * **** AAAAAA corresponde ao número da sua  **conta**


1. Clique em **Ligar ao Search &amp; Promote**.

   Quando a mensagem de sucesso da conexão for exibida, clique em **OK**.

   (Após a conexão, o texto do botão muda para** Reconectar-se ao Search &amp; Promote**.)

1. Clique em **OK**. A página Configurações de Search &amp; Promote é exibida para a configuração que você acabou de criar.

## Configuração do data center {#configuring-the-data-center}

Se a sua conta do Search &amp; Promote estiver na Ásia ou na Europa, será necessário alterar o data center padrão para que ele aponte para a direita (o data center padrão é para contas norte-americanas).

Para configurar o data center:

1. Navegue até o console da Web em `https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`

   ![](assets/chlimage_1-61.png)

1. Dependendo do local do servidor, altere o URI para um dos seguintes:

   * América do Norte: [https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA: [https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC: [https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. Clique em **Salvar**.

## Adicionar componentes do Search &amp; Promote ao Sidekick {#adding-search-promote-components-to-sidekick}

No modo Design, edite um componente **par** para permitir os componentes do Search &amp; Promote no Sidekick. (Consulte a documentação [Componentes](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode) para obter mais informações.)

Para obter informações sobre como usar os componentes, consulte [Adicionar recursos de Search &amp; Promote a uma página da Web](/help/sites-authoring/search-and-promote.md).)

## Especificação do serviço de Search &amp; Promote que suas páginas usam {#specifying-the-search-promote-service-that-your-pages-use}

Configure páginas da Web para que elas usem um serviço de Search &amp; Promote específico. Os componentes do Search &amp; Promote usam automaticamente o serviço de sua página de host.

Quando você define as propriedades do Search &amp; Promote para uma página, todas as páginas secundárias herdam as configurações. Se necessário, é possível configurar páginas secundárias para substituir as configurações herdadas.

>[!NOTE]
>
>A conexão de serviço já deve estar configurada. (Consulte [Configurar a conexão com o Search &amp; Promote](#connection).)

1. Abra a caixa de diálogo **Propriedades da página**. Por exemplo, na página** Sites**, clique com o botão direito do mouse na página e clique em **Propriedades**.
1. Clique na guia **Cloud Services**.
1. Para desativar a herança das configurações de serviços em nuvem de uma página pai, clique no ícone de cadeado ao lado do caminho de herança.

   ![](assets/sandpinheritpadlock.png)

1. Clique em **Adicionar Serviço**, selecione **Search &amp; Promote de Adobe** e clique em **OK**.
1. Selecione a configuração de conexão para sua conta do Search &amp; Promote e clique em **OK**.

## Feed do produto {#product-feed}

A integração de Search &amp; Promote permite:

* use a API eCommerce, independentemente da estrutura do repositório subjacente e da plataforma de comércio.
* aproveite o recurso Conector de índice do Search &amp; Promote para fornecer um feed de produto no formato XML.
* aproveitar o recurso de Controle remoto do Search &amp; Promote para executar solicitações sob demanda ou programadas do feed do produto
* geração de feed para diferentes contas de Search &amp; Promote, configurada como configurações de serviços em nuvem.

Para obter mais informações, leia [Feed do produto](/help/sites-administering/product-feed.md).
