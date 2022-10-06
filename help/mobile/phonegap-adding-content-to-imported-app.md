---
title: O seu aplicativo híbrido está pronto para o AEM Mobile?
seo-title: Is your hybrid app ready for AEM Mobile?
description: Siga esta página para saber mais sobre aplicativos hrybrid. Um aplicativo no AEM geralmente é dividido em duas partes. O "shell" e o "content" e esta página fornecem mais informações sobre esses tópicos.
seo-description: Follow this page to learn about hrybrid apps. An app in AEM is commonly divided into two parts. The 'shell' and 'content' and this page provides more insight on these topics.
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
exl-id: 4625890c-2b76-4c78-88e8-23741bc09f5b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# O seu aplicativo híbrido está pronto para o AEM Mobile?{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Então você importou seu aplicativo Hybrid PhoneGap ou Cordova para AEM, e agora? Provavelmente, você desejará adicionar conteúdo autorável ao seu aplicativo. Para realizar essa tarefa, você precisará de um entendimento geral da estrutura de um aplicativo AEM. Um aplicativo no AEM geralmente é dividido em duas partes. O &quot;shell&quot; e o &quot;content&quot;. O &quot;shell&quot; consiste nas partes estáticas do seu aplicativo; como os arquivos de configuração do PhoneGap, a estrutura do aplicativo e os controles de navegação. O conteúdo do arquivo importado é armazenado como parte do shell. No contexto deste documento, o shell é todo o conteúdo não criado AEM do seu aplicativo Hybrid PhoneGap criado pelo desenvolvedor do aplicativo.

Conteúdo refere-se aos componentes, modelos e páginas criadas que são criadas em AEM criadas pelo Desenvolvedor de AEM. O conteúdo é categorizado como conteúdo do desenvolvedor ou como conteúdo criado. Componentes, designs e modelos de página são considerados conteúdo dev, já que são criados por um desenvolvedor. conteúdo do autor são páginas que foram criadas usando os componentes e modelos. Normalmente, são feitas por um designer ou um profissional de marketing.

Adicionar AEM páginas criadas ao aplicativo híbrido requer coordenação entre o desenvolvedor do aplicativo e o desenvolvedor AEM. Em qualquer lugar do aplicativo em que você deseja adicionar conteúdo criado, o desenvolvedor do aplicativo precisa organizar essas páginas em uma estrutura que possa ser sobreposta no AEM. O desenvolvedor do aplicativo deve ser capaz de fornecer ao desenvolvedor do AEM os caminhos para onde o conteúdo de criação do AEM será adicionado e, em seguida, fornecer uma página de espaço reservado no aplicativo híbrido que será substituído após o desenvolvedor do AEM ter criado o conteúdo da página.

Para facilitar a explicação, estaremos usando o Marketing Cloud AEM: Referência híbrida do AEM Mobile para explicar os conceitos. O aplicativo de Referência híbrida consiste em uma página de boas-vindas com um menu lateral.

![chlimage_1-76](assets/chlimage_1-76.png)

Neste exemplo, vamos criar a página de boas-vindas do aplicativo. Como examinar a fonte [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). Vemos que o desenvolvedor do aplicativo definiu uma página de boas-vindas e forneceu um modelo para a página que é renderizada pelo aplicativo. É aqui que o desenvolvedor do aplicativo e AEM desenvolvedor precisam coordenar. O caminho para o modelo de página de boas-vindas no Aplicativo de referência híbrido é definido como &#39;&#39;content/mobileapps/hybrid-reference-app/en/welcome.template.html&#39;&#39;. Esse caminho é extremamente importante porque o desenvolvedor de AEM criará sua página de boas-vindas no repositório de AEM usando o mesmo caminho.

![chlimage_1-77](assets/chlimage_1-77.png)

É importante que o aplicativo híbrido e o conteúdo criado do AEM usem o mesmo caminho, pois dependemos da capacidade de sobrepor o conteúdo usando a Sincronização de conteúdo para adicionar novas páginas ao aplicativo híbrido. Quando o aplicativo híbrido é importado para o AEM como parte do processo de importação, as configurações de Sincronização de conteúdo são configuradas.

![chlimage_1-78](assets/chlimage_1-78.png)

Ao &quot;Baixar fonte&quot; no painel do aplicativo, esses scripts ContentSync são executados para montar um arquivo do aplicativo híbrido.

![chlimage_1-79](assets/chlimage_1-79.png)

O ContentSync primeiro extrai &quot;shell&quot; do aplicativo, que é onde todo o conteúdo desenvolvido do aplicativo Híbrido é armazenado e, em seguida, extrai o &quot;conteúdo&quot; do aplicativo. Agora, se houver páginas no &quot;shell&quot; que tenham o mesmo caminho que no &quot;conteúdo&quot;, as páginas em &quot;shell&quot; serão (substituídas) pelas páginas em &quot;conteúdo&quot;. Em outras palavras, na amostra do aplicativo de referência híbrido, se criarmos uma página no AEM que tenha o mesmo caminho que &#39;&#39;content/mobileapps/hybrid-reference-app/en/welcome.template.html&#39;&#39; quando o ContentSync for executado, ela sobreporá a página que fazia parte do aplicativo de referência híbrido com o que estiver AEM nesse local. A sobreposição é cuidada pelo ContentSync, portanto, para alguém que esteja usando o aplicativo, as atualizações para o aplicativo com AEM conteúdo criado parecerão ininterruptas e não exigirão uma recriação do aplicativo. Como resultado, ao executar o aplicativo, a página de boas-vindas será exibida da seguinte maneira:

![chlimage_1-80](assets/chlimage_1-80.png)
