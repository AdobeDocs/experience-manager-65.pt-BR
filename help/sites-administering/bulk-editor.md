---
title: O Editor em massa
seo-title: O Editor em massa
description: Saiba como usar o Editor de itens em massa.
seo-description: Saiba como usar o Editor de itens em massa.
uuid: 5f5e4190-d9b2-40a6-8cf4-4b7aebe35ad3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3649cffb-418a-4ad6-862f-56346a831b0b
docset: aem65
translation-type: tm+mt
source-git-commit: 743512254850698a32fd77151e2278dd8cc4ce7d
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 1%

---


# O Editor em Massa{#the-bulk-editor}

O Editor de itens em massa permite uma edição muito eficiente quando o contexto visual da página não é necessário, pois permite:

* procurar (e exibir) conteúdo de várias páginas; isso é feito usando o GQL (Google Query Language)
* editar este conteúdo diretamente no editor em massa
* salvar as alterações (nas páginas de origem)
* exportar este conteúdo para um arquivo de planilha (.tsv) separado por tabulação

>[!NOTE]
>
>Você também pode importar conteúdo para o repositório, mas por padrão isso é desativado para o Editor de itens em massa, conforme disponível no console **Ferramentas**.

Esta seção descreve como trabalhar com o editor em massa no console **Ferramentas**. Normalmente, os administradores usam o editor em massa para pesquisar e editar vários itens. Isso é feito preenchendo a tabela usando um query GQL e selecionando os itens de conteúdo nos quais trabalhar. Os autores geralmente usam o editor em massa como parte de um aplicativo editor em massa personalizado acessível por meio do componente [listagem de produtos](/help/sites-authoring/default-components.md#productlist).

>[!CAUTION]
>
>Com a substituição [da interface clássica](/help/release-notes/deprecated-removed-features.md) no AEM 6.4, o Editor de itens em massa também foi substituído e, portanto, o Adobe não planeja aprimorar ainda mais o Editor de itens em massa.

## Exemplo de caso de uso para o Editor em massa {#example-use-case-for-the-bulk-editor}

Por exemplo, se você precisar de todos os nomes e endereços de email dos usuários que preencheram uma pesquisa específica, o Editor de itens em massa poderá fornecer essas informações e exportá-las para uma planilha.

Um exemplo para ilustrar esse caso de uso está incluído no site do Geometrixx:

1. Navegue até a página **Suporte** e, em seguida, até a pesquisa **Satisfação do Serviço de Atendimento ao Cliente**.
1. **** Edite o  **Start de** Formparágrafo. Na caixa de diálogo, clique na guia **Avançado**, expanda **Configuração de Ação** e, em seguida, clique em **Dados de Visualização...**.

   ![](assets/custsatsurvey.png)

1. O Editor em massa é totalmente personalizável. Embora neste exemplo o editor em massa não permita que os usuários editem o conteúdo, apenas permite que eles exportem as informações para uma planilha.

   ![](assets/bulkeditor.png)

## Como usar o Editor em massa {#how-to-use-the-bulk-editor}

O editor em massa permite:

* [pesquise por conteúdo com base nos parâmetros do query, para exibir as propriedades especificadas dos resultados em colunas, para editar esse conteúdo e salvar as alterações](#searching-and-editing-content)
* [para exportar esse conteúdo para uma planilha separada por tabulações](#exporting-content)

* [para importar conteúdo de uma planilha separada por tabulação](#importing-content)

### Como pesquisar e editar conteúdo {#searching-and-editing-content}

Para usar o editor em massa para editar vários itens simultaneamente:

1. No console **Ferramentas**, clique na pasta **Importadores** para expandi-la.
1. Clique com o duplo no **Editor em massa** para abri-lo.
1. Informe seus requisitos de seleção:

<table>
 <tbody>
  <tr>
   <td>Texto</td>
   <td>Propriedade</td>
  </tr>
  <tr>
   <td>Caminho raiz</td>
   <td>Indica o caminho raiz que o editor em massa pesquisa.<br /> Por exemplo, <code>/content/geometrixx/en</code>. O editor em massa pesquisa por todos os nós secundários.</td>
  </tr>
  <tr>
   <td>Parâmetros de consulta </td>
   <td>Usando parâmetros de GQL, digite a string de pesquisa que deseja que o editor em massa procure no repositório; por exemplo, <code>type:Page</code> procura por todas as páginas no caminho raiz, <code>text:professional</code> procura por todas as páginas que têm a palavra "profissional" nelas e <code>"jcr:title":English</code> procura por todas as páginas que têm "inglês" como título. Você só pode pesquisar por strings.</td>
  </tr>
  <tr>
   <td>Caixa de seleção Modo de conteúdo</td>
   <td>Marque essa caixa de seleção para ler as propriedades no subnó <code>jcr:content</code> dos resultados da pesquisa, se houver. Use apenas para páginas. Os nomes de propriedades recebem o prefixo <code>"jcr:content/"</code></td>
  </tr>
  <tr>
   <td>Propriedades / Colunas</td>
   <td>Marque as caixas de seleção para as propriedades que você deseja que o editor em massa volte. As propriedades selecionadas são os cabeçalhos de coluna no painel de resultados. Por padrão, o caminho do nó é exibido nos resultados.</td>
  </tr>
  <tr>
   <td>Propriedades / Colunas personalizadas</td>
   <td>Insira quaisquer outras propriedades que não estejam listadas no campo <strong>Propriedades/Colunas</strong>. Essas propriedades personalizadas aparecem no painel de resultados. É possível adicionar várias propriedades usando uma vírgula para separar as propriedades. <i>Observação: </i> se você adicionar uma propriedade personalizada que ainda não existe, AEM WCM exibirá uma célula vazia. Quando você modifica a célula vazia e a salva, a propriedade é adicionada ao nó. A propriedade recém-criada deve respeitar as restrições de tipo de nó e as namespaces de propriedade.</td>
  </tr>
 </tbody>
</table>

Por exemplo:

![](assets/searchfilter.png)

1. Clique em **Pesquisar**. O Editor em massa exibe os resultados.
Para o exemplo acima, todas as páginas que atendem aos seus critérios de pesquisa são retornadas e exibidas com as colunas solicitadas.

   ![](assets/chlimage_1-39.png)

1. Faça as alterações necessárias clicando no duplo em uma célula.

   ![](assets/srchresultedit.png)

1. Clique em **Salvar** para salvar suas alterações (o botão **Salvar** será ativado depois que você editar uma célula).

   >[!CAUTION]
   >
   >As alterações feitas aqui são gravadas no conteúdo do repositório; por exemplo, a página referenciada em **Path**.

#### Parâmetros de Query GQL adicionais {#additional-gql-query-parameters}

* **caminho:** somente nós de pesquisa abaixo desse caminho. Se você especificar mais de um termo com um prefixo de caminho, somente o último será considerado.
* **type:** apenas os nós de retorno dos tipos de nó especificados. Isso inclui tipos primários e de mixagem. Você pode especificar vários tipos de nós separados por vírgulas. O GQL retornará nós de qualquer um dos tipos especificados.
* **order:** ordenar o resultado pelas propriedades especificadas. Você pode especificar vários nomes de propriedade separados por vírgula. Para ordenar o resultado em ordem decrescente, basta prefixar o nome da propriedade com um sinal de menos. Por exemplo: order:-name. O uso de um sinal de mais retornará o resultado em ordem crescente, que também é o padrão.
* **limite:** limita o número de resultados usando um intervalo. Por exemplo: limit:10.20 Observe que o intervalo é baseado em zero, o start é inclusivo e o fim é exclusivo. Você também pode especificar um intervalo aberto:limit:10. ou limite:..20 Se os pontos forem omitidos e apenas um valor for especificado, o GQL retornará no máximo esse número de resultados. Por exemplo, limite:10 (retornará os primeiros 10 resultados)

### Exportar conteúdo {#exporting-content}

Talvez seja necessário exportar o conteúdo e alterá-lo em uma planilha do Excel. Por exemplo, você pode exportar uma lista de correspondência e alterar o código de área de todos os números de telefone listados diretamente no Excel, adicionar outras linhas e assim por diante.

Para exportar conteúdo:

1. Procure o conteúdo conforme descrito em [Como pesquisar e editar conteúdo](#searching-and-editing-content).
1. Clique em **Exportar** para exportar as alterações para uma planilha do Excel separada por tabulações. AEM WCM pergunta onde deseja baixar o arquivo.

   >[!NOTE]
   >
   >Por padrão, as alterações são codificadas em [Windows-1252](https://en.wikipedia.org/wiki/Windows-1252) (também conhecido como CP-1252). Você pode verificar UTF-8 para exportar as alterações no UTF-8.

   ![](assets/srchrsesultexport.png)

1. Selecione o local e confirme que deseja baixar o arquivo.
1. Depois de baixar o arquivo, é possível abri-lo a partir do programa da planilha, por exemplo, do Microsoft Excel. O programa da planilha importa o arquivo e o converte em um formato de planilha.

   ![](assets/exportinexcel.png)

### Importando conteúdo {#importing-content}

Por padrão, a funcionalidade de importação fica oculta quando você abre o Editor de itens em massa. A simples adição do parâmetro `hib=false` ao URL exibirá o botão **Importar** na página do Editor em massa. Você pode importar conteúdo de qualquer arquivo separado por tabulação ( `.tsv`). Para que a importação funcione corretamente, os cabeçalhos de coluna (primeira linha de células) devem corresponder aos cabeçalhos de coluna da tabela para a qual você está importando.

>[!NOTE]
>
>Ao importar novamente o conteúdo, você apaga qualquer conteúdo anterior para esses nós. Tenha cuidado para não substituir informações importantes.

Para importar conteúdo:

1. Abra o Editor em massa.
1. Adicione `?hib=false` ao URL, por exemplo:
   `https://localhost:4502/etc/importers/bulkeditor.html?hib=false`
1. Clique em **Importar**.
1. Selecione o arquivo `.tsv`. Os dados são importados para o repositório.