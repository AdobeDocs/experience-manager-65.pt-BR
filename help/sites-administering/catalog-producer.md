---
title: Produtor do Catálogo
seo-title: Catalog Producer
seo-description: Learn how to use Catalog Producer in AEM Assets to generate product catalogs using your digital assets.
uuid: da822d83-8b99-4089-ae1b-11d897d4044e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 90e36522-3af1-4a8a-b044-1c828c52974e
description: Produtor do Catálogo
exl-id: 76a46c62-d47d-4970-8a3a-d56015639548
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---

# Produtor do Catálogo{#catalog-producer}

Saiba como usar o Catalog Producer no AEM Assets para gerar catálogos de produtos usando seus ativos digitais.

Com o Adobe Experience Manager (AEM) Assets Catalog Producer, você pode criar catálogos para seus produtos de marca usando modelos de InDesign importados de um aplicativo InDesign. Para importar templates do InDesign, primeiro integre o AEM Assets a um servidor do InDesign.

## Integração com o servidor do InDesign {#integrating-with-indesign-server}

Como parte do processo de integração, configure a variável **Ativo de atualização DAM** fluxo de trabalho, que é adequado para integração com o InDesign. Além disso, configure um trabalhador proxy para o servidor do InDesign. Para obter detalhes, consulte [Integração do AEM Assets com o InDesign Server](/help/assets/indesign.md).

>[!NOTE]
>
>Você pode gerar templates do InDesign a partir de arquivos do InDesign antes de importá-los para o AEM Assets. Para obter detalhes, consulte [Trabalhar com arquivos e modelos](https://helpx.adobe.com/indesign/using/files-templates.html).
>
>Você pode mapear os elementos em seus modelos de InDesign para tags XML. As tags mapeadas são exibidas como propriedades ao mapear propriedades de produto com propriedades de modelo no produtor do catálogo. Para saber mais sobre a marcação XML em arquivos InDesign, consulte [Marcação de conteúdo para XML](https://helpx.adobe.com/indesign/using/tagging-content-xml.html).

>[!NOTE]
>
>Somente os arquivos InDesign (.indd) são usados como modelos. Arquivos com a extensão .indt não são suportados.

## Criação de um catálogo {#creating-a-catalog}

O Catalog Producer usa dados do gerenciamento de informações do produto (PIM) para mapear propriedades do produto com as propriedades XML exibidas no modelo. Para criar um catálogo, execute estas etapas:

1. Na interface do usuário do Assets, toque/clique no botão **Logotipo AEM** e vá para **Ativos > Catálogos**.
1. No **Catálogos** página, toque/clique **Criar** na barra de ferramentas e selecione **Catálogo** na lista.
1. No **Criar catálogo** , insira um nome e uma descrição (opcional) para o catálogo e especifique as tags, se houver. Você também pode adicionar uma imagem em miniatura ao catálogo.

   ![create_catalog](assets/create_catalog.png)

1. Toque/clique **Salvar**. Uma caixa de diálogo de confirmação notifica que o catálogo foi criado. Toque/clique **Concluído** para fechar a caixa de diálogo.
1. Para abrir o catálogo que você criou, toque/clique nele no link **Catálogos** página.

   >[!NOTE]
   >
   >Para abrir o catálogo, você também pode tocar/clicar em **Abrir** na caixa de diálogo de confirmação mencionada na etapa anterior.

1. Para adicionar páginas ao catálogo, toque/clique **Criar** na barra de ferramentas e escolha a opção **Nova página** opção.
1. No assistente, selecione um modelo de InDesign para a página. Em seguida, toque/clique em **Próximo**.
1. Especifique um nome para a página e uma descrição opcional. Especifique tags, se houver.
1. Toque/clique no botão **Criar** na barra de ferramentas. Em seguida, toque/clique em **Abrir** na caixa de diálogo. As propriedades do produto são exibidas no painel esquerdo. As propriedades predefinidas para o modelo de InDesign aparecem no painel direito.
1. No painel esquerdo, arraste as propriedades do produto para as propriedades do modelo de InDesign e crie um mapeamento entre elas.

   Para exibir como a página é exibida em tempo real, toque/clique no botão **Visualizar** no painel direito.

1. Para criar mais páginas, repita as etapas de 6 a 9. Para criar páginas semelhantes para outros produtos, selecione a página e toque/clique no botão **Criar páginas semelhantes** ícone na barra de ferramentas.

   ![create_like_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >Você só pode criar páginas semelhantes para produtos com estrutura semelhante.

   Toque/clique no ícone Adicionar , selecione produtos no seletor de produtos e toque/clique **Selecionar** na barra de ferramentas.

   ![select_product](assets/select_product.png)

1. Na barra de ferramentas, clique/toque em **Criar**. Toque/clique **Concluído** para fechar a caixa de diálogo. Páginas semelhantes são incluídas no catálogo.
1. Para adicionar qualquer arquivo de InDesign existente ao catálogo, toque/clique **Criar** na barra de ferramentas e escolha a opção **Adicionar à página existente** opção.
1. Selecione o arquivo de InDesign e toque/clique **Adicionar** na barra de ferramentas. Em seguida, toque/clique em **OK** para fechar a caixa de diálogo.

   Se os metadados dos produtos que você faz referência nas páginas do catálogo forem alterados, as alterações não serão refletidas automaticamente nas páginas do catálogo. Um banner rotulado **Stale** aparece nas imagens do produto nas páginas do catálogo de referência, indicando que os metadados dos produtos referenciados não estão atualizados.

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   Para garantir que as imagens do produto reflitam as alterações mais recentes de metadados, selecione a página no console Catálogo e clique/toque no **Atualizar página** ícone na barra de ferramentas.

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >Para alterar os metadados de um produto referenciado, navegue até o console Produtos (**Logotipo AEM** > **Comércio** > **Produtos**) e selecione o produto. Em seguida, clique/toque no botão **Propriedades da exibição** ícone na barra de ferramentas e edite os metadados na página Propriedades do ativo.

1. Para reorganizar as páginas no catálogo, toque/clique no botão **Criar** ícone na barra de ferramentas e escolha **Mesclar** no menu . No assistente, o carrossel na parte superior permite reordenar as páginas, arrastando-as. Também é possível remover páginas.

1. Toque/clique **Próximo**. Para adicionar um arquivo de InDesign existente como uma folha de rosto, toque/clique **Procurar** ao lado do **Escolha a página de capa** e especifique o caminho para o modelo da folha de rosto.
1. Toque/clique **Salvar** e toque/clique em **Concluído** para fechar a caixa de diálogo de confirmação.
Ao selecionar o **Concluído** , uma caixa de diálogo é aberta para selecionar se deseja que a renderização seja .pdf.
   ![exportar para pdf](assets/CatalogPDF.png)
Se a opção Acrobat(PDF) estiver selecionada, uma renderização de pdf será criada em  **/jcr:content/renditions** além da representação do indesign. Você pode baixar todas as representações marcando a caixa de seleção &quot;Representações&quot; na caixa de diálogo de download.

1. Para gerar uma pré-visualização para o catálogo criado, selecione-a no **Catálogos** e clique no **Visualizar** ícone na barra de ferramentas.

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   Revise as páginas do catálogo na pré-visualização. Toque/clique **Fechar** para fechar a visualização.
