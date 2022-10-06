---
title: Criar uma sandbox SCF
seo-title: Create An SCF Sandbox
description: Este tutorial é principalmente para desenvolvedores, novos em AEM, que estão interessados em usar componentes SCF.  Ele aborda a criação de um site de sandbox do SCF
seo-description: This tutorial is primarily for developers, new to AEM, who are interested in using SCF components.  It walks through the creation of An SCF Sandbox site
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
exl-id: 89858814-6625-4a56-8359-cc1eca402816
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---

# Criar uma sandbox SCF  {#create-an-scf-sandbox}


A partir AEM Comunidades 6.1, a maneira mais fácil de criar rapidamente uma sandbox é criar um site da comunidade. Consulte [Introdução ao AEM Communities](getting-started.md).

Outra ferramenta útil para desenvolvedores é a [Guia de componentes da comunidade](components-guide.md), que permite a exploração e o protótipo rápido de componentes e recursos do Communities.

O exercício de criar um site pode ser útil para entender a estrutura de um site AEM que pode incluir recursos das Comunidades, além de fornecer páginas simples nas quais explorar o trabalho com a [quadro de componentes sociais (SCF)](scf.md).

Este tutorial é principalmente para desenvolvedores, novos em AEM, que estão interessados em usar componentes SCF. Ele aborda a criação de um site Sandbox de SCF, semelhante ao tutorial para [Como criar um site da Internet em destaque](../../help/sites-developing/website.md) que se concentra nas estruturas do site, como navegação, logotipo, pesquisa, barra de ferramentas e listagem de páginas filhas.

O desenvolvimento ocorre em uma instância do autor, enquanto o experimento com o site é melhor em uma instância de publicação.

As etapas neste tutorial são:

* [Configurar estrutura do site](setup-website.md)
* [Aplicativo de sandbox inicial](initial-app.md)
* [Conteúdo inicial da sandbox](initial-content.md)
* [Desenvolver aplicativo de sandbox](develop-app.md)
* [Adicionar Clientlibs](add-clientlibs.md)
* [Desenvolver conteúdo do Sandbox](develop-content.md)

>[!CAUTION]
>
>Este tutorial não cria um site da comunidade com a funcionalidade criada usando o [Console de sites das comunidades](sites-console.md). Por exemplo, este tutorial não descreve como configurar o logon, o registro automático, [logon social](social-login.md), mensagens, perfis e assim por diante.
>
>Se preferir um site de comunidade simples, siga as [Criar uma página de exemplo](create-sample-page.md) tutorial.

## Pré-requisitos {#prerequisites}

Este tutorial supõe que você tenha um autor de AEM e uma instância de publicação de AEM instalada que tenha o [versão mais recente](deploy-communities.md#latest-releases) das Comunidades.

A seguir estão alguns links úteis para desenvolvedores novos na plataforma AEM:

* [Introdução](../../help/sites-deploying/deploy.md#getting-started): para implantar instâncias de AEM.

   * [Noções básicas](../../help/sites-developing/the-basics.md): para desenvolvedores de sites e recursos.
   * [Primeiros passos para autores](../../help/sites-authoring/first-steps.md): para criação de conteúdo de página.

## Usar o ambiente de desenvolvimento do CRXDE Lite {#using-crxde-lite-development-environment}

Os desenvolvedores do AEM passam a maior parte do tempo na [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) ambiente de desenvolvimento em uma instância do autor. O CRXDE Lite fornece um acesso menos restrito ao repositório CRX. As ferramentas da interface clássica e os consoles de interface habilitada para toque fornecem acesso mais estruturado a partes específicas do repositório CRX.

Depois de fazer logon com privilégios administrativos, há várias maneiras de acessar o CRXDE Lite:

1. Na navegação global, selecione navegação **[!UICONTROL Ferramentas > CRXDE Lite]**.

   ![crxde-lite](assets/tools-crxde.png)

2. No [página de boas-vindas da interface clássica](http://localhost:4502/welcome.html), role para baixo e clique em **[!UICONTROL CRXDE Lite]** no painel direito.

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. Navegue diretamente para `CRXDE Lite`: `<server>:<port>/crx/de`

   Por exemplo, em uma instância de autor local: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

Para trabalhar com o CRXDE Lite, você deve fazer logon com privilégios de desenvolvedor ou de administrador. Para a instância padrão do host local, você pode fazer logon com a

* `username: admin`
* `password: admin`


**Esteja ciente** que esse logon atingirá o tempo limite e você precisará fazer logon novamente periodicamente usando a opção suspensa na extremidade direita da barra de ferramentas do CRXDe Lite.

Se não estiver conectado, você não poderá navegar pelo repositório JCR ou executar operações de edição/salvamento.

***Em caso de dúvida, faça logon novamente!***

![fazer logon novamente](assets/relogin.png)
