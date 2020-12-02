---
title: Gerenciamento de coleções
seo-title: Gerenciamento de coleções
description: As coleções representam um conjunto bem definido preenchido com conteúdo, como artigos ou banners, que se adequam ao tema da capa. Siga esta página para saber mais.
seo-description: As coleções representam um conjunto bem definido preenchido com conteúdo, como artigos ou banners, que se adequam ao tema da capa. Siga esta página para saber mais.
uuid: 1d2e9769-d2cc-4d43-a428-e962a51eb5d0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 64c6d198-983f-4a52-9c83-560206363868
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 1%

---


# Gerenciar coleções{#managing-collections}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

As ações de gestão de conteúdo são os blocos de construção que ajudam a criar e gerenciar conteúdo em um aplicativo. As ações a seguir são executadas no conteúdo do aplicativo.

## Visão geral das coleções {#collections-overview}

As coleções representam um *bucket* bem definido preenchido com conteúdo, como artigos ou banners, que se encaixa no tema da capa.

>[!NOTE]
>
>Consulte os seguintes recursos na Ajuda online para saber mais sobre os seguintes tópicos em aplicativos AEM Mobile:
>
>* [Considerações de design](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [Gerenciamento de coleções](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)

>



## Criação de uma coleção {#creating-a-collection}

O fluxo de trabalho geral para criar uma coleção é o seguinte:

1. Selecione **Móvel** no painel lateral.
1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Clique na seta para baixo no canto superior direito do bloco **Gerenciar coleções**.
1. Execute cada etapa do assistente para continuar criando seu novo artigo.
1. Quando estiver pronto, clique em **Criar**.
1. O novo artigo é exibido no bloco **Gerenciar coleções**.

![chlimage_1-1](assets/chlimage_1-1.gif)

## Importando uma Nova Coleção {#importing-a-new-collection}

O conteúdo Mobile On-Demand existente pode ser baixado (importado) do Mobile On-Demand para o AEM. Isso permite a edição e visualização de conteúdo local.

>[!NOTE]
>
>A importação não inclui imagens.

O fluxo de trabalho para importar uma nova coleção

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Clique na seta para baixo no canto superior direito do bloco **Gerenciar coleções** e selecione Importar coleções.
1. Clique em **Importar coleções** na caixa de diálogo e, em seguida, em Fechar.
1. Suas coleções Mobile On-Demand agora aparecem no bloco **Gerenciar coleções**.

>[!CAUTION]
>
>É necessário associar uma conexão Mobile On-Demand primeiro.

## Editando uma coleção {#editing-a-collection}

Use o editor incorporado AEM arrastar e soltar para adicionar ou alterar um artigo. Componentes como texto e imagens podem ser adicionados/removidos. Imagens de ativos DAM podem ser inseridas.

O fluxo de trabalho para editar uma coleção:

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Selecione um artigo de origem AEM no bloco **Gerenciar coleções**.
1. Clique na coleção realçada da visualização da lista para abri-la no editor de conteúdo.
1. Use o editor de conteúdo para arrastar o conteúdo da coleção (manuscritos, imagens, texto etc.).

### Exibição e edição de metadados em uma coleção {#viewing-and-editing-the-metadata-within-a-collection}

As coleções têm várias propriedades, como títulos, descrições e imagens. Essa ação é usada para visualização e modificação dessas propriedades. Como opção, essas alterações podem ser carregadas para Mobile On-Demand ao salvar.

O fluxo de trabalho geral para visualização/edição de uma coleção:

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Escolha uma coleção no bloco **Gerenciar coleções**.

1. Selecione **Propriedades** na barra de ações.
1. Visualização todos os metadados disponíveis para esse artigo.
1. Edite os metadados, se desejar, e clique em **Salvar** quando terminar.
1. Como opção, carregue as alterações imediatamente no Mobile On-Demand.

## Carregando uma coleção {#uploading-a-collection}

A ação de upload copia o conteúdo selecionado e o adiciona a um projeto Mobile On-Demand. O conteúdo Mobile On-Demand já existente é substituído pela nova versão.

O fluxo de trabalho geral para carregar uma coleção:

1. Em **Mobile**, escolha seu aplicativo Mobile On-Demand do catálogo.
1. No bloco **Gerenciar coleções**, selecione um artigo para upload para Mobile On-Demand.
1. Adicione mais coleções, se necessário, da visualização da lista.
1. Selecione **Carregar** na barra de ações e clique em Carregar na caixa de diálogo.
1. Agora, suas coleções são carregadas no Mobile On-Demand.

## Excluindo uma coleção {#deleting-a-collection}

Essa operação exclui a coleção selecionada do Mobile On-Demand e, opcionalmente, da instância de AEM local.

O fluxo de trabalho geral para excluir uma coleção:

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Selecione o artigo a ser excluído no bloco **Gerenciar coleções**.
1. Verifique se está selecionado na lista (selecione outras pessoas para excluir, conforme necessário).
1. Clique em **Excluir** na barra de ações.
1. Verifique se você deseja excluir do AEM, bem como Mobile On-Demand.
1. Clique em **Excluir**.
1. Sua coleção agora é removida da lista.

## Adicionar conteúdo às coleções {#adding-content-to-collections}

As coleções são essencialmente uma categoria de conteúdo relacionado. Eles coletam conteúdo como artigos, banners em pacotes que definem a estrutura de navegação do aplicativo. As coleções podem ser aninhadas.

>[!NOTE]
>
>O conteúdo deve ser carregado no Mobile On-Demand antes de ser adicionado a uma coleção.

As coleções são essencialmente uma categoria de conteúdo relacionado: Eles coletam conteúdo como artigos, banners em pacotes que definem a estrutura de navegação do aplicativo. As coleções podem ser aninhadas.

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Selecionar um artigo carregado anteriormente (ou banner/coleção)
1. Escolha Adicionar a na barra de ações.
1. Selecione uma coleção carregada anteriormente na caixa de diálogo.
1. Clique em **Atualizar** para adicionar conteúdo à coleção.

![chlimage_1-2](assets/chlimage_1-2.gif)

### Próximas etapas {#the-next-steps}

Uma vez que você aprender sobre como gerenciar coleções, consulte

* [Gerenciamento de banners](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gerenciamento de artigos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Upload de recursos compartilhados](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicar/desfazer a publicação do conteúdo](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Visualização com o Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
