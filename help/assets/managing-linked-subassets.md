---
title: Gerenciar ativos compostos com referências e várias páginas
description: Saiba como criar referências a ativos digitais dentro do [!DNL Adobe InDesign], [!DNL Adobe Illustrator], e [!DNL Adobe Photoshop]. Use o recurso Visualizador de páginas para exibir páginas de subativos individuais de arquivos de várias páginas, como arquivos PDF, INDD, PPT, PPTX e AI.
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

[!DNL Adobe Experience Manager Assets] O pode identificar se um arquivo carregado contém referências a ativos que já existem no repositório. Esse recurso está disponível somente para formatos de arquivo compatíveis. Se o ativo carregado contiver referências a [!DNL Experience Manager] ativos, um link bidirecional é criado entre os ativos carregados e referenciados.

Além de eliminar a redundância, fazer referência aos ativos em [!DNL Adobe Creative Cloud] Os aplicativos da melhoram a colaboração e aumentam a eficiência e a produtividade dos usuários.

[!DNL Experience Manager Assets] O oferece suporte à referência bidirecional. Você pode encontrar ativos referenciados na página de detalhes do ativo do arquivo carregado. Além disso, é possível exibir os arquivos de referência na página de detalhes do ativo do ativo referenciado.

As referências são resolvidas com base no caminho, na ID do documento e na ID da instância dos ativos referenciados.

## [!DNL Adobe Illustrator]: adicionar ativos digitais como referências {#refai}

Você pode fazer referência a ativos digitais existentes em um [!DNL Adobe Illustrator] arquivo.

1. Usar [[!DNL Experience Manager] aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html), busque os ativos digitais no sistema de arquivos local. Navegue até o local do sistema de arquivos do ativo que deseja referenciar.
1. Arraste o ativo da pasta local para a [!DNL Illustrator] arquivo.

1. Salve o [!DNL Illustrator] arquivo na unidade montada ou [upload](/help/assets/manage-assets.md#uploading-assets) para o [!DNL Experience Manager] repositório.

1. Depois que o fluxo de trabalho for concluído, acesse a página de detalhes do ativo. As referências aos ativos digitais existentes estão listadas em **[!UICONTROL Dependências]** no **[!UICONTROL Referências]** coluna.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Os ativos referenciados que aparecem em **[!UICONTROL Dependências]** também podem ser referenciados por arquivos diferentes do atual. Para exibir uma lista de arquivos de referência para um ativo, clique no ativo na em **[!UICONTROL Dependências]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Clique em **[!UICONTROL Propriedades da exibição]** na barra de ferramentas. No [!UICONTROL Propriedades] página, a lista de arquivos que fazem referência ao ativo atual aparece na **[!UICONTROL Referências]** na **[!UICONTROL Básico]** guia.

   ![exibir as referências do Experience Manager Assets na coluna Referências nos detalhes do ativo](assets/asset-references.png)

   *Figura: Referências de ativos nos detalhes do ativo.*

## [!DNL Adobe InDesign]: adicionar ativos digitais como referências {#add-aem-assets-as-references-in-adobe-indesign}

Para fazer referência a ativos digitais de dentro de um [!DNL InDesign] arquivo, arraste os ativos para a caixa [!DNL InDesign] arquive ou exporte o [!DNL InDesign] como um arquivo ZIP.

Os ativos referenciados já existem no [!DNL Experience Manager Assets]. Você pode extrair subativos ao [configuração do InDesign Server](indesign.md). Ativos incorporados em um [!DNL InDesign] arquivo são extraídos como subativos.

>[!NOTE]
>
>Se a variável [!DNL InDesign Server] é enviada por proxy, [!DNL InDesign] os arquivos têm sua pré-visualização incorporada aos metadados XMP. Nesse caso, a extração de miniaturas não é explicitamente necessária. No entanto, se a [!DNL InDesign Server] não for enviada por proxy, as miniaturas devem ser extraídas explicitamente para [!DNL InDesign] arquivos.

Quando um arquivo INDD é carregado, as referências são buscadas consultando ativos que têm `xmpMM:InstanceID` e `xmpMM:DocumentID` no repositório.

### Criar referências ao arrastar ativos {#create-references-by-dragging-aem-assets}

Esse procedimento é semelhante ao [adicionar ativos digitais como referências no Adobe Illustrator](#refai).

### Criar referências a ativos exportando um arquivo ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Execute as etapas em [Criar modelos de fluxo de trabalho](/help/sites-developing/workflows-models.md) para criar um workflow.
1. Use o [Recurso de pacote](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) de [!DNL Adobe InDesign] para exportar o documento. [!DNL Adobe InDesign] O pode exportar um documento e os ativos vinculados como um pacote. Nesse caso, a pasta exportada contém uma `Links` pasta que contém subativos na [!DNL InDesign] arquivo. A variável `Links` pasta está presente na mesma pasta que o arquivo INDD.
1. Crie um arquivo ZIP e faça upload dele para a [!DNL Experience Manager] repositório.
1. Inicie o `Unarchiver` fluxo de trabalho.
1. Quando o fluxo de trabalho é concluído, as referências na pasta Links são automaticamente referenciadas como subativos. Para exibir uma lista de ativos referenciados, navegue até a página de detalhes do ativo do [!DNL InDesign] ativo e feche o [Trilho](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: adicionar ativos digitais como referências {#refps}

1. Uso [!DNL Experience Manager] aplicativo de desktop para acessar [!DNL Experience Manager Assets]. Baixe e revele os ativos no sistema de arquivos local. Use o [!UICONTROL Local vinculado] funcionalidade no [!DNL Adobe Photoshop]. Consulte [colocar ativos no aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. Salvar em [!DNL Photoshop] para a unidade montada ou [upload](/help/assets/manage-assets.md#uploading-assets) para o [!DNL Experience Manager] repositório.
1. Após a conclusão do fluxo de trabalho, as referências a [!DNL Experience Manager] os ativos estão listados na página detalhes do ativo.

   Para exibir os ativos referenciados, feche o [Trilho](/help/sites-authoring/basic-handling.md#rail-selector) na página de detalhes do ativo.

1. Os ativos referenciados também contêm a lista de ativos dos quais eles são referenciados. Para exibir uma lista de ativos referenciados, navegue até a página de detalhes do ativo e feche a [Trilho](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>Os ativos nos ativos compostos também podem ser referenciados com base na ID do documento e na ID da instância. Essa funcionalidade está disponível com o [!DNL Adobe Illustrator] e [!DNL Adobe Photoshop] somente versões. Para outros, a referência é feita com base no caminho relativo de ativos vinculados no ativo composto principal, conforme feito em versões anteriores do [!DNL Experience Manager].

## Criar subativos {#generate-subassets}

Para os ativos compatíveis com formatos de várias páginas — arquivos PDF, arquivos AI, [!DNL Microsoft PowerPoint] e [!DNL Apple Keynote] arquivos e [!DNL Adobe InDesign] arquivos — [!DNL Experience Manager] O pode gerar subativos que correspondem a cada página individual do ativo original. Esses subativos estão vinculados à *pai* ativo e facilitar a visualização de várias páginas. Para todos os outros fins, os subativos são tratados como ativos normais no [!DNL Experience Manager].

A geração de subativos está desativada por padrão. Para habilitar a geração de subativos, siga estas etapas:

1. Efetue logon no [!DNL Experience Manager] como administrador. Access **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Selecionar **[!UICONTROL Ativo de atualização DAM]** e clique em **[!UICONTROL Editar]**.
1. Clique em **[!UICONTROL Ativar/desativar painel lateral]** e localize o **[!UICONTROL Criar sub-ativo]** etapa. Adicione a etapa ao fluxo de trabalho. Clique em **[!UICONTROL Sincronizar]**.

Para gerar os subativos, siga um destes procedimentos:

* Novos ativos: o [!UICONTROL Ativos de atualização DAM] o fluxo de trabalho é executado em qualquer novo ativo que é carregado para [!DNL Experience Manager]. Os subativos são gerados automaticamente para novos ativos de várias páginas.
* Ativos de várias páginas existentes: execute manualmente o [!UICONTROL Ativos de atualização DAM] fluxo de trabalho seguindo uma das etapas:

   * Selecione um ativo e clique em [!UICONTROL Linha do tempo] para abrir o painel esquerdo. Como alternativa, use o atalho de teclado `alt + 3`. Clique em [!UICONTROL Iniciar fluxo de trabalho], selecione [!UICONTROL Ativo de atualização DAM], clique em [!UICONTROL Início]e clique em [!UICONTROL Continuar].
   * Selecione um ativo e clique em [!UICONTROL Criar] > [!UICONTROL Fluxo de trabalho] na barra de ferramentas. Na caixa de diálogo pop-up, selecione [!UICONTROL Ativo de atualização DAM] workflow, clique em [!UICONTROL Início]e clique em [!UICONTROL Continuar].

Especificamente para documentos do Microsoft Word, execute o **[!UICONTROL Documentos Word da análise DAM]** fluxo de trabalho. Ele gera um `cq:Page` componente do conteúdo do documento do Microsoft Word. As imagens extraídas do documento são referenciadas a partir do `cq:Page` componente. Essas imagens são extraídas mesmo se a geração de sub-ativos estiver desativada.

>[!NOTE]
>
>No [!UICONTROL Processo de criação de sub-ativos - Propriedades da etapa] in [!UICONTROL Argumentos do processo], é possível especificar o número de subativos que [!DNL Experience Manager] gera. O valor padrão é 5. Para gerar todos os ativos secundários, deixe o campo vazio. Se o campo tiver negativo, nenhum ativo secundário será gerado.

## Exibir subativos {#viewing-subassets}

Os ativos secundários são exibidos somente se os ativos secundários forem gerados e estiverem disponíveis para o ativo de várias páginas selecionado. Para exibir os subativos gerados, abra o ativo de várias páginas. Na área superior esquerda da página, clique em ![Opção para abrir o painel esquerdo](assets/do-not-localize/aem_leftrail_contentonly.png) e clique em **[!UICONTROL Subativos]** da lista. Ao selecionar **[!UICONTROL Subativos]** da lista. Como alternativa, use o atalho de teclado `alt + 5`.

![Exibir subativos de um ativo de várias páginas](assets/view_subassets_simulation.gif)

## Visualizar páginas de um arquivo de várias páginas {#view-pages-of-a-multi-page-file}

Você pode visualizar um arquivo de várias páginas, como PDF, INDD, PPT, PPTX e arquivo AI, usando o recurso Visualizador de páginas de [!DNL Experience Manager Assets]. Abra um ativo de várias páginas e clique em **[!UICONTROL Visualizar páginas]** no canto superior esquerdo da página. O Visualizador de página aberto exibe as páginas do ativo e os controles para navegar e aplicar zoom em cada página.

![Visualizar e visualizar páginas de um ativo de várias páginas](assets/view_multipage_asset_fmr.gif)

Para [!DNL InDesign], você pode extrair páginas usando [!DNL InDesign Server]. Se as visualizações das páginas forem salvas durante [!DNL InDesign] criação de arquivo, depois [!DNL InDesign Server] não é necessário para a extração de páginas.

As seguintes opções estão disponíveis na barra de ferramentas, no painel à esquerda e nos controles do Visualizador de páginas:

* **[!UICONTROL Ações da área de trabalho]** para abrir ou revelar um subativo específico usando [!DNL Experience Manager] aplicativo de desktop. Veja como [configurar ações da área de trabalho](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) se você estiver usando [!DNL Experience Manager] aplicativo de desktop.

* **[!UICONTROL Propriedades]** abre a variável [!UICONTROL Propriedades] página do subativo específico.

* **[!UICONTROL Anotar]** permite anotar o subativo específico. As anotações usadas em subativos separados são coletadas e exibidas juntas quando o ativo principal é aberto para visualização.

* **[!UICONTROL Visão geral da página]** exibe todos os subativos simultaneamente.

* **[!UICONTROL Linha do tempo]** no painel esquerdo depois de clicar em ![Opção para abrir o painel esquerdo](assets/do-not-localize/aem_leftrail_contentonly.png) exibe o fluxo de atividade para o arquivo.

## Práticas recomendadas e limitação {#best-practice-limitation-tips}

* A geração de subativos pode consumir muitos recursos em qualquer [!DNL Experience Manager] implantação. Se você estiver gerando subativos quando ativos complexos forem carregados, adicione a etapa no fluxo de trabalho Atualizar ativo do DAM. Se você estiver gerando subativos sob demanda, crie um fluxo de trabalho separado para gerar subativos. Um fluxo de trabalho dedicado permite ignorar outras etapas no fluxo de trabalho Atualizar ativo do DAM e salvar recursos computacionais.

>[!MORELIKETHIS]
>
>* [Usar o aplicativo de desktop do Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Configurar ações da área de trabalho no Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Criar Objetos Inteligentes Vinculados no Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Inserir gráficos no Adobe InDesign](https://helpx.adobe.com/indesign/using/placing-graphics.html)
