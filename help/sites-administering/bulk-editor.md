---
title: O Editor de itens em massa
description: Saiba como usar o Editor de itens em massa.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: c63e044c-4d2a-44d3-853b-8e7337e1ee03
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 1%

---


# O Editor de itens em massa{#the-bulk-editor}

O Editor de itens em massa permite uma edição eficiente quando o contexto visual da página não é necessário, pois permite:

* pesquisar (e exibir) conteúdo de várias páginas; isso é feito usando o GQL (Google Query Language)
* editar este conteúdo diretamente no Editor de itens em massa
* salvar as alterações (nas páginas de origem)
* exportar este conteúdo para um arquivo de planilha separado por tabulação (.tsv)

>[!NOTE]
>
>Você também pode importar conteúdo para o repositório, mas, por padrão, isso está desativado para o Editor de itens em massa, conforme disponível na **Ferramentas** console.

Esta seção descreve como trabalhar com o Editor de itens em massa na **Ferramentas** console. Normalmente, os administradores usam o Editor de itens em massa para pesquisar e editar vários itens. Isso é feito preenchendo a tabela com uma consulta GQL e selecionando os itens de conteúdo nos quais trabalhar. Os autores geralmente usam o Editor de itens em massa como parte de um aplicativo personalizado do Editor de itens em massa acessível por meio do [lista de produtos](/help/sites-authoring/default-components.md#productlist) componente.

>[!CAUTION]
>
>Com o [desativação da interface clássica](/help/release-notes/deprecated-removed-features.md) no AEM 6.4, o Editor de itens em massa também foi descontinuado e, portanto, o Adobe não planeja aprimorar ainda mais o Editor de itens em massa.

## Exemplo de caso de uso para o editor de itens em massa {#example-use-case-for-the-bulk-editor}

Por exemplo, se você precisar de todos os nomes e endereços de email de usuários que preencheram uma pesquisa específica, o Editor de itens em massa poderá fornecer essas informações e você poderá exportá-las para uma planilha.

Um exemplo para ilustrar esse caso de uso está incluído no site do Geometrixx:

1. Navegue até a **Suporte** e, em seguida, para a **Satisfação do Atendimento ao Cliente** pesquisa.
1. **Editar** o **Início do formulário** parágrafo. Na caixa de diálogo, clique no link **Avançado** , expanda a **Configuração de ação** e, em seguida, clique em **Exibir Dados...**.

   ![Exemplo de pesquisa de satisfação do cliente](assets/custsatsurvey.png)

1. O Editor de itens em massa é totalmente personalizável, embora, neste exemplo, o Editor de itens em massa não permita que os usuários editem o conteúdo, apenas permita exportar as informações para uma planilha.

   ![Console do editor de itens em massa](assets/bulkeditor.png)

## Como usar o editor em massa {#how-to-use-the-bulk-editor}

O Editor de itens em massa permite:

* [pesquisar conteúdo com base em parâmetros de consulta, exibir propriedades especificadas dos resultados em colunas, editar este conteúdo e salvar as alterações](#searching-and-editing-content)
* [para exportar este conteúdo para uma planilha separada por tabulação](#exporting-content)

* [para importar conteúdo de uma planilha separada por tabulação](#importing-content)

### Pesquisar e editar conteúdo {#searching-and-editing-content}

Para usar o Editor de itens em massa para editar vários itens simultaneamente:

1. No **Ferramentas** clique no link **Importadores** pasta para expandi-la.
1. Clique duas vezes no ícone **Editor de itens em massa** para abri-lo.
1. Insira os requisitos de seleção:

<table>
 <tbody>
  <tr>
   <td>Texto</td>
   <td>Propriedade</td>
  </tr>
  <tr>
   <td>Caminho raiz</td>
   <td>Indica o caminho raiz que o Editor de itens em massa pesquisa.<br /> Por exemplo, <code>/content/geometrixx/en</code>. O Editor de itens em massa pesquisa em todos os nós filhos.</td>
  </tr>
  <tr>
   <td>Parâmetros de consulta</td>
   <td>Usando parâmetros GQL, insira a sequência de pesquisa que o Editor de itens em massa deve procurar no repositório; por exemplo, <code>type:Page</code> procura todas as páginas no caminho raiz, <code>text:professional</code> procura todas as páginas que contenham a palavra "profissional", e <code>"jcr:title":English</code> O procura todas as páginas cujo título seja "inglês". Você só pode pesquisar por cadeias de caracteres.</td>
  </tr>
  <tr>
   <td>Caixa de seleção Modo de conteúdo</td>
   <td>Marque esta caixa de seleção para ler as propriedades na <code>jcr:content</code> subnó dos resultados da pesquisa, se existir. Use somente para páginas. Os nomes de propriedades recebem o prefixo <code>"jcr:content/"</code></td>
  </tr>
  <tr>
   <td>Propriedades / Colunas</td>
   <td>Marque as caixas de seleção das propriedades que você deseja que o Editor de itens em massa retorne. As propriedades selecionadas são os cabeçalhos de coluna no painel de resultados. Por padrão, o caminho do nó é exibido nos resultados.</td>
  </tr>
  <tr>
   <td>Propriedades / Colunas personalizadas</td>
   <td>Insira quaisquer outras propriedades que não estejam listadas no <strong>Propriedades/Colunas</strong> campo. Essas propriedades personalizadas são exibidas no painel de resultados. É possível adicionar várias propriedades usando uma vírgula para separá-las. <i>Nota:</i> Se você adicionar uma propriedade personalizada que ainda não existe, o AEM WCM exibe uma célula vazia. Quando você modifica a célula vazia e a salva, a propriedade é adicionada ao nó. A propriedade recém-criada deve respeitar as restrições do tipo de nó e os namespaces de propriedade.</td>
  </tr>
 </tbody>
</table>

Por exemplo:

![Opções de filtro do editor de itens em massa](assets/searchfilter.png)

1. Clique em **Pesquisar**. O Editor de itens em massa exibe os resultados.
Para o exemplo acima, todas as páginas que atendem aos seus critérios de pesquisa são retornadas e exibidas com as colunas solicitadas.

   ![Resultados do editor em massa](assets/chlimage_1-39.png)

1. Faça as alterações necessárias clicando duas vezes em uma célula.

   ![Edição em massa](assets/srchresultedit.png)

1. Clique em **Salvar** para salvar as alterações (a variável **Salvar** será ativado assim que você editar uma célula).

   >[!CAUTION]
   >
   >As alterações feitas aqui são gravadas no conteúdo do repositório; por exemplo, a página referenciada em **Caminho**.

#### Parâmetros de consulta GQL adicionais {#additional-gql-query-parameters}

* **caminho:** pesquisar somente nós abaixo deste caminho. Se você especificar mais de um termo com um prefixo de caminho, somente o último será considerado.
* **tipo:** retorna somente nós dos tipos de nó fornecidos. Isso inclui os tipos primário e mixin. Você pode especificar vários tipos de nó separados por vírgula. O GQL retorna nós que sejam de qualquer um dos tipos especificados.
* **pedido:** ordenar o resultado pelas propriedades fornecidas. Você pode especificar vários nomes de propriedades separados por vírgulas. Para ordenar o resultado em ordem decrescente, basta adicionar um prefixo ao nome da propriedade com um sinal de menos. Por exemplo, order:-name. Usar um sinal de mais retorna o resultado em ordem crescente, que também é o padrão.
* **limite:** limita o número de resultados usando um intervalo. Por exemplo, limit:10..20 O intervalo é baseado em zero, start é inclusivo e end é exclusivo. Você também pode especificar um intervalo aberto:limit:10. ou limite:..20 Se os pontos forem omitidos e somente um valor for especificado, o GQL retornará no máximo esse número de resultados. Por exemplo, limit:10 (retorna os primeiros dez resultados).

### Exportar conteúdo {#exporting-content}

Talvez seja necessário exportar o conteúdo e alterá-lo em uma planilha do Excel. Por exemplo, você pode exportar uma lista de endereçamento e alterar o código de área de todos os números de telefone listados diretamente no Excel, ou adicionar linhas adicionais, e assim por diante.

Para exportar conteúdo:

1. Pesquise o conteúdo conforme descrito em [Pesquisar e editar conteúdo](#searching-and-editing-content).
1. Clique em **Exportar** para exportar as alterações para uma planilha do Excel separada por tabulação. O AEM WCM pergunta onde você deseja baixar o arquivo.

   >[!NOTE]
   >
   >Por padrão, as alterações são codificadas em [Windows-1252](https://en.wikipedia.org/wiki/Windows-1252) (também conhecido como CP-1252). Você pode verificar UTF-8 para exportar as alterações em UTF-8.

   ![Exportação de resultados](assets/srchrsesultexport.png)

1. Selecione o local e confirme se deseja baixar o arquivo.
1. Depois de baixar o arquivo, você pode abri-lo no seu programa de planilhas, por exemplo, Microsoft® Excel. O programa de planilha importa o arquivo e o converte em um formato de planilha.

   ![Resultados exportados em uma planilha](assets/exportinexcel.png)

### Importação de conteúdo {#importing-content}

Por padrão, a funcionalidade de importação fica oculta quando você abre o Editor de itens em massa. Basta adicionar o parâmetro `hib=false` para o URL exibe a variável **Importar** botão na página Editor de itens em massa. É possível importar conteúdo de qualquer arquivo separado por tabulação ( `.tsv`) arquivo. Para que a importação funcione corretamente, os cabeçalhos de coluna (primeira linha de células) devem corresponder aos cabeçalhos de coluna da tabela para a qual você está importando.

>[!NOTE]
>
>Ao reimportar o conteúdo, você apaga qualquer conteúdo anterior desses nós. Tenha cuidado para não sobregravar informações importantes.

Para importar conteúdo:

1. Abra o Editor de itens em massa.
1. Adicionar `?hib=false` ao URL, por exemplo:
   `https://localhost:4502/etc/importers/bulkeditor.html?hib=false`
1. Clique em **Importar**.
1. Selecione o `.tsv` arquivo. Os dados são importados para o repositório.
