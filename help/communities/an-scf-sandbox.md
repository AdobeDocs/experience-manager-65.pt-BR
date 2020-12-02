---
title: Criar uma caixa de proteção SCF
seo-title: Criar uma caixa de proteção SCF
description: Este tutorial destina-se principalmente a desenvolvedores, novos AEM, interessados em usar componentes SCF.  Ele percorre a criação de um site de segurança do SCF
seo-description: Este tutorial destina-se principalmente a desenvolvedores, novos AEM, interessados em usar componentes SCF.  Ele percorre a criação de um site de segurança do SCF
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
translation-type: tm+mt
source-git-commit: 548e19b0fc76ede8685ea938ed871fbdc8c3858f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---



# Criar uma caixa de proteção SCF {#create-an-scf-sandbox}


Desde AEM Comunidades 6.1, a maneira mais fácil de criar rapidamente uma caixa de proteção é criar um site da comunidade. Consulte [Introdução ao AEM Communities](getting-started.md).

Outra ferramenta útil para desenvolvedores é o [Guia de componentes da comunidade](components-guide.md), que permite a exploração e o protótipo rápido de componentes e recursos das Comunidades.

O exercício de criar um site pode ser útil para entender a estrutura de um site AEM que pode incluir recursos das Comunidades, além de fornecer páginas simples nas quais explorar o trabalho com a [estrutura de componentes sociais (SCF)](scf.md).

Este tutorial destina-se principalmente a desenvolvedores, novos AEM, interessados em usar componentes SCF. Ele percorre a criação de um site da Caixa de proteção SCF, semelhante ao tutorial para [Como criar um site da Internet com recursos completos](../../help/sites-developing/website.md) que foca nas estruturas do site, como navegação, logotipo, pesquisa, barra de ferramentas e listagem de páginas filhas.

O desenvolvimento ocorre em uma instância do autor, enquanto o teste com o site é melhor em uma instância de publicação.

As etapas neste tutorial são:

* [Configurar estrutura do site](setup-website.md)
* [Aplicativo Sandbox Inicial](initial-app.md)
* [Conteúdo inicial do sandbox](initial-content.md)
* [Desenvolver aplicativo Sandbox](develop-app.md)
* [Adicionar Clientlibs](add-clientlibs.md)
* [Desenvolver conteúdo do Sandbox](develop-content.md)

>[!CAUTION]
>
>Este tutorial não cria um site da comunidade com a funcionalidade criada usando o console [Communities Sites](sites-console.md). Por exemplo, este tutorial não descreve como configurar o logon, o autoregistro, [login social](social-login.md), as mensagens, os perfis e assim por diante.
>
>Se um site de comunidade simples for o preferido, siga o tutorial [Criar uma página de amostra](create-sample-page.md).

## Pré-requisitos {#prerequisites}

Este tutorial supõe que você tenha um autor AEM e uma instância de publicação AEM instalada que tenha a [versão mais recente](deploy-communities.md#latest-releases) das Comunidades.

Veja a seguir alguns links úteis para desenvolvedores novos à plataforma AEM:

* [Introdução](../../help/sites-deploying/deploy.md#getting-started): para implantar instâncias AEM.

   * [Noções básicas](../../help/sites-developing/the-basics.md): para desenvolvedores de sites e recursos.
   * [Primeiros passos para autores](../../help/sites-authoring/first-steps.md): para criar conteúdo de página.

## Usando o Ambiente de desenvolvimento de CRXDE Lite {#using-crxde-lite-development-environment}

AEM desenvolvedores passam boa parte do seu tempo no ambiente de desenvolvimento [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) em uma instância do autor. O CRXDE Lite fornece um acesso menos restrito ao repositório CRX. As ferramentas de interface clássica e os consoles de interface habilitada para toque fornecem acesso mais estruturado a partes específicas do repositório CRX.

Depois de fazer logon com privilégios administrativos, há várias maneiras de acessar o CRXDE Lite:

1. Na navegação global, selecione navigation **[!UICONTROL Tools > CRXDE Lite]**.

   ![crxde-lite](assets/tools-crxde.png)

2. Na página de boas-vindas [interface clássica](http://localhost:4502/welcome.html), role para baixo e clique em **[!UICONTROL CRXDE Lite]** no painel direito.

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. Navegue diretamente para `CRXDE Lite`: `<server>:<port>/crx/de`

   Por exemplo, em uma instância de autor local: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

Para trabalhar com o CRXDE Lite, você deve fazer logon com privilégios de desenvolvedor ou administrador. Para a instância padrão localhost, você pode fazer logon com

* `username: admin`
* `password: admin`


**Esteja ciente de** que esse logon atingirá o tempo limite e que você precisará fazer login novamente periodicamente usando a lista suspensa na extremidade direita da barra de ferramentas CRXDe Lite.

Se não estiver conectado, você não poderá navegar no repositório JCR nem executar operações de edição/salvamento.

***Na dúvida, faça login novamente!***

![relogin](assets/relogin.png)
