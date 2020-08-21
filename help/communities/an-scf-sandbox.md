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



# Criar uma caixa de proteção SCF  {#create-an-scf-sandbox}


Desde AEM Comunidades 6.1, a maneira mais fácil de criar rapidamente uma caixa de proteção é criar um site da comunidade. See [Getting Started with AEM Communities](getting-started.md).

Outra ferramenta útil para desenvolvedores é o guia [Componentes da](components-guide.md)comunidade, que permite a exploração e o protótipo rápido de componentes e recursos das Comunidades.

O exercício de criação de um sítio web pode ser útil para compreender a estrutura de um sítio web AEM que pode incluir os elementos das Comunidades, fornecendo igualmente páginas simples sobre as quais explorar o trabalho com o quadro de componentes [sociais (SCF)](scf.md).

Este tutorial destina-se principalmente a desenvolvedores, novos AEM, interessados em usar componentes SCF. Ele percorre a criação de um site da Caixa de proteção do SCF, semelhante ao tutorial [Como criar um site](../../help/sites-developing/website.md) da Internet com recursos completos que foca nas estruturas do site, como navegação, logotipo, pesquisa, barra de ferramentas e listagem de páginas secundárias.

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
>Este tutorial não cria um site da comunidade com a funcionalidade criada usando o console [Sites de](sites-console.md)comunidades. Por exemplo, este tutorial não descreve como configurar o logon, o autoregistro, o logon [](social-login.md)social, as mensagens, os perfis e assim por diante.
>
>Se um site de comunidade simples for o preferido, siga o tutorial [Criar uma página](create-sample-page.md) de amostra.

## Pré-requisitos {#prerequisites}

Este tutorial supõe que você tenha uma instância AEM autor e uma instância de publicação AEM instalada que tenha a versão [](deploy-communities.md#latest-releases) mais recente das Comunidades.

Veja a seguir alguns links úteis para desenvolvedores novos à plataforma AEM:

* [Introdução](../../help/sites-deploying/deploy.md#getting-started): para implantar instâncias AEM.

   * [Noções básicas](../../help/sites-developing/the-basics.md): para desenvolvedores de sites e recursos.
   * [Primeiros passos para autores](../../help/sites-authoring/first-steps.md): para criar conteúdo de página.

## Usando o Ambiente de desenvolvimento de CRXDE Lite {#using-crxde-lite-development-environment}

AEM desenvolvedores passam boa parte do seu tempo no ambiente de desenvolvimento do [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) em uma instância do autor. O CRXDE Lite fornece um acesso menos restrito ao repositório CRX. As ferramentas de interface clássica e os consoles de interface habilitada para toque fornecem acesso mais estruturado a partes específicas do repositório CRX.

Depois de fazer logon com privilégios administrativos, há várias maneiras de acessar o CRXDE Lite:

1. Na navegação global, selecione **[!UICONTROL Ferramentas de navegação > CRXDE Lite]**.

   ![crxde-lite](assets/tools-crxde.png)

2. Na página [de boas-vindas da interface](http://localhost:4502/welcome.html)clássica, role para baixo e clique em **[!UICONTROL CRXDE Lite]** no painel direito.

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. Navegue diretamente para `CRXDE Lite`: `<server>:<port>/crx/de`

   Por exemplo, em uma instância de autor local: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

Para trabalhar com o CRXDE Lite, você deve fazer logon com privilégios de desenvolvedor ou administrador. Para a instância padrão localhost, você pode fazer logon com

* `username: admin`
* `password: admin`


**Esteja ciente** de que esse logon atingirá o tempo limite e que você precisará fazer login novamente periodicamente usando o menu suspenso na extremidade direita da barra de ferramentas CRXDe Lite.

Se não estiver conectado, você não poderá navegar no repositório JCR nem executar operações de edição/salvamento.

***Na dúvida, faça login novamente!***

![relogin](assets/relogin.png)
