---
title: Seu aplicativo híbrido está pronto para o AEM Mobile?
description: Saiba mais sobre aplicativos híbridos. Um aplicativo no Experience Manager geralmente é dividido em duas partes. O "shell" e o "conteúdo" e esta página fornecem mais informações sobre esses tópicos.
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
exl-id: 4625890c-2b76-4c78-88e8-23741bc09f5b
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%

---

# Seu aplicativo híbrido está pronto para o Adobe Experience Manager Mobile?{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Então você importou seu aplicativo híbrido PhoneGap ou Cordova para AEM, agora o que? Provavelmente você deseja adicionar conteúdo autorável ao seu aplicativo. Para realizar essa tarefa, você precisa de uma compreensão geral da estrutura de um aplicativo AEM. Um aplicativo no AEM geralmente é dividido em duas partes. O &quot;shell&quot; e o &quot;conteúdo&quot;. A &quot;shell&quot; compreende as partes estáticas do aplicativo; como os arquivos de configuração do PhoneGap, a estrutura do aplicativo e os controles de navegação. O conteúdo do arquivo que você importou é armazenado como parte do shell. No contexto deste documento, o shell é todo o conteúdo não-AEM criado do seu aplicativo híbrido PhoneGap criado pelo desenvolvedor do aplicativo.

Conteúdo refere-se aos componentes, modelos e páginas criadas no AEM criado pelo AEM Developer. O conteúdo é categorizado como conteúdo do desenvolvedor ou como conteúdo criado. Componentes, designs e modelos de página são considerados conteúdo de desenvolvimento, pois são criados por um desenvolvedor. Conteúdos do autor são páginas que foram criadas usando os componentes e modelos. Normalmente, essas páginas são feitas por um Designer ou um Profissional de marketing.

Adicionar páginas de AEM criadas ao seu aplicativo híbrido requer coordenação entre o desenvolvedor do aplicativo e o desenvolvedor do AEM. Em qualquer lugar no aplicativo onde você deseja adicionar conteúdo criado, o desenvolvedor do aplicativo deve organizar essas páginas em uma estrutura que pode ser sobreposta em Experience Manager. O desenvolvedor do aplicativo deve ser capaz de fornecer ao desenvolvedor de Experience Manager os caminhos para onde o conteúdo criado no Experience Manager foi adicionado. Em seguida, forneça uma página de espaço reservado no aplicativo híbrido que será substituída depois que o desenvolvedor de Experience Manager criar o conteúdo da página.

Para facilitar a explicação, o Experience Cloud AEM está sendo usado: AEM Mobile Hybrid Reference para explicar os conceitos. O aplicativo de Referência híbrida consiste em uma página de boas-vindas com um menu lateral.

![chlimage_1-76](assets/chlimage_1-76.png)

Neste exemplo, a página de boas-vindas do aplicativo será criada. Olhando para a origem [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). Observe que o desenvolvedor do aplicativo definiu uma página de boas-vindas e forneceu um modelo para a página que é renderizada pelo aplicativo. Esta página é onde o desenvolvedor do aplicativo e o desenvolvedor de AEM devem se coordenar. O caminho para o modelo da página de boas-vindas no aplicativo de referência híbrido é definido como &#39;&#39;content/mobileapps/hybrid-reference-app/en/welcome.template.html&#39;&#39;. Esse caminho é importante porque o desenvolvedor do AEM criará sua página de boas-vindas no repositório AEM usando o mesmo caminho.

![chlimage_1-77](assets/chlimage_1-77.png)

É importante que o aplicativo híbrido e o conteúdo criado pelo AEM usem o mesmo caminho, pois ele depende da capacidade de sobrepor conteúdo usando a Sincronização de conteúdo para adicionar novas páginas ao aplicativo híbrido. Quando o aplicativo híbrido é importado para o AEM, como parte do processo de importação, as configurações de sincronização de conteúdo são definidas.

![chlimage_1-78](assets/chlimage_1-78.png)

Quando você faz o &quot;Download de origem&quot; no painel do aplicativo, esses scripts do ContentSync são executados para reunir um arquivo do aplicativo híbrido.

![chlimage_1-79](assets/chlimage_1-79.png)

Primeiro, o ContentSync extrai o &quot;shell&quot; do aplicativo, que é onde todo o conteúdo desenvolvido pelo aplicativo híbrido é armazenado. Em seguida, ele extrai o &quot;conteúdo&quot; do aplicativo. Agora, se houver páginas no &quot;shell&quot; com o mesmo caminho de &quot;conteúdo&quot;, as páginas em &quot;shell&quot; serão (substituídas) pelas páginas em &quot;conteúdo&quot;. Portanto, na amostra do aplicativo de referência híbrida, se uma página for criada no AEM que tenha o mesmo caminho que &#39;&#39;content/mobileapps/hybrid-reference-app/en/welcome.template.html&#39;&#39;, quando o ContentSync for executado, ela sobreporá a página que fazia parte do aplicativo de referência híbrida. Ele se sobrepõe a qualquer AEM naquele local. A sobreposição é resolvida pelo ContentSync, portanto, para alguém que estiver usando o aplicativo, as atualizações para o aplicativo com conteúdo criado por AEM parecem perfeitas e não exigem uma recriação do aplicativo. Como resultado, quando você executa o aplicativo, a página de boas-vindas é exibida da seguinte maneira:

![chlimage_1-80](assets/chlimage_1-80.png)
