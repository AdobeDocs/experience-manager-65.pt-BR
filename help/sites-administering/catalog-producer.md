---
title: Produtor do catálogo
seo-title: Catalog Producer
seo-description: Learn how to use Catalog Producer in AEM Assets to generate product catalogs using your digital assets.
uuid: da822d83-8b99-4089-ae1b-11d897d4044e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 90e36522-3af1-4a8a-b044-1c828c52974e
description: Produtor do catálogo
exl-id: 76a46c62-d47d-4970-8a3a-d56015639548
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# Produtor do catálogo{#catalog-producer}

Saiba como usar o Produtor de catálogo no AEM Assets para gerar catálogos de produtos usando seus ativos digitais.

Com o Adobe Experience Manager (AEM) Assets Catalog Producer, é possível criar catálogos para seus produtos de marca usando modelos de InDesign importados de um aplicativo do InDesign. Para importar templates de InDesign, primeiro integre o AEM Assets a um servidor do InDesign.

## Integração com o servidor do InDesign {#integrating-with-indesign-server}

Como parte do processo de integração, configure a variável **Ativo de atualização DAM** fluxo de trabalho, que é adequado para integração com o InDesign. Além disso, configure um trabalhador proxy para o servidor do InDesign. Para obter detalhes, consulte [Integração do AEM Assets com o InDesign Server](/help/assets/indesign.md).

>[!NOTE]
>
>Você pode gerar modelos de InDesign a partir de arquivos InDesign antes de importá-los para o AEM Assets. Para obter detalhes, consulte [Trabalho com arquivos e modelos](https://helpx.adobe.com/indesign/using/files-templates.html).
>
>Você pode mapear os elementos nos modelos de InDesign para tags XML. As tags mapeadas são exibidas como propriedades quando você mapeia propriedades de produto com propriedades de modelo no Produtor de catálogo. Para saber mais sobre marcação XML em arquivos InDesign, consulte [Como marcar conteúdo para XML](https://helpx.adobe.com/indesign/using/tagging-content-xml.html).

>[!NOTE]
>
>Somente arquivos de InDesign (.indd) são usados como modelos. Arquivos com a extensão .indt não são suportados.

## Criação de um catálogo {#creating-a-catalog}

O Catalog Producer usa os dados de gerenciamento de informações do produto (PIM) para mapear propriedades do produto com as propriedades XML exibidas no modelo. Para criar um catálogo, execute estas etapas:

1. Na interface do Assets, clique na guia **Logotipo do AEM**, e vá para **Ativos > Catálogos**.
1. No **Catálogos** clique em **Criar** na barra de ferramentas e selecione **Catálogo** da lista.
1. No **Criar catálogo** insira um nome e uma descrição (opcional) para o catálogo e especifique tags, se houver. Você também pode adicionar uma imagem em miniatura para o catálogo.

   ![create_catalog](assets/create_catalog.png)

1. Clique em **Salvar**. Uma caixa de diálogo de confirmação notifica que o catálogo foi criado. Clique em **Concluído** para fechar o diálogo.
1. Para abrir o catálogo criado, clique nele no link **Catálogos** página.

   >[!NOTE]
   >
   >Para abrir o catálogo, você também pode clicar em **Abertura** na caixa de diálogo de confirmação mencionada na etapa anterior.

1. Para adicionar páginas ao catálogo, clique em **Criar** na barra de ferramentas e escolha a opção **Nova página** opção.
1. No assistente, selecione um modelo de InDesign para sua página. Em seguida, clique em **Próxima**.
1. Especifique um nome para a página e uma descrição opcional. Especifique as tags, se houver.
1. Clique em **Criar** na barra de ferramentas. Em seguida, clique em **Abertura** da caixa de diálogo. As propriedades do produto são exibidas no painel esquerdo. As propriedades predefinidas para o modelo de InDesign são exibidas no painel direito.
1. No painel esquerdo, arraste as propriedades do produto para as propriedades do modelo de InDesign e crie um mapeamento entre elas.

   Para visualizar como a página aparece em tempo real, clique no link **Visualizar** no painel direito.

1. Para criar mais páginas, repita as etapas de 6 a 9. Para criar páginas semelhantes para outros produtos, selecione a página e clique no link **Criar páginas semelhantes** ícone na barra de ferramentas.

   ![create_similar_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >Você só pode criar páginas semelhantes para produtos com estrutura semelhante.

   Clique no ícone Adicionar, selecione produtos no seletor de produtos e clique em **Selecionar** na barra de ferramentas.

   ![select_product](assets/select_product.png)

1. Na barra de ferramentas, clique em **Criar**. Clique em **Concluído** para fechar o diálogo. Páginas semelhantes são incluídas no catálogo.
1. Para adicionar qualquer arquivo de InDesign existente ao catálogo, clique em **Criar** na barra de ferramentas e escolha o **Adicionar à página existente** opção.
1. Selecione o arquivo de InDesign e clique em **Adicionar** na barra de ferramentas. Em seguida, clique em **OK** para fechar o diálogo.

   Se os metadados dos produtos que você faz referência nas páginas do catálogo forem alterados, as alterações não serão refletidas automaticamente nas páginas do catálogo. Um banner rotulado **Obsoleto** é exibido nas imagens do produto nas páginas do catálogo de referência, indicando que os metadados dos produtos referenciados não estão atualizados.

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   Para garantir que as imagens do produto reflitam as alterações de metadados mais recentes, selecione a página no console Catálogo e clique no **Atualizar página** ícone na barra de ferramentas.

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >Para alterar os metadados de um produto referenciado, navegue até o console Produtos (**Logotipo do AEM** > **Commerce** > **Produtos**) e selecione o produto. Em seguida, clique no link **Propriedades da exibição** ícone na barra de ferramentas e edite os metadados na página Propriedades do ativo.

1. Para reorganizar as páginas no catálogo, clique no link **Criar** na barra de ferramentas e escolha **Mesclar** no menu. No assistente, o carrossel na parte superior permite reorganizar as páginas arrastando-as. Também é possível remover páginas.

1. Clique em **Avançar**. Para adicionar um arquivo de InDesign existente como uma página de capa, clique em **Procurar** ao lado da variável **Escolha uma página de capa** e especifique o caminho para o modelo de folha de rosto.
1. Clique em **Salvar** e clique em **Concluído** para fechar o diálogo de confirmação.
Ao selecionar a variável **Concluído** , uma caixa de diálogo será aberta para selecionar se deseja a representação de .pdf.
   ![exportar para pdf](assets/CatalogPDF.png)
Se a opção Acrobat(PDF) estiver selecionada, uma representação de pdf será criada em  **/jcr:content/renditions** além da representação do indesign. Você pode baixar todas as representações marcando a caixa de seleção &quot;Representações&quot; na caixa de diálogo de download.

1. Para gerar uma visualização do catálogo criado, selecione-o na **Catálogos** e, em seguida, clique no link **Visualizar** ícone na barra de ferramentas.

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   Revise as páginas no catálogo na visualização. Clique em **Fechar** para fechar a visualização.
