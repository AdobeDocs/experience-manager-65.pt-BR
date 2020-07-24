---
title: Pesquise ativos digitais e imagens [!DNL Adobe Experience Manager].
description: Saiba como localizar os ativos necessários [!DNL Adobe Experience Manager] usando o painel Filtros e como usar os ativos exibidos na pesquisa.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 76f2df9b1d3e6c2ca7a12cc998d64423d49ebc5b
workflow-type: tm+mt
source-wordcount: '5830'
ht-degree: 5%

---


# Pesquisar ativos em [!DNL Adobe Experience Manager] {#search-assets-in-aem}

[!DNL Adobe Experience Manager Assets] fornece métodos robustos de descoberta de ativos que ajudam você a atingir uma velocidade de conteúdo mais alta. Suas equipes reduzem o tempo de comercialização com uma experiência de pesquisa inteligente e perfeita, usando recursos prontos para uso e métodos personalizados. Pesquisar ativos é fundamental para o uso de um sistema de gerenciamento de ativos digitais — seja para uso adicional por parte de profissionais de criação, para o gerenciamento robusto de ativos por parte de usuários e comerciantes, ou para administração por administradores de DAM. Pesquisas simples, avançadas e personalizadas que podem ser realizadas pela interface do [!DNL Assets] usuário ou outros aplicativos e superfícies ajudam a atender a esses casos de uso.

[!DNL Experience Manager Assets] suporta os seguintes casos de uso e este artigo descreve o uso, os conceitos, as configurações, as limitações e a solução de problemas para esses casos de uso.

| Pesquisar ativos | Configuração e administração | Trabalhar com resultados de pesquisa |
|---|---|---|
| [Pesquisas básicas](#searchbasics) | [Índice de pesquisa](#searchindex) | [Classificar resultados](#sort) |
| [Compreender a interface de usuário de pesquisa](#searchui) | [Pesquisa visual ou de semelhança](#configvisualsearch) | [Verificar propriedades e metadados de um ativo](#checkinfo) |
| [Sugestões de pesquisa](#searchsuggestions) | [Metadados obrigatórios](#mandatorymetadata) | [Download](#download) |
| [Compreender os resultados e o comportamento da pesquisa](#searchbehavior) | [Modificar aspectos de pesquisa](#searchfacets) | [Atualizações de metadados em massa](#metadataupdates) |
| [Classificação de pesquisa e aumento](#searchrank) | [extração de texto](#extracttextupload) | [Coleções inteligentes](#collections) |
| [Pesquisa avançada: filtragem e escopo da pesquisa](#scope) | [Previsões personalizadas](#custompredicates) | [Entenda os resultados inesperados e solucione problemas](#troubleshoot-unexpected-search-results-and-issues) |
| [Pesquise de outras soluções e aplicativos](#beyondomnisearch):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brandportal)</li><li>[aplicativo de desktop Experience Manager](#desktopapp)</li><li>[Imagens do Adobe Stock](#adobestock)</li><li>[Ativos Dynamic Media](#dynamicmedia)</li></ul> |  |  |
| [Seletor de ativos](#assetselector) |  |  |
| [Limitações](#limitations) e [dicas](#tips) |  |  |
| [Exemplos ilustrados](#samples) |  |  |

Procure ativos usando o campo Omnisearch na parte superior da interface da [!DNL Experience Manager] Web. Vá para **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]** em [!DNL Experience Manager], clique em pesquisar na barra superior, digite a palavra-chave de pesquisa e pressione return. Como alternativa, use o atalho de palavra-chave / (barra) para abrir o campo Omnisearch. `Location:Assets` é pré-selecionada para limitar as pesquisas aos ativos DAM. [!DNL Experience Manager] fornece sugestões enquanto seu start digita uma palavra-chave de pesquisa.

Use o painel **[!UICONTROL Filtros]** para restringir sua pesquisa filtrando os resultados da pesquisa com base nas várias opções (predicados), como tipo de arquivo, tamanho do arquivo, data da última modificação, status do ativo, dados de insights e licenciamento do Adobe Stock. Seus administradores podem personalizar o painel Filtros e adicionar ou remover predicados de pesquisa usando aspectos de pesquisa. O filtro Tipo [!UICONTROL de] arquivo no painel [!UICONTROL Filtros] tem caixas de seleção de estado misto. Portanto, a menos que você selecione todos os predicados aninhados (ou formatos), as caixas de seleção de primeiro nível estarão parcialmente marcadas.

[!DNL Experience Manager] o recurso de pesquisa suporta a pesquisa por coleções e a pesquisa por ativos dentro de uma coleção. Consulte Coleções [de pesquisa](/help/assets/managing-collections-touch-ui.md).

## Compreender a interface de pesquisa {#searchui}

Familiarize-se com a interface de pesquisa e as ações disponíveis.

![Compreender a interface de resultados de pesquisa do Experience Manager Assets](assets/aem_search_results.png)

*Figura: Entenda a interface dos resultados da[!DNL Experience Manager Assets]pesquisa.*

**A.** Salve a pesquisa como uma coleção inteligente. **B.** Filtros ou previsões para restringir os resultados da pesquisa. **C.** Exibir arquivos, pastas ou ambos. **D.** Clique em Filtros para abrir ou fechar o painel à esquerda. **E.** O local de pesquisa é DAM. **F.** Campo Omnisearch com palavra-chave de pesquisa fornecida pelo usuário. **G.** Selecione os resultados de pesquisa carregados. **H.** Número de resultados de pesquisa exibidos fora do total de resultados de pesquisa. **Eu.** Feche a pesquisa **J.** Alterne entre a visualização da placa e a visualização da lista.

### Aspectos de pesquisa dinâmica {#dynamicfacets}

Você pode descobrir os ativos desejados mais rapidamente a partir da página de resultados da pesquisa usando o número atualizado dinamicamente dos resultados de pesquisa esperados nas facetas de pesquisa. O número esperado de ativos é atualizado mesmo antes de aplicar o filtro de pesquisa. Ver a contagem esperada em relação ao filtro ajuda a navegar pelos resultados da pesquisa de forma rápida e eficiente. Para obter mais informações, consulte [Pesquisar ativos no Experience Manager](search-assets.md).

![Consulte o número aproximado de ativos sem filtrar os resultados da pesquisa em aspectos de pesquisa.](assets/asset_search_results_in_facets_filters.png)

*Figura: Consulte o número aproximado de ativos sem filtrar os resultados da pesquisa em aspectos de pesquisa.*

## Compreender os resultados e o comportamento da pesquisa {#searchbehavior}

### Termos e resultados básicos da pesquisa {#searchbasics}

Você pode executar pesquisas de palavras-chave a partir do campo OmniSearch. A pesquisa de palavra-chave não diferencia maiúsculas de minúsculas e é uma pesquisa de texto completo (nos campos de metadados populares). Se mais de uma palavra-chave for pesquisada, o operador padrão entre as palavras-chave será `AND` para pesquisa padrão e será `OR` quando os ativos tiverem tags inteligentes.

Os resultados são classificados por relevância, começando com correspondências mais próximas. Para várias palavras-chave, os resultados mais relevantes são os ativos que contêm ambos os termos em seus metadados. Nos metadados, as palavras-chave que aparecem como tags inteligentes são classificadas mais alto do que as palavras-chave que aparecem em outros campos de metadados. [!DNL Experience Manager] permite fornecer um termo de pesquisa específico com maior peso. Além disso, é possível [aumentar a classificação](#searchrank) de alguns ativos direcionados para termos de pesquisa específicos.

Para encontrar rapidamente os ativos relevantes, a interface avançada fornece mecanismos de filtragem, classificação e seleção. Você pode filtrar os resultados com base em vários critérios e ver o número de ativos pesquisados para vários filtros. Como alternativa, você pode executar novamente a pesquisa alterando o query no campo Omnisearch. Quando você altera seus termos ou filtros de pesquisa, os outros filtros permanecem aplicados para preservar o contexto da pesquisa.

Quando os resultados forem muitos ativos, [!DNL Experience Manager] exibirá os primeiros 100 na visualização do cartão e 200 na visualização da lista. À medida que os usuários rolam, mais ativos são carregados. Isso é para melhorar o desempenho.

>[!VIDEO](https://www.youtube.com/watch?v=LcrGPDLDf4o)

Às vezes, você pode ver alguns ativos inesperados nos resultados da pesquisa. Para obter mais informações, consulte resultados [](#troubleshoot-unexpected-search-results-and-issues)inesperados.

[!DNL Experience Manager] pode pesquisar vários formatos de arquivo e os filtros de pesquisa podem ser personalizados para atender às suas necessidades comerciais. Entre em contato com o administrador para saber quais opções de pesquisa estão disponíveis para o repositório DAM e quais restrições sua conta tem.

### Resultados com e sem tags inteligentes aprimoradas {#withsmarttags}

Por padrão, [!DNL Experience Manager] a pesquisa combina os termos de pesquisa com uma cláusula AND. Por exemplo, considere pesquisar por palavras-chave mulheres em execução. Por padrão, somente os ativos com as palavras-chave de mulher e de execução nos metadados são exibidos nos resultados da pesquisa. O mesmo comportamento é mantido quando caracteres especiais (pontos, sublinhados ou traços) são usados com as palavras-chave. Os seguintes query de pesquisa retornam os mesmos resultados:

* `woman running`
* `woman.running`
* `woman-running`

No entanto, o query `woman -running` retorna ativos sem `running` seus metadados.
O uso de tags inteligentes adiciona uma `OR` cláusula extra para localizar qualquer um dos termos de pesquisa como as tags inteligentes aplicadas. Um ativo marcado com tags inteligentes `woman` ou `running` usando tags inteligentes também é exibido nesse query de pesquisa. Então os resultados da pesquisa são uma combinação de...

* Ativos com `woman` e `running` palavras-chave nos metadados (comportamento padrão).

* Ativos marcados com inteligência com qualquer uma das palavras-chave (comportamento de tags inteligentes).

### Search suggestions as you type {#searchsuggestions}

Ao digitar palavras-chave com start, [!DNL Experience Manager] sugere as possíveis palavras-chave ou frases de pesquisa. As sugestões são baseadas nos metadados dos ativos existentes. [!DNL Experience Manager] indexa todos os campos de metadados para ajudar na pesquisa. Para fornecer sugestões de pesquisa, o sistema usa os valores dos seguintes poucos campos de metadados. Para fornecer sugestões de pesquisa, considere preencher os seguintes campos com as palavras-chave apropriadas:

* Tags de ativos. (mapeia para `jcr:content/metadata/cq:tags`)
* Título do ativo. (mapeia para `jcr:content/metadata/dc:title`)
* Descrição do ativo. (mapeia para `jcr:content/metadata/dc:description`)
* Título no repositório JCR. O valor pode ser mapeado para o título do ativo. (mapeia para `jcr:content/jcr:title`)
* Descrição no repositório JCR. O valor pode ser mapeado para a descrição do ativo. (mapeia para `jcr:content/jcr:description`)

Para receber sugestões para mais de uma palavra-chave de pesquisa, continue digitando todas as palavras-chave sem selecionar qualquer sugestão para uma única palavra-chave.

![Digite várias palavras-chave em sugestões visualizações que se ajustem a todas](assets/search_suggestionsmanykeywords.gif)

*Figura: Digite várias palavras-chave para sugestões visualizações que se ajustem a todas elas.*

### Classificação de pesquisa e aumento {#searchrank}

Os resultados da pesquisa que correspondem a todos os termos de pesquisa nos campos de metadados são exibidos primeiro, seguidos dos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. No exemplo acima, a ordem aproximada de exibição dos resultados da pesquisa é:

1. Corresponde `woman running` aos vários campos de metadados.
1. Corresponde a `woman running` tags inteligentes.
1. Corresponde a `woman` ou de `running` em tags inteligentes.

Você pode melhorar a relevância das palavras-chave de ativos específicos para ajudar a aumentar as pesquisas com base nas palavras-chave. Em outras palavras, as imagens para as quais você promove palavras-chave específicas aparecem na parte superior dos resultados da pesquisa quando você pesquisa com base nessas palavras-chave.

1. From the [!DNL Assets] user interface, open the properties page for the asset. Click **[!UICONTROL Advanced]** and click **[!UICONTROL Add]** under **[!UICONTROL Elevate for search keywords]**.
1. Na caixa **[!UICONTROL Pesquisar promoção]** , especifique uma palavra-chave para a qual deseja aumentar a pesquisa da imagem e clique em **[!UICONTROL Adicionar]**. É possível especificar várias palavras-chave da mesma maneira.
1. Clique em **[!UICONTROL Salvar e fechar]**. O ativo que você promoveu para essa palavra-chave aparece entre os principais resultados da pesquisa.

Você pode usar isso em sua vantagem ao aumentar a classificação de alguns ativos nos resultados da pesquisa para a palavra-chave direcionada. Veja o exemplo de vídeo abaixo. Para obter informações detalhadas, consulte [pesquisa no Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/search-and-discovery/search.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*Entenda como os resultados da pesquisa são classificados e como a classificação pode ser influenciada.*

## Advanced search {#scope}

[!DNL Experience Manager] fornece vários métodos, como filtros, que se aplicam aos ativos pesquisados, para ajudá-lo a localizar os ativos desejados mais rapidamente. Alguns métodos comumente usados estão descritos abaixo. Alguns exemplos [](#samples) ilustrados são compartilhados abaixo.

**Procurar ficheiros ou pastas**: Nos resultados da pesquisa, consulte arquivos, pastas ou ambos. No painel **[!UICONTROL Filtros]** , é possível selecionar a opção apropriada. Consulte interface [de](#searchui)pesquisa.

**Pesquisar ativos em uma pasta**: Você pode limitar a pesquisa a uma pasta específica. No painel **[!UICONTROL Filtros]** , adicione o caminho de uma pasta. Você pode selecionar apenas uma pasta por vez.

![Limitar os resultados da pesquisa a uma pasta adicionando um caminho de pasta no painel Filtros](assets/search_folder_select.gif)

*Figura: Limite os resultados da pesquisa a uma pasta adicionando um caminho de pasta no painel Filtros.*

### Localizar imagens semelhantes {#visualsearch}

Para localizar imagens visualmente semelhantes a uma imagem selecionada pelo usuário, clique na opção **[!UICONTROL Localizar semelhante]** na exibição de cartão de uma imagem ou na barra de ferramentas. [!DNL Experience Manager]O exibe as imagens com tags inteligentes do repositório DAM que são semelhantes a uma imagem selecionada pelo usuário. Consulte [como configurar a pesquisa de semelhança](#configvisualsearch).

![Encontre imagens semelhantes usando a opção na visualização do cartão](assets/search_find_similar.png)

*Figura: Encontre imagens semelhantes usando a opção na visualização do cartão.*

### Imagens do Adobe Stock {#adobestock}

Na interface do [!DNL Experience Manager] usuário, os usuários podem pesquisar ativos [do](/help/assets/aem-assets-adobe-stock.md) Adobe Stock e licenciar os ativos necessários. Adicione `Location: Adobe Stock` na barra Omnisearch. Você também pode usar o painel Filtros para localizar todos os ativos licenciados ou não licenciados ou pesquisar um ativo específico usando o número de arquivo do Adobe Stock.

### Ativos Dynamic Media {#dmassets}

Você pode filtrar por imagens do Dynamic Media selecionando **[!UICONTROL Dynamic Media]** > **[!UICONTROL Conjuntos]** no painel **[!UICONTROL Filtros]**. Isso filtra e exibe ativos como conjuntos de imagens, carrosséis, conjuntos de mídia mista e conjuntos de rotação.

### Pesquisar usando valores específicos em campos de metadados {#gqlsearch}

Você pode pesquisar ativos com base nos valores exatos de campos de metadados específicos, como título, descrição e autor. O recurso de pesquisa de texto completo do GQL busca apenas os ativos cujo valor de metadados corresponda exatamente ao seu query de pesquisa. Os nomes das propriedades (por exemplo, autor, título e assim por diante) e os valores distinguem maiúsculas de minúsculas.

| Campo de metadados | Valor e uso da faceta |
| ----------------------------------------- | ------------------------------------- |
| Título | título:John |
| Criador | criador:John |
| Local | local:NA |
| Descrição | descrição:&quot;Imagem de amostra&quot; |
| Ferramenta Criador | criatortool:&quot;Adobe Photoshop CC 2020&quot; |
| Proprietário de direitos autorais | copyrights towner:&quot;Adobe Systems&quot; |
| Contribuinte | colaborador:John |
| Termos de Uso  | usageterms:&quot;CopyRights Reserved&quot; |
| Criado | criado:AAAA-MM-DDTHH |
| Data de expiração | expira:AAAA-MM-DDTHH |
| Hora | hora única:AAAA-MM-DTHH |
| Hora de desligar | offtime:YYYY-MM-DTHH |
| Intervalo de tempo(expira em dateontime,offtime) | campo de faceta: limite inferior...upperbound |
| Caminho | /content/dam/&lt;nome da pasta> |
| Título do PDF | pdftitle: &quot;Documento da Adobe&quot; |
| Assunto | assunto: &quot;Formação&quot; |
| Tags | tags:&quot;Localização E Viagem&quot; |
| Tipo | type:&quot;image\png&quot; |
| Largura da imagem | largura:limite inferior..upperbound |
| Altura da imagem | height:limite inferior..upperbound |
| Person | pessoa:John |

As propriedades `path`, `limit`, `size`e `orderby` não podem ser *OUed* com qualquer outra propriedade.

A palavra-chave para uma propriedade gerada pelo usuário é seu rótulo de campo no editor de propriedades em minúsculas, com espaços removidos.

Estes são alguns exemplos de formatos de pesquisa para query complexos:

* Para exibir todos os ativos com vários campos de facetas (por exemplo: title=John Doe e ferramenta criadora = Adobe Photoshop): `tiltle:"John Doe" creatortool:Adobe*`
* Para exibir todos os ativos quando o valor de facetas não for uma única palavra, mas uma sentença (por exemplo: title=Scott Reynolds): `title:"Scott Reynolds"`
* Para exibir ativos com vários valores de uma única propriedade (por exemplo: title=Scott Reynolds ou John Doe): `title:"Scott Reynolds" OR "John Doe"`
* Para exibir ativos com valores de propriedade começando com uma string específica (por exemplo: o título é Scott Reynolds): `title:Scott*`
* Para exibir ativos com valores de propriedade que terminam com uma string específica (por exemplo: o título é Scott Reynolds): `title:*Reynolds`
* Para exibir ativos com um valor de propriedade que contenha uma string específica (por exemplo: título = Sala de reuniões de Basileia): `title:*Meeting*`
* Para exibir ativos que contêm uma determinada string e têm um valor de propriedade específico (por exemplo: procure a string Adobe em ativos com título=João da Silva): `*Adobe* title:"John Doe"`

## Pesquisar ativos de outras [!DNL Experience Manager] ofertas ou interfaces {#beyondomnisearch}

[!DNL Adobe Experience Manager] conecta o repositório DAM a várias outras [!DNL Experience Manager] soluções para fornecer acesso mais rápido aos ativos digitais e dinamizar os workflows criativos. Qualquer start de descoberta de ativos com navegação ou pesquisa. O comportamento de pesquisa permanece basicamente o mesmo em várias superfícies e soluções. Alguns métodos de pesquisa mudam conforme a audiência do público alvo, os casos de uso e a interface do usuário variam nas [!DNL Experience Manager] soluções. Os métodos específicos estão documentados para as soluções individuais nos links abaixo. As dicas e comportamentos universalmente aplicáveis estão documentados neste artigo.

### Pesquisar ativos no painel Adobe Asset Link {#aal}

Usando o Adobe Asset Link, os profissionais criativos agora podem acessar o conteúdo armazenado em [!DNL Experience Manager Assets], sem sair dos aplicativos compatíveis da Adobe Creative Cloud. Creatives can seamlessly browse, search, check out, and check in assets using the in-app panel in the [!DNL Adobe Creative Cloud apps]: [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], and [!DNL Adobe InDesign]. O Link de ativo também permite que os usuários pesquisem resultados visualmente semelhantes. Os resultados da exibição da pesquisa visual são capacitados pelos algoritmos de aprendizado de máquina do Adobe Sensei e ajudam os usuários a encontrar imagens esteticamente semelhantes. Consulte [pesquisar e procurar ativos](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) usando o Adobe Asset Link.

### Pesquisar ativos no aplicativo [!DNL Experience Manager] de desktop {#desktopapp}

Profissionais criativos usam o aplicativo de desktop para tornar o desktop [!DNL Experience Manager Assets] facilmente pesquisável e disponível em seu desktop local (Win ou Mac). Os profissionais de criação podem revelar facilmente os ativos desejados no Mac Finder ou no Windows Explorer, abertos em aplicativos de desktop e alterados localmente - as alterações são salvas de volta [!DNL Experience Manager] com uma nova versão criada no repositório. O aplicativo oferece suporte a pesquisas básicas usando uma ou mais palavras-chave, `*` curingas e `?` `AND` operadores. Consulte [Pesquisar, pesquisar e pré-visualização ativos](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) no aplicativo de desktop.

### Pesquisar ativos em [!DNL Brand Portal] {#brandportal}

Usuários e comerciantes de linha de negócios usam o Brand Portal para compartilhar de forma eficiente e segura os ativos digitais aprovados com suas equipes internas, parceiros e revendedores estendidos. See [search assets on Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### Pesquisar [!DNL Adobe Stock] imagens {#adobestock-1}

Na interface do [!DNL Experience Manager] usuário, os usuários podem pesquisar ativos do Adobe Stock e licenciar os ativos necessários. Adicione `Location: Adobe Stock` no campo Omnisearch. Você também pode usar o painel **[!UICONTROL Filtros]** para localizar todos os ativos licenciados ou não licenciados ou pesquisar um ativo específico usando o número de arquivo do Adobe Stock. Consulte [Gerenciar imagens do Adobe Stock no Experience Manager](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Pesquisar ativos da Dynamic Media {#dynamicmedia}

Você pode filtrar por imagens do Dynamic Media selecionando **[!UICONTROL Dynamic Media]** > **[!UICONTROL Conjuntos]** no painel **[!UICONTROL Filtros]**. Isso filtra e exibe ativos como conjuntos de imagens, carrosséis, conjuntos de mídia mista e conjuntos de rotação. Ao criar páginas da Web, os autores podem pesquisar por conjuntos no Localizador de conteúdo. Há um filtro para conjuntos disponível em um menu pop-up.

### Pesquisar ativos no Localizador de conteúdo ao criar páginas da Web {#contentfinder}

Os autores podem usar o Localizador de conteúdo para pesquisar no repositório do DAM os ativos relevantes e usar os ativos nas páginas da Web que eles criam. Os autores também podem usar a funcionalidade Ativos conectados para pesquisar ativos que estão disponíveis em uma [!DNL Experience Manager] implantação remota. Os autores podem usar esses ativos em páginas da Web em uma [!DNL Experience Manager] implantação local. See [use remote assets](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### Pesquisar coleções {#collections}

[!DNL Experience Manager] o recurso de pesquisa suporta a pesquisa por coleções e a pesquisa por ativos dentro de uma coleção. Consulte Coleções [de pesquisa](/help/assets/managing-collections-touch-ui.md).

## Seletor de ativos {#assetselector}

O Seletor de ativos permite que você pesquise, filtre e navegue pelos ativos DAM de uma maneira especial. O Seletor de ativos está disponível em `https://[aem-server]:[port]/aem/assetpicker.html`. Você pode buscar os metadados dos ativos selecionados usando essa funcionalidade. Você pode iniciá-lo com parâmetros de solicitação suportados, como tipo de ativo (imagem, vídeo, texto) e modo de seleção (seleções únicas ou múltiplas). Esses parâmetros definem o contexto do Seletor de ativos para uma instância de pesquisa específica e permanecem intactos durante toda a seleção.

O Seletor de ativos usa a mensagem HTML5 `Window.postMessage` para enviar dados do ativo selecionado para o recipient. O Seletor de ativos funciona somente no modo de navegação e funciona somente com a página de resultados do Omnisearch.

Você pode passar os seguintes parâmetros de solicitação em um URL para iniciar o Seletor de ativos em um contexto específico:

| Nome | Valores | Exemplo | Propósito |
|---|---|---|---|
| sufixo do recurso (B) | Caminho da pasta como o sufixo do recurso no URL:[https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | Para iniciar o Seletor de ativos com uma pasta específica selecionada, por exemplo, com a pasta `/content/dam/we-retail/en/activities` selecionada, o URL deve ter o formato: [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | Se você precisar que uma pasta específica seja selecionada quando o seletor de ativos for iniciado, passe-o como um sufixo de recurso. |
| modo | único, múltiplo | <ul><li>[https://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=single)</li><li>[https://localhost:4502/aem/assetpicker.html?mode=multiple](https://localhost:4502/aem/assetpicker.html?mode=multiple)</li></ul> | No modo múltiplo, você pode selecionar vários ativos simultaneamente usando o seletor de ativos. |
| mimetype | mimetype(s) (`/jcr:content/metadata/dc:format`) de um ativo (curinga também compatível) | <ul><li>[https://localhost:4502/aem/assetpicker.html?mimetype=image/png](https://localhost:4502/aem/assetpicker.html?mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png)</li></ul> | Use-o para filtrar ativos com base em tipos MIME |
| caixa de diálogo | verdadeiro, falso | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | Use esses parâmetros para abrir o seletor de ativos como Caixa de diálogo Granite. Essa opção só é aplicável quando você inicia o seletor de ativos por meio do campo Caminho de Granite e o configura como URL pickerSrc. |
| tipo de ativo (S) | imagens, documentos, multimídia, arquivos | <ul><li>[https://localhost:4502/aem/assetpicker.html?assettype=images](https://localhost:4502/aem/assetpicker.html?assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=multimedia](https://localhost:4502/aem/assetpicker.html?assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=archives](https://localhost:4502/aem/assetpicker.html?assettype=archives)</li></ul> | Use essa opção para filtrar os tipos de ativos com base no valor passado. |
| root | &lt;caminho_da_pasta> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities) | Use essa opção para especificar a pasta raiz do seletor de ativos. Nesse caso, o seletor de ativos permite que você selecione apenas ativos secundários (diretos/indiretos) na pasta raiz. |

Para acessar a interface do Seletor de ativos, acesse `https://[aem_server]:[port]/aem/assetpicker`. Navegue até a pasta desejada e selecione um ou mais ativos. Como alternativa, procure o ativo desejado na caixa Omnisearch, aplique o filtro conforme necessário e selecione-o.

![Procurar e selecionar ativo no seletor de ativos](assets/assetpicker.png)

*Figura: Procure e selecione o ativo no seletor de ativos.*

## Limitações           {#limitations}

O recurso de pesquisa no tem [!DNL Experience Manager Assets] as seguintes limitações:

* Não insira um espaço à esquerda no query de pesquisa; caso contrário, a pesquisa não funcionará.
* [!DNL Experience Manager] pode continuar a mostrar o termo de pesquisa depois de selecionar as propriedades de um ativo dos resultados pesquisados e cancelar a pesquisa. <!-- (CQ-4273540) -->
* Ao procurar pastas ou arquivos e pastas, os resultados da pesquisa não podem ser classificados em nenhum parâmetro.
* Se você pressionar return sem digitar nada na barra Omnisearch, [!DNL Experience Manager] retornará uma lista de apenas arquivos e não pastas. Se você pesquisar especificamente por pastas sem usar uma palavra-chave, [!DNL Experience Manager] não retornará nenhum resultado.
* Use a opção **[!UICONTROL Selecionar tudo]** no canto superior direito da página de pesquisa para selecionar os ativos pesquisados. [!DNL Experience Manager] exibe inicialmente 100 ativos na visualização do cartão e 200 ativos na visualização da lista. Mais ativos são carregados à medida que você percorre os resultados da pesquisa. Você pode selecionar mais ativos do que os ativos carregados. A contagem dos ativos selecionados é exibida no canto superior direito da página de resultados da pesquisa. Você pode operar na seleção, por exemplo, baixar os ativos selecionados, atualizar as propriedades de metadados em massa para os ativos selecionados ou adicionar os ativos selecionados a uma Coleção. Quando mais ativos são selecionados do que exibidos, uma ação é aplicada em todos os ativos selecionados ou uma caixa de diálogo exibe o número de ativos nos quais ela é aplicada. Para aplicar uma ação aos ativos que não foram carregados, verifique se todos os ativos estão selecionados explicitamente.

Pesquisa visual ou pesquisa de semelhança tem as seguintes limitações:

* A pesquisa visual funciona melhor com repositórios maiores. Embora não haja um número mínimo de imagens necessário para bons resultados, a qualidade das correspondências com algumas imagens pode não ser tão boa quanto as correspondências de um repositório grande.
* Não é possível alterar o modelo ou o trem [!DNL Experience Manager] para encontrar imagens semelhantes. Por exemplo, adicionar ou remover tags inteligentes a alguns ativos não altera o modelo. Os ativos são excluídos dos resultados de pesquisa visualmente semelhantes.

A funcionalidade de pesquisa pode ter limitações de desempenho nos seguintes cenários:

* A visualização de cartão tem um tempo de carregamento mais rápido do que a visualização de lista para exibir os resultados da pesquisa.

## Dicas de pesquisa {#tips}

* Ao monitorar o status da revisão de ativos, use a opção apropriada para descobrir quais ativos estão aprovados ou quais ativos estão pendentes de aprovação.
* Use o predicado Insights para pesquisar ativos suportados com base em suas estatísticas de uso obtidas de vários aplicativos Creative. Os dados de uso são agrupados em Pontuação de uso, Impressões, Cliques e canais de mídia nos quais os ativos aparecem categorias.
* Use a caixa de seleção **[!UICONTROL Selecionar tudo]** para selecionar os ativos pesquisados. [!DNL Experience Manager] exibe inicialmente 100 ativos na visualização do cartão e 200 ativos na visualização da lista. Mais ativos são carregados à medida que você percorre os resultados da pesquisa. Você pode selecionar mais ativos do que os ativos carregados. A contagem dos ativos selecionados é exibida no canto superior direito da página de resultados da pesquisa. Você pode operar na seleção, por exemplo, baixar os ativos selecionados, atualizar as propriedades de metadados em massa para os ativos selecionados ou adicionar os ativos selecionados a uma Coleção. Quando mais ativos são selecionados do que exibidos, uma ação é aplicada em todos os ativos selecionados ou uma caixa de diálogo exibe o número de ativos nos quais ela é aplicada. Para aplicar uma ação aos ativos que não foram carregados, verifique se todos os ativos estão selecionados explicitamente.
* Para pesquisar ativos que não contenham os metadados obrigatórios, consulte os metadados [](#mandatorymetadata)obrigatórios.
* A pesquisa usa todos os campos de metadados. Uma pesquisa genérica, como a pesquisa por 12, geralmente retorna muitos resultados. Para obter melhores resultados, use aspas de duplo (não simples) ou certifique-se de que o número seja contíguo a uma palavra sem um caractere especial (por exemplo, *shoe12*).
* A pesquisa de texto completo oferece suporte a operadores como - e ^. Para pesquisar essas letras como literais de string, coloque a expressão de pesquisa entre aspas duplos. Por exemplo, use &quot;Notebook - Beauty&quot; em vez de Notebook - Beauty.
* Se os resultados da pesquisa forem demais, limite o [escopo da pesquisa](#scope) para zero nos ativos desejados. Funciona melhor quando você tem alguma ideia de como procurar melhor os ativos desejados, por exemplo, tipo de arquivo específico, local específico, metadados específicos e assim por diante.

* **Marcação**: As tags ajudam a categorizar ativos que podem ser pesquisados e pesquisados com mais eficiência. A marcação ajuda a propagar a taxonomia apropriada para outros usuários e workflows. [!DNL Experience Manager] Métodos do oferta para marcar automaticamente ativos usando os serviços artificialmente inteligentes do Adobe Sensei que continuam a melhorar a identificação dos ativos com o uso e o treinamento. Quando você pesquisa ativos, as tags inteligentes são fatoradas se o recurso estiver ativado em sua conta. Funciona juntamente com a funcionalidade de pesquisa incorporada. Consulte Comportamento [da](#searchbehavior)pesquisa. Para otimizar a ordem na qual os resultados da pesquisa são exibidos, é possível [aumentar a classificação](#searchrank) de pesquisa de alguns ativos selecionados.

* **Indexação**: Somente metadados indexados e ativos são retornados nos resultados da pesquisa. Para melhor cobertura e desempenho, assegure a indexação correta e siga as práticas recomendadas. Consulte [indexação](#searchindex).

## Alguns exemplos ilustrando a pesquisa {#samples}

Use aspas de duplo em torno de palavras-chave para localizar ativos que contenham a frase exata na ordem exata, conforme especificado pelo usuário.

![Comportamento de pesquisa com e sem aspas](assets/search_with_quotes.gif)

*Figura: Comportamento de pesquisa com e sem aspas.*

**Pesquisar com o curinga** de asterisco: Para ampliar a pesquisa, use um asterisco antes ou depois da palavra de pesquisa para corresponder a qualquer número de caracteres. Por exemplo, a pesquisa por executar sem um asterisco não retorna ativos que contenham qualquer variação da palavra (incluindo nos metadados). Um asterisco substitui qualquer número de caracteres. Por exemplo,

* `run` retorna ativos com uma palavra-chave de execução exata
* `run*` retorna ativos com execução, execução, desistência e assim por diante.
* `*run` retorna para trás, execute-o novamente e assim por diante.
* `*run*` retorna todas as combinações possíveis.

![Ilustrando o uso do curinga de asterisco na pesquisa de Ativos usando um exemplo](assets/search_with_asterisk_run.gif)

*Figura: Ilustrando o uso de um asterisco curinga na pesquisa Ativos usando um exemplo.*

**Pesquisa com curinga de ponto de interrogação**: Para ampliar a pesquisa, use um ou mais &#39;?&#39; caracteres para corresponder ao número exato de caracteres. Por exemplo, na ilustração a seguir,

* `run???` O query não corresponde a nenhum ativo.

* `run????` query corresponde à palavra `running` com quatro caracteres depois `run`.

* `??run` O query corresponde à palavra `rerun` com dois caracteres antes `run`.

![Ilustrando o uso do caractere curinga de ponto de interrogação na pesquisa de Ativos usando um exemplo](assets/search_with_questionmark_run.gif)

*Figura: Ilustrando o uso do caractere curinga de ponto de interrogação na pesquisa de Ativos usando um exemplo.*

**Excluir uma palavra-chave**: Use o traço para procurar ativos que não contêm uma palavra-chave. Por exemplo, `running -shoe` o query retorna ativos que contêm `running`, mas não `shoe`. Da mesma forma, `camp -night` o query retorna ativos que contêm `camp` , mas não `night`. O query `camp-night` retorna ativos que contêm `camp` e `night`.

![Uso do traço para pesquisar ativos que não contenham uma palavra-chave excluída](assets/search_dash_exclude_keyword.gif)

*Figura: Uso do traço para pesquisar ativos que não contenham uma palavra-chave excluída.*

## tarefas de configuração e administração relacionadas à funcionalidade de pesquisa {#configadmin}

### Pesquisar configurações de índice {#searchindex}

A descoberta de ativos depende da indexação do conteúdo do DAM, incluindo os metadados. A descoberta mais rápida e precisa de ativos depende da indexação otimizada e das configurações apropriadas. Consulte índice [de](/help/assets/performance-tuning-guidelines.md#search-indexes)pesquisa, query de [carvalho e indexação](/help/sites-deploying/queries-and-indexing.md)e práticas [](/help/sites-deploying/best-practices-for-queries-and-indexing.md)recomendadas.

### Pesquisa visual ou de semelhança {#configvisualsearch}

A pesquisa visual usa marcação inteligente e requer [!DNL Experience Manager] 6.5.2.0 ou posterior. Após configurar a funcionalidade de marcação inteligente, siga estas etapas:

1. No [!DNL Experience Manager] CRXDE, no `/oak:index/lucene` nó, adicione as seguintes propriedades e valores e salve as alterações.

   * `costPerEntry` propriedade do tipo `Double` com o valor `10`.
   * `costPerExecution` propriedade do tipo `Double` com o valor `2`.
   * `refresh` propriedade do tipo `Boolean` com o valor `true`.

   Essa configuração permite pesquisas a partir do índice apropriado.

1. Para criar o índice Lucene, no CRXDE, em `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`, crie um nó com o nome `imageFeatures` do tipo `nt-unstructured`. No `imageFeatures` nó,

   * Adicione a `name` propriedade do tipo `String` com o valor `jcr:content/metadata/imageFeatures/haystack0`.
   * Adicione a `nodeScopeIndex` propriedade do tipo `Boolean` com o valor de `true`.
   * Adicione a `propertyIndex` propriedade do tipo `Boolean` com o valor de `true`.
   * Adicione a `useInSimilarity` propriedade do tipo `Boolean` com o valor `true`.

   Salve as alterações.

1. Acesse `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` e adicione `similarityTags` propriedade do tipo `Boolean` com o valor de `true`.
1. Aplique tags inteligentes aos ativos em seu [!DNL Experience Manager] repositório. Consulte [como configurar tags](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)inteligentes.
1. No CRXDE, no `/oak-index/damAssetLucene` nó, defina a `reindex` propriedade como `true`. Salve as alterações.
1. (Opcional) Se você tiver um formulário de pesquisa personalizado, copie o `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` nó para `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Salve as alterações.

Para obter informações relacionadas, consulte [entender tags inteligentes no Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-feature-video-use.html) e [como gerenciar tags](/help/assets/managing-smart-tags.md)inteligentes.

### Metadados obrigatórios {#mandatorymetadata}

Os usuários empresariais, administradores ou bibliotecários DAM podem definir alguns metadados como metadados obrigatórios que são necessários para que os processos de negócios funcionem. Por vários motivos, esses metadados podem estar ausentes em alguns ativos, como ativos herdados ou ativos migrados em massa. Os ativos com metadados ausentes ou inválidos são detectados e reportados com base na propriedade de metadados indexados. Para configurá-lo, consulte os metadados [](/help/assets/metadata-schemas.md#define-mandatory-metadata)obrigatórios.

### Modificar aspectos de pesquisa {#searchfacets}

Para melhorar a velocidade da descoberta, o [!DNL Experience Manager Assets] oferta pesquisa aspectos usando os quais você pode filtrar os resultados da pesquisa. O painel Filtros inclui algumas facetas padrão por padrão. Os administradores podem personalizar o painel Filtros para modificar os aspectos padrão usando os predicados incorporados. [!DNL Experience Manager] fornece uma boa coleção de predicados incorporados e um editor para personalizar as facetas. Consulte aspectos [de pesquisa](/help/assets/search-facets.md).

### Extrair texto ao carregar ativos {#extracttextupload}

Você pode configurar [!DNL Experience Manager] para extrair o texto dos ativos quando os usuários carregam ativos, como arquivos PSD ou PDF. [!DNL Experience Manager] indexa o texto extraído e ajuda os usuários a pesquisar nesses ativos com base no texto extraído. Consulte [fazer upload de ativos](/help/assets/managing-assets-touch-ui.md#uploading-assets).

### Previsões personalizadas para filtrar os resultados da pesquisa {#custompredicates}

Os predicados são usados para criar facetas. Os administradores podem personalizar os aspectos de pesquisa no painel Filtros usando predicados pré-configurados. Esses predicados podem ser personalizados usando sobreposições. Consulte [criar predicados](/help/assets/searchx.md)personalizados.

Você pode procurar ativos digitais com base em uma ou mais das seguintes propriedades. Filtros que se aplicam a algumas dessas propriedades estão disponíveis por padrão e alguns outros filtros podem ser criados personalizados para serem aplicados a outras propriedades.

| Campo Pesquisa | Pesquisar valores de propriedade |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| Tipos MIME | Imagens, Documentos, Multimídia, Arquivos ou Outros. |
| Última modificação | Hora, dia, semana, mês ou ano. |
| Tamanho do arquivo | Pequeno, Médio ou Grande. |
| Publicar status | Publicado ou Não publicado. |
| Status aprovado | Aprovado ou Rejeitada. |
| Orientação | Horizontal, Vertical ou Quadrado. |
| Estilo | Cor ou Preto e branco. |
| Altura do vídeo | Especificado como um valor mínimo e máximo. O valor é armazenado apenas nos metadados de representações de vídeo. |
| Largura do vídeo | Especificado como um valor mínimo e máximo. O valor é armazenado apenas nos metadados de representações de vídeo. |
| Formato de vídeo | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. O valor é armazenado nos metadados do vídeo de origem e de qualquer representação. |
| Codec de vídeo | x264. O valor é armazenado apenas nos metadados de representações de vídeo. |
| Taxa de bits do vídeo | Especificado como um valor mínimo e máximo. O valor é armazenado apenas nos metadados de representações de vídeo. |
| Codec de áudio | Libvorbis, Lame MP3, Codificação AAC. O valor é armazenado apenas nos metadados de representações de vídeo. |
| Taxa de áudio | Especificado como um valor mínimo e máximo. O valor é armazenado apenas nos metadados de representações de vídeo. |

## Trabalhar com resultados de pesquisa de ativos {#aftersearch}

Você pode fazer o seguinte com os ativos que pesquisou no Experience Manager:

* Propriedades de metadados de Visualização e outras informações.
* Baixe um ou mais ativos.
* Use as Ações da área de trabalho para abrir esses ativos no aplicativo da área de trabalho.
* Crie coleções inteligentes.

### Classificar resultados pesquisados {#sort}

Classifique os resultados da pesquisa para descobrir os ativos necessários mais rapidamente. You can sort the search results in list view and only when you select **[!UICONTROL [Files](#searchui)]**from the**[!UICONTROL  Filters ]**panel.[!DNL Experience Manager Assets]O usa a classificação do lado do servidor para classificar rapidamente todos os ativos (independente da quantidade) em uma pasta ou nos resultados de uma consulta de pesquisa. A classificação do lado do servidor fornece resultados mais rápidos e precisos do que a classificação do lado do cliente.

Na visualização da lista, você pode classificar os resultados da pesquisa da mesma forma que pode classificar os ativos em qualquer pasta. A classificação funciona nessas colunas — Nome, Título, Status, Dimensões, Tamanho, Classificação, Uso, (Data) Criado, (Data) Modificado, (Data) Publicado, Fluxo de trabalho e Finalizado.

Para obter as limitações da funcionalidade de classificação, consulte [limitações](#limitations).

### Verificar informações detalhadas de um ativo {#checkinfo}

Você pode verificar informações detalhadas de ativos pesquisados na página de resultados da pesquisa.

Para ver todos os metadados de um ativo, selecione o ativo e clique em **[!UICONTROL propriedades]** na barra de ferramentas.

Para verificar os comentários em um ativo ou histórico de versão de um ativo, clique nele para abrir uma visualização de grande. Abra a linha do tempo no painel à esquerda e selecione **[!UICONTROL Comentários]** ou **[!UICONTROL Versões]**. Também é possível classificar a atividade da linha do tempo, como comentários ou versões em ordem cronológica.

![Classificar entradas de linha do tempo para um ativo de pesquisa](assets/sort_timeline_search_results.gif)

*Figura: Classificar entradas de linha do tempo para um ativo de pesquisa.*

### Baixar ativos pesquisados {#download}

Você pode baixar os ativos pesquisados e suas representações da mesma forma que baixa ativos comuns de pastas. Selecione um ou mais ativos dos resultados da pesquisa e clique em **[!UICONTROL Download]** na barra de ferramentas.

### Propriedades de metadados de atualização em massa {#metadataupdates}

É possível fazer atualizações em massa nos campos de metadados comuns de vários ativos. Nos resultados da pesquisa, selecione um ou mais ativos. Clique em **[!UICONTROL Propriedades]** na barra de ferramentas e atualize os metadados conforme necessário. Clique em **[!UICONTROL Salvar e fechar]** quando terminar. Os metadados existentes anteriormente nos campos atualizados são substituídos.

Para os ativos que estão disponíveis em uma única pasta ou coleção, é mais fácil [atualizar os metadados em massa](/help/assets/managing-multiple-assets.md) sem usar a funcionalidade de pesquisa. Para os ativos que estão disponíveis em pastas ou que correspondem a critérios comuns, é mais rápido atualizar os metadados em massa por meio da pesquisa.

### Coleções inteligentes {#collections-1}

Uma coleção é um conjunto ordenado de ativos que podem incluir ativos de locais diferentes, pois as coleções contêm somente referências a esses ativos. As coleções são dos dois tipos a seguir:

* Uma lista de referência estática de ativos, pastas e outras coleções.
* Uma lista dinâmica (coleção inteligente) que preenche ativos na coleção com base em critérios de pesquisa.

Você pode criar coleções inteligentes com base nos critérios de pesquisa. No painel **[!UICONTROL Filtros]**, selecione **[!UICONTROL Arquivos]** e clique em **[!UICONTROL Salvar coleção inteligente]**. Consulte [gerenciar coleções](/help/assets/managing-collections-touch-ui.md).

## Solucionar problemas e resultados de pesquisa inesperados {#troubleshoot-unexpected-search-results-and-issues}

| Erro, problemas, sintomas | Possível motivo | Possível correção ou compreensão do problema |
|---|---|---|
| Resultados incorretos ao procurar ativos com metadados ausentes. | Ao pesquisar ativos que não têm os metadados obrigatórios, [!DNL Experience Manager] é possível exibir alguns ativos que têm metadados válidos. Os resultados são baseados na propriedade de metadados indexados. | Após a atualização dos metadados, a reindexação é necessária para refletir o estado correto dos metadados dos ativos. Consulte metadados [](metadata-schemas.md#define-mandatory-metadata)obrigatórios. |
| Muitos resultados de pesquisa. | Parâmetro de pesquisa abrangente. | Considere limitar o [escopo da pesquisa](#scope). O uso de tags inteligentes pode fornecer mais resultados de pesquisa do que o esperado. Consulte Comportamento [de pesquisa com tags](#withsmarttags)inteligentes. |
| Resultados de pesquisa não relacionados ou parcialmente relacionados. | Alterações no comportamento da pesquisa com marcação inteligente. | Entenda [como a pesquisa muda após a marcação](#withsmarttags)inteligente. |
| Nenhuma sugestão de preenchimento automático para ativos. | Os ativos carregados recentemente ainda não estão indexados. Os metadados não estão disponíveis imediatamente como sugestões quando você start digitar uma palavra-chave de pesquisa na barra Omnisearch. | [!DNL Assets] aguarda até a expiração de um período de tempo limite (uma hora por padrão) antes de executar um trabalho em segundo plano para indexar os metadados de todos os ativos recentemente carregados ou atualizados e, em seguida, adiciona os metadados à lista de sugestões. |
| Nenhum resultado de pesquisa. | <ul><li>Os ativos correspondentes ao seu query não existem. </li><li> Espaço em branco adicionado antes do query de pesquisa. </li><li> O campo de metadados não suportados contém a palavra-chave que você pesquisou.</li><li> Pesquisa feita durante o tempo de inatividade de um ativo. </li></ul> | <ul><li>Pesquise usando uma palavra-chave diferente. Como alternativa, use a marcação inteligente ou a pesquisa de semelhança para melhorar os resultados da pesquisa. </li><li>[Limitação](#limitations)conhecida.</li><li>Nem todos os campos de metadados são considerados para pesquisas. Consulte [escopo](#scope).</li><li>Pesquise mais tarde ou modifique os ativos necessários em tempo real e inativo.</li></ul> |
| O filtro de pesquisa ou um predicado não está disponível. | <ul><li>O filtro de pesquisa não está configurado.</li><li>Ele não está disponível para seu logon.</li><li>(Menos provável) As opções de pesquisa não são personalizadas na implantação que você está usando.</li></ul> | <ul><li>Entre em contato com o administrador para verificar se as personalizações de pesquisa estão disponíveis ou não.</li><li>Entre em contato com o administrador para verificar se sua conta tem o privilégio/permissões para usar a personalização.</li><li>Entre em contato com o administrador e verifique as personalizações disponíveis para a [!DNL Assets] implantação que você está usando.</li></ul> |
| Ao procurar imagens visualmente semelhantes, uma imagem esperada está ausente. | <ul><li>A imagem não está disponível em [!DNL Experience Manager].</li><li>A imagem não está indexada. Normalmente, quando é carregado recentemente.</li><li>A imagem não está com tags inteligentes.</li></ul> | <ul><li>Adicione a imagem a [!DNL Assets].</li><li>Entre em contato com o administrador para reindexar o repositório. Além disso, verifique se você está usando o índice apropriado.</li><li>Entre em contato com o administrador para obter uma tag inteligente dos ativos relevantes.</li></ul> |
| Ao procurar imagens visualmente semelhantes, uma imagem irrelevante é exibida. | Comportamento da pesquisa visual. | [!DNL Experience Manager] exibe quantos ativos potencialmente relevantes forem possíveis. Imagens menos relevantes, se houver, são adicionadas aos resultados, mas com uma classificação de pesquisa mais baixa. A qualidade das correspondências e a relevância dos ativos pesquisados diminuem à medida que você percorre os resultados da pesquisa. |
| Ao selecionar e operar nos resultados da pesquisa, todos os ativos pesquisados não são operados. | A opção [!UICONTROL Selecionar tudo] seleciona apenas os primeiros 100 resultados de pesquisa na visualização do cartão e os primeiros 200 resultados de pesquisa na visualização da lista. |  |

>[!MORELIKETHIS]
>
>* [Guia de implementação de pesquisa de Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [Configuração avançada de predições de pesquisa de tags e valores múltiplos](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/search-feature-video-use.html)
>* [Configurar pesquisa de tradução inteligente](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

