---
title: Pesquisar aspectos.
description: Como criar, modificar e usar aspectos de pesquisa no Adobe Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 91caca39b0b6c5c0c98b58be02f518901a3d90e3
workflow-type: tm+mt
source-wordcount: '2525'
ht-degree: 18%

---


# Pesquisar aspectos {#search-facets}

Uma implantação corporativa dos ativos Adobe Experience Manager tem a capacidade de armazenar muitos ativos. Às vezes, encontrar o ativo certo pode ser árduo e demorado se você usar apenas os recursos de pesquisa genéricos do Experience Manager.

Use aspectos de pesquisa no painel Filtros para adicionar mais granularidade à sua experiência de pesquisa e tornar a funcionalidade de pesquisa mais eficiente e versátil. Os aspectos de pesquisa adicionam várias dimensões (predicados) que permitem executar pesquisas mais complexas. O painel Filtros inclui algumas facetas padrão. Você também pode adicionar aspectos de pesquisa personalizados.

Em resumo, as facetas de pesquisa permitem que você pesquise ativos de várias maneiras, em vez de em uma única ordem taxonômica pré-determinada. É possível detalhar facilmente para o nível de detalhes desejado para uma pesquisa mais focada.

Por exemplo, se você estiver procurando uma imagem, poderá escolher se deseja um bitmap ou uma imagem vetorial. Você pode reduzir ainda mais o escopo da pesquisa especificando o tipo MIME para a imagem. Da mesma forma, ao pesquisar documentos, você pode especificar o formato, por exemplo, PDF ou MS Word.

## Adicionar um predicado {#adding-a-predicate}

Os aspectos de pesquisa exibidos no painel Filtros são definidos no formulário de pesquisa subjacente usando predicados. Para exibir mais ou diferentes aspectos, adicione predicados ao formulário padrão ou use um formulário personalizado que inclua aspectos de sua escolha.

Para pesquisas de texto completo, adicione o predicado de [!UICONTROL Texto completo] ao formulário. Use o predicado Propriedade para procurar ativos que correspondam a uma única propriedade especificada. Use o predicado Opções para pesquisar ativos que correspondam a um ou mais valores para uma propriedade específica. Adicione o predicado Intervalo de datas para pesquisar ativos criados dentro de um intervalo de datas especificado.

1. Click the Experience Manager logo, and then go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. From the Search Forms page, select **[!UICONTROL Assets Admin Search Rail]**, then click **Edit** ![edit icon](assets/do-not-localize/aemassets_edit.png).

   ![Localize e selecione o painel de pesquisa do administrador de ativos](assets/assets_admin_searchrail.png)

   Localize e selecione o painel de pesquisa do administrador de ativos

   >[!NOTE]
   >
   >Para usar a funcionalidade de pesquisa de pastas do painel **de pesquisa do administrador de** ativos pré-configurado de uma versão anterior, execute estas etapas:
   >
   >1. Navegue até */conf/global/settings/dam/search/facets/assets/jcr:content/items* no CRXDE.
   >1. Exclua o nó **type** .
   >1. No caminho */libs/settings/dam/search/facets/assets/jcr:content/items*, copie os nós **asset, directory, typeor, excludepaths** e **searchtype** no caminho mencionado na etapa 1.
   >1. Salve as alterações.


1. In the Edit Search Forms page, drag a predicate from the **[!UICONTROL Select Predicate]** tab to the main pane. Por exemplo, arraste o Predicado **[!UICONTROL de propriedade]**.

   ![Pressione e mova um predicado para personalizar os filtros de pesquisa](assets/drag_predicate.png)

   *Figura: Pressione e mova um predicado para personalizar os filtros de pesquisa.*

1. Na guia Configurações, digite um rótulo de campo, um texto de espaço reservado e uma descrição para o predicado. Especifique um nome válido para a propriedade de metadados que deseja associar ao predicado.

   O rótulo do cabeçalho na guia Configurações identifica o tipo do predicado selecionado.

   ![Use a guia Configurações para fornecer as opções necessárias de um predicado](assets/settings.png)

   Use a guia Configurações para fornecer as opções necessárias de um predicado

1. No campo **[!UICONTROL Nome da propriedade]**, especifique um nome válido para a propriedade de metadados que deseja associar ao predicado. É o nome com base no qual a pesquisa é realizada. Por exemplo, insira `jcr:content/metadata/dc:description` ou `./jcr:content/metadata/dc:description`.

   Você também pode selecionar um nó existente na caixa de diálogo de seleção.

   ![Associar uma propriedade de metadados a um predicado no campo Nome da propriedade](assets/property_settings.png)

   Associar uma propriedade de metadados a um predicado no campo Nome da propriedade

1. Clique na **[!UICONTROL Pré-visualização]** da ![pré-visualização](assets/do-not-localize/preview_icon.png) para gerar uma pré-visualização do painel Filtros como ela aparece depois de adicionar o predicado.
1. Revise o layout do predicado no modo de Pré-visualização.

   ![Pré-visualização o formulário de pesquisa antes de enviar as alterações](assets/preview-1.png)

   Pré-visualização o formulário de pesquisa antes de enviar as alterações

1. Para fechar a pré-visualização, clique em **[!UICONTROL Fechar]** ![fechando](assets/do-not-localize/close.png) no canto superior direito da pré-visualização.
1. Clique em **[!UICONTROL Concluído]** para salvar as configurações.
1. Navegue até o painel Pesquisar na interface do usuário Ativos. O predicado Propriedade é adicionado ao painel.
1. Insira uma descrição para o ativo a ser pesquisado na caixa de texto. Por exemplo, digite &quot;Adobe&quot;. Quando você realiza uma pesquisa, os ativos com a descrição correspondente a &quot;Adobe&quot; são listados nos resultados da pesquisa.

## Adicionar um predicado de opções {#adding-an-options-predicate}

O predicado Opções permite que você adicione várias opções de pesquisa no painel Filtros. Você pode selecionar uma ou mais dessas opções no painel Filtros para pesquisar ativos. Por exemplo, para pesquisar ativos com base no tipo de arquivo, configure opções, como Imagens, Multimídia, Documentos e Arquivos, no formulário de pesquisa. Depois de configurar essas opções, a pesquisa será realizada em ativos do tipo GIF, JPEG, PNG e assim por diante, quando você selecionar a opção Imagens no painel Filtros.

Para mapear as opções para a respectiva propriedade, crie uma estrutura de nó para as opções e forneça o caminho do nó pai na propriedade Nome da propriedade do predicado Opções. O nó pai deve ser do tipo `sling`: `OrderedFolder`. As opções devem ser do tipo `nt:unstructured`. Os nós de opção devem ter as propriedades `jcr:title` e `value` configurados.

A `jcr:title` propriedade é um nome amigável para a opção exibida no painel Filtros. O `value` campo é usado no query para corresponder à propriedade especificada.

Quando você seleciona uma opção, a pesquisa é executada com base na `value` propriedade do nó de opção e de seus nós filhos, se houver. A árvore inteira sob o nó de opção é atravessada e a `value` propriedade de cada nó filho é combinada usando uma operação OU para formar o query de pesquisa.

Por exemplo, se você selecionar &quot;Imagens&quot; para tipos de arquivos, a consulta de pesquisa dos ativos será criada ao combinar a propriedade `value` usando uma operação OR. Por exemplo, a consulta de pesquisa de imagens é construída combinando os resultados correspondentes de *image/jpeg*, *image/gif*, *image/png*, *image/pjpeg* e *image/tiff* da propriedade `jcr:content/metadata/dc:format` usando uma operação OR.

![A propriedade value de um tipo de arquivo, como visto no CRXDE, é usada para query de pesquisa funcionarem](assets/chlimage_1-418.png)

A propriedade value de um tipo de arquivo, como visto no CRXDE, é usada para query de pesquisa funcionarem

Em vez de criar manualmente uma estrutura de nó para as opções no repositório CRXDE, você pode definir as opções em um arquivo JSON especificando pares de valores chave correspondentes. Especifique o caminho do arquivo JSON no campo **[!UICONTROL Nome da propriedade]**. Por exemplo, defina os pares de valores chave, `image/bmp`, `image/gif`, `image/jpeg` e `image/png` e especifique os valores, como mostrado no seguinte arquivo JSON de amostra. In the **[!UICONTROL Property Name]** field, you can specify the CRXDE path for this file.

```JSON
{
    "options" :
 [
          {"value" : "image/bmp","text" : "BMP"},
          {"value" : "image/gif","text" : "GIF"},
          {"value" : "image/jpeg","text" : "JPEG"},
          {"value" : "image/png","text" : "PNG"}
 ]
}
```

Se desejar usar um nó existente, especifique-o usando a caixa de diálogo de seleção.

>[!NOTE]
>
>O predicado Opções é um invólucro personalizado que inclui predicados de propriedade para demonstrar o comportamento descrito. Atualmente, não há um terminal REST disponível para suportar a funcionalidade nativamente.

1. Click the Experience Manager logo, and then go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. From the **[!UICONTROL Search Forms]** page, select **[!UICONTROL Assets Admin Search Rail]**, then click **[!UICONTROL Edit]**.
1. Na página **[!UICONTROL Editar formulário de pesquisa]**, arraste o **[!UICONTROL Predicado de opções]** da guia **[!UICONTROL Selecionar predicado]** até o painel principal.
1. Na guia **[!UICONTROL Configurações]**, digite um rótulo e um nome para a propriedade. Por exemplo, para pesquisar ativos com base no formato, especifique um nome amigável para o rótulo, por exemplo, **[!UICONTROL Tipo de arquivo]**. Especifique a propriedade com base na qual a pesquisa deve ser realizada no campo de propriedade, por exemplo `jcr:content/metadata/dc:format.`
1. Faça uma das seguintes opções:

   * In the **[!UICONTROL Property Name]** field, mention the path of the JSON file where you define the nodes for the options and specify corresponding key-value pairs.
   * Clique no `+` símbolo ao lado do campo Opções para especificar o texto e o valor de exibição para as opções que deseja fornecer no painel Filtros. Para adicionar outra opção, clique no `+` símbolo e repita a etapa.

1. Certifique-se de que **[!UICONTROL Seleção única]** esteja desmarcada para permitir que o usuário selecione várias opções para tipos de arquivos de cada vez (por exemplo, Imagens, Documentos, Multimídia e Arquivos). Se você marcar **[!UICONTROL Seleção única]**, o usuário poderá selecionar apenas uma opção para tipos de arquivo por vez.

   ![Os campos disponíveis no predicado Opções](assets/options_predicate.png)

   Os campos disponíveis no predicado Opções

1. No campo **[!UICONTROL Descrição]** , insira uma descrição opcional e clique em **[!UICONTROL Concluído]**.
1. Navegue até o painel Pesquisar. O predicado Opções é adicionado ao painel **Pesquisar** . As opções para Tipo **[!UICONTROL de]** arquivo são exibidas como caixas de seleção.

## Adicionar um predicado de propriedade de vários valores {#adding-a-multi-value-property-predicate}

O predicado Propriedade de vários valores permite pesquisar ativos por vários valores. Considere um cenário em que você tem imagens de vários produtos em Ativos e os metadados de cada imagem incluem um número SKU associado ao produto. Você pode usar esse predicado para procurar imagens de produtos com base em vários números de SKU.

1. Click the Experience Manager logo, and then go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. Na página Pesquisar formulários, selecione Painel **[!UICONTROL de pesquisa do administrador de]** ativos e clique no ícone **[!UICONTROL Editar]** ![editar](assets/do-not-localize/aemassets_edit.png).
1. Na página Editar formulário de pesquisa, arraste um **[!UICONTROL Predicado de propriedades de vários valores]** da guia **[!UICONTROL Selecionar predicado]** para o painel principal.
1. In the **[!UICONTROL Settings]** tab, enter a label and placeholder text for the predicate. Specify the property name based on which the search is to be performed in the property field, for example `jcr:content/metadata/dc:value`. Você também pode usar a caixa de diálogo de seleção para selecionar um nó.
1. Verifique se a opção **[!UICONTROL Suporte a delimitadores]** está selecionada. No campo **[!UICONTROL Delimitadores de entrada]**, especifique delimitadores para separar valores individuais. Por padrão, a vírgula é especificada como delimitador. É possível especificar um delimitador diferente.
1. No campo **Descrição** , insira uma descrição opcional e clique em **[!UICONTROL Concluído]**.
1. Navegue até o painel Filtros na interface do usuário do Assets. O predicado **[!UICONTROL Propriedade de vários valores]** é adicionado ao painel.
1. Especifique vários valores no campo Vários valores separados pelos delimitadores e execute a pesquisa. O predicado busca uma correspondência de texto exata para os valores especificados.

## Adicionar um predicado de tags {#adding-a-tags-predicate}

O predicado de tag permite que você realize pesquisas baseadas em tags para ativos. Por padrão, o Assets pesquisa ativos por uma ou mais tags correspondentes com base nas tags especificadas. Em outras palavras, o query de pesquisa executa uma operação OU usando as tags especificadas. No entanto, você pode usar a opção de correspondência de todas as tags para pesquisar ativos que incluem todas as tags especificadas.

1. Click the Experience Manager logo, and then go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. From the Search Forms page, select **[!UICONTROL Assets Admin Search Rail]** and then click **[!UICONTROL Edit]** ![edit icon](assets/do-not-localize/aemassets_edit.png).
1. In the Edit Search Form page, drag **[!UICONTROL Tags Predicate]** from the Select Predicate tab to the main pane.
1. Na guia Configurações, insira um texto de espaço reservado para o predicado. Specify the property name based on which the search is to be performed in the property field, for example *jcr:content/metadata/cq:tags*. Como alternativa, você pode selecionar um nó no CRXDE na caixa de diálogo de seleção.
1. Configure a propriedade de caminho de tags raiz desse predicado para preencher várias tags na lista Tags.
1. Selecione a opção **[!UICONTROL Mostrar correspondência de todas as tags]** para procurar ativos que incluem todas as tags especificadas.

   ![Configurações típicas do predicado Tags](assets/tags_predicate.png)

   Configurações típicas do predicado Tags

1. No campo **[!UICONTROL Descrição]** , insira uma descrição opcional e clique em **[!UICONTROL Concluído]**.
1. Navegue até o painel Pesquisar. O predicado **[!UICONTROL Tags]** é adicionado ao painel Pesquisar.
1. Especifique tags com base nas quais você deseja pesquisar ativos ou selecione na lista de sugestões.

   ![Sugestão fornecida pelo Experience Manager ao digitar o nome da tag](assets/chlimage_1-419.png)

   *Figura: Sugestão fornecida pelo Experience Manager ao digitar o nome da tag.*

1. Select **[!UICONTROL Match all]** to search for matches that include all tags that you specify.

## Adicionar outros predicados {#adding-other-predicates}

Semelhante à forma como você adiciona um predicado de Propriedade ou um predicado de Opções, você pode adicionar os seguintes predicados adicionais ao painel Pesquisar:

| Nome do Predicado | Descrição | Propriedades |
|---|---|---|
| [!UICONTROL Texto completo] | Predicado de pesquisa para executar pesquisa de texto completo em um nó de ativo inteiro. Ela é mapeada com o operador jcr:contains. Você pode especificar um caminho relativo se desejar executar uma pesquisa de texto completo em uma parte específica do nó do ativo. | <ul><li>Etiqueta</li><li>Espaço reservado</li><li>Nome da propriedade</li><li>Descrição</li></ul> |
| [!UICONTROL Navegador de caminhos] | Projetar pesquisa para procurar ativos em pastas e subpastas em um caminho raiz pré-configurado | <ul><li>Espaço reservado</li><li>Caminho raiz</li><li>Descrição</li></ul> |
| [!UICONTROL Caminho] | Use-o para filtrar os resultados no local. É possível especificar caminhos diferentes como opções. | <ul><li>Etiqueta</li><li>Caminho</li><li>Descrição</li></ul> |
| [!UICONTROL Publicar status] | Projetar pesquisa para pesquisar ativos com base em seu status de publicação | <ul><li>Etiqueta</li><li>Nome da propriedade</li><li>Descrição</li></ul> |
| [!UICONTROL Data relativa] | O predicado de pesquisa para pesquisar ativos com base na data relativa de sua criação. Por exemplo, você pode configurar opções, como 2 meses atrás, 3 semanas atrás e assim por diante. | <ul><li>Etiqueta</li><li>Nome da propriedade</li><li>Data relativa</li></ul> |
| [!UICONTROL Intervalo] | O predicado de pesquisa para pesquisar ativos que estão dentro de um intervalo especificado. No painel Pesquisar, você pode especificar valores mínimos e máximos para o intervalo. | <ul><li>Etiqueta</li><li>Nome da propriedade</li><li>Descrição</li></ul> |
| [!UICONTROL Intervalo de datas] | Projete de pesquisa para pesquisar ativos criados em um intervalo especificado para uma propriedade de data. No painel Pesquisar, é possível especificar datas de Start e término usando seletores de data. | <ul><li>Etiqueta</li><li>Espaço reservado</li><li>Nome da propriedade</li><li>Texto do intervalo (de)</li><li>Texto do intervalo (até)</li><li>Descrição</li></ul> |
| [!UICONTROL Data] | Projete de pesquisa para uma pesquisa de ativos baseada em controle deslizante com base em uma propriedade de data. | <ul><li>Etiqueta</li><li>Nome da propriedade</li><li>Descrição</li></ul> |
| [!UICONTROL Tamanho do arquivo] | Predicado de pesquisa para pesquisar ativos com base em seu tamanho. É um predicado baseado em silder no qual você seleciona as opções do controle deslizante de um nó configurável. As opções padrão são definidas em /libs/dam/options/predicates/filesize no repositório CRXDE. O tamanho do arquivo é fornecido em bytes. | <ul><li>Etiqueta</li><li>Nome da propriedade</li><li>Caminho</li><li>Descrição</li></ul> |
| [!UICONTROL Última modificação do ativo] | Projetar pesquisa para pesquisar ativos modificados recentemente | <ul><li>Nome da propriedade</li><li>Valor da propriedade</li><li>Descrição</li></ul> |
| [!UICONTROL Publicar status] | Projetar pesquisa para pesquisar ativos com base em seu status de publicação | <ul><li>Etiqueta</li><li>Nome da propriedade</li><li>Descrição</li></ul> |
| [!UICONTROL Classificação] | Projetar pesquisa para pesquisar ativos com base em sua classificação média | <ul><li>Etiqueta</li><li>Nome da propriedade</li><li>Caminho da opção</li><li>Descrição</li></ul> |
| [!UICONTROL Status da expiração] | Projetar pesquisa para pesquisar ativos com base em seu status de expiração | <ul><li>Etiqueta</li><li>Nome da propriedade</li><li>Descrição</li></ul> |
| [!UICONTROL Oculto] | predicado de pesquisa que define uma propriedade de campo oculto para procurar ativos | <ul><li>Nome da propriedade</li><li>Valor da propriedade</li><li>Descrição</li></ul> |

## Redefinir aspectos de pesquisa padrão {#restoring-default-search-facets}

Por padrão, um ícone de cadeado ícone de ![cadeado ícone](assets/do-not-localize/lock_closed_icon.svg) fechado é exibido antes do Painel **[!UICONTROL de pesquisa do administrador do]** Assets na página **[!UICONTROL Pesquisar formulários]** . O ícone de bloqueio em relação a uma opção na página Pesquisar formulários indica que as configurações padrão estão intactas e não são personalizadas. O ícone ![Bloquear ícone](assets/do-not-localize/lock_closed_icon.svg) fechado desaparece se você adicionar aspectos de pesquisa ao formulário indicando que o formulário padrão foi modificado.

![O ícone de bloqueio em relação a uma opção na página Pesquisar formulários indica que as configurações padrão estão intactas e não são personalizadas.](assets/locked_admin_rail.png)

Para restaurar o aspecto de pesquisa padrão, execute estas etapas:

1. Selecione **[!UICONTROL Assets Admin Search Rail]** na página **[!UICONTROL Pesquisar formulários]** .
1. Clique em **[!UICONTROL Excluir]** contorno ![excluído](assets/do-not-localize/deleteoutline.png) na barra de ferramentas.
1. Na caixa de diálogo de confirmação, clique em **[!UICONTROL Excluir]** para remover as alterações personalizadas.

   After you delete the custom changes to search facets, the lock icon ![lock closed icon](assets/do-not-localize/lock_closed_icon.svg) reappears before **[!UICONTROL Assets Admin Search Rail]** in the **[!UICONTROL Search Forms]** page.

## User permissions {#user-permissions}

Se você não tiver uma função de administrador atribuída, esta é uma lista de permissões necessárias para executar ações de edição, exclusão e pré-visualização envolvendo aspectos de pesquisa.

| Ação | Permissões  |
| ------------------- | ---------------------------------------------------------------- |
| [!UICONTROL Editar] | Permissões de leitura e gravação no `/apps` nó no CRXDE |
| [!UICONTROL Excluir] | Permissões de leitura, gravação e exclusão no `/apps` nó no CRXDE |
| [!UICONTROL Visualizar] | Permissões de Leitura, Gravação e Exclusão no `/var/dam/content` nó no CRXDE. Além disso, permissões de leitura e gravação no `/apps` nó. |

>[!MORELIKETHIS]
>
>* [Estender o recurso de pesquisa de ativos](searchx.md)
>* [Pesquisar ativos](search-assets.md)

