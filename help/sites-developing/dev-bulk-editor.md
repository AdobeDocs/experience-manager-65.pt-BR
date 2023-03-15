---
title: Desenvolvimento do editor em massa
seo-title: Developing the Bulk Editor
description: A marcação permite que o conteúdo seja categorizado e organizado
seo-description: Tagging allows content to be categorized and organized
uuid: 3cd04c52-5bdb-47f6-9fa3-d7a4937e8e20
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e9a1ff95-e88e-41f0-9731-9a59159b4653
exl-id: 8753aaab-959f-459b-bdb6-057cbe05d480
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1837'
ht-degree: 2%

---

# Desenvolvimento do editor em massa{#developing-the-bulk-editor}

Esta seção descreve como desenvolver a ferramenta de editor em massa e como estender o componente Lista de produtos, que é baseado no editor em massa.

## Parâmetros de consulta do editor em massa {#bulk-editor-query-parameters}

Ao trabalhar com o editor em massa, há vários parâmetros de consulta que você pode adicionar ao URL para chamar o editor em massa com uma configuração específica. Se você quiser que o editor em massa seja sempre usado com uma determinada configuração, por exemplo, como no componente Lista de produtos , será necessário modificar bulkeditor.jsp (localizado em /libs/wcm/core/components/bulkeditor) ou criar um componente com a configuração específica. As alterações feitas usando parâmetros de consulta não são permanentes.

Por exemplo, se você digitar o seguinte no URL do navegador:

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

o editor em massa é exibido sem o **Caminho raiz** o campo como hrp=true oculta o campo. Com o parâmetro hrp=false, o campo é exibido (o valor padrão).

Veja a seguir uma lista dos parâmetros de consulta do editor em massa:

>[!NOTE]
>
>Cada parâmetro pode ter um nome longo e curto. Por exemplo, o nome longo do caminho raiz de pesquisa é `rootPath`, a abreviatura é `rp`. Se o nome longo não estiver definido, o curto será lido da solicitação.

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
   <td> rootPath / rp<br /> </td>
   <td> Sequência de caracteres </td>
   <td> caminho raiz de pesquisa</td>
  </tr>
  <tr>
   <td> queryParams / qp<br /> </td>
   <td> Sequência de caracteres</td>
   <td> consulta de pesquisa</td>
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
   <td> quando true, a consulta é executada no carregamento da página<br /> </td>
  </tr>
  <tr>
   <td> colsSelection / cs<br /> </td>
   <td> Sequência de caracteres[]</td>
   <td> seleção de propriedades pesquisadas (exibida como caixas de seleção)</td>
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
   <td> hideExtraCols / HI</td>
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
   <td> quando verdadeiro, oculta o botão de inserção de grade</td>
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

### Desenvolvimento de um componente baseado no editor em massa: o componente Lista de produtos {#developing-a-bulk-editor-based-component-the-product-list-component}

Esta seção fornece uma visão geral de como usar o editor em massa e fornece uma descrição do componente existente do Geometrixx com base no editor em massa: o componente Lista de produtos .

O componente Lista de produtos permite que os usuários exibam e editem uma tabela de dados. Por exemplo, você pode usar o componente Lista de produtos para representar produtos em um catálogo. As informações são apresentadas em uma tabela de HTML padrão e qualquer edição é executada na variável **Editar** , que contém um widget BulkEditor. (Esse editor em massa é exatamente o mesmo que o acessível em /etc/importers/bulkeditor.html ou pelo menu Ferramentas ). O componente Lista de produtos foi configurado para funcionalidade específica e limitada do editor em massa. Toda parte do editor em massa (ou componentes derivados do editor em massa) pode ser configurada.

Com o editor em massa, é possível adicionar, modificar, excluir, filtrar e exportar as linhas, salvar modificações e importar um conjunto de linhas. Cada linha é armazenada como um nó na própria instância do componente Lista de produtos . Cada célula é uma propriedade de cada nó. Essa é uma opção de design e pode ser facilmente alterada, por exemplo, você pode armazenar nós em outro lugar no repositório. A função do servlet de consulta é retornar a lista dos nós a serem exibidos; o caminho de pesquisa é definido como uma instância da Lista de produtos.

O código-fonte do componente Lista de produtos está disponível no repositório em /apps/geometrixx/components/productlist e é composto por várias partes, como todos os componentes do AEM:

* Renderização de HTML: a renderização é feita em um arquivo JSP (/apps/geometrixx/components/productlist/productlist.jsp). O JSP lê os subnós do componente Lista de produtos atual e exibe cada um deles como uma linha de uma tabela de HTML.
* Caixa de diálogo Editar, que é onde você define a configuração do Editor em massa. Configure a caixa de diálogo para atender às necessidades do componente: colunas disponíveis e possíveis ações executadas na grade ou na pesquisa. Consulte [propriedades de configuração do editor em massa](#bulk-editor-configuration-properties) para obter informações sobre todas as propriedades de configuração.

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

### Propriedades de configuração do editor em massa {#bulk-editor-configuration-properties}

Todas as partes do editor em massa podem ser configuradas. A tabela a seguir lista todas as propriedades de configuração do editor em massa.

<table>
 <tbody>
  <tr>
   <td>Nome da propriedade</td>
   <td>Definição</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>Caminho raiz de pesquisa</td>
  </tr>
  <tr>
   <td>queryParams</td>
   <td>Pesquisar consulta</td>
  </tr>
  <tr>
   <td>contentMode</td>
   <td>Verdadeiro para ativar o modo de conteúdo: as propriedades são lidas no nó jcr:content e não no nó do resultado da pesquisa</td>
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
   <td>Verdadeiro para executar consulta no carregamento da página</td>
  </tr>
  <tr>
   <td>colsSelection</td>
   <td>Seleção de propriedades pesquisadas (exibida como caixas de seleção)</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>Verdadeiro para mostrar apenas a grade e não o painel de pesquisa (não se esqueça de definir initialSearch como true)</td>
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
   <td>Campo Ocultar modo de conteúdo</td>
  </tr>
  <tr>
   <td>hideColsSelection</td>
   <td>Ocultar campo de seleção de colunas</td>
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
   <td>Botão Ocultar exportação</td>
  </tr>
  <tr>
   <td>hideImportButton</td>
   <td>Botão Ocultar importação</td>
  </tr>
  <tr>
   <td>hideResultNumber</td>
   <td>Ocultar texto do número do resultado da pesquisa em grade</td>
  </tr>
  <tr>
   <td>hideInsertButton</td>
   <td>Ocultar botão de inserção de grade</td>
  </tr>
  <tr>
   <td>hideDeleteButton</td>
   <td>Botão Ocultar exclusão de grade</td>
  </tr>
  <tr>
   <td>hidePathCol</td>
   <td>Ocultar coluna de "caminho" da grade</td>
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
   <td>Configuração do widget de botão Importar</td>
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
   <td>Configuração do modelo da coluna de grade</td>
  </tr>
  <tr>
   <td>rootPathInput</td>
   <td>configuração do widget rootPath</td>
  </tr>
  <tr>
   <td>queryParamsInput</td>
   <td>Configuração do widget queryParams</td>
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
   <td>Configuração do widget extraCols</td>
  </tr>
  <tr>
   <td>colsMetadata</td>
   <td>Configuração dos metadados da coluna. As possíveis propriedades são (aplicadas a todas as células da coluna): <br />
    <ul>
     <li>cellStyle: estilo html </li>
     <li>cellCls: classe css </li>
     <li>readOnly: true para não poder alterar o valor </li>
     <li>caixa de seleção: true para definir todas as células da coluna como caixas de seleção (valores true/false) </li>
     <li>forcedPosition: valor inteiro para especificar onde a coluna deve ser colocada na grade (entre 0 e número de colunas-1)<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Configuração de metadados de colunas {#columns-metadata-configuration}

É possível configurar para cada coluna:

* propriedades de exibição: estilo html, classe CSS e somente leitura

* uma caixa de seleção
* uma posição forçada

Colunas CSS e somente leitura

O editor em massa tem três configurações de coluna:

* Nome da classe CSS da Célula (cellCls): um nome de classe CSS adicionado a cada célula da coluna configurada.
* Estilo da célula (cellStyle): um estilo HTML adicionado a cada célula da coluna configurada.
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

Se a propriedade de configuração da caixa de seleção estiver definida como true, todas as células da coluna serão renderizadas como caixas de seleção. Uma caixa marcada envia **true** para o servlet Save do servidor, **false** caso contrário. No menu de cabeçalho, também é possível **selecionar tudo** ou **selecionar nenhum**. Essas opções serão ativadas se o cabeçalho selecionado for o cabeçalho de uma coluna de caixa de seleção.

No exemplo anterior, a coluna de seleção contém apenas caixas de seleção como caixa de seleção=&quot;true&quot;.

**Posição forçada**

Os metadados de posição forçada forcedPosition permitem especificar onde a coluna é colocada na grade: 0 é o primeiro lugar e &lt;number of=&quot;&quot; columns=&quot;&quot;>-1 é a última posição. Qualquer outro valor será ignorado.

No exemplo anterior, a coluna de seleção é a primeira coluna como forcedPosition=&quot;0&quot;.

### Servlet de consulta {#query-servlet}

Por padrão, o servlet Query pode ser encontrado em `/libs/wcm/core/components/bulkeditor/json.java`. Você pode configurar outro caminho para recuperar os dados.

O servlet Query funciona da seguinte maneira: recebe uma consulta GQL e as colunas a serem retornadas, calcula os resultados e envia os resultados para o editor em massa como um fluxo JSON.

No caso do componente Lista de produtos , os dois parâmetros enviados para o servlet Consulta são os seguintes:

* query: &quot;path:/content/geometrixx/en/customers/jcr:content/par/productlist Cube&quot;
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

Cada ocorrência corresponde a um nó e suas propriedades, e é exibida como uma linha na grade.

Você pode estender o servlet Query para retornar um modelo de herança complexo ou nós de retorno armazenados em um local lógico específico. O servlet Query pode ser usado para fazer qualquer tipo de computação complexa. A grade pode então exibir linhas que são uma agregação de vários nós no repositório. A modificação e o salvamento dessas linhas devem, nesse caso, ser gerenciadas pelo Servlet Salvar.

### Salvar servlet {#save-servlet}

Na configuração padrão do editor em massa, cada linha é um nó e o caminho desse nó é armazenado no registro de linha. O editor em massa mantém o link entre a linha e o nó pelo caminho jcr. Quando um usuário edita a grade, uma lista de todas as modificações é criada. Quando um usuário clica em **Salvar**, uma consulta POST é enviada para cada caminho com os valores de propriedades atualizados. Essa é a base do conceito do Sling e funciona bem se cada célula for uma propriedade do nó. Mas se o servlet Query estiver implementado para fazer o cálculo de herança, esse modelo não poderá funcionar como uma propriedade retornada pelo servlet Query pode ser herdada de outro nó.

O conceito de servlet Save é que as modificações não são publicadas diretamente em cada nó, mas são publicadas em um servlet que faz o trabalho de salvamento. Isso dá a esse servlet a possibilidade de analisar as modificações e salvar as propriedades no nó direito.

Cada propriedade atualizada é enviada para o servlet no seguinte formato:

* Nome do parâmetro: &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>

   Exemplo: /content/geometrixx/en/products/jcr:content/par/productlist/1258674859000/SellingSku

* Valor: &lt;value>

   Exemplo: 12123

O servlet precisa saber onde a propriedade catalogCode é armazenada.

Uma implementação padrão Salvar servlet está disponível em /libs/wcm/bulkeditor/save/POST.jsp e é usada no componente Lista de produtos . Leva todos os parâmetros da solicitação (com um &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;> ) e grava propriedades em nós usando a API JCR. Ele também cria um nó se eles não existirem (linhas inseridas na grade).

O código padrão não deve ser usado como está, pois reimplementa o que o servidor faz nativamente (um POST on &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>) e, portanto, é apenas um bom ponto de partida para criar um servlet Save que gerenciará um modelo de herança de propriedade.
