---
title: Pesquisar aspectos para filtrar os resultados da pesquisa
description: Como criar, modificar e usar aspectos de pesquisa no [!DNL Adobe Experience Manager].
contentOwner: AG
role: Admin, Developer
feature: Search
exl-id: acaf46e6-ff70-4825-8922-ce8f82905a92
hide: true
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2416'
ht-degree: 18%

---

# Pesquisar aspectos {#search-facets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/search-facets.html?lang=en) |
| AEM 6.5 | Este artigo |

Uma implantação corporativa de [!DNL Adobe Experience Manager Assets] O tem a capacidade de armazenar muitos ativos. Às vezes, encontrar o ativo certo pode ser árduo e demorado se você usar apenas os recursos de pesquisa genéricos do [!DNL Experience Manager].

Use os aspectos de pesquisa no painel Filtros para adicionar mais granularidade à sua experiência de pesquisa e tornar a funcionalidade de pesquisa mais eficiente e versátil. Os aspectos de pesquisa adicionam várias dimensões (predicados) que permitem realizar pesquisas mais complexas. O painel Filtros inclui algumas facetas padrão. Você também pode adicionar aspectos de pesquisa personalizados.

Em resumo, os aspectos de pesquisa permitem pesquisar ativos de várias maneiras, em vez de em uma única ordem taxonômica predeterminada. Você pode facilmente detalhar o nível desejado de detalhes para uma pesquisa mais focada.

Por exemplo, se estiver procurando uma imagem, você pode escolher se deseja uma imagem de bitmap ou de vetor. É possível reduzir ainda mais o escopo da pesquisa especificando o tipo MIME da imagem. Da mesma forma, ao pesquisar documentos, você pode especificar o formato, por exemplo, PDF ou MS Word.

## Adicionar um predicado {#adding-a-predicate}

Os aspectos de pesquisa exibidos no painel Filtros são definidos no formulário de pesquisa subjacente usando predicados. Para exibir mais facetas ou diferentes, adicione predicados ao formulário padrão ou use um formulário personalizado que inclua facetas de sua escolha.

Para pesquisas de texto completo, adicione o **[!UICONTROL Texto completo]** para o formulário. Use o predicado Propriedade para pesquisar ativos que correspondem a uma única propriedade especificada. Use o predicado Opções para pesquisar ativos que correspondem a um ou mais valores de uma propriedade específica. Adicione o predicado Intervalo de datas para pesquisar ativos criados em um intervalo de datas especificado.

1. Clique em [!DNL Experience Manager] e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Pesquisar no Forms]**.
1. No [!UICONTROL Pesquisar no Forms] selecione **[!UICONTROL Trilho de pesquisa do administrador de ativos]** e, em seguida, clique em **[!UICONTROL Editar]** ![ícone editar](assets/do-not-localize/aemassets_edit.png).

   >[!NOTE]
   >
   >Para usar a funcionalidade de pesquisa de pasta do pré-configurado [!DNL Assets] Trilho de pesquisa do administrador de uma versão anterior, execute estas etapas:
   >
   >1. Navegue até `/conf/global/settings/dam/search/facets/assets/jcr:content/items` no CRXDE.
   >1. Exclua o `type` nó.
   >1. Do caminho `/libs/settings/dam/search/facets/assets/jcr:content/items`, copiar os nós `asset`, `directory`, `typeor`, `excludepaths`, e `searchtype` ao caminho mencionado na etapa 1.
   >1. Salve as alterações.

1. No [!UICONTROL Editar Forms de pesquisa] arraste um predicado da caixa de diálogo **[!UICONTROL Selecionar predicado]** para o painel principal. Por exemplo, arrastar **[!UICONTROL Predicado da propriedade]**.

   ![Selecionar e mover um predicado para personalizar os filtros de pesquisa](assets/drag_predicate.png)

   *Figura: selecione e mova um predicado para personalizar os filtros de pesquisa.*

1. No [!UICONTROL Configurações] insira um rótulo de campo, um texto de espaço reservado e uma descrição para o predicado. Especifique um nome válido para a propriedade de metadados que deseja associar ao predicado. O rótulo do cabeçalho na variável [!UICONTROL Configurações] A guia identifica o tipo do predicado selecionado.

1. No campo [!UICONTROL Nome da propriedade], especifique um nome válido para a propriedade de metadados que deseja associar ao predicado. É o nome com base no qual a pesquisa é realizada. Por exemplo, insira `jcr:content/metadata/dc:description` ou `./jcr:content/metadata/dc:description`.

   Você também pode selecionar um nó existente na caixa de diálogo de seleção.

   ![Associar uma propriedade de metadados a um predicado no campo Nome da propriedade](assets/property_settings.png)

   Associar uma propriedade de metadados a um predicado no campo Nome da propriedade

1. Clique em **[!UICONTROL Visualizar]** ![pré-visualização](assets/do-not-localize/preview_icon.png) para gerar uma pré-visualização do painel Filtros como ele aparece após a adição do predicado.
1. Revise o layout do predicado no modo Visualizar.

   ![Pré-visualizar o formulário de pesquisa antes de enviar as alterações](assets/preview-1.png)

   Pré-visualizar o formulário de pesquisa antes de enviar as alterações

1. Para fechar a visualização, clique no link **[!UICONTROL Fechar]** ![fechar](assets/do-not-localize/close.png) no canto superior direito da visualização.
1. Clique em **[!UICONTROL Concluído]** para salvar as configurações.
1. Navegue até o painel Pesquisa na [!DNL Assets] interface do usuário. O predicado Propriedade é adicionado ao painel.
1. Insira uma descrição para o ativo a ser pesquisado na caixa de texto. Por exemplo, insira `Adobe`. Ao realizar uma pesquisa, os ativos com correspondência de descrição `Adobe` são listados nos resultados da pesquisa.

## Adicionar um predicado de Opções {#adding-an-options-predicate}

O predicado Opções permite adicionar várias opções de pesquisa no painel Filtros. É possível selecionar uma ou mais dessas opções no painel Filtros para procurar ativos. Por exemplo, para pesquisar ativos com base no tipo de arquivo, configure opções como Imagens, Multimídia, Documentos e Arquivos no formulário de pesquisa. Após configurar essas opções, a pesquisa é executada em ativos do tipo GIF, JPEG, PNG e assim por diante, ao selecionar a opção Imagens no painel Filtros.

Para mapear as opções para a respectiva propriedade, crie uma estrutura de nó para as opções e forneça o caminho do nó principal na propriedade Nome da propriedade do predicado Opções. O nó principal deve ser do tipo `sling`: `OrderedFolder`. As opções devem ser do tipo `nt:unstructured`. Os nós de opção devem ter as propriedades `jcr:title` e `value` configurado.

A variável `jcr:title` propriedade é um nome amigável para a opção que é exibida no painel Filtros. A variável `value` é usado na consulta para corresponder à propriedade especificada.

Quando você seleciona uma opção, a pesquisa é executada com base no `value` propriedade do nó da opção e seus nós filhos, se houver. A árvore inteira sob o nó de opção é percorrida e a variável `value` A propriedade de cada nó secundário é combinada usando uma operação OR para formar a consulta de pesquisa.

Por exemplo, se você selecionar &quot;Imagens&quot; para tipos de arquivos, a consulta de pesquisa dos ativos será criada ao combinar a propriedade `value` usando uma operação OR. Por exemplo, a consulta de pesquisa de imagens é construída combinando os resultados correspondentes de *image/jpeg*, *image/gif*, *image/png*, *image/pjpeg* e *image/tiff* da propriedade `jcr:content/metadata/dc:format` usando uma operação OR.

![A propriedade Value de um tipo de arquivo, como visto no CRXDE, é usada para consultas de pesquisa funcionarem](assets/filetype-value-property.png)

A propriedade Value de um tipo de arquivo, como visto no CRXDE, é usada para consultas de pesquisa funcionarem

Em vez de criar manualmente uma estrutura de nó para as opções no repositório CRXDE, defina as opções em um arquivo JSON especificando pares de valores chave correspondentes. Especifique o caminho do arquivo JSON no campo **[!UICONTROL Nome da propriedade]**. Por exemplo, defina os pares de valores chave, `image/bmp`, `image/gif`, `image/jpeg` e `image/png` e especifique os valores, como mostrado no seguinte arquivo JSON de amostra. No **[!UICONTROL Nome da propriedade]** , você pode especificar o caminho CRXDE desse arquivo.

```json
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

Se quiser usar um nó existente, especifique-o usando a caixa de diálogo de seleção.

>[!NOTE]
>
>O predicado Opções é um invólucro personalizado que inclui predicados de propriedade para demonstrar o comportamento descrito. Atualmente, não há nenhum endpoint REST disponível para oferecer suporte à funcionalidade nativamente.

1. Clique em [!DNL Experience Manager] e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Pesquisar no Forms]**.
1. No **[!UICONTROL Pesquisar no Forms]** selecione **[!UICONTROL Trilho de pesquisa do administrador de ativos]** e, em seguida, clique em **[!UICONTROL Editar]**.
1. Na página **[!UICONTROL Editar formulário de pesquisa]**, arraste o **[!UICONTROL Predicado de opções]** da guia **[!UICONTROL Selecionar predicado]** até o painel principal.
1. Na guia **[!UICONTROL Configurações]**, digite um rótulo e um nome para a propriedade. Por exemplo, para pesquisar ativos com base no formato, especifique um nome amigável para o rótulo, por exemplo, **[!UICONTROL Tipo de arquivo]**. Especifique a propriedade com base na qual a pesquisa deve ser realizada no campo de propriedade, por exemplo `jcr:content/metadata/dc:format.`
1. Siga uma das seguintes opções:

   * No **[!UICONTROL Nome da propriedade]** mencione o caminho do arquivo JSON onde você define os nós das opções e especifica os pares de valores chave correspondentes.
   * Clique em `+` símbolo ao lado do campo Opções para especificar o texto e o valor de exibição das opções que você deseja fornecer no painel Filtros. Para adicionar outra opção, clique em `+` e repita a etapa.

1. Certifique-se de que **[!UICONTROL Seleção única]** esteja desmarcada para permitir que o usuário selecione várias opções para tipos de arquivos de cada vez (por exemplo, Imagens, Documentos, Multimídia e Arquivos). Se você marcar **[!UICONTROL Seleção única]**, o usuário poderá selecionar apenas uma opção para tipos de arquivo por vez.

   ![Os campos disponíveis no predicado Opções](assets/options_predicate.png)

   Os campos disponíveis no predicado Opções

1. No **[!UICONTROL Descrição]** insira uma descrição opcional e clique em **[!UICONTROL Concluído]**.
1. Navegue até o painel Pesquisa. O predicado Opções é adicionado à variável **Pesquisar** painel. As opções para **[!UICONTROL Tipo de arquivo]** são exibidos como caixas de seleção.

## Adicionar um predicado de propriedade de vários valores {#adding-a-multi-value-property-predicate}

O predicado Propriedade de vários valores permite pesquisar ativos para vários valores. Considere um cenário em que você tem imagens de vários produtos no [!DNL Assets] e os metadados de cada imagem incluem um número SKU associado ao produto. Você pode usar esse predicado para pesquisar imagens de produtos com base em vários números SKU.

1. Clique em [!DNL Experience Manager] e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Pesquisar no Forms]**.
1. Na página Pesquisar Forms, selecione **[!UICONTROL Trilho de pesquisa do administrador de ativos]**, clique em **[!UICONTROL Editar]** ![ícone editar](assets/do-not-localize/aemassets_edit.png).
1. Na página Editar formulário de pesquisa, arraste um **[!UICONTROL Predicado de propriedades de vários valores]** da guia **[!UICONTROL Selecionar predicado]** para o painel principal.
1. No **[!UICONTROL Configurações]** insira um rótulo e um texto de espaço reservado para o predicado. Especifique o nome da propriedade com base na qual a pesquisa deve ser realizada no campo de propriedade, por exemplo `jcr:content/metadata/dc:value`. Você também pode usar a caixa de diálogo de seleção para selecionar um nó.
1. Verifique se a opção **[!UICONTROL Suporte a delimitadores]** está selecionada. No campo **[!UICONTROL Delimitadores de entrada]**, especifique delimitadores para separar valores individuais. Por padrão, a vírgula é especificada como delimitador. É possível especificar um delimitador diferente.
1. No **Descrição** insira uma descrição opcional e clique em **[!UICONTROL Concluído]**.
1. Navegue até o painel Filtros na [!DNL Assets] interface do usuário. O predicado **[!UICONTROL Propriedade de vários valores]** é adicionado ao painel.
1. Especifique vários valores no campo Vários valores separados pelos delimitadores e execute a pesquisa. O predicado busca uma correspondência exata de texto para os valores especificados.

## Adicionar um predicado de tags {#adding-a-tags-predicate}

O predicado Tag permite realizar pesquisas por ativos com base em tags. Por padrão, [!DNL Assets] O pesquisa ativos para uma ou mais correspondências de tags com base nas tags especificadas. Em outras palavras, a consulta de pesquisa executa uma operação OR usando as tags especificadas. No entanto, você pode usar a opção Corresponder todas as tags para procurar ativos que incluem todas as tags especificadas.

1. Clique em [!DNL Experience Manager] e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Pesquisar no Forms]**.
1. Na página Pesquisar Forms, selecione **[!UICONTROL Trilho de pesquisa do administrador de ativos]** e clique em **[!UICONTROL Editar]** ![ícone editar](assets/do-not-localize/aemassets_edit.png).
1. Na página Editar formulário de pesquisa, arraste **[!UICONTROL Predicado de tags]** na guia Selecionar predicado até o painel principal.
1. Na guia Configurações, insira um texto de espaço reservado para o predicado. Especifique o nome da propriedade com base na qual a pesquisa deve ser realizada no campo de propriedade, por exemplo *jcr:content/metadata/cq:tags*. Como alternativa, você pode selecionar um nó no CRXDE na caixa de diálogo de seleção.
1. Configure a propriedade Root tags path desse predicado para preencher várias tags na lista Tags.
1. Selecione a opção **[!UICONTROL Mostrar correspondência de todas as tags]** para procurar ativos que incluem todas as tags especificadas.

1. No **[!UICONTROL Descrição]** insira uma descrição opcional e clique em **[!UICONTROL Concluído]**.
1. Navegue até o painel Pesquisa. A variável **[!UICONTROL Tags]** O predicado é adicionado ao painel Pesquisar.
1. Especifique as tags com base nas quais deseja pesquisar ativos ou selecione na lista de sugestões.

1. Selecionar **[!UICONTROL Corresponder a todos]** para procurar correspondências que incluem todas as tags especificadas.

## Adicionar outros predicados {#adding-other-predicates}

Semelhante à maneira como você adiciona um predicado de Propriedade ou um predicado de Opções, é possível adicionar os seguintes predicados adicionais ao painel Pesquisar:

| Nome do predicado | Descrição | Propriedades |
|---|---|---|
| [!UICONTROL Texto completo] | Pesquisar predicado para executar uma pesquisa de texto completo em um nó de ativo inteiro. Ele é mapeado com o operador jcr:contains. Você pode especificar um caminho relativo se quiser executar uma pesquisa de texto completo em uma parte específica do nó do ativo. | <ul><li>Etiqueta</li><li>Espaço reservado</li><li>Nome da propriedade</li><li>Descrição</li></ul> |
| [!UICONTROL Navegador de caminhos] | Pesquisar predicado para pesquisar ativos em pastas e subpastas em um caminho raiz pré-configurado | <ul><li>Espaço reservado</li><li>Caminho raiz</li><li>Descrição</li></ul> |
| [!UICONTROL Caminho] | Use-a para filtrar os resultados no local. Você pode especificar caminhos diferentes como opções. | <ul><li>Etiqueta</li><li>Caminho</li><li>Descrição</li></ul> |
| [!UICONTROL Publicar status] | Pesquisar predicado para pesquisar ativos com base no status de publicação | <ul><li>Etiqueta</li><li>Nome da propriedade</li><li>Descrição</li></ul> |
| [!UICONTROL Data relativa] | Predicado de pesquisa para pesquisar ativos com base na data relativa de sua criação. Por exemplo, você pode configurar opções, como 2 meses atrás, 3 semanas atrás e assim por diante. | <ul><li>Etiqueta</li><li>Nome da propriedade</li><li>Data relativa</li></ul> |
| [!UICONTROL Intervalo] | Pesquisar predicado para pesquisar ativos dentro de um intervalo especificado. No painel Pesquisar, é possível especificar valores mínimos e máximos para o intervalo. | <ul><li>Etiqueta</li><li>Nome da propriedade</li><li>Descrição</li></ul> |
| [!UICONTROL Intervalo de datas] | Pesquisar predicado para pesquisar ativos criados em um intervalo especificado para uma propriedade de data. No painel Pesquisar, é possível especificar datas de Início e Término usando seletores de datas. | <ul><li>Etiqueta</li><li>Espaço reservado</li><li>Nome da propriedade</li><li>Texto do intervalo (de)</li><li>Texto do intervalo (até)</li><li>Descrição</li></ul> |
| [!UICONTROL Data] | Pesquisar predicado para uma pesquisa com base em controle deslizante de ativos com base em uma propriedade de data. | <ul><li>Etiqueta</li><li>Nome da propriedade</li><li>Descrição</li></ul> |
| [!UICONTROL Tamanho do arquivo] | Pesquisar predicado para pesquisar ativos com base em seu tamanho. É um predicado baseado em controle deslizante no qual você seleciona as opções de controle deslizante de um nó configurável. As opções padrão são definidas em /libs/dam/options/predicates/filesize no repositório CRXDE. O tamanho do arquivo é fornecido em bytes. | <ul><li>Etiqueta</li><li>Nome da propriedade</li><li>Caminho</li><li>Descrição</li></ul> |
| [!UICONTROL Última modificação do ativo] | Pesquisar predicado para pesquisar ativos modificados recentemente | <ul><li>Nome da propriedade</li><li>Valor da propriedade</li><li>Descrição</li></ul> |
| [!UICONTROL Publicar status] | Pesquisar predicado para pesquisar ativos com base no status de publicação | <ul><li>Etiqueta</li><li>Nome da propriedade</li><li>Descrição</li></ul> |
| [!UICONTROL Avaliação] | Pesquisar predicado para pesquisar ativos com base em sua classificação média | <ul><li>Etiqueta</li><li>Nome da propriedade</li><li>Caminho de opção</li><li>Descrição</li></ul> |
| [!UICONTROL Status da expiração] | Pesquisar predicado para pesquisar ativos com base no status de expiração | <ul><li>Etiqueta</li><li>Nome da propriedade</li><li>Descrição</li></ul> |
| [!UICONTROL Oculto] | Pesquisar predicado que define uma propriedade de campo oculta para pesquisar ativos | <ul><li>Nome da propriedade</li><li>Valor da propriedade</li><li>Descrição</li></ul> |

## Redefinir aspectos de pesquisa padrão {#restoring-default-search-facets}

Por padrão, um ícone de bloqueio ![ícone bloquear fechado](assets/do-not-localize/lock_closed_icon.svg) aparece antes de **[!UICONTROL Trilho de pesquisa do administrador de ativos]** no **[!UICONTROL Pesquisar no Forms]** página. O ícone de Bloqueio em relação a uma opção na página Pesquisar Forms indica que as configurações padrão estão intactas e não são personalizadas. O ícone ![ícone bloquear fechado](assets/do-not-localize/lock_closed_icon.svg) desaparecerá se você adicionar aspectos de pesquisa ao formulário, indicando que o formulário padrão foi modificado.

![Ícone Bloquear](assets/locked_admin_rail.png)

Para restaurar o aspecto de pesquisa padrão, execute estas etapas:

1. Selecionar **[!UICONTROL Trilho de pesquisa do administrador de ativos]** no **[!UICONTROL Pesquisar no Forms]** página.
1. Clique em **[!UICONTROL Excluir]** ![deleteoutline](assets/do-not-localize/deleteoutline.png) na barra de ferramentas.
1. Na caixa de diálogo de confirmação, clique em **[!UICONTROL Excluir]** para remover as alterações personalizadas.

   Depois de excluir as alterações personalizadas nos aspectos de pesquisa, o ícone de bloqueio ![ícone bloquear fechado](assets/do-not-localize/lock_closed_icon.svg) reaparece antes de **[!UICONTROL Trilho de pesquisa do administrador de ativos]** no **[!UICONTROL Pesquisar no Forms]** página.

## Permissões de usuário {#user-permissions}

Se você não recebeu uma função de administrador, esta é uma lista de permissões necessárias para executar ações de edição, exclusão e visualização envolvendo aspectos de pesquisa.

| Ação | Permissões |
| ------------------- | ---------------------------------------------------------------- |
| [!UICONTROL Editar] | Permissões de Leitura e Gravação no `/apps` nó no CRXDE |
| [!UICONTROL Excluir] | Permissões de Leitura, Gravação e Exclusão no `/apps` nó no CRXDE |
| [!UICONTROL Visualização] | Permissões de Leitura, Gravação e Exclusão no `/var/dam/content` no CRXDE. Além disso, as permissões de Leitura e Gravação em `/apps` nó. |

>[!MORELIKETHIS]
>
>* [Estender o recurso de pesquisa de ativos](searchx.md)
>* [Pesquisar ativos](search-assets.md)
