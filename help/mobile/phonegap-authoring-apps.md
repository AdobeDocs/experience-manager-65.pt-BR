---
title: Criação de aplicativos móveis
seo-title: Criação de aplicativos móveis
description: O Painel AEM Mobile permite que você crie, crie e implante seu aplicativo móvel, crie, exclua e edite metadados do aplicativo. Siga esta página para saber mais.
seo-description: O Painel AEM Mobile permite que você crie, crie e implante seu aplicativo móvel, crie, exclua e edite metadados do aplicativo. Siga esta página para saber mais.
uuid: 293b5d29-df7e-42dd-ae64-8c677317e7a5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: abfeea65-102d-4800-abeb-304d61afcc13
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 0%

---


# Criação de aplicativos móveis{#authoring-mobile-applications}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

O Painel AEM Mobile permite que você crie, crie e implante seu aplicativo móvel, crie, exclua e edite metadados do aplicativo. Quando seu aplicativo estiver ativo, você poderá analisar a análise do aplicativo, incluindo o ciclo de vida e as métricas de uso, para melhorar a conversão do cliente e a fidelidade da marca.

Para criar seu aplicativo AEM Mobile, consulte a página [Criação de aplicativos móveis](/help/mobile/building-app-mobile-phonegap.md).

Para configurar seu ambiente e começar, consulte [Administrando AEM para Usar AEM PhoneGap Enterprise](/help/mobile/administer-phonegap.md).

## O Catálogo de Aplicativos AEM Mobile {#the-aem-mobile-apps-catalog}

O [Catálogo de aplicativos AEM Mobile](http://localhost:4502/aem/apps.html/content/phonegap) exibe todos os aplicativos móveis gerenciados no AEM.

Considere este catálogo como a &quot;landing page&quot; para a AEM Mobile, onde os administradores podem start um novo aplicativo AEM Mobile criando com base em um modelo ou fazendo upload de um aplicativo existente já iniciado por um desenvolvedor móvel.

Siga estas etapas para acessar a landing page de catálogo de aplicativos:

1. Navegue até **Navegação** e escolha **Dispositivo Móvel**.

1. Escolha **Aplicativos** para abrir o catálogo de aplicativos.

![Catálogo de aplicativos AEM Mobile](assets/chlimage_1-135.png)

## O Painel do aplicativo AEM Mobile {#the-aem-mobile-app-dashboard}

Selecionar um aplicativo AEM Mobile do catálogo exibirá seu painel. Aqui você pode gerenciar seu aplicativo, estatísticas de visualização, criar, implantar e gerenciar o conteúdo do aplicativo móvel.

Você pode expandir para cada bloco do Painel AEM Mobile para visualização ou editar detalhes clicando em &#39;...&#39; no canto inferior direito.

![Centro de comando de aplicativos AEM Mobile](assets/chlimage_1-136.png)

### O bloco Gerenciar aplicativos {#the-manage-app-tile}

O bloco Gerenciar aplicativo exibe o ícone, o nome, a descrição, as plataformas compatíveis, a página inicial para atualizações URL e informações sobre versões. Você pode detalhar esse bloco para editar e manter a Configuração do aplicativo PhoneGap (config.xml) e preparar seu aplicativo para submissão aos vários armazenamentos de aplicativos para distribuição.

Clique [aqui](/help/mobile/phonegap-app-details-tile.md) para obter detalhes.

![chlimage_1-137](assets/chlimage_1-137.png)

### O mosaico Gerenciar conteúdo da página {#the-manage-page-content-tile}

O conteúdo pode ser criado, atualizado e excluído no AEM Mobile da mesma forma que você faz no AEM Sites. O **Gerenciar bloco de conteúdo da página** exibe o número de páginas do conteúdo gerenciado e da última modificação. É possível detalhar o conteúdo para criar, copiar, mover, excluir e atualizar páginas clicando em cada registro no bloco. Depois que o conteúdo for atualizado, você poderá enviar uma atualização de conteúdo para seus clientes por meio do **Gerenciar blocos de conteúdo.**

![Bloco de conteúdo](assets/chlimage_1-138.png)

### O mosaico Gerenciar pacotes de conteúdo {#the-manage-content-packages-tile}

Depois de adicionar ou modificar seu conteúdo por meio do título Gerenciar conteúdo da página, você poderá enviar essas alterações para seus clientes com uma atualização de versão de conteúdo.

O Pacote de conteúdo permite que o autor do aplicativo AEM gerencie o conteúdo da página no AEM e faça com que sua equipe de desenvolvimento faça alterações no aplicativo PhoneGap Shell (ou seja, estrutura ou infraestrutura do aplicativo) e envie essas alterações para seus clientes rapidamente e sem precisar inscrever um desenvolvedor para reenviar para as várias lojas para distribuição.

O Pacote de conteúdo cria um arquivo ZIP, considerado um Pacote de versão de conteúdo, para cada atualização. Esses pacotes contêm recursos html e páginas html que são geradas durante a renderização do aplicativo e são inteligentes o suficiente para disponibilizar apenas os arquivos que foram modificados desde a última atualização.

A coluna Gerenciar blocos do pacote de conteúdo **Tipo** exibirá o conteúdo do &#39;Aplicativo&#39; para indicar o conteúdo do shell de aplicativos, por exemplo, a estrutura ou a infraestrutura do aplicativo gerenciado por um desenvolvedor ou &#39;Conteúdo&#39; que representa o conteúdo da página gerenciado pelo autor do conteúdo.

O conteúdo pode ser representado como um idioma ou como uma parte específica do aplicativo, onde vários pacotes de versão de conteúdo são consumidos pelo aplicativo. A escolha de como agrupar seu conteúdo foi projetada para ser flexível e totalmente compatível com a forma como você deseja gerenciar o conteúdo do aplicativo.

A coluna **Modificado** indica quando as páginas foram modificadas pela última vez.

A coluna **Preparado** mostra quando a última atualização de conteúdo foi criada. Para criar uma nova atualização de conteúdo e preparar suas alterações, abra qualquer registro no bloco e crie uma nova atualização.

A coluna **Publicado** mostra quando a última atualização de conteúdo foi publicada e disponibilizada para consumo pelos clientes. Para publicar o conteúdo, você deve primeiro preparar esse conteúdo e depois publicar a atualização fazendo drilldown neste bloco e publicando no console de detalhes da Versão de conteúdo.

![Pacote ](assets/chlimage_1-139.png) ![TileContentSync da versão de conteúdo para o shell do aplicativo](do-not-localize/chlimage_1-5.png)

Este ícone representa um pacote de versão de conteúdo para o shell do aplicativo

![](do-not-localize/chlimage_1-6.png)

Esses ícones representam um pacote de versão de conteúdo para o conteúdo do aplicativo

### O mosaico do PhoneGap Build {#the-phonegap-build-tile}

O **PhoneGap Build mosaico** conecta-se com [https://build.phonegap.com](https://build.phonegap.com) para criar e hospedar compilações remotas. Depois de criada, a compilação é disponibilizada como download ou diretamente para seu dispositivo por meio de um código QR.

Como alternativa, você pode baixar a fonte do dispositivo para criar localmente por meio da [CLI do PhoneGap](https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html).

![PhoneGap Build](assets/chlimage_1-140.png)

### O bloco de métricas {#the-metrics-tile}

>[!CAUTION]
>
>O bloco Métricas é exibido somente depois que você configura o serviço de nuvem.
>
>Consulte [Configure seu Cloud Service do Adobe Mobile Services](/help/mobile/configure-adobe-mobile-cloud-service.md) para obter detalhes.

A AEM Mobile integra-se ao Adobe Analytics por meio do SDK do Adobe Mobile Services[ (AMS).](https://www.adobe.com/ca/solutions/digital-marketing/mobile-services/app-sdk.html)

O bloco **Métricas** do Centro de controle exibe as análises de resumo obtidas do AMS para seu aplicativo. Você pode detalhar o painel do Analytics clicando em &#39;...&#39; na parte inferior direita.

![Mosaico de métricas](assets/chlimage_1-141.png)

### O mosaico Gerenciar conteúdo da entidade {#the-manage-entity-content-tile}

O título Gerenciar conteúdo da entidade permite que você adicione e gerencie definições de aplicativos. As definições do aplicativo são uma forma de identificar quais espaços (e outras configurações) são apropriados para o aplicativo. Dessa forma, um novo espaço pode ser adicionado, sem precisar recompilar o aplicativo. A definição do aplicativo é atualizada e incluirá as informações de quaisquer novos espaços.

Clique [aqui](/help/mobile/phonegap-app-definitions.md) para criar e gerenciar as definições do aplicativo.

Você pode detalhar o painel de conteúdo da entidade de gerenciamento clicando em &#39;...&#39; na parte inferior direita.

![chlimage_1-142](assets/chlimage_1-142.png)

#### Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Desenvolvimento para Adobe PhoneGap Enterprise com AEM](/help/mobile/developing-in-phonegap.md)
* [Administração de conteúdo para Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)

