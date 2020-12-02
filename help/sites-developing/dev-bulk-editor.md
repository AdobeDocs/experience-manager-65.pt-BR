---
title: Desenvolver o Editor em massa
seo-title: Desenvolver o Editor em massa
description: A marcação permite que o conteúdo seja categorizado e organizado
seo-description: A marcação permite que o conteúdo seja categorizado e organizado
uuid: 3cd04c52-5bdb-47f6-9fa3-d7a4937e8e20
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e9a1ff95-e88e-41f0-9731-9a59159b4653
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1849'
ht-degree: 1%

---


# Desenvolver o Editor de itens em massa{#developing-the-bulk-editor}

Esta seção descreve como desenvolver a ferramenta de editor em massa e como estender o componente de Lista do Produto, que é baseado no editor em massa.

## Parâmetros de Query do Editor em Massa {#bulk-editor-query-parameters}

Ao trabalhar com o editor em massa, há vários parâmetros de query que podem ser adicionados ao URL para chamar o editor em massa com uma configuração específica. Se você quiser que o editor em massa seja sempre usado com uma determinada configuração, por exemplo, como no componente de Lista do produto, é necessário modificar bulkeditor.jsp (localizado em /libs/wcm/core/components/bulkeditor) ou criar um componente com a configuração específica. As alterações feitas usando parâmetros de query não são permanentes.

Por exemplo, se você digitar o seguinte no URL do seu navegador:

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

o editor em massa é exibido sem o campo **Caminho raiz** como hrp=true oculta o campo. Com o parâmetro hrp=false, o campo é exibido (o valor padrão).

Veja a seguir uma lista dos parâmetros de query do editor em massa:

>[!NOTE]
>
>Cada parâmetro pode ter um nome longo e curto. Por exemplo, o nome longo do caminho raiz de pesquisa é `rootPath`, o nome abreviado é `rp`. Se o nome longo não estiver definido, o curto será lido da solicitação.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p> Parâmetro</p> <p>(nome longo / nome abreviado)<br /> </p> </td>
   <td> Tipo <br /> </td>
   <td> Descrição <br /> </td>
  </tr>
  <tr>
   <td> rootPath / rp<br /> </td>
   <td> Sequência de caracteres </td>
   <td> caminho raiz de pesquisa</td>
  </tr>
  <tr>
   <td> queryParams / qp<br /> </td>
   <td> Sequência de caracteres</td>
   <td> query de pesquisa</td>
  </tr>
  <tr>
   <td> contentMode / cm<br /> </td>
   <td> Booleano</td>
   <td> quando verdadeiro, o modo de conteúdo é ativado<br /> </td>
  </tr>
  <tr>
   <td> colsValue / cv<br /> </td>
   <td> Sequência de caracteres[]</td>
   <td> propriedades pesquisadas (valores marcados de colsSelection exibidos como caixas de seleção)</td>
  </tr>
  <tr>
   <td> extraCols / ec<br /> </td>
   <td> Sequência de caracteres[]</td>
   <td> propriedades pesquisadas extras (exibidas em um campo de texto separado por vírgulas)</td>
  </tr>
  <tr>
   <td> initialSearch / is<br /> </td>
   <td> Booleano</td>
   <td> quando verdadeiro, o query é executado no carregamento da página<br /> </td>
  </tr>
  <tr>
   <td> colsSelection / cs<br /> </td>
   <td> Sequência de caracteres[]</td>
   <td> seleção de propriedades pesquisadas (exibido como caixas de seleção)</td>
  </tr>
  <tr>
   <td> showGridOnly / sgo<br /> </td>
   <td> Booleano</td>
   <td> quando verdadeiro, mostra somente a grade e não o painel de pesquisa <br /> </td>
  </tr>
  <tr>
   <td> searchPanelCollapsed / spc</td>
   <td> Booleano</td>
   <td> quando verdadeiro, o painel de pesquisa é recolhido ao carregar</td>
  </tr>
  <tr>
   <td> hideRootPath / hrp</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o campo do caminho raiz</td>
  </tr>
  <tr>
   <td> hideQueryParams / hqp</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o campo query</td>
  </tr>
  <tr>
   <td> hideContentMode / hcm</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o campo do modo de conteúdo</td>
  </tr>
  <tr>
   <td> hideColsSelection / hcs</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o campo de seleção de colunas</td>
  </tr>
  <tr>
   <td> hideExtraCols / i</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o campo de colunas extras</td>
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
   <td> quando verdadeiro, oculta o texto do número do resultado da pesquisa de grade</td>
  </tr>
  <tr>
   <td> hideInsertButton / hinsertb</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o botão de inserção da grade</td>
  </tr>
  <tr>
   <td> hideDeleteButton / hdelb</td>
   <td> Booleano</td>
   <td> quando verdadeiro, oculta o botão de exclusão de grade</td>
  </tr>
  <tr>
   <td> hidePathCol / hpc</td>
   <td> Booleano</td>
   <td> quando true, oculta a coluna "caminho" da grade</td>
  </tr>
 </tbody>
</table>

### Desenvolvimento de um componente baseado no Editor em massa: o componente de Lista do produto {#developing-a-bulk-editor-based-component-the-product-list-component}

Esta seção fornece uma visão geral de como usar o editor em massa e fornece uma descrição do componente de Geometrixx existente com base no editor em massa: o componente Lista do produto.

O componente Lista do produto permite que os usuários exibam e editem uma tabela de dados. Por exemplo, você pode usar o componente Lista do produto para representar produtos em um catálogo. As informações são apresentadas em uma tabela HTML padrão e qualquer edição é realizada na caixa de diálogo **Editar**, que contém um widget do BulkEditor. (Esse Editor em massa é exatamente o mesmo que aquele que pode ser acessado em /etc/importers/bulkeditor.html ou pelo menu Ferramentas). O componente Lista do produto foi configurado para a funcionalidade específica e limitada do editor em massa. Todas as partes do editor em massa (ou componentes derivados do editor em massa) podem ser configuradas.

Com o editor em massa, você pode adicionar, modificar, excluir, filtrar e exportar as linhas, salvar modificações e importar um conjunto de linhas. Cada linha é armazenada como um nó na própria instância do componente Lista do Produto. Cada célula é uma propriedade de cada nó. Esta é uma opção de design e pode ser facilmente alterada, por exemplo, você pode armazenar nós em outro lugar no repositório. A função do servlet do query é retornar a lista dos nós para exibição; o caminho de pesquisa é definido como uma instância de Lista do Produto.

O código-fonte do componente Lista do produto está disponível no repositório em /apps/geometrixx/components/productlist e é composto de várias partes, como todos os componentes AEM:

* Renderização HTML: a renderização é feita em um arquivo JSP (/apps/geometrixx/components/productlist/productlist.jsp). O JSP lê os subnós do componente Lista do produto atual e exibe cada um deles como uma linha de uma tabela HTML.
* Caixa de diálogo Editar, que é onde você define a configuração do Editor em massa. Configure a caixa de diálogo para corresponder às necessidades do componente: colunas disponíveis e ações possíveis executadas na grade ou na pesquisa. Consulte [propriedades de configuração do editor em massa](#bulk-editor-configuration-properties) para obter informações sobre todas as propriedades de configuração.

Esta é uma representação XML dos subnós da caixa de diálogo:

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

### Propriedades de Configuração do Editor em Massa {#bulk-editor-configuration-properties}

Todas as partes do editor em massa podem ser configuradas. A tabela a seguir lista todas as propriedades de configuração do editor em massa.

<table>
 <tbody>
  <tr>
   <td>Nome da propriedade</td>
   <td>Definição</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>Caminho raiz da pesquisa</td>
  </tr>
  <tr>
   <td>queryParams</td>
   <td>Pesquisar consulta</td>
  </tr>
  <tr>
   <td>contentMode</td>
   <td>Verdadeiro para ativar o modo de conteúdo: as propriedades são lidas em jcr:nó de conteúdo e não no nó de resultado da pesquisa</td>
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
   <td>Verdadeiro para executar query no carregamento da página</td>
  </tr>
  <tr>
   <td>colsSelection</td>
   <td>Seleção de propriedades pesquisadas (exibida como caixas de seleção)</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>True para mostrar somente a grade e não o painel de pesquisa (não se esqueça de definir initialSearch como true)</td>
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
   <td>Ocultar campo query</td>
  </tr>
  <tr>
   <td>hideContentMode</td>
   <td>Ocultar campo de modo de conteúdo</td>
  </tr>
  <tr>
   <td>hideColsSelection</td>
   <td>Ocultar campo de seleção de cores</td>
  </tr>
  <tr>
   <td>hideExtraCols</td>
   <td>Ocultar campo de cores extras</td>
  </tr>
  <tr>
   <td>hideSearchButton</td>
   <td>Ocultar botão de pesquisa</td>
  </tr>
  <tr>
   <td>hideSaveButton</td>
   <td>Botão Ocultar salvar</td>
  </tr>
  <tr>
   <td>hideExportButton</td>
   <td>Ocultar botão exportar</td>
  </tr>
  <tr>
   <td>hideImportButton</td>
   <td>Botão Ocultar importação</td>
  </tr>
  <tr>
   <td>hideResultNumber</td>
   <td>Ocultar texto do número de resultado da pesquisa em grade</td>
  </tr>
  <tr>
   <td>hideInsertButton</td>
   <td>Ocultar botão de inserção da grade</td>
  </tr>
  <tr>
   <td>hideDeleteButton</td>
   <td>Botão Ocultar exclusão de grade</td>
  </tr>
  <tr>
   <td>hidePathCol</td>
   <td>Ocultar coluna "caminho" da grade</td>
  </tr>
  <tr>
   <td>queryURL</td>
   <td>Caminho para o servlet de query</td>
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
   <td>insertResourceType</td>
   <td>Tipo de recurso adicionado ao nó quando uma linha é inserida</td>
  </tr>
  <tr>
   <td>saveButton</td>
   <td>Salvar configuração do widget de botão</td>
  </tr>
  <tr>
   <td>searchButton</td>
   <td>Configuração do widget de botão de pesquisa</td>
  </tr>
  <tr>
   <td>exportButton</td>
   <td>Configuração do widget de botão Exportar</td>
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
   <td>Configuração da loja</td>
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
     <li>cellStyle: estilo html </li>
     <li>cellCls: classe css </li>
     <li>readOnly: true para não ser capaz de alterar o valor </li>
     <li>caixa de seleção: true para definir todas as células da coluna como caixas de seleção (valores true/false) </li>
     <li>forcedPosition: valor inteiro para especificar onde a coluna deve ser colocada na grade (entre 0 e número de colunas-1)<p><br /> </p> </li>
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

O editor em massa tem três configurações de coluna:

* Nome da classe Cell CSS (cellCls): um nome de classe CSS que é adicionado a cada célula da coluna configurada.
* Estilo da célula (cellStyle): um estilo HTML que é adicionado a cada célula da coluna configurada.
* Somente leitura (somente leitura): somente leitura está definida para cada célula da coluna configurada.

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

Se a propriedade de configuração da caixa de seleção estiver definida como true, todas as células da coluna serão renderizadas como caixas de seleção. Uma caixa marcada envia **true** para o servidor Salvar servlet, caso contrário, **false**. No menu de cabeçalho, você também pode **selecionar tudo** ou **selecionar nenhum**. Essas opções serão ativadas se o cabeçalho selecionado for o cabeçalho de uma coluna de caixa de seleção.

No exemplo anterior, a coluna de seleção contém apenas caixas de seleção como caixa de seleção=&quot;true&quot;.

**Posição forçada**

Os metadados de posição forçada forcedPosition permitem especificar onde a coluna é colocada na grade: 0 é o primeiro lugar e &lt;número de colunas>-1 é a última posição. Qualquer outro valor é ignorado.

No exemplo anterior, a coluna de seleção é a primeira coluna como forcedPosition=&quot;0&quot;.

### Servlet de query {#query-servlet}

Por padrão, o servlet de Query pode ser encontrado em `/libs/wcm/core/components/bulkeditor/json.java`. Você pode configurar outro caminho para recuperar os dados.

O servlet do Query funciona da seguinte maneira: ele recebe um query GQL e as colunas a serem retornadas, calcula os resultados e envia os resultados de volta ao editor em massa como um fluxo JSON.

No caso do componente Lista do produto, os dois parâmetros enviados para o servlet do Query são os seguintes:

* query: &quot;path:/content/geometrixx/en/customers/jcr:content/par/productlist Cubo&quot;
* cols: &quot;Selection,ProductId,ProductName,Color,CatalogCode,SellingSku&quot;

e o fluxo JSON retornado é o seguinte:

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

Você pode estender o servlet Query para retornar um modelo de herança complexo ou nós de retorno armazenados em um local lógico específico. O servlet do Query pode ser usado para fazer qualquer tipo de computação complexa. A grade pode então exibir linhas que são uma agregação de vários nós no repositório. A modificação e o salvamento dessas linhas devem, nesse caso, ser gerenciados pelo Servlet Salvar.

### Salvar Servlet {#save-servlet}

Na configuração padrão do editor em massa, cada linha é um nó e o caminho desse nó é armazenado no registro de linha. O editor em massa mantém o link entre a linha e o nó pelo caminho jcr. Quando um usuário edita a grade, uma lista de todas as modificações é criada. Quando um usuário clica em **Salvar**, um query POST é enviado para cada caminho com os valores de propriedades atualizados. Esta é a base do conceito Sling e funciona bem se cada célula for uma propriedade do nó. Mas se o servlet do Query for implementado para fazer a computação de herança, esse modelo não poderá funcionar como uma propriedade retornada pelo servlet do Query poderá ser herdada de outro nó.

O conceito Salvar servlet é que as modificações não são publicadas diretamente em cada nó, mas são publicadas em um servlet que faz a tarefa de salvar. Isso dá a este servlet a possibilidade de analisar as modificações e salvar as propriedades no nó direito.

Cada propriedade atualizada é enviada para o servlet no seguinte formato:

* Nome do parâmetro: &lt;caminho jcr>/&lt;nome da propriedade>

   Exemplo: /content/geometrixx/en/products/jcr:content/par/productlist/1258674859000/SellingSku

* Valor: &lt;valor>

   Exemplo: 12123

O servlet precisa saber onde a propriedade CatalogCode é armazenada.

Uma implementação padrão do servlet Save está disponível em /libs/wcm/bulkeditor/save/POST.jsp e é usada no componente Lista do produto. Ele pega todos os parâmetros da solicitação (com um formato &lt;jcr path>/&lt;property name>) e grava propriedades em nós usando a API JCR. Ele também cria nó se eles não existirem (linhas inseridas na grade).

O código padrão não deve ser usado como está, pois reimplementa o que o servidor faz nativamente (um POST no &lt;caminho do jcr>/&lt;nome da propriedade>) e, portanto, é apenas um bom ponto de partida para a criação de um servlet Save que gerenciará um modelo de herança de propriedade.
