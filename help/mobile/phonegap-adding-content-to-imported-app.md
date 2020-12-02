---
title: Seu aplicativo híbrido está pronto para AEM Mobile?
seo-title: Seu aplicativo híbrido está pronto para AEM Mobile?
description: Siga esta página para saber mais sobre aplicativos híbridos. Um aplicativo em AEM é comumente dividido em duas partes. O 'shell' e o 'content' e esta página fornecem mais informações sobre estes tópicos.
seo-description: Siga esta página para saber mais sobre aplicativos híbridos. Um aplicativo em AEM é comumente dividido em duas partes. O 'shell' e o 'content' e esta página fornecem mais informações sobre estes tópicos.
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 0%

---


# Seu aplicativo híbrido está pronto para AEM Mobile?{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Então você importou seu aplicativo Hybrid PhoneGap ou Cordova para AEM, e agora? Provavelmente, você desejará adicionar conteúdo autorável ao seu aplicativo. Para realizar essa tarefa, você precisará de um entendimento geral da estrutura de um aplicativo AEM. Um aplicativo em AEM é comumente dividido em duas partes. O &#39;shell&#39; e o &#39;content&#39;. A &#39;shell&#39; é composta das partes estáticas do seu aplicativo; como os arquivos de configuração do PhoneGap, a estrutura do aplicativo e os controles de navegação. O conteúdo do arquivo importado é armazenado como parte do shell. No contexto desse documento, o shell é todo o conteúdo não AEM criado do aplicativo Hybrid PhoneGap criado pelo desenvolvedor do aplicativo.

Conteúdo refere-se aos componentes, modelos e páginas criadas que são criados em AEM criados pelo desenvolvedor AEM. O conteúdo é categorizado como conteúdo de desenvolvedor ou como conteúdo de autoria. Os componentes, designs e modelos de página são considerados como conteúdo dev, já que são criados por um desenvolvedor. author-content são páginas que foram criadas usando os componentes e modelos. Normalmente, são feitas por um designer ou um comerciante.

A adição de páginas de AEM criadas ao aplicativo Híbrido requer coordenação entre o desenvolvedor do aplicativo e o desenvolvedor AEM. Em qualquer lugar no aplicativo em que você deseja adicionar conteúdo de criação, o desenvolvedor do aplicativo precisa organizar essas páginas em uma estrutura que possa ser sobreposta no AEM. O desenvolvedor do aplicativo deve ser capaz de fornecer ao desenvolvedor do AEM os caminhos para onde o conteúdo de autoria do AEM será adicionado e, em seguida, fornecer uma página de espaço reservado no aplicativo Híbrido que será substituída depois que o desenvolvedor do AEM tiver criado o conteúdo da página.

Para tornar a explicação mais fácil de seguir, usaremos o Marketing Cloud AEM: Referência híbrida da AEM Mobile para explicar os conceitos. O aplicativo de referência híbrida consiste em uma página de boas-vindas com um menu lateral.

![chlimage_1-76](assets/chlimage_1-76.png)

Neste exemplo, vamos criar a página de boas-vindas do aplicativo. Observando a fonte [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). Vemos que o desenvolvedor do aplicativo definiu uma página de boas-vindas e forneceu um modelo para a página que é renderizada pelo aplicativo. É aqui que o desenvolvedor do aplicativo e AEM desenvolvedor precisam coordenar. O caminho para o modelo de página de boas-vindas no Aplicativo de referência híbrido é definido como &#39;&#39;content/mobileapps/hybrid-reference-app/en/welcome.template.html&#39;&#39;. Esse caminho é extremamente importante porque o desenvolvedor AEM criará sua página de boas-vindas no repositório AEM usando o mesmo caminho.

![chlimage_1-77](assets/chlimage_1-77.png)

É importante que o aplicativo híbrido e o conteúdo AEM criado usem o mesmo caminho, pois dependemos da capacidade de sobrepor o conteúdo usando a Sincronização de conteúdo para adicionar novas páginas ao aplicativo híbrido. Quando o aplicativo híbrido é importado para AEM como parte do processo de importação, as configurações de Sincronização de conteúdo são configuradas.

![chlimage_1-78](assets/chlimage_1-78.png)

Quando você &#39;Baixar origem&#39; do painel do aplicativo, esses scripts ContentSync serão executados para montar um arquivo do aplicativo híbrido.

![chlimage_1-79](assets/chlimage_1-79.png)

O ContentSync primeiro obtém &quot;shell&quot; do aplicativo, que é o local onde todo o conteúdo desenvolvido do aplicativo Híbrido é armazenado e, em seguida, puxa o &quot;conteúdo&quot; do aplicativo. Agora, se houver páginas no &#39;shell&#39; que tenham o mesmo caminho que no &#39;conteúdo&#39;, as páginas em &#39;shell&#39; serão (substituídas) pelas páginas em &#39;content&#39;. Em outras palavras, na amostra do aplicativo de referência híbrido, se criarmos uma página no AEM que tenha o mesmo caminho que &#39;&#39;content/mobileapps/hybrid-reference-app/en/welcome.template.html&#39;&#39; quando o ContentSync for executado, ela sobreporá a página que fazia parte do aplicativo de referência híbrido com o que está no AEM desse local. A sobreposição é cuidada pelo ContentSync, de modo que para alguém que esteja usando o aplicativo, as atualizações para o aplicativo com conteúdo criado AEM parecerão perfeitas e não precisarão de uma recriação do aplicativo. Como resultado, quando você executa o aplicativo, a página de boas-vindas será exibida da seguinte maneira:

![chlimage_1-80](assets/chlimage_1-80.png)
