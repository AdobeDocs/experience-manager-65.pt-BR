---
title: Gerenciamento de artigos
description: Siga esta página para saber mais sobre como criar e gerenciar artigos.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: ea6c8aa3-f86e-4878-8550-fe1662f10696
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---

# Gerenciamento de artigos{#managing-articles}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

As ações de Gestão de conteúdo são os blocos fundamentais que ajudam a criar e gerenciar artigos em um aplicativo. As ações a seguir são executadas em artigos do aplicativo.

## Visão geral dos artigos {#articles-overview}

Os artigos representam o texto com base na arte para transmitir informações.

>[!NOTE]
>
>Consulte os seguintes recursos na Ajuda online para saber mais sobre os seguintes tópicos em aplicativos AEM Mobile:
>
>* [Considerações sobre o design](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [Gerenciar artigos](https://helpx.adobe.com/digital-publishing-solution/help/creating-articles.html)
>

## Criação de um artigo {#creating-an-article}

O fluxo de trabalho geral para criar um artigo é o seguinte:

1. Selecione **Dispositivo móvel** no painel lateral.
1. Em Dispositivo móvel, escolha seu aplicativo móvel por demanda no catálogo.
1. Clique na seta para baixo no canto superior direito do bloco **Gerenciar artigos**.
1. Escolha um modelo de artigo e clique em **Próximo**.
1. Analise cada etapa do assistente para continuar criando seu novo artigo.
1. Quando estiver pronto, clique em **Criar**.
1. O novo artigo aparece no bloco **Gerenciar artigos**.

## Importando um novo artigo {#importing-a-new-article}

O conteúdo do Mobile On-Demand existente pode ser baixado (importado) do Mobile On-Demand para o AEM. Isso permite a edição e a exibição de conteúdo local.

>[!NOTE]
>
>A importação não inclui imagens.

O fluxo de trabalho para importar um novo artigo

1. Em Dispositivo móvel, escolha seu aplicativo móvel por demanda no catálogo.
1. Clique na seta para baixo no canto superior direito do bloco **Gerenciar artigos** e selecione Importar artigos.
1. Clique em **Importar artigos** na caixa de diálogo e em Fechar.
1. Seus artigos do Mobile On-Demand agora aparecem no bloco **Gerenciar artigos**.

>[!CAUTION]
>
>Associe uma conexão do Mobile On-Demand primeiro.

![chlimage_1-3](assets/chlimage_1-3.gif)

## Edição de um artigo {#editing-an-article}

Use o editor de arrastar e soltar AEM integrado para adicionar ou alterar um artigo. Componentes como texto e imagens podem ser adicionados/removidos. As imagens do Assets do DAM podem ser inseridas.

>[!CAUTION]
>
>Somente artigos criados no AEM podem ser abertos no editor.

O workflow para editar um artigo:

1. Em Dispositivo móvel, escolha seu aplicativo móvel por demanda no catálogo.
1. Selecione um artigo de origem AEM no bloco **Gerenciar artigos**.
1. Clique no artigo destacado da exibição em lista para abri-lo no editor de conteúdo.
1. Use o editor de conteúdo para arrastar o conteúdo do artigo (manuscritos, imagens, texto etc.).

### Visualização e edição dos metadados em um artigo {#viewing-and-editing-the-metadata-within-an-article}

Conteúdo como artigos, banners e assim por diante têm várias propriedades, como títulos, descrições e imagens. Esta ação é usada para exibir e modificar essas propriedades. Como opção, essas alterações podem ser carregadas no Mobile On-Demand ao salvar.

O workflow geral para exibir/editar um artigo:

1. Em Dispositivo móvel, escolha seu aplicativo móvel por demanda no catálogo.
1. Escolha um artigo no bloco **Gerenciar artigos**.

1. Selecione **Exibir Propriedades** na barra de ações.
1. Visualize todos os metadados disponíveis para esse artigo.
1. Edite os metadados, se desejar, e clique em **Salvar** quando terminar.
1. Como opção, carregue as alterações imediatamente no Mobile On-Demand.

## Carregamento de um artigo {#uploading-an-article}

A ação de upload copia o conteúdo selecionado e o adiciona a um projeto do Mobile On-Demand. O conteúdo já existente do Mobile On-Demand é substituído pela nova versão.

O fluxo de trabalho geral para carregar um artigo:

1. Em **Mobile**, escolha seu aplicativo Mobile On-Demand no catálogo.
1. No bloco **Gerenciar artigos**, selecione um artigo para carregar no Mobile On-Demand.
1. Adicione mais artigos, se necessário, na exibição em lista.
1. Selecione **Carregar** na barra de ações e clique em Carregar na caixa de diálogo.
1. Seus artigos foram carregados no Mobile On-Demand.

![chlimage_1-4](assets/chlimage_1-4.gif)

## Exclusão de um artigo {#deleting-an-article}

Essa operação exclui o conteúdo selecionado do Mobile On-Demand e, opcionalmente, da instância do AEM local.

O workflow geral para excluir um artigo:

1. Em Dispositivo móvel, escolha seu aplicativo móvel por demanda no catálogo.
1. Selecione o artigo a ser excluído no bloco **Gerenciar artigos**.
1. Verifique se está selecionado na lista; selecione outras para excluir, conforme necessário.
1. Clique em **Excluir** da barra de ações.
1. Marque se deseja excluir do AEM e do Mobile On-Demand.
1. Clique em **Excluir**.
1. O artigo foi removido da lista.

![chlimage_1-5](assets/chlimage_1-5.gif)

### Próximas etapas {#the-next-steps}

Depois de aprender sobre como gerenciar artigos, consulte

* [Gerenciamento de banners](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gerenciar coleções](/help/mobile/mobile-on-demand-managing-collections.md)
* [Upload de recursos compartilhados](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicar/desfazer publicação do conteúdo](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Visualização com simulação](/help/mobile/aem-mobile-manage-ondemand-services.md)
