---
title: Gerenciar ativos compostos com referências e várias páginas
description: Saiba como criar referências a ativos digitais no [!DNL Adobe InDesign], [!DNL Adobe Illustrator]e [!DNL Adobe Photoshop]. Use o recurso Visualizador de página para exibir páginas de subativos individuais de arquivos de várias páginas, como arquivos PDF, INDD, PPT, PPTX e AI.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: 79d8b5896f5f8eb7a22dccea81acf0656d435f2b
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 0%

---

# Gerenciar ativos compostos e de várias páginas {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] pode identificar se um arquivo carregado contém referências a ativos que já existem no repositório. Esse recurso está disponível somente para formatos de arquivo compatíveis. Se o ativo carregado contiver referências a [!DNL Experience Manager] ativos, um link bidirecional é criado entre os ativos carregados e referenciados.

Além de eliminar a redundância, faça referência aos ativos em [!DNL Adobe Creative Cloud] aplicativos aumentam a colaboração e a eficiência e produtividade dos usuários.

[!DNL Experience Manager Assets] O suporta referência bidirecional. Você pode encontrar ativos referenciados na página de detalhes do ativo do arquivo carregado. Além disso, é possível exibir os arquivos de referência na página de detalhes do ativo do ativo referenciado.

As referências são resolvidas com base no caminho, na ID do documento e na ID da instância dos ativos referenciados.

## [!DNL Adobe Illustrator]: Adicionar ativos digitais como referências {#refai}

Você pode fazer referência a ativos digitais existentes em um [!DNL Adobe Illustrator] arquivo.

1. Usando [[!DNL Experience Manager] aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html), busque os ativos digitais no sistema de arquivos local. Navegue até o local do sistema de arquivos do ativo que deseja referenciar.
1. Arraste o ativo da pasta local para o [!DNL Illustrator] arquivo.

1. Salve as [!DNL Illustrator] à unidade montada, ou [fazer upload](/help/assets/manage-assets.md#uploading-assets) para [!DNL Experience Manager] repositório.

1. Depois que o fluxo de trabalho for concluído, acesse a página de detalhes do ativo. As referências aos ativos digitais existentes estão listadas em **[!UICONTROL Dependências]** no **[!UICONTROL Referências]** coluna.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Os ativos referenciados que aparecem em **[!UICONTROL Dependências]** também pode ser referenciado por arquivos diferentes do atual. Para exibir uma lista de arquivos de referência para um ativo, clique no ativo em **[!UICONTROL Dependências]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Clique em **[!UICONTROL Propriedades da exibição]** na barra de ferramentas. No [!UICONTROL Propriedades] página, a lista de arquivos que fazem referência ao ativo atual é exibida sob a **[!UICONTROL Referências]** na coluna **[!UICONTROL Básico]** guia .

   ![exibir as referências do Experience Manager Assets na coluna Referências em detalhes do ativo](assets/asset-references.png)

   *Figura: Referências de ativos nos detalhes do ativo.*

## [!DNL Adobe InDesign]: Adicionar ativos digitais como referências {#add-aem-assets-as-references-in-adobe-indesign}

Para fazer referência a ativos digitais em uma [!DNL InDesign] , arraste os ativos para a [!DNL InDesign] ou exporte o [!DNL InDesign] arquivo como arquivo ZIP.

Os ativos referenciados já existem em [!DNL Experience Manager Assets]. Você pode extrair subativos ao [configuração do InDesign Server](indesign.md). Ativos incorporados em um [!DNL InDesign] são extraídos como subativos.

>[!NOTE]
>
>Se a variável [!DNL InDesign Server] é proxy, [!DNL InDesign] os arquivos têm a visualização incorporada nos metadados de XMP. Nesse caso, a extração em miniatura não é explicitamente necessária. No entanto, se a variável [!DNL InDesign Server] não for proxy, as miniaturas devem ser explicitamente extraídas para [!DNL InDesign] arquivos.

Quando um arquivo INDD é carregado, as referências são buscadas consultando os ativos com `xmpMM:InstanceID` e `xmpMM:DocumentID` no repositório.

### Criar referências arrastando ativos {#create-references-by-dragging-aem-assets}

Este procedimento é semelhante a [adicionar ativos digitais como referências no Adobe Illustrator](#refai).

### Criar referências a ativos exportando um arquivo ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Execute as etapas em [Criar modelos de fluxo de trabalho](/help/sites-developing/workflows-models.md) para criar um novo workflow.
1. Use o [Recurso de pacote](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) de [!DNL Adobe InDesign] para exportar o documento. [!DNL Adobe InDesign] pode exportar um documento e os ativos vinculados como um pacote. Nesse caso, a pasta exportada contém um `Links` pasta que contém subativos na [!DNL InDesign] arquivo. O `Links` está presente na mesma pasta que o arquivo INDD.
1. Crie um arquivo ZIP e faça upload dele para o [!DNL Experience Manager] repositório.
1. Inicie o `Unarchiver` fluxo de trabalho.
1. Quando o fluxo de trabalho é concluído, as referências na pasta Links são automaticamente referenciadas como subativos. Para exibir uma lista dos ativos referenciados, navegue até a página de detalhes do ativo do [!DNL InDesign] e fechar o [Trilho](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: Adicionar ativos digitais como referências {#refps}

1. Use [!DNL Experience Manager] aplicativo de desktop para acessar [!DNL Experience Manager Assets]. Baixe e revele os ativos no sistema de arquivos local. Use o [!UICONTROL Local vinculado] em [!DNL Adobe Photoshop]. Consulte [colocar ativos no aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. Salvar em [!DNL Photoshop] à unidade montada ou [fazer upload](/help/assets/manage-assets.md#uploading-assets) para [!DNL Experience Manager] repositório.
1. Após a conclusão do workflow, as referências a [!DNL Experience Manager] os ativos são listados na página de detalhes do ativo.

   Para exibir os ativos referenciados, feche o [Trilho](/help/sites-authoring/basic-handling.md#rail-selector) na página de detalhes do ativo.

1. Os ativos referenciados também contêm a lista de ativos dos quais são referenciados. Para exibir uma lista de ativos referenciados, navegue até a página de detalhes do ativo e feche o [Trilho](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>Os ativos em ativos compostos também podem ser referenciados com base na ID do documento e na ID da instância. Essa funcionalidade está disponível com [!DNL Adobe Illustrator] e [!DNL Adobe Photoshop] somente versões. Para outros, a referência é feita com base no caminho relativo de ativos vinculados no ativo composto principal, conforme feito em versões anteriores do [!DNL Experience Manager].

## Criar subativos {#generate-subassets}

Para os ativos compatíveis com formatos de várias páginas — arquivos PDF, arquivos AI, [!DNL Microsoft PowerPoint] e [!DNL Apple Keynote] arquivos e [!DNL Adobe InDesign] arquivos — [!DNL Experience Manager] pode gerar subativos que correspondem a cada página individual do ativo original. Esses subativos estão vinculados ao *parent* e facilitar a visualização de várias páginas. Para todos os outros fins, os ativos secundários são tratados como ativos normais em [!DNL Experience Manager].

A geração de subconjunto é desabilitada por padrão. Para ativar a geração de subativos, siga estas etapas:

1. Faça logon [!DNL Experience Manager] como administrador. Acesso **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Selecionar **[!UICONTROL Ativo de atualização DAM]** e clique em **[!UICONTROL Editar]**.
1. Clique em **[!UICONTROL Alternar painel lateral]** e localize a **[!UICONTROL Criar sub-ativo]** etapa. Adicione a etapa ao workflow. Clique em **[!UICONTROL Sincronizar]**.

Para gerar os subativos, siga um destes procedimentos:

* Novos ativos: O [!UICONTROL Ativos de atualização do DAM] O fluxo de trabalho é executado em qualquer novo ativo carregado para [!DNL Experience Manager]. Os subativos são gerados automaticamente para novos ativos de várias páginas.
* Ativos de várias páginas existentes: Execute manualmente o [!UICONTROL Ativos de atualização do DAM] fluxo de trabalho seguindo uma das etapas:

   * Selecione um ativo e clique em [!UICONTROL Linha do tempo] para abrir o painel esquerdo. Como alternativa, use o atalho do teclado `alt + 3`. Clique em [!UICONTROL Iniciar fluxo de trabalho], selecione [!UICONTROL Ativo de atualização DAM], clique em [!UICONTROL Iniciar]e clique em [!UICONTROL Continue].
   * Selecione um ativo e clique em [!UICONTROL Criar] > [!UICONTROL Fluxo de trabalho] na barra de ferramentas. Na caixa de diálogo pop-up, selecione [!UICONTROL Ativo de atualização DAM] do fluxo de trabalho, clique em [!UICONTROL Iniciar]e clique em [!UICONTROL Continue].

Especificamente para documentos do Microsoft Word, execute o **[!UICONTROL Documentos de Palavra de Análise do DAM]** fluxo de trabalho. Ele gera um `cq:Page` do conteúdo do documento do Microsoft Word. As imagens extraídas do documento são referenciadas da `cq:Page` componente. Essas imagens são extraídas mesmo se a geração de sub-ativos estiver desativada.

>[!NOTE]
>
>No [!UICONTROL Criar processo de subativo - Propriedades da etapa] em [!UICONTROL Argumentos do processo], é possível especificar o número de subativos que [!DNL Experience Manager] gera. O valor padrão é 5. Para gerar todos os subativos, deixe o campo vazio. Se o campo tiver um valor negativo, nenhum subativo será gerado.

## Exibir subativos {#viewing-subassets}

Os subativos são exibidos somente se os subativos forem gerados e estiverem disponíveis para o ativo de várias páginas selecionado. Para exibir os subativos gerados, abra o ativo de várias páginas. Na área superior esquerda da página, clique em ![Opção para abrir o painel esquerdo](assets/do-not-localize/aem_leftrail_contentonly.png) e clique em **[!UICONTROL Subativos]** na lista. Ao selecionar **[!UICONTROL Subativos]** na lista. Como alternativa, use o atalho do teclado `alt + 5`.

![Exibir subativos para um ativo de várias páginas](assets/view_subassets_simulation.gif)

## Exibir páginas de um arquivo de várias páginas {#view-pages-of-a-multi-page-file}

Você pode visualizar um arquivo de várias páginas, como PDF, INDD, PPT, PPTX e AI, usando o recurso Visualizador de página de [!DNL Experience Manager Assets]. Abra um ativo de várias páginas e clique em **[!UICONTROL Exibir páginas]** no canto superior esquerdo da página. O Visualizador de página que é aberto exibe as páginas do ativo e os controles para navegar e aplicar zoom a cada página.

![Exibir e ver páginas de um ativo de várias páginas](assets/view_multipage_asset_fmr.gif)

Para [!DNL InDesign], você pode extrair páginas usando [!DNL InDesign Server]. Se as visualizações de páginas forem salvas durante [!DNL InDesign] criação do arquivo e [!DNL InDesign Server] não é necessário para extração de página.

As seguintes opções estão disponíveis na barra de ferramentas, no painel à esquerda e nos controles do Visualizador de páginas:

* **[!UICONTROL Ações da área de trabalho]** para abrir ou revelar um subativo específico usando [!DNL Experience Manager] aplicativo de desktop. Veja como [configurar ações do desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) se estiver usando [!DNL Experience Manager] aplicativo de desktop.

* **[!UICONTROL Propriedades]** abre a opção [!UICONTROL Propriedades] página do subativo específico.

* **[!UICONTROL Anotar]** permite anotar o subativo específico. As anotações usadas em subativos separados são coletadas e exibidas juntas quando o ativo principal é aberto para exibição.

* **[!UICONTROL Visão geral da página]** exibe todos os subativos simultaneamente.

* **[!UICONTROL Linha do tempo]** no painel esquerdo depois de clicar ![Opção para abrir o painel esquerdo](assets/do-not-localize/aem_leftrail_contentonly.png) exibe o fluxo de atividade do arquivo.

## Práticas recomendadas e limitação {#best-practice-limitation-tips}

* A geração de subconjunto pode consumir muitos recursos em qualquer [!DNL Experience Manager] implantação. Se você estiver gerando subativos quando ativos complexos forem carregados, adicione a etapa no fluxo de trabalho Ativo de atualização DAM . Se você estiver gerando subativos sob demanda, crie um workflow separado para gerar subativos. Um fluxo de trabalho dedicado permite ignorar as outras etapas no fluxo de trabalho Ativo de atualização DAM e salvar recursos computacionais.

>[!MORELIKETHIS]
>
>* [Usar o aplicativo de desktop do Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Configurar ações da área de trabalho no Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Criar objetos inteligentes vinculados no Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Colocar gráficos no Adobe InDesign](https://helpx.adobe.com/indesign/using/placing-graphics.html)

