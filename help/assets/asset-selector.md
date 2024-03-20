---
title: Seletor de ativos
description: Saiba como usar o seletor de ativos para pesquisar, filtrar, navegar e buscar metadados de ativos no Adobe Experience Manager Assets. Saiba também como personalizar a interface do seletor de ativos.
contentOwner: Adobe
feature: Asset Management,Metadata,Search
role: User
hide: true
exl-id: c84ce84a-1e52-48fd-a16c-38c7769df9af
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---

# Seletor de ativos {#asset-selector}

>[!NOTE]
>
>A variável [Seletor de ativos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-selector.html?lang=en) foi chamado [Seletor de ativos](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) em versões anteriores do [!DNL Experience Manager].

O seletor de ativos permite navegar, pesquisar e filtrar ativos no [!DNL Adobe Experience Manager] Assets. Também é possível buscar os metadados dos ativos selecionados usando o seletor de ativos. Para personalizar a interface do seletor de ativos, você pode iniciá-lo com parâmetros de solicitação compatíveis. Esses parâmetros definem o contexto do seletor de ativos para um cenário específico.

No momento, você pode passar os parâmetros da solicitação `assettype` (*Imagem/Vídeo/Texto*) e seleção `mode` (*Único/Múltiplo*) como informações contextuais para o seletor de ativos, que permanece intacto durante toda a seleção.

O seletor de ativos usa o HTML 5 **Window.postMessage** mensagem para enviar dados do ativo selecionado para o recipient.

O seletor de ativos é baseado no vocabulário do Granite. Por padrão, o seletor de ativos opera no modo de navegação. No entanto, você pode aplicar filtros usando a experiência do Omnisearch para refinar sua pesquisa por ativos específicos.

É possível integrar qualquer página da Web (independentemente de fazer parte do contêiner do CQ) ao seletor de ativos (`https://[AEM_server]:[port]/aem/assetpicker.html`).

## Parâmetros contextuais {#contextual-parameters}

Você pode passar os seguintes parâmetros de solicitação em um URL para iniciar o seletor de ativos em um contexto específico:

| Nome | Valores | Exemplo | Propósito |
|---|---|---|---|
| sufixo do recurso (B) | Caminho da pasta como o sufixo do recurso no URL:`http://localhost:4502/aem/`<br>`assetpicker.html/<folder_path>` | Para iniciar o seletor de ativos com uma pasta específica selecionada, por exemplo, com a pasta `/content/dam/we-retail/en/activities` selecionada, a URL deve estar no formato: `http://localhost:4502/aem/assetpicker.html`<br>`/content/dam/we-retail/en/activities?assettype=images` | Se você precisar que uma determinada pasta seja selecionada quando o seletor de ativos for iniciado, você a passou como um sufixo de recurso. |
| modo | único, múltiplo | `http://localhost:4502/aem/assetpicker.html`<br>`?mode=multiple` <br> `http://localhost:4502/aem/assetpicker.html`<br>`?mode=single` | No modo múltiplo, é possível selecionar vários ativos simultaneamente usando o seletor de ativos. |
| caixa de diálogo | verdadeiro, falso | `http://localhost:4502/aem/assetpicker.html`<br>`?dialog=true` | Use esses parâmetros para abrir o seletor de ativos como uma caixa de diálogo do Granite. Essa opção só é aplicável quando você inicia o seletor de ativos por meio do Campo de caminho do Granite e o configura como URL do pickerSrc. |
| raiz | `<folder_path>` | `http://localhost:4502/aem/`<br>`assetpicker.html?assettype=images`<br>`&root=/content/dam/we-retail/en/activities` | Use essa opção para especificar a pasta raiz do seletor de ativos. Nesse caso, o seletor de ativos permite selecionar somente ativos secundários (diretos/indiretos) na pasta raiz. |
| viewmode | pesquisa |  | Para iniciar o seletor de ativos no modo de pesquisa, com parâmetros assettype e mimetype. |
| tipo de ativo (S) | imagens, documentos, multimídia, arquivos | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives`</li> | Use essa opção para filtrar tipos de ativos com base no valor transmitido. |
| mimetype | tipo(s) mime (`/jcr:content/metadata/dc:format`) de um ativo (curinga também é compatível) | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=image/png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&?mimetype=*png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=*presentation`</li>  <li>`http://localhost:4502/aem/assetpicker?viewmode=search&mimetype=*presentation&mimetype=*png`</li></ul> | Use-a para filtrar ativos com base nos tipos MIME |

## Usar o seletor de ativos {#using-the-asset-selector}

1. Para acessar a interface do seletor de ativos, acesse `https://[AEM_server]:[port]/aem/assetpicker`.
1. Navegue até a pasta desejada e selecione um ou mais ativos.

   ![chlimage_1-441](assets/chlimage_1-441.png)

   Como alternativa, você pode pesquisar pelo ativo desejado na caixa OmniSearch e depois selecioná-lo.

   ![chlimage_1-442](assets/chlimage_1-442.png)

   Se pesquisar ativos usando a caixa OmniSearch, você poderá selecionar vários filtros na caixa **[!UICONTROL Filtros]** para refinar sua pesquisa.

   ![chlimage_1-443](assets/chlimage_1-443.png)

1. Clique em **[!UICONTROL Selecionar]** na barra de ferramentas.

>[!MORELIKETHIS]
>
>* [Seletor de ativos de microfront-end no AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-selector.html?lang=en)
