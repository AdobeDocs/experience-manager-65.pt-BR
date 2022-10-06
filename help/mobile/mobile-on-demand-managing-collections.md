---
title: Gerenciando Coleções
seo-title: Managing Collections
description: As coleções representam um recipiente bem definido preenchido com conteúdo, como artigos ou banners, que se adequam ao tema da capa. Siga esta página para saber mais.
seo-description: Collections represent a well defined bucket filled with content such as articles or banners that suits the cover's theme. Follow this page to learn more.
uuid: 1d2e9769-d2cc-4d43-a428-e962a51eb5d0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 64c6d198-983f-4a52-9c83-560206363868
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 1%

---

# Gerenciando Coleções{#managing-collections}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

As ações de Gerenciamento de conteúdo são os blocos fundamentais que ajudam a criar e gerenciar conteúdo em um aplicativo. As seguintes ações são executadas no conteúdo do aplicativo.

## Visão geral das coleções {#collections-overview}

As coleções representam um *bucket* preenchido com conteúdo como artigos ou banners que se encaixam no tema da capa.

>[!NOTE]
>
>Consulte os seguintes recursos na Ajuda online para saber mais sobre os seguintes tópicos em aplicativos AEM Mobile:
>
>* [Considerações de design](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [Gerenciando Coleções](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)
>


## Criação de uma coleção {#creating-a-collection}

O fluxo de trabalho geral para criar uma coleção é o seguinte:

1. Selecionar **Celular** no painel lateral.
1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Clique na seta para baixo no canto superior direito da **Gerenciar coleções** mosaico.
1. Execute cada etapa do assistente para continuar criando seu novo artigo.
1. Quando estiver pronto, clique em **Criar**.
1. Seu novo artigo aparece no **Gerenciar coleções** mosaico.

![chlimage_1-1](assets/chlimage_1-1.gif)

## Importação de uma nova coleção {#importing-a-new-collection}

O conteúdo móvel sob demanda existente pode ser baixado (importado) do Mobile On-Demand para AEM. Isso permite a edição e a visualização de conteúdo local.

>[!NOTE]
>
>A importação não inclui imagens.

O fluxo de trabalho para importar uma nova coleção

1. Em Dispositivo móvel, escolha seu aplicativo móvel sob demanda no catálogo.
1. Clique na seta para baixo no canto superior direito da **Gerenciar coleções** e selecione Importar coleções.
1. Clique em **Importar Coleções** na caixa de diálogo, em seguida, em Fechar.
1. Suas coleções Mobile On-Demand agora aparecem no **Gerenciar coleções** mosaico.

>[!CAUTION]
>
>Você deve associar uma conexão móvel sob demanda primeiro.

## Edição de uma coleção {#editing-a-collection}

Use o editor arrastar e soltar incorporado AEM adicionar ou alterar um artigo. Componentes como texto e imagens podem ser adicionados/removidos. Imagens de ativos DAM podem ser inseridas.

O fluxo de trabalho para editar uma coleção:

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Selecione um artigo de origem AEM do **Gerenciar coleções** mosaico.
1. Clique na coleção realçada na exibição de lista para abri-la no editor de conteúdo.
1. Use o editor de conteúdo para arrastar o conteúdo da coleção (manuscritos, imagens, texto etc.).

### Visualização e edição dos metadados em uma coleção {#viewing-and-editing-the-metadata-within-a-collection}

As coleções têm várias propriedades, como títulos, descrições, imagens. Essa ação é usada para exibir e modificar essas propriedades. Como opção, essas alterações podem ser carregadas no Mobile On-Demand ao salvar.

O fluxo de trabalho geral para exibir/editar uma coleção:

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Escolha uma coleção no **Gerenciar coleções** mosaico.

1. Selecionar **Propriedades** na barra de ações.
1. Exibir todos os metadados disponíveis para esse artigo.
1. Edite os metadados, se desejado, e clique em **Salvar** quando concluído.
1. Como opção, carregue as alterações imediatamente no Mobile On-Demand.

## Fazer upload de uma coleção {#uploading-a-collection}

A ação de upload copia o conteúdo selecionado e o adiciona a um projeto Mobile On-Demand. O conteúdo Mobile On-Demand já existente é substituído pela nova versão.

O fluxo de trabalho geral para fazer upload de uma coleção:

1. De **Celular**, escolha seu aplicativo Mobile On-Demand no catálogo.
1. No **Gerenciar coleções** em bloco, selecione um artigo para upload no Mobile On-Demand.
1. Adicione mais coleções, se necessário, na exibição de lista.
1. Selecionar **Upload** na barra de ações, em seguida, clique em Fazer upload na caixa de diálogo.
1. Suas coleções agora são carregadas no Mobile On-Demand.

## Excluindo uma coleção {#deleting-a-collection}

Essa operação exclui a coleção selecionada do Mobile On-Demand e, opcionalmente, da instância de AEM local.

O fluxo de trabalho geral para excluir uma coleção:

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Selecione o artigo a ser excluído no **Gerenciar coleções** mosaico.
1. Certifique-se de que está selecionada na lista (selecione outras pessoas para eliminar conforme necessário).
1. Clique em **Excluir** na barra de ações.
1. Verifique se deseja excluir do AEM, bem como do Mobile On-Demand.
1. Clique em **Excluir**.
1. Sua coleção foi removida da lista.

## Adicionar conteúdo às coleções {#adding-content-to-collections}

As coleções são essencialmente uma categoria de conteúdo relacionado. Eles coletam conteúdo, como artigos, banners em pacotes que definem a estrutura de navegação do seu aplicativo. As coleções podem ser aninhadas.

>[!NOTE]
>
>O conteúdo deve ser carregado no Mobile On-Demand antes de ser adicionado a uma coleção.

As coleções são essencialmente uma categoria de conteúdo relacionado: Eles coletam conteúdo, como artigos, banners em pacotes que definem a estrutura de navegação do seu aplicativo. As coleções podem ser aninhadas.

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Selecione um artigo carregado anteriormente (ou banner/coleção)
1. Escolha Adicionar a na barra de ações.
1. Selecione uma coleção carregada anteriormente na caixa de diálogo.
1. Clique em **Atualizar** para adicionar conteúdo à coleção.

![chlimage_1-2](assets/chlimage_1-2.gif)

### Próximas etapas {#the-next-steps}

Uma vez que você saiba mais sobre gerenciamento de coleções, consulte

* [Gerenciamento de banners](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gerenciamento de artigos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Upload de recursos compartilhados](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicar/desfazer a publicação do conteúdo](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Visualização com comprovação](/help/mobile/aem-mobile-manage-ondemand-services.md)
