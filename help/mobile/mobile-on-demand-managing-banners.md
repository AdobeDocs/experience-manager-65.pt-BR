---
title: Gerenciamento de banners
seo-title: Managing Banners
description: Os banners geralmente representam links promocionais gráficos. Siga esta página para saber mais.
seo-description: Banners represent typically graphical promotional links. Follow this page to learn more.
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
exl-id: c65a24e6-3041-4774-aeed-8e188ea19b78
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 1%

---

# Gerenciamento de banners{#managing-banners}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

As ações de gerenciamento de conteúdo são os blocos fundamentais que ajudam a criar e gerenciar conteúdo em um aplicativo. As ações a seguir são executadas no conteúdo do aplicativo.

## Visão geral dos banners {#banners-overview}

Os banners geralmente representam links promocionais gráficos.

>[!NOTE]
>
>Consulte os seguintes recursos na Ajuda online para saber mais sobre os seguintes tópicos em aplicativos AEM Mobile:
>
>* [Considerações de design](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [Criação de banners](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)
>

## Criação de um banner {#creating-a-banner}

O fluxo de trabalho geral para criar um artigo é o seguinte:

1. Selecionar **Dispositivo móvel** do painel lateral.
1. Em Dispositivo móvel, escolha seu aplicativo móvel por demanda no catálogo.
1. Clique na seta para baixo no canto superior direito da **Gerenciar banners** bloco.
1. Analise cada etapa do assistente para continuar criando seu novo banner.
1. Quando estiver pronto, clique em **Criar**.
1. Seu novo banner aparece na tag **Gerenciar banners** bloco.

![chlimage_1-6](assets/chlimage_1-6.gif)

## Importação de um novo banner {#importing-a-new-banner}

O conteúdo do Mobile On-Demand existente pode ser baixado (importado) do Mobile On-Demand para o AEM. Isso permite a edição e a exibição de conteúdo local.

>[!NOTE]
>
>A importação não inclui imagens.

O fluxo de trabalho para importar um novo artigo

1. Em Dispositivo móvel, escolha seu aplicativo móvel por demanda no catálogo.
1. Clique na seta para baixo no canto superior direito da **Gerenciar banners** e selecione Importar banners.
1. Clique em **Importar banner** na caixa de diálogo e, em seguida, em Fechar.
1. Os artigos do Mobile On-Demand agora aparecem no **Gerenciar banners** bloco.

>[!CAUTION]
>
>Você deve associar uma conexão do Mobile On-Demand primeiro.

## Edição de um banner {#editing-a-banner}

Use o editor de arrastar e soltar AEM integrado para adicionar ou alterar um artigo. Componentes como texto e imagens podem ser adicionados/removidos. As imagens dos ativos DAM podem ser inseridas.

>[!CAUTION]
>
>Somente os banners criados no AEM podem ser abertos no editor.

O workflow para editar um artigo:

1. Em Dispositivo móvel, escolha seu aplicativo móvel por demanda no catálogo.
1. Selecione um banner de origem AEM no bloco ** Gerenciar banners**.
1. Clique no banner destacado da exibição de lista para abri-lo no editor de conteúdo.
1. Use o editor de conteúdo para arrastar o conteúdo do banner (manuscritos, imagens, texto etc.).

### Visualização e edição de metadados em um banner {#viewing-and-editing-the-metadata-within-a-banner}

Os banners têm várias propriedades, como títulos, descrições e imagens. Esta ação é usada para exibir e modificar essas propriedades. Como opção, essas alterações podem ser carregadas no Mobile On-Demand ao salvar.

O workflow geral para exibir/editar um artigo:

1. Em Dispositivo móvel, escolha seu aplicativo móvel por demanda no catálogo.
1. Escolha um banner na **Gerenciar banners** bloco.

1. Selecionar **Propriedades** na barra de ações.
1. Visualize todos os metadados disponíveis para esse artigo.
1. Edite os metadados se desejar e clique em **Salvar** quando terminar.
1. Como opção, carregue as alterações imediatamente no Mobile On-Demand.

## Carregamento de um banner {#uploading-a-banner}

A ação de upload copia o conteúdo selecionado e o adiciona a um projeto do Mobile On-Demand. O conteúdo já existente do Mobile On-Demand é substituído pela nova versão.

O fluxo de trabalho geral para carregar um banner:

1. De **Dispositivo móvel**, escolha seu aplicativo Mobile On-Demand no catálogo.
1. No **Gerenciar banners** selecione um banner para fazer upload no Mobile On-Demand.
1. Adicione mais banners, se necessário, da exibição de lista.
1. Selecionar **Carregar** na barra de ações e, em seguida, clique em Fazer upload na caixa de diálogo.
1. Seus banners agora são carregados no Mobile On-Demand.

![chlimage_1-7](assets/chlimage_1-7.gif)

## Excluir um banner {#deleting-a-banner}

Essa operação exclui o banner selecionado do Mobile On-Demand e, opcionalmente, da instância do AEM local.

O fluxo de trabalho geral para excluir um banner:

1. Em Dispositivo móvel, escolha seu aplicativo móvel por demanda no catálogo.
1. Selecione o banner a ser excluído na **Gerenciar banners** bloco.
1. Verifique se ele está selecionado na lista (selecione outros para excluir conforme necessário).
1. Clique em **Excluir** na barra de ações.
1. Verifique se você deseja excluir do AEM e do Mobile On-Demand.
1. Clique em **Excluir**.
1. Seu banner foi removido da lista.

### Próximas etapas {#the-next-steps}

Depois de aprender sobre o gerenciamento de banners, consulte

* [Gerenciamento de artigos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gerenciar coleções](/help/mobile/mobile-on-demand-managing-collections.md)
* [Upload de recursos compartilhados](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicar/desfazer publicação do conteúdo](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Visualização com simulação](/help/mobile/aem-mobile-manage-ondemand-services.md)
