---
title: Produtor do catálogo
seo-title: Produtor do catálogo
seo-description: Saiba como usar o Catalog Producer na AEM Assets para gerar catálogos de produtos usando seus ativos digitais.
uuid: da822d83-8b99-4089-ae1b-11d897d4044e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 90e36522-3af1-4a8a-b044-1c828c52974e
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 0%

---


# Catalog Producer{#catalog-producer}

Saiba como usar o Catalog Producer na AEM Assets para gerar catálogos de produtos usando seus ativos digitais.

Com o Adobe Experience Manager (AEM) Assets Catalog Producer, você pode criar catálogos para seus produtos de marca usando modelos de InDesigns importados de um aplicativo de InDesign. Para importar modelos de InDesigns, integre primeiro o AEM Assets a um servidor de InDesigns.

## Integração com o servidor de InDesigns {#integrating-with-indesign-server}

Como parte do processo de integração, configure o fluxo de trabalho **DAM Update Asset**, adequado para integração com o InDesign. Além disso, configure um trabalho proxy para o servidor de InDesigns. Para obter detalhes, consulte [Integração do AEM Assets com o InDesign Server](/help/assets/indesign.md).

>[!NOTE]
>
>Você pode gerar modelos de InDesigns a partir de arquivos de InDesign antes de importá-los para o AEM Assets. Para obter detalhes, consulte [Trabalhar com arquivos e modelos](https://helpx.adobe.com/indesign/using/files-templates.html).
>
>É possível mapear os elementos em seus modelos de InDesigns para tags XML. As tags mapeadas são exibidas como propriedades quando você mapeia propriedades de produtos com propriedades de modelo no Catalog Producer. Para saber mais sobre a marcação XML em arquivos de InDesign, consulte [Marcação de conteúdo para XML](https://helpx.adobe.com/indesign/using/tagging-content-xml.html).

>[!NOTE]
>
>Somente arquivos de InDesign (.indd) são usados como modelos. Arquivos com a extensão .indt não são suportados.

## Criação de um catálogo {#creating-a-catalog}

O Catalog Producer usa dados de gerenciamento de informações do produto (PIM) para mapear as propriedades do produto com as propriedades XML exibidas no modelo. Para criar um catálogo, execute estas etapas:

1. Na interface do usuário do Assets, toque/clique no logotipo **AEM** e vá para **Ativos > Catálogos**.
1. Na página **Catálogos**, toque/clique em **Criar** na barra de ferramentas e selecione **Catálogo** na lista.
1. Na página **Criar catálogo**, digite um nome e uma descrição (opcional) para o catálogo e especifique as tags, se houver. Também é possível adicionar uma imagem em miniatura ao catálogo.

   ![create_Catalog](assets/create_catalog.png)

1. Toque/clique em **Salvar**. Uma caixa de diálogo de confirmação notifica que o catálogo foi criado. Toque/clique em **Concluído** para fechar a caixa de diálogo.
1. Para abrir o catálogo criado, toque/clique na página **Catálogos**.

   >[!NOTE]
   >
   >Para abrir o catálogo, você também pode tocar/clicar em **Abrir** na caixa de diálogo de confirmação mencionada na etapa anterior.

1. Para adicionar páginas ao catálogo, toque/clique em **Criar** na barra de ferramentas e escolha a opção **Nova página**.
1. No assistente, selecione um modelo de InDesign para sua página. Em seguida, toque/clique em **Próximo**.
1. Especifique um nome para a página e uma descrição opcional. Especifique as tags, se houver.
1. Toque/clique em **Criar** na barra de ferramentas. Em seguida, toque/clique em **Abrir** na caixa de diálogo. As propriedades do produto são exibidas no painel esquerdo. As propriedades predefinidas para o modelo de InDesign aparecem no painel direito.
1. No painel esquerdo, arraste as propriedades do produto para as propriedades do modelo de InDesign e crie um mapeamento entre elas.

   Para visualização de como a página aparece em tempo real, toque/clique na guia **Pré-visualização** no painel direito.

1. Para criar mais páginas, repita as etapas de 6 a 9. Para criar páginas semelhantes para outros produtos, selecione a página e toque/clique no ícone **Criar páginas semelhantes** na barra de ferramentas.

   ![create_similar_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >Você só pode criar páginas semelhantes para produtos com estrutura semelhante.

   Toque/clique no ícone Adicionar, selecione produtos no seletor de produtos e toque/clique em **Selecionar** na barra de ferramentas.

   ![select_product](assets/select_product.png)

1. Na barra de ferramentas, clique/toque em **Criar**. Toque/clique em **Concluído** para fechar a caixa de diálogo. Páginas semelhantes são incluídas no catálogo.
1. Para adicionar qualquer arquivo de InDesign existente ao catálogo, toque/clique em **Criar** na barra de ferramentas e escolha a opção **Adicionar à página existente**.
1. Selecione o arquivo de InDesign e toque/clique em **Adicionar** na barra de ferramentas. Em seguida, toque/clique em **OK** para fechar a caixa de diálogo.

   Se os metadados dos produtos que você menciona nas páginas do catálogo forem alterados, as alterações não serão refletidas automaticamente nas páginas do catálogo. Um banner chamado **Stale** aparece nas imagens do produto nas páginas de catálogo de referência, indicando que os metadados dos produtos referenciados não estão atualizados.

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   Para garantir que as imagens do produto reflitam as alterações de metadados mais recentes, selecione a página no console Catálogo e clique/toque no ícone **Atualizar página** na barra de ferramentas.

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >Para alterar os metadados de um produto referenciado, navegue até o console Produtos (**AEM Logo** > **Commerce** > **Products**) e selecione o produto. Em seguida, clique/toque no ícone **Propriedades da Visualização** na barra de ferramentas e edite os metadados na página Propriedades do ativo.

1. Para reorganizar as páginas no catálogo, toque/clique no ícone **Criar** na barra de ferramentas e escolha **Mesclar** no menu. No assistente, o carrossel na parte superior permite reordenar as páginas arrastando-as. Também é possível remover páginas.

1. Toque/clique em **Próximo**. Para adicionar um arquivo de InDesign existente como uma página de capa, toque/clique em **Procurar** ao lado da caixa **Escolher página de capa** e especifique o caminho para o modelo de folha de rosto.
1. Toque/clique em **Salvar** e toque/clique em **Concluído** para fechar a caixa de diálogo de confirmação.
Ao selecionar a opção **Concluído**, uma caixa de diálogo é aberta para selecionar se você deseja renderização .pdf.
   ![exportar para ](assets/CatalogPDF.png)
pdfSe a opção Acrobat(PDF) estiver selecionada, uma execução pdf será criada em   **/jcr:content/** renditions, além da execução do indesign. Você pode baixar todas as execuções marcando a caixa de seleção &quot;Representações&quot; na caixa de diálogo de download.

1. Para gerar uma pré-visualização para o catálogo criado, selecione-a no console **Catálogos** e clique no ícone **Pré-visualização** da barra de ferramentas.

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   Revise as páginas em seu catálogo na pré-visualização. Toque/clique em **Fechar** para fechar a pré-visualização.

