---
title: Criação de aplicativos móveis
seo-title: Authoring Mobile Applications
description: O Painel do AEM Mobile permite criar, construir e implantar o aplicativo móvel, criar, excluir e editar metadados do aplicativo. Siga esta página para saber mais.
seo-description: he AEM Mobile Dashboard allows you to create, build and deploy your mobile application, create, delete and edit application metadata. Follow this page to learn more.
uuid: 293b5d29-df7e-42dd-ae64-8c677317e7a5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: abfeea65-102d-4800-abeb-304d61afcc13
exl-id: 073daff7-0c1d-4715-bfd4-3e2336e4cb88
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 0%

---

# Criação de aplicativos móveis{#authoring-mobile-applications}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

O Painel do AEM Mobile permite criar, construir e implantar o aplicativo móvel, criar, excluir e editar metadados do aplicativo. Assim que o aplicativo estiver ativo, você poderá analisar as análises do aplicativo, incluindo as métricas de ciclo de vida e uso, para melhorar a conversão do cliente e a fidelidade à marca.

Para criar seu aplicativo AEM Mobile, consulte [Desenvolvimento de aplicativos móveis](/help/mobile/building-app-mobile-phonegap.md) página.

Para configurar seu ambiente e começar, consulte [Administração do AEM para usar AEM PhoneGap Enterprise](/help/mobile/administer-phonegap.md).

## O catálogo de aplicativos do AEM Mobile {#the-aem-mobile-apps-catalog}

A variável [Catálogo de aplicativos AEM Mobile](http://localhost:4502/aem/apps.html/content/phonegap) exibe todo o seu aplicativo móvel gerenciado no AEM.

Pense nesse catálogo como a &quot;página de aterrissagem&quot; do AEM Mobile, em que os administradores podem iniciar um novo aplicativo do AEM Mobile criando com base em um modelo ou fazendo upload de um aplicativo existente já iniciado por um desenvolvedor de dispositivos móveis.

Siga estas etapas para acessar a página de aterrissagem do catálogo de aplicativos:

1. Navegue até **Navegação** e escolha **Dispositivo móvel**.

1. Escolher **Aplicativos** para abrir o catálogo de aplicativos.

![Catálogo de aplicativos AEM Mobile](assets/chlimage_1-135.png)

## O painel do aplicativo AEM Mobile {#the-aem-mobile-app-dashboard}

Selecionar um aplicativo AEM Mobile no catálogo exibe seu painel. Aqui você pode gerenciar o aplicativo, exibir estatísticas, criar, implantar e gerenciar o conteúdo do aplicativo móvel.

É possível expandir cada bloco no Painel do AEM Mobile para exibir ou editar detalhes clicando em &quot;...&quot; no canto inferior direito.

![Centro de comando dos aplicativos AEM Mobile](assets/chlimage_1-136.png)

### O mosaico Gerenciar aplicativo {#the-manage-app-tile}

O Bloco Gerenciar aplicativo exibe o ícone do aplicativo, nome, descrição, plataformas compatíveis, call home para atualizações de URL e informações de versão. Você pode detalhar este bloco para editar e manter a Configuração do aplicativo PhoneGap (config.xml) e preparar seu aplicativo para envio às várias lojas de aplicativos para distribuição.

Clique em [aqui](/help/mobile/phonegap-app-details-tile.md) para obter detalhes.

![chlimage_1-137](assets/chlimage_1-137.png)

### O mosaico Gerenciar conteúdo da página {#the-manage-page-content-tile}

O conteúdo pode ser criado, atualizado e excluído no AEM Mobile da mesma maneira que você faz no AEM Sites. A variável **Gerenciar mosaico de conteúdo da página** exibe o número de páginas de conteúdo gerenciado e a última modificação. Você pode detalhar o conteúdo para criar, copiar, mover, excluir e atualizar páginas clicando em cada registro no bloco. Depois que o conteúdo for atualizado, você poderá enviar uma atualização de conteúdo para seus clientes por meio do **Gerenciar Bloco De Pacotes De Conteúdo.**

![Mosaico de conteúdo](assets/chlimage_1-138.png)

### O Bloco Gerenciar Pacotes De Conteúdo {#the-manage-content-packages-tile}

Depois de adicionar ou modificar o conteúdo por meio do Bloco Gerenciar conteúdo da página, você pode enviar essas alterações para os clientes com uma atualização de Versão de conteúdo.

O pacote de conteúdo permite que o autor do aplicativo AEM gerencie o conteúdo da página no AEM e solicite que sua equipe de desenvolvimento faça alterações no aplicativo PhoneGap Shell (ou seja, estrutura ou infraestrutura do aplicativo) e, em seguida, envie essas alterações para seus clientes rapidamente e sem precisar solicitar que um desenvolvedor envie novamente para as várias lojas para distribuição.

O Pacote de conteúdo cria um arquivo ZIP, considerado um Pacote de versão de conteúdo, para cada atualização. Esses pacotes contêm recursos html e páginas html que são gerados durante a renderização do aplicativo e são inteligentes o suficiente para empacotar apenas os arquivos que foram modificados desde a última atualização.

O bloco do Gerenciar pacote do conteúdo **Tipo** A coluna exibe &quot;Aplicativo&quot; para indicar o conteúdo do Shell do aplicativo, por exemplo, a estrutura ou a infraestrutura do aplicativo gerenciado por um desenvolvedor ou &quot;Conteúdo&quot;, que representa o conteúdo da página gerenciado pelo autor de conteúdo.

O conteúdo pode ser representado como um idioma ou como uma parte específica do aplicativo, onde vários pacotes de versão de conteúdo são consumidos pelo aplicativo. A escolha de como você agrupa seu conteúdo é flexível e depende totalmente de como você deseja gerenciar o conteúdo de seu aplicativo.

A variável **Modificado** indica quando as páginas foram modificadas mais recentemente.

A variável **Preparado** mostra quando a última atualização de conteúdo foi criada. Para criar uma atualização de conteúdo e preparar suas alterações, abra qualquer registro no bloco e crie uma atualização.

A variável **Publicado** A coluna mostra quando a última atualização de conteúdo foi publicada e disponibilizada para consumo pelos clientes. Para publicar conteúdo, primeiro prepare esse conteúdo e, em seguida, publique a atualização fazendo drill-down nesse bloco e publicando no console Detalhes da versão do conteúdo.

![Bloco de versão de conteúdo](assets/chlimage_1-139.png) ![Pacote ContentSync para o shell do aplicativo](do-not-localize/chlimage_1-5.png)

Este ícone representa um pacote de Versão de conteúdo para o shell do aplicativo

![](do-not-localize/chlimage_1-6.png)

Esses ícones representam um pacote de Versão de conteúdo para conteúdo do aplicativo

### O mosaico do PhoneGap Build {#the-phonegap-build-tile}

A variável **Mosaico de PhoneGap Build** conecta-se com [https://build.phonegap.com](https://build.phonegap.com) para criar e hospedar builds remotos. Depois de criada, a build é disponibilizada como download ou diretamente no seu dispositivo por meio de um código QR.

Como alternativa, baixe a origem do dispositivo para criar localmente por meio da [CLI do PhoneGap](https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html).

![Mosaico de PhoneGap Build](assets/chlimage_1-140.png)

### O mosaico de métricas {#the-metrics-tile}

>[!CAUTION]
>
>O bloco Métricas é exibido somente após a configuração do serviço na nuvem.
>
>Consulte [Configurar o Cloud Service do Adobe Mobile Services](/help/mobile/configure-adobe-mobile-cloud-service.md) para obter detalhes.

O AEM Mobile integra-se ao Adobe Analytics por meio de [SDK do Adobe Mobile Services](https://experienceleague.adobe.com/docs/mobile.html?lang=en) (AMS) (em inglês).

Centro de controle **Mosaico de métricas** exibe o resumo de análise extraído do AMS para o seu aplicativo. Você pode detalhar o painel do Analytics clicando em &quot;...&quot; na parte inferior direita.

![Mosaico de métricas](assets/chlimage_1-141.png)

### O Bloco Gerenciar Conteúdo da Entidade {#the-manage-entity-content-tile}

O Bloco Gerenciar conteúdo da entidade permite adicionar e gerenciar definições de aplicativos. As definições de aplicativo são uma maneira de identificar quais espaços (e outras configurações) são apropriados para o aplicativo. Dessa forma, um novo espaço pode ser adicionado sem precisar recompilar o aplicativo. A definição do aplicativo é atualizada e inclui as informações de todos os novos espaços.

Clique em [aqui](/help/mobile/phonegap-app-definitions.md) para criar e gerenciar as definições do aplicativo.

Você pode detalhar o painel de conteúdo gerenciar entidade clicando em &quot;...&quot; na parte inferior direita.

![chlimage_1-142](assets/chlimage_1-142.png)

#### Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Desenvolvimento do Adobe PhoneGap Enterprise com AEM](/help/mobile/developing-in-phonegap.md)
* [Administração de conteúdo para o Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)
