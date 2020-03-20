---
title: Gerenciar ativos compostos com referências e ativos de várias páginas no Experience Manager
description: Saiba como criar referências a ativos AEM no InDesign, no Illustrator e no Photoshop. Use o recurso Visualizador de página para exibir páginas de subativos individuais de arquivos de várias páginas, como arquivos PDF, INDD, PPT, PPTX e AI.
contentOwner: AG
translation-type: tm+mt
source-git-commit: d15273e9308926ca4745fc1045e2da9fe8ed91d4

---


# Gerenciar ativos compostos e de várias páginas {#managing-compound-assets}

Os ativos Adobe Experience Manager (AEM) podem identificar se um arquivo carregado contém referências a ativos que já existem no repositório. Este recurso está disponível somente para formatos de arquivo suportados. Se o ativo carregado contiver referências a ativos AEM, um link bidirecional será criado entre os ativos carregados e referenciados.

Além de eliminar a redundância, a referência aos ativos AEM nos aplicativos da Adobe Creative Cloud melhora a colaboração e aumenta a eficiência e a produtividade dos usuários.

Os ativos AEM oferecem suporte para referência bidirecional. Você pode encontrar ativos referenciados na página de detalhes do ativo do arquivo carregado. Além disso, você pode exibir os arquivos de referência para ativos AEM na página de detalhes do ativo referenciado.

As referências são resolvidas com base no caminho, na ID do documento e na ID da instância dos ativos referenciados.

## Adicionar ativos AEM como referências no Adobe Illustrator {#refai}

Você pode fazer referência a ativos AEM existentes em um arquivo do Adobe Illustrator.

1. Usando o aplicativo [](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)AEM para desktop, monte o repositório AEM Assets como uma unidade em sua máquina local. Na unidade montada, navegue até o local do ativo que deseja referenciar.
1. Arraste o ativo da unidade montada para o arquivo do Illustrator.

1. Salve o arquivo do Illustrator na unidade montada ou [carregue](/help/assets/managing-assets-touch-ui.md#uploading-assets) no repositório do AEM.

1. Após a conclusão do fluxo de trabalho, vá para a página de detalhes do ativo do ativo. As referências aos ativos AEM existentes estão listadas em **[!UICONTROL Dependências]** na coluna **[!UICONTROL Referências]** .

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Os ativos referenciados que aparecem em **[!UICONTROL Dependências]** também podem ser referenciados por arquivos diferentes do atual. Para exibir uma lista de arquivos de referência para um ativo, clique no ativo em **[!UICONTROL Dependências]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Clique em **[!UICONTROL Exibir propriedades]** na barra de ferramentas. Na página [!UICONTROL Propriedades] , a lista de arquivos que fazem referência ao ativo atual é exibida na coluna **[!UICONTROL Referências]** da guia **[!UICONTROL Básico]** .

   ![exibir as referências dos ativos do Experience Manager na coluna Referências nos detalhes do ativo](assets/asset-references.png)

   *Figura: Referências de ativos em detalhes de ativos*

## Adicionar ativos AEM como referências no Adobe InDesign {#add-aem-assets-as-references-in-adobe-indesign}

Para referenciar ativos AEM de um arquivo do InDesign, arraste os ativos AEM para o arquivo do InDesign ou exporte o arquivo do InDesign como um arquivo ZIP.

Os ativos referenciados já existem nos ativos AEM. Você pode extrair subativos [configurando o servidor](/help/assets/indesign.md)do InDesign. Os ativos incorporados em um arquivo do InDesign são extraídos como subativos.

>[!NOTE]
>
>Se o servidor do InDesign for proxy, os arquivos do InDesign terão sua visualização incorporada aos metadados XMP. Nesse caso, a extração de miniaturas não é explicitamente necessária. No entanto, se o servidor do InDesign não tiver proxy, as miniaturas deverão ser explicitamente extraídas para arquivos do InDesign.

### Criar referências arrastando ativos {#create-references-by-dragging-aem-assets}

Esse procedimento é semelhante a [Adicionar ativos AEM como referências no Adobe Illustrator](#refai).

### Criar referências a ativos exportando um arquivo ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Execute as etapas em [Criar modelos](/help/sites-developing/workflows-models.md) de fluxo de trabalho para criar um novo fluxo de trabalho.
1. Use o recurso Pacote do Adobe InDesign para exportar o documento.
O Adobe InDesign pode exportar um documento e os ativos vinculados como um pacote. Nesse caso, a pasta exportada contém uma pasta Links que contém subativos no arquivo do InDesign.
1. Crie um arquivo ZIP e carregue-o no repositório do AEM.
1. Inicie o `Unarchiver` fluxo de trabalho.
1. Quando o fluxo de trabalho é concluído, as referências na pasta Links são automaticamente mencionadas como subativos. Para exibir uma lista de ativos referenciados, navegue até a página de detalhes do ativo do InDesign e feche o [Painel](/help/sites-authoring/basic-handling.md#rail-selector).

## Adicionar ativos AEM como referências no Adobe Photoshop {#refps}

1. Usando um cliente WebDav, monte os ativos AEM como uma unidade.
1. Para criar referências a ativos AEM em um arquivo do Photoshop, navegue até os ativos correspondentes na unidade montada usando a funcionalidade Colocar vinculado no Photoshop.

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. Salve o arquivo do Photoshop na unidade montada ou [carregue](/help/assets/managing-assets-touch-ui.md#uploading-assets) no repositório do AEM.
1. Após a conclusão do fluxo de trabalho, as referências aos ativos AEM existentes são listadas na página de detalhes do ativo.

   Para exibir os ativos referenciados, feche o [Painel](/help/sites-authoring/basic-handling.md#rail-selector) na página de detalhes do ativo.

1. Os ativos referenciados também contêm a lista de ativos dos quais são referenciados. Para exibir uma lista de ativos referenciados, navegue até a página de detalhes do ativo e feche o [Painel](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>Os ativos em ativos compostos também podem ser referenciados com base na ID do documento e na ID da instância. Essa funcionalidade está disponível somente nas versões do Adobe Illustrator e do Adobe Photoshop. Para outros, a referência é feita com base no caminho relativo dos ativos vinculados no ativo composto principal, conforme feito em versões anteriores do AEM.

## Criar subativos {#generate-subassets}

Para os ativos suportados com formatos de várias páginas — Arquivos PDF, arquivos AI, arquivos Microsoft PowerPoint e Apple Keynote e arquivos Adobe InDesign — O AEM pode gerar subativos que correspondem a cada página individual do ativo original. Esses subativos estão vinculados ao ativo *pai* e facilitam a visualização de várias páginas. Para todos os outros fins, os subativos são tratados como ativos normais no AEM.

Por padrão, a geração de conjunto de subconjuntos é desativada. Para ativar a geração de subativos, siga estas etapas:

1. Faça logon no Experience Manager como administrador. Acesse **[!UICONTROL Ferramentas > Fluxo de trabalho > Modelos]**.
1. Selecione Fluxo de trabalho **[!UICONTROL Atualizar ativo]** DAM e clique em **[!UICONTROL Editar]**.
1. Clique em **[!UICONTROL Alternar painel]** lateral e localize a etapa **[!UICONTROL Criar subativo]** . Adicione a etapa ao fluxo de trabalho. Clique em **[!UICONTROL Sincronizar]**.

Para gerar os subativos, execute um dos procedimentos a seguir:

* Novos ativos: O fluxo de trabalho de Atualização de ativos [!UICONTROL do] DAM é executado em qualquer novo ativo carregado no AEM. Os subativos são gerados automaticamente para novos ativos de várias páginas.
* Ativos de várias páginas existentes: Execute manualmente o fluxo de trabalho Atualizar ativos [!UICONTROL do] DAM seguindo uma das etapas:

   * Selecione um ativo e clique em [!UICONTROL Linha do tempo] para abrir o painel esquerdo. Como alternativa, use o atalho do teclado `alt + 3`. Clique em [!UICONTROL Iniciar fluxo de trabalho], selecione [!UICONTROL DAM Update Asset (Ativo]de atualização de DAM), clique em [!UICONTROL Iniciar]e em [!UICONTROL Continuar].
   * Selecione um ativo e clique em [!UICONTROL Criar > Fluxo de trabalho] na barra de ferramentas. Na caixa de diálogo pop-up, selecione Fluxo de trabalho [!UICONTROL DAM Update Asset (Atualizar ativo] DAM), clique em [!UICONTROL Start (Iniciar]) e em [!UICONTROL Continue (Continuar]).

Especificamente para documentos do Microsoft Word, execute o fluxo de trabalho Analisar Documentos **[!UICONTROL do Word]** DAM. Ele gera um `cq:Page` componente do conteúdo do documento do Microsoft Word. As imagens extraídas do documento são referenciadas do `cq:Page` componente. Essas imagens são extraídas mesmo se a geração de subativos estiver desativada.

## View subassets {#viewing-subassets}

Os subativos são exibidos somente se os subativos forem gerados e estiverem disponíveis para o ativo multipáginas selecionado. Para exibir os subativos gerados, abra o ativo de várias páginas. Na área superior esquerda da página, clique no ícone ![Painel](assets/do-not-localize/aem_leftrail_contentonly.png) esquerdo e clique em **[!UICONTROL Subativos]** na lista. Quando você seleciona **[!UICONTROL Subativos]** na lista. Como alternativa, use o atalho do teclado `alt + 5`.

![Exibir subativos para um ativo de várias páginas](assets/view_subassets_simulation.gif)

## Exibir páginas de um arquivo de várias páginas {#view-pages-of-a-multi-page-file}

É possível exibir um arquivo de várias páginas, como PDF, INDD, PPT, PPTX e AI, usando o recurso Visualizador de páginas dos ativos AEM. Abra um ativo de várias páginas e clique em **[!UICONTROL Exibir páginas]** no canto superior esquerdo da página. O Visualizador de página que é aberto exibe as páginas do ativo e os controles para navegar e aplicar zoom em cada página.

![Exibir e ver páginas de um ativo de várias páginas](assets/view_multipage_asset_fmr.gif)

Para o InDesign, é possível extrair páginas usando o servidor do InDesign. Se as visualizações das páginas forem salvas durante a criação do arquivo do InDesign, o InDesign Server não será necessário para a extração da página.

As seguintes opções estão disponíveis na barra de ferramentas, no painel esquerdo e nos controles do Visualizador de páginas:

* **[!UICONTROL Ações]** da área de trabalho para abrir ou revelar um subativo específico usando o aplicativo da área de trabalho do AEM. Consulte como [configurar as ações](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2) da área de trabalho se estiver usando o aplicativo da área de trabalho do AEM.

* **[!UICONTROL A opção Propriedades]** abre a página [!UICONTROL Propriedades] do subativo específico.

* **[!UICONTROL A opção Anotar]** permite que você anote o subativo específico. As anotações usadas em subativos separados são coletadas e exibidas juntas quando o ativo pai é aberto para exibição.

* **[!UICONTROL A opção Visão geral]** da página exibe todos os subativos simultaneamente.

* **[!UICONTROL A opção Linha do tempo]** do painel esquerdo depois de clicar no ícone ![do painel](assets/do-not-localize/aem_leftrail_contentonly.png) esquerdo exibe o fluxo de atividade do arquivo.
