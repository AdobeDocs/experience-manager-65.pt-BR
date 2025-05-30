---
title: Gerenciar coleções
description: As coleções representam um balde bem definido e recheado de conteúdo como artigos ou banners que se encaixam no tema da capa. Siga esta página para saber mais.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Gerenciar coleções{#managing-collections}

{{ue-over-mobile}}

As ações de gerenciamento de conteúdo são os blocos fundamentais que ajudam a criar e gerenciar conteúdo em um aplicativo. As ações a seguir são executadas no conteúdo do aplicativo.

## Visão geral das coleções {#collections-overview}

As coleções representam um *balde* bem definido e repleto de conteúdo, como artigos ou banners que se adaptam ao tema da capa.

>[!NOTE]
>
>Consulte os seguintes recursos na Ajuda online para saber mais sobre os seguintes tópicos em aplicativos AEM Mobile:
>
>* [Considerações sobre o design](https://helpx.adobe.com/br/digital-publishing-solution/help/design-app.html)
>
>* [Gerenciando Coleções](https://helpx.adobe.com/br/digital-publishing-solution/help/creating-collections.html)
>

## Criação de uma coleção {#creating-a-collection}

O fluxo de trabalho geral para criar uma coleção é o seguinte:

1. Selecione **Dispositivo móvel** no painel lateral.
1. Em Dispositivo móvel, escolha seu aplicativo móvel por demanda no catálogo.
1. Clique na seta para baixo no canto superior direito do bloco **Gerenciar coleções**.
1. Analise cada etapa do assistente para continuar criando seu novo artigo.
1. Quando estiver pronto, clique em **Criar**.
1. Seu novo artigo aparece no bloco **Gerenciar Coleções**.

![chlimage_1-1](assets/chlimage_1-1.gif)

## Importando uma nova coleção {#importing-a-new-collection}

O conteúdo do Mobile On-Demand existente pode ser baixado (importado) do Mobile On-Demand para o AEM. Isso permite a edição e a exibição de conteúdo local.

>[!NOTE]
>
>A importação não inclui imagens.

O fluxo de trabalho para importar uma nova coleção

1. Em Dispositivo móvel, escolha seu aplicativo móvel por demanda no catálogo.
1. Clique na seta para baixo no canto superior direito do bloco **Gerenciar coleções** e selecione Importar coleções.
1. Clique em **Importar coleções** na caixa de diálogo e em Fechar.
1. Suas coleções do Mobile On-Demand agora aparecem no bloco **Gerenciar coleções**.

>[!CAUTION]
>
>Associe uma conexão do Mobile On-Demand primeiro.

## Editar uma coleção {#editing-a-collection}

Use o editor de arrastar e soltar AEM integrado para adicionar ou alterar um artigo. Componentes como texto e imagens podem ser adicionados/removidos. As imagens do Assets do DAM podem ser inseridas.

O fluxo de trabalho para editar uma coleção:

1. Em Dispositivo móvel, escolha seu aplicativo móvel por demanda no catálogo.
1. Selecione um artigo de origem AEM no bloco **Gerenciar coleções**.
1. Clique na coleção destacada na exibição de lista para abri-la no editor de conteúdo.
1. Use o editor de conteúdo para arrastar o conteúdo da coleção (manuscritos, imagens, texto etc.).

### Exibição e edição de metadados em uma coleção {#viewing-and-editing-the-metadata-within-a-collection}

As coleções têm várias propriedades, como títulos, descrições e imagens. Esta ação é usada para exibir e modificar essas propriedades. Como opção, essas alterações podem ser carregadas no Mobile On-Demand ao salvar.

O fluxo de trabalho geral para exibir/editar uma coleção:

1. Em Dispositivo móvel, escolha seu aplicativo móvel por demanda no catálogo.
1. Escolha uma coleção no bloco **Gerenciar Coleções**.

1. Selecione **Propriedades** na barra de ações.
1. Visualize todos os metadados disponíveis para esse artigo.
1. Edite os metadados, se desejar, e clique em **Salvar** quando terminar.
1. Como opção, carregue as alterações imediatamente no Mobile On-Demand.

## Fazendo upload de uma coleção {#uploading-a-collection}

A ação de upload copia o conteúdo selecionado e o adiciona a um projeto do Mobile On-Demand. O conteúdo já existente do Mobile On-Demand é substituído pela nova versão.

O fluxo de trabalho geral para fazer upload de uma coleção:

1. Em **Mobile**, escolha seu aplicativo Mobile On-Demand no catálogo.
1. No bloco **Gerenciar coleções**, selecione um artigo para carregar no Mobile On-Demand.
1. Adicione mais coleções, se necessário, na exibição em lista.
1. Selecione **Carregar** na barra de ações e clique em Carregar na caixa de diálogo.
1. Suas coleções foram carregadas no Mobile On-Demand.

## Excluindo uma coleção {#deleting-a-collection}

Essa operação exclui a coleção selecionada do Mobile On-Demand e, opcionalmente, da instância do AEM local.

O fluxo de trabalho geral para excluir uma coleção:

1. Em Dispositivo móvel, escolha seu aplicativo móvel por demanda no catálogo.
1. Selecione o artigo a ser excluído no bloco **Gerenciar Coleções**.
1. Verifique se está selecionado na lista; selecione outras para excluir, conforme necessário.
1. Clique em **Excluir** da barra de ações.
1. Marque se deseja excluir do AEM e do Mobile On-Demand.
1. Clique em **Excluir**.
1. Sua coleção foi removida da lista.

## Adicionar conteúdo às coleções {#adding-content-to-collections}

As coleções são essencialmente uma categoria de conteúdo relacionado. Eles reúnem conteúdo como artigos, banners em pacotes que definem a estrutura de navegação do seu aplicativo. As coleções podem ser aninhadas.

>[!NOTE]
>
>O conteúdo deve ser carregado para o Mobile On-Demand antes de ser adicionado a uma coleção.

As coleções são essencialmente uma categoria de conteúdo relacionado: elas reúnem conteúdo como artigos, banners em pacotes que definem a estrutura de navegação do seu aplicativo. As coleções podem ser aninhadas.

1. Em Dispositivo móvel, escolha seu aplicativo móvel por demanda no catálogo.
1. Selecione um artigo carregado anteriormente (ou banner/coleção)
1. Escolha Adicionar a na barra de ações.
1. Selecione uma coleção carregada anteriormente na caixa de diálogo.
1. Clique em **Atualizar** para adicionar conteúdo à coleção.

![chlimage_1-2](assets/chlimage_1-2.gif)

### Próximas etapas {#the-next-steps}

Depois de aprender sobre o gerenciamento de coleções, consulte

* [Gerenciamento de banners](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gerenciamento de artigos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Upload de recursos compartilhados](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicar/desfazer publicação do conteúdo](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Visualização com simulação](/help/mobile/aem-mobile-manage-ondemand-services.md)
