---
title: Gerenciar ativos compostos com referências e várias páginas
description: Saiba como criar referências a ativos digitais no  [!DNL Adobe InDesign], [!DNL Adobe Illustrator] e [!DNL Adobe Photoshop]. Use o recurso Visualizador de páginas para exibir páginas de subativos individuais de arquivos de várias páginas, como arquivos PDF, INDD, PPT, PPTX e AI.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 0%

---

# Gerenciar ativos compostos e de várias páginas {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] pode identificar se um arquivo carregado contém referências a ativos que já existem no repositório. Esse recurso está disponível somente para formatos de arquivo compatíveis. Se o ativo carregado contiver referências a [!DNL Experience Manager] ativos, um link bidirecional será criado entre os ativos carregados e referenciados.

Além de eliminar a redundância, a referência aos ativos nos aplicativos do [!DNL Adobe Creative Cloud] melhora a colaboração e aumenta a eficiência e a produtividade dos usuários.

[!DNL Experience Manager Assets] dá suporte à referência bidirecional. Você pode encontrar ativos referenciados na página de detalhes do ativo do arquivo carregado. Além disso, é possível exibir os arquivos de referência na página de detalhes do ativo do ativo referenciado.

As referências são resolvidas com base no caminho, na ID do documento e na ID da instância dos ativos referenciados.

## [!DNL Adobe Illustrator]: adicionar ativos digitais como referências {#refai}

Você pode fazer referência a ativos digitais existentes em um arquivo do [!DNL Adobe Illustrator].

1. Usando o [[!DNL Experience Manager] aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html), busque os ativos digitais no sistema de arquivos local. Navegue até o local do sistema de arquivos do ativo que deseja referenciar.
1. Arraste o ativo da pasta local para o arquivo [!DNL Illustrator].

1. Salve o arquivo [!DNL Illustrator] na unidade montada ou [carregue](/help/assets/manage-assets.md#uploading-assets) no repositório [!DNL Experience Manager].

1. Depois que o fluxo de trabalho for concluído, acesse a página de detalhes do ativo. As referências a ativos digitais existentes estão listadas em **[!UICONTROL Dependências]** na coluna **[!UICONTROL Referências]**.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Os ativos referenciados que aparecem em **[!UICONTROL Dependências]** também podem ser referenciados por arquivos diferentes do atual. Para exibir uma lista de arquivos de referência para um ativo, clique no ativo em **[!UICONTROL Dependências]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Clique em **[!UICONTROL Exibir Propriedades]** na barra de ferramentas. Na página [!UICONTROL Propriedades], a lista de arquivos que fazem referência ao ativo atual aparece na coluna **[!UICONTROL Referências]** da guia **[!UICONTROL Básico]**.

   ![exibir as referências do Experience Manager Assets na coluna Referências nos detalhes do ativo](assets/asset-references.png)

   *Figura: referências do ativo nos detalhes do ativo.*

## [!DNL Adobe InDesign]: adicionar ativos digitais como referências {#add-aem-assets-as-references-in-adobe-indesign}

Para fazer referência a ativos digitais de um arquivo [!DNL InDesign], arraste os ativos para o arquivo [!DNL InDesign] ou exporte o arquivo [!DNL InDesign] como um arquivo ZIP.

Os ativos referenciados já existem em [!DNL Experience Manager Assets]. Você pode extrair subativos [configurando o InDesign Server](indesign.md). Os ativos inseridos em um arquivo [!DNL InDesign] são extraídos como subativos.

>[!NOTE]
>
>Se o [!DNL InDesign Server] for encaminhado por proxy, [!DNL InDesign] os arquivos terão sua visualização incorporada aos metadados XMP. Nesse caso, a extração de miniaturas não é explicitamente necessária. No entanto, se [!DNL InDesign Server] não for intermediado por proxy, as miniaturas deverão ser explicitamente extraídas para os arquivos [!DNL InDesign].

Quando um arquivo INDD é carregado, as referências são buscadas consultando ativos com as propriedades `xmpMM:InstanceID` e `xmpMM:DocumentID` no repositório.

### Criar referências ao arrastar ativos {#create-references-by-dragging-aem-assets}

Este procedimento é semelhante a [adicionar ativos digitais como referências no Adobe Illustrator](#refai).

### Criar referências a ativos exportando um arquivo ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Execute as etapas em [Criar modelos de fluxo de trabalho](/help/sites-developing/workflows-models.md) para criar um fluxo de trabalho.
1. Use o [recurso Pacote](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) de [!DNL Adobe InDesign] para exportar o documento. [!DNL Adobe InDesign] pode exportar um documento e os ativos vinculados como um pacote. Nesse caso, a pasta exportada contém uma pasta `Links` que contém subativos no arquivo [!DNL InDesign]. A pasta `Links` está presente na mesma pasta que o arquivo INDD.
1. Crie um arquivo ZIP e carregue-o no repositório [!DNL Experience Manager].
1. Inicie o fluxo de trabalho `Unarchiver`.
1. Quando o fluxo de trabalho é concluído, as referências na pasta Links são automaticamente referenciadas como subativos. Para exibir uma lista de ativos referenciados, navegue até a página de detalhes do ativo [!DNL InDesign] e feche o [Painel](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: adicionar ativos digitais como referências {#refps}

1. Use o aplicativo de desktop [!DNL Experience Manager] para acessar [!DNL Experience Manager Assets]. Baixe e revele os ativos no sistema de arquivos local. Usar a funcionalidade [!UICONTROL Colocar Vinculado] em [!DNL Adobe Photoshop]. Consulte [colocar ativos no aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. Salve no arquivo [!DNL Photoshop] na unidade montada ou [carregue](/help/assets/manage-assets.md#uploading-assets) no repositório [!DNL Experience Manager].
1. Após a conclusão do fluxo de trabalho, as referências aos [!DNL Experience Manager] ativos existentes são listadas na página de detalhes do ativo.

   Para exibir os ativos referenciados, feche o [Painel](/help/sites-authoring/basic-handling.md#rail-selector) na página de detalhes do ativo.

1. Os ativos referenciados também contêm a lista de ativos dos quais eles são referenciados. Para exibir uma lista de ativos referenciados, navegue até a página de detalhes do ativo e feche o [Painel](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>Os ativos nos ativos compostos também podem ser referenciados com base na ID do documento e na ID da instância. Esta funcionalidade está disponível somente com as versões [!DNL Adobe Illustrator] e [!DNL Adobe Photoshop]. Para outros, a referência é feita com base no caminho relativo de ativos vinculados no ativo composto principal, conforme feito em versões anteriores do [!DNL Experience Manager].

## Criar subativos {#generate-subassets}

Para os ativos compatíveis com formatos de várias páginas — arquivos PDF, arquivos AI, [!DNL Microsoft PowerPoint] e [!DNL Apple Keynote] arquivos e [!DNL Adobe InDesign] arquivos — o [!DNL Experience Manager] pode gerar subativos que correspondem a cada página individual do ativo original. Estes subativos estão vinculados ao ativo *pai* e facilitam a exibição de várias páginas. Para todos os outros fins, os subativos são tratados como ativos normais no [!DNL Experience Manager].

A geração de subativos está desativada por padrão. Para habilitar a geração de subativos, siga estas etapas:

1. Entre em [!DNL Experience Manager] como administrador. Acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de Trabalho]** > **[!UICONTROL Modelos]**.
1. Selecione o fluxo de trabalho **[!UICONTROL Ativo de atualização do DAM]** e clique em **[!UICONTROL Editar]**.
1. Clique em **[!UICONTROL Alternar painel lateral]** e localize a etapa **[!UICONTROL Criar subativo]**. Adicione a etapa ao fluxo de trabalho. Clique em **[!UICONTROL Sincronizar]**.

Para gerar os subativos, siga um destes procedimentos:

* Novos ativos: o fluxo de trabalho [!UICONTROL Atualização DAM do Assets] é executado em qualquer novo ativo que seja carregado para [!DNL Experience Manager]. Os subativos são gerados automaticamente para novos ativos de várias páginas.
* Ativos de várias páginas existentes: execute manualmente o fluxo de trabalho [!UICONTROL DAM Atualizar Assets] seguindo uma das etapas:

   * Selecione um ativo e clique em [!UICONTROL Linha do tempo] para abrir o painel esquerdo. Como alternativa, use o atalho de teclado `alt + 3`. Clique em [!UICONTROL Iniciar fluxo de trabalho], selecione [!UICONTROL Ativo de atualização do DAM], clique em [!UICONTROL Iniciar] e em [!UICONTROL Continuar].
   * Selecione um ativo e clique em [!UICONTROL Criar] > [!UICONTROL Fluxo de trabalho] na barra de ferramentas. Na caixa de diálogo pop-up, selecione o fluxo de trabalho [!UICONTROL Ativo de atualização do DAM], clique em [!UICONTROL Iniciar] e em [!UICONTROL Continuar].

Especificamente para documentos do Microsoft Word, execute o fluxo de trabalho **[!UICONTROL Analisar documentos do Word]** do DAM. Ele gera um componente `cq:Page` a partir do conteúdo do documento do Microsoft Word. As imagens extraídas do documento são referenciadas do componente `cq:Page`. Essas imagens são extraídas mesmo se a geração de sub-ativos estiver desativada.

>[!NOTE]
>
>Em [!UICONTROL Criar processo de subativos - Propriedades da etapa] em [!UICONTROL Argumentos do processo], você pode especificar o número de subativos gerados por [!DNL Experience Manager]. O valor padrão é 5. Para gerar todos os ativos secundários, deixe o campo vazio. Se o campo tiver negativo, nenhum ativo secundário será gerado.

## Exibir subativos {#viewing-subassets}

Os ativos secundários são exibidos somente se os ativos secundários forem gerados e estiverem disponíveis para o ativo de várias páginas selecionado. Para exibir os subativos gerados, abra o ativo de várias páginas. Na área superior esquerda da página, clique em ![Opção para abrir o painel esquerdo](assets/do-not-localize/aem_leftrail_contentonly.png) e clique em **[!UICONTROL Subativos]** na lista. Ao selecionar **[!UICONTROL Subativos]** na lista. Como alternativa, use o atalho de teclado `alt + 5`.

![Exibir subativos para um ativo de várias páginas](assets/view_subassets_simulation.gif)

## Visualizar páginas de um arquivo de várias páginas {#view-pages-of-a-multi-page-file}

Você pode exibir um arquivo de várias páginas, como PDF, INDD, PPT, PPTX e arquivo AI, usando o recurso Visualizador de Páginas do [!DNL Experience Manager Assets]. Abra um ativo de várias páginas e clique em **[!UICONTROL Exibir páginas]** no canto superior esquerdo da página. O Visualizador de página aberto exibe as páginas do ativo e os controles para navegar e aplicar zoom em cada página.

![Exibir e ver páginas de um ativo de várias páginas](assets/view_multipage_asset_fmr.gif)

Para [!DNL InDesign], você pode extrair páginas usando [!DNL InDesign Server]. Se as visualizações de páginas forem salvas durante a criação do arquivo [!DNL InDesign], [!DNL InDesign Server] não será necessário para a extração de páginas.

As seguintes opções estão disponíveis na barra de ferramentas, no painel à esquerda e nos controles do Visualizador de páginas:

* **[!UICONTROL Ações da área de trabalho]** para abrir ou revelar um subativo específico usando o aplicativo de desktop [!DNL Experience Manager]. Veja como [configurar ações da área de trabalho](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) se estiver usando o aplicativo de área de trabalho [!DNL Experience Manager].

* A opção **[!UICONTROL Propriedades]** abre a página [!UICONTROL Propriedades] do subativo específico.

* A opção **[!UICONTROL Anotar]** permite anotar o subativo específico. As anotações usadas em subativos separados são coletadas e exibidas juntas quando o ativo principal é aberto para visualização.

* A opção **[!UICONTROL Visão geral da página]** exibe todos os subativos simultaneamente.

* A opção **[!UICONTROL Linha do Tempo]** no painel esquerdo depois de clicar em ![Opção para abrir o painel esquerdo](assets/do-not-localize/aem_leftrail_contentonly.png) exibe o fluxo de atividade para o arquivo.

## Práticas recomendadas e limitação {#best-practice-limitation-tips}

* A geração de subativos pode consumir muitos recursos em qualquer implantação do [!DNL Experience Manager]. Se você estiver gerando subativos quando ativos complexos forem carregados, adicione a etapa no fluxo de trabalho Atualizar ativo do DAM. Se você estiver gerando subativos sob demanda, crie um fluxo de trabalho separado para gerar subativos. Um fluxo de trabalho dedicado permite ignorar outras etapas no fluxo de trabalho Atualizar ativo do DAM e salvar recursos computacionais.

>[!MORELIKETHIS]
>
>* [Usar o aplicativo de desktop do Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Configurar Ações da Área de Trabalho no Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Criar Objetos Inteligentes Vinculados no Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Inserir elementos gráficos no Adobe InDesign](https://helpx.adobe.com/indesign/using/placing-graphics.html)
