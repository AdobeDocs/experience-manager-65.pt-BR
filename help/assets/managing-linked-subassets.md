---
title: Gerencie ativos compostos com referências e ativos de várias páginas no Adobe Experience Manager.
description: Saiba como criar referências a ativos digitais no Adobe InDesign, no Adobe Illustrator e no Adobe Photoshop. Use o recurso Visualizador de página para visualização de páginas de subativos individuais de arquivos de várias páginas, como arquivos PDF, INDD, PPT, PPTX e AI.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 790efeaff6c8cf7e60104601e08955180dbb9600

---


# Gerenciar ativos compostos e de várias páginas {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] pode identificar se um arquivo carregado contém referências a ativos que já existem no repositório. Este recurso está disponível somente para formatos de arquivo suportados. Se o ativo carregado contiver qualquer referência aos ativos do Experience Manager, um link bidirecional será criado entre os ativos carregados e referenciados.

Além de eliminar a redundância, a referência aos ativos nos aplicativos da Adobe Creative Cloud melhora a colaboração e aumenta a eficiência e a produtividade dos usuários.

[!DNL Experience Manager Assets] suporta referenciação bidirecional. Você pode encontrar ativos referenciados na página de detalhes do ativo do arquivo carregado. Além disso, você pode visualização os arquivos de referência na página de detalhes do ativo referenciado.

As referências são resolvidas com base no caminho, na ID do documento e na ID da instância dos ativos referenciados.

## Adicionar ativos digitais como referências em [!DNL Adobe Illustrator]{#refai}

Você pode fazer referência a ativos digitais existentes em um [!DNL Adobe Illustrator] arquivo.

1. Usando o aplicativo [](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)Experience Manager para desktop, busque os ativos digitais no sistema de arquivos local. Navegue até o local do sistema de arquivos do ativo que deseja referenciar.
1. Arraste o ativo da pasta local para o [!DNL Illustrator] arquivo.

1. Salve o [!DNL Illustrator] arquivo na unidade montada ou [carregue](/help/assets/managing-assets-touch-ui.md#uploading-assets) no repositório do Experience Manager.

1. Após a conclusão do fluxo de trabalho, vá para a página de detalhes do ativo do ativo. As referências a ativos digitais existentes são listadas em **[!UICONTROL Dependências]** na coluna **[!UICONTROL Referências]** .

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Os ativos referenciados que aparecem em **[!UICONTROL Dependências]** também podem ser referenciados por arquivos diferentes do atual. Para visualização de uma lista de arquivos de referência para um ativo, clique no ativo em **[!UICONTROL Dependências]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Clique em Propriedades **[!UICONTROL da]** Visualização na barra de ferramentas. Na página [!UICONTROL Propriedades] , a lista de arquivos que fazem referência ao ativo atual é exibida na coluna **[!UICONTROL Referências]** da guia **[!UICONTROL Básico]** .

   ![visualização das referências dos ativos do Experience Manager na coluna Referências nos detalhes do ativo](assets/asset-references.png)

   *Figura: Referências de ativos em detalhes de ativos*

## Adicionar ativos digitais como referências em [!DNL Adobe InDesign]{#add-aem-assets-as-references-in-adobe-indesign}

Para referenciar ativos digitais de dentro de um [!DNL InDesign] arquivo, arraste os ativos para o [!DNL InDesign] arquivo ou exporte o [!DNL InDesign] arquivo como um arquivo ZIP.

Os ativos referenciados já existem em [!DNL Experience Manager Assets]. Você pode extrair subativos [configurando o InDesign Server](indesign.md). Os ativos incorporados em um [!DNL InDesign] arquivo são extraídos como subativos.

>[!NOTE]
>
>Se o proxy [!DNL InDesign Server] for feito, [!DNL InDesign] a pré-visualização dos arquivos será incorporada aos metadados XMP. Nesse caso, a extração em miniatura não é explicitamente exigida. No entanto, se o proxy não [!DNL InDesign Server] for feito, as miniaturas deverão ser explicitamente extraídas para [!DNL InDesign] arquivos.

### Criar referências arrastando ativos {#create-references-by-dragging-aem-assets}

Esse procedimento é semelhante a [adicionar ativos digitais como referências no Adobe Illustrator](#refai).

### Criar referências a ativos exportando um arquivo ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Execute as etapas em [Criar modelos](/help/sites-developing/workflows-models.md) de fluxo de trabalho para criar um novo fluxo de trabalho.
1. Use o recurso Package (Pacote) de [!DNL Adobe InDesign] para exportar o documento. [!DNL Adobe InDesign] pode exportar um documento e os ativos vinculados como um pacote. Nesse caso, a pasta exportada contém uma pasta Links que contém subativos no [!DNL InDesign] arquivo.
1. Crie um arquivo ZIP e carregue-o no [!DNL Experience Manager] repositório.
1. Start do `Unarchiver` fluxo de trabalho.
1. Quando o fluxo de trabalho é concluído, as referências na pasta Links são automaticamente mencionadas como subativos. Para visualização de uma lista de ativos referenciados, navegue até a página de detalhes do ativo e feche o [!DNL InDesign] Painel [](/help/sites-authoring/basic-handling.md#rail-selector).

## Adicionar ativos digitais como referências em [!DNL Adobe Photoshop]{#refps}

1. Use o aplicativo [!DNL Experience Manager] desktop para acessar [!DNL Experience Manager Assets]. Baixe e revele os ativos no sistema de arquivos local. Use a funcionalidade [!UICONTROL Inserir vinculado] em [!DNL Adobe Photoshop]. Consulte [colocar ativos no aplicativo](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents)de desktop.

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. Salve o arquivo na unidade montada ou [!DNL Photoshop] carregue [no](/help/assets/managing-assets-touch-ui.md#uploading-assets) [!DNL Experience Manager] repositório.
1. Após a conclusão do fluxo de trabalho, as referências aos ativos existentes são listadas na página de detalhes do ativo. [!DNL Experience Manager]

   Para visualização dos ativos referenciados, feche o [Painel](/help/sites-authoring/basic-handling.md#rail-selector) na página de detalhes do ativo.

1. Os ativos referenciados também contêm a lista de ativos dos quais são referenciados. Para visualização de uma lista de ativos referenciados, navegue até a página de detalhes do ativo e feche o [Painel](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>Os ativos em ativos compostos também podem ser referenciados com base na ID do Documento e na ID da instância. Essa funcionalidade está disponível somente com [!DNL Adobe Illustrator] e [!DNL Adobe Photoshop] versões. Para outros, a referência é feita com base na trajetória relativa dos ativos vinculados no ativo composto principal, conforme feito em versões anteriores do [!DNL Experience Manager].

## Criar subativos {#generate-subassets}

Para os ativos suportados com formatos de várias páginas — arquivos PDF, arquivos AI [!DNL Microsoft PowerPoint] e [!DNL Apple Keynote] arquivos e [!DNL Adobe InDesign] arquivos — [!DNL Experience Manager] pode gerar subativos que correspondem a cada página individual do ativo original. Esses subativos estão vinculados ao ativo *pai* e facilitam a visualização de várias páginas. Para todos os outros fins, os subativos são tratados como ativos normais em [!DNL Experience Manager].

Por padrão, a geração de conjunto de subconjuntos é desativada. Para ativar a geração de subativos, siga estas etapas:

1. Faça logon no Experience Manager como administrador. Acesse **[!UICONTROL Ferramentas > Fluxo de trabalho > Modelos]**.
1. Selecione Fluxo de trabalho **[!UICONTROL Atualizar ativo]** DAM e clique em **[!UICONTROL Editar]**.
1. Clique em **[!UICONTROL Alternar painel]** lateral e localize a etapa **[!UICONTROL Criar subativo]** . Adicione a etapa ao fluxo de trabalho. Clique em **[!UICONTROL Sincronizar]**.

Para gerar os subativos, execute um dos procedimentos a seguir:

* Novos ativos: O fluxo de trabalho dos Ativos [!UICONTROL de atualização do] DAM é executado em qualquer novo ativo carregado para [!DNL Experience Manager]. Os subativos são gerados automaticamente para novos ativos de várias páginas.
* Ativos de várias páginas existentes: Execute manualmente o fluxo de trabalho Atualizar ativos [!UICONTROL do] DAM seguindo uma das etapas:

   * Selecione um ativo e clique em [!UICONTROL Linha do tempo] para abrir o painel esquerdo. Como alternativa, use o atalho do teclado `alt + 3`. Clique em Fluxo de trabalho [!UICONTROL do]Start, selecione Ativo [!UICONTROL de atualização]DAM, clique em [!UICONTROL Start]e em [!UICONTROL Prosseguir].
   * Selecione um ativo e clique em [!UICONTROL Criar > Fluxo de trabalho] na barra de ferramentas. Na caixa de diálogo pop-up, selecione Fluxo de trabalho [!UICONTROL DAM Update Asset (Atualizar ativo] DAM), clique em [!UICONTROL Start]e em [!UICONTROL Continue (Continuar]).

Especificamente para documentos do Microsoft Word, execute o fluxo de trabalho de Documentos **[!UICONTROL do]** DAM Parse Word. Ele gera um `cq:Page` componente do conteúdo do documento do Microsoft Word. As imagens extraídas do documento são referenciadas do `cq:Page` componente. Essas imagens são extraídas mesmo se a geração de subativos estiver desativada.

## View subassets {#viewing-subassets}

Os subativos são exibidos somente se os subativos forem gerados e estiverem disponíveis para o ativo multipáginas selecionado. Para visualização dos subativos gerados, abra o ativo de várias páginas. Na área superior esquerda da página, clique no ícone ![Painel](assets/do-not-localize/aem_leftrail_contentonly.png) esquerdo e clique em **[!UICONTROL Subativos]** na lista. Quando você seleciona **[!UICONTROL Subativos]** na lista. Como alternativa, use o atalho do teclado `alt + 5`.

![Visualização de subativos para um ativo de várias páginas](assets/view_subassets_simulation.gif)

## páginas de Visualização de um arquivo de várias páginas {#view-pages-of-a-multi-page-file}

É possível visualização de um arquivo de várias páginas, como PDF, INDD, PPT, PPTX e AI, usando o recurso Visualizador de página de [!DNL Experience Manager Assets]. Abra um ativo de várias páginas e clique em Páginas **[!UICONTROL de]** Visualização no canto superior esquerdo da página. O Visualizador de página que é aberto exibe as páginas do ativo e os controles para navegar e aplicar zoom em cada página.

![Visualização e visualização de páginas de um ativo de várias páginas](assets/view_multipage_asset_fmr.gif)

Para [!DNL InDesign], você pode extrair páginas usando [!DNL InDesign Server]. Se as pré-visualizações das páginas forem salvas durante a criação do [!DNL InDesign] arquivo, então não [!DNL InDesign Server] será necessário para a extração da página.

As seguintes opções estão disponíveis na barra de ferramentas, no painel esquerdo e nos controles do Visualizador de páginas:

* **[!UICONTROL Ações]** da área de trabalho para abrir ou revelar um subativo específico usando o aplicativo da [!DNL Experience Manager] área de trabalho. Veja como [configurar as ações](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2) da área de trabalho se você estiver usando o aplicativo da [!DNL Experience Manager] área de trabalho.

* **[!UICONTROL A opção Propriedades]** abre a página [!UICONTROL Propriedades] do subativo específico.

* **[!UICONTROL A opção Anotar]** permite que você anote o subativo específico. As anotações usadas em subativos separados são coletadas e exibidas juntas quando o ativo pai é aberto para exibição.

* **[!UICONTROL A opção Visão geral]** da página exibe todos os subativos simultaneamente.

* **[!UICONTROL A opção Linha do tempo]** do painel esquerdo depois de clicar no ícone ![do painel](assets/do-not-localize/aem_leftrail_contentonly.png) esquerdo exibe o fluxo de atividade do arquivo.

>[!MORELIKETHIS]
>
>* [Usar o aplicativo de desktop Adobe Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)
>* [Configurar ações da área de trabalho no Adobe Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Criar objetos inteligentes vinculados no Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Inserir gráficos no Adobe InDesign](https://helpx.adobe.com/indesign/using/placing-graphics.html)