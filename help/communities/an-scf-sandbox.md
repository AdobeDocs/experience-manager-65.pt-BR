---
title: Criar uma sandbox SCF
description: Este tutorial é principalmente para desenvolvedores novos no AEM, que estão interessados em usar os componentes SCF. Ele aborda a criação de um site de sandbox SCF
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 89858814-6625-4a56-8359-cc1eca402816
source-git-commit: fd937341e26edd0c3edfced8e862066ebc30f9a3
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Criar uma sandbox SCF  {#create-an-scf-sandbox}

Desde o AEM 6.1 Communities, a maneira mais fácil de criar rapidamente uma sandbox é criar um site da comunidade. Consulte [Introdução ao AEM Communities](getting-started.md).

Outra ferramenta útil para os desenvolvedores é a [Guia de componentes da comunidade](components-guide.md), que permite a exploração e a prototipagem rápida de componentes e recursos do Communities.

O exercício de criar um site pode ser útil para entender a estrutura de um site AEM que pode incluir recursos das Comunidades, além de fornecer páginas simples nas quais explorar o trabalho com a [estrutura da componente social (SCF)](scf.md).

Este tutorial é principalmente para desenvolvedores novos no AEM, que estão interessados em usar os componentes SCF. Ele aborda a criação de um site de sandbox SCF, semelhante ao tutorial para [Como criar um site completo da Internet](../../help/sites-developing/website.md) que focaliza estruturas no site, como navegação, logotipo, pesquisa, barra de ferramentas e listagem de páginas secundárias.

O desenvolvimento ocorre em uma instância do autor, enquanto o teste com o site é melhor em uma instância de publicação.

As etapas deste tutorial são:

* [Configurar estrutura do site](setup-website.md)
* [Aplicativo de sandbox inicial](initial-app.md)
* [Conteúdo inicial da sandbox](initial-content.md)
* [Desenvolver aplicativo de sandbox](develop-app.md)
* [Adicionar Clientlibs](add-clientlibs.md)
* [Desenvolver conteúdo da sandbox](develop-content.md)

>[!CAUTION]
>
>Este tutorial não cria um site da comunidade com a funcionalidade criada usando o [Console de sites das comunidades](sites-console.md). Por exemplo, este tutorial não descreve como configurar o login, o autorregistro, [login social](social-login.md), mensagens, perfis e assim por diante.
>
>Se um site de comunidade simples for preferido, siga as [Criar uma página de exemplo](create-sample-page.md) tutorial.

## Pré-requisitos {#prerequisites}

Este tutorial pressupõe que você tenha um autor de AEM e uma instância de publicação AEM instalada com o [versão mais recente](deploy-communities.md#latest-releases) das Comunidades.

A seguir estão alguns links úteis para desenvolvedores novos na plataforma AEM:

* [Introdução](../../help/sites-deploying/deploy.md#getting-started): para implantar instâncias do AEM.

   * [Noções básicas](../../help/sites-developing/the-basics.md): para desenvolvedores de sites e recursos.
   * [Primeiras etapas para autores](../../help/sites-authoring/first-steps.md): para criação de conteúdo de página.

## Uso do ambiente de desenvolvimento do CRXDE Lite {#using-crxde-lite-development-environment}

Os desenvolvedores de AEM passam grande parte do tempo no [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) ambiente de desenvolvimento em uma instância do autor. O CRXDE Lite fornece um acesso menos restrito ao repositório CRX. As ferramentas da interface clássica e os consoles de interface habilitados para toque fornecem acesso mais estruturado a partes específicas do repositório CRX.

Depois de fazer logon com privilégios administrativos, há várias maneiras de acessar o CRXDE Lite:

1. Na navegação global, selecione navegação **[!UICONTROL Ferramentas > CRXDE Lite]**.

   ![crxde-lite](assets/tools-crxde.png)

2. No [página de boas-vindas da interface clássica](http://localhost:4502/welcome.html), role para baixo e clique em **[!UICONTROL CRXDE Lite]** no painel direito.

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. Navegue diretamente para `CRXDE Lite`: `<server>:<port>/crx/de`

   Por exemplo, em uma instância de autor local: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

Para trabalhar com o CRXDE Lite, é necessário fazer logon com privilégios de desenvolvedor ou administrador. Para a instância localhost padrão, você pode fazer logon com

* `username: admin`
* `password: admin`


Esse logon expira e você deve fazer logon novamente periodicamente usando o menu suspenso na extremidade direita da barra de ferramentas do CRXDE Lite.

Se não estiver conectado, você não poderá navegar no repositório JCR nem executar operações de edição/salvamento.

***Na dúvida, faça o logon novamente!***

![fazer logon novamente](assets/relogin.png)
