---
title: Pesquisar ativos e imagens digitais em [!DNL Adobe Experience Manager]
description: Saiba como localizar os ativos necessários em [!DNL Adobe Experience Manager] usando o painel Filtros e como usar os ativos que aparecem na pesquisa.
contentOwner: AG
mini-toc-levels: 1
feature: Pesquisar, metadados
role: User
exl-id: 588433b2-564a-430f-9d04-480465ece2ad
source-git-commit: 19dd081674b4954498d6aa62335f6b5a9f2a4146
workflow-type: tm+mt
source-wordcount: '5573'
ht-degree: 5%

---

# Pesquisar ativos em [!DNL Adobe Experience Manager] {#search-assets-in-aem}

[!DNL Adobe Experience Manager Assets] O oferece métodos robustos de detecção de ativos que ajudam a alcançar uma velocidade de conteúdo maior. Suas equipes podem reduzir o tempo de comercialização com uma experiência de pesquisa inteligente e contínua usando recursos prontos para uso e métodos personalizados. Pesquisar ativos é fundamental para o uso de um sistema de gerenciamento de ativos digitais — seja para uso adicional por parte dos criadores, para o gerenciamento robusto de ativos pelos usuários e profissionais de marketing ou para administração por administradores de DAM. Pesquisas simples, avançadas e personalizadas que você pode realizar por meio da [!DNL Assets] interface do usuário ou outros aplicativos e superfícies ajudam a atender a esses casos de uso.

[!DNL Experience Manager Assets] O suporta os seguintes casos de uso e este artigo descreve o uso, os conceitos, as configurações, as limitações e a solução de problemas desses casos de uso.

| Pesquisar por ativos | Configurar e administrar a funcionalidade de pesquisa | Trabalhar com resultados de pesquisa |
|---|---|---|
| [Pesquisas básicas](#searchbasics) | [Índice de pesquisa](#searchindex) | [Classificar resultados](#sort) |
| [Entender a interface do usuário de pesquisa](#searchui) | [Pesquisa visual ou de semelhança](#configvisualsearch) | [Verificar propriedades e metadados de um ativo](#checkinfo) |
| [Sugestões de pesquisa](#searchsuggestions) | [Metadados obrigatórios](#mandatorymetadata) | [Download](#download) |
| [Entender os resultados e o comportamento da pesquisa](#searchbehavior) | [Modificar aspectos de pesquisa](#searchfacets) | [Atualizações de metadados em massa](#metadataupdates) |
| [Classificação de pesquisa e reforço](#searchrank) | [Extração de texto](#extracttextupload) | [Coleções inteligentes](#collections) |
| [Pesquisa avançada: filtragem e escopo da pesquisa](#scope) | [Predicados personalizados](#custompredicates) | [Entender e solucionar problemas de resultados inesperados](#unexpected-results) |
| [Pesquisar a partir de outras soluções e aplicativos](#search-assets-other-surfaces):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brand-portal)</li><li>[Aplicativo de desktop do Experience Manager](#desktop-app)</li><li>[Imagens do Adobe Stock](#adobe-stock)</li><li>[Ativos da Dynamic Media](#dynamic-media)</li></ul> |  |  |
| [Seletor de ativos](#asset-picker) |  |  |
| [](#limitations) Limitações e  [dicas](#tips) |  |  |
| [Exemplos ilustrados](#samples) |  |  |

Pesquise ativos usando o campo Omnisearch na parte superior da interface da Web [!DNL Experience Manager]. Vá para **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]** em [!DNL Experience Manager], clique em ![ícone_de_pesquisa](assets/do-not-localize/search_icon.png) na barra superior, digite palavra-chave de pesquisa e selecione `Return`. Como alternativa, use o atalho de palavra-chave `/` (barra) para abrir o campo Omnisearch. `Location:Assets` O é pré-selecionado para limitar as pesquisas a ativos do DAM. [!DNL Experience Manager] O fornece sugestões para começar a digitar uma palavra-chave de pesquisa.

Use o painel **[!UICONTROL Filtros]** para pesquisar ativos, pastas, tags e metadados. Você pode filtrar os resultados da pesquisa com base em várias opções (predicados), como tipo de arquivo, tamanho do arquivo, data da última modificação, status do ativo, dados do insights e licenciamento do Adobe Stock. Você pode personalizar o painel Filtros e adicionar ou remover predicados de pesquisa usando [facetas de pesquisa](/help/assets/search-facets.md). O filtro [!UICONTROL File Type] no painel [!UICONTROL Filters] tem caixas de seleção de estado misto. Portanto, a menos que você selecione todos os predicados aninhados (ou formatos), as caixas de seleção de primeiro nível estarão parcialmente marcadas.

[!DNL Experience Manager] o recurso de pesquisa suporta a pesquisa de coleções e a pesquisa de ativos dentro de uma coleção. Consulte [pesquisar coleções](/help/assets/manage-collections.md).

## Entender a interface de pesquisa {#searchui}

Familiarize-se com a interface de pesquisa e as ações disponíveis.

![Entender a interface de resultados de pesquisa do Experience Manager Assets](assets/aem_search_results.png)

*Figura: Entenda a interface  [!DNL Experience Manager Assets] de resultados de pesquisa.*

**A.** Salve a pesquisa como uma coleção inteligente. **B.** Filtros ou predicados para limitar os resultados da pesquisa. **C.** Exibir arquivos, pastas ou ambos. **D.** Clique em Filtros para abrir ou fechar o painel à esquerda. **E.** O local de pesquisa é DAM. **F.** Campo Omnisearch com a palavra-chave de pesquisa fornecida pelo usuário. **G.** Selecione os resultados de pesquisa carregados. **H.** Número de resultados de pesquisa exibidos do total de resultados de pesquisa. **I.** Feche a pesquisa. **J.** Alterne entre exibição de cartão e exibição de lista.

### Aspectos de pesquisa dinâmica {#dynamicfacets}

Você pode descobrir os ativos desejados mais rapidamente na página de resultados da pesquisa usando o número dinamicamente atualizado de resultados de pesquisa esperados nos aspectos de pesquisa. O número esperado de ativos é atualizado mesmo antes de aplicar o filtro de pesquisa. Ver a contagem esperada em relação ao filtro ajuda a navegar pelos resultados da pesquisa de forma rápida e eficiente.

![Veja o número aproximado de ativos sem filtrar os resultados da pesquisa nos aspectos de pesquisa.](assets/asset_search_results_in_facets_filters.png)

*Figura: Veja o número aproximado de ativos sem filtrar os resultados da pesquisa nos aspectos de pesquisa.*

## Entender os resultados e o comportamento da pesquisa {#searchbehavior}

### Termos e resultados básicos da pesquisa {#searchbasics}

Você pode executar pesquisas de palavras-chave a partir do campo OmniSearch . A pesquisa de palavra-chave não diferencia maiúsculas de minúsculas e é uma pesquisa de texto completo (nos campos de metadados populares). Se mais de uma palavra-chave for usada, `AND` será o operador padrão entre as palavras-chave.

Os resultados são classificados por relevância, começando com correspondências mais próximas. Para várias palavras-chave, os resultados mais relevantes são os ativos que contêm ambos os termos em seus metadados. Nos metadados, as palavras-chave que aparecem como tags inteligentes são classificadas mais alto do que as palavras-chave que aparecem em outros campos de metadados. [!DNL Experience Manager] permite que um termo de pesquisa específico tenha um peso maior. Além disso, é possível [aumentar a classificação](#searchrank) de alguns ativos direcionados para termos de pesquisa específicos.

Para encontrar rapidamente os ativos relevantes, a interface avançada fornece mecanismos de filtragem, classificação e seleção. Você pode filtrar resultados com base em vários critérios e ver o número de ativos pesquisados para vários filtros. Como alternativa, execute novamente a pesquisa alterando a consulta no campo Omnisearch . Quando você altera os termos ou filtros de pesquisa, os outros filtros permanecem aplicados para preservar o contexto da pesquisa.

Quando os resultados são muitos ativos, [!DNL Experience Manager] exibe os primeiros 100 na exibição de cartão e 200 na exibição de lista. À medida que os usuários rolam, mais ativos são carregados. Isso melhora o desempenho. Assista a uma demonstração em vídeo do [número de ativos exibidos](https://www.youtube.com/watch?v=LcrGPDLDf4o).

Às vezes, você pode ver alguns ativos inesperados nos resultados da pesquisa. Para obter mais informações, consulte [resultados inesperados](#unexpected-results).

[!DNL Experience Manager] O pode pesquisar vários formatos de arquivo e os filtros de pesquisa podem ser personalizados para atender às necessidades de sua empresa. Entre em contato com o administrador para entender quais opções de pesquisa são disponibilizadas para o repositório DAM e quais restrições sua conta tem.

### Resultados com e sem Tags inteligentes aprimoradas {#withsmarttags}

Por padrão, a pesquisa [!DNL Experience Manager] combina os termos de pesquisa com uma cláusula AND. Por exemplo, considere pesquisar palavras-chave em execução. Somente os ativos com mulheres e palavras-chave em execução nos metadados aparecem nos resultados da pesquisa por padrão. O mesmo comportamento é retido quando caracteres especiais (pontos, sublinhados ou traços) são usados com as palavras-chave. As seguintes consultas de pesquisa retornam os mesmos resultados:

* `woman running`
* `woman.running`
* `woman-running`

No entanto, a consulta `woman -running` retorna ativos sem `running` em seus metadados.
O uso de Tags inteligentes adiciona uma cláusula `OR` extra para localizar qualquer um dos termos de pesquisa como as tags inteligentes aplicadas. Um ativo marcado com `woman` ou `running` usando Tags inteligentes também aparece nessa consulta de pesquisa. Então os resultados da pesquisa são uma combinação de...

* Ativos com `woman` e `running` palavras-chave nos metadados (comportamento padrão).

* Os ativos são marcados com tags inteligentes com uma das palavras-chave (comportamento das Tags inteligentes).

### Pesquisar sugestões à medida que você digita {#searchsuggestions}

Quando você começa a digitar palavras-chave, [!DNL Experience Manager] sugere as possíveis palavras-chave ou frases de pesquisa. As sugestões são baseadas nos metadados dos ativos existentes. [!DNL Experience Manager] indexa todos os campos de metadados para ajudar na pesquisa. Para fornecer sugestões de pesquisa, o sistema usa os valores dos poucos campos de metadados a seguir. Para fornecer sugestões de pesquisa, considere preencher os seguintes campos com palavras-chave apropriadas:

* Tags de ativos. (mapeia para `jcr:content/metadata/cq:tags`)
* Título do ativo. (mapeia para `jcr:content/metadata/dc:title`)
* Descrição do ativo. (mapeia para `jcr:content/metadata/dc:description`)
* Título no repositório JCR. O valor pode ser mapeado para o título do ativo. (mapeia para `jcr:content/jcr:title`)
* Descrição no repositório JCR. O valor pode ser mapeado para a descrição do ativo. (mapeia para `jcr:content/jcr:description`)

Para receber sugestões para mais de uma palavra-chave de pesquisa, continue digitando todas as palavras-chave sem selecionar qualquer sugestão para uma palavra-chave única.

![Digite várias palavras-chave para exibir sugestões que se ajustem a todas](assets/search_suggestionsmanykeywords.gif)

*Figura: Digite várias palavras-chave para exibir sugestões que se ajustem a todas.*

### Classificação de pesquisa e reforço {#searchrank}

Os resultados da pesquisa que correspondem a todos os termos de pesquisa nos campos de metadados são exibidos primeiro, seguidos pelos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. No exemplo acima, a ordem aproximada de exibição dos resultados da pesquisa é:

1. Corresponde a `woman running` nos vários campos de metadados.
1. Corresponde a `woman running` em tags inteligentes.
1. Corresponde a `woman` ou de `running` em tags inteligentes.

Você pode melhorar a relevância das palavras-chave para ativos específicos para ajudar a aumentar as pesquisas com base nas palavras-chave. Em outras palavras, as imagens para as quais você promove palavras-chave específicas são exibidas na parte superior dos resultados da pesquisa quando você pesquisa com base nessas palavras-chave.

1. Na interface do usuário [!DNL Assets], abra a página de propriedades do ativo. Clique em **[!UICONTROL Avançado]** e clique em **[!UICONTROL Adicionar]** em **[!UICONTROL Elevar para palavras-chave de pesquisa]**.
1. Na caixa **[!UICONTROL Promover de pesquisa]**, especifique uma palavra-chave para a qual deseja impulsionar a pesquisa da imagem e clique em **[!UICONTROL Adicionar]**. É possível especificar várias palavras-chave da mesma maneira.
1. Clique em **[!UICONTROL Salvar e fechar]**. O ativo que você promoveu para essa palavra-chave aparece entre os principais resultados de pesquisa.

Você pode usar isso para aproveitar ao otimizar a classificação de alguns ativos nos resultados de pesquisa para a palavra-chave direcionada. Veja o exemplo de vídeo abaixo. Para obter informações detalhadas, consulte [pesquisar em [!DNL Experience Manager]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*Vídeo: Entenda como os resultados da pesquisa são classificados e como a classificação pode ser influenciada.*

## Pesquisa avançada {#scope}

[!DNL Experience Manager] O fornece vários métodos, como filtros que se aplicam aos ativos pesquisados, para ajudá-lo a localizar os ativos desejados com mais rapidez. Abaixo estão descritos alguns métodos comumente usados. Alguns [exemplos ilustrados](#samples) são compartilhados abaixo.

**Procurar ficheiros ou pastas**: Nos resultados da pesquisa, consulte arquivos, pastas ou ambos. No painel **[!UICONTROL Filters]**, é possível selecionar a opção apropriada. Consulte [interface de pesquisa](#searchui).

**Pesquisar ativos em uma pasta**: É possível limitar a pesquisa para uma pasta específica. No painel **[!UICONTROL Filters]**, adicione o caminho de uma pasta. Você pode selecionar apenas uma pasta de cada vez.

![Limitar os resultados da pesquisa a uma pasta adicionando um caminho de pasta no painel Filtros](assets/search_folder_select.gif)

*Figura: Limite os resultados da pesquisa a uma pasta adicionando um caminho de pasta no painel Filtros .*

### Localizar imagens semelhantes {#visualsearch}

Para localizar imagens visualmente semelhantes a uma imagem selecionada pelo usuário, clique na opção **[!UICONTROL Localizar semelhante]** na exibição de cartão de uma imagem ou na barra de ferramentas. [!DNL Experience Manager]O exibe as imagens com tags inteligentes do repositório DAM que são semelhantes a uma imagem selecionada pelo usuário. Consulte [como configurar a pesquisa de semelhança](#configvisualsearch).

![Encontre imagens semelhantes usando a opção na exibição de cartão](assets/search_find_similar.png)

*Figura: Encontre imagens semelhantes usando a opção na exibição de cartão.*

### Imagens do Adobe Stock {#adobe-stock}

Na interface do usuário [!DNL Experience Manager], os usuários podem pesquisar [Adobe Stock assets](/help/assets/aem-assets-adobe-stock.md) e licenciar os ativos necessários. Adicione `Location: Adobe Stock` na barra Omnisearch. Você também pode usar o painel Filtros para localizar todos os ativos licenciados ou não licenciados ou pesquisar um ativo específico usando o número de arquivo do Adobe Stock.

### Ativos da Dynamic Media {#dmassets}

Você pode filtrar por imagens do Dynamic Media selecionando **[!UICONTROL Dynamic Media]** > **[!UICONTROL Conjuntos]** no painel **[!UICONTROL Filtros]**. Isso filtra e exibe ativos como conjuntos de imagens, carrosséis, conjuntos de mídia mista e conjuntos de rotação.

### Pesquisa GQL usando valores específicos nos campos de metadados {#gql-search}

Você pode pesquisar ativos com base em valores exatos de campos de metadados, como título, descrição e criador. O recurso de pesquisa de texto completo do GQL busca apenas os ativos cujo valor de metadados corresponda exatamente à sua consulta de pesquisa. Os nomes das propriedades (Criador, Título e assim por diante) e os valores distinguem maiúsculas de minúsculas.

| Campo de metadados | Valor e uso da faceta |
|---|---|
| Título | title:John |
| Criador | criador:John |
| Local | local:NA |
| Descrição | description: &quot;Imagem de exemplo&quot; |
| Ferramenta Criador | criatortool: &quot;Adobe Photoshop CC 2015&quot; |
| Proprietário de direitos autorais | copyrights towner: &quot;Adobe Systems&quot; |
| Contribuinte | colaborador:John |
| Termos de Uso  | usageterms:&quot;CopyRights Reserved&quot; |
| Criado | criado:AAAA-MM-DDTHH |
| Expira Data | expira:AAAA-MM-DDTHH |
| No horário | ontime:YYYY-MM-DDTHH |
| Hora de desligar | offtime:AAAA-MM-DDTHH |
| Intervalo de tempo (expira o dateontime, offtime) | campo de faceta : limite inferior..upperbound |
| Caminho | /content/dam/&lt;nome da pasta> |
| Título do PDF | pdftitle:&quot;Documento do Adobe&quot; |
| Assunto | assunto: &quot;Formação&quot; |
| Tags | Tags: &quot;Localização E Viagem&quot; |
| Tipo | type: &quot;image\png&quot; |
| Largura da imagem | largura:limite inferior..upperbound |
| Altura da imagem | altura:limite inferior..upperbound |
| Person | pessoa:John |

As propriedades `path`, `limit`, `size` e `orderby` não podem ser combinadas usando o operador `OR` com qualquer outra propriedade.

<!-- TBD: Where are the limit, size, orderby properties defined?
-->

A palavra-chave de uma propriedade gerada pelo usuário é seu rótulo de campo no editor de propriedades em minúsculas, com espaços removidos.

Estes são alguns exemplos de formatos de pesquisa para consultas complexas:

* Para exibir todos os ativos com vários campos de facetas (por exemplo: title=John Doe e ferramenta criadora = Adobe Photoshop): `title:"John Doe" creatortool:Adobe*`
* Para exibir todos os ativos quando o valor das facetas não for uma única palavra, mas uma frase (por exemplo: title=Scott Reynolds): `title:"Scott Reynolds"`
* Para exibir ativos com vários valores de uma única propriedade (por exemplo: title=Scott Reynolds ou John Doe): `title:"Scott Reynolds" OR "John Doe"`
* Para exibir ativos com valores de propriedade começando com uma string específica (por exemplo: é Scott Reynolds): `title:Scott*`
* Para exibir ativos com valores de propriedade terminando com uma string específica (por exemplo: é Scott Reynolds): `title:*Reynolds`
* Para exibir ativos com um valor de propriedade que contenha uma string específica (por exemplo: título = Sala de Reunião de Basileia): `title:*Meeting*`
* Para exibir ativos que contêm uma string específica e têm um valor de propriedade específico (por exemplo: procure por Adobe de sequência em ativos com title=John Doe): `*Adobe* title:"John Doe"`

## Pesquisar ativos de outras [!DNL Experience Manager] ofertas ou interfaces {#search-assets-other-surfaces}

[!DNL Adobe Experience Manager] conecta o repositório DAM a várias outras  [!DNL Experience Manager] soluções para fornecer acesso mais rápido a ativos digitais e simplificar os fluxos de trabalho criativos. Qualquer descoberta de ativo começa com navegação ou pesquisa. O comportamento de pesquisa permanece basicamente o mesmo em várias superfícies e soluções. Alguns métodos de pesquisa são alterados conforme o público-alvo, os casos de uso e a interface do usuário variam nas soluções [!DNL Experience Manager]. Os métodos específicos estão documentados para as soluções individuais nos links abaixo. As dicas e comportamentos universalmente aplicáveis estão documentados neste artigo.

### Pesquisar ativos no painel Adobe Asset Link {#aal}

Usando o Adobe Asset Link, os profissionais criativos agora podem acessar o conteúdo armazenado em [!DNL Experience Manager Assets], sem sair dos aplicativos Adobe Creative Cloud compatíveis. Os criadores podem navegar, pesquisar, sair e fazer check-in de ativos com facilidade usando o painel no aplicativo nos aplicativos [!DNL Adobe Creative Cloud]: [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] e [!DNL Adobe InDesign]. O Asset Link também permite que os usuários pesquisem resultados visualmente semelhantes. Os resultados da exibição de pesquisa visual são fornecidos por algoritmos de aprendizado de máquina da Adobe Sensei e ajudam os usuários a encontrar imagens esteticamente semelhantes. Consulte [pesquisar e procurar ativos](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) usando o Adobe Asset Link.

### Pesquisar ativos no aplicativo de desktop [!DNL Experience Manager] {#desktop-app}

Os profissionais de criação usam o aplicativo de desktop para tornar o [!DNL Experience Manager Assets] facilmente pesquisável e disponível em seu desktop local (Win ou Mac). Os criadores podem revelar facilmente os ativos desejados no Mac Finder ou no Windows Explorer, abertos em aplicativos de desktop e alterados localmente - as alterações são salvas em [!DNL Experience Manager] com uma nova versão criada no repositório. O aplicativo suporta pesquisas básicas usando uma ou mais palavras-chave, curingas `*` e `?` e operador `AND`. Consulte [procurar, pesquisar e visualizar ativos](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) no aplicativo de desktop.

### Pesquisar ativos em [!DNL Brand Portal] {#brand-portal}

Usuários de linha de negócios e profissionais de marketing usam o Brand Portal para compartilhar com eficiência e segurança os ativos digitais aprovados com suas equipes internas estendidas, parceiros e revendedores. Consulte [pesquisar ativos no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### Pesquisar imagens [!DNL Adobe Stock] {#adobe-stock1}

Na interface do usuário [!DNL Experience Manager], os usuários podem pesquisar ativos da Adobe Stock e licenciar os ativos necessários. Adicione `Location: Adobe Stock` no campo Omnisearch . Você também pode usar o painel **[!UICONTROL Filters]** para localizar todos os ativos licenciados ou não licenciados ou pesquisar um ativo específico usando o número de arquivo Adobe Stock. Consulte [gerenciar [!DNL Adobe Stock] imagens em [!DNL Experience Manager]](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Pesquisar ativos [!DNL Dynamic Media] {#dynamic-media}

Você pode filtrar por imagens do Dynamic Media selecionando **[!UICONTROL Dynamic Media]** > **[!UICONTROL Conjuntos]** no painel **[!UICONTROL Filtros]**. Isso filtra e exibe ativos como conjuntos de imagens, carrosséis, conjuntos de mídia mista e conjuntos de rotação. Ao criar páginas da Web, os autores podem pesquisar por conjuntos no Localizador de conteúdo. Há um filtro para conjuntos disponível em um menu pop-up.

### Pesquisar ativos no Localizador de conteúdo ao criar páginas da Web {#content-finder}

Os autores podem usar o Localizador de conteúdo para pesquisar o repositório DAM para os ativos relevantes e usar os ativos nas páginas da Web que eles criam. Os autores também podem usar a funcionalidade Ativos conectados para procurar ativos que estão disponíveis em uma implantação remota [!DNL Experience Manager]. Os autores podem usar esses ativos em páginas da Web em uma implantação local [!DNL Experience Manager]. Consulte [usar ativos remotos](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### Pesquisar coleções {#collections}

[!DNL Experience Manager] o recurso de pesquisa suporta a pesquisa de coleções e a pesquisa de ativos dentro de uma coleção. Consulte [pesquisar coleções](/help/assets/manage-collections.md).

## Seletor de ativos {#asset-picker}

>[!NOTE]
>
>O seletor de ativo era chamado [seletor de ativo](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) em versões anteriores de [!DNL Adobe Experience Manager].

O seletor de ativos permite pesquisar, filtrar e navegar pelos ativos do DAM de uma maneira especial. O seletor de ativos está disponível em `https://[aem_server]:[port]/aem/assetpicker.html`. Você pode buscar os metadados dos ativos selecionados usando o seletor de ativos. Você pode iniciá-lo com parâmetros de solicitação compatíveis, como tipo de ativo (imagem, vídeo, texto) e modo de seleção (seleções únicas ou múltiplas). Esses parâmetros definem o contexto do seletor de ativos para uma instância de pesquisa específica e permanecem intactos durante toda a seleção.

O seletor de ativos usa a mensagem HTML5 `Window.postMessage` para enviar dados do ativo selecionado para o recipient. Funciona somente no modo de navegação e somente com a página de resultados do Omnisearch.

Passe os seguintes parâmetros de solicitação em um URL para iniciar o seletor de ativos em um contexto específico:

| Nome | Valores | Exemplo | Propósito |
|---|---|---|---|
| sufixo do recurso (B) | Caminho da pasta como o sufixo de recurso no URL: [https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | Para iniciar o seletor de ativos com uma pasta específica selecionada, por exemplo, com a pasta `/content/dam/we-retail/en/activities` selecionada, o URL deve ser do formato: `https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images` | Se você precisar selecionar uma pasta específica quando o seletor de ativos for iniciado, passe-a como um sufixo de recurso. |
| `mode` | único, múltiplo | <ul><li>`https://localhost:4502/aem/assetpicker.html?mode=single`</li><li>`https://localhost:4502/aem/assetpicker.html?mode=multiple`</li></ul> | No modo múltiplo, é possível selecionar vários ativos simultaneamente usando o seletor de ativos. |
| `dialog` | true, false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | Use esses parâmetros para abrir o seletor de ativos como Caixa de diálogo do Granite. Essa opção só é aplicável quando você inicia o seletor de ativos por meio do Campo de caminho do Granite e o configura como URL pickerSrc. |
| `root` | &lt;folder_path> | `https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities` | Use essa opção para especificar a pasta raiz do seletor de ativos. Nesse caso, o seletor de ativos permite selecionar apenas ativos secundários (diretos/indiretos) na pasta raiz. |
| `viewmode` | pesquisa |  | Para iniciar o seletor de ativos no modo de pesquisa, com os parâmetros `assettype` e `mimetype`. |
| `assettype` | Imagens, documentos, multimídia, arquivos. | <ul><li>`https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives` </li></ul> | Use a opção para filtrar tipos de ativos com base no valor fornecido. |
| `mimetype` | Tipo MIME (`/jcr:content/metadata/dc:format`) de um ativo (curinga também compatível). | <ul><li>`https://localhost:4502/aem/assetpicker.html?mimetype=image/png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png`</li></ul> | Use-o para filtrar ativos com base no tipo MIME. |

Para acessar a interface do seletor de ativos, vá para `https://[aem_server]:[port]/aem/assetpicker`. Navegue até a pasta desejada e selecione um ou mais ativos. Como alternativa, pesquise o ativo desejado na caixa Omnisearch , aplique o filtro conforme necessário e selecione-o.

![Navegar e selecionar ativo no seletor de ativos](assets/assetpicker.png)

*Figura: Procure e selecione ativo no seletor de ativos.*

## Limitações           {#limitations}

O recurso de pesquisa em [!DNL Experience Manager Assets] tem as seguintes limitações:

* Não insira um espaço à esquerda na consulta de pesquisa; caso contrário, a pesquisa não funcionará.
* [!DNL Experience Manager] pode continuar a mostrar o termo de pesquisa depois de selecionar as propriedades de um ativo de resultados pesquisados e cancelar a pesquisa.  <!-- (CQ-4273540) -->
* Ao procurar pastas ou arquivos e pastas, os resultados da pesquisa não podem ser classificados em nenhum parâmetro.
* Se você selecionar `Return` sem digitar na barra Omnisearch, [!DNL Experience Manager] retornará uma lista de somente arquivos e não pastas. Se você pesquisar especificamente por pastas sem usar uma palavra-chave, [!DNL Experience Manager] não retornará nenhum resultado.
* Você pode realizar pesquisa de texto completo nas pastas. Especifique um termo de pesquisa para que a pesquisa funcione.

Pesquisa visual ou pesquisa de semelhança tem as seguintes limitações:

* A pesquisa visual funciona melhor com um repositório grande. Embora não haja um número mínimo de imagens necessário para bons resultados, a qualidade das correspondências com algumas imagens não é tão boa quanto as correspondências de um repositório grande.
* Não é possível alterar o modelo ou treinar [!DNL Experience Manager] para localizar imagens semelhantes. Por exemplo, adicionar ou remover tags inteligentes de alguns ativos não altera o modelo. Os ativos são excluídos dos resultados de pesquisa visualmente semelhantes.

A funcionalidade de pesquisa pode ter limitações de desempenho nos seguintes cenários:

* A exibição de cartão tem um tempo de carregamento mais rápido em comparação à exibição em lista para exibir os resultados da pesquisa.

## Dicas de pesquisa {#tips}

* Ao monitorar o status de revisão de ativos, use a opção apropriada para descobrir quais ativos estão aprovados ou quais ativos estão pendentes de aprovação.
* Use o predicado Insights para procurar ativos compatíveis com base em suas estatísticas de uso obtidas de vários aplicativos criativos. Os dados de uso são agrupados em Canais de Uso, Impressões, Cliques e Mídia , onde os ativos aparecem em categorias.
* Use a caixa de seleção **[!UICONTROL Selecionar tudo]** para selecionar os ativos pesquisados. [!DNL Experience Manager] exibe inicialmente 100 ativos na exibição de cartão e 200 ativos na exibição em lista. Mais ativos são carregados à medida que você rolar os resultados da pesquisa. Você pode selecionar mais ativos do que os ativos carregados. A contagem dos ativos selecionados é exibida no canto superior direito da página de resultados da pesquisa. Você pode operar na seleção, por exemplo, baixar os ativos selecionados, atualizar as propriedades de metadados em massa dos ativos selecionados ou adicionar os ativos selecionados a uma Coleção. Quando mais ativos são selecionados do que exibidos, uma ação é aplicada em todos os ativos selecionados ou uma caixa de diálogo exibe o número de ativos em que é aplicada. Para aplicar uma ação aos ativos que não foram carregados, verifique se todos os ativos foram selecionados explicitamente.
* Para pesquisar ativos que não contêm os metadados obrigatórios, consulte [metadados obrigatórios](#mandatorymetadata).
* A pesquisa usa todos os campos de metadados. Uma pesquisa genérica, como a pesquisa por 12, geralmente retorna muitos resultados. Para obter melhores resultados, use aspas duplas (não simples) ou verifique se o número é contíguo a uma palavra sem um caractere especial (por exemplo `shoe12`).
* A pesquisa de texto completo oferece suporte a operadores como `-` e `^`. Para pesquisar essas letras como literais de string, coloque a expressão de pesquisa entre aspas duplas. Por exemplo, use `"Notebook - Beauty"` em vez de `Notebook - Beauty`.
* Se os resultados da pesquisa forem muitos, limite o [escopo da pesquisa](#scope) para zero nos ativos desejados. Ele funciona melhor quando você tem uma ideia de como procurar melhor os ativos desejados, por exemplo, tipo de arquivo específico, local específico, metadados específicos e assim por diante.

* **Marcação**: As tags ajudam a categorizar ativos que podem ser pesquisados e pesquisados com mais eficiência. A marcação ajuda a propagar a taxonomia apropriada para outros usuários e fluxos de trabalho. [!DNL Experience Manager] O oferece métodos para marcar ativos automaticamente usando serviços inteligentes artificialmente da Adobe Sensei que estão melhorando a marcação dos ativos com uso e treinamento. Ao procurar ativos, as tags inteligentes são fatoradas se o recurso estiver ativado em sua conta. Funciona junto com a funcionalidade de pesquisa integrada. Consulte [comportamento de pesquisa](#searchbehavior). Para otimizar a ordem em que os resultados da pesquisa são exibidos, você pode [aumentar a classificação de pesquisa](#searchrank) de alguns ativos selecionados.

* **Indexação**: Somente metadados indexados e ativos são retornados nos resultados da pesquisa. Para melhor cobertura e desempenho, assegure a indexação adequada e siga as práticas recomendadas. Consulte [indexing](#searchindex).

* Para excluir ativos específicos dos resultados da pesquisa, use a propriedade `excludedPath` no índice Lucene.

## Alguns exemplos ilustrando a pesquisa {#samples}

Use aspas duplas em palavras-chave para localizar ativos que contenham a frase exata na ordem exata, conforme especificado pelo usuário.

![Comportamento de pesquisa com e sem aspas](assets/search_with_quotes.gif)

*Figura: Comportamento de pesquisa com e sem aspas.*

**Pesquisar com asterisco curinga**: Para ampliar a pesquisa, use um asterisco antes ou depois da palavra de pesquisa para corresponder a qualquer número de caracteres. Por exemplo, a pesquisa por executar sem um asterisco não retorna ativos que contenham qualquer variação da palavra (incluindo nos metadados). Um asterisco substitui qualquer número de caracteres. Por exemplo,

* `run` retorna ativos com a palavra-chave de execução exata
* `run*` retorna ativos com  `running`,  `run`,  `runaway` e assim por diante.
* `*run` retorna ativos com  `outrun`,  `rerun`, e assim por diante.
* `*run*` retorna todas as combinações possíveis.

![Ilustração do uso de asterisco curinga na pesquisa de ativos usando um exemplo](assets/search_with_asterisk_run.gif)

*Figura: Ilustração do uso do asterisco curinga na pesquisa de Ativos usando um exemplo.*

**Pesquisar com o curinga do ponto de interrogação**: Para ampliar a pesquisa, use um ou mais &#39;?&#39; caracteres para corresponder ao número exato de caracteres. Por exemplo, na ilustração a seguir,

* `run???` A consulta não corresponde a nenhum ativo.

* `run????` O query corresponde a palavra  `running` com quatro caracteres depois de  `run`.

* `??run` O query corresponde a palavra  `rerun` com dois caracteres antes  `run`.

![Ilustração do uso do curinga do ponto de interrogação na pesquisa de Ativos usando um exemplo](assets/search_with_questionmark_run.gif)

*Figura: Ilustração do uso do curinga do ponto de interrogação na pesquisa de Ativos usando um exemplo.*

**Excluir uma palavra-chave**: Use traço para procurar ativos que não contêm uma palavra-chave. Por exemplo, a consulta `running -shoe` retorna ativos que contêm `running`, mas não `shoe`. Da mesma forma, a consulta `camp -night` retorna ativos que contêm `camp`, mas não `night`. A consulta `camp-night` retorna ativos que contêm `camp` e `night`.

![Uso de traço para procurar ativos que não contêm uma palavra-chave excluída](assets/search_dash_exclude_keyword.gif)

*Figura: Use o traço para procurar ativos que não contêm uma palavra-chave excluída.*

## Tarefas de configuração e administração relacionadas à funcionalidade de pesquisa {#configadmin}

### Pesquisar configurações do índice {#searchindex}

A descoberta de ativos depende da indexação do conteúdo do DAM, incluindo os metadados. A detecção mais rápida e precisa de ativos depende da indexação otimizada e das configurações apropriadas. Consulte [índice de pesquisa](/help/assets/performance-tuning-guidelines.md#search-indexes), [consultas e indexação do oak](/help/sites-deploying/queries-and-indexing.md) e [práticas recomendadas](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

Para excluir ativos específicos dos resultados da pesquisa, use a propriedade `excludedPath` no índice Lucene.

### Pesquisa visual ou de semelhança {#configvisualsearch}

A pesquisa visual usa Tags inteligentes. Após configurar a funcionalidade de marcação inteligente, siga estas etapas.

1. No [!DNL Experience Manager] CRXDE, no nó `/oak:index/lucene`, adicione as seguintes propriedades e valores e salve as alterações.

   * `costPerEntry` propriedade do tipo  `Double` com o valor  `10`.
   * `costPerExecution` propriedade do tipo  `Double` com o valor  `2`.
   * `refresh` propriedade do tipo  `Boolean` com o valor  `true`.

   Essa configuração permite pesquisas no índice apropriado.

1. Para criar o índice Lucene, no CRXDE, em `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`, crie o nó chamado `imageFeatures` do tipo `nt-unstructured`. No nó `imageFeatures`,

   * Adicione a propriedade `name` do tipo `String` com o valor `jcr:content/metadata/imageFeatures/haystack0`.
   * Adicione a propriedade `nodeScopeIndex` do tipo `Boolean` com o valor `true`.
   * Adicione a propriedade `propertyIndex` do tipo `Boolean` com o valor `true`.
   * Adicione a propriedade `useInSimilarity` do tipo `Boolean` com o valor `true`.

   Salve as alterações.

1. Acesse `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` e adicione a propriedade `similarityTags` do tipo `Boolean` com o valor `true`.
1. Aplique Tags inteligentes aos ativos em seu repositório [!DNL Experience Manager]. Consulte [como configurar tags inteligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/tagging.html#configuring).
1. No CRXDE, no nó `/oak-index/damAssetLucene`, defina a propriedade `reindex` para `true`. Salve as alterações.
1. (Opcional) Se você tiver personalizado o formulário de pesquisa, copie o nó `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` para `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Salve as alterações.

Para obter informações relacionadas, consulte [entender tags inteligentes no Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html) e [como gerenciar tags inteligentes](/help/assets/enhanced-smart-tags.md).

>[!CAUTION]
>
>Se a indexação do Lucene for feita a partir de [!DNL Adobe Experience Manager], a pesquisa baseada em tags inteligentes não funcionará conforme esperado.

### Metadados obrigatórios {#mandatorymetadata}

Usuários empresariais, administradores ou bibliotecas DAM podem definir alguns metadados como metadados obrigatórios que são necessários para que os processos comerciais funcionem. Por vários motivos, alguns ativos podem não ter esses metadados, como ativos herdados ou ativos migrados em massa. Os ativos com metadados ausentes ou inválidos são detectados e relatados com base na propriedade de metadados indexada. Para configurá-lo, consulte [metadados obrigatórios](/help/assets/metadata-schemas.md#define-mandatory-metadata).

### Modificar aspectos de pesquisa {#searchfacets}

Para melhorar a velocidade da descoberta, [!DNL Experience Manager Assets] oferece facetas de pesquisa usando o que você pode filtrar os resultados da pesquisa. O painel Filtros inclui algumas facetas padrão por padrão. Os administradores podem personalizar o painel Filtros para modificar as facetas padrão usando os predicados incorporados. [!DNL Experience Manager] O fornece uma boa coleção de predicados incorporados e um editor para personalizar as facetas. Consulte [pesquisar aspectos](/help/assets/search-facets.md).

### Extrair texto ao fazer upload de ativos {#extracttextupload}

Você pode configurar [!DNL Experience Manager] para extrair o texto dos ativos quando os usuários fazem upload de ativos, como arquivos PSD ou PDF. [!DNL Experience Manager] indexa o texto extraído e ajuda os usuários a pesquisar esses ativos com base no texto extraído. Consulte [fazer upload de ativos](/help/assets/manage-assets.md#uploading-assets).

Se a extração de texto se tornar muito intensiva em recursos para sua implantação, considere [desativar a extração de texto](https://helpx.adobe.com/experience-manager/kb/Disable-binary-text-extraction-to-optimize-Lucene-indexing-AEM.html).

### Predicados personalizados para filtrar os resultados da pesquisa {#custompredicates}

Os predicados são usados para criar facetas. Os administradores podem personalizar os aspectos de pesquisa no painel Filtros usando predicados pré-configurados. Esses predicados podem ser personalizados usando sobreposições. Consulte [criar predicados personalizados](/help/assets/searchx.md).

Você pode pesquisar ativos digitais com base em uma ou mais das seguintes propriedades. Os filtros que se aplicam a algumas dessas propriedades estão disponíveis por padrão e alguns outros filtros podem ser personalizados para serem aplicados em outras propriedades.

| Campo Pesquisa | Pesquisar valores de propriedade |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| Tipos MIME | Imagens, documentos, multimídia, arquivos ou outros. |
| Última modificação | Hora, dia, semana, mês ou ano. |
| Tamanho do arquivo | Pequeno, Médio ou Grande. |
| Publicar status | Publicado ou Não publicado. |
| Status Aprovado | Aprovado ou Rejeitado. |
| Orientação | Horizontal, Vertical ou Quadrado. |
| Estilo | Cor ou Preto e Branco. |
| Altura do vídeo | Especificado como valor mínimo e máximo. O valor é armazenado somente nos metadados de representações de vídeo. |
| Largura do vídeo | Especificado como valor mínimo e máximo. O valor é armazenado somente nos metadados de representações de vídeo. |
| Formato de vídeo | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. O valor é armazenado nos metadados do vídeo de origem e de qualquer representação. |
| Codec de vídeo | x264. O valor é armazenado somente nos metadados de representações de vídeo. |
| Taxa de bits do vídeo | Especificado como valor mínimo e máximo. O valor é armazenado somente nos metadados de representações de vídeo. |
| Codec de áudio | Libvorbis, Lame MP3, Codificação AAC. O valor é armazenado somente nos metadados de representações de vídeo. |
| Taxa de áudio | Especificado como valor mínimo e máximo. O valor é armazenado somente nos metadados de representações de vídeo. |

## Trabalhar com resultados de pesquisa de ativos {#aftersearch}

Você pode fazer o seguinte com os ativos que pesquisou em [!DNL Experience Manager]:

* Exibir propriedades de metadados e outras informações.
* Baixe um ou mais ativos.
* Use as Ações do desktop para abrir esses ativos no aplicativo de desktop.
* Criar coleções inteligentes.

### Classificar resultados de pesquisa {#sort}

Classifique os resultados da pesquisa para descobrir mais rapidamente os ativos necessários. Você pode classificar os resultados da pesquisa na exibição de lista e somente ao selecionar **[[!UICONTROL Arquivos]](#searchui)** no painel **[!UICONTROL Filtros]**. [!DNL Assets]O usa a classificação do lado do servidor para classificar rapidamente todos os ativos (independente da quantidade) em uma pasta ou nos resultados de uma consulta de pesquisa. A classificação do lado do servidor fornece resultados mais rápidos e precisos do que a classificação do lado do cliente.

Na exibição em lista, é possível classificar os resultados da pesquisa da mesma maneira que você pode classificar ativos em qualquer pasta. A classificação funciona nessas colunas — Nome, Título, Status, Dimension, Tamanho, Classificação, Uso, (Data) Criado, (Data) Modificado, (Data) Publicado, Fluxo de trabalho e Check-out.

Para obter limitações da funcionalidade de classificação, consulte [limitações](#limitations).

### Verificar informações detalhadas de um ativo {#checkinfo}

Você pode verificar informações detalhadas de ativos pesquisados na página de resultados da pesquisa.

Para visualizar todos os metadados de um ativo, selecione-o e clique em **[!UICONTROL properties]** na barra de ferramentas.

Para verificar os comentários em um ativo ou histórico de versão de um ativo, clique nele para abrir uma visualização de grande. Abra a linha do tempo no painel à esquerda e selecione **[!UICONTROL Comentários]** ou **[!UICONTROL Versões]**. Também é possível classificar a atividade da linha do tempo, como comentários ou versões em ordem cronológica.

![Classificar entradas de linha do tempo de um ativo de pesquisa](assets/sort_timeline_search_results.gif)

*Figura: Classifique entradas de linha do tempo de um ativo de pesquisa.*

### Baixar ativos pesquisados {#download}

Você pode baixar os ativos pesquisados e suas representações da mesma forma que faz o download de ativos comuns a partir de pastas. Selecione um ou mais ativos dos resultados da pesquisa e clique em **[!UICONTROL Baixar]** na barra de ferramentas.

### Propriedades de metadados de atualização em massa {#metadataupdates}

É possível fazer atualizações em massa nos campos de metadados comuns de vários ativos. Nos resultados da pesquisa, selecione um ou mais ativos. Clique em **[!UICONTROL Properties]** na barra de ferramentas e atualize os metadados conforme necessário. Clique em **[!UICONTROL Salvar e fechar]** quando terminar. Os metadados existentes anteriormente nos campos atualizados são substituídos.

Para os ativos que estão disponíveis em uma única pasta ou coleção, é mais fácil [atualizar os metadados em massa](/help/assets/metadata.md) sem usar a funcionalidade de pesquisa. Para os ativos que estão disponíveis em pastas ou que correspondem a um critério comum, é mais rápido atualizar os metadados em massa por meio da pesquisa.

### Coleções inteligentes {#smart-collections}

Uma coleção é um conjunto ordenado de ativos que pode incluir ativos de locais diferentes, pois as coleções contêm apenas referências a esses ativos. As coleções são dos dois tipos a seguir:

* Uma lista de referência estática de ativos, pastas e outras coleções.
* Uma lista dinâmica (coleção inteligente) que preenche ativos na coleção com base em um critério de pesquisa.

Você pode criar coleções inteligentes com base nos critérios de pesquisa. No painel **[!UICONTROL Filtros]**, selecione **[!UICONTROL Arquivos]** e clique em **[!UICONTROL Salvar coleção inteligente]**. Consulte [gerenciar coleções](/help/assets/manage-collections.md).

## Resultados e problemas de pesquisa inesperados {#unexpected-results}

| Erro, problemas, sintomas | Possível motivo | Possível correção ou compreensão do problema |
|---|---|---|
| Resultados incorretos ao procurar ativos com metadados ausentes. | Ao pesquisar ativos que não têm os metadados obrigatórios, [!DNL Experience Manager] pode exibir alguns ativos que têm metadados válidos. Os resultados são baseados na propriedade de metadados indexados. | Após atualizar os metadados, a reindexação é necessária para refletir o estado correto dos metadados do ativo. Consulte [metadados obrigatórios](metadata-schemas.md#define-mandatory-metadata). |
| Muitos resultados de pesquisa. | Amplo parâmetro de pesquisa. | Considere limitar o [escopo da pesquisa](#scope). O uso de tags inteligentes pode fornecer mais resultados de pesquisa do que o esperado. Consulte [comportamento de pesquisa com tags inteligentes](#withsmarttags). |
| Resultados de pesquisa não relacionados ou parcialmente relacionados. | O comportamento da pesquisa muda com a marcação inteligente. | Entenda [como a pesquisa muda após a marcação inteligente](#withsmarttags). |
| Nenhuma sugestão de preenchimento automático para ativos. | Os ativos recém-carregados ainda não são indexados. Os metadados não estão imediatamente disponíveis como sugestões quando você começa a digitar uma palavra-chave de pesquisa na barra Omnisearch. | [!DNL Experience Manager] O aguarda até a expiração de um período de tempo limite (uma hora por padrão) antes de executar um trabalho em segundo plano para indexar os metadados de todos os ativos recém-carregados ou atualizados e, em seguida, adiciona os metadados à lista de sugestões. |
| Nenhum resultado de pesquisa. | <ul><li>Os ativos correspondentes ao seu query não existem. </li><li> Espaço em branco adicionado antes da consulta de pesquisa. </li><li> O campo de metadados não suportado contém a palavra-chave que você pesquisou.</li><li> Pesquisa feita durante o tempo de desativação de um ativo. </li></ul> | <ul><li>Pesquisar usando uma palavra-chave diferente. Como alternativa, use a marcação inteligente ou a pesquisa de semelhança para melhorar os resultados da pesquisa. </li><li>[Limitação](#limitations) conhecida.</li><li>Todos os campos de metadados não são considerados para pesquisas. Consulte [escopo](#scope).</li><li>Pesquise posteriormente ou modifique os ativos por tempo e por tempo indeterminado para os ativos necessários.</li></ul> |
| O filtro de pesquisa ou um predicado não está disponível. | <ul><li>O filtro de pesquisa não está configurado.</li><li>Não está disponível para o seu logon.</li><li>(Menos provável) As opções de pesquisa não são personalizadas na implantação que você está usando.</li></ul> | <ul><li>Entre em contato com o administrador para verificar se as personalizações de pesquisa estão ou não disponíveis.</li><li>Entre em contato com o administrador para verificar se sua conta tem privilégios/permissões para usar a personalização.</li><li>Entre em contato com o administrador e verifique as personalizações disponíveis para a implantação [!DNL Assets] que você está usando.</li></ul> |
| Ao procurar imagens visualmente semelhantes, uma imagem esperada está ausente. | <ul><li>A imagem não está disponível em [!DNL Experience Manager].</li><li>Imagem não indexada. Normalmente, quando é carregado recentemente.</li><li>A imagem não é marcada com tags inteligentes.</li></ul> | <ul><li>Adicione a imagem a [!DNL Assets].</li><li>Entre em contato com o administrador para reindexar o repositório. Além disso, verifique se você está usando o índice apropriado.</li><li>Entre em contato com o administrador para adicionar tags inteligentes aos ativos relevantes.</li></ul> |
| Ao procurar imagens visualmente semelhantes, uma imagem irrelevante é exibida. | Comportamento de pesquisa visual. | [!DNL Experience Manager] exibe o máximo possível de ativos potencialmente relevantes. Imagens menos relevantes, se houver, são adicionadas aos resultados, mas com uma classificação de pesquisa mais baixa. A qualidade das correspondências e a relevância dos ativos pesquisados diminuem à medida que você rolar para baixo os resultados da pesquisa. |
| Ao selecionar e operar em resultados de pesquisa, todos os ativos pesquisados não são operados. | A opção [!UICONTROL Selecionar Tudo] seleciona apenas os primeiros 100 resultados de pesquisa na exibição de cartão e os primeiros 200 resultados de pesquisa na exibição de lista. |  |

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] guia de implementação de pesquisa](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [Configuração avançada para aumentar os resultados da pesquisa](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [Configurar pesquisa de tradução inteligente](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

