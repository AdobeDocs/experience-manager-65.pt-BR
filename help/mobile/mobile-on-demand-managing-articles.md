---
title: Gerenciamento de artigos
seo-title: Gerenciamento de artigos
description: Siga esta página para saber mais sobre como criar e gerenciar artigos.
seo-description: Siga esta página para saber mais sobre como criar e gerenciar artigos.
uuid: 72b86cd7-3016-41b6-a001-9dce4084e9db
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: b46058f9-4691-4fba-a656-0f8507875a79
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---


# Gerenciamento de artigos{#managing-articles}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

As ações de gestão de conteúdo são os blocos de construção que ajudam a criar e gerenciar artigos em um aplicativo. As ações a seguir são executadas em artigos dentro do aplicativo.

## Visão geral dos artigos {#articles-overview}

Os artigos representam o texto com base na arte para transmitir informações.

>[!NOTE]
>
>Consulte os seguintes recursos na Ajuda online para saber mais sobre os seguintes tópicos em aplicativos AEM Mobile:
>
>* [Considerações de design](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [Gerenciamento de artigos](https://helpx.adobe.com/digital-publishing-solution/help/creating-articles.html)

>



## Criação de um artigo {#creating-an-article}

O fluxo de trabalho geral para criar um artigo é o seguinte:

1. Selecione **Móvel** no painel lateral.
1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Clique na seta para baixo no canto superior direito do bloco **Gerenciar artigos**.
1. Escolha um modelo de artigo e clique em **Next**.
1. Execute cada etapa do assistente para continuar criando seu novo artigo.
1. Quando estiver pronto, clique em **Criar**.
1. O novo artigo é exibido no bloco **Gerenciar artigos**.

## Importando um novo artigo {#importing-a-new-article}

O conteúdo Mobile On-Demand existente pode ser baixado (importado) do Mobile On-Demand para o AEM. Isso permite a edição e visualização de conteúdo local.

>[!NOTE]
>
>A importação não inclui imagens.

O fluxo de trabalho para importar um novo artigo

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Clique na seta para baixo no canto superior direito do bloco **Gerenciar artigos** e selecione Importar artigos.
1. Clique em **Importar artigos** na caixa de diálogo e, em seguida, em Fechar.
1. Seus artigos Mobile On-Demand agora aparecem no bloco **Gerenciar artigos**.

>[!CAUTION]
>
>É necessário associar uma conexão Mobile On-Demand primeiro.

![chlimage_1-3](assets/chlimage_1-3.gif)

## Editar um artigo {#editing-an-article}

Use o editor incorporado AEM arrastar e soltar para adicionar ou alterar um artigo. Componentes como texto e imagens podem ser adicionados/removidos. Imagens de ativos DAM podem ser inseridas.

>[!CAUTION]
>
>Somente os artigos criados no AEM podem ser abertos no editor.

O fluxo de trabalho para editar um artigo:

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Selecione um artigo de origem AEM no bloco **Gerenciar artigos**.
1. Clique no artigo destacado da visualização de lista para abri-la no editor de conteúdo.
1. Use o editor de conteúdo para arrastar o conteúdo do artigo (manuscritos, imagens, texto etc.).

### Exibição e edição dos metadados em um artigo {#viewing-and-editing-the-metadata-within-an-article}

Conteúdos como artigos, banners etc têm várias propriedades, como títulos, descrições, imagens. Essa ação é usada para visualização e modificação dessas propriedades. Como opção, essas alterações podem ser carregadas para Mobile On-Demand ao salvar.

O fluxo de trabalho geral para visualização/edição de um artigo:

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Escolha um artigo no bloco **Gerenciar artigos**.

1. Selecione **Propriedades da Visualização** na barra de ações.
1. Visualização todos os metadados disponíveis para esse artigo.
1. Edite os metadados, se desejar, e clique em **Salvar** quando terminar.
1. Como opção, carregue as alterações imediatamente no Mobile On-Demand.

## Upload de um artigo {#uploading-an-article}

A ação de upload copia o conteúdo selecionado e o adiciona a um projeto Mobile On-Demand. O conteúdo Mobile On-Demand já existente é substituído pela nova versão.

O fluxo de trabalho geral para carregar um artigo:

1. Em **Mobile**, escolha seu aplicativo Mobile On-Demand do catálogo.
1. No bloco **Gerenciar artigos**, selecione um artigo para upload no Mobile On-Demand.
1. Adicione mais artigos, se necessário, da visualização da lista.
1. Selecione **Carregar** na barra de ações e clique em Carregar na caixa de diálogo.
1. Seus artigos agora são carregados para Mobile On-Demand.

![chlimage_1-4](assets/chlimage_1-4.gif)

## Excluindo um artigo {#deleting-an-article}

Esta operação exclui o conteúdo selecionado do Mobile On-Demand e, opcionalmente, da instância de AEM local.

O fluxo de trabalho geral para excluir um artigo:

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Selecione o artigo a ser excluído no bloco **Gerenciar artigos**.
1. Verifique se está selecionado na lista (selecione outras pessoas para excluir, conforme necessário).
1. Clique em **Excluir** na barra de ações.
1. Verifique se você deseja excluir do AEM, bem como Mobile On-Demand.
1. Clique em **Excluir**.
1. Seu artigo agora é removido da lista.

![chlimage_1-5](assets/chlimage_1-5.gif)

### Próximas etapas {#the-next-steps}

Uma que você aprende sobre como gerenciar artigos, consulte

* [Gerenciamento de banners](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gerenciamento de coleções](/help/mobile/mobile-on-demand-managing-collections.md)
* [Upload de recursos compartilhados](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicar/desfazer a publicação do conteúdo](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Visualização com o Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
