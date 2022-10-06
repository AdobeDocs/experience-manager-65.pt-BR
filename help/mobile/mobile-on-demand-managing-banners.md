---
title: Gerenciamento de banners
seo-title: Managing Banners
description: Banners representam links promocionais gráficos. Siga esta página para saber mais.
seo-description: Banners represent typically graphical promotional links. Follow this page to learn more.
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
exl-id: c65a24e6-3041-4774-aeed-8e188ea19b78
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---

# Gerenciamento de banners{#managing-banners}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

As ações de Gerenciamento de conteúdo são os blocos fundamentais que ajudam a criar e gerenciar conteúdo em um aplicativo. As seguintes ações são executadas no conteúdo do aplicativo.

## Visão geral dos banners {#banners-overview}

Banners representam links promocionais gráficos.

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

1. Selecionar **Celular** no painel lateral.
1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Clique na seta para baixo no canto superior direito da **Gerenciar banners** mosaico.
1. Execute cada etapa do assistente para continuar criando seu novo banner.
1. Quando estiver pronto, clique em **Criar**.
1. O novo banner aparece na **Gerenciar banners** mosaico.

![chlimage_1-6](assets/chlimage_1-6.gif)

## Importar um novo banner {#importing-a-new-banner}

O conteúdo móvel sob demanda existente pode ser baixado (importado) do Mobile On-Demand para AEM. Isso permite a edição e a visualização de conteúdo local.

>[!NOTE]
>
>A importação não inclui imagens.

O fluxo de trabalho para importar um novo artigo

1. Em Dispositivo móvel, escolha seu aplicativo móvel sob demanda no catálogo.
1. Clique na seta para baixo no canto superior direito da **Gerenciar banners** e selecione Importar banners.
1. Clique em **Importar Banner** na caixa de diálogo, em seguida, em Fechar.
1. Seus artigos sobre dispositivos móveis sob demanda agora aparecem no **Gerenciar banners** mosaico.

>[!CAUTION]
>
>Você deve associar uma conexão móvel sob demanda primeiro.

## Edição de um banner {#editing-a-banner}

Use o editor arrastar e soltar incorporado AEM adicionar ou alterar um artigo. Componentes como texto e imagens podem ser adicionados/removidos. Imagens de ativos DAM podem ser inseridas.

>[!CAUTION]
>
>Somente os banners criados no AEM podem ser abertos no editor.

O fluxo de trabalho para editar um artigo:

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Selecione um banner de origem AEM no bloco ** Gerenciar banners**.
1. Clique no banner destacado na exibição de lista para abri-lo no editor de conteúdo.
1. Use o editor de conteúdo para arrastar o conteúdo do banner (manuscritos, imagens, texto etc.).

### Visualização e edição dos metadados em um banner {#viewing-and-editing-the-metadata-within-a-banner}

Os banners têm várias propriedades, como títulos, descrições, imagens. Essa ação é usada para exibir e modificar essas propriedades. Como opção, essas alterações podem ser carregadas no Mobile On-Demand ao salvar.

O fluxo de trabalho geral para exibir/editar um artigo:

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Escolha um banner na **Gerenciar banners** mosaico.

1. Selecionar **Propriedades** na barra de ações.
1. Exibir todos os metadados disponíveis para esse artigo.
1. Edite os metadados, se desejado, e clique em **Salvar** quando concluído.
1. Como opção, carregue as alterações imediatamente no Mobile On-Demand.

## Fazer upload de um banner {#uploading-a-banner}

A ação de upload copia o conteúdo selecionado e o adiciona a um projeto Mobile On-Demand. O conteúdo Mobile On-Demand já existente é substituído pela nova versão.

O fluxo de trabalho geral para fazer upload de um banner:

1. De **Celular**, escolha seu aplicativo Mobile On-Demand no catálogo.
1. No **Gerenciar banners** bloco , selecione um banner para upload no Mobile On-Demand.
1. Adicione mais banners, se necessário, na exibição em lista.
1. Selecionar **Upload** na barra de ações, em seguida, clique em Fazer upload na caixa de diálogo.
1. Agora seus banners são carregados no Mobile On-Demand.

![chlimage_1-7](assets/chlimage_1-7.gif)

## Exclusão de um banner {#deleting-a-banner}

Essa operação exclui o banner selecionado do Mobile On-Demand e, opcionalmente, da instância de AEM local.

O fluxo de trabalho geral para excluir um banner:

1. No Mobile, escolha seu aplicativo Mobile On-Demand no catálogo.
1. Selecione o banner a ser excluído na **Gerenciar banners** mosaico.
1. Certifique-se de que está selecionada na lista (selecione outras pessoas para eliminar, conforme necessário).
1. Clique em **Excluir** na barra de ações.
1. Verifique se deseja excluir do AEM, bem como do Mobile On-Demand.
1. Clique em **Excluir**.
1. Seu banner foi removido da lista.

### Próximas etapas {#the-next-steps}

Uma vez que você aprende sobre gerenciamento de banners, veja

* [Gerenciamento de artigos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gerenciando Coleções](/help/mobile/mobile-on-demand-managing-collections.md)
* [Upload de recursos compartilhados](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicar/desfazer a publicação do conteúdo](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Visualização com comprovação](/help/mobile/aem-mobile-manage-ondemand-services.md)
