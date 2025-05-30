---
title: Produtor do catálogo
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
description: Produtor do catálogo
exl-id: 76a46c62-d47d-4970-8a3a-d56015639548
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# Produtor do catálogo{#catalog-producer}

Saiba como usar o Produtor de catálogo no AEM Assets para gerar catálogos de produtos usando seus ativos digitais.

Com o Adobe Experience Manager (AEM) Assets Catalog Producer, é possível criar catálogos para seus produtos de marca usando modelos de InDesign importados de um aplicativo do InDesign. Para importar templates de InDesign, primeiro integre o AEM Assets a um servidor do InDesign.

## Integração com o servidor do InDesign {#integrating-with-indesign-server}

Como parte do processo de integração, configure o fluxo de trabalho **Ativo de atualização do DAM**, que é adequado para integração com o InDesign. Além disso, configure um trabalhador proxy para o servidor do InDesign. Para obter detalhes, consulte [Integração do AEM Assets com o InDesign Server](/help/assets/indesign.md).

>[!NOTE]
>
>Você pode gerar modelos de InDesign a partir de arquivos InDesign antes de importá-los para o AEM Assets. Para obter detalhes, consulte [Trabalhando com arquivos e modelos](https://helpx.adobe.com/br/indesign/using/files-templates.html).
>
>Você pode mapear os elementos nos modelos de InDesign para tags XML. As tags mapeadas são exibidas como propriedades quando você mapeia propriedades de produto com propriedades de modelo no Produtor de catálogo. Para saber mais sobre marcação XML em arquivos de InDesign, consulte [Marcação de conteúdo para XML](https://helpx.adobe.com/br/indesign/using/tagging-content-xml.html).

>[!NOTE]
>
>Somente arquivos de InDesign (.indd) são usados como modelos. Arquivos com a extensão .indt não são suportados.

## Criação de um catálogo {#creating-a-catalog}

O Catalog Producer usa os dados de gerenciamento de informações do produto (PIM) para mapear propriedades do produto com as propriedades XML exibidas no modelo. Para criar um catálogo, execute estas etapas:

1. Na interface do usuário do Assets, clique no **logotipo do AEM** e vá para **Assets > Catálogos**.
1. Na página **Catálogos**, clique em **Criar** na barra de ferramentas e selecione **Catálogo** na lista.
1. Na página **Criar Catálogo**, digite um nome e uma descrição (opcional) para o catálogo e especifique as marcas, se houver. Você também pode adicionar uma imagem em miniatura para o catálogo.

   ![criar_catálogo](assets/create_catalog.png)

1. Clique em **Salvar**. Uma caixa de diálogo de confirmação notifica que o catálogo foi criado. Clique em **Concluído** para fechar a caixa de diálogo.
1. Para abrir o catálogo criado, clique nele na página **Catálogos**.

   >[!NOTE]
   >
   >Para abrir o catálogo, você também pode clicar em **Abrir** na caixa de diálogo de confirmação mencionada na etapa anterior.

1. Para adicionar páginas ao catálogo, clique em **Criar** na barra de ferramentas e escolha a opção **Nova Página**.
1. No assistente, selecione um modelo de InDesign para sua página. Em seguida, clique em **Avançar**.
1. Especifique um nome para a página e uma descrição opcional. Especifique as tags, se houver.
1. Clique em **Criar** na barra de ferramentas. Em seguida, clique em **Abrir** na caixa de diálogo. As propriedades do produto são exibidas no painel esquerdo. As propriedades predefinidas para o modelo de InDesign são exibidas no painel direito.
1. No painel esquerdo, arraste as propriedades do produto para as propriedades do modelo de InDesign e crie um mapeamento entre elas.

   Para exibir como a página aparece em tempo real, clique na guia **Visualizar** no painel direito.

1. Para criar mais páginas, repita as etapas de 6 a 9. Para criar páginas semelhantes para outros produtos, selecione a página e clique no ícone **Criar páginas semelhantes** na barra de ferramentas.

   ![criar_páginas_semelhantes](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >Você só pode criar páginas semelhantes para produtos com estrutura semelhante.

   Clique no ícone Adicionar, selecione produtos no seletor de produtos e clique em **Selecionar** na barra de ferramentas.

   ![select_product](assets/select_product.png)

1. Na barra de ferramentas, clique em **Criar**. Clique em **Concluído** para fechar a caixa de diálogo. Páginas semelhantes são incluídas no catálogo.
1. Para adicionar qualquer arquivo de InDesign existente ao catálogo, clique em **Criar** na barra de ferramentas e escolha a opção **Adicionar à página existente**.
1. Selecione o arquivo de InDesign e clique em **Adicionar** na barra de ferramentas. Em seguida, clique em **OK** para fechar a caixa de diálogo.

   Se os metadados dos produtos que você faz referência nas páginas do catálogo forem alterados, as alterações não serão refletidas automaticamente nas páginas do catálogo. Um banner rotulado **Desatualizado** aparece nas imagens do produto nas páginas do catálogo de referência, indicando que os metadados dos produtos referenciados não estão atualizados.

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   Para garantir que as imagens do produto reflitam as alterações mais recentes dos metadados, selecione a página no console Catálogo e clique no ícone **Atualizar página** na barra de ferramentas.

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >Para alterar os metadados de um produto referenciado, navegue até o console Produtos (**Logotipo AEM** > **Commerce** > **Produtos**) e selecione o produto. Em seguida, clique no ícone **Exibir propriedades** na barra de ferramentas e edite os metadados na página Propriedades do ativo.

1. Para reorganizar as páginas no catálogo, clique no ícone **Criar** na barra de ferramentas e escolha **Mesclar** no menu. No assistente, o carrossel na parte superior permite reorganizar as páginas arrastando-as. Também é possível remover páginas.

1. Clique em **Avançar**. Para adicionar um arquivo de InDesign existente como uma folha de rosto, clique em **Procurar** ao lado da caixa **Escolher folha de rosto** e especifique o caminho para o modelo de folha de rosto.
1. Clique em **Salvar** e em **Concluído** para fechar a caixa de diálogo de confirmação.
Ao selecionar a opção **Concluído**, uma caixa de diálogo é aberta para selecionar se você deseja uma representação em .pdf.
   ![exportar para pdf](assets/CatalogPDF.png)
Se a opção Acrobat(PDF) for selecionada, uma representação de pdf será criada em **/jcr:content/renditions**, além da representação do indesign. Você pode baixar todas as representações marcando a caixa de seleção &quot;Representações&quot; na caixa de diálogo de download.

1. Para gerar uma visualização do catálogo criado, selecione-o no console **Catálogos** e clique no ícone **Visualizar** na barra de ferramentas.

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   Revise as páginas no catálogo na visualização. Clique em **Fechar** para fechar a visualização.
