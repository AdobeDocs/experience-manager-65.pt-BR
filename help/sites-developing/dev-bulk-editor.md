---
title: Desenvolvimento do editor de itens em massa
description: A marcação permite que o conteúdo seja categorizado e organizado
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 8753aaab-959f-459b-bdb6-057cbe05d480
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 1%

---

# Desenvolvimento do editor de itens em massa{#developing-the-bulk-editor}

Esta seção descreve como desenvolver a ferramenta Editor de itens em massa e como estender o componente Lista de produtos, que é baseado no Editor de itens em massa.

## Parâmetros de consulta do editor em massa {#bulk-editor-query-parameters}

Ao trabalhar com o Editor de itens em massa, há vários parâmetros de consulta que você pode adicionar ao URL para chamar o Editor de itens em massa com uma configuração específica. Se você quiser que o Editor de itens em massa seja sempre usado com uma determinada configuração, por exemplo, como no componente Lista de produtos, edite `bulkeditor.jsp` (em /libs/wcm/core/components/bulkeditor) ou crie um componente com a configuração específica. As alterações feitas usando parâmetros de consulta não são permanentes.

Por exemplo, se você digitar o seguinte no URL do navegador:

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

O Editor de itens em massa é exibido sem a **Caminho raiz** field como hrp=true oculta o campo. Com o parâmetro hrp=false, o campo é exibido (o valor padrão).

Veja a seguir uma lista dos parâmetros de consulta do Editor de itens em massa:

>[!NOTE]
>
>Cada parâmetro pode ter um nome longo e curto. Por exemplo, o nome longo do caminho raiz de pesquisa é `rootPath`, a curta é `rp`. Se o nome longo não estiver definido, o nome curto será lido da solicitação.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p> Parâmetro</p> <p>(nome longo/nome curto)<br /> </p> </td>
   <td> Tipo <br /> </td>
   <td> Descrição <br /> </td>
  </tr>
  <tr>
   <td> rootPath/rp<br /> </td>
   <td> String </td>
   <td> caminho raiz de pesquisa</td>
  </tr>
  <tr>
   <td> queryParams / qp<br /> </td>
   <td> String</td>
   <td> pesquisar consulta</td>
  </tr>
  <tr>
   <td> contentMode/cm<br /> </td>
   <td> Booleano</td>
   <td> quando true, o modo de conteúdo é habilitado<br /> </td>
  </tr>
  <tr>
   <td> colsValue / cv<br /> </td>
   <td> String[]</td>
   <td> propriedades pesquisadas (valores marcados de colsSelection exibidos como caixas de seleção)</td>
  </tr>
  <tr>
   <td> extraCols / ec<br /> </td>
   <td> String[]</td>
   <td> propriedades adicionais pesquisadas (exibidas em um campo de texto separado por vírgulas)</td>
  </tr>
  <tr>
   <td> initialSearch / é<br /> </td>
   <td> Booleano</td>
   <td> quando verdadeiro, a consulta é executada no carregamento da página<br /> </td>
  </tr>
  <tr>
   <td> colsSelection / cs<br /> </td>
   <td> String[]</td>
   <td> seleção de propriedades pesquisadas (exibidas como caixas de seleção)</td>
  </tr>
  <tr>
   <td> showGridOnly / sgo<br /> </td>
   <td> Booleano</td>
   <td> quando verdadeiro, mostra somente a grade e não o painel de pesquisa <br /> </td>
  </tr>
  <tr>
   <td> searchPanelCollapsed/spc</td>
   <td> Booleano</td>
   <td> quando verdadeiro, o painel de pesquisa é recolhido ao carregar</td>
  </tr>
  <tr>
   <td> hideRootPath / hrp</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o campo de caminho raiz</td>
  </tr>
  <tr>
   <td> hideQueryParams / hqp</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o campo de consulta</td>
  </tr>
  <tr>
   <td> hideContentMode / hcm</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o campo de modo de conteúdo</td>
  </tr>
  <tr>
   <td> hideColsSelection / hcs</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o campo de seleção de colunas</td>
  </tr>
  <tr>
   <td> hideExtraCols / hec</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o campo de colunas extra</td>
  </tr>
  <tr>
   <td> hideSearchButton</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o botão de pesquisa</td>
  </tr>
  <tr>
   <td> hideSaveButton / hsavep</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o botão salvar</td>
  </tr>
  <tr>
   <td> hideExportButton / hexpb</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o botão exportar</td>
  </tr>
  <tr>
   <td> hideImportButton / hib</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o botão importar</td>
  </tr>
  <tr>
   <td> hideResultNumber / hrn</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o texto do número do resultado da pesquisa da grade</td>
  </tr>
  <tr>
   <td> hideInsertButton / hinsertb</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o botão de inserção de grade</td>
  </tr>
  <tr>
   <td> hideDeleteButton / hdelb</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o botão excluir da grade</td>
  </tr>
  <tr>
   <td> hidePathCol / hpc</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta a coluna "path" da grade</td>
  </tr>
 </tbody>
</table>

### Desenvolvimento de um componente baseado no Editor de itens em massa: o componente de Lista de produtos {#developing-a-bulk-editor-based-component-the-product-list-component}

Esta seção fornece uma visão geral de como usar o Editor de itens em massa e fornece uma descrição do componente Geometrixx existente com base no Editor de itens em massa: o componente Lista de produtos.

O componente Lista de produtos permite que os usuários exibam e editem uma tabela de dados. Por exemplo, você pode usar o componente Lista de produtos para representar produtos em um catálogo. As informações são apresentadas em uma tabela de HTML padrão e qualquer edição é executada no **Editar** que contém um dispositivo BulkEditor. (Este Editor de itens em massa é o mesmo que o acessível em /etc/importers/bulkeditor.html ou através do menu Ferramentas). O componente Lista de produtos foi configurado para funcionalidade específica e limitada do Editor de itens em massa. Cada parte do Editor de itens em massa (ou componentes derivados do Editor de itens em massa) pode ser configurada.

Com o Editor de itens em massa, você pode adicionar, modificar, excluir, filtrar e exportar as linhas, salvar modificações e importar um conjunto de linhas. Cada linha é armazenada como um nó na própria instância do componente Lista de produtos. Cada célula é uma propriedade de cada nó. Essa é uma opção de design e pode ser facilmente alterada. Por exemplo, você pode armazenar nós em outro lugar no repositório. A função do servlet de consulta é retornar a lista dos nós a serem exibidos; o caminho de pesquisa é definido como uma instância da Lista de produtos.

O código-fonte do componente Lista de produtos está disponível no repositório em /apps/geometrixx/components/productlist e é composto por várias partes, como todos os componentes do Adobe Experience Manager (AEM):

* Renderização de HTML: a renderização é feita em um arquivo JSP (/apps/geometrixx/components/productlist/productlist.jsp). O JSP lê os subnós do componente Lista de produtos atual e exibe cada um deles como uma linha de uma tabela HTML.
* Caixa de diálogo de edição, que é onde você define a configuração do Editor de itens em massa. Configure a caixa de diálogo para corresponder às necessidades do componente: colunas disponíveis e possíveis ações executadas na grade ou na pesquisa. Consulte [Propriedades de configuração do Editor de itens em massa](#bulk-editor-configuration-properties) para obter informações sobre todas as propriedades de configuração.

Aqui está uma representação XML dos subnós do diálogo:

```xml
        <editor
            jcr:primaryType="cq:Widget"
            colsSelection="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            colsValue="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            contentMode="false"
            exportURL="/etc/importers/bulkeditor/export.tsv"
            extraCols="Selection"
            hideColsSelection="false"
            hideContentMode="true"
            hideDeleteButton="false"
            hideExportButton="false"
            hideExtraCols="true"
            hideImportButton="false"
            hideInsertButton="false"
            hideMoveButtons="false"
            hidePathCol="true"
            hideRootPath="true"
            hideSaveButton="false"
            hideSearchButton="false"
            importURL="/etc/importers/bulkeditor/import"
            initialSearch="true"
            insertedResourceType="geometrixx/components/productlist/sku"
            queryParams=""
            queryURL="/etc/importers/bulkeditor/query.json"
            saveURL="/etc/importers/bulkeditor/save"
            xtype="bulkeditor">
            <saveButton
                jcr:primaryType="nt:unstructured"
                text="Save modifications"/>
            <searchButton
                jcr:primaryType="nt:unstructured"
                text="Apply filter"/>
            <queryParamsInput
                jcr:primaryType="nt:unstructured"
                fieldDescription="Enter here your filters"
                fieldLabel="Filters"/>
            <searchPanel
                jcr:primaryType="nt:unstructured"
                height="200">
                <defaults
                    jcr:primaryType="nt:unstructured"
                    labelWidth="150"/>
            </searchPanel>
            <grid
                jcr:primaryType="nt:unstructured"
                height="275"/>
            <store jcr:primaryType="nt:unstructured">
                <sortInfo
                    jcr:primaryType="nt:unstructured"
                    direction="ASC"
                    field="CatalogCode"/>
            </store>
            <colModel
                jcr:primaryType="nt:unstructured"
                width="150"/>
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
        </editor>
```

### Propriedades de configuração do editor de itens em massa {#bulk-editor-configuration-properties}

Cada parte do Editor de itens em massa pode ser configurada. A tabela a seguir lista todas as propriedades de configuração do Editor de itens em massa.

<table>
 <tbody>
  <tr>
   <td>Nome da propriedade</td>
   <td>Definição</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>Pesquisar caminho raiz</td>
  </tr>
  <tr>
   <td>queryParams</td>
   <td>Pesquisar consulta</td>
  </tr>
  <tr>
   <td>contentMode</td>
   <td>Verdadeiro para ativar o modo de conteúdo: as propriedades são lidas no nó jcr:content e não no nó de resultado de pesquisa</td>
  </tr>
  <tr>
   <td>colsValue</td>
   <td>Propriedades pesquisadas (valores marcados de colsSelection exibidos como caixas de seleção)</td>
  </tr>
  <tr>
   <td>extraCols</td>
   <td>Propriedades pesquisadas extras (exibidas em um campo de texto separado por vírgulas)</td>
  </tr>
  <tr>
   <td>initialSearch</td>
   <td>Verdadeiro para executar a consulta no carregamento da página</td>
  </tr>
  <tr>
   <td>colsSelection</td>
   <td>Seleção de propriedades pesquisadas (exibidas como caixas de seleção)</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>Verdadeiro para mostrar apenas a grade e não o painel de pesquisa (não se esqueça de definir initialSearch como verdadeiro)</td>
  </tr>
  <tr>
   <td>searchPanelCollapsed</td>
   <td>Verdadeiro para recolher o painel de pesquisa por padrão</td>
  </tr>
  <tr>
   <td>hideRootPath</td>
   <td>Ocultar campo de caminho raiz</td>
  </tr>
  <tr>
   <td>hideQueryParams</td>
   <td>Ocultar campo de consulta</td>
  </tr>
  <tr>
   <td>hideContentMode</td>
   <td>Ocultar campo de modo de conteúdo</td>
  </tr>
  <tr>
   <td>ocultarColsSelection</td>
   <td>Ocultar campo de seleção de colunas</td>
  </tr>
  <tr>
   <td>hideExtraCols</td>
   <td>Ocultar campo cols extra</td>
  </tr>
  <tr>
   <td>hideSearchButton</td>
   <td>Ocultar botão de pesquisa</td>
  </tr>
  <tr>
   <td>hideSaveButton</td>
   <td>Ocultar botão Salvar</td>
  </tr>
  <tr>
   <td>hideExportButton</td>
   <td>Ocultar botão de exportação</td>
  </tr>
  <tr>
   <td>hideImportButton</td>
   <td>Ocultar botão de importação</td>
  </tr>
  <tr>
   <td>hideResultNumber</td>
   <td>Ocultar texto do número do resultado de pesquisa da grade</td>
  </tr>
  <tr>
   <td>hideInsertButton</td>
   <td>Ocultar botão de inserção de grade</td>
  </tr>
  <tr>
   <td>hideDeleteButton</td>
   <td>Ocultar o botão de exclusão da grade</td>
  </tr>
  <tr>
   <td>hidePathCol</td>
   <td>Ocultar a coluna "caminho" da grade</td>
  </tr>
  <tr>
   <td>queryURL</td>
   <td>Caminho para o servlet de consulta</td>
  </tr>
  <tr>
   <td>exportURL</td>
   <td>Caminho para exportar servlet</td>
  </tr>
  <tr>
   <td>importURL</td>
   <td>Caminho para importar servlet</td>
  </tr>
  <tr>
   <td>insertedResourceType</td>
   <td>Tipo de recurso adicionado ao nó quando uma linha é introduzida</td>
  </tr>
  <tr>
   <td>saveButton</td>
   <td>Salvar configuração do widget de botão</td>
  </tr>
  <tr>
   <td>searchButton</td>
   <td>Pesquisar configuração do widget de botão</td>
  </tr>
  <tr>
   <td>exportButton</td>
   <td>Exportar configuração do widget de botão</td>
  </tr>
  <tr>
   <td>importButton</td>
   <td>Importar configuração do widget de botão</td>
  </tr>
  <tr>
   <td>searchPanel</td>
   <td>Configuração do widget do painel de pesquisa</td>
  </tr>
  <tr>
   <td>grade</td>
   <td>Configuração do widget de grade</td>
  </tr>
  <tr>
   <td>loja</td>
   <td>Armazenar configuração</td>
  </tr>
  <tr>
   <td>colModel</td>
   <td>Configuração do modelo de coluna de grade</td>
  </tr>
  <tr>
   <td>rootPathInput</td>
   <td>configuração do widget rootPath</td>
  </tr>
  <tr>
   <td>queryParamsInput</td>
   <td>configuração do widget queryParams</td>
  </tr>
  <tr>
   <td>contentModeInput</td>
   <td>configuração do widget contentMode</td>
  </tr>
  <tr>
   <td>colsSelectionInput</td>
   <td>configuração do widget colsSelection</td>
  </tr>
  <tr>
   <td>extraColsInput</td>
   <td>configuração do widget extraCols</td>
  </tr>
  <tr>
   <td>colsMetadata</td>
   <td>Configuração de metadados da coluna. As possíveis propriedades são (aplicadas a todas as células da coluna): <br />
    <ul>
     <li>cellStyle: html style </li>
     <li>cellCls: classe css </li>
     <li>readOnly: verdadeiro para não poder alterar o valor </li>
     <li>caixa de seleção: true para definir todas as células da coluna como caixas de seleção (valores true/false) </li>
     <li>forcedPosition: valor inteiro para especificar onde a coluna deve ser colocada na grade (entre 0 e o número de colunas-1)<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Configuração de metadados de colunas {#columns-metadata-configuration}

Você pode configurar para cada coluna:

* propriedades de exibição: estilo html, classe CSS e somente leitura

* uma caixa de seleção
* uma posição forçada

Colunas CSS e somente leitura

O Editor de itens em massa tem três configurações de coluna:

* Nome da classe CSS da célula (cellCls): um nome de classe CSS que é adicionado a cada célula da coluna configurada.
* Estilo da célula (cellStyle): um estilo de HTML que é adicionado a cada célula da coluna configurada.
* Somente leitura (readOnly): somente leitura é definido para cada célula da coluna configurada.

A configuração deve ser definida como a seguinte:

```
"colsMetadata": {
"Column name": {
     "cellStyle": "html style",
     "cellCls": "CSS class",
     "readOnly": true/false
}
}
```

O exemplo a seguir pode ser encontrado no componente da lista de produtos (/apps/geometrixx/components/productlist/dialog/items/editor/colsMetadata):

```xml
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
```

**Caixa de seleção**

Se a propriedade de configuração da caixa de seleção estiver definida como verdadeira, todas as células da coluna serão renderizadas como caixas de seleção. Uma caixa de seleção envia **true** ao servidor Salvar servlet, **false** caso contrário. No menu de cabeçalho, você também pode **selecionar tudo** ou **selecionar nenhum**. Essas opções serão ativadas se o cabeçalho selecionado for o cabeçalho de uma coluna de caixa de seleção.

No exemplo anterior, a coluna de seleção contém apenas caixas de seleção como checkbox=&quot;true&quot;.

**Posição forçada**

Os metadados de posição forçada forcedPosition permitem especificar onde a coluna é colocada na grade: 0 é o primeiro lugar e &lt;number of=&quot;&quot; columns=&quot;&quot;>-1 é a última posição. Qualquer outro valor é ignorado.

No exemplo anterior, a coluna de seleção é a primeira coluna como forcedPosition=&quot;0&quot;.

### Query Servlet {#query-servlet}

Por padrão, o servlet Query pode ser encontrado em `/libs/wcm/core/components/bulkeditor/json.java`. Você pode configurar outro caminho para recuperar os dados.

O servlet Query funciona da seguinte maneira: ele recebe uma consulta GQL e as colunas a serem retornadas, calcula os resultados e os envia de volta para o Editor de itens em massa como um fluxo JSON.

No caso do componente Lista de produtos, os dois parâmetros enviados para o servlet de consulta são os seguintes:

* query: &quot;path:/content/geometrixx/en/customers/jcr:content/par/productlist Cube&quot;
* cols: &quot;Selection,ProductId,ProductName,Color,CatalogCode,SellingSku&quot;

E o fluxo JSON é retornado da seguinte maneira:

```
{
  "hits": [{
      "jcr:path": "/content/geometrixx/en/products/jcr:content/par/productlist/1258674828905",
      "ProductId": "21",
      "ProductName": "Cube",
      "Color": "Blue",
      "CatalogCode": "43244",
      "SellingSku": "32131"
    }
  ],
  "results": 1
}
```

Cada ocorrência corresponde a um nó e suas propriedades e é exibida como uma linha na grade.

Você pode estender o servlet Query para retornar um modelo de herança complexo ou retornar nós armazenados em um local lógico específico. O servlet Query pode ser usado para fazer qualquer tipo de computação complexa. A grade pode exibir linhas que são uma agregação de vários nós no repositório. A modificação e o salvamento dessas linhas devem, nesse caso, ser gerenciados pelo Servlet de gravação.

### Salvar servlet {#save-servlet}

Na configuração padrão do Editor de itens em massa, cada linha é um nó e o caminho desse nó é armazenado no registro de linhas. O Editor de itens em massa mantém o link entre a linha e o nó pelo caminho jcr. Quando um usuário edita a grade, uma lista de todas as modificações é criada. Quando um usuário clica em **Salvar**, uma consulta POST é enviada para cada caminho com os valores de propriedades atualizados. Essa é a base do conceito Sling e funciona bem se cada célula for uma propriedade do nó. Mas se o servlet Query estiver implementado para fazer o cálculo de herança, esse modelo não poderá funcionar como uma propriedade retornada pelo servlet Query que pode ser herdada de outro nó.

O conceito de servlet Salvar é que as modificações não são publicadas diretamente em cada nó, mas são publicadas em um servlet que realiza o trabalho de gravação. Isso dá a esse servlet a possibilidade de analisar as modificações e salvar as propriedades no nó direito.

Cada propriedade atualizada é enviada para o servlet no seguinte formato:

* Nome do parâmetro: &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>

  Exemplo: /content/geometrixx/en/products/jcr:content/par/productlist/1258674859000/SellingSku

* Valor: &lt;value>

  Exemplo: 12123

O servlet precisa saber onde a propriedade catalogCode está armazenada.

Uma implementação padrão para Salvar servlet está disponível em /libs/wcm/bulkeditor/save/POST.jsp e é usada no componente Lista de produtos. São necessários todos os parâmetros da solicitação (com um &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;> format) e grava as propriedades nos nós usando a API JCR. Também cria nó se eles não existirem (linhas inseridas na grade).

Não use o código padrão como está, pois ele reimplementa o que o servidor faz nativamente (um POST em &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>) e, portanto, é apenas um bom ponto de partida para criar um servlet Save que possa gerenciar um modelo de herança de propriedade.
