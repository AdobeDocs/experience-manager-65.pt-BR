---
title: Gerenciar ativos compostos com referências e várias páginas
description: Saiba como criar referências a ativos digitais de dentro de [!DNL Adobe InDesign], [!DNL Adobe Illustrator], and [!DNL Adobe Photoshop]. Use o recurso Visualizador de página para exibir páginas de subativos individuais de arquivos de várias páginas, como arquivos PDF, INDD, PPT, PPTX e AI.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: 79d8b5896f5f8eb7a22dccea81acf0656d435f2b
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 0%

---

# Gerenciar ativos compostos e de várias páginas {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] pode identificar se um arquivo carregado contém referências a ativos que já existem no repositório. Esse recurso está disponível somente para formatos de arquivo compatíveis. Se o ativo carregado contiver qualquer referência a [!DNL Experience Manager] ativos, um link bidirecional será criado entre os ativos carregados e referenciados.

Além de eliminar a redundância, referenciar os ativos em [!DNL Adobe Creative Cloud] aplicativos melhora a colaboração e aumenta a eficiência e a produtividade dos usuários.

[!DNL Experience Manager Assets] O suporta referência bidirecional. Você pode encontrar ativos referenciados na página de detalhes do ativo do arquivo carregado. Além disso, é possível exibir os arquivos de referência na página de detalhes do ativo do ativo referenciado.

As referências são resolvidas com base no caminho, na ID do documento e na ID da instância dos ativos referenciados.

## [!DNL Adobe Illustrator]: Adicionar ativos digitais como referências {#refai}

Você pode fazer referência a ativos digitais existentes em um arquivo [!DNL Adobe Illustrator].

1. Usando [[!DNL Experience Manager] aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html), busque os ativos digitais no sistema de arquivos local. Navegue até o local do sistema de arquivos do ativo que deseja referenciar.
1. Arraste o ativo da pasta local para o arquivo [!DNL Illustrator].

1. Salve o arquivo [!DNL Illustrator] na unidade montada ou [carregue](/help/assets/manage-assets.md#uploading-assets) no repositório [!DNL Experience Manager].

1. Depois que o fluxo de trabalho for concluído, acesse a página de detalhes do ativo. As referências a ativos digitais existentes são listadas em **[!UICONTROL Dependências]** na coluna **[!UICONTROL Referências]**.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Os ativos referenciados que aparecem em **[!UICONTROL Dependências]** também podem ser referenciados por arquivos diferentes do atual. Para exibir uma lista de arquivos de referência para um ativo, clique no ativo em **[!UICONTROL Dependências]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Clique em **[!UICONTROL Exibir propriedades]** na barra de ferramentas. Na página [!UICONTROL Properties], a lista de arquivos que fazem referência ao ativo atual aparece na coluna **[!UICONTROL References]** na guia **[!UICONTROL Basic]**.

   ![exibir as referências dos ativos Experience Manager na coluna Referências em detalhes do ativo](assets/asset-references.png)

   *Figura: Referências de ativos nos detalhes do ativo.*

## [!DNL Adobe InDesign]: Adicionar ativos digitais como referências {#add-aem-assets-as-references-in-adobe-indesign}

Para fazer referência a ativos digitais em um arquivo [!DNL InDesign], arraste os ativos para o arquivo [!DNL InDesign] ou exporte o arquivo [!DNL InDesign] como um arquivo ZIP.

Os ativos referenciados já existem em [!DNL Experience Manager Assets]. Você pode extrair subativos ao configurar o InDesign Server](indesign.md). [ Os ativos incorporados em um arquivo [!DNL InDesign] são extraídos como subativos.

>[!NOTE]
>
>Se [!DNL InDesign Server] for enviado por proxy, os arquivos [!DNL InDesign] terão sua visualização incorporada aos metadados XMP. Nesse caso, a extração em miniatura não é explicitamente necessária. No entanto, se [!DNL InDesign Server] não for proxy, as miniaturas deverão ser extraídas explicitamente para arquivos [!DNL InDesign].

Quando um arquivo INDD é carregado, as referências são buscadas consultando ativos com as propriedades `xmpMM:InstanceID` e `xmpMM:DocumentID` no repositório.

### Criar referências arrastando ativos {#create-references-by-dragging-aem-assets}

Esse procedimento é semelhante a [adicionar ativos digitais como referências no Adobe Illustrator](#refai).

### Criar referências a ativos exportando um arquivo ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Execute as etapas em [Criar modelos de fluxo de trabalho](/help/sites-developing/workflows-models.md) para criar um novo fluxo de trabalho.
1. Use o [recurso do pacote](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) de [!DNL Adobe InDesign] para exportar o documento. [!DNL Adobe InDesign] pode exportar um documento e os ativos vinculados como um pacote. Nesse caso, a pasta exportada contém uma pasta `Links` que contém subativos no arquivo [!DNL InDesign]. A pasta `Links` está presente na mesma pasta que o arquivo INDD.
1. Crie um arquivo ZIP e faça upload dele para o repositório [!DNL Experience Manager].
1. Inicie o workflow `Unarchiver`.
1. Quando o fluxo de trabalho é concluído, as referências na pasta Links são automaticamente referenciadas como subativos. Para exibir uma lista de ativos referenciados, navegue até a página de detalhes do ativo [!DNL InDesign] e feche o [Painel](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: Adicionar ativos digitais como referências {#refps}

1. Use o [!DNL Experience Manager] aplicativo de desktop para acessar [!DNL Experience Manager Assets]. Baixe e revele os ativos no sistema de arquivos local. Use a funcionalidade [!UICONTROL Colocar Linked] em [!DNL Adobe Photoshop]. Consulte [colocar ativos no aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. Salve no arquivo [!DNL Photoshop] na unidade montada ou [carregue](/help/assets/manage-assets.md#uploading-assets) no repositório [!DNL Experience Manager].
1. Após a conclusão do fluxo de trabalho, as referências aos ativos [!DNL Experience Manager] existentes são listadas na página de detalhes do ativo.

   Para exibir os ativos referenciados, feche o [Trilho](/help/sites-authoring/basic-handling.md#rail-selector) na página de detalhes do ativo.

1. Os ativos referenciados também contêm a lista de ativos dos quais são referenciados. Para exibir uma lista de ativos referenciados, navegue até a página de detalhes do ativo e feche o [Trilho](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>Os ativos em ativos compostos também podem ser referenciados com base na ID do documento e na ID da instância. Essa funcionalidade está disponível somente com as versões [!DNL Adobe Illustrator] e [!DNL Adobe Photoshop]. Para outros, a referência é feita com base no caminho relativo de ativos vinculados no ativo composto principal, conforme feito em versões anteriores de [!DNL Experience Manager].

## Criar subativos {#generate-subassets}

Para os ativos suportados com formatos de várias páginas — arquivos PDF, arquivos AI, arquivos [!DNL Microsoft PowerPoint] e [!DNL Apple Keynote] e arquivos [!DNL Adobe InDesign] — [!DNL Experience Manager] pode gerar subativos que correspondem a cada página individual do ativo original. Esses subativos estão vinculados ao ativo *principal* e facilitam a visualização de várias páginas. Para todos os outros fins, os subativos são tratados como ativos normais em [!DNL Experience Manager].

A geração de subconjunto é desabilitada por padrão. Para ativar a geração de subativos, siga estas etapas:

1. Faça logon em [!DNL Experience Manager] como administrador. Acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Selecione **[!UICONTROL Ativo de atualização do DAM]** e clique em **[!UICONTROL Editar]**.
1. Clique em **[!UICONTROL Alternar painel lateral]** e localize a etapa **[!UICONTROL Criar subativo]**. Adicione a etapa ao workflow. Clique em **[!UICONTROL Sincronizar]**.

Para gerar os subativos, siga um destes procedimentos:

* Novos ativos: O workflow [!UICONTROL Ativos de atualização do DAM] é executado em qualquer novo ativo que seja carregado para [!DNL Experience Manager]. Os subativos são gerados automaticamente para novos ativos de várias páginas.
* Ativos de várias páginas existentes: Execute manualmente o fluxo de trabalho [!UICONTROL Atualizar ativos do DAM] seguindo uma das etapas:

   * Selecione um ativo e clique em [!UICONTROL Linha do tempo] para abrir o painel esquerdo. Como alternativa, use o atalho de teclado `alt + 3`. Clique em [!UICONTROL Iniciar Fluxo de Trabalho], selecione [!UICONTROL Ativo de Atualização DAM], clique em [!UICONTROL Iniciar] e clique em [!UICONTROL Continuar].
   * Selecione um ativo e clique em [!UICONTROL Create] > [!UICONTROL Workflow] na barra de ferramentas. Na caixa de diálogo pop-up, selecione [!UICONTROL DAM Update Asset] fluxo de trabalho, clique em [!UICONTROL Iniciar] e clique em [!UICONTROL Continuar].

Especificamente para documentos do Microsoft Word, execute o workflow **[!UICONTROL Documentos do DAM Parse Word]**. Ele gera um componente `cq:Page` do conteúdo do documento do Microsoft Word. As imagens extraídas do documento são referenciadas do componente `cq:Page`. Essas imagens são extraídas mesmo se a geração de sub-ativos estiver desativada.

>[!NOTE]
>
>No [!UICONTROL Create Sub Asset Process - Step Properties] em [!UICONTROL Process Arguments], você pode especificar o número de sub-ativos gerados por [!DNL Experience Manager]. O valor padrão é 5. Para gerar todos os subativos, deixe o campo vazio. Se o campo tiver um valor negativo, nenhum subativo será gerado.

## Exibir subativos {#viewing-subassets}

Os subativos são exibidos somente se os subativos forem gerados e estiverem disponíveis para o ativo de várias páginas selecionado. Para exibir os subativos gerados, abra o ativo de várias páginas. Na área superior esquerda da página, clique em ![Option para abrir o painel à esquerda](assets/do-not-localize/aem_leftrail_contentonly.png) e clique em **[!UICONTROL Subassets]** na lista. Ao selecionar **[!UICONTROL Subassets]** na lista. Como alternativa, use o atalho de teclado `alt + 5`.

![Exibir subativos para um ativo de várias páginas](assets/view_subassets_simulation.gif)

## Exibir páginas de um arquivo de várias páginas {#view-pages-of-a-multi-page-file}

Você pode visualizar um arquivo de várias páginas, como PDF, INDD, PPT, PPTX e arquivo AI, usando o recurso Visualizador de página de [!DNL Experience Manager Assets]. Abra um ativo de várias páginas e clique em **[!UICONTROL Exibir páginas]** no canto superior esquerdo da página. O Visualizador de página que é aberto exibe as páginas do ativo e os controles para navegar e aplicar zoom a cada página.

![Exibir e ver páginas de um ativo de várias páginas](assets/view_multipage_asset_fmr.gif)

Para [!DNL InDesign], você pode extrair páginas usando [!DNL InDesign Server]. Se as visualizações de páginas forem salvas durante a criação do arquivo [!DNL InDesign], [!DNL InDesign Server] não será necessário para a extração de página.

As seguintes opções estão disponíveis na barra de ferramentas, no painel à esquerda e nos controles do Visualizador de páginas:

* **[!UICONTROL As]** ações da área de trabalho para abrir ou revelar um subativo específico usando o aplicativo da  [!DNL Experience Manager] área de trabalho. Consulte como [configurar as Ações da Área de Trabalho](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) se estiver usando o [!DNL Experience Manager] aplicativo de área de trabalho.

* **** A opção Propriedades abre a   página Propriedades do subativo específico.

* **** A opção Anotar permite anotar o subativo específico. As anotações usadas em subativos separados são coletadas e exibidas juntas quando o ativo principal é aberto para exibição.

* **[!UICONTROL A opção]** Visão geral da página exibe todos os subativos simultaneamente.

* **** A opção Linha do tempo no painel esquerdo depois de clicar em  ![Opção para abrir o ](assets/do-not-localize/aem_leftrail_contentonly.png) painel esquerdo exibe o fluxo de atividade do arquivo.

## Práticas recomendadas e limitação {#best-practice-limitation-tips}

* A geração de subconjunto pode consumir muitos recursos em qualquer implantação [!DNL Experience Manager]. Se você estiver gerando subativos quando ativos complexos forem carregados, adicione a etapa no fluxo de trabalho Ativo de atualização DAM . Se você estiver gerando subativos sob demanda, crie um workflow separado para gerar subativos. Um fluxo de trabalho dedicado permite ignorar as outras etapas no fluxo de trabalho Ativo de atualização DAM e salvar recursos computacionais.

>[!MORELIKETHIS]
>
>* [Usar o aplicativo de desktop do Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Configurar ações da área de trabalho no Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Criar objetos inteligentes vinculados no Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Colocar gráficos no Adobe InDesign](https://helpx.adobe.com/indesign/using/placing-graphics.html)

