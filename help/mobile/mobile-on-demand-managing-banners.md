---
title: Gerenciamento de banners
seo-title: Gerenciamento de banners
description: Os banners representam links promocionais tipicamente gráficos. Siga esta página para saber mais.
seo-description: Os banners representam links promocionais tipicamente gráficos. Siga esta página para saber mais.
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 1%

---


# Gerenciando banners{#managing-banners}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

As ações de gestão de conteúdo são os blocos de construção que ajudam a criar e gerenciar conteúdo em um aplicativo. As ações a seguir são executadas no conteúdo do aplicativo.

## Visão geral dos banners {#banners-overview}

Os banners representam links promocionais tipicamente gráficos.

>[!NOTE]
>
>Consulte os seguintes recursos na Ajuda online para saber mais sobre os seguintes tópicos em aplicativos AEM Mobile:
>
>* [Considerações de design](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [Criação de banners](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)

>



## Criação de um banner {#creating-a-banner}

O fluxo de trabalho geral para criar um artigo é o seguinte:

1. Selecione **Móvel** no painel lateral.
1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Clique na seta para baixo no canto superior direito do bloco **Gerenciar banners**.
1. Trabalhe em cada etapa do assistente para continuar criando seu novo banner.
1. Quando estiver pronto, clique em **Criar**.
1. Seu novo banner será exibido no bloco **Gerenciar banners**.

![chlimage_1-6](assets/chlimage_1-6.gif)

## Importando um novo banner {#importing-a-new-banner}

O conteúdo Mobile On-Demand existente pode ser baixado (importado) do Mobile On-Demand para o AEM. Isso permite a edição e visualização de conteúdo local.

>[!NOTE]
>
>A importação não inclui imagens.

O fluxo de trabalho para importar um novo artigo

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Clique na seta para baixo no canto superior direito do bloco **Gerenciar banners** e selecione Importar banners.
1. Clique em **Importar banner** na caixa de diálogo e, em seguida, em Fechar.
1. Seus artigos Mobile On-Demand agora aparecem no bloco **Gerenciar banners**.

>[!CAUTION]
>
>É necessário associar uma conexão Mobile On-Demand primeiro.

## Editar um banner {#editing-a-banner}

Use o editor incorporado AEM arrastar e soltar para adicionar ou alterar um artigo. Componentes como texto e imagens podem ser adicionados/removidos. Imagens de ativos DAM podem ser inseridas.

>[!CAUTION]
>
>Somente os banners criados no AEM podem ser abertos no editor.

O fluxo de trabalho para editar um artigo:

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Selecione um banner de origem AEM do bloco** Manage Banners**.
1. Clique no banner realçado da visualização da lista para abri-lo no editor de conteúdo.
1. Use o editor de conteúdo para arrastar o conteúdo do banner (manuscritos, imagens, texto etc.).

### Exibindo e editando os metadados em um banner {#viewing-and-editing-the-metadata-within-a-banner}

Os banners têm várias propriedades, como títulos, descrições, imagens. Essa ação é usada para visualização e modificação dessas propriedades. Como opção, essas alterações podem ser carregadas para Mobile On-Demand ao salvar.

O fluxo de trabalho geral para visualização/edição de um artigo:

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Escolha um banner no bloco **Gerenciar banners**.

1. Selecione **Propriedades** na barra de ações.
1. Visualização todos os metadados disponíveis para esse artigo.
1. Edite os metadados, se desejar, e clique em **Salvar** quando terminar.
1. Como opção, carregue as alterações imediatamente no Mobile On-Demand.

## Carregando um banner {#uploading-a-banner}

A ação de upload copia o conteúdo selecionado e o adiciona a um projeto Mobile On-Demand. O conteúdo Mobile On-Demand já existente é substituído pela nova versão.

O fluxo de trabalho geral para carregar um banner:

1. Em **Mobile**, escolha seu aplicativo Mobile On-Demand do catálogo.
1. No bloco **Gerenciar banners**, selecione um banner para carregar no Mobile On-Demand.
1. Adicione mais banners, se necessário, da visualização da lista.
1. Selecione **Carregar** na barra de ações e clique em Carregar na caixa de diálogo.
1. Seus banners agora são carregados para Mobile On-Demand.

![chlimage_1-7](assets/chlimage_1-7.gif)

## Excluindo um banner {#deleting-a-banner}

Essa operação exclui o banner selecionado do Mobile On-Demand e, opcionalmente, da instância de AEM local.

O fluxo de trabalho geral para excluir um banner:

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Selecione o banner a ser excluído no bloco **Gerenciar banners**.
1. Verifique se está selecionado na lista (selecione outras pessoas para excluir, conforme necessário).
1. Clique em **Excluir** na barra de ações.
1. Verifique se você deseja excluir do AEM, bem como Mobile On-Demand.
1. Clique em **Excluir**.
1. Seu banner foi removido da lista.

### Próximas etapas {#the-next-steps}

Um que você aprende sobre como gerenciar banners, consulte

* [Gerenciamento de artigos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gerenciamento de coleções](/help/mobile/mobile-on-demand-managing-collections.md)
* [Upload de recursos compartilhados](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicar/desfazer a publicação do conteúdo](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Visualização com o Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
