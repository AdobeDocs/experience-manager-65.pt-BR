---
title: AEM Adobe PhoneGap
seo-title: AEM Adobe PhoneGap
description: O AEM se integra ao PhoneGap para que você possa criar aplicativos facilmente usando páginas AEM. Siga esta página para começar a usar o Adobe PhoneGap Enterprise.
seo-description: AEM integrates with PhoneGap so that you can easily create apps using AEM pages. Follow this page to get started with Adobe PhoneGap Enterprise.
uuid: bdd90cda-2489-4763-a90a-9c409d6e68ae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: fbcdea8a-72e9-431b-9c32-dc02d4cdb9c8
exl-id: d989e235-5993-4738-8523-5b9a5f6bf712
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

O AEM se integra ao PhoneGap para que você possa criar aplicativos facilmente usando páginas AEM. O PhoneGap permite que o usuário crie aplicativos de utilitário que permitem que os usuários trabalhem com o conteúdo. A Sincronização de conteúdo permite criar arquivos com versão de páginas para empacotamento com aplicativos.

Normalmente, um ***Administrador AEM*** O é responsável por adicionar um novo aplicativo ao catálogo do AEM Mobile, criando um aplicativo usando o assistente de criação ou importando um aplicativo existente.

Aqui, um ***Autor do AEM*** (ou *Profissional de marketing*) agora pode usar os modelos e componentes prontos para uso para adicionar e editar páginas, arrastar e soltar componentes e adicionar mídia de todos os tipos no DAM, incluindo imagens, vídeos e fragmentos de texto (fragmentos de conteúdo).

O verdadeiro poder do AEM Mobile é que um *experiente* ***Desenvolvedor de AEM*** pode estender e criar modelos e componentes personalizados da Web para habilitar a *Autor do AEM* para criar experiências móveis atraentes e atraentes. Esses modelos e componentes não são apenas otimizados para o mundo do aplicativo móvel, mas também se comunicam com o dispositivo e com o servidor AEM (qualquer servidor remoto) para pontos finais de serviço omnicanal.

>[!NOTE]
>
>Quando a variável *Autor do AEM* acredita que o aplicativo está pronto, primeiro as partes interessadas podem baixá-lo com **[Verificação de Adobe](/help/mobile/phonegap-mobile-quickstart.md)** (disponível na AppStore e na PlayStore) para revisão e aprovação. Depois de receber a luz verde, eles podem lançar esse conteúdo novo ou atualizado diretamente para os usuários por meio do painel de gerenciamento de lançamento de conteúdo do AEM Mobile ContentSync. Uma pessoa pode assumir qualquer número de funções, depende de você e de suas políticas de governança.

## Pré-requisitos {#prerequisites}

O AEM Mobile é apenas um pilar que compõe a plataforma AEM completa.

Antes de trabalhar com o AEM Mobile e seguir as etapas deste guia de introdução, os usuários devem se familiarizar com o AEM e o Centro de controle da AEM Mobile. Consulte:

[Introdução ao AEM](/help/sites-deploying/deploy.md)

[Uma apresentação do AEM Mobile Control Center](/help/mobile/phonegap-authoring-apps.md)

## Links rápidos para autores {#quicklinks-for-authors}

Consulte [Criação para Adobe PhoneGap Enterprise no AEM](/help/mobile/phonegap.md) para saber mais sobre as funções e responsabilidades de um autor.

## QuickLinks para desenvolvedores {#quicklinks-for-developers}

Existem aplicativos de amostra que serão integrados ao AEM Mobile e podem ser personalizados pelo desenvolvedor. Clique em [Desenvolvimento de Adobe PhoneGap Enterprise com AEM](/help/mobile/developing-in-phonegap.md).

Nos capítulos subsequentes, você aprenderá sobre conceitos avançados, como White rotulando seu aplicativo, Localização, Internacionalização, ContentSync, Direcionamento, Analytics e muito mais.

## QuickLinks para administradores {#quicklinks-for-administrators}

Consulte [Administração de conteúdo para o Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md) para configurar e gerenciar seu aplicativo móvel.

>[!NOTE]
>
>Com tecnologias híbridas para dispositivos móveis, você pode criar aplicativos avançados que *executar off-line e on-line* na verdade, com o AEM Mobile, muitos clientes optam por criar aplicativos que verificam quando estão online ou offline e se comportam adequadamente.
