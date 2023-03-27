---
title: Seletor de ativos
description: Saiba como usar o seletor de ativos para pesquisar, filtrar, navegar e buscar metadados para ativos no Adobe Experience Manager Assets. Saiba também como personalizar a interface do seletor de ativos.
contentOwner: Adobe
feature: Asset Management,Metadata,Search
role: User
exl-id: 4b518ac0-5b8b-4d61-ac31-269aa1f5abe4
source-git-commit: 0c6c269e9f0cbdcc0c5e3b925ef09b9923cbb2b3
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---

# Seletor de ativos {#asset-selector}

>[!NOTE]
>
>O seletor de Ativos foi chamado [Seletor de ativos](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) em versões anteriores do [!DNL Experience Manager].

O seletor de ativos permite navegar, pesquisar e filtrar ativos no [!DNL Adobe Experience Manager] Ativos. Também é possível buscar os metadados dos ativos selecionados usando o seletor de ativos. Para personalizar a interface do seletor de ativos, você pode iniciá-lo com parâmetros de solicitação compatíveis. Esses parâmetros definem o contexto do seletor de ativos para um cenário específico.

Atualmente, você pode transmitir os parâmetros da solicitação `assettype` (*Imagem/Vídeo/Texto*) e seleção `mode` (*Único/Múltiplo*) como informações contextuais para o seletor de ativos, que permanece intacto durante toda a seleção.

O seletor de ativos usa a HTML5 **Window.postMessage** mensagem para enviar dados do ativo selecionado para o recipient.

O seletor de ativos é baseado no vocabulário do seletor de fundações do Granite. Por padrão, o seletor de ativos opera no modo de navegação. No entanto, você pode aplicar filtros usando a experiência do Omnisearch para refinar sua pesquisa de ativos específicos.

É possível integrar qualquer página da Web (independentemente de fazer parte do contêiner CQ) ao seletor de ativos (`https://[AEM_server]:[port]/aem/assetpicker.html`).

## Parâmetros contextuais {#contextual-parameters}

Você pode transmitir os seguintes parâmetros de solicitação em um URL para iniciar o seletor de ativos em um contexto específico:

| Nome | Valores | Exemplo | Propósito |
|---|---|---|---|
| sufixo do recurso (B) | Caminho da pasta como o sufixo de recurso no URL:`http://localhost:4502/aem/`<br>`assetpicker.html/<folder_path>` | Para iniciar o seletor de ativos com uma pasta específica selecionada, por exemplo, com a pasta `/content/dam/we-retail/en/activities` selecionado, o URL deve estar no formato: `http://localhost:4502/aem/assetpicker.html`<br>`/content/dam/we-retail/en/activities?assettype=images` | Se você precisar selecionar uma pasta específica quando o seletor de ativos for iniciado, passe-a como um sufixo de recurso. |
| modo | único, múltiplo | `http://localhost:4502/aem/assetpicker.html`<br>`?mode=multiple` <br> `http://localhost:4502/aem/assetpicker.html`<br>`?mode=single` | No modo múltiplo, é possível selecionar vários ativos simultaneamente usando o seletor de ativos. |
| caixa de diálogo | true, false | `http://localhost:4502/aem/assetpicker.html`<br>`?dialog=true` | Use esses parâmetros para abrir o seletor de ativos como Caixa de diálogo do Granite. Essa opção só é aplicável quando você inicia o seletor de ativos por meio do Campo de caminho do Granite e o configura como URL pickerSrc. |
| root | `<folder_path>` | `http://localhost:4502/aem/`<br>`assetpicker.html?assettype=images`<br>`&root=/content/dam/we-retail/en/activities` | Use essa opção para especificar a pasta raiz do seletor de ativos. Nesse caso, o seletor de ativos permite selecionar apenas ativos secundários (diretos/indiretos) na pasta raiz. |
| modo de visualização | pesquisar |  | Para iniciar o seletor de ativos no modo de pesquisa, com parâmetros tipo de ativo e tipo de ativo. |
| tipo de ativo (S) | imagens, documentos, multimídia, arquivos | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives`</li> | Use essa opção para filtrar tipos de ativos com base no valor transmitido. |
| mimetype | mimetype(s) (`/jcr:content/metadata/dc:format`) de um ativo (curinga também compatível) | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=image/png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&?mimetype=*png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=*presentation`</li>  <li>`http://localhost:4502/aem/assetpicker?viewmode=search&mimetype=*presentation&mimetype=*png`</li></ul> | Use-o para filtrar ativos com base em tipos MIME |

## Usar o seletor de ativos {#using-the-asset-selector}

1. Para acessar a interface do seletor de ativos, acesse `https://[AEM_server]:[port]/aem/assetpicker`.
1. Navegue até a pasta desejada e selecione um ou mais ativos.

   ![chlimage_1-441](assets/chlimage_1-441.png)

   Como alternativa, você pode pesquisar o ativo desejado na caixa OmniSearch e depois selecioná-lo.

   ![chlimage_1-442](assets/chlimage_1-442.png)

   Se você pesquisar ativos usando a caixa OmniSearch , poderá selecionar vários filtros da variável **[!UICONTROL Filtros]** para refinar sua pesquisa.

   ![chlimage_1-443](assets/chlimage_1-443.png)

1. Toque/clique **[!UICONTROL Selecionar]** na barra de ferramentas.
